---
title: 'What’s New With DevTools: Cross-Browser Edition'
slug: devtools-cross-browser-edition
author: patrickbrosset
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e0eef0e-e4b0-45b6-8afd-1d1a60b7c53b/devtools-cross-browsers.jpg
date: 2021-09-07T10:00:00.000Z
summary: >-
  Learn what’s new with developer tools in Firefox, Edge, Chrome and Safari. Discover new and powerful features that will help you be more comfortable and productive when testing and debugging across browsers.
description: >-
  Learn what’s new with developer tools in Firefox, Edge, Chrome and Safari. Discover new and powerful features that will help you be more comfortable and productive when testing and debugging across browsers.
categories:
  - Tools
  - Browsers
  - Debugging
  - Testing
  - DevTools
---

Browser developer tools keep evolving, with new and improved features added all the time. It’s hard to keep track, especially when using more than one browser. With that much on offer, it is not surprising that we feel overwhelmed and use the features we already know instead of keeping up with what’s new. 

It’s a shame though, as some of them can make us much more productive.

So, my goal with this article is to raise awareness on some of the newest features in Chrome, Microsoft Edge, Firefox and Safari. Hopefully, it will make you want to try them out, and maybe will help you get more comfortable next time you need to debug a browser-specific issue.

With that said, let’s jump right in.

## Chrome DevTools

The Chrome DevTools team has been hard at work modernizing their (now 13 years old) codebase. They have been busy improving the build system, migrating to TypeScript, introducing new WebComponents, re-building their theme infrastructure, and way more. As a result, the tools are now easier to extend and change.

But on top of this less user-facing work, the team did ship a lot of features too. Let me go over a few of them here, related to CSS debugging.

### Scroll-snapping

CSS scroll-snapping offers web developers a way to control the position at which a scrollable container stops scrolling. It’s a useful feature for, e.g., long lists of photos where you want the browser to position each photo neatly within its scrollable container automatically for you.

