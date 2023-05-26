---
title: Review of Popular Web Font Embedding Services
slug: review-of-popular-web-font-embedding-services
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4cbe12b-e7df-45ef-a536-2c69f67bd989/fontdeck.jpg
date: 2010-10-20T12:55:52.000Z
author: andrew-follett
description: >-
  Even though `@font-face` was introduced in the CSS2 spec in 1998, it wasn't until this past year that all in-use web browsers added support for it. This year we're seeing a wave of web font services being marketed, and this could have a profound impact on web typography.
categories:
  - Typography
  - Fonts
---
In the mid-80s the desktop publishing revolution began with the introduction of the Mac Plus, Aldus PageMaker and the Apple LaserWriter printer. It took quite a few years for these tools to make an impact on the design and publishing world, but once they did, there was no looking back.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Dear Web Font Providers](https://www.smashingmagazine.com/2013/09/dear-web-font-providers/)
*   [<span class="headline">Setting Weights And Styles With The @font-face Declaration</span>](https://www.smashingmagazine.com/2013/02/setting-weights-and-styles-at-font-face-declaration/)
*   [The @Font-Face Rule And Useful Web Font Tricks](https://www.smashingmagazine.com/2011/03/the-font-face-rule-revisited-and-useful-tricks/)
*   [Balancing Line Length And Font Size In Responsive Web Design](https://www.smashingmagazine.com/2014/09/balancing-line-length-font-size-responsive-web-design/)

Web font services, like Typekit and now the Google Font API, have captured a lot of attention. But in the past 3 months there's been an explosion of new services; services like Fonts Live, Fontdeck, Webtype and others with conjugated names involving "Font" or "Type".

{{% feature-panel %}}

While all of these services are unique, they each provide a tool for web designers and developers to legally display professional fonts on their website. <strong>The guide below compares 10 of these services</strong>, breaking down the pros and cons of each. We hope this comparison will help you make a more informed decision on which service to use when you venture into the ever-growing, sometimes confusing, world of web fonts.</p>

## Typekit

<a href="https://www.typekit.com/">Typekit, Inc.</a> is a popular web font service from Small Batch Inc and founder Jeffrey Veen. Typekit was one of the first services on the scene and is currently one of the most widely adopted services on the market.

<a href="https://www.typekit.com"><img loading="lazy" decoding="async" class="63068" title="typekit" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/506f97a0-fe00-487e-b3d2-bc3ab1029f1a/fonts-11.jpg" alt="Typekit" width="500" height="305" /></a>

<strong>Font Selection</strong>
4000 (about half of these are through the Typekit library, and the other half via licensing arrangements with foundries who sell their own web licences)

<strong>Advantages Over Other Services</strong>
Strong platform integrations. Typekit is a scaled service, with well over 80 million unique users each month.

<strong>Pros</strong>
Extremely easy setup for designers and developers, allowing integration within minutes. Integration with Google Font API and blogging platforms including WordPress, Posterous and Typepad. The full font library is available via most plans for a single low price, allowing customers to try different fonts on one site as well as use different fonts on multiple projects. Now offering <a href="https://typekit.com/foundries/adobe">Adobe fonts</a>. Enterprise customers can self-host using their own CDN. The service allows you to host custom fonts. The simple free plan doesn't expire.

<strong>Cons</strong>
Implementation requires JavaScript (although on the Typekit blog they list <a href="https://blog.typekit.com/2009/06/02/fonts-javascript-and-how-designers-design/">some reasons that JavaScript-based implementation has its advantages</a>). Fonts are not available for desktop use.

<strong>Pricing</strong>
Free trial account includes the use of 2 fonts on 1 website. Paid plans start at $24.99 per year (2 sites, 5 fonts per site). The more popular plans allow unlimited font usage on unlimited domains.

<strong>Fee Schedule</strong>
Annual subscription

### Our Experience with Typekit

Setting up TypeKit is fairly straightforward. You just set the domains you want to use (the free trial site includes one domain and up to two fonts) and then build your Kit by adding fonts. A little JavaScript inserted into the header pulls in all the necessary CSS information. You can also reference the fonts in your own CSS, and use wild cards when adding to your list of allowed domains (e.g. *.domain.com will work on sub.domain.com).

As is the case with any web font service, there is a brief delay before the proper font is shown, but it's barely noticeable. Since Typekit's fonts are loaded via JavaScript, Typekit offers tools <a href="https://typekit.zendesk.com/entries/245989-controlling-the-flash-of-unstyled-text-or-fout">to control the loading process</a>, so delays are not as noticeable to the user.</p>

## Webtype

<a href="https://www.webtype.com/">Webtype</a> is a recent creation of <a href="https://www.fontbureau.com/">The Font Bureau</a>, <a href="https://www.ascendercorp.com">Ascender</a>, <a href="https://www.devbridge.com/">DevBridge</a>, and font experts Roger Black and Petr Van Blokland. Webtype is all about quality and boasts “fonts for the highest quality online typography, including typefaces which were designed from scratch specifically for onscreen reading”.

<a href="https://www.webtype.com"><img loading="lazy" decoding="async" class="63070" title="webtype" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b51f22c-aa0b-4e9f-a2f3-a98ecc090a84/fonts-12.jpg" alt="Webtype" width="500" height="357" /></a>

<strong>Font Selection</strong>
365

<strong>Advantage Over Other Services</strong>
Font quality

<strong>Pros</strong>
Quick and easy setup. Flexible pricing. Ability to host custom fonts as well as self-host. JavaScript-free integration. Desktop license available.

<strong>Cons</strong>
Some fonts are expensive compared to other web font services.

<strong>Pricing</strong>
Free 30-day trial on all fonts. Fonts start at $10 per year per site.

<strong>Fee Schedule</strong>
Annual subscription

### Our Experience with Webtype

Webtype was easy to set up and use from the signup process on. Just browse and purchase fonts (a 30-day free trial license is available for testing fonts) and then create projects. Select the font you want to use for each project and you’ll be given a link code and CSS selector for each font. Then you copy and paste them into your HTML and CSS files and you’re ready to go.

Make sure you click “Save” from the CSS resource page that gives you the code, or it won’t be live. Resource size is also given on this page, which can be helpful if you’re trying to estimate bandwidth usage. The load time for the font was possibly a bit slower than some of the other services here, despite the small file size of the font tested.

## Fontdeck

Fontdeck is a relatively new service by <a href="https://clearleft.com/">Clearleft</a> and <a href="https://omniti.com/">OmniTI</a>. It was conceived in March 2009 by Jon Tan and Richard Rutter as a way to bring quality fonts to a wide audience while levelling the playing field for type foundries. It went into private beta in January 2010 and was open to the public in June of 2010.

<a href="https://www.fontdeck.com"><img loading="lazy" decoding="async" class="63071" title="fontdeck" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff95cffc-880c-4440-bb57-239c5da8da85/fonts-13.jpg" alt="FontDeck" width="500" height="337" /></a>

<strong>Font Selection</strong>
600, with plans for this number to be doubled before Christmas.

<strong>Advantage Over Other Services</strong>
Only pay for the fonts you want to use. No bandwidth limit. Unlimited trial periods for all fonts (with a 20 IP address cap).

<strong>Pros</strong>
Easy to set up. Affordable options available. Automatically include similar style fonts in the font stack. Pure CSS with no JavaScript required.

<strong>Cons</strong>
No self-hosting option available. Fonts not available for desktop use.

<strong>Pricing</strong>
Some free fonts, but most start at $2.50 per year per site.

<strong>Fee Schedule</strong>
Annual subscription (which applies only to fonts on live web sites; as mentioned, all fonts have unlimited trial periods).</p>

### Our Experience with Fontdeck

Fontdeck was incredibly easy to set up. While it does require manual insertion of the CSS selectors into the stylesheet for your site (which is by design, to give designers as much control as possible), it provides the code for this immediately without the added step of setting up a stylesheet (the link is ready as soon as you select to add the font). Prior to purchasing the license, the first 20 visitors to your site can see the font.

I did find that I had to add the subdirectory to the hostname in order to get it working. But all the options and controls are located on a single page for each font, making it easy to update settings. Fonts are displayed quickly, but as with the other services, there is a split of a second when you can see the default font.

One added bonus from Fontdeck is that they include similar style fonts in the font stack, in case the user's browser doesn't support <code>@font-face</code>, and to help with the perceived change in text. Many of the other services just use the default font or a generic serif/sans-serif.</p>

## Fonts Live

Fonts Live is a new web font service from <a href="https://www.ascendercorp.com">Ascender Corporation</a> — the company behind the “Droid” fonts for Google’s Android mobile platform, the “Segoe” family of fonts for Microsoft Windows, and the Ascender Fonts desktop font web store. Fonts Live is similar to Webtype (both were developed by <a href="https://www.devbridge.com/">DevBridge</a>), however, Fonts Live serves fonts exclusively from Ascender and its partners.

<img loading="lazy" decoding="async" class="63072" title="Fonts Live" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/553c7b43-66aa-4d45-ae2c-797546aa01a7/fonts-14.jpg" alt="Fonts Live" width="500" height="388" />

<strong>Font Selection</strong>
499

<strong>Advantage Over Other Services</strong>
Font quality

<strong>Pros</strong>
Flexible pricing. Desktop license available. Option to self-host web fonts. Integration with Google Font API. JavaScript-free integration. Now offering Hallmark fonts.

<strong>Cons</strong>
Some fonts are expensive compared to other web font services. Back-end was among the least user-friendly of the services featured here.

<strong>Pricing</strong>
Free 30-day trial on all fonts. Fonts start at $10 per year per site.

<strong>Fee Schedule</strong>
Annual subscription

### Our Experience with Fonts Live

Setting up Fonts Live is a bit more labor intensive than setting up some others featured here. Setting up the service wasn't without its bugs, either. First of all, read the documentation before you start, or you're likely to get confused. With the first font I tried (Corsiva Italic), the site was unable to set up the resource and kept returning errors. It also created blank files for each of these failures, meaning I had to go in and manually delete them. Not sure if this was just an exception for that particular font or if it's a more widespread problem. There was no mention of it in the site’s documentation.

I had better luck with the second font I tried (Romany). This time it created the resource without any issues. From there, you have to insert the stylesheet (“resource” in Fonts Live terms) link in your header and then insert the font family, style, and weight for whichever elements you want styled. The plus side here is that you don't run into issues with your original stylesheet interfering.

Once it was up and running, however, it was noticeably faster serving the fonts than TypeKit, though this is likely due to smaller file sizes in the fonts used.</p>

## TypeFront

TypeFront is a hosting-only service which lets you upload a font you already own, as long as it has a web-friendly license (make sure you read the license agreement carefully!). Once you add the domain(s) you want to use, TypeFront provides you with the code to add to your website.

<img loading="lazy" decoding="async" class="63074" title="typefront" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acf3083f-c9ce-4aae-aa21-98525a395c3e/fonts-15.jpg" alt="TypeFront" width="500" height="332" />

<strong>Font Selection: </strong>N/A

<strong>Advantage Over Other Services</strong>
Ideal for do-it-yourself designers and developers who understand the ins and outs of web typography.

<strong>Pros</strong>
Inexpensive. No noticeable delay when displaying web fonts.

<strong>Cons</strong>
You must supply your own fonts. Requires a solid understanding of your font license agreement.

<strong>Pricing</strong>
Free plan offers 1 font and 500 requests per day. Paid plans start at $5 per month (Australian dollars) and include 10 hosted fonts and 5000 requests per day. 30-day trial on all paid plans.

<strong>Fee Schedule</strong>
Monthly subscription

### Our Experience with TypeFront

Once you've signed up for an account, uploading fonts is simple. Just make sure the fonts you're using have a web-friendly license. From this point you have to enable the format you'd like to use for the font (included are EOT, OpenType, SVG, TrueType, and WOFF — at least for the font I used). Once one of those formats is enabled, you have to add domains.

After you've enabled your formats and set up the domains you want to use, you have to copy the <code>@font-face</code> code into your CSS files and add the font to your font stacks. The big advantage TypeFront has over the other services listed here is that there is no noticeable delay before the correct font is displayed.</p>

## Fontspring

<a href="https://www.fontspring.com/">Fontspring</a> offers downloadable fonts for self-hosting. Unlike a hosted service, Fontspring provides downloadable font files and sample code to host web fonts on your own.

<a href="https://www.fontspring.com"><img loading="lazy" decoding="async" class="63075" title="fontspring" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d72db4b-5eda-4e29-8cf4-7d85d585444c/fonts-16.jpg" alt="Fontspring" width="500" height="334" /></a>

<strong>Font Selection</strong>
1,937 families

<strong>Advantage Over Other Services</strong>
No recurring subscription fee

<strong>Pros</strong>
Large font selection. No recurring fees or bandwidth restrictions. Desktop license included.

<strong>Cons</strong>
Font quality varies. Self-hosting only, which requires additional setup and technical skills.

<strong>Pricing</strong>
Free or up to several hundred dollars depending on the font family

<strong>Fee Schedule</strong>
One-time fee

### Our Experience with Fontspring

Because these are self-hosted files, it's a bit harder to get everything set up properly than it is with the other services here. When you purchase and download a font that includes an <code>@font-face</code> license, the download package includes all the files you'll need for web implementation, including the various font file formats like EOT and WOFF.

I found it easier to just copy and paste the stylesheet information included into the existing site's stylesheet. Once that's done, you need to make sure your fonts are loaded into the same folder as your stylesheet (or change the URL information in the CSS). Add the font to your font stack and you're ready to go.

The speed at which the fonts loaded was roughly the same as for most of the other services here. The advantage to using this service is that you own a permanent license to the fonts, without any recurring annual fees and with no restrictions on bandwidth or traffic.</p>

## Fonts.com Web Fonts

Web fonts from <a href="https://webfonts.fonts.com/">Fonts.com</a> is a new venture from <a href="https://www.monotypeimaging.com/">Monotype Imaging</a>, the largest font distributor on the web. Fonts.com currently has, by far, the largest web font selection with more than 7,500 fonts.

<a href="https://www.webfonts.fonts.com"><img loading="lazy" decoding="async" class="63076" title="fonts-com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3183f6-9b8b-4c8e-8b5a-fc1f3220e38a/fonts-17.jpg" alt="Fonts.com" width="500" height="344" /></a>

<strong>Font Selection</strong>
7,500+

<strong>Advantage Over Other Services</strong>
Large Font selection

<strong>Pros</strong>
Currently the largest selection of fonts on the web. Exclusive home to popular fonts like Helvetica, Frutiger and Univers. Support for more than 40 languages. Use on unlimited domains. Download up to 50 desktop fonts per month with the Professional plan. JavaScript-free integration available to Standard and Professional subscribers.

<strong>Cons</strong>
Relatively expensive on a price-per-font basis when using a limited number of web fonts. The font selection interface is slower than average.

<strong>Pricing</strong>
Various tiers ranging from free up to $500/month. With a free tier, you have the ability to use any of 2000 fonts on an unlimited number of websites (up to 25,000 page views). Standard and Pro tiers will give you access to any of over 7,000 fonts. All pricing is dependent upon page views.

<strong>Fee Schedule</strong>
30 days

### Our Experience with Fonts.com Web Fonts

The service looks pretty straightforward. You set up a project with as many domains as you want and then select the fonts you want to use for that project. Selecting fonts is a bit slow (it takes 30 seconds or more for a font to actually be added to a project), but not enough to be prohibitive. There’s a huge selection of fonts and powerful tools for sorting through them, in addition to search capability.

From there, you have to enter each CSS selector for which you would like to use a web font and select the font used for that particular selector using a drop down menu that lists the fonts you already selected for the project. One place where Fonts.com really stands out is in the options you have for publishing your new web fonts. There are two different JavaScript options — an “Easy” option and an “Advanced” one — that let you add the fonts to selectors directly in your stylesheet rather than just through the web interface, as well as two non-JS options (also “Easy” and “Advanced”).

Again, the Fonts.com site was a bit slow overall but the end result is just as fast and seamless as any other service listed here.</p>

## Google Fonts

<strong>Google Fonts</strong>, announced last May, represents Google’s foray into web fonts. Google offers the service free of charge. Although the selection is currently limited to certain public domain fonts, it has the potential to have a significant impact on the future of web fonts.

<img loading="lazy" decoding="async" class="63077" title="google" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/379167d5-b92f-4ece-852c-012a0f00d8d2/fonts-18.jpg" alt="Google Fonts" width="500" height="337" />

<strong>Font Selection</strong>
60 (including international fonts)

<strong>Advantage Over Other Services</strong>
Free

<strong>Pros</strong>
Easy to implement. Fast font loading. Google’s WebFont Loader lets you use their service with multiple web font providers.

<strong>Cons</strong>
Small font selection in the Google font directory. <del>No support for iPhone or iPad (Mobile Safari).</del> Now with support for iPhone and iPad (Mobile Safari).

<strong>Pricing</strong>
Free

<strong>Fee Schedule</strong>
N/A

### Our Experience with Google Fonts

The Google Fonts API is probably the easiest of the services listed here to get started with, mostly because there is no sign-up process. You simply browse the fonts they offer, select one, and then get the code. Link the stylesheet in your website's head, and then add the font to the font stack in your stylesheet.

The service is very fast, with only a barely noticeable lag before loading the proper font. The fact that there are no limits on usage of the service puts it among the top contenders on this list. The only major drawback is the limited number of fonts available.</p>

## Kernest

<strong><a href="https://www.kernest.com/">Kernest</a></strong> is a hosted or self-hosted (you can also use Fontue, Kernest’s open source web font serving engine) web font tool that converts fonts into web font ready formats and sample code.

<a href="https://www.kernest.com"><img loading="lazy" decoding="async" class="63078" title="kernest" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a490026-f9ea-486f-b3a0-1be1127c401c/fonts-19.jpg" alt="Kernest" width="500" height="310" /></a>

<strong>Font Selection</strong>
2,450

<strong>Advantage Over Other Services</strong>
Most fonts are free

<strong>Pros</strong>
Open source web font serving engine. Large font selection.

<strong>Cons</strong>
Self-hosting only, which requires additional setup and technical skills

<strong>Pricing</strong>
Free or up to $15

<strong>Fee Schedule</strong>
One-time fee

### Our Experience with Kernest

Kernest has a great selection of free and paid fonts available. Free fonts could be set up without having to sign up for an account. Just find the font you want to use, make sure the permissions are acceptable for your intended use (not every font is allowed to be used on commercial sites, for example), and then copy and paste the link and CSS code into your files.

Kernest works as well as any of the others on this site, with minimal lag time before the fonts load.</p>

## Typotheque

<a href="https://www.typotheque.com/webfonts">Typotheque</a> is a graphic design studio and type foundry located in the Netherlands. Their hosted web font service includes a relatively small selection of Typotheque fonts. Typotheque was the first foundry to start its own web font service, and all fonts are designed in-house.

<a href="https://www.typotheque.com/webfonts"><img loading="lazy" decoding="async" class="63079" title="typotheque" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039aed24-f509-4f9b-bd3b-aa7d3338a0b9/fonts-20.jpg" alt="Typotheque" width="500" height="318" /></a>

<strong>Font Selection</strong>
37 font families, many supporting various styles and languages; this means there are over 500 single fonts.

<strong>Advantage Over Other Services</strong>
Use on unlimited websites

<strong>Pros</strong>
Option to purchase a full (web and desktop) license. Over 250 languages supported, and from those up to 5 languages can be embedded. All fonts are exclusive to and designed by Typotheque. Offers self-hosting for large websites.

<strong>Cons</strong>
Limited font selection (although this is only true because their fonts are exclusive) and monthly bandwidth (500MB for each font within a font family).

<strong>Pricing</strong>
20% of the full desktop license (ex. Fedra Sans Std Book: Full @ €90, Web @ €18).  Includes 500MB monthly bandwidth.

<strong>Fee Schedule</strong>
One-time fee (€5 for every extra GB over 500MB)

### Our Experience with Typotheque

Setup is similar to the other services listed here. Just select the font you want to use and the domains on which it will be used, add the stylesheet link to the head of your page, add the font to your font stacks, and you're ready to go. Lag time for the font to load is comparable to the other services. The biggest drawback is the lack of font selection, but as mentioned, this is due to the fact that their fonts are exclusive to Typotheque.

The service did return an error when generating the font subset, but it appeared to work fine, so not sure if that's a bug or if there would actually be problems with more extensive testing.</p>

## WebINK

<a href="https://www.extensis.com/en/WebINK/">WebINK</a> is a hosted web font platform developed by <a href="https://www.extensis.com/">Extensis</a>, a software development company based out of Portland, Oregon and specializing in font management.

<a href="https://www.extensis.com/en/WebINK/index.jsp"><img loading="lazy" decoding="async" class="63080" title="webink" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3f5e3f1-ae60-4752-8bcb-2f8dcc424659/fonts-21.jpg" alt="WebINK" width="500" height="357" /></a>

<strong>Font Selection:</strong>
2,000

<strong>Advantage Over Other Services</strong>
Can be affordable for the right type of user

<strong>Pros</strong>
Affordable pricing structure (similar to Typekit). Decent selection of fonts. Offers access both through the usual web interface, or alternatively through a desktop font management application called <a href="https://www.extensis.com/en/products/suitcasefusion3/overview.jsp">Suitcase Fusion 3</a> (Mac and Windows). This application has a live website preview mode for testing different fonts, and something called QuickMatch that finds the closest match to the chosen font on your computer.

<strong>Cons</strong>
Confusing interface and back-end. Each plan is limited to 4 websites (Note: Each user can set up as many "Type Drawers" as they want, allowing 4 websites per Type Drawer; so really the number of websites is only limited to an individual plan within a single user account, whereas the number of Type Drawers is unlimited).

<strong>Pricing</strong>
Free 30-day trial on all fonts. Packages start at $0.99 per month (only includes “Promotional” font selection) for 1GB usage and up to 4 websites.

<strong>Fee Schedule</strong>
Monthly subscription

### Our Experience with WebINK

We only tested the web interface for WebINK, not Suitcase Fusion 3. The WebINK online interface is probably more confusing than the others listed here. The service allows you to create an unlimited amount of Type Drawers to hold the fonts for your different projects. To add fonts from the library into your Type Drawers, you need to click the "add fonts" button within a specific Drawer. Going directly to the font library will not allow you to have direct access to your Drawers, so this takes some getting used to.

Once you get the fonts you want into your Type Drawer, setting them up on your website requires adding the <code>@font-face</code> information to your stylesheet and placing the fonts into your font stacks. The speed at which the font loads on the site is about the same as any other service.</p>

## Font-Face

<a href="https://www.font-face.com/">Font-Face</a> recently scrapped its project after the recent Google Font announcement. However, according to their website, they are "hatching a new plan" so we may hear more from them yet.

<a href="https://www.font-face.com"><img loading="lazy" decoding="async" class="63081" title="font-face" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bcc11c1-be00-43ed-94ef-cc76199cbfe9/fonts-22.jpg" alt="Font-Face" width="500" height="335" /></a>

## How to Choose a Service

There is no “right” answer when it comes to choosing a web font service. Selecting the proper service usually depends on what you or your client need. You could ask yourself the following questions to help assess your needs:

*   How important is font selection? Are there specific fonts you need?
*   How important is font quality to you and your clients?
*   Do you require a self-hosting option?
*   Do you or your client have a budget? What type of fee structure would be ideal?
*   Is iPhone and iPad (Mobile Safari) support important?

Web fonts from <a href="https://webfonts.fonts.com/">Fonts.com</a> is a new venture from <a href="https://www.monotypeimaging.com/">Monotype Imaging</a>, the largest font distributor on the web. Fonts.com currently has, by far, the largest web font selection with more than 7,500 fonts.

<a href="https://www.webfonts.fonts.com"><img loading="lazy" decoding="async" class="63076" title="fonts-com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3183f6-9b8b-4c8e-8b5a-fc1f3220e38a/fonts-17.jpg" alt="Fonts.com" width="500" height="344" /></a>

<strong>Font Selection</strong>
7,500+

<strong>Advantage Over Other Services</strong>
Large Font selection

<strong>Pros</strong>
Currently the largest selection of fonts on the web. Exclusive home to popular fonts like Helvetica, Frutiger and Univers. Support for more than 40 languages. Use on unlimited domains. Download up to 50 desktop fonts per month with the Professional plan. JavaScript-free integration available to Standard and Professional subscribers.

<strong>Cons</strong>
Relatively expensive on a price-per-font basis when using a limited number of web fonts. The font selection interface is slower than average.

<strong>Pricing</strong>
Various tiers ranging from free up to $500/month. With a free tier, you have the ability to use any of 2000 fonts on an unlimited number of websites (up to 25,000 page views). Standard and Pro tiers will give you access to any of over 7,000 fonts. All pricing is dependent upon page views.

<strong>Fee Schedule</strong>
30 days

### Our Experience with Fonts.com Web Fonts

The service looks pretty straightforward. You set up a project with as many domains as you want and then select the fonts you want to use for that project. Selecting fonts is a bit slow (it takes 30 seconds or more for a font to actually be added to a project), but not enough to be prohibitive. There’s a huge selection of fonts and powerful tools for sorting through them, in addition to search capability.

From there, you have to enter each CSS selector for which you would like to use a web font and select the font used for that particular selector using a drop down menu that lists the fonts you already selected for the project. One place where Fonts.com really stands out is in the options you have for publishing your new web fonts. There are two different JavaScript options — an “Easy” option and an “Advanced” one — that let you add the fonts to selectors directly in your stylesheet rather than just through the web interface, as well as two non-JS options (also “Easy” and “Advanced”).

Again, the Fonts.com site was a bit slow overall but the end result is just as fast and seamless as any other service listed here.</p>

## Google Fonts

<strong>Google Fonts</strong>, announced last May, represents Google’s foray into web fonts. Google offers the service free of charge. Although the selection is currently limited to certain public domain fonts, it has the potential to have a significant impact on the future of web fonts.

<img loading="lazy" decoding="async" class="63077" title="google" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/379167d5-b92f-4ece-852c-012a0f00d8d2/fonts-18.jpg" alt="Google Fonts" width="500" height="337" />

<strong>Font Selection</strong>
60 (including international fonts)

<strong>Advantage Over Other Services</strong>
Free

<strong>Pros</strong>
Easy to implement. Fast font loading. Google’s WebFont Loader lets you use their service with multiple web font providers.

<strong>Cons</strong>
Small font selection in the Google font directory. <del>No support for iPhone or iPad (Mobile Safari).</del> Now with support for iPhone and iPad (Mobile Safari).

<strong>Pricing</strong>
Free

<strong>Fee Schedule</strong>
N/A

### Our Experience with Google Fonts

The Google Fonts API is probably the easiest of the services listed here to get started with, mostly because there is no sign-up process. You simply browse the fonts they offer, select one, and then get the code. Link the stylesheet in your website's head, and then add the font to the font stack in your stylesheet.

The service is very fast, with only a barely noticeable lag before loading the proper font. The fact that there are no limits on usage of the service puts it among the top contenders on this list. The only major drawback is the limited number of fonts available.</p>

## Kernest

<strong><a href="https://www.kernest.com/">Kernest</a></strong> is a hosted or self-hosted (you can also use Fontue, Kernest’s open source web font serving engine) web font tool that converts fonts into web font ready formats and sample code.

<a href="https://www.kernest.com"><img loading="lazy" decoding="async" class="63078" title="kernest" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a490026-f9ea-486f-b3a0-1be1127c401c/fonts-19.jpg" alt="Kernest" width="500" height="310" /></a>

<strong>Font Selection</strong>
2,450

<strong>Advantage Over Other Services</strong>
Most fonts are free

<strong>Pros</strong>
Open source web font serving engine. Large font selection.

<strong>Cons</strong>
Self-hosting only, which requires additional setup and technical skills

<strong>Pricing</strong>
Free or up to $15

<strong>Fee Schedule</strong>
One-time fee

### Our Experience with Kernest

Kernest has a great selection of free and paid fonts available. Free fonts could be set up without having to sign up for an account. Just find the font you want to use, make sure the permissions are acceptable for your intended use (not every font is allowed to be used on commercial sites, for example), and then copy and paste the link and CSS code into your files.

Kernest works as well as any of the others on this site, with minimal lag time before the fonts load.</p>

## Typotheque

<a href="https://www.typotheque.com/webfonts">Typotheque</a> is a graphic design studio and type foundry located in the Netherlands. Their hosted web font service includes a relatively small selection of Typotheque fonts. Typotheque was the first foundry to start its own web font service, and all fonts are designed in-house.

<a href="https://www.typotheque.com/webfonts"><img loading="lazy" decoding="async" class="63079" title="typotheque" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039aed24-f509-4f9b-bd3b-aa7d3338a0b9/fonts-20.jpg" alt="Typotheque" width="500" height="318" /></a>

<strong>Font Selection</strong>
37 font families, many supporting various styles and languages; this means there are over 500 single fonts.

<strong>Advantage Over Other Services</strong>
Use on unlimited websites

<strong>Pros</strong>
Option to purchase a full (web and desktop) license. Over 250 languages supported, and from those up to 5 languages can be embedded. All fonts are exclusive to and designed by Typotheque. Offers self-hosting for large websites.

<strong>Cons</strong>
Limited font selection (although this is only true because their fonts are exclusive) and monthly bandwidth (500MB for each font within a font family).

<strong>Pricing</strong>
20% of the full desktop license (ex. Fedra Sans Std Book: Full @ €90, Web @ €18).  Includes 500MB monthly bandwidth.

<strong>Fee Schedule</strong>
One-time fee (€5 for every extra GB over 500MB)

### Our Experience with Typotheque

Setup is similar to the other services listed here. Just select the font you want to use and the domains on which it will be used, add the stylesheet link to the head of your page, add the font to your font stacks, and you're ready to go. Lag time for the font to load is comparable to the other services. The biggest drawback is the lack of font selection, but as mentioned, this is due to the fact that their fonts are exclusive to Typotheque.

The service did return an error when generating the font subset, but it appeared to work fine, so not sure if that's a bug or if there would actually be problems with more extensive testing.</p>

## WebINK

<a href="https://www.extensis.com/en/WebINK/">WebINK</a> is a hosted web font platform developed by <a href="https://www.extensis.com/">Extensis</a>, a software development company based out of Portland, Oregon and specializing in font management.

<a href="https://www.extensis.com/en/WebINK/index.jsp"><img loading="lazy" decoding="async" class="63080" title="webink" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3f5e3f1-ae60-4752-8bcb-2f8dcc424659/fonts-21.jpg" alt="WebINK" width="500" height="357" /></a>

<strong>Font Selection:</strong>
2,000

<strong>Advantage Over Other Services</strong>
Can be affordable for the right type of user

<strong>Pros</strong>
Affordable pricing structure (similar to Typekit). Decent selection of fonts. Offers access both through the usual web interface, or alternatively through a desktop font management application called <a href="https://www.extensis.com/en/products/suitcasefusion3/overview.jsp">Suitcase Fusion 3</a> (Mac and Windows). This application has a live website preview mode for testing different fonts, and something called QuickMatch that finds the closest match to the chosen font on your computer.

<strong>Cons</strong>
Confusing interface and back-end. Each plan is limited to 4 websites (Note: Each user can set up as many "Type Drawers" as they want, allowing 4 websites per Type Drawer; so really the number of websites is only limited to an individual plan within a single user account, whereas the number of Type Drawers is unlimited).

<strong>Pricing</strong>
Free 30-day trial on all fonts. Packages start at $0.99 per month (only includes “Promotional” font selection) for 1GB usage and up to 4 websites.

<strong>Fee Schedule</strong>
Monthly subscription

### Our Experience with WebINK

We only tested the web interface for WebINK, not Suitcase Fusion 3. The WebINK online interface is probably more confusing than the others listed here. The service allows you to create an unlimited amount of Type Drawers to hold the fonts for your different projects. To add fonts from the library into your Type Drawers, you need to click the "add fonts" button within a specific Drawer. Going directly to the font library will not allow you to have direct access to your Drawers, so this takes some getting used to.

Once you get the fonts you want into your Type Drawer, setting them up on your website requires adding the <code>@font-face</code> information to your stylesheet and placing the fonts into your font stacks. The speed at which the font loads on the site is about the same as any other service.</p>

## Font-Face

<a href="https://www.font-face.com/">Font-Face</a> recently scrapped its project after the recent Google Font announcement. However, according to their website, they are "hatching a new plan" so we may hear more from them yet.

<a href="https://www.font-face.com"><img loading="lazy" decoding="async" class="63081" title="font-face" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bcc11c1-be00-43ed-94ef-cc76199cbfe9/fonts-22.jpg" alt="Font-Face" width="500" height="335" /></a>

## How to Choose a Service

There is no “right” answer when it comes to choosing a web font service. Selecting the proper service usually depends on what you or your client need. You could ask yourself the following questions to help assess your needs:

*   How important is font selection? Are there specific fonts you need?
*   How important is font quality to you and your clients?
*   Do you require a self-hosting option?
*   Do you or your client have a budget? What type of fee structure would be ideal?
*   Is iPhone and iPad (Mobile Safari) support important?

Based on your answers to these questions you should be able to use the quick comparison chart below, along with the more detailed information above, to make an informed decision, or at the very least find a few starting points to start digging deeper (also be sure to check out the great chart <a href="https://fffo.grahambird.co.uk/">@font-face face off</a>).

<a href="https://fffo.grahambird.co.uk/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/363082be-db3d-42f8-af7c-96687d01e710/fonts-23.jpg" alt="Screenshot" width="500" height="339" /></a>

## Quick Overview

Here is a short overview of the services reviewed in this article, including the number of fonts in each, advantages over other services, price and fee schedule.
<table border="0" cellspacing="0" cellpadding="4"><br>
<tbody>
<tr>
<td width="103"><strong>Service</strong></td>
<td width="96"><strong>Fonts</strong></td>
<td width="126"><strong>Advantage Over Other Services</strong></td>
<td width="162"><strong>Price</strong></td>
<td width="102"><strong>Fee Schedule</strong></td>
</tr>
<tr>
<td width="103"><a href="https://www.typekit.com/">Typekit</a></td>
<td width="96">4000</td>
<td width="126">Integrations</td>
<td width="162">Plans start at $24.99</td>
<td width="102">Annual</td>
</tr>
<tr>
<td width="103"><a href="https://www.webtype.com/">Webtype</a></td>
<td width="96">365</td>
<td width="126">Font quality</td>
<td width="162">Fonts start at $10</td>
<td width="102">Annual</td>
</tr>
<tr>
<td width="103">Fontdeck</td>
<td width="96">600</td>
<td width="126">Pay-per-use</td>
<td width="162">Free / $2.50 and up</td>
<td width="102">Annual</td>
</tr>
<tr>
<td width="103">Fonts Live</td>
<td width="96">499</td>
<td width="126">Font quality</td>
<td width="162">Fonts start at $10</td>
<td width="102">Annual</td>
</tr>
<tr>
<td width="103">TypeFront</td>
<td width="96">N/A</td>
<td width="126">Do-it-yourself</td>
<td width="162">Plans start at $5</td>
<td width="102">Monthly</td>
</tr>
<tr>
<td width="103"><a href="https://www.fontspring.com/">Fontspring</a></td>
<td width="96">1,937 families</td>
<td width="126">No recurring fee</td>
<td width="162">Free to $100s</td>
<td width="102">One-time</td>
</tr>
<tr>
<td width="103"><a href="https://webfonts.fonts.com/">Fonts.com</a></td>
<td width="96">7,500+</td>
<td width="126">Font selection</td>
<td width="162">Free or up to $500</td>
<td width="102">30 days</td>
</tr>
<tr>
<td width="103">Google Fonts</td>
<td width="96">60</td>
<td width="126">Easy to implement</td>
<td width="162">Free</td>
<td width="102">N/A</td>
</tr>
<tr>
<td width="103"><a href="https://www.kernest.com/">Kernest</a></td>
<td width="96">2,450</td>
<td width="126">Most fonts free</td>
<td width="162">Free or up to $15</td>
<td width="102">One-time</td>
</tr>
<tr>
<td width="103"><a href="https://www.typotheque.com/webfonts">Typotheque</a></td>
<td width="96">524</td>
<td width="126">Unlimited websites</td>
<td width="162">20% of desktop license</td>
<td width="102">One-time</td>
</tr>
<tr>
<td width="103"><a href="https://www.extensis.com/en/WebINK/">WebINK</a></td>
<td width="96">2,000</td>
<td width="126">Affordable</td>
<td width="162">Plans start at $0.99</td>
<td width="102">Monthly</td>
</tr>
</tbody>
</table>

## Summary

Web font services, like any relatively new popular technology, are complex and rapidly proliferating.  While there is no “perfect” service, it’s promising to see such a wide variety of companies entering the industry and continually raising the bar for web fonts. I hope this breakdown helps you get a better handle on what’s available. If you’ve had your own experience using a web font service, please let us know in the comments.</p>

### Related Resources

*   [Graham Bird's Font Face Face Off](https://fffo.grahambird.co.uk/)
*   [10 Tools for Better Web Fonts](https://www.paper-leaf.com/blog/2010/06/10-tools-for-better-web-fonts/)
*   [Font-Face Guide](https://sixrevisions.com/css/font-face-guide/)
*   [50 Useful Design Tools For Beautiful Web Typography](https://www.smashingmagazine.com/2009/01/27/css-typographic-tools-and-techniques/)
*   [Expressive Web Typography: Useful Examples and Techniques](https://www.smashingmagazine.com/2010/09/13/expressive-web-typography-useful-examples-and-techniques/)
*   Why webfont services are the future of fonts on the web
*   [The Font-as-Service](https://ilovetypography.com/2009/08/07/the-font-as-service/ "The Font-as-Service")
*   Web Fonts: Foundries Evolved
*   [On Web Typography](https://www.alistapart.com/articles/on-web-typography/)
*   Ultimate Web Typography: Resources and Inspiration

<strong><em>Disclosure:</em></strong><em> This article was co-written by Andrew Follett and Cameron Chapman. Andrew has provided consulting services for Ascender Corporation. Impressions were written exclusively by Cameron. All facts were checked and updated by Louis Lazaris.</em>

