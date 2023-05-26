---
title: 'How To Poison The Mobile User'
slug: how-to-poison-the-mobile-user
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f23bfc15-eff7-4b2c-9764-d4582e0c986b/image-3-opt.png
date: 2016-10-24T19:32:47.000Z
author: martinmichalek
summary: >-
  Is your website on mobile devices friends with your users? In this article, Martin Michálek goes through them and suggests best practices to optimize the user experience on mobile devices.
description: >-
  Is your website on mobile devices friends with your users? In this article, Martin Michálek goes through them and suggests best practices to optimize the user experience on mobile devices.
categories:
  - Mobile
  - Performance
  - Optimization
  - User Experience
---

One of the most popular children’s television heroes here in the Czech Republic is <a href="https://en.wikipedia.org/wiki/Mole_(Zden%C4%9Bk_Miler_character)">The Little Mole</a>, an innocent, speechless and cheerful creature who helps other animals in the forest.

TV heroes often fight against people who destroy their natural environment. When watching The Little Mole with my kids, I sometimes picture him as a mobile website user. Do you want to know why?

We, as web designers, often treat our users the same way the “bad guys” treat The Little Mole, especially on mobile websites.

One episode of the series is particularly dramatic. An old man tries to get rid of the mole in the garden by any means and eventually tries to poison him. Web designers do the same thing when they make it difficult to use the mobile version of a website and try to “poison” the user, eventually making them leave the website.

So let’s be a little sarcastic today and try to poison the mobile user. How does that sound? Just follow my instructions.

Let’s make a slow website, disable zooming, hide the navigation and fill up the page with fixed-positioned elements. I’ll bet the poor mobile user won’t be able to survive this.

{{% feature-panel %}}

## 1. Make The Website Load Slowly

<em>Making the website load slowly is the best weapon against the mobile user. Can the visitor go to and return from the post office before the website has finished loading? Then you’re doing a great job! You are poisoning the mobile user effectively.</em>

Now, let’s be serious. The transmission speed of mobile networks is slow, and even though speeds are increasing to 3G and 4G, the networks <a href="https://twitter.com/firt/status/757587453234454528">aren’t everywhere</a>, and they just can’t compete with wired ones.

Various test and surveys show that the <a href="https://wpostats.com/">website speed has a significant impact</a> on conversions and a website’s overall effectiveness. The user shouldn’t have to wait more than a couple of seconds for a website to render, even when using an EDGE connection.

Moreover, don’t forget that website speed is one of the criteria that Google considers for search results and AdWords campaigns. Therefore, it affects not only conversions but also whether users will land on your website at all.

The solution is quite simple: Think about speed when you are developing a website’s concept. Start with a performance budget.

Optimizing speed is not that complicated. Let me share with you some best practices from Google:

*   **Minimize data transmission.**
    *   [Optimize images.](https://developers.google.com/speed/docs/insights/OptimizeImages)
    *   [Minify CSS, JavaScript and HTML](https://developers.google.com/speed/docs/insights/MinifyResources).
*   **Don’t block rendering.**
    *   [Optimize CSS delivery.](https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery)
    *   [Remove render-blocking JavaScript.](https://developers.google.com/speed/docs/insights/BlockingJS)
    *   [Prioritize visible content.](https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent)
*   **Optimize the back end.**
    *   [Improve the server’s response time.](https://developers.google.com/speed/docs/insights/Server)
    *   [Enable compression.](https://developers.google.com/speed/docs/insights/EnableCompression)
    *   [Leverage browser caching.](https://developers.google.com/speed/docs/insights/LeverageBrowserCaching)
    *   [Avoid unnecessary redirects.](https://developers.google.com/speed/docs/insights/AvoidRedirects)

Don’t have time to read this now? I completely understand. Save the text for later. Fortunately, tools are available to tell you what is wrong with your website. First, test your website with <a href="https://developers.google.com/speed/pagespeed/insights/">PageSpeed Insights</a>, and then continue to <a href="https://www.webpagetest.org/">WebPagetest</a>.

## 2. Design Your Carousel Poorly

<em>The user will never come back.</em>

It is true that various studies on carousels do not explicitly say they are inappropriate. However, carousels are complicated both in implementation and for the user experience. So, using them is risky.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbcd881-88af-4c53-8823-0e2cf594781f/comparison-nike-bestbuy.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbcd881-88af-4c53-8823-0e2cf594781f/comparison-nike-bestbuy.png" alt="image alt text" width="500" height="281" /></a><figcaption>Nike’s carousel (left) does not make it clear that the content continues to the right. Best Buy’s (right) does it better: Subsequent items are visible, and therefore it is evident you can scroll to the right. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbcd881-88af-4c53-8823-0e2cf594781f/comparison-nike-bestbuy.png">View large version</a>)</figcaption></figure>

It is highly probable that, by using carousels, you will be hiding some content, instead of promoting it. According to some surveys, the vast majority of users <a href="https://erikrunyon.com/2013/07/carousel-interaction-stats/">see only the first image</a>, and banner-based carousels are usually just ignored because of “banner blindness”.

If you plan to <a href="https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/">use a mobile carousel</a>, make sure it meets the following criteria:

*   **Don’t use the carousel just as eye candy or to hide unnecessary content.**  
Carousels are great at advertising secondary content that is related to the main content.
*   **Use the first slide to announce the other slides.**  
The main purpose of that first slide is entice the user to view the second and third slides.
*   **Make the navigation usable on small phones.**  
Those small dots used as navigation on the desktop do not count as “usable” on mobile phones!
*   **Make sure custom gestures don’t conflict with default browser gestures.**  
Are you using the swipe gesture? Make sure it does not conflict with a built-in browser gesture.
*   **Don’t slow down the website.**  
This has to do primarily with data demand and implementation of the carousel.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/275c7da6-dc05-4017-bd44-2d29b7d1be4a/image-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8289263-6a67-4a57-a65d-07bd2815f838/image-1-500-opt.png" alt="image alt text" width="500" height="281" /></a><figcaption>Newegg’s carousel (left) represents a conventional approach. B&amp;H’s (right) is a good example, saving vertical space and enticing the user to browse additional slides by showing the next one. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/275c7da6-dc05-4017-bd44-2d29b7d1be4a/image-1-opt.png">View large version</a>)</figcaption></figure>

## 3. Hide The Menu Under A Hamburger Icon

<em>Make the navigation easily accessible? Come on, get serious! You could end up with thousands of users.</em>

When you hide the menu on a website, people will stop using it. In a recently published study, <a href="https://www.nngroup.com/articles/hamburger-menus/">Nielsen Norman Group found</a> that hidden navigation on mobile has a negative effect on content discoverability, task completion and time spent on task.

If there is something important in the navigation, and you can display it, do it. If you can’t show the whole menu, then simplify it, or at least show the important parts of it. For this reason, I tend to recommend the <a href="https://css-tricks.com/diy-priority-plus-nav/">“priority plus” navigation pattern</a>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ccbf545-244b-479f-bd59-f5c9a30892a6/image-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94d75db9-c2e3-4bc9-ba11-4dedab215cd6/image-2-500-opt.png" alt="image alt text" width="500" height="269" /></a><figcaption>If the navigation also carries content, always display at least a few items. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ccbf545-244b-479f-bd59-f5c9a30892a6/image-2-opt.png">View large version</a>)</figcaption></figure>

What if you can’t show the important items? OK, then, hide it under a hamburger icon, <a href="https://exisweb.net/mobile-menu-abtest">label it “Menu”</a>, and make sure users can use the website without the menu.

{{% ad-panel-leaderboard %}}

## 4. Always Rely On The Swipe Gesture

<em>Swipe away all users with the swipe gesture.</em>

I regard less common gestures to be risky for a mobile UI, for <a href="https://medium.com/@kollinz/misused-mobile-ux-patterns-84d2b6930570#.1qxxllypd">two reasons</a>:

*   **Custom gestures might conflict with the browser’s default gestures.**  
If your carousel supports swipe gestures, for example, the user might accidentally perform an “edge swipe” (a gesture very similar to a regular swipe), which some mobile browsers interpret as a command to navigate the browsing history.
*   **Less common gestures are unknown to many users.**  
Therefore, you’ll have to teach the user. This makes sense if we are talking about daily-used apps, but not about websites.

Using a carousel does not have to be such a problem. However, I have seen news websites support swipe gesture for navigation between articles. For the user, this is unusual and confusing.

The swipe gesture is not the only problem here. Tapping the bottom part of the Safari browser on iOS will reveal a hidden menu. Therefore, if you stick navigation elements at the bottom, the user might be forced to <a href="https://www.eventbrite.com/engineering/mobile-safari-why/">tap twice</a>.

Before using any uncommon gesture, test that it doesn’t conflict with any browser’s built-in gestures.

## 5. Make All Tap Targets Nice And Small

<em>One millimeter is good enough.</em>

OK, let’s be serious. Are your tap targets big enough that a basketball player could easily hit them with their thumb?

In his book <a href="https://abookapart.com/products/designing-for-touch"><em>Designing For Touch</em></a>, Josh Clark refers to a <a href="https://www.elearningguild.com/insights/index.cfm?id=174&amp;action=viewonly">study by Steven Hoober and Patti Shank</a>. The researchers found that, if placed at the center of the mobile screen, a tap target can be as small as 7 square millimeters; however, if placed at the top or bottom, it should be at least 11 square millimeters.

However, millimeters are rather impractical for web use. We use pixels, right? So, how do we deal with the variety of DPIs on mobile devices? Probably to most readers’ surprise, Josh Clark says in his book:
<blockquote>Nearly all mobile browsers now report a device-width that sizes virtual pixel at roughly the same pixel density: 160 DPI is the de facto standard for touchscreen web pixels.</blockquote>

Again, all you need to do is set the <code>viewport</code> meta tag correctly:

<pre><code class="language-html">&lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;</code></pre>

There is one more step: Use em or rem units that best suit the responsive design. The default font size for most browsers is 16 pixels, so we can use the following conversion:

<pre><code class="language-css">/* 7mm = 44px = 2.75rem */
.touch { height: 2.75rem; }
/* 11mm = 69px = 4.3125rem */
.touch-big { height: 4.3125rem; }
</code></pre>

That’s it, folks. Don’t forget to provide a <a href="https://github.com/robwierzbowski/grunt-pixrem">fallback for old browsers</a>. And if you are into details, I suggest you buy <a href="https://abookapart.com/products/designing-for-touch">Josh’s book</a>.

## 6. Make It Responsive, But Only For Certain Resolutions

<em>Force users to leave your website. Make them go buy a phone that has the “correct” resolution.</em>

We are faced with an <a href="https://screensiz.es/phone">enormous variety of screen resolutions</a> on mobile devices. Before, only the Android platform was affected, but now <a href="https://twitter.com/LiquidLightUK/status/644827716739592192">Apple devices are</a>, too.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f23bfc15-eff7-4b2c-9764-d4582e0c986b/image-3-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b867cc-5b2b-455c-8671-88c88eedf7d4/image-3-500-opt.png" alt="image alt text" width="500" height="281" /></a><figcaption>Even if your website is not “meant” for mobile devices, there is no reason not to let mobile users get a sneak peek. Some websites don’t adapt to particular viewport sizes. What a shame! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f23bfc15-eff7-4b2c-9764-d4582e0c986b/image-3-opt.png">View large version</a>)</figcaption></figure>

We can’t assume that smartphone screens are around 320 pixels, that tablets are around 768 pixels and that desktops are over 1024 pixels. A page should seamlessly adjust to screens that are 768 pixels and lower.

So, what resolutions should we take into account? All of them, my friend.

In my development career, I have been testing responsive websites from 240 to approximately 2600 pixels wide. I admit that making all sizes look perfect is sometimes not humanly possible, but the bottom line is that the layout should not fall apart &mdash; assuming your intention is not to scare away mobile users.

Like most of you, I simply expand the browser window (or use the developer tools’ responsive mode) from the smallest size to full width. It is a kind of “Hay! mode”, found in the <a href="https://bradfrost.com/demo/ish/">Brad Frost’s testing tool</a>.

### Also, Don’t Change the Design When the Phone Switches from Portrait to Landscape Mode

I think that users expect the same, or at least a very similar, look when browsing a website, regardless of how they hold their phone. I remember one of my lecture participants telling me a story. When his company redesigned a website, a lot of people started calling the support desk. They were all complaining about a particular error: The website menu was disappearing. After a while, they discovered that these were tablet users. When they viewed the website in landscape mode, the menu was there. If the tablet was rotated into portrait mode, the menu was hidden under a “hamburger” icon.

## 7. Don’t Make Phone Numbers Tappable

<em>Make the user angry. Prevent them from calling phone numbers directly from the website.</em>

Contacting you can be a piece of cake for mobile users. Just set <a href="https://www.mobilexweb.com/blog/click-to-call-links-mobile-browsers">phone numbers as links that open a phone call</a>. It is similar to activating FaceTime, SMS and Skype on Apple devices.

We have a problem, though. People usually can’t make calls from a <a href="https://css-tricks.com/the-current-state-of-telephone-links/#article-header-id-1">desktop browser</a>. However, instead of ignoring phone links, desktop browsers open an incomprehensible dialog box that invites the user to select an app to make the call. In most cases, no such app is available.

Dear friend, we don’t want to poison desktop users either. So, on this rare occasion, I recommend using device detection and inserting an active link for mobile users only.

In the HTML, the phone number would be inactive. We’ll just wrap it in a <code>span</code> tag and apply Javascript later:

<pre><code class="language-markup">Phone: &lt;span class="phone-number"&gt;123456789&lt;/span&gt;
</code></pre>

Using jQuery and the <a href="https://github.com/kaimallea/isMobile">isMobile</a> detection library, we’ll replace the element with a <code>phone-number</code> class and a link:

<pre><code class="language-javascript">if(isMobile.phone) {
  $('.phone-number').each(function() {
    $(this).replaceWith(
      $('&lt;a href="tel:' + this.innerHTML + '"&gt;' + this.innerHTML + '&lt;/a&gt;')
    );
  });
}
</code></pre>

On smartphones, the markup looks like this:

<pre><code class="language-markup">Phone: &lt;a href="tel:123456789" class="phone-number"&gt;123456789&lt;/a&gt;
</code></pre>

## 8. Disable Zooming

<em>Disable the zoom if you really want to stick it to users. It’s inhumane &mdash; and very effective.</em>

But seriously, by disabling zooming, you are not only making life a little more complicated for users with poor eyesight. <a href="https://adrianroselli.com/2015/10/dont-disable-zoom.html">Even users with good eyesight</a> zoom on mobile devices, for various reasons:

*   to see an image up close,
*   to more easily select text,
*   to magnify content with low contrast.

Zooming is actually disabled on a sizeable proportion of mobile websites. Consider the importance of viewing image details in an online store. Zooming is disabled on <a href="https://baymard.com/blog/mobile-image-gestures">40% of e-commerce websites</a> tested by the Baymard Institute. Mind-boggling, isn’t it?

Just as desktop users can’t do without the back button and scrolling, so too do mobile users need zooming.

The WCAG’s accessibility guidelines tell us that users must be able to increase text size by <a href="https://www.w3.org/TR/2008/REC-WCAG20-20081211/#visual-audio-contrast-scale">200%.</a>

Sure, there are cases when you have to disable zooming &mdash; for fixed elements, for example. But zooming is sometimes disabled by accident, such as by insertion of the wrong meta <code>viewport</code> tag. The one below is the only correct one, whereas incorrect tags contain parameters such as <code>maximum-scale=1</code> and <code>user-scalable=no</code>.

<pre><code class="language-markup">&lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;
</code></pre>

## 9. Set `* { user-select: none }`, And All Is Good

<em>Some users will visit your beloved website and copy all of the text. This is shocking and must be stopped.</em>

Dear friends, setting the <a href="https://css-tricks.com/almanac/properties/u/user-select/"><code>user-select</code> property</a> to <code>none</code> can be useful, but only in parts of an interface that you expect users to interact with, where selection might do no good.

Therefore, I recommend using <code>user-select: none</code> for the following elements only:

*   icon navigation items,
*   carousels with overlaid text,
*   control elements such as dropdowns and navigation.

Please, never ever disable the selection of static text and images.

{{% ad-panel-leaderboard %}}

## 10. Load Web Fonts Incorrectly

<em>If the user lives to see the page load, kill them for good by making the font flicker or hide the content completely.</em>

Using web fonts is not wrong, but we have to make sure they are the first elements of the website to load. Some browsers wait for web fonts to load before displaying the content. This is known as a flash of invisible text (FOIT). Other browsers (Edge and Explorer) show a system font right where you least want it, known as a flash of unstyled text (FOUT).

There is a third possibility, <a href="https://www.zachleat.com/web/foft/">flash of faux text</a> (FOFT). Here, content is rendered with a regular cut of the web font, and then bold and italic cuts are displayed right after that.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b9799b-b8d3-4d29-baa0-bd9767756d41/image-4-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5951c603-167e-4fe0-8b28-717ccb7c79bd/image-4-500-opt.png" alt="image alt text" /></a><figcaption>FOUT in practice: Showing system fonts is better than showing a blank screen while the web fonts load. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b9799b-b8d3-4d29-baa0-bd9767756d41/image-4-opt.png">View large version</a>)</figcaption></figure>

My projects are usually content-based websites, so I prefer to display the content as quickly as possible using a system font (FOUT). This is when I like Microsoft browsers. I also use a small library named <a href="https://github.com/bramstein/fontfaceobserver">Font Face Observer</a>. Let’s look at the code. First, the JavaScript:

<pre><code class="language-javascript">var font = new FontFaceObserver('Webfont family');
font.load().then(function () {
  document.documentElement.className += ' webfont-loaded';
});
</code></pre>

And here is the CSS:

<pre><code class="language-css">body {
  font-family: sans-serif;
}

.webfont-loaded body {
  font-family: Webfont Family;
}
</code></pre>

Every website requires something different. Refer to Zach Leatherman’s “<a href="https://www.zachleat.com/web/comprehensive-webfonts/">Comprehensive Guide to Font-Loading Strategies</a>.”

## 11. Clutter The Page With Social Media Buttons

<em>If you can’t poison them with your own concoction, use your neighbor’s.</em>

Facebook, Twitter and Google buttons are uncomfortable for mobile users, for two reasons:

*   **They download a huge amount of data and slow the loading and rendering of websites.**  
Tests show that when the official social sharing buttons are used, visitors will download 300 KB more over more than 20 requests.
*   **They are usually useless. Social sharing is often integrated in the operating system.**  
A Moovweb study carried over the course of one year across 61 million mobile sessions showed that only 0.2% of mobile users do any social sharing.

The vast majority of social buttons are useless, even on desktop. Sharing is particularly useless in an online store, because a low sharing count is <a href="https://vwo.com/blog/removing-social-sharing-buttons-from-ecommerce-product-page-increase-conversions/">demotivating</a> for the buyer. But let’s not go there. We are trying to poison the mobile beast.

If you don’t want to poison the mobile user but you need social sharing buttons, try <a href="https://github.com/bradvin/social-share-urls#google">using social sharing URLs</a> or a plugin such as <a href="https://social-likes.js.org/">Social Likes</a>, which implements them with less impact on loading speed.

## 12. Faulty Redirection From Desktop To Mobile

<em>A “killer” developer who has an m-dot version of a website has one more way to poison the user. Hooray!</em>

We see <a href="https://developers.google.com/webmasters/mobile-sites/mobile-seo/common-mistakes#faulty-redirects">faulty redirects</a> on practically every other website with an m-dot version.

The correct implementation looks something like this:

1.  If a mobile visitor goes to `www.example.com/example`, the server detects their device and redirects them to `m.example.com/example` (not to `m.example.com`). The same happens on a mobile version accessed from a desktop.
2.  If that URL does not exist, then leaving the user on the desktop version is better than redirecting them to the m-dot home page.
3.  Let search engines know about the two versions of the website by using `<link rel="alternate">` or by indicating it in the `sitemap.xml` file. A [detailed guide](https://developers.google.com/webmasters/mobile-sites/mobile-seo/separate-urls) is in Google’s help section for webmasters.

## 13. Hide The Content Well

<em>Hide content from the mobile user. They don’t need it anyway.</em>

Whether you like it or not, people visit websites to see the content. Yes, we are forced to live among such spiteful creatures.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdf9e9ba-32c4-4c42-9ea7-fa5821078e5b/image-5-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eadd5345-8664-425d-8a1f-61469f7875de/image-5-500-opt.png" alt="image alt text" width="500" height="281" /></a><figcaption>The user seeks content. Give it to them as quickly as possible. Then, you can force them to download an app or submit their contact details. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdf9e9ba-32c4-4c42-9ea7-fa5821078e5b/image-5-opt.png">View large version</a>)</figcaption></figure>

Unfortunately, a lot of websites hide content, for reasons I don’t understand. Perhaps the content is not worthwhile, but I find that hard to believe. Numerous elements can cause content to be hidden:

*   **Cookie bar**.  
Some European websites are obliged to show the unfortunate [cookie consent](https://www.cookiechoices.org/) notification. And we can do nothing about it. However, this doesn’t mean that a cookie bar should be fixed and take up half the screen.
*   **Online chat window or newsletter subscription ad**.  
Positioning elements as fixed is very unfortunate on mobile devices. You are hiding content that the user came to see and are displaying content that they are not interested in. Using these elements is OK, but avoid fixing their position on mobile devices.
*   **App-download interstitials**.  
These are painful. Some websites invite you to install the accompanying app, instead of showing you the content. But users came to see the website! Instead, use [smart app banners](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html) on iOS or [native app install banners](https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android#native) on Android to advertise your native app.

<a href="https://webmasters.googleblog.com/2016/08/helping-users-easily-access-content-on.html">Google has decided</a> that, effective January 2017, overlapping content on mobile websites will be penalized:
<blockquote>[Content that is visually obscured by an interstitial] can frustrate users because they are unable to easily access the content that they were expecting when they tapped on the search result.

Pages that show intrusive interstitials impair the user experience more than pages whose content is immediately accessible.</blockquote>

For the record, Google will not penalize websites that show interstitials, such as cookie bars or age confirmations on adult websites.

## How Many Mobile Users Have You Poisoned Today?

That’s about it. Now, let’s be serious. There wasn’t anything “new” above, was there?

All the more reason to be sorry that the vast majority of responsive websites poison the mobile user.

Let’s summarize the critical information in a short checklist:

*   **Does your website render quickly enough on mobile?**  
Do less important elements block more important ones? Have you chosen the optimal strategy to render web fonts? Are third-party plugins (such as for social media) slowing down the website?
*   **Are you hiding content?**  
Are fixed elements getting in the way? Are you hiding content for particular resolutions or in landscape or portrait mode?
*   **Is the UI mobile-friendly?**  
Are the tap targets large enough? Are complex UI elements such as carousels implemented correctly on mobile? Are phone numbers clickable? Does content selection remain enabled? Do you make navigation visible wherever possible?
*   **Do you respect the native browser?**  
Have you disabled zooming by accident? Do you support gestures that conflict with browser defaults?
*   **Is your redirection implemented correctly** (if you’re using an m-dot version)?

Be kind to mobile users. Do not be the wicked old man who tries to get rid of The Little Mole in his yard. Do you want to know how the fairy tale ends? The Little Mole survives, laughs at the old man and moves to another garden.

#### Further Reading

- [Managing Mobile Performance Optimization](https://www.smashingmagazine.com/2016/03/managing-mobile-performance-optimization/)
- [The Thumb Zone: Designing For Mobile Users](https://www.smashingmagazine.com/2016/09/the-thumb-zone-designing-for-mobile-users/)
- [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)
- [Mobile-First Is Just Not Good Enough: Meet Journey-Driven Design](https://www.smashingmagazine.com/2017/02/mobile-first-is-just-not-good-enough-meet-journey-driven-design/)

{{< signature "da, yk, al, il, mrn" >}}
