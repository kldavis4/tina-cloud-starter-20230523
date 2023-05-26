---
title: 10 Useful CSS/JS-Coding Solutions For Web-Developers
slug: 10-useful-cssjs-coding-solutions-for-web-developers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ddcf962-843a-4b14-aa83-385b8c22e078/pencils-illu101.jpg
date: 2009-07-06T17:53:25.000Z
author: justin-johnson
description: >-
  Often creative and truly **remarkable design solutions** remain unknown because we, designers, simply overlook them. Being busy with our own projects, we sometimes try to grasp the intuition behind (probably) complex and cluttered code of other designers to understand how they manage to implement particular design ideas. In fact, by just observing the code of other developers we can learn a lot from them; we can find interesting ideas and improve the quality of our work.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
---
Over the last months we've been paying closer attention to interesting design techniques and coding solutions and tried to understand how each of these solutions work and how they can benefit other designers and developers. Such designs are often hard to find, so it would be great if you could suggest some solutions that are worth exploring in detail – we'll certainly cover them in our next posts!

So let's take a closer look at **10 useful CSS & Javascript techniques and coding solutions** that can turn out to be useful for your next project. You should have at least a basic knowledge of CSS and JavaScript before you read the entire article.

{{% feature-panel %}}

## 1\. Inline Content Imagery

When viewing a blog post or an online article, we typically tend to find that most images which are "dropped" into the story's actual content are often presented in a boring or bland manner.

<p>However, it is actually quite easy to create <strong>attractive content imagery</strong> that maintains a strong sense of design and branding, yet still manages to flow naturally with the content of your site. UXBooth provides a clean and elegant example of this technique (scroll down until you see a silverback). In the screenshot below, notice how the <a href="https://silverbackapp.com/">Silverback</a>'s image sits naturally in-line and in flow with the content on the page.

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6e391f0-28a4-442b-b0b8-4e6be198c42d/silv.gif" width="450" height="330" alt="UxBooth Silverback" /><br /> <em>UxBooth's Inline Content Imagery in Action</em></p>

### How Is It Done?
<p>At the first glance the silverback looks like a background image that has been positioned in the center of the content column with CSS or JavaScript (or a combination of the two); however, this is a pure CSS solution. A div wrapping the image of the silverback (a simple .png-image) is floated to the right. Immediately after that in the HTML comes a paragraph and an ordered list. The "silverback"-div has a left-margin of 47px which keeps the p tag and the ol tag's content from overlapping the image, thus providing good visual spacing and overall page flow.</p>

<p><strong>HTML</strong></p>

<pre><code class="language-markup tmp-html">&lt;h3&gt;Contest Details&lt;/h3&gt;

&lt;div class="imagery""&gt;
  &lt;img src="imagery.png" width="205" height="400" alt="Imagery" /&gt;
&lt;/div&gt;

&lt;p&gt;...the introductory paragraph...&lt;/p&gt;

&lt;ol>
  &lt;li&gt;...various bullet points went here...&lt;/li&gt;
&lt;/ol&gt;</code></pre>

<p><strong>CSS</strong></p>

<pre><code class="language-css">.imagery {

 /* The image is floated to the right */
  width: 205px;
  float: right;

 /* The image is positioned precisely, 
    by pushing it 20px from the right border */
  margin-right: -20px;

/* The image is pushed away from the text
    (to the right) with a left margin of 47px */
  margin-left: 47px;
}</code></pre>

## 2. Typographic Tricks
<p> CommandShift3, self proclaimed hot-or-not of websites, uses an interesting typographic trick to display the vote results for each website in which you have submitted a vote. Obviously, this effect is achieved using only CSS.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb0b938d-f00e-46a0-9b21-2cb75e7a2b5b/blt.gif" width="520" height="330" alt="Typographic Percentages" /><br /> <em>Nice typographic effects to show percentages of votes</em></p>

