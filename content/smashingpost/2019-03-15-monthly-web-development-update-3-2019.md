---
title: 'Monthly Web Development Update 3/2019: React Hooks, Constructable Stylesheets, And Building Trust'
slug: monthly-web-development-update-3-2019
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d62d27-dd5e-474f-a8a7-531d0c5867c8/accessibility-insights-opt.png
date: 2019-03-15T13:13:08+01:00
summary: >-
  Staying on top of what’s happening in the web community can be hard with so much going on. Anselm’s monthly reading list gives you an overview of the most important news and articles.
description: >-
  Staying on top of what’s happening in the web community can be hard with so much going on. Anselm’s monthly reading list gives you an overview of the most important news and articles.
categories:
  - Web Development Reading List
---
Do you sometimes feel like there’s so much to read and learn that your brain can’t take it anymore? It’s something most of us experience from time to time when we have too much to do and then overload our brains with even more. I’m aware that my reading lists aren’t helpful in that regard, as they contain even more things to learn. But it’s the very reason why I try to compile a diverse, open-minded set of articles that aren’t entirely frontend- or tech-related. And in weeks like this one where there aren’t too many articles for me to summarize, I realize how relieving this can be. Let’s give our brains the chance to wind down a bit when it tells us to and use the opportunity to reconsider how we do work.

