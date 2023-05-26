---
title: Coding An HTML 5 Layout From Scratch
slug: designing-a-html-5-layout-from-scratch
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63359009-cca5-43fe-bc88-c928d5dbac4d/01-html-baby-opt.jpg
date: 2009-08-04T07:00:46.000Z
author: enrique-ramirez
description: >-
  **HTML5** and **CSS3** have just arrived (kinda), and with them a whole new
  battle for the 'best markup' trophy has begun. Truth to be told, all these
  technologies are mere tools waiting for a skilled developer to work on the
  right project. As developers we shouldn't get into pointless discussions of
  which markup is the best. They all lead to nowhere. Rather, we must get a
  brand new ideology and modify our coding habits to keep the web accessible.
categories:
  - Coding
  - Layouts
  - HTML5
  - HTML
---
<strong>HTML5</strong> and <strong>CSS3</strong> have just arrived (kinda), and with them a whole new battle for the 'best markup' trophy has begun. Truth to be told, all these technologies are mere tools waiting for a skilled developer to work on the right project. As developers we shouldn't get into pointless discussions of which markup is the best. They all lead to nowhere. Rather, we must get a brand new ideology and modify our coding habits to keep the web accessible. 

While it is true <a title="Road Map To Coding With HTML5: Tutorials and Guidelines" href="https://www.smashingmagazine.com/coding-with-html5-tutorials-guidelines/">HTML5</a> and <a title="Push Your Web Design Into The Future With CSS3" href="https://www.smashingmagazine.com/2009/01/push-your-web-design-into-the-future-with-css3/">CSS3</a> are both a work in progress and is going to stay that way for some time, there's no reason not to start using it <strong>right now</strong>. After all, time's proven that implementation of <a href="https://www.w3.org/TR/CSS2/" rel="external">unfinished specifications</a> does work and can be easily mistaken by a complete W3C recommendation. That's were <strong>Progressive Enhancement</strong> and <strong>Graceful Degradation</strong> come into play.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sexy New HTML5 Semantics](https://www.smashingmagazine.com/2011/11/html5-semantics/)
*   [Learning to Love HTML5](https://www.smashingmagazine.com/2010/11/learning-to-love-html5/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/html-5-cheat-sheet-pdf/)

{{% feature-panel %}}

<p>So today we're going to experiment a little with these new technologies. At the end of this article you'll learn how to:</p>

*   Use Graceful Degradation techniques and technologies to keep things in place for legacy browsers.
*   Use Progressive Enhancement techniques and technologies to be up to date with the latest trends.
*   Use HTML5 alongside a rising technology: [Microformats](https://www.smashingmagazine.com/2007/05/microformats-what-they-are-and-how-to-use-them/ "Microformats: What They Are and How To Use Them").
*   Have a clear vision of some of the most exciting new features HTML5 and CSS3 will bring.

It'd be a good idea to have a read at some of these articles first:

*   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/16/html5-and-the-future-of-the-web/ "HTML5 and The Future of the Web") which teaches the very basics of HTML5, introduces new elements and explains some of the advantages of the new markup language.
*   [HTML5 enabling script](https://remysharp.com/2009/01/07/html5-enabling-script/ "HTML5 enabling script") which shows a method that enables HTML5 tags on IE6 to be styled.
*   [Understanding aside](https://html5doctor.com/understanding-aside/ "HTML5 understanding Aside") where the usually misunderstood new tag is explained.

I'll also assume you know the basics of HTML and CSS. Including all the "old school" tags and the basic selectors and properties.</p>

## The HTML 5 Layout - Before we begin...

There's a couple of things you have to bear in mind before adventuring on the new markup boat. HTML5 is not for everyone. Therefore, you must be wise and select how and where to use it. Think of all the markup flavours you've got available as tools: use the right one for the right job. Therefore, if your website is coded in standards compliant <strong>XHTML strict</strong> there's no real need to change to HTML5.

There's also the fact that by using HTML5 code right now your website gets stuck in some kind of "limbo" since even though your browser will render HTML5, it <strong>does not understand it</strong> as of yet. This may also apply to other software such as <strong>screenreaders</strong> and <strong>search engines.</strong>

Lastly you must consider that HTML5 is still under heavy development, and it's probably the "most open" project the W3C has ever done. With the immense amount of feedback and all the hype around it, <a href="https://dev.w3.org/html5/spec/Overview.html" rel="external">the current draft</a> is bound to change and it's impossible to predict how much.

So if you're ready to do the switch, are not afraid of using technology that in the near future will be way more meaningful and can easily change whatever piece of code that might get broken, then keep reading.</p>

## A word on Progressive Enhancement and Graceful Degradation

So what are these two terms all about? <strong>Graceful Degradation</strong> is a widely used term which ideology is basically using the latest technologies first, and then fix anything that needs fixing for older browsers. We do this on a daily basis: most of us code for Firefox first, then fix Internet Explorer. That is Graceful Degradation in the practice.

<strong>Progressive Enhancement</strong> refers to the habit of building first for the less capable, outdated browser and then enhance for the latest technologies. We, too, use this on a daily basis. For example, most of the times we code a website we start with the markup and then apply an external CSS file where we add all the styling. That is Progressive Enhancement in the practice.

Both technologies usually go hand in hand and have been part of the ways we do things for years. It's just the terms that are not that well-known. And now, both of these practices need to evolve due to the new languages that are approaching. If you want to go deeper into both of these terms, <a title="Graceful Degradation and Progressive Enhancement" href="https://accessites.org/site/2007/02/graceful-degradation-progressive-enhancement/" rel="external">check a related article on accessites.org</a>.</p>

## 1\. The Design

This will be the sample layout we'll be coding:

[![HTML 5 Layout](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12dfc62a-6854-414b-97c7-2c4f3a50f7ae/design-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0834045e-4970-486e-a28d-8a3b22cafdb2/index.html)

A very basic layout brilliantly named <em>Smashing HTML5!</em> which covers most of the elements we can start coding using HTML5. Basically: the page's name and it's slogan, a menu, a highlighted (featured) area, a post listing, an extras section with some external links, an about box and finally a copyright statement.</p>

## 2\. The markup

As a very basic start to our markup, this is our html file skeleton:

<pre><code class="language-markup"> 
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
&lt;meta charset="utf-8" /&gt;
&lt;title&gt;Smashing HTML5!&lt;/title&gt;

&lt;link rel="stylesheet" href="css/main.css" type="text/css" /&gt;

&lt;!--[if IE]&gt;
  &lt;script src="https://html5shiv.googlecode.com/svn/trunk/html5.js"&gt;&lt;/script&gt;&lt;![endif]--&gt;
&lt;!--[if lte IE 7]&gt;
  &lt;script src="js/IE8.js" type="text/javascript"&gt;&lt;/script&gt;&lt;![endif]--&gt;
&lt;!--[if lt IE 7]&gt;

  &lt;link rel="stylesheet" type="text/css" media="all" href="css/ie6.css"/&gt;&lt;![endif]--&gt;
&lt;/head&gt;

&lt;body id="index" class="home"&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

A few highlights:

*   3 different [Conditional comments](https://www.quirksmode.org/css/condcom.html "Conditional Comments") for IE. First one includes [html5 shiv](https://remysharp.com/2009/01/07/html5-enabling-script/) code directly from Google Code for all versions of IE. The second one includes [IE8.js](https://code.google.com/p/ie7-js/ "IE8.js") for better backwards compatibility for IE7 and below as well as an ie.css file which will sove IE7 and below CSS bugs. Third one is just a CSS file to fix IE6 bugs.
*   The use of an "index" id and a "home" class on the `<body>` tag. This is just a habit I've developed over the past year that has simplified the coding of inner-sections of overly complicated websites.
*   A simplified version of the charset property for better backwards compatibility with legacy browsers.
*   I'm using XHTML 1.0 syntax on a HTML5 document. That's the way I roll. It's a habit that I really like and since [I can still use it](https://www.w3.org/TR/html-design-principles/#pave-the-cowpaths "Pave the Cowpaths principle"), I will. You can, however, use normal HTML syntax here. That is, uppercase attribute and tag names, unclosed tags and no quotes for wrapping attributes' values. It's up to you.

This is a very basic and solid startup for all and any HTML5 projects you might do in the future. With this, we can start assigning tags to the different sections of our layout.

If we had an x-ray machine designed for websites, this would be our page's skeleton:

![Smashing HTML5! template x-rayed](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acff5986-b283-45ac-949e-e8a690259ba9/design-x-ray.png)

### The header

![Smashing HTML5! Header block](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c15d404-c38a-4e32-aae2-e37d981ec060/header-block.png)

The layout header is as simple as it gets. The new <a title="The header tag spec" href="https://dev.w3.org/html5/spec/Overview.html#the-header-element" rel="external"><code>&lt;header&gt;</code></a> tag spec reads as follows:
<blockquote>The header element represents a group of introductory or navigational aids</blockquote>

Thus it is more than logic that we use this to markup our header. We'll also use the <a title="The Nav Tag spec" href="https://dev.w3.org/html5/spec/Overview.html#the-nav-element" rel="external"><code>&lt;nav&gt;</code></a> tag. The spec reads:
<blockquote cite="https://dev.w3.org/html5/spec/Overview.html#the-nav-element">The <code>nav</code> element represents a section of a page that links to other pages or to parts within the page: a section with navigation links. Not all groups of links on a page need to be in a nav element — only sections that consist of major navigation blocks are appropriate for the nav element.</blockquote>

There's a lot of buzz regarding the spec of the nav element since "major navigation blocks" is not a very helpful description. But this time we're talking about our main website navigation; it can't get any major than that. So after a couple of id's and classes our header ends up like this:

<pre><code class="language-markup">
&lt;header id="banner" class="body"&gt;
  &lt;h1&gt;&lt;a href="#"&gt;Smashing HTML5! &lt;strong&gt;HTML5 in the year &lt;del&gt;2022&lt;/del&gt; &lt;ins&gt;2009&lt;/ins&gt;&lt;/strong&gt;&lt;/a&gt;&lt;/h1&gt;

  &lt;nav&gt;&lt;ul&gt;
    &lt;li class="active"&gt;&lt;a href="#"&gt;home&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;portfolio&lt;/a&gt;&lt;/li&gt;

    &lt;li&gt;&lt;a href="#"&gt;blog&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;contact&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;&lt;/nav&gt;

&lt;/header&gt;&lt;!-- /#banner --&gt;
</code></pre>

### Featured block

![Smashing HTML5! Featured block](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7640bcbe-eae9-4942-b7c5-e92e5084341d/featured-block.png)

Next is the featured block. This is best marked up as an <a title="The aside tag spec" href="https://dev.w3.org/html5/spec/Overview.html#the-aside-element" rel="external"><code>&lt;aside&gt;</code></a> since it's spec says:
<blockquote cite="https://dev.w3.org/html5/spec/Overview.html#the-aside-element">The aside element represents a section of a page that consists of content that is tangentially related to the content around the aside element, and which could be considered separate from that content. Such sections are often represented as sidebars in printed typography.</blockquote>

That pretty much sums up our featured block, so let's go for it. Now, inside of this block there's a lot going on. Firstly, this is an article, so alongside the <code>&lt;aside&gt;</code> tag, we should be using <a title="The article tag Spec" href="https://dev.w3.org/html5/spec/Overview.html#the-article-element" rel="external"><code>&lt;article&gt;</code></a> right away.

We also have two consecutive headings ('Featured Article' and 'HTML5 in Smashing Magazine!') so we'll be using yet another new element: <a title="The hgroup tag Spec" href="https://dev.w3.org/html5/spec/Overview.html#the-hgroup-element" rel="external"><code>&lt;hgroup&gt;</code></a>. This is a wonderful tag used for grouping series of <code>&lt;h#&gt;</code> tags which is exactly what we have here. It exist <q cite="https://dev.w3.org/html5/spec/Overview.html#the-hgroup-element">to mask an h2 element (that acts as a secondary title) from the outline algorithm</q>, which will save developers some headaches in the future.

The last element on this block is the Smashing Magazine logo to the right. We have yet another new tag for this element: <a title="The figure tag Spec" href="https://dev.w3.org/html5/spec/Overview.html#the-figure-element" rel="external"><code>&lt;figure&gt;</code></a>. This tag is used to enclose <q cite="https://dev.w3.org/html5/spec/Overview.html#the-figure-element">some flow content, optionally with a caption, that is self-contained and is typically referenced as a single unit from the main flow of the document</q>. This tag allows us to use a <code>&lt;legend&gt;</code> tag to add a caption to the elements inside. Sadly, this last feature is broken on some browsers as they try to add a <code>&lt;fieldset&gt;</code> around and it is impossible to override it with simple CSS rules. Therefore, I'd suggest leaving it aside and just use <code>&lt;figure&gt;</code> for the time being.

Featured block code will look like this in the end:

<pre><code class="language-markup">
&lt;aside id="featured" class="body"&gt;&lt;article&gt;
  &lt;figure&gt;
    &lt;img src="images/temp/sm-logo.gif" alt="Smashing Magazine" /&gt;
  &lt;/figure&gt;
  &lt;hgroup&gt;

    &lt;h2&gt;Featured Article&lt;/h2&gt;
    &lt;h3&gt;&lt;a href="#"&gt;HTML5 in Smashing Magazine!&lt;/a&gt;&lt;/h3&gt;
  &lt;/hgroup&gt;
  &lt;p&gt;Discover how to use Graceful Degradation and Progressive Enhancement techniques to achieve an outstanding, cross-browser &lt;a href="https://dev.w3.org/html5/spec/Overview.html" rel="external"&gt;HTML5&lt;/a&gt; and &lt;a href="https://www.w3.org/TR/css3-roadmap/" rel="external"&gt;CSS3&lt;/a&gt; website today!&lt;/p&gt;

&lt;/article&gt;&lt;/aside&gt;&lt;!-- /#featured --&gt;
</code></pre>

### The layout's body

![Smashing HTML5! Body block](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24818cac-5cdb-4ae3-91e1-4646eb41685b/body-block.png)

Next is our document's body, where all the content will be. Since this block <q cite="https://dev.w3.org/html5/spec/Overview.html#the-section-element">represents a generic document section</q> and a section is <q cite="https://dev.w3.org/html5/spec/Overview.html#the-section-element">a thematic grouping of content</q>, this one is without a doubt a <a title="The section tag spec" href="https://dev.w3.org/html5/spec/Overview.html#the-section-element" rel="external"><code>&lt;section&gt;</code></a> tag.

For the posts, we'll use the old <code>&lt;ol&gt;</code> tag since, well, it's an ordered list of articles. Each <code>&lt;li&gt;</code> should have an <code>&lt;article&gt;</code> tag and within this, we'll have a <code>&lt;header&gt;</code> for the <strong>post title</strong>, a <code>&lt;footer&gt;</code> for the <strong>post information</strong> and a <code>&lt;div&gt;</code> for the <strong>post content</strong>. Yes, a <code>&lt;div&gt;</code>.

The reason for using a div is simple: we'll be using the <a title="hAtom 0.1 Microformat draft" href="https://microformats.org/wiki/hatom" rel="external">hAtom 0.1 Microformat</a> and it requires the content entry to be wrapped by an element. Since no other tag applies to this (it is not a section, it is not a full article, it is not a footer, etc.) we'll use a <code>&lt;div&gt;</code> since it provides no semantic value by itself and keeps the markup as clean as possible.

With all these tags, and the hAtom microformat in place, the code shall look like this:

<pre><code class="language-markup">
&lt;section id="content" class="body"&gt;

  &lt;ol id="posts-list" class="hfeed"&gt;

    &lt;li&gt;&lt;article class="hentry"&gt;  
      &lt;header&gt;
        &lt;h2 class="entry-title"&gt;&lt;a href="#" rel="bookmark" title="Permalink to this POST TITLE"&gt;This be the title&lt;/a&gt;&lt;/h2&gt;
      &lt;/header&gt;

      &lt;footer class="post-info"&gt;
        &lt;abbr class="published" title="2005-10-10T14:07:00-07:00"&gt;&lt;!-- YYYYMMDDThh:mm:ss+ZZZZ --&gt;
          10th October 2005
        &lt;/abbr&gt;

        &lt;address class="vcard author"&gt;
          By &lt;a class="url fn" href="#"&gt;Enrique Ramírez&lt;/a&gt;

        &lt;/address&gt;
      &lt;/footer&gt;&lt;!-- /.post-info --&gt;

      &lt;div class="entry-content"&gt;
        &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque venenatis nunc vitae libero iaculis elementum. Nullam et justo &lt;a href="#"&gt;non sapien&lt;/a&gt; dapibus blandit nec et leo. Ut ut malesuada tellus.&lt;/p&gt;

      &lt;/div&gt;&lt;!-- /.entry-content --&gt;
    &lt;/article&gt;&lt;/li&gt;

    &lt;li&gt;&lt;article class="hentry"&gt;
      ...
    &lt;/article&gt;&lt;/li&gt;

    &lt;li&gt;&lt;article class="hentry"&gt;
      ...
    &lt;/article&gt;&lt;/li&gt;
  &lt;/ol&gt;&lt;!-- /#posts-list --&gt;

&lt;/section&gt;&lt;!-- /#content --&gt;

</code></pre>

For the mighty ones: yes, I did not use the <a href="https://dev.w3.org/html5/spec/Overview.html#the-time-element"><code>&lt;time&gt;</code></a> element. This tag is rather new, and it is not compatible with the current <strong>microformat</strong> implementations out there. Since I'm indeed using hAtom it made little point to have both an invalid microformat and a yet-incomprehensible tag. If you're not using a microformat, I'd suggest using <code>&lt;time&gt;</code> instead.</p>

### The extras block

![Smashing HTML5! Extras block](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f503db25-b6f2-42bf-b78a-b83e29f9615b/extras-block.png)

The extras block is yet another section of our document. You might struggle for a while deciding whether an <code>&lt;aside&gt;</code> or a <code>&lt;section&gt;</code> tag would be best for this section. In the end, this section could not be <q cite="https://dev.w3.org/html5/spec/Overview.html#the-aside-element">considered separate from the main content</q> since it contains the blogroll links and some social information of the website. Thus, a <code>&lt;section&gt;</code> element is more appropriate.

Here we'll also find another use for the <code>&lt;div&gt;</code> tag. For styling needs and grouping's sake, we may add two divs here: one for the <strong>blogroll</strong> section and one for the <strong>social</strong> section.

For the rest of the block there's nothing much to decide. It's the everyday <code>&lt;ul&gt;</code> accommodated set of links on both sections, which in the end may look like this:

<pre><code class="language-markup">
&lt;section id="extras" class="body"&gt;
  &lt;div class="blogroll"&gt;
    &lt;h2&gt;blogroll&lt;/h2&gt;
    &lt;ul&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Spec (working draft)&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;W3C&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wordpress&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wikipedia&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Spec (working draft)&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;W3C&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wordpress&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wikipedia&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Spec (working draft)&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;W3C&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wordpress&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wikipedia&lt;/a&gt;&lt;/li&gt;

    &lt;/ul&gt;
  &lt;/div&gt;&lt;!-- /.blogroll --&gt;

  &lt;div class="social"&gt;
    &lt;h2&gt;social&lt;/h2&gt;
    &lt;ul&gt;

      &lt;li&gt;&lt;a href="https://delicious.com/enrique_ramirez" rel="me"&gt;delicious&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://digg.com/users/enriqueramirez" rel="me"&gt;digg&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://facebook.com/enrique.ramirez.velez" rel="me"&gt;facebook&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="https://www.lastfm.es/user/enrique-ramirez" rel="me"&gt;last.fm&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://website.com/feed/" rel="alternate"&gt;rss&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://twitter.com/enrique_ramirez" rel="me"&gt;twitter&lt;/a&gt;&lt;/li&gt;

    &lt;/ul&gt;
  &lt;/div&gt;&lt;!-- /.social --&gt;
&lt;/section&gt;&lt;!-- /#extras --&gt;
</code></pre>

### The About and footer blocks

![Smashing HTML5! About and Footer blocks](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/849ea6ee-83be-4db9-97a4-d7b084d72576/about-footer-block.png)

The footer has no real difficulty. We'll use the brand new <a title="The footer Tag spec" href="https://dev.w3.org/html5/spec/Overview.html#the-footer-element" rel="external"><code>&lt;footer&gt;</code></a> tag to wrap both the about and the copyright information since the spec reads:
<blockquote cite="https://dev.w3.org/html5/spec/Overview.html#the-footer-element">The footer element represents a footer for its nearest ancestor sectioning content. A footer typically contains information about its section such as who wrote it, links to related documents, copyright data, and the like.</blockquote>

Since the nearer ancestor of our <code>&lt;footer&gt;</code> tag is the <code>&lt;body&gt;</code> tag, is more than right to wrap both elements here since we're adding information about the website's owner (and thus, author).

For the about block we'll use an <code>&lt;address&gt;</code> tag, which <q cite="https://dev.w3.org/html5/spec/Overview.html#the-address-element">contains contact information for it's nearest <code>&lt;article&gt;</code> or <code>&lt;body&gt;</code> element ancestor</q>. We'll also use the <a title="hCard standard" href="https://microformats.org/wiki/hcard" rel="external">hCard Microformat</a> to enhance the semantic value. For the copyright information we'll go with a simple <code>&lt;p&gt;</code> tag so the code ends like this:

<pre><code class="language-markup">
&lt;footer id="contentinfo" class="body"&gt;
  &lt;address id="about" class="vcard body"&gt;
    &lt;span class="primary"&gt;
      &lt;strong&gt;&lt;a href="#" class="fn url"&gt;Smashing Magazine&lt;/a&gt;&lt;/strong&gt;

      &lt;span class="role"&gt;Amazing Magazine&lt;/span&gt;
    &lt;/span&gt;&lt;!-- /.primary --&gt;

    &lt;img src="images/avatar.gif" alt="Smashing Magazine Logo" class="photo" /&gt;
    &lt;span class="bio"&gt;Smashing Magazine is a website and blog that offers resources and advice to web developers and web designers. It was founded by Sven Lennartz and Vitaly Friedman.&lt;/span&gt;

  &lt;/address&gt;&lt;!-- /#about --&gt;
  &lt;p&gt;2005-2009 &lt;a href="https://smashingmagazine.com"&gt;Smashing Magazine&lt;/a&gt;.&lt;/p&gt;
&lt;/footer&gt;&lt;!-- /#contentinfo --&gt;
</code></pre>

### Summing it all up

So, after all this mess, the complete code looks like this:

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
&lt;meta charset="utf-8" /&gt;
&lt;title&gt;Smashing HTML5!&lt;/title&gt;

&lt;link rel="stylesheet" href="css/main.css" type="text/css" /&gt;

&lt;!--[if IE]&gt;
  &lt;script src="https://html5shiv.googlecode.com/svn/trunk/html5.js"&gt;&lt;/script&gt;&lt;![endif]--&gt;
&lt;!--[if lte IE 7]&gt;
  &lt;script src="js/IE8.js" type="text/javascript"&gt;&lt;/script&gt;&lt;![endif]--&gt;

&lt;!--[if lt IE 7]&gt;
  &lt;link rel="stylesheet" type="text/css" media="all" href="css/ie6.css"/&gt;&lt;![endif]--&gt;
&lt;/head&gt;

&lt;body id="index" class="home"&gt;

&lt;header id="banner" class="body"&gt;
  &lt;h1&gt;&lt;a href="#"&gt;Smashing HTML5! &lt;strong&gt;HTML5 in the year &lt;del&gt;2022&lt;/del&gt; &lt;ins&gt;2009&lt;/ins&gt;&lt;/strong&gt;&lt;/a&gt;&lt;/h1&gt;

  &lt;nav&gt;&lt;ul&gt;
    &lt;li class="active"&gt;&lt;a href="#"&gt;home&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;portfolio&lt;/a&gt;&lt;/li&gt;

    &lt;li&gt;&lt;a href="#"&gt;blog&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;contact&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;&lt;/nav&gt;

&lt;/header&gt;&lt;!-- /#banner --&gt;  

&lt;aside id="featured" class="body"&gt;&lt;article&gt;
  &lt;figure&gt;
    &lt;img src="images/temp/sm-logo.gif" alt="Smashing Magazine" /&gt;
  &lt;/figure&gt;
  &lt;hgroup&gt;

    &lt;h2&gt;Featured Article&lt;/h2&gt;
    &lt;h3&gt;&lt;a href="#"&gt;HTML5 in Smashing Magazine!&lt;/a&gt;&lt;/h3&gt;
  &lt;/hgroup&gt;
  &lt;p&gt;Discover how to use Graceful Degradation and Progressive Enhancement techniques to achieve an outstanding, cross-browser &lt;a href="https://dev.w3.org/html5/spec/Overview.html" rel="external"&gt;HTML5&lt;/a&gt; and &lt;a href="https://www.w3.org/TR/css3-roadmap/" rel="external"&gt;CSS3&lt;/a&gt; website today!&lt;/p&gt;

&lt;/article&gt;&lt;/aside&gt;&lt;!-- /#featured --&gt;

&lt;section id="content" class="body"&gt;
  &lt;ol id="posts-list" class="hfeed"&gt;
    &lt;li&gt;&lt;article class="hentry"&gt;  
      &lt;header&gt;
        &lt;h2 class="entry-title"&gt;&lt;a href="#" rel="bookmark" title="Permalink to this POST TITLE"&gt;This be the title&lt;/a&gt;&lt;/h2&gt;

      &lt;/header&gt;

      &lt;footer class="post-info"&gt;
        &lt;abbr class="published" title="2005-10-10T14:07:00-07:00"&gt;&lt;!-- YYYYMMDDThh:mm:ss+ZZZZ --&gt;
          10th October 2005
        &lt;/abbr&gt;

        &lt;address class="vcard author"&gt;

          By &lt;a class="url fn" href="#"&gt;Enrique Ramírez&lt;/a&gt;
        &lt;/address&gt;
      &lt;/footer&gt;&lt;!-- /.post-info --&gt;

      &lt;div class="entry-content"&gt;

        &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque venenatis nunc vitae libero iaculis elementum. Nullam et justo &lt;a href="#"&gt;non sapien&lt;/a&gt; dapibus blandit nec et leo. Ut ut malesuada tellus.&lt;/p&gt;
      &lt;/div&gt;&lt;!-- /.entry-content --&gt;
    &lt;/article&gt;&lt;/li&gt;

    &lt;li&gt;&lt;article class="hentry"&gt;
      ...
    &lt;/article&gt;&lt;/li&gt;

    &lt;li&gt;&lt;article class="hentry"&gt;
      ...
    &lt;/article&gt;&lt;/li&gt;

  &lt;/ol&gt;&lt;!-- /#posts-list --&gt;
&lt;/section&gt;&lt;!-- /#content --&gt;

&lt;section id="extras" class="body"&gt;
  &lt;div class="blogroll"&gt;
    &lt;h2&gt;blogroll&lt;/h2&gt;

    &lt;ul&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Spec (working draft)&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;W3C&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wordpress&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wikipedia&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Spec (working draft)&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;W3C&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wordpress&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wikipedia&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Doctor&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;HTML5 Spec (working draft)&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;Smashing Magazine&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;W3C&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wordpress&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="#" rel="external"&gt;Wikipedia&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;&lt;!-- /.blogroll --&gt;

  &lt;div class="social"&gt;

    &lt;h2&gt;social&lt;/h2&gt;
    &lt;ul&gt;
      &lt;li&gt;&lt;a href="https://delicious.com/enrique_ramirez" rel="me"&gt;delicious&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://digg.com/users/enriqueramirez" rel="me"&gt;digg&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="https://facebook.com/enrique.ramirez.velez" rel="me"&gt;facebook&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://www.lastfm.es/user/enrique-ramirez" rel="me"&gt;last.fm&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="https://website.com/feed/" rel="alternate"&gt;rss&lt;/a&gt;&lt;/li&gt;

      &lt;li&gt;&lt;a href="https://twitter.com/enrique_ramirez" rel="me"&gt;twitter&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;&lt;!-- /.social --&gt;
&lt;/section&gt;&lt;!-- /#extras --&gt;

&lt;footer id="contentinfo" class="body"&gt;
  &lt;address id="about" class="vcard body"&gt;
    &lt;span class="primary"&gt;
      &lt;strong&gt;&lt;a href="#" class="fn url"&gt;Smashing Magazine&lt;/a&gt;&lt;/strong&gt;

      &lt;span class="role"&gt;Amazing Magazine&lt;/span&gt;
    &lt;/span&gt;&lt;!-- /.primary --&gt;

    &lt;img src="images/avatar.gif" alt="Smashing Magazine Logo" class="photo" /&gt;
    &lt;span class="bio"&gt;Smashing Magazine is a website and blog that offers resources and advice to web developers and web designers. It was founded by Sven Lennartz and Vitaly Friedman.&lt;/span&gt;

  &lt;/address&gt;&lt;!-- /#about --&gt;
  &lt;p&gt;2005-2009 &lt;a href="https://smashingmagazine.com"&gt;Smashing Magazine&lt;/a&gt;.&lt;/p&gt;
&lt;/footer&gt;&lt;!-- /#contentinfo --&gt;

&lt;/body&gt;
&lt;/html&gt;

</code></pre>

Say, isn't that readable? It's also way more semantic than a bunch of <code>&lt;div&gt;</code>s all over the place.</p>

## 3\. The CSS

Just like our markup, the CSS will also have a very basic start. Call this a frameworks of sorts which I've been using for a long time and works fairly well. Here's the code for our main.css file:

<pre><code class="language-css">
/*
  Name: Smashing HTML5
  Date: July 2009
  description: >-
  Sample layout for HTML5 and CSS3 goodness.
  Version: 1.0
  Author: Enrique Ramírez
  Autor URI: https://enrique-ramirez.com
*/

/* Imports */
@import url("reset.css");
@import url("global-forms.css");

/***** Global *****/
/* Body */
  body {
    background: #F5F4EF url('../images/bg.png');
    color: #000305;
    font-size: 87.5%; /* Base font size: 14px */
    font-family: 'Trebuchet MS', Trebuchet, 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    line-height: 1.429;
    margin: 0;
    padding: 0;
    text-align: left;
  }

/* Headings */
h2 {font-size: 1.571em} /* 22px */
h3 {font-size: 1.429em} /* 20px */
h4 {font-size: 1.286em} /* 18px */
h5 {font-size: 1.143em} /* 16px */
h6 {font-size: 1em} /* 14px */

h2, h3, h4, h5, h6 {
  font-weight: 400;
  line-height: 1.1;
  margin-bottom: .8em;
}

/* Anchors */
a {outline: 0;}
a img {border: 0px; text-decoration: none;}
a:link, a:visited {
  color: #C74350;
  padding: 0 1px;
  text-decoration: underline;
}
a:hover, a:active {
  background-color: #C74350;
  color: #fff;
  text-decoration: none;
  text-shadow: 1px 1px 1px #333;
}

/* Paragraphs */
p {margin-bottom: 1.143em;}
* p:last-child {margin-bottom: 0;}

strong, b {font-weight: bold;}
em, i {font-style: italic;}

::-moz-selection {background: #F6CF74; color: #fff;}
::selection {background: #F6CF74; color: #fff;}

/* Lists */
ul {
  list-style: outside disc;
  margin: 1em 0 1.5em 1.5em;
}

ol {
  list-style: outside decimal;
  margin: 1em 0 1.5em 1.5em;
}

dl {margin: 0 0 1.5em 0;}
dt {font-weight: bold;}
dd {margin-left: 1.5em;}

/* Quotes */
blockquote {font-style: italic;}
cite {}

q {}

/* Tables */
table {margin: .5em auto 1.5em auto; width: 98%;}

  /* Thead */
  thead th {padding: .5em .4em; text-align: left;}
  thead td {}

  /* Tbody */
  tbody td {padding: .5em .4em;}
  tbody th {}

  tbody .alt td {}
  tbody .alt th {}

  /* Tfoot */
  tfoot th {}
  tfoot td {}

</code></pre>

This is our first step into getting the layout together. We can style most of the basic elements from here, so feel free to do so. Here's a few highlights:

*   For optimum coding, a few basic information on the .css file is at the top in comments form.
*   2 imports at the beginning of the file. The first one is [Eric Meyer's CSS reset](https://meyerweb.com/eric/tools/css/reset/) file. Second one is a personalized global forms file which I'll discuss more deeply later on.
*   Very basic styling for the default tags.</p>

### Explaining some properties

For this very part, there's little to be mentioned. Firstly there's the <a href="https://www.w3.org/Style/Examples/007/text-shadow" rel="external"><code>text-shadow</code></a> CSS3 property. To explain it, here's a sample:

<pre><code class="language-css">
  text-shadow: 1px 5px 2px #333;
</code></pre>

This will give us a #333 shadow on our text that's 1px to the right, 5px down and with a 2px blur. Simple, right? You can use hex and rgba values plus any <a title="CSS Units" href="https://htmlhelp.com/reference/css/units.html" rel="external">CSS unit</a> (except %) here.

We also have this little baby:

<pre><code class="language-css">
  * p:last-child {margin-bottom: 0;}
</code></pre>

This line will remove the margin bottom of any <code>&lt;p&gt;</code> tag that's the last child of it's parent. Useful when using boxes (like we're doing) to avoid large vertical gaps.

Lastly, we have a couple of selectors:

<pre><code class="language-css">
  ::-moz-selection {background: #F6CF74; color: #fff;}
  ::selection {background: #F6CF74; color: #fff;}
</code></pre>

<code>::selection</code> is a <a title="CSS3 Selectors" href="https://www.w3.org/TR/2001/CR-css3-selectors-20011113/#selectors" rel="external">CSS3 selector</a> that lets us style how the text selection looks. It only allows <code>color</code> and <code>background</code> CSS properties, so keep it simple. <code>::-moz-selection</code> needs to go here since Mozilla haven't implemented the <code>::selection</code> selector.</p>

### Enabling HTML5 elements

Now, as I've stated before, browsers do not understand HTML5 as of yet. And since HTML5 is still in development, little has been discussed about the default styling the new elements will have. Thus, being tags that do not exist for the browser, it does not display any styling in them.

Perhaps it's fair to assume that most browsers apply something like <code>display: inline</code> for all unknown tags that they might encounter. This is not what we want for some of them, such as <code>&lt;section&gt;</code>, so we need to tell explicitly to the browser how to display these elements:

<pre><code class="language-css">
/* HTML5 tags */
header, section, footer,
aside, nav, article, figure {
  display: block;
}
</code></pre>

There! Now we can magically style our tags as if they were <code>&lt;div&gt;</code>s!

### Limiting our blocks

Some of you might have noticed how I added the <code>class="body"</code> attribute to the major sections of the layout in the markup. This is because we want the body of my website to be for a certain width (800px), and I've never been a fan of the big wrapping <code>&lt;div&gt;</code> to do that. So we'll use the basic block centering technique using margins for this. I'm also adding a couple of generic classes to this section that might be used for a post side content.

<pre><code class="language-css">
/***** Layout *****/
.body {clear: both; margin: 0 auto; width: 800px;}
img.right figure.right {float: right; margin: 0 0 2em 2em;}
img.left, figure.left {float: right; margin: 0 0 2em 2em;}
</code></pre>

### Header styling

We'll begin with our header. This one is fairly easy. We just want a couple of spacing and a few text styling here and there. Nothing we haven't done before.

<pre><code class="language-css">
/*
  Header
*****************/
#banner {
  margin: 0 auto;
  padding: 2.5em 0 0 0;
}

  /* Banner */
  #banner h1 {font-size: 3.571em; line-height: .6;}
  #banner h1 a:link, #banner h1 a:visited {
    color: #000305;
    display: block;
    font-weight: bold;
    margin: 0 0 .6em .2em;
    text-decoration: none;
    width: 427px;
  }
  #banner h1 a:hover, #banner h1 a:active {
    background: none;
    color: #C74350;
    text-shadow: none;
  }

  #banner h1 strong {font-size: 0.36em; font-weight: normal;}
</code></pre>

We now pass on to the navigation. Pretty much the same as before, nothing really new here. The regular horizontal list, a couple of colour edits. Nothing fancy.

<pre><code class="language-css">
  /* Main Nav */
  #banner nav {
    background: #000305;
    font-size: 1.143em;
    height: 40px;
    line-height: 30px;
    margin: 0 auto 2em auto;
    padding: 0;
    text-align: center;
    width: 800px;

    border-radius: 5px;
    -moz-border-radius: 5px;
    -webkit-border-radius: 5px;
  }

  #banner nav ul {list-style: none; margin: 0 auto; width: 800px;}
  #banner nav li {float: left; display: inline; margin: 0;}

  #banner nav a:link, #banner nav a:visited {
    color: #fff;
    display: inline-block;
    height: 30px;
    padding: 5px 1.5em;
    text-decoration: none;
  }
  #banner nav a:hover, #banner nav a:active,
  #banner nav .active a:link, #banner nav .active a:visited {
    background: #C74451;
    color: #fff;
    text-shadow: none !important;
  }

  #banner nav li:first-child a {
    border-top-left-radius: 5px;
    -moz-border-radius-topleft: 5px;
    -webkit-border-top-left-radius: 5px;

    border-bottom-left-radius: 5px;
    -moz-border-radius-bottomleft: 5px;
    -webkit-border-bottom-left-radius: 5px;
  }
</code></pre>

We're using another CSS3 property here: <code>border-radius</code>. This new CSS3 property lets us add rounded borders to our blocks without the need of unnecessary, non-semantic tags that will clutter our code or a million of images and clever background-positioning. No, that's all a thing of the past. With this we just need to set the radius of our border and that's it.

Of course, border-radius is not widely adopted yet, and thus, we need to use the equivalent properties for Mozilla- and Webkit-browsers. There are a lot of <a title="Border-radius: create rounded corners with CSS!" href="https://www.css3.info/preview/rounded-border/" rel="external">variations to this property</a>, and can make your code a little big, but if you want rounded corners on most of the current browsers, you might as well add them.

You might as well notice the use of <a title="!important declaration" href="https://www.w3.org/TR/CSS2/cascade.html#important-rules" rel="external"><code>!important</code></a>. This is basically to override the default styles (<code>text-shadow</code>) without complex specificity selectors. In this example it's here mostly for educational purposes.</p>

### Featured block and Body styling

Here's the CSS code for both blocks. Note that this is not the styling for the posts' list. Just the major content block. As both of these blocks have no real special CSS properties, I'll let you guys figure it out.

<pre><code class="language-css">
/*
  Featured
*****************/
#featured {
  background: #fff;
  margin-bottom: 2em;
  overflow: hidden;
  padding: 20px;
  width: 760px;

  border-radius: 10px;
  -moz-border-radius: 10px;
  -webkit-border-radius: 10px;
}

#featured figure {
  border: 2px solid #eee;
  float: right;
  margin: 0.786em 2em 0 5em;
  width: 248px;
}
#featured figure img {display: block; float: right;}

#featured h2 {color: #C74451; font-size: 1.714em; margin-bottom: 0.333em;}
#featured h3 {font-size: 1.429em; margin-bottom: .5em;}

#featured h3 a:link, #featured h3 a:visited {color: #000305; text-decoration: none;}
#featured h3 a:hover, #featured h3 a:active {color: #fff;}

/*
  Body
*****************/
#content {
  background: #fff;
  margin-bottom: 2em;
  overflow: hidden;
  padding: 20px 20px;
  width: 760px;

  border-radius: 10px;
  -moz-border-radius: 10px;
  -webkit-border-radius: 10px;
}
</code></pre>

Again, this is our everyday coding style. Backgrounds, margins, colours and text styles we've been using for years. Perfect example of how styling HTML5 is not that different from current markup languages. It's just as easy to style as it's always been.</p>

### Extras block styling

Here things begin to get interesting. We'll begin with basic styling for the block itself:

<pre><code class="language-css">
/*
  Extras
*****************/
#extras {margin: 0 auto 3em auto; overflow: hidden;}

#extras ul {list-style: none; margin: 0;}
#extras li {border-bottom: 1px solid #fff;}
#extras h2 {
  color: #C74350;
  font-size: 1.429em;
  margin-bottom: .25em;
  padding: 0 3px;
}

