---
title: 'How To Choose A Headless CMS'
slug: how-to-choose-a-headless-cms
author: emmanuel-tissera
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fa37a67-9079-4b4d-9489-fcd87c7c3807/how-to-choose-a-headless-cms.jpg
date: 2021-07-06T10:30:00.000Z
summary: >-
  There is an array of Headless CMSes out there. In this article, we delve into headless CMS features to satisfy your content editors, marketers and yourself as a developer. For the experience headless practitioner, this could be a checklist to see what’s new out there. For those starting out on their headless journey, this could be a guide on what to look for.
description: >-
  There is an array of Headless CMSes out there. In this article, we delve into headless CMS features to satisfy your content editors, marketers and yourself as a developer. For the experience headless practitioner, this could be a checklist to see what’s new out there. For those starting out on their headless journey, this could be a guide on what to look for.
categories:
  - Headless
  - Tools
  - CMS
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Storyblok
  link: https://www.storyblok.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb5f98-1b75-4f2a-9e13-b5a2fbe1a71d/storyblok-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.storyblok.com/">Storyblok</a>, a friendly headless CMS with a visual editor, nested components and customizable content blocks for websites and apps. <em>Thank you!</em>
---

Web pages, such as the one you’re reading now, have text, images, videos and other assets to bring information to you. This data would be collated and authored in a Web Content Management System (WCMS) by a content editor. WCMSes have gone through an evolution moving from a Traditional CMS to a Decoupled CMS to a headless CMS.

Moving to a headless CMS is not an easy decision and the selection process should not be taken lightly. In this article, I will highlight a few **core features that every headless CMS should provide**. We will explore those features, the associated challenges and help you choose a headless CMS to satisfy your organization’s unique requirements.

As the Technical Director at Luminary, I have been helping our clients choose the best CMS, DXP (Digital Experience Platform) or headless CMS to suit their needs. With Luminary’s 21 years of experience in the digital space, my experience of 17 years in the CMS space as well as our focus on Headless since 2016, here are my two cents on what you should look out for.

### Things To Consider When Choosing A Headless CMS

<ul>
<li>Concepts</li>
<ul>
<li><a href="#microservices-architecture">Microservices architecture</a></li>
<li><a href="#omnichannel">Omnichannel</a></li>
</ul>
<li>For content authors</li>
<ul>
<li><a href="#editing-experience">Editing experience</a></li>
<li><a href="#managing-images">Managing images</a></li>
</ul>
<li><a href="#authoring-roles">Authoring Roles</a></li>
<ul>
<li><a href="#workflows">Workflows</a></li>
<li><a href="#previewing-content">Previewing content</a></li>
<li><a href="#localizing-content">Localizing content</a></li>
</ul>
<li>For developers</li>
<ul>
<li><a href="#restful-graphql-api">RESTful and GraphQL APIs</a></li>
<li><a href="native-sdk">Native SDKs</a></li>
<li><a href="#environments">Environments</a></li>
<li><a href="#cdn">CDNs</a></li>
<li><a href="#usage-limits">Usage Limits</a></li>
</ul>
<li>Other Factors</li>
<ul>
<li><a href="#data-centre-locations">Data centre locations</a></li>
<li><a href="#technical-sales-support">Technical and sales support</a></li>
<li><a href="#enterprise-features">Enterprise features</a></li>
<li><a href="#infrastructure-integration">Infrastructure Integration</a></li>
</ul>

## Monolithic vs Microservices

