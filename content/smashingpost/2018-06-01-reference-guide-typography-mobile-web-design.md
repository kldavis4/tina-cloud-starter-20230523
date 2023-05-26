---
title: 'A Reference Guide For Typography In Mobile Web Design'
slug: reference-guide-typography-mobile-web-design
author: suzanne-scacca
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbb389c7-4cdb-4859-95b9-e9fca2ffe6f5/roboto.png
date: 2018-06-01T13:17:42+02:00
summary: >-
  In terms of how to handle typography in mobile web design, it appears that simpler and safer works best. In this article, we will break down the elements you need to pay attention to in mobile typography and then visit what the research says about how to handle them. 
description: >-
  In terms of how to handle typography in mobile web design, it appears that simpler and safer works best. In this article, we will break down the elements you need to pay attention to in mobile typography and then visit what the research says about how to handle them. 
categories:
  - Typography
  - Mobile
  - Fonts
  - Responsive Design
---
<p>With mobile taking a front seat in search, it's important that websites are designed in a way that prioritize the best experience possible for their users. While Google has brought attention to elements like <a href="https://www.smashingmagazine.com/2018/04/mobile-pop-up-ads/">pop-ups</a> that might disrupt the mobile experience, what about something as seemingly simple as choice of typography?</p>

<p>The answer to the typography question might seem simple enough: what works on desktop should work on mobile so long as it scales well. Right?</p>

<p>While that would definitely make it a lot easier on web designers, that’s not necessarily the case. The problem in making that statement a decisive one is that there haven’t been a lot of studies done on the subject of mobile typography in recent years. So, what I intend to do today is give a brief summary of what it is we know about typography in web design, and then see what UX experts and tests have been able to reveal about using typography for mobile.</p>

## Understanding The Basics Of Typography In Modern Web Design

<p>Look, I know typography isn’t the most glamorous of subjects. And, being a web designer, it might not be something you spend too much time thinking about, especially if clients bring their own style guides to you prior to beginning a project.</p>

<p>That said, with mobile-first now here, typography requires additional consideration.</p>

{{% feature-panel %}}

### Typography Terminology

<p>Let’s start with the basics: terminology you’ll need to know before digging into mobile typography best practices.</p>

<p><strong>Typography:</strong> This term refers to the <em>technique</em> used in styling, formatting, and arranging “printed” (as opposed to handwritten) text.</p>