#extras a:link, #extras a:visited {
  color: #444;
  display: block;
  border-bottom: 1px solid #F4E3E3;
  text-decoration: none;
  padding: .3em .25em;
}

  /* Blogroll */
  #extras .blogroll {
    float: left;
    width: 615px;
  }

  #extras .blogroll li {float: left; margin: 0 20px 0 0; width: 185px;}

  /* Social */
  #extras .social {
    float: right;
    width: 175px;
  }
</code></pre>

As you can see, I'm doing a 3 column layout for the blogroll block by floating the <code>&lt;li&gt;</code>s and a 1 column layout for the social block by merely changing its width. This already works very well by itself, but there's one thing that bothers me. The borders I've added for separating each of the links:

![Smashing HTML5! Extras block border issue](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5373ebd-6908-4f07-a06e-7692417c77b1/extras-border.png)

The highlighted row is the one troubling me. The borders I've added are actually on two elements. Each <code>&lt;li&gt;</code> and <code>&lt;a&gt;</code> tag have a border-bottom of 1px, which I don't want on the last row. So we'll remove the borders for the last 3 elements on blogroll, and the last element on social.

First we'll remove the borders on the last <code>&lt;li&gt;</code> of each block. By using the CSS3 <a title=":last-child Pseudo class" href="https://www.w3.org/TR/css3-selectors/#last-child-pseudo" rel="external"><code>:last-child</code></a> selector, we can target the last <code>&lt;li&gt;</code> of it's parent <code>&lt;ul&gt;</code>.

