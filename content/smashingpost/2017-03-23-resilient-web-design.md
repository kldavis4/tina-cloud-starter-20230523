---
title: The Road To Resilient Web Design
slug: resilient-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0efddac-20a3-44dd-a92a-a609c0f93066/jan-tchichold-medieval-manuscript-framework-500w-opt.png
date: 2017-03-23T19:41:57.000Z
author: jeremy-keith
description: >-
  In the world of web design, we tend to become preoccupied
  with the here and now. In "_Resilient Web Design_", Jeremy Keith emphasizes
  the importance of learning from the past in order to better prepare ourselves
  for the future. So, perhaps we should stop and think more beyond our present
  moment? The following is an excerpt from Jeremy's web book.
categories:
  - Responsive Design
  - Layouts
---
Design adds clarity. Using colour, typography, hierarchy, contrast, and all the other tools at their disposal, designers can take an unordered jumble of information and turn it into something that’s easy to use and pleasurable to behold. Like life itself, design can win a small victory against the entropy of the universe, creating pockets of order from the raw materials of chaos.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2016/11/building-shaders-with-babylon-js/#further-reading-on-smashingmag)

*   [CSS Inheritance, The Cascade And Global Scope: Your New Old Worst Best Friends](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)
*   [Improving Your UI Design Skills With Copywork](https://www.smashingmagazine.com/2017/02/improving-ui-design-skills-copywork/)
*   [Pursuing Semantic Value](https://www.smashingmagazine.com/2011/11/pursuing-semantic-value/)

The Book of Kells is a beautifully illustrated manuscript created over 1200 years ago. It’s tempting to call it a work of art, but it is a work of design. The purpose of the book is to communicate a message; the gospels of the Christian religion. Through the use of illustration and calligraphy, that message is conveyed in an inviting context, making it pleasing to behold.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8bb021-187c-4202-9284-966a273e8fe5/book-of-kells-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31d86101-6c41-4f56-b86e-0db2eff28b9f/book-of-kells-preview-opt.jpg" alt="A page from an illuminated manuscript." width="“780&quot;" height="1040" /></a><figcaption>The incipit to the Gospel of Matthew in the Book of Kells. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8bb021-187c-4202-9284-966a273e8fe5/book-of-kells-large-opt.jpg">Large preview</a>)</figcaption></figure>

Design works within constraints. The Columban monks who crafted the Book of Kells worked with four inks on vellum, a material made of calfskin. The materials were simple but clearly defined. The cenobitic designers knew the hues of the inks, the weight of the vellum, and crucially, they knew the dimensions of each page.</p>

## Prints And The Revolution

Materials and processes have changed and evolved over the past millennium or so. Gutenberg’s invention of movable type was a revolution in production. Whereas it would have taken just as long to create a second copy of the Book of Kells as it took to create the first, multiple copies of the Gutenberg bible could be produced with much less labour. Even so, many of the design patterns such as drop caps and columns were carried over from illuminated manuscripts. The fundamental design process remained the same: knowing the width and height of the page, designers created a pleasing arrangement of elements.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b9605c4-0d51-4dcf-bb78-136813c94525/gutenberg-bible-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b9605c4-0d51-4dcf-bb78-136813c94525/gutenberg-bible-preview-opt.jpg" alt="Old style text in two columns." width="“600&quot;" height="" /></a><figcaption>A page from Gutenberg’s Bible.</figcaption></figure>

The techniques of the print designer reached their zenith in the 20th century with the rise of the Swiss Style. Its structured layout and clear typography is exemplified in the work of designers like Josef Müller‐Brockmann and Jan Tschichold. They formulated grid systems and typographic scales based on the preceding centuries of design.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61be02b6-fdac-455c-a77c-c379aba22c40/jan-tchichold-medieval-manuscript-framework-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66ea1074-1b6e-45f1-bc32-8fdd47411ab9/jan-tchichold-medieval-manuscript-framework-preview-opt.png" alt="A diagram demonstrating proportions." width="“780&quot;" height="592" /></a><figcaption>A framework for medieval manuscripts by Jan Tschichold. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61be02b6-fdac-455c-a77c-c379aba22c40/jan-tchichold-medieval-manuscript-framework-large-opt.png">Large preview</a>)</figcaption></figure>

Knowing the ratio of the dimensions of a page, designers could position elements with maximum effect. The page is a constraint and the grid system is a way of imposing order on it.</p>

## Taking Your Talent To The Web

