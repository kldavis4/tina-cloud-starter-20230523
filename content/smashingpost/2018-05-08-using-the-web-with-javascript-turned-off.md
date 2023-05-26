---
title: 'I Used The Web For A Day With JavaScript Turned Off'
slug: using-the-web-with-javascript-turned-off
author: chrisbashton
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49029a7b-1626-4aca-a420-2841f27b0691/web-with-no-js-14.png
date: 2018-05-08T14:30:10+02:00
summary: >-
  Have you ever wondered whether it's possible to do anything on the web without JavaScript? How many sites use progressive enhancement in practice? Chris Ashton did an experiment to find out.
description: >-
  Have you ever wondered whether it's possible to do anything on the web without JavaScript? How many sites use progressive enhancement in practice? Chris Ashton did an experiment to find out.
categories:
  - JavaScript
  - Usability
  - Accessibility
  - UX
---
This article is part of a series in which I attempt to use the web under various constraints, representing a given demographic of user. I hope to raise the profile of difficulties faced by real people, which are avoidable if we design and develop in a way that is sympathetic to their needs. This week, I’m disabling JavaScript.

## Why `noscript` Matters

Firstly, to clarify, there’s a difference between supporting a `noscript` experience and using the `noscript` tag. I don’t generally like the `noscript` tag, as it fragments your web page into JavaScript and non-JavaScript versions rather than working from the same baseline of content, which is how experiences get messy and things get overlooked.

You may have lots of useful content inside your `noscript` tags, but if I’m using a JavaScript-enabled browser, I’m not going to see any of that &mdash; I’m going to be stuck waiting for the JS experience to download. When I refer to the ‘noscript’ experience, I generally mean **the experience of using the web page without JavaScript**, rather than the explicit use of the tag.

<div class="c-felix-the-cat">
<h4 class="h3">Web MIDI API: Getting Started</h4>
<p>Is it possible to use digital musical instruments as browser inputs? With the Web MIDI API, the answer is yes! The best part is, it’s fairly quick and easy to implement and even create a really fun project.  <a href="https://www.smashingmagazine.com/2018/03/web-midi-api/">Read article&nbsp;&rarr;</a></p>
</div>

So, who cares about users who don’t have JavaScript? Do such `noscript` users even exist anymore?