<pre><code class="language-css">
  #extras li:last-child, /* last &lt;li&gt;*/
  #extras li:last-child a /* &lt;a&gt; of last &lt;li&gt; */
  {border: 0}
</code></pre>

That will remove the border from the last link on both of our blocks. Now we have a new problem. How are we going to remove the border on the other two elements on the blogroll block?

![Smashing HTML5! Extras block border second issue](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d87221f-a346-4be6-9fc0-5e8b5474de76/extras-border2.png)

Well, meet <a title=":nth-last-child() Pseudo Selector" href="https://www.w3.org/TR/css3-selectors/#nth-last-child-pseudo" rel="external"><code>:nth-last-child()</code></a>.

<pre><code class="language-css">
#extras .blogroll li:nth-last-child(2),
#extras .blogroll li:nth-last-child(3),
#extras .blogroll li:nth-last-child(2) a,
#extras .blogroll li:nth-last-child(3) a {border: 0;}
</code></pre>

Phew! Looks pretty hard, uh? Not really. This basically targets the second (2) and third (3) elements starting from the end. Exactly the ones I want to remove the border from.

As expected, this will not work on IE, though <a href="https://code.google.com/p/ie7-js/">IE8.js</a> does support <code>:last-child</code>, it does not support <code>:nth-last-child</code>, thus, borders will appear on IE. This is NOT a major design problem, information is still accessible, thus it is pointless to try to achieve the same effect on IE.</p>

