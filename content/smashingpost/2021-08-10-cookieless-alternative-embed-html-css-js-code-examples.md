---
title: 'Cookieless Alternative To Embed HTML, CSS And JS Code Snippets'
slug: cookieless-alternative-embed-html-css-js-code-examples
author: henrik-fricke
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fa2ab15-b98d-48b5-ab26-8a1fde75c13f/cookieless-alternative-embed-html-css-js-code-examples.jpg
date: 2021-08-10T11:45:00.000Z
summary: >-
  Embedding code examples with third-party scripts often leads to tracking or cookies. We always wanted to have a simple website with a good UX, so setting cookies for no reason wasn’t an option for us. Now, with Indiepen, we are proud to introduce a privacy-friendly alternative.
description: >-
  Embedding code examples with third-party scripts often leads to tracking or cookies. We always wanted to have a simple website with a good UX, so setting cookies for no reason wasn’t an option for us. Now, with Indiepen, we are proud to introduce a privacy-friendly alternative.
categories:
  - HTML
  - CSS
  - JavaScript
  - Tools
disable_ads: true
---

When we implement websites today, we are **confronted by a lot of things** we need to take care of. Ideally, we want to have a fast, secure, accessible, and fair website. At the same time, we want to have an interactive website with comments, polls, videos, code examples, and many more. 

Together with a friend, I launched a tech blog last year and we ran exactly into that issue. We wanted to have a simple solution to embedding HTML, CSS, and JavaScript code examples but existing solutions often include **tracking, cookies**, a ton of features or bad performance. After some research, we realized that we had to build an alternative.

Let’s have a look: 

<iframe src="https://indiepen.tech/embed/?url=https%3A%2F%2Findiepen.tech%2Fexample%2F" style="width: 100%; overflow: hidden; display: block; border: 0; margin-bottom: 1.4em" title="indiepen example" loading="lazy" width="100%" height="500"></iframe>

[Indiepen](https://indiepen.tech/) is a **privacy-friendly, lightweight,** and accessible solution to embed code examples. In fact, we don’t set any cookies or tracking! 

## Get Started

Indiepen can preview every website that follows a very simple convention. You need to provide a website with the following file structure: 

<pre><code class="language-bash">.
├── index.html
├── main.js
└── styles.css</code></pre>

Deploy the code example with your favorite hosting provider (e.g. GitHub Pages, Netlify, or Vercel) and copy the URL. After that, go to [our start page](https://indiepen.tech/#code-snippet-generator) and use the code snippet generator. 

The generated code looks like this:

<pre><code class="language-html">&lt;iframe class="indiepen"
  src="https://indiepen.tech/embed/?url=https%3A%2F%2Findiepen.tech%2Fexample%2F&tab=result"
  style="width: 100%; overflow: hidden; display: block; border: 0;"
  title="Indiepen Embed"
  loading="lazy"
  width="100%"
  height="450"&gt;
&lt;/iframe&gt;</code></pre>

You can now use the code snippet and integrate it on your website. That’s it! You should now see your code example with an editor to discover the code. 

## Under The Hood

It sounds a bit strange nowadays but we haven’t used any JavaScript framework like React or Vue.js. It’s **pure HTML, CSS and JavaScript** with some help from Lea Verou’s [Prism.js](https://prismjs.com/) for syntax highlighting. Those libraries are very helpful to implement and maintain complex web applications but in our case, we just have three files we need to fetch and pass onto Prism.js.

Additionally, we have three buttons in the upper right corner to **switch between the HTML, CSS, and JavaScript views**. By introducing a UI framework, we couldn’t deliver a lightweight solution with less than 20 kb in size. For us, it was good learning, that UI libraries are important in our day-to-day business but we should carefully consider them and don’t forget the good old vanilla JavaScript.

{{% feature-panel %}}

## Final Words

[Indiepen](https://indiepen.tech/) is our first open-source project and we are very excited to share our ideas with you. We would love to get feedback and have discussions about a fair web. Get in touch with me on [Twitter](https://twitter.com/henrik_fricke) or check out the project on [GitHub](https://github.com/yetanother-blog/indiepen/). 

Last but not least, I’d like to mention that Indiepen has a limited scope and we want to **keep it simple by design**. If you need to deal with more complex code examples, preprocessors for CSS or JavaScript, or you want to benefit from a platform to share your ideas, then please consider more sophisticated solutions like [CodePen](https://codepen.io/) or [JSFiddle](https://jsfiddle.net/). 

Happy coding, everyone!

{{< signature "vf, yk, il" >}}
