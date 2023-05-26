---
title: 'Techniques For Gracefully Degrading Media Queries'
slug: techniques-for-gracefully-degrading-media-queries
image: >-
  null
date: 2011-08-10T07:00:04.000Z
author: lewis-nyman
summary: >-
  Media Queries are a great tool to enhance the experience of browsing a website on multiple devices. Lewis Nyman outlines some of the techniques that developers can follow to address the problem of mobile and desktop browsers that lack media queries support. 
description: >-
  Media Queries are a great tool to enhance the experience of browsing a website on multiple devices. Find some techniques you can follow to address the problem of browsers that lack media queries support.
categories:
  - Coding
  - CSS
  - Responsive Design
  - Media Queries
---

Media queries are the third pillar in Ethan Marcotte’s implementation of [responsive web design](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design). Without media queries, fluid layouts would struggle to adapt to the array of screen sizes on the hundreds of devices out there. Fluid layouts can appear cramped and unreadable on small mobile devices and too large and chunky on big widescreen displays. Media queries enable us to adapt typography to the size and resolution of the user’s device, making it a powerful tool for crafting the perfect reading experience.

CSS3 media queries, which include the browser width variable, are supported by most modern Web browsers. Mobile and desktop browsers that lack support will present a subpar experience to the user unless we step up and take action. I’ll outline some of the techniques that developers can follow to address this problem.

{{% feature-panel %}}

### It Depends

<blockquote>“If you’re looking for the more honest, truthful answer to pretty much any question on web design and usability, here it is: It depends.”

&ndash; Jeremy Keith</blockquote>

There is no one-size-fits-all fix. Each project has its own focus, requirements and audience. This article will hopefully help you make the best decision for your project by outlining the advantages and disadvantages of each solution.

## Mobile First

Your chosen implementation of media queries will have a big effect on how you tackle this. Mobile-first responsive design is the process of building a mobile layout first, and then progressively modifying the layout as more screen space becomes available. This ensures that only the minimum required files are loaded, and it keeps the mobile solution lightweight. Mobile first has the advantage of providing a nice fallback for mobile devices that don’t support media queries, such as older BlackBerrys, Opera Mini and Windows Mobile devices. These devices simply see the most basic layout, with no extra work required of the developer. Ideal!

## Technique 1: Do Nothing

Sometimes the lazy approach is the best approach. It keeps your code light and maintainable and reduces any needless processing on the client side. Some old browsers run Javascript like a dog, and old mobile phones struggle to run intensive Javascript. The proprietary non-Webkit browser in most BlackBerrys can take up to eight seconds just to parse the jQuery library. If your project has a long tail of users with low-powered mobile devices, then maybe a mobile-first approach is enough for you.

The elephant in the room is Internet Explorer for the desktop. With a mobile-first solution, large screens will display the content in one column, resulting in a painful reading experience for the user, way past the established maximum for comfort: <a href="https://www.webtypography.net/Rhythm_and_Proportion/Horizontal_Motion/2.1.2/">50 to 75 characters.</a> It might be worth setting a <code>max-width</code> property in your main container and then upping that <code>max-width</code> in a media query.

<pre><code class="language-css">#container {
 _width: 460px; /* Take that, IE6! */
max-width: 460px;
}

@media only screen and (width) { /* A quick and simple test for CSS3 media query support. */

#container {
  max-width: 1200px; /* Add the real maximum width here. */
 }

}</code></pre>

### Do Nothing If…

*   Your core audience uses modern smartphones,
*   You are required to provide an acceptable experience to a long tail of feature-phone users,
*   The desktop is not a big part of your Web strategy.

**Example**: <a href="https://jquerymobile.com/gbs/">jQuery Mobile</a> (“Any device that doesn’t support media queries will receive the basic C-grade experience”).

## Technique 2: Conditional IE Style Sheets

