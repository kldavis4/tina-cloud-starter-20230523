---
title: 'Sneak Peek Into The Future: CSS Selectors, Level 4'
slug: sneak-peek-future-selectors-level-4
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/186ac353-bdfa-4d6e-8997-0c2022070287/css4.jpg'
date: 2013-01-21T11:19:16.000Z
author: andrzej-mazur
description: >-
  The buzzword “CSS4” came out of nowhere, just as we were getting used to the
  fact that CSS3 is here and will stick around for some time. Browser vendors
  are working hard to implement the latest features, and front-end developers
  are creating more and more tools to be able to work with the style sheets more
  effectively.
categories:
  - Coding
  - Tools
  - CSS
  - CSS3
---
The buzzword “CSS4” came out of nowhere, just as we were getting used to the fact that CSS3 is here and will stick around for some time. Browser vendors are working hard to implement the latest features, and front-end developers are creating more and more tools to be able to work with the style sheets more effectively. But now, on hearing about CSS4, you might ask, “Hey, what about CSS3? <strong>Is it over already?</strong>”

We’ve been working hard to spread the goodness of CSS3, and now it’s obsolete? In fact, nothing’s wrong. It’s just natural evolution — a process that will help CSS as a whole — because “Level 3” and “Level 4” just follow the naming convention of the various documents of the specification.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)
*   [Taming Advanced CSS Selectors](https://www.smashingmagazine.com/2009/08/taming-advanced-css-selectors/)
*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)

### Why Level 4? What About CSS3?

“Level 4” is just the number of the W3C document. Have you heard about the new “Filter Effects, Level 1” specification? Where should it go? To CSS3? CSS4? Hey, maybe CSS1 because it’s Level 1? Doesn’t matter, because <strong>CSS is just CSS</strong>. Selectors are the first document to reach the fourth level of the specification, and it’s still a draft, a work in progress. Each document is on its own when it comes to the specification number; the documents are developed independently of each other.

{{% feature-panel %}}

This is a big advantage, because finished parts of the document can be closed and set as recommendations — like Selectors Level 3. Finishing a document quickly and moving problematic parts to the next level helps to push the Web forward because it implements the specification one chunk at a time.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3e36b0b-ca28-4f2d-867c-7c98b594943a/css4.jpg" alt="How the CSS4 logo could look like." width="500" height="300" />

The buzzword “CSS3” will share the same fate as “HTML5”: we’re not talking about a specification number, but about the language as a whole. HTML5 is basically just the next version of the markup language, which adds support for new elements. But when you talk about it, you can bring up anything you want, from the audio API to Web sockets to geolocation (which isn’t even in the HTML5 specification).

The same goes for CSS3: it’s the shiny bit of magic that we do with CSS when building cutting-edge demos. You don’t have to know what part of the specification <code>border-radius</code> or <code>box-shadow</code> belongs to, as long as you know how to properly use it. Same goes for selectors; they’re <strong>just another version of the “Selectors” specification</strong>.</p>

## What Are Selectors?

The specification explains selectors as patterns that match against elements in a tree. Most of the selectors from the Level 4 specification are pseudo-classes. Selectors have been with us since the beginning of CSS, but now they are at the fourth level and have gotten a lot of cool new additions. Let’s jump into the action and see what’s interesting. I won’t describe the entire document — only the new additions in Level 4.</p>

### Logical Combinators: :matches, :not

Let’s start with logical pseudo-classes. The first, <code>:matches</code>, some of you might already know from <a href="https://developer.mozilla.org/en/CSS/%3A-moz-any">Mozilla’s <code>:-moz-any()</code></a>, which was implemented a long time ago in Firefox 4. Thanks to this selector, we can group and match items in our CSS document. Why is it so useful? Well, the most basic use I can think of is to gather multiple definitions of anchor states into one. So, instead of this…

<pre><code class="language-css">ul.menu li a:link,
ul.menu li a:hover,
ul.menu li a:visited,
ul.menu li a:focus {
   color: red;
}</code></pre>

… we can just do this:

<pre><code class="language-css">ul.menu li a:matches(:link, :hover, :visited, :focus) {
   color: red;
}</code></pre>

