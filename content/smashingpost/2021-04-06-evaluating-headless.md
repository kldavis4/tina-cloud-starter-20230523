---
title: 'Don’t Lose Your Head: Evaluating Headless'
slug: evaluating-headless
author: david-eglin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b748342e-9555-4f02-83c6-82589729d760/cms-options.png
date: 2021-04-06T16:10:00.000Z
summary: >-
  With the explosion in popularity of the Jamstack has come the proliferation of new options for managing your content. [Headless](/2021/03/going-headless-use-cases/) has become quite the hot topic in development circles of late, but where do you start if you are embarking on a new project and haven’t yet decided where to store and organize your content?
description: >-
  With many options comes many decisions, and it is easy to drown in all the many benefits of  headless CMS. How do we approach evaluating these options? Let’s figure it out.
categories:
  - CMS
  - Headless
  - Jamstack
  - Workflow
  - Guides
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Storyblok
  link: https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=evaluating-headless
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb5f98-1b75-4f2a-9e13-b5a2fbe1a71d/storyblok-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=evaluating-headless">Storyblok</a>, a friendly headless CMS with a visual editor, nested components and customizable content blocks for websites and apps. <em>Thank you!</em>
---

With many options comes many decisions, and it is easy to drown in all the many and various stated benefits of the different systems. So how do you approach evaluating these options? Two weeks ago, Aaron Hans shed light on the [use cases of going headless and what it is good for](https://www.smashingmagazine.com/2021/03/going-headless-use-cases/) here on Smashing Magazine. Today, I’ll give you a little bit of a primer on the CMS landscape, as well as some questions to ask to aid you in making a decision.

## Headless? What?

Headless content management is the practice of decoupling your content management system (CMS) from your front-end. Unlike with traditional (or “monolith”) systems, the CMS is not directly responsible for powering the web front-end. Instead, content is served to the front end from a remote system by way of an API, and the front-end consumes this data to render its pages. This can occur either at **run-time** (when a user lands on your website), or at **build-time** (content gets pre-rendered and generated in advance), but the important concept here is the separation between content and presentation layers.

If you’re planning to create a site using the Jamstack, you’re going to end up heading in this direction by default, but the approach is just as valid for other kinds of projects, using server-side languages such as PHP, .Net, or Ruby.

## But Why Is This Even A Thing?

Headless came about originally as a way to manage content for the Jamstack (before Jamstack got its snazzy name), but the approach has garnered fans for a lot of reasons. Headless content management allows us to deploy content to different platforms, so you can use content from your website in a native mobile app, for example.

Headless also allows us to **patch up shortcomings** in other systems. For example, Shopify. Whilst great at what it does, it isn’t the most flexible system when it comes to managing content for your online store. Using a headless CMS, we can remotely manage additional content for a Shopify site and bring more power and flexibility than we would have by default.

I recently worked on a project doing exactly this &mdash; extending the content that Shopify provides with additional, richer content from a headless CMS (we happened to use Contentful for this particular project, but any headless CMS could do this job). Using a headless content management solution allowed us to **create custom data structures** that we could tailor to our needs. For instance, the client wanted to highlight the ingredients they used in the making of their products, and Shopify doesn’t really provide a good way to manage this. We created a new content type in Shopify and allowed that to be added to a custom product page full of other types of content we created.

Shopify content was pulled through and synced to Contentful, and this became the primary data driver for the site, with the Shopify APIs only really getting involved for stock level checks and basket creation. Being able to add this kind of rich data to a SaaS-based eCommerce site was incredibly powerful.

We happened to achieve this result using Nuxt to build the site, but we could equally have chosen to integrate data from the CMS directly within the Shopify templates. **Jamstack** was chosen as the better approach here, but headless is flexible enough that it can be used almost anywhere. So long as you have access to some kind of scripting through JavaScript or a more traditional back-end language such as PHP or .Net, you can integrate headless into your workflow.

Decoupling your content from your presentation layer can be really powerful. Allowing your content to plug in to different platforms and presentation layers helps keep your content consistent across your touchpoints, and it helps make sure that your content doesn’t get fragmented across a bunch of different systems managed by different teams.

Imagine you have a product that you want to talk about on your website, in a mobile app and also in programatic ads. With headless, you could have **one central content repository** and deploy the same content (or aspects of it) to all of these platforms and more. With more traditional content management, you would need to manage the content for different platforms separately.

{{< rimg breakout="true" href="https://jamstack.org/headless-cms/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b748342e-9555-4f02-83c6-82589729d760/cms-options.png" width="721" height="333" sizes="100vw" caption="Where do you even start? There are plenty of options for headless CMS. <a href='https://jamstack.org/headless-cms/'>Headless CMS</a> helps you make your choice." alt="" >}}

## This Sounds Great! So Is Headless Right For Me?

There are a bunch of things to consider when choosing your approach. There are benefits to going headless, but there are costs as well. Here are some questions to ask yourself when considering headless as an approach:

### Are You Comfortable With The Knowledge Requirements Of Making The Split?

A lot of people think that moving to headless can “get rid” of the need for back-end developers, but the truth is that the mindset to **structure data effectively** and build content models that work and scale well is still very different from the mindset needed to be a great front-end developer much of the time. There is still a knowledge gap and that will still need to be filled.

If you’re dealing with a project of significant scale, you’re still probably going to want some developers to focus on the “back end” areas, and some to focus on the “front end”. The divisions are finer and more malleable in headless land, but don’t labor under the false assumption that you can halve your development workforce just by going headless.

### Do You Know The Total Cost Of Ownership?

Whilst headless can often prove cheaper than a monolith, the SaaS nature of most of these systems can mean that for large, rapidly changing datasets, or very large teams, the costs may not add up. Always check how the costs scale, and what that scaling is based on. Some vendors scale based on **data volume**, some on **number of API requests**, and some on **number of collaborators** editing your content. The combination of these can have a dramatic effect on how your costs grow with scale.

You will also likely need to look at multiple different platforms to formulate an idea of your total cost of ownership. If you aren’t getting search “out of the box”, you’ll need to consider how much it will cost you to add that feature. You can usually predict how these costs will scale, and you can often start out small, but it’s worth being aware of what these things might cost you in the long run.

Also keep a close eye on your **build minutes** if you do choose to go headless: these can mount up quickly, especially in the development and content population phases. Be aware that, if you choose to staticly generate your site, then you will require a build after each publish action from the CMS. With large sites, these builds can take a while, so its worth keeping in mind that these will need to be kept in check. Many of the popular static hosting services (such as Netlify and Vercel) support build asset caching and, in combination with modern frameworks enabling incremental builds, this can help mitigate this increasing cost, but you still need to keep an eye on it and do your research to ensure you don’t get caught out.

### Have You Explained It Well Enough For Your Client?

You might love the developer experience of working with the Jamstack and headless, but when making these evaluations, you must keep in mind that the clients are the ones who have to use and live with the solutions you put together, so you’ll want to try to make their lives as easy as possible.

In a previous role, I was involved in a pitch to an automotive manufacturer who said they wanted **industry-leading performance** as a top priority, but they ultimately went with another agency offering a more traditional solution. This can happen for a number of reasons. (We most probably didn’t do a good enough job of selling the benefits of our approach, but going headless can also seem pretty scary to content editors, especially when put up against some of the traditional “enterprise” systems who have a talent for making it look like everything “just works”.)

When you go headless, you will be bringing together individual tools that are each designed to be very good at one particular thing, rather than having one large system that can do all of these things in one place. That can be pretty intimidating to deal with unless you can make it easy as possible for your client to deal with.

### Are You Taking The Additional Development Time Into Account?

All of the potential power and flexibility of headless doesn’t come for free. One of the downsides to everything being custom is that this means that everything needs to be **developed from scratch**. With many of the options in this space, there is no real “default” document schema &mdash; indeed, they are set up very deliberately to not have any defaults like that. This is great on the one hand because it means that you get tightly-tailored document models that precisely match your needs.

On the other hand, though, it means that someone needs to define these document models, and then someone needs to create them for the system you are using. Then, because the frontend and backend are decoupled, somebody will usually need to create an engine to **allow previewing of draft content**; many modern frameworks include a system to allow previewing of draught content, but they universally require additional configuration to get working, and some will require a level of custom code. Of course, the front-end isn’t tied to the content, so any mapping of data to front-end components needs to be done as well. You will usually have to do at least some of this even with a tightly-coupled CMS, but the fact that you will likely have to allocate time to all of these things can be costly.

### Are You/Your Client Comfortable With Data Not Living On Your Own Infrastructure?

Whilst many who work with headless CMS systems and other SaaS vendors frequently consider this a positive, there are situations where your data being outside of your own infrastructure could be less than desirable, for instance where sensitive product or non-public production data is involved. Security for these companies is usually pretty good, but there are always risks.

Make sure you **weigh up the relative benefits** of having your content housed on an anonymous AWS server somewhere. We have seen before that even the mighty AWS can have outages and, for business-critical systems, these can be extremely costly. The difference here between SaaS on AWS or using your own infrastructure is that if you have an outage or security breach on your own infrastructure, that is likely to be down to your own product or code, but in a SaaS/AWS environment, outages are more likely to be caused by factors unrelated to your business. These instances are rare, but they do happen and it is important that this is taken into account when making these decisions.

## Ok, Great. So What Are My Options?

The number of headless and headless-capable content management solutions available in 2021 is staggering and growing constantly. Rather than trying to cover all of the options here, I want to give just a very brief introduction to a few of the better-known options. If you’re looking for a more comprehensive list, then you might want to check out [Headless CMS](https://jamstack.org/headless-cms/) or [CMS Comparison](https://cms-comparison.io/).

{{< rimg breakout="true" href="https://cms-comparison.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753b10e0-77d0-44ac-bbde-f02d732442fc/headless-cms-comparison.png" width="721" height="558" sizes="100vw" caption="<a href='https://cms-comparison.io/'>CMS Comparison</a> allows you to compare all headless CMS choices and filter them by their features." alt="" >}}

### Contentful

[Contentful](https://www.contentful.com/) is one of the most established of the headless CMS options, having been founded in 2016 and having enjoyed several successful seed investment rounds, and describe themselves as “an API-first content platform to deliver digital experiences”.

Contentful have made great strides in recent years to better support translated and trans-created content, and they have good support for multiple content “environments”, allowing changes to be made away from your production data and migrated later.

{{< rimg breakout="true" href="https://www.contentful.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef9776f3-69e7-4809-8311-0a812c05d4d8/contentful-image.png" width="720" height="367" sizes="100vw" caption="<a href='https://www.contentful.com/'>Contentful</a>, one of the most established of the headless CMS options." alt="" >}}

Contentful have a suite of integrations with other SaaS apps, so it’s easy to integrate with the likes of Shopify or CommerceLayer for e-commerce, or Cloudinary for asset hosting and processing.

#### Best For:

Those who are looking for the most well-established solution in the headless space.

### Storyblok

[Storyblok](https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=evaluating-headless) is the only one of the headless-first options here to actually describe themselves as a CMS, and features a really nice visual content editor which allows you to create and edit your content seemingly in-situ with a marvelous WYSIWYG interface. This is one of the traditional weaknesses of separating the CMS from the website, so seeing this kind of editing environment being created by Storyblok is a big step forward and the team should be proud to be driving the market forward in this regard.

{{< rimg breakout="true" href="https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=evaluating-headless" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebaf343c-5689-46c7-bab8-56a0c9b10bc6/storyblok-edtior.png" width="811" height="492" sizes="100vw" caption="<a href='https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=evaluating-headless'>Storyblok</a>, the only one of the headless-first options here to actually describe themselves as a CMS." alt="Storyblok" >}}

Storyblok also has the ability to use their API to generate content schemas that allow these things to live as and with your code, which is great for maintainability. Role-based permissions and translation/transcreation capabilities make distributed teams working on multilingual sites happily. Overall, Storyblok feels like an extremely polished and well-thought-out offering, and one that content teams, in particular, are likely to be a fan of.

#### Best For:

Those looking for a best-in-class WYSIWYG content editing solution from a headless CMS.

### Sanity

[Sanity](https://www.sanity.io/) are one of the newer kids on the block in this space, but have been garnering attention fast. They describe themselves as “the ultimate content platform that helps teams dream big and deliver quickly”.

Sanity does things a little differently from the other options here in that all your configuration and content models are done as code which, for developers, is a comfortable place to keep things. By allowing an almost limitless amount of creativity with document models and custom field types, Sanity allows developers to create deep, rich content structures for all manner of things &mdash; not just web content.

{{< rimg breakout="true" href="https://www.sanity.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c6e7cd2-cf81-4eb8-9d8f-eef8a6ad3fac/sanity-studio.png" width="750" height="540" sizes="100vw" caption="With <a href='https://www.sanity.io'>Sanity</a>, all your configuration and content models are done as code. Image credit: <a href='https://jamstack.org/headless-cms/sanity/'>Jamstack Headless CMS: Sanity</a>." alt="Sanity" >}}

The editing suite in Sanity is clean and simple, customizable, open-source, and is based on React. You can deploy the editing studio to any host you like, or choose to use a Sanity subdomain to host on their infrastructure.

#### Best For:

Those who need absolute control over nearly every aspect of implementation, from custom data structures to input components.

### Prismic

[Prismic](https://prismic.io/) really is the old character in the room in the headless space, being around way back in 2013, but that hasn’t stopped them innovating in the space. Just last year, they introduced SliceMachine, which aims to bridge the gap between front-end developers creating components and content authors by creating a 1:1 relation between content blocks (or “slices”) and front-end components, which makes building new pages and content sections a breeze for editors.

{{< rimg breakout="true" href="https://prismic.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84f9b16e-b361-47e3-8010-4184569f506f/prismic-image.jpg" width="720" height="357" sizes="100vw" caption="<a href='https://prismic.io/'>Prismic</a> creates a 1:1 relation between content blocks (or slices) and front-end components." alt="" >}}

Prismic’s editing suite is lovely and it seems that they have patched up some holes that used to exist in their field selection, so it offers a well-rounded experience.

#### Best For:

Those looking to minimize friction for content editors.

## What If I Want Something A Little More Traditional?

### Wordpress

[Wordpress](https://wordpress.org/) is still huge in 2021. For all the hype around other platforms, WordPress still powers some 40% of the internet, and it isn’t going to go anywhere. The developers are helping to make sure of this by improving its headless capabilities and focussing more heavily on its API support. New editing tools also make the experience of writing within WordPress more enjoyable, and some of the inherent tradeoffs of working with WordPress have been massively improved in recent years.

Working with a WordPress-as-a-service company such as Nestify takes much of the anxiety and headaches of security out of your hands as a developer, but be aware that, as the largest platform on the internet, WordPress still presents a very tempting target for those with malicious intentions.

#### Best For:

Those looking to stick to a comfortable, familiar content platform, whilst bringing the tech up to date.

### Sitecore

As one of the giants of enterprise content management, [Sitecore](https://www.sitecore.com/) is perhaps one of the names you would least expect to see on this list, but they have made huge strides in supporting headless, releasing Sitecore JSS to enable Jamstack projects to interface with Sitecore data.

The big difficulty in working with Sitecore or other enterprise CMS systems in a headless manner has always been getting personalization up and running, but that issue has been solved by the folks at Uniform, who actually got started working with Sitecore to enable this kind of functionality.

Sitecore is a big beast, and it’s not going to be right for a lot of projects &mdash; the cost alone puts it out of range of all but enterprise-level customers &mdash; but it is worth listing here, along with AEM, because there are still a lot of people who think that headless content management is only for small websites.

#### Best For:

Those looking at an enterprise project with a client that doesn’t necessarily want to go “all in” on new tech.

### Adobe Experience Manager

[Adobe Experience Manager](https://www.adobe.com/marketing/experience-manager.html) (or AEM) is another one of the major players at the enterprise end of things. It’s huge, and hugely expensive, just like most of its competition, but Adobe is another vendor that has made massive efforts to make their offering more friendly to those who want to separate their content from the presentation of their website.

AEM now supports a couple of different methods of requesting data out of their platform and Adobe now markets AEM as a “hybrid CMS”, which means it combines headless and more traditional, channel-specific, operation under one hood. This can be a big advantage to marketing teams who need to work across diverse platforms and need fine-grained control of content between these platforms, but those wanting in on Adobe’s “one platform to rule them all” will need deep pockets to get started.

#### Best For:

Those looking at the very top end of an enterprise, with deep pockets! AEM does a lot (more than we could ever hope to mention here), but it is *expensive.*

## Now I Have An Idea Of My Options, But How Can I Ever Hope To Choose Between Them?

There are so many options in the headless space now, you can easily end up in option paralysis. There are, however, a few questions you can use to help form an initial opinion or at least slim down the field:

### How Long Will It Take You To Get Up To Speed?

Different systems have different learning curves and different ways of supporting developers. Every system listed here has a community of developers built around it, but not all communities are created equal. Does the vendor provide detailed documentation? Starter projects? All of these can have a big impact on spin-up time.

### What Kind Of Support Model Will You Need?

Support models are usually most important to clients, and you often find that to access the more direct lines of support, you need to pay for the “enterprise” packages, which could make your investment higher than you might expect looking at your usage.

### How Well Established Is The Vendor?

How well established is the vendor? How are they financed? Again, these are usually client considerations rather than developer ones, but it pays to be able to tell the client early on that the vendor you are recommending is stable, has been around for X number of years, and that they have sufficient **financial backing** to be sure they aren’t going to be going anywhere any time soon. The last thing any client wants to have to deal with is a forced re-platforming because their existing vendor is sunsetting their product whilst the client is mid-way through their engagement!

### What Is The Editing Experience Like?

The editing experience is likely to be wildly important to a number of people at the client-side of any project. These are the people who will be working with whatever CMS you choose **day in and day out**. If the CMS is a nightmare to use, they will say so &mdash; a lot. Trust me, I’ve been in many pitches and follow-up meetings where a significant amount of time has been spent with the client listing the many frustrations they have with their existing system!

<blockquote><p>“Can the system(s) you are looking at provide in-context editing or live draft previews?”<br /><br />“How much effort is it to set these up?”<br /><br />“How fast or slow does the editor itself run?”<br /><br />“Is the user bombarded with options and unfamiliar buttons or are things well organised?”</p></blockquote>

All of these questions feed into the overall ease of use of the system. Some solutions, such as [Storyblok](https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=evaluating-headless), have gone to great lengths to make content editing **a rich and seamless experience**, but it is not generally considered a strength in the headless landscape as a whole, so it is definitely worth putting a small-scale demo in front of your content editors and seeing how they feel about the solution(s) you have your eye on.

### How Easy Is It To Get Your Data Off The Platform?

I’ve lost count of the number of pitch meetings that I have sat in and been told that we will probably have to start from scratch or write a custom scraper for content because the client’s content is completely tied up in a proprietary content management system, and they can’t easily export their data.

No matter how cool your CMS of choice seems, make absolutely certain that there is an easy way to get all of your content off of the system at some point. Sadly, no system is forever, and the client is eventually going to want to change their site, and their infrastructure with it. Anything you can do to **make life easier** for them at that point will be a huge positive.

This is generally easier with headless CMS solutions because they are API-able at their core, but it still bears closer scrutiny to make sure that you aren’t going to be causing a huge headache a few years down the line.

## Summing Up

Choosing an approach to, and platform for, content management is a big choice in any digital project. Headless content management is powerful and flexible but does come with some costs, and it isn’t ideal for every situation.

**Be mindful** that the price you see up-front from the vendor is rarely the final, total cost of the solution, and be sure that you don’t fall into the trap of thinking you can cut down on development costs by removing traditional “back-end” developers.

Make sure that **everyone is comfortable** with the realities of working with a headless CMS as opposed to a more traditional setup, and be sure to bring content editors along for the journey because they are the people who will be working with the system you set up most frequently.

Hopefully, this guide has at least helped to give some context to the hype and can help you to make a decision that you and your client can be comfortable with. You can build pretty much anything you want with **headless at its center** now &mdash; but always ask yourself whether you are reaching for a solution because it is familiar or hyped, or if it really is the best solution for your circumstances.

{{< signature "vf, il" >}}
