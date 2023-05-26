---
title: 'HTML5 And The Document Outlining Algorithm'
slug: html5-and-the-document-outlining-algorithm
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85e4ddf3-af32-44a8-be7f-48bf94c4e8d3/html5-logo-512.png
date: 2011-08-16T08:29:44.000Z
author: derek-johnson
summary: >-
  One important part of HTML5 that is still not widely understood is sectioning content, and to understand that, we need to grasp the document outlining algorithm. And that can be a challenge... but the rewards are well worth it.
description: >-
  The logic behind the document outlining algorithm can be hard to grasp. In this article Derek Johnson explains how can we understand it.
categories:
  - Coding
  - HTML5
  - HTML
---

By now, we all know that <a href="https://www.smashingmagazine.com/2010/12/10/why-we-should-start-using-css3-and-html5-today/">we should be using HTML5</a> to build websites. The discussion now is moving on to how to use HTML5 correctly. One important part of HTML5 that is still not widely understood is sectioning content: <code>section</code>, <code>article</code>, <code>aside</code> and <code>nav</code>. To understand sectioning content, we need to grasp the document outlining algorithm.

<a href="https://www.smashingmagazine.com/2011/08/16/html5-and-the-document-outlining-algorithm/"><img loading="lazy" decoding="async" title="HTML5 And The Document Outlining Algorithm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85e4ddf3-af32-44a8-be7f-48bf94c4e8d3/html5-logo-512.png" alt="Screenshot" width="450" height="450" /></a>

Understanding the document outlining algorithm can be a challenge, but the rewards are well worth it. No longer will you agonize over whether to use a <code>section</code> or <code>div</code> element &mdash; you will know straight away. Moreover, you will know *why* these elements are used, and this knowledge of semantics is the biggest benefit of learning how the algorithm works.

{{% feature-panel %}}

## What Is The Document Outlining Algorithm?

The document outlining algorithm is a mechanism for producing outline summaries of Web pages based on how they are marked up. Every Web page has an outline, and checking it is easy using a really simple free online tool, which we’ll cover shortly.

So, let’s start with a sample outline. Imagine you have built a website for a horse breeder, and he wants a page to advertise horses that he is selling. The structure of the page might look something like this:

<figure><br>
 	1. Horses for sale
 	    1. Mares
         1. Pink Diva
         2. Ring a Rosies
 	      3. Chelsea’s Fancy
       2. Stallions
         1. Korah’s Fury
 	      2. Sea Pioneer
 	      3. Brown Biscuit

<figcaption>Figure 1: How a page about horses for sale might be structured.</figcaption></figure>

That’s all it is: a nice, clean, easy-to-follow list of headings, displayed in a hierarchy &mdash; much like a table of contents.

To make things even simpler, only two things in your mark-up affect the outline of a Web page:

*   [heading content](https://developers.whatwg.org/content-models.html#heading-content-0) (`h1` to `h6` and `hgroup`),
*   [sectioning content](https://developers.whatwg.org/content-models.html#sectioning-content-0) (`section`, `article`, `aside` and `nav`).

Obviously, the sectioning of content is the new HTML5 way to create outlines. But before we get into that, let’s go back to HTML 101 and review how we should all be using headings.

## Creating Outlines With Heading Content

To create a structure for the horses page outlined in figure 1, we could use mark-up like the following:

<figure>

<pre><code class="language-markup tmp-html">&lt;div&gt;				
   &lt;h1&gt;Horses for sale&lt;/h1&gt;

   &lt;h2&gt;Mares&lt;/h2&gt;

   &lt;h3&gt;Pink Diva&lt;/h3&gt;
   &lt;p&gt;Pink Diva has given birth to three Grand National winners.&lt;/p&gt;

   &lt;h3&gt;Ring a Rosies&lt;/h3&gt;
   &lt;p&gt;Ring a Rosies has won the Derby three times.&lt;/p&gt;

   &lt;h3&gt;Chelsea’s Fancy&lt;/h3&gt;
   &lt;p&gt;Chelsea’s Fancy has given birth to three Gold Cup winners.&lt;/p&gt;

   &lt;h2&gt;Stallions&lt;/h2&gt;

   &lt;h3&gt;Korah’s Fury&lt;/h3&gt;
   &lt;p&gt;Korah’s Fury has fathered three champion race horses.&lt;/p&gt;

   &lt;h3&gt;Sea Pioneer&lt;/h3&gt;
   &lt;p&gt;Sea Pioneer has won The Oaks three times.&lt;/p&gt;

   &lt;h3&gt;Brown Biscuit&lt;/h3&gt;
   &lt;p&gt;Brown Biscuit has fathered nothing of any note.&lt;/p&gt;

   &lt;p&gt;All our horses come with full paperwork and a family tree.&lt;/p&gt;
&lt;/div&gt;</code></pre>

<figcaption>Figure 2: Our “Horses for sale” page, marked up using headings.</figcaption></figure>

It’s as simple as that. The outline in figure 1 is created by the levels of the headings.

Just so you know that I’m not making this up, you should copy and paste the code above into Geoffrey Sneddon’s <a href="https://gsnedders.html5.org/outliner/">excellent outlining tool</a>. Click the big “Outline this” button, et voila!

An outline created with heading content this way is said to consist of implicit, or implied, sections. Each heading creates its own implicit section, and any subsequent heading of a lower level starts another layer, of implicit sub-section, within it.

An implicit section is ended by a heading of the same level or higher. In our example, the “Mares” section is ended by the beginning of the “Stallions” section, and each section that contains details of an individual horse is ended by the beginning of the next one.

Figure 3 below is an example of an implicit section that ends with a heading of the same level. And figure 4 is an implicit section that ends with a heading of a higher level.

<figure>

<pre><code class="language-markup tmp-html">&lt;h3&gt;Sea Pioneer&lt;/h3&gt;&lt;!-- start of implicit section --&gt;
&lt;p&gt;Sea Pioneer has won The Oaks three times.&lt;/p&gt;

&lt;h3&gt;Brown Biscuit&lt;/h3&gt;&lt;!-- This heading starts a new implicit section,
so the previous Sea Pioneer section is closed --&gt;</code></pre>

<figcaption>Figure 3: An implicit section being closed by a heading of the same level</figcaption></figure>

<figure>

<pre><code class="language-markup tmp-html">&lt;h3&gt;Chelsea’s Fancy&lt;/h3&gt;&lt;!-- start of implicit section --&gt;
&lt;p&gt;Chelsea’s Fancy has given birth to 3 Gold Cup winners.&lt;/p&gt;

&lt;h2&gt;Stallions&lt;/h2&gt;&lt;!-- this heading starts a new implicit section
using a higher level heading, so Chelsea’s Fancy is now closed --&gt;</code></pre>

<figcaption>Figure 4: An implicit section being closed by a heading of a higher level.</figcaption></figure>

## Creating Outlines With Sectioning Content

Now that we know how heading content works in creating an outline, let’s mark up our horses page using some new HTML5 structural elements:

<figure>

<pre><code class="language-markup tmp-html">&lt;div&gt;
   &lt;h6&gt;Horses for sale&lt;/h6&gt;

   &lt;section&gt;
      &lt;h1&gt;Mares&lt;/h1&gt;

      &lt;article&gt;
         &lt;h1&gt;Pink Diva&lt;/h1&gt;
         &lt;p&gt;Pink Diva has given birth to three Grand National winners.&lt;/p&gt;
      &lt;/article&gt;

      &lt;article&gt;
         &lt;h5&gt;Ring a Rosies&lt;/h5&gt;
         &lt;p&gt;Ring a Rosies has won the Derby three times.&lt;/p&gt;
      &lt;/article&gt;

      &lt;article&gt;
         &lt;h2&gt;Chelsea’s Fancy&lt;/h2&gt;
         &lt;p&gt;Chelsea’s Fancy has given birth to three Gold Cup winners.&lt;/p&gt;
      &lt;/article&gt;
   &lt;/section&gt;

   &lt;section&gt;
      &lt;h6&gt;Stallions&lt;/h6&gt;

      &lt;article&gt;
         &lt;h3&gt;Korah’s Fury&lt;/h3&gt;
         &lt;p&gt;Korah’s Fury has fathered three champion race horses.&lt;/p&gt;
      &lt;/article&gt;

      &lt;article&gt;
         &lt;h3&gt;Sea Pioneer&lt;/h3&gt;
         &lt;p&gt;Sea Pioneer has won The Oaks three times.&lt;/p&gt;
      &lt;/article&gt;

      &lt;article&gt;
         &lt;h1&gt;Brown Biscuit&lt;/h1&gt;
         &lt;p&gt;Brown Biscuit has fathered nothing of any note.&lt;/p&gt;
      &lt;/article&gt;			
   &lt;/section&gt;

   &lt;p&gt;All our horses come with full paperwork and a family tree.&lt;/p&gt;
&lt;/div&gt;</code></pre>

<figcaption>Figure 5: The horses page, marked up with some new HTML5 structural elements.</figcaption></figure>

Now, I know what you’re thinking, but I haven’t taken leave of my senses with these crazy headings. I am making a very important point, which is that **the outline is created by the sectioning content, not the headings**.

Go ahead and copy and paste that code into the <a href="https://gsnedders.html5.org/outliner/">outliner</a>, and you will see that the heading levels have absolutely no effect on the outline where sectioning content is used.

The <code>section</code>, <code>article</code>, <code>aside</code> and <code>nav</code> elements are what create the outline, and this time the sections are called explicit sections.

One of the most talked about features of HTML5 is that multiple <code>h1</code> elements are allowed, and this is why. It’s not an open invitation to mark up every heading on the page as <code>h1</code>; rather, it’s an acknowledgement that where sectioning content is used, *it* creates the outline, and that each explicit section has its own heading structure.

The <a href="https://developers.whatwg.org/sections.html#headings-and-sections">part of the HTML5 spec</a> that deals with headings and sections makes this clear:
<blockquote>“Sections may contain headings of any rank, but authors are strongly encouraged to either use only <code>h1</code> elements, or to use elements of the appropriate rank for the section’s nesting level.”</blockquote>

I would strongly advise that until browsers &mdash; and, more critically, screen readers &mdash; understand that sectioning content introduces a sub-section, using multiple <code>h1</code> elements is less safe than using a heading structure that reflects the level of each heading in the document, as shown in figure 6 below.

This means that user agents that haven’t implemented the outlining algorithm can use implicit sectioning, and those that have implemented it can effectively ignore the heading levels and use sectioning content to create the outline.

At the time of this writing, no browsers or screen readers have implemented the outlining algorithm, which is why we need third-party testing tools such as the outliner. The latest versions of Chrome and Firefox style <code>h1</code> elements in nested sections differently, but that is very different from actually implementing the algorithm.

When most user agents finally do support it, using an <code>h1</code> in every explicit section will be the preferred option. It will allow syndication tools to handle articles without needing to reformat any heading levels in the original content.

<figure>

<pre><code class="language-markup tmp-html">&lt;div&gt;
      &lt;h1&gt;Horses for sale&lt;/h1&gt;

      &lt;section&gt;
         &lt;h2&gt;Mares&lt;/h2&gt;

         &lt;article&gt;
            &lt;h3&gt;Pink Diva&lt;/h3&gt;
            &lt;p&gt;Pink Diva has given birth to three Grand National winners.&lt;/p&gt;
         &lt;/article&gt;

         &lt;article&gt;
            &lt;h3&gt;Ring a Rosies&lt;/h3&gt;
            &lt;p&gt;Ring a Rosies has won the Derby three times.&lt;/p&gt;
         &lt;/article&gt;

         &lt;article&gt;
            &lt;h3&gt;Chelsea’s Fancy&lt;/h3&gt;
            &lt;p&gt;Chelsea’s Fancy has given birth to three Gold Cup winners.&lt;/p&gt;
         &lt;/article&gt;
      &lt;/section&gt;

      &lt;section&gt;
         &lt;h2&gt;Stallions&lt;/h2&gt;

         &lt;article&gt;
            &lt;h3&gt;Korah’s Fury&lt;/h3&gt;
            &lt;p&gt;Korah’s Fury has fathered three champion race horses.&lt;/p&gt;
         &lt;/article&gt;

         &lt;article&gt;
            &lt;h3&gt;Sea Pioneer&lt;/h3&gt;
            &lt;p&gt;Sea Pioneer has won The Oaks three times.&lt;/p&gt;
         &lt;/article&gt;

         &lt;article&gt;
            &lt;h3&gt;Brown Biscuit&lt;/h3&gt;
            &lt;p&gt;Brown Biscuit has fathered nothing of any note.&lt;/p&gt;
         &lt;/article&gt;			
      &lt;/section&gt;

      &lt;p&gt;All our horses come with full paperwork and a family tree.&lt;/p&gt;
   &lt;/div&gt;</code></pre>

<figcaption>Figure 6: Our horses page, marked up sensibly.</figcaption></figure>

One other point worth noting here is the position of the paragraph “All our horses come with full paperwork and a family tree.” In the example that used headings to create the outline (figure 2), this paragraph is part of the implicit section created by the “Brown Biscuit” heading. Human readers will clearly see that this text applies to the whole document, not just Brown Biscuit.

Sectioning content solves this problem quite easily, moving it back up to the top level, headed by “Horses for sale.”

{{% ad-panel-leaderboard %}}

## Mixing It Up

So, what happens when implicit sections and explicit sections are combined? As long as you remember that implicit sections can go inside explicit sections, but not the other way round, you will be fine. For example, the following works well and is perfectly valid:

<figure>

<pre><code class="language-markup tmp-html">&lt;h1&gt;Horses for sale&lt;/h1&gt;

   &lt;section&gt;
      &lt;h2&gt;Mares&lt;/h2&gt;

      &lt;h3&gt;Pink Diva&lt;/h3&gt;
      &lt;p&gt;Pink Diva has given birth to three Grand National winners.&lt;/p&gt;

      &lt;h3&gt;Ring a Rosies&lt;/h3&gt;
      &lt;p&gt;Ring a Rosies has won the Derby three times.&lt;/p&gt;

      &lt;h3&gt;Chelsea’s Fancy&lt;/h3&gt;
      &lt;p&gt;Chelsea’s Fancy has given birth to three Gold Cup winners.&lt;/p&gt;
   &lt;/section&gt;</code></pre>

</figure>

And it creates a sensible hierarchical outline:

<figure>

 	1. Horses for sale
      1. Mares
         1. Pink Diva
 	      2. Ring a Rosies
 	      3. Chelsea’s Fancy

<figcaption>Figure 7: Implicit sections created by headings inside an explicit section.</figcaption></figure>

However, if you hope to achieve the same outline by nesting an explicit section inside an implicit section, it won’t work. The sectioning element will simply close the implicit section created by the heading and create a very different outline, as shown below:

<figure>

<pre><code class="language-markup tmp-html">&lt;h1&gt;Horses for sale&lt;/h1&gt;

   &lt;h2&gt;Mares&lt;/h2&gt;

   &lt;article&gt;
      &lt;h3&gt;Pink Diva&lt;/h3&gt;
      &lt;p&gt;Pink Diva has given birth to three Grand National winners.&lt;/p&gt;
   &lt;/article&gt;

   &lt;article&gt;
      &lt;h3&gt;Ring a Rosies&lt;/h3&gt;
      &lt;p&gt;Ring a Rosies has won the Derby three times.&lt;/p&gt;
   &lt;/article&gt;

   &lt;article&gt;
      &lt;h3&gt;Chelsea’s Fancy&lt;/h3&gt;
      &lt;p&gt;Chelsea’s Fancy has given birth to three Gold Cup winners.&lt;/p&gt;
   &lt;/article&gt;</code></pre>

</figure>

This would produce the following outline:

<figure>

 	1. Horses for sale
      1. Mares
 	   2. Pink Diva
 	   3. Ring a Rosies
 	   4. Chelsea’s Fancy

<figcaption>Figure 8: Explicit sections can’t go inside implicit sections.</figcaption></figure>

There is no way to make the explicit sections created by the <code>article</code> elements become sub-sections of the Mare’s implicit section.

You can use headings to split up the content of sectioning elements, but not the other way round.

## Things To Watch Out For

### Untitled Sections

Until now we haven’t really looked at <code>nav</code> and <code>aside</code>, but they work exactly the same as <code>section</code> and <code>article</code>. If you have secondary content that is generally related to your website &mdash; say, horse-training tips and industry news &mdash; you would mark it up as an <code>aside</code>, which creates an explicit section in the document outline. Similarly, major navigation would be marked up as <code>nav</code>, again creating an explicit section.

There is no requirement to use headings for <code>aside</code> and <code>nav</code>, so they can appear in the outline as untitled sections. Go ahead and try the following code in the outliner:

<figure>

<pre><code class="language-markup tmp-html">&lt;nav&gt;
      &lt;ul&gt;
         &lt;li&gt;&lt;a href="/"&gt;home&lt;/a&gt;&lt;/li&gt;
         &lt;li&gt;&lt;a href="/about.html"&gt;about us&lt;/a&gt;&lt;/li&gt;
         &lt;li&gt;&lt;a href="/horses.html"&gt;horses for sale&lt;/a&gt;&lt;/li&gt;
       &lt;/ul&gt;
   &lt;/nav&gt;

   &lt;h1&gt;Horses for sale&lt;/h1&gt;

   &lt;section&gt;
      &lt;h2&gt;Mares&lt;/h2&gt;
   &lt;/section&gt;

   &lt;section&gt;
      &lt;h2&gt;Stallions&lt;/h2&gt;
   &lt;/section&gt;</code></pre>

<figcaption>Figure 9: An untitled &lt;nav&gt;.</figcaption></figure>

The <code>nav</code> appears as an untitled section. Now, this generally wouldn’t be a problem and is not considered bad HTML5 code, although in his <a href="https://html5doctor.com/outlines/">recent HTML5 Doctor article</a> on outlining, Mike Robinson recommends using headings for all sectioning content in order to increase accessibility.

Untitled <code>section</code> and <code>article</code> elements, on the other hand, are generally to be avoided. In fact, if you’re unsure whether to use a <code>section</code> or <code>article</code>, a good rule of thumb is to see whether the content has a natural, logical heading. If it doesn’t, then you will more than likely be wiser to use a good old <code>div</code>.

Now, the spec doesn’t actually require <code>section</code> elements to have a title. It says:
<blockquote>“The section element represents a generic section of a document or application. A section, in this context, is a thematic grouping of content, typically with a heading.”</blockquote>

Your interpretation of this probably hinges on your understanding of the word “typically.” I take it to mean that you need a damn good reason not to use headings with <code>section</code> elements. I do not take it to mean that you can ignore it whenever you feel the urge to use a new HTML5 element.

<a href="https://developers.whatwg.org/sections.html#the-article-element">Where the <code>article</code> element is specified</a>, the spec goes even further by showing an example of blog comments marked up as untitled <code>article</code>s, so there are exceptions. However, if you see an untitled <code>section</code> or <code>article</code> in the outline, make sure you have a good reason for not giving it a title.

If you are unsure whether your untitled section is a <code>nav</code>, <code>aside</code>, <code>section</code> or <code>article</code>, a <a href="https://addons.opera.com/addons/extensions/details/html5-outliner/1.0/?display=en">very handy Opera extension</a> will let you know which type of sectioning content you have left untitled. The tool will also let you view the outline without leaving the page, which can be hugely beneficial when you’re debugging sections.

### Sectioning Root

The eagle-eyed among you will have noticed that when I said that sectioning content cannot create a sub-section of an implicit section, there was an <code>h1</code> (“Horses for sale”) not in sectioning content immediately followed by a <code>section</code> (“Mares”), and that the sectioning content did actually create a sub-section of the <code>h1</code>.

The reason for this is sectioning root. <a href="https://dev.w3.org/html5/spec/Overview.html#sectioning-root">As the spec says</a>, sectioning elements create sub-sections of their nearest ancestor sectioning root or sectioning content.
<blockquote>“<a href="https://dev.w3.org/html5/spec/Overview.html#sectioning-content">Sectioning content</a> elements are always considered subsections of their nearest ancestor <a href="https://dev.w3.org/html5/spec/Overview.html#sectioning-root">sectioning root</a> or their nearest ancestor element of <a href="https://dev.w3.org/html5/spec/Overview.html#sectioning-content">sectioning content</a>, whichever is nearest, regardless of what implied sections other headings may have created.”</blockquote>

The <code>body</code> element is sectioning root. So, if you paste the code from figure 7 into the outliner, the <code>h1</code> would be the sectioning root heading, and the <code>section</code> element would be a sub-section of the <code>body</code> sectioning root.

The <code>body</code> element is not the only one that acts as sectioning root. There are five others:

\1.  `blockquote`
\2.  `details`
\3.  `fieldset`
\4.  `figure`
\5.  `td`

The status of these elements as sectioning root has two implications. First, each can have its own outline. Secondly, the outline of nested sectioning root does not appear in, nor does it have an effect on, the outline of its parent sectioning root.

In practice, this means that headings inside any of the five sectioning root elements listed above do not affect the outline of the document that they are a part of.

The final thing (you’ll be glad to hear) that I’ll say about sectioning root is that the first heading in the document that is not inside sectioning content is considered to be the document title.

Try the following code in the outliner to see what happens:

<figure>

<pre><code class="language-markup tmp-html">&lt;section&gt;
   &lt;h1&gt;this is an h1&lt;/h1&gt;
&lt;/section&gt;

&lt;h6&gt;this h6 comes first in the source&lt;/h6&gt;

&lt;h1&gt;this h1 comes last in the source&lt;/h1&gt;</code></pre>

<figcaption>Figure 10: How heading levels at the root level affect the outline.</figcaption></figure>

I won’t try to explain this to you because it will probably only confuse both of us, so I’ll let you play with it in the outliner. Hint: try using different heading levels for the implicit sections to see how the outline is affected; for example, <code>h3</code> and <code>h4</code>, or two <code>h5</code>s.

### Untitled Documents

If no heading is at the root level of the document (i.e. not inside sectioning content), then the document itself will be untitled. This is a pretty serious problem, and it can occur either through carelessness or, paradoxically, by thinking carefully about how sectioning content should be used.

<a href="https://www.456bereastreet.com/">Roger Johansson</a> addresses this issue in his excellent <a href="https://www.456bereastreet.com/archive/201103/html5_sectioning_elements_headings_and_document_outlines/">article on document outlines and HTML5</a> and the <a href="https://www.456bereastreet.com/archive/201104/html5_document_outline_revisited/">follow-up article</a>.

Johansson asks how a proper document outline is supposed to be created for a blog post or other news-type item using HTML5. If you subscribe to the belief that your logo or website name should not be in an <code>h1</code> element, you could mark up your blog post along the lines of the following:

<pre><code class="language-markup tmp-html">&lt;body&gt;
   &lt;article&gt;
      &lt;h1&gt;Blog post title&lt;/h1&gt;

      &lt;p&gt;Blog post content&lt;/p&gt;
   &lt;/article&gt;
&lt;/body&gt;</code></pre>

The document is untitled. Somewhat reluctantly, Johansson settles on marking up the website’s title in <code>h1</code> and using another <code>h1</code> to mark up the article’s title. This is a sensible solution and is backed up by the results of the <a href="https://webaim.org/projects/screenreadersurvey3/#headings">WebAIM screenreader user survey</a>, in which the majority of respondents stated a preference for two top-level headings in exactly this format.

This same approach is also widely used on static pages that are built with HTML5 structural elements, and it could be very useful indeed for screen reader users. Imagine that you are using a screen reader to find a decent recipe for chicken pie, and you have a handful of recipe websites open for comparison. Being able to quickly find out which website you are on using the shortcut key for headings would be much more useful than seeing only “chicken pie” on each one.

Not too far behind two top-level headings in the screen reader user survey was one top-level heading for the document. This is probably my preferred option in most cases; but as we have already seen, it creates an untitled body, which is undesirable.

In my opinion, there is an easy way around this problem: don’t use <code>article</code> as a wrapper for single-blog posts, news items or static page main content. Remember that <code>article</code> is sectioning content: it creates a sub-section of the document. But in these cases, the document is the content, and the content is the document. Setting aside the name of the element, why would we want to create a sub-section of a document before it has even begun?

Remember, <a href="https://html5doctor.com/you-can-still-use-div/">you can still use div</a>!

### hgroup

This is the final item in the list of things to watch out for, and it’s very easy to understand. The <code>hgroup</code> element can contain only headings (<code>h1</code> to <code>h6</code>), and its purpose is to remove all but the highest-level heading it contains from the outline.

It has been and continues to be the subject of controversy, and its inclusion in the specification is by no means a given. However, for now, it does exactly what it says on the tin: it groups headings into one, as far as the outlining algorithm is concerned.

## In Conclusion

The logic behind the document outlining algorithm can be hard to grasp, and the spec can sometimes feel like physics: understandable as you’re reading it, but when you try to confirm your understanding, it dissolves and you find yourself re-reading it again and again.

But if you remember the basics &mdash; that <code>section</code>, <code>article</code>, <code>aside</code> and <code>nav</code> create sub-sections on Web pages &mdash; then you are 90% of the way there. Get used to marking up content with sectioning elements and to checking your pages in the outliner, because the more you practice creating well-outlined documents, the sooner you will grasp the algorithm.

I promise, you will have it cracked after only a handful of times, and you will never look back. And from that moment on, every Web page you create will be structured, semantic, robust, well-outlined content.

### Other Resources

*   “[Creating an Outline](https://dev.w3.org/html5/spec/Overview.html#outlines)” The full W3C specification of the outlining algorithm.
*   “[Document Outlines](https://html5doctor.com/outlines/)” An explanation of the document outlines from the HTML5 Doctor.
*   “[Sectioning content](https://dev.w3.org/html5/spec/Overview.html#sectioning-content)” and “[Sectioning root](https://dev.w3.org/html5/spec/Overview.html#sectioning-root)” The W3C specifications of sectioning content and sectioning root.
*   “[HTML5 Sectioning Elements, Headings, and Document Outlines](https://www.456bereastreet.com/archive/201103/html5_sectioning_elements_headings_and_document_outlines/)” and “[HTML5 Document Outline Revisited](https://www.456bereastreet.com/archive/201104/html5_document_outline_revisited/)” Roger Johansson’s articles on the issue of sectioning content creating untitled documents.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)
*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [Our Pointless Pursuit Of Semantic Value](https://www.smashingmagazine.com/2011/11/our-pointless-pursuit-of-semantic-value/)

{{< signature "al, mrn" >}}