Simple, right? Although this example might look silly, it shows the power of the <code>:matches</code> pseudo-class, and it can be used in more complicated situations:

<pre><code class="language-css">article:matches(.active, .visible, #important) {
   background: red;
}</code></pre>

The second logical combinator we’ll look at was introduced in the CSS3 specification, but it became even more powerful in Level 4. I’m talking about <code>:not</code>, the simple negation pseudo-class, which now can take a list of selectors as parameters:

<pre><code class="language-css">p:not(.active, .visible) {
   color: red;
}</code></pre>

The code above will apply red to all paragraphs to which the <code>active</code> or <code>visible</code> class <strong>are not</strong> assigned in the markup.</p>

### Location Pseudo-Classes: :any-link, :local-link

Thanks to the location pseudo-classes, we will have more control over the styling of links. First, <code>:any-link</code> (a temporary name that could change) gathers definitions of <code>a:link</code> and <code>a:visited</code> into one, so you don’t have to write them both:

<pre><code class="language-css">a:link,
a:visited {
   color: red;
}</code></pre>

Now, it won’t matter whether a link has been visited or not. It will be styled the same either way:

<pre><code class="language-css">a:any-link {
   color: red;
}</code></pre>

Our second pseudo-class, <code>:local-link</code>, is way more interesting. You could, for example, give a different style to the links that target your home page, leaving all others untouched:

<pre><code class="language-css">nav :local-link {
   text-decoration: none;
}</code></pre>

Thanks to this line of CSS, links pointing to the current page will not have the <code>text-decoration</code> style, so they’ll look different than the others in the menu or breadcrumb.

Let’s see another example:

<pre><code class="language-css">:not(:local-link(0)) {
   color: red;
}</code></pre>

This style will apply red to all external links. (You could add, say, an icon or background image to them if you’d like.)

As you can see in this last example, <code>:local-link</code> can be used with a parameter. The number in the parentheses determines the level of the URL path that will be checked and matched against every given link. Sounds a little complicated, but an example should clarify:

<pre><code class="language-css">nav :local-link(0) {
   color: red;
}
nav :local-link(1) {
   color: green;
}
nav :local-link(2) {
   color: blue;
}
nav :local-link(3) {
   color: yellow;
}
nav :local-link(4) {
   color: gray;
}</code></pre>

Suppose the current address is <code>https://end3r.com/2012/10/20/some-title/</code>, and you have these links in the breadcrumb:

1.  Home `https://end3r.com/`
2.  2012 `https://end3r.com/2012/`
3.  October 2012 `https://end3r.com/2012/10/`
4.  20 October 2012 `https://end3r.com/2012/10/20/`
5.  Article `https://end3r.com/2012/10/20/some-title/`

The first link will be red, the second green, the third blue, then yellow, then gray.</p>

### Time-Dimensional Pseudo-Classes: :past, :current, :future

This pseudo-classes is very handy for users of screen readers. With only one line of CSS, the word being spoken can be given a different style (think karaoke-style):

<pre><code class="language-css">p:current {
   background: yellow;
}</code></pre>

This will highlight the word being spoken in yellow.

The second use case is styling subtitles for the WebVTT video format, changing their color and other properties. The <code>:past</code> and <code>:future</code> pseudo-classes refer, respectively, to elements that have been selected and ones that will be selected.</p>

### UI State Pseudo-Class: :indeterminate

While the UI elements of online forms can be given many interesting pseudo-classes, such as <code>:enabled</code>, <code>:disabled</code> or <code>:checked</code>, one is quite new: <code>:indeterminate</code>. As you may know, checkboxes and radio buttons have two states, either checked or unchecked. Either state can be enabled using the <code>:checked</code> pseudo-class (and <code>:not(:checked)</code> for unchecked). But what if you want to style inputs that haven’t been used? They’re neither checked nor unchecked, so their state is indeterminate. Easy, right? We can give nice styles to these inputs that haven’t been used yet or for which a default state hasn’t been set:

<pre><code class="language-css">input.checkbox:indeterminate {
   background: #ccc;
}</code></pre>

