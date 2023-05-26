---
title: How To Build A Mobile Website
slug: how-to-build-a-mobile-website
image: null
date: 2010-11-03T12:00:56.000Z
author: jon-raasch
description: >-
  **Over the past few years, mobile web usage has considerably increased** to the point that web developers and designers can no longer afford to ignore it.
categories:
  - Mobile
  - Android
  - Strategy
---
In wealthy countries, the shift is being fueled by faster mobile broadband connections and cheaper data service. However, a large increase has also been seen in developing nations where people have skipped over buying PCs and gone straight to mobile.

Unfortunately, the mobile arena introduces a layer of complexity that can be difficult for developers to accommodate. Mobile development is more than cross-browser, it should be <strong>cross-platform</strong>. The vast number of mobile devices makes thorough testing a practical impossibility, leaving developers nostalgic for the days when they only had to support legacy browsers.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why We Shouldn’t Make Separate Mobile Websites](https://www.smashingmagazine.com/2012/04/why-we-shouldnt-make-separate-mobile-websites/)
*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)
*   [How To Use CSS3 Media Queries To Create a Mobile Version of Your Website](https://www.smashingmagazine.com/2010/07/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/)
*   [<span class="headline">Building A Better Responsive Website</span>](https://www.smashingmagazine.com/2013/03/building-a-better-responsive-website/)

In addition to supporting different platforms, each device may use any number of <a href="https://webtrends.about.com/od/mobileweb20/tp/list_of_mobile_web_browsers.htm">mobile web browsers</a>. For instance, an Android user could access your site using the native Android browser, or could have also installed Opera Mini or Firefox Mobile. It's fine as long as the smartphone uses a progressive web browser (and it's safe to say that most browsers are progressive nowadays), but it doesn't have to.

{{% feature-panel %}}

<a href="https://tech.fortune.cnn.com/2010/06/04/nielsen-iphone-android-gain-on-rim/"><img loading="lazy" decoding="async" class="66996" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/665bb9cd-c0e6-4fbf-932c-45ec6d610f02/smartphone.jpg" alt="Smartphone Market Share" width="450" height="511" /></a><br>
<em>Source: <a href="https://blog.nielsen.com/nielsenwire/online_mobile/iphone-vs-android/">Nielsen Study</a>, <a href="https://tech.fortune.cnn.com/2010/06/04/nielsen-iphone-android-gain-on-rim/">Image credit</a></em>

The mobile web reintroduces several issues that have been largely ignored in recent years. First, even with 4G networks, <em>bandwidth </em>becomes a serious issue for mobile consumers. Additionally, mobile devices have a<strong> significantly reduced screen size</strong>, which presents screen real estate issues that have not existed since the days of projection monitors. Combine these issues with cross-platform compatibility problems, and it isn't hard to see how mobile development is a lot like 'stepping backwards in time'. So let's tackle these issues one at a time and create a road map for mobile web development:

*   [How To Implement Mobile Stylesheets](#mobile-stylesheets)
*   [What To Change With Mobile Stylesheets](#styles-to-change)
*   [Beyond Stylesheets](#beyond-stylesheets)
*   [Special Concerns For iPhone / iPad](#iphone)

<a name="mobile-stylesheets"></a>

## How To Implement Mobile Stylesheets

The first step to adding mobile support to a website is including a special stylesheet to adjust the CSS for mobile devices:

### Server-side Methods & The UA String

One approach to including mobile stylesheets involves detecting the <a href="https://en.wikipedia.org/wiki/User_agent">user agent string</a> with a server-side language such as PHP. With this technique, the site detects mobile devices and either serves an appropriate stylesheet or redirects the user to a mobile subdomain, for instance <a href="https://m.facebook.com/">m.facebook.com</a>. This server-side approach has several advantages: it guarantees the highest level of compatibility and also allows the website to serve special mark-up/content to mobile users.

<img loading="lazy" decoding="async" class="66991" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5564edbd-f3bc-4f5e-bf47-c2d71adc0ef1/facebook-mobile.jpg" alt="Facebook Mobile (m.facebook.com)" width="215" height="400" /><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5564edbd-f3bc-4f5e-bf47-c2d71adc0ef1/facebook-mobile.jpg">Large image</a></em>

While this technique is perfect for enterprise level websites, there are <strong>practical concerns</strong> that make it difficult to implement on most sites. New user agent strings come out almost daily, so keeping the UA list current is next to impossible. Additionally, this approach depends on the device to relay its true user agent. Even though, browsers have spoofed their UA string to get around this type of detection in the past. For instance, most UA strings still start with "Mozilla" to get through the Netscape checks used in the 90's, and for several years <a href="https://www.betanews.com/article/Opera-to-Stop-Spoofing-IE-User-Agent/1122911404">Opera pretended to be IE</a>. As <a href="https://www.quirksmode.org/blog/archives/2010/09/state_of_mobile_1.html">Peter-Paul Koch writes</a>:
<blockquote>"It's an arms race. If device detection really catches on, browsers will start to spoof their user agent strings to end up on the right side of the detects."</blockquote>

### Client-side Methods & Media Queries

Alternately, the easiest approach involves detecting the mobile device on the client side. One of the earliest techniques for including mobile stylesheets involves taking advantage of the stylesheet's media type, for instance:

<pre>&lt;link rel="stylesheet" href="site.css" media="screen" /&gt;
&lt;link rel="stylesheet" href="mobile.css" media="handheld" /&gt;</pre>

Here we've included two stylesheets, the first <code>site.css</code> targets desktops and laptops using the <code>screen</code> media type, while the second <code>mobile.css</code> targets mobile devices using <code>handheld</code>. While this would otherwise be an excellent approach, device support is another issue. Older mobile devices tend to support the <code>handheld</code> media type, however they vary in their implementation: some disable the <code>screen</code> stylesheets and only load <code>handheld</code>, whereas others load both.

Additionally, most newer devices have done away with the <code>handheld</code> distinction altogether, in order to serve their users fully-featured web pages as opposed to duller mobile layouts. To support newer devices, we'll need to use <a href="https://www.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/">media queries</a>, which allow us to target styles to the device width (you can see another practical adaptation of media queries in Ethan Marcotte's article <a href="https://www.alistapart.com/articles/responsive-web-design/">Responsive Web Design</a>). Since mobile devices typically have smaller screens, we can target handheld devices by detecting screens that are 480px and smaller:

<pre>&lt;link rel="stylesheet" href="mobile.css" media="only screen and (max-device width:480px)"/&gt;</pre>

While this targets most newer devices, many older devices don't support media queries, so we'll need a <a href="https://www.alistapart.com/articles/return-of-the-mobile-stylesheet">hybrid approach</a> to get the largest market penetration.

First, define two stylesheets: <code>screen.css</code> with everything for normal browsers and <code>antiscreen.css</code> to overwrite any styles that you don't want on mobile devices. Tie these two stylesheets together in another stylesheet <code>core.css</code>:

<pre>@import url("screen.css");
@import url("antiscreen.css") handheld;
@import url("antiscreen.css") only screen and
(max-device-width:480px);</pre>

Finally, define another stylesheet <code>handheld.css</code> with additional styling for mobile browsers and link them on the page:

<pre>&lt;link rel="stylesheet" href="core.css" media="screen"/&gt;
&lt;link rel="stylesheet" href="handheld.css" media="handheld,
only screen and (max-device-width:480px)"/&gt;</pre>

While this technique reaches a large market share of mobile devices, it is by no means perfect. Some mobile devices such as iPad are more than 480 pixels wide and will not work with this method. However, these larger devices arguably don't need a condensed mobile layout. Moving forward, there will likely be more devices that don't fit into this mold. Unfortunately, it is very difficult to future-proof mobile detection, since standards are still emerging.

Besides device detection, the media query approach also presents other issues. Mainly, media queries can only style content differently and provide no control over content delivery. For instance, a media query can be used to hide a side column's content, but it cannot prevent that mark-up from being downloaded by your users. Given mobile bandwidth issues, this additional HTML should not simply be ignored.</p>

### User Initiated Method

<a href="https://www.ikea.com/us/en/"><img loading="lazy" decoding="async" class="68330" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6cbe9b2-0931-4f9a-bf0e-65633f65f7b4/ikea-website.jpg" alt="Ikea's non-mobile site" width="500" height="264" /></a>

Considering the difficulties with mobile UA detection and the pitfalls of media queries, some companies such as <a href="https://www.ikea.com/us/en/">IKEA</a> have opted to simply<strong> allow the user to decide</strong> whether to view the mobile version of their website. While this has the clear disadvantage of requiring more user interaction, it is arguably the most fool-proof method and also the easiest to accomplish.

The site contains a link that reads "Visit our mobile site" which transports the user to a mobile subdomain. This approach has some drawbacks. Of course, some mobile users may miss the link, and other non-mobile visitors may click it, since it is visible regardless of what device is being used. Even though, this technique has the advantage of allowing the user to make the mobile decision. Some users prefer a condensed layout that is optimized for their device, whereas other users may prefer to access the entire website, without the restrictions of a limited mobile layout.

<a name="styles-to-change"></a>

## What To Change With Mobile Stylesheets

Now that we've implemented mobile stylesheets, it's time to get down to the nuts and bolts of which styles we actually want to change.</p>

### Increase & Alter Screen Real Estate

<img loading="lazy" decoding="async" class="68597" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc67a28c-13ac-4280-b26f-dd607ab2d0d2/cnn-regular-vs-mobile1.jpg" alt="CNN Standard Site vs. Mobile" width="500" height="265" />

The primary goal of mobile stylesheets is to alter the layout for a smaller display. First and foremost this means reducing multi-column layouts to <strong>single columns</strong>. Most mobile screens are vertical, so horizontal space becomes even more "expensive" and mobile layouts can rarely afford more than one column of content. Next, reduce clutter throughout the page by setting <code>display: none;</code> on any less important elements. Finally, save additional pixels by reducing margins and padding to create a tighter layout.</p>

### Reduce Bandwidth

Another goal of mobile stylesheets is to reduce bandwidth for slower mobile networks. First make sure to remove or replace any large background images, especially if you use a background image for the whole site. Additionally set <code>display: none</code> on any unnecessary content images.

If your site uses images for buttons or navigation, consider replacing these with plain-text / CSS counterparts. Finally if you'd like to force the browser to use the alternate text for any of your images, use this snippet (and use JavaScript to add the <code>as-text</code> class for <code>img</code> and make sure that <code>alt</code>-attributes are properly defined in your markup):

<pre>img.as-text { content: attr(alt); }</pre>

### Other Changes

Besides addressing screen size and bandwidth concerns, there are a few additional changes that should be made in any mobile stylesheet. First, you can <strong>improve readability by increasing the font size</strong> of any small or medium-sized text. Next, clicking is generally less precise on mobile devices, so make sure to increase the clickable areas of any important buttons or links by setting <code>display: block</code> and adding padding to the clickable elements.

Additionally, <strong>floated elements</strong> can cause problems for mobile layouts, so consider removing any floats that aren't absolutely necessary. Remember that horizontal real estate is especially expensive on mobile, so you should always opt for adding vertical scrolling as opposed to horizontal.

Finally, <strong>mouseover states</strong> do not work with most mobile devices, so make sure to have proper definitions of <code>:active</code>-states. Also, sometimes it may be useful to apply definitions from the already defined <code>:hover</code> states to the <code>:active</code> states. This pseudo-class is displayed when the user clicks an item, and therefore will work on mobile devices. However this only enhances the user experience and should not be relied on for more important elements, such as drop-down navigation. In these cases it is best to show the links at all times in mobile devices.

<a name="beyond-stylesheets"></a>

## Beyond Stylesheets

In addition to mobile stylesheets, we can add a number of special mobile features through mark-up.</p>

### Clickable Phone Numbers

First, most handheld devices include a phone, so let's make our phone numbers clickable:

<pre>&lt;a href="tel:15032084566" class="phone-link"&gt;(503) 208-4566&lt;/a&gt;</pre>

Now mobile users can click this number to call it, however there are a few things to note. First, the number in the actual link starts with a 1 which is important since the web is international (1 is the US country code).

Second, this link is clickable whether or not the user has a mobile device. Since we're not using the server-side method described above, our best option is to simply hide the fact that the number is clickable via CSS. So use the <code>phone-link</code> class to disable the link styling in your screen stylesheet, and then include it again for mobile.</p>

### Special Input Types

<img loading="lazy" decoding="async" class="67000" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9649b9eb-d439-40e5-b3fb-936bb57aaa91/iphone-html5-input-types.jpg" alt="iPhone displays special HTML5 input types " width="450" height="327" />

When it comes to mobile browsing, another concern is the difficulty of typing compared to a standard full-sized keyboard. But we can make it easier on our users by taking advantage of some special <a href="https://www.456bereastreet.com/archive/201004/html5_input_types/">HTML5 input types</a>:

<pre>&lt;input type="tel" /&gt;
&lt;input type="email" /&gt;</pre>

These input types allow devices such as iPhone to display a <strong>contextual keyboard</strong> that relates to the input type. In the example above <code>type="tel"</code> triggers a numeric keypad ideal for entering phone numbers, and <code>type="email"</code> triggers a keypad with <code>@</code> and <code>.</code> buttons.

HTML5 input types also provide in-browser validation and special input menus that are useful in both mobile and non-mobile browsing. Furthermore, since non-supportive browsers naturally degrade to view these special input types as <code>&lt;input type="text" /&gt;</code>, there's no loss in using HTML5 input types throughout your websites today.

<a href="https://www.456bereastreet.com/archive/201004/html5_input_types/">See a complete list of HTML5 input types</a>. You can find some information about the current browser support of HTML5 input attributes in the post <a href="https://www.standardista.com/html5-input-attributes-browser-support">HTML5 Input Attributes &amp; Browser Support</a> by Estelle Weyl.</p>

### Viewport Dimensions & Orientation

When modern mobile devices render a webpage, they scale the page content to fit inside their viewport, or visible area. Although the default viewport dimensions work well for most layouts, it is sometimes useful to <a href="https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html">alter the viewport</a>. This can be accomplished using a <code>&lt;meta&gt;</code> tag that was introduced by Apple and has since been picked up by other device manufacturers. In the document's <code>&lt;head&gt;</code> include this snippet:

<pre>&lt;meta name="viewport" content="width=320" /&gt;</pre>

In this example we've set the viewport to <code>320</code>, which means that 320 pixels of the page will be visible across the width of the device.

The viewport meta tag can also be used to disable the ability to resize the page:

<pre>&lt;meta name="viewport" content="width=320,user-scalable=false" /&gt;</pre>

However, similar to disabling the scrollbars, this technique takes control away from the user and should only be used for a good reason.

Additionally, it is possible to add certain styles based on the <strong>device orientation</strong>. This means that different styles can be applied depending on whether the user is holding their phone vertically or horizontally.

To detect the device orientation, we can use a media query similar to the client-side device detection we discussed earlier. Within your stylesheet, include:

<pre>@import url("portrait.css") all and
(orientation:portrait);
@import url("landscape.css") all and
(orientation:landscape);</pre>

Here <code>portrait.css</code> styles will be added for vertical devices and the <code>landscape.css</code> will be added for horizontal.

However orientation media queries have <a href="https://www.quirksmode.org/blog/archives/2010/04/the_orientation.html">not been adopted by all devices</a>, so this is best accomplished with the <a href="https://www.1stwebdesigner.com/tutorials/how-to-use-css3-orientation-media-queries/"><code>max-width</code> media query</a>. Simply apply different max-width queries for the different orientation widths you want to target. This is a much more robust approach, since presumably the reason to target different orientations is to style for different widths.

<a name="iphone"></a>

## Special Concerns For iPhone / iPad

<img loading="lazy" decoding="async" class="67001" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046b33d7-0ede-46dd-8e5f-b191d7155993/iphone-41.jpg" alt="iPhone 4" width="204" height="300" />

With a <a href="https://news.cnet.com/8301-13579_3-20006889-37.html">market share of 28%</a> and estimates of as much as <a href="https://techcrunch.com/2009/03/24/iphone-now-50-percent-of-smartphone-web-traffic-in-the-us/">50% of mobile browsing</a> going through iPhone, it makes sense that developers make special accommodations for the mobile giant.</p>

### No Flash

Regardless of Apple's ethics, the reality is that iPhones do not play Flash unless they are <a href="https://en.wikipedia.org/wiki/IOS_jailbreaking">jailbroken</a>. Fortunately, there are alternatives to Flash, and iPhone's issues with this technology are often easy to get around. The main use for Flash in modern websites is Flash video, which can easily be circumvented using <strong>HTML5 video</strong>. However since older browsers don't support HTML5, make sure to <a href="https://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-html-5-video-with-a-fallback-to-flash/">include a Flash backup</a> for non-supportive browsers (this is why the whole debate about Flash vs. HTML5 is a bit pointless, because you can actually offer both to your users and the user's device will pick up the one it can render automatically).

Beyond video, it is usually best to use JavaScript to accommodate any simple functionality. JavaScript libraries such as jQuery make it easy to build rich interactive applications without Flash. Regardless of your desire to support iPhone, these JavaScript apps typically have a number of additional advantages over Flash alternatives.

Finally, certain applications are simply too hard to recreate with HTML5 and Javascript. For these, iPhone users will have to be left out, however make sure to include appropriate alternate content.

<img loading="lazy" decoding="async" class="66994" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c553c90-2454-48fc-9d4d-27c28d99b4b1/apple-loves-adobe.jpg" alt="Apple Loves Adobe" width="400" height="230" /><br>
<em>A spoof of Adobe's "We Love Apple" campaign, where the heart is replaced by the broken plugin icon.</em>

### Other Shortcomings

Besides Flash, there are a few additional caveats to supporting iPhones and iPads.

First, iPhone <a href="https://stackoverflow.com/questions/1577003/uploading-files-using-html-file-input-on-iphone">does not support</a> <code>&lt;input type="file" /&gt;</code>, since it does not have an accessible internal file structure. While most mobile devices connect to a computer as an external hard-drive, Apple has taken steps to ensure that the iPhone file structure remains obfuscated.

Next, iPhone will only cache files that are <strong>25 kb</strong> or less, so try to keep any reused files under this restriction. This can be a bit counter-intuitive, as it often means breaking out large image sprites and concatenated JavaScripts into smaller chunks. However be careful to serve these files only to iPhone, or it will cause extra HTTP requests in all other browsers.

Finally, when it comes to <code>@font-face</code> font embedding, iPhone's Mobile Safari doesn't fully support it and supports the <strong>SVG file format</strong> instead. However, SVG fonts are only supported by Chrome, Opera and iPhone, so we'll need a hybrid approach to target all browsers. In addition to the SVG, we'll need an .otf or .ttf for Firefox and Safari, as well as an <a href="https://en.wikipedia.org/wiki/Embedded_OpenType">EOT</a> for IE (IE has actually supported <code>@font-face</code> since IE4).

After obtaining the necessary files, tie them all together with the appropriate CSS:

<pre>@font-face {
    font-family: 'Comfortaa Regular';
    src: url('Comfortaa.eot');
    src: local('Comfortaa Regular'),
         local('Comfortaa'),
         url('Comfortaa.ttf') format('truetype'),
         url('Comfortaa.svg#font') format('svg');
}</pre>

For more information, read this article on cross-platform font-face support.</p>

### Special iPhone / iPad Enhancements

Despite iPhone's various shortcomings, the device offers a wonderfully rich user experience that developers can leverage in ways not possible with older mobile devices.

First, there are a variety of <strong>JavaScript libraries</strong> that can be used to access some of the more advanced functionality available in iPhone. Take a look at <a href="https://www.sencha.com/products/touch/">Sencha Touch</a>, <a href="https://www.jqtouch.com/">jQTouch</a> and <a href="https://code.google.com/p/iui/">iui</a>. These three libraries allow you to better interface with the iPhone, and also work on similar devices such as Android. Additionally, keep an eye on the much anticipated <a href="https://jquerymobile.com">jQuery Mobile</a> which has just been released in alpha.

Next, the <a href="https://www.apple.com/iphone/apps-for-iphone/#heroOverview">App Store</a> isn't the only way to get an icon on your users' iPhones: you can simply have them bookmark your page. Unfortunately the default <strong>bookmark icon</strong> is a condensed screen shot of the page, which doesn't usually look very good, so let's create a special iPhone icon. Also check the <a href="https://www.hicksdesign.co.uk/iconreference/">Icon Reference Chart</a> by Jon Hicks for further details.

Start by saving a 57 x 57 pixel PNG somewhere on your website, then add this snippet within your <code>&lt;head&gt;</code> tag:

<pre>&lt;link rel="apple-touch-icon" href="/customIcon.png"/&gt;</pre>

Don't worry about rounded corners or a glossy effect, iPhone will add those by default.

<a name="conclusion"></a>

## Conclusion

As the worldwide shift to mobile continues, handheld device support will become increasingly important. Hopefully this article has left you with both the desire and toolset necessary to make mobile support a reality in your websites.

Although mobile occupies a significant chunk of global web browsing, the technology is still very much in its infancy. Just as standards emerged for desktop browsing, new standards are emerging to unify mobile browsers. This means that the techniques described in this article are only temporary, and it is your responsibility to stay on top of this ever-changing technology.

In fact, the only thing in web development that remains constant is the perpetual need to continue learning!

### Additional Reading

*   [State of Mobile Web Development](https://www.quirksmode.org/blog/archives/2010/09/state_of_mobile.html) - A general discussion of mobile dev in 3 parts
*   [Return of the Mobile Stylesheet](https://www.alistapart.com/articles/return-of-the-mobile-stylesheet) - More about the client-side stylesheet technique we used
*   [Hardboiled CSS3 Media Queries](https://stuffandnonsense.co.uk/blog/about/hardboiled_css3_media_queries) - How to target stylesheets for specific devices
*   <span class="removed_link" title="https://www.cloudfour.com/css-media-query-for-mobile-is-fools-gold/">CSS Media Query for Mobile is Fool's Gold</span> - Arguments against using media queries
*   [Mobile Web Design](https://abduzeedo.com/mobile-web-design) - A design perspective
*   [Mobile operating systems and browsers are headed in opposite directions](https://radar.oreilly.com/2010/05/mobile-operating-systems-and-b.html) - Trends in mobile platforms and browsers
*   [Pocket-Sized Design: Taking Your Website to the Small Screen](https://www.alistapart.com/articles/pocket/) - An older but still useful high quality article.

<em>(ik) (vf)</em>

