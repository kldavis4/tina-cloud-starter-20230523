---
title: 'Comparing Styling Methods In Next.js'
slug: comparison-styling-methods-next-js
author: adebiyi-adedotun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7579d8d1-2d12-4da8-938e-b731d4282bfb/comparison-styling-methods-next-js.png
date: 2020-09-17T10:30:00.000Z
summary: >-
  Among others, [Next.js](https://nextjs.org) has dubbed itself: *The React Framework for Static Websites*. But just like every other framework whose goal is to help you build what matters by abstracting common, redundant tasks, you’re often required to learn something new and opinionated. With Next.js, one of the things you need to know is how to integrate different CSS methods with its API, and that is the focus of this tutorial.
description: >-
  Among others, [Next.js](https://nextjs.org) has dubbed itself: *The React Framework for Static Websites*. But just like every other framework whose goal is to help you build what matters by abstracting common, redundant tasks, you’re often required to learn something new and opinionated. With Next.js, one of the things you need to know is how to integrate different CSS methods with its API, and that is the focus of this tutorial.
categories:
  - React
  - Next.js
---

As you might be aware, there are many [differing perspectives on CSS-in-JS](https://css-tricks.com/the-differing-perspectives-on-css-in-js/), and we all have an opinion of the topic in one way or the other that might be quite different from the opinions of framework authors.

**Next.js** is one of the [recommended tool-chains](https://reactjs.org/docs/create-a-new-react-app.html#recommended-toolchains) when creating a new React app. Tools like Next have a simple goal of abstracting away commonly redundant tasks when writing a React app. This helps developers focus more on writing code than reinventing the wheel. While this is usually a good thing, it can also be a little tedious to get started with. For one, there’s a hurdle to cross by learning about the abstractions, and while there are a bevy of that in Next (Routing, Data Fetching…), one often overlooked is Styling.

To serve a wider audience, Next.js supports a myriad of ways to style your components. Whether you belong to the Utility first or CSS-in-JS party isn’t much of Next’s concern, its concern is how you inject your choice into its API.

The goal of this article is to help you understand how to set up styling in your Next app. We’ll be using different methods to handle the comparison. We’ll implement the different types of styling in a book application I have set up. The styling methods we’ll be looking at include:

1. [Global CSS](https://nextjs.org/docs/basic-features/built-in-css-support#adding-a-global-stylesheet),
2. [SASS/SCSS](https://nextjs.org/docs/basic-features/built-in-css-support#sass-support),
3. [Component-Level SASS/SCSS](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css),
4. [Component-Level CSS (CSS Modules)](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css),
5. [Styled-Components](https://github.com/vercel/next.js/tree/canary/examples/with-styled-components),
6. [Styled JSX](https://github.com/vercel/next.js/tree/canary/examples/with-styled-jsx),
7. [Emotion](https://github.com/vercel/next.js/tree/canary/examples/with-emotion).

### Prerequisite

Before we begin our styling tour, there are some Next nuances you need to acquaint yourself with.

1. [`_app.js`](https://nextjs.org/docs/advanced-features/custom-app)    
This is a custom component that resides in the pages folder. Next.js uses this component to initialize pages.
2. [`_document.js`](https://nextjs.org/docs/advanced-features/custom-document)  
Like `_app.js`, `_document.js` is a custom component that Next.js uses to augment your applications `<html>` and `<body>` tags. This is necessary because Next.js pages skip the definition of the surrounding document’s markup.
3. [`_.babelrc`](https://nextjs.org/docs/advanced-features/customizing-babel-config)  
When present, Next.js uses this file as the single source of truth for some internal configuration and gives you permission to extend it.

Keep in mind that if you have your server running before adding the `_app.js` file, then you need to restart it.

{{% feature-panel %}}

## Creating A Next App With `create-next-app`

Creating a Next app with `create-next-app` is as simple as following the steps below:

- Install `create-next-app` globally.

<pre><code class="language-bash">yarn global add create-next-app // Installs create-next-app globally</code></pre>

- Create a new Next app named **styling-in-next**.

<div class="break-out">

<pre><code class="language-bash">create-next-app styling-in-next // Creates a new Next app named styling-in-next</code></pre>
</div>

- Change directory into the new site.

<pre><code class="language-bash">cd styling-in-next // Switch directory into the new Next app</code></pre>

- Run the site.

<pre><code class="language-bash">yarn dev -p 3000 // Instruct Next to run on port 3000</code></pre>
    
> Refer to the [documentation](https://nextjs.org/docs/getting-started) for more information on creating and running a Next app.

The app should now be running on `https://localhost:3000`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f64b3d5c-eddd-4746-96ce-f9bc29d3c91b/welcome-to-next-js.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f64b3d5c-eddd-4746-96ce-f9bc29d3c91b/welcome-to-next-js.png" sizes="100vw" caption="Next.js default starter index page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f64b3d5c-eddd-4746-96ce-f9bc29d3c91b/welcome-to-next-js.png'>Large preview</a>)" alt="A screenshot of Next.js default starter index page" >}}

## Demo Repository

As we go along we’ll be building a contrived *Bookshelf* by applying different styling methods to each *books*. The end result will look like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acdc7dc3-4b6a-45cc-91d9-c05311501f81/final-styled-bookshelf.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acdc7dc3-4b6a-45cc-91d9-c05311501f81/final-styled-bookshelf.png" sizes="100vw" caption="Final styled Bookshelf. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acdc7dc3-4b6a-45cc-91d9-c05311501f81/final-styled-bookshelf.png'>Large preview</a>)" alt="A screenshot of the final demo styled Bookshelf" >}}

The image above shows 6 books; each book will have its own components, then we’ll apply a specific style type to each specific book, i.e. Book 1 will make use of a global style while Book 2 will make use of another. This way we’ll see how each of these styles work and how they can be used. This will help you in making a better decision on what option to choose.

To make things simple, I’ve scaffolded a GitHub repository for you to follow along. You can grab it [here](https://github.com/smashingmagazine/styling-in-next.git).

Some changes have also been made to the default starter generated by `create-next-app`. Folders like *emotion*, *global*, *modules*, *styled-components* etc. have been added to the `styles` folder &mdash; with their corresponding style files &mdash; as well as a `components` directory with multiple components.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9176ecf1-44d3-40fe-b6e4-2c0fdd03256a/changes-to-styes-and-components-folders.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9176ecf1-44d3-40fe-b6e4-2c0fdd03256a/changes-to-styes-and-components-folders.png" sizes="100vw" caption="Changes to the styles and components folders. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9176ecf1-44d3-40fe-b6e4-2c0fdd03256a/changes-to-styes-and-components-folders.png'>Large preview</a>)" alt="A screenshot of the initial changes made to the demo repository styles and components directory" >}}

The `index.js` file has been modified to `import` and `render` the needed `components`, and each of the components has a similar structure as shown in the image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7682eb20-902b-4748-b833-36d6208a2811/changes-to-component-files-and-index.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7682eb20-902b-4748-b833-36d6208a2811/changes-to-component-files-and-index.png" sizes="100vw" caption="Changes to the individual components and index files. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7682eb20-902b-4748-b833-36d6208a2811/changes-to-component-files-and-index.png'>Large preview</a>)" alt="A screenshot of the initial changes made to BookTwo.js, BookOne.js, and index.js" >}}

If you cloned and ran the [demo repository](https://github.com/smashingmagazine/styling-in-next.git), here’s what your page should look like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f50a7f2-bac2-464b-8fd1-0270aa8e21ea/demo-app-repo-index-page.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f50a7f2-bac2-464b-8fd1-0270aa8e21ea/demo-app-repo-index-page.png" sizes="100vw" caption="Default index page from demo repo. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f50a7f2-bac2-464b-8fd1-0270aa8e21ea/demo-app-repo-index-page.png'>Large preview</a>)" alt="A screenshot of the default index page from the demo repository" >}}

With all that out of the way, let’s get styling.

## Global Style

One of the common things you’d normally do when you start a new web project is to [reset](https://bitsofco.de/my-css-reset-base/) or [normalize](https://necolas.github.io/normalize.css/) your CSS so there’s a uniform starting position among browsers. This is a perfect example of using Global CSS without worrying about [scoping](https://css-tricks.com/saving-the-day-with-scoped-css/).

- Update `styles/global/globals.css` with this extended [Minimal CSS Reset](https://www.digitalocean.com/community/tutorials/css-minimal-css-reset).

<div class="break-out">

<pre><code class="language-css">/* styles/global/globals.css */
html {
  box-sizing: border-box;
  font-size: 16px;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
    Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}
body,
h1,
h2,
h3,
h4,
h5,
h6,
p,
ol,
ul {
  margin: 0;
  padding: 0;
  font-weight: normal;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: bold;
}

ol,
ul {
  list-style: none;
}

img {
  max-width: 100%;
  height: auto;
}

a {
  color: inherit;
  text-decoration: none;
}</code></pre>
</div>

- Import the CSS reset *`styles/global/globals.css`* in `pages/_app.js`.

<pre><code class="language-css">// pages/_app.js
import "../styles/global/globals.css";

function MyApp({Component, pageProps}) {
  return &lt;Component {...pageProps} /&gt;;
}

export default MyApp;</code></pre>

*Global styles can only be imported in the* `pages/_app.js`*. This is directly logical because these styles will apply to all* `pages` *and* `components` *in your application &mdash; regardless of where you import them &mdash; so it is better to have a single source of [import] truth to keep things straightforward, and/or if something goes wrong.*

At this point, we do not have a lot of visual changes to our *Bookshelf* since we have only made *normalization* changes. One thing you might notice is the font and spacing changes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba94a1d7-1461-43e2-87a9-6388d69048d9/demo-app-repo-index-page-with-css-reset.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba94a1d7-1461-43e2-87a9-6388d69048d9/demo-app-repo-index-page-with-css-reset.png" sizes="100vw" caption="Changes to the index page after adding a CSS reset. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba94a1d7-1461-43e2-87a9-6388d69048d9/demo-app-repo-index-page-with-css-reset.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after adding a CSS reset" >}}

{{% ad-panel-leaderboard %}}

## SASS/SCSS

Next.js also allows styling with SASS with the `.sass` or `.scss` extension. Installing [Sass](https://yarnpkg.com/package/sass) is a requirement. Just like global styles, they can only be imported in `pages/_app.js`.

- Install the [Sass](https://yarnpkg.com/package/sass) package.

<pre><code class="language-bash">yarn add sass</code></pre>

- Update `styles/scss/bookshelf.scss`.

<pre><code class="language-css">// styles/scss/bookshelf.scss
.the-bookshelf {
  width: 100vw;
  height: 100vh;
  background-color: #e3e3e3;
  display: flex;
  justify-content: center;
  align-items: center;

  .bookshelf-wrap {
    &gt; .bookshelf {
      box-shadow: inset 0 -20px #7b5019;
      padding-bottom: 20px;
      display: flex;
      align-items: flex-end;
    }

    [class*="book"] {
      font-size: 32px;
      letter-spacing: -0.045em;
      display: flex;
      transition: 0.2s;

      &:hover {
        transform: none;
      }
    }

    .book-info {
      text-transform: uppercase;
      writing-mode: sideways-rl;
      display: flex;
      justify-content: space-around;
      flex: 1;
      align-items: center;
      font-weight: bold;
      padding: 16px 0;

      .title {
        font-weight: inherit;
        font-size: 20px;
      }

      .author {
        font-weight: inherit;
        font-size: 15px;
      }
    }
  }
}</code></pre>
  
- Also update `styles/sass/bookone.sass` and `styles/sass/booktwo.sass` like so:

<pre><code class="language-css">// styles/sass/bookone.sass
  .book-one
    color: #f00
    width: 78px
    height: 350px
    transform: rotate(-4deg)
    margin-left: 16px
    margin-right: 23px
    background-color: black</code></pre>

<pre><code class="language-css">// styles/sass/booktwo.sass
.book-two
  color: #781e0b
  width: 38px
  height: 448px
  margin-right: 23px
  background-color: #ffab44</code></pre>

*SASS (*`.sass`*) is based on indentation.  To make formatting easier, you can install* [*this VSCode Extension*](https://marketplace.visualstudio.com/items?itemName=Syler.sass-indented) *for SASS files support (formatting, syntax highlighting…)* 

- Import the three style files &mdash; `styles/scss/bookshelf.scss` , `styles/sass/bookone.sass`, and `styles/sass/booktwo.sass` &mdash; in `pages/_app.js`.

<pre><code class="language-css">// pages/_app.js
import "../styles/globals.css";
import "../styles/scss/bookshelf.scss";
import "../styles/sass/bookone.sass";
import "../styles/sass/booktwo.sass";

function MyApp({Component, pageProps}) {
  return <Component {...pageProps} />;
}

export default MyApp;</code></pre>

Our Bookshelf is beginning to take shape. With the styles applied, the first and second book should be styled and displayed as intended.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c196d28-f40f-4f47-9031-ef5cdb9513ea/book-one-two-styled-with-sass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c196d28-f40f-4f47-9031-ef5cdb9513ea/book-one-two-styled-with-sass.png" sizes="100vw" caption="BookOne and BookTwo styled with SASS. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c196d28-f40f-4f47-9031-ef5cdb9513ea/book-one-two-styled-with-sass.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after styling the first and second book with SASS" >}}

{{% ad-panel-leaderboard %}}

## CSS Modules

CSS Modules is a [component-level CSS](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css), that comes built-in with Next and can be activated by naming the style files with the `.module.css` extension. It is also possible to use CSS Modules with SASS/SCSS with the  `.module.sass` or `.module.scss` extension.

Let’s style the `components/BookThree.js` component with it.

- Update `styles/modules/BookThree.module.css`.

<pre><code class="language-css">
/* styles/modules/BookThree.module.css */
.book-three {
  color: #df66c3;
  width: 106px;
  height: 448px;
  margin-right: 23px;
  background-color: #153086;
  transform: rotate(-4deg);
}</code></pre>

- Import `styles/modules/BookThree.module.css` in `components/BookThree.js`, and apply the `.book-three` class.

<div class="break-out">

<pre><code class="language-javascript">// components/BookThree.js
import BookThreeStyles from "../styles/modules/BookThree.module.css";

export default function BookThree() {
  return (
    &lt;div className={BookThreeStyles["book-three"]}&gt;
      &lt;div className="book-info"&gt;
        &lt;p className="title"&gt;the revolt of the public&lt;/p&gt;
        &lt;p className="author"&gt;Martin Gurri&lt;/p&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}</code></pre>
</div>

Accessing class names in CSS Modules is similar to [Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors) in JavaScript &mdash; with the dot or bracket notation. Here we import `BookThreeStyles` and then use the bracket notation to apply the style we have in `styles/modules/BookThree.module.css` file.

If the selector (in this case, class name) was properly accessed, the third book should be styled now.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c80c6b3-e9a8-4711-9fe1-f06a2898894c/book-three-styled-with-css-modules.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c80c6b3-e9a8-4711-9fe1-f06a2898894c/book-three-styled-with-css-modules.png" sizes="100vw" caption="BookThree styled with CSS Modules. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c80c6b3-e9a8-4711-9fe1-f06a2898894c/book-three-styled-with-css-modules.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after styling the third book with CSS Modules" >}}

## Emotion

[Emotion](https://emotion.sh/docs/introduction) is a CSS-in-JS library and like any other CSS-in-JS, allows you to write CSS styles with JavaScript. 

Let’s style the  `components/BookFour.js` component with it.

- Install the packages: `@emotion/core`, `@emotion/styled`, `emotion`, `emotion-server`.

<pre><code class="language-bash">yarn add @emotion/core @emotion/styled emotion emotion-server</code></pre>

- Update `styles/emotion/StyledBookFour.js`.

<pre><code class="language-css">// styles/emotion/StyledBookFour.js
import styled from "@emotion/styled";

export const StyledBookFour = styled.div`
  color: white;
  width: 38px;
  height: 400px;
  margin-left: 20px;
  margin-right: 10px;
  background-color: #2faad2;
  transform: rotate(4deg);
`;</code></pre>
 
After importing `styled` from `@emotion/styled`, we export the `StyledBookFour` *styled component* &mdash; not to be confused with the other CSS-in-JS [Styled Component](https://styled-components.com/) &mdash; enhanced with the `styled` emotion method as in `styled.div`. Then we can use `<StyledBookFour/>` as in the next step below.

> Learn more about emotion’s [styled](https://emotion.sh/docs/styled) function.

- Using `<StyledBookFour/>` is similar to how you’d use any other React component. Import `styles/emotion/StyledBookFour.js` in `components/BookFour.js`, and apply the `StyledBookFour` component.

<pre><code class="language-javascript">// components/BookFour.js
import {StyledBookFour} from "../styles/emotion/StyledBookFour";

export default function BookFour() {
  return (
    &lt;StyledBookFour className="book-four"&gt;
      &lt;div className="book-info"&gt;
        &lt;p className="title"&gt;the man died&lt;/p&gt;
        &lt;p className="author"&gt;wole soyinka&lt;/p&gt;
      &lt;/div&gt;
    &lt;/StyledBookFour&gt;
  );
}</code></pre>
    
With a *sufficient dose of emotion*, the fourth book should be thus styled.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abfd659a-fa7f-4599-88a7-bfff3d6b8ea0/book-four-styled-with-emotion.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abfd659a-fa7f-4599-88a7-bfff3d6b8ea0/book-four-styled-with-emotion.png" sizes="100vw" caption="BookFour styled with Emotion. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abfd659a-fa7f-4599-88a7-bfff3d6b8ea0/book-four-styled-with-emotion.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after styling the fourth book with Emotion" >}}

## Styled JSX

Like Global CSS and CSS-Modules, [Styled-JSX](https://github.com/vercel/styled-jsx) works with Next.js without any extra setup required. If it helps, Styled-JSX is also [Vercel](https://vercel.com)’s offering of a component-based CSS, the same creators of Next.js.

Let’s style the  `components/BookFive.js` component with it.

To keep things simple, we use the internal mode of styled-jsx here. By passing the `jsx` prop to the `<style/>` component, we are able to write as much CSS as we want like we did with `.book-five`, with the additional benefit of the style being localized to the `<BookFive/>` component.

<pre><code class="language-javascript">// components/BookFive.js
export default function BookFive() {
  return (
    &lt;div className="book-five"&gt;
      &lt;div className="book-info"&gt;
        &lt;p className="title"&gt;there was a country&lt;/p&gt;
        &lt;p className="author"&gt;Chinua Achebe&lt;/p&gt;
      &lt;/div&gt;
      &lt;style jsx&gt;{`
        .book-five {
          color: #fff;
          width: 106px;
          height: 448px;
          margin-right: 23px;
          background-color: #000;
          transform: rotate(4deg);
        }
      `}&lt;/style&gt;
    &lt;/div&gt;
  );
}</code></pre>
    
And just like that, the fifth book takes its styling.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af1c0ba4-8c9e-482a-8468-6b6886c5c4bf/book-five-styled-with-styled-jsx.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af1c0ba4-8c9e-482a-8468-6b6886c5c4bf/book-five-styled-with-styled-jsx.png" sizes="100vw" caption="BookFive styled with Styled JSX. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af1c0ba4-8c9e-482a-8468-6b6886c5c4bf/book-five-styled-with-styled-jsx.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after styling the fifth book with Styled JSX" >}}

## Styled Components

[Styled-Component,](https://styled-components.com) just like Emotion, is also a CSS-in-JS library that allows you to write CSS styles with JavaScript. Getting it setup is a little bit involved.

- First, install `babel-plugin-styled-components` and `styled-components`.

<pre><code class="language-bash">yarn add babel-plugin-styled-components styled-components</code></pre>
    
- Create a `.babelrc` file at the root of your app, and a `pages/_document.js` file, as shown in the before (left) and after(right) image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37e5780-2301-482e-bef0-383fbb7881b7/new-files-document-babelrc-added.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37e5780-2301-482e-bef0-383fbb7881b7/new-files-document-babelrc-added.png" sizes="100vw" caption="New files added: <code>_document.js</code> and <code>.babelrc</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37e5780-2301-482e-bef0-383fbb7881b7/new-files-document-babelrc-added.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after adding two new files - <code>_.document.js</code> and <code>.babelrc</code>" >}}

- Update the [`.babelrc`](https://nextjs.org/docs/advanced-features/customizing-babel-config) file to include the `next/babel` preset and include the `styled-components` plugin, with server-side-rendering (ssr) enabled. 

<pre><code class="language-javascript">// .babelrc
{
  "presets": ["next/babel"],
  "plugins": [
    [
      "styled-components",
      {
        "ssr": true
      }
    ]
  ]
}</code></pre>

- Update `pages/_document.js` by *injecting the server-side rendered styles into the `<head>`*.

Keep in mind, the snippet below (`pages/_document.js`) is a **required** logic for styled-components to work with Next.js. You almost have to do *nothing* but copy the logic as pointed out in the [styled-components documentation](https://styled-components.com/docs/advanced#nextjs).

<pre><code class="language-javascript">// pages/_document.js
import Document from "next/document";
import {ServerStyleSheet} from "styled-components";

export default class MyDocument extends Document {
  static async getInitialProps(ctx) {
    const sheet = new ServerStyleSheet();
    const originalRenderPage = ctx.renderPage;

    try {
      ctx.renderPage = () =&gt;
        originalRenderPage({
          enhanceApp: (App) =&gt; (props) =&gt;
            sheet.collectStyles(&lt;App {...props} /&gt;),
        });

      const initialProps = await Document.getInitialProps(ctx);
      return {
        ...initialProps,
        styles: (
          &lt;&gt;
            {initialProps.styles}
            {sheet.getStyleElement()}
          &lt;/&gt;
        ),
      };
    } finally {
      sheet.seal();
    }
  }
}</code></pre>

After the updates to `.babelrc`, and `pages/_document.js`, we can now begin to use styled-components.

- Update `styles/styled-components/StyledBookSix.js`.

`styled` is an internal utility method that transforms the styling from JavaScript into actual CSS. `<StyledBookSix/>` is, and, can be used as any other React component.

<pre><code class="language-javascript">// styles/StyledBookSix.js
import styled from "styled-components";

const StyledBookSix = styled.div`
  color: #fff;
  width: 106px;
  height: 448px;
  margin-right: 23px;
  background-color: rebeccapurple;
`;

export default StyledBookSix;</code></pre>

> Learn more about [How To Use Styled-Components in React](https://www.smashingmagazine.com/2020/07/styled-components-react/).

- Import `styles/styled-components/StyledBookSix.js` in `components/BookSix.js`, using the imported styled-components `<StyledBookSix/>`.

<pre><code class="language-javascript">// components/BookSix.js
import StyledBookSix from "../styles/styled-components/StyledBookSix";

export default function BookSix() {
  return (
    &lt;StyledBookSix className="book-six"&gt;
      &lt;div className="book-info"&gt;
        &lt;p className="title"&gt;purple hibiscus&lt;/p&gt;
        &lt;p className="author"&gt;chimamanda ngozi adichie&lt;/p&gt;
      &lt;/div&gt;
    &lt;/StyledBookSix&gt;
  );
}</code></pre>

With the first to sixth step completed, the sixth should be styled, and the Bookshelf done:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00da961-2114-4886-92f1-c81f7deb32c8/book-six-styled-with-styled-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00da961-2114-4886-92f1-c81f7deb32c8/book-six-styled-with-styled-components.png" sizes="100vw" caption="BookSix styled with Styled Components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b00da961-2114-4886-92f1-c81f7deb32c8/book-six-styled-with-styled-components.png'>Large preview</a>)" alt="A screenshot of the change to the demo Bookshelf after styling the sixth book with Styled Components" >}}

That’s it.

If all went well, then you should have the complete Bookshelf with the books waiting to be read.

<ul>
  <li><a href="https://github.com/smashingmagazine/styling-in-next/tree/finished">You can grab the complete code on GitHub&nbsp;&rarr;</a></li>
</ul>

## Conclusion

In my own usage with Next.js, Global styles and styled-components have often been sufficient. But there’s no doubt that all these methods have their pros and cons. And as you settle on what method to use, just keep in mind: in the end, it’s all CSS. At this point, I believe you can be able to figure out which pattern best serves you in your next project.

### Resources

I find that for learning about setting up styling methods with Next.js, there’s no better place than its [official documentation.](https://nextjs.org/docs/basic-features/built-in-css-support)

But there are also specific repositories for various styling methods. You can go through the various repository to learn more, or check for update, as things may change incognito.

1. [Tailwind CSS](https://github.com/vercel/next.js/tree/canary/examples/with-tailwindcss)
2. [CSS Modules](https://github.com/css-modules/css-modules)
3. [Less](https://github.com/vercel/next-plugins/tree/master/packages/next-less)
4. [Stylus](https://github.com/vercel/next-plugins/tree/master/packages/next-stylus)
5. [Tailwind CSS with Emotion](https://github.com/vercel/next.js/tree/canary/examples/with-tailwindcss-emotion)
6. [Styletron](https://github.com/vercel/next.js/tree/canary/examples/with-styletron)
7. [Glamor](https://github.com/vercel/next.js/tree/canary/examples/with-glamor)
8. [CXS](https://github.com/vercel/next.js/tree/canary/examples/with-cxs)
9. [Aphrodite](https://github.com/vercel/next.js/tree/canary/examples/with-aphrodite)
10. [Fela](https://github.com/vercel/next.js/tree/canary/examples/with-fela)
11. [Styled-JSX](https://github.com/vercel/styled-jsx)

{{< signature "ks, ra, yk, il" >}}
