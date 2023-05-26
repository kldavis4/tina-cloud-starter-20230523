---
title: The Problem Of CSS Form Elements
slug: css-form-elements-problem
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4d1826b-efbe-4ba9-97a7-90f85b6910a8/css-form-elements-problem.png
date: 2013-02-27T13:28:14.000Z
author: gabriele-romanato
description: >-
  Before 1998, the birth year of CSS Level 2, form elements were already widely
  implemented in all major browsers. The CSS 2 specification did not address the
  problem of how form elements should be presented to users.
categories:
  - Coding
  - CSS
  - Semantics
---
Before 1998, the birth year of CSS Level 2, form elements were already widely implemented in all major browsers. The CSS 2 specification did not address the problem of <strong>how form elements should be presented to users</strong>. Because these elements are part of the UI of every Web document, the specification’s authors preferred to leave the visual layout of such elements to the default style sheet of Web browsers.

Through the years, this lack of detail in the CSS specification has forced Web developers to produce a significant number of tests and examples whose primary goal is to reduce form elements to a common visual denominator in order to get a cross-browser rendering of elements such as <code>input</code>, <code>select</code>, <code>fieldset</code>, <code>legend</code> and <code>textarea</code>. In this article, we will cover some of the CSS patterns used by Web developers to tame the visual layout of form elements.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Form Inputs: The Browser Support Issue You Didn’t Know You Had](https://www.smashingmagazine.com/2015/05/form-inputs-browser-support-issue/)
*   [Web Form Design: Showcases And Solutions](https://www.smashingmagazine.com/web-form-design-showcases-and-solutions/)
*   [New Approaches To Designing Log-In Forms](https://www.smashingmagazine.com/web-form-design-showcases-and-solutions/#n10)
*   [Designing CSS Buttons: Techniques and Resources](https://www.smashingmagazine.com/2009/11/designing-css-buttons-techniques-and-resources/)

## Roger Johansson’s Tests

Back in 2004 and later in 2007, Roger Johansson created a complete test suite for form elements and CSS. These seminal tests, which can be found in his article “<a href="https://www.456bereastreet.com/archive/200701/styling_form_controls_with_css_revisited/">Styling Form Controls With CSS, Revisited</a>,” lead to the frustrating conclusion that Johansson summarizes with the following words:
<blockquote>"So what does this experiment show? Like I already stated, it shows that using CSS to style form controls to look exactly the same across browsers and platforms is impossible. It also shows that most browsers ignore many CSS properties when they are applied to form controls."</blockquote>

{{% feature-panel %}}

Despite the underlying truth of these conclusions, Web developers continued to extensively test CSS styles on form elements to find the Holy Grail of — or at least a reasonable compromise between — the browser’s default rendering and the author’s styles.</p>

## The Default Model

The CSS 2.1 specification states in its proposed <a href="https://www.w3.org/TR/CSS21/sample.html">default style sheet for HTML4</a> that form elements such as <code>textarea</code>, <code>input</code> and <code>select</code> are inline-block elements:

<pre><code class="language-css">textarea, input, select {
   display: inline-block;
}</code></pre>

Conversely, the <code>form</code> and <code>fieldset</code> elements are block-level elements:

<pre><code class="language-css">fieldset, form {
   display: block;
}</code></pre>

The default model proposed by the CSS specification stops here. All other visual aspects of form elements <strong>rely on the browser’s default style sheet</strong>. However, the above rules indicate the following:

*   Inline-block elements can be styled using an inline formatting context. This implies the use of CSS properties such as `line-height` and `vertical-align` to control the height of the box and its vertical alignment. Padding and margins can also be applied to define the outer and inner spacing of the affected box. As well, inline-block elements accept widths and heights because they share the block formatting model.
*   Block-level elements can be styled using the well-known block formatting context. However, problems arise with the `fieldset` and `legend` elements because `legend` relies entirely on the default styles provided by Web browsers.

How do Web developers manage these problems?

## Defining Dimensions

Web developers soon noticed that Web browsers handle inline-block elements oddly when it comes to defining dimensions. Defining an height often leads to unexpected results:

<pre><code class="language-css">input, select {
   width: 120px;
   height: 32px;
}</code></pre>

Developers tried to fix this problem by turning these elements into block-level elements:

<pre><code class="language-css">input, select {
   width: 120px; block;
}</code></pre>

Results are still poor, except for the <code>textarea</code> element. A common pattern to solve this problem is to avoid the <code>height</code> property and instead to use the <code>font-size</code> and <code>padding</code> properties.

Browsers do not use the same font family and size on these elements, so the first thing to do is normalize them:

<pre><code class="language-css">input, select {
   width: 120px;
   font: 1em Arial, sans-serif;
}</code></pre>

For an example, see the page “<a href="https://jsfiddle.net/gabrieleromanato/J2nUn/">CSS: Defining Form Element Dimensions</a>” on jsFiddle.

Once the font in use is normalized, you can add padding to give some inner spacing to the element’s box:

<pre><code class="language-css">input, select {
   width: 120px;
   font: 1em Arial, sans-serif;
   padding: 3px 6px;
}</code></pre>

The <code>input</code> elements and <code>textarea</code> also show a border that affects their box model:

<pre><code class="language-css">input[type="text"],
input[type="password"],
textarea {
   border: 1px solid #ccc;
}</code></pre>

The <code>input</code> elements of the types <code>button</code> and <code>submit</code> have additional padding set by Web browsers. So, a common practice is to normalize them:

<pre><code class="language-css">input[type="button"],
input[type="submit"] {
   padding: 2px;
}</code></pre>

The problem with this approach is that <strong>Web browsers also apply vendor-specific properties</strong> to these elements, so our padding is not always able to normalize this property. For example, in a Webkit-based browser, you might have this:

<pre><code class="language-css">input[type="button"], input[type="submit"],
input[type="reset"], input[type="file"]::-webkit-file-upload-button,
button {
   -webkit-box-align: center;
   text-align: center;
   cursor: default;
   color: buttontext;
   padding: 2px 6px 3px;
   border: 2px outset buttonface;
   border-image: initial;
   background-color: buttonface;
   box-sizing: border-box;
}
input[type="button"], input[type="submit"], input[type="reset"] {
   -webkit-appearance: push-button;
   white-space: pre;
}</code></pre>

Padding is also used on the <code>fieldset</code> and <code>legend</code> elements but with different results:

*   Setting the padding on `fieldset` to `0` will reset the default indentation of the `legend` elements in some browsers (though not in IE).
*   Setting the padding on `legend` to `0` has the effect of making this element shrink.

Select boxes, checkboxes and radio buttons can be normalized with good results with only a few properties, namely:

*   `font-family`,
*   `font-size`,
*   `width` (on select boxes),
*   `padding`.

Applying other properties to this group of elements often leads to inconsistent results across browsers.

## Alignment

Form elements can be vertically or horizontally aligned. They can be laid out on the same line or as a group of boxes on multiple rows. To align them on the same line, you can follow one of two approaches:

1.  Use floating,
2.  Use the default inline-block context on some of these elements.

When you use floating, elements are automatically turned into block-level elements. This means that form elements are now subject to the <a href="https://www.w3.org/TR/CSS21/visuren.html#floats">nine rules that govern floated elements</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9ca37d0-0bef-4e5d-8f2f-ea32abf15ad1/vertical-grid1.jpg"><img loading="lazy" decoding="async" class="125270" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9ca37d0-0bef-4e5d-8f2f-ea32abf15ad1/vertical-grid1.jpg" alt="vertical-grid1" width="500" height="266" /></a><br>
<em>Form elements can be vertically or horizontally aligned.</em>

With floats, the main challenge is to achieve good vertical alignment on the current line. In this case, using vertical margins or padding is a common practice:

<pre><code class="language-css">input, select {
   width: 120px;
   float: left;
   margin-top: 0.4em;
}</code></pre>

This approach works when you do not have to align boxes with text, such as with the contents of a <code>label</code> element. In this case, you could use <strong>relative positioning, padding or margins</strong> on the element that contains only text:

<pre><code class="language-css">label {
   float: left;
   padding-top: 0.4em;
   width: 5em;
   margin-right: 1em;
}</code></pre>

Another problem arises with buttons. In this case, when you have a button whose dimensions are greater than those of other elements, you can force its vertical alignment with relative positioning:

<pre><code class="language-css">input[type="submit"] {
   float: left;
   width: 90px;
   position: relative;
   top: 0.4em;
}</code></pre>

This approach with <strong>relative positioning also works with checkboxes and radio buttons</strong>. Relative positioning can even be applied to normalize the left indentation of the <code>legend</code> element within a <code>fieldset</code> element, the only difference being that you would use the <code>left</code> property instead of <code>top</code>.

When using inline formatting, you can rely on the <code>vertical-align</code> property to vertically align elements:

<pre><code class="language-css">label, input[type="text"] {
   vertical-align: middle;
   margin-right: 1em;
}</code></pre>

Good results can be achieved by combining this property with the <code>line-height</code> property. However, this property must be set on the parent element. If you set this property directly on the form’s elements, their computed height would be affected:

<pre><code class="language-css">.form-row {
   line-height: 1.4;
}</code></pre>

Using a declared height on the parent element is also effective when paired with the same value for the line height:

<pre><code class="language-css">.form-row {
   line-height: 1.8;
   height: 1.8em;
}</code></pre>

With inline formatting, you can also use the <code>text-align</code> property on the parent element to align elements to the right, left or center.</p>

## The Strange Case Of File Inputs

The file input element — that is, <code>&lt;input type="file"/&gt;</code> — is a special case. This kind of element must always be visible and recognizable in the browser’s UI for security reasons. This implies that browsers deliberately ignore some style rules (such as those related to visibility) and tend to apply the algorithms defined in their default style sheet.

Furthermore, the default rendering varies from browser to browser: some browsers display only a single button, while others add a text field to display the path of the uploaded file.

Web developers, however, soon found a way to circumvent these limitations. First, they wrapped the input element in a container:

<pre><code class="language-markup tmp-xml">&lt;form action="" method="post" enctype="multipart/form-data"&gt;
   &lt;div class="upload"&gt;
      &lt;input type="file" name="upload"/&gt;
   &lt;/div&gt;
&lt;/form&gt;</code></pre>

Then, they hid the input element using the <code>opacity</code> property and applied certain styles to the input’s container:

<pre><code class="language-css">.upload {
   width: 157px;
   height: 57px;
   background: url(upload.png) no-repeat;
   overflow: hidden;
}

.upload input {
   display: block !important;
   width: 157px !important;
   height: 57px !important;
   opacity: 0 !important;
   overflow: hidden !important;
}</code></pre>

Notice the <code>!important</code> statement. This is the preferred way to override the browser’s default rules.

For an example, see the page “<a href="https://jsfiddle.net/gabrieleromanato/mxq9R/">CSS: Styling Inputs of Type ‘file’</a>” on jsFiddle.</p>

## Conclusion

Totally taming form elements is impossible due to the lack of detail in the CSS specification and because of the default styles applied by Web browsers. However, by following some common practices, reducing (though not eliminating) the differences and achieving good visual results are possible.

{{< signature "al" >}}

