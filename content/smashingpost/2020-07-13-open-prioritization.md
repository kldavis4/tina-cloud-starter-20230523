---
title: 'Crowdfunding Web Platform Features With Open Prioritization'
slug: crowdfunding-web-platform-features-open-prioritization
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e2c8ffa-f900-487c-b608-4f849ffef42b/crowdfunding-web-platform-features-open-prioritization.png
date: 2020-07-13T13:00:00.000Z
summary: >-
  Rachel Andrew takes a look at a new effort to crowdfund the costs of implementing browser features.
description: >-
  Rachel Andrew takes a look at a new effort to crowdfund the costs of implementing browser features.
categories:
  - Browsers
disable_ads: true
disable_newsletterbox: true
---

[In my last post](https://www.smashingmagazine.com/2020/07/css-news-july-2020/), I described some interesting CSS features &mdash; some of which are only available in one browser. Most web developers have some feature they wish was more widely available, or that was available at all. I encourage developers to use, talk about, and raise implementation bugs with browsers to try to get features implemented, however, what if there was a more direct way to do so? What if web developers could get together and fund the development of these features?

This is the model that open-source consultancy [Igalia](https://www.igalia.com/) is launching with their [Open Prioritization experiment](https://www.igalia.com/open-prioritization/). The basic idea is a crowdfunding model for web platform features. If we want a feature implemented, we can put in a small amount of money to help fund that work. If the goal is reached, the feature can be implemented. This article is based on an interview with [Brian Kardell](https://twitter.com/briankardell), Developer Advocate at Igalia.

## What Is Open Prioritization?

The idea of open prioritization is that the community gets to choose and help fund feature development. Igalia have selected a list of target features, all of which are implemented or currently being implemented in at least one engine. Therefore, funding a feature will help it become available cross-browser, and more usable for us as developers. The initial list is:

- CSS `lab( )` colors in Firefox
- `:focus-visible` in WebKit/Safari
- HTML `inert` in WebKit/Safari
- Selector list arguments for `:not( )` in Chrome
- CSS Containment support in WebKit/Safari
- CSS `d` (SVG path) support in Firefox

[The website](https://www.igalia.com/open-prioritization/) gives more explanation of each feature and all of the details of how the funding will work. Igalia are working with Open Collective to manage the pledges.

## Who Are Igalia?

You may never have heard of Igalia, but you will have benefited from their work. Igalia works on browser engines, and have specialist knowledge of all of the engines. They had the second-highest number of commits to the Chrome and WebKit source in 2019. If you love CSS Grid Layout, then you have Igalia to thank for the implementation in Chrome and WebKit. The work to add the feature to those browsers was done by a team at Igalia, rather than engineers working internally at the browser company.

This is what makes this idea so compelling. It isn’t a case of raising some money and then trying to persuade someone to do the work. Igalia have a track record of doing the work. Developers need to be paid, so by crowdsourcing the money we are able to choose what is worked on next. Igalia also already have the relationships with the engines to make any suggested feature likely to be a success.

## Will Browsers Accept These Features If We Fund Them?

The fact that Igalia already have relationships within browser engine teams, and have already discussed the selected features with them means that if funded, we should see the features in browsers. And, there are already precedents for major features being funded by third parties and developed by Igalia. The Grid Layout implementation in Chrome and WebKit was funded by Bloomberg Tech. They were frustrated by the lack of Grid Layout implementation, and it was Bloomberg Tech who provided the money to develop that feature over several years.

Chrome and WebKit were happy to accept the implementation; there was no controversy over adding the feature. Rather, it was a matter of prioritization. The browsers had other work that was deemed a higher priority, and financial commitment and developer time was therefore directed elsewhere. The features that have been selected for this initial crowdfunding attempt are also non -controversial in terms of their implementation. If the work can be done then the engines are likely to accept it. Interoperability &mdash; things working in the same way across browsers &mdash; is something all browser vendors care about. There is no benefit to an engine to lag behind. We essentially just get to bypass the internal prioritization process for the feature.

## Why Don’t Browsers Just Do This Stuff?

I asked Brian why the browser companies don’t fund these things themselves. He explained,

<blockquote>“People might think, for example, ‘Apple has all of the money in the world’ but this ignores complex realities. Apple’s business is not their Web browser. In fact, the web browser itself isn’t a money-making endeavor for anyone. Browsers and standards are voluntary, they are a commons. Cost-wise, however, browsers are considerable. They are massively more complex than most of us realize. Only 3 organizations today have invested the many years and millions of dollars annually that it takes to evolve and maintain a rendering engine project. Any one of them is already making a massive and unparalleled investment in the commons.”</blockquote>

Brian went on to point out the considerable investment of Firefox into [Servo](https://servo.org/), and Google into [LayoutNG](https://www.chromium.org/blink/layoutng), projects which will improve the browser experience and also make it possible to implement new features of the platform. There is a lot that any browser _could_ be implementing in their engine, but the way those features are internally prioritized may not always map to our needs as developers.

It occurred to me that by funding browser implementation, we are doing the same thing that we do for other products that we use. Many of us will have developed a plugin for a needed feature in a CMS or paid a third party to provide it. The CMS developers spend their time working on the core product, ensuring that it is robust, secure, and up to date. Without the core product, adding plugins would be impossible. Third parties however can contribute parts to that platform, and in a sense that is what we can do via open prioritization. Show that a feature is worthwhile enough for us to pledge some cash to get it over the line.

## How Does This Fit With Projects Such As Web We Want?

SmashingConf has supported the [Web We Want](https://webwewant.fyi/) project, where developers pitched web platform ideas to be discussed and voted for onstage at conferences. I was involved in several of these events as a host and on the panel. I wondered how open prioritization fits with these existing efforts. Brian explained that these are quite different things saying,

<blockquote>“... if you asked me what could make my house better I could name a million things. Some of those aren’t even remotely practical, they would just be really neat. But if you said make a list of things you could do with a budget for what each one costs &mdash; my list will be considerably more practical and bound by realities I know exist.<br /><br />At the end of the month if you say "there is your list, and here is $100, what will you do with it?" that’s a very direct question that helps me accomplish something practical. Maybe I will paint. Maybe I will buy some new lighting. Or, maybe I will save it for some months toward something more costly.”</blockquote>

The *Web We Want* project asks an open question, it asks what we want of the platform. Many of the wants aren’t things that already exist as a specification. To actually start to implement any of these things would mean starting right at the beginning, with an idea that needs taking right from the specification stage. There are few certainties, and they would be very hard to put a price on.

The features selected for this first open prioritization experiment are deliberately limited in scope. They already have some implementation; they have a specification, and Igalia have already spoken to browser maintainers to check that the features are ready to work on but don’t feature in immediate priorities.

Supporting this project means supporting a concrete chunk of development, that can happen within a reasonably short timeframe. Posting an idea to Web We Want, writing up an idea on your blog, or adding an issue describing a totally new feature on the [CSSWG GitHub repo](https://github.com/w3c/csswg-drafts/issues) potentially gets a new idea out into the discussion. However, those ideas may have a long slow path to becoming reality. And, given the nature of standards discussions, probably won’t happen in exactly the way that you imagined. It is valuable to propose these things, but very hard to estimate time and costs to a final implementation.

The same problem is true for the much-wanted feature of container queries, Igalia have gone so far as to mention container queries in their FAQ. Container queries are something that many people involved in the standards process and at browser vendors are looking into, however, those discussions are at an early stage. It isn’t something it would be possible to put a monetary value on at this point.

## Get Involved!

There is more information at the [Open Prioritization](https://www.igalia.com/open-prioritization/) site, along with a detailed FAQ answering other questions that you might have. I’m excited about this because I’m always keen to help find ways for designers and developers to get involved in the web platform. It is our platform. We can wait for things to be granted to use by browser vendors, or we can actively contribute via ideas, bug reports, and with Open Prioritization a bit of cash, to help to make it better.

{{% feature-panel %}}

{{< signature "il" >}}