Surprisingly, in researching this article, I found this to be the most popular technique in use on responsive websites. Instead of polyfilling support for media queries, you simply <del>you simply load an additional style sheet only for Internet Explorer</del> load the same stylesheet that you’re serving up to browsers that do understand media queries for Internet Explorer. For mobile-first approaches, this usually entails loading a basic style sheet that sets up a multi-column layout for large screens. Jeremy Keith <a href="https://adactio.com/journal/4494/">documents this approach</a> in detail on his blog. He also adds a condition that doesn’t load the style sheet for mobile versions of IE. Crafty.

It’s a simple and effective technique for supporting Internet Explorer on the desktop, and it supports the mobile-first approach because it loads a light and appropriate linear layout for feature phones.

<del>On the other hand, this technique could potentially degrade maintainability, requiring you to maintain a style sheet of duplicate content.</del> It also adds another HTTP request for IE users, which should be avoided if possible.

<del>I’m surprised that Jeremy Keith advocates this technique. The man who proclaimed on stage that user-agent sniffing is “<a href="https://adactio.com/articles/4661/">the spawn of Satan</a>” is using a solution aimed squarely at one browser.</del> Bear in mind that this does not work with browsers that do not support CSS3 media queries. But it can be perfectly acceptable in situations where support for other legacy browsers is not required.

{{% ad-panel-leaderboard %}}

### Use Conditional IE Comments If…

*   You are using a mobile-first workflow;
*   Your media queries are simple enough to include in a single style sheet;
*   Desktop Internet Explorer requires a multi-column layout, at the expense of speed;
*   You do not have to support a long tail of legacy desktop browsers.

**Example:** <a href="https://huffduffer.com/">Huffduffer</a>, a mobile-first approach with an additional column for screen widths over 480 pixels.

**Bonus example:** Designing With Data by Five Simple Steps. I love these guys.

## Technique 3: Circumvent Media Query Conditions

The Opera Developer Blog published an article in 2007 detailing the safe usage of media queries. It helped pave the way for CSS3 media query usage by presenting research on the correct way to write them, a way that prevents browsers from applying the containing CSS when they do not understand a media query.

… Browsers like IE.

But what if, with a mobile-first approach, that’s exactly what we do want? What if we were to write our media queries so that the containing CSS gets applied by IE unconditionally. We could then have our full desktop layout without any additional style sheets to load or maintain.

<pre><code class="language-css">@media screen, all and (min-width: 300px) {
	div {
		background: blue;
	}
}</code></pre>

As the blog post states:
<blockquote>“Now it is no longer the case that IE does not apply the contents of the query. It now doesn’t understand the second part (<code>all and</code>), so it ignores that and happily applies the contents of the query…”</blockquote>

### Circumvent Media Query Conditions If…

*   You are only required to support modern smartphones,
*   You are building mobile first and require a desktop layout in IE,
*   Loading time and maintainability must be kept to a minimum.

## Technique 4: Respond.js

Scott Jehl’s lightweight polyfill <a href="https://github.com/scottjehl/Respond">Respond.js</a> offers a leg up for browsers that do not support CSS3 media queries. It can be compressed down to as little as 1 KB, and it parses CSS files fast, without needing any additional libraries.

JavaScript reliance aside, Respond.js appears to be a solid solution for full support of media queries. However, the small file size and speed come at a cost. Respond.js was never meant to be a full-featured solution. Its purpose is to provide the bare minimum for responsive layouts to work.

It supports only the <code>min-width</code> and <code>max-width</code> queries, so it’s not the right solution if you are looking at using <code>device-width</code>, <code>device-height</code>, <code>orientation</code>, <code>aspect-ratio</code>, <code>color</code>, <code>monochrome</code> or <code>resolution</code>. Some good use cases here are not supported, one being the detection of high-resolution devices such as the iPhone 4 and non-color devices such as the Kindle.