### Adding icons to social

Now we'll spice things up a little. We all love how little icons look besides each link. We've seen that design technique everywhere. There's a million ways of applying them, but we'll use some advanced <strong>CSS3 selectors</strong> to do this.

Let's begin with a little introduction. <code>a[n='b']</code> will target all <code>&lt;a&gt;</code> that has an <code>n</code> attribute value of <code>b</code>. So, for example, if we use this: <code>a[href='picture.jpg']</code> we'll be targeting an element like <code>&lt;a href="picture.jpg"&gt;</code>. This is great, but not exactly what we want, since the follow-ups of the URL might have a different value. Here's a couple of other selectors that might come in handy:

*   `a[n]` will target all `<a>` that has an `n` attribute, regardless of its value.
*   `a[n='b']` will target all `<a>` that has an `n` attribute value of `b`.
*   `a[n~='b']` will target all `<a>` that has an `n` attribute which one of its space-separated values is `b`.
*   `a[n^='b']` will target all `<a>` that has an `n` attribute that starts with `b`.
*   `a[n*='b']` will target all `<a>` that has an `n` attribute that has `b` somewhere within its value.

Note that neither of these is restricted to the <code>&lt;a&gt;</code> tag. This last one fits us perfectly. So we'll search for an <code>&lt;a&gt;</code> tag that has a piece of text somewhere within its URL. So this is our code:

<pre><code class="language-css">
#extras div[class='social'] a {
  background-repeat: no-repeat;
  background-position: 3px 6px;
  padding-left: 25px;
}

/* Icons */
.social a[href*='delicious.com'] {background-image: url('../images/icons/delicious.png');}
.social a[href*='digg.com'] {background-image: url('../images/icons/digg.png');}
.social a[href*='facebook.com'] {background-image: url('../images/icons/facebook.png');}
.social a[href*='last.fm'], .social a[href*='lastfm'] {background-image: url('../images/icons/lastfm.png');}
.social a[href*='/feed/'] {background-image: url('../images/icons/rss.png');}
.social a[href*='twitter.com'] {background-image: url('../images/icons/twitter.png');}
</code></pre>

The first bit lets us add a padding to the social links, where the icon will be. It'll also set the default background settings so we don't have to repeat ourselves. You might be wondering why I'm using <code>div[class='social']</code> rather than the normal <code>div.social</code>. Simply because, for the browsers that don't support this kind of selectors (*cough* IE *Cough*), we don't want a white gap on the left of our links. Thus, using the same selector used for the background icons will keep me safe. IE won't have a padding nor a background image, while the rest will do.

The second section uses the selector explained above to target each social network and add the proper icon.

This CSS technique <a title="Showing Hyperlink Cues with CSS (Ask the CSS Guy)" href="https://www.askthecssguy.com/2006/12/showing_hyperlink_cues_with_cs_1.html" rel="external">is nothing new</a>, and as powerful as it might be, it is not widely used (I've even seen JavaScript used to achieve this same thing). Yet another CSS feature that goes unnoticed and shouldn't be.</p>

### Footer Styling

Lastly, we have our footer. As other examples above, this has just basic styling here and there. Besides the <code>border-radius</code> property, there's nothing new in here.

<pre><code class="language-css">
/*
  About
*****************/
#about {
  background: #fff;
  font-style: normal;
  margin-bottom: 2em;
  overflow: hidden;
  padding: 20px;
  text-align: left;
  width: 760px;

  border-radius: 10px;
  -moz-border-radius: 10px;
  -webkit-border-radius: 10px;
}

