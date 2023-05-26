---
title: 'A Guide To New And Experimental CSS DevTools In Firefox'
slug: guide-new-experimental-css-devtools-firefox
author: victoria-wang
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08344d1d-3013-4a44-8567-37afcd12f50f/guide-new-experimental-css-devtools-firefox.png
date: 2019-10-10T14:30:59+02:00
summary: >-
  Ever since releasing Grid Inspector, the Firefox DevTools team has been inspired to build a new suite of tools to solve the problems of the modern web. In this article, we’ll learn about all 7 tools and take a peek at potential future projects.
description: >-
  Ever since releasing Grid Inspector, the Firefox DevTools team has been inspired to build a new suite of tools to solve the problems of the modern web. In this article, we’ll learn about all 7 tools and take a peek at potential future projects.
categories:
  - CSS
  - Browsers
  - DevTools
  - Tools
  - Debugging
disable_newsletterbox: true
---
Over the last few years, our team at Firefox has been working on new CSS tools that address both cutting-edge techniques and age-old frustrations. We’re the Layout Tools team, a subset of Firefox Developer Tools, and our quest is to improve the modern web design workflow.

The web has seen an incredible evolution in the last decade: new HTML/CSS features, browser improvements, and design techniques. Our team is devoted to building tools that match that innovation so that designers and developers can harness more of the efficiency and creativity that’s now possible.

In this guide, we’ll share an overview of our seven new tools, with stories from the design process and practical steps for trying out each tool.


<div class="c-felix-the-cat">
<h4 class="h3">Editorial Design Patterns</h4>
<p>By naming lines when setting up our CSS Grid layouts, we can tap into some interesting and useful features of Grid — features that become even more powerful when we introduce subgrids. <a href="https://www.smashingmagazine.com/2019/10/editorial-design-patterns-css-grid-subgrid-naming/" class="btn btn--small btn--white btn--white--bordered">Read related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## 1. Grid Inspector

