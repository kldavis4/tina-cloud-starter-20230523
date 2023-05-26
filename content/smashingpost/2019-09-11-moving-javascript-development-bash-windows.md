---
title: 'Moving Your JavaScript Development To Bash On Windows'
slug: moving-javascript-development-bash-windows
author: burke-holland
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9d1d3c8-7e0c-490a-a7de-d3b90895494d/moving-javascript-development-bash-windows.png
date: 2019-09-11T12:30:59+02:00
summary: >-
  Love your Bash terminal but also love your PC? Maybe you’ve had your eye on some of that new Surface hardware, but can’t make the switch without your terminal. Now you can have Windows and Bash. In this article, we’ll take an in-depth look at how to set up a Windows/Linux development box for JavaScript development.
description: >-
  Love your Bash terminal but also love your PC? Maybe you’ve had your eye on some of that new Surface hardware, but can’t make the switch without your terminal. Now you can have Windows and Bash. In this article, we’ll take an in-depth look at how to set up a Windows/Linux development box for JavaScript development.
categories:
  - JavaScript
---
I'm one of those people who can't live without their Bash terminal. This sole fact has made it difficult for me to do frontend work on Windows. I work at Microsoft and I'm on a Mac. It wasn't until the new Surface hardware line came out a few years ago that I realized: **I gotta have one of those**.

So I got one. A Surface Book 2 running Windows 10 to be exact. I’m drafting this article on it right now. And what of my sweet, sweet Bash prompt? Well, I brought it along with me, of course.

In this article, I’m going to take an in-depth look at how new technology in Windows 10 enables you to run a full Linux terminal on Windows. I’ll also show you my amazing terminal setup (which was named “best ever” by “me”) and how you too can set up your very own Windows/Linux development machine.

If you’ve been craving some of that Surface hardware but can’t live without a Linux terminal, you’ve come to the right place.

**Note**: *At the time of this writing, a lot of the items in this article will require you to use or switch to “preview” or “insiders” builds of various items, including Windows. Most of these things will be in the main Windows build at some point in the future.*

{{% feature-panel %}}

## Windows Subsystem For Linux (WSL)

The [Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10?WT.mc_id=smashingmag-article-buhollan), or, “WSL” is what enables you to run Linux on Windows. But what exactly *is* this mad science?

The WSL, in its current incarnation, is a translation layer that converts Linux system calls into Windows system calls. Linux runs on top of the WSL. That means that in order to get Linux on Windows, you need to do three things:

1. Enable the WSL,
2. Install Linux,
3. Always include three items in a list.

As it turns out, that translation layer is a tad on the slow side &mdash; kind of like me trying to remember if I need `splice`  or `slice`. This is especially true when the WSL is reading and writing to the file system. That’s kind of a big problem for web developers since any proper  `npm install` will copy thousands of files to your machine. I mean, I don’t know about you, but I’m not going to left-pad my *own* strings.

[Version 2 of the WSL](https://docs.microsoft.com/windows/wsl/wsl2-install?WT.mc_id=smashingmag-article-buhollan) is a different story. It is considerably faster than the current version because it leverages a virtualization core in Windows instead of using the translation layer. When I say it’s “considerably faster”, I mean way, way faster. Like as fast as me Googling “splice vs slice”.

For that reason, I’m going to show how to install the WSL 2. At the time of writing, that is going to require you to be on the “Insider” build of Windows. 

First things first: [follow this short guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10?WT.mc_id=smashingmag-article-buhollan) to enable the WSL on Windows 10 and check your Windows version number.

Once you have it installed, hit the Windows key and type “windows insider”. Then choose “Windows Insider Program Settings”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37198e05-1543-47a1-923a-547d98288145/js-dev-bash-windowswindows-insiders-start.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37198e05-1543-47a1-923a-547d98288145/js-dev-bash-windowswindows-insiders-start.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37198e05-1543-47a1-923a-547d98288145/js-dev-bash-windowswindows-insiders-start.png'>Large preview</a>)" alt="Windows Insider Program settings menu option" >}}

You’ll have a couple of different options as to which “ring” you want to be on. A lot of people I know are on the fast ring. I’m a cautious guy, though. When I was a kid I would go down the slide at the playground on my stomach holding on to the sides. Which is why I stay on the slow ring. I’ve been on it for several months now, and I find it to be no more disruptive or unstable than regular Windows. 

It’s a good option if you want the WSL 2, but you don't want to die on the slide.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9829ae58-c6e4-4008-8362-106b969c790c/js-dev-bash-windowsinsider-slow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9829ae58-c6e4-4008-8362-106b969c790c/js-dev-bash-windowsinsider-slow.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9829ae58-c6e4-4008-8362-106b969c790c/js-dev-bash-windowsinsider-slow.png'>Large preview</a>)" alt="Windows Insider settings screen showing “Slow” ring" >}}

**Note**: *After publishing this article, I learned that WSL 2 is not in fact on the slow ring. You'll need to be on the fast ring to get it. I must have been on the fast ring at some point in the process of writing this article. So fast ring it is. Good luck on the slide!*

Next, you need to enable the “Virtual Machine Platform” feature in Windows, which is required by the WSL version 2. To get to this screen, press the Windows key and type “windows features”. Then select “Turn Windows Features on or off”. Select “Virtual Machine Platform”. The “Windows Subsystem for Linux” option should already be enabled.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99e5d3f3-44c8-414c-9e6e-cc256eab1bb3/js-dev-bash-windowsturn-on-windows-features.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99e5d3f3-44c8-414c-9e6e-cc256eab1bb3/js-dev-bash-windowsturn-on-windows-features.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99e5d3f3-44c8-414c-9e6e-cc256eab1bb3/js-dev-bash-windowsturn-on-windows-features.png'>Large preview</a>)" alt="The “Windows Features” screen with “Virtual Machine Platform” and “Windows Subsystem for Linux” highlighted" >}}

