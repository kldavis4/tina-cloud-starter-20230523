---
title: Do Mobile And Desktop Interfaces Belong Together?
slug: do-mobile-desktop-interfaces-belong-together
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/303b8607-b7a5-49ee-8698-005599db60f2/crispinporter-overloading-information.jpg
date: 2012-07-19T11:22:34.000Z
author: mike-sierra
description: >-
  The term “responsive design” has gathered a lot of well-deserved buzz among
  Web designers. As you probably know, it refers to an easy way to dynamically
  customize interfaces for different devices and to serve them all from the same
  website, with no need for a separate mobile domain.
categories:
  - Mobile
  - Responsive Design
  - Hybrid
---
The term “responsive design” has gathered a lot of well-deserved buzz among Web designers. As you probably know, it refers to an easy way to dynamically customize interfaces for different devices and to serve them all from the same website, with no need for a separate mobile domain.

It solves one major problem, and very elegantly: how to adapt visual interfaces for mobile, tablet and desktop browsers. But when unifying a website, you have to solve problems other than how it will appear in different browsers, which could make the task much more difficult than you first realize. A solid design has to account for differences in interaction when using mouse pointers and when using touch gestures, as well as the bandwidth constraints on mobile users.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Improve Mobile Support With Server-Side Responsive Design</span>](https://www.smashingmagazine.com/2013/04/improve-mobile-support-with-server-side-enhanced-responsive-design/)
*   [Approaches For Multiplatform UI Design Adaptation: A Case Study](https://www.smashingmagazine.com/2015/09/approaches-for-multiplatform-ui-design-adaptation/)
*   [How To Sketch For Better Mobile Experiences](https://www.smashingmagazine.com/2013/06/sketching-for-better-mobile-experiences/)
*   [Authentic Design](https://www.smashingmagazine.com/2013/07/authentic-design/)

You might also have to restructure content according to how much information it makes sense to present on each screen. And the new breed of mobile Web apps that leverage HTML5’s offline capabilities might have to be built much differently than conventional desktop websites. Hopefully, after considering these problems, you should be able to implement a responsive website that is suitable for all devices; but you’ll need a fallback plan if that’s not possible.

{{% feature-panel %}}

This article looks at how a typical responsive website is targeted to mobile handsets and tablets, contrasting it with its desktop-facing sister website. It considers how such a website might also be deployed as a cached HTML5 Web app, and why you might want to do that instead. For various reasons, discussed here, you might decide to target your responsive design more narrowly as a hybrid for smartphones and tablets, keeping it separate from the desktop interface. For those of you who opt for this route, the remainder of the article will explore ways to better integrate the different websites, or Web apps, and how to make it easier for users to learn about the appropriate interface, get to it and stay there.</p>

## A Responsive Design For Mobile And Tablet

The BBC recently started rolling out a <a href="https://m.bbc.co.uk/news/">new version of its mobile news website</a>, which serves as a perfect example of how to adapt an interface very effectively just by detecting the screen’s width. Below is the same page viewed with different layouts targeted for the iPhone and iPad. You can see the interface transform dynamically by viewing it in a desktop browser and resizing the window:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca5d4457-f067-430f-aae1-a471b911a5d1/bbc1.png"><img loading="lazy" decoding="async"  class="alignnone size-medium wp-image-130355" style="margin-right: 1em;border: thin solid #777" title="bbc1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26589dfb-251d-47b2-88d4-97f4bb432052/bbc1-234x300.png" alt="BBC mobile UI" width="234" height="300" /></a><br>
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a200a3-4b21-4723-bb33-dded311bf0ba/bbc2.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="130356" style="border: thin solid #777" title="bbc2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a200a3-4b21-4723-bb33-dded311bf0ba/bbc2.png" alt="BBC tablet UI" width="510" height="344" /></a>

The single-column mobile interface transforms into a multi-column interface more suitable for tablets, with a richer set of navigation options appearing at the top of the screen. While the multi-column interface is a bit more complex, it’s still cleaner and less cluttered than most desktop-facing websites. BBC News, along with similar websites such as the <a href="https://bostonglobe.com/">Boston Globe</a> and Smashing Magazine, exemplifies the trend towards “mobile-first” design; i.e. starting with a clean mobile design and progressing upwards as needed, rather than trying to jam a full desktop-style interface into a single column. Most responsive websites rely on CSS media queries that reference screen widths, but they can also respond to specific browser features and exhibit fallback behavior that “progressively enhances” an interface.

These techniques are so easy to apply that you might wonder why not all websites are built like this. It could simply be due to inertia, in which case developers need to do a better job of spreading the word. But the next section explores what may be deeper reasons.</p>

## Why Desktop Is Different

The adaptive interfaces referred to above are a healthy development, one that could lead to uncluttered desktop interfaces in the future. Still, there may be times when mobile or tablet interfaces should feature a different set of content than for desktop browsers. For one thing, media queries use up precious bandwidth. The BBC’s <a href="https://www.bbc.co.uk/news/">desktop design</a> features a much richer set of content around the margins, such as ads and sidebars, which you’d typically exclude from the mobile interface.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ab350a-9fa2-4389-b1df-fbdc3dadc696/bbc0.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="130364" style="border: thin solid #777" title="bbc0" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ab350a-9fa2-4389-b1df-fbdc3dadc696/bbc0.png" alt="BBC desktop UI" width="572" height="425" /></a>

Unless you perform feats of conditional loading for various regions on the page, any content that you hide using CSS’s <code>display: none</code> declaration is still served to the browser, perhaps at considerable cost over a mobile network.

A desktop page also features a much richer set of navigation options, especially up in the banner. On many desktop websites, users have drop-down menus to access nested categories in a single move. But in mobile interfaces, each set of navigation options is usually presented one at a time; for example, with iPhone-style sliding drill-down menu panels. You might also have to fix navigation elements to the screen, so that users don’t have to scroll to the top of the page to access them. Imagining how you would consolidate such requirements within a single hybrid website might be fun, but it can certainly get complex. Desktop websites can also rely more heavily on navigation driven by search, which is more difficult to manage with virtual keyboards.

Below is the sort of adapted mobile interface you might encounter in the wild. Those tiny navigation tabs might be fine for a desktop interface, but they are uncomfortably small for a touch interface and should serve merely as visual cues. Increasing their size would only crowd out other screen elements and limit the total number of tabs you could use. In this situation, swiping left and right to navigate the panels would be natural for mobile users. You could certainly add support for touch gestures to a mouse-driven website, but that’s another input mode to account for and to integrate in the interface.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/772aa7c0-103c-484a-a886-1c063cde6d80/algae-red.png"><img loading="lazy" decoding="async"  class="alignnone size-medium wp-image-130377" style="margin-right: 1em;border: thin solid #777" title="algae_red" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7575037c-2865-4968-8286-9de736182a53/algae-red-198x300.png" alt="" width="198" height="300" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7138980-405b-46e7-9756-25669d461008/algae-brown.png"><img loading="lazy" decoding="async"  class="alignnone size-medium wp-image-130375" style="margin-right: 1em;border: thin solid #777" title="algae_brown" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d4bfb6-cabc-4922-8932-3de305edfa42/algae-brown-196x300.png" alt="" width="196" height="300" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd49e609-3b38-4b22-953a-7f56149d809c/algae-green.png"><img loading="lazy" decoding="async"  class="alignnone size-medium wp-image-130376" style="border: thin solid #777" title="algae_green" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8474066-89a8-4cca-9299-149364a8bfac/algae-green-195x300.png" alt="" width="195" height="300" /></a>

Most of all, mobile users are usually in a different frame of mind than desktop users. We can't really make any precise assumptions about the context of the device usage, but compared to desktop usage they quite often will be standing up and walking around or driving, and sometimes just scanning their handset or tablet. This might call for less detailed content than what you would use for more focused desktop users. Instead of presenting all of the day’s news items, for example, tracking unread items or the most popular trending items might be more important. Users might also want different content depending on their location. Even viewing a browser in full sunlight calls for a higher-contrast design, with fewer details that would make you stop and squint. Other times, such as when waiting for a connecting flight, mobile users will have more time on their hands and attention to spare. Overall, mobile contexts are far more varied than desktop and laptop contexts.

Even though mobile handsets and tablets are much more varied in size, their similar usage patterns and reliance on touch gestures could make deploying a responsive interface for those devices easier than deploying one that also targets desktop browsers.</p>

## Mobile Web Apps Vs. Mobile Websites

Using media queries to adapt an interface is a powerful technique, but we must recognize how superficial it is. It does little to address the particular needs of cached mobile Web apps, which could be built much differently than conventional websites. Consider how the BBC’s website is deployed. Users navigate links to load separate pages, and the overall set of available URLs shifts as the news changes.

A Web app might rely on the HTML5 application cache. A small set of HTML and other files would load once and install in a browser cache, and then populate data dynamically using AJAX. Assuming that you also cache the data, users would be able to open the application and retrieve the news in the absence of a network connection (a common “reading on the subway” scenario), with data updating once the browser detects that it is online again. It’s a much looser system that adapts to the more wide-ranging needs of mobile users.

A cache is implemented as a manifest file that’s specified at the top of the HTML file and evaluated before the rest of the HTML loads:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html manifest="appcache.php"&gt;
&lt;!-- the rest loads conditionally --&gt;</code></pre>

The manifest lists all of the component files that need to be cached. The example above uses PHP to specify the correct MIME type within the markup, rather than as a server configuration option:

<pre><code class="language-markup tmp-html">&lt;?php header('Content-type: text/cache-manifest'); ?&gt;
CACHE MANIFEST
# version 1.0; change version# or other content to update app
CACHE:
index.html
css/styles.css
js/app.js
img/home.png
img/about.png
img/back.png</code></pre>

The first time you land on the page, all of these files will be cached. After that, they are reloaded from the browser’s cache without ever touching your server. Only by changing the content of the manifest will the files be refreshed from your server. The JavaScript might communicate separately via AJAX, but typically with some sort of fallback for offline use.

This way of structuring a website as a fixed-footprint package of files doesn’t adapt well to more conventional server-driven websites. There would be no point in caching an application whose set of component pages changes frequently, as the BBC’s does with each batch of news.

Web apps are becoming popular because they offer developers a cross-device alternative to native application platforms. Most features of native apps can be implemented as browser-based apps, executing on the client as if the app had been formally “installed” from an app store. Web apps can be accessed on most platforms using icons on the home screen, and they might be set to hide browser controls in order to take total control of the interface. Once a Web app is saved to the home screen, there may be nothing to indicate that it is being implemented as a Web page.

The following lines, placed in the page’s <code>head</code> region, target different devices with different-sized home screen icons, with the <code>precomposed</code> fallback that is supported by some Android browsers:

<pre><code class="language-markup tmp-html">&lt;link rel="apple-touch-icon" href="img/app_iphone.png" sizes="114x114" /&gt;
&lt;link rel="apple-touch-icon" href="img/app_ipad.png" sizes="72x72" /&gt;
&lt;link rel="apple-touch-icon" href="img/app_nokiaN9.png" sizes="80x80" /&gt;
&lt;link rel="apple-touch-icon-precomposed" href="img/apple-touch-icon-precomposed.png"&gt;</code></pre>

The following line enables full-screen Web apps on iPhones. Thus, when the user selects the app from the home screen icon, nothing on the screen would tell them that the app is running in a browser:

<pre><code class="language-markup tmp-html">&lt;meta name="apple-mobile-web-app-capable" content="yes" /&gt;</code></pre>

These three features — the application cache, home screen icons and full-screen mode — are what most strongly distinguish mobile Web apps from ordinary Web pages. To get into more details about the Application Cache, make sure to read Jake Archibald's article <a href="https://www.alistapart.com/articles/application-cache-is-a-douchebag/">Application Cache is a Douchebag</a> on <em>A List Apart</em>.

## Traffic Control

For all of the reasons discussed above, websites that were created specifically for certain device classes might be easier to control and optimize. Either forking or consolidating a website has its pros and cons. Having a single access point means that the same URL will serve the content to all devices without the risk of losing context, but with the extra cost of designing and maintaining a structure that fits all needs. Developing separate websites tailored to different device classes means you can focus on highly optimized content, but at the cost of maintaining more than one design. With the latter approach, you might also have to consider ways to maintain context when the user jumps from one interface to the other.

On many websites, if you land on a page with the "wrong" browser, nothing happens. Many websites seem to assume that users are aware of the availability of a separate mobile website and don’t account for the likelihood that they’ve landed on a random desktop-facing page via a Facebook or Twitter link. At the very least, each website should link to its various interfaces, as done at the bottom of many BBC pages:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb6c6f6a-618b-4485-a163-36988382d457/bbc-2desk.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="130382" title="bbc_2desk" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb6c6f6a-618b-4485-a163-36988382d457/bbc-2desk.png" alt="" width="375" height="166" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51cb8572-10c2-4e3d-830f-0fb4ec28d477/bbc-2mob.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="130383" title="bbc_2mob" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51cb8572-10c2-4e3d-830f-0fb4ec28d477/bbc-2mob.png" alt="" width="477" height="97" /></a>

Alternatively, consider placing such controls prominently at the top of the page, otherwise the availability of an alternative interface might not be obvious. Pages designed for the desktop usually don’t specify a viewport, so they would load with tiny content on mobile devices. The user would have to zoom in to view the page, then scroll to somewhere around the bottom of the page to find the link, if they even thought to look there. Assuming that visitors to your website have just arrived from the planet Neptune is not a bad idea.

The BBC uses another approach, simply redirecting many smartphone browsers from the desktop website to the mobile website. If you decide to navigate back to the desktop website using the link at the bottom of the page, the URL will be appended with a <code>?mobile</code>, which prevents another redirect from firing. That works during each browsing session but is not saved as a preference.

You could instead prompt users to go to the other website, but be sure not to do so every time they visit, or else it will get annoying. The simple example below is relevant if you host different websites on the same domain. It sends a prompt and uses jQuery to cache the answer as a domain-wide cookie. The <code>matchMedia</code> API offers the ability to test the same set of CSS media queries that you use to assign the layout, but instead calling them from within JavaScript:

<pre><code class="language-javascript">function checkRedirect() {
    // media query
    var query = 'only screen and (max-device-width: 800px)';
    // from a page on www.foo.com
    var mobileUrl = 'https://m.foo.com/';
    // does the user already prefer desktop UI?
    if ($.cookie('preferMobile') == 'n') return(false);
    // is app running on a mobile/tablet browser?
    if (!!window.matchMedia &amp;&amp; window.matchMedia(query).matches) {
        // has user already stated preference for mobile UI?
        if ($.cookie('preferMobile') == 'y') window.location.href = mobileUrl;
        // get user's preference
        if (confirm('Would you like to try the web app instead?')) {
            $.cookie('preferMobile', 'y', { path: 'foo.com' });
            window.location.href = mobileUrl;
        } else {
            $.cookie('preferMobile', 'n', { path: 'foo.com' });
        }
    }
}</code></pre>

The destination page would have to feature a control to reset the preference. Otherwise, users who change their mind would have no easy way to view the desktop interface without once again being redirected to the mobile interface. If you used the browser’s <code>localStorage</code> feature to cache the preference indefinitely, then its scope would be limited to each host name, rather than available across the entire <code>foo.com</code> domain. So, cookies are still good for something.

Once you’ve refined the basic redirect mechanism, devote some thought to how to retain more detailed context. Otherwise, users might become disoriented when they navigate back to the information they originally expected. If the URL structure for each website is the same, then a contextual redirect is as simple as modifying the host name:

<pre><code class="language-markup tmp-html">www.foo.com/news/local/041912/police-log/
m.foo.com/news/local/041912/police-log/</code></pre>

If the mobile interface is implemented as a cached Web app, then the information would be passed more like this:

<pre><code class="language-markup tmp-html">www.foo.com/news/local/041912/police-log/
m.foo.com?category=news&amp;subcategory=local&amp;date=041912&amp;item=police-log</code></pre>

The Web app would then dynamically respond to the query portion of the URL.</p>

## Promoting Your Web App

Many websites present splash screens that alert users to a native iPhone or Android app, but there’s no simple way on a Web page to check whether such an app is already installed. There’s also no way to open the app so that the user can view the content they are looking for.

Because they’re basically Web pages, Web apps are easier to integrate with your other Web pages. Matteo Spinelli has a useful “<a href="https://cubiq.org/add-to-home-screen">Add to Home Screen</a>” script that tells users how to install the mobile page as a Web app. So far, there is no single Web application-store portal to help users find Web apps to install, so the script might be the best way to raise awareness for now. The script points to the button on each handset that the user needs to press in order to save the Web app. These screenshots show how it looks at the bottom of the iPhone and at the top of the Nokia N9:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fde049d-411a-48f1-b579-28d4b4e72127/add2home-ios.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="130395" style="margin-right: 1em" title="add2home_ios" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fde049d-411a-48f1-b579-28d4b4e72127/add2home-ios.png" alt="" width="320" height="205" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51c22516-9beb-47c6-8c25-b45d703d67b6/add2home-n9.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="130396" title="add2home_n9" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51c22516-9beb-47c6-8c25-b45d703d67b6/add2home-n9.png" alt="" width="317" height="205" /></a><br>
<em>(Source: <a href="https://letmespellitoutforyou.com/pub/add2home.htm">Let Me Spell It Out for You</a>)</em>

This useful feature can be set to prompt users to install the page only after they have landed on the website more than once.

There’s not yet any reliable way to track how many users follow through and save the page as a Web app. But you could enhance your website with an interesting workaround for the iPhone. If a page is enabled for full-screen viewing and the user saves it as a Web app and then loads it from the home screen, the browser controls will disappear from the interface. At this point, the <code>standalone</code> property will indicate that the user is accessing the full-screen app from the home screen, which you can interpret as a preference:

<pre><code class="language-javascript">if (window.navigator.standalone) $.cookie('preferMobile', 'y', { path: 'foo.com' });</code></pre>

However, the <code>standalone</code> property is contextual. It returns <code>true</code> when the user loads the page directly from the home screen, in which case the page will have no browser controls. But if the user navigates to the page conventionally within the browser application (such as via a redirect from a desktop-facing page), then the browser controls will still appear and <code>standalone</code> will return <code>false</code>. So, it’s a good way to track interest, although not to track the lack of interest among users who later decide to remove the Web app.

The W3C is formulating a more comprehensive full-screen specification that might fix such problems in browsers. Until then, apply a flexible screen layout to account for visitors who land on the page with or without browser controls.</p>

## Conclusion

This article asks whether your desktop and mobile interfaces really belong together and whether they should work as a single client-adapted website. This question has no single answer, but asking it is important. We’ve explored some of the reasons why the answer might be no, particularly if your needs are complex.

But your goal, as a developer with a vision of a unified design and an appreciation of technical elegance, should be to be able to answer yes, having dealt with those issues. Just don’t focus too much on visual design to the neglect of variations in interaction design, information design and underlying deployment. Be prepared if the answer is no. If you find you have to split off your desktop website, find ways to make the overall experience as graceful as possible for users, regardless of whether they land on one of your pages via an external link or via a home screen icon. That’s the whole point of responsive design.

{{< signature "al" >}}

