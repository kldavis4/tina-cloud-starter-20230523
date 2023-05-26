---
title: 'Developing For The Semantic Web'
slug: developing-semantic-web
author: frederick-o-brien
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d387422a-3e36-4270-afd1-f2586c699cd8/developing-semantic-web.png
date: 2020-10-07T10:30:00.000Z
summary: >-
  The dream of a machine-readable Internet is as old as the Internet itself, but only in recent years has it really seemed possible. As major websites take strides towards data-fying their content, now’s the perfect time to jump on the bandwagon.
description: >-
  The dream of a machine-readable Internet is as old as the Internet itself, but only in recent years has it really seemed possible. As major websites take strides towards data-fying their content, now’s the perfect time to jump on the bandwagon.
categories:
  - Design
  - Accessibility
---

In July the [Wikimedia Foundation announced Abstract Wikipedia](https://www.neowin.net/news/new-wiki-project---abstract-wikipedia---will-boost-content-across-languages/), an attempt to markup knowledge that is language-independent. In many respects, this is the culmination of decades of buildup, during which the dream of a Semantic Web has never quite taken off, but never quite disappeared either.

As a matter of fact the Semantic Web is growing, and as it renews its mission we all stand to gain from incorporating semantic markup into our websites, be they personal blogs or social media giants. Whether you care about sophisticated web experiences, SEO, or fending off the tyranny of web monopolies, the Semantic Web deserves our attention.

The benefits of developing for the Semantic Web are not always immediate, or visible, but every site that does strengthens the foundations of an open, transparent, decentralized internet.

## The Semantic Web

What exactly is the Semantic Web? It is a machine-readable web, providing through metadata “a common framework that allows data to be shared and reused across application, enterprise, and community boundaries."

The idea is as old as the World Wide Web itself. Older, in fact. It was a focal point of Tim Berners-Lee's 1989 proposal. As he outlined, not only should documents form webs, but the data *inside* them should too:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10ed965d-d1d1-480f-874c-96df72a62fde/tim-berners-lee-web-proposal-diagram.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10ed965d-d1d1-480f-874c-96df72a62fde/tim-berners-lee-web-proposal-diagram.png" sizes="100vw" caption="A diagram from <a href='https://www.w3.org/History/1989/proposal.html'>Sir Tim Berners-Lee's original proposal for the World Wide Web</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10ed965d-d1d1-480f-874c-96df72a62fde/tim-berners-lee-web-proposal-diagram.png'>Large preview</a>)" alt="Diagram from Tim Berners-Lee’s World Wide Web proposal to CERN" >}}

The Semantic Web’s tread a rocky road in the decades since. Since the turn of the millennium, it has morphed into multiple concepts &mdash; open data, knowledge graphs &mdash; all effectively meaning the same thing: webs of data.

{{% feature-panel %}}

[As the W3C summarises](https://www.w3.org/RDF/Metalog/docs/sw-easy), it is “an extension of the current web in which information is given well-defined meaning, better-enabling computers and people to work in cooperation."

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff33886f-8617-40d9-be8d-af53135739d8/aaron-swartz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff33886f-8617-40d9-be8d-af53135739d8/aaron-swartz.png" sizes="100vw" caption="Aaron Swartz speaking in 2012. Photograph by <a href='https://commons.wikimedia.org/wiki/File:Aaron_swartz_6722391455.jpg'>Daniel J. Sieradski</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff33886f-8617-40d9-be8d-af53135739d8/aaron-swartz.png'>Large preview</a>)" alt="Aaron Swartz speaking in front of a crowd" >}}

The idea has had its fair share of advocates. Internet hacktivist Aaron Swartz wrote a book manuscript about the Semantic Web called [*A Programmable Web*](https://upload.wikimedia.org/wikipedia/commons/3/3f/Aaron_Swartz_s_A_Programmable_Web_An_Unfinished_Work.pdf). In it he wrote:

<blockquote>“Documents can’t really be merged and integrated and queried; they serve mostly as isolated instances to be viewed and reviewed. But data are protean, able to shift into whatever shape best suits your needs.”</blockquote>

For a variety of reasons, the Semantic Web has not taken off in the same way the Web has, though it is catching up. Several markups have tried to seize the mantle over the years &mdash; RDFa, OWL, and Schema to name a few &mdash; though none have become standard in the way, say, HTML or CSS have. The barrier to entry was too high.

However, the dream of the Semantic Web has endured, and as more and more sites incorporate it into their designs there’s all the more reason to join the party. The more sites that get on board, the stronger the Semantic Web becomes.

### Further Reading

- [*Data Intelligence*](https://www.data-intelligence-journal.org/#)
- [The Semantic Web](https://www-sop.inria.fr/acacia/cours/essi2006/Scientific%20American_%20Feature%20Article_%20The%20Semantic%20Web_%20May%202001.pdf), a 2001 article by Tim Berners-Lee, James Hensley, and Ora Lassila
- [Credible Web Community Group](https://www.w3.org/community/credibility/) at W3C

## Knowledge Without Borders

Before getting into the weeds of *how* to design for the Semantic Web, it’s worth digging a little deeper into the *why*. What does it matter whether data is connected? Aren’t connected documents enough?

There are several reasons why the Semantic Web continues to be pushed by those who care about a free and open internet. Understanding those reasons is essential to the implementation process. It shouldn’t be a case of ‘eat your vegetables, use semantic markup.’ The Semantic Web is something to believe in and be a part of.

Benefits of the Semantic Web include:

- Richer, more sophisticated web experiences
- Bypassing content silos and internet monopolies
- Improved search engine readability and rankings
- Democratisation of information

Most of these can be traced back to a core tenet of the Semantic Web: a universal language for data. Although the internet has already done wonders for international communication, there’s no escaping the fact some countries have it much better than others. Take languages used on the web vs. languages used in the real world, for example. The eagle-eyed among you may be able to spot a slight imbalance in the data below...

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14929159-271e-444e-98b5-90a7510143e4/languages-online-vs-real-world.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14929159-271e-444e-98b5-90a7510143e4/languages-online-vs-real-world.png" sizes="100vw" caption="The proportion of languages used on <a href='https://w3techs.com/technologies/overview/content_language'>the web</a> do not match up with those used in <a href='https://www.indexmundi.com/world/languages.html'>the real world</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14929159-271e-444e-98b5-90a7510143e4/languages-online-vs-real-world.png'>Large preview</a>)" alt="Bar chart comparing languages spoken online and in real life" >}}

The borderless utopia of the web is not as close as it might seem to those of us inside the English-speaking bubble. Is that something to chastise anyone for? Not necessarily, but it is something to face up to. Doing so highlights the importance of markup that bridges those gaps. **By enriching the data of the web, we take the strain off of its languages.**

This is the crux of the recently announced [Abstract Wikipedia](https://meta.wikimedia.org/wiki/Abstract_Wikipedia/July_2020_announcement), which will attempt to decouple articles from the language they happen to be written in. Wikimedia Executive Director Katherine Maher writes: “Using code, volunteers will be able to translate these abstract ‘articles’ into their own languages. If successful, this could eventually allow everyone to read about any topic in Wikidata in their own language.”

Abstract Wikipedia creator Denny Vrandečić has been a Semantic Web advocate for years, recognizing its potential to unlock untapped potential online. Breaking down national barriers is essential to that process.

<blockquote>“No matter what language you publish your content in, you are going to miss out on including the vast majority of people in the world. The Web gave us this wonderful opportunity to have global reach &mdash; but by relying on a single language, or a small set of languages, we are squandering this opportunity. While the most important objective is to create good content in the first place, you invite more people to participate in the development of better content by being language-independent. It helps you lower the barriers to contribution and consumption, and it allows for many more people to benefit from that effort.”<br /><br />&mdash; Denny Vrandečić, Abstract Wikipedia creator</blockquote>

A timely example of this has been data visualization during the COVID-19 pandemic. The virus has wreaked unspeakable havoc worldwide, but it has also been a shining moment for open data networks, allowing superb web apps, reporting, and more to be common across the web.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cacad799-e4ac-43c4-8f21-f821b9fd6752/ncovid2019-live-homepage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cacad799-e4ac-43c4-8f21-f821b9fd6752/ncovid2019-live-homepage.png" sizes="100vw" caption="The <a href='https://ncov2019.live/'>ncovid2019.live</a> dashboard was made by American high schooler Avi Schiffman and pulls data from WHO, the CDC, and COV19. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cacad799-e4ac-43c4-8f21-f821b9fd6752/ncovid2019-live-homepage.png'>Large preview</a>)" alt="Homepage of ncovid2019.live" >}}

And of course, when data is transparent and easily accessible, it makes it easier to identify anomalies… or straight up deceit. Widespread public access to the kind of information above would be unthinkable even 20 years ago. Now we expect it, and smell a rat when it’s denied us. Data is *powerful*, and if we want to, can be wielded for good.

Similarly, checking ourselves out of content silos &mdash; a hallmark of the modern web experience &mdash; takes power away from web monopolies like Google, Facebook, and Twitter. We’re so used to third party platforms deciphering and presenting information that we forget they’re not strictly necessary.

<blockquote>“If we had shared formats, shared protocols, we might still end up with certain providers playing a large role in certain markets &mdash; think of Gmail for email &mdash; but everyone is free to move to another provider, and the market remains competitive.”<br /><br />&mdash; Denny Vrandečić, Abstract Wikipedia creator</blockquote>

The Semantic Web is silo-less; it is free, open, and abstract, enabling communication between different languages and platforms that would be far more difficult otherwise.

{{% ad-panel-leaderboard %}}

## Data-fying Online Content

Designing for the Semantic Web boils down to data-fying online content &mdash; looking at your content and seeing what can (and should) be abstracted. What does this mean in practical terms, beyond vaguely agreeing it’s a worthwhile thing to do? It depends:

1. If starting a project from scratch, incorporate Semantic Web considerations into what you do. As a website takes shape, weave semantic markup into its DNA.
2. If updating or rebuilding a project, assess what could be woven into the Semantic Web that currently isn’t, then implement.

Both cases basically amount to data-fying content. In this section, we will go through some examples of data abstraction and how it can make content better, smarter, and more widely available. 
 
### Abstracting Information

**Designing and developing for the Semantic Web means looking at online content with your data hat on.** Most of us experience the web as a series of connecting documents or pages; what you want to do with the Semantic Web is connect information. This means assessing your content for data points then adjusting the design based on what you find.

Semantic Web advocate James Hendler outlines this process particularly well with his [DIVE ethos](https://youtu.be/FchE3ktj7U0). (*DIVE* into the data, eh? Eh?). It breaks down as follows:

- **Discover**  
Find datasets and/or content (including outside your own organization).
- **Integrate**  
Link the relations using meaningful labels.
- **Validate**  
Provide inputs to modeling and simulation systems.
- **Explore**  
Develop approaches to turn data into actionable knowledge.

Developing for the Semantic Web is largely about having that birds-eye view of the things you make, and how it potentially feeds into infinitely richer web experiences. As Hendler says, actionable knowledge is the goal. 

This really can be applied to almost any type of web content, but let’s start with a common example: **recipes**. Let’s say you run a cooking blog, with new recipes every Thursday. If you’re French and post a smashing soufflé recipe on your personal blog in plain text, it’s only useful to those who can read French. 

However, by implementing semantic markup the blog can be transformed into a machine-readable recipe data set. Syntax exists for cooking terms to be abstracted. Schema, for example, which can work alongside Microdata, RDFa, or JSON-LD, has markup including:

- prepTime
- cookTime
- recipeYield
- recipeIngredient
- estimatedCost
- nutrition, breaking down into calories and fatContent
- suitableForDiet.

I could go on. The full range of options, with examples, can be read at [Schema.org](https://schema.org/Recipe). In adding them to the post format the format of the recipe needn’t change at all &mdash; you’re simply putting the information in terms computers can understand.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/755a8123-695d-4232-b17c-adf042acbb87/bbc-good-food-cottage-pie-screenshot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f47b544-f7ae-4691-8c87-bad6b8ae80f9/bbc-good-food-cottage-pie-screenshot-preview.png" sizes="100vw" caption="By converting editorial content into data, BBC recipes massively increase their potential usefulness. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/755a8123-695d-4232-b17c-adf042acbb87/bbc-good-food-cottage-pie-screenshot.png'>Click for large preview</a>)" alt="Screenshot of a BBC cottage pie recipe" >}}

For example, everything highlighted blue in the BBC recipe above has also been given semantic markup &mdash; from cooking time to nutritional content. You can see what’s going on under the hood by entering [the recipe URL](https://www.bbcgoodfood.com/recipes/cottage-pie) into Google’s [Rich Results Test](https://search.google.com/test/rich-results). Note the ‘Add to shopping list’ functionality, an example of connection made possible by Semantic Web implementation. Good content becomes usable data. 

Most of us have crossed paths with this kind of sophistication via search results, but the applications are much wider than that. Semantic markup of recipes makes it easier for websites to be found and used by home assistants. Listed ingredients can be ordered from the local supermarket. Recipes could be filtered in all sorts of ways &mdash; for diets, allergies, religion, cost, you name it. Or let's say you had a limited number of ingredients in the house. With a database you could input those ingredients and see what recipes fit the bill.

The range of possibilities really do border on limitless. As Swartz said, data is protean. Once you have it you can use it in all sorts of weird and wonderful ways. This piece is not about those weird and wonderful ways so much as it is about making them possible. **Designing for the Semantic Web makes subsequent design infinitely richer.**

Here’s a more personal example to show what I mean. A couple of friends and I run a little music webzine as a hobby. Though we publish the odd article or interview, the ‘main event’ is our weekly album reviews, in which the three of us each assign a score, choose favorite tracks, and write summaries. We’ve been going for more than five years, which means we have close to 250 reviews, which means an awful lot of potential data. We didn’t realize how much until we started redesigning the site. 

I touched upon this in a piece about [baking structured data into the design process](https://www.smashingmagazine.com/2020/04/structured-data-design-process/). In dissecting our reviews we realized they were chock full of information that could be given semantic markup. Artists, album names, artwork, release date, individual scores, overall scores, release type, and more. What’s more &mdash; and this is where it gets really exciting &mdash; we realized we could connect to an existing database: MusicBrainz.

This two-way approach is the crux of the Semantic Web. When our music website relaunches it will be its own open data source with thousands of unique data points. Connecting to an existing music database will give our own data more context &mdash; and potential. Thousands of data points becomes tens of thousands of data points, maybe more.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe3e9f5-a074-40ce-a5ae-7845aa52dd08/updated-audioxide-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe3e9f5-a074-40ce-a5ae-7845aa52dd08/updated-audioxide-web.png" sizes="100vw" caption="With some simple semantic markup, seemingly innocuous web pages can become the centre of an huge information network. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe3e9f5-a074-40ce-a5ae-7845aa52dd08/updated-audioxide-web.png'>Large preview</a>)" alt="Chart showing how semantic markup connects on an album review" >}}

The graphic above only scratches the surface of how much information will be connected to reviews pages. The content is the same as it was before, only now it is plugged into a metadata ecosystem &mdash; the [Giant Global Graph](https://www.cnet.com/news/bye-bye-world-wide-web-welcome-giant-global-graph/), as Berners-Lee once called it. 

Developing for the Semantic Web means identifying your own data, markup it up, then sussing out how it connects to other data. Because it does. It always does. And that process is how this…

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8657fdeb-0ba7-4c28-980f-38d651e8e7e6/tim-berners-lee-data-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8657fdeb-0ba7-4c28-980f-38d651e8e7e6/tim-berners-lee-data-web.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8657fdeb-0ba7-4c28-980f-38d651e8e7e6/tim-berners-lee-data-web.png'>Large preview</a>)" alt="Illustration showing how semantic data connects across web pages" >}}

… in time becomes this…

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094d2a37-408d-438a-997e-6c93811612b3/linked-open-data-cloud.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094d2a37-408d-438a-997e-6c93811612b3/linked-open-data-cloud.png" sizes="100vw" caption="<a href='https://lod-cloud.net/'>The Linked Open Data Cloud</a>, a constantly updating visualisation of the state of linked data online. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094d2a37-408d-438a-997e-6c93811612b3/linked-open-data-cloud.png'>Large preview</a>)" alt="The Linked Open Data Cloud" >}}

The second image is The Linked Open Data Cloud, a constantly updating visualization of the web’s connected data. That red hive of connections is the sciences; the rest has some way to go. That’s where we come in. 

### Useful Semantic Web Resources

- [RDF at w3schools.com](https://www.w3schools.com/xml/xml_rdf.asp)
- [W3C’s RDF validator](https://www.w3.org/RDF/Validator/)
- “[The Semantic Web Made Easy](https://www.w3.org/RDF/Metalog/docs/sw-easy)” by W3C
- “[Whatever Happened to the Semantic Web?](https://twobithistory.org/2018/05/27/semantic-web.html)” by Two-Bit History 
- [JSON-LD generator](https://hallanalysis.com/json-ld-generator/)
- [Google’s Structured Data Markup Helper](https://www.google.com/webmasters/markup-helper/u/0/)

{{% ad-panel-leaderboard %}}

## Plugging In

The ideal of the Semantic Web is connection. Make data, share data, demand data. Be part of an information ecosystem. When you’re creating original data, great. Share it. When data already exists and you’d like to use it, pull it in. 

Here are just a handful of the data resources out there:

- [DPpedia](https://wiki.dbpedia.org/)
- [MusicBrainz](https://musicbrainz.org/)
- [WorldCat](https://www.worldcat.org/default.jsp)
- [ISBNdb](https://isbndb.com/)

Indeed, where databases like these exist, I’d go so far as to say the right thing to do would be update them where they’re lacking information. Why keep it to yourself? Become a contributor, a Semantic Web advocate. 

### Implementation

As far as building Semantic Webness into your sites goes, I’m certainly not advocating manual, doc-by-doc markup. Who’s got time for that? More often than not the solution is a case of standardizing a format and templating for it. 

Templating is the big opportunity here. How many people really have time to markup all that information manually? However, if you have custom inputs, you get the best of both worlds. Content can be filled with people-friendly information and the information exists as data ready to serve whatever purpose comes to mind.

Take, for example, a static site generator like [Eleventy](https://www.11ty.dev/), which has been enjoying a bit of a love-in from the dev community lately. You write a post, run it through a template, and you’re golden. So why not incorporate semantic markup into the template itself?

Like Eleventy, the new version of our music webzine site uses Markdown for its posts. While we have the same old text posts we always did, every review now also includes the following metadata inputs, which are then pulled into the template: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffd46472-86b5-445d-b90e-5005596f9d80/audioxide-review-metadata.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffd46472-86b5-445d-b90e-5005596f9d80/audioxide-review-metadata.png" sizes="100vw" caption="Incorporating metadata inputs into templates allows content to be converted into data, and at most adds a couple of minutes to any given post upload. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffd46472-86b5-445d-b90e-5005596f9d80/audioxide-review-metadata.png'>Large preview</a>)" alt="Metadata inputs in a Markdown document" >}}

Together with author details in the body of the post and some generic website info, this then translates to the following semantic markup:

<div class="break-out">

<pre><code class="language-javascript">&lt;script type="application/ld+json"&gt;
	{
  "@context": "https://schema.org/",
  "@type": "Review",
  "reviewBody": "One of the definitive albums released by, quite possibly, the greatest singer-songwriter we've ever seen. To those looking to probe Young's daunting discography: start here.",
  "datePublished": "2020-08-14",
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
  	"name": "After the Gold Rush",
  	"@id": "https://musicbrainz.org/release-group/b6a3952b-9977-351c-a80a-73e023143858",
  	"image": "https://audioxide.com/images/album-artwork/after-the-gold-rush-neil-young.jpg",
  	"albumProductionType": "https://schema.org/StudioAlbum",
	"albumReleaseType": "https://schema.org/AlbumRelease",
  	"byArtist": {
    	"@type": "MusicGroup",
    	"name": "Neil Young",
    	"@id": "https://musicbrainz.org/artist/75167b8b-44e4-407b-9d35-effe87b223cf"
  	}
  },
  "reviewRating": {
	"@type": "Rating",
	"ratingValue": 27,
	"worstRating": 0,
	"bestRating": 30
  },
  "publisher": {
  	"@type": "Organization",
  	"name": "Audioxide",
  	"description": "Independent music webzine founded in 2015. Publishes reviews, articles, interviews, and other oddities.",
  	"url": "https://audioxide.com",
  	"logo": "https://audioxide.com/logo-location.jpg",
  	"sameAs" : [
	"https://facebook.com/audioxide",
	"https://twitter.com/audioxide",
	"https://instagram.com/audioxidecom"
  ]
	}
}
    
	&lt;/script&gt;</code></pre>
</div>

Where before there was just text, on every single review page there will now also be machine-readable versions of [what readers see when they visit the site](https://audioxide.com/reviews/neil-young-after-the-gold-rush/). The words are all still there, the content has barely changed at all &mdash; it’s just been data-fyed. From rich search results to interactive review statistics pages, this massively increases what’s possible. The road ahead is wide and open. It also gives us a stake in MusicBrainz’s future. By connecting their data to our own data, we in turn want to see it do well, and will do our part to ensure it does. 

The appropriate semantic markup depends on the nature of a website, but odds are it exists. Start with the obvious inputs (date, author, content type, etc.) and work your way into the weeds of the content. The first step could be as simple as a [hCard](https://microformats.org/wiki/h-card) (a kind of digital ID card) for your personal website. Print out screenshots of pages and start annotating. You’ll be amazed by how much content can be data-fyed.

## Beyond Imagination

Designing and developing for the Semantic Web is a practice that dates back to the Internet’s founding ideals. Whether you value beautiful, informative data visualization, want more sophisticated search results, wish to remove power from web monopolies, or simply believe in free and open information, the Semantic Web is your ally. 

Aaron Swartz closed his manuscript with a call to hope:

<blockquote>“The Semantic Web is based on bet, a bet that giving the world tools to easily collaborate and communicate will lead to possibilities so wonderful we can scarcely even imagine them right now.”</blockquote>

Abstract Wikipedia Denny Vrandečić echoes those sentiments today, saying:

<blockquote>“There’s a need for a web infrastructure that will facilitate interoperability between services, which requires a common set of standards for representing data, and common protocols across providers.”</blockquote>

The Semantic Web has limped along long enough for it to be clear that a silver bullet language is unlikely to appear, but there are enough now peacefully coexisting for Berners-Lee’s founding dream to be a reality for most of the web. Each of us can be advocates in our own neighborhoods.

### Be Better, Demand Better

As Tim Berners-Lee has said, the Semantic Web is a culture as much as it is a technical hurdle. In [a 2009 TED Talk](https://www.youtube.com/watch?v=OM6XIICm_qo&feature=youtu.be) he summed it up nicely: **make linked data, demand linked data**. That’s truer now than ever. The World Wide Web is only as open and connected and good as we force it to be. Whenever you make something online ask yourself, “How can this plug into the Semantic Web?” The answers will add new dimensions to the things we create, and create unimaginably wonderful new possibilities for years to come.

{{< signature "ra, yk, il" >}}
