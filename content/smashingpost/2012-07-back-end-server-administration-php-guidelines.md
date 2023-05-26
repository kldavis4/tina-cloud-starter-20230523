---
title: Back-End and Server Administration Guidelines
slug: back-end-server-administration-php-guidelines
image: null
date: 2012-07-30T12:30:17.000Z
author: vitaly-friedman
description: >-
  Here you will find posts featuring some of the most useful articles related to
  back-end and server administration which have been published on Smashing
  Magazine over all the years.
categories: []
---

Here you will find posts featuring some of the most useful articles related to back-end and server administration which have been published on Smashing Magazine over all the years.



#### Quick Overview

*   [Introduction to DNS: Explaining The Dreaded DNS Delay](#n1)
*   [Image Manipulation With jQuery and PHP GD](#n2)
*   [Speeding Up Your Website’s Database](#n3)
*   [Keeping Web Users Safe By Sanitizing Input Data](#n4)
*   [What To Do When Your Website Goes Down](#n5)
*   [Common Security Mistakes in Web Applications](#n6)
*   [PHP: What You Need To Know To Play With The Web](#n7)
*   [Developing Sites With AJAX: Design Challenges and Common Issues](#n8)
*   [Web Security: Are You Part Of The Problem?](#n9)
*   [Website Performance: What To Know and What You Can Do](#n10)
*   [Introduction To URL Rewriting](#n101)
*   [All About Unicode, UTF8 & Character Sets](#n102)
*   [Twelve Commandments Of Software Localization](#n103)
*   [How To Develop Websites On Linux](#n11)
*   [Introduction To Linux Commands](#n111)
*   [Crucial Concepts Behind Advanced Regular Expressions](#n12)
*   [10 Advanced PHP Tips To Improve Your Programming](#n13)
*   [The Big PHP IDE Test: Why Use One And Which To Choose](#n14)
*   [My Favorite Programming Mistakes](#n141)
*   [A Guide To PHP Error Messages For Designers](#n142)

## [Introduction to DNS: Explaining The Dreaded DNS Delay](https://www.smashingmagazine.com/2011/05/25/introduction-to-dns-explaining-the-dreaded-dns-delay/ "Permanent Link to Introduction to DNS: Explaining The Dreaded DNS Delay")

Imagine that your biggest client calls because they are having trouble retrieving their email. Or they want to know what their best-selling item is right now. Or their most popular blog post. Perhaps their website has suddenly gone down. You can hardly reply, “No problem, I’ll get back to you in 24 to 48 hours.” And yet DNS gets away with it! If you need to move a website or change the way a domain’s email is handled, you’ll be faced with a vague 24 to 48-hour delay.

<figure><a href="https://www.smashingmagazine.com/2011/05/25/introduction-to-dns-explaining-the-dreaded-dns-delay/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f81e294c-7080-47fb-b676-ed686db4dd97/domain-registration-ip-screenshot.jpg" width="556" height="262" alt="Screenshot" /></a></figure>

This is quite an anomaly in a world of ultra-convenience and super-fast everything. This article explains what DNS is, how it works, where that pesky delay comes from, and a couple of ways to work around it. DNS is the “domain name system.” It translates human-friendly website addresses like www.cnn.com into computer-friendly IP addresses like 157.166.224.25\. Try visiting https://157.166.224.25 if you’d like to verify this.



[Read more...](https://www.smashingmagazine.com/2011/05/25/introduction-to-dns-explaining-the-dreaded-dns-delay/)

## [Image Manipulation With jQuery and PHP GD](https://www.smashingmagazine.com/2011/04/05/image-manipulation-with-jquery-and-php-gd/ "Permanent Link to Image Manipulation With jQuery and PHP GD")

One of the numerous advantages brought about by the explosion of jQuery and other JavaScript libraries is the ease with which you can create interactive tools for your site. When combined with server-side technologies such as PHP, this puts a serious amount of power at your finger tips.

<figure><a href="https://www.smashingmagazine.com/2011/04/05/image-manipulation-with-jquery-and-php-gd/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdad1820-9e92-4284-9a81-a74d902c4a11/uploaded-image.gif" width="500" height="271" alt="Image Manipulation With jQuery and PHP GD" /></a></figure>

In this article, I’ll be looking at how to combine JavaScript/jQuery with PHP and, particularly, PHP’s GD library to create an image manipulation tool to upload an image, then crop it and finally save the revised version to the server. Sure, there are plugins out there that you can use to do this; but this article aims to show you what's behind the process. You can [download the source files](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99e2aff8-9705-46e2-8cfe-9d417db37476/sm-image-manipulation.zip) for reference.



[Read more...](https://www.smashingmagazine.com/2011/04/05/image-manipulation-with-jquery-and-php-gd/)

## [Speeding Up Your Website’s Database](https://www.smashingmagazine.com/2011/03/23/speeding-up-your-websites-database/ "Permanent Link to Speeding Up Your Website’s Database")

Website speed has always been a big issue, and it has become even more important since April 2010, when Google decided to use it in search rankings. However, the focus of the discussion is generally on minimizing file sizes, improving server settings and optimizing CSS and Javascript.

<figure><a href="https://www.smashingmagazine.com/2011/03/23/speeding-up-your-websites-database/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b15f6122-17ca-48c0-bac6-9f580611700c/sql-speed.jpg" width="500" height="306" alt="Screenshot" /></a></figure>

The discussion glosses over another important factor: the speed with which your pages are actually put together on your server. Most big modern websites store their information in a database and use a language such as PHP or ASP to extract it, turn it into HTML and send it to the Web browser.

So, even if you get your home page down to 1.5 seconds (Google’s threshold for being considered a “fast” website), you can still frustrate customers if your search page takes too much time to respond, or if the product pages load quickly but the “Customer reviews” delay for several seconds.



[Read more...](https://www.smashingmagazine.com/2011/03/23/speeding-up-your-websites-database/)

## [Keeping Web Users Safe By Sanitizing Input Data](https://www.smashingmagazine.com/2011/01/11/keeping-web-users-safe-by-sanitizing-input-data/ "Permanent Link to Keeping Web Users Safe By Sanitizing Input Data")

In my [last article](https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/), I spoke about several common mistakes that show up in web applications. Of these, the one that causes the most trouble is insufficient input validation/sanitization. In this article, I'm joined by my colleague Peter (evilops) Ellehauge in looking at input filtering in more depth while picking on a few real examples that we've seen around the web. As you'll see from the examples below, insufficient input validation can result in various kinds of code injection including <abbr title="Cross Site Scripting">XSS</abbr>, and in some cases can be used to phish user credentials or spread malware.

<figure><a href="https://www.smashingmagazine.com/2011/01/11/keeping-web-users-safe-by-sanitizing-input-data/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87fafbb6-a11f-44b8-b1c7-ded35df4f2b7/exploits.gif" width="480" height="205" alt="Screenshot" /></a></figure>

To start with, we'll take an example<sup>[[1](https://www.smashingmagazine.com/2011/01/11/keeping-web-users-safe-by-sanitizing-input-data/#bm-cablegate)]</sup> from one of the most discussed websites today. This example is from a site that hosts WikiLeaks material. Note that the back end code presented is not the actual code, but what we think it might be based on how the exploit works. The HTML was taken from their website. We think it's fair to assume that it's written in PHP as the form's action is index.php.



[Read more...](https://www.smashingmagazine.com/2011/01/11/keeping-web-users-safe-by-sanitizing-input-data/)

## [What To Do When Your Website Goes Down](https://www.smashingmagazine.com/2010/12/13/what-to-do-when-your-website-goes-down/ "Permanent Link to What To Do When Your Website Goes Down")

Have you ever heard a colleague answer the phone like this: "Good afterno… Yes… What? Completely?… When did it go down?… Really, that long?… We'll look into it right away… Yes, I understand… Of course… Okay, speak to you soon… Bye." The call may have been followed by some cheesy ’80s rock ballad coming from the speaker phone, interrupted by "Thank you for holding. You are now caller number 126 in the queue." That's your boss calling the hosting company's 24 hour "technical support" line.

<figure><a href="https://www.smashingmagazine.com/2010/12/13/what-to-do-when-your-website-goes-down/"><img loading="lazy" decoding="async" class="77993" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3bd8345-b476-4005-9bf2-fcf24a6cda7d/linux-commands-dfh.png" alt="Screenshot" width="528" height="243" /></a></figure>

An important **website has gone down**, and sooner or later, heads will turn to the Web development corner of the office, where you are sitting quietly, minding your own business, regretting that you ever mentioned "Linux" on your CV. You need to take action. Your company needs you. Your client needs you. Here's what to do.



[Read more...](https://www.smashingmagazine.com/2010/12/13/what-to-do-when-your-website-goes-down/)

## [Common Security Mistakes in Web Applications](https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/ "Permanent Link to Common Security Mistakes in Web Applications")

Web application developers today need to be skilled in a multitude of disciplines. It's necessary to build an application that is user friendly, highly performant, accessible and secure, all while executing partially in an untrusted environment that you, the developer, have no control over. I speak, of course, about the User Agent. Most commonly seen in the form of a web browser, but in reality, one never really knows what's on the other end of the HTTP connection.

<figure><a href="https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb2a3284-8578-4422-b859-fcba4d52e33f/sql.png" width="550" height="169" alt="https://xkcd.com/327/" border="0" /></a></figure>

There are many things to worry about when it comes to **security on the Web**. Is your site protected against denial of service attacks? Is your user data safe? Can your users be tricked into doing things they would not normally do? Is it possible for an attacker to pollute your database with fake data? Is it possible for an attacker to gain unauthorized access to restricted parts of your site? Unfortunately, unless we're careful with the code we write, the answer to these questions can often be one we'd rather not hear.



[Read more...](https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/)

## [PHP: What You Need To Know To Play With The Web](https://www.smashingmagazine.com/2010/04/15/php-what-you-need-to-know-to-play-with-the-web/ "Permanent Link to PHP: What You Need To Know To Play With The Web")

In this article, I'll introduce you to the fundamentals of PHP. We'll focus on **using PHP to access Web services** and on turning static HTML pages into dynamic ones by retrieving data from the Web and by showing different content depending on what the user has entered in a form or requested in the URL. You won't come out a professional PHP developer, but you'll be well on your way to building a small page that uses Web services. You can find a lot of great PHP info on the Web, and most of the time you will end up on [PHP.net](https://php.net) itself. But I was asked repeatedly on several hack days and competitions to write this quick introduction article, so here it is.

<figure><a href="https://www.smashingmagazine.com/2010/04/15/php-what-you-need-to-know-to-play-with-the-web/"><img width="500" height="328" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1558a647-0c7c-485e-8bfc-371e97c2dfa4/phperrorlog1.jpg" alt="PHP rendered in a browser" /></a></figure>

PHP is a server-side language that has become a massive success for three reasons: it is a very easy and forgiving language. Variables can be anything, and you can create them anytime you want. It is part of the free LAMP stack (Linux, Apache, MySQL, PHP) and thus available on almost any server you can rent on the Web. And it does not need a special editor, environment or build process. All you do is create a file of the _.php_ file type, mix PHP and HTML and then put it on your server for rendering.



[Read more...](https://www.smashingmagazine.com/2010/04/15/php-what-you-need-to-know-to-play-with-the-web/)

## [Developing Sites With AJAX: Design Challenges and Common Issues](https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/ "Permanent Link to Developing Sites With AJAX: Design Challenges and Common Issues")

Almost every movie has a scene in which a character pull the protagonist aside and says, "There's something you should know about [insert another character's name here]." Most of the time, we find out some dark secret about a supposed friend of the protagonist or that the main ally is actually an evil overlord. This is that moment, and I am here to tell you a few things about our friend in the Web 2.0 world: AJAX.

<figure><a href="https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0077280-16c6-41f7-aa4e-64b7795c985c/get-satisfaction-small2.jpg" width="550" height="390" alt="Modal Pop-Up form by get satisfaction"></a></p>

**We seem to have AJAX licked**. The Web technology is ubiquitous, and libraries and frameworks make it dead easy for us to create highly interactive Web applications and to spice up our static pages and blogs.

After the main HTML document has loaded, AJAX loads content from the server and replaces parts of the document with that content rather than reload the main document. It's as simple as that. AJAX stands for "Asynchronous JavaScript and XML" and was meant to load only XML documents, but we soon used it to load everything under the sun, and so the XML part was quickly forgotten. The asynchronous part is the killer feature; but what is it?



[Read more...](https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/)

## [Web Security: Are You Part Of The Problem?](https://www.smashingmagazine.com/2010/01/14/web-security-primer-are-you-part-of-the-problem/ "Permanent Link to Web Security: Are You Part Of The Problem?")

**Website security** is an interesting topic and should be high on the radar of anyone who has a Web presence under their control. Ineffective Web security leads to all of the things that make us hate the Web: spam, viruses, identity theft, to name a few.

<figure><a href="https://www.smashingmagazine.com/2010/01/14/web-security-primer-are-you-part-of-the-problem/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ef5c5c-fef5-498f-804e-33c22a059c6c/4239939571-b7d3cddc83-o.gif" alt="Web Vulnerabilities Q1/Q2 2009."></a></p>

The problem with Web security is that, as important as it is, it is also very complex. I am quite sure that some of you reading this are already part of an network of attack computers and that your servers are sending out spam messages without you even knowing it. Your emails and passwords have been harvested and resold to people who think you need either a new watch, a male enhancement product or a cheap mortgage. Fact is, you are part of the problem and don't know what you did to cause it.

**Disclaimer**: the things we'll talk about in this article today won't make you a security expert, just as buying a Swiss Army knife won't make you a locksmith or buying a whip won't make you a lion tamer. The purpose here is to **raise awareness** and perhaps make some of that security mumbo-jumbo a bit more understandable to you.



[Read more...](https://www.smashingmagazine.com/2010/01/14/web-security-primer-are-you-part-of-the-problem/)

## [Website Performance: What To Know and What You Can Do](https://www.smashingmagazine.com/2010/01/06/page-performance-what-to-know-and-what-you-can-do/ "Permanent Link to Website Performance: What To Know and What You Can Do")

**Website performance** is a hugely important topic, so much so that the big companies of the Web are obsessed with it. For the Googles, Yahoos, Amazons and eBays, slow websites mean fewer users and less happy users and thus lost revenue and reputation. In your case, annoying a few users wouldn't be much of a problem, but if millions of people are using your product, you'd better be snappy in delivering it. For years, Hollywood movies showed us how fast the Internet was: time to make that a reality.

<figure><a href="https://www.smashingmagazine.com/2010/01/06/page-performance-what-to-know-and-what-you-can-do/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/100e072c-0b68-4da1-a081-1b3da38e9f7b/optimization.gif" width="489" height="330" alt="Screenshot" /></a></figure>

Even if you don't have millions of users (yet), consider one very important thing: people are consuming the Web nowadays less with fat connections and massive computers and more with mobile phones over slow wireless and 3G connections, but they still expect the same performance. Waiting for a slow website to load on a mobile phone is doubly annoying because the user is usually already in a hurry and is paying by the byte or second. It's 1997 all over again.

**Performance is an expert's game... to an extent**. You can do innumerable things to make a website perform well, and much of it requires in-depth knowledge and boring testing and research. I am sure a potential market exists for website performance optimization, much like there is one now for search engine optimization. Interestingly, Google recently announced that [it will factor performance into its search rankings](https://www.downloadsquad.com/2009/11/14/google-to-use-page-load-speed-as-a-search-result-ranking-factor/), so this is already happening. That said, you can do a lot of things without having to pay someone to point out the obvious.



[Read more...](https://www.smashingmagazine.com/2010/01/06/page-performance-what-to-know-and-what-you-can-do/)

## [Introduction To URL Rewriting](https://www.smashingmagazine.com/2011/11/02/introduction-to-url-rewriting/ "Permanent Link to Introduction To URL Rewriting")

Many Web companies spend hours and hours agonizing over the best domain names for their clients. They try to find a domain name that is relevant and appropriate, sounds professional yet is distinctive, is easy to spell and remember and read over the phone, looks good on business cards and is available as a dot-com.

They go through all that trouble with the domain name but neglect the rest of the URL, the element _after_ the domain name. It, too, should be relevant, appropriate, professional, memorable, easy to spell and readable. And for the same reasons: to attract customers and improve in search ranking.

<figure><a href="https://www.smashingmagazine.com/2011/11/02/introduction-to-url-rewriting/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac912e5b-987e-44ee-a44f-fbe2e28b6e12/wikipedia-barack-short.png" alt="screenshot"></a></p>

Fortunately, there is a technique called URL rewriting that can turn unsightly URLs into nice ones—with a lot less agony and expense than picking a good domain name. It enables you to fill out your URLs with friendly, readable keywords without affecting the underlying structure of your pages.

This article covers the following:

1.  What is URL rewriting?
2.  How can URL rewriting help your search rankings?
3.  Examples of URL rewriting, including regular expressions, flags and conditionals;
4.  URL rewriting in the wild, such as on Wikipedia, WordPress and shopping websites;
5.  Creating friendly URLs;
6.  Changing pages names and URLs;
7.  Checklist and troubleshooting.

[Read more...](https://www.smashingmagazine.com/2011/11/02/introduction-to-url-rewriting/)

## [All About Unicode, UTF8 & Character Sets](https://www.smashingmagazine.com/2012/06/06/all-about-unicode-utf8-character-sets/ "Permanent Link to All About Unicode, UTF8 & Character Sets")

This is a story that dates back to the earliest days of computers. The story has a plot, well, sort of. It has competition and intrigue, as well as traversing oodles of countries and languages. There is conflict and resolution, and a happyish ending. But the main focus is the characters — **110,116** of them. By the end of the story, they will all find their own unique place in this world.

<figure><a href="https://www.smashingmagazine.com/2012/06/06/all-about-unicode-utf8-character-sets/"><img loading="lazy" decoding="async" class="119962" title="Same sequence of numbers shown using the ISO-8859-1 character set" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16b3151f-5dfb-4d73-ad2f-88c78f720d4a/characters-iso-8859-1-blue.png" alt="Same sequence of numbers shown using the ISO-8859-1 character set"></a></p>

This story (or _article_, as known on Smashing Magazine) will follow a few of those characters more closely, as they journey from Web server to browser, and back again. Along the way, you'll find out more about the history of characters, character sets, Unicode and UTF-8, and why question marks and odd accented characters sometimes show up in databases and text files.

[Read more...](https://www.smashingmagazine.com/2012/06/06/all-about-unicode-utf8-character-sets/)

## [Twelve Commandments Of Software Localization](https://www.smashingmagazine.com/2012/07/18/12-commandments-software-localization/ "Permanent Link to Twelve Commandments Of Software Localization")

You've presented the new website and everyone loves it. The design is crisp, the code is bug-free, and you're ready to release. Then someone asks, “Does it work in Japanese?”

You break out in a cold sweat: you have no idea. The website works in English, and you figured other languages would come later. Now you have to rework the whole app to support other languages. Your release date slips, and you spend the next two months fixing bugs, only to find that you’ve missed half of them.

<figure><a href="https://www.smashingmagazine.com/2012/07/18/12-commandments-software-localization/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06256223-d1b2-43bb-8855-8f129cbf716e/repeat-password.png" alt="Repeat password example" title="Repeat password example" class="aligncenter size-full wp-image-120596"></a></p>

Localization makes your application ready to work in any language — and it's much easier if you do it from the beginning. Just follow these 12 simple rules and you'll be ready to run anywhere in the world.

[Read more...](https://www.smashingmagazine.com/2012/07/18/12-commandments-software-localization/)

## [How To Develop Websites On Linux](https://www.smashingmagazine.com/2009/08/28/how-to-develop-web-sites-on-linux/ "Permanent Link to How To Develop Websites On Linux")

In this article we will look at tools that can help those of you who want to **develop websites on a Linux platform**, from powerful text editors to desktop and system features. How do you edit files remotely without FTP plug-ins? What are package managers, and why they are cool? In which Web browsers can you test your applications?

<figure><a href="https://www.smashingmagazine.com/2009/08/28/how-to-develop-web-sites-on-linux/"><img alt="Gedit Themed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88affbc0-6e56-42f9-a1f6-2a174d9e7843/003.jpg" width="500" height="343" /></a></figure>

I wish I could cover many more topics: using the command line, basics of Vim, Nautilus features in detail, Nautilus scripting, neat command line tools, basic server configuration and many others. But if I addressed all of the issues that arise from time to time on the Internet, this article would turn into a small book. This isn't an article on "How to do X or Y on Linux" or "How to use [insert app name here]." And we cannot cover more comprehensive IDEs such as Eclipse and NetBeans, each of which requires separate articles.

You probably already have some idea of how to find and install applications for your favorite distros. However, we will point you to the right place anyway to download, for example, scripts and plug-ins. So, let's begin!

[Read more...](https://www.smashingmagazine.com/2009/08/28/how-to-develop-web-sites-on-linux//#more-8179)

## [Introduction To Linux Commands](https://www.smashingmagazine.com/2012/01/23/introduction-to-linux-commands/ "Permanent Link to Introduction To Linux Commands")

At the heart of every modern Mac and Linux computer is the “terminal.” The terminal evolved from the [text-based computer terminals](https://en.wikipedia.org/wiki/VT52) of the 1960s and ’70s, which themselves replaced punch cards as the main way to interact with a computer. It’s also known as the command shell, or simply “shell.” Windows has one, too, but it’s called the “command prompt” and is descended from the MS-DOS of the 1980s.

Mac, Linux and Windows computers today are mainly controlled through user-friendly feature-rich graphical user interfaces (GUIs), with menus, scroll bars and drag-and-drop interfaces. But all of the basic stuff can still be accomplished by typing text commands into the terminal or command prompt.

<figure><a href="https://www.smashingmagazine.com/2012/01/23/introduction-to-linux-commands/"><img loading="lazy" decoding="async" class="116399" title="Successful SSH to a server" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7ab0607-bd7c-4cfa-9760-d5834feeacd2/home-ssh-successful.png" alt="Successful SSH to a server"></a></p>

Sometimes these lean Linux servers are managed through a Web browser interface, such as cPanel or Plesk, letting you create databases, email addresses and websites; but sometimes that is not enough. This article provides a broad introduction to text commands and the situations in which they are useful. We’ll cover the following:

*   Why knowing a few commands is useful;
*   Issuing commands on your own computer;
*   Using SSH to log into your Web server;
*   Getting your bearings: `pwd`, `cd ls`;
*   Viewing and moving files: `cat`, `more`, `head`, `tail`, `mv`, `cp`, `rm`;
*   Searching for files: `find`;
*   Looking through and editing files: `grep`, `vi`;
*   Backing up and restoring files and databases: `tar`, `zip`, `unzip`, `mysqldump`, `mysql`;
*   File permissions: `chmod`.

[Read more...](https://www.smashingmagazine.com/2012/01/23/introduction-to-linux-commands/)

## [Crucial Concepts Behind Advanced Regular Expressions](https://www.smashingmagazine.com/2009/05/06/introduction-to-advanced-regular-expressions/ "Permanent Link to Crucial Concepts Behind Advanced Regular Expressions")

Regular expressions (or regex) are a powerful way to traverse large strings in order to find information. They rely on underlying patterns in a string’s structure to work their magic. Unfortunately, simple regular expressions are unable to cope with complex patterns and symbols. To deal with this dilemma, you can use **advanced regular expressions**.

<figure><a href="https://www.smashingmagazine.com/2009/05/06/introduction-to-advanced-regular-expressions/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034e0c67-55bd-44bc-a003-06e5c823e97f/recursion.jpg" width="400" height="300" alt="Recursion" /></a></figure>



Below, we present an **introduction to advanced regular expressions**, with eight commonly used concepts and examples. Each example outlines a simple way to match patterns in complex strings. If you do not yet have experience with basic regular expressions, have a look at this article to get started. The syntax used here matches PHP regular expressions.



[Read more...](https://www.smashingmagazine.com/2009/05/06/introduction-to-advanced-regular-expressions//#more-6185)

## [10 Advanced PHP Tips To Improve Your Programming](https://www.smashingmagazine.com/2008/11/18/10-advanced-php-tips-to-improve-your-progamming/ "Permanent Link to 10 Advanced PHP Tips To Improve Your Programming")

PHP programming has climbed rapidly since its [humble beginnings](https://en.wikipedia.org/wiki/PHP) in 1995\. Since then, PHP has become the most popular programming language for Web applications. Many popular websites are powered by PHP, and an overwhelming majority of scripts and Web projects are built with the popular language.


<figure><a href="https://www.smashingmagazine.com/2008/11/18/10-advanced-php-tips-to-improve-your-progamming"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4409db11-ffcd-4c11-b85d-a30e506712cf/cakephp.png" alt="Framework" width="459" height="249" /></a></figure>

Because of PHP’s huge popularity, it has become almost impossible for Web developers not to have at least a working knowledge of PHP. This tutorial is aimed at people who are just past the beginning stages of learning PHP and are ready to roll up their sleeves and get their hands dirty with the language. Listed below are **10 excellent techniques that PHP developers should learn and use** every time they program. These tips will speed up proficiency and make the code much more responsive, cleaner and more optimized for performance.



[Read more...](https://www.smashingmagazine.com/2008/11/18/10-advanced-php-tips-to-improve-your-progamming//#more-1958)

## [The Big PHP IDE Test: Why Use One And Which To Choose](https://www.smashingmagazine.com/2009/02/11/the-big-php-ides-test-why-use-oneand-which-to-choose/ "Permanent Link to The Big PHP IDE Test: Why Use One And Which To Choose")

Everyone wants to be more productive, make fewer mistakes and write good code. Of course, that all depends on you, but in most cases integrated development environments (IDEs) can help you achieve those goals more easily. Unfortunately, choosing the right IDE is very difficult because a lot needs to be considered. And the website of almost every IDE [tells us it is the best one](https://www.zend.com/en/products/studio/compare).

<figure><a href="https://www.smashingmagazine.com/2009/02/11/the-big-php-ides-test-why-use-oneand-which-to-choose/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5860de2-bf42-4adf-ae81-803a38d1d892/ides-best.png" alt="I am the best!" width="577" height="299" /></a></figure>

In this post, we'll **take a close look at the most popular PHP IDEs**, exploring their functions, comparing them in a table and drawing some conclusions. Hopefully, you'll get an idea of what each PHP IDE has to offer and which one best fits your needs.



[Read more...](https://www.smashingmagazine.com/2009/02/11/the-big-php-ides-test-why-use-oneand-which-to-choose//#more-3932)



## [My Favorite Programming Mistakes](https://www.smashingmagazine.com/2011/07/07/my-favorite-programming-mistakes/ "Permanent Link to My Favorite Programming Mistakes")

Over my programming career, I have made a lot of mistakes in several different languages. In fact, if I write 10 or more lines of code and it works the first time, I’ll get a bit suspicious and test it more rigorously than usual. I would expect to find a syntax error or a bad array reference or a misspelled variable or _something_.

I like to classify these mistakes into three broad groups: cock-ups (or screw-ups in American English), errors and oversights. A cock-up is when you stare blankly at the screen and whisper “Oops”: things like deleting a database or website, or overwriting three-days worth of work, or accidentally emailing 20,000 people.

<figure><a href="https://www.smashingmagazine.com/2011/07/07/my-favorite-programming-mistakes/"><img loading="lazy" decoding="async" class="104010" title="Mwnt beach" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7390f9b8-e36d-4aaf-ae27-65d7d912cb32/mwnt-beach.jpg" alt="Mwnt beach" width="542" height="214" /></a></figure>

Errors cover everything, from simple syntax errors like forgetting a `}` to fatal errors and computational errors. When an error is so subtle and hard to find that it is almost beautiful, I would call it an oversight. This happens when a block of code is forced to handle a completely unforeseen and very unlikely set of circumstances. It makes you sit back and think “Wow”: like seeing a bright rainbow or shooting star, except a bit less romantic and not quite as impressive when described to one's partner over a candlelit dinner.

This article discusses some of the spectacular and beautiful mistakes I have made, and the lessons learned from them. The last three are my favorites.

[Read more...](https://www.smashingmagazine.com/2011/07/07/my-favorite-programming-mistakes/)

## [A Guide To PHP Error Messages For Designers](https://www.smashingmagazine.com/2011/11/30/a-guide-to-php-error-messages-for-designers/ "Permanent Link to A Guide To PHP Error Messages For Designers")

PHP is widely available with inexpensive hosting plans, which makes it a popular choice for developers who write software for the Web. From big platforms, such as WordPress, down to small scripts, such as ones to display image galleries or to send forms to email, thousands of script and products are out there written in PHP that can be installed and used even if you don’t know much about PHP yourself.

<figure><a href="https://www.smashingmagazine.com/2011/11/30/a-guide-to-php-error-messages-for-designers/"><img loading="lazy" decoding="async" class="119387" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09a62738-44a5-4172-99a9-0666c7868871/privs.png" alt="screenshot"></a></p>

This article is aimed at designers who are not PHP developers but need to install PHP scripts from time to time. Thus, the problems and error messages we will look at here are those you are most likely to encounter when installing scripts, rather than when writing PHP. The tips should help you work through other error messages and should at least help you give clear information to the script’s developer if you need to ask them for assistance.

[Read more...](https://www.smashingmagazine.com/2011/11/30/a-guide-to-php-error-messages-for-designers/)

### Related Posts

You might be interested in the following "Best of" selections as well:

*   [Learning CSS3: A Reference Guide](https://www.smashingmagazine.com/learning-css3-useful-reference-guide/)
*   [Learning JavaScript: Essentials And Guidelines](https://www.smashingmagazine.com/learning-javascript-essentials-guidelines-tutorials/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)
*   [Learning WordPress: Most Useful Tips and Tutorials](https://www.smashingmagazine.com/learning-wordpress-useful-wordpress-tips-tutorials/)