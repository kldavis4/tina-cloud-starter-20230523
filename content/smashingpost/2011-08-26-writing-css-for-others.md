---
title: 'How To Write CSS For Others'
slug: writing-css-for-others
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc53661a-24f6-40a2-a647-76b7ae2cf505/cfo-01-700.png
date: 2011-08-26T09:57:40.000Z
author: harry-roberts
summary: >-
   When it comes to writing CSS, everyone has their own favorite format, their own preference between single-line and multi-line, their own ideas on organization, and so on. How can we write CSS so that others can understand and use with ease?
description: >-
   When it comes to writing CSS, everyone has their own favorite format. In this article, Harry Roberts explores how we can write CSS so that others can understand and use it with ease.
categories:
  - Coding
  - CSS
  - Maintenance
---

I think a lot of us CSS authors are doing it wrong. We are selfish by nature; we get into our little bubbles, writing CSS (as amazing as it may be) with only ourselves in mind. How many times have you inherited a CSS file that’s made you say “WTF” at least a dozen times.

HTML has a standard format and syntax that everyone understands. For years, programmers have widely agreed on standards for their respective languages. CSS doesn’t seem to be there yet: everyone has their own favorite format, their own preference between single-line and multi-line, their own ideas on organization, and so on.

{{% feature-panel %}}

## A New Way of Thinking

Recently, I have begun to think that CSS authors could take a leaf from the programmers’ book. We need to write CSS that others can understand and use with ease. Programmers have been writing sharable code since day one, and it’s high time that CSS be written with as much organization and openness.

In writing <a href="https://inuitcss.com">inuit.css</a> and working on a huge front-end framework at my job at sky.com, it has become more apparent to me that writing code that can be easily picked up by others is extremely important. I wouldn’t say that I’ve nailed everything yet, but I’ll share with you some things that I think are vital when writing code, specifically CSS, that will be used by others.

First, the reasoning: my number one tip for developers is to **always code like you’re working in a team, even when you’re not**. You may be the only developer on your project right now, but it might not stay that way:

*   Your project could be taken to another developer, agency or team. Even though this is not the best situation to find yourself in, handing over your work smoothly and professionally to others is ideal.
*   If you’re doing enough work to warrant employing someone else or expanding the team at all, then your code ceases to be yours and becomes the team’s.
*   You could leave the company, take a vacation or be off sick, at which point someone else will inherit your code, even if only temporarily.
*   Someone will inevitably poke through your source code, and if they’ve never met you, this could be the only basis on which they judge your work. First impressions count!

## Comments Are King!

One thing I’ve learned from building a massive front-end framework at work and from producing inuit.css is that comments are vital. Comments, comments, comments. Write one line of code, then write *about* it. <ins datetime="2011-08-29T09:56:25+00:00">**N.B. This is not meant to mean write about *every* line of code, as that would be overkill. Only comment where it helps/is useful.**</ins>

It might seem like overkill at first, but write about everything you do. The code might look simple to you, but there’s bound to be someone out there who has no idea what it does. Write it down. I had already gotten into this habit when I realized that this was the same technique that a good friend and incredibly talented developer, <a title="Nick Payne on Twitter" href="https://twitter.com/makeusabrew">Nick Payne</a>, told me about. That technique is called “<a title="Wikipedia entry for Rubber Duck Debugging" href="https://en.wikipedia.org/wiki/Rubber_duck_debugging">rubber-duck debugging</a>”:
<blockquote>… an unnamed expert programmer would keep a rubber duck by his desk at all times, and debug his code by forcing himself to explain it, line by line, to the duck.</blockquote>

Write comments like you’re talking to a rubber duck!

Good comments take care of 99% of what you hand over and &mdash; more importantly &mdash; take care of your documentation. Your code should *be* the documentation.

Comments are also an excellent way to show off. Ever wanted to tell someone how awesome a bit of your code is but never found the chance? This is that chance! Explain how clever it is, and just wait for people to read it.

Egos aside, though, comments do force you to write nicer code. I’ve found that writing extensive comments has made me a better developer. I write cleaner code, because writing comments reminds me that I’m intending for others to read the code.

## Multi-Line CSS

This issue really divides developers: single-line versus multi-line CSS. I’ve always written multi-line CSS. I love it and despise single-line notation. But others think the opposite &mdash; and they’re no more right or wrong than I am. Taste is taste, and consistency is what matters.

