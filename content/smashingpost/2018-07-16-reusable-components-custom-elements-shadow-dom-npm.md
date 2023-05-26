---
title: 'The Holy Grail Of Reusable Components: Custom Elements, Shadow DOM, And NPM'
slug: reusable-components-custom-elements-shadow-dom-npm
author: oliver-williams
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2ac1b2e-92a2-44b7-a7bb-2c8357304b5a/frameworkgraph-800w.png
date: 2018-07-16T13:30:58+02:00
summary:
  This article looks at augmenting HTML with components that have built-in functionality and styles. We’ll also learn how to make these custom elements reusable across projects using NPM.
description:
  This article looks at augmenting HTML with components that have built-in functionality and styles. We’ll also learn how to make these custom elements reusable across projects using NPM.
categories:
  - Accessibility
  - HTML
  - CSS
  - JavaScript
---
<p>For even the simplest of components, the cost in human-labour may have been significant. UX teams do usability testing. An array of stakeholders have to sign off on the design.</p>

<p>Developers conduct AB tests, accessibility audits, unit tests and cross-browser checks. Once you’ve solved a problem, <em>you don’t want to repeat that effort</em>. By building a reusable component library (rather than building everything from scratch), we can continuously utilize past efforts and avoid revisiting already solved design and development challenges.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd61c2a7-6c87-42c0-864c-624bc0e0403f/materialcomponents.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd61c2a7-6c87-42c0-864c-624bc0e0403f/materialcomponents.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd61c2a7-6c87-42c0-864c-624bc0e0403f/materialcomponents.png'>Large preview</a>" alt="A screenshot of Google’s material components website – showing various components." >}}

<p>Building an arsenal of components is particularly useful for companies such as Google that own a considerable portfolio of websites all sharing a common brand. By codifying their UI into composable widgets, larger companies can both speed up development time and achieve consistency of both visual and user-interaction design across projects. There’s been a rise in interest in style guides and pattern libraries over the last several years. Given multiple developers and designers spread over multiple teams, large companies seek to attain consistency. We can do better than simple color swatches. <strong>What we need is easily distributable code</strong>.</p>

### Sharing And Reusing Code

<p>Manually copy-and-pasting code is effortless. Keeping that code up-to-date, however, is a maintenance nightmare. Many developers, therefore, rely on a package manager to reuse code across projects. Despite its name, the Node Package Manager has become the unrivalled platform for <em>front-end</em> package management. There are currently over 700,000 packages in the NPM registry and <em>billions</em> of packages are downloaded every month. Any folder with a package.json file can be uploaded to NPM as a shareable package. While NPM is primarily associated with JavaScript, a package can include CSS and markup. NPM makes it easy to reuse and, importantly, <em>update</em> code. Rather than needing to amend code in myriad places, you change the code only in the package.</p>

{{% feature-panel %}}

### The Markup Problem

<p>Sass and Javascript are easily portable with the use of import statements. Templating languages give HTML the same ability &mdash; templates can import other fragments of HTML in the form of partials. You can write the markup for your footer, for example, just once, then include it in other templates. To say there exists a multiplicity of templating languages would be an understatement. Tying yourself to <em>just one</em> severely limits the potential reusability of your code. The alternative is to copy-and-paste markup and to use NPM only for styles and javascript.</p>

<p>This is the approach taken by the Financial Times with their <a href="https://origami.ft.com"><em>Origami</em></a> component library. In her talk “<a href="https://www.youtube.com/watch?v=LAVNOQroZYA">Can't You Just Make It More like Bootstrap?</a>” Alice Bartlett concluded “there is no good way to let people include templates in their projects”. Speaking about his experience of maintaining a component library at Lonely Planet, <a href="https://www.ianfeather.co.uk/a-maintainable-style-guide/">Ian Feather reiterated the problems with this approach:</a></p>

<blockquote>“Once they copy that code they are essentially cutting a version which needs to be maintained indefinitely. When they copied the markup for a working component it had an implicit link to a snapshot of the CSS at that point. If you then update the template or refactor the CSS, you need to update all versions of the template scattered around your site.”</blockquote>

### A Solution: Web Components

<p>Web components solve this problem by defining markup in JavaScript. The author of a component is free to alter markup, CSS, and Javascript. The consumer of the component can benefit from these upgrades without needing to trawl through a project altering code by hand. Syncing with the latest changes project-wide can be achieved with a terse <code>npm update</code> via terminal. Only the name of the component and its API need to stay consistent.</p>

<p>Installing a web component is as simple as typing <code>npm install component-name</code> into a terminal. The Javascript can be included with an import statement:</p>

