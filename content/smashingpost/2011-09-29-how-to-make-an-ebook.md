---
title: 'How To Make An eBook'
slug: how-to-make-an-ebook
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/907de0c2-bed4-4723-847d-ca00c77b9b28/templates-email-mobile-illu.jpg
date: 2011-09-29T10:58:08.000Z
author: jason-mark
summary: >-
  In this post, Jason Mark focuses on the eBook formats for EPUB, Kindle and PDF. What kind of book makes the best eBook, coding by hand, the future of EPUB and other resources.
description: >-
  In this post, Jason Mark focuses on the eBook formats for EPUB, Kindle and PDF. What kind of book makes the best eBook, coding by hand, the future of EPUB and other resources.
categories:
  - Coding
  - Workflow
  - Techniques
---

Making an eBook is easy, regardless of your coding experience. This is good, because 99.9% of your time should be spent on writing and getting your book out there, rather than on technology.

Any electronic book can be called an eBook, but because over 90% of all eBooks are read on Amazon’s Kindle, Apple’s iOS devices (iPad, iPhone and iPod) and the Barnes &amp; Noble Nook, I’ll focus on the formats for those platforms:

1.  **EPUB** This is an open standard adopted by Apple (iOS), Barnes & Noble (Nook) and many other makers of eBook readers (such as Sony). <del datetime="2011-09-30T08:19:14+00:00">Thankfully, Amazon has said that its next Kindle will also support EPUB, but the newest version of Kindle doesn’t support it.</del> (**Update**: Unfortunately, Amazon has decided NOT to support EPUB in the next version of their Kindle.)
2.  **Kindle** This is a proprietary format that Amazon uses for its Kindle, which is a modification of the Mobipocket format.
3.  **PDF** PDF is inherently made for print and doesn’t display well on digital devices. But if you really need to get data out to an iOS or Android device _now_, then it’s a useful format. <del datetime="2011-10-04T09:20:03+00:00">We’ll have to wait one more generation for the Kindle to support it</del>. (**Update**: Kindle DOES support PDF.)

**Aside to geeks:** The current version of EPUB is based on XHTML 1.1, which was officially proposed in 1999. That was the year when Internet Explorer 5.0 was released and grabbed over 50% of browser market share from Netscape Navigator. This is great because XHTML is an open standard that many developers know; unfortunately, it’s very old.

{{% feature-panel %}}

## What Kind Of Book Makes The Best eBook?

EPUB was truly designed to display text, possibly with some inline images. While creating an EPUB illustrated children’s book, comic book, travel book or cookbook is possible, it’s a lot more work and doesn’t work very consistently across platforms. A good rule of thumb is that eBooks are best for books with a lot of words (think New York Times bestseller list).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9805abe-029b-4e99-a508-f6f8509682eb/illustrated-epub-books.jpg"><img class="99484" title="illustrated-epub-books" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9805abe-029b-4e99-a508-f6f8509682eb/illustrated-epub-books.jpg" alt="How a picture book should look and how it looks in EPUB. Novels don’t have this problem because images don’t matter." width="550" height="210" /></a><figcaption>eBooks don’t handle pictures well.</figcaption></figure>

When deciding whether your book is a good candidate for an eBook, keep in mind that the “killer feature” of eBooks, surprisingly, is their ability to increase in font size. This means that every book becomes a large-type book, which is why baby-boomers have driven the adoption of digital books over the past few years.

Also keep in mind that more than half of all eBook-reading devices are black and white, which is another reason to steer clear of picture-based books.

These demographics and format limitations will change over time. But for now, my recommendation is to **make your first eBook a text-based one**.

**Aside to geeks:** If you’re interested in making a picture book for iOS devices and aren’t afraid of code, check out Elizabeth Castro’s <a href="https://www.pigsgourdsandwikis.com/2011/02/fixed-layout-epubs-for-ipad-and-iphone.html">excellent guide</a> on how to code a fixed-layout EPUB file.

## Making Your First eBook

The easiest way to make an eBook is to outsource it. A number of services, such as Lulu and Smashwords, will translate your Word document into an EPUB fairly inexpensively. These services have relationships with Amazon and Apple (as well as other digital bookstores) and will not only create your digital eBook but submit it to these bookstores for a small fee. For more information on choosing a service, see Christine Mark’s <a href="https://www.gravityswitch.com/blog/guide-to-comparing-services-for-publishing-ebooks-to-ipad_119/">guide on choosing an EPUB publisher</a>.

