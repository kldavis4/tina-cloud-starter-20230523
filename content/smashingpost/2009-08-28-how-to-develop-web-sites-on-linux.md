---
title: How To Develop Websites On Linux
slug: how-to-develop-web-sites-on-linux
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7227de00-b2c0-4774-9f1c-d204221f00b0/linux.png
date: 2009-08-28T13:58:01.000Z
author: ricardo-cappellano
description: >-
  In this article we will look at tools that can help those of you who want to
  **develop websites on a Linux platform**, from powerful text editors to
  desktop and system features. How do you edit files remotely without FTP
  plug-ins? What are package managers, and why they are cool? In which Web
  browsers can you test your applications?
categories:
  - Coding
  - Linux
---
In this article we will look at tools that can help those of you who want to <strong>develop websites on a Linux platform</strong>, from powerful text editors to desktop and system features. How do you edit files remotely without FTP plug-ins? What are package managers, and why they are cool? In which Web browsers can you test your applications?

I wish I could cover many more topics: using the command line, basics of Vim, Nautilus features in detail, Nautilus scripting, neat command line tools, basic server configuration and many others. But if I addressed all of the issues that arise from time to time on the Internet, this article would turn into a small book. This isn't an article on "How to do X or Y on Linux" or "How to use [insert app name here]." And we cannot cover more comprehensive IDEs such as Eclipse and NetBeans, each of which requires separate articles.

Be sure to check out our previous articles:

*   [Introduction To Linux Commands](https://www.smashingmagazine.com/2012/01/introduction-to-linux-commands/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [VI Editor / Linux Terminal Cheat Sheet](https://www.smashingmagazine.com/2010/05/vi-editor-linux-terminal-cheat-sheet-pdf/)

You probably already have some idea of how to find and install applications for your favorite distros. However, we will point you to the right place anyway to download, for example, scripts and plug-ins.

{{% feature-panel %}}

So, let's begin!

## 1\. Our Tools

Below, for your quick reference, is a list of tools that we will mention or explain in this article.

<strong>Text Editors:</strong>

*   Gedit
*   Geany

<strong>Browsers:</strong>

*   Opera
*   Mozilla Firefox
*   Epiphany (with the WebKit engine)
*   Chromium (for some other WebKit examples)

<strong>General and command line tools:</strong>

*   FUSE
*   SSHFS
*   Vim
*   Parcellite

## 2\. Gedit

Gedit is the default and simplest text editor for the GNOME environment. The default installation already comes with some good resources, although not all of them are activated by default. It is bundled with some plug-ins; however, you can add many more plug-ins to make it a nice simple IDE. If you go to <em>Edit &gt; Preferences &gt; Plugins</em>, you'll see which plug-ins are installed by default. There, you can configure and activate them. On the same screen, you can configure other elements of the text editor, such as indentation, line numbering and current line highlighting.

<img title="Gedit Preferences" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1a0eb5-7d9b-49c4-914e-2fa7f4715266/001.jpg" alt="Gedit Preferences" width="390" height="414" />

Your default installation probably won’t have many plug-ins by default other than those. Check if your distro has a package to automatically install a set of plug-ins. The package would be named gedit-plugins. I recommend installing it because it adds at least five helpful plug-ins: bracket completion, color picker (quite helpful with your CSS), session saver, smart spaces and terminal. These are all of the plug-ins installed with the package:

*   Bracket completion
*   Charmap select
*   Code comment
*   Color picker
*   Join and split lines
*   Session saver
*   Smart spaces
*   Show tabbar
*   Terminal

See the plug-ins section for a fuller overview of them.

Let's look at the most useful of these basic plug-ins for developers and see how we can configure them, in needed.</p>

### Snippets

Snippets inserts frequently used pieces of text quickly. To configure it, check it on the plug-in tab and hit "Configure Plugin." You can edit existing snippets, add new ones, import and export snippets and create global snippets. It is also possible to add tab triggers, shortcuts and drop targets. To activate a snippet, you must be editing a file with a corresponding snippet (e.g. if it is a Python snippet, you should be editing a Python file). If it is a blank pure-text file, just change its syntax on <em>View &gt; Highlight Mode</em>. <strong>Many good snippets are on the Internet</strong>; some that I use are Django and RoR snippets.

<img title="Snippets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/909ab06a-191f-444c-8b2a-54d46d8ad628/002.jpg" alt="Snippets" width="522" height="431" />

### External Tools

External tools executes external commands and shell scripts. As with snippets, you can configure those that ship with the plug-in or create your own. For more complex tasks, <strong>you will need some knowledge of shell-scripting</strong> and how to use some of the shell tools. We won't go into how to master Gedit and its amazing plug-ins (we recommend reading Gedit manuals for that), but we will give you links to some scripts that you can play with.</p>

### Modelines

If you use Vim or Emacs in your daily work, you may know what modelines are. If you wish you could import them to other text editors, modelines lets you do exactly that.

For those who aren’t familiar with them, modelines are "definitions" of tabbing, spacing, line ending, tabbing level and so on.

The basic and gedit-plugins packages are the ones I use most often. Some other functionality can be added only through third-party plug-ins, which you can find all over the Web; GNOME Live's Gedit section is a good start. Have a look at AutoComplete, Better Python Console (the Python Console that ships with Gedit is only useful for developing gedit plug-ins), ClassBrowserPlugin and Autosave editing sessions.

Finally, you can customize the look of Gedit with color themes. Gedit comes with a few, but you can find many more.

<img title="Gedit Themed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88affbc0-6e56-42f9-a1f6-2a174d9e7843/003.jpg" alt="Gedit Themed" width="500" height="343" />

### Further Reading

*   Modelines: Modelines page at GNOME library website.
*   [Gedit Plug-ins](https://www.makeuseof.com/tag/top-plugins-to-extend-and-make-gedit-a-more-useful-text-editor-linux/) Gedit plug-ins repository at GNOME Live
*   External Tools Plug-in External Tools plug-in page at Live GNOME.
*   [Text-mate like Gedit in a few steps](https://grigio.org/pimp_my_gedit_was_textmate_linux)A guide with resources for making Gedit look more like Text-mate.
*   [Using Gedit with Django:](https://code.djangoproject.com/wiki/gedit) A guide to using Gedit for Django programming
*   Django Snippets: Snippets for Django.
*   [RoR Development with Gedit](https://ca.rroll.net/2008/02/05/ruby-on-rails-development-with-gedit/) A guide to using Gedit for Ruby On Rails programming.
*   RoR Snippets Snippets for Ruby On Rails. There are also more snippets here.
*   RHTML integration: A guide to integrating RHTML in Gedit.</p>

## 3\. Geany

Unlike Gedit, Geany is more of a general purpose "minimalist" IDE than text editor. It already comes with such resources as an embed terminal, compiler tab, messages tab and note-taking tab (Scribble). You also have a side-pane listing of file symbols (i.e. classes and methods in Java files, sections and sub-sections in LaTeX files) and documents that can be extended to include a tab with file browsing. In addition, Geany comes with a simple completion tool, color picker, finder, simple project builder and tools for some languages. Its search tool is capable of searching the whole session or only the current file, with or without regex, and a "Find in files" option if the browser files plug-in is on.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d65991c-ecb3-4f9b-a8ef-a5badda06231/004.jpg" alt="Geany Main Screen" width="500" height="489" />

Yet one of the nicest features of Geany is its <strong>Compile and Execute buttons</strong>. Based on the file you are editing, Geany tries to find the corresponding compiler/interpreter. So, if you are editing a Java file, you can compile it with javac and run it right after the compilation ends. At the same time, you can compile a LaTeX file and preview it in a really simple DVI viewer without having to change any configuration parameters. For interpreted languages, you don’t even have to run the compiler: just hit "Execute." Of course, if your executable has a different name (let’s say, <em>ruby1.8</em> instead of <em>ruby</em>), it will fail and report that it couldn’t find <em>ruby</em>. But you simply need to configure that to make things work wonderfully again.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3e2762-b48f-436d-bf1c-8d4469de885b/005.jpg" alt="Geany Compiler output" width="500" height="189" />

Another interesting aspect of Geany is its built-in tags information. You can create <em>*.tags</em> files for a language or framework that Geany does not support by default, as well as add support for auto-completion and call tips. Consult Geany’s documentation for more details

Finally, you can extend Geany with plug-ins (find the plug-ins manager in the Tools menu) and themes. Or simply configure everything the way you want: just go to "Preferences" and adjust things to your taste, from the browser to your shortcuts.</p>

### Further Reading

*   [Geany snippets](https://geany.org/manual/#user-definable-snippets) A collection of snippets to use with Geany.
*   Integrating with SVN/Git: How to use Geany with SVN or Git version control systems.
*   [Geany extras](https://www.geany.org/Download/Extras) Extra goodies to extend Geany.</p>

## 4\. What About Remote File Editing?

Nowadays, things are pretty easy, and you almost don’t need to install plug-ins to access FTP and SSH accounts or to edit files, because most modern distros comes with FUSE. And if you have GVFS installed, <strong>GNOME integrates it</strong> so that you can use it on Nautilus.

"But what is it?” you may be asking. In short, it allows you to mount a virtual file system on your system and work there just as you would in common directories.

You would just click on a file and start editing it. When you're finished, just save and everything is done. A big advantage of this method over the FTP plug-in method is that you make things available to more than one application.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01c57ed4-7c54-4898-ab64-b3ad79785039/006.jpg" alt="FUSE on action" width="500" height="358" />

Note: since my server has only SFTP access, I'm not sure how stable this is with simple FTP, but it works flawlessly with SFTP. Nevertheless, when I need to edit a remote file, I prefer to connect via SSH using a terminal and use Vim to edit the file, only because the method reminds me that I'm not working locally and to be careful.</p>

### Further Reading

*   [Mounting FUSE file system](https://www.debuntu.org/2006/04/27/39-mounting-a-fuse-filesystem-form-etcfstab) A quick guide to mounting a FUSE system and adding it to fstab.
*   [Creating file systems with Ruby and FUSE](https://www.debian-administration.org/article/Creating_Filesystems_with_Ruby__and_FUSE) Using FUSE with Ruby

## 5\. File Browsing FTP and SSH, Natively

In more recent versions of Nautilus, the GNOME file browser, you have native access to network protocols, such as WebDAV, FTP, SSH and Windows shares. You can add other protocols, like SVN, or extend it through its plug-ins and scripts. (Unfortunately, I cannot cover this topic here but only point you to an extensions and scripts website.)

You can browser different servers at the same time on different windows, which can be really helpful for transferring files from one server to another.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf45105f-1064-464c-aaeb-584d9126c237/007.jpg" alt="Nautilus SSH" width="500" height="291" />

Of course, you don’t need to be stuck in the graphical portion of Linux. You can use the command line to perform most of these tasks.</p>

### Further Reading

*   [SVN on Nautilus:](https://code.google.com/p/nautilussvn/) Nautilus SVN integration project page.
*   [Nautilus subversion integration tool. Execute SVN commands with Gnome scripts](https://www.harecoded.com/nautilus-subversion-integration-tool-execute-svn-commands-with-gnome-scripts-96355) A tutorial on how to integrate and use SVN on Nautilus.
*   [Nautilus File Manager Scripts](https://g-scripts.sourceforge.net/) A page with a good collection of Nautilus scripts.
*   Nautilus on GNOME Live Nautilus page on GNOME Live.
*   Extending Nautilus A guide on how to write scripts and extensions for the Nautilus File Browser.</p>

## Web Browsers

Linux has a lot of Web browsers to play with, from Mozilla’s family to console-based browsers. All of them have their pros and cons. But most of the time, we need only a few for testing, probably Firefox, Opera and one with the WebKit/KHTML engine.

Because I’m covering the GNOME environment, I chose Epiphany, with the WebKit engine (Epiphany's project developers switched from Gecko to WebKit in the latest versions). Epiphany with WebKit is named epiphany-webkit on Debian and probably on some other distros

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33f8514b-f743-4584-b7c7-93df86171cb3/009.jpg" alt="Epiphany WebKit" width="500" height="481" />

If you are on KDE, though, Chromium would probably suit you better because it does not depend on GNOME libraries or even use Konqueror (KHTML).

Note: I’m no specialist on rendering engines, so I can’t say for sure whether testing on more recent versions of Konqueror (which uses KHTML) would be sufficient for WebKit tests. I do all my testing on Epiphany.

If you really need to test your website in Internet Explorer, you can use the Wine library with Wine Tricks. Or use VirtualBox images, which is provided by Microsoft itself. For now, IE8 on Wine is still too buggy. But IE7 can run on Wine: check the "Further Reading" section below for more information. Running them on VirtualBox should work flawlessly.</p>

### Further Reading

*   [Chromium](https://code.google.com/chromium/) Chromium project page.
*   Epiphany WebKit Epiphany WebKit page at GNOME Live.
*   IE 7 on Wine How to run IE7 on Wine.
*   [HOWTO: run IE6, IE7, IE8 on Linux in VirtualBox](https://ubuntuforums.org/showthread.php?t=1097080) How to use VirtualBox to run Microsoft browsers. Another guide is here.
*   [Wine Tricks](https://wiki.winehq.org/winetricks) Wine tricks page at Wine HQ wiki.</p>

## Package Manager: Your Best Friend

If there is one thing I really love on every Linux distro I have used, it is the package management. Okay, some are better than others, but generally speaking you need only the command line to take control of your system applications. Package managers help you find, install and keep track of security updates and new versions of your applications. And you can install more than one application at a time, even if they are not related.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33f8514b-f743-4584-b7c7-93df86171cb3/009.jpg" alt="apt-get on action" width="500" height="165" />

Depending on the package manager, when you search for and install new applications, others that might work well with the ones you have found are suggested to you, such as GUIs for configuring and managing an FTP server.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4808fb6-d0fa-4490-9465-3463d468e5f6/010.jpg" alt="apt-get suggestions" width="500" height="162" />

Some bundles for installing AMP include too many applications (even on Linux) or are strict in what they have packed. But when using a package manager on Linux, installing a server environment can be easier and flexible: you can tailor your installation more efficiently, choosing only what you need. Why would you install PHP if you are not a PHP developer? Why install MySQL if SQLite serves your needs? You probably don’t need an FTP server or an email service either. Nevertheless, you can install any of them easily if you need to in future. Also, you needn’t be restricted to Apache if you plan to use, say, lighttpd.

Open-source version control systems are available for Linux and, even better, in distro repositories. For Debian, you have Git (as git-core), Mercurial, CVS, Subversion and Bazaar all in the official repository (though Bazaar is over the backports and unstable). No need to go to a bunch of different websites.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1257f7f0-e24f-4465-bc21-ba16997ebeca/011.jpg" alt="apt-get suggetions" width="500" height="250" />

### Further Reading

*   [The Perfect Server: Debian Lenny](https://www.howtoforge.com/perfect-server-debian-lenny-ispconfig3) Tips and instructions on how to set up a complete server on Debian
*   [Debian lighttpd](https://www.debianhelp.co.uk/lighttpd.htm) How to configure a lighttpd server on Debian
*   Gentoo Tutorials A collection of tutorials at Getoo Wiki. Could be useful for others distro, too.
*   CrossFTP Server An FTP server with an LDAP/database back end and GUI configuration/monitoring.
*   GAdmin ProFTPD GAdmin module for administrating ProFTPD servers using a GUI.
*   PureAdmin PureAdmin is a user and server administration for the pure-ftpd.</p>

## Native Multi-Paste And Multiple Desktops

I started using Linux seriously at the end of 2003, when I got sick of Windows 98 SE freezing after 20 minutes of use and having to be reinstalled after 2 weeks.

After installing Debian and exploring KDE features, I discovered how cool and useful the virtual multi-desktop concept was. Now when I use other operating systems, this is what I miss most. But really understanding how it can help you organize your windows and work takes some time.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5a458bc-f752-4970-ba05-35c799387d9e/012.jpg" alt="Multiple desktops" width="291" height="31" />

Another thing I find really helpful and miss in every other system I use is being able to buffer two things on the clipboard with any external tools. (Okay, I know when using Vim you have as many buffers as keys, but I’d need a whole book to talk about Vim!) All I need to do is highlight a piece of text and press the middle button to paste it. And if I have something in the buffer (loaded previously with Control + C), I won’t lose it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c18ca62-8fcd-4d20-ad04-73aa26252dbc/013.jpg" alt="Multiple clipboard" width="355" height="292" />

You have plenty of options for controlling multiple buffers in the clipboard. KDE already comes with Klipper, which is great. GNOME comes with no such tool, but you do have some good options (I use Parcellite).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b6a7ae7-3b85-4784-bf7a-42b34e2e3b30/014.jpg" alt="Parcelite" width="279" height="255" />

One little thing I miss is a native way to call programs without having to click on their icons or menu entries or call them through the terminal. GNOME and KDE both have a <strong>native application runner</strong> that you can call by pressing Alt + F2. Then, just start typing and it shows your options. Even though QuickSilver, and programs like it, does something similar and even better, you have to install it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/369bea1f-b131-4930-9416-44562c9b06e0/015.jpg" alt="Application runner" width="440" height="327" />

### Further Reading

*   [X Window System Multiple Desktops](https://en.wikipedia.org/wiki/Virtual_desktop#X_Window_System_and_Unix) Wikipedia entry about multiple desktops on X Window System
*   Glipper A GTK clipboard manager.
*   Parcellite Another GTK clipboard manager.
*   GNOME Launch Box A QuickSilver-like tool for the GNOME environment.
*   GNOME Do Another tool inspired by QuickSilver.
*   Katapult KDE's tool inspired by QuickSilver.
*   [GNOME Deskbar](https://projects.gnome.org/deskbar-applet/) Deskbar is an applet the comes bundled with GNOME with the goal of providing a common search interface.</p>

## A Note About KDE

Linux is a rich world and has many variables to experiment with. I have never used any of KDE's specific tools. For programming, I use NetBeans. I have used KWriter for simple edits but never for programming (nor Kate). Though I haven't used KDE4, I can say by experience that, for file browsing, Konqueror is a killer app: integrated preview for many file types, native access to SSH, (S)FTP and other network protocols, extensible, tabbed file browsing and many other great features.</p>

## Conclusion

We have seen a lot of simple tools to play with, a rich environment for building testing and development servers and a good range of tools to improve your workflow. Although Linux isn't the most popular OS for desktops, it is not necessarily ill-suited to most kinds of development work — and it may even be better than more popular OS's. It is up to you now to try it if you are not satisfied with your current environment.</p>

### Further Reading

*   [Vim](https://www.vim.org) Vim official page
*   [Vim doc](https://vimdoc.sourceforge.net/) A Vim documentation project, with references, tips, FAQs and tutorials. A good resource for any Vim user.
*   [Shlomi Fish's Vim for begginers](https://www.shlomifish.org/lecture/Vim/beginners/) A good place to start if you want to learn Vim.
*   [VIM for Django](https://code.djangoproject.com/wiki/UsingVimWithDjango) Tips, plug-ins and scripts to make Vim more suitable for Django.
*   [Vim for Rails](https://www.vim.org/scripts/script.php?script_id=1567) A plug-in to enhance Vim for Ruby On Rails.</p>

## Related posts

You may be interested in the following related posts:

*   [CSS Editors Reviewed](https://www.smashingmagazine.com/2008/06/19/css-editors-reviewed/) This review includes JustStyle CSS Editor, CSSED and other CSS editors for Linux.
*   [35 Useful Source Code Editors Reviewed](https://www.smashingmagazine.com/2008/05/07/35-useful-source-code-editors-reviewed/) This review includes Komodo Edit, Aptana Studio, Screem, Quanta Plus, Emacs and other editors for Linux.

{{< signature "al" >}}