### How Is It Done?
<p>Each result line contains a "winning percentage"-div + screenshot as well as a "losing percentage"-div + screenshot (the image below should make it clear what is meant here). Each of the percentages blocks is given a width that is slightly smaller than the width it needs to display its full text. Besides, the CSS attribute <em>overflow:hidden</em> is applied to hide the content that is not needed.</p>
<p>This is all the code necessary for the "winning percentage"-div. The "losing percentage"-div gets the same bit of code with the addition of a negative margin to make it appear to slide behind the losing site's thumbnail. </p>
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0838bf0b-3395-4b52-95f0-e5bf79674197/expl.gif" width="450" height="243" alt="Typographic Percentages" /></p>

<strong>HTML</strong>

<pre><code class="language-markup tmp-html">&lt;div class="bar"&gt; 
  &lt;div class="screen-left loser choice"&gt;
  &lt;div class="pct"&gt;
    &lt;div&gt;46&lt;span&gt;%&lt;/span&gt;&lt;/div&gt;
    &lt;/div&gt;
    &lt;div&gt;
      --the image goes here--
    &lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="screen-right winner"&gt;
  &lt;div&gt;
    --the image goes here--
  &lt;/div&gt;
    &lt;div class="pct"&gt;
      &lt;div&gt;54&lt;span&gt;%&lt;/span&gt;&lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;div class="legend"&gt;
      --You voted for text goes here--
     &lt;/div&gt;
&lt;/div&gt;</code></pre>

<strong>CSS</strong>

<pre><code class="language-css">.result .pct {
  float:left;
  height:80px;
  margin:0;
  overflow:hidden;
  padding:0;
  white-space:nowrap;
  width:95px;
  }
.result .screen-left .pct div {
  margin:28px 0 0 10px;
  float: left;
  }
.result .loser .pct div {
  color:#84C3FF;
  } 
.result .pct div span {
  display:inline;
  font-size:55px;
  }
.result .screen-right .pct div {
  margin:28px 0 0 -8px;
  float: left;
  }
.result-first .pct div {
  color:#FFFFFF;
  }</code></pre>

## 3. Inline Informational Overlays
<p>This <a href="https://www.31three.com/projects/myfamily/home/home3a.html">31three.com version of myfamily.com</a> has an interesting use of icons sprinkled throughout the body text. If you roll over the calendar icon an informational overlay (very similar to a tooltip) is displayed &ndash; the latter one shows a graphic of what your potential calendar would look like when you sign up with myfamily.com. Notice the transparency effect and the arrow on the left side of the appearing block.</p>
<p><a href="https://www.31three.com/projects/myfamily/home/home3a.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d6a8aba-8cf9-4536-a1c0-a0839cb6f65f/event.gif" width="450" height="330" alt="My Family Overlay" /></a></p>
### How Is It Done?
<p>When a user mouses over the calendar icon, JavaScript is used to show a hidden div that contains a <a href="https://www.31three.com/projects/myfamily/home/img/event_hover.png">transparent .png-image</a>. When your mouse moves away from the calendar icon, the div is hidden again. This particular example doesn't use a JavaScript framework like jQuery or Prototype, instead it uses two custom functions to hide and show the div accordingly.</p>
<p>Please notice that this code does not adher to good coding practices as it does not separate JavaScript functionality from the styling of the site. You should <strong>never include Javascript events as inline attributes</strong> and this example is rather a quick prototype. It is better to encapsulate the JavaScript code in a single .js-file and embed it on your web page using the &lt;script&gt;-tag. Read more in our article <a href="https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/">jQuery: Examples and Best Practices</a>.</p> 

<p><strong>HTML</strong></p>

<pre><code class="language-php">&lt;div id="hover" onmouseover="showLayer('image')" onmouseout="hideLayer('image')"&gt;&nbsp;&lt;/div&gt;

&lt;div id="image" style="visibility: hidden;">
  &lt;img src="img/event_hover.png" alt="image" height="" width=""&gt;
&lt;/div&gt;</code></pre>

<p><strong>Javascript</strong></p>

