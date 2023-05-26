---
title: It's Time To Start Using CSS Custom Properties
slug: start-using-css-custom-properties
author: serghospodarets
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47f90569-ec87-43bf-91b1-460c5c539739/css-variables-780w-opt.png
date: 2017-04-19T22:52:09.000Z
description: >-
  Today, CSS preprocessors are a standard for web development. One of the main
  advantages of preprocessors is that they enable you to use variables. This
  helps you to avoid copying and pasting code, and it simplifies development and
  refactoring.
categories:
  - Coding
  - CSS
  - Techniques
---
We use preprocessors to store colors, font preferences, layout details — mostly everything we use in CSS.</p>

<div class="c-felix-the-cat">
<h4 class="h3">A Detailed Introduction To Custom Elements</h4>
<p>You’ve probably heard about Web Components and how they’re going to change Web development forever. The most transformative technology of is Custom Elements, a method of defining your own elements, with their own behavior and properties. <a href="https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/" class="btn btn--small btn--green">Read the introduction →</a></p>
</div>

But preprocessor variables have some limitations:

*   You cannot change them dynamically.
*   They are not aware of the DOM’s structure.
*   They cannot be read or changed from JavaScript.

As a silver bullet for these and other problems, the community invented CSS custom properties. Essentially, these look and work like CSS variables, and the way they work is reflected in their name.

Custom properties are opening new horizons for web development.

{{% feature-panel %}}

## Syntax To Declare And Use Custom Properties

The usual problem when you start with a new preprocessor or framework is that you have to learn a new syntax.

Each preprocessor requires a different way of declaring variables. Usually, it starts with a reserved symbol — for example, <code>$</code> in Sass and <code>@</code> in LESS.

CSS custom properties have gone the same way and use <code>-&#8203;-</code> to introduce a declaration. But the good thing here is that you can learn this syntax once and reuse it across browsers!

You may ask, “Why not reuse an existing syntax?”

<a href="https://www.xanthir.com/blog/b4KT0">There is a reason</a>. In short, it’s to provide a way for custom properties to be used in any preprocessor. This way, we can provide and use custom properties, and our preprocessor will not compile them, so the properties will go directly to the outputted CSS. <em>And</em>, you can reuse preprocessor variables in the native ones, but I will describe that later.

(Regarding the name: Because their ideas and purposes are very similar, sometimes custom properties are called the CSS variables, although the correct name is CSS custom properties, and reading further, you will understand why this name describes them best.)

So, to declare a variable instead of a usual CSS property such as <code>color</code> or <code>padding</code>, just provide a custom-named property that starts with <code>-&#8203;-</code>:

<pre><code class="language-css">.box{
  --box-color: #4d4e53;
  --box-padding: 0 10px;
}</code></pre>

The value of a property may be any valid CSS value: a color, a string, a layout value, even an expression.

Here are examples of valid custom properties:

<pre><code class="language-css">:root{
  --main-color: #4d4e53;
  --main-bg: rgb(255, 255, 255);
  --logo-border-color: rebeccapurple;

  --header-height: 68px;
  --content-padding: 10px 20px;

  --base-line-height: 1.428571429;
  --transition-duration: .35s;
  --external-link: "external link";
  --margin-top: calc(2vh + 20px);

  /* Valid CSS custom properties can be reused later in, say, JavaScript. */
  --foo: if(x &gt; 5) this.width = 10;
}
</code></pre>

In case you are not sure what <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/:root"><code>:root</code></a> matches, in HTML it’s the same as <code>html</code> but with a higher specificity.

As with other CSS properties, custom ones cascade in the same way and are dynamic. This means they can be changed at any moment and the change is processed accordingly by the browser.

To use a variable, you have to use the <code>var()</code> CSS function and provide the name of the property inside:

<pre><code class="language-css">.box{
  --box-color:#4d4e53;
  --box-padding: 0 10px;

  padding: var(--box-padding);
}

.box div{
  color: var(--box-color);
}
</code></pre>

### Declaration and Use Cases

The <code>var()</code> function is a handy way to provide a default value. You might do this if you are not sure whether a custom property has been defined and want to provide a value to be used as a fallback. This can be done easily by passing the second parameter to the function:

<pre><code class="language-css">.box{
  --box-color:#4d4e53;
  --box-padding: 0 10px;

  /* 10px is used because --box-margin is not defined. */
  margin: var(--box-margin, 10px);
}
</code></pre>

As you might expect, you can reuse other variables to declare new ones:

<pre><code class="language-css">.box{
  /* The --main-padding variable is used if --box-padding is not defined. */
  padding: var(--box-padding, var(--main-padding));
  --box-text: 'This is my box';
  /* Equal to --box-highlight-text:'This is my box with highlight'; */
  --box-highlight-text: var(--box-text)' with highlight';
}
</code></pre>

## Operations: +, -, *, /

As we got accustomed to with preprocessors and other languages, we want to be able to use basic operators when working with variables. For this, CSS provides a <code>calc()</code> function, which makes the browser recalculate an expression after any change has been made to the value of a custom property:

<pre><code class="language-css">:root{
  --indent-size: 10px;

  --indent-xl: calc(2*var(--indent-size));
  --indent-l: calc(var(--indent-size) + 2px);
  --indent-s: calc(var(--indent-size) - 2px);
  --indent-xs: calc(var(--indent-size)/2);
}
</code></pre>

A problem awaits if you try to use a unit-less value. Again, <code>calc()</code> is your friend, because without it, it won’t work:

<pre><code class="language-css">:root{
  --spacer: 10;
}

.box{
  padding: var(--spacer)px 0; /* DOESN'T work */
  padding: calc(var(--spacer)*1px) 0; /* WORKS */
}
</code></pre>

## Scope And Inheritance

Before talking about CSS custom property scopes, let’s recall JavaScript and preprocessor scopes, to better understand the differences.

We know that with, for example, JavaScript variables (<code>var</code>), a scope is limited to the functions.

We have a similar situation with <code>let</code> and <code>const</code>, but they are block-scope local variables.

A <code>closure</code> in JavaScript is a function that has access to the outer (enclosing) function’s variables — the scope chain. The closure has three scope chains, and it has access to the following:

*   its own scope (i.e. variables defined between its braces),
*   the outer function’s variables,
*   the global variables.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03f35b18-9242-44ff-ad9c-9654f11ce4e1/closure-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5bce548-b21c-47d5-aa43-fb9494cb7984/closure-780w-opt.png" alt="" width="780" height="274" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03f35b18-9242-44ff-ad9c-9654f11ce4e1/closure-large-opt.png">View large version</a>)</figcaption></figure>

The story with preprocessors is similar. Let’s use Sass as an example because it’s probably the most popular preprocessor today.

With Sass, we have two types of variables: local and global.

A global variable can be declared outside of any selector or construction (for example, as a mixin). Otherwise, the variable would be local.

Any nested blocks of code can access the enclosing variables (as in JavaScript).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2834d9ac-ffa2-4f7c-974a-dcd90b5877d2/closure-scss-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/840f3a8d-2ae9-43bc-af67-7d6ce28d1d3f/closure-scss-780w-opt.png" alt="" width="780" height="277" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2834d9ac-ffa2-4f7c-974a-dcd90b5877d2/closure-scss-large-opt.png">View large version</a>)</figcaption></figure>

This means that, in Sass, the variable’s scopes fully depend on the code’s structure.

However, CSS custom properties are inherited by default, and like other CSS properties, they cascade.

You also cannot have a global variable that declares a custom property outside of a selector — that’s not valid CSS. The global scope for CSS custom properties is actually the <code>:root</code> scope, whereupon the property is available globally.

Let’s use our syntax knowledge and adapt the Sass example to HTML and CSS. We’ll create a demo using native CSS custom properties. First, the HTML:

<pre><code class="language-markup">global
&lt;div class="enclosing"&gt;
  enclosing
  &lt;div class="closure"&gt;
    closure
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

And here is the CSS:

<pre><code class="language-css">:root {
  --globalVar: 10px;
}

.enclosing {
  --enclosingVar: 20px;
}

.enclosing .closure {
  --closureVar: 30px;

  font-size: calc(var(--closureVar) + var(--enclosingVar) + var(--globalVar));
  /* 60px for now */
}
</code></pre>

