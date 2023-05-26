---
title: 'Enhancing Grid Design With GuideGuide, A Plugin For Photoshop And Illustrator'
slug: enhancing-grid-design-guideguide-plugin-photoshop-illustrator
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d725fca-669b-488e-bd69-ee54f26c371d/create-guides-outside-of-the-context-preview-opt.png
date: 2016-11-30T17:59:53.000Z
author: cameron-mcefee
description: >-
  Almost five years ago, I had the honor of [writing a post on Smashing
  Magazine](https://www.smashingmagazine.com/2012/01/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/)
  about my Photoshop panel [GuideGuide](https://guideguide.me). Since then it has
  seen wild success as the most installed third-party Photoshop extension, an
  achievement I’m quite proud. In that time, I’ve added some powerful features
  and, most recently, expanded it to Illustrator. This post will give you a
  taste of how GuideGuide can change the way you use guides in Photoshop and
  Illustrator.

  If you’re one of the many people who already use GuideGuide, please read on.
  You may discover some unconventional uses that are not immediately apparent.
  I’ll provide a overview of the major features, and then give some examples of
  advanced and unusual ways it can be used to make you a more efficient
  designer.
categories:
  - Graphics
  - Tools
  - Illustrator
  - Photoshop
  - Workflow
---
Almost five years ago, I had the honor of <a href="https://www.smashingmagazine.com/2012/01/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/">writing a post on Smashing Magazine</a> about my Photoshop panel <a href="https://guideguide.me">GuideGuide</a>. Since then it has seen wild success as the most installed third-party Photoshop extension, an achievement I’m quite proud. In that time, I’ve added some powerful features and, most recently, expanded it to Illustrator. This post will give you a taste of how GuideGuide can change the way you use guides in Photoshop and Illustrator.

If you’re one of the many people who already use GuideGuide, please read on. You may discover some unconventional uses that are not immediately apparent. I’ll provide a overview of the major features, and then give some examples of advanced and unusual ways it can be used to make you a more efficient designer.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [40 Excellent Adobe Illustrator Tutorials](https://www.smashingmagazine.com/2009/09/back-to-school-with-40-excellent-adobe-illustrator-tutorials/)
*   [Illustrator’s Live Trace: Sketch To Vector](https://www.smashingmagazine.com/2010/11/illustrator-s-live-trace-sketch-to-vector/)
*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)

While I’m going to focus this post on Illustrator, nearly everything is applicable to Photoshop as well.

{{% feature-panel %}}

<em>Please note that at the time of the original Smashing Magazine post, GuideGuide was a free extension. It now costs $10 (you can read about <a href="https://guideguide.me/blog/selling-out-ruining-everything/">why I chose to do this</a>), and it supports Photoshop and Illustrator CC+. To try it for yourself, you can <a href="https://guideguide-downloads.s3.amazonaws.com/guideguide-trial-smashing-magazine.zip">download a special Smashing Magazine edition of the GuideGuide trial</a>. It is fully featured for the first 90 times you use it to add guides.</em>

## System Requirements

This tutorial uses GuideGuide 4, which supports Photoshop and Illustrator CC and later. If you have Photoshop CS5 or CS6, you can still <a href="https://guideguide.me/versions/">download GuideGuide 3</a> for free, which works but lacks some of the features mentioned in this article. Older versions of Illustrator are not supported.

Installation of Adobe extensions is notoriously unpredictable. I’ve done my best to make the process smooth with the included installer and documentation, but if you have issues, you’re always welcome to <a href="https://guideguide.me/support/">contact me for support</a>.</p>

## The Basics

Grids are one of the fundamentals of design, regardless of the tools you use. <a href="https://www.smashingmagazine.com/2010/04/grid-based-web-design-simplified/">Chris Brauckmuller’s article</a>, while a bit dated, is a great quick overview to grids on the web, and <a href="https://www.amazon.com/Making-Breaking-Grid-Graphic-Workshop/dp/1592531253"><em>Making and Breaking the Grid</em></a> deserves a place on every design bookshelf. Many artists and designers have lamented that Photoshop and Illustrator suffer from a lack of grid features. GuideGuide fills this void by automatically doing the complicated math necessary to produce grids, making your design life easier.

I’ve written this post using inches for measurement, but GuideGuide works with all measurement types supported by Illustrator and Photoshop.</p>

### A Basic Grid

Imagine you are preparing an 11 × 8.5-inch document for a trifold brochure, with 0.5-inch margins, a 0.125-inch bleed and a baseline grid. Once you’re a GuideGuide expert, it will be possible to create this grid in a single action; however, I’m going to break it down into steps to illustrate some of GuideGuide’s features.

With a freshly created document open, the first thing to do is add columns. By default, GuideGuide will use the selected artboard as its reference. Enter <code>3</code> in the column-count field, and hit “Add guides.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69b53b8b-c013-4db3-9ab1-c8a4dacc067f/3-columns-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a34328f-0190-4916-97f3-76c037384115/3-columns-preview-opt.png" alt="Image of an Illustrator document with a three column grid." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69b53b8b-c013-4db3-9ab1-c8a4dacc067f/3-columns-large-opt.png">View large version</a>)</figcaption></figure>

Next, we’ll add margins to each column. GuideGuide can use a selected object as its reference; so, create a rectangle that is the size of one of the columns, select it, add <code>.5in</code> in each of the margin fields, and then click “Add guides.” Repeat this process for each column, and leave the shapes in the document for now.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69dca94b-badd-4c2d-a741-1a9db9bc81d8/size-of-the-column-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe80dd76-3897-4d06-95a0-b9c4c135a7de/size-of-the-column-preview-opt.png" alt="Image of an Illustrator document with the grid from before, plus margins for each column." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69dca94b-badd-4c2d-a741-1a9db9bc81d8/size-of-the-column-large-opt.png">View large version</a>)</figcaption></figure>

I mentioned earlier that we’re going to add bleed guides to the document. In this example, we don’t want to use the built-in bleed setting. GuideGuide supports negative values in the form fields, which will allow you to create guides outside of the context. Deselect any shapes you have selected, then put <code>-0.125in</code> in the margin fields, and click “Add guides.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ba8fd14-f03a-488d-a462-38c54a954626/create-guides-outside-of-the-context-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d725fca-669b-488e-bd69-ee54f26c371d/create-guides-outside-of-the-context-preview-opt.png" alt="Image of an Illustrator document with the grid from before, plus guides indicating bleed area." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ba8fd14-f03a-488d-a462-38c54a954626/create-guides-outside-of-the-context-large-opt.png">View large version</a>)</figcaption></figure>

