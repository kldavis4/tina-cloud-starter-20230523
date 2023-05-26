---
title: Is There Ever A Justification For Responsive Text?
slug: ever-justification-for-responsive-text
image: null
date: 2012-02-27T22:15:56.000Z
author: james-young
description: >-
  Depending on who you follow and what you read, you may have noticed the concept of “responsive text” being discussed in design circles recently. It’s not what you might imagine — resizing and altering the typography to make it easier to read on a range of devices — but rather delivering varying amounts of content to devices based on screen size.
categories:
  - Mobile
  - Content
  - Responsive Design
---
Depending on who you follow and what you read, you may have noticed the concept of “responsive text” being discussed in design circles recently. It’s not what you might imagine — resizing and altering the typography to make it easier to read on a range of devices — but rather delivering varying amounts of content to devices based on screen size.

One example of this is an <a title="Frankie Roberto responsive text demo" href="https://www.frankieroberto.com/responsive_text">experiment by designer Frankie Roberto</a>. Another is the navigation menu on the website for <a title="Sifter App" href="https://sifterapp.com/">Sifter App</a>. Roberto and Sifter are using media queries to actually hide and display text based on screen size (i.e. not rewriting or delivering different content based on context — as one would do with mobile-focused copy, for example).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)
*   [Introducing Responsive Web Typography With FlowType.JS](https://www.smashingmagazine.com/2013/09/introducing-flowtype-js/)
*   [Balancing Line Length And Font Size In RWD](https://www.smashingmagazine.com/2014/09/balancing-line-length-font-size-responsive-web-design/)
*   [A Case Study On Art-Directed Responsive Web Typography](https://www.smashingmagazine.com/2015/05/benton-modern-typography-case-study/)

Having looked at how this technique works, I wouldn’t endorse it yet, because its practical value is not clear. Also, describing this as “responsive” could legitimize what is possibly a less than optimal coding technique. Below are screenshots of how it works on the Sifter website:

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36b14342-5970-4174-b124-8c1b530c015c/sifter.jpg"><img loading="lazy" decoding="async" class="125994" title="The website for Sifter App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f7fd53-9564-48cc-8465-1e8ffa54f70c/sifter1.jpg" alt="Website for Sifter App" width="500" height="446" /></a><br>
<em>Altering the tabbed content in the navigation menu at <a href="https://sifterapp.com/">Sifter</a>. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36b14342-5970-4174-b124-8c1b530c015c/sifter.jpg">Large view</a>.</em>

## How Is This Accomplished?

In this example (and in Roberto’s demo), you’ll notice a couple of things. The screenshots show two versions of the Sifter website at different screen sizes to demonstrate what is happening at two breakpoints.

When you view the website on a large device, the second-last menu tab will show the full label of “Pricing &amp; Plans.” On smaller devices (anything up to the size of a tablet), the label changes to just “Pricing.” This particular example might not be a big deal, but my main concern is that this is being regarded as “responsive text.” It’s not. It’s simply hiding bloated content, and if the content is not important enough to show on smaller screens, then it’s probably not vital at any size.

Does the change in wording mean that information on Sifter’s plans is offered only to users on large devices, or is the “Plans” part redundant? We can assume not, because the tab at all screen sizes links to the <code>…/plans</code> page. This is potentially confusing for users on small devices: they clicked on “Pricing” but are sent to a page that outlines the plans first.

To show and hide the “Plans &amp;” part of the tab, Sifter’s designer has wrapped the element in a span. For a single menu item, this isn’t the end of the world, but good luck going down the path that <a title="Frankie Roberto responsive text demo" href="https://www.frankieroberto.com/responsive_text">Frankie Roberto demonstrates</a> with his paragraphs. I can’t imagine what a nightmare it would be to maintain multiple versions of actual page content and then tie them into breakpoints! (Not to mention our earlier question about whether text that is hidden at certain sizes is redundant in the first place.)

Hopefully, we all know to avoid hiding content with <code>display: none !important;</code>. Responsive design is many things; its many little tricks and techniques constitute a wonderful approach to making websites flexible. But hiding elements on a screen in this way should not be one of them.</p>

### It’s Just a Demo, Though, Right?

Frankie Roberto’s demo is just that: a demo. He’s clear about that, and he offers a suggestion for a use case. I applaud the effort — everyone should experiment with the Web. The Sifter website is a live website, though — not a demo or proof of concept — and what it has done is being described as “responsive text.”

I’m a huge fan of the concept of “<a title="Jeremy Keith discussing One Web" href="https://adactio.com/journal/1716/">one Web</a>.” If you find you have to hide parts of your content on smaller devices, then you might need to refocus your efforts and write less bloated copy or reconsider your wording of page elements.

One of the joys of working “mobile-first” is having to maintain a sharp and critical eye in order to cut bloat (a capacity we should always exercise, of course). <strong>Responsive text seems to be the polar opposite of this approach.</strong> You are practically admitting from the outset that too much text is on the page. You are making the dangerous assumption that someone on a small device wouldn’t want to read the hidden text.</p>

## Maintenance Problems Will Come Hard And Fast

Frankie Roberto achieves a clever effect in his demo. On a large screen, you see all of the copy. And as the screen shrinks, so does the amount of content (and vice versa, of course).

<a href="https://www.frankieroberto.com/responsive_text"><img loading="lazy" decoding="async" class="125992" title="Responsive text demo on a large screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ccea60-38c2-483c-8a17-c43da939a3c4/responsive-text-demo-large.jpg" alt="Responsive text demo on a large screen" width="900" height="500" /></a><br>
<em>Roberto’s full content, on a desktop screen.</em>

<a href="https://www.frankieroberto.com/responsive_text"><img loading="lazy" decoding="async" class="125993" title="Responsive text demo on a small screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98ae31e2-0b30-42a6-bc82-cd6fb20093f3/responsive-text-demo-small.jpg" alt="Responsive text demo on a small screen" width="900" height="500" /></a><br>
<em>On a smaller screen, the content is reduced.</em>

Achieving this in the demo is easy. A CSS class is applied to the excess paragraphs to hide them.</p>

### Some Potential Problems to Consider

*   The copy will have to be highly structured in order for it to be readable when parts of it are hidden on small devices. For example, if a content block has 10 lines, then it should still flow when lines 2, 5, 9 and 10 are hidden on a tablet and lines 2, 4, 5, 9 and 10 are hidden on a phone.
*   The writer would need some mechanism in the CMS for flagging the breakpoints in the content. The method for updating content would end up being rather technical as a result.

If the message you are communicating on a small screen is sound, then there is nothing you could really “enhance” it with. Anything you add would simply be bloat.</p>

## Are There Any Potential Uses For Responsive Text?

I don’t think there are. But I realize this is just my opinion, and I encourage readers and the wider Web community to evaluate it for themselves and disprove me with solid examples.

When discussing this on Twitter the other day, I got interesting responses from a number of fellow designers. Many agreed that whatever you display on a small screen should be your content everywhere, because that is the distillation of your message.

Roberto (<a title="@frankieroberto" href="https://twitter.com/frankieroberto">@frankieroberto</a>) suggests a potential use case for adaptive news content; for example, showing a summary, a mid-length version or the full article depending on the device. This does sound like a useful way to digest news, but in such a fast-moving environment, I can’t imagine copyeditors would thank you for assigning them to write content that adapts so extensively and still makes sense in these different contexts. But it’s something to think about.

<a href="https://twitter.com/stephanierieger/status/170142401669763074">Stephanie Rieger points out</a> that producing bloat-free content on a big website can be incredibly time-consuming:
<blockquote>@welcomebrand @froots101 Discussions with stakeholders reveal last round of copywriting took 6 mths End result, hide text on ‘lesser’ screen</blockquote>

No argument there. I’m working on rebuilding a large website, too, and am encountering the same issues. But I’m not sure that hiding content based purely on screen size is wise. If it’s not relevant or worth displaying, don’t simply hide it: delete or unpublish it.</p>

## In Conclusion

My interpretation of the Sifter website and what its designer is trying to achieve may be wrong (this is an opinion piece, remember!). Feel free to tell me as much in the comments below. But from my quick look at the design, code and copy, I won’t be embracing responsive text anytime soon, despite it being an interesting experiment and endorsed by some very clever folks.

I struggle to think of a use case that withstands the basic scrutiny that I apply to content for my clients, which is that if all of the content is not good enough to show on all devices, then the amount of content is not optimal. I recognize that this is a harsh stance, so do check out the code and experiments covered here so that you can make up your own mind.

Remember, just because something is “responsive,” it might not be best for your project.

{{< signature "al" >}}

