---
title: 'Revisiting Firefox’s DevTools'
slug: revisiting-firefox-devtools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45de18eb-a1a3-48c2-b81d-6a85bd963a95/excerpt-firefox-devtools.png
date: 2015-12-30T20:46:18.000Z
author: patrickbrosset
summary: >-
  A walk through some of the main tools and differential features of Firefox Developer Edition. Patrick Brosset explores how this browser can be used to keep updated about the latest tools for CSS features and animations, testing website displays and some tips and tricks for developers and designers.
description: >-
  In this article, Patrick Brosset explores how this browser can be used to keep updated about the latest tools for CSS features and animations, testing website displays and some tips and tricks for developers and designers.
categories:
  - Coding
  - Tools
  - Workflow
  - Browsers
---

If you do any kind of development for the web, then **you know how important tools are**, and you like finding tools that make your life easier. Developing and testing new browser features, however, takes time. Between the time a useful tool first appears in an experimental nightly build and the time it’s available for everyone to use in Firefox, a while has passed.

That’s one of the reasons Mozilla released [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) in November 2014 as the recommended Firefox browser for developers. It **gets new feature updates more quickly** so that you can use the latest tools.

Of course, testing your websites in the standard Firefox release is still crucial. Thankfully, Developer Edition makes this easy by letting you run both programs side by side. Plus, Developer Edition comes with a slick new theme that matches its tools.

## A Bit Of History

How far back do we go? Way back in 2001, a debugger called “Venkman” was available for Netscape Navigator version 7. The Netscape corporation had a system for UIs named XML User Interface Language (XUL). It also had a love of the movie “Ghostbusters” and its demonic character Zuul; so, Rob Ginder, who wrote that early debugger, had four options for naming his new debugger, and Venkman beat out Stantz, Spengler and Zeddemore.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8227baa8-9568-465c-b280-d4b07db23f92/1-venkman-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8227baa8-9568-465c-b280-d4b07db23f92/1-venkman-opt.png" alt="UI of the Venkmann JavaScript debugger" /></a><figcaption>Venkman, the JavaScript debugger. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8227baa8-9568-465c-b280-d4b07db23f92/1-venkman-opt.png">View large version</a>)</figcaption></figure>

Venkmann was just a JavaScript debugger. It couldn’t inspect the DOM or show network traffic. Netscape had a built-in console, but that was it as far as debugging tools went.

{{% feature-panel %}}

The next piece of the puzzle was the **DOM inspector**, which was released around 2004 or 2005. It wasn’t friendly to web developers, and it was about debugging XUL as much as HTML.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0876da7-f969-4491-8f7d-db488c320645/2-dom-inspector-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0876da7-f969-4491-8f7d-db488c320645/2-dom-inspector-opt.png" alt="DOM Inspector add-on" /></a><figcaption>DOM Inspector add-on. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0876da7-f969-4491-8f7d-db488c320645/2-dom-inspector-opt.png">View large version</a>)</figcaption></figure>

So, in early 2006 Firefox had three pieces of the puzzle: a built-in console, a debugger and a DOM inspector &mdash; each separate and not all built in.

In late 2006 Joe Hewitt, who worked on the early release of Firefox, released Firebug version 1.0. Firebug broke new ground in allowing developers to view the DOM and in providing a JavaScript console and debugger and DOM inspector all in the same tool.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a88082b-a5e9-466e-a0ab-678be82849e4/3-firebug-opt.jpeg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a88082b-a5e9-466e-a0ab-678be82849e4/3-firebug-opt.jpeg" alt="The first Firebug UI" /></a><figcaption>Firebug, an all-in-one developer tool. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a88082b-a5e9-466e-a0ab-678be82849e4/3-firebug-opt.jpeg">View large version</a>)</figcaption></figure>

But Firebug was never an official Mozilla project, and with Joe’s departure to Parakey and then Facebook, the development of Firebug was taken up by a group of volunteers led by John J. Barton. Mozilla contributed to the project, supporting Honza Odvarko, who led the project after John left.

