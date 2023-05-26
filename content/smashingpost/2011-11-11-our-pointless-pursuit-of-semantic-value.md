---
title: Our Pointless Pursuit Of Semantic Value
slug: our-pointless-pursuit-of-semantic-value
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f3bd866-9452-4555-9ede-c357222dd0d3/article-footer-code-illu-opt.jpg
date: 2011-11-11T12:09:02.000Z
author: divya-manian
description: >-
  **Update** (November 12th 2011): Read a [reply by Jeremy Keith](https://www.smashingmagazine.com/2011/11/12/pursuing-semantic-value/)
  to this article in which he strongly argues about the importance of pursuing semantic value and addresses issues discussed in the article as well as in the comments here on Smashing Magazine.
categories:
  - Coding
  - HTML5
  - HTML
  - Semantics
---
<strong>Disclaimer</strong>: This article is published in the <em>Opinion column</em> section in which we provide active members of the community with the opportunity to share their thoughts and ideas publicly. Do you agree with the author? Please leave a comment. And if you disagree, would you like to write a rebuttal or counter piece? Leave a comment, too, and we will get back to you! Thank you.
<blockquote>Meta-utopia is a world of reliable meta data. When poisoning the well confers benefits to the poisoners, the meta-waters get awfully toxic in short order.

– <a href="https://www.well.com/~doctorow/metacrap.htm">Cory Doctorow</a></blockquote>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sexy New HTML5 Semantics](https://www.smashingmagazine.com/2011/11/html5-semantics/)
*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)
*   [A Detailed Introduction To Custom Elements](https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/)

{{% feature-panel %}}

Allow me to paint a picture:

1.  You are busy creating a website.
2.  You have a thought, “Oh, now I have to add an element.”
3.  Then another thought, “I feel so guilty adding a `div`. Div-itis is terrible, I hear.”
4.  Then, “I should use something else. The `aside` element might be appropriate.”
5.  Three searches and five articles later, you’re fairly confident that `aside` is not semantically correct.
6.  You decide on `article`, because at least it’s not a `div`.
7.  You’ve wasted 40 minutes, with no tangible benefit to show for it.</p>

## This Just Straight Up Sucks

This is not the first time this topic has been broached. In 2004, Andy Budd wrote on <a href="https://www.andybudd.com/archives/2004/05/semantic_coding/">semantic purity versus semantic realism</a>.

If your biggest problem with HTML5 is the <a href="https://www.impressivewebs.com/aside-vs-blockquote-html5/">distinction between an aside and a blockquote</a> or the <a href="https://twitter.theinfo.org/29661575610630145">right way to mark up addresses</a>, then you are not using HTML5 the way it was intended.

Mark-up structures content, but your choice of tags matters a lot less than we’ve been taught for a while. Let’s go through some of the reasons why.</p>

### The Web No Longer Consists Of Structured Content

In the golden days of the Web, Web pages were supposed to be repositories of information and meaning, nothing more. Today, the Web has content, but meaning is derived from users’ interactions with it.

XML, RDFA, Dublin Core and other structured specifications have very solid use cases, but those use cases <a href="https://www.alexa.com/topsites">do not account for the majority of interactions</a> on the Web. Heck, no website really has the purity of semantic mark-up that such specifications demand. <a href="https://web.archive.org/web/20060428021228/https://diveintomark.org/archives/2002/12/30/the_tag_soup_of_a_new_generation">Mark Pilgrim writes about this</a> much better than I do.

If you have content that demands semantic purity — such as a library database, a document that needs a table of contents, or an online book (i.e. anything for which semantic purity makes sense) — then by all means stick to the HTML5 outlining algorithm, and split hairs on which element should be an <code>article</code> and which a <code>section</code>. No customer-facing tool exists that takes advantage of this algorithm by producing a table of contents. No browser seems to exploit such tools either.</p>

### Is It Really Accessible?

If accessibility is your reason for using semantic mark-up, then understand that accessibility and semantic mark-up have very little correlation, due to the massive abuse of HTML mark-up on the Web. (I would love to link to Mark Pilgrim’s post on this, but it is dead, so <a href="https://krijnhoetmer.nl/irc-logs/whatwg/20090604#l-877">this will have to do</a>.)

