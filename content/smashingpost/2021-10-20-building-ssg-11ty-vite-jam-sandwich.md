---
title: 'Building The SSG I’ve Always Wanted: An 11ty, Vite And JAM Sandwich'
slug: building-ssg-11ty-vite-jam-sandwich
author: ben-holmes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ff6275f-bf33-480f-bdd4-690e94f96314/building-ssg-11ty-vite-jam-sandwich.jpg
date: 2021-10-20T11:00:00.000Z
summary: >-
  Back in January 2020, Ben Holmes set out to do what just about every web developer does each year: rebuild his personal site. In this article, he shares his story of how he set out to build his own build pipeline from absolute ground zero and created [Slinkity](https://slinkity.dev/).
description: >-
  Back in January 2020, Ben Holmes set out to do what just about every web developer does each year: rebuild his personal site. In this article, he shares his story of how he set out to build his own build pipeline from absolute ground zero and created “Slinkity”.
categories:
  - Tools
  - Generators
  - Static Generators
  - Eleventy
---

I don’t know about you, but I’ve been *overwhelmed* by all the web development tools we have these days. Whether you like Markdown, plain HTML, React, Vue, Svelte, Pug templates, Handlebars, Vibranium &mdash; you can probably mix it up with some CMS data and get a nice static site cocktail.

I’m not going to tell you which UI development tools to reach for because they’re all great &mdash; depending on the needs of your project. This post is about finding the perfect static site generator for *any* occasion; something that lets us use JS-less templates like markdown to start, and bring in “islands” of component-driven interactivity as needed.

I’m distilling a year’s worth of learnings into a single post here. Not only are we gonna talk code (aka duct-taping 11ty and Vite together), but we’re also going to explore *why* this approach is so universal to Jamstackian problems. We’ll touch on:

- Two approaches to static site generation, and why we should bridge the gap;
- Where templating languages like Pug and Nunjucks still prove useful;
- When component frameworks like React or Svelte should come into play;
- How the new, hot-reloading world of Vite helps us bring JS interactivity to our HTML with almost zero configs;
- How this complements 11ty’s data cascade, bringing CMS data to any component framework or HTML template you could want.

So without further ado, here’s my tale of terrible build scripts, bundler breakthroughs, and spaghetti-code-duct-tape that (eventually) gave me the SSG I always wanted: an 11ty, Vite and Jam sandwich called [Slinkity](https://slinkity.dev)!

## A Great Divide In Static Site Generation

Before diving in, I want to discuss what I’ll call two “camps” in static site generation. 

In the first camp, we have the **“simple” static site generator.** These tools don’t bring JavaScript bundles, single-page apps, and any other buzzwords we’ve come to expect. They just nail the Jamstack fundamentals: pull in data from whichever JSON blob of CMS you prefer, and slide that data into plain HTML templates + CSS. Tools like Jekyll, Hugo, and 11ty dominate this camp, letting you turn a directory of markdown and [liquid](https://shopify.github.io/liquid/) files into a fully-functional website. Key benefits:

- **Shallow learning curve**  
If you know HTML, you’re good to go!
- **Fast build times**  
We’re not processing anything complex, so each route builds in a snap.
- **Instant time to interactive**  
There’s no (or very little) JavaScript to parse on the client.

Now in the second camp, we have the **“dynamic” static site generator.** These introduce component frameworks like React, Vue, and Svelte to bring interactivity to your Jamstack. These fulfill the same core promise of combining CMS data with your site’s routes at build time. Key benefits:

- **Built for interactivity**  
Need an animated image carousel? Multi-step form? Just add a componentized nugget of HTML, CSS, and JS.
- **State management**  
Something like React Context of Svelte stores allow seamless data sharing between routes. For instance, the cart on your e-commerce site.

There are distinct pros to either approach. But what if you choose an SSG from the first camp like Jekyll, only to realize six months into your project that you need some component-y interactivity? Or you choose something like NextJS for those powerful components, only to struggle with the learning curve of React, or needless KB of JavaScript on a static blog post?

Few projects *squarely* fit into one camp or the other in my opinion. They exist on a spectrum, constantly favoring new feature sets as a project’s needs evolve. So how do we find a solution that lets us *start* with the simple tools of the first camp, and gradually add features from the second when we need them?

Well, let’s walk through my learning journey for a bit.

**Note:** *If you’re already sold on static templating with 11ty to build your static sites, feel free to [hop down to the juicy code walkthrough](#11ty-vite-a-match-made-in-heaven).* 😉

{{% feature-panel %}}

## Going From Components To Templates And Web APIs

Back in January 2020, I set out to do what just about every web developer does each year: rebuild my personal site. But this time was gonna be *different.* I challenged myself to build a site with my hands tied behind my back, **no frameworks or build pipelines allowed!**

This was no simple task as a React devotee. But with my head held high, I set out to build my own build pipeline from absolute ground zero. There’s a lot of poorly-written code I *could* share from v1 of my personal site... but I’ll let you [click this README](https://github.com/Holben888/bholmesdev/tree/v1) if you’re so brave. 😉 Instead, I want to focus on the higher-level takeaways I learned starving myself of my JS guilty pleasures.

### Templates Go A Lot Further Than You Might Think

I came at this project a recovering JavaScript junky. There are a few static-site-related needs I loved using component-based frameworks to fill:

1. **We want to break down my site into reusable UI components** that can accept JS objects as parameters (aka “props”).
2. **We need to fetch some information at build time** to slap into a production site.
3. **We need to generate a bunch of URL routes** from either a directory of files or a fat JSON object of content.

*List taken from [this post](https://bholmes.dev/blog/before-building-your-next-static-site-with-react-consider-this/) on my personal blog.*

But you may have noticed... none of these *really* need clientside JavaScript. Component frameworks like React are mainly built to handle state management concerns, like the Facebook web app inspiring React in the first place. If you’re just breaking down your site into bite-sized components or design system elements, templates like Pug work pretty well too!

Take this navigation bar for instance. In Pug, we can define a “mixin” that receives data as props:

<pre><code class="language-javascript">// nav-mixins.pug
mixin NavBar(links)
    // pug's version of a for loop
    each link in links
        a(href=link.href) link.text</code></pre>

Then, we can apply that mixin anywhere on our site.

<pre><code class="language-javascript">// index.pug
// kinda like an ESM "import"
include nav-mixins.pug
html
  body
    +NavBar(navLinksPassedByJS)
    main
      h1 Welcome to my pug playground 🐶</code></pre>

If we “render” this file with some data, we’ll get a beautiful `index.html` to serve up to our users.

<pre><code class="language-javascript">const html = pug.render('/index.pug', { navLinksPassedByJS: [
    { href: '/', text: 'Home' },
    { href: '/adopt', text: 'Adopt a Pug' }
] })
// use the NodeJS filesystem helpers to write a file to our build
await writeFile('build/index.html', html)</code></pre>

Sure, this doesn’t give niceties like scoped CSS for your mixins, or stateful JavaScript where you want it. But it has some very powerful benefits over something like React:

1. **We don’t need fancy bundlers we don’t understand.**  
We just wrote that `pug.render` call by hand, and we already have the first route of a site ready-to-deploy.
3. **We don’t ship any JavaScript to the end-user.**  
Using React often means sending a big ole runtime for people’s browsers to run. By calling a function like `pug.render` at build time, we keep all the JS on our side while sending a clean `.html` file at the end.

This is why I think templates are a great “base” for static sites. Still, being able to reach for component frameworks where we *really* benefit from them would be nice. More on that later. 🙃

**Recommended Reading**: [*How To Create Better Angular Templates With Pug*](https://www.smashingmagazine.com/2020/05/angular-templates-pug/) by Zara Cooper

### You Don’t Need A Framework To Build Single Page Apps

While I was at it, I also wanted some sexy page transitions on my site. But how do we pull off something like this without a framework?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cfcdeb4-7d7f-4261-a55b-8ba45d0a5c02/page-transitions.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cfcdeb4-7d7f-4261-a55b-8ba45d0a5c02/page-transitions.gif" width="589" height="385" alt="Crossfade with vertical wipe transition" /></a><figcaption>Crossfade with vertical wipe transition. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cfcdeb4-7d7f-4261-a55b-8ba45d0a5c02/page-transitions.gif">Large preview</a>)</figcaption></figure>

Well, we can’t do this if every page is its own `.html` file. The whole browser refreshes when we jump from one HTML file to the other, so we can’t have that nice cross-fade effect (since we’d briefly show both pages on top of each other).

We need a way to “fetch” the HTML and CSS for wherever we’re navigating to, and animate it into view using JavaScript. This sounds like a job for single-page apps!
I used a simple browser API medley for this:

1. Intercept all your link clicks using an event listener.
2. [**fetch API**](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)**:** Fetch all the resources for whatever page you want to visit, and grab the bit I want to animate into view: the content outside the navbar (which I want to remain stationary during the animation).
3. [**web animations API**](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API)**:** Animate the new content into view as a keyframe.
4. [**history API**](https://developer.mozilla.org/en-US/docs/Web/API/History_API)**:** Change the route displaying in your browser’s URL bar using `window.history.pushState({}, 'new-route')`. Otherwise, it looks like you never left the previous page!

For clarity, here’s a visual illustration of that single page app concept using a simple find-and-replace ([*source article*](https://bholmes.dev/blog/spas-clientside-routing/)):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a013427d-89c6-423f-9f22-fb5add5b69a6/1-building-ssg-11ty-vite-jam-sandwich.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a013427d-89c6-423f-9f22-fb5add5b69a6/1-building-ssg-11ty-vite-jam-sandwich.gif" width="800" height="629" alt="Step-by-step clientside routing process: 1. Medium rare hamburger is returned, 2. We request a well done burger using the fetch API, 3. We massage the response, 4. We pluck out the 'patty' element and apply it to our current page." /></a><figcaption>Step-by-step clientside routing process: 1. Medium rare hamburger is returned, 2. We request a well done burger using the fetch API, 3. We massage the response, 4. We pluck out the 'patty' element and apply it to our current page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a013427d-89c6-423f-9f22-fb5add5b69a6/1-building-ssg-11ty-vite-jam-sandwich.gif">Large preview</a>)</figcaption></figure>

**Note**: *You can also [visit the source code](https://github.com/Holben888/bholmesdev/blob/v1/src/routes/_layout/client.js#L80-L96) from my personal site.*

Sure, some pairing of React et al and your animation library of choice can do this. But for a use case as simple as a fade transition... web APIs are pretty dang powerful on their own. And if you want more robust page transitions on static templates like Pug or plain HTML, libraries like [Swup](https://swup.js.org) will serve you well.

## What 11ty Brought To The Table

I was feeling pretty good about my little SSG at this point. Sure it couldn’t fetch any CMS data at build-time, and didn’t support different layouts by page or by directory, and didn’t optimize my images, and didn’t have incremental builds.

Okay, I might need some help.

Given all my learnings from v1, I thought I earned my right to drop the “no third-party build pipelines” rule and reach for existing tools. Turns out, 11ty has a treasure trove of features I need!

- [Data fetching at buildtime](https://www.11ty.dev/docs/data-template-dir/) using `.11ydata.js` files;
- [Global data](https://www.11ty.dev/docs/data-global/) available to *all* my templates from a `_data` folder;
- [Hot reloading](https://www.11ty.dev/docs/usage/#re-run-eleventy-when-you-save) during development using browsersync;
- Support for [fancy HTML transforms](https://www.11ty.dev/docs/config/#transforms);
- ...and countless other goodies.

If you’ve tried out bare-bones SSGs like Jekyll or Hugo, you should have a pretty good idea of how 11ty works. Only difference? 11ty uses JavaScript through-and-through.

11ty supports basically every template library out there, so it was happy to render all my Pug pages to `.html` routes. It’s layout chaining option helped with my faux-single-page-app setup too. I just needed a single `script` for all my routes, and a “global” layout to import that script:

<pre><code class="language-javascript">// _includes/base-layout.html
&lt;html&gt;
&lt;body&gt;
  &lt;!--load every page's content between some body tags--&gt;
  {{ content }}
  &lt;!--and apply the script tag just below this--&gt;
  &lt;script src="main.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;

// random-blog-post.pug
---
layout: base-layout
---

article
  h2 Welcome to my blog
  p Have you heard the story of Darth Plagueis the Wise?</code></pre>

As long as that `main.js` does all [that link intercepting we explored](#you-don-t-need-a-framework-to-build-single-page-apps), we have page transitions!

{{% ad-panel-leaderboard %}}

### Oh, And The Data Cascade

So 11ty helped clean up all my spaghetti code from v1. But it brought another important piece: **a clean API to load data into my layouts.** This is the bread and butter of the [Jamstack](https://jamstack.org/what-is-jamstack/) approach. Instead of fetching data in the browser with JavaScript + DOM manipulation, you can:

1. **Fetch data at build-time using Node.**  
This could be a call to some external API, a local JSON or YAML import, or even [the content of *other routes* on your site](https://www.11ty.dev/docs/collections/) (imagine updating a table-of-contents whenever new routes are added 🙃).
2. Slot that data into your routes. Recall that `.render` function we wrote earlier:

<pre><code class="language-javascript">const html = pug.render('/index.pug', { navLinksPassedByJS: [
    { href: '/', text: 'Home' },
    { href: '/adopt', text: 'Adopt a Pug' }
] })</code></pre>

...but instead of calling `pug.render` with our data every time, we let 11ty do this behind-the-scenes.

Sure, I didn’t have a lot of data for my personal site. But it felt great to whip up a `.yaml` file for all my personal projects:

<pre><code class="language-javascript"># _data/works.yaml
- title: Bits of Good Homepage
  hash: bog-homepage
  links:
    - href: https://bitsofgood.org
      text: Explore the live site
    - href: https://github.com/GTBitsOfGood/bog-web
      text: Scour the Svelt-ified codebase
  timeframe: May 2019 - present
  tags:
    - JAMstack
    - SvelteJS
- title: Dolphin Audio Visualizer
...</code></pre>

And access that data across any template:

<pre><code class="language-javascript">// home.pug
.project-carousel
  each work in works
    h3 #{title}
    p #{timeframe}
    each tag in tags
    ...</code></pre>

Coming from the world of “[clientside rendering](https://www.applozic.com/blog/right-way-to-render-your-jamstack-site/)” with [create-react-app](https://create-react-app.dev), this was a pretty big revelation. No more sending API keys or big JSON blobs to the browser. 😁

I also added some goodies for JavaScript fetching and animation improvements over version 1 of my site. If you’re curious, here’s [where my README stood](https://github.com/Holben888/bholmesdev#readme) at this point.

## I Was Happy At This Point But Something Was Missing

I went surprisingly far by abandoning JS-based components and embracing templates (with animated page transitions to boot). But I know this won’t satisfy my needs forever. Remember that great divide I kicked us off with? Well, there’s clearly still that ravine between my build setup (firmly in camp #1) and the haven of JS-ified interactivity (the Next, SvelteKit, and more of camp #2). Say I want to add:

- a pop-up modal with an open/close toggle,
- a component-based design system like [Material UI](https://material-ui.com), complete with scoped styling,
- a complex multi-step form, maybe driven by [a state machine](https://xstate.js.org/docs/).

If you’re a plain-JS-purist, you probably have framework-less answers to all those use cases. 😉  But there’s a reason JQuery isn’t the norm anymore! There’s something appealing about creating discrete, easy-to-read components of HTML, scoped styles, and pieces of JavaScript “state” variables. React, Vue, Svelte, etc. offer so many niceties for debugging and testing that straight DOM manipulation can’t quite match.

So here’s my million dollar question:

<blockquote>Can we use straight HTML templates to start, and gradually add React/Vue/Svelte components where we want them?</blockquote>

The answer is *yes*. Let’s try it.

## 11ty + Vite: A Match Made In Heaven ❤️

Here's the dream that I’m imagining here. Wherever I want to insert something interactive, I want to leave a little flag in my template to “put X React component here.” This could be the [shortcode syntax](https://www.11ty.dev/docs/shortcodes/) that 11ty supports:

<pre><code class="language-javascript"># Super interesting programming tutorial

Writing paragraphs has been fun, but that's no way to learn. Time for an interactive code example!

{% react './components/FancyLiveDemo.jsx' %}</code></pre>

But remember, the one-piece 11ty (purposely) avoids: a way to bundle all your JavaScript. Coming from the OG guild of bundling, your brain probably jumps to building Webpack, Rollup, or Babel processes here. Build a big ole entry point file, and output some beautiful optimized code right?

Well yes, but this can get pretty involved. If we’re using React components, for instance, we’ll probably need some loaders for JSX, a fancy Babel process to transform everything, an interpreter for SASS and CSS module imports, *something* to help with live reloading, and so on.

If only there were a tool that could just see our `.jsx` files and know exactly what to do with them.

### Enter: Vite

[Vite](https://vitejs.dev)’s been the talk of the town as of late. It’s meant to be the all-in-one tool for building just about anything in JavaScript. Here’s an example for you to try at home. Let’s make an empty directory somewhere on our machine and install some dependencies:

<pre><code class="language-bash">npm init -y # Make a new package.json with defaults set
npm i vite react react-dom # Grab Vite + some dependencies to use React</code></pre>

Now, we can make an `index.html` file to serve as our app’s “entry point.” We’ll keep it pretty simple:

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;Hello Vite! (wait is it pronounced "veet" or "vight"...)&lt;/h1&gt;
  &lt;div id="root"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

The only interesting bit is that `div id="root"` in the middle. This will be the root of our React component in a moment!

If you want, you can fire up the Vite server to see our plain HTML file in your browser. Just run `vite` (or `npx vite` if the command didn’t get configured in your terminal), and you’ll see this helpful output:

<pre><code class="language-javascript">vite vX.X.X dev server running at:

> Local: http://localhost:3000/
> Network: use `--host` to expose

ready in Xms.</code></pre>

Much like Browsersync or other popular dev servers, the name of each `.html` file corresponds to a route on our server. So if we renamed `index.html` to `about.html`, we would visit `http://localhost:3000/about/` (yes, you’ll need a trailing slash!)

Now let’s do something interesting. Alongside that `index.html` file, add a basic React component of some sort. We’ll use React’s `useState` here to demonstrate interactivity:

<pre><code class="language-javascript">// TimesWeMispronouncedVite.jsx
import React from 'react'

export default function TimesWeMispronouncedVite() {
  const [count, setCount] = React.useState(0)
  return (
    &lt;div&gt;
      &lt;p&gt;I've said Vite wrong {count} times today&lt;/p&gt;
      &lt;button onClick={() =&gt; setCount(count + 1)}&gt;Add one&lt;/button&gt;
    &lt;/div&gt;
  )
}</code></pre>

Now, let’s load that component onto our page. This is all we have to add to our `index.html`:

<pre><code class="language-html">&lt;!DOCTYPE html>
...
&lt;body>
  &lt;h1&gt;Hello Vite! (wait is it pronounced "veet" or "vight"...)&lt;/h1&gt;
  &lt;div id="root"&gt;&lt;/div&gt;
  &lt;!--Don't forget type="module"! This lets us use ES import syntax in the browser--&gt;
  &lt;script type="module"&gt;
    // path to our component. Note we still use .jsx here!
    import Component from './TimesWeMispronouncedVite.jsx';
    import React from 'react';
    import ReactDOM from 'react-dom';
    const componentRoot = document.getElementById('root');
    ReactDOM.render(React.createElement(Component), componentRoot);
  &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

Yep, that’s it. No need to transform our `.jsx` file to a browser-ready `.js` file ourselves! Wherever Vite sees a `.jsx` import, it’ll auto-convert that file to something browsers can understand. There isn’t even a `dist` or `build` folder when working in development; Vite processes everything on the fly &mdash; complete with hot module reloading every time we save our changes. 🤯

Okay, so we have an incredibly capable build tool. How can we bring this to our 11ty templates?

### Running Vite Alongside 11ty

Before we jump into the good stuff, let’s discuss running 11ty and Vite side-by-side. Go ahead and install 11ty as a dev dependency into the same project directory from last section:

<pre><code class="language-bash">npm i -D @11ty/eleventy # yes, it really is 11ty twice</code></pre>

Now let’s do a little pre-flight check to see if 11ty’s working. To avoid any confusion, I’d suggest you:

1. Delete that `index.html` file from earlier;
2. Move that `TimesWeMispronouncedVite.jsx` inside a new directory. Say, `components/`;
3. Create a `src` folder for our website to live in;
4. Add a template to that `src` directory for 11ty to process.

For example, a `blog-post.md` file with the following contents:

<pre><code class="language-html"># Hello world! It’s markdown here</code></pre>

Your project structure should look something like this:

<pre><code class="language-bash">src/
  blog-post.md
components/
  TimesWeMispronouncedVite.jsx</code></pre>

Now, run 11ty from your terminal like so:

<pre><code class="language-bash">npx eleventy --input=src</code></pre>

If all goes well, you should see an build output like this:

<pre><code class="language-bash">_site/
  blog-post/
    index.html</code></pre>

Where `_site` is our default output directory, and `blog-post/index.html` is our markdown file beautifully converted for browsing.

Normally, we’d run `npx eleventy --serve` to spin up a dev server and visit that `/blog-post` page. But we’re using Vite for our dev server now! The goal here is to:

1. Have eleventy build our markdown, Pug, nunjucks, and more to the `_site` directory.
2. Point Vite at that same `_site` directory so it can process the React components, fancy style imports, and other things that 11ty didn’t pick up.

So a two-step build process, with 11ty handing off the Vite. Here’s the CLI command you’ll need to start 11ty and Vite in “watch” mode simultaneously:

<pre><code class="language-bash">(npx eleventy --input=src --watch) & npx vite _site</code></pre>

You can also run these commands in two separate terminals for easier debugging. 😄

With any luck, you should be able to visit `http://localhost:3000/blog-post/` (again, don’t forget the trailing slash!) to see that processed Markdown file.

{{% ad-panel-leaderboard %}}

## Partial Hydration With Shortcodes

Let’s do a brief rundown on [shortcodes](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwi1lLjx2IPzAhW9F1kFHYMdAJcQFnoECAsQAw&url=https%3A%2F%2Fwww.11ty.dev%2Fdocs%2Fshortcodes%2F&usg=AOvVaw3B_PvBaTDeHg5ztR0i7C07). Time to revisit that syntax from earlier:

<pre><code class="language-javascript">{% react '/components/TimesWeMispronouncedVite.jsx' %}</code></pre>

For those unfamiliar with shortcodes: they’re about the same as a function call, where the function returns a string of HTML to slide into your page. The “anatomy” of our shortcode is:

- `{% … %}`  
Wrapper denoting the start and end of the shortcode.
- `react`  
The name of our shortcode function we’ll configure in a moment.
- `'/components/TimesWeMispronouncedVite.jsx'`  
The first (and only) argument to our shortcode function. You can have as many arguments as you’d like.

Let’s wire up our first shortcode! Add a `.eleventy.js` file to the base of your project, and add this config entry for our `react` shortcode:

<pre><code class="language-javascript">// .eleventy.js, at the base of the project
module.exports = function(eleventyConfig) {
  eleventyConfig.addShortcode('react', function(componentPath) {
   // return any valid HTML to insert
   return `&lt;div id="root"&gt;This is where we'll import ${componentPath}&lt;/div&gt;`
  })

  return {
    dir: {
      // so we don't have to write `--input=src` in our terminal every time!
      input: 'src',
    }
  }
}</code></pre>

Now, let’s spice up our `blog-post.md` with our new shortcode. Paste this content into our markdown file:

<pre><code class="language-html"># Super interesting programming tutorial

Writing paragraphs has been fun, but that's no way to learn. Time for an interactive code example!

{% react '/components/TimesWeMispronouncedVite.jsx' %}</code></pre>

And if you run a quick `npx eleventy`, you should see this output in your `_site` directory under `/blog-post/index.html`:

<pre><code class="language-html">&lt;h1&gt;Super interesting programming tutorial&lt;/h1&gt;

&lt;p&gt;Writing paragraphs has been fun, but that's no way to learn. Time for an interactive code example!&lt;/p&gt;

&lt;div id="root"&gt;This is where we'll import /components/TimesWeMispronouncedVite.jsx&lt;/div&gt;</code></pre>

### Writing Our Component Shortcode

Now let’s do something useful with that shortcode. Remember that `script` tag we wrote while trying out Vite? Well, we can do the same thing in our shortcode! This time we’ll use the `componentPath` argument to generate the import, but keep the rest pretty much the same:

<pre><code class="language-javascript">// .eleventy.js
module.exports = function(eleventyConfig) {
  let idCounter = 0;
  // copy all our /components to the output directory
  // so Vite can find them. Very important step!
  eleventyConfig.addPassthroughCopy('components')

  eleventyConfig.addShortcode('react', function (componentPath) {
      // we'll use idCounter to generate unique IDs for each "root" div
      // this lets us use multiple components / shortcodes on the same page 👍
      idCounter += 1;
      const componentRootId = `component-root-${idCounter}`
      return `
  &lt;div id="${componentRootId}"&gt;&lt;/div&gt;
  &lt;script type="module"&gt;
    // use JSON.stringify to
    // 1) wrap our componentPath in quotes
    // 2) strip any invalid characters. Probably a non-issue, but good to be cautious!
    import Component from ${JSON.stringify(componentPath)};
    import React from 'react';
    import ReactDOM from 'react-dom';
    const componentRoot = document.getElementById('${componentRootId}');
    ReactDOM.render(React.createElement(Component), componentRoot);
  &lt;/script&gt;
      `
    })
  
  eleventyConfig.on('beforeBuild', function () {
    // reset the counter for each new build
    // otherwise, it'll count up higher and higher on every live reload
    idCounter = 0;
  })

  return {
    dir: {
      input: 'src',
    }
  }
}</code></pre>

Now, a call to our shortcode (ex. `{% react '/components/TimesWeMispronouncedVite.jsx' %}`) should output something like this:

<pre><code class="language-javascript">&lt;div id="component-root-1"&gt;&lt;/div&gt;
&lt;script type="module"&gt;
    import Component from './components/FancyLiveDemo.jsx';
    import React from 'react';
    import ReactDOM from 'react-dom';
    const componentRoot = document.getElementById('component-root-1');
    ReactDOM.render(React.createElement(Component), componentRoot);
&lt;/script&gt;</code></pre>

Visiting our dev server using `(npx eleventy --watch) & vite _site`, we should find a beautifully clickable counter element. ✨

### Buzzword Alert &mdash; Partial Hydration And Islands Architecture

We just demonstrated “islands architecture” in its simplest form. This is the idea that our interactive component trees *don’t* have to consume the entire website. Instead, we can spin up mini-trees, or “islands,” throughout our app depending on where we actually need that interactivity. Have a basic landing page of links without any state to manage? Great! No need for interactive components. But do you have a multi-step form that could benefit from X React library? No problem. Use techniques like that `react` shortcode to spin up a `Form.jsx` island.

This goes hand-in-hand with the idea of “partial hydration.” You’ve likely heard the term “hydration” if you work with component-y SSGs like NextJS or Gatsby. In short, it’s a way to:

1. **Render your components to static HTML first.**  
This gives the user something to view when they initially visit your website.
3. **“Hydrate” this HTML with interactivity.**  
This is where we hook up our state hooks and renderers to, well, make button clicks actually trigger something.

This 1-2 punch makes JS-driven frameworks viable for static sites. As long as the user has something to view before your JavaScript is done parsing, you’ll get a decent score on those lighthouse metrics.

Well, until you don’t. 😢 It can be expensive to “hydrate” an entire website since you’ll need a JavaScript bundle ready to process *every last DOM element*. But our scrappy shortcode technique *doesn’t* cover the entire page! Instead, we “partially” hydrate the content that’s there, inserting components only where necessary.

## Don’t Worry, There’s A Plugin For All This: Slinkity

Let’s recap what we discovered here:

1. Vite is an incredibly capable bundler that can process most file types (`jsx`, `vue`, and `svelte` to name a few) without extra config.
2. Shortcodes are an easy way to insert chunks of HTML into our templates, component-style.
3. We can use shortcodes to render dynamic, interactive JS bundles wherever we want using partial hydration.

So what about optimized production builds? Properly loading scoped styles? Heck, using `.jsx` to create entire pages? Well, I’ve bundled all of this (and a whole lot more!) into a project called Slinkity. I’m excited to see the [warm community reception](https://twitter.com/jadenguitarman/status/1430988821529833473?s=20) to the project, and I’d love for you, dear reader, to give it a spin yourself!

🚀 [**Try the quick start guide**](https://slinkity.dev)

### Astro’s Pretty Great Too

Readers with their eyes on cutting-edge tech *probably* thought about Astro at least once by now. 😉 And I can’t blame you! It’s built with a pretty similar goal in mind: start with plain HTML, and insert stateful components wherever you need them. Heck, they’ll even let you start writing React components *inside* Vue or Svelte components *inside* HTML template files! It’s like MDX Xtreme edition. 🤯

There’s one pretty major cost to their approach though: **you need to rewrite your app from scratch.** This means a new template format based on JSX (which you might not be comfortable with), a whole new data pipeline that’s missing a couple of niceties right now, and general bugginess as they work out the kinks.

But spinning up an 11ty + Vite cocktail with a tool like Slinkity? Well, if you already have an 11ty site, Vite should bolt into place without any rewrites, and shortcodes should cover many of the same use cases as `.astro` files. I’ll admit it’s *far* from perfect right now. But hey, it’s been useful so far, and I think it’s a pretty strong alternative if you want to avoid site-wide rewrites!

## Wrapping Up

This Slinkity experiment has served my needs pretty well so far (and [a few of y’all’s](https://twitter.com/Rich_McCartney/status/1428730629148061696?s=20) too!). Feel free to use whatever stack works for your JAM. I’m just excited to share the results of my year of build tool debauchery, and I’m so pumped to see how we can bridge the great Jamstack divide.

### Further Reading

Want to dive deeper into partial hydration, or ESM, or SSGs in general? Check these out:

- [**Islands Architecture**](https://jasonformat.com/islands-architecture/)  
This blog post from Jason Format really kicked off a discussion of “islands” and “partial hydration” in web development. It’s chock-full of useful diagrams and the philosophy behind the idea.
- [**Simplify your static with a custom-made static site generator**](https://www.smashingmagazine.com/2020/09/stack-custom-made-static-site-generator/)  
Another SmashingMag article that walks you through crafting Node-based website builders from scratch. It was a huge inspiration to me!
- [**How ES Modules have redefined web development**](https://bholmes.dev/blog/how-es-modules-have-redefined-web-development/)  
A personal post on how ES Modules have changed the web development game. This dives a little further into the “then and now” of import syntax on the web.
- [**An introduction to web components**](https://css-tricks.com/an-introduction-to-web-components/)  
An excellent walkthrough on what web components are, how the shadow DOM works, and where web components prove useful. Used this guide to apply custom components to my own framework!

{{< signature "vf, yk, il" >}}