Well, they do exist, albeit in small numbers: [roughly 0.2% of users in the UK](https://blockmetry.com/blog/javascript-disabled) have JavaScript disabled. But looking at the numbers of users who have explicitly disabled JavaScript is missing the point.

I’m reminded of this quote by Jake Archibald:

<blockquote>“All your users are non-JS while they’re downloading your JS.”</blockquote>

Think of those users who have JavaScript enabled but who don’t get the JavaScript experience, for any number of reasons, including corporate or local blocking or stripping of JavaScript elements, existing JavaScript errors in the browser from browser add-ons and toolbars, network errors, and so on. BuzzFeed recently revealed that [around 1% of requests for their JavaScript time out](https://twitter.com/philhawksworth/status/990890920672456707), equating to 13 million failed requests per month.

{{% feature-panel %}}

Sometimes the issue isn’t with the user but with the CDN delivering the JavaScript. Remember in February 2017 when [Amazon’s servers went down](https://aws.amazon.com/message/41926/)? Millions of sites that rely on JavaScript delivered over Amazon’s CDNs were in major trouble, [costing companies in the S&P 500 index $150 million](https://www.npr.org/sections/thetwo-way/2017/03/03/518322734/amazon-and-the-150-million-typo) in the four-hour outage.

Think also of the emerging global markets; countries still battling to build a network of fast internet, with populations unable to afford fast hardware to run CPU-intensive JavaScript. Or think of the established markets, where even an iPhone X on a 4G connection is not immune to the effects of a partially loaded webpage interrupted by their train going into a tunnel.

The web is a hostile, unpredictable environment, which is why many developers follow the [principle of progressive enhancement](https://www.smashingmagazine.com/2009/04/progressive-enhancement-what-it-is-and-how-to-use-it/) to build their sites up from a core experience of semantic HTML, layering CSS and [unobtrusive JavaScript](https://www.w3.org/wiki/The_principles_of_unobtrusive_JavaScript) on top of that. I wanted to see how many sites apply this in practice. What better way than disabling JavaScript altogether?

## How To Disable JavaScript

If you’d like to recreate my experiment for yourself, you can disable JavaScript by digging into the settings in Chrome:

- Open the Developer Tools (Chrome -> View -> Developer Tools, or ⌥⌘I on the keyboard)
- Open the developer submenu (the three dots next to the close icon on the Developer Tools)
- Choose ‘Settings’ from this submenu
- Find the ‘Debugger’ section and check the ‘Disable JavaScript’ box

Or, like me, you can use the excellent [Toggle JavaScript Chrome Extension](https://chrome.google.com/webstore/detail/toggle-javascript/cidlcjdalomndpeagkjpnefhljffbnlo) which lets you disable JS in one click.

## Creating A WordPress Post With JavaScript Disabled

After disabling JavaScript, my first port of call was to go to my personal portfolio site &mdash; which runs on WordPress &mdash; with the aim of writing down my experiences in real time.

WordPress is actually very noscript-friendly, so I was able to start writing this post without any difficulty, although it was missing some of the text formatting and media embedding features I’m used to.

Let's compare WordPress’ post screen with and without JavaScript:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4405d58-16c4-4bd1-8b0c-d39e69248163/web-with-no-js-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4405d58-16c4-4bd1-8b0c-d39e69248163/web-with-no-js-1.png" sizes="100vw" caption="The <code>noscript</code> version of WordPress’ post page, which is made up of two basic text inputs." alt="The Noscript version of WordPress’ post page, which is made up of two basic text inputs." >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85d319a0-3b28-4d23-8ad8-8b08cd0bcd76/web-with-no-js-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85d319a0-3b28-4d23-8ad8-8b08cd0bcd76/web-with-no-js-2.png" sizes="100vw" caption="The JavaScript version contains shortcuts for formatting text, embedding quotes and media, and previewing the content as HTML." alt="The JavaScript version contains shortcuts for formatting text, embedding quotes and media, and previewing the content as HTML." >}}

I felt quite comfortable without the toolbars until I needed to embed screenshots in my post. Without the ‘Add Media’ button, I had to go to separate screens to upload my files. This makes sense, as ‘background uploading’ content requires Ajax, which requires JavaScript. But I was quite surprised that the separate media screen also required JavaScript!

Luckily, there was a fallback view:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e9b41da-91f7-419f-bf0a-262d58c97a31/web-with-no-js-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e9b41da-91f7-419f-bf0a-262d58c97a31/web-with-no-js-3.png" sizes="100vw" caption="The <code>noscript</code> version of the Media section in the admin backend. I was warned that the grid view was not supported without JavaScript." alt="WordPress media grid view (requires JS)" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4af92eb7-6f35-4e82-a202-7a551bbf05bd/web-with-no-js-4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4af92eb7-6f35-4e82-a202-7a551bbf05bd/web-with-no-js-4.png" sizes="100vw" caption="Who needs grids anyway? The list view was perfectly fine for my needs." alt="WordPress media list view (fallback)" >}}

After uploading the image, I had to manually write an HTML `img` tag in my post and copy and paste the image URL into it. There was no way of determining the thumbnail URL of the uploaded image, and any captions I wrote also had to be manually copied. I soon got fed up of this approach and planned to come back the next day and re-insert all of the images when I allowed myself to use JavaScript again.

I decided to take a look at how the front-end of my site was doing.

## Viewing My Site Without JavaScript

I was pleasantly surprised that my site looked largely the same without JS:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc39549b-1e1e-4e04-b351-075503b8a745/web-with-no-js-5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc39549b-1e1e-4e04-b351-075503b8a745/web-with-no-js-5.png" sizes="100vw" caption="Personal site with JavaScript." alt="With JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0697b178-37ef-4f4b-b2c0-ac892ae9e59c/web-with-no-js-6.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0697b178-37ef-4f4b-b2c0-ac892ae9e59c/web-with-no-js-6.png" sizes="100vw" caption="Personal site without JavaScript. Only the Twitter embed looks any different." alt="Without JavaScript" >}}

Let’s take a closer look at that Twitter embed:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50f59b31-87a4-4165-9831-392874d998e4/web-with-no-js-7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50f59b31-87a4-4165-9831-392874d998e4/web-with-no-js-7.png" sizes="100vw" caption="Note the author information, engagement stats, and information link that we don’t get with the <code>noscript</code> version. The ‘tick’ is an external PNG. (<a href='https://twitter.com/heydonworks/status/969520320754438144'>Source</a>)" alt="Tweet with JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eede9681-3fcd-41b8-b370-1e407f8f87c6/web-with-no-js-8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eede9681-3fcd-41b8-b370-1e407f8f87c6/web-with-no-js-8.png" sizes="100vw" caption="Missing styles, but contains all of the content, including hashtag link and link to tweet. The ‘tick’ is an ASCII character: ✔." alt="Tweet without JavaScript" >}}

Below the fold of my site, I’ve also embedded some Instagram content, which held up well to the `noscript` experience.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b97997a-ed53-4622-a749-876d15a2525c/web-with-no-js-9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b97997a-ed53-4622-a749-876d15a2525c/web-with-no-js-9.png" sizes="100vw" caption="Notice the slideshow dots underneath the image, indicating there are more images in the gallery." alt="Instagram embed with JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca3b40a-8a79-473d-9f77-59f0ae025aad/web-with-no-js-10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca3b40a-8a79-473d-9f77-59f0ae025aad/web-with-no-js-10.png" sizes="100vw" caption="The noJS version doesn’t have such dots. Other than the missing slideshow functionality, this is indistinguishable from the JS version." alt="Instagram embed without JavaScript" >}}

Finally, I have a GitHub embed on my site. GitHub doesn’t offer a native embed, so I use the unofficial [GitHub Cards by Hsiaoming Yang](https://lab.lepture.com/github-cards/).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647cfcbb-a5e8-4b3b-b441-3e7eba893ab6/web-with-no-js-11.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/647cfcbb-a5e8-4b3b-b441-3e7eba893ab6/web-with-no-js-11.png" sizes="100vw" caption="The unofficial card gives a nice little snapshot and links to your GitHub profile." alt="GitHub embed with JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4f54507-41a8-454d-a889-4b70e0a87ff5/web-with-no-js-12.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4f54507-41a8-454d-a889-4b70e0a87ff5/web-with-no-js-12.png" sizes="100vw" caption="I provide a fallback link to GitHub if no JavaScript is available." alt="GitHub embed without JavaScript" >}}

I was half hoping to shock you with the before and after stats (_megabytes of JS for a small embed! End of the world! Let’s ditch JavaScript!_), and half hoping there’d by very little difference (_progressive enhancement! Leading by example! I’m a good developer!_).

Let’s compare page weights with and without JavaScript. Firstly, with JavaScript:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9dc35e2-d36d-48ee-b5c6-596207371175/web-with-no-js-13.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9dc35e2-d36d-48ee-b5c6-596207371175/web-with-no-js-13.png" sizes="100vw" caption="51 HTTP requests, with 1.9MB transferred." alt="Page weight with JavaScript" >}}

Now without JavaScript:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49029a7b-1626-4aca-a420-2841f27b0691/web-with-no-js-14.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49029a7b-1626-4aca-a420-2841f27b0691/web-with-no-js-14.png" sizes="100vw" caption="18 HTTP requests, with 1.3MB transferred." alt="Page weight without JavaScript" >}}

For the sake of a styled tweet, a GitHub embed and a full-fat Instagram embed, my site grows an extra 600KB. I’ve also got Google analytics tracking and some [nerdy hidden interactive features](https://github.com/chrisbashton/js-terminal). All things considered, 600KB doesn’t seem over the top &mdash; though I am a little surprised by the number of additional requests the browser has to make for all that to happen.

All the content is still there without JavaScript, all the menus are still navigable, and with the exception of the Twitter embed, you’d be hard-pressed to realize that JavaScript is turned off. As a result, my site passes the NOSCRIPT-5 level of validation &mdash; the very best non-JavaScript rating possible.

**ashton.codes `noscript` rating: NOSCRIPT-5. ✅**

What’s that? You haven’t heard of the `noscript` classification system? I’d be very surprised if you had because I just made it up. It’s my handy little indicator of a site’s usability without JavaScript, and by extension, it’s a pretty good indicator of how good a site is at progressively enhancing its content.

## `noscript` Classification System

Websites &mdash; or more accurately, their individual pages &mdash; tend to fall into one of the following categories:

- **NOSCRIPT-5**  
The site is virtually indistinguishable from the JavaScript-enabled version of the site.
- **NOSCRIPT-4**  
The site provides functionality parity for noscript, but links to or redirects to a _separate version_ of the site to achieve that.
- **NOSCRIPT-3**  
Site largely works without JavaScript, but some non-key features are unsupported or look broken.
- **NOSCRIPT-2**  
The site offers message saying their browser is not supported.
- **NOSCRIPT-1**  
The site appears to load, but the user is unable to use key functionality at all.
- **NOSCRIPT-0**  
The site does not load at all and offers no feedback to the user.

Let’s look at some popular sites and see how they score.

## Amazon

I’ve had my eye on a little robotic vacuum cleaner for a while. My lease doesn’t allow any pets, and this is the next best thing once you put some googly eyes on it.

At first glance, Amazon does a cracking job with its non-JavaScript solution, although the main product image is missing.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d66e774b-3468-4106-abee-3eda436b87a4/web-with-no-js-16.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d66e774b-3468-4106-abee-3eda436b87a4/web-with-no-js-16.png" sizes="100vw" caption="Missing the main image, but unmistakably Amazon." alt="Amazon without JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df16295-6f98-4d34-80b3-b8d192852622/web-with-no-js-15.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df16295-6f98-4d34-80b3-b8d192852622/web-with-no-js-15.png" sizes="100vw" caption="With JavaScript, we get the main image. Look at this lovely little vacuum." alt="Amazon with JavaScript" >}}

On closer inspection, quite a few things were a bit broken on the `noscript` version. I’d like to go through them one by one and suggest a solution for each.

## No Gallery Images

I wanted to see some pictures of the products, but clicking on the thumbnails gave me nothing.

### Issue

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a3beb3-15b7-4346-9692-a4c5a9959756/web-with-no-js-17.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a3beb3-15b7-4346-9692-a4c5a9959756/web-with-no-js-17.png" sizes="100vw" caption="I clicked on these thumbnails but nothing happened." alt="Issue" >}}

### Potential Solution

It would have been nice if these thumbnails were **links to the full image, opening in a new tab. They could then be progressively enhanced** into the image gallery by using JavaScript:

- Hijack the click event of the thumbnail link;
- Grab the `href` attribute;
- Update the `src` attribute of the main image with the `href` attribute value.

### The ‘Report Incorrect Product Information’ Link Is JavaScript-Only

Is this feature really so commonly used that it’s worth downloading extra bytes of JavaScript to all of your users so that it opens as an integrated modal within the page?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/044fd83b-8826-468f-a420-491695ef71ee/web-with-no-js-19.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/044fd83b-8826-468f-a420-491695ef71ee/web-with-no-js-19.png" sizes="100vw" caption="Amazon integrated modal window (JavaScript version)" alt="Issue" >}}

### Issue

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33a44264-217e-486e-892b-815e1a3f8fb6/web-with-no-js-18.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33a44264-217e-486e-892b-815e1a3f8fb6/web-with-no-js-18.png" sizes="100vw" caption="It’s a good thing the product information looked accurate to me, because there was no way I could report any issues! The `href` attribute had a value of <code>javascript://</code>, which opens an integrated modal form" alt="Potential solution" >}}

### Potential Solution

The Amazon integrated modal form requires JavaScript to work. I would **make the ‘report feature’ a standalone form on a separate URL**, e.g. `/report-product?product-id=123`. This could be progressively enhanced into the integrated modal using Ajax to download the HTML separately.

### Reviews Are Only Partially Visible By Default

### Issue

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61925e3b-c200-41ea-84d5-55d3b475a622/web-with-no-js-20.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61925e3b-c200-41ea-84d5-55d3b475a622/web-with-no-js-20.png" sizes="100vw" caption="The Read more link does nothing." alt="Potential solution" >}}

### Potential Solution

Why not **show the whole review by default and then use JavaScript to truncate** the review text and add the ‘Read more’ link?

It’s worth pointing out that the review title is a link to the review on a standalone page, so it is at least still possible to read the content.

On the whole, I was actually pleasantly surprised just how well the site worked without JavaScript. It could just as easily have been a blank white page. However, the lack of product images means we’re missing out on a really core feature &mdash; I’d argue it’s critical to be able to see what you’re buying! &mdash; so it’s a shame we couldn’t put the icing on the cake and award it a NOSCRIPT-5 rating.

**Amazon `noscript` rating: NOSCRIPT-3. 🤷‍**

I still hadn’t decided which product I wanted to buy, so I turned to Camel Camel Camel, the Amazon price tracker.

## Camel Camel Camel

I wanted to decide between the iLife V3s Pro versus the iLife A4s, so headed over to https://uk.camelcamelcamel.com/. At first, the site looked indistinguishable from the JavaScript-enabled version.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f31d9f8-49fe-458e-a37d-4a0fed009379/web-with-no-js-22.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f31d9f8-49fe-458e-a37d-4a0fed009379/web-with-no-js-22.png" sizes="100vw" caption="Camel Camel Camel, looking nice and professional &mdash; with no JavaScript." alt="Potential Solution" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd43f7bf-540d-44f0-a7fa-c381e4e8785f/web-with-no-js-21.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd43f7bf-540d-44f0-a7fa-c381e4e8785f/web-with-no-js-21.png" sizes="100vw" caption="You could run a git diff on these screenshots and struggle to see the difference!" alt="no JavaScript issue" >}}

Unfortunately, the price history chart did not render. It did provide an alt text fallback, but the alt text did not give me any idea of whether or not the price trend has been going up or down.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd59dc46-3430-4701-8114-c4e86fbcfcd3/web-with-no-js-24.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd59dc46-3430-4701-8114-c4e86fbcfcd3/web-with-no-js-24.png" sizes="100vw" caption="Alt text says “Amazon price history chart” but provides no insight into the data." alt="Noscript version" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b018fcef-8bb5-417a-926e-68c9cde8c920/web-with-no-js-23.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b018fcef-8bb5-417a-926e-68c9cde8c920/web-with-no-js-23.png" sizes="100vw" caption="Look at this lovely chart you get when JavaScript is enabled." alt="JavaScript version" >}}

General suggestion: **provide meaningful alt text at all times**. I don’t necessarily need to see the chart, but I would appreciate a summary of what it contains. Perhaps, in this case, it might be “Amazon price history chart showing that the price of this item has remained largely unchanged since March 2017.” But automatically generating a summary like that is admittedly difficult and prone to anomalies.

Specific suggestion for this use case: **show the image**. The chart on the scripted version of the site is actually a [standalone image](https://charts.camelcamelcamel.com/uk/B01M27CSMI/new.png?force=1&amp;zero=0&amp;w=725&amp;h=440&amp;desired=false&amp;legend=1&amp;ilt=1&amp;tp=all&amp;fo=0&amp;lang=en), so there’s no reason why it couldn’t be displayed on the `noscript` version!

Still, the core content below the chart gave me the information I needed to know.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12badd3c-bfb6-4a86-979d-6cbea198983f/web-with-no-js-25.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12badd3c-bfb6-4a86-979d-6cbea198983f/web-with-no-js-25.png" sizes="100vw" caption="Who needs a chart? We’ve got a table!" alt="Who needs a chart? We’ve got a table!" >}}

The table provides the feature parity needed to secure a NOSCRIPT-5 rating. I take my hat off to you, Camel Camel Camel!

**Camel Camel Camel `noscript` rating: NOSCRIPT-5 ✅**

## Google Products

At this point in my day, I received a phone call out of the blue: A friend phoned me and asked about meeting up this week. So I went to Google Calendar to check my availability. Google had other ideas!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/994cdd03-d9c5-422d-a0d2-b9110b1bf023/web-with-no-js-26.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/994cdd03-d9c5-422d-a0d2-b9110b1bf023/web-with-no-js-26.png" sizes="100vw" caption="Surprisingly, Google Calendar offers nothing for <code>noscript</code> users." alt="Issue" >}}

I was disappointed that there wasn’t a `noscript` fallback &mdash; Google is usually pretty good at this sort of thing.

I wouldn’t expect to necessarily be able to add/edit/delete entries to my calendar, but it should be possible to **provide a read-only view of my calendar as core content**.

**Google calendar `noscript` rating: NOSCRIPT-0 🔥**

Interested in seeing how Google manages other products, I had a quick look at Google Spreadsheets:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee08d3c1-e5d6-4b79-aeea-9839df0be859/web-with-no-js-27.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee08d3c1-e5d6-4b79-aeea-9839df0be859/web-with-no-js-27.png" sizes="100vw" caption="Google Spreadsheets shows my spreadsheet but has a big warning message saying “JavaScript isn’t enabled” and won’t let me edit its contents." alt="Issue" >}}

In this case, the site fails a lot more gracefully. I can at least read the spreadsheet contents, even if I can’t edit them. Why doesn’t the calendar offer the same fallback solution?

I have no suggestions to improve Google Spreadsheets! It does a good job at **informing the user if core functionality is missing** from the `noscript` experience.

**Google spreadsheets `noscript` rating: NOSCRIPT-2 😅**

This rating isn’t actually that bad! Not all sites are going to be able to offer a `noscript` experience, but at least if they’re upfront and honest (i.e. they'll say “yeah, we’re not going to try to give you anything”) that prepares you &mdash; the `noscript` user &mdash; for when it fails. You won’t waste a few precious seconds trying to fill in a form that won’t ever submit, or start reading an article that then has to use Ajax to retrieve the rest of its contents.

Now, back to my potential Amazon purchase. I wanted to look at some third-party reviews before making a purchase.

Google search works really well without JavaScript. It just looks a little dated, like those old desktop-only sites at fixed resolutions.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da776be-1e75-4ef6-8a6f-55e3275f47b2/web-with-no-js-29.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da776be-1e75-4ef6-8a6f-55e3275f47b2/web-with-no-js-29.png" sizes="100vw" caption="<code>noscript</code> version has extra search options on the left (otherwise tucked away in settings on the JS version) &mdash; and no privacy banner (perhaps because ‘tracking’ is not relevant to <code>noscript</code> users?)" alt="Noscript version" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c6d9e9b-a458-4ac8-9713-c75dbcff78d6/web-with-no-js-28.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c6d9e9b-a458-4ac8-9713-c75dbcff78d6/web-with-no-js-28.png" sizes="100vw" caption="JavaScript version has the ability to search via voice input, and the ‘privacy reminder’ message." alt="JavaScript version" >}}

The images view looks even more different, and I actually _prefer_ it in a few ways &mdash; this version loads super quickly and lists the dimensions and image size in kilobytes underneath each thumbnail:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f62ddc7e-d2a4-4438-ac8c-e4b8ba1718bb/web-with-no-js-31.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f62ddc7e-d2a4-4438-ac8c-e4b8ba1718bb/web-with-no-js-31.png" sizes="100vw" caption="<code>noscript</code> version: notice the image meta information which is not supplied on the scripted version!" alt="Noscript version" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2716f197-95f1-48d2-8f9a-a9e57ecf7c06/web-with-no-js-30.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2716f197-95f1-48d2-8f9a-a9e57ecf7c06/web-with-no-js-30.png" sizes="100vw" caption="JavaScript version: notice the ‘related search terms’ area which is not supplied on the <code>noscript</code> version." alt="JavaScript version" >}}

**Google Search `noscript` rating: NOSCRIPT-5 ✅**

One of the search results took me to a review on YouTube. I clicked, not expecting much. I was right not to get excited:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb0e52aa-1c51-4811-8fa6-42faf7bacd30/web-with-no-js-32.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb0e52aa-1c51-4811-8fa6-42faf7bacd30/web-with-no-js-32.png" sizes="100vw" caption="YouTube doesn’t offer much of a <code>noscript</code> experience." alt="Issue" >}}

I wouldn’t really expect a site like YouTube to work without JavaScript. YouTube requires advanced streaming capabilities, not to mention that it would open itself up to copy theft if it provided a standalone MP4 download as a fallback. In any case, no site should look broken. I stared at this screen for a few seconds before realizing that nothing else was going to happen.

**Suggestion**: *If your site is not able to provide a fallback solution for `noscript` users, at a minimum you should provide a `noscript` warning message.*

**YouTube `noscript` rating: NOSCRIPT-0 🔥**

## Which?

I clicked a couple more review links. The _Which?_ advice site failed me completely.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbd02077-70f0-43fc-87b8-3a12ca9bf544/web-with-no-js-33.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbd02077-70f0-43fc-87b8-3a12ca9bf544/web-with-no-js-33.png" sizes="100vw" caption="The site says there are 10 good vacuums to choose from, but the list is clearly populated with Ajax or something as I’m seeing nothing." alt="Issue" >}}

This was a page that looked like it loaded fine, but only when you read the content would you realize you must actually be missing some key information. That key information is absolutely core to the purpose of the page, and I can’t get it. Therefore, unfortunately, that’s a NOSCRIPT-1 violation.

**Suggestion**: *If your site Ajaxes in content, that content exists at another URL. Provide a link to that content for your `noscript` users. You can always hide the link when you’ve successfully Ajaxed with JavaScript.*

**Which? review site `noscript` rating: NOSCRIPT-1 😫**

## Facebook

Eventually, I concede that I can’t really afford a vacuum right now. So, I decided to hop onto social media.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/036a04f4-0315-49de-a7c3-f5f2c821d719/web-with-no-js-34.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/036a04f4-0315-49de-a7c3-f5f2c821d719/web-with-no-js-34.png" sizes="100vw" caption="Facebook says JavaScript is required to proceed, or we can click the link to the mobile site." alt="Facebook says JavaScript is required to proceed, or we can click the link to the mobile site." >}}

Facebook flat-out refuses to load without JavaScript, but it does offer a fallback option. Here’s our first example of a NOSCRIPT-4 &mdash; a site which offers a separate version of its content for `noscript` or feature phone users.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bed1dec2-bb71-4147-85f1-1c608201024f/web-with-no-js-35.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bed1dec2-bb71-4147-85f1-1c608201024f/web-with-no-js-35.png" sizes="100vw" caption="The mobile site version of Facebook." alt="The mobile site version of Facebook." >}}

The mobile version loads instantly. It looks ugly, but it seems as though I get the same content as I normally would. Crucially, I have _feature parity_: I can accomplish the same things here as I can on the main site.

**Facebook `noscript` rating: NOSCRIPT-4 🤔**

The page loaded at lightning speed:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070c291e-65be-4689-8ba9-3548d4fa3d21/web-with-no-js-36.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/070c291e-65be-4689-8ba9-3548d4fa3d21/web-with-no-js-36.png" sizes="100vw" caption="50.8KB. Page loaded in 1.39 seconds" alt="50.8KB. Page loaded in 1.39 seconds" >}}

I could only see 7 items in the news feed at any one time, but I could click to “See More Stories,” which takes me to a new page, using traditional pagination techniques.

I find myself impressed that I have the option to ‘react’ to a Facebook comment, though this is a multi-screen task:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b77c5937-6c7c-4d1e-ac6b-1e21dd4185f2/web-with-no-js-37.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b77c5937-6c7c-4d1e-ac6b-1e21dd4185f2/web-with-no-js-37.png" sizes="100vw" caption="Reacting first requires you to click ‘React’…" alt="Reacting first requires you to click ‘React’…" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1c7cf4-d64b-4a3f-8468-1d43cbc51d86/web-with-no-js-38.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1c7cf4-d64b-4a3f-8468-1d43cbc51d86/web-with-no-js-38.png" sizes="100vw" caption="…which then takes you to a separate screen to choose your reaction." alt="…which then takes you to a separate screen to choose your reaction." >}}