<p><strong>Typeface:</strong> This is the classification system used to label a family of characters. So, this would be something like Arial, Times New Roman, Calibri, Comic Sans, etc.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/161dc3ab-6283-4450-a58d-1210b529b360/typeface.png" sizes="100vw" caption="A typical offering of typefaces in word processing applications. (Source: <a href='https://www.google.com/docs/about/'>Google Docs</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/161dc3ab-6283-4450-a58d-1210b529b360/typeface.png'>Large preview</a>)" alt="Typefaces in Office 365" >}}

<p><strong>Font:</strong> This drills down further into a website’s typeface. The font details the typeface family, point size, and any special stylizations applied. For instance, 11-point Arial in bold.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2aa74f-7b8a-4935-a83f-622ef49d1e6a/font.png" sizes="100vw" caption="An example of the three elements that define a font. (Source: <a href='https://www.google.com/docs/about/'>Google Docs</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f2aa74f-7b8a-4935-a83f-622ef49d1e6a/font.png'>Large preview</a>)" alt="3 essential elements to define a font" >}}

<p><strong>Size:</strong> There are two ways in which to refer to the size (or height) of a font: the word processing size in points or the web design size in pixels. For the purposes of talking about mobile web design, we use pixels.</p>

<p>Here is a line-by-line comparison of various font sizes:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb324b3c-d7bb-462b-9dd3-5c7110a9e6c3/font-size.png" sizes="100vw" caption="An example of how the same string of text appears at different sizes. (Source: <a href='https://www.google.com/docs/about/'>Google Docs</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb324b3c-d7bb-462b-9dd3-5c7110a9e6c3/font-size.png'>Large preview</a>)" alt="An example of font sizes" >}}

<p>As you can see in <a href="https://wordpress.org/">WordPress</a>, font sizes are important when it comes to establishing hierarchy in header text:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52aca192-c627-455e-a30a-39912bd4675b/wordpress-sizes.png" sizes="100vw" caption="Header size defaults available with a WordPress theme. (Source: <a href='https://wordpress.org/'>WordPress</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52aca192-c627-455e-a30a-39912bd4675b/wordpress-sizes.png'>Large preview</a>)" alt="An example of font size choices in WordPress" >}}

<p><strong>Weight:</strong> This is the other part of defining a typeface as a font. Weight refers to any special styles applied to the face to make it appear heavier or lighter. In web design, weight comes into play in header fonts that complement the typically weightless body text.</p>

<p>Here is an example of options you could choose from in the <a href="https://wordpress.org/">WordPress</a> theme customizer:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e69e803f-06b0-4972-a821-88809d7f0016/font-weight.png" sizes="100vw" caption="Sample font weights available with a WordPress theme. (Source: <a href='https://wordpress.org/'>WordPress</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e69e803f-06b0-4972-a821-88809d7f0016/font-weight.png'>Large preview</a>)" alt="An example of font weight choices" >}}

<p><strong>Kerning:</strong> This pertains to the space between two letters. It can be adjusted in order to create a more aesthetically pleasing result while also enhancing readability. You will need a design software like Photoshop to make these types of adjustments.</p>

<p><strong>Tracking:</strong> Tracking, or letter-spacing, is often confused with kerning as it too relates to adding space in between letters. However, whereas kerning adjusts spacing between two letters in order to improve appearances, tracking is used to adjust spacing across a line. This is used more for the purposes of fixing density issues while reading.</p>

<p>To give you a sense for how this differs, here’s an example from <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing">Mozilla</a> on how to use tracking to change letter-spacing:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8796345c-99cd-4880-9fa2-030a2848bb4d/mozilla-tracking-normal.png" sizes="100vw" caption="This is what normal tracking looks like. (Source: <a href='https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing'>Mozilla</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8796345c-99cd-4880-9fa2-030a2848bb4d/mozilla-tracking-normal.png'>Large preview</a>)" alt="Normal tracking example" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f20eef1-e161-4d88-9596-2b1c87b72591/mozilla-neg1px-tracking.png" sizes="100vw" caption="This is what (tighter) -1px tracking looks like. (Source: <a href='https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing'>Mozilla</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f20eef1-e161-4d88-9596-2b1c87b72591/mozilla-neg1px-tracking.png'>Large preview</a>)" alt="-1px tracking example" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/474724ce-eb22-4f0f-b459-7561176f0fa4/mozilla-1px-tracking.png" sizes="100vw" caption="This is what (looser) 1px tracking looks like. (Source: <a href='https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing'>Mozilla</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/474724ce-eb22-4f0f-b459-7561176f0fa4/mozilla-1px-tracking.png'>Large preview</a>)" alt="1px tracking example" >}}

<p><strong>Leading:</strong> Leading, or line spacing, is the amount of distance granted between the baselines of text (the bottom line upon which a font rests). Like tracking, this can be adjusted to fix density issues.</p>

<p>If you’ve been using word processing software for a while, you’re already familiar with leading. Single-spaced text. Double-spaced text. Even 1.5-spaced text. That’s leading.</p>

## The Role Of Typography In Modern Web Design

<p>As for why we care about typography and each of the defining characteristics of it in modern web design, there’s a good reason for it. While it would be great if a well-written blog post or super convincing sales jargon on a landing page were enough to keep visitors happy, that’s not always the case. The choices you make in terms of typography can have major ramifications on whether or not people even give your site’s copy a read.</p>

<p>These are some of the ways in which typography affects your end users:</p>

<p><strong>Reinforce Branding</strong><br />Typography is another way in which you create a specific style for your web design. If images all contain clean lines and serious faces, you would want to use an equally buttoned-up typeface.</p>

<p><strong>Set the Mood</strong><br />It helps establish a mood or emotion. For instance, a more frivolous and light-bodied typeface would signal to users that the brand is fun, young and doesn’t take itself seriously.</p>

<p><strong>Give It a Voice</strong><br />It conveys a sense of personality and voice. While the actual message in the copy will be able to dictate this well, using a font that reinforces the tone would be a powerful choice.</p>

<p><strong>Encourage Reading</strong><br />As you can see, there are a number of ways in which you can adjust how type appears on a screen. If you can give it the right sense of speed and ease, you can encourage more users to read through it all.</p>

<p><strong>Allow for Scanning</strong><br />Scanning or glancing (which I’ll talk about shortly) is becoming more and more common as people engage with the web on their smart devices. Because of this, we need ways to format text to improve scannability and this usually involves lots of headers, pull quotes and in-line lists (bulleted, numbered, etc.).</p>

<p><strong>Improve Accessibility</strong><br />There is a lot to be done in order to <a href="https://www.smashingmagazine.com/2018/04/designing-accessibility-inclusion/">design for accessibility</a>. Your choice of font plays a big part in that, especially as the mobile experience has to rely less on big, bold designs and swatches of color and more on how quickly and well you can get visitors to your message.</p>

<p>Because typography has such a diverse role in the user experience, it’s a matter that needs to be taken seriously when strategizing new designs. So, let’s look at what the experts and tests have to say about handling it for mobile.</p>

## Typography For Mobile Web Design: What You Need To Know

<p>Too small, too light, too fancy, too close together… You can run into a lot of problems if you don’t strike the perfect balance with your choice of typography in design. On mobile, however, it’s a bit of a different story.</p>

<p>I don’t want to say that playing it safe and using the system default from Google or Apple is the way to go. After all, you work so hard to develop unique, creative and eye-catching designs for your users. Why would you throw in the towel at this point and just slap Roboto all over your mobile website?</p>

<p>We know what the key elements are in defining and shaping a typeface and we also know how powerful fonts are within the context of a website. So, let’s drill down and see what exactly you need to do to make your typography play well with mobile.</p>

### 1. Size

<p>In general, the rule of thumb is that font size needs to be <a href="https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/">16 pixels for mobile websites</a>. Anything smaller than that could compromise readability for visually impaired readers. Anything too much larger could also make reading more difficult. You want to find that perfect Goldilocks formula and, time and time again, it comes back to 16 pixels.</p>

<p>In general, that rule is a safe one to play by when it comes to the main body text of your mobile website. However, what exactly are you allowed to do for header text? After all, you need to be able to distinguish your main headlines from the rest of the text. Not just for the sake of calling attention to bigger messages, but also for the purposes of increasing scannability of a mobile web page. </p>

<p>The Nielsen Norman Group reported on <a href="https://journals.sagepub.com/doi/10.1177/1541931213601698">a study from MIT</a> that covered this exact question. What can you do about text that users only have to <em>glance</em> at? In other words, what sort of sizing can you use for short strings of header text?</p>

<p>Here is what they found:</p>

<p>Short, glanceable strings of text lead to faster reading and greater comprehension when:</p>

<ul>
<li>They are larger in size (specifically, 4mm as opposed to 3mm).</li>
<li>They are in all caps.</li>
<li>Lettering width is regular (and not condensed).</li>
</ul>

<p><a href="https://www.nngroup.com/articles/glanceable-fonts/">In sum</a>:</p>

<blockquote>Lowercase lettering required 26% more time for accurate reading than uppercase, and condensed text required 11.2% more time than regular. There were also significant interaction effects between case and size, suggesting that the negative effects of lowercase letters are exacerbated with small font sizes.</blockquote>

<p>I’d be interested to see how the <a href="https://www.nerdwallet.com/">NerdWallet</a> website does, in that case. While I do love the look of this, they have violated a number of these sizing and styling suggestions:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5936dbcd-487f-4ea1-9c45-ef36ccec2a76/nerdwallet-mobile.PNG" sizes="70vw" caption="NerdWallet’s use of all-caps and smaller font sizes on mobile. (Source: <a href='https://www.nerdwallet.com/home/dashboard/home?trk=nw_hp&'>NerdWallet</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5936dbcd-487f-4ea1-9c45-ef36ccec2a76/nerdwallet-mobile.PNG'>Large preview</a>)" alt="The NerdWallet home page" >}}

<p>Having looked at this a few times now, I do think the choice of a smaller-sized font for the all-caps header is an odd choice. My eyes are instantly drawn to the larger, bolder text beneath the main header. So, I think there is something to MIT’s research.</p>

<p><a href="https://www.flywheelsports.com/">Flywheel Sports</a>, on the other hand, does a great job of exemplifying this point.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ec85dab-11b3-45bf-9244-d27e2f6ea851/flywheel-sports-mobile.PNG" sizes="70vw" caption="Flywheel Sports’ smart font choices for mobile. (Source: <a href='https://www.flywheelsports.com/'>Flywheel Sports</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ec85dab-11b3-45bf-9244-d27e2f6ea851/flywheel-sports-mobile.PNG'>Large preview</a>)" alt="The Flywheel Sports home page" >}}

<p>There’s absolutely no doubt where the visitors’ attention needs to go: to the eye-catching header. It’s in all caps, it’s larger than all the other text on the page, and, although the font is incredibly basic, its infusion with a custom handwritten-style type looks really freaking cool here. I think the only thing I would fix here is the contrast between the white and yellow fonts and the blue background.</p>

<p>Just remember: this only applies to the sizing (and styling) of header text. If you want to keep large bodies of text readable, stick to the aforementioned sizing best practices.</p>

### 2. Color and Contrast

<p>Color, in general, is an important element in web design. There’s a lot you can convey to visitors by choosing the right color palette for designs, images and, yes, your text. But it’s not just the base color of the font that matters, it’s also the contrast between it and the background on which it sits (as evidenced by my note above about Flywheel Sports).</p>

<p>For some users, a white font on top of a busy photo or a lighter background may not pose too much of an issue. But “too much” isn’t really acceptable in web design. There should be no issues users encounter when they read text on a website, especially from an already compromised view of it on mobile.</p>

<p>Which is why color and contrast are top considerations you have to make when styling typography for mobile.</p>

<p>The Web Content Accessibility Guidelines (<a href="https://www.w3.org/TR/WCAG20/">WCAG</a>) has clear recommendations regarding how to address color contrast in section 1.4.3. At a minimum, the WCAG suggests that a contrast of 4.5 to 1 should be established between the text and background for optimal readability. There are a few exceptions to the rule:</p>

<ul>
<li>Text sized using 18-point or a bold 14-point only needs a contrast of 3 to 1.</li>
<li>Text that doesn’t appear in an active part of the web page doesn’t need to abide by this rule.</li>
<li>The contrast of text within a logo can be set at the designer’s discretion.</li>
</ul>

<p>If you’re unsure of how to establish that ratio between your font’s color and the background upon which it sits, use a color contrast checking tool like <a href="https://webaim.org/resources/contrastchecker/">WebAIM</a>.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3a364a-d57b-43e6-8845-583299f582c9/webaim.png" sizes="100vw" caption="An example of how to use the WebAIM color contrast checker tool. (Source: <a href='https://webaim.org/resources/contrastchecker/'>WebAIM</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3a364a-d57b-43e6-8845-583299f582c9/webaim.png'>Large preview</a>)" alt="WebAIM color contrast checker" >}}

<p>The one thing I would ask you to be mindful of, however, is using opacity or other color settings that may compromise the color you’ve chosen. While the HEX color code will check out just fine in the tool, it may not be an accurate representation of how the color actually displays on a mobile device (or any screen, really).</p>

<p>To solve this problem and ensure you have a high enough contrast for your fonts, use a color eyedropper tool built into your browser like the ones for <a href="https://developer.mozilla.org/en-US/docs/Tools/Eyedropper">Firefox</a> or <a href="https://chrome.google.com/webstore/detail/eye-dropper/hmdcmlfkchdmnmnmheododdhjedfccka?hl=en">Chrome</a>.  Simply hover the eyedropper over the color of the background (or font) on your web page, and let it tell you what the actual color code is now.</p>

<p>Here is an example of this in action: <a href="https://www.dollarshaveclub.com/">Dollar Shave Club</a>.</p>

<p>This website has a rotation of images in the top banner of the home page. The font always remains white, but the background rotates.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c49e97-d661-4f8b-950b-64086e0ee116/dollarshaveclub-grey.PNG" sizes="70vw" caption="Dollar Shave Club’s home page banner with a grey background. (Source: <a href='https://www.dollarshaveclub.com/'>Dollar Shave Club</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c49e97-d661-4f8b-950b-64086e0ee116/dollarshaveclub-grey.PNG'>Large preview</a>)" alt="Dollar Shave Club grey banner" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2bd46f-6ed0-4a0a-809d-b2756298986c/dollarshaveclub-beige.PNG" sizes="70vw" caption="Dollar Shave Club’s home page banner with a beige/taupe background. (Source: <a href='https://www.dollarshaveclub.com/'>Dollar Shave Club</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2bd46f-6ed0-4a0a-809d-b2756298986c/dollarshaveclub-beige.PNG'>Large preview</a>)" alt="Dollar Shave Club beige banner" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25372d2b-b8a3-42d1-98f5-0b720c34dd14/dollarshaveclub-purple.PNG" sizes="70vw" caption="Dollar Shave Club’s home page banner with a purple background. (Source: <a href='https://www.dollarshaveclub.com/'>Dollar Shave Club</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25372d2b-b8a3-42d1-98f5-0b720c34dd14/dollarshaveclub-purple.PNG'>Large preview</a>)" alt="Dollar Shave Club purple banner" >}}

<p>Based on what we know now, the purple is probably the only one that will pass with flying colors. However, for the purposes of showing you how to work through this exercise, here is what the eyedropper tool says about the HEX color codes for each of the backgrounds:</p>

<ul>
<li>Grey: #9a9a9a</li>
<li>Beige/taupe: #ffd0a8</li>
<li>Purple: #4c2c59.</li>
</ul>

<p>Here is the contrast between these colors and the white font:</p>

<ul>
<li>Grey: 2.81 to 1</li>
<li>Beige/taupe: 1.42 to 1</li>
<li>Purple: 11.59 to 1.</li>
</ul>

<p>Clearly, the grey and beige backgrounds are going to lend themselves to a very poor experience for mobile visitors.</p>

<p>Also, if I had to guess, I’d say that “Try a risk-free Starter Set now.” is only a 10-point font (which is only about 13 pixels). So, the size of the font is also working against the readability factor, not to mention the poor choice of colors used with the lighter backgrounds.</p>

<p>The lesson here is that you should really make some time to think about how color and contrast of typography will work for the benefit of your readers. Without these additional steps, you may unintentionally be preventing visitors from moving forward on your site.</p>

### 3. Tracking

<p>Plain and simple: tracking in mobile web design needs to be used in order to control density. The standard recommendation is that there be no more than between 30 and 40 characters to a line. Anything more or less could affect readability adversely.</p>

<p>While it does appear that <a href="https://www.dove.com/us/en/home.html">Dove</a> is pushing the boundaries of that 40-character limit, I think this is nicely done.<p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/295c55a1-f409-4655-87e4-950539162016/dove-mobile.PNG" sizes="70vw" caption="Dove’s use of even tracking and (mostly) staying within the 40-character limit. (Source: <a href='https://www.dove.com/us/en/home.html'>Dove</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/295c55a1-f409-4655-87e4-950539162016/dove-mobile.PNG'>Large preview</a>)" alt="The Dove home page" >}}

<p>The font is so simple and clean, and the tracking is evenly spaced. You can see that, by keeping the amount of words on a line relegated to the recommended limits, it gives this segment of the page the appearance that it will be easy to read. And that’s exactly what you want your typography choices to do: to welcome visitors to stop for a brief moment, read the non-threatening amount of text, and then go on their way (which, hopefully, is to conversion).</p>

### 4. Leading

<p>According to the <a href="https://www.nngroup.com/articles/mobile-ux/">NNG</a>, content that appears above the fold on a 30-inch desktop monitor equates to five swipes on a 4-inch mobile device. Granted, this data is a bit old as most smartphones are now <a href="https://techcrunch.com/2017/05/31/phables-are-the-phuture/">between five and six inches</a>:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e868980-108e-48e0-a4fc-f76abaacb5d8/techcrunch-screen-size.png" sizes="100vw" caption="Average smartphone screen sizes from 2015 to 2021. (Source: <a href='https://techcrunch.com/2017/05/31/phables-are-the-phuture/'>TechCrunch</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e868980-108e-48e0-a4fc-f76abaacb5d8/techcrunch-screen-size.png'>Large preview</a>)" alt="Average smartphone screen sizes" >}}

<p>Even so, let’s say that equates to three or four good swipes of the smartphone screen to get to the tip of the fold on desktop. That’s a lot of work your mobile visitors have to do to get to the good stuff. It also means that their patience will already be wearing thin by the time they get there. As the NNG pointed out, a mobile session, on average, usually lasts about only 72 seconds. Compare that to desktop at 150 seconds and you can see why this is a big deal.</p>

<p>This means two things for you:</p>

<ol>
<li>You absolutely need to cut out the excess on mobile. If this means creating a completely separate and shorter set of content for mobile, do it.</li>
<li>Be very careful with leading.</li>
</ol>

<p>You’ve already taken care to keep optimize your font size and width, which is good. However, too much leading and you could unintentionally be asking users to scroll even more than they might have to. And with every scroll comes the possibility of fatigue, boredom, frustration, or distraction getting in the way.</p>

<p>So, you need to strike a good balance here between using line spacing to enhance readability while also reigning in how much work they need to do to get to the bottom of the page.</p>

<p>The <a href="https://www.hhcc.com/">Hill Holliday</a> website isn’t just awesome inspiration on how to get a little “crazy” with mobile typography, but it also has done a fantastic job in using leading to make larger bodies of text easier to read:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e51d3fb7-d76a-4dfc-ad2c-852f0057c9a1/hill-holliday-mobile.PNG" sizes="70vw" caption="Hill Holliday uses the perfect ratio of leading between lines and paragraphs. (Source: <a href='https://www.hhcc.com/'>Hill Holliday</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e51d3fb7-d76a-4dfc-ad2c-852f0057c9a1/hill-holliday-mobile.PNG'>Large preview</a>)" alt="The Hill Holliday home page" >}}

<p>Different resources will give you different guidelines on how to create spacing for mobile devices. I’ve seen suggestions for anywhere between 120% to 150% of the font’s point size. Since you also need to consider accessibility when designing for mobile, I’m going to suggest you follow <a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-visual-presentation.html">WCAG’s guidelines</a>:</p>

<ul>
<li>Spacing between lines needs to be 1.5 (or 150%, whichever ratio works for you).</li>
<li>Spacing between paragraphs then needs to be 2.5 (or 250%).</li>
</ul>

<p>At the end of the day, this is about making smart decisions with the space you’re given to work with. If you only have a minute to hook them, don’t waste it with too much vertical space. And don’t turn them off with too little.</p>

### 5. Acceptable Fonts

<p>Before I break down what makes for an acceptable font, I want to first look at what Android’s and Apple’s typeface defaults are. I think there’s a lot we can learn just by looking at these choices:</p>

<p><strong>Android</strong><br /><a href="https://material.io/guidelines/style/typography.html#">Google</a> uses two typefaces for its platforms (both desktop and mobile): Roboto and Noto. Roboto is the primary default. If a user visits a website in a language that doesn’t accept Roboto, then Noto is the secondary backup.</p>

<p>This is <a href="https://fonts.google.com/specimen/Roboto">Roboto</a>:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d6c42dd-1845-49b3-b0ef-fc9e727328b7/roboto.png" sizes="100vw" caption="A snapshot of the Roboto character set. (Source: <a href='https://fonts.google.com/specimen/Roboto'>Roboto</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d6c42dd-1845-49b3-b0ef-fc9e727328b7/roboto.png'>Large preview</a>)" alt="The Roboto character set" >}}

<p>It’s also important to note that Roboto has a number of <a href="https://fonts.google.com/?query=roboto">font families</a> to choose from:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a099bd1-c54f-456e-9784-dd737b129087/roboto-families.png" sizes="100vw" caption="Other options of Roboto fonts to choose from. (Source: <a href='https://fonts.google.com/specimen/Roboto'>Roboto</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a099bd1-c54f-456e-9784-dd737b129087/roboto-families.png'>Large preview</a>)" alt="The Roboto families" >}}

<p>As you can see, there are versions of Roboto with condensed kerning, a heavier and serifed face as well as a looser, serif-like option. Overall, though, this is just a really clean and simply stylized typeface. You’re not likely to stir up any real emotions when using this on a website, and it may not convey much of a personality, but it’s a safe, smart choice.</p>

<p><strong>Apple</strong><br /><a href="https://developer.apple.com/ios/human-interface-guidelines/visual-design/typography/">Apple</a> has its own set of typography guidelines for iOS along with its own system typeface: <a href="https://developer.apple.com/fonts/">San Francisco</a>.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bbd8c8c-a0b9-497c-a897-b7a438ccb676/san-francisco.png" sizes="100vw" caption="The San Francisco font for Apple devices. (Source: <a href='https://developer.apple.com/fonts/'>San Francisco</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bbd8c8c-a0b9-497c-a897-b7a438ccb676/san-francisco.png'>Large preview</a>)" alt="The San Francisco font" >}}

<p>For the most part, what you see is what you get with San Francisco. It’s just a basic sans serif font. If you look at Apple’s recommended suggestions on default settings for the font, you’ll also find it doesn’t even recommend using bold stylization or outlandish sizing, leading or tracking rules:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd069d4c-ef2d-4277-84ec-dc67bcaa89b1/san-francisco-defaults.png" sizes="100vw" caption="Default settings and suggestions for the San Francisco typeface. (Source: <a href='https://developer.apple.com/fonts/'>San Francisco</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd069d4c-ef2d-4277-84ec-dc67bcaa89b1/san-francisco-defaults.png'>Large preview</a>)" alt="San Francisco default settings" >}}

<p>Like with pretty much everything else Apple does, the typography formula is very basic. And, you know what? It really works. Here it is in action on the <a href="https://www.apple.com/">Apple</a> website:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71f475b5-a3ca-4267-a1c7-e2b0889a483c/apple-mobile.PNG" sizes="70vw" caption="Apple makes use of its own typography best practices. (Source: <a href='https://www.apple.com/'>Apple</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71f475b5-a3ca-4267-a1c7-e2b0889a483c/apple-mobile.PNG'>Large preview</a>)" alt="The Apple home page" >}}

<p>Much like Google’s system typeface, Apple has gone with a simple and classic typeface. While it may not help your site stand out from the competition, it will never do anything to impair the legibility or readability of your text. It also would be a good choice if you want your visuals to leave a greater impact.</p>

#### My Recommendations

<p>And, so, this now brings me to my own recommendations on what you should use in terms of type for mobile websites. Here’s the verdict:</p>

<ol>
<li>Don’t be afraid to start with a system default font. They’re going to be your safest choices until you get a handle on how far you can push the limits of mobile typography. </li>
<li><p>Use only a sans serif or serif font. If your desktop website uses a decorative or handwritten font, ditch it for something more traditional on mobile.</p>

<p>That said, you don’t have to ignore decorative typefaces altogether. In the examples from Hill Holliday or Flywheel Sports (as shown above), you can see how small touches of custom, non-traditional type can add a little flavor.</p></li>
<li><p>Never use more than two typefaces on mobile. There just isn’t enough room for visitors to handle that many options visually.</p>

<p>Make sure your two typefaces complement one another. Specifically, look for faces that utilize a similar character width. The design of each face may be unique and contrast well with the other, but there should still be some uniformity in what you present to mobile visitors’ eyes.</p></li>
<li><p>Avoid typefaces that don’t have a distinct set of characters. For instance, compare how the uppercase “i”, lowercase “l” and the number “1” appear beside one another. Here’s an example of the Myriad Pro typeface from the Typekit website:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/102dc7cf-89d5-44d7-87ae-b7738aa638fd/myriad-pro-lettering.png" sizes="100vw" caption="Myriad Pro’s typeface in action. (Source: <a href='https://typekit.com/fonts/myriad'>Typekit</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/102dc7cf-89d5-44d7-87ae-b7738aa638fd/myriad-pro-lettering.png'>Large preview</a>)" alt="Myriad Pro characters" >}}

<p>While the number “1” isn’t too problematic, the uppercase “i” (the first letter in this sequence) and the lowercase “l (the second) are just too similar. This can create some unwanted slowdowns in reading on mobile.</p>

<p>Also, be sure to review how your font handles the conjunction of “r” and “n” beside one another. Can you differentiate each letter or do they smoosh together as one indistinguishable unit? Mobile visitors don’t have time to stop and figure out what those characters are, so make sure you use a typeface that gives each character its own space.</p></li>
<li><p>Use fonts that are <a href="https://jordanm.co.uk/tinytype/">compatible across as many devices</a> as possible. Your best bets will be: Arial, Courier New, Georgia, Tahoma, Times New Roman, Trebuchet MS and Verdana.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/511447d0-44ac-4294-92dc-cd598c7a5c30/tinytype-compatibility.png" sizes="100vw" caption="A list of system default typefaces for various mobile devices. (Source: <a href='https://jordanm.co.uk/tinytype/'>tinytype</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/511447d0-44ac-4294-92dc-cd598c7a5c30/tinytype-compatibility.png'>Large preview</a>)" alt="Default typefaces on mobile" >}}

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fd968e7-20cc-418d-8550-cf1ebccc11dc/tinytype-android-fonts.png" sizes="100vw" caption="Another view of the table that includes some Android-supported typefaces. (Source: <a href='https://jordanm.co.uk/tinytype/'>tinytype</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fd968e7-20cc-418d-8550-cf1ebccc11dc/tinytype-android-fonts.png'>Large preview</a>)" alt="Android-supported typefaces" >}}

<p>I think the <a href="https://www.typeform.com/">Typeform</a> website is a good example of one that uses a “safe” typeface choice, but doesn’t prevent them from wowing visitors with their message or design.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/797c5507-4cfa-4fdb-aaa7-2514e4561b47/typeform-mobile.PNG" sizes="70vw" caption="Typeform’s striking typeface has nothing to do with the actual font. (Source: <a href='https://www.typeform.com/'>Typeform</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/797c5507-4cfa-4fdb-aaa7-2514e4561b47/typeform-mobile.PNG'>Large preview</a>)" alt="The Typeform home page" >}}

<p>It’s short, to the point, perfectly sized, well-positioned, and overall a solid choice if they’re trying to demonstrate stability and professionalism (which I think they are).</p></li>
<li>When you’re feeling comfortable with mobile typography and want to branch out a little more, take a look at this list of the best web-safe typefaces from <a href="https://websitesetup.org/web-safe-fonts-html-css/">WebsiteSetup</a>. You’ll find here that most of the choices are your basic serif and sans serif types. It’s definitely nothing exciting or earth-shattering, but it will give you some variation to play with if you want to add a little more flavor to your mobile type.</li>
</ol>

## Wrapping Up

<p>I know, I know. Mobile typography is no fun. But web design isn’t always about creating something exciting and cutting edge. Sometimes sticking to practical and safe choices is what will guarantee you the best user experience in the end. And that’s what we’re seeing when it comes to mobile typography.</p>

<p>The reduced amount of real estate and the shorter times-on-site just don’t lend themselves well to the experimental typography choices (or design choices, in general) you can use on desktop. So, moving forward, your approach will have to be more about learning how to reign it in while still creating a strong and consistent look for your website.</p>

{{< signature "lf, ra, yk, il" >}}

