---
title: The Front-End Operations Engineer
slug: front-end-ops
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7afff14b-0a35-4c37-aa67-4b46c557a790/.tools-11
date: 2013-06-11T20:02:43.000Z
author: alex-sexton
description: >-
  When a team builds a complex application, there is often a common breakdown of roles. Specifically on the back end, there are database engineers, application engineers and operations engineers, or something close to this. In recent years, more and more application logic is being deferred to the client side "Front-End Ops")](https://www.smashingmagazine.com/2013/06/11/front-end-ops/).
categories:
  - Web Design
  - Workflow
  - Productivity
  - Teams
  - Business
---
When a team builds a complex application, there is often a common breakdown of roles. Specifically on the back end, there are database engineers, application engineers and operations engineers, or something close to this.

I recently wrote an article on “<a href="https://alexsexton.com/blog/2013/03/deploying-javascript-applications/">Deploying JavaScript Applications</a>.” It was largely well received, and I was happy with the content, but one negative comment stuck out to me. I probably didn’t have the reaction that the commenter was intending, but it pointed out something to me nonetheless.

<blockquote>"With all due respect, may I ask if you actually enjoy your job? I am a dev, and I do enjoy using tech to do stuff to a point. If your role is to squeeze every last second of performance out of your app, then yea, all this stuff must be cool. BUT if you are a coder doing something else and then come back to all of this as well, then wow, I don’t know how you haven’t gone mad already. I’d be sick to the stomach if I had to do all of this, in addition to my usual work."</blockquote>

See, I had written my article with a few too many assumptions. I understood ahead of time that a few of my solutions weren’t globally applicable, and that many people wouldn’t have the time or energy to implement them. What I didn’t fully grasp was how different the role in that article is from the picture that people have of a front-end developer in their head. Up to this point, a front-end developer had just the few operations duties lumped into their role, and even then, many people chose to skip those steps (that’s why Steve Souders is constantly yelling at you to make your pages faster).</p>

{{% feature-panel %}}

I think things are about to shift, and I’d (humbly) like to help guide that shift, because I think it’ll be great for the Web.</p>

## The Front-End Ops

A front-end operations engineer is not a title you’ve likely come across, but hopefully one that you will. Such a person would need to be an expert at serving and hosting front-end resources. They’d need to be pros at Grunt (or something similar) and have strong opinions about modules. They would find the best ways to piece together the parts of a Web application, and they'd be pros at versioning, caching and deployment.

A front-end operations engineer would <em>own</em> external performance. They would be critical of new HTTP requests, and they would constantly be measuring file size and page-load time. They wouldn’t necessarily always worry about the number of times that a loop can run in a second — that’s still an application engineer’s job. They own everything <em>past</em> the functionality. <strong>They are the bridge between an application’s intent and an application’s reality</strong>.

A front-end operations engineer would be very friendly with the quality assurance team, and they would make sure that "performance" is a test that comes up green. They’d monitor client-side errors and get alerts when things go wrong. They’d make sure that migrations to new versions of the application go smoothly, and they’d keep all external and internal dependencies up to date, secure and stable. They are the gatekeepers of the application.</p>

## Why?

We have reached a point where there is enough work to be done in the operations space that it often no longer serves us to have an application engineer do both jobs. When the application's features are someone's priorities, and that person has a full plate, they will typically deprioritize the critical steps in delivering their application most successfully to the end users.

Not every company or team can afford this person, but even if someone puts on the “front-end operations” hat for one day a week and prioritizes their work accordingly, users win. It doesn’t matter how many features you have or how sexy your features are if they aren’t delivered to the user quickly, with ease, and then heavily monitored. Front-end operations engineers are the <strong>enablers of long-term progress</strong>.</p>

## Builds And Deployment

If you were to ask most back-end engineers which person on their team has traditionally worried about builds and deployment, I’m sure you’d get a mixed bag. However, a very sizeable chunk of engineers would tell you that they have build engineers or operations engineers who handle these things. In that world, this often entails generating an RPM file, spinning up EC2 instances, running things through continuous integration tools, and switching load balancers over to new machines. Not all of this will necessarily go away for a front-end operations engineer, but there will be new tools as well.

Recommended reading: [How To Improve The Deployment Of WordPress Websites](https://www.smashingmagazine.com/2013/04/wordpress-deployment-survey/)

A front-end operations engineer will be a master of the build tool chain. They’ll help run and set up the continuous integration (or similar) server but, more specifically, <strong>they'll set up the testing instances</strong> that their application runs on and then, eventually, the deployment instances. They’ll integrate Git post-commit hooks into the application and run the tests (either in Node.js and PhantomJS or against something like Sauce Labs, Testling or BrowserStack) before anything gets merged into the master. They’ll need to make sure that those servers can take the raw code and, with a few commands, build up the resulting application.

This is where many people use Grunt these days. With a quick <code>grunt build</code>, these machines could be serving the built version of an application in order to enable proper testing environments. The front-end operations engineer would be in charge of much that’s behind that command as well. <code>grunt build</code> could call out to RequireJS’ r.js build tool, or a Browserify process, or it could simply minify and concatenate a list of files in order. It would also do similar things to the CSS (or your favorite preprocessed CSS dialect), in addition to crushing images, building sprites and reducing requests in any other way necessary or possible.

Front-end operations engineers would <strong>make sure that all of this stuff works on people’s local machines</strong>. A quick <code>grunt test</code> should be able to build everything locally, serve it and test it (likely with some WebDriver API-compatible server). They’d make sure that team members have the power to push their applications into the continuous integration environment and test them there. And they’d remove single points of failure from deployment (GitHub being down during launch wouldn’t scare them).

They’d facilitate internal deployments of feature branches and future release branches. They’d make sure that the quality assurance team has an easy time of testing anything and that the managers have an easy time of demoing things that aren’t ready.

They’d help build multiple versions of an application to best suit each of their core sets of users. This could mean builds for mobile or for old versions of Internet Explorer, but all of it should be relatively transparent to those who are programming against those feature, browser or device tests.

They’d facilitate the process of taking a release, building it, uploading it to a static edge-cached content delivery network, and flipping the switch to make it live. And they’d have a documented and fast roll-back mechanism in place.

Perhaps most importantly, <strong>they’d automate everything</strong>.

<a href="https://en.wikipedia.org/wiki/Rube_Goldberg_machine"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="163686" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65a1656d-8bcb-4f28-9b81-07152d56fdc0/front-end-ops-start-image-mini.jpg" alt="front-end ops start image_mini" width="500" height="294" /></a><br>
<em>(Image credits: <a href="https://en.wikipedia.org/wiki/Rube_Goldberg_machine">Rube Goldberg</a>)</em>

## Tracking Speed

The metric by which a front-end operations engineer would be judged is speed: the speed of the application, the speed of the tests, of the builds and deployment, and the speed at which other teammates understand the operational process.

A front-end operations engineer would live in a dashboard that feeds them data. Data is king when it comes to speed. This dashboard would integrate as much of it as possible. Most importantly, it would constantly be running the team's app in multiple browsers and tracking all important metrics of speed. This space currently doesn’t have a ton of options, so they’d likely set up a private cloud of WebPageTest instances. They’d put them in multiple zones around the world and just run them non-stop.

They’d run against production servers and new commits and pull requests and anything they can get their hands on. At any given point, they’d be able to tell when, where, and what the surrounding circumstances were behind a slow-down. <strong>A decrease in speed would be directly correlated to some change</strong>, whether a new server, a diff of code, a dependency or third-party outage, or something similar.

They’d have a chart that graphs the number of HTTP requests on load. They’d also have a chart that tells them the Gzip’ed and minified payload of JavaScript, CSS and images that are delivered on load. And they'd also go crazy and have the unGzip’ed payload of JavaScript so that they can measure the effect of code parsing, because they know how important it can be on mobile. They’d instrument tools like mod_pagespeed and nginx_pagespeed to catch any mistakes that fall through the cracks.

They’d be masters of the latest development and measurement tools. They’d read flame graphs and heap snapshots of their apps from their development tools (in each browser that has them). They’d measure frames per second on scrolling and animations, prevent layout thrashing, build memory profiles, and keep a constant eye on compositing, rendering and the overall visual performance of the application. They’d do all of this for desktop and mobile devices, and they’d track trends in all of these areas.

Recommended reading: [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)

They’d <strong>religiously parallelize tasks</strong>. They’d track the application via waterfalls and <code>.har</code> data to make sure that all serial operations are necessary or intentional.

They’d chart the average run time of the tests, builds and deploys. And they’d fight to keep them low. They’d chart their external dependencies in size and speed. They may not have control over slow API requests, but they’d want to be able to point to the reasons why their numbers are increasing.

They’d set an alarm if any of these numbers rose above an acceptable limit.

## Monitoring Errors And Logs

Managing logging is a critical job of a normal operations engineer. The data that is generated from running an application is vital to understanding where things go wrong in the real world. A front-end operations engineer would also instrument tools and code that allow the same level of introspection on the client side.

This would often manifest itself as an analytics tool. Application engineers would be encouraged to log important events and any errors at certain levels to a logging service. These would be appropriately filtered and batched on the client and sent back as events to an internal or external analytics-style provider. The engineer would have enough information to identify the circumstances, such as browser name and version, application deployment version, screen size and perhaps a bit of other data. (Though they’d want to avoid storing personally identifiable information here.)

Logging stack traces can be very helpful in browsers that support them. You can integrate third-party services that do this for you.

The front-end operations engineer would <strong>encourage a very small tolerance for errors</strong>. Any error that happened would be investigated and either fixed or logged differently. With the data that comes back, they should be able to visualize groups of errors by browser or by state information from the application. A threshold of errors would be allowed to occur, and when that is passed, engineers would be notified. Severities would be assigned, and people would be responsible for getting patches out or rolling back as necessary (with quick patches being heavily favored to roll backs).

Much like today’s operations people focus on the security of the systems they manage, a front-end operations engineer would have probes for XSS vulnerabilities and would constantly be looking for holes in the app (along with the quality assurance team).

A front-end operations engineer would have an up-to-date picture of the state of the application in production. This is challenging in the front-end world, because your application doesn't run on your machines — but that makes it even <em>more</em> necessary.</p>

## Keeping Things Fresh and Stable

My favorite thing that good operations people who I’ve worked with in the past were really good at was keeping things up to date. For some applications, stability and security are so deeply necessary that caution is the larger priority; but in most cases, failure to keep dependencies and environments up to date is what causes applications to get stale over time. We’ve all worked on a project that’s four years old where all of the tools are very old versions of the ones we know, and getting good performance out of it is impossible.

Recommended reading: [Are You Loosing Traffic By Poor Website Performance?](https://www.smashingmagazine.com/2010/01/page-performance-what-to-know-and-what-you-can-do/)

A front-end operations engineer would be effective at keeping dependencies up to date and at removing cruft in systems. When the next version of jQuery is released, they’d use their skills to switch out the dependency in the application to work with the new version and then test it to validate the change. They’d keep Grunt up to date (and Node.js along with it). When WebP becomes viable, they’d automate moving the application's images over to that format.

They’d work closely with the more architecture-oriented application engineers to make sure that the entire system still feels viable and is not lagging behind in any one area. They would keep on top of this stuff as often as possible. Updating a dependency here and there as you build is far easier than having a big “Update Everything” day. It encourages application developers to loosely couple dependencies and to build good, consistent interfaces for their own modules.

A front-end operations engineer makes it viable and fun to work on a project long after it’s new.</p>

## The Future

I’m sure plenty of commenters will tell me that these tasks have been going on for years, and plenty will tell me that they should be the concern of all developers on a team. I would agree with both statements. I am not introducing new concepts; I’m compiling tasks we’ve all been doing for years and giving them a name. I think this will help us build better tools and document better processes in the future.

The addition of this role to a team doesn’t absolve the other members of performance responsibilities. It’s just that right now, front-end operations are no one’s explicit priority on most of the teams that I’ve encountered, and because of that, they often get skipped in crunch time. I think there’s enough to be done, especially in the configuration and monitoring of these tools, outside of the normal job of a front-end engineer, to justify this role.

Most importantly, regardless of whether a new job comes from these tasks, or whether we solve the problem in a different way, we do all need to be conscious of the importance of solving these problems in some way. You simply can't ignore them and still achieve reliable, robust, high-experience applications. Addressing these concerns is critical to the stability and longevity of our applications and to the happiness of programmers and users.

If we build with that in mind, it helps the Web win, and we all want the Web to win.

<em>(al) (il) (ea)</em>

