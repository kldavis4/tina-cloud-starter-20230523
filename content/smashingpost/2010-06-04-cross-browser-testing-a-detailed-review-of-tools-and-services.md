---
title: 'Cross-Browser Testing: A Detailed Review Of Tools And Services'
slug: cross-browser-testing-a-detailed-review-of-tools-and-services
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e0df9e8-6e5d-44fb-82db-951ebd2bab28/diagram-raphael-illu.jpg
date: 2010-06-04T11:23:47.000Z
author: demiurg
description: >-
  As you probably know, cross-browser testing is an important part of any
  developer's routine. As the number of browsers increase, and they certainly
  have in recent years, the need for automatic tools that can assist us in the
  process becomes ever greater. In this article, we present an overview of
  different cross-browser testing applications and services. Surely, you are
  already familiar with some of them, and you may have even stumbled across
  another overview article, but this one takes a different approach.

  This is not just a list of available tools, but rather a **comprehensive
  analysis** based on my experience with each of them. For the impatient among
  you, a summary table is at the end summarizing key metrics and unique features
  for each service. But if you're interested in my personal experience with
  these tools, then read on.
categories:
  - Coding
  - Tools
  - Browsers
  - Testing
---
As you probably know, cross-browser testing is an important part of any developer's routine. As the number of browsers increase, and they certainly have in recent years, the need for automatic tools that can assist us in the process becomes ever greater. In this article, we present an overview of different cross-browser testing applications and services. Surely, you are already familiar with some of them, and you may have even stumbled across another overview article, but this one takes a different approach.

This is not just a list of available tools, but rather a <strong>comprehensive analysis</strong> based on my experience with each of them. For the impatient among you, a summary table is at the end summarizing key metrics and unique features for each service. But if you're interested in my personal experience with these tools, then read on.

You may also want to check out the following Smashing Magazine articles:

*   [Review Of Cross-Browser Testing Tools](https://www.smashingmagazine.com/2011/08/a-dozen-cross-browser-testing-tools/)
*   [Reliable Cross-Browser Testing, Part 1: Internet Explorer](https://www.smashingmagazine.com/2011/09/reliable-cross-browser-testing-part-1-internet-explorer/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [High-Impact, Minimal-Effort Cross-Browser Testing](https://www.smashingmagazine.com/2016/02/high-impact-minimal-effort-cross-browser-testing/)

Probably the most important metric of these services is the capture delay, which I measured for the URL <a href="https://www.stackoverflow.com">stackoverflow</a>, with the following browsers enabled: Firefox, IE, Chrome and Safari.

{{% feature-panel %}}

## BrowserShots

<a href="https://www.browsershots.org">BrowserShots</a> is the oldest and best known free online multi-browser screenshot service. It supports the largest number of browsers: a total of 61 different browser versions and operating systems, which is great, but I can hardly imagine anyone wanting to test their website under Kazahakase 0.5 running on BSD Unix. Feature-wise, it allows you to enable and disable Javascript, Java and Flash and change the screen size. I find the latter very useful, especially nowadays when one has to take into account smartphone browsers with non-standard resolutions.

<a href="https://www.browsershots.org"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b90362dd-6cb5-4d3c-819c-89d56ac484a2/testing-01.jpg" alt="Screenshot" width="500" height="300" /></a>

The interface is <strong>not very user-friendly</strong>. Selecting the browsers and options you want takes time, and because it is a Web service you have to do it over every time you want to take a screenshot. When (and if) you finally get your screenshots, there is no easy way to compare different captures in order to find rendering inconsistencies. HTTP redirect is not fully automated: BrowserShots displays the URL you are being redirected to, but you have to start the screenshot again manually.

The biggest disadvantage of BrowserShots—which, in my opinion, makes it practically unusable for a professional developer — is the response time. In our test scenario, it was more than 45 minutes. Note that a screenshot expires in 30 minutes, unless you manually extend it. As you can see from the shot below, BrowserShots has serious bugs with scrolling (see MSIE 8.0 screenshot) and at least one browser screenshot failed, even though it said the operation was successful.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bb0655c-fe39-4a60-9485-66bae325c594/browsershots1.jpg"><img loading="lazy" decoding="async" class="44720 aligncenter" title="browsershots" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bb0655c-fe39-4a60-9485-66bae325c594/browsershots1.jpg" alt="" width="500" height="388" /></a>

### Conclusion

Unless you need only a single test on a particular browser, this service is not for you. Even then, by the way, it would probably take less time to install that browser, test the page and then uninstall it.

<strong>Unique features:</strong> None.

<strong>Disadvantages:</strong> Painfully slow.</p>

## BrowserCam

BrowserCam is another well-known screenshot service. Unlike BrowserShots, this is a commercial service. The cheapest plan cost $159.80 a year and provides access for five users. The <strong>interface is nice</strong>. It allows you to create a project and specify the URL and browsers you want to capture, so that you do not have to do it all over again to re-test the page. But because it is a non-AJAX Web-based interface, its response time is not comparable to that of a native application, which is a bit annoying.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e46d2fa-d905-431e-b53a-97b66fad3119/testing-09.jpg" alt="Screenshot" width="500" height="300" />

Browser support is slightly more limited than that of BrowserShots, but it is good enough for practical purposes; it supports multiple versions of IE, Firefox, Safari, Opera and Chrome, as well as some older browsers on OS X, Linux and multiple versions of Windows. Capture speed is decent: it took about two minutes to take a screenshot of our test scenario.

BrowserCam supports multiple resolutions and has window and full-page capture, which means scroll bar support. Another nice feature is mobile device capture: it supports Blackberry, iPhone, Android and Windows Mobile devices. Note that mobile capture support is not part of the browser capture plan and costs $999.95 extra annually. It also has an <strong>email capture service</strong>, which in my opinion is of limited use, and remote access, which can be useful for troubleshooting rendering inconsistencies that are detected from a screen capture. Both services cost extra. The screenshot below is of a BrowserCam results window.

Remote access packages allow you to connect using VNC to your choice of Linux, Windows and Mac machines with different browser versions. This can be a good option for debugging on hardware that you do not have, such as Mac. But the price of $499.95 a year is not far from the price of Mac mini, and because the VNC protocol is not terribly efficient, extensive remote debugging via VNC can be daunting.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7608e195-1c5c-40c3-8d58-cf8fbd6ec248/browsercam.jpg"><img loading="lazy" decoding="async" class="43565 aligncenter" title="browsercam" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7608e195-1c5c-40c3-8d58-cf8fbd6ec248/browsercam.jpg" alt="" width="500" height="400" /></a>

### Conclusion

A very good professional service with advanced features and thoughtful interface.

<strong>Unique features:</strong> Mobile device support, remote access.

<strong>Disadvantages:</strong> Expensive.</p>

## Adobe BrowserLab

<a href="https://browserlab.adobe.com">BrowserLab</a> is a new offering from Adobe and was previously known as <em>Meer-Meer</em>. It is written in Flash and as such has the advantage of being cross-platform compatible and of having the look, feel and (most importantly) response time of an application. It is currently offered <strong>free of charge in preview mode</strong> while Adobe "is monitoring the performance." Because it will monitor it for more than one year, one wonders whether it has other reasons for this. According to Adobe, it will charge $10 to $20 per month for this service starting in 2011.

<a href="https://browserlab.adobe.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d0dc78b-561d-433e-a761-05226fa7344e/testing-03.jpg" alt="Screenshot" width="500" height="300" /></a>

The interface is attractive, polished and easy to use, as you can see from the screenshot below. You can inspect captures one by one or view two captures side by side, which is more useful. The much lauded "onion skin" option is not very practical: most of the time, browsers will not render a page identically pixel by pixel, but the page might still look the same.

Browser support is modest compared to the competition. At the time of writing, BrowserLab supports only Chrome, Firefox, IE and Safari: a total of 12 browsers and OS version combinations. But it looks like the quality of the product is still at beta level; in two captures, it actually cut the image horizontally. Scroll bar support is buggy, too.

Screenshot speed is very good. Our test scenario did it in less than one minute.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35603226-4240-48cf-821f-bc057837f360/browserlab1.jpg"><img loading="lazy" decoding="async" class="44718 aligncenter" title="browserlab" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35603226-4240-48cf-821f-bc057837f360/browserlab1.jpg" alt="" width="500" height="388" /></a>

### Conclusion

A very nice interface, and free till the end of 2010.

<strong>Unique features:</strong> None.

<strong>Disadvantages:</strong> Modest browser support, minor bugs.</p>

## Microsoft Expression Web SuperPreview

<a href="https://expression.microsoft.com/en-us/cc136529.aspx">SuperPreview</a> is a new addition to Microsoft's Expression Web WYSIWYG development environment. This is the standalone version, limited to Internet Explorer and available for download free of charge. Browser support is limited. The standalone version supports only IE 6, 7 and 8, while the full version has support for Firefox and Safari. The user experience, on the other hand, is very impressive.

<a href="https://expression.microsoft.com/en-us/cc136529.aspx"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f90b0665-a4f2-4814-91e0-38e5f85d0b9c/testing-04.jpg" alt="Screenshot" width="500" height="300" /></a>

Because it is an application that runs on your PC, the response time and screenshot delay are among the best in class. In our test scenario, it loaded the website in a matter of seconds. Please note, though, that because SuperPreview works with only two browsers at a time and does not support Chrome, this test was not identical to that of other services.

SuperPreview cannot be purchased without the Expression Web, whose retail price is $149.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20203dce-ced9-48b5-bbb7-e273e85508d2/superpreview1.jpg"><img loading="lazy" decoding="async" class="44723 aligncenter" title="superpreview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20203dce-ced9-48b5-bbb7-e273e85508d2/superpreview1.jpg" alt="" width="500" height="388" /></a>

### Conclusion

The interface is extremely easy to use, and the speed is incredible. But browser support is very limited, and being part of the Expression Web package, it's almost unusable.

<strong>Unique features:</strong> None.

<strong>Disadvantages:</strong> Limited browser support, expensive.</p>

### Conclusion

A very nice tool, with comprehensive browser support. The interface is easy to use, the capture speed is great, and the price is competitive.

<strong>Unique features:</strong>: Comes with standalone versions for all major browsers; has command-line mode for automation scripts.

<strong>Disadvantages:</strong>: Runs on Windows only.</p>

## Litmus

<a href="https://litmusapp.com/">Litmus</a> is another Web-based screenshot service. Its browser support is impressive, with 23 browser versions and operating system combinations, including IE, Firefox, Chrome, Safari, Opera, Flock, Camino, SeaMonkey and Netscape. Capture speed is okay but not comparable to that of native applications: our test took five minutes.

<a href="https://litmusapp.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd7a92ac-7a9f-4dac-a827-b878bc162c3a/testing-06.jpg" alt="Screenshot" width="500" height="300" /></a>

The interface is clear and simple but lacks some features. For instance, there is no easy way to compare capture results. All you can do is view them one by one or download them to your PC. The app, though, does support projects, so you don't have to enter URLs and change browser settings every time you want to take a screenshot, but this is pretty much all it does.

Litmus does not support scrolling; that is, it captures only the top of long pages, which is a major drawback. The price is a bit high for a service that has such basic features: a single-user license costs $588 annually.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5bd7728-8a87-4d3d-9cfe-5dab0504d371/litmusapp1.jpg"><img loading="lazy" decoding="async" class="44721 aligncenter" title="litmusapp" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5bd7728-8a87-4d3d-9cfe-5dab0504d371/litmusapp1.jpg" alt="" width="500" height="388" /></a>

### Conclusion

Good browser support, and average capture speed, which is probably good enough for most users. But very few features.

<strong>Unique features:</strong>: None.

<strong>Disadvantages:</strong> Does not support scrolling, and lacks other standard features found in competing products.</p>

## Multi-Browser Viewer

<a href="https://www.multibrowserviewer.com">Multi-Browser Viewer</a> is an application but relies on a server farm for browser rendering; in other words, the application is just a graphical interface, so it is as easy to use as an application but suffers the delays of a typical Web-based service.

<a href="https://www.multibrowserviewer.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/251f9b88-de39-472a-9b4d-b6c5a1593d73/testing-07.jpg" alt="Screenshot" width="500" height="300" /></a>

One interesting feature is that it comes with standalone browsers that can be used for debugging. But note that these are not the same browsers used for screen capture. Multi-Browser Viewer has standalone browsers that can be used for debugging, and it has a rendering farm with many more browsers that can be used for screen capture.

Browser support is impressive, with 54 browser and OS version combinations (out of which 17 are available in standalone versions), including IE, Firefox, Chrome, Opera, Safari, Camino, Konqueror. The price is reasonable: a single-user license costs $129.95 annually.

Feature-wise, it does lag significantly behind the competition: there is no support for authentication or capture delay. Scroll bar support is buggy; in our test case, it worked for IE, Firefox and Safari, but not for Opera.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8173d5a4-6600-49ec-b476-5c050599c073/multibrowserviewer1.jpg"><img loading="lazy" decoding="async" class="44722 aligncenter" title="multibrowserviewer" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8173d5a4-6600-49ec-b476-5c050599c073/multibrowserviewer1.jpg" alt="" width="500" height="387" /></a>

### Conclusion

A good interface and impressive browser support.

<strong>Unique features:</strong> Standalone versions of some (but not all) browsers.

<strong>Disadvantages:</strong> Lacks many features of competing products, buggy scroll bar support, runs on Windows only.</p>

## Browsera

<a href="https://www.browsera.com/">Browsera</a> is a Web-based screenshot service. Browser support is limited compared to that of most competitors: only IE, Firefox and Safari are supported. The standard plan costs $588 annually. The interface is attractive, fast and clean. You can conveniently organize your screenshot sessions into projects.

<a href="https://www.browsera.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87e3a3ec-b289-45f6-8a15-d6a3d597b659/testing-08.jpg" alt="Screenshot" width="500" height="300" /></a>

Browsera supports authentication, scroll bars and page crawling (i.e. you can ask Browsera to crawl your website recursively and take a screenshot of every page). The screenshot response time is very fast for a Web-based service; it completed our test in three minutes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8478c3-9f3a-4735-8fca-ad1a21ba3071/browsera1.jpg"><img loading="lazy" decoding="async" class="44716 aligncenter" title="browsera" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8478c3-9f3a-4735-8fca-ad1a21ba3071/browsera1.jpg" alt="" width="500" height="388" /></a>

### Conclusion

A professional service with a good interface and interesting features, but limited browser support.

<strong>Unique features:</strong> Recursive website crawling.

<strong>Disadvantages:</strong> Limited browser support, expensive.</p>

## Browser Packs

If all you need is to test your website in specific browsers with and you are willing to perform the tests manually, there are a few free services and applications that could help:

*   [Spoon](https://spoon.net/browsers/)
*   [BrowserSeal.BrowserPack](https://www.browserseal.com/?option=com_content&view=article&id=35)
*   [Internet Explorer Collection](https://utilu.com/IECollection/)
*   [IE Tester](https://www.my-debugbar.com/wiki/IETester/HomePage)

At first glance, Spoon looks convenient because it is a Web service, which relieves you from having to install many browsers locally. But I had some stability problems with this service.

Meanwhile, both the IE Collection and BrowserSeal.BrowserPack (offered free of charge, separate from the BrowserSeal commercial screenshot service) work very reliably. I did not have any issues with browsers installed by these packs. The IE Collection has every IE version you could think of. BrowserSeal.BrowserPack, which relies on the IE Collection for IE support, also supports two Firefox, three Opera and two Safari versions.</p>

## Conclusion

The following table summarizes services that were tested and analyzed in the article. You can use the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/365277f8-d4aa-4d52-a1f9-bf5bc167cede/cross-browser-testing-table.html">separate page for the full table</a> for a better overview. I have included some metrics for each service to make it easier for you to choose the best one based on price, features and performance trade-offs.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th></th>
<th style="min-width: 190px">Supported Browsers</th>
<th>Capture speed</th>
<th style="min-width: 100px">Price (1 year)</th>
<th>Interface</th>
<th>Authentication</th>
<th>Capture delay</th>
<th>Scroll bars</th>
<th style="min-width: 200px">Special features</th>
</tr>
</thead>
<tbody>
<tr>
<td class="head"><a href="https://www.browsershots.org/">BrowserShots</a></td>
<td>IE, Firefox, Chrome, Opera, Safari, Dilo, SeaMonkey, Minefield, Epiphany, Flock, Galeon, Konqueror, K-Meleon, Avant, Netscape, Shireteko, Kazehakase, Iceweasel</td>
<td>45 mins</td>
<td>Free</td>
<td>Bad</td>
<td>No</td>
<td>No</td>
<td>No</td>
<td>None</td>
</tr>
<tr>
<td class="head">BrowserCam</td>
<td>IE, Firefox, Chrome, Opera, Safari, Konqueror, Camino, Netscape, AOL</td>
<td>2 mins</td>
<td>$999.95</td>
<td>Good</td>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
<td>Mobile browsers support, remote access service</td>
</tr>
<tr>
<td class="head"><a href="https://browserlab.adobe.com/">BrowserLab</a></td>
<td>IE, Firefox, Chrome and Safari</td>
<td>1 min</td>
<td>Free (till end of 2010)</td>
<td>Good</td>
<td>No</td>
<td>Yes</td>
<td>Buggy</td>
<td>None</td>
</tr>
<tr>
<td class="head"><a href="https://expression.microsoft.com/en-us/cc136529.aspx">SuperPreview</a></td>
<td>IE, Firefox and Safari</td>
<td>1 min</td>
<td>$149</td>
<td>Good</td>
<td>No</td>
<td>No</td>
<td>Yes</td>
<td>None</td>
</tr>
<tr>
<td class="head"><a href="https://www.browserseal.com/">BrowserSeal</a></td>
<td>IE, Firefox, Chrome, Opera and Safari</td>
<td>1 min</td>
<td>$49</td>
<td>Good</td>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
<td>Standalone browser versions, support for automation scripts</td>
</tr>
<tr>
<td class="head"><a href="https://litmusapp.com/">Litmus</a></td>
<td>IE, Firefox, Chrome, Opera, Safari, Flock, Camino, SeaMonkey, Netscape</td>
<td>5 mins</td>
<td>$588</td>
<td>Basic</td>
<td>Yes</td>
<td>No</td>
<td>No</td>
<td>None</td>
</tr>
<tr>
<td class="head"><a href="https://www.multibrowserviewer.com/">Multi Browser Viewer</a></td>
<td>IE, Firefox, Chrome, Opera, Safari, Flock, SeaMonkey, Netscape, K-Meleon, Camino, Konqueror, Epiphany, Kazehakase</td>
<td>2 mins</td>
<td>$129.95</td>
<td>Good</td>
<td>No</td>
<td>No</td>
<td>Buggy</td>
<td>Standalone browser versions</td>
</tr>
<tr>
<td class="head"><a href="https://www.browsera.com/">Browsera</a></td>
<td>IE, Firefox, Safari</td>
<td>3 mins</td>
<td>$588</td>
<td>Good</td>
<td>Yes</td>
<td>No</td>
<td>Yes</td>
<td>Recursive crawling</td>
</tr>
</tbody>
</table>

Obviously, we have no clear winner. Each service has its advantages and disadvantages, and you are left to decide what is the best trade-off for your case. Professional developers would likely not use BrowserShots because of the unreasonably long response time. SuperPreview and Browsera are probably also impractical because of their very limited browser support.

BrowserLab will probably remain popular as long as it is free. Once Adobe starts charging about $20 per month for it, one would hardly have reason to use it, unless you worked in Dreamweaver, which has a BrowserLab extension, because there are much better alternatives.

When choosing a tool, one of the most important factors in your decision will be whether to use a Web service or application. Some people prefer Web-based tools because they do not require installation. Personally, I prefer applications, at least for the development tools that I use frequently. They generally have a better interface and faster response time; they never have outages, and they can be used to debug locally (i.e. on my hard drive or company intranet — although some Web-based services offer a workaround for this issue).

BrowserCam, BrowserSeal, Litmus and Multi-Browser Viewer are all very good choices. But they do vary significantly in price. If you need to test mobile browsers, BrowserCam is probably your only option. For everyone else, I would recommend either BrowserSeal or Multi-Browser Viewer; both come with standalone browser versions that are extremely important for testing. Unfortunately, both of them are Windows only, so Mac users will probably have to go with BrowserLab or BrowserCam. If automatic testing is important to you, then the BrowserSeal automation edition is your best bet.

{{< signature "al" >}}