When the web began to conquer the world in the 1990s, designers started migrating from paper to pixels. David Siegel’s <em>Creating Killer Websites</em> came along at just the right time. Its clever <code>TABLE</code> and <abbr>GIF</abbr> hacks allowed designers to replicate the same kind of layouts that they had previously created for the printed page.

Those <code>TABLE</code> layouts later became <abbr>CSS</abbr> layouts, but the fundamental thinking remained the same: the browser window — like the page before it — was treated as a known constraint upon which designers imposed order.

There’s a problem with this approach. Whereas a piece of paper or vellum has a fixed ratio, a browser window could be any size. There’s no way for a web designer to know in advance what size any particular person’s browser window will be.

Designers had grown accustomed to knowing the dimensions of the rectangles they were designing within. The web removed that constraint.

## If It Ain’t Fixed, Don’t Break It

There’s nothing quite as frightening as the unknown. These words of former <abbr>US</abbr> Secretary of Defense Donald Rumsfeld should be truly terrifying (although the general consensus at the time was that they sounded like nonsense):
<blockquote>There are known knowns. There are things we know we know. We also know there are known unknowns, that is to say we know there are some things we do not know. But there are also unknown unknowns — the ones we don’t know we don’t know.</blockquote>

The ratio of the browser window is just one example of a known unknown on the web. The simplest way to deal with this situation is to use flexible units for layout: percentages rather than pixels. Instead, designers chose to pretend that the browser dimensions were a known known. They created fixed‐width layouts for one specific window size.

In the early days of the web, most monitors were 640 pixels wide. Web designers created layouts that were 640 pixels wide. As more and more people began using monitors that were 800 pixels wide, more and more designers began creating 800 pixel wide layouts. A few years later, that became 1024 pixels. At some point web designers settled on the magic number of 960 pixels as the ideal width.

It was as though the web design community were participating in a shared consensual hallucination. Rather than acknowledge the flexible nature of the browser window, they chose to settle on one set width as the ideal …even if that meant changing the ideal every few years.

Not everyone went along with this web‐wide memo.</p>

## Dao Or Dao Not

In the year 2000 the online magazine A List Apart published an article entitled <em>A Dao of Web Design</em>. It has stood the test of time remarkably well.

In the article, John Allsopp points out that new mediums often start out by taking on the tropes of a previous medium. Scott McCloud makes the same point in his book <em>Understanding Comics</em>:
<blockquote>Each new medium begins its life by imitating its predecessors. Many early movies were like filmed stage plays; much early television was like radio with pictures or reduced movies.</blockquote>

With that in mind, it’s hardly surprising that web design began with attempts to recreate the kinds of layouts that designers were familiar with from the print world. As John put it:
<blockquote>“Killer Web Sites” are usually those which tame the wildness of the web, constraining pages as if they were made of paper — Desktop Publishing for the Web.</blockquote>

Web design can benefit from the centuries of learning that have informed print design. Massimo Vignelli, whose work epitomises the Swiss Style, begins his famous Canon with a list of The Intangibles including discipline, appropriateness, timelessness, responsibility, and more. Everything in that list can be applied to designing for the web. Vignelli’s Canon also includes a list of The Tangibles. That list begins with paper sizes.

The web is not print. The known constraints of paper — its width and height — simply don’t exist. The web isn’t bound by pre‐set dimensions. John Allsopp’s <em>A Dao Of Web Design</em> called on practitioners to acknowledge this:
<blockquote>The control which designers know in the print medium, and often desire in the web medium, is simply a function of the limitation of the printed page. We should embrace the fact that the web doesn’t have the same constraints, and design for this flexibility.</blockquote>

This call to arms went unheeded. Designers remained in their Matrix-like consensual hallucination where everyone’s browser was the same width. That’s understandable. There’s a great comfort to be had in believing a reassuring fiction, especially when it confers the illusion of control.

There is another reason why web designers clung to the comfort of their fixed‐width layouts. The tools of the trade encouraged a paper‐like approach to designing for the web.

## Ship Of Tools

It’s a poor craftsperson who always blames their tools. And yet every craftsperson is influenced by their choice of tools. As Marshall McLuhan’s colleague John Culkin put it, “we shape our tools and thereafter our tools shape us.”

When the discipline of web design was emerging, there was no software created specifically for visualising layouts on the web. Instead designers co‐opted existing tools.

