---
title: 5 Useful Coding Solutions For Designers And Developers
slug: 6-useful-coding-solutions-for-designers-and-developers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffb88481-23a2-4fb8-95da-87a81bfe23a8/css-typography.jpg
date: 2009-11-23T12:41:19.000Z
author: soh-tanaka
description: >-
  Let's look at some clever techniques developed and used
  by top professionals in the Web design industry. We can use their examples
  to develop our own alternative solutions.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
---
This post is the the next installment of posts featuring "[Useful Coding Solutions for Designers and Developers](https://www.smashingmagazine.com/2008/08/11/5-useful-coding-solutions-for-designers-and-developers/)", a series of posts focusing on unique and creative CSS/JavaScript-techniques being implemented by talented professionals in our industry. A key talent that any Web designer must acquire is the ability to observe, understand and build on other people's designs. This is a great way to develop the skills and techniques necessary to produce effective websites.

With that in mind, **let's look at some clever techniques developed and used by top professionals in the Web design industry**. We can use their examples to develop our own alternative solutions.</p>

## 1\. Designing a Slick CSS Timeline

Designing a timeline is one of the tasks that frequently need to be solved when it comes to the design of portfolios. Some designers present the timeline as an image, others use plain text or use a good old table. We found an interesting CSS-based solution of a timeline over at [37Signals.com](https://37signals.com/about). While timelines are usually designed horizontally, this one is vertical, zig-zagging down each time slot.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4c968f2-88a0-4ccb-8d24-11ac3839fbe9/css-timeline.jpg)](https://37signals.com/about)

{{% feature-panel %}}

**How is this done?**  
To achieve this zig-zag effect, we will be floating each row. By assigning an "even" class, we are able to specify a different style for the right-aligned time slots, controlling their colors and alignment.  
[See the demo](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35647be2-5eb1-47b6-92df-0c7c27b5ae1a/timeline.htm).

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fac9df7-f8ea-4104-8e67-d1fd7da55ef7/article-2-b.gif)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35647be2-5eb1-47b6-92df-0c7c27b5ae1a/timeline.htm)

Here is the HTML:

<pre><code class="language-markup tmp-xml">&lt;div class=&quot;timeslot&quot;&gt;
  &lt;span&gt;2009&lt;/span&gt;
  &lt;p&gt;Duis acsi ullamcorper humo decet, incassum validus, appellatio in qui tation roto, lobortis brevitas epulae. Et ymo eu utrum probo ut, jugis, delenit.
  &lt;/p&gt;
  &lt;/div&gt;
  &lt;div class=&quot;timeslot even&quot;&gt;
  &lt;span&gt;2008&lt;/span&gt;
  &lt;p&gt;Duis acsi ullamcorper humo decet, incassum validus, appellatio in qui tation roto, lobortis brevitas epulae. Et ymo eu utrum probo ut, jugis, delenit.
  &lt;/p&gt;
&lt;/div&gt;</code></pre> 

And here is the CSS:

The default `timeslot` will float left and have a 100-pixel padding to the right. This leaves room for the year (`<span>`) to sit to its right. I also used absolute positioning for the year so that I could easily switch from left to right without worrying about colliding float issues.

Add a class of `even` to each even row, so that we get it right-aligned in red and the year positioned to the left.

<pre><code class="language-css">.timeslot {
  width: 235px;
  float: left;
  margin: 0 0 10px;
  padding: 10px 100px 0 0;
  border-top: 3px solid #ddd;
  position: relative;
}
.timeslot span {
  position: absolute;
  right: 0;
  top: 27px;
  font-size: 3em;
  color: #999;
}
.even {
  float: right;
  padding: 10px 0 0 100px;
  border-color: #ca0000;
}
.even span {
  left: 0;
  color: #ca0000;
}</code></pre>

## 2\. Custom Page Styling, CSS Drop Caps and Footnotes