There’s nothing stopping Facebook building a hover ‘reaction’ menu in non-JavaScript, but to be fair this is aimed at mobile devices that aren’t able to hover.

**Suggestion**: *Get creative with CSS. You may find that you don’t need JavaScript at all.*

Before long, a video item came up in my news feed. (At this point, it dawned on me just how much less video content I had seen on the mobile version compared to normal Facebook, meaning I’d actually been seeing peoples’ statuses rather than a random video they ‘liked’ &mdash; a major improvement as far as I’m concerned!)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ff33362-a4c7-40df-bfad-a0173fb713c8/web-with-no-js-39.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ff33362-a4c7-40df-bfad-a0173fb713c8/web-with-no-js-39.png" sizes="100vw" caption="" alt="" >}}

I fully expected the video not to work when I clicked it, but clicking on the thumbnail opened the video in a new tab:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae91371b-2b75-4235-9b2b-c127b900d8be/web-with-no-js-40.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae91371b-2b75-4235-9b2b-c127b900d8be/web-with-no-js-40.png" sizes="100vw" caption="You don’t need JavaScript to play MP4 files." alt="You don’t need JavaScript to play MP4 files" >}}

I’m pleasantly surprised that all of the functionality appears to be there on this `noscript` version of the site. Eventually, however, I found one feature that was just too clunky and cumbersome to see through to the end: album creation.