<pre><code class="language-javascript">function showLayer(layerName, shadowLayerName)
{
    if (document.getElementById) // Netscape 6 and IE 5+
    {
        var targetElement = document.getElementById(layerName);
        targetElement.style.visibility = 'visible';
    }
}

function hideLayer(layerName)
{
   if (document.getElementById) 
   {
       var targetElement = document.getElementById(layerName);
       targetElement.style.visibility = 'hidden';
   }
}</code></pre>

## 4. Product Highlighting
<p><a href="https://basecamphq.com/signup">Basecamp</a>, a 37signals product, chooses to <strong>highlight its most popular product plan</strong> in order to draw attention to it and hopefully create more conversions of visitors to customers. The featured product plan also has the added bonus of <strong>Javascript tooltips</strong> to offer more detail to the highlighted product features. Please notice that each link has its own tooltip that appears on the right hand side when a text link is hovered.</p>
<p><a href="https://basecamphq.com/signup"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc0f042d-3500-464d-8c36-e34b7dd0320d/basecamp.gif" width="450" height="330" alt="Featured Product Plans for Basecamp" /></a><br/><em>Featured Product Plans for Basecamp</em></p>
### How Is It Done?
<p>The team at 37signals choose to use <strong>Prototype.js and CSS to achieve the tooltip effect</strong>, while relying on pure CSS to highlight the featured product plan. Each of the plans resides in its own div, with a class "short"; the highlighted plan replaces the short class with a class "tall".</p>
<p>The divs to the left and right of the highlighted plan have additional CSS classes added to them to provide shadows on their left and right hand sides to give the appearance that the featured plan is rising off the page. The Javascript, written using <a href="https://www.prototypejs.org/">prototype.js</a>, listens for each of the product features to be hovered over. When a feature is hovered over, the tooltips are all hidden, and then the appropriate tooltip is shown.</p>

<p><a href="https://basecamphq.com/signup"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efdb24f1-be0b-402c-b4ad-e8cce323aeaf/basecamp2.jpg" width="450" height="300" alt="Featured Product Plans for Basecamp with Tooltip" /></a><br/><em>Product Plan Tooltips in Action</em></p>

<p><strong>HTML (for the highlighted plan)</strong></p>

<pre><code class="language-css">&lt;div class="tall"&gt;
         &lt;h1&gt;&lt;a href="https://signup.projectpath.com/signup/Plus"&gt;Plus&lt;/a&gt;&lt;/h1&gt;
         &lt;h2&gt;$49/month&lt;/h2&gt;

         &lt;h3&gt;Most popular plan&lt;/h3&gt;
         &lt;ul class="highlight" style="margin-top: 12px;"&gt;
           &lt;li&gt;
             &lt;a href="#" onclick="return false" class="hover_target" hover_container="users_bubble"&gt;&lt;strong&gt;35&lt;/strong&gt; projects&lt;/a&gt;
             &lt;span class="hover_container" id="users_bubble"&gt;
               &lt;div class="bubble hover_target"&gt;&lt;div class="wrapper"&gt;&lt;div class="content"&gt;&lt;div class="inner"&gt;
                 &lt;div class="arrow"&gt;&lt;/div&gt;

                 &lt;h2&gt;What are active projects?&lt;/h2&gt;
                 &lt;p&gt;..Content for the tool tip...&lt;/p&gt;
               &lt;/div&gt;&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;
             &lt;/span&gt;

           &lt;/li&gt;
          ...code repeats for all product bullet points...
         &lt;/ul&gt;

         &lt;a href="https://signup.projectpath.com/signup/Plus" onClick="return ConversionCount()"&gt;&lt;img src="https://www.smashingmagazine.com/images/btn_signupchart_large.png" width="113" height="45" alt="Sign Up" /&gt;</a>
       &lt;/div&gt;</code></pre>

**CSS**

