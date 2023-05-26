---
title: 'Going Headless: Use Cases And What It’s Good For'
slug: going-headless-use-cases
author: aaron-hans
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd6d0f4a-e4b2-4db9-8313-b4f527b8f0c5/3-the-headless-landscape.png
date: 2021-03-23T15:15:00.000Z
summary: >-
  One of the drivers of the popularity of headless options is that expectations for the quality of user experience are constantly going up. We have a wealth of tools to help developers build things fast so results are expected quickly. Going headless lets your team take full control of the user experience instead of wrestling with a large tool that doesn’t do quite what you wanted.
description: >-
  One of the drivers of the popularity of headless options is that expectations for the quality of user experience are constantly going up. In this article, we explore what headless means, use cases for it, and how to decide if headless is a good fit for you.
categories:
  - CMS
  - Jamstack
  - Headless
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Storyblok
  link: https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=headless-landscape
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb5f98-1b75-4f2a-9e13-b5a2fbe1a71d/storyblok-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.storyblok.com/?utm_source=smashing&utm_medium=referral&utm_campaign=headless-landscape">Storyblok</a>, a friendly headless CMS with a visual editor, nested components and customizable content blocks for websites and apps. <em>Thank you!</em>
---

Looking back at the years of developing for the web, I’ve used dozens of different CMS tools both off the shelf and homebrewed. I’ve been deploying and building plenty of **WordPress sites and plugins**, as well as extensions for full-service CMS sites in .NET. But for me, everything changed when I first heard of headless, and now, years later, I couldn’t be feeling more comfortable in the **headless ecosystem**.

This enthusiasm doesn’t come out of nowhere. While it might seem daunting to make sense of all the headless options, I’ve been refining my own strategy for different headless options in different environments, and made myself closely familiar with usual suspects in the headless space. Moving to headless helped me avoid running into roadblocks caused by limitations of larger all-in-one systems.

**Compartmentalizing functionality** so you can meet complex goals today and prepare your app to easily evolve in the future brings me peace of mind. It has been a pleasure contributing to successful deployments and iterations on web services built on headless solutions for private companies and the California state government.

In this article, I’d love to share some of the **useful pointers and guidelines** that I’ve learned throughout these years, with the hope that they will help you make sense of the headless world, and find the right candidates for your projects. But before we dive in, we need to go back in time a little bit to understand what headless brings to the table.

## Before Headless

Just a few years ago, our workflows seemed to be focusing on a range of tools, stacks and technologies. For CMS, we were mostly using all-in-one-tools. They included both the content authoring and content viewing functions.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ae462a5-da06-46ef-be03-1e125befc96b/textpattern-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ae462a5-da06-46ef-be03-1e125befc96b/textpattern-cms.png" sizes="100vw" caption="Some of you might be remembering the good ol' Textpattern, PHP-Nuke, Mambo and others — some of the first CMS, released in early 2000s." alt="Textpattern CMS" >}}

Users of these tools were **stuck with the front end** that came with the backend. Your ability to customize things was limited. You could install plugins but they all had to be built for your tool. You could write custom code &mdash; but only in the language that your tool is built on and within its constraints.

It all changed over the last few years with **headless CMS** gaining traction all over the industry.

## A Renaissance Of Specialized Tools

