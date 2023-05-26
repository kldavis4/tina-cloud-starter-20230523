---
title: 'What’s New In DevTools?'
slug: devtools-updates-2022
author: patrickbrosset
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e516aa85-3b77-418a-9b43-cec06943b129/devtools-updates-2022.jpg
date: 2022-01-25T13:00:00.000Z
summary: >-
  What’s new in Chrome, Edge, Safari and Firefox? Patrick Brosset breaks it down with the latest features in DevTools across browsers.
description: >-
  What’s new in Chrome, Edge, Safari and Firefox? Patrick Brosset breaks it down with the latest features in DevTools across browsers.
categories:
  - Tools
  - Browsers
  - Debugging
  - DevTools
  - Testing
last_updated: 2022-01-26T08:00:00.000Z
updated_by: patrickbrosset
---

In September last year, [I wrote about some of the latest updates](https://www.smashingmagazine.com/2021/09/devtools-cross-browser-edition/) in our beloved DevTools, across Firefox, Chrome, Safari, and Edge. Four months have already passed since then, and the different teams working on DevTools have been busy! In these four months, they built a lot of new things for us to use. From powerful **productivity improvements** to entire new panels, they’ve been continuing to close the parity gap and innovate with new means of debugging and improving our web experiences.

That means it’s high time for another DevTools update, so let’s jump right in!

- [Chrome](#chrome)
- [Edge](#edge)
- [Safari](#safari)
- [Firefox](#firefox)

## Chrome

The Chrome team just released a new panel that makes it very straightforward to record and replay user flows: the Recorder panel.

### Record, Replay And Measure User Flows

If you’ve ever found yourself having to repeat the same navigation steps over and over again in a web app in order to investigate a bug, then this might change your life!

{{< vimeo id="668570851" caption="Devtools recorder panel" breakout="true" >}}

But there’s more! Once the steps are recorded, you can replay them while measuring performance. This way, you can work on optimizing your code, while being sure to always run the same scenario every time you test.

You can [learn more about the Recorder here](https://developer.chrome.com/docs/devtools/recorder/). And if you have feedback about this tool, the team will be very happy to hear your thoughts on this [chromium issue](https://bugs.chromium.org/p/chromium/issues/detail?id=1257499).

### Navigate The Accessibility Tree

Rendering pages to the screen isn’t the only thing that browsers do. They also use the DOM tree they build in the process to create another tree: the [accessibility tree](https://developer.mozilla.org/en-US/docs/Glossary/Accessibility_tree). The accessibility tree is another representation of the current page that can be used by assistive technologies, like screen readers.

As a web developer, it is very useful to have access to this accessibility tree. It helps understand how the markup you choose influences the way screen readers interpret the page.

Chrome DevTools has had an Accessibility panel for some time in the sidebar of the Elements panel which contains the accessibility tree. Recently though, the team has been experimenting with displaying both the accessibility and the DOM tree in the same place, allowing developers to go back and forth between the two.

To enable this experiment, go to the Accessibility sidebar panel, and check the “Enable full-page accessibility tree”. You will then have a new button displayed in the top-right corner of the DOM tree that lets you switch between the DOM and accessibility trees.

[Find out more here](https://developer.chrome.com/blog/full-accessibility-tree/), and let the team know your [feedback](https://bugs.chromium.org/p/chromium/issues/detail?id=1275891).

{{< vimeo id="668572520" breakout="true" >}}

### CSS Overview Is Now On By Default

The [CSS overview](https://developer.chrome.com/docs/devtools/css-overview/) panel isn’t new, but with so many panels to choose from, you might have never used it. It has been an experiment for a very long time, which means you needed to go into DevTools settings to enable it before being able to use it.

This is no longer necessary. The CSS Overview panel is just a regular feature now, and you can open it by going into `… > More tools > CSS Overview`.

If you’ve never used it, give it a try as it is a very useful tool to identify potential CSS improvements like contrast issues or unused CSS declarations.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28d81ed-26b2-485c-bb08-e342137c2ebf/css-overview-panel.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28d81ed-26b2-485c-bb08-e342137c2ebf/css-overview-panel.png" width="800" height="575" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28d81ed-26b2-485c-bb08-e342137c2ebf/css-overview-panel.png'>Large preview</a>)" alt="CSS overview panel." >}}

While you’re in the `More tools` menu, take a look around. Chrome DevTools has more than 30 individual panels! That’s a lot, but keep in mind they’re all here for a specific reason. There might be aspects of your web app that certain panels could help you with. Be curious, and if you have no idea what a thing does, remember there are [docs you can read](https://devtoolstips.org/tips/en/find-devtools-documentation/).

{{% feature-panel %}}

## Edge

While Microsoft’s browser team continues to be an active contributor to the Chromium project, they’re also spending more time on new and unique features that only Edge has. Let’s review two of them here.

### Debug DOM Memory Leaks With The Detached Elements Panel

Edge just launched a memory leak investigation tool, the Detached Elements tools, which can be very useful to investigate leaks in long-running apps.

One of the multiple reasons why web pages leak memory is detached DOM elements: elements that might have been needed at some point, but got removed from the DOM, and never re-attached. When a code base grows in complexity, it’s easier to make mistakes and forget to clean those detached elements up.

If you find that your app keeps on needing more and more memory over time as you use it, give the Detached Elements a try. It can very quickly point you in the right direction.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fe2865e-fa10-4487-8b19-00113264091f/detached-elements.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fe2865e-fa10-4487-8b19-00113264091f/detached-elements.png" width="800" height="520" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fe2865e-fa10-4487-8b19-00113264091f/detached-elements.png'>Large preview</a>)" alt="Detached elements." >}}

Learn more about it on the [announcement blog post](https://blogs.windows.com/msedgedev/2021/12/09/debug-memory-leaks-detached-elements-tool-devtools/), and the [docs](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/memory-problems/dom-leaks).

### A Brand New User Interface For DevTools With Focus Mode

Our DevTools have looked the way they do ever since the early [Firebug](https://getfirebug.com/) days. Sure, the user interface has evolved over time a little bit, with more tools added, and things re-arranged, but at a high level, it’s still mostly the same.

The Edge team has conducted experiments and user studies that indicate that DevTools can be very overwhelming (did I say DevTools had more than 30 panels already?). While new web developers don’t have a clear idea of where to start and how to explore and use the tools, more experienced developers tend to find themselves in just one or two familiar workflows.

Based on this, the Edge team released a new experimental feature that makes it easier to learn and use DevTools: `Focus Mode`.

{{< vimeo id="668576149" breakout="true" >}}

`Focus Mode` has a new activity bar, an easy way to add and remove tools, a quick view drawer, and re-designed menus.

To give `Focus Mode` a try, enable it first by going to `Settings > Experiments > Focus Mode`.

You can learn more about `Focus Mode` in this [Edge explainer document](https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/DevTools/FocusMode/explainer.md).

{{% ad-panel-leaderboard %}}

## Safari

While Safari itself updates roughly twice a year (with a major version in the fall with new features and another one in spring), it’s possible to get more frequent updates and access to early features by using the [Safari Technology Preview channel](https://developer.apple.com/safari/technology-preview/). This version of the browser updates itself approximately every 2 to 3 weeks.

You might not want to use the Technology Preview channel for all of your testing since your customers will likely only have the regular Safari version installed, but it’s still a very interesting browser to use from time to time. By doing so, you’ll have access to new features earlier, and check what’s coming to Safari soon.

Here are some of the latest updates to the Safari Web Inspector available in the Technology Preview channel that make working with CSS much better.

### Fuzzy Auto-Completion For CSS In The Styles Panel

Changing CSS is one of the things we do most in DevTools, and Safari just made it a lot faster for us all.

Now, their auto-completion for CSS supports fuzzy matching, which means you can type things like “pat” to match padding-top, or “bob” to match border-bottom.

If you use VS Code or another text editor that supports fuzzy auto-completion, you will feel right at home.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a771bfc-812e-4d83-a9f5-8a4fae5651ac/fuzzy-autocomplete.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a771bfc-812e-4d83-a9f5-8a4fae5651ac/fuzzy-autocomplete.png" width="662" height="322" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a771bfc-812e-4d83-a9f5-8a4fae5651ac/fuzzy-autocomplete.png'>Large preview</a>)" alt="Fuzzy autocomplete" >}}

### Grouping Of CSS Variables By Types In The Computed Panel

CSS variables (aka [Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)) have now been supported on all major browsers for years, and site owners, design systems, and libraries have really started to make extensive use of them. For good reasons, they’re great!

But with this increase in usage, the `Styles` and `Computed` panes of our DevTools are starting to feel a little crowded.

Safari released a feature that helps a little bit with this. The `Computed` pane now lists all CSS variables neatly tucked inside a collapsible section and grouped by value types too. As an example, all color variables are grouped together.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a953d45-84b4-4871-a46e-5f2795e0a937/computed-css-variables.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a953d45-84b4-4871-a46e-5f2795e0a937/computed-css-variables.png" width="800" height="533" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a953d45-84b4-4871-a46e-5f2795e0a937/computed-css-variables.png'>Large preview</a>)" alt="Computed CSS variables" >}}

### Visually Align And Justify Flex Lines And Grid Tracks

Not long ago, Chrome and Edge got really nice [alignment editors](https://devtoolstips.org/tips/en/tweak-grid-flex-alignment/) for flexbox and grid layouts in their `Styles` panel. They make working with complex alignment properties such as `justify-content` or `align-items` more visual, and therefore a lot easier to understand.

Safari now has a similar visual editor for `align-content/items/self` and `justify-content/items/self` CSS properties. It’s very simple to use, just click on the icon next to an alignment value in the Styles panel to open the editor. You can then choose the type of alignment for your flex lines and grid tracks.

{{< vimeo id="668591801" breakout="true" >}}

{{% ad-panel-leaderboard %}}

## Firefox

The Firefox DevTools team had been on a journey to re-architecture the DevTools code base for some time and, while this had resulted in fewer features being shipped during that period, that project is now complete. That means the team is back with a lot of really cool improvements.

### Choose Your Execution Context

Sometimes you need to deal with multiple contexts on your site, whether those are from multiple iframes or web workers. Because the browser runs these things in multiple different processes, it's not always possible to access them easily from DevTools.

To help with this situation, Firefox just added a context selector in the Console which you can use to choose where the code you type gets executed. For example, if you want to know the value of some global variable in an iframe, you can use the selector to switch to the iframe.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d5daf8-fd2b-44ad-997f-395550f53f57/context-selector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d5daf8-fd2b-44ad-997f-395550f53f57/context-selector.png" width="800" height="556" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d5daf8-fd2b-44ad-997f-395550f53f57/context-selector.png'>Large preview</a>)" alt="Context selector" >}}

### Support For `hwb()` Function In Inspector

The [`hwb()`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hwb()) CSS color function is part of the [CSS Color Module 4 specification](https://www.w3.org/TR/css-color-4/#the-hwb-notation) and is a very intuitive method for specifying colors. HWB colors use 3 values: the first one is the hue, which is the starting point for the color. The second and third values are the amount of white and the amount of black that should be mixed in to create the final color.

The `hwb` function is currently supported on Safari and Firefox, and the Firefox DevTools team just released support for it in the Inspector. Now the `hwb` function is recognized correctly, and as an added bonus incrementing and decrementing the `W` and `B` values with the keyboard automatically keeps them between `0%` and `100%`.

{{< vimeo id="669366353" breakout="true" >}}

### Select Unselectable Elements

Interestingly, selecting elements from DevTools is subject to the pointer-events CSS property. That is, if an element is specified not to receive any pointer events (with `pointer-events:none`), then you won’t be able to select it using the element picker in DevTools, because it requires mouse interaction.

Well, in Chrome and Edge, there is a [special trick](https://devtoolstips.org/tips/en/select-pointer-events-none-elements/) you can do that few people know about. If you hold the `Shift` key while using the element picker, then even `pointer-events:none` elements become selectable.

The good news is that Firefox just implemented the same feature as well. The parity of features across different DevTools is always great news for users because it makes testing and debugging websites on multiple browsers a lot easier.

{{< vimeo id="669367546" breakout="true" >}}

While we’re on the topic of parity, it’s worth also mentioning that Firefox just shipped a way to disable individual event listeners too. 

In the Inspector panel, you can list event listeners attached to elements by clicking the `[env]` badges next to them. Now, the list of event listeners also contains checkboxes to toggle listeners.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8309203-ea52-49a7-a26a-7855a444182d/disable-events.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8309203-ea52-49a7-a26a-7855a444182d/disable-events.png" width="800" height="314" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8309203-ea52-49a7-a26a-7855a444182d/disable-events.png'>Large preview</a>)" alt="Disable events" >}}

### Ignore Single Lines Of Code In The Debugger

If you spend time debugging JavaScript in DevTools on a large code base that uses frameworks and libraries, you might already be familiar with how to [ignore source files](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Ignore_a_source). This feature lets you mark entire files as ignored so the debugger does pause within them.

This means you can mark a framework bundle file as ignored for example, and happily debug your own code without fear of stepping into the framework code.

While other browsers also support this feature too, Firefox is innovating with a really cool evolution of it: the ability to ignore ranges of lines within a file! Imagine, you have a utility function in a file that gets called all the time. It might be useful to mark just this function as ignored, and still be able to debug everything else in that file as normal. It may also come useful when using a bundler that groups all of your source code and libraries in the same file.

This feature is, at the time of writing, still experimental. You will need to set the `devtools.debugger.features.blackbox-lines` boolean to true on the `about:config` page first.

Once enabled, you can right-click on any line of your source code and choose `Ignore line`.

{{< vimeo id="669370107" breakout="true" >}}

## That’s It For Now!

I hope you enjoyed these updates, and that they’ll turn out useful when doing web development. As always, if you have feedback, bugs to report, or new feature ideas for DevTools, [make yourself heard](https://devtoolstips.org/tips/en/send-feedback-about-devtools/)! It’s impressive to see how far the web platform debugging capabilities have come, and we all can help make it even better!

{{< signature "vf, yk, il" >}}
