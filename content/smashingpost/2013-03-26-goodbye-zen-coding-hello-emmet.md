---
title: 'Goodbye, Zen Coding. Hello, Emmet!'
slug: goodbye-zen-coding-hello-emmet
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdce6ef1-6ba2-4919-a38e-053e6d00fa47/ellipsis-500.jpg
date: 2013-03-26T10:10:03.000Z
author: zeno-rocha
summary: >-
  Emmet, previously known as Zen Coding, is the most productive and time-saving text-editor plugin you will ever see. By instantly expanding simple abbreviations into complex code snippets, Emmet can turn you into a more productive developer.
description: >-
  Emmet, previously known as Zen Coding, is the most productive and time-saving text-editor plugin you will ever see. By instantly expanding simple abbreviations into complex code snippets, Emmet can turn you into a more productive developer.
categories:
  - Coding
  - CSS
  - Plugins
  - HTML
---
Back in 2009, Sergey Chikuyonok wrote an [article](https://www.smashingmagazine.com/2009/11/21/zen-coding-a-new-way-to-write-html-code/) on how to present a new way of writing HTML and CSS code. This revolutionary plugin (called *Zen Coding*) has helped many developers through the years and has now reached a new level.

For those who prefer to watch instead of read, here is a summary of my favorite tricks.

## How Does It Work?

Let’s face it: writing HTML code takes time, with all of those tags, attributes, quotes, braces, etc. Of course, most text editors have code completion, which helps a lot, but you still have to do a lot of typing. [Emmet](https://emmet.io) instantly expands simple abbreviations into complex code snippets.

## HTML Abbreviations

### Initializers

Getting started with a new HTML document takes less than a second now. Just type `!` or `html:5`, hit “Tab,” and you’ll see an HTML5 doctype with a few tags to jumpstart your application.

![Emmet Demonstration - Initializers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a2e08da-ab7d-4f78-93ca-4804a0f2c77c/initializers.gif)

*   `html:5` or `!` for an HTML5 doctype
*   `html:xt` for an XHTML transitional doctype
*   `html:4s` for an HTML4 strict doctype

{{% feature-panel %}}

### Easily Add Classes, IDs, Text and Attributes

Because Emmet’s syntax for describing elements is similar to CSS selectors, getting used to it is very easy. Try mixing an element’s name (e.g. `p`) with an identifier (e.g. `p#description`).

![Emmet Demonstration - Classes and IDs](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36fa04eb-1c5e-49c8-b911-93e1822c3bde/classes-ids.gif)

Also, you can combine classes and IDs. For example, `p.bar#foo` will output this:

<pre><code class="language-html">&lt;p class="bar" id="foo"&gt;&lt;/p&gt;
</code></pre>

Now let’s see how to define content and attributes for your HTML elements. Curly brackets are used for content. So, `h1{foo}` will produce this:

<pre><code class="language-html">&lt;h1&gt;foo&lt;/h1&gt;
</code></pre>

And square brackets are used for attributes. So, `a[href=#]` will generate this:

<pre><code class="language-html">&lt;a href="#"&gt;&lt;/a&gt;
</code></pre>

![Emmet Demonstration - Texts and Attributes](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8d84b80-38b7-4382-9231-e9d063638ca7/texts-attrs.gif)

### Nesting

By nesting abbreviations, you can build a whole page using just one line of code. First, the child operator, represented by `>`, allows you to nest elements. The sibling operator, represented by `+`, lets you place elements near each other, on the same level. Finally, the new climb-up operator, represented by `^`, allows you to climb up one level in the tree.

![Emmet Demonstration - Nesting operators](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a87378f5-fa92-46d0-b898-dfdf872059e1/nesting.gif)

### Grouping

To effectively take advantage of nesting without turning them into a confusing mess of operators, you’ll need to group some pieces of code. It’s like math — you just need to use parentheses around certain pieces. For example, `(.foo>h1)+(.bar>h2)` will output this:

<pre><code class="language-html">&lt;div class="foo"&gt;
  &lt;h1&gt;&lt;/h1&gt;
&lt;/div&gt;
&lt;div class="bar"&gt;
  &lt;h2&gt;&lt;/h2&gt;
&lt;/div&gt;
</code></pre>

![Emmet Demonstration - Grouping](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d303d8-9fd3-4264-8b75-5c2a1c4d9385/grouping.gif)

### Implicit Tag Names

To declare a tag with a class, just type `div.item`, and then it will generate `<div class="item"></div>`.

In the past, you could omit the tag name for a `div`; so, you just had to type `.item` and it would generate `<div class="item"></div>`. Now Emmet is more intelligent. It looks at the parent tag name every time you expand the abbreviation with an implicit name. So, if you declare `.item` inside of a `<ul>`, it will generate `<li class="item"></li>` instead of `<div class="item"></div>`.

![Emmet Demonstration - Implicit tag names](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21bd35b3-882e-4642-9578-c2f3bc33282a/implicit-tags.gif)

Here’s a list of all implicit tag names:

*   `li` for `ul` and `ol`
*   `tr` for `table`, `tbody`, `thead` and `tfoot`
*   `td` for `tr`
*   `option` for `select` and `optgroup`

{{% ad-panel-leaderboard %}}

### Multiplication

You can define how many times an element should be outputted by using the `*` operator. So, `ul>li*3` will produce:

<pre><code class="language-html">&lt;ul&gt;
  &lt;li&gt;&lt;/li&gt;
  &lt;li&gt;&lt;/li&gt;
  &lt;li&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

![Emmet Demonstration - Multiplication](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13da0cf1-d53e-4b91-854e-ba59a4242db4/multiplication.gif)

### Numbering

What about mixing the multiplication feature with some item numbering? Just place the `$` operator in the element’s name, the attribute’s name or the attribute’s value to output the number of currently repeated elements. If you write `ul>li.item$*3`, it will output:

<pre><code class="language-html">&lt;ul&gt;
  &lt;li class="item1"&gt;&lt;/li&gt;
  &lt;li class="item2"&gt;&lt;/li&gt;
  &lt;li class="item3"&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

![Emmet Demonstration - Numbering](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb9f8f8b-c6e3-40fa-a423-613a68fa3200/numbering.gif)

## Try It Now!

Why not try it right now? Go ahead: type in an Emmet HTML abbreviation, and hit the `Tab` key.</p>

## CSS Abbreviations

### Values

Emmet is about more than just HTML elements. You can inject values directly into CSS abbreviations, too. Let’s say you want to define a width. Type `w100`, and it will generate:

<pre><code class="language-css">width: 100px;
</code></pre>

![Emmet Demonstration - Values](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ba9d78b-6eeb-4d8a-b888-46357d4ab726/values.gif)

Pixel is not the only unit available. Try running `h10p+m5e`, and it will output:

<pre><code class="language-css">height: 10%;
margin: 5em;
</code></pre>

Here’s a list with a few aliases:

*   `p` → %
*   `e` → em
*   `x` → ex

### Extra Operator

You already know many intuitive abbreviations, such as `@f`, which produces:

<pre><code class="language-css">@font-face {
  font-family:;
  src:url();
}
</code></pre>

Some properties — such as `background-image`, `border-radius`, `font`, `@font-face`, `text-outline`, `text-shadow` — have some extra options that you can activate by using the `+` sign. For example, `@f+` will output:

<pre><code class="language-css">@font-face {
  font-family: 'FontName';
  src: url('FileName.eot');
  src: url('FileName.eot?#iefix') format('embedded-opentype'),
     url('FileName.woff') format('woff'),
     url('FileName.ttf') format('truetype'),
     url('FileName.svg#FontName') format('svg');
  font-style: normal;
  font-weight: normal;
}
</code></pre>

![Emmet Demonstration - Extra operator](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49eea769-2832-437f-8b90-710686aaf34b/extra.gif)

### Fuzzy Search

The CSS module uses fuzzy search to find unknown abbreviations. So, every time you enter an unknown abbreviation, Emmet will try to find the closest snippet definition. For example, `ov:h` and `ov-h` and `ovh` and `oh` will generate the same:

<pre><code class="language-css">overflow: hidden;
</code></pre>

![Emmet Demonstration - Fuzzy Search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5464ff7d-07fc-442d-8924-84c3cc2c576c/fuzzy-search.gif)

### Vendor Prefixes

CSS3 is awesome, but those vendor prefixes are a real pain for all of us. Well, not anymore — Emmet has abbreviations for them, too. For example, the `trs` abbreviation will expand to:

<pre><code class="language-css">-webkit-transform: ;
-moz-transform: ;
-ms-transform: ;
-o-transform: ;
transform: ;
</code></pre>

![Emmet Demonstration - Vendor Prefixes](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3355ac85-ea19-48ff-a164-e4402dbcdbe6/vendor-prefixes.gif)

You can also add prefixes to any kind of element. You just need to use the `-` prefix. So, `-super-foo` will expand to:

<pre><code class="language-css">-webkit-super-foo: ;
-moz-super-foo: ;
-ms-super-foo: ;
-o-super-foo: ;
super-foo: ;
</code></pre>

What if you don’t want all of those prefixes? No problem. You can define exactly which browsers to support. For example, `-wm-trf` will output:

<pre><code class="language-html">-webkit-transform: ;
-moz-transform: ;
transform: ;
</code></pre>

*   `w` → `-webkit-`
*   `m` → `-moz-`
*   `s` → `-ms-`
*   `o` → `-o-`

### Gradients

Speaking of annoying CSS3 features, we cannot forget gradients. Those long definitions with different notations can now be easily replaced with a concise, bulletproof abbreviation. Type `lg(left, #fff 50%, #000)`, and the output will be:

<pre><code class="language-css">background-image: -webkit-gradient(linear, 0 0, 100% 0, color-stop(0.5, #fff), to(#000));
background-image: -webkit-linear-gradient(left, #fff 50%, #000);
background-image: -moz-linear-gradient(left, #fff 50%, #000);
background-image: -o-linear-gradient(left, #fff 50%, #000);
background-image: linear-gradient(left, #fff 50%, #000);
</code></pre>

![Emmet Demonstration - Gradients](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df980dce-8e0f-45c1-83e4-6623e0ed1730/gradient.gif)

## Try It Now!

Had enough of the animated GIFs? Go ahead — type an Emmet CSS abbreviation, and hit the `Tab` key.</p>

## Extras

### Lorem Ipsum

Forget about those third-party services that generate “Lorem ipsum” text. Now you can do that right in your editor. Just use the `lorem` or `lipsum` abbreviations. You can specify how many words to generate. For instance, `lorem10` will output:

<pre><code class="language-html">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Libero delectus.
</code></pre>

![Emmet Demonstration - Lorem Ipsum](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03b4acf8-d93f-4ee2-8251-e8c37cc35128/lorem.gif)

Also, lorem can be chained to other elements. So, `p*3>lorem5` will generate:

<pre><code class="language-html">&lt;p&gt;Lorem ipsum dolor sit amet.&lt;/p&gt;
&lt;p&gt;Voluptates esse aliquam asperiores sunt.&lt;/p&gt;
&lt;p&gt;Fugiat eaque laudantium explicabo omnis!&lt;/p&gt;
</code></pre>

## Customization

Emmet offers a wide range of tweaks that you can use to fine-tune your plugin experience. There are three files you can edit to do this:

*   To add your own or to update an existing snippet, edit [snippets.json](https://docs.emmet.io/customization/snippets/).
*   To change the behavior of Emmet’s filters and actions, try editing [preferences.json](https://docs.emmet.io/customization/preferences/).
*   To define how generated HTML or XML should look, edit [syntaxProfiles.json](https://docs.emmet.io/customization/syntax-profiles/).</p>

{{% ad-panel-leaderboard %}}

## And A Lot More!

This is just the beginning. Emmet has a lot of other cool features, such as [encoding and decoding images to `data:URL`](https://docs.emmet.io/actions/base64/), [updating image sizes](https://docs.emmet.io/actions/update-image-size/) and [incrementing and decrementing numbers](https://docs.emmet.io/actions/inc-dec-number/).

Go check out the new [website](https://emmet.io), the awesome [documentation](https://docs.emmet.io/) and the handy [cheat sheet](https://docs.emmet.io/cheat-sheet/)!

## Supported Editors

If you are wondering, “Will it work in my text editor?,” The answer is, “Oh yes, my friend!” A lot of editors are supported, and I hope you find yours in the list below.

*   [Sublime Text 2](https://github.com/sergeche/emmet-sublime)
*   [TextMate 1.x](https://github.com/emmetio/Emmet.tmplugin)
*   [Eclipse/Aptana](https://github.com/emmetio/emmet-eclipse)
*   [Coda 1.6 and 2.x](https://github.com/emmetio/Emmet.codaplugin)
*   [Espresso](https://github.com/emmetio/Emmet.sugar)
*   [Chocolat](https://github.com/sergeche/emmet.chocmixin) (available via the “Install Mixin” dialog)
*   [Komodo Edit/IDE](https://github.com/emmetio/emmet/downloads) (available via `Tools → Add-ons`)
*   [Notepad++](https://github.com/emmetio/emmet/downloads)
*   [PSPad](https://github.com/emmetio/emmet/downloads)
*   [`<textarea>`](https://github.com/emmetio/emmet/downloads)
*   [CodeMirror2/3](https://github.com/emmetio/codemirror)
*   [Brackets](https://github.com/emmetio/brackets-emmet)

### And You?

What are your favorite tricks? Leave a comment below. Now it’s your turn to share your favorite tricks.

{{< signature "al, ea, il" >}}
