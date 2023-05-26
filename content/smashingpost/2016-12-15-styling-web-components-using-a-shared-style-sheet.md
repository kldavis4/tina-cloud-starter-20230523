---
title: Styling Web Components Using A Shared Style Sheet
slug: styling-web-components-using-a-shared-style-sheet
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb1e21c2-7386-472b-aeeb-18e32a083e95/custom-elements-perf-500w-opt.png
date: 2016-12-15T18:48:39.000Z
author: stevenlambert
description: >-
  Web components are an amazing new feature of the web, allowing developers to
  define their own custom HTML elements. When combined with a style guide, web
  components can create a component API, which allows developers to stop copying
  and pasting code snippets and instead just use a DOM element.

  By using the shadow DOM, we can encapsulate the web component and not have to
  worry about specificity wars with any other style sheet on the page. However,
  web components and style guides currently seem to be at odds with each other.
categories:
  - Coding
  - Web Components
---
<a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements?hl=en">Web components</a> are an amazing new feature of the web, allowing developers to define their own custom HTML elements. When combined with a style guide, web components can create a <a href="https://engineering.lonelyplanet.com/2014/05/18/a-maintainable-styleguide.html">component API</a>, which allows developers to stop copying and pasting code snippets and instead just use a DOM element. By using the shadow DOM, we can encapsulate the web component and not have to worry about <a href="https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/">specificity wars</a> with any other style sheet on the page.

