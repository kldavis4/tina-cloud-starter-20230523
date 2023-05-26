---
title: 'Block Quotes and Pull Quotes: Examples and Good Practices'
slug: block-quotes-and-pull-quotes-examples-and-good-practices
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b17b17a-dd10-4238-8d9b-cd796bc62e3f/quote.gif
date: 2008-06-12T13:41:10.000Z
author: sven-lennartz
description: >-
  **Quotes** are used to emphasize excerpts of text. Since users almost never read but scan we need to provide them with some focus anchors to fix their attention to the most important parts of our articles. Furthermore, quotes are always used for testimonials and sometimes for blog comments. They can be styled using graphics, CSS and a little bit of JavaScript. Sometimes, creative dynamic solutions can be applied as well.
categories:
  - Showcases
  - Design
  - Web Design
---
This post presents <strong>creative examples and best practices for design of pull quotes</strong>. We’ve tried to identify some common solutions and interesting approaches you may want to use or develop further in your projects.

## Aren't all these quotes the same?

No. First of all: quote ≠ block quote ≠ pull quote. <strong>Pull quotes</strong> are short excerpts from the presented text. They are used to pull a text passage out of the reader's flow and give it a more dominant position in the post or the article.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6d568c5-f35b-44c1-a124-178537bade53/andy.gif" alt="Screenshot Pullquote" width="386" height="161" /><br>
<em>Pull quote included into an article. The pulled out passage is mentioned few blocks further.</em></figure>

Just like a pull quote <strong>blockquote</strong> (actually <em>block quotations</em>) are also set off from the main text as a distinct paragraph or block. However, they refer to some external citation which isn't already mentioned in the article. Block quotations are usually placed within the reader's flow.

Finally, "normal" <strong>quotes</strong> cite the content found in some other sources and are included to support the content rather than dominate over it.</p>

## Blockquote vs. Q vs. Cite

According to HTML specifications, there are three elements which are supposed to semantically mark up quotations, namely <code>&lt;blockquote&gt;</code>, <code>&lt;q&gt;</code> and <code> &lt;cite&gt;</code>. Although all intended to markup quotes, they should be used in different contexts. So when should you use what? <a href="https://htmldog.com/reference/htmltags/" rel="nofollow">HTML Dog</a> provides a nice and compact overview of these elements:

### <blockquote>

<strong>blockquote</strong> is a large quotation. The content of a blockquote
element must include block-level elements such as headings, lists, paragraphs
or div's. This element can also have an optional attribute <code>cite</code>
that specifies the location (in the form of a URI) where the quote has come from. Example:

<pre><code class="language-html">&lt;blockquote cite="https://www.htmldog.com/reference/htmltags/blockquote/"&gt;

 &lt;p&gt;A large quotation. The content of a blockquote element must include block-level elements such as headings, lists, paragraphs or div's.&lt;/p&gt;
 &lt;p&gt;cite can be used to specify the location (in the form of a URI) where the quote has come from.&lt;/p&gt;

&lt;/blockquote&gt;
</code></pre>

### &lt;q&gt;

<strong>q</strong> is a small quotation. The content of this element is an in-line quote. Modern browsers know how to interpret <code>&lt;q&gt;</code> which is why you can style quotations using this HTML-elements via CSS. Example:

<pre><code class="language-html">&lt;p&gt;Bob said &lt;q&gt;sexy pyjamas&lt;/q&gt; but Chris said &lt;q&gt;a kimono&lt;/q&gt;&lt;/p&gt;</code></pre>

Although <code>&lt;q&gt;</code> is almost never used, it has some useful properties. For instance, you can <strong>specify the appearance of quotes</strong> within the <code>&lt;q&gt;</code>-element via CSS. That's reasonable as different languages use different quotation marks for the same purpose. For instance, these ones:

<pre><code class="language-html">Q {}
Q { quotes: '»' '«' }
Q { quotes: '„' '“' }</code></pre>

Modern browsers support this way of styling. Of course, Internet Explorer (even in its 8th version) doesn't support it although it knows <code>&lt;q&gt;</code> pretty well. In particular, since some problems with encoding of quotes can appear sometimes it's useful to provide numeric values (see below).

According to standards you can even specify the appearance of quotation marks depending on the browser's language of the user. This is how a W3C-example looks like:

<pre><code class="language-html">:lang(fr) &gt; Q { quotes: '« ' ' »' }
:lang(de) &gt; Q { quotes: '»' '«' '2039' '203A' }</code></pre>