#about .primary {float: left; width: 165px;}
#about .primary strong {color: #C64350; display: block; font-size: 1.286em;}
#about .photo {float: left; margin: 5px 20px;}

#about .url:link, #about .url:visited {text-decoration: none;}

#about .bio {float: right; width: 500px;}

/*
  Footer
*****************/
#contentinfo {padding-bottom: 2em; text-align: right;}
</code></pre>

### The Posts List

There's only one last element to style. Once again, basic styling here, but this time, we'll add a quick effect for when the user hovers over the post.

<pre><code class="language-css">

/* Blog */
.hentry {
  border-bottom: 1px solid #eee;
  padding: 1.5em 0;
}
li:last-child .hentry, #content &gt; .hentry {border: 0; margin: 0;}
#content &gt; .hentry {padding: 1em 0;}

.entry-title {font-size: 1.429em; margin-bottom: 0;}
.entry-title a:link, .entry-title a:visited {text-decoration: none;}

.hentry .post-info * {font-style: normal;}

  /* Content */
  .hentry footer {margin-bottom: 2em;}
  .hentry footer address {display: inline;}
  #posts-list footer address {display: block;}

  /* Blog Index */
  #posts-list {list-style: none; margin: 0;}
  #posts-list .hentry {padding-left: 200px; position: relative;}
  #posts-list footer {
    left: 10px;
    position: absolute;
    top: 1.5em;
    width: 190px;
  }
