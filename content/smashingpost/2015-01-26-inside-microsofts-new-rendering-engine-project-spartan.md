---
title: 'Inside Microsoft’s New Rendering Engine For The “Project Spartan”'
slug: inside-microsofts-new-rendering-engine-project-spartan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf974b02-727f-4162-96ce-d6ec95eb5ade/ie-preview-snippet-illu-opt.png
date: 2015-01-26T18:00:09.000Z
author: jacobrossi
summary: >-
  This article will cover the inside story of the rendering engine powering Spartan, how it came to be, and how 20 years of the Internet Explorer platform (Trident) has helped inform how it was designed.
description: >-
  This article will cover the inside story of the rendering engine powering Spartan, how it came to be, and how 20 years of the Internet Explorer platform (Trident) has helped inform how it was designed.
categories:
  - Coding
  - Browsers
  - Internet Explorer
---
**Editor’s Note**: *Last week, Microsoft made its biggest announcement for the web since it first introduced Internet Explorer in 1995: a new browser, codenamed “<a href="https://blogs.msdn.com/b/ie/archive/2015/01/22/project-spartan-and-the-windows-10-january-preview-build.aspx">Project Spartan</a>.” So, what does this mean for us as designers and developers? What rendering engine will Spartan be using, and how will it affect our work? We spoke with Jacob Rossi, the senior engineer at Microsoft's web platform team, about the new browser, the **rendering engine** behind it, and whether it's going to replace Internet Explorer in the long run. This article, written by Jacob, is the result of our conversations, with a few insights that you may find quite useful.*

