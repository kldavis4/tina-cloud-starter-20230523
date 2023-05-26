---
title: 'Responsive Nav: A Simple JavaScript Plugin For Responsive Navigation'
slug: javascript-plugin-for-responsive-navigation
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2808b59a-deae-4083-8a7f-f58912c69789/responsivenav-new1.png
date: 2013-04-09T09:25:33.000Z
author: viljami-salminen
description: >-
  There are several ways to make navigation responsive, and usually the solution
  we need is quite straightforward. But despite the apparent simplicity, there
  are many underlying factors which, when thought through and implemented
  properly, can make a simple solution even better without adding more
  complexity to the user interface.
categories:
  - Coding
  - Tools
  - JavaScript
  - Navigation
  - Plugins
  - Optimization
---
There are several ways to make navigation responsive, and usually the solution we need is quite straightforward. But despite the apparent simplicity, there are many underlying factors which, when thought through and implemented properly, can make a simple solution even better without adding more complexity to the user interface.

One of the problems I’ve encountered while building responsive navigations is that browsers currently don’t support CSS3 transitions to a height which is defined <code>auto</code>. Most of the time, we shouldn’t use fixed height either because the height of menu items might not be the same in all browsers, and the number of items may change. I also always try to reduce the weight of pages I build, so I’ve been wanting <strong>a solution that doesn’t require a big library</strong> such as jQuery to work.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Navigation On Complex Websites](https://www.smashingmagazine.com/2013/09/responsive-navigation-on-complex-websites/)
*   [<span class="headline">Sticky Menus Are Quicker To Navigate</span>](https://www.smashingmagazine.com/2012/09/sticky-menus-are-quicker-to-navigate/)
*   [Progressive And Responsive Navigation](https://www.smashingmagazine.com/2012/02/progressive-and-responsive-navigation/)

Today, I’m pleased to introduce <a href="https://responsive-nav.com">Responsive Nav</a>, a free and open-source JavaScript plugin that solves these problems and more in one tiny package. It’s released under the <a href="https://opensource.org/licenses/MIT">MIT License</a>, so you can use it in all of your projects for free and without any restrictions. The solution is not one size fits all, nor is it meant to be. But for those who are looking for a solution that does one thing well, it’s definitely a good choice.

{{% feature-panel %}}

<a href="https://responsive-nav.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="125985" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa62999f-1c33-4e1a-bf95-85685ce115ff/responsivenav-new.png" alt="Official site of Responsive Nav plugin." width="500" height="354" /></a><br>
<em>The official site, view live at <a href="https://responsive-nav.com/">responsive-nav.com</a>.</em>

## Features

Responsive Nav is a tiny JavaScript plugin which weighs only 1.6 KB minified and Gzip’ed, and helps you to create a toggled navigation for small screens. It uses touch events and CSS3 transitions for the best possible performance. It also contains a “clever” workaround that makes it possible to transition from <code>height: 0</code> to <code>height: auto</code>, which isn’t normally possible with CSS3 transitions.

*   Simple, semantic markup.
*   Weighs only 1.6 KB minified and Gzip’ed.
*   Doesn’t require any external library.
*   Uses CSS3 transitions and touch events.
*   Removes the 300 ms delay between a physical tap and the click event.
*   Makes it possible to use CSS3 transitions with `height: auto`.
*   Built with accessibility in mind, meaning that everything works on screen readers and with JavaScript disabled, too.
*   Works in all major desktop and mobile browsers, including IE 6 and up.
*   Free to use under the MIT license.

<a href="https://responsive-nav.com/demo"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="125987" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d4e3b8-69c6-4006-bb24-3e5e64ffc4c4/example-opt.png" alt="The official demo of Responsive Nav plugin." width="500" height="452" /></a><br>
<em>The official demo, View live at <a href="https://responsive-nav.com/demo">responsive-nav.com/demo</a>.</em>

## How It Works?

Responsive Nav is the successor of <a href="https://tinynav.viljamis.com/">TinyNav.js</a> which was released in 2011. While TinyNav worked so that it converted a regular navigation to a select menu, Responsive Nav only hides the original navigation and adds a toggle which opens and closes it. Responsive Nav doesn’t basically alter the html structure of the document at all, so it’s in that sense a much simpler solution.

Responsive Nav works by calculating in the background the max-height needed to fit all the menu items. When the user taps the navigation toggle the plugin uses CSS3 transitions to transition from a height that is set to 0 to the max-height it calculated earlier. Responsive Nav also attaches a <code>touchstart</code> event listener to the toggle, which makes it possible to remove the default 300 ms delay that happens when using click events.</p>

## Why Choose This Over Another Solution?

Responsive Nav is lightweight and doesn’t depend on any external library. The navigation opens instantly on <code>touchstart</code> — no more 300 ms delay on touch devices. It’s also (as far as I know) the only responsive navigation plugin out there that uses CSS3 transitions with variable height (although correct me if I’m wrong). Responsive Nav is also built with accessibility in mind, meaning that everything works on screen readers and with JavaScript disabled, right out of the box. Finally, Responsive Nav <strong>has been tested to work on 60+ mobile and desktop browsers</strong>, so that you would’t have to worry about browser support. <a href="https://github.com/viljamis/responsive-nav.js#tested-on-the-following-platforms">See the full list</a> of tested platforms.</p>

## Demo And Download

*   [Official website](https://responsive-nav.com), including instructions (works as a demo, too!)
*   [Live Demo](https://responsive-nav.com/demo)
*   [Download](https://github.com/viljamis/responsive-nav.js/archive/master.zip) (ZIP archive includes seven examples)
*   [GitHub repository](https://github.com/viljamis/responsive-nav.js)

<em>(al) (ea)</em>

