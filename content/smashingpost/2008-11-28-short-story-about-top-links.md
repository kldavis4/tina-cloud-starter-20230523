---
title: A Short Story About "Back To Top" Links
slug: short-story-about-top-links
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e3ce4ed-c2dd-427f-ab67-7de6461cc5e2/top.jpg
date: 2008-11-28T00:11:07.000Z
author: sven-lennartz
description: >-
  Often it is the **close attention to small details** that makes a design
  outstanding. During the development of a website, designers tend to quickly
  forget about small details and focus on major design elements, such as
  navigation, typography and layout. If done properly, the result is usually a
  solid, impressive and highly professional design that communicates
  information. However, it is not memorable. The reason is that such designs
  often do not have a memorable voice: they may look visually appealing, but
  they don't provide a vivid anchor for users to remember a website after
  leaving it.
categories:
  - UX
  - Web Design
  - Navigation
  - Usability
---
Often it is the <strong>close attention to small details</strong> that makes a design outstanding. During the development of a website, designers tend to quickly forget about small details and focus on major design elements, such as navigation, typography and layout. If done properly, the result is usually a solid, impressive and highly professional design that communicates information. However, it is not memorable. The reason is that such designs often do not have a memorable voice: they may look visually appealing, but they don't provide a vivid anchor for users to remember a website after leaving it. 

In this way, little details are important because they can help the design stand out. Have you ever thought about the design of your shopping cart? What about the design of tags, date stamps, "Previous" and "Next" links? All of these small details are not crucial for website navigation, but they add up to a more user-friendly, more convenient and sometimes also more sophisticated design. And this is why we have focused the attention of our readers on such things as <a href="https://www.smashingmagazine.com/2008/11/image-caption-design-simply-elegant-or-boldly-graphic/">image captions</a>, <a href="https://www.smashingmagazine.com/2008/06/block-quotes-and-pull-quotes-examples-and-good-practices/">block quotes</a>, <a href="https://www.smashingmagazine.com/2007/11/pagination-gallery-examples-and-good-practices/">pagination</a>, <a href="https://www.smashingmagazine.com/2008/08/the-hr-contest/">&lt;hr&gt; lines</a> and <a href="https://www.smashingmagazine.com/2007/11/tag-clouds-gallery-examples-and-good-practices/">tag clouds</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01072204-91cd-466f-b964-daaff211a41d/dawghouse.jpg" alt="Screenshot - Top Link" width="293" height="103" />

In this post, we showcase the <strong>design of "Back to top" links</strong>, a forgotten and rarely used link that helps users jump to the top of a given page. A visitor can achieve this effect by pressing the "Home" button on his or her keyboard; however, not every user is aware of that shortcut, and most probably use the vertical scroll bar in the browser for that purpose. As designers, we can help our users out by adding a stand-alone "top" link to our designs.</p>

## When "Back to Top" Links are Useful

Unfortunately, this friendly service -- letting users jump to the top of the page -- is offered very rarely. Most designers don't include it, which is why it took us over 5 weeks to collect at least a few dozen nice examples for this post.

{{% feature-panel %}}

In fact, "Back to top" links are not always useful. For example, they may be unnecessary for websites that have rather short pages or articles. In such cases, there is no need for users to jump to the head of the page, because the whole page is completely visible anyway; if a "top" link is included on such pages, clicking on it will produce no effect, which is rather irritating. This is another reason why many designers don't use it: the variety of currently available screen resolutions makes the "top" link unusable and unnecessary. That's why using "Back to top" links for rather short pages is not a good idea.

However, <strong>websites with long pages</strong> can offer visitors a nifty feature that saves time and avoids the need for vertical scrolling with the mouse.</p>

## Where Should the "Top" Link be Placed?

The most obvious and common place for a "Back to top" link is the footer. This is where it belongs and should be placed. We weren't able to identify a common design scheme for the alignment of the "Back to top" link. Some designers place it on the left side of the footer, others place it in the middle and yet others put it on the right side of the footer. It is also very common to place the "top" link on the left-hand side of the content area, directly under the article.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e75f507-7aa5-4832-a352-947c1a60fdc1/wannabee.gif" alt="Screenshot - Top Link" width="311" height="117" /><br>
<em>Meet the friendly "top" link: it is often placed in the footer of the page and almost always appears very modest and almost bashful.</em>

"Back to top" links are also often used in FAQs, help sections and site maps, where they help divide chapters or paragraphs and provide users with a quick way to jump to the beginning of the page, where the main navigation is placed.</p>

## How to Create a "Top" Link?

