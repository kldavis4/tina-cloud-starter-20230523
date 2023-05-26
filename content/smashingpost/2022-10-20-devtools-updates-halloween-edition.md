---
title: 'What’s New In DevTools: Halloween Edition 🎃'
slug: devtools-updates-halloween-edition
author: patrickbrosset
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbfdc666-af60-48cf-9c7c-c9a1eb8ecb34/devtools-updates-oct-2022.jpg
date: 2022-10-20T14:00:00.000Z
summary: >-
  In this article, Patrick Brosset gives an update on the most impactful new features that are now available in DevTools, across Firefox, Chrome, Safari, and Edge.
description: >-
  In this article, Patrick Brosset gives an update on the most impactful new features that are now available in DevTools, across Firefox, Chrome, Safari, and Edge.
categories:
  - Tools
  - Browsers
  - Debugging
  - DevTools
  - Testing
---

I can’t believe it’s already been nine months since I last wrote about [the new DevTools features](https://www.smashingmagazine.com/2022/01/devtools-updates-2022/) across browsers! You folks are due for an update. And what an update this is going to be!

Our friendly DevTools teams at Mozilla, Google, Microsoft, and Apple have once again been hard at work. And in this article, I’ll attempt to summarize the most impactful new features that are now available in browser developer tools.

So much has happened over these past few months that I may have missed a few things, but hopefully, you’ll find something that helps you in this article. There should be a little bit for everyone, whatever your level of experience with web development is, and whatever browser you use.

So, without further ado, let’s jump right in.

**Note**: *Because Edge is based on Chromium, the open-source browser engine that also powers Chrome, all of the Chrome features listed below are also available in Edge (unless otherwise noted).*

## CSS Debugging

We’ve got a lot of long-awaited and profoundly impacting new features in CSS lately.

To name just a few: 

- [Container Queries](https://developer.mozilla.org/docs/Web/CSS/CSS_Container_Queries) help us style components based on the size of their containers,
- The [`:has()`](https://developer.mozilla.org/docs/Web/CSS/:has) pseudo-class lets us style elements based on what they contain, and 
- [CSS Cascade Layers](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/Cascade_layers) make it easy to gracefully handle increasing complexity in our websites’ code.

But, although these features are amazing, shipping support for them in browsers is only part of the story. For people to comfortably use them, documentation and tooling are necessary too.

We’re in luck because both Container Queries and CSS Cascade Layers have associated DevTools features now.

Specifically, Container Queries are supported in Safari WebInspector and Chrome DevTools where information about the corresponding `@container` at-rules is displayed when viewing CSS in the Styles sidebar.

Here is an example in Safari WebInspector:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca81b6e3-aa8f-4f9a-860b-6bcf0e4b6bff/safari-container-queries-code.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca81b6e3-aa8f-4f9a-860b-6bcf0e4b6bff/safari-container-queries-code.png" width="800" height="591" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca81b6e3-aa8f-4f9a-860b-6bcf0e4b6bff/safari-container-queries-code.png'>Large preview</a>)" alt="The Safari WebInspector Styles sidebar, showing multiple CSS rules, some preceded by @container rules" >}}

Chrome, Safari, and Firefox DevTools also now have support for CSS Cascade layers in their Elements (or Inspector) tools. The layer to which a particular rule belongs is now displayed next to that rule:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b86cbb-1cac-427b-b945-7ba736347165/18-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b86cbb-1cac-427b-b945-7ba736347165/18-devtools-updates-halloween-edition.png" width="800" height="549" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b86cbb-1cac-427b-b945-7ba736347165/18-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Chrome, with DevTools opened on the side, showing the Styles sidebar with CSS layers" >}}

