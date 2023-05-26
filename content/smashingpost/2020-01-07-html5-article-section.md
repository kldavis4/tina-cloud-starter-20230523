---
title: 'Why You Should Choose HTML5 `article` Over `section`'
slug: html5-article-section
author: bruce-lawson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e75e9287-985f-4f79-b406-5e178b51e183/html5-article-section-sharing-card.png
date: 2020-01-07T11:30:00.000Z
summary: >-
  Browsers’ visual display of headings nested inside `<section>` elements makes it look as if they are assigning a logical hierarchy to those headings. However, this is purely visual and is not communicated to assistive technologies. What use is `<section>`, and how should authors mark up headings that are hugely important to AT users?
description: >-
  In this article, Bruce Lawson explains what use we have of `<section>` and how authors should mark up headings that are hugely important to AT users.
categories:
  - CSS
  - HTML
  - Browsers
---
A few days ago, I was having a chat with some friends, one of whom asked me the difference between `<article>` and `<section>` in HTML. This is one of the eternal mysteries of web development, up there with “why is it white-space: nowrap, not white-space: no-wrap?” and “why is CSS ‘gray’ a darker color than ‘darkgray’?”.

I gave my usual answer: think of `<article>` not just as a newspaper article, or a blog post, but as an article of clothing &mdash; a discrete entity that can be reused in another context. So your trousers are an article, and you can wear them with a different outfit; your shirt is an article, and can be worn with different trousers; your knee-length patent leather stiletto boots are an article (you wouldn’t wear just one of them, would you?).

