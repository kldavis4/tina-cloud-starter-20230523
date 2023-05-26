---
title: Designing For Print With CSS
slug: designing-for-print-with-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c13eeb44-35bc-4a1b-9a86-08ed9899ee29/our-cats-print-css.png
date: 2015-01-07T23:12:57.000Z
author: rachel-andrew
description: >-
  If you mention printing with CSS to many people who work on the web, [print
  style
  sheets](https://www.smashingmagazine.com/2013/03/08/tips-and-tricks-for-print-style-sheets/)
  are the use that comes to mind. We are all well used to creating a style sheet
  that is called upon when a web document is printed. These style sheets ensure
  that the print version is legible and that we don’t cause a user to print out
  huge images.
categories:
  - Coding
  - Tools
  - CSS
  - Techniques
  - Print
---
If you mention printing with CSS to many people who work on the web, print style sheets are the use that comes to mind. We are all well used to creating a style sheet that is called upon when a web document is printed. These style sheets ensure that the print version is legible and that we don’t cause a user to print out huge images. However, CSS is also being used to format books, catalogs and brochures — content that may never have been designed to be a web page at all.

In this article, we’ll take a look at the CSS modules that have been created not for use in web browsers, but to deal with printed and paged media. I’ll explain how the selectors, properties and values that they introduce work. I’ll finish up with a working example that you can use as a starting point for your own experiments. For that example, we’ll need a user agent that supports this specialized CSS. I’ll be using Prince, which is a commercial product. However, Prince has a free version that can be used for non-commercial use, making it a good tool to try out these examples.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing For Print With CSS](https://www.smashingmagazine.com/2015/01/designing-for-print-with-css/)
*   [5 Powerful Tips And Tricks For Print Style Sheets](https://www.smashingmagazine.com/2013/03/tips-and-tricks-for-print-style-sheets/)
*   [Web Design Industry Jargon: Glossary and Resources](https://www.smashingmagazine.com/2009/05/web-design-industry-jargon-glossary-and-resources/)
*   [Taking Pattern Libraries To The Next Level](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)

## Why HTML And CSS Make Sense For Print

It may seem a bit strange that content not particularly destined for the web should be maintained as HTML and formatted with CSS. It seems less strange when you realize that popular <a href="https://www.smashingmagazine.com/2011/09/how-to-make-an-ebook/">eReader formats such as EPUB and MOBI</a> are HTML and CSS under the hood. In addition, even if the entirety of a manuscript or catalog isn’t to be published on a website, some of it likely will be. HTML becomes a handy format to standardize on, far easier to deal with than having everything in a Word document or a traditional desktop publishing package.

{{% feature-panel %}}

## The Differences Between CSS For The Web And For Print CSS

The biggest difference, and conceptual shift, is that printed documents refer to a page model that is of a fixed size. Whereas on the web we are constantly reminded that we have no idea of the size of the viewport, in print the fixed size of each page has a bearing on everything that we do. Due to this fixed page size, we have to consider our document as a collection of pages, paged media, rather than the continuous media that is a web page.

Paged media introduces concepts that make no sense on the web. For example, you need to be able to generate page numbers, put chapter titles in margins, break content appropriately in order that figures don’t become disassociated from their captions. You might need to create cross-references and footnotes, indexes and tables of content from your document. You could import the document into a desktop publishing package and create all of this by hand, however, the work would then need redoing the next time you update the copy. This is where CSS comes in, whose specifications are designed for use in creating paged media.

Because the specifications are designed for paged media, we won’t be considering browser support in this article — it wouldn’t make a lot of sense. Later on, we’ll look at a user agent designed to turn your HTML and CSS into a PDF using these specifications.</p>

## The Specifications

Much of the CSS you already know will be useful for formatting for print. Specifically for print, we have the "<a href="https://www.w3.org/TR/css3-page/" rel="nofollow">CSS Paged Media Module</a>" and the "<a href="https://www.w3.org/TR/css-gcpm-3/" rel="nofollow">CSS Generated Content for Paged Media Module</a>" specifications. Let’s look at how these work.</p>

### The @page Rule

The <code>@page</code> rule lets you specify various aspects of a page box. For example, you will want to specify the dimensions of your pages. The rule below specifies a default page size of 5.5 by 8.5 inches. If you intend to print a book, perhaps by a print-on-demand service, then finding out the sizes you can use is important.</p>

<pre><code class="language-css">
@page {
  size: 5.5in 8.5in;
}
</code></pre>

In addition to specifying sizes with length values, you may also use paper size keywords, such as "A4" or "legal."

<pre><code class="language-css">
@page {
  size: A4;
}
</code></pre>

You may also use a keyword to specify the page’s orientation — "portrait" or "landscape."

<pre><code class="language-css">
@page {
  size: A4 landscape;
}
</code></pre>

### Understanding the Page Model

Before going any further, we should understand how the page model for paged media works, because it behaves somewhat differently to how things work on screen.

The page model defines a page area and then 16 surrounding <a href="https://www.w3.org/TR/css3-page/#margin-boxes" rel="nofollow">margin boxes</a>. You can control the size of the page area and the size of the margin between the edge of the page area and the end of the page itself. The table in the specification explains very well how these boxes are sized.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05d0cb51-22ec-4eaf-93c0-222f16de6136/1-image-margin-boxes-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8d8de59-54e3-43f3-9a0e-da9bc17522d6/1-image-margin-boxes-opt.jpg" alt="print css" width="500" height="372" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05d0cb51-22ec-4eaf-93c0-222f16de6136/1-image-margin-boxes-large-opt.jpg">See large version</a>)</figcaption></figure>

The page area is the space on the page into which your page’s content will flow. When it runs out of room, another page will be created. The margin boxes are used only for CSS-generated content.</p>

### Left and Right Page Spreads

Another aspect of the page model is that it defines pseudo-class selectors for the left and right pages of your document. If you look at any printed book you have on hand, you’ll probably see that the margin’s size and the margin’s content are different on the left and right pages.

We can use these selectors to define different margin sizes for our pages.</p>

<pre><code class="language-css">
@page :left {
  margin-left: 3cm;
}

@page :right {
  margin-left: 4cm;
}
</code></pre>

Two other pseudo-class selectors are defined. The <code>:first</code> selector targets the first page of a document.</p>

<pre><code class="language-css">
@page :first {

}
</code></pre>

The <code>:blank</code> pseudo-class selector targets any page that is "intentionally left blank." To add this text, we can use generated content that targets the top-center margin box.</p>

<pre><code class="language-css">
@page :blank {
  @top-center { content: "This page is intentionally left blank." }
}
</code></pre>

### Generated Content and Paged Media

In the last example, we used CSS-generated content to add the text to the top-center margin box. As you will discover, generated content is vitally important to creating our book. It’s the only way things can be added to our margin boxes at all. For example, if we want to add the title of the book to the bottom-left margin box of right-hand pages, we would do this using generated content.</p>

<pre><code class="language-css">
@page:right{ 
  @bottom-left {
    margin: 10pt 0 30pt 0;
    border-top: .25pt solid #666;
    content: "My book";
    font-size: 9pt;
    color: #333;
  }
}
</code></pre>

### Page Breaks

Also part of the "Paged Media" specification is information about how to control page breaks. As already described, once the content fills a page area, it will move onto a new page. If a heading has just been written to the page, you might end up with a page that finishes with a heading, with the related content beginning on the next page. In a printed book, you would try to avoid this situation. Other places you might want to avoid a break are in the middle of a table and between a figure and its caption.

Starting a new chapter of a book with an <code>h1</code> heading is common. To force this heading to always be the beginning of a page, set <code>page-break-before</code> to <code>always</code>.</p>

<pre><code class="language-css">
h1 {
  page-break-before: always;
}
</code></pre>

To avoid breaks directly after a heading, use <code>page-break-after</code>.</p>

<pre><code class="language-css">
h1, h2, h3, h4, h5 {
  page-break-after: avoid;
}
</code></pre>

To avoid breaking figures and tables, use the <code>page-break-inside</code> property.</p>

<pre><code class="language-css">
table, figure {
  page-break-inside: avoid;
}
</code></pre>

### Counters

Books are all about numbering things — pages, chapters, even figures. We can actually add these numbers via CSS, saving us from having to renumber everything because we decided to, say, add a new figure partway through a chapter. We do this using <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Counters" rel="nofollow">CSS counters</a>.

The obvious place to start is with page numbers. CSS gives us a predefined page counter; it starts at 1 and increments with every new page. In your style sheet, you would use this counter as the value of generated content, to put the page counter in one of your margin boxes. In the example below, we are adding page numbers to the bottom-right of right-hand pages and the bottom-left of left-hand pages.</p>

<pre><code class="language-css">
@page:right{
  @bottom-right {
    content: counter(page);
  }
}

@page:left{
  @bottom-left {
    content: counter(page);
  }
}
</code></pre>

We’ve also created a counter named <code>pages</code>. This counter will always be the total number of pages in your document. If you want to output "Page 3 of 120," you can.</p>

<pre><code class="language-css">
@page:left{
  @bottom-left {
    content: "Page " counter(page) " of " counter(pages);
  }
}
</code></pre>

You can create your own named counters and increment and reset them as you require. To create a counter, use the <code>counter-reset</code> property, increment it with <code>counter-increment</code>. The CSS rules below will create a counter for chapters named <code>chapternum</code> and increment it with each <code>h1</code> — being the start of a chapter in this book. We then use the value of that counter in generated content to add the chapter number and a period before the chapter’s actual title.</p>

<pre><code class="language-css">
body {
  counter-reset: chapternum;
}

h1.chapter:before {
  counter-increment: chapternum;
  content: counter(chapternum) ". ";
}
</code></pre>

We can do the same for figures in the book. A common way to number figures is to use <code>chapternum.figurenum</code>. So, "Figure 3-2" would be the second figure in chapter 3. On the <code>h1</code>, we could reset <code>figurenum</code> in order that it starts from 1 for each chapter.</p>

<pre><code class="language-css">
body {
  counter-reset: chapternum figurenum;
}

h1 {
  counter-reset: figurenum;
}

h1.title:before {
  counter-increment: chapternum;
  content: counter(chapternum) ". ";
}

figcaption:before {
  counter-increment: figurenum;
  content: counter(chapternum) "-" counter(figurenum) ". ";
}
</code></pre>

### Setting Strings

Take a look at a printed book again. As you leaf through a chapter, you’ll probably see that the chapter’s title is printed on the left or right page. As strange as it may sound, the "Generated Content for Paged Media" specification lets us achieve this using CSS.

We do this using a property named <code>string-set</code> in the selector that we want to take the content from. For the chapter title, this would be the <code>h1</code>. The value of <code>string-set</code> is the name you would like to give this content and then <code>content()</code>. You can then output this as generated content using <code>string()</code>.</p>

<pre><code class="language-css">
h1 { 
  string-set: doctitle content(); 
}

@page :right {
  @top-right {
    content: string(doctitle);
    margin: 30pt 0 10pt 0;
    font-size: 8pt;
  }
}
</code></pre>

When your paged media is generated, each time an <code>h1</code> occurs, the content is written to <code>doctitle</code> and then outputted in the top-right margin box of right-hand pages, changing only when another <code>h1</code> occurs.</p>

### Footnotes

Footnotes are a part of the "<a href="https://www.w3.org/TR/css-gcpm-3/#footnotes" rel="nofollow">CSS Generated Content for Paged Media Module</a>" specification. The way footnotes work is that you would add the text of your footnote inline, wrapped in HTML tags (probably a span), with a class to identify it as a footnote. When the page is generated, the content of that "footnote element" is removed and turned into a footnote.

In your CSS, use the footnote value of the <code>float</code> property to create a rule for your footnote class.</p>

<pre><code class="language-css">
.fn {
  float: footnote;
}
</code></pre>

In your document, use that class to wrap any footnote text.</p>

<pre><code class="language-markup">
&lt;p&gt;Footnotes&lt;span class="footnotes"&gt;Footnotes and notes placed in the footer of a document to reference the text. The footnote will be removed from the flow when the page is created.&lt;/span&gt; are useful in books and printed documents.&lt;/p&gt;
</code></pre>

Footnotes have a predefined counter that behaves in the same way as the page counter. Typically, you will want to increment the counter by 1 each time a <code>fn</code> class occurs and reset it at the beginning of each chapter.</p>

<pre><code class="language-css">
.fn {
  counter-increment: footnote;
}

h1 {
  counter-reset: footnote;
}
</code></pre>

The various parts of a footnote can be targeted with CSS pseudo-elements. The <code>footnote-call</code> is the numeric anchor in the text that indicates there is a footnote. This uses the value of the footnote counter as generated content.</p>

<pre><code class="language-css">
.fn::footnote-call {
  content: counter(footnote);
  font-size: 9pt;
  vertical-align: super;
  line-height: none;
}
</code></pre>

The <code>footnote-marker</code> is the numeric marker placed in front of the footnote text in the footer of your document. These behave in a similar way to the numbers generated for an ordered list in CSS.</p>

<pre><code class="language-css">
.fn::footnote-marker {
  font-weight: bold;
}
</code></pre>

The footnotes themselves are placed in the margin, within a special area of the page named <code>@footnote</code>. You would target and style that area as follows.</p>

<pre><code class="language-css">
@page {
  @footnote {
    border-top: 1pt solid black;
  }
}
</code></pre>

### Cross-References

Before moving on to a working example of everything we’ve learned, let’s look at cross-references. On the web, we cross-reference things by adding links. In a book or other printed document, you would normally refer to the page number where that reference is to be found. Because page numbers might change according to the format that the book is printed in — and between editions — doing this with CSS saves us from having to go through and change all of the numbers.

We use another new property, <code>target-counter</code>, to add these numbers. Start by creating links in your document, giving them an <code>href</code>, which is the ID of the element in the document that you want to target. Also, add a class to identify them as a cross-reference, rather than an external link; I’m using <code>xref</code>.</p>

<pre><code class="language-markup">
&lt;a class="xref" href="#ch1" title="Chapter 1"&gt;Chapter 1&lt;/a&gt;
</code></pre>

Then, after the link, use generated content again to output <code>(page x)</code>, where <code>x</code> is the number of the location in the book where that ID can be found.</p>

<pre><code class="language-css">
a.xref:after {
  content: " (page " target-counter(attr(href, url), page) ")";
}
</code></pre>

We’ll be looking at this technique in practice when we create a table of contents for the working example.</p>

## Putting It All Together: An Example Book

We’ve looked at a lot of different properties here in isolation. They make more sense once you put them to use by building a book.

To actually create a book using this CSS, you’ll need a user agent that supports it. Currently, very few things implement this specification well; the one that is most accessible is <a href="https://princexml.com" rel="nofollow">Prince</a>. A standalone commercial license for Prince is expensive, however, you may use Prince free of charge for non-commercial projects. This means that if you just want to try out these techniques, you can. Additionally, if you do have non-commercial uses for this technology, you may use Prince to format those books.

I have extracted passages from one of my favorite books on Project Gutenberg, <a href="https://www.gutenberg.org/ebooks/35450" rel="nofollow"><em>Our Cats</em> by Harrison Weir</a>. I’ve chosen this book because I like cats and because it has images and footnotes that I can use to demonstrate formatting.

You can find the files I am using, plus a generated PDF, over <a href="https://github.com/rachelandrew/css-for-print" rel="nofollow">on GitHub</a>. If you want to experiment with the CSS and build the book yourself, then you will need to download and install <a href="https://princexml.com" rel="nofollow">Prince</a>. Prince is a command-line tool on the Mac, and although there is a Windows GUI, I’ll use the command line because it really is very simple.

Using a Terminal window, switch to your book’s directory or the location where you downloaded my files from GitHub.</p>

<pre><code class="language-bash">
cd /Users/username/smashing-css-books
</code></pre>

Now, run Prince:

<pre><code class="language-bash">
prince -s pdf-styles.css book.html builds/book.pdf
</code></pre>

This will create a PDF in the <code>builds</code> folder named <code>book.pdf</code>. Now, if you make any changes to the CSS or HTML, you can run Prince to see what is different.</p>

### The HTML Document

My entire "book" is compiled in a single HTML document. Compiling documents in Prince is possible, but I’ve found it simpler to just deal with one large document. Before the chapters, which start with an <code>h1</code>, I have a div that contains the cover image, and then the table of contents for the book.

The table of contents links to the IDs of the chapters’ <code>h1</code> headings.</p>

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html dir="ltr" lang="en-US"&gt;
  &lt;head&gt;
  &lt;meta charset="utf-8" /&gt;
  &lt;title&gt;Our Cats and All About Them&lt;/title&gt;
  &lt;meta name="author" content="Harrison Weir"/&gt;
  &lt;meta name="subject" content="Cats. Their Varieties, Habits and Management; and for show, the Standard of Excellence and Beauty"/&gt;
  &lt;meta name="keywords" content="cats,feline"/&gt;
  &lt;meta name="date" content="2014-12-05"/&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div class="frontcover"&gt;
    &lt;/div&gt;
    &lt;div class="contents"&gt;
      &lt;h1&gt;Extracts from Our Cats and All About Them by Harrison Weir&lt;/h1&gt;

        &lt;ul class="toc"&gt;
          &lt;li&gt;&lt;a href="#ch1"&gt;The First Cat Show&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="#ch2"&gt;Trained Cats&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="#ch3"&gt;General Management&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="#ch4"&gt;Superstition and Witchcraft&lt;/a&gt;&lt;/li&gt;
        &lt;/ul&gt;

    &lt;/div&gt;

    &lt;h1 id="ch1" class="chapter"&gt;The First Cat Show&lt;/h1&gt;
      &lt;p&gt;… &lt;/p&gt;

    &lt;h1 id="ch2" class="chapter"&gt;Trained Cats&lt;/h1&gt;
      &lt;p&gt;… &lt;/p&gt;

    &lt;h1 id="ch3" class="chapter"&gt;General Management&lt;/h1&gt;
      &lt;p&gt;… &lt;/p&gt;

    &lt;h1 id="ch4" class="chapter"&gt;Superstition and Witchcraft&lt;/h1&gt;
      &lt;p&gt;… &lt;/p&gt;

  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

The CSS then uses all of the things we have described so far. To start, we need to set up a size for the book using the <code>@page</code> rule. We then use the <code>:first</code> pseudo-class selector to remove the margin on page 1, because this page will have the cover image.</p>

<pre><code class="language-css">
@page {
  size: 5.5in 8.5in;  
  margin: 70pt 60pt 70pt;
}

@page:first {
  size: 5.5in 8.5in;  
  margin: 0;
}
</code></pre>

We then deal with the image for the front cover, making sure that it covers the whole page area.</p>

<pre><code class="language-css">
div.frontcover { 
  page: cover; 
  content: url("images/cover.png");
  width: 100%;
  height: 100%; 
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee0fcc9-3571-46c3-ba46-748501f1ea81/2-image-cover-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e6a5f76-a84a-44af-8c18-69267b11a4da/2-image-cover-opt.jpg" alt="print css sample" width="500" height="782" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee0fcc9-3571-46c3-ba46-748501f1ea81/2-image-cover-large-opt.jpg">See large version</a>)</figcaption></figure>

Next, we deal with the specifics of the left- and right-hand pages, using the <code>:right</code> and <code>:left</code> spread pseudo-classes.

The right-hand spread will have the title of the book in the bottom-left margin box, a page counter in the bottom-right, and the chapter’s title in the top-right. The chapter’s title is set using <code>string-set</code> further down in the style sheet.</p>

<pre><code class="language-css">
@page:right{ 
  @bottom-left {
    margin: 10pt 0 30pt 0;
    border-top: .25pt solid #666;
    content: "Our Cats";
    font-size: 9pt;
    color: #333;
  }

  @bottom-right { 
    margin: 10pt 0 30pt 0;
    border-top: .25pt solid #666;
    content: counter(page);
    font-size: 9pt;
  }

  @top-right {
    content:  string(doctitle);
    margin: 30pt 0 10pt 0;
    font-size: 9pt;
    color: #333;
  }
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4fc5b92-5748-419f-9568-bbc4f3bf00cb/3-image-spread-right-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cc4273d-c3dc-488d-bf04-529e6e41e505/3-image-spread-right-opt.jpg" alt="3-image-spread-right-opt" width="500" height="773" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4fc5b92-5748-419f-9568-bbc4f3bf00cb/3-image-spread-right-large-opt.jpg">See large version</a>)</figcaption></figure>

The left-hand spread has the book’s title in the bottom-right and the page counter in the bottom-left.</p>

<pre><code class="language-css">
@page:left {
  @bottom-right {
    margin: 10pt 0 30pt 0;
    border-top: .25pt solid #666;
    content: "Our Cats";
    font-size: 9pt;
    color: #333;
  }

  @bottom-left { 
    margin: 10pt 0 30pt 0;
    border-top: .25pt solid #666;
    content: counter(page);
    font-size: 9pt;
  }
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bfc8005-0c07-4b1e-80df-78bd374a0c09/4-image-spread-left-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32e2625e-9459-4ff9-810d-dceaaceb51c7/4-image-spread-left-opt.jpg" alt="4-image-spread-left-opt" width="500" height="771" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bfc8005-0c07-4b1e-80df-78bd374a0c09/4-image-spread-left-large-opt.jpg">See large version</a>)</figcaption></figure>

For the first page, which contains the cover image, we’ll make sure that no generated content appears by setting it to <code>normal</code>.</p>

<pre><code class="language-css">
@page:first {
  @bottom-right {
    content: normal;
    margin: 0;
  }

  @bottom-left {
    content: normal;
    margin: 0;
  }
}
</code></pre>

The next section of the style sheet deals with counters. In addition to the preset page counter, we are defining counters for chapters and figures.</p>

<pre><code class="language-css">
/* Reset chapter and figure counters on the body */
body {
  counter-reset: chapternum figurenum;
  font-family: "Trebuchet MS", "Lucida Grande", "Lucida Sans Unicode", "Lucida Sans", Tahoma, sans-serif;
  line-height: 1.5;
  font-size: 11pt;
}

/* Get the title of the current chapter, which will be the content of the h1.
Reset figure counter because figures start from 1 in each chapter. */
h1 {
  string-set: doctitle content();
  page-break-before: always;
  counter-reset: figurenum;
  counter-reset: footnote;
  line-height: 1.3;
}

/* Increment chapter counter */
h1.chapter:before {
  counter-increment: chapternum;
  content: counter(chapternum) ". ";
}

/* Increment and display figure counter */
figcaption:before {
  counter-increment: figurenum;
  content: counter(chapternum) "-" counter(figurenum) ". ";
}
</code></pre>

Chapters now have their number placed before the title. Figures also display their number.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db3caf7f-a4a4-48ab-95a0-1cc8dd86ff82/5-image-figure-number-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5056391c-33ea-43c0-895f-0a8562866c52/5-image-figure-number-opt.jpg" alt="5-image-figure-number-opt" width="500" height="303" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db3caf7f-a4a4-48ab-95a0-1cc8dd86ff82/5-image-figure-number-large-opt.jpg">See large version</a>)</figcaption></figure>

We create footnotes as in the explanation earlier, superscripting the footnote’s call.</p>

<pre><code class="language-css">
.fn {
  float: footnote;
}

.fn {
  counter-increment: footnote;
}

.fn::footnote-call {
  content: counter(footnote);
  font-size: 9pt;
  vertical-align: super;
  line-height: none;
}

.fn::footnote-marker {
  font-weight: bold;
}

@page {
  @footnote {
    border-top: 0.6pt solid black;
    padding-top: 8pt;
  }
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8703cde-60dd-4725-88ce-320fd9c55dc6/6-image-footnotes-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ece802d-939c-4aba-8919-ad8d74f576cb/6-image-footnotes-opt.jpg" alt="6-image-footnotes-opt" width="500" height="271" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8703cde-60dd-4725-88ce-320fd9c55dc6/6-image-footnotes-large-opt.jpg">See large version</a>)</figcaption></figure>

We then add some rules to control where pages break. You need to be fairly careful about being too heavy handed with this. If your book has a lot of tables and figures, then adding many specific rules here could cause a lot of long gaps in the book. Experimenting and testing will show how far you can take the control of breaks. I have found the rules below to be a good starting point.

Remember that this is a suggestion to the user agent. In some cases, keeping a table from breaking will be impossible if the table doesn’t fit on a page!

<pre><code class="language-css">
h1, h2, h3, h4, h5 {
  font-weight: bold;
  page-break-after: avoid;
  page-break-inside:avoid;
}

h1+p, h2+p, h3+p {
  page-break-before: avoid;
}

table, figure {
  page-break-inside: avoid;
}
</code></pre>

Finally, we style the table of contents, and we use an interesting trick here. When describing cross-references, I explained how we use <code>target-counter</code> to display the page number that the ID is on. This is what we’ll do for our table of contents. The rule below puts the page number after the link to each chapter in the table of contents.</p>

<pre><code class="language-css">
ul.toc a::after {
  content: target-counter(attr(href), page);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05a27cd1-64c5-47ff-b4a4-8da05c568141/7-image-toc-numbers-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/845813ad-5b52-463b-93e8-e428e923f431/7-image-toc-numbers-opt.jpg" alt="7-image-toc-numbers-opt" width="500" height="263" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05a27cd1-64c5-47ff-b4a4-8da05c568141/7-image-toc-numbers-large-opt.jpg">See large version</a>)</figcaption></figure>

Commonly in books, however, you would use leader dots to line up all of the page numbers against the right margin. Amazingly, CSS gives us a way to do this, by adding <code>leader()</code> before the number in the generated content.</p>

<pre><code class="language-css">
ul.toc a::after {
  content: leader('.') target-counter(attr(href), page);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df43c974-fde2-4455-86de-37c1bd3e8e90/8-image-toc-leader-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31e57501-1269-4fcf-ba29-859f4c3f3475/8-image-toc-leader-opt.jpg" alt="8-image-toc-leader-opt" width="500" height="771" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df43c974-fde2-4455-86de-37c1bd3e8e90/8-image-toc-leader-large-opt.jpg">See large version</a>)</figcaption></figure>

We now have a complete style sheet with which to build our book. I’ve avoided spending a lot of time on typography here, concentrating instead on the specifics of creating a book. From this point, however, you can experiment and add your own styles to create a unique book design.</p>

## Not Just Books!

Remember that these techniques are not just for books. You could use them to generate print and PDF versions of a product catalog directly from the HTML of a website that you have developed for a client. Or you could create flyers and brochures from web content.

If you want to create PDF documents from a website using Prince, then <a href="https://docraptor.com/" rel="nofollow">DocRaptor</a> is a great option. This service uses Prince via an API. You can send documents via the API and receive a PDF — perfect for allowing users to download content as a PDF on the fly. Everything we have looked at in this article is possible via an API integration with DocRaptor.

Even if you don’t have an immediate need for PDF generation, it’s a fascinating aspect of CSS — and it’s a useful skill to have tucked away, so that you know what is possible when a use case presents itself.</p>

## Resources And Further Reading

*   "[CSS Paged Media Module Level 3](https://www.w3.org/TR/css3-page/)," W3C
*   "[CSS Generated Content for Paged Media Module](https://www.w3.org/TR/css-gcpm-3/)," W3C
*   "[Using CSS Counters](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Counters)," Mozilla Developer Network
*   "[CSS Books: Living Standard](https://books.spec.whatwg.org/)," WHATWG
*   "[User Guide for Prince 9.0](https://www.princexml.com/doc/)" A lot of simple examples that work in Prince
*   "[How to Write a Book](https://24ways.org/2013/how-to-write-a-book/)," Jonathan Snook, 24 Ways
*   "[Building Books With CSS3](https://alistapart.com/article/building-books-with-css3)," Nellie McKesson, A List Apart
*   "[Printing a Book With CSS: Boom!](https://alistapart.com/article/boom)," Bert Bos and Håkon Wium Lie, A List Apart
*   "[HTML, EPUB, MOBI, PDF, WTF: Creating an Ebook](https://rachelandrew.co.uk/archives/2014/01/07/html-epub-mobi-pdf-wtf-creating-an-ebook/)," Rachel Andrew

{{< signature "vf, al, il" >}}