Similarly, a progress bar could be given an indeterminate state when its percentage of completion is unknown:

<pre><code class="language-css">progress:indeterminate {
   background: #ccc;
}</code></pre>

In this situation, we can target the default state and style it to indicate to the user that the time left to load a resource can’t be determined.</p>

### Tree-Structural Pseudo-Classes: :nth-match, :nth-last-match

Tree-structural pseudo-classes are also new and interesting in the Selectors Level 4 specification. With the help of <code>:nth-match</code>, you can now achieve more than ever. Curious how it works? Well, if you take the <code>:nth-child</code> pseudo-class, which selects an item, and combine it with the power of <code>:matches</code>, you’ve got the answer.

Suppose you have a list of links, some of which have the class <code>active</code>, and you want to select only the even-numbered items from the active links. We could use <code>:nth-child(even)</code> to select all of the even-numbered children in the list, but that’s not what we want, because then we wouldn’t be accounting for the <code>active</code> class. Nor is <code>:matches(.active)</code> sufficient, because then we’d be targeting <em>all</em> elements with the class <code>active</code>. This is where <code>:nth-match</code> comes in:

<pre><code class="language-css">li a:nth-match(even of .active) {
   color: red;
}</code></pre>

Thanks to this one line, we can finally select only the even-numbered items from among those that have the <code>active</code> class.

This is just a simple example. We can achieve a lot more using the complex syntax <code>An+B</code>, like so:

<pre><code class="language-css">p:nth-match(2n+1 of .active, .visible, #important) {
   color: red;
}</code></pre>

This combination of selectors we want to match here is more complicated. The <code>:nth-last-match</code> works exactly the same as <code>:nth-match</code> but starts matching from the end of the DOM structure.</p>

### Grid-Structural Pseudo-Classes: :column, :nth-column, :nth-last-column

Let’s apply some pseudo-classes to tabular data. We all know that tables are bad for layouts but good for data that warrants it. An HTML table is row-oriented (<code>&lt;tr&gt;</code>), so columns are missing out. Creating a column-based table is possible, but then you’d be missing rows because you can’t have both at the same time, and row-based tables are more popular. Being able to use CSS to style the columns in a table that is row-based and created in the DOM would be useful when you want to, say, <strong>alternate background colors</strong>. Of course, we could use additional classes or markup; but with a little help from Selectors Level 4, we can do it with grid-structural pseudo-classes.

<pre><code class="language-css">:column(.total) {
   background: red;
}

:nth-column(even) {
   background: blue;
}</code></pre>

This will set red as the background color of every cell in the <code>.total</code> column, and blue for every even-numbered column in the table.

Now we can select columns just like rows, and even get crazy with something like <code>:nth-column(3n+2)</code>. Just remember that columns are styled based on their order in the DOM structure, not how they are displayed on the page. Of course, a table isn’t the only thing that benefits from grid-structural pseudo-classes: column-based layouts are on the way.</p>

### Parent Selector!

This is the long-awaited Swiss Army knife, the holy grail of CSS. It is the most discussed aspect of the Selectors Level 4 specification, and it gives you a lot more power with CSS. Thanks to the parent selector (also referred to as the subject of the selector), you can <strong>easily style elements</strong> other than the default last ones in a selectors list. This can be super-useful when styling generated menus, and you avoid having to add classes for styling purposes only.

Let’s see it in action with the most basic example. Suppose we have a menu, a simple list of links. We want to be able to style it, but the PHP on the server is generating the menu, so we can’t change it. The problem arises when we want to style the <code>li</code> element based on the <code>active</code> class added to the anchor; we can style <code>a</code> using <code>a.active {}</code>, but we can’t get to the <code>li</code> element. The easiest thing to do would be to add the <code>active</code> class to the list element, not to the link itself — like so: <code>ul li.active a</code> — so that we can style both the list and the anchor if needed. The problem is that the menu is generated by a script over which we don’t have control, so we end up with <code>ul li a.active</code>.