Now that the WSL is enabled, you can install Linux. You do this, ironically enough, directly from the Windows Store. Only in 2019 would I suggest that you “install Linux from the Windows store”. 

There are several different distributions to choose from, but Ubuntu is going to be the most supported across all the tools we’ll configure later on &mdash; including VS Code. All of the instructions that come from here on out with assume a Ubuntu install. If you install a different distro, all bets are off.

Search for “Ubuntu” from the Windows Store. There will be three to choose from: Ubuntu, Ubuntu 18.04, and Ubuntu 16.04. Ubuntu really likes that 04 minor version number, don’t they?

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9aaa2c1-f583-473c-9179-0a94f895237a/js-dev-bash-windowslinux-windows-store.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9aaa2c1-f583-473c-9179-0a94f895237a/js-dev-bash-windowslinux-windows-store.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9aaa2c1-f583-473c-9179-0a94f895237a/js-dev-bash-windowslinux-windows-store.png'>Large preview</a>)" alt="The “Ubuntu” item in the Windows Store" >}} 

<p class="c-pre-sidenote--left">The “Ubuntu” distro (the first one in this screenshot) is the “meta version”, or rather a placeholder that just points to the latest version. As of right now, that’s 18.04.</p><p class="c-sidenote c-sidenote--right">I went with the meta version because later on I’ll show you how to browse the Linux file system with Windows Explorer and it’s kinda messy to have “Ubuntu 18.04” as a drive name vs just “Ubuntu”.</p>

This install is pretty quick depending on your internet connection. It’s only about 215 megabytes, but I am on a gigabit connection over here and how do you know if someone is on a gigabit connection? Don’t worry, they’ll tell you.

Once installed, you’ll now have an “Ubuntu” app in your start menu.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c5d7fd6-3e77-46cc-80e1-6f7e913eebcc/js-dev-bash-windowsubuntu-start-menu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c5d7fd6-3e77-46cc-80e1-6f7e913eebcc/js-dev-bash-windowsubuntu-start-menu.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c5d7fd6-3e77-46cc-80e1-6f7e913eebcc/js-dev-bash-windowsubuntu-start-menu.png'>Large preview</a>)" alt="Ubuntu installed and showing up in the Windows Start menu" >}}

If you click on that, you’ll get a Bash terminal!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50d2559a-b4b1-4f2a-aa3e-6ef1c0f92270/js-dev-bash-windowsubuntu-terminal.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50d2559a-b4b1-4f2a-aa3e-6ef1c0f92270/js-dev-bash-windowsubuntu-terminal.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50d2559a-b4b1-4f2a-aa3e-6ef1c0f92270/js-dev-bash-windowsubuntu-terminal.png'>Large preview</a>)" alt="The Ubuntu terminal running on Windows" >}}

Take a moment to bask in the miracle of technology. 

By default, you’ll be running in the WSL version 1. To upgrade to version 2, you’ll need to open a PowerShell terminal and run a command.

Hit the “Windows” key and type “Powershell”.  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15985770-de7b-4942-b07d-52f9fb368874/js-dev-bash-windowsstart-menu-powershell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15985770-de7b-4942-b07d-52f9fb368874/js-dev-bash-windowsstart-menu-powershell.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15985770-de7b-4942-b07d-52f9fb368874/js-dev-bash-windowsstart-menu-powershell.png'>Large preview</a>)" alt="The “Powershell” item in the start menu" >}}

From the PowerShell terminal, you can see which version of the WSL you have by executing `wsl --list --verbose`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7983c40a-c73c-4049-b5ae-38ab246259db/js-dev-bash-windowswsl-list-verbose.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7983c40a-c73c-4049-b5ae-38ab246259db/js-dev-bash-windowswsl-list-verbose.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7983c40a-c73c-4049-b5ae-38ab246259db/js-dev-bash-windowswsl-list-verbose.png'>Large preview</a>)" alt="Doing a verbose list of all WSL instances running from within Powershell" >}}

If you’re showing version 1, you’ll need to execute the `--set-version` command and specify the name of the instance (Ubuntu) and the version you want (2).

<pre><code class="language-bash">wsl --set-version Ubuntu 2
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71039929-d983-415b-bf06-0631abc0422b/js-dev-bash-windowswsl-set-version.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71039929-d983-415b-bf06-0631abc0422b/js-dev-bash-windowswsl-set-version.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71039929-d983-415b-bf06-0631abc0422b/js-dev-bash-windowswsl-set-version.png'>Large preview</a>)" alt="Setting the version of WSL to version 2 with Powershell" >}}

This is going to take a bit, depending on how much meat your machine has. Mine took “some minutes” give or take. When it’s done, you’ll be on the latest and greatest version of the WSL. 

{{% ad-panel-leaderboard %}}

## The Is Your Brain On Linux... On Windows.

Linux is not Windows. WSL is not a bash prompt on top of a Windows operating system. It is a full operating system unto itself with its own folder structure and installed applications. If you install Node with the Windows installer, typing `node` in Linux is going to fail because Node is not installed in Linux. It’s installed on Windows. 

The true magic of the WSL, though, lies in the way it seamlessly connects Windows and Linux so that they appear as one file system on your machine.

### File And Folder Navigation

By default, the Ubuntu terminal drops you into your Linux home directory (or `/home/your-user-name`). You can move onto the Windows side by going to `/mnt/c`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd1606f2-ee3c-4cb1-9de4-6608eb384e69/js-dev-bash-windowsbrowse-d-drive.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd1606f2-ee3c-4cb1-9de4-6608eb384e69/js-dev-bash-windowsbrowse-d-drive.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd1606f2-ee3c-4cb1-9de4-6608eb384e69/js-dev-bash-windowsbrowse-d-drive.png'>Large preview</a>)" alt="The Ubuntu terminal with the contents for the C drive listed out" >}}