One website that is truly unique is [Jason Santa Maria's](https://jasonsantamaria.com/articles/mathematics-of-the-tootsie-pop/). What's impressive about Jason's website is that each article and blog post is entirely unique, with its design tailored to the content. Looking at a recent article, "[Mathematics of the Tootsie Pop](https://jasonsantamaria.com/articles/mathematics-of-the-tootsie-pop/)," we'll go over a few techniques that stand out for us.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c9dd973-7dec-4108-b5b1-f6ce9e60a8a2/article-1-a.gif)](https://jasonsantamaria.com/articles/mathematics-of-the-tootsie-pop/)

### 1. Custom Page Styling in WordPress

The first question that came to mind when visiting Jason's blog was, "How did he give each post a unique design?" You can achieve this simply by referencing a custom style sheet to override the website's default style. By using a combination of [custom fields](https://codex.wordpress.org/Custom_Fields) in WordPress and understanding [CSS specificity](https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/), you can freely give each post a design of its own. So, **how is this done?**

_Step 1\. Customize post with custom style sheet_  
Start by creating a new style sheet, and name the file to match your post's title. With a good understanding of [CSS specificity](https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/), you can customize the look and feel of the post.

_Step 2\. Create custom field values_  
Log in to your WordPress admin area, and go to the edit page for the post. Scroll down to the "Custom Field" area, and enter a new custom field name called "customStyles". Then, for the value of that custom field, enter the full URL of your custom style sheet.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c3f4d82-4b50-4c1e-bc57-cb0946188dc8/article-1-d.gif)

_Step 3\. Call the custom style sheet_  
Open up the _header.php_ file in your custom theme, and above your `<title>` tag, add the following:

<pre><code class="language-php">&lt;?php $customStyles = get_post_meta($post-&gt;ID, &quot;customStyles&quot;, true);
if (!empty($customStyles)) { ?&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;&lt;?php echo $customStyles; ?&gt;&quot; type=&quot;text/css&quot; media=&quot;screen&quot; /&gt;
&lt;?php } ?&gt;</code></pre>

In this step, we're checking if a custom field of "customStyles" exists. If it does, then it will inject the value within the `href` of the style sheet reference.

Custom field tutorials:

*   [Custom Fields Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-WordPress/)
*   [WordPress Custom Fields, Part I: The Basics](https://perishablepress.com/press/2008/12/17/WordPress-custom-fields-tutorial/)
*   [WordPress Custom Fields, Part II: Tips and Tricks](https://perishablepress.com/press/2008/12/22/WordPress-custom-fields-tips-tricks/)

CSS specificity tutorials:

*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/)
*   [Specifics on CSS Specificity](https://css-tricks.com/specifics-on-css-specificity/)
*   [Understanding CSS Specificity](https://snook.ca/archives/html_and_css/understanding_c/)

### 2. Creating Drop Caps

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50cf1f8-40a5-47a6-9c4f-1ac05524fcd8/article-1-b.gif)

Drop caps are commonly seen in print design, but with the recent rise in popularity of Web typography, this technique seems to be becoming more common. We have various ways of achieving this technique.

Here is the HTML you would use:

<pre><code class="language-markup tmp-xml">&lt;p&gt;&lt;span class=&quot;dropCap&quot;&gt;E&lt;/span&gt;ros decet bis eligo jumentum brevitas vel abigo iusto commoveo ex abigo, euismod ulciscor. Bene enim vulputate enim, nisl illum patria. Enim te, verto euismod in nisl lucidus. Capio incassum quadrum nunc ex proprius praesent et quod. Autem in commoveo similis nostrud turpis paulatim quadrum, tristique. &lt;/p&gt;</code></pre> 

_Plain-text drop caps_  
Plain-text drop caps can be achieved with just a few lines of CSS. Until Web typography advances, and the `@font-face` standard becomes more widely supported, this is probably the easiest way to achieve drop caps. [See demo](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/912dda45-e44e-46ab-aa27-e178ce2abe30/dropcaps.htm).

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93a1485c-e2e9-497a-8022-922566d7fcb4/article-1-g.gif)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/912dda45-e44e-46ab-aa27-e178ce2abe30/dropcaps.htm)

Here is the CSS:

<pre><code class="language-css">.dropCap {
  float: left;
  font-size: 5em;
  line-height: 0.9em;
  padding: 0 5px 0 0;
  font-family: Georgia, "Times New Roman", Times, serif;
}</code></pre> 

To jazz up your plain text, check out the following tutorials on enhancement:

*   [Create a Letterpress Effect with CSS Text-Shadow](https://line25.com/tutorials/create-a-letterpress-effect-with-css-text-shadow)
*   [CSS Gradient Text Effect](https://www.webdesignerwall.com/tutorials/css-gradient-text-effect/)

_Text-replacement drop caps_  
Here, we are simply substituting an image for a letter, using a combination of `text-indent` and background image. [See demo](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b21a86b3-bff2-4884-ac2c-5d547df1d9c7/dropcaps2.htm).

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6fd4ed7-32b8-43f8-896f-024eb1f58766/article-1-h.gif)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b21a86b3-bff2-4884-ac2c-5d547df1d9c7/dropcaps2.htm)

Here is the CSS:

<pre><code class="language-css">.dropCap {
  text-indent: -99999px;
  background: url(drop_cap_e.gif) no-repeat left 5px;
  height: 50px; width: 55px;
  float: left;
  display: block;
}</code></pre> 

While this technique is perfect for Jason's post (because he uses only one drop cap), if you plan to use multiple drop caps, you should look into using [CSS sprites](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/). [Mark Boulton](https://www.markboulton.co.uk/) offers a great example of this technique.

_jQuery-based Drop Caps_  
A few years ago, [Karl Swedberg](https://www.karlswedberg.com/) of [LearningjQuery.com](https://www.learningjquery.com/) introduced an awesome way to incorporate drop caps using jQuery. Please notice that using jQuery for presentational purposes may be not a good idea and contradicts the strict separation between the presentation and behaviour layers, but it does solve the problem nevertheless. You may want to check out Karl Swedberg's drop-cap plugin that does a better job of keeping the presentation and behavior layers separate by simply wrapping a span around the first letter (with appropriate classes). That way you can style the letter however you like with CSS. Also check out the tutorials below:

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd3036bd-caa3-49d5-8c57-470234c8ca0a/article-1-e.gif)](https://www.learningjquery.com/2006/09/fancy-drop-cap-part-1)

*   [Fancy Drop Cap – Part 1](https://www.learningjquery.com/2006/09/fancy-drop-cap-part-1)
*   [Fancy Drop Cap – Part 2](https://www.learningjquery.com/2006/10/fancy-drop-cap-part-2)
*   [Multiple Fancy Drop Caps](https://www.learningjquery.com/2006/12/multiple-fancy-drop-caps)

### 3. Footnotes

Footnotes are another interesting part of Jason's post. The red stripe that bleeds across the page really accents the footnotes well here.

That bleeding red stripe can be achieved by nesting two DIV tags: the parent DIV, which contains a repeating background image (positioned at the bottom), and a second DIV, which is the actual fixed container where the content lies. This way, the red stripe follows the end of the content and aligns perfectly with the footnotes.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f73065-3c6f-4fce-8fb1-601d1066014a/article-1-f.jpg)

## 3\. Text Flow

Like Jason Santa Maria, Dustin Curtis has his own way of giving each post a unique style. In the example below, you can see the interesting way in which the text flows down the page beside the pictures of the MRI. This technique is quite simple to do and is a good use of relative positioning.

**How is this done?** The text flow seen in Dustin's design can be achieved by giving each text block a relative position, a fixed width and fixed coordinates. His post has a mix of large backgrounds, text replacement and relatively positioned text blocks.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5362e188-1091-4c18-a08a-7844b06a05df/brain.jpg)

Sample HTML:

<pre><code class="language-markup tmp-xml">&lt;p class=&quot;small&quot;
  style=&quot; position: relative;top: 260px;width: 430px;left: 290px;&quot;&gt;
    &lt;strong&gt;At its core, it is the &quot;artful&quot; hemisphere.&lt;/strong&gt; Abstract thinking, intonation
    and rhythm of language, artistic ability, and the perception of joy from music are centered here.
    The right hemisphere specializes in thinking about big picture ideas and overarching themes holistically
    instead of linearly.
&lt;/p&gt;</code></pre> 

Although inline styles are typically not recommended, this would be a rare exception. Create a global class name for the default styling of all text blocks (margin, padding, text size, color, etc.), and use inline styling for the page-specific design (coordinates, width, etc.). [See demo](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70cc5ccb-7a85-4ec8-8c31-201e090e7310/textflow.htm).

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb8537a-4847-4d04-85d0-81f36d54ee51/article-3-b.gif)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70cc5ccb-7a85-4ec8-8c31-201e090e7310/textflow.htm)

CSS:

<pre><code class="language-css">.textflow {
  font-size: 1.2em;
  color: #2d2d2d;
  margin: 20px 0;
  padding: 5px 0;
  position: relative;
}</code></pre> 

HTML:

<pre><code class="language-markup tmp-xml">&lt;div class=&quot;textflow&quot; style=&quot;width:300px; left: 680px;&quot;&gt;
  &lt;p&gt;Ad, natu virtus, ut ea, tristique aptent illum iustum abigo ad vulputate gravis melior quae.&lt;/p&gt; 
&lt;/div&gt;</code></pre> 

CSS positioning tutorials:

*   [CSS Positioning](https://www.w3schools.com/Css/css_positioning.asp)
*   [Absolute, Relative, Fixed Positioning: How Do They Differ?](https://css-tricks.com/absolute-relative-fixed-positioining-how-do-they-differ/)
*   Stopping the CSS positioning panic (Part 1)
*   [Mastering CSS Coding: Getting Started](https://www.smashingmagazine.com/2009/10/05/mastering-css-coding-getting-started/#CSS-Basics7)

## 4\. Combo Carousel Breakdown

Over at [Technikwürze](https://technikwuerze.de/das-team/#teammod_dm), we have found a carousel with a combination of animation effects. This is no ordinary carousel. For this example, rather than go over specific techniques, we'll discuss the logic behind this unique carousel.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c002c93-d484-4fa6-a2cb-65848a3516e9/combo2.jpg)](https://technikwuerze.de/das-team/#teammod_dm)

**How is this done?** As you can see, when clicking on a member's thumbnail, three primary animations are triggered:

1.  The member bio slides in horizontally,
2.  The profile image slides in vertically,
3.  The grid of member photos updates, and the height of the container adjusts.

To begin, the full member profiles are floated so that they appear side by side. We use `overflow: hidden;` to mask the non-active profiles. Here is a visual demo of this carousel's logic:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e70a5c1-ed60-4213-bfd3-f8851f68e856/article-5-default.gif)

**1\. Horizontal animation**  
Each time a thumbnail is clicked, jQuery calculates how far the profiles need to slide over. This is the classic [horizontal-sliding carousel](https://zendold.lojcomm.com.br/icarousel/example6.asp) effect.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48106221-2bd9-464e-98fa-728923e14848/article-5-b.gif)

**2\. Vertical animation**  
Once the active profile slides into position, the image for the profile slides down. To begin, all profile images are position `-190px` above the frame. When jQuery detects that the horizontal animation has been triggered, it slides the profile image down.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f83e5c8-5502-4a3d-9038-419af5f07554/article-5-c.gif)

**3\. Vertical animation**  
During the transition to the active profile, its height is calculated and the container is adjusted. This way, the container stays snug and does not leave any excess white space at the bottom.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/694b34cc-146b-4d8e-b72a-f7d51539a1e1/article-5-d.gif)

Carousel tutorials and plug-ins:

*   jQuery Infinite Carousel
*   [Create a Simple Infinite Carousel with jQuery](https://www.queness.com/post/923/create-a-simple-infinite-carousel-with-jquery)
*   <span class="removed_link" title="https://woork.blogspot.com/2009/05/7-powerful-image-carousels-for-web.html">Create a Simple Infinite Carousel with jQuery</span>
*   Coda-Slider

### Graceful Degradation

The team at Technikwürze also implemented a fall-back option for this carousel. With a smart use of CSS, it crafted this page so that anything JavaScript-driven is tucked away. The resulting page is clean and accessible to all users.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5377d005-8081-4524-b220-15d7a592a936/carousel-fallback.jpg)

## 5\. Beautiful Typographic CSS-Based Ratings

Over at [Web Appstorm](https://web.appstorm.net/reviews/getting-started-with-google-wave-an-early-look/#summary), we have an interesting way of showing ratings with CSS. This CSS-based system can be achieved using absolute positioning and an image of the maximum rating.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ecf26d-19f9-4aae-ac45-6daaa171ba3c/score.jpg)](https://web.appstorm.net/reviews/getting-started-with-google-wave-an-early-look/#summary)

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9952375a-69b4-4e52-8642-19e50767c3a7/article-4-a.gif)](https://web.appstorm.net/reviews/getting-started-with-google-wave-an-early-look/#summary)

**How is this done?** Here is the HTML and CSS:

<pre><code class="language-markup tmp-xml">&lt;span class=&quot;the_score&quot;&gt;8&lt;/span&gt;
&lt;img class=&quot;ten&quot; src=&quot;https://web.appstorm.net/wp-content/themes/appstorm_v2/images/ten.gif&quot; alt=&quot;&quot;&gt;</code></pre> 

<pre><code class="language-css">.tabdiv .the_score {
  font-family: "Myriad Pro", Helvetica, Arial, sans-serif;
  font-size: 110px;
  line-height: 110px;
  font-weight: bold;
  position: absolute;
  top: 30px;
  right: 100px;
  color: #262626;
  text-align: center;
  letter-spacing: -17px;
}
.tabdiv .ten {
  position: absolute;
  top: 80px;
  right: 45px;
}</code></pre> 

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c002c93-d484-4fa6-a2cb-65848a3516e9/combo2.jpg)](https://technikwuerze.de/das-team/#teammod_dm)

**How is this done?** As you can see, when clicking on a member's thumbnail, three primary animations are triggered:

1.  The member bio slides in horizontally,
2.  The profile image slides in vertically,
3.  The grid of member photos updates, and the height of the container adjusts.

To begin, the full member profiles are floated so that they appear side by side. We use `overflow: hidden;` to mask the non-active profiles. Here is a visual demo of this carousel's logic:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e70a5c1-ed60-4213-bfd3-f8851f68e856/article-5-default.gif)

**1\. Horizontal animation**  
Each time a thumbnail is clicked, jQuery calculates how far the profiles need to slide over. This is the classic [horizontal-sliding carousel](https://zendold.lojcomm.com.br/icarousel/example6.asp) effect.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48106221-2bd9-464e-98fa-728923e14848/article-5-b.gif)

**2\. Vertical animation**  
Once the active profile slides into position, the image for the profile slides down. To begin, all profile images are position `-190px` above the frame. When jQuery detects that the horizontal animation has been triggered, it slides the profile image down.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f83e5c8-5502-4a3d-9038-419af5f07554/article-5-c.gif)

**3\. Vertical animation**  
During the transition to the active profile, its height is calculated and the container is adjusted. This way, the container stays snug and does not leave any excess white space at the bottom.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/694b34cc-146b-4d8e-b72a-f7d51539a1e1/article-5-d.gif)

Carousel tutorials and plug-ins:

*   jQuery Infinite Carousel
*   [Create a Simple Infinite Carousel with jQuery](https://www.queness.com/post/923/create-a-simple-infinite-carousel-with-jquery)
*   <span class="removed_link" title="https://woork.blogspot.com/2009/05/7-powerful-image-carousels-for-web.html">Create a Simple Infinite Carousel with jQuery</span>
*   Coda-Slider

### Graceful Degradation

The team at Technikwürze also implemented a fall-back option for this carousel. With a smart use of CSS, it crafted this page so that anything JavaScript-driven is tucked away. The resulting page is clean and accessible to all users.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5377d005-8081-4524-b220-15d7a592a936/carousel-fallback.jpg)

## 5\. Beautiful Typographic CSS-Based Ratings

Over at [Web Appstorm](https://web.appstorm.net/reviews/getting-started-with-google-wave-an-early-look/#summary), we have an interesting way of showing ratings with CSS. This CSS-based system can be achieved using absolute positioning and an image of the maximum rating.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ecf26d-19f9-4aae-ac45-6daaa171ba3c/score.jpg)](https://web.appstorm.net/reviews/getting-started-with-google-wave-an-early-look/#summary)

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9952375a-69b4-4e52-8642-19e50767c3a7/article-4-a.gif)](https://web.appstorm.net/reviews/getting-started-with-google-wave-an-early-look/#summary)

**How is this done?** Here is the HTML and CSS:

<pre><code class="language-markup tmp-xml">&lt;span class=&quot;the_score&quot;&gt;8&lt;/span&gt;
&lt;img class=&quot;ten&quot; src=&quot;https://web.appstorm.net/wp-content/themes/appstorm_v2/images/ten.gif&quot; alt=&quot;&quot;&gt;</code></pre> 

<pre><code class="language-css">.tabdiv .the_score {
  font-family: "Myriad Pro", Helvetica, Arial, sans-serif;
  font-size: 110px;
  line-height: 110px;
  font-weight: bold;
  position: absolute;
  top: 30px;
  right: 100px;
  color: #262626;
  text-align: center;
  letter-spacing: -17px;
}
.tabdiv .ten {
  position: absolute;
  top: 80px;
  right: 45px;
}</code></pre> 

### Alternative Solution

If you would like the maximum rating to vary, you can achieve this effect using the following alternative method.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89bf6792-f88e-4279-8726-78544294f595/article-4-b.gif)

HTML:

<pre><code class="language-markup tmp-html">&lt;div class=&quot;ratingblock&quot;&gt;
  &lt;span class=&quot;rating&quot;&gt;8&lt;/span&gt;
  &lt;span class=&quot;max&quot;&gt;10&lt;/span&gt;
&lt;/div&gt;</code></pre> 

CSS:

As you can see, `.max` is absolute positioned, has a transparent background and is layered above `.rating`. That way, if you need to adjust the maximum rating, you can do so without modifying any images.

<pre><code class="language-css">.ratingblock{
  position: relative;
  height: 100px;
}
.ratingblock .rating {
  font-size: 8em; 
  padding: 0 5px;
}
.ratingblock .max{
  display: block;
  background: url(rating_bg.gif) no-repeat;
  position: absolute;
  top: 0; left: 0;
  font-size: 5em; 
  width: 50px;
  height: 60px;
  padding: 40px 0 0 50px;
}</code></pre>

## Final Thoughts

By examining the techniques others have used to achieve unique and inspirational results, we expand our foundation in Web design. It's a great way to learn and push ourselves to ever-higher levels. Stay hungry and keep learning!

{{< signature "al" >}}

