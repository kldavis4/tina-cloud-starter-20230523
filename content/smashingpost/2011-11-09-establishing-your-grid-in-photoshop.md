---
title: How To Establish Your Grid In Photoshop
slug: establishing-your-grid-in-photoshop
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecf4eba4-7d5b-4232-b9c6-a03b34224bde/smashing-title-slide1.jpg
date: 2011-11-09T12:49:42.000Z
author: steve-schoeffel
description: >-
  Creating a grid is typically one of the very first things you do when starting a design comp. After all, it provides the basic structure on which the rest of your design will lie. In this article, we’ll provide two different methods for efficiently establishing a grid. These methods enable you to quickly and smartly form a grid so that you can spend more time designing.
categories:
  - Graphics
  - Photoshop
  - Grids
---
## Method 1

The first method uses <a title="GuideGuide" href="https://guideguide.me/">GuideGuide</a> by <a title="Cameron McEfee" href="https://www.cameronmcefee.com/">Cameron McEfee</a> to set up vertical columns. Instructions on installing it can be found on the <a title="GuideGuide" href="https://guideguide.me/documentation/">GuideGuide page</a>. There is also a <a href="https://av.adobe.com/russellbrown/GuideGuide_SM.mov">video tutorial</a> on using it that was put together by Russell Brown at Adobe.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e01596fa-44f2-44b2-afd1-3437da35aa5d/guide-guide.jpg" alt="GuideGuide" />

### Set Up Your Grid in 5 Seconds

1.  Determine the margins, number of columns and gutter widths. Then click “Create Guides.”
2.  If the canvas for your design comp is wide, do the quick math so that the margin lengths allow for the grid to be constrained to your 960 pixels. For example, if the canvas is 1200 pixels wide, then the left and right margins would be 120 pixels each.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8425c739-5b80-4789-a87e-9f8359a5b54b/guideguide-overview-setup.jpg" alt="GuideGuide example" /><br>
<em>An example of 12 columns with 20-pixel gutters and margins set to 120 pixels.</em>

You can also set a baseline grid this way, but you’d end up with a lot of guides. A better option might be the method featured on a <a title="Extensible Baseline Grids" href="https://methodandcraft.com/videos/extensible-baseline-grids/">Method &amp; Craft video</a> by Mike Precious…

### Method & Craft’s Extensible Baseline Grid

Here is a brief summary of the steps for setting up an extensible baseline grid.

1.  Establish the grid’s baseline value, then create your pattern template. The baseline grid is determined by the leading (or line height) of the body text. For example, if the main body copy of your design is set in 13-point Helvetica, with the leading at 18 points, then you would set up an 18-pixel baseline grid.
2.  Create a Photoshop file that is the height of your baseline grid, fill the bottom pixel, and leave the remaining pixels transparent. In this case, the dimensions of your canvas would be 1-pixel wide and 18-pixels tall.
3.  “Select All,” and then save this as a new pattern. You can do this by going to Edit → Define Pattern… ![grid2b](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbdc1425-3e31-418c-a57d-610b932cdd1d/grid2b.png)
4.  Go to Adjustment Layer → Pattern, and select your newly created grid pattern. ![grid3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52d626d4-e7b4-4ba6-87a4-5653d29ecaf2/grid3.png)
5.  Adjust the opacity as desired.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed4c040d-d94c-4091-a92f-9c184892f5b5/method-1.jpg" alt="Method #1" /><br>
<em>An example of method 1 with the columns and baseline grid together.</em>

### Advantages

*   You get an optional baseline grid, which you can use independent of the vertical column grid. A baseline grid can create visual clutter when laid over top a design comp. With this method, it can just be toggled on when needed.
*   If you prefer to use guides for your grid, this is the better solution.
*   You can hide and show the grid through an easy shortcut.</p>

### Drawbacks

*   Using vertical guides to mark other elements in the document can be difficult because you might confuse them with the grid.
*   Compared to method 2, your options for the grid are not as specific or comprehensive (such as setting the height of the horizontal module).
*   Grid lines are determined mathematically and won’t necessarily align with the pixel grid. This means that your guides could in some cases fall unevenly and end up being positioned down the middle of the actual pixels.
*   This method requires two separate processes to create a vertical and baseline grid, compared to just the one method coming up.</p>

## Method 2

<a title="Modular Grid Pattern" href="https://modulargrid.org/">Modular Grid Pattern</a> is an all-in-one grid solution. The tool creates a vertical columnar grid and a baseline grid all as one pattern. There are two ways to go about using Modular Grid Pattern:

<strong>Application Panel</strong>
In addition to Photoshop, this also works with Fireworks, GIMP and Microsoft Expression Design. Please note that you must have the latest software (Adobe CS5 or the equivalent of one of the other applications) and an Internet connection for this panel to work. That being said, if you have already created a pattern and saved it in your library, then you would be able to access it without needing anything else.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a55f975a-ef08-44af-8ed7-07929bdda37f/modular-grid-ps.jpg" alt="Modular Grid Pattern Extension" />

<strong>Web app</strong>
This works in Chrome, Firefox, Safari and Opera. The Web app enables you to create a grid pattern and download it straight from the browser in all formats.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f27f42-32dc-4a84-9748-4df8447da506/modular-grid-web.jpg" alt="Modular Grid Pattern" />

Whichever way you choose, just pick a module width, gutter width and baseline number, and Modular Grid Pattern does the rest. You can also specify a height for the horizontal module.</p>

### Advantages

*   This is a fast way to get it all; an all-in-one layer.
*   You have the option to download a Photoshop pattern file, PNG or transparency mask.
*   You can label the patterns and put them in a folder so that you can come back to the grid with virtually no set-up required at all.
*   Frees your guide to be used for other purposes.
*   You can specify a height for the vertical module to establish an overall vertical rhythm.
*   The grid can be overlaid with varying degrees of opacity, so you can make it less distracting as you are designing.
*   Supports applications other than Photoshop.</p>

### Drawbacks

*   If your canvas is wide, then making the grid a pattern will make it extend across the entire page, which could be annoying and make it harder to see the boundaries of the content. This can be fixed in a couple of ways:
    1.  Apply a layer mask to constrain the grid to just the main content area.
    2.  Draw a rectangle the size of the main content area (for example, 960 × 1200 pixels), and apply the grid as a layer style, with the fill set to 0% in this case.
*   This method forces you to choose a baseline grid, preventing you from just creating vertical columnar modules.
*   It requires you to manually hide and show the grid layer, without the benefit of a keyboard shortcut.</p>

## Concluding Thoughts

We hope these methods will increase your efficiency and precision in establishing a grid. In the end, the way you set up the grid will depend on your workflow. Evaluate your needs, then choose the method best suited to them. Either method requires minimal set-up but can save much time and frustration.</p>

### Additional Resources

*   [Enhancing Grid Design With GuideGuide, A Plugin](https://www.smashingmagazine.com/2016/11/enhancing-grid-design-guideguide-plugin-photoshop-illustrator/)
*   [A Better Way To Design For Retina In Photoshop](https://www.smashingmagazine.com/2015/05/retina-design-in-photoshop/)
*   [Grid-Based Web Design, Simplified](https://www.smashingmagazine.com/2010/04/grid-based-web-design-simplified/)
*   [Useful Photoshop Tools and Techniques For Your Workflow](https://www.smashingmagazine.com/2011/05/useful-photoshop-tools-and-techniques-for-your-workflow/)

{{< signature "al" >}}

