---
title: 'What’s New In Next.js 13?'
slug: whats-new-nextjs-13
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48e8a36f-2bd6-4fdf-8a56-acec206c23c8/whats-new-nextjs-13.jpg
date: 2022-11-07T14:00:00.000Z
summary: >-
  Let’s talk about Next.js, one of the most well-known React frameworks used for production. From new components to font optimization, Atila shares a quick overview and invites you to join his [Advanced Next.js Masterclass](https://smashingconf.com/online-workshops/workshops/advanced-nextjs-atila-fassina) taking place later this month.
description: >-
  Let’s talk about Next.js, one of the most well-known React frameworks used for production. From new components to font optimization, Atila shares a quick overview and invites you to join his [Advanced Next.js Masterclass](https://smashingconf.com/online-workshops/workshops/advanced-nextjs-atila-fassina) taking place later this month.
categories:
  - Next.js
  - JavaScript
  - API
  - Coding
---

October has come and gone, and with it, Next.js has released a new major version packed (pun intended) with tons of new features &mdash; some of which can be seamlessly adopted from your Next.js 12 app, while others not so much.

If you’re just jumping on the bandwagon, it may be confusing to distinguish the hype, the misinformation, and what’s stable for your production apps, but fear not! I’m here to give you a nice overview and get you up to speed.

## What Misinformation?

As with all Next.js releases, there are a few APIs that are moved into the stable core and for recommended use, and there are others still in the experimental channel. “Experimental” APIs are still up for debate. The main functionality is there, but the question of **how these APIs behave and how they can be used** is still susceptible to change as there may be bugs or unexpected side effects.

In version 13, the experimental releases were big and took over the spotlight. This caused many people to consider the whole release unstable and experimental &mdash; but it’s not. Next.js 13 is actually quite stable and **allows for a smooth upgrade from version 12** if you don’t intend to adopt any experimental API. Most changes can be incrementally adopted, which we’ll get into detail later in this post.

## Releases Summary

Before we dig deeper into what each announcement entails, let’s check on a quick list and balance experiments and stable features.

#### Experimental

- App Directory;
- New Bundler (Turbopack);
- Font Optimization.

#### Stable

- “New” Image Component to replace legacy `Image` component as default;
- ES Module Support for `next.config.mjs`;
- “New” `Link` component.

## The App Directory

This feature is actually a big architectural rewrite. It puts React Server Components front and center, leverages a whole new routing system and router hooks (under `next/navigation` instead of `next/router`), and flips the entire data-fetching story.

This is all meant to enable big performance improvements, like eagerly rendering each part of your view which doesn’t depend on data while **suspending** (you read that right!) the pieces which are fetching data and getting rendered on the server.

As a consequence, this also brings a huge mental model change to how you architect your Next.js app.

{{% feature-panel %}}

Let’s compare how things were versus how they will work in the App directory. When using the `/pages` directory (the architecture we have been using up to now), data is fetched from the page level and is cascaded down toward the leaf components.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2baebac0-1cfe-4ca8-a180-d3828a764978/visualization-architecture-app-directory-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2baebac0-1cfe-4ca8-a180-d3828a764978/visualization-architecture-app-directory-feature.png" width="800" height="625" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2baebac0-1cfe-4ca8-a180-d3828a764978/visualization-architecture-app-directory-feature.png'>Large preview</a>)" alt="Visualization of the architecture of the App Directory feature" >}}

In contrast, given that the app directory is powered by Server Components, **each component is in charge of its own data**, meaning you can now *fetch-then-render* every component you need and cache them individually, performing [Incremental Static Regeneration (ISR)](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration) at a much more granular level.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647ff188-e91c-4864-9059-39f8455b1e61/visualization-fetch-then-render.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647ff188-e91c-4864-9059-39f8455b1e61/visualization-fetch-then-render.png" width="800" height="481" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647ff188-e91c-4864-9059-39f8455b1e61/visualization-fetch-then-render.png'>Large preview</a>)" alt="Visualization of how fetch-then-render works" >}}

Additionally, Next.js will carry on optimizations: Requests will be deduped (not allowing different components to fire the same request in parallel), thanks to a change in how the `fetch` runtime method works with the cache. By default, all requests will use strong cache heuristics (“force-cache”), which can be opted out via configuration.

<blockquote>You read it right. Next.js and React Server Components both interfere with the <code>fetch</code> standard in order to provide resource-fetching optimisations.</blockquote>

### You Don’t Need To Go "All-In"

It is important to point out that the transition from the `/pages` architecture to `/app` can be done incrementally, and both solutions can coexist as long as routes don’t overlap. There’s currently **no mention** in Next.js’ roadmap about deprecating support for `/pages`.

