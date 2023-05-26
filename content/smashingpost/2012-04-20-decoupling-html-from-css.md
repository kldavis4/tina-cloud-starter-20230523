---
title: Decoupling HTML From CSS
slug: decoupling-html-from-css
image: null
date: 2012-04-20T13:09:56.000Z
author: jonathan-snook
description: >-
  For years, the Web standards community has talked about the separation of
  concerns. Separate your CSS from your JavaScript from your HTML. We all do
  that, right? CSS goes into its own file; JavaScript goes in another; HTML is
  left by itself, nice and clean.
categories:
  - Coding
  - CSS
  - HTML
---
For years, the Web standards community has talked about the separation of concerns. Separate your CSS from your JavaScript from your HTML. We all do that, right? CSS goes into its own file; JavaScript goes in another; HTML is left by itself, nice and clean.

<a href="https://www.csszengarden.com/">CSS Zen Garden</a> proved that we can alter a design into a myriad of permutations simply by changing the CSS. However, we’ve rarely seen the flip side of this — the side that is more likely to occur in a project: the HTML changes. We modify the HTML and then have to go back and revise any CSS that goes with it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Challenging CSS Best Practices](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/)
*   [53 CSS-Techniques You Couldn’t Live Without](https://www.smashingmagazine.com/2007/01/53-css-techniques-you-couldnt-live-without/)
*   [<span class="headline">The Road To Reusable HTML Components</span>](https://www.smashingmagazine.com/2012/10/road-reusable-html-components/)
*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)

In this way, we haven’t really separated the two, have we? We have to make our changes in two places.

{{% feature-panel %}}

## Exploring Approaches

Over the course of my career, I’ve had the pleasure and privilege to work on hundreds of different websites and Web applications. For the vast majority of these projects, I was the sole developer building out the HTML and CSS. I developed a way of coding websites that worked well for me.

Most recently, I spent two years at Yahoo working on Mail, Messenger, Calendar and other projects. Working on a much larger project with a much larger team was a great experience. A small team of prototypers worked with a larger team of designers to build out all of the HTML and CSS for multiple teams of engineers.

It was the largest-scale project I had worked on in many aspects:

*   Yahoo’s user base is massive. Mail alone has about 300 million users.
*   Hundreds of people spread across multiple teams were working with the HTML and CSS.
*   We were developing a system of components to work across multiple projects.

It was during my time at Yahoo that I began to really examine how I and the team at Yahoo build websites. What pain points did we keep running into, and how could we avoid them?

I looked to see what everyone else was doing. I looked at Nicole Sullivan’s <a title="Object Oriented CSS" href="https://github.com/stubbornella/oocss/wiki">Object-Oriented CSS</a>, Jina Bolton’s presentation on “<a href="https://vimeo.com/15982903">CSS Workflow</a>” and Natalie Downe’s “<a href="https://www.slideshare.net/nataliedowne/practical-maintainable-css">Practical, Maintainable CSS</a>,” to name just a few.

I ended up writing my thoughts as a long-form style guide named “<a href="https://smacss.com/">Scalable and Modular Architecture for CSS</a>.” That sounds wordy, so you can just call it SMACSS (pronounced “smacks”) for short. It’s a guide that continues to evolve as I refine and expand on ways to approach CSS development.

As a result of this exploration, I’ve noticed that designers (including me) traditionally write CSS that is deeply tied to the HTML that it is designed to style. How do we begin to decouple the two for more flexible development with less refactoring?

In other words, how do we avoid throwing <code>!important</code> at everything or falling into selector hell?

## Reusing Styles

In the old days, we wrapped <code>font</code> tags and applied <code>background</code> attributes to every HTML element that needed styling. This was, of course, very impractical, and thus CSS was born. CSS enabled us to reuse styles from one part of the page on another.

For example, a navigation menu has a list of items that all look the same. Repeating inline styles on each item wouldn’t be practical. As a result, we begin to see CSS like this:

<pre><code class="language-css">#nav {
   margin: 0;
   padding: 0;
   list-style: none;
}

#nav li {
   float: left;
}

#nav li a {
   display: block;
   padding: 5px 10px;
   background-color: blue;
}</code></pre>