Maybe a little less popular, but still very useful, the [`hwb()`](https://developer.mozilla.org/docs/Web/CSS/color_value/hwb) CSS function makes it possible to express colors in a more natural way based on hue and an amount of whiteness and blackness.

`hwb()` is now supported in all major browsers, and Chrome (and Chromium-based browsers), as well as Firefox, both have support for it in DevTools. That means they will show `hwb` in the autocomplete list when editing CSS in the Styles (or Rules) sidebar and will show the same color swatch used for other color formats too.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e194a91a-c8d5-419e-9cc4-eaae4f7cb0cf/16-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e194a91a-c8d5-419e-9cc4-eaae4f7cb0cf/16-devtools-updates-halloween-edition.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e194a91a-c8d5-419e-9cc4-eaae4f7cb0cf/16-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Rules sidebar in Firefox, showing a hwb function with a color swatch next to it" >}}

Next, it has also become easier to edit CSS in the Styles sidebar and get meaningful autocompletion results across browsers.

Chrome now previews all CSS variable values when autocompleting the `var()` function, not just colors, and it also displays `@supports` and `@scope` at-rules.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca9f2972-5960-4d95-a474-9856795ed882/1-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca9f2972-5960-4d95-a474-9856795ed882/1-devtools-updates-halloween-edition.png" width="800" height="549" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca9f2972-5960-4d95-a474-9856795ed882/1-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Chrome DevTools, showing the var() autocomplete, with previews for all variables" >}}

Safari now uses fuzzy matching when auto-completing CSS, making it much faster to type property names and values.

And Firefox added support for the [`color-mix()`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/color-mix) function in its auto-complete too.

Talking about Firefox, the browser has had the amazing **Inactive CSS** feature [since 2019](https://hacks.mozilla.org/2019/10/firefox-70-a-bountiful-release-for-all/#developertools), which lets you know when a particular CSS declaration doesn’t have an impact on the current element.

Firefox continued to improve this feature over time and recently added more coverage for use cases such as warning when `border-image-*` is used on elements within a table with `border-collapse` or warning when width or height are used on ruby elements.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82e91f9d-366a-4729-a300-d2960e864fb0/10-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82e91f9d-366a-4729-a300-d2960e864fb0/10-devtools-updates-halloween-edition.png" width="800" height="506" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82e91f9d-366a-4729-a300-d2960e864fb0/10-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Firefox, with a ruby annotation in the webpage, and DevTools showing an information tooltip about the inactive width CSS property on it" >}}

And, while we’re on the topic of inactive CSS, the Chrome team is actually working on a similar feature. In fact, it’s [already available in Chrome](https://devtoolstips.org/tips/en/find-inactive-styles/) (and all Chromium-based browsers) by enabling the **CSS authoring hints** experiment under `Settings (F1) > Experiments` in DevTools and should become available by default with Chrome 108.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f52f9b62-910a-4ea8-9a39-af09a1cbca53/11-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f52f9b62-910a-4ea8-9a39-af09a1cbca53/11-devtools-updates-halloween-edition.png" width="800" height="460" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f52f9b62-910a-4ea8-9a39-af09a1cbca53/11-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Chrome DevTools Styles pane with the authoring hints feature enabled, showing a tooltip with information about an inactive property" >}}

Over the past few years, browser DevTools has gotten fantastic layout debugging tools to inspect, understand, and tweak grid and flex layouts. More recently, Safari has been adding more features in this area as well.

You can now use CSS alignment controls in the *Styles* sidebar and inspect Flexbox layouts too.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b88dbca-94b7-4196-8757-a878928766f0/17-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b88dbca-94b7-4196-8757-a878928766f0/17-devtools-updates-halloween-edition.png" width="800" height="450" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b88dbca-94b7-4196-8757-a878928766f0/17-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Safari, with the WebInspector opened, showing a flex container selected in the Elements tool. The Layout sidebar shows options for inspecting the container. And the layout is highlighted on the page">}}

{{% feature-panel %}}

## JavaScript Debugging

Let’s change gears a bit and talk about JavaScript debugging.

