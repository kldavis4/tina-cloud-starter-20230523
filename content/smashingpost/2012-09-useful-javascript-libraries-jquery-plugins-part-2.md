---
title: Useful JavaScript Libraries and jQuery Plugins — Part 2
slug: useful-javascript-libraries-jquery-plugins-part-2
image: null
date: 2012-09-26T15:49:12.000Z
author: vitaly-friedman
description: ''
categories:
  - JavaScript
  - jQuery
---

If you have a problem and need a solution for it, chances are high that a JavaScript library or jQuery plugin exists that was created to solve this very problem. Such libraries are always great to have in your bookmarks or in your local folders, especially if you aren't a big fan of cross-browser debugging.

In this overview, we feature <strong>some of the recent useful JavaScript and jQuery libraries</strong> which could be just the right solutions for your common problems. You might know some of these libraries, but you probably don’t know most of them. In either case, we hope that this overview will help you find or rediscover some tools that you could use in your next projects.

Due to the length of this post, we've split it into two parts for your convenience:

*   [Part 1: Web Forms, Typography, Time-Savers and Images](https://www.smashingmagazine.com/2012/09/23/useful-javascript-libraries-jquery-plugins-web-developers/)
*   **Part 2: Text, Tables, List and Useful Development Tools**

#### Quick Overview:

Below you'll find a brief overview and links to the libraries and tools featured in this post.

*   **Text Manipulation:** [syntax highlighter](https://prismjs.com/) - URI.js - [jQuery URL parser](https://github.com/tombonner/jurlp) - [cutting paragraphs](https://github.com/tcorral/Cutter.js) - [text truncation](https://github.com/rviscomi/trunk8) - [TOC generator](https://projects.jga.me/toc/) - [FAQ generator](https://johnpolacek.github.com/MagicNav.js/) - [sorting text by relevancy](https://github.com/padolsey/relevancy.js).
*   **Manipulating Tables and Lists:** [table styling](https://tableclothjs.com/) - [searchable/sortable lists](https://listjs.com/) - [visual search](https://documentcloud.github.com/visualsearch/) - [nested sortable lists](https://farhadi.ir/projects/html5sortable/) - [large data sets](https://square.github.com/crossfilter/) - [CSV to table conversion](https://code.google.com/p/jquerycsvtotable/) (or [Csonv.js](https://archan937.github.com/csonv.js/)) - Excel-like tables - [advanced tables](https://datatables.net/)
*   **Useful JavaScript Tools for Web Development:** [Yeoman](https://yeoman.io/) - [command line for JS](https://gruntjs.com/) - [image placeholder](https://imsky.github.com/holder/) - [percentage loader](https://widgets.better2web.com/loader/) - [URL parser](https://github.com/tombonner/jurlp) - URI normalization - [touch events](https://github.com/jairajs89/Touchy.js) - [multi-touch gestures](https://eightmedia.github.com/hammer.js/) - [Markdown Embedding](https://strapdownjs.com/) - [accessibility enhancement](https://github.com/yatil/accessifyhtml5.js) - [templating engine](https://twitter.github.com/hogan.js/) - [filepicker](https://www.filepicker.io/) - [extensible regex](https://xregexp.com/) - [client-side caching](https://github.com/d0ugal/locache)

### Text Manipulation Libraries

<a href="https://prismjs.com/">Prism</a>
A lightweight and extensible syntax highlighter. There are no Prism-specific markup or class names, you can use the standard markup. Prism supports parallelism with Web workers, if available. All styling is done through CSS, with sensible class names like <code>.comment</code>, <code>.string</code>, <code>.property</code> etc. The overall core core size is only 1.5Kb (minified and gzipped).

<figure><a href="https://prismjs.com/"><img title="Prism" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e17ddbb-78d3-41bf-81f5-6d9e098aa7ed/prism.gif" alt="Prism" width="500" height="316" /></a></figure>

<a href="https://projects.jga.me/toc/">TOC jQuery Plugin: Generate Tables Of Contents</a>
This library automatically generates and guides the user through a table of contents on a page. It's customizable and is able to automatically highlight a current section of the document. The plugin is also very lightweight, can be used multiple times on a page, and even includes a smooth scrolling functionality for the correct section. The plugin is developed by Greg Allen and is currently available in beta. You might want to check out <a href="https://gregfranko.com/jquery.tocify.js/">Tocify jQuery plugin</a> as well.

<figure><a href="https://projects.jga.me/toc/"><img loading="lazy" decoding="async" class="121584" title="JavaScript Library" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5fea030-b802-429c-9c5b-08f414969789/toc.gif" alt="JavaScript Library" width="500" height="282" /></a></figure>

<a href="https://johnpolacek.github.com/MagicNav.js/">MagicNav: Generates Links for The FAQ</a>
If you want to create a quick navigation for your FAQ page, you can use this jQuery plugin for generating navigation links dynamically from page elements.

<a href="https://github.com/tcorral/Cutter.js">Cutter.js</a>
This library solves the problem when cutting content by a number of words is required but you don't want to change the markup. It simply cuts the content to the required length, while allowing the user to see the full content again.

<a href="https://github.com/rviscomi/trunk8">Trunk8</a>
Trunk8 is a text truncation jQuery plugin that cuts off just enough text from a large block of text to prevent it from spilling over. While conventional truncation just limits the character length, this library is able to measure the content area for spill-over and chooses the text that best fits into a given space.

<a href="https://github.com/padolsey/relevancy.js">Relevancy.js</a>
This library allows you to sort an array of items based on their relevancy. This script is attempting to implement basic partial matching which so far has not been successfully implemented. It assigns strings to their respective elements.

### Manipulating Tables and Lists

Handsontables: Excel-Like Tables For The Web
This jQuery library allows you to use auto-expanding and auto-complete as well as add new rows and columns. It also includes a legend, scrolling (so as your table grows, it won't take up your entire page and become unwieldy), context menus, conditional formatting and other features. You can even set it to track changes made to the table. And, all the data you enter in Handsontable can be copied and pasted to Excel, Google Spreadsheet, or LibreOffice.

<figure><img loading="lazy" decoding="async" class="121575" title="nl-3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a90cb865-0016-4ba6-a429-1d32fb9ef588/handsontable.jpg" alt="JavaScript Library" width="500" height="273" /></figure>

<a href="https://listjs.com/">List.js</a>
A cross-browser native JavaScript library that transforms HTML lists into flexible content that you can easily edit. It makes your list easily searchable and sortable. A template-driven concept lets you simply add and edit items.

<figure><a href="https://listjs.com/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147883b7-d757-40d1-92c4-a2fab397a289/listjs.jpg" alt="List.js" width="500" height="331" /></a></figure>

<a href="https://farhadi.ir/projects/html5sortable/">Create Nested Sortable Lists With jQuery</a>
This plugin lets you create a sortable list where your users can drag and drop list items into any configuration they choose. You can set various attributes, such as the maximum number of nested levels, as well as setting custom methods (including To hierarchy, To array, and Serialize). As an alternative, there's also the <a href="https://farhadi.ir/projects/html5sortable/">HTML5 Sortable</a> plugin, which uses HTML5 and jQuery for a similar functionality.

<figure><a href="https://farhadi.ir/projects/html5sortable/"><img loading="lazy" decoding="async" class="121573" title="nl-1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f60faba-409e-46a4-a34c-130fe04d2052/html5sortable.jpg" alt="JavaScript Library" width="500" height="324" /></a></figure>

Pivot.js
With Pivot you can easily summarize large data sets on the fly. The library lets you create customizable table views from your browser. The results of pivot-table tools (which automatically sort, count, total or give the average) will be displayed as an HTML table pivoting from the input data (CSV or JSON).

<figure><img title="Pivot.js" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a2e25e-d995-46f0-99dd-c25f6c486990/pivotjs.jpg" alt="Pivot.js" width="500" height="313" /></figure>

<a href="https://square.github.com/crossfilter/">Crossfilter</a>
Crossfilter is a JavaScript library which supports exploring large multivariate datasets in the browser. It enables fast (&lt;30ms) interaction with coordinated views, even with large data sets containing more than a million records. It was built to power analytics for Square Register and allows merchants to slice and dice their payment history fluidly. By using sorted indexes, the library speeds up incremental filtering and thereby increases the performance of live histograms and top-K lists.

<figure><a href="https://square.github.com/crossfilter/"><img title="Crossfilter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08d143bd-af81-40c8-8e86-4b9a76aed7bd/crossfilter.jpg" alt="Crossfilter" width="500" height="348" /></a></figure>

<a href="https://code.google.com/p/jquerycsvtotable/">jQuery CSV to Table</a>
This library reads in comma separated values (CSV) or tab separated values (TSV) data and generates an HTML table.

<a href="https://code.google.com/p/jquerycsvtotable/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fb68f84-760c-4ff2-97ef-be2a94984ed1/csvtable.png" alt="jQuery CSV to Table" width="498" height="313" /></a>

<a href="https://archan937.github.com/csonv.js/">Csonv.js</a>
Paul Engel has released a tiny library to fetch relational CSV data client-side (JSON). When using CSV, one file represents one entity; the librarycan also nest relational data within the resulting objects as if you are joining SQL tables.

<a href="https://datatables.net/">DataTables jQuery Plug-in</a>
The library can display data from different sources, be it DOM, a JavaScript array, or a server-side file with JSON formatting. Among other features, the library provides pagination, on-the-fly filtering, and multi-column sorting with data type detection. And the features that DataTables provides can be enhanced by many freely available plug-ins: e.g. with row grouping, column filtering, column resizer, etc. The library weighs 68Kb minified, and 20Kb gzip'd. Open source, and released under GPL and BSD.

<figure><a href="https://datatables.net/"><img loading="lazy" decoding="async" class="121585" title="nl-11" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67298bbc-955d-46d1-b4b7-bbcf67c526d7/datatables.jpg" alt="JavaScript Library" width="500" height="299" /></a></figure>

### Useful JavaScript Tools for Web Development

<a href="https://yeoman.io">Yeoman</a>
Yeoman is a set of tools and libraries that helps to scaffold new projects, automatically compiles CoffeeScript &amp; Compass, runs yours scripts against jshint for proper language coverage and optimizes all your images. It effectively uses plugins like NodeJS, Compass, Grunt and PhantomJS and actually requires the installation of Node 0.8.x.

<a href="https://yeoman.io"><img title="Yeoman" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed15e0df-ee3c-4260-821b-a1fe58c40751/yeoman.png" alt="JavaScript Library" width="500" height="548" /></a>

<a href="https://gruntjs.com/">Grunt.js: Task-Based Command Line Tool</a>
Grunt is a task-based command line build tool for JavaScript projects. It has a dozen of predefined tasks built-in already: file concatenation, project scaffolding from a predefined template, validation with JSHint, minifcation with UglifyJS, qUnit tests, server start, running unit tests with nodeunit and running watched files.

<figure><a href="https://gruntjs.com/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12c9eb9a-2db1-463b-a657-cca0e87f775e/grunt-cmd1.jpg" alt="Grunt.js: Task-Based Command Line Tool" width="500" height="277" /></a></figure>

<a href="https://imsky.github.com/holder/">Holder.js</a>
A client-side image placeholder library to render placeholders entirely in browser. It works both online and offline, and offers a chainable API to style and create placeholders with ease. You can use Holder in different areas on different images with custom themes. Since it extends its default settings with the settings you provide, you only have to include those settings which you want changed.

<figure><a href="https://imsky.github.com/holder/"><img title="Holder.js" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/116bce54-084a-4baa-b047-5f8832860a47/js-libraries-107.jpg" alt="Holder.js" width="500" height="300" /></a></figure>

<a href="https://thinkpixellab.com/pxloader/">PxLoader</a>
A JavaScript library that makes it easier to download images, sound files or any other file needed before taking an action on your website. The script lets you set up a preloader for HTML5 games and websites. You can monitor download status and even prioritize downloads in tagged groups.

<figure><a href="https://thinkpixellab.com/pxloader/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b06de15-b694-42d8-acee-3ee37bfd71b6/js-01-110.jpg" alt="PxLoader" width="500" /></a></figure>

<a href="https://widgets.better2web.com/loader/">Percentage Loader</a>
With this jQuery plugin the common horizontal progress bar is displayed differently. The script uses HTML5 canvas and data URI encoding (vector graphics) to allow for visually appealing and variably sizable graphics. Also, it can be used to display feedback during long-running tasks.

<figure><a href="https://widgets.better2web.com/loader/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69aab9f7-b5cf-4918-8aae-c4894e13e39c/percentage-loader1.jpg" alt="Percentage Loader" width="500" height="279" /></a></figure>

<a href="https://github.com/23/resumable.js">Resumable.js</a>
The library is designed to introduce fault-tolerance into the upload of large files through HTTP. It thus provides multiple, simultaneous and resumable uploads through the HTML5 File API. That means, losing the networks connection doesn't require a completely new upload. Users can also manage their uploads without loss of data. However, due to the reliance on the HTML5 File API, support is currently limited to Firefox 4+ and Chrome 11+.

<a href="https://github.com/balupton/History.js/">History.js</a>
The library gracefully supports the HTML5 History/State APIs (<code>pushState</code>, <code>replaceState</code>, <code>onPopState</code>) in all browsers. Including continued support for data, titles, replaceState. Supports jQuery, MooTools and Prototype. You can modify the URL directly, without needing to use hashes.

<a href="https://github.com/tombonner/jurlp">Jurlp</a>
Jurlp is a jQuery URL parser plugin for parsing, manipulating, filtering and monitoring URLs in <code>href</code> and <code>src</code> attributes within arbitrary elements, as well as creating anchor elements from URLs found in HTML or text.

<figure><a href="https://github.com/tombonner/jurlp"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/641c2276-957c-4898-89c3-45b05b147614/js-01-126.jpg" alt="Jurlp" width="500" /></a></figure>

URI.js
To work with URLs you could use this JavaScript library, that offers a jQuery-like API. URI.js offers simple, yet powerful ways of working with query string, has a number of URI-normalization functions and converts relative/absolute paths.

<a href="https://github.com/jairajs89/Touchy.js">Touchy.js</a>
A JavaScript library which handles touch events without any dependencies. It's an easy way to assign hand functionality for touchscreen devices to your website. You might want to check out <a href="https://eightmedia.github.com/hammer.js/">Hammer.js</a> as well.

<figure><a href="https://github.com/jairajs89/Touchy.js"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/843930ee-f78c-4900-985d-5d95d48e957f/js-01-105.jpg" alt="Touchy.js" width="500" /></a></figure>

<a href="https://gridster.net/">gridster.js</a>
A jQuery plugin that allows building intuitive draggable layouts from elements spanning multiple columns. You can even dynamically add and remove elements from the grid. It is on par with sliced bread, or possibly better. MIT licensed.

<figure><a href="https://gridster.net/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86618a35-6dfd-4b50-b7d2-3d8d781e2a17/gridster.png" alt="gridster.js" width="498" height="335" /></a></figure>

<a href="https://yconst.com/web/freetile/">Freetile</a>
A jQuery plugin that enables you to organize the page content in a dynamic and responsive layout. Once applied to a container element, it attempts to arrange its children in a layout that makes optimal use of screen space, by "packing" them in a tight arrangement.

<figure><a href="https://yconst.com/web/freetile/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42593508-3569-40fc-9efa-10d5d796478d/arrangement.png" alt="Freetile.js" width="498" height="298" /></a></figure>

<a href="https://strapdownjs.com">Strapdown.js</a>
This tool makes it easy for you to embed a Markdown editor into your page. No server-side compilation required. The tool is cross-browser-compatible and has Github-style syntax highlighting.

<a href="https://strapdownjs.com"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8cee677-bd16-4ad1-ab01-441912d4db76/strapdown.png" alt="Strapdown.js" width="500" height="331" /></a>

<a href="https://github.com/yatil/accessifyhtml5.js">accessifyhtml5.js</a>
Eric Eggert has released a practical polyfill to make HTML5 more accessible. Most modern browsers work fine with HTML5's new semantic elements, however, they often lack the ARIA accessibility attributes that the specification demands. This small script adds those attributes to enhance accessibility of web sites.

<figure><a href="https://github.com/yatil/accessifyhtml5.js"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62de9a30-8a5e-413f-805c-9adabf8ae43d/js-01-107.jpg" alt="accessifyhtml5.js" width="500" /></a></figure>

<a href="https://jquerypp.com/">jQuery++</a>
An MIT-licensed collection of useful DOM helpers such as jQuery.cookie, jQuery.formParams, jQuery.within and special events for jQuery 1.7 that provide low-level utilities for features that jQuery doesn’t support. You can download a variety of plugins you might wish to use and disregard the rest.

<figure><a href="https://jquerypp.com/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5066e19f-4d33-4541-acbb-105b80d00aa2/js-01-117.jpg" alt="jQuery++" width="500" /></a></figure>

<a href="https://twitter.github.com/hogan.js/">Hogan.js</a>
Twitter's templating engine that lets you precompile your templates ahead of time for vanilla JavaScript. This engine was developed with Mustache test suite compatibility and performance in mind.

<a href="https://zeptojs.com/">Zepto.js</a>
Zepto is a lightweight JavaScript library with a largely jQuery-compatible API. The main purpose of the library is to cover the most important jQuery functions yet have a relatively small modular library that loads and executes fast, with a familiar and versatile API. If you use jQuery, you already know how to use Zepto. You might want to check <a href="https://minijs.com/">Mini.js</a> and <a href="https://createjs.com/#!/CreateJS">CreateJS</a> as well if you are looking for simple and lightweight JavaScript libraries to perform very specific tasks.

<figure><a href="https://zeptojs.com/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4594edc-2226-4eb7-8ece-be95a246f72b/zeptojs.gif" alt="Zepto.js" width="500" height="301" /></a></figure>

<a href="https://cssrefresh.frebsite.nl/">CSSrefresh</a>
A useful small script file that immediately implements changes on your browser made to your CSS-files, by surveying the CSS files in your Web page. Saved CSS-files are executed right away.

<figure><a href="https://cssrefresh.frebsite.nl/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f9115b7-f1f7-4f74-9352-e918b28a95f7/js-01-102.jpg" alt="CSSrefresh" width="500" /></a></figure>

<a href="https://badassjs.com/post/1217357060/hasjs">Has.js</a>
Instead of browser sniffing and feature inference, this library provides a collection of self-contained tests and a unified framework using pure feature detection for whatever library consumes it. Make sure to <a href="https://www.netmagazine.com/features/essential-javascript-top-five-script-loaders">consider other alternatives</a>, too.

<a href="https://www.filepicker.io">Filepicker.io</a>
An advanced solution for uploading files to the server as well as conversion, synchronization and integration of file uploads with services such as Facebook, Dropbox etc. A free plan is available.

<figure><a href="https://www.filepicker.io"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51e1d44a-2010-4ded-b4c2-e1a8584ce60f/filepicker-io.gif" alt="Filepicker.io" width="493" height="269" /></a></figure>

<a href="https://xregexp.com/">XRegExp</a>
An open source MIT licensed JavaScript library, XRegExp provides augmented, extensible regular expressions. The library provides a new syntax, flags, and methods beyond what browsers support natively. Also, take a look at <a href="https://github.com/natefaubion/matches.js">Matches.js</a>, an advanced pattern matching library for JavaScript.

<figure><a href="https://xregexp.com/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b774c847-9702-4450-ac6a-68d13b6d2449/js-01-128.jpg" alt="XRegExp" width="500" /></a></figure>

<a href="https://demo.tutorialzine.com/2012/07/framewarp-jquery-plugin/">FrameWarp</a>
This library helps you to show pages on your site with a CSS-driven transition effect. It has a helper function which compares the URL of the iframe with the address of the current page. If both the domain and the protocol match, Framewarp will try to access the DOM of the iframe and add the APU methods – one for hiding it, and another one for sending a message to the parent.

<a href="https://ericbidelman.tumblr.com/post/14866798359/introducing-filer-js">Filer.js</a>
Eric Bidelman released a wrapper library for the HTML5 Filesystem API. Filer.js reuses familiar UNIX commands and makes the HTML5 API more approachable for developers that have done file I/O in other languages. Repetitive operations (renaming, moving, duplicating) are easier to manage. You might want to check out <a href="https://gregfranko.com/DownloadBuilder.js/">DownloadBuilder.js</a>, a library that supports concatenation of local files and uses session storage to cache Ajax/JSONP requests.

<figure><a href="https://ericbidelman.tumblr.com/post/14866798359/introducing-filer-js"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6e5cab-7cbd-4c07-b835-16545a415173/js-01-120.jpg" alt="Filer.js" width="500" /></a></figure>

<a href="https://github.com/d0ugal/locache">Client Side Caching For JavaScript</a>
Server caching is useful for quick response times, but sometimes, especially when you are developing a Web application, you migh need to cache objects client-side rather than server-side. Maybe you need to cache something for offline use, or for reuse later. That's where <a href="https://github.com/d0ugal/locache">locache.js</a> comes in. It's a JavaScript caching framework for client side caching in the browser using HTML5 local storage. The library has a memcache-similar API, no dependencies and is very small. And the best part: locache gracefully degrades when the browser doesn't support local storage. So users with IE6 and IE7 will not get any errors, but as developers say, "caching attempts will be silently dropped and lookups will always appear to be a cache miss." You can provide an expiration time for cached objects as well.

<figure><a href="https://github.com/d0ugal/locache"><img loading="lazy" decoding="async" class="121581" title="nl-7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd935f41-5a14-40bf-8c08-fc7dc3c42d2d/nl-7.jpg" alt="JavaScript Library" width="500" height="300" /></a></figure>

### Last Click

<a href="https://responsiveviewport.com/">ReView.js</a>
This library provides a responsive Web design viewing choice. Users can either "opt-in" or "opt-out" of responsive design states and keep the persistent view preference for each session. Developed in pure JavaScript according to the principles of core (mobile-) first progressive enhancement. You might want to check FlexiNavCalc as well, a responsive navigation library that calculates navigation item widths in percentages to ensure that the navigation holds the layout until a break-point is executed.

<figure><a href="https://responsiveviewport.com/"><img loading="lazy" decoding="async" class="121578" title="JavaScript library" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08ecbc99-c0ab-41b4-abc8-70a9591b15f8/review-js.gif" alt="JavaScript Library" width="500" height="207" /></a></figure>

<a href="https://www.pockethotline.com">A Hotline For All Your JavaScript Problems</a>
Do you feel like giving up? Nothing makes sense anymore? Your problems seem insurmountable? Wouldn't it be great if you could talk to someone who cares and knows your woes? Why don't you give the friendly, supporting folk at JS Hotline a call when your JavaScript wisdom is at an end? Garann Means created JS Hotline as a helpline for people who are stuck with a JavaScript problem. This call-service powered by <a href="https://www.pockethotline.com">Pocket Hotline</a> promises professional help to people who need advice concerning JavaScript. They'll talk you off the ledge when you just can't make it work. And it won't cost you anything but a smile.

<figure><a href="https://www.pockethotline.com"><img loading="lazy" decoding="async" class="121578" title="JavaScript library" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec421b7e-89cb-416f-9307-8de1a4fa9238/nl-5.jpg" alt="JavaScript Library" width="500" height="300" /></a></figure>

### Useful JavaScript and jQuery Libraries

Due to the length of this post, we've split it into two parts for your convenience:

*   [Part 1: Web Forms, Typography, Time-Savers and Images](https://www.smashingmagazine.com/2012/09/23/useful-javascript-libraries-jquery-plugins-web-developers/)
*   **Part 2: Text, Tables, List and Useful Development Tools**