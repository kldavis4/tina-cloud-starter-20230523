---
title: 'Databases For Front-End Developers: The Rise Of Serverless Databases (Part 1)'
slug: databases-frontend-developers-rise-serverless-databases
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37dc0212-cede-409c-9e35-612cb2a58332/databases-frontend-developers-rise-serverless-databases.jpg
date: 2022-08-11T08:00:00.000Z
summary: >-
  In this article, the first part of “Databases for Front-end Developers” series, Atila Fassina helps you understand the concepts behind database architecture in order to use them reliably and sheds some light on serverless databases.
description: >-
  In this article, the first part of “Databases for Front-end Developers” series, Atila Fassina helps you understand the concepts behind database architecture in order to use them reliably and sheds some light on serverless databases.
categories:
  - CMS
  - API
  - Apps
  - Browsers
  - Serverless
---

As front-end developers, we understand the foundational role **data** plays in our daily jobs. It may come from an external API, a CMS, or even a spreadsheet. But god forbid we need to talk about setting up databases.

Those days are over. With serverless databases becoming popular by the day, it has never been easier to create a full-stack architecture with both vertical and horizontal scaling, high availability, and bulletproof consistency.

To fully reap the benefits of such an architecture, it’s essential to understand what decisions are made **for you**. In the same way that the “learn JavaScript, not a framework” mantra became popular, we also ought to understand the concepts behind database architecture in order to use them reliably. So, welcome to the first part of our **“Databases for Front-end Developers”** series.

This series is not going to make you an expert on distributed systems or capable of jumping into a database admin role, but it will shed some light on the concepts, terms, and acronyms you will face when getting ready to choose your next stack. See it as a primer on (serverless) databases. Hopefully, it will give you a push into the rabbit hole and make you confident in joining conversations to evaluate tradeoffs for different solutions.

## Spreadsheets And Content Management Systems

What?! Spreadsheets? Well, yes. The user interface (you and I, or U and I, or UI) is quite similar to that of a database. Spreadsheets give you a table in which to store data. In some cases, they will only allow you to define specific data types per column. The familiarities are there, but spreadsheets find an abrupt end once we pop the hood. 

The availability is questionable: spreadsheets are not meant to *serve* content, only *store* content. For starters, they will not fuel an app as it scales, and they may not obey certain best practices when it comes to assuring data integrity. Up to very recently, they were the quickest way to get started with some data layer. But now, there is no point for an app *not* to use a real (serverless) database (more on this later).

A **Content Management System (CMS)** is another kind of database. “Content” is a special kind of data that the CMS specializes in. It will provide the user (developer) with enough abstractions to facilitate managing such data to a point where the underlying database is not a concern. It will handle the deliverability, availability, and integrity of your data. But the heavier the abstraction is, the higher the tradeoff. The data types are limited to what the CMS will give you, with most even imposing their own architecture for handling relations, queries, types, etc. Of course, there are still significant and viable use cases for CMSs, and they aren’t going anywhere. So, as long as you’re sure that’s *your* use case, you’ll be fine with one.

## Growth Pains

If you choose the simpler, “abstractionful” route of a spreadsheet or a CMS as your source of truth and your data begins to diversify, obstacles will show up. The first issue with a spreadsheet is usually about the underlying API, it’s often not intended for most average-sized apps’ traffic, and then there are the first refactoring conversations.

With a CMS, APIs are usually not the problem, but managing the data can be. As an app grows and data diversifies, some of it ends up not being *content* anymore and may be more related to application logic.

When data is not content, managing it in a CMS is not ideal. It’s less flexible and often doesn’t fit the owner-team workflow. Now, while it is perfectly possible for other databases and CMSs to coexist, it’s up to the developers to understand the pros and cons of each solution and decide what is best for their app’s delivery and user experience.

{{% feature-panel %}} 

## Database Admin Is Hard

As front-end developers, the first time we talk about databases is usually a conversation about “relational vs. non-relational.” From then on, while trying to figure out the differences, we loosely hear a myriad of terms, such as ACID, BASE, and even CAP Theorem. This article will skip a thorough explanation of these differences. We will look better into them in the next part of this series. For now, it is sufficient to say “non-relational” databases impose **eventual consistency** on an app.

Eventual consistency can also be unwrapped into a longer discussion, but let’s take it as this: 

<blockquote>Eventual consistency means that in certain special conditions, the data received is stale.</blockquote>

Like comments in a blog post, they won’t affect your app if a few seconds after a *write* you still don’t see the latest one. But password updates need to be **strongly consistent** always, not **eventually consistent**.

Of course, those are not the only differences. Query performance is different between each type of database. One can imagine being eventually consistent allows for quicker *reads* because there is less assurance involved.

## More Growth Pains

