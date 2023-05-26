---
title: 'DevTools Debugging Tips And Shortcuts (Chrome, Firefox, Edge)'
slug: useful-chrome-firefox-devtools-tips-shortcuts
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20b67a97-e8f3-497f-a43d-fe321969a56c/better-browser-profiles.png
date: 2021-02-16T16:30:00.000Z
summary: >-
  DevTools is very advanced and helpful, but can also be very intimidating and overwhelming. Let’s fix that. In this article, Vitaly reviews useful features and shortcuts for debugging in Chrome, Firefox, Edge and Safari.
description: >-
  DevTools is very advanced and helpful, but can also be very intimidating and overwhelming. Let’s fix that. In this article, Vitaly reviews useful features and shortcuts for debugging in Chrome, Firefox, Edge and Safari.
categories:
  - Tools
  - Debugging
  - Refactoring
  - Workflow
  - DevTools
  - Guides
---

Out of all the tools available at our fingertips these days, DevTools is probably one of the most advanced ones. Over the years, it has become a tool for debugging, profiling, auditing and even prototyping &mdash; all living within the same interface, and always just a keyboard shortcut away. Still, DevTools has plenty of obscure gems and undiscovered treasures, living on the remote fringes of hidden tabs and experimental settings. Let’s fix that.

In this article, let’s dive into some of the **useful and obscure features in DevTools**. We’ll look into all modern browsers (Chrome, Firefox, Edge, Safari) and look into the useful tools that they provide to us, web developers. We’ll focus on the ones that we use frequently on SmashingMag, and some of the little techniques and strategies that help us fix pesky bugs and write better code.  

## Creating Browser Profiles

When it comes to profiling a website for performance, or tracking a particular accessibility issue, we’ve been creating separate browser profiles for each task for a while now. We usually work with at least 5 user profiles, each with its own extensions, bookmarks, bookmarklets and features turned on or off. Let’s take a closer look at them.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20b67a97-e8f3-497f-a43d-fe321969a56c/better-browser-profiles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20b67a97-e8f3-497f-a43d-fe321969a56c/better-browser-profiles.png" width="800" height="635" sizes="100vw" caption="Dedicated browser profiles for accessibility testing, debugging, performance audits and checking the experience for happy and unhappy customers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20b67a97-e8f3-497f-a43d-fe321969a56c/better-browser-profiles.png'>Large preview</a>)" alt="Dedicated browser profiles for accessibility testing, debugging, performance audits and checking the experience for happy and unhappy customers." >}}