As lovely as they may be, pull quotes have inherent problems in the way they are placed in the middle of HTML content. To a visual, CSSenabled browser all might seem hunky-dory, but to those browsers that are not CSS-abled and fall back on the plain HTML or to screen readers for visually impaired users, the pull quotes will appear slap bang in the middle of the main content. A quote suddenly appearing between two paragraphs is clearly out of place and will confusingly break the flow.

If you are using pull-quotes, it is wise to provide a little extra information for users who would stumble on this problem. In the XHTMLyou can provide a message, hidden from view with CSS that reads something like "Start of pull-quote" before the quote and then "endquote" after it.You could even have a link similar to the "skip navigation" link, which would offer the user the ability to skip the pull-quote and continue to the main content.</p>

### &lt;cite&gt;

<strong>cite</strong> defines an in-line citation or reference to another source. Example:

<pre><code class="language-html">&lt;p&gt;And &lt;cite&gt;Bob&lt;/cite&gt; said &lt;q&gt;No, I think it's a banana&lt;/q&gt;.&lt;/p&gt;</code></pre>

Summing up: for large quotes use <em>blockquote</em>, for small quotes use <em>q</em> and for references to another sources <em>cite</em> should be used. In practice, usually only <em>blockquote</em> and <em>q</em> are used.</p>

## Gallery of Pull Quotes and Citations

Quotes, braces, lines, dialogue boxes, balloons — there are some paths a designer can take to create a beautiful and <strong>memorable quote</strong>. Design solutions vary in colors, forms, and sizes. Different techniques produce different result: However, it is important that it is clear to the visitors that the quote is a quote. Otherwise, it becomes easy to keep track on the content.

Keep in mind: pull quotes shouldn't be used too often, they shouldn't be too large, and they shouldn't be included for the wrong purposes. In most cases an ordinary article should have at most 1-2 pull quotes. Otherwise, they lose their appeal, and the article becomes harder to scan.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9d74c26-9e9b-46e9-b555-70ebefab9a16/99.gif" alt="Screenshot Pullquote" width="659" height="116" /></figure>

Take a look at the example above. 99designs uses a block quotation to emphasize what the site is about. However, the text put in the quotes actually isn't a quotation. We do not know why quotation mark is used in this case. We do know, though, that they shouldn't be used in this context.</p>

## 1\. Simple indentation

In most cases simple indentation is enough. In this case, the <strong>structure of the content makes clear</strong> that the intended content is taken out from the main content flow. However, using this approach you need to make sure you have a very intuitive typographic and visual hierarchy and the indentation won't be misunderstood. Often <em>italics</em> are used to indicate that the content is a quote, and sometimes quotation is centered. The latter technique, however, is used quite rarely.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8072a25a-f29c-4ab8-b855-980b964de687/webr.jpg" alt="Screenshot Pullquote" width="539" height="102" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87436544-6690-408c-b07e-aa8340e8a9a6/prax.jpg" alt="Screenshot Pullquote" width="258" height="96" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1c133a2-8241-4a67-9cd4-642cd17a3553/matt.jpg" alt="Screenshot Pullquote" width="556" height="91" /></figure>

## 2\. Quotes and indentation

Another standard approach for design of pull quotes is to use the quote itself as a visual element to clearly indicate what the text passage is supposed to stand for. This technique is by far the most popular one and there is a good reason behind it: it unambiguously communicates the meaning of the text block. Surprisingly, the quote visuals are almost always <strong>placed on the left of the quote</strong>. You may try to experiment with quote on the right, or at the bottom of the passage.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8f162e6-11cb-4a4f-a6e5-13ca7957f08c/block.jpg" alt="Screenshot Pullquote" width="393" height="267" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1e31adf-8a80-4e86-9771-159356eab4d0/ala.jpg" alt="Screenshot Pullquote" width="515" height="83" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3c6d218-cd33-45f9-af5c-84f100547960/dville.jpg" alt="Screenshot Pullquote" width="467" height="82" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/547422d0-1df9-4db2-bcd6-a9391ab06e04/artyp.jpg" alt="Screenshot Pullquote" width="447" height="96" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a15015e-857c-4d1f-8d40-7de42f7882dc/shaun.jpg" alt="Screenshot Pullquote" width="402" height="199" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be842b52-58f4-4cbd-881e-e6c52b5b71ac/456.jpg" alt="Screenshot Pullquote" width="500" height="85" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/979040a6-3e67-4369-be6b-8bb3d2cbf523/el.jpg" alt="Screenshot Pullquote" width="496" height="87" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f89def57-a52b-4534-98bd-e71c7e9ebd82/webstr.gif" alt="Screenshot Pullquote" width="294" height="56" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ce51ccd-6028-40cc-ac5a-430d4f0025a2/mezzo.jpg" alt="Screenshot Pullquote" width="508" height="115" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d4435d-f714-4601-a85f-86ad1274fe5d/wish.jpg" alt="Screenshot Pullquote" width="500" height="105" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74ad47db-22be-489a-a6fc-231a2d70d5b0/45rb.jpg" alt="Screenshot Pullquote" width="552" height="142" /></figure>

