---
title: 'Baking Structured Data Into The Design Process'
slug: structured-data-design-process
author: frederick-o-brien
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/621d96e3-dc74-47f4-873f-75bf349b11d8/structured-data-design-process.png
date: 2020-04-09T11:30:00.000Z
summary: >-
 Retrofitting search engine optimization only gets you so far. As metadata gets smarter, it’s more important than ever to build it into the design process from the start.
description: >-
  Retrofitting search engine optimization only gets you so far. As metadata gets smarter, it’s more important than ever to build it into the design process from the start.
categories:
  - SEO
  - Business
  - UX
---

<p>Search engine optimization (<a href="https://www.smashingmagazine.com/category/seo">SEO</a>) is essential for almost every kind of website, but its finer points remain something of a specialty. Even today SEO is often treated as something that can be tacked on after the fact. It can up to a point, but it really shouldn’t be. <a href="https://www.google.com/search/howsearchworks/algorithms/">Search engines get smarter every day</a> and there are ways for websites to be smarter too.</p>

<p>The foundations of SEO are the same as they’ve always been: great content clearly labeled will win the day sooner or later &mdash; regardless of how many people try to game the system. The thing is, those labels are far more sophisticated than they used to be. Meta titles, image alt text, and backlinks are important, but in 2020, they’re also fairly primitive. There is another tier of metadata that only a fraction of sites are currently using: structured data.</p>

<p>All search engines share the same purpose: to organize the web’s content and deliver the most relevant, useful results possible to search queries. How they achieve this has changed enormously since the days of Lycos and Ask Jeeves. Google alone uses more than 200 ranking factors, and those are just the ones we know about.</p>

<p>SEO is a huge field nowadays, and I put it to you that structured data is a really, <em>really</em> important factor to understand and implement in the coming years. It doesn’t just improve your chances of ranking highly for relevant queries. More importantly, it helps make your websites better &mdash; opening it up to all sorts of useful web experiences.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2020/02/seo-web-design-process/">Where Does SEO Belong In Your Web Design Process?</a></em></p>

{{% feature-panel %}}

## What Is Structured Data?

<p>Structured data is a way of labeling content on web pages. Using vocabulary from <a href="https://blog.hubspot.com/marketing/google-ranking-algorithm-infographic">Schema.org</a>, it removes much of the ambiguity from SEO. Instead of trusting the likes of Google, Bing, Baidu, and DuckDuckGo to work out what your content is about, you tell them. It’s the difference between a search engine <em>guessing</em> what a page is about and <em>knowing</em> for sure.</p>

<p>As Schema.org puts it:</p>

<blockquote>By adding additional tags to the HTML of your web pages &mdash; tags that say, "Hey search engine, this information describes this specific movie, or place, or person, or video" &mdash; you can help search engines and other applications better understand your content and display it in a useful, relevant way.</blockquote>

<p>Schema.org launched in 2011, a project shared by Google, Microsoft, Yahoo, and Yandex. In other words, it’s a ‘bipartisan’ effort &mdash; if you like. The markup transcends any one search engine. In Schema.org’s own words,</p>

<blockquote>“A shared vocabulary makes it easier for webmasters and developers to decide on a schema and get the maximum benefit for their efforts.”</blockquote>

<p>It is in many respects a more expansive cousin of microformats (launched around 2005) which embed semantics and structured data in HTML, mainly for the benefit of search engines and aggregators. Although <a href="https://microformats.org/2020/03/04/google-confirms-microformats-are-still-a-recommended-metadata-format-for-content">microformats are currently still supported</a>, the ‘official’ nature of the Schema.org library makes it a safer bet for longevity.</p>

<p><a href="https://json-ld.org">JSON for Linked Data</a> (JSON-LD) has emerged as the dominant underlying standard for structured data, although <a href="https://www.w3.org/TR/microdata/">Microdata</a> and <a href="https://rdfa.info/">RDFa</a> are also supported and serve the same purpose. Schema.org provides examples for each type depending on what you’re most comfortable with.</p>

<p>As an example, let’s say Joe Bloggs writes a review of Joseph Heller’s 1961 novel <em>Catch-22</em> and publishes it on his blog. Sadly, Bloggs has poor taste and gives it two out of five stars. For a person looking at the page, this information would be understood unthinkingly, but computer programs would have to connect several dots to reach the same conclusion.</p>

