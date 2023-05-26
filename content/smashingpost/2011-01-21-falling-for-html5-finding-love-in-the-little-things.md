---
title: 'Falling for HTML5: Finding Love in the Little Things'
slug: falling-for-html5-finding-love-in-the-little-things
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56b8a8f8-a6b0-4800-8ece-99a3de68994c/rings3-optimised.jpg
date: 2011-01-21T10:44:17.000Z
author: felicity-evans
summary: >-
  Make a difference in the way you code day-in, day-out with some examples to start implementing parts of the HTML5 spec right now. In this article, Felicity Evans goes through some examples that will make every front-end developer smile.
description: >-
  Get to know some HTML5 hacks that will make front-end developers smile. Felicity Evans gives some examples to start implementing many parts of the HTML5 spec right now.
categories:
  - Coding
  - HTML5
  - HTML
---

I’ve lost count of the number of posts that have been written about the big features of HTML5: amongst the most anticipated being rich media (video, audio, canvas) and JavaScript APIs. However, call me a woman of simple tastes, but this is not the sort of thing that gets me swooning. What does? The small additions to the spec that will make the world of difference to the way I code day-in, day-out. This is the stuff fairy tales are made of.

## The Ugly Duckling

HTML has had a troubled past. It was never really designed for what we are now accomplishing with it. This is in part a testimony to its flexibility and adaptability, but there have been inevitable growing pains.

So what was it originally intended for? Well it’s there in the name: Hyper-Text Markup Language. Yes, text; hyper-text to be more exact. Not layout, or images, or video, or fonts, or menus &mdash; or any of the other frippery that it now incorporates.

All these techniques started as “hacks” &mdash; ways of extending the language which were not accounted for in the original spec. Some of the hacks were uglier than others. For example tables for layout (eek!) were a workable (and reliable) way to manipulate the display of information. Similarly, <a title="Scalable Inman Flash Replacement" href="https://www.mikeindustries.com/blog/sifr">sIFR</a> and other JavaScript techniques often account for things that would more naturally be handled natively by the browser, but at the time were not.

## The Handsome Prince

What we need is someone to come to our rescue. In steps HTML5.

The spec is full of ‘a-ha’ and ‘of course’ moments, and that’s not a surprise seeing as one of its founding design principles is that of <a title="HTML5 design principle" href="https://dev.w3.org/cvsweb/~checkout~/html5/html-design-principles/Overview.html?rev=HEAD#pave-the-cowpaths">*paving the cowpaths*</a>:
<blockquote>“When a practice is already widespread among authors, consider adopting it rather than forbidding it or inventing
something new.”

&mdash; HTML Design Principles, W3C Working Draft 26 May 2009</blockquote>

What this means on the ground is that many of the hacks which are used to bend the existing HTML Doctype to our will are now being legitimised in HTML5. Let’s take a look at three examples which are guaranteed to make every front-end developer smile:

{{% feature-panel %}}

### The `<a>` element

This little beauty is fundamental to how the whole web operates, but up until HTML5 it has been very limited. Limited, in fact to being solely inline. Want to create a large clickable banner which wraps around a title, image and text? Well, you’re out of luck. Plain ol’ HTML4.01 won’t let you &mdash; not without JavaScript that is.

However, now that the <code>&lt;a&gt;</code> tag has been declared a block-level within HTML5, there is no end to the elements you can wrap it with. You can confidently (and legitimately) have your <code>&lt;p&gt;</code> and link it too!

### Forms: the place-holder

Web forms are complex things, and we have developed a number of JavaScript add-ons to make them more usable: date pickers, auto-completes, required elements, validation. A lot of these have a new home in HTML5 but I’m going to focus on one common technique: placeholder text.

This is used where you have a text field but you want to prompt the user &mdash; either with the format you would like the text entered (such as a date) or with an example. It is sometimes used in-place of a label when space is premium. Up until now, using placeholder text has required a JavaScript function that auto-clears on focus, and reinstates when the element loses focus (if it has not been replaced by user-entered text). Quite a complex task, one which is now accomplished by the following snippet:

<pre><code class="language-markup tmp-xml">&lt;input id="examples" name="examples" type="text" placeholder="Enter the things you love about HTML5" /&gt;</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/534020f2-28e1-4502-9fe1-79d493c344dc/html5falling.gif"><img loading="lazy" decoding="async"  class="84817" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/534020f2-28e1-4502-9fe1-79d493c344dc/html5falling.gif" alt="input showing placeholder attribute" width="478" height="290" /></a><figcaption>The placeholder attribute removes the need to add JavaScript to input elements.</figcaption></figure>

