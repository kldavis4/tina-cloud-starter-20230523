---
title: HTML5 and The Future of the Web
slug: html5-and-the-future-of-the-web
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/460cf717-6eb9-4851-8ac9-8236afc6d37a/html5-ta-da-illu.jpg
date: 2009-07-16T20:49:22.000Z
author: tim-wright
description: >-
  Some have [embraced
  it](https://radar.oreilly.com/2009/05/google-bets-big-on-html-5.html), some
  have [discarded it](https://ishtml5readyyet.com/) as too far in the future, and
  some have [abandoned a misused
  friend](https://mezzoblue.com/archives/2009/04/20/switched/) in favor of an old
  flame in preparation. Whatever side of the debate you're on, you've most
  likely heard all the blogging chatter surrounding the "new hotness" that is
  **HTML5**. It's everywhere, it's coming, and you want to know everything you
  can before it's old news.

  Things like jQuery plugins, formatting techniques, and design trends change
  very quickly throughout the Web community. And for the most part we've all
  accepted that some of the things we learn today can be obsolete tomorrow, but
  that's the nature of our industry.

  When looking for some stability, we can usually turn to the code itself as it
  tends to stay unchanged for a long time (relatively speaking). So when
  something comes along and changes our code, it's a big deal; and there are
  going to be some growing pains we'll have to work through. Luckily, rumor has
  it, that we have [once less change to worry
  about](https://www.zeldman.com/2009/07/02/xhtml-wtf/).

  In this article, I'm hoping to give you some tips and insight into HTML5 to
  help ease the inevitable pain that comes with transitioning to a slightly
  different syntax. **Welcome to HTML5**.
categories:
  - Coding
  - HTML5
  - HTML
---
Some have <a href="https://radar.oreilly.com/2009/05/google-bets-big-on-html-5.html">embraced it</a>, some have <a href="https://ishtml5readyyet.com/">discarded it</a> as too far in the future, and some have <a href="https://mezzoblue.com/archives/2009/04/20/switched/">abandoned a misused friend</a> in favor of an old flame in preparation. Whatever side of the debate you're on, you've most likely heard all the blogging chatter surrounding the "new hotness" that is <strong>HTML5</strong>. It's everywhere, it's coming, and you want to know everything you can before it's old news.

Things like jQuery plugins, formatting techniques, and design trends change very quickly throughout the Web community. And for the most part we've all accepted that some of the things we learn today can be obsolete tomorrow, but that's the nature of our industry.

When looking for some stability, we can usually turn to the code itself as it tends to stay unchanged for a long time (relatively speaking). So when something comes along and changes our code, it's a big deal; and there are going to be some growing pains we'll have to work through. Luckily, rumor has it, that we have <a href="https://www.zeldman.com/2009/07/02/xhtml-wtf/">one less change to worry about</a>.

Be sure to check out our previous articles:

*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [Road Map To Coding With HTML5: Tutorials and Guidelines](https://www.smashingmagazine.com/coding-with-html5-tutorials-guidelines/)
*   [HTML5 Semantics](https://www.smashingmagazine.com/2011/11/html5-semantics/)
*   [HTML5: The Facts And The Myths](https://www.smashingmagazine.com/2010/09/html5-the-facts-and-the-myths/)

{{% feature-panel %}}

In this article, I'm hoping to give you some tips and insight into HTML5 to help ease the inevitable pain that comes with transitioning to a slightly different syntax.

<strong>Welcome to HTML5</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742dca9f-0727-4883-ace2-4d2e5c501f87/html5-logo.png" alt="HTML5 logo" width="450" height="180" />

## What are the basics?

### The DOCTYPE

When I first started researching HTML5 a few months ago, one of the main things I struggled to find was the doctype. A simple thing, you'd think it would be everywhere, but after much frustration, I finally found it buried within <a href="https://w3.org">w3.org</a> and here it is:

<pre><code class="language-markup tmp-xml">&lt;!DOCTYPE html&gt;</code></pre>

I was also curious why they chose to "html" rather than "html5", it seemed like the logical way to tell a browser that the current document was written in HTML5, and offered a good template for the future. But I found that <code>&lt;!DOCTYPE html5&gt;</code> triggers <a href="https://www.quirksmode.org/">Quirks Mode</a> in IE6, and when taking backwards compatibility into consideration <code>&lt;!DOCTYPE html&gt;</code> is a pretty good choice (in my opinion).

Overall, I really like the new DOCTYPE; it's small, meaningful, and maybe we'll actually be able to remember this one by heart and not have to paste it from site to site.</p>

### New Elements you should know

At first glance, with HTML5, the new elements immediately jump out and command attention. The W3C really listened to the community and planned for the future when architecting the abundance of new elements available. We have everything from basic structural elements like <code>&lt;header&gt;</code> and <code>&lt;footer&gt;</code> to others like <code>&lt;canvas&gt;</code> and <code>&lt;audio&gt;</code> that tap into, what seems to be, a very powerful API which allows us the freedom to create more user-friendly applications while further distancing ourselves from reliance on Flash for saving data and intense animation.

#### The new structural elements

*   `<header>` The header element contains introductory information to a section or page. This can involve anything from our normal documents headers (branding information) to an entire **table of contents**.
*   `<nav>` The nav element is reserved for a section of a document that contains links to other pages or links to sections of the same page. Not all link groups need to be contained within the <nav> element, just **primary navigation**.
*   `<section>` The section element represents a **generic document or application section**. It acts much the same way a `<div>` does by separating off a portion of the document.
*   `<article>` The article element represents a portion of a page which can stand alone such as: a blog post, a forum entry, user submitted comments or any **independent item of content**.
*   `<aside>` Aside, represents content related to the main area of the document. This is usually expressed in sidebars that contain elements like related posts, tag clouds, etc. They can also be used for **pull quotes**.
*   `<footer>` The footer element is for marking up the footer of, not only the current page, but each section contained in the page. So, it's very likely that you'll be using the <footer> element multiple times within one page.

When you take a look at these new elements, it looks like they're just replacing our common DIV IDs; and in a way, it's true. But, the diagram below shows that elements like <code>&lt;header&gt;</code> and <code>&lt;footer&gt;</code> can be used more than once on a single page where they behave more like classes and normal HTML elements that you can use over and over again to retain a semantic structure.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5aae2c5-9c90-49ca-8a93-44dd63cf132e/html5-structure.png" alt="HTML5 Structure Doc" width="434" height="320" />

Elements like &lt;header&gt; and &lt;footer&gt; are not just meant to represent the top and bottom of the current document, but they also represent the <code>&lt;header&gt;</code> and <code>&lt;footer&gt;</code> of each document section, much the way we use <code>&lt;thead&gt;</code> and <code>&lt;tfoot&gt;</code> in data tables.

The benefits of using these structural elements is mainly due to the fact that they are extremely well defined and provide a great way to semantically structure your document. However, these elements do need to be used with some <strong>careful thought</strong> because they can, very easily be overused.

#### Further Reading on structural HTML5

*   Steve Smith on Structural Tags in HTML5
*   Lachlan Hunt's [Preview of HTML5](https://www.alistapart.com/articles/previewofhtml5)
*   Elliot Harold on [New Elements in HTML5](https://www.ibm.com/developerworks/library/x-html5/?ca=dgr-lnxw01NewHTML)
*   Bruce Lawson's [HTML5 Form Demo](https://www.brucelawson.co.uk/tests/html5-forms-demo.html)

### Easing the transition from XHTML

Even though HTML 4.01, XHTML 1.0, &amp; HTML5 are all very similar there are some small syntax differences that can, very easily, slip past anyone and invalidate code. Keeping this in mind, HTML5 has some built-in "slack" to make the transition a little easier.

For example, when marking up a form in HTML5, this is the proper syntax for an input text element:

<pre><code class="language-markup tmp-xml">&lt;input type="text" id="name"&gt;</code></pre>

But this is also accepted as valid code in an attempt to ease the pain for avid XHTML coders (like myself) who are used to self-closing elements:

<pre><code class="language-markup tmp-xml">&lt;input type="text" id="name"/&gt;</code></pre>

The same rules apply to <code>&lt;meta&gt;</code> and other self closing elements. Legacy elements like <code>&lt;b&gt;</code> and <code>&lt;i&gt;</code> were also left in to help those coming over from HTML 4.01.l

## What are the benefits?

With any new technology there has to be benefit; why else would you use it? If your old code works just as well and efficient as the new code there's no reason to upgrade. No reason at all, trust me, I checked.

Luckily HTML5 is <em>packed</em> with cool new features, code slimming techniques and a lot of stuff I would call very large <strong>benefits</strong>. Most of which circle around the new APIs and the <strong>DOM tree</strong>.</p>

### Extending the API

The most obvious benefit built into HTML5 is the numerous <a href="https://www.w3.org/TR/html5-diff/#apis">APIs</a> and the opportunities it opens up for the future of web apps with Holy Grail of <strong>application cache </strong>and <strong>offline capabilities</strong>. Google Gears gave us offline data storage and Flash introduced us to the power of application cache (Pandora uses it to save your log in information). With HTML5, these capabilities are now available to use right in the language and can easily be expanded with JavaScript.

HTML5 relies on light scripting to flex its muscles on the Web; this is very possibly the first time, other than jQuery, that one (front-end) technology has fully acknowledged another. Sure, we connect them with classes and IDs but up until now, they have been perceived as separate layers by the principles of progressive enhancement. But as the Web grows we need unity like this across the Web.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1a35ea5-df91-4278-9032-5d5dc039b329/html5-api.png" alt="HTML5 API" width="450" height="100" />

#### Offline Data Storage

The coolest part about HTML5 is definitely its offline capabilities. Programs like Thunderbird and Outlook (and now GMail to an extent) let you browse through your old data while staying offline. With HTML5, you'll have this same functionality, but in the browser. This is the first serious step towards bridging the gap between the desktop and the Web, and opens all sorts of doors for the future of Web apps.

The W3C has taken the best parts from the various Web technologies and rolled them into, what is being dubbed the most powerful markup language to date.

#### Some other of the HTML5 APIs

*   [Drag & Drop](https://www.w3.org/TR/2008/WD-html5-20080122/#dnd) The drag and drop API defines an event-based drag and drop system. However, it never defines what "drag and drop" is. This API requires JavaScript to fully work as normal think drag and drop functionality.
*   [Video](https://dev.w3.org/html5/spec/Overview.html#video) & [Audio](https://dev.w3.org/html5/spec/Overview.html#audio) The audio & video APIs are massive upgrades in media embedding. Although support is limited right now, something like video embedding has never been easier:

        <video width="400" height="360" src="vid.mp4">

*   [Geolocation](https://dev.w3.org/geo/api/spec-source.html) Geolocation is a very cool API available within HTML5\. Its object can be used to programmatically determine location information through a device's user agent (hint hint: mobile devices).

#### Further reading on the HTML5 API

*   [Offline Web Applications](https://www.w3.org/TR/offline-webapps/)
*   [Offline Application Caching](https://www.w3.org/TR/offline-webapps/#offline)
*   Remy Sharp on [JavaScript APIs HTML5](https://www.slideshare.net/remy.sharp/html5-js-apis) (presentation)
*   [O3D Beach Demo](https://youtube.com/html5) from Google (must have an HTML5 capable browser)

## Where can I use it?

Even with the very limited support for HTML5, the Web is far too progressive to not create a testing environment for us to play around. Currently, Safari is our best testing platform, as it supports most of the new elements and APIs. Of course, that may change at anytime so keep and eye on Opera, Chrome and Firefox as well.

Normally you might think since Safari is a Webkit browser, by default, all Webkit browsers would support the same elements, unfortunately, this isn't the case. While many of the HTML5 features <em>are</em> supported across the board in Webkit browsers, there are some, like <code>&lt;video&gt;</code>, that are not.</p>

### Mobile devices

To effectively use HTML5 right now, we need to be able to <strong>control the environment</strong> in which it is used. Since support is not as widespread as we'd like it doesn't make real sense for it to be heavily used unless, of course, we can lock down the usage to certain platforms which have HTML5 support. With Webkit leading the way for HTML5, we can safely focus on devices powered by Webkit.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d233acbb-9f5b-4e7e-89ee-a9fa869cc78c/mobile-phones.png" alt="HTML5 API" width="480" height="242" />

The 3 hottest mobile devices right now: The Palm Pre, iPhone 3Gs and the new Google Android phone all have browsers that are based off the <strong>Webkit rendering engine</strong>.

Safari is even leading the way on the mobile HTML5 front; The iPhone (with the latest software upgrade) is the only device I could get to properly render the &lt;audio&gt; element. Because these devices are so young and all use the same rendering engine, the likelihood of them pushing a rapid software upgrade is pretty high.

Right now, you can confidently use many of the HTML5 features in iPhone Web app development and mostly likely expect Pre and Android to follow in suit.

#### Further reading on where you can use HTML5

*   [HTML5 Features in latest iPhone](https://ajaxian.com/archives/html5-features-in-latest-iphone-application-cache-and-database)
*   [GMail for HTML5](https://google-code-updates.blogspot.com/2009/06/gmail-for-mobile-html5-series.html)
*   [HTML5 Cheat Sheet](https://www.smashingmagazine.com/2009/07/06/html-5-cheat-sheet-pdf/)

## How can we move forward?

Even with all the recent hype surrounding HTML5 and how we all want to use it, it is still going to be a very slow transition away from HTML4.01 &amp; XHTML1.0. It will take time to get developers up to speed, test all the features, waiting for all the :ahem: browsers to catch up, and it will take an especially long time for users to transition out of those old browsers. With all that in mind, we know who we are, we're all reading this article (I've read it about 30 times so far) and we know we have to find a legitimate way to move forward without damaging the past.

We can't make the full switch yet and there's no use at this point pointing out who is holding up the show. We all know that any responsible developer would not drop support for a browser that is still heavily used. So rather than yell at a brick wall, here are some things I've found that might help us move forward in a positive way:

### Semantic DIV naming

Semantically aligning your DIV names with that of the new HTML5 elements will help you get used to the names themselves and also the new functionality and nesting that they want you to do with the <code>&lt;header&gt;</code> and <code>&lt;footer&gt;</code> elements. These are akin to learning the intro to Enter Sandman (for the guitarist out there); it's not very difficult, but it takes a little practice to get it to feel natural.

Before jumping in full-force to HTML5 production sites, I recommend trying the soft transition with changing your DIV names slightly. There's no downside that I've found to doing this, you can even use the new DOCTYPE with very little consequence.</p>

### Faking it with JavaScript

First off, I'd like to say: Please don't do this in production. If the client side scripting fails, it will completely collapse the site in browsers that won't take CSS applied to the new elements. This is simply not a good option. It is, however, an option and I'm all about knowing your options no matter what they are.

#### Creating the new elements with JavaScript

Working in jQuery is cool and all, but as it turns out, there is a built in function to JavaScript to deal with creating new elements:
<pre class="js">document.createElement('header');
document.createElement('footer');
document.createElement('section');
document.createElement('aside');
document.createElement('nav');
document.createElement('article');
document.createElement('figure');
document.createElement('time');</pre>
...and so on in that fashion.

This will allow you to style these elements in Internet Explorer. Again, the downside of using this technique is that, without the all-important JavaScript, the site will not only be unstyled, all the unrecognized elements will default to inline. So your site will literally collapse on itself.

Client side JavaScript is not the answer for using HTML5. <strong><a href="https://ejohn.org/blog/server-side-javascript-with-jaxer/">Server side javascript</a></strong>, now that's a completely different story...</p>

### Building browser-specific apps

I've always promoted building sites for your audience, so depending on your audience, building browser-specific applications may be a real option. As I mentioned above, it's all about <strong>controlling the environment</strong>, if we can control the environment we can control features delivered to the user much better. Google is currently attempting to do this with <a href="https://wave.google.com/">Google Wave</a>.

The idea behind Google's new monster product is to revolutionize communication, and do so with the newest technology. Google Wave is built in HTML5 and isn't usable in all browsers yet. But that's alright since they're controlling the audience by only releasing it to select developers for testing.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/906ce6ab-ff9d-4467-acfa-385418e2174e/google-wave.png" alt="Google Wave" />

With Wave, Google is pushing HTML5 as far as it will go (and even a little further). They are taking blogs, wikis, instant messaging, e-mail and synchronous communication to the next level by combining them into place.

<strong>Here is what the Wave inbox looks like.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c33f3e05-b6f2-4302-a2a0-3575c0bb2867/google-wave-inbox.png" alt="Google Wave" />

<strong>Below is a sort of wiki/chat area with all sorts of real-time communication treats for you to check out (once they release it).</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3beb0d-5aad-44d5-9803-18e44d1685bd/google-wave-inline-editing.png" alt="Google Wave" />

Google Wave being powered by HTML5 is definitely the biggest step forward we have seen in this area. They have done a phenomenal job putting together a creative and innovative product.</p>

### Focusing on the mobile

Just like Google is currently doing with Wave by selectively releasing it to developers, we can control the viewing environment when working with mobile devices. By grabbing the <a href="https://detectmobilebrowsers.mobi/">user agent</a>, we can design specific applications that use HTML5 for supported devices.

Targeting the user agent of a device is not an ideal method in designing for the general mobile web, but when we need to <strong>specifically target a device</strong>, like the iPhone, Pre or Google's Android it's a pretty solid option.

Right now, the best mobile testing platform we have is the iPhone. With the recent software upgrade, it is very close to having full support. But, if you just want to use the new elements, most any of the big 3 mobile platforms will work fine. If you're looking for API support I suggest testing on the iPhone with the new upgraded software.</p>

## Conclusion

With the strong foundations set up by previous versions of (X)HTML and large community activity surrounding <a href="https://www.webstandards.org/">Web standards</a>, we're coming into a new age with a wealth of knowledge and the ability to learn from our past mistakes (and make some new ones). HTML5 is being set up with the expectations of a very powerful markup language and it's up to us to utilize it in a way that can benefit us all.

There are so many great features to look forward to from new elements to tons of killer APIs. We can make data available offline, easily combine technologies and create very intricate animations all within a familiar landscape. If you have the time, I encourage you to browse through the <a href="https://dev.w3.org/html5/spec/Overview.html">entire spec</a> and familiarize yourself even further with all the bells and whistles (there are a lot) so we can use HTML5 to build stronger, richer Web applications for years to come.

<strong>Here's to HTML5, let's hope it lives up to the hype.</strong>

## Resources

*   23 Essential HTML 5 Resources A comprehensive list of articles and resources related to HTML 5. ![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1e6acc0-3087-45f7-a2f0-f39fc34096a2/ess.gif)
*   [HTML5 Demos](https://html5demos.com/) HTML5 Demos is a great resource for checking out the HTML5 APIs such as: geolocation, drag and drop, offline detection, and storage. This is a very good and unique resources to test out and see exactly with we can do with HTML5.[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7a544e-7a73-402d-9012-c7ef06b47137/1.jpg)](https://html5demos.com/)
*   [HTML5 Gallery](https://html5gallery.com/) The HTML5 Gallery, like any gallery, is a web site showcase where you can see how others are using HTML5 in every day development. I've looked round though this site quite a bit and did some cross browser testing on some of the entries. Many are broken in older browsers, but there are some that [hold up very well](https://www.design-this.co.uk/blog.htm). [![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3b37a7b-c62b-438f-87ad-76fd3f122c83/html5g.jpg)](https://html5gallery.com/)
*   [HTML5 Doctor](https://html5doctor.com/) A resource that catered for the people who wished to find out more about implementing HTML5 and how to go about it. This blog publishes articles relating to HTML5 and it’s semantics and how to use them, here and now.[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8970fa9d-6fcd-4e33-aa58-bfc83d0b5174/doctor.jpg)](https://html5doctor.com/)
*   [HTML5 Cheat Sheet](https://www.smashingmagazine.com/2009/07/06/html-5-cheat-sheet-pdf/) A handy printable HTML 5 Cheat Sheet that lists all currently supported tags, their descriptions, their attributes and their support in HTML 4\. Released here, at Smashing Magazine. [![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92ea70c3-9262-4592-83dd-935e17a32516/html5.gif)](https://www.smashingmagazine.com/2009/07/06/html-5-cheat-sheet-pdf/)
*   [W3C HTML5 Spec Overview](https://dev.w3.org/html5/spec/Overview.html) Whenever you want to know about something that no one has written about on the Web, the W3C is your answer. I spent hours scouring this site in researching HTML5\. It's a great resource and I highly recommend reading through whatever you can.
*   [HTML5 Validator](https://html5.validator.nu/) Even with such little support, we still want to make sure our code is valid. Validating your code is a great way to learn and ease yourself into developing with HTML5.
*   [WHATWG Wiki](https://wiki.whatwg.org/wiki/Main_Page) The [HTML Working Group](https://www.whatwg.org/) has put together some great documentation for tracking what exactly is going on in the world of HTML5.</p>

## References

*   [Yes, You Can Use HTML 5 Today!](https://www.sitepoint.com/article/html-5-snapshot-2009/)
*   [W3C HTML5 Differences](https://dev.w3.org/html5/html4-differences/)
*   [Preview of HTML5](https://www.alistapart.com/articles/previewofhtml5)
*   [Preparing for HTML5 with Semantic Class Names](https://jontangerine.com/log/2008/03/preparing-for-html5-with-semantic-class-names)
*   XHTML2 vs. HTML5
*   [HTML4 vs. HTML5](https://www.w3.org/TR/html5-diff/)
*   [Accessibility in HTML5](https://www.456bereastreet.com/archive/200706/html_5_and_accessibility/)
*   [HTML5 Doctor](https://html5doctor.com/)