Think about **how you approach tasks**, for example. Do you ask for more details when you’re given a specific task? Do you figure out how to do it yourself? Or are you just following the task’s details? Only doing the latter will get things done, of course. But it’ll also increase the risk that you forget about necessary details, as a [study on storing passwords](https://net.cs.uni-bonn.de/fileadmin/user_upload/naiakshi/Naiakshina_Password_Study.pdf) reveals now. If there’s nothing in the task description about hashing a password, for example, many people will not apply it, even if they know it’s the better solution. Or take the process of building a website: If we forget to add the correct caching, server costs will be unnecessarily high, and performance will suffer. It’s these **little extra steps of thinking** that make the difference between good, solid work and “just getting stuff done”.

## News

- Chrome 74 brings some [new features to DevTools](https://developers.google.com/web/updates/2019/03/devtools): It now highlights all elements that are affected by a CSS property, Lighthouse 4 is integrated into the Audits panel, and a WebSocket binary message viewer has been added, too.
- Intersection Observer is still quite new and yet Chrome developers are currently introducing version 2 to tackle some common problems and implement learnings from the first version. Here’s what’s going to change in [Intersection Observer v2](https://developers.google.com/web/updates/2019/02/intersectionobserver-v2).

{{% feature-panel %}}

## General

- It’s easy to forget about it, but even today we often build non-diverse solutions in many areas of life. This article shows how that happens with [car crash test dummies that neglect women](https://www.theguardian.com/lifeandstyle/2019/feb/23/truth-world-built-for-men-car-crashes).
- Voice is becoming more and more important in our lives, mainly because we use more devices without real display interfaces today — Homepod, Alexa, Siri, Google Assistant, or Amazon Echo. Mozilla teamed up with institutes from around the world to create an [open-source pool of high-quality voices](https://voice.mozilla.org/en) that helps teach machines how real people speak.
- “In our modern world, it’s easy to junk things up. Simple is hard. We’re quick to add more questions to research surveys, more buttons to a digital interface, more burdens to people”. Kate Clayton explores [how to be an elegant simplifier](https://behavioralscientist.org/be-an-elegant-simplifier/).
- “People think that data is in the cloud, but it’s not. It’s in the ocean.” Let’s [dive deep into how communication works](https://www.nytimes.com/interactive/2019/03/10/technology/internet-cables-oceans.html) and how it came to be that Microsoft, Google, Facebook, and Amazon own more than half of the undersea bandwidth. The article shows how the Internet depends on these big four companies nowadays and that we’d face massive struggles and performance impacts if we avoided them.
- Jason Miller wrote an [introduction to rendering on the web](https://developers.google.com/web/updates/2019/02/rendering-on-the-web), summarizing what happens when a user accesses a website through a modern browser. There’s a lot to learn in here.

{{< rimg href="https://www.nytimes.com/interactive/2019/03/10/technology/internet-cables-oceans.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd147293-b242-407e-8447-b41e0699d2f1/undersea-cables-opt.png" sizes="100vw" caption="Data is not in the cloud. <a href='https://www.nytimes.com/interactive/2019/03/10/technology/internet-cables-oceans.html'>It’s in the ocean</a>. And more than half of the undersea bandwidth is owned by Amazon, Facebook, Google, and Microsoft. (<a href='https://www.nytimes.com/interactive/2019/03/10/technology/internet-cables-oceans.html'>Image credit</a>)" alt="Map of the world showing undersea internet cables in 2021" >}}

## UI/UX

- Anand Satyan explains why it’s important to [start designing without color first](https://medium.com/devsdesign/4-reasons-why-you-should-design-without-color-first-c0e38180f689). It helps you understand the structure of data and layout better and often results in cleaner, more consistent designs.
- Brad Frost wrote about the importance of providing [forms that are simple, not clever](https://bradfrost.com/blog/post/dont-get-clever-with-login-forms/), especially if you want users to log in</a>.
- Nikita Prokopov tried to analyze and [redesign Github’s repository page](https://tonsky.me/blog/github-redesign/). While I don’t like the final result too much, there are a lot of great takeaways from improving existing design patterns and the user experience with simple methods.

## JavaScript

- Addy Osmani shares a table that explains [how different methods of loading JavaScript affect loading and rendering of websites](https://addyosmani.com/blog/script-priorities/) in Chrome. And while other browsers might behave slightly differently, this table is transferable.
- Faraz Kelhini shares the latest JavaScript features that [ease the task of writing regular expressions](https://www.smashingmagazine.com/2019/02/regexp-features-regular-expressions/).
- We don’t hear a lot about integrating videos on websites efficiently. Now Oscar from Kitchen Stories shares [their approach to using HTTP Live Streaming (HLS)](https://engineering.kitchenstories.io/our-road-to-native-videos-on-the-web-22ffb807657b) and optimizing load times.
- I’m a big fan of [Filepond](https://pqina.nl/filepond/) as a JavaScript upload library, but [Uppy](https://uppy.io/) seems to be worth mentioning as an alternative as it can fetch files not only from your local disk, but also from Google Drive, Dropbox, Instagram, remote URLs, and cameras, for example.
- React Hooks are the new hot topic in the React community but [how do we write one](https://hashnode.com/post/write-your-first-react-hook-cjrt8lfci00aw18s1z8v9s06n)? Leonardo Maldonado explains.
- Ever wanted to know which element has focus? This article by Kayce Basques explains [how to use Chrome DevTools to track focus of elements](https://developers.google.com/web/tools/chrome-devtools/accessibility/focus).

## CSS

- [Constructable Stylesheets](https://developers.google.com/web/updates/2019/02/constructable-stylesheets) is a new way of initializing an external stylesheet or set of styles in a non-blocking way. This new approach allows us to dynamically construct stylesheets via JavaScript which is especially useful when we use it for Web Components in a ShadowDOM. The feature is available in Chrome Preview builds currently.
- Rachel Andrew explains how we’re going to [break boxes with the new CSS Fragmentation](https://www.smashingmagazine.com/2019/02/css-fragmentation/) specification. With CSS Fragmentation, we can do things we used to do with `float`, but it’s more flexible and helps us control page breaks and other things relevant for print or eBooks.
- [This CSS-only experiment](https://codepen.io/ivorjetski/pen/xMJoYO) is mind-blowing. I’m seriously impressed and wouldn’t have imagined that we can do something like this with CSS today.

{{% ad-panel-leaderboard %}}

## Security

- This study shows interesting insights into how engineers tackle their tasks and [why security is often so weakly implemented](https://net.cs.uni-bonn.de/fileadmin/user_upload/naiakshi/Naiakshina_Password_Study.pdf) in projects.

## Web Performance

- How much do you know about caching on the web? Harry Roberts summarized [the basic, and some extended, concepts about caching](https://csswizardry.com/2019/03/cache-control-for-civilians/). Caching can make a huge performance difference, and we all should think about it before we follow other optimization strategies.
- Matthew Ström shows [how he switched to variable fonts](https://matthewstrom.com/writing/variable-fonts.html) and what he learned along the way.
- Tim Kadlec has a lot of experience with performance budgets. Now he shares [how to work out performance budgets that stick](https://timkadlec.com/remembers/2019-03-07-performance-budgets-that-stick/).

## Accessibility

- Ben Robertson shares [five tools we can use for automated accessibility audits](https://benrobertson.io/accessibility/tools-for-website-audits). This is great because it allows us to use these tools in CIs, in regression testing (e.g., via Selenium or Chrome/Firefox headless browsers), or directly in our browsers.
- Alex Carpenter [summarized takeaways from WebAIM’s recent accessibility analysis of the top one million sites](https://alexcarpenter.me/posts/2019/03/form-inputs-unlabeled/): 59% of form inputs are unlabeled and, thus, not accessible. Making them accessible for everyone wouldn’t be hard at all. It’s as easy as wrapping the input and describing it, for example like this: `<label>Name<input name="name"></label>` Of course, there are even better labeling practices out there, but this would already be enough to make a difference for all users of a website, not only those who rely on assistive technologies.
- [Accessibility Insights](https://accessibilityinsights.io/) is a new platform service that provides developers with tools to analyze the accessibility of their web projects.

{{< rimg href="https://accessibilityinsights.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6d62d27-dd5e-474f-a8a7-531d0c5867c8/accessibility-insights-opt.png" sizes="100vw" caption="The <a href='https://accessibilityinsights.io/'>Accessibility Insights</a> extension helps you spot accessibility errors and shows how to fix them. (<a href='https://accessibilityinsights.io/'>Image credit</a>)" alt="Cartoon cat and a laptop which is running the Accessibility Insights extension" >}}

## Work &amp; Life

- [How do we build trust as leaders](https://m.signalvnoise.com/the-3-most-effective-ways-to-build-trust-as-a-leader/)? Claire Lew shares why business retreats and team building activities don’t matter much compared to the things that really make a difference: showing vulnerability, communicating the intent behind actions, and, finally, following through on commitments.
- I found this article by Sahil Lavingia, the founder of Gumroad, very insightful. In it, [he shares the failures, the struggles, and the bad decisions](https://medium.com/s/story/reflecting-on-my-failure-to-build-a-billion-dollar-company-b0c31d7db0e7) when getting Venture Capital, and why having a “normal” company is worth a thought, too, to prevent the whole thing from failing.
- Our children are technology-focused and spend a lot of time in front of screens, playing games or watching videos. Pamela Paul advocates for [letting our children get bored again](https://www.nytimes.com/2019/02/02/opinion/sunday/children-bored.html).

## Going Beyond…

- What does a public event like a concert feel like if there are no phones allowed? David Cain experienced it at a Jack White concert and is sharing the emotions, the different atmosphere, and why it’s important to think about [how we experience life with a smartphone and how without it](https://www.raptitude.com/2018/11/joy-no-phones/).
- Leo Babauta on [the issue of thinking we don’t have enough time](https://zenhabits.net/intentionally/). Spending our time intentionally and setting the right expectations is very important in our hectic lives.
- Sara Soueidan shares what led her to [leading a mostly waste-free lifestyle](https://www.sarasoueidan.com/desk/waste-free/).
- Despite climate change being a big topic now, big [tech companies are automating the crisis](https://gizmodo.com/how-google-microsoft-and-big-tech-are-automating-the-1832790799) by closing deals with fossil energy companies to place their artificial intelligence services and products.

Here’s one more thing: The periodic — yet not regular — [reminder to give something back](https://wdrl.info/donate) if you enjoy reading my writings and summary of articles.
*— Anselm*

{{< signature "cm" >}}