It all started three years ago when our CSS layout expert and dev advocate, [Jen Simmons](https://jensimmons.com/), worked with members of Firefox DevTools to build a tool that would aid users in [examining CSS Grid layouts](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_grid_layouts ).

As one of the most powerful new features of the modern web, [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/grid) had quickly gained decent browser adoption, but it still had low website adoption. There’s a steep learning curve, and you still need fallbacks for certain browsers. Thus, part of our goal was to help popularize Grid by giving developers a more hands-on way to learn it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ba92694-fce0-4a57-a4a6-7912f78b1cec/guide-firefox-new-css-tools-grid-inspector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ba92694-fce0-4a57-a4a6-7912f78b1cec/guide-firefox-new-css-tools-grid-inspector.png" sizes="100vw" caption="Grid Inspector (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ba92694-fce0-4a57-a4a6-7912f78b1cec/guide-firefox-new-css-tools-grid-inspector.png'>Large preview</a>)" alt="An example of the Grid Inspector displaying an outline of the grid layout" >}}

The core of the tool is a grid outline, overlaid on the page, which helps devs visualize how the grid is positioning their elements, and how the layout changes when they tweak their styles. We added numbered labels to identify each grid line, the ability to view up to three grids at once, and color customization for the overlays. Recently, we also added support for [subgrid](https://hacks.mozilla.org/2019/06/css-grid-level-2-subgrid-is-coming-to-firefox/), a brand new CSS specification implemented in Firefox and hopefully in more browsers soon.

Grid Inspector was an inspiration for all the tools that followed. It was even an inspiration for a new team: Layout Tools! Formed in late 2017, we’re spread across four time zones and collaborate with many others in Mozilla, like our rendering engine developers and the good folks at [MDN](https://developer.mozilla.org/).

### Try Out The Grid Inspector

<ol>
    <li>In Firefox, visit our <a href="https://www.mozilla.org/en-US/developer/css-grid/">Grid example site</a>.</li>
    <li>Open the Inspector with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd>.</li>
    <li>Turn on Grid overlay via one of three ways:</li>
    <ul>
        <li><strong>Layout Panel</strong>:<br />In the Grid section, check the checkbox next to <code>.content.grid-content</code>;</li>
        <li><strong>Markup View</strong>:<br />Toggle the “grid” badge next to <code>&lt;div class="content grid-content"&gt;</code>;</li>
        <li><strong>Rules View</strong>:<br />Click the {{< inline-icon src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b451bc-ddb1-4a67-b243-b19e9c6b24f2/gridicon.png" >}} button next to <code>display:grid;</code> inside <code>#page-intro .grid-content</code>;</li>
    </ul>
    <li>Experiment with the Grid Inspector:</li>
    <ul>
        <li>Change the purple overlay color to red;</li>
        <li>Toggle “Line numbers” or “Extend lines infinitely”;</li>
        <li>Turn on more grid overlays;</li>
        <li>See what happens when you disable <code>grid-gap: 15px</code> in Rules.</li>
    </ul>
</ol>

{{% pull-quote %}}
 Since Grid, we’ve been seeking to expand on the possibilities of what a browser CSS tool can be.
{{% /pull-quote %}}

## 2. Shape Path Editor

The next project we worked on was the [Shape Path Editor](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Edit_CSS_shapes): our first visual editing tool.

{{< vimeo id="365133763" >}}

[CSS Shapes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes) allows you to define shapes for text to flow around: a circle, a triangle, or a many-sided polygon. It can be used with the `clip-path` property which allows you to trim elements to any of those same shapes. These two techniques together open the possibility for some very unique graphic design-inspired layouts.

However, creating these sometimes complex shapes can be difficult. Typing all of the coordinates manually and using the right CSS units is error-prone and far removed from the creative mindset that Shapes allows. Therefore, we made a tool that allows you to edit your code by directly clicking and dragging shapes on the page.

This type of feature—visual editing—was new for us and browser tools in general. It’s an example of how we can go beyond inspecting and debugging and into the realm of design.

### Try Out The Shape Path Editor

1. In Firefox, visit [this page](https://aneventapart.com/who-attends) on the An Event Apart website.
2. Open the Inspector with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> and select the first circular image.
3. In Rules, click on the {{< inline-icon src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfef4ac3-5d78-45b8-abe9-774ffc885818/shapesicon.png" >}} icon next to the `shape-outside` property.
4. On the page, click on the points of the shape and see what happens when you drag to make the shape huge or tiny. Change it to a size that looks good to you.

{{% pull-quote %}}
 Visual editing is an example of how we can go beyond inspecting and debugging and into the realm of design.
{{% /pull-quote %}}

## 3. Fonts Editor

For years, we’ve had a Fonts panel in Firefox that shows an informative list of all the fonts used in a website. In continuing our theme of designing in the browser, we decided to turn this into a Font Editor for fine-tuning a font’s properties.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce68cc41-ae3c-4263-b2ac-3f142f383351/guide-firefox-new-css-tools-fonts-editor.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce68cc41-ae3c-4263-b2ac-3f142f383351/guide-firefox-new-css-tools-fonts-editor.png" sizes="100vw" caption="Fonts Editor (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce68cc41-ae3c-4263-b2ac-3f142f383351/guide-firefox-new-css-tools-fonts-editor.png'>Large preview</a>)" alt="An example of the Fonts Editor index of fonts and variable fonts editing" >}}

A driving force behind this project was our goal to support [Variable Fonts](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/Variable_Fonts_Guide) at the same time that the Firefox rendering engine team was adding support for it. Variable Fonts gives font designers a way to offer fine-grained variations along axes, like weight, within one font file. It also supports custom axes, which give both font creators and web designers an amazing amount of flexibility. Our tool automatically detects these custom axes and gives you a way to adjust and visualize them. This would otherwise require specialized websites like [Axis-Praxis](https://www.axis-praxis.org/specimens/decovar).

Additionally, we added a feature that provides the ability to hover over a font name to highlight where that particular font is being used on the page. This is helpful because the way browsers select the font used to render a piece of text can be complex and depend on one’s computer. Some characters may be unexpectedly swapped out for a different font due to [font subsetting](https://www.bramstein.com/writing/web-font-anti-patterns-subsetting.html).

### Try Out The Fonts Editor

<ol>
    <li>In Firefox, visit this <a href="https://zeichenschatz.net/demos/vf/variable-web-typo/">variable fonts demo site</a>.</li>
    <li>Open the Inspector with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> and select the word “variable” in the title (the element’s selector is <code>.title__variable-web__variable</code>).</li>
    <li>In the third pane of the Inspector, navigate to the Fonts panel:</li>
    <ul>
        <li>Hover over the font name <strong>Output Sans Regular</strong> to see what gets highlighted;</li>
        <li>Try out the <strong>weight</strong> and <strong>slant</strong> sliders;</li>
        <li>Take a look at the preset font variations in the <strong>Instances</strong> dropdown menu.</li>
    </ul>
</ol>

{{% ad-panel-leaderboard %}}

## 4. Flexbox Inspector

Our Grid, Shapes, and Variable Fonts tools can together power some very advanced graphic design on the web, but they’re still somewhat cutting-edge based on browser support. ([They’re](https://caniuse.com/#feat=css-grid) [almost](https://caniuse.com/#feat=css-shapes) [there](https://caniuse.com/#feat=variable-fonts), but still require fallbacks.) We didn’t want to work only on new features—we were drawn to the problems that most web developers face on a daily basis.

So we started work on the [Flexbox Inspector](https://hacks.mozilla.org/2019/01/firefox-65-webp-flexbox-inspector-new-tooling/). Design-wise, this has been our most ambitious project, and it sprouted some new user research strategies for our team.

Like Grid, [CSS Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout) has a fairly steep learning curve when you first get started. It takes time to really understand it, and many of us resort to trial and error to achieve the layouts we want. At the beginning of the project, our team wasn’t even sure if we understood Flexbox ourselves, and we didn’t know what the main challenges were. So we leveled up our understanding, and we ran a survey to discover what people needed the most when it came to Flexbox.

The results had a big effect on our plans, making the case for complicated visualizations like grow/shrink and min/max. We continued working with the community throughout the project by incorporating feedback into evolving [visual prototypes](https://discourse.mozilla.org/t/flexbox-inspector-input-wanted/30611) and Nightly builds.

The tool includes two major parts: a highlighter that works much like the Grid Inspector’s, and a detailed Flexbox tool inside the Inspector. The core of the tool is a flex item diagram with sizing info.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/360fa04d-7bc6-4a2c-a3b3-0ec3d6d5bfe6/guide-firefox-new-css-tools-flexbox-inspector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/360fa04d-7bc6-4a2c-a3b3-0ec3d6d5bfe6/guide-firefox-new-css-tools-flexbox-inspector.png" sizes="100vw" caption="Flex item diagram and sizing (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/360fa04d-7bc6-4a2c-a3b3-0ec3d6d5bfe6/guide-firefox-new-css-tools-flexbox-inspector.png'>Large preview</a>)" alt="An example of the flex item diagram and sizing table" >}}

With help from Gecko layout engineers, we were able to show the step-by-step size decisions of the rendering engine to give users a full picture of why and how a flex item ended up with a certain size.

**Note**: *Learn the full story of our design process in “[Designing the Flexbox Inspector](https://hacks.mozilla.org/2019/01/designing-the-flexbox-inspector/)”.*

### Try Out The Flexbox Inspector

<ol>
    <li>In Firefox, visit Mozilla’s <a href="https://bugzilla.mozilla.org/">Bugzilla</a>.</li>
    <li>Open the Inspector with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> and select the element <code>div.inner</code> (just inside the header bar).</li>
    <li>Turn on the Flexbox overlay via one of three ways:</li>
    <ul>
        <li><strong>Layout Panel</strong>:<br />In the Flex Container section, turn on the switch;</li>
        <li><strong>Markup View</strong>:<br />Toggle the “flex” badge next to <code>&lt;div class="inner"&gt;</code>;</li>
        <li><strong>Rules View</strong>:<br />Click the {{< inline-icon src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ae65a78-3762-45e6-8c9c-870893218629/flexicon.png" >}} button next to <code>display:flex</code>.</li>
    </ul>
    <li>Use the Flex Container panel to navigate to a Flex Item called <code>nav#header-nav</code>.</li>
    <ul>
        <li>Note the sizes shown in the diagram and size chart;</li>
        <li>Increase and decrease your browser’s width and see how the diagram changes.</li>
    </ul>
</ol>

## Interlude: Doubling Down on Research

As a small team with no formal user research support, we’ve often resorted to design-by-dogfooding: basing our opinions on our own experiences in using the tools. But after our success with the Flexbox survey, we knew we wanted to be better at collecting data to guide us. We ran a [new survey](https://hacks.mozilla.org/2018/11/new-experimental-web-design-tools-feedback-requested/) to help inform our next steps.

We crowdsourced a list of the 20 biggest challenges faced by web devs and asked our community to rank them using a max-diff format.

When we found that the big winner of the challenges was CSS Layout Debugging, we ran a [follow-up survey](https://hacks.mozilla.org/2019/02/web-design-challenges-survey-finding/) on specific CSS bugs to discover the biggest pain points. We supplemented these surveys with user interviews and user testing.

We also asked folks to rank their frustrations with browser developer tools. The clear top issue was moving CSS changes back to the editor. This became our next project.

## 5. Changes Panel

The difficulty in transferring one’s work from a browser developer tool to the editor is one of those age-old issues that we all just got used to. We were excited to make a simple and immediately usable solution.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4056e9e7-5f22-4f4f-8b91-e1ea6dc71b68/guide-firefox-new-css-tools-changes-panel.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4056e9e7-5f22-4f4f-8b91-e1ea6dc71b68/guide-firefox-new-css-tools-changes-panel.png" sizes="100vw" caption="Changes Panel (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4056e9e7-5f22-4f4f-8b91-e1ea6dc71b68/guide-firefox-new-css-tools-changes-panel.png'>Large preview</a>)" alt="An example of the diff view provided by the Changes Panel" >}}

Edge and Chrome DevTools came out with variants of this tool first. Ours is focused on assisting a wide range of CSS workflows: Launch DevTools, change any styles you want, and then export your changes by either copying the full set of changes (for collaboration) or just one changed rule (for pasting into code).

This improves the robustness of the entire workflow, including our other layout tools. And this is just a start: We know accidental refreshing and navigation from the page is a big source of data loss, so a way to bring persistence to the tool will be an important next step.

### Try Out The Changes Panel

<ol>
    <li>In Firefox, navigate to any website.</li>
    <li>Open the Inspector with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> and select an element.</li>
    <li>Make some changes to the CSS:</li>
    <ul>
        <li>Modify styles in the Rules pane;</li>
        <li>Adjust fonts in the Fonts pane.</li>
    </ul>
    <li>In the right pane of the Inspector, navigate to the Changes tab and do the following:</li>
    <ul>
        <li>Click <strong>Copy All Changes</strong>, then paste it in a text editor to view the output;</li>
        <li>Hover over the selector name and click <strong>Copy Rule</strong>, then paste it to view the output.</li>
    </ul>
</ol>

{{% ad-panel-leaderboard %}}

## 6. Inactive CSS

Our Inactive CSS feature solves one of the top issues from our layout debugging survey on specific CSS bugs:

<blockquote>“Why is this CSS property not doing anything?”</blockquote>

Design-wise, this feature is very simple—it grays out CSS that doesn’t affect the page, and shows a tooltip to explain why the property doesn’t have an effect. But we know this can boost efficiency and cut down on frustration. We were bolstered by [research](https://users.eecs.northwestern.edu/~hq/papers/ply.pdf) from Sarah Lim and her colleagues who built a similar tool. In their studies, they found that novice developers were 50% faster at building with CSS when they used a tool that allowed them to ignore irrelevant code.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e6c73d1-cc10-49cb-ad56-06b55c9ad148/guide-firefox-new-css-tools-inactive-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e6c73d1-cc10-49cb-ad56-06b55c9ad148/guide-firefox-new-css-tools-inactive-css.png" sizes="100vw" caption="Inactive CSS tooltip (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e6c73d1-cc10-49cb-ad56-06b55c9ad148/guide-firefox-new-css-tools-inactive-css.png'>Large preview</a>)" alt="An example of an inactive CSS tooltip warning" >}}

In a way, this is our favorite kind of feature: A low-hanging UX fruit that barely registers as a feature, but improves the whole workflow without really needing to be discovered or learned.

Inactive CSS launches in Firefox 70 but can be used now in prerelease versions of Firefox, including Developer Edition, Beta, and Nightly.

### Try Out Inactive CSS

1. Download [Firefox Developer Edition](https://www.mozilla.org/firefox/developer/);
2. Open Firefox and navigate to [wikipedia.org](https://www.wikipedia.org/);
3. Open the Inspector with <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> and select the center content area, called `central-featured`;
4. Note the grayed out `vertical-align` declaration;
5. Hover over the info icon, and click “Learn more” if you’re interested.

## 7. Accessibility Panel

Along the way we’ve had accessibility features developed by a separate team that’s mostly one person &mdash; [Yura Zenevich](https://twitter.com/yura_zen/), this year with his intern [Maliha Islam](https://twitter.com/malihaiiislam).

Together they've turned the new Accessibility panel in Firefox into a powerful inspection and auditing tool. Besides displaying the accessibility tree and properties, you can now run different types of checks on a page. So far the checks include color contrast, text labels, and keyboard focus styling.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50a2df42-0543-416a-ae6d-73a1a71c92db/guide-firefox-new-css-tools-accessibility.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50a2df42-0543-416a-ae6d-73a1a71c92db/guide-firefox-new-css-tools-accessibility.png" sizes="100vw" caption="Auditing in the Accessibility Panel (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50a2df42-0543-416a-ae6d-73a1a71c92db/guide-firefox-new-css-tools-accessibility.png'>Large preview</a>)" alt="An example of the Accessibility Panel’s auditing feature" >}}

Now in Nightly, you can try the new [color blindness simulator](https://developer.mozilla.org/en-US/docs/Tools/Accessibility_inspector/Simulation) which harnesses our upcoming [WebRender](https://www.ghacks.net/2019/05/20/firefox-webrender-rollout-begins-with-the-release-of-firefox-67/) tech.

### Try Out The Accessibility Panel

1. Download [Firefox Developer Edition](https://www.mozilla.org/firefox/developer/);
2. Navigate to [meetup.com](https://meetup.com);
3. In the developer tools, navigate to the Accessibility tab, and click the “Turn on Accessibility Features” button;
4. Click the drop-down menu next to “Check for issues” and select “All Issues”;
5. Take a look at the various contrast, keyboard, and text label issues, and click the “Learn more” links if you’re interested.

## Next Up

We’re currently hard at work on a browser compatibility tool that uses information from MDN to show browser-specific issues for a selected element. You can follow along on [GitHub](https://github.com/firefox-devtools/ux/issues/65) to learn more.

## The Future

We’re committed to supporting the modern web, and that means continuously changing and growing.

New specifications get implemented by browser vendors all the time. Guidelines and best practices around progressive enhancement, responsiveness, and accessibility evolve constantly. Us tool makers need to keep evolving too.

And what of the long-lived, ever-present problems in creating the web? What everyday user interfaces need to be rethought? These are some of the questions that keep us going!

What about a better way to navigate the DOM tree of a page? That part of DevTools has gone essentially unchanged since the Firebug days.

We've been experimenting with features like back and forward buttons that would ease navigation between recently visited elements.

A more dramatic change we’re discussing is adding a compact DOM view that uses a syntax similar to HTML templating engines. The focus would be on the most common use case—navigating to CSS—rather than viewing/editing the source.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1d5987-b5fd-43f9-b6b7-04db4d8bb65d/guide-firefox-new-css-tools-html-outline.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1d5987-b5fd-43f9-b6b7-04db4d8bb65d/guide-firefox-new-css-tools-html-outline.png" sizes="100vw" caption="HTML Outline View (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1d5987-b5fd-43f9-b6b7-04db4d8bb65d/guide-firefox-new-css-tools-html-outline.png'>Large preview</a>)" alt="A mockup of the simplified HTML Outline View" >}}

We've also been thinking about a better element selector. We know how it can be more productive to work inside the page, with less jumping back and forth into DevTools. We could make the element selector more powerful and more persistent. Perhaps it could select whitespace on a page and tell you what causes that space, or it could shed light on the relationships between different elements.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5c8e2a-f8b8-4ca7-b091-f86519823fd9/guide-firefox-new-css-tools-visual-picker.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5c8e2a-f8b8-4ca7-b091-f86519823fd9/guide-firefox-new-css-tools-visual-picker.png" sizes="100vw" caption="Visual Element Selector (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5c8e2a-f8b8-4ca7-b091-f86519823fd9/guide-firefox-new-css-tools-visual-picker.png'>Large preview</a>)" alt="A mockup of element overlay with collapsed margin" >}}

These are just two of the many ideas we hope to explore further with the help of the community.

## We Need Your Input!

We want to keep making awesome tools that make your life easier as a developer or designer.

Here’s an easy way to help: Download [Firefox Developer Edition](https://www.mozilla.org/firefox/developer/) and try using it for some of your work next week.

Then, tell us what you think by taking our [1-page survey](https://www.surveygizmo.com/s3/5262916/8S).

We’re always interested in hearing ideas for improvements, particularly any low-hanging fruit that could save us all from some regular frustration. We do our work in the open, so you can [follow along](https://firefox-dev.tools/) and chime in. We’ll keep you updated at [@FirefoxDevTools](https://twitter.com/FirefoxDevTools).

_Thanks to [Patrick Brosset](https://twitter.com/patrickbrosset/) for his contributions to this article._

{{< signature "dm, il" >}}
