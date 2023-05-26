---
title: 'BEM For Beginners: Why You Need BEM'
slug: bem-for-beginners
author: inna-belaya
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a93b95e-3e4e-4367-86cb-0606ace15af3/sign-theme-batman.png
date: 2018-06-18T14:00:51+02:00
summary: >-
  CSS styles isolation is the most frequent start point of the BEM usage. But this is the least that BEM can give you. BEM brings a system approach in your project and keeps it from the mess.
description: >-
  CSS styles isolation is the most frequent start point of the BEM usage. But this is the least that BEM can give you. BEM brings a system approach in your project and keeps it from the mess.
categories:
  - Tools
  - Coding
  - CSS
---
BEM makes your code scalable and reusable, thus increasing productivity and facilitating teamwork. Even if you are the only member of the team, BEM can be useful for you. Nevertheless, many developers believe that such a system approach like BEM puts additional boundaries on their project and makes your project overloaded, cumbersome, and slow.

We’ll be collecting all of the main aspects of BEM in a condensed form. This article helps you understand the basic ideas of BEM in just 20 minutes, and to reject prejudices that the system approach is detrimental to your project.

The Big BEM consists of **Methodology**, **Technologies**, **Libraries**, and **Tools**. In this article, we’ll talk more about the methodology itself because it is the concentrated experience of a huge number of developers and it brings a systematic approach to any project. 

In order to show you some practical cases of BEM, we’ll touch on the BEM technologies and completely skip the libraries and tools.

From theory to practice:

- [The Main Reasons Why We Do Not Use Any Selectors Except Classes](#the-main-reasons-why-we-do-not-use-any-selectors-except-classes)
- [The Basics Of BEM](#the-basics-of-bem)
  * [Blocks And Elements](#block-and-elements)
  * [Modifiers And Mixes](#modifiers-and-mixes)
  * [Blocks In The File Structure](#blocks-in-the-file-structure)
- [Non-Evident Advantages Of The Methodology](#non-evident-advantages-of-the-methodology)
- [Practical Case: BEM Is Not Only For CSS](#practical-case-bem-is-not-only-for-css)
- [BEM Is A Customizable System](#bem-is-a-customizable-system)

So, is BEM a hero or a villain? It’s up to you! But first, read the article.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a93b95e-3e4e-4367-86cb-0606ace15af3/sign-theme-batman.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a93b95e-3e4e-4367-86cb-0606ace15af3/sign-theme-batman.png" sizes="100vw" caption="BEMBatman" alt="BEM as a Batman logo" >}}

{{% feature-panel %}}

## The Main Reasons Why We Do Not Use Any Selectors Except Classes

One of the basic rules of the BEM methodology is to use only class selectors. In this section, we’ll explain why.

- Why don’t we use IDs?
- Why don’t we use tag selectors?
- Why don’t we use a universal selector?
- Why don’t we use CSS reset?
- Why don’t we use nested selectors?
- Why don’t we combine a tag and a class in a selector?
- Why don’t we use combined selectors-
- Why don’t we use attribute selectors?

###  We Don’t Use IDs (ID Selectors)

The ID provides a unique name for an HTML element. If the name is unique, you can’t reuse it in the interface. This prevents you from reusing the code.

#### Common Misconceptions

1. **IDs are required for using JavaScript.**  
Modern browsers can work with either IDs or classes. Any type of selector is processed at the same rate in the browser.
2. **IDs are used with the  `<label>` tag.**  
If you place `<label>` inside a control, it doesn’t need an ID. Instead of `<input id="ID"><label for="ID">Text</label>`, simply use `<label><input type="...">Text</label>`.

### We Don’t Use Tag Selectors

HTML page markup is unstable: A new design can change the nesting of the sections, heading levels (for example, from `<h1>` to `<h3>`) or turn the `<p>` paragraph into the `<div>` tag. Any of these changes will break styles that are written for tags. Even if the design doesn’t change, the set of tags is limited. To use an existing layout in another project, you have to solve conflicts between styles written for the same tags.

An extended set of semantic tags can’t meet all layout needs, either.

An example is when the page header contains a logo. A click on the logo opens the main page of the site (`index`). You can mark it up with tags by using the `<img>` tag for the image and the `<a>` tag for the link.

<pre><code class="language-html">&lt;header&gt;
  &lt;a href="/"&gt;
    &lt;img src="img.logo.png" alt="Logo"&gt;
  &lt;/a&gt;
&lt;/header&gt;
</code></pre>

To distinguish between the logo link and an ordinary link in the text, you need extra styles. Now remove underlining and the blue color from the logo link:

<pre><code class="language-css">header a {
  ...
}
</code></pre>

The logo link doesn’t need to be shown on the main page, so change the index page markup:

<pre><code class="language-html">&lt;header&gt;
  &lt;!-- the &lt;a&gt; tag is replaced with &lt;span&gt; --&gt;
  &lt;span&gt;
    &lt;img src="img.logo.png" alt="Logo"&gt;
  &lt;/span&gt;
&lt;/header&gt;
</code></pre>

You don’t need to remove the underlining and the blue color for the `<span>` tag. So let’s make general rules for the logo link from different pages:

<pre><code class="language-css">header a,
header span
{
  ...
}
</code></pre>

At first glance, this code seems all right, but imagine if the designer removes the logo from the layout. The selector names don’t help you understand which styles should be removed from the project with the logo. The "header a" selector doesn’t show the connection between the link and the logo. This selector could belong to the link in the header menu or, for example, to the link to the author’s profile. The "header span" selector could belong to any part of the header.

To avoid confusion, just use  the `logo` class selector to write the logo styles:

<pre><code class="language-css">.logo {
  ...
}
</code></pre>

### We Don’t Use CSS Reset

CSS reset is a set of global CSS rules created for the whole page. These styles affect all layout nodes, violate the independence of components, and make it harder to reuse them.

In BEM, "reset" and "normalize" aren’t even used for a single block. Resetting and normalization cancel existing styles and replace them with other styles, which you will have to change and update later in any case. As a result, the developer has to write styles that override the ones that were just reset.

### We Don’t Use The Universal Selector (`*`)

The universal selector indicates that the project features a style that affects all nodes in the layout. This limits reuse of the layout in other projects:

- You have to additionally transfer the styles with an asterisk to the project. But in this case, the universal selector might affect the styles in the new project.
- The styles with an asterisk must be added to the layout you are transferring.

In addition, a universal selector can make the project code unpredictable. For example, it can affect the styles of the universal library components.

Common styles don’t save you time. Often developers start by resetting all margins for components (`* { margin: 0; padding: 0; }`), but then they still set them the same as in the layout (for example, `margin: 12px; padding: 30px;`).

### We Don’t Use Nested Selectors

Nested selectors increase code coupling and make it difficult to reuse the code.

The BEM methodology doesn’t prohibit nested selectors, but it recommends not to use them too much. For example, nesting is appropriate if you need to change styles of the elements depending on the block’s state or its assigned theme.

<pre><code class="language-css">.button_hovered .button__text
{
  text-decoration: underline;
}
.button_theme_islands .button__text
{
  line-height: 1.5;
}
</code></pre>

### We Don’t Use Combined Selectors

Combined selectors are more specific than single selectors, which makes it more difficult to redefine blocks.

Consider the following code:

<pre><code class="language-html">&lt;button class="button button_theme_islands"&gt;...&lt;/button&gt;
</code></pre>

Let’s say you set CSS rules in the `.button.button_theme_islands` selector to do less writing. Then you add the "active" modifier to the block:

<pre><code class="language-html">&lt;button class="button button_theme_islands button_active"&gt;...&lt;/button&gt;
</code></pre>

The `.button_active` selector doesn’t redefine the block properties written as `.button.button_theme_islands` because  `.button.button_theme_islands` is more specific than `.button_active`. To redefine it, combine the block modifier selector with the `.button` selector and declare it below the `.button.button_theme_islands` because both selectors are equally specific:

<pre><code class="language-css">.button.button_theme_islands {}
.button.button_active {}
</code></pre>

If you use simple class selectors, you won’t have problems redefining the styles:

<pre><code class="language-css">.button_theme_islands {}
.button_active {}
.button {}
</code></pre>

### We Don’t Combine A Tag And A Class In A Selector

Combining a tag and a class in the same selector (for example, `button.button`) makes CSS rules more specific, so it is more difficult to redefine them.

Consider the following code:

<pre><code class="language-html">&lt;button class="button"&gt;...&lt;/button&gt;
</code></pre>

Let’s say you set CSS rules in the `button.button` selector.
Then you add the `active` modifier to the block:

<pre><code class="language-css">&lt;button class="button button_active"&gt;...&lt;/button&gt;
</code></pre>

The `.button_active` selector doesn’t redefine the block properties written as `button.button` because  `button.button` is more specific than `.button_active`. To make it more specific, you should combine the block modifier selector with the `button.button_active` tag.

As the project develops, you might end up with blocks with `input.button`, `span.button` or `a.button` selectors. In this case, all modifiers of the `button` block and all its nested elements will require four different declarations for each instance.

#### Possible Exceptions

In rare cases, the methodology allows combining tag and class selectors. For example, this can be used for setting the comments style in CMS systems that can’t generate the correct layout.

You can use the comment to write a text, insert images, or add markup. To make them match the site design, the developer can pre-define styles for all tags available to the user and cascade them down to the nested blocks:

<pre><code class="language-html">&lt;div class="content"&gt;
  ... &lt;!-- the user’s text --&gt;
&lt;/div&gt;
CSS rules:
.content a {
  ...
}
.content p {
  font-family: Arial, sans-serif;
  text-align: center;
}
</code></pre>

### We Don’t Use Attribute Selectors

Attribute selectors are less informative than class selectors. As proof, consider an example with a search form in the header:

<pre><code class="language-html">&lt;header&gt;
  &lt;form action="/"&gt;
    &lt;input name="s"&gt;
    &lt;input type="submit"&gt;
  &lt;/form&gt;
&lt;/header&gt;
</code></pre>

Try using selector attributes to write the form styles:

<pre><code class="language-css">header input[type=submit],
header input[type=checkbox] {
  width: auto;
  margin-right: 20px;
}
header input[type=checkbox] {
  margin: 0;
}
</code></pre>

In this example, you can’t tell for sure from the selector name that the styles belong to the search form. Using classes makes it clearer. Classes don’t have restrictions that prevent you from writing clearly. For example, you can write it like this:

<pre><code class="language-css">.form .search {
  ...
}
</code></pre>

Now the code is less ambiguous, and it’s clear that the styles belong to the search form.

But the nested selectors still make the CSS rules more specific and prevent you from transferring the layout between projects. To get rid of nesting, use BEM principles.

**Summary**: *`class` is the only selector that allows you to isolate the styles of each component in the project; increase the readability of the code and do not limit the re-use of the layout.*

CSS styles isolation is the most frequent start point of the BEM journey. But this is the least that BEM can give you. To understand how isolated independent components are arranged in BEM, you need to learn the basic concepts, i.e. Block, Element, Modifier, and Mix. Let’s do this in the next section.

## The Basics Of BEM

- [Blocks And Elements](#block-and-elements)
- [Modifiers And Mixes](#modifiers-and-mixes)
- [Blocks In The File Structure](#blocks-in-the-file-structure)

### Block And Elements

The BEM methodology is a set of universal rules that can be applied regardless of the technologies used, such as CSS, Sass, HTML, JavaScript or React.

BEM helps to solve the following tasks:

- Reuse the layout;
- Move layout fragments around within a project safely;
- Move the finished layout between projects;
- Create stable, predictable and clear code;
- Reduce the project debugging time.

In a BEM project, the interface consists of [blocks](https://en.bem.info/methodology/key-concepts/#block) that can include [elements](https://en.bem.info/methodology/key-concepts/#element). Blocks are independent components of the page. An element can’t exist outside the block, so keep in mind that each element can belong to one block only.

The first two letters in BEM stand for **B**locks and **E**lements. The block name is always unique. It sets the namespace for elements and provides a visible connection between the block parts. Block names are long but clear in order to show the connection between components and to avoid losing any parts of these components when transferring the layout.

To see the full power of BEM naming, consider this example with a form. According to the BEM methodology, the form is implemented using the `form` block. In HTML, the block name is included in the `class` attribute:

<pre><code class="language-html">&lt;form class="form" action="/"&gt;
</code></pre>

All parts of the form (the `form` block) that don’t make sense on their own are considered its elements. So the search box (`search`) and the button (`submit`) are elements of the `form` block. Classes also indicate that an element belongs to the block:

<pre><code class="language-html">&lt;form class="form" action="/"&gt;
  &lt;input class="form__search" name="s"&gt;
  &lt;input class="form__submit" type="submit"&gt;
&lt;/form&gt;
</code></pre>

Note that the block’s name is separated from the element’s name with a special separator. In the BEM [classic naming scheme](https://en.bem.info/methodology/naming-convention/#naming-convention), two underscores are used as a separator. Anything can work as a separator. There are [alternative naming conventions](https://en.bem.info/methodology/naming-convention/#alternative-naming-conventions), and each developer chooses the one that suits them. The important thing is that separators allow you to distinguish blocks from elements and modifiers programmatically.

Selector names make it clear that in order to move the form to another project, you need to copy all of its components:

<pre><code class="language-css">.form__search {}
.form__submit {}
</code></pre>

Using blocks and elements for class names solves an important problem: It helps us get rid of nested selectors. All selectors in a BEM project have the same weight. That means it is much easier to redefine styles written according to BEM. Now, to use the same form in another project, you can just copy its layout and styles.

The idea of the [naming](https://en.bem.info/methodology/naming-convention/)  of BEM components is that you can explicitly define the connection between the block and its elements.

### Modifiers And Mixes

Officially, "M" stands for **M**odifier, but it also implies one more important notion in BEM: "mix". Both modifiers and mixes make changes to a block and its elements. Let’s take a closer look at this.

#### Modifiers

A [modifier](https://en.bem.info/methodology/key-concepts/#modifier) defines the look, state and behavior of a block or an element. Adding modifiers is optional. Modifiers let you combine different block features, as you can use any number of modifiers. But a block or an element can’t be assigned different values of the same modifier.

Let’s explore how modifiers work.

Imagine the project needs the same search form as in the example above. It should have the same functions but look different (for example, the search forms in the header and in the footer of the page should differ). The first thing you can do to change the appearance of the form is to write additional styles:

<pre><code class="language-css">header .form {}
footer .form {}
</code></pre>

The `header .form` selector has more weight than the `form` selector, which means that one rule will override the other one. But as we have discussed, nested selectors increase code coupling and make reuse difficult, so this approach doesn’t work for us.

In BEM, you can use a modifier to add new styles to the block:

<pre><code class="language-css">&lt;!-- Added the form_type_original modifier--&gt;
&lt;form class="form form_type_original" action="/"&gt;
  &lt;input class="form__search" name="s"&gt;
  &lt;input class="form__submit" type="submit"&gt;
&lt;/form&gt;
</code></pre>

The line `<form class="form form_type_original"></form>` indicates that the block was assigned a `type` modifier with the `original` value. In a classic scheme, the modifier name is separated from the block or element name with an underscore.

The form can have a unique color, size, type, or design theme. All these parameters can be set with a modifier:

<pre><code class="language-html">&lt;form class="form form_type_original form_size_m form_theme_forest"&gt;</form>
</code></pre>

The same form can look different but stay the same size:

<pre><code class="language-html">&lt;form class="form form_type_original form_size_m form_theme_forest"&gt;&lt;/form&gt;
&lt;form class="form form_type_original form_size_m form_theme_sun"&gt;&lt;/form&gt;
</code></pre>

But the selectors for each modifier will still have the same weight:

<pre><code class="language-css">.form_type_original {}
.form_size_m {}
.form_theme_forest {}
</code></pre>

**Important**: *A modifier contains only additional styles that change the original block implementation in some way. This allows you to set the appearance of a universal block only once, and add only those features that differ from the original block code into the modifier styles.*

<pre><code class="language-css">.form {
  /* universal block styles */
}
.form_type_original {
  /* added styles */
}
</code></pre>

This is why a modifier should always be on the same DOM node with the block and the element it is associated with.

<pre><code class="language-css">&lt;form class="form form_type_original"&gt;&lt;/form&gt;
</code></pre>

You can use modifiers to apply universal components in very specific cases. The block and element code doesn’t change. The necessary combination of modifiers is created on the DOM node.

#### Mixes

A [mix](https://en.bem.info/methodology/key-concepts/#mix) allows you to apply the same formatting to different HTML elements and combine the behavior and styles of several entities while avoiding code duplication. They can replace abstract wrapper blocks.

A mix means that you host several BEM entities (blocks, elements, modifiers) on a single DOM node. Similar to modifiers, mixes are used for changing blocks. Let’s look at some examples of when you should use a mix.

Blocks can differ not only visually but also semantically. For example, a search form, a registration form and a form for ordering cakes are all forms. In the layout, they are implemented with the "form" block but they don’t have any styles in common. It is impossible to handle such differences with a modifier.
You can define common styles for such blocks but you won’t be able to reuse the code.

<pre><code class="language-css">.form,
.search,
.register {
  ...
}
</code></pre>

You can use a mix to create semantically different blocks for the same form:

<pre><code class="language-html">&lt;form class="form" action="/"&gt;
  &lt;input class="form__search" name="s"&gt;
  &lt;input class="form__submit" type="submit"&gt;
&lt;/form&gt;
</code></pre>

The `.form` class selector describes all styles that can be applied to any form (order, search or registration):

<pre><code class="language-css">.form {}
</code></pre>

Now you can make a search form from the universal form. To do this, create an additional `search` class in the project. This class will be responsible only for the search. To combine the styles and behavior of the`.form`and`.search` classes, place these classes on a single DOM node:

<pre><code class="language-html"><!-- A mix of "form" and "search" blocks -->
&lt;form class="form search" action="/"&gt;
  &lt;input class="form__search" name="s"&gt;
  &lt;input class="form__submit" type="submit"&gt;
&lt;/form&gt;
</code></pre>

In this case, the `.search` class is a separate block that defines behavior. This block can’t have modifiers responsible for the form, themes, and sizes. These modifiers already belong to the universal form. A mix helps to combine the styles and behavior of these blocks.

Let’s take one more example where the component’s semantics is changed. Here is a navigation menu in the page header in which all entries are links:

<pre><code class="language-html">&lt;nav class="menu"&gt;
  &lt;a class="link" href=""&gt;&lt;/a&gt;
  &lt;a class="link" href=""&gt;&lt;/a&gt;
  &lt;a class="link" href=""&gt;&lt;/a&gt;
&lt;/nav&gt;
</code></pre>

The link functionality is already implemented in the `link` block, but the menu links have to differ visually from the links in the text. There are several ways to change the menu links:

<ol>
<li>Create a menu entry modifier that turns the entry into a link:<br />

<pre><code class="language-html">&lt;nav class="menu"&gt;
  &lt;a class="menu__item menu__item_link" href=""&gt;&lt;/a&gt;
  &lt;a class="menu__item menu__item_link" href=""&gt;&lt;/a&gt;
  &lt;a class="menu__item menu__item_link" href=""&gt;&lt;/a&gt;
&lt;/nav&gt;
</code></pre>
<br />In this case, to implement the modifier, you should copy the `link` block behavior and styles. This will lead to code duplication.</li>
<li>Use a mix of the `link` universal block and the `item` element of the `menu` block:<br />

<pre><code class="language-html">&lt;nav class="menu"&gt;
  &lt;a class="link menu__item" href=""&gt;&lt;/a&gt;
  &lt;a class="link menu__item" href=""&gt;&lt;/a&gt;
  &lt;a class="link menu__item" href=""&gt;&lt;/a&gt;
&lt;/nav&gt;
</code></pre>
<br />With the mix of the two BEM entities, you can now implement the basic link functionality from the `link` block and additional CSS rules from the `menu` block, and avoid code duplication.</li>
</ol>

#### External Geometry And Positioning: Giving Up Abstract HTML Wrappers

Mixes are used to position a block relative to other blocks or to position elements inside a block. In BEM, styles responsible for geometry and positioning are set in the parent block. Let’s take a universal menu block that has to be placed in the header. In the layout, the block has to have a 20px indent from the parent block.

This task has several solutions:

<ol>
<li>Write styles with indents for the menu block:<br />

<pre><code class="language-css">.menu {
  margin-left: 20px;
}
</code></pre>
<br />In this case, the "menu" block isn’t universal anymore. If you have to place the menu in the page footer, you will have to edit styles because the indents will probably be different.</li>
<li>Create the menu block modifier:<br />

<pre><code class="language-html">&lt;div&gt;
  &lt;ul class="menu menu_type_header"&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>

<pre><code class="language-css">.menu_type_header {
  margin-left: 20px;
}
.menu_type_footer {
  margin-left: 30px;
}
</code></pre>
<br />In this case, the project will include two kinds of menus, although this is not the case. The menu stays the same.</li>
<li>Define the external positioning of the block:  nest the `menu` block in the abstract wrapper (for example, the `wrap` block) setting all indents:<br />

<pre><code class="language-html">&lt;div class="wrap"&gt;
  &lt;ul class="menu"&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>
<br />To avoid the temptation to create modifiers and change the block styles to position the block on the page, you need to understand one thing:<br /><br />
<blockquote>The indent from a parent block isn’t a feature of the nested block. It is a feature of the parent block. It has to know that the nested block has to be indented from the border by a certain number of pixels.</blockquote></li>
<li>Use a mix. The information about nested block positioning is included in the parent block elements. Then the parent block element is mixed into the nested block. In this case, the nested block doesn’t specify any indents and can be easily reused in any place.</li>
</ol>

Let’s go on with our example:

<pre><code class="language-html">&lt;div&gt;
  &lt;ul class="menu header__menu"&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li class="menu__item"&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>

In this case, external geometry and positioning of the `menu` block are set through the `header__menu` element. The `menu` block doesn’t specify any indents and can be easily reused.

The parent block element (in our case it is `header__menu`) performs the task of the wrapper blocks responsible for external positioning of the block.

### Blocks In The File Structure

All BEM projects have a similar [file structure](https://en.bem.info/methodology/filestructure/). The familiar file structure makes it easier for developers to navigate the project, switch between projects, and move blocks from one project to another.

The implementation of each block is stored in a separate project folder. Each technology (CSS, JavaScript, tests, templates, documentation, images) is in a separate file.

For example, if the `input` block appearance is set with CSS, the code is saved in the `input.css` file.

<pre><code class="language-css">project
  common.blocks/
    input/
      input.css # The "input" block implementation with CSS
      input.js  # The "input" block implementation with JavaScript
</code></pre>

The code for modifiers and elements is also stored in separate files of the block. This approach allows you to include in the build only those modifiers and elements that are necessary for the implementation of the block.

<pre><code class="language-css">project
  common.blocks/
    input/
      input.css           # The "input" block implementation with CSS
      input.js            # The "input" block implementation with JavaScript
      input_theme_sun.css # The "input_theme_sun" modifier implementation
      input__clear.css    # The "input__clear" element implementation with CSS
      input__clear.js     # The "input__clear" element implementation with JavaScript
</code></pre>

To improve the project navigation, combine block modifiers with multiple values in directories.

The file structure of any BEM project consists of [redefinition levels](https://en.bem.info/methodology/key-concepts/#redefinition-level) (you can learn more on them over [here](https://en.bem.info/methodology/redefinition-levels/)). Redefinition levels allow you to:

- Divide the project into platforms;
- Easily update the block libraries included in the project;
- Use common blocks to develop multiple projects;
- Change the design themes without affecting the project logic;
- Conduct experiments in a live project.

Using blocks and storing all block technologies in the same folder makes it easy to move blocks between projects. To move all styles and behavior of the block together with the layout, just copy the block folder to the new project.

## Non-Evident Advantages Of The Methodology

### The Convenience Of Parallel Development

In BEM, any layout is divided into blocks. Because the blocks are independent, they can be developed in parallel by several developers.

A developer creates a block as a universal component that can be reused in any other project.

An example is the [bem-components](https://en.bem.info/platform/libs/bem-components/6.0.0/) block library, which contains universal blocks, such as a [link](https://en.bem.info/platform/libs/bem-components/6.0.0/desktop/link/), [button](https://en.bem.info/platform/libs/bem-components/6.0.0/desktop/button/), and [input field](https://en.bem.info/platform/libs/bem-components/6.0.0/desktop/input/). It is easier to create more complex blocks from universal components. For example, a [selector](https://en.bem.info/platform/libs/bem-components/6.0.0/desktop/select/) or [checkbox](https://en.bem.info/platform/libs/bem-components/6.0.0/desktop/checkbox/).

Using blocks in project layout helps you save the time on integrating code written by several developers, guarantees the uniqueness of component names, and lets you test blocks at the development stage.

### Testing The Layout

It is problematic to test the functionality of the whole page, especially in a dynamic project connected to a database.

In BEM, each block is covered by tests. Tests are a block implementation technology, like Javascript or CSS. Blocks are tested at the development stage. It is easier to check the correctness of one block and then assemble the project from tested blocks. After that, all you have to do is to make sure that the block wrapper is working correctly.

### Customizable Build Of A Project

For convenient development, all blocks and technologies in a BEM project are placed in separate folders and files. To combine the source files into a single file (for example, to put all CSS files in `project.css`, all JS files in `project.js`, and so on), we use the build process.

The build performs the following tasks:

- Combines source files that are spread out across the project’s file system;
- Includes only necessary blocks, elements, and modifiers (BEM entities) in the project;
- Follows the order for including entities;
- Processes the source file code during the build (e.g. compiles LESS code to CSS code).

To include only the necessary BEM entities in the build, you need to create a list of blocks, elements, and modifiers used on the pages. This list is called a **declaration**.

Since BEM blocks are developed independently and placed in separate files in the file system, they don’t 'know' anything about each other. To build blocks based on other blocks, specify dependencies. There is a BEM technology responsible for this: the `deps.js` files. Dependency files let the build engine know which additional blocks have to be included in the project.

## Practical Case: BEM Is Not Only For CSS

In the previous sections, all code examples are for CSS. But BEM allows you to modify the behavior of the block and its representation in HTML in the same declarative way like in CSS.

### How To Use Templating In BEM

In HTML, the block markup is repeated every time the block appears on the page. If you create the HTML markup manually and then need to fix an error or make changes, you will need to modify the markup for every instance of the block. To generate HTML code and apply fixes automatically, BEM uses templates; blocks are responsible for the way they are presented in HTML.

Templates allow you to:

- Reduce the time used for project debugging, because the template changes are automatically applied to all project blocks;
- Modify the block layout;
- Move blocks with the current layout to another project.

BEM uses the [bem-xjst](https://en.bem.info/platform/bem-xjst/8/) template engine which features two engines:

- **BEMHTML**  
Transforms the [BEMJSON](https://en.bem.info/platform/bemjson/) description of the page to HTML. The templates are described in .bemhtml.js files.
- **BEMTREE**  
Transforms data to BEMJSON. The templates are described in BEMJSON format in *.bemtree.js* files.

If templates aren’t written for the blocks, the template engine sets the `<div>` tag for the blocks by default.

Compare the declaration of the blocks and the HTML output:

Declaration:

<pre><code class="language-css">{
  block: 'menu',
  content: [
    {
      elem: 'item',
      content: {
        block: 'link'}
    },
    { 
      elem: 'item',
      elemMods: { current: true }, // Set the modifier for the menu item
      content: {
        block: 'link'
      }
    }
  ]
}
</code></pre>

HTML:

<pre><code class="language-html">&lt;div class="menu"&gt;
  &lt;div class="menu__item"&gt;
    &lt;div class="link"&gt;&lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="menu__item menu__item_current"&gt;
    &lt;div class="link"&gt;&lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

To modify the `menu` block layout, you need to write templates for the block:

<ol>
<li>Let’s change the <code>menu</code> block tag:<br />

<pre><code class="language-css">block('menu')(
  tag()('menu') // Set the "menu" tag for the menu block 
)
</code></pre>
<br />Modified HTML:<br />

<pre><code class="language-html">&lt;menu class="menu"&gt; &lt;!-- Replace the "div" tag with the "menu" tag for the "menu" block --&gt;
  &lt;div class="menu__item"&gt;
    &lt;div class="link"&gt;&lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="menu__item menu__item_current"&gt;
    &lt;div class="link"&gt;&lt;/div&gt;
  &lt;/div&gt;
&lt;/menu&gt;
</code></pre>
<br />Similar to CSS, the template is applied to all "menu" blocks on the page.</li>
<li>Add an extra element (<code>menu__inner</code>) that works as an inner wrapper and is responsible for the layout of the elements in the <code>menu</code> block. Originally the <code>menu__inner</code> element wasn’t included in the declaration, so we have to add it when the templates are built.<br /><br />BEM templates are written in JavaScript, so you can also use JavaScript to add a new element to the template:<br />

<pre><code class="language-css">block('menu')(
  tag()('menu'),
  content()(function() {
    return {
      elem: 'inner',
      content: this.ctx.content
    };
  })
)
</code></pre>

<pre><code class="language-html">&lt;menu class="menu"&gt; &lt;!-- Replace the "div" tag with the "menu" tag for the "menu" block --&gt;
  &lt;div class="menu__inner"&gt;
    &lt;div class="menu__item"&gt;
      &lt;div class="link"&gt;&lt;/div&gt;
    &lt;/div&gt;
    &lt;div class="menu__item menu__item_current"&gt;
      &lt;div class="link"&gt;&lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/menu&gt;
</code></pre>
</li>
<li>Replace tags for all <code>inner</code> and <code>item</code> elements:<br />

<pre><code class="language-css">block('menu')(
  tag()('menu'),
  content()(function() {
    return {
      elem: 'inner',
      content: this.ctx.content
    }
  }),
  elem('inner')(
    tag()('ul')
  ),
  elem('item')(
    tag()('li')
  )
)
</code></pre>

<pre><code class="language-html">&lt;menu class="menu"&gt;
  &lt;ul class="menu__inner"&gt;
    &lt;li class="menu__item"&gt;
      &lt;div class="link"&gt;&lt;/div&gt;
    &lt;/li&gt;
    &lt;li class="menu__item menu__item_current"&gt;
      &lt;div class="link"&gt;&lt;/div&gt;
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/menu&gt;
</code></pre>
</li>
<li>Set the <code>&lt;a&gt;</code> tag for all links on the page:<br />

<pre><code class="language-css">block('menu')(
  tag()('menu'),
  content()(function() {
    return {
      elem: 'inner',
      content: this.ctx.content
    }
  }),
  elem('inner')(
    tag()('ul')
  ),
  elem('item')(
    tag()('li')
  )
);
block('link')(
  tag()('a')
);
</code></pre>

<pre><code class="language-html">&lt;menu class="menu"&gt;
  &lt;ul class="menu__inner"&gt;
    &lt;li class="menu__item"&gt;
      &lt;a class="link"&gt;&lt;/a&gt;
    &lt;/li&gt;
    &lt;li class="menu__item menu__item_current"&gt;
      &lt;a class="link"&gt;&lt;/a&gt;
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/menu&gt;
</code></pre>
</li>
<li>Modify the existing template. Rules in templates are applied in the same way as in CSS: a lower rule overrides a higher rule. Add new rules to the template, and change the link tag from  <code>&lt;a&gt;</code> to <code>&lt;span&gt;</code>:<br />

<pre><code class="language-css">block('link')(
  tag()('a')
);
block('link')(
  tag()('span')
);
</code></pre>

<pre><code class="language-html">&lt;menu class="menu"&gt;
  &lt;ul class="menu__inner"&gt;
    &lt;li class="menu__item"&gt;
      &lt;span class="link"&gt;&lt;/span&gt;
    &lt;/li&gt;
    &lt;li class="menu__item menu__item_current"&gt;
      &lt;span class="link"&gt;&lt;/span&gt;
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/menu&gt;
</code></pre>
</li>
</ol>

## BEM Is A Customizable System

BEM methodology provides you strict rules to create a system in your project. But at the same time, a lot of BEM rules can be customized. BEM methodology allows you to change the naming convention, choose the most convenient file structure or add any technologies you want to the block. 

Now you can tune in the system and make your own superhero of BEM!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c6b06e-9ccb-409d-84cb-589e07607e32/sign-theme-captain-america.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c6b06e-9ccb-409d-84cb-589e07607e32/sign-theme-captain-america.png" sizes="100vw" caption="BEM Captain America" alt="BEM as a Captain America logo" >}}

## How To Get More Out Of BEM

To start learning BEM principles, visit our [website](https://en.bem.info/). If you have any questions you'd like to ask the team, join our [Telegram](https://t.me/bem_en) channel or open up a discussion in our [BEM Forum](https://en.bem.info/forum/).

{{< signature "rb, ra, il" >}}