<pre><code class="language-css">&lt;script type="module"&gt;
import './node_modules/component-name/index.js';
&lt;/script&gt;
</code></pre>

<p>Then you can use the component anywhere in your markup. Here is a simple example component that copies text to the clipboard.</p>

{{< codepen height="480" theme_id="light" slug_hash="KemvbM" default_tab="result" user="cssgrid" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/cssgrid/pen/KemvbM/">Simple web component demo</a> by CSS GRID (<a href="https://codepen.io/cssgrid">@cssgrid</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

<p>A component-centric approach to front-end development has become ubiquitous, ushered in by Facebook’s React framework. Inevitably, given the pervasiveness of frameworks in modern front-end workflows, a number of companies have built component libraries using their framework of choice. Those components are reusable only within that particular framework.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5cdd3ce-b918-405b-b709-0b6a9a60f5eb/reactonly.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5cdd3ce-b918-405b-b709-0b6a9a60f5eb/reactonly.png" sizes="100vw" caption="A component from IBM’s Carbon Design System. For use in React applications only. Other significant examples of component libraries built in React include <a href='https://atlaskit.atlassian.com/packages'>Atlaskit</a> from Atlassian and <a href='https://polaris.shopify.com/components/get-started/'>Polaris</a> from Shopify. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5cdd3ce-b918-405b-b709-0b6a9a60f5eb/reactonly.png'>Large preview</a>)" alt="A component from IBM’s Carbon Design System" >}}

<p>It’s rare for a sizeable company to have a uniform front-end and replatorming from one framework to another isn’t uncommon. Frameworks come and go. To enable the maximum amount of potential reuse across projects, we need components that are <em>framework agnostic</em>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb17761-cd4a-4de8-aa1c-518eef1a6281/fragmented.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb17761-cd4a-4de8-aa1c-518eef1a6281/fragmented.png" sizes="100vw" caption="Searching for components via <a href='https://www.npmjs.com'>npmjs.com</a> reveals a fragmented Javascript ecosystem. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb17761-cd4a-4de8-aa1c-518eef1a6281/fragmented.png'>Large preview</a>)" alt="A screenshot from npmjs.com showing components that do that same thing built exclusively for particular javascript frameworks." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d9a4a9-4ee2-4982-ac18-e3f3257bbe16/frameworkgraph.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d9a4a9-4ee2-4982-ac18-e3f3257bbe16/frameworkgraph.png" sizes="100vw" caption="The ever-changing popularity of frameworks over time. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d9a4a9-4ee2-4982-ac18-e3f3257bbe16/frameworkgraph.png'>Large preview</a>)" alt="A graph charting the popularity of frameworks over time. Ember, Knockout and Backbone have plunged in popularity, replaced by newer offerings." >}}

<blockquote>“I have built web applications using: Dojo, Mootools, Prototype, jQuery, Backbone, Thorax, and React over the years...I would love to have been able to bring that killer Dojo component that I slaved over with me to my React app of today.”<br /><br />&mdash; <a href="https://medium.com/ben-and-dion/web-components-building-web-tools-for-future-dion-1d0e731c96d2">Dion Almaer</a>, Director of Engineering, Google</blockquote>

<p>When we talk about a web component, we are talking about the combination of a custom element with shadow DOM. Custom Elements and shadow DOM are part of both the W3C DOM specification and the WHATWG DOM Standard &mdash; <em>meaning web components are a web standard</em>. Custom elements and shadow DOM are <em>finally</em> set to achieve cross-browser support this year. By using a standard part of the native web platform, we ensure that our components can survive the fast-moving cycle of front-end restructuring and architectural rethinks. Web components can be used with any templating language and any front-end framework &mdash; they’re truly cross-compatible and interoperable. They can be used everywhere from a Wordpress blog to a single page application.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8727121e-eefc-44b8-8ef4-1b64f3bbb432/frameworkcompat.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8727121e-eefc-44b8-8ef4-1b64f3bbb432/frameworkcompat.png" sizes="100vw" caption="The <a href='https://custom-elements-everywhere.com/'>Custom Elements Everywhere</a> project by Rob Dodson documents the interoperability of web components with various client-side Javascript frameworks. React, the outlier here, will hopefully resolve these issues with React 17. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8727121e-eefc-44b8-8ef4-1b64f3bbb432/frameworkcompat.png'>Large preview</a>)" alt="The Custom Elements Everywhere project by Rob Dodson documents the interoperability of web components with various client-side Javascript frameworks." >}}

## Making A Web Component

### Defining A Custom Element

<p>It's always been possible to make up tag-names and have their content appear on the page.</p>

<pre><code class="language-html">&lt;made-up-tag&gt;Hello World!&lt;/made-up-tag&gt;</code></pre>

<p>HTML is designed to be fault tolerant. The above will render, even though it’s not a valid HTML element. There’s never been a good reason to do this &mdash; deviating from standardized tags has traditionally been a bad practice. By defining a new tag using the custom element API, however, we can augment HTML with reusable elements that have built-in functionality. Creating a custom element is much like creating a component in React &mdash; but here were extending <code>HTMLElement</code>.</p>

<pre><code class="language-css">class ExpandableBox extends HTMLElement {
      constructor() {
        super()
      }
    }
</code></pre>

<p>A parameter-less call to <code>super()</code> must be the first statement in the constructor. The constructor should be used to set up initial state and default values and to set up any event listeners.  A new custom element needs to be defined with a name for its HTML tag and the elements corresponding class:</p>

<pre><code class="language-css">customElements.define('expandable-box', ExpandableBox)</code></pre>

<p>It’s a convention to capitalize class names. The syntax of the HTML tag is, however, more than a convention. What if browsers wanted to implement a new HTML element and they wanted to call it expandable-box? To prevent naming collisions, no new standardized HTML tags will include a dash. By contrast, the names of custom elements <em>have to</em> include a dash.</p>

<pre><code class="language-css">customElements.define('whatever', Whatever) // invalid
customElements.define('what-ever', Whatever) // valid
</code></pre>

{{% ad-panel-leaderboard %}}

### Custom Element Lifecycle

<p>The API offers four custom element <em>reactions</em> &mdash; functions that can be defined within the class that will automatically be called in response to certain events in the lifecycle of a custom element.</p>

<p><strong>connectedCallback</strong> is run when the custom element is added to the DOM.</p>

<pre><code class="language-css">connectedCallback() {
    console.log("custom element is on the page!")
}
</code></pre>

<p>This includes adding an element with Javascript:</p>

<pre><code class="language-javascript">document.body.appendChild(document.createElement("expandable-box")) //“custom element is on the page”</code></pre>

<p>as well as simply including the element within the page with a HTML tag:</p>

<pre><code class="language-html">&lt;expandable-box&gt;&lt;/expandable-box&gt; // "custom element is on the page"</code></pre>

<p>Any work that involves fetching resources or rendering should be in here.</p>

<p><strong>disconnectedCallback</strong> is run when the custom element is removed from the DOM.</p>

<pre><code class="language-javascript">disconnectedCallback() {
    console.log("element has been removed")
}
document.querySelector("expandable-box").remove() //"element has been removed"
</code></pre>

<p><code>adoptedCallback</code> is run when the custom element is adopted into a new document. You probably don’t need to worry about this one too often.</p>

<p><code>attributeChangedCallback</code> is run when an attribute is added, changed, or removed. It can be used to listen for changes to both standardized native attributes like <em>disabled</em> or <em>src</em>, as well as any custom ones we make up. This is one of the most powerful aspects of custom elements as it enables the creation of a user-friendly API.</p>

### Custom Element Attributes

<p>There are a great many HTML attributes. So that the browser doesn’t waste time calling our <code>attributeChangedCallback</code> when <em>any</em> attribute is changed, we need to provide a list of the attribute changes we want to listen for. For this example, we’re only interested in one.</p>

<pre><code class="language-javascript">static get observedAttributes() {
            return ['expanded']
        }
</code></pre>

<p>So now our <code>attributeChangedCallback</code> will only be called when we change the value of the expanded attribute on the custom element, as it’s the only attribute we’ve listed.</p>

<p>HTML attributes can have corresponding values (think <em>href, src, alt, value</em> etc) while others are either true or false (e.g. <em>disabled, selected, required</em>). For an attribute with a corresponding value, we would include the following within the custom element’s class definition.</p>

<pre><code class="language-javascript">get yourCustomAttributeName() {
  return this.getAttribute('yourCustomAttributeName');
}
set yourCustomAttributeName(newValue) {
  this.setAttribute('yourCustomAttributeName', newValue);
}
</code></pre>

<p>For our example element, the attribute will either be true or false, so defining the getter and setter is a little different.</p>

<pre><code class="language-javascript">get expanded() {
  return this.hasAttribute('expanded')
}

// the second argument for setAttribute is mandatory, so we’ll use an empty string
set expanded(val) {
  if (val) {
    this.setAttribute('expanded', '');
  }
  else {
    this.removeAttribute('expanded')
  }
}
</code></pre>

<p>Now that the boilerplate has been dealt with, we can make use of <code>attributeChangedCallback</code>.</p>

<pre><code class="language-javascript">attributeChangedCallback(name, oldval, newval) {
  console.log(`the ${name} attribute has changed from ${oldval} to ${newval}!!`);
  // do something every time the attribute changes
}
</code></pre>

<p>Traditionally, configuring a Javascript component would have involved passing arguments to an <code>init</code> function. By utilising the <code>attributeChangedCallback</code>, its possible to make a custom element that’s configurable just with markup.</p>

<p>Shadow DOM and custom elements can be used separately, and you may find custom elements useful all by themselves. Unlike shadow DOM, they <em>can</em> be polyfilled. However, the two specs work well in conjunction.</p>

{{% ad-panel-leaderboard %}}

### Attaching Markup And Styles With Shadow DOM

<p>So far, we’ve handled the <em>behavior</em> of a custom element. In regard to markup and styles, however, our custom element is equivalent to an empty unstyled <code>&lt;span></code>. To encapsulate HTML and CSS as part of the component, we need to attach a shadow DOM. It’s best to do this within the constructor function.</p>

<div class="break-out">

<pre><code class="language-javascript">class FancyComponent extends HTMLElement {
        constructor() {
            super()
            var shadowRoot = this.attachShadow({mode: 'open'})
            shadowRoot.innerHTML = `&lt;h2>hello world!&lt;/h2>`
            }
</code></pre></div>

<p>Don’t worry about understanding what the mode means &mdash; its boilerplate you have to include, but you’ll pretty much <em>always</em> want <code>open</code>. This simple example component will just render the text “hello world”. Like most other HTML elements, a custom element can have children &mdash; but not by default. So far the above custom element we’ve defined won’t render any children to the screen. To display any content between the tags, we need to make use of a <code>slot</code> element.</p>

<pre><code class="language-html">shadowRoot.innerHTML = `
&lt;h2&gt;hello world!&lt;/h2&gt;
&lt;slot&gt;&lt;/slot&gt;
`
</code></pre>

<p>We can use a style tag to apply some CSS to the component.</p>

<pre><code class="language-css">shadowRoot.innerHTML = 
`&lt;style&gt;
p {
color: red;
}
&lt;/style&gt;
&lt;h2&gt;hello world!&lt;/h2&gt;
&lt;slot&gt;some default content&lt;/slot&gt;`
</code></pre>

<p>These styles will only apply to the component, so we are free to make use of element selectors without the styles affecting anything else of the page. This simplifies writing CSS, making naming conventions like BEM unnecessary.</p>

### Publishing A Component On NPM

<p>NPM packages are published via the command line. Open a terminal window and move into a directory that you would like to turn into a reusable package. Then type the following commands into the terminal:</p>

<ol>
<li>If your project doesn’t already have a <a href="https://docs.npmjs.com/files/package.json">package.json</a>, <code>npm init</code> will walk you through generating one.</li>
<li><code>npm adduser</code> links your machine to your NPM account. If you don’t have a preexisting account, it will create a new one for you.</li>
<li><code>npm publish</code></li>
</ol>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b594f06b-c102-49bd-9463-3caf5d742be7/terminal.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b594f06b-c102-49bd-9463-3caf5d742be7/terminal.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b594f06b-c102-49bd-9463-3caf5d742be7/terminal.png'>Large preview</a>" alt="NPM packages are published via the command line" >}}

<p>If all’s gone well, you now have a component in the NPM registry, ready to be installed and used in your own projects &mdash; and shared with the world.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9b48c4-72c9-49ae-829e-28e3611f322a/npm.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9b48c4-72c9-49ae-829e-28e3611f322a/npm.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9b48c4-72c9-49ae-829e-28e3611f322a/npm.png'>Large preview</a>" alt="An example of a component in the NPM registry, ready to be installed and used in your own projects." >}}

<p>The web components API isn’t perfect. Custom elements are currently unable to <a href="https://github.com/w3c/webcomponents/issues/187">include data in form submissions</a>. The progressive enhancement story isn’t great. Dealing with <a href="https://github.com/WICG/aom/blob/gh-pages/explainer.md#use-case-1-setting-non-reflected-default-accessibility-properties-for-web-components">accessibility isn’t as easy as it should be</a>.</p>

<p>Although originally announced in 2011, browser support still isn’t universal. Firefox support is due later this year. Nevertheless, some high-profile websites (like Youtube) are already making use of them. Despite their current shortcomings, for <em>universally</em> shareable components they’re the singular option and in the future we can expect <a href="https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Template-Instantiation.md">exciting additions</a> to what they have to offer.</p>

{{< signature "il, ra, yk" >}}
