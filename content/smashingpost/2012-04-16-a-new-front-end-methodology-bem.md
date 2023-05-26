---
title: 'BEM: A New Front-End Methodology'
slug: a-new-front-end-methodology-bem
image: null
date: 2012-04-16T10:00:14.000Z
author: varvara-stepanova
description: >-
  _This article is the sixth in our new series that introduces the latest,
  useful and freely available tools and techniques, developed and released by
  active members of the Web design community. The first article covered
  [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/);
  the second introduced
  [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/),
  a responsive framework; the third presented
  [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/),
  a library for Gmail-like client-side drafts, the fourth covered a free plugin
  called
  [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/)
  and the fifth presented Erskine Design's responsive grid generator
  [Gridpak](https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/).
  Today, we are happy to feature a toolkit devised by Yandex: **BEM**._
categories:
  - Coding
  - Frameworks
  - CSS
  - JavaScript
  - Templates
  - HTML
---
<em>This article is the sixth in our new series that introduces the latest, useful and freely available tools and techniques, developed and released by active members of the Web design community. The first article covered <a href="https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/">PrefixFree</a>; the second introduced <a href="https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/">Foundation</a>, a responsive framework; the third presented <a href="https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/">Sisyphus.js</a>, a library for Gmail-like client-side drafts, the fourth shared with us a free plugin called <a href="https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/">GuideGuide</a> and the fifth presented Erskine Design's responsive grid generator <a href="https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/">Gridpak</a>. Today, we are happy to feature a toolkit devised by Yandex: <strong>BEM</strong>.</em>

<strong>BEM</strong> stands for "Block", "Element", "Modifier". It is a front-end methodology: a new way of thinking when developing Web interfaces. This article will elaborate on the theory as well as the practice of building websites at Yandex—one of the leading internet companies in Russia.