Sure beats adding <code>float:left</code> to every list item and <code>display:block; padding:5px 10px;</code> to every link. Efficiency, for the win! Just looking at this, you can see the HTML structure that is expected:

<pre><code class="language-markup tmp-html">&lt;ul id="nav"&gt;
   &lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
   &lt;li&gt;&lt;a href="/products"&gt;Products&lt;/a&gt;&lt;/li&gt;
   &lt;li&gt;&lt;a href="/contact"&gt;Contact Us&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

Now, the client comes back and says, “I want a drop-down menu to appear when the user clicks on ‘Products.’ Give them easy access to each of the pages!” As a result, our HTML changes.

<pre><code class="language-markup tmp-html">&lt;ul id="nav"&gt;
   &lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
   &lt;li&gt;&lt;a href="/products"&gt;Products&lt;/a&gt;
      &lt;ul&gt;
         &lt;li&gt;&lt;a href="/products/shoes"&gt;Shoes&lt;/a&gt;&lt;/li&gt;
         &lt;li&gt;&lt;a href="/products/jackets"&gt;Jackets&lt;/a&gt;&lt;/li&gt;
      &lt;/ul&gt;
   &lt;/li&gt;
   &lt;li&gt;&lt;a href="/contact"&gt;Contact Us&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

We now have a list item within a list item, and links within it. Our menu has a horizontal navigation when the client wants a vertical list, so we add some rules to style the inner list to match what the client wants.

<pre><code class="language-css">#nav ul {
   margin: 0;
   padding:0;
   list-style:none;
}

#nav li li {
   float: none;
}

#nav li li a {
   padding: 2px;
   background-color: red;
}</code></pre>

Problem solved! Sort of.</p>

## Reducing The Depth Of Applicability

Probably the most common problem with CSS is managing specificity. Multiple CSS rules compete in styling a particular element on the page. With our menu, our initial rules were styling the list items and the links in the navigation and the menu. Not good.

By adding more element selectors, we were able to increase specificity and have our menu styles win out over the navigation styles.

However, this can become a game of cat and mouse as a project increases in complexity. Instead, we should be limiting the impact of CSS. Navigation styles should apply to and affect only the elements that pertain to it, and menu styles should apply to and affect only the elements that pertain to it.

I refer to this impact in SMACSS as the “<a href="https://smacss.com/book/applicability">depth of applicability</a>.” It’s the depth at which a particular rule set impacts the elements around it. For example, a style like <code>#nav li a</code>, when given an HTML structure that includes our menus, has a depth of 5: from the <code>ul</code> to the <code>li</code> to the <code>ul</code> to the <code>li</code> to the <code>a</code>.

The deeper the level of applicability, the more impact the styles can have on the HTML and the more tightly coupled the HTML is to the CSS.

The goal of more manageable CSS — especially in larger projects — is to limit the depth of applicability. In other words, write CSS to affect only the elements that we want them to affect.</p>

### Child Selectors

One tool for limiting the scope of CSS is the child selector (<code>&gt;</code>). If you no longer have to worry about Internet Explorer 6 (and, thankfully, many of us don’t), then the child selector should be a regular part of your CSS diet.

Child selectors limit the scope of selectors. Going back to our navigation example, we can use the child selector to limit the scope of the navigation so that it does not affect the menu.

<pre><code class="language-css">#nav {
   margin: 0;
   padding: 0;
   list-style: none;
}

#nav &gt; li {
   float: left;
}

#nav &gt; li &gt; a {
   display: block;
   padding: 5px 10px;
   background-color: blue;
}</code></pre>

For the menu, let’s add a class name to it. This will make it more descriptive and provide a base for the rest of our styles.

<pre><code class="language-css">.menu {
   margin: 0;
   padding: 0;
   list-style: none
}

.menu &gt; li &gt; a { 2px;
   background-color: red;
}</code></pre>

What we’ve done is limited the scope of our CSS and isolated two visual patterns into separate blocks of CSS: one for our navigation list and one for our menu list. We’ve taken a small step towards modularizing our code and a step towards decoupling the HTML from the CSS.</p>

## Classifying Code