However, web components and style guides currently seem to be at odds with each other. On the one hand, style guides provide a set of rules and styles that are globally applied to the page and ensure consistency across the website. On the other hand, web components with the shadow DOM prevent any global styles from penetrating their encapsulation, thus preventing the style guide from affecting them.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Enforcing Best Practices In Component-Based Systems](https://www.smashingmagazine.com/2017/01/styled-components-enforcing-best-practices-component-based-systems/)
*   [How To Use The LESS CSS Preprocessor For Smarter Style Sheets](https://www.smashingmagazine.com/2010/12/using-the-less-css-preprocessor-for-smarter-style-sheets/)
*   [A Deep Dive Into Adobe Edge Reflow](https://www.smashingmagazine.com/2015/02/deep-dive-into-adobe-edge-reflow/)

So, how can the two co-exist, with global style guides continuing to provide consistency and styles, even to web components with the shadow DOM? Thankfully, there are solutions that work today, and more solutions to come, that enable global style guides to provide styling to web components. (For the remainder of this article, I will use the term “web components" to refer to custom elements with the shadow DOM.)

{{% feature-panel %}}

## What Should A Global Style Guide Style In A Web Component?

Before discussing how to get a global style guide to style a web component, we should discuss what it should and should not try to style.

First of all, current <a href="https://webcomponents.org/articles/web-components-best-practices/">best practices for web components</a> state that a web component, including its styles, should be encapsulated, so that it does not depend on any external resources to function. This allows it to be used anywhere on or off the website, even when the style guide is not available.

Below is a simple log-in form web component that encapsulates all of its styles.</p>

<pre><code class="language-markup">&lt;template id="login-form-template"&gt;
  &lt;style&gt;
    :host {
      color: #333333;
      font: 16px Arial, sans-serif;
    }

    p {
      margin: 0;
    }

    p + p {
      margin-top: 20px;
    }

    a {
      color: #1f66e5;
    }

    label {
      display: block;
      margin-bottom: 5px;
    }

    input[type="text"],
    input[type="password"] {
      background-color: #eaeaea;
      border: 1px solid grey;
      border-radius: 4px;
      box-sizing: border-box;
      color: inherit;
      font: inherit;
      padding: 10px 10px;
      width: 100%;
    }

    input[type="submit"] {
      font: 16px/1.6 Arial, sans-serif;
      color: white;
      background: cornflowerblue;
      border: 1px solid #1f66e5;
      border-radius: 4px;
      padding: 10px 10px;
      width: 100%;
    }

    .container {
      max-width: 300px;
      padding: 50px;
      border: 1px solid grey;
    }

    .footnote {
      text-align: center;
    }
  &lt;/style&gt;

  &lt;div class="container"&gt;
    &lt;form action="#"&gt;
      &lt;p&gt;
        &lt;label for="username"&gt;User Name&lt;/label&gt;
        &lt;input type="text" id="username" name="username"&gt;
      &lt;/p&gt;
      &lt;p&gt;
        &lt;label for="password"&gt;Password&lt;/label&gt;
        &lt;input type="password" id="password" name="password"&gt;
      &lt;/p&gt;
      &lt;p&gt;
        &lt;input type="submit" value="Login"&gt;
      &lt;/p&gt;
      &lt;p class="footnote"&gt;Not registered? &lt;a href="#"&gt;Create an account&lt;/a&gt;&lt;/p&gt;
    &lt;/form&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
  const doc = (document._currentScript || document.currentScript).ownerDocument;
  const template = doc.querySelector('#login-form-template');

  customElements.define('login-form', class extends HTMLElement {
    constructor() {
      super();

      const root = this.attachShadow({mode: 'closed'});
      const temp = document.importNode(template.content, true);

      root.appendChild(temp);
    }
  });
&lt;/script&gt;
</code></pre>

<strong>Note:</strong> Code examples are written in the version 1 specification for web components.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5441497-22e2-4ea8-908f-a1e09600d7e4/login-form-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5441497-22e2-4ea8-908f-a1e09600d7e4/login-form-preview-opt.png" alt="Log-in form with user name and password." width="413" height="364" /></a><figcaption>A simple log-in form web component</figcaption></figure>

However, fully encapsulating every web component would inevitably lead to a lot of duplicate CSS, especially when it comes to setting up the typography and styling of native elements. If a developer wants to use a paragraph, an anchor tag or an input field in their web component, it should be styled like the rest of the website.

If we fully encapsulate all of the styles that the web component needs, then the CSS for styling paragraphs, anchor tags, input fields and so on would be duplicated across all web components that use them. This would not only increase maintenance costs, but also lead to much larger download sizes for users.

Instead of encapsulating all of the styles, web components should only encapsulate their unique styles and then depend on a set of shared styles to handle styles for everything else. These shared styles would essentially become a kind of <a href="https://necolas.github.io/normalize.css/">Normalize.css</a>, which web components could use to ensure that native elements are styled according to the style guide.

In the previous example, the log-in form web component would declare the styles for only its two unique classes: <code>.container</code> and <code>.footnote</code>. The rest of the styles would belong in the shared style sheet and would style the paragraphs, anchor tags, input fields and so on.

In short, the style guide should not try to style the web component, but instead should provide a set of shared styles that web components can use to achieve a consistent look.</p>

## How Styling The Shadow DOM With External Style Sheets Used To Be Done

The initial specification for web components (known as version 0) allowed any external style sheet to penetrate the shadow DOM through use of the <code>::shadow</code> or <code>/deep/</code> CSS selectors. The use of <code>::shadow</code> and <code>/deep/</code> enabled you to have a style guide penetrate the shadow DOM and set up the shared styles, whether the web component wanted you to or not.</p>

<pre><code class="language-markup">/* Style all p tags inside a web components shadow DOM */
login-form::shadow p {
  color: red;
}
</code></pre>

With the advent of the newest version of the web components specification (known as version 1), the authors have <a href="https://hayato.io/2016/shadowdomv1/#shadow-piercing-combinators">removed the capability</a> of external style sheets to penetrate the shadow DOM, and they have provided no alternative. Instead, the philosophy has changed from <a href="https://meowni.ca/posts/styling-the-dome/">using dragons to style web components</a> to instead using bridges. In other words, web component authors should be in charge of what external style rules are allowed to style their component, rather than being forced to allow them.

Unfortunately, that philosophy hasn’t really caught up with the web just yet, which leaves us in a bit of a pickle. Luckily, a few solutions available today, and some coming in the not-so-distant future, will allow a shared style sheet to style a web component.

## What You Can Do Today

There are three techniques you can use today that will allow a web component to share styles: <code>@import</code>, custom elements and a web component library.</p>

### Using @import

The only native way today to bring a style sheet into a web component is to use <code>@import</code>. Although this works, <a href="https://www.stevesouders.com/blog/2009/04/09/dont-use-import/">it’s an anti-pattern</a>. For web components, however, it’s an even bigger performance problem.</p>

<pre><code class="language-markup">&lt;template id="login-form-template"&gt;
  &lt;style&gt;
    @import "styleguide.css"
  &lt;/style&gt;

  &lt;style&gt;
    .container {
      max-width: 300px;
      padding: 50px;
      border: 1px solid grey;
    }

    .footnote {
      text-align: center;
    }
  &lt;/style&gt;

  &lt;!-- rest of template DOM --&gt;
&lt;/template&gt;
</code></pre>

Normally, <code>@import</code> is an anti-pattern because it downloads all style sheets in series, instead of in parallel, especially if they are nested. In our situation, downloading a single style sheet in series can’t be helped, so in theory it should be fine. But <a href="https://github.com/straker/webcomponent-perf/tree/master/shared-styles">when I tested</a> this in Chrome, the results showed that using <code>@import</code> caused the page to <a href="https://www.webpagetest.org/result/161023_VK_9ZC/">render up to a half second slower</a> than when just <a href="https://www.webpagetest.org/result/161023_2X_9ZB/">embedding the styles directly</a> into the web component.</p>

<strong>Note:</strong> Due to differences in how the <a href="https://webcomponents.org/polyfills/html-imports/#polyfill-notes">polyfill of HTML imports</a> works compared to native HTML imports, <a href="https://www.webpagetest.org/">WebPagetest.org</a> can only be used to give reliable results in browsers that natively support HTML imports (i.e. Chrome).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039833c6-cb34-4f89-b2b1-2afe5bfe52a4/native-web-components-perf-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039833c6-cb34-4f89-b2b1-2afe5bfe52a4/native-web-components-perf-preview-opt.png" alt="Bar graph of native web component performance." width="500" height="" /></a><figcaption>Results from three performance tests show that <code>@import</code> causes the browser to render up to a half second slower than when just embedding the styles directly into the web component.</figcaption></figure>

In the end, <code>@import</code> is still an anti-pattern and can be a performance problem in web components. So, it’s not a great solution.</p>

### Don’t Use the Shadow DOM

Because the problem with trying to provide shared styles to web components stems from using the shadow DOM, one way to avoid the problem entirely is to not use the shadow DOM.

By not using the shadow DOM, you will be creating <a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements?hl=en">custom elements</a> instead of web components (see the aside below), the only difference being the lack of the shadow DOM and scoping. Your element will be subject to the styles of the page, but we already have to deal with that today, so it’s nothing that we don’t already know how to handle. Custom elements are fully supported by the webcomponentjs polyfill, which has <a href="https://github.com/webcomponents/webcomponentsjs/tree/v1#browser-support">great browser support</a>.

The greatest benefit of custom elements is that you can <a href="https://medium.com/dev-channel/the-case-for-custom-elements-part-1-65d807b4b439">create a pattern library</a> using them today, and you don’t have to wait until the problem of shared styling is solved. And because the only difference between web components and custom elements is the shadow DOM, you can always enable the shadow DOM in your custom elements once a solution for shared styling is available.

If you do decide to create custom elements, be aware of a few differences between custom elements and web components.

First, because styles for the custom element are subject to the page styles and vice versa, you will want to ensure that your selectors don’t cause any conflicts. If your pages already use a style guide, then leave the styles for the custom element in the style guide, and have the element output the expected DOM and class structure.

By leaving the styles in the style guide, you will create a smooth migration path for your developers, because they can continue to use the style guide as before, but then slowly migrate to using the new custom element when they are able to. Once everyone is using the custom element, you can move the styles to reside inside the element in order to keep them together and to allow for easier refactoring to web components later.

Secondly, be sure to encapsulate any JavaScript code inside an immediately invoked function expression (IFFE), so that you don’t bleed any variables to the global scope. In addition to not providing CSS scoping, custom elements do not provide JavaScript scoping.

Thirdly, you’ll need to use the <code>connectedCallback</code> function of the custom element to <a href="https://stackoverflow.com/questions/40181683/failed-to-execute-createelement-on-document-the-result-must-not-have-childr">add the template DOM to the element</a>. According to the web component specification, custom elements should not add children during the constructor function, so you’ll need to defer adding the DOM to the <code>connectedCallback</code> function.

Lastly, the <code>&lt;slot&gt;</code> element does not work outside of the shadow DOM. This means that you’ll have to use a different method to provide a way for developers to insert their content into your custom element. Usually, this entails just manipulating the DOM yourself to insert their content where you want it.

However, because there is no separation between the shadow DOM and the light DOM with custom elements, you’ll also have to be very careful not to style the inserted DOM, due to your elements’ cascading styles.</p>

<pre><code class="language-markup">&lt;!-- login-form.html --&gt;
&lt;template id="login-form-template"&gt;
  &lt;style&gt;
    login-form .container {
      max-width: 300px;
      padding: 50px;
      border: 1px solid grey;
    }

    login-form .footnote {
      text-align: center;
    }
  &lt;/style&gt;

  &lt;!-- Rest of template DOM --&gt;
&lt;/template&gt;

&lt;script&gt;
(function() {
  const doc = (document._currentScript || document.currentScript).ownerDocument;
  const template = doc.querySelector('#login-form-template');

  customElements.define('login-form', class extends HTMLElement {
    constructor() {
      super();
    }

    // Without the shadow DOM, we have to manipulate the custom element
    // after it has been inserted in the DOM.
    connectedCallback() {
      const temp = document.importNode(template.content, true);
      this.appendChild(temp);
    }
  });
})();
&lt;/script&gt;
</code></pre>

<pre><code class="language-markup">&lt;!-- index.html --&gt;
&lt;link rel="stylesheet" href="styleguide.css"&gt;
&lt;link rel="import" href="login-form.html"&gt;

&lt;login-form&gt;&lt;/login-form&gt;
</code></pre>

In terms of performance, <a href="https://www.webpagetest.org/result/161025_CE_60T/">custom elements are almost as fast</a> as <a href="https://www.webpagetest.org/result/161023_5D_9ZA/">web components not being used</a> (i.e. linking the shared style sheet in the <code>head</code> and using only native DOM elements). Of all the techniques you can use today, this is by far the fastest.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec4ac785-d0a6-4a20-b87e-f5645fe1ae13/custom-elements-perf-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec4ac785-d0a6-4a20-b87e-f5645fe1ae13/custom-elements-perf-preview-opt.png" alt="Bar graph of custom element performance." width="500" height="" /></a><figcaption>The results from two performance tests show that custom elements are almost as fast as not using web components at all.</figcaption></figure>

<strong>Aside:</strong> A custom element is still a web component for all intents and purposes. The term “web components" is used to describe <a href="https://developer.mozilla.org/en-US/docs/Web/Web_Components">four separate technologies</a>: custom elements, template tags, HTML imports and the shadow DOM.

Unfortunately, the term has been used to describe anything that uses any combination of the four technologies. This has led to a lot of confusion around what people mean when they say “web component." <a href="https://medium.com/dev-channel/the-case-for-custom-elements-part-1-65d807b4b439#7d6c.tlzb4zis3">Just as Rob Dodson discovered</a>, I have found it helpful to use different terms when talking about custom elements with and without the shadow DOM.

Most of the developers I’ve talked to tend to associate the term “web component" with a custom element that uses the shadow DOM. So, for the purposes of this article, I have created an artificial distinction between a web component and a custom element.</p>

### Using a Web Component Library

Another solution you can use today is a web component library, such as <a href="https://www.polymer-project.org/">Polymer</a>, <a href="https://github.com/skatejs/skatejs">SkateJS</a> or <a href="https://x-tag.github.io/">X-Tag</a>. These libraries help fill in the holes of today’s support and can also simplify the code necessary to create a web component. They also usually provide added features that make writing web components easier.

For example, Polymer lets you create a simple web component in just a few lines of JavaScript. An added benefit is that Polymer provides a solution for <a href="https://www.polymer-project.org/1.0/docs/devguide/styling#style-modules">using the shadow DOM and a shared style sheet</a>. This means you can create web components today that share styles.

To do this, create what they call a style module, which contains all of the shared styles. It can either be a <code>&lt;style&gt;</code> tag with the shared styles inlined or a <code>&lt;link rel="import"&gt;</code> tag that points to a shared style sheet. In either case, include the styles in your web component with a <code>&lt;style include&gt;</code> tag, and then Polymer will parse the styles and add them as an inline <code>&lt;style&gt;</code> tag to your web component.</p>

<pre><code class="language-markup">&lt;!-- shared-styles.html --&gt;
&lt;dom-module id="shared-styles"&gt;
  &lt;!-- Link to a shared style sheet --&gt;
  &lt;!-- &lt;link rel="import" href="styleguide.css"&gt; --&gt;

  &lt;!-- Inline the shared styles --&gt;
  &lt;template&gt;
    &lt;style&gt;
    :host {
      color: #333333;
      font: 16px Arial, sans-serif;
    }

    /* Rest of shared CSS */
    &lt;/style&gt;
  &lt;/template&gt;
&lt;/dom-module&gt;
</code></pre>

<pre><code class="language-markup">&lt;!-- login-form.html --&gt;
&lt;link rel="import" href="../polymer/polymer.html"&gt;
&lt;link rel="import" href="../shared-styles/shared-styles.html"&gt;

&lt;dom-module id="login-form"&gt;
  &lt;template&gt;
    &lt;!-- Include the shared styles --&gt;
    &lt;style include="shared-styles"&gt;&lt;/style&gt;

    &lt;style&gt;
      .container {
        max-width: 300px;
        padding: 50px;
        border: 1px solid grey;
      }

      .footnote {
        text-align: center;
      }
    &lt;/style&gt;

    &lt;!-- Rest of template DOM --&gt;
  &lt;/template&gt;

  &lt;script&gt;
  Polymer({
    is: 'login-form'
  });
  &lt;/script&gt;
&lt;/dom-module&gt;
</code></pre>

The only downside to using a library is that it can delay the rendering time of your web components. This shouldn’t come as a surprise because downloading the library’s code and processing it take time. Any web components on the page can’t begin rendering until the library is done processing.

In Polymer’s case, it can delay the page-rendering time by up to half a second compared to native web components. A <a href="https://www.webpagetest.org/result/161101_AT_73B/">style module that embeds the styles</a> is slightly slower than a <a href="https://www.webpagetest.org/result/161101_CB_73C/">style module that links the styles</a>, and <a href="https://www.webpagetest.org/result/161101_XK_73A/">embedding the styles directly into the web component</a> is just as fast as using a style module.

Again, Polymer does nothing in particular to make the rendering time slower. Downloading the Polymer library and processing all of its awesome features, plus creating all of the template bindings, take time. It’s just the trade-off you’ll have to make to use a web component library.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cca87d2a-8abe-4b77-b23a-802ab32439c8/polymer-web-components-perf-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cca87d2a-8abe-4b77-b23a-802ab32439c8/polymer-web-components-perf-preview-opt.png" alt="Bar graph of Polymer web component performance." width="500" height="" /></a></figure>

Results from performance tests show that, using Polymer, web components will render up to half a second slower than native web components.</p>

## The Promise Of The Future

If none of the current solutions work for you, don’t despair. If all goes well, within a few months to a few years, we’ll be able to use shared styles using a few different approaches.</p>

### Custom Properties

<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables">Custom properties</a> (or <a href="https://www.youtube.com/watch?v=2an6-WVPuJU">CSS variables</a>, as they’ve been called) are a way to set and use variables in CSS. This notion is not new to CSS preprocessors, but as a native CSS feature, custom properties are actually <a href="https://csswizardry.com/2016/10/pragmatic-practical-progressive-theming-with-custom-properties/">more powerful than a preprocessor variable</a>.

To declare a custom property, use the custom property notation of <code>--my-variable: value</code>, and access the variable using <code>property: var(--my-variable)</code>. A custom property cascades like any other CSS rule, so its value inherits from its parent and can be overridden. The only caveat to custom properties is that they must be declared inside a selector and cannot be declared on their own, unlike a preprocessor variable.</p>

<pre><code class="language-markup">&lt;style&gt;
/* Declare the custom property */
html {
  --main-bg-color: red;
}

/* Use the custom property */
input {
  background: var(--main-bg-color);
}
&lt;/style&gt;
</code></pre>

One thing that makes custom properties so powerful is their ability to pierce the shadow DOM. This isn’t the same idea as the <code>/deep/</code> and <code>::shadow</code> selectors because they don’t force their way into the web component. Instead, the author of the web component must use the custom property in their CSS in order for it to be applied. This means that a web component author can create a custom property API that consumers of the web component can use to apply their own styles.</p>

<pre><code class="language-markup">&lt;template id="my-element-template"&gt;
  &lt;style&gt;
  /* Declare the custom property API */
  :host {
    --main-bg-color: brown;
  }

  .one {
    color: var(--main-bg-color);
  }
  &lt;/style&gt;

  &lt;div class="one"&gt;Hello World&lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
/* Code to set up my-element web component */
&lt;/script&gt;

&lt;my-element&gt;&lt;/my-element&gt;

&lt;style&gt;
/* Override the custom variable with own value */
my-element {
  --main-bg-color: red;
}
&lt;/style&gt;
</code></pre>

Browser support for custom properties is <a href="https://caniuse.com/#search=custom%20properties">surprisingly good</a>. The only reason it is not a solution you can use today is that there is <a href="https://github.com/webcomponents/shadycss/issues/11">no working polyfill</a> without Custom Elements version 1. The team behind the webcomponentjs polyfill is <a href="https://github.com/Polymer/polymer/tree/2.0-preview#polymer-20-goals">currently working to add it</a>, but it is not yet released and in a built state, meaning that if you hash your assets for production, you can’t use it. From what I understand, it’s due for release sometime early next year.

Even so, custom properties are not a good method for sharing styles between web components. Because they can only be used to declare a single property value, the web component would still need to embed all of the styles of the style guide, albeit with their values substituted with variables.

Custom properties are more suited to theming options, rather than shared styles. Because of this, custom properties are not a viable solution to our problem.

/* Use the custom property */
input {
  background: var(--main-bg-color);
}
&lt;/style&gt;
</code></pre>

One thing that makes custom properties so powerful is their ability to pierce the shadow DOM. This isn’t the same idea as the <code>/deep/</code> and <code>::shadow</code> selectors because they don’t force their way into the web component. Instead, the author of the web component must use the custom property in their CSS in order for it to be applied. This means that a web component author can create a custom property API that consumers of the web component can use to apply their own styles.</p>

<pre><code class="language-markup">&lt;template id="my-element-template"&gt;
  &lt;style&gt;
  /* Declare the custom property API */
  :host {
    --main-bg-color: brown;
  }

  .one {
    color: var(--main-bg-color);
  }
  &lt;/style&gt;

  &lt;div class="one"&gt;Hello World&lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
/* Code to set up my-element web component */
&lt;/script&gt;

&lt;my-element&gt;&lt;/my-element&gt;

&lt;style&gt;
/* Override the custom variable with own value */
my-element {
  --main-bg-color: red;
}
&lt;/style&gt;
</code></pre>

Browser support for custom properties is <a href="https://caniuse.com/#search=custom%20properties">surprisingly good</a>. The only reason it is not a solution you can use today is that there is <a href="https://github.com/webcomponents/shadycss/issues/11">no working polyfill</a> without Custom Elements version 1. The team behind the webcomponentjs polyfill is <a href="https://github.com/Polymer/polymer/tree/2.0-preview#polymer-20-goals">currently working to add it</a>, but it is not yet released and in a built state, meaning that if you hash your assets for production, you can’t use it. From what I understand, it’s due for release sometime early next year.

Even so, custom properties are not a good method for sharing styles between web components. Because they can only be used to declare a single property value, the web component would still need to embed all of the styles of the style guide, albeit with their values substituted with variables.

Custom properties are more suited to theming options, rather than shared styles. Because of this, custom properties are not a viable solution to our problem.</p>

### @apply Rules

In addition to custom properties, CSS is also getting <a href="https://tabatkins.github.io/specs/css-apply-rule/"><code>@apply</code> rules</a>. Apply rules are essentially <a href="https://blog.hospodarets.com/css_apply_rule">mixins for the CSS world</a>. They are declared in a similar fashion to custom properties but can be used to declare groups of properties instead of just property values. Just like custom properties, their values can be inherited and overridden, and they must be declared inside a selector in order to work.</p>

<pre><code class="language-markup">&lt;style&gt;
/* Declare rule */
html {
  --typography: {
    font: 16px Arial, sans-serif;
    color: #333333;
  }
}

/* Use rule */
input {
  @apply --typography;
}
&lt;/style&gt;
</code></pre>

Browser support for <code>@apply</code> rules is basically non-existent. <a href="https://www.chromestatus.com/feature/5753701012602880">Chrome currently supports it</a> behind a feature flag (which I couldn’t find), but that’s about it. There is also no working polyfill for the same reason as there is no polyfill for custom properties. The webcomponentjs polyfill team is also working to add <code>@apply</code> rules, along with custom properties, so both will be available once the new version is released.

Unlike custom properties, <code>@apply</code> rules are a much better solution for sharing styles. Because they can set up a group of property declarations, you can use them to set up the default styling for all native elements and then use them inside the web component. To do this, you would have to create an <code>@apply</code> rule for every native element.

However, to consume the styles, you would have to apply them manually to each native element, which would still duplicate the style declaration in every web component. While that’s better than embedding all of the styles, it isn’t very convenient either because it becomes boilerplate at the top of every web component, which you have to remember to add in order for styles to work properly.</p>

<pre><code class="language-css">/* styleguide.css */
html {
  --typography: {
    color: #333333;
    font: 16px Arial, sans-serif;
  }

  --paragraph: {
    margin: 0;
  }

  --label {
    display: block;
    margin-bottom: 5px;
  }

  --input-text {
    background-color: #eaeaea;
    border: 1px solid grey;
    border-radius: 4px;
    box-sizing: border-box;
    color: inherit;
    font: inherit;
    padding: 10px 10px;
    width: 100%;
  }

  --input-submit {
    font: 16px/1.6 Arial, sans-serif;
    color: white;
    background: cornflowerblue;
    border: 1px solid #1f66e5;
    border-radius: 4px;
    padding: 10px 10px;
    width: 100%;
  }

  /* And so on for every native element */
}
</code></pre>

<pre><code class="language-markup">&lt;!-- login-form.html --&gt;
&lt;template id="login-form-template"&gt;
  &lt;style&gt;
    :host {
      @apply --typography;
    }

    p {
      @apply --paragraph;
    }

    label {
      @apply --label;
    }

    input-text {
      @apply --input-text;
    }

    .input-submit {
      @apply --input-submit;
    }

    .container {
      max-width: 300px;
      padding: 50px;
      border: 1px solid grey;
    }

    .footnote {
      text-align: center;
    }
  &lt;/style&gt;

  &lt;!-- Rest of template DOM --&gt;
&lt;/template&gt;
</code></pre>

Due to the need for extensive boilerplate, I don’t believe that <code>@apply</code> rules would be a good solution for sharing styles between web components. They are a great solution for theming, though.</p>

### <link rel="stylesheet"> in the Shadow DOM

According to the <a href="https://w3c.github.io/webcomponents/spec/shadow/#inertness-of-html-elements-in-a-shadow-tree">web component specification</a>, browsers ignore any <code>&lt;link rel="stylesheet"&gt;</code> tags in the shadow DOM, treating them just like they would inside of a document fragment. This prevented us from being able to link in any shared styles in our web components, which was unfortunate — that is, until a few months ago, when the Web Components Working Group proposed that <a href="https://github.com/w3c/webcomponents/issues/530"><code>&lt;link rel="stylesheet"&gt;</code> tags should work in the shadow DOM</a>. After only a week of discussion, they all agreed that they should, and a few days later they <a href="https://github.com/whatwg/html/pull/1572">added it to the HTML specification</a>.</p>

<pre><code class="language-markup">&lt;template id="login-form-template"&gt;
  &lt;link rel="stylesheet" href="styleguide.css"&gt;

  &lt;style&gt;
    .container {
      max-width: 300px;
      padding: 50px;
      border: 1px solid grey;
    }

    .footnote {
      text-align: center;
    }
  &lt;/style&gt;

  &lt;!-- rest of template DOM --&gt;
&lt;/template&gt;
</code></pre>

If that sounds a little too quick for the working group to agree on a specification, that’s because it wasn’t a new proposal. Making <code>link</code> tags work in the shadow DOM was actually <a href="https://www.w3.org/Bugs/Public/show_bug.cgi?id=22539">proposed at least three years ago</a>, but it was backlogged until they could ensure it wasn’t a problem for performance.

If acceptance of the proposal isn’t exciting enough, Chrome 55 (currently Chrome Canary) <a href="https://codereview.chromium.org/2177163002/">added the initial functionality</a> of making <code>link</code> tags work in the shadow DOM. It even seems that this functionality <a href="https://jsfiddle.net/straker/vj6vc7pn/">has landed in the current version of Chrome</a>. Even <a href="https://developer.apple.com/safari/technology-preview/release-notes/">Safari has implemented the feature in Safari 18</a>.

Being able to link in the shared styles is by far the most convenient method for sharing styles between web components. All you would have to do is create the <code>link</code> tag, and all native elements would be styled accordingly, without requiring any additional work.

Of course, the way browser makers implement the feature will determine whether this solution is viable. For this to work properly, <code>link</code> tags would need to be deduplicated, so that multiple web components requesting the same CSS file would cause only one HTTP request. The CSS would also need to be parsed only once, so that each instance of the web component would not have to recompute the shared styles, but would instead reuse the computed styles.

Chrome <a href="https://github.com/w3c/webcomponents/issues/282#issuecomment-122186756">does both of these</a> already. So, if all other browser makers implement it the same way, then <code>link</code> tags working in the shadow DOM would definitely solve the issue of how to share styles between web components.</p>

### Constructable Style Sheets

You might find it hard to believe, since we haven’t even got it yet, but a <code>link</code> tag working in the shadow DOM is <a href="https://github.com/w3c/webcomponents/issues/530#issuecomment-231310687">not a long-term solution</a>. Instead, it’s just a short-term solution to get us to the real solution: constructable style sheets.</p>

<a href="https://tabatkins.github.io/specs/construct-stylesheets/">Constructable style sheets</a> are a proposal to allow for the creation of <code>StyleSheet</code> objects in JavaScript through a constructor function. The constructed style sheet could then be added to the shadow DOM through an API, which would allow the shadow DOM to use a set of shared styles.

Unfortunately, this is all I could gather from the proposal. I tried to find out more information about what constructable style sheets were by <a href="https://github.com/w3c/webcomponents/issues/501">asking the Web Components Working Group</a>, but they redirected me to the W3C’s CSS Working Group’s <a href="https://lists.w3.org/Archives/Public/www-style/2016May/0218.html">mailing list</a>, where I asked again, but no one responded. I couldn’t even figure out how the proposal was progressing, because it <a href="https://github.com/tabatkins/specs/tree/gh-pages/construct-stylesheets">hasn’t been updated in over two years</a>.

Even so, the Web Components Working Group <a href="https://github.com/w3c/webcomponents/issues/82#issuecomment-197300382">uses it</a> as <a href="https://github.com/w3c/webcomponents/issues/99#issuecomment-197685253"><em>the</em> solution</a> for <a href="https://github.com/w3c/webcomponents/issues/530#issuecomment-231310687">sharing styles</a> between web components. Hopefully, either the proposal will be updated or the Web Components Working Group will release more information about it and its adoption. Until then, the “long-term" solution seems like it won’t happen in the foreseeable future.</p>

## Lessons Learned

After months of research and testing, I am quite hopeful for the future. It is comforting to know that after years of not having a solution for sharing styles between web components, there are finally answers. Those answers might not be established for a few more years, but at least they are there.

If you want to use a shared style guide to style web components today, either you can not use the shadow DOM and instead create custom elements, or you can use a web component library that polyfills support for sharing styles. Both solutions have their pros and cons, so use whichever works best for your project.

If you decide to wait a while before delving into web components, then in a few years we should have some great solutions for sharing the styles between them. So, keep checking back on how it’s progressing.</p>

## Things To Keep In Mind

Keep in mind a few things if you decide to use custom elements or web components today.

Most importantly, the web component specification is still being actively developed, which means that things can and will change. Web components are still very much the bleeding edge, so be prepared to stay on your toes as you develop with it.

If you decide to use the shadow DOM, know that it is quite <a href="https://github.com/Polymer/polymer/issues/2389">slow</a> and <a href="https://news.ycombinator.com/item?id=11654362">unperformant</a> in <a href="https://www.polymer-project.org/1.0/blog/shadydom#shadow-dom-is-awesome-why-is-there-a-shady-dom">polyfilled browsers</a>. It was for this reason that Polymer’s developers created their shady DOM implementation and made it their default.

Chrome, Opera and, recently, <a href="https://developer.apple.com/library/prerelease/content/releasenotes/General/WhatsNewInSafari/Articles/Safari_10_0.html">Safari</a> are the only browsers that support the <a href="https://caniuse.com/#feat=shadowdom">shadow DOM version 0</a>. Firefox is still in development, although it has <a href="https://developer.mozilla.org/en-US/docs/Web/Web_Components#Enabling_Web_Components_in_Firefox">supported it behind an experiment</a> since version 29. Microsoft is <a href="https://developer.microsoft.com/en-us/microsoft-edge/platform/status/shadowdom">still considering it</a> for Edge and has it as a high priority on its road map.

However, shadow DOM version 0 is the old specification. <a href="https://hayato.io/2016/shadowdomv1/">Shadow DOM version 1</a> is the new one, and only Chrome, Safari and Opera <a href="https://caniuse.com/#feat=shadowdomv1">fully support it</a>. Not to mention that <a href="https://caniuse.com/#feat=custom-elements">custom elements version 0</a> went through the same upgrade, and only Chrome <a href="https://caniuse.com/#feat=custom-elementsv1">fully supports custom elements version 1</a>, whereas <a href="https://webkit.org/blog/7071/release-notes-for-safari-technology-preview-17/">Safari technical preview supports it as of version 17</a>. Custom elements version 1 has some major changes in how web components are written, so be sure to <a href="https://developers.google.com/web/fundamentals/getting-started/primers/customelements">fully understand what that entails</a>.

Lastly, the webcomponentjs polyfill only supports the version 0 implementation of the shadow DOM and custom elements. A <a href="https://github.com/webcomponents/webcomponentsjs/tree/v1">version 1 branch of the polyfill</a> will support version 1, but it’s not yet released.

{{< signature "il, vf, yk, al" >}}