In 2011 Mozilla decided that it needed to put more effort into its developer tools and start from a clean slate to build some next-generation tools, while continuing to support the maintenance of Firebug.

One of the challenges with developer tools is that they **need to reach deep into the platform** to understand how the system works. They need to be a part of the browser and can’t easily be made as add-ons.

So, as Firefox gets updated, keeping Firebug running as a separate add-on becomes harder and harder. Upgrading the debugger APIs, which Firebug needed to keep up with, was significant work, and when the initiative to have separate browser and content processes in Firefox was announced, **Mozilla decided to rebuild Firebug on top of the built-in tools**.

## A Solid Set Of Standard Features

Firefox’s DevTools have come a long way since their inception, quickly bridging the gaps between Firebug and other browsers’ developer tools. It now has all of the tools you’d expect from a browser. Let’s go through some of the main ones.

The [page inspector](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector) has a a box-model highlighter, a CSS rules editor, a viewer for computed styles, fonts and layout, support for pseudo-elements, and a search tool.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba33f3d4-a508-4647-b418-4da5d4c0ba39/4-inspector-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba33f3d4-a508-4647-b418-4da5d4c0ba39/4-inspector-opt.png" alt="The Page Inspector" /></a><figcaption>The page inspector. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba33f3d4-a508-4647-b418-4da5d4c0ba39/4-inspector-opt.png">View large version</a>)</figcaption></figure>