<p>With structured data, the following markup could be added to the page’s <code>&lt;head&gt;</code> code. (This is a JSON-LD approach. Microdata and RDFa can be used to weave the same information into <code>&lt;body&gt;</code> content):</p>

<div class="break-out">

<pre><code class="language-json">&lt;script type="application/ld+json"&gt;
{
  "@context" : "https://schema.org",
  "@type" : "Book",
  "name" : "Catch-22",
  "author" : {
    "@type" : "Person",
    "name" : "Joseph Heller"
  },
  "datePublished" : "1961-11-10",
  "review" : {
    "@type" : "Review",
    "author" : {
      "@type" : "Person",
      "name" : "Joe Bloggs"
    },
    "reviewRating" : {
      "@type" : "Rating",
      "ratingValue" : "2",
    "worstRating" : "0",
      "bestRating" : "5"
    },
    "reviewBody" : "A disaster. The worst book I&#39;ve ever read, and I&#39;ve read The Da Vinci Code."
  }
}
&lt;/script&gt;</code></pre>
</div>

<p>This sets in stone that the page is about <em>Catch-22</em>, a novel by Joseph Heller published on November 10th, 1961. The reviewer has been identified, as has the parameters of the scoring system. Different schemas can be combined (or tiered) to describe different things. For example, through tagging of this sort, you could make clear a page is the event listing for an open-air film screening, and the film in question is <em>The Life Aquatic with Steve Zissou</em> by Wes Anderson.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/07/better-research-design-results/">Better Research, Better Design, Better Results</a></em></p>

### Why Does It Matter?

<p>Ok, wonderful. I can label my website up to its eyeballs and it will look exactly the same, but what are the benefits? To my mind, there are two main benefits to including structured data in websites:</p>

<ol>
<li><strong>It makes search engine’s jobs much easier.</strong><br />They can index content more accurately, which in turn means they can present it more richly.</li>
<li><strong>It helps web content to be more thorough and useful.</strong><br />Structured data gives you a ‘computer perspective’ on content. Quality content is fabulous. Quality content thoroughly tagged is the stuff of dreams.</li>
</ol>

<p>You know when you see snazzy search results that include star ratings? That’s structured data. Rich snippets of film reviews? Structured data. When a selection of recipes appear, ingredients, preparation time and all? You guessed it. Dig into the code of any of these pages and you’ll find the markup somewhere. Search engines reward sites using structured data because it tells them exactly what they’re dealing with.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d81222e-33fd-4d8e-a66b-1a637c0d7886/1-film-review-snippets-in-google-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d81222e-33fd-4d8e-a66b-1a637c0d7886/1-film-review-snippets-in-google-search.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d81222e-33fd-4d8e-a66b-1a637c0d7886/1-film-review-snippets-in-google-search.png'>Large preview</a>)" alt="Review snippets using structured data markup on Google Search" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d869a5b6-f9da-4243-be9d-d92430ae881b/2-apple-pie-recipe-snippets-in-google-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d869a5b6-f9da-4243-be9d-d92430ae881b/2-apple-pie-recipe-snippets-in-google-search.png" sizes="100vw" caption="Examine the code on the websites featured above and sure enough, structured data is there. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d869a5b6-f9da-4243-be9d-d92430ae881b/2-apple-pie-recipe-snippets-in-google-search.png'>Large preview</a>)" alt="Recipe snippets using structured data markup on Google Search" >}}

<p>It’s not just search either, to be clear. That’s a big part of it but it’s not the whole deal. Structured data is primarily about tagging and organizing content. Rich search results are just one way for said content to be used. Google Dataset Search uses <a href="https://schema.org/Dataset">Schema.org/Dataset</a> markup, for example.</p>

<p>Below are a handful of examples of structured data being useful:</p>

<ul>
<li><a href="https://schema.org/Recipe">Recipes</a></li>
<li><a href="https://schema.org/Review">Reviews</a></li>
<li><a href="https://schema.org/FAQPage">FAQs</a></li>
<li><a href="https://developers.google.com/search/docs/data-types/speakable">Voice queries</a></li>
<li><a href="https://schema.org/Event">Event listings</a></li>
<li><a href="https://developers.google.com/assistant/content/overview">Content Actions</a>.</li>
</ul>

