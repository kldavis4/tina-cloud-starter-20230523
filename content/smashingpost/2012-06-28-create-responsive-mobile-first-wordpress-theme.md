---
title: 'Create A Responsive, Mobile-First WordPress Theme'
slug: create-responsive-mobile-first-wordpress-theme
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b60e8c6-9068-48e1-a82b-76af0568fe48/wpmanyillus45.jpg
date: 2012-06-28T08:21:26.000Z
author: ellen-bauer
description: >-
  Let’s see what we got: WordPress as this flexible, easy to use Open-Source
  blogging and CMS system. More and more mobile devices flooding the market
  every day and being extremely popular. Plus the need of more beautiful
  designed and coded WordPress themes for users to choose from that will work
  well across all these different devices. So what are we waiting for? Let's get
  to work!
categories:
  - WordPress
  - Themes
  - Responsive Design
---
Let’s assess the situation. WordPress is an extremely popular, flexible, easy to use and open-source blogging and CMS system. More and more mobile devices are flooding the market every day, changing the way people use the Internet. And the need is growing for more beautifully designed and coded WordPress themes that work well across all of these devices. So, what are we waiting for? Let’s get to work!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2396a817-d319-4736-b67e-c0e472fb8318/responsive-wordpress-themes-splash.jpg"><img loading="lazy" decoding="async" class="105745" style="border: 1px solid gray" title="How to create a responsive mobile first WordPress Theme" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2396a817-d319-4736-b67e-c0e472fb8318/responsive-wordpress-themes-splash.jpg" alt="How to create a responsive mobile first WordPress Theme" width="500" height="357" /></a>

At first, the idea of designing and developing a fully responsive, mobile-ready WordPress theme might be overwhelming. You might be thinking, “How do I handle a responsive design with all of this flexible content that a WordPress theme has? What should I consider when designing for touch devices? And do I really have to get rid of drop-down menus and other hover elements on mobile devices?”

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/05/customize-wordpress-admin-easily/#further-reading-on-smashingmag)