## 3\. Lines and indentation

Standard, most usual and recommended way of designing blockquotes.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/548a4f96-b77e-4c91-b6c8-de90c9eb7af6/coda.jpg" alt="Screenshot Pullquote" width="527" height="80" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9615a296-9cd9-42a5-b3c5-1543f4fd7e49/oneman.jpg" alt="Screenshot Pullquote" width="498" height="140" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa12a104-3471-4d6e-8708-f5b492a75c27/sfl2.jpg" alt="Screenshot Pullquote" width="431" height="200" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68f77873-6ed0-42cc-8210-ef8b8f631e03/sh1.jpg" alt="Screenshot Pullquote" width="496" height="85" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0822dadb-9b32-475b-9d0d-d153b2e74fcd/sh2.jpg" alt="Screenshot Pullquote" width="500" height="99" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8524fa6d-8474-4ef7-8d3b-288c97de7292/ilove.jpg" alt="Screenshot Pullquote" width="485" height="127" /></figure>

## 4\. Quotations highlighted with a color

Frequently designers use indentation together with a <strong>variation of </strong>color which is applied to the quote. Usually if the layout is dark quotes are presented in colors which are darker than the main content. And if the layout is light the quote is presented in lighter colors. If quotes need to be strongly emphasized vibrant colors are used. For modest highlighting usually slight variations of main colors suffices to indicate the difference between the main content and cited text.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c75c1df-ea9c-44ca-ab92-3d80c70cabbf/sfl.jpg" alt="Screenshot Pullquote" width="243" height="107" /><br>
<em>Natalie Jost displays a random quote from the Bible on her blog</em></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58b04635-b4d8-4372-8221-74244988d98e/croft.jpg" alt="Screenshot Pullquote" width="453" height="134" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fd4e7a1-8e70-4564-ab04-e820f8d05632/jesse.jpg" alt="Screenshot Pullquote" width="248" height="187" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4f00dd1-c588-4bc1-9986-4f75498962cf/matt2.jpg" alt="Screenshot Pullquote" width="287" height="159" /></figure>

## 5\. Pull Quotes

Actually we know it from print where <em>quotes-neighbours</em> are supposed to <strong>emphasize some important message</strong> or interview excerpts. Pull quotes are placed not within, but next to the content. Such quotes are usually short and don't provide any additional information as they can also be found in the article. In Web the technique is seen rather rarely, but it has a charm of its own and — if used properly and for the right purposes — may strongly support the content. To clearly separate the "neighbours" from the main content designers often use lines or a large amount of whitespace.

It is important to understand that in such cases pull quotes break the usual content flow which may make it harder for the readers to actually follow the argumentation of the article. In some cases it is more effective to avoid quotes (e.g. if a complex matter is described) while in other cases quotes can quicken and simplify the understanding (e.g. the main statement in the interview).

Quotes-neighbours are <strong>usually placed on the right side</strong> of the content in order to not break the reader's flow and remain passive.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/558819eb-a2b5-42b8-aebd-8418ea751779/dweb2.jpg" alt="Screenshot Pullquote" width="487" height="201" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2d5d549-3647-4107-9100-4a008ed09360/garr.jpg" alt="Screenshot Pullquote" width="448" height="271" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4447350e-ab4f-404f-9558-d5020f067b08/freelance.jpg" alt="Screenshot Pullquote" width="400" height="299" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5873be0-0e4b-4e8d-9d2e-8ef0088ae48f/ianjames.jpg" alt="Screenshot Pullquote" width="355" height="268" /></figure>

## 6\. Creative solutions