<pre><code class="language-css">body.signup4 div.tall {
  background-color:#FFFFFF;
  border:3px solid #3671A1;
  float:left;
  font-family:helvetica,arial,sans-serif;
  height:310px;
  padding:8px 10px 10px;
  text-align:center;
  width:220px;
}
body.signup4 div.tall h1, body.signup4 div.tall h1 a {
  color:#000000;
  font-size:42px;
  line-height:1em;
  margin:0;
  padding:0;
  text-decoration:none;
}
body.signup4 div.tall h2 {
  color:#000000;
  font-size:24px;
  font-weight:normal;
  margin:0 0 2px;
  padding:0;
}
body.signup4 div.tall h3 {
  border-bottom:1px solid #CCCCCC;
  color:#4582B5;
  font-size:16px;
  font-weight:bold;
  margin:0;
  padding:0 0 4px text-transform:uppercase;
} 
body.signup4 a.hover_target {
  border-bottom:1px dotted #888888;
  color:#64503F;
  margin-left:6px;
  text-decoration:none;
}
body.signup4 div.tall li strong, body.signup4 div.short li strong {
  color:#C33700;
}</code></pre>

<strong>Javascript</strong>

37Signals created a custom class HoverObserver (see the .js-snippet) that uses the functionality from prototype.js. Note that there are other ways to achieve this same effect.

</pre>

## 5\. Sliding Menus

The portfolio section at [Clear Focus Designs](https://clearfocusdesigns.com/work/) contains a nice menu on the right hand side of the page that follows you as you scroll down. This **sliding menu with JQuery and CSS** is an effective way to display a long list of information and still present a constant navigation choice to website visitors.

[![Sliding Menu Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3b5c54c-ff26-4bbb-9af6-ee30c722f8fc/vision.gif)](https://clearfocusdesigns.com/work/)  
_This menu detects when the page scrolls and follows it_

### How Is It Done?

This page uses a jQuery plugin called [scrollFollow](https://kitchen.net-perspective.com/open-source/scroll-follow/) which allows a specified div to follow the page as the user scrolls through the page. In the Clear Focus Designs example, the right hand menu is being told by this plugin to follow the page.

**HTML**

<pre><code class="language-markup tmp-html">&lt;ul id="sites"&gt;
        &lt;li&gt;&lt;a href="#copperStone"&gt;CopperStone Partners&lt;br /&gt;
          &lt;span class="projectDesc"&gt;Development&lt;/span&gt;&lt;/a&gt;
  &lt;/li&gt;
        &lt;li&gt;&lt;a href="#vmg"&gt;Visionary Marketing Group&lt;br /&gt;
          &lt;span class="projectDesc">Development&lt;/span&gt;&lt;/a&gt;
  &lt;/li&gt;
  ...code repeats for all menu items...
  &lt;/ui&gt;</code></pre>

**Javascript**

<pre><code class="language-javascript">$( document ).ready( function ()
{ 
  $( '#ourWork' ).scrollFollow(
    {
      speed: 1000,
      easing: 'linear'
    }
  );
}
);</code></pre>

## 6\. Authors "Flagging"

Placing avatars next to an individual's post in a comment thread is quite a common practice. UxBooth (again) **has taken comment flagging a step further** by allowing a user's thumbnail to float outside of his/her comments in the article. This allows a user to quickly scan the page and know who posted a response on that page. UxBooth does approach this method a little differently, as the article is written by several different authors. Using this 'flagging' method helps a user identify which author contributed which part of the article.

![UxBooth Flags](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be560a7-da5b-407b-8996-f98ba7a000f1/wwl.gif)  
_UxBooth's Using comment 'Flags' to show which author wrote the comment_

### How Is It Done?

On UxBooth, each author has his/her own div with a class named after the author. For example, the author, Andrew, has an author div with a class "author andrew". The "author" class sets up the basic styling that is common among all authors comments. The div is placed in the document using the _relative_ positioning within the document's flow.

<p>Inside of the div there is an image with a class of "avatar". The "avatar" class is positioned <em>absolutely</em> within the relatively positioned parent-element (using the classic <a href="https://stopdesign.com/archive/2003/09/03/absolute.html">Making the absolute, relative</a>-CSS-technique</a>). The image is given a top value of 0, with a left value of -54px. Essentially, this technique sucks the image out of the content column and lays it over the container background color/image.

**HTML**

<pre><code class="language-php">&lt;div class="matt review-quote"&gt;
&lt;p&gt;...The user's comment went here...&lt;/p&gt;
&lt;p&gt;&lt;img class="avatar" src="https://www.smashingmagazine.com/images/matt.gif" alt="Matthew Kammerer"&gt;&lt;/p&gt;
&lt;/div&gt;</code></pre>

**CSS**

<pre><code class="language-css">div#ux-booth div#content div.matt.review-quote {
  border-color:#FF9F26;
}
div#ux-booth div#content div.review-quote {
  border-left:6px solid #D8C9A1;
  margin:0 -21px 0 -24px;
  padding:0.5em 21px 1.5em 20px;
  position:relative;
} 
div#ux-booth div#content div.matt.review-quote img.avatar {
  border-color:#CC7200;
}
div#ux-booth div#content div.andrew.review-quote img.avatar{
  -moz-border-radius-bottomleft:9px;
  -moz-border-radius-topleft:9px;
  background:#888888 none repeat scroll 0 0;
  border:4px solid #4B6500;
  left:-54px;
  position:absolute;
  top:0;
}</code></pre>