In the normal structure of a CSS document, we always refer to the last item in the selectors list. In <code>ul li a.active</code>, that would be the link with the <code>active</code> class; in <code>article p span</code>, it would be the <code>span</code>; and so on. Thanks to the parent selector, we can <strong>change the subject</strong> of the used selector. This gives us incredible power and flexibility when styling:

<pre><code class="language-css">ul li! a.active {
   color: red;
}</code></pre>

Now we can style the <code>li</code> element according to whether the <code>active</code> class has been added to the link. When we add the parent selector, we are saying that we want to style the <code>li</code> element instead of <code>a.active</code>.

We can also manipulate the background color of the whole page just by adding a simple link somewhere in the document:

<pre><code class="language-css">body! header a.styleSwitcher:hover {
   background: red;
}</code></pre>

This applies a red background to the body of the document whenever the user hovers over an anchor with the <code>styleSwitcher</code> class. To do this without the parent selector, you’d have to add custom classes in JavaScript. It’s not impossible, but the native one line in the CSS is definitely the best solution for this.

Note: The first draft of the specification document (dated 29 September 2011) targets the parent selector with a dollar sign before the given selector (<code>$li</code>). The latest draft (22 June 2012) uses new syntax in which the subject of the selector is indicated by an exclamation mark after the given selector (<code>li!</code>). Of course, this could change (it’s just a draft), so don’t forget about it. What matters is that the parent selector will be implemented sooner or later, and the exact syntax is just a matter of preference. It doesn’t matter to me what it looks like, as long as it works properly in the browser.

To see the parent selector in action, check out the <a href="https://github.com/Idered/cssParentSelector">cssParentSelector</a> jQuery plugin.</p>

## Summary

As you can see, the new additions to the Selectors specification look very interesting. I can’t wait to use them in my projects. The only problem is that we will have to wait for them to be implemented in browsers — although you can test some in the browser with the help of a JavaScript library.</p>

### State of the Document

Level 4 of the Selectors document is not yet an official recommendation — just an evolving draft (as demonstrated by the parent selector, which has changed a couple of times and is still in flux). You can’t rely on the document because it will certainly change in future. But there’s an advantage to this: <strong>you can take part in the discussion and suggest ideas</strong>. Everyone with an interesting point of view can add something that will eventually be made part of the official specification.</p>

### Implementation and Browser Support

Some think it’s hard to implement something that’s still a work in progress. Yes, that’s partially true; browser vendors start to think about implementation only when the documentation has gone from messy to solid. But even though we can’t use the goodness of Selectors Level 4 today, we can use something like <a href="https://github.com/amccollum/sel">Sel</a>, one of a few engines that have already implemented some of the features. Thanks to shims and polyfills, we can start experimenting with features that will be available in our favorite browsers in the coming months and even years.</p>

### Other Level 4 Specifications

There are already other Level 4 documents:

*   [CSS4 Media Queries](https://dev.w3.org/csswg/css4-mediaqueries/)
*   [CSS4 Background](https://dev.w3.org/csswg/css4-background/)
*   [CSS4 Images](https://dev.w3.org/csswg/css4-images/)
*   [CSS4 Text](https://dev.w3.org/csswg/css4-text/)

All of them are still in development, so we will have to wait a bit for the next official W3C Working Draft. Of course, you can get involved right away and influence the decisions that will be made.</p>

### Resources

The first and most interesting place to visit, of course, is the <a href="https://www.w3.org/TR/selectors4/">official W3C documentation</a> for Selectors Level 4. Just remember that it’s still <a href="https://dev.w3.org/csswg/selectors4/">in development</a>. You can also check out a couple of interesting articles in the wild, like the <a href="https://generatedcontent.org/post/10865123182/selectors4">one by David Storey</a>, a W3C Working Group member.</p>

### Shape the Future

Help with the document, suggest ideas, comment on other people’s ideas — now is the best time to be a part of the future. Who knows? Maybe in a few years from now, you’ll be in the Working Group and will be responsible for an awesome breakthrough CSS feature that will be used by millions of Web developers every day? It’s an incredible opportunity: to be at the <strong>bleeding edge</strong> of a standard or, better still, to <strong>take part in the creative process</strong> as one of the main contributors!

{{< signature "al" >}}

