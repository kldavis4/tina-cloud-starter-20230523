---
title: 'Hands On The Sigmund Freud Typeface: Making A Font For Your Shrink'
slug: hands-on-sigmund-freud-typeface-making-fonts
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d3d4b2-9965-4004-a133-7fe28d505a82/5-brief-english-deutsch-large-opt.jpg
date: 2014-06-02T23:18:52.000Z
author: harald-geisler
summary: >-
  Handwritten text shows a personal side of its author, a side that is not easy to put into words and that contrasts with the standardized look of digital communication. This contrast and “aura” is perhaps what makes handwriting fonts so popular.
description: >-
  Handwritten text shows a personal side of its author, a side that is not easy to put into words and that contrasts with the standardized look of digital communication. This contrast and “aura” is perhaps what makes handwriting fonts so popular.
categories:
  - Inspiration
  - Typography
  - Fonts
---
Over the past four years, I’ve completed three typefaces inspired by handwriting. I started with the digitization of Albert Einstein’s handwriting and continued with <a href="https://haraldgeisler.com/conspired-lovers/">Conspired Lovers</a>, a font based on my own love-letter writing. In 2013, I ran a <a href="https://www.kickstarter.com/projects/201030759/sigmund-freud-typeface-a-letter-to-your-shrink">Kickstarter campaign</a> to fund the creation of a font based on Sigmund Freud’s handwriting. The public interest in the project was overwhelming, and the Sigmund Freud typeface became the first typeface to be <a href="https://blogs.wsj.com/speakeasy/2013/11/25/typographer-turns-freud-into-a-font/">reviewed in the Wall Street Journal</a>:

<blockquote>For those who regret what keyboards and touch screens have done to their penmanship, typographer Harald Geisler has an answer:</blockquote>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb5ffb5c-9848-4376-aa75-c42ec4b2b76d/1-sigmund-freud-signatur.gif" alt="" width="500" />

