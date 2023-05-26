---
title: Harnessing Flexbox For Today's Web Apps
slug: harnessing-flexbox-for-todays-web-apps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c53a77cd-d54b-42a4-a24a-f3b735449cb3/harnessing-flexbox-for-todays-web-apps.jpg
date: 2015-03-02T23:18:10.000Z
author: karenmenezes
description: >-
  Although the syntax might be initially confounding, flexbox lives up to its
  name. It creates intelligent boxes that are stretchable, squeezable and
  capable of changing visual order. It provides simple solutions to layout
  paradigms that CSS has always struggled with: vertical centering and equal
  heights.
categories:
  - Coding
  - Tools
  - Layouts
  - CSS
  - Flexbox
---
Although the syntax might be initially confounding, <a title="Flexbox Is As Easy As Pie – Designing CSS Layouts" href="https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/">flexbox</a> lives up to its name. It creates intelligent boxes that are stretchable, squeezable and capable of changing visual order. It provides simple solutions to layout paradigms that CSS has always struggled with: vertical centering and equal heights. Flex items are truly accommodating and a pleasure to work with.

<a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox">Chris Coyier sums up flexbox</a> nicely:
<blockquote>The <code>Flexbox Layout</code> (Flexible Box) module (currently a W3C Last Call Working Draft) aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word "flex").

The main idea behind the flex layout is to give the container the ability to alter its items’ width/height (and order) to best fill the available space (mostly to accommodate to all kind of display devices and screen sizes). A flex container expands items to fill available free space, or shrinks them to prevent overflow.</blockquote>