Adobe Photoshop was originally intended for image manipulation; touching up photos, applying filters, compositing layers, and so on. By the mid nineties it had become an indispensable tool for graphic designers. When those same designers began designing for the web, they continued using the software they were already familiar with.

If you’ve ever used Photoshop then you’ll know what happens when you select “New” from the “File” menu: you will be asked to enter fixed dimensions for the canvas you are about to work within. Before adding a single pixel, a fundamental design decision has been made that reinforces the consensual hallucination of an inflexible web.

Photoshop alone can’t take the blame for fixed‐width thinking. After all, it was never intended for designing web pages. Eventually, software was released with the specific goal of creating web pages. Macromedia’s Dreamweaver was an early example of a web design tool. Unfortunately it operated according to the idea of <abbr>WYSIWYG</abbr>: What You See Is What You Get.

While it’s true that when designing with Dreamweaver, what <em>you</em> see is what <em>you</em> get, on the web there is no guarantee that what you see is what everyone else will get. Once again, web designers were encouraged to embrace the illusion of control rather than face the inherent uncertainty of their medium.

It’s possible to overcome the built‐in biases of tools like Photoshop and Dreamweaver, but it isn’t easy. We might like to think that we are in control of our tools, that we bend them to our will, but the truth is that all software is opinionated software. As futurist Jamais Cascio put it, “software, like all technologies, is inherently political”:
<blockquote>Code inevitably reflects the choices, biases and desires of its creators.</blockquote>

Small wonder then that designers working with the grain of their tools produced websites that mirrored the assumptions baked into those tools — assumptions around the ability to control and tame the known unknowns of the World Wide Web.</p>

## Reality Bites

By the middle of the first decade of the twenty‐first century, the field of web design was propped up by multiple assumptions:

*   that everyone was browsing with a screen large enough to view a 960 pixel wide layout;
*   that everyone had broadband internet access, mitigating the need to optimise the number and file size of images on web pages;
*   that everyone was using a modern web browser with the latest plug‐ins installed.

A minority of web designers were still pleading for fluid layouts. I counted myself amongst their number. We were tolerated in much the same manner as a prophet of doom on the street corner wearing a sandwich board reading “The End Is Nigh” — an inconvenient but harmless distraction.

There were even designers suggesting that Photoshop might not be the best tool for the web, and that we could consider designing directly in the browser using <abbr>CSS</abbr> and <abbr>HTML</abbr>. That approach was criticised as being too constraining. As we’ve seen, Photoshop has its own constraints but those had been internalised by designers so comfortable in using the tool that they no longer recognised its shortcomings.

This debate around the merits of designing Photoshop comps and designing in the browser would have remained largely academic if it weren’t for an event that would shake up the world of web design forever.</p>

## Stuck Inside Of Mobile

<blockquote>An iPod. A phone. And an internet communicator. An iPod. A phone …are you getting it? These are not three separate devices. This is one device. And we are calling it: iPhone.</blockquote>

With those words in 2007, Steve Jobs unveiled a mobile device that could be used to browse the World Wide Web.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2b45f61-8a07-45ba-a349-859ed84c7415/iphone-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79cb7574-4f23-42f3-9af6-df36813c8e0a/iphone-preview-opt.jpg" alt="A web page on the screen of a mobile phone." width="“780&quot;" height="1040" /></a><figcaption>The iPhone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2b45f61-8a07-45ba-a349-859ed84c7415/iphone-large-opt.jpg">Large preview</a>)</figcaption></figure>

Web‐capable mobile devices existed before the iPhone, but they were mostly limited to displaying a specialised mobile‐friendly file format called <abbr>WML</abbr>. Very few devices could render <abbr>HTML</abbr>. With the introduction of the iPhone and its competitors, handheld devices were shipping with modern web browsers capable of being first‐class citizens on the web. This threw the field of web design into turmoil.

Assumptions that had formed the basis for an entire industry were now being called into question:

*   How do we know if people are using wide desktop screens or narrow handheld screens?
*   How do we know if people are browsing with a fast broadband connection at home or with a slow mobile network?
*   How do we know if a device even supports a particular technology or plug‐in?

The rise of mobile devices was confronting web designers with the true nature of the web as a flexible medium filled with unknowns.

The initial reaction to this newly‐exposed reality involved segmentation. Rather than rethink the existing desktop‐optimised website, what if mobile devices could be shunted off to a separate silo? This mobile ghetto was often at a separate subdomain to the “real” site: m.example.com or mobile.example.com.