</code></pre>

Some basics. I'm removing all margin and padding for the last post entry (so I don't end up with a big gap at the bottom of my box). I'm also using the <code>&gt;</code> selector which basically targets a direct child. For example, <code>#content &gt; .hentry</code> will target a <code>.hentry</code> element that's directly inside the <code>#content</code>. If the <code>.hentry</code> is inside, let's say, an ordered list, this rule will not apply since it's a grandchild and not a direct child of <code>#content</code>. This is to target the single post view once we get onto that.

Continuing with our code, we'll get this:

<pre><code class="language-css">
#posts-list .hentry:hover {
  background: #C64350;
  color: #fff;
}
#posts-list .hentry:hover a:link, #posts-list .hentry:hover a:visited {
  color: #F6CF74;
  text-shadow: 1px 1px 1px #333;
}
</code></pre>

This code will change the <code>&lt;li&gt;</code> background color, text color and its <code>&lt;a&gt;</code> color when the mouse is directly above the <code>&lt;li&gt;</code>. This is nothing new and has been possible since forever, but we're adding it for a simple reason.

HTML5 lets users <a title="HTML5 block level links" href="https://html5doctor.com/block-level-links-in-html-5/" rel="external">wrap block-level elements with <code>&lt;a&gt;</code> tags to create block linking areas</a>. Basically, we'll be able to wrap the entire <code>&lt;hentry&gt;</code> contents with an anchor and have it behave as a proper link. However, after some testing, I've figured that <strong>Firefox 3.5.1</strong> is not ready for this. Perhaps because of the non-understandable new elements inside of each <code>.hentry</code>, everytime I added an anchor to wrap the contents, everything inside started to behave in weird manners. Safari, Opera and even IE6 work properly. Take a look at the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbb7db12-ac90-4aba-b311-27dffae0463b/block-level-links.html">test page</a>. Below are a couple of screenshots for all of you single-browser users.