[The spec says](https://html.spec.whatwg.org/dev/sections.html#the-article-element):

<blockquote>“The article element represents a complete, or self-contained, composition in a document, page, application, or site and that is, in principle, independently distributable or reusable, e.g. in syndication. This could be a forum post, a magazine or newspaper article, a blog entry, a user-submitted comment, an interactive widget or gadget, or any other independent item of content.”</blockquote>

So a homepage with a list of blog posts would be a `<main>` element wrapping a series of `<article>` elements, one for each blog post. You would use the same structure for a list of videos (think YouTube) with each video being wrapped in an `<article>`, a list of products (think Amazon) and so on. Any of those `<article>`s is conceptually syndicatable &mdash; each could stand alone on its own dedicated page, in an advert on another page, as an entry in an RSS feed, and so on.

Apple’s WatchOS contains Reader which uses the `<article>` element to know the primary content of your page. [Apple says](https://developer.apple.com/videos/play/wwdc2018/239/?time=349):

<blockquote>“We’ve brought Reader to watchOS 5 where it automatically activates when following links to text-heavy web pages. It’s important to ensure that Reader draws out the key parts of your web page by using semantic markup to reinforce the meaning and purpose of elements in the document. Let’s walk through an example. First, we indicate which parts of the page are the most important by wrapping it in an article tag.”</blockquote>

[Combining `<article>` with HTML5 microdata](https://www.brucelawson.co.uk/2018/the-practical-value-of-semantic-html/) helps Reader construct the optimal display for small watch screens:

<blockquote>“Specifically, enclosing these header elements inside the article ensure that they all appear in Reader. Reader also styles each header element differently depending on the value of its itemprop attribute. Using itemprop, we’re able to ensure that the author, publication date, title, and subheading are prominently featured.”</blockquote>

{{% feature-panel %}}

## So What About &lt;section&gt;?

My usual advice continues: don’t bother with `<section>` or worry about how it differs from `<article>`. It was invented as a generic wrapper for headings so that the browser could determine the HTML5 document outline.

The what? The document outline algorithm is a way to use only one heading tag &mdash; `<h1>` &mdash; and have it magically “become” the correct level of heading (e.g. turn into an `<h2>`, `<h3>`, etc.), depending on how deeply it’s nested in HTML5 sectioning elements:`<article>`, `<section>`, and so on.

So, for example, here’s what you’ve typed into your CMS:

<pre><code class="language-html">&lt;h1&gt;My Fabulous article&lt;/h1&gt;

&lt;p&gt;Lorem Ipsum Trondant Fnord&lt;/p&gt;
</code></pre>

This works brilliantly when shown as a standalone article. But what about on your homepage, which is a list of your latest articles?

<pre><code class="language-html">&lt;h1&gt;My latest posts&lt;/h1&gt;

&lt;article&gt;

  &lt;h1&gt;My fabulous article&lt;/h1&gt;

 &lt;p&gt;Lorem Ipsum Trondant Fnord&lt;/p&gt;

&lt;/article&gt;

&lt;article&gt;

  &lt;h1&gt;Another magnum opus&lt;/h1&gt;

  &lt;p&gt;Magnum solero paddle pop&lt;/p&gt;

&lt;/article&gt;
</code></pre>

In this example, according to the specification, the `<h1>`s inside the `<article>` elements “become” logical `<h2>`s, because `<article>`, like `<section>`, is a _sectioning element_.

**Note**: *This isn’t a new idea. Way back in 1991, [Sir Uncle Timbo wrote](https://lists.w3.org/Archives/Public/www-talk/1991SepOct/0003.html):*

<blockquote>“I would in fact prefer, instead of <code>&lt;h1&gt;</code>, <code>&lt;h2&gt;</code>, etc. for  headings [those come from the AAP DTD] to have a nestable <code>&lt;SECTION&gt;</code>...<code>&lt;/SECTION&gt;</code> element, and a generic <code>&lt;H&gt;</code>...<code>&lt;/H&gt;</code> which at any level within the sections would produce the required level of Heading.”</blockquote>

Unfortunately, however, [no browser implements HTML5 outlining](https://html5doctor.com/computer-says-no-to-html5-document-outline/), so there is no point in using `<section>`.  At one point, the JAWS screen reader attempted to implement the document outlining algorithm (in IE, but not on Firefox) but [implemented it buggily](https://accessibleculture.org/articles/2011/10/jaws-ie-and-headings-in-html5/). It seems that browser developers simply aren’t interested (more sordid details in the <a href="#further-reading">Further Reading</a> section for true anoraks).

“But,” interjected another friend in the conversation, “now browsers display different sizes of font depending on how deeply the `<h1>` is nested in `<section>`s”, and proceeded to prove it. *Mind blown!*

[Here’s a similar demo](https://jsbin.com/bizaqokiha/edit?html,output). The left column shows four `<h1>`s, nested in sections; the right column shows a, `<h1>`, `<h2>`, `<h3>`, `<h4>` with no nesting. The Firefox screenshot shows that the nested `<h1>`s default to the same font as the traditional `<h1>`...`<h4>` tags:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbddcbc3-6c56-4d08-bb16-823fbc45ed24/fig1-html5-article-section.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbddcbc3-6c56-4d08-bb16-823fbc45ed24/fig1-html5-article-section.png" sizes="100vw" caption="A comparison of &lt;h1&gt;s nested in &lt;section&gt; elements and &lt;h1&gt;, &lt;h2&gt;, &lt;h3&gt;, &lt;h4&gt; (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbddcbc3-6c56-4d08-bb16-823fbc45ed24/fig1-html5-article-section.png'>Large preview</a>)" alt="Screenshot showing that the nested h1 elements, and the real heading elements display in the same sizes" >}}

The results are the same in Chrome, Chromium derivatives such as Edge beta for Mac, and Safari on Mac.

So does this mean that we should all happily start using `<h1>` as our only heading element, nesting it in `<section>`s?

No. Because this is only a change in the visual styling of the h1s. If we crack open the Firefox Accessibility inspector in devtools, we can see that the text “level 2” is styled to look like an H2, but is still set at “level 1” &mdash; the Accessibility Tree hasn’t been changed to be level 2.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73e3a302-6ca0-4609-bf75-458448c378e7/fig2-html5-article-section.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73e3a302-6ca0-4609-bf75-458448c378e7/fig2-html5-article-section.png" sizes="100vw" caption="Firefox’s Accessibility Inspector shows that a nested <code>&lt;h1&gt;</code> appears visually the same as an <code>&lt;h2&gt;</code> but its aria-level is incorrectly set to “1”, not “2” (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73e3a302-6ca0-4609-bf75-458448c378e7/fig2-html5-article-section.png'>Large preview</a>)" alt="Screenshot of the firefox accessibility inspector selecting a nested h1 element" >}}

Compare this with the Real H2 in the right column:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a73df0e9-60b7-4970-b88a-5616340f3a31/fig3-html5-article-section.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a73df0e9-60b7-4970-b88a-5616340f3a31/fig3-html5-article-section.png" sizes="100vw" caption="Firefox’s Accessibility Inspector shows that a real <code>&lt;h2&gt;</code> has a computed aria-level of “2”, which is correct (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a73df0e9-60b7-4970-b88a-5616340f3a31/fig3-html5-article-section.png'>Large preview</a>)" alt="Screenshot of the firefox accessibility inspector selecting a real h2 element" >}}

This shows the accessibility tree has been correctly informed that this is a level 2 heading. In fact, [Mozilla did try](https://twitter.com/ecbos_/status/1207362954762555392) communicating the computed level to the accessibility tree:

<blockquote>“We experimented a bit with that... but had to revert it because people in our a11y team complained about too many regressions (accidentally lowering <code>&lt;h1&gt;</code> levels and such).”</blockquote>

For assistive technology users, a proper hierarchy of headings is vital. As the eighth [WebAIM screenreader user survey](https://webaim.org/projects/screenreadersurvey8/#heading ) shows,

<blockquote>“The usefulness of proper heading structures is very high, with 86.1% of respondents finding heading levels very or somewhat useful.”</blockquote>

Therefore, you should continue to use `<h1>` until `<h6>`, and ignore `section`.

{{% ad-panel-leaderboard %}}

## Never Say Never

“But..” you might now be spluttering indignantly, “there’s a `<section>` element right on this very page!”. And you would be right, dear reader. The “quick summary” is wrapped in a `<section>`, for accessibility reasons. When screen reader user Léonie Watson gave her webinar “[How A Screen Reader User Accesses The Web](https://www.smashingmagazine.com/2019/02/accessibility-webinar/)”, she pointed out an area where Smashing Magazine’s markup could be tweaked to make her experience better.

As you can see from the screenshot, Smashing articles are preceded by a quick summary, followed by a horizontal line separating the summary from the article proper.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f69d2f-c610-4807-bdd4-106940ee6c87/fig4-html5-article-section.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f69d2f-c610-4807-bdd4-106940ee6c87/fig4-html5-article-section.png" sizes="100vw" caption="The Smashing “Quick Summary” is separated from its full article by a horizontal line. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f69d2f-c610-4807-bdd4-106940ee6c87/fig4-html5-article-section.png'>Large preview</a>)" alt="Screenshot of the top of a Smashing Magazine article" >}}

But the separator is purely decorative, so Léonie couldn’t tell where the summary ends and the article begins. She suggested a fix: we wrapped the summary in a `<section>` element:

<pre><code class="language-html">&lt;section aria-label="quick summary"&gt;

    Summary text

&lt;/section&gt;
</code></pre>

In most screen readers, a `<section>` element isn’t announced unless it has an _accessible name_. In this case, the text of the aria label. Now, her screen reader announced “Quick summary region”, and after the summary “Quick summary region end”. This simple markup also makes it possible for a screen reader user to jump over the summary if they want to.

We could have used a simple `<div>` but then, as [Marco Zehe writes](https://marcozehe.de/2019/12/12/if-you-aria-label-something-give-it-a-role/),

<blockquote>“As a rule of thumb, if you label something via aria-label or aria-labelledby, make sure it has a proper widget or landmark role.”</blockquote>

So rather than use `<div role=”region” aria-label=”quick summary”>`, we chose `<section>` as that has a built-in role of region and Bruce’s infallible law of ARIA™ applies: _built-in beats bolt-on. Bigly._

{{% ad-panel-leaderboard %}}

## Conclusion

Hopefully, you’ve come away with these take-homes:

- Don’t use loads of `<h1>`s. Make `<h1>` the main heading of your page, then use `<h2>`, `<h3>`, `<h4>`, etc. in a proper hierarchy without skipping levels.
- `<section>` can be used with aria-label to signal to a screen reader user where a particular sub-part of an article begins and ends. Otherwise, forget about it, or use another element, such as `<aside aria-label=”quick summary”>` or `<div role=”region” aria-label=”quick summary”>`.
- `<main>`, `<header>`, `<footer>` and `<nav>` are very useful for screen reader users, and entirely transparent to those who don’t use assistive technology. So use them.
- `<article>` isn’t just for blog posts &mdash; it’s for any self-contained thing. It also helps WatchOS display your content properly.

*I gratefully acknowledge [Léonie Watson](https://twitter.com/leoniewatson)’s help writing this article. Any errors are totally her fault.*

### Further Reading

- “[Headings And Sections](https://www.w3.org/TR/html52/sections.html#headings-and-sections),” *HTML 5.2
W3C Recommendation* (14 Dec. ’17)
Note its warning: “There are currently no known native implementations of the outline algorithm ... Therefore the outline algorithm cannot be relied upon to convey document structure to users. Authors should use heading rank (h1-h6) to convey document structure.”
- “[There Is No Document Outline Algorithm](https://adrianroselli.com/2016/08/there-is-no-document-outline-algorithm.html),” *Adrian Roselli*
All the gory details of how the specification for the sectioning algorithm has changed.
- “[ARIA in HTML](https://w3c.github.io/html-aria/),” *W3C Editor’s Draft* (19 Dec. ’19)
Rules to live by if you do find yourself adding ARIA roles and attributes to HTML.
- [The Practical Value Of Semantic HTML](https://www.brucelawson.co.uk/2018/the-practical-value-of-semantic-html/),” *Bruce Lawson*
My own article, linking to details of how WatchOS uses HTML5 and microdata.

{{< signature "ra, il" >}}
