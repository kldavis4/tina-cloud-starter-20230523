---
title: 'Reliable Cross-Browser Testing, Part 1: Internet Explorer'
slug: reliable-cross-browser-testing-part-1-internet-explorer
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d893ddec-dcc7-447c-ac7b-7ae3ac51ad85/remotedesktop.jpeg
date: 2011-09-02T08:41:48.000Z
author: addy-osmani
summary: >-
  In this multi-part post, Addy Osmani takes you through the exact set-up he uses to accurately test content that will be potentially viewed by up to millions of users with a very diverse set of browsers.
description: >-
  In this multi-part post, Addy Osmani takes you through the exact set-up he uses to accurately test content that will be potentially viewed by up to millions of users with a very diverse set of browsers.
categories:
  - Coding
  - Browsers
  - Testing
  - Internet Explorer
---

In a perfect world, cross-browser testing would be straightforward. We would download a legacy version of a browser, run it, and be able to instantly test our pages and scripts without a single care in the world. The reality of cross-browser testing, though, is very different.

Issues such as runtime conflicts when running multiple versions of the same browser and inaccurate third-party testing tools mean we can spend hours just evaluating whether a testing set-up is anywhere near reliable.

I’m a user-interface developer at AOL (yes, we’re not dead yet!), and in this multi-part post I’ll take you through the exact set-up we use to accurately test content that will be potentially viewed by up to millions of users with a very diverse set of browsers. This set-up is similar to the one used by some of my colleagues at Opera, Mozilla and Google, so, fingers crossed, we’re doing this optimally.

**A quick note before we begin**. Setting up accurate testing for Internet Explorer as outlined in this post requires a bit of effort. So, please check your website analytics first to ensure that a sufficient number of IE users visit your website in the first place to warrant this effort.

{{% feature-panel %}}

## Internet Explorer 6 To 10

Let’s begin with our old friend, Internet Explorer (IE). As most of us know, running multiple versions of the original Internet Explorer executables on the same system is very difficult due to issues ranging from runtime version conflicts to operating-system incompatibility. In truth, I don’t think Microsoft ever considered a scenario in which developers needed a way to achieve this back when it was first conceiving IE 6, 7 and 8.

This has left developers in a chasm of uncertainty, forced through trial and error to discover a way to accurately test what is (for better or worse) the world’s most widely used set of browsers.

In this section, I’ll take you through some IE testing options that you may be using or have heard of before. I’ll explain why they might not be reliable; and then I’ll present the solutions we currently use at AOL for production websites.

In case you’re interested, our team generally uses IE 7 as a baseline, although we do also test stable, beta and preview or dev-channel versions of Chrome, Firefox, Opera, Safari and, of course, IE 8 to 10.

Our reason for using IE 7 as a baseline comes down to our global website analytics: IE 6, 7 and 8 are the most common browsers used to access our websites. However, we stopped supporting IE 6 as of a few months ago. The reality is that IE 6 has major compatibility issues with modern technologies, and our team has found that we are able to deliver projects up to 20% more quickly when we don’t have to worry about catering a basic experience to it.

## Most Third-Party IE Testing Tools Are Unreliable

A Google search for third-party IE testing tools will result in at least ten different options, nine of which are likely to be unreliable. Let’s go through a sample of them, in case you’re using one of them to test against staging or production websites at your work.

The following reviews may sound a little harsh, but the purpose is to stress the importance of using approaches that have been well engineered, tried and tested over time.

### IETester

Unfortunately, <a href="https://www.my-debugbar.com/wiki/IETester/HomePage">IETester</a> is probably the most popular third-party tool that I see designers and developers use to test multiple versions of IE. When I first tried it, I too was drawn by the promise of a single application that would solve all of my IE testing woes. However, all that glitters is not gold.

<figure><img title="IE Tester" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/108c4b83-a2a2-48fb-ad59-dc912d0d09e4/ietester.jpeg" alt="screenshot" width="500" height="289" /></figure>

The tool has a number of inconsistencies when testing IE 6, 7 and 8, with none providing a 1:1 experience of the original browsers. Our and many other teams have confirmed not only that the rendered output of IETester varies significantly from any real version of IE, but that pop-up interactions cause failures, Flash and CSS filters don’t work in user mode, conditional CSS comments often fail, and switching between versions makes it very prone to crashing.

In short, it’s unreliable, and this should be enough for any developer to consider alternatives.

### Multiple IE

