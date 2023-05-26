---
title: 'Native And PWA: Choices, Not Challengers!'
author: aarongustafson
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c585f48-c957-4b11-8270-422e8f513f01/laptop-pexels-photo-160107-opt.jpeg
date: 2018-02-09T14:00:34+01:00
slug: native-and-pwa-choices-not-challengers
summary: >-
  Deciding to build a PWA or a native app should be based on the needs of the specific project, not hype. In this article, Aaron Gustafson walks you through the pros and cons of each approach to help you arrive at an informed decision.
description: >-
  Deciding to build a PWA or a native app should be based on the needs of the specific project, not hype. In this article, Aaron Gustafson walks you through the pros and cons of each approach to help you arrive at an informed decision.
categories:
  - Native
  - PWA
  - Apps
---
It’s hard to tell exactly where the rift between "native" and "web" really started. I feel like it’s one of those things that had been churning just below the surface since the early days of Flash, only to erupt more recently with the rise of mobile platforms. Regardless, developers have squared off across this “great chasm,” lobbing insults at one another in an attempt to bolster their own side.

I have no interest in that fight. Sure, I’m a “web guy,” but that doesn’t mean I can’t see the appeal of native development; I’m also a software developer. Above all, though, I’m a pragmatist. I realize every project is different and that our approach to each should be tailored to the project’s needs and goals.