The [web console](https://developer.mozilla.org/en-US/docs/Tools/Web_Console) lists JavaScript, CSS, and network and security logs. It supports custom formatting, as well as previews and inspection of DOM nodes, objects and arrays, allowing you to search and filter them.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1036adc2-f52c-45d3-b788-0d7eb19c7629/5-console-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1036adc2-f52c-45d3-b788-0d7eb19c7629/5-console-opt.png" alt="The web console" /></a><figcaption>The web console. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1036adc2-f52c-45d3-b788-0d7eb19c7629/5-console-opt.png">View large version</a>)</figcaption></figure>

The [JavaScript debugger](https://developer.mozilla.org/en-US/docs/Tools/Debugger) lets you halt the execution of scripts at any point, navigate the call stack and inspect variables. It supports source maps, pretty printing of minified sources, and black boxing of library files. And it supports dynamically evaluated scripts.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f46a032d-5e00-4d2f-b79d-61ebffebf962/6-debugger-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f46a032d-5e00-4d2f-b79d-61ebffebf962/6-debugger-opt.png" alt="The JavaScript debugger" /></a><figcaption>The JavaScript debugger. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f46a032d-5e00-4d2f-b79d-61ebffebf962/6-debugger-opt.png">View large version</a>)</figcaption></figure>

The [network monitor](https://developer.mozilla.org/en-US/docs/Tools/Network_Monitor) lists all requests that Firefox makes for a web page. It displays headers, responses and cookies, letting you search through them. It also shows a performance analysis of the page load.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a50f480-081c-4c91-ada0-4ad23f681dc2/7-netmonitor1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a50f480-081c-4c91-ada0-4ad23f681dc2/7-netmonitor1-opt.png" alt="The network monitor's requests list" /></a><figcaption>The network monitor’s requests list. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a50f480-081c-4c91-ada0-4ad23f681dc2/7-netmonitor1-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bdb838b-6ff2-4e9d-986e-50404711fbdd/8-netmonitor2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bdb838b-6ff2-4e9d-986e-50404711fbdd/8-netmonitor2-opt.png" alt="The network monitor performance analysis" /></a><figcaption>The network monitor’s performance analysis. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bdb838b-6ff2-4e9d-986e-50404711fbdd/8-netmonitor2-opt.png">View large version</a>)</figcaption></figure>

The [performance tools](https://developer.mozilla.org/en-US/docs/Tools/Performance) give you insight into a website’s JavaScript and layout performance by recording browser activity over time and exposing frame-rate data, memory usage, JavaScript calls and browser-rendering events such as styling, layout and paints.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9916735b-194a-46f3-93e3-fe8276c04c52/9-performance1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9916735b-194a-46f3-93e3-fe8276c04c52/9-performance1-opt.png" alt="The performance tool's waterfall graph" /></a><figcaption>The performance tool’s waterfall graph. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9916735b-194a-46f3-93e3-fe8276c04c52/9-performance1-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e5ee000-403d-4b42-b388-a321ccccfd68/10-performance2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e5ee000-403d-4b42-b388-a321ccccfd68/10-performance2-opt.png" alt="The performance tool's JavaScript flame chart" /></a><figcaption>The performance tool’s JavaScript flame chart. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e5ee000-403d-4b42-b388-a321ccccfd68/10-performance2-opt.png">View large version</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

## Some Key Differentiators

On top of the usual set of tools, Firefox has a number of neat features to make your life as a developer or designer easier. We’ll go over some of them now, but download [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) and try them out for yourself.

### Work With Animations

CSS animations and transitions are a great way to improve the UX of a website, but they’re also **hard to get right**, and they can easily get in the way instead of guiding the user’s flow. If you want your animations to look and feel just right, then you’ll need to spend time finetuning those keyframes, durations and timing functions. Firefox comes with a set of tools to help with just that. Let’s go through a few.

#### Timing Function

The [timing function](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Work_with_animations#Edit_timing_functions) drives the way that an animation or transition progresses through time. Timing functions are often described with a cubic-bezier curve. Coming up with the perfect curve is not straightforward; so, Firefox’s DevTools comes with a **tooltip** that allows you to modify a curve visually or even choose from a list of presets.

{{< youtube IEUonpRmX64 >}}

CSS animations are described with a set of [@keyframe rules](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Work_with_animations#Edit_keyframes). Firefox displays these keyframe rules in the view for CSS rules when the selected element is animated, so that you can directly **edit** them there, where you’d expect. You can even edit keyframe properties while an animation is playing.

{{< youtube K_DvRJBTbKk >}}

#### Animation Inspector

[The animation inspector](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Work_with_animations#Animation_inspector) allows you to view all individual animations on a page, detect when they get added or removed, as well as pause them at any point, slow them down or speed them up. It’s a powerful feature for looking at animations in detail.

{{< youtube x6METmQLswQ >}}

### Test on Multiple Devices, Browsers and Screens

When it comes to making sure a website displays correctly for everyone, things are a lot more complex than they used to be. We now have to deal with many aspect ratios and pixel densities, as well as many browsers on all sorts of operating systems and devices. Thankfully, Firefox comes with tools just for this.

#### Responsive Design View

[The responsive design view](https://developer.mozilla.org/en-US/docs/Tools/Responsive_Design_View) makes it really easy to see how a website looks at different screen sizes. Either choose a size from the list of presets or adjust the size to anything you want by entering custom dimensions or dragging the viewport. The responsive design view can quickly be toggled from the keyboard (Command + Alt + M or Control + Shift + M) or by clicking the corresponding icon in the DevTools toolbar.

{{< youtube OZ4kv4jsDoc >}}

#### Valence

[Valence](https://github.com/mozilla/valence) is an add-on that comes preinstalled with Firefox’s WebIDE. WebIDE already allows you to connect Firefox’s DevTools to any website or app on Firefox OS and in Firefox for Android. Now, with Valence, you can also connect the tools to Chrome on Android and the desktop and to Safari on iOS and Mac OS X. Valence gives you pretty much all you need for multi-browser testing without having to leave the DevTools you’re used to.

{{< youtube roCrC-VB-AY >}}

#### Developer Toolbar

The developer toolbar (GCLI) has a handy media command that’s useful for emulating any media type in the browser. It’s very useful for testing your website’s print CSS, for instance.

{{< youtube japR143cWbE >}}

### Discover, Use and Understand Complex CSS Features

CSS can be complex. Some strings of syntax are hard to remember, some you might not even know about, and others, even ones you know of, have effects that are hard to predict. Firefox’s DevTools, being built into the browser, are ideally positioned to give you all of the information necessary to work with the syntax. Let’s see some examples.

#### CSS Properties Tooltips

The [CSS properties tooltips](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_and_edit_CSS#Get_help_for_CSS_properties) help you remember the different values and syntax constructions that properties can have. Firefox makes it super-easy to get documentation for any CSS property directly in the tools where you need it. Right-click on any property’s name in the CSS rules editor to get documentation in a tooltip, with a list of possible values and documentation about them, too.

{{< youtube j9cZ_giWvQ0 >}}

#### CSS Transforms Previewer

[The CSS transforms previewer](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Visualize_transforms) helps you understand how a given set of transform functions have changed an element. The `transform` property is the sort of CSS property that is hard to get right just by looking at the code; a visual rendering of what has happened is usually much better. The CSS transform previewer highlights the element as it was before and after it got transformed, so that you can easily see the effect of the transformation.

{{< youtube dG9Ma776yVE >}}

#### CSS Filter Tooltip

Filters are a relatively new feature in CSS and really powerful. With them, you can blur, add shadow or rotate the colors of any element simply. Writing a valid CSS filter function isn’t the easiest thing in the world, and you can chain as many functions as you want, so Firefox’s DevTools has a handy [tooltip that allows you to create filters](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Edit_CSS_filters) in a simple and visual way.

{{< youtube 3vFUW7LxCfs >}}

{{% ad-panel-leaderboard %}}

### Miscellaneous Tips and Tricks

Ever need to take a screenshot of all or part of a page? Capturing web pages or parts of web pages as images is a powerful way to show a design or a bug to other people. Doing this in Firefox is easy, either by right-clicking on any node in the page inspector or by using the full-page screenshot button in the toolbar (make sure it’s enabled in the options panel first).

{{< youtube nxj4lZFfPfc >}}

#### Eyedropper Tool

[The eyedropper](https://developer.mozilla.org/en-US/docs/Tools/Eyedropper) tool is useful for sampling any color from a page. If you need to copy the color of any part of a web page or want to change the color on an element’s CSS property, then use the eyedropper. In the CSS rules view, with an element selected, click on the color swatch next to any `color` property’s value to change it. Or, in the developer menu bar, choose the eyedropper item to copy colors from the page.

{{< youtube S7CLo5U5tog >}}

Highlight all elements that match a selector by clicking on the selector icon in the CSS rules view.

{{< youtube i2PQZ6-NwnQ >}}

#### CSS Rules View Search Bar

Filter styles using the [CSS rules view search bar](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_and_edit_CSS#Filtering_rules). This might be helpful if you’re not sure which property has overridden another.

{{< youtube IdS8rHUGls8 >}}

## Closing Words

Firefox’s DevTools have evolved quite rapidly in recent years, and feature-packed versions are now getting released every six weeks. The project is being driven by an [active community](http://firefox-dev.tools/#getting-in-touch), which you can be a part of!

Feel free to download [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) to try out the latest version of the tools. And stay up to date on new features at [Mozilla Hacks](https://hacks.mozilla.org/category/developer-tools/).

#### Further Reading

-   [What’s New In DevTools?](https://www.smashingmagazine.com/2022/01/devtools-updates-2022/)
-   [What’s New With DevTools: Cross-Browser Edition](https://www.smashingmagazine.com/2021/09/devtools-cross-browser-edition/)
-   [DevTools Debugging Tips And Shortcuts (Chrome, Firefox, Edge)](https://www.smashingmagazine.com/2021/02/useful-chrome-firefox-devtools-tips-shortcuts/)
-   [A Guide To New And Experimental CSS DevTools In Firefox](https://www.smashingmagazine.com/2019/10/guide-new-experimental-css-devtools-firefox/)

{{< signature "rb, jb, al, mrn" >}}
