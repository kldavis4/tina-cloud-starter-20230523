---
title: 'Open Device Labs: Why Should We Care?'
slug: open-device-labs-why-should-we-care
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284a234-0a44-4c41-abc6-ff0a4749f847/odl-nbg-2-4-500-mini.jpg
date: 2013-05-29T00:08:28.000Z
author: anselm-hannemann
description: >-
  With all of the different smartphones, tablets and other devices that sport
  various operating systems and versions thereof, a Web developer’s job —
  testing (sometimes virtually) on multiple devices to resolve errors — hasn’t
  become any simpler. This article suggests how we can manage these tasks without pouring a truck-load of money into actually buying all of these different devices.
categories:
  - Tools
  - Design
  - Web Design
  - Community
  - Testing
---
With all of the different smartphones, tablets and other devices that sport various operating systems and versions thereof, a Web developer’s job — testing (sometimes virtually) on multiple devices to resolve errors — hasn’t become any simpler. This article suggests how we can manage these tasks without pouring a truck-load of money into actually buying all of these different devices.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [<span class="headline">Establishing An Open Device Lab</span>](https://www.smashingmagazine.com/2012/09/establishing-an-open-device-lab/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)

<figure><figcaption></figcaption></figure>

## Do You Test On Actual Devices?

Whether you develop websites or apps, you face several problems in ensuring that a product runs correctly on as many devices as possible. Emulators for iOS, Android, Opera and the rest can help with that, but they differ from the software that runs on real devices. One of the things you just can’t simulate properly is <strong>touch interaction</strong>. Without being able to test gestures, there is no way to find out whether your users will understand how to use your interface. Because this is unlikely to change anytime soon, there is no way around testing on real devices.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5cf18c3-47db-4975-b9df-68e04736dd4d/odl-nbg-2-4-mini.jpg"><img loading="lazy" decoding="async" class="161628" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284a234-0a44-4c41-abc6-ff0a4749f847/odl-nbg-2-4-500-mini.jpg" alt="odl-nbg-2-4-500" width="500" height="333" /></a><figcaption>A user tests his website on a Blackberry device and takes notes of bugs.</figcaption></figure>

While most developers probably have a smartphone and a tablet at home, two devices cover only a fraction of the types of devices and operating systems available — devices and operating systems that you should be testing your projects on. There are <strong>dozens of screen sizes, browsers and display types</strong>, and they make a huge difference when you’re fixing bugs in a responsive design. Despite your CSS and JavaScript being valid and well written, malfunctions on some mobile devices will occur simply because the variety of rendering engines haven’t been sufficiently standardized.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e917a84-f0f2-4b8c-b01a-cd5f2b702768/odl-nbg-2-15-mini.jpg"><img loading="lazy" decoding="async" class="162503" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe8ab68a-e527-4d51-8706-75fb83638ece/odl-nbg-2-15-500-mini.jpg" alt="odl-nbg-2-15-500_mini" width="500" height="333" /></a><figcaption>Testing touch gestures on different devices.</figcaption></figure>

Some errors you would probably never notice because they appear only on devices that are uncommon in your country — but may be common in others. Thus, buying a lot of devices for testing seems to be an obvious solution. But that leads to two major problems: buying all of these devices would become very expensive (and you probably would not use them regularly anyway). Secondly, remote <strong>debugging on a wide variety of devices is not that simple</strong>. Fortunately, this has become much easier with all of the tools available today, but you still have to deal with it.</p>

## Crowd-Sourcing Makes Life Easier

This is where crowd-sourcing comes in. No one needs all of these devices every day. In fact, most developers need them only every few weeks.

Instead of every developer buying them all, what if there was a place where people could share devices for testing? If each person purchased a single device, you might already have enough to set up a device lab — which would <strong>save you a lot of money</strong>. The bigger the community of people contributing to this lab, the larger the variety of devices to test on. Even better, the community could even ask manufacturers to provide their devices to the lab, thus saving you even more money. Thus, access to mobile devices and a great testing space would be made available not just to you, but to everyone.

The <a href="https://opendevicelab.com/">Open Device Lab</a> initiative aims to do just that. Currently, there are more than 50 locations around the world where a developer can go to test their project on multiple devices (some labs have more than 80 in stock). Most are completely free to use, while a few charge a small fee to cover the cost of running the lab. Because open device labs are meant to be non-profit, this is a fair deal and still much cheaper than buying the devices on your own.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1f791b-25c1-49a0-8a03-ae6364fe30bc/odl-nbg-2-2-mini.jpg"><img loading="lazy" decoding="async" class="162506" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/086d01bf-d543-4349-b7bd-5e8f125cd0c4/odl-nbg-2-2-500-mini.jpg" alt="odl-nbg-2-2-500_mini" width="500" height="333" /></a><figcaption>A co-working space can be a nice surrounding for an Open Device Lab.</figcaption></figure>

The people behind the labs range from individual developers who establish labs in their local co-working spaces to agencies that open their doors to share their hardware and knowledge with everyone. Different labs focus on different types of development: some on websites, some on apps, others on operating systems. Most have rules on using the lab. In general, you will want to make sure that installing your own software or wiping a device is OK.

Most sites cover a wide range of mobile manufacturers. In general, open device labs aim to supply at least the devices most used in their area. To check which devices are available in your area, <a href="https://opendevicelab.com/#find">search for a lab</a> and check the list of manufacturers.

Many labs also provide <strong>development tools</strong>, such as <a href="https://people.apache.org/~pmuellr/weinre/docs/latest/">Weinre</a>, Adobe <a href="https://html.adobe.com/edge/inspect/">Edge Inspect</a>, <a href="https://jsconsole.com/">JS Console</a> and <a href="https://github.com/viljamis/Remote-Preview">Remote Preview</a>, as well as platform-specific tools, such as the Safari <a href="https://developer.apple.com/library/ios/#documentation/AppleApplications/Reference/SafariWebContent/DebuggingSafarioniPhoneContent/DebuggingSafarioniPhoneContent.html">Web Inspector</a>. <a href="https://gist.github.com/3816624">Remote inspection</a> might be set up in some labs so that you can test and debug your websites from your computer, while some labs will have helper tools to enable you to test a product synchronously on all devices and debug individually. Each lab has its own features, so check to see whether the one near you meets your needs.

While Remote Preview will display a website on different devices, JS Console is just a remote console for your website. Weinre and Edge Inspect allow for remote inspection through a WebKit inspector and synchronized browsing, but they only run in the embedded Web view of the OS.

The labs also address <a href="https://klick-ass.com/news/affordable-wifi-access-point-capable-to-support-50-100-clients-wanted/">Wi-Fi issues</a> that occur with normal routers when more than an 40 devices are connected to the network. People have already <strong>solved problems that would normally drive you crazy</strong>, and they are happy to share their solution with you. And you can do the same by sharing your knowledge with others.

Many labs are built in existing co-working spaces, which makes it easy to maintain and access them. Another advantage of this is that you can schedule your time in the co-working space to coincide with when you will need to test extensively.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a5a78b4-7263-4873-9359-4c605765fe6e/odl-nbg-2-16-mini.jpg"><img loading="lazy" decoding="async" class="162509" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db2b326a-4d82-40cb-ae94-60965ced8496/odl-nbg-2-16-500-mini.jpg" alt="odl-nbg-2-16-500_mini" width="500" height="333" /></a><figcaption>A user takes notes about viewing his website on a Blackberry.</figcaption></figure>

## Help Yourself And The Community

You can benefit a lot from such spaces. When you’re tackling a particularly tricky problem, the lab very likely has people who can assist you.

But make sure to help others when they ask for it. Developing websites together is much more fun and, from my experience, produces better results. And when you deliver great work, other people will notice and will consider hiring you for future work.</p>

## Support Open Device Labs

Because open device labs are built by the community for the community, it is very important that users give a little back. Doing this is rather simple. Most people have old devices at home. If you do and don’t need them anymore, <strong>consider donating them</strong>.

Secondly, offer some spare time to maintain a lab or at least spread the word among your colleagues. All of these little things help labs to grow, in turn helping developers like you all around the world.

The <a href="https://opendevicelab.com/">Open Device Labs</a> website has a map of all existing labs. You can see how many devices are available and from which manufacturers, and you can read and give feedback on each lab. Thus, you can easily find a lab that fits your needs.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cc9d4aa-18ad-4314-b903-93c29c700055/odl-nbg-2-18-mini.jpg"><img loading="lazy" decoding="async" class="162512" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac629cee-ddba-46c6-ade9-60cc773fb158/odl-nbg-2-18-500-mini.jpg" alt="odl-nbg-2-18-500_mini" width="500" height="333" /></a><figcaption>Viewing your product on various devices at one place makes it easy for you to identify problems.</figcaption></figure>

Nonetheless, many more labs are needed around the world, as shown in the <a href="https://opendevicelab.com/#find">world map</a>. The demand is worldwide, but many people don’t know that such labs exist or how easy starting one actually is. Labs flourish with enough supporters, and the more supporters in a region, the better a lab gets. So, <strong>help to build these spaces</strong>, and tell others about the movement.

An <a href="https://api.opendevicelab.com/">API</a> enables easy access to information about all of the labs. To open up your own lab, the non-profit organization <a href="https://lab-up.org/">LabUp</a> will support you by providing relevant information. You can easily build a website for your lab, and keep basic information about the lab up to date using the API. It is CORS- and JSONP-enabled, so you can access it right from your own domain. The <a href="https://opendevicelab.com/api-documentation.php">documentation</a> describes what kind of data you can access with the API and how to implement it on your website.

## Create An Open Device Lab

Open device labs are a new movement, so you might not find one near you. But filling the gap is easy. Just search for colleagues in your region, connect with them, build the lab together, and move the Web forward! If you work at a company that owns a lot of devices, creating an open device lab is especially easy. But creating one wouldn’t be much harder for a freelancer. <a href="https://lab-up.org/">LabUp</a> will be happy to help you <a href="https://www.smashingmagazine.com/2012/069/24/establishing-an-open-device-lab/">establish a lab</a> by giving you tips on setting up the technical aspects and by connecting you to device manufacturers.

If you’d like to spearhead a lab in your area, taking care of the following details will give you a good start:

*   Make the space open and freely accessible.
*   Create a pleasant interior so that people look forward to coming.
*   Provide some devices at launch, and invite contributions or sponsorships.
*   Make sure the Internet connection is fast and reliable.
*   Build rock-solid Wi-Fi.
*   Install stands for the devices.
*   Secure the devices so that they don’t get stolen.
*   Coordinate people to run the lab when it’s open. (And consider keeping it open for long hours).
*   Find ways to reduce costs for you and the lab’s users.

In short, seriously consider creating, maintaining or supporting an open device lab in your area.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b53fb9ae-4d86-4f04-b7fc-6dcf779ebdfb/odl-devicepark-mini.jpg"><img loading="lazy" decoding="async" class="162514" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d437c6d-8382-438e-b949-a6bc336901a2/odl-devicepark-500-mini.jpg" alt="odl-devicepark-500_mini" width="500" height="127" /></a><figcaption>Open Device Labs often have a lot of different devices to test on.</figcaption></figure>

### More Resources

*   [LabUp!](https://lab-up.org/)
*   “[Establishing an Open Device Lab](https://www.smashingmagazine.com/2012/09/24/establishing-an-open-device-lab/),” Viljami Salminen, Smashing Magazine
*   “[How to Build a Device Lab](https://www.dmolsen.com/mobile-in-higher-ed/2012/06/26/how-to-build-a-device-lab-part-1/)” Dave Olsen
*   [Jay Meissner](https://klick-ass.com/tag/open-device-lab/) Articles on Jay's blog related to open device labs

<em>All images by Open Device Lab Nuremberg.</em>

<em>(al) (ea)</em>