We’ve explored the [concepts behind headless CMSes](https://www.smashingmagazine.com/category/headless) in detail here on Smashing Magazine, but let’s do a quick recap. When it comes to a Traditional CMS, the CMS and the resulting front-end website are built on a monolithic architecture. The Traditional CMS tries and succeeds in many ways to serve the needs of the developer, content author, and marketer. For example, if the CMS is built on Microsoft’s .NET Framework, the front-end website would also be built on the same technology. All functionality and integrations would also have a tight dependency which in turn results in a large, cumbersome monolithic code base.

**Decoupled CMSes** have removed this interdependence to a certain extent. This has been achieved by separating the front-end website from the CMS back-office and content repository.

Monolithic architecture takes a back seat with headless CMSes. The CMS and every other integration is a microservice. The CMS itself is provided on a **Software-as-a-Service** (SaaS) model which I like to term **Content-as-as-Service** (CaaS). With this microservices architecture, everything you got from your Traditional CMS does not come out of the tin. You may have different services and vendors to provide you with the best of breed for each of your requirements.

The move to a microservices mindset needs a bit of patience. We had marketers from a Traditional CMS background who resisted the idea of delving into multiple systems and services when using a headless CMS. We managed to take them along on the journey during selection and implementation of their headless CMS platform. Now, they are advocates for that headless CMS platform as it allows them to integrate new systems and services rather than being bound to one provided by a Traditional CMS.

**Look out for:**

- Reputed SaaS vendors
- Integrating headless CMS as a microservice
- Best of breed services

## Omnichannel At Its Core

As much as a microservices mindset would help you when integrating a headless CMS, the true power of headless is realized in its omnichannel nature. An omnichannel experience revolves around your customer and creates a single customer experience across your brand by unifying sales and marketing. With a headless CMS, content is provided to different channels such as web, mobile, social, no-UI smart devices, IoT devices and even non-digital touchpoints such as a bricks-and-mortar shopfront.

With a headless CMS, you need to **define the schema for each content model from scratch**. The process of defining this sound, logical taxonomy structure for the content items you create and publish is known as content modeling. If your first channel is going to be your website, make sure your content modeling takes omnichannel into account to alleviate any future pain. If you are only looking for a replacement CMS to just power your website, take another hard look at the Traditional or Decoupled CMS space to see if there’s something that would suit your requirements better. 

When modeling content schemas, think of the future. Working for a major airline not even a decade ago, I can remember trying to model content for mobile devices (yes! there was a separate subdomain for a mobile website).  This was excruciatingly difficult since the content schemas were geared towards only a desktop website. But the story holds true even today that we need to be vigilant about content modeling.

**Look out for:**

- Channels you want to target
- Good content modeling practices

## Creating Great Content

Whether it is a traditional CMS or a headless CMS, the main requirement is managing content. Content authors should love working in the back-office. If you see authors turning to other authoring tools such as Google Docs for its commenting or suggestions capabilities, it may be a red flag as to what features you are missing.

Microsoft word documents, spreadsheets, Google docs always rear their heads up when working with content authors. Rather than trying to banish them upfront, the easiest way to get content authors to work on the CMS is to **give them the features they need** and they will automatically phase those out. When we pushed Luminary’s own website live on a headless CMS, every team member (50 of them) was given enough access to add and edit their own profile for the website. It worked a treat without having 50 Google Docs flying all over the place.

### Editing Experience

The decision to use a headless CMS may be an IT decision. But buy-in from the marketers and content authors within the organization is critical for its adoption and success.  A headless CMS which allows content authors to enter content easily, find existing content and reuse content is something that should come out of the box. 

For ease of authoring content, having **easy-to-use editors** such as WYSIWYG editors, text editors, dropdowns and custom editors is a must. A clean and minimalist interface that allows a content author to focus on the task at hand will be appreciated. An editing interface that allows for concurrent editing, commenting, and creation of child content items in the same interface will increase the productivity of content authors.

A word of caution when using WYSIWYG editors or heavy reliance on any editing interface which produces HTML. As a headless CMS is geared to cater to multiple channels, relying on WYSIWYG editors would take away the atomic nature of content which can be reused. Make sure that custom editors **allow accessing data fields at a granular level**. We have seen this hamper the reuse of content across different channels such as mobile and desktop for example.

With a headless CMS, organizing content items in a tree structure is not the norm. But it is a bridge allowing content authors to transition easily from a Traditional CMS to a Headless one. If content items are not visualized in a tree structure, a strong search engine with facets and tagging capabilities is paramount for your content editors. This allows authors to find and reuse existing content easily.

When reusing content, another aspect to consider is whether content items can be nested easily within other content items. This allows for maximum reuse of existing content. But **beware of circular references to content** which could cause headaches and performance issues. An example is a content item for a lawyer which is linked to a content item for an expertise. Then if the expertise content item is again linked to multiple Lawyer content items this could form a circular reference. Look for a headless CMS with smarts baked in to limit depth in the API and visualizations to show linked content items to avoid this pitfall.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67b9c060-1169-4a9a-ad19-62a60fc7f0b0/headless-tree-search-editors.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67b9c060-1169-4a9a-ad19-62a60fc7f0b0/headless-tree-search-editors.png" width="800" height="" sizes="100vw" caption="Tree structure, search and data type editors (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67b9c060-1169-4a9a-ad19-62a60fc7f0b0/headless-tree-search-editors.png'>Large preview</a>)" alt="Tree structure, search and data type editors" >}}

**Look out for:**

- Authoring experience
- Structure of content items
- Ease of searching content
- Overuse of WYSIWYG editors
- Reusing content

### A Picture’s Worth: How To Handle Media

A picture is worth a thousand words. But image assets are heavy to transport, difficult to organize, and hard to search. In a typical CMS, you will see duplicates and poorly named image assets over time. It is important that content editors are given tools to organize, categorize, tag, reuse and search for images within a headless CMS. For me, this means organizing assets in folders or containers. But it would be good to **understand what your team requires** in terms of managing static assets.

The ability to upload a single image, set a focal point to it and then manipulate its dimensions and quality for different devices and screen sizes, brings massive time-savings to a content editor and even those designers/graphics artists who work behind the scenes. The **delivery of static assets in formats** such as WebP via a Content Delivery Network (CDN) is also crucial to serving your users a fast website.

Most headless CMSes come with these features out of the box. If not, you need to decide which features you can live without. There’s a caveat to that rule. For extensive editing of the original images, you should stick to the best tools for the job such as Photoshop.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f179a29-635b-4cbd-8976-62bd98300783/focal-points.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f179a29-635b-4cbd-8976-62bd98300783/focal-points.png" width="800" height="" sizes="100vw" caption="Focal points and image crops (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f179a29-635b-4cbd-8976-62bd98300783/focal-points.png'>Large preview</a>)" alt="Focal points and image crops" >}}

Along with images, the next heaviest assets are videos. Once again, with the microservices mindset, streaming of videos should be left to service providers such as YouTube, Vimeo and other online streaming services. If your headless CMS can provide you with a nice editing interface to search or select a video from one of these providers, it’s a bonus. 

**Look out for:**

- Organising images
- Cropping and delivering images via a CDN
- External best of breed video services

### Authoring Roles

Who can enter content and who can approve or publish content to a live site and other granular permissions need to be managed via the headless CMS as well. A two-person team could survive without having distinct authoring roles, but as organizations and content teams grow, authoring roles are a must.

I have worked with content teams of over 40 editors and this requirement needs to be carefully evaluated against the headless CMS you chose. If not, pandemonium will reign. With the team of 40 I worked with, we had copywriters, translators, QA personnel and legal approvers who had **different permissions to access certain content**, language variants, workflow approvals and publishing rights.

The number of distinct roles and back-office users is usually how headless CMSes structure their pricing. When comparing price points between vendors think of current numbers and the future growth of your content team.

**Look out for:**

- Distinct roles
- Number of back-office users

### Workflows

Not every content item needs to be managed via a workflow. But when workflows, audit trails and approvals are necessary, the process needs to be managed within your headless CMS. Having a robust workflow built from the ground-up on your headless CMS gives you peace of mind and the opportunity to handle every content item according to your business process. The ability to integrate third-party systems via webhooks or APIs is a bonus you should watch out for.

**Look out for:**

- Robust workflows
- Webhooks

### Content Previews

The content editor has authored the content, added images and sent it via a workflow for approval. But where do they preview the content before it is made available to the general public? This is where preview APIs to retrieve unpublished content and the ability to set preview environments come into play.

With a headless CMS, having moved away from a single channel mindset, your content editors should not expect to see full page previews within the CMS back-office. Each channel should have its own staging or preview environment to view yet-to-be-published draft content. This could be a staging site for your website or a locally installed version of your mobile app. A preview feature must be available in the pricing plan you have chosen for the headless CMS of your choice.

**Look out for:**

- Preview APIs from the vendor
- Separate staging and production environments on your end

### Locales

If your content needs to be served to different locales, that requirement needs to be identified early on in your project. Retrofitting is possible, but is not a fun activity. How you manage content and assets across cultures and languages should be thought out and documented. I would recommend creating a blueprint to identify which languages and assets inherit or default from another. Then make sure your choice of headless CMS supports that blueprint or explore avenues to achieve the same outcome differently.

**Look out for:**

- Internationalisation and Localisation support
- Creating your own blueprint for handling locales

{{% pull-quote %}}
 Creating great content is always important. Thus, content authors should be given the best possible experience in their day-to-day activities to make your transition to headless CMS a success.
{{% /pull-quote %}}

## Dev Time Is Precious

With a headless CMS, developer involvement is a must. This could be a back-end developer or a front-end developer consuming the headless API to display content on the website. But once initial development is done, a content author should be able to work with minimal intervention. That’s the whole point of using a CMS. It stands true for headless CMSes too.

As much as content authors are considered when comparing features, developer features should be explored as well. In this section, we will look at features that will save time for developers.

### APIs/GraphQL Support

A mature API, that allows for selection, pagination and projection of content items, is critical for a developer to work with a headless CMS. Out-of-the-box GraphQL support is another defining factor as it will allow the developer to define the result they need at a very granular level. Comprehensive documentation and code samples are also a must. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/626ebb9a-51f4-47f9-b671-849b57292ef4/graphql-ootb.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/626ebb9a-51f4-47f9-b671-849b57292ef4/graphql-ootb.png" width="800" height="" sizes="100vw" caption="GraphQL out-of-the-box (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/626ebb9a-51f4-47f9-b671-849b57292ef4/graphql-ootb.png'>Large preview</a>)" alt="GraphQL out-of-the-box" >}}

Make sure your developers are happy with the content retrieval APIs before committing to a headless CMS. Don’t forget preview APIs, secure APIs and the ease of using them via code. Do you want to automate content creation? Then **content management APIs** should be considered.

Content Management APIs have been a blessing where we automated the import of over 2,000 blog posts from a WordPress site to a headless CMS. All the blog posts and related images were imported with minimal work for the content authors. Some headless CMSes offer Google Sheets Add-ons and other nifty tools to do this at a click of a button.

With many headless CMSes offering free trials, it’s a good idea to take them on a test drive to see their suitability and conformance to your choice of content creation and retrieval.

**Look out for:**

- Mature REST APIs
- GraphQL support
- Preview and secure APIs
- Content Management APIs for CRUD operations
- Free trials to try it out

### Native SDKs

Software Development Kits (SDKs) for various technologies, languages and platforms are available directly from the Headless vendor, an open-source initiative or a third-party. Make sure these SDKs support the technology, language and platform you will be building your website or consumer app on. As much as RESTful and GraphQL APIs allow you to query content, having **a native SDK could reduce dev hours quite significantly**.

At Luminary, working with native SDKs for headless CMSes has allowed us to embrace the latest technologies such as Microsoft .NET Core and .NET 5. Also, building on an existing SDK has allowed us to follow the best practices recommended by the vendor while saving time.

**Look out for:**

- A supported SDK for your choice of technology, language, and platform.

### Environments

A website or an app for a mom-and-pop shop might be able to curate and preview content with a single production environment. But as organizations, teams and features grow, multiple environments to curate and preview content become necessary. Not only does your headless CMS need to provide environments, but your consuming application should have environments set up as well. Methods to refresh content across environments need to be considered.

**Look out for:**

- Environments within your headless CMS
- Ability to port content between environments 

### Images, Files and CDNs

We touched on managing images when talking about features for the content author. From a developer perspective, not only static assets need to be cached on a CDN. Many headless CMSes cache content retrieved via RESTful or GraphQL APIs. This speeds up the retrieval process and brings in performance improvements to your application.

While CDN caching is super useful, there are times when cache corruption or **older cached items could create issues**. The ability to purge the CDN cache or the ability to pull in the latest content with specific HTTP headers should be a part of your headless CMS’ API functionality.

The ability to use custom domains against a CDN to deliver your content or static assets might be a requirement you need to consider.

**Look out for:**

- Caching of images and content via CDN
- Custom domain capabilities

### Usage Limits Across Plans

Another factor to consider is the usage limits set for each plan you subscribe to on your choice of headless CMS. The number of content items, bandwidth consumption, the number of back-office users, the number of API calls, and rate limits need to be thought out. When planning for usage limits, consider current usage and future usage. Remember that **many headless CMSes operate on a subscription basis** and they do allow you to upgrade almost instantaneously to plans with higher limits.

However, it’s worth being aware of how many users will be using the platform, and whether the solution would need to scale up massively. We witnessed a client get a very large bill as they unwittingly added a large number of users over their allocated quota. It’s a good idea for administrators to be aware of what their Headless plan offers and keep tabs on usage.

Do consider keeping under usage limits on your current limits with client-side caching, static page generators and smart API or GraphQL calls to reduce your operating expenditure.  

**Look out for:**

- Limits on certain features
- Operating expense

{{% pull-quote %}}
 A developer’s time is expensive. Whereas a headless CMS is touted as a developer-friendly CMS, each vendor has different features they support natively. Understanding and comparing those against your developers’ needs is highly recommended.
{{% /pull-quote %}}

## Other Factors

There are a few other factors that may not impact the content author or the developer. This could range from marketing to finance to legal and regulatory requirements for your industry and your business. 

### Data Centre Locations

One question we often get asked is, where is the data stored? Yup, in the cloud. But which geographic data center is an important question due to the legal and regulatory requirements of certain businesses. A headless CMS which allows you to store data in the data center of your choice might be a critical factor in deciding which CMS you choose.

### Technical And Sales Support

The ability to receive technical and sales support in your timezone is another deciding factor when choosing your headless CMS. Not having a local salesperson has tipped many projects in favor of those vendors who have people on the ground in the relevant region.

We had a large NFP (Not for Profit) organization choose a headless CMS vendor due to the ability to store data in an Azure Data Centre within Australia. Having on-the-ground sales support and around-the-clock technical support clinched the sale for that headless CMS vendor.

**Look out for:**

- Legal and regulatory requirements of storing data
- Local sales and technical support 

### Enterprise Features To Consider

Some large organizations might require a Single-sign-on (SSO) tied to the company’s authentication system or audit logs which can be easily queried. There might be integrations to existing systems and certain ISO certifications which need to be in place before a SaaS product is considered a right fit. Making a list of these enterprise features and others unique to your enterprise-level organization is a good starting point when choosing a headless CMS.

## The Community In Action

Another usually overlooked area is the community around a given headless CMS. Are there people out there who are passionate about the product? I’m not talking about the vendor’s marketing peeps. Are there enough open-source resources shared by the people who are using the tool? This might not be a deciding factor but will help when you are in a tight spot during your implementation or support phase of a project.

## Infrastructure Integration

With headless CMSes, you are not bound to technology, language or platform. The technology or platform on which the headless CMS is built does not influence the client application. You can use a technology of your choice from .NET to Node.js, your OS could be Windows, Linux or macOS, and your language could be anything from Python to C#.

Similarly, when it comes to procuring infrastructure, you can choose to host your site on Netlify, Azure, GCP or AWS. The architecture of your website and its infrastructure decisions are now solely based on your requirements. There are also native first-class integrations with services like Gatsby Cloud which bring in more combos that make your life easier. For some, this could be a major decision and should be made by talking to some expert practitioners in the Headless space. 

**Look out for:**

- Enterprise features you can’t live without
- The community engagement with the vendor and the product
- Support for your choice of Infrastructure

## Our Experience At Luminary

At Luminary, we have been fortunate to partner with headless CMSes such as Acoustic, Contentful, Kentico Kontent, and Umbraco Heartcore. We have been working with some of these CMSes since the beta versions of their platforms. Public roadmaps, awesome technical support, and addressing our feature requests have been some of our highlights with these platforms. 

We’ve had experience with tackling SEO for Headless websites with front-end only implementations, caching large listing pages, dealing with large server-side caches, and integrating other microservices with headless CMSs. **Each of these had its unique challenges** which you should watch out for. Also, simple tasks on a Traditional CMS like form submissions and site search need to be well thought out along with more advanced features such as user authentication and authorization with third-party services.

If you choose the correct headless CMS with the pointers above and with the correct implementation partner, you should end up with a headless CMS which makes happy marketers, happy content editors, and happy developers.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Going Headless: Use Cases And What It’s Good For'" href="https://www.smashingmagazine.com/2021/03/going-headless-use-cases/" rel="bookmark">Going Headless: Use Cases And What It’s Good For</a></li>
<li><a title="Read 'Don’t Lose Your Head: Evaluating Headless'" href="https://www.smashingmagazine.com/2021/04/evaluating-headless/" rel="bookmark">Don’t Lose Your Head: Evaluating Headless</a></li>
</ul>

{{< signature "vf, il" >}}
