---
title: 'Why Web Application Maintenance Should Be More Of A Thing'
slug: web-app-maintenance
author: darren-beale
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33a5d074-119a-4d9b-8f9b-1d73164ea20b/web-maintenance-pixabay.png
date: 2019-02-16T13:10:18+02:00
summary: >-
  Web applications require maintenance just like any other type of software, but as an industry, it is not something that we highlight enough. As a result, we are exposing our clients to a tangible risk as well as leaving money on the table.
description: >-
  Web applications require maintenance just like any other type of software, but as an industry, it is not something that we highlight enough. As a result, we are exposing our clients to a tangible risk as well as leaving money on the table.
categories:
  - Contracts
  - Maintenance
  - Software
---
Traditional software developers have been hiding a secret from us in plain sight. It’s not even a disputed fact. It’s part of their business model.

It doesn’t matter if we’re talking about high-end enterprise software vendors or smaller software houses that write the tools that we all use day to day in our jobs or businesses such as a [free syslog manager](https://papertrailapp.com/free-syslog). It’s right there front and center. Additional costs that they don’t hide and that we’ve become accustomed paying.

So what is this secret?

Well, a lot of traditional software vendors **make more money from maintaining the software that they write** than they do in the initial sale.

Not convinced?

A quick search on the term "Total Cost of Ownership" will provide you with lots of similar [definitions like this one from Gartner](https://www.gartner.com/it-glossary/total-cost-of-ownership-tco) (emphasis mine): 

<blockquote>[TCO is] <strong>the cost to implement, operate, support &amp; maintain</strong> or extend, and decommission an application.</blockquote>

Furthermore, [this paper](https://infolab.stanford.edu/pub/gio/2006/worth40.pdf) by Stanford university asserts that maintenance normally amounts to 60% to 90% of the TCO of a software product.

**It’s worth letting that sink in for a minute**. They make well over the initial purchase price by selling ongoing support and maintenance plans.

{{% feature-panel %}}

## We Don’t Push Maintenance

The problem as I see it is that in the web development industry, web application maintenance isn’t something that we focus on. We might put it in our proposals because we like the idea of a monthly retainer, but they will likely cover simple housekeeping tasks or new feature requests.

It is not unheard of to hide essential upgrades and optimizations within our quotes for later iterations because we‘re not confident that the client will want to pay for the things that we see as essential improvements.  We try and get them in through the back door. Or in other words, we are not open and transparent that, just like more traditional software, these applications need maintaining.

Regardless of the reasons why, it is becoming clear that we are storing up problems for the future. **The software applications we’re building are here for the long-term**. We need to be thinking like traditional software vendors. Our software will still be running for 10 or 15 years from now, and it should be kept well maintained.

So, how can we change this? How do we all as an industry ensure that our clients are protected so that things stay secure and up to date? Equally, **how do we get to take a share of the maintenance pie**?

## What Is Maintenance?

In their 2012 paper [Effective Application Maintenance](https://aisel.aisnet.org/cais/vol30/iss1/5/), Heather Smith and James McKeen define maintenance as (emphasis is mine):

<blockquote>Porting an application to a new server, interfacing with a different operating system, upgrading to a newer release, altering a tax table, or complying with new regulations—all necessitate application &mdash; maintenance. As a result, <strong>maintenance is focused on upgrading an application to ensure it remains productive and/or cost effective</strong>. The definition of application maintenance preferred by the focus group is &mdash; any modification of an application to correct faults; to improve performance; or to adapt the application to a changed environment or changed requirements. Thus, <strong>adding new functionality to an existing application (i.e., enhancement) is not, strictly speaking, considered maintenance</strong>.</blockquote>

In other words, maintenance is essential work that needs to be carried out on a software application so it can continue to reliably and securely function. 

It is not adding new features. It is not checking log files or ensuring backups have ran (these are housekeeping tasks). It is working on the code and the underlying platform to ensure that things are up to date, that it performs as its users would expect and that the lights stay on.

Here are a few examples:

- **Technology and Platform Changes**  
Third-party libraries need updating. The underlying language requires an update, e.g. PHP 5.6 to PHP 7.1  Modern operating systems send out updates regularly. Keeping on top of this is maintenance and at times will also require changes to the code base as the old ways of doing certain things become deprecated.

- **Scaling**  
As the application grows, there will be resource issues. Routines within the code that worked fine with 10,000 transactions per day struggle with 10,000 per hour. The application needs to be monitored, but also action needs to be taken when alerts are triggered.

- **Bug Fixing**  
Obvious but worth making explicit. The software has bugs, and they need fixing. Even if you include a small period of free bug fixes after shipping a project, at some point the client will need to start paying for these. 

## Hard To Sell?

Interestingly, when I discuss this with my peers, they feel that it is difficult to convince clients that they need maintenance. They are concerned that their clients don’t have the budget and they don’t want to come across as too expensive.

Well, here’s the thing: it’s actually a pretty easy sell. We’re dealing with business people, and we simply need to be talking to them about maintenance in commercial terms. **Business people understand that assets require maintenance** or they’ll become liabilities. It's just another standard ongoing monthly overhead. A cost of doing business. We just need to be putting this in our proposals *and making sure that we follow up on it*.

An extremely effective method is to offer a retainer that incorporates maintenance at its core but also bundles a lot of extra value for the client, things like:

- Reporting on progress vs. KPIs (e.g. traffic, conversions, search volumes)
- Limited ‘free’ time each month for small tweaks to the site
- Reporting on downtime, server updates or development work completed
- Access to you or specific members of your team by phone to answer questions

Indeed, you can make the retainer save the client money and pay for itself.  A good example of this would be a client’s requirement to get a simple report or export from the database each month for offline processing. 

You *could* quote for a number of development days to build out a &mdash; probably more complex than initially assumed &mdash; reporting user interface or alternatively point the client to your retainer. Include within it a task each month for a developer to manually run a pre-set SQL query to manually provide the same data.

A trivial task for you or your team; lots of value to your client.

### A Practical Example

You’ll, of course, have your own way of writing proposals but here are a couple of snippets from an example pitch.

In the section of your proposal where you might paint your vision for the future, you can add something about maintenance. Use this as an opportunity to plant the seed about forming a long-term relationship.

<blockquote>You are looking to minimize long-term risk.<br /><br />You want to ensure that your application performs well, that it remains secure and that it is easy to work on.<br /><br />You also understand how important maintenance is for any business asset.</blockquote>

Later on, in the deliverables section, you can add a part about maintenance either as a stand-alone option or bundled in with an ongoing retainer. 

In the following example, we keep it simple and bundle it in with a pre-paid development retainer: 

<blockquote>We strongly advocate that all clients consider maintenance to be an essential overhead for their website. Modern web applications require maintenance and just like your house or your car; you keep your asset maintained to <strong>reduce the tangible risk that they become liabilities later on</strong>.<br /><br />As a client who is sensibly keen to keep on top of the application’s maintenance as well as getting new features added, we’d suggest N days per month (as a starting point) for general maintenance and development retainer.<br /><br />We’d spread things out so that a developer is working on your system at least [some period per week/month] giving you the distinct advantage of having a developer able to switch to something more important should issues arise during the [same period]. Depending upon your priorities that time could all be spent on new feature work or divided with maintenance, it’s your call. We normally suggest a 75%/25% split between new features and important maintenance.</blockquote>

As previously mentioned, this is also a great opportunity to lump maintenance in with other value-added ongoing services like performance reporting, conducting housekeeping tasks like checking backups and maybe a monthly call to discuss progress and priorities. 

What you’ll probably find is that after you land the work, the retainer is then not mentioned again. This is understandable as there is lots for you and your client to be considering at the beginning of a project, but as the project is wrapping up is a great time to re-introduce it as part of your project offboarding process. 

Whether this is talking about phase 2 or simply introducing final invoices and handing over, remind them about maintenance. **Remind them of ongoing training, reporting, and being available for support**. Make the push for a retainer, remembering to talk in those same commercial terms: *their new asset needs maintaining to stay shiny*.

## Can Maintenance Be Annoying?

A common misconception is that maintenance retainers can become an additional burden. The concern is that clients will be constantly ringing you up and asking for small tweaks as part of your retainer. This is a particular concern for smaller teams or solo consultants.

It is not usually the case, though. Maybe at the beginning, the client will have a list of snags that need working through, but this is par for the course; if you’re experienced, then you’re expecting it. These are **easily managed by improving communication channels** (use an issue tracker) and lumping all requests together, i.e, working on them in a single hit.

As the application matures, you’ll drop into a tick-over mode. This is where the retainer becomes particularly valuable to both parties. It obviously depends on *how* you’ve structured the retainer but from your perspective, you are striving to remind the client each month how valuable you are. You can send them your monthly report, tell them how you fixed a slowdown in that routine and that the server was patched for this week’s global OS exploit.

You were, of course, also available to work on a number of new requested features *that were additionally chargeable*. From your client’s perspective, they see that you are there, they see progress, and they get to remove “worry about the website” from their list. Clearly, ‘those clients’ do exist, though, so the most important thing is to get your retainer wording right and manage expectations accordingly.

If your client is expecting the moon on the stick for a low monthly fee, push back or renegotiate. Paying you to do &mdash; say &mdash; two hours maintenance and housekeeping per month in amongst providing a monthly report and other ancillary tasks is exactly that; it’s not a blank cheque to make lots of ad-hoc changes. Remind them what is included and what isn’t. 

## How Do We Make Maintenance Easier?

Finally, to ensure the best value for your clients and to make your life easier, use some of these tactics when building your applications.

### Long-Term Support (LTS)

- Use technology platforms with well documented LTS releases and upgrade paths.
- Ongoing OS, language, framework and CMS upgrades should be expected and factored in for all projects so tracking an LTS version is a no-brainer.
- Everything should be running on a supported version. Big alarm bells should be ringing if this is not the case.

### Good Project Hygiene

- Have maintenance tasks publicly in your feature backlog or issue tracking system and agree on priorities with your client. Don’t hide the maintenance tasks away.
- Code level and functional tests allow you to keep an eye on particularly problematic code and will help when pulling modules out for refactoring.
- Monitor the application and understand where the bottlenecks and errors are. Any issues can get added to the development backlog and prioritized accordingly.
- Monitor support requests. Are end users providing you with useful feedback that could indicate maintenance requirements?

### The Application Should Be Portable

- Any developer should be able to get the system up and running easily locally &mdash; not just you! Use virtual servers or containers to ensure that development versions of the applications are identical to production.
- The application should be well documented. At a minimum, the provisioning and deployment workflows and any special incantations required to deploy to live should be written down.

## Maintenance Is A Genuine Win-Win

Maintenance is the work we need to do on an application so it can safely stand still. It is a standard business cost. On average 75% of the total cost of ownership over a software application’s lifetime.

As professionals, **we have a duty of care to be educating our clients about maintenance** from the outset. There is a huge opportunity here for additional income while providing tangible value to your clients. You get to keep an ongoing commercial relationship and will be the first person they turn to when they have new requirements.

Continuing to provide value through your retainer will build up trust with the client. You’ll get a platform to suggest enhancements or new features. Work that you have a great chance of winning. Your client reduces their lifetime costs, they reduce their risk, and they get to stop worrying about performance or security.

Do yourself, your client and our entire industry a favor: help make web application maintenance become more of a thing.

{{< signature "rb, ra, hj, il" >}}