### Section element

Have you ever run a validation on a page and died inside when the following error has come back?
<blockquote>“WCAG v1 3.5 (AA)] Nest headings properly (H1 &gt; H2 &gt; H3”...”</blockquote>

It might be just me, but this error is particularly hard to fix. Imagine a scenario where you have a main column with heading levels inside the content, followed by a right-hand column containing featured items e.g.

<pre><code class="language-markup tmp-xml">&lt;div id="mainCol"&gt;
&lt;h1&gt;Main title&lt;/h1&gt;
&lt;h2&gt;Secondary title&lt;/h2&gt;
&lt;/div&gt;
&lt;div id="featureCol"&gt;
&lt;h4&gt;Title of feature&lt;/h4&gt;
&lt;p&gt;Sed ut perspiciatis unde omnis iste natus error sit voluptatem
accusantium doloremque&lt;/p&gt;
&lt;/div&gt;</code></pre>

Without knowing what content will be entered in the main column, how do you choose the correct level of heading to start the following column with? You could play it safe and use an <code>h2</code>, but does this really signify the correct semantic importance of this content? Probably not.

HTML5 introduces something called a *section* element. Each section has its own hierarchy, so you can now have multiple <code>h1</code>s on a page. Do I hear you saying ‘a-ha’? As well as eliminating the above error, this also means that content can be more easily reused. For example, when using a CMS, the modules and components can be reordered on a page without having to consider how this might upset the existing hierarchy. Genius.

{{% ad-panel-leaderboard %}}

## Happily Ever After

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56b8a8f8-a6b0-4800-8ece-99a3de68994c/rings3-optimised.jpg"><img loading="lazy" decoding="async"  class="82130" title="wedding rings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56b8a8f8-a6b0-4800-8ece-99a3de68994c/rings3-optimised.jpg" alt="Ensuring you code 'happily ever after'" width="450" height="361" /></a><figcaption>Ensuring your code ‘happily ever after.’ Illustration.</figcaption></figure>

The best news by far is that we can start implementing many parts of the HTML5 spec right now. This is due to another founding design principle; <a title="HTML5 design principle" href="https://dev.w3.org/cvsweb/~checkout~/html5/html-design-principles/Overview.html?rev=HEAD#degrade-gracefully">*graceful degradation*</a>:

<blockquote>“On the World Wide Web, authors are often reluctant to use new language features that cause problems in older user agents, or that do not provide some sort of graceful fallback. HTML 5 document conformance requirements should be designed so that Web content can degrade gracefully in older or less capable user agents, even when making use of new elements, attributes, APIs and content models.”<br /><br />&mdash; HTML Design Principles, W3C Working Draft 26 May 2009</blockquote>

That means no more waiting for IE6 to fall of its perch, or constantly asking “is HTML5 ready yet?” like the impatient child in the back car seat. It means continuing to support IE6 (for most of anyway) but shattering the myth that a website should look exactly the same in all browsers. It means carefully considering which HTML5 elements to use, which CSS3 selectors and properties to adopt to ensure we are building websites for tomorrow, not today.

### Changing Habits

In the short term it’ll mean a bit more work for us in the templating process, and we might need to adapt our workflow accordingly. Here are some questions you might need to ask yourself:

*   Have I adjusted my estimates to allow for adapting the design in different browsers?
*   Have I given myself enough time during build to familiarize myself with new processes and techniques?
*   Have I set the right expectations with my client / the designer / my manager about how the website will look across different browsers?
*   Are there few enough users to degrade support for IE6?
*   Do I need to include JavaScript to add support for CSS3 and HTML5 features in older browsers?

It might seem like a lot of hard work, and something to be put off, but ignore the changing landscape at your peril. Besides, you’ll have plenty of time on your hand as soon as you stop slicing up all those images to add rounded corners, drop shadows and gradients to your design!

So how will this fairytale end? Crack-open your favourite code-editor, type “<code>&lt;!DOCTYPE html&gt;</code>” and you get to write it...

{{% ad-panel-leaderboard %}}

### Further Reading

-   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/html5-and-the-future-of-the-web/)
-   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
-   [The HTML5 Logo: What Do You Think?](https://www.smashingmagazine.com/2011/01/the-html5-logo-what-do-you-think-opinion-column/)
-   [Learning to Love HTML5](https://www.smashingmagazine.com/2010/11/learning-to-love-html5/)

{{< signature "mrn" >}}
