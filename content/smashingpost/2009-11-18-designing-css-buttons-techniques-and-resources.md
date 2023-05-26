---
title: 'Designing CSS Buttons: Techniques and Resources'
slug: designing-css-buttons-techniques-and-resources
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed26d34a-b8e2-4936-8309-92f9488a85bb/buttons.png
date: 2009-11-18T15:23:29.000Z
author: janko-jovanovic
description: >-
  Buttons, whatever their purpose, are important design elements. They could be
  the end point of a Web form or a [call to
  action](https://www.smashingmagazine.com/2009/10/13/call-to-action-buttons-examples-and-best-practices/).
  Designers have many reasons to style buttons, including to make them more
  attractive and to enhance usability. One of the most important reasons,
  though, is that standard buttons can **easily be missed by users** because
  they often look similar to elements in their operating system. Here, we
  present you several techniques and tutorials to help you learn how to style
  buttons using CSS. We'll also address usability.

  Before we explain how to style buttons, let's clear up a common misconception:
  buttons are not links. The main purpose of a link is to navigate between pages
  and views, whereas buttons allow you to perform an action (such as submit a
  form).
categories:
  - Coding
  - Buttons
  - CSS
  - Techniques
  - Essentials
---
Buttons, whatever their purpose, are important design elements. They could be the end point of a Web form or a <a href="/2009/10/13/call-to-action-buttons-examples-and-best-practices/">call to action</a>. Designers have many reasons to style buttons, including to make them more attractive and to enhance usability. One of the most important reasons, though, is that standard buttons can <strong>easily be missed by users</strong> because they often look similar to elements in their operating system. Here, we present you several techniques and tutorials to help you learn how to style buttons using CSS. We'll also address usability.

You may want to take a look at the following related posts:

*   [Pushing Your Buttons With Practical CSS3](https://www.smashingmagazine.com/2009/12/pushing-your-buttons-with-practical-css3/)
*   [Mastering CSS, Part 1: Styling Design Elements](https://www.smashingmagazine.com/2009/08/mastering-css-styling-design-elements/)
*   [Designing “Read More” And “Continue Reading” Links](https://www.smashingmagazine.com/2009/07/designing-read-more-and-continue-reading-links/)
*   [Web Design Elements: Examples And Best Practices](https://www.smashingmagazine.com/web-design-essentials-examples-and-best-practices/)

## Links vs. buttons

Before we explain how to style buttons, let's clear up a common misconception: buttons are not links. The main purpose of a link is to navigate between pages and views, whereas buttons allow you to perform an action (such as submit a form).

{{% feature-panel %}}

In one of his articles, Jakob Nielsen writes about <a href="https://www.useit.com/alertbox/command-links.html" rel="nofollow">command links</a>, which are a blend of links and buttons. But he recommended that command links be limited to actions with minor consequences and to secondary commands. To learn more about primary and secondary commands (and actions), check out <a href="https://www.lukew.com/resources/articles/PSactions.asp" rel="nofollow">Primary and Secondary Actions in Web Forms</a> by Luke Wroblewski. To learn more about the differences between links and buttons, read <a href="https://www.uxbooth.com/blog/creating-usable-links-and-buttons/" rel="nofollow">Creating Usable Links and Buttons</a> at UXBooth.</p>

## Basic Styling

The simplest way to style links and buttons is to add background color, padding and borders. Below are examples of the code for the link, <code>button</code> and <code>input</code> ("Submit") elements.

<pre><code class="language-markup tmp-xml">&lt;a class="button" href="#"&gt;Sample button&lt;/a&gt;
  &lt;button class="button" id="save"&gt;Sample button&lt;/button&gt;
  &lt;input class="button" value="Sample Button" type="submit" /&gt;</code></pre>

<pre><code class="language-markup tmp-xml">.button {
  padding:5px;
  background-color: #dcdcdc;
  border: 1px solid #666;
  color:#000;
  text-decoration:none;
}</code></pre>

This simple code minimizes the visual differences between links and buttons. And here are the rendered examples of the code above:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f834ebde-4fb7-41fb-92ec-de6c28459222/different-buttons.jpg" alt="Screenshot" width="372" height="68" /></figure>

The important thing to note is that these three elements <strong>render differently with the same CSS</strong>. So, you should style these elements carefully to ensure consistency across your website or application.</p>

### Images

Adding images to buttons can make the buttons more obvious. Sometimes the image itself clearly <strong>communicates the purpose of a button</strong>; e.g. a loupe icon for searching or a floppy disk icon for saving. The easiest way to add an image to a button is to use a background image and then position it accordingly. Below are our examples with a checkmark icon.

<pre><code class="language-markup tmp-xml">.button {
  padding: 5px 5px 5px 25px;
  border: 1px solid #666;
  color:#000;
  text-decoration:none;
  background: #dcdcdc url(icon.png) no-repeat scroll 5px center;
}</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de6cbd22-2c40-4419-92a8-d4883b5ad31b/different-buttons2.jpg" alt="Screenshot" width="484" height="64" /></figure>

### Button States

In addition to their default state, buttons and links can have two other states: hover and active (i.e. pressed). It is important that buttons appear different in different states so that users are clear about what is happening. Any element in a hover state can be styled by invoking the <code>:hover</code> CSS pseudo-class.

<pre><code class="language-css">a:hover {
  color:#f00;
}</code></pre>

Though very important, the active state is rarely implemented on websites. By showing this state, you ensure that your buttons are responsive and send a visual cue to users that a button has been pressed. This is called <strong>isomorphic correspondence</strong>, and it is "the relationship between the appearance of a visual form and a comparable human behavior" (Luke Wroblewski, Site-Seeing). The article <a href="https://www.usabilitypost.com/2008/12/16/pressed-button-state-with-css/" rel="nofollow">Pressed Button State With CSS</a> elaborates on the importance of the active state.

<pre><code class="language-css">a:active {
  color:#f00;
}</code></pre>

There is yet one more state, one that is seen when navigating with the keyboard: the focus state. When the user navigates to a button using the Tab key, it should change appearance, preferably to have the same appearance as the hover state.

<pre><code class="language-css">a:focus {
  color:#f00;
}</code></pre>

The examples below shows the common way to style button states. The hover state is a bit lighter than the normal state, while the active state has an inverted gradient that simulates a pressed action. Although you need not limit yourself to this styling, it is a good place to start.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d10a05a-d5af-450d-be04-0064cb54f149/button-states.png" alt="Screenshot" width="462" height="52" /></figure>

We should talk about how to handle the outline property for the <code>:active</code> and <code>:focus</code> states. Handling this property well is important for the experience of users who employ the keyboard as well as the mouse. In the article Better CSS Outline Suppression," Patrick Lauke shows how buttons and links behave in different combinations of states and explains why the outline property should be invoked only with the <code>:active</code> state.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef758962-dc6c-4b5d-a508-466b2cbb1cef/apple.jpg" alt="Screenshot" width="500" height="245" /></figure>

The blue "Buy now" button on <a href="https://www.apple.com" rel="nofollow">Apple.com</a> has a slightly lighter background for the hover state and an inset style for active state. Even the main navigation button on Apple's website implements all three states.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/819395ea-ee57-49a7-9308-66fdd157d14a/tearoundapp.jpg" alt="Screenshot" width="500" height="188" /></figure>

Although it doesn't implement the active state, this fancy button on <a href="https://tearoundapp.com/" rel="nofollow">Tea Round</a> has a nice fading effect on hover.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a12ef36d-517e-4664-8707-ab868e26ad78/uxbooth-button.png" alt="Screenshot" width="500" height="250" /></figure>

The "Read more" button on <a href="https://www.uxbooth.com/" rel="nofollow">UX Booth</a> turns green on hover and moves down one pixel in the active state, which simulates the effect of pressing a button.</p>

### Useful Reading

The article <a href="https://particletree.com/features/rediscovering-the-button-element/" rel="nofollow">Rediscovering the Button Element</a> shows the differences between links and buttons and explains how to style buttons easily.

<figure><a href="https://particletree.com/features/rediscovering-the-button-element/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc9d16aa-1dc1-4b48-92cb-7529e7a4771b/rediscover-button.jpg" alt="Screenshot" width="370" height="88" /></a></figure>

<a href="https://www.tyssendesign.com.au/articles/css/styling-form-buttons/" rel="nofollow">Styling Form Buttons</a> covers the basics of styling buttons, with many examples.

<figure><a href="https://www.tyssendesign.com.au/articles/css/styling-form-buttons/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19d354ce-c3f5-4e8d-bba9-194b8418176c/tyssendesign.jpg" alt="Screenshot" width="450" height="230" /></a></figure>

<span class="removed_link" title="https://woork.blogspot.com/2008/06/beautiful-css-buttons-with-icon-set.html">Beautiful CSS Buttons With Icon Set</span> shows how to style buttons using background images. Although not scalable, these are really nice buttons.

<figure><span class="removed_link" title="https://woork.blogspot.com/2008/06/beautiful-css-buttons-with-icon-set.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5381b912-941b-4e5b-94cc-7d5900cd489b/buttonnice.gif" alt="Screenshot" width="420" height="150" /></span></figure>

<a href="https://stopdesign.com/archive/2009/02/04/recreating-the-button.html" rel="nofollow">Recreating the Button</a> is a very good article that explains how Google ended up with the buttons that it uses on majority of its websites.

<figure><a href="https://stopdesign.com/archive/2009/02/04/recreating-the-button.html" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0db3f8c-4923-439f-b2db-a61042ab9cb5/stopdesign.jpg" alt="Screenshot" width="450" height="232" /></a></figure>

<a href="https://monc.se/kitchen/59/scalable-css-buttons-using-png-and-background-colors/" rel="nofollow">Scalable CSS Buttons Using PNG and Background Colors</a> explains how to create really stunning buttons for all states. Although it uses jQuery, it degrades gracefully if JavaScript is turned off.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/516a9864-1e16-475d-9705-46dff064a580/monc.jpg" alt="Screenshot" width="450" height="230" /></figure>

## Sliding Doors: Flexible Buttons

One important consideration needs to be made when styling buttons: scalability. Scalability in this context means being able to stretch a button to fit text and to reuse images. Unless you want to create a different image for each button, consider the "sliding doors" technique. This technique enables you to create scalable, rich buttons.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d12f82-092e-4900-8019-8797f7b5952e/sliding-doors.png" alt="Screenshot" width="500" height="198" /></figure>

The principle involves making <strong>two images slide over each other, allowing the button to stretch to the content</strong>. Usually, this is done by nesting a span element within a link. As shown in the image above, each element has its own background image, allowing for the sliding effect. The two code snippets below show the structure and basic styling for this effect.

<pre><code class="language-markup tmp-xml">&lt;a href="#"&gt;&lt;span&gt;Typical sliding doors button&lt;/span&gt;&lt;/a&gt;</code></pre>

<pre><code class="language-css">a {
  background: transparent url('button_right.png') no-repeat scroll top right;
  display: block;
  float: left;
  /* padding, margins and other styles here */
}
a span {
  background: transparent url('button_left.png') no-repeat;
  display: block;
  /* padding, margins and other styles here */
}</code></pre>

The advantages of this technique are that it:

*   Is an easy way to create visually rich buttons;
*   Ensures accessibility, flexibility and scalability;
*   Requires no JavaScript;
*   Works in all major browsers.</p>

### Useful Reading

The "Sliding Doors of CSS" article on A List Apart (<a href="https://www.alistapart.com/articles/slidingdoors/" rel="nofollow">part 1</a> and <a href="https://www.alistapart.com/articles/slidingdoors2/" rel="nofollow">part 2</a>) covers the basics of this technique. Although a bit old, these articles are a must-read for every Web developer.

<figure><a href="https://www.alistapart.com/articles/slidingdoors/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18c41105-8b5c-49f3-ab33-cf61509182f5/alistapart.jpg" alt="Screenshot" width="450" height="230" /></a></figure>

Also a bit old, <a href="https://www.456bereastreet.com/archive/200705/creating_bulletproof_graphic_link_buttons_with_css/" rel="nofollow">Creating Bulletproof Graphic Link Buttons With CSS</a> is an excellent article that shows how to create bulletproof, resizable, shrunk-wrap buttons. Also a must-read.

<figure><a href="https://www.456bereastreet.com/archive/200705/creating_bulletproof_graphic_link_buttons_with_css/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d8b13a6-93df-4ddd-9dba-60c1e4155ccf/456bereast.jpg" alt="Screenshot" width="450" height="228" /></a></figure>

Filament Group has a variety of excellent articles and tutorials. Its second article on CSS buttons, Styling the Button Element With CSS Sliding Doors," explains how to create buttons by combining techniques. Although it doesn't support the active state, it can be easily extended.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a189e1c3-2fab-492e-9448-9acd9dc22240/filament.jpg" alt="Screenshot" width="450" height="230" /></figure>

If you want Wii-like buttons, the article <a href="https://www.hedgerwow.com/360/dhtml/css-round-button/demo.php" rel="nofollow">Simple Round CSS Links (Wii Buttons)</a> provides all the necessary resources and explanation on how to style them.

<figure><a href="https://www.hedgerwow.com/360/dhtml/css-round-button/demo.php" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f13e1c11-3b98-4c43-abfb-118d1934cc1f/wii.jpg" alt="Screenshot" width="450" height="230" /></a></figure>

The common way to achieve the CSS sliding doors technique is to use two images. However, the article <a href="https://kailoon.com/css-sliding-door-using-only-1-image/" rel="nofollow">CSS Sliding Door Using Only One Image</a> shows that it is possible to achieve the same effect with only one image.

<figure><a href="https://kailoon.com/css-sliding-door-using-only-1-image/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21fc035c-4fcc-47b3-9829-d62335e1811e/kailoon.jpg" alt="Screenshot" width="450" height="230" /></a></figure>

<a href="https://www.dynamicdrive.com/style/csslibrary/item/css_oval_buttons/" rel="nofollow">CSS Oval Buttons</a> and <a href="https://www.dynamicdrive.com/style/csslibrary/item/css_square_buttons/" rel="nofollow">CSS Square Buttons</a> from Dynamic Drive are two other articles that show the effectiveness of CSS sliding doors.

<figure><a href="https://www.dynamicdrive.com/style/csslibrary/item/css_oval_buttons/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19d8894c-ee1c-4ad4-b645-a63a0e7044dd/dynamicdrive.jpg" alt="Screenshot" width="450" height="232" /></a></figure>

## CSS Sprites: One Image, Not Many

With CSS Sprites, <strong>one image file contains multiple graphic elements</strong>, usually laid out in a grid. By tiling the image, we show only one Sprite at a time. For buttons, we can include graphics for all three states in a single file. This technique is efficient because it requires fewer resources and the page loads faster. We all know that many requests to the server for multiple small resources can take a long time. This is why CSS Sprites are so handy. They significantly reduces round-trips to the server. They are so powerful that some developers use CSS Sprites for all their graphics. The <a href="https://css-tricks.com/holy-sprites/" rel="nofollow">Holy Sprites</a> round-up on CSS Tricks offers some very creative solutions.

The example below shows the simplest use of CSS Sprites. A single image contains graphics for all three button states. By adjusting the <code>background-position</code> property, we define the exact position of the background image we want. The image we're choosing to show here corresponds to a background position of <code>top: -30px</code> and <code>left: 0</code>.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/516a86e0-c15c-4fde-b46e-d9ae58c6e5ae/sprites.png" alt="Screenshot" width="450" height="184" /></figure>

<pre><code class="language-css">a {
  background: white url(buttons.png) 0px 0px no-repeat;
}
a:hover {
  background-position: -30px 0px;
}
a:active {
  background-position: -60px 0px;
}</code></pre>

For general information and resources on CSS Sprites, check out <a title="The Mystery Of CSS Sprites: Techniques, Tools And Tutorials" href="/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/" rel="bookmark">The Mystery of CSS Sprites: Techniques, Tools and Tutorials</a>."

### Useful Reading

In this easy-to-follow tutorial <a href="https://line25.com/tutorials/how-to-build-a-simple-button-with-css-image-sprites" rel="nofollow">How to Build a Simple Button with CSS Image Sprites</a>," Chris Spooner explains how to create a CSS Sprites image in Photoshop and use it with CSS.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afe137f4-b169-48ca-b154-c2679946eeae/line25.jpg" alt="Screenshot" width="450" height="250" /></figure>

Transforming the Button Element With Sliding Doors and Image Sprites shows how to enrich a button element with a combination of sliding doors and image Sprites. It implements the active state in a very interesting way, not by using different images or colors but rather by positioning.</p>

## CSS 3: Buttons Of The Future

CSS 3 allows us to create visually rich buttons with just a few lines of code. So far, this is the easiest way to create buttons. The downside of CSS 3 is that it is currently supported only by Firefox and Safari. The upside is that buttons styled with CSS 3 <strong>degrade gracefully in unsupported browsers</strong>. By using the browser-specific properties <code>-moz-border-radius</code> (for Firefox) or <code>-webkit-border-radius</code> (for Safari), you can define the radius of corners. Here are a few examples of what can be done with the border radius property.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c970389f-3fa9-47fb-8661-c101d30ac2e8/css3-rounded.png" alt="Screenshot" width="495" height="285" /></figure>

For better results, you can combine CSS 3 rounded corners with the background image property. The example below shows a typical button with a gradient image, the first without rounded corners, and the second with.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91f7f9fb-d78e-410b-bbcb-9ed9292c233f/rounded-corners.png" alt="Screenshot" width="500" height="190" /></figure>

Compared to sliding doors, this technique is far simpler. However, if you want to maintain visual consistency across all browsers, then use sliding doors, because it works in all major browsers, including IE6. To learn more about the capabilities of CSS 3, read CSS 3 Exciting Functions and Features: 30+ Useful Tutorials." And here are a few good tutorials on styling buttons with CSS 3 features.</p>

### Useful Reading

<a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba" rel="nofollow">Super Awesome Buttons With CSS 3 and RGBA</a> shows the power of CSS 3 with rounded corners, Mozilla box shadows and RGBA, which is a color mode that adds alpha-blending to your favorite CSS properties. This is one of the best examples of CSS 3 buttons.

<figure><a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20659536-7ad4-4719-b4a9-bc0f60b8b613/zurb.jpg" alt="Screenshot" width="450" height="230" /></a></figure>

<a href="https://my.opera.com/dstorey/blog/show.dml/717521" rel="nofollow">Creating buttons without Images Using CSS 3</a> explains the drawbacks of using images for buttons and shows several options for creating image-less CSS 3 buttons.

<figure><a href="https://my.opera.com/dstorey/blog/show.dml/717521" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8cf4994-6f7c-4052-b2fb-053339dbe18a/opera.png" alt="Screenshot" width="410" height="188" /></a></figure>

## Instant Tools: Are They Useful?

Tools exist for creating buttons, such as <a href="https://www.blumentals.net/buttonmenumaker/" rel="nofollow">Easy Button and Menu Maker</a> and <a href="https://www.mycoolbutton.com/" rel="nofollow">My Cool Button</a>, and for creating CSS Sprites, such as <a href="https://spritegen.website-performance.org/" rel="nofollow">CSS Sprite Generator</a>, but the question is, do they really help you create buttons that fit your needs. Although they are configurable and easy to use, your creativity and control over the results are limited, which makes for average-looking buttons. Using one-size-fits-all buttons is not a good idea.

The solution is to use Photoshop (or a <a href="https://sixrevisions.com/graphics-design/10-excellent-open-source-and-free-alternatives-to-photoshop/" rel="nofollow">free alternative</a>) and the proven techniques described in this article. If you are a beginner with Photoshop, here are several excellent tutorials on creating amazing buttons.

If you don't know where to start, <a href="https://yesterdayishere.com/now/log/iphone-like-button-in-photoshop/" rel="nofollow">iPhone-Like Button in Photoshop</a> is the perfect choice. In only 10 to 15 minutes, you will be able to create the kind of buttons seen on the iPhone.

<figure><a href="https://yesterdayishere.com/now/log/iphone-like-button-in-photoshop/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2888b3aa-3aea-4a06-a4b4-785f42a3aba1/iphone-button.png" alt="Screenshot" width="300" height="100" /></a></figure>

<a title="Permanent Link to How to Create a Slick and Clean Button in Photoshop" href="https://sixrevisions.com/tutorials/photoshop-tutorials/how-to-create-a-slick-and-clean-button-in-photoshop/" rel="bookmark">How to Create a Slick and Clean Button in Photoshop</a> is a very detailed tutorial that guides you through 30 simple steps and helps you learn the Photoshop basics. In addition, the article explains how to use these graphics in combination with HTML and CSS to create fully functional CSS buttons.

<figure><a title="Permanent Link to How to Create a Slick and Clean Button in Photoshop" href="https://sixrevisions.com/tutorials/photoshop-tutorials/how-to-create-a-slick-and-clean-button-in-photoshop/" rel="bookmark"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6fca7e7-3c5a-4c1b-a143-13cad3e57c3e/sixrevisions.png" alt="Screenshot" width="500" height="130" /></a></figure>

## Buttons And Usability: Instead Of Conclusion

The techniques described above can help you create stunning buttons. However, because they play a critical role in website usability, the buttons should meet some key principles:

1.  First consider the labeling. Always **label buttons with the name of the action that the user is performing**. And always make it a [verb](https://www.usabilitypost.com/2008/08/30/usability-tip-use-verbs-as-labels-on-buttons/). A common mistake is to label buttons "Go" for various actions such as searching, sending email and saving. Labels should also be short and to the point; no need to clutter the user interface.
2.  As mentioned, include all button states (default, hover, active) to provide clear visual cues to the user as to what is happening. Button outlines should remain in the active state only.
3.  Clearly distinguish between **primary and secondary actions**. The most important action should be the most prominent. This is usually done by giving primary and secondary actions different colors.
4.  Pay close attention to **consistency**. Buttons should be consistent throughout a Web application, both visually and behavior-wise. Use CSS sliding doors for reused buttons or CSS 3 rounded corners to maintain consistency.
5.  Though obvious, we should note that the entire button area should be clickable.

<a href="https://www.uxbooth.com/blog/creating-usable-links-and-buttons/" rel="nofollow">Creating Usable Links and Buttons</a> explains why users expect buttons sometimes and links other times. It also shows how to choose between the two elements.

<figure><a href="https://www.uxbooth.com/blog/creating-usable-links-and-buttons/" rel="nofollow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c71b0484-1168-462f-944a-2fea78476de0/uxbooth.jpg" alt="Screenshot" width="450" height="235" /></a></figure>

<a href="https://inspectelement.com/tutorials/how-to-design-buttons-to-help-improve-usability/" rel="nofollow">How to Design Buttons to Help Improve Usability</a> explains some usability principles that should be considered when designing buttons. It covers the basics of icon usage, appearance, behavior, hierarchy and consistency.

{{< signature "al" >}}