If you want to sell your book only in Amazon’s Kindle Store, you can convert your Word file for free by submitting it yourself to Amazon’s <a href="https://kdp.amazon.com">Kindle Direct Publishing</a> (KDP). Creating an account is free, and the service is easy to use.

If you’re mostly interested in Apple’s eco-system, then you probably already have a copy of Pages on your machine (if not, you can get it for $20). Pages is Apple’s version of Microsoft Word and has a simple and effective EPUB export option. To create your book, simply make the first page your book’s cover, use section breaks between chapters, and then select <code>File</code> → <code>Export</code> → <code>EPUB</code>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/052e21a2-4b2d-426c-900d-219b231aec31/pages-to-epub-graphic.jpg"><img class="99489" title="pages-to-epub-graphic" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/052e21a2-4b2d-426c-900d-219b231aec31/pages-to-epub-graphic.jpg" alt="Using Pages to make an EPUB book" width="550" height="352" /></a><figcaption>In my experience, Pages’ EPUB exporting is rock-solid.</figcaption></figure>

If you don’t have a Mac or want to convert to more formats, your best choice of software is <a href="https://calibre-ebook.com/">Calibre</a>. Calibre is relatively easy to use and does a good job of converting from many standard formats (including Microsoft Word) to the top eBook formats (EPUB and the Kindle’s Mobipocket format). You can download Calibre for free. Alternatively, if you need to convert only to Kindle, Amazon provides free conversion software called <a title="Amazon Kindlegen" href="https://www.amazon.com/gp/feature.html?ie=UTF8&amp;docId=1000234621">Kindlegen</a>.

Another common choice for building eBooks is InDesign, but I’d recommend that you steer clear from it until you have a few eBooks under your belt. Even though it technically can export to EPUB and Kindle formats, it’s a bit clunky and adds a lot of crud. More importantly, InDesign was built from the ground up to handle print, so it encourages you to think in print metaphors, which don’t always apply to eBooks and which will lead to layout problems. In our experience, programming your own EPUBs by hand is easier. Even still, I don’t recommend it…

## Coding By Hand

If everything said above sounds too easy and you’re looking for a challenge, another option is to code your EPUB by hand. This feels like programming in a time warp. EPUB is built on such an outdated version of XHTML that half the time you’ll be reminding yourself that *everything* in the EPUB must be declared in the manifest file (really?), while the other half of the time you’ll be recalling how you used to program HTML in the ’90s.

If you’re still not convinced and have a pressing desire to learn how to code an EPUB by hand, you have two options:

1.  Grab an EPUB from the Web that doesn’t have any DRM in it. Change the extension from _.epub_ to _.zip_ and unZip it (you may need to use Stuffit Expander if you’re on a Mac). Now you’re free to hack away at the file and see what happens. Keep in mind that *every* file in the EPUB must be in the manifest (_package.opf_). There are a couple of books you can pick apart to get started (including my best-selling children’s book, which you can get for free on my website or buy from the Apple bookstore to show your love).
2.  Check out “[EPUB Straight to the Point](https://www.elizabethcastro.com/epub/)” by Elizabeth Castro, and she’ll walk you through it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6d38ea-85da-49ae-ae53-69f1c5be7662/epub-file-structure.png"><img class="112586" title="EPUB File Structure" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6d38ea-85da-49ae-ae53-69f1c5be7662/epub-file-structure.png" alt="" width="181" height="267" /></a><figcaption>The typical structure of an EPUB file.</figcaption></figure>

The *container.xml* file, MIME type, and folder structure are pretty standard for all books. Images can be in PNG, JPEG, GIF or SVG format. I usually stick with PNG, with JPEG as a fall-back.

The *epb.ncx* file is the table of contents and is pretty straightforward.

The *epb.opf* file is the manifest where you set the meta data (title, author, ISBN, etc.), but it’s also where *every other* file in the EPUB is declared. Every image, HTML or CSS file must be listed here. It’s a pain in the butt and one reason why I personally avoid hand-coding EPUB if possible.

The CSS is pretty much what you’d expect, although a very limited subset.

The HTML is also very straightforward. Below is a sample of the HTML that Apple Pages spit out for my book. As you can see, it’s not very pretty (<code>&lt;div class="s6"&gt;</code> instead of a simple <code>&lt;h1&gt;</code>), but it’s functional and easy to understand.

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;!DOCTYPE html

PUBLIC "-//W3C//DTD XHTML 1.1//EN"

"https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd"&gt;

&lt;html xml:lang="en" xmlns="https://www.w3.org/1999/xhtml"&gt;

&lt;head&gt;

&lt;title&gt;1 Moving Day | Ghost Hunters - Book 1 The Haunted House&lt;/title&gt;

&lt;link rel="stylesheet" href="css/book.css" type="text/css"/&gt;

&lt;meta http-equiv="Content-Type" content="application/xhtml+xml; charset=utf-8"/&gt;&lt;meta name="EPB-UUID" content="3B0A6B89-F890-4843-AA2A-01C27CE8D573"/&gt;

&lt;/head&gt;

&lt;body&gt;

&lt;div style="white-space:pre-wrap"&gt;

&lt;div&gt;CHAPTER 1&lt;/div&gt;

&lt;div&gt;Samantha and Dylan looked eagerly out the car window. Today was the day that they were moving to their new house. They were both excited, but sometimes a look of worry would cross Sam’s face.&lt;/div&gt;

&lt;/div&gt;

&lt;/body&gt;

&lt;/html&gt;</code></pre>

If you are creating your own EPUB, be sure to validate it with <a href="https://threepress.org/document/epub-validate/">Threepress’ validator</a>, and consider using <a href="https://calibre-ebook.com/">Calibre</a> to convert your EPUB to a Kindle-friendly format.

{{% ad-panel-leaderboard %}}

## The Future Of EPUB

EPUB 3.0 holds a lot of promise and includes the following changes (many of which Apple has already adopted):

*   Support for HTML5 (yay!) and CSS 2.1;
*   Various structural changes to file names and locations;
*   Support for embedded fonts, audio and video, as well as media overlays and triggers and scripts.

Unfortunately, EPUB 3.0 doesn’t support illustrated books, so we can expect to see some fragmentation as Apple and other vendors innovate around these limitations.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856464c4-fea6-40fe-9740-dceeadb7e95f/fixed-layout-books.01"><img class="99521" title="fixed-layout-books.01.jm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856464c4-fea6-40fe-9740-dceeadb7e95f/fixed-layout-books.01" alt="" width="550" height="250" /></a><figcaption>Olivia was one of the first fixed-layout EPUB books released by Apple. Also pictured is the bestselling fixed-layout EPUB book ‘The Girl Who Wouldn’t Wash Her Hands’.</figcaption></figure>

With the next version of Kindle supporting EPUB, we’ll see over the next year or two whether we wind up with an “Apple EPUB” and an “Amazon EPUB,” or a “pure” EPUB format. Ultimately, the answer will depend on how quickly the International Digital Publishing Forum (IDPF) can finalize its standards.

Of course, all of this speculation about the future is somewhat theoretical. If you have a book to publish now, my suggestion is don’t worry about the future; just dive right in and make it. And let me know in the comments how it turned out and what worked best for you.

## Other Resources

You may be interested in the following articles and related resources:

*   “[Fixed-Layout EPUBs for iPad and iPhone](https://www.pigsgourdsandwikis.com/2011/02/fixed-layout-epubs-for-ipad-and-iphone.html)” Elizabeth Castro’s excellent guide on how to code a fixed-layout EPUB.
*   “[Guide to Comparing Services for Publishing eBooks to iPad](https://www.gravityswitch.com/blog/guide-to-comparing-services-for-publishing-ebooks-to-ipad_119/)” Christine Mark’s guide on choosing an EPUB publisher.
*   [Amazon’s Kindle Direct Publishing](https://kdp.amazon.com) The fast and easy way to self-publish your books for sale in the Kindle Store.
*   [Calibre eBook Management](https://calibre-ebook.com/) Calibre is a free and open-source eBook library-management application, developed by eBook users for eBook users.
*   “[EPUB Straight to the Point](https://www.elizabethcastro.com/epub/)” Elizabeth Castro’s guide to creating eBooks for the iPad and other eReaders.
*   “[Validate EPUB Documents](https://threepress.org/document/epub-validate/)” Threepress Consulting offers a convenient way to validate your EPUBs before publishing.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [50 Free Resources That Will Improve Your Writing Skills](https://www.smashingmagazine.com/2009/06/50-free-resources-that-will-improve-your-writing-skills/)
*   [The Search For Alternative Collaborative Online Writing Tools](https://www.smashingmagazine.com/2014/04/after-editorially-alternative-collaborative-online-writing-tools/)

{{< signature "al, mrn" >}}
