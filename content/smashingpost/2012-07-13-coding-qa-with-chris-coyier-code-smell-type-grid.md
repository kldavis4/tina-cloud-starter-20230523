---
title: 'Coding Q&A With Chris Coyier: Code Smell And Type On A Grid'
slug: coding-qa-with-chris-coyier-code-smell-type-grid
image: null
date: 2012-07-13T07:56:58.000Z
author: chris-coyier
description: >-
  Here we are again! Smashing Magazine’s Q&A. Your question could be about a
  very specific problem you are having, or it could be a question about
  philosophical approach. Go wild and challenge us!
categories:
  - Coding
  - CSS
---
Howdy, folks! Welcome to the new incarnation of Smashing Magazine’s Q&amp;A. It’s going to work like this: you send in questions you have about CSS, and at least once a month we’ll pick out the best questions and answer them so that everyone can benefit from the exchange. Your question could be about a very specific problem you're having, or it could be a question about a philosophical approach. We’ll take all kinds.

We’ve done a bit of this kind of exchange before with a wider scope, so if you enjoy reading the Q&amp;A, check out <a href="https://www.smashingmagazine.com/author/chris-coyier/">my author archive</a> for more of them.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Optimize Email Newsletters With CSS](https://www.smashingmagazine.com/2011/08/from-monitor-to-mobile-optimizing-email-newsletters-with-css/)
*   [Email Newsletter Design: Guidelines And Examples](https://www.smashingmagazine.com/2010/02/email-newsletters-guidelines-and-examples/)
*   [Typographic Patterns In HTML Email Newsletter Design](https://www.smashingmagazine.com/2015/08/typographic-patterns-in-html-newsletter-email-design/)
*   [CSS Baseline: The Good, The Bad And The Ugly](https://www.smashingmagazine.com/2012/12/css-baseline-the-good-the-bad-and-the-ugly/)

## Designing For Email

Andrejs Abrickis asks:
<blockquote>"Sometimes I face trouble with HTML email design and the proper CSS code. It takes quite a lot of time to make it cross-client compatible. I would like to know your opinion about the best CSS reset that could help to speed up email newsletter development. Is there any good tool for testing HTML emails?"</blockquote>

{{% feature-panel %}}

First and foremost, I recommend keeping <strong>emails very simple</strong>. Ask yourself what the primary message of the email is and how well the current design of the email is serving that. Could it simply be text? Would it be <em>better</em> if it was text? I find that's often true.

If you are certain you need to make an HTML email, I’d again err on the side of simplicity. An idea I've been toying around with is making the email design the size of a portrait smartphone layout. That constraint forces you to think about the message again, enforces simplicity (and as a side bonus, will look good on both mobile and desktop clients). When is the last time you got an email and thought: <em>"Man, I wish this email was more complicated!"</em>

<a href="https://htmlemailboilerplate.com/"><img class="aligncenter size-full wp-image-120729" title="HTML Email Boilerplate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3aaf900-6e90-4d97-aea1-e1197092abfe/html-email-boilerplate.gif" alt="HTML Email Boilerplate" width="500" height="300" /></a><br>
<em><a href="https://htmlemailboilerplate.com/">HTML Email Boilerplate</a> provides a template of sorts, absent of design or layout, that will help you avoid some of the major rendering problems with the most common email clients out there — Gmail, Outlook, Yahoo Mail, etc.</em>

But you wanted to know about cross-client compatibility and testing. Do check out the <a href="https://htmlemailboilerplate.com/">HTML Email Boilerplate</a>. It was created in the same spirit as the HTML5 Boilerplate in that it addresses all the various quirks across email clients and gives an example of a very minimal structure by which to start. I've tried to use it as is, but I have to admit that I found it a bit too much for the simple email work I was doing. More complex and varied emails will certainly benefit from it and it's also certainly a great reference for snagging quick problem-solving bits of code.

The two simple rules of thumb for HTML email development are:

1.  **Use tables for layout.** This is still the most sturdy layout method for cross-client.
2.  **Inline style everything.** Any other CSS support is spotty.

Designing using inline styles is a big pain in the butt, so I'd recommend developing with a <code>&lt;style&gt;</code> block in the <code>&lt;head&gt;</code> for your CSS. Save that as your development copy, and then just before deployment, run it through MailChimp's <a href="https://beaker.mailchimp.com/inline-css">Automatic CSS Inliner Tool</a> which will do the dirty work of inline styling everything for you.

Speaking of MailChimp, you might want to consider just using their service to build and deploy emails. Their templates are already cross-client compatible (plus they have a <a href="https://mailchimp.com/features/inbox-inspector/">testing service</a>). Their designer tool is easy to use and helps you through the process. Not to mention, you get all these other huge benefits like better deliverability that you can't get on your own, statistics, support, and many more features. Sorry if that sounded like an ad, but I'm all about using services that make our lives easier and better as developers.

MailChimp isn't the only service on the block either, <a href="https://www.campaignmonitor.com/">Campaign Monitor</a> is also great, and do great things for the developer community, including maintaining this <a href="https://www.campaignmonitor.com/css/">epic chart of CSS support</a> for email clients.

<a href="https://www.campaignmonitor.com/css/"><img class="aligncenter size-full wp-image-120729" title="Campaign Monitor HTML Email Reference" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afc7a5f2-c6a3-4c2a-a0f6-59f05ad0a90f/campaignmonitor.gif" alt="Campaign Monitor HTML Email Reference" width="500" height="403" /></a><br>
<em>CSS support on <a href="https://www.campaignmonitor.com/css/">Campaign Monitor</a>.</em>

## Type On A Grid

Maxime Parmentier asks:
<blockquote>"I was wondering how you keep a consistent line-height in every element of your page? It's much more difficult than it sounds in practice. Any tools or techniques that you can recommend?"</blockquote>

Often times that practice is called maintaining a "baseline grid." Here's <a href="https://24ways.org/examples/compose-to-a-vertical-rhythm/example.html">a demo</a> from a <a href="https://24ways.org/2006/compose-to-a-vertical-rhythm">Richard Rutter article</a>. And <a href="https://www.alistapart.com/d/settingtypeontheweb/example.html">another demo</a> from a <a href="https://www.alistapart.com/articles/settingtypeontheweb/">Wilson Miner article</a>. I've <a href="https://css-tricks.com/examples/TypographicGrid/">played with it myself</a> a bit.

Dave Rupert offers <a href="https://dl.dropbox.com/u/3649202/slides/2012/gettinflexy/index.html">a talk about responsive design</a>, where he discusses how <code>em</code>s are useful for baseline grids because they are based on ratios. He also talks about how they are particularly good in the math-ridden world of responsive design. Here's an example by Dave of type lining up nicely to a grid that also accommodates some of the weirdness of different-sized headers.

<img class="aligncenter size-full wp-image-120729" title="Baseline Grid" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5a92960-6b47-483d-bb62-232371c2410d/type-grid.png" alt="Baseline Grid" width="500" height="376" /><br>
<em>View this example.</em>

There is a book by Khoi Vinh all about grids (including type grids) called <a href="https://www.amazon.com/gp/product/0321703537/ref=as_li_ss_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=0321703537&amp;linkCode=as2&amp;tag=indesignhelpc-20&amp;l=as2&amp;o=1&amp;a=0321703537">Ordering Disorder: Grid Principals for Web Design</a>. Khoi teaches all about grids but is clear that you don't have to be dogmatic about them. Breaking the grid sometimes is OK, as long as you come back to it. I think a nice metaphor is <em>syncopation in music</em>—the rhythm is broken on purpose during a song, so that when it kicks back in, it’s noticed and feels good.</p>

## Centering And Resets

Smarajit Dasgupta asks:
<blockquote>"<strong>1.</strong> What is a decent browser-compatible way to center floated (or inline) elements like buttons and links in flexible (or unknown) width scenarios?

<strong>2.</strong> What is your preferred CSS reset in the HTML5 age? Do you still advise the usage of the great Eric Meyer's reset, which pretty much strips all the browser-induced styles for elements? Or do you use something such as normalize.css or write your own on a case basis?"</blockquote>

<strong>1.</strong> Inline elements are easy to center, as they respect the <code>text-align</code> value of the parent, which you can set to <code>center</code>. So say you have a bunch of anchor links in a row, you'd just wrap them in a nav element and apply the center text alignment to that (<a href="https://codepen.io/chriscoyier/pen/hIcGj">like this</a>). If you need them to behave a bit more like block level elements (e.g. be of a set width or height), you can make them <code>display: inline-block;</code> and they will still stay centered (<a href="https://codepen.io/chriscoyier/pen/CjhxI">like this</a>).

Unfortunately you can't center a floated element. I'm not surprised really, as the "what happens if" scenarios surrounding that are too many to count. But just for funzies, let's say you had two columns of text and you wanted to "center float" an image between them, meaning that the text in the left column would wrap to the left, and the text in the right column would wrap to the right. You can "fake" this by positioning two elements half the size (might as well be pseudo elements, because they have no semantic meaning) on the right-side of the left column and left-side of the right column. A picture is easier to understand:

<a href="https://css-tricks.com/float-center/"><img class="aligncenter size-full wp-image-120729" title="Floating Image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1bb1f0-c246-49f2-8e0b-07295d67580c/floating-image.jpg" alt="Floating Image" width="500" height="349" /></a><br>
<em>The floating kitty <a href="https://css-tricks.com/float-center/">demo</a>.</em>

Then you would place the element in the space that makes sense (probably with absolute positioning). <a href="https://css-tricks.com/float-center/">More about this idea here.</a>

<strong>2.</strong> I like <a href="https://necolas.github.com/normalize.css/">normalize.css</a>. I don't like the idea of stripping things away just to put them back. So my process is to take a copy of normalize.css, not remove anything, but change some declarations to my liking (which still ensures consistency, because you are being explicit). Then include that in my global style sheet like I would include a reset, and go from there.</p>

## Opacity Blues

Chris Klein asks:
<blockquote>"How do I stop inheritation of opacity? I can't use another png with 50% opacity and higher <code>z-index</code> above it as the layout has to stay 100% liquid. Also, I tried to insert spans between the box with opacity and the following boxes—but the opacity still is inherited to all other boxes it follows. Even if the following boxes claim <code>opacity: 1;</code>, it doesn't matter, inheritation goes on."</blockquote>

There are a lot of little bits in there that make me wish we could look at the exact layout you're working with. If the backgrounds in question are flat colors, just use <a href="https://css-tricks.com/rgba-browser-support/">RGBa</a> or <a href="https://css-tricks.com/examples/HSLaExplorer/">HSLa</a>. These are both color value types you can use to declare an alpha value, which essentially means "what percentage transparent is this color?". For instance <code>rgba(255, 0, 0, 0.5)</code> means "50% red". This makes a lot more sense than using actual <code>opacity</code> on element, which as you know, affects everything inside (not just the background).

As you also know, opacity affects all child elements and you can't fight against it by setting a child element's opacity higher (the child <em>does</em> have full opacity by default, it's just within a parent that doesn't). It is like that for good reason. We would be much worse off if, in order to fade out an area of a website, we had to select theoretically infinite child elements and fade each individually.

If the background in your design isn't a flat color, you can join the club for wishing there was a <code>background-opacity</code> property. One thing you may want to try are pseudo elements. Leave the main element at full opacity, but apply <code>::before</code> and <code>::after</code> selectors that you position as needed and apply opacity to those. Nicolas Gallagher has <a href="https://nicolasgallagher.com/css-background-image-hacks/demo/opacity.html">a demo of that</a>.

<a href="https://nicolasgallagher.com/css-background-image-hacks/demo/opacity.html"><img class="aligncenter size-full wp-image-120729" title="Pseudo Element" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36ee76b6-cdac-445e-89b9-01b19e06e639/pseudo-element.jpg" alt="Pseudo Element" width="500" height="450" /></a><br>
<em>The Jupiter oppacity <a href="https://nicolasgallagher.com/css-background-image-hacks/demo/opacity.html">demo</a>.</em>

## Border-Radius On Images

Donovan Hutchinson asks:
<blockquote>"Why isn't it possible to directly apply <code>border-radius</code> to an image? And is the best approach to use a wrapping <code>div</code>?"</blockquote>

It is possible! You apply it just like you think you would:

<pre><code class="language-css">img {
  border-radius: 10px;
}</code></pre>

<img class="aligncenter size-full wp-image-120729" title="Border Radius" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2477632c-7c40-4f0f-9b68-e8fd4af13b42/border-radius-image.png" alt="Border Radius" width="448" height="162" /><br>
<em>Border Radius demo.</em>

I think there was some confusion on this for a while, because in the not-so-distant past, Firefox 3.6 required the use of <code>-moz-border-radius</code> for rounded corners, and that implementation didn't work on images. IE9 was the first version to support border radius and it does so un-prefixed and perfectly fine on images so even IE isn't a concern here.

If you absolutely need Firefox 3.6 (and down) support (<a href="https://gs.statcounter.com/#browser_version-ww-monthly-201106-201206">1.55% global usage and falling fast</a>), yep, like you mentioned, you can get it by using a div instead and setting the background-image of the div to the src of the image. You would do that in your template wherever it spits out that URL (or if that's not possible, with a bit of jQuery):

<pre><code class="language-javascript">$("div.avatar").each(function() {
  var el = $(this);
  var url = el.find("img").hide().attr("src");
  el.css("background-image", "url(" + url + ")");
});</code></pre>

## Spotting Bad Code

Michael Zanzini asks:
<blockquote>"How can you tell if your CSS code smells? What are the signs that the code is sub-optional, or that the developer hasn't done a good job? What do you look for in the code to determine how good or bad it is?"</blockquote>

The most obvious way to tell: does the website look all screwed up? Then it's bad CSS. If the website looks perfect, then it passes the first test.

The next thing I'd look for without getting too down and dirty is the formatting. I wouldn't care about trivial things like tabs or spaces or spacing after selectors, but instead general cleanliness and consistency. Does it look like they <strong>have a style that they adhere to</strong>, or is it sloppy and random? Clean code is a sign of a respectful developer. It's not proof the code is good but it's a good start. Mind you, you should be looking at the authored CSS, not deployed CSS, as that could be altered during a build process.

After those rather obvious things, you'll have to get mentally more into the code. Read through it. Do the selectors look nice and rational (e.g. nothing too ridiculously specific like <code>.article #comments ul &gt; li &gt; a.button</code>)? Does there appear to be an awful lot of repeated code (e.g. the same complex box-shadow declared 15 times)? Is it absolutely enormous (e.g. 100k would be be absolutely enormous, as a check)?

The last thing I might do is try and test understandability by running a personal test. Assuming that you are half-way decent at CSS yourself, think of a small task you might need to do on the website. Adjust the colors and spacing of a particular header. Try and do it. Was it easy? Good. Was it hard to figure out? Not good.</p>

## Submit Your Question!

Keep up the great questions, folks! Got a good one? Submit your CSS question via our form, and we’ll pick the best for the next edition. So long!

{{< signature "jvb" >}}

