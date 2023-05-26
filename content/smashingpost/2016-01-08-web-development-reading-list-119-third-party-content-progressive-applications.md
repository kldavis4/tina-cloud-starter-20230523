---
title: >-
  'Web Development Reading List #119: Bulletproof Third-Party Content and
  Progressive Applications'
slug: web-development-reading-list-119-third-party-content-progressive-applications
image: "https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9fcd908-2f32-450a-87d0-c5b14e4867ee/mars-journeys.jpg"
date: 2016-01-08T20:20:25.000Z
author: anselm-hannemann
summary: >-
  What’s going on in the industry? What new techniques have emerged recently? What insights, tools, tips and tricks is the web design community talking about? Anselm Hannemann is collecting everything that popped up over the last week in his web development reading list so that you don’t miss out on anything. The result is a carefully curated list of articles and resources that are worth taking a closer look at.
description: >-
  This list of articles gather information about the Web Development industry, Web Development tools and Web Design insights, tools, tips and tricks.
categories:
  - Web Development Reading List
  - Coding
  - Tools
---

I wish you a happy New Year! But although we write another number now &mdash; 2016 &mdash; your habits and goals won’t change overnight. That is why I’m **not convinced of New Year’s resolutions**. You should have goals, resolutions and you should try to improve yourself.

But bear in mind to make these goals reasonable, actually _achievable_ for you, and **re&ndash;iterate in smaller periods than just once a year**. I think that works way better than having one large resolution and then feeling bad because, of course, you failed to reach your big goal. Make the small things count and improve in small steps!

## News

