---
title: 'Classes? Where We’re Going, We Don’t Need Classes!'
slug: classes-where-were-going-we-dont-need-classes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80957ac4-7fde-4078-b0dd-9763645f25b8/css-tricks-illu-101.jpg
date: 2012-06-19T08:20:39.000Z
author: heydon-pickering
description: >-
  Classes, classes, classes everywhere. What if we don’t need CSS classes at all? What if we stopped worrying about how many classes we’re using and what we should be calling them and just finished with them once and for all?
categories:
  - Coding
  - CSS
  - Opinion Column
  - HTML
---
It would be no revelation to you to say that HTML elements can be styled without recourse to the <code>class</code> attribute, but have you considered the multitude of benefits that come from forgoing classes altogether?

In the article, I’ll demonstrate that the class is as antiquated and inappropriate for styling as the table is for layout, and that omitting them can discipline us to create more usable, reusable content. I appreciate that this is a contentious subject; I’ll meet you in the comments.

(For those who aren’t “of a certain age,” the title of this article is a play on a <a href="https://youtube.com/watch?v=flge_rw6RG0&amp;feature=related">famous line</a> from the 1980s film Back to the Future.)

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Introduction To Object Oriented CSS (OOCSS)](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)
*   [An Ultimate Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)
*   [53 CSS-Techniques You Couldn’t Live Without](https://www.smashingmagazine.com/2007/01/53-css-techniques-you-couldnt-live-without/)

{{% feature-panel %}}

## It’s Not About Maintainability

In her recent presentation “<a href="https://www.slideshare.net/stubbornella/our-best-practices-are-killing-us">Our Best Practices Are Killing Us</a>,” Nicole Sullivan addresses the horrors of maintaining inefficient style sheets. Sullivan offers some helpful ideas and observations, especially for dealing with the convoluted code of major longstanding clients. My approach is more cavalier; if the style sheet schema I’m dealing with is so convoluted that it could affect the website’s performance all by itself, then I’ll do one of three things:

*   Consider a different client,
*   Consider a different career,
*   Stop using Drupal.

Maintainability is a problem, but it’s a problem <em>for</em> coders <em>by</em> coders, and CSS classes, as Sullivan points out, aren’t even the main culprit. The <code>class</code> attribute is implicated in a much graver crime, and usability—not maintainability—is ultimately at stake. Rather than the overuse of classes, I question the efficacy of the <code>class</code> attribute <em>per se</em>.</p>

## The Class As Imposter

A few years back, a girlfriend of mine gave me the pet name Stinky. I appreciate that this might seem off topic; please bear with me. She assured me that the name was actually not due to any malodor, but rather had some cryptic link with a fond childhood memory. Nonetheless, it was not a moniker that I wished anyone else to know about. Well, until now—but it’s important for my argument.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63b23e21-a5f5-41c9-8f41-ff64ab5e5a95/label-78x66.png"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119340" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63b23e21-a5f5-41c9-8f41-ff64ab5e5a95/label-78x66.png" alt="Name label" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63b23e21-a5f5-41c9-8f41-ff64ab5e5a95/label-78x66.png">View image</a>.</em>

<a href="https://www.tizag.com/cssT/class.php">CSS classes</a> are a lot like pet names. They are coined in private, where they belong and usually remain, and on the rare occasion that they are aired in public, they’re frequently a source of <strong>great embarrassment</strong>. While I’m embarrassed to have disclosed my own pet name of Stinky (there it is again), I feel equally red-faced about the <code>.nudge-right</code> class that I once used to deal with an awkward <code>div</code>.

Not all classes are ugly hacks. Many <a href="https://github.com/stubbornella/oocss">frameworks</a> employ sensibly named classes, sometimes even in an “object-oriented” fashion. The question is, why have classes at all? We already have the names of elements (<code>&lt;p&gt;</code>, <code>&lt;small&gt;</code>, <code>&lt;address&gt;</code>, <code>&lt;ul&gt;</code>, etc.). Better still, like my legal name of Heydon Pickering, they actually have some currency: they can be interpreted by more than one or two people.</p>

## Parity And Disparity

The reason we “mark up” Web content is to create parity between the way it is perceived by human readers and the way it is <strong>read and archived by machines</strong>. This parity has many benefits, some of which are discussed in an <a href="https://html5doctor.com/lets-talk-about-semantics/">excellent post by Dr. Mike</a>. Perhaps the greatest benefit is that when someone searches for some content, the engine that carries out the search request has a better chance of identifying and finding it. The machine and the human have “an understanding.” Parity is extremely important because, without it, the mechanisms of data storage and retrieval would get out of sync.

Aside from <a href="https://microformats.org/">microformats</a> (which, like tag names, have been endowed with agreed meanings), no class is able to affect the actual <em>meaning</em> of the marked-up content as read by an indexing bot or screen reader. Classes can only affect the <strong>visual appearance</strong> of the content. That’s right: <em>all</em> classes are “decorator classes.” You knew that already, but is it a moot point? I think not.</p>

### An Example

Please consider the following code and corresponding illustration. Think of the tags as pseudo-HTML.

<pre><code class="language-markup tmp-html">// HTML:

&lt;sea&gt;
&lt;crustacean class="crab"&gt;Shane&lt;/crustacean&gt;
&lt;crustacean class="lobster"&gt;Martin&lt;/crustacean&gt;
&lt;/sea&gt;</code></pre>

<pre><code class="language-css">// CSS:

sea {
   background:blue;
}

crustacean {
   width:200px;
   height:200px;
   border:2px solid;
   text-align:center;
   color:white;
}

.crab {
   background-image:url(../images/crab.jpg);
}

.lobster {
   background-image:url(../images/lobster.jpg);
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a5296fe-d407-4468-8e21-9e05be16093d/crustacea.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119337" title="crustacea" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a5296fe-d407-4468-8e21-9e05be16093d/crustacea.jpg" alt="" /></a><br>
<em>(Images: <a href="https://www.flickr.com/photos/patrick/45087811/">Patrick Tanguay</a> and <a href="https://www.flickr.com/photos/ajmexico/3315595873/">ajmexico</a>)</em>

*   **What the human sees**.  An angry-looking crab and a yellow lobster next to each other in a watery blue box, bearing the unlikely names of Martin and Shane, respectively.
*   **What the bot sees**.  Two adjacent bits of text that both belong to `sea` and should be treated as `crustacean`-related.

Both the human and the bot are correct. However, they are both <strong>missing some information</strong>. The bot is not aware that the two crustaceans are, specifically, a crab and a lobster. The human, meanwhile, has not been told that the crab and the lobster both belong to the crustacea family. Despite a correct use of semantic HTML and a judicious application of CSS classes, there is a disparity between the way the machine and the human interpret the information.

We can’t expect <a href="https://dev.w3.org/html5/spec/single-page.html">the specification</a> to contain a tag for every conceivable concept. It will be no surprise that <code>&lt;slippery&gt;</code>, <code>&lt;disappointing&gt;</code> and <code>&lt;airborne&gt;</code> are not so far being considered for HTML5. Neither could we expect parsers to be able to meaningfully interpret each and every <strong>individually authored class name</strong>. In this case, what else can we do to supply both the human and the bot with as much of the same information as possible? That is, what tool can accurately explicate the intended “lobsterness” of the second element without alienating either party?

The answer is something called <strong>content</strong>. So far, our “content” consists of a spurious label (much like your typical <code>class</code> attribute). I think we can do a lot better:

<pre><code class="language-markup tmp-html">&lt;crustacean&gt;
   &lt;hgroup&gt;
      &lt;h1&gt;Shane&lt;/h1&gt;
      &lt;h2&gt;The Lobster&lt;/h2&gt;
   &lt;/hgroup&gt;
   &lt;p&gt;Shane is a &lt;a href="lobsters.html"&gt;lobster&lt;/a&gt;, which is a type of &lt;a href="crustacea.html"&gt;crustacean&lt;/a&gt;. He is &lt;em&gt;big&lt;/em&gt; and &lt;em&gt;yellow&lt;/em&gt;.&lt;/p&gt;
   &lt;img src="images/shane.jpg" alt="Shane sitting on the sea bed"&gt;
   &lt;p&gt;
      &lt;small&gt;Photo by ajmexico&lt;/small&gt;
   &lt;/p&gt;
&lt;/crustacean&gt;</code></pre>

The mistake we made in the first snippet was to make two items that are similar appear different. As a general rule, if two elements are of the same type and appear in the same context, then they are alike—in which case, they should <em>appear</em> alike. The job of styling is to make items presentable, not to define them. <strong>Only the content should be definitive</strong>, and only the tags should be used to define the content’s taxonomy.

By depriving ourselves of the <code>class</code> attribute, we are forced to rely on content to add meaning to our design. In our example, the background images invoked via the classes have been replaced by image tags—i.e. actual content tags that can be interpreted by both bots and screen readers (via the <code>alt</code> attribute). This makes the machine’s experience of the resulting design much closer to our own.</p>

### The Document Outline

In the example above, we showed that, even when used sensibly and sparsely, classes can undermine the parity that should be maintained between the essence and appearance of content. However, nothing is to stop us from <strong>going completely mad</strong>: we could create as many classes as we wanted, place them in whichever elements we wanted as many times as we wanted, and name them whatever we wanted.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e361b-83bd-404b-a514-2e7cdc0f93d4/divya.png"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119338" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e361b-83bd-404b-a514-2e7cdc0f93d4/divya.png" alt="The Divya Debacle" /></a><br>
<em>Homogeneous code like the sort referred to in this strip would not be practical if we couldn’t visually differentiate between the same elements via classes. (Strip by <a href="https://cssquirrel.com/">Kyle Weems</a>)</em>

This kind of freedom allows us to break with conventions that make HTML documents apprehensible and, therefore, useful. Heeding Mark Boulton’s advice about icon design would be better:
<blockquote>Leave “creativity” to the bad designers.</blockquote>

Classes enable us to represent differences that don’t really exist, but nothing is wrong with <em>reflecting</em> differences that <em>do</em> exist. In HTML5, the <a href="https://www.smashingmagazine.com/2012/06/classes-where-were-going-we-dont-need-classes/">document-outlining algorithm</a> more than ever seeks to enforce structure in an HTML document. By harnessing this structure, we can use CSS to reflect legitimate differences between the parts of our page. This requires a basic understanding of <strong>semiotics</strong> and will be the subject of the next section.

(While not necessary to understand the following section, I highly recommend Derek Johnson’s <a href="https://www.smashingmagazine.com/2011/08/16/html5-and-the-document-outlining-algorithm/">introduction to the document outline</a> as background reading.)

## Semiotic Style

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/440c9587-a281-4df3-af05-839c35faec0a/saussure.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119344" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/440c9587-a281-4df3-af05-839c35faec0a/saussure.jpg" alt="" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/440c9587-a281-4df3-af05-839c35faec0a/saussure.jpg">View image</a> of Ferdinand de Saussure.</em>

It would be difficult to overestimate the impact that <a href="https://en.wikipedia.org/wiki/Ferdinand_de_Saussure">Ferdinand de Saussure</a> had on the way we understand language—and, for that matter, anything we use to elicit meaning. To Saussure, how we choose to define things is not important. Rather, their <strong>relationship to one another</strong> is truly what makes them what they are. As Saussure’s translator <a href="https://en.wikipedia.org/wiki/Roy_Harris_%28linguist%29">Roy Harris</a> put it, Saussure’s contribution to linguistics was to cease viewing words as “mere vocal labels or communicational adjuncts superimposed upon an already given order of things.” If you’ve been following closely so far, you’ll appreciate why I’m a big fan of Saussure: he sees no value in extraneous classification.

Saussure’s understanding of language as a system is based on two basic relationships; the paradigmatic and the syntagmatic. The illustration below transposes these concepts to an example of some semantic HTML.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be1c6d0e-1d07-4c86-a789-164db5973e87/paradigm-syntagm.png"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119342" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be1c6d0e-1d07-4c86-a789-164db5973e87/paradigm-syntagm.png" alt="Semiotic HTML" /></a>

### Paradigm

A paradigm is a set of words—or, in our case, tags—with functional similarities but subtle or radical differences in meaning. In the sentence, “The crab sat next to the lobster,” the word “sat” belongs to a paradigm of alternative words that include “rested” and “crouched” as well as “stood.” It is a relationship of substitution.

There are certain rules. In English, a verb cannot be substituted with a noun, just as in HTML an <a href="https://en.wikipedia.org/wiki/HTML_element#Inline_elements">inline element</a> cannot always be substituted with a <a href="https://en.wikipedia.org/wiki/HTML_element#Block_elements">block-level</a> one. In the diagram above, omitted members of paradigms are shown in light gray.</p>

### Syntagm

A syntagm is essentially a structure composed of paradigmatic choices. In English, sentences, paragraphs, chapters and books are all syntagms. In HTML, a block of code made from your choice of elements could be considered a syntagm.

Each syntagm is its own <strong>semantic system</strong>, and smaller syntagms can belong to larger ones. Just as a paragraph can belong to a chapter, so can an <code>&lt;hgroup&gt;</code> belong to an <code>&lt;article&gt;</code> and an <code>&lt;article&gt;</code> belong to a <code>&lt;section&gt;</code>.</p>

### What Am I Getting At?

This is all pretty straightforward stuff, so what’s the point? The point is this: The Saussurian model of language recognizes that terabytes of poems, novels, essays and plays can all be written (and have all been written) without having to invent new words or redefine old ones. If this model is good enough for natural languages such as English, then it is more than good enough for a simple metalanguage such as HTML. Of course, new words <em>are</em> coined over time, just as new elements are slowly introduced to the HTML specification, but this is done with careful deliberation and consensus. Classes have no such mandate.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b259de78-e2d9-4f2d-b737-0b340ab9b125/roles.gif"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119343" style="width: 90%" title="roles" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/614f7628-6a05-4874-a78c-bded0c0a4a39/roles.gif" alt="" /></a><br>
<em>If you really need to add a styling hook, choose something that pertains to a function, such as the <code>role</code> attribute. Roles are standardized and machine-readable. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/440c9587-a281-4df3-af05-839c35faec0a/saussure.jpg">View image</a>.)</em>

Meanwhile, the Saussurian model gives us more than enough scope for elegance and invention, as well as prohibits us from making bad choices. By styling the elements that make up our documents according only to <strong>what and where</strong> they are, then misleading or confusing the user becomes extremely difficult—without conscious effort. All you are doing is using CSS to <strong>expose the inherent structure of your page</strong>.

Paradigmatic styling is really just about choosing the right element for the job. There are many ways to traverse “syntagms,” so let’s look at a few examples. You’ll already be familiar with most or all of these; just imagine using this kind of styling exclusively:

*   `aside h1` A simple descendant selector that styles top-level headings that belong to asides.
*   `body > div` Styles divs that directly descend from `<body>` exclusively (helpful for unsemantic layout such as “wrapper” blocks).
*   `p + p` Targets all paragraphs that directly follow other paragraphs.
*   `* + h2` Styles second-level headings that do not appear at the head of their parent section.
*   `section ~ article h2` Targets all second-level headings in articles that are together preceded by a section.
*   `li:nth-child(odd)` Targets every other (i.e. odd) list item in either `ol` or `ul` elements.
*   `ol li:first-child h3:before` Styles the pseudo-content that precedes the third-level heading in the first item of an ordered list.

You will realize that any content styled using these methods will change in appearance upon being moved to another part of the page. Never fear: <strong>that is supposed to happen</strong>. Unfortunately, the employment of classes can all too easily undo this legitimate influence of context.</p>

### An Example

To provide an example to accompany this article, I took the step of removing all class attributes from <a href="https://www.heydonworks.com">my own blog</a>. The style sheet isn’t as neat as I’d like it to be, but that’s my fault, not Saussure’s. Note that my design is responsive and relies on a single <code>id</code> attribute to enable smartphone users to jump to the main navigation; however, it is not used as a styling hook.</p>

## The Importance Of Context

Previously, we explored how classes can be used to illustrate differences that don’t exist. By the same token, they can be used to <strong>gloss over differences</strong> that <em>do</em> exist.

From a semiotic perspective, perhaps the only real difference between two things that are otherwise alike is their context: the circumstances in which they are found. An English native and a French native are genetically similar but culturally different. The context of their nationality makes them, in many noteworthy ways, unalike.

Please consider the following code example:

<pre><code class="language-markup tmp-html">// HTML:

&lt;article&gt;
   &lt;h1 class="main-title"&gt;Article Title&lt;/h1&gt;
   &lt;aside&gt;
      &lt;h1 class="main-title"&gt;Aside Title&lt;/h1&gt;
   &lt;/aside&gt;
&lt;/article&gt;</code></pre>

<pre><code class="language-css">// CSS:

.main-title {
   font-size:30px;
}</code></pre>

By coining the class <code>.main-title</code>, we have created a cypher to help us easily style all top-level headings similarly. However, the two headings in our example are <em>not</em> similar. Any parser that understands HTML5 will know that the <code>h1</code> in the aside is, in fact, less important than the one that belongs directly to the <code>article</code>. How does it know this? Well, the specification mandates that asides are for <a href="https://html5doctor.com/aside-revisited/">tangentially related</a> content, not important stuff like that found in the main body of the article. Also, the parser’s understanding of the document-outlining algorithm means that it will consider the <code>aside</code>’s heading as a mere subheading, belonging to the <code>h1</code> that precedes it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a3c0e2-a3a1-47ef-8cb2-e1cdefaec3ed/context1.gif"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119365" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a3c0e2-a3a1-47ef-8cb2-e1cdefaec3ed/context1.gif" alt="Context Definitions" /></a><br>
<em>Google is aware that the word “context” has more than one meaning… depending on the context.<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a3c0e2-a3a1-47ef-8cb2-e1cdefaec3ed/context1.gif">View image</a>.)</em>

If this is all being read and understood by the parser, then shouldn’t it also be disclosed to the user? In truth, the class in this example is redundant anyway: we could just style the <code>h1</code> element with the property of <code>font-size: 30px</code>. The point is that if we differentiate the two elements according to <em>context</em> (say, by using the descendent selector <code>aside h1</code>), then the CSS will be bound to the HTML’s structure and the appearance of the element will fall in line with its computed meaning. In practice, by moving from an aside into the main article, an <code>h1</code> would automatically look more important — which would <strong>reflect its greater importance</strong>. The <code>aside h1.main-title</code> selector would work, too, but the class is absolutely redundant.

Seems obvious, doesn’t it? However, popular frameworks such as <abbr title="Object Oriented Cascading Style Sheets"><a href="https://oocss.org/">OOCSS</a></abbr> specifically sanction the use of classes in a way that denies the influence of context. To quote OOCSS’ <a href="https://github.com/stubbornella/oocss/wiki">GitHub page</a>, “An object should look the same no matter where you put it.” In fact, we’re told to avoid the descendent selector altogether, thus largely negating the “cascading” part of the technology.

The innovators of OOCSS are not the only ones who discourage the use of the descendent selector either. An <a href="https://csswizardry.com/2012/03/hacker-news-rebuttal/">article on CSS Wizardry</a> reads, “As soon as an element begins to rely on its parent, and their parent, and their parent’s parent then you are doing it wrong. Your styles should never rely too heavily on where they live as this makes them incredibly unportable.”

In the next section, I’ll make the case that only content, not styles, should be portable.</p>

## Modularity And Mobility

An element that insists on looking the same wherever it appears is a bit like a Briton who travels from country to country refusing to speak the native language and burping the English national anthem. It’s <strong>aggressive and inappropriate</strong>.

I don’t see CSS as being object-oriented; I see it as being <strong>interface-oriented</strong>. The purpose of CSS is not to make individual items look the way we want them, but to make the interfaces that we build by styling HTML documents cogent and readable. For an interface to be optimally apprehensible, all of its components should work together politely and should respect the overall visual structure, no matter where the components come from.
<blockquote>Get your content ready to go anywhere because it’s going to go everywhere.

<footer>– <a href="https://bradfrostweb.com/blog/web/for-a-future-friendly-web/">Brad Frost</a></footer></blockquote>

With the advent of elements such as <a href="https://html5doctor.com/the-article-element/"><code>article</code></a>, which are intended to carry content to be dispersed <em>between</em> documents, we should consider an approach to styling that does not permit externally sourced content to spoil the coherence of the context into which it is introduced. Once again, classes get in the way.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cd09fd0-ddf5-4f2d-88fe-2c4f4fc1bf27/my-class.gif"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-119341" title="my-class" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cd09fd0-ddf5-4f2d-88fe-2c4f4fc1bf27/my-class.gif" alt="" width="716" height="268" /></a>

Unsemantic pieces of content that are styled with classes depend on the style sheets that give their particular content visual form. The class acts as a key, <strong>pairing the HTML with a specific CSS file</strong>. This has two undesirable outcomes:

*   The document that hosts the third party’s content has to load an additional resource (i.e. the third party’s style sheet);
*   The third party’s content defies the aesthetic conventions of the page and sticks out like an **obnoxious advert**.

By agreeing to basic semantic conventions and refusing to superimpose our own styling rules, we can instead manufacture content nodes that travel seamlessly from document to document. This approach to styling creates a scenario that allows our HTML to be <a href="https://en.wikipedia.org/wiki/Interoperability">interoperable</a>, like <abbr title="Really Simple Syndication">RSS</abbr>. Website owners will maintain CSS files that style elements according only to the elements’ ownership by and proximity to other elements. Content manufacturers, meanwhile, will produce content that (by virtue of its semantic conventionality) is ready to take on the styling of any context it may enter, integrating itself with a minimum of effort.

In short, we should aim to truly separate style and content, allowing content to travel between interfaces but with the interfaces remaining unmoved. As within any properly formatted document, attribution — not aesthetics — should be what discloses the source of a piece of content.</p>

## Conclusion

“Roads? Where we’re going, we don’t need roads!” exclaims the inventor, Doc Brown, as his <a href="https://en.wikipedia.org/wiki/DeLorean_Motor_Company">Delorean</a>-based time machine’s wheels fold under its chasis and the car takes off, headed for 2020. It’s a great line for its defiance: Roads, which have literally paved the way for automobile travel and made it viable, are no longer even needed. At all.

&lt;abbr="Extensible HTML"&gt;XHTML, which sought to enforce <a href="https://en.wikipedia.org/wiki/Well-formed_element">well-formed</a> code, did little to enforce or cater to well-formed content. CSS classes, like the roads in Doc Brown’s line, were a costly and substandard necessity. We wouldn’t have gotten very far as <abbr title="User Interface">UI</abbr> designers without them. However, classes were only ever a <a href="https://remysharp.com/2010/10/08/what-is-a-polyfill/">polyfill</a>. Now that the new technology has arrived, they have become obsolete.

<em>(al) (km)</em>