[Spartan](https://blogs.msdn.com/b/ie/archive/2015/01/22/project-spartan-and-the-windows-10-january-preview-build.aspx) is a project that has been in the making for some time now and over the next few months we’ll continue to learn more about the new browser, what it has to offer users, and what its platform will look like. It will be a matter of few months until users and developers alike will be able to try Spartan for themselves, but we can share some of the interesting bits already today. This article will cover the **inside story of the rendering engine powering Spartan**, how it came to be, and how 20 years of the Internet Explorer platform (Trident) has helped inform how our team designed it.

{{< rimg href="https://blogs.msdn.com/b/ie/archive/2015/01/22/project-spartan-and-the-windows-10-january-preview-build.aspx" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23aa6df4-267a-4094-adc0-1ba77edf92a3/spartan-1000px.jpg" sizes="100vw" caption="Project “Spartan”, a new browser by Microsoft, was officially announced last week. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23aa6df4-267a-4094-adc0-1ba77edf92a3/spartan-1000px.jpg'>Large preview</a>)" alt="Project “Spartan”, a new browser by Microsoft." >}}

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2011/11/but-the-client-wants-ie-6-support/">But The Client Wants IE 6 Support!</a></em></p>

{{% feature-panel %}}

## Lessons Learned From Internet Explorer

Twenty years ago, Microsoft first introduced Internet Explorer to the world. For many users, it’s a household name and a brand recognized across the globe, but for web developers, those quirky older versions of Internet Explorer often make it difficult to recognize Microsoft's recent efforts in supporting and implementing web standards. Though Internet Explorer's legacy versions are likely to be remembered by web developers for bugs, hacks and dirty workarounds, <a href="https://www.nczonline.net/blog/2012/08/22/the-innovations-of-internet-explorer/">IE did shape the web in a positive way</a> for web developers by bringing CSS, dynamic HTML scripting and the DOM, AJAX/XMLHttpRequest, drag drop, innerHTML, hardware acceleration, and other technologies to the web.

On the browser team at Microsoft, we consider ourselves a learning organization. Each year, we take the time to reflect on our achievements and our failures to learn and grow. From that, each release of IE has made a lasting impact on how we engineer. Our learnings about the importance of cooperation amongst browser vendors, standards, compatibility, interoperability, performance, and security all come together to shape how we designed our new rendering engine.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2016/10/whats-the-deal-with-the-samsung-internet-browser/">What’s The Deal With The Samsung Internet Browser?</a></em></p>

## Microsoft’s New Rendering Engine

The new Microsoft browser is going to be powered by a new rendering engine, _EdgeHTML.dll_. Windows 10 already has it integrated, and it will be separate from Trident (MSHTML.dll) that powered Internet Explorer for decades.

As we know, the latest versions of Trident powering Internet Explorer 11, did show a remarkable support for standards (I started to make <a href="https://gist.github.com/jacobrossi/044ea8ad3b0165e46eaf">a list</a> of some of the notable ones, but stopped after I hit 75 specs). But its progress was heavily weighed down by the burden of legacy support for IE5.5, IE7, IE8, IE9, and IE10 document modes — a concept the web no longer needs.

So we set about to create a new engine **using IE11’s standards support as a baseline**. I watched Justin Rogers, one of our engineers, press "Enter" on the commit that forked the engine—it took almost 45 minutes just to process it (just committing the changes, not building!). When it completed, there was a liberating silence when we realized what this now enabled us to do: delete code, every developer’s favorite catharsis.

In the coming months, swathes of IE legacy were deleted from the new engine. Gone were document modes. Removed was the subsystem responsible for emulating IE8 layout quirks. VBScript eliminated. Remnants like attachEvent, X-UA-Compatible, currentStyle were all purged from the new engine. The codebase looks little like Trident anymore (far more diverged already than even Blink is from WebKit).

<a href="https://blogs.msdn.com/b/ie/archive/2015/01/22/project-spartan-and-the-windows-10-january-preview-build.aspx"><img style="max-width: 100% !important;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c9191f-35e7-4038-a44c-fb0fc697d69a/spartan-scheme.jpg" srcset="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c9191f-35e7-4038-a44c-fb0fc697d69a/spartan-scheme.jpg 500w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e42d645-17e9-41c6-8c39-09e5c985dd18/spartan-scheme-large.jpg 739w" alt="Project Spartan" width="500" height="281" /></a><br>
_Project Spartan will be powered by a new rendering engine and the Chakra JavaScript engine, introduced with IE 9._

What remained was a clean slate. A modern web platform built with interoperability and standards at its core. From there, we began a major investment in interoperability with other modern browsers to ensure that developers don't have to deal with cross-browser inconsistencies. To date, we’ve fixed over 3000 interoperability issues (some dating back to code written in the 90’s) on top of the <a href="https://status.modern.ie/?iestatuses=indevelopment,iedev">over 40 new web standards</a> we’re working on. For example, longstanding innerHTML issues are now fixed. Even recent standards, like Flexbox, are getting renewed love so that the new engine matches the latest spec (this will show up in a future Windows 10 preview build). Project Spartan will also have an **updated version of the F12 developer tools**. A few of my personal favorites that are in the preview builds or on their way:

*   Preserve-3d
*   The most [advanced support for ES6](https://kangax.github.io/compat-table/es6/ ) at the moment
*   XPath
*   Web Audio
*   Media Capture API
*   Web RTC 1.1 (ORTC)
*   Touch Events
*   Content Security Policy
*   HTTP/2

As it turns out, a modern and interoperable rendering engine alone isn’t enough to magically make the web just work. To do that, the browser also has to make sure that sites provide the browser with the up-to-date, "modern browsers" code. So our new engine also comes with a **new user agent string**. If user agent string tokens were stickers, then the new engine’s UA String looks like the backs of most web devs laptops these days. But this yields surprisingly positive results in compatibility and enables lots of sites to send our new engine modern content. It also gives me one more opportunity to beat the drum again: **user agent sniffing should be avoided at all costs**!

{{% ad-panel-leaderboard %}}

### "That’s great, but my company has sites that require IE8."

In order to ensure that we also retain backwards compatibility, we will not be getting rid of Trident. Instead, we designed and implemented a dual-engine approach, where either the new modern rendering engine or Trident can be loaded. This switch happens transparently to the user. Windows 10 will use EdgeHTML for the web (so no more worrying about doc modes) and only load Trident for <a href="https://blogs.msdn.com/b/ie/archive/2014/04/02/stay-up-to-date-with-enterprise-mode-for-internet-explorer-11.aspx">legacy enterprise sites</a>. This dual-engine approach enables businesses to update to a modern engine for the web while running their mission critical applications designed for IE of old, all within the same browser. Even better, with the dual-engine approach we can ensure that only essential security fixes are made to Trident, minimizing code churn and ensuring that compatibility is preserved for enterprise sites, while we focus on innovating in the new (and always up to date) rendering engine untethered.

Spartan is the browser we expect people will be using on Windows 10. That said, there are a set of businesses that have built key tools on top of Internet Explorer’s legacy extensibility model (e.g. custom ActiveX, toolbars, browser helper objects, etc.). So, Internet Explorer will be made available on Windows 10 for some enterprise web applications that require a higher degree of backward compatibility. This version of Internet Explorer will use the same dual-engine approach as Spartan with EdgeHTML the default for the web, meaning developers won't need to treat Internet Explorer and Spartan differently and our <a href="https://status.modern.ie">standards roadmap</a> will be the same. The browser will be powered by the <a href="https://blogs.msdn.com/b/ie/archive/2012/06/13/advances-in-javascript-performance-in-ie10-and-windows-8.aspx">Chakra JavaScript engine</a>.

### "That’s great, but some of my users still have IE8."

We hear you. What’s painful for web devs to support is also painful for our browser team. Back in May, we talked about getting our users upgraded as <a href="https://blogs.msdn.com/b/ie/archive/2014/05/27/launching-status-modern-ie-amp-internet-explorer-platform-priorities.aspx">a top priority</a>. Later in August, we announced a <a href="https://blogs.msdn.com/b/ie/archive/2014/05/27/launching-status-modern-ie-amp-internet-explorer-platform-priorities.aspx">browser support policy</a> that will encourage users to get up to date. Most significantly, we announced last week that Windows 10 will be a <a href="https://blogs.windows.com/bloggingwindows/2015/01/21/the-next-generation-of-windows-windows-10/">free upgrade</a> to customers running Windows 7, Windows 8.1, and Windows Phone 8.1 who upgrade in the first year after launch. Furthermore, we’ll treat Windows 10 as a service—keeping users up to date and delivering features when they are ready ("auto-update"), not waiting for the next major release. This means the **new rendering engine will always be truly evergreen**.</p>

{{% ad-panel-leaderboard %}}

## The Roadmap Ahead

Another welcomed change that we’ve been rolling out over the past year is a promise for increased openness about our web platform plans and roadmap. Over the last year, you’ve hopefully experienced some of this through our <a href="https://status.modern.ie">open standards roadmap</a> (one of my personal side projects), our <a href="https://www.reddit.com/r/IAmA/comments/2dk60t/we_build_internet_explorer_i_know_right_ask_us/">Reddit AMA</a>, regular dialog through <a href="https://twitter.com/iedevchat">@IEDevChat</a>, and sharing <a href="https://insider.windows.com/">preview builds</a> very early in our development process. You’ll see more of this over the next year.

For standards support, we will maintain a pipeline of new features we’re working on. What’s ahead in the near future are Web Audio, Image srcset, @supports, Flexbox updates, Touch Events, ES6 generators, and others that have all seen commits in the recent weeks. What lies beyond are big ticket items like Web RTC 1.1 (ORTC) and Media Capture (getUserMedia() for webcam/mic access). Beyond that, we’re starting to use <a href="https://uservoice.modern.ie/">your input</a> (and other factors, such as real world usage data gathered through the Bing crawler, which now can run our new engine) to shape how we prioritize our next platform investments.

Our plans for the platform in the initial release aren’t fixed—developer feedback has and will continue to shape it. So please expect agile changes. Here’s what you can do to get ahead:

*   **Test out the new engine**.  EdgeHTML can be enabled today within Internet Explorer in the [Windows 10 Technical Preview](https://preview.windows.com) (a preview of Project Spartan will come later) by navigating to `about:flags` and enabling “Experimental Web Platform Features.” If you’re on a Mac or don’t have a machine you can upgrade to Windows 10 preview builds yet, there’s the recently launched RemoteIE cloud service that lets you stream a version of IE running the new engine without downloading large virtual machine images (note: we’re still in the process of rolling out the last week’s preview build to RemoteIE).
*   **File bugs**.  Our investment in interoperability with modern browsers is fueled by data from [bug reports](https://connect.microsoft.com/ie) and real world site impact.
*   Feel free to monitor and give us feedback on our standards roadmap – based on [developer feedback](https://uservoice.modern.ie) over 40 different standards have gone from “under consideration” to in development since we launched our [open roadmap](https://status.modern.ie) back in May 2014.

Personally, I’m excited to share this inside scoop on the new web rendering engine powering Project Spartan in Windows 10 so early in our development process. We look forward to sharing more of our plans and in the coming months. In the meantime, if you have feedback, <a href="https://twitter.com/jacobrossi">reach out to me</a> and the <a href="https://twitter.com/iedevchat">rest of our team</a>. Let’s make the web work for you.

{{< signature "rb, vf, il" >}}