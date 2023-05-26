---
title: 30 Must-Have Tweaks For Your Mac
slug: 30-must-have-tweaks-for-your-mac
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8a7a74-8225-4c16-8d11-9b811cb5e874/macbook.gif
date: 2009-06-04T15:25:25.000Z
author: mark-nutter
description: >-
  In [one of the recent
  posts](https://www.smashingmagazine.com/2009/04/26/five-reasons-why-designers-are-switching-to-mac/),
  we looked at some reasons why some developers switch to the Mac. If you've
  decided to make the switch yourself, you can do a lot to make the transition
  smoother. We will take a look at some must-have software, configurations and
  hacks that can make your life easier as you switch and that can get you up to
  full productivity (and maybe beyond) in no time at all.

  [![Picture](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a46edd6-2ffe-4c93-9234-33937a983dc4/picture12.png)](https://www.smashingmagazine.com/2009/06/04/30-must-have-tweaks-for-your-mac/)

  We have tried to find as many free solutions as possible, but you have to pay
  for some applications to get their full functionality. If we have missed a
  configuration, hack or piece of software that you found helpful when
  switching, please post it in the comments.
categories:
  - Apps
  - Productivity
  - Mac
  - Workflow
---
In one of the recent posts, we looked at some <a href="https://www.smashingmagazine.com/2009/04/26/five-reasons-why-designers-are-switching-to-mac/">reasons why some developers switch to the Mac</a>. If you've decided to make the switch yourself, you can do a lot to make the transition smoother. We will take a look at some must-have software, configurations and hacks that can make your life easier as you switch and that can get you up to full productivity (and maybe beyond) in no time at all.

We have tried to find as many free solutions as possible, but you have to pay for some applications to get their full functionality. If we have missed a configuration, hack or piece of software that you found helpful when switching, please post it in the comments.

You may also be interested in the following related posts:

*   [25 Free Mac Apps That Will Boost Your Productivity](https://www.smashingmagazine.com/2009/07/25-open-source-mac-apps-that-will-boost-your-productivity/)
*   [Mac Hacks: 17 AppleScripts To Make Your Life Easier](https://www.smashingmagazine.com/2009/05/mac-hacks-17-applescripts-to-make-your-life-easier/)
*   [Why Web Developers Don’t Need A Mac](https://www.smashingmagazine.com/2009/06/why-web-developers-dont-need-a-mac/)

## Configurations

### Right-Clicking

One of the most visible differences between Macs and other computers is the former's lack of a second button on the mouse. The Mac mouse harkens back to the original mouse invented at the Xerox Palo Alto Research Center, which also had only one button. Eventually, Windows grew to ubiquity, touting its two-button mouse, and the world became comfortable with that configuration. As a switcher, you're used to that handy right-click, and lucky for you, the habit doesn't have to end.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 1.png" alt="Picture 1" width="303" height="432" />

All Macs support right-clicking, and it works just as it does on a Windows system, popping up menus and extras. Without messing with your settings, you can always hold "Control" and click to active a right-click on a Mac, but this gets tedious pretty quickly. To make the experience more seamless, go into your preferences and activate "Tap to click" and "Secondary click," which will allow you to tap the trackpad with two fingers simultaneously to trigger a right click. It may sound odd, but it takes only a few minutes to get used to. You can also just hold two fingers down on the trackpad and click the physical mouse button to get the same effect. Of course, plugging a two-button mouse into a Mac is another way to get your right-click back.</p>

### Tweak Mouse-Tracking Speed

The mouse tracking on a Mac feels quite different from that of Windows because it does not accelerate. This can be partly alleviated by turning the tracking speed all the way up. But if you really pine for that Windows feel, you can try <a href="https://plentycom.jp/en/steermouse/">SteerMouse</a>, albeit for $20.</p>

### Turn Off Screen-Dimming

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 2.png" alt="Picture 2" width="500" height="226" />

While some people want their screen to dim after a period of inactivity, it can quickly become annoying for others. This feature can be turned off in the preferences under the options for "Energy saver."

### Turn on the Firewall

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 3.png" alt="Picture 3" width="500" height="357" />

Macs include two firewalls: a packet-filtering firewall called <a href="https://www.macdevcenter.com/pub/a/mac/2005/03/15/firewall.html">IPFW</a> that filters traffic based on type, port number, origin and destination, and a socket-filter firewall (new in Leopard) that filters based on the application making the request. While the socket-filter firewall in OS X is disabled by default, you can go into "Preferences &gt; Security &gt; Firewall" to enable it. IPFW is short on configuration options, but that can be remedied by downloading either <a href="https://www.hanynet.com/noobproof/index.html">NoobProof</a> or <a href="https://www.hanynet.com/waterroof/index.html">WaterRoof</a>, which give you more security options.</p>

### Log-In Items

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 4.png" alt="Picture 4" width="500" height="352" />

Setting applications to start upon logging in is actually quite simple on a Mac. If the application you want to start at log-in is on your dock, simply right-click its icon and choose "Open at log-in." You can also go into "Preferences &gt; Accounts &gt; [your account] &gt; Log-in items" and add applications manually there. Keep in mind that the more applications you set to open at log-in, the longer your systems will take to boot.

You can also change the background for the main log-in screen on your Mac. This handy little piece of freeware takes whatever your desktop background is and mirrors it onto your log-in screen. Or you can use the following command in your terminal to change it to any image you want:
<blockquote>sudo defaults write /Library/Preferences/com.apple.loginwindow DesktopPicture "/Library/path_to_your_pic/your_pic.jpg"</blockquote>

### Hot Corners

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 5.png" alt="Picture 5" width="500" height="165" />

Hot corners allow you to set up each corner of your screen to be a hot spot that triggers an event whenever you mouse over it, such as shuffling active windows to off screen to show the desktop or displaying widgets. This gets interesting when combined with the "Expose" and "Spaces" features.

Expose spreads your windows out on the screen so that you can focus on a new one. Once you get used to it, you'll wonder how you ever lived without it. To make it really useful, set up a hot corner to activate it. Additionally, Spaces allows you to display multiple desktops from a bird's-eye view. Add this to another corner and you've got something really special. You'll be able to show the desktop, drag a file, switch to a different space, find a window that's hidden behind several others and drop the file into that window, all with one mouse click. Check it out in the video below:

Play around with different hot corner configurations to find the one that best suits you. I recommend using three of the four for the "Expose All Windows" and "Show Desktop" functions and Spaces. If you have a laptop, setting one of the corners to put the display to sleep is handy because no button or key does that otherwise.</p>

### Configure Spaces

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 6.png" alt="Picture 6" width="500" height="391" />

Having multiple desktops to work from can be a boon to productivity. Spaces allows you to create up to 16 different desktops, enough to satisfy even the most spastic multi-tasker. Along with these desktops, you can specify that certain applications only open in certain spaces, as well as specify that some apps display no matter which desktop you're working in. Here are a few applications we suggest displaying in all spaces: Chat applications (Adium, iChat, IRC), movie players (VLC, QuickTime, DVD player), Twitter clients and any application useful in more than one context. I have a space for general Web browsing, iTunes and iPhoto, email and communications, Photoshop and design, coding and development, Windows virtualization, notes and reminders and one that I keep clean just in case.</p>

### Add Activity Monitor to the Dock

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 8.png" alt="Picture 7" />

Activity monitor is the equivalent of the task manager in Windows. Certain items, when added to the Dock, take on a few extra behaviors. In the case of the activity monitor, those items can display helpful information instead of their icons while sitting in the dock: such as a pie chart showing how much memory is being used, a live graph of processor activity and more. While you can always pop up a window and hit Command + Option + Esc (your new Ctrl + Alt + Delete) to force quit an application, you don't get any information about programs that are running. Clicking on the activity monitor gives you the force quit option and a wealth of information about your processes.</p>

### A Smarter Finder

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 9.png" alt="Picture 9" width="500" />

Finder is a file explorer that people either love or loath. You can do a few things to make it more useful, though. Right-click on the top part of the finder window, much like you would to edit a toolbar in the browser, and you'll see that you can configure the buttons in the finder window. Choose "Customize Toobar" and add the "Path," "Delete," and "New Folder" buttons, along with any others you desire.

In the left sidebar of the finder, you'll see a list of favorites, including your home folder, main disk drives, any attached drives and the most used folders (photos, music, sites, etc.). You can customize this list by dragging folders and other items onto the sidebar. You can also add "smart folders" (File &gt; New smart folder) that filter files based on a set of rules. For instance, one smart folder I keep in my sidebar is a list of all files over 100 MB, in case I need to free up some hard drive space. If you want to add separators to the sidebar, there's <a href="https://www.typoet.com/separators/index.html">a neat little guide on how to do that here</a>.

You can download toolbar scripts for even more functionality. For instance, you can add a button that opens the terminal in whatever folder you are currently browsing. Check them out here. Of course, if you end up hating the finder, you can try an alternative, like <a href="https://www.cocoatech.com/">Cocoatech's Path Finder</a>

## Hacks

### Widgets on Your Desktop

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 10.png" alt="Picture 10" width="500" height="82" />

Widgets are Apple's version of Konfabulator (now Yahoo! Widgets), but unlike Konfabulator, they are doomed to exile in the dashboard (a "second desktop" that pops up when you hit the right keys or hot corner). The problem with Dashboard is that the more widgets you have running, the longer they all take to pop up the first time you activate it after a restart. If you prefer to have your widgets available on demand on the desktop, enter the following command into your Mac terminal:
<blockquote>defaults write com.apple.dashboard devmode YES</blockquote>

To place a widget on the desktop, open up Dashboard, start dragging the widget and close the dashboard. Unfortunately, widgets will stay on top of all your windows. Frustratingly, the only way to override this behavior is to get a paid application called Amnesty Widgets, which makes OS X's widgets more like Yahoo Widgets. Of course, you could just use Yahoo! Widgets and forget OS X's widgets altogether.</p>

### Change Command to Control

This is an adequate configuration for most, but an absolute lifesaver for some. It took me a while to get used to using Command instead of Control, but I eventually broke the old habit. Some people have been known to give up on the platform because of this issue. For those of you who have a hard time adjusting, simply map the Command key to Control. <a href="https://doublecommand.sourceforge.net/">doublecommand</a> and <a href="https://www.kodachi.com/software/fKeys/">fKeys</a> are popular utilities that let you do all sorts of custom mapping to make your switch easier.</p>

### Maximize Your Zoom

One of the weirdest quirks to get used to when switching to the Mac is the behavior of the "Zoom" button on windows (the green button in the top-left corner of all windows). Instead of sticking the four sides of the window to the very edges of the screen, Zoom will simply expand the size of the window to fit the screen but the window will remain draggable. Often it doesn't even do this and instead changes the size of the window in unexpected and frustrating ways. Luckily you can download a <a href="https://www.switchingtomac.com/tutorials/make-the-os-x-maximize-button-work-like-windows">handy little plug-in</a> to force Zoom to use the window's maximize function. Other than using this plug-in, you'll have to get used to dragging the bottom-right corner of the window to force it.</p>

### Hidden Applications, Hidden Files

If you ever need to find files that are hidden by default, type this into the terminal:
<blockquote>defaults write com.apple.finder AppleShowAllFiles TRUE</blockquote>

You can hide windows by hitting Command + h, but you get no indication that a window is hidden once it's gone. To make the application icon more transparent in the dock when it is hidden, type this into the terminal:
<blockquote>defaults write com.apple.Dock showhidden -bool YES
killall Dock</blockquote>

### Quick Look Expanded

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 11.png" alt="Picture 11" width="526" height="455" />

Quick Look can save you precious seconds by showing you a preview of a file before opening it in its default program. Simply hit the space bar on a file to activate it. This is limited to certain files, but a few handy plug-ins out there give you Quick Look functionality for folders, Zip files and more. theAppleBlog.com has compiled a great list of fours such plug-ins.</p>

### Safari Debugger

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 12.png" alt="Picture 12" width="500" height="401" />

Safari offers a great browsing experience, despite what you may have heard. It's quick, clean and powerful, although not that easy to customize. You can apply a few neat hacks to make it a little more useful though. To enable the surprisingly rich Web development debugger tool, type this into your terminal:
<blockquote>defaults write com.apple.Safari IncludeDebugMenu YES</blockquote>

For a wealth of Safari hacks and plug-ins, check out <a href="https://www.safarihacks.com/">Safari Hacks</a> and <a href="https://pimpmysafari.com">Pimp My Safari</a>. <a href="https://pimpmysafari.com/plugins/saft">SAFT</a> is a great extension for Safari that provides a lot of great functionality for $12.</p>

### Customize Your Dock

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 13.png" alt="Picture 13" width="500" height="58" />

Apple has very definite feelings about how the Dock should look because it does not give you many means of customization. To mess with the look and feel of the Dock, you can try <a href="https://dockulicious.com/docks/view/mirage">Mirage</a>, which removes all styling, <a href="https://www.panic.com/candybar/">Candybar</a>, which gives you a variety of styling options, and <a href="https://leoparddocks.net/">Leopard Docks</a>, a website dedicated to custom Dock stylings.

When the Dock is on the left or right side of your screen, it goes from a 3-D look to 2-D. If you prefer the 2-D and bottom-screen configuration, type this into your terminal:
<blockquote>defaults write com.apple.dock no-glass -boolean YES
killall Dock</blockquote>

As far as the Dock's behavior goes, here's a must-have hack you can apply. Add a "Recent files" stack to the Dock by entering the following in your terminal:
<blockquote>defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1; }; "tile-type" = "recents-tile"; }'
killall Dock</blockquote>

### Open-With Defaults

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 14.png" alt="Picture 14" width="400" height="194" />

If you want a certain file to open in a certain program, right-click on a file of that file type and select "Get info," which will bring up a box with all sorts of information about the file. We're interested here in the "Open with" section, where you can choose its default program. Once you've selected the proper program, click the "Change All" button to make it the default program for all files of that file type. One suggestion: make TextEdit your default program for .doc and .docx files: it opens them much faster than Word or OpenOffice.</p>

## Software

While the software library on the Mac pales in comparison to the one on Windows in terms of sheer volume, it does have quite a bit of polish. This polish, however, often doesn't come without a price. Free software for the Mac does exist out there, but it's not nearly as widely available as you're probably used to with Windows. That being said, there are quite a few apps, both free and paid, that you should install on your Mac to make the experience much more enjoyable and productive. Here are a few to get you started:

### Multimedia

*   [Flip4Mac](https://www.microsoft.com/downloads/details.aspx?FamilyId=915D874D-D747-4180-A400-5F06B1B5E559&displaylang=en) Install the free version to play WMV with QuickTime.
*   [Perian](https://perian.org/) Every codec you'll ever need for QuickTime.
*   [VLC](https://www.videolan.org/vlc/) The de facto media player for the Mac. Not only does it eliminate the need for the two pieces of software mentioned above, it provides more features than you'll probably ever care to use. Use VLC instead of the built-in DVD player as well. VLC integrates nicely with OS X, and you can even use your Apple remote with it. Just download it.
*   [Connect360](https://www.nullriver.com/products/connect360) If you want to stream movies, pictures and music to your Xbox 360, this is a great solution for the Mac; some claim it works better than Microsoft's implementation.
*   [Transmission](https://www.transmissionbt.com/) A very lightweight and solid bit torrent client for the Mac. It fits in very well with OS X, style-wise.
*   [Songbird](https://getsongbird.com/) Not everyone wants to use iTunes to manage their music collection. Many prefer Songbird, the much-loved open-source alternative.</p>

### System and General Purpose

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/mac-hacks/Picture 19.png" alt="Picture 19" width="500" height="210" />

*   [Growl](https://www.google.com/url?sa=t&source=web&ct=res&cd=1&url=http%3A%2F%2Fgrowl.info%2F&ei=KHQISuvDGuSwtgeYrJifBw&usg=AFQjCNEGpuLHxoMiqgCdTaBHx0SxrNZZ1w&sig2=xyruG-JWH2P7Zv3rOF4YyQ) If having uniform system-wide notifications for all your applications sounds intriguing, you'll want to check out Growl. It works with a vast array of software and is extremely customizable. Some notifications you'll receive let you know when new email, instant messages or Twitter messages arrive, when your downloads are complete, when your computer has been unplugged and when a new song is playing on Last.fm (complete with artist and details). Growl has a myriad of useful plug-ins and uses. Take, for instance, the growl notification that tells you when your tests have passed in your Web application: a must for any Mac user.
*   Unplugged https://unplugged.en.softonic.com/mac/download (unplugged)
*   Quicksilver While OS X does have the "Spotlight" feature, which allows you to quickly find files and launch applications, it pales in comparison to the snappiness and customizability of the application-launcher Quicksilver, which is very similar to Firefox's Ubiquity. Much like Growl, you can install tons of useful plugins to tailor the experience to your needs. When you start using Quicksilver regularly, you'll find yourself going to the Dock less and less to launch and interact with your applications. It's lightening fast and quite powerful. Imagine hitting a keyboard shortcut, typing "email," "tab," "compose," , and "enter" to send a quick email to somebody. Another must have.
*   [Fluid](https://fluidapp.com/) If you're anything like me, you spend a lot of your computer time interacting with Web applications rather than client-side applications. You may miss the neatness of applications existing independently of your Web browser, too. If you do, then Fluid is the solution. It takes any Web page you specify and contains it within its own Mac application, complete with icon and windowing preferences. Imagine having a dedicated app for your Google documents, Facebook, your favorite Twitter client, your Web analytics and more. It draws on the same idea that Adobe is pushing with Air. Fluid is as extensible and customizable as Growl and Quicksilver.
*   [The Unarchiver](https://wakaba.c3.cx/s/apps/unarchiver.html) You're going to want a program that can handle StuffIt, RAR, ZIP and other compression file types with ease, and the Unarchiver is it. Free and straightforward.
*   [smcFanControl](https://www.eidac.de/) Macs tend to be a bit more of a walled garden than other computers, but that doesn't mean they have to be. With the right amount of research, you can usually find a piece of software or terminal hack that bends the Mac to your will. smcFanControl is one such application, made for those who want to control just how hot their laptops get.
*   [Carbon Copy Cloner](https://www.google.com/url?sa=t&source=web&ct=res&cd=1&url=http%3A%2F%2Fwww.bombich.com%2Fsoftware%2Fccc.html&ei=unQIStvFG5CmM-Tz-aID&usg=AFQjCNHZS043mX7M2C_I6f35FVLXI2DpQA&sig2=ybpvvch0vEJInTTgWreSng) If you ever need to transfer your hard drive to another machine, and you will, Carbon Copy Cloner is truly the best solution to the problem. It's rock solid, simple to use and makes the whole process extremely pain free.</p>

### Communications

*   [Adium](https://www.google.com/url?q=https://adiumx.com/&ei=zXQISqSBB5fItgeu_MWXBw&sa=X&oi=spellmeleon_result&resnum=1&ct=result&usg=AFQjCNE3QA6eEmics5LwT3b_yw3hLGt_sg) Adium is the de facto chat client for the majority of high-end Mac users out there. It covers more networks than are worth listing here. This is another must-have app.
*   [Colloquy](https://www.google.com/url?sa=t&source=web&ct=res&cd=1&url=http%3A%2F%2Fcolloquy.info%2F&ei=5nQISqzZMMOEtwfgrKmBBw&usg=AFQjCNFhJnLCkdL_kAI7SOHXRi7OKnklXw&sig2=5yZbsQyVD6-BK7DlhRaYkg) Probably the best IRC client for the Mac. Well designed and extremely extensible.
*   [Thunderbird](https://www.mozillamessaging.com/en-US/thunderbird/) A great alternative to the default Mail application.</p>

### Productivity

*   Gimp Because the Mac doesn't come with built-in image editing software of any kind, Gimp, the open-source alternative to Photoshop, is a handy install.
*   [Textmate](https://macromates.com/) Probably the most popular text editor for the Mac. It's a hefty $50 but worth every penny.
*   [Sketchbox](https://www.omz-software.de/sketchbox/) An improvement to OS X's Stickies.</p>

## Conclusion

So, there you have it, some configurations, hacks and applications that will make your transition easier. As you make your way on your journey switching over, remember to seek out other Mac users, specifically other switchers, when you have questions or need advice. And as always, check Smashing Magazine regularly for more helfpul Mac guides, articles and resources.

{{< signature "al" >}}

