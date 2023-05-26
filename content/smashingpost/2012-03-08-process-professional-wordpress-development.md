---
title: A Process For Professional WordPress Development
slug: process-professional-wordpress-development
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dc06153-10c7-4f21-81fc-f40b665364e8/wordpress-files-illu101.jpg
date: 2012-03-08T15:55:36.000Z
author: tom-mcfarlin
description: >-
  Recently, we discussed “[How Commercial Plugin Developers Are Using The
  WordPress
  Repository](https://www.smashingmagazine.com/2012/01/13/commercial-plugin-developers-wordpress-repository/).”
  This article provided a solid explanation of the plugin repository, how to use
  it, how not to abuse it, and how to leverage it for success, even with premium
  plugins.

  [![professional-wp](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/146c182e-4e08-46f7-9f4b-05165460ff8d/professional-wp.jpg)](https://www.smashingmagazine.com/2012/03/08/process-professional-wordpress-development/)

  Now is a great time to be working as a WordPress developer: the community is
  active and growing, the platform has a solid API and the platform is under
  constant development. Despite these advantages, many developers have a hard
  time getting started building premium products.
categories:
  - WordPress
  - Themes
  - Plugins
  - Techniques (WP)
---
Recently, we discussed “<a href="https://www.smashingmagazine.com/2012/01/13/commercial-plugin-developers-wordpress-repository/">How Commercial Plugin Developers Are Using The WordPress Repository</a>.” This article provided a solid explanation of the plugin repository, how to use it, how not to abuse it, and how to leverage it for success, even with premium plugins.

Now is a great time to be working as a WordPress developer: the community is active and growing, the platform has a solid API and the platform is under constant development. Despite these advantages, many developers have a hard time getting started building premium products.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/146c182e-4e08-46f7-9f4b-05165460ff8d/professional-wp.jpg"><img loading="lazy" decoding="async" class="105216" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/146c182e-4e08-46f7-9f4b-05165460ff8d/professional-wp.jpg" alt="professional-wp" width="550" height="365" /></a>

In this article, we’ll look at what’s required to develop professional WordPress products (either themes or plugins). Specifically, we’ll look at several key factors in building and releasing a successful product. We’ll also discuss idea generation, development and testing, business models, how to offer support, and simple marketing strategies.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Process For Professional WordPress Development](https://www.smashingmagazine.com/2012/03/process-professional-wordpress-development/)
*   [Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)
*   <span>[How To Create Custom Taxonomies In WordPress](https://www.smashingmagazine.com/2012/01/create-custom-taxonomies-wordpress/)</span>
*   <span>[Adding Custom Fields In WordPress’ Comment Form](https://www.smashingmagazine.com/2012/05/adding-custom-fields-in-wordpress-comment-form/)</span>

{{% feature-panel %}}

## Get An Idea

For many, the biggest challenge is coming up with an idea for a premium product that will work. As developers, we often make this harder than it needs to be. Many of us will dismiss our own ideas, thinking “Ah, that’s too obvious,” or “Anyone could build that, so why bother?" But this is absolutely unfounded.

Regardless of how obvious an idea may seem or how easy it may be to implement, the idea is still valid. And just because you would not necessarily buy it does not mean there is no market for it.

That being said, here are a couple of ways to seed an idea:

*   **Look for something you need.**.  Simply put, if there’s something you wish you had in your toolbox, you’re likely not the only one who wants it.
*   **Identify major players, then compete.**.  Competition is good because it fosters innovation. Nothing is wrong with being second (or third or ninth) to market with a product. Identify successful plugins or themes, offer some additional features or a new take on the concept, and compete.

Finally, neither simplicity nor complexity matter — utility does. If you’re afraid that your idea is too simple to sell or too complex to build, you’re probably wrong. The market doesn’t care how easy it was for you to build something, nor does it care how complex the product is under the hood. If the product would make its users lives easier, then it’s marketable.</p>

## Bring It To Life

Once you’ve got an idea, it’s time to get started. One of the most important steps in professional WordPress development is to lay a solid foundation.</p>

### Identifying The Environment

Although WordPress is under active development, not everyone runs the latest version of the platform. Some are several versions behind, some are one version behind, some are up to date, and some will have installed the next version before your product is even released. Nail down your product’s requirements from the beginning because it will dictate all of your work, from development to release.

A few things to consider:

*   Which version of WordPress will you support?
*   Will you provide updates to future releases?
*   Will your product run on WordPress Multisite?
*   What browsers will you target?

This list is merely a starting point, but the questions are key to building the most solid product possible given the constraints of the environment.</p>

### Development

With your requirements defined, you should have a clear picture of the environment needed to support your work. At this point, it’s time to set up the development environment.

Simply put, the development environment is the local installation of the Web server, database system and platform (in our case, WordPress) in which you will build the product. Ideally, the development environment should mirror the staging (or testing) environment (we’ll talk about this more later). The staging environment should, in turn, mirror the production environment (i.e. the environment in which you will release the website) as close as possible.

So, if you’re going to be targeting WordPress 3.3.1, with support for IE 9, Chrome 13+, Safari 5+ and Firefox 6+, then your local development environment should include the proper tools for developing the website across the board.</p>

### Staging

The biggest difference between the development and staging environments is that the latter is meant for mistakes. If you destroy the database by accident, no problem. Staging, on the other hand, acts as a simulator for the production environment.

Similarly, the staging environment should be very similar to the development environment’s Web server, database system and WordPress version. Ideally, it would be loaded with content as a solid demonstration of how the product would perform under actual use.

Ultimately, you should treat the staging environment as a live website. That is, consider it as something of a black box, and manage it as if you were an end user, not a developer.

For example, install the project using the WordPress administration panel, and tweak the settings in the dashboard. If a problem occurs, check out the error logs, but stay out of the code as much as possible. Remember, you’re simulating usage as if you were an end user.</p>

## Testing

When building software, regardless of the platform, you need to have the proper testing in place. After all, you want your work to be used by a lot of people, right? So, you’ll need a testing infrastructure to catch any bugs prior to release.

There are a variety of tools, utilities and libraries for automated testing of both server-side code (in our case, PHP) and client-side code (in our case, HTML, CSS and JavaScript). These tools could take up many articles by themselves, but let’s cover a few general best practices.</p>

### Bug Tracking

Bug tracking is simple. It typically consists of listing all of the features of the project, their expected inputs, how they should perform given each input, and what output they should return, if any.

But many developers don’t track bugs seriously, which is why so many themes and plugins behave unexpectedly. Although tracking bugs during development is important, that’s only the half of it. Ultimately, you’ll have to set up a system that tracks bugs during development and after release, because no matter how much you test beforehand, users will always find something that you missed or that can be enhanced.

There are a variety of ways to track bugs. Some people use a simple notebook or spreadsheet, but if you’re working on a professional product, then look to professional tools. Some bug-tracking systems are standalone, while others are integrated in source-code control systems.

#### Bug Tracking and Source Control

Most intermediate to advanced developers use some form of source control to manage their work. If you don’t, then definitely read “<a href="https://www.smashingmagazine.com/2008/09/18/the-top-7-open-source-version-control-systems/">7 Version-Control Systems Reviewed</a>,” which provides a great introduction to source-code management and project versioning.

A number of applications integrate bug tracking with source control, providing a cohesive all-in-one solution for managing your project’s versions and the bugs that appear during testing and upon release.

Although this article isn’t a resource for source-control systems, we’ll touch on two in particular, which do a killer job of providing both source-code management and bug tracking:

*   [Codebase](https://www.codebasehq.com/) provides hosting for Git, Mercurial and Subversion. It has solid back-end administration and well-integrated ticketing and bug tracking.
*   [GitHub](https://github.com) is (obviously) a Git-based source-control system that also includes ticketing and tracking. Its interface is simpler than Codebase’s, but it’s no less of an application.

Of course, the Web is full of applications that provide this functionality, and rolling one on your own server is even possible, if you feel so inclined.

The bottom line is that if you use source-control software in your work, you can cut out an extra step by using a solution that integrates source control and issue tracking.

#### Standalone Applications

If you’re a seasoned developer, odds are that you don’t want to disrupt your workflow. As convenient as an all-in-one solution can be, it could end up duplicating a part of your existing process (such as source control). So, a standalone application that does one thing might be a better alternative.

Two products in particular are elegant bug-tracking solutions for freelancers and teams:

*   [ZenDesk](https://www.zendesk.com/) provides support-ticket management that can be done via email or in the product itself. It also provides general help-desk functionality, which is great for issues unrelated to bugs.
*   [Lighthouse](https://lighthouseapp.com/) is a lean support system that aggressively focuses on providing support ticket functionality. It offers task functionality, email support and document integration.

Whatever your preference, there is a solution for it, and standalone ticketing applications are no exception. Similar to source-control systems, these come with a wide variety of options, so do shop around.</p>

### Beta Testing

Running through features and use cases on your own can shake out a lot of problems, but it’s easy to miss obvious things, especially when you’re so close to the code. After all, <em>you</em> know how it works, so following the steps that work is natural.

This is why having a team of beta testers is helpful. Ideally, you would send a copy of your theme or plugin to a handful of testers, anywhere from 5 to 10 people. Don’t leave them in the dark, though. All products have some sort of manual or documentation, and although your work is still in beta, give the testers some instruction on the purpose of the product, how to use it, what to look for and how to provide feedback.

Having customers figure out how to use the product is as much a part of testing as the features themselves. If a user complains about not being able to figure something out, mark that as a bug. Usability is a feature, and you want to avoid frustrating users as much as possible.

To this end, when handing off the beta to testers, provide them with instructions on how to get started, but avoid giving so much information that they don’t have to figure out how to use it on their own.

As your testers put the product to work, you’ll likely discover issues that you had no idea existed. That’s OK — that’s exactly what beta testing is for. As in the process of tracking bugs, note the issues, resolve them and then ship another beta. With each round of testing, you’ll shake out more bugs.</p>

### On Bugs, Testing and Releases

Even though you’ve tracked issues and beta tested, your product will still have bugs — it’s inevitable. That’s fine; the Internet is a highly agile environment in which you can get nearly instant feedback. Simply note the problem, add it to the issue tracker, and resolve it in the next release.

Ultimately, your goal is to rid the software of bugs. While you might not be able to do that completely, the strategies above will minimize the number of defects in the product upon release.</p>

## Choose a Pricing Model

When your project is complete — that is, when it has undergone development, staging and several rounds of testing — it is time to bring it to market. A slew of articles could be written on the strategies for doing this; the topic is rich. Here, we’ll cover the most popular methods of pricing and marketing a product. Take this only as an general overview.

While picking any price point and then selling the product on a simple website would be much easier, you will ultimately help your bottom line more by carefully planning the pricing model, customer support and marketing strategy.</p>

### Freemium

This option is very common, not just with WordPress-related products, but with many applications and services on the Internet. According to this model, you would provide a free version of the product — perhaps a trial or feature-crippled version — and then give users the ability to upgrade to the premium version.

For example, you could provide a simple plugin that makes it easy for users to display their three most recently favorited tweets from their Twitter account. And then the premium version of the plugin could support multiple Twitter accounts, more than three favorited tweets, and manually selected favorites.

*   **Advantage**.  Users get to “try before they buy,” getting a chance to evaluate whether they would prefer the premium features.
*   **Disadvantage**.  Of your sizeable customer base, relatively few would probably purchase the premium version.</p>

### One-Time Purchase

This model is simple. If the user wants the functionality offered by the plugin, then they purchase it. It’s a one-time fee, and the product is theirs to keep.

One such product might be a plugin that helps users optimize their WordPress database. Say the user is an avid blogger and saves a number of half-written drafts. Perhaps they have a ton of stuff in the “Trash” that they’ve not taken the time to delete, generating a bit of overhead in the database. A plugin that guts all of this from the WordPress installation and database would deliver value to the user for a long time. But it would probably not be frequently used and, thus, would not warrant a monthly payment model.

*   **Advantage**.  You generate income right away because users must purchase the product in order to use it.
*   **Disadvantage**.  Will upgrades be free? What’s the refund policy? Will you provide support?

We’ll discuss support a bit later in the article, but don’t neglect these questions when choosing a pricing model.</p>

### Subscription

We’re all familiar with the subscription model. The user purchases the product and agrees to pay a certain amount for a set period of time (each month, quarter, etc.) for as long as they use the product.

One product that could warrant a subscription model is a plugin that backs up the user’s database every day, along with the contents of the <code>wp-content</code> folder, and stores it off site on a reliable server that you manage. The user is essentially paying for peace of mind in having their data backed up, and you’re expending your resources to store this data.

*   **Advantage**.  You’ll have an ongoing revenue stream and the flexibility to develop the product long term.
*   **Disadvantage**.  You’ll have fewer customers because people are generally reluctant to pay monthly fees. Depending on the product, you’ll have the burden of being responsible for critical data.</p>

### The Best Pricing Model

There is no silver bullet for pricing your product. Ultimately, it’s up to you and your team. The goal is to provide solid service to your customers while maximizing profit from your time and resources.</p>

## Offering Support

Regardless of how much work you put into the interface or how much you and your beta testers test it, some users will always have questions or need help using the product.

That’s OK. Knowing this in advance enables you to put an infrastructure in place to minimize frustration and answer questions that come up.</p>

### Documentation

Any product you ship should include <em>some</em> form of documentation. Software developers do this in a variety of ways, and WordPress developers are no different:

*   **Text file**.  Typically, text-based “readme” files briefly describe what the product does, how to install it and how to get in touch with you. While common, they don’t provide a whole lot of detail on how to use the product; they’re usually meant to supplement another source of documentation. Also, readme files are required in order for a plugin to be included in the WordPress repository.
*   **Website**.  In recent years, providing documentation for a theme or plugin on a dedicated website has become customary. The website becomes the main point of reference and can be linked to from the product itself, from other websites, from Twitter, in email and so on. It is an easy way to thoroughly document the product using text, screenshots, video and more.
*   **Contextual help**.  This form of documentation is less common but is an elegant solution when done right. Generally, inline documentation is done via labels, tooltips and other methods that guide the user through the application.

While you’ll have to decide what works best for your business and product, most professional products come with both a website for documentation and a help guide that is either built into the product or in the form of an accompanying manual.

A readme file is considered the bare minimum and is rarely sufficient as documentation for a professional product.</p>

### Support Options

In addition to documentation, some type of customer support for premium products is common. Again, there’s no single best solution, but most developers adopt one of two general approaches.

One option is to provide support through a forum using free <strong>open-source software</strong>, such as <a href="https://bbpress.org/">bbPress</a> and <a href="https://www.vbulletin.com/">vBulletin</a>. These packages are relatively easy to install, set up and configure.

*   **Advantage**.  The bulletin board-like experience is familiar to users, it’s functional, and it gets the job done.
*   **Disadvantage**.  All data is housed on a machine that you manage. And the user experience is less elegant than modern paid solutions.

A dedicated location where users can ask questions publicly is most advantageous if most of the questions come up repeatedly. This way, users can always refer to a single definitive answer.

The second option is to use <strong>paid software as a service</strong> (SaaS) that provides off-site managed hosting for your help desk.

*   **Advantage**.  The data is housed off site, making it the vendor’s responsibility to provide a high-quality user experience and tools such as mobile optimization.
*   **Disadvantage**.  These solutions are usually subscription-based, so revenue from your product will need to cover the cost.

While most commercial developers opt for a paid solution, the bottom line is that you have to know what works best for your target market for the product you’re offering.</p>

### A Word About Support and Pricing

There is typically a correlation between the support model and the pricing model of a product:

*   **Freemium** products usually ship with a user manual or documentation and nothing else. Support is typically not offered.
*   **Single-purchase** products lend themselves to a user manual or documentation website, or perhaps a support forum. Also, even if users pay for the product one time, they might expect ongoing support from you.
*   **Subscriptions** are best suited to documentation and a support forum. Thus, as long as users subscribe, they will have access to the support forums.

Of course, these are just generalizations. For example, if you opt for a freemium model, you could still offer support, but it all comes down to tradeoffs. Would you be willing to provide support if the time spent is not being directly paid for?

Each combination of support and pricing has its pros and cons. Your goal is to maximize the benefit to customers and your revenue.</p>

## Going To Market

The final issue to consider before going live is how to present the product and how to get the word out. Luckily, landing pages and social networks make it easier than ever to promote products.</p>

### Marketplaces

WordPress has spawned a number of website marketplaces where you can sell your work. The way it usually works is, in exchange for leveraging the marketplace’s built-in audience, you give the vendor a commission for each sale of your product.

Two of the most popular marketplaces for WordPress right now are <a href="https://themeforest.net/">ThemeForest</a> and <a href="https://www.mojo-themes.com/">MojoThemes</a>. Both follow a commission-based model and offer a much broader audience than what you would be able to reach on your own. But the requirements for publishing your work in these marketplaces can be strict compared to self-publishing.</p>

### Landing Page

If you’re serious about marketing your premium project, it’s worth paying for a home page with a dedicated domain and a decent design. After all, you’ve poured a significant amount of time into developing this, so the promotional material that people see should reflect this level of quality.

Keep the website simple. A single landing page that describes what the project does and why it’s useful and that provides a few screenshots and a convenient way to purchase it will suffice.

Depending on the product, a demo might be useful, too. In this case, set up a WordPress installation on the same server, add some sample data to give users a feel for what the product would look like, and then configure the demo.

Follow two key principles when setting up a landing page:

1.  Describe the need that your product satisfies;
2.  Make it easy to purchase.

If the landing page doesn’t address these two points, then reconsider whether you even need one.</p>

### Marketplace or Landing Page?

Inevitably, the question arises of which will yield higher sales, a marketplace or self-hosted landing page? The truth is there’s no right answer.

A case can be made for each. Some development teams have made <a href="https://wpcandy.com/reports/orman-clark-sets-theme-forest-record-and-expands-team">well over six figures</a> in established theme marketplaces. <a href="https://www.studiopress.com/themes/genesis">Other teams</a> have found great success by relying mainly on self-hosted websites.

The decision is largely personal. Evaluate your product and target audience, and see whether an existing marketplace provides the best opportunity. If not, then move forward with a landing page or website.</p>

### Share It

Once the product is complete, the documentation written, the support forum open and the landing page live, it’s time to get the word out. Thankfully, the WordPress community is exceptionally welcoming of new projects and usually does a stellar job of helping developers share their work.

To get the word out about your work, consider the following starting points:

*   **Blog posts and newsletters**.  In addition to using your own website, consider reaching out to a couple of authors and contributors of well-known WordPress websites and newsletters. More often than not, they’ll be glad to get the word out about your project.
*   **Twitter, Facebook and Google+**.  By now, social networks seem like a no-brainer. Although there are a variety to choose from, cross-promoting across the big three generally has the best result. A simple note mentioning the release, along with a link to a blog post or landing page, is sufficient.
*   **Advertising**.  Assuming you can afford it, consider running an ad on an advertising network whose reach extends farther than your own networks.

As with anything, it comes down to what’s best for your project. That being said, don’t limit yourself to just one channel, such as social media. Try out a combination of outlets. You’ve got little to lose.</p>

## Conclusion

We’ve taken a product from inception to development and testing to pricing and support to launch and marketing. Of course, none of the solutions covered here is a silver bullet. Rather, each provides an array of options for you to leverage as you move your project forward.

Give them a try on your next project and, once it’s launched, repeat!

{{< signature "al" >}}