This segmented approach was bolstered by the use of the term “the mobile web” instead of the more accurate term “the web as experienced on mobile.” In the tradition of their earlier consensual hallucinations, web designers were thinking of mobile and desktop not just as separate classes of device, but as entirely separate websites.

Determining which devices were sent to which subdomain required checking the browser’s user‐agent string against an ever‐expanding list of known browsers. It was a Red Queen’s race just to stay up to date. As well as being error‐prone, it was also fairly arbitrary. While it might have once been easy to classify, say, an iPhone as a mobile device, that distinction grew more difficult over time. With the introduction of tablets such as the iPad, it was no longer clear which devices should be redirected to the mobile <abbr>URL</abbr>. Perhaps a new subdomain was called for — t.example.com or tablet.example.com — along with a new term like “the tablet web”. But what about the “<abbr>TV</abbr> web” or the “internet‐enabled fridge web?”

## We Are One

The practice of creating different sites for different devices just didn’t scale. It also ran counter to a long‐held ideal called One Web:
<blockquote>One Web means making, as far as is reasonable, the same information and services available to users irrespective of the device they are using.</blockquote>

But this doesn’t mean that small‐screen devices should be served page layouts that were designed for larger dimensions:
<blockquote>However, it does not mean that exactly the same information is available in exactly the same representation across all devices.</blockquote>

If web designers wished to remain true to the spirit of One Web, they needed to provide the same core content at the same <abbr>URL</abbr> to everyone regardless of their device. At the same time, they needed to be able to create different layouts depending on the screen real‐estate available.

The shared illusion of a one‐size‐fits‐all approach to web design began to evaporate. It was gradually replaced by an acceptance of the ever‐changing fluid nature of the web.</p>

## Positive Response

In April of 2010 Ethan Marcotte stood on stage at An Event Apart in Seattle, a gathering for people who make websites. He spoke about an interesting school of thought in the world of architecture: responsive design, the idea that buildings could change and adapt according to the needs of the people using the building. This, he explained, could be a way to approach making websites.

One month later he expanded on this idea in an article called <em>Responsive Web Design</em>. It was published on A List Apart, the same website that had published John Allsopp’s <em>A Dao Of Web Design</em> ten years earlier. Ethan’s article shared the same spirit as John’s earlier rallying cry. In fact, Ethan begins his article by referencing <em>A Dao Of Web Design</em>.

Both articles called on web designers to embrace the idea of One Web. But whereas <em>A Dao Of Web Design</em> was largely rejected by designers comfortable with their <abbr>WYSIWYG</abbr> tools, <em>Responsive Web Design</em> found an audience of designers desperate to resolve the mobile conundrum.</p>

## The Adjacent Possible

Writer Steven Johnson has documented the history of invention and innovation. In his book <em>Where Good Ideas Come From</em>, he explores an idea called “the adjacent possible”:
<blockquote>At every moment in the timeline of an expanding biosphere, there are doors that cannot be unlocked yet. In human culture, we like to think of breakthrough ideas as sudden accelerations on the timeline, where a genius jumps ahead fifty years and invents something that normal minds, trapped in the present moment, couldn’t possibly have come up with. But the truth is that technological (and scientific) advances rarely break out of the adjacent possible; the history of cultural progress is, almost without exception, a story of one door leading to another door, exploring the palace one room at a time.</blockquote>

This is why the microwave oven could not have been invented in medieval France; there are too many preceding steps required — manufacturing, energy, theory — to make that kind of leap. Facebook could not exist without the World Wide Web, which could not exist without the internet, which could not exist without computers, and so on. Each step depends upon the accumulated layers below.

By the time Ethan coined the term Responsive Web Design a number of technological advances had fallen into place. As I wrote in the foreword to Ethan’s subsequent book on the topic:
<blockquote>The technologies existed already: fluid grids, flexible images, and media queries. But Ethan united these techniques under a single banner, and in so doing changed the way we think about web design.</blockquote>

1.  Fluid grids. The option to use percentages instead of pixels has been with us since the days of `TABLE` layouts.
2.  Flexible images. Research carried out by Richard Rutter showed that browsers were becoming increasingly adept at resizing images. The intrinsic dimensions of an image need not be a limiting factor.
3.  Media queries. Thanks to the error‐handling model of <abbr>CSS</abbr>, browsers had been adding feature upon feature over time. One of those features was <abbr>CSS</abbr> media queries — the ability to define styles according to certain parameters, such as the dimensions of the browser window.

