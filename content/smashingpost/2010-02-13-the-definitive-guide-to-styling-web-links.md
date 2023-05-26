---
title: The Definitive Guide To Styling Links With CSS
slug: the-definitive-guide-to-styling-web-links
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/748a768a-9e9c-4347-86f1-e008c4865c89/ampersands2.jpg
date: 2010-02-13T12:48:09.000Z
author: lee-munroe
description: >-
  Hyperlinks (or links) connect Web pages. They are what make the Web work,
  enabling us to travel from one page to the next at the click of a button. As Web Standardistas put it, “without hypertext links the Web wouldn't be the Web, it would simply be a collection of separate, unconnected pages.”
categories:
  - SEO
  - Design
  - Web Design
---
So without links, we'd be lost. We look for them on the page when we want to venture further. Sure, we pause to read a bit, but inevitably we end up clicking a link of some sort.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing “Read More” And “Continue Reading” Links](https://www.smashingmagazine.com/2009/07/designing-read-more-and-continue-reading-links/)
*   [Why Your Links Should Never Say “Click Here”](https://www.smashingmagazine.com/2012/06/links-should-never-say-click-here/)
*   [Should Links Open In New Windows?](https://www.smashingmagazine.com/2008/07/should-links-open-in-new-windows/)
*   [A Short Story About “Back To Top” Links](https://www.smashingmagazine.com/2008/11/short-story-about-top-links/)

## Styling Links

When you style links, remember that users don't read; they scan. You've heard that before, and it's true. So, make sure your links are obvious. They should also <strong>indicate where they will take the user</strong>.

{{% feature-panel %}}

Let's start by looking at CSS selectors and pseudo-classes:

*   `a:link { }` Unvisited link.
*   `a:visited { }` Visited links.
*   `a:hover { }` The user mouses over a link.
*   `a:focus { }` The user clicks on a link.
*   `a:active { }` The user has clicked a link.

<figure><a title="The TLC" href="https://www.thetlc.org.uk"><img loading="lazy" decoding="async" class="21237" title="tlc" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4428b72-260d-4a38-a3ed-99abecb36c1f/tlc1.gif" alt="tlc" width="500" height="210" /></a></figure>

<em>The TLC uses not only plaint text links, but also icons to communicate the corresponding file types.</em>

### Ensure Contrast

Links should stand out not only from the background but from the surrounding text. If the font color is black and the link color is black, you have a problem. Make your links stand out by using one or more than one of the following techniques.

*   `text-decoration: underline;` Underline.
*   `font-weight: bold;` Bold.
*   `font-size: 1.4em;` Enlarge.
*   `color: #ed490a;` Color.
*   `background-color: #c0c0c0;` Background.
*   `border-bottom: 2px solid #a959c3;` Border.

If you decide to make links blue, then make sure no other text (including headings) is blue, because users will expect it to be a link, too.

Also, <strong>don't underline text that isn't linked</strong> because users expect underlined text to be a link. And keep in mind <strong>users with poor sight</strong>. Red won't stand out to someone who is color blind, so consider underlining or bolding links, in addition to changing the color.

<figure><img loading="lazy" decoding="async" class="21218" title="komodo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c841091f-9f45-4160-84d0-fb26712a2d7f/komodo.gif" alt="komodo" width="500" height="120" /></figure>

<figure><img loading="lazy" decoding="async" class="21217" title="hicks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ae47c9d-f132-4c4c-a0b6-d606581c698c/hicks.gif" alt="hicks" width="500" height="140" /></figure>

A helpful technique that I always use is to <strong>slightly blur the focus</strong>. Links with good contrast should still stand out when you look at the page.

### Don't Forget About Visited Links

Visited links are often overlooked, but they are very helpful, especially on larger websites. Knowing where they've been before is helpful for users, whether because they want to avoid pages they've visited or to make a point of visiting them again.

<strong>Give visited links a darker shade of color</strong>, so that they stand out but aren't as obvious as unvisited links.

<figure><img loading="lazy" decoding="async" class="21216" title="google" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42c00ce1-d6ad-47e2-9130-5d1c81447a44/google.gif" alt="google" width="500" height="220" /></figure>

<figure><img loading="lazy" decoding="async" class="21215" title="lee" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34914358-f8e1-40ea-bc89-d70328bc901f/lee.gif" alt="lee" width="500" height="90" /></figure>

### Use the Title Attribute

The title attribute is usually overlooked, but it's a convenient way to add descriptions to your links and can be especially useful for those who rely on screen readers.

<pre><code class="language-markup tmp-html">&lt;a href="example.com" title="This is an example link"&gt;Example&lt;/a&gt;</code></pre>

### Use Button Styles

To make really important links stand out—say, <strong>a call to action</strong> or a "More info" link at the bottom—use a button style. And you can reuse the style again and again without having to edit any graphics.

<figure><img loading="lazy" decoding="async" class="21214" title="notable" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d10c81a1-9663-4c07-8ee7-27ff54cf5e2a/notable.gif" alt="notable" width="500" height="130" /></figure>

<figure><img loading="lazy" decoding="async" class="21213" title="ux" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/695201d2-c433-4c87-b8ca-6b53dd76111e/ux.gif" alt="ux" width="500" height="140" /></figure>

For more information, check out "<a title="Super awesome buttons with CSS3 and RGBA tutorial" href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba">Super-Awesome Buttons With CSS3 and RGBA</a>" and "<a title="Call to action button techniques" href="https://www.leemunroe.com/call-to-action-buttons/">Call to Action Buttons</a>."

### Hover State

<strong>Offering feedback to users that they're hovering over a link</strong> is good practice. The best way to do this is to change the background color, change the text color or remove the underline.

<pre><code class="language-css">a:hover { text-decoration:none;
text-shadow: 0 0 2px #999;
}</code></pre>

<figure><img loading="lazy" decoding="async" class="21209" title="adii" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f847de01-da82-49ce-834f-7cbe45025834/adii.gif" alt="adii" width="500" height="101" /></figure>

<figure><img loading="lazy" decoding="async" class="21208" title="cars" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ace32d7-8cbc-497c-b87e-60c0a1fdad8e/cars.gif" alt="cars" width="500" height="90" /></figure>

The mouse pointer usually turns from an arrow into a hand when the user hovers over a link. But this functionality is sometimes lost; for example, in IE when the link contains a <code>span</code> element, or on "Submit" buttons. Fix this by <strong>adding the cursor type</strong> via CSS.

<pre><code class="language-css">a:hover span { cursor: pointer }</code></pre>

### Active State

Provide visual feedback to the user to indicate that they have clicked a link, so that they know to wait. One nice effect is to move the link down one or two pixels, which gives the link the appearance of being pressed.

<pre><code class="language-css">a:active { padding-top: 2px; }</code></pre>

<figure><img loading="lazy" decoding="async" class="21206" title="tim" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40eb791a-1a4c-49ab-8696-3bf8051bc0c7/tim.gif" alt="tim" width="500" height="85" /></figure>

<figure><img loading="lazy" decoding="async" class="21207" title="elliot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/913c82af-f237-4441-bc9e-af5283b8e2bb/elliot.gif" alt="elliot" width="500" height="60" /></figure>

### Apply Padding

Here is a good usability tip. <strong>Add padding to your links</strong>. This way, the user doesn't have to hover over the exact point of the text. Instead, they can hover in proximity and still be able to click. This works well for navigation links.

<pre><code class="language-css">a { padding: 5px; }</code></pre>

<figure><img loading="lazy" decoding="async" class="21235" title="simple" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/980ba1bd-dd1b-4154-8ce7-4b3ffd78f5a6/simple.gif" alt="simple" width="500" height="100" /></figure>

### Use Icons for File Types

If your links point to files in various formats, <strong>inform the user of as much using icons</strong>. This prepares them for the file type they are about to open, whether it's PDF or JPEG, for example.

<figure><img loading="lazy" decoding="async" class="21237" title="tlc" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4428b72-260d-4a38-a3ed-99abecb36c1f/tlc1.gif" alt="tlc" width="500" height="210" /></figure>

For some great resources, check out <a title="Fam Fam Fam icons" href="https://www.famfamfam.com/lab/icons/silk/">Fam Fam Fam Silk Icons</a>.</p>

### Use Icons for Recognition

Just as you would use icons for file types, <strong>use icons to identify where links go</strong> or what they do. This user can more quickly absorb a visual icon than text.

<figure><img loading="lazy" decoding="async" class="21239" title="sam" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d88d643-0d35-427e-bd18-4a57fc5e3eef/sam1.gif" alt="sam" width="300" height="150" /></figure>

<figure><img loading="lazy" decoding="async" class="21247" title="wufoo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/724a3d02-92be-4c33-a0b4-58ccfff0881a/wufoo.gif" alt="wufoo" width="500" height="110" /></figure>

### Make Anchor Text Descriptive

Use meaningful text, not "Click here." The problem with the latter is that it forces the user to read around the link to understand why they should "Click here." Anchor text such as "See Britney on a beach" speaks for itself. It's also more SEO-friendly.

<figure><img loading="lazy" decoding="async" class="21747" title="clickhere" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc2c7960-93a7-492c-b603-b4677f38983a/clickhere.gif" alt="clickhere" width="600" height="143" /></figure>

### Link Your Logo

<strong>Always link your logo to the home page.</strong> Most users expect this convention across the Web. That said, don't assume that users know this. Regular surfers expect it, but a number of users still look for the "Home" link.

<pre><code class="language-markup tmp-html">&lt;h1&gt;&lt;a href="/" title="Homepage"&gt;Site name&lt;/a&gt;&lt;/h1&gt;</code></pre>

<pre><code class="language-css">h1 a {
background: url(images/logo.gif) no-repeat top left;
display: block;
text-indent: -9999px;
width: 200px;
height: 60px;
}</code></pre>

### Don't Open New Windows

Just don't do it. <strong>Let the user decide when and where to open a new tab or window</strong>. <a href="https://www.smashingmagazine.com/2008/07/should-links-open-in-new-windows/">Users expect links to open in the same window</a>. If you really must do it, at least add an icon to show that this will happen. There are exceptions; for example, it you don't want to break the flow of a check-out process.</p>

### Micro-Formats

As the Web becomes more semantic, <strong>consider incorporating <a href="https://www.smashingmagazine.com/2007/05/microformats-what-they-are-and-how-to-use-them/">microformats</a> into your link structures</strong>, to help machines understand how a link fits into a page and its relationship to other pages. For example, the following...

<pre><code class="language-markup tmp-html">&lt;a href="https://myfriend.example.com" rel="friend met"&gt;My Friend&lt;/a&gt;</code></pre>

tells search bots that this text links to a friend who I've met, which is useful for discovering connections between links. You can also <a href="https://www.smashingmagazine.com/2007/05/microformats-what-they-are-and-how-to-use-them/">read more about microformats</a>.</p>

## Further Reading

*   [Padded Link Targets for Better Mousing](https://37signals.com/svn/posts/1048-padded-link-targets-for-better-mousing), 37 Signals
*   [Top Ten Mistakes in Web Design](https://www.useit.com/alertbox/9605.html), Useit
*   [Guidelines for Visualizing Links](https://www.useit.com/alertbox/20040510.html), Useit
*   [Styling Text Links](https://www.andyrutledge.com/styling-text-links.php), Andy Rutledge
*   [Showing Hyperlink Cues With CSS](https://www.askthecssguy.com/2006/12/showing_hyperlink_cues_with_cs_1.html)
*   [Don't Lose Your Focus](https://24ways.org/2009/dont-lose-your-focus)

{{< signature "al" >}}

