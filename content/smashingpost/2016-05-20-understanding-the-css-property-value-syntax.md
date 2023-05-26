---
title: Understanding The CSS Property Value Syntax
slug: understanding-the-css-property-value-syntax
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/885cb3de-1faa-4aaf-bdf0-72918b37f226/understanding-syntax-image-opt.jpg
date: 2016-05-20T21:00:15.000Z
author: russweakley
description: >-
  The _World Wide Web Consortium_ uses a particular syntax to define the
  possible values that can be used for all CSS properties. You may have seen
  this syntax in action if you have ever looked at a CSS specification.
categories:
  - Coding
  - CSS
---
The <em>World Wide Web Consortium</em> uses a particular syntax to define the possible values that can be used for all CSS properties. You may have seen this syntax in action if you have ever looked at a CSS specification — as in the <a href="https://www.w3.org/TR/css3-border/#the-border-image-slice">syntax for <code>border-image-slice</code></a>. Let's take a look:

<pre><code class="language-html">&lt;'border-­image-­slice'&gt; = [&lt;number&gt; | &lt;percentage&gt;]{1,4} &amp;&amp; fill?
</code></pre>

This syntax can be hard to understand if you don’t know the various symbols and how they work. However, it is worth taking the time to learn. If you understand how the W3C defines property values, you will be able to understand any of the W3C’s <a href="https://www.w3.org/Style/CSS/specs.en.html">CSS specifications</a>.

<figure><img title="Understanding The CSS Property Value Syntax" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/885cb3de-1faa-4aaf-bdf0-72918b37f226/understanding-syntax-image-opt.jpg" alt="Understanding The CSS Property Value Syntax" width="500" height="301" /></figure>

## Backus-Naur Form

We will start with a look at Backus-Naur Form, because this will help us understand the W3C’s property value syntax.

{{% feature-panel %}}