I wanted to upload a photo album to Facebook, but in `noscript`-land this is a beast of a task. It involves uploading one photo at a time, going through two or three screens for each upload. I desperately tried and failed to find a bulk-upload option.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a525cf3-661c-4b44-afd2-499aae40bab0/web-with-no-js-41.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a525cf3-661c-4b44-afd2-499aae40bab0/web-with-no-js-41.png" sizes="100vw" caption="" alt="" >}}

The laboriousness of this got to me after photo number three (my album will contain many more), so I decided to call it a day and come back tomorrow when I’ve got JavaScript.

## Twitter

Things got weird when I flew over to Twitter.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11585021-5f76-4c46-827e-408038daffd8/web-with-no-js-42.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11585021-5f76-4c46-827e-408038daffd8/web-with-no-js-42.png" sizes="100vw" caption="On first load, I got what looked like the normal desktop site." alt="Twitter on first load" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac787ea-ea99-439c-a36a-1b5987234439/web-with-no-js-43.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac787ea-ea99-439c-a36a-1b5987234439/web-with-no-js-43.png" sizes="100vw" caption="After a couple of seconds, I was automatically redirected to the mobile site." alt="Twitter redirect site" >}}

I was intrigued by this mechanism, so dug into the source code, which was actually surprisingly simple:

<div class="break-out">

<pre><code class="language-javascript">&lt;noscript&gt;&lt;meta http-equiv="refresh" content="0; URL=https://mobile.twitter.com/i/nojs_router?path=%2F"&gt;&lt;/noscript&gt;</code></pre></div>

As beautifully simple as this solution is, I found the experience quite clunky because in the flash before I was redirected, I saw that one of the people I follow on Twitter had got engaged. His tweet didn’t appear at the top of the ‘mobile’ version, so I had to go looking for it.

**Suggestion**: *Build in a grace period into your server-side logic so that redirects and careless refreshes don’t lose interesting tweets before you’ve had a chance to read them.*

I couldn’t remember my friend’s Twitter handle. Searching was a little tricky &mdash; I started to really miss the autofill suggestions!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0488cf8-49f0-4725-bfc3-26685631cad9/web-with-no-js-44.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0488cf8-49f0-4725-bfc3-26685631cad9/web-with-no-js-44.png" sizes="100vw" caption="No autofill suggestions appeared as I typed." alt="A screenshot of me filling in 'andy' as a search term, but no autofill suggestions appearing as I type." >}}

Luckily, the search results page brought his account right up, and I was able to find his tweet. I was even able to reply.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eae7674-8a80-4309-8d42-4ed550d1f66c/web-with-no-js-45.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eae7674-8a80-4309-8d42-4ed550d1f66c/web-with-no-js-45.png" sizes="100vw" caption="" alt="" >}}