Sometimes designers come up with creative solutions one actually wouldn't expect from such an element as a quote. Here are some of them. Hopefully, they'll help you to come up with further interesting ideas for the design of pull quotes.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08b0e270-2fff-4e35-8401-486f36248ec5/mega.jpg" alt="Screenshot Pullquote" width="357" height="371" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6b61bdb-b506-4059-80b9-efe8276cbec2/wdindia.gif" alt="Screenshot Pullquote" width="285" height="237" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70830e0b-68ad-40a2-aefe-f116b9d2edb6/miss.jpg" alt="Screenshot Pullquote" width="411" height="289" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21072cab-d7cd-48f6-9cdc-164389c05385/spr.jpg" alt="Screenshot Pullquote" width="534" height="189" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4dde717-e161-4306-ac57-e1957e6599d5/trff4.jpg" alt="Screenshot Pullquote" width="500" height="133" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d91bc6e7-049c-4c1f-b568-c6b558c3c529/mhv.gif" alt="Screenshot Pullquote" width="281" height="194" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31c64ba8-6524-448d-b1ee-08867a51795c/eton.gif" alt="Screenshot Pullquote" width="236" height="245" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95ab77a6-e320-4bbf-b0e2-6e9027140f62/cnet.gif" alt="Screenshot Pullquote" width="235" height="134" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76086784-75ef-491c-a517-9a5bb954ef63/eguest.gif" alt="Screenshot Pullquote" width="395" height="261" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1a5cec-b5ed-4a44-aed9-be2930aa83c4/bild10.jpg" alt="Screenshot Pullquote" width="297" height="372" /></figure>

## 7\. Quotations as a standalone element

Often quotations are used and designed not inside an article, but as a standalone design element which is given the dominant position in the design. This is often the case in <strong>testimonials</strong> where companies present quotes from their customers and clients to confirm the quality they actually promise. In such cases quotations are usually big, bold and clearly visible.

In testimonials quotes are sometimes "rotated" meaning that among 5-7 testimonials only one is displayed at once.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bc6da5d-ad29-4681-bca8-3ef0e0685880/dweb.jpg" alt="Screenshot Pullquote" width="269" height="338" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3a1c127-eadc-4d4f-93d1-c71ed79a3193/cog.jpg" alt="Screenshot Pullquote" width="326" height="170" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/131e6405-cad0-475f-b57b-211e0fd4e0f3/tony.jpg" alt="Screenshot Pullquote" width="247" height="270" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38a3b468-1fe2-48ed-b9ec-22e587a755f7/listpilot.gif" alt="Screenshot Pullquote" width="276" height="194" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ebd514c-f889-4f6e-b971-cb89e36f4f83/trale.gif" alt="Screenshot Pullquote" width="370" height="274" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07a4a2d2-3f67-4d98-89de-9ec1424d8ad3/45r.jpg" alt="Screenshot Pullquote" width="408" height="132" /></figure>

## 8\. Bonus: Footnotes

In books and scientific documents citations are often provided with a <strong>footnote reference</strong> to the original document. In the Web, where references are commonly just linked to, this technique has never managed to become popular, however footnotes aren't difficult to achieve with pure CSS.

For instance, if you'd like to cite an excerpt from a book, instead of providing the corresponding title and page number you can simply refer to a footnote below the article. Thus, you can avoid overloading your article with too many references. Footnotes, hence, can <strong>make it easier for your readers to read your article</strong> and provide details "on-demand" — only when they are needed.

Sometimes footnotes are also used by authors to provide some remarks to the article (similar to books). However, it is not always reasonable to use footnotes for links. The Web is a dynamic medium and links are extremely powerful - you don't have to send your visitors to the footer of the page first to be able to follow a given link.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2f6c3a8-dd29-4eb5-a2c4-cbae2cd421d3/nznr.jpg" alt="Screenshot" width="491" height="622" /></figure>

Take a look at the following example. Naz Hamid uses both a blockquote (label 2 in the image above) and a footnote in his articles. The reference to the footnote and the footnote itself are interconnected: visitors can click on the reference and jump to the footnote. And in the footnote the "return"-icon allows the user to jump from the footnote to the place in the article where it is referred to. The author uses the footnotes to provide a personal remark on what has been mentioned in the article (labels 1 and 2).

With footnotes you can offer your visitors some traditional, classic layout feeling without overwhelming them with long references to citations you provide.</p>

## Tutorials

<ul>
 	<li><a title="Permanent Link: Simple CSS Blockquotes and Pullquotes" href="https://blogsolid.com/ideas/2007/simple-css-blockquotes-and-pullquotes/" rel="nofollow">Simple CSS Blockquotes and Pullquotes</a></li>
 	<li><a href="https://24ways.org/2005/swooshy-curly-quotes-without-images" rel="nofollow">Swooshy Curly Quotes Without Images </a><br>
