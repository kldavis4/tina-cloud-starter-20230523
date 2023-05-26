---
title: 'How BBC Interactive Content Works Across AMP, Apps, And The Web'
slug: bbc-interactive-content-amp-apps-web
author: chrisbashton
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41c046f7-220e-454f-b273-4e3401a0509e/trump-interactive-amp.png
date: 2018-03-15T12:20:27.000Z
summary: >-
  Publishing content to so many media without lots of extra development overhead
  can be difficult. Chris Ashton explains how they've approached the problem in
  BBC's Visual Journalism department.
description: >-
  Publishing content to so many media without lots of extra development overhead
  can be difficult. Chris Ashton explains how they've approached the problem in
  BBC's Visual Journalism department.
categories:
  - Apps
  - AMP
  - Case Studies
  - JavaScript
---
In the Visual Journalism team at the BBC, we produce exciting visual, engaging and interactive content, ranging from [calculators](https://www.bbc.co.uk/news/business-23234033) to [visualizations](https://www.bbc.co.uk/news/resources/idt-5aceb360-8bc3-4741-99f0-2e4f76ca02bb)  new [storytelling formats](https://www.bbc.co.uk/news/science-environment-41207827).

Each application is a unique challenge to produce in its own right, but even more so when you consider that we have to deploy most projects in [many](https://www.bbc.co.uk/sport/olympics/36984887) [different](https://www.bbc.com/persian/sport/2016/08/160809_rio2016_olympics_body_match.shtml) [languages](https://www.bbc.com/russian/features-37021150). Our content has to work not only on the BBC News and Sports websites but on their equivalent apps on iOS and Android, as well as on third-party sites which consume BBC content.

Now consider that **there is an increasing array of new platforms** such as AMP, Facebook Instant Articles, and Apple News. Each platform has its own limitations and proprietary publishing mechanism. Creating interactive content that works across all of these environments is a real challenge. I'm going to describe how we've approached the problem at the BBC.

## Example: Canonical vs. AMP

This is all a bit theoretical until you see it in action, so let's delve straight into an example.

Here is a [BBC article](https://www.bbc.co.uk/news/world-us-canada-39732845) containing Visual Journalism content:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d603e5ba-17d9-4683-b2a1-30f12227a675/trump-interactive-embed.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d603e5ba-17d9-4683-b2a1-30f12227a675/trump-interactive-embed.png" sizes="100vw" caption="Our Visual Journalism content begins with the Donald Trump illustration, and is inside an iframe" alt="Screenshot of BBC News page containing Visual Journalism content" >}}

This is the canonical version of the article, i.e., the default version, which you'll get if you navigate to the article from the homepage.

{{% feature-panel %}}

Now let's look at the [AMP version of the article](https://www.bbc.co.uk/news/amp/world-us-canada-39732845):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41c046f7-220e-454f-b273-4e3401a0509e/trump-interactive-amp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41c046f7-220e-454f-b273-4e3401a0509e/trump-interactive-amp.png" sizes="100vw" caption="This looks like the same content as the normal article, but is pulling in a different iframe designed specifically for AMP" alt="Screenshot of BBC News AMP page containing same content as before, but content is clipped and has a Show More button" >}}

While the canonical and AMP versions look the same, **they are actually two different endpoints** with different behavior:

- The canonical version scrolls you to your chosen country when you submit the form.
- The AMP version doesn't scroll you, as you cannot scroll the parent page from within an AMP iframe.
- The AMP version shows a cropped iframe with a 'Show More' button, depending on viewport size and scroll position. This is a feature of AMP.

As well as the canonical and AMP versions of this article, this project was also shipped to the News App, which is yet another platform with its own intricacies and limitations. So **how do we do support all of these platforms?**

## Tooling Is Key

We don't build our content from scratch. We have a [Yeoman](https://yeoman.io)-based scaffold which uses Node to generate a boilerplate project with a single command.

New projects come with [Webpack](https://webpack.js.org/), [SASS](https://sass-lang.com/), deployment and a componentization structure out of the box. Internationalization is also baked into our projects, using a [Handlebars](https://handlebarsjs.com/) templating system. Tom Maslen writes about this in detail in his post, [13 tips for making responsive web design multi-lingual](https://responsivenews.co.uk/post/123104512468/13-tips-for-making-responsive-web-design).

Out of the box, this works pretty well for compiling for one platform but **we need to support multiple platforms**. Let's delve into some code.

### Embed vs. Standalone

In Visual Journalism, we sometimes output our content inside an iframe so that it can be a self-contained "embed" in an article, unaffected by the global scripting and styling. An example of this is the Donald Trump interactive embedded in the canonical example earlier in this article.

On the other hand, sometimes we output our content as raw HTML. We only do this when we have control over the whole page or if we require [really responsive scroll interaction](https://www.bbc.co.uk/news/resources/idt-c1dffc35-fe53-492d-a4bf-752a22bd1ebc). Let's call these our "embed" and "standalone" outputs respectively.

Let's imagine how we might build the "[Will a robot take your job?](https://www.bbc.co.uk/news/technology-34066941)" interactive in both the "embed" and "standalone" formats.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/475d321a-6b36-4ab4-9aa8-41f68d41a28b/embed-vs-standalone.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/475d321a-6b36-4ab4-9aa8-41f68d41a28b/embed-vs-standalone.png" sizes="100vw" caption="Contrived example showing an 'embed' on the left, versus the content as a 'standalone' page on the right" alt="Two screenshots side by side. One shows content embedded in a page; the other shows the same content as a page in its own right." >}}

Both versions of the content would share the vast majority of their code, but there would be some crucial differences in the implementation of the JavaScript between the two versions.

For example, look at the 'Find out my automation risk' button. When the user hits the submit button, they should be automatically scrolled to their results.

The "standalone" version of the code might look like this:

<pre><code class="language-javascript">button.on('click', (e) => {
    window.scrollTo(0, resultsContainer.offsetTop);
});
</code></pre>

But if you were building this as "embed" output, you know that your content is inside an iframe, so would need to code it differently:

<div class="break-out">

<pre><code class="language-javascript">// inside the iframe
button.on('click', () => {
    window.parent.postMessage({ name: 'scroll', offset: resultsContainer.offsetTop }, '*');
});

// inside the host page
window.addEventListener('message', (event) => {
    if (event.data.name === 'scroll') {
        window.scrollTo(0, iframe.offsetTop + event.data.offset);
    }
});
</code></pre></div>

Also, what if our application needs to go full screen? This is easy enough if you're in a "standalone" page:

<pre><code class="language-javascript">document.body.className += ' fullscreen';
</code></pre>

<pre><code class="language-css">.fullscreen {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c0c80b7-847c-4c8f-a173-b08cdf563454/full-screen-success.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c0c80b7-847c-4c8f-a173-b08cdf563454/full-screen-success.png" sizes="100vw" caption="We successfully use full-screen functionality to make the most of our map module on mobile" alt="Screenshot of map embed with 'Tap to Interact' overlay, followed by a screenshot of the map in full screen mode after it has been tapped." >}}

If we tried to do this from inside an "embed," this same code would have the content scaling to the width and height of the _iframe_, rather than the viewport:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4007ec28-b26e-4b00-928f-9dc3dd56f819/full-screen-fail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4007ec28-b26e-4b00-928f-9dc3dd56f819/full-screen-fail.png" sizes="100vw" caption="It can be difficult going full screen from within an iframe" alt="Screenshot of map example as before, but full screen mode is buggy. Text from the surrounding article is visible where it shouldn't be." >}}

...so in addition to applying the full-screen styling inside the iframe, we have to send a message to the host page to apply styling to the iframe itself:

<div class="break-out">

<pre><code class="language-javascript">// iframe
window.parent.postMessage({ name: 'window:toggleFullScreen' }, '*');

// host page
window.addEventListener('message', function () {
    if (event.data.name === 'window:toggleFullScreen') {
       document.getElementById(iframeUid).className += ' fullscreen';
    }
});
</code></pre></div>

This can translate into a lot of spaghetti code when you start supporting multiple platforms:

<div class="break-out">

<pre><code class="language-javascript">button.on('click', (e) => {
    if (inStandalonePage()) {
        window.scrollTo(0, resultsContainer.offsetTop);
    }
    else {
        window.parent.postMessage({ name: 'scroll', offset: resultsContainer.offsetTop }, '*');
    }
});
</code></pre></div>

Imagine doing an equivalent of this for every meaningful DOM interaction in your project. Once you've finished shuddering, make yourself a relaxing cup of tea, and read on.

## Abstraction Is Key

Rather than forcing our developers to handle these conditionals inside their code, we built an abstraction layer between their content and the environment. We call this layer the 'wrapper.'

Instead of querying the DOM or native browser events directly, we can now proxy our request through the `wrapper` module.

<pre><code class="language-javascript">import wrapper from 'wrapper';
button.on('click', () => {
    wrapper.scrollTo(resultsContainer.offsetTop);
});
</code></pre>

Each platform has its own wrapper implementation conforming to a common interface of wrapper methods. The wrapper wraps itself around our content and handles the complexity for us.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53762fb3-a68e-498f-b598-b242aee10704/uml-standalone.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53762fb3-a68e-498f-b598-b242aee10704/uml-standalone.png" sizes="100vw" caption="Simple 'scrollTo' implementation by the standalone wrapper" alt="UML diagram showing that when our application calls the standalone wrapper scroll method, the wrapper calls the native scroll method in the host page." >}}

The standalone wrapper's implementation of the `scrollTo` function is very simple, passing our argument directly to `window.scrollTo` under the hood.

Now let's look at a separate wrapper implementing the same functionality for the iframe:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d2d544-de6b-4c53-9186-faaa0f853e1a/uml-embed.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d2d544-de6b-4c53-9186-faaa0f853e1a/uml-embed.png" sizes="100vw" caption="Advanced 'scrollTo' implementation by the embed wrapper" alt="UML diagram showing that when our application calls the embed wrapper scroll method, the embed wrapper combines the requested scroll position with the offset of the iframe before triggering the native scroll method in the host page." >}}

The "embed" wrapper takes the same argument as in the "standalone" example but manipulates the value so that the iframe offset is taken into account. Without this addition, we would have scrolled our user somewhere completely unintended.

## The Wrapper Pattern

Using wrappers results in code that is cleaner, more readable and consistent between projects. It also allows for micro-optimisations over time, as we make incremental improvements to the wrappers to make their methods more performant and accessible. Your project can, therefore, benefit from the experience of many developers.

So, what does a wrapper look like?

## Wrapper Structure

Each wrapper essentially comprises three things: a Handlebars template, wrapper JS file, and a SASS file denoting wrapper-specific styling. Additionally, there are build tasks which hook into events exposed by the underlying scaffolding so that each wrapper is responsible for its own pre-compilation and cleanup.

This is a simplified view of the embed wrapper:

<pre><code class="language-javascript">embed-wrapper/
    templates/
        wrapper.hbs
    js/
        wrapper.js
    scss/
        wrapper.scss
</code></pre>

Our underlying scaffolding exposes your main project template as a Handlebars partial, which is consumed by the wrapper. For example, `templates/wrapper.hbs` might contain:

<pre><code class="language-html">&lt;div class="bbc-news-vj-wrapper--embed"&gt;
    {{&gt;your-application}}
&lt;/div&gt;
</code></pre>

`scss/wrapper.scss` contains wrapper-specific styling that your application code shouldn't need to define itself. The embed wrapper, for example, replicates a lot of BBC News styling inside the iframe.

Finally, `js/wrapper.js` contains the iframed implementation of the wrapper API, detailed below. It is shipped separately to the project, rather than compiled in with the application code &mdash; we flag `wrapper` as a global in our Webpack build process. This means that though we deliver our application to multiple platforms, we only compile the code once.

### Wrapper API

The wrapper API abstracts a number of key browser interactions. Here are the most important ones:

**`scrollTo(int)`**

Scrolls to the given position in the active window. The wrapper will _normalise_ the provided integer before triggering the scroll so that the host page is scrolled to the correct position.

**`getScrollPosition: int`**

Returns the user's current (normalized) scroll position. In the case of the iframe, this means that the scroll position passed to your application is actually _negative_ until the iframe is at the top of the viewport. This is super useful and lets us do things such as animate a component only when it comes into view.

**`onScroll(callback)`**

Provides a hook into the scroll event. In the standalone wrapper, this is essentially hooking into the native scroll event. In the embed wrapper, there will be a slight delay in receiving the scroll event since it is passed via postMessage.

**`viewport: {height: int, width: int}`**

A method to retrieve the viewport height and width (since this is implemented very differently when queried from within an iframe).

**`toggleFullScreen`**

In standalone mode, we hide the BBC menu and footer from view and set a `position: fixed` on our content. In the News App, we do nothing at all &mdash; the content is already full screen. The complicated one is the iframe, which relies on applying styles both inside and outside the iframe, coordinated via postMessage.

**`markPageAsLoaded`**

Tell the wrapper your content has loaded. This is crucial for our content to work in the News App, which will not attempt to display our content to the user until we explicitly tell the app our content is ready. It also removes the loading spinner on the web versions of our content.

### List Of Wrappers

In the future, we envisage creating additional wrappers for large platforms such as Facebook Instant Articles and Apple News. We have created six wrappers to date:

**Standalone Wrapper**

The version of our content that should go in standalone pages. Comes bundled with BBC branding.

**Embed Wrapper**

The iframed version of our content, which is safe to sit inside articles or to syndicate to non-BBC sites, since we retain control over the content.

**AMP Wrapper**

This is the endpoint which is pulled in as an `amp-iframe` into AMP pages.

**News App Wrapper**

Our content must make calls to a proprietary `bbcvisualjournalism://` protocol.

**Core Wrapper**

Contains only the HTML &mdash; none of our project's CSS or JavaScript.

**JSON Wrapper**

A JSON representation of our content, for sharing across BBC products.

## Wiring Wrappers Up To The Platforms

For our content to appear on the BBC site, we provide journalists with a namespaced path:

<div class="break-out">

<pre><code class="language-markup">/include/[department]/[unique ID], e.g. </code><code class="language-markup" style="font-weight: bold;">/include/visual-journalism/123-quiz</code></pre></div>

The journalist puts this "include path" into the CMS, which saves the article structure into the database. All products and services sit downstream of this publishing mechanism. Each platform is responsible for choosing the flavor of content it wants and requesting that content from a proxy server.

Let's take that [Donald Trump interactive](https://www.bbc.co.uk/news/world-us-canada-39732845) from earlier. Here, the include path in the CMS is:

<pre><code class="language-markup">/include/newsspec/15996-trump-tracker/english/index
</code></pre>

The canonical article page knows it wants the "embed" version of the content, so it appends `/embed` to the include path:

<pre><code class="language-markup">/include/newsspec/15996-trump-tracker/english/index</code><code class="language-markup" style="font-weight: bold;">/embed</code></pre>

...before requesting it from the proxy server:

<div class="break-out">

<pre><code class="language-markup">https://news.files.bbci.co.uk/include/newsspec/15996-trump-tracker/english/index/embed
</code></pre></div>

The AMP page, on the other hand, sees the include path and appends `/amp`:

<pre><code class="language-markup">/include/newsspec/15996-trump-tracker/english/index</code><code class="language-markup" style="font-weight: bold;">/amp</code></pre>

The AMP renderer does a little magic to render some AMP HTML which references our content, pulling in the `/amp` version as an iframe:

<div class="break-out">

<pre><code class="language-html">&lt;amp-iframe src="https://news.files.bbci.co.uk/include/newsspec/15996-trump-tracker/english/index/amp" width="640" height="360"&gt;
    &lt;!-- some other AMP elements here --&gt;
&lt;/amp-iframe&gt;
</code></pre></div>

Every supported platform has its own version of the content:

<div class="break-out">

<pre><code class="language-markup">/include/newsspec/15996-trump-tracker/english/index</code><code class="language-markup" style="font-weight: bold;">/amp</code>

<code>/include/newsspec/15996-trump-tracker/english/index</code><code class="language-markup" style="font-weight: bold;">/core</code>

<code>/include/newsspec/15996-trump-tracker/english/index</code><code class="language-markup" style="font-weight: bold;">/envelope</code>

...and so on</pre></div>

This solution can scale to incorporate more platform types as they arise.

## Abstraction Is Hard

Building a "write once, deploy anywhere" architecture sounds quite idealistic, and it is. For the wrapper architecture to work, we have to be _very_ strict on working within the abstraction. This means we have to fight the temptation to "do this hacky thing to make it work in [insert platform name here]." We want our content to be completely unaware of the environment it is shipped in &mdash; but this is easier said than done.

### Features Of The Platform Are Hard To Configure Abstractly

Before our abstraction approach, we had complete control over every aspect of our output, including, for example, the markup of our iframe. If we needed to tweak anything on a per-project basis, such as add a `title` attribute to the iframe for accessibility reasons, we could just edit the markup.

Now that the wrapper markup exists in isolation from the project, the only way of configuring it would be to expose a hook in the scaffold itself. We can do this relatively easily for cross-platform features, but exposing hooks for specific platforms breaks the abstraction. We don't really want to expose an 'iframe title' configuration option that's only used by the one wrapper.

We could name the property more generically, e.g. `title`, and then use this value as the iframe `title` attribute. However, it starts to become difficult to keep track of what is used where, and we risk abstracting our configuration to the point of no longer understanding it. By and large, we try to keep our config as lean as possible, only setting properties that have global use.

### Component Behaviour Can Be Complex

On the web, our [sharetools module](https://github.com/bbc/news-vj-sharetools) spits out social network share buttons that are individually clickable and open a pre-populated share message in a new window.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c692e55-b04b-42d9-848e-425607aa94bc/sharetools-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c692e55-b04b-42d9-848e-425607aa94bc/sharetools-web.png" sizes="100vw" caption="BBC Visual Journalism sharetools present a list of social share options" alt="Screenshot of BBC sharetools section containg Twitter and Facebook social media icons." >}}

In the News App, we don't want to share through the mobile web. If the user has the relevant application installed (e.g. Twitter), we want to share in the app itself. Ideally, we want to present the user with the native iOS/Android share menu, then let them choose their share option before we open the app for them with a pre-populated share message. We can trigger the native share menu from the app by making a call to the proprietary `bbcvisualjournalism://` protocol.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d5d8f5-9555-4f8c-a04b-61c95ea0108a/sharetools-app-popup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d5d8f5-9555-4f8c-a04b-61c95ea0108a/sharetools-app-popup.png" sizes="100vw" caption="Native share menu on Android" alt="Screenshot of the share menu on Android with options for sharing via Messaging, Bluetooth, Copy to clipboard, and so on." >}}

However, this screen will be triggered whether you tap 'Twitter' or 'Facebook' in the 'Share your results' section, so the user ends up having to make their choice twice; the first time inside our content, and a second time on the native popup.

This is a strange user journey, so we want to remove the individual share icons from the News app and show a generic share button instead. We are able to do this by explicitly checking which wrapper is in use before we render the component.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a19e4d0-cf02-4ee4-932b-d791a0b55f55/sharetools-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a19e4d0-cf02-4ee4-932b-d791a0b55f55/sharetools-app.png" sizes="100vw" caption="Generic share button used in the News App" alt="Screenshot of the news app share button. This is a single button with the following text: 'Share how you did'." >}}

Building the wrapper abstraction layer works well for projects as a whole, but when your choice of wrapper affects changes at the _component_ level, it's very difficult to retain a clean abstraction. In this case, we've lost a little abstraction, and we have some messy forking logic in our code. Thankfully, these cases are few and far between.

### How Do We Handle Missing Features?

Keeping abstraction is all well and good. Our code tells the wrapper what it wants the platform to do, e.g. "go full screen." But what if the platform we're shipping to can't actually go full-screen?

The wrapper will try its best not to break altogether, but ultimately you need a design which gracefully falls back to a working solution whether or not the method succeeds. We have to design defensively.

Let's say we have a results section containing some bar charts. We often like to keep the bar chart values at zero until the charts are scrolled into view, at which point we trigger the bars animating to their correct width.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11cf34de-cc60-4ec1-9112-294eff70fd6c/barchart-with-values.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11cf34de-cc60-4ec1-9112-294eff70fd6c/barchart-with-values.png" sizes="100vw" caption="Bar chart showing values relevant to my area" alt="Screenshot of a collection of bar charts comparing the user's area with the national averages. Each bar has its value displayed as text to the right of the bar." >}}

But if we have no mechanism to hook into the scroll position &mdash; as is the case in our AMP wrapper &mdash; then the bars would forever remain at zero, which is a thoroughly misleading experience.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4afba113-eb38-483b-9f8e-6aa24bc8a3fb/barchart-with-zeroes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4afba113-eb38-483b-9f8e-6aa24bc8a3fb/barchart-with-zeroes.png" sizes="100vw" caption="How the bar chart could look if scrolling events aren't forwarded" alt="Same screenshot of bar charts as before, but bars have 0&#37; width and the values of each bar are fixed at 0&#37;. This is incorrect." >}}

We are increasingly trying to adopt more of a progressive enhancement approach in our designs. For example, we could provide a button which will be visible for all platforms by default, but which gets hidden if the wrapper supports scrolling. That way, if the scroll fails to trigger the animation, the user can still trigger the animation manually.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca1b2f48-0000-4aa9-8a84-677b77a875b3/barchart-with-fallback.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca1b2f48-0000-4aa9-8a84-677b77a875b3/barchart-with-fallback.png" sizes="100vw" caption="We could display a fallback button instead, which triggers the animation on click." alt="Same screenshot of bar charts as the incorrect 0&#37; bar charts, but this time with a subtle grey overlay and a centered button inviting the user to 'View results'." >}}

## Plans For The Future

We hope to develop new wrappers for platforms such as Apple News and Facebook Instant Articles, as well as to offer all new platforms a 'core' version of our content out of the box.

We also hope to get better at progressive enhancement; succeeding in this field means developing defensively. You can never assume all platforms now and in the future will support a given interaction, but **a well-designed project should be able to get its core message across** without falling at the first technical hurdle.

Working within the confines of the wrapper is a bit of a paradigm shift, and feels like a bit of a halfway house in terms of the *long-term* solution. But until the industry matures onto a cross-platform standard, publishers will be forced to roll out their own solutions, or use tooling such as [Distro](https://distro.mic.com/) for platform-to-platform conversion, or else ignore entire sections of their audience altogether.

It's early days for us, but so far we've had great success in using the wrapper pattern to build our content once and deliver it to the myriad of platforms our audiences are now using.

{{< signature "rb, ra, il" >}}

