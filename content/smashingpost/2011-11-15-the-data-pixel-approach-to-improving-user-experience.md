---
title: The Data-Pixel Approach To Improving User Experience
slug: the-data-pixel-approach-to-improving-user-experience
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f91fa1-1358-430a-8a9b-7dfe1cb7f203/datapixelsml.jpg
date: 2011-11-15T14:54:26.000Z
author: rian-van-der-merwe
description: >-
  There are many ways to skin a redesign (I _think_ that’s how the saying goes). On a philosophical level, I agree with those who advocate for **realigning, not redesigning**, but these are mere words when you’re staring a design problem in the face with no idea where to start.
categories:
  - UX
  - Design
  - Redesign
  - Graphic Design
---
This article came out of my own questions about how to make the realignment philosophy practical and apply it to my day-to-day work — especially when what’s needed is more than a few tweaks to the website here and there.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Reducing Cognitive Overload For A Better User Experience](https://www.smashingmagazine.com/2016/09/reducing-cognitive-overload-for-a-better-user-experience/)
*   [<span class="headline">How Functional Animation Helps Improve User Experience</span>](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/)
*   [Improve User Experience With Real-Time Features](https://www.smashingmagazine.com/2016/04/improve-user-experience-real-time-features/)
*   [Improving User Flow Through Page Transitions](https://www.smashingmagazine.com/2016/07/improving-user-flow-through-page-transitions/)

I propose an approach to redesign <em>through</em> realignment, by using a framework adapted from Edward Tufte’s principles on the visual display of quantitative information.

{{% feature-panel %}}

But first, a little context.</p>

## Redesign Through Realignment

Let’s recap the redesign versus realign argument. Here is Cameron Moll in “<a href="https://www.alistapart.com/articles/redesignrealign">Good Designers Redesign, Great Designers Realign</a>”:
<blockquote>The desire to redesign is aesthetic-driven, while the desire to realign is purpose-driven. One approach seeks merely to <em>refresh</em>, the other aims to fully <em>reposition</em> and may or may not include a full refresh.</blockquote>

A realignment can include a full refresh, but the starting point is not the visual layer. The starting point is an understanding of the website’s users and their objectives, of market trends and of brand strategy. These are the hard questions that guide a realignment — not a desire to try out some new fonts or see whether a +1 button would look good on the home page.

But surely a visual refresh can be beneficial, too? What’s the danger in giving users something new to look at? In an essay that builds on Cameron’s article, Francisco Inchauste <span class="removed_link" title="https://www.getfinch.com/finch/entry/long-live-the-redesign/">sums up the problem as follows</span>:
<blockquote>Great designers adjust an existing work with little disruption of the foundational design for a goal or purpose. The end result is a modification to the design that improves the user experience. Good designers, on the other hand, recreate existing work focusing on the aesthetic, with a misunderstood notion that it will always improve it. However, they end up disrupting and/or damaging the user’s experience, making no real impact with the effort.</blockquote>

The main problem with big redesigns, therefore, is that, even though objectively the UX might have been improved, users are often left confused about what has happened and are unable to find their way. In most cases, making “steady, relentless, incremental progress” on a website (to borrow <a href="https://daringfireball.net/linked/2011/06/14/thurrott-ios-5-lion">a phrase of John Gruber</a>) is much more desirable. With this approach, users are pulled gently into a better experience, as opposed to being thrown into the deep end and forced to sink or swim.

So, if we agree that a realignment is preferable to a redesign (and I’m sure we never will, but let’s assume we do for the sake of this article), a big question remains unanswered: <strong>What happens when a realignment requires major changes to the website?</strong> What happens when small tweaks aren’t enough, when a website’s UX is so far gone that you’re tempted to scrap everything and start over?

One way to go about it is to use a <strong>continual realignment process</strong> to redesign the website. Build a vision, and know where you’re going in the long term; but get there incrementally, not with a big-bang release. Remaining rooted in the realignment approach ensures that the focus remains purpose-driven, even if the process results in major visual changes. “That’s fine,” you say, “but how do you do it? Where do you begin with such a project?” Let’s now look at one possible approach to redesigning through realignment.</p>

## Edward Tufte And The Data-Ink Ratio

I’ve always been intrigued by Edward Tufte’s principles for visualizing large quantities of data. <a href="https://www.amazon.com/Visual-Display-Quantitative-Information/dp/0961392142"><em>The Visual Display of Quantitative Information</em></a> is one of my favorite books of all time. Recently, I’ve been wondering whether its principles could be applied to Web design and, specifically, the realignment process. The deeper I got into it, the more I realized that within Tufte’s principles lies a goldmine for people who make websites.

<a href="https://www.amazon.com/Visual-Display-Quantitative-Information/dp/0961392142"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108678" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfd5777d-7c17-4f9f-995e-9491a733d7ac/tufte-book.jpg" alt="Tufte Book" width="500" height="350" /></a>

One of Tufte’s central principles in <em>The Visual Display of Quantitative Information</em> is what he calls <strong>data-ink</strong>:
<blockquote>Data-Ink is the non-erasable core of a graphic, the non-redundant ink arranged in response to variation in the numbers represented.</blockquote>

Before we unpack what this means for Web design, it’s important to note that Tufte’s work applies specifically to information graphics and the display of quantitative data, not to the design of graphical user interfaces. However, when carefully interpreted and applied to the field of Web design, the principles are extremely useful.

With that in mind, I propose the concept of <strong>data-pixels</strong> for the design of user interfaces to mirror Tufte’s data-ink for information graphics. In the context of Web design, we can then think of data-pixels as the <strong>simplest and most desirable path that a user can take through a flow</strong> (the “non-erasable core of an interface”). It is what would remain in “<a href="https://www.informationarchitects.jp/en/ia-writer-for-mac/">focus mode</a>” — if nothing else existed on the screen, just the design elements that enable users to get from one screen to the next.

For example, on a payment screen, data-pixels would be the credit-card fields, text labels and “Pay now” button. Nothing else. This is obviously not possible — you need headers, payment summaries, tooltips, trust seals, etc. But the “core data” are the elements of the page that we cannot remove without the user getting stuck with no ability to recover.

From this irreducible point of the design, you can start to add other elements as necessary, and this is what Tufte’s work is all about. Much of what Tufte espouses is finding the right <strong>data-ink ratio</strong> (or what we’ll call data-pixel ratio) for quantitative data, so that the core data can shine through. He lays out five principles for data-ink. Here is an overview and how these principles can be adapted to redesign through realignment.</p>

### Principle 1: Above All Else, Show the Data

<blockquote>Data graphics should draw the viewer’s attention to the sense and substance of the data, not to something else.

– Edward Tufte, <em>The Visual Display of Quantitative Information</em></blockquote>

During a realignment, we should be guided by the principle that <strong>every page should be focused on the core data and the primary task that users need to take in that particular flow.</strong> Anything else is noise and should be added only after very careful consideration.

Craig Mod has written a great article titled “<a href="https://craigmod.com/satellite/our_future_book/">The Shape of Our Future Book</a>.” In it, he describes the “quiet confidence” that a Kindle has when it is woken from its sleep state (compared to the iPad in particular), and then he addresses the data-pixel issue as follows:
<blockquote>I think the same concept of “quiet confidence” can be applied to data. Namely, in designing user experiences, we need to produce data that doesn’t draw attention to itself explicitly as data.</blockquote>

This doesn’t mean that design has to be boring or that aesthetics are not important. It means that we need to be mindful that any layer of design we add to the core data has to serve a specific function and cannot distract from the data itself.

<a href="https://twitter.com/blakey"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108558" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbef6be0-7284-4e8e-8b48-b678859847ce/technology.jpg" alt="Technology in the background" width="500" height="385" /></a><br>
<em>Image credit: <a href="https://twitter.com/blakey">Sarah Blake</a></em>

### Principle 2: Erase Non-Data Pixels, Within Reason

<blockquote>While it is true that these boring [pixels] sometimes help set the stage for the data action, it is surprising […] how often the [pixels] themselves can serve as their own stage.

– Edward Tufte, <em>The Visual Display of Quantitative Information</em></blockquote>

Once the context for the realignment is set by the overarching principle of focusing on core data, it’s time to evaluate the design and start improving the data-pixel ratio.

The first step is to look for ways to erase non-data pixels — the parts of the design that don’t directly apply to the user’s primary task. Look for elements that cannot be connected to <strong>guiding a user to the desired outcome</strong>, such as:

*   Colors that don’t support the visual hierarchy through contrast;
*   Typefaces that draw attention to themselves for no good reason;
*   Gratuitous imagery (stock photography in particular) that does nothing more than break up the page (consider using white space and proximity grouping to create natural breaks instead);
*   Alignment, sizes and color contrast that draw unwanted attention (for example, indented paragraphs, large social-media icons, a bright ad that doesn’t fit the website’s visual style).

One website that could certainly benefit from the removal of non-data pixels is <a href="https://www.do.co.za/">doHome</a>. Notice the gratuitous reflection of the navigation menu, the unnecessary stock photography, and the fact that so little content on the page tells you what the website is about:

<a href="https://www.do.co.za/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108559" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba7107fc-06dd-4874-a30b-8041a406d8df/gradients.jpg" alt="Do.co.za home page" width="500" height="385" /></a>

<a href="https://www.mailchimp.com">MailChimp</a> does a good job of limiting the non-data pixels on its sign-up page. Clear language indicates what to do; large fields with top-aligned labels ensure that you complete the form quickly; some information is included about the plan you’re signing up for; and the button to sign up is big and high-contrast.

<a href="https://www.mailchimp.com"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108560" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/243793ba-1165-4beb-9578-bad51b69e7a6/mailchimp.jpg" alt="Mail Chimp Sign Up" width="500" height="385" /></a>

<a href="https://www.squarespace.com/">Squarespace</a>’s sign-up page removes as much non-data pixels as possible to put all the focus on the task at hand. The background disappears as soon as you click the “Sign up” link, and you’re presented with the following zero-distraction form:

<a href="https://www.squarespace.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108561" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8716e149-d505-401f-90f9-47c2001e8af1/squarespace.jpg" alt="Squarespace Sign Up" width="500" height="385" /></a>

Google+ is another example of a design that employs minimal non-data pixels. As <a href="https://plus.google.com/115711522874757126523/posts/6EbG2uwnE3c">Oliver Reichenstein says</a>:
<blockquote>It is extremely difficult to keep a complicated user interface so light, white and free of lines, boxes and ornaments. The content hierarchy is always clear, color definitions and consistent and clear without labeling them.</blockquote>

This list isn’t exhaustive, but it illustrates the purpose of the principle: to critically evaluate the visual elements in order to strip out what isn’t necessary.</p>

### Principle 3: Erase Redundant Data-Pixels, Within Reason

<blockquote>Gratuitous decoration and reinforcement of the data measures generate much redundant data-[pixels].

– Edward Tufte, <em>The Visual Display of Quantitative Information</em></blockquote>

“Redundant data-pixels” refer to elements of the design that are <strong>repeated without good reason</strong>. Some examples:

*   Rows of products in a table with an “Add to cart” button next to each one. (Consider using check boxes, with one “Add to cart” button at the bottom.)
*   Animation as a way to draw attention to an element. (Consider using high-contrast color and size instead.)
*   “Are you sure you want to do this?” dialogs for simple tasks such as adding a product to a cart. (For potentially catastrophic actions, like deleting an account, this type of dialog is, of course, appropriate.)

Below is an example from the offline word, courtesy of <a href="https://plus.google.com/106699847074126281204/posts/UzhFechmQKr">Allan Kent</a>. The chart shows the price of parking per hour. Surely a simple sign that reads “R10 per hour” would suffice?

<a href="https://plus.google.com/106699847074126281204/posts/UzhFechmQKr"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="109071" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/840cc7ab-78ac-4df0-bd08-1bdd9b2c54f6/parking.jpg" alt="" width="343" height="564" /></a>

Note the addition of “within reason” to each of the data-pixel principles. Tufte himself acknowledges that redundant pixels are sometimes necessary:
<blockquote>Redundancy, upon occasion, has its uses: giving a context and order to complexity, facilitating comparisons over various parts of the data, perhaps creating an aesthetic balance.</blockquote>

The exception, then, is when, in Tufte’s words again, “redundancy has a distinctly worthy purpose”. A “Pay now” button at the top and bottom of a check-out page could be an example of this. One of the buttons is redundant, yet it introduces efficiency so that users don’t have to scroll up or down to place their order.

The guiding principle here is to strive for a minimalist aesthetic, adding redundant pixels only when they serve a larger purpose (for example, when they’re essential to the brand’s promise or to user efficiency).</p>

### Principle 4: Maximize the Data-Pixel Ratio, Within Reason

<blockquote>Every [pixel] on a graphic requires a reason. And nearly always that reason should be that the [pixel] presents new information.

– Edward Tufte, <em>The Visual Display of Quantitative Information</em></blockquote>

Once you’ve erased as many non-data pixels and redundant data pixels as possible, the next step is to figure out what (if anything) is missing from the design. The goal of this principle is to add more pixels to the design, if necessary.

There <strong>should always be a reason</strong> for adding elements to a design, and the reason will usually be that those elements provide information and/or functionality that increases usability. Some examples:

*   Breadcrumbs that tell users where they are on the website and give them an easy way to get back to where they came from.
*   An aesthetic layer of color, typography, layout and so on, to ensure consistency between brand perception and the website.
*   Hover states or tooltips to provide appropriate guidance or contextual help to users.

An example of necessary pixels is relevant inline error messages. Consider the sign-up form on <a href="https://www.quora.com">Quora</a> below. Very few non-data pixels are on the page. The form’s layout is simple, with no extraneous decoration. But if you try to enter only your first name, the page instantly reminds you that a full name is required:

<a href="https://www.quora.com"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108707" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3c7cd9-474e-4e83-b2c7-9bfcdaa77241/quora-2.jpg" alt="Quora Registration" width="500" height="350" /></a>

One could argue that this isn’t technically part of the “core data” of the design. Quora could have let this slide and either allowed accounts with first names only or sorted it out after users have signed up. But it has decided that data integrity is important from the start, so it has added this real-time check.

A little closer to home, this is what the header of <a href="https://www.kalahari.com/">kalahari.com</a> (where I currently work) looked like when I started at the company:

<a href="https://www.kalahari.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108563" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee159c3b-0d59-4a50-b563-f412e852e5ef/k1.jpg" alt="Kalahari old header" width="500" height="164" /></a>

Identifying the non-data pixels in this design is easy: very large radii on the rounded corners, color that grabs too much attention, too many unimportant links, etc. After maximizing the data-pixel ratio to put the focus on the core data (which is search), we ended up with this header:

<a href="https://www.kalahari.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="108566" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcdd5ae4-713d-45a6-b38d-1716b3775aa0/k21.jpg" alt="Kalahari new header" width="500" height="164" /></a>

### Principle 5: Revise and Edit

<blockquote>Probably, indeed, the larger part of the labour of an author in composing his work is critical labour; the labour of sifting, combining, constructing, expunging, correcting, testing: this frightful toil is as much critical as creative.

– T.S. Eliot, <a href="https://www.amazon.com/Selected-Essays-T-S-Eliot/dp/0151803870/"><em>Selected Essays, 1917–1932</em></a></blockquote>

Tufte quotes T.S. Eliot to describe the relentless effort of editing and revising in graphic design work, and it’s certainly true for Web design.

Once you’ve completed a cycle through these principles, it’s time to go back and start again. Every realignment cycle exposes new opportunities to “above all else, show the data”. UX is a never-ending cycle of improvement, and following a realignment process bakes this constant cycle into the strategy in a very natural way.</p>

## Summary

As I mentioned at the beginning of this article, there are many approaches to redesigning a website. The hardest part often is <strong>knowing how and where to start</strong>. As I’ve shown, Edward Tufte’s timeless principles for the visual display of data can be adjusted and used as a framework to get over that initial hump and serve as a catalyst for a cycle of continual improvement through realignment.

What other models or approaches are there to frame a realignment project? How do you get started?

<em>Front page image source: <a href="https://elliotjaystocks.com/">Elliot Jay Stocks</a></em>

{{< signature "al" >}}

