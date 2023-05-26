---
title: The Vanilla Web Diet
slug: the-vanilla-web-diet
image: null
date: 2012-11-13T13:12:12.000Z
author: christian-heilmann
description: >-
  **Editor's note**: This is an introductory article about how we build websites to ensure they are leaner and more future-proof. At the end of the article, we'd ask you to fill out a quick survey to show your interest.
categories:
  - Coding
  - Tools
  - Performance
---
**Editor's note**: _This is an introductory article about a **book idea** to be published by Smashing Magazine with Chris Heilmann. Check out what we propose as an idea — explaining a way to reconsider how we build websites to ensure they are leaner and more future-proof. At the end of the article, we'd ask you to fill out a quick survey to show your interest._

The Web as it is now is suffering from an obesity problem. If you surf the Web on a flaky mobile connection or some hotel wireless, you'll find yourself a lot of times staring at a page or app that doesn't do anything and doesn't tell you what is going on either. The spinner in the tab or the URL bar seems to be the thing that gets the most mileage in browsers. Surfing with a net tab open in your developer tools shows you an incredible amount of data being sent for seemingly very simple end products.

Why is that? Shouldn't years of Web development and advocacy about performance by [Yahoo](https://developer.yahoo.com/performance/) and [Google](https://developers.google.com/speed/docs/best-practices/rules_intro) and many others have born fruit and made us aware of how much each HTTP request costs? If you look at the final products, it doesn't seem that way.