Having said that, when working on a team, I firmly believe that multi-line CSS is the way to go. Multi-line ensures that each CSS declaration is accounted for. One line represents one piece of functionality (and can often be attributed to one person).

As a result, each line will show up individually on a diff between two versions. If you change, say, only one hex value in a <code>color</code> declaration, then that is all that needs to be flagged. A diff on a single-line document would flag an entire rule set as having been changed, even when it hasn’t.

Take the following example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/209fca1d-2ed9-453e-aa98-c9301f7c0787/cfo-011.png"><img style="width: 100%" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc53661a-24f6-40a2-a647-76b7ae2cf505/cfo-01-700.png" alt="screenshot" /></a></figure>

Above, we just changed a <code>color</code> value in a rule set, but because it was a single-line CSS file, the entire rule set appears to have changed. This is very misleading, and also not very readable or obvious. At first glance, it appears that a whole rule set has been altered. But look closely and you’ll see that only <code>#333</code> has been changed to <code>#666</code>. We can make this distinction far more obvious by using multi-line CSS, like so:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f94feade-be3d-4425-a8cb-7040b69453a5/cfo-02.png"><img style="width: 100%" title="Git diff on multi-line CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f94feade-be3d-4425-a8cb-7040b69453a5/cfo-02.png" alt="screenshot" /></a></figure>

Having said all this, I am by no means a version-control expert. I’ve only just started using GitHub for inuit.css, so I’m very new to it all. Instead, I’ll leave you with Jason Cale’s excellent article on the subject.

Furthermore, single-line CSS makes commenting harder. Either you end up with one comment per rule set (which means your comments might be less specific than had they been done per line), or you get a messy single line of comment, then code, then comment again, as shown here:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13ec21bd-70b9-4138-897f-3184a7d829ab/cfo-03.png"><img style="width: 100%" title="Screenshot of single-line commented CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13ec21bd-70b9-4138-897f-3184a7d829ab/cfo-03.png" alt="screenshot" width="1331" /></a></figure>

With multi-line CSS, you have a much neater comment structure:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72817ce-6d1c-4b0c-a566-a997e207613c/cfo-04.png"><img style="width: 100%" title="Screenshot of multi-line commented CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72817ce-6d1c-4b0c-a566-a997e207613c/cfo-04.png" alt="screenshot" /></a></figure>

## Ordering CSS Properties

Likewise, the order in which people write their CSS properties is very personal.

Many people opt for alphabetized CSS, but this is counter-intuitive. <a href="https://github.com/csswizardry/inuit.css/pull/1#issuecomment-1066990">I commented briefly on the subject on GitHub</a>; my reasoning is that ordering something by a meaningless metric makes no sense; the initial letter of a declaration has no bearing on the declaration itself. Ordering CSS alphabetically makes as much sense as ordering CDs by how bright their covers are.

A more sensible approach is to order by type and relevance. That is, group your color declarations together, your box-model declarations together, your font declarations together and so on. Moreover, order each grouping according to its relevance to the selector. If you are styling an <code>h1</code>, then put font-related declarations first, followed by the others. For example:

<pre><code class="language-markup tmp-html">#header {
   /* Box model */
   width: 100%;
   padding: 20px 0;
   /* Color */
   color: #fff;
   background: #333;
}

h1 {
   /* Font */
   font-size: 2em;
   font-weight: bold;
   /* Color */
   color: #c00;
   background: #fff;
   /* Box model */
   padding: 10px;
   margin-bottom: 1em;
}</code></pre>

<ins datetime="2011-08-29T09:56:25+00:00">**Please note that the comments above are not intended to go into your CSS file, but are just to illustrate my point in the article.**</ins>

## Ordering CSS Files

Ordering CSS files is always tricky, and there is no right or wrong way. A good idea, though, is to section the code into defined groups, with headings, as well as a table of contents at the top of the file. Something like this:

<pre><code class="language-markup tmp-html">/*------------------------------------*
   CONTENTS
*------------------------------------*/
/*
MAIN
TYPE
IMAGES
TABLES
MISC
RESPONSIVE
*/

/*------------------------------------*
   $MAIN
*------------------------------------*/
html {
   styles
}

body {
   styles
}

/*------------------------------------*
   $TYPE
*------------------------------------*/</code></pre>

And so on.

