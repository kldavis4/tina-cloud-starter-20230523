---
title: 'Meet Skeleton: Svelte + Tailwind For Reactive UIs'
slug: skeleton-svelte-tailwind-reactive-uis
author: chris-simmons
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/beaede58-125c-47db-8c29-7af80ea35534/skeleton-svelte-tailwind-reactive-uis.jpg
date: 2022-08-12T08:00:00.000Z
summary: >-
  The power of framework-specific UI libraries, such as Skeleton, can lead to more productivity using the combined ability of Svelte and Tailwind to build modern web-based apps.
description: >-
  The power of framework-specific UI libraries, such as Skeleton, can lead to more productivity using the combined ability of Svelte and Tailwind to build modern web-based apps.
categories:
  - Tools
  - UI
  - Techniques
---

If you’ve ever found yourself tasked with creating and implementing custom UI, then you know how difficult it can be to meet the demands of the modern web. Your interface must be responsive, reactive, and accessible, all while remaining visually appealing to a broad spectrum of users. Let’s face it; this can be a challenge for even the most seasoned frontend developer.

Over the last ten years, we’ve seen the introduction of UI frameworks that help ease this burden. Most rely on JavaScript and lean into components and reactive patterns to handle real-time user interaction. Frameworks such as [Angular](https://angular.io/), [React](https://reactjs.org/), and [Vue](https://vuejs.org/) have been [established as the standard](https://2021.stateofjs.com/en-US/libraries/front-end-frameworks/) for what we currently know as modern frontend development.

Alongside the tools, we’ve seen the rise of framework-specific libraries like [Angular Material](https://material.angular.io/), [Mantine](https://mantine.dev/) (for React), and [Vuetify](https://vuetifyjs.com/en/) that to provide a “batteries included” approach to implementing UI, including deep integration of each framework’s unique set of features. With the emergence of new frameworks such as Svelte, we might expect to see similar libraries appear to fulfill this role. To gain insight into how these tools might work, let’s review what Svelte brings to frontend development.

## Svelte And SvelteKit

In 2016, [Rich Harris](https://twitter.com/rich_harris) introduced [Svelte](https://svelte.dev/), a fresh take on components for the web. To understand the benefits of Svelte, see his 2019 conference talk titled “Rethinking Reactivity,” where Rich explains the origins of Svelte and demonstrates its unique compiler-driven approach.

{{< youtube AdNJ3fydeao >}}

Of course, component libraries only take you so far. To meet the demands of today’s web, app frameworks like [Next.js](https://nextjs.org/) and [Nuxt](https://nuxtjs.org/) have been introduced to manage routing, server-side rendering (SSR), handle asynchronous tasks like HTTP, and much, much more. Svelte’s answer to this is [SvelteKit](https://kit.svelte.dev/), a web app framework built for Svelte on top of next-generation technologies like [Vite](https://vitejs.dev/). It is [fast approaching version 1.0](https://github.com/sveltejs/kit/milestone/2), but still early days for the framework itself.

When considering UI for Svelte and SvelteKit, you’ll find several wrappers for general-purpose UI libraries, such as [Smelte](https://smeltejs.com/) for Material Design and [Svelma](https://c0bra.github.io/svelma/) for Bulma. However, your options are more limited if you seek tight integration with Svelte itself. Many also lack direct integration with Tailwind, a popular CSS tool to help create and manage design systems within your apps.

## Design Systems With Tailwind

First introduced in 2019, [Tailwind](https://tailwindcss.com/) provides a unique utility-based approach to CSS and styling. When designing for the web, it can be challenging to translate static design mocks to rendered web pages in a consistent manner.

Using CSS to create a set of reusable styles, while simple in concept, can quickly become a headache as the scale of your project grows. You have to manage your color palette, find a way to standardize common styles and sizes, and continuously recreate common layouts with CSS properties like [Grid](https://css-tricks.com/snippets/css/complete-guide-grid/) and [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/). Then do it all over again for your next project!

This is what Tailwind aims to address while providing a customizable shorthand CSS syntax that can be maintained directly within HTML or implemented via a more classic approach with [@apply](https://tailwindcss.com/docs/reusing-styles#extracting-classes-with-apply).

Let’s compare a few examples of standard CSS versus the Tailwind equivalent. 

**Note:** *Tailwind provides a handy [test environment](https://play.tailwindcss.com/) if you would like to try these as we go.*

### Utility Classes

Standard CSS and HTML:

<pre><code class="language-css">.padding-8 { padding: 8px; }
.padding-16 { padding: 16px; }</code></pre>

<pre><code class="language-html">&lt;div class="padding-8"&gt;Foobar&lt;/div&gt;
&lt;div class="padding-16"&gt;Foobar&lt;/div&gt;</code></pre>

Tailwind:

<pre><code class="language-html">&lt;div class="p-4"&gt;Foobar&lt;/div&gt;
&lt;div class="p-8"&gt;Foobar&lt;/div&gt;</code></pre>

**Note:** *No extra CSS is needed as Tailwind creates this for us.*

### Managing Colors

Standard CSS:

<pre><code class="language-css">:root {
	--color-red: #FF0000;
}
.text-red { color: var(--color-red); }
.background-red { background: var(--color-red); }</code></pre>

Tailwind:

<pre><code class="language-html">&lt;div class="text-red-500"&gt;Foobar&lt;/div&gt;
&lt;div class="bg-red-500"&gt;Foobar&lt;/div&gt;</code></pre>

**Note:** *Tailwind includes a [default color palette](https://tailwindcss.com/docs/customizing-colors) with colors scaled from 50-900. Shade 500 is typically treated as the base color.*

### Handling Grid Layouts

Standard CSS and HTML:

<pre><code class="language-css">.grid-three-column {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	grid-template-rows: repeat(3, 1fr);
	grid-column-gap: 16px;
	grid-row-gap: 16px;
}</code></pre>

<pre><code class="language-html">&lt;div class="grid-three-column"&gt;
    &lt;div&gt;Cell&lt;/div&gt;
    &lt;div&gt;Cell&lt;/div&gt;
    &lt;div&gt;Cell&lt;/div&gt;
&lt;/div&gt;</code></pre>

Tailwind:

<pre><code class="language-html">&lt;div class="grid grid-cols-3 gap-4"&gt;
    &lt;div&gt;Cell&lt;/div&gt;
    &lt;div&gt;Cell&lt;/div&gt;
    &lt;div&gt;Cell&lt;/div&gt;
&lt;/div&gt;</code></pre>

**Note:** *Values are REM, so gap-4 translates to 4 REM (or 16px).*

Even with these basic examples, you can imagine how Tailwind can help boost productivity:

- you can tweak and adjust styles on the fly (ex: switch from 3 to 4 grid columns);
- make use of the default color palette;
- easily recreate intricate layouts.

Tailwind essentially provides a set of design building blocks that can be extended and adjusted to fit the needs of any sort of app.

{{% feature-panel %}}

## Introducing Skeleton

Now that you understand the benefit of each of these tools, I’d like to take a moment to introduce [Skeleton](https://skeleton.brainandbonesllc.com/) &mdash; a new open-source UI component library that tightly integrates both Svelte and Tailwind. It provides a broad set of Svelte components that can easily be adjusted using Tailwind’s utility classes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85cec3f2-b29a-479b-91bd-da6547d62fc0/3-skeleton-svelte-tailwind-reactive-uis.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85cec3f2-b29a-479b-91bd-da6547d62fc0/3-skeleton-svelte-tailwind-reactive-uis.png" width="800" height="579" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85cec3f2-b29a-479b-91bd-da6547d62fc0/3-skeleton-svelte-tailwind-reactive-uis.png'>Large preview</a>)" alt="A screenshot of Skeleton library" >}}

Skeleton was founded by the development team at [Brain & Bones](https://www.brainandbonesllc.com/). The team, myself included, has been consistently impressed with Svelte and the tools it brings to the frontend developer’s arsenal. The team and I were looking to migrate several internal projects from Angular to SvelteKit when we realized there was an opportunity to combine Svelte’s intuitive component system with the utility-driven design systems of Tailwind, and thus Skeleton was born.

The team realized Skeleton has the potential to benefit many in the Svelte community, and as such, we’ve decided to make it [open-source](https://github.com/Brain-Bones/skeleton). We hope to see Skeleton grow into a powerful UI toolkit that can help many developers, whether your skills lie within the frontend space or not.

To see what we mean, let’s take a moment to create a basic SvelteKit app and integrate Skeleton.

{{% ad-panel-leaderboard %}}
 
## Getting Started With Skeleton

Open your terminal and run each of the following commands. Be sure to set “my-skeleton-app” to whatever name you prefer. When prompted, we recommend using Typescript and creating a barebones (aka “skeleton”) project:

<pre><code class="language-bash">npm create svelte@latest my-skeleton-app
cd my-skeleton-app
npm install
npm run dev -- --open</code></pre>

This will generate the SvelteKit app, move your terminal into the project directory, install all required dependencies, then start a local dev server. Using the `-- --open` flag here will open the following address in your browser automatically:

<pre><code class="language-bash">http://localhost:5173/</code></pre>

In your terminal, use <kbd>Ctrl</kbd> + <kbd>C</kbd> to close and stop the server. Don’t worry; we’ll resume it in a moment.

Next, we need to install Tailwind. [Svelte-add](https://github.com/svelte-add/tailwindcss) helps make this process trivial. Simply run the following commands, and it’ll handle the rest.

<pre><code class="language-bash">npx svelte-add@latest tailwindcss
npm install</code></pre>

This will install the latest Tailwind version into your project, create `/src/app.css` to house your global CSS, and generate the necessary `tailwind.config.cjs`. Then we install our new Tailwind dependency.

Finally, let’s install the Skeleton package via NPM:

<pre><code class="language-bash">npm i @brainandbones/skeleton --save-dev</code></pre>

We’re nearly ready to add our first component, and we just need to make a couple of quick updates to the project configuration.

### Configure Tailwind

To ensure Skeleton plays well with Tailwind, open `tailwind.config.cjs` in the root of your project and add the following:

<div class="break-out">

<pre><code class="language-javascript">module.exports = {
    content: [
		// ...
        './node_modules/@brainandbones/skeleton/**/*.{html,js,svelte,ts}'
    ],
    plugins: [
        require('@brainandbones/skeleton/tailwind.cjs')
    ]
}</code></pre>
</div>

The `content` section ensures the compiler is aware of all Tailwind classes within our Skeleton components, while `plugins` uses a Skeleton file to prepare for the theme we’ll set up in the next section.

### Implement A Skeleton Theme

Skeleton includes a simple yet powerful [theme system](https://skeleton.brainandbonesllc.com/guides/themes) that leans into [Tailwind’s best practices](https://tailwindcss.com/docs/customizing-colors#using-css-variables). The theme controls the visual appearance of all components and intelligently adapts for [dark mode](https://tailwindcss.com/docs/dark-mode) while also providing access to Tailwind utility classes that represent your theme’s unique color palette.

The Skeleton team has provided a [curated set of themes](https://skeleton.brainandbonesllc.com/guides/themes), as well as a [theme generator](https://skeleton.brainandbonesllc.com/guides/themes) to help design custom themes using either Tailwind colors or hex colors to match your brand’s identity.

To keep things simple, we’ll begin with Skeleton’s default theme. Copy the following CSS into a new file in *`/src/theme.css`.*

<pre><code class="language-css">:root {
	/* --- Skeleton Theme --- */
	/* primary (emerald) */
	--color-primary-50: 236 253 245;
	--color-primary-100: 209 250 229;
	--color-primary-200: 167 243 208;
	--color-primary-300: 110 231 183;
	--color-primary-400: 52 211 153;
	--color-primary-500: 16 185 129;
	--color-primary-600: 5 150 105;
	--color-primary-700: 4 120 87;
	--color-primary-800: 6 95 70;
	--color-primary-900: 6 78 59;
	/* accent (indigo) */
	--color-accent-50: 238 242 255;
	--color-accent-100: 224 231 255;
	--color-accent-200: 199 210 254;
	--color-accent-300: 165 180 252;
	--color-accent-400: 129 140 248;
	--color-accent-500: 99 102 241;
	--color-accent-600: 79 70 229;
	--color-accent-700: 67 56 202;
	--color-accent-800: 55 48 163;
	--color-accent-900: 49 46 129;
	/* warning (rose) */
	--color-warning-50: 255 241 242;
	--color-warning-100: 255 228 230;
	--color-warning-200: 254 205 211;
	--color-warning-300: 253 164 175;
	--color-warning-400: 251 113 133;
	--color-warning-500: 244 63 94;
	--color-warning-600: 225 29 72;
	--color-warning-700: 190 18 60;
	--color-warning-800: 159 18 57;
	--color-warning-900: 136 19 55;
	/* surface (gray) */
	--color-surface-50: 249 250 251;
	--color-surface-100: 243 244 246;
	--color-surface-200: 229 231 235;
	--color-surface-300: 209 213 219;
	--color-surface-400: 156 163 175;
	--color-surface-500: 107 114 128;
	--color-surface-600: 75 85 99;
	--color-surface-700: 55 65 81;
	--color-surface-800: 31 41 55;
	--color-surface-900: 17 24 39;
}</code></pre>

**Note:** *Colors are converted from Hex to RGB to properly support [Tailwind’s background opacity](https://tailwindcss.com/docs/background-color#changing-the-opacity).*

Next, let’s configure SvelteKit to use our new theme. To do this, open your root layout file at `/src/routes/__layout.svelte`. Declare your theme just before your global stylesheet `app.css`.

<pre><code class="language-javascript">import '../theme.css'; // &lt;--
import '../app.css';</code></pre>

To make things look a bit nicer, we’ll add some basic `<body>` element styles that support either light or [dark mode](https://tailwindcss.com/docs/dark-mode) system settings. Add the following to your `/src/app.css`.

<div class="break-out">

<pre><code class="language-css">body { @apply bg-surface-100 dark:bg-surface-900 text-black dark:text-white p-4; }</code></pre>
</div>

For more instruction, consult the [Style](https://skeleton.brainandbonesllc.com/guides/styling) documentation which covers global styles in greater detail.

### Add A Component

Finally, let’s implement our first Skeleton component. Open your app’s home page `/src/routes/index.svelte` and add the follow. Feel free to replace the file’s entire contents:

<pre><code class="language-html">&lt;script lang="ts"&gt;
    import { Button } from '@brainandbones/skeleton';
&lt;/script&gt;

&lt;Button variant="filled-primary"&gt;Skeleton&lt;/Button&gt;</code></pre>

To preview this, we’ll need to restart our local dev server. Run `npm run dev` in your terminal and point your browser to `http://localhost:5173/`. You should see a Skeleton Button component appear on the page!

### Customizing Components

As with any Svelte component, custom “props” (read: properties) can be provided to configure your component. For example, the Button component’s `variant` prop allows us to set any number of [canned options](https://skeleton.brainandbonesllc.com/components/buttons) that adapt to your theme. By switching the variant value to `filled-accent` we’ll see the button change from our theme’s primary color (emerald) to the accent color (indigo).

Each component provides a set of props for you to configure as you please. See the [Button documentation](https://skeleton.brainandbonesllc.com/components/buttons) to try an interactive sandbox where you can test different sizes, colors, etc.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee60c94-44dd-464d-b8da-126ea888442b/1-skeleton-svelte-tailwind-reactive-uis.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee60c94-44dd-464d-b8da-126ea888442b/1-skeleton-svelte-tailwind-reactive-uis.png" width="800" height="248" sizes="100vw" caption="The button styles will update as you adjust the fields on the right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee60c94-44dd-464d-b8da-126ea888442b/1-skeleton-svelte-tailwind-reactive-uis.png'>Large preview</a>)" alt="A screenshot with an interactive sandbox where you can test different sizes, colors, etc." >}}

You may notice that many of the prop values resembled Tailwind class names. In fact, this is exactly what these are! These props are provided verbatim to the component’s template. This means we can set a component’s background style to any theme color, any Tailwind color, or even set a one-off color using [Tailwind’s arbitrary value syntax](https://tailwindcss.com/docs/background-color#arbitrary-values).

<pre><code class="language-html">&lt;!-- Using our theme color --&gt;
&lt;Button background="bg-accent-500"&gt;Accent&lt;/Button&gt;

&lt;!-- Using Tailwind colors --&gt;
&lt;Button background="bg-orange-500"&gt;Orange&lt;/Button&gt;

&lt;!-- Using Tailwind's arbitrary value syntax --&gt;
&lt;Button background="bg-[#BADA55]"&gt;Arbitrary&lt;/Button&gt;</code></pre>

This gives you the control to maintain a cohesive set of styles or choose to “draw outside of the lines” with arbitrary values. You’re not limited to the default props, though. You can provide any valid CSS classes to a component using a standard `class` attribute:

<div class="break-out">

<pre><code class="language-html">&lt;Button variant="filled-primary" class="py-10 px-20"&gt;Big!&lt;/Button&gt;</code></pre>
</div>

### Form Meets Function

One of the primary benefits of framework-specific libraries like Skeleton is the potential for deep integration of the framework’s unique set of features. To see how Skeleton integrates with Svelte, let’s try out [Skeleton’s dialog system](https://skeleton.brainandbonesllc.com/utilities/dialogs).

First, add the Dialog component within the global scope of your app. The easiest way to do this is to open `/src/routes/__layout.svelte` and add the following above the `<slot />` element:

<pre><code class="language-html">&lt;script lang="ts"&gt;
	// ...
    import { Dialog } from '@brainandbones/skeleton';
&lt;/script&gt;

&lt;!-- Add the Dialog component here --&gt;
&lt;Dialog /&gt;

&lt;slot /&gt;</code></pre>

**Note:** *The Dialog component will not be visible on the page by default.*

Next, let’s update our home page to trigger our first Dialog. Open `/src/routes/index.svelte` and replace the entire contents with the following:

<div class="break-out">

<pre><code class="language-javascript">&lt;script lang="ts"&gt;
    import { Button, dialogStore } from '@brainandbones/skeleton';
    import type { DialogAlert } from '@brainandbones/skeleton/Notifications/Stores';

    function triggerDialog(): void {
        const d: DialogAlert = {
            title: ‘Welcome to Skeleton.’,
            body: ‘This is a standard alert dialog.’,
        };
        dialogStore.trigger(d);
    }
&lt;/script&gt;

&lt;Button variant="filled-primary" on:click={() =&gt; { triggerDialog() }}&gt;Trigger Dialog&lt;/Button&gt;</code></pre>
</div>

This provides all the scaffolding needed to trigger a dialog. In your browser, click the button, and you should see your new dialog message appear!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e323dbf-e1c0-4605-9718-1c3ad55023cc/2-skeleton-svelte-tailwind-reactive-uis.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e323dbf-e1c0-4605-9718-1c3ad55023cc/2-skeleton-svelte-tailwind-reactive-uis.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e323dbf-e1c0-4605-9718-1c3ad55023cc/2-skeleton-svelte-tailwind-reactive-uis.png'>Large preview</a>)" alt="An alert dialog" >}}

Skeleton accomplishes this using Svelte’s [writable stores](https://svelte.dev/tutorial/writable-stores), which are reactive objects that help manage the global state. When the button is clicked, the dialog store is triggered, and an instance of a dialog is provided to the store. The store then acts as a queue. Since stores are reactive, this means our Dialog component can listen for any updates to the store’s contents. When a new dialog is added to the queue, the Dialog component updates to show the contents on the screen.

Skeleton always shows the top-most dialog in the queue. When dismissed, it then displays the following dialog in the queue. If no dialogs remain, the Dialog component hides and returns to its default non-visible state.

Here’s a simple mock to help visualize the data structure of the dialog store queue:

<pre><code class="language-javascript">dialogStore = [
    // dialog #1, &lt;-- top items the queue, shown on screen
    // dialog #2, &lt;-- the next dialog in line
    // dialog #3, &lt;-- bottom of the queue, the last added
];</code></pre>

It’s Skeleton’s tight integration with Svelte features that makes this possible. That’s the power of framework-specific tooling &mdash; structure, design, and functionality all in one tightly coupled package!

{{% ad-panel-leaderboard %}}
 
## Learn More About Skeleton

Skeleton is currently available in early access beta, but feel free to visit our [documentation](https://skeleton.brainandbonesllc.com/) if you would like to learn more. The site provides detailed guides to help get started and covers the full suite of available components and utilities. You can report issues, request walkthroughs, or contribute code at [Skeleton’s GitHub](https://github.com/Brain-Bones/skeleton). You’re also welcome to join our [Discord community](https://discord.gg/EXqV7W8MtY) to chat with contributors and showcase projects you’ve created with Skeleton.

Skeleton was founded by [Brain & Bones](https://www.brainandbonesllc.com/). We feed gamers’ love for competition, providing a platform that harnesses the power of hyper-casual games to enhance engagement online and in-person.

### Further Resources

- [Skeleton](https://skeleton.brainandbonesllc.com/) by [Brain & Bones](https://www.brainandbonesllc.com/)
- [Skeleton’s GitHub repo](https://github.com/Brain-Bones/skeleton)
- [Skeleton’s Discord community](https://discord.gg/EXqV7W8MtY)
- Featured in the [official Svelte August 2022 community showcase](https://svelte.dev/blog/whats-new-in-svelte-august-2022)

{{< signature "vf, yk, il" >}}
