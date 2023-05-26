---
title: 'CSS Frameworks Or CSS Grid: What Should I Use For My Project?'
slug: css-frameworks-css-grid
author: rachel-andrew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c78c0525-f3e8-4a1d-a8c0-d85e20971dfd/rachel-new-css-framework-or-css-grid-what-should-i-use.png
date: 2018-11-09T12:30:30+02:00
summary: >-
  Have you ever considered whether CSS Grid can actually replace the need for CSS frameworks or third-party component libraries? In doing so, Rachel Andrew discovered a range of reasons people use a third-party framework and the positive and negative things about doing so.
description: >-
  Have you ever considered whether CSS Grid can actually replace the need for CSS frameworks or third-party component libraries? In doing so, Rachel Andrew discovered a range of reasons people use a third-party framework and the positive and negative things about doing so.
categories:
  - CSS
  - Frameworks
---
Among the questions I am most frequently asked is some variety of the question, "Should I use CSS Grid or Bootstrap?" In this article, I will take a look at that question. You will discover that the reasons for using frameworks are varied, and not simply centered around use of the grid system contained in that framework. I hope that by unpacking these reasons, I can help you to make your own decision, in terms of what is best for the sites and applications that you are working on, and also for the team you work with.

In this article when I talk about **a framework**, I’m describing a third party CSS framework such as Bootstrap or Foundation. You might argue these are really component libraries, but many people (including their own docs) would describe them as a framework so that is what we will use here. The important factor is that these are something developed externally to you, without reference to your specific issues. The alternative to using a third party framework is to write your own CSS &mdash; that might involve developing your own internal framework, using a bunch of common files as a starting point, or creating every project as a new thing. All these things are done in reference to your own specific needs rather than very generic ones.

## Why Choose A CSS Framework?

The question of whether to use Grid or a framework is flawed, as CSS Grid is not a drop-in replacement for the things that a CSS framework does. Any exploration of the subject needs to consider what of our framework CSS Grid is going to replace. I wanted to start by finding out why people had chosen to use a CSS framework at all. So I turned to Twitter and posted this tweet.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">A question: if you have chosen to use a CSS framework (Bootstrap, Foundation etc.) for your project, what were the main reasons for doing so?</p>&mdash; Rachel Andrew (@rachelandrew) <a href="https://twitter.com/rachelandrew/status/1052133688614576128?ref_src=twsrc%5Etfw">October 16, 2018</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

There were _a lot_ of responses. As I expected, there are far more reasons to use a framework than simply the grid system that it contains. 

{{% feature-panel %}}

### A Framework Gives Your Team Ready Made Documentation

If you are working on a project with a number of other developers then any internal system you create will need to also include documentation to help your team members use it effectively. Creating useful documentation is time-consuming, skilled work in itself, and something that the big frameworks do very well.