Now that we have our bleed guides, we can expand the artboard to fit them.

Next, we will add a midpoint guide to each column. If you left the column shapes in the document like I suggested, then select the first shape, and use the vertical “Midpoint” quick-guide button at the bottom of the panel. Repeat this for each column.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/526bb959-7f3e-4caf-b7b1-da71786f9e50/add-a-midpoint-guide-to-each-column-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937ac5f5-6c9a-4f62-84ba-f3e09348e7bc/add-a-midpoint-guide-to-each-column-preview-opt.png" alt="Image of an Illustrator document with the grid from before, plus column midpoints." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/526bb959-7f3e-4caf-b7b1-da71786f9e50/add-a-midpoint-guide-to-each-column-large-opt.png">View large version</a>)</figcaption></figure>

If you like to keep things clean and organized, it’s worth noting that GuideGuide adds guides to the active layer (only Illustrator supports layer-specific guides). If you plan ahead, you can create different parts of your grid on separate layers, so that you can turn them on and off independently as needed.

For example, let’s add a baseline grid. Create a new layer named “Baseline grid” and select it. Type <code>16pts</code> into the row height field. When you leave the row count field blank, GuideGuide will automatically fill the screen with rows until it runs out of space. By adding the guides to the selected “Baseline grid” layer, you can turn them on and off separately from your main grid by toggling the layer visibility.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4c040f8-02c3-46b4-b750-d3750f75ade2/baseline-grid-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4000d9ad-f138-4113-a934-638bcd105339/baseline-grid-preview-opt.png" alt="Image of an Illustrator document with a baseline grid created using guides." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4c040f8-02c3-46b4-b750-d3750f75ade2/baseline-grid-large-opt.png">View large version</a>)</figcaption></figure>

## Getting Down To Business

