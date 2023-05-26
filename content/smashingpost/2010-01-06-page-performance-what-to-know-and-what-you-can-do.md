---
title: 'Are You Loosing Traffic By Poor Website Performance?'
slug: page-performance-what-to-know-and-what-you-can-do
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51e3ab90-06fd-40bb-be1e-ab480d100870/performance.jpg
date: 2010-01-06T13:48:05.000Z
author: christian-heilmann
summary: >-
  Website performance is a hugely important topic, so much so that the big companies of the Web are obsessed with it. For the Googles, Yahoos, Amazons and eBays, slow websites mean fewer users and less happy users and thus lost revenue and reputation.
description: >-
  Website performance is a hugely important topic, for big companies such 
  as Google, Yahoo, Amazon, eBay, slow websites mean fewer users, less happy 
  users, and thus lost revenue and reputation.
categories:
  - Coding
  - PHP
  - Performance
---

In your case, annoying a few users wouldn’t be much of a problem, but if millions of people are using your product, you’d better be snappy in delivering it. For years, Hollywood movies showed us how fast the Internet was: time to make that a reality.

Even if you don’t have millions of users (yet), consider one very important thing: people are consuming the Web nowadays less with fat connections and massive computers and more with mobile phones over slow wireless and 3G connections, but they still expect the same performance. Waiting for a slow website to load on a mobile phone is doubly annoying because the user is usually already in a hurry and is paying by the byte or second. It’s 1997 all over again.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/100e072c-0b68-4da1-a081-1b3da38e9f7b/optimization.gif" alt="Screenshot" width="489" height="330" />
</figure>

**Performance is an expert’s game... to an extent**. You can do innumerable things to make a website perform well, and much of it requires in-depth knowledge and boring testing and researceh. I am sure a potential market exists for website performance optimization, much like there is one now for search engine optimization. Interestingly, Google recently announced that it will factor performance into its search rankings, so this is already happening. That said, you can do a lot of things without having to pay someone to point out the obvious.

## Know Your Performance Blockers

Performance can be measured in various ways. One way is technical: seeing how fast a page loads and how many bytes are transferred. Another is perceived performance, which ties into usability testing. This can only be measured by testing with users and seeing how satisfied they are with the speed of your interface (e.g. do they start clicking on your JavaScript carousel before it is ready?).

The good news (and hard truth) about performance is that **80 to 90% of poor performance happens in the front end**. Once the browser gets the HTML, the server is done and the back-end developer can do nothing more. The browser then starts doing things to our HTML, and we are at its mercy. This means that to achieve peak performance, we have to optimize our JavaScript, images, CSS and HTML, as well as the back end.

So here are the things that slow down your page the most.

### External Resources (Images, Scripts, Style Sheets)

Every time you load something from another server, the following happens:

1. The browser opens up the Internet’s address book and looks up the number associated with the name of the server that’s holding the things you want (i.e. its [DNS](https://en.wikipedia.org/wiki/Domain_Name_System) entry).
2. It then negotiates a delivery.
3. It receives the delivery (waiting for all the bytes to come in).
4. It tries to understand what was sent through and displays it.

**Every request is costly** and slows down the loading of the page. This is also caused by browsers loading things in chunks (usually four at a time) rather than all at the same time. This is akin to ordering a product from a website, choosing the cheapest delivery option and not being at home between 9:00 am and 5:00 pm. If you include several JavaScript libraries because you like a certain widget in each, then you’ll double, triple or even quadruple the time that your page takes to load and display.

{{% feature-panel %}}

### Scripts

JavaScript makes our websites awesome and fun to use, but it can also make for an annoying experience.

The first thing to know about scripts that you include in a document is that they are not HTML or CSS; the browser has to call in an expert to do something with them. Here is what happens:

1. Whenever the browser encounters a `<script>` block in the document, it calls up the JavaScript engine, sits back and has a coffee.
2. The script engine then looks at the content in the script block (which may have been delivered earlier), sighs, complains about the poor code, scratches its head and then does what the script tells it to do.
3. Once the script engine is done, it reports back to the browser, which puts down its coffee, says good-bye to the script engine and looks at the rest of the document (which might have been changed, because the script may have altered the HTML).

The moral of the story is to **use as few script blocks as possible** and to put them as far down the document as possible. You could also use clever and lazy JavaScript, but more on that later.

### Images

Here is where things get interesting. Optimizing images has always been the bane of every visual designer. We build our beautiful images in Illustrator, Photoshop or Fireworks and then have to save them as JPG, GIF or PNG, which changes the colors and deteriorates the quality; and if we use PNG, then IE6 arrives as the party-pooper, not letting us take advantage of PNG’s cool features.

**Optimizing your images is absolutely necessary** because most of the time they are the biggest files on page. I’ve seen people jump through hoops to cut their JavaScript down from 50 KB to 12 KB and then happily use a 300 KB logo or "hero shot" in the same document. Performance needs you!

Finding the right balance between visual loss and file size can be daunting, but be grateful for the Web preview tool, because we didn’t always have it. I recall using Photoshop 4 and then Photoshop with the Ulead SmartSaver, for example.

The interesting thing about images, though, is that after you have optimized them you can still save many more bytes by stripping unnecessary data from the files and running the files through tools that further compress the images but are non-lossy. The bad news is that many of them are out there, and you’ll need different ones for different image formats. The good news is that tools exist that do all that work for you, and we will come back to this later. For more advanced optimizaition techniques feel free to take a closer look at the Smashing Magazine’s articles [Clever JPEG Optimization Techniques](https://www.smashingmagazine.com/2009/07/01/clever-jpeg-optimization-techniques/), [PNG Optimization Guide](https://www.smashingmagazine.com/2009/07/25/png-optimization-guide-more-clever-techniques/) and [Clever PNG Optimization Techniques](https://www.smashingmagazine.com/2009/07/15/clever-png-optimization-techniques/).

## Simple Tools You Can Use Now To Improve Performance

All of those companies that obsess about page performance offer tools that allow you to check your own website automatically and make it easy to work around problems.

### Test Your Performance

The first thing to do is find out how your website can be optimized. Here are three great tools (among others that crop up all the time) to use and combine.

### Yahoo’s YSlow

[YSlow](https://developer.yahoo.com/yslow/) is a Firebug add-on from Yahoo that allows you to automatically check your website for performance issues. The results are ranked like American school grades, with A being the best and F being the worst. The grades are cross-linked to best practice documentation on the Yahoo performance pages. You can test several settings: "classic YSlow," which is targeted to Yahoo-sized websites and "small site or blog." Results are listed clearly and let you click through to learn.

[![YSlow Smashing mag overall grade.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8cfcb83-eaf8-4aa1-95f3-9e83c2b3144d/image1-new.jpg)](https://www.flickr.com/photos/codepo8/4198617150/sizes/o/)

In the components view, YSlow lists all of the issues it has found on your website and how serious they are:

[![Smashing Magazine on YSlow components view.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326b96a4-731f-4757-b500-314f2cddfa64/image2new.jpg)](https://www.flickr.com/photos/codepo8/4197863687/sizes/o/)

The statistics view in YSlow gives you all information in pie charts:

[![Smashing Magazine in YSlow - statistics.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1c5b980-23c6-4ca5-85eb-6fa095484514/image3.gif)](https://www.flickr.com/photos/codepo8/4198630210/sizes/o/)

The tools section in YSlow offers a lot of goodies:

- [JSLint](https://www.jslint.com/) Checks the quality and security of your JavaScripts by running them through JSLint.
- All JS Shows all JavaScript code in a document.
- All JS Beautified Shows all JavaScript code in a document in an easy-to-read format
- All JS Minified Shows all JavaScript code in a document in a minified format (i.e. no comments or white space)
- All CSS Show all CSS code in a document
- All Smush.it Automatically compresses all of your images (more on this later).
- Printable View Creates a printable document of all of YSlow’s results (great for showing to a client after you’ve optimized the page!)

[![YSlow tools.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aed6cb53-19b8-493f-8f3a-42ac4c442eac/image4.gif)](https://www.flickr.com/photos/codepo8/4197872303/sizes/o/)

{{% ad-panel-leaderboard %}}

### Google’s Page Speed

Like YSlow, [Page Speed by Google](https://code.google.com/speed/page-speed/) is also an add-on for Firebug. Its main difference is that it does a lot of the optimization for you and provides the modified code and images immediately.

[![Smashing Magazine on Google Page Speed.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e572a522-dee4-4371-bcc4-aef754399fee/4198657574-5865ccbda5.jpg)](https://www.flickr.com/photos/codepo8/4198657574/sizes/o/)

Page Speed’s other extra is that it monitors the overall activity of your page, allowing you to see when a document loads other resources after it has been loaded and to see what happens when a user rolls over elements or opens tabs and menus that load content via AJAX.

[![Smashing Magazine Page Speed Activity.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa3137b3-0dad-4154-a845-b4880397294f/4198689498-2e2acd4ccf.jpg)](https://www.flickr.com/photos/codepo8/4198689498/sizes/o/)

Be careful with this feature, though: it hammers your browser quite hard.

### AOL’s WebPageTest

Rather late to the game, [AOL’s WebPageTest](https://www.webpagetest.org/) is an application with some very neat features. (It is also available as a desktop application, in case you want to check Intranets or websites that require authentication.)

WebPageTest allows you to run tests using either IE8 or IE7 from a server in the US or the UK, and it allows you to set all kinds of parameters, such as speed and what to check for:

[![Pagetest web page performance test.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d9beef-72da-43ce-a239-90002e41d2c3/4198701698-900086ced1.jpg)](https://www.flickr.com/photos/codepo8/4198701698/sizes/o/)

Once you have defined your parameters and the testing is completed, you will get in-depth advice on what you can do to optimize. You’ll get:

- A summary,
- Detailed results,
- A performance review,
- An optimization report,
- The content breakdown,
- The domain breakdown,
- A screenshot.

[![Web page performance test results.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc70e9dd-7886-4ed4-8b78-743eceeddf61/4198726620-9a32df8ff4.jpg)](https://www.flickr.com/photos/codepo8/4198726620/sizes/l/)

One very cool feature of WebPageTest is the visual recording you get of how long it takes for page elements to show up on screen for users. The following screenshot compares the results of this blog, Ajaxian and Nettuts+:

[![Web page visual comparison by you.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a77f5fb7-ce33-48da-9ed1-9204a200862d/4198697096-7eff3706bf.jpg)](https://www.flickr.com/photos/codepo8/4198697096/sizes/o/)

You can even create a video of the rendering, which is another very cool thing to show clients.

Once you get the test results, it is time to fix any problems.

### Use Image Sprites

[Image Sprites](https://www.alistapart.com/articles/sprites/) were first discussed in an article published by Dave Shea and based on the work of [Petr Stanicek](https://wellstyled.com/css-nopreload-rollovers.html). They have been covered [extensively here before](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/), but understanding their full benefit is important before you start using them:

- All of your images will be available as soon as the main image has loaded (no flickering on roll-overs or other annoyances).
- One HTTP request is made, instead of dozens (or hundreds, in some cases).
- Images have a much higher chance of staying cached on the user’s machine because they are contained in a single file.

### Optimize Your Images

You know now that Page Speed can automatically optimize your images. Another way to do this is with Yahoo’s Smush It, which is a set of image optimization tools that analyze your images, create the smallest possible versions and sends you a ZIP file of them all.

You can use [reSmush.it](https://resmush.it/). reSmush.it is a FREE API that provides image optimization. reSmush.it has been implemented on the most common CMS such as Wordpress, Drupal or Magento.

[![Yahoo! Smush.it™](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86817235-25a4-496f-975c-cc1f48d8e9dd/4197963651-f99567a8f0.jpg)](https://www.flickr.com/photos/codepo8/4197963651/sizes/o/)

[![Smush.it optimization results.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed6f75ca-7136-42ea-a535-5c66df7963f3/4197968099-720bc44915.jpg)](https://www.flickr.com/photos/codepo8/4197968099/sizes/o/)

{{% ad-panel-leaderboard %}}

### Collate Scripts and Load Scripts on Demand

As noted, try not to spread your `<script>` nodes all over the document, because the browser stops whenever it encounters one. Instead, insert them as far down in the document as possible.

JavaScript can be added dynamically to the page after the page has loaded. This technique is called "lazy loading," and several tools are available to do it. Jan Jarfalk has one to lazy load jQuery plug&ndash;ins.

Some JavaScript libraries let you import only what you really need, instead of bringing in the whole singing&ndash;and&ndash;dancing library. YUI, for example, has a configurator that allows you to pick and choose what you need from the library and either gives you a single URL where you can get the different scripts or creates a JavaScript that loads them on demand:

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adf0513c-afc8-47b6-b38a-3e171d8ce183/4196935915-39584ab3e9.jpg" alt="yui configurator" />
</figure>

Notice that a tab tells you what the overall size of the library will be.

The main trick in lazy loading is to dynamically create script nodes with JavaScript after the page has loaded and only when they are needed. It has been a best practice for displaying badges and widgets for a long time now.

### Use Network Distributed Hosting

If you use a library or CSS provided by a library, make sure to use the hosted versions of the files. In the case of YUI, this is done for you if you use the configurator. And you can pick from Yahoo or Google’s network.

For other libraries, there is a [Google code repository of AJAX libraries](https://code.google.com/apis/ajaxlibs/). This is useful for a few reasons:

- Visitors to your website will get the JavaScript and CSS from the server that is as geographically close to them as possible and won’t have to wait for your server to send the information from around the globe.
- There is a high probability that these servers are faster than yours.
- Visitors who have visited other websites that use the same includes will already have them on their computers and won’t need to load them again.
- You save on bandwidth and can easily upgrade the library by changing the version number of the include.

You might be interested in the following related posts:

- [Improving Smashing Magazine’s Performance: A Case Study](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)
- [Why Performance Matters, Part 1: The Perception Of Time](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
- [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
- [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)

## Watch Some Videos

If you want to see how some of this work, check out the following videos, especially Nicole Sullivan’s, which shows some very cool CSS tricks:

- Using YSLow2
- [Using Google Page Speed](https://youtube.com/watch?v=a-9pCfyYPdQ)
- [Nicole Sullivan tells you not to blame the rounded corners but to design for fast websites](https://www.youtube.com/watch?v=7HC3OV1dDZ4)

## Follow The Leaders

To learn more about website performance, here are some resources and people to follow. (Be warned: some of the content is technically tough.)

- [The Yahoo Developer Network Performance Section](https://developer.yahoo.com/performance/) Home of YSLow and probably the first official performance research website.
- [Performance Planet](https://www.perfplanet.com/) A collation of all performance blogs and posts in one RSS feed.
- [Steve Souders](https://www.stevesouders.com/) ([@souders](https://www.twitter.com/souders)) Ex&ndash;maintainer of the performance section of Yahoo, now at Google. Author of the biggest performance books. And organizer of the Velocity conference.
- [Nicole Sullivan](http://www.stubbornella.org/content/) ([@stubbornella](https://www.twitter.com/stubbornella)) Ex&ndash;team member of the performance group at Yahoo and co&ndash;creator of Smush.it. Also CSS performance goddess with great tips for designers. Currently working on making Facebook perform better.
- [Stoyan Stefanov](https://phpied.com/) ([@stoyanstefanov](https://www.twitter.com/stoyanstefanov)) Coder of Smush.it and member of the performance team at Yahoo. Created his own [advent calendar of performance tips](https://www.phpied.com/performance-advent-calendar-2009/) this year, and runs Performance Planet, as mentioned above.
- [Ed Eliot and Stuart Colville](https://website-performance.org/) Builders of the [CSS Sprite Generator](https://css.spritegen.com/).
- [Jake Archibald](https://www.jakearchibald.com/) ([@jaffathecake](https://www.twitter.com/jaffathecake)) Delivered a [great talk on Instant loading offline-first progressive web apps](https://www.youtube.com/watch?v=M1eoAz0mMCg) At Progressive Web Apps.
- [Phillip Tellis](https://bluesmoon.info/) ([@bluesmoon](https://twitter.com/bluesmoon)) Performance junkie at Yahoo.
- And me, their fanboy and person asking for features: [Chris Heilmann](https://christianheilmann.com/) ([@codepo8](https://www.twitter.com/codepo8)).

{{< signature "al, lu, li" >}}