- This week, IPv6 is twenty years old and [it celebrates its birthday with a global share of 10%](https://arstechnica.com/business/2016/01/ipv6-celebrates-its-20th-birthday-by-reaching-10-percent-deployment/). It’s incredible how slow the usage of IPv6 has spread but for two years now we have been seeing a growing adoption of the technology and I’m delighted to see how it will develop over the next two years.
- Finally, Amazon [Cloudfront now supports gzipping](https://aws.amazon.com/blogs/aws/new-gzip-compression-support-for-amazon-cloudfront/) text and binary content. You can and _should_ enable it right now if you serve such files over the service.

<figure><a href="https://arstechnica.com/business/2016/01/ipv6-celebrates-its-20th-birthday-by-reaching-10-percent-deployment/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feca301c-1e6a-488a-bac5-1c6a7a464c7a/ipv6-adoption-opt.png" width="434" height="243" alt="World Map highlighting the USA in green bright with a label stating that the IPv6 Adoption is 24.41%, the Latency is 10ms and the Impact is 0.08%" /></a><figcaption>The adoption of the IPv6 technology is growing, albeit slowly, <a href="https://arstechnica.com/business/2016/01/ipv6-celebrates-its-20th-birthday-by-reaching-10-percent-deployment/">reaching 10% in January</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feca301c-1e6a-488a-bac5-1c6a7a464c7a/ipv6-adoption-opt.png">Large preview</a>)</figcaption></figure>

{{% feature-panel %}}

## General

- Really, if you only read one thing this week about web development, let it be this transcript of Maciej Ceglowski’s talk “[The Website Obesity Crisis](https://idlewords.com/talks/website_obesity.htm)” or [watch the talk](https://vimeo.com/147806338).
- Stephen Hay writes about best practices featured in blog articles and why reality is often very different, requiring us to be more pragmatic and less idealistic. [The reality is sometimes messy](https://www.the-haystack.com/2016/01/05/reality-is-messy/), not all people can spend days optimizing the smallest details.
- Everybody who has ever linked to a third party and checked the health of links from time to time knows the issue: broken links. And we still change URLs or remove resources (yes, I did this myself a couple of times) without sending a proper redirect or notice to the user. We do that despite knowing that [the hyperlink is one of the most important parts of the web](https://aworkinglibrary.com/writing/hypertext-for-all/). I think this is also a good place to [remind you of this article](https://medium.com/matter/the-web-we-have-to-save-2eb1fe15a426), too.

## Concepts & Design

- Troy Hunt complains that in 2016, [websites still fail on basic user experiences](https://www.troyhunt.com/2016/01/its-2016-already-how-are-websites-still.html) and, instead, take over the user’s screen with newsletter subscriptions, surveys, multi&ndash;part articles, password restrictions, popover ads, cookie warnings and scroll&ndash;jacking.

## Tools

- Working with npm? Then you’re probably annoyed by installing dependencies over and over again over the network. Fortunately, there is a second option that lets you [use many features of npm offline](https://addyosmani.com/blog/using-npm-offline/). Addy Osmani explains what you need to do to use it.

## Security

- There is a common misunderstanding of services like Cloudflare or CDNs regarding the way they handle HTTPS. [I wrote an article why it’s wrong to think your website data is secured](https://helloanselm.com/2016/choose-your-own-https/) when you use HTTPS provided by Cloudflare and what privacy implication the usage of a CDN usually has.
- How lazy authentication can lead you to you being associated with, well, terrorism is being [described in this article by Brian Krebs](https://krebsonsecurity.com/2015/12/2016-reality-lazy-authentication-still-the-norm/) whose PayPal account has been taken over. We should really aim for the best authentication method available for the products we build.

{{% ad-panel-leaderboard %}}

## Web Performance

- If you include a third-party script, you should always be aware of its consequences. As you don’t control the resource but [often rely on it](https://helloanselm.com/2015/see-the-progress/), you should spend some time thoroughly considering whether it’s worth implementing it, what happens if the script is not available on the remote server any longer and, more specifically, whether your application will still work in such cases. Tammy Everts shares a couple of [tips to consider when you include a third party script](https://www.soasta.com/blog/10-pro-tips-for-managing-the-performance-of-your-third-party-scripts/). Lots of great advice regarding advertising scripts, their ROI, caching methods, and how to detect malicious changes in such scripts.
- Web app loading times are a problem. Gleb Bahmutov has published an article describing [what you can do to show the user a nearly instant application state](https://glebbahmutov.com/blog/run-express-server-in-your-browser/) by using Service Workers. Furthermore, a small addition shows how you can run the Express server in the browser with Service Workers.

## HTML / SVG

- Ian Devlin’s new article “[On Accessibility and the Lack of Proper HTML](https://www.iandevlin.com/blog/2016/01/opinion/on-accessibility-and-the-lack-of-proper-html)” points out the problem of why we have so few websites and applications that actually have the basic principles of proper HTML incorporated, with accessibility suffering as a result.
- Andreas Larsen shares a 2½&ndash;article series on how to optimize SVGs for the use on the web: [The first steps](https://medium.com/@larsenwork/optimising-svgs-for-web-use-part-1-67e8f2d4035#.7rx09etiw), [a deeper dive into SVG](https://medium.com/@larsenwork/optimising-svgs-for-web-use-part-2-6711cc15df46#.sr1x89hsv), and how to [drastically optimize an existing logo](https://medium.com/@larsenwork/optimising-svgs-for-web-use-part-2-1-598815d74f9c#.ws158y36v).

## Accessibility

- [An overview of free tools you can use to make sure your website is accessible](https://medium.com/bread-crumbs/free-web-accessibility-tools-round-up-b83a33797789). A short introduction that helps you to test your application or site easily.

## JavaScript

- [Reimagining Single-Page Applications With Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/) provides you with a different view on how to write web applications in a better way. And Addy Osmani gives you some [interesting ideas on how to progressively enhance web apps](https://addyosmani.com/blog/getting-started-with-progressive-web-apps/) these days.

## CSS / Sass

- For many people, CSS Blend Modes are still not very well-known. Justin McDowell explains [how the different modes work](https://alistapart.com/article/blending-modes-demystified), what effects you can achieve with them and the remaining (and new) problems you have to deal with.

{{% ad-panel-leaderboard %}}

## Work & Life

- Even with a strong repertoire of techniques for making each hour count more, you will still fail regularly. What matters is [increasing the aggregate quality of your hours](https://m.signalvnoise.com/manufacturing-quality-time-fe043fa7b7a1) over the long term, not to stress when you fail to turn out a perfect build.
- Dann Petty, designer and founder of the Epicurrence conference, gives us some [life guidance on how to stay creative](https://blog.crew.co/dann-petty-interview/), productive and to reflect on what really matters in your life.
- An article outlining [why people leave a company, what makes people happy at a job](https://randsinrepose.com/archives/shields-down/) and how companies and employees can make a job a great experience for everybody.
- “Why can I hit deadlines imposed by others, but not those imposed by myself?” &mdash; [Ian Feather raises this question](https://ianfeather.co.uk/communal-momentum-and-accountability/) and tries to find an answer and an approach on how to fix this human behavior.

## Go beyond…

- In California, [a massive methane leak](https://www.nytimes.com/2016/01/07/us/california-governor-declares-emergency-over-los-angeles-gas-leak.html) has been happening since October and it’s as bad as the BP oil spill a few years ago. In fact, the daily leakage has the same 20&ndash;year climate impact as driving 7 million cars a day. And it’s yet to see [if the leak can be fixed](https://www.latimes.com/local/california/la-me-porter-ranch-delay-20160102-story.html) by March, 2016. Gosh, this is bad and I still can’t believe it’s only covered so little in the media.
- Paul Krugman has a good column on [privilege, pathology, and power](https://www.nytimes.com/2016/01/01/opinion/privilege-pathology-and-power.html). It’s been proven that extreme wealth can be bad for your soul. But it also affects other people, governments due to bad decisions and our mind which worries more about saving taxes than about other people or laws.
- SpaceX, the space company by Elon Musk, has created [some beautiful posters](https://twitter.com/jordanmoore/status/685400505095471104/photo/1) advertising traveling to Mars as a tourist destination.

<figure><a href="https://twitter.com/jordanmoore/status/685400505095471104/photo/1"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9fcd908-2f32-450a-87d0-c5b14e4867ee/mars-journeys.jpg" width="500" height="750" alt="Mars Journeys illustration with an astronaut flying on a jetpack in Mars" /></a><figcaption>SpaceX, the space company by Elon Musk, has created <a href="https://www.flickr.com/photos/spacexphotos/17071818163/in/photostream/">some beautiful posters</a> advertising traveling to Mars as a tourist destination. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9fcd908-2f32-450a-87d0-c5b14e4867ee/mars-journeys.jpg">Large preview</a>)</figcaption></figure>

And with that I’ll close for this week. In case you like what I write each week, please [support me with a donation](https://wdrl.info/donate)or share this resource with other people. You can learn more [about the costs of the project here]("https://wdrl.info/costs/"). It’s available via E&ndash;Mail, RSS and online.

_Thanks and all the best,
Anselm_

### Further Reading on Smashing Magazine:

- “[Facing Failure: Tips For Handling A Failed Web Project](https://www.smashingmagazine.com/2014/11/facing-failure-tips-handling-failed-web-project/),” Jeremy Girard
- “[The More You Fail, The Greater Your Success: A Case Study](https://www.smashingmagazine.com/2014/12/the-more-you-fail-the-greater-your-success/),” Matt Reamer
- “[Lessons Learned After Shutting My Startup](https://www.smashingmagazine.com/2015/11/lessons-learned-shutting-startup/),” Yaakov Karda
- “[How Limitations Led To My Biggest App Store Success and Failure](https://www.smashingmagazine.com/2014/07/my-biggest-app-store-success-and-failure/),” Ben Johnson

{{< signature "nl" >}}