**Twitter `noscript` rating: NOSCRIPT-4 🤔**

This may seem like a generous score, given the clunky feel, but remember that the key thing here is feature parity. It doesn’t have to look beautiful.

I tried out a couple more social media sites, which, unlike Twitter, didn’t reach the dizzy heights of NOSCRIPT-4 compliance.

## Other Social Networks

LinkedIn has a nice, bespoke loading screen. But it never loads, so all I could do was stare at the logo.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8a0f89-7c5b-41d2-80bb-a852079f70ee/web-with-no-js-46.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8a0f89-7c5b-41d2-80bb-a852079f70ee/web-with-no-js-46.png" sizes="100vw" caption="" alt="LinkedIn" >}}

**LinkedIn `noscript` rating: NOSCRIPT-0 🔥**

Instagram gave me literally nothing. A blank page. A whole other flavor of NOSCRIPT-0.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b9acace-ce83-447d-8689-11e724a16081/web-with-no-js-47.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b9acace-ce83-447d-8689-11e724a16081/web-with-no-js-47.png" sizes="100vw" caption="" alt="Instagram" >}}

**Instagram `noscript` rating: NOSCRIPT-0 🔥🔥🔥**

I was surprised Instagram failed so spectacularly here, given that the Instagram embed worked flawlessly on my portfolio site. I guess with an embed you never know what the browser support expectations of the third party are, but as I’m visiting the site directly, Instagram is happy making the call to drop support.

