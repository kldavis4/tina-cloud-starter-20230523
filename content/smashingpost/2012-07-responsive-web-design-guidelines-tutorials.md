---
title: Responsive Web Design Guidelines and Tutorials
slug: responsive-web-design-guidelines-tutorials
image: null
date: 2012-07-02T18:28:19.000Z
author: vitaly-friedman
description: >-
  In this overview you will find the most useful and popular articles we have
  published on Smashing Magazine on Responsive Web Design.
categories: []
---

In this overview you will find the most useful and popular articles we have published on Smashing Magazine on Responsive Web Design.




#### Quick Overview



*   [Design Process In The Responsive Age](#a1)
*   [Responsive Web Design: What It Is and How To Use It](#a2)
*   [A Foot On The Bottom Rung: First Forays Into Responsive Web Development](#a3)
*   [Techniques For Gracefully Degrading Media Queries](#a4)
*   [Responsive Web Design Techniques, Tools and Design Strategies](#a5)

*   [How To Use CSS3 Media Queries To Create a Mobile Version of Your Website](#b1)
*   [Device-Agnostic Approach To Responsive Web Design](#b2)

*   [Progressive And Responsive Navigation](#c1)
*   [Content Prototyping In Responsive Web Design](#c2)
*   [Is There Ever A Justification For Responsive Text?](#c3)

### [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/30/design-process-responsive-age/ "Design Process In The Responsive Age")



You cannot plan for and design a [responsive](https://www.alistapart.com/articles/responsive-web-design/), [content-focused](https://adactio.com/journal/4523/), [mobile-first](https://www.lukew.com/ff/entry.asp?933) <sup class="print_only">1</sup> website the same way you’ve been creating websites for years—you just can’t. If your goal is to produce something that is not fixed-width and serves smaller devices just the styles they require, why would you use a dated process that contradicts those goals?

<figure><a href="https://www.smashingmagazine.com/2012/05/30/design-process-responsive-age/"><img loading="lazy" decoding="async" class="112248" title="Design Process In the Responsive Age" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b65ed49-3664-47ea-8538-5d4286dd9645/change-process-feature-image500.jpeg" alt="Design Process In the Responsive Age" /></a></figure>

I’d like to walk you through some problems caused by using old processes with responsive design. Let’s look into an evolving design process [we’ve](https://seesparkbox.com/ "SparkBox") <sup class="print_only">2</sup> been using with some **promising new deliverables and tools**. This should provide a starting point for you to freshen up your own process and bring it into the responsive age.



[Read more...](https://www.smashingmagazine.com/2012/05/30/design-process-responsive-age/)



### [Responsive Web Design: What It Is and How To Use It](https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/ "Permanent Link to Responsive Web Design: What It Is and How To Use It")



Almost every new client these days wants a mobile version of their website. It's practically essential after all: one design for the BlackBerry, another for the iPhone, the iPad, netbook, Kindle — and all screen resolutions must be compatible, too. In the next five years, we'll likely need to design for a number of additional inventions. When will the madness stop? It won't, of course.


<figure><a href="https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/"><img loading="lazy" decoding="async" class="75671" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58bf6358-449a-488b-b42b-8258d98bd3d7/croppinglogo.jpg" alt="Responsive Web Design" width="550" height="321" /></a></figure>



In the field of Web design and development, we're quickly getting to the point of being unable to keep up with the endless new resolutions and devices. For many websites, creating a website version for each resolution and new device would be impossible, or at least impractical. Should we just suffer the consequences of losing visitors from one device, for the benefit of gaining visitors from another? Or is there another option?



[Read more...](https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/)



### [A Foot On The Bottom Rung: First Forays Into Responsive Web Development](https://www.smashingmagazine.com/2012/05/18/first-forays-into-responsive-web-development/ "A Foot On The Bottom Rung: First Forays Into Responsive Web Development")



Responsive design is the hottest topic in front-end Web development right now. It’s going to transform the Web into an all-singing, all-dancing, all-devices party, where we can access any information located anywhere in the world. But does responsive design translate well from the text-heavy Web design blogosphere to the cold hard reality of commercial systems?

<figure><a href="https://www.smashingmagazine.com/2012/05/18/first-forays-into-responsive-web-development/"><img loading="lazy" decoding="async" class="111690" title="Availability grid mobile view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45aa152b-b6db-474e-a02d-62b3ac9bad87/starting-with-desktop-ok-mobile.png" alt="Mobile view of availability results" /></a></figure>

Rumors came through our office grapevine that management was looking to revamp our mobile presence. There was talk of multiple apps being built externally that could be used on some of the major mobile devices. Our team had been getting familiar with responsive design and put forward a proposal of doing away with device-specific apps and developing a single responsive website that could be served to both desktop and mobile users. After a few hasty demos and prototypes, the idea was accepted and we began work.



[Read more...](https://www.smashingmagazine.com/2012/05/18/first-forays-into-responsive-web-development/)



### [Techniques For Gracefully Degrading Media Queries](https://www.smashingmagazine.com/2011/08/10/techniques-for-gracefully-degrading-media-queries/ "Permanent Link to Techniques For Gracefully Degrading Media Queries")



Media queries are the third pillar in Ethan Marcotte's implementation of responsive design. Without media queries, fluid layouts would struggle to adapt to the array of screen sizes on the hundreds of devices out there. Fluid layouts can appear cramped and unreadable on small mobile devices and too large and chunky on big widescreen displays. Media queries enable us to adapt typography to the size and resolution of the user's device, making it a powerful tool for crafting the perfect reading experience.


<figure><a href="https://www.smashingmagazine.com/2011/08/10/techniques-for-gracefully-degrading-media-queries/"><img loading="lazy" decoding="async" class="105637" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/232dbac1-9044-49da-bf24-0163029e44ce/broken-media-queries.png" alt="" width="500" height="240" /></a></figure>



CSS3 media queries, which include the browser width variable, are supported by most modern Web browsers. Mobile and desktop browsers that lack support will present a subpar experience to the user unless we step up and take action. I'll outline some of techniques that developers can follow to address this problem.



[Read more...](https://www.smashingmagazine.com/2011/08/10/techniques-for-gracefully-degrading-media-queries/)




### [Responsive Web Design Techniques, Tools and Design Strategies](https://www.smashingmagazine.com/2011/07/22/responsive-web-design-techniques-tools-and-design-strategies/ "Permanent Link to Responsive Web Design Techniques, Tools and Design Strategies")



Back in January, we published an article on responsive design, "[Responsive Web Design: What It Is and How to Use It](https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/)." Responsive design continues to get a lot of attention, but considering how different it is from the "traditional" way of designing websites, it can be a bit overwhelming for those designers who have yet to try it.


<figure><a href="https://www.smashingmagazine.com/2011/07/22/responsive-web-design-techniques-tools-and-design-strategies/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22198853-8458-4ec3-9d0e-e2340da41bcb/trentwalton1.gif" width="500" height="350" /></a></figure>



To that end, we've compiled this roundup of resources for creating responsive website designs. Included are tutorials, techniques, articles, tools and more, all geared toward giving you the specific knowledge you need to create your own responsive designs.



[Read more...](https://www.smashingmagazine.com/2011/07/22/responsive-web-design-techniques-tools-and-design-strategies/)



### [How To Use CSS3 Media Queries To Create a Mobile Version of Your Website](https://www.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/ "Permanent Link to How To Use CSS3 Media Queries To Create a Mobile Version of Your Website")



CSS3 continues to both excite and frustrate web designers and developers. We are excited about the possibilities that CSS3 brings, and the problems it will solve, but also frustrated by the lack of support in Internet Explorer 8\. This article will demonstrate a technique that uses part of CSS3 that is also unsupported by Internet Explorer 8\. However, **it doesn't matter** as one of the most useful places for this module is somewhere that does have a lot of support - small devices such as the iPhone, and Android devices.


<figure><a href="https://www.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/"><img class="50751" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adb9b33a-46f2-4f22-adf6-713aa40db248/dconstruct-desktop-crop.jpg" alt="dConstruct 2010 website on a desktop browser" width="480" height="350" /></a></figure>



In this article I'll explain how, with a few CSS rules, you can create an iPhone version of your site using CSS3, that will work now. We'll have a look at a very simple example and I'll also discuss the process of adding a small screen device stylesheet to my own site to show how easily we can add stylesheets for mobile devices to existing websites.



[Read more...](https://www.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/)



### [Device-Agnostic Approach To Responsive Web Design](https://www.smashingmagazine.com/2012/03/22/device-agnostic-approach-to-responsive-web-design/ "Device-Agnostic Approach To Responsive Web Design")



This is a different take on Responsive Web design. This article discusses how we can better embrace what the Web is about by ignoring the big elephant in the room; that is, how we can rely on media queries and breakpoints without any concern for devices.



[Read more...](https://www.smashingmagazine.com/2012/03/22/device-agnostic-approach-to-responsive-web-design/)



### [Progressive And Responsive Navigation](https://www.smashingmagazine.com/2012/02/13/progressive-and-responsive-navigation/ "Progressive And Responsive Navigation")



Developing for the Web can be a difficult yet rewarding job. Given the number of browsers across the number of platforms, it can sometimes be a bit overwhelming. But if we start coding with a little forethought and apply the principles of progressive enhancement from the beginning and apply some responsive practices at the end, we can easily accommodate for less-capable browsers and reward those with modern browsers in both desktop and mobile environments.

<figure><a href="https://www.smashingmagazine.com/2012/02/13/progressive-and-responsive-navigation/"><img title="Compass" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a3e15b3-e213-4420-95d2-7a8892492476/compass.jpg" alt="screenshot"></a></figure>

[Read more...](https://www.smashingmagazine.com/2012/02/13/progressive-and-responsive-navigation/)



### [Content Prototyping In Responsive Web Design](https://www.smashingmagazine.com/2011/09/26/content-prototyping-in-responsive-web-design/ "Content Prototyping In Responsive Web Design")



While the reality of client work sometimes makes it challenging to gather and produce content prior to starting the design, this is now widely accepted as being necessary. You may have heard this referred to as “[content-driven design](https://www.zeldman.com/2008/05/06/content-precedes-design/ "Content Precedes Design").” I’m not the first to suggest <sup class="print_only">2</sup> that our current approach to **responsive Web design** could be improved by [imparting a bigger role to content](https://adactio.com/journal/4523/ "Content First") in determining how our websites respond. However, I haven’t seen many (if not any) practical explanations on how to do this. I’d like to start this conversation by introducing a theoretical concept called a “**content prototype**.”

<figure><a href="https://www.smashingmagazine.com/2011/09/26/content-prototyping-in-responsive-web-design/"><img class="108716" title="Photoshop’s new file dialog box" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79a2fca6-8d4a-434f-8772-fcf20ddb9840/dialog-box-screenshot1.jpg" alt="Photoshop’s new file dialog box" /></a></figure>

[Read more...](https://www.smashingmagazine.com/2011/09/26/content-prototyping-in-responsive-web-design/)



### [Is There Ever A Justification For Responsive Text?](https://www.smashingmagazine.com/2012/02/27/ever-justification-for-responsive-text/ "Is There Ever A Justification For Responsive Text?")



Depending on who you follow and what you read, you may have noticed the concept of “responsive text” being discussed in design circles recently. It’s not what you might imagine — resizing and altering the typography to make it easier to read on a range of devices — but rather delivering varying amounts of content to devices based on screen size.

One example of this is an [experiment by designer Frankie Roberto](https://www.frankieroberto.com/responsive_text "Frankie Roberto responsive text demo"). Another is the navigation menu on the website for [Sifter App](https://sifterapp.com/ "Sifter App"). Roberto and Sifter are using media queries to actually hide and display text based on screen size (i.e. not rewriting or delivering different content based on context — as one would do with mobile-focused copy, for example).

<figure><a href="https://www.smashingmagazine.com/2012/02/27/ever-justification-for-responsive-text/"><img loading="lazy" decoding="async" class="125994" title="The website for Sifter App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f7fd53-9564-48cc-8465-1e8ffa54f70c/sifter1.jpg" alt="Website for Sifter App" /></a></figure>

Having looked at how this technique works, I wouldn’t endorse it yet, because its practical value is not clear. Also, describing this as “responsive” could legitimize what is possibly a less than optimal coding technique. Below are screenshots of how it works on the Sifter website:



[Read more...](https://www.smashingmagazine.com/2012/02/27/ever-justification-for-responsive-text/)