As a typographer, I love handwriting, and in this article I’d like to share a hands-on overview of my creation process of creating a handwriting font inspired by the Sigmund Freud typeface, assuming that you’re familiar with illustration software or font-creation software or both.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Reviving A Historic Typeface](https://www.smashingmagazine.com/2012/08/legitima-experience-fossils-revivals/)
*   [Hands-On Experience: The Rehabilitation Of The Script](https://www.smashingmagazine.com/2012/07/hands-on-experience-the-rehabilitation-of-the-script/)
*   [Beautiful Handwriting, Lettering And Calligraphy](https://www.smashingmagazine.com/2008/04/beautiful-handwriting-lettering-and-calligraphy/)
*   [Weird And Wonderful Typography – Yet Still Illegible](https://www.smashingmagazine.com/2012/03/weird-and-wonderful-yet-still-illegible/)

{{% feature-panel %}}

### Freudian Zombies

I am aware that the prospect of creating a typeface based on Einstein or Freud’s handwriting introduces a lot of questions — specifically, issues of authorship and authority, originality, copyright, personality and identity. I never thought I’d find myself in an <a href="https://www.kickstarter.com/projects/201030759/sigmund-freud-typeface-a-letter-to-your-shrink/posts/465419">archive</a> in Vienna, wearing white gloves, confronted by the relics of a great thinker.

To me, “relic” was a religious term. Suddenly, the idea of resurrecting Freud’s handwriting raised questions about the <a href="https://en.wikipedia.org/wiki/Death_of_the_Author">death of the author</a>, and the religious dimension came in through the back door. Would this font be a Freudian <a href="https://en.wikipedia.org/wiki/Philosophical_zombie">zombie</a> or <a href="https://en.wikipedia.org/wiki/Vampire#Psychodynamic_understanding">vampire</a>? Despite these interesting questions, I am going to focus on technical and aesthetic aspects in this article, but if you have a thought to share, I would love to hear it in the comments.

Now, <a href="https://www.youtube.com/watch?v=FtgWu5ysh-Y">let’s get typographical</a>.</p>

## How Can A Font Look Like Handwriting?

Fonts are very different from handwriting. One letter connects to the next in handwriting, but not in a regular typeface. When I type the word “look” in a regular font, the two “o”s look the same. Handwriting has a vivid character because you never write the same letter twice.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b1ae37b-7452-4c7e-892d-56ee3a6e4ad0/look-look.gif" alt="Typing and writing look." width="500" />

In a handwriting font, the letters do two things:

1.  connect organically;
2.  vary so that the same two “o”s never appear next to each other.

A font can be programmed to render alternates during writing. Two different "o"s have to be drawn and stored in the font’s memory. In the next step, the font is programmed to replace the second "o" with the alternate "o". I will focus on creating digital drawings of connecting letters and how to turn them into a font, rather than the creative possibilities of OpenType programming. At the end of this article, I will briefly introduce my thoughts on manipulating the appearance of type through code.

I’ll be working with Adobe Illustrator and FontLab, but the principles apply to any vector-drawing or font-creation software. You’ll find a list of such software at the end of this article.

Now, before we start working with famous people...

*   **Legal issues, personal rights, licensing and clearance**.  Whether a person is living or dead, famous or not, their name and handwriting are protected. If you plan to reference another person’s hand in your design, make sure to clear the rights beforehand. Before working with Sigmund Freud’s letters, I contacted the Freud Museum in London and the Sigmund Freud Museum in Vienna, asking for written permission to create an artistic yet commercial product based on Freud’s writing. The easiest way to avoid problems is to start with your own handwriting: You already own the copyright.
*   **Where to find manuscripts?** Most online archives offer only transcripts of written letters, focusing on the content rather than form. A good place to start is the [Psychoanalytic Document Database](https://www.padd.at/items/7317?locale=en "Psychoanalytical Document Data Base"). Some handwritten letters are available on it as high-resolution PDFs. The [Einstein Archives Online](https://alberteinstein.info/manuscripts.html "Einstein Archive") offers scans of all documents, but not for downloading. [Vincent van Gogh: The Letters](https://vangoghletters.org/vg/letters/let083/letter.html "Van Gogh Archive") offers transcripts and even translations of all letters. If you know of other good archives, please link to them in the comments.</p>

## 1\. Inspecting The Letters

### 1.1\. Collecting

I went through hundreds of Freud’s letters and intuitively compiled the documents in a way that appeals to me. You could organize it according to the quality of the handwriting, as well as distinctive qualities, such as a special uppercase letter or number.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b4a94ed-f29e-4d18-b3dd-4b8385ee3c6e/1-freud-work-situation-large-opt.jpg"><img title="Inspecting the letters in the Sigmund Freud Museum." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bd0399-bc14-47b5-8eed-48a630dd2a60/1-freud-work-situation-opt.jpg" alt="Inspecting the letters in the Sigmund Freud Museum." width="500" height="375" /></a><br>
<em>Inspecting the letters in the Sigmund Freud Museum. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b4a94ed-f29e-4d18-b3dd-4b8385ee3c6e/1-freud-work-situation-large-opt.jpg">Large preview</a>)</em>

### 1.2\. Copy

<blockquote>"Copy, copy, copy, copy what you love. And at the end of copying, you will find yourself."

<em>– <a title="Yohji Yamamoto in conversation with Prof Frances Corner, OBE" href="https://youtube.com/watch?v=SyCdbBiiKyE">Yōji Yamamoto</a></em></blockquote>

One technique to become familiar with the hand of a writer is to copy characteristic letters, letter combinations and words. Learning the movement that a writer made to create a letter is essential to creating its digital counterpart. I keep these exercises in a little notebook. The sketches do not go into the final design but are an important step in understanding the script.

<img title="My notebook with studies of Freud’s handwriting." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3422c04e-d732-4690-bd36-d58471e82689/freud-6-sketchbook1.gif" alt="My notebook with studies of Freud’s handwriting." width="500" height="591" /><br>
<em>My notebook with studies of Freud’s handwriting.</em>

Don’t be surprised if studying how another writer makes the bow of an "l" or the slope of a "g" also affects your own handwriting. Suddenly, I found myself writing my grocery lists with Freudian loops and hoops.

A cinematic example of this process of copying movement or, as Criterion calls it, "Identity Theft" can be found in René Clément’s "Purple Noon", starring Alain Delon (<em>Note: four minutes of film, without one spoken word</em>).</p>

### 1.3\. Select

From the collection, I chose eight sample letters as a starting point for the typeface. The specimens were representative of different time periods, ranging from the 1880s to the late 1930s, and different purposes, ranging from scientific reports to personal letters and notes. This variety gave me an overview of how Freud’s writing changed over the years and according to formal and informal occasions.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2846eb9-5b96-40b4-ae58-55235c0855ea/2-overview-of-all-documents-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1394762-0aa7-4306-88d7-2920f9056ec5/2-overview-of-all-documents-opt.jpg" width="500" height="428" /></a><br>
<em>Eight specimen spanning from 1883 to 1937. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2846eb9-5b96-40b4-ae58-55235c0855ea/2-overview-of-all-documents-large-opt.jpg">Large preview</a>)</em>

### 1.4\. Focus

The next step was to look further for details and find documents to focus on. I marked exceptional letters on prints of the manuscripts, which I kept in a binder.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/012ccca5-2c42-41ae-896f-4c6c0b641a02/3-letters-prints-manuscripts-opt.jpg" alt="Binder with Manuscripts" width="500" height="289" />

To keep track of the markings, I noted the particular letter and its file name and page number in another notebook.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8d5d11f-df9a-43df-827b-08602ca62f57/4-markings-letters-opt.jpg" alt="Workbook" width="500" height="367" />

I ended up with two documents to focus on: a letter from Freud to his grandson in 1925, and a letter from 1919 containing English and German text.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca8e2316-f13e-446f-b1c7-aefe089469d6/freud-7-selected-letters-20-85-1.gif"><img title="The letter to his grandson was full of beautiful letterforms." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca8e2316-f13e-446f-b1c7-aefe089469d6/freud-7-selected-letters-20-85-1.gif" alt="The letter to his grandson was full of beautiful letterforms." width="800" height="1028" /></a><br>
<em>The letter to his grandson was full of beautiful letterforms.</em>

The combination of German and English is important because until the late 1950s, the custom throughout German-speaking countries was to practice a German script called <a title="Wikipedia Article on Kurrent." href="https://en.wikipedia.org/wiki/Kurrent">Kurrent</a>. This form of handwriting was used only to write German; every other language (such as Latin, English and French) was written in a cursive still readable today. This passage was an important reference because I wanted to create a typeface that is true to the original but also readable today.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d3d4b2-9965-4004-a133-7fe28d505a82/5-brief-english-deutsch-large-opt.jpg"><img title="An excerpt from Freud’s letter of 1919, mixing German and English, reading: If I court more woman, you will couch with more men." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01fa3330-e790-4e9e-9bae-4c9e25fc6d10/5-brief-english-deutsch-opt.jpg" alt="An excerpt from Freud’s letter of 1919, mixing German and English, reading: If I court more woman, you will couch with more men." width="500" height="173" /></a><br>
<em>An excerpt from Freud’s letter of 1919, mixing German and English, reading “If I court more woman, you will couch with more men.” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d3d4b2-9965-4004-a133-7fe28d505a82/5-brief-english-deutsch-large-opt.jpg">Large preview</a>)</em>

## 2\. The ABCs, Letter By Letter

<strong>Size matters.</strong> Digital type scales to any size, whereas handwriting exists only at a particular size. The size of one’s handwriting varies little from day to day and depends on the tool and surface being used. This is key to the digitalization process. If you are gathering scans and images, matching all DPI settings to the dimensions of the original scanned document is critical. So, an image file that is 1000 × 1000 pixels, scanned from a piece of paper that is 1 × 1 inch, should be set to 1000 DPI.</p>

### 2.1\. Preparing Illustrator

Before importing the material, we have to set up the Illustrator file. We’ll create a PostScript font, which stores letters (i.e. glyphs) on a 1000 × 1000 grid. Later we will copy the drawings to this format. To make the conversion accurate, select <code>Illustrator → Preferences → Units</code>, and set the file-size unit from millimeters or inches to points. Double-click the Artboard tool, and set the canvas’ size to 1000 × 1000 points.

#### 2.1.1 Layers

We’ll work with four layers:

1.  **Guides** A layer to place guides that mark, for example, the baseline on which all letters will sit, the height at which letters connect, etc.
2.  **Angle** A layer with mobile guides regarding the angles used in handwriting
3.  **Drawing** Where the drawing happens
4.  **Template** A layer to place our handwritten originals

<img title="Our Layers panel in Illustrator." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0716f1-ac10-45ff-a1c3-57812b3c5ddd/6-layers-panel-illustrator-opt.png" alt="Our Layers panel in Illustrator." width="252" height="202" /><br>
<em>Our Layers panel in Illustrator.</em>

### 2.2\. Adjust the Templates

I’ll place the scanned documents on the template layer. Scale the letter that you’re working with (“e” in the screenshot below ) until the glyph comfortably fills the workspace.

Keep in mind that some letters, including “g,” “p” and “j,” have long ascenders and that some uppercase letters have wide swashes. Leave some extra room for them.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b0caa57-e884-4c8b-ab52-2642089be13b/7-positioning-template-large-opt.jpg"><img title="Positioning the template in Illustrator." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af20f307-c72f-4f16-809f-3bfc146de2dc/7-positioning-template-opt.jpg" alt="Positioning the template in Illustrator." width="500" /></a><br>
<em>Positioning the template in Illustrator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b0caa57-e884-4c8b-ab52-2642089be13b/7-positioning-template-large-opt.jpg">Large preview</a>)</em>

<strong>Tip</strong> (optional): If you’re working with more than one template, instead of individually scaling each template, just adjust the DPI of the template itself.

Now that we’ve positioned and sized the template, copy the size of the scaled document (in this case, we’ve scaled the envelop to 7647,938 points wide). Open the document in Photoshop. Select the menu item <code>Image → Image Size</code>. Adjust the picture’s width to 7647,938 points, and uncheck “Resample Image.” This way, the document’s DPI value will be adjusted accordingly — in this case, to about 19 DPI.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a69129e6-44b8-406b-a882-15dc9ffc41a0/8-adjusting-dpi-photoshop-large-opt.jpg"><img title="Adjusting the DPI in Photoshop." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5ad9397-55bd-4228-890a-72b9e161bcec/8-adjusting-dpi-photoshop-opt.jpg" alt="Adjusting the DPI in Photoshop." width="500" height="403" /></a><br>
<em>Adjusting the DPI in Photoshop. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a69129e6-44b8-406b-a882-15dc9ffc41a0/8-adjusting-dpi-photoshop-large-opt.jpg">Large preview</a>)</em>

Adjust all of your templates so that all of your documents will appear in the correct size as you place them on the template layer. (If your templates were scanned with varying DPI values, insert some math here.)

### 2.3\. Guides

I work with three guides: the baseline, the x-height guide and the connecting-height guide.

The letter sits on the baseline. It’s like the line that one writes on in a notebook. The x-height marks the average height of lowercase letters. The connecting height marks the height at which the letters connect.

<img title="The guides in the Illustrator template." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a81b42d7-221f-4065-bddb-050547024298/9-x-height-opt.jpg" alt="The guides in the Illustrator template." width="500" height="357" /><br>
<em>The guides in the Illustrator template.</em>

### 2.4\. Finding the Right Angle

Every writer has their own angle at which one letter connects to the next. Not all letters connect at the same angle, but you will find that an average exists. Compare a few words and find that sweet spot that matches most letters. The guides in the angle layer represent the average angle at which most letters connect. Not all letters will have the same width, so move these left and right to match the width of each letter.

<img title="Placing the guides on the angle layer." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9162cbfe-3e5b-427a-88d3-8e9cb3f5294f/2.41" alt="Placing the guides on the angle layer." width="500" height="410" /><br>
<em>Placing the guides on the angle layer.</em>

### 2.5\. Finally, Drawing

Lock the template, guides and angle layers, and activate the drawing layer. Select the Brush tool and reset all settings (i.e. 1-point width, no shape, etc.). Because I had practiced the movements and rhythm in my notebook, the forms of the letters are familiar to me. Now, let’s draw.

I am fascinated by how good people can draw with a mouse. I can only draw with a pen, which is why I recommend using a graphic tablet for digitizing.

<img title="Drawing letters on a graphics tablet with a screen." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca62b340-9b46-478e-a8f4-08ab637ac351/2.5" alt="Drawing letters on a graphics tablet with a screen." width="500" height="281" /><br>
<em>Drawing letters on a graphics tablet with a screen.</em>

The position of the line should be centered to the letterform and should represent the movement of the pen, not the outline of the letterform.

<img title="With the Direct Selection tool, adjust the position and Bézier handles of each point until you are satisfied." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2339e84-3a15-4dea-803e-d0c365351814/2.5" alt="With the Direct Selection tool, adjust the position and Bézier handles of each point until you are satisfied." width="483" height="533" /><br>
<em>With the Direct Selection tool, adjust the position and Bézier handles of each point until you are satisfied.</em>

### 2.6\. Max Width and Min Width

Before using the Width tool to expand the stroke, we have to determine three width values:

*   maximum width,
*   minimal width,
*   connection-point width (i.e. the part where the letters join).

The handwriting in our example was written with a fountain pen. A traditional nib makes thick strokes when moved downward with pressure and thin lines when moved upwards without pressure. I look for downstrokes to determine the maximum thickness. The minimum width can be found by looking at upstrokes.

<img title="In this example, the minimal and connecting width is 18 points, and the maximal width is 39 points." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7446a5b-a055-4299-a935-460be10f5a53/2.6" alt="In this example, the minimal and connecting width is 18 points, and the maximal width is 39 points." width="483" height="533" /><br>
<em>In this example, the minimal and connecting width is 18 points, and the maximal width is 39 points.</em>

### 2.7\. Forming the Line

Select the line and adjust the stroke’s width to the minimal width, also setting the stroke cap to “round” and the corner to “round join.”

<img title="Adjusting the stroke’s width." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23f9210d-c8fa-479a-bc77-66a07bdacac7/10-adjusting-stroke-width-opt.jpg" alt="Adjusting the stroke’s width." width="252" height="223" /><br>
<em>Adjusting the stroke’s width.</em>

Using the Width tool, expand the line to the desired form.

<strong>Tip:</strong> Reducing opacity makes it easier to adjust the stroke’s width to the template.

<img title="Working with the Width tool." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce11937f-3524-4d5d-90c0-82a400748489/2.7" alt="Working with the Width tool." width="483" height="533" /><br>
<em>Working with the Width tool.</em>

Double-click a width’s point to adjust its values precisely.

<img title="The dialog to edit a width’s point." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb997739-2b9e-4532-9a67-88d4e0ad3b8b/11-dialog-width-point-opt.jpg" alt="The dialog to edit a width’s point." width="440" height="384" /><br>
<em>The dialog to edit a width’s point.</em>

The writing in different documents will sometimes appear thicker or thinner than the defined range of the maximal and minimal width. Keep calm and carry on: Stick to the defined values. The width is not entirely controlled by the writer, but also depends on the nib, the ink’s flow and the paper. But a writer can't deviate from his unique movement patterns.

Even if the forms of individual letters look whimsical, they have been whimsically formed by that particular writer. Capturing this originality, rather than the “scanned” form, is important.</p>

### 2.8\. Setting up FontLab

Create a new project in FontLab. At the bottom of the font window, select a code page: <code>Type 1 Basic → ISO 8859 - 1 Latin 1 (Western)</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79256ce0-7853-42ba-876d-1ce4a9653563/12-dont-window-fontlab-large-opt.jpg"><img title="The font window in FontLab." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33f2f5ae-aacb-443d-a642-9de3cebc8d4b/12-dont-window-fontlab-opt.jpg" alt="The font window in FontLab." width="500" height="940" /></a><br>
<em>The font window in FontLab. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79256ce0-7853-42ba-876d-1ce4a9653563/12-dont-window-fontlab-large-opt.jpg">Large preview</a>)</em>

Double-click the prepared letter to create the glyph. Double-click again to open the glyph window.

<img title="The glyph window in FontLab." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ebbb76f-a2b0-421d-abbb-24d47c8016e1/13-glyph-window-fontlab-opt.jpg" alt="The glyph window in FontLab." width="496" height="607" /><br>
<em>The glyph window in FontLab.</em>

### 2.9\. Copy and Paste

Let’s go back to Illustrator and prepare the drawing that will be used as a Glyph.

Here is the conventional way:

1.  Duplicate the object that you have just created.
2.  Select the path, and execute `Object → Expand Appearance`.
3.  Open `Window → Pathfinder`, and click “Unite.” ![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0af79f5e-c01e-4aec-ad3e-3e6414bc14fb/2.9)
4.  Cut the expanded drawing to the clipboard.
5.  Switch to FontLab, and paste in the drawing.

And the unconventional way:

1.  Copy the drawing to the clipboard.
2.  Switch to FontLab and paste in the drawing.
3.  In FontLab, select `Contour → Transform → Merge Contours`.

Surprisingly, the unconventional way can lead to a better rendering in FontLab. Why? Illustrator works with decimal coordinates (like <code>x=111,95438 y=-90,451</code>), whereas FontLab only supports integer coordinates. The coordinates we’ve copied would convert to <code>x=112 y=-90</code>.

Copying and pasting is never just copying and pasting — it is an interpretation. Drawings that look smooth in Illustrator can end up looking bumpy. Copying the line with the width data probably triggers a different algorithm in FontLab, leading to a better result. In case you run into trouble here, you now have an idea of where it might come from.</p>

### 2.10\. Bringing It Together

Making a joined script has a huge advantage over making disconnected fonts: no <a title="Wikipedia on kerning." href="https://en.wikipedia.org/wiki/Kerning">kerning</a>. Kerning is the art of adjusting the space between all possible letter combinations. The drawback of a joined script, however, is that all letters have to join.

When you write with your hand, the letters will naturally join. In the following steps, we’ll prepare the form to connect seamlessly with all letters.

After pasting the letter, place it on the solid baseline (y=0):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de97497a-1e56-4e61-963b-e883269a6b0b/2.10" alt="Placing the letter on the baseline." width="520" height="628" />

Pull a horizontal guide out of the rulers at the height where the glyphs connect. Right-click on the guide and select “Convert to Global.” The guide will turn from blue to red and will now be fixed in all future glyph windows.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f439c1e8-378b-4880-8cca-8cb5f93c6b18/2.10" alt="Setting a global guide line." width="499" height="632" />

The next step has to do with overlapping. Move the letter a bit beyond the dashed line on the left. The dashed line marks the left <code>0</code> position of the glyph. Placing the letter beyond that line ensures that other letters will join seamlessly from the left. Now, let’s pull the dashed line on the right over the letter a bit to make the joints seamless on the right.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60eb3443-c651-419e-9dcd-1590cd715200/2.10" alt="Adjusting the Overlapping." width="635" height="509" />

### 2.11\. Our First Letter Is Ready. Let’s Make It a Font!

Before simply exporting the font, we have to fill out some lengthy and technical forms, which is a good time to introduce you to FontLab’s Diamonds. Open the the Font Info dialog at <code>File → Font Info</code>.

All of the important information regarding the font is shown in this window. In the first dialog, enter a name and click the green diamond; magically, all mandatory fields will be filled in with the necessary information. Head to the next page by clicking the right arrow. Again, click the diamond and continue until you reach the first page again. Only press the diamonds; never enter any information that you do not understand. You will find extensive information about all of these details in the <em>User’s Manual</em> (ZIP’ed PDF).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9434da-c7d6-4370-97a8-c64f889cc2e8/2.11" alt="Font Info Dialog." width="925" height="592" />

After you are done with the Font Info dialog, close it with “OK.”

To export the font, select <code>File → Generate Font</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d4cbac4-da81-4a91-8886-c97bd015e828/14-exporting-font-large-opt.jpg"><img title="Generate Font Dialog." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc328a6a-edf3-48db-bda4-d61ed85c60b5/14-exporting-font-opt.jpg" alt="Generate Font Dialog." width="500" height="413" /></a>

Win TrueType/OpenType TT is the preselected output format. For now, I recommend using this format because it is easier to handle and outputs fewer errors.

Congrats! Here it is, your font! Double-click to install.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3532da8-ca27-4baa-a1cc-9fe9d36e7e05/15-exporting-font-large-opt.jpg"><img title="Font file in Mac OS X." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c3ef0b-eb96-4a25-8ddf-406643750c74/15-exporting-font-opt.jpg" alt="Font file in Mac OS X." width="500" height="527" /></a>

After installing the font, you can select it under the given name in your font menu. For example, in TextEdit:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7289d6b0-8be1-46c9-89ba-1cc10157e5c1/2.11" alt="For example here in TextEdit." width="500" height="391" />

Now, continue to draw all letters from a to z and A to Z, as well as punctuation, numbers, diacritics, dingbats, etc. You’re halfway there.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe13c25f-fad4-4ae5-b487-5ce23f07def7/16-overview-glyphs-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f240f3a-4676-49cc-b3e2-98ee0ec3ecc7/16-overview-glyphs-opt.jpg" alt="Overview of all 1467 Glyphs of the Sigmund Freud Typeface Pro." width="1987" height="1148" /></a><br>
<em>Overview of all 1467 glyphs in the Sigmund Freud Pro typeface. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe13c25f-fad4-4ae5-b487-5ce23f07def7/16-overview-glyphs-large-opt.jpg">Large preview</a>)</em>

### 2.12 What Is Freud’s Take on the @ Sign?

By now, you are probably asking yourself how to deal with missing glyphs. Freud probably never drew an “@” sign in his life or the letter combination “www.”

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22460e56-6724-45bd-ac9c-aaf2b4b4a037/2.12" alt="" width="500" height="148" />

In the beginning of this article, I emphasized the <em>movement</em> of creating a letter, rather than the form of a letter. Once I get a feel for the way a writer moves to write a loop or a hoop, I can improvise with that knowledge. You, the artist, have to fill in the gaps by improvising based on what you’ve learned.

To dance means to move to a model in your head — is a possible <a title="Funkkolleg Musik - Sinfonie des Lebens #4 - Haben nur Menschen Musik? Musik und Evolution." href="https://mp3.podcast.hr-online.de/mp3/podcast/hr2_funkkolleg_musik/hr2_funkkolleg_musik_20111118.mp3">conclusion (MP3 in German)</a> to the research of Neuroscientists studies about <a title="Studying synchronization to a musical beat in nonhuman animals" href="https://birdloversonly.org/wp-content/uploads/2012/07/Patel_Iversen_Bregman_Schulz_NYAS_in_press.pdf">beat perception and synchronization</a>. They’ve also found that only humans, a <a title="Snowball Dancing " href="https://www.youtube.com/watch?v=N7IZmRnAo6s">few</a> <a title="PDF " href="https://www.birdloversonly.org/docs/Patel.pdf">birds</a>, whales and probably <a href="https://www.economist.com/node/13570066">elephants</a> are able to move to a model in their heads. (Sorry, <a title="Breakdancing Gorilla at the Calgary Zoo Explained" href="https://youtube.com/watch?v=yLHmt3YFuXQ">apes</a> are playful but do not dance.) This act of moving to a model in one’s head is an interpretation. The more intensely one studies and internalizes the movements that a writer made to draw letters in their manuscripts, the more profound this interpretation will be.</p>

### 2.13 Tip for InDesign Users: Rapid Testing

Depending on the complexity of your typeface, you will export the font hundreds or thousands of times to test it outside of your development environment. If you are an InDesign user, here’s a tip on how to speed up testing.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79975e59-1b20-42b7-ba28-ab83d52a106c/2.13" alt="" width="500" height="284" />

In the “Export” dialog, navigate to the InDesign application folder. There you will find a folder named <code>Fonts</code>. Export into this folder, and Indesign will instantly make the font available to you. As soon as you overwrite the font file with a new version, InDesign will update all open documents, and you can observe the change immediately on screen. This only works in InDesign.</p>

### 2.14 What Is The Right Size For A Handwriting Font?

Looking at your own handwriting, you will find that it is always about the same size. Digital type, however, can be reproduced at any size, from fine print to a billboard lettering.

If it’s a print project and you’d like to give the rendered text a natural look, I would suggest finding the size of the original handwriting. And how does one find this original size?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc31c567-8d9a-4559-8dab-d8449fe1bfc3/2.14" alt="" width="500" height="516" />

Open a new document in Illustrator (letter or A4 size), and place a template with the original DPI setting in the background. Input the opening lines of text in the newly created typeface on top of the template. Modify the size until the text aligns with the template.

The size of written text will vary from sample to sample, and the size of a digital handwriting font is a range, rather than fixed. The size that renders Sigmund Freud’s handwriting correctly is between 18 and 24 points. The same rules apply to line-height settings.</p>

## Conclusion

I hope you’ve found this to be a helpful introduction to creating handwriting fonts. Creating a typeface in a day is possible, but usually it takes months or even years to finish all of the glyphs and for testing and production. When one writes by hand, every letter is a little different. At the beginning of this article, I mentioned the possibility of altering the appearance of type through code. In my opinion, this is a necessity for contemporary handwriting fonts.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c21a044-049c-4f93-b4c0-5366fb33d03c/3.contemporary" alt="" width="500" height="92" />

A font can be programmed to render alternates during writing. Two different “o”s have to be drawn and stored in the font’s memory. Then, you would program the font to replace a second “o” with the alternate “o.”

With the Kickstarter funding, I was able to make the Sigmund Freud typeface the first handwriting font that holds four separate lowercase alphabets, and programmed the font to continuously alternate between the four glyphs. With every key pushed by the writer, the sequence of letters will alter to create a unique look.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82441278-51e2-4652-b13f-ac477ea0fcf3/freud-pro-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82441278-51e2-4652-b13f-ac477ea0fcf3/freud-pro-animation.gif" alt="Sigmund Freud Typeface Overview." width="500" /></a><br>
<em>Overview of the Sigmund Freud typeface.</em>

I refer to this alternating mechanism as polyalphabetic substitution — “polyalphabetic” because it includes multiple alphabets, and “substitution” because the letters are being replaced.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72366f33-f37d-44f2-a93a-e4191bb7cae9/17-polyalphabetic-substitution-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc4ae126-7126-4f7c-969d-7bfcffadec04/17-polyalphabetic-substitution-opt.jpg" width="500" /></a>

If you are familiar with encryption, you might think of a <a href="https://en.wikipedia.org/wiki/Polyalphabetic_cipher">polyalphabetic cipher</a>. Indeed, what happens in the font is inspired by the encryption of the Enigma machine, which used a combination of rotating barrels to encrypt a message.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa2b587-d44e-473c-998a-fe25476bfb0a/18-enigma-machine-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccb388ca-2dfb-4423-adca-20a9cb45a0c3/18-enigma-machine-opt.jpg" width="500" /></a>

My intention is not to encode the message, but to hide its computerized origin. Of course, this hiding does not make the rendered result more human; it is an obvious matter of hide and seek.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14394e34-0d53-4074-8bb1-b4dc52ac0875/3.you-will-couch2" alt="Original and digital." width="500" height="117" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3799fe7e-6972-4b21-bff7-c55c9505a16c/3.you-will-couch21" alt="" width="500" height="253" /><br>
<em>Original and digital side by side.</em>

The loss of the art of handwriting is an ongoing discussion among typographers and enthusiasts of the written word, a discussion that could easily be mistaken as an attack on increasingly inhuman technology. Fonts cannot make up for the cultural value of handwriting, but I do hope that this project enriches written communication and shifts the focus of typography-related discussions from loss to the creative possibilities of new technology.

In the beginning, I quoted Japanese fashion designer Yōji Yamamoto. Fashion and typography are an interesting pair. One can look at words as if they wear a typeface, just like humans wear clothes. The word is not the typeface, and we are not the clothes we wear. Type designers are often confronted by the question, “Don’t we already have…

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2b254cd-d4be-43cf-ad0d-b8171800c087/3.enough-typeface" alt="" width="500" height="113" />

Looking at the <a href="https://youtube.com/watch?v=YLDUXZ4X5b8">2014-2015 fashion runway</a>, staged between supermarket shelves (great music, by the way — I hope they use that soundtrack in my supermarket soon), the obvious question springs to mind, “Don’t we already have <a href="https://www.youtube.com/watch?v=atmkF7CVTTg">enough</a> <a href="https://youtube.com/watch?v=oimQuCk1J10">clothes</a>?”

The clothes we wear and the type we use do not have to express personality, but rather indicate our circumstances. We can have a wide or narrow range of brands to choose from. Some people know how to fabricate their own clothes. Fabric is, by definition, material. Writing, meanwhile, has been digitized to a great extent. My own written communication is almost completely digital.</p>

### The Future of Writing: A Lifetime In Fonts

This digitized circumstance can be an opportunity and a space for <a href="https://publicdomainreview.org/collections/fashions-of-the-future-as-imagined-in-1893/">future</a> cultural development. When I think of the future of written communication, it would be wonderful if everybody had his own font and could continually refine the appearance of his/her own digital personal typeface. In elementary school children would learn how to draw their own typeface, and over years one builds, develops, adapts and extends the design to ones needs and...

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a71c1712-fce6-4bad-9d48-edad19f471f6/3.personality-anime4" alt="" width="350" height="132" />

If we think of a typeface being continually refined and designed over a lifetime, would this make up for the cultural value of handwriting? I would love to hear your thoughts on this.

Let’s go back to Illustrator and prepare the drawing that will be used as a Glyph.

Here is the conventional way:

1.  Duplicate the object that you have just created.
2.  Select the path, and execute `Object → Expand Appearance`.
3.  Open `Window → Pathfinder`, and click “Unite.” ![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0af79f5e-c01e-4aec-ad3e-3e6414bc14fb/2.9)
4.  Cut the expanded drawing to the clipboard.
5.  Switch to FontLab, and paste in the drawing.

And the unconventional way:

1.  Copy the drawing to the clipboard.
2.  Switch to FontLab and paste in the drawing.
3.  In FontLab, select `Contour → Transform → Merge Contours`.

Surprisingly, the unconventional way can lead to a better rendering in FontLab. Why? Illustrator works with decimal coordinates (like <code>x=111,95438 y=-90,451</code>), whereas FontLab only supports integer coordinates. The coordinates we’ve copied would convert to <code>x=112 y=-90</code>.

Copying and pasting is never just copying and pasting — it is an interpretation. Drawings that look smooth in Illustrator can end up looking bumpy. Copying the line with the width data probably triggers a different algorithm in FontLab, leading to a better result. In case you run into trouble here, you now have an idea of where it might come from.</p>

### 2.10\. Bringing It Together

Making a joined script has a huge advantage over making disconnected fonts: no <a title="Wikipedia on kerning." href="https://en.wikipedia.org/wiki/Kerning">kerning</a>. Kerning is the art of adjusting the space between all possible letter combinations. The drawback of a joined script, however, is that all letters have to join.

When you write with your hand, the letters will naturally join. In the following steps, we’ll prepare the form to connect seamlessly with all letters.

After pasting the letter, place it on the solid baseline (y=0):

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de97497a-1e56-4e61-963b-e883269a6b0b/2.10" alt="Placing the letter on the baseline." width="520" height="628" />

Pull a horizontal guide out of the rulers at the height where the glyphs connect. Right-click on the guide and select “Convert to Global.” The guide will turn from blue to red and will now be fixed in all future glyph windows.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f439c1e8-378b-4880-8cca-8cb5f93c6b18/2.10" alt="Setting a global guide line." width="499" height="632" />

The next step has to do with overlapping. Move the letter a bit beyond the dashed line on the left. The dashed line marks the left <code>0</code> position of the glyph. Placing the letter beyond that line ensures that other letters will join seamlessly from the left. Now, let’s pull the dashed line on the right over the letter a bit to make the joints seamless on the right.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60eb3443-c651-419e-9dcd-1590cd715200/2.10" alt="Adjusting the Overlapping." width="635" height="509" />

### 2.11\. Our First Letter Is Ready. Let’s Make It a Font!

Before simply exporting the font, we have to fill out some lengthy and technical forms, which is a good time to introduce you to FontLab’s Diamonds. Open the the Font Info dialog at <code>File → Font Info</code>.

All of the important information regarding the font is shown in this window. In the first dialog, enter a name and click the green diamond; magically, all mandatory fields will be filled in with the necessary information. Head to the next page by clicking the right arrow. Again, click the diamond and continue until you reach the first page again. Only press the diamonds; never enter any information that you do not understand. You will find extensive information about all of these details in the <em>User’s Manual</em> (ZIP’ed PDF).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9434da-c7d6-4370-97a8-c64f889cc2e8/2.11" alt="Font Info Dialog." width="925" height="592" />

After you are done with the Font Info dialog, close it with “OK.”

To export the font, select <code>File → Generate Font</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d4cbac4-da81-4a91-8886-c97bd015e828/14-exporting-font-large-opt.jpg"><img title="Generate Font Dialog." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc328a6a-edf3-48db-bda4-d61ed85c60b5/14-exporting-font-opt.jpg" alt="Generate Font Dialog." width="500" height="413" /></a>

Win TrueType/OpenType TT is the preselected output format. For now, I recommend using this format because it is easier to handle and outputs fewer errors.

Congrats! Here it is, your font! Double-click to install.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3532da8-ca27-4baa-a1cc-9fe9d36e7e05/15-exporting-font-large-opt.jpg"><img title="Font file in Mac OS X." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c3ef0b-eb96-4a25-8ddf-406643750c74/15-exporting-font-opt.jpg" alt="Font file in Mac OS X." width="500" height="527" /></a>

After installing the font, you can select it under the given name in your font menu. For example, in TextEdit:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7289d6b0-8be1-46c9-89ba-1cc10157e5c1/2.11" alt="For example here in TextEdit." width="500" height="391" />

Now, continue to draw all letters from a to z and A to Z, as well as punctuation, numbers, diacritics, dingbats, etc. You’re halfway there.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe13c25f-fad4-4ae5-b487-5ce23f07def7/16-overview-glyphs-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f240f3a-4676-49cc-b3e2-98ee0ec3ecc7/16-overview-glyphs-opt.jpg" alt="Overview of all 1467 Glyphs of the Sigmund Freud Typeface Pro." width="1987" height="1148" /></a><br>
<em>Overview of all 1467 glyphs in the Sigmund Freud Pro typeface. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe13c25f-fad4-4ae5-b487-5ce23f07def7/16-overview-glyphs-large-opt.jpg">Large preview</a>)</em>

### 2.12 What Is Freud’s Take on the @ Sign?

By now, you are probably asking yourself how to deal with missing glyphs. Freud probably never drew an “@” sign in his life or the letter combination “www.”

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22460e56-6724-45bd-ac9c-aaf2b4b4a037/2.12" alt="" width="500" height="148" />

In the beginning of this article, I emphasized the <em>movement</em> of creating a letter, rather than the form of a letter. Once I get a feel for the way a writer moves to write a loop or a hoop, I can improvise with that knowledge. You, the artist, have to fill in the gaps by improvising based on what you’ve learned.

To dance means to move to a model in your head — is a possible <a title="Funkkolleg Musik - Sinfonie des Lebens #4 - Haben nur Menschen Musik? Musik und Evolution." href="https://mp3.podcast.hr-online.de/mp3/podcast/hr2_funkkolleg_musik/hr2_funkkolleg_musik_20111118.mp3">conclusion (MP3 in German)</a> to the research of Neuroscientists studies about <a title="Studying synchronization to a musical beat in nonhuman animals" href="https://birdloversonly.org/wp-content/uploads/2012/07/Patel_Iversen_Bregman_Schulz_NYAS_in_press.pdf">beat perception and synchronization</a>. They’ve also found that only humans, a <a title="Snowball Dancing " href="https://www.youtube.com/watch?v=N7IZmRnAo6s">few</a> <a title="PDF " href="https://www.birdloversonly.org/docs/Patel.pdf">birds</a>, whales and probably <a href="https://www.economist.com/node/13570066">elephants</a> are able to move to a model in their heads. (Sorry, <a title="Breakdancing Gorilla at the Calgary Zoo Explained" href="https://youtube.com/watch?v=yLHmt3YFuXQ">apes</a> are playful but do not dance.) This act of moving to a model in one’s head is an interpretation. The more intensely one studies and internalizes the movements that a writer made to draw letters in their manuscripts, the more profound this interpretation will be.</p>

### 2.13 Tip for InDesign Users: Rapid Testing

Depending on the complexity of your typeface, you will export the font hundreds or thousands of times to test it outside of your development environment. If you are an InDesign user, here’s a tip on how to speed up testing.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79975e59-1b20-42b7-ba28-ab83d52a106c/2.13" alt="" width="500" height="284" />

In the “Export” dialog, navigate to the InDesign application folder. There you will find a folder named <code>Fonts</code>. Export into this folder, and Indesign will instantly make the font available to you. As soon as you overwrite the font file with a new version, InDesign will update all open documents, and you can observe the change immediately on screen. This only works in InDesign.</p>

### 2.14 What Is The Right Size For A Handwriting Font?

Looking at your own handwriting, you will find that it is always about the same size. Digital type, however, can be reproduced at any size, from fine print to a billboard lettering.

If it’s a print project and you’d like to give the rendered text a natural look, I would suggest finding the size of the original handwriting. And how does one find this original size?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc31c567-8d9a-4559-8dab-d8449fe1bfc3/2.14" alt="" width="500" height="516" />

Open a new document in Illustrator (letter or A4 size), and place a template with the original DPI setting in the background. Input the opening lines of text in the newly created typeface on top of the template. Modify the size until the text aligns with the template.

The size of written text will vary from sample to sample, and the size of a digital handwriting font is a range, rather than fixed. The size that renders Sigmund Freud’s handwriting correctly is between 18 and 24 points. The same rules apply to line-height settings.</p>

## Conclusion

I hope you’ve found this to be a helpful introduction to creating handwriting fonts. Creating a typeface in a day is possible, but usually it takes months or even years to finish all of the glyphs and for testing and production. When one writes by hand, every letter is a little different. At the beginning of this article, I mentioned the possibility of altering the appearance of type through code. In my opinion, this is a necessity for contemporary handwriting fonts.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c21a044-049c-4f93-b4c0-5366fb33d03c/3.contemporary" alt="" width="500" height="92" />

A font can be programmed to render alternates during writing. Two different “o”s have to be drawn and stored in the font’s memory. Then, you would program the font to replace a second “o” with the alternate “o.”

With the Kickstarter funding, I was able to make the Sigmund Freud typeface the first handwriting font that holds four separate lowercase alphabets, and programmed the font to continuously alternate between the four glyphs. With every key pushed by the writer, the sequence of letters will alter to create a unique look.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82441278-51e2-4652-b13f-ac477ea0fcf3/freud-pro-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82441278-51e2-4652-b13f-ac477ea0fcf3/freud-pro-animation.gif" alt="Sigmund Freud Typeface Overview." width="500" /></a><br>
<em>Overview of the Sigmund Freud typeface.</em>

I refer to this alternating mechanism as polyalphabetic substitution — “polyalphabetic” because it includes multiple alphabets, and “substitution” because the letters are being replaced.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72366f33-f37d-44f2-a93a-e4191bb7cae9/17-polyalphabetic-substitution-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc4ae126-7126-4f7c-969d-7bfcffadec04/17-polyalphabetic-substitution-opt.jpg" width="500" /></a>

If you are familiar with encryption, you might think of a <a href="https://en.wikipedia.org/wiki/Polyalphabetic_cipher">polyalphabetic cipher</a>. Indeed, what happens in the font is inspired by the encryption of the Enigma machine, which used a combination of rotating barrels to encrypt a message.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa2b587-d44e-473c-998a-fe25476bfb0a/18-enigma-machine-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccb388ca-2dfb-4423-adca-20a9cb45a0c3/18-enigma-machine-opt.jpg" width="500" /></a>

My intention is not to encode the message, but to hide its computerized origin. Of course, this hiding does not make the rendered result more human; it is an obvious matter of hide and seek.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14394e34-0d53-4074-8bb1-b4dc52ac0875/3.you-will-couch2" alt="Original and digital." width="500" height="117" /><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3799fe7e-6972-4b21-bff7-c55c9505a16c/3.you-will-couch21" alt="" width="500" height="253" /><br>
<em>Original and digital side by side.</em>

The loss of the art of handwriting is an ongoing discussion among typographers and enthusiasts of the written word, a discussion that could easily be mistaken as an attack on increasingly inhuman technology. Fonts cannot make up for the cultural value of handwriting, but I do hope that this project enriches written communication and shifts the focus of typography-related discussions from loss to the creative possibilities of new technology.

In the beginning, I quoted Japanese fashion designer Yōji Yamamoto. Fashion and typography are an interesting pair. One can look at words as if they wear a typeface, just like humans wear clothes. The word is not the typeface, and we are not the clothes we wear. Type designers are often confronted by the question, “Don’t we already have…

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2b254cd-d4be-43cf-ad0d-b8171800c087/3.enough-typeface" alt="" width="500" height="113" />

Looking at the <a href="https://youtube.com/watch?v=YLDUXZ4X5b8">2014-2015 fashion runway</a>, staged between supermarket shelves (great music, by the way — I hope they use that soundtrack in my supermarket soon), the obvious question springs to mind, “Don’t we already have <a href="https://www.youtube.com/watch?v=atmkF7CVTTg">enough</a> <a href="https://youtube.com/watch?v=oimQuCk1J10">clothes</a>?”

The clothes we wear and the type we use do not have to express personality, but rather indicate our circumstances. We can have a wide or narrow range of brands to choose from. Some people know how to fabricate their own clothes. Fabric is, by definition, material. Writing, meanwhile, has been digitized to a great extent. My own written communication is almost completely digital.</p>

### The Future of Writing: A Lifetime In Fonts

This digitized circumstance can be an opportunity and a space for <a href="https://publicdomainreview.org/collections/fashions-of-the-future-as-imagined-in-1893/">future</a> cultural development. When I think of the future of written communication, it would be wonderful if everybody had his own font and could continually refine the appearance of his/her own digital personal typeface. In elementary school children would learn how to draw their own typeface, and over years one builds, develops, adapts and extends the design to ones needs and...

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a71c1712-fce6-4bad-9d48-edad19f471f6/3.personality-anime4" alt="" width="350" height="132" />

If we think of a typeface being continually refined and designed over a lifetime, would this make up for the cultural value of handwriting? I would love to hear your thoughts on this.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3272f6b1-0f8a-4f18-9d0c-96f506503575/3.sincerely" alt="" width="500" height="189" />

Are you interested in learning more about the creative possibilities of coding fonts, ligatures, contextual alternates, polyalphabetic glyph substitution or the future of personal fonts? Write a comment below, and let me know what you’re interested in.

<em>You can support the author by getting the Sigmund Freud typeface on <a href="https://haraldgeisler.com/sigmund-freud-typeface">his website</a>. Also, thanks again to the <a href="https://www.freud-museum.at/">Sigmund Freud Museum</a> in Vienna who kindly provided Harald with the digital images of Freud’s manuscripts for this project. — Ed.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5180d627-5fd8-4102-b4cd-e4d61c649182/siogmund-freud-1926-2014.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5180d627-5fd8-4102-b4cd-e4d61c649182/siogmund-freud-1926-2014.gif" alt="Sigmund Freud 1926 - 2014" width="500" /></a>

## Related Resources

### FontLab

<a href="https://www.fontlab.com/font-editor/fontlab-studio/">FontLab Studio</a> is the industry standard for font creation. A free trial is available. Have a look at its <a href="https://www.font.to/downloads/manuals/FLS5MacManual.zip">manual</a> and <a href="https://www.font.to/downloads/documents/FLS5MagTypo14.pdf">introductory article</a>.</p>

### Glyphs

The software most talked about (but only for Mac OS 10.6 to 10.9) is Berlin-based <a href="https://www.glyphsapp.com">Glyphs</a>. A free trial, an extensive manual, <a href="https://www.glyphsapp.com/tutorials">tutorials</a> and a <a href="https://vimeo.com/43552747">video demonstration</a> are available, too. Glyphs has a much more modern look and feel than FontLab. The quick responses to feature requests and regular updates are making more and more designers switch to Glyphs. The app has a presence on <a href="https://twitter.com/glyphsapp">Twitter</a>, too.</p>

### Prototypo

This intriguing <a href="https://www.kickstarter.com/projects/599698621/prototypo-streamlining-font-creation">Kickstarter campaign</a> by <a href="https://twitter.com/_____________y">Yannick Mathey</a> and <a href="https://twitter.com/louis_remi">Louis-Rémi Babé</a> gives us a glimpse of a possible future of tools for designing type. According to the founders:
<blockquote>"Prototypo is an open-source online application that allows to control the design of a complete typeface using sliders, and refine spacing and outlines manually. Hobbyists and professionals alike can use twenty-plus parameters to create a wide range of fonts.

We’re building our own language on top of SVG and JS. The syntax is still in its infancy, but the idea is that a glyph is made from a list of segments and components. Those are made of points whose coordinates are calculated using the parameters manipulated by the users and the drawing of Genèse as a reference. In the future, we might explore alternative ways of drawing glyphs, such as a skeleton based approach."</blockquote>

### FontForge

<a href="https://fontforge.org">FontForge</a> is a free and powerful font editor. Its developers describe it as:
<blockquote>"An outline font editor that lets you create your own postscript, truetype, opentype, cid-keyed, multi-master, cff, svg and bitmap (bdf, FON, NFNT) fonts, or edit existing ones. Also lets you convert one format to another. FontForge has support for many macintosh font formats.

FontForge’s user interface has been localized for: (English), Russian, Japanese, French, Italian, Spanish, Vietnamese, Greek, Simplified &amp; Traditional Chinese, German, Polish, Ukrainian and Catalan."</blockquote>

This software is available only as a <strong>source package</strong>, not a binary package. If you know how to handle that, then try it out (and check out the <a href="https://youtube.com/watch?v=q2mNOTo9lqQ">video tutorial</a>).</p>

### Inkscape

According to <a href="https://youtube.com/watch?v=_KX-e6sijGE">Kay Hall’s video</a>, creating a font with the open-source vector-graphics editor <a href="https://www.inkscape.org/en/">Inkscape</a> is also possible.</p>

### FontArk

An online editor for fonts also exists. <a href="https://fontark.net">FontArk</a> is currently in beta and free to try. Check out the <a href="https://www.youtube.com/watch?v=2X-ofQ8ox4Y">introductory video</a>. It is described as:
<blockquote>"A professional browser-based font editor under development, featuring the most versatile real-time multiple glyph editing system, with the mission of making type design faster and easier than ever. No download, No installation, Any OS."</blockquote>

### iFont

Yes, font-creation software for the iPad exists, too. And yes, I recommend it. <a href="https://2ttf.com">iFont</a> is fun, as the <a href="https://www.youtube.com/watch?v=9a6CNYbdhIM">video demo</a> shows.</p>

### Typophile

Typophile is a good forum for all type-related questions.

{{< signature "al, il" >}}

