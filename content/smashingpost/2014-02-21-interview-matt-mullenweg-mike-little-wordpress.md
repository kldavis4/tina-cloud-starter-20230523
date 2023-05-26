---
title: How WordPress Came To Be - An Interviews With Matt Mullenweg And Mike Little
slug: interview-matt-mullenweg-mike-little-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5649524c-2826-417b-905e-88aa1339e966/matt-mullenweg-summit-opt1.png
date: 2014-02-21T12:07:54.000Z
author: alex-moss
description: >-
  2013 was a busy year for me for conferences and travel. I met [Mike Little](https://mikelittle.org/), one of the two co-founders of WordPress. Three months later, I was honored to meet the other co-founder, [Matt
  Mullenweg](https://ma.tt/), twice in three weeks: at [WordCamp Europe and at The Summit.
categories:
  - WordPress
  - Inspiration
  - Interviews
---
2013 was a busy year for me for conferences and travel. I met [Mike Little](https://mikelittle.org/), one of the two co-founders of WordPress. Three months later, I was honored to meet the other co-founder, [Matt Mullenweg](https://ma.tt/), twice in three weeks: at WordCamp Europe and at The Summit.

## Interview With Matt Mullenweg

<strong>Q:</strong> Matt, you've attended nearly every Summit since its inception and were the first speaker to be announced and the only person who has returned every year to attend. What is it about The Summit that brings you back to Dublin every year, and what can you share about The Summit with someone who has never attended?

{{% feature-panel %}}

<strong>Matt:</strong> I love Ireland and have visited several times before The Summit. Paddy [Cosgrave] and the team bring together a great group of people, and I always enjoy the activities and the folks I meet.

<strong>Q:</strong> Over the years, more code is becoming the standard practice on any website. Is WordPress making any plans to integrate features such as Schema or Facebook Open Graph tags into the core?

<strong>Matt:</strong> We’re happy to adopt and support standards but generally don’t integrate tags that are proprietary to a third party.

<strong>Q:</strong> Do you have any plans for a “from the ground up rebuild,” or maybe to drop <code>deprecated.php</code> and make a cleaner, lighter version for 4.0?

<strong>Matt:</strong> We rewrite or refactor about 10 to 15% of WordPress in most releases, so that we can keep users getting updates and new features quickly, while doing the “ground up rebuild” incrementally in the background, fixing bugs and getting feedback as we go. Sometimes old functions hang out for a while, as you noted with <code>deprecated.php</code>. That’s because we try to be good about backwards-compatibility, so that people can upgrade to the latest version without worry.

<a style="border: none" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b909bde-7243-4aed-85f0-7c8b02eb51aa/matt-mullenweg-wordpress-cofounder.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/301576e6-8aab-4e25-9fef-dd0f06ed3dae/matt-mullenweg-summit-opt.png" alt="Matt Mullenweg at The Summit in Dublin, October 2013" width="500" height="331" /></a><br>
<em>Matt Mullenweg at The Summit in Dublin, October 2013 (Image: <a href="https://www.flickr.com/photos/websummit/10707615933/in/set-72157637157375516">Dan Taylor/Heisenberg Media</a>)</em>

<strong>Q:</strong> Some WordPress developers say that users and roles are generally quite limited in core and that not a lot of great plugins exist to enhance features that user roles could provide. Are there any plans to evolve this section of the core?

Recommended reading: [How To Become A Top WordPress Developer](https://www.smashingmagazine.com/2012/08/how-to-become-a-top-wordpress-developer/)

<strong>Matt:</strong> I’m not aware of anything that you can’t do with the user and roles system. Usually I’ll get the opposite complaint, that roles and capabilities are too complex.

<strong>Q:</strong> At WordCamp Europe, you briefly mentioned that you were going to be more hands-on with development of the core. Can you elaborate on that?

<strong>Matt:</strong> I was alluding to 3.8, the release I led that <a href="https://wordpress.org/news/2013/12/parker/">came out on December 12th</a>.

<strong>Q:</strong> If WordPress didn’t exist today, what CMS would you be using right now?

<strong>Matt:</strong> I’d probably use something bespoke.

<strong>Q:</strong> Premium theme and plugin websites have increasingly grown outside of the official repository. Does WordPress.org have any plans to serve GPL-friendly premium plugins in a repository, similar to the themes offered on WordPress.com?

<strong>Matt:</strong> We have no plans to have paid products hosted or sold on WordPress.org.

<strong>Q:</strong> Do you have a particular non-Automattic plugin that you could share with users?

<strong>Matt:</strong> Sure, I like <a href="https://wordpress.org/plugins/dropbox-photo-sideloader/">Dropbox Photo Sideloader</a>, <a href="https://wordpress.org/plugins/email-post-changes/">Email Post Changes</a> and… most everything else I love is covered by <a href="https://wordpress.org/plugins/jetpack/">Jetpack</a>.

<strong>Q:</strong> What one piece of advice would you give to anyone who is thinking about developing a theme or plugin?

Recommended reading: [Practical Tips From Top WordPress Pros](https://www.smashingmagazine.com/2013/03/practical-tips-top-wordpress-pros/)

<strong>Matt:</strong> Design and usability are more important than ever. Watch a friend or family member try to use your plugin from start to finish, and it’ll give you a ton of ideas on how to make it better.

<strong>Q:</strong> Would you and/or your core team consider becoming more active in groups and/or forums? Facebook groups such as <a href="https://www.facebook.com/groups/advancedwp/">Advanced WP</a> are very active.

<strong>Matt:</strong> We have a hard enough time keeping up with the activity on Wordpress.org, but we’re happy when conversations about WordPress are happening anywhere, and I try to chip in where I can.

<strong>Q:</strong> What are the biggest challenges facing WordPress’ growth, beyond powering “just” 20% of the Web?

<strong>Matt:</strong> I think mobile is very challenging because it’s fundamentally on closed platforms.

<strong>Q:</strong> When we met in Leiden, we briefly spoke about Mike Little and how you still keep in touch. Have you considered a reunion?

<strong>Matt:</strong> That’d be great, I’m sure we will run into each other sometime in the near future.

<strong>Q:</strong> What can we see next from Automattic?

<strong>Matt:</strong> Stay tuned. :)

## Interview With Mike Little

<strong>Q:</strong> How did you get into programming?

<strong>Mike:</strong> I actually wrote my first program a very long time ago, in 1978. I was in 6th form, and one day a week we went down to the local college, which had one of these computer things. And I started programming there. It was really old school; it was a teletype terminal, which means that it didn’t have a screen — what you typed came out of the printer in the back. I saved my program onto punched tape. That was OK, but it didn’t last long; our class got banned from the college computers because one of the guys got caught smoking, which was not good. [laughs]

Fast forward a couple of years, and I was working with a couple of bands, and one of the bands wanted to do something fancy with what were then home computers. I ended up borrowing a ZX Spectrum (so it would have been 1982) and managed to put a program together with it, which we completed. Although we never managed to put it live on stage, I really got the programming bug from that. I loved the problem-solving, taking it as far as I could and just making the machines dance to my code. That’s how I got the bug, and I've just kept at it since then.

<a style="border: none" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b0617f9-c98f-4530-9221-670a6a92a5e2/mike-award-1280.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d185d5f2-1ec1-4d5d-9856-e855497552d5/mike-little-award-opt.png" alt="SONY DSC" width="500" height="282" /></a><br>
<em>Mike Little accepts his award for Outstanding Contribution to Digital at SAScon 2013. (Image: <a href="https://mikelittle.org/outstanding-contribution-award/">Mike Little</a>)</em>

<strong>Q:</strong> It has been 10 years since WordPress launched. Did you realize how big it would become? And if not, did you have any thoughts on how big it might be?

<strong>Mike:</strong> No, not at all. I wasn’t thinking at all in those terms. It was more about fixing the software that Matt, I and a few others were using. [Editorial note: Matt Mullenweg and Mike Little were working with the abandoned PHP-based blogging software b2/cafelog, by Michel Valdrighi, which eventually became WordPress.] The software had a few bugs in it, and our primary intention was to fix the bugs and make some tweaks to make it better.

Speaking for myself, I never really had any thoughts lined up in terms of marketshare or anything like that. I’m not really a business-oriented person, so for me it was just about fixing the code, making it better and seeing how it goes.

<strong>Q:</strong> How does it feel now, knowing that more websites are running on a system that you partially created than there are people living in the United Kingdom?

<strong>Mike:</strong> I’m astonished every day, looking at the number of things built on WordPress. I’m astonished by the size of the community, the number of plugins and themes, and all of the businesses that are making a living from WordPress. I’m humbled by the small part that I played at the start of all of this.

<strong>Q:</strong> It reminds of this funny anecdote at the dinner table, where someone says, “And what do you do?” “I founded this CMS.” “Oh, what’s it called?” “WordPress.” “I use that!”

<strong>Mike:</strong> Yes, it’s not really something that I talk about. I’ll mention it in a WordPress-type situation, but it’s not really something I want to brag about. I think — and I’m happy to say this — WordPress is as good as it is because of all the people who have worked on it after me.

<strong>Q:</strong> It’s good to know that the community is so big. On the other hand, what do think are the biggest challenges facing the growth of WordPress?

<strong>Mike:</strong> Keeping it usable. In fact, making it even more usable. I know there are multiple strands of work in progress to achieve that and make it even easier for people starting out. I actually do WordPress training, including a beginners course, with people who have literally just had a quick dabble with WordPress.

I still find it amazing how hard it is to do the easy stuff. Generally, computers are not intuitive. A touchscreen is a little more intuitive than a keyboard and mouse. As soon as you learn the basics in WordPress, it’s all really easy, but until you learn the basics, it’s actually not. I know that a lot of effort is being put into making these first steps much easier, so that someone brand new can just press that “one-click install” button and be easily led through the next steps.

I think this is the biggest challenge, because as more and more people use WordPress, essentially you’ll have more people who are less tech-savvy, and it’s important to make it easy for them to come on board.

<strong>Q:</strong> I agree. Our clients mostly use WordPress. It looks ominous to them for about 10 seconds, but then you tell them to take a deep breath, and after 10 minutes it just clicks with them. You mentioned that you do training. Do you find that this is part of the evolution of WordPress? Do you think training services are more in demand now than custom WordPress builds, which is what we both do for a living?

<strong>Mike:</strong> I think it’s a mixture of both. When you have to build a site with very specific features for a client, you can take away the development part and make it much easier for the client to use it. However, the training that I’ve been doing is for a more general purpose. The people who I train are looking to build and manage sites for themselves or the companies they work for. They need to know a reasonable amount about WordPress (for example, how to build or configure a site with it). There is a lot of things that people can do with WordPress to make themselves a sophisticated site, but it isn’t at all intuitive and it's where they need a bit of leading. But they can do it. Sometimes it’s quite amazing how even seasoned users learn new things about it or things that came along after they went through that learning curve.

<strong>Q:</strong> I like to consider myself a seasoned user and admit that I still find new functions that I didn’t know about, and it’s good to know that it’s the same for others. Do most clients just want to expand their general knowledge, or do they want their WordPress site to do A, B and C and leave the programming to you?

<strong>Mike:</strong> It’s quite a mixture. At the moment, there is a fairly equal split between the classroom training that I do and the one-to-one training. I have just as many consultations on how to build a site as I get requests for development work for existing clients. On the one hand, I tend to be more interested in the development part — making WordPress jump through hoops and building complex sophisticated sites that stretch WordPress and match the client’s needs in more interesting ways. On the other hand, I do training for absolute beginners. I teach them the difference between posts and pages, and how to insert images.

<strong>Q:</strong> In making WordPress jump through hoops, what has been the hardest hoop to jump through, and how did you do it?

<strong>Mike:</strong> Most of the hoops aren’t actually that hard to jump through. This sounds a bit crazy, I know, but with the hooks, actions and filters, WordPress is such a capable system now. It’s a fantastic framework to build whatever site or even Web app a person wants.

It’s been a few years since I’ve had any real difficulties making WordPress do something. It was for one particular client with a very sophisticated site. Two of the things he wanted was the ability to register new users without an email address or, optionally, with an email address that might already be used by somebody else. WordPress really didn’t like doing that at the time, so this was a very difficult problem to overcome. Actually, back then, I ended up hacking core code to do that. Since then, WordPress has caught up, and enough filters are in place now to get around it in legitimate ways.

For the things I need, finding the right hooks and library functions is usually enough. I might be learning stuff that I didn’t know before, but WordPress is still capable of meeting the needs.

<strong>Q:</strong> Yes, we even build complex commerce sites with WordPress. You say that WordPress covers pretty much everything you want. However, if WordPress didn’t exist right now, what CMS would you be using?

<strong>Mike:</strong> That is a really good question. I think last year when I was asked that question, I said Drupal. I don’t think that’s true anymore. I don’t know what I would be using, to be honest. Without WordPress, I might still be using whatever the latest trend in Java is. I remember just about getting into all of the declarative frameworks, like Spring, that were very popular the last time I worked full time with Java. But yes, without WordPress, which did take me away from my old day job in Java development, I would probably still be using Java.

<strong>Q:</strong> So, what’s changed since less than a year ago when you said Drupal?

<strong>Mike:</strong> Probably I’ve thought a bit more about the question. [laughs] I’ve looked at Drupal a number of times. I looked at it before I got to b2/cafelog and also after a particular project. I even started working with Drupal because at the time I wasn’t sure that WordPress was good enough for what I wanted to do. I ended up giving up on Drupal because it was just too hard for what I wanted to do. And in the end I did use WordPress for that particular project, and it fit it very nicely, although we did hit some of the limitations of WordPress at the time.

The last time I used Drupal, it was probably version 4 or 5, and since then I haven’t heard anything new that makes me think that it’s what I would use for any large project. That’s not to say that it’s not capable; it’s just that its learning curve is probably similar to the one I went through when I learned about all of the Java frameworks. It’s a developers’ tool, and it’s been made to be beautifully architected, and that means there is an investment you have to make, and I’m just not sure that I’d want to continue working with Drupal when I’d probably pick up something that I have more experience with a lot more easily.

<strong>Q:</strong> You mentioned other frameworks. Have you ever worked with one in depth, such as Laravel, Zend or CakePHP?

<strong>Mike:</strong> Not really PHP. I used Zend in the early days when it was more a collection of useful libraries than a framework. I played about with CakePHP in the early days when it was kind of emulating the Ruby on Rails-type thing, where you use the command line to create the structure of your application. But I haven’t seriously worked with any PHP frameworks for a long time.

<strong>Q:</strong> Do you use any software in particular for Web development?

I’ve been using a programmer’s editor called Epsilon for more than 20 year now. I first used it back in the DOS days, pre-Windows, in the early ’90s. It’s my programming tool of choice, a text editor with a lot of bells and whistles. The only thing that I miss from my earliest days of programming is that it doesn’t support debugging. I’ve actually been investigating one of the IDEs — PhpStorm — for doing some proper debugging, which I miss from my old days of C programming and assembler programming. Otherwise, I use Chrome’s Inspector for Web-level front-facing stuff, and everything else I do in a plain text editor.

<strong>Q:</strong> Have you ever used a CSS preprocessor, such as LESS, SASS or Stylus, or do you plan to?

<strong>Mike:</strong> I haven’t yet because I don’t generally do much theme work. I’m more at the plugin level and tweaking themes, rather than creating anything. I’m not a designer by any stretch of the imagination. But funnily enough, just today I’ve scheduled a phone call with a client to talk about exactly that. We’re probably going to use one of those tools because we have a very sophisticated WordPress app that has a main theme with a lot of functionality and half a dozen child themes. Managing the different color schemes across the child themes is becoming a bit of a burden, and that’s exactly what the preprocessors are for. So, I will be looking into it very soon.

<strong>Q:</strong> What’s the one programming language that you would like to learn the most?

<strong>Mike:</strong> I’m not too sure actually. At one point I tried learning Python, and I vaguely know it. Maybe Ruby — I don’t even know it that well. The funny thing is that I’ve got so many programming languages under my belt that, at least for the procedural ones, they are all the same except for the syntax and library calls. A couple of years ago I felt that I needed to know Python because I was mentoring some kids who were learning to code. I think I spent one day going through a Python tutorial before I felt confident enough to help someone who had just started. Nothing that I’ve heard of recently makes me think, “Oh, I’d really like to learn that,” because most of these languages have some kind of specialization, but at the end of the day it’s mostly about syntax and good libraries.

<strong>Q:</strong> What advice would you give to someone who is thinking about starting out in WordPress as a theme or plugin developer?

<strong>Mike:</strong> In both instances, I would say you definitely do need to learn some coding. Even theme developers need to learn some WordPress coding at the PHP level. The key thing is to understand some aspects of the architecture of WordPress — in particular, the actions and filters. Without that understanding, you will struggle to know what you’re doing, even if you can find stuff to copy and paste and fiddle with to make it do what you want. Without that fundamental understanding, people really do struggle and will end up limited, even if they do find some success. That’s key for both roles: learn some coding, learn the fundamentals of the architecture of WordPress, and take it from there.

<strong>Q:</strong> WordPress.org has pages dedicated to developing <a href="https://make.wordpress.org/themes/guidelines/">themes</a> and <a href="https://wordpress.org/plugins/about/guidelines/">plugins</a>, with minimum requirements. Whenever I develop something, even if it’s not going in the repository, I develop as though it will, so that I meet the guidelines.

<strong>Mike:</strong> That’s right. It should be natural to run anything you develop through the automated theme tester, and also to follow the plugins guidelines. Unfortunately, plugin testing can’t be as automated as the theme tester. But follow the guidelines and coding standards, and never stop learning.

<strong>Q:</strong> Do you have any favorite themes or theme developers?

<strong>Mike:</strong> I’m very fond of StudioPress and its Genesis framework. If I’m working on a project that isn’t completely custom or the client doesn’t have a preference, then I’m quite comfortable working with those themes, mainly because I like their flexibility. They have a lot of actions and filters, and you can do an awful lot just by adding and removing actions. Even changing the order of actions makes the theme do different things on the page. I quite like those.

<strong>Q:</strong> Do you have any favorite plugins? Are there any that go into every one of your installations?

<strong>Mike:</strong> There are some basic onces that I install, configure and forget: Limit Login Attempts, WP Super Cache, Yoast’s Google Analytics, Yoast’s SEO. If I’m not hosting the site myself, then a decent backup plugin, although I can’t remember off the top of my head which one; if I host it myself, then the backup is independent of WordPress. If the site has a lot of pages, then I’ll stick the CMS Tree Page View on there, which makes it much easier to manage a lot of pages. Everything else really depends on what the site needs to do.

<strong>Q:</strong> You’re still quite involved in the WordPress community. What exactly do you do in terms of community contributions?

Recommended reading: [How To Contribute To WordPress](https://www.smashingmagazine.com/2013/05/contributing-to-wordpress/)

<strong>Mike:</strong> I run a monthly <a href="https://mwug.info/">WordPress meetup in Manchester</a>, which is thriving. I realized the other day that it’s been going five years. That’s huge. I think there are about 400 members of the meetup, and we generally have around 30 to 40 turn up on the third Wednesday of the month. I also do some of my training for MadLab, which hosts the meetups. It’s a non-profit organization that provides meeting space for tech groups. So, I do some of my training to raise funds for it. I have also been involved in most of the WordCamps in the UK and a few other WordPress-related things in Scotland and various other places. I’m still on the old WP Hackers mailing list and make the odd contribution there, although it’s been fairly dead for a while now. I just keep myself as involved as I can.

<strong>Q:</strong> So, that’s “all” you do? [laughs]

<strong>Mike:</strong> Well, if I get the chance, I try to give back to WordPress itself. I managed to get some code into version 3.8 and 3.6. I haven’t really had the time to get involved, which isn’t a good excuse. Fingers crossed, this year I’ll make more contributions. I certainly try to keep up with what’s going on. I’m just looking for an opportunity to get more involved in the development side.

<strong>Q:</strong> Lastly, WordPress has been growing consistently over the years and shows no signs of slowing down. Why do you think WordPress is the most popular CMS? With all of the other options people have now to produce content (for example, Tumblr and Medium), what do you think it is about WordPress, both .com and .org, that keeps people interested?

<strong>Mike:</strong> I think WordPress is better for the end user than many of the others, although I know things like Tumblr are easier to use. An issue with the hosted ones — for me, anyway — is that you don’t have control. Even though WordPress.com is hosted, you have a lot more freedom than with many of the others, like Tumblr and Blogger and hosted solutions like that. It still is easy to use, and I know a lot of the others are emulating the things that WordPress does.

But also there is a fantastic community around WordPress, a community that shares and is very helpful. So, once somebody learns how good and flexible WordPress is and how they can bend it to do exactly what they need, if anyone comes to them for advice, they’re going to recommend WordPress first of all because they’ve had the experience with it and they’ve seen what it can do and it has provided solutions for them. And it grows like that. The community around it is very friendly, helpful and inclusive, first and foremost, and that comes across. Whenever someone is thinking about getting a website, if they ask enough people, several of them will recommend WordPress because they’ve had their own good experiences with it. It’s self-perpetuating, which has got to be a good thing.</p>

## Thank You

I can’t thank both Matt and Mike enough for taking the time to conduct these interviews. Their contributions to WordPress have enabled people like me to make a living from this community-based open-source platform. Mike concluded the interview by summing up what he and Matt (and I) want for the future of WordPress:
<blockquote>I remember Matt said at one point, “It would be fantastic if everybody used WordPress and nobody knew what it was, if it was just the thing you do if you do the Web.” We’ve all got televisions in our front room, and we don’t even think about how they work or how to operate them. We just use them, and they’re just there. And yeah, every now and then you’ll get a new one that’s got some new controls, but you just use it, and it’s a commodity. It would be fantastic if WordPress became like that. So, if somebody says, “I think I’ll do something on the Web,” what they end up doing is using WordPress, whether they know it or not.</blockquote>

{{< signature "al, dp, ml, il" >}}

