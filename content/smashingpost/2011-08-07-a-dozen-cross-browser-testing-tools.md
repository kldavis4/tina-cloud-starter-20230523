---
title: 'Review Of Cross-Browser Testing Tools'
slug: a-dozen-cross-browser-testing-tools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddbf57fb-1f59-4135-8b5b-eceedcfc371f/browsers-bunch-illu.jpg
date: 2011-08-07T08:24:40.000Z
author: cameron-chapman
summary: >-
  Regardless of the tool you choose, testing early and often during the Web development process can save you from a lot of headaches later. Find a tool that fits your workflow with a little help from Cameron Chapman.
description: >-
  Regardless of the tool you choose, testing early and often during the Web development process can save you from a lot of headaches later. Find a tool that fits your workflow with a little help from Cameron Chapman.
categories:
  - Coding
  - Tools
  - Testing
  - Reviews
---

At some point in the future, the way that all major browsers render Web code will likely be standardized, which will make testing across multiple browsers no longer necessary as long as the website is coded according to Web standards. But because that day is still a way off (if it will really come at all), testing your design the advanced browsers as well as legacy browsers is a necessary part of any project.

The old-school way to test code was to load your website on as many computers as you could find, using as many different combinations of browsers and operating systems as possible. That was fine if you had access to a bunch of different computers (and had some time to kill). But there are much more **efficient ways to test across browsers**, using either free or commercial Web services and software. In this article we review some of the most useful ones.

{{% feature-panel %}}

## Free Cross-Browser Testing

Good news: very powerful free testing tools are available for Web designers today. Some are more user-friendly than others, and some have significantly better user interfaces. Don’t expect much (if any) support with these tools. But if you’d rather not spend extra money on testing, some great options are here as well.

### Adobe BrowserLab

Adobe BrowserLab is a free cross-browser compatibility tool that lets you test a number of modern and legacy browsers, including various versions of Chrome, Safari, IE and Firefox. It gives you a number of ways to view pages, including a full-page view in a single browser, as well as side-by-side comparisons of browsers and an onion skin view. The service can access dynamic pages across the web, or viewed locally via Firebug or Adobe Dreamweaver CS5. The ability to create pre-defined browser sets is also useful, in case you don’t need to test on older browsers.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/377215d9-15a5-41eb-b38d-4a00b484f468/adobebrowserlab.jpg" alt="" /></figure>

### Browsershots

<a href="https://browsershots.org/">Browsershots</a> is probably the most comprehensive free testing tool available. It includes Linux, Windows and BSD browsers. It also includes a number of browsers you’ve probably never heard of (like Galeon, Iceape, Kazehakase and Epiphany). For the most part, Browsershots tests on the most recent version of each browser, as well as on legacy versions.

While Browsershots does support a huge variety of browsers, the more you test, the more slowly it prepares the results. So, you may want to stick to the major browsers.

<figure><a href="https://browsershots.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c7b3be-6406-46c8-a7ab-6b0f292e40bc/browsershots.jpg" alt="" /></a></figure>

### SuperPreview (Free and Commercial)

<a href="https://expression.microsoft.com/en-us/dd565874.aspx">SuperPreview</a> is Microsoft’s offering in this space (and it’s compatible only with Windows). It lets you define your own “baseline” (or default) browser, and it works with any browser installed on your system (and comes with the IE6 rendering engine built in). The fact that it only works with your built-in browsers does make it faster (because you’re not uploading anything or waiting for a remote server), but it also limits the number of browsers you can compare.

SuperPreview trial comes with 60 days of cloud services before you have to either buy it or go into reduced, (local browsers and IE 6-9 mode). In an online version, you have support for Chrome, Safari (Mac) 4+5, Firefox 3+4. You can also use an interactive mode to log into sites that require a login before displaying the page you want to test. There are also debugging tools for the DOM and onion skinning available in Adobe Browserlabs. Unfortunately, there is no support for Opera whether installed locally or in the cloud and you do have to have the version included with Expression Web to get the cloud services option but the base version with support for IE 6, IE 7, IE 8 (and IE 8 rendering as IE 7) are included with the free version as well as IE 9 if it is installed locally. (*Thanks, Cheryl D Wise*)