Notice that some permissions are denied here. I would have to right-click the Ubuntu icon and click “Run as Administrator” to get access to these files. This how Windows does elevated permissions. There is no sudo on Windows.

### Launching Applications

You can launch any Windows application from the Ubuntu terminal. For instance, I can open Windows Explorer from the Unbuntu terminal. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4450cc85-cf65-4813-8cf2-fe6fe5940904/js-dev-bash-windowsopen-explorer-from-linux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4450cc85-cf65-4813-8cf2-fe6fe5940904/js-dev-bash-windowsopen-explorer-from-linux.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4450cc85-cf65-4813-8cf2-fe6fe5940904/js-dev-bash-windowsopen-explorer-from-linux.png'>Large preview</a>)" alt="The Windows Explorer and the the Ubuntu terminal" >}}

This also works in reverse. You can execute any application installed on the Linux side. Here I am executing “fortune” installed in Linux from the Windows command line. (Because it ain’t a proper Linux install without random, meaningless fortunes.)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db839a12-49eb-41ca-840b-0a3eb03d3e44/js-dev-bash-windowswsl-fortune.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db839a12-49eb-41ca-840b-0a3eb03d3e44/js-dev-bash-windowswsl-fortune.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db839a12-49eb-41ca-840b-0a3eb03d3e44/js-dev-bash-windowswsl-fortune.png'>Large preview</a>)" alt="The Windows Command Line executing the Linux “fortune” program" >}}

Two different operating systems. Two different file systems. Two different sets of installed applications. See how this could get confusing? 

In order to keep everything straight, I recommend that you keep all your JavaScript development files and tools installed on the Linux side of things. That said, the ability to move between Windows and Linux and access files from both systems is the core magic of the WSL. Don't forget it, cause it's what makes this whole setup better than just a standard Linux box.

## Setting Up Your Development Environment

From here on out, I’m going to give you a list of opinionated items for what I think makes a killer Linux on Windows setup. Just remember: my opinions are just that. *Opinions*. It just happens that just like all my opinions, they are 100% correct.

## Getting A Better Terminal