{{< rimg  breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b850a48a-e888-4a42-a6a6-c4a021558941/bootstraps-docs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b850a48a-e888-4a42-a6a6-c4a021558941/bootstraps-docs.png" sizes="100vw" caption="The Bootstrap Documentation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b850a48a-e888-4a42-a6a6-c4a021558941/bootstraps-docs.png'>Large preview</a>)" alt="Screenshot of the Bootstrap documentation homepage" >}}

Framework documentation came up again and again, with many experienced front-end developers chipping in and explaining this is why they would recommend and use a CSS framework. I sometimes hear the opinion that people are using frameworks because they don’t really know CSS, many of the people replying, however, are well known to me as expert CSS developers. I’m sure that they are sometimes frustrated by the choices made by the framework, however, the positive aspects of that choice outweigh that.

### Online Communities: Easy Access To Help

When you decide to use a particular tool, you also gain a community of users to ask for help. Unless you have a very clear CSS issue, and can produce a reduced use case to demonstrate it, asking for help with CSS can be difficult. It is especially so if you want to ask how to approach building a certain component. Using a framework can give you a starting point for your question; in general, you will be asking how to modify or style a particular component rather than starting from scratch. This is an easier thing to ask, as well as an easier thing to answer.

{{% ad-panel-leaderboard %}}

### The Grid System

Despite the fact that we have CSS Grid, many people replied that the main reason they decided to use a framework was for the grid system. Of course, many of these projects may have been started a long time before CSS Grid was available. Even today, however, concerns about backwards compatibility or team understanding of newer layout methods might cause people to decide to use a framework rather than adopting native CSS.

### Speed Of Project Delivery

<blockquote class="twitter-tweet" data-conversation="none" data-lang="en"><p lang="en" dir="ltr">when having a unique design and efficient css were a much lower priority than the due date</p>&mdash; CodingBlocks.net (@CodingBlocks) <a href="https://twitter.com/CodingBlocks/status/1052165704445829121?ref_src=twsrc%5Etfw">October 16, 2018</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Opting for a framework will, in general, make it far quicker to deliver your project, in particular if that project fits very well with the way the framework does things and doesn’t need a lot of customization.

In the case of developing an MVP for a new idea, a framework may well be an excellent choice. You will have many things to spend time on, and be still testing assumptions in terms of what the project needs. Being able to develop that first version using a framework can help you get the product in front of users more quickly, and save burning up a lot of time developing things you then decide not to use.

<blockquote class="twitter-tweet" data-conversation="none" data-lang="en"><p lang="en" dir="ltr">I go with a framework on anything that’s an MVP &mdash; minimal dev effort on tooling and frameworks to optimise for time working on the actual concept.<br><br>I make my own CSS “framework” on anything that’s a redo of an existing large-scale site/app.</p>&mdash; Ben Bodien (@bbodien) <a href="https://twitter.com/bbodien/status/1052134529362788353?ref_src=twsrc%5Etfw">October 16, 2018</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Another place where speed and a bunch of ready built components can be very useful is when developing the backend admin system for a site or application. In the case where you simply need to create a few admin screens, a framework can save a lot of time styling form fields and other components! There are even dashboard themes for Bootstrap and Foundation that can give a helpful starting point.

{{< rimg  breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b33cdffb-5792-4db7-a543-370154e97a00/foundation-dashboard.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b33cdffb-5792-4db7-a543-370154e97a00/foundation-dashboard.png" sizes="100vw" caption="Collections of dasboard components make it quicker to build out the admin for an app. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b33cdffb-5792-4db7-a543-370154e97a00/foundation-dashboard.png'>Large preview</a>)" alt="Screenshot of a dashboard kit for Foundation" >}}

### I’m Not A Designer!

This point is the reason I’ve opted for a CSS framework in the past. I’m not a designer, and if I have to both design and build something, I’ll spend a long time trying to make design decisions I am entirely unqualified to make. It would be lovely to have the funds to hire a designer for every side project, however, I don’t, and so a framework might mean the difference between shipping the thing and not.

{{% ad-panel-leaderboard %}}

### Dealing With CSS Bugs And Browser Compatibility Issues

Mentioned less than I thought it might be was the fact that the framework authors would already have dealt with browser issues, be that due to actual bugs or lack of support for certain features. However, this was still a factor in the decision-making for many people.

### To Help With Responsive Design

<blockquote class="twitter-tweet" data-conversation="none" data-lang="en"><p lang="en" dir="ltr">Responsiveness of web pages . I found it difficult for me to decide breakpoints for web pages.</p>&mdash; Faisal Ali (@f_a_akhtar) <a href="https://twitter.com/f_a_akhtar/status/1052985976836911104?ref_src=twsrc%5Etfw">October 18, 2018</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This came up a few times; people were opting for a framework specifically due to the fact it was responsive, or that I made decisions about breakpoints for them. I thought it interesting that this specifically was something called out as a factor in choosing to use a framework.

## Why Not Use A Framework?

Among positive reasons why frameworks had been selected were some of the issues that people have had with that choice.

### Difficulty Of Overriding Framework Code

Many people commented on the fact that it could become difficult to override the code used in the framework, and that frameworks were a good choice if they didn’t need a lot of overriding. The benefits of ease of use, and everyone on the team understanding how to use the framework can be lost if there are then a huge number of customizations in place.

### All Websites End Up Looking The Same

The blame for all websites starting to look the same has been placed squarely at the door of the well known CSS frameworks. I have seen sites where I am sure a certain framework has been used, then discover they are custom CSS, so prevalent are the design choices made in these frameworks.

The difficulty in overriding framework styles already mentioned is a large part of why sites developed using a particular framework will tend to look similar. This isn’t just a creative issue, it can be very odd as a user of a few websites which have all opted for the same framework to feel that they are all the same thing. In terms of conveying your brand, and making good user experience part of that, perhaps you lose something when opting for the generic choices of a framework.

### Inheriting The CSS Problems Of The Entire World

Whether front or back-end, any tool or framework that seeks to hit the mainstream has to solve as many problems as possible. Unless the tool is tightly coupled to solving one particular use-case it is going to contain a lot of very generic code, and code which solves problems that you do not have, and will never have.

You may be in the fortunate position of only needing your full experience to be viewed in the most current browsers, allowing for a more limited experience in Internet Explorer, or older versions of Chrome. Using a framework with lots of built-in support going back to IE9 would result in lots of additional code &mdash; especially given the improvements in CSS layout recently. It might also prevent you from being creative, as everything in the framework is assuming this requirement for support. Things which are possible using CSS may well be limited by the framework.

As an example, the grid systems in popular frameworks do not have an ability to span rows, as there isn’t any concept or rows in layout systems prior to Grid Layout. CSS Grid Layout easily allows for this. If you are tied to the Bootstrap Grid and your designer comes up with a design that includes elements which span rows, you are left unable to implement it &mdash; despite the fact that Grid might be supported by your target browsers.

### Performance Issues

Related to the above are performance issues inherent in using fairly generic code, rather than something optimized for the exact use cases that you have. When trying to improve performance you will find yourself hitting up against the decisions of the framework.

### Increased Technical Debt

<blockquote class="twitter-tweet" data-conversation="none" data-lang="en"><p lang="en" dir="ltr">Speed, mainly, though we quickly found out it was a bit of a false economy because it created substantial technical debt in the long run.</p>&mdash; Tim Cthulhuegdon (@nefarioustim) <a href="https://twitter.com/nefarioustim/status/1052134084640694272?ref_src=twsrc%5Etfw">October 16, 2018</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

While a framework might be a great way to get your startup quickly off the ground, and at the time of making that decision you are sure that you will replace it, is there a plan to make that happen? 

### Learning A Framework Rather Than Learning CSS

When talking to conference and workshop attendees, I have discovered that many people have only ever used a framework to write CSS. There is nothing wrong with coming into web development via one of these tools, given the complexity of the web platform today I imagine that will be the route in for many people. However, it can become a career-limiting choice, especially if the framework you based your skills around falls out of favor.

Having front-end developers without CSS knowledge should worry a company. It makes it incredibly hard to move away from that framework if your team doesn’t actually understand how to do CSS without it. While this isn’t really a reason not to use a framework, it is something to bear in mind when using one. When the day comes to move away you would hope that the team will be ready to take on something new, not needing to remember (or learn for the first time) how to write CSS!

### The Choice Doesn’t Consider End Users

Nicole Sullivan asked [pretty much the same question](https://mobile.twitter.com/stubbornella/status/1050119577823113216) a few days prior to my question as I was thinking about writing this article, although she was considering front-end frameworks as a whole rather than just CSS frameworks. [Jeremy Keith noted that precisely zero of the answers concerned end users](https://adactio.com/links/14430). This was also the case with the responses to my question.

In our race to get our site built quickly, our desire to make things as good as possible for ourselves as the designers and developers of the site, do we forget who we are doing this for? Do the decisions made by the framework developer match up with the needs of the users of the site you are building?

{{% ad-panel-leaderboard %}}

## Can We Replace Frameworks With “Vanilla” CSS?

If you are considering replacing your framework or starting a new project without one, what are some of the things that you could consider in order to make that process easier? 

### Understand Which Parts Of The Framework You Need

If you are replacing the use of a framework with your own CSS, a good place to start would be to audit your use of the current framework. Work out what you are using and why. Consider how you will replace those things in the new design.

You could follow a similar process when thinking about whether to select a framework or write your own. What parts of this could you reasonably expect to need? How well does it fit with your requirements? Will there be a lot of code that you import, potentially ask visitors to download, but never make use of?

### Create A Documented Pattern Library Or Style Guide

I am a huge fan of working with pattern libraries and you can read my post here on Smashing Magazine about [our use of Fractal](https://www.smashingmagazine.com/2018/07/pattern-library-first-css/). A pattern library or a style guide enables the creation of documentation along with all of your components. I start all of my projects by working on the CSS in the pattern library.

You are still going to need to write the documentation, as someone who writes documentation, however, I know that often the hardest thing is knowing where to start and how to structure the docs. A pattern library helps with this by keeping the docs along with the CSS for the component itself. This approach can also help prevent the docs becoming out of date as they are tightly linked to the component they refer to.

### Develop Your Own CSS Code Guidelines

Consistency across the team is incredibly useful, and without a framework, there may be nothing dictating that. With newer layout methods, in particular, there are often several ways in which a pattern could be built, if everyone picks a different one then inconsistencies are likely to creep in.

### Better Places To Ask For Help

Other than sending people in the direction of Stack Overflow, it seems that there are very few places to ask for help on CSS. In particular there seem to be few places which are approachable for beginners. If we are to encourage people away from third-party tools then we need to fill that need for friendly, helpful support which comes from the communities around those tools.

Within a company, it is possible that more experienced developers can become the CSS support for newer team members. If moving away from a framework to your own solution, it would be wise to consider what training might be needed to help bridge the gap, especially if people are used to using the help provided around the third party tool when they needed help in the past.

### Style Guides Or Starting Points For Non-Designers

I tie myself in knots with questions such as, "Which fonts should I use?", "How big should the headings be in relationship to the body text?", "Is it OK to use a drop shadow?" I can easily write the CSS &mdash; if I know what I’m trying to do! What I really need are some rules for making a not-terrible design, some kind of typography starting point, or a set of basic guidelines would replace being able to use the defaults of a framework in a lot of cases.

### Educating People About The State Of Modern Browser Interoperability

I have discovered that people who have been immersed in framework-based development for a number of years, often have a view of browser interoperability which is several years out of date. We have never been in a better situation in terms of CSS working cross-browser. It may be that some browsers don’t support one new shiny bit of CSS, but in general, CSS (when supported) won’t be full of strange bugs. For example, in almost all cases if you use CSS Grid in one browser your CSS will work in exactly the same way in another.

If trying to make a case for not using a framework to team members who believe that the framework saves them from browser bugs, this point may be a useful one to raise. Are the browser compatibility problems real, or based on the concerns of the past?

## Will We See A New Breed Of Frameworks?

Something that interests me is whether our new layout methods will help usher in a new breed of tools and frameworks. Will we see tools which take advantage of new layout methods, allow for more creativity but still give teams and individuals some of the undeniable advantages that came out of the responses to my tweet.

Perhaps by relying on new layout methods, rather than an inbuilt grid system, a new-style framework could be much lighter, becoming a collection of useful components. It might be able to then get away from some of the performance issues inherent in very generic code.

An area a framework could help with would be in helping to create solid fallbacks for browsers which don’t support newer layout methods, or by having really solid accessibility baked into the components. This could help provide guidance into a way of working that considers interoperability and accessibility, even for those people who don’t have these things in the forefront of their minds.

I don’t think that simply switching the Bootstrap Grid for CSS Grid Layout will achieve this. Instead, authors coming up with new frameworks, should perhaps look at some of the reasons outlined here, and try to solve them in new ways, using the new functionality we have in CSS to do that.

## Should *You* Use A Framework?

You and your team will need to answer that question yourself. And, despite what people might try to have you believe, there is no universal right or wrong answer. There is only what is right or wrong for your project. I hope that this article and the many responses to my original question might give you some things to discuss as you ponder that question.

Remember that the answer will change over time. It might be a useful thought experiment to not only consider what you need right now, in terms of initially doing the development for the site, but consider the lifespan of the site. Do you expect this still to be around in five years? Will your choice be a positive or negative one then?

Document your decisions, don’t be afraid to revisit them, and do ensure that you and your team maintain your skills outside of any framework that you decide to use. That way, you will be in a good place to move on in future and to make the best decisions for the next phases of your project.

I’d love the conversation started in that tweet to continue. Let us know your stories in the comments &mdash; they may well help other folks trying to work out what is best for their projects right now.

{{< signature "il" >}}