The <code>b</code>, <code>strong</code>, <code>i</code> and <code>em</code> tags are equivalent to the <code>span</code> tag as far as the <a href="https://www.w3.org/TR/2011/WD-html-aapi-20110414/">specification is concerned</a>. And so are some of HTML5’s tags.

As stated on <a href="https://www.html5accessibility.com/">HTML5 Accessibility</a>, almost every new HTML5 element currently provides to assistive technology only as much semantic information as a div element. So, if you thought that using HTML5 elements would make your website more accessible, think again. (How much additional information do <code>&lt;figure&gt;</code> and <code>&lt;figcaption&gt;</code> bring? <a href="https://www.paciellogroup.com/blog/2011/08/html5-accessibility-chops-the-figure-and-figcaption-elements/">None</a>.)

The recent <a href="https://html5doctor.com/time-and-data-element/">debate (or debacle?) on the <code>&lt;time&gt;</code> element</a> is just more proof of the impermanence of the semantic meanings associated with elements.</p>

### Is It Really Searchable?

If SEO is your grand purpose for using semantic mark-up, then know that most search engines do not give more credence to a page just because of its mark-up. The only thing recommended in this <a href="https://www.google.com/support/webmasters/bin/answer.py?hl=en&amp;answer=35291">SEO guide from Google</a> is to use relevant headings and anchor links (other search engines work similarly). Your use of HTML5 elements or of <code>strong</code> or <code>span</code> tags will not affect how your content is read by them.

There is another way to provide rich data to search engines, and that is via <a href="https://schema.org/">micro-data</a>. In no way does this make your website rank better on search engines; it simply <a href="https://www.google.com/support/webmasters/bin/answer.py?answer=1211158">adds value to the search result</a> when a relevant one is found for your website.</p>

### Is It Really Portable?

Another much-touted advantage of the semantic Web is data portability. Miraculously, all devices are supposed to understand the semantic mark-up used everywhere and be able to parse the information therein with no effort. Aryeh Gregor <a href="https://plus.google.com/105458233028934590147/posts/Q2Wnvy1ysBD">puts that myth to sleep</a>:
<blockquote>… +Manu Sporny said that semantic Web people had received feedback that out-of-band data was harder to keep in sync with content. I can attest that in MediaWiki’s case this isn’t true, though… The only times I can see where you’d want to use RDFa or microdata instead of separate RDF is if either you don’t have good enough page-generation tools, or you want the metadata to be consumed by specific known clients that only support inline metadata (e.g. search engines supporting schema.org or such). If the page is being processed by a script anyway, and if the script author has ready access to server-side tools that can extract the metadata into a separate RDF stream, then it’s normally going to be just as easy to publish as a separate stream as to publish inline. And it saves a lot of bloat on every page view.</blockquote>

## What Now, Then?

*   There is no harm using `div` elements; you can continue using them instead of `section` and `article`. I think we should use the new elements to make your mark-up readable, not for any inherent semantic advantage. If you want to use HTML5 `section` and `article` tags to enhance some particular textual documentation for a future document reader, do it.
*   Tools exist today that take advantage of the `nav`, `header` and `footer` elements. [NVDA now assigns implied semantics](https://www.accessibleculture.org/research/html5-aria-2011/) with these elements. The elements are straightforward to understand and use.
*   There is [good support](https://www.html5accessibility.com/tests/landmarks.html) for ARIA landmarks in screen readers, but [be careful](https://www.accessibleculture.org/articles/2011/04/html5-aria-2011/) when using them with HTML5 elements.
*   HTML5 has a host of [new features](https://platform.html5.org). I think we should learn about them, use them, give feedback. Make these features more robust and stable. Yes, most of these features require that you understand and write JavaScript and expose features that create a richer experience for your audience. If that task sounds formidable to you, then start [learning how to code](https://www.highercomputingforeveryone.com/), particularly JavaScript.</p>

### What do you think?

This article is published in the <em>Opinion column</em> section in which we provide active members of the community with the opportunity to share their thoughts and ideas publicly. Do you agree with the author? Please leave a comment. And if you disagree, would you like to write a rebuttal or counter piece? Leave a comment, too, and we will get back to you! Thank you.

{{< signature "al" >}}