If you want to learn more about scroll-snapping, you can read [this MDN documentation](https://css-at-cds.netlify.app/), and take a look at [Adam Argyle's demos here](https://css-at-cds.netlify.app/).

The key properties of scroll-snapping are:

- `scroll-snap-type`, which tells the browser the direction in which snapping happens, and how it happens;
- `scroll-snap-align`, which tells the browser where to snap.

Chrome DevTools introduced new features that help debug these key properties:

- if an element defines scroll-snapping by using `scroll-snap-type`, the Elements panel shows a badge next to it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44dd651-bef8-4831-9748-db99cbec6b05/01-chrome-scroll-snap-badge.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44dd651-bef8-4831-9748-db99cbec6b05/01-chrome-scroll-snap-badge.png" width="800" height="643" sizes="100vw" caption="The scroll-snap badge is useful to quickly find elements that define scroll snapping. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44dd651-bef8-4831-9748-db99cbec6b05/01-chrome-scroll-snap-badge.png'>Large preview</a>)" alt="Screenshot of Chrome DevTools' Elements panel showing a scroll-snap badge in the DOM tree" >}}

- You can click on the scroll-snap badge to enable a new overlay. When you do, several things are highlighted on the page:
  - the scroll container,
  - the items that scroll within the container,
  - the position where items are aligned (marked by a blue dot).

This overlay makes it easy to understand if and how things snap into place after scrolling around. This can be very useful when, e.g., your items don’t have a background and boundaries between them are hard to see.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad3f4ec-b07c-4550-914f-13f877ca60bb/02-chrome-scroll-snap-overlay.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad3f4ec-b07c-4550-914f-13f877ca60bb/02-chrome-scroll-snap-overlay.PNG" width="800" height="" sizes="100vw" caption="Highlight the items that are part of the scroll snapping container. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad3f4ec-b07c-4550-914f-13f877ca60bb/02-chrome-scroll-snap-overlay.PNG'>Large preview</a>)" alt="Screenshot of Chrome DevTools' Elements panel showing a scroll-snap badge has been enabled and an overlay appears in the page" >}}

While scroll snapping isn’t a new CSS feature, adoption is rather low ([less than 4% according to chromestatus.com](https://www.chromestatus.com/metrics/css/popularity)), and since the specification changed, not every browser supports it the same way.

I hope that this DevTools feature will make people want to play more with it and ultimately adopt it for their sites.

{{% feature-panel %}}

### Container queries

If you have done any kind of web development in recent years, you have probably heard of [container queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries). It’s been one of the most requested CSS features for the longest time and has been a very complex problem for browser makers and spec writers to solve.

If you don’t know what container queries are, I would suggest going through Stephanie Eckles’ [Primer On CSS Container Queries article](https://www.smashingmagazine.com/2021/05/complete-guide-css-container-queries/) first.

In a few words, they’re a way for developers to define the layout and style of elements depending on their container’s size. This ability is a huge advantage when creating reusable components since we can make them adapt to the place they are used in (rather than only adapt to the viewport size which media queries are good for).

Fortunately, things are moving in this space and Chromium now supports container queries and the Chrome DevTools team has started adding tooling that makes it easier to get started with them.

Container queries are not enabled by default in Chromium yet (to enable them, go to [chrome://flags](chrome://flags/) and search for “container queries”), and it may still take a little while for them to be. Furthermore, the DevTools work to debug them is still in its early days. But some early features have already landed.

- When selecting an element in DevTools that has styles coming from a `@container` at-rule, then this rule appears in the Styles sidebar of the Elements panel. This is similar to how media queries styles are presented in DevTools and will make it straightforward to know where a certain style is coming from.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093d70ea-4043-47e0-a0ba-9a0060f44ec1/03-chrome-container-query-1.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093d70ea-4043-47e0-a0ba-9a0060f44ec1/03-chrome-container-query-1.PNG" width="800" height="" sizes="100vw" caption="Easily see when a CSS rule is applied when a container query matched in the Styles pane. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093d70ea-4043-47e0-a0ba-9a0060f44ec1/03-chrome-container-query-1.PNG'>Large preview</a>)" alt="Screenshot of Chrome DevTools' Styles pane showing a CSS rule nested in a @container rule" >}}

As the above screenshot shows, the Styles sidebar displays 2 rules that apply to the current element. The bottom one applies to the `.media` element at all times and provides its default style. And the top one is nested in a `@container (max-width:300px)` container query that only takes effect when the container is narrower than 300px.

- On top of this, just above the `@container` at-rule, the Styles pane displays a link to the element that the rule resolves to, and hovering over it displays extra information about its size. This way you know exactly why the container query matched.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/727f3310-2f55-46af-a999-dba5f970cc93/04-chrome-container-query-2.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/727f3310-2f55-46af-a999-dba5f970cc93/04-chrome-container-query-2.gif" width="827" height="599" alt="Gif animation of the Chrome DevTools' Styles pane showing how hovering over the @container a CSS rule nested in a @container rule" /></a><figcaption>Hover over the container query to know why and where it matched.</figcaption></figure>

The Chrome DevTools team is actively working on this feature and you can expect much more in the future.

## Chromium Collaboration

Before going into features that other browsers have, let’s talk about Chromium for a little bit. [Chromium](https://www.chromium.org/Home) is an open-source project that Chrome, Edge, Brave, and other browsers are built upon. It means all these browsers have access to the features of Chromium.

Two of the most active contributors to this project are Google and Microsoft and, when it comes to DevTools, they collaborated on a few interesting features that I’d like to go over now.

### CSS Layout Debugging Tools

A few years ago, Firefox innovated in this space and shipped the first-ever [grid](https://hacks.mozilla.org/2016/12/css-grid-and-grid-highlighter-now-in-firefox-developer-edition/) and [flexbox](https://hacks.mozilla.org/2019/01/designing-the-flexbox-inspector/) inspectors. Chromium-based browsers now also make it possible for web developers to debug grid and flexbox easily.

This collaborative project involved engineers, product managers and designers from Microsoft and Google, working towards a shared goal (learn more about the project itself in [my BlinkOn talk](https://www.youtube.com/watch?v=D5x1Fa-Atew)).

Among other things, DevTools now has the following layout debugging features:

- Highlight multiple grid and flex layouts on the page, and customize if you want to see grid line names or numbers, grid areas, and so on.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c900609-373f-4e93-9ace-ad0919839e10/05-chromium-grid-flex-overlays.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c900609-373f-4e93-9ace-ad0919839e10/05-chromium-grid-flex-overlays.png" width="800" height="456" sizes="100vw" caption="Highlight grid lines and flex items. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c900609-373f-4e93-9ace-ad0919839e10/05-chromium-grid-flex-overlays.png'>Large preview</a>)" alt="Screenshot of Edge DevTools with a flex and a grid container being highlighted in the page" >}}

- Flex and grid editors to visually play around with the various properties.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4d21568-9181-4fda-ad2c-8da50d09fe60/06-chromium-flex-editor.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e6c1744-7816-4d4f-a5fd-17683a57c55a/06-chromium-flex-editor-800w.gif" width="800" height="433" alt="Gif animation of the flex editor in Edge DevTools showing the user cycling through various justify-content values" /></a><figcaption>Play with the various flex alignment properties visually. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4d21568-9181-4fda-ad2c-8da50d09fe60/06-chromium-flex-editor.gif">Large preview</a>)</figcaption></figure>

- Alignment icons in the CSS autocomplete make it easier to choose properties and values.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd326f02-c541-4167-ad29-9b15714a471b/07-chromium-autocomplete-icons.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd326f02-c541-4167-ad29-9b15714a471b/07-chromium-autocomplete-icons.png" width="800" height="456" sizes="100vw" caption="Easily see how a given CSS property value will impact the layout with the new icons. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd326f02-c541-4167-ad29-9b15714a471b/07-chromium-autocomplete-icons.png'>Large preview</a>)" alt="Screenshot of Edge DevTools showing the CSS autocomplete in the Styles pane with icons in front of most property values to help choose" >}}

- Highlight on property hover to understand what parts of the page a property applies to.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0184069-cdd5-4aa4-bfbf-41333b75e658/08-chromium-gap-highlight.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60a22110-bf36-4103-a30c-7665075b0706/08-chromium-gap-highlight-800w.gif" width="800" height="377" alt="Gif animation of the Styles pane in Edge DevTools showing that hovering over column-gap highlights just the area of the page impacted by this property" /></a><figcaption>Highlight various CSS properties independently to understand how they affect the layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0184069-cdd5-4aa4-bfbf-41333b75e658/08-chromium-gap-highlight.gif">Large preview</a>)</figcaption></figure>

You can read more information about this on [Microsoft’s and Google’s](https://developer.chrome.com/docs/devtools/css/grid/) documentation sites.

### Localization

This was another collaborative project involving Microsoft and Google which, now, makes it possible for all Chromium-based DevTools to be translated in languages other than English.

Originally, there was never a plan to localize DevTools, which means that this was a huge effort. It involved going over the entire codebase and making UI strings localizable.

The result was worth it though. If English isn’t your first language and you’d feel more comfortable using DevTools in a different one, head over to the Settings (`F1`) and find the language drop-down.

Here is a screenshot of what it looks like in Chrome DevTools:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e82da6c-e5bd-4323-ba65-0d098f7a5f4f/09-chromium-chrome-languages.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e82da6c-e5bd-4323-ba65-0d098f7a5f4f/09-chromium-chrome-languages.png" width="800" height="578" sizes="100vw" caption="Changing the language in Chrome DevTools’ settings panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e82da6c-e5bd-4323-ba65-0d098f7a5f4f/09-chromium-chrome-languages.png'>Large preview</a>)" alt="Screenshot of the settings panel in chrome devtools showing the language drop-down" >}}
  
And here is how Edge looks in Japanese:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267b1376-4e5b-4d9f-9f6d-92113cf9992a/10-chromium-edge-japanese.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267b1376-4e5b-4d9f-9f6d-92113cf9992a/10-chromium-edge-japanese.png" width="800" height="582" sizes="100vw" caption="What the DevTools UI looks like when localized in Japanese. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267b1376-4e5b-4d9f-9f6d-92113cf9992a/10-chromium-edge-japanese.png'>Large preview</a>)" alt="Screenshot of the Edge DevTools UI in Japanese" >}}

{{% ad-panel-leaderboard %}} 

## Edge DevTools

Microsoft [switched to Chromium to develop Edge](https://blogs.windows.com/windowsexperience/2018/12/06/microsoft-edge-making-the-web-better-through-more-open-source-collaboration/) more than 2 years ago now. While, at the time, it caused a lot of discussions in the web community, not much has been written or said about it since then. The people working on Edge (including its DevTools) have been busy though, and the browser has a lot of unique features now.

Being based on the Chromium open source project does mean that Edge benefits from all of its features and bug fixes. Practically speaking, the Edge team ingests the changes made in the Chromium repository in their own repository.

But over the past year or so, the team started to create Edge-specific functionality based on the needs of Edge users and feedback. Edge DevTools now has a series of unique features that I will go over.

### Opening, Closing, and Moving Tools
  
With almost 30 different panels, DevTools is a really complicated piece of software in any browser. But, you never really need access to all the tools at the same time. In fact, when starting DevTools for the first time, only a few panels are visible and you can add more later.

On the other hand though, it’s hard to discover the panels that aren’t shown by default, even if they could be really useful to you.

Edge added 3 small, yet powerful, features to address this:

- a close button on tabs to close the tools you don’t need anymore,
- a `+` (plus) button at the end of the tab bar to open any tool,
- a context menu option to move tools around.

The following GIF shows how closing and opening tools in both the main and drawer areas can be done in Edge.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d271eeaf-b930-421e-8d66-294e5f27b0ea/11-edge-close-open-tools.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b173b58-6e4a-4d20-8dcc-2cfeb29a22f8/11-edge-close-open-tools-800w.gif" width="800" height="604" alt="Gif animation showing the close button on tabs and the + button to open new tools." /></a><figcaption>Easily open the tools you need and close the ones you don’t. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d271eeaf-b930-421e-8d66-294e5f27b0ea/11-edge-close-open-tools.gif">Large preview</a>)</figcaption></figure>
  
You can also move tools between the main area and drawer area:

- right-clicking on a tab at the top shows a “Move to bottom” item, and
- right-clicking on a tab in the drawer shows a “Move to top” item.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4899e151-531d-430a-8002-baeb1466765a/12-edge-move-to-top-bottom.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d75349c5-d98c-42c8-9069-03c94c00e418/12-edge-move-to-top-bottom-800w.gif" width="800" height="604" alt="Gif animation showing the move to top and bottom contextual menus" /></a><figcaption>Move tools between the main top area and the bottom drawer area. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4899e151-531d-430a-8002-baeb1466765a/12-edge-move-to-top-bottom.gif">Large preview</a>)</figcaption></figure>
  
### Getting Contextual Help with the DevTools Tooltips

It is hard for beginners and seasoned developers alike to know all about DevTools. As I mentioned before, there are so many panels that it’s unlikely you know them all.

To address this, Edge added a way to go directly from the tools to [their documentation on Microsoft’s website](https://docs.microsoft.com/en-US/microsoft-edge/devtools-guide-chromium/).

This new [Tooltips feature](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/whats-new/2021/02/devtools#learn-about-devtools-with-informative-tooltips) works as a toggleable overlay that covers the tools. When enabled, panels are highlighted and contextual help is provided for each of them, with links to documentation.

You can start the Tooltips in 3 different ways:

- by using the <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>H</kbd> keyboard shortcut on Windows/Linux (<kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>H</kbd> on Mac);
- by going into the main (`...`) menu, then going into Help, and selecting “Toggle the DevTools Tooltips”;
- by using the [command menu](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/command-menu/) and typing “Tooltips”.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f531021-2826-4b39-85e0-21ae3982c8f6/13-edge-tooltips.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea9f3a6-29f2-4c8a-8e71-72cb1cc5d28b/13-edge-tooltips-800w.gif" width="800" height="604" alt="Gif animation showing the Tooltips overlay by going into the Help menu" /></a><figcaption>Display contextual help on the tools. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f531021-2826-4b39-85e0-21ae3982c8f6/13-edge-tooltips.gif">Large preview</a>)</figcaption></figure>

### Customizing Colors

In code editing environments, developers love customizing their color themes to make the code easier to read and more pleasant to look at. Because web developers spend considerable amounts of time in DevTools too, it makes sense for it to also have customizable colors.

Edge just [added a number of new themes to DevTools](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/whats-new/2021/07/devtools#apply-themes-from-visual-studio-code-to-devtools), on top of the already available dark and light themes. A total of 9 new themes were added. These come from [VS Code](https://code.visualstudio.com/) and will therefore be familiar to people using this editor.

You can select the theme you want to use by going into the settings (using `F1` or the gear icon in the top-right corner), or by using the [command menu](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/command-menu/) and typing `theme`.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e1fa87e-13f7-4870-a507-8defd4f454b7/14-edge-themes.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52ad08b4-ea32-4a8a-aed8-e183568d3431/14-edge-themes-800w.gif" width="800" height="604" alt="Gif animation showing how to choose different VS Code themes in DevTools by using the command menu" /></a><figcaption>Customize DevTools with one of 9 VS Code themes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e1fa87e-13f7-4870-a507-8defd4f454b7/14-edge-themes.gif">Large preview</a>)</figcaption></figure>
  
## Firefox DevTools

Similar to the Chrome DevTools team, the folks working on Firefox DevTools have been busy with a big architecture refresh aimed at modernizing their codebase. Additionally, their team is quite a bit smaller these days as Mozilla had to refocus over recent times. But, even though this means they had less time for adding new features, they still managed to release a few really interesting ones that I’ll go over now.

### Debugging Unwanted Scrollbars
  
Have you ever asked yourself: “where is this scrollbar coming from?” I know I have, and now Firefox has a tool to debug this very problem.

In the Inspector panel, all elements that scroll have a `scroll` badge next to them, which is already useful when dealing with deeply nested DOM trees. On top of this, you can click this badge to reveal the element (or elements) that caused the scrollbar to appear.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/299180c8-deb8-4d2a-80c0-68a14b7bf66b/15-firefox-overflow-debug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/299180c8-deb8-4d2a-80c0-68a14b7bf66b/15-firefox-overflow-debug.png" width="800" height="461" sizes="100vw" caption="Find the elements that cause unwanted overflow by clicking on the scroll badge. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/299180c8-deb8-4d2a-80c0-68a14b7bf66b/15-firefox-overflow-debug.png'>Large preview</a>)" alt="Screenshot of the Firefox Inspector panel showing a node with a scroll badge that was clicked on, and 2 descendant nodes with overflow badges that are highlighted" >}}

You can find [more documentation about it here](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Debug_Scrollable_Overflow).

### Visualizing Tabbing Order

Navigating a web page with the keyboard requires using the `tab` key to move through focusable elements one by one. The order in which focusable elements get focused while using `tab` is an important aspect of the accessibility of your site and an incorrect order may be confusing to users. It’s especially important to pay attention to this as modern layout CSS techniques allow web developers to rearrange elements on a page very easily.

Firefox has a useful Accessibility Inspector panel that provides information about the accessibility tree, finds and reports various accessibility problems automatically, and lets you simulate different color vision deficiencies.

On top of these features, the panel now provides a new page overlay that displays the tabbing order for focusable elements.

To enable it, use the “Show Tabbing Order” checkbox in the toolbar.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36bb80c4-9661-461a-b5e1-1dae1cb95861/16-firefox-tab-order.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36bb80c4-9661-461a-b5e1-1dae1cb95861/16-firefox-tab-order.png" width="800" height="444" sizes="100vw" caption="Highlight all the focusable elements and see the order in which they will be focused. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36bb80c4-9661-461a-b5e1-1dae1cb95861/16-firefox-tab-order.png'>Large preview</a>)" alt="Screenshot of Firefox DevTools' accessibility inspector with the tab order overlay enabled and labels on top of the page where focusable elements are" >}}

You can find [more documentation about it here](https://developer.mozilla.org/en-US/docs/Tools/Accessibility_inspector#show_web_page_tabbing_order).

### A Brand New Performance Tool
  
Not many web development areas depend on tooling as much as performance optimization does. In this domain, Chrome DevTools’ [Performance panel](https://developer.chrome.com/docs/devtools/evaluate-performance/) is best in class.

Over the past few years, Firefox engineers have been focusing on improving the performance of the browser itself, and to help them do this, they built a performance profiler tool. The tool was originally built to optimize the engine native code but supported analyzing JavaScript performance right from the start, too.

Today, this new performance tool replaces the old Firefox DevTools performance panel in pre-release versions (Nightly and Developer Edition). Take it for a spin when you get the chance.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6cceb4f-1ae5-44a8-b756-fe8cce3d425d/17-firefox-profiler.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6cceb4f-1ae5-44a8-b756-fe8cce3d425d/17-firefox-profiler.PNG" width="800" height="543" sizes="100vw" caption="The new Firefox Profiler lets you dig deep to discover where performance problems come from. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6cceb4f-1ae5-44a8-b756-fe8cce3d425d/17-firefox-profiler.PNG'>Large preview</a>)" alt="Screenshot of Firefox profiler." >}}

Among other things, the new Firefox profiler supports sharing profiles with others so they can help you improve the performance of your recorded use case.

You can read [documentation about it here](https://profiler.firefox.com/docs/#/), and learn more about [the project on their GitHub repository](https://github.com/firefox-devtools/profiler).

{{% ad-panel-leaderboard %}} 

## Safari Web Inspector

Last but not least, let’s go over a few of the recent Safari features.

The small team at Apple has been keeping itself very busy with a wide range of improvements and fixes around the tools. Learning more about the Safari Web Inspector can help you be more productive when debugging your sites on iOS or tvOS devices. Furthermore, it has a bunch of features that other DevTools don’t, and that not a lot of people know about.

### CSS Grid Debugging

With Firefox, Chrome, and Edge (and all Chromium-based browsers) having dedicated tools for visualizing and debugging CSS grids, Safari was the last major browser not to have this. Well, now it does!

Fundamentally, Safari now has the same features just like other browsers’ DevTools in this area. This is great as it means it’s easy to go from one browser to the next and still be productive.

- Grid badges are displayed in the Elements panel to quickly find grids.
- Clicking on the badge toggles the visualization overlay on the page.
- A new Layout panel is now displayed in the sidebar. It allows you to configure the grid overlay, see the list of all grids on the page and toggle the overlay for them.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c87fd0b1-b2e7-432c-a7ac-4bdee1b9e242/18-safari-grid-inspector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c87fd0b1-b2e7-432c-a7ac-4bdee1b9e242/18-safari-grid-inspector.png" width="800" height="567" sizes="100vw" caption="Highlight grid lines, grid gaps, grid areas, show line numbers, line names, and track sizes in the new Safari Grid inspector. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c87fd0b1-b2e7-432c-a7ac-4bdee1b9e242/18-safari-grid-inspector.png'>Large preview</a>)" alt="Screenshot of Safari, with the Elements panel showing the new Layout sidebar, and a highlighted grid in the page" >}}

What's interesting about Safari’s implementation though is that they’ve really nailed the performance aspect of the tool. You can enable many different overlays at once, and scroll around the page without it causing any performance problems at all.

The other interesting thing is Safari introduced a 3-pane Elements panel, just like Firefox, which allows you to see the DOM, the CSS rules for the selected element, **and** the Layout panel all at once.

Find out more about the CSS Grid Inspector on [this WebKit blog post](https://webkit.org/blog/11588/introducing-css-grid-inspector/).

### A Slew of Debugger Improvements
  
Safari used to have a separate Resources and Debugger panel. They have merged them into a single Sources panel that makes it easier to find everything you need when debugging your code. Additionally, this makes the tool more consistent with Chromium which a lot of people are used to.

Consistency for common tasks is important in a cross-browser world. Web developers already need to test across multiple browsers, so if they need to learn a whole new paradigm when using another browser’s DevTools, it can make things more difficult than they need to be.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03afe06d-30b8-4985-9dbf-0693f5a9532f/19-safari-sources.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03afe06d-30b8-4985-9dbf-0693f5a9532f/19-safari-sources.png" width="800" height="520" sizes="100vw" caption="The new unified Sources panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03afe06d-30b8-4985-9dbf-0693f5a9532f/19-safari-sources.png'>Large preview</a>)" alt="Screenshot of the Sources tab in Safari" >}}

But Safari also recently focused on adding innovative features to its debugger that other DevTools don’t have.

[Bootstrap script](https://webkit.org/web-inspector/inspector-bootstrap-script/):  
Safari lets you write JavaScript code that is guaranteed to run first before any of the scripts on the page. This is very useful to instrument built-in functions for adding `debugger` statements or logging for example.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c2012a-266f-4c90-842c-3a474b3eb00f/20-safari-bootstrap-script.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c2012a-266f-4c90-842c-3a474b3eb00f/20-safari-bootstrap-script.png" width="800" height="353" sizes="100vw" caption="Safari’s bootstrap scripts allow to run code before the page loads to override built-in objects and APIs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c2012a-266f-4c90-842c-3a474b3eb00f/20-safari-bootstrap-script.png'>Large preview</a>)" alt="Screenshot of Safari’s Sources tab, showing the Bootstrap Script with code that overrides localStore.setItem to log information when this API is called." >}}
  
[New breakpoint configurations](https://webkit.org/web-inspector/javascript-breakpoints/):  
All browsers support multiple types of breakpoints like conditional breakpoints, DOM breakpoints, event breakpoints, and more.

Safari recently improved their entire suite of breakpoint types by giving them all a way to configure them extensively. With this new breakpoint feature, you can decide:

- if you want a breakpoint to only hit when a certain condition is true,
- if you want the breakpoint to pause execution at all, or just execute some code,
- or even play an audio beep so you know some line of code was executed.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85a159c6-e5c5-4bc7-86ca-cd3a63946d7e/21-safari-breakpoint-options.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85a159c6-e5c5-4bc7-86ca-cd3a63946d7e/21-safari-breakpoint-options.png" width="800" height="453" sizes="100vw" caption="Configure your breakpoints exactly how you want them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85a159c6-e5c5-4bc7-86ca-cd3a63946d7e/21-safari-breakpoint-options.png'>Large preview</a>)" alt="Screenshot of the breakpoint options tooltip in Safari, showing how you can configure breakpoints" >}}
  
[`queryInstances` and `queryHolders` console functions](https://webkit.org/web-inspector/console-command-line-api/#functions):  
These two functions are really useful when your site starts using a lot of JavaScript objects. In some situations, it may become difficult to keep track of the dependencies between these objects, and memory leaks may start to appear, too.
  
Safari does have a Memory tool that can help resolve these issues by letting you explore memory heap snapshots. But sometimes you already know which class or object is causing the problem and you want to find what instances exist or what refers to it.

If `Animal` is a JavaScript class in your application, then `queryInstances(Animal)` will return an array of all of its instances.

If `foo` is an object in your application, then `queryHolders(foo)` will return an array of all the other objects that have references to `foo`.

## Closing Thoughts

I hope these features will be useful to you. I can only recommend using multiple browsers and getting familiar with their DevTools. Being more familiar with other DevTools can prove useful when you have to debug an issue in a browser you don’t use on a regular basis.

Know that the companies which make browsers all have teams working on DevTools actively. They’re invested in making them better, less buggy, and more powerful. These teams depend on **your feedback** to build the right things. Without hearing about what problems you are facing, or what features you lack, it’s harder for them to make the right decisions about what to build.

Reporting bugs to a DevTools team won’t just help you when the fix comes, but may also be helping many others who have been facing the same issue.

It’s worth knowing that the DevTools teams at Microsoft, Mozilla, Apple and Google are usually fairly small and receive a lot of feedback, so reporting an issue does not mean it will be fixed quickly, but it does help, and those teams **are listening**.

Here are a few ways you can report bugs, ask questions or request features:

- **Firefox DevTools**
  - Firefox uses [Bugzilla](https://bugzilla.mozilla.org/) as their public bug tracker and anyone is welcome to report bugs or ask for new features by creating a new entry there. All you need is a GitHub account to log in.
  - Getting in touch with the team can either be done on Twitter by using the [@FirefoxDevTools](https://twitter.com/FirefoxDevTools) account or logging in to [the Mozilla chat](https://chat.mozilla.org) (find documentation about the chat [here](https://wiki.mozilla.org/Matrix)).
- **Safari Web Inspector**
  - Safari also uses public bug tracking for their [WebKit bugs](https://bugs.webkit.org/). Here is documentation about how to [search for bugs and report new ones](https://webkit.org/reporting-bugs/).
  - You can also get in touch with the team on Twitter with [@webkit](https://twitter.com/webkit).
  - Finally, you can also signal bugs about Safari and the Safari Web Inspector using the [feedback assistant](https://developer.apple.com/bug-reporting/).
- **Edge DevTools**
  - The easiest way to report a problem or ask for a feature is by using [the feedback button](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/#getting-in-touch-with-the-microsoft-edge-devtools-team) in DevTools (the little stick figure in the top-right corner of the tools).
  - Asking questions to the team works best over Twitter by mentioning the [@EdgeDevTools](https://twitter.com/EdgeDevTools) account.
- **Chrome DevTools**
  - The team listens for feedback on [the devtools-dev mailing list](https://www.chromium.org/teams/devtools) as well as on twitter at [@ChromeDevTools](https://twitter.com/ChromeDevTools).
- **Chromium**
  - Since Chromium is the open-source project that powers Google Chrome and Microsoft Edge (and others), you can also report issues on the [Chromium’s bug tracker](https://bugs.chromium.org/p/chromium/issues/list).

With that, thank you for reading!

{{< signature "vf, yk, il" >}}
