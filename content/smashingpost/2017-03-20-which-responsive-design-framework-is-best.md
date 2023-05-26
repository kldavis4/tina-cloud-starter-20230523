---
title: 'Which Responsive Design Framework Is Best? Of Course, It Depends.'
slug: which-responsive-design-framework-is-best
image: >-
  https://www.smashingmagazine.com/general/2013/09/05/137741-revision-34/attachment/staples-lba-before-after-2/attachment/responsive-frameworks-opt2/
date: 2017-03-20T18:04:13.000Z
author: jen-kramer
description: >-
  In 2017, the question is not whether we should use a responsive design
  framework. Increasingly, we are using them. The question is which framework
  should we be using, and why, and whether we should use the whole framework or
  just parts of it.

  With dozens of responsive design frameworks available to download, many web
  developers appear to be unaware of any except for Bootstrap. Like most of web
  development, **responsive design frameworks are not one-size-fits-all**. Let's
  compare the latest versions of Bootstrap, Foundation and UIkit for their
  similarities and differences.
categories:
  - Mobile
  - Frameworks
  - Responsive Design
---
<figure><a href="https://www.smashingmagazine.com/2017/03/which-responsive-design-framework-is-best"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7670bf85-f317-4793-8714-94c37099af05/bootstrap-nav-500w-opt.png" width="500" height="140" alt="Responsive Framework" title="Which Responsive Design Framework Is Best? Of Course, It Depends." /></a></figure>