Flexbox truly shines with HTML5 web applications. Most web apps consist of a series of modular, reusable components. You can use flexbox for those bits of layout that induce headaches and that depend on brittle CSS hacks to work. Small modules work very well with flexbox, and you can use floats and other tools for broader sections of the layout.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)
*   [<span class="headline">The Flexbox Reading List: Techniques And Tools</span>](https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/)
*   [CSS Grid, Flexbox And Box Alignment](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [Laying Out A Flexible Future For Web Design With Flexbox](https://www.smashingmagazine.com/2015/08/flexible-future-for-web-design-with-flexbox/)

{{% feature-panel %}}

I’m using flexbox in a big way for a web app that I’m currently working on, and I am very pleased with how it handles layout and box calculations intelligently. I’d like to share some demos and examples of this — any feedback would be appreciated.

This article presumes that you have working knowledge of flexbox. A wealth of information is available online. Keep in mind that the specification has undergone several changes over the years.

There are three versions of flexbox, largely differentiated by the syntax changes between 2009 and 2012:

1.  The **new** syntax is in sync with the current specification (e.g. `display: flex`).
2.  The **tweener** syntax is an unofficial syntax from 2012, adopted only by IE 10 (e.g. `display: -ms-flexbox`).
3.  The **old** syntax is from 2009 (e.g. `display: box`).</p>

## Browser Support

Let’s look in detail at which browsers support which syntax, <a href="https://caniuse.com/#search=flexbox">courtesy of Can I Use</a>.</p>

### Browsers That Support the New Syntax

<strong>Desktop:</strong>

*   _Unprefixed:_ Chrome 29+, Firefox 28+, IE 11+, Opera 17+
*   _Prefixed:_ `-webkit-` prefix for Chrome 21+, Safari 6.1+, Opera 15+

<strong>Note:</strong> Old versions of Firefox (22 to 27) support the new syntax minus the <code>flex-wrap</code> and <code>flex-flow</code> properties. Opera (12.1+ and 17+) supports flexbox without vendor prefixes, but intermediate versions 15 and 16 require vendor prefixes.

<strong>Touch:</strong>

*   _Unprefixed:_ Android 4.4+, Opera mobile 12.1+, BlackBerry 10+, Chrome for Android 39+, Firefox for Android 33+, IE 11+ mobile
*   _Prefixed:_ `-webkit-` prefix for iOS 7.1+

Almost all of the browsers mentioned above have old versions that support a prior variant of flexbox, minus some properties such as <code>flex-wrap</code> and <code>flex-flow</code> (the latter of which is a shorthand for the <code>flex-direction</code> and <code>flex-wrap</code> properties). By avoiding <code>flex-wrap</code> (and, therefore, using flexbox in multi-line layouts), we get amazing browser support, merging the old and current syntax.</p>

### Browsers That Support the Tweener Syntax

<strong>Desktop and touch:</strong> IE 10 (with <code>-ms-</code> vendor prefix)

### Browsers That Support the Old Syntax

All of these desktop and touch browsers require the <code>-webkit-</code> vendor prefix (except for Firefox, which needs the <code>-moz-</code> prefix).

<strong>Desktop:</strong> Firefox 2 – 21, Chrome 4 – 20, Safari 3.1 – 6

<strong>Touch:</strong> Android 2.1 – 4.3, iOS 3.2 – 6.1, UC browser 9.9 on Android, BlackBerry 7

For modern browsers that auto-update (i.e. desktop Chrome, Firefox, IE and Opera), the new syntax works out of the box.</p>

### Browsers That Don’t Support Flexbox

<strong>Desktop:</strong> Old versions of IE (9) and Opera (12)

<strong>Touch:</strong> Opera Mini

If you’re getting intimidated by the number of vendor prefixes and changes in syntax, have a look at <a href="https://css-tricks.com/using-flexbox">Chris Coyier’s recommendation</a>.

You can also use the following tools to get the best browser support via vendor prefixes:

*   [Autoprefixer](https://github.com/postcss/autoprefixer) With this general-purpose tool for vendor prefixing, you write the CSS or use a preprocessor, and it does what’s needed.
*   [Sass flexbox mixins](https://github.com/mastastealth/sass-flex-mixin)
*   **Less**.  The LESS mixin comes in two flavors: [with](https://gist.github.com/kenstone/5460000) and [without](https://gist.github.com/jayj/4012969) the tweener syntax for IE 10.

I would recommend Autoprefixer from among these. I haven’t experimented with the other preprocessor-specific solutions and welcome feedback if you have. Note that if you’re using a mixin with a helper library (such as Bourbon or Compass for Sass, Nib for Stylus or LESS Hat for LESS), it comes built in with vendor-prefix support for flexbox.

With a tool like Autoprefixer, you actually get great support across the board for flexbox, save for IE 9 and Opera Mini. Of course, you’ll need to thoroughly test your app across all browsers to make sure that the different syntaxes hold up.

Let’s look at a few good <strong>use cases for flexbox with web app modules</strong>.

## 1\. Unknown Number Of Children Within A Parent

<strong>Use case:</strong> My app has search filters. The number of search filters depends on whether a user is signed in. Anonymous users see two filters (“Popular” and “Latest”), while signed-in users see four (“Starred” and “Favorites”, additionally).

<strong>Issue:</strong> I’d like the styling to accommodate both options, without any change to the CSS.

<strong>Discussion:</strong> You’d generally have an <code>if</code> statement in your template to handle the state for signed-in users. If you were using floats for the layout, you’d have to set a width of 50% for the filters for anonymous users and a width of 25% for the filters for signed-in users.

<strong>Solution:</strong> With flexbox, you can just make the parent a flex container by declaring <code>display: flex</code> and give the children the property of <code>flex</code> and a value of <code>1</code>, which would make each of the children take up equal widths inside their parent. So, the CSS would remain the same no matter the view. Remember that the <code>flex</code> property is a shorthand for <a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox"><code>flex-grow</code>, <code>flex-shrink</code> and <code>flex-basis</code></a>.

<strong>Demo:</strong>

See the Pen [Flexbox: Parents with an unknown number of children](https://codepen.io/imohkay/pen/vENEEe/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/vENEEe/">Flexbox: Parents with an unknown number of children</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

## 2\. Inputs With Icons

<strong>Use case:</strong> I wish to add meaningful icons to my form inputs.

<strong>Issue:</strong> I want an elegant, flexible solution that works without having to declare unnecessary heights and widths on the elements.

<strong>Discussion:</strong> This one’s a classic problem. Different front-end frameworks approach this differently, generally using <code>display: table-cell</code> or absolute positioning.

<strong>Solution:</strong> Here’s the flexbox way. All we need to do is wrap the input and the icon besides it in a parent with <code>display: flex</code>. Then, we apply <code>flex: 1</code> to the input, so that it takes up the remaining space of the parent, minus the width of the icon.

<strong>Demo</strong> (using Font Awesome font icons via the CDN for convenience):

See the Pen [Flexbox: Inputs with icons](https://codepen.io/imohkay/pen/QwjwwY/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/QwjwwY/">Flexbox: Inputs with icons</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

## 3\. Visual Order

Flexbox can be used to change the visual order of a document, leaving <a href="https://www.w3.org/TR/css3-flexbox/#flow-order">speech order and navigation intact</a> according to the document’s source order. Our job as developers is to <em>responsibly</em> use the immense power of flexbox’s ordering mechanisms.

In fact, we can structure our documents with a source order that is appropriate to assistive technologies such as screen readers (for example, putting the sidebar before the main content in the source order), and use flexbox to simply alter the visual order for those who enjoy the benefits of a graphical user interface (by placing the sidebar on the right of the main content via the <code>order</code> or <code>flex-direction</code> property). Let’s look at this in detail.</p>

### A. Visual Order Independence With Flex-Direction

<strong>Use case:</strong> I have a sidebar positioned to the right of the main content section. On small screens, I want the sidebar to be at the top of the main content, reversing the order.

<strong>Issue:</strong> I don’t want to use JavaScript or a CSS hack to change the visual order.

<strong>Discussion:</strong> Flexbox is agnostic about the order in a layout. This makes it a miraculous tool for responsive layouts. We can do this in two ways: using the <code>flex-direction</code> property or the <code>order</code> property. Let’s look at the first option here.

<strong>Solution:</strong> Let’s build the layout with the sidebar as the first section in our markup. This is logical for two reasons: It adheres to the principle of a mobile-first layout, and it is beneficial to screen readers because the sidebar links are first in the source order. Let’s declare <code>flex-direction: column</code> on the parent (because <code>row</code> is the default). In our media query for large screens, we’ll change <code>flex-direction</code> to <code>row-reverse</code>, which solves our issue.

As a bonus, we’ll throw in a fixed-width sidebar (which is always 180 pixels on large screens and full width on mobile).

<strong>Demo:</strong>

See the Pen [Flexbox: Sidebar with source order independence using flex-direction](https://codepen.io/imohkay/pen/JoYoRE/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/JoYoRE/">Flexbox: Sidebar with source order independence using flex-direction</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

### B. Visual Order Independence With the Order Property

Our use case and issue are the same as in the example above.

<strong>Discussion:</strong> The <code>order</code> property provides more fine-grained control over the visual order than <code>flex-direction</code>.

<strong>Solution:</strong> We’ll declare <code>flex-direction: column</code> on the parent to stack both the columns on mobile. Then, on a <code>min-width</code> media query, we’ll change the <code>flex-direction</code> to <code>row</code>, which will show the sidebar on the left and the main content on the right. To reverse the order, we simply declare <code>order: 1</code> on the main content and <code>order: 2</code> on the sidebar!

<strong>Demo:</strong>

See the Pen [Flexbox: Sidebar with source order independence using order](https://codepen.io/imohkay/pen/VYvYKM/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/VYvYKM/">Flexbox: Sidebar with source order independence using order</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

### C. Toggling Ascending and Descending Order

<strong>Use case:</strong> I want to show a list of the five highest-paid actors in Hollywood in 2013, allowing their order to be toggled.

<strong>Issue:</strong> I want to do this in pure CSS and I can’t explain why, but I’m not sure it’s even possible.

<strong>Discussion:</strong> This is a simple no-JavaScript demo to show how powerful flexbox can be. Perhaps a bit impractical and crazy, but let’s see if there’s a way.

<strong>Solution:</strong> We’ll add a checkbox input with a label, which we’ll use to toggle the order from lowest to highest. Below this, we’ll add a list of the actors. Using the <code>:checked</code> CSS pseudo-class selector, we select the immediate <code>ul</code> sibling of the checkbox in order to reverse the direction of the unordered list’s items (by using <code>flex-direction: column-reverse</code>). It’s weird but it works perfectly, unless you’re using a screen reader or the keyboard for navigation. In the demo below, check the box and use the keyboard to navigate to see the implications of this. The specification mentions that the <a href="https://www.w3.org/TR/css3-flexbox/#order-accessibility"><code>order</code> property affects neither <code>tabindex</code> nor non-visual media such as speech.</a> Therefore, I wouldn’t recommend this solution for a real-world project. Perhaps it would come in handy in a quick prototype.

Note: <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=812687">Firefox has a bug</a> in its current version (version 34 on Ubuntu and Mac OS X, version 33 on Windows) that results in the <code>tabindex</code> complying with the flex order and not the source order. You can look at the <a href="https://sprungmarker.de/wp-content/uploads/css-a11y-group/css-a11y-flexbox.html#newspec">test cases</a> for the CSS Accessibility Community Group.

<strong>Demo:</strong>

See the Pen [Flexbox: Toggling a list's order](https://codepen.io/imohkay/pen/QwjwKP/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/QwjwKP/">Flexbox: Toggling a list's order</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

## 4\. The Comment Module

<strong>Use case:</strong> I have a typical comment module, with an image to the left and content on the right. The image avatar is always the same width and height (i.e. it’s not responsive).

<strong>Issue:</strong> I’m using flexbox, but the content overlaps the image:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8090ec-d9ff-4417-bda3-4889df71bed5/1-flexbox-comments-overlap-opt.jpg" alt="flexbox-comments-overlap" /></figure>

If you set <code>max-width</code> to <code>100%</code> and <code>height</code> to <code>auto</code> on the image, you will end up with the following:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e38f9e12-99a8-4d3d-a8bd-41cf1fd9de5e/2-flexbox-comments-max-width-opt.jpg" alt="flexbox-comments-max-width" /></figure>

<strong>Discussion:</strong> This example is similar to the “Inputs with icons” demo. However, we can use it to discuss the <code>flex-shrink</code> property, which is very handy in some cases.

<strong>Solution:</strong> Apply <code>display: flex</code> to the parent wrapper. You will notice that the text overlays the avatar image (or that the avatar image is very small, as in the image above). To overcome this, you can declare <code>flex-shrink: 0</code> on the image, which ensures that it will not shrink to accommodate the width of other flex items. The alternative is to apply the <code>flex: 1</code> shorthand to the comment text. In this case, you wouldn’t need <code>flex-shrink: 0</code> on the avatar. In general, the specification <a href="https://www.w3.org/TR/css-flexbox-1/#flex-components">recommends the flex shorthand method</a>, but it’s good to know about the <code>flex-shrink</code> standalone property as well.

<strong>Demo:</strong>

See the Pen [Comments module with flexbox](https://codepen.io/imohkay/pen/OPyPbo/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/OPyPbo/">Comments module with flexbox</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

## 5\. Complex Menus

<strong>Use case:</strong> My app has a menu that includes a search and sort widget. It’s a mix of buttons, inputs, icons and text.

<strong>Issue:</strong> I’m worried about the layout breaking across different screen sizes.

<strong>Discussion:</strong> This is a perfect use case for flexbox. We have some items with a fixed width (although we don’t need to declare these widths) and other items that need to fill up the rest of the screen’s width.

<strong>Solution:</strong> We can use flexbox to get vertical centering and a flexible search-and-sort module with relatively little code.

<strong>Demo</strong> (using Font Awesome via the CDN for convenience):

See the Pen [Flexbox demo: Search and filter](https://codepen.io/imohkay/pen/QwjwGP/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/QwjwGP/">Flexbox demo: Search and filter</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

## 6\. Cards

<strong>Use case:</strong> I’m creating a card module for my app, based on the card component in Google’s <a href="https://www.google.com/design/spec/components/cards.html">material design documentation</a>. The cards will stack on mobile.

<strong>Issue:</strong> On large screens, I want the cards to be inline. The height of cards in a <em>line</em> should be the same, although the markup won’t include rows that wrap sets of cards. The “See More” button should always be positioned at the bottom of the card.

<strong>Discussion:</strong> We can look at additional properties in the flexbox module, such as <code>margin: auto</code> to intelligently handle spacing.

<strong>Solution:</strong> Flexbox provides an incredible solution to a mammoth CSS issue: equal heights. In fact, flexbox is so flexible that it allows cards in a row to be of equal heights, even though there are no wrapper <em>row</em> divs around a set of cards. It also allows the “See More” buttons to appear as if they are absolutely positioned at the bottom of the card, using a nifty <code>margin: auto</code> trick.

<strong>Demo</strong> (using the <code>flex-wrap</code> property, which does not work in some older browsers):

See the Pen [Flexbox: Card module](https://codepen.io/imohkay/pen/PwPwWd/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

See the Pen <a href="https://codepen.io/imohkay/pen/PwPwWd/">Flexbox: Card module</a> by Karen Menezes (<a href="https://codepen.io/imohkay">@imohkay</a>) on <a href="https://codepen.io">CodePen</a>.</p>

## Conclusion

Flexbox could be the perfect fit for a hybrid web app whose target audience is on smartphones with the latest browsers. In fact, some popular front-end frameworks use flexbox, including ZURB’s <a href="https://foundation.zurb.com/apps/">Foundation for Apps</a> (see also <a href="https://github.com/zurb/foundation-apps">GitHub page</a>) and <a href="https://ionicframework.com">Ionic</a>.

If your app requires only modern browser support, welcome aboard! Using a tool like Autoprefixer eases the transition into the world of flexbox, with its multiple versions and syntax soup. While flexbox pairs well with floats, it can also replace it and do things that no other layouting model currently can, including inline blocks, table displays and absolute positioning. The “<a href="https://www.w3.org/TR/css-grid-1">CSS Grid Layout Module</a>” is intended to replace workarounds and hacks such as floats, but it’s at a nascent stage, with <a href="https://caniuse.com/#search=grid">poor browser support</a>. Some day in the future, I dare to dream that CSS grids and flexbox will be all we use to build intuitive user interfaces, because they play well together.

It takes a while to have your “Aha!” moment with flexbox, because it involves unlearning what you already know about CSS layouting. Once you speak the flexbox language fluently, your process of designing responsive apps will become effortless and your style sheets will get leaner.</p>

### Helpful Links and Resources

*   “[Flexbox](https://tympanus.net/codrops/css_reference/flexbox/),” Sara Soueidan, Codrops This useful CSS reference guide includes a comprehensive documentation on all things flexbox.
*   “[Designing CSS Layouts With Flexbox Is as Easy as Pie](https://www.smashingmagazine.com/2013/05/22/centering-elements-with-flexbox),” David Storey, Smashing Magazine This in-depth article provides great solutions using flexbox for real-world CSS problems. It includes tables that map the differences between the old and new specifications.
*   “[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox),” Chris Coyier This valuable article on CSS-Tricks lists the properties related to flex containers (i.e. parents) and flex items (i.e. children) side by side. It’s one of the best references for working on a layout that incorporates flexbox.
*   “[Flexbox Adventures](https://chriswrightdesign.com/experiments/flexbox-adventures),” Chris Wright This thorough article analyzes the `flex-grow` and `flex-shrink` properties, information that is hard to find online. Chris Wright provides helpful examples and has a cautionary view of flexbox, suggesting progressive enhancement for small UI components.
*   “[Are We Ready to Use Flexbox?](https://www.sitepoint.com/are-we-ready-to-use-flexbox),” Nick Salloum, SitePoint This beginner’s introduction to flexbox also covers possible solutions to the profusion of vendor prefixes for all versions of the syntax.
*   [Flexy Boxes](https://the-echoplex.net/flexyboxes) This “flexbox playground and code generator” covers all of the flexbox properties, with all versions of the syntax.
*   “[Flexbox Nav Bar With Fixed, Variable, and Take-Up-The-Rest Elements](https://css-tricks.com/flexbox-nav-bar-fixed-variable-take-rest-elements),” Chris Coyier This entire article is devoted to the traditional fixed-plus-fluid CSS layouting nightmare — in this case, for a navigation bar. It reiterates how flexbox trumps all other layouting methods.
*   “[Solved by flexbox](https://philipwalton.github.io/solved-by-flexbox),” Philip Walton Philip Walton makes a compelling case for using flexbox, with demos for grids, sticky footers, the media object and more.
*   “[Flexbugs](https://github.com/philipwalton/flexbugs),” Philip Walton Github repo by Philip Walton for cross browser flexbox bugs and workarounds
*   “[Using CSS Flexible Boxes](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Flexible_boxes),” Mozilla Developer Network This dives into the details while covering the edge cases and quirks of flexbox. You’ll find the so-called Holy Grail layout done in flexbox.
*   [The Ultimate Flexbox Cheat Sheet](https://www.sketchingwithcss.com/samplechapter/cheatsheet.html) Highly recommended, and written for humans.
*   “[A Visual Guide to CSS3 Flexbox Properties](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties),” Dimitar Stojanov As the name indicates, this flexbox guide provides a quick visual reference, eliminating the need for lengthy explanations. Equally useful for beginners as well as advanced users, who need a handy resource while building flexbox intensive layouts.

{{< signature "ds, il, al" >}}

<em>Front page image credits: "<a href="https://lincolnloop.com/blog/introducing-flexbox-fridays/">Introducing Flexbox Fridays</a>" by Joni Trythall.</em>

