---
title: Progressive Enhancement Is Faster
slug: progressive-enhancement-is-faster
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00b0216f-c030-4f44-b471-34fcaf56e5dd/illu-enhancement.jpg
date: 2013-09-03T12:48:54.000Z
author: jake-archibald
description: >-
  Progressive enhancement has become a bit of a hot topic recently, most
  recently with Tom Dale [conclusively showing it to be a futile
  act, but only by misrepresenting what progressive enhancement is and what its benefits are.
categories:
  - Coding
  - Opinion Column
---
_The aim of republishing the [original article by Jake](https://jakearchibald.com/2013/progressive-enhancement-is-faster/) is to raise awareness and support the discussion about the role of progressive enhancement within the community. We look forward to your opinions and thoughts in the comments section. – Ed._

Progressive enhancement has become a bit of a hot topic recently, most recently with Tom Dale [conclusively showing it to be a futile act](https://tomdale.net/2013/09/progressive-enhancement-is-dead/), but only by misrepresenting what progressive enhancement is and what its benefits are.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Progressive Enhancement: What It Is, And How To Use It?](https://www.smashingmagazine.com/2009/04/progressive-enhancement-what-it-is-and-how-to-use-it/)
*   [Progressive Enhancement Is Faster](https://www.smashingmagazine.com/2013/09/progressive-enhancement-is-faster/)
*   [Reimagining Single-Page Applications With Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)

**You shouldn't cater to those who have deliberately disabled JavaScript**, unless of course you have a particular use case there, e.g. you're likely to get significant numbers of users with the Tor Browser, which comes with JS disabled by default for security. If you do have that use case, progressive enhancement helps, but that's not its main benefit.

{{% feature-panel %}}

You should use progressive enhancement for [the reasons I covered a few weeks back](https://jakearchibald.com/2013/progressive-enhancement-still-important/). However, my article was called out on Twitter (the home of reasonable debate) as just "words on a page" and incompatible with "real-life production".

Of course, the article is an opinion piece on best practice, but it's based on real examples and actual browser behaviour. However, I wanted to find more tangible "real-world" evidence. Turns out I was staring at it.</p>

## I Love Tweetdeck

I don't have Chrome open without a [Tweetdeck](https://tweetdeck.com) tab. I use it many times a day, it's my Twitter client of choice. It does, however, depend on JavaScript to render more than a loading screen.

Twitter used to be the same, but they started [delivering initial content as HTML](https://blog.twitter.com/2012/improving-performance-twittercom) and enhancing from there to improve performance. So, they deliver similar data and cater for similar use cases, this makes them perfect for a real-world comparison.</p>

## The Test

To begin, I:

*   Set up a Tweetdeck account with six columns,
*   Closed all other apps (to avoid them fighting for bandwidth),
*   Connected to an extremely fast wired network,
*   Used the [Network Link Conditioner](https://mattgemmell.com/2011/07/25/network-link-conditioner-in-lion/) to simulate a stable 2 Mbit ADSL connection and
*   Cleared the browser cache.

I recorded Tweetdeck loading in a new tab, then cleared the browser cache again and recorded six Chrome windows loading the equivalent content on Twitter ([here's the launcher](https://jsbin.com/agExako/1/edit) if you're interested).

Now, 2 Mbit may sound slow, but I've stayed at many hotels where I'd have done dirty, dirty things for anything close to 2 Mbit. The maximum broadband in the area I live is 4 Mbit unless you can get fibre. On mobile, you'll be on much lower speeds depending on signal type and strength.</p>

## The Results

Here are the two tests playing simultaneously (note: they were executed separately):

<table id="price_list">

<tbody>

<tr>

<td>02.080s</td>

<td>Tweetdeck renders loading screen. So Tweetdeck gets past the blank screen first.</td>

</tr>

<tr>

<td>02.150s</td>

<td>Twitter renders three "columns" of tweets, that's only 70ms later than Tweetdeck shows it's loading screen.</td>

</tr>

<tr>

<td>02.210s</td>

<td>Twitter renders six columns of tweets. Twitter has delivered the core content of the page.</td>

</tr>

<tr>

<td>04.070s</td>

<td>Tweetdeck renders six empty columns. Twitter is downloading background images.</td>

</tr>

<tr>

<td>05.180s</td>

<td>Tweetdeck renders its first column of tweets.</td>

</tr>

<tr>

<td>06.070s</td>

<td>Tweetdeck delivers another column.</td>

</tr>

<tr>

<td>06.270s</td>

<td>...and another.</td>

</tr>

<tr>

<td>08.030s</td>

<td>...and another.</td>

</tr>

<tr>

<td>08.230s</td>

<td>...and another.</td>

</tr>

<tr>

<td>10.120s</td>

<td>...and another, and that's all the core content delivered by Tweetdeck. Tweetdeck is fully loaded at this point, whereas Twitter continues to load secondary content (trends, who to follow etc).</td>

</tr>

<tr>

<td>10.120s</td>

<td>Twitter finishes loading secondary content.</td>

</tr>

</tbody>

</table>

So Twitter gets the core content on the screen 7.91 seconds earlier than Tweetdeck, despite six windows fighting for resources. For the first bit of core content, Twitter gets it on screen 3.03 seconds sooner.

Twitter takes 4.09 seconds longer to finish loading completely, but this includes a lot of secondary content and heavy background imagery that Tweetdeck doesn't initially show. On Twitter, the core content is prioritised.

That's with an empty cache, but what about a full one? Here's the same test, but ran a second time without emptying the browser cache:

<p><table id="price_list">
<tr>
<td>00.060s</td>
<td>Tweetdeck renders loading screen. So Tweetdeck gets past the blank screen first, again, but much sooner.</td>
</tr>
<tr>
<td>00.090s</td>
<td>Twitter renders the first "column" of tweets.</td>
</tr>
<tr>
<td>01.010s</td>
<td>Twitter renders second "column".</td>
</tr>
</tr>
<tr>
<td>01.110s</td>
<td>Twitter renders third "column".</td>
</tr>
<tr>
<td>01.190s</td>
<td>Twitter renders fourth "column".</td>
</tr>
<tr>
<td>01.200s</td>
<td>Tweetdeck renders six empty columns.</td>
</tr>
<tr>
<td>01.230s</td>
<td>Twitter renders fifth "column".</td>
</tr>
<tr>
<td>01.240s</td>
<td>Twitter renders sixth "column". Twitter has now delivered all core content.</td>
</tr>
<tr>
<td>02.100s</td>
<td>Tweetdeck renders first column.</td>
</tr>
<tr>
<td>02.160s</td>
<td>Tweetdeck renders second column.</td>
</tr>
<tr>
<td>02.260s</td>
<td>Tweetdeck renders third column.</td>
</tr>
<tr>
<td>03.030s</td>
<td>Tweetdeck renders fourth column.</td>
</tr>
<tr>
<td>04.010s</td>
<td>Tweetdeck renders fourth and fifth columns. Tweetdeck has now delivered all core content.</td>
</tr>
<tr>
<td>04.050s</td>
<td>Twitter finishes downloading secondary content.</td>
</tr>
</table>

So, with a full cache, Twitter beats Tweetdeck to all core content by 2.77 seconds, and first core content by 2.01 seconds.

Which test represents the "real-life" case? Well, something in between the two. As you browse the Web you'll knock resources out of your cache, but also the site will cause cache misses through rapid deployments which change the URLs of resources. Current best practice is to combine and; minify your CSS/JS files and give them a unique URL, so whenever you need to make a change, no matter how small, the URL changes and the client has to download the new resource. Roll on HTTP2, I say.

## Is This Test Fair?

Well, no. It's real life, and as such it has the uncertainty of real life. But those are two expertly-built sites that offer similar content.

**The test is unfair to Tweetdeck because:**

*   A lot of the XHR requests they make could be rolled into one, improving performance despite JS reliance (assuming this wouldn't have large overhead on the server)

**The test is unfair to Twitter because:**

*   Six separate requests are made for markup, whereas a true progressive competitor would use one. This incurs the HTTP overhead and repetition of common markup.
*   It undergoes 6x the style calculations and layouts compared to Tweetdeck (because Twitter is running in six separate windows).
*   I zoomed out all the Twitter windows so more content was visible, so the six windows have the paint overhead of scaling.

Of course, Tweetdeck gets away with it because it's a tab I always have open, so I don't go through the startup cost often. This is extremely rare for a website, even for those that claim to be "apps".

You shouldn't bet your performance on being a perma-tab. Twitter did this, but it turned out people shared and followed links to individual tweets and timelines, and the startup cost made them feel incredibly slow. They [fixed this with progressive enhancement](https://blog.twitter.com/2012/improving-performance-twittercom).</p>

## The Results Aren't Surprising

Here's what a progressively enhancing site needs to download to show content:

*   _some_ HTML
*   CSS

…and those two download pretty much in parallel. The HTML will get a head start, because the browser needs to read the HTML to discover the CSS.

The whole of the CSS will block rendering to avoid [FOUC](https://en.wikipedia.org/wiki/Flash_of_unstyled_content), although if you want to put your foot to the floor you can inline the CSS for top-of-page content, then include your `link[rel=stylesheet]` just before the content that isn't covered by the inlined CSS.

Rendering isn't blocked by _all_ your HTML, the browser can update the rendering as it receives more markup. This works with gzipped HTML too. Check out the full WHATWG spec (warning: it's 2.6mb), although the markup is huge, it gets to first-render really quickly.

Ideally you'd have your script in the head of the page loading async, so it gets picked up by the parser early and enhances the page as soon as possible.

If a site does its content-building on the client based on API calls, such as Tweetdeck, here's what it needs to download:

*   All HTML (although small)
*   CSS
*   JavaScript
*   JSON (API call)

The HTML, CSS and JavaScript will download pretty much in parallel, but the JSON download cannot start until the JavaScript has downloaded, because the JavaScript triggers the request.

The JavaScript on one of these pages can be significant, for instance Tweetdeck's scripts total 263k gzipped. [As Adam Sontag points out](https://twitter.com/miketaylr/statuses/227056824275333120) (using Mike Taylor as his medium), that's the size of a few images we'd use on a page without thinking twice. But we _would_ think twice if those images blocked core content from downloading and displaying, which is the case with the JavaScript on these sites. Hey, images even progressively render as they download, JavaScript can't do anything until the whole file is there.

Getting something on screen as soon as possible really improves the user experience. So much so that Apple recommends giving iOS apps a static bitmap ["Launch Image"](https://developer.apple.com/library/ios/documentation/userexperience/conceptual/mobilehig/IconsImages/IconsImages.html#//apple_ref/doc/uid/TP40006556-CH14-SW5) that looks like the first screen of your app. It's a basic form of progressive enhancement. Of course, we can't do that on the Web, we can do better, we can show actually core content as soon as possible.

I'm open to examples to the contrary, but I don't think a JS-rendered page can beat a progressively enhanced page to rendering core content, unless the latter is particularly broken or the content can be automatically generated on the client (and generating it is faster than downloading it).

I'm keen on the progressive enhancement debate continuing, but can we ditch the misrepresentation and focus on evidence?

{{< signature "il" >}}
#price_list { margin: 1em 0 2.5em 0; border-collapse: collapse;width:
100%;border: 1px solid rgba(0,0,0,0.1);border-radius: 8px !important;margin-top:
30px;}#price_list .desc { font-size: 12px; color: #555;}#price_list a { font-family:
"Proxima Nova Bold", Arial, serif; }#price_list td {padding: 8px 15px;border: 1px
solid rgba(0,0,0,0.05);}#price_list tr:nth-child(2n+1) { background-color:
rgba(0,0,0,0.03); }#price_list thead td { color: #fff; font-size: 13px; text-transform:
uppercase; background-color: #888;}#price_list td.new_price { color:
#cc0000; font-weight: bold; width: 55px;}#price_list td.old_price { width: 55px;
color: rgba(0,0,0,0.45); font-weight: bold;}