<figure><a href="https://expression.microsoft.com/en-us/dd565874.aspx"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bda560fe-fc76-48a0-b08b-fbabf39b73b1/superpreview.jpg" alt="" /></a></figure>

### Lunascape 6

<a href="https://www.lunascape.tv/">Lunascape</a> is a triple-engine browser for Windows. It runs Trident (IE), Gecko (Firefox) and Webkit (Chrome and Safari), so that you can see how your website looks in all three, side by side. While it’s not a traditional browser compatibility tester, it is nonetheless a useful tool for designers and developers. One major benefit is that you get to view your website instantly in all three major rendering engines. There’s also support for Firefox extensions and plug-ins, so you can use developer tools like Firebug to diagnose compatibility problems.

<figure><a href="https://www.lunascape.tv/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d115617-758e-4372-a1d4-835c21b1340e/lunascape.jpg" alt="" width="550" height="400" /></a></figure>

### IETester

<a href="https://www.my-debugbar.com/wiki/IETester/HomePage">IETester</a> is a free (both for personal and professional usage) browser for Windows that allows you to have the rendering and JavaScript engines of IE10 preview, IE9, IE8, IE7, IE6 and IE5.5 on Windows 7, Vista and XP, as well as the installed IE. Only an alpha version of the tool is available. Windows 7, Windows Vista or Windows XP with IE7 minimum are required for the tool to run.

<figure><a href="https://www.my-debugbar.com/wiki/IETester/HomePage"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c90dd1-4020-441f-96bb-41659c60712c/ietester1.jpg" alt="" width="550" height="318" /></a></figure>

### IE NetRenderer

<a href="https://www.ipinfo.info/netrenderer/">IE NetRenderer</a> lets you check compatibility in Internet Explorer versions 5.5 through 9. You’ll have to check each version individually, but the service is free.

<figure><a href="https://www.ipinfo.info/netrenderer/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/068e8e1b-3b89-40d5-bc1a-6a17b34576e6/ienetrenderer.jpg" alt="" /></a></figure>

### Spoon

<a href="https://spoon.net/browsers/">Spoon</a> is an application emulation service. It provides free versions of Firefox, Chrome, Opera and Safari for Windows users. A number of versions of each browser are included: Firefox 2&ndash;5, Chrome 4&ndash;8, Safari 3&ndash;5 and Opera 9&ndash;10. Bad news: Internet Explorer is supported by Spoon virtualization but is not available by request of Microsoft.

<figure><a href="https://spoon.net/browsers/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937f3e48-9c2c-495a-81f1-bc12bdf4fc7a/spoon.jpg" alt="" /></a></figure>

### Sauce Labs (free and commercial)

<a href="https://saucelabs.com/">Sauce Labs</a> provides a lot of browser and OS options and sets you up with a browser dedicated VM instance that you operate inside the browser of your choice. It also records a video of your entire testing session. The service offers 200 free minutes of testing per month and allows you to quickly build automated tests from your browser with Selenium.

<figure><a href="https://saucelabs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f7d47d-49b4-40d9-8822-b74f421bffe9/sauce-labs.jpg" alt="" width="550" height="335" /></a></figure>

### Browsera (free and commercial)

<a href="https://www.browsera.com/">Browsera</a> provides automated compatibility testing. It automatically highlights differences in the way browsers render your design, thus simplifying the testing process. It also detects JavaScript errors, and the commercial version can test pages behind subscription or log-in walls. It can also test dynamic pages.

The free plan includes a limited number of browsers and low-resolution screenshots. Premium plans start at $39 for a single project and $49 to $99 for monthly subscriptions, and they support more browsers, provide high-resolution screenshots and let you test private pages.

<figure><a href="https://www.browsera.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a66f2ce2-0926-4f73-8f76-5814804ed063/browsera.jpg" alt="" /></a></figure>

{{% ad-panel-leaderboard %}}

### Browserling (Free And Commercial)

<a href="https://browserling.com/">Browserling</a> is a relatively new cross-browser testing app. It supports a limited number of browsers (and not necessarily the newest versions), which makes it of limited use to some developers. It’s still in beta, though, so hopefully more browsers will be supported in the near future.

The free version comes with a five-minute session limit, and the developer version is $20 per month with no time limit.

<figure><a href="https://browserling.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff6d283c-07c9-46fa-9684-ddab4ca6287d/browserling.jpg" alt="" /></a></figure>