[![The Vanilla Web Diet](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8b57d7d-40cc-4fc5-9f6f-13c8fd7833ab/vanilla-500-1.jpg)](https://www.flickr.com/photos/seelensturm/4638581563/)  
_Image Credit: [seelensturm](https://www.flickr.com/photos/seelensturm/4638581563/)._

## Reasons For An Obese Web

There are a few reasons why our Web is on the chubby side, and most of them actually are possible for us as developers to change.

{{% feature-panel %}}

### We Don't Develop in Realistic Environments

Probably the main reason is that as developers, we work on fast and big computers connected to a fat line, and the first time someone tests our products on slow connections is during quality assurance (QA). And as QA is the first thing to get ditched when deadlines are not met, sometimes this never happens at all.</p>

### Clinging On to the Past

Another reason for the love handles on our Web products is a false sense of allegiance to outdated and old technology, namely browsers of the '90s that refuse to go away. There are many attempted solutions to the problem of legacy environments, each of them with its own problems. The fact is that there are a lot of end users out there on terribly outdated computers with — in our view — bad browsers and probably limited connections. These users should not be blocked out, but they should also not dictate what we build.</p>

### Browser Differences

Another big reason is the annoyance of browser differences. There are not many Web technologies and APIs where all browsers are in agreement when it comes to supporting them, and many times we need to repeat code and fork and test to give the same functionality to all of them.</p>

## Embracing The Chaos And Celebrating Differences

The last point is the main mistake we make: instead of embracing the chaos that is the Web and our end users' environments and abilities, we don't seem to be able to give up on the dream of having a product that works and looks exactly the same everywhere.</p>

### My Browser Isn't the World?

In the worst case, we try to achieve this by blocking out all the browsers we don't like and proclaiming proudly that “everybody uses browser X and whoever doesn't is an enemy of the modern web.” This, of course, is just lying to ourselves, and is based on the fleeting concept of a “modern web.” A lot of the most terrible web-based products out there were built years ago to only work in Internet Explorer (IE) 6, which was the bee's knees at that time. It does not matter which cool hardware has a hardwired browser that is hot right now — we are making the same mistake again if we only build to one browser and lock out others.

Locking out any browser means actually writing more code to test for browsers, and it is almost impossible to reliably detect which browser is in use. If you want proof, just take a quick look at the user agent string of the [Yandex browser](https://browser.yandex.com/), which contains the names of almost every browser engine out there:

_Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_2) AppleWebKit/536.5 (KHTML, like Gecko) YaBrowser/1.0.1084.5402 Chrome/19.0.1084.5402 Safari/536.5_

I hope we can agree that building for one browser (or engine) only works for you if you are targeting a certain market and group, and even then you are not safe from losing them in the near future.</p>

## Libraries Are The Future

Another attempt to achieve the dream of cross-browser uniformity is a strategy of abstraction, using libraries, polyfills and frameworks to allow us to write in one language and have all the browser-difference magic happen under the hood. For production use, this is a very good idea. In the long run, libraries should get us where we want to be — almost every software environment, sooner or later, is running using libraries that unify the access to hardware or data APIs. For app development, we need to define and nurture these libraries and use them to our advantage.</p>

## Built-In Redundancy

The issue we have now, though, is that libraries and abstraction frameworks are becoming the starting point, and in the case of simple websites with a bit of extra flair, they are not needed. We just started to use them without considering their impact or even forgot how to do things without them. And in many cases, a lot of the things we do with them are already available in the browser for us, we just need to use what is there instead of simulating it. Libraries themselves start to suffer from obesity, and in a lot of cases, the extra fat is the functionality to make legacy browsers do things they were never meant to do but that browsers based on the HTML5 specification have already built in.</p>

## Death By A Thousand Plugins

Misuse of abstraction of code is rampant these days. We use libraries and converters that allow us to write the least amount of code possible to achieve a lot. This comes with a price. The three lines we write in an abstracted language can result in dozens after conversion to browser-understandable code. It is very tempting to use 20 small scripts on our pages when all of them are just a few lines, but this amounts to a mass of HTTP requests and generated code that chokes the browser. As we never see this code, it doesn't appear to be our mistake — we just wrote the least amount of code possible. Surely adding yet another script with just five lines of code can't make a difference?

So this is where we should start thinking harder about what we do right now. We've become dependent on abstractions for the most simple things and follow a cult of adding lots of helper tools, as they make things much simpler and are needed for a product to be maintainable and able to grow. A lot of the best practices in Web development were found and defined by large companies who had to build products that are maintained across different countries and teams and have to stand up to the requests of millions of users. What is a best practice for the Yahoo homepage or Gmail does not necessarily have to be what makes your smaller product most effective.

Jonathan Snook has a great example of this when he talks about his [SMACCS](https://smacss.com/) approach to writing CSS. He points out that almost every product starts with a `reset.css` file, but once finished, removing that file doesn't show any difference at all because for the elements we use we do define the margin, padding and sizing.</p>

## A Vanilla Diet For The Web

So here is what I propose: we need to put the Web on a diet, using vanilla Web technology that comes with browsers. As Alex Russell put it in his talk at Fronteers this year, if we want to change the Web it is up to us to move it ahead, and using polyfills and libraries is a future tax we currently pay.

Every successful diet is connected with a change in lifestyle. For the Vanilla Web Diet, here is what I propose we can do to slim down the products we build. This will not be applicable to everything, of course, and there is a place to start with a library and an abstraction layer. As I said before, sooner or later we will have an environment where libraries allow us to build great apps and products. But for a simple website with a few enhancements, it is time we stop randomly putting things together because they look shiny or seem very small.

The principles of a vanilla Web diet:

*   **Build on what works**  
    Our base layer should be HTML, plain and simple and doing the thing the product is meant to do. Something that looks like a button but doesn't do anything is not helping our users. When everything else fails, HTML is the thing users get — let's not deprive them of that.
*   **Lack of support is an opportunity**  
    If an old browser cannot do something, it allows us to test for that and not give it that functionality. In 99% of cases, the functionality is a nice-to-have and not needed.
*   **Browser-specific code cannot be trusted**  
    Every functionality you make dependent on browser-prefixed code adds to the landfill of code that breaks very, very soon.
*   **Use a mix of technologies — each for what it does best**  
    It is very tempting to do everything in JavaScript, but it is not needed.
*   **Ask questions**  
    Whatever you do should be wrapped in an “if,” making sure that only environments that can apply what you want get it.
*   **Write as much as needed, not the least possible**  
    Let's think about what we write before we write it, instead of adding lots of small, quick solutions.
*   **It is not about what you can add — it is about what we can't take away**  
    Basic functionality should always be there.
*   **Usefulness beats consistency across browsers**  
    Instead of giving everyone the same experience, always consider what is the best way to ensure people can use what we build.
*   **Load only what is needed**  
    Why should a browser get a library or a data file if it cannot do anything with it?
*   **Analyzing effects beats adding FX**  
    If you want to add shiny things, make sure they can perform in a shiny fashion; nobody likes their browser to slow down for a laggy effect.
*   **Strong foundations beat a possible future addition**  
    A lot of times we add a lot of code and interfaces to allow for a future that will need them. This future hardly ever comes about. Let's build for the now.

## A Quick Example: Adding A Video To A Website

Let's take a simple example: adding a video to a page. Conditioned and burdened with years of Web development, our thinking might be:

*   HTML5 video is nice, as it is native to the browser, the controls are readily accessible and I could build my own controls using the JavaScript API that comes with it.
*   Older versions of IE, however, don't play any HTML5 video, so I need to add a Flash fallback.
*   Furthermore, not all browsers support MP4, so I need to have the video in two formats, MP4 and WebM, as well as OGV if I want to support even older Firefox and Opera.

With these in mind, we'll probably get a video player from GitHub and use that one. The video player would be clever enough to recognize what the current browser supports and write out a Flash video or a native video. It will not help with the codec and browser support issue, unless we also use a player that detects that and sends the correct format, like [Vid.ly](https://m.vid.ly/user/).

That makes everybody happy and ensures everyone can see the video, right? True, but it also adds a lot of overhead that is really not needed. Let's think about the use cases here:

*   If I am on an old browser, do I want to load a JavaScript library, have some detection happening and get a Flash player? What if I have no Flash? I loaded a library for nothing and I still cannot get to the video at all.
*   If I am on a modern browser, I loaded a library, and if I have Flash enabled, then I will get a Flash player with all the memory consumption and initialization overhead (granted, this isn't much, but on my MacBook Air for example, the fan mostly starts because of Flash).

A vanilla diet approach to this would be the following:

	<pre><code class="language-markup">&lt;video controls="">
	    &lt;source src="hedgehogs.mp4" type="video/mp4">
	    &lt;source src="hedgehogs.webm" type="video/webm">
	    &lt;a href="hedgehogs.mp4" style="border: medium none;">
	        &lt;img src="/web/20121114223746im_/https://www.smashingmagazine.com:80/2012/11/13/the-vanilla-web-diet/hedgehogs.jpg" alt="Frolicking hedgehogs">
	    &lt;/a>
	    Click image above to download video
	&lt;/video></code></pre>

HTML5 video-capable browsers will show the video, and others will get an image preview linked to the video. This way, users on old computers and bad connections or browsers without HTML5 video capability will get an image and can watch the movie in the video app of their operating system. They can even do something else while the video is downloading instead of staring at a “buffering” message.

Is is too much work to have the video in two formats? Fine, use one and move the link out of the video tag — that way you offer the option to download the video to everyone on flaky connections:

<pre><code class="language-markup">&lt;video src="https://www.smashingmagazine.com/2012/11/13/the-vanilla-web-diet/hedgehogs.mp4" controls="">
	    &lt;img src="https://www.smashingmagazine.com/2012/11/13/the-vanilla-web-diet/hedgehogs.jpg" alt="Frolicking hedgehogs">
	&lt;/video>
	&lt;a href="hedgehogs.mp4">Download video (MP4, 3MB)&lt;/a></code></pre>

Don't want your video to be downloadable? Use Flash or Silverlight. This will not stop anyone dedicated enough to download it, but it makes sure you've done your part in securing the content. It blocks quite a few potential customers and readers, though.</p>

## Another Example: Expandable News Items

A lot of times we use a JavaScript library to have some headings that, when clicked or rolled over, show some paragraphs below them. jQuery's `show()` and `hide()` are meant for that and there are a myriad of plugins to give us that functionality.

If you want to do this in a vanilla Web diet way, there is no need for JavaScript. Let's start with the HTML. There are many right and wrong ways to do this — lists, definition lists, headings and `div`s and so on. Many an hour was wasted on forums discussing what the perfect markup is for this. Taking a leaf out of Nicole Sullivan's book, let's apply some [OOCSS](https://oocss.org/) and make ourselves independent of the element names by adding classes:

<pre><code class="language-markup tmp-html">&lt;article class="collapsible"&gt;
  &lt;h1 class="trigger"&gt;Interesting news&lt;/h1&gt;
  &lt;p class="content"&gt;Amazing stuff happened&lt;/p&gt;
&lt;/article&gt;</code></pre>

Now, in order to make these collapse and expand in a smooth way, all we need to do is apply some CSS:

<pre><code class="language-css">.collapsible .content {
  overflow: hidden;
  max-height: 0;
  opacity: 0;
  transition: 1s;
}
.collapsible:hover .content,
.collapsible:focus .content {
  max-height: 200px;
  opacity: 1;
}</code></pre>

Here you can see some of the principles in action. Older versions of IE do not understand `max-height` or `opacity`, so they will never apply the styles that hide the content. The much larger `max-height` of the hover and focus states makes sure that the browser expands the content all the way (it will always go to the real height, the only problem you will have is when the content is higher than 200 pixels, so this is something to point out to whoever is maintaining the code). The transition of one second makes sure the browser does this smoothly instead of just showing the content. Browsers that don't support transitions still show and hide the content. You can add browser-prefixed transitions, too. Firefox and IE10 already dropped the prefix for transitions and others will follow.

Now, if you want to add `onclick` functionality to the header, we need some JavaScript. First of all, though, we change our CSS to look for a class on the collapsible element instead of relying on hover. We also make the hiding dependent on a JavaScript class as we don't want to hide the content in browsers that don't fulfill all the requirements of our script.

<pre><code class="language-css">.js .collapsible .content {
  overflow: hidden;
  max-height: 0;
  opacity: 0;
  transition: 1s;
}
.js .collapsible.show .content {
  max-height: 200px;
  opacity: 1;
}</code></pre>

When the user clicks the header, we want to add the class of `show` to the collapsible element, and then remove it the next time the user clicks. For this, all we need is a single event handler on the document. To remove and add the class, we could change the `className` property, but newer browsers have the much more flexible [`classList`](https://developer.mozilla.org/en-US/docs/DOM/element.classList) implementation. We test for the things we use in an if statement and end up with not much code at all:

<pre><code class="language-javascript">if (addEventListener &amp;&amp; 'classList' in document.body) {
 document.body.classList.add('js');
 document.addEventListener('click', function(ev){
   var t = ev.target;
   if (t.classList.contains('trigger')) {
     t.parentNode.classList.toggle('show');
   }
 }, true);
}</code></pre>

Older versions of IE don't understand `addEventListener()`, so this will not be executed as we test for its existence. If `classList` is supported, we apply a click handler to the document. We then test for and toggle the `show` class to trigger the CSS change using `classList` whenever the element with the class trigger is clicked.</p>

## More?

Now here's the idea: I am planning to write a book about this, published with and by Smashing Magazine. I really believe that there is a lot to be said about the things in HTML5 that browsers now give us and that allow us to write simple and effective code to release pragmatic products instead of adding a lot of code we just don't need for what we want to achieve.

If you are interested, quickly fill out the survey below or drop us a comment and we'll go ahead.

Loading...