This way, you can easily read the contents and jump straight to a particular section by performing a quick search (Command/Control + F). Prepending each heading with a dollar sign makes it unique, so that a search will yield only headings.

{{% ad-panel-leaderboard %}}

### The “Shared” Section

All CSS files should have a section for sharing, where you tether selectors to a single declaration, rather than write the same declaration over and over.

So, instead of writing this…

<pre><code class="language-markup tmp-html">/*------------------------------------*
   $TYPE
*------------------------------------*/
h1 {
   font-size: 2em;
   color: #c00;
}

h2 {
   font-size: 1.5em;
   color: #c00;
}

a {
   color: #c00;
   font-weight: bold;
}

#tagline {
   font-style: italic;
   color: #c00;
}</code></pre>

… you would write this:

<pre><code class="language-markup tmp-html">/*------------------------------------*
   $TYPE
*------------------------------------*/
h1 {
   font-size: 2em;
}
h2 {
   font-size: 1.5em;
}
a {
   font-weight: bold;
}
#tagline {
   font-style: italic;
}

/*------------------------------------*
   $SHARED
*------------------------------------*/
h1, h2, a, #tagline {
   color:#c00;
}</code></pre>

This way, if the brand color of <code>#c00</code> ever changes, a developer would only ever need to change that value once. This is essentially using variables in CSS.

### Multiple CSS Files For Sections, Or One Big File With All Sections?

A lot of people separate their sections into multiple files, and then use the <code>@import</code> rule to put them all back together in one meta file. For example:

<pre><code class="language-markup tmp-html">@import url(main.css)
@import url(type.css)
@import url(images.css)
@import url(tables.css)
@import url(misc.css)
@import url(responsive.css)</code></pre>

This is fine, and it does keep everything in sections, but it does lead to a lot more HTTP requests than is necessary; and minimizing requests is one of the most important rules for a high-performance website.

Compare this…

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/611c3170-dedc-4ac3-aeaa-0412206118c0/firebug-1.jpg"><img style="width: 100%" title="Lots of CSS files" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/611c3170-dedc-4ac3-aeaa-0412206118c0/firebug-1.jpg" alt="screenshot" /></a></figure>

… to this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5975871-e68a-4843-b805-0e9f3c3abe44/firebug-2.jpg"><img style="width: 100%" title="One CSS file" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5975871-e68a-4843-b805-0e9f3c3abe44/firebug-2.jpg" alt="screenshot" /></a></figure>

If you section and comment your CSS well enough, using a table of contents and so forth, then you avoid the need to split up your CSS files, thus keeping those requests down.

If you really want to break up your CSS into multiple style sheets, you can do that &mdash; just combine them into one at build time. This way, your developers can work across multiple files, but your users will download one concatenated file.

## Learning From Programmers

Programmers have been doing this for ages, and doing it well. Their job is to write code that is as readable as it is functional. We front-end developers could learn a lot from how programmers deal with code.

The code of my good friend (and absolutely awesome chap) <a href="https://twitter.com/dan_bentley">Dan Bentley</a> really struck a chord with me. It’s beautiful. I don’t understand what it does most of the time, but it’s so clean and lovely to look at. So much white space, so neat and tidy, all commented and properly looked after. His PHP, Ruby, Python or whatever-he-decides-to-use-that-day always looks so nice. It made me want to write my CSS the same way.

White space is your friend. You can remove it before you go live if you like, but the gains in cleanliness and readability are worth the few extra bytes (which you could always cut back down on by Gzip’ing your files anyway).

Make the code readable and maintainable first and foremost, then worry about file size later. Happy developers are worth more than a few kilobytes in saved weight.

## Code Should Take Care Of Itself

So far, we’ve talked about people maintaining your code, but what about actually using it?

You can do a number of things to make the life of whoever inherits your code much easier &mdash; and to make you look like a saint. I can’t think of many generic examples, but I have a few specific ones, mainly from inuit.css.

### Internationalize Your Selectors

Inuit.css has a class named <code>.centered</code>, which is spelt in US English. CSS is written in US English anyway, so we’re used to this; but as an English developer, I always end up typing UK English at least once in a project. Here is the way I have accounted for this:

<pre><code class="language-markup tmp-html">.centred, .centered {
   [style]
}</code></pre>

Both classes do the same thing, but the next developer doesn’t have to remember to be American!

If your selectors include words that have US and UK spelling variants, include both.

### Let The Code Do The Heavy Lifting