<p>There are thousands more. Like, literally. Schema.org even <a href="https://blog.schema.org/2020/03/schema-for-coronavirus-special.html">fast-tracked the release of markup for Covid-19</a> recently. It’s an ever-growing library.</p>

<p>In many respects, structured data is a branch of the Semantic Web, which strives for a fully machine-readable Internet. It gives you a machine-readable perspective on web content that (when properly implemented) feeds back into richer functionality for people.</p>

<p>As such, just about anyone with a website would benefit from knowing what structured data is and how it works. <a href="https://w3techs.com/technologies/overview/structured_data">According to W3Techs</a>, only 29.6% of websites use JSON-LD, and 43.2% don’t use any structured data formats at all. There’s no obligation, of course. Not everyone cares about SEO or being machine-readable. On the flip side, for those who do there’s currently a big opportunity to one-up rival sites.</p>

<p>In the same way that HTML forces you to think about how content is organized, structured data gets you thinking about the substance. It makes you more thorough. Whatever your website is about, if you comb through the relevant schema documentation you’ll almost certainly spot details that you didn’t think to include beforehand.</p>

<p>As humans, it is easy to take for granted the connections between information. Search engines and computer programs are smart, but they’re not <em>that</em> smart. Not yet. Structured data translates content into terms they can understand. This, in turn, allows them to deliver richer experiences.</p>

#### Resources And Further Reading

<ul>
<li>“<a href="https://moz.com/blog/structured-data-for-seo-1">The Beginner's Guide To Structured Data For SEO: A Two-Part Series</a>,” Bridget Randolph, Moz</li>
<li>“<a href="https://www.searchenginejournal.com/technical-seo/schema/">What Is Schema Markup And Why It’s Important For SEO</a>,” Chuck Price, Search Engine Journal</li>
<li>“<a href="https://www.semrush.com/blog/what-is-schema-beginner-s-guide-to-structured-data/">What Is Schema? Beginner‘s Guide To Structured Data</a>,” Luke Harsel, SEMrush</li>
<li>“<a href="https://blog.codeship.com/json-ld-building-meaningful-data-apis/">JSON-LD: Building Meaningful Data APIs</a>,” Benjamin Young, Rollout Blog</li>
<li>“<a href="https://developers.google.com/search/docs/guides/intro-structured-data">Understand How Structured Data Works</a>,” Google Search for Developers</li>
<li>“<a href="https://www.bing.com/webmaster/help/marking-up-your-site-with-structured-data-3a93e731">Marking Up Your Site With Structured Data</a>,” Bing</li>
</ul>

{{% ad-panel-leaderboard %}}

## Incorporating Structured Data Into Website Design

<p>Weaving structured data into a website isn’t as straightforward as, say, changing a meta title. It’s the data DNA of your web content. If you want to implement it properly, then you need to be willing to get into the weeds &mdash; at least a little bit. Below are a few simple steps developers can take to weave structured data into the design process.</p>

<p><strong>Note</strong>: <em>I personally subscribe to a holistic approach to design, where design and substance go hand in hand. Juggling a bunch of disciplines is nothing new to web design, this is just another one, and if it’s incorporated well it can strengthen other elements around it. Think of it as an enhancement to your site’s engine. The car may not look all that different but it handles a hell of a lot better.</em></p>

### Start With A Concept

<p>I’ll use myself as an example. For five years, two friends and I have been reviewing an album a week as a hobby (with others stepping in from time to time). Our sneering, insufferable prose is currently housed in a WordPress site, which &mdash; under my well-meaning but altogether ignorant care &mdash; had grown into a Frankenstein’s monster of plugins.</p>

<p>We are in the process of redesigning the site which (among other things) has entailed bringing structured data into the core design. Here, as with any other project, the first thing to do is establish what your content is about. The better you answer this question, the easier everything that follows will be.</p>

<p>In our case, these are the essentials:

<ul> 
  <li>We review music albums;</li>
  <li>Each review has three reviewers who each write a summary by choosing up to three favorite tracks and assigning a personal score out of ten;</li>
  <li>These three scores are combined into a final score out of 30;</li>
  <li>From the three summaries, a passage is chosen to serve as an ‘at-a-glance’ roundup of all our thoughts.</li>