TredoSoft’s <a href="https://tredosoft.com/Multiple_IE">Multiple IE</a> is another tool that often shows up when searching for an IE testing solution. Unfortunately, it too suffers from a number of issues, including inaccurate rendering. One common complaint is that people experience IE 5.5 rendering bugs even when they’re just testing IE 6; this certainly is not something we want to deal with at a time when many of us are trying to ditch IE 6 completely.

Multiple IE isn’t updated regularly either, and if the long thread of user issues experienced with it since its release doesn’t put you off, then consider that the tool’s IE textboxes actually break in a number of circumstances.

<figure><img title="Multiple IE" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6637147-9fb5-4ffb-9096-fdf296366977/multipleie.jpeg" alt="screenshot" width="500" height="400" /></figure>

To the best of my knowledge, both IETester and Multiple IE rely on an exploit known as DLL redirection in order to bypass issues with DLL naming conflicts, allowing the tools to attempt to run standalone copies of IE. I would recommend avoiding such tools, because implementing a completely sandboxed environment for IE that is as accurate as running the originals independently is very difficult.

### Expression Web SuperPreview

Next up is Microsoft’s Expression Web SuperPreview, which claims to simplify the process of testing and debugging layouts across multiple versions of Web browsers.

<figure><img title="Super Preview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ee4642e-d335-4fef-9ead-b271cfb58cf3/expression.jpeg" alt="screenshot" width="500" height="325" /></figure>

Unfortunately, you won’t be able to test complete user interaction, JavaScript, DOM manipulation, animation or much else with this tool. We live in an age when the Web can be very dynamic and, in some cases, highly interactive. A tool like this might work for baseline testing, but not for accurate cross-browser testing.

### BrowserLabs, Browsershots, BrowserCam

I personally use Adobe’s BrowserLabs &mdash; or sometimes <a href="https://browsershots.org">Browsershots</a>, if a static layout test is absolutely necessary. But again, neither of these options allow you to test interactions with your pages. The same goes for BrowserCam. These services simply weren’t designed for this purpose, but we still regularly see designers and developers using them as if they were.

I’m not in any way saying to flat out avoid these services, but rather that they’re inadequate for complete cross-browser testing. Designers and developers need to know exactly what a user sees when they interact with their website. No visitor will be using a static page renderer, so why rely on one yourself?

### Windows Virtual PC

One other solution you’ll probably come across is Microsoft’s Virtual PC, with <a href="https://www.microsoft.com/download/en/details.aspx?id=11575">time-bombed images</a> for IE6 to 8.

For a brief time this was considered to be the answer to cries from developers for a better solution. Unfortunately, it is by far the most inadequate (and demanding) solution to testing that I’ve seen proposed in the past few years. At least 12 GB of disk space is required to install all of the images, and the images regularly expire during the year.

A cross-browser testing environment for legacy browsers should have reasonable system requirements and, for the most part, not require regular manual updating in order to continue using it. Because the Virtual PC option fails these criteria, I can’t recommend using it either.

{{% ad-panel-leaderboard %}}

## Browser And Document Modes

We’ve looked at third-party tools, but what about Microsoft’s current solutions to these problems?

Both IE 9 and IE 10 PP2 support switchable document and browser modes via the F12 Developer Tools for cross-version compatibility testing. To be specific, browser-version testing here is made possible using a kind of emulation.

<figure><img title="Document Modes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d43cbb0b-a2ff-4037-88cb-bfe7cc02db08/browsermode.jpeg" alt="screenshot" width="530" height="136" /></figure>

“Document mode” determines what features a page has access to and what can be adjusted based on the page’s doc type, X-UA-compatible meta tag and headers. For example, the standards document mode allows the page to take advantage of IE’s implementation of ECMAScript 5 (ES5), while the IE 7 and 8 standards modes offer an alternative experience.

“Browser mode,” on the other hand, emulates different IE browser version behaviors and can be changed directly from the IE Developer Tools. Emulation is achieved in a few different ways, but it includes altering both the document mode and the user-agent string. In case you’re wondering, the UA string is adjusted here to ensure that code that relies on UA sniffing functions as though the correct version of the browser were being used.

<figure><img title="Browser Mode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/436a4ffa-d538-4b53-bf27-1ca5c9142c71/modes.jpeg" alt="screenshot" width="500" height="321" /></figure>

