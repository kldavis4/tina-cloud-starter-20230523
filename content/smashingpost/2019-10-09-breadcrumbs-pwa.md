---
title: 'How To Use Breadcrumbs On A PWA'
slug: breadcrumbs-pwa
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48bcf0ae-0013-4edb-8181-b081cf038c64/breadcrumbs-pwa.png
date: 2019-10-09T12:30:59+02:00
summary: >-
  PWAs are supposed to provide visitors with a better experience than a mobile website. But just because PWAs will use sticky navigation the way that native apps do, that doesn’t make them as easy to get around. If you’re worried that your PWA is going to be difficult to navigate without some guidance, put breadcrumbs to work. You can use them to improve navigation, readability, conversions, and more.
description: >-
  PWAs are supposed to provide visitors with a better experience than a mobile website. But just because PWAs will use sticky navigation the way that native apps do, that doesn’t make them as easy to get around. If you’re worried that your PWA is going to be difficult to navigate without some guidance, put breadcrumbs to work. You can use them to improve navigation, readability, conversions, and more.
categories:
  - PWA
  - Design
  - Mobile
---
I’ve seen a lot of questions about whether or not breadcrumbs are necessary for PWAs. It makes sense why the question is raised. After all, PWAs have an app shell and sticky menu, so shouldn’t it be easy for users to move around it without a secondary navigation?

It’s not as simple as that.

Because <a href="https://www.smashingmagazine.com/2018/11/guide-pwa-progressive-web-applications/">PWAs</a> often straddle the line <a href="https://www.smashingmagazine.com/2018/12/pwa-native-mobile-apps/">between website and native app</a>, navigation isn’t always minimized &mdash; especially if you’re building large e-commerce stores or blogs. Plus, don’t forget that breadcrumbs aren’t just for navigation. They’re often used to show progress. 

So, today, we’re going to look at how to design breadcrumbs for PWAs and some interesting use cases where they come in handy.

<div class="c-felix-the-cat">
<h4 class="h3">Will PWAs Replace Native Mobile Apps?</h4>
<p>When it comes to the mobile user experience, are mobile websites all that bad? You hear so much about the benefits of building a dedicated native app, but that can become an incredibly costly gamble if users don’t take to it. <a href="https://www.smashingmagazine.com/2018/12/pwa-native-mobile-apps/" class="btn btn--small btn--white btn--white--bordered">Read related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

One of the reasons we build PWAs instead of websites is because they offer a better mobile experience. But that doesn’t mean you can strictly rely on your visitors to use the navigation to get around. In some cases, they’re going to need a bit of hand-holding.

Breadcrumbs are a great way to step in and say:

<blockquote>Did you go too far? Let us help you backtrack a step or two.</blockquote>

<a href="https://www.yankeecandle.com/">Yankee Candle</a> shows us one way this can be done:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd4ce3c9-6646-48b8-9799-9ec50a6cb0e0/yankee-candle-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd4ce3c9-6646-48b8-9799-9ec50a6cb0e0/yankee-candle-breadcrumbs.png" sizes="100vw" caption="Yankee Candle displays a breadcrumbs navigation as visitors move deeper through its candle inventory and categories. (Source: <a href='https://www.yankeecandle.com/'>Yankee Candle</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd4ce3c9-6646-48b8-9799-9ec50a6cb0e0/yankee-candle-breadcrumbs.png'>Large preview</a>)" alt="Yankee Candle breadcrumbs navigation" >}}

Or your breadcrumbs might be saying:

<blockquote>Not sure how much further you have to go (or how much more you can take)? Here are your remaining steps.</blockquote>

The checkout process can certainly get tiresome on mobile when it’s broken into multiple steps. That’s why breadcrumbs progress bars like the one <a href="https://www.cort.com/">Cort</a> uses are so helpful.

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/700f73f0-06c7-4b44-836f-268d207f3875/cort-button-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/700f73f0-06c7-4b44-836f-268d207f3875/cort-button-breadcrumbs.png" sizes="100vw" caption="Customers looking to rent furniture from Cort are taking through a multi-step checkout process with breadcrumb dots indicating progress. (Source: <a href='https://www.cort.com/'>Cort</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/700f73f0-06c7-4b44-836f-268d207f3875/cort-button-breadcrumbs.png'>Large preview</a>)" alt="Cort breadcrumbs for progress" >}}

These aren’t the only ways you can use breadcrumbs to improve the visitor experience with a PWA. Here are some other use cases you can take advantage of:

## 1. Enhance e-Commerce Search

If you’re building a large e-commerce PWA with multiple hierarchies or categories of products, breadcrumbs are 100% necessary.

{{% pull-quote %}}
There’s just no room on mobile to display that sort of deep navigation without driving your shoppers mad.
{{% /pull-quote %}}

Breadcrumbs also make it easier for shoppers to see the steps they’ve taken, so they can determine how far back they need to skip.

For example, let’s say someone were shopping for a new moisturizer on the <a href="https://www.lancome-usa.com/">Lancôme</a> PWA:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47246496-5172-4998-bd8d-5728ba2d1e5d/lancome-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47246496-5172-4998-bd8d-5728ba2d1e5d/lancome-breadcrumbs.png" sizes="100vw" caption="The Lancôme PWA uses breadcrumbs to help shoppers backtrack more easily. (Source: <a href='https://www.lancome-usa.com/'>Lancôme</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47246496-5172-4998-bd8d-5728ba2d1e5d/lancome-breadcrumbs.png'>Large preview</a>)" alt="Lancôme PWA breadcrumbs trail" >}}

But let’s say they were looking for something they could wear during the day and hadn’t paid enough attention to the name of the product before clicking on it. Breadcrumbs, then, allow them to go to the exact spot they need to be (i.e. “Moisturizers”) to find the right category (“Day Creams”).

This type of breadcrumbs navigation becomes especially important the deeper the navigation goes.

Just be careful.

Although Yankee Candle has an example of what <em>to do</em> above, if you pry deeper into its inventory, you’ll find that it’s breadcrumbing is somewhat compromised:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/312cfd22-d330-422b-a0c6-2d45d3c49bd9/yankee-candle-long-breadcrumb.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/312cfd22-d330-422b-a0c6-2d45d3c49bd9/yankee-candle-long-breadcrumb.png" sizes="100vw" caption="As visitors go deeper into Yankee Candle’s store, the breadcrumbs go offscreen. (Source: <a href='https://www.yankeecandle.com/'>Yankee Candle</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/312cfd22-d330-422b-a0c6-2d45d3c49bd9/yankee-candle-long-breadcrumb.png'>Large preview</a>)" alt="Yankee Candle offscreen breadcrumbs" >}}

You might not be able to tell from the screenshot above, but the breadcrumbs go offscreen. And if you can’t tell that, then the visitors of the PWA aren’t going to be able to tell that either.

The extra breadcrumbs do exist. They just require visitors to scroll to the right to find them:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6006cdd-5962-4a52-91df-917bf3a640f9/yankee-candle-breadcrumb-trail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6006cdd-5962-4a52-91df-917bf3a640f9/yankee-candle-breadcrumb-trail.png" sizes="100vw" caption="Yankee Candle adds a scroll to its breadcrumb trail. (Source: <a href='https://www.yankeecandle.com/'>Yankee Candle</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6006cdd-5962-4a52-91df-917bf3a640f9/yankee-candle-breadcrumb-trail.png'>Large preview</a>)" alt="Yankee Candle breadcrumb scroll" >}}

Realistically, this could cause problems for visitors who are familiar with scrolling, but not with having to scroll individual elements like a breadcrumbs navigation.

One thing that Yankee Candle has done well in this example is that it’s preserved the size of its breadcrumbs so that they remain readable and clickable. That’s something that doesn’t always happen if you add a wrap function to the navigation.

I’ll show you why the matter of size might come up when you’re designing this element.

This is the <a href="https://www.bedbathandbeyond.com/">Bed Bath & Beyond</a> website:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc699417-0085-44ee-b299-fd5ae67b3803/bed-bath-beyond-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc699417-0085-44ee-b299-fd5ae67b3803/bed-bath-beyond-breadcrumbs.png" sizes="100vw" caption="Bed Bath & Beyond’s breadcrumbs take up about a quarter of the mobile web page. (Source: <a href='https://www.bedbathandbeyond.com/'>Bed Bath & Beyond</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc699417-0085-44ee-b299-fd5ae67b3803/bed-bath-beyond-breadcrumbs.png'>Large preview</a>)" alt="Bed Bath & Beyond’s oversized breadcrumbs" >}}

This is certainly a neat way to design your breadcrumbs, especially since the last crumb enables users to dig even deeper to categories like:

<ul>
<li>Casual Dinnerware,</li>
<li>Fine China,</li>
<li>Charger Plates.</li>
</ul>

Once the visitor selects one of the products, they’re shown a standard plain-text breadcrumbs along the top of the page. That said, this in-between “Dining | Dinnerware | Dinnerware Sets” breadcrumbs trail takes up nearly a quarter of the page. It doesn’t totally compromise the shopping experience, but it might cause undue irritation since visitors have to do a lot of scrolling to see each of the available dinnerware sets now.

Your best bet? Visitors know to look for breadcrumbs in e-commerce, whether it’s on desktop, mobile or PWA. So, don’t try and get creative with it. Place them where they belong (i.e. just under the header) and use uniform typography. If your breadcrumbs have a tendency to run on the long side, you can wrap them or, better yet, reduce how many are displayed at once.

In the Yankee Candle example above, this is what visitors see when they scroll the full width of the breadcrumb:

<p><strong>Home / Seasonal Candles / Fall Candles / Fall Jar Candles / Sweet Maple Chai Large Fall Jar Candles</strong></p>

This is what it could be instead:

<p><strong>Seasonal Candles / Fall Candles / Fall Jar Candles</strong></p>

There’s really no need to include the “Home” attribute as everyone knows the logo points there. And there’s no need to spell out the name of the product since it’s right below the breadcrumb. When you do this for your PWA, just remember to trim it back so that only the essentials appear.

{{% ad-panel-leaderboard %}}

## 2. Improve the Browsability of Blogs

When someone reads a blog from the comfort of their desktop or laptop, they usually have the convenience of a sidebar that shows them other recent or relevant articles. On mobile, though, that’s impossible. Instead, they have to:

<ul>
<li>Scroll to the bottom of the post and see if related links are available there,</li>
<li>Use the blog’s search function (if there is one),</li> 
<li>Or go to a relevant category or date using breadcrumbs.</li>
</ul>

Scrolling isn’t ideal, especially if your readers don’t always get through the full post. Search would be fine, but it requires them to have a very clear idea of what they’re looking for. Breadcrumbs, on the other hand, provides some context about what they’re reading as well as guidance for what else they can find.

The <a href="https://www.cookinglight.com/">Cooking Light</a> blog handles this well:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c4d5323-41d8-4dd0-bb4c-8053315ff105/cooking-light-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c4d5323-41d8-4dd0-bb4c-8053315ff105/cooking-light-breadcrumbs.png" sizes="100vw" caption="The Cooking Light blog uses a simplified breadcrumbs to help users find related content. (Source: <a href='https://www.cookinglight.com/'>Cooking Light</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c4d5323-41d8-4dd0-bb4c-8053315ff105/cooking-light-breadcrumbs.png'>Large preview</a>)" alt="Cooking Light content" >}}

Let’s say a visitor lands on the Cooking Light home page and sees this article about measuring how much pumpkin comes in a can. They click on it and find it a worthwhile read.

Now, someone who clicks on an article like this is likely to be a novice cook, so they’d most definitely be interested in picking up other beginner tips and insights. That’s why Cooking Light’s breadcrumb is so useful. This could’ve ended up being something like this: 

<p><strong>Home > Cooking > Thanksgiving > Pies > Pumpkin Pie</strong></p>

Instead, the article was properly and simply categorized so that the kinds of readers it attracts can find other useful and relevant content.

While you might be tempted to categorize blog posts a different way, it can over-complicate the breadcrumbs. Case in point, this is how the Transportation Security Administration (<a href="https://www.tsa.gov/">TSA</a>) does theirs:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa424d9d-133f-4e2d-b7d0-660d0829284a/tsa-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa424d9d-133f-4e2d-b7d0-660d0829284a/tsa-breadcrumbs.png" sizes="100vw" caption="The TSA designs its blog breadcrumbs using dates (years and months). (Source: <a href='https://www.tsa.gov/'>TSA</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa424d9d-133f-4e2d-b7d0-660d0829284a/tsa-breadcrumbs.png'>Large preview</a>)" alt="TSA blog breadcrumbs" >}}

In the example above, you can see that the breadcrumbs are nothing more than a breakdown of the publication date. Unless you have visitors constantly searching for time-sensitive information instead of valuable guides, this type of breadcrumb isn’t going to work very well.

Another thing I want to mention is that the inclusion of the title in the breadcrumbs is unnecessary. It’s nothing more than a duplication of the blog post title that appears directly below it. What’s more, the length of the title forces the breadcrumbs to wrap and take up more space than it needs to.

Simpler is always better, especially if the goal of the breadcrumbs is to help visitors read more of your blog content. You can use my tip from #1 about shortening your breadcrumbs to fix this issue.

## 3. Make It Easier to Get Help</h3>

One of the cool things about building products for the web is that it allows us to sell exponentially more than we could if we had to constantly stock a physical inventory. But that doesn’t release us from the responsibility of supporting our products. When you build a piece of software, you better be there to help customers with it.

That said, a lot of the problems SaaS users run into are commonplace and can easily be answered with a support portal. That way, you empower users to look up answers to their own problems and avoid clogging up your support queue. It’s a win-win for both sides.

Now, support portals are a lot like blogs in that they can be tough to get around if you don’t have the convenience of a sidebar or search bar to show you the way. Even if those elements are present, it’s still nice to have additional context as you go deeper and deeper into the support archives.

For instance, this is <a href="https://www.freshworks.com/freshsales-crm/">FreshWorks</a>’ Freshsales CRM support portal:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5529a03-9651-47b3-8568-c3d2b084ac3a/freshsales-documentation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5529a03-9651-47b3-8568-c3d2b084ac3a/freshsales-documentation.png" sizes="100vw" caption="The Freshsales support portal always keeps breadcrumbs at the top of the page for reference. (Source: <a href='https://www.freshworks.com/freshsales-crm/'>FreshWorks</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5529a03-9651-47b3-8568-c3d2b084ac3a/freshsales-documentation.png'>Large preview</a>)" alt="Freshsales support portal breadcrumbs" >}}

There is a ton of documentation in this support portal. It would be silly not to have a breadcrumbs navigation available at the top of the page. And like the blog breadcrumbs examples, this one helps users in two ways.

It’s useful for backtracking, for one. It’s also helpful for users that are trying to learn a lot more about the same subject. By providing this level of support, your users will learn how to master your product more easily and be more likely to renew their subscriptions at the end of the term.

Another software that uses breadcrumbs in its support section is <a href="https://calendly.com/">Calendly</a>:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80ed11ca-9495-446d-a640-b507c5d36cab/calendly-support-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80ed11ca-9495-446d-a640-b507c5d36cab/calendly-support-breadcrumbs.png" sizes="100vw" caption="Calendly includes too many attributes in its support breadcrumbs navigation. (Source: <a href='https://calendly.com/'>Calendly</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80ed11ca-9495-446d-a640-b507c5d36cab/calendly-support-breadcrumbs.png'>Large preview</a>)" alt="Calendly support breadcrumbs" >}}

Notice how the name of the page and category of support topics is present just below the search bar. Now, look at the attributes included in the breadcrumbs:

<p><strong>Help Center > Calendly > Getting Started > Getting Started</strong></p>

None of these belong here except “Help Center”. Anyone who’s landed on this page knows that the support topic pertains to the product (Calendly). And they’re also going to see the page title is “Getting Started”, so the duplication of it here is of no help.

Really, the breadcrumbs shouldn’t even come into play until they dig deeper in the navigation. Even then, I don’t know if it’s necessary since the title is always present at the top of the page.

When building out your own SaaS support portal, really think about what belongs in the breadcrumbs and what doesn’t. If it’s a simple enough self-support system, you might not need it at all.

## 4. Improve Conversions with Progress Bars

When you give your PWA visitors a multi-step process to work through &mdash; be it an e-commerce checkout, quiz, questionnaire and so on &mdash; don’t leave them wondering whether it’s worth it to finish.

Now, that doesn’t mean you need to overwhelm them with a long form that appears all at once &mdash; that could just as well hurt your conversion rate. It’s completely fine to break longer processes into multiple steps. Just remember to use progress bar breadcrumbs to split them up.

This is something that’ll be especially useful in hospitality as the <a href="https://www.citizenm.com/">CitizenM</a> reservation form demonstrates:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f56d1121-a5d5-487d-a84e-50546a2f3c6d/citizenm-checkout.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f56d1121-a5d5-487d-a84e-50546a2f3c6d/citizenm-checkout.png" sizes="100vw" caption="When booking a reservation at the CitizenM hotel, visitors see exactly how much more work is ahead of them with breadcrumbs. (Source: <a href='https://www.citizenm.com/'>CitizenM</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f56d1121-a5d5-487d-a84e-50546a2f3c6d/citizenm-checkout.png'>Large preview</a>)" alt="CitizenM progress bar breadcrumbs" >}}

These breadcrumbs serve two purposes:

<ol>
<li>Visitors can see how much work is actually involved in the process.</li>
<li>They can use them to backtrack if they need to change a response.</li>
</ol>

This can make what might otherwise seem like a never-ending booking process more manageable. But that doesn’t mean that breadcrumbs, as a whole, always contribute to higher conversions.

Part of the reason the breadcrumbs example above works so well is because it’s well-labeled and simplified. When you remove the transparency and logic from breadcrumbs progress bars, though, they can end up harming your conversion rates. 

For example, <a href="https://www.ipsy.com/">Ipsy</a> is a monthly makeup subscription service. In order to get started, visitors to the PWA must fill out this quiz:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf34bc3-3e08-441e-abc1-f67a815c79f5/ipsy-button-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf34bc3-3e08-441e-abc1-f67a815c79f5/ipsy-button-breadcrumbs.png" sizes="100vw" caption="Ipsy requires new users to fill out a beauty quiz before they can subscribe. (Source: <a href='https://www.ipsy.com/'>Ipsy</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf34bc3-3e08-441e-abc1-f67a815c79f5/ipsy-button-breadcrumbs.png'>Large preview</a>)" alt="Ipsy quiz with breadcrumbs" >}}

While the design of the quiz is certainly attractive, is it necessary to have built it this way, especially since there are 12 pages that require two clicks or more on each page? That comes to <em>at least</em> 24 clicks in total (one or more for the answer and one for the “Next” button).

That doesn’t even include filling out the subscription form!

That said, the breadcrumbs progress bar is there to show potential customers how much more work is to be done. However, there’s no transparency over what each of those pages involves. In fact, most of them are much longer than this first one, asking for things like favorite name brands, types of makeup they like, how frequently they wear it, etc.

In the end, it’ll probably take five minutes or more to complete the quiz and I don’t think the progress bar does any good in demonstrating that fact.

<p><strong>Bottom line:</strong> If you want to get visitors to the point of conversion more quickly, design it that way. And if it does require some work on their part, be honest about how much work there is. Don’t mask it with breadcrumbs.</p>

{{% ad-panel-leaderboard %}}

## 5. Make Directories Easier to Explore

Thankfully, directories no longer live inside of massive phone books or travel guides. We now digitize those directories for quicker and more convenient consumption.

That said, online directories are a lot like big data. Now that they’re on the web, there’s almost too much information to sift through. And while most PWAs give visitors the ability to filter and sort their results, that doesn’t necessarily help with moving around the PWA itself.

What you need for that is breadcrumbs.

You’ll find a nice example of this on the <a href="https://www.opentable.com/">OpenTable</a> PWA:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e04d49e1-66de-4c13-a3c3-ec788ebe9a6a/opentable-location-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e04d49e1-66de-4c13-a3c3-ec788ebe9a6a/opentable-location-breadcrumbs.png" sizes="100vw" caption="OpenTable displays location breadcrumbs to users as they search for and book reservations. (Source: <a href='https://www.opentable.com/'>OpenTable</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e04d49e1-66de-4c13-a3c3-ec788ebe9a6a/opentable-location-breadcrumbs.png'>Large preview</a>)" alt="OpenTable location breadcrumbs" >}}

There are hundreds of thousands of restaurants using OpenTable as their reservation system &mdash; and from locations all over the world.

While it might not be totally necessary to show breadcrumbs, especially if users know exactly which city they want to dine in, it’s a nice touch. It serves as a quick reminder to users that this is the location they’re searching in. If they change their mind and want to try the next town over, all it takes is a click back to the state or province to change their response. 

<a href="https://www.tripadvisor.com/">TripAdvisor</a> is another massive directory site, this one storing massive amounts of data on locations, places to stay, things to do, etc. There’s just so much going on inside this PWA that there’s no way to get by without breadcrumbs:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0590957e-876b-4534-8eaf-acbc1ffab4fb/trip-advisor-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0590957e-876b-4534-8eaf-acbc1ffab4fb/trip-advisor-breadcrumbs.png" sizes="100vw" caption="The TripAdvisor travel directory PWA uses breadcrumbs to break down the attributes of a search. (Source: <a href='https://www.tripadvisor.com/'>TripAdvisor</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0590957e-876b-4534-8eaf-acbc1ffab4fb/trip-advisor-breadcrumbs.png'>Large preview</a>)" alt="TripAdvisor PWA breadcrumbs" >}}

In this example, you can see how deep and specific the breadcrumbs attributes get:

<p><strong>Things to Do > Tickets & Tours > Water Sports > Hanauma Bay Snorkeling Service</strong></p>

This is useful for visitors that may have stumbled upon a particular activity or location, but, upon inspecting the breadcrumbs, realize there’s a different way to go.

For instance, let’s say someone gets to this page and starts wondering what other kinds of tours they can do in Hawaii. So, rather than restart their search (which they’d have to do if they landed on the page from the home page), they can use the breadcrumbs to backtrack.

That said, this is another one of those examples of putting too much into the breadcrumbs. There’s no need to include the name of the activity or location unless there are sub-categories beneath it. It only makes the breadcrumbs run past the width of the page, which can be distracting (and annoying).

Again, it’s a good idea to keep breadcrumbs as simple as possible when you can.

## 6. Convert Anchor Tags into Breadcrumbs

Earlier, I talked about how breadcrumbs can be used as progress bars on PWAs. What if we were to use them for a similar purpose, but this time to represent the anchor tags on a page?

It’s really no different than what developers do when they build a navigation into the top of a single-page website. The only difference is that the anchor tags from your page will be represented by breadcrumbs as a secondary navigation.

And if you’re publishing lengthy articles or guides on your PWA, this is something to seriously think about.

Here’s one example from the <a href="https://www.webmd.com/">WebMD</a> website:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcaa3975-c4a1-4fa8-95db-62b005ab9a42/webmd-secondary-nav.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcaa3975-c4a1-4fa8-95db-62b005ab9a42/webmd-secondary-nav.png" sizes="100vw" caption="WebMD turns its anchor tags into a sort of breadcrumbs navigation. (Source: <a href='https://www.webmd.com/'>WebMD</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcaa3975-c4a1-4fa8-95db-62b005ab9a42/webmd-secondary-nav.png'>Large preview</a>)" alt="WebMD breadcrumbs navigation for anchor tags" >}}

The WebMD PWA allows visitors to check their symptoms or look up medications they’re taking. As you might imagine, these pages can go on and on for a while.

Rather than force visitors to scroll through them, WebMD attaches this secondary navigation to the bottom of its header. As visitors scroll past the corresponding anchor tag and section, it gets highlighted in the breadcrumbs. Users can also use the breadcrumbs to quickly move around the page without having to scroll.

<a href="https://www.airbnb.com/">Airbnb</a> does something similar:

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfb64f3a-efb7-4b4b-a5de-bb593530c82e/airbnb-secondary-nav.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfb64f3a-efb7-4b4b-a5de-bb593530c82e/airbnb-secondary-nav.png" sizes="100vw" caption="Airbnb creates a breadcrumbs navigation from its anchor tags. (Source: <a href='https://www.airbnb.com/'>Airbnb</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfb64f3a-efb7-4b4b-a5de-bb593530c82e/airbnb-secondary-nav.png'>Large preview</a>)" alt="Airbnb breadcrumbs navigation" >}}

Airbnb could easily just leave its visitors to scroll through the page to try to pull out the details most relevant to them. Instead, it’s chosen to display a breadcrumbs navigation (built from the page’s anchor tags).

This makes it easy for them to see which section they’re in and then bounce around as they like to pick up the details they need to make their decision.

I know it’s not necessarily a common use of breadcrumbs, but I expect this one to appear more and more as the web shifts over to PWAs.

## Wrapping Up</h3>

We’ve seen a lot of examples of PWAs now to know what good and bad breadcrumbs look like. Let’s sum up the basic rules:

<ul>
<li>Always place the breadcrumbs as close to the top of the page as possible. If the header is present, it goes directly below. If it’s not, it should take the top spot.</li>
<li>Use unique separators. The most common ones are the Guillemet (>), slash (/) and the pipe (|).</li>
<li>Build enough padding around the separators so it’s clear where the attributes start and end.</li>
<li>Make sure clickable links in breadcrumbs are big enough to tap. <a href="https://www.nngroup.com/articles/touch-target-size/">At minimum, they should be 1 cm x 1 cm.</a></li>
<li>Be careful with color. You don’t want breadcrumbs to distract from the content of the page. That said, they should at least change color or become underlined upon hover.</li>
<li>Simplify the attribute labels as much as possible.</li>
<li>Don’t include the name of the post, page, product, etc. in the breadcrumbs if it’s clearly visible on the page. “Home” probably doesn’t need to be there either.</li>
<li>If the breadcrumbs tend to run past the width of the page, wrap the text only if it doesn’t compromise clickability. It’s really best to display only the last few attributes/links.</li>
</ul>

There’s a lot you can do with breadcrumbs on PWAs and, if handled well, can help you increase your conversion rate. Just be careful with them. If they’re included without just cause or they present more work to your visitors, it’s best to just do without them.

{{< signature "ra, yk, il" >}}
