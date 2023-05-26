---
title: 'How To Develop A Text Editor For The Web'
slug: develop-text-editor-web
author: ilya-medvedev
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e771d289-5725-48a4-b8b6-4ba30f2a2f44/develop-text-editor-web.jpg
date: 2022-02-22T13:00:00.000Z
summary: >-
  How do text typing and editing work on the web? Although this process might seem straightforward, there is a lot of technical nuance behind its apparent simplicity. This article looks at how typing on the web works.
description: >-
  How do text typing and editing work on the web? Although this process might seem straightforward, there is a lot of technical nuance behind its apparent simplicity. This article looks at how typing on the web works.
categories:
  - CSS
  - Tools
  - Workflow
---

I work for [Readymag](https://readymag.com/), which makes a browser-based design tool that helps people create websites, portfolios, and all kinds of online publications, without coding. Many widgets are available in our tool, and the text widget is one of the most widely used.

The text widget is a text-entry field where the user can style text using a range of controls in the editor. Each control applies a CSS property to the text. From the user’s side, it looks like an ordinary field for entering text, but a huge number of complex processes are hidden behind its apparent simplicity.

In this article, I’ll explain the challenges my company faced and the solutions we used to create a text widget in our application. I’ll also dive into how we implemented it and what we learned along the way &mdash; and how typing on the web works in general.

## Editing Text On The Web

There are several ways to implement text-input fields on the web. We could use a simple text field, or a multi-line `textarea` element, or the `contenteditable` attribute to make an input editable, or `document.designMode = on`. How are they different?

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8dd538-6663-4756-b699-bc1a97990c14/1-develop-text-editor-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8dd538-6663-4756-b699-bc1a97990c14/1-develop-text-editor-web.png" width="800" height="456" sizes="100vw" caption="Text widget in Readymag. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8dd538-6663-4756-b699-bc1a97990c14/1-develop-text-editor-web.png'>Large preview</a>)" alt="Text widget in Readymag" >}}

The `input` and `textarea` elements are ideal for adding text to a page, but they don’t provide a rich text-formatting experience. For this, we can use the [`contenteditable`](https://html.spec.whatwg.org/multipage/interaction.html#contenteditable) attribute to make almost any element editable and enable the use of text styles.

{{< codepen height="480" theme_id="light" slug_hash="bGYaGKL" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen “Text Inputs” by <a href="https://codepen.io/imedvedev">Ilya Medvedev</a>.{{< /codepen >}}

If you need to edit the entire page at once, you can use [`document.designMode`](https://developer.mozilla.org/en-US/docs/Web/API/Document/designMode). This mode allows any element within a given document to be edited, even an `iframe`.

We opted for the `contenteditable` attribute, which includes all of the necessary text-editing capabilities. With this attribute, any text on the page becomes editable, which is very important if we want to **enable people to style text with CSS**. For example, users could then style selected sections or the entire text directly.

## Text Styles And Font Properties

We enable users to style text in any way they wish by providing access to all options that CSS provides out of the box. In addition to the well-known properties, such as font, style, color, and decoration, we give users the opportunity to use [OpenType font features](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/OpenType_fonts_guide), such as ligatures, stylistic sets, fractions, and so on. These features work through the [`font-feature-settings`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-feature-settings) CSS property, which allows users to customize text styles.

**Note**: *I highly recommend reading Sparanoid’s excellent article showcasing [all of OpenType’s features](https://sparanoid.com/lab/opentype-features/).*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d94d7223-4d74-4ede-844c-e38819960663/2-develop-text-editor-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d94d7223-4d74-4ede-844c-e38819960663/2-develop-text-editor-web.png" width="800" height="456" sizes="100vw" caption="Using font properties in the text widget. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d94d7223-4d74-4ede-844c-e38819960663/2-develop-text-editor-web.png'>Large preview</a>)" alt="Using font properties in the text widget" >}}

Modern typography has taken a big step forward, allowing for the use of [variable fonts](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/Variable_Fonts_Guide) on the web via the [`font-variation-settings`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variation-settings) property.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff31bc7a-ff1b-46a0-a51b-eec36ffdd4c4/3-develop-text-editor-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff31bc7a-ff1b-46a0-a51b-eec36ffdd4c4/3-develop-text-editor-web.png" width="800" height="456" sizes="100vw" caption="OpenType font features showcase. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff31bc7a-ff1b-46a0-a51b-eec36ffdd4c4/3-develop-text-editor-web.png'>Large preview</a>)" alt="OpenType font features showcase" >}}

Each variable font has variable properties whose values you can change. For example, in a standard font, you can change the font weight using strictly specified values (`400`, `500`, `600`, and so on), whereas in a variable font, you can use any value in the available range, providing more extensive possibilities for text styling.

<pre><code class="language-css">.style-1 {
  font-weight: 600;
}

.style-2 {
  font-variation-settings: "wght" 777;
}</code></pre>

Below you can see an example of how working with a variable font looks in a text widget.

{{< vimeo id="678507493" caption="Example of font-variation-settings" breakout="true" >}}

In addition to the [registered values](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variation-settings#registered_and_custom_axes) (`wght`, `wdth`, `slnt`, etc.), font makers can also create their own unique font features (as in the example above). To give our users the opportunity to use all possible font features, we need this information first.

All of the features you want to use should be defined in the font file. Let’s look at its specifications. Each font can be represented in the form of tables, providing all of the different information used when rendering its characters.

We use two tables to collect this information about fonts:

1. **Glyph Substitution Table**  
The [glyph substitution table](https://docs.microsoft.com/en-us/typography/opentype/spec/gsub) (GSUB) contains a list of glyph-rendering data. The `GSUB.featureList` object is an enumeration of font features and their properties. You can view an example of [data in the table on GitHub](https://gist.github.com/iam-medvedev/1bc41c8b6b049f3cf8ad2ce6deda4eaf). In this table, the `tag` field is most interesting. This is the name of the font feature, and it indicates that this feature is available with this font. We can safely use `tag` in the `font-feature-settings` property.
2. **Font Variations Table**  
The [font variations table](https://developer.apple.com/fonts/TrueType-Reference-Manual/RM06/Chap6fvar.html) (fvar) is a representation of the variable properties associated with a font. An example of the table is also [available on GitHub](https://gist.github.com/iam-medvedev/cfc3f525d1bcf2081b8c46815c47aaf0). Each object is a font property, with a description of possible values (`min`, `max`, default) and a localized name (if any). We use these values with the `font-variation-settings` property.

With the help of these two tables, we can cover all of our requirements: using variable font properties and various font features. The resulting data is displayed in the text-widget controls in the editor, where users can style text without using any code.

## Using Your Keyboard

Text input is one of the most important aspects of the text-widget user experience. In addition to enabling shortcuts for working with text, we had to deal with some unusual challenges. Navigating text with the arrow keys was definitely one of them.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/872d7c17-d3b1-4cf7-adfe-90911e278fbd/5-develop-text-editor-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/872d7c17-d3b1-4cf7-adfe-90911e278fbd/5-develop-text-editor-web.png" width="800" height="456" sizes="100vw" caption="Hidden characters icons. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/872d7c17-d3b1-4cf7-adfe-90911e278fbd/5-develop-text-editor-web.png'>Large preview</a>)" alt="Hidden characters icons" >}}

While the user is editing, the text widget also shows hidden characters, such as non-breaking spaces and line breaks. They are implemented as SVG icons inserted in the text, which poses a problem: If we use `contenteditable`, then these icons prevent users from moving their cursor with the arrow keys.

The solution is simple enough: Use a `span` and the `:before` pseudo-element. This way, the browser perceives the icon as being text and the arrow keys work great.

<pre><code class="language-css">span:before {
  content: "";
  height: 1em;
  position: relative;
  background-repeat: no-repeat;
  background-image: url("data:image/svg+xml,...");
  background-position: center bottom;
  background-size: 1em;
}</code></pre>

## Shortcuts

There are two keyboard shortcuts for pasting text in a text widget.

<kbd>Cmd</kbd>/<kbd>Ctrl</kbd> + <kbd>V</kbd> pastes text from the clipboard and keeps any styles it had in the original document. If the text was copied from an application such as Pages, Notes, Word or Google Docs, then your clipboard will contain HTML information, not just plain text. This HTML can be parsed and pasted while keeping the original styles.

You can get the HTML data as follows:

<pre><code class="language-javascript">// https://www.w3.org/TR/clipboard-apis/#reading-from-clipboard
document.addEventListener('paste', (e) =&gt; {
  const text = e.clipboardData.getData('text/plain');
  const html = e.clipboardData.getData('text/html');
  
  handlePaste();
});</code></pre>

In addition, we have the <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>V</kbd> shortcut. When you insert text using this keyboard combination, the browser will leave the plain data in the payload, so styling is controlled by the paste destination. These shortcuts exist in the browser by default, but you need to remember to implement them in your project.

## Text Selection And Focus

{{< codepen height="480" theme_id="light" slug_hash="GROygrx" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen “Selection example” by <a href="https://codepen.io/imedvedev">Ilya Medvedev</a>.{{< /codepen >}}

Text selection helps users see which piece of text is currently being edited. Let’s try a simple example: an input field with a button to control the boldness of the text.

In this example, we can select a piece of text and press the `Bold` button, and the selection in the text will remain afterwards. But what if our example is more complicated? Say we add an input field to the text-size selector. In this case, the focus will shift to the new input.

There are **two options for solving this problem**:

- After each input event, we force the focus to move back to the text block. In this case, the selection will start blinking after a certain number of input events &mdash; we don’t want that.
- We can add the text block to an `iframe`. As you probably know, an `iframe` has its own global `window` object. So, as long as the selection is within the `iframe`, it will persist even if the focus outside is moved.

We ended up with an `iframe`-wrapped text widget. So, as long as the selection is within the `iframe`, it will persist even if the focus outside is moved. Take a look at the screenshot below. We have two selections on the page: the selected fragment in the text widget and the selected value of the text size in the control.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c672be5-8ccf-4e00-b6da-144713cf1c6a/6-develop-text-editor-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c672be5-8ccf-4e00-b6da-144713cf1c6a/6-develop-text-editor-web.png" width="800" height="456" sizes="100vw" caption="Text selection within iframe. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c672be5-8ccf-4e00-b6da-144713cf1c6a/6-develop-text-editor-web.png'>Large preview</a>)" alt="Text selection within iframe" >}}

## Performance During Text Input

The responsiveness of your text-editing interface is important. Monitor the frames-per-second (FPS) value closely, especially when it comes to tasks like editing text at a high speed or changing the font size.

Readymag has two viewports: **desktop** and **mobile**. Text styles can appear different in each. While the text is being entered, the editor will perform various calculations to synchronize data between viewports. High responsiveness is achieved by using the browser API: `requestAnimationFrame` and `requestIdleCallback`:

- [`requestAnimationFrame`](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame) is called every time the screen is refreshed;
- [`requestIdleCallback`](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback) is called only when the browser is idle.

This is a great way to perform tedious operations without blocking the main thread.

## Accessibility

Enabling accessibility is one of the most important practices in web development today. If your website is designed with accessibility in mind, it will **give more people access to your product**. This means accommodating not only people with disabilities but also users on different platforms: desktop and touch devices, screen readers, hearing devices, and so on. To understand just how important making projects accessible can be, I recommend checking out the recent [accessibility statistics](https://monsido.com/blog/accessibility-statistics).

To begin incorporating web accessibility practices, first check the [Web Content Accessibility Guidelines](https://www.w3.org/WAI/standards-guidelines/wcag/) (WCAG), the most comprehensive resource on the topic. And as long as Readymag is a tool for publication, in addition to WCAG, we also need to follow the [Authoring Tool Accessibility Guidelines](https://www.w3.org/WAI/standards-guidelines/atag/) (ATAG).

Our team is currently at the stage of integrating accessibility into the editor. In subsequent articles, we will share more about our journey towards fully integrating accessibility at Readymag. You can also check any work made with Readymag using our [accessibility checklist](https://readymag.com/readymag/readycheck/accessibility/).

## Best Practices

Finally, here are some tips to help you develop a text editor on the web:

- **Think carefully about layout.**  
Identify in advance what capabilities you need and how you will work with the elements in the text editor.
- **Set up visual testing.**  
When you work with text, you cannot rely entirely on the snapshot test result. You might get the correct result in the test, expecting the given CSS for the block, but sometimes the result might not be what you expected.
- **Test your work in different browsers.**  
While most browsers support new online features reasonably well, there are often problems with displaying the same styles in different browsers.
- **Use [feature flags](https://dev.to/readymag/what-makes-feature-flags-a-path-to-faster-and-safer-development-obd)** for safer development of new features.
- **Measure FPS in the browser when entering text.**  
Don’t do CPU-intensive tasks in a single thread.
- **Don’t be afraid to experiment**.
- Last but not least, **try [Text Widget](https://readymag.com/readymag/newsletter/)** in Readymag.

## Some Useful Links

- “[The Complete CSS Demo For OpenType Features](https://sparanoid.com/lab/opentype-features/),” Sparanoid
- “[Introduction To Variable Fonts On The Web](https://web.dev/variable-fonts/),” web.dev
- “[Awesome Typography](https://github.com/Jolg42/awesome-typography),” Joël Galeran
- “[Variable Fonts](https://v-fonts.com/),” Nick Sherman
- [Fontkit](https://github.com/foliojs/fontkit)
- [OpenType.js](https://github.com/opentypejs/opentype.js)

{{< signature "vf, il, al, yk" >}}