Once the database is decided, the app can grow steadily and smoothly for a while. As an app gets big, data complexity grows, and as data complexity grows, the database becomes slower. At scale, how do we make a database faster?

- Do you add more resources to a single server? (vertical scale)
- How do you replicate data across a cluster of machines?
    - Do you split your database into smaller partitions (shards) instead? (horizontal scale, more about this in part 2)
- Do you add a faster in-memory database in front of it for common queries? (key-value store)

Those are not easy questions to answer. It depends on the user base, the type of data, the amount, frequency, and origin of queries. Is your database read-heavy or write-heavy? And though there is a multitude of factors impacting this decision, there’s also a high cost attached to making the wrong choice.

Additionally, some use cases may even require searching through data easier from user-land. A search engine is not an easy problem to solve and often requires an additional type of database to properly index your data (if sharded, it’s even harder). Having all this around your user’s data also brings a whole set of tools around it just to make it maintainable.

Even more, keeping an eye on our databases (now “data infrastructure” if we’ve got a search engine in the mix) requires a high level of observability and **OLAP (Online Analytical Processing)**. This introduces a whole new level of complexity!

As you may have noticed, very high stakes are associated with creating, maintaining, and growing a database. Decisions that can make or break an app, decisions that are costly to go back on, and that must be made relatively early.

{{% ad-panel-leaderboard %}}

## Serverless Databases Are Fun

Because of all the complexity mentioned above, many investors and incubators have their eyes turned to startups creating serverless databases. They are a whole new category of databases. The concepts of traditional ones still apply, but differently.

### Serverless Databases

To understand what a “serverless database” really is, we first need to deconstruct the term. It is a common joke that “serverless” is a misnomer. Still, the point of a serverless architecture is to abstract away from the consumer (developer) the complexity of handling site reliability and server maintenance provided by a serverless vendor, such as Netlify, Vercel, Amazon Web Services (AWS), and so many others. I tend to like [Xata’s definition of “serverless database”](https://xata.io/blog/what-is-a-serverless-database).

A “serverless database” does for databases what serverless does for servers. The complexity is lifted away (to different degrees depending on the chosen platform). Some, like Supabase and Firebase, will offer a multitude of serverless related features to couple with your database; others, like AWS Aurora or PlanetScale, focus on making it easier to use and scale PostgreSQL and MySQL DBs. And finally, there are others that abstract the database entirely, like Xata. They provide you with an ORM-like SDK, keep the database behind an API, and are able to offer a complex set of database features, bending the current limitations of traditional relational and non-relational databases.

Once we get to the next part of this series, we will talk about different kinds of databases. Then you will be ready to pop the hood on any serverless database offering you want and understand the differences for yourself. Meanwhile, let’s keep it superficial.

## Batteries Included

Don’t take the “serverless” prefix lightly; these databases are from a different breed. They are able to offer guarantees and performance that “traditional” databases require some effort to reach, sometimes not even so. This is because on serverless databases, the work has been done, just not by your team.

{{% pull-quote %}}
The same way “serverless” means you don’t need to handle your server, “serverless database” means you don’t need to handle your database. The platform will handle it for you.
{{% /pull-quote %}}

Because of this, the decisions about scalability and deliverability are often made external to your team. What your team gets is the assurance that any request will receive a response in a timely manner and that data will respect the consistency guarantees. Again, different solutions have different tradeoffs. It’s important to check what each offering imposes before jumping in.

{{% ad-panel-leaderboard %}}

## See You On The Next One

Hopefully, this has been enough to spark your curiosity. This is the first article of a 3-part series. In the next ones, we will cover more in-depth information about what databases actually *are*. Specifically, we’ll look into:

- Schemas,
- Theorems and models,
- Types of databases,
- whatever you suggest in the comments below!

All that necessary knowledge will enable you to choose the best solution for your app. Understanding the tradeoffs of different serverless solutions and surrounding yourself with the right kind of help is crucial to setting your app up for success. [Reach out to me](https://twitter.com/atilafassina) if you need anything meanwhile. Otherwise, see you in a few days!

### Further Reading on Smashing Magazine

- “[Gatsby Serverless Functions And The International Space Station](https://www.smashingmagazine.com/2021/07/gatsby-serverless-functions-international-space-station/),” Paul Scanlon
- “[Choosing A New Serverless Database Technology At An Agency (Case Study)](https://www.smashingmagazine.com/2021/03/choosing-new-serverless-database-technology-agency/),” Michael Rispoli
- “[Smashing Podcast Episode 22 With Chris Coyier: What Is Serverless?](https://www.smashingmagazine.com/2020/08/smashing-podcast-episode-22/),” Drew McLellan
- “[Building A Serverless Contact Form For Your Static Site](https://www.smashingmagazine.com/2018/05/building-serverless-contact-form-static-website/),” Brian Holt

{{< signature "yk, il" >}}