Respond.js <a href="https://github.com/scottjehl/Respond/issues/18">does not support em-based queries</a>, which makes impossible any decent support for font-size user preferences (even more important on a small screen than on a desktop). Products like <a href="https://www.readability.com/">Readability</a> and <a href="https://reederapp.com/">Reeder</a> validate this desire among users to control and refine the reading experience. Em-based media queries will become only more important as we head towards a <a href="https://adactio.com/journal/4523/">content-first</a> approach to Web design, so they are worth considering.

There are a lot of small bumps and caveats with Respond.js. I recommend browsing the <a href="https://github.com/scottjehl/Respond#readme">read-me text</a> and the <a href="https://github.com/scottjehl/Respond/issues">issue queue</a> before settling on it for you project.

### Use Respond.js If…

*   Desktop support is a <del>primary</del> high concern,
*   You are querying only the width and height of the browser,
*   You don’t want to query the width by ems,
*   You have no problem with non-JavaScript users seeing an unoptimized page.

**Example:** Aaron Weyenberg, a desktop-centric website with a basic layout.

## Technique 5: CSS3-MediaQueries-js

<a href="https://code.google.com/p/css3-mediaqueries-js/">CSS3-MediaQueries-js</a> picks up where Respond.js leaves off. It supports the full range of media queries introduced in CSS3. The “everything and the kitchen sink” approach is great for a developer’s peace of mind. Simply drop it in, and tick the “IE support” box.

But there are significant downsides to consider: this script is not fast; it parses CSS much slower than Respond.js; and it weighs in at a hefty 15 KB.

### Pro Tip 1

Let’s be responsible and load this file only if the browser doesn’t actually support CSS3 media queries. Otherwise, you’re wasting good time and data. You can use Yepnope to load the 15 KB file if it detects that media queries are not available.

Here’s a modification of a Yepnope function that I wrote for <a href="https://www.modernizr.com/">Modernizr</a>’s media query test. Yepnope now comes bundled with Modernizr.

<pre><code class="language-javascript">yepnope({
test : Modernizr.mq('@media only screen and (width)'),
yep : ’,
nope : 'css3-mediaqueries.js',
});</code></pre>

If you don’t require support for non-IE devices, then replace the Yepnope function with a much lighter conditional comment.

<pre><code class="language-markup tmp-xhtml">&lt;!--[if (lt IE 9) &amp; (!IEMobile)]&gt;
 &lt;script src="css3-mediaqueries.js"&gt;&lt;/script&gt;
 &lt;![endif]--&gt;</code></pre>

### Pro Tip 2

If you are building for mobile first, then adding a <code>min-device-width</code> condition to the Yepnope query is definitely worthwhile. This will prevent the hefty 15 KB file from loading on small screens that will never use it. Win!

### Use CSS3-MediaQueries-js If…

*   You are using advanced media queries, beyond simple pixel-width conditions;
*   You are happy to take that 15 KB loading hit;
*   Your audience doesn’t include a long tail of feature-phone users.

**Example:** <a href="https://hicksdesign.co.uk/">Hicksdesign</a> uses complex media queries beyond simple width and height.

## In Conclusion

Responsive design is still a new way of thinking. Media Queries are a great tool to enhance the experience of browsing a web site on multiple devices and it’s a great idea to consider devices that do no support them. We would be dreaming if we expected an easy solution from day one but at least we have a range of options in front of us that allow us to find the best solution for the problem at hand.

It’s important to bear in mind that context is key, a well informed decision will always yield better results instead of quickly choosing the most popular solution.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Absolute Horizontal And Vertical Centering In CSS](https://www.smashingmagazine.com/2013/08/absolute-horizontal-vertical-centering-css/)
*   [How To Use CSS3 Media Queries](https://www.smashingmagazine.com/2010/07/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/)
*   [Responsive Web Design With Physical Units](https://www.smashingmagazine.com/2013/03/responsive-web-design-with-physical-units/)
*   [Logical Breakpoints For Your Responsive Design](https://www.smashingmagazine.com/2013/03/logical-breakpoints-responsive-design/)

{{< signature "al, mrn" >}}