With [Progressive Web Apps (PWAs)](https://www.scnsoft.com/blog/progressive-web-apps) encroaching on native development’s turf, I thought this might be a good time to step back and take stock of these two approaches to building products. My hope is that we will all walk away with the ability to clearly see the strengths of each approach in hopes of finding the right fit for the products we create.

## A Rapid-Fire Comparison

Since pretty much the beginning, web-based experiences have been compared with everything from desktop software (the original ”native apps“) to interactive CD-ROMs to Flash and, most recently, to mobile apps. Despite being declared dead [on numerous occasions](https://www.wired.com/2014/01/death-pc-also-mean-end-web/), the web has persisted. In many cases, it’s even outlived its alleged killers (R.I.P. Flash).

One of the web’s chief strengths in this regard is its adaptability. It’s been able to go pretty much anywhere there’s an Internet connection and continues to gain new capabilities. All programming languages evolve, so it’s not unexpected, but over time the web’s growing borders have continued to encroach on traditional software’s turf.

{{% feature-panel %}}

One area where the web has historically come up short, however, has been in the realm of performance. Installed software is able to tie into the underlying operating system in ways the web simply can’t. They’re written in the *lingua franca* of their host, with direct access to the hardware or “closer to the metal” as we often say. The web, which nearly always operates one or more layers of abstraction above that, has had a hard time competing when it comes to performance. While the performance gap has narrowed over time, native code is likely to continue running faster than web code, at least until the web becomes capable of interpreting signals directly off the pins of the hardware.

Hand-in-hand with the performance advantage, native development has far greater (and earlier) access to device features such as NFC, Bluetooth, proximity and ambient light sensors, and more. The web is steadily gaining access to these features as well, but it will always lag behind native because the native APIs need to be developed before the web can tap into them and standardization across the browser-scape takes time.

Additionally, native code can hook into OS-level features like the address book and calendars. Push notifications was another big one, but [Service Workers](https://developer.mozilla.org/docs/Web/API/Service_Worker_API) now enable the web to take advantage of that feature as well. [Payment processing has similarly improved on the web recently](https://www.w3.org/TR/payment-request/). Perhaps address book and calendar access will come to the web eventually as well.

Circling back to Service Workers for a moment, this recent addition to the web developer’s toolbox has a number of other tricks up its sleeve, too. First of all, it offers a much more robust caching system than the web had previously with [AppCache](https://developer.mozilla.org/docs/Web/HTML/Using_the_application_cache). You can use Service Workers to manage offline requests, cache specific resources, sync data with a remote server when the user doesn’t even have the site open, and a ton more. Perhaps more than any other single technology, Service Workers have enabled the web to offer a more app-like experience.

Service Workers are one of [the three technical lynchpins of PWAs](https://adactio.com/journal/13098). Another one is the Web App Manifest. While it may sound a little boring, a [Web App Manifest](https://developer.mozilla.org/docs/Web/Manifest) is actually an incredibly powerful tool in that it enables a website to advertise itself as an app. This relatively straightforward JSON file format provides a wealth of information about the website it describes and enables PWA-aware browsers and operating systems to install the site as though it was native software.

Some [app stores are even beginning to index PWAs](https://www.thurrott.com/windows/windows-10/142649/microsofts-bold-plan-bring-pwas-windows-10), using their Manifest to populate their associated entries. From a user perspective, PWAs in app stores aren’t any different than the native apps surrounding them. They are installable, un-installable, and can even expose their settings to the underlying operating system’s app management tool. It’s also worth noting that PWAs don’t actually need a user to explicitly install them in order to use them because, well, they live on the web.

Being both on and of the web also means PWAs are always up to date. Users won’t need to actively download anything new to access new functionality. And even when new content and features do get rolled out, it’s highly unlikely a user would need to re-download your entire PWA as they would in the case of most native apps. If anything, they may get a few new assets and some new HTML, and it would happen pretty instantaneously, no app store required. Of course, you still have the discovery and distribution option provided by app stores, so really it’s the best of both worlds.

Being in app stores puts PWAs on equal footing with native apps in terms of discovery, distribution, and monetization. In fact, it may even vault the web over native as PWAs are also discoverable via search engines and are infinitely more shareable than apps because they exist at a URL. When well-built, PWAs are also interoperable across browsers, platforms, and devices. [PWAs even work in browsers that don’t support features like Service Workers](https://cloudfour.com/thinks/ios-doesnt-support-progressive-web-apps-so-what/), because PWA features are [progressive enhancements](https://alistapart.com/article/understandingprogressiveenhancement).

The web also offers very mature accessibility support, making it relatively easy to ensure your projects are usable by the broadest number of users. Complex interfaces do require a little more diligence when it comes to programming, but the accessibility benefits afforded by semantic HTML handle baseline accessibility with aplomb &mdash; especially when it comes to text-heavy, informational or simple form-based products. By contrast, you nearly always need to be aware of and incorporate accessibility APIs into your native code.

On the topic of development, I don’t think there’s a clear winner when it comes to development experience. Every language has its fans, and the same can be said for developer tools. You like what you like, and you tend to be more efficient with the tools and languages you know and are passionate about. Neither the web nor native development has any distinct advantage there.

Where native development does shine, however, is when it comes to ensuring a consistent level of quality for UIs, built using their SDKs (Software Development Kits). Most native SDKs offer tools for testing performance, design, functionality, and more. They also include boilerplate code, design systems, and other tools that help raise the overall bar of native software offerings. Sure, there are similar tools for the web, but they are scattered across the web and aren’t universal across all of the different development environments folks use to build websites. There is no single entity defining quality web experiences and providing the tools to build them (though many have tried).

{{% ad-panel-leaderboard %}}

When it comes to staffing the development of a product, it’s definitely easier to hire folks who know how to build for the web. As I type, the [Programming Language Index](https://web.archive.org/web/20171127050313/https://langpop.corger.nl/) currently ranks JavaScript as the most popular language, with Java right behind it. C# is in 5th place, HTML in 7th, CSS in 9th, and Swift comes in 15th. This index cross-references Stack Overflow tags with lines changed in public repositories on GitHub, so it should be taken with a grain of salt, but it provides a pretty clear indication that many folks know (and use) web technologies. On the flip side, it can often be challenging to find and hire talented native developers because there are fewer of them and they are in high demand.

Scarce talent means you’ll likely end up paying more for native development. Every project is obviously different and has different features and requirements, but it can be illustrative to look at average development costs as a comparison. Comentum suggests that [building a moderately-sized web app ranges from under US$10,000 to US$150,000](https://www.comentum.com/web-development-cost-rate-comparison.html). On the native end, Appster estimates that [moderately-sized mobile app projects cost between US$110,000 and US$305,000 to build](https://www.appsterhq.com/blog/app-development-cost/). It’s probably safe to assume native projects are likely to cost about twice as much to develop as a web project. And that’s per platform. Native apps also [typically take longer to develop](https://mashable.com/2012/09/12/web-vs-native-apps/).

It’s worth noting that there are options for building native software using web technologies without building a PWA. Frameworks like [React Native](https://facebook.github.io/react-native/), [PhoneGap](https://phonegap.com/), [Ionic](https://ionicframework.com/), and [Appcelerator Titanium](https://www.appcelerator.com/mobile-app-development-products/) enable you to generate native code from HTML, CSS, and JavaScript. Using one of these tools could lower your staffing and development costs when compared with hiring a team of native developers, but in terms of access to device features your project will be limited to the ones the framework has implemented. Plan accordingly.

Once the app is developed, you also have to account for ongoing maintenance costs of said app or apps. In response to a survey run by Clutch, Dom & Tom recommends [budgeting 50% of the product’s initial price in the first year, 25% in the second year, and between 15-25% for every year after](https://clutch.co/app-developers/resources/cost-build-mobile-app-survey).

Once you have a decent grasp on how web and native development compare and contrast, you can begin to assess which strengths and weaknesses are relevant to your project. You’ll likely have to make some tradeoffs, and that’s to be expected. There is no one-size-fits-all solution. And if there was, [it wouldn’t fit anyone well](https://cheezburger.com/6582709504).

Let’s run through a couple of hypothetical projects to bring the distinctions between development for native and PWA more clearly into focus.

### Project #1: An Existing Native App

Let’s say you’ve already gone through the process of building out a native app. If everything is going well, there’s no reason to change course. Don’t throw out all of your existing work to switch over to a PWA unless you have a really good reason to do so. I can only really think of one scenario that might warrant considering a switch to PWA: Bringing support for a new OS into the mix. And even then, it only really makes sense if your app’s needs can be met by the web alone.

If you are adding support for a new platform to a product, it creates the perfect opportunity to evaluate the needs and goals of the project with regard to the cost of meeting those needs. If the web isn’t up to the task, stick with native. If it is, however, pause and consider this: Adding support for the new platform using a PWA would allow you to support additional platforms (including the web) down the road and could even enable you to replace your existing native application once the PWA has been thoroughly tested.

If replacing an existing native app with a PWA seems unthinkable to you, consider this: [Starbucks](https://formidable.com/work/starbucks-progressive-web-app/) and [Twitter](https://blog.twitter.com/engineering/en_us/topics/open-source/2017/how-we-built-twitter-lite.html) are already exploring this idea.

If there are specific reasons you need to keep your apps native, it can still worth considering “outsourcing” certain app features to the web. A few years back, I was working on a project for a large financial services firm, and they opted to move the login flow for their native apps to the web in order to enable them to roll out security features more quickly than the typical app store approval process enabled them to achieve. Perhaps your project has similar needs that the web could empower your native app to meet.

{{% ad-panel-leaderboard %}}

### Project #2: An Existing Cross-Platform App

If you’ve got an existing app that works cross-platform, you”re likely shelling out a lot of money for the ongoing development and maintenance of that app. You’re also likely seeing some divergence in-app features as each native platform tends to have its own development timeline. The app for the retailer Target, for instance, currently allows users to manage a shopping list on iOS, but the Android version doesn’t have that feature. In many ways it’s similar [to the divergence we sometimes see between the “desktop” and “mobile” versions of a website](https://www.creativebloq.com/separate-mobile-website-no-forking-way-8124169).

If the web is already part of your cross-platform mix, it provides a good opportunity to double down on your investments there and consider replacing your native apps with PWAs. Tools such as [sonar](https://sonarwhal.com/) and [Lighthouse](https://developers.google.com/web/tools/lighthouse/) can give you insight into how well-prepared your existing site is for PWA-ification and they can also tell you what you need to work on. From there, turning your website into a PWA is relatively straightforward. There are even free tools that can help you [upgrade your site to a PWA in a few short minutes](https://www.pwabuilder.com/). If it’s not, however, there’s really not much incentive to make this move unless the feature divergence between platforms becomes really egregious or you are considering adding yet another native platform (or the web) into the mix.

### Project #3: A New Cross-Platform Product

If you’re kicking off a new project aimed at more than one platform, creating and maintaining it in one place as a PWA should definitely be on the table. Depending on your budget and staff, it’s likely to stretch your budget the furthest. That said, if your product requires a direct connection to hardware or the underlying OS, you may still need to go native. But before you go that route, make a list of all of your requirements and then verify [what the web can do](https://whatwebcando.today/) (and what it can’t). Be sure to [check for support in more than one browser too](https://caniuse.com/).

### Project #4: A New Hyper-Focused Product

If you are building a new product and part of that product’s whole purpose is its deep connection to a particular platform, by all means, build for that platform. For instance, if your product relies on Apple’s Messages platform or integration with HomeKit, by all means, build for iOS and/or macOS in Swift. If your product will best meet user needs via a widget or you’re building a custom launcher, you’re best off building Android, and you’ll need to use Java.

Not all native features are walled gardens, however. While Amazon’s Alexa, Apple’s Siri, and the Google Assistant all require native code (or a JSON API) to integrate with your app, interestingly Microsoft’s [Cortana will voice-enable your PWA using only an XML file linked from the `head` of your HTML](https://gist.github.com/seksenov/17032e9a6eb9c17f88b5). Perhaps others will follow their lead.

## PWA Or Native? The Choice Is Yours

The web and native each have a lot to offer. If you were to ask me which is better, I’d simply reply “It depends” because it does. I’m not being evasive or noncommittal; figuring out which is the right fit for your project depends entirely on the specific needs of your project. It requires taking into consideration what you are building, the composition of the existing team tasked with building it or the team you will need to hire to do so, and the budget you have to work with. In many cases, the web likely offers everything you need to accomplish your project’s goals, but there are always exceptions. If you want to explore the possibilities the web offers, I’ve included some resources at the end of this article.

The most important thing you can do when weighing different approaches to software development &mdash; or different frameworks, libraries, languages, design systems, etc. &mdash; is to consider your options in relation to the project at hand. Do your research and weigh your options. And don’t allow yourself to be swayed one way or another by clever marketing, sexy demos, or rabid fanboys. Including this one.

### PWA-Related Resources
- [PWA Builder](https://www.pwabuilder.com/)  
A 3-step website-to-PWA creation tool with helpful recommendations and recipes. It also enables you to turn your PWA into installable native apps for Windows, Android, and iOS.
- [A Progressive Road Map for your Progressive Web App](https://cloudfour.com/thinks/a-progressive-roadmap-for-your-progressive-web-app/)  
Jason Grigsby on how his team began incorporating aspects of PWAs into their website over the course of several months, nicely demonstrating how the different features can be added a bit at a time.
- [Yes, That Web Project Should Be a PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa)  
An overview of the UX opportunities (and risks) of PWAs, written by yours truly.
- [Progressive Web Apps on MDN](https://developer.mozilla.org/en-US/Apps/Progressive)  
A hub for all of the technical bits you need to know about what characterizes a quality PWA.
- [What Web Can Do Today](https://whatwebcando.today/)  
Take a look at the APIs your device, OS, and browser support. What you find might surprise you.
- [Can I Use](https://caniuse.com/)  
The definitive database of what APIs and features are available in every major browser and how that support measures up relative to the browsers people are actually using. It can also give you an excellent view back in time to see how backward compatible certain features are.

{{< signature "rb, ra, hjc, il" >}}

