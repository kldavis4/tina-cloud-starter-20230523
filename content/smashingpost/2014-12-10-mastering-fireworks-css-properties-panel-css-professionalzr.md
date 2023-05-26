---
title: How To Master Fireworks’ CSS Properties Panel And CSS Professionalzr
slug: mastering-fireworks-css-properties-panel-css-professionalzr
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b809c6c-adb6-4587-86a8-9a9a8bc161a2/extracting-css-500px.jpg
date: 2014-12-10T15:01:16.000Z
author: gauthier-eloy
description: >-
  Today, being a designer is about much more than drawing beautiful interfaces
  in Photoshop or Fireworks. To properly design a website or application, a UI
  designer must understand the technology with which their products will be
  built; therefore, they must have a minimum set of front-end development
  skills. The World Wide Web is not static. Quite the opposite: It’s
  [responsive](https://www.smashingmagazine.com/tag/responsive-web-design/),
  [fluid](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/),
  [evolving](https://www.smashingmagazine.com/2014/09/08/improving-smashing-magazine-performance-case-study/)
  and [ever changing](https://caniuse.com/).

  Web designers need to be familiar with [HTML and
  CSS](https://www.w3.org/standards/webdesign/htmlcss) code and front-end
  technologies when they conceive a website or application’s interface. It might
  be of no real interest to some of you, but it could add some precious assets
  to your range of skills.
categories:
  - Coding
  - Fireworks
  - Tools
  - CSS
  - Techniques
  - Extensions
---
Today, being a designer is about much more than drawing beautiful interfaces in Photoshop or Fireworks. To properly design a website or application, a UI designer must understand the technology with which their products will be built; therefore, they must have a minimum set of front-end development skills. The World Wide Web is not static. Quite the opposite: It’s <a href="https://www.smashingmagazine.com/tag/responsive-web-design/">responsive</a>, <a href="https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/">fluid</a>, <a href="https://www.smashingmagazine.com/2014/09/08/improving-smashing-magazine-performance-case-study/">evolving</a> and <a href="https://caniuse.com/">ever changing</a>.

Web designers need to be familiar with <a href="https://www.w3.org/standards/webdesign/htmlcss">HTML and CSS</a> code and front-end technologies when they conceive a website or application’s interface. It might be of no real interest to some of you, but it could add some precious assets to your range of skills. Or, as <a href="https://twitter.com/zeldman/status/4818978868">Jeffrey Zeldman put it</a> five years ago:
<blockquote>Real web designers write code. Always have, always will.</blockquote>

His words are still valid today.

I recommend that you read a very interesting article, “<a href="https://nicolasgallagher.com/about-html-semantics-front-end-architecture/">About HTML Semantics and Front-End Architecture</a>,” by <a href="https://twitter.com/necolas">Nicolas Gallagher</a>, creator of <a href="https://necolas.github.io/normalize.css/">Normalize.css</a> (a modern alternative to <a href="https://stackoverflow.com/questions/11578819/css-reset-what-exactly-does-it-do">CSS resets</a>) and one of the web’s most popular front-end templates, <a href="https://html5boilerplate.com/">HTML5 Boilerplate</a>.

Knowing front-end development will also facilitate the work of the developer who will implement your design later (that is, if you’re not both the designer and the developer).

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

I still notice that quite a few designers are extremely good at creating beautiful user interfaces but do not have enough experience in HTML and CSS — and coding experience is even more important these days.

Adobe Fireworks is a graphic design tool, but it has always been focused on web and UI design. In Creative Suite (CS) version 6, a CSS Properties panel was added to its toolset — a tool that, if used properly, could help both designers with CSS coding experience and beginners alike.

By the end of this article, you should have a better overview of this feature and also know how to use it with <a href="https://mattstow.com/css-professionalzr.html">CSS Professionalzr</a>, a free extension developed by <a title="Matt Stow's Twitter profile" href="https://twitter.com/stowball">Matt Stow</a> to further optimize the code generated by the panel.</p>

<strong>Note:</strong> Even though Adobe Fireworks CS6 was “feature-frozen” in 2013, it still works as of the end of 2014, with no issues in the <a href="https://twitter.com/optimiced/status/532172093472116736">latest editions of Windows</a> (8.1) and <a href="https://twitter.com/gradykelly/status/522982484879753216">of Mac OS X</a> (Yosemite). Not only does it work, but it’s still being actively used by many designers — among them, designer and illustrator <a href="https://dribbble.com/cocorino">Fabio Benedetti</a>, who recently <a title="(Rocket) Icon Design with Adobe Fireworks" href="https://www.smashingmagazine.com/2014/09/23/designing-a-rocket-icon-in-adobe-fireworks/">wrote an extensive piece</a> about designing and illustrating icons in Fireworks.</p>

## The CSS Properties Panel In Fireworks

### What Is It?

Initially introduced as a beta feature in Adobe Labs, <a href="https://helpx.adobe.com/fireworks/learn/tutorials/how-to/extract-css-properties.html">Fireworks’ CSS Properties panel</a> was finalized and released in version CS6.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b809c6c-adb6-4587-86a8-9a9a8bc161a2/extracting-css-500px.jpg" alt="" /><figcaption>The article “<a href="https://helpx.adobe.com/fireworks/learn/tutorials/how-to/extract-css-properties.html">Extracting CSS Properties From Design Objects in Fireworks</a>” was first published on Adobe Devnet and later republished in Adobe Creative Cloud’s tutorials series. The article mentions that you need both Fireworks and Dreamweaver, but you only really need Fireworks CS6.</figcaption></figure>

In a nutshell, the CSS Properties panel is a tool that displays the most important properties of any object selected on the canvas in Fireworks. The data provided by the panel enables you to perfectly recreate the very same element with CSS3 code. This will save you time and speed up your work.

(CSS Professionalzr is a free extension that further enhances the CSS panel’s capabilities. More on that later.)

### Basic Features

The panel displays the CSS properties of any object selected on the canvas (including vector and text objects), allowing you to easily copy the CSS code to your clipboard. The panel also supports Fireworks’ live filters and Photoshop’s live effects. So, if a Drop Shadow live filter has been applied to an object, then it would be translated to the CSS3 equivalent, <a href="https://css-tricks.com/almanac/properties/b/box-shadow/">box-shadow</a>.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86b54638-645a-417c-b77e-cf63c1f47c33/fw-cs6-properties-panel.png" alt="CSS Properties panel in Fireworks CS6" /><figcaption>The CSS Properties panel in Fireworks CS6</figcaption></figure>

Here is a quick list of what the panel’s features enable you to do:

*   Directly copy to the clipboard all (or some) of the CSS properties that make up an element.
*   Automatically include (or exclude) CSS comments, to better understand and organize your code.
*   Automatically include (or exclude) some (or all) browser vendor prefixes: `-webkit` (for Chrome, Safari and now also Opera), `-moz` (for Firefox), `-o` (for old Opera versions) and `-ms` (for Internet Explorer).</p>

<strong>Note:</strong> The panel lets you include (or exclude) browser vendor prefixes.

When version CS6 was being developed (from 2012 to 2013), browser vendor prefixes were still quite popular in the web design community. Today, their need is quite reduced because major browsers (yes, including the latest versions of Internet Explorer — both on mobile and desktop!) have made great leaps forward. As <a href="https://www.456bereastreet.com/archive/201311/cutting_down_on_vendor_prefixes/">Roger Johansson recently said</a>:
<blockquote>I think there are a bunch of CSS properties that we can safely stop using vendor prefixes for, or at least considerably cut down on the number of prefixes. […] You may be thinking “But no! You’re shutting out people using older versions of browser X!” No, this is not about shutting anyone out or not “supporting” a certain browser version. It is about using progressive enhancement to make your CSS smaller and easier to handle and maintain. We’re not talking about essential features here. If a browser doesn’t support an un-prefixed property, well, there won’t be any rounded corners or shadows or gradients or whatever. The result will look the way it does in IE8, which currently often has a lot more users than, say, Firefox 3.6 or Chrome 9 or Safari for iOS 4 or some other old browser version that may need a vendor prefix. As long as the entire layout doesn’t crash when something isn’t supported, that’s OK in general, given that at least the latest couple of versions of all major browsers will apply your CSS.</blockquote>

So, I think it’s safe to omit all of them. To do so, simply unselect all of the checkboxes, and the CSS Properties panel will output clean CSS. (<a href="https://css-tricks.com/do-we-need-box-shadow-prefixes/">Chris Coyier has written about vendor prefixes</a>, if you’d like to read more.)

<strong>Note:</strong> One way to be safe with browser prefixes is to use <a href="https://github.com/postcss/autoprefixer">Autoprefixer</a>. This plugin parses CSS code and adds vendor prefixes to CSS rules using values from <a title="Can I use?" href="https://caniuse.com/">Can I Use?</a>. In fact, the plugin allows you to write CSS code completely prefix-free by adding all required prefixes automatically. To learn more, take a look at “<a href="https://css-tricks.com/autoprefixer/">Autoprefixer: A Postprocessor for Dealing With Vendor Prefixes in the Best Possible Way</a>,” quite a detailed article. (Autoprefixer is also included in the <a title="Grunt JS" href="https://gruntjs.com/">Grunt</a> template in the wonderful web app generator from <a href="https://yeoman.io/">Yeoman</a>.)

### Supported CSS Properties

Here’s an overview of the types of CSS properties and values you’ll get with the help of this panel:

*   border values: `border-width`, `border-color`, `border-style`, `border-radius` (in `px` or `%`)
*   background color: solid (in `rgba()` format) or with gradients (including linear and radial gradients, along with their colors and directions)
*   box-shadow values: horizontal offset, vertical offset, blur radius, spread radius, color
*   width and height of selected element (although you won’t usually need these in a responsive design — more on this later)

### Limitations

The CSS panel doesn’t use the shorthand syntax for borders. As you can see in the screenshot below, border properties are separated into <code>border-color</code>, <code>border-width</code> and <code>border-style</code>.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2272eba1-e07f-4357-a386-121ce89288f6/css-properties-shorthand-500px.png" alt="Borders are not displayed with shorthand syntax." /><figcaption>The CSS panel doesn’t use the shorthand syntax for borders.</figcaption></figure>

Granted, getting the shortened declaration would be much easier:

<pre><code class="language-css">
 border: 1px solid rgba(43,75,133,1.0);
</code></pre>

That’s much cleaner than this:

<pre><code class="language-css">
 border-width: 1px;
 border-style: solid;
 border-color: rgba(43,75,133,1.0);
</code></pre>

I also recommend ignoring the <code>width</code> and <code>height</code> properties of objects reported in the panel, at least in most cases. Instead, use the <code>padding</code> CSS property. Let me explain.

Sample images in a mockup will often have particular widths and heights, whereas the actual elements used in the final design might vary. So, defining the padding (i.e. the distance between the content and the edge of the container) is better because then the element can be as small or as large as necessary to accommodate the content. You can set the size to be proportional or even assign minimum and maximum dimensions to control the container’s size.

Let’s see an example of why fixing the dimensions with <code>width</code> and <code>height</code> properties is not such a good idea for buttons:

*   We usually need text to be automatically centered in a button, but this won’t happen with fixed properties.
*   By setting the padding, you will have much better control if you have to change the text inside the button. We all know that clients are often indecisive about their copy; so, our buttons must support text of different lengths. Whether the button says “Connect with Facebook” or “Share with Facebook,” the padding will control the button’s width and height perfectly. (A bonus is that the button will adapt to whatever text size a user has set in their browser.)
*   [Responsive design](https://alistapart.com/article/responsive-web-design). ’nuff said.

Back to the CSS panel and its limitations.

Another issue was that the Fireworks panel had some bugs with the direction of gradients. Fortunately, these issues were corrected in the last update (<a href="https://blogs.adobe.com/fireworks/2013/06/fireworks-cs6-update-12-0-1-is-live.html">CS6 12.0.1</a>). Nevertheless, the CSS Properties panel might still display a few deprecated CSS declarations, which will increase the number of lines in your code and the weight of your CSS file.

So, while the CSS panel is very useful, it’s far from perfect. But guess what?! A <a title="Personal website of Matt Stow" href="https://mattstow.com">kind developer</a> who is passionate about Fireworks and clean, lightweight CSS has made a free extension that fixes many of the issues mentioned above. I’ll review his extension, <a href="https://mattstow.com/css-professionalzr.html">CSS Professionalizr</a>, in detail later in the article — but first, a few questions for Matt Stow, which he was so kind to answer in an email interview!

## Interlude: Interview With Matt Stow

<strong>Question: Hello Matt, and thanks for taking the time to answer my questions. First, could you introduce yourself in a few words to Smashing Magazine’s readers?</strong>

<strong>Matt:</strong> I’m Matt Stow, a 30-something English ex-pat living in Newcastle, Australia. I’m the senior UI developer for <a href="https://izilla.com.au">Izilla</a> and have been involved with computers since owning a <a href="https://en.wikipedia.org/wiki/ZX_Spectrum">ZX Spectrum</a> as a child.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45a8efda-5551-45af-8b1e-810b07efe00f/zx-pectrum48k-large.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/691dcf52-3db8-48c0-9d6f-141a8017a19e/zx-pectrum48k-500px.jpg" alt="" /></a><figcaption><a href="https://en.wikipedia.org/wiki/ZX_Spectrum">ZX Spectrum</a></figcaption></figure>

<strong>Question: When did you start using Fireworks? What’s your daily use of the app like?</strong>

<strong>Matt:</strong> I first started playing with Fireworks MX, but it wasn’t until Fireworks 8 was released in 2005 that it really grabbed my attention, quickly becoming my primary tool for designing and creating web assets. As I mainly do front-end development, I generally import our designers’ PSD files and export what I can as sprites, but I’ll often end up redrawing elements in Fireworks to achieve pixel-perfection and to easily convert them to CSS code.</p>

<strong>Question: Can you tell us how you started developing Fireworks extensions?</strong>

<strong>Matt:</strong> My first extension was my Frame Commands pack in early 2007. During the Fireworks CS3 prerelease cycle, I was doing a lot of frame-based animation and design, and I was frustrated by not being able to easily loop through my frames (now called “states”) with the keyboard. <a href="https://johndunning.com/fireworks/">John Dunning</a>, Fireworks extension developer extraordinaire, gave me some pointers on getting started with extending Fireworks, and it snowballed from there. I’ve created countless extensions since then, most of which address my own needs and improve the efficiency of my particular workflows. However, I’ve also taken requests from members of the community and built extensions for them.</p>

<strong>Question: Why did you decide to create an extension to improve Fireworks’ CSS Properties panel?</strong>

<strong>Matt:</strong> I’ve been writing CSS for over 10 years and am very particular about how it’s formatted and structured. While I admire what the Fireworks team achieved with the CSS Properties panel, the outputted code didn’t meet my standards as it was so verbose, and I knew the panel might not be updated regularly enough to keep pace with the landscape of modern browsers. My fears were well founded, too. Without CSS Professionalzr, gradients exported from Fireworks rendered incorrectly in Firefox 16+, IE 10+ and Opera 12.10+ (luckily, the Fireworks team resolved this with <a href="https://blogs.adobe.com/fireworks/2013/06/fireworks-cs6-update-12-0-1-is-live.html">its latest patch</a>, released in June 2013).

Adding base64 SVG gradients for IE 9 was another major reason for creating the extension.</p>

<strong>Question: Do you plan further updates to CSS Professionalzr?</strong>

<strong>Matt:</strong> Yes! I’ve just released an update (1.1) to deal with Fireworks CS6’s new patch, to improve SVG support and to remove other unnecessary vendor prefixes.

In the near future, I plan to add Sass and possibly LESS syntaxes, too. I want to include support for the mixins from my Sass framework, <a href="https://github.com/izilla/Suzi">Suzi</a>, <a href="https://compass-style.org">Compass</a> and <a href="https://bourbon.io">Bourbon</a>. Although I don’t personally use Compass, Bourbon or LESS, I want to help the community and would like it to help decide on which I should support first and to help test.</p>

<strong>Question: Last question, what do you think about Adobe’s recent decision to stop adding new features to Fireworks and not to include it in the new CC subscription model? What are the alternatives to Fireworks? (Or will you continue using it for now?)</strong>

<strong>Matt:</strong> It was inevitable. I’ve known Fireworks was doomed for a while now — Adobe just didn’t understand its potential. But does it matter? Even if Adobe isn’t adding new features, extension developers are giving it the life it deserves. For me, there still isn’t an alternative (especially on Windows) that does everything Fireworks can. So, until one comes along or I’m no longer being productive in Fireworks, I’ll continue to use it.</p>

<strong>Question: Thanks a lot, Matt. I’m sure our readers would be interested in getting in touch with you on the web, so drop us your links here.</strong>

<strong>Matt:</strong> Thank you, and I’d love to hear from them! You can visit <a href="https://mattstow.com">my website</a>, where I release my Fireworks and Dreamweaver extensions and also where I blog and release plugins for the web, especially for responsive web design. Alternatively, you can also <a href="https://twitter.com/stowball">follow me on Twitter</a>, where I do try to tweet web-related things.</p>

## CSS Professionalizr

### Features

<a href="https://mattstow.com/css-professionalzr.html">CSS Professionalizr</a> is a free extension that improves and extends the functionality of the CSS Properties panel in Fireworks. Here are some of the many enhancements that this extension brings to Fireworks:

*   It consolidates `border-color`, `border-style` and `border-width` into one shorthand `border` rule.
*   It removes `width` and `height` attributes (you won’t need these often).
*   It formats all of the properties consistently (with commas, colons, spaces, etc.) and removes redundant new lines, which could save you some lines of code. (While this step might seem unnecessary, in a medium-sized to large project, it will greatly affect the final weight of a CSS file.)
*   It uses the new syntax for unprefixed gradient properties.
*   It sorts all rules alphabetically — handy!
*   It converts linear gradients to `base64`. (In case you are not familiar with data URIs, then the article “[The What, Why and How of Data URIs in Web Design](https://webdesign.tutsplus.com/articles/the-what-why-and-how-of-data-uris-in-web-design--webdesign-8648)” will help.)

Another great point is that the extension removes deprecated declarations and unused properties, such as <code>-ms-gradients</code> and all filters for Internet Explorer. (<strong>Tip:</strong> If you want better CSS3 control in old versions of Internet Explorer, try <a href="https://css3pie.com/">PIE</a> instead!)

Finally, here are some of the improvements that Matt has added in version 1.1 of his extension:

*   fixed SVG generation (because the angles changed),
*   removed legacy `-webkit-border-radius` syntax,
*   removed legacy `-o-gradients` and the non-standard legacy `-webkit-gradient` syntax,
*   cleaned up the `-moz-gradient` rule.

(This version brought many more fixes, all of which you can check in the <a href="https://mattstow.com/css-professionalzr.html">version history</a>.)

## Using CSS Properties Panel With CSS Professionalzr: A Case Study

### Installation

1.  Download the `.MXP` file from the [CSS Professionalzr](https://mattstow.com/css-professionalzr.html) page.
2.  Double-click on `CSS-Professionalzr.mxp`, accept the license agreement, and install the extension.</p>

<strong>Hint:</strong> If you’re having any kind of problem installing the extension or you simply want to learn more about the basics of Fireworks extensions, Ashish Bogawat’s article “<a href="https://www.smashingmagazine.com/2012/08/28/fireworks-extensions-for-better-workflow/">Optimizing the Design Workflow With Fireworks Extensions</a>” (and specifically the section titled “Working With Extensions in Fireworks”) will give you quite a few valuable tips.

Now that CSS Professionalzr is installed, it’s time to try it out.</p>

### Let’s Create a Button

Suppose we need a certain social-media button for our next web project.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/463bad62-9e65-4047-a92b-2a864143accb/connect-with-fb-button-500px.png" alt="Connect with Facebook button" /><figcaption>“Connect with Facebook” button? Why not!</figcaption></figure>

Before we continue, I’d like to address one issue that some designers face when using Fireworks.</p>

### A Note About Strokes and Live Filters

Fireworks’ stroke feature gives us quite a lot of options, but the effect isn’t always consistent. As <a href="https://www.twitter.com/bdc">Benjamin de Cock</a> wrote in his very interesting article “<a href="https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/">Refining Your Design in Adobe Fireworks</a>,” using the “Align Stroke to Outside” option usually gives the best result. (To learn more, check out the section titled “Improve Fine Strokes” in Ben’s article.)

The detail I’d like to point out here is the combination of Fireworks’ stroke effect and the Inner Shadow live filter. To create a highlight effect, like in this example, you would use a white Inner Shadow live filter with a darker-colored stroke. The problem is that Fireworks would consider the shadow to start at the top of the button, <em>including</em> the stroke. This gives an unsightly result.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9065668-454b-4276-84af-cfe8b135f204/05.png" alt="2" /><figcaption>Notice where the Inner Shadow live filter effect starts.</figcaption></figure>

The border color and inner shadow are mixed together. This isn’t the behavior we want from the Inner Shadow live filter. Rather, we want the inner shadow to start <em>after</em> the stroke (as <code>box-shadow</code> does).

We could use a composite path instead of a stroke to create the border, which would give us better control of the result. It’s a good alternative, but the problem is that the CSS panel won’t be able to translate and retrieve the exact values of the effect because the values will come from a vector path and not from a live filter applied to the object.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b0de143-5987-4aed-bd74-293b05185ac7/04.png" alt="" /><figcaption>Things are looking much better in the alternative.</figcaption></figure>

All right, is there a good reliable solution? I believe there is. The trick is to use the stroke property from Photoshop’s Live Effects in Fireworks, instead of the native stroke-color option. Go to the Properties panel and then select “Live Filters” → “Add a Live Filter” → “Photoshop Live Effects” → “Stroke” and bingo!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7c25067-f212-433f-9685-1be307a0be16/ps-live-effects-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc71b2ac-2bc2-423e-9580-47ab395db495/ps-live-effects-500px.png" alt="Ps Live Effects filter option instead of Fw native stroke." /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7c25067-f212-433f-9685-1be307a0be16/ps-live-effects-large.png">View large version</a>)</figcaption></figure>

<strong>Tip:</strong> You’ll have to put the live filters in the right order or else this won’t work. (The Inner Shadow live filter should be first, then the stroke from Photoshop’s Live Effects.)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26a38283-1387-4932-9b71-96ce4e4aa3ed/07.png" alt="Recommended order of the live filters (Properties panel)." /><figcaption>This should be the order of the live filters.</figcaption></figure>

And here we are. Much better, isn’t it?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76e6da89-7c0f-4cc2-87ad-6d670e2a8337/08.png" alt="Before and after…" /><figcaption>Our button before (top) and after (bottom) — much better!</figcaption></figure>

Another potential problem with live filters in Fireworks is that the angles of drop shadows sometimes look slightly “cut” (especially when you use a large Drop Shadow live filter). It’s not a big problem because the CSS Properties panel will convert your live filter to a CSS <code>box-shadow</code> rule, which will display correctly in browsers. (<strong>Note:</strong> To fix cut angles on some drop shadows, many designers use a rectangle with the edge set to “Feather.” The shadow effect certainly looks smoother in Fireworks, but it results in the same issue when using a border made from a vector path: The CSS panel won’t be able to translate it into a CSS <code>box-shadow</code> rule because the shadow was made not with a live filter but with another vector object. In this case, a live filter is a much better option.)

### How to Get the CSS Information From Objects on the Canvas?

OK, so you have the perfect button in Fireworks. Now you would like to see its corresponding CSS properties. That’s easy.

First, open the CSS Properties panel (<code>Window → CSS Properties</code> in the menu or <code>Control/Command + F7</code> on the keyboard), select the object on the canvas, and see what the panel outputs:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a045053d-62cb-4dc5-9390-9b2c227ccbda/vector-object-and-css-panel-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc7b7ae6-fb64-46e7-a5c4-30a46b93c47b/vector-object-and-css-panel-500px.png" alt="Select the object on the canvas and check the CSS Properties panel." /></a><figcaption>Select the button on the canvas and check the CSS Properties panel.</figcaption></figure>

Let’s zoom around the panel a bit:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86b54638-645a-417c-b77e-cf63c1f47c33/fw-cs6-properties-panel.png" alt="CSS Properties panel in Fireworks CS6" /><figcaption>The CSS Properties panel in Fireworks CS6</figcaption></figure>

The CSS Properties panel is divided into two major sections. The top lists all of the CSS properties and their corresponding values, and the bottom is a simple box with all of the outputted CSS code (copying the code directly from this box is easy). Also, five checkboxes let you select whether to include browser-specific vendor prefixes — for Firefox, WebKit browsers, Opera and Internet Explorer — as well as CSS comments. In the bottom-right corner of the panel are two buttons, “All” and “Selected.” Pressing "All" will copy all of the code; if you hold <code>Control/Command</code> and select some of the properties (in the upper part of the panel) and then press the “Selected” button, only these will be copied to the clipboard.

As you can see, now that we’ve selected the button on the canvas, we have all the data needed to reproduce this element with CSS3 code. (Note: If you’re not sure about the browser support for some of the CSS3 properties that you’re planning to use, I recommend checking <a href="https://caniuse.com/#">Can I Use?</a>, an excellent resource!)

The CSS Properties panel works very effectively not only with vector shapes, but with text objects, too. The <code>text-shadow</code> property is supported (but <a href="https://caniuse.com/#feat=css-textshadow">not in Internet Explorer 9 and below</a>).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ae7f6af-afab-470e-ab39-142c26886a5a/text-object-and-css-panel-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/782ad8c5-670f-4b56-b79f-06d0cdd4da62/text-object-and-css-panel-500px.png" alt="Select a text object on the canvas and check its CSS properties." /></a><figcaption>Select a text object and check its CSS properties: <code>font-family</code>, <code>font-size</code>, <code>color</code>, etc.</figcaption></figure>

### How to Retrieve CSS Information With CSS Professionalzr

The process of retrieving information with CSS Professionalzr is pretty straightforward.

1.  On Fireworks’ canvas, select the object whose CSS3 properties you’d like to get.
2.  Open the CSS Properties panel (if you haven’t already). You will see the object’s CSS properties listed there. (Now is the time to decide whether to include browser vendor prefixes in your CSS and, if so, for which browsers. The panel will also let you select whether to include comments in the code.)
3.  Next, run the CSS Professionalzr command: in the menu, “Commands” → “CSS” → “CSS Profesionnalzr.” I recommend assigning a shortcut key for quick access to CSS Professionalzr, which is easily done by going in the menu to “Edit” → “Keyboard Shortcuts” on Windows or “Fireworks” → “Keyboard Shortcuts” on a Mac.
4.  CSS Professionalzr will take the CSS generated by Fireworks and consolidate its properties, fix the gradients, clean up and reduce the code, and then copy the clean code to your clipboard for you to use in a project.

Let’s review the code that the CSS Properties panel and CSS Professionalzr have outputted:

<pre><code class="language-css">
background: #4567ac;
background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHZpZXdCb3g9IjAgMCAxIDEiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjxsaW5lYXJHcmFkaWVudCBpZD0iZzIyOSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIwJSIgeTE9IjAlIiB4Mj0iMCUiIHkyPSIxMDAlIj48c3RvcCBzdG9wLWNvbG9yPSIjNjE4NGNlIiBvZmZzZXQ9IjAiLz48c3RvcCBzdG9wLWNvbG9yPSIjNDk2YWIxIiBvZmZzZXQ9IjAuNCIvPjxzdG9wIHN0b3AtY29sb3I9IiM0MzY0YWEiIG9mZnNldD0iMC40OSIvPjxzdG9wIHN0b3AtY29sb3I9IiM0NTY3YWMiIG9mZnNldD0iMSIvPjwvbGluZWFyR3JhZGllbnQ+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEiIGhlaWdodD0iMSIgZmlsbD0idXJsKCNnMjI5KSIgLz48L3N2Zz4=);
background: -moz-linear-gradient(-90deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
background: -webkit-linear-gradient(-90deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
background: linear-gradient(180deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
border-radius: 1px;
border: 1px solid #2c4c88;
-webkit-box-shadow: 0 1px 1px rgba(44,76,135,.65), inset 0 1px 1px rgba(255,255,255,.35);
box-shadow: 0 1px 1px rgba(44,76,135,.65), inset 0 1px 1px rgba(255,255,255,.35);
</code></pre>

In the snippet above, I have included the <code>-webkit</code> and <code>-moz</code> browser prefixes. Omitting them would make the code even more lightweight. Even better, the code will work just fine in all modern browsers:

<pre><code class="language-css">
background: #4567ac;
background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHZpZXdCb3g9IjAgMCAxIDEiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjxsaW5lYXJHcmFkaWVudCBpZD0iZzIyOSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIwJSIgeTE9IjAlIiB4Mj0iMCUiIHkyPSIxMDAlIj48c3RvcCBzdG9wLWNvbG9yPSIjNjE4NGNlIiBvZmZzZXQ9IjAiLz48c3RvcCBzdG9wLWNvbG9yPSIjNDk2YWIxIiBvZmZzZXQ9IjAuNCIvPjxzdG9wIHN0b3AtY29sb3I9IiM0MzY0YWEiIG9mZnNldD0iMC40OSIvPjxzdG9wIHN0b3AtY29sb3I9IiM0NTY3YWMiIG9mZnNldD0iMSIvPjwvbGluZWFyR3JhZGllbnQ+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEiIGhlaWdodD0iMSIgZmlsbD0idXJsKCNnMjI5KSIgLz48L3N2Zz4=);
background: linear-gradient(180deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
border-radius: 1px;
border: 1px solid #2c4c88;
box-shadow: 0 1px 1px rgba(44,76,135,.65), inset 0 1px 1px rgba(255,255,255,.35);
</code></pre>

As you can see, this code is much cleaner. Now, all you have to do is copy and paste the code in your CSS file et voilà!

### More Questions?

Do you have any other questions about how to use CSS Professionalzr? Matt has recorded a <a href="https://youtube.com/watch?v=iBzXt9Y6cBw">little screencast</a> that explains how to use the CSS panel with his extension. It should help in case you have some questions left.</p>

<iframe loading="lazy" src="//www.youtube.com/embed/iBzXt9Y6cBw" width="420" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
“Using the CSS Professionalzr Extension for Adobe Fireworks CS6” (screencast by Matt Stow)

### Live HTML and CSS Demo

Now, have a look at a <a href="https://pixelize.be/stuff/smashingmagazine/">live browser preview</a> of this demo button to see what we have achieved by exporting CSS properties right from within Fireworks CS6!

I think the result looks much better than the button we created in Fireworks.</p>

### A Quick Note on Font Rendering

<strong>Matt:</strong> It was inevitable. I’ve known Fireworks was doomed for a while now — Adobe just didn’t understand its potential. But does it matter? Even if Adobe isn’t adding new features, extension developers are giving it the life it deserves. For me, there still isn’t an alternative (especially on Windows) that does everything Fireworks can. So, until one comes along or I’m no longer being productive in Fireworks, I’ll continue to use it.</p>

<strong>Question: Thanks a lot, Matt. I’m sure our readers would be interested in getting in touch with you on the web, so drop us your links here.</strong>

<strong>Matt:</strong> Thank you, and I’d love to hear from them! You can visit <a href="https://mattstow.com">my website</a>, where I release my Fireworks and Dreamweaver extensions and also where I blog and release plugins for the web, especially for responsive web design. Alternatively, you can also <a href="https://twitter.com/stowball">follow me on Twitter</a>, where I do try to tweet web-related things.</p>

## CSS Professionalizr

### Features

<a href="https://mattstow.com/css-professionalzr.html">CSS Professionalizr</a> is a free extension that improves and extends the functionality of the CSS Properties panel in Fireworks. Here are some of the many enhancements that this extension brings to Fireworks:

*   It consolidates `border-color`, `border-style` and `border-width` into one shorthand `border` rule.
*   It removes `width` and `height` attributes (you won’t need these often).
*   It formats all of the properties consistently (with commas, colons, spaces, etc.) and removes redundant new lines, which could save you some lines of code. (While this step might seem unnecessary, in a medium-sized to large project, it will greatly affect the final weight of a CSS file.)
*   It uses the new syntax for unprefixed gradient properties.
*   It sorts all rules alphabetically — handy!
*   It converts linear gradients to `base64`. (In case you are not familiar with data URIs, then the article “[The What, Why and How of Data URIs in Web Design](https://webdesign.tutsplus.com/articles/the-what-why-and-how-of-data-uris-in-web-design--webdesign-8648)” will help.)

Another great point is that the extension removes deprecated declarations and unused properties, such as <code>-ms-gradients</code> and all filters for Internet Explorer. (<strong>Tip:</strong> If you want better CSS3 control in old versions of Internet Explorer, try <a href="https://css3pie.com/">PIE</a> instead!)

Finally, here are some of the improvements that Matt has added in version 1.1 of his extension:

*   fixed SVG generation (because the angles changed),
*   removed legacy `-webkit-border-radius` syntax,
*   removed legacy `-o-gradients` and the non-standard legacy `-webkit-gradient` syntax,
*   cleaned up the `-moz-gradient` rule.

(This version brought many more fixes, all of which you can check in the <a href="https://mattstow.com/css-professionalzr.html">version history</a>.)

## Using CSS Properties Panel With CSS Professionalzr: A Case Study

### Installation

1.  Download the `.MXP` file from the [CSS Professionalzr](https://mattstow.com/css-professionalzr.html) page.
2.  Double-click on `CSS-Professionalzr.mxp`, accept the license agreement, and install the extension.</p>

<strong>Hint:</strong> If you’re having any kind of problem installing the extension or you simply want to learn more about the basics of Fireworks extensions, Ashish Bogawat’s article “<a href="https://www.smashingmagazine.com/2012/08/28/fireworks-extensions-for-better-workflow/">Optimizing the Design Workflow With Fireworks Extensions</a>” (and specifically the section titled “Working With Extensions in Fireworks”) will give you quite a few valuable tips.

Now that CSS Professionalzr is installed, it’s time to try it out.</p>

### Let’s Create a Button

Suppose we need a certain social-media button for our next web project.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/463bad62-9e65-4047-a92b-2a864143accb/connect-with-fb-button-500px.png" alt="Connect with Facebook button" /><figcaption>“Connect with Facebook” button? Why not!</figcaption></figure>

Before we continue, I’d like to address one issue that some designers face when using Fireworks.</p>

### A Note About Strokes and Live Filters

Fireworks’ stroke feature gives us quite a lot of options, but the effect isn’t always consistent. As <a href="https://www.twitter.com/bdc">Benjamin de Cock</a> wrote in his very interesting article “<a href="https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/">Refining Your Design in Adobe Fireworks</a>,” using the “Align Stroke to Outside” option usually gives the best result. (To learn more, check out the section titled “Improve Fine Strokes” in Ben’s article.)

The detail I’d like to point out here is the combination of Fireworks’ stroke effect and the Inner Shadow live filter. To create a highlight effect, like in this example, you would use a white Inner Shadow live filter with a darker-colored stroke. The problem is that Fireworks would consider the shadow to start at the top of the button, <em>including</em> the stroke. This gives an unsightly result.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9065668-454b-4276-84af-cfe8b135f204/05.png" alt="2" /><figcaption>Notice where the Inner Shadow live filter effect starts.</figcaption></figure>

The border color and inner shadow are mixed together. This isn’t the behavior we want from the Inner Shadow live filter. Rather, we want the inner shadow to start <em>after</em> the stroke (as <code>box-shadow</code> does).

We could use a composite path instead of a stroke to create the border, which would give us better control of the result. It’s a good alternative, but the problem is that the CSS panel won’t be able to translate and retrieve the exact values of the effect because the values will come from a vector path and not from a live filter applied to the object.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b0de143-5987-4aed-bd74-293b05185ac7/04.png" alt="" /><figcaption>Things are looking much better in the alternative.</figcaption></figure>

All right, is there a good reliable solution? I believe there is. The trick is to use the stroke property from Photoshop’s Live Effects in Fireworks, instead of the native stroke-color option. Go to the Properties panel and then select “Live Filters” → “Add a Live Filter” → “Photoshop Live Effects” → “Stroke” and bingo!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7c25067-f212-433f-9685-1be307a0be16/ps-live-effects-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc71b2ac-2bc2-423e-9580-47ab395db495/ps-live-effects-500px.png" alt="Ps Live Effects filter option instead of Fw native stroke." /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7c25067-f212-433f-9685-1be307a0be16/ps-live-effects-large.png">View large version</a>)</figcaption></figure>

<strong>Tip:</strong> You’ll have to put the live filters in the right order or else this won’t work. (The Inner Shadow live filter should be first, then the stroke from Photoshop’s Live Effects.)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26a38283-1387-4932-9b71-96ce4e4aa3ed/07.png" alt="Recommended order of the live filters (Properties panel)." /><figcaption>This should be the order of the live filters.</figcaption></figure>

And here we are. Much better, isn’t it?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76e6da89-7c0f-4cc2-87ad-6d670e2a8337/08.png" alt="Before and after…" /><figcaption>Our button before (top) and after (bottom) — much better!</figcaption></figure>

Another potential problem with live filters in Fireworks is that the angles of drop shadows sometimes look slightly “cut” (especially when you use a large Drop Shadow live filter). It’s not a big problem because the CSS Properties panel will convert your live filter to a CSS <code>box-shadow</code> rule, which will display correctly in browsers. (<strong>Note:</strong> To fix cut angles on some drop shadows, many designers use a rectangle with the edge set to “Feather.” The shadow effect certainly looks smoother in Fireworks, but it results in the same issue when using a border made from a vector path: The CSS panel won’t be able to translate it into a CSS <code>box-shadow</code> rule because the shadow was made not with a live filter but with another vector object. In this case, a live filter is a much better option.)

### How to Get the CSS Information From Objects on the Canvas?

OK, so you have the perfect button in Fireworks. Now you would like to see its corresponding CSS properties. That’s easy.

First, open the CSS Properties panel (<code>Window → CSS Properties</code> in the menu or <code>Control/Command + F7</code> on the keyboard), select the object on the canvas, and see what the panel outputs:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a045053d-62cb-4dc5-9390-9b2c227ccbda/vector-object-and-css-panel-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc7b7ae6-fb64-46e7-a5c4-30a46b93c47b/vector-object-and-css-panel-500px.png" alt="Select the object on the canvas and check the CSS Properties panel." /></a><figcaption>Select the button on the canvas and check the CSS Properties panel.</figcaption></figure>

Let’s zoom around the panel a bit:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86b54638-645a-417c-b77e-cf63c1f47c33/fw-cs6-properties-panel.png" alt="CSS Properties panel in Fireworks CS6" /><figcaption>The CSS Properties panel in Fireworks CS6</figcaption></figure>

The CSS Properties panel is divided into two major sections. The top lists all of the CSS properties and their corresponding values, and the bottom is a simple box with all of the outputted CSS code (copying the code directly from this box is easy). Also, five checkboxes let you select whether to include browser-specific vendor prefixes — for Firefox, WebKit browsers, Opera and Internet Explorer — as well as CSS comments. In the bottom-right corner of the panel are two buttons, “All” and “Selected.” Pressing "All" will copy all of the code; if you hold <code>Control/Command</code> and select some of the properties (in the upper part of the panel) and then press the “Selected” button, only these will be copied to the clipboard.

As you can see, now that we’ve selected the button on the canvas, we have all the data needed to reproduce this element with CSS3 code. (Note: If you’re not sure about the browser support for some of the CSS3 properties that you’re planning to use, I recommend checking <a href="https://caniuse.com/#">Can I Use?</a>, an excellent resource!)

The CSS Properties panel works very effectively not only with vector shapes, but with text objects, too. The <code>text-shadow</code> property is supported (but <a href="https://caniuse.com/#feat=css-textshadow">not in Internet Explorer 9 and below</a>).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ae7f6af-afab-470e-ab39-142c26886a5a/text-object-and-css-panel-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/782ad8c5-670f-4b56-b79f-06d0cdd4da62/text-object-and-css-panel-500px.png" alt="Select a text object on the canvas and check its CSS properties." /></a><figcaption>Select a text object and check its CSS properties: <code>font-family</code>, <code>font-size</code>, <code>color</code>, etc.</figcaption></figure>

### How to Retrieve CSS Information With CSS Professionalzr

The process of retrieving information with CSS Professionalzr is pretty straightforward.

1.  On Fireworks’ canvas, select the object whose CSS3 properties you’d like to get.
2.  Open the CSS Properties panel (if you haven’t already). You will see the object’s CSS properties listed there. (Now is the time to decide whether to include browser vendor prefixes in your CSS and, if so, for which browsers. The panel will also let you select whether to include comments in the code.)
3.  Next, run the CSS Professionalzr command: in the menu, “Commands” → “CSS” → “CSS Profesionnalzr.” I recommend assigning a shortcut key for quick access to CSS Professionalzr, which is easily done by going in the menu to “Edit” → “Keyboard Shortcuts” on Windows or “Fireworks” → “Keyboard Shortcuts” on a Mac.
4.  CSS Professionalzr will take the CSS generated by Fireworks and consolidate its properties, fix the gradients, clean up and reduce the code, and then copy the clean code to your clipboard for you to use in a project.

Let’s review the code that the CSS Properties panel and CSS Professionalzr have outputted:

<pre><code class="language-css">
background: #4567ac;
background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHZpZXdCb3g9IjAgMCAxIDEiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjxsaW5lYXJHcmFkaWVudCBpZD0iZzIyOSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIwJSIgeTE9IjAlIiB4Mj0iMCUiIHkyPSIxMDAlIj48c3RvcCBzdG9wLWNvbG9yPSIjNjE4NGNlIiBvZmZzZXQ9IjAiLz48c3RvcCBzdG9wLWNvbG9yPSIjNDk2YWIxIiBvZmZzZXQ9IjAuNCIvPjxzdG9wIHN0b3AtY29sb3I9IiM0MzY0YWEiIG9mZnNldD0iMC40OSIvPjxzdG9wIHN0b3AtY29sb3I9IiM0NTY3YWMiIG9mZnNldD0iMSIvPjwvbGluZWFyR3JhZGllbnQ+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEiIGhlaWdodD0iMSIgZmlsbD0idXJsKCNnMjI5KSIgLz48L3N2Zz4=);
background: -moz-linear-gradient(-90deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
background: -webkit-linear-gradient(-90deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
background: linear-gradient(180deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
border-radius: 1px;
border: 1px solid #2c4c88;
-webkit-box-shadow: 0 1px 1px rgba(44,76,135,.65), inset 0 1px 1px rgba(255,255,255,.35);
box-shadow: 0 1px 1px rgba(44,76,135,.65), inset 0 1px 1px rgba(255,255,255,.35);
</code></pre>

In the snippet above, I have included the <code>-webkit</code> and <code>-moz</code> browser prefixes. Omitting them would make the code even more lightweight. Even better, the code will work just fine in all modern browsers:

<pre><code class="language-css">
background: #4567ac;
background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHZpZXdCb3g9IjAgMCAxIDEiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjxsaW5lYXJHcmFkaWVudCBpZD0iZzIyOSIgZ3JhZGllbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIHgxPSIwJSIgeTE9IjAlIiB4Mj0iMCUiIHkyPSIxMDAlIj48c3RvcCBzdG9wLWNvbG9yPSIjNjE4NGNlIiBvZmZzZXQ9IjAiLz48c3RvcCBzdG9wLWNvbG9yPSIjNDk2YWIxIiBvZmZzZXQ9IjAuNCIvPjxzdG9wIHN0b3AtY29sb3I9IiM0MzY0YWEiIG9mZnNldD0iMC40OSIvPjxzdG9wIHN0b3AtY29sb3I9IiM0NTY3YWMiIG9mZnNldD0iMSIvPjwvbGluZWFyR3JhZGllbnQ+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEiIGhlaWdodD0iMSIgZmlsbD0idXJsKCNnMjI5KSIgLz48L3N2Zz4=);
background: linear-gradient(180deg, #6184ce 0%, #496ab1 40%, #4364aa 49%, #4567ac 100%);
border-radius: 1px;
border: 1px solid #2c4c88;
box-shadow: 0 1px 1px rgba(44,76,135,.65), inset 0 1px 1px rgba(255,255,255,.35);
</code></pre>

As you can see, this code is much cleaner. Now, all you have to do is copy and paste the code in your CSS file et voilà!

### More Questions?

Do you have any other questions about how to use CSS Professionalzr? Matt has recorded a <a href="https://youtube.com/watch?v=iBzXt9Y6cBw">little screencast</a> that explains how to use the CSS panel with his extension. It should help in case you have some questions left.</p>

<iframe loading="lazy" src="//www.youtube.com/embed/iBzXt9Y6cBw" width="420" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
“Using the CSS Professionalzr Extension for Adobe Fireworks CS6” (screencast by Matt Stow)

### Live HTML and CSS Demo

Now, have a look at a <a href="https://pixelize.be/stuff/smashingmagazine/">live browser preview</a> of this demo button to see what we have achieved by exporting CSS properties right from within Fireworks CS6!

I think the result looks much better than the button we created in Fireworks.</p>

### A Quick Note on Font Rendering

Fonts might render in the browser slightly differently than in your Fireworks PNG file, which is to be expected. Fireworks, Photoshop and Illustrator (which, by the way, share the same text-rendering engine: Adobe Type Engine, or ATE) cannot render and preview fonts in the same way that fonts will be rendered by browsers. Font rendering varies between graphic design apps (Fireworks, Photoshop, Illustrator, Sketch, GIMP and so on) and between browsers (and browser versions) on various operating systems (Windows, Mac OS X, iOS, Android, Windows Phone, etc.).

However, you can still control (to some extent) how text looks when previewed in Fireworks by adjusting the “Anti-aliasing level” setting in the Properties panel. The available options are “Crisp anti-alias,” “Strong anti-alias,” “Smooth anti-alias,” “No anti-alias” and “Custom.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/625f4e5c-cc28-4ca3-8103-ef12e74b0184/fw-cs6-anti-aliasing-settings-500px.png" alt="Anti-alising settings in Fireworks" /></figure>

In the Properties panel, you can adjust the anti-aliasing method that Fireworks applies to a block of text. here is the drop-down menu that shows all of the options.

None of the anti-aliasing settings will perfectly match the text rendering in a real browser, but depending on your goal and the selected font, you can still achieve a pretty good result; just play a bit and explore the options. (<a title="Ivo Mynttinen" href="https://www.smashingmagazine.com/author/ivo-mynttinen/">Ivo Mynttinen</a> shares some tips for working with text in Fireworks in his article “<a href="https://ivomynttinen.com/blog/how-to-achieve-pixel-perfection-in-your-designs-with-adobe-fireworks/">How to Achieve Pixel Perfection in Your Designs With Adobe Fireworks</a>,” particularly the section “Get the Most Out of Your Text.”)

<strong>Note:</strong> Of course, “Anti-aliasing level” won’t have any effect on the CSS code that you’ll get from the CSS Properties panel in Fireworks. It will only affect the rendering of text on the canvas.</p>

## Alternatives To Fireworks’ CSS Properties Panel

Fireworks’ CSS Properties panel is not a unique feature in the world of graphic design apps. Also, the fact that Fireworks’ development was feature-frozen recently means that many designers will have to look for alternatives. I’ll review a couple of them here.</p>

### Copy CSS

Recently, a “<a href="https://helpx.adobe.com/photoshop/using/copy-css-shape-or-text.html">Copy CSS</a>” feature was added to Photoshop CC, although it’s a bit more limited than Fireworks’ CSS Properties panel. The feature generates CSS code from shape or text layers. For shapes, it captures values for size, position, stroke color, fill color and drop shadows. For text layers, it also captures font family, font size, font weight, line height, underlining and text alignment. (Note that Photoshop CC is available only as part of an Adobe Creative Cloud (CC) subscription, whereas you can still use Fireworks CS6 as a standalone app. If you have an Adobe CC subscription, you may download and use Fireworks as well as part of your subscription.)

### Creative Cloud Extract

This year, Adobe released some new Creative Cloud functionality and integrated it with Dreamweaver CC. While in beta, the feature was called “Project Parfait,” but later it was renamed to <a href="https://www.adobe.com/creativecloud/extract.html">Creative Cloud Extract</a>. With CC Extract, Web designers can view PSD files in Dreamweaver CC and use contextual code hinting to define fonts, colors and gradients in their CSS. CC Extract works only with Photoshop PSD files and requires a CC subscription.</p>

### Sketch

Since <a href="https://blog.mengto.com/the-best-hidden-features-in-sketch/">version 2.2</a>, the <a href="https://www.bohemiancoding.com/sketch/">Sketch</a> app has has implemented a feature to extract CSS properties (in Sketch, it’s simply called “Copy CSS”). It was further improved in Sketch 3.</p>

### CSS Hat

If you are using Photoshop, there is a third-party CSS-exporting tool you could try. It’s called <a href="https://csshat.com/">CSS Hat</a>, and it performs tasks similar to Fireworks’ CSS Properties panel. The price is around $35 and the latest version of it (2.0) works with Photoshop CC 2014 only.</p>

### Specctr

Also, plugins such as <a href="https://www.specctr.com/products">Specctr</a> allow you to export CSS code for objects created in some Adobe CC and CS6 apps. Specctr 2.0 has both paid and free versions and is compatible with Fireworks, Photoshop, Illustrator and InDesign. Only the Photoshop, Illustrator and InDesign versions have a feature to extract CSS, though, because the last Fireworks version of the plugin is 1.6. (Recently, Smashing Magazine published a couple of articles about Specctr: “<a href="https://www.smashingmagazine.com/2012/05/25/blueprints-for-the-web-specctr-adobe-fireworks-plugin/">Blueprints for the Web: Specctr Adobe Fireworks Plugin</a>” and “<a href="https://www.smashingmagazine.com/2013/11/15/specctr-an-adobe-illustrator-plugin-freebie/">Blueprints for Web and Print: Specctr, a Free Adobe Illustrator Plugin</a>.”)

Did I miss any similar tools? Let me know in the comments!

## Conclusion

The CSS Properties panel in Fireworks and CSS Professionalzr are simple yet powerful tools to extract CSS code from vector and text objects on a canvas. Designing a UI element and then copying and pasting the corresponding CSS3 code is definitely one of my favorite native features in Fireworks CS6. How it could be faster or easier than that?

Of course, the panel does not replace your favorite code editor, nor does it help you to write better, more <a href="https://learn.shayhowe.com/html-css/getting-to-know-html/">semantically correct HTML</a>. Still, together with CSS Professionalzr, it will help you to quickly view the CSS properties of the objects on the canvas. You can also use the extracted code during the development stage. It’s a time-saving feature that will make the life of both designers and developers a bit easier.</p>

### Further Reading

Finally, for those of you interested in learning more, here are a few useful resources related to the topics covered in this article:

*   [CSS Professionalzr](https://mattstow.com/css-professionalzr.html), Matt Stow
*   “[Extracting CSS Properties From Design Objects in Fireworks](https://helpx.adobe.com/fireworks/learn/tutorials/how-to/extract-css-properties.html),” Shubhashri C. G., Adobe Fireworks Tutorials
*   “[CSS3 Support: Extraction](https://tv.adobe.com/watch/learn-fireworks-cs6/css3-support-extraction/),” Patrick Foster, Adobe TV
*   “[Improved CSS Support](https://tv.adobe.com/watch/learn-fireworks-cs6/improved-css-suppport/)”, Patrick Foster, Adobe TV
*   “[Refining Your Design in Adobe Fireworks](https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/),” Benjamin de Cock, Smashing Magazine
*   “[How to Achieve Pixel Perfection in Your Designs With Adobe Fireworks](https://ivomynttinen.com/blog/how-to-achieve-pixel-perfection-in-your-designs-with-adobe-fireworks/),” Ivo Mynttinen
*   “[Designing a Rocket Icon in Adobe Fireworks](https://www.smashingmagazine.com/2014/09/23/designing-a-rocket-icon-in-adobe-fireworks/),” Fabio Benedetti, Smashing Magazine
*   “[Useful Adobe Fireworks Resources, Part 1: Extensions](https://www.smashingmagazine.com/2014/07/18/useful-adobe-fireworks-resources-extensions-part1/),” Michel Bozgounov, Smashing Magazine
*   “[Useful Adobe Fireworks Resources, Part 2: Tutorials, Articles and Freebies](https://www.smashingmagazine.com/2014/08/07/useful-adobe-fireworks-resources-tutorials-articles-freebies-part2/),” Michel Bozgounov, Smashing Magazine
*   “[Mojo Motors’ Responsive Redesign With Fireworks: UX and Interaction Design Stage](https://www.smashingmagazine.com/2013/08/26/mojo-motors-responsive-redesign-with-adobe-fireworks-part-1/),” Olawale Oladunni, Smashing Magazine
*   “[Mojo Motors’ Responsive Redesign With Fireworks: Visual Design Stage](https://www.smashingmagazine.com/2014/03/24/mojo-motors-responsive-redesign-with-adobe-fireworks-part-2/),” Olawale Oladunni, Smashing Magazine
*   “[About HTML Semantics and Front-End Architecture](https://nicolasgallagher.com/about-html-semantics-front-end-architecture/),” Nicolas Gallagher
*   “[Semantic Code: What? Why? How?](https://boagworld.com/dev/semantic-code-what-why-how/),” Paul Boag
*   “[Cutting Down on Vendor Prefixes](https://www.456bereastreet.com/archive/201311/cutting_down_on_vendor_prefixes/),” Roger Johansson, 456 Berea Street

<em>(Note: A big thanks to <a href="https://www.smashingmagazine.com/author/michel-bozgounov/">Michel</a> and <a href="https://www.mattstow.com/">Matt</a> for helping me with this article.)</em>

{{< signature "mb, al" >}}