**Recommended Reading**: *[ISR vs DPR: Big Words, Quick Explanation](https://www.smashingmagazine.com/2021/07/isr-dpr-explained/) by Cassidy Williams*

## New Bundler And Benchmarks

Since its first release, Next.js has used [webpack](https://webpack.js.org/) under the hood. This year, we have watched a new generation of bundlers, written in low-level languages, popping up, such as ESBuild (which powers Vite), Parcel 2 (Rust), and others. We have also watched Vercel setting the stage for a big change in Next.js. In version 12, they added [SWC](https://swc.rs/) to their build and transpilation process as a step to replacing both [Babel](https://babeljs.io/) and [Terser](https://github.com/terser/terser).  

In version 13, they announced Turbopack, a new bundler written in Rust with very [bold performance claims](https://nextjs.org/blog/next-13#introducing-turbopack-alpha). Yes, there has been controversy on Twitter about which bundler is the fastest overall and how those benchmarks were measured. Still, it’s beyond debate how much Turbopack can actually help large projects written in Next.js with way better ergonomics than any other tool (for starters, with built-in configuration).

<blockquote>This feature is not only experimental but actually only works with <code>next dev</code>. You should not (and as of now <strong> can’t </strong>) use it for a production build.</blockquote>

{{% ad-panel-leaderboard %}}

## Font Optimization

The new `@next/font` module allows making performance optimization to your Web Fonts during build time. It will download the font assets during build-time and host them in your very own `/public` folder. This will save a round-trip to a further server, avoid an additional handshake, and ultimately deliver your font in the fastest way possible and cache it properly with the rest of your resources.

Remember that when using this package, the it's important to have a working internet connection when you run your development build the first time so it can cache it properly, otherwise it will fallback to system fonts if [`adjustFontFallback` is not set](https://nextjs.org/docs/api-reference/next/font#adjustfontfallback).

Additionally, `@next/font` has a special module for Google Web Fonts, conveniently available as they are widely used:

<pre><code class="language-javascript">import { Jost } from '@next/font/google';
// get an object with font styles:
const jost = Jost();
// define them in your component:
&lt;html className={jost.className}&gt;
</code></pre>

The module will also work in case you use custom fonts:

<pre><code class="language-javascript">import localFont from '@next/font/local';
</code></pre>

<pre><code class="language-javascript">const myFont = localFont({ src: './my-font.woff2' });
</code></pre>

<pre><code class="language-javascript">&lt;html className={myFont.className}&gt;
</code></pre>

Even though this feature is still in Beta, it is considered stable enough for you to use in production.

## New Image And Link Components

Arguably the most important components within the Next.js package have received a slight overhaul. Next `Image` has been living a double life since Next.js 12 in `@next/image` and `@next/future/image`. In Next.js 13, the default component is switched:

- `next/image` moves to `next/legacy/image`;
- `next/future/image` moves to `next/image`.

This change comes with a codemod, a command that attempts to automigrate the code in your app. This allows for a smooth migration when upgrading Next.js:

<pre><code class="language-bash">npx @next/codemod next-image-to-legacy-image ./pages
</code></pre>

If you make this change and do not have visual regression tests set up, I'd recommend taking a good look at your pages in every major browser to see if everything looks correct.

For the new Link component, the change should also be smooth. The `<a>` element within `<Link>` is not necessary *nor recommended* anymore. The codemod will either remove it or add a `legacyBehavior` prop to your component.

<pre><code class="language-bash">npx @next/codemod new-link ./pages
</code></pre>

In case the codemod fails, you will receive a linting warning on dev, so keep an eye on your terminal!

## ES Modules and Automatic Module Transpilation

There two upgrades have passed under the radar for most, but I consider them **especially useful for people working with Monorepos**. Up until now, it was not very ergonomic to share configuration between configuration files and other files that may be used in runtime. That’s because `next.config.js` is written with CommonJS as the module system, which can't import from ESM files. Now, Next.js supports ESM simply by adding `type: "module"` to your `package.json` and renaming `next.config.js` → `next.config.mjs`.

**Note**: *The “m” stands for “module” and is part of the Node.js spec for ESM support.*

For Monorepos using internal packages (JavaScript packages that are not published to NPM but instead are consumed from source by sibling apps within the monorepo), a special plugin was necessary to transpile those modules on build-time when consuming them. From Next.js 13 onwards, **this can be arranged without a plugin** by simply passing an (experimental) property to your `next.config.mjs`:

<pre><code class="language-javascript">const nextConfig = {
  experimental: {
    transpilePackages: ['@my-org/internal-package'],
  },
};
</code></pre>

You can see an example in the [Apex-Monorepo template](https://github.com/atilafassina/apex-monorepo/blob/main/apps/web/next.config.mjs#L8). With these settings, it is possible to develop both the dependency component and your app simultaneously without any publishing or workaround.

## What’s *Next*?

If you’re still interested in playing around and talking more about these features, I’ll be running a [Advanced Next.js Masterclass](https://smashingconf.com/online-workshops/workshops/advanced-nextjs-atila-fassina) from Nov 30 &ndash; Dec 15, 2022 &mdash; I’d be super happy to welcome you there and answer all of your questions!

{{< rimg href="https://smashingconf.com/online-workshops/workshops/advanced-nextjs-atila-fassina" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3109fc33-fce0-412e-99c2-da019c2eb6bb/workshops-advanced-nextjs-atila-fassina.png" width="800" height="428" sizes="100vw" caption="" alt="Smashing Workshop by Atila Fassina" >}}

Until then, let me know in the comments below or tweet over to me at [@AtilaFassina](https://atila.io/twitter) on how your migration has been and your thoughts on the experimental features.

{{% ad-panel-leaderboard %}}

{{< signature "vf, yk, il" >}}
