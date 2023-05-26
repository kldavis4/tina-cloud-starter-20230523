---
title: Progressive And Responsive Navigation
slug: progressive-and-responsive-navigation
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a02f072-85a4-49ab-b936-f1eba53100e1/prog-resp-nav-13.jpg
date: 2012-02-13T11:47:03.000Z
author: jeremy-hixon
description: >-
  Developing for the Web can be a difficult yet rewarding job. Given the number
  of browsers across the number of platforms, it can sometimes be a bit
  overwhelming. But if we start coding with a little forethought and apply the
  principles of progressive enhancement from the beginning and apply some
  responsive practices at the end, we can easily accommodate for less-capable
  browsers and reward those with modern browsers in both desktop and mobile
  environments.
categories:
  - Coding
  - CSS
  - jQuery
  - HTML5
  - HTML
---
Developing for the Web can be a difficult yet rewarding job. Given the number of browsers across the number of platforms, it can sometimes be a bit overwhelming. But if we start coding with a little forethought and apply the principles of progressive enhancement from the beginning and apply some responsive practices at the end, we can easily accommodate for less-capable browsers and reward those with modern browsers in both desktop and mobile environments.

<img loading="lazy" decoding="async" title="Compass" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a3e15b3-e213-4420-95d2-7a8892492476/compass.jpg" alt="screenshot" width="448" height="268" />

## A Common Structure