</ul>

<p>Some of this may sound a bit specific or even a bit arbitrary (because it is), but you’d be surprised how much of it can be woven together using structured data.</p>

<p>Below is a mockup of what the revamped review pages will look like, and the information that can be translated into schema markup:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e29dc4-2af2-4a37-ae39-a09d7e940446/3-web-page-annotated-with-structured-data.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e29dc4-2af2-4a37-ae39-a09d7e940446/3-web-page-annotated-with-structured-data.png" sizes="100vw" caption="Even the most sprawling content is packed full of information just waiting to be tagged and structured. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e29dc4-2af2-4a37-ae39-a09d7e940446/3-web-page-annotated-with-structured-data.png'>Large preview</a>)" alt="A web page annotated with structured data markup" >}}

<p>There’s no trick to this process. I know what the content is about, so I know where to look in the documentation. In this case, I go to <a href="https://schema.org/MusicAlbum">Schema.org/MusicAlbum</a> and am met with all manner of potential properties, including:</p>

<ul>
<li><code>albumReleaseType</code></li>
<li><code>byArtist</code></li>
<li><code>genre</code></li>
<li><code>producer</code></li>
<li><code>datePublished</code></li>
<li><code>recordedAt</code></li>
</ul>

<p>There are dozens; some exclusive to MusicAlbum, others falling under the larger umbrella of CreativeWork. Digging deeper into the documentation, I find that the markup can connect to <a href="https://musicbrainz.org/">MusicBrainz</a>, a music metadata encyclopedia. The same process unfolds when I go to the <a href="https://schema.org/Review">Review documentation</a>.</p>

<p>From that one simple page, the following information can be gleaned and organized:</p>

<div class="break-out">

<pre><code class="language-json">&lt;script type="application/ld+json"&gt;
    
        {
  "@context": "https://schema.org/",
  "@type": "Review",
  "reviewBody": "Whereas My Love is Cool was guilty of trying too hard no such thing can be said of Visions. The riffs roar and the melodies soar, with the band playing beautifully to Ellie Rowsell's strengths.",
  "datePublished": "October 4, 2017",
  "author": [{
    "@type": "Person",
    "name": "André Dack"
  },
             {
    "@type": "Person",
    "name": "Frederick O'Brien"
  },
             {
    "@type": "Person",
    "name": "Marcus Lawrence"
  }],
  "itemReviewed": {
    "@type": "MusicAlbum",
      "@id": "https://musicbrainz.org/release-group/7f231c61-20b2-49d6-ac66-1cacc4cc775f",
      "byArtist": {
        "@type": "MusicGroup",
        "name": "Wolf Alice",
        "@id": "https://musicbrainz.org/artist/3547f34a-db02-4ab7-b4a0-380e1ef951a9"
      },
      "image": "https://lesoreillescurieuses.files.wordpress.com/2017/10/a1320370042_10.jpg",
      "albumProductionType": "https://schema.org/StudioAlbum",
    "albumReleaseType": "https://schema.org/AlbumRelease",
      "name": "Visions of a Life",
      "numTracks": "12",
      "datePublished": "September 29, 2017"
  },
  "reviewRating": {
    "@type": "Rating",
    "ratingValue": 27,
    "worstRating": 0,
    "bestRating": 30
  }
}
&lt;/script&gt;
</code></pre>
</div>

<p>And honestly, I may yet add a lot more. Initially, I found the things that are already part of a review page’s structures (i.e. artist, album name, overall score) but then new questions began to present themselves. What could be clearer? What could I add?</p>

<p>This should obviously be counterbalanced by questions of what’s <em>unnecessary</em>. Just because you can do something doesn’t mean that you should. There <em>is</em> such a thing as ‘too much information’. Still, sometimes a bit more detail can really take a page up a notch.</p>

### Familiarize Yourself With Schema

<p>There’s no way around it; the best way to get the ball rolling is to immerse yourself in the documentation. There are tools that implement it for you (more on those <a href="#tools">below</a>), but you’ll get more out of the markup if you have a proper sense of how it works.</p>

<p>Trawl through the <a href="https://schema.org">Schema.org</a> documentation. Whoever you are and whatever your website’s for, the odds are that there are plenty of relevant schemas. The site is very good with examples, so it needn’t remain theoretical.</p>