It is worth noting that IE 9 shipped with a newer JavaScript engine, called Chakra. While the browser itself supports a number of compatibility modes, because the JavaScript engine itself differs significantly from what shipped with IE 6, 7 and 8, there are <a href="https://blogs.msdn.com/b/ie/archive/2011/03/24/ie9-s-document-modes-and-javascript.aspx">acknowledged differences</a> between the experience in IE 9 and testing in a standalone browser.

That aside, there are, unfortunately, a number of **quirks** in the way that both document mode and browser mode function. Our team has run into scenarios where IE returns the wrong user-agent string to the server; and, as with the third-party tools, there have been several instances of inaccuracies with the expected rendering when tested against the original browsers.

Finally (and rather strangely), these modes have a number of issues of their own that are not present in IE 6, 7 or 8, making it even more difficult to establish whether the issues experienced are specific to a browser version or just the mode being used.

For these reasons, I would urge developers not to rely strictly on document or browser mode for their cross-version testing needs.

## Accurate IE Testing Solutions

### Option 1: Virtual Machines + IECollection

We’ve reviewed a number of solutions that don’t provide an accurate means of testing multiple versions of IE. So, what *does* work? The answer lies in using dedicated virtual machines (VMs) and a tool called <a href="https://utilu.com/IECollection/">IE Collection</a>.

<figure><img title="IE Collection" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1019a396-ac97-43ea-80bd-ce64919263e5/iecollection.jpeg" alt="screenshot" width="500" height="447" /></figure>

Out of the box, Utilu’s IE Collection offers the following:

*   A tested collection of **standalone** versions of IE, including versions 1 through 9;
*   Confirmed support for **accurate rendering** when compared against the original IE executables;
*   Confirmed support (to date) for the **correct IE JavaScript engine** implementations that shipped with the originals;
*   Confirmed support for the correct UA strings being detectable (not that you should be UA-string testing in the first place &mdash; however, if needed, it’s there);
*   Support for both the 32-bit and 64-bit versions of Windows XP, 2003, Vista and 7;
*   Access to the **IE Developer Toolbar**, which comes with the standard IE Collection set-up; this is compatible with IE 5 and above, but you also have the option to install Firebug Lite if you prefer that.

Although the majority of IE versions are supported and function reliably within the collection, there are known issues with versions of IE 7 when used under Windows Vista or Windows 7 (as noted on Utilu’s website). I’ll discuss how we handle this limitation shortly, but let’s first briefly go over virtual machines.

<figure><img title="Virtual Box" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c31e611b-73a7-4a64-afd8-6bcc461c6d50/virtual1.jpeg" alt="screenshot" width="500" height="312" /></figure>

A **virtual machine** (VM) is a sandboxed “guest” operating system that run within a normal “host” operating system. It effectively enables you to install and run a dedicated copy of almost any other operating system on your current one and to share a configurable set of memory and disk resources between the two. For example, a Windows 7 VM could easily be run on Mac OS X, as could an Ubuntu VM be run on Windows, and so on.

You’ll need two things to get started using VMs: a virtualization tool to create VMs on your OS, and a CD or image of the operating system that you wish to run as a virtual machine. Your company should be able to furnish you with Windows licenses relatively easily (… famous last words). If you’re a college student, you could probably get licenses for Windows XP SP3, Vista and 7 for free through the <a href="https://msdn.microsoft.com/en-us/academic/bb250591">MSDN Academic Alliance</a> program.

You could set up a number of different configurations to test Windows and IE, but if you’re using IE Collection, I would generally recommend the following:

*   Windows 7 for IE 6, 8, 9, 10;
*   Windows XP (SP3) for IE 7.

You shouldn’t need to support anything below IE 6 nowadays, but IE 4 to 5.5 also work fine on XP SP3.

At AOL, we use a combination of <a href="https://virtualbox.org">VirtualBox</a>, <a href="https://www.parallels.com/uk/products/desktop/">Parallels</a> and <a href="https://www.vmware.com/">VMware</a> for our virtualization needs. I prefer Sun’s VirtualBox because it has the following advantages:

*   It’s free, providing a lower barrier to entry for developers who cannot afford commercial licenses for Parallels or VMware;
*   In my experience, it tends to perform more optimally than Parallels or VMware under the same configuration settings;
*   It has a marginally better UI than the alternatives.

That said, VMware is considered better if you’re working with a standalone server. At the end of the day, all three options are equally valid, and both Parallels and VMware come with trial versions that you can easily evaluate. Choose whichever option best suits your needs.

