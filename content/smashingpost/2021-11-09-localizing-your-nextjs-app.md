---
title: 'Localizing Your Next.js App'
slug: localizing-your-nextjs-app
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12e7620f-0e7b-4b95-a1b6-cd2f25ccac52/localizing-your-nextjs-app.jpg
date: 2021-11-09T13:00:00.000Z
summary: >-
  Internationalized routing is not exactly a new feature on Next.js. (It has been out since [v.10](https://nextjs.org/blog/next-10).) In this article, we are not only checking what we get from this feature, but also how to leverage such functionalities to achieve the best user experience and a smooth developer experience as well. Keep reading if you enjoy self-documented code, lean bundle-sizes and compile-time errors instead of runtime errors.
description: >-
  Internationalized routing is not exactly a new feature on Next.js. In this article, we are not only checking what we get from this feature, but also how to leverage such functionalities to achieve the best user experience and a smooth developer experience as well.
categories:
  - Apps
  - Next.js
  - User Experience
---

Instructing Next.js your app intends to have routes for different locales (or countries, or both) could not be more smooth. On the root of your project, create a `next.config.js` if you have not had the need for one. You can copy from this snippet.

<pre><code class="language-javascript">/** @type {import('next').NextConfig} */

module.exports = {
  reactStrictMode: true,
  i18n: {
    locales: ['en', 'gc'],
    defaultLocale: 'en',
  }
}</code></pre>

**Note**: *The first line is letting the TS Server (if you are on a TypeScript project, or if you are using VSCode) which are the properties supported in the configuration object. It is not mandatory but definitely a nice feature.*

You will note two property keys inside the `i18n` object:

- `locales`  
A list of all locales supported by your app. It is an `array` of `strings`.
- `defaultLocale`  
The locale of your main root. That is the default setting when either no preference is found or you forcing to the root.

Those property values will determine the routes, so do not go too fancy on them. Create valid ones using [locale code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) and/or [country codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) and stick with lower-case because they will generate a `url` soon.

Now your app has multiple locales supported there is one last thing you must be aware of in Next.js. Every route now exists on every locale, and the framework is aware they are the same. If you want to navigate to a specific locale,  we must provide a `locale` prop to our `Link` component, otherwise, it will fall back based on the browser’s `Accept-Language` header.

<pre><code class="language-javascript">&lt;Link href="/" locale="de"&gt;&lt;a&gt;Home page in German&lt;/a&gt;&lt;/Link&gt;</code></pre>

Eventually, you will want to write an anchor which will just obey the selected locale for the user and send them to the appropriate route. That can easily be achieved with the `useRouter` custom hook from Next.js, it will return you an `object` and the selected `locale` will be a `key` in there.

<pre><code class="language-javascript">import type { FC } from 'react'
import Link from 'next/link'
import { useRouter } from 'next/router'

const Anchor: FC&lt;{ href: string }&gt; = ({ href, children }) =&gt; {
  const { locale } = useRouter()

  return (
    &lt;Link href={href} locale={locale}&gt;
      &lt;a&gt;{children}&lt;/a&gt;
    &lt;/Link&gt;
  )
}</code></pre>

Your Next.js is now fully prepared for internationalization. It will:

- Pick up the user’s preferred locale from the `Accepted-Languages` header in our request: courtesy of Next.js;
- Send the user always to a route obeying the user’s preference: using our `Anchor` component created above;
- Fall back to the default language when necessary.

The last thing we need to do is make sure we can handle translations. At the moment, routing is working perfectly, but there is no way to adjust the content of each page.

{{% feature-panel %}}

## Creating A Dictionary

Regardless if you are using a Translation Management Service or getting your texts some other way, what we want in the end is a JSON object for our JavaScript to consume during runtime. Next.js offers three different runtimes:

- client-side,
- server-side,
- compile-time.

But keep that at the back of your head for now. We’ll first need to structure our data.

Data for translation can vary in shape depending on the tooling around it, but ultimately it eventually boils down to locales, keys, and values. So that is what we are going to get started with. My locales will be `en` for English and `pt` for Portuguese.

<pre><code class="language-javascript">module.exports = {
  en: {
    hello: 'hello world'
  },
  pt: {
    hello: 'oi mundo'
  }
}</code></pre>

## Translation Custom Hook

With that at hand, we can now create our translation custom hook. 

<pre><code class="language-javascript">import { useRouter } from 'next/router'
import dictionary from './dictionary'

export const useTranslation = () =&gt; {
  const { locales = [], defaultLocale, ...nextRouter} = useRouter()
  const locale = locales.includes(nextRouter.locale || '')
    ? nextRouter.locale
    : defaultLocale
  
  return {
    translate: (term) =&gt; {
      const translation = dictionary[locale][term]

      return Boolean(translation) ? translation : term
    }
  }
}</code></pre>

Let’s breakdown what is happening upstairs:

1. We use `useRouter` to get all available locales, the default one, and the current;
2. Once we have that, we check if we have a valid locale with us, if we do not: fallback to the default locale;
3. Now we return the `translate` method. It takes a `term` and fetches from the dictionary to that specified locale. If there is no value, it returns the translation `term` again.

Now our Next.js app is ready to translate at least the more common and rudimentary cases. Please note, this is not a dunk on translation libraries. There are **tons of important features** our custom hook over there is missing: interpolation, pluralization, genders, and so on.

{{% ad-panel-leaderboard %}}

## Time To Scale

The lack of features to our custom hook is acceptable if we do not need them right now; it is always possible (and arguably better) to implement things when you actually need them. But there is one fundamental issue with our current strategy that is worrisome: it is not leveraging the isomorphic aspect of Next.js.

The worst part of scaling localized apps is not managing the translation actions themselves. That bit has been done quite a few times and is somewhat predictable. The problem is dealing with the bloat of shipping endless dictionaries down the wire to the browser &mdash; and they only multiply as your app requires more and more languages. That is data that very often becomes useless to the end-user, or it affects performance if we need to fetch new keys and values when they switch language. If there is one big truth about user experience, it’s this: your users will surprise you. 

We cannot predict *when* or *if* users will switch languages or need that additional key. So, ideally, our apps will have all translations for a specific route at hand when such a route is loaded. For now, we need to split chunks of our dictionary based on what the page renders, and what permutations of state it can have. This rabbit hole goes deep.

## Server-Side Pre-Rendering

Time to recap our new requirements for scalability:

1. Ship as little as possible to the client-side;
2. Avoid extra requests based on user interaction;
3. Send the first render already translated down to the user.

Thanks to the `getStaticProps` method of Next.js pages, we can achieve that without needing to dive at all into compiler configuration. We will import our entire dictionary to this special Serverless Function, and we will send to our page a list of special objects carrying the translations of each key.

## Setting Up SSR Translations

Back to our app, we will create a new method. Set a directory like `/utils` or `/helpers` and somewhere inside we will have the following:

<pre><code class="language-javascript">export function ssrI18n(key, dictionary) {
  return Object.keys(dictionary)
    .reduce((keySet, locale) =&gt; {
      keySet[locale] = (dictionary[locale as keyof typeof dictionary][key])
      return keySet
    , {})
}</code></pre>

Breaking down what we are doing:

1. Take the translation `key` or `term` and the `dictionary`;
2. Turn the `dictionary` object into an array of its `keys`;
3. Each key from the dictionary is a `locale`, so we create an object with the `key` name and each `locale` will be the value for that specific language.

An example output of that method will have the following shape:

<pre><code class="language-javascript">{
  'hello': {
    'en': 'Hello World',
    'pt': 'Oi Mundo',
    'de': 'Hallo Welt'
  }
}</code></pre>

Now we can move to our Next.js page.

<pre><code class="language-javascript">import { ssrI18n } from '../utils/ssrI18n'
import { DICTIONARY } from '../dictionary'
import { useRouter } from 'next/router'

const Home = ({ hello }) =&gt; {
  const router = useRouter()
  const i18nLocale = getLocale(router)

  return (
    &lt;h1 className={styles.title}&gt;
      {hello[i18nLocale]}
    &lt;/h1&gt;
  )
}

export const getStaticProps = async () =&gt; ({
  props: {
    hello: ssrI18n('hello', DICTIONARY),
    // add another entry to each translation key
  }
})</code></pre>

And with that, we are done! Our pages are only receiving exactly the translations they will need in every language. No external requests if they switch languages midway, on the contrary: the experience will be super quick.

{{% ad-panel-leaderboard %}}

## Skipping All Setup

All that is great, but we can still do better for ourselves. The developer could take some attention; there is a lot of bootstrapping in it, and we are still relying on not making any typos. If you ever worked on translated apps, you’ll know that there will be a mistyped key somewhere, somehow. So, we can bring the type-safety of TypeScript to our translation methods.

To skip this setup *and* get the TypeScript safety and autocompletion, we can use [`next-g11n`](https://github.com/atilafassina/next-g11n). This is a tiny library that does exactly what we have done above, but adds types and a few extra bells and whistles.

## Wrapping Up

I hope this article has given you a larger insight into what [Next.js Internationalized Routing](https://nextjs.org/docs/advanced-features/i18n-routing) can do for your app to achieve Globalization, and what it means to provide a top-notch user experience in localized apps in today’s web. Let hear what you think in the comments below, or send a [tweet](https://atila.io/twitter) my way.

{{< signature "vf, yk, il" >}}
