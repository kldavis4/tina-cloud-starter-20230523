---
title: 'Learning JavaScript: Essentials And Guidelines'
slug: learning-javascript-essentials-guidelines-tutorials
image: null
date: 2012-07-02T12:28:00.000Z
author: vitaly-friedman
description: >-
  This is a selection of most popular and useful Smashing Magazine’s articles on
  learning JavaScript and jQuery published over all the years here, on Smashing
  Magazine.
categories: []
---

This is a selection of most popular and useful Smashing Magazine's articles on learning JavaScript and jQuery published over all the years here, on Smashing Magazine.




#### Quick Overview



*   [My Favorite Programming Mistakes](#n1)
*   [Ten Oddities And Secrets About JavaScript](#n2)
*   [Seven JavaScript Things I Wish I Knew Much Earlier In My Career](#n3)
*   [The Seven Deadly Sins Of JavaScript Implementation](#n4)
*   [Find The Right JavaScript Solution With A 7-Step Test](#n5)
*   [What You Need To Know About JavaScript Scope](#n6)
*   [jQuery And JavaScript Coding: Examples And Best Practices](#n7)
*   [Image Manipulation With jQuery And PHP GD](#n8)
*   [jQuery Plugin Checklist: Should You Use That jQuery Plug-In?](#n9)
*   [Commonly Confused Bits Of jQuery](#n10)
*   [Make Your Own Bookmarklets With jQuery](#n11)
*   [Behind The Scenes Of Nike Better World](#n12)
*   [Five Useful Interactive CSS/jQuery Techniques Deconstructed](#n13)
*   [Five Useful CSS/jQuery Coding Techniques For More Dynamic Websites](#n14)
*   [10 Useful CSS/JS-Coding Solutions For Web-Developers](#n15)
*   [Useful HTML-, CSS- and JavaScript Tools And Libraries](#n16)
*   [50 Fresh JavaScript Tools That Will Improve Your Workflow](#n17)
*   [40 Useful jQuery Techniques And Plugins](#n18)
*   [45 Fresh Useful JavaScript And jQuery Techniques And Tools](#n19)
*   [50 Brilliant CSS3/JavaScript Coding Techniques](#n20)
*   [45 Powerful CSS/JavaScript-Techniques](#n21)
*   [Develop A One-Of-A-Kind CSS/JS-Based Game Portfolio](#n22)
*   [A Quick Look Into The Math Of Animations With JavaScript](#n23)
*   [Create An Animated Bar Graph With HTML, CSS And jQuery](#n24)
*   [Essential jQuery Plugin Patterns](#n25)
*   [Introduction To JavaScript Unit Testing](#n26)
*   [Analyzing Network Characteristics Using JavaScript And The DOM, Part 1](#n27)
*   [Lessons From A Review Of JavaScript Code](#n28)
*   [Optimizing Long Lists Of Yes/No Values With JavaScript](#n29)
*   [Searchable Dynamic Content With AJAX Crawling](#n30)

## [My Favorite Programming Mistakes](https://www.smashingmagazine.com/2011/07/07/my-favorite-programming-mistakes/ "Permanent Link to My Favorite Programming Mistakes")



Over my programming career, I have made a lot of mistakes in several different languages. In fact, if I write 10 or more lines of code and it works the first time, I'll get a bit suspicious and test it more rigorously than usual. I would expect to find a syntax error or a bad array reference or a misspelled variable or _something_.


<figure><a href="https://www.smashingmagazine.com/2011/07/07/my-favorite-programming-mistakes/"><img loading="lazy" decoding="async" class="106061" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58d54737-e035-4614-b5d6-ca0c6bca0105/spam-error.png" alt="My Favourite Programming Mistakes" width="542" height="315" /></a></figure>



I like to classify these mistakes into three broad groups: cock-ups (or screw-ups in American English), errors and oversights. A cock-up is when you stare blankly at the screen and whisper â€œOopsâ€: things like deleting a database or website, or overwriting three-days worth of work, or accidentally emailing 20,000 people. Errors cover everything, from simple syntax errors like forgetting a `}` to fatal errors and computational errors.



[Read more...](https://www.smashingmagazine.com/2011/07/07/my-favorite-programming-mistakes/7)



## [Ten Oddities And Secrets About JavaScript](https://www.smashingmagazine.com/2011/05/30/10-oddities-and-secrets-about-javascript/ "Permanent Link to Ten Oddities And Secrets About JavaScript")



JavaScript. At once bizarre and yet beautiful, it is surely the programming language that Pablo Picasso would have invented. Null is apparently an object, an empty array is apparently equal to false, and functions are bandied around as though they were tennis balls.


<figure><a href="https://www.smashingmagazine.com/2011/05/30/10-oddities-and-secrets-about-javascript/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0910d78-a774-4b2e-988e-50fb3f416dcb/js.jpg" alt="Ten Oddities And Secrets About JavaScript" width="441" height="206" /></a></figure>

This article is aimed at intermediate developers who are curious about more advanced JavaScript. It is a collection of JavaScript's oddities and well-kept secrets. Some sections will hopefully give you insight into how these curiosities can be useful to your code, while other sections are pure WTF material. So, let's get started.



[Read more...](https://www.smashingmagazine.com/2011/05/30/10-oddities-and-secrets-about-javascript/4)




## [Seven JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/20/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/ "Permanent Link to Seven JavaScript Things I Wish I Knew Much Earlier In My Career")



I've been writing JavaScript code for much longer than I care to remember. I am very excited about the language's recent success; it's good to be a part of that success story. I've written dozens of articles, book chapters and one full book on the matter, and yet I keep finding new things. Here are some of the "aha!" moments I've had in the past, which you can try out rather than waiting for them to come to you by chance.


<figure><a href="https://www.smashingmagazine.com/2010/04/20/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65ca36c3-6e4e-4dc7-a0e6-f5c59fe451a2/javascript-code-snippet.gif" alt="Screenshot" width="500" height="361" /></a></figure>



_Shortcut notations_. One of the things I love most about JavaScript now is shortcut notations to generate objects and arrays. So, in the past when we wanted to create an object, we wrote...



[Read more...](https://www.smashingmagazine.com/2010/04/20/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)





## [The Seven Deadly Sins Of JavaScript Implementation](https://www.smashingmagazine.com/2010/02/22/the-seven-deadly-sins-of-javascript-implementation/ "Permanent Link to The Seven Deadly Sins Of JavaScript Implementation")



Using JavaScript has become increasingly easy over the last few years. Whereas back in the day we needed to know the quirks of every browser, now many libraries such as jQuery, YUI, Dojo and MooTools allow someone who doesn't even know JavaScript to spruce up boring HTML documents with impressive and shiny effects. By piggy-backing on the CSS selector engine, we have moved away from the complexity and inconsistencies of the DOM and made things much easier.


<figure><a href="https://www.smashingmagazine.com/2010/02/22/the-seven-deadly-sins-of-javascript-implementation/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/905a3258-9b66-454e-8fad-c7fcd4a6bac3/javascript.jpg" alt="The Seven Deadly Sins Of JavaScript Implementation" width="452" height="204" /></a></figure>



If you look at some of the code that has been released, though, we do seem to have taken a step backwards. In gaining easier access, we also became a bit sloppy with our code. Finding clearly structured, easy-to-maintain jQuery code is quite tough, which is why many plug-ins do the same thing. Writing one yourself is faster than trying to fathom what other developers have done.



The **rules for solid, maintainable and secure JavaScript** haven't changed, though. So, let's run through the seven sins of JavaScript development that will bite you in the backside when you have to maintain the code later on or hand it over to another party.



[Read more...](https://www.smashingmagazine.com/2010/02/22/the-seven-deadly-sins-of-javascript-implementation/)





## [Find The Right JavaScript Solution With A 7-Step Test](https://www.smashingmagazine.com/2010/01/21/find-the-right-javascript-solution-with-a-7-step-test/ "Permanent Link to Find The Right JavaScript Solution With A 7-Step Test")



As Web developers and designers, we are spoilt for choice right now. To build a complex Web application or even just spice up a website with some highly interactive interface element, we have hundreds of pre-built solutions to choose from. Every library comes with widgets and solutions, and every developer tries to make a name for him or herself by releasing a funky JavaScript solution to a certain interface problem. We can pick from dozens of menus, image carousels, tabs, form validators and "lightboxes."


<figure><a href="https://www.smashingmagazine.com/2010/01/21/find-the-right-javascript-solution-with-a-7-step-test/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c46f9eb-6442-43ac-9f40-1534e653ea73/litmus-disable-javascript.jpg" alt="Disable JavaScript with the web developer toolbar" width="400" height="333" /></a></figure>



Having this much choice makes it easy for us to pick and choose, which is where things go wrong. In most cases, we measure the quality of a solution by its convenience to us. Our main reasons for picking one solution over another are: Does it do what I need it to do? Does it look cool? Does it sound easy to use? Would I want to use it? Does it use the framework I'm committed to?



[Read more...](https://www.smashingmagazine.com/2010/01/21/find-the-right-javascript-solution-with-a-7-step-test/)





## [What You Need To Know About JavaScript Scope](https://www.smashingmagazine.com/2009/08/01/what-you-need-to-know-about-javascript-scope/ "Permanent Link to What You Need To Know About JavaScript Scope")



Understanding scope in programming is key to appreciating how your variables interact with the rest of your code. In some languages, this can be quite straightforward, but JavaScript's anonymous functions and event handling features, along with a couple of little quirks, mean that handling scope in your applications can become frustrating.


<figure><a href="https://www.smashingmagazine.com/2009/08/01/what-you-need-to-know-about-javascript-scope/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e6a4b99-0031-4827-999b-933247001387/js.jpg" alt="JavaScript Scope" width="502" height="335" /></a></figure>



This article discusses how JavaScript handles scope and how various JavaScript libraries provide methods for dealing with it and how they smooth out a few bumps. We'll also look at how you can get back to basics and do some interesting scope wrangling without a library, a useful approach if you're writing code that needs to stand alone.



[Read more...](https://www.smashingmagazine.com/2009/08/01/what-you-need-to-know-about-javascript-scope//#more-8893)





## [jQuery And JavaScript Coding: Examples And Best Practices](https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/ "Permanent Link to jQuery and JavaScript Coding: Examples and Best Practices")



When used correctly, [jQuery](https://jquery.com/) can help you make your website more interactive, interesting and exciting. This article will share some best practices and examples for using the popular Javascript framework to create unobtrusive, accessible DOM scripting effects.


<figure><a href="https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c5466a0-622a-444e-b0fd-e17b27e4d723/jquery.jpg" alt="jQuery" width="500" height="351" /></a></figure>



The article will explore what constitutes best practices with regard to Javascript and, furthermore, why jQuery is a good choice of a framework to implement best practices.



[Read more...](https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices//#more-719)





## [Image Manipulation With jQuery And PHP GD](https://www.smashingmagazine.com/2011/04/05/image-manipulation-with-jquery-and-php-gd/ "Permanent Link to Image Manipulation With jQuery and PHP GD")



One of the numerous advantages brought about by the explosion of jQuery and other JavaScript libraries is the ease with which you can create interactive tools for your site. When combined with server-side technologies such as PHP, this puts a serious amount of power at your finger tips.


<figure><a href="https://www.smashingmagazine.com/2011/04/05/image-manipulation-with-jquery-and-php-gd/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdad1820-9e92-4284-9a81-a74d902c4a11/uploaded-image.gif" alt="Image Manipulation With jQuery and PHP GD" width="500" height="271" /></a></figure>



In this article, I'll be looking at how to combine JavaScript/jQuery with PHP and, particularly, PHP's GD library to create an image manipulation tool to upload an image, then crop it and finally save the revised version to the server. Sure, there are plugins out there that you can use to do this; but this article aims to show you what's behind the process. You can [download the source files](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99e2aff8-9705-46e2-8cfe-9d417db37476/sm-image-manipulation.zip) for reference.



[Read more...](https://www.smashingmagazine.com/2011/04/05/image-manipulation-with-jquery-and-php-gd/)





## [jQuery Plugin Checklist: Should You Use That jQuery Plug-In?](https://www.smashingmagazine.com/2010/08/26/jquery-plugin-checklist-should-you-use-that-jquery-plug-in/ "Permanent Link to jQuery Plugin Checklist: Should You Use That jQuery Plug-In?")



jQuery plug-ins provide an excellent way to save time and streamline development, allowing programmers to avoid having to build every component from scratch. But plug-ins are also a wild card that introduce an element of uncertainty into any code base. A good plug-in saves countless development hours; a bad plug-in leads to bug fixes that take longer than actually building the component from scratch.


<figure><a href="https://www.smashingmagazine.com/2010/08/26/jquery-plugin-checklist-should-you-use-that-jquery-plug-in"><img class="aligncenter size-full wp-image-57094" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e9bf8c1-9b98-4485-a8ea-a86698158cd5/jquery21.gif" alt="jQuery logo" width="439" height="127" /></a></figure>



Fortunately, one usually has a number of different plug-ins to choose from. But even if you have only one, figure out whether it's worth using at all. The last thing you want to do is introduce bad code into your code base. The first step is to figure out whether you even need a plug-in. If you don't, you'll save yourself both file size and time.



[Read more...](https://www.smashingmagazine.com/2010/08/26/jquery-plugin-checklist-should-you-use-that-jquery-plug-in/)




## [Commonly Confused Bits Of jQuery](https://www.smashingmagazine.com/2010/08/04/commonly-confused-bits-of-jquery/ "Permanent Link to Commonly Confused Bits Of jQuery")



The explosion of JavaScript libraries and frameworks such as **jQuery** onto the front-end development scene has opened up the power of JavaScript to a far wider audience than ever before. It was born of the need  —  expressed by a crescendo of screaming by front-end developers who were fast running out of hair to pull out  —  to improve JavaScript's somewhat primitive API, to make up for the lack of unified implementation across browsers and to make it more compact in its syntax.


<figure><a href="https://www.smashingmagazine.com/2010/08/04/commonly-confused-bits-of-jquery/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24f50c0a-d7af-4945-8317-ebf79833aa84/jquery.png" alt="Screenshot" width="474" height="242" /></a></figure>



All of which means that, unless you have some odd grudge against jQuery, those days are gone  —  you can actually get stuff done now. A script to find all links of a certain CSS class in a document and bind an event to them now requires one line of code, not 10\. To power this, jQuery brings to the party its own API, featuring a host of functions, methods and syntactical peculiarities. Some are confused or appear similar to each other but actually differ in some way. **This article clears up some of these confusions**.



[Read more...](https://www.smashingmagazine.com/2010/08/04/commonly-confused-bits-of-jquery/)





## [Make Your Own Bookmarklets With jQuery](https://www.smashingmagazine.com/2010/05/23/make-your-own-bookmarklets-with-jquery/ "Permanent Link to Make Your Own Bookmarklets With jQuery")



**Bookmarklets** are small JavaScript-powered applications in link form. Often "one-click" tools and functions, they're typically used to extend the functionality of the browser and to interact with Web services. They can do things like post to your WordPress or Tumblr blog, submit any selected text to Google Search, or modify a current page's CSS... and _many_ other things!


<figure><a href="https://www.smashingmagazine.com/2010/05/23/make-your-own-bookmarklets-with-jquery/"><img class="37608" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e4d2fb-b30e-4a4b-a76a-ddcb6df0ab7b/makeyourownbookmarklets.jpg" alt="Make Your Own Bookmarklets with jQuery" width="500" height="333" /></a></figure>



Because they run on JavaScript (a client-side programming language), bookmarklets (sometimes called "favelets") are supported by all major browsers on all platforms, without any additional plug-ins or software needed. In most instances, the user can just drag the bookmarklet link to their toolbar, and that's it!



In this article, we'll go through how to **make your own** bookmarklets, using the [jQuery](https://jquery.com/) JavaScript framework.



[Read more...](https://www.smashingmagazine.com/2010/05/23/make-your-own-bookmarklets-with-jquery/)





## [Behind The Scenes Of Nike Better World](https://www.smashingmagazine.com/2011/07/12/behind-the-scenes-of-nike-better-world/ "Permanent Link to Behind The Scenes Of Nike Better World")



Perhaps one of the most talked about websites in the last 12 months has been Nike Better World. It's been featured in countless Web design galleries, and it still stands as an example of what a great idea and some clever design and development techniques can produce.


<figure><a href="https://www.smashingmagazine.com/2011/07/12/behind-the-scenes-of-nike-better-world/"><img class="aligncenter size-full wp-image-106650" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/117aa0d2-1553-4115-bc6f-048e17f5e6c2/parallax-sketch.png" alt="screenshot" width="550" height="374" /></a></figure>



In this article, **we'll talk to the team behind Nike Better World** to find out how the website was made. We'll look at exactly how it was put together, and then use similar techniques to create our own parallax scrolling website. Finally, we'll look at other websites that employ this technique to hopefully inspire you to build on these ideas and create your own variation.



[Read more...](https://www.smashingmagazine.com/2011/07/12/behind-the-scenes-of-nike-better-world/2)





## [Five Useful Interactive CSS/jQuery Techniques Deconstructed](https://www.smashingmagazine.com/2011/06/16/five-useful-interactive-css-jquery-techniques-deconstruted/ "Permanent Link to Five Useful Interactive CSS/jQuery Techniques Deconstructed")



With the wide variety of CSS3 and JavaScript techniques available today, it's easier than ever to create unique interactive websites that delight visitors and provide a more engaging user experience. In this article, we'll walk through five interactive techniques that you can start using right now. We'll cover animated text effects, animated images without GIFs, mega drop-down menus, fancy slideshow navigation and animated icons for the hover state of buttons.


<figure><a href="https://www.smashingmagazine.com/2011/06/16/five-useful-interactive-css-jquery-techniques-deconstruted/"><img loading="lazy" decoding="async" class="104010" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0a794a7-632e-46da-bb00-adf0b3221ab4/screenshot-frontpage1.jpeg" alt="Five Useful Interactive CSS/jQuery Techniques Deconstruted" width="498" height="392" /></a></figure>



Besides learning how to accomplish these specific tasks, you'll also master a variety of **useful CSS and jQuery tricks** that you can leverage when creating your own interactive techniques. The solutions presented here are certainly not perfect, so any thoughts, ideas and suggestions on how you would solve these design problems would be very appreciated.



[Read more...](https://www.smashingmagazine.com/2011/06/16/five-useful-interactive-css-jquery-techniques-deconstruted/5)





## [Five Useful CSS/jQuery Coding Techniques For More Dynamic Websites](https://www.smashingmagazine.com/2010/09/21/5-coding-techniques-for-more-dynamic-websites/ "Permanent Link to Five Useful CSS/jQuery Coding Techniques For More Dynamic Websites")



Interactivity can transform a dull static website into a dynamic tool that not only delights users but conveys information more effectively. In this post, we'll walk through five different coding techniques that can be easily implemented on any website to provide a richer user experience. These techniques will allow you to better display difficult content, help users find information more effectively and provide meaningful UI cues without overwhelming the user: on-page text search, drag controls for oversized content, subtle hover effects, comment count bars and a full-page slider.


<figure><a href="https://www.smashingmagazine.com/2010/09/21/5-coding-techniques-for-more-dynamic-websites/"><img loading="lazy" decoding="async" class="61294" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcc29c8b-50fb-4db5-8c94-b10b0c73c847/moscow.jpg" alt="Drag controls for oversized content" width="500" height="432" /></a></figure>



Websites often have search boxes to allow users to find content from their archives. But what if you want to find content on the given page? Information Architects <del>has</del> had on-page text search that provides a great user experience. Let's recreate this using jQuery.



[Read more...](https://www.smashingmagazine.com/2011/06/16/five-useful-interactive-css-jquery-techniques-deconstruted/5)





## [10 Useful CSS/JS-Coding Solutions For Web-Developers](https://www.smashingmagazine.com/2009/07/06/10-useful-cssjs-coding-solutions-for-web-developers/ "Permanent Link to 10 Useful CSS/JS-Coding Solutions For Web-Developers")



Often creative and truly **remarkable design solutions** remain unknown because we, designers, simply overlook them. Being busy with our own projects, we sometimes try to grasp the intuition behind (probably) complex and cluttered code of other designers to understand how they manage to implement particular design ideas. In fact, by just observing the code of other developers we can learn a lot from them; we can find interesting ideas and improve the quality of our work.


<figure><a href="https://www.smashingmagazine.com/2009/07/06/10-useful-cssjs-coding-solutions-for-web-developers/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb0b938d-f00e-46a0-9b21-2cb75e7a2b5b/blt.gif" alt="Typographic Percentages" width="520" height="330" /></a></figure>



Over the last months we've been paying closer attention to interesting design techniques and coding solutions and tried to understand how each of these solutions work and how they can benefit other designers and developers. Such designs are often hard to find, so it would be great if you could suggest some solutions that are worth exploring in detail â€“ we'll certainly cover them in our next posts!



So let's take a closer look at **10 useful CSS & Javascript techniques and coding solutions** that can turn out to be useful for your next project. You should have at least a basic knowledge of CSS and JavaScript before you read the entire article.



[Read more...](https://www.smashingmagazine.com/2009/07/06/10-useful-cssjs-coding-solutions-for-web-developers//#more-8256)





### JavaScript And jQuery Tools



## [Useful HTML-, CSS- and JavaScript Tools and Libraries](https://www.smashingmagazine.com/2011/06/10/useful-html-css-and-javascript-tools-and-libraries/ "Permanent Link to Useful HTML-, CSS- And JavaScript Tools And Libraries")



Front-end development is a tricky beast. It's not difficult to learn, but it's quite difficult to master. There are just too many things that need to be considered; too many tweaks that might be necessary here and there; too many details to make everything just right. Luckily, developers and designers out there keep releasing useful tools and resources for all of us to learn, improve our skills and just get better at what we do.


<figure><a href="https://www.smashingmagazine.com/2011/06/10/useful-html-css-and-javascript-tools-and-libraries/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/049bb861-d254-4922-b8fc-a921e2182002/useful-resources-189.jpg" alt="Flexible Font Sizes with jQuery" width="500" height="300" /></a></figure>



Here at Smashing Magazine, we're continuously searching for **time-saving, useful HTML-, CSS- and JavaScript-resources** for our readers, to make the search of these ever-growing tools easier. We hope that these tools will help you improve your skills as well as your professional workflow. A sincere thanks to all designers and developers who are featured in this round-up. We respect and appreciate your contributions to the design community.



[Read more...](https://www.smashingmagazine.com/2011/06/10/useful-html-css-and-javascript-tools-and-libraries/8)





## [50 Fresh JavaScript Tools That Will Improve Your Workflow](https://www.smashingmagazine.com/2009/06/21/50-fresh-javascript-tools-that-will-improve-your-workflow/ "Permanent Link to 50 Fresh JavaScript Tools That Will Improve Your Workflow")



**JavaScript** is an integral part of the RIA revolution. JavaScript allows developers to create rich and interactive web interfaces and establish asynchronous communication with servers for constantly up-to-date data without a page refresh.



Many things that were once accomplished using Flash objects can now be built using JavaScript - with the added benefit that it is free, typically more web and mobile accessible under most circumstances using best practices for development techniques, and without the need to use proprietary software for development.


<figure><a href="https://www.smashingmagazine.com/2009/06/21/50-fresh-javascript-tools-that-will-improve-your-workflow/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/148fc31a-9f40-4dd1-91c8-c3cf1fc9408a/unit.gif" alt="FireUnit" width="488" height="467" /></a></figure>



Though JavaScript has been around for a while, new tools, techniques, and information are constantly being pumped out to continually push the technology into greater heights. In this article, we wish to share with you a **huge list of fresh and new tools and resources** that JavaScript developers will find useful and informative.



[Read more...](https://www.smashingmagazine.com/2009/06/21/50-fresh-javascript-tools-that-will-improve-your-workflow//#more-7938)




## [40 Useful jQuery Techniques And Plugins](https://www.smashingmagazine.com/2010/04/27/45-useful-jquery-techniques-and-plugins/ "Permanent Link to 40 Useful jQuery Techniques and Plugins")



Over the last year, Smashing Magazine has evolved. We've been publishing fewer lists and more in-depth articles about design and Web development. We have invited professionals and high-profile developers to write for us. We've been investing more resources in the quality and relevance of our articles. We've also explored new formats; and on weekends we've been publishing more inspirational pieces, leaving the in-depth articles to weekdays.


<figure><a href="https://www.smashingmagazine.com/2010/04/27/45-useful-jquery-techniques-and-plugins/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d086349-cd6d-421c-8154-70d5f98449db/js-00.jpg" alt="TipTip jQuery Plugin" width="480" height="300" /></a></figure>

We've tried our best to fuel the growing appetite of our readers for more advanced articles, but recently we've been receiving more requests for carefully selected, useful round-ups. We are not big fans of lists either, but the format is useful and  —  if the resources are relevant  —  can be extremely helpful. Therefore, we've decided to add a couple of round-ups per month as a bonus to our regular articles. Instead of replacing the main articles, we will add round-ups on top of our regular schedule. If you don't like round-ups or find them inappropriate, please feel free to skip them. How does this work for you?



In this post, we present **40 useful but obscure jQuery plug-ins** that will hopefully help you improve the user experience on your websites. We look forward to your ideas and suggestions in the comments to this post.



[Read more...](https://www.smashingmagazine.com/2010/04/27/45-useful-jquery-techniques-and-plugins/)




## [45 Fresh Useful JavaScript And jQuery Techniques And Tools](https://www.smashingmagazine.com/2010/03/12/45-fresh-useful-javascript-and-jquery-techniques-and-tools/ "Permanent Link to 45 Fresh Useful JavaScript and jQuery Techniques and Tools")



Yes, this is another round-up of **fresh and useful Javascript techniques, tools and resources**. But don't close the tab yet, as you might find this one very useful. In this selection we present calendars, forms, buttons, navigation, debugging, optimization and compatibility tables as well as handy resources and tools. We also cover various jQuery-plugins that will help you extend the functionality of your website and improve user experience with ready components or coding solutions.


<figure><a href="https://www.smashingmagazine.com/2010/03/12/45-fresh-useful-javascript-and-jquery-techniques-and-tools/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed40117c-d43e-4795-9abf-314c5a9c3623/javascript-techniques-82.jpg" alt="jDigiClock - Digital Clock (HTC Hero inspired)" width="480" height="300" /></a></figure>



The last section also covers a number of useful educational resources such as a compilation of useful JavaScript coding practices, a detailed comparison of JavaScript frameworks and general JavaScript programming conventions. We are looking forward to your feedback.



[Read more...](https://www.smashingmagazine.com/2010/03/12/45-fresh-useful-javascript-and-jquery-techniques-and-tools/)



## [50 Brilliant CSS3/JavaScript Coding Techniques](https://www.smashingmagazine.com/2010/02/01/50-brilliant-css3-javascript-coding-techniques/ "Permanent Link to 50 Brilliant CSS3/JavaScript Coding Techniques")



**CSS3 is coming**. Although the browser support of CSS 3 is [still very limited](https://www.findmebyip.com/litmus/), many designers across the globe experiment with new powerful features of the language, using graceful degradation for users with older browsers and using the new possibilites of CSS3 for users with modern browsers. That's a reasonable solution  —  after all it doesn't make sense to avoid learning CSS3 (that will be heavily used in the future) only because these features are not supported yet. The point of this article is to give you a glimpse of what will be possible soon and what you will be using soon and provide you with an opportunity to learn about new CSS3 techniques and features.


<figure><a href="https://www.smashingmagazine.com/2010/02/01/50-brilliant-css3-javascript-coding-techniques/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab7aa69-d7cb-4c3e-904e-fbc93ef04535/css3-last-08.jpg" alt="CSS3" width="481" height="300" /></a></figure>



In this post we present **50 useful and powerful CSS3/jQuery-techniques** that can strongly improve user experience, improve designer's workflow and replace dirty old workarounds that we used in Internet Explorer 6 & Co. Please notice that most techniques presented below are experimental, and many of them are not pure CSS3-techniques as they use jQuery or other JavaScript-library.



[Read more...](https://www.smashingmagazine.com/2010/02/01/50-brilliant-css3-javascript-coding-techniques/)




## [45 Powerful CSS/JavaScript-Techniques](https://www.smashingmagazine.com/2010/01/12/45-powerful-css-javascript-techniques/ "Permanent Link to 45 Powerful CSS/JavaScript-Techniques")



**CSS and JavaScript** are extremely powerful tools for designers and developers. However, sometimes it's difficult to come up with the one excellent idea that would solve a problem that you are facing right now. Good news: almost every day designers and developers come up with fresh and clever CSS tricks and techniques and share them with other developers online. We regularly collect all these tricks, filter them, sort them, revise them and prepare them for Smashing Magazine readers.


<figure><a href="https://www.smashingmagazine.com/2010/01/12/45-powerful-css-javascript-techniques/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/984fdbe1-12b6-4501-a623-7cecc6a5e611/annotation.jpg" alt=" Building the New Visual Annotations" width="480" height="300" /></a></figure>

In this post we present **45 useful CSS/JavaScript-techniques** that may help you find clever solutions to some of your problems or just get inspired by what is possible with CSS. We cover interesting CSS-techniques, navigation menus, CSS typography, CSS lists and CSS buttons. The focus of this post lies on CSS; please notice that some of the techniques use JavaScript or PHP for enhanced functionality.



Please notice that this is the first part of our large round-up of fresh CSS/JavaScript-techniques. Other techniques (CSS tables, CSS layouts, CSS for Mobile and CSS forms) will be featured in an upcoming article. So don't forget to [subscribe to our RSS-feed](https://rss1.smashingmagazine.com/feed/) and [follow us on Twitter](https://twitter.com/smashingmag) for similar articles and a stream of useful resources. Please also let us know what we should change or improve in our future posts!



[Read more...](https://www.smashingmagazine.com/2010/01/12/45-powerful-css-javascript-techniques/)

## [Develop A One-Of-A-Kind CSS/JS-Based Game Portfolio](https://www.smashingmagazine.com/2012/05/28/develop-a-one-of-a-kind-cssjs-based-game-portfolio/ "Permanent Link to Develop A One-Of-A-Kind CSS/JS-Based Game Portfolio")



A portfolio is a must-have for any designer or developer who wants to stake their claim on the Web. It should be as unique as possible, and with a bit of HTML, CSS and JavaScript, you could have a one-of-a-kind portfolio that capably represents you to potential clients. In this article, I’ll show you how I created my 2-D Web-based game portfolio.

<figure><a href="https://www.smashingmagazine.com/2012/05/28/develop-a-one-of-a-kind-cssjs-based-game-portfolio/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4de27900-6ef5-46a0-9dc1-cbb0faddbc49/1.png" alt="Daniel Sternlicht Portfolio." /></a></figure>

Before getting down to business, let’s talk about portfolios.

A portfolio is a great tool for Web designers and developers to show off their skills. As with any project, spend some time learning to develop a portfolio and doing a little research on what’s going on in the Web design industry, so that the portfolio presents you as an up to date, innovative and inspiring person. All the while, keep in mind that going with the flow isn’t necessarily the best way to stand out from the crowd.

One last thing before we dive into the mystery of my Web-based game portfolio. I use jQuery which has made my life much easier by speeding up development and keeping my code clean and simple.

[Read more...](https://www.smashingmagazine.com/2012/05/28/develop-a-one-of-a-kind-cssjs-based-game-portfolio/)

## [A Quick Look Into The Math Of Animations With JavaScript](https://www.smashingmagazine.com/2011/10/04/quick-look-math-animations-javascript/ "Permanent Link to A Quick Look Into The Math Of Animations With JavaScript")



In school, I hated math. It was a dire, dry and boring thing with stuffy old books and very theoretical problems. Even worse, a lot of the tasks were repetitive, with a simple logical change in every iteration (dividing numbers by hand, differentials, etc.). It was exactly the reason why we invented computers. Suffice it to say, a lot of my math homework was actually done by my trusty Commodore 64 and some lines of Basic, with me just copying the results later on.

These tools and the few geometry lessons I had gave me the time and inspiration to make math interesting for myself. I did this first and foremost by creating visual effects that followed mathematical rules in demos, intros and other seemingly pointless things.

<figure><a href="https://www.smashingmagazine.com/2011/10/04/quick-look-math-animations-javascript/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b39fe442-f795-482f-bedb-64b1f7533f3f/forloop.png" alt="45 degree graph, a result of a simple for loop" /></a></figure>

There is a lot of math in the visual things we do, even if we don’t realize it. If you want to make something look natural and move naturally, you need to add a bit of physics and rounding to it. Nature doesn’t work in right angles or linear acceleration. This is why zombies in movies are so creepy. This was [covered here before in relation to CSS animation](https://www.smashingmagazine.com/2011/09/14/the-guide-to-css-animation-principles-and-examples/), but today let’s go a bit deeper and look at the simple math behind the smooth looks.

[Read more...](https://www.smashingmagazine.com/2011/10/04/quick-look-math-animations-javascript/)

## [Create An Animated Bar Graph With HTML, CSS And jQuery](https://www.smashingmagazine.com/2011/09/23/create-an-animated-bar-graph-with-html-css-and-jquery/ "Permanent Link to Create An Animated Bar Graph With HTML, CSS And jQuery")



People in boardrooms across the world love a good graph. They go nuts for PowerPoint, bullet points and phrases like “run it up the flagpole,” “blue-sky thinking” and “low-hanging fruit,” and everything is always “moving forward.” Backwards is not an option for people who [facilitate paradigm shifts in the zeitgeist](https://startupista.com/corporate-bullshit-generator/). Graphs of financial projections, quarterly sales figures and market saturation are a middle-manager’s dream.

<figure><a href="https://www.smashingmagazine.com/2011/09/23/create-an-animated-bar-graph-with-html-css-and-jquery/"><img loading="lazy" decoding="async" class="106433" title="Creating an Animated Bar Graph with HTML, CSS &amp; jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a8dd25-425f-4c1d-9fd0-41a3cb23cc2b/graph-tut-image-header.jpg" alt="screenshot" /></a></figure>

How can we as Web designers get in on all of this hot graph action? There are actually quite a few ways to display graphs on the Web. We could simply create an image and nail it to a Web page. But that’s not very accessible or interesting. We could use Flash, which is quite good for displaying graphs?—?but again, not very accessible. Besides, designers, developers and [deities](https://www.apple.com/hotnews/thoughts-on-flash/) are falling out of love with Flash. Technologies such as HTML5 can do many of the same things without the need for a plug-in. The new HTML5 `<canvas>` element could even be adapted to the task. Plenty of charting tools are online that we might use. But what if we wanted something a little more tailored?

There are pros and cons to the wide range of resources available to us, but this tutorial will not explore them all. Instead, we’ll create our graph using a [progressively enhanced](https://www.smashingmagazine.com/2009/04/22/progressive-enhancement-what-it-is-and-how-to-use-it/) sprinkling of CSS3 and jQuery. Because we can.

[Read more...](https://www.smashingmagazine.com/2011/09/23/create-an-animated-bar-graph-with-html-css-and-jquery/)

## [Essential jQuery Plugin Patterns](https://www.smashingmagazine.com/2011/10/11/essential-jquery-plugin-patterns/ "Permanent Link to Essential jQuery Plugin Patterns")



I occasionally write about implementing [design patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/) in JavaScript. They’re an excellent way of building upon proven approaches to solving common development problems, and I think there’s a lot of benefit to using them. But while well-known JavaScript patterns are useful, another side of development could benefit from its own set of design patterns: jQuery plugins. The official jQuery [plugin authoring guide](https://docs.jquery.com/Plugins/Authoring) offers a great starting point for getting into writing plugins and widgets, but let’s take it further.

Plugin development has evolved over the past few years. We no longer have just one way to write plugins, but many. In reality, certain patterns might work better for a particular problem or component than others.

Some developers may wish to use the jQuery UI [widget factory](https://ajpiano.com/widgetfactory/); it’s great for complex, flexible UI components. Some may not. Some might like to structure their plugins more like modules (similar to the module pattern) or use a more formal module format such as [AMD (asynchronous module definition)](https://github.com/amdjs/amdjs-api/wiki/AMD). Some might want their plugins to harness the power of prototypal inheritance. Some might want to use custom events or pub/sub to communicate from plugins to the rest of their app. And so on.

I began to think about plugin patterns after noticing a number of efforts to create a one-size-fits-all jQuery plugin boilerplate. While such a boilerplate is a great idea in theory, the reality is that we rarely write plugins in one fixed way, using a single pattern all the time.

Let’s assume that you’ve tried your hand at writing your own jQuery plugins at some point and you’re comfortable putting together something that works. It’s functional. It does what it needs to do, but perhaps you feel it could be structured better. Maybe it could be more flexible or could solve more issues. If this sounds familiar and you aren’t sure of the differences between many of the different jQuery plugin patterns, then you might find what I have to say helpful.

My advice won’t provide solutions to every possible pattern, but it will cover popular patterns that developers use in the wild.

[Read more...](https://www.smashingmagazine.com/2011/10/11/essential-jquery-plugin-patterns/)

## [Introduction To JavaScript Unit Testing](https://www.smashingmagazine.com/2012/06/27/introduction-to-javascript-unit-testing/ "Permanent Link to Introduction To JavaScript Unit Testing")



You probably know that testing is good, but the first hurdle to overcome when trying to write unit tests for client-side code is the lack of any actual units; JavaScript code is written for each page of a website or each module of an application and is closely intermixed with back-end logic and related HTML. In the worst case, the code is completely mixed with HTML, as inline events handlers.

This is likely the case when no JavaScript library for some DOM abstraction is being used; writing inline event handlers is much easier than using the DOM APIs to bind those events. More and more developers are picking up a library such as jQuery to handle the DOM abstraction, allowing them to move those inline events to distinct scripts, either on the same page or even in a separate JavaScript file. However, putting the code into separate files doesn’t mean that it is ready to be tested as a unit.

<figure><a href="https://www.smashingmagazine.com/2012/06/27/introduction-to-javascript-unit-testing/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62de4cec-cfdc-4cc3-8cb1-2e4603345705/4b-red.png" alt="" title="4b-red" loading="lazy" decoding="async" class="118915" /></a></figure>

What is a unit anyway? In the best case, it is a pure function that you can deal with in some way — a function that always gives you the same result for a given input. This makes unit testing pretty easy, but most of the time you need to deal with side effects, which here means DOM manipulations. It’s still useful to figure out which units we can structure our code into and to build unit tests accordingly.

[Read more...](https://www.smashingmagazine.com/2012/06/27/introduction-to-javascript-unit-testing/)

## [Analyzing Network Characteristics Using JavaScript And The DOM, Part 1](https://www.smashingmagazine.com/2011/11/14/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/ "Permanent Link to Analyzing Network Characteristics Using JavaScript And The DOM, Part 1")



As Web developers, we have an affinity for developing with JavaScript. Whatever the language used in the back end, JavaScript and the browser are the primary language-platform combination available at the user’s end. It has many uses, ranging from silly to experience-enhancing.

<figure><a href="https://www.smashingmagazine.com/2011/11/14/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/"></a></figure>

In this article, we’ll look at some methods of manipulating JavaScript to determine various network characteristics from within the browser — characteristics that were previously available only to applications that directly interface with the operating system. Much of this was discovered while building the [Boomerang](https://github.com/bluesmoon/boomerang) project to measure real user performance.

[Read more...](https://www.smashingmagazine.com/2011/11/14/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/)

## [Lessons From A Review Of JavaScript Code](https://www.smashingmagazine.com/2011/10/27/lessons-from-a-review-of-javascript-code/ "Permanent Link to Lessons From A Review Of JavaScript Code")



Before we start, I’d like to pose a question: when was the last time you asked someone to review your code? Reviewing code is possibly the single best technique to improve the overall quality of your solutions, and if you’re not actively taking advantage of it, then you’re missing out on identifying bugs and hearing suggestions that could make your code better.

None of us write 100% bug-free code all of the time, so don’t feel there’s a stigma attached to seeking help. Some of the most experienced developers in our industry, from framework authors to browser developers, regularly request reviews of their code from others; asking whether something could be tweaked should in no way be considered embarrassing. Reviews are a technique like any other and should be used where possible.

<figure><a href="https://www.smashingmagazine.com/2011/10/27/lessons-from-a-review-of-javascript-code/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0174f16b-fe31-41c8-bba1-824291fd6d99/exhaustion.jpg" /></a></figure>

Today we’ll look at _where_ to get your code reviewed, _how_ to structure your requests, and _what_ reviewers look for. I was recently asked to review some code for a new JavaScript application, and thought I’d like to share some of my feedback, because it covers some JavaScript fundamentals that are always useful to bear in mind.

[Read more...](https://www.smashingmagazine.com/2011/10/27/lessons-from-a-review-of-javascript-code/)

## [Optimizing Long Lists Of Yes/No Values With JavaScript](https://www.smashingmagazine.com/2011/10/19/optimizing-long-lists-of-yesno-values-with-javascript/ "Permanent Link to Optimizing Long Lists Of Yes/No Values With JavaScript")



Very frequently in Web development (and programming in general), you need to store a long list of boolean values (yes/no, true/false, checked/unchecked… you get the idea) into something that accepts only strings. Maybe it’s because you want to store them in `localStorage` or in a cookie, or send them through the body of an HTTP request. I’ve needed to do this countless times.

The last time I stumbled on such a case wasn’t with my own code. It was when Christian Heilmann showed me his then new slide deck, with a cool feature where you could toggle the visibility of individual slides in and out of the presentation. On seeing it, I was impressed. Looking more closely, though, I realized that the checkbox states did not persist after the page reloaded. So, someone could spend a long time carefully tweaking their slides, only to accidentally hit F5 or crash their browser, and then?—?boom!?—?all their work would be lost. Christian told me that he was already working on storing the checkbox states in `localStorage`. Then, naturally, we endlessly debated the storage format. That debate inspired me to write this article, to explore the various approaches in depth.

[Read more...](https://www.smashingmagazine.com/2011/10/19/optimizing-long-lists-of-yesno-values-with-javascript/)

## [Searchable Dynamic Content With AJAX Crawling](https://www.smashingmagazine.com/2011/09/27/searchable-dynamic-content-with-ajax-crawling/ "Permanent Link to Searchable Dynamic Content With AJAX Crawling")



Google Search likes simple, easy-to-crawl websites. You like dynamic websites that show off your work and that really pop. But search engines can’t run your JavaScript. That cool AJAX routine that loads your content is hurting your SEO.

<figure><a href="https://www.smashingmagazine.com/2011/09/27/searchable-dynamic-content-with-ajax-crawling/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea75c388-0c4e-423a-a4ff-fdf8a170669a/crawlerserverdiagram-front-page1.jpg" alt="screenshot" /></a></figure>

Google’s robots parse HTML with ease; they can pull apart Word documents, PDFs and even images from the far corners of your website. But as far as they’re concerned, AJAX content is invisible.

[Read more...](https://www.smashingmagazine.com/2011/09/27/searchable-dynamic-content-with-ajax-crawling/)