Opera 9.64:

[![Opera block level anchors render](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4e71550-3c4b-431f-acdf-bc4dbad75186/opera-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dee81da9-a484-4582-8ead-58492c940bec/opera-big.png)

Safari 4.0.2:

[![Safari block level anchors render](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06d29bcb-8f1e-4346-a008-3d998a7c5543/safari-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4876437d-59f4-4ebc-937f-76397a3b64e5/safari-big.png)

Internet Explorer 6:

[![IE6 block level anchors render](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23b4450f-ac14-497c-9bd8-c95eecbbeb6c/ie-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4928dc54-9fa9-4efe-8d20-87bf6ef5b6d5/ie-big.png)

Firefox 3.5.1:

[![Firefox block level anchors render](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93cdc06e-e09c-490c-bc2d-431d25b945c5/firefox-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0fc6750-4776-4b34-9802-f3efe35fedc6/firefox-big.png)

So block level anchors are really broken on Firefox, yet we can add a nice :hover effect to the <code>&lt;li&gt;</code>. So we can enhance our user experience visually, though not from the accessibility point of view.</p>

### Fixing IE6

Finally, we need to do some fixing for IE6. Below is the complete ie.css and ie6.css file. Each line has a comment on its right side or on the top explaining what it's fixing. Pretty straightforward. This is ie.css:

<pre><code class="language-css">
#banner h1 {line-height: 1;} /* Fixes Logo overlapping */
</code></pre>

And this is ie6.css file:

<pre><code class="language-css">
#featured figure {display: inline;} /* Double margin fix */
#posts-list footer {left: -190px;} /* Positioning fix */

/* Smaller width for Social block
so it won't jump to next line */
#extras .social {width: 165px;}
</code></pre>

## 4\. The aftermath

So, how does everything look now? It has been tested on IE6, Firefox 3, Firefox 3.5, Opera 9.64 and Safari 4.0.2. They all behave properly. Below are a series of screenshots of every browser.

[![Final Version Safari Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ba9b0c7-9ec1-4f7e-abfa-e4354840be65/final-safari-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7b2e6bc-4c87-4ea1-a155-cc1d621ffda2/final-safari.png "Final Version Safari Screenshot") [![Final Version Firefox Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b43134d-62e3-49f9-98f9-6f3c569f2794/final-firefox-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e1c102a-086f-4258-b661-0f3b4a7ab966/final-firefox.png "Final Version Firefox Screenshot") [![Final Version Opera Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48a29f49-4939-458c-8241-5296c479f016/final-opera-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96188833-8dac-4983-b1d0-99c26f2ec3fd/final-opera.png "Final Version Opera Screenshot") [![Final Version Internet Explorer 6 Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c262393-a09d-461c-a24e-39e38dbca60a/final-ie6-thumb.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d199275-970f-4196-8593-6cdddfea92c6/final-ie6.png "Final Version Internet Explorer 6 Screenshot")

It is now safe to say that you can achieve an HTML 5 Layout with CSS3 today that will work on past, current and future browsers without a problem. We are still far away from the time we can fully implement much of HTML5 video player code, but we can begin using it today.

## Further Resources

There's a lot of hype and websites dedicated right now to the HTML5 wonder. Here's a couple:

*   [HTML5 Doctor](https://html5doctor.com/) Tips and tutorials that will help you implement HTML 5 today
*   [HTML5 Editor's Draft](https://dev.w3.org/html5/spec/Overview.html) Current Draft with everything you'll ever need to know about HTML5
*   [HTML5 Gallery](https://html5gallery.com/) In the wild examples of HTML5 implementations
*   [The power of HTML 5 and CSS 3](https://perishablepress.com/press/2009/07/19/power-of-html5-css3/) Great article about some of the major HTML 5 and CSS 3 features
*   [HTML 5 and the Future of the Web](https://www.smashingmagazine.com/2009/07/16/html5-and-the-future-of-the-web/) This articles gives you some tips and insights into HTML5 to help ease the inevitable pain that comes with transitioning to a slightly different syntax.
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/) In this article, we’ll look at the advantages of CSS3 and some examples of how Web designers are already using it. By the end, we’ll know a bit of what to expect from CSS3 and how we can use its new features in our projects.