## 7\. Archive Page Layouts

Warpspire uses a different approach when it comes to the layout of their archive page. Instead of a long list, they've chosen to use a column approach underneath each month in the archive.

![Sliding Menu Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bf5bd82-a1d6-467c-a580-a37a16725a35/feb.gif)

### How Is It Done?

Each entry in the archive contains a `h3`- and a `p`-tag inside of a listed item `li`. Each even numbered `li` is floated to the left, each odd numbered `li` is floated to the right. And that's it – as simple as that.

**HTML**

<pre><code class="language-markup tmp-html">&lt;div class="section-heading-small"&gt;
    &lt;h2&gt;February 09&lt;/h2&gt;
&lt;/div&gt;
&lt;ul class="archives"&gt;
    &lt;li class="odd"&gt;
      &lt;h3&gt;...title of archived article...&lt;/h3&gt;
      &lt;p&gt;...summary and read more link for article...&lt;/p&gt;
    &lt;/li&gt;
    &lt;li&gt;
      &lt;h3&gt;...title of archived article...&lt;/h3&gt;
      &lt;p&gt;...summary and read more link for article...&lt;/p&gt;
    &lt;/li&gt;
&lt;/ul&gt;</code></pre>

**CSS**

<pre><code class="language-css">ul.archives li.odd {
  clear:both;
  float:left;
  padding-right:20px;
}
ul.archives li {
  float:right;
  font-size:11px;
  list-style-type:none;
  margin:0 0 20px;
  padding:0;
  width:270px;
}</code></pre>

## 8\. Transparent Rounded Rollovers

This is an example of another archive layout, this time from Particletree, which uses **transparent pngs as article title rollover backgrounds.**

![Transparent Rollovers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0167d502-36f5-49e3-af02-81eec38dca6c/tree.gif)  
_Transparent Rollovers at ParticleTree_

### How Is It Done?

Each article title is placed inside of a `h3`-element that has an anchor (`a`) inside. The `a` tag has a transparent .png-background image that has its `background-position` shifted on hover as well as a background color.

The .png-image is positioned to the right hand side and sits above the tree image. The background color fills the space between the two, creating the illusion of 3D-dimension (the content block appear to be in front of the "tree"-image). Each link also uses CSS-based rounded corners (using -moz-border-radius).

<strong>HTML</strong>

<pre><code class="language-markup tmp-html">&lt;div class="red headline"&gt;
  &lt;h3&gt;
  The Importance of Design in&nbsp;Business
    &lt;cite&gt;&lt;b&gt;By Chris Campbell&lt;/b&gt; · Comments (&lt;strong&gt;15&lt;/strong&gt;) · August 14th&lt;/cite&gt;
  &lt;/h3&gt;