Limiting the depth of applicability helps to minimize the impact that a style might have on a set of elements much deeper in the HTML. However, the other problem is that as soon as we use an element selector in our CSS, we are depending on that HTML structure never to change. In the case of our navigation and menu, it’s always a list with a bunch of list items, with a link inside each of those. There’s no flexibility to these modules.

Let’s look at an example of something else we see in many designs: a box with a heading and a block of content after it.

<pre><code class="language-markup tmp-html">&lt;div class="box"&gt;
   &lt;h2&gt;Sites I Like&lt;/h2&gt;
   &lt;ul&gt;
      &lt;li&gt;&lt;a href="https://smashingmagazine.com/"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://smacss.com/"&gt;SMACSS&lt;/a&gt;&lt;/li&gt;
   &lt;/ul&gt;
&lt;/div&gt;</code></pre>

Let’s give it some styles.

<pre><code class="language-css">.box {
   border: 1px solid #333;
}

.box h2 {
   margin: 0;
   padding: 5px 10px;
   border-bottom: 1px solid #333;
   background-color: #CCC;
}

.box ul {
   margin: 10px;
}</code></pre>

The client comes back and says, “That box is great, but can you add another one with a little blurb about the website?”

<pre><code class="language-markup tmp-html">&lt;div class="box"&gt;
   &lt;h2&gt;About the Site&lt;/h2&gt;
   &lt;p&gt;This is my blog where I talk about only the bestest things in the whole wide world.&lt;/p&gt;
&lt;/div&gt;</code></pre>

In the previous example, a margin was given to the list to make it line up with the heading above it. With the new code example, we need to give it similar styling.

<pre><code class="language-css">.box ul, .box p {
   margin: 10px;
}</code></pre>

That’ll do, assuming that the content never changes. However, the point of this exercise is to recognize that websites can and do change. Therefore, we have to be proactive and recognize that there are alternative elements we might want to use.

For greater flexibility, let’s use classes to define the different parts of this module:

<pre><code class="language-css">.box .hd { }  /* this is our box heading */
.box .bd { }  /* this is our box body */</code></pre>

When applied to the HTML, it looks like this:

<pre><code class="language-markup tmp-html">&lt;div class="box"&gt;
   &lt;h2 class="hd"&gt;About the Site&lt;/h2&gt;
   &lt;p class="bd"&gt;This is my blog where I talk about only the bestest things in the whole wide world.&lt;/p&gt;
&lt;/div&gt;</code></pre>

### Clarifying Intent

Different elements on the page could have a heading and a body. They’re “protected” in that they’re a child selector of <code>box</code>. But this isn’t always as evident when we’re looking at the HTML. We should clarify that these particular <code>hd</code> and <code>bd</code> classes are for the <code>box</code> module.

<pre><code class="language-css">.box .box-hd {}
.box .box-bd {}</code></pre>

With this improved naming convention, we don’t need to combine the selectors anymore in an attempt to namespace our CSS. Our final CSS looks like this:

<pre><code class="language-css">.box {
border: 1px solid #333;
}

.box-hd {
margin: 0;
padding: 5px 10px;
border-bottom: 1px solid #333;
background-color: #CCC;
}

.box-bd {
   margin: 10px;
}</code></pre>

The bonus of this is that each of these rules affects only a single element: the element that the class is applied to. Our CSS is easier to read and easier to debug, and it’s clear what belongs to what and what it does.</p>

## It’s All Coming Undone

We’ve just seen two ways to decouple HTML from CSS:

1.  Using child selectors,
2.  Using class selectors.

In addition, we’ve seen how naming conventions allow for clearer, faster, simpler and more understandable code.

These are just a couple of the concepts that I cover in “<a href="https://smacss.com/book/">Scalable and Modular Architecture for CSS</a>,” and I invite you to read more.</p>

### Postscript

In addition to the resources linked to above, you may wish to look into <span class="removed_link" title="https://bem.github.com/bem-method/pages/beginning/beginning.en.html">BEM</span>, an alternative approach to and framework for building maintainable CSS. Mark Otto has also been documenting the development of Twitter Bootstrap, including the recent article “<a href="https://www.markdotto.com/2012/03/02/stop-the-cascade/">Stop the Cascade</a>,” which similarly discusses the need to limit the scope of styles.

<em>(al) (il)</em>

