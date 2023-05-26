---
title: 'Microformats: What They Are and How To Use Them'
slug: microformats-what-they-are-and-how-to-use-them
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ded98607-127b-47a9-a597-2224f44c9031/microformats.jpg
date: 2007-05-04T15:04:11.000Z
author: vitaly-friedman
description: >-
  Web 2.0 has its positive and its negative sides. Apart from tremendous
  technological improvements, provided by Ajax, semantically organized content
  and the growing popularity of RSS-Feeds, the term "Web 2.0" still hadn't
  managed to assert itself as the renewed Web rather than a new revolutionary
  technology as it is mistakenly being called.
categories:
  - Coding
  - Semantics
---
Web 2.0 has its positive and its negative sides. Apart from tremendous technological improvements, provided by Ajax, semantically organized content and the growing popularity of RSS-Feeds, the term Web 2.0 still hadn't managed to assert itself as the renewed Web rather than a new revolutionary technology as it is mistakenly being called. Here are the microformats. 

<figure><a href="https://microformats.org/about/"><img loading="lazy" decoding="async" title="About Microformats" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1d4dbcb-a865-4275-8ce3-db3a27f87ed2/microformats-04.gif" alt="About Microformats" width="144" height="36" /></a></figure>

Consequence: many renewed techniques, which somehow seem to be related to the "new" Web, aren't fully or properly understood. This results in public misunderstandings and keeps both developers and users away from the use (the improvement) of these techniques.

You may want to take a look at the following related posts:

*   [When One Word Is More Meaningful Than A Thousand](https://www.smashingmagazine.com/2010/07/when-one-word-is-more-meaningful-than-a-thousand/)
*   [<span class="headline">The Importance Of HTML5 Sectioning Elements</span>](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)

{{% feature-panel %}}

One of the new terms on the horizon is <strong>Microformats</strong> (sometimes abbreviated µF or uF) - formats, which make it possible to create meta-content which can be <em>not only read</em>, <em>but</em> also <em>understood</em> by machines (which was the basic idea of <a href="https://en.wikipedia.org/wiki/Semantic_Web">Semantic Web</a>, which is <strong>not</strong> Web 2.0). This post is supposed to give you an idea, <strong>what Microformats actually mean, which advantages they have and how you can use them to enrich your content and make it more visible and understandable for search engines</strong>.</p>

## Things you should know

<figure><a href="https://microformats.org/about/"><img title="About Microformats" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/036f1cec-be8f-4e48-9f15-32e3dad27593/microformats-01.gif" alt="About Microformats" width="445" height="213" /></a></figure>

*   "Designed for humans first and machines second, microformats are a set of simple, open data formats built upon existing and widely adopted standards." [[Official definition](https://microformats.org/wiki/what-are-microformats)]
*   "A microformat is a piece of mark up that allows expression of semantics in an HTML (or XHTML) web page. Programs can extract meaning from a web page that is marked up with one or more microformats." [[Wikipedia](https://en.wikipedia.org/wiki/Microformats)]
*   "With Microformats, you can send & publish things like events, business cards, and product reviews as meaningful XHTML that a person can read in a browser, but a program can import, index and remix as native data." [[Michael McCracken](https://microformats.org/wiki/what-can-you-do-with-microformats)]
*   "Microformats are about using the standards we all know [...] to convey as much semantic meaning as possible. They use current XHTML tags such as `address`, `cite`, and `blockquote` and attributes such as `rel`, `rev`, and `title` to create semantically appropriate blocks of code." [[Primer](https://www.digital-web.com/articles/microformats_primer/)]
*   "Microformats are not a new language, but adapted to current behaviors and usage patterns and is connected with semantic XHTML." [[About](https://microformats.org/about/)]
*   "Principles: solve a specific problem, simple as possible, reuse from widely adopted standards (semantic (X)HTML), modularity / embeddability, decentralized development, content, services. [[What are microformats](https://tantek.com/presentations/2006/07/what-are-microformats/)]
*   "That’s what microformats are, adding semantics to markup to take it from being machine readable to being machine understandable." [[Introduction](https://blog.mozilla.com/faaborg/2006/12/11/microformats-part-0-introduction/)]
*   "There are lots of different microformats, ranging from very fundamental types of information like [contacts](https://microformats.org/wiki/hcard), [locations](https://microformats.org/wiki/adr), and [events](https://microformats.org/wiki/hcalendar), to the slightly more domain specific, like [reviews](https://microformats.org/wiki/hreview) and [resumes](https://microformats.org/wiki/hresume), to the very domain specific, like [wines](https://microformats.org/discuss/mail/microformats-discuss/2006-November/007180.html)."[[Introduction](https://blog.mozilla.com/faaborg/2006/12/11/microformats-part-0-introduction/)]

## Existing Microformats

<figure><a href="https://microformats.org/wiki/"><img title="Microformats List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07c5759-d6ea-4f47-97d1-8b272f52279c/microformats-03.png" alt="Microformats List" width="110" height="99" /></a></figure>

*   [hAtom](https://microformats.org/wiki/hatom) hAtom is a micro format for content that can be syndicated, primarily but not exclusively weblog postings. hAtom is based on a subset of the [Atom](https://www.atomenabled.org/) syndication format.
*   [hCalendar](https://microformats.org/wiki/hcalendar) | [hCalendar Creator](https://microformats.org/code/hcalendar/creator) hCalendar is a simple, open, distributed calendaring and events format, suitable for embedding in (X)HTML, Atom, RSS, and arbitrary XML.
*   [hCard](https://microformats.org/wiki/hcard) | [hCard Creator](https://microformats.org/code/hcard/creator) hCard is a format for representing people, companies, organizations, and places, in semantic XHTML.
*   [hResume](https://microformats.org/wiki/hresume) | hResume Creator hResume is a microformat for publishing resumes and CVs.
*   [hReview](https://microformats.org/wiki/hreview) | [hReview Creator](https://microformats.org/code/hreview/creator) hReview is an open, distributed format, suitable for embedding reviews (of products, services, businesses, events, etc.) in (X)HTML, Atom, RSS, and arbitrary XML.
*   `rel="nofollow"` Is an HTML attribute value used to instruct search engines that a hyperlink should not influence the link target's ranking in the search engine's index. Regarded as a microformat.
*   `rel="tag"` By adding rel="tag" to a hyperlink, a page indicates that the destination of that hyperlink is an author-designated "tag" (or keyword/subject) for the current page. Note that a tag may just refer to a major portion of the current page (i.e. a blog post). e.g. by placing this link on a page, `<a href="https://technorati.com/tag/tech" rel="tag">tech</a>`, the author indicates that the page has the tag "tech".
*   [XFN](https://en.wikipedia.org/wiki/XHTML_Friends_Network) XHTML Friends Network (XFN) is a simple way to represent human relationships using hyperlinks developed by Global Multimedia Protocols Group. XFN enables web authors to indicate their relationship(s) to the people in their blogrolls simply by adding a 'rel' attribute to their `<a href>` tags, e.g.: `<a href="https://jeff.example.org" rel="friend met">`.
*   [XOXO](https://en.wikipedia.org/wiki/XOXO) XOXO (eXtensible Open XHTML Outlines) is an XML format for outlines built from XHTML modularization. Developed by several authors as an attempt to reuse XHTML building blocks instead of inventing unnecessary new XML elements/attributes, XOXO is both based on existing behavior of publishing outlines, lists, and blogrolls on the Web, and as a general outline format for 1:1 processing of fundamental programming language datastructures.
*   [xFolk](https://microformats.org/wiki/xfolk) xFolk is a simple and open format for publishing collections of bookmarks.</p>

## Advantages of Microformats

*   "Now your information is scattered all over the Web, and you have to pick which sites you want to use. Soon: the combination of blogging and microformats is now reversing this model. Now, your information remains in your blog, and the Web sites come to you. For instance, if you want to sell something, you can blog about it using an hListing, and a site like edgeio will find it when it aggregates classified advertisements across the Web." [[Introduction](https://blog.mozilla.com/faaborg/2006/12/11/microformats-part-0-introduction/)]
*   "Microformats enable the publishing and sharing of higher fidelity information on the Web. Small bits of (X)HTML that identify richer data types like people and events in your webpages. Building blocks that enable users to own, control, move, and share their data on the Web." [[What are microformats](https://tantek.com/presentations/2006/07/what-are-microformats/)]
*   "Like CSS, microformats let you to do some interesting things through JavaScript and the DOM. After all, microformats are just a bunch of XHTML." [[Primer](https://www.digital-web.com/articles/microformats_primer/)]
*   Benefits: they are (search) machine-readable, accurate and appropriate metadata, meaningful markup.
*   "So what use would microformats be in a web browser? [...] Future Web browsers are likely going to associate semantically marked up data you encounter on the Web with specific applications, either on your system or online. This means the contact information you see on a Web site will be associated with your favorite contacts application." [[Mozilla Does Microformats](https://readwrite.com/2007/01/01/mozilla_does_microformats_firefox3/)]
*   "The idea is that i.e. as soon as any page that has an hCard on it you can add to your address book, you can sync it with your PDA, your handheld, and it makes contact information, personal information, on the web a lot more useful." [[Evolving the Web](https://adactio.com/articles/1146/)]

## Microformats are already being used!

*   Edgeio.com (Weblog based business as niche for small and large companies), [Rubhub.com](https://www.rubhub.com) (determines relationships between websites and peoples, scenarios: find alternative connections for supplies in producer chains, bookseller, car suppliers, internal contact management within large companies), [Technorati.com](https://www.technorati.com) (indexes hCard, hCalendar, and hReview, and also cumulative data is updated via event-driven pings)
*   Microformats can be used within Firefox Extensions ([Tails](https://addons.mozilla.org/firefox/addon/2240), [Greasemonkey scripts](https://microformats.org/wiki/Greasemonkey) for hCard, hCalendar, xFolks, etc.) and Blogging Extensions (Structured Blogging for Wordpress)

## Articles About Microformats

*   [What are micro formats?](https://microformats.org/) Designed for humans first and machines second, microformats are a set of simple, open data formats built upon existing and widely adopted standards. Learn more about microformats. The official web-page.
*   [Digital Web Magazine - Primer](https://www.digital-web.com/articles/microformats_primer/) Introductory article by Garrett Dimon
*   [Add magic to your site](https://blog.teamtreehouse.com/add-microformats-magic-to-your-site) Heard of the semantic web? Using Microformats everyone can contribute to the richness of the web. John Allsopp explains how.
*   [Evolving the Web](https://adactio.com/articles/1146/) Jeremy Keith - This is a transcript of a panel I sat in on at South by Southwest 2006\. My fellow panelists are Chris Messina and Norm! The moderator is Tantek Çelik.
*   [Introduction](https://blog.mozilla.com/faaborg/2006/12/11/microformats-part-0-introduction/) Microformats: Introduction, Structured Data, The Fundamental, Introducing Operator
*   [Microformats Challenge Web Feeds and Web APIs!](https://duncan-cragg.org/blog/post/microformats-challenge-web-feeds-and-web-apis/) Microformats are subversive: they not only challenge the approach of full-blown Semantic Web approaches, but even question fundamental Web 2.0 building blocks such as Web Feeds and Web APIs.
*   [Microformats](https://myhpi.de/~schapran/pke/) Designed for humans first.by Prof. Dr. Mathias Weske

## Microformats Tools

<figure><a href="https://www.bartelme.at/journal/archive/microformats_icons/"><img title="Microformats Icons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a20d7b92-b050-4771-ae1f-606e20e0f4f5/microformats-00.png" alt="Microformats Icons" width="480" height="90" /></a></figure>

*   [Highlight Microformats with CSS](https://www.hicksdesign.co.uk/journal/highlight-microformats-with-css) Those that use Firefox with the Tails extension, read no further. This is not for you. You have it given to you on a plate, you don’t know how lucky you are. This is for those of us using Camino, Safari or Omniweb.
*   [Dreamweaver Extension](https://www.webstandards.org/action/dwtf/microformats/) Dreamweaver extension (ideally for use with Dreamweaver 8, although should work for MX and above) implements a few simple Insert Bar Objects to help Dreamweaver users to add hCalendar, hCard, rel-license, rel-tag and XFN data to their documents. After installing, you’ll find a new Microformats category on your Insert Bar. Support for more formats is to follow, so check back.
*   [Cheat Sheet](https://suda.co.uk/projects/microformats/cheatsheet/) This microformats cheat sheet lists the properties by format and also lists each format and the hierarchy. This includes elemental microformats, compound microformats and some of the standard design patterns used.
*   [Icons](https://www.bartelme.at/journal/archive/microformats_icons/) The starter set contains icons for hCal, hResume, hCard, XFN and a generic TAG icon.</p>

## Tutorials, Introductions

*   [Tutorials on Microformats](https://www.xfront.com/microformats/) This series of articles deals with numerous aspects of Microformats, including basic theory and purpose of Microformats, hCard, hCalendar, AHAH, hReview, xFolk, hResume, XOXO and hAtom.

Mike Jolley explains step-by-step, what Microformats are, how they can be integrated in web-pages and how you can enhance the efficicency of your content using them.

*   [Pairing Wine and Microformats](https://www.simplebits.com/notebook/2006/06/10/wineformats.html) Microformats in Practice: Dan Cederholm about the use of Microformats in Cork'd.
*   [Wikipedia: Microformats](https://en.wikipedia.org/wiki/Microformat) The Wikipedia Entry.
*   Using Microformats in WordPress There are two approaches you can take. One: Manually pasting relevant microformat code created via microformat creators. Step-by-step instructions are as follows.</p>

## Blogs & Wikis

*   [Microformats.org](https://microformats.org/) Designed for humans first and machines second, microformats are a set of simple, open data formats built upon existing and widely adopted standards. Learn more about microformats.
*   [Microformats Wiki](https://microformats.org/wiki/Main_Page) What are microformats? What can you do with them?