<a href="https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form">Backus–Naur Form</a> (BNF) is a formal notation used to describe the syntax of computer languages. It is designed to be unambiguous, so that there is no disagreement or ambiguity as to how the language can be expressed.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Introduction To PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)
*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)
*   [Creating Responsive Shapes With Clip-Path](https://www.smashingmagazine.com/2015/05/creating-responsive-shapes-with-clip-path/)

A wide range of extensions and variants of the original Backus–Naur notation are used today, including <a href="https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_Form">Extended Backus–Naur Form</a> (EBNF) and <a href="https://en.wikipedia.org/wiki/Augmented_Backus%E2%80%93Naur_Form">Augmented Backus–Naur Form</a> (ABNF).

A BNF specification is a set of rules written in the following way:

<pre><code class="language-html">&lt;symbol&gt;  ::=  __expression__
</code></pre>

On the left there is always a non-terminal symbol, followed by a <code>::=</code> symbol, which means “may be replaced with.” On the right is the <code>__expression__</code>, which consists of one or more sequences of symbols that are used to derive the meaning of the symbol on the left.

BNF specifications basically say, “Whatever is on the left may be replaced with whatever is on the right.”

## Non-Terminal And Terminal Symbols

Non-terminal symbols are symbols that can be replaced or broken down further. In BNF, non-terminal symbols appear between angled brackets, <code>&lt;</code> and <code>&gt;</code>. In the example below, <code>&lt;integer&gt;</code> and <code>&lt;digit&gt;</code> are non-terminal symbols.

<pre><code class="language-html">&lt;integer&gt;  ::=  &lt;digit&gt; | &lt;digit&gt;&lt;integer&gt;
</code></pre>

A terminal symbol indicates that the value cannot be replaced or broken down further. In the example below, all of the digital values are terminal symbols.

<pre><code class="language-html">&lt;digit&gt;  ::=  0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
</code></pre>

## The CSS Property Value Syntax

While the W3C’s CSS property value syntax is based on the concept of BNF, it has some differences. Like BNF, it begins with a non-terminal symbol. Unlike BNF, it describes symbols used within the expression as “component values.”

In the example below, <code>&lt;line-width&gt;</code> is a non-terminal symbol, and <code>&lt;length&gt;</code>, <code>thin</code>, <code>medium</code> and <code>thick</code> are component values.

<pre><code class="language-html">&lt;line-­width&gt;  =  &lt;length&gt; | thin | medium | thick
</code></pre>

## Component Values

There are four types of component values: keywords, basic data types, property data types and non-property data types.</p>

### 1. Keyword Values

Keyword values appear without quotation marks or angle brackets. They are used as is, as property values. Because they cannot be replaced or broken down further, they are terminal. In the example below, <code>thin</code>, <code>medium</code> and <code>thick</code> are all keyword values. This means they can be used as is, as values in our <a href="https://www.smashingmagazine.com/2015/08/understanding-critical-css/">CSS</a>.

<pre><code class="language-html">&lt;line-­width&gt;  =  &lt;length&gt; | thin | medium | thick
</code></pre>

### 2. Basic Data Types

Basic data types define core values such as <code>&lt;length&gt;</code> and <code>&lt;color&gt;</code>. They are non-terminal because they can be replaced with actual length or color values. In the example below, the <code>&lt;color&gt;</code> symbol is a basic data type.

<pre><code class="language-html">&lt;'background-color'&gt;  =  &lt;color&gt;
</code></pre>

This <code>&lt;color&gt;</code> value may be replaced in our CSS with an actual color value, using a keyword, an extended keyword, an RGB, RGBA, HSL or HSLA value, or the <code>transparent</code> keyword.

<pre><code class="language-css">.example { background-color: red; }
.example { background-color: honeydew; }
.example { background-color: rgb(50%,50%,50%); }
.example { background-color: rgba(100%,100%,100%,.5); }
.example { background-color: hsl(280,100%,50%); }
.example { background-color: hsla(280,100%,50%,0.5); }
.example { background-color: transparent; }
</code></pre>

### 3. Property Data Types

A property data type is a non-terminal symbol that defines the property’s actual name. It is defined using the property’s name (complete with quotation marks) set between angled brackets (<code>&lt;</code> … <code>&gt;</code>). In the example below, the <code>&lt;'border-width'&gt;</code> symbol is a property data type.

<pre><code class="language-html">&lt;'border-­width'&gt;  =  &lt;line-­width&gt;{1,4}
</code></pre>

Property data types may appear directly in our CSS as properties. In the example below, the <code>border-width</code> property is used to define a 2-pixel border for the <code>.example</code> class.

<pre><code class="language-css">.example { border-width: 2px; }
</code></pre>

### 4. Non-Property Data Types

A non-property data type is a non-terminal symbol that does not share the same name as a property. However, it defines aspects of one property or another. For example, <code>&lt;line-­width&gt;</code> is not a property, but it is a data type that defines the various <code>&lt;border&gt;</code> properties.

<pre><code class="language-html">
&lt;line-­width&gt;  =  &lt;length&gt; | thin | medium | thick

&lt;'border-­width'&gt;  =  &lt;line-­width&gt;{1,4}
</code></pre>

## Component Value Combinators

Component values can be arranged into property value combinators using one of the following five methods.</p>

### 1. Adjacent Values

Component values that are written one after another means that all of these values must occur in the given order. In the example below, the syntax lists three different values: <code>value1</code>, <code>value2</code> and <code>value3</code>. In the CSS rule, all three of these values must appear in the correct order for the property syntax to be valid.

<pre><code class="language-css">/* Component arrangement: all in given order */
&lt;'property'&gt; = value1 value2 value3

/* Example */
.example { property: value1 value2 value3; }
</code></pre>

### 2. Double Ampersand

A double ampersand (<code>&amp;&amp;</code>) separating two or more values means that all of them must occur, in any order. In the example below, the syntax lists two values, separated by a double ampersand. The CSS rules show that both of these values must appear but may appear in any order.

<pre><code class="language-css">/* Component arrangement: all, in any order */
&lt;'property'&gt; = value1 &amp;&amp; value2

/* Examples */
.example { property: value1 value2; }
.example { property: value2 value1; }
</code></pre>

### 3. Single Pipe

A single pipe (<code>|</code>) separating two or more values means that only one of them must occur. In the example below, the syntax lists three values, separated by single pipes. The following CSS rules show three possible options:

<pre><code class="language-css">/* Component arrangement: one of them must occur */
&lt;'property'&gt; = value1 | value2 | value3

/* Examples */
.example { property: value1; }
.example { property: value2; }
.example { property: value3; }
</code></pre>

### 4. Double Pipe

A double pipe (<code>||</code>) separating two or more options means that one or more of them must occur, in any order. In the example below, the syntax lists three values, separated by double pipes. Numerous options are available when you’re writing CSS rules to match this syntax — you could use one, two or three values, in any order.

<pre><code class="language-css">/* Component arrangement: one or more in any order */
&lt;'property'&gt; = value1 || value2 || value3

/* Examples */
.example { property: value1; }
.example { property: value2; }
.example { property: value3; }
.example { property: value1 value2; }
.example { property: value1 value2 value3; }
...etc
</code></pre>

### 5. Brackets

Brackets (<code>[ ]</code>) surrounding two or more alternatives means that the components inside are of a single grouping. In the example below, the syntax lists three values, but two of them appear inside brackets, so they are of a single group. Two options are available in the CSS rules: either <code>value1</code> and <code>value3</code> or <code>value2</code> and <code>value3</code>.

<pre><code class="language-css">/* Component arrangement: a single grouping */
&lt;'property'&gt; = [ value1 | value2 ] value3

/* Examples */
.example { property: value1 value3; }
.example { property: value2 value3; }
</code></pre>

## Component Value Multipliers

Component values may also be multiplied using one of the following eight methods.</p>

### 1. The `?` Symbol

A question mark (<code>?</code>) indicates that the preceding type, word or group is optional and occurs zero or one time. In the example below, the second value is placed inside brackets along with a comma. The question mark placed after this group means that <code>value1</code> must occur, but we could also use <code>value1</code> and <code>value2</code>, each separated by a comma.

<pre><code class="language-css">/* Component multiplier: zero or one time */
&lt;'property'&gt; = value1 [, value2 ]?

/* Examples */
.example { property: value1; }
.example { property: value1, value2; }
</code></pre>

### 2. The `*` Symbol

An asterisk (<code>*</code>) indicates that the preceding type, word or group occurs zero or more times. In the example below, the second value is placed inside brackets along with a comma. The asterisk placed after this group means that <code>value1</code> must occur, but we could also use <code>&lt;value2&gt;</code> as many times as we want, with each instance separated by a comma.

<pre><code class="language-css">/* Component multiplier: zero or more times */
&lt;'property'&gt; = value1 [, &lt;value2&gt; ]*

/* Examples */
.example { property: value1; }
.example { property: value1, &lt;value2&gt;; }
.example { property: value1, &lt;value2&gt;, &lt;value2&gt;; }
.example { property: value1, &lt;value2&gt;, &lt;value2&gt;, &lt;value2&gt;; }
...etc
</code></pre>

### 3. The `+` Symbol

A plus (<code>+</code>) indicates that the preceding type, word or group occurs one or more times. In the example below, the plus symbol placed after the value means that the value may be used more than once — without the need for commas.

<pre><code class="language-css">/* Component multiplier: one or more times */
&lt;'property'&gt; = &lt;value&gt;+

/* Examples */
.example { property: &lt;value&gt;; }
.example { property: &lt;value&gt; &lt;value&gt;; }
.example { property: &lt;value&gt; &lt;value&gt; &lt;value&gt;; }
...etc
</code></pre>

### 4. The `{A}` Symbol

A single number in braces (<code>{A}</code>) indicates that the preceding type, word or group occurs <code>A</code> times. In the example below, two instances of the value must be present in order for the declaration to be valid.

<pre><code class="language-css">/* Component multiplier: occurs A times */
&lt;'property'&gt; = &lt;value&gt;{2}

/* Examples */
.example { property: &lt;value&gt; &lt;value&gt;; }
</code></pre>

### 5. The `{A,B}` Symbol

A comma-separated pair of numbers in braces (<code>{A,B}</code>) indicates that the preceding type, word or group occurs at least <code>A</code> and at most <code>B</code> times. In the example below, a minimum of one value and a maximum of three values may be used to define the property. None of these values would be separated with a comma.

<pre><code class="language-css">/* Component multiplier: at least A and at most B */
&lt;'property'&gt; = &lt;value&gt;{1,3}

/* Examples */
.example { property: &lt;value&gt;; }
.example { property: &lt;value&gt; &lt;value&gt;; }
.example { property: &lt;value&gt; &lt;value&gt; &lt;value&gt;; }
</code></pre>

### 6. The `{A,}` Symbol

The <code>B</code> may be omitted in <code>{A,}</code> to indicate that there must be at least <code>A</code> repetitions, with no upper limit on the number of repetitions. In the example below, a minimum of one value must be used, but any number of additional values may also be used. None of these values would be separated with a comma.

<pre><code class="language-css">/* Component multiplier: at least A, with no upper limit */
&lt;'property'&gt; = &lt;value&gt;{1,}

/* Examples */
.example { property: &lt;value&gt;; }
.example { property: &lt;value&gt; &lt;value&gt;; }
.example { property: &lt;value&gt; &lt;value&gt; &lt;value&gt;; }
...etc
</code></pre>

### 7. The `#` Symbol

A hash (<code>#</code>) indicates that the preceding type, word or group occurs one or more times, separated by commas. In the example below, one or more values may be used, each separated by a comma.

<pre><code class="language-css">/* Component multiplier: one or more, separated by commas */
&lt;'property'&gt; = &lt;value&gt;#

/* Examples */
.example { property: &lt;value&gt;; }
.example { property: &lt;value&gt;, &lt;value&gt;; }
.example { property: &lt;value&gt;, &lt;value&gt;, &lt;value&gt;; }
...etc
</code></pre>

### 8. The `!` Symbol

An exclamation point <code>!</code> after a group indicates that the group is required and must produce at least one value. In the example below, <code>value1</code> is required, along with a value from the group comprising <code>value2</code> and <code>value3</code>. There may be only two values in total; so, the options are <code>value1</code> and <code>value2</code> or <code>value1</code> and <code>value3</code>.

<pre><code class="language-css">/* Component multiplier: required group, at least one value */
&lt;'property'&gt; = value1 [ value2 | value3 ]!

/* Examples */
.example { property: value1 value2; }
.example { property: value1 value3; }
</code></pre>

## The `<'text-shadow'>` Syntax: An Example

Let’s look at the <code>&lt;'text-shadow'&gt;</code> property as an example. This is how the property is defined in the <a href="https://www.w3.org/TR/css-text-decor-3/#text-shadow-property">specification</a>:

<pre><code class="language-html">&lt;'text-shadow'&gt; = none | [ &lt;length&gt;{2,3} &amp;&amp; &lt;color&gt;? ]#
</code></pre>

We can break down the various symbols:

*   The `|` indicates that we can use the keyword `none` or a group `[]`.
*   The `#` multiplier means that we can use one or more of these groups, separated by commas.
*   Inside the group, the `{2,3}` indicates that we can use two or three length values.
*   The `&&` indicates that we must include all values, but they can be included in any order.
*   Just to be tricky, the `<color>` value includes a `?` multiplier, which means that it may occur zero or one time.

In plain language, this could be written as following:
<blockquote>Specify none <strong>or</strong> one or more comma-separated groups that contain two to three length values and an optional color value. The length values and optional color value may be written in any order.</blockquote>

This means we could write the <code>text-shadow</code> property in a wide range of different ways. For example, we could set the <code>text-shadow</code> value to be <code>none</code>:

<pre><code class="language-css">.example { text-shadow: none; }</code></pre>

We could write two length values only, which would mean that we would be setting the horizontal and vertical offset of the shadow, but that it would have no blur radius or color value.

Because no blur radius has been defined, the initial value of <code>0</code> would be used; so, the shadow would be hard-edged. With no color defined, the color of the text would be used for the color of the shadow.

<pre><code class="language-css">.example { text-shadow: 10px 10px; }</code></pre>

If we used three length values, we would be defining the blur radius as well as the horizontal and vertical offsets of the shadow.

<pre><code class="language-css">.example { text-shadow: 10px 10px 10px; }</code></pre>

We could include a color, and it could go before or after the two or three length values. In the examples below, the red value could be placed at either end of the set of values.

<pre><code class="language-css">.example { text-shadow: 10px 10px 10px red; }
.example { text-shadow: red 10px 10px 10px; }
</code></pre>

Finally, we could include multiple text shadows, written as comma-separated groups. The shadow effects would be applied front to back: the first shadow on top and the others layered behind. The shadows cannot overlay the text itself. In the example below, the red shadow would sit on top of the lime shadow.

<pre><code class="language-css">.example {
    text-shadow:
        10px 10px red,
        -20px -20px 5px lime;
}
</code></pre>

## Conclusion

If you write CSS for a living, it is important to understand how to write valid CSS property values correctly. Once you understand how different values can be combined or multiplied, the CSS property value syntax becomes much easier to comprehend. It will then be easier to read the various specifications and to write valid CSS.

For further reading, check out the following websites:

*   “[Value Definition Syntax](https://www.w3.org/TR/css3-values/#value-defs)” in “CSS Values and Units Module Level 3,” W3C
*   “[CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference),” Mozilla Developer Network
*   “[How to Read W3C Specs](https://alistapart.com/article/readspec),” J. David Eisenberg, A List Apart

{{< signature "vf, al, il" >}}