The layers were in place. A desire for change — driven by the relentless rise of mobile — was also in place. What was needed was a slogan under which these could be united. That’s what Ethan gave us with Responsive Web Design.</p>

## Changing Mindset

The first experiments in responsive design involved retrofitting existing desktop‐centric websites: converting pixels to percentages, and adding media queries to remove the grid layout on smaller screens. But this reactive approach didn’t provide a firm foundation to build upon. Fortunately another slogan was able to encapsulate a more resilient approach.

Luke Wroblewski coined the term Mobile First in response to the ascendency of mobile devices:
<blockquote>Losing 80% of your screen space forces you to focus. You need to make sure that what stays on the screen is the most important set of features for your customers and your business. There simply isn’t room for any interface debris or content of questionable value. You need to know what matters most.</blockquote>

If you can prioritise your content and make it work within the confined space of a small screen, then you will have created a robust, resilient design that you can build upon for larger screen sizes.

Stephanie and Bryan Rieger encapsulated the mobile‐first responsive design approach:
<blockquote>The lack of a media query is your first media query.</blockquote>

In this context, Mobile First is less about mobile devices per se, and instead focuses on prioritising content and tasks regardless of the device. It discourages assumptions. In the past, web designers had fallen foul of unfounded assumptions about desktop devices. Now it was equally important to avoid making assumptions about mobile devices.

Web designers could no longer make assumptions about screen sizes, bandwidth, or browser capabilities. They were left with the one aspect of the website that was genuinely under their control: the content.

Echoing <em>A Dao Of Web Design</em>, designer Mark Boulton put this new approach into a historical context:
<blockquote>Embrace the fluidity of the web. Design layouts and systems that can cope to whatever environment they may find themselves in. But the only way we can do any of this is to shed ways of thinking that have been shackles around our necks. They’re holding us back.
<em>Start designing from the content out, rather than the canvas in.</em></blockquote>

This content‐out way of thinking is fundamentally different to the canvas‐in approach that dates all the way back to the Book of Kells. It asks web designers to give up the illusion of control and create a materially‐honest discipline for the World Wide Web.

Relinquishing control does not mean relinquishing quality. Quite the opposite. In acknowledging the many unknowns involved in designing for the web, designers can craft in a resilient flexible way that is true to the medium.

Texan web designer Trent Walton was initially wary of responsive design, but soon realised that it was a more honest, authentic approach than creating fixed‐width Photoshop mock‐ups:
<blockquote>My love for responsive centers around the idea that my website will meet you wherever you are — from mobile to full‐blown desktop and anywhere in between.</blockquote>

For years, web design was dictated by the designer. The user had no choice but to accommodate the site’s demand for a screen of a certain size or a network connection of a certain speed. Now, web design can be a conversation between the designer and the user. Now, web design can reflect the underlying principles of the web itself.

On the twentieth anniversary of the World Wide Web, Tim Berners‐Lee wrote an article for Scientific American in which he reiterated those underlying principles:
<blockquote>The primary design principle underlying the Web’s usefulness and growth is universality. The Web should be usable by people with disabilities. It must work with any form of information, be it a document or a point of data, and information of any quality — from a silly tweet to a scholarly paper. And it should be accessible from any kind of hardware that can connect to the Internet: stationary or mobile, small screen or large.</blockquote>

### References

1.  [<cite>A Dao of Web Design</cite>](https://alistapart.com/article/dao) by John Allsopp
2.  [<cite>The Vignelli Canon</cite>](https://www.vignelli.com/canon.pdf) by Massimo Vignelli
3.  [<cite>Openness and the Metaverse Singularity</cite>](https://www.kurzweilai.net/openness-and-the-metaverse-singularity) by Jamais Cascio
4.  [<cite>One Web</cite>](https://www.w3.org/TR/mobile-bp/#OneWeb) by Jo Rabin and Charles McCathieNevile
5.  [<cite>Responsive Web Design</cite>](https://alistapart.com/article/responsive-web-design) by Ethan Marcotte
6.  [<cite>A Richer Canvas</cite>](https://markboulton.co.uk/journal/a-richer-canvas) by Mark Boulton
7.  [<cite>Fit To Scale</cite>](https://trentwalton.com/2011/05/10/fit-to-scale/) by Trent Walton
8.  [<cite>Long Live the Web: A Call for Continued Open Standards and Neutrality</cite>](https://www.scientificamerican.com/article/long-live-the-web/) by Tim Berners‐Lee

{{< signature "yk, il" >}}