To point the link to the top of the page, in most cases it is enough to define an empty anchor and put it right after the &lt;body&gt; tag:
<pre class="html">&lt;div id="footer"&gt;
&lt;!-- footer goes here --&gt;

&lt;a href="#"&gt;top&lt;/a&gt;

&lt;/div&gt;
</pre>

However, older browsers and, in particular, legacy browsers have problems interpreting this markup. An alternate solution is to use a real anchor that is explicitly defined and placed right after the &lt;body&gt; tag:
<pre class="html">&lt;body&gt;

	&lt;a name="top"&gt;&lt;/a&gt;

	&lt;!-- content goes here --&gt;

	&lt;a href="#top"&gt;top&lt;/a&gt;

&lt;/body&gt;
</pre>

<strong>Update</strong>: another method that avoids unnecessary markup and therefore should be preferred is to use the ID of the wrapper or header for the same purpose. For instance, if you use the div-container with the ID "wrapper", you may use the following markup:
<pre class="html">&lt;body&gt;
	&lt;div id="wrapper"&gt;

	&lt;!-- content goes here --&gt;

	&lt;a href="#wrapper"&gt;back to top&lt;/a&gt;

	&lt;/div&gt;
&lt;/body&gt;
</pre>

Of course, the link itself doesn't have to be text; it can also be an image, a button or any other element of your choice (using images may have some usability issues -- see below).</p>

## Wording

Never mind what phrase you actually use: you just need to <strong>make sure that visitors understand the function of the link</strong> and aren't irritated by it. For instance, it's probably not a good idea to use the word "Return" because it is not immediately clear if the user will be taken to the home page, the previous page in the browser's history or the top of the page.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c4748cf-d50f-4ead-be25-422a22e877d3/webleed.png" alt="Screenshot - Top Link" width="220" height="90" />

<strong>Use clear and concise terms</strong>, such as "Go to top," "Back to top," "Return to top" or "Jump to top." Sometimes a harmless "Up" is used. However, we're not sure if that's actually a good idea. Probably not.</p>

## Problems and Disadvantages

Some usability experts and even the Yoda of usability, Jakob Nielsen, <a href="https://www.cs.tut.fi/~jkorpela/www/totop.html">reject the "top" link</a> unanimously. According to them, in-page links should be avoided at all because the scroll bar suffices completely, and additional options can be irritating and unnecessary. However, they agree that "Back to top" links may be useful if pages are extremely long, which should be avoided anyway.

One major problem with "top" links is that they have an impact on the browser's navigation buttons and as such <strong>pollute the browsing history</strong>. Because "top" links are anchors just like any other links, clicking on the browser's "Back" button will take users to the foot of the page they are currently viewing, not to the previous page. On top of that, accessibility experts claim that "Back to top" links may disrupt the use of speech-based user agents, that the "top" concept is vague and that "Back to top" links are not used consistently across websites.

## "Back to Top" Link vs. "Home" Link

In our search for interesting "Back to top" examples, we stumbled across some solutions in which designers used images to allow users to jump to the top of the page. However, it is worth mentioning that images should make it clear to users that the link leads not to the home page of the website but to the top of the page. "Home links" are not "Back to top" links, and "Back to top" links are not "Home links". If you decide to use such links in your design, make sure that visitors can understand the difference immediately.

<em>Mistake: "Home" instead of "top"</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d85e9d5-8c0a-4486-ab86-678a6f28e6ae/wild.jpg" alt="Screenshot - Top Link" width="304" height="208" /><br>
<em>Home, sweet home...</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6279c7ac-16fc-4864-bdaa-91fe536f2038/inicio.jpg" alt="Screenshot - Top Link" width="401" height="118" /><br>
<em>Back to the home page in Spanish</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8437c045-1218-48ac-aac3-7fab14f62304/lucy.jpg" alt="Screenshot - Top Link" width="397" height="103" /><br>
<em>Another "home" example in the footer.</em>

<span class="removed_link" title="https://www.fuelyourcreativity.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e2342ef-62e1-4d4f-95d1-2050a779924f/ade.gif" alt="Screenshot - Top Link" width="324" height="110" /></span>
<em>The icon on the right-hand side is not clickable: it could be used to lead to the home page, but not the top of the page.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49819dc2-21ec-41aa-8282-95e5a464417c/diab.jpg" alt="Screenshot - Top Link" width="324" height="110" /><br>
<em>Same here: the illustration is not clickable.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2648131c-7a26-49d4-af91-3e8caf6a8428/wef.jpg" alt="Screenshot - Top Link" width="324" height="110" /><br>
<em>And here, too.</em>