It’s very common to use external libraries and frameworks in a JavaScript codebase, to avoid having to re-implement things that have already been solved. For some years already, DevTools have allowed users to ignore third-party scripts when debugging (see docs for [Chrome](https://developer.chrome.com/docs/devtools/javascript/reference/#ignore-list), [Edge](https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/javascript/guides/mark-content-scripts-library-code), [Firefox](https://firefox-source-docs.mozilla.org/devtools-user/debugger/how_to/ignore_a_source/index.html)).

Hiding scripts makes it easier to debug your code. It avoids ending up in foreign-looking library code when stepping through your own logic.

Recently, Firefox shipped a new feature that builds on top of this. You can now ignore **pieces of code within a file**. If you have a function that keeps getting called all the time but isn’t interesting for what you’re trying to debug, you can simply ignore that one function now.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c23f6d6c-d8a6-4e9a-8bab-ed1e4645f568/7-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c23f6d6c-d8a6-4e9a-8bab-ed1e4645f568/7-devtools-updates-halloween-edition.png" width="800" height="506" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c23f6d6c-d8a6-4e9a-8bab-ed1e4645f568/7-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Debugger tool in Firefox, with a few lines of code selected and the contextual menu displayed, showing the 'Ignore lines' option" >}}

Over in Chrome (and Chromium), a whole lot of small and not-so-small JavaScript debugging improvements were made:

The Page source tree was improved, and there’s now a way to group sources by authored (to show the original source files, thanks to source maps) or deployed (to show the actual files on the server).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b63e2fde-eb8a-4fa2-8479-86e89986bfab/20-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b63e2fde-eb8a-4fa2-8479-86e89986bfab/20-devtools-updates-halloween-edition.png" width="800" height="581" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b63e2fde-eb8a-4fa2-8479-86e89986bfab/20-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Page source tree, showing two top level nodes: authored and deployed" >}}

It is now also possible to live edit the code of a function while debugging. If you’re paused at a breakpoint inside a function and want to test a quick fix, you can edit the code right there and save the file. The function will be restarted with the new code.

Next, stack traces for asynchronous operations are now reported entirely, showing you the full story of what happened before your current breakpoint, even if those things happened asynchronously.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e7729cb-b97e-4e3c-bb11-dc6f34a0ab36/9-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e7729cb-b97e-4e3c-bb11-dc6f34a0ab36/9-devtools-updates-halloween-edition.png" width="800" height="460" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e7729cb-b97e-4e3c-bb11-dc6f34a0ab36/9-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Chrome DevTools Console, showing an async stack trace after a 404 error in the Console" >}}

Stack traces now also automatically ignore known third-party scripts, making it much easier to debug your own code.

## Performance Investigation

Web performance is probably an area where we depend on tools even more than in other areas. You can’t really guess what’s running slow or eating too much memory until you profile your webpage. Fortunately, we keep on getting new options to investigate performance and memory problems, making our lives easier.

In fact, Chrome shipped an entirely new panel dedicated just to this! 

**Note**: *This panel is available in Chrome only and not in other Chromium-based browsers.*

The [**Performance Insights**](https://developer.chrome.com/docs/devtools/performance-insights/) panel shipped with Chrome 102 and has gradually gotten better and better, with recent additions like **First Contentful Paint**, **Last Contentful Paint**, **Time To Interactive** metrics and **text flashes** identification.

Think of the Performance Insights panel as a simpler version of the (sometimes scary) Performance panel:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d89e536-f185-4599-bcac-ad3713ab1272/19-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d89e536-f185-4599-bcac-ad3713ab1272/19-devtools-updates-halloween-edition.png" width="800" height="435" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d89e536-f185-4599-bcac-ad3713ab1272/19-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The performance insights panel, in Chrome DevTools" >}}

Talking about the Performance panel, it recently got a brand new [**Interactions track**](https://developer.chrome.com/docs/devtools/evaluate-performance/reference/#interactions) in Chromium-based browsers, giving you a way to know when user events occur and how long they last, making it easier to debug responsiveness issues.

Edge has also been busy shipping new features in this area.

In the Performance tool, source maps can now be used to display original function names, even when sharing recorded profiles with other people:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c3bf36-d680-439e-ac60-758c19805a82/21-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c3bf36-d680-439e-ac60-758c19805a82/21-devtools-updates-halloween-edition.png" width="800" height="571" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c3bf36-d680-439e-ac60-758c19805a82/21-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Edge, showing a ski game in a tab, and the Performance tool next to it, with a link to an original typescript file highlighted" >}}

