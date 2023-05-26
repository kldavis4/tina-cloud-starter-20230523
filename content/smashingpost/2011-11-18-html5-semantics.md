---
title: Sexy New HTML5 Semantics
slug: html5-semantics
image: null
date: 2011-11-18T16:40:10.000Z
author: bruce-lawson
description: >-
  Much of the excitement we’ve seen so far about HTML5 has been for the new APIs: local storage, application cache, Web workers, 2-D drawing and the like. But let’s not overlook that **HTML5 brings us 30 new elements to mark up documents and applications**, boosting the total number of elements available to us to over 100.
categories:
  - Coding
  - HTML5
  - HTML
  - Semantics
---
<a href="https://www.brucelawson.co.uk/2011/html5-and-hollow-demos/">Sexy yet hollow demos</a> aside, even the most JavaScript-astic Web 2.0-alicious application will likely have textual content that needs to be marked up sensibly, so let’s look at some of the new elements to make sure that your next project is as semantic as it is interactive.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/html-5-cheat-sheet-pdf/)
*   [Learning to Love HTML5](https://www.smashingmagazine.com/2010/11/learning-to-love-html5/)
*   [<span class="headline">The Importance Of HTML5 Sectioning Elements</span>](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)

To keep this article from turning into a book, we won’t look at each in depth. Instead, this is a taster menu: you can see what’s available, and there are links that I’ve vetted for when you want to learn more.

{{% feature-panel %}}

Along the way, we’ll see that HTML5 semantics are carefully designed to extend the current capabilities of HTML, while always enabling users of older browsers to access the content. We’ll also see that semantic markup is not “nice to have,” but is rather a cornerstone of Web development, because it is what enhances <strong>accessibility, searchability, internationalization and interoperability</strong>.

A human language like English, with its vocabulary of a million words, can't express every nuance of thought unambiguously, so with only 100 or so words that we can use in HTML, there will be situations when it's not clear-cut which element to use for which piece of content. In that case, choose one; be consistent across the site.</p>

## Some Presentational Elements Are Gone

Purely presentational elements such as <code>center</code>, <code>font</code> and <code>big</code> are now obsolete. Their role has been perfectly usurped by Cascading Style Sheets. Now, this doesn’t mean you have to rush out and recode all of those ancient pages; HTML5 makes them obsolete for authors, but because HTML5 strives not to break the Web, browsers will still render those cobwebbed legacy pages.

For the same reason, presentational attributes have been removed from current elements; for example, <code>align</code> on <code>img</code>, <code>table</code>, <code>background</code> on <code>body</code>, and <code>bgcolor</code> on <code>table</code>.

The evil <code>frame</code> element is absent in HTML5. Frames caused usability and accessibility nasties. If you get the urge to use them, use an older <code>DOCTYPE</code> so that your pages still validate.

Beyond this short overview, see the W3C’s exhaustive list of <a href="https://www.w3.org/TR/html5-diff/#absent-elements">removed elements and attributes</a>.</p>

## Some Presentational Elements Have Been Redefined To Be Semantic

Not all presentational elements have been taken out and shot. Some have undergone an extensive re-education program and emerged with shiny new semantics. For example, the <code>small</code> element no longer means “use a small font,” although it will display that way in browser style sheets. Now it represents side comments, such as small print:
<blockquote>Small print typically features disclaimers, caveats, legal restrictions, or copyrights. Small print is also sometimes used for attribution, or for satisfying licensing requirements.</blockquote>

Some of the redefinitions feel to me to be a mop-up. While I can get behind <code>&lt;b&gt;</code> for drawing attention to product names, keywords and so forth, without any special emphasis implied, specifying the semantics for marking up ship names (<code>&lt;i&gt;</code>, if you’re so inclined) feels weirdly precise. But I get seasick, and your nautical mileage may vary. With similar niche precision:
<blockquote>The <code>u</code> element [now] represents a span of text with an unarticulated, though explicitly rendered, non-textual annotation, such as labeling the text as being a proper name in Chinese text (a Chinese proper name mark), or labeling the text as being misspelt.</blockquote>

You can read more about <a href="https://www.w3.org/TR/html5-diff/#changed-elements">changed elements and attributes</a> on the W3C website.</p>

## Sexy New Semantics

We all know about <a href="https://dev.opera.com/articles/view/introduction-html5-video/"><code>video</code></a> and <code>audio</code>. And <code>canvas</code> is particularly popular at the moment because it allows for 3-D graphics using webGL, so game designers can port their products to the Web. Like good ol’ <code>img</code>, these semantics are embedded content, because they drag in content from another source — either a file, a data URI or JavaScript.

Unlike <code>img</code>, however, they have opening and closing tags, allowing for fallbacks. Therefore, browsers that don’t support the new semantics can be fed some content: an image could be the fallback for a canvas, for example, or a Flash movie could be the fallback for <code>video</code>, a technique called “<a href="https://camendesign.com/code/video_for_everybody">video for everybody</a>.”

The <code>source</code> and <code>track</code> elements are empty elements (with no closing tags) that are children of <code>video</code> or <code>audio</code>.

The <code>source</code> element gets past the codec Tower of Babel that we have. Each element points to a different source file (WebM, MP4, Ogg Theora), and the browser will play the first one it knows how to deal with:

<pre><code class="language-markup">
&lt;audio controls&gt;
  &lt;source src=bieber.ogg type=audio/ogg&gt;
  &lt;source src=bieber.mp3 type=audio/mp3&gt;
    &lt;!-- fallback content: --&gt;
    Download &lt;a href=bieber.ogg&gt;Ogg&lt;/a&gt; or &lt;a href=bieber.mp3&gt;MP3&lt;/a&gt; formats.
&lt;/audio&gt;
</code></pre>

In this example, Opera, Firefox and Chrome will download the Ogg version of Master Bieber’s latest toe-tappin’ masterpiece, while Safari and IE will grab the MP3 version. Chrome can play both Ogg and MP3, but browsers will download the first source file that they understand. The fallback content between the opening and closing tags is a link to download the content to the desktop and play it via a separate media player, and it is only shown in browsers that can’t play native multimedia.

For video, you could use an embedded Flash movie hosted on YouTube:

<pre><code class="language-markup">
&lt;video controls&gt;
  &lt;source src=best-video-ever.webm type=video/webm&gt;
  &lt;source src=best-video-ever.mp4 type=video/mp4&gt;
    &lt;!-- fallback content: --&gt;
    &lt;iframe width="480" height="360" 
      src="https://youtube.com/embed/xzMUyqmaqcw?rel=0" 
      frameborder="0" allowfullscreen&gt;
    &lt;/iframe&gt;
&lt;/video&gt;
</code></pre>

This way, users of older browsers, such as IE 6-8, will see a YouTube movie (as long as they have the Flash Player), so they will at least be able to see the video, while users with modern browsers will get the full native-video experience. Everyone gets the content, then, which is what your website is there for, after all.

The <code>track</code> element is a newer addition to the HTML5 family and is being implemented by Opera, Chrome and IE at the moment. It points to a subtitle file that contains text and timing information. When implemented, it synchronizes captions with the media file to enable on-demand subtitling and captioning; useful not only for viewers who are hard of hearing, but also for those who do not speak the language used in the audio or video file.</p>

## Semantics For Internationalization

Less woo! than the semantics for multimedia and games are the semantics for internationalization. It may surprise the cool kids in Silicon Valley to learn that a worldwide Web of people use languages other than English and even use different writing systems.

Languages such as Arabic and Hebrew are written right to left, unlike European languages, which are written left to right. On pages that use only one writing system, this doesn’t present a problem, but on pages with bi-directional (“bidi”) writing, browsers have to decide where to put punctuation, bullets, numbers and the like. Browsers usually do a pretty good job using the Unicode bidirectional algorithm, but it gets it wrong in some cases, which can seriously dent the comprehensibility of content.

HTML5 gives us a <code>bdi</code> element, which enables authors to override the Unicode bidirectional algorithm and make their text more comprehensible. For a further description of the problem and to see how <code>bdi</code> solves it, see “<a href="https://rishida.net/blog/?p=564">HTML5’s New <code>bdi</code> Element</a>” by <a href="https://twitter.com/r12a">Richard Ishida</a>, the W3C’s internationalization activity lead.

Some languages have scripts that are not alphabetic at all, but that express an idea rather than a sound. Occasionally, an author will have to assist readers with pronunciation for especially rare or awkward characters, usually by providing an alternate script in a small font above the relevant character. In print, this was traditionally done with a very small 5-point font called “ruby,” and HTML5 gives us three new elements for marking up ruby text: <code>ruby</code>, <code>rt</code> and <code>rp</code>.

For more information, see “<a href="https://my.opera.com/tagawa/blog/the-html5-ruby-element-in-words-of-one-syllable-or-less">The HTML5 <code>ruby</code> Element in Words of One Syllable or Less</a>” by Daniel Davis.

## Structural Semantics

Most people are aware that HTML5 gives us many new elements to describe parts of a Web page, such as <code>header</code>, <code>footer</code>, <code>nav</code>, <code>section</code>, <code>article</code>, <code>aside</code> and so on. These exist because we Web developers actually wanted such semantics. How did the authors of the HTML5 specification know this? Because in 2005 <a href="https://code.google.com/webstats/">Google analyzed 1 billion pages</a> to see what authors were using as class names on <code>div</code>s and other elements. More recently, in 2008, Opera MAMA analyzed 3 million URLs to see the <a href="https://devfiles.myopera.com/articles/572/classlist-url.htm">top class names</a> and <a href="https://devfiles.myopera.com/articles/572/idlist-url.htm">top IDs</a> used in the wild. These analyses revealed that authors wanted to mark up these areas of the page but had no elements to do so, other than the humble and generic <code>div</code>, to which they then added descriptive classes and IDs.

(HTML5 Doctor has many articles about <a href="https://html5doctor.com/article-archive/">HTML5 semantics</a>, so we won’t bloat this article by going in depth here. Warning: some were written by me.)

The new semantics were built to degrade gracefully. For example, consider what the specification has to say about the new <code>figure</code> element:
<blockquote>The <code>figure</code> element represents some flow content, optionally with a caption, that is self-contained and is typically referenced as a single unit from the main flow of the document.

The element can thus be used to annotate illustrations, diagrams, photos, code listings, etc…</blockquote>

This isn’t a new idea. HTML3 proposed a <a href="https://www.w3.org/MarkUp/html3/figures"><code>fig</code> element</a> (which never made it into the final HTML 3.2 specification). It looked like this:

<pre><code class="language-markup">
&lt;FIG SRC="nicodamus.jpeg"&gt;
   &lt;CAPTION&gt;Ground dweller: &lt;I&gt;Nicodamus bicolor&lt;/I&gt; builds silk snares&lt;/CAPTION&gt;
   &lt;P&gt;A small hairy spider.
   &lt;CREDIT&gt;J. A. L. Cooke/OSF&lt;/CREDIT&gt;&lt;/P&gt;
&lt;/FIG&gt;
</code></pre>

There’s a big problem with this. In browsers that do not support <code>fig</code> (and none do), the image wouldn’t be displayed because the <code>fig</code> element would be completely ignored. The contents of the <code>credit</code> element would be displayed, because it’s just text. So you'd get a credit with no image on older browsers.

In HTML5, you would code the same example like so:

<pre><code class="language-markup">
&lt;figure&gt; 
&lt;img src="nicodamus.jpeg"&gt; 
   &lt;figcaption&gt;
      &lt;p&gt;Ground dweller: &lt;i&gt;Nicodamus bicolor&lt;/i&gt; builds silk snares.&lt;/p&gt;
      &lt;p&gt;A small hairy spider.
      &lt;small&gt;J. A. L. Cooke/OSF&lt;/small&amp;gt&lt;/p&gt;
   &lt;/figcaption&gt;
&lt;/figure&gt;
</code></pre>

Unlike the aborted HTML3 syntax, the HTML5 version is backwards-compatible: a browser that doesn’t “know” about the <code>figure</code> element will still show the <code>img</code> and the text inside <code>figcaption</code> (as the HTML3 <code>credit</code> element would similarly display its content). Note that we’re using the redefined <code>small</code> element, instead of minting a new <code>credit</code> element. Remember that “Small print is also sometimes used for attribution.”

HTML5 also gives us a new <code>figcaption</code> element. Originally, the specification’s authors tried to reuse <code>caption</code>, as suggested in HTML3, but there were legacy problems, because <code>caption</code> had previously only been a child of <code>table</code>.

One of the <a href="https://www.w3.org/TR/html-design-principles/">design principles on which HTML5 is based</a> is that new features should <a href="https://www.w3.org/TR/html-design-principles/#degrade-gracefully">degrade gracefully</a>. When they can’t, the language allows for fallback content. It tries to reuse elements rather than mint new ones — but it’s a pragmatic language: when minting something new is necessary, it does so.</p>

## Interactive Semantics

The structural elements of HTML5 currently don’t do much in visual browsers, although software that sits on top of browsers (such as screen readers) are starting to use them (see “<a href="https://www.accessibleculture.org/articles/2011/04/html5-aria-2011/">HTML5, ARIA Roles, and Screen Readers in March 2011</a>“ and “<a href="https://www.accessibleculture.org/articles/2011/10/jaws-ie-and-headings-in-html5/">JAWS, IE and Headings in HTML5</a>.”)

Other elements do have a visual effect. The <a href="https://html5doctor.com/the-details-and-summary-elements/"><code>details</code> element</a>, for example, is a groovy interactive element that functions as “a disclosure widget from which the user can obtain additional information or controls.”

Most browsers will implement it as an “expando box”: when the user clicks on some browser-generated icon (such as a triangle or downwards-pointing arrow) or the word “Details” (which can be replaced by the author’s own rubric in a child <code>summary</code>), the element will slide open, revealing its details within. The details could be a full description of an image or graph, a description of a complex table, advanced options for a search form, or just about anything else. This is a common need on the Web today, now made native and obviating the need for custom JavaScript.

Most of us have seen HTML5’s new <a href="https://dev.opera.com/articles/view/new-form-features-in-html5/">form semantics</a>. Most of these are attributes of the <code>input</code> element, thereby ensuring graceful degradation to <code>&lt;input type=text&gt;</code> in older browsers. New elements include <code><a href="https://adactio.com/journal/4272/">datalist</a></code>, <code>output</code>, <code>progress</code> and <code><a href="https://html5doctor.com/measure-up-with-the-meter-tag/">meter</a></code>.</p>

## Do We Have The Right Semantics?

So, we have many new semantics, but are they the right ones? After all, the Google research on which they were based was conducted in 2005 — quite some time ago! Perhaps the semantics are already somewhat behind the times? Many have noted that they’re document-centric rather than application-centric. Do we need more application-centered semantics, such as a <code>login</code> or <code>share</code> element, or some kind of <code>modal</code> element for modal dialogue boxes?

I don’t know; I’m not an app developer. But at least HTML is a “living standard,” and so these can be added if strong enough use cases are presented to the Working Group.

I think most coders would welcome a new way to embed images that respond to the device’s context. Borrowing from the <code>video</code> element, which displays source video according to what media queries instruct, I can imagine a new element such as <code>picture</code>:

<pre><code class="language-markup">
&lt;picture alt="angry pirate"&gt;
   &lt;source src=hires.png media="min-width:800px"&gt;
   &lt;source src=midres.png media="min-width:480px"&gt;
   &lt;source src=lores.png&gt;
      &lt;!-- fallback for browsers without support --&gt;
      &lt;img src=midres.png alt="angry pirate"&gt;
&lt;/picture&gt;
</code></pre>

This would pull in <code>hires.png</code> for widescreen devices, <code>midres.png</code> for devices between 480 and 800 pixels wide, and <code>lores.png</code> for everything else, thereby rendering moot the question that designers currently ask themselves, “Do I make every browser download a high-resolution image and then squash it down for small screens, thus wasting bandwidth, or do I send a low-resolution image to every browser and scale it up for big screens, potentially sacrificing quality?”

Taking a leaf from the other popular semantics we’ve seen, there would be a fallback in the middle — in this case, a conventional <code>img</code> element — so everyone would get the right content.

Sending the right-sized image to devices without wasting bandwidth is one of the knottiest problems in cross-device and responsive design at the moment. Perhaps we’ll see a solution to this in HTML6. At the moment, the best solutions, which include Matt Wilcox’s <a href="https://adaptive-images.com/">Adaptive Images</a> and Filament Group’s <a href="https://github.com/filamentgroup/Responsive-Images">Responsive Images</a>, require JavaScript and tweaks to the server’s <code>htaccess</code> file. The worst solutions require old-fashioned techniques, such as <a href="https://farukat.es/journal/2011/02/499-lest-we-forget-or-how-i-learned-whats-so-bad-about-browser-sniffing">browser-sniffing</a>, now rebranded as “device detection” but still the same old user-agent string-pattern matching, which is <a href="https://webaim.org/blog/user-agent-string-history/">hilariously fragile</a>, not future-proof or scalable, and straight out of the days of “Best viewed in Netscape Navigator at 800 × 600” badges on websites.</p>

### When, Where, Who?

A lot of data depends on three pieces of information: <em>when</em>, <em>where </em>and <em>who</em>?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/257cb1a2-83d2-482b-a2e1-ca207cd5bd80/html5-logo-500.png" alt="HTML5 Semantics" width="450" height="450" />

HTML5 has a <code>time</code> element (which has been a bit of a <a href="https://www.brucelawson.co.uk/2011/goodbye-html5-time-hello-data/">battleground</a> lately). This enables you to annotate a human-readable date with an unambiguous machine-readable one. It doesn’t matter what goes between the tags, because that’s the content for people to read. So, you could use either of the following:

<pre><code class="language-markup">
&lt;time datetime="1982-07-18"&gt;The day the woman I love was born&lt;/time&gt;

&lt;time datetime="1982-07-18"&gt;Priyanka Chopra’s birthday&lt;/time&gt;
</code></pre>

Whichever you choose, the machine would still know the date you mean because of the <code>datetime</code> attribute, formatted as <code>YYYY-MM-DD</code>. If you wanted to add a time, you could: separate the time from the date with a <code>T</code>, and then put the time in 24-hour format, terminated by a <code>Z</code>, along with any time-zone offset. So, <code>2011-11-13T20:00Z</code> would be 8:00 pm on 13 November 2011 UTC, while <code>2011-11-13T23:26.083Z-05.00</code> would be 23:26 pm and 83 milliseconds in the time zone lying 5 hours before UTC. A Sri Lankan-localised browser could use this information to automatically convert dates into Buddhist calendar. Search engines could use timestamps to help <a href="https://www.googleblog.blogspot.com/2011/11/giving-you-fresher-more-recent-search.html">evaluate "freshness"</a>.

It’s perhaps surprising that, even though geolocation is so prevalent now, we don’t have a location element that simply takes three attributes: latitude, longitude and (optionally) altitude. It would be great to be able to write the following:

<pre><code class="language-markup">
&lt;location lat=51.502064 long=-0.131981&gt;London SW1A 4WW&lt;/location&gt;
</code></pre>

The browser would then offer to show you a map or give you directions from the current GPS location or any other location-based service.

(Since I gave the talk that this article is based on, Ian Hickson, the HTML5 editor, said that he expects to add <a href="https://www.netmagazine.com/news/ian-hickson-responds-over-html5-getting-time-element-back-111552">a new &lt;geo&gt; element</a>. If I could choose, I’d prefer <code>place</code>, so I could wear a T-shirt with the slogan "I've got the <code>time</code> if you've got the <code>place</code>".)

<a href="https://www.w3.org/MarkUp/html3/logical.html">HTML3 had a <code>person</code> element</a>, “used for names of people to allow these to be extracted automatically by indexing programs,” but it was never implemented. In HTML4, the <a href="https://www.w3.org/TR/html401/struct/text.html#h-9.2.1"><code>cite</code> element</a> could be used to wrap names of people, but this has been removed in HTML5 — controversially (see “<a href="https://www.24ways.org/2009/incite-a-riot">Incite a Riot</a>” by Jeremy Keith). In HTML5, then, we’re left with no way to unambiguously denote a person. People’s names are, however, a hard problem to solve. Whereas times and dates have well-known standardized ISO formats (<code>YYYY-MM-DD</code> and <code>HH:MM:SS.mmm</code>, respectively), and location is always latitude, longitude and altitude, personal names are harder to break down into useful parts: there are Russian patronymics, Indonesian single-word names, multiple family names, and Thai nicknames to consider. (See Richard Ishida’s excellent article “<a href="https://www.w3.org/International/questions/qa-personal-names">Personal Names Around the World</a>” for more information and discussion.)

The new <a href="https://www.html5doctor.com/time-and-data-element/"><code>data</code> element, which replaces <code>time</code></a>, has a value attribute that passes machine-readable information, but it has no required or implied format, so there is no way for a browser or search engine to know, for example, whether <code>1936-10-19</code> is a date, a part number or a postal code.</p>

## Microdata

HTML5, like HTML4, is extensible (but not in the oh-so-dirty eXtensibility way of XML formats, so loathed by the Working Group). You can use the tried and tested microformats, which use HTML classes, or the full RDFa specification, which doesn’t validate in HTML4 or HTML5. Because RDFa was considered to be too hard for authors to write (Google has conducted research that finds that authors make 30% more mistakes with RDFa than with other formats), HTML5 specifies microdata, a mechanism for adding common semantics via agreed-upon markup patterns. HTML5 Doctor has more information on <a href="https://www.html5doctor.com/tag/microdata/">HTML5 microdata</a>, and <a href="https://www.opera.com/next">Opera 11.60</a> supports the Microdata DOM API.

Like microformats and RDFa, the extra semantics added to the markup make sense only if you have a cheat sheet that tells you what each piece means. This means that the data has to point to a vocabulary that tells any crawler how to interpret the lump of data it finds. For microdata, there is the newly established <a href="https://www.schema.org/">Schema.org</a>, which is “a collection of schemas, i.e. HTML tags, that webmasters can use to mark up their pages in ways recognized by major search providers.”

## Do Semantics Matter Anyway?

Now that more and more markup is generated by JavaScript, some people are tempted to think that semantics don't matter. We see various products marketed as HTML5 which simply make <code>div</code>s fly around the screen with JavaScript  —  simple DHTML techniques unchanged from 10 years ago.

I've even seen some Web pages with no markup at all. Some frameworks emit skeletal HTML with empty <code>body</code> tags and inject all the HTML with script. If you're squirting some minified JavaScript down the wire, with no markup at all, you're closer to Flash than you are to the Web.

In the same way that 47 minutes is (apparently) too long to to struggle making a CSS layout, at which point you should just give up and use tables, some people suggest that thinking about which element to use is a waste of time. "There are two types of developers: those who argue about div's not being semantic and those who create epic shit" writes Thomas Fuchs, as if the two activities were mutually exclusive.

A better argument is that no software cares about or consumes semantics anyway, so why bother? This isn't true (work is underway already to <a href="https://www.paciellogroup.com/blog/2011/11/html5-semantics-and-accessibility/">map assistive technologies to new semantics</a>), but even if it were true, it ignores that this is a chicken-and-egg argument. It assumes that no new search engine will ever come to the market and be able to use new elements, or that browsers will never release new versions that can make use of these semantics, and that developers will write no new extensions  —  in short, it assumes that the evolution of the Web is complete.

<strong>Semantics do matter</strong>. Semantics communicate meaning, and once that is established, machines can do something meaningful with that data, without having to develop and use algorithms to guess. A browser extension might allow a user to jump straight to the <code>nav</code> with a single keystroke. It can do this because it looks for <code>nav</code> rather than having to employ heuristics to find a <code>div</code> with an <code>id</code> or <code>class</code> that would suggest it's being used as navigation (assuming the author decided to use something sensible like nav, navigation, sidebar, or menu  —  and a restaurant site with a <code>div</code> called "menu" might be a list of foods rather than other pages...ah, the ambiguity of natural language). A crawler might dynamically assemble articles on a timeline. There are many more possibilities than my meagre imagination can dream up.

The Web is based on simple technologies, mashed up together to bring surprising results  —  results which have certainly surpassed the inventors' original intents or expectations. The Web will continue to do so. What makes the Web so great, so flexible and so powerful is the fact that content is in open formats that can be parsed and mashed up in new and surprising ways.

These can happen if the content is marked up for meaning by the author  —  and if the language has the right markup elements for authors to use as a vocabulary. <strong>HTML5 extends our vocabulary</strong>. We'll need more words  —  and those will come about with HTML6 etc.

If, like me, you believe the Web to be a system that works across browsers, across operating systems, across devices, across languages, that is View-sourcable, hackable, mash-uppable, accessible, indexable, reusable, then we need to ensure that we use the small number of semantic tools at our disposal properly, and we'll all benefit.

<em>(This article is based on a talk I gave at the <a href="https://fronteers.nl/congres/2011/sessions/html5-semantics-bruce-lawson">Fronteers Conference</a>.)</em>

### About the Author

<img style="float: left;padding: 0 15px 12px 0" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36a60b3e-4741-4982-9ed7-15c14cd0ea0f/bruce-lawson-html5-150.jpg" alt="Introducing HTML5" width="100" height="129" />

<a href="https://twitter.com/brucel">Bruce</a> evangelizes Open Web Standards for <a href="https://www.opera.com/developer">Opera</a>. He wrote the book Introducing HTML5 together with Remy Sharp. The book points out the good and bad parts of HTML5 specifications and shows you how to use the language as well as some areas of spec will be discussed theoretically as they’re not yet implemented anywhere. It's the first full-length book on HTML5 (New Riders, appearing in the 2nd edition).

&nbsp;

<em>(al) (il) (vf)</em>