<figure><a href="https://24ways.org/2005/swooshy-curly-quotes-without-images" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53fbf71e-a736-46c4-aa01-169a0b8563ea/curly-finished.gif" alt="Screenshot Pullquote" width="521" height="149" /></a></figure>&nbsp;</li>
 	<li><a href="https://www.456bereastreet.com/archive/200609/automatic_pullquotes_with_javascript_and_css/" rel="nofollow">Automatic pullquotes with JavaScript and CSS</a><br>
<figure><a rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92be6bbf-51e4-4ca5-b53a-c0cff2c8756f/jquery.gif" alt="Screenshot Pullquote" width="191" height="97" /></a></figure>&nbsp;</li>
 	<li><a href="https://webservices.blog.gustavus.edu/2007/03/21/automatic-pull-quotes-with-behaviour-and-css/" rel="nofollow">Automatic Pull-quotes with Behaviour and CSS</a></li>
 	<li><a href="https://www.fonts.com/AboutFonts/Articles/fyti/PullQuotes.htm" rel="nofollow">Pull Quotes, Article at fonts.com</a><br>
<figure><a href="https://www.fonts.com/AboutFonts/Articles/fyti/PullQuotes.htm" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad5722a3-b0ee-4b3c-a87f-129426492f1e/fontscom.gif" alt="Screenshot Pullquote" width="206" height="78" /></a></figure>&nbsp;</li>
 	<li><a title="Permanent Link to Better Pull Quotes: Don’t Repeat Markup" href="https://css-tricks.com/better-pull-quotes/" rel="nofollow">Better Pull Quotes: Don’t Repeat Markup</a><br>
<figure><a href="https://www.sitepoint.com/examples/pullquotes/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e3a808f-d6ea-47ed-9eea-d9268d5eeb4c/sitepoint.gif" alt="Screenshot Pullquote" width="218" height="127" /></a></figure>&nbsp;</li>
 	<li><a href="https://www.pearsonified.com/2006/09/snazzy_pullquotes_for_your_blo.php" rel="nofollow">Snazzy Pullquotes for Your Blog</a></li>
 	<li><a href="https://www.htmldog.com/articles/pullquotes/" rel="nofollow">HTML Dog: Pull Quotes</a><br>
<figure><a href="https://www.htmldog.com/articles/pullquotes/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db8d31f-a704-4ba1-ac17-7ef642ab1779/dog.gif" alt="Screenshot Pullquote" width="228" height="225" /></a></figure>&nbsp;</li>
 	<li><a href="https://desktoppub.about.com/cs/pagelayout/ht/pull_quotes.htm" rel="nofollow">How To Use Pull-quotes</a></li>
 	<li><a title="Permanent Location of Making a WordPress Pull Quote" href="https://green-beast.com/blog/?p=189" rel="nofollow">Making a WordPress Pull Quote</a><br>
<figure><a href="https://green-beast.com/blog/?p=189" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b35a2d6d-490b-4803-9626-befe4a96e29b/wordpress.gif" alt="Screenshot Pullquote" width="291" height="147" /></a></figure></li>
 	<li><a href="https://www.brandspankingnew.net/archive/2006/01/footnotes-with-css-and-javascript.html" rel="nofollow">Footnotes with CSS and Javascript</a>
A XHTML+CSS+Javascript solution for displaying and marking up footnotes. There is also an updated <a href="https://www.brandspankingnew.net/specials/footnote_4.html" rel="nofollow">sidenotes version</a> which displays footnotes in the sidebar of a page instead of the footer of the page. Advantages: you don't have to worry about numbering, the footnotes can be edited at their insertion point, you could give users the choice of how footnotes are formatted, or whether they are shown at all.<figure><a href="https://www.brandspankingnew.net/archive/2005/07/format_footnote.html" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a049c92-0747-4c38-b699-b5e02cc56570/footn.jpg" alt="Screenshot Pullquote" width="404" height="126" /></a></figure></li>
</ul>

## Further references

You may also want to take a look at the posts:

*   [Web Design Elements: Examples And Best Practices](https://www.smashingmagazine.com/web-design-essentials-examples-and-best-practices/)
*   [Mind Your En And Em Dashes: Typographic Etiquette](https://www.smashingmagazine.com/2011/08/mind-your-en-and-em-dashes-typographic-etiquette/)
*   [Grid-Based Design: Six Creative Column Techniques at Smashing Magazine](/2008/03/26/grid-based-design-six-creative-column-techniques/) 

Look at the "Escaping Boundaries" section (fourth from the top). Pull-quotes are an example of a design element that presents an opportunity to break out of your established visual flow.

The older version of Andy Rutledge’s Design View used interesting pull-quotes that broke the visual flow of the column.

Doing this places greater emphasis on the pull-quotes than if they were kept within the content of the column.