Now that we’ve covered the easy on-the-fly features, let’s dig into some uses of GuideGuide that are super-powerful but require a little thinking ahead.</p>

### Grid Notation

If you fill out some values in the “Form” tab and then click the “Custom” tab, you will find something that looks a little like a programming language. This is <strong>grid notation</strong>, a language you can use in the “Custom” tab (and in the “Form” tab to a certain extent) to tell GuideGuide about your grids. In fact, every feature works by using grid notation under the hood.

Here is a quick introduction. The most important part of grid notation is the pipe character, <code>|</code>. It tells GuideGuide to “put a guide here.” Next is a <strong>command</strong><em>,</em> that says “move over this much.” If you put a bunch of these together, GuideGuide will read it from left to right, interpreting it as “Add a guide, move over, add a guide, move over, add a guide.” You can read all about grid notation <a href="https://guideguide.me/documentation/grid-notation/">in the documentation</a>, including about the commands that help with computation, such as <strong>variables</strong> and <strong>fills</strong>.

For now, I will show you one of the most important grid notation commands, the wildcard <code>~</code>. GuideGuide equally divides whatever space isn’t accounted for in the grid between each wildcard. Practically speaking, this is how GuideGuide calculates the width of columns and rows. For example, <code>| ~ | ~ | ~ |</code> would be a three-column grid.

You may be wondering, if the GuideGuide form can already do all of this, why bother? Consider the common web design pattern of pairing icons with paragraphs.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26422cbf-4a59-4bba-b58e-922517150996/common-web-design-pattern-of-pairing-icons-with-paragraphs-preview-opt-300x160.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b8a49be-f118-439b-b8da-7c25970a56d2/common-web-design-pattern-of-pairing-icons-with-paragraphs-preview-opt.png" alt="Image of an Illustrator document with a three column layout in which each column contains an icon and a paragraph. Below, a ruler measures the width of each element." width="500" height="160" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26422cbf-4a59-4bba-b58e-922517150996/common-web-design-pattern-of-pairing-icons-with-paragraphs-preview-opt-300x160.png">View large version</a>)</figcaption></figure>

Visualize this pattern across the x-axis. There is a bit of space for the page’s margin, the width of the icon, another margin, the width of the paragraph, and then the margin before the next instance of this pattern.

If you are designing a responsive website this way, then you probably know the width of the icon but not of the paragraph. This is where the wildcard is useful. In this example, the document’s margins and gutters are 40 pixels, the icon’s width is 60 pixels, the space between the paragraph is 10 pixels, and the column’s widths are unknown but should be equal to one another. This can be expressed in grid notation like so:

<pre><code>| 40px | 60px | 10px | ~ | 40px | 60px | 10px | ~ | 40px | 60px | 10px | ~ | 40px |</code></pre>

GuideGuide adds up the commands that have an explicit value and subtracts that from the width of the available space. It then splits the remaining area between the wildcards. The result will look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e5f286-c152-41ba-93f9-1a940e79a5ae/document-margins-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4432d0e-e0ec-48b9-a874-e023fef4e111/document-margins-preview-opt.png" alt="Image of an Illustrator document with the icon grid from before, now with guides overlaid on it." width="500" height="160" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e5f286-c152-41ba-93f9-1a940e79a5ae/document-margins-large-opt.png">View large version</a>)</figcaption></figure>

### Grid Notation in Fields

Grid notation in its raw form is powerful, but you’ll often want the convenience of the grid form with just a little bit of that power. For example, what if you want your gutters to have a midpoint? Easy! Just use grid notation. To create a 40-pixel gutter with a midpoint, add <code>20px | 20px</code> to the gutter-width field.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/028ed2ed-dc15-4a03-aeba-b3b5c0c83756/grid-notation-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4968823d-4365-4029-8aeb-598d1b53864c/grid-notation-preview-opt.png" alt="Image of an Illustrator document with a three column grid and gutters with midpoints." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/028ed2ed-dc15-4a03-aeba-b3b5c0c83756/grid-notation-large-opt.png">View large version</a>)</figcaption></figure>

