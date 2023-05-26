---
title: How To Establish An Open Device Lab For Better Mobile Testing
slug: establishing-an-open-device-lab
image: >-
  https://www.smashingmagazine.com/inspiration/2014/04/11/get-excited-about-emotional-branding/attachment/why-you-should-get-excited-about-emotional-branding-mystery-series-illus-jpg-3/attachment/devicewall-500/
date: 2012-09-24T08:04:35.000Z
author: viljami-salminen
description: >-
  Managing a personal device lab can be quite hard with an ever expanding number
  of devices. It’s not only expensive, but also bad for our environment. Think
  of a situation where every web developer would purchase a large pile of
  gadgets and keep adding new ones as they are launched — this wouldn’t make
  much sense. Thankfully, there are better ways to handle the problem.

  During the spring of 2012, Jeremy Keith wrote on his website that anybody is
  welcome to visit their device lab at Clearleft’s office in Brighton, UK and
  use their devices. What they didn’t expect, though, was that in response many
  local developers offered to add their own devices to the collection as well.
  Two weeks later Jeremy Keith and Remy Sharp also presented this idea at the
  Mobilism conference in Amsterdam and the people attending loved it. A few
  months after Mobilism, similar labs started popping up in places like
  Amsterdam, Berlin, London and Malmö.
categories:
  - Mobile
  - Testing
  - Devices
  - Responsive Design
---
Managing a personal device lab can be quite hard with an ever expanding number of devices. It’s not only expensive, but also bad for our environment. Think of a situation where <em>every</em> Web developer would purchase a large pile of gadgets and keep adding new ones as they are launched — this wouldn’t make much sense. Thankfully, there are better ways to handle the problem.

During the spring of 2012, Jeremy Keith <a href="https://adactio.com/journal/5433/">wrote on his website</a> that anybody is welcome to visit their <a href="https://clearleft.com/testlab/">device lab</a> at Clearleft’s office in Brighton, UK and use their devices. What they didn’t expect, though, was that in response many local developers offered to add their own devices to the collection as well. Two weeks later Jeremy Keith and Remy Sharp also presented this idea at the Mobilism conference in Amsterdam and the people attending loved it. A few months after Mobilism, similar labs started popping up in places like Amsterdam, Berlin, London and Malmö.

You may also want to take a look at the following related posts:

*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Open Device Labs: Why Should We Care?](https://www.smashingmagazine.com/2013/05/open-device-labs-why-should-we-care/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)

Following this example, we decided to bring our own devices to the <a href="https://kiskolabs.com/">Kisko Labs</a> office and do the same thing in Helsinki. We now have an open device lab where anyone can come, start using the devices and contribute by lending their old devices. Three weeks after establishing this we already have three new devices from the local community: a Nokia N900 running Maemo, a Nokia Lumia 800 running Windows Mobile and an HTC Desire HD running Android. I have also been in contact with the device manufacturers and so far at least Nokia, <a href="https://www.hpwebos.com/us/">Palm</a> and <a href="https://developer.sonymobile.com">Sony</a> have promised to help us out with the lab.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async"  class="alignnone" title="Open Device Lab" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9edb3a98-d348-46bc-8ea3-283b1fc41367/helsinki-lab-500.jpg" alt="Open Device Lab" width="500" height="232" /><figcaption>Helsinki Open Device Lab, devicelab.fi.</figcaption></figure>

I encourage everyone to do the same thing in the city they live in as well. This article will cover most of the things needed to be considered when doing that. It will also work as a guide and give practical tips — things like location, how to get devices, what devices to get and what software to use. At the end of the article is also a list of all the current open device labs around the world.</p>

## Location

This is probably the hardest part as it should be relatively open, easily accessible, but also a safe location to prevent burglars. I wouldn’t be too worried though as that’s a risk you need to take with any office space that’s filled with desktop computers and other gadgets. Just make sure that the space has proper locks and an alarm system in place.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4ea8cb0-7f77-40fa-8d74-8833b167b82a/mozilla2-500.jpg" alt="Mozilla’s workspace in London" width="500" height="324" /><figcaption>Mozilla’s workspace in London. Image by <a href="https://www.flickr.com/photos/mozillaeu/">@mozillaeu</a>.</figcaption></figure>

Finding a location was never a problem for us as we had a space at the office which wasn’t used that often, but I understand that it might be hard to find one unless you already work in a location like that. However, I imagine that the best places to start asking are local Web community meet-ups, conferences and Twitter. Find out about local co-working spaces too, as those could be the best candidates to host these kind of projects. I also asked <a href="https://twitter.com/shaundunne/">Shaun Dunne</a> (who established the London Device Lab) if he had any advice on how to find a space, and this is what he answered:
<blockquote>"I was in the <a href="https://www.reasonstobeappy.com">Reasons to be Appy</a> conference during April when <a href="https://christianheilmann.com">Christian Heilmann</a> mentioned Mozilla’s new London office and how it had a co-op space with free WiFi for anyone to use. I spoke to him after his talk and mentioned what I was trying to do and he said that he thought Mozilla would be more than happy to host it. He said I should speak to <a href="https://twitter.com/cyberdees">@cyberdees</a> who runs things in the office. We exchanged a few emails and I went there a couple of times and it was born from there."</blockquote>

## Devices

You don’t need a huge collection of devices to establish a lab — it can initially be small and grow once other developers start contributing their devices. Some device manufacturers are also willing to help the community by providing test devices for initiatives like this, so you should definitely contact them too.

There are basically four main areas that need to be covered in the lab. These are: feature phones, smartphones with low level support, smartphones and tablets. Later on you might also want to consider adding a Smart TV and other more exotic devices like <a href="https://www.alistapart.com/articles/testing-websites-in-game-console-browsers/">game consoles</a>. Additionally, the lab should also efficiently cover <a href="https://viljamis.com/blog/2012/responsive-workflow/#device-diagram">various screen sizes</a> between 240 x 320 and 1280 x 800 pixels, as well as some high-DPI variants.</p>

<figure><span class="removed_link" title="https://phonegap.com/2012/03/29/phonegaps-new-device-wall/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57f70258-ea2c-4c87-abc7-6ca473588027/devicewall-500.jpg" alt="PhoneGap’s Device Wall" width="500" height="332" /></span><figcaption>PhoneGap’s <span class="removed_link" title="https://phonegap.com/2012/03/29/phonegaps-new-device-wall/">Device Wall</span>. Photo © 2012 Adobe Systems Inc.</figcaption></figure>

<a href="https://twitter.com/dblooman">David Blooman</a> from BBC <span class="removed_link" title="https://mobiletestingfordummies.tumblr.com/post/20056227958/testing">recently shared</span> the process that they use while testing on mobile devices, and the minimum set of devices to get the job done. This list is a slightly modified version of their minimum test device stack. For now it is a good starting point for anyone who is thinking about setting up an open device lab:

*   iOS 5 — iPhone 4
*   iOS 6 — iPad 3 Retina
*   Android 2.2 — HTC desire
*   Android 2.3 — Huawei U8650
*   Android 2.3 — Kindle Fire (Silk browser)
*   Android 3.X — Motorola Xoom
*   Android 4.X — Samsung Galaxy Tab 2
*   Blackberry OS 5 — Curve 8900
*   Blackberry OS 6 — Bold 9700
*   Windows Phone 7.5 — Lumia 800
*   Symbian S40 — Nokia 2700
*   Symbian S60 — Nokia N95
*   Symbian Belle — Nokia 500

<strong>Remember:</strong> You will want to end up with a collection that represents the audience and overall market share in your own location, which might be different from what I have listed here. Stephanie Rieger, who is a co-owner of <a href="https://yiibu.com">Yiibu</a>, has written an excellent article explaining Strategies for choosing test devices (so be sure to read that to find out more about the subject). Dave Olsen has also written an article about <a href="https://www.dmolsen.com/mobile-in-higher-ed/2012/06/26/how-to-build-a-device-lab-part-1/">how to build a device lab</a>, where he explains how and why they decided to get certain devices.
<blockquote>"If I had to start from nothing, I would start with the phone in my pocket. After that, I would take the usual suspects — Android 2.3, iOS5, etc., and make sure to have the more popular phones in place, but not go overboard. One of each to begin with, and then more varieties as time goes on. In a good way, everyone’s device lab should be different, as every market is going to have variations. There is no golden list of devices."

— David Blooman</blockquote>

## How To Contact Device Manufacturers

*   You will need to have a space and a website (a single-page website is fine) for the lab before asking for any devices. Otherwise, it may be hard to look convincing.
*   Twitter and email seem to be the best way. Look for developer relations accounts [like this](https://twitter.com/shaundunne/lists/oem-relations/members) from Twitter and send emails to their developer related addresses. You can find the addresses from the developer websites, which usually reside in an URL formed like this: developer.manufacturer.com.
*   Ask people on Twitter if they know someone who works at one of the companies you are trying to contact. It may be an easier way to begin communicating with the right people.
*   When sending emails, explain carefully what the project is about, what you need and why you need it. It’s good to keep it short and get straight to the point.
*   Remember that you are sending emails to other human beings, not to some random corporations.
*   If you don’t get any answer from them within two weeks try to contact another person from that manufacturer.
*   Last but not least: Don’t be afraid to ask for help. I contacted several people about their test devices and where they got them from. Shaun Dunne (from the London Device Lab) was also kind enough to provide his perspective on how to contact the manufacturers:

<blockquote>"I started hitting the developer relations people up on Twitter. BB and Palm got back to me via Twitter and an email conversation went on from there. Nokia had their developer relations person at <a href="https://mobilism.nl">Mobilism</a>, so I found out his email and sent him an email directly. It’s about being persistent, really, email is hard because it could end up in their spam or they can ignore it."

"In a public forum like Twitter it’s harder for them not to engage. Don’t just go after the hardware manufacturers either, it’s worth speaking to the Android + WP7/8 people to see what they can do for you. If they want people to develop applications and websites that work on their devices, then it’s in their best interests to get those devices in developers' hands. The best and easiest way to get the devices in their hands is through a community lab."</blockquote>

## Setting Up The Lab

You don’t need much in the beginning: a table, a few chargers and a Wi-Fi connection is all you need to get things up and running. If you have more than five devices, it may be a good idea to get a <a href="https://www.amazon.co.uk/Trust-Port-Usb-2-0-Power/dp/B001UE6OC8">USB hub</a> which can provide power to avoid cable clutter and <a href="https://www.theironmill.co.uk">stands</a> where you can put the devices on. A few of the labs have also built their own stands and you can get some ideas from the resources listed below.

Jeremy Keith also told me that they have all the devices running through a wall socket that’s on a timer which switches the power off in the evening and nighttime and back on again in the morning. That might be useful for saving some energy and also to keep the batteries healthy.</p>

<figure><a href="https://www.64digital.co.uk/blog/66/the-64-digital-super-dooper-device-testing-station"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/948f19eb-c575-4747-8942-ca5e6e00a0a1/64digital-500.jpg" alt="64 Digital’s device testing station" width="500" height="332" /></a><figcaption>64 Digital’s <a href="https://www.64digital.co.uk/blog/66/the-64-digital-super-dooper-device-testing-station">device testing station</a>. Photo © 2012 64Digital.</figcaption></figure>

Later on, when there are many more devices in the lab, you may want to start considering getting a better wireless router which can handle all the devices. <a href="https://twitter.com/klick_ass">Andre Jay Meissner</a> told me that Apple’s Airport Extreme can handle up to around 30 devices, but not much more (it claims to support 50!). SIM cards with data plans are also something which you might need once you start adding older devices that exclude Wi-Fi.

*   [64 Digital’s Device Testing Station](https://www.64digital.co.uk/blog/66/the-64-digital-super-dooper-device-testing-station)
*   [Clearleft’s Laboratory Conditions](https://adactio.com/journal/5661/)
*   [Anna Debenham’s Sketches for the Clearleft Lab](https://www.flickr.com/photos/adactio/7801326422/in/photostream)
*   [Animoca’s iOS Testing Wall](https://techcrunch.com/2012/05/11/this-is-what-developing-for-android-looks-like/)
*   [How to Build a Device Lab [Part 1]](https://www.dmolsen.com/mobile-in-higher-ed/2012/06/26/how-to-build-a-device-lab-part-1/)
*   [Need: Multi-Device Stand for Mobile Web Development](https://klick-ass.com/awesomeness/need-multidevice-stand-for-mobile-web-development/)
*   [Handmade Phone and Tablet Stands by The Iron Mill](https://www.theironmill.co.uk): These are the same stands used by both Clearleft and ourselves. The website doesn’t really say it, but you can order them from anywhere in the world, just send a direct email to the contact address and ask for a delivery price.</p>

## Software Tools To Get You Started

*   [Adobe Shadow](https://labs.adobe.com/technologies/shadow/): Probably one of the best tools for testing at the moment. It allows device pairing, synchronous browsing and remote inspection using [Chrome extension](https://support.google.com/chrome/bin/answer.py?hl=en&answer=154007) on either Mac or Windows. To be able to use Adobe Shadow you will need to download and install the mobile client to all test devices. In addition, you will also need the Google Chrome extension to run Shadow on your laptop.
*   [JS Bin](https://jsbin.com): JS Bin is a Web app specifically designed to help JavaScript and CSS folks test snippets of code, within some context, and debug the code collaboratively. You can use JS Bin together with the Adobe Shadow mentioned earlier.
*   [xip.io](https://xip.io) xip.io is a domain name that provides wildcard DNS for any IP address. You can use these domains to access virtual hosts on your development Web server from devices on your local network (like iPads, iPhones, and other computers).
*   [Showoff.io](https://showoff.io), Localtunnel, [Proxylocal](https://proxylocal.com): For sharing your localhost over the Web.
*   Mobile browsers: Remember to install various browsers like Opera Mobile, Opera Mini, Chrome and Firefox to all of your supported test devices.</p>

<blockquote>"Be sure to track the OS versions found on your test devices, and think carefully each time you upgrade. Owning four BlackBerry devices with four different versions of the OS is infinitely more valuable than owning four with the same version."

— "Strategies for choosing test devices" by Stephanie Rieger.</blockquote>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc1a2dbb-75be-4440-bc52-19436114bfd0/shadow-500.jpg" alt="Adobe Shadow running on multiple devices" width="500" height="281" /><figcaption>Adobe Shadow running on multiple devices. Photo © 2012 Adobe Systems Inc.</figcaption></figure>

## Maintenance

There are some running expenses — rent, Wi-Fi, personal time used — and you may initially need to spend a few hundred bucks to provide chargers, wires and stands for the devices. So it’s worth considering if a small monthly payment would be acceptable. As it also might not be possible to find a space which is completely open like the one in London, it’s possible to have everything available by appointment too. This seems to be quite common practice and it allows you to use the same space for your own workshops as well, if needed.

In the beginning, when you are setting up the lab, I wouldn’t worry about all of this though. It’s possible that the lab will get popular and have lots of visitors and that someone might be using the devices when someone else comes in, but only time will tell. Shaun Dunne also said that they were discussing this very same problem in the beginning and decided finally that the lab should just be open. Jeremy Keith seems to think in a similar manner:
<blockquote>"When I started the device lab in Brighton, I didn’t worry about the paperwork. Instead of worrying about insurance, theft, liability and all those other worst-case scenarios, I decided to just do it and deal with the bad stuff if and when it arises. So far, so good."</blockquote>

## Closing Words

I believe in testing on real devices. Software emulators and simulators can be useful, but in the end they can only do that; simulate the experience (as Paul Robert Lloyd <a href="https://www.netmagazine.com/tutorials/build-responsive-site-week-going-further-part-5">points out</a>). To make testing on real devices possible for everybody, we need open device labs. If your city doesn’t yet have such a lab, I would say go for it, establish one. Don’t worry about the amount of devices you start off with, you'll be surprised about how much the community is willing to help.</p>

<strong>Last but not least:</strong> just a few days ago, while writing this, Andre Jay Meissner contacted me about the possibility to set up <a href="https://lab-up.org">LabUp!</a>, which would help people around the world in establishing nonprofit Open Device Labs. I think it’s a splendid idea and everyone who can help should <a href="https://lab-up.org">join the movement</a>.</p>

## Open Device Labs Around The World

There are now more than 150 ODLs in 35+ countries, but ODLs may have reached the peak of their popularity, given the growing attention on in-house device labs (IDLs). Look at this: <a title="Read 'Where Are The World’s Best Open Device Labs?'" href="https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/" rel="bookmark">Where Are The World’s Best Open Device Labs?</a>

<em>(jvb) (il) (sl)
</em>