Today, we have a [flowering of tools](https://jamstack.org/headless-cms/) that specialize in either authoring or content presentation views. A **headless CMS** focuses on the content authoring piece and provides a way to connect a separate content presentation tool. The lack of a user-facing frontend is what makes it headless and gives it the flexibility to work with any tool via its API.

Being able to engineer your own frontend from scratch is freeing for many development teams. You may have a crack team of engineers fluent in delivering slick single-page apps in Vue.js or fast rendering, bulletproof static generated sites with 11ty. All of the latest web development frameworks are designed to work easily with structured data that can be provided from any headless CMS.

A headless CMS is a focused tool. It has **less responsibility** than an all-in-one solution. The API endpoints provided by a headless CMS provide a clean separation between systems so you can swap out front or backend architectures independently as things evolve. Your product grows, the ecosystem of tools expands, new approaches become available. Your backend and frontend requirements are going to change. If you have a headless setup you will be able to adapt more easily because your front and backend are already cleanly separated by an API and you can upgrade them independently.

## Is Headless Right For Me?

Most notably, headless gives you the flexibility you may need to meet challenging requirements. It might be difficult to meet your goals if you have to heavily modify an all-in-one product. Combining a headless tool with a smaller, different or homebrewed frontend might be the easiest way to deliver your desired designs and user flows.

*   If you want to **fine-tune every step of the product checkout flow**, you can use a headless commerce option to achieve that,
*   If you want to heavily **optimizex for Time to First Byte**, you might want to use a static site generator that rebuilds content on change based on a headless CMS API,
*   If you **host your own tools** and are cautious about security, you may want to lock down your authoring environment behind the firewall and consume it headlessly from a simpler Jamstack-based frontend,
*   If you are **serving the same content** to a variety of clients, such as web, native apps or third-party widgets, you can build them in a way that they all would communicate through the same CMS headlessly.

If you can meet your project’s requirements flawlessly with an all-in-one tool, then headless options are probably a bit of an overkill for you. In the same way, if your team is perfectly happy and well-versed with your current all-in-one-solution, you don’t really need to worry about splitting front and backend tooling. However, if instead, you are running into the limitations of your tools, then going headless will allow you to address your pain points directly.

### Example: Headless eCommerce

Let’s look at a specific headless choice: You can integrate an existing eCommerce platform, such as Shopify, as a complete flow that takes over the entire checkout process, or you could use a headless option that Shopify provides as well.

- In the former case, your design will heavily rely on Shopify’s **templates and out-of-the-box functionality**, so adjusting the checkout flow will be possible, but quite limited.
- In the latter case, you can design your checkout flow in any way you like, and you are going to rely on Shopify to merely perform the financial transaction.

The significant difference is that the headless option is going to require you to **build every single view** your user sees. Yet again, if that sounds like a hassle with no upside, then you probably don’t need a headless solution.

A team in need of the headless version will welcome the freedom this provides. Your design will have no constraints, and you will be able to control every pixel of every view. You will be in total control of all the code executing on your user’s devices, so you can track, optimize and speed up literally every single interaction.

At the same time, you are still **leaving the processing of transactions** up to your headless eCommerce solution, so you’re getting the benefits of their backend system.

The **bottom line** is: if you are struggling with the bottlenecks within your current eCommerce solution — be it heavy front-end, complex UI or just inaccessible design — then a headless option will make it *easier* for your team to resolve these issues. Similarly, if it sounds like it will make it easier for your team to increase your conversion funnel by making the deployment of new features faster and smoother, then it’s a good idea to consider the headless option as well.

### Avoding Lock-In With A Single Platform

Looking at the state of front-end today, **decoupling** your authoring and content delivery vehicles is the safest way to architect things in a world where options for front and backend tools are constantly expanding. It’s not uncommon that the authoring and reading environments have different sets of requirements, so being able to choose tools that address these separately gives you better options for both sides.

Jamstack-based setups are [enabled by APIs](https://jamstack.wtf/) so they are often tied to a headless CMS. Making a headless choice **doesn’t require a Jamstack front-end** though. Of course, you could still run some server-side code if you wanted.

For example, I’ve helped build a few sites running Node.js and Express consuming back-end APIs like *Wordnik.com* and this popular pattern works smoothly. Having **access to your data via APIs** makes it possible to ditch your server-side code in production, so you can easily embrace client-side approaches like Jamstack if that makes sense in your project.

The issue with “all-in-one”-solutions is that each of them has a lot of *commitments* baked into it. For example, you have to be committed to supporting a database and programming environment or choosing from SaaS vendors that do; also, your design changes will have to occur within the available themes and plugins.

With headless, we break out from being locked into a single platform. So if you need to use a **new front-end framework** for your website, or you want to remove expensive production infrastructure and use static site generators, or perhaps want to switch your CMS without rebuilding all your front-end from scratch — compared to alternatives, you can achieve all of it with far less friction when you are using a headless option.

Let’s take a look at a simple example. Imagine that your organization comes up with a new initiative and new design, and flows are created from scratch to serve new user needs. Suddenly a new technology stack needs to be assembled to fulfill these requirements.

{{% pull-quote %}}
 Choosing a headless option will give your products a better shot at longevity, and make it much easier to let your content move into multiple delivery channels smoothly.
{{% /pull-quote %}}

In such cases, you’ll need to search for a perfect off-the-shelf solution that perfectly matches your needs, or compromise some of the design and user flow requirements so that it works well enough. But if your design or performance requirements are strict, it may be easier to meet these goals by going headless.

The bottom line is that there are plenty of use cases when choosing a headless option that will give your products a **better shot at longevity**, as well as make it much easier to let your content move into multiple delivery channels smoothly. Being able to consume your content as structured data lets it thrive on your own website, in your native apps, and be syndicated to external sources.

### Not Everything Has To Be Headless

It might sound that headless is always a better option, but it isn’t. If in your current project you aren’t too concerned with the design and technical options described above, or you just need an operational website that does the job today, then you probably won’t need headless that much.

Of course, **speed from concept to delivery** is important, so as you are a few clicks away from a decently looking website without proper engineering support on your side, you may want to defer headless options for a later time. You can focus on site optimization and longevity once you feel like your idea might be working.

## How Headless Choices Help You Recover From Missteps

### Upgrading The Backend

#### Perils Of Per User Pricing

A while back, I helped set up a blogging system that would be used by dozens of authors. We were very impressed with the feature set of one of the headless CMS vendors, chose it for the headless CMS and enjoyed building a frontend on top of it that melded smoothly into our product suite. Eventually, the company decided that the number of authors should be expanded to a few thousand.

Most hosted CMS solutions **don’t publish the pricing structure** for user numbers this big. When we inquired about the cost of continuing to run this on the same platform, we didn’t quite like the answer. In order for this system to continue to make business sense, we had to swap out our CMS. We were able to make the swap without scrapping the frontend too because of the headless architecture.

#### API Throttling

So many startups focusing purely on the authoring environment are able to build beautiful products with developer-friendly APIs. Airtable is an example of spreadsheet innovation through user-friendly UI combined with clean developer experience via a well-documented API.

I built some useful prototypes where I fed scraped data into Airtable where it was edited by human experts, then used their APIs to power content views running on the main site and in embeds running on third party sites. When setting up the *read* system I pulled the Airtable data into a production-ready system that could **handle large traffic loads** and this worked well for a while.

I started to run into problems with writing data though. Calls were failing due to the hard limit of 5 requests per second. Hitting this limit gives a 30 second complete API request lockout. I was attempting to send in data from a distributed system so I added throttles and split things up into separate bases.

As the system expanded and the amount of data grew we were outgrowing this tool. I was able to address this by building rudimentary data editing features into a system based on the AWS DynamoDB instance that had been reading from airtable. We were able to quickly trade the slick Airtable authoring UI features for a bigger scale and lower monthly SaaS bills.

This is another example of how a **clean separation between the frontend and backend** provided by the APIs of headless authoring tools lets you target pain points precisely.

### Upgrading The Frontend

#### Shiny New Frameworks

Organizations that have been around for a while often have the problem of needing to support production systems built on a **variety of tech stacks**. There is constant pressure to homogenize tooling but also to innovate. I was part of a team tasked with building views and widgets that would integrate into existing products based on a headless CMS. We had a lot of fun quickly building prototypes with different lightweight frontend tools.

We ran an internal contest to see which engineer on the frontend team could whip up the best frontend based on the content delivered from the headless CMS API endpoints. One presentation had the best feature set and the smallest code footprint so the deveopers got the project and delivered the product by building it with [Riot.js](https://riot.js.org/).

*Riot.js* is a cool little library that packs a ton of features into a small size. It helps you write data-driven single file components like Vue.js. When the developer of this frontend left the company shortly after shipping version 1.0 the team lost the only person with enthusiasm for that library.

{{% pull-quote %}}
 Sometimes the fall from exciting, new, speedy development pattern to tech debt happens rapidly.
{{% /pull-quote %}}

Luckily, the decoupled nature of headless CMS architecture provides the flexibility to **change your frontend without touching the backend**. We were able to rewrite the front-end code and swap in updated front-end components based on different libraries that were more commonly used on other projects.

#### Raw Speed

I love the [Ghost](https://ghost.org/) project. I was an early subscriber because it was cool to see a WordPress-like solution built on Node.js. I respect this organization for offering a service built on open source tools they are constantly refining. I was really happy with this tool when I used it for my personal blog.

There was one facet of the solution that wasn’t perfect though. The **Time to First Byte** on my Ghost-hosted blog was too slow. Since I could retrieve all the post content via an API I was able to set up my own statically generated frontend on S3 + Cloudfront that used all the post content I had written in Ghost but had a faster time to first byte.

## Headless CMS As A Service

There are many Software As A Service businesses that have gone *all-in* on headless. Signing up with one of these vendors can immediately give you a **friendly content editing environment** and clean API endpoints to work with. Here is a quick comparison of a few of them all of whom have very low-cost entry-level plans and a laser focus on the headless CMS experience.

All of these services have a **solid base set of features**. They all include static asset hosting, saved revision history, and well-documented localization support. They differ in their content creation user interface and API features.

<table class="break-out tablesaw">
  <thead>
    <tr>
      <th>Vendor</th>
      <th>Content Editing</th>
      <th>API</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://buttercms.com/">ButterCMS</a></td>
      <td>Forms with a Word-style WYSIWIG-editor, with a  toggle to HTML code. You can configure a one click full preview by linking your frontend template URLs.</td>
      <td>REST API preview showing full JSON available in overlay on the same screen as content editor.</td>
    </tr>
    <tr>
      <td><a href="https://www.comfortable.io">Comfortable</a></td>
      <td>Forms-based editor; did not see how to set up a 1-click-in-context-preview.</td>
      <td>REST API endpoint link available in the editor mode, GraphQL available soon.</td>
    </tr>
    <tr>
      <td><a href="https://www.cosmicjs.com/">Cosmic</a></td>
      <td>Forms with a Word-style WYSIWIG-editor, with a toggle to HTML code. You can configure your own preview URLs to pull the draft JSON.</td>
      <td>REST API. Can view a full JSON in 2 clicks from the Object editor.</td>
    </tr>
    <tr>
      <td><a href="https://www.datocms.com/">DatoCMS</a></td>
      <td>Forms-based editor, can set up a plugin to enable a full page preview.</td>
      <td>GraphQL API with an API explorer.</td>
    </tr>
    <tr>
      <td><a href="https://www.storyblok.com/">Storyblok</a></td>
      <td>Forms-based editor, visual edit mode, with a full page preview.</td>
      <td>REST API, one click to full JSON from the editor mode.</td>
    </tr>
    <tr>
      <td><a href="https://www.takeshape.io/">TakeShape</a></td>
      <td>Forms-based editor, with a live preview configurable by uploading templates.</td>
      <td>GraphQL API with an API explorer.</td>
    </tr>
  </tbody>
</table>

## Exciting Headless Patterns

### Using A CMS Based On GitHub

Being able to take advantage of the user management, version control and approval workflows in GitHub are big advantages. It is helpful **not to have to set up new accounts** on new systems. Being able to see the history of reviews alongside the content updates is nice.

There are different flavors of GitHub-based CMS tools. This one has been a quick way to spin up documentation sites: [Spacebook](https://spacebook.app/) you can integrate it with Netlify to get a cleaner markdown editing UI or use it directly on GitHub.

The **preview features** that are now built into GitHub web editor make some of these tools more accessible to people who aren’t familiar with HTML. I love the view-rich diff option where GitHub shows markdown changes in full preview mode.

This is an [excellent list of 85 CMS tools](https://jamstack.org/headless-cms/) that allows you to sort on whether they are GitHub-based or not.

### APIs For Familiar Tools

Your **WordPress installation** comes with API endpoints, so you can continue using authoring tools your team has experience in a headless fashion. WordPress has [nice documentation](https://developer.wordpress.org/rest-api/using-the-rest-api/) for their REST API. This is enabled on new WordPress installs, so when you spin up a new WordPress authoring environment you can start reading JSON from `https://example.com/wp-json/wp/v2/posts`.

The WordPress settings page contains an update service field where you can enter URLs for services you want it to ping when content changes. This is perfect for triggering a serverless tool to grab the latest updates. WordPress v5 has this field in the Writing section of settings

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb9853b1-f792-4255-9ea2-83e20c776405/1-the-headless-landscape.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb9853b1-f792-4255-9ea2-83e20c776405/1-the-headless-landscape.png" width="800" height="" sizes="100vw" caption="With WordPress, you can adjust the 'update service' field where you can enter URLs for services you want it to ping when content changes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb9853b1-f792-4255-9ea2-83e20c776405/1-the-headless-landscape.png'>Large preview</a>)" alt="" >}}

### Combining Data Sources

Using headless tools for the state of California helped us craft emergency response sites that raised the bar for performance. We had full control of the frontend architecture and were still able to let writers use familiar authoring tools.

**We use WordPress headlessly**, writing to GitHub via FAAS. We are also writing other data sources into the repository and triggering static site generator builds on every change. Examples of data that get written to git in addition to the original editorial content are data that only changes once a day like the topline stats and our human-translated versions of each page.

Using **GitHub actions as build triggers** allowed us to integrate several different data sources into the site so we get fast publishing and a small production infrastructure footprint. Less production infrastructure lets us breathe easily when we hit big traffic spikes related to government pandemic announcements.

The WordPress -> FAAS -> GitHub repo part of the architecture was created by Carter Medlin. He wired this pipeline together from scratch in a couple of days while we designed and built the site frontend. This is running on a serverless MS Azure function so there are low infrastructure costs and maintenance. It gets pings from the WordPress update service described earlier, pulls json from the WordPress API and writes new content into GitHub. The code for this serverless endpoint is [viewable on GitHub](https://github.com/cagov/wordpress-integration-api/tree/master/WordPressService).

Out bots are hard at work **publishing all content updates** as they receive pings from WordPress. This activity creates an easily reviewable log of each update and the ability to revert changes with usual GitHub processes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad280253-27ce-4eb7-97c9-c597cebbf71a/2-the-headless-landscape.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad280253-27ce-4eb7-97c9-c597cebbf71a/2-the-headless-landscape.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad280253-27ce-4eb7-97c9-c597cebbf71a/2-the-headless-landscape.png'>Large preview</a>)" alt="" >}}

Building the frontend of this site using the [11ty static site generator](https://www.11ty.dev/) was fast, fun and worked perfectly. We get big traffic spikes on pandemic-related news and knowing we have a static frontend reduces risk when the concurrent user counts start ramping up and we are publishing a lot of content updates.

I like how the 11ty community **focuses on performance and accessibility** with its [community leaderboards](https://www.11ty.dev/speedlify/) and lightweight architecture. Making sure that tools built by the state work for all Californians is important. We want things to work on *any* device under low bandwidth conditions and support *all* assistive tech. It is pretty cool that we can use tools like 11ty which make delivering fast, accessible sites easier. We use web components on the frontend to provide additional features while keeping the code weight small.

{{< rimg breakout="true" href="https://covid19.ca.gov/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd6d0f4a-e4b2-4db9-8313-b4f527b8f0c5/3-the-headless-landscape.png" width="800" height="" sizes="100vw" caption="On <a href='https://covid19.ca.gov/'>Covid19.ca.gov</a>, we can use tools like 11ty which make delivering fast, accessible sites easier. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd6d0f4a-e4b2-4db9-8313-b4f527b8f0c5/3-the-headless-landscape.png'>Large preview</a>)" alt="" >}}

## Considerations When Making Headless Choices

Excited about the capabilities headless tools give your team? The number of options available can be overwhelming. This is a list of features that may help you whittle down the options:

### Authoring Environment Features

*   Ease of **authoring documents**
*   Ease of adding structured data
*   Layout options
*   **Preview** features
*   Content approval workflows

### Content API Features

*   What queries are available
*   How **granular** is the content structure
*   Are there any limitations on data access (Airtable REST API hard limits)
*   **Scalability**: do you need to put a CDN in front of your content API
*   Ease of adding localization
*   Getting your content out, what if you change your plans, how hard is extracting all your data going to be?

### Cost

*   Are you **paying per user** for hosted solutions?
*   Are you managing open source software you install in your own environment?
*   Are user accounts easy to administer?
*   Can you integrate with your existing single sign-on solutions?
*   Has the product passed security audits, does it include **two-factor authentication**?

### Source Control/Approval Flows

*   Is content **versioned**, so that you can roll back to prior versions and keep track of what was published and what edits were made when?
*   Can you **share new versions** of content before publishing them? Can you restrict access to these previews?

### Static File Management

*   How easy is it for your authors to add new images, pdfs, etc.?
*   Ease of hooking author uploaded files into image optimization flows?

## Where Headless Is Heading

When you look closely into the headless landscape, you’ll find out that **headless tools intentionally limit their functional scope** and provide ways to integrate into larger systems. Unbundling specific features is beneficial when systems get more complex. It’s just easier to make specific choices that limit the cost, security, maintenance, hosting requirements of larger code footprints when you work with smaller, focused tools.

It’s worth noting that headless options **usually require writing some code** yourself. However, as frontends are increasingly a set of pre-built components and often an entire off-the-shelf design filled in with your own data, it shouldn’t be too presumptuous to expect more ways to mix and match specialized tools and seamlessly integrate headless options without writing code yourself.

The perfect backend for a project could be just a SAAS subscription or an open-source project install away. This may integrate codelessly with an off-the-shelf frontend that meets all your needs. I see that [Stackbit](https://www.stackbit.com/) is already melding headless CMS with their no code frontend. I can set up a new site using Stackbit’s WYSIWYG no code page creation tool and then I can pick from a set of headless CMS options from different vendors to manage the full site data.

In this article, we’ve gone over some use cases where going headless helped companies I’ve worked for cope with change. **Headless choices are enticing** whether you are interested in them for application architecture flexibility, user experience control or thinking carefully about the longevity of your service.

I am excited to see how this space continues to grow and will be continuing to look for ways to use these options to deliver better products and make my job as a developer easier.

### Further Resources

- [Headless CMS](https://jamstack.org/headless-cms/), An excellent list of 85 CMS tools that allows you to sort on whether they are GitHub-based or not.
- “[How To Create A Headless WordPress Site On The Jamstack](https://www.smashingmagazine.com/2020/02/headless-wordpress-site-jamstack/),” Sarah Drasner &amp; Geoff Graham
- [Headless Commerce](https://www.shopify.com/plus/solutions/headless-commerce), Shopify
- “[GoTrue JS: Bringing Authentication To Static Sites With Just 3kb Of JS](https://www.netlify.com/blog/2018/12/07/gotrue-js-bringing-authentication-to-static-sites-with-just-3kb-of-js/),”  Divya Sasidharan, Netlify
- [The Editing Experience For Jamstack Sites](https://www.stackbit.com/), Stackbit
- [Wordpress Integration API](https://github.com/cagov/wordpress-integration-api), CAdotGov, GitHub

<div class="sponsor-panel c-felix-the-cat">
	<p class="sponsor-panel-content">
		This article has been kindly supported by our dear friends at <a href="https://www.storyblok.com/?utm_source=smashing&amp;utm_medium=referral&amp;utm_campaign=headless-landscape">Storyblok</a>, a friendly headless CMS with a visual editor, nested components and customizable content blocks for websites and apps. <em>Thank you!</em>
	</p>
	<a class="sponsor-panel-image" href="https://www.storyblok.com/?utm_source=smashing&amp;utm_medium=referral&amp;utm_campaign=headless-landscape">
		<img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb5f98-1b75-4f2a-9e13-b5a2fbe1a71d/storyblok-logo.svg" loading="eager" width="200" alt="Storyblok">
	</a>
</div>

{{< signature "vf, il" >}}