## BBC News

I headed over to the BBC to get my fix of news.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8115d515-fdf6-465d-921e-045d50971ceb/web-with-no-js-49.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8115d515-fdf6-465d-921e-045d50971ceb/web-with-no-js-49.png" sizes="100vw" caption="In the <code>noscript</code> version, notice the narrow column and the single story with thumbnail." alt="BBC without JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3073d3-504d-4f6f-bfbc-711bba760ff2/web-with-no-js-48.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3073d3-504d-4f6f-bfbc-711bba760ff2/web-with-no-js-48.png" sizes="100vw" caption="JavaScript version: notice the full use of the desktop screen and multiple article thumbnails." alt="BBC with JavaScript" >}}

The menu is a little bit off, and the column is quite narrow (definitely a pattern I’m seeing on a lot of sites &mdash; why does “no JavaScript” mean “mobile device”?) but I _am_ able to access the content.

I clicked on the ‘Most Read’ tab, which takes me to another part of the page. With scripting, this anchor link is progressively enhanced to achieve actual tab behavior, which is a lovely example of building up from a solid HTML core.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2235a7-10af-40ea-bbd5-609da70f3948/web-with-no-js-50.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2235a7-10af-40ea-bbd5-609da70f3948/web-with-no-js-50.png" sizes="100vw" caption="" alt="Issue" >}}

So far, this is the only example of an anchor link I’ve come across in my experiment, which is a shame as it’s a nice technique that saves an additional page load and saves fragmenting the site into lots of micro pages.

It does look a little odd though, the ordered list CSS meaning we have a double numbering glitch here. I click on one of the stories.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2e8be9-aefd-4c54-9a3e-79cab5fd1bb2/web-with-no-js-51.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2e8be9-aefd-4c54-9a3e-79cab5fd1bb2/web-with-no-js-51.png" sizes="100vw" caption="The article should contain a video, but instead reads “Media playback is unsupported on your device”. There is no transcript." alt="The article should contain a video, but instead reads “Media playback is unsupported on your device”. There is no transcript." >}}

I can’t access the video content, but due to rights issues, I suspect the BBC cannot provide a separate standalone video as Facebook does. A transcript would be nice though &mdash; and beneficial to more than just `noscript` users.

**Suggestion**: *Provide textual fallbacks for audio-visual content.*

To be fair, the article content basically sums up the content that appears in the video, so I’m not really missing out on information.

The article and index pages load lightning-fast, at about 300KB (mostly images). I do miss the thumbnail images for the other articles on the page, and the ability to make full use of my screen real estate &mdash; but that shouldn’t hamper the rating.

**BBC `noscript` rating: NOSCRIPT-5 ✅**

## GitHub

GitHub looks almost _exactly the same_ as its JavaScript-enabled counterpart. Wow! But I guess this is a site developed by developers, for developers. 😉

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/997c2444-c963-4c0d-8c7e-80bdda39311e/web-with-no-js-52.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/997c2444-c963-4c0d-8c7e-80bdda39311e/web-with-no-js-52.png" sizes="100vw" caption="The one difference I can see is the way GitHub deals with time. With JavaScript enabled, notice how it says ‘2 days ago’..." alt="GitHub with JavaScript" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0b39647-9ea9-4295-8bf7-c5086a5ce2ec/web-with-no-js-53.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0b39647-9ea9-4295-8bf7-c5086a5ce2ec/web-with-no-js-53.png" sizes="100vw" caption="On the no script version, it instead says “Mar 1, 2018”." alt="GitHub without JavaScript" >}}

I did a little housekeeping on GitHub, looking around repos and deleting old branches. For a while I genuinely forgot I was on the non-JavaScript version until I came across one little bug:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd0abd19-2247-4263-9984-e02695f908f6/web-with-no-js-54.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd0abd19-2247-4263-9984-e02695f908f6/web-with-no-js-54.png" sizes="100vw" caption="The “Fetching latest commit…” section will spin forever…" alt="The “Fetching latest commit…” section will spin forever…" >}}

Then I wondered, “How is GitHub going to handle applying labels to issues?” so I gave that a go.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30efa40d-7ba0-479a-8bfb-41089c4da969/web-with-no-js-55.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30efa40d-7ba0-479a-8bfb-41089c4da969/web-with-no-js-55.png" sizes="100vw" caption="These fields are unresponsive when you click on them." alt="These fields are unresponsive when you click on them." >}}

I was unable to create an issue and add labels to it at the same time. In fact, I couldn’t find any way of adding the label even after creating a blank issue. It’s a shame the site fell at the last hurdle because it was very nearly a seamless comparison with the scripted version.

**GitHub `noscript` rating: NOSCRIPT-3 🤗**