## Commercial Cross-Browser Testing

Commercial tools often have features not found in the free ones, including live interactive browser virtualization and mobile device testing.

### Mogotest

Mogotest does complete browser-compatibility testing, including for private pages. There’s an API, so it can be integrated in your current tools and workflow. Mogotest also offers a website health report that tells you about broken links and pages, redirect loops and other issues common to new websites. The service also offer screenshot comparison tools for testing screenshots against each other as well as site-level testing including page consistency testing and individual page tests. HTTP basic and cookie-based login systems are supported as well.

There are two plans for individuals: a personal plan starting at $15 per month that lets you test up to 50 pages on three websites, and a freelancer plan for $45 per month that includes up to 10 websites and 350 pages. The team plans start at $125 per month and go up to $4499+ for unlimited access. The two highest-cost plans include custom reports.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fa8b2cb-95cc-49b3-989b-ed0215b76c86/mogotest.jpg" alt="" /></figure>

### Cloud Testing

Cloud Testing offers functional cross-browser testing. You record the user journey with your browser and Selenium IDE, upload it, and then Cloud Testing will run that script in multiple operating systems and browsers. It then provides screenshots and HTML and component diagnostics. No prices are listed on its website.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0257322-9dab-4ad2-9c7f-c4a375991acb/cloudtesting.jpg" alt="" /></figure>

### BrowserCam

BrowserCam includes testing tools for both desktop and mobile browser compatibility (the latter is still absent in many other tools). It also offers remote access for live testing on Windows, Linux and OS X configurations, and email capture for checking your HTML, RTF and TXT emails.

Pricing for BrowserCam starts at only $19.95 per day for a single service (and $24.95 for the browser, remote access and email capture package), up to an annual subscription price of $399.95 for a single service (and $499.95 for browser capture, remote access, email capture and multi-user access, or $999.95 for all of those features plus device capture).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efa09f23-2905-4b83-969c-d06e75095d6b/browsercam.jpg" alt="" /></figure>

### Multi-Browser Viewer

<a href="https://www.multibrowserviewer.com/">Multi-Browser Viewer</a> covers both desktop and mobile browsers. It includes 26 virtualized Web browsers, 5 mobile browsers (including the iPhone and iPad) and 61 screenshot browsers (meaning you can see how the website renders but not interact with it). It’s also available in five languages: English, Spanish, German, Russian and French.

Multi-Browser Viewer is $139.95 for a single-user license and includes a year of product usage and updates. Updates after the first year are currently $99.95. A free trial is available through the website.

<figure><a href="https://www.multibrowserviewer.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e10c2f9c-9d2a-4a04-8b77-3cbacef71556/multibrowserviewer.jpg" alt="" /></a></figure>

### CrossBrowserTesting

<a href="https://crossbrowsertesting.com/">CrossBrowserTesting</a> provides live interactive browser testing with remote VNC sessions. It also generates automated screenshots across multiple browsers for more basic testing. There are more than 100 browser and operating system combinations, including many mobile platforms.

Monthly subscriptions range from $29.95 to $199.95, depending on the number of users and the minutes of testing (minutes can roll over to the next month, but they’re not unlimited). A one-week free trial is available for all plans.

<figure><a href="https://crossbrowsertesting.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed606a78-9d10-46ff-b126-e04a625ea202/crossbrowsertesting.jpg" alt="" /></a></figure>

## Testing Services Compared

