---
title: A Responsive Material Design App With Polymer Starter Kit
slug: responsive-material-design-app-with-polymer-starter-kit
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8afaa9f-6153-44e6-9b3a-2fe2da4bb971/02-maps-screenshot-opt-small.png
date: 2015-10-14T02:00:33.000Z
author: sebastianmetzger
description: >-
  One upcoming technology that represents a big leap forward in making the web a
  mature application platform is [web
  components](https://www.smashingmagazine.com/2014/03/04/introduction-to-custom-elements/).
  From a high-level perspective, **web components will enable better
  composability**, reusability and interoperability of front-end web application
  elements by providing a common way to write components in HTML.

  The goal of this article is to show you why this will be such an important
  step, by showing off **what can be accomplished right now using Polymer**.
  Polymer is currently the most advanced and (self-proclaimed) production-ready
  library based on web components.
categories:
  - Coding
  - Workflow
  - Techniques
  - Web Components
---
One upcoming technology that represents a big leap forward in making the web a mature application platform is <a href="https://www.smashingmagazine.com/2014/03/04/introduction-to-custom-elements/">web components</a>. From a high-level perspective, web components will enable <strong>better composability</strong>, reusability and interoperability of front-end web application elements by providing a common way to write components in HTML.

The goal of this article is to show you why this will be such an important step, by showing off what can be accomplished right now using <a href="https://www.polymer-project.org/1.0/">Polymer</a>. Polymer is currently the most advanced and (self-proclaimed) production-ready library based on web components.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2015/07/material-design-icons-templates-tools/#further-reading-on-smashingmag)

*   [Material Design Icons, Goodies And Starter Kits](https://www.smashingmagazine.com/2015/07/material-design-icons-templates-tools/)
*   [Sketch With Material Design](https://www.smashingmagazine.com/2015/05/sketch-with-material-design/)
*   [Styling Web Components Using A Shared Style Sheet](https://www.smashingmagazine.com/2016/12/styling-web-components-using-a-shared-style-sheet/)
*   [<span class="headline">How To Design Better Buttons</span>](https://www.smashingmagazine.com/2016/11/a-quick-guide-for-designing-better-buttons/)

## What Is Polymer?

Let’s get this out of the way: “Polymer is not a framework.” The team behind it strongly emphasized this at this year’s Google I/O talk about the 1.0 release. Polymer was announced at Google I/O 2013. Its purpose is to enable developers to work with web components and the four underlying low-level APIs — <a href="https://webcomponents.org/articles/introduction-to-html-imports/">HTML imports</a>, <a href="https://webcomponents.org/polyfills/shadow-dom/">shadow DOM</a>, HTML templates and <a href="https://webcomponents.org/articles/introduction-to-custom-elements/">custom elements</a> — before the standards are finalized and implemented by all browser vendors.

{{% feature-panel %}}

This is accomplished by providing a <strong>set of polyfills</strong> that, well, "fake" the new API behavior where it is not yet implemented for the last two versions of all major browsers. Beyond these polyfills, Polymer also provides some syntactic sugar that makes working with web components a bit easier.

One year later, the project got a big boost at Google I/O 2014, as the team announced its ambitions to drive Polymer forward by providing an extensive library of prebuilt elements for developers, based on the <a href="https://www.smashingmagazine.com/2015/07/material-design-icons-templates-tools/">material design</a> <a href="https://google.com/design/">guidelines</a>. Now, one year later, the “production-ready” 1.0 version of Polymer was <a href="https://www.youtube.com/watch?v=fD2As5RmM8Q">officially announced in the I/O 2015 keynote.</a>

So, let’s take a closer look at what all the fuss is about and what working with web components and Polymer feels like.</p>

## The Polymer Components

With version 1.0, the Polymer team announced different sets of <a href="https://elements.polymer-project.org/">element product lines</a>. These reusable building blocks are prebuilt for developers and show how web components will enable an ecosystem of modular building blocks.

*   [Iron elements](https://elements.polymer-project.org/browse?package=iron-elements) These are utility elements that handle basic layouting and core functionality, without applying any complex visual styles.
*   [Paper elements](https://elements.polymer-project.org/browse?package=paper-elements) These are a web component implementation of material design based on the iron element.
*   [Google web components](https://elements.polymer-project.org/browse?package=google-web-components) These web components are wrappers for Google APIs and services. For example, there is an element for Google Maps, YouTube and Google Calendar.
*   [Gold elements](https://elements.polymer-project.org/browse?package=gold-elements) These are special elements that can be used for e-commerce, such as credit-card input elements.
*   [Neon elements](https://elements.polymer-project.org/browse?package=neon-elements) All fancy special effects fall under this label. Currently, only a [web animations](https://w3c.github.io/web-animations/) element is in there, which has [some pretty cool demos](https://github.com/PolymerElements/neon-animation#demos).
*   [Platinum elements](https://elements.polymer-project.org/browse?package=platinum-elements) This category is for components that enable complex web app functionality, such as push notifications.
*   [Molecules](https://elements.polymer-project.org/browse?package=molecules) These elements are wrappers for other JavaScript libraries.

Beyond this official Polymer repository, you should check out <a href="https://customelements.io/">Custom Elements</a>, a repository of even more elements. These elements are not necessarily based on Polymer but are still compatible thanks to the web component magic.</p>

## Example Application

### Create Boilerplate Using Starter Kit

Enough with the high-level talk and overviews. How do we start developing with Polymer? Thankfully, the guys at <a href="https://developers.google.com/web/tools/polymer-starter-kit/">Google have released</a> a neat <a href="https://github.com/polymerelements/polymer-starter-kit">starter kit</a> with version 1.0.

If you have Node.js, npm, Bower and Gulp installed, you can run the following command in the project directory to install all dependencies:

<pre><code class="language-bash">npm install -g gulp bower &amp;&amp; npm install &amp;&amp; bower install</code></pre>

For additional information on modern JavaScript tooling, check out the respective pages on <a href="https://www.npmjs.com/">npm</a>, <a href="https://bower.io/">Bower</a> and <a href="https://gulpjs.com/">Gulp</a>.

After installing the dependencies, you can run the kit with Gulp:

<pre><code class="language-bash">gulp serve</code></pre>

This command will build and serve the starter kit.</p>

### A Look at the Starter Kit

What we have here with the starter kit is a very basic application skeleton, with responsive layout, material design, routing functionality and offline caching via the service worker API.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6132821e-9cfc-4d65-af29-8045807479f3/01-starter-kit-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ea8057f-7a67-4c98-b015-d341db98251c/01-starter-kit-opt-small.png" alt="Polymer starter kit" /></a><figcaption>Polymer starter kit. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6132821e-9cfc-4d65-af29-8045807479f3/01-starter-kit-opt.png">View large version</a>)</figcaption></figure>

Let’s take a closer look at what an application like this looks like under the hood in web component land. Look at the <code>app/index.html</code> file. In the head you can see that the script is included in the page:

<pre><code class="language-markup">&lt;script src="bower_components/webcomponentsjs/webcomponents-lite.js"&gt;&lt;/script&gt;</code></pre>

This is the web component polyfill part of Polymer, which will become obsolete over time; <a href="https://caniuse.com/#search=web%20components">Can I Use lists its current state</a>. At the time of writing, web components are supported natively 100% in Chrome and Opera and are currently behind a flag in Firefox.

A bit further down the line, you will find this part:

<pre><code class="language-markup">&lt;link rel="import" href="elements/elements.html"&gt;</code></pre>

This is HTML imports in action. When you go further and open the <code>elements/elements.html</code> file, you will see that all of the elements used in the body of <code>index.html</code> are imported here. You could also directly import them into <code>index.html</code>, but the source file is a bit cleaner if you put them into their own <code>.html</code> file.

Now, let’s have a look at the actual markup of the application.</p>

### Structure an App With Web Components

Most importantly when looking at <code>index.html</code>, you will see a lot of custom elements, which are used to mark up the app. Here, you will see mostly elements from the <a href="https://elements.polymer-project.org"><code>iron-*</code> and <code>paper-*</code> element libraries</a>. Custom elements need to be prefixed with this <code>-</code> notation to avoid collision with potential future base HTML elements.

You can see that the complete layout of the page is made up of paper and iron elements from the Polymer library:

<pre><code class="language-markup">&lt;paper-drawer-panel&gt;
   &lt;!--Responsive sidebar drawer --&gt;
   &lt;paper-header-panel&gt;
      &lt;!-- Header of the drawer --&gt;
      &lt;paper-toolbar&gt;
      &lt;/paper-toolbar&gt;
      &lt;!--Menu in the drawer --&gt;
      &lt;paper-menu&gt;
      &lt;/paper-menu&gt;
   &lt;/paper-header-panel&gt;
   &lt;!--Main content area --&gt;
      &lt;paper-header-panel&gt;
         &lt;!--Header of the main content --&gt;
         &lt;paper-toolbar&gt;
         &lt;/paper-toolbar&gt;
         &lt;!--Main content --&gt;
      &lt;iron-pages&gt;
      &lt;/iron-pages&gt;
   &lt;/paper-header-panel&gt;
&lt;/paper-drawer-panel&gt;
</code></pre>

This shows the very declarative and semantic way of structuring an app with web components. Imagine looking at the markup of such an application in a traditional web application; it would have hundreds of divs all over the place.</p>

### Web Components as APIs

Additionally, you have an example of the <code>platinum-*</code> elements that provide more complex functionality, such as facilitating the new service worker API. Service workers are another new standard API that enables you to create a background service in the browser that can handle caching, an offline experience for your web app and much more. It is not directly related to web components, so <a href="https://www.html5rocks.com/en/tutorials/service-worker/introduction/">check out HTML5 Rocks’ article</a> if you want to learn more about it. Similarly, the <code>paper-toast</code> element adds a notification toast functionality to the application. This shows the way web components can be used to capture more complex functionality and APIs.

Overall, the markup of the application shows the very declarative way of marking up an application by combining reusable elements. Notice that there is not a lot of additional JavaScript or CSS throughout the starter kit app. Most of the complex code is nicely encapsulated in the elements that were pulled in as dependencies.</p>

### Data Binding and Routing

You probably noticed that the application is wrapped in an HTML template tag:

<pre><code class="language-markup">&lt;template is="dom-bind" id="app"&gt;
   …
&lt;/template&gt;
</code></pre>

This is done because Polymer uses HTML templates as context (as AngularJS does with the <code>$scope</code>, for example) for <a href="https://www.polymer-project.org/1.0/docs/devguide/data-binding.html">data binding.</a> The <code>is="dom-bind"</code> shows the <code>is</code> attribute, which is a way to declare that some element is a custom element of the type provided as a value, while still inheriting from the tag it is placed on. So, this template tag gets treated as a <code>dom-bind</code> element, which is a custom element provided by Polymer that now inherits from the <code>template</code> element it was placed on. The <code>dom-bind</code> element here turns on Polymer’s binding capabilities in the <code>template</code> tag it was placed on.</p>

<a href="https://www.polymer-project.org/1.0/docs/devguide/data-binding.html">AngularJS developers will probably spot this</a> on first sight: The app is held together via data binding with the Mustache syntax. The connection between the <code>paper-menu</code> element and the <code>iron-pages</code> element is a great example of what can be done with this in a web component world.

The <code>paper-menu</code> element, which contains several anchor elements, is responsible for the state of the menu. The selected attribute is bound to the <code>{{route}}</code> variable.</p>

<pre><code class="language-markup">&lt;paper-menu class="list" attr-for-selected="data-route" selected="{{route}}" on-iron-select="onMenuSelect"&gt;
   …
&lt;/paper-menu&gt;
</code></pre>

The <code>iron-pages</code> element is responsible for filling the main content area with one of its child elements, depending on the state of the selected attribute. Here you can see that the <code>{{route}}</code> variable is being used to connect it with the menu state.</p>

<pre><code class="language-markup">&lt;iron-pages attr-for-selected="data-route" selected="{{route}}"&gt;
   …
&lt;/iron-pages&gt;
</code></pre>

This data-binding functionality is part of Polymer’s syntactic sugar and is not part of the basic web components standard.

Additionally, to bind the route correctly to a URL, a lightweight router is inside the <code>elements/routing.html</code> file.</p>

<pre><code class="language-markup">page('/', function () {
   app.route = 'home';
});

page('/users', function () {
   app.route = 'users';
});

page('/users/:name', function (data) {
   app.route = 'user-info';
   app.params = data.params;
});

page('/contact', function () {
   app.route = 'contact';
});

// add #! before urls
page({
   hashbang: true
});
</code></pre>

Here you can see how the route variable is accessed programmatically via <code>app.route</code>. Notice that the <code>template</code> element, used for data binding, has an ID of <code>app</code>. Inside the routing JavaScript code, the data inside the custom element is now available via its ID attribute value; that is why it can be accessed via <code>app.*</code>.</p>

### Creating Your Own Custom Elements

If you are interested in <a href="https://www.polymer-project.org/1.0/docs/devguide/data-binding.html">creating your own custom elements</a> with Polymer, you will find the <code>app/elements/my-greeting</code> and <code>app/elements/my-list</code> elements that are defined and used in the starter kit application.

We won’t go in depth into how to create your own reusable elements, though, because that would probably require a whole article of its own.</p>

### Adding an Existing Custom Element

Let’s go beyond the boilerplate project and add another custom element. How about a Google Map?

Thankfully, there is <a href="https://elements.polymer-project.org/elements/google-map">already an element for that</a> in Google’s product line. Adding it to your project is just one <code>bower install</code> away:

<pre><code class="language-bash">bower install --save GoogleWebComponents/google-map#^1.0.0</code></pre>

Now, you can include it with the imported elements in the <code>app/elements/elements.html</code> file:

<pre><code class="language-markup">&lt;link rel="import" href="../bower_components/google-map/google-map.html"&gt;
</code></pre>

Now that the element is imported, include it in your application — for example, on the “Contact“ screen:

<pre><code class="language-markup">(…)
&lt;section data-route="contact"&gt;
   &lt;paper-material elevation="1"&gt;
      &lt;h2 class="paper-font-display2"&gt;Contact&lt;/h2&gt;
      &lt;p&gt;This is the contact section&lt;/p&gt;
   &lt;/paper-material&gt;
   &lt;paper-material elevation="1"&gt;
      &lt;google-map latitude="37.77493" longitude="-122.41942"&gt;&lt;/google-map&gt;
   &lt;/paper-material&gt;
&lt;/section&gt;
(…)
</code></pre>

Some additional CSS is still needed in the <code>app/styles/main.css</code> file to set the display height of the map.</p>

<pre><code class="language-css">(…)
google-map {
   height: 600px;
}
(…)
</code></pre>

Voila! You’ve just added a Google Map to your application, without tinkering with any iframe or initializing a JavaScript library.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b85b79a3-4727-47fd-8311-c096c2928d1f/02-maps-screenshot-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8afaa9f-6153-44e6-9b3a-2fe2da4bb971/02-maps-screenshot-opt-small.png" alt="Adding a Google Map without tinkering with any iframe or initializing a JavaScript library" /></a><figcaption>Adding a Google Map without tinkering with any iframe or initializing a JavaScript library. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b85b79a3-4727-47fd-8311-c096c2928d1f/02-maps-screenshot-opt.png">View large version</a>)</figcaption></figure>

This neatly showcases how developers can take advantage of web components to reuse elements without having to create the same boilerplate or reinvent the wheel. The <a href="https://developers.google.com/maps/tutorials/fundamentals/adding-a-google-map">standard method of adding a Google Map</a> to an app without web components is cumbersome by contrast.</p>

### Adding a Non-Polymer Custom Element

Another thing we might want on the web page is an animated GIF. Go to <a href="https://customelements.io">Custom Elements</a> and find the <a href="https://github.com/geelen/x-gif/">x-gif element</a>, which promises smooth GIF playback. Unfortunately, it is not based on Polymer. But no problem! It can be added like any other web component.

Again, let’s do a quick <code>bower install</code> to fetch the x-gif component:

<pre><code class="language-bash">bower install --save x-gif</code></pre>

Add it to your <code>app/elements/elements.html</code> imports list:

<pre><code class="language-markup">&lt;link rel="import" href="../bower_components/google-map/google-map.html"&gt;
&lt;link rel="import" href="../bower_components/x-gif/dist/x-gif.html"&gt;
</code></pre>

Put your favorite GIF in <code>app/images/epic.gif</code>, and add it to the home screen using the <code>x-gif</code> tag:

<pre><code class="language-markup">&lt;section data-route="home"&gt;
   &lt;paper-material elevation="1"&gt;
      &lt;my-greeting&gt;&lt;/my-greeting&gt;

      &lt;p class="paper-font-subhead"&gt;You now have:&lt;/p&gt;
      &lt;my-list&gt;&lt;/my-list&gt;

      &lt;x-gif src="images/epic.gif"&gt;&lt;/x-gif&gt;

      &lt;p class="paper-font-body2"&gt;Looking for more web app layouts? Check out our &lt;a href="https://github.com/PolymerElements/app-layout-templates"&gt;layouts&lt;/a&gt; collection. You can also &lt;a href="https://polymerelements.github.io/app-layout-templates/"&gt;preview&lt;/a&gt; them live.&lt;/p&gt;
   &lt;/paper-material&gt;
&lt;/section&gt;
</code></pre>

Mind-blowing:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1381dde-98be-42b2-bc32-9dc1fb28c1a8/03-mindblowing-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9838d681-dc55-4e21-b8f3-5afca5b800d1/03-mindblowing-opt-small.png" alt="Using the x-gif web component" /></a><figcaption>Using the the x-gif web component. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1381dde-98be-42b2-bc32-9dc1fb28c1a8/03-mindblowing-opt.png">View large version</a>)</figcaption></figure>

Just remember that the x-gif web component has nothing to do with the Polymer library; it is built using the vanilla web components APIs. This really shows the interoperability of web component-based elements. Now, think about how popular frameworks like <a href="https://angular.io/">AngularJS 2.0</a> and <a href="https://www.gwtproject.org/">Google Web Toolkit 3.0</a> will be based on web components in future versions and how much more interoperable frameworks will be in future. By the way, Mozilla is also working on a web component-based library, <a href="https://brick.mozilla.io/">Bricks</a>, which is pretty far along in development.</p>

## Conclusion

We’ve seen now what working with web components in Polymer 1.0 looks like, using the starter kit as a foundation. And we’ve seen the declarative and boilerplate-free way to combine reusable elements, elements that interoperate without necessarily having been developed with the same libraries or frameworks.

I am really excited about web components because they mark a huge step in the advancement of the web and its transformation into a fully capable application distribution platform, without the quirky hacks and framework silos of the past.</p>

### Resources

*   [Polymer Starter Kit](https://developers.google.com/web/tools/polymer-starter-kit)
*   [Application Layout Templates](https://polymerelements.github.io/app-layout-templates), Polymer
*   [Application Layout Templates](https://github.com/PolymerElements/app-layout-templates), GitHub

#### Elements

*   [Polymer Element Catalog](https://elements.polymer-project.org)
*   [Custom Elements](https://customelements.io/)

#### Videos

*   “[Polymer and Modern Web APIs: In Production at Google Scale](https://www.youtube.com/watch?v=fD2As5RmM8Q),” Google I/O 2015

{{< signature "al, ml, rb, jb" >}}

