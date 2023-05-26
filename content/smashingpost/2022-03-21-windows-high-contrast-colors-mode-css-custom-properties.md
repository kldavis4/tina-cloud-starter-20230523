---
title: 'Windows High Contrast Mode, Forced Colors Mode And CSS Custom Properties'
slug: windows-high-contrast-colors-mode-css-custom-properties
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb1649b-2b93-4626-851d-5178033d0894/windows-high-contrast-colors-mode-css-custom-properties.jpg
date: 2022-03-21T12:30:00.000Z
summary: >-
  CSS Custom Properties can be used for far more than just color, and their values update in realtime, both via display mode updates and JavaScript logic. This is powerful stuff. Eric explains how modern CSS is a powerful piece of assistive technology that can thread into it to create flexible, maintainable and adaptive digital experiences.
description: >-
  CSS Custom Properties can be used for far more than just color, and their values update in realtime, both via display mode updates and JavaScript logic. This is powerful stuff. Eric explains how modern CSS is a powerful piece of assistive technology that can thread into it to create flexible, maintainable and adaptive digital experiences.
categories:
  - CSS
  - Tools
  - Techniques
  - Accessibility
---

I’m extremely excited about [the upcoming Forced Colors media query](https://www.w3.org/TR/mediaqueries-5/#forced-colors). It takes the work done for [Windows High Contrast mode](https://assistivlabs.com/assistive-tech/display/high-contrast-mode) and elevates it to an open, cross-browser standard. This means that a person will be able to use whatever browser works best for them to get what they need, instead of being forced to use one specific browser.

## What Is Windows High Contrast Mode? What Is Forced Colors Mode?

Windows High Contrast mode, and its successor, Forced Colors mode, are important pieces of assistive technology. These two [display modes](https://www.a11yproject.com/posts/operating-system-and-browser-accessibility-display-modes/#high-contrast-mode) affect:

- The operating system installed on a device,
- The browser is installed on the operating system, and
- All web content is loaded by that browser.

These display modes prioritize legibility above all else. Ornamentation and decoration are discarded in order to allow content to be displayed clearly.

All content affected by these two modes maps to a color theme. This color theme can be modified by someone to use any combination of colors, to create a suite of colors that works for their specific access needs. 

For some, Windows High Contrast/Forced Colors mode represents the last option they have to view content on their device &mdash; including web content. This is highly specialized, highly personalized assistive technology, and using it is a very intentional act. 

Others may circumstantially benefit from using Windows High Contrast/Forced Colors mode. One of my favorite examples of this is being able to use your laptop in the park, despite the glare of the noonday sun.

Here’s how Smashing Magazine looks with Forced Colors activated and set to use the High Contrast #1 theme:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/308f9538-a0b6-4d1b-82ce-78d82c312e78/1-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/308f9538-a0b6-4d1b-82ce-78d82c312e78/1-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="507" sizes="100vw" caption="You might not think this looks pretty, but it’s hard to argue that it’s difficult to read. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/308f9538-a0b6-4d1b-82ce-78d82c312e78/1-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot of the Smashing Magazine homepage in Microsoft Edge. Forced Color mode is enabled, showing a stark design using neon colors on a dark background. The featured article is ‘New CSS Features In 2022’, by Michelle Barker. A photo of Michelle accompanies the headline." >}}

And this is how Smashing Magazine looks with Forced Colors activated and set to use the High Contrast White theme:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094fbdb6-e541-4add-900b-06754889d519/2-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094fbdb6-e541-4add-900b-06754889d519/2-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="507" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094fbdb6-e541-4add-900b-06754889d519/2-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot of the Smashing Magazine homepage in Microsoft Edge. Forced Color mode is enabled, now showing a stark design using mostly blue text on a white background." >}}

And this is how Smashing Magazine looks with Forced Colors activated and set to use a custom theme:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a7a405-6edb-4a3e-96d9-f6b1ed101759/3-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a7a405-6edb-4a3e-96d9-f6b1ed101759/3-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="507" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a7a405-6edb-4a3e-96d9-f6b1ed101759/3-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot of the Smashing Magazine homepage in Microsoft Edge. Forced Color mode is enabled, now showing a stark design using mostly yellow text on a red background. It looks like a McDonalds." >}}

## High Contrast Mode, Forced Colors Mode, And Browser Support

I’ll be honest, the current state of Forced Colors support is a bit of a mess. 

Internet Explorer will never support Forced Colors mode because Microsoft has discontinued support of the browser. It will also [never support Custom Properties](https://caniuse.com/css-variables). Internet Explorer does, however, support High Contrast mode.

Edge supports Forced Colors mode. It also has legacy support for Windows High Contrast mode. This means that code written specifically to support High Contrast mode in Internet Explorer will work in Edge as well.

The Forced Color mode syntax is an update on Windows High Contrast mode syntax, which uses specialized keywords (more on this in a bit). As a consequence of this, Internet Explorer supports some, but not all Forced Color mode syntax.

Every other major evergreen browser has [support for Forced Colors mode, except for Safari](https://caniuse.com/mdn-css_at-rules_media_forced-colors). The trick here is that macOS, iOS, and Android currently do not have a way to specify Forced Color mode themes. This means that for now, only Windows is capable of fully supporting a full Forced Color mode experience.

Here are two tables of the current support landscape if you need help visualizing this:

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Browser</th>
			<th>Supports legacy High Contrast Mode CSS properties?</th>
      <th>Supports Forced Colors mode CSS properties?</th>
      <th>Supports CSS Custom Properties?</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Internet Explorer</td>
			<td>✅ Yes</td>
      <td>⚠ Some</td>
      <td>🚫 No</td>
		</tr>
    <tr>
			<td>Edge</td>
			<td>✅ Yes</td>
      <td>✅ Yes</td>
      <td>✅ Yes</td>
		</tr>
    <tr>
			<td>Chrome</td>
			<td>🚫 No</td>
      <td>✅ Yes</td>
      <td>✅ Yes</td>
		</tr>
    <tr>
			<td>Firefox</td>
			<td>🚫 No</td>
      <td>✅ Yes</td>
      <td>✅ Yes</td>
		</tr>
    <tr>
			<td>Safari</td>
			<td>🚫 No</td>
      <td>⏳ Soon</td>
      <td>✅ Yes</td>
		</tr>
	</tbody>
</table>

<br>

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Operating System</th>
			<th>Supports switching and creating Forced Color mode themes?</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Windows</td>
			<td>✅ Yes</td>
		</tr>
		<tr>
			<td>macOS</td>
			<td>🚫 Not yet</td>
		</tr>
		<tr>
			<td>iOS</td>
			<td>🚫 Not yet</td>
		</tr>
    <tr>
			<td>Android</td>
			<td>🚫 Not yet</td>
		</tr>
	</tbody>
</table>

### SVG That Uses `currentColor`

This is a whole thing unto itself, and beyond the scope of this post, but there are some issues right now with how Forced Color mode works with [SVGs that utilize](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#currentcolor_keyword) [`currentColor`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#currentcolor_keyword) to control their coloring. 

If you’d like to learn more about the particulars &mdash; including how to work with them &mdash; I recommend reading [this excellent, in-depth article by Melanie Richards](https://melanie-richards.com/blog/currentcolor-svg-hcm/).

### Why This Is All Worth Mentioning

The reason why this is important is that Forced Colors mode syntax differs slightly from the Windows High Contrast mode syntax. 

Edge has backwards compatibility, but Internet Explorer will never have forwards compatibility. This means that Internet Explorer viewing web content with High Contrast mode activated **may not** properly display content using the newer Forced Color mode syntax.

This is worth mentioning because [not everyone can or will be able to upgrade their device](https://ericwbailey.design/writing/truths-about-digital-accessibility/#assistive-technology-may-not-be-running-on-high-powered-devices%2C-or-be-running-the-latest-software) to use something other than Internet Explorer, regardless of Microsoft’s upcoming discontinuation of support. 

As a result of this, it is vital to approach High Contrast/Forced Color mode work with a cautious, ego-free mindset. If at all possible, talk to High Contrast/Forced Color mode users to determine what their specific preferences actually are.

{{% feature-panel %}}

## How To Design For Windows High Contrast And Forced Colors Mode

[You don’t](https://twitter.com/KittyGiraudel/status/877123359418576896).

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">High contrast mode is not about design anymore but strict usability. You should aim for highest readability, not color aesthetics.</p>&mdash; Kitty Giraudel (@KittyGiraudel) <a href="https://twitter.com/KittyGiraudel/status/877123359418576896?ref_src=twsrc%5Etfw">June 20, 2017</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<br>

No, seriously. Forced Colors and Windows High Contrast modes are all about presenting all content &mdash; including web content &mdash; in a predictable and consistent way. 

You only want to make small, surgical tweaks to your content, not create a completely new, bespoke Forced Color mode experience. 

Each element’s [inherent HTML semantics](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html) tell Forced Colors and Windows High Contrast modes how to be displayed. Areas, where semantic HTML isn’t used, are good areas to check &mdash; to see if your content holds up.

## Forced Colors Mode Keywords

Forced Colors mode &mdash; like Windows High Contrast mode &mdash; uses a suite of specialized keywords. These keywords assign color to meaning. For example, all inert, regular text will use the same theme color, with this color being mapped to the `CanvasText` keyword.

The reason keywords are used is because the text color could be any color. Every content type Forced Color mode effect can also, potentially, be any color.

Forced Colors mode has multiple themes, including ones that a person can create for themselves. This lets someone tweak how things look until it works for them.

[Sourced from this excellent post](https://blogs.windows.com/msedgedev/2020/09/17/styling-for-windows-high-contrast-with-new-standards-for-forced-colors/), the list of Forced Color keywords is:

<table>
	<thead>
		<tr>
			<th>Content</th>
			<th>Keyword</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Text</td>
			<td><code>CanvasText</code></td>
		</tr>
    <tr>
			<td>Hyperlinks</td>
			<td><code>LinkText</code></td>
		</tr>
    <tr>
			<td>Disabled Text</td>
			<td><code>GrayText</code></td>
		</tr>
    <tr>
			<td>Selected Text, foreground</td>
			<td><code>HighlightText</code></td>
		</tr>
    <tr>
			<td>Selected Text, background</td>
			<td><code>Highlight</code></td>
		</tr>
    <tr>
			<td>Buttons, foreground</td>
			<td><code>ButtonText</code></td>
		</tr>
    <tr>
			<td>Buttons, background</td>
			<td><code>ButtonFace</code></td>
		</tr>
    <tr>
			<td>Backgrounds</td>
			<td><code>Canvas</code></td>
		</tr>
	</tbody>
</table>

Here is how these keywords map to the Windows High contrast theme selection interface:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab25fbb-4c72-4c7a-8449-fe1c9643714c/4-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab25fbb-4c72-4c7a-8449-fe1c9643714c/4-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="492" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab25fbb-4c72-4c7a-8449-fe1c9643714c/4-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot from Windows 10 with Windows High contrast settings, showing how color keywords map to the High Contrast #1 theme." >}}

And here is an example of a custom theme:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb546fe-f7ba-4b84-89d6-c2575363902e/5-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb546fe-f7ba-4b84-89d6-c2575363902e/5-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="492" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb546fe-f7ba-4b84-89d6-c2575363902e/5-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot from Windows 10 with a custom Forced Color mode theme called ‘Custom Theme.’ The theme uses a bright red background, purple buttons, black text, and pale blue hyperlinks." >}}

This theme might look like the ugliest thing you’ve ever seen, but it’s vital to remember, that this combination of colors might be what lets someone use their device.

{{% ad-panel-leaderboard %}}

## CSS Custom Properties

The upgrade of Windows High Contrast mode into Forced Colors mode works really well with another contemporary feature of CSS: [Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/). 

If you are unfamiliar, Custom Properties are a way to create “variables” in CSS—formalized, encoded values that can be dynamically manipulated.

<pre><code class="language-css">:root {
  --color-background: #ffffff;
  --color-text: #000000;
} 

@media (prefers-color-scheme: dark) {
  :root {
    --color-background: #000000;
    --color-text: #ffffff;
  }
}

body {
  background-color: var(--color-background);
  color: var(--color-text);
}</code></pre>

In this example, I’m creating Custom Properties in [the `:root` selector](https://developer.mozilla.org/en-US/docs/Web/CSS/:root) that will be used to control the background and text color. 

I’m initially setting the text color to black and the background color to white, and then updating the Custom Properties to use white text and a black background when dark mode is activated. Invoking the Custom Properties in the `body` selector is the magic that makes it all happen. 

CSS Custom Properties can be used for far more than just color, and their values update in realtime, both via display mode updates and [JavaScript logic](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty). This is powerful stuff.

## Using Custom Properties With Forced Colors Mode

We’re going to take all this background information and apply it to something concrete: A modal dialog. Do you remember how I said Custom Properties can use more than just color values? We’re going to take advantage of that now.

Unfortunately, [the `dialog` element still has assistive technology compatibility issues](https://www.scottohara.me/blog/2019/03/05/open-dialog.html#incoming-dialog), meaning that the most accessible solution is still to use one constructed with the help of ARIA and JavaScript. [Kitty Giraudel’s `a11y-dialog`](https://github.com/KittyGiraudel/a11y-dialog) is a wonderful, flexible resource that I enthusiastically recommend to help you do just that.

### Accessibility Workarounds

Since the modal is constructed by using `div`s, Forced Colors mode does not know it is a modal. It, like Windows High Contrast Mode, [does not take ARIA into consideration](https://ericwbailey.design/writing/truths-about-digital-accessibility/#windows-high-contrast-mode-ignores-aria) when determining how color is assigned. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/929fc708-6400-4246-a034-a45c5b13f24a/6-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/929fc708-6400-4246-a034-a45c5b13f24a/6-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="258" sizes="100vw" caption="Windows High Contrast #2 theme showing how semantic HTML maps to Forced Color mode keywords, while ARIA does not. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/929fc708-6400-4246-a034-a45c5b13f24a/6-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="Side-by-side comparison of sample text, link and button. The left side uses a paragraph element, an anchor element, and a button element, while the right side uses ARIA roles of text, link, and button respectively. The left-hand side is picking up Forced Color mode keyword mapping for CanvasText, LinkText, and ButtonText and ButtonFace, while the right side does not." >}}

This is one of the reasons why the Forced Color mode media query and its keywords exist &mdash; to tweak content until it works the way someone would expect it to. 

Sometimes content isn’t written semantically, and there’s nothing you can do about it. It is no different than using CSS to make tweaks to vendor-supplied code you have no direct control over.

### Styling The Modal For Forced Colors Mode

Here’s a CodePen for our modal, before we make our Forced Color mode tweaks:

{{< codepen height="480" theme_id="light" slug_hash="KKyjovK" default_tab="css,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Modal dialog [forked]](https://codepen.io/smashingmag/pen/KKyjovK) by <a href="https://codepen.io/ericwbailey">Eric Bailey</a>.{{< /codepen >}}  

Here’s how it looks without Forced Color mode activated:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51a68ca0-d2e8-46c5-8395-973a5453b5ef/7-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51a68ca0-d2e8-46c5-8395-973a5453b5ef/7-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="508" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51a68ca0-d2e8-46c5-8395-973a5453b5ef/7-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot of a small modal with a title, close button, body content, and a dark background floating above some placeholder text on the page with a light background below it." >}}

And here is a screenshot of how it looks with Forced Color mode activated:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8e5a291-eb88-42c1-95fc-5caf012b246f/8-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8e5a291-eb88-42c1-95fc-5caf012b246f/8-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="507" sizes="100vw" caption="Windows High Contrast #2 theme. Notice, that all text is using the <code>CanvasText</code> color, and the modal’s close button is using the <code>ButtonText</code> color. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8e5a291-eb88-42c1-95fc-5caf012b246f/8-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="The same small modal as the previous example, only now with Forced Color mode enabled. All text, including the modal and the background content, is the same color. Both the modal and the page’s background colors are the same. The modal’s border is very thin, and it’s hard to tell where the background content stops and the modal begins." >}}

While a blind person using a screen reader may know a modal is present, because of how it is announced, a low vision person using Forced Colors mode may be confused because the modal’s boundaries are not communicated strongly enough visually. This may be further complicated by [low vision people who use both Forced Colors mode and a screen reader](https://adrianroselli.com/2017/02/not-all-screen-reader-users-are-blind.html).

Notice, that even though Forced Colors mode does not know it is a `dialog`, it does know what a CSS `outline` declaration is. It takes the very faint, thin light gray border we’re using and colors it with the color value mapped to the `CanvasText` Forced Color mode keyword. 

Also notice, that the modal’s `box-shadow` has been discarded when Forced Color mode is activated. This, and the outline recoloring are by design. 

**Remember:** *Forced Color mode prioritizes legibility above all else, and makes visual updates to honor that.*

### Making Our Update

Much as how we’re redefining component-level CSS Custom Properties for things like `:hover` and `:active` state on the modal close icon, we can redefine for different display modes. Here is a CodePen for our modal after our Forced Color mode tweaks have been made:

{{< codepen height="480" theme_id="light" slug_hash="zYPVjPa" default_tab="css,result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Modal dialog with Forced Color mode tweaks [forked]](https://codepen.io/smashingmag/pen/zYPVjPa) by <a href="https://codepen.io/ericwbailey">Eric Bailey</a>.{{< /codepen >}}  

On line 104 of this CodePen example, we are redefining the `--dialog-border-width` Custom Property inside a Forced Color mode media query declaration. The reason for doing so is a highly intentional tweak. It takes the thin outline border and makes it dramatically thicker. 

<pre><code class="language-css"> @media (forced-colors: active) {
  --dialog-border-width: var(--size-300);
}</code></pre>

The reason for this adjustment is that it helps to show the modal’s outer boundary and communicate that it is floating on top of the rest of the page’s content. Forced Color mode removes the modal’s `box-shadow`, so we cannot rely on that visual affordance in this specialized viewing mode.

Here is a screenshot of it in action:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9175e6e-6222-49d8-b2a1-335ae9b98b15/9-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9175e6e-6222-49d8-b2a1-335ae9b98b15/9-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png" width="800" height="507" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9175e6e-6222-49d8-b2a1-335ae9b98b15/9-windows-high-contrast-mode-forced-colors-mode-css-custom-properties.png'>Large preview</a>)" alt="A screenshot of the same small modal in Forced Color mode, only now the modal’s outer border is a lot thicker. It is easy to see where the background content stops and the modal’s content begins." >}}

{{% ad-panel-leaderboard %}}

## Testing

Here’s [how to enable contrast themes in Windows](https://support.microsoft.com/en-us/windows/change-color-contrast-in-windows-fedc744c-90ac-69df-aed5-c8a90125e696). Use macOS or Linux? You’re in luck! There are multiple ways to test for Forced Color support:

1. Get a Windows [craptop](https://css-tricks.com/test-your-product-on-a-crappy-laptop/) and use a tunneling service, such as [ngrok](https://ngrok.com/). The craptop is also a chance to test your website or web app’s performance &mdash; another potential access barrier.
2. Use an app to load a Virtual Machine with [a Windows image provided by Microsoft](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/).
3. Use a service like [Assistiv Labs](https://assistivlabs.com/), which provides a cloud-hosted on-demand Windows Virtual Machine geared towards accessibility testing.
4. Use [Polypane’s media emulation functionality](https://polypane.app/docs/emulation/) to toggle an emulated Forced Color mode.
5. Use Microsoft Edge’s DevTools to toggle an emulated Forced Color mode.

I would advise some caution for options four and five, as [an emulated experience only uses a single theme](https://melanie-richards.com/blog/forced-colors-emulation/), and it’s not representative of the Forced Color mode’s full capabilities. 

I particularly like the Assistiv Labs option, because it’s focused on accessibility testing, and it does not heavily tax my laptop the way a local app-run Virtual Machine would.

## Wrapping Up

At the surface level, this might seem like a lot of words just to demonstrate how to update a CSS Custom Property. This post’s goal, however, is to introduce you to a powerful piece of assistive technology and show how modern CSS can elegantly thread into it to make flexible, maintainable, and adaptive digital experiences.

Now that you know about Forced Color mode and how it works, why not take some time and audit how your websites and web apps look when it is activated? Some little tweaks might make a huge difference for someone who relies on a Forced Color mode experience to browse the web.

### Further Reading

- “[Styling for Windows high contrast with new standards for forced colors](https://blogs.windows.com/msedgedev/2020/09/17/styling-for-windows-high-contrast-with-new-standards-for-forced-colors/),” Microsoft Edge Team
- “[CurrentColor SVG in forced colors modes](https://melanie-richards.com/blog/currentcolor-svg-hcm/),” Melanie Richards
- “[Assistive technology: Operating System and Browser Accessibility Display Modes](https://www.a11yproject.com/posts/operating-system-and-browser-accessibility-display-modes/),” Eric Bailey
- “[Working with the text backplate in Windows High Contrast](https://www.gwhitworth.com/posts/2019/high-contrast-text-backplate/),” Greg Whitworth
- “[WHCM and System Colors](https://adrianroselli.com/2021/02/whcm-and-system-colors.html),” Adrian Roselli
- “[Quick Tips for High Contrast Mode](https://sarahmhigley.com/writing/whcm-quick-tips/),” Sarah Higley

{{< signature "vf, yk, il" >}}