The article has three parts: BEM Principles, Blocks Reiteration and File System Representation For A Block

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Scaling Down The BEM Methodology For Small Projects](https://www.smashingmagazine.com/2014/07/bem-methodology-for-small-projects/)
*   [The Evolution Of The BEM Methodology](https://www.smashingmagazine.com/2013/02/the-history-of-the-bem-methodology/)
*   [Battling BEM: 10 Common Problems And How To Avoid Them](https://www.smashingmagazine.com/2016/06/battling-bem-extended-edition-common-problems-and-how-to-avoid-them/)

{{% feature-panel %}}

## BEM Principles

To begin, let's first put <a href="https://getbem.com/">BEM</a> in some historical perspective.

We first began sketching out the internal front-end framework at Yandex around the year 2007, starting with a robust CSS naming convention, and a file system layout that was associated with it. Since the naming convention was well-structured, it seemed suitable to develop certain JavaScript helpers (to work with the DOM and CSS classes in particular, on a higher level of abstraction). We then used those approaches to build an internal library of UI components that could be shared among our various websites and rich applications, built using different technology stacks (XML/XSLT, Python/Django, Perl/TT2).

As our ambitions, complexity and performance requirements grew, we aimed at replacing XSLT and Perl templates with a JS-based declarative templating DSL, built on top of Node.js. Along with those efforts, we looked into simplifying development workflow and developed a bunch of command-line tools that already helped us manage front-end code on the file system, preprocess CSS and JavaScript code, and so on, and so forth.

Some parts of the BEM stack started as open source projects, while others (like the UI component library) are being gradually open sourced. Our goal is to publish most of them during 2012.

BEM is a toolkit that will help address and resolve front-end issues quickly and effectively. It is available in a range of reusable code libraries—all of them are hosted on Github and are completely open source.</p>

## BEM Principles

One of the most common examples of a methodology in programming is <em>Object-Oriented Programming</em>. It's a programming paradigm embodied by many languages. In some ways, BEM is similar to OOP—a way of describing reality in code, with a range of patterns, and a way of thinking about program entities regardless of the programming languages being used.

We've used BEM principles to create a set of front-end development techniques and tools that allow us to build websites quickly and maintain them over a long period of time. The principles are the following:

## Unified Data Domain

Imagine an ordinary website, like the one pictured below:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e4d7375-39a8-4690-b9cf-7914e4ff33dc/site.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a118d71-1d2f-4f61-a1a2-3ea3fea113a8/site-screenshot.jpg" alt="bem - ordinary website example" width="500" height="300" /></a>

While developing such a website, it's useful to mark out "blocks" from which the website consists of. For example, in this picture there are <code>Head</code>, <code>Main Layout</code> and <code>Foot</code> blocks. The <code>Head</code> in turn consists of <code>Logo</code>, <code>Search</code>, <code>Auth Block</code> and <code>Menu</code>. <code>Main Layout</code> contains a <code>Page Title</code> and a <code>Text Block</code>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7acc506d-9963-4013-b8c3-ad11e9f510fe/site-marked.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/980a9b7c-e0f9-4cef-a3f1-7c2ba55c8011/site2.jpg" alt="bem - site marked" width="500" height="320" /></a>

Giving each part of the page a name is very useful when it comes to team communication.

A project manager could ask:

*   To make the `Head` bigger, or
*   To create a page without a `Search` form in the `Head`.

An HTML guy could ask a fellow JavaScript developer:

*   To make `Auth Block` animated, etc.

Let's now take a closer look at what constitutes BEM:

### Block

A <code>block</code> is an independent entity, a "building block" of an application. A block can be either simple or compound (containing other blocks).

<strong>Example</strong>
Search form block:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8653b141-dace-47f6-8997-6f66edce93e0/search-block.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fa03b3b-632f-4467-8758-facd7a7b9a6e/search-bar.jpg" alt="search form block" width="500" height="120" /></a>

### Element

An <code>element</code> is a part of a block that performs a certain function. Elements are context-dependent: they only make sense in the context of the block that they belong to.

<strong>Example</strong>

An input field and a button are elements of the Search Block:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac793350-a948-428e-9968-e01bc46766cf/search-block-marked.en_"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d8766e0-df2a-4486-a3c9-b922eae2ca90/input-button.jpg" alt="elements of search block" width="500" height="155" /></a>

## Means Of Describing Pages And Templates

Blocks and elements constitute page content. Besides simply being present on a page, their arrangement is also important.

Blocks (or elements) may follow each other in a certain order. For example, a list of goods on a commerce website:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d601c2c1-e008-46b1-8d00-101746701452/goods-list.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b01ce790-a401-4da5-9ff5-9f78dd6098a6/list-of-goods.jpg" alt="list of goods on a commerce website" width="500" height="360" /></a>

...or menu items:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb5574c7-13e3-45a3-acc5-1865ac270674/menu-items.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fedc4e5-2fec-4c64-8c0f-fcb61e59041d/menu-items2.jpg" alt="menu items" width="500" height="290" /></a>

Blocks may also be contained inside other blocks. For example, a <code>Head Block</code> includes other blocks:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dacab506-9c20-4a86-a5c2-e4266176bf4e/head-marked.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c702b771-3101-46e1-9908-faf586684640/head-marked2.jpg" alt="blocks inside other blocks" width="500" height="260" /></a>

Besides, our building blocks need a way to describe page layout in plain text. To do so, every block and element should have a keyword that identifies it.

A keyword designating a specific block is called <code>Block Name</code>. For example, <code>Menu</code> can be a keyword for the <code>Menu Block</code> and <code>Head</code> can be a keyword for the <code>Head</code> block.

A keyword designating an element is called <code>Element Name</code>. For example, each item in a menu is an element <code>Item</code> of the <code>Menu</code> block.

Block names must be unique within a project to unequivocally designate which block is being described. Only instances of the same block can have the same names. In this case, we can say that one block is present on the page twice (or 3, 4, times... etc.).

Element names must be unique within the scope of a block. An element can be repeated several times. For example, menu items:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/519deb2d-3229-457b-8e4e-cc90fb77d159/repeated-elements.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c99a0bf-6da0-4948-af13-4f29f74bf1de/elements-repeated.jpg" alt="repeated elements" width="500" height="300" /></a>

Keywords should be put in a certain order. Any data format that supports nesting (XML, JSON) will do:

<pre><code class="language-markup tmp-xml">&lt;b:page&gt;
  &lt;b:head&gt;
    &lt;b:menu&gt;
      ...
    &lt;/b:menu&gt;
    &lt;e:column&gt;
      &lt;b:logo/&gt;
    &lt;/e:column&gt;
    &lt;e:column&gt;
      &lt;b:search&gt;
        &lt;e:input/&gt;
        &lt;e:button&gt;Search&lt;/e:button&gt;
      &lt;/b:search&gt;
    &lt;/e:column&gt;
    &lt;e:column&gt;
      &lt;b:auth&gt;
        ...
      &lt;/b:auth&gt;
    &lt;e:column&gt;
  &lt;/b:head&gt;
&lt;/b:page&gt;</code></pre>

In this example, <code>b</code> and <code>e</code> namespaces separate block nodes from element nodes.

The same in JSON:

<pre><code class="language-javascript">{
  block: 'page',
  content: {
    block: 'head',
    content: [
      { block: 'menu', content: ... },
      {
        elem: 'column',
        content: { block: 'logo' }
      },
      {
        elem: 'column',
        content: [
          {
            block: 'search',
            content: [
              { elem: 'input' },
              {
                elem: 'button',
                content: 'Search'
              }
            ]
          }
        ]
      },
      {
        elem: 'column',
        content: {
          block: 'auth',
          content: ...
        }
      }
    ]
  }
}</code></pre>

Examples above show an object model with blocks and elements nested inside each other. This structure can also contain any number of custom data fields. We call this structure <code>BEM Tree</code> (by analogy with DOM tree).

Final browser markup is generated by applying template transformations (using XSL or JavaScript) to a BEM tree.

If a developer needs to move a block to a different place on a page, he does so by changing the BEM tree. Templates generate the final view themselves.

In our recent products we went with JSON as a page description format. It is then turned into HTML by a JS-based template engine. The tools we use are listed at the end of this article.</p>

## Block Independence

As projects grow, blocks tend to be added, removed, or moved around on the page. For example, you may want to swap the <code>Logo</code> with the <code>Auth Block</code>, or place the <code>Menu</code> under the <code>Search Block</code>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/158bb8c5-ee1f-47e2-8a08-1ec45276ae59/switch-function.jpg" alt="swapping blocks" width="500" height="285" />

To make this process easier, blocks must be <code>Independent</code>.

An <code>Independent</code> block is implemented in a way that allows arbitrary placement anywhere on the page—including nesting inside another block.</p>

### Independent CSS

From the CSS point of view it means that:

*   A block (or an element) must have a unique "name" (a CSS class) that could be used in a CSS rule.
*   HTML elements must not be used in CSS selectors (.menu td) as such selectors are inherently not context-free.
*   Cascading selectors for several blocks should be avoided.

#### Naming for Independent CSS Classes

One of the possible naming schemes for CSS classes that satisfies said requirements is the following:

*   CSS class for a block coincides with its `Block Name`.

<pre><code class="language-markup tmp-xml">&lt;ul class="menu"&gt;
  ...
&lt;/ul&gt;</code></pre>

*   CSS class for an element is a `Block Name` and an `Element Name` separated by some character(s)

<pre><code class="language-markup tmp-xml">&lt;ul class="menu"&gt;
  &lt;li class="menu__item"&gt;
    ...
  &lt;/li&gt;
  &lt;li class="menu__item"&gt;
    ...
  &lt;/li&gt;
&lt;/ul&gt;</code></pre>

It's necessary to include block name in a CSS class for an element to minimize cascading. It's also important to use separators consistently to allow the tools and helpers to have unambiguous programmatic access to the elements.

Different naming schemes can be used. Take a look <a href="https://bem.github.com/bem-bl/pages/naming/naming.en.wiki?from=smashingmagazine">here</a> for the naming convention we used.</p>

### Independent Templates

From the template engine's perspective, block independence means that:

*   Blocks and elements must be described in the input data. Blocks (or elements) must have unique "names" to make things like "`Menu` should be placed here" expressible in our templates.
*   Blocks may appear anywhere in a BEM tree.

#### Independent templates for blocks

When coming across a block in a template, the template engine should be able to unambiguously transform it into HTML. Thus, every block should have a template for that.

For example, a template can look like this in XSL:

<pre><code class="language-markup tmp-xml">&lt;xsl:template match="b:menu"&gt;
  &lt;ul class="menu"&gt;
    &lt;xsl:apply-templates/&gt;
  &lt;/ul&gt;
&lt;/xsl:template&gt;

&lt;xsl:template match="b:menu/e:item"&gt;
  &lt;li class="menu__item"&gt;
    &lt;xsl:apply-templates/&gt;
  &lt;/li&gt;
&lt;xsl:template&gt;</code></pre>

We are gradually discarding XSLT in our products in favor of our own JavaScript-based template engine <a href="https://github.com/veged/xjst?from=smashingmagazine">XJST</a>. This template engine absorbs everything we like about XSLT (we are fans of declarative programming), and implements it with JavaScript's productivity on either the client or the server side.

We, at Yandex, write our templates using a domain-specific language called BEMHTML, which is based on XJST. <span class="removed_link" title="https://clubs.ya.ru/bem/replies.xml?item_no=992&amp;from=smashingmagazine">The main ideas of BEMHTML</span> are published in the BEM club on Ya.Ru (in Russian).</p>

## Blocks Reiteration

The second <code>Menu Block</code> can occur in the <code>Foot Block</code> of a website. Also, a <code>Text Block</code> can divide into two, separated by an advertisement.

Even if a block was developed as a singular unit, the same one can appear on a page at any moment.

In CSS related terms, this means:

*   ID-based CSS selectors must not be used. Only class selectors satisfy our non-uniqueness requirement.

On the JavaScript side it means:

*   Blocks with similar behavior are detected unequivocally—they have the same CSS classes. Using CSS class selectors allows for picking all blocks with a given name to apply the required dynamic behavior.</p>

## Modifiers For Elements And Blocks

We often need to create a block very similar to an existing one, but with a slightly altered appearance or behavior.
Let's say, we have a task:

*   Add another `Menu` in the `Footer` with a _different layout_.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29be905b-d70e-402c-8c25-66507b11bdcc/site-footer-menu.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6613141-0775-4fa6-87ec-513d5c37aee5/sitefootermenu.jpg" alt="site footer menu" width="500" height="310" /></a></figure>

To avoid developing another block that is only minimally different from an existing one, we can use a <code>Modifier</code>.

A <code>Modifier</code> is a property of a block or an element that alters its look or behavior. A modifier has both a name and a value. Several modifiers can be used at once.

<strong>Example:</strong>
A block modifier specifies background color

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b362686-0f47-4606-bc70-79facb840b77/search-background.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa33fa27-d0e4-4d38-ac8b-b101104cb76a/search-background2.jpg" alt="search background" width="500" height="135" /></a></figure>

<strong>Example:</strong>
An element modifier changes the look of the "current" item

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be24a60d-27af-4a48-9058-24cba13be727/menu-current-item.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5f86638-e2aa-49be-8d38-aeb5b7789a16/menu-current-items.jpg" alt="current item in menu" width="500" height="135" /></a></figure>

From the input data point of view:

*   In a BEM tree, modifiers are properties of an entity that describes a block or an element.

For example, they can be attribute nodes in XML:

<pre><code class="language-markup">&lt;b:menu m:size="big" m:type="buttons"&gt;
  ...
&lt;/b:menu&gt;</code></pre>

The same expressed in JSON:

<pre><code class="language-javascript">{
  block: 'menu',
  mods: [
   { size: 'big' },
   { type: 'buttons' }
  ]
}</code></pre>

From the CSS point of view:

*   A modifier is an additional CSS class for a block or an element.

<pre><code class="language-markup">&lt;ul class="menu menu_size_big menu_type_buttons"&gt;
  ...
&lt;/ul&gt;</code></pre>

<pre><code class="language-css">.menu_size_big {
  // CSS code to specify height
}
.menu_type_buttons .menu__item {
  // CSS code to change item's look
}</code></pre>

Element modifiers are implemented in the same fashion. Again, when writing CSS by hand, it's very important to use separators consistently for programmatic access.

E.g., current menu item can be marked with a modifier:

<pre><code class="language-markup">&lt;b:menu&gt;
  &lt;e:item&gt;Index&lt;e:item&gt;
  &lt;e:item m:state="current"&gt;Products&lt;/e:item&gt;
  &lt;e:item&gt;Contact&lt;e:item&gt;
&lt;/b:menu&gt;</code></pre>

<pre><code class="language-javascript">{
  block: 'menu',
  content: [
    { elem: 'item', content: 'Index' },
    {
      elem: 'item',
      mods: { 'state' : 'current' },
      content: 'Products'
    },
    { elem: 'item', content: 'Contact' }
  ]
}</code></pre>

<pre><code class="language-markup">&lt;div class="menu"&gt;
  &lt;ul class="menu__layout"&gt;
    &lt;li class="menu__layout-unit"&gt;
      &lt;div class="menu__item"&gt;Index&lt;/div&gt;
    &lt;/li&gt;
    &lt;li class="menu__layout-unit"&gt;
      &lt;div class="menu__item menu__item_state_current"&gt;Products&lt;/div&gt;
    &lt;/li&gt;
    &lt;li class="menu__layout-unit"&gt;
      &lt;div class="menu__item"&gt;Contact&lt;/div&gt;
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;</code></pre>

<pre><code class="language-css">.menu__item_state_current {
  font-weight: bold;
}</code></pre>

## Subject-Matter Abstraction

When many people work on a project, they should agree on a data domain and use it when naming their blocks and elements.

For example, a <code>Tag Cloud</code> block is always named <code>Tags</code>. Each of its elements is a <code>Tag</code>. This convention spreads across all languages: CSS, JavaScript, XSL, etc.

From the development process' point of view:

*   All participants operate on the same terms.

From the CSS point of view:

*   CSS for blocks and elements can be written in a pseudo language that compiles down to CSS according to the naming convention.

<pre><code class="language-css">  .menu {
    __layout {
      display: inline;
    }
    __layout-item {
      display: inline-block;
      ...
    }
    __item {
      _state_current {
        font-weight: bold;
      }
    }
  }</code></pre>

On the JavaScript side:

*   Instead of using class selectors directly to find DOM elements, a special helper library may be used.

<pre><code class="language-javascript">$('menu__item').click( ... );
$('menu__item').addClass('menu__item_state_current');
$('menu').toggle('menu_size_big').toggle('menu_size_small');</code></pre>

The naming convention for CSS classes of blocks and elements can change over the course of time. Using special JavaScript functions to access blocks and elements (and to work with their modifiers) makes it possible to change only these functions if the naming convention changes.

<pre><code class="language-javascript">Block('menu').elem('item').click( ... );
Block('menu').elem('item').setMod('state', 'current');
Block('menu').toggleMod('size', 'big', 'small');</code></pre>

The code above is abstract. In real life we use the JavaScript core of <code>i-bem</code> block from the <code>bem-bl</code> block library: <a href="https://bem.github.com/bem-bl/sets/common-desktop/i-bem/i-bem.ru.html?from=smashingmagazine">https://bem.github.com/bem-bl/sets/common-desktop/i-bem/i-bem.ru.html</a> (described in Russian)

## Blocks Consistency

A website has a <code>Button</code> block with certain dynamic behavior.

When a block is hovered, it changes its appearance.

A manager could ask:

*   To use the same button on another page.

Having a CSS implementation of a block is not enough. Reusing a block also means reusing its behavior, described in JavaScript.

So a block must "know" everything about itself. To implement a block, we describe its appearance and behavior in all technologies being used—we call that <code>Multilingualism</code>.

<code>Multilingual</code> presentation is a description of a block in all the programming languages that are necessary to implement the view and the functionality of that block.

To have a block present on a page as a UI element, we need to implement it in the following techs:

*   Templates (XSL, TT2, JavaScript, etc), which turn block declarations into HTML code.
*   CSS that describes appearance of the block.

If a block has dynamic behavior, we add it to this list:

*   A JavaScript implementation for the block.

Everything that constitutes a block is a technology, including images.</p>

## Unequivocal Placement of Code

#### File Naming

When a project is:

*   Long-lived and under constant development.

If the development team:

*   Consists of several people.
*   Grows and changes.

Then being able to navigate the code base quickly is crucial.

Block code is easiest to find when it's placed in files using the same naming scheme as the one we use for naming our entities:

<pre><code class="language-javascript">menu.xsl
menu.js
menu.css</code></pre>

#### Expressing Blocks on a File System

There could be a task:

*   To reuse some blocks from a previous project for a new one.

We want the procedure of block reuse to be as simple as possible—like simply copying the files, or using partial checkout of a repository from a "donor" project. In both cases, it is useful to have all of the files under the same directory:

<pre><code class="language-javascript">menu/
  menu.xsl
  menu.js
  menu.css</code></pre>

#### File Structure of a Block

When working on a project we might need to change a block at some point.

A manager could ask:

*   To change the color of the `Current Menu Item,` or
*   To make the `Menu` react on hover.

A developer could ask their colleague:

*   To help with `Search Form` styling for IE.

To understand where the relevant code is located, follow these (or similar) rules:

*   Block code is placed in a separate directory.
    *   Directory name matches block name.
    *   Implementation is placed under this directory.
*   Elements are placed in subdirectories under the block directory.
    *   Directory name matches element name.
    *   Implementation is placed under this directory.
*   Modifiers are placed in subdirectories under the block directory.
    *   Directory name matches modifier name.
    *   Implementation is placed under this directory.
    *   File name includes both key and value of the modifier (again, for programmatic access).

<strong>Example</strong>

File structure of a <code>Menu</code> block:

<pre><code class="language-javascript">menu/
  __item/
    _state/
      menu__item_state_current.css
      menu__item_state_current.xsl
    menu__item.css
    menu__item.xsl
  menu.css
  menu.js
  menu.xsl</code></pre>

Maintaining such file structure manually is, quite obviously, inconvenient. So we've developed <a href="https://github.com/bem/bem-tools?from=smashingmagazine">BEM Tools</a> to handle the burden. These tools help with creating the directory structure, placing files, generating placeholder content, etc.

#### Grouping Blocks in Directories

Big internet portals often need to reuse the same blocks across different websites.

There could be a task:

*   To create the same `Footer` on _all the portals' websites,_ or
*   To create a _new project_ using blocks from the existing websites.

Working for a Web design agency often means that one has to use typical solutions for typical Web pages.

A project manager could ask you:

*   To create an order page with a Web form _as on the previous project._

We have to do these tasks while preferably avoiding copying blocks around manually. So it's nice to have a repository of shared blocks that can be linked to a project. Blocks should then be united under a single directory for that.

Such a directory is usually called <code>Blocks</code>.

<strong>E.g.</strong>

<pre><code class="language-javascript">blocks/
  foot/
  head/
  menu/
  page/
  search/</code></pre>

That directory can be linked to another project straight from the version control system, so that we can make changes to shared blocks in a single location.</p>

## Levels Of Definition

If a group of blocks (united under one directory) is linked to a project directly (via a partial checkout, svn:externals, etc.), then every change committed to these blocks influences all projects.

When developing a website based on an existing one, we might want:

*   To enlarge the font in the `Head` on site A without affecting site B.
*   To add animation when showing a drop-down menu.

To do so, we need to be able to define or redefine blocks in different technologies for a specific website only, or for certain pages only. This can be achieved using <code>Definition Levels</code>.

A <code>Definition Level</code> is a set of blocks grouped in one directory.

<figure class="fwi"></figure>

An implementation of every block from the library can be changed (or completely redefined) at project level.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23f45039-3e3a-4f12-b398-3d268c4de081/block-levels.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/265eefc7-3944-41f1-af1a-b7cce18dcf90/block-levels2.jpg" alt="block levels" width="500" height="235" /></a></figure>

From page-building process' perspective:

*   When building a page, we can set a list of levels (directories) to use their blocks on that page. E.g., `build-page -l blocks-common -l blocks-my my-page.html`

From the file structure point of view:

*   A project can have any number of levels. But only the levels that are evaluated during the build will be present on the page. It is possible to specify different sets of definition levels for different parts of the website.

On the JavaScript side:

*   We need to define dynamic behavior of a page in declarative style. Final behavior is gathered from different definition levels. E.g.,

<pre><code class="language-javascript">/* blocks-common/dropdown/dropdown.js */
Block('dropdown', {
  init: function() {
    ...
  }
});

/* blocks-my/dropdown/dropdown.js */
Block('dropdown', {
  init: function() {
    this.__base();
    ...
  }
});</code></pre>

From the viewpoint of a template engine:

*   To be able to not only define, but to redefine a template, one needs to apply a preceding template implementation. E.g., for XSL:

<pre><code class="language-markup">&lt;xsl:template match="b:head"&gt;
  &lt;div&gt; &lt;!-- Node for extra design --&gt;
    &lt;xsl:apply-imports/&gt;
  &lt;/div&gt;
&lt;/xsl:template&gt;</code></pre>

From the architectural point of view:

*   When developing a portal of several websites, we can extract a block library that serves as one of the definition levels for all the websites which are part of the portal. The blocks for a specific website will form another level.
*   The same repo can hold blocks of both desktop and mobile versions. Such a project will have the following levels: common, mobile, desktop. Different combinations of these levels give the resulting implementation, required by specific pages.

<a href="https://bem.github.com/bem-bl/index.en.html?from=smashingmagazine">Open source block library bem-bl (in development)</a> is an example of having several definition levels in one repository.</p>

## Building A Page

Working in terms of blocks means having a <code>Subject-Matter Abstraction</code>. This abstraction is for developers only, and browsers will get a compiled version of the code.

So we have <code>Code For People</code> and <code>Code For Browsers</code>—they are not the same.

*   Programmers code blocks—browsers get the code for the whole page.

To turn <code>Code For People</code> into <code>Code For Browsers</code> we <code>Build</code> a page.

<code>Building A Page</code> means generating HTML, CSS, and JavaScript code from a page declaration (written in XML or JSON) by applying implementations of declared blocks.

On the CSS side:

*   All CSS files are combined into a "single page" CSS file. Despite the fact that CSS for every block, element or modifier is stored in separate files, we don't have to link these files to the page as is. It's possible to collect all the required CSS implementations into one file. This also solves the well-known "number of imports" issue in IE, and decreases the number of HTTP requests. For combining CSS we use [borschik](https://github.com/veged/borschik?from=smashingmagazine).
*   Browser gets minimized code. When building CSS, we can minimize and optimize CSS code using the [CSSO](https://github.com/afelix/csso?from=smashingmagazine) utility, for example.
*   Each browser can get CSS code written especially for it. It is also possible to divide CSS implementations for different browsers and deliver only the code needed for each browser. [setochka—currently in prototype](https://github.com/afelix/setochka?from=smashingmagazine) can be used for that.

From the JavaScript point of view:

*   Similarly to CSS, JavaScript files can be combined into one.

From the template engine's point of view:

*   Only needed templates are included. Final set of templates that are used for displaying a page includes only the templates for required blocks. This boosts template performance and reduces the likelihood of side effects.

From the viewpoint of development process:

*   Robots serve people (not the other way around). Developer writes code as they see fit. "Robots" take (some) care of performance by optimizing the code (together with making it unreadable) when building a page.

In terms of work organization:

*   Division of labor. We have developers working on the core framework (compilers, tools, performance); library developers, who maintain the block library; application developers, who develop websites using the framework.

We use <a href="https://github.com/bem/bem-tools?from=smashingmagazine">BEM tools</a> to build pages.

#### How to Automate the Building Process?

The usage of <a href="https://github.com/bem/bem-tools?from=smashingmagazine">bem tools</a> requires to run several commands for each page whenever page input data or blocks implementation are changed. As a result of these commands, you get CSS and JavaScript files for the page, page's template, and if you are developing static pages, the HTML code of your page.

To avoid running these commands manually, there is also the <a href="https://www.gnu.org/software/make/manual/make.html">GNUmakefile</a>, which was written for a project that includes the instructions on how to build pages.
You can find an example of such a file in the test project <a href="https://github.com/bem/bem-bl-test/blob/master/GNUmakefile">bem-bl-test</a>.

But the usage of GNU Make has a list of problems:

*   You have to run it every time you have changed something.
*   Every time you run gmake, it reads the information from a disk. So the compilation process could not be fast.
*   The pages you build not only depend on the content of block files, but on their file structure as well. But it's impossible to write a gmake goal dependency in these terms.

So we'd like to create something to replace GNU Make for the process of page building. This will be both a development server and a tool to build production files. <code>Bem Server</code> will be run in a project root directory, and give HTTP response with the page files built (so you won't need to run gmake manually after each change).
Besides, it will be able to watch the files (the adding and removing of them) via fs.FSWatcher that help to chache results efficiently.

<code>BEM Server</code> is a subcommand of <a href="https://github.com/bem/bem-tools">bem-tools</a>. Currently it can run an HTTP server, apply <code>BEMhtml</code> templates to <code>BEMjson</code> data and inline CSS imports using <a href="https://github.com/veged/borschik?from=smashingmagazine">borschik</a> utility.</p>

## Real Examples

<a href="https://yandex.ru/">Yandex</a> is a large (mostly Russian) company that use BEM methodology to develop its services.

BEM methodology does not request that you use a certain framework. You also don't have to use BEM for all the technologies you have on your pages (but that would be the most efficient).

<a href="https://www.yandex.ru/all">All the services of Yandex</a> have BEM in their CSS, JavaScript code or XSL templates for their pages. E.g.,

*   [Yandex.Maps](https://maps.yandex.ru/?text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0&amp;sll=37.609218%2C55.753559&amp;ll=37.609218%2C55.753563&amp;spn=2.570801%2C0.884460&amp;z=9&amp;l=map)
*   [Yandex.Images](https://images.yandex.ru/yandsearch?text=Yandex+office&amp;rpt=image) This is a service for searching images in the Internet.
*   [Yandex.Video](https://video.yandex.ru/#search?text=yac%202011) This is a service for both hosting and searching images.
*   [Yandex.Jobs](https://rabota.yandex.ru/)
*   [Turkish Yandex](https://www.yandex.com.tr/)

Some services don't use XSL templates, building their pages with our newest template product, <code>Bemhtml</code> template engine which was mentioned above. These are the following services:

*   Yandex Search or [Yandex Search in English](https://yandex.com/yandsearch?text=%22What+is+BEM%3F%22+front-end&amp;lr=213)
*   [Mobile Apps Search](https://apps.yandex.ru/) This website is to look under smartphones.

There are also other companies that use BEM methodology.

For example, the guys at <a href="https://mail.ru/">Mail.ru</a> partly use BEM for their services. Some blocks on their pages are BEM-based in terms of CSS code. They also have their own C++ template engine, and write block templates according to this methodology.

More examples:

*   [Rambler.News](https://beta.news.rambler.ru/)
*   [HeadHunter](https://hh.ru/)
*   [TNK Racing Team](https://futurecolors.ru/tnkracing/)

You also may be interested in websites that use <a href="https://bem.github.com/bem-bl/index.en.html?from=smashingmagazine">bem-bl</a> block library (in development):

*   [Mikhail Troshev vCard](https://mishanga.pro/?from=smashingmagazine) Source code is hosted at GitHub: [https://github.com/mishanga/bem-vcard](https://github.com/mishanga/bem-vcard?from=smashingmagazine)
*   BEM based web form with JZ validation

## Related Links

### Libraries

*   [An open source block library bem-bl](https://bem.github.com/bem-bl/index.en.html?from=smashingmagazine) (in development).</p>

### Tools

*   [Tools for working with files according to BEM methodology.](https://github.com/bem/bem-tools?from=smashingmagazine)
*   [Borschik](https://github.com/veged/borschik?from=smashingmagazine) A utility for building static files into one.
*   [Setochka, a working prototype](https://github.com/afelix/setochka?from=smashingmagazine) A tool for dividing CSS into several browser-specific files.
*   [CSSO](https://github.com/afelix/csso?from=smashingmagazine) A utility that performs advanced, structural optimizations of CSS code.</p>

### Additional Information

*   [How to use BEM! outside Yandex](https://vimeo.com/38346573) (screencast presentation).

{{< signature "jvb" >}}