With dozens of responsive design frameworks available to download, many web developers appear to be unaware of any except for Bootstrap. Like most of web development, **responsive design frameworks are not one-size-fits-all**. Let's compare the latest versions of Bootstrap, Foundation and UIkit for their similarities and differences.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Creating A Complete Web App In Foundation For Apps](https://www.smashingmagazine.com/2015/04/creating-web-app-in-foundation-for-apps/)
*   [Diverse Test-Automation Frameworks For React Native Apps](https://www.smashingmagazine.com/2016/08/test-automation-frameworks-for-react-native-apps/)
*   [Hybrid Mobile Apps: Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)
*   [The Basics Of Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)

{{% feature-panel %}}

Three years ago, I wrote an article for Smashing Magazine, "[Responsive Design Frameworks: Just Because You Can, Should You?](https://www.smashingmagazine.com/2014/02/responsive-design-frameworks-just-because-you-can-should-you/)

Since that time, the industry has evolved at its typical breakneck pace. Sass, the CSS preprocessor, has become standard to most workflows. We're more accustomed to adjusting Sass variables to customize existing code. We confidently work with mixins, building our own styles. We've even got [Sass formulas for generating color schemes](https://tallys.github.io/color-theory/) that we can incorporate in our work.

Workflows themselves have become standard, making use of technologies such as Node.js, Bower, Grunt, Gulp, Git and more. Old browsers continue to fall away, allowing front-end developers to confidently use more features of HTML5 and CSS3, with fewer worries about significant cross-browser compatibility issues.

Revisiting the 131 comments on my 2014 article, I saw readers suggesting a number of approaches to making use of responsive design frameworks:

*   Some suggested using part of a framework with your own custom code.
*   Several developers plugged their own framework, either written from scratch or with code forked from another framework.
*   Several developers suggested frameworks that I did not cover, including Susy, Singularity, Breakpoint, UIkit, Pattern Lab, Toolkit, Pure, Cardinal, Skeleton, ResponsiveBP and many others.

All of these are legitimate approaches. Hundreds of frameworks are available. Many who have been in the business for some time have a favorite, whether it's an established framework or one they've created.

However, increasingly, I see students, clients and web development firms defaulting to Bootstrap as their starting point, often with little critical evaluation of whether it's an appropriate solution to the task at hand. Clients hire me for training in Bootstrap, for example, and then ask how they can add functionality that's native to Foundation. When I ask, "Why not use Foundation?," they tell me they've never heard of it and didn't know there are options beyond Bootstrap for responsive design.

There is no way I could review the dozens, if not hundreds, of responsive design frameworks. However, given that Bootstrap is the 500-pound gorilla of responsive design, I've chosen two other frameworks to evaluate compared to [Bootstrap](https://getbootstrap.com/): [Foundation](https://foundation.zurb.com/) and [GetUIkit](https://getuikit.com/). **I've chosen these three frameworks based on the characteristics they share**, in that they are full-service responsive design frameworks. They offer grid systems, SCSS with piles of variables and mixins for customizations, basic styling of nearly all HTML5 tags, prestyled components such as badges, labels and cards, and piles of JavaScript-based features such as dropdown menus, accordions, tabs, image galleries, image carousels and so much more. All three frameworks offer ways of reducing file sizes to just those styles and functionalities needed to work on a given website. They are all in active development.

Again, I am not suggesting that these are the only responsive design frameworks, nor am I implying that they are the best frameworks. These are, however, popular frameworks with piles of features out of the box, making them attractive to many development firms wanting to work with "Bootstrap or a close equivalent."

## Background Information

To start the discussion, let's examine some of the basic background features of each framework.</p>

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist"></th>
<th>Bootstrap 4</th>
<th>Foundation for Sites 6</th>
<th>UIkit 3</th>
</tr>
</thead>
<tbody>
<tr>
<th>Current version, release date</th>
<th>4.0.0-alpha 6, released January 2017</td>
<th>6.3.0, released January 2017</td>
<th>3.00 beta 9, released February 2017</td>
</tr>
<tr>
<th>Owned by</th>
<td>Originally developed at Twitter by Mark Otto and Jacob Thornton, now an open-source project</td>
<td>ZURB, a web development company in Campbell, California</td>
<td>YOOtheme, a WordPress and Joomla theme development company in Hamburg, Germany</td>
</tr>
<tr>
<th>Website</th>
<td><a href="https://v4-alpha.getbootstrap.com/">Bootstrap</a></td>
<td><a href="https://foundation.zurb.com/sites/docs/">Foundation</a></td>
<td><a href="https://getuikit.com/"GetUiKit</a></td>
</tr>
<tr>
<th>Standard distribution package includes</th>
<td>Required CSS (1 minified, 1 standard, both with <code>.map</code> files); required JavaScript (1 minified, 1 standard). Former theme is incorporated in Sass files, activated by variables. (Glyphicons are not distributed with Bootstrap 4.) Also contains two additional sets of CSS files (1 minified, 1 standard, both with <code>.map</code> files): bootstrap-grid, which appears to be a flexbox-based grid system, possibly redundant at this point; and bootstrap-reboot, based on normalize.css. A CDN is available for standard distribution files.</td>
<td><a href="https://foundation.zurb.com/sites/download/">Four distributions</a>: Complete, Essential, Custom, Sass. Complete version includes compiled CSS (minified and not), plus compiled JavaScript, including individual vendor files. Essential includes typography, grid, Reveal, and Interchange only. Custom can be customized on the website for downloading, and the developer can choose elements to include and change a few variables. The Sass version can only be downloaded using the command line, Foundation CLI or Yeti Launcher. A CDN is available for standard distribution files.</td>
<td>Distribution includes a single minified CSS file, a single minified JavaScript file and 26 SVG graphics. LESS, CSS, and JavaScript source files are available via Bower or npm. A CDN is available for standard distribution files.</td>
</tr>
<tr>
<th>Additional JavaScript libraries required?</th>
<td>Yes, you must download or link to a CDN separately: jQuery 3.1.1 Slim, Tether 1.4.0. Files are linked to just before end of <code>body</code> element.</td>
<td>All dependencies are bundled in the distribution. jQuery is required, but it is part of the distribution. Files are linked to just before end of <code>body</code> element.</td>
<td>All dependencies are bundled in the distribution. jQuery is required, but it is part of the distribution. Linking to files in the <code>head</code> is recommended.</td>
</tr>
<tr>
<th>Browser support</th>
<td>Latest versions of: Chrome (macOS, Windows, iOS and Android), Safari (macOS and iOS), Firefox (macOS, Windows, Android, iOS) (latest version of Firefox plus Extended Support Release), Edge (Windows, Windows 10 Mobile), Opera (macOS, Windows), Android Browser &amp; WebView 5.0+, Windows 10 Mobile, Internet Explorer 10+</td>
<td>Last two versions of Chrome, Firefox, Safari, Opera, mobile Safari, Internet Explorer mobile, as well as Internet Explorer 9+ and Android browser 2.3+</td>
<td>Latest versions of Chrome, Firefox, Opera, Edge, Safari 7.1+, Internet Explorer 10+, No mention of mobile-specific browsers</td>
</tr>
<tr>
<th>Internet Explorer support</th>
<td>Internet Explorer 10 and higher (Bootstrap 3 recommended for Internet Explorer 8 and 9)</td>
<td>Internet Explorer 9 and higher</td>
<td>Internet Explorer 10 and higher</td>
</tr>
<tr>
<th>Other browser support notes</th>
<td>"Unofficially, Bootstrap should look and behave well enough in Chromium and Chrome for Linux, Firefox for Linux, and Internet Explorer 9, though they are not officially supported." (<a href="https://v4-alpha.getbootstrap.com/getting-started/browsers-devices/">source</a>)</td>
<td>"JavaScript: Our plugins use a number of handy ECMAScript 5 features that aren't supported in IE8." (<a href="https://foundation.zurb.com/sites/docs/compatibility.html">source</a>)</td>
<td></td>
</tr>
<tr>
<th>License and copyright</th>
<td>Code and documentation copyright (2011 to 2017) of the Bootstrap authors and Twitter, Inc. Code released under the MIT License. Docs released under Creative Commons.</td>
<td>MIT license, no mention of copyright</td>
<td>MIT license, copyright of YOOtheme GmbH</td>
</tr>
<tr>
<th>Build tools</th>
<td>"Bootstrap uses Grunt for its CSS and JavaScript build system and Jekyll for the written documentation. Our Gruntfile includes convenient methods for working with the framework, including compiling code, running tests, and more." (<a href="https://v4-alpha.getbootstrap.com/getting-started/build-tools/">source</a>)</td>
<td><a href="https://foundation.zurb.com/sites/docs/installation.html">To access Sass files</a>, you must install using the command line, the Node.js-powered Foundation CLI, or with its Yeti Launch application (Mac only). "Foundation is available on npm, Bower, Meteor, and Composer. The package includes all of the source SCSS and JavaScript files, as well as compiled CSS and JavaScript, in uncompressed and compressed flavors." Other versions of Foundation are available as simple downloads without using these tools, but without SCSS files.</td>
<td>Bower and npm. Offer a SublimeText plugin and an Atom plugin for working with UIkit 3 as well.</td>
</tr>
</tbody>
</table>

In general, all three frameworks are in active development (all were updated in January or February 2017) and are mobile-first. All generally have some type of CSS preprocessor. UIkit version 3 beta currently only offers LESS. It will offer a SCSS port, as it's offered in previous versions of UIkit, in future releases.
<blockquote class="twitter-tweet"><br>
<p dir="ltr" lang="en"><a href="https://twitter.com/jen4web">@jen4web</a> Yes, we will have a SASS port too. (like we have in UIkit 2)</p>
— UIkit (@getuikit) <a href="https://twitter.com/getuikit/status/829680161968775168">February 9, 2017</a></blockquote>

Bootstrap transitioned from LESS to SCSS as part of its version 4 update. Foundation has always been written in SCSS, because ZURB is a Ruby on Rails shop, and Sass hails from the Ruby on Rails world.

There are notable differences with the build tools. Foundation is extremely picky about you using its workflow when working with the framework, if you wish to work with SCSS files. Unfortunately, Foundation offers few choices in tools. Bootstrap is much less picky about workflow, offering several options, including no workflow at all, even with its SCSS files. All frameworks offer at least one distribution ZIP file, containing all elements of the framework. Foundation offers a way to choose only certain elements in a download. Bootstrap 4 alpha and UIkit 3 beta do not offer this functionality currently, but they have previously offered this in older Bootstrap and UIkit versions. We can assume that once these frameworks reach their stable releases, this functionality will be offered as well.</p>

## Grid System

Each framework comes with a grid system, as one might expect. Bootstrap and Foundation's grid systems include multiple breakpoints, nested grids, offsets and source ordering (i.e. changing the order of content on collapse). Exact breakpoint values vary, but the breakpoints are generally customizable with SCSS. UIkit's grid is radically different and is described below.

With the most recent alpha 6 release, Bootstrap features a flexbox-based grid system by default. (This is partly the reason for its Internet Explorer 10+ browser support.) By default, Foundation features a floated grid system (which helps, in part, with its Internet Explorer 9+ support). Optionally in Foundation, you can compile a flexbox-based grid system by toggling an appropriate Sass variable and recompiling to CSS. Foundation notes that flexbox is not supported in Internet Explorer 9, so keep this in mind if this is a target browser for you.

Foundation offers a few more grid features than Bootstrap, including centered columns, incomplete rows, responsive gutters, semantic grid options and fluid rows.

Equal-height columns are a common problem when working with float-based grid systems. Foundation includes a JavaScript component named Equalizer. Because UIkit and Bootstrap are based on flexbox and not floats, equal-height columns are built into the grid system and are never an issue.

UIkit has a very different grid than Foundation and Bootstrap. Rather than a standard 12-column system, UIkit has broken its layouts into three components: grid, flex and width. <a href="https://getuikit.com/docs/grid#usage">Starting with the grid component</a>, you can create as many columns as you wish:

<blockquote>To create the grid container, add the <code>uk-grid</code> attribute to a <code>&lt;div&gt;</code> element. There's no need to add a class. Add child <code>&lt;div&gt;</code> elements to create the cells. By default, all grid cells are stacked. To place them side by side, add one of the classes from the Width component. Using <code>uk-child-width-expand</code> will automatically apply equal width to items, regardless of how many there are.</blockquote>

As implied in the documentation, grid sets up the boxes that might be next to each other in some layouts, while width determines the width of those boxes, and flex determines the layout within each box, using flexbox properties. Finally, unlike other grid systems, UIkit offers a border between grid columns.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48851798-ffed-4ad3-a0ff-acc2d33a37e1/foundation-grid-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48851798-ffed-4ad3-a0ff-acc2d33a37e1/foundation-grid-opt.png" alt="Foundation's equalizer demonstrated." width="800" height="260" /></a><figcaption>Foundation's equalizer is designed to create equal-height columns. (Image: <a href="https://foundation.zurb.com/sites/docs/equalizer.html">Foundation Docs</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48851798-ffed-4ad3-a0ff-acc2d33a37e1/foundation-grid-opt.png">View large version</a>)</figcaption></figure>

## CSS And Default Styling

All three frameworks come with some level of CSS styling. The styling can be changed through an overriding style sheet or by modifying the provided SCSS or LESS preprocessor files. Generally speaking, basic styling is provided for all, or nearly all, HTML5 elements. All frameworks provide some quantity of utility classes, generally used for printing, responsiveness and the visibility of elements. Foundation and UIkit offer right-to-left support for languages written in that direction. UIkit states that it will feature a RTL version and the option to compile UIkit with a custom prefix.</p>

<blockquote class="twitter-tweet"><br>
<a href="https://twitter.com/jen4web">@jen4web</a> Also a RTL version and the option to compile UIkit with a custom prefix (like ba- instead of uk-)

— UIkit (@getuikit) <a href="https://twitter.com/getuikit/status/829680541179985920">February 9, 2017</a></blockquote>

It is unclear from its documentation whether Bootstrap 4 is offering RTL support, but it has been available in previous versions. It seems like this might be part of a <a href="https://github.com/twbs/bootstrap/issues/19555">future stable release</a>. There is much interest in including this feature in the Bootstrap community.

The framework with the least out-of-the-box styling is Foundation. This framework has long assumed that its users are more advanced developers who will want to write their own styling for their projects. Therefore, ZURB has always provided less styling out of the box by design, meaning there will be fewer styles to override later.

UIkit offers two color options, accessible via the Inverse component. They include the standard scheme (light backgrounds and dark text) and a contrast scheme (dark backgrounds and light text). UIkit also offers some unique styled components, such as Articles and Comments, as well as Placeholder, which provides an empty space for drag-and-drop file-uploading interfaces. If you recall YOOtheme's WordPress and Joomla theming roots, these features make perfect sense. Neither Bootstrap nor Foundation includes this styling specific to content management systems, so this is a distinguishing characteristic of the framework.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/805187ba-a9c2-44e5-91ce-dbba0ec4a5fc/uikit-comment-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/805187ba-a9c2-44e5-91ce-dbba0ec4a5fc/uikit-comment-opt.png" alt="UIkit's comment styling." width="682" height="608" /></a><figcaption>UIkit offers comment styling out of the box, one of its unique styling features. (Image: <a href="https://getuikit.com/docs/comment#lists">UIkit Docs</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/805187ba-a9c2-44e5-91ce-dbba0ec4a5fc/uikit-comment-opt.png">View large version</a>)</figcaption></figure>

Bootstrap offers much more than Foundation. Indeed, Bootstrap's distinctive look has permeated websites for several years. Bootstrap 4 has a similar look to Bootstrap 3. Bootstrap still offers several colors, such as "warning," "danger," "primary," "info" and "success," and it typically offers a few variations on styling certain HTML elements, such as tables and forms.

It's also worth comparing the CSS units in each framework. Bootstrap 4 uses rem as its primary CSS unit throughout. However, it states, "pixels are still used for media queries and grid behavior as viewports are not affected by type size." Bootstrap also increased its base font size from 14 pixels in version 3 to 16 pixels in version 4.</p>

<a href="https://foundation.zurb.com/sites/docs/typography-base.html">Foundation says</a>, "We use the rem unit nearly everywhere in Foundation, and even wrote a Sass function to make it a little easier. The <code>rem-calc()</code> function can take one or more pixel values and convert them to proper rem values."

Finally, UIkit seems to use pixels as a primary size unit, although occasionally uses percentages and rems in a few places in its LESS files. Its CSS size philosophy is not addressed in its documentation.

## Navigation And Navigation Elements

All three frameworks ship with responsive navigation elements. All include some fairly common navigation components, like formatted breadcrumbs, tabs, accordions and pagination. There are minor variations between these, but they all typically work as expected.

All three frameworks ship with dropdown menus. In general, these dropdowns may be used in several scenarios: with standard responsive navbars, with tabs, with buttons, etc. All three include vertical dropdowns. Foundation and UIkit also include horizontal dropdowns, in which the dropdown is displayed as a row rather than a column.

Navigation bars are present in all three frameworks. Each navbar can accommodate website branding and search and can be made sticky, and elements can be aligned left or right in the bar. All navigation bars collapse, but they may present collapsed content differently (some via a hamburger button plus a dropdown, some via an off-canvas menu). The navigation bars also have a few differences among themselves.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b5fe32-8163-4127-98eb-af4ef32c1450/bootstrap-nav-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b5fe32-8163-4127-98eb-af4ef32c1450/bootstrap-nav-opt.png" alt="Bootstrap's nav demonstrated." width="724" height="202" /></a><figcaption>Bootstrap's iconic navigation bar now comes with easy color options by combining class names, or an inline color option. (Image: <a href="https://v4-alpha.getbootstrap.com/components/navbar/">Bootstrap Docs</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b5fe32-8163-4127-98eb-af4ef32c1450/bootstrap-nav-opt.png">View large version</a>)</figcaption></figure>

Bootstrap offers some basic horizontal and vertical navigation bars with different styling options (tabs, pills, stacked pills, justified or plain styling). It offers a separate horizontal responsive navigation bar, which creates a hamburger button on collapse. Two color schemes are available, with colors and breakpoints customizable through SCSS.

Foundation had a responsive navigation bar in previous versions similar to Bootstrap's. In version 6, it has turned several navigation bar treatments into individual elements that can be combined. For example, on collapse, the navigation may be hidden behind a hamburger button, behind an off-canvas treatment or behind a drilldown menu, in which the user loads screens of menu items. These types of navigation treatment may be changed at specific screen sizes. For example, the full navigation bar may be available at desktop dimensions but switch to a drilldown for mobile.

UIkit's bar offers functionality similar to Bootstrap's. By default, it does not have a built-in toggle, but this is easily added with the appropriate CSS classes and JavaScript. Collapsed content is typically behind a hamburger button, and it may be coupled with off-canvas functionality. UIkit also specifically offers an icon-based navigation bar (iconbar). It ships with 26 SVG icons, which can be integrated in this bar, with the promise of more icons in the future.</p>

## JavaScript Components

All three frameworks depend on jQuery for their JavaScript-based components. Foundation and UIkit ship with a copy of jQuery, while Bootstrap relies on connecting to jQuery via a CDN or a download.

All three frameworks contain similar types of functionality: tooltips, modal windows, accordions, tabs, dropdown menus, image carousels, etc.

Foundation has two handy components that set it apart. One is Abide, a full-featured HTML5 form-validation library. It can handle client-side error-checking of forms. The other is Interchange, a JavaScript-based responsive image loader. It's compatible with images and with bits of HTML and text. It loads the appropriate content on the page based on media queries. Despite the fact that one of the defining characteristics of responsive design is images that resize, neither Bootstrap nor UIkit offers similar functionality.

UIkit combines its styles and JavaScript components in its documentation, calling it all "components." Some of the unique JavaScript-based components currently available in its beta release include Scroll, which allows smooth scrolling to other parts of the web page, and Sortable, which enables drag-and-drop grids on the page.</p>

<a href="https://yootheme.com/blog/2017/01/09/uikit-3-beta-released">In future versions of UIkit</a>, we are promised many components from UIkit 2, including "Slideshow, Slider, Slideset, Parallax, Nestable, Lightbox, Dynamic Grid, HTML editor, Date- and Timepicker components." It's worth highlighting HTML Editor, and the Date- and Timepicker components, because these are typically used in administrative interfaces and in applications. Remember that YOOtheme creates Joomla and WordPress themes as part of its business, so these are important components for it. Neither Foundation nor Bootstrap includes these admin-friendly widgets, so this is a distinguishing characteristic of this framework.

One of UIkit's most <a href="https://getuikit.com/docs/javascript#uikit-and-reactive-javascript-frameworks">distinguishing JavaScript features</a>, however, is this:
<blockquote>UIkit is listening for DOM manipulations and will automatically initialize, connect and disconnect components as they are inserted or removed from the DOM. That way it can easily be used with JavaScript frameworks like Vue.js and React.</blockquote>

## So, Which Is Best?

It depends! All three projects are actively maintained and have devoted followers. In the end, the right framework for you will depend on your project's requirements, where you need help in programming (making it pretty? coding functionality?) and your personal coding philosophy (rems versus pixels? LESS versus Sass?). As with all technology, there is no perfect choice, and you will have to make compromises on features, functionality and code styles.

With this in mind, here are some points to weigh in making your decision.

*   **Browser support**.  The framework versions reviewed here support similar browsers. However, going back one framework version, or following the instructions for incorporating polyfills, might increase support for important browsers. In particular, if you need Internet Explorer 8 support, you might want to look at Bootstrap 3.
*   **CSS unit differences**.  Foundation keeps nearly all of its units in ems and rems. Bootstrap uses mostly ems and rems, with pixels for media queries. UIkit uses mostly pixel measurements. Some developers have strong opinions about these approaches and might choose a framework based on them.
*   **Quantity of styling**.  UIkit has a lot of out-of-the box styling. Foundation has much less. Bootstrap is somewhere in between. How much styling do you need to override? How much styling do you want to be present already? Do you want to write very little or none?
*   **CSS preprocessors**.  Foundation was written in SCSS natively. Bootstrap had a port from LESS to SCSS in version 3, then rewrote its SCSS in version 4\. UIkit continues to work in LESS while in beta, but it will offer a SCSS port in future releases. This could also affect your choice of framework.
*   **Workflow**.  If you wish to modify SCSS files, know that Foundation will lock you into a fairly rigid workflow. Bootstrap and UIkit offer a workflow, but you can choose a different workflow or no workflow at all.
*   **JavaScript components**.  Foundation offers form validation and responsive content management. UIkit is specifically built to work with reactive JavaScript frameworks, and it includes components for building an admin interface. Depending on the components you require, this could sway your decision.
*   **Grid differences**.  Bootstrap and Foundation offer 12-column grids. UIkit offers a very different approach to grid layout, with very different styling. Foundation's grid can easily be modified to greater or fewer columns with SCSS, and it can be made semantic as well. Grids for UIkit and Bootstrap are flexbox-based by default, while Foundation's are float-based, but convertible to flexbox through SCSS.

{{< signature "da, al, il" >}}

