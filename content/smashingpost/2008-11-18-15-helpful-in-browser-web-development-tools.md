---
title: 15 Helpful In-Browser Web Development Tools
slug: 15-helpful-in-browser-web-development-tools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c150141-1c00-45ad-b235-1ded9954984b/debug.jpg
date: 2008-11-18T22:00:43.000Z
author: jacob-gube
description: >-
  There are many useful Web development tools that integrate in your browser.
  These in-browser tools are commonly known as _add-ons_ or _extensions_. Though
  add-ons and extensions aren't _just_ for Web development, many of them out
  there are designed specifically for Web developers. In-browser tools vary
  greatly in the jobs they perform; for example, some of them help you diagnose
  issues with CSS, HTML and JavaScript, while others evaluate the accessibility
  of your website.
categories:
  - Tools
  - Design
  - Web Design
  - Browsers
  - Development
  - Open Source
  - Plugins
---
There are many useful Web development tools that integrate in your browser. These in-browser tools are commonly known as <em>add-ons</em> or <em>extensions</em>. Though add-ons and extensions aren't <em>just</em> for Web development, many of them out there are designed specifically for Web developers. In-browser tools vary greatly in the jobs they perform; for example, some of them help you diagnose issues with CSS, HTML and JavaScript, while others evaluate the accessibility of your website.

In this article, we explore some of <strong>the most popular and useful in-browser Web development tools</strong>. You'll find tools for popular Web browsers like Firefox and Internet Explorer. Whether you need to debug and inspect your HTML, inspect HTTP headers, access FTP source files, evaluate accessibility or just figure out what color a Web page element is, you may find a variety of tools discussed here useful. 

You might be interested in the following related posts:

*   [40+ Desert Island Web Development Tools](https://www.smashingmagazine.com/2009/09/40-desert-island-web-development-tools/)
*   [Useful Coding Tools and JavaScript Libraries For Web Developers](https://www.smashingmagazine.com/2011/10/useful-coding-workflow-tools-for-web-designers-developers/)
*   [Next-Generation Responsive Web Design Tools: Webflow, Edge Reflow, Macaw](https://www.smashingmagazine.com/2014/05/next-generation-responsive-web-design-tools-webflow-edge-reflow-macaw/)

## Firebug

<a href="https://getfirebug.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a627cb3-dd44-4603-b844-43cd9a3ba17a/01-firebug.jpg" alt="Firebug - screen shot." width="480" height="300" /></a>

{{% feature-panel %}}

<a href="https://getfirebug.com/">Firebug</a> is an extension for the Mozilla Firefox browser that allows you to debug and inspect HTML, CSS, the Document Object Model (DOM) and JavaScript. Though it has many strong features, it's most known for revolutionizing the way developers debug and profile JavaScript code.

For example, before Firebug, many developers would use the <em>alert()</em> function to see what a variable contains or to find what line the code breaks. With Firebug enabled, you're told specifically what the error is and which line it comes from. Firebug is an excellent tool for AJAX application developers because it lets you explore and perform on-the-fly edits on the DOM to see what happens when you manipulate Web page elements after a user action.

Aside from its popular JavaScript and DOM functionalities, Firebug can also log network activity to allow you to see detailed results of HTTP connections, inspect and edit HTML on the fly and debug and visualize your CSS.

<strong>Further Reading</strong>

*   [Debug and tune applications on the fly with Firebug](https://www.ibm.com/developerworks/web/library/wa-aj-firebug/)

## Web Developer

<a href="https://chrispederick.com/work/web-developer/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1429a6a6-c0c4-4b28-aeb6-4fc65498fdc8/02-web-developer-toolbar.jpg" alt="Web Developer - screen shot." width="480" height="300" /></a>

The <a href="https://chrispederick.com/work/web-developer/">Web Developer</a> extension (for the Firefox, Flock and SeaMonkey Web browsers) is an add-on that adds a tool bar with a menu of options for debugging and inspecting Web pages. It has a ton of features, my favorite being the <em>View CSS Information</em> option (CSS &gt;&gt; View Style Information, or <em> Control</em> + <em>Shift</em> + <em>Y</em> on Windows) which makes a page element clickable and shows you CSS selectors that affect that particular page element. It's helpful for exploring and understanding large CSS files and projects that you're unfamiliar with (such as a new open-source content management system).

It has built-in options for syntax validation for popular Web services, such as <a href="https://jigsaw.w3.org/css-validator/">W3C's CSS Validator</a> and <a href="https://www.cynthiasays.com/">HiSoftware's Web Content Accessibility Report</a>, for your convenience. It has many other useful features, such as disable options for CSS, JavaScript and images, to test for degradation and progressive enhancement; a <em>Forms</em> menu with options for working with Web forms; <em>Display Div Order</em> and <em>Display Block Size</em> options to help you visualize the layout; and <em>so much more</em>.</p>

## YSlow

<a href="https://developer.yahoo.com/yslow/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fbb98c3-8b46-45bd-a998-7dd905ad87f7/03-yslow.jpg" alt="YSlow - screen shot." width="480" height="300" /></a>

<a href="https://developer.yahoo.com/yslow/">YSlow</a> is a Firefox extension created by Yahoo! developers that integrates with Firebug (therefore you need to have Firebug enabled for it to work). YSlow analyzes a Web page for front-end performance and, in its simplest usage, gives you a letter grade (A being the best and F being the poorest) for each of the <a href="https://developer.yahoo.com/performance/rules.html">best practices for speeding up  your website</a>.

YSlow also allows you to inspect in detail things that are essential for a high-performance website. For example, the <em>Stats</em> view gives you the total size of a Web page and a summary of items that are loaded when the Web page is requested (i.e. style sheets, JavaScript files, Flash objects and images), so that you can hunt down the bottlenecks that cause a Web page to load slowly.

The <em>Components</em> view outlines every single component of a Web page in tabular format and allows you to inspect it to see attributes such as size, expiration date (for cached files), whether it uses server-side compression (Gzip) and response time (how long the component took to load).

<strong>Further Reading</strong>

*   [What the 80/20 Rule Tells Us about Reducing HTTP Requests](https://yuiblog.com/blog/2006/11/28/performance-research-part-1/)
*   [Maximizing Parallel Downloads in the Carpool Lane](https://yuiblog.com/blog/2007/04/11/performance-research-part-4/)
*   [Yahoo's Problems Are Not Your Problems](https://www.codinghorror.com/blog/archives/000932.html): counter-arguments for some of the rules developed by Yahoo!, such as penalizing you for not having a Content Delivery Network.</p>

## Internet Explorer Web (Edge) Developer Toolbar

<a href="https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ac63b5b-3a51-41c9-9528-110bf06338c8/04-ie-web-developer-toolbar.jpg" alt="Internet Explorer Web Developer Toolbar - screen shot." width="480" height="300" /></a>

If you need similar functionality to that of Firebug and Web Developer for Firefox, but want to debug, inspect and tune your Web pages and applications on the Internet Explorer browser, check out the Internet Explorer Web Developer Toolbar. The IE Web Developer Toolbar, when enabled, opens a toggle-able pane located at the bottom of the Web browser, giving you access to many helpful options for exploring Web page components.

For example, you can experiment to see how page elements work by editing the Web page's DOM and HTML directly in the browser, allowing you to quickly change and edit DOM elements to see what happens when you perform certain actions or modify certain parts of the code. You can also debug, test and inspect JavaScript with the IE Web Developer Toolbar, giving you options for setting breakpoints, seeing the call stack and exploring variable attributes.

It has a ton of other helpful features, such as selectively disabling IE settings (to see how your Web pages degrade in IE); the ability to view the HTML and CSS source of any Web page with syntax-highlighting; and an in-browser ruler to help you measure things on a Web page.</p>

## Fiddler Web Debugger

<a href="https://www.fiddlertool.com/fiddler/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c52574-2e04-470f-ae29-ef4231c248ce/05-fiddler.jpg" alt="Fiddler Web Debugger - screen shot." width="480" height="300" /></a>

<a href="https://www.fiddlertool.com/fiddler/">Fiddler</a> is an Internet Explorer extension that analyzes and profiles a Web page's HTTP traffic. If you've ever wanted to know exactly what happens when a client requests a Web page, Fiddler is the tool that'll help you do the job. The <em>HTTP Statistics</em> view exposes all components and files required to generate a particular page, giving you details such as the total number of HTTP requests, total page weight, HTTP response headers and cache expiration.

Fiddler permits you to set up breakpoints, allowing you to step through and edit HTTP traffic (to see how it would affect your Web page), a useful feature for analyzing AJAX-based interaction and potential security flaws in a Web application. Perhaps what makes Fiddler so powerful is its extensibility, allowing you to create your own scripts (or import other developers' scripts) to perform certain tasks or make interface modifications to the extension itself.

<strong>Further Reading</strong>

*   [Fiddler PowerToy - Part 1: HTTP Debugging](https://msdn.microsoft.com/en-us/library/bb250446.aspx)
*   [Using Fiddler with non-Internet Explorer Browsers](https://www.west-wind.com/WebLog/posts/4085.aspx)

## DebugBar

<a href="https://www.debugbar.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4779f6b9-82a6-413c-8256-4c83567d14cf/06-debugbar.jpg" alt="DebugBar - screen shot." width="480" height="300" /></a>

<a href="https://www.debugbar.com/">DebugBar</a> is a debugging in-browser extension for the Internet Explorer browser. It has many helpful features, such as the ability to send a Web page screenshot via email, a color picker, the ability to view both the original and interpreted code (i.e. if you use JavaScript to manipulate the styles of a DOM object, then you can see the interpreted HTML source code of that manipulation) and a <a href="https://www.my-debugbar.com/wiki/CompanionJS/ConsoleAPI">Console API</a> (after installing Companion.JS) to help you gain information through a command-line interface about particular components of a Web page.

DebugBar is free for personal and educational use, but you are required to buy a license if you use it for commercial purposes.</p>

## HttpWatch

<a href="https://www.httpwatch.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe16a9c2-bdc2-4680-9277-496f64451c40/07-httpwatch.jpg" alt="HttpWatch - screen shot." width="480" height="300" /></a>

<a href="https://www.httpwatch.com/">HttpWatch</a> is another HTTP traffic viewer and debugger for Firefox and Internet Explorer that is similar to Fiddler. It has many unique features and a more intuitive, less intimidating interface than Fiddler. Some notable features are the ability to generate request-level time charts (useful for documentation and presentation purposes); decryption of HTTPS traffic to help you debug, inspect and tweak your secure <a href="https://en.wikipedia.org/wiki/Secure_Sockets_Layer">SSL-based connections</a>; and the ability to export captured data to XML and CSV formats for importing into spreadsheet applications such as Microsoft Excel or Google Spreadsheets.

HTTPWatch has a <em>Basic edition</em>, which is free, and a <em>Professional edition</em>, which has more options. Check out <a href="https://www.httpwatch.com/editions.htm">the comparison table between the two editions</a> to see the exact differences.</p>

## Live HTTP Headers

<a href="https://livehttpheaders.mozdev.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc04861e-f380-400a-85f0-966de7b270c7/08-livehttpheaders.jpg" alt="LiveHTTPHeaders - screen shot," width="480" height="300" /></a>

<a href="https://livehttpheaders.mozdev.org/">Live HTTP Headers</a> is a Firefox extension that allows you to inspect <a href="https://en.wikipedia.org/wiki/List_of_HTTP_headers">HTTP request and response headers</a>. Exploring HTTP headers allows you to debug Web applications, glean some information about the website's server and inspect cookies sent to the client requesting the page.

For example, the <em>Server</em> response header gives you a website's HTTP server type (Apache, IIS, nginx, etc.), the HTTP server version and the operating system (though server administrators can remove or limit the information you see for security purposes).</p>

## Web Accessibility Toolbar

<a href="https://www.paciellogroup.com/resources/wat/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e45faa8-ef31-4b62-9f5f-fb39afb80690/09-web-accessibility-toolbar.jpg" alt="Web Accessibility Toolbar - screen shot." width="480" height="300" /></a>

The <a href="https://www.paciellogroup.com/resources/wat/">Web Accessibility Toolbar</a> is a freeware extension for Internet Explorer and Opera that gives you a slew of options for quickly evaluating and analyzing your Web content's accessibility. It has validation options for submitting your URL to content accessibility web services, a grayscale converter to simulate the user experience of individuals with color-blindness and poor eyesight, and a search function for particular page structures (e.g. finding list objects and unordered lists).</p>

## [Venkman JavaScript Debugger](https://en.wikipedia.org/wiki/Venkman)

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9b6504-133e-49bc-8d7f-a3e7432f3c98/11-venkman.jpg" alt="Venkman JavaScript Debugger - screen shot" width="480" height="300" />

<a href="https://en.wikipedia.org/wiki/Venkman">Venkman</a> is the codename for Mozilla's very own JavaScript debugging environment. It is available as an add-on that can be used to extend browsers such as Firefox, Netscape, and SeaMonkey. It is a robust environment for doing complex JavaScript debugging and troubleshooting. The <em>Console</em> view gives you a command-line interface for interacting with the debugger. It has an excellent <em>Stack</em> view feature that allows you to step through active functions when it reaches breakpoints.

<strong>Further Reading</strong>

*   [Debugging JavaScript Using Venkman, Part 1](https://www.webreference.com/programming/javascript/venkman/)
*   [Venkman 0.9.x Frequently Asked Questions](https://www.hacksrus.com/~ginda/venkman/faq/venkman-faq.html)

## ColorZilla

<a href="https://www.colorzilla.com/firefox/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17660693-c908-4100-9f1a-ea409eb360b2/12-colorzilla.jpg" alt="ColorZilla - screen shot." width="480" height="300" /></a>

<a href="https://www.colorzilla.com/firefox/">ColorZilla</a> is an incredibly simple — but very useful — extension for Firefox. If you've ever wanted to determine what colors are used on a Web page, ColorZilla is the tool for the job. It adds an eyedropper icon to the bottom-left corner of Firefox.

Clicking on the eyedropper icon makes objects on the Web page clickable, and upon clicking a particular section of a Web page, it outputs the hexadecimal, RGB and hue/saturation values of that area . Before ColorZilla, you might have pasted a screen capture of a Web page into a graphics editor like Photoshop and then used the eyedropper tool in the editor to sample colors. ColorZilla saves you time and streamlines color-sampling processes.</p>

## FireShot

<a href="https://screenshot-program.com/fireshot/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dab031d2-b736-4454-852d-729ad87e92ba/13-fireshot.jpg" alt="FireShot - screen shot." width="480" height="300" /></a>

<a href="https://screenshot-program.com/fireshot/">FireShot</a> is an in-browser tool for Firefox and Internet Explorer that allows you to take screenshots and then annotate, edit, organize and export them. Screen-grabbing is a common activity for Web developers to document previews of Web application prototypes and share them with clients, and FireShot gives you a feature-packed in-browser option to manage and streamline your screenshot needs.</p>

## Web Inspector

<a href="https://webkit.org/blog/41/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f763cd2-e0fe-4ea3-8645-6a883e11430c/14-web-inspector.jpg" alt="Web Inspector - screen shot." width="480" height="300" /></a>

<a href="https://webkit.org/blog/41/">Web Inspector</a> is part of the Webkit <a href="https://webkit.org/">open-source browser engine project</a>. It's an ultra-sleek tool for inspecting the DOM hierarchy in a separate, compact HUD-style window. You can easily search the DOM, explore the DOM tree (hierarchy) and have a useful interface for isolating DOM sub-trees and nodes so that you can focus on particular sections of a Web page. The Web Inspector also provides you with a <em>Style</em> pane to explore CSS rules applied to particular page elements.</p>

## FireFTP

<a href="https://fireftp.mozdev.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c37a566b-3b70-4f93-a667-abc1b488fd49/15-fireftp.jpg" alt="FireFTP - screen shot." width="480" height="300" /></a>

<a href="https://fireftp.mozdev.org/">FireFTP</a> is a free, cross-platform Firefox extension for FTP'ing files. It offers several advantages to stand-alone FTP applications, such as its operating system-independent requirements. What's exceptional about FireFTP is that even though it is an in-browser (and free!) application, it has all the features you would expect from a standalone FTP application, such as support for secure (SSL, TLS, SFTP) protocols, a synchronization feature to sync up local and remote files, and directory comparison to help you see what files are missing or different between two directories and much more.</p>

## What's your favorite in-browser tool?

There is an overwhelming amount of in-browser tools for Web development out there. Some are specific to particular Web technologies and set-ups (such as FirePHP for PHP developers, <a href="https://code.google.com/p/sqlite-manager/">SQLite Manager</a> for developers using SQLite databases. If your favorite tool isn't on the list, let us know in the comments section why it's your favorite and why we should check it out.

{{< signature "al" >}}

