---
title: 'Structural Semantics: The Importance Of HTML5 Sectioning Elements'
slug: the-importance-of-sections
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07b3cca6-f289-4473-adc6-47ce25f6bc96/the-importance-of-sections.png
date: 2013-01-18T13:29:32.000Z
author: heydon-pickering
description: >-
  Whatever you call them — blocks, boxes, areas, regions — we’ve been dividing
  our Web pages into visible sections for well over a decade. The problem is,
  we’ve never had the right tools to do so. While our interfaces look all the
  world like grids, the underlying structure has been cobbled together from
  numbered headings and unsemantic helper elements; an unbridled stream of
  content at odds with its own box-like appearance.
categories:
  - Coding
  - HTML5
  - Semantics
---
Whatever you call them — blocks, boxes, areas, regions — we’ve been dividing our Web pages into visible sections for well over a decade. The problem is, we’ve never had the right tools to do so. While our interfaces look all the world like grids, the underlying structure has been cobbled together from numbered headings and unsemantic helper elements; an unbridled stream of content at odds with its own box-like appearance.

Because we can make our <code>&lt;div&gt;</code>s look but not <em>behave</em> like sections, the experience for assistive technology (<abbr title="Assistive Technology">AT</abbr>) users and data-mining software is quite different from the experience enjoyed by those gifted with sight.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [Sexy New HTML5 Semantics](https://www.smashingmagazine.com/2011/11/html5-semantics/)
*   [Learning to Love HTML5](https://www.smashingmagazine.com/2010/11/learning-to-love-html5/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/html-5-cheat-sheet-pdf/)

Now that HTML5 has finally made <a href="https://www.w3.org/WAI/GL/wiki/Using_HTML5_section_elements">sectioning elements</a> available, many of us greet them with great reluctance. Why? Partly, because we’re a community which is deceptively resistant to change, but also because of some perceived discrepancies regarding advice in the specification. In truth, the advice is sound and the algorithm for sectioning is actually easier to use than previous implementations. Some developers are just very married to their old workflow, and they think you should be too. There's no good reason why.

{{% feature-panel %}}

Make no mistake: Sectioning elements help you improve document structure, and they're in the spec’ to stay. Once and for all, I will be exploring the problems these elements solve, the opportunities they offer and their important but misunderstood contribution to the semantic Web. If you’re unfamiliar with the concept of the “semantic Web,” <a href="https://youtube.com/watch?gl=GB&amp;hl=en-GB&amp;v=OGg8A2zfWKg">this video</a> is a great introduction.</p>

## Making Websites

My introduction to Web design was via a university course module called something like “2.1: Dreamweaver,” and I recall my first website well. I remember my deliberately garish choice of <a href="https://en.wikipedia.org/wiki/Web_colors#Web-safe_colors">Web-safe</a> colors. I remember it looking right only in <a href="https://en.wikipedia.org/wiki/Netscape_Navigator">Netscape Navigator</a>. Most of all, I remember hours of frustration from tugging at the perimeter of a visual layout tool named “table.” I had no idea at the time that this layout tool represented a type of annotation called an <abbr title="Hypertext Markup Language">HTML</abbr> tag. Furthermore, no one told me that this annotation invited my patchwork of <span style="color: red;font-weight: bold">primary</span> <span style="color: blue;font-weight: bold">colors</span> and compressed JPEGs to be computed as a sort of demented Excel spreadsheet. In other words, I had no idea I was <strong>doing it wrong</strong>.

<figure><img loading="lazy" decoding="async" class="123743" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70f6ea7e-9212-4b4f-99c3-2c592466de1e/table.gif" alt="A Dreamweaver table" width="432" height="217" /><br>
<figcaption>*Bites tongue*</figcaption><br>
<blockquote>The fundamental failure of most graphic, product, architectural, and even urban design is its insistence on serving the God of Looking-Good rather than the God of Being-Good.

<footer>– Richard Saul Wurman</footer></blockquote>

Macromedia’s Dreamweaver didn’t make the creation of valid documents impossible, but it was one of a number of emerging <abbr title="Graphical User Interface">GUI</abbr> editors that pandered to <strong>our desire for visual expression</strong> more than it encouraged informational clarity. Dreamweaver, and other editors classified under the misnomer “<abbr title="What You See Is What You Get">WYSIWYG</abbr>,” helped transform a standardized information system into a home for graphic design and enabled a legion of insufferable Nathan Barleys to flypost the World Wide Web with their vapid eye candy. I was one of many.
### Web Standards
By the time I made my first website, the Web standards movement, promoting compliance, uniformity and inclusion, was burgeoning. I just wasn’t aware of it until much later. I didn’t have to be: Agency-based Web design was still mainly graphic design with a reluctant programming department clumsily bolted on. If you’re doubtful of the grip that this culture has had on the World Wide Web, look no further than the fact it took until 2010 (<em>2010!</em>) for us to concede that <a href="https://www.alistapart.com/articles/responsive-web-design/">Web browsers are not really made of paper</a>.

When I finally became familiar with Web standards and the practice of “doing things right,” it was as someone who still worked primarily as a visual designer. Inevitably, my first forays into standards-based design revolved around mastering “CSS layout,” the practice of visually arranging content without relying on the semantically incorrect <code>&lt;table&gt;</code> element. We’ve held up <code>&lt;div&gt;</code>-based layout as a mark of quality for a number of years now. You might even say that it has become a time-honored rite of passage for graphic designers who are moving into “proper” HTML coding.

As I shall demonstrate, the <code>&lt;div&gt;</code> is the ultimate Graphic Design tool. By affecting only appearance, it licenses poor document structure and overengineered interfaces; all without making your document technically invalid. As such, it sanctions <strong>the worst kind of hacks</strong>.
## The Problem With &lt;div&gt;

Every day, thousands of Web developers invoke the almighty <code>&lt;div&gt;</code> to divide, partition and ring-fence their Web pages’ content. We use the <code>&lt;div&gt;</code> to police content, to prevent disparate chunks of information from collapsing into each other. In truth, the <code>&lt;div&gt;</code> has no such power.

Consider the following example:

<figure><img loading="lazy" decoding="async" class="alignnone size-medium wp-image-123733" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daf11c35-cc95-4e5e-ba17-0ca0b9581efd/drawing1-300x300.png" alt="Two column layout with sidebar encircled with dark border" width="300" height="300" /></figure>In this basic layout, I have included a body of text and an adjacent “sidebar.” To make it absolutely clear to the reader that the sidebar is tangential and does not belong to the main content, I’ve drawn a <strong>fat line</strong> around it using the <code>border</code> property. For those of you screaming, “That sidebar heading should be an &lt;h3&gt;!”, I’ll get to that shortly. All of my design decisions (the adjacent position, the border and the reduced font size) are facilitated by <abbr title="Cascading Stylesheets">CSS</abbr> alone. So, when I take the CSS away, I get this:

<figure><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-123734" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37c5a186-056f-4783-9698-d7bff4b77dff/drawing2-300x300.png" alt="The same layout as before is now one column, no borders" width="300" height="300" /></figure>Not only is switching off CSS the quickest way to make a Web page <a href="https://www.smashingmagazine.com/tag/responsive-web-design/">responsive</a>, but it’s a great way to see how HTML4 documents (which lack sectioning elements) are actually computed. In this case, our so-called “sidebar” is revealed to be just another raft of information in the <a href="https://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-utilizing-normal-document-flow/">linear flow</a> of the document.
### Why Is This So?
The reason for this is that the <code>&lt;div&gt;</code> is, and always has been, a <a href="https://www.w3.org/TR/2011/WD-html5-20110525/content-models.html#flow-content-0">flow content</a> element. No matter how thick the <code>&lt;div&gt;</code>’s borders or how dark its background color, it does not stand apart in the structure of the document. Neither, therefore, does its content. With the CSS removed, the faux sidebar’s heading of “Resources” now seems less a distinct component of the page and more a part of the main content. To a parser or screen reader, it would have seemed this way all along.

For reasons of clarity, let’s look at a further example using a snippet of HTML:

<pre><code class="language-markup tmp-html">&lt;div class="parent"&gt;
   &lt;h2&gt;Heading&lt;/h2&gt;
   &lt;p&gt;Some content...&lt;/p&gt;
      &lt;div class="child"&gt;
         &lt;h2&gt;Another heading&lt;/h2&gt;
         &lt;p&gt;Some other content...&lt;/p&gt;
      &lt;/div&gt;
   &lt;/div&gt;</code></pre>

I’ve done something slightly different here by entering the two <code>&lt;div&gt;</code>s into a parent-child relationship: The <code>div.child</code> tag <em>belongs</em> to <code>div.parent</code>. We can certainly make it look that way with CSS, anyway. However, <code>&lt;div&gt;</code>s, to quote the specification, “have no special meaning.” Not only do they not mean anything semantically, but they have no impact on the <strong>computable structure</strong> of the page (sometimes called the “<a href="https://html5doctor.com/outlines/">document outline</a>”). The <code>&lt;div&gt;</code>s we’ve used may as well be invisible; so, to get a meaningful map of the structure we’ve created, we should <strong>remove them completely</strong>. That leaves just four elements and reveals the parent-child relationship to be an illusion:

<pre><code class="language-markup tmp-html">&lt;h2&gt;Heading&lt;/h2&gt;
   &lt;p&gt;Some content...&lt;/p&gt;
   &lt;h2&gt;Another heading&lt;/h2&gt;
   &lt;p&gt;Some other content...&lt;/p&gt;</code></pre>

As HTML coders interested in sound structure, we should be interested that the above reduction — which omits all meaningless elements — is what we’ve <strong>actually made</strong>, and it’s not what we set out to do: By not really <em>belonging</em> to “parent,” “child” has a different contextual status in the document than intended.
### Heading Levels Don’t Really Help
It’s popular to believe that replacing the second <code>&lt;h2&gt;</code> with an <code>&lt;h3&gt;</code> would solve our problem. If we did so, we’d get the following, more dynamic outline:
<ul>
 	<li>A Heading (<code>h2</code>)
<ul>
 	<li>Another Heading (<code>h3</code>)</li>
</ul>
</li>
</ul>
This solution certainly seems more purposeful, but is it the right decision? Should the second heading be a subheading within the same topic (an <code>&lt;h3&gt;</code>) or be the introduction of an entirely new topic (an <code>&lt;h2&gt;</code>, as we had in the first place)? Headings alone can only show where a piece of content starts, not where it ends, which makes it difficult to tell <strong>what belongs to what</strong>. We have to simulate belonging by choosing the correct heading level for the context. Just think about that for a second: We're defining the content's structural status by labeling it retroactively. It's just <em>begging</em> to go wrong.

Lets have a look at the homepage of accessibility experts <cite>The Paciello Group</cite>. Naturally, it's a highly accessible and pretty well organized site, but <strong>could the structure be improved with HTML5 sections</strong>? You'll notice their use of a <code>&lt;div&gt;</code> to collectively wrap the three <code>&lt;h2&gt;</code>s, <em>Software Developers</em>, <em>Website Owners</em> and <em>Mike Paciello</em>. Since the <code>&lt;div&gt;</code> doesn't computably contain these three blocks, the last <code>&lt;h2&gt;</code> and the following <code>&lt;h3&gt;</code> are allowed to pair off in this relationship:
<ul>
 	<li>Mike Paciello (h2)
<ul>
 	<li>Contact Us Now (h3)</li>
</ul>
</li>
</ul>
Wait … so, “Contact Us Now” is a subtopic belonging to the larger theme of “Mike Paciello”. Can that be right? It certainly doesn't look this way in the visual layout. It’s worth noting at this point that the <code>&lt;div&gt;</code> which fails to thematically group those three <code>&lt;h2&gt;</code> blocks has a class of <code>class="region"</code>. Ironically, if this <code>&lt;div&gt;</code> had been a <code>&lt;section&gt;</code>, some screen readers would consider it a "region". If a <code>&lt;section&gt;</code> <em>had</em> been used in place of the <code>&lt;div&gt;</code>, the observed relationship would not have emerged: The "region" would be self-contained. The <em>class</em> of "region", however, is not taken into consideration in any meaningful way and does not affect the structure.

Okay, so that's a weird one, but the situation only gets more confusing when we start to include items for which <strong>headings aren’t really even appropriate</strong>. Take this further example:

<figure><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-123735" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82fd7f41-1508-4cad-8796-10d534594d60/drawing3-300x300.png" alt="This layout has an h1, an h2 for content and an h3 sidebar with a footer div at the bottom" width="300" height="300" /></figure>In my HTML4 page, I have an <code>&lt;h1&gt;</code> to introduce the document, an <code>&lt;h2&gt;</code> for the main content and an <code>&lt;h3&gt;</code> to mark the start of my “sidebar” (which is just a wishy-washy <code>&lt;div&gt;</code>, as in previous examples). The page follows long-standing convention by having an untitled <code>div#footer</code> resting at the foot of the document for copyright information and other such necessary evils. (It has to be a <code>&lt;div&gt;</code> in HTML4, because the <code>&lt;footer&gt;</code> tag doesn’t exist yet.) The question is, to which heading does the footer belong?
### Whose Footer Is This?
Most of us, based on appearances, would agree that the footer must belong to the document. That is what we’ve learned to expect. To the unsighted, it is a different story: Because there is no new introductory heading between the sidebar <code>&lt;h3&gt;</code> and the footer content, it could be extrapolated that these two components are as one (see image below left). By the same token, one could also argue that we’ve included the “sidebar” as a mere “break” from the flow of the main content, before returning to that flow at the advent of the footer (see image below right). This would make the <code>&lt;h2&gt;</code> the footer’s heading.

<figure><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-123807" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6f1977f-9bd2-46c3-bfb8-a19e7869f7dc/leftandright1.png" alt="Red outlines show different interpretations of structure" width="640" height="320" /></figure>The only decent chance we have of understanding the intended structure of the page is by inferring it from a reading of the content. Remembering that the whole point of a “markup language” is to make the structure of information easier to follow, I may as well have chucked the HTML and <strong>written my Web page on the back of a napkin</strong>.

Some accessibility gurus would suggest that you use a remedial <code>&lt;h2&gt;</code> to head the <code>#footer</code> and bring it back in line, marking up the end of the sidebar like so:
<ul>
 	<li><code>h1</code> (page)
<ul>
 	<li><code>h2</code> (main)
<ul>
 	<li><code>h3</code> (sidebar)</li>
</ul>
</li>
 	<li><code>h2</code> (footer)</li>
</ul>
</li>
</ul>
This kind of works as a hack, but it’s not really sound. Do you really want to make a big announcement of the footer — an announcement as big and bold as the one used to summon the main content, not to mention <em>bolder</em> than the sidebar? <strong>No</strong>. If our Web page were a film, the footer wouldn’t be the titles — it would be the credits. In HTML5, the <a href="https://dev.w3.org/html5/markup/footer.html"><code>&lt;footer&gt;</code> element</a> “contains information about its section.” This is semantically superior: We don’t use footers to introduce topics; we use them to conclude them. Accordingly, footers — unlike their parent sections in HTML5 — do not require headings.

<a href="https://www.smashingmagazine.com/2013/01/18/the-importance-of-sections/tweet/"><img loading="lazy" decoding="async" class="alignleft size-full wp-image-123744" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1803e200-a60a-4983-9c5b-ae1d377934a0/tweet.png" alt="Tweet reads: Marking up lots of headings in a page significantly dilutes a screen reader user's ability to navigate between parts of a page efficiently" width="444" height="181" /></a>

<figcaption>Just because the nesting level of headings is correct doesn’t necessarily make a page easy to read.</figcaption>The closest thing we have to a “system” for structuring documents properly in HTML4 is numbered headings. Not only does this lead to ambiguity, as explained, but in practice we don’t really even <em>use</em> headings to define structure. We use <code>&lt;div&gt;</code>s to define structure and throw in some apologetic headings for accessibility’s sake. To make matters <em>even</em> worse, <a href="https://www.w3.org/TR/WCAG-TECHS/H42.html">advice regarding the deployment of numbered headings</a> isn't even clear on whether we should use them in order (h1-h6) or not.

The loose coupling between headings and <code>&lt;div&gt;</code>s is inadequate. Now, with the introduction of sectioning elements, we still use boxes, of sorts, but boxes that actually <em>say something</em> on their own. We are making a move from merely implying sections (by labeling them) to <strong>letting them define themselves</strong>. Simultaneously, sighted readers and unsighted parsers can experience content that one has effortlessly divided into clear, manageable portions.
<blockquote>The HTML4 spec is very imprecise on what is a section and how its scope is defined. Automatic generation of outlines is important, especially for assistive technology, that are likely to adapt the way they present information to the users according to the structure of the document. HTML5 removes the need for &lt;div&gt; elements from the outlining algorithm by introducing a new element, &lt;section&gt;, the HTML Section Element.

<footer>– “<a href="https://developer.mozilla.org/en-US/docs/Sections_and_Outlines_of_an_HTML5_document">Sections and Outlines of an HTML5 Document</a>,” Mozilla Development Network</footer></blockquote>

## Sectioning

Aware of our desire for legitimate elements to create computable sections, HTML5 offers <code>&lt;section&gt;</code>, <code>&lt;article&gt;</code>, <code>&lt;aside&gt;</code> and <code>&lt;nav&gt;</code>. Like some sort of obnoxious holiday rep’, I’ll introduce the topic of practical sectioning using these elements with a quick quiz. Study the following diagram. How many sections do you count?

<a href="https://www.smashingmagazine.com/2013/01/18/the-importance-of-sections/sectioning1/"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-123738" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5941cc75-cb6d-43e5-9054-248b2a78aa99/sectioning1-300x300.png" alt="An HTML5 page with header, aside and footer" width="300" height="300" /></a>

</figure>

<strong>Multiple-choice answers:</strong>

1.  1
2.  2
3.  3
4.  4

The correct answer is (b), 2. We have included just one of HTML5’s new sectioning elements in the form of an <a><code>&lt;aside&gt;</code></a>. Because <code>&lt;footer&gt;</code>s and <code>&lt;header&gt;</code>s are not sectioning elements, what does that leave us with? The <code>&lt;body&gt;</code> tag is the outermost element, making the document itself a kind of section (a <em>super</em>section, to be precise). So, there you have it: We’ve been using “sectioning” since HTML 1.0, just not with any <strong>subsections</strong> to speak of.

Some of you may have missed the clue earlier in this article and thought that <code>&lt;header&gt;</code> and <code>&lt;footer&gt;</code> were sectioning elements. Don’t fret; it’s not your fault. Whenever developers like myself try to explain HTML5 page structure, they usually brandish a diagram like the one I used above. In these diagrams, the boxes marked “header,” “aside” and “footer” exist in the same visual paradigm and occupy a similar area. They seem alike, you might say. The other culprit for this endemic confusion is the way the specification is written. Believe it or not, the document structure of some pages in the specification that <em>refer</em> to document structure is <strong>structurally unclear</strong>! This sort of thing sometimes happens when a standard is constantly evolving. The navigation tree for “4.4 Sections” found in <a href="https://www.w3.org/TR/2011/WD-html5-20110525/sections.html">this draft</a> is laid out like so:

*   4.4 Sections
    *   4.4.1 `body`
    *   4.4.2 `nav`
    *   4.4.3 `article`
    *   4.4.4 `aside`
    *   4.4.5 `h1`, `h2`, `h3`, `h4`, `h5` and `h6`
    *   4.4.6 `hgroup`
    *   4.4.7 `header`
    *   4.4.8 `footer`
    *   4.4.9 `address`

You’d be forgiven for thinking that anything in this list qualifies as a sectioning element, absurd as some of them (<code>&lt;address&gt;</code>?) may sound. It’s only when you navigate to 4.4 Sections &gt; 4.4.8 Footer that you’re told that “the footer element is not sectioning content; it doesn’t introduce a new section.” Thanks!

Despite these ambiguities in the spec’ itself, as well as in the surrounding publicity for HTML5, sectioning in practice <em>just works</em>. The following three axioms are probably all you’ll need to understand the algorithm:

1.  `<body>` is the first section;
2.  `<article>`, `<section>`, `<nav>` and `<aside>` make subsections;
3.  Subsections may contain more sections (subsections)

Aside from a few trifling details, that’s it. In a little while I'll cover the <em>completely unnecessary worry</em> that is had over headings combined with sections. For now, let’s take another look at that example from before about footer ownership. This time, I’ll make a few HTML5 substitutions:

<a href="https://www.smashingmagazine.com/2013/01/18/the-importance-of-sections/sectioning2/"><img loading="lazy" decoding="async" class="alignleft size-full wp-image-123739" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77f2938e-3d7e-4117-b214-9e67daea56ff/sectioning2-300x300.png" alt="The diagram clearly shows the footer in the context of the document" width="300" height="300" /></a>
Note the lack of illustrated headings. Wherever a section is opened, it assumes responsibility for nesting: The heading type is unimportant. More on this soon …

The outline for this example looks like this:

*   Document
    *   Article
        *   Aside

Now that we’ve implemented sections, the boundaries are clear. Our document contains an article, which, in turn, contains an aside. There are three sections, each belonging to the last, and the depth of each section is reflected in the outline. Importantly, because sectioning elements <em>wrap</em> their contents, we know perfectly well where they <em>end</em>, as well as where they begin. And yes — screen readers like JAWS actually <strong>announce the end of sections</strong> like these! We know <strong>what content belongs to what</strong>, which makes deducing the purpose of the footer much easier. Because it exists outside the bounds of both the <code>&lt;article&gt;</code> and its <code>&lt;aside&gt;</code>, it <em>must</em> be the document’s footer. Here’s the same diagram again, with subsections faded out:

<a href="https://www.smashingmagazine.com/2013/01/18/the-importance-of-sections/sectioning3/"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-123740" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f4a813a-e500-4e34-8522-b15b507d8a09/sectioning3-300x300.png" alt="The same diagram with subsections faded out" width="300" height="300" /></a>

The power of sectioning lies in its ability to prescribe clearly defined boundaries, resulting in a more modular document hierarchy. The footer unequivocally belongs within the <strong>immediate scope</strong> of the highest-level section, giving assistive technologies and indexing parsers a good idea of its scope, which helps to make sense of the page’s overall structure.</p>

## Headings And Accessibility

When Sir Tim Berners-Lee conceived the <code>&lt;section&gt;</code> element <a href="https://1997.webhistory.org/www.lists/www-talk.1991/0003.html">all the way back in 1991</a>, he envisioned the obsolescence of ranked heading levels. The thrust of the idea was that headings should act as mere labels for blocks of content, and the nature (i.e. the importance, scope, etc.) of the content would be calculated automatically based on the content’s standing in the document.
<blockquote>I would in fact prefer, instead of &lt;h1&gt;, &lt;h2&gt; etc for headings [those come from the AAP DTD] to have a nestable &lt;section&gt;..&lt;/section&gt; element, and a generic &lt;h&gt;..&lt;/h&gt; which at any level within the sections would produce the required level of heading.

<footer>– <a href="https://1997.webhistory.org/www.lists/www-talk.1991/0003.html">Tim Berners-Lee</a></footer></blockquote>

Why is this preferable? Determining heading level systemically, based on nesting level, is much more dependable because it <strong>removes a layer of decision-making</strong>: By “producing” the required heading level automatically, we no longer have to decide separately which numbered heading we should include. It effectively prevents us from choosing the wrong heading level, which would be bad for parsable structure. A subsection <em>must</em> be subject to its parent section. Because this relationship between sections determines “level,” numbered headings are made redundant — hence, the proposed <code>&lt;h&gt;</code>.</p>

### A lot of fuss over nothing

Now, this is the supposedly tricky part; the part that causes all the <strong>consternation and gnashing of teeth</strong>. This is the part that caused Luke Stevens to write <a href="https://www.netmagazine.com/features/truth-about-structuring-html5-page">this diatribe</a>, and prompted Roger Johansson into a state of uncharacteristic apoplexy, asking, “<a href="https://www.456bereastreet.com/archive/201103/html5_sectioning_elements_headings_and_document_outlines/">are you confused too?</a>”. Ready?

In the WHATWG specification (in the same place where <code>&lt;footer&gt;</code>s were ostensibly classified as sectioning elements!), we are “strongly encouraged to either use only h1 elements, or to <strong>use elements of the appropriate rank for the section's nesting level</strong>.” On first appearance, this seems contrary. Surely only one of these courses of action can possibly be right? What do you do? I'm thinking maybe the first option. Or the second. Who am I?

It certainly confused me, so I spoke with HTML Editor, Ian Hickson. He explained the outline to me in detail and I'm convinced it is perfectly robust. I'm going to do my best to explain it to you here.

Okay. As it turns out, we didn’t get the generic <code>&lt;h&gt;</code> element. This wouldn't be backwards compatible because older browsers wouldn't recognise it. However, headings that introduce sections are — regardless of their numbered level — <em>treated</em> as a generic <code>&lt;h&gt;</code>. Quite correctly, it is the <strong>section itself</strong> that takes responsibility for nesting in these situations — not the heading — and whenever you introduce a new section, you introduce a new nesting level <em>without fail</em>. What does this mean in practice? It means that we can introduce and benefit from the structural clarification offered by sections <em>without</em> abandoning heading levels. Take the following example:

<pre><code class="language-markup tmp-html">&lt;h4&gt;Page heading&lt;/h4&gt;
&lt;p&gt;Introductory paragraph...&lt;/p&gt;
&lt;section&gt;
    &lt;h3&gt;Section heading&lt;/h3&gt;
    &lt;p&gt;some content...&lt;/p&gt;
    &lt;h2&gt;Subheading&lt;/h2&gt;
    &lt;p&gt;content following subheading...&lt;/p&gt;
    &lt;section&gt;
        &lt;h1&gt;Sub-subheading&lt;/h1&gt;
        &lt;p&gt;content two levels deep...&lt;/p&gt;
    &lt;/section&gt;
&lt;/section&gt;
&lt;h5&gt;Another heading&lt;/h5&gt;
&lt;p&gt;Continued content...&lt;/p&gt;</code></pre>

Our heading levels are all over the place. This is not recommended by the specification, but it helps demonstrate just how robust the HTML5 outlining algorithm really is. If we replace all the headings that open sections with a generic ("wildcard", if you prefer) <code>&lt;h&gt;</code>, things become clearer:

<pre><code class="language-markup tmp-html">&lt;h&gt;Page heading&lt;/h&gt;
&lt;p&gt;Introductory paragraph...&lt;/p&gt;
&lt;section&gt;
    &lt;h&gt;Section heading&lt;/h&gt;
    &lt;p&gt;some content...&lt;/p&gt;
    &lt;h2&gt;Subheading&lt;/h2&gt;
    &lt;p&gt;content following subheading...&lt;/p&gt;
    &lt;section&gt;
        &lt;h&gt;Sub-subheading&lt;/h&gt;
        &lt;p&gt;content two levels deep...&lt;/p&gt;
    &lt;/section&gt;
&lt;/section&gt;
&lt;h5&gt;Another heading&lt;/h5&gt;
&lt;p&gt;Continued content...&lt;/p&gt;</code></pre>

It’s important to note that the only errors revealed in the computed outline are ones relating to <strong>badly ordered numbered headings within the same section</strong>. In the original example, you’ll see that I've followed an <code>&lt;h3&gt;</code> with an <code>&lt;h2&gt;</code>. Because they are in the wrong order, the outline interprets them as being on the same level. Had I encapsulated the <code>&lt;h2&gt;</code> in <code>&lt;section&gt;</code>, this error would have been suppressed.

Well, how about that? If you're not convinced, go ahead and paste my example into the <a href="https://gsnedders.html5.org/outliner/">test outliner</a> and play around. It works just fine. In fact, it’s really difficult to break.

If you think there is a benefit to screen reader users, you may wish to adhere to the second of the two clauses from the specification and incorporate numbered headings that reflect nesting level. As demonstrated, this will have no effect on the outline, but since heading level (“Heading Level 2 - The Importance Of Sections”) is announced, it gives a clearer impression of structure to those who can't see boxes inside boxes.

The assertation that heading levels are perpetually indispensable to screen reader users comes under pressure when you consider advancements being made by screen reader vendors. Screen readers like JAWS mark the territory of sections more clearly than headings, by announcing the beginnings and ends of sections and the thematic regions they represent (“Article End!”). From this perspective, using more than one <code>&lt;h1&gt;</code>s in your document might sometimes be applicable. You'll come up against some accessibility experts who are keen on their “there can only be one [h1]!” mantra, but <a href="https://webaim.org/projects/screenreadersurvey3/#headings">research shows</a> that even in HTML4 or XHTML, this is not necessarily the case.

The approach you choose is yours to make; just employ some common sense and consistency. Bear in mind, though, that not all screen readers are able to announce the bounds of sectioned content. In these cases, there are measures you can take …

### ARIA Enhancement

Transition to an HTML5 document structure is made smoother by incorporating some <abbr title="Accessible Rich Internet Applications">ARIA</abbr> <a href="https://www.paciellogroup.com/blog/2010/10/using-wai-aria-landmark-roles/">landmark roles</a>, which are both relatively <a href="https://www.paciellogroup.com/blog/2011/07/html5-accessibility-chops-aria-landmark-support/">well supported</a> and somewhat analogous to the section-based navigation we should expect later. ARIA offers many more accessibility-specific features than baseline HTML5 could ever withstand; so, including “bolt-on” ARIA enhancements is <a href="https://www.456bereastreet.com/archive/201004/built-in_or_bolt-on_accessibility_in_html5_how_about_a_bit_of_both/">certainly polite</a>. However, regarding ARIA roles as a substitute for semantic HTML would be a grave misconception.

Landmark roles, such as <code>role="contentinfo"</code> and <code>role="banner"</code>, address accessibility only — not data mining — and each may be used only once per document. They are essentially shortcuts to parts of the page. HTML elements are more like building blocks, which are used in a repeated and modular fashion. So, while you can assist accessibility by placing <code>role=”banner”</code> into the <code>&lt;header&gt;</code> element closest to the document’s root, this does not preclude you from using <code>&lt;header&gt;</code> to introduce other sections:

<figure><img loading="lazy" decoding="async" class="alignleft size-full wp-image-123732" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aba2c726-0e14-4e72-ba80-4b4bac2a8ab9/banner-300x300.png" alt="The banner landmark role is used just once" width="300" height="300" /></figure>

### Are Sections The New `<div>`s?

This is a common misconception.

If it wasn’t clear already, it should be clear to you now that <code>&lt;div&gt;</code>s are semantically inert elements — elements that don’t really do or say anything. If this is clear, then it should also be clear that, when building a structured document, relying heavily on “<a href="https://www.w3.org/wiki/HTML/Elements/div">an element of last resort</a>” makes for a very poor foundation.

If the new <code>&lt;section&gt;</code> element, for example, was just <code>&lt;div&gt;</code> with a new name, adopting it would be a straightforward matter of search and replace. It wouldn’t exactly be progress, though. The truth is, <code>&lt;div&gt;</code> still has a rightful place in the spec’; we’ve just given its organizational responsibilities to a team of elements that are better qualified. Sorry, <code>&lt;div&gt;</code>, old mate. What <em>do</em> we use <code>&lt;div&gt;</code>s for, then? Precisely what they were good at from the beginning: as a tool for “<a href="https://en.wikipedia.org/wiki/Span_and_div">stylistic applications… when extant meaningful elements have exhausted their purpose</a>.”

For instance, you shouldn’t employ sections as <a href="https://www.w3.org/TR/CSS2/box.html">box-model</a> controlling measures like this…

<pre><code class="language-markup tmp-html">&lt;section class="outer"&gt;
      &lt;section class="inner"&gt;
         &lt;h1&gt;Section title&lt;/h1&gt;
      &lt;/section&gt;
   &lt;/section&gt;</code></pre>

… because there’s nothing that the outer section does that the inner section doesn’t. We've created two sections for one piece of content. A quick run through <a href="https://gsnedders.html5.org/outliner/">our outliner</a> throws the “Untitled Section” warning:

*   _[Untitled Section]_
    *   Section title

The brilliance of <code>&lt;div&gt;</code> in this context is that it refuses to affect the outline, which is why we can use it without fear of reprisal. This…

<pre><code class="language-markup tmp-html">&lt;section&gt;
      &lt;div&gt;
         &lt;h1&amp;gtSection title&lt;/h1&gt;
      &lt;/div&gt;
   &lt;/section&gt;</code></pre>

… averts <a href="https://twitter.com/jvhellemond/status/257850976478842880">disaster</a> and results in this unsullied, if simplistic, outline:

*   Section title

### Sections And Semantics

A lot of developers have trouble with the word “semantic.” You might even say that they don’t know what the word means, which (if you <em>are</em> familiar with the term) makes an interesting paradox. For instance, when <a href="https://www.zeldman.com/2012/11/21/in-defense-of-descendant-selectors-and-id-elements/">Jeffrey Zeldman advocates</a> for the “semantic” application of the <code>id</code> attribute, he’s kind of missing the point. The main purpose of semantic HTML is for the automated extraction of meaning from content. Applying a private, non-standard <code>id</code> to a <code>&lt;div&gt;</code> would not improve the semantics of the element one iota: Visitors can’t see it and parsers will ignore it. So much for the <a href="https://en.wikipedia.org/wiki/Semantic_Web">semantic Web</a>!

Sections are often characterized as the “semantic” equivalent of <code>&lt;div&gt;</code>. This is a half-truth at best, and I apologize for throwing the term “semantic” around so much — it’s become a bit of a shorthand. Some HTML elements <em>are</em> inherently semantic in that they prescribe specific meaning to their contents. The <code>&lt;address&gt;</code> element is a good example: When a parser reaches <code>&lt;address&gt;</code>, it knows that the contents should probably be interpreted as contact information. What it chooses to do with this knowledge is another matter, but it’s plausible that a screen reader could provide a shortcut to the address or a search engine could use it to refine its results pages.

<figure><img loading="lazy" decoding="async" class="alignleft size-full wp-image-123742" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d71834a2-2566-4bef-9212-471fcf7c488a/syntax.png" alt="Definition of syntax from Google search: The arrangement of words and phrases to create well-formed sentences in a language" width="444" height="83" /></figure>

Sectioning elements are not so much semantic as syntactic. All <code>&lt;section&gt;</code> tells us is that it is a part of a whole. However, the <em>syntactic</em> contribution of sectioning elements to document structure is not unimportant. Consider the following sentence: <strong>If sections you don’t websites your are use obsolete</strong>. A lot of recognizable words are in there, but the lack of sensible syntax makes the sentence difficult to unpick. So it is with sectioning: You are not creating meaning so much as assembling it. Meaning isn't always about the "thing"; it's sometimes about what that thing's role is amongst other things.</p>

### Microdata

Efficient, syntactically sound data structures are worthless if they are semantically lacking. Fortunately, HTML5 has both angles covered and provides a mechanism for attaching semantic <a href="https://en.wikipedia.org/wiki/Metadata">meta data</a>, called “<a href="https://googlewebmastercentral.blogspot.co.uk/2012/07/introducing-structured-data-dashboard.html">microdata</a>,” to our structured content. Using microdata, and by consulting <a href="https://schema.org/docs/full.html">schema.org</a>, you can define a page’s content as anything from a <strong>scholarly article</strong> to an <strong>exercise regimen</strong>. Unlike classes and IDs, this is information that can actually be interpreted usefully.

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="123893" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9796bc97-3ac5-4d96-b34b-2f3124d3fd8e/typical.png" alt="Google's structured data dashboard" width="599" height="166" /><br>
<figcaption>This microdata was found by Google and displayed in its “Structured Data Dashboard” for the WordPress theme <a href="https://typical-theme.heydonworks.com">Typical</a>.</figcaption></figure>

## Conclusion

HTML isn’t just an <abbr title="Software Development Kit">SDK</abbr> or a Graphic Designer's palette. It is a metalanguage, a language that tells you special information <em>about</em> information. Sometimes we — or, more precisely, the parsers we employ — benefit from added information about the subject, timing, origin or popularity of content. This is what APIs such as microdata and RDFa are for. Other times, the context, hierarchy, relative importance and codependence of the information are what need to be determined. This is where appropriate syntax, facilitated by sectioning elements, can be employed.

Some people will tell you not to bother with sectioning. They say that it’s hard work or that it doesn’t make sense. This is hokum. Sure, if you're lazy, <em>don't</em> bother with sectioning, but don't pretend you're doing it on principle. <strong>Using sections demonstrably enhances HTML structure without breaking accessibility</strong>. We've covered this.

Still, there will always be people who will attack this aspect of the specification. Perhaps we'll enjoy some of these objections in the comments:

1.  They will point to bad implementations by specific vendors: _These are bugs and bugs get fixed!_
2.  They will cite the actions of large websites who don't use sectioning elements: _Just because large sites haven't implemented sections doesn't mean they wouldn't like to. Since when does big mean 'right' anyway?_
3.  They will flood you with examples of developers implementing sections badly: _Some developers do stupid things and their misuse of HTML doesn't stop at sections. I include myself here, by the way._
4.  They will present you with anecdotal evidence about user behavior within specific groups: _It is expensive and impractical to address problems on a case-by-case basis. Fragmentation and complexity would also be inevitable: a loss for the majority of users._

I don’t think anyone would advocate making badly structured Web documents any more than they’d suggest building a house by stuffing a bag full of bricks and throwing it into a ravine. The case has been made and the specification bears it out: Sections aren’t just good for document structure — they finally make proper structure attainable. Some browsers and screen readers have some catching up to do, that’s for sure, but the situation is improving rapidly. Any kind of change is a little turbulent, but this kind is worth it.