- **Accessibility profile**    
A clean browser profile that includes various tools for checking accessibility, e.g. [Accessibility Insights](https://accessibilityinsights.io/), [aXe](https://www.deque.com/axe/) and [a11y.css](https://github.com/ffoodd/a11y.css), along with a few other [accessibility linters](https://twitter.com/alexanderadam__/status/1274982660666986496) and color vision simulator.

- **Debugging profile**  
A profile with a few experimental settings for profiling turned on, as well as an option to automatically open DevTools for every new window, along with a custom [diagnostics CSS](https://gist.github.com/tkadlec/683b26344cde774170b94c0fcf0088b4) for quick auditing and profiling.

- **Performance profile**  
A clean profile without extensions, with a few special bookmarks for auditing with Lighthouse, [RequestMap](https://requestmap.webperf.tools/), a performance [diagnostics CSS](https://gist.github.com/tkadlec/683b26344cde774170b94c0fcf0088b4) and a few performance-related links to keep in mind (e.g. [resource priority in loading](https://addyosmani.com/blog/script-priorities/)). Always goes well with 4 × [CPU throttling](https://umaar.com/dev-tips/88-cpu-throttling/) and [Network throttling](https://umaar.com/dev-tips/66-network-throttling-profiles/) (Slow 3G).

- **Happy customer**  
Based on the data we have from our analytics, that’s a profile that is close enough to the one that many of our readers (wonderful people like you) will have. It will contain a few [popular extensions](https://www.debugbear.com/blog/2020-chrome-extension-performance-report), common web development extensions, ad-blockers, tab management, Google Docs offline, LastPass, VPN, Browserstack, Grammarly etc. No throttling in use.
    
- **Unhappy customer**  
A profile for a reader on a slow, throttled connection (slow 3G), low memory, poor CPU, with 10 most popular browser extensions on. We usually use this profile to test our *heaviest* pages to experience the worst possible customer experiences.

Depending on the task at hand, we can jump to one of the dedicated profiles. The actual convenience comes from the simple arrangement that each of the profiles has **specific extensions**, bookmarklets and browser settings all set and ready to go. So if needed, we can get right to performance debugging or accessibility auditing without any hassle for searching the right extensions.

It probably goes without saying that we do our best to keep each profile clean and uncluttered &mdash; that goes for browser extensions as well as browser bookmarks, cookies and cache.

{{% feature-panel %}}

## Global Keyboard Shortcuts

Admittedly, with the sheer amount of features available in DevTools, it’s not very surprising that some of them are quite difficult to find between tabs, panels, gear icons and dots. However, there is no need to memorize the place where they are placed. Instead, it’s worth remembering just a couple of useful global keyboard shortcuts &mdash; they will help you jump to specific features faster.

- **Opening the Command Menu** (Chrome, Edge)  
Being probably one of the most well-known ones, this command actually has two features. <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> opens a quick **autocomplete search** for panels, drawers and all the features within DevTools. <kbd>Cmd/Ctrl</kbd> + <kbd>P</kbd> opens a drawer with all available **files** used on the current page. If you need to quickly access any DevTools feature, the Command Menu is a quick way to get there &mdash; for general drawers, hidden menus or specific features.
    
- **Opening DevTools Settings** (all modern browsers)  
Usually there are plenty of obscure tools and features hidden in the “Settings” panel &mdash; from emulated devices to network throttling profiles and experiments. In Chrome,  you can click on the gear icon in the right upper corner or use <kbd>Shift</kbd> + <kbd>?</kbd>. In Firefox, you can jump to Settings with <kbd>F1</kbd>.
    
- **Toggle Inspect Element Mode** (all modern browsers)  
Instead of clicking on an Inspect icon and then focusing on the element you’d like to debug, you can toggle Inspect Element Mode with <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd>.
    
- **Toggle the HTML mode** (all modern browsers)
While inspecting an element, you might want to change its attributes, e.g. classes or states. Instead of right-clicking on the element and adding values one-by-one, you can toggle the HTML mode on the currently selected element with <kbd>Fn</kbd> + <kbd>F2</kbd> (or just <kbd>F2</kbd> on Windows). 
    
- **Toggle Device mode** (all modern browsers)
To jump into the device toolbar mode, e.g. to preview how the mock-up looks like on narrow screens, or trigger a media query debugger, you can use <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>M</kbd> in Chrome, and <kbd>Cmd/Ctrl</kbd> + <kbd>Opt/Alt</kbd> + <kbd>M</kbd> in Firefox.

There are also plenty of other useful keyboard shortcuts, e.g. for pausing and resuming script execution, and go to matching bracket (for lengthy media queries and JS functions) in the source editor.

You can find a full overview of all keyboard shortcuts on [Chrome DevTools Keyboard Shortcuts](https://developers.google.com/web/tools/chrome-devtools/shortcuts?utm_source=devtools) and [Firefox DevTools Keyboard Shortcuts](https://developer.mozilla.org/en-US/docs/Tools/Keyboard_shortcuts) &mdash; more often than not, they are quite consistent across modern browsers.

## Turn On Experimental Settings

DevTools comes along with a set of experimental settings which aren’t quite recommended for a wide audience, but can indeed be very useful for debugging. A word of caution though: sometimes these settings might freeze Chrome or make it quite sluggish (which is why they are experimental in the first place).

However, with **separate profiles** in place, you could safely turn on some of these settings for each profile, and then turn them off if necessary. So while we use our regular profiles without experiments turned on for casual browsing, in debugging mode we always pick a dedicated profile first, to squish those bugs just a little bit faster.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0bcb71b-8b33-451f-8619-862826a03def/experimental-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0bcb71b-8b33-451f-8619-862826a03def/experimental-settings.png" width="800" height="635" sizes="100vw" caption="Experimental settings, with a few useful settings turned on, e.g. CSS Overview, CSS Grid, Flexbox and Timeline settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0bcb71b-8b33-451f-8619-862826a03def/experimental-settings.png'>Large preview</a>)" alt="A screenshot of experimental settings in Chrome, for comparison." >}}

With DevTools open in Chrome, jump to “Settings” (<kbd>Shift</kbd> + <kbd>?</kbd> with DevTools open) and find “Experiments” in the sidebar. Obviously, there are plenty of experimental settings available in every DevTools, but the ones mentioned below are just the ones we find quite helpful at our work.

Across the featured listed there, it’s worth turning on *“Automatically pretty print in the Source Panel”*, which would prettify compressed styles and scripts by default when viewing source. You can also *enable CSS Grid debugger* and *Flexbox debugging* for dealing with layout issues. There is also a source diff and a source order viewer that can come in handy.

And for performance audits, you could mark **“Timeline: event initiators”** and “Timeline: invalidation tracking” that will show in the Performance panel, highlighting scripts that caused expensive operations such as Long Tasks and Style Recalculations. Additionally, in Edge, you can enable composited layers in 3D view.

For a given profile, you can access more hidden features by heading to `chrome://flags/` in the browser profile of your choice. for example, that’s where you can turn on **latest and experimental JavaScript features**, experimental Web Platform features or enable resource loading hints to provide a preview over slow network connections.

In Firefox, jump to Settings with <kbd>F1</kbd>. At the bottom of the dock, you can prompt the browser to show browser styles, turn on/off autocomplete CSS, change editor preferences, toggle paint flashing, adjust screenshot behavior and enable **source maps** (not turned on by default). In Safari, you can find Experimental Settings under "Develop &rarr; Experimental Settings".

## Switching Between Dock States (Chrome, Edge, Firefox)

Admittedly, the pane view in DevTools isn’t a particularly big revelation. In the “Styles” tab of the dock, styles appear from top to bottom, ordered by their CSS specificity. However, one little thing we’ve been overlooking a lot for years is a little toggle button `:hov` placed just above the styles.

It allows you to force an element state (`:active`, `:focus`, `:focus-within`, `:hover`, `:visited` and `:focus-visible`, and most recently `:target`) on a particular interactive element &mdash; e.g. to enforce `:focus` and `:active` states on buttons for accessibility checks.

In Firefox, you can change a pseudo-class for a DOM element as you are inspecting it — the feature is available with a right-click on a DOM node.

One thing that always gets in the way though is the **position of the dock**, which sometimes works better on the right hand side, and sometimes at the bottom &mdash; depending on where your bug has invaded your DOM tree.

To quickly **switch between dock states**, you can use <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>D</kbd>. One catch to keep in mind is that the shortcut will undock DevTools into a separate window only if DevTools has been in its default position (docked to the right). Otherwise the shortcut will just switch between the default position and the one you’ve changed it to.

## Triple Panes View (Firefox)

While we might be used to a double-pane view, Firefox provides a helpful **triple-panes-view** by default — it looks slightly differently across different sections. In the Inspector view, alongside HTML and styles you can place layout debugger, show computer styles or track CSS changes &mdash; it’s very useful to have quick access to all this information without having to switch between tabs.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a819e8c1-ba84-4fd2-862c-0eb02b2b9117/02-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a819e8c1-ba84-4fd2-862c-0eb02b2b9117/02-useful-devtools-tips-shortcuts.png" width="800" height="552" sizes="100vw" caption="Triple Panes View in Firefox, with Layout features explained at the bottom right corner. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a819e8c1-ba84-4fd2-862c-0eb02b2b9117/02-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Triple-panes-view of Smashing Magazine website" >}}

Whenever you are editing styles in Firefox, DevTools highlights **media queries used across the page**, with quick jumps to CSS sections where a breakpoint behavior is defined. All of it is displayed right next to the source code, so no need to search for a specific breakpoint. (Not to mention styles pretty-formatted by default &mdash; that’s handy!).

A similar view is also available in Chrome and Edge as well, but it’s available only in the "Elements" panel (sidebar icon in the right upper corner), and so far it shows only computed styles (which is why it’s called "Computed Styles Sidebar").
## Filtering Styles By Property (Firefox)

In general, Firefox DevTools are heavily underrated. Another remarkable feature that Firefox provides is an option to **filter all styles by a particular property** (indicated with a filter icon). For example, if you notice that some styles are overwritten by other ones scattered somewhere across the stylesheet, you can hide all the definitions that don’t affect that particular property with a quick filter and see where exactly overrides are happening.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507c4f74-a36c-4ca3-9c98-10c74c5437b1/filter-styles-firefox.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507c4f74-a36c-4ca3-9c98-10c74c5437b1/filter-styles-firefox.png" width="800" height="697" sizes="100vw" caption="In Firefox, if some styles are overwritten, you can filter out the entire overview by the exact places where the styles get redefined. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507c4f74-a36c-4ca3-9c98-10c74c5437b1/filter-styles-firefox.png'>Large preview</a>)" alt="Filtering styles by a property in Firefox." >}}

Also, on a given page, you can **highlight all instances that match a particular selector.** For example, if you notice a bug with a rendering of profile images on dark and light sections of the page, you can highlight all instances of a particular class without manually searching for them or adding extra styles to highlight them. It’s enough to locate the selector in Styles panel and choose a target icon to “highlight all elements matching this selector”.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3edfc9be-f744-433a-ae2e-e1c086e62fac/03-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3edfc9be-f744-433a-ae2e-e1c086e62fac/03-useful-devtools-tips-shortcuts.png" width="800" height="697" sizes="100vw" caption="Highlighting all elements matching a selector in Firefox DevTools. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3edfc9be-f744-433a-ae2e-e1c086e62fac/03-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Highlighting all elements matching a selector in Firefox DevTools." >}}

In the “Styles” panel, Firefox also explains which CSS properties aren’t affecting the selected element and why, along with recommendations of what might help to fix the issue or avoid unexpected behavior (the feature is called [Inactive CSS](https://hacks.mozilla.org/2019/10/firefox-70-a-bountiful-release-for-all/#developertools)).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40e1ecbc-f5c0-4bc0-9210-0034f7fec8a0/04-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40e1ecbc-f5c0-4bc0-9210-0034f7fec8a0/04-useful-devtools-tips-shortcuts.png" width="800" height="471" sizes="100vw" caption="Helpful notes on CSS properties that aren’t affecting the selected element and why, along with useful recommendations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40e1ecbc-f5c0-4bc0-9210-0034f7fec8a0/04-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Inactive CSS feature" >}}

Another handy feature is that Firefox assigns `scroll` and `overflow` badges to elements that are causing the container to overflow or scroll ([overflow debugging](https://twitter.com/FirefoxDevTools/status/1316443562867912704)) &mdash; very helpful when you are trying to figure out why a horizontal scrollbar appears all of a sudden, or an element doesn’t behave as expected.

{{% ad-panel-leaderboard %}} 

## Expanding Nodes Recursively (Chrome, Edge, Firefox)

When inspecting an element with a deeply nested DOM, sometimes it might take a while to traverse down the tree, from one nested node to another. By right-clicking on the arrow on a node, you can choose “Expand recursively” and the currently-selected node (and all of its children) will expand with one single click. Alternatively, you can hold <kbd>Option</kbd> (or <kbd>Ctrl</kbd> + <kbd>Alt</kbd> on Windows) while clicking the arrow icon next to the element’s name.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38420f1e-66af-4c16-af35-9c6dc023655b/05-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38420f1e-66af-4c16-af35-9c6dc023655b/05-useful-devtools-tips-shortcuts.png" width="760" height="528" sizes="100vw" caption="Expanding a node recursively with a quick shortcut. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38420f1e-66af-4c16-af35-9c6dc023655b/05-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="“Expand recursively” node" >}}

## Gather And Export Code Coverage (Chrome, Edge)

On a given page, much of the CSS and JavaScript might not be used at all, although it will be shipped to the browser. The <strong>“Code coverage” panel</strong> (Command menu → “Show coverage”) allows you to explore which styles and code aren’t used on a given page. We use code coverage to collect critical CSS for each of the templates used on the site, and doing so manually can be quite tiring.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75a1874-f431-44e9-87a3-993593580ded/06-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75a1874-f431-44e9-87a3-993593580ded/06-useful-devtools-tips-shortcuts.png" width="800" height="546" sizes="100vw" caption="Exploring the amount of used and unused CSS and JavaScript, with Code Coverage. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75a1874-f431-44e9-87a3-993593580ded/06-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="The Code coverage panel" >}}

With “Code coverage” in place, going through a couple of scenarios that include a lot of tapping, tabbing and window resizing, we also [export coverage data](https://twitter.com/chromedevtools/status/1286663677240737793) that DevTools collects as JSON (via the export/download icon). On top of that, you could use Puppeteer that also provides an [API to collect coverage](https://pptr.dev/#?product=Puppeteer&show=api-class-coverage) (but we aren’t there yet). 

## Media Queries Debugging (Chrome, Edge)

With dozens of media queries in flight for a given page, it can easily become difficult to keep track of the styles being overwritten by other styles scoped within a media query. To find the specific section in your CSS file that might be causing unexpected behavior, we could turn our attention to the **media query debugger**. By default, it’s hidden away behind the "Settings" cog in the device toolbar, but it’s actually quite helpful when it’s available by default.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5df01468-0db8-4a5a-adad-46fb4d77bd0b/07-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5df01468-0db8-4a5a-adad-46fb4d77bd0b/07-useful-devtools-tips-shortcuts.png" width="800" height="499" sizes="100vw" caption="The horizontal bars on the top indicate media queries and breakpoint ranges, starting from center and going outwards. The ones closer to the center of the screen are overwritten by the ones further away from the center. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5df01468-0db8-4a5a-adad-46fb4d77bd0b/07-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="The horizontal bars on the top indicate media queries and breakpoint ranges, starting from center and going outwards. The ones closer to the center of the screen are overwritten by the ones further away from the center." >}}

Toggle the device toolbar (responsive mode) with <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>M</kbd> and choose the three dots in the right upper corner. Then choose “Show media queries”. Now you should be able to see horizontal bars representing the **scope of each media query**.

They might appear a bit confusing at first, but the way these bars are aligned represents screen width, and is replicated on the left and on the right side of the viewport. The bars closer to the center of the screen are overwritten by the ones further away from the center. The blue bar on the top indicates `max-width`  media queries, the green one `min-width` and `max-width` media queries, and orange one stands for only `min-width` media queries. 

For all of the bars, you can track which media queries they contain when hovering over them. You can jump to a **specific media query range** and inspect layout issues in detail with Styles panel open. By clicking on any position on a bar, you can trigger specific breakpoints, and if you right click on a bar, you can reveal its position in the source code. In fact, you can quickly jump back and forth between media queries, rather than resizing the screen manually and checking the screen width over and and over again.

As a quick side note, you can also **specify your custom emulated devices** instead of the pre-defined ones &mdash; in fact, there are plenty of device presets available already. Plus, you can use the "Sensors" pane to [control specific device sensors](https://umaar.com/dev-tips/106-sensors-pane/) if needed. Additionally, in Firefox you can enable and disable touch simulation, and define a specific User Agent, e.g. to check how the page behaves with a search engine crawler requesting the page.

## Emulate Preference Media Queries (Chrome, Edge, Firefox)

Additionally to screen size-related media queries, we can also emulate accessibility-specific media queries, e.g. `prefers-color-scheme`, `prefers-reduced-motion` and vision deficiencies. To toggle the emulation, head to the Command Control panel (<kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>) and type “Show rendering”. Now, in the settings you can choose a preferred emulation.

(That’s also where you can choose to highlight areas that need to be repainted ("Paint Flashing"), areas that have shifted ("Layout Shift Regions") and debug scrolling performance issues.)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a5e1d66-1e35-4cb2-9d88-1250dc916959/08-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a5e1d66-1e35-4cb2-9d88-1250dc916959/08-useful-devtools-tips-shortcuts.png" width="800" height="539" sizes="100vw" caption="DuckDuckGo supports dark mode out of the box, by using prefers-color-scheme media query. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a5e1d66-1e35-4cb2-9d88-1250dc916959/08-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="DuckDuckGo supports dark mode out of the box, by using prefers-color-scheme media query." >}}

Talking about emulation: remember how in the past you might have struggled with finding a layout bug for you print stylesheet? In the same panel, you can preview how your **print styles** work here as well &mdash; no need to print a PDF of a random page over and over again to figure out what caused a major rendering issue any more.

Also, in the same panel in Chrome you can add all sorts of rendering debugging features &mdash; e.g. paint flashing, layer borders, scrolling performance issues, disabling AVIF and WebP.

As a side note, there is a DevTools toolbar option for “**Force Dark Appearance**” and a "**Force Print Media styles**" in Safari, and you can simulate vision deficiencies in the “Accessibility” tab in Firefox. (We’ll talk a bit more about Accessibility later.) In Firefox, the print view is also available above the "Styles" pane in the "Inspect" mode.

## Automatically Open DevTools In Each New Tab (Chrome)

With performance audits, we might want to be exploring multiple page at once, and observe how they behave with separate DevTools, without having to wondering which DevTools is responsible for which window. To save a bit of time during debugging, you could create a **shortcut with a Terminal command** that would open a browser with DevTools automatically opening by default in each new tab.

To achieve that, we need to pass the flag `--auto-open-devtools-for-tabs` when running a Chrome, Edge-based browser. We run a simple Alfred script to open the Canary browser with the flag when needed (hat tip to [Addy](https://addyosmani.com/blog/automatically-open-chrome-devtools-in-each-new-tab/)) &mdash; very useful when you really need it:

<pre class="language-bash break-out">
<code>/Applications/Google\ Chrome\ Canary.app/Contents/MacOS/Google\ Chrome\ Canary --auto-open-devtools-for-tabs htps://www.smashingmagazine.com</code></pre>

You can find a very comprehensive overview of all Chrome, Edge command line switches in Peter Beverloo’s guide on [Chrome Command Line Switches](https://peter.sh/experiments/Chrome, Edge-command-line-switches/).

## Full Page Screenshots (Chrome, Edge, Firefox)

When selecting an HTML node in the “Elements” pane, you could right-click on the node and prompt the DevTools to create a screenshot of that node, and in the “Responsive mode” you can capture a screenshot of the visible portion of the page or a full size screenshot (three dots in the right upper corner).

To create a **full size screenshot** a little bit faster, you can also prompt a “Full page screenshot” in the Command Menu (<kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> → “Full page screenshot”). Usually it’s a little bit faster. Just keep in mind that portions of the page that are lazy-loaded or rendered progressively (e.g. with `content-visibility`) might not show up properly in the screenshot, so you might need to scroll all the way down the page first.

In Firefox, you can generate a screenshot of the **visible portion of the page** by going to the "Device Toolbar" mode first, then spotting the camera icon in the right upper corner and activating it. Or for a full page screenshot, you’d need to toggle "Take a screenshot of the entire page" in "Settings" first, and then you’ll find the camera icon in the DevTools toolbar.

## Rulers For Components (Chrome, Edge, Firefox)

Perhaps you’d like to quickly check the width and height of an image, or an advertising spot. But rather than taking a screenshot, or inspecting element and copy/pasting `width` and `height` values, you can use a rules to measure the size of a component. Rules are provided all across modern browsers, but Firefox DevTools also allows you to **measure a portion of the page**. You can find the measurement tool on the right hand side of DevTools, right next to the “Responsive mode” icon.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ae5eaf-eb3a-437b-987c-177781f9cd2f/09-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ae5eaf-eb3a-437b-987c-177781f9cd2f/09-useful-devtools-tips-shortcuts.png" width="800" height="646" sizes="100vw" caption="Measuring a portion of the page out of the box, with Firefox. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ae5eaf-eb3a-437b-987c-177781f9cd2f/09-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Rulers" >}}

## Tracking Changes (Chrome, Edge, Firefox)

As you are debugging a particular problem, you might have commented out some lines of code, and probably added some new code that seems to be fixing the problem for good. Your changes now have to be replicated in the actual source files. To do that, there is **no need to manually collect all the changes you’ve made** all across your files.

In Chrome, toggle “Local Modifications” command when editing the source file. You should see a tracker of changes appearing in the panel below. If it’s collapsed, pull it out by dragging it vertically. The pane **highlights changed properties** and what exactly has changed, so you can copy-paste modifications right away.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73a89cd9-cd0e-441a-b433-7922df802cfb/10-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73a89cd9-cd0e-441a-b433-7922df802cfb/10-useful-devtools-tips-shortcuts.png" width="800" height="330" sizes="100vw" caption="You can call “Local Modifications” pane from within your source code changes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73a89cd9-cd0e-441a-b433-7922df802cfb/10-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Local Modifications pane, called from source code changes." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e4a6dbb-c58d-44a7-b38d-5f93762d368a/11-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e4a6dbb-c58d-44a7-b38d-5f93762d368a/11-useful-devtools-tips-shortcuts.png" width="800" height="528" sizes="100vw" caption="No need to keep track of your changes: Devtools does it for you, with the “Changes” pane. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e4a6dbb-c58d-44a7-b38d-5f93762d368a/11-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="No need to keep track of your changes: Devtools does it for you, with the “Changes” pane." >}}

One thing to keep in mind is that it’s probably a good idea to track changes while running your local server &mdash; without automatic removal of line breaks and spaces as they would show up as changes as well. This problem doesn’t exist in Firefox, where you can also find a **“Changes” pane** which does the same thing, along with a friendly button “Copy All Changes”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f7411e2-ed77-4702-96fb-b22cecd64d01/12-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f7411e2-ed77-4702-96fb-b22cecd64d01/12-useful-devtools-tips-shortcuts.png" width="800" height="344" sizes="100vw" caption="The “Changes” pane in Firefox tracks all the changes made. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f7411e2-ed77-4702-96fb-b22cecd64d01/12-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="The “Changes” pane in Firefox tracks all the changes made." >}}

## Local Overrides (Chrome, Edge)

You might have been in this situation before: you just want to experiment with a few changes, but might be quite afraid to accidentally hit “Refresh” in the browser to lose all the changes made on the page. Perhaps you **can’t really run the site locally**, or perhaps you just don’t want to run your entire build for some minor local modifications. In such cases, Chrome’s “Local Overrides” can be a godsend.

First, create a folder on your machine where all your **local modifications** will be stored (`local-overrides` on Desktop seems like a reasonable name and place for this kind of task). Then head to the “Sources” tab, and choose “Overrides” in the top-left corner of DevTools (it might be hidden behind a double-chevron). Now click on “Select folder for overrides” and choose your freshly created folder &mdash; that’s the folder that Chrome will be using to store your local modifications. You’ll need to click “Allow” to grant Chrome permissions to save files to your hard drive.

Now, you can choose any file in the “Sources” panel, right-click anywhere in the code and choose **“Save for overrides”** with the right-click. That’s a clue for Chrome to create a new file, and store all contents of the file, along with your modifications, to your hard drive. (You might want to click the `{}` button first to make the code slightly more readable). (*Thanks to* [*Trys*](https://www.trysmudford.com/blog/chrome-local-overrides/) *for the hint!*)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a65a674-755d-4cb5-ad4a-39c41a78c769/13-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a65a674-755d-4cb5-ad4a-39c41a78c769/13-useful-devtools-tips-shortcuts.png" width="800" height="436" sizes="100vw" caption="A purple icon next to the source file indicates that the file is stored locally, via local overrides. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a65a674-755d-4cb5-ad4a-39c41a78c769/13-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="“Sources” panel" >}}

Once you’ve defined your local overrides, Chrome will intercept network requests and use your code instead of the actual response. It will also watch out for modifications made to the file and **inject changes into the page automatically**, very much as if you had a local development installed with the watch mode on. Any files that are overwritten by local overrides will have a little **purple dot** next to them in the “Elements” panel.

*The best part*: now you can **open the file in your text editor and make changes from there**, while seeing these changes appearing in DevTools as well &mdash; and if you need to switch to DevTools to add breakpoints, you can do it from DevTools, make changes to the code, and these changes will be visible in your text editor as well. Almost magic!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17aaf849-d9f6-43ca-bca7-3fd1aaa2ad5c/14-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17aaf849-d9f6-43ca-bca7-3fd1aaa2ad5c/14-useful-devtools-tips-shortcuts.png" width="800" height="508" sizes="100vw" caption="Pro-tip from a local-overrides-fan <a href='https://twitter.com/csswizardry/status/1357311634528755712/photo/1'>Harry Roberts</a>: attach a query string to the URL and you can load separate variants of the same page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17aaf849-d9f6-43ca-bca7-3fd1aaa2ad5c/14-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="exaple of a query string" >}}

[Pro-tip from Harry Roberts](https://twitter.com/csswizardry/status/1357311634528755712/photo/1): Local Overrides don’t allow you to keep or track versions or variants, but you can attach a **query string** to the URL and load separate variants of the same page. Extremely useful when editing HTML pages.

Ah, and if you need to disable local overrides again, just check off “Enable Local Overrides” in the same pane &mdash; otherwise the styles will overwrite existing styles over and over again, which is something you might not want.

## Remote Debugging (Chrome, Safari)

If you need to debug your apps or pages on a mobile phone, you can [use a Devtools proxy for iOS devices](https://jonsadka.com/blog/how-to-debug-a-chrome-specific-bug-on-ios-using-remote-debugging) to debug Chrome on iOS, and also use DevTools to [debug Mobile Safari on iOS with Chrome DevTools](https://medium.com/@nikoloza/how-to-debug-remote-ios-device-using-chrome-devtools-f44d697003a7).

To [debug Mobile Safari with Safari Inspector](https://www.kenst.com/2019/03/how-to-debug-problems-on-mobile-safari/), enable "Web Inspector" in "Settings &rarr; Safari &rarr; Advanced &rarr; Web Inspector" and open the debugger with "Develop" &rarr; (Your phone’s name). You should have Safari’s DevTools opening up for you.

For Android devices, open the *Developer Options* on Android and select **"Enable USB Debugging"**. On your development machine, you can then discover your mobile device by going to [`chrome://inspect#devices`](chrome://inspect#devices) and choosing your "Remote Target". You can find plenty of details and instructions on ["Get Started With Remote Debugging Android Devices"](https://developers.google.com/web/tools/chrome-devtools/remote-debugging). That’s also where you can find a dedicated DevTools for Node.js debugging.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/153b4026-6ddf-4e78-aca1-3c331ebcf847/mobile-web-page-safari-inspector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/153b4026-6ddf-4e78-aca1-3c331ebcf847/mobile-web-page-safari-inspector.png" width="800" height="548" sizes="100vw" caption="Debugging a mobile web page with Safari Inspector. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/153b4026-6ddf-4e78-aca1-3c331ebcf847/mobile-web-page-safari-inspector.png'>Large preview</a>)" alt="Debugging a mobile web page with Safari Inspector" >}}

## Pause Script Execution (Chrome, Edge, Firefox)

When testing critical CSS or debugging JavaScript, you might want to **hold on to the state of the DOM** before a particular script gets executed or a particular style gets applied. That’s what DOM change breakpoints in DevTools are for.

By right-clicking on the three ominous dots next to the element’s name, you could pick “Break on” subtree modifications (node insertions and removals in the DOM tree rooted at the given node), attribute modifications (e.g. when an attribute is added or removed, or an attribute value changes &mdash; e.g. with classes) or node removal.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e2567c-648f-490b-b905-a9218cd6ea6f/15-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e2567c-648f-490b-b905-a9218cd6ea6f/15-useful-devtools-tips-shortcuts.png" width="800" height="553" sizes="100vw" caption="A conditional line-of-code breakpoint on line 32. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89e2567c-648f-490b-b905-a9218cd6ea6f/15-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="A conditional line-of-code breakpoint on line 32." >}}

However, you can also use a [conditional line-of-code breakpoint](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints#conditional-loc) when you know the exact region of code that you need to investigate, but you want to pause only when some other condition is true. Plus, not to forget [logpoints](https://twitter.com/dan_abramov/status/1255692247061929991) to **output a value in a code snippet** without writing `console.log` over and over again.

{{% ad-panel-leaderboard %}} 

## Code Snippets (Chrome, Edge)

If you have a couple of code snippets that you use often to track what might have caused the buggy behavior, you can store and access these snippets in the “Snippets” pane. In a way, these JavaScript snippets are similar to bookmarklets, but unlike the latter, you can manage them from the convenience of a dedicated area in DevTools.

Because they are scripts, we can add breakpoints when these scripts are running, or select **portion of your code** inside “Snippets” and run that particular portion of the code instead of executing the entire snippet.

The “Snippets” pane is located among “Sources”, next to “Local Overrides”. Once you’ve added a snippet, you can run it either by right-clicking and selecting “Run”, or with <kbd>Cmd/Ctrl</kbd> + <kbd>Enter</kbd>. Of course, each snippet is available from the Command Panel as well.

In general, if you find yourself running a routine task over and over again, there is a good chance that you might want to place it in “Code Snippets” and automate this task with a script. [DevTools Snippets](https://bgrins.github.io/devtools-snippets/) includes some useful scripts for cache busting, showing headers and saving objects as .json files from the console, but you could use it to modify the DOM or display any useful information, such as performance marks (which is what we do). Plus, you could also plug in a [performance diagnostics CSS](https://gist.github.com/tkadlec/683b26344cde774170b94c0fcf0088b4) to indicate lazy-loaded images, unsized images or synchronous scripts.

## Run Custom Automated Tests (Safari)

One of the often forgotten features in Safari DevTools is the option to define and run a series of automated checks. Think of it as a **custom-built testing suite**, with a series of small tests, which can be fully defined based on the type of audit a developer would like to run. By default, the test suite is focused around accessibility, but you can adjust it as you see fit, e.g. in order to check if there are any sync scripts in the DOM, or if all of the images have a defined `width` and `height` attribute, or even if all images are lazy-loaded. (*thanks, [Nikita](https://twitter.com/dark_mefody)!*)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b1451a2-ea40-44dc-8471-0c4f703f8a99/safari-devtools-audit-panel.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b1451a2-ea40-44dc-8471-0c4f703f8a99/safari-devtools-audit-panel.png" width="800" height="" sizes="100vw" caption="Safari DevTools’ “Audit” panel, with a series of small automated tests. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b1451a2-ea40-44dc-8471-0c4f703f8a99/safari-devtools-audit-panel.png'>Large preview</a>)" alt="Safari DevTools’ “Audit” panel, with a series of small automated tests" >}}

## Source Maps (Chrome, Edge, Firefox)

When debugging production code, it’s extremely handy to be able to track down the changes to a specific component or module that you use in your code base. To map minified code to source code, we can use source maps. If you generate a source map as a part of your build, you can **use source maps while debugging your code in DevTools**.

In Chrome, you need to enable source maps for JavaScript and CSS in “Settings”, and then add a folder to “Workspace”. DevTools with then try to [infer all mappings automatically](https://developers.google.com/web/tools/chrome-devtools/javascript/source-maps) and load your source files in addition to your minified ones. You can then read and debug compiled code in its original source. Even better than that: you can still walk through your breakpoints, and all errors, logs and breakpoints will map to the actual code. To build out your source map, [Webpack’s Devtool](https://webpack.js.org/configuration/devtool/) might help.

For Firefox, once the source map is generated, a transformed file has to include a **comment that points to the source map**. Just make sure that your bundler does the job for you. Once it’s in place, in the source list pane, the original source (.scss or .ts files) will appear, and you can debug it right there.


## Clear Service Worker’s Cache And Storage (Chrome, Edge)

When we hit "Hard Refresh" in the browser, the browser will not use anything from the cache when reloading the page. Instead, it will re-fetch all assets from the server, without relying on caching.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0409bc8-7271-4bac-a452-7602200e0181/16-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0409bc8-7271-4bac-a452-7602200e0181/16-useful-devtools-tips-shortcuts.png" width="800" height="343" sizes="100vw" caption="Empty Cache and Hard Reload option in the browser, with DevTools open. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0409bc8-7271-4bac-a452-7602200e0181/16-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Empty Cache and Hard Reload option" >}}

If you right-click the “Refresh” button with DevTools open, you’ll find another option: “Empty Cache and Hard Reload”. The difference is that if the page prompts any **dynamic fetches** via JavaScript, they might still use the cache. The latter option clears them, too, while the former doesn’t.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44914245-cc04-47b3-bb6c-2a48b2bfea3c/17-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44914245-cc04-47b3-bb6c-2a48b2bfea3c/17-useful-devtools-tips-shortcuts.png" width="800" height="685" sizes="100vw" caption="Clearing site data, including service worker’s cache, cookies and all stored data at once. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44914245-cc04-47b3-bb6c-2a48b2bfea3c/17-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="“Clear site data” option" >}}

Both of these options, however, don’t clear cookie or service worker’s cache &mdash; which you might want to do in some scenarios. Jump to the Command menu (<kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>) and type/autocomplete “Clear site data”. When this option is activated, the browser will clean all of the data (as the name assumes), including the service worker’s cache as well as the unregistering of the service worker. (Alternatively, you can click “Clear Site Data” in the Application panel.)

And if you want to delete **only cache or only cookies** quickly, you can right-click on any request in the "Network" panel, and choose "Clean browser cache" from there.

In Firefox, you’ll need to head to the "Privacy &amp; Security" panel and find the "Cookies and Site Data" section there.

## Filters In The Network Panel (Chrome, Edge, Firefox)

There seems to be not much to explore in the "Network" panel as it basically just shows the list of browser requests (along with server responses) in chronological order. However, there are plenty of obscure little helpers as well.

First of all, with an overview of requests in front of us, we can **choose which columns we’d like to see**. Right-click on the header of one of the columns and select the ones that you find useful for the task at hand. We always choose the **“Priority” column** to see in which priorities assets are being requested, and if we need to adjust that order to deliver critical assets faster (based on [JavaScript Resource Loading Priorities](https://addyosmani.com/blog/script-priorities/) in Chrome, Edge).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/731143f0-8155-41cb-a292-4dcac278b2a6/18-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/731143f0-8155-41cb-a292-4dcac278b2a6/18-useful-devtools-tips-shortcuts.png" width="800" height="480" sizes="100vw" caption="There are plenty of options for filtering requests in the 'Network' panel, accessible with a prefix `-`. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/731143f0-8155-41cb-a292-4dcac278b2a6/18-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Examples of commands for filtering" >}}

We can also **filter requests** to find specific ones that might be causing trouble (*thanks for the tip, [Harry](https://twitter.com/csswizardry)*). At the top of the “Network” panel you’ll find an input field, which accepts not only keywords but also commands for filtering. Here are a few examples of the useful ones:

- `is:from-cache` shows all resources that were delivered from the cache,
- `is:service-worker-initiated`, shows only requests prompted by a service worker,
- `is:running` shows all incomplete or unresponsive requests,
- `larger-than:250k` shows all resources that are larger than 250 Kb,
- `-larger-than:250k` shows all resources that aren’t larger than 250 Kb (same size and smaller),
- `mixed-content:`shows all assets that are loaded over HTTP instead of HTTPS,
- `-has-response-header:Cache-Control` highlights assets that don’t have any caching headers,
- Obviously we can also search for bad practices like `document.write` and `@import` in HTML and CSS, plus we can use [regular expressions](https://www.freecodecamp.org/news/chrome-devtools-network-tab-tricks/) as well.

All filters can be combined as well, separated by an empty space. You can check a [comprehensive list of all filters](https://developers.google.com/web/tools/chrome-devtools/network/reference) as well, or just type `-` in the filters input and get an autocomplete preview of all features (*huge thanks to Harry for the tip!*).

## Check Initiators In The Network Panel (Chrome, Edge)

If you want to quickly check which assets a particular resource has requested, or by which resource an asset was requested, there is a simple way to discover it in DevTools as well. This is especially useful in cases where you might have a couple of **third-party scripts** that might be calling fourth-party-scripts.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/820fa96e-7dd2-4587-97f4-479166727873/19-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/820fa96e-7dd2-4587-97f4-479166727873/19-useful-devtools-tips-shortcuts.png" width="800" height="316" sizes="100vw" caption="Check the initiators by holding 'Shift' when hovering over a request. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/820fa96e-7dd2-4587-97f4-479166727873/19-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Initiators In The Network Panel" >}}

When you are inspecting a request in the “Network” panel, hold <kbd>Shift</kbd> while hovering over an element. The pink background color will indicate resources that this element has prompted to download, and the green background color will indicate the initiator that actually prompted the request.

## Choose a User Agent (Chrome, Edge, Firefox)

Sometimes you might want to check how the page will render with a different user agent, e.g. to make sure that a Googlebot gets a properly rendered version of the page. By heading to "Network conditions", you can define the behavior for caching, network throttling and a user agent.

By default, the latter is "automatic" but there are 10 predefined groups, ranging from GoogleBot Desktop and Mobile to Android and UC Browser. You can also **define your own user agent** if you need to. However, these settings will not remain preserved as you navigate from one tab to another.

In Firefox, you’ll need to head to <a href="https://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/">Firefox’s `about:config` page</a> and define a `general.useragent.override` string. 

## Change Scrolling Behavior In The Performance Panel (Chrome, Edge)

At first glance, the Performance panel might appear quite daunting with its **flame charts**, plenty of data displayed at once, and quite non-conventional scrolling behavior. By default, regular vertical scrolling acts as **zooming** into a selected portion of the timeline, but we can change it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31d84db7-a004-4a74-b4f4-6c64dbb4bbba/20-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31d84db7-a004-4a74-b4f4-6c64dbb4bbba/20-useful-devtools-tips-shortcuts.png" width="800" height="560" sizes="100vw" caption="Changing the Zooming behavior for Performance panel in Chrome’s settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31d84db7-a004-4a74-b4f4-6c64dbb4bbba/20-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="“Flamechart mouse wheel" >}}

In “Settings”, you can switch “Flamechart mouse wheel action” from “Zoom” to “Scroll” &mdash; and voilà, your preferred scrolling will be preserved! But what if you wanted to use **both zooming and scrolling** though? The key hint there is to hold “Shift” while scrolling to toggle the preferred behavior.

## Making Sense Of The Performance Panel (Chrome, Edge)

Remember “Timeline: event initiators” and “Timeline: invalidation tracking” we mentioned in the Experimental settings? These experimental features come in handy in the Performance panel when you are looking for a cause of expensive operations &mdash; so-called *Long* tasks (tasks that take over 50ms to complete). The goal then is to break down Long tasks into shorter tasks, and usually it makes sense to focus on the longest Long tasks first.

Jump to the Performance panel and start profiling with <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>E</kbd>. After a bit of time needed for refresh and collecting data, those expensive long tasks will show up in the timeline, highlighted with a red rectangle in the right upper corner. Their length indicates how expensive the operation actually is. Tasks have a **friendly budget of 50ms to finish**, which is why the first 50ms-portion of the task is displayed in solid grey. Whenever you are beyond that budget, the rest of the task is highlighted with red/grey stripes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc73c69-ff9a-4676-914c-4376db97f113/21-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc73c69-ff9a-4676-914c-4376db97f113/21-useful-devtools-tips-shortcuts.png" width="800" height="670" sizes="100vw" caption="The Performance panel can be quite daunting, but you just need to pull out the 'Summary' panel at the bottom to make sense of it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc73c69-ff9a-4676-914c-4376db97f113/21-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="“Evaluate script” option" >}}

The flame chart is a visualization of what each task consists of. All parts of a task are displayed under the actual tasks, with a yellow background representing scripting. If you click on **“Evaluate script”** under each of the tasks, you can pull up the “Summary” drawer at the bottom and see which script caused the cost. If you click on the purple bar labeled **“Recalculate style”**, DevTools will show what exactly has triggered styles invalidation.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b17fa9bc-b92b-4a59-a0fa-dc4fcf7db06f/22-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b17fa9bc-b92b-4a59-a0fa-dc4fcf7db06f/22-useful-devtools-tips-shortcuts.png" width="800" height="670" sizes="100vw" caption="If you click on purple bar labelled 'Recalculate style', DevTools will show what exactly has triggered styles invalidation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b17fa9bc-b92b-4a59-a0fa-dc4fcf7db06f/22-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Recalculate style initiator displayed in DevTools" >}}

Probably the most underrated feature in DevTools is indeed the **“Summary” drawer** which would then also show up which elements were affected by style recalculation (so you can jump to them right away) and what has initiated this task in the first place.

## Debugging Janky Animations With Layers (Chrome, Edge, Safari)

You just need a couple of animations, perhaps with a little bit of parallax, a sliding navigation or mischievous z-index manipulation, to run into **dropping frames and janky animations**. The FPS meter from the performance panel (Chrome) will reveal if you are running frames smoothly, but if it isn’t the case, you can explore rendering issues in the “Layers” tab.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e80a4e28-1ba7-4ecd-9a84-92a62dc65a87/23-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e80a4e28-1ba7-4ecd-9a84-92a62dc65a87/23-useful-devtools-tips-shortcuts.png" width="800" height="716" sizes="100vw" caption="All layers in action, with the 'Layers' tab. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e80a4e28-1ba7-4ecd-9a84-92a62dc65a87/23-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="“Layers” tab" >}}

Some of the issues can be easily detected by tracking which of the elements are missing a `will-change` property, and which ones are using a **disproportionate amount of memory**. That’s how we spotted a large component that was hidden away off the screen with relative positioning of `-1000px` off the screen, causing a couple of MB of memory usage. Also, when debugging a canvas issue, keep in mind that Safari has a [Canvas Memory Usage debugger](https://twitter.com/rikschennink/status/1356877701857083392).

## 3D View Z-Index Debugger (Edge)

Another helpful tool to track rendering issues and z-index issues is Edge’s 3D View of the DOM (“Settings” → “More tools” → 3D View). The tool provides an **interactive visualization of the DOM and z-index layers**. You can even choose to view the DOM colored with the actual background colors of the DOM elements or show only stacking contexts.

It really has never been simpler to see how `z-index` values are distributed across the page, and why overlays or panels don’t appear as expected when triggered.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b2ce54-9470-4ab3-badf-8dfb7b6a8f0d/24-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b2ce54-9470-4ab3-badf-8dfb7b6a8f0d/24-useful-devtools-tips-shortcuts.png" width="800" height="507" sizes="100vw" caption="3D visualization of the DOM in MS Edge, to track how deep and nested the DOM actually is. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b2ce54-9470-4ab3-badf-8dfb7b6a8f0d/24-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="3D View of the DOM" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba58baf0-37f4-41c7-b4c6-ead2f94c9cab/25-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba58baf0-37f4-41c7-b4c6-ead2f94c9cab/25-useful-devtools-tips-shortcuts.png" width="800" height="504" sizes="100vw" caption="3D Visualization is also useful for z-index-debugging. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba58baf0-37f4-41c7-b4c6-ead2f94c9cab/25-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="z-index values" >}}

## Better Accessibility Profiling (Chrome, Edge, Firefox)

Wouldn’t it be great to have **one-in-all accessibility tool** that would provide details and guidance about everything from tab order to ARIA-attributes and screen reader announcements? To get close to that, we’ve set up a dedicated accessibility profile with useful extensions and bookmarklets mentioned at the beginning of the article. However, DevTools provides some useful features out of the box as well.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/452005e0-5c9d-45cc-8333-e4512539af18/26-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/452005e0-5c9d-45cc-8333-e4512539af18/26-useful-devtools-tips-shortcuts.png" width="800" height="546" sizes="100vw" caption="In Chrome, Edge, when choosing a color, a little helper shows the boundary you need to cross to get to an AA/AAA grade. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/452005e0-5c9d-45cc-8333-e4512539af18/26-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="In Chrome, Edge, when choosing a color, a little helper shows the boundary you need to cross to get to an AA/AAA grade." >}}

In Chrome and Edge, the “Accessibility” panel shows the accessibility tree, used ARIA attributes and computed properties. When using a color picker, you can check and conveniently adjust the colors to accommodate for a AA/AAA-compliant contrast ratio (along with the ability to [switch between HEX, RGB, HSL](https://twitter.com/anatudor/status/1358112306203418630) with <kbd>Shift</kbd> + Click on swatch &mdash; *thanks Ana!*).

As already mentioned, the “Rendering” panel also allows you to emulate vision deficiencies. Lighthouse audits also include a section with recommendations around the accessibility of the page. Plus, when you inspect an element, accessibility information is appearing in the overview as well.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e11438-db1b-4dd5-8220-7ae192dc5cff/27-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e11438-db1b-4dd5-8220-7ae192dc5cff/27-useful-devtools-tips-shortcuts.png" width="800" height="595" sizes="100vw" caption="The Inspect Mode tooltip with accessibility information. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14e11438-db1b-4dd5-8220-7ae192dc5cff/27-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="The Inspect Mode tooltip with accessibility information." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e188c28-dac5-438e-8372-4abb286e878b/28-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e188c28-dac5-438e-8372-4abb286e878b/28-useful-devtools-tips-shortcuts.png" width="800" height="537" sizes="100vw" caption="Advanced accessibility tooling in Firefox, with accessibility checks and recommendations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e188c28-dac5-438e-8372-4abb286e878b/28-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Advanced accessibility tooling in Firefox, with accessibility checks and recommendations." >}}

Firefox has advanced accessibility tooling as well. Additionally to the accessibility tree and contrast checker, Firefox DevTools highlights roles and landmarks, along with **accessibility recommendations and checks**. For example, you can check for contrast issues on the entire page, check if all links are focusable and include focus styling, and review text labels. Plus, you can toggle tabbing order as well.  

Additionally, you can install accessibility-focused extensions such as [Accessibility Insights](https://accessibilityinsights.io/), [aXe](https://www.deque.com/axe/) and [a11y.css](https://github.com/ffoodd/a11y.css), along with a few other [accessibility linters](https://twitter.com/alexanderadam__/status/1274982660666986496) and color vision simulators.

## Worth Mentioning

Obviously, there are literally hundreds, and perhaps even thousands, of other useful features available in DevTools. Many of them are quite well-known and don’t need much introduction, but are still worth mentioning.

- **CSS Grid / Flexbox Inspectors** (Firefox, Chrome, Edge)    
If you have *any* layout issue related to Grid and Flexbox, you’ll probably find a cause of the problem via DevTools. Grid and Flexbox inspectors are very useful as they show grid overlay and the boundaries of containers, as well as hints on everything from `flex-basis` to `grid-gap`. 
    
- **Live Expressions**    
If you’ve been running into habit of typing the same JavaScript expression in the console, you could look into automating it with Live Expressions. The feature, available in Chrome, Edge and Firefox, allows you to type an expression once and then pin it to the top of your console, and the value of the live expression will update automatically.

- **Animations Panel**    
Firefox has a very handy panel to track issues with animations, including slowing it down and visualizing how an element is changing over time. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f81326-2be1-41ad-b2f6-30c5c5e12dd8/29-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f81326-2be1-41ad-b2f6-30c5c5e12dd8/29-useful-devtools-tips-shortcuts.png" width="800" height="651" sizes="100vw" caption="The Animations panel gives insight into animations, and allows you to replay them in slow motion. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f81326-2be1-41ad-b2f6-30c5c5e12dd8/29-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Animations Panel" >}}

- **Fonts Panel**    
Firefox also has a handy “Fonts” panel that’s worth exploring for any kind of font-related issue. We used it quite a lot when trying to match the fallback font against the web font, for example, as you can refine typographic properties with a slider and see impact in action. It also provides text previews when hovering over a font-family in styles.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c504b40-cd2a-418d-a265-0d42f3d0946a/30-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c504b40-cd2a-418d-a265-0d42f3d0946a/30-useful-devtools-tips-shortcuts.png" width="800" height="711" sizes="100vw" caption="The Fonts panel in Firefox with a few controls to adjust typographic settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c504b40-cd2a-418d-a265-0d42f3d0946a/30-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="Fonts Panel" >}}

- **CSS Overview**  
If you activate the “CSS Overview” in Chrome’s experimental settings, DevTools will add a tab with a comprehensive report of CSS declarations used on a page. It will also list all colors and fonts used, as well as media queries and unused declarations which you can jump to right away.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bf35fc7-aaa9-43d5-8bb2-a1be4b493b0c/31-useful-devtools-tips-shortcuts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bf35fc7-aaa9-43d5-8bb2-a1be4b493b0c/31-useful-devtools-tips-shortcuts.png" width="800" height="544" sizes="100vw" caption="CSS Overview provides a thorough summary of CSS found on the page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bf35fc7-aaa9-43d5-8bb2-a1be4b493b0c/31-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="CSS Overview" >}}

## And That’s A Wrap!

When we set out to prepare this overview, it was supposed to be quite short, featuring just some of the useful features that DevTools provides. It turned out that there are plenty of features that we didn’t know of before we started writing this article &mdash; and we were able to stumble upon them with the kind help of wonderful Smashing readers who contributes their experiences on Twitter. Thank you so much for your kind contributions!

Also, a huge *thank-you* to *all* contributors of *all* DevTools across *all* browsers &mdash; we applaud you for your efforts, and your time and effort to make our development experiences better. It matters.

**If we missed something valuable**, please reply in the comments. And if you found something useful, we hope you’ll be able to apply these little helpers to your workflow right away, and perhaps send a link to this post to a friend or two &mdash; perhaps they’ll find it useful. Ah, and don’t forget: you could also debug DevTools with DevTools &mdash; just hit <kbd>Cmd/Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd> twice in a row. ;-)

Now, happy debugging, everyone!

{{< signature "yk, il" >}}