Also in inuit.css, I devised a method to not need <code>class="end"</code> for the last column in a row of grids. Most frameworks require this class, or something similar, to omit the <code>margin-right</code> on the last item in a list and thus prevent the grid system from breaking.

Remembering to add this class isn’t a big deal, but it’s still one more thing to remember. So, <a href="https://csswizardry.com/2011/08/building-better-grid-systems/">I worked out a way to remove it</a>.

In another major inuit.css update, I removed a <code>.grid</code> class that used to be required for every single grid element. This was a purely functional class that developers had to add to any <code>&lt;div&gt;</code> that they wanted to behave like a grid column. For example:

<pre><code class="language-markup tmp-html">&lt;div class="grid grid-4"&gt;
    …
&lt;/div&gt;</code></pre>

This <code>.grid</code> class, in conjunction with the <code>.grid-4</code> class, basically says, “I want this <code>&lt;div&gt;</code> to be a grid item and to span four columns.” This isn’t a huge burden on developers, but again, it’s one more thing that could be removed to make their lives easier.

The solution was to use a regex CSS attribute selector: <code>[class^="grid-"]{}</code>. This says, “Select any element whose class begins with <code>.grid-</code>,” and it allows the developer’s mark-up to now read as follows:

<pre><code class="language-markup tmp-html">&lt;div class="grid-4"&gt;
    …
&lt;/div&gt;</code></pre>

CSS attribute selectors may be less efficient than, say, classes, but not to the point that you’d ever notice it (unless you were working on a website with massive traffic, like Google). The benefits of making the mark-up leaner and the developer’s life easier far outweigh the performance costs.

Do the hard work once and reap the benefits later. Plus, get brownie points from whoever picks up your project from you.

### Be Pre-emptive, Think About Edge Cases

An example of being pre-emptive in inuit.css is the grid system. The grids are meant to be used in a series of sibling columns that are all contained in one parent, with a class of <code>.grids</code>. This is their intended use. But what if someone wants a standalone grid? That’s not their intended use, but <a title="Example on GitHub" href="https://github.com/csswizardry/inuit.css/blob/v2.0/css/inuit.css#L114">let’s account for it should it happen</a>.

**Note:** inuit.css has changed since this was written, but the following is true as of <a href="https://github.com/csswizardry/inuit.css/blob/v1.5/css/inuit.css#L212">version 2.5</a>.

Another and perhaps better example is the 12-column grid system in inuit.css. By default, the framework uses a 16-column grid, with classes <code>.grid-1</code> through <code>.grid-16</code> for each size of column.

A problem arises, though, when you attempt to switch from the 16-column system to the 12-column system. The <code>.grid-15</code> class, for example, doesn’t exist in a 12-column layout; and even if it did, it would be too big.

What I did here was to make <code>.grid-13</code> through <code>.grid-16</code> use the exact same properties as <code>.grid-12</code>. So, if you switch from a 16-column layout to a 12-column one, your <code>.grid-13</code> through <code>.grid-16</code> would’t break it &mdash; they would all just become <code>.grid-12</code>s.

This means that developers can switch between them, and inuit.css will take care of everything else.

Pre-empt the developer’s next problem, and solve it for them.

## Addendum

A few people have mentioned that some of these practices lead to a bloated CSS file. Bloat is where *unnecessary* code makes its way into a file, and your comments should be anything but unnecessary. It *will* lead to a larger CSS file, but not a bloated one.

If you are worried about increased file size then you should <a href="https://developer.yahoo.com/yui/compressor/">minify</a> and gzip your stylesheets, but this is best practice (particularly for highly trafficked websites) anyway.

## That’s It

There you have it: a few humble suggestions on how CSS authors can write code that is perfect for other developers to inherit, understand, maintain, extend and enjoy.

If you have any other tips, do please add them in the comments.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [12 Principles For Keeping Your Code Clean](https://www.smashingmagazine.com/2008/11/12-principles-for-keeping-your-code-clean/)
*   [Zen Coding: A Speedy Way To Write HTML/CSS Code](https://www.smashingmagazine.com/2009/11/zen-coding-a-new-way-to-write-html-code/)
*   [Using the LESS CSS Preprocessor for Smarter Style Sheets](https://www.smashingmagazine.com/2010/12/using-the-less-css-preprocessor-for-smarter-style-sheets/)

{{< signature "al, mrn" >}}