**Pro tip:** Remember to configure your VM to use the minimim amount of memory needed to test, unless you are using a dedicated testing box. By default, not all virtualization tools are configured to do this. This will simply ensure that the rest of your OS runs more smoothly.

**Here are the three steps to setting this up:**

1.  If you’re a Mac user, I recommend using a 32-bit Windows 7 Pro or Ultimate image (or installation CD), with a minimum of 17 GB of disk space allocated for the installation. 512 MB of virtualized RAM (which can be adjusted in the settings panel) should work fine for testing on a non-dedicated testing machine, but use more if feasible. You can create this as a new VM using VirtualBox, which I have configured to run at a resolution of between 800 × 600 and 1024 × 768 pixels. Windows users have two options. If you’re already running a version of Windows 7, skip to step 2, where we’ll begin installing IE Collection. If you’re running a different version of Windows and would like to run a virtualized copy of Windows 7 on top of it, then follow the steps above for Mac users. Mac and Windows users should boot up their VM or desktop Windows installation before proceeding to step 2.
2.  Next, download [IE Collection](https://utilu.com/IECollection/) from Utilu’s website, and then install Windows 7 on either your VM or your primary system, depending on your set-up. This will give you access to IE 6, 8 and 9\. I usually install IE 10 for testing purposes separately, but bear in mind that it is only in the platform preview phase at the time of writing. Ideally, install only the bare essentials to test on any VM in order to avoid excessive start-up times.
3.  Mac and Windows users: to address the issue of IE 7 not working on Windows 7, you’ll have to create another virtual machine with Windows XP installed (ideally with SP3). Because no reliability issues have been reported for running either IE Collection’s IE 7 or the original IE 7 on this OS, your bases should be covered here. As stated in my previous instructions, obtain a Windows XP image or installation CD, and create a new VM using VirtualBox. Boot it up, install IE7 through the link above, and you should be good to go.

That’s it really! Some developers prefer to run IE 6 and 7 on XP (step 3) rather than on Windows 7 or Vista, because XP accounts for the majority of users who have yet to upgrade to IE 8 or 9. This, too, is completely valid; the set-up is flexible enough to support a little personal preference.

Next, for the sake of being thorough, let’s look at some alternatives to the set-up I’ve recommended above.

### Option 2: Dedicated VMs For Each Version of IE

Pragmatic developers might wish to maintain a dedicated VM for each version of IE being tested. On these VMs, rather than using any third-party tools, they would install the original, official IEs instead.

<figure><img title="Dedicated VMs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05704723-ad85-41ef-94fa-ad79410965fb/multivm.jpeg" alt="screenshot" width="500" height="302" /></figure>

The reasoning behind this is that it potentially **minimizes the risk** of individual browser configurations or overrides from interfering with one another, and it ensures that you get only the exact version of IE that you wish to test (and, in turn, the corresponding JavaScript engine in that version).

If you’re setting up dedicated VMs for individual releases of IE, I recommend the following set-up:

*   Windows XP (SP3) for IE 6,
*   Windows Vista (SP2) for IE 7,
*   Windows Vista (SP2) for IE 8,
*   Windows 7 for IE 9 and 10.

Knowing now about dedicated VMs, you might be wondering why we don’t use this set-up at AOL. I can only speak for my team, but we moved away from this approach because running three to four VMs on the same system and still using it efficiently for other tasks can become unmanageable.

With a minimum configuration of 512 MB of RAM per VM, we would be looking at around 2 GB of RAM (if not more) just for testing purposes. This set-up might work if you currently have 8 GB or more of system memory. But if not, there’s still hope.

We could always get a **dedicated box** just for testing purposes, and run all of our virtual machines directly on there instead. I recently acquired a second box at work for this very purpose. But at the end of the day, both options 1 and 2 are set-ups you can rely on.

### Option 3: VNC Or RDP + Dedicated Testing Boxes

<figure><img title="VNC or RDP" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d893ddec-dcc7-447c-ac7b-7ae3ac51ad85/remotedesktop.jpeg" alt="screenshot" width="500" height="358" /></figure>

A few companies (such as ZURB) prefer to use a form of remote desktop access to allow designers and developers to log into a dedicated testing box or set of boxes for cross-browser testing, over a network. The benefit of this is reduced demand on memory for each client. And this can be implemented in a few ways; VNC and RDP are the first that come to mind.

Virtual network computing (VNC) is a platform-independent desktop sharing system that allows you to remotely control another computer. It transmits both keyboard and mouse events from one system to another, relaying screen updates back in the other direction over a network. Similarly, RDP allows users to access applications over a network, but it is a proprietary protocol developed by Microsoft. If you happen to be running Mac OS X, VNC is already built in, but a number of VNC clients are also available in the wild, such as <a href="https://realvnc.com">RealVNC</a>. On the RDP side of things, Mac users can use Apple’s own <a href="https://www.apple.com/remotedesktop/">Remote Desktop </a> and Remote Desktop Connection by Microsoft.

You might be wondering what the differences are between VNC and RDP. RDP is semantic and is more aware of controls, fonts and other graphical primitives, while VNC is a little “dumber” in this regard. VNC, though, permits a session to be shared on the target machine, which might be useful for multi-user demos; whereas RDP does not, as far as I’m aware.

With the decreased memory requirements, you might then wonder why we don’t opt to use remote desktops for testing at AOL. The primary reason is that, in some cases, testing over a network can result in packets (effectively, frames) being dropped, which can affect our ability to test highly interactive applications or websites. Also, websites that make use of rich-media experiences based on canvas, SVG or otherwise aren’t reliably tested over networks for this reason. But don’t let our experience put you off. I know of teams in other companies that haven’t run into these issues, and remote testing might be suitable for some networks more than others.

### Option 4: Remote Testing Through A Third-Party Service

If your team is unable to purchase or rent dedicated boxes for remote testing due to cost, there are third-party services you can use which which readily host host multiple versions of Windows, along with historic versions of IE and other browsers out of the box for a low subscription fee.

<a href="https://www.browserstack.com/features">BrowserStack.com</a> and <a href="https://browserling.com/">Browserling</a> are two such options. You might be surprised to know that both actually support local testing of your servers and files through ssh tunneling and as long as your company are comfortable with content being tested in this manner, it’s an adequate and affordable way of getting reliable cross-browser testing into your business.

If I had to personally recommend one of the services over the other, it would definitely be BrowserStack. They offer a wider range of browser versions and OS versions than Browserling and also include debugging and developer tools as a part of their service.

There is however one downside to the services recommended above: at the time of writing, neither currently appear to support the Firefox nightlies/builds for FF7,8,9, Opera.next nor the dev/beta/canary builds of Google Chrome.

I personally like the flexibility to test how my projects might render and function in upcoming browsers as this provides you with a level of comfort about a release - eg. if FF7 gets released next week, I’d rather be able to patch projects before everyone starts updating rather than after. That said, this isn’t a concern thats shared by a lot of developers or designers, so feel free to try out BrowserStack or Browserling if Options 1-3 aren’t for you.

## Another Alternative For Developers Wishing To Avoid Purchasing Multiple Licenses

Some developers may be familiar with Microsofts virtual machine disk images which I mentioned earlier. It can be quite a challenging task getting these images to work with anything other than Microsofts VirtualPC, however a recent project called <a href="https://github.com/xdissent/ievms">IEVMS</a> (thanks to Paul Irish for the heads up) attempts to solve this problem. IEVMS offers a set of scripts that facilitate using the images with VirtualBox on Linux or OSX and with a single command it’s possible to have IE6 - IE9 running in separate virtual machines.

The project also offers a clean snapshot mode, potentially enabling developers to roll-back these VMs so that its possible to have them working indefinitely. This project does (at the time of writing) suffer from a few minor bugs that are being worked out, but is certainly worth looking at if it sounds more appealing than the alternatives. Bear in mind that this script will still need to download the 10-12GB of disk images required for the VMs and I’m not sure if IEVMS breaks the EULA, so ensure this won’t be an issue before launching the scripts.

## Conclusion

I hope this guide has come in handy. Please feel free to share your own stories and experiences of cross-version testing IE, because they may help other readers decide which option to try out first.

In part 2 of this post, we’ll look at cross-browser testing modern browsers. See you then!

{{% ad-panel-leaderboard %}}

## Further Reading

*   [Testing For And With Windows Phone](https://www.smashingmagazine.com/2015/05/testing-for-windows-phone/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [Review Of Cross-Browser Testing Tools](https://www.smashingmagazine.com/2011/08/a-dozen-cross-browser-testing-tools/)
*   [What’s The Deal With The Samsung Internet Browser?](https://www.smashingmagazine.com/2016/10/whats-the-deal-with-the-samsung-internet-browser/)

{{< signature "al, mrn" >}}
