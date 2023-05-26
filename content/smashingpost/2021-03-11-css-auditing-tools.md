---
title: 'CSS Auditing Tools'
slug: css-auditing-tools
author: iris-ljesnjanin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/128fa8b4-643a-45f2-a37b-aabd7fececf1/4-complexity.png
date: 2021-03-11T13:40:00.000Z
summary: >-
  In a new short series of posts, we highlight some of the useful tools and techniques for developers and designers to get their work done better and faster. Starting out with a few tools for getting to the bottom of CSS.
description: >-
  A complete guide to CSS auditing tools for debugging and refactoring your CSS. Tools to discover CSS specificity issues, duplicated and invalid selectors and improve your CSS architecture.
categories:
  - Tools
  - Techniques
  - CSS
  - Debugging
  - Generators
  - Round-Ups
disable_ads: true
last_updated: 2021-06-24T12:20:00.000Z
---

How large is your CSS? How repetitive is it? What about your CSS specificity score? Can you safely remove some declarations and vendor prefixes, and if so, how do you spot them quickly? Over the last few weeks, we’ve been working on refactoring and cleaning up our CSS, and as a result, we stumbled upon a couple of useful tools that helped us identify duplicates. So let’s review some of them.

{{< refs >}}
    <h4 style="margin-top: 1.25em">More On CSS:</h4>
    <ul>
    <li><a href="https://www.smashingmagazine.com/2021/03/css-generators/">CSS Generators</a>
    <li><a href="https://www.smashingmagazine.com/guides/css-layout/">Comprehensive Guide To CSS Layout</a>
    <li><a href="https://www.smashingmagazine.com/2021/02/css-z-index-large-projects/">Managing CSS Z-Index</a></li>
    <li><a href="https://www.smashingmagazine.com/2019/03/css-alignment/">How To Align Things In CSS</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/things-you-can-do-with-css-today/">Things You Can Do With CSS Today</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/02/useful-chrome-firefox-devtools-tips-shortcuts/">Useful DevTools Tips and Shortcuts</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>
{{< /refs >}}


## CSS Stats

