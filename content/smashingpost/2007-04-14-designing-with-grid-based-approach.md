---
title: Designing With Grid-Based Approach
slug: designing-with-grid-based-approach
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8916ce3f-db08-4c9a-8ba7-18bd6761ab52/grid-00.gif'
date: 2007-04-14T09:50:48.000Z
author: vitaly-friedman
description: >-
  The main idea behind grid-based designs is a **solid visual and structural
  balance of web-sites** you can create with them. Sophisticated layout
  structures offer more flexibility and enhance the visual experience of
  visitors. In fact, users can easier follow the consistency of the page, while
  developers can update the layout in a well thought-out, consistent way.
  However, it's quite hard to find your way through all the theory behind grid
  systems: it isn't easy at all. Some important notions and related key-facts
  can help to learn basics and keep essential techniques in mind.
categories:
  - Design
  - Web Design
  - Techniques
  - Grids
  - Mathematics
---
The main idea behind grid-based designs is a <strong>solid visual and structural balance of web-sites</strong> you can create with them. Sophisticated layout structures offer more flexibility and enhance the visual experience of visitors. In fact, users can easier follow the consistency of the page while developers can update the layout in a well thought-out, consistent way. However, it's quite hard to find your way through all the theory behind grid systems: it isn't easy at all. Some important notions and related key facts can help to learn basics and keep essential techniques in mind.

And this is what this article is all about. Inspired by Khoi Vinn's and Mark Boulton's presentation Grids are Good, we've decided to take a deep look in the articles about grid-based designs. We've read through over 50 articles and selected some of the <strong>most important and interesting facts web-developers should know about the grid-based approach</strong>. Besides, we've listed the most useful references, tutorials and tools we found - with precise descriptions of what the articles are about. 

You may want to take a look at the following newer related posts:

*   [Grid-Based Web Design, Simplified](https://www.smashingmagazine.com/2010/04/grid-based-web-design-simplified/)
*   [Grid-Based Design: Six Creative Column Techniques](https://www.smashingmagazine.com/2008/03/grid-based-design-six-creative-column-techniques/)
*   [CSS Grid, Flexbox And Box Alignment: Our New System For Web Layout](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)

## Examples of Grid-based design in 2007

But first few examples of grid-based designs to make clear what the article is about.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/840825b7-b1a7-4e5e-badd-4ec7dec35cbc/grid-00.png" alt="Screenshot of the UX Mag homepage" height="245" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ab89dc-37d2-4c89-9cd5-5dcb43087412/grid-02-78x39.png" alt="Screenshot of the New York Times homepage" height="245" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2aaef597-edc7-4bc9-8322-d1468dacb772/grid-05.png" alt="Screenshot of the Times Online homepage" height="245" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fe1c498-48ce-447a-b3b6-d40e8dcffcc4/grid-07.png" alt="Screenshot of Jeff Crofts homepage" height="245" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70df6c3-1a81-4b9a-be65-727826b4c1c5/grid-06.png" alt="Screenshot of an article at the Guardian Online" height="245" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c220d75-ae5d-4547-ab61-2398551d0358/grid-04.png" alt="Screenshot of the Subtraction website" height="245" /></figure>

## Things You Probably Don’t Know About Grid-based Design

*   "The grid is the most vivid manifestation of the will to order in graphic design. [...] Units are the basic buildung block of a grid. They're all uniform. Columns are the grouping of units that create the visual structure of the page. They are not necessary uniform."
*   "A grid is a consistent system for placing objects. It works on two levels: At the unit level of cells (e.g. 20x20 pixels) and at the column level (e.g. 4 columns)." [ [Grid-based Layout](https://www.welie.com/patterns/showPattern.php?patternID=grid-based-layout) ].
*   "A balanced and consistently implemented design scheme will increase readers' confidence in your site. [...] Your first step is to establish a basic layout grid. With this graphic "backbone" you can determine how the major blocks of type and illustrations will regularly occur in your pages. [..] To start, gather representative examples of your text, along with some graphics, scans, or other illustrative material, and experiment with various arrangements of the elements on the page. [...] Your **goal is to establish a consistent, logical screen layout, one that allows you to "plug in" text and graphics without having to stop** and rethink your basic design approach on each new page."
*   "One of the larger problems in working with grids in web pages is that you often can’t do much about vertical proportions. Often your content is dynamic, so the best you can do is approximate. [...] So the focus is usually on the horizontal layout, which usually means columns." [ [Dave Shea](https://www.mezzoblue.com/archives/2005/05/13/columns_grid/index.php) ]
*   "On the Web, vertical rhythm – the spacing and arrangement of text as the reader descends the page – is contributed to by three factors: font size, line height and margin or padding. [..] The basic unit of vertical space is line height." [ [Richard Rutter](https://24ways.org/2006/compose-to-a-vertical-rhythm) ]
*   "In order that typographic integrity is maintained when text is resized by the user **we must use ems for all our vertical measurements**, including line-height, padding and margins." [ [Richard Rutter](https://24ways.org/2006/compose-to-a-vertical-rhythm) ]
*   "Designing Grid Systems in Graphic Design, 1\. figure out the page size, 2\. divide it into a grid, 3\. start designing". [ Josef Muller-Brockmann's "Grid Systems in Graphic Design" ]
*   "Use the canonical grid to adjust the sizes and positions of elements across rows. **Short elements are extended to begin and end on grid boundaries, while long elements are allowed to span multiple grid units** or are shortened to fit within the standard unit. In this way, the grid is merely being used to help establish consistent alignment relationships. [...] For dynamic layouts, identifying the minimum size that can be accomodated by the layout is usually a better solution than trying to recompute the layout for arbitrarily small display sizes." [ Module and Program ]
*   "One of the **most effective principles in grid design is called the Rule of Thirds**, also known as the golden grid rule. The Rule of Thirds is a technique which is applied by dividing a space into thirds, both vertically and horizontally, creating a grid of rectangles." — _Mark Boulton_
*   "The Golden Section, Golden Ratio, and the grandiose Divine Proportion are all names for the same thing; a ratio of 1.618\. Nodding off? Not yet? Good! Bear with me. Here?s the maths: **the Golden Ratio is the ratio between two segments so that the ratio between point ac/bc is 1.618.**" _— Mark Boulton_. You can also use Phiculator for your grids.
*   "The Golden Section is a ratio which is evident throughout the universe as the number Phi. You can use this ratio to good effect in design by making sure that elements of your grid conform to this ratio. Using the Golden Section can ensure a natural sense of correct composition, even though it is based in mathematics it will 'feel' right." — _Mark Boulton_
*   "Grid Structures: Once you have answered most of the questions regarding the content, format and typography, you should begin sketching out grid structures based on the appropriate page sizes and formats. You should first begin by defining the Type Area. The Type Area is the area where your grid will be contained. It is surrounded on all sides by margins and in some cases running heads and page footers, numbers, marginalia, etc." [ Typographic Grids ]
*   "The main principle of the baseline grid is that **the bottom of every line of text (the baseline) falls on a vertical grid set in even increments** all the way down the page." [ [Wilson Miner](https://www.alistapart.com/articles/settingtypeontheweb) ]
*   "You can **use relative sizes, but it quickly becomes a lot more difficult to maintain** as the math becomes more complicated. It’s easy to get 12 out of 18 (just set the line-height to 1.5em), but when you want to adjust the text size but keep the same line-height, the fractions start to get messy". [ [Wilson Miner](https://www.alistapart.com/articles/settingtypeontheweb) ]
*   "**Table layouts are great for grid designs.** The markup itself reproduces a specific grid, and the tendency is for us to just fill up the boxes with the images, type, and interface elements that make up our design." [ [Molly Holzschlag](https://www.alistapart.com/articles/outsidethegrid) ]
*   "Ratios are at the core of any well designed grid system. [..] By using the size of the paper as a guide we can divide using that ratio to begin creating the grid. You can see this through diagrams 1 - 6 that we begin by simply layering division upon division to slowly build up the grid." [ Mark Boulton ]
*   "Well designed grid systems can make your designs not only more beautiful and legible, but **more usable**." [ Mark Boulton ]
*   "Gutters are the gaps in between columns. They are there so text, or image, from different columns don't run into each other. In grid system design **sometimes**, depending on what theory you read, **gutters are seperate to the columns**." [ Mark Boulton ]
*   "The thing about designing to grids is that in order for the grid to work you must consistently align items on the grid lines." [ Mark Boulton ]
*   "One of the most useful 'tools' for creating pixel-perfect grid systems for the web is Khoi's superb idea of using a grid as a background-image element on the body tag. To summarise: Using the grid I designed in photoshop, I save it out as a gif and then apply that to the background of the body tag. This provides me, throughout the build of the site, the grid so I can align all the content elements accordingly." [ Mark Boulton ]
*   "In your page layout, you've probably set margins. These margins often show up as light solid or dashed lines on the screen. These top, bottom, left, and right margins create a box in the middle of your page. Stop there and you have a **single unit grid**. Further divide the page into uniform parts and you've created a **multiple unit grid**." [ [Jacci Howard Bear](https://desktoppub.about.com/od/grids/l/aa_gridsorder.htm) ]
*   "Grid units are the primary locations on your page where you will place text and images. They determine placement not necessarily size. That is, if you have a graphic image that is larger than your grid unit, it doesn't mean you can't use it. " [ [Jacci Howard Bear](https://desktoppub.about.com/od/grids/l/aa_gridsorder.htm) ]
*   "1, 2, and 3 column grids are common. Each can accommodate lots of text, especially long articles. [..] 4 or more columns offer greater flexibility for publications with text, photos, and other graphic elements and a mix of long and short articles. [..] Grids based on an even number of grid columns can suffer from too much symmetry if text and graphics are confined to individual or double grid columns throughout." [ [Grids - Flexible Options](https://desktoppub.about.com/od/grids/l/aa_gridsflex.htm) ]
*   "A grid is made up of vertical and horizontal lines and is the foundation of nearly every type of visual media. The structure is there to shape the content into proportions that are pleasing to the eye." [ Anne Van Wagener ]
*   "To add flexibility you can break the grid down into 10 or 12 columns. Half-columns are a good place to anchor mug-shots, refers, and other info." [ Anne Van Wagener ]
*   "You can have more than one grid. Your front page could be based on a five column grid while inside pages with ads on a six column. There is no one right way." [ Anne Van Wagener ]
*   "The grid is the mannequin and the comp is the pattern. [..] Using the grid-based design comps provided me with units of measurement that I could easily turn into divs for the style sheet. I figure out the areas of content in the same way I would work with a wireframe to block out content and graphics. I come up with a naming scheme for these blocks and turn them into CSS elements. Next, I measure out the blocks of content or graphics in the designer's comp and record measurements for my style sheet." [ Michael Angeles ]
*   "You can use the grid like a wireframe (page schematic) by selecting areas of content and blocking them out, labeling them as you go." [ Michael Angeles ]
*   "Basic Outline for Grid-based Design: Content, Audience, Illustrations / Photography / Icons, Format, Typography." [ Feeling your way around grids ]

## Articles about Grid-based Design Approach

<ul>
 	<li><a href="https://www.mezzoblue.com/archives/2005/05/13/columns_grid/index.php" rel="nofollow">Columns &amp; Grids</a>
Dave Shea talks about the difficulty of grid systems in web pages and the compromise of columns.
<figure><a href="https://www.mezzoblue.com/archives/2005/05/13/columns_grid/index.php" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/723355c4-a15b-479a-b166-852039249c96/gridlinks-00.png" alt="A wireframe of a grid-based design by Dave Shea" height="140" /></a></figure></li>
 	<li>Subtraction: Oh Yeeaahh! - "Grids Are Good"
Download the "Grids are Good" presentation (8 MB PDF) created by Khoi Vinh and Mark Boulton. <a href="https://www.subtraction.com/archives/2007/0402_layers_cake.php" rel="nofollow">Layers Cake</a>.</li>
 	<li><a href="https://24ways.org/2006/compose-to-a-vertical-rhythm" rel="nofollow">Compose to a Vertical Rhythm</a>
On the Web, vertical rhythm – the spacing and arrangement of text as the reader descends the page – is contributed to by three factors: <strong>font size, line height and margin or padding</strong>. All of these factors must calculated with care in order that the rhythm is maintained.</li>
 	<li>Design grids for Web pages
No one design grid system is appropriate for all Web pages. Your first step is to establish a basic layout grid. With this graphic "backbone" you can determine how the major blocks of type and illustrations will regularly occur in your pages and set the placement and style guidelines for major screen titles, subtitles, and navigation links or buttons.</li>
 	<li><a href="https://www.emanuelblagonic.com/2007/02/16/developing-the-grid-that-supports-your-design/" rel="nofollow">Developing the grid that supports your design</a>
Just a few months ago when I created any design, I didn’t practice a grid system. I didn’t know much about it so I thought that I can live without it. Yes it’s true. You can live without a grid system, but should you? Why is the grid important? I will try to answer to all of your questions in this article.</li>
 	<li>Grid-Based Design
Few basic rules and techniques in grid-based design.<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aefcbb2-8be6-48c5-877b-d853570f6589/gridlinks-01.png" alt="Bottom end of an example of a grid wireframe" height="140" /></figure></li>
 	<li>Typographic Grids
Grids, Ratios and Typography. Theories, such as the golden ratio (also known as the golden mean, golden number, golden section, golden proportion, divine proportion and section aurea) arise from natural patterns and they are applied in the visual and creative fields to create "beauty" by way of considered composition. The Golden Section is derived from a naturally occurring number, called Phi (1.618), which has intrigued humanity for thousands of years.</li>
 	<li>The Grid: The Structure of Design
Using a grid is one of those basic design principles. Most news designers are working with a grid someone else designed. No matter what you think about it, you need to understand how to use it. And, at some point in your career you will likely be called upon to create a grid for a new section, or to do a re-design for a paper.</li>
 	<li>Cutting and sewing grid-based design: Part 1,working with other people's comps
"In this article I'm going to discuss the steps I take when measuring and cutting a comp layed over a grid and turning that data into CSS. The point is to demonstrate the steps to site developers who are new to grids."<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6266727-eeee-49cf-8b41-1be54c192927/gridlinks-02.png" alt="A grid wireframe with text added to describe the different parts in it" height="140" /></figure></li>
 	<li><a href="https://www.digital-web.com/articles/principles_of_design/" rel="nofollow">The Principles of Design</a>
We can group all of the basic tenets of design into two categories: principles and elements. For this article, the principles of design are the overarching truths of the profession. They represent the basic assumptions of the world that guide the design practice, and affect the arrangement of objects within a composition.</li>
 	<li>Grid-based design: Designing blog theme templates
The previous grid article dealt with how to come up with a CSS strategy when you're working with another visual designer's comps. Now I'd like to discuss doing grid-based theme design for open source content management systems, e.g. Drupal and WordPress....</li>
 	<li>Feeling your way around grids
Designing grids carefully and thoughtfully, using simple compositional theory, such as the Rule of Thirds or the Golden Section, increases the legibility of your designs. By using a grid a designer shows an understanding of systems within visual communication and a sympathetic knowledge of conventions.<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b2fb1f0-5adc-4edd-8310-806bca95db6d/gridlinks-03.png" alt="Screenshot of an article about the West End of London" height="140" /></figure></li>
 	<li><a href="https://www.welie.com/patterns/showPattern.php?patternID=grid-based-layout" rel="nofollow">Grid-based Layout</a>
A grid is a technique that comes from print design but easily be applied to web design as well. In its strictest form a grid is literally a grid of X by Y pixels. The elements on the page are then placed on the cell border lines and overall aligned on horizontal and vertical lines.
<figure><a href="https://www.welie.com/patterns/showPattern.php?patternID=grid-based-layout" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef0de46a-37e3-4eec-af5a-ae3ff9703fa0/gridlinks-04.png" alt="Screenshot of a grid overlay on the Audi Website" height="140" /></a></figure></li>
 	<li>Grid Computing… and Design
A look at the layout grid behind the Subtraction's 7.0 redesign.</li>
 	<li>Adobe Web Tech Curriculum - Page Layout Grids
Introduction to Layout Grids. On each page layout grid, you'll want to decide placements for main content, branding or logo, page title, global and local navigation elements, copyright or contact information, etc.</li>
 	<li><a href="https://www.alistapart.com/articles/settingtypeontheweb" rel="nofollow">Setting Type on the Web to a Baseline Grid</a>
We web designers get excited about the littlest things. Our friends in the print world must get a kick out of watching us talk about finally being able to achieve layouts on the web that they’ve taken for granted for years. Let’s face it: it’s easier these days to embed a video on the web than it is to set type consistently or align elements to a universal grid....A List Apart Article by Wilson Miner</li>
 	<li><a href="https://www.subtraction.com/archives/2005/0901_the_funniest.php" rel="nofollow">The Funniest Grid You Ever Saw</a>
An in-depth look at the complicated layout grid behind The Onion.<figure><a href="https://www.subtraction.com/archives/2005/0901_the_funniest.php" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50ae2492-5eb5-4137-a428-277e7a5c9168/gridlinks-05-84x84.png" alt="Screenshot of the The Onion homepage" height="140" /></a></figure></li>
 	<li><a href="https://www.smileycat.com/miaow/archives/000264.php" rel="nofollow">Using a Background Image Grid to Lay Out Your Web Site</a>
"Simply put, you apply the grid to the body of your page as a background image so that it displays behind your site. Thus you can use it to precisely line up your layout." Article by Christian Watson.</li>
 	<li>Why use a grid?
Grid design is a fundamental skill of any designer. Understanding proportional relationships, white space and composition are all vital in constructing a grid for any delivery platform - web, print &amp; real 3d environments.</li>
 	<li><a href="https://en.wikipedia.org/wiki/Grid_(page_layout)" rel="nofollow">Wikipedia: Grid (page layout)</a>
A typographic grid is a two-dimensional structure made up of a series of intersecting vertical and horizontal axis used to structure content. The grid serves as an armature on which a designer can organize text and images in a rationalist, easy to absorb manner....</li>
 	<li><a href="https://www.alistapart.com/articles/outsidethegrid" rel="nofollow">Thinking Outside the Grid</a>
“There is a new kid on the block, and her name is ‘I’ve never designed with a table in my career.’” An article by Molly E. Holzschlag<figure><a href="https://www.alistapart.com/articles/outsidethegrid" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/978159f4-5bfd-4672-9dce-364d7a8d8375/gridlinks-06.png" alt="Boxes creating a grid" height="140" /></a></figure></li>
 	<li>Grids: Show 'em if you got 'em
Grids are a topic that’s rarely discussed or disected in the online community, yet is one of the fundamental components of good design. Why is it that many designers have a hard time with the grid?</li>
 	<li>Grid systems in Web Design
An overview of grid-based techniques. Every design you make should have a clear grid system whether its print or for the web because they help to organise information into a clear easy to follow layout. Here we roundup the best articles and resources on the subject.</li>
</ul>

## Tutorials

<ul>
 	<li>Five simple steps to designing grid systems - Preface
In the context of graphic design, a grid is an instrument for ordering graphical elements of text and images. The grid is a child of Constructivist art and came into being through the same thought processes that gave rise to that art movement.</li>
 	<li>Five simple steps to designing grid systems - Part 1
The first part of this Five Simple Steps series is taking some of the points discussed in the preface and putting it to practice.</li>
 	<li>Five simple steps to designing grid systems - Part 2
In part one of this Simple Steps series I talked about how to use a simple ratio, that of the paper size you are using, to create a symmetrical grid on which to create your designs. This, the second part in the series, will deal with other ratios and how they can be combined to create more complex grid systems.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70aa017-c8fc-4e1f-9626-780339cd7a9f/gridlinks-07.png" alt="Screenshot of a grid wireframe" height="140" /></figure></li>
 	<li>Five simple steps to designing grid systems - Part 3
The third installment to this series is going to be a little different. The previous installments have been talking through some of the basics of grid construction using ratios as the primary device.</li>
 	<li>Five simple steps to designing grid systems - Part 4
For the purposes of this article, I'm going to be focussing on the theory of creating the grid rather than the implementation. I did mention in the last series that I would cover implementation using CSS, well I'm not going to.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20c15fa1-bec1-4535-962a-597d6716dbad/gridlinks-08.png" alt="Grid overlay of the BBC website" height="140" /></figure></li>
 	<li>Five simple steps to designing grid systems - Part 5
Flexible vs Fixed. Which one to choose? Why choose one over the other? Well you won't find the answers to those questions here. What I'm aiming to do with this article is to investigate how the theory of grid design can be applied to a flexible web page.</li>
 	<li>Grids make eyes happy: how to use Grids
An example on how to create effective grid systems.</li>
 	<li><a href="https://desktoppub.about.com/od/grids/l/aa_gridsorder.htm" rel="nofollow">Grids: Order Out of Chaos</a>
Invisible Structures: When and Why to Use Grids in Page Layout. Many of the pages that you see everyday have a grid. You may not see it but it is there, holding up the design, establishing structure, guiding the page elements.</li>
 	<li><a href="https://www.aisleone.net/?p=301" rel="nofollow">Designing Grid Systems for Flash</a>
I’ve decided that I’m going to write a little something up for those people interested in grids. I’m going to walk you through the process of creating a grid for a Flash based site that will work for screen resolutions of 1024×768 and up.</li>
 	<li>How to Create Page Layouts in GoLive CS2
GoLive CSS-based or table-based layout grids enable you to create designs by freely positioning objects anywhere on the page. You can convert a CSS-based layout grid to a table-based layout grid. You can also convert a table-based layout grid to an HTML table.</li>
</ul>

## Useful Tools for Grid-based Designs

<ul>
 	<li><a href="https://nickcowie.com/other/golden_section.html" rel="nofollow">Adaptive Grid System based on the Golden Section</a>
The Columns are defined using em to keep line length consistent and varying text size using javascript to make the web page fill the browser window.</li>
 	<li><a href="https://www.andybudd.com/archives/2006/07/layout_grid_bookmarklet/" rel="nofollow">Layout Grid Bookmarklet </a>
Inspired by Khoi Vinh’s post about using a background image of a grid for layout, and a subsequent post over at Smiley Cat about the same thing, I decided to knock up a quick Photoshop style Layout Grid Bookmarklet....</li>
 	<li><a href="https://subtlegradient.com/articles/2006/07/27/grid-overlay-bookmarklet" rel="nofollow">Grid Overlay Bookmarklet</a>
Just a quick note to share my version of Andy Budd’s <a href="https://www.andybudd.com/archives/2006/07/layout_grid_bookmarklet/" rel="nofollow">Layout Grid Bookmarklet</a>.</li>
 	<li>WPDFD Browser Grid
This grid represents the maximum safe sizes for the three main monitor sizes in use today (June 2001). It takes into account such things as browser menubars and scrollbars and assumes that the browser window has been maximised. 640 x 480, 800 x 600, 1024 x 768</li>
 	<li><a href="https://www.incompetech.com/beta/plainGraphPaper/" rel="nofollow">Free Online Graph Paper / Grid Paper PDFs</a>
Downloadable and very printable</li>
 	<li><a href="https://cameronmoll.com/archives/2006/12/gridding_the_960/" rel="nofollow">Gridding the 960</a>
Background image grid + pixel ruler + column divisions for 960px-width layout, all in one mean little package.
<figure><a href="https://cameronmoll.com/archives/2006/12/gridding_the_960/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21bb1a66-52aa-410b-9012-5f8740bcd42d/gridlinks-10.png" alt="A chart in a grid layout" height="140" /></a></figure></li>
 	<li><a href="https://www.smileycat.com/miaow/archives/layout_grid.php" rel="nofollow">Web Page Layout Grid</a>
Add this image as a background to the body of your page to help you lay it out.</li>
 	<li><a href="https://positioniseverything.net/articles/onetruelayout/verticalgrid" rel="nofollow">Position is Everything - Vertical Grids</a>
A method enabling the vertical positioning of elements across grids/columns</li>
 	<li><a href="https://www.gwhite.us/downloads/css_grid_calc.html" rel="nofollow">CSS Grid Calculator</a>
Use the CSS Grid Calculator to quickly visualize page layout and draw grids in a variety of ways. It provides accurate visual feedback on how text blocks and page divisions will appear within a browser window, and returns style declarations for divisions and text to copy and paste into style sheets.</li>
 	<li><a href="https://milianw.de/projects/typogridder/" rel="nofollow">TypoGridder</a>
To get to the heart of it: a baseline grid is added. You initialize the TypoGridder and it automatically gets the lineheight of an element (by default p, but you can choose any jQuery selector). Then it queries a little PHP script which creates a very simple image which is used for tiling. The result is an opaque layer with a tiling baseline grid.</li>
 	<li><a href="https://www.airbagindustries.com/archives/airbag/ruler.php" rel="nofollow">Grid Ruler</a>
A simple image that can be applied as the background to most block level elements that will help you get an idea what's going on between browsers and platforms without the need for another application.
<figure><a href="https://www.airbagindustries.com/archives/airbag/ruler.php" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36087583-f2c0-4761-89aa-2c4bf02b5729/gridlinks-09.png" alt="Screenshot of an image of a ruler accompanied by some text" height="140" /></a></figure></li>
 	<li>YUI: CSS Grid Builder
A simple interface for Grids customization.</li>
 	<li>YUI Grids CSS
The foundational YUI Grids CSS file offers three preset page widths, seven core templates, and the ability to nest subdivided regions of one to four columns..</li>
 	<li>How to play with Yahoo Grids CSS
Yahoo released their Yahoo! User Interface. One part of which is their webpage templates, the Grids CSS. To follow along you will need to download the YUI library, a working test Drupal install and a text editor of some sort.</li>
 	<li>Page Grids
Successful web page design often leverages methods rooted in print design by utilizing an underlying grid system. First, establish a grid, or system of grids, that take into account advertising needs, dynamic elements, etc. Next, create templates and code to support designers and developers..</li>
 	<li>Hacking Technique: Yahoo's Grid System (Part 1)
"And what Yahoo! UI CSS Grid has to do with us? Well, I tried to integrate Yahoo! Grid into Blogger Beta, and the result was sweet. By injecting some additional CSS code and some div tags into the simplified version of the Beta template, one can rearrange one's layout without any CSS knowledge. This article will show you how to do that."</li>
 	<li>Hacking Technique: Yahoo's Grid System (Part 2)
In this post, I get into some technical details, and it also serves as a note for myself in finding interesting things about the Yahoo! CSS Grid system. Read on if you curious on how 3, 4, or 5 columns can be achieved.</li>
 	<li><a href="https://os3grid.sourceforge.net/website/index.html" rel="nofollow">OS3Grid - Grid for Web Sites</a>
OS3Grid a JavaScript component allowing you to create and use powerful grids in your web sites.
As you can see from the Examples OS3Grid is both flexible and powerful, with a rich set of features and an easy to use API for the developer.</li>
</ul>

## Grid design-related books

*   "Grid Systems in Graphic Design" by _Josef Muller-Brockmann_
*   "Geometry of Design: Studies in Proportion and Composition" by _Kimberly Elam_
*   "Grids for the Internet and Other Digital Media" by _Veruschka Gotz_
*   "Geometry of Design" by _Kimberly Elan_
*   "The Elements of Typographic Style" by _Robert Bringhurst_
*   "Making and Breaking the Grid: A Graphic Design Layout Workshop" by _Timothy Samara_