Below is the HTML structure of a navigation menu created by WordPress. This unordered list is pretty common for content management systems and hand-coded websites alike. This will be the basis for our work.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Elements Of Navigation + 6 Design Guidelines](https://www.smashingmagazine.com/2012/03/the-elements-of-navigation/)
*   <span>[Responsive Menus: Enhancing Navigation On Mobile Websites](https://www.smashingmagazine.com/2012/06/responsive-menus-enhancing-navigation-on-mobile-websites/)</span>
*   <span>[Can User Experience Be Beautiful? An Analysis Of Navigation In Portfolio Websites](https://www.smashingmagazine.com/2012/03/an-analysis-navigation-portfolio-websites/)</span>
*   <span>[Sticky Menus Are Quicker To Navigate](https://www.smashingmagazine.com/2012/09/sticky-menus-are-quicker-to-navigate/)</span>

{{% feature-panel %}}

<strong>Please note:</strong> Any ellipses (…) in the snippets below stand in for code that we have already covered. We have used them to shorten the code and highlight the parts that are relevant to that section.

<pre><code class="language-markup tmp-html">&lt;nav class="main-navigation"&gt;
   &lt;ul&gt;
      &lt;li&gt;&lt;a href="#home"&gt;Home&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;
         &lt;a href="#about"&gt;About Us&lt;/a&gt;
         &lt;ul class="children"&gt;
            &lt;li&gt;&lt;a href="#leadership"&gt;Leadership&lt;/a&gt;&lt;/li&gt;
            &lt;li&gt;&lt;a href="#involvement"&gt;Involvement&lt;/a&gt;&lt;/li&gt;
            &lt;li&gt;&lt;a href="#vision"&gt;Our Vision&lt;/a&gt;&lt;/li&gt;
         &lt;/ul&gt;
      &lt;/li&gt;
      &lt;li&gt;&lt;a href="#clients"&gt;Our Clients&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;
         &lt;a href="#support"&gt;Support&lt;/a&gt;
         &lt;ul class="children"&gt;
            &lt;li&gt;&lt;a href="#blog"&gt;Blog&lt;/a&gt;&lt;/li&gt;
            &lt;li&gt;&lt;a href="#downloads"&gt;Downloads&lt;/a&gt;&lt;/li&gt;
            &lt;li&gt;&lt;a href="#faq"&gt;FAQ&lt;/a&gt;&lt;/li&gt;
         &lt;/ul&gt;
      &lt;/li&gt;
      &lt;li&gt;&lt;a href="#contact"&gt;Contact Us&lt;/a&gt;&lt;/li&gt;
   &lt;/ul&gt;
&lt;/nav&gt;</code></pre>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117114" title="prog-resp-nav_01b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d5d798c-b979-447a-a2ef-c60792028b62/prog-resp-nav-01b.jpg" alt="Unstyled Navigation" width="179" height="237" /><br>
<em>Our navigation, unstyled.</em>

## Our Tools

*   CSS Reset
*   HTML5 elements
*   LESS CSS
*   jQuery

### CSS Reset

Resetting our CSS styles is where we’ll start. Browsers have different default styles for the elements we’ll be using, so understanding this and getting all of the elements to look the same is important. In this example, since we’re using an unordered list, there will be default left padding, top and bottom margins, and a <code>list-style</code>. You can either deal with these individually or, if you’re project will include more than just this navigation, use a reset to clear all of the styles and start fresh. I prefer Eric Meyer’s <a href="https://meyerweb.com/eric/tools/css/reset/">Reset CSS</a>, but there are a few others to choose from, listed below. Whichever you choose, make sure it accounts for the new HTML5 elements.

*   [Yahoo! YUI CSS Reset](https://yuilibrary.com/yui/docs/cssreset/)
*   [HTML5 Doctor CSS Reset](https://html5doctor.com/html-5-reset-stylesheet/)
*   [Normalize.css](https://necolas.github.com/normalize.css/) (HTML5-ready alternative to CSS resets)

### HTML5 and CSS3 Elements

We’ll be wrapping the menu in HTML5’s <code>nav</code> element, which is one HTML5 feature that <a href="https://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-html5-features-you-should-be-using-right-now/">we should be using right now</a>. If you need more good reasons to use HTML5 in your daily work, such as accessibility, then read “<a href="https://tympanus.net/codrops/2011/11/24/top-10-reasons-to-use-html5-right-now/">Top 10 Reasons to Use HTML5 Right Now</a>” over at Codrops.

CSS3 will give our menu the progressive feel we’re looking for. We can use nifty effects such as linear gradients, text and box shadows and rounded corners, while providing a reasonable appearance for browsers that are dragging their feet. You could also consider using something like <a href="https://css3pie.com/">CSS3 Pie</a> in the process. This will give those lagging browsers most of the functionality they lack to display your CSS3 properties.</p>

### LESS CSS

To make our CSS more efficient, we’ll use <a title="Less « The Dynamic Stylesheet Language" href="https://lesscss.org/">LESS</a> along with a class file to <a href="https://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-never-type-a-vendor-prefix-again/">ease the difficulty</a> of dealing with all of those browser prefixes. Other options, such as Sass and Compass, do effectively the same thing and might better fit your particular development environment. If you’re interested in learning more about LESS and how it compares to Sass, check out another article of mine, “<a href="https://www.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/">An Introduction to LESS, and Comparison to Sass</a>.”

### jQuery

To make our navigation a little friendlier in small browsers, such as those on mobile devices, we’ll use JavaScript. Essentially, we will gather all of the elements in our navigation and reorganize them into a <code>select</code> form element. Then, when the user selects an option from the list, they will navigate to that page. Interaction with a <code>select</code> element is one of the easiest and best ways to handle navigation in a small window. The practice is pretty common as well, so the learning curve for users will be gentler.</p>

## Getting Started

After applying a reset, we get something like the following. You can see that the margins, padding and list styles have been cleared.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117118" title="prog-resp-nav_02" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c31235f-e298-4982-b341-dd284b5c9c16/prog-resp-nav-02.jpg" alt="Reset navigation" width="120" height="187" /><br>
<em>Reset navigation</em>

### Child-Level Menus

For now, the child-level menus will only get in the way. The best thing to do is remove them from the equation and add them back in when it’s time to style them. To achieve this, we will apply <code>position: relative</code> to all of the list elements, and move the children off screen until they are needed.

<pre><code class="language-css">.main-navigation {
   li {
      position: relative;
   }
   .children {
      left: -999em;
      position: absolute;
   }
}</code></pre>

Applying <code>left: -999em; position: absolute;</code> will move the children to the left of the screen by a significant margin. This method is preferable to just using <code>display: none</code> because it is more accessible to screen readers.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117120" title="prog-resp-nav_03" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3d2268-3ede-4db9-a4a3-5eee091eb7c1/prog-resp-nav-03.jpg" alt="Unstyled without children" width="113" height="104" /><br>
<em>Unstyled without children</em>

### Common Navigation Styles

Every navigation menu will probably have links in it. But these links are not like the links we see in the main body of the page, which are blue, underlined and distinguishable from the surrounding text. Rather, links in the navigation will stand alone, and their function will be obvious. That being said, the links in a <code>nav</code> element will probably have a few features of their own that distinguish them from typical anchor tags.

<pre><code class="language-css">nav {
   a {
      color: inherit;
      display: block;
      text-decoration: none;
   }
}</code></pre>

Thus, a link will inherit the color of the text assigned to the parent element, in this case <code>nav</code>. It will be set to display as a block-level element, because we want the clickable area to be large and we do not want underlining (because that would just look funny).

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117128" title="prog-resp-nav_04" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507e6657-ace6-4d12-8ac3-fab59fc8d5b9/prog-resp-nav-04.jpg" alt="Navigation with more functional links" width="112" height="102" /><br>
<em>Navigation with more functional links</em>

<strong>Please note:</strong> <code>color: inherit</code> is not supported in IE 6 or 7. If you need to support those browsers, then you will need to explicitly set the color that you want.</p>

### Lining Up

Getting the menu in line calls for the use of floats. Initially, we’ll float all of the elements in the <code>nav</code> element to the left. Later, we’ll undo this property for the child-level menus, along with a lot of the other styles that we’ll set along the way.

<pre><code class="language-css">.main-navigation {
   ul, li, a {
      float: left;
   }
   …
}</code></pre>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117159" title="prog-resp-nav_05" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afdeb270-f7d6-4cc7-ada7-01fc9c012be2/prog-resp-nav-05.jpg" alt="Inline navigation" width="337" height="44" /><br>
<em>Inline navigation</em>

Because every element in the <code>nav</code> element is now floated, the element itself will collapse as though it were empty. There are a few ways to deal with this. One is to also float the <code>nav</code> element itself, which will expand it to wrap around its contents. If need be, you can set it to <code>width: 100%</code> to fill any remaining space to the right. Or you could use Nicolas Gallagher’s <a href="https://nicolasgallagher.com/micro-clearfix-hack/">“micro” clearfix</a> solution, which essentially adds <code>clear: both</code> just before the closing of the <code>nav</code> element.

<pre><code class="language-css">/* For modern browsers */
.cf:before,
.cf:after {
    content:"";
    display:table;
}
.cf:after {
    clear:both;
}
/* For IE 6/7 (trigger hasLayout) */
.cf {
    zoom:1;
}</code></pre>

Because we’re using LESS for our CSS, applying the clearfix to our <code>main-navigation</code> class without modifying the markup is very easy.

<pre><code class="language-css">.main-navigation {
   .cf;
   …
}</code></pre>

We’ll see more of this, as well as a description of how this works, in the section titled “Rounded Corners and Gradients” below.</p>

## Styling

All righty. By now, you’re probably as tired of looking at an unstyled menu as I am. To start, we’ll build what looks like a block wall, and then chisel a nice menu out of it. We won’t serve the block wall to antiquated browsers, but it’s a good start anyway.</p>

### Background Color and Borders

<pre><code class="language-css">.main-navigation {
   font-size: 0.8em;

   ul, li, a {
      …
   }
   ul {
      background: #eee;
      border: 1px solid #ddd;
   }
   li {
      …
      border-right: 1px solid #ddd;
   }
   li:last-child {
      border-right: none;
   }
   a {
      height: 35px;
      line-height: 35px;
      margin: 3px;
      padding: 0 15px;
   }
   .children {
      …
   }
}</code></pre>

In the code above, the text was just too big, so we shrunk it with <code>font-size: 0.8em</code>. This property is set on the <code>main-navigation</code> class, so it applies throughout the navigation. The top-level unordered list has a <code>border: 1px solid #ddd</code> property to break it out from the page. Each list item element is given a <code>border-right: 1px solid #ddd;</code> to separate it from each other. The <code>li:last-child</code> selector targets the last list item element in the unordered list, removing the right border because no item follows it.

The links within the navigation are given a background color and some left and right padding to add distinction and increase their clickable area. We’re fixing the <code>height</code> and <code>line-height</code>, instead of using top and bottom padding, so that we can predict more accurately where the child-level menus will be positioned relative to their shared parent list item.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117208" title="prog-resp-nav_06b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/264feecd-b7ef-470c-9a65-95e3690d6e6a/prog-resp-nav-06b.jpg" alt="Navigation resembling a block wall" width="459" height="74" /><br>
<em>Navigation resembling a block wall</em>

### Rounded Corners and Gradients

<pre><code class="language-css">.main-navigation {
   …
   text-shadow: 0 1px 1px #fff;

   ul {
      border: 1px solid #ddd;
      .border-radius();
      .linear-gradient();
   }
   …
}

.border-radius (@radius: 5px) {
   border-radius: @radius;
}
.linear-gradient (@start: #fff, @end: #ddd, @percent: 100%) {
   background: @start; /* Old */
   background: -moz-linear-gradient(top,  @start 0%, @end @percent); /* FF3.6+ */
   background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,@start), color-stop(@percent,@end)); /* Chrome, Safari 4+ */
   background: -webkit-linear-gradient(top,  @start 0%,@end @percent); /* Chrome 10+, Safari 5.1+ */
   background: -o-linear-gradient(top,  @start 0%,@end @percent); /* Opera 11.10+ */
   background: -ms-linear-gradient(top,  @start 0%,@end @percent); /* IE 10+ */
   background: linear-gradient(top,  @start 0%,@end @percent); /* W3C */
}</code></pre>

Above, we have created two new classes, <code>border-radius</code> and <code>linear-gradient</code>.

The <code>border-radius</code> class is actually what LESS developers refer to as a <a href="https://lesscss.org/#-parametric-mixins">parametric mixin</a>. Essentially, it’s like a class, but you can pass variables to it in case the default value isn’t exactly what you want. In this case, if 5 pixels isn’t what you want, you could reference the mixin as <code>.border-radius(10px)</code>, and then it would use <code>10px</code> instead of the original <code>5px</code>. With the <code>border-radius</code> property, you could also pass it something like <code>.border-radius(5px 0 0 5px)</code>, and it would apply the 5-pixel rounding to only the top-left and bottom-left corners. For more information and possibilities on <code>border-radius</code>, see “<a href="https://www.css3.info/preview/rounded-border/">Border-Radius: Create Rounded Corners With CSS</a>” at CSS3.info.

Another parametric mixin is <code>linear-gradient</code>. But with LESS, you can add classes to other selectors and it will apply the same styles—thus negating the need to modify the markup just to add another class (and, by extension, its styles) to an element. Both of the classes I’ve created cover the possibilities of browser syntax. Currently, Webkit has two different syntaxes, because for some reason the browser makers decided to ignore the specification when first implementing it and made up their own syntax. With Chrome 10 and Safari 5.1, they went back to the specification, joining the other browsers, and made things a little easier for us. However, if you still care about the previous versions, you’ll need to add their crazy syntax as well. We’ve also added a white <code>text-shadow</code> to the text in the navigation to give it a slightly beveled look.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117210" title="prog-resp-nav_07c" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7feee1e7-9d54-4d98-8bc3-08e8bfb42ffd/prog-resp-nav-07c.jpg" alt="Navigation with a gradient and rounded corners" width="458" height="72" /><br>
<em>With the two classes applied, you can see the slight gradient and the rounded corners.</em>

<strong>Some browsers do not support CSS3 gradients.</strong> Yes, I’m looking at you, Internet Explorer 6, 7, 8 and 9. If you want to use something other than the filter syntax for gradients, you’ll have to wait for version 10. In the meantime, either you could use the filter syntax for IE (see the “For Internet Explorer” section of “<a href="https://webdesignerwall.com/tutorials/cross-browser-css-gradient">Cross-Browser CSS Gradient</a>”) and put them in an IE-specific style sheet, or you could use an image gradient. You could also just leave them without the gradient, but that’s not the point here.</p>

### Parent-Level Hover States

<pre><code class="language-css">.main-navigation {
   …
   li:hover {
      a {
         .linear-gradient(#dfdfdf, #c0bebe, 100%);
      }
      .children {
         …
         a {
            background: none;
         }
      }
   }
   …
}</code></pre>

The code above will trigger the hover state for anchor elements when the user hovers over their parent list item, rather than hovering over the anchors themselves. This way is preferable so that the anchor element maintains its hover state when the user is mousing over the child-level menu as well. Doing it this way does, however, create the need to reset the background color of anchor elements within the child-level menus. That’s the part you see within the <code>children</code> selector.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117214" title="prog-resp-nav_07d" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35977425-047a-449a-92ff-58b433a51c56/prog-resp-nav-07d.jpg" alt="Hovering over the parent-level links" width="460" height="72" /><br>
<em>Hovering over the parent-level links</em>

## Displaying the Children

Bringing the children back onto the screen is easy enough. But before we get carried away, we need to clear out a few styles that are applied to all unordered lists, list items and anchors.

<pre><code class="language-css">.main-navigation {
   …
   .children {
      background: #fff;
      left: -999em;
      position: absolute;

      li, a {
         float: none;
      }
      li {
         border-right: none;
      }
   }
}</code></pre>

The code above changes the background of the child-level menu to white, instead of the light gradient that we used in the parent-level menu. The next couple of lines remove the left float from the list items and anchors. We’ve also gotten rid of the right border that separates the list items in the parent-level menu.</p>

### The Hovering Box

<pre><code class="language-css">.main-navigation {
   …
   .children {
      background: #fff;
      .box-shadow();
      left: -999em;
      margin-left: -65px;
      position: absolute;
      top: 30px;
      width: 130px;
      …
   }
}

…
.box-shadow (@x: 0, @y: 5px, @blur: 5px, @spread: -5px, @color: #000) {
   -moz-box-shadow: @x @y @blur @spread @color;
   -webkit-box-shadow: @x @y @blur @spread @color;
   box-shadow: @x @y @blur @spread @color;
}
…</code></pre>

We’ve added another parametric mixin to the equation. This one produces the box shadow, with all of its parameters as variables, and with the browser prefixes. We’ve borrowed the styles from <code>.children</code> to make the box appear to hover over the parent menu. To center the child underneath the parent element, we’ve set the left position to 50%, and set the left margin to the negative value of half the width of the child. In this case, the child level menu is set to 130 pixels wide, so we’ve set the left margin to -65 pixels.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117216" title="prog-resp-nav_08b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c666d52-e6b6-4c71-be77-89daab32ca3f/prog-resp-nav-08b.jpg" alt="Navigation w/child reset to hover style" width="457" height="166" /><br>
<em>Navigation with the child reset to hover style</em>

### Child-Level Hovers

<pre><code class="language-css">.main-navigation {
   …
   .children {
      …
      a {
         .border-radius(3px);
         height: 30px;
         line-height: 30px;
         margin: 3px;
      }
      a:hover {
         background: #dff2ff;
      }
   }
}</code></pre>

We’re using the parametric mixin that we created for the <code>border-radius</code> for the links in the children as well. Adding a 3-pixel margin and 3-pixel border radius to all of the anchor elements within the child menu will accent the 5-pixel border radius of the menu well. We’ve also adjusted the height and line height a little, because they just seemed too high. Finally, we gave the list items a nice soft-blue background color on hover.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117218" title="prog-resp-nav_09b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e619cdb-6a16-4984-9f9d-fc700523c679/prog-resp-nav-09b.jpg" alt="Navigation w/child menus and their hover state" width="460" height="166" /><br>
<em>Navigation with child menus and their hover state</em>

## Responding to Mobile Browsers and Size Constraints

A lot of screen sizes and browsers are out there. The iPhone has had two resolutions. Up to the 3GS model, it was 480 × 320; since the iPhone 4, it has been 960 × 640. Android browsers run from 480 × 320 to 854 × 480. Android also has a lot of browsers to choose from. There are the usual Firefox and Opera, as well as a ton of browsers by small start-ups. You can get Opera for the iPhone, but since you can’t make it the default browser, you’re pretty much stuck with Safari. Given this variety, we’ll have to make some adjustments if we want our navigation to be useful on all devices and in all browsers.</p>

### Fitting the Content

Accomplishing this part is easy, but doing it will probably require adjusting our styles. But that’s why we’re here, isn’t it?

Currently, when we open the navigation demo in iOS, it looks like this:

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117446" title="prog-resp-nav_10b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e02d934-c1e6-4c3f-ba23-98b3b93d453e/prog-resp-nav-10b.jpg" alt="Original navigation in iOS" width="320" height="480" /><br>
<em>Original navigation in iOS</em>

This might not look too bad on a giant screen, and it might even be usable on the iPad, but you would struggle to use it on a phone. Zooming in might make it easier, but that’s not ideal. Optimizing for the device is preferable, and forcing the browser to use the available space is simple.

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width"&gt;</code></pre>

This alone makes a huge difference in the way the browser renders the page. And while the menu is not the prettiest it’s ever been, it is a lot more functional.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117449" title="prog-resp-nav_11" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23058560-5f55-4062-803a-eb93a8bda702/prog-resp-nav-11.jpg" alt="Navigation on iOS with the viewport adjusted" width="320" height="480" /><br>
<em>Navigation on iOS with the viewport adjusted</em>

### Media Queries

We can use media queries to adjust the styles based on the media in the browser. In this case, we’ll use the width of the page to change the look and feel of the navigation to make it more suitable to the available space. In this case, we’ll make the menu items more button-like.

<pre><code class="language-css">@media only screen and (max-width: 640px) {
   .main-navigation {
      ul {
         border: none;
         background: none;
         .border-radius(0);
      }
      li {
         border-right: none;
      }
      a {
         border: 1px solid #ddd;
         .border-radius();
         font-size: 1.2em;
         height: auto;
         .linear-gradient();
         line-height: 1em;
         padding: 15px;
      }
   }
}</code></pre>

In the code above, we’ve used a media query to target situations in which the user is only looking at a screen and in which the width of the window is a maximum of 640 pixels. In this scenario, we’ve removed the border, background and border radius from the unordered list, and applied those styles to the anchors themselves. We’ve also increased the font size of the anchors, cleared the height and line height, and adjusted the padding of the links to increase the clickable area.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117453" title="prog-resp-nav_12" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cd94733-c35c-421b-ae8b-ea4deb60328f/prog-resp-nav-12.jpg" alt="Navigation adjusted for mobile display" width="320" height="480" /><br>
<em>Navigation adjusted for mobile</em>

As you can see, the links look much friendlier in a mobile browser. They are, however, only half functional, because touch devices don’t have a hover state. This means that if you have child-level menus, as we do here, you’ll have to figure out a way to display them as well. You could replace the hover state with a touch event of some kind, or expand the children out onto the page. That would greatly increase the size of the navigation, though. The following method might be best.</p>

### Replacing the Menu in Mobile Browsers With JavaScript

<pre><code class="language-javascript">$(function() {
   /* Get the window's width, and check whether it is narrower than 480 pixels */
   var windowWidth = $(window).width();
   if (windowWidth &lt;= 480) {

      /* Clone our navigation */
      var mainNavigation = $('nav.main-navigation').clone();

      /* Replace unordered list with a "select" element to be populated with options, and create a variable to select our new empty option menu */
      $('nav.main-navigation').html('&lt;select class="menu"&gt;&lt;/select&gt;');
      var selectMenu = $('select.menu');

      /* Navigate our nav clone for information needed to populate options */
      $(mainNavigation).children('ul').children('li').each(function() {

         /* Get top-level link and text */
         var href = $(this).children('a').attr('href');
         var text = $(this).children('a').text();

         /* Append this option to our "select" */
         $(selectMenu).append('&lt;option value="'+href+'"&gt;'+text+'&lt;/option&gt;');

         /* Check for "children" and navigate for more options if they exist */
         if ($(this).children('ul').length &gt; 0) {
            $(this).children('ul').children('li').each(function() {

               /* Get child-level link and text */
               var href2 = $(this).children('a').attr('href');
               var text2 = $(this).children('a').text();

               /* Append this option to our "select" */
               $(selectMenu).append('&lt;option value="'+href2+'"&gt;--- '+text2+'&lt;/option&gt;');
            });
         }
      });
   }

   /* When our select menu is changed, change the window location to match the value of the selected option. */
   $(selectMenu).change(function() {
      location = this.options[this.selectedIndex].value;
   });
});</code></pre>

To summarize, first we’re checking whether the window is less than or equal to 480 pixels. To ensure an accurate reading on mobile devices, you can use a meta tag to scale the viewport accordingly:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width"&gt;</code></pre>

We populate the first variable, <code>windowWidth</code>, with the value of the window’s width as defined by the given device. We can use this value to then check whether the width is narrower than a particular value. We’ve chosen 480 pixels here because, while we might want to use media queries to adjust the menu below 640 pixels, at a certain point the viewport would be just too small to justify the menu taking up all that space.

We then use jQuery to create a clone of our menu that we can later crawl to create our options. After we’ve done that, it’s safe to replace the unordered list with the <code>select</code> element that we’ll be using and then select it with jQuery.

In the largest part of the code, we’re crawling through the clone of our navigation. The selector used, <code>$(mainNavigation).children('ul').children('li')</code>, ensures that we go through only the uppermost list elements first. This is key to creating the nested appearance of the select menu. With it, we select the “direct” child-level unordered list elements and then their “direct” child-level list elements, and then parse through them.

Inside each of these “direct” descendants, we get the value of the <code>href</code> attribute and the text of the link, and we store them in variables to be inserted in their respective options. This is implemented by appending <code>&lt;option value="'+href+'"&gt;'+text+'&amp;kt;/option&gt;</code> to our new select list.

While we’re in the top-level list item elements, we can check whether any child-level menus need to be parsed. The statement <code>if ($(this).children('ul').length &gt; 0)</code> checks whether the count of the selector is greater than 0. If it is, that means child-level items need to be added. We can use that same selector, with a slight addition, to go through these elements and add them to our select list, <code>$(this).children('ul').children('li').each()</code>.

The same parsing method applies to these elements, although they use different variables to store the values of the anchor tags, so as not to create conflicts. We have also prefixed text to the menu labels at this level, <code>--- </code>, to differentiate them from the other items.

Parsing through the menu in this method (nested) will create the parent-child relationship you would expect.

After the menu is created, a little more JavaScript will enable the select list to serve as navigation.

<pre><code class="language-javascript">$(selectMenu).change(function() {
   location = this.options[this.selectedIndex].value;
});</code></pre>

When the select menu is changed, a new option is selected, and the window location is changed to reflect the value of the option. That value comes from the <code>href</code> of the original anchor element.

The result is like so:

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="116137" title="Select menu on desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a28a8923-9473-40d1-8462-370dac6822c0/screen-shot-2011-11-14-at-21.jpg" alt="screenshot" width="162" height="215" /><br>
<em>The select menu in a desktop browser</em>

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="117565" title="prog-resp-nav_13" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5caa255-8977-45b4-a591-b90ec92dcb38/prog-resp-nav-13.jpg" alt="Select menu on Android and iPhone" width="500" height="427" /><br>
<em>The select menu in Android and iPhone browsers</em>

Given the increased clickable area of the native controls, the select menu is obviously much more user-friendly on mobile.</p>

## Share Your Experience

We’d love to see and hear about some of your experiences with menus across browsers and platforms; please share below. And if you have any questions, we’ll do our best to find answers for you.

{{< signature "al" >}}