*   [Modifying Admin Post Lists In WordPress](https://www.smashingmagazine.com/2013/12/modifying-admin-post-lists-in-wordpress/)
*   [Useful Free Admin Plugins For WordPress](https://www.smashingmagazine.com/2012/03/useful-free-admin-plugins-wordpress/)
*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Inside The WordPress Toolbar](https://www.smashingmagazine.com/2012/03/inside-the-wordpress-toolbar/)

{{% feature-panel %}}

But after doing some research and looking more closely at some of the responsive WordPress themes and theme frameworks out there, you will probably wrap your head around the idea pretty quickly, and the evolving world of WordPress theme design will sound like a huge opportunity that you can’t wait to get started on.</p>

## It’s All About Preparation

Having a <strong>detailed design concept</strong> is even more important for a responsive WordPress theme than for a static-width theme. At this stage, you haven’t decided anything, so nothing will get in your way of creating a clever and practical layout that adapts smoothly to different screens.

First, consider what you want to achieve with your WordPress theme, which user group you are targeting, and what their needs are. With these considerations, you can create a list of useful elements for your layout.</p>

### Creating the Theme’s Concept

Using this list, you can plan your theme by sketching the layout at various screen sizes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147d5dfd-8bf5-4663-9fc8-05ac768a6204/responsive-layout-sketches.jpg"><img loading="lazy" decoding="async" class="120045" title="Responsive WordPress theme layout sketches" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147d5dfd-8bf5-4663-9fc8-05ac768a6204/responsive-layout-sketches.jpg" alt="Responsive WordPress theme layout sketches" width="500" height="357" /></a>

When sketching, be aware that the layout widths you choose are only rough reference points to represent the common screen sizes of today’s smartphones, tablets and desktop computers. Your goal should always be to create a responsive design that adapts smoothly to a wide diversity of screen sizes.

Ethan Marcotte, author of <a href="https://www.abookapart.com/products/responsive-web-design"><em>Responsive Web Design</em></a>, described his approach to responsive Web design in a <a href="https://www.netmagazine.com/interviews/ethan-marcotte-answers-your-responsive-web-design-questions">recent interview</a>, explaining:
<blockquote>I’m a big, big believer of matching breakpoints to the design, not to individual devices. If we’re after more future-proof responsive designs, we should stop thinking in terms of “320px,” “480px,” “768px,” or whatever — the Web’s so much more flexible than that, and those pixels are a snapshot of the Web as we know it today. Instead, we should focus on breakpoints tailored to the design we’re working on.</blockquote>

While working on your concept sketches, also think about which <strong>layout options</strong> to offer in the theme (such as header and sidebar options or multiple widget areas) and how they will adapt to different screen sizes as well.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f488de02-0c1f-449f-bdfb-d93cefc5861e/ipad-layout-sketches.jpg"><img loading="lazy" decoding="async" class="119995" title="Responsive Layout Sketches" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f488de02-0c1f-449f-bdfb-d93cefc5861e/ipad-layout-sketches.jpg" alt="Responsive Layout Sketches" width="500" height="381" /></a><br>
<em>An optional sidebar element in a responsive layout.</em>

### Tools for Concept Sketching

Which tool you use to develop the theme’s concept is not important. Just choose one that allows you to work quickly and that doesn’t interrupt your workflow.

If you feel most comfortable sketching on a piece of paper or in a notebook, go for it. You could also try sketching on an iPad using a popular app such as <a href="https://www.fiftythree.com/paper">Paper</a> by FiftyThree or Bamboo Paper, together with a digital pen like Wacom’s <a href="https://www.wacom.com/en/Products/Bamboo/BambooStylus.aspx">Bamboo Stylus</a>. Working directly on a tablet will make sharing your ideas later with the developer a lot easier. One of my all-time favorite articles is Mike Rohde’s “<a href="https://www.alistapart.com/articles/sketching-the-visual-thinking-power-tool/">Sketching: The Visual Thinking Power Tool</a>,” which promotes sketching as a simple visual tool for thinking.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8def7b39-bfb7-4f6d-8386-239c3d01abe8/ipad-sketching-tool.jpg"><img loading="lazy" decoding="async" class="119999" title="The iPad as a Sketching Tool" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8def7b39-bfb7-4f6d-8386-239c3d01abe8/ipad-sketching-tool.jpg" alt="The iPad as a Sketching Tool" width="500" height="348" /></a><br>
<em>Use your tablet a simple fast sketching tool.</em>

### A Good Concept Saves Time

If you develop the concept precisely at the beginning of the project, you will save a lot of time and effort later in the design process. The layout will adapt to different screen sizes more intelligently if you have thought a lot about the design’s behavior before even opening Photoshop (or your software of choice).</p>

## Theme-Specific Challenges to Consider

Because designing a WordPress theme with very <strong>flexible content</strong> is quite a different challenge than designing a static website, at this early stage of the process you should find solutions to the following theme-specific problems:

### 1. WordPress’ Navigation Menu

Until responsive Web design found its way into WordPress theme designs, most themes seemed to rely on good old-fashioned drop-down menus to give users multi-level navigation. But because drop-down menus rely on mouse hovering, they don’t work well on touch devices.

We already have some smart solutions for developing responsive, touch device-ready navigation. Brad Frost has a very helpful resource comparing common solutions for responsive menus in his post “<a href="https://bradfrostweb.com/blog/web/responsive-nav-patterns/">Responsive Navigation Patterns</a>.”

### 2. Responsive Layout Options

Most themes offer users at least some layout options, such as left or right sidebar, header widget and footer elements. To offer this kind of flexibility in a responsive theme, you will have to consider how all of the layout elements will behave on different screen sizes. For instance, if you want to offer a left sidebar option, consider that the content of this sidebar would appear above the main content area on mobile devices. In most cases, this wouldn’t be the best solution because mobile users want to read the most important content first (such as the latest blog post) without having to scroll down a sidebar.</p>

### 3. Flexible Widget Areas

Widget areas are another challenge for responsive designers. After all, designing one is not easy if you don’t know what kind of content the user will put in it. So, you need to make sure that the design works no matter which and how many widgets are used in the widget areas.</p>

## Enough Headaches. Let’s Get To The Fun.

Because you are creating a responsive website, designing the entire website pixel by pixel in Photoshop and then just handing it over to the developer would result in too static a design and too time-consuming a process.</p>

### Working With Reference Points

Instead, the design process should be used to figure out the general look and feel of the theme. At this stage, you should also work more intensively on the challenges mentioned, such as responsive navigation, layout variations and flexible widget areas.

How you prepare the design for further development will depend partly on the nature of the project and how closely you will work with the developer. In general, showing your design in the three layout versions is a good starting point: smartphone, tablet and desktop. These “screenshots” can then be used as reference points for development.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d752ef-a4fc-467a-acc4-56ffec5c7c47/responsive-design-layouts.jpg"><img loading="lazy" decoding="async" class="120038" title="Responsive web design layouts" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d752ef-a4fc-467a-acc4-56ffec5c7c47/responsive-design-layouts.jpg" alt="Responsive web design layouts" width="500" height="291" /></a><br>
<em>A responsive layout in three variations.</em>

### Designing in the Browser

Design details such as font sizes, white space and button styles can be defined later directly in the browser. Because browsers often treat these elements differently, designing and testing them directly in their final environments is way more efficient.</p>

### Designing for Touch Devices

Because your design will also be used on touch devices, you have to consider the special requirements of these devices. Using a finger to navigate a website is entirely different than using a precise mouse cursor.

This is why buttons and form input fields need to be at the right size. Font sizes and white space should also be applied more generously, so that users can navigate easily and read content comfortably.</p>

### Exercise Your Communication Skills

Staying in constant communication with the developer during the entire process is very important (i.e. if you are not the developer yourself). Especially in a responsive design process, incorporating the developer’s knowledge into your decisions will keep you from having to change things later on.</p>

## Development

After wrapping up the design process, the first decision to make is whether to code the theme from scratch or to use a blank or starter theme (such as Automattic’s Toolbox or the newer <a href="https://themeshaper.com/2012/02/13/introducing-the-underscores-theme/">_s</a> theme).

If you want to work with one of the popular responsive frameworks such as Twitter’s <a href="https://twitter.github.com/bootstrap/">Bootstrap</a> or ZURB’s <a href="https://foundation.zurb.com/">Foundation</a>, then you could use a starter theme that already includes the framework, such as <a href="https://bootstrapwp.rachelbaker.me/">BootstrapWP</a> or <a href="https://320press.com/wp-foundation/">WordPress Foundation</a>. Another popular starter theme is <a href="https://themble.com/bones/">Bones</a>, which uses <a href="https://stuffandnonsense.co.uk/projects/320andup/">320 and Up</a> as a mobile-first boilerplate.

Of course, the way you start a theme will always depend on the project and your personal preferences. But if you’re still learning, then a blank theme would serve as a solid foundation for development.</p>

### Go Mobile First

A smart approach is to design and develop for the smallest layout first (i.e. smartphones) and then work your way up to tablet and desktop screen sizes. To get further insight into the mobile-first approach to Web design, read the book <a href="https://www.abookapart.com/products/mobile-first"><em>Mobile First</em></a> by Luke Wroblewski.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04b621e-3d2e-4592-870f-12ef25067eab/mobile-first.jpg"><img loading="lazy" decoding="async" class="120002" title="Mobile First Web Design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04b621e-3d2e-4592-870f-12ef25067eab/mobile-first.jpg" alt="Mobile First Web Design" width="500" height="311" /></a><br>
<em>Design and develop your WordPress theme starting with the smallest size first.</em>

### Supporting Media Queries in Old Browsers

With the smartphone layout as your default, you will need to rely on a JavaScript solution such as <a href="https://github.com/scottjehl/Respond">Respond.js</a> to support media queries in old browsers (such as Internet Explorer 7 and 8).

Alternatively, you could add CSS classes for old IE browsers through conditional comments, and then add CSS styles to set a maximum width for old IE browsers outside of your media queries. You can find a detailed explanation of this method in the article “<a href="https://jonikorpi.com/leaving-old-IE-behind/">Leaving Old Internet Explorer Behind</a>.”

### Images in a Responsive Theme

With the release of high-pixel-density devices such as the new iPad and new MacBook Pro, you will also need to <strong>reconsider the images</strong> in your theme.

Alternatives to images would be to use a CSS solution or use <a href="https://css-tricks.com/flat-icons-icon-fonts/">icon fonts</a>. Fewer images will also result in a much more lightweight theme, which will speed up performance on slow mobile Internet connections. Trent Walton shares his reflections on the Retina-optimization of Web design in his article “<a href="https://trentwalton.com/2012/05/08/in-flux/">In Flux</a>.”

## Test, Test, Test

Particularly when developing a responsive theme, testing your work live as soon and as often as possible is critical. This way, you can quickly correct styles during development as necessary. Also, test whether fonts are easy to read and whether images, gallery sliders and embedded elements such as video work correctly on different devices.</p>

### How to Test on Mobile Devices

Of course, checking your theme on one of the many screen-resolution-testing tools, such as <a href="https://quirktools.com/screenfly/">Screenfly</a>, during development is very helpful, too.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/676b0c86-d860-402e-8682-dd60f8fccec8/screenfly-testing.jpg"><img loading="lazy" decoding="async" class="120005" title="Testing a web design with Screenfly" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/676b0c86-d860-402e-8682-dd60f8fccec8/screenfly-testing.jpg" alt="Testing a web design with Screenfly" width="500" height="473" /></a><br>
<em>The mobile version of <a href="https://www.unitedpixelworkers.com/">United Pixelworkers</a>’s website tested with Screenfly.</em>

But because of the different behavior of mobile browsers, touchscreens and high-density screens, <strong>constantly testing your theme on actual devices</strong> is important.

Unless you work for a big company, finding ways to test your theme during the development process can be quite a challenge. Of course, you won’t be able to test on all of the devices out there, but besides the devices that you own, you could ask friends, family, other freelancers and coworkers to help you test. You can also visit your local electronics store to test on the devices there.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5707278f-11a8-4592-b839-116fdf98d336/device-testing.jpg"><img loading="lazy" decoding="async" class="120007" title="Test your WordPress theme on multiple devices" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5707278f-11a8-4592-b839-116fdf98d336/device-testing.jpg" alt="Test your WordPress theme on multiple devices" width="500" height="364" /></a><br>
<em>Test your WordPress theme on various devices as often as you can.</em>

A helpful post with a lot of testing advice is part 5 of the recent “<a href="https://www.netmagazine.com/tutorials/build-responsive-site-week-going-further-part-5">Build a Responsive Site in a Week</a>” tutorial series on .NET magazine.</p>

## Responsive Theme Vs. Mobile Plugin

A mobile theme plugin such as the popular <a href="https://wordpress.org/extend/plugins/wptouch/">WPtouch plugin</a> can be a great temporary solution to give mobile users a better experience on an existing website. In most cases, offering visitors an optimized mobile experience with the help of a plugin is probably better than not optimizing at all.

But in the long term, a fully responsive theme has many advantages to a plugin:

*   The website can maintain its **unique branding** across all devices.
*   Users will get the **same experience** on all devices and thus have less trouble navigating the website.
*   The website will be **easier to maintain** (the administrator won’t need to install and update the plugin).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a17fea-1f65-462a-9919-afb06cbc772c/responsive-vs-plugin.jpg"><img loading="lazy" decoding="async" class="120010" title="Responsive theme vs mobile theme plugin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a17fea-1f65-462a-9919-afb06cbc772c/responsive-vs-plugin.jpg" alt="Responsive theme vs mobile theme plugin" width="500" height="417" /></a><br>
<em>A responsive WordPress theme on the left, and a mobile plugin at work on the right.</em>

## Conclusion

Responsive Web design is often still described as a trend. And some might quietly hope that the trend will pass sooner or later. But responsive Web design is so much more than a trend: <strong>it’s a new mindset</strong>, as <a href="https://twitter.com/smashingmag/statuses/175477183551242240">has been said</a>:
<blockquote>It’s such a shame that Responsive design is often degraded to being a ‘Web design trend’. It isn’t. It’s a new mindset.</blockquote>

In a multiple-device world, where the Internet seems to be available everywhere, responsive Web design feels so much more like a natural process that is just starting to show its potential.

So, what should our job as theme designers and developers be? Because responsive WordPress themes are still so new and in constant development, we must not be afraid to start from scratch, search for improvements and continue learning. And let’s share our knowledge and experience with each other along the way.

{{< signature "al" >}}