## "Back to Top" Links Showcase

Here are some more examples of "Back to top" links. It took a while to collect them. Hopefully, they'll serve as a good source of inspiration for some of our readers.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b00d71b-e280-48e2-ac5f-6513578ca10c/verhoef.jpg" alt="Screenshot - Top Link" width="293" height="104" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9144c994-3529-4919-926d-b57411619499/chigarden.gif" alt="Screenshot - Top Link" width="293" height="132" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01072204-91cd-466f-b964-daaff211a41d/dawghouse.jpg" alt="Screenshot - Top Link" width="293" height="103" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8596788f-f03a-4a13-aa66-679912fd5307/moust.gif" alt="Screenshot - Top Link" width="293" height="100" /><br>
<em>An animated "Back to top" link</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48de8afe-1e82-497b-ac4d-5ba7f4eb9359/taufiq.jpg" alt="Screenshot - Top Link" width="324" height="146" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b2e1970-0144-4e3e-adfc-3ea8369026ac/decatur.gif" alt="Screenshot - Top Link" width="324" height="88" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98e0e2bb-c178-46ec-a9ca-723fceddce88/digital.gif" alt="Screenshot - Top Link" width="324" height="95" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/041990cf-19b6-43fa-8b04-369771422a8a/slivo.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32097c5e-11d5-475e-a15e-0b929755dd75/brady.jpg" alt="Screenshot - Top Link" width="324" height="122" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b585c21-4aa8-4cb3-b0dc-5aaa9c78914e/heba.jpg" alt="Screenshot - Top Link" width="324" height="151" /><br>
<em>A link as part of the navigation. Looks good but may be a little irritating at first glance.</em>

<span class="removed_link" title="https://www.nue-media.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c72ba9-18b9-407f-ac3c-1f582129d904/slide.jpg" alt="Screenshot - Top Link" width="324" height="110" /></span>
<em>The "top" icon here follows the scroll bar vertically.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cdf81e7-5d4e-4a0b-b53e-090d47e17fcd/blue.jpg" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c83a1594-bcd8-44b3-a398-671d510b0f3b/js.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77e16583-6d37-4047-b6ca-2e5aa15e7a78/oben.jpg" alt="Screenshot - Top Link" width="279" height="205" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56351b8a-9767-41f3-b5cc-07f11b868e8a/bt.jpg" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71186d1e-2711-44c8-a2d2-a26142fe9dd7/strange.gif" alt="Screenshot - Top Link" width="324" height="110" /><br>
<em>We don't know why the remote control is placed there: it is not clickable, but it could be.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba8128fa-05e8-4962-b15c-5ee9793021ef/cooper.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0497cca-7f54-4f5d-abb7-a4b1270c7052/dan.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb7aad68-91b0-4e06-91a2-77f9d41aa53b/ilt.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1aba35f-b2e9-443b-b266-f8be8e6e8e64/alb.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97f46401-9e96-40e7-86a9-5225b56ba1a8/gap.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fb3b867-0cfb-44ce-b9ac-3fb579bb5bfe/des.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7d18909-d596-4bf3-a389-21353234f749/bain.gif" alt="Screenshot - Top Link" width="324" height="110" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68350155-aa52-4edc-948b-c9499393e637/ollie.jpg" alt="Screenshot - Top Link" width="324" height="110" />

## Sources and Resources

*   [Replicating Browser Behavior: The Top Link](https://green-beast.com/blog/?p=177 "Permanent Location of Replicating Browser Behavior: The Top Link")
*   [Nielsen: Within-Page Links for AJAX, "Return to Top", Skip Links](https://www.useit.com/alertbox/within_page_links_comments.html)

{{< signature "al" >}}

<script src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6de57c0f-e4f7-4cb5-bfaf-13bafbfa6557/shcore.js" type="text/javascript"></script><script src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17db2d31-0879-4c1e-a62b-1b3593ef2ddc/shbrushxml.js" type="text/javascript"></script><script class="javascript" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a398a4c-3397-4504-8e06-a64d1cc1b99b/shbrushcss.js"></script><script class="javascript" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8279b8cd-2497-4f3d-bd55-e95d5ed33126/shbrushjscript.js"></script><script type="text/javascript">// <![CDATA[
dp.SyntaxHighlighter.ClipboardSwf = "https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40361c9f-c7b3-4c31-ae48-e38f13d1c9a4/clipboard.swf";dp.SyntaxHighlighter.HighlightAll("code");
// ]]></script>