GuideGuide supports basic notation in any field that allows for a measurement input. Going back to the example from earlier, you can create the same effect with the form and a grid notation:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f380a20-60b3-4618-93fd-3b6292901566/little-grid-notation-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ceab8d-dce8-4dcd-b4a3-9cec4a851845/little-grid-notation-preview-opt.png" alt="Image of an Illustrator document with the three column icon grid from before, now created using the GuideGuide form." width="500" height="160" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f380a20-60b3-4618-93fd-3b6292901566/little-grid-notation-large-opt.png">View large version</a>)</figcaption></figure>

Grid notation is super-useful and is a great way to create and share complicated grids, like the <a href="https://codepen.io/CSWApps/post/guideguide">preset grids based on Bootstrap</a> created by Christophor Wilson.</p>

## Getting Weird Guides

With a combination of the form and grid notation, GuideGuide can do almost anything. Going back to our original example of a trifold brochure, the entire grid that I created in multiple steps can actually be done with one.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b14b1aff-1417-461b-937b-d72b2e0ba95f/combination-of-the-form-and-grid-notation-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/827b535a-5d5c-4b4d-b7c2-756a137ff699/combination-of-the-form-and-grid-notation-preview-opt.png" alt="Image of an Illustrator document with guides reflecting margins, bleed, columns, column midpoints, gutters, gutter midpoints, and a baseline grid." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b14b1aff-1417-461b-937b-d72b2e0ba95f/combination-of-the-form-and-grid-notation-large-opt.png">View large version</a>)</figcaption></figure>

It’s even possible to save a grid as a preset to reuse or share with someone.</p>

### The Golden Ratio

While GuideGuide is meant to spare you from doing calculations, some grids benefit from a little math, like a 3 × 3 grid whose guides in the center indicate the golden ratio. I avoid doing math whenever I can, so a quick search tells me that the golden ratio expressed as percentages is <code>38.2%</code> and <code>61.8%</code>. I also know that subtracting one value from <code>100%</code> will give me the other; so, if I type <code>38.2%</code> for each margin, voila! A golden-ratio grid.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e21b94-4a84-44c2-a23a-fbe9b338a022/golden-ratio-grid-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bed9d72-411d-41b3-a6f2-29672c5a157d/golden-ratio-grid-preview-opt.png" alt="Image of an Illustrator document with guides reflecting the golden ratio." width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e21b94-4a84-44c2-a23a-fbe9b338a022/golden-ratio-grid-large-opt.png">View large version</a>)</figcaption></figure>

### The Fibonacci Sequence

To drive home my point that you can do almost anything, how about a grid based on the Fibonacci sequence? I’m going to base the grid on percentages, and the Fibonacci values under 100% are 1%, 1%, 2%, 3%, 5%, 8%, 13%, 21%, 34%, 55%, 89%. We don’t need two guides at 1%; we can leave off the second 1%.

While this seems pretty straightforward, we have to make an adjustment in order for the grid to be accurate. Each command tells GuideGuide to move over; so, each guide’s coordinates are the sum of all commands given up to that point. For example, to express 8% in the sequence, you’d use <code>3%</code>, which is 8% minus the sum of all values before it. Confused? That’s OK. If you try it a few times, you’ll get the hang of it.

Once all of the adjustments have been made, this grid notation string will give you a Fibonacci grid:

<pre><code>| 1% | 1% | 1% | 2% | 3% | 5% | 8% | 13% | 21% | 34% | ( vl )</code></pre>

You can paste that in the “Custom” form, or, if you look at the presets in the “Saved” tab, you’ll see that it’s one of the defaults.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4bbb44a-fd8b-40d6-b00f-fc0396b93ea8/custom-form-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45cda73c-039c-4774-83a1-dbe3286b8887/custom-form-preview-opt.png" alt="Image of an Illustrator document with guides aligned according to the Fibonacci sequence" width="500" height="391" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4bbb44a-fd8b-40d6-b00f-fc0396b93ea8/custom-form-large-opt.png">View large version</a>)</figcaption></figure>

## Getting Excited?

I hope you’ve found this GuideGuide <em>guide</em> guide helpful. As I mentioned at the beginning of this post, you can <a href="https://guideguide-downloads.s3.amazonaws.com/guideguide-trial-smashing-magazine.zip">download a special Smashing Magazine edition of the GuideGuide trial</a>, which lasts three times longer than the standard trial.

{{< signature "il, al" >}}