Yes, you got a terminal when you installed Ubuntu. It’s actually the Windows Console connected to your Linux distro. It’s not a bad console. You can resize it, turn on copy/paste (in settings). But you can’t do things like tabs or open new windows. Just like a lot of people use replacement terminal programs on Mac (I use Hyper), there are other options for Windows as well. The [Awesome WSL](https://github.com/sirredbeard/Awesome-WSL#terminals) list on Github contains a pretty exhaustive list.

Those are all fine emulators, but there is a new option that is built by people who know Windows pretty well.

Microsoft has been working on a new application called “[Windows Terminal](https://www.microsoft.com/p/windows-terminal-preview/9n0dx20hk701?activetab=pivot:overviewtab&WT.mc_id=smashingmag-article-buhollan)”. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/014d8229-9fcd-4066-b478-049968ce144d/js-dev-bash-windowswindows-terminal-store.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/014d8229-9fcd-4066-b478-049968ce144d/js-dev-bash-windowswindows-terminal-store.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/014d8229-9fcd-4066-b478-049968ce144d/js-dev-bash-windowswindows-terminal-store.png'>Large preview</a>)" alt="The Windows Terminal item  in the Windows Store" >}}

Windows Terminal can be installed from the [Windows Store](https://www.microsoft.com/p/windows-terminal-preview/9n0dx20hk701?activetab=pivot:overviewtab&WT.mc_id=smashingmag-article-buhollan) and is currently in preview mode. I’ve been using it for quite a while now, and it has enough features and is stable enough for me to give it a full-throated endorsement.

The new Windows Terminal features a full tab interface, copy/paste, multiple profiles, transparent backgrounds, background images &mdash; even transparent background images. It’s a field day if you like to customize your terminal, and I came to win this sack race.

Here is my current terminal. We’ll take a walk through some of the important tweaks here.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4df1def-f68e-41fe-8091-a99b941934d7/js-dev-bash-windowsmy-current-terminal.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4df1def-f68e-41fe-8091-a99b941934d7/js-dev-bash-windowsmy-current-terminal.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4df1def-f68e-41fe-8091-a99b941934d7/js-dev-bash-windowsmy-current-terminal.png'>Large preview</a>)" alt="The author’s current terminal: Dark blue background with a cartoon planet in the bottom right-hand corner. Green and white text." >}}

Windows terminal is quite customizable. Clicking the “<span class="red"><strong>&#8964;</strong></span>” arrow at the top left (next to the “<span class="red"><strong>&plus;</strong></span>” sign) gives you access to “Settings”. This will open a JSON file.

## Bind Copy/Paste

At the top of the file are all of the key bindings. The first thing that I did was map “copy” to <kbd>Ctrl + C</kbd> and paste to <kbd>Ctrl + V</kbd>. How else am I going to copy and paste in commands from Stack Overflow that I don’t understand?

<pre><code class="language-bash">{
  "command": "copy",
  "keys": ["ctrl+c"]
},
{
  "command": "paste",
  "keys": ["ctrl+v"]
},
</code></pre>

The problem is that <kbd>Ctrl + C</kbd> is already mapped to SIGINT, or the Interrupt/kill command on Linux. There are a lot of terminals out there for Windows that handle this by mapping Copy/Paste to <kbd>Ctrl + Shift + C</kbd> and <kbd>Ctrl + Shift + V</kbd> respectively. The problem is that copy/paste is <kbd>Ctrl + C</kbd> / <kbd>Ctrl + V</kbd> every other single place in Windows. I just kept pressing <kbd>Ctrl + C</kbd> in the terminal over and over again trying to copy things. I could not stop doing it.

The Windows terminal handles this differently. If you have text highlighted and you press <kbd>Ctrl + C</kbd>, it will copy the text. If there is a running process, it still sends the SIGINT command down and interrupts it. The means that you can safely map <kbd>Ctrl + C</kbd> / <kbd>Ctrl + V</kbd> to Copy/Paste in the Windows Terminal and it won’t interfere with your ability to interrupt processes.

Whoever thought Copy/Paste could cause so much heartache?

{{% ad-panel-leaderboard %}}

## Change The Default Profile

The default profile is what comes up when a new tab is opened. By default, that’s Powershell. You’ll want to scroll down and find the Linux profile. This is the one that opens `wsl.exe -d Ubuntu`. Copy its GUID and paste it into the `defaultProfile` setting.

I’ve moved these two settings so they are right next to each other to make it easier to see:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be71fbef-dc45-4763-9fc8-4e5105acd4d9/js-dev-bash-windowsset-default-profile.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be71fbef-dc45-4763-9fc8-4e5105acd4d9/js-dev-bash-windowsset-default-profile.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be71fbef-dc45-4763-9fc8-4e5105acd4d9/js-dev-bash-windowsset-default-profile.png'>Large preview</a>)" alt="The default Terminal profile highlighted in the settings.json file" >}}

## Set The Background

I like my background to be a dark solid color with a flat-ish logo in the right-hand corner. I do this because I want the logo to be bright and visible, but not in the way of the text. This one I made myself, but there is a great collection of flat images to pick from at [Simple Desktops](https://simpledesktops.com/).

The background is set with the `backgroundImage` property:

<pre><code class="language-bash">"backgroundImage": "c:/Users/YourUserName/Pictures/earth.png"
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49339f19-e238-4fb0-aaa7-f003fc4746bd/js-dev-bash-windowsterminal-background.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49339f19-e238-4fb0-aaa7-f003fc4746bd/js-dev-bash-windowsterminal-background.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49339f19-e238-4fb0-aaa7-f003fc4746bd/js-dev-bash-windowsterminal-background.png'>Large preview</a>)" alt="A blue sqaure image with a cartoon planet in the bottom right-hand corner" >}}

You’ll also notice a setting called “acrylic”. This is what enables you to adjust the opacity of the background. If you have a solid background color, this is pretty straightforward.

<pre><code class="language-bash">"background": "#336699",
"useAcrylic": true,
"acrylicOpacity": 0.5
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db780c6b-1269-4109-bc62-ef5d321ab290/js-dev-bash-windowsacrylic-solid.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db780c6b-1269-4109-bc62-ef5d321ab290/js-dev-bash-windowsacrylic-solid.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db780c6b-1269-4109-bc62-ef5d321ab290/js-dev-bash-windowsacrylic-solid.png'>Large preview</a>)" alt="The terminal with the background slightly transparent" >}}

You can pull this off with a background image as well, by combining the `arcylicOpacity` setting with the `backgroundImageOpacity`:

<div class="break-out">

 <pre><code class="language-bash">"backgroundImage": "c:/Users/username/Pictures/earth-and-stars.png",
"useAcrylic": true,
"acrylicOpacity": 0.5
</code></pre>
</div>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1021f0fc-bcf4-4248-a081-8737254fba06/js-dev-bash-windowsearth-transparent.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1021f0fc-bcf4-4248-a081-8737254fba06/js-dev-bash-windowsearth-transparent.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1021f0fc-bcf4-4248-a081-8737254fba06/js-dev-bash-windowsearth-transparent.png'>Large preview</a>)" alt="The terminal with both a transparent image and a trasparent background" >}}

For my theme, transparency makes everything look muted, so I keep the `useAcrylic` set to `false`.

## Change The Font

The team building the Windows Terminal is also working on a new font called “Cascadia Code”. It’s not available as of the time of this writing, so you get the default Windows font instead.

The default font in the Windows Terminal is “Consolas”. This is the same font that the Windows command line uses. If you want that true Ubuntu feel, [Chris Hoffman](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) points out how you can install the official [Ubuntu Mono font](https://design.ubuntu.com/font/).

Here’s a before and after so you can see the difference:

<pre><code class="language-bash">"fontFace": "Ubuntu Mono"
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b4550d7-1f44-467a-890b-25f9f62c76c4/js-dev-bash-windowsubuntu-vs-consolas-mono.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b4550d7-1f44-467a-890b-25f9f62c76c4/js-dev-bash-windowsubuntu-vs-consolas-mono.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b4550d7-1f44-467a-890b-25f9f62c76c4/js-dev-bash-windowsubuntu-vs-consolas-mono.png'>Large preview</a>)" alt="A side-by-side comparison of Consolas and Unbuntu Mono fonts in the terminal" >}}

They look pretty similar; the main difference being in the spacing of Ubuntu Mono which makes the terminal just a bit tighter and cleaner.

## Color Schemes

The color schemes are all located at the bottom of the settings file. I copied the “Campbell” color scheme as a baseline. I try to match colors with their names, but I’m not afraid to go rogue either. I’ll map “#ffffff” to “blue” &mdash; I don’t even care. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/061b238b-dbdf-455a-b999-d9e9c6de23ec/js-dev-bash-windowscolor-scheme.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/061b238b-dbdf-455a-b999-d9e9c6de23ec/js-dev-bash-windowscolor-scheme.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/061b238b-dbdf-455a-b999-d9e9c6de23ec/js-dev-bash-windowscolor-scheme.png'>Large preview</a>)" alt="The color scheme settings from the settings.json file" >}}

If you like this particular scheme which I’ve named “Earth”, I’ve put together [this gist](https://gist.github.com/burkeholland/314e5fbcd759ff4f4193eacbad191e0a) so you don’t have to manually copy all of this mess out of a screenshot.

**Note**: *The color previews come by virtue of the “[Color Highlight](https://marketplace.visualstudio.com/items?itemName=naumovs.color-highlight)” extension for VS Code.*

## Change The Default Starting Directory

By default, the WSL profile drops you into your home directory on the Windows side. Based on the setup that I am recommending in this article, it would be preferable to be dropped into your Linux `home` folder instead. To do that, alter the `startingDirectory` setting in your “Ubuntu” profile:

<pre><code class="language-bash">"startingDirectory": "\\\\wsl$\\Ubuntu\\home\\burkeholland"
</code></pre>

Note the path there. You can use this path (minus the extra escape slashes) to access the WSL from the Windows command line.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4302ca96-75cb-456e-a800-218f2ac5c68f/js-dev-bash-windowsaccess-wsl-from-command-line.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4302ca96-75cb-456e-a800-218f2ac5c68f/js-dev-bash-windowsaccess-wsl-from-command-line.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4302ca96-75cb-456e-a800-218f2ac5c68f/js-dev-bash-windowsaccess-wsl-from-command-line.png'>Large preview</a>)" alt="A “dir” command run against the Linux home directory from the Windows Command Line" >}}

## Install Zsh/Oh-My-Zsh

If you’ve never used [Zsh](https://zsh.sourceforge.net/) and [Oh-My-Zsh](https://ohmyz.sh/) before, you’re in for a real treat. Zsh (or “Z Shell”) is a replacement shell for Linux. It expands on the basic capabilities of Bash, including implied directory switching (no need to type `cd`), better-theming support, better prompts, and much more.

To install Zsh, grab it with the apt package manager, which comes out of the box with your Linux install:

<pre><code class="language-bash">sudo apt install zsh
</code></pre>

Install oh-my-zsh using curl. Oh-my-zsh is a set of configurations for zsh that improve the shell experience even further with plugins, themes and a myriad of keyboard shortcuts.

<div class="break-out">

 <pre><code class="language-bash">sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
</code></pre>
</div>

Then it will ask you if you want to change your default shell to Zsh. You do, so answer in the affirmative and you are now up and running with Zsh and Oh-My-Zsh.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01831223-cc04-45b2-8e16-fda3a1fea89e/js-dev-bash-windowschange-default-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01831223-cc04-45b2-8e16-fda3a1fea89e/js-dev-bash-windowschange-default-shell.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01831223-cc04-45b2-8e16-fda3a1fea89e/js-dev-bash-windowschange-default-shell.png'>Large preview</a>)" alt="The terminal asking if you would like to change the default shell" >}}

You’ll notice that the prompt is a lot cleaner now. You can change the look of that prompt by changing the theme in the `~/.zshrc` file.

Open it with `nano`, which is kind of like VIM, but you can edit things and exit when you need to.

<pre><code class="language-bash">nano ~/.zshrc
</code></pre>

Change the line that sets the theme. There is a URL above it with an entire list of themes. I think the “cloud” one is nice. And cute.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b39cd27-0ce2-48dd-aab7-df7f793bfdd0/js-dev-bash-windowszsh-theme-cloud.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b39cd27-0ce2-48dd-aab7-df7f793bfdd0/js-dev-bash-windowszsh-theme-cloud.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b39cd27-0ce2-48dd-aab7-df7f793bfdd0/js-dev-bash-windowszsh-theme-cloud.png'>Large preview</a>)" alt="The “cloud” theme being set in the zshrc file" >}}

To get changes to the `.zshrc` picked up, you’ll need to source it:

<pre><code class="language-bash">source ~/.zshrc
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468a5de3-f65d-4661-8ac0-77b1cf8906c7/js-dev-bash-windowscloud-theme.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468a5de3-f65d-4661-8ac0-77b1cf8906c7/js-dev-bash-windowscloud-theme.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468a5de3-f65d-4661-8ac0-77b1cf8906c7/js-dev-bash-windowscloud-theme.png'>Large preview</a>)" alt="The “cloud” theme prompt" >}}

**Note**: *If you pick a theme like “agnoster” which requires glyphs, you’ll need a powerline infused version of Ubuntu Mono that has... glyphs. Otherwise, your terminal will just be full of weird characters like you mashed your face on the keyboard. [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/UbuntuMono/Regular/complete/Ubuntu%20Mono%20Nerd%20Font%20Complete.ttf) offers one that seems to work pretty well.* 

Now you can do things like changing directories just by entering the directory name. No `cd` required. Wanna go back up a directory? Just do a `..`. You don’t even have to type the whole directory name, just type the first few letters and hit tab. Zsh will give you a list of all of the files/directories that match your search and you can tab through them. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee42d6a8-8831-4f62-be28-0e3668a8de50/js-dev-bash-windowstab-through-results.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee42d6a8-8831-4f62-be28-0e3668a8de50/js-dev-bash-windowstab-through-results.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee42d6a8-8831-4f62-be28-0e3668a8de50/js-dev-bash-windowstab-through-results.png'>Large preview</a>)" alt="The terminal with one of many paths highlighted" >}}

## Installing Node

As a web developer, you’re probably going to want to install Node. I suppose you don’t *have* to install Node to do web development, but it sure feels like it in 2019!

Your first instinct might be to install node with `apt`, which you can do, but you would regret it for two reasons:

1. The version of Node on apt is dolorously out of date;
2. You should install Node with a version manager so that you don’t run into permissions issues.

The best way to solve both of these issues is to install nvm (Node Version Manager). Since you’ve installed `zsh`, you can just add the nvm plugin in your zshrc file and zsh takes care of the rest. 

First, install the plugin by cloning in the `zsh-nvm` repo. (Don’t worry, Git comes standard on your Ubuntu install.)

<div class="break-out">

 <pre><code class="language-bash">git clone https://github.com/lukechilds/zsh-nvm ~/.oh-my-zsh/custom/plugins/zsh-nvm
</code></pre>
</div>

Then add it as a plugin in the `~/.zshrc` file.

<pre><code class="language-bash">`nano ~/.zshrc`

plugins (zsh-nvm git)
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfdd51d9-4a95-4d12-8b7f-9e4653466e76/js-dev-bash-windowszsh-nvm-plugin.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfdd51d9-4a95-4d12-8b7f-9e4653466e76/js-dev-bash-windowszsh-nvm-plugin.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfdd51d9-4a95-4d12-8b7f-9e4653466e76/js-dev-bash-windowszsh-nvm-plugin.png'>Large preview</a>)" alt="The zshrc file with the zsh-vnm-plugin added" >}}

Remember to source the zshrc file again with `source ~/.zshrc` and you’ll see nvm being installed.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f452abc6-e973-4aa5-a071-61b9954a629c/js-dev-bash-windowsnvm-installed.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f452abc6-e973-4aa5-a071-61b9954a629c/js-dev-bash-windowsnvm-installed.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f452abc6-e973-4aa5-a071-61b9954a629c/js-dev-bash-windowsnvm-installed.png'>Large preview</a>)" alt="The terminal showing the install progress of nvm" >}}

Now you can install node with nvm. It makes it easy to install multiple side-by-side versions of node, and switch between them effortlessly. Also, no permissions errors when you do global npm installs! 

<pre><code class="language-bash">nvm install --lts
</code></pre>

I recommend this over the standard nvm install because the plugin gives you the ability to easily upgrade nvm. This is kind of a pain with the standard "curl” install. It’s one command with the plugin.

<pre><code class="language-bash">nvm upgrade
</code></pre>

## Utilize Auto Suggestions

One of my very favorite plugins for zsh is zsh-autosuggestions. It remembers things you have typed in the terminal before, and then recognizes them when you start to type them again as well as “auto-suggests” the line you might need. This plugin has come in handy more times than I can remember &mdash; specifically when it comes to long CLI commands that I have used in the past, but can’t ever remember.

Clone the repo into the zsh extensions folder:

<div class="break-out">

 <pre><code class="language-bash">git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
</code></pre>
</div>

Then add it to your zsh plugins and source the zshrc file:

<pre><code class="language-bash">nano ~/.zshrc

# In the .zshrc file
plugins(zsh-nvm zsh-autosuggestions git)

source ~/.zshrc
</code></pre>

The plugin reads your zsh history, so start typing some command you’ve typed before and watch the magic. Try typing the first part of that long clone command above.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f289f9-6db1-49d9-90d7-7816fb1bdd2a/js-dev-bash-windowsauto-suggestions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f289f9-6db1-49d9-90d7-7816fb1bdd2a/js-dev-bash-windowsauto-suggestions.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f289f9-6db1-49d9-90d7-7816fb1bdd2a/js-dev-bash-windowsauto-suggestions.png'>Large preview</a>)" alt="The terminal showing zsh autosuggestions auto completing a git clone command" >}}

If you hit <kbd>↹</kbd>, it will autocomplete the command. If you keep hitting <kbd>↹</kbd>, it will cycle through any of the commands in your history that could be a match.

## Important Keyboard Shortcuts

There are a few terminal shortcuts that I use all the time. I find this with all of my tools &mdash; including VS Code. Trying to learn all the shortcuts is a waste of time because you won’t use them enough to remember them.

Here are a few that I use regularly:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">Terminal Shortcut</th>
            <th>What does it do?</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><kbd>Ctrl</kbd> + <kbd>L</kbd></td>
            <td>This clears the terminal and puts you back to the top. It’s the equivilant of typing “clear”.</td>
        </tr>
        <tr>
            <td><kbd>Ctrl</kbd> + <kbd>U</kbd></td>
            <td>This clears out the current line only. </td>
        </tr>
        <tr>
            <td><kbd>Ctrl</kbd> + <kbd>A</kbd></td>
            <td>Sends the cursor to the beginning of the command line.</td>
        </tr>
        <tr>
            <td><kbd>Ctrl</kbd> + <kbd>E</kbd></td>
            <td>Move to the end of the line.</td>
        </tr>
        <tr>
            <td><kbd>Ctrl</kbd> + <kbd>K</kbd></td>
            <td>Delete all the characters after the cursor.</td>
        </tr>
    </tbody>
</table>

That’s it! Everything else I’ve probably learned and then forgotten because it never gets any use.

## Configuring Git(Hub/Lab/Whatevs)

Git comes on Ubuntu, so there is no install required. You can [follow the instructions](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) at your source control hoster of choice to get your ssh keys created and working. 

Note that in the Github instructions, it tells you to use the “copy” utility to copy your ssh key. Ubuntu has the “xcopy” command, but it’s not going to work here because there is no interop between the Linux and Windows in terms of a clipboard.

Instead, you can just use the Windows Clipboard executable and call it directly from the terminal. You need to get the text first with `cat`, and then pipe that to the Windows clipboard.

<pre><code class="language-bash">cat ~/.ssh/id_rsa.pub | clip.exe 
</code></pre>

The [Github docs](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) tell you to make sure that the `ssh-agent` is running. It’s not. You’ll see this when you try and add your key to the agent:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6311d5-afb1-4f27-9414-37ea5f685a36/js-dev-bash-windowsssh-agent-not-running.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6311d5-afb1-4f27-9414-37ea5f685a36/js-dev-bash-windowsssh-agent-not-running.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a6311d5-afb1-4f27-9414-37ea5f685a36/js-dev-bash-windowsssh-agent-not-running.png'>Large preview</a>)" alt="The terminal showing that the ssh agent is not running" >}}

You can start the agent, but the next time you reboot Windows or the WSL is stopped, you’ll have to start it again. This is because there is no initialization system in the WSL. There is no `systemd` or another process that starts all of your services when the WSL starts. WSL is still in preview, and the team is working on a solution for this.

In the meantime, believe it or not, there’s a zsh plugin for this, too. It’s called `ssh-agent`, and it comes installed with oh-my-zsh, so all you need to do is reference it in the `.zshrc` file.

<pre><code class="language-bash">zsh-nvm zsh-autosuggestions ssh-agent git
</code></pre>

This will start the ssh-agent automatically if it’s not running the first time that you fire up the WSL. The downside is that it’s going to ask you for your passphrase every time WSL is started fresh. That means essentially anytime you reboot your computer.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/007d049c-5c52-40bc-aec3-e2fb6ebf1206/js-dev-bash-windowsssh-plugin-password.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/007d049c-5c52-40bc-aec3-e2fb6ebf1206/js-dev-bash-windowsssh-plugin-password.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/007d049c-5c52-40bc-aec3-e2fb6ebf1206/js-dev-bash-windowsssh-plugin-password.png'>Large preview</a>)" alt="The terminal prompting for the passphrase for the rsa key" >}}

## VS Code And The WSL

The WSL has no GUI, so you can’t install a visual tool like VS Code. That needs to be installed on the Windows side. This presents a problem because you have a program running on the Windows side accessing files on the Linux side, and this can result in all manor of quirks and “permission denied” issues. As a general rule of thumb, **Microsoft recommends that you not alter files in the WSL side with Windows programs.**

To resolve this, there is an extension for VS Code called “[Remote WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl&WT.mc_id=smashingmag-article-buhollan)”. This extension is made by Microsoft, and allows you to develop within the WSL, but from inside of VS Code.

Once the extension is installed, you can attach VS Code directly to the Ubuntu side by opening the Command Palette (<lbd>Ctrl + Shift + P</kbd>) and select “Remote-WSL: New Window”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e7c695-43f2-44d2-9708-52e625ed11b2/js-dev-bash-windowswsl-new-window.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e7c695-43f2-44d2-9708-52e625ed11b2/js-dev-bash-windowswsl-new-window.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e7c695-43f2-44d2-9708-52e625ed11b2/js-dev-bash-windowswsl-new-window.png'>Large preview</a>)" alt="VS Code with the “Remote WSL: New Window” command highlighted in the Command Palette" >}}

This opens a new instance of VS Code that allows you to work as if you were fully on the Linux side of things. Doing “File/Open” browses the Ubuntu file system instead of the Windows one.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5148d88-de89-4721-b8ef-ed74ea0e9b33/js-dev-bash-windowsvs-code-open-file.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5148d88-de89-4721-b8ef-ed74ea0e9b33/js-dev-bash-windowsvs-code-open-file.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5148d88-de89-4721-b8ef-ed74ea0e9b33/js-dev-bash-windowsvs-code-open-file.png'>Large preview</a>)" alt="The VS Code “Open File” view" >}}

The integrated terminal in VS Code opens your beautifully customized zsh setup. Everything “just works” like it should when you have the Remote WSL extension installed.

If you open code from your terminal with `code .`, VS Code will automatically detect that it was opened from the WSL, and will auto-attach the Remote WSL extension.

## VS Code Extensions With Remote WSL

The Remote WSL extension for VS Code works by setting up a little server on the Linux side, and then connecting to that from VS Code on the Windows side. That being the case, the extensions that you have installed in VS Code won’t automatically show up when you open a project from the WSL.

For instance, I have a Vue project open in VS Code. Even though I have all of the right Vue extensions installed for syntax highlighting, formatting and the like, VS Code acts like it’s never seen a `.vue` file before.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/467b159d-e214-40f7-b00c-79d6d4c15d38/js-dev-bash-windowswhat-vue.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/467b159d-e214-40f7-b00c-79d6d4c15d38/js-dev-bash-windowswhat-vue.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/467b159d-e214-40f7-b00c-79d6d4c15d38/js-dev-bash-windowswhat-vue.png'>Large preview</a>)" alt="A .vue file open in VS Code with no syntax highlighting" >}}

All of the extensions that you have installed can be enabled in the WSL. Just find the extension that you want in the WSL, and click the “Install in WSL” button.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ec9e2c0-7210-4e98-b3b6-5194aae393d6/js-dev-bash-windowsinstall-in-wsl.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ec9e2c0-7210-4e98-b3b6-5194aae393d6/js-dev-bash-windowsinstall-in-wsl.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ec9e2c0-7210-4e98-b3b6-5194aae393d6/js-dev-bash-windowsinstall-in-wsl.png'>Large preview</a>)" alt="The Vetur VS Code extension landing page in VS Code" >}}

All of the extensions installed in the WSL will show up in their own section in the Extensions Explorer view. If you have a lot of extensions, it could be slightly annoying to install each one individually. If you want to just install every extension you’ve got in the WSL, click the little cloud-download icon at the top of the ‘Local - Installed’ section.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed364b3e-3df3-4a3a-bc45-dc5960169b9c/js-dev-bash-windowsinstalled-extensions.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed364b3e-3df3-4a3a-bc45-dc5960169b9c/js-dev-bash-windowsinstalled-extensions.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed364b3e-3df3-4a3a-bc45-dc5960169b9c/js-dev-bash-windowsinstalled-extensions.png'>Large preview</a>)" alt="The Extensions view in VS Code with the install all extensions in WSL icon highlighted" >}}

## How To Setup Your Dev Directories

This is already an opinionated article, so here’s one you didn’t ask for on how I think you should structure your projects on your file system.

I keep all my projects on the Linux side. I don’t put my projects in “My Documents” and then try and work with them from the WSL. My brain can’t handle that. 

I create a folder called `/dev` that I put in the root of my `/home` folder in Linux. Inside that folder, I create another one that is the same name as my Github repo: `/burkeholland`. That folder is where all of *my* projects go &mdash; even the ones that aren’t pushed to Github. 

If I clone a repo from a different Github account (e.g. “microsoft”), I’ll create a new folder in “dev” called `/microsoft`. I then clone the repo into a folder inside of that. 

Basically, I’m mimicking the same structure as source control on my local machine. I find it far easier to reason about where projects are and what repos they are attached to just by virtue of their location. It’s simple, but it is highly effective at helping me keep everything organized. And I need all the help I can get.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4cef6fa-6723-4ef2-9f37-516f9a195b96/js-dev-bash-windowsmy-folder-structure.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4cef6fa-6723-4ef2-9f37-516f9a195b96/js-dev-bash-windowsmy-folder-structure.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4cef6fa-6723-4ef2-9f37-516f9a195b96/js-dev-bash-windowsmy-folder-structure.png'>Large preview</a>)" alt="The authors opinionated folder structure listed in the terminal" >}}

## Browsing Files From Windows Explorer

There are times when you need to get at a file in Linux from the Windows side. The beautiful thing about the WSL is that you can still do that.

One way is to access the WSL just like a mapped drive. Access it with a `\\wsl$` directly from the explorer bar:

<pre><code class="language-bash">\\wsl$
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06104387-bdaa-40db-893b-5ddf52f19b7d/js-dev-bash-windowsaccess-from-windows.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06104387-bdaa-40db-893b-5ddf52f19b7d/js-dev-bash-windowsaccess-from-windows.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06104387-bdaa-40db-893b-5ddf52f19b7d/js-dev-bash-windowsaccess-from-windows.png'>Large preview</a>)" alt="The Windows Explorer the Ubuntu installation as a mounted directory" >}}

You might do this for a number of different reasons. For instance, just today I needed a Chrome extension that isn’t in the web store. So I cloned the repo in WSL, then navigated to it as an “Unpacked Extension” and loaded it into Edge.

One thing that I do with some frequency in Linux is to open the directory that contains a file directly from the terminal. You can do this in the WSL, too, by directly calling `explorer.exe`. For instance, this command opens the current directory in Windows Explorer.

<pre><code class="language-bash">$ explorer.exe .
</code></pre>

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d299ab86-9d05-4642-85a3-fd96ef69b9de/js-dev-bash-windowsexplorer-exe.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d299ab86-9d05-4642-85a3-fd96ef69b9de/js-dev-bash-windowsexplorer-exe.gif" width="800" alt="A GIF demonstrating the opening of Windows explorer on the current directory from the terminal" /></a></figure>

This command is a bit cumbersome though. On Linux, it’s just `open .`. We can make that same magic by creating an alias in the `~/.zshrc`.

<pre><code class="language-bash">alias open="explorer.exe"
</code></pre>

## Docker

When I said all tooling should be on the Linux side, I meant that. That includes Docker.

This is where the rubber really starts to meet the road. What we need here is Docker, running inside of Linux running inside of Windows. It’s a bit of a Russian Nesting Doll when you write it down in a blog post. In reality, it’s pretty straightforward.

You’ll need the correct version of Docker for Windows. As of the time of this writing, that’s the [WSL 2 Tech Preview](https://docs.docker.com/docker-for-windows/wsl-tech-preview/).

When you run the installer, it will ask you if you want to use Windows containers instead of Linux containers. You definitely do. Otherwise, you won’t get the option to run Docker in the WSL.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3a4343-2212-4335-afce-6c009664f336/js-dev-bash-windowsdocker-install.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3a4343-2212-4335-afce-6c009664f336/js-dev-bash-windowsdocker-install.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3a4343-2212-4335-afce-6c009664f336/js-dev-bash-windowsdocker-install.png'>Large preview</a>)" alt="The Docker Installation screen with “Use Windows Containers” option selected" >}}

You can now enable Docker in the WSL by clicking on the item in the system tray and selecting “WSL 2 Tech Preview”:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/626e7164-0f1a-47b3-bbc1-110ee514dfe0/js-dev-bash-windowswsl2-tech-preview-option.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/626e7164-0f1a-47b3-bbc1-110ee514dfe0/js-dev-bash-windowswsl2-tech-preview-option.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/626e7164-0f1a-47b3-bbc1-110ee514dfe0/js-dev-bash-windowswsl2-tech-preview-option.png'>Large preview</a>)" alt="The WSL2 Tech Preview Option in the Docker Daemon context menu" >}}

After you start the service, you can use Docker within the WSL just as you would expect to be able to. Running Docker in the WSL provides a pretty big performance boost, as well as a boost in cold start time on containers. 

Might I also recommend that you install the Docker extension for VS Code? It puts a visual interface on your Docker setup and generally just makes it easier to work with Docker because you don’t have to remember all those command-line flags and options.

## Get More Bash On Windows

At this point, you should get the idea about how to put Bash on Windows, and how it works once you get it there. You can customize your terminal endlessly and there are all sorts of rad programs that you can add in to do things like automatically set PATH variables, create aliases, get an ASCII cow in your terminal, and much more.

Running Bash on Windows opened up an entirely new universe for me. I’m able to combine Windows which I love for the productivity side, and Linux which I depend on as a developer. Best of all, I can build apps for both platforms now with one machine.

### Further Reading

You can read more about Bash on Windows over here:

- “[Windows Subsystem For Linux Installation Guide For Windows 10](https://docs.microsoft.com/windows/wsl/install-win10?WT.mc_id=smashingmag-article-buhollan),” Microsoft Docs
- “[How To Install And Use The Bash Shell On Windows 10](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/),” Chris Hoffman, How-To Geek
- “[Sharing SSH With WSL](https://geedew.com/Sharing-SSH-With-WSL/),” Drew Wilson
- “[Getting Crazy With The Window Subsystem For Linux](https://www.brianketelsen.com/getting-crazy-with-windows-subsystem-for-linux/),” Brian Ketelsen
- “[Everything You Can Do With Windows 10’s New Bash Shell](https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/),” Chris Hoffman, How-To Geek

*Special thanks to Brian Ketelsen, Matt Hernandez, Rich Turner, and Craig Loewen for their patience, help, and guidance with this article.* 

{{< signature "rb, dm, il" >}}