The chart below shows the basic features offered by these cross-browser testing services and applications, making it quick and easy to compare.
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr style="background: #e1e1e1">
<th>Tool</th>
<th style="text-align: left;width: 135px">Number of browser versions supported</th>
<th>IE?</th>
<th>Interactive testing?</th>
<th>Side-by-side testing?</th>
<th>Pricing</th>
</tr>
</thead>
<tbody>
<tr>
<td>Adobe BrowserLab</td>
<td>13</td>
<td>IE6+</td>
<td>No</td>
<td>Yes</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://browsershots.org/">Browsershots</a></td>
<td>60+</td>
<td>IE6+</td>
<td>No</td>
<td>No</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://expression.microsoft.com/en-us/dd565874.aspx">SuperPreview</a></td>
<td>Varies</td>
<td>IE6+</td>
<td>Yes</td>
<td>Yes</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://www.lunascape.tv/">Lunascape</a></td>
<td>3</td>
<td>IE6+</td>
<td>Yes</td>
<td>Yes</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://www.my-debugbar.com/wiki/IETester/HomePage">IETester</a></td>
<td>6 versions of IE</td>
<td>IE5.5+</td>
<td>Yes</td>
<td>Yes</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://www.ipinfo.info/netrenderer/">IE NetRenderer</a></td>
<td>5 versions of IE</td>
<td>IE5.5+</td>
<td>No</td>
<td>No</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://spoon.net/browsers/">Spoon</a></td>
<td>16+</td>
<td>no IE</td>
<td>Yes</td>
<td>No</td>
<td>Free</td>
</tr>
<tr>
<td><a href="https://saucelabs.com/">Sauce Labs</a></td>
<td>40+</td>
<td>IE6+</td>
<td>Yes</td>
<td>No</td>
<td>Free — $499 per month</td>
</tr>
<tr>
<td><a href="https://www.browsera.com/">Browsera</a></td>
<td>9</td>
<td>IE6+</td>
<td>No</td>
<td>Yes</td>
<td>Free – $99/month</td>
</tr>
<tr>
<td><a href="https://browserling.com/">Browserling</a></td>
<td>9</td>
<td>IE5.5+</td>
<td>No</td>
<td>No</td>
<td>Free – $20/month</td>
</tr>
<tr>
<td>Mogotest</td>
<td>7+</td>
<td>IE6+</td>
<td>No</td>
<td>Yes</td>
<td>$15 – $4,499/month</td>
</tr>
<tr>
<td>Cloud Testing</td>
<td>4+</td>
<td>IE6+</td>
<td>Yes</td>
<td>Yes</td>
<td>Not specified</td>
</tr>
<tr>
<td>BrowserCam</td>
<td>90+</td>
<td>IE5.2+</td>
<td>Yes</td>
<td>Yes</td>
<td>$19.95 – $89.95/month</td>
</tr>
<tr>
<td><a href="https://www.multibrowserviewer.com/">Multi-Browser Viewer</a></td>
<td>80+</td>
<td>IE6+</td>
<td>For some browsers</td>
<td>Yes</td>
<td>$139.95</td>
</tr>
<tr>
<td><a href="https://crossbrowsertesting.com/">CrossBrowserTesting</a></td>
<td>100+</td>
<td>IE6+</td>
<td>Yes</td>
<td>Yes</td>
<td>$29.95 – $199.95/month</td>
</tr>
</tbody>
</table>

### Conclusion

Regardless of the tool you choose, testing early and often during the Web development process can save you from a lot of headaches later. Find a tool that fits your workflow (so that you’ll actually want to use it and it won’t be a hassle), and test whenever you make major changes to a design.

### What tools do you use for cross-browser testing?

How has your experience been with cross-browser testing tools and services? Which ones do you use? How do you integrate cross-browser testing in your professional workflow? Let us know in the comments!

## Related Posts

You might be interested in the following related articles:

*   [Review of Text Batch Processing Tools](https://www.smashingmagazine.com/2009/04/10/25-text-batch-processing-tools-reviewed/)
*   [Useful Resources, Tools and Services for Web Designers](https://www.smashingmagazine.com/2011/06/17/useful-resources-tools-and-services-for-web-designers/)
*   [Time-Saving and Educational Resources for Web Designers](https://www.smashingmagazine.com/2011/01/18/time-saving-and-educational-resources-for-web-designers/)

{{% ad-panel-leaderboard %}}

### Further Reading

*   [High-Impact, Minimal-Effort Cross-Browser Testing](https://www.smashingmagazine.com/2016/02/high-impact-minimal-effort-cross-browser-testing/)
*   [How To Create Your Own Front-End Website Testing Plan](https://www.smashingmagazine.com/2014/11/how-to-create-your-own-front-end-website-testing-plan/)
*   [Reliable Cross-Browser Testing, Part 1: Internet Explorer](https://www.smashingmagazine.com/2011/09/reliable-cross-browser-testing-part-1-internet-explorer/)
*   [Impressive Web Browser Alternatives](https://www.smashingmagazine.com/2015/09/chrome-firefox-safari-opera-edge-impressive-web-browser-alternatives/)

{{< signature "al, mrn" >}}