<p>The step beyond that, of course, is to find rich search results you would like to emulate, visiting the page, and using browser dev tools to look at what they’re doing. They are often excellent examples of websites that know their content inside out. You can also feed code snippets or URLs into Google’s Structured Data Markup Helper, which then generates appropriate schema.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed67f6f1-33f3-43f7-8ef2-bfc6df1f1469/4-google-structured-data-markup-helper.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed67f6f1-33f3-43f7-8ef2-bfc6df1f1469/4-google-structured-data-markup-helper.png" sizes="100vw" caption="Tools like Google’’s Structured Data Markup Helper are excellent for getting to grips with how structured data works. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed67f6f1-33f3-43f7-8ef2-bfc6df1f1469/4-google-structured-data-markup-helper.png'>Large preview</a>)" alt="Example of Google Structured Data Markup Helper in action" >}}

<p>The fundamentals are actually very simple. Once you get your head around them, it’s the breadth of options that take time to explore and play around with. You don’t want to be that person who gets to the end of a design process, looks into schema options, and starts second-guessing everything that’s been done.</p>

{{% ad-panel-leaderboard %}}

### Ask The Right Questions

<p>Now that you’re armed with your wealth of structured data knowledge, you’re better positioned to lay the foundations for a strong website. Structured data rides a fairly unique line. In the immediate sense, it exists ‘under the hood’ and is there for the benefit of computers. At the same time, it can enable richer experiences for the user.</p>

<p>Therefore, it pays to look at structured data from both a technical and user perspective. How can structured data help my website be better understood? What other resources, online databases, or hardware (e.g. smart speakers) might be interested in what you’re doing? What options appear in the documentation that I hadn’t accounted for? Do I want to add them?</p>

<p>It is especially important to identify recurring types of content. It’s safe to say a blog can expect lots of blog posts over time, so incorporating structured data into post templates will yield the most results. The example I gave above is all well and good on its own, but there’s no reason why the markup process can’t be automated. That’s the plan for us.</p>

<p>Consider also the ways that people might find your content. If there are opportunities to, say, highlight a snippet of copy for use in voice search, do it. It’s that, or leave it to search engines to work it out for themselves. No-one knows your content better than you do, so make use of that understanding with descriptive markup.</p>

<p>You don’t need to guess how content will be understood with structured data. With tools like Google’s Rich Results Tester, you can see exactly how it gives content form and meaning that might otherwise have been overlooked.</p>

#### Resources And Further Reading

<ul>
<li>“<a href="https://schema.org/docs/gs.html">Getting Started With Schema.org Using Microdata</a>,” Schema.org</li>
<li>“<a href="https://github.com/schemaorg/schemaorg">Schema.org Project Repository</a>,” GitHub community</li>
<li>“<a href="https://www.google.com/webmasters/markup-helper/">Structured Data Markup Helper</a>,” Googe Webmasters</li>
<li>“<a href="https://codelabs.developers.google.com/codelabs/structured-data/index.html">Add Structured Data To Your Web Pages</a>,” Google Developers Codelabs</li>
<li>“<a href="https://search.google.com/test/rich-results">Rich Results Test</a>,” Google</li>
</ul>

## Quality Content Deserves Quality Markup

<p>You’ll find no greater advocate of great content than me. The SEO industry loses its collective mind whenever Google rolls out a major search update. The response to the hysteria is always the same: make quality content. To that I add: mark it up properly.</p>

<p>Familiarize yourself with the documentation and be clear on what your site is about. Every piece of information you tag makes it that much easier for it to be indexed and shared with the right people.</p>

<p>Whether you’re a Google devotee or a DuckDuckGo convert, the spirit remains the same. It’s not about ranking so much as it is about making websites as good as possible. Accommodating structured data will make other aspects of your website better.</p>

<p>You don’t need to trust tech to understand what your content is about &mdash; you can tell it. From reviews to recipes to audio search, developers can add a whole new level of sophistication to their content.</p>

<p>The heart and soul of optimizing a website for search have never changed: produce great content and make it as clear as possible what it is and why it’s useful. Structured data is another tool for that purpose, so use it.</p>

{{< signature "ra, yk, il" >}}