&lt;/div&gt;
  ...code repeats...</code></pre>

<strong>CSS</strong>

<pre><code class="language-css">#features .red a:hover {
  background-position: 498px -30px;
}
#features .red a:hover{
  background-image:url(/images/fadetree.png);
  background-repeat:no-repeat;
}
#features[id] h3 a {
  height:auto;
  min-height:66px;
}
#features h3 a {
  -moz-border-radius-bottomright:30px;
  -moz-border-radius-topleft:30px;
  font-size:210%;
  height:66px;
  padding:11px 15px 3px 105px;
}
.red a:hover, a.red:hover {
  background:#5E2510 none repeat scroll 0 0;
  color:#FFFFFF;
}
.red a, .red cite strong {
  color:#843418;
}
h3 a {
  display:block;
  text-decoration:none;
}</code></pre>

## 9\. Blending Flash and CSS

[HunterBoot.com](https://www.hunter-boot.com/) has wonderfully constructed black and white imagery on their homepage panel. This imagery is a part of a Flash movie that contains not only the imagery, but also nice hover-effects for the link lists at the bottom of the layout. See the screenshot below for a better understanding of what is going on structurally. When you mouse over one of the links in the four columns below the main image panel, you get a nice animated rollover in the background of that column.

[![Transparent Rollovers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd3bf0f3-aeec-40f7-afdd-35e3ed139696/hunter2.jpg)](https://www.hunter-boot.com)

### How Is It Done?

At first glance it appears that this is some type of jQuery plugin or something similar. However this is a pure CSS-based solution that uses Flash-elements for hover-effects. This technique starts out with some markup. There is a main div that contains the Flash movie (inside a containing div), then four distinct divs, one for each of the sections.

These four divs have a heading and then an unordered list containing the individual links. The main containing div is positioned relatively to its parent. These four URLs are positioned absolutely inside of the relative main container div – this puts the URLs on the top of the Flash movie. When you move your mouse over the four implied columns, this triggers a rollover animation in the Flash movie, because your mouse is actually _over_ the Flash movie. Since the links sit above the Flash you can still click on them with no unfcomfortable side effects.

**HTML**

<pre><code class="language-markup tmp-html">&lt;!-- the flash container --&gt;
  &lt;div id="featurePanelHomeFlashBoxCntr"&gt;
     ...the flash movie is inserted here via SWFObject...
     ...it's important to note that the .swf's wmode is set to transparent...
  &lt;/div&gt;

  &lt;!-- the product category links -- &gt;
  &lt;div class="homeFlashListFun"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href="/product/link/goes/here" &gt;Link Text&lt;/a&gt;&lt;/li&gt;
    ...repeat li's for each link
  &lt;/ul&gt;
  &lt;/div&gt;
  &lt;div class="homeFlashListSport"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href="/product/link/goes/here" &gt;Link Text&lt;/a&gt;&lt;/li&gt;
    ...repeat li's for each link
  &lt;/ul&gt;
  &lt;/div&gt;
  &lt;div class="homeFlashListWork"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href="/product/link/goes/here" &gt;Link Text&lt;/a&gt;&lt;/li&gt;
    ...repeat li's for each link
  &lt;/ul&gt;
  &lt;/div&gt;
  &lt;div class="homeFlashListKids"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href="/product/link/goes/here" &gt;Link Text&lt;/a&gt;&lt;/li&gt;
    ...repeat li's for each link
  &lt;/ul&gt;
  &lt;/div&gt;</code></pre>

**CSS**

<pre><code class="language-css">.featurePanelHomeFlashBox { margin: 0px; padding: 0px; float: left; height: 528px; width: 720px; position: relative; }
#featurePanelHomeFlashBoxCntr { width: 720px; height: 528px; position: absolute; top: 0px; left: 0px; background: #ffffff; z-index: 300; }

---This chunk of CSS is repeated for each of the lists, with the difference being the positioning of the ul---
.homeFlashListFun ul { position: absolute; top: 380px; left: 15px; z-index: 599; width: 100px; background: transparent; list-style: none; list-style-image: none; list-style-type: none; margin: 0px; padding: 10px 0px 0px 0px; }
.homeFlashListFun ul li { margin: 0px; padding: 0px 0px 6px 0px; background: transparent; text-decoration: none; line-height: 1em; }
.homeFlashListFun ul li a { text-decoration: none; color: #999; font-size: 0.95em; letter-spacing: -0.00em; background: transparent; }
.homeFlashListFun ul li a:hover { text-decoration: underline; color: #bf0000; }</code></pre>

## 10\. Popular Tags Graphs

[Ogilvy](https://www.ogilvydurham.com/allTags.php) chooses to display their **popular tags with a graph-like background** (scroll all the way to the bottom to see the "Top 5 Tags").

[![Popular Tags](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/508fbcd5-630e-4d4f-a171-be56dacd76f7/populartags.jpg)](https://www.ogilvydurham.com/allTags.php)

### How Is It Done?

The tag list is a simple unordered list; each list item has an inline style with a hard coded width given to it (not really a good coding solution). This seems like it is coming from a server side calculation and being outputted inline on the element. Oglivy uses PHP, but this could be done in pretty much any server side language, or it could even be done with JavaScript if necessary. Each of the li's has its own background color and because they all have different widths this gives the appearance of a graph.

**HTML**

<pre><code class="language-markup tmp-html">&lt;ol class="transGreen"&gt;
  &lt;li style="width: 242px"&gt;
    &lt;a href="" style="display:block;width:100%;color:#fff" class="tag tag_1"&gt;work&lt;/a&gt;
  &lt;/li&gt;
  &lt;li style="width: 216px">
    &lt;a href="" style="display:block;width:100%;color:#fff" class="tag tag_2"&gt;philosophy&lt;/a&gt;
  &lt;/li&gt;
  &lt;li style="width: 153px">
    &lt;a href="" style="display:block;width:100%;color:#fff" class="tag tag_3"&gt;agency&lt;/a&gt;
  &lt;/li&gt;
  &lt;li style="width: 104px">
    &lt;a href="" style="display:block;width:100%;color:#fff" class="tag tag_4"&gt;culture&lt;/a&gt;
  &lt;/li&gt;
  &lt;li style="width: 77px"&gt;
    &lt;a href="" style="display:block;width:100%;color:#fff" class="tag tag_5"&gt;maslow&lt;/a&gt;
  &lt;/li&gt;
&lt;/ol&gt;</code></pre>

**CSS**

<pre><code class="language-css">#top5 li a.tag {
  padding: 1px 5px;
  margin-bottom: 2px;
  color: #fff;
  text-transform: uppercase;
  font-weight: normal;
}

#top5 li a.tag:hover { background: #000; }

.tag_1 { background: #c12; }
.tag_2 { background: #990000; }
.tag_3 { background: #ee6666; }
.tag_4 { background: #ee2222; }
.tag_5 { background: #cc6666; }</code></pre>

## What coding solutions should we cover next?

Please feel free to suggest interesting, unusual, creative, advanced techniques in the comments to this post! We'll do our best to take a closer look at them and explain them in details in one of our upcoming posts!

## Related posts

You may be interested in the following related posts:

*   [5 Useful Coding Solutions For Designers and Developers](https://www.smashingmagazine.com/2008/08/11/5-useful-coding-solutions-for-designers-and-developers/)
*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/18/7-principles-of-clean-and-optimized-css-code/)
*   [8 Simple Ways to Improve Typography In Your CSS-Designs](https://www.smashingmagazine.com/2009/04/03/8-simple-ways-to-improve-typography-in-your-designs/)
*   [Fixed vs. Fluid vs. Elastic Layout: What’s The Right One For You?](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/)

