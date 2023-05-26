---
title: Reimagining Single-Page Applications With Progressive Enhancement
slug: reimagining-single-page-applications-progressive-enhancement
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/996cc519-7c54-45b2-a6de-3b12dffb6472/hashtag-opt.png'
date: 2015-12-21T20:27:15.000Z
author: heydon-pickering
description: >-
  What is the difference between a web page and a web application? Though we tend to identify documents with reading and applications with interaction, most web-based applications are of the blended variety: Users can consume information and perform tasks in the same place. Regardless, the way we approach _building_ web applications usually dispenses with some of the simple virtues of the readable web.
categories:
  - Coding
  - CSS
  - JavaScript
  - Performance
---
What is the difference between a web page and a web application? Though we tend to identify documents with reading and applications with interaction, most **web-based applications are of the blended variety**: Users can consume information and perform tasks in the same place. Regardless, the way we approach _building_ web applications usually dispenses with some of the simple virtues of the readable web.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Perceived Performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
*   [Perception Management](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/)
*   [Preload: What is it good for?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

Single-page applications tend to take the form of runtimes, JavaScript executables deployed like popup shops into vacant `<body>` elements. They’re temporary, makeshift and [not cURL-able](https://indiewebcamp.com/curlable): Their content is not really _there_ without a script being executed. They’re also brittle and underperforming because, in service of architectural uniformity and convenience, they make all of their navigation, data handling and even the **basic display of content** the responsibility of one thing: client-side JavaScript.

Recently, there’s been a move towards “isomorphic” (or “[universal](https://medium.com/@mjackson/universal-javascript-4761051b7ae9)”) applications — applications that can run the same code on the client and the server, sending prerendered HTML from the server before delegating to client-side code. This approach (possible [using Express as the server and React as the rendering engine](/2015/04/react-to-the-future-with-isomorphic-apps/), for instance) is a huge step towards a more performant and robust web application architecture.

{{% feature-panel %}}

But **isomorphism is surely not the only way to go about progressive enhancement** for single-page applications. I’m looking into something more flexible and with less configuration, a new philosophy that capitalizes on standard browser behavior and that can blend indexable, static prose with JavaScript-embellished interactivity, rather than just “handing off” to JavaScript.

This little exposition amounts to no more than the notion of doing things The Web Way™ with a few loosely confederated concepts and techniques, but I think you could take it and make it something special.</p>

## Writing Views

In your typical single-page app, **rendering views** (i.e. individual screens) and routing between them is made the concern of JavaScript. That is, locations are defined, evaluated and brought into existence entirely by what was, until recent years, a technology considered supplementary to this kind of behavior. Call me a [Luddite](https://www.oxforddictionaries.com/definition/english/luddite), but I’m not going to use JavaScript for this at all. Heretically, I’m going to let HTML and the browser take care of it instead.

I’ll start by creating an HTML page and making the `<main>` part of that page my views container:

<pre><code class="language-markup">&lt;main role=&quot;main&quot;&gt;
    /* Views go here. */
&lt;/main&gt;</code></pre>

Then, I’ll begin constructing individual views, placing each as a child element of `<main>`. Each view must bear an `id`. This will be used as part of our “routing solution.” It should also have a first-level heading: Views will be displayed one at a time, as the only perceivable content of the page, so this is preferable for screen-reader accessibility.

<pre><code class="language-markup">&lt;div id=&quot;some-view&quot;&gt;
    &lt;h1&gt;Some view&lt;/h1&gt;
    &lt;!-- the static view content, enhanceable with JavaScript --&gt;
&lt;/div&gt;</code></pre>

For brevity and to underline the importance of working directly in HTML, I’m hand-coding my views. You may prefer to compile your views from data using, say, [Handlebars](https://handlebarsjs.com/) and a Node.js script, in which case each view within your `{{#each}}` block might look like the following. Notice that I’m using a Handlebars helper to dynamically create the `id` by [slugifying](https://gist.github.com/Heydon/12fd8b4947b2a05fe5f3) the view’s `title` property.

<pre><code class="language-markup">&lt;div id=&quot;{{slugify title}}&quot;&gt;
    &lt;h1&gt;{{title}}&lt;/h1&gt;
    {{{content}}}
&lt;/div&gt;</code></pre>

Maybe using PHP to generate the content from a MySQL database is more your thing? It’s really not important _how_ you compile your views so long as content is served precompiled to the client. Some content and functionality **should be available in the absence of client-side scripting**. Then, we can progressively enhance it, only in cases where we actually _want_ to progressively enhance it. As I shall explain, my method will preserve static content within the app as just that: static content.</p>

## Navigation

Not being interested in breaking with convention, I think my single-page app would benefit from a navigation block, allowing users to traverse between the views. Above the `<main>` view area, I might provide something like this:

<pre><code class="language-markup">&lt;nav role=&quot;navigation&quot;&gt;
    &lt;ul&gt;
        &lt;li&gt;&lt;a href=&quot;#the-default-view&quot;&gt;the default view&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=&quot;#some-view&quot;&gt;some view&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=&quot;#another-view&quot;&gt;another view&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/nav&gt;</code></pre>

My views are document fragments, identified by their `id`s, and can be [navigated to using links](https://www.w3.org/TR/html5/browsers.html#scroll-to-fragid) bearing this identifier, or “hash.” So, when users click on the first link, pointing at `#the-default-view`, they’ll be transported to that view. If it is not currently visible in the viewport, the browser will scroll it into visibility. Simultaneously, the URL will update to reflect the new location. To determine where you are in the application, you need only query the URL:

<pre><code class="language-markup">https://my-app-thing.com#the-default-view</code></pre>

As you might imagine, leveraging standard browser behavior to traverse static content is _really_ rather performant. It can be expected to work unencumbered by JavaScript and will even succeed where JavaScript errs. Although my “app” is more akin to a Wikipedia page than the kind of thing you’re familiar seeing built with AngularJS, the navigation part of my routing is now complete.

**Note:** Because conforming browsers [send focus to page fragments](https://html.spec.whatwg.org/multipage/interaction.html#sequential-focus-navigation-starting-point), keyboard accessibility is already taken care of here. I can enhance keyboard accessibility when JavaScript is, eventually, employed. More on that later.</p>

## One View At A Time

Being an accessibility consultant, a lot of my work revolves around reconciling state and behavior with the _appearance_ of these things. At this point, the behavior of changing routes within our app is already supported, but the app does not look or feel like a single-page application because each view is ever present, rather than mutually exclusive. We should only ever show the view to which the user has navigated.

Is this the turning point at which I begin to progressively enhance with JavaScript? No, not yet. In this case, I’ll be harnessing CSS’ `:target` pseudo-class. Progressive enhancement does not just mean “adding JavaScript”: Our web page should work OK without JavaScript _or_ CSS.

<pre><code class="language-css">main &gt; * {
    display: none;
}

main &gt; *:target {
    display: block;
}</code></pre>

The `:target` pseudo-class relates to the element matching the fragment identifier in the URL. In other words, if the URL is `https://my-app-thing.com#some-view`, then only the element with the `id` of `some-view` will have `display: block` applied. To “load” that view (and hide the other views), all one has to do is click a link with the corresponding `href`. Believe it or not, I’m using links as links, not hijacking them and suppressing their default functionality, as most single-page apps (including client-rendered isomorphic apps) would do.

<pre><code class="language-markup">&lt;a href=&quot;#some-view&quot;&gt;some view&lt;/a&gt;</code></pre>

This now feels more like a single-page application (which, in turn, is designed to feel like you’re navigating between separate web pages). Should I so desire, I could take this a step further by adding some animation.

<pre><code class="language-css">main &gt; * {
    display: none;
}

@keyframes pulse {
    0% { transform: scale(1) }
    50% { transform: scale(1.05) }
    100% { transform: scale(1) }
}

main &gt; *:target {
    display: block;
    animation: pulse 0.5s linear 1;
}</code></pre>

Fancy! And, admittedly, somewhat pointless, but there is something to be said for a visual indication that the context has changed — especially when switching views is instantaneous. I’ve [set up a Codepen](https://codepen.io/heydon/debug/JGoaVw) for you to see the effect. Note that the browser’s “back” button works as expected, because no JavaScript has hijacked or otherwise run roughshod over it. Pleasingly, the animation triggers either via an in-page link or with the “back” and “forward” buttons.

Everything works great so far, except that no view is displayed upon `https://my-app-thing.com` being hit for the first time. We can fix this! No, not with JavaScript, but with a CSS enhancement again. If we used JavaScript here, it would make our whole routing system dependent on it and all would be lost.

## The Default View

Because I can’t rely on users navigating to `https://my-app-thing.com#the-default-view` according to my saying so, and because `:target` needs the fragment identifier `#the-default-view` to work, I’ll need to try something else to display that default view.

As it turns out, this is achievable by controlling the source order and being a [bit of a monster with CSS selectors](https://alistapart.com/article/quantity-queries-for-css). First, I’ll make my default view the last of the sibling view elements in the markup. This is perfectly acceptable accessibility-wise because views are “loaded” one at a time, with the others hidden from assistive technology using `display: none`. Order is not pertinent.

<pre><code class="language-markup">&lt;main role=&quot;main&quot;&gt;
    &lt;div id=&quot;some-view&quot;&gt;
        &lt;h1&gt;some view&lt;/h1&gt;
        &lt;!-- … --&gt;
    &lt;/div&gt;
    &lt;div id=&quot;another-view&quot;&gt;
        &lt;h1&gt;another view&lt;/h1&gt;
        &lt;!-- … --&gt;
    &lt;/div&gt;
    &lt;div id=&quot;the-default-view&quot;&gt;
        &lt;h1&gt;the default view&lt;/h1&gt;
        &lt;!-- … --&gt;
    &lt;/div&gt;
&lt;/main&gt;</code></pre>

Putting the default view last feels right to me. It’s like a fallback. Now, we can adapt the CSS:

<pre><code class="language-css">main &gt; * {
    display: none;
}

main &gt; *:last-child {
    display: block;
}

@keyframes pulse {
    0% { transform: scale(1) }
    50% { transform: scale(1.05) }
    100% { transform: scale(1) }
}

main &gt; *:target {
    display: block;
    animation: pulse 0.5s linear 1;
}

main &gt; *:target ~ * {
    display: none;
}</code></pre>

There are two new declaration blocks: the second and final. The second overrules the first to show our default `> *:last-child` view. This will now be visible when the user hits `https://my-app-thing.com`. The final block, using the general sibling combinator, applies `display: none` to any element _following_ the `:target` element. Because our default view comes last, this rule will always apply to it, but _only_ if a `:target` element exists. (Because CSS doesn’t work backwards, a `:first-child` default element would not be targetable from a sibling `:target` element that appears after it.)

Try reloading [the Codepen](https://codepen.io/heydon/debug/JGoaVw) with just the root URL (no hash in the address bar) to see this in practice.</p>

### It’s Time

We’ve come a long way without using JavaScript. The trick now is to **add JavaScript behavior judiciously**, enhancing what’s been achieved so far without replacing it. We should be able to react to view changes with JavaScript without causing those view changes to fall in the realm of JavaScript. Anything short of this would be overengineering, thereby diminishing performance and reliability.

I’m going to use a modicum of plain, well-supported JavaScript, not jQuery or any other helper library: The skeleton of the app should remain small but extensible.</p>

## The `hashchange` Event

As stated, popular web application frameworks tend to render views with JavaScript. They then allow callback hooks, like Meteor’s `Template.my-template.rendered`, for augmenting the view at the point it’s made available. Even isomorphic apps like to use script-driven routing and rendering if they get the chance. My little app does not render views so much as _reveal_ them. However, it’s entirely likely that, in some cases, I’ll want to act upon a newly revealed view with JavaScript, upon its arrival.

Fortuitously, the Web API affords us the [extremely well-supported](https://caniuse.com/#feat=hashchange) (from Internet Explorer 8 and up) `hashchange` event type, which fires when the URL’s fragment identifier changes. This has a similar effect but, crucially, does not rely on JavaScript rendering the view (from which it would emit a custom event) to provide us with a hook.

In the following script ([demoed in another Codepen](https://codepen.io/heydon/pen/BjNXba)), I use the `hashchange` event to log the identity of the current view, which doubles as the `id` of that view’s parent element. As you might imagine, it works no matter how you change that URL, including by using the “back” button.

<pre><code class="language-javascript">window.addEventListener(&#39;hashchange&#39;, function() {
    console.log(&#39;this view\&#39;s id is &#39;, location.hash.substr(1));
});</code></pre>

We can scope DOM operations to our view by setting a variable inside this event handler, such as `viewElem`, to signify the view’s root element. Then, we can target view-specific elements with expressions such as `viewElem.getElementsByClassName('button')[0]` and so on.

<pre><code class="language-javascript">window.addEventListener(&#39;hashchange&#39;, function() {
    var viewID = location.hash.slice(1);
    var viewElem = document.getElementById(viewID);
    viewElem.innerHTML = &#39;&lt;p&gt;View loaded!&lt;/p&gt;&#39;;
});</code></pre>

## Abstraction

I’m wary of abstraction because it can become its own end, making program logic opaque in the process. But things are going to quickly turn into a mess of ugly `if` statements if I carry on in this vein and begin to support different functionality for individual views. I should also be addressing the issue of **filling the global scope**. So, I’m going to borrow a common [singleton](https://robdodson.me/javascript-design-patterns-singleton/) pattern: defining an object with our functionality inside of a self-executing function that then attaches itself to the `window`. This is where I'll define my routes and application-scope methods.

In the following example, my `app` object contains four properties: `routes` for defining each route by name, `default` for defining the default (first-shown) root, `routeChange` for handling a change of route (a hash change), and `init` to be fired once to start the app (when JavaScript is available) using `app.init()`.

<pre><code class="language-javascript">(function() {
    var app = {
        // routes (i.e. views and their functionality) defined here
        &#39;routes&#39;: {
            &#39;some-view&#39;: {
                &#39;rendered&#39;: function() {
                    console.log(&#39;this view is &quot;some-view&quot;&#39;);
                }
            },
            &#39;another-view&#39;: {
                &#39;rendered&#39;: function() {
                    console.log(&#39;this view is &quot;another-view&quot;&#39;);
                    app.routeElem.innerHTML = &#39;&lt;p&gt;This JavaScript content overrides the static content for this view.&lt;/p&gt;&#39;;
                }
             }
        },
        // The default view is recorded here. A more advanced implementation
        // might query the DOM to define it on the fly.
        &#39;default&#39;: &#39;the-default-view&#39;,
        &#39;routeChange&#39;: function() {
            app.routeID = location.hash.slice(1);
            app.route = app.routes[app.routeID];
            app.routeElem = document.getElementById(app.routeID);
            app.route.rendered();
        },
        // The function to start the app
        &#39;init&#39;: function() {
            window.addEventListener(&#39;hashchange&#39;, function() {
                app.routeChange();
            });
            // If there is no hash in the URL, change the URL to
            // include the default view&#39;s hash.
            if (!window.location.hash) {
                window.location.hash = app.default;
            } else {
                // Execute routeChange() for the first time
                app.routeChange();
            }
        }
    };
    window.app = app;
})();

app.init();</code></pre>

### Notes

*   The context for the current route is set within `app.routeChange`, using the syntax `app.routes[app.routeID]`, where `app.routeID` is equal to `window.location.hash.substr(1)`.
*   Each named route has its own `rendered` function, which is executed within `app.routeChange` with `app.route.rendered()`.
*   The `hashchange` listener is attached to the `window` during `init`.
*   So that any JavaScript that should run on the default view when loading `https://my-app-thing.com` _is_ run, I force that URL with `window.location.hash = app.default`, thereby triggering `hashchange` to execute `app.routeChange()`, including the default route’s `rendered()` function.
*   If the user first hits the app at a specific hashed URL (like `https://my-app-thing.com#a-certain-view`), then this view’s `rendered` function will execute if one is associated with it.
*   If I comment out `app.init()`, my views will still “render,” will still be navigable, styled and animated, and will contain my static content.

One thing you could use the `rendered` function for would be to improve keyboard and screen-reader accessibility by focusing the `<h1>`. When the `<h1>` is focused, it announces in screen readers which view the user is in and puts keyboard focus in a convenient position at the top of that view’s content.

<pre><code class="language-javascript">&#39;rendered&#39;: function() {
        app.routeElem.querySelector(&#39;h1&#39;).setAttribute(&#39;tabindex&#39;, &#39;-1&#39;);
        app.routeElem.querySelector(&#39;h1&#39;).focus();                                          
}</code></pre>

[Another Codepen is available](https://codepen.io/heydon/pen/YwyPZv) using this tiny app “framework.” There are probably neater and even terser(!) ways to write this, but all of the fundamentals are there to explore and rearrange. I’d welcome any suggestions for enhancement, too. Perhaps something could be achieved with `hashchange`’s `oldURL` property, which (for our purposes) references the previous route.

<pre><code class="language-javascript">app.prevRoute = app.routes[e.oldURL.split("#")[1]];</code></pre>

Then, each route, in place of the singular `rendered` function, could have `entered` and `exited` functions. Among other things, both adding and removing event listeners would then be possible.

<pre><code class="language-javascript">app.prevRoute.exited();</code></pre>

## Completely Static Views

The eagle-eyed among you will have noticed that the default view, identified in `app.default` as `the-default-view`, is not, in this case, listed in the `app.routes` object. This means that our app will throw an error when it tries to execute its nonexistent `rendered` function. The view will still appear just fine, but we can remove the error anyway by checking for the existence of the route first:

<pre><code class="language-javascript">if (app.route) {
    app.route.rendered();
}</code></pre>

The implication is that completely static “views” can exist, error-free, side by side with views that are (potentially) highly augmented by JavaScript. This breaks from single-page app normality, wherein you would forfeit the ability to serve static prerendered content by generating _all_ of the content from scratch in the client — well, unless JavaScript fails and you render just a blank page. A _lot_ of examples of that unfortunate behavior can be found on [Sigh, JavaScript](https://sighjavascript.tumblr.com/).

(**Note:** Because I actually _have_ static content to share, I’ll want to add my `app` script after the content at the bottom of the page, so that it doesn’t block its rendering… But you knew that already.)

### Static Views With Enhanced Functionality

You could, of course, mix static and JavaScript-delivered content within the same view, too. As part of the `rendered` function of a particular view, you could insert new DOM nodes and attach new event handlers, for instance. Maybe throw in some AJAX to fetch some fresh data before compiling a template in place of the server-rendered HTML. You could include a form that runs a PHP script on the server when JavaScript is unavailable and that returns the user to the form’s specific view with `header('Location: https://my-app-thing.com#submission-form')`. You could also handle query parameters, using URLs like `https://my-app-thing.com/?foo=bar#some-view`.

It’s entirely flexible, allowing you to combine any build tasks, server technologies, HTML structures and JavaScript libraries you wish. All that this approach does “out of the box” is to keep things on one web page in a responsible, progressive way.

Whatever you want to achieve, you have the option of attaching functions, data and other properties on either the global app scope (`app.custom()`) or on specific views (`app.routes['route-name'].custom()`), just like in a “real” single-page application. Your responsibility, then, is to blend static content and enhanced functionality as seamlessly as possible, and to avoid relegating your static content to being just a perfunctory fallback.</p>

## Conclusion

In this article, I’ve introduced a solution for **architecting progressive single-page applications** using little more than a couple of CSS tricks, less than 0.5 KB of JavaScript and, importantly, some static HTML. It is not a perfect or complete solution, just a modest skeleton, but it testifies to the notion that performant, robust and indexable single-page applications are achievable: You can embrace web standards while reaping the benefits of sharing data and functionality between different interface screens on a single web page. That is all that makes a single-page app a single-page app, really. Everything else is an add-on.

If you have any suggestions for improvements or want to raise any questions or concerns, please leave a comment. I’m not interested in building a “mature” (read: overengineered) framework, but I am interested in solving important problems in the simplest possible ways. Above all, I want us to help each other to make applications that are not just _on_ the web, but _of_ the web, too.

If you’re not sure what I mean by that or you’re wondering why it excites me so much, I recommend reading Aaron Gustafson’s [_Adaptive Web Design_](https://www.peachpit.com/store/adaptive-web-design-crafting-rich-experiences-with-9780134216140). If that’s too much for the moment, do yourself a favour and read the short article, “[Where to Start](https://adactio.com/journal/9963)” by Jeremy Keith.

{{< signature "jb, ml, al" >}}