<figure>{{< codepen height="170" theme_id="0" slug_hash="MJmebz" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/MJmebz/'>css-custom-properties-time-to-start-using 1</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

### Changes to Custom Properties Are Immediately Applied to All Instances

So far, we haven’t seen how this is any different from Sass variables. However, let’s reassign the variable after its usage:

In the case of Sass, this has no effect:

<pre><code class="language-scss">.closure {
  $closureVar: 30px; // local variable
  font-size: $closureVar +$enclosingVar+ $globalVar;
  // 60px, $closureVar: 30px is used

  $closureVar: 50px; // local variable
}
</code></pre>

<figure>{{< codepen height="170" theme_id="0" slug_hash="bgWerv" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/bgWerv/'>css-custom-properties-time-to-start-using 3</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

But in CSS, the calculated value is changed, because the <code>font-size</code> value is recalculated from the changed <code>--closureVar</code> value:

<pre><code class="language-css">.enclosing .closure {
  --closureVar: 30px;

  font-size: calc(var(--closureVar) + var(--enclosingVar) + var(--globalVar));
  /* 80px for now, --closureVar: 50px is used */

  --closureVar: 50px;
}
</code></pre>

<figure>{{< codepen height="190" theme_id="0" slug_hash="WRjxOy" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/WRjxOy/'>css-custom-properties-time-to-start-using 2</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

That’s the first huge difference: If you reassign a custom property’s value, the browser will <strong>recalculate all variables and <code>calc()</code> expressions</strong> where it’s applied.</p>

### Preprocessors Are Not Aware of the DOM’s Structure

Suppose we wanted to use the default <code>font-size</code> for the block, except where the <code>highlighted</code> class is present.

Here is the HTML:

<pre><code class="language-markup">&lt;div class="default"&gt;
  default
&lt;/div&gt;

&lt;div class="default highlighted"&gt;
  default highlighted
&lt;/div&gt;
</code></pre>

Let’s do this using CSS custom properties:

<pre><code class="language-css">.highlighted {
  --highlighted-size: 30px;
}

.default {
  --default-size: 10px;

  /* Use default-size, except when highlighted-size is provided. */
  font-size: var(--highlighted-size, var(--default-size));
}
</code></pre>

Because the second HTML element with the <code>default</code> class carries the <code>highlighted</code> class, properties from the <code>highlighted</code> class will be applied to that element.

In this case, it means that <code>--highlighted-size: 30px;</code> will be applied, which in turn will make the <code>font-size</code> property being assigned use the <code>--highlighted-size</code>.

Everything is straightforward and works:

<figure>{{< codepen height="100" theme_id="0" slug_hash="ggWMvG" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/ggWMvG/'>css-custom-properties-time-to-start-using 4</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

Now, let’s try to achieve the same thing using Sass:

<pre><code class="language-scss">.highlighted {
  $highlighted-size: 30px;
}

.default {
  $default-size: 10px;

  /* Use default-size, except when highlighted-size is provided. */
  @if variable-exists(highlighted-size) {
    font-size: $highlighted-size;
  }
  @else {
    font-size: $default-size;
  }
}
</code></pre>

The result shows that the default size is applied to both:

<figure>{{< codepen height="100" theme_id="0" slug_hash="PWmzQO" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/PWmzQO/'>css-custom-properties-time-to-start-using 5</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

This happens because all Sass calculations and processing happen at compilation time, and of course, it doesn’t know anything about the DOM’s structure, relying fully on the code’s structure.

As you can see, custom properties have the advantages of variables scoping and add the usual cascading of CSS properties, being aware of the DOM’s structure and following the same rules as other CSS properties.

The second takeaway is that CSS custom properties are <strong>aware of the DOM’s structure and are dynamic</strong>.</p>

## CSS-Wide Keywords And The `all` Property

CSS custom properties are subject to the same rules as the usual CSS custom properties. This means you can assign any of the common CSS keywords to them:

*   `inherit`  
This CSS keyword applies the value of the element’s parent.
*   `initial`  
This applies the initial value as defined in the CSS specification (an empty value, or nothing in some cases of CSS custom properties).
*   `unset`  
This applies the inherited value if a property is normally inherited (as in the case of custom properties) or the initial value if the property is normally not inherited.
*   `revert`  
This resets the property to the default value established by the user agent’s style sheet (an empty value in the case of CSS custom properties).

Here is an example:

<pre><code class="language-css">.common-values{
  --border: inherit;
  --bgcolor: initial;
  --padding: unset;
  --animation: revert;
}
</code></pre>

Let’s consider another case. Suppose you want to build a component and want to be sure that no other styles or custom properties are applied to it inadvertently (a modular CSS solution would usually be used for styles in such a case).

But now there is another way: to use the <a href="https://developer.mozilla.org/en/docs/Web/CSS/all"><code>all</code> CSS property</a>. This shorthand resets all CSS properties.

Together with CSS keywords, we can do the following:

<pre><code class="language-css">.my-wonderful-clean-component{
  all: initial;
}
</code></pre>

This reset all styles for our component.

Unfortunately, the <code>all</code> keyword <a href="https://drafts.csswg.org/css-variables/#defining-variables">doesn’t reset custom properties</a>. There is an ongoing <a href="https://github.com/w3c/webcomponents/issues/300#issuecomment-144551648">discussion about whether to add the <code>-&#8203;-</code> prefix</a>, which would reset all CSS custom properties.

So, in future, a full reset might be done like this:

<pre><code class="language-css">.my-wonderful-clean-component{
  --: initial; /* reset all CSS custom properties */
  all: initial; /* reset all other CSS styles */
}
</code></pre>

## CSS Custom Properties Use Cases

There are many uses of custom properties. I will show the most interesting of them.</p>

### Emulate Non-Existent CSS Rules

The name of these CSS variables is “custom properties,” so why not to use them to emulate non-existent properties?

There are many of them: <code>translateX/Y/Z</code>, <code>background-repeat-x/y</code> (still not cross-browser compatible), <code>box-shadow-color</code>.

Let’s try to make the last one work. In our example, let’s change the box-shadow’s color on hover. We just want to follow the DRY rule (don’t repeat yourself), so instead of repeating <code>box-shadow</code>’s entire value in the <code>:hover</code> section, we’ll just change its color. Custom properties to the rescue:

<pre><code class="language-css">.test {
  --box-shadow-color: yellow;
  box-shadow: 0 0 30px var(--box-shadow-color);
}

.test:hover {
  --box-shadow-color: orange;
  /* Instead of: box-shadow: 0 0 30px orange; */
}
</code></pre>

<figure>{{< codepen height="200" theme_id="0" slug_hash="KzZXRq" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/KzZXRq/'>Emulating "box-shadow-color" CSS property using CSS Custom Properties</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

### Color Themes

One of the most common use cases of custom properties is for color themes in applications. Custom properties were created to solve just this kind of problem. So, let’s provide a simple color theme for a component (the same steps could be followed for an application).

Here is the <a href="https://codepen.io/malyw/pen/XpRjNK">code for our button component</a>:

<pre><code class="language-css">.btn {
  background-image: linear-gradient(to bottom, #3498db, #2980b9);
  text-shadow: 1px 1px 3px #777;
  box-shadow: 0px 1px 3px #777;
  border-radius: 28px;
  color: #ffffff;
  padding: 10px 20px 10px 20px;
}
</code></pre>

Let’s assume we want to invert the color theme.

The first step would be to extend all of the color variables to CSS custom properties and rewrite our component. So, the <a href="https://codepen.io/malyw/pen/EZmgmZ">result would be the same</a>:

<pre><code class="language-css">.btn {
  --shadow-color: #777;
  --gradient-from-color: #3498db;
  --gradient-to-color: #2980b9;
  --color: #ffffff;

  background-image: linear-gradient(
    to bottom,
    var(--gradient-from-color),
    var(--gradient-to-color)
  );
  text-shadow: 1px 1px 3px var(--shadow-color);
  box-shadow: 0px 1px 3px var(--shadow-color);
  border-radius: 28px;
  color: var(--color);
  padding: 10px 20px 10px 20px;
}
</code></pre>

This has everything we need. With it, we can override the color variables to the inverted values and apply them when needed. We could, for example, add the global <code>inverted</code> HTML class (to, say, the <code>body</code> element) and change the colors when it’s applied:

<pre><code class="language-css">body.inverted .btn{
  --shadow-color: #888888;
  --gradient-from-color: #CB6724;
  --gradient-to-color: #D67F46;
  --color: #000000;
}
</code></pre>

Below is a demo in which you can click a button to add and remove a global class:

<figure>{{< codepen height="150" theme_id="0" slug_hash="dNWpRd" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/dNWpRd/'>css-custom-properties-time-to-start-using 9</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

This behavior cannot be achieved in a CSS preprocessor without the overhead of duplicating code. With a preprocessor, you would always need to override the actual values and rules, which always results in additional CSS.

With CSS custom properties, the solution is as clean as possible, and copying and pasting is avoided, because only the values of the variables are redefined.</p>

## Using Custom Properties With JavaScript

Previously, to send data from CSS to JavaScript, we often had to <a href="https://blog.hospodarets.com/passing_data_from_sass_to_js">resort to tricks</a>, writing CSS values via plain JSON in the CSS output and then reading it from the JavaScript.

Now, we can easily interact with CSS variables from JavaScript, reading and writing to them using the well-known <code>.getPropertyValue()</code> and <code>.setProperty()</code> methods, which are used for the usual CSS properties:

<pre><code class="language-javascript">/**
* Gives a CSS custom property value applied at the element
* element {Element}
* varName {String} without '--'
*
* For example:
* readCssVar(document.querySelector('.box'), 'color');
*/
function readCssVar(element, varName){
  const elementStyles = getComputedStyle(element);
  return elementStyles.getPropertyValue(`--${varName}`).trim();
}

/**
* Writes a CSS custom property value at the element
* element {Element}
* varName {String} without '--'
*
* For example:
* readCssVar(document.querySelector('.box'), 'color', 'white');
*/
function writeCssVar(element, varName, value){
  return element.style.setProperty(`--${varName}`, value);
}
</code></pre>

Let’s assume we have a list of media-query values:

<pre><code class="language-css">.breakpoints-data {
  --phone: 480px;
  --tablet: 800px;
}
</code></pre>

Because we only want to reuse them in JavaScript — for example, in <a href="https://developer.mozilla.org/en/docs/Web/API/Window/matchMedia">Window.matchMedia()</a> — we can easily get them from CSS:

<pre><code class="language-javascript">const breakpointsData = document.querySelector('.breakpoints-data');

// GET
const phoneBreakpoint = getComputedStyle(breakpointsData)
  .getPropertyValue('--phone');
</code></pre>

To show how to assign custom properties from JavaScript, I’ve created an interactive 3D CSS cube demo that responds to user actions.

It’s not very hard. We just need to add a simple background, and then place five cube faces with the relevant values for the <code>transform</code> property: <code>translateZ()</code>, <code>translateY()</code>, <code>rotateX()</code> and <code>rotateY()</code>.

To provide the right perspective, I added the following to the page wrapper:

<pre><code class="language-css">#world{
  --translateZ:0;
  --rotateX:65;
  --rotateY:0;

  transform-style:preserve-3d;
  transform:
    translateZ(calc(var(--translateZ) * 1px))
    rotateX(calc(var(--rotateX) * 1deg))
    rotateY(calc(var(--rotateY) * 1deg));
}
</code></pre>

The only thing missing is the interactivity. The demo should change the X and Y viewing angles (<code>--rotateX</code> and <code>--rotateY</code>) when the mouse moves and should zoom in and out when the mouse scrolls (<code>--translateZ</code>).

Here is the JavaScript that does the trick:

<pre><code class="language-javascript">// Events
onMouseMove(e) {
  this.worldXAngle = (.5 - (e.clientY / window.innerHeight)) * 180;
  this.worldYAngle = -(.5 - (e.clientX / window.innerWidth)) * 180;
  this.updateView();
};

onMouseWheel(e) {
  /*…*/

  this.worldZ += delta * 5;
  this.updateView();
};

// JavaScript -&gt; CSS
updateView() {
  this.worldEl.style.setProperty('--translateZ', this.worldZ);
  this.worldEl.style.setProperty('--rotateX', this.worldXAngle);
  this.worldEl.style.setProperty('--rotateY', this.worldYAngle);
};
</code></pre>

Now, when the user moves their mouse, the demo changes the view. You can check this by moving your mouse and using mouse wheel to zoom in and out:

<figure>{{< codepen height="500" theme_id="0" slug_hash="xgdEQp" default_tab="result" user="malyw" >}}See the Pen <a href='https://codepen.io/malyw/pen/xgdEQp/'>css-custom-properties-time-to-start-using 10</a> by Serg Hospodarets (<a href='https://codepen.io/malyw'>@malyw</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}</figure>

Essentially, we’ve just changed the CSS custom properties’ values. Everything else (the rotating and zooming in and out) is done by CSS.</p>

<strong>Tip:</strong> One of the easiest ways to debug a CSS custom property value is just to show its contents in CSS generated content (which works in simple cases, such as with strings), so that the browser will automatically show the current applied value:

<pre><code class="language-css">body:after {
  content: '--screen-category : 'var(--screen-category);
}
</code></pre>

You can check it <a href="https://codepen.io/malyw/pen/oBWMOY">in the plain CSS demo</a> (no HTML or JavaScript). (Resize the window to see the browser reflect the changed CSS custom property value automatically.)

## Browser Support

CSS custom properties are <a href="https://caniuse.com/#feat=css-variables">supported in all major browsers</a>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a6fd2d9-ab90-4059-a355-d17f15c3d1ca/css-variables-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47f90569-ec87-43bf-91b1-460c5c539739/css-variables-780w-opt.png" alt="" width="780" height="412" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a6fd2d9-ab90-4059-a355-d17f15c3d1ca/css-variables-large-opt.png">View large version</a>)</figcaption></figure>

This means that, you can start using them natively.

If you need to support older browsers, you can learn the syntax and usage examples and consider possible ways of switching or using CSS and preprocessor variables in parallel.

Of course, we need to be able to detect support in both CSS and JavaScript in order to provide fallbacks or enhancements.

This is quite easy. For CSS, you can use a <a href="https://developer.mozilla.org/en/docs/Web/CSS/@supports"><code>@supports</code> condition</a> with a dummy feature query:

<pre><code class="language-css">@supports ( (--a: 0)) {
  /* supported */
}

@supports ( not (--a: 0)) {
  /* not supported */
}
</code></pre>

In JavaScript, you can use the same dummy custom property with the <code>CSS.supports()</code> static method:

<pre><code class="language-javascript">const isSupported = window.CSS &amp;&amp;
    window.CSS.supports &amp;&amp; window.CSS.supports('--a', 0);

if (isSupported) {
  /* supported */
} else {
  /* not supported */
}
</code></pre>

As we saw, CSS custom properties are still not available in every browser. Knowing this, you can progressively enhance your application by checking if they are supported.

For instance, you could generate two main CSS files: one with CSS custom properties and a second without them, in which the properties are inlined (we will discuss ways to do this shortly).

Load the second one by default. Then, just do a check in JavaScript and switch to the enhanced version if custom properties are supported:

<pre><code class="language-markup">&lt;!-- HTML --&gt;
&lt;link href="without-css-custom-properties.css"
    rel="stylesheet" type="text/css" media="all" /&gt;
</code></pre>

<pre><code class="language-javascript">// JavaScript
if(isSupported){
  removeCss('without-css-custom-properties.css');
  loadCss('css-custom-properties.css');
  // + conditionally apply some application enhancements
  // using the custom properties
}
</code></pre>

This is just an example. As you’ll see below, there are better options.</p>

## How To Start Using Them

According to a <a href="https://ashleynolan.co.uk/blog/frontend-tooling-survey-2016-results">recent survey</a>, Sass continues to be the preprocessor of choice for the development community.

So, let’s consider ways to start using CSS custom properties or to prepare for them using Sass.

We have a few options.</p>

### 1. Manually Check in the Code for Support

One advantage of this method of manually checking in the code whether custom properties are supported is that it works and we can do it right now (don’t forget that we have switched to Sass):

<pre><code class="language-scss">$color: red;
:root {
  --color: red;
}

.box {
  @supports ( (--a: 0)) {
    color: var(--color);
  }
  @supports ( not (--a: 0)) {
    color: $color;
  }
}
</code></pre>

This method does have many cons, not least of which are that the code gets complicated, and copying and pasting become quite hard to maintain.</p>

### 2. Use a Plugin That Automatically Processes the Resulting CSS

The PostCSS ecosystem provides dozens of plugins today. A couple of them process custom properties (inline values) in the resulting CSS output and make them work, assuming you provide only global variables (i.e. you only declare or change CSS custom properties inside the <code>:root</code> selector(s)), so their values can be easily inlined.

An example is <a href="https://github.com/postcss/postcss-custom-properties">postcss-custom-properties</a>.

This plugin offers several pros: It makes the syntax work; it is compatible with all of PostCSS’ infrastructure; and it doesn’t require much configuration.

There are cons, however. The plugin requires you to use CSS custom properties, so you don’t have a path to prepare your project for a switch from Sass variables. Also, you won’t have much control over the transformation, because it’s done after the Sass is compiled to CSS. Finally, the plugin doesn’t provide much debugging information.</p>

### 3. [css-vars Mixin](https://github.com/malyw/css-vars)

I started using CSS custom properties in most of my projects and have tried many strategies:

*   Switch from Sass to PostCSS with [cssnext](https://cssnext.io/).
*   Switch from Sass variables to pure CSS custom properties.
*   Use CSS variables in Sass to detect whether they are supported.

As a result of that experience, I started looking for a solution that would satisfy my criteria:

*   It should be easy to start using with Sass.
*   It should be straightforward to use, and the syntax must be as close to native CSS custom properties as possible.
*   Switching the CSS output from the inlined values to the CSS variables should be easy.
*   A team member who is familiar with CSS custom properties would be able to use the solution.
*   There should be a way to have debugging information about edge cases in the usage of variables.

As a result, I created css-vars, a Sass mixin that you can <a href="https://github.com/malyw/css-vars">find on Github</a>. Using it, you can sort of start using CSS custom properties syntax.</p>

## Using css-vars Mixin

To declare variable(s), use the mixin as follows:

<pre><code class="language-scss">$white-color: #fff;
$base-font-size: 10px;

@include css-vars((
  --main-color: #000,
  --main-bg: $white-color,
  --main-font-size: 1.5*$base-font-size,
  --padding-top: calc(2vh + 20px)
));
</code></pre>

To use these variables, use the <code>var()</code> function:

<pre><code class="language-scss">body {
  color: var(--main-color);
  background: var(--main-bg, #f00);
  font-size: var(--main-font-size);
  padding: var(--padding-top) 0 10px;
}
</code></pre>

This gives you a way to control all of the CSS output from one place (from Sass) and start getting familiar with the syntax. Plus, you can reuse Sass variables and logic with the mixin.

When all of the browsers you want to support work with CSS variables, then all you have to do is add this:

<pre><code class="language-scss">$css-vars-use-native: true;
</code></pre>

Instead of aligning the variable properties in the resulting CSS, the mixin will start registering custom properties, and the <code>var()</code> instances will go to the resulting CSS without any transformations. This means you’ll have fully switched to CSS custom properties and will have all of the advantages we discussed.

If you want to turn on the useful debugging information, add the following:

<pre><code class="language-scss">$css-vars-debug-log: true;
</code></pre>

This will give you:

*   a log when a variable was not assigned but was used;
*   a log when a variable is reassigned;
*   information when a variable is not defined but a default value gets passed that is used instead.</p>

## Conclusion

Now you know more about CSS custom properties, including their syntax, their advantages, good usage examples and how to interact with them from JavaScript.

You have learned how to detect whether they are supported, how they are different from CSS preprocessor variables, and how to start using native CSS variables until they are supported across browsers.

This is the right time to start using CSS custom properties and to prepare for their native support in browsers.

{{< signature "rb, vf, al, il" >}}