[CSS Stats](https://cssstats.com/) runs a  thorough audit of the CSS files requested on a page. Like many similar tools, it provides a dashboard-alike view of rules, selectors, declarations and properties, along with pseudo-classes and pseudo-elements. It also **breaks down all styles into groups**, from layout and structure to spacing, typography, font stacks and colors.

{{< rimg breakout="true" href="https://cssstats.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a08575e-e863-4963-bffa-3df841ee074c/specificity-graph.png" width="700" height="513" sizes="100vw" caption="Specificity scores, built with <a href='https://cssstats.com/'>CSS Stats</a>. Lower scores and flatter curves are better for maintainability. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a08575e-e863-4963-bffa-3df841ee074c/specificity-graph.png'>Large preview</a>)" alt="A screengrab of Base 10 specificity score for each selector by source order" >}}

One of the useful features that CSS Stats provides is the **CSS specificity score**, showing how unnecessarily specific some of the selectors are. Lower scores and flatter curves are better for maintainability.

{{< rimg breakout="true" href="https://cssstats.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e455a16-1c4f-4585-93a3-632793436122/colors-used.png" width="700" height="513" sizes="100vw" caption="An overview of colors used, printed by declaration order in source code, with <a href='https://cssstats.com/'>CSS Stats</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e455a16-1c4f-4585-93a3-632793436122/colors-used.png'>Large preview</a>)" alt="An overview of colors used, printed by declaration order in source code." >}}

It also includes an overview of colors used, printed by declaration order, and a score for **Total vs. Unique declarations**, along with the comparison charts that can help you identify which properties might be the best candidates for creating abstractions. That’s a great start to understand where the main problems in your CSS lie, and what to focus on.

{{% feature-panel %}}

## Yellow Lab Tools

[Yellow Lab Tools](https://yellowlab.tools/), is a free tool for auditing web performance, but it also includes some very helpful helpers for **measure the complexity of your CSS** &mdash; and also provides actionable insights into how to resolve these issues.

{{< rimg breakout="true" href="https://yellowlab.tools/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b61a4ee5-44c8-44fb-8c15-f7ae6ed88f08/2-css-complexity-bad-css.png" width="800" height="357" sizes="100vw" caption="<a href='https://yellowlab.tools/'>Yellow Lab Tools</a> highlights plenty of CSS issue, along with actionable recommendations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b61a4ee5-44c8-44fb-8c15-f7ae6ed88f08/2-css-complexity-bad-css.png'>Large preview</a>)" alt="Two tables showing CSS complexity and bad CSS." >}}

The tool highlights **duplicated selectors and properties**, old IE fixes, old vendor prefixes and redundant selectors, along with complex selectors and syntax errors. Obviously, you can dive deep into each of the sections and study which selectors or rules specifically are overwritten or repeated. That’s a great option to discover some of the low-hanging fruits and resolve them quickly.

{{< rimg breakout="true" href="https://yellowlab.tools/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e893b895-2cf2-4f18-a083-6dc1b787dbeb/3-duplicated-selectors.png" width="800" height="385" sizes="100vw" caption="<a href='https://yellowlab.tools/'>Yellow Lab Tools</a> also shows duplicated selectors and how often they are duplicated, so you can check them immediately. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e893b895-2cf2-4f18-a083-6dc1b787dbeb/3-duplicated-selectors.png'>Large preview</a>)" alt="A list of duplicated selectors" >}}

We can go a bit deeper though. Once you tap into the overview of old vendor prefixes, you can not only check the offenders but also **which browsers** these prefixes are accommodating for. Then you can head to your [Browserslist configuration](https://github.com/browserslist/browserslist) to double-check if you aren’t serving too many vendor prefixes, and test your configuration on [Browsersl.ist](https://browserl.ist/) or via Terminal.

## CSS Specificity Visualizer

[CSS Specificity Visualizer](https://isellsoap.github.io/specificity-visualizer/) provides an overview of CSS selectors and their specificities across a CSS file. Once you submit a stylesheet, the tool returns a specificity graph. The x-axis shows the physical location of selectors in the CSS, laid out from left to right, with the first one on the left, and the last one on the right. The y-axis shows the actual **specificity of selectors**, starting with the least specific at the bottom and ending with the most specific at the top.

{{< rimg breakout="true" href="https://isellsoap.github.io/specificity-visualizer/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8859e3e-37a4-4db8-9426-a81bf7622408/specificity-graph.png" width="800" height="385" sizes="100vw" caption="<a href='https://isellsoap.github.io/specificity-visualizer/'>Specificity Visualizer</a> provides a visual way to analyze the specificity of CSS selectors in your stylesheets. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8859e3e-37a4-4db8-9426-a81bf7622408/specificity-graph.png'>Large preview</a>)" alt="A visual way to analyze the specificity of CSS selectors in your stylesheets" >}}

In general, **high specificity is usually a red flag**, so watch out for a spiky graph and high amount of noise. On the other hand, an upward-trending graph with overall low specificity and low amount of noise can be considered “good”. You can also hover over single data points to see the exact selector or zoom into areas of interest.
## Project Wallace

Unlike other tools, [Project Wallace](https://www.projectwallace.com/), created by Bart Veneman, additionally keeps the history of your CSS over time. You can use webhooks to [automatically analyze CSS on every push](https://www.projectwallace.com/blog/automatically-analyze-css-on-every-push/) in your CI. The tool tracks the state of your CSS over time by looking into specific CSS-related metrics such as **average selector per rule**, maximum selectors per rule and declarations per rule, along with a general overview of CSS complexity.

{{< rimg breakout="true" href="https://www.projectwallace.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/128fa8b4-643a-45f2-a37b-aabd7fececf1/4-complexity.png" width="800" height="493" sizes="100vw" caption="<a href='https://www.projectwallace.com/'>Wallace</a> provides a thorough dashaboard on the complexity of your CSS, along with a few custom metrics. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/128fa8b4-643a-45f2-a37b-aabd7fececf1/4-complexity.png'>Large preview</a>)" alt="Source lines of code showing 19,894 alongside total rules, average selectors per rule, declarations per rule, supports and supports hacks" >}}

## Parker

Katie Fenn’s [Parker](https://github.com/katiefenn/parker) is a command-line stylesheet analysis tool that runs metrics on your stylesheets and reports on their complexity. It runs on Node.js, and, unlike CSS Stats, you can run it to measure your local files, e.g. as a part of your build process.

## DevTools CSS Auditing

Of course, we can also use DevTools’ [CSS overview](https://umaar.com/dev-tips/209-css-overview/) panel. (You can enable it in the “Experimental Settings”). Once you capture a page, it provides an overview of media queries, colors and font declarations, but also highlights **unused declarations** which you can safely remove.

Also, [CSS coverage](https://developers.google.com/web/tools/chrome-devtools/coverage) returns an overview of unused CSS on a page. You could even go a bit further and [bulk find unused CSS/JS with Puppeteer](https://willmanntobias.medium.com/how-to-bulk-find-unused-css-and-javascript-with-puppeteer-and-chrome-coverage-f79f7d885d59).

{{< rimg breakout="true" href="https://developers.google.com/web/tools/chrome-devtools/coverage" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75a1874-f431-44e9-87a3-993593580ded/06-useful-devtools-tips-shortcuts.png" width="800" height="546" sizes="100vw" caption="Exploring the amount of used and unused CSS and JavaScript, with Code Coverage. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75a1874-f431-44e9-87a3-993593580ded/06-useful-devtools-tips-shortcuts.png'>Large preview</a>)" alt="The Code coverage panel" >}}

With “Code coverage” in place, going through a couple of scenarios that include a lot of tapping, tabbing and window resizing, we also [export coverage data](https://twitter.com/chromedevtools/status/1286663677240737793) that DevTools collects as JSON (via the export/download icon). On top of that, you could use Puppeteer that also provides an [API to collect coverage](https://pptr.dev/#?product=Puppeteer&show=api-class-coverage).

We’ve highlighted some of the details, and a few further **DevTools tips in Chrome**, Firefox, and Edge in [Useful DevTools Tips And Shortcuts](https://www.smashingmagazine.com/2021/02/useful-chrome-firefox-devtools-tips-shortcuts/) here on Smashing Magazine.

## Style Check

How do you usually check the effect of your CSS on HTML elements? Directly in your project or do you have a dedicated test HTML file that includes all HTML elements you’re using to see all the styling at a glance? Austin Gill created a little tool that takes a similar approach: [Style Check](https://style-check.austingil.com/). The benefit: You won’t need to set up a test HTML file yourself, the tool does it for you.

{{< rimg href="https://style-check.austingil.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/635b59f5-e615-4ba6-be9e-2ba520666bf9/stylecheck-opt.png" width="800" height="467" sizes="100vw" caption="Check the effect of your styling on HTML elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/635b59f5-e615-4ba6-be9e-2ba520666bf9/stylecheck-opt.png'>Large preview</a>)" alt="Style Check" >}}

Just upload your *.css* file to Style Check to audit its effect on plain HTML elements. You can also select a library (Bedrocss, Bootstrap, Eric Meyer’s CSS Reset, and Normalize.css are available) or enter inline styles. The elements range from headings and paragraphs to media, lists, and tables, buttons, forms, as well as other kinds of input, and details such as sub- and superscript, code, quotes, and much more. A handy little helper.

## What Tools Are You Using?

Ideally, a CSS auditing tool would provide some insights about how heavily CSS implact rendering performance, and which operations lead to **expensive layout recalculations**. It could also highlight what properties don’t affect the rendering at all (like Firefox DevTools does it), and perhaps even suggest how to write [slightly more efficient CSS selectors](https://csswizardry.com/2011/09/writing-efficient-css-selectors/).

These are just a few tools that we’ve discovered — we’d love to hear your stories and your tools that work well to identify the bottlenecks and fix CSS issues faster. Please **leave a comment** and share your story in the comments!

You can also <a href="/the-smashing-newsletter/">subscribe to our friendly email newsletter</a> to not miss next posts like this one. And, of course, happy CSS auditing and debugging!

{{< signature "vf, il" >}}