In the Memory tool, you now get a summary of your [heap snapshots](https://learn.microsoft.com/microsoft-edge/devtools-guide-chromium/memory-problems/heap-snapshots) organized by node types. Heap snapshots are hard to dig through, and these node types make it easier to see what is using the most memory on your webpage. There are also new ways to filter memory retainers to find memory leak culprits quickly.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8190cb-3509-496f-85cf-d96ae922f2e3/13-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8190cb-3509-496f-85cf-d96ae922f2e3/13-devtools-updates-halloween-edition.png" width="800" height="512" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8190cb-3509-496f-85cf-d96ae922f2e3/13-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Edge, with the Memory tool showing a heap snapshot and a bunch of node types highlighted" >}}

Finally, Firefox has also been active in this area over the past few months. A number of years ago, Firefox created a brand new [Performance tool](https://profiler.firefox.com/) for its own use. The idea, at the time, was to have a tool to debug performance problems in the browser code itself. But over time, the tool was adapted to become useful to web developers too.

And now, the final changes have been made, and the old Firefox DevTools’ Performance panel has fully been replaced with the new one:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc943ba-91c4-4679-851a-5f82088bb850/8-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc943ba-91c4-4679-851a-5f82088bb850/8-devtools-updates-halloween-edition.png" width="800" height="561" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc943ba-91c4-4679-851a-5f82088bb850/8-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The new Firefox Performance panel" >}}

{{% ad-panel-leaderboard %}}

## Network Debugging

Debugging your frontend code is important, but sometimes problems can happen in the network layer of your app when communicating with your server. Thankfully, a few very useful features were recently added to the Network tools in various browsers.

In Edge, a new column was added to the Network log. The **Fulfilled by** column makes it easier to debug your service worker logic and Progressive Web Apps.

You can now discover straight away whether a request was handled by the service worker, the browser cache, or your server.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd080aaa-77f2-4442-82de-88fa5318e33e/15-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd080aaa-77f2-4442-82de-88fa5318e33e/15-devtools-updates-halloween-edition.png" width="800" height="512" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd080aaa-77f2-4442-82de-88fa5318e33e/15-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Network tool in Edge, showing the new Fulfilled by column" >}}

Firefox just shipped a completely redesigned version of its **Edit and Resend** feature. This feature has been available in Firefox for a long time already and is a great way to debug your server-side APIs or just test something quickly.

With it, you can right-click on any HTTP request displayed in the Network tool, select `Edit and Resend`, then manipulate the request parameters, headers, and body, and finally send the modified request.

Firefox completely redesigned it recently. It’s now much easier to edit the parameters before sending a new request.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acc5b5a0-8f29-47ec-bcf7-b13344fb2ebb/24-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acc5b5a0-8f29-47ec-bcf7-b13344fb2ebb/24-devtools-updates-halloween-edition.png" width="800" height="521" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acc5b5a0-8f29-47ec-bcf7-b13344fb2ebb/24-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Network tool in Firefox, showing the Edit and Resend sidebar" >}}

And finally, Safari has added quite a few great features in this area too. You can now block network requests entirely, and you can also locally override requests by using regular expressions.

## Editor Integration

Microsoft also does VSCode, which is a very popular code editor amongst web developers, and some time ago, the Edge team released [the Edge Tools extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-edgedevtools.vscode-edge-devtools). The extension gives you an embedded browser and the browser DevTools right in VS Code alongside your code.

This year, the team continued to work on the extension and added more features. In particular, the following things are now possible:

- The extension now has the **Console** and **Application** tools available. Previously, only the **Elements** and **Network** tools were available. Console logs used to go to VSCode’s output, but now they also go to the Console tool in the embedded DevTools.
- The embedded browser has been completely redesigned and features a lot of emulation and rendering options to test your webpage under different conditions. For example, you can emulate different media types or the prefers-code-scheme media feature. You can also emulate different color vision deficiencies.
- Next, you can launch the embedded browser and DevTools simply by right-clicking an HTML file in VS Code.
- Finally, you can use VS Code’s **Quick Fix** options to automatically fix a number of issues reported by the extension in your code.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fe7485c-9493-486a-90b2-807ca647dd69/4-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fe7485c-9493-486a-90b2-807ca647dd69/4-devtools-updates-halloween-edition.png" width="800" height="492" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fe7485c-9493-486a-90b2-807ca647dd69/4-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="VSCode, with the Edge Tools extension installed, showing the Elements tool and the embedded browser, in VSCode" >}}

One more thing, if you like using Visual Studio (not VS Code), note that the team released an extension for it too. Check out the [Edge Developer Tools for Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-edgedevtools.VisualStudioEdgeDevTools) extension.

## Test Automation

It’s possible to automate browsers nowadays, and it can be very useful for testing. With browser automation libraries such as [WebDriver](https://webdriver.io/), [Puppeteer](https://pptr.dev/), and [Playwright](https://playwright.dev/), you can write tests that mimic what users would do on your website and verify that these scenarios continue working over time, as you make changes to your product.

This area is in constant evolution; in particular, the WebDriver spec is evolving with a new [bi-directional](https://w3c.github.io/webdriver-bidi/) version. Also, the Chrome DevTools team has been innovating quite a lot lately. They shipped a new tool called the [**Recorder**](https://developer.chrome.com/docs/devtools/recorder/) last year and have been improving it over time.

Here are some of the new features that got added to the panel in recent months:

- It’s now possible to wait until elements are visible and clickable before continuing a recording.
- Element selectors are better supported.
- You can import and export recorded flows as JSON.
- Double-click, mouse over, and right-click events can be recorded too.
- There’s also an option to replay a recording slowly or step-by-step.
- And, finally, the Recorder tool now supports extensions to export recordings to a variety of test automation formats, such as **Cypress**, **WebPageTest**, **Nightwatch**, or **WebdriverIO**.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71088936-4fcc-426f-a0b4-ed378b28d09f/23-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71088936-4fcc-426f-a0b4-ed378b28d09f/23-devtools-updates-halloween-edition.png" width="800" height="647" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71088936-4fcc-426f-a0b4-ed378b28d09f/23-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Recorder panel in Chrome DevTools, showing a recorded flow with multiple steps" >}}

{{% ad-panel-leaderboard %}}

## Miscellaneous Updates

Phew, that was a lot! But we’re not done. Let’s wrap this up with a list of somewhat random but very useful features.

Chrome made a lot of source maps and stack traces improvements, providing a more stable and easier-to-use debugging experience. If you usually debug your JavaScript code with logs, now may be a good time to give [breakpoint debugging](https://developer.chrome.com/docs/devtools/javascript/) a try and see if it speeds things up for you.

Talking about logging, they also made it possible to properly style logs with [ANSI escape codes](https://en.wikipedia.org/wiki/ANSI_escape_code).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fac6de0-f25a-4c87-98b8-dcb301fa1ee5/3-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fac6de0-f25a-4c87-98b8-dcb301fa1ee5/3-devtools-updates-halloween-edition.png" width="800" height="504" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fac6de0-f25a-4c87-98b8-dcb301fa1ee5/3-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Console tool in Chrome DevTools, showing a lot of colorful console logs" >}}

Next, you can now pick colors from anywhere on your screen when changing colors in the Styles sidebar. 

**Note**: *This was made possible thanks to the [EyeDropper API](https://developer.mozilla.org/en-US/docs/Web/API/EyeDropper_API), which you can also use on your web pages.*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/050f11ca-ae01-4e11-b464-f521a06efdd4/12-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/050f11ca-ae01-4e11-b464-f521a06efdd4/12-devtools-updates-halloween-edition.png" width="800" height="480" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/050f11ca-ae01-4e11-b464-f521a06efdd4/12-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The color picker in Edge DevTools, showing that the eyedropper tool was selected, and that it is possible to sample a color from outside of the browser, including in other app windows" >}}

Edge shipped a feature to publish and retrieve production source maps from Azure, making it much easier to securely debug your code in production even when you don’t want to publish source maps and original source code to your server.

Read more about [publishing your source maps](https://learn.microsoft.com/en-gb/microsoft-edge/devtools-guide-chromium/javascript/publish-source-maps-to-azure) and [consuming them from DevTools](https://learn.microsoft.com/en-gb/microsoft-edge/devtools-guide-chromium/javascript/consume-source-maps-from-azure).

The team also opened a [new public feedback repository on GitHub](https://github.com/MicrosoftEdge/DevTools) which you can use to report ideas, issues, and features or just discuss them.

Finally, they shipped a redesigned **Welcome** tool where you can find all sorts of useful videos and links to documentation.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e857c21c-ab2e-4c29-a7b5-91f8733a8b48/6-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e857c21c-ab2e-4c29-a7b5-91f8733a8b48/6-devtools-updates-halloween-edition.png" width="800" height="468" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e857c21c-ab2e-4c29-a7b5-91f8733a8b48/6-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="The Welcome tool in Edge DevTools, showing a bunch of different documentation and update links" >}}

Switching to Firefox, the DevTools team continued to keep their **Compatibility** panel up to date with new [browser compatibility data](https://github.com/mdn/browser-compat-data), so you can get relevant cross-browser support issues right when debugging your CSS.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb686ebd-a76b-4943-b4b1-22694531771b/5-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb686ebd-a76b-4943-b4b1-22694531771b/5-devtools-updates-halloween-edition.png" width="800" height="592" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb686ebd-a76b-4943-b4b1-22694531771b/5-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Firefox, with DevTools open, showing the Compatibility panel filled with issues about cross-browser support" >}}

The team also made it possible to disable and re-enable any event listener for a given element in the Inspector.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879b4dbb-ead9-4f62-8315-176e9e437762/14-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879b4dbb-ead9-4f62-8315-176e9e437762/14-devtools-updates-halloween-edition.png" width="800" height="551" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879b4dbb-ead9-4f62-8315-176e9e437762/14-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Firefox, showing the Inspector tool, and the event listener tooltip displayed on an HTML element. The tooltip now has checkboxes to toggle event listeners">}}

Finally, Edge just shipped a cool new experimental feature that enables one to type commands and access common browser and DevTools features from one keyboard shortcut.

[The Command palette experiment](https://learn.microsoft.com/en-gb/microsoft-edge/devtools-guide-chromium/experimental-features/edge-command-palette) lets you enter commands in the browser by pressing <kbd>Ctrl</kbd>+<kbd>Q</kbd> (note that prior to Edge 108, the shortcut was <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Space</kbd>).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14592039-7182-4ea9-9a35-4193c740b696/2-devtools-updates-halloween-edition.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14592039-7182-4ea9-9a35-4193c740b696/2-devtools-updates-halloween-edition.png" width="800" height="425" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14592039-7182-4ea9-9a35-4193c740b696/2-devtools-updates-halloween-edition.png'>Large preview</a>)" alt="Edge, with the command palette opened, showing a few devtools commands" >}}

And that’s it for today. I hope you found a few things that will be useful for your web development projects.

DevTools has gotten impressively full of features over the years, and it’s [hard to keep track](https://www.smashingmagazine.com/2022/05/whats-that-dev-tool/), but here are a few pointers that I hope will make it easier to discover new features:

- The [Chrome DevTools What’s New](https://www.youtube.com/playlist?list=PLNYkxOF6rcIBDSojZWBv4QJNoT4GNYzQD) video playlist on YouTube.
- The [Edge DevTools What’s New](https://www.youtube.com/watch?v=LJxjFo4DuA0&list=PL4z1-7pjJU6wCla3QZuWuWjsCB2hCnTvr) video playlist on YouTube.
- The [@FirefoxDevTools](https://twitter.com/firefoxdevtools) Twitter, where new features are often announced.
- The [WebInspector category](https://webkit.org/blog/category/web-inspector/) on the WebKit blog.

And with this, thanks for reading, and if you have great DevTools tips you want to share with everyone, please drop us a comment!

{{< signature "yk" >}}