While GitHub _looks_ incredible &mdash; I would never have known my JavaScript was turned off &mdash; not being able to use the same key functionality as the scripted version is a bummer. Even an ugly looking `noscript` site would get a higher score because functionality is more important than form.

## Online Banking

If there’s one place I expected JavaScript to be required, it was on the NatWest bank website. I was wrong.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec4ea19-645e-44bf-8c70-8cb890271aae/web-with-no-js-56.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec4ea19-645e-44bf-8c70-8cb890271aae/web-with-no-js-56.png" sizes="100vw" caption="" alt="" >}}

Not only does it work, but it’s also hard to distinguish from the normal site. The login screen is the same, the only difference being that the focus doesn’t automatically progress through each field as you complete it.

**NatWest `noscript` rating: NOSCRIPT-5 ✅**

## Miscellaneous

I came across a few more sites throughout my day.

FreeAgent &mdash; the tax software site I use for my freelancing &mdash; doesn’t even try a `noscript` fallback. But hey, that’s better than showing a broken website.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4d94209-0126-45c2-bf20-bae5936373e0/web-with-no-js-58.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4d94209-0126-45c2-bf20-bae5936373e0/web-with-no-js-58.png" sizes="100vw" caption="FreeAgent shows a no-JavaScript message." alt="FreeAgent shows a no-JavaScript message." >}}

**FreeAgent `noscript` rating: NOSCRIPT-2 ⛔**

And CodePen, somewhat understandably, has to be a NOSCRIPT-2 too.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ef9a850-b09b-4cfc-913c-451dda3114fc/web-with-no-js-59.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ef9a850-b09b-4cfc-913c-451dda3114fc/web-with-no-js-59.png" sizes="100vw" caption="" alt="A CodePen shows a no-JavaScript message, and suggests it would be pretty foolish to expect the site to work without JavaScript!" >}}

**CodePen `noscript` rating: NOSCRIPT-2 ⛔**

Tonik, the energy provider, doesn’t let me log in, but this seems like an oversight rather than a deliberate decision:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8b579c-aa22-4f2d-9865-847be95363aa/web-with-no-js-60.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8b579c-aa22-4f2d-9865-847be95363aa/web-with-no-js-60.png" sizes="100vw" caption="I see the words “embedded area” where I’m supposed to see a login form." alt="I see the words “embedded area” where I’m supposed to see a login form." >}}

**Tonik `noscript` rating: NOSCRIPT-1 ❌**

M&S Energy lets me log in &mdash; only to tell me it needs JavaScript to do anything remotely useful.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea792c8f-de66-4f87-ad63-0cf7348ea4ac/web-with-no-js-61.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea792c8f-de66-4f87-ad63-0cf7348ea4ac/web-with-no-js-61.png" sizes="100vw" caption="M&S requires JavaScript to work, but you have to put more effort in to get to that point." alt="M&S requires JavaScript to work, but you have to put more effort in to get to that point." >}}

**M&S `noscript` rating: NOSCRIPT-1 ❌**

Now I come to my favorite screenshot of the day.

One of my colleagues once recommended an [Accessibility for Web Design course](https://www.lynda.com/Web-Design-tutorials/Personas/606090/698850-4.html), which I bookmarked. I decided to take a look at it today, and laughed at the irony of the alt text:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15e08b1-78c8-4fd9-aa72-e9bdec7d89cf/web-with-no-js-62.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15e08b1-78c8-4fd9-aa72-e9bdec7d89cf/web-with-no-js-62.png" sizes="100vw" caption="Alt text of “Personas: Accessibility for Web Design”. Soooo… what am I missing?" alt="Alt text of “Personas: Accessibility for Web Design”. Soooo… what am I missing?" >}}

With the alt text of “Personas: Accessibility for Web Design,” I’m not too sure what I’m missing here &mdash; is it an image? A video? A PDF? The course itself?

**Hint**: *It’s actually a video, though you have to be logged in to watch it.*

The alt text isn’t really supporting its purpose, partly because it’s populated automatically. We as a dev community need to get better at this sort of thing. I don’t think I’ve read any useful alt text today.

## Summary

I started this experiment with the aim of seeing how many sites are implemented using progressive enhancement. I’ve only visited a tiny handful of sites here, most of them big names with big budgets, so it’s interesting to see the wide variation in no-JavaScript support.

It’s interesting to see that relatively simple sites &mdash; Instagram and LinkedIn particularly &mdash; have such poor `noscript` support. I believe this is partly down to the ever-growing popularity of JavaScript frameworks such as React, Angular, and Vue. Developers are now building “web applications” rather than “websites,” with the aim of recreating the look and feel of native apps, and using JavaScript to manage the DOM is the most manageable way of creating such experiences.

There is a danger that more and more sites will require JavaScript to render any content at all. Luckily, it is usually possible to build your content in the same, developer-friendly way but rendered on the server, for example by using Preact instead of React. Making the conscious decision to care about `noscript` gives the benefits of a core experience as outlined at the beginning of this article, and can make for a faster perceived loading time, too.

It can be quite daunting to think about an application from the ground up, but a decent core experience is usually possible and actually only involves simple tweaks in a lot of cases. A good core experience is indicative of a well-structured web page, which, in turn, is usually a good sign for SEO and for accessibility. It’s usually a well _designed_ web page, as the designer and developer have spent time and effort thinking about what’s truly core to the experience. Progressive enhancement means more robust experiences, with fewer bugs in production and fewer individual browser quirks, because we’re letting the platform do the job rather than trying to write it all from scratch.

What `noscript` rating does your site conform to? Let us know in the comments!

{{< signature "rb, ra, il" >}}

