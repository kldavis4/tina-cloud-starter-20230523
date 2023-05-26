---
title: 'How To Build Your Own Mouseless Development Environment'
slug: mouseless-development-environment
author: matthieu-cneude
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c58e67b-deff-4745-b162-f60f468469ac/mouseless-development-environment.jpg
date: 2021-09-21T11:30:00.000Z
summary: >-
  Building a development environment with the shell as a keystone offers multiple benefits. You can use tools that fit nicely with each other, you can customize everything depending on your own needs, and the biggest of all, you can control your entire development environment with your keyboard. This can save a lot of cognitive energy as well as deliver a pleasant user experience.
description: >-
  Building a development environment with the shell as a keystone offers multiple benefits. You can customize everything depending on your own needs, and the biggest of all, you can control your entire development environment with your keyboard.
categories:
  - Tools
  - Workflow
---

Once upon a time, in the magical land of Software development, there was a young developer, your humble servant, discovering Linux for the first time. Suddenly, I had access to the Linux shell, a tool offering many ways to automate everything I didn’t want to do again and again.

But Ubuntu wasn’t without drawbacks. I was often the victim of display bugs and crashes, and it was getting slower and slower as time passed.

One day, something terrible happened: I had to update Ubuntu to its next major version. **Everything crashed.** I couldn’t start my system anymore. I had no idea how I could solve the problems I was facing because I had no idea how Linux was working under the hood. Ubuntu was *abstracting* all the nitty-gritty for me not to care about it.

I had to reinstall everything manually &mdash; Ubuntu and all my tools. The worst part was reconfiguring everything. All and all, it took me days to get back to the system I had before the crash. But I didn’t know any other alternative, so I kept using Ubuntu for years. During this time, I’ve never managed to update it to its next major version without the need to reinstall everything manually, again and again.

My life as a developer changed again when my company hired two great developers. They knew a lot about Linux and the different distributions I could use. They guided me, showed me the tools which solved all the problems I had with Ubuntu. These tools **improved my workflow drastically**; they showed me how practical it was for a developer to keep the hands on the keyboard as much as possible.

This happened six years ago. I still use the same development environment today. **I use the keyboard 92.8% of the time** to manage all my tools, using keystrokes that make sense and which are easy to remember. I can reinstall my whole system with a bunch of scripts I’ve written, including all the tools I use and their configurations.

Today, I’d like to share with you these tools so that you too can increase your efficiency and your comfort in your daily job. They work well together &mdash; shaping what I call my *Mouseless Development Environment*. More precisely, we’ll discuss:

- Why using the Linux shell can be very powerful when working with plain text (including code);
- Why using the dreaded Arch Linux;
- The advantage of a tiling window manager;
- How to have a great terminal experience with URxvt, tmux, and tmuxp;
- Why Vim can become your best friend.

**Note**: *The tools I advocate in this article work on Linux-based systems. You can also use them with macOS except for i3. For Windows, the easiest way is to use the Windows Linux Subsystem (WSL) to install and use them.*

I would have never discovered this new way of working without trying these tools. That’s why I encourage you to install them, experiment with them, and see by yourself if you fall in love as I did.

## Mouseless With The Shell

As a developer, it’s almost impossible to avoid using a shell. This is a powerful tool that can simplify your workflow by automating away all the boring tasks.

### The Benefits Of The Shell

Before speaking about the benefits of using the shell and the terminal, let’s explain briefly what’s the difference between these two ideas. 

The terminal is a graphical interface that allows you to interact with the shell. On Linux, this shell is often Bash, but it can be another one too, e.h. Zsh. The shell is an interpreter. You can **feed it with commands** and it will execute them to perform some actions. It will also, sometimes, give you an output back. The terms “command-line” and “shell” are synonyms.

If we would compare the Mouseless Development Environment to the solar system, the shell would be the sun and everything else would turn around it. It’s because the shell is really powerful: it allows you to run many small programs which work very well together. They’re called CLIs (Command-Line Interfaces).

The big advantage of these tools: they are very simple and limited in isolation, but you can **chain them for powerful results**. For example, you can use altogether the CLIs “history”, “sort”, “uniq” and “head” to display the CLIs you use the most and the frequency of their use.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3915c43b-7bc5-4d9c-a57e-0934edce548e/01-linux-shell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3915c43b-7bc5-4d9c-a57e-0934edce548e/01-linux-shell.png" width="800" height="489" sizes="100vw" caption="The Linux Shell. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3915c43b-7bc5-4d9c-a57e-0934edce548e/01-linux-shell.png'>Large preview</a>)" alt="The Linux Shell" >}}

There are many CLIs available out there. First, because the Linux shell is around for a long time; developers had time to develop many tools and make them reliable. Second, because **it’s easier to develop CLIs than GUIs** (Graphical User Interfaces). Designing and implementing these graphical interfaces takes a lot more work. CLIs have only *textual interfaces*, which are easier to develop, to change, and to maintain.

It’s also why CLIs are fast: no need to mess up with the display and other graphical elements. It was one of my main problems with Ubuntu: its desktop environment, Unity, was quite heavy, slow, and buggy. At least in my experience. Using more GUIs on top made things worse.

Another big **advantage of the command-line**: you can write shell scripts to automate all the boring tasks you repeat day after day. For example, if you need to resize images to the same size very often, you can write a script for that. If you often search in some specific type of files, you can automate that too. The sky’s the limit.

{{% feature-panel %}}

CLIs have drawbacks, too. It’s a bit more daunting to use for beginners, but there are ways to get quickly what you need even if you don’t know how to use a specific CLI.

Finally, if you have some tasks to do on remote servers, you’ll often end up using the shell. They don’t have any graphical interface most of the time, so you won’t have any choice. In these cases, it’s necessary to know your way around the command-line.

### A Mouseless Approach

Because the shell has a textual interface, your hands stay on your keyboard when you use it. This is something I never really considered during my first years as a developer, but it’s a big advantage. 

In my experience, avoiding the hundreds of **hand movements between the keyboard and the mouse** saves a lot of cognitive energy. I was shocked to discover how comfortable it was when I really tried to stick to my keyboard. As a bonus, I feel like a hacker using solely my keyboard with my shell, even if I only write my shopping list! How great is that?

I have to admit, I was very skeptical about this “mouseless” idea before trying it. With the tools I describe below, I didn’t have to change all my habits from one day to another: you can use the mouse with them, too. But they really shine when they’re managed with the keyboard.

Even if it was never really proved, I also believe that **staying on the keyboard makes us more efficient**. As the book *The Pragmatic Programmer* pointed out:

<blockquote>“Using only keystrokes for common editing operations is more efficient than mouse or menu-driven commands because your hands never leave the keyboard.”</blockquote>

That being said, efficiency is not the main goal here. I love staying on my keyboard and using all these tools because I can entirely focus on the tasks at hand. It motivates me to start working and get my tasks done.

## The Bedrock: Arch Linux

At the beginning of my mouseless journey, one of my new friends advised me to use [Arch Linux](https://archlinux.org/) instead of Ubuntu. Again, skepticism was creeping, doubts were invading my poor brain. Arch Linux? This horrible Linux distribution you need to install and configure entirely manually? This unstable system became a joke for many?

Sometimes, stereotypes have nothing to do with reality, and Arch Linux is the perfect example for this idea. I’ve used Windows (from 98 to 7), macOS, and I tried other Linux distributions too. My conclusion, without doubt: Arch Linux is the most stable of all.

That being said, Arch Linux it’s not a requirement for a Mouseless Development Environment. You can use all the other tools described in this article with other Linux distributions, too. You can also use them with macOS (except i3), or Windows if you have the Windows Subsystem for Linux (WSL). But, before you do so, let me tell you **why you should seriously consider Arch Linux**.

### A Rolling Release System

Arch Linux has a *rolling release system*. It means that you need to update your whole system often, weekly or bi-weekly. To come back to Ubuntu, it has a *long-term support system*: you only need to update it a couple of times a year, or even less if you want to.

Many developers think that a rolling release system makes your development environment unstable, which explain partly the reputation of Arch Linux. But I never had a problem in six years of daily use, and my friends using it either. On another side, **the advantages of a rolling system** are great:

- All the applications I use are constantly up-to-date. No need to compile them manually to have the most recent version when needed.
- Updating your system often means that less changes will be introduced at once. As a result, there are less chances for crashes, too.

I told you my experience with Ubuntu and the crashes I had when updating it. I never had any problem with Arch Linux.

### Everything You Need

Additionally, the repositories of Arch Linux are huge. It’s very likely that you’ll find every tool you need in there. If you don’t, you can look at the AUR (Arch User Repositories), where there is everything else. The AUR is not an official repository, so there could be some security problems with the applications found there. Again, I never had any problem with them, but it’s possible. As long as you stick to the official repositories and you don’t install everything and anything from the AUR, you won’t have any problem.

### A Learning Opportunity

Let’s also mention that Arch Linux is a very minimal distribution. It doesn’t impose many useless applications when you install it. Speaking of which, you need to install the whole distribution manually using the shell. The task can feel daunting but, on the other side, you’ll learn a lot from the experience.

As I mentioned at the beginning of this article, **knowing a minimum of how Linux-based systems work under the hood** can help you when your system is behaving weirdly, or when it crashes. It’s not as complex as it might seem and, if you’re a developer, I would argue that it’s mandatory. The Web, your phone, or your Raspberry Pie run on Linux nowadays.

Last but not least, the [Arch Wiki](https://wiki.archlinux.org/) is the best place you can find for anything Linux-related. It helped me a lot over the years, even when I was using Ubuntu. It’s a great place for **troubleshooting your system** and finding new tools.



<h3 id="marker" style="text-transform: none;">Managing Your Windows With i3</h3> 

Now that we reviewed why Arch Linux can be a solid bedrock for your Mouseless Development Environment, let’s see what we can add on top. 

But first, a bit of theory. Operating systems have often three layers, more or less coupled with each other:

1. The **kernel**, which directly dabbles with the hardware of your computer;
2. The **shell**, an interface for you, or some applications, to interact with the kernel;
3. A **display layer** on top, like a desktop manager or a tiling windows manager.

Gnome or Unity are both desktop managers for Linux-based systems. They manage your windows and many other things, like your status bar or your application launcher. Tiling windows managers are an alternative to desktop managers, and they’re often smaller and more focused on manipulating windows.

The [tiling window manager i3](https://i3wm.org/) is indeed very light: I’m using it right now on a ten-year-old computer (Lenovo x220) and it doesn’t slow down. It’s also simple to use, the documentation is great, and most importantly, you can manage your windows with your keyboard only (if you want to).

The basics of i3 are simple: you can open windows in **different workspaces representing an entire screen**. It’s very similar to the virtual desktops many Linux desktop managers have. Then, when you open your favorite applications, the screen will be automatically shared depending on the number of windows on the screen.

For example, if you open Firefox, its window will take 100% of the screen. If you open three instances of Firefox, each of them will take 33% of the screen.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0672e51-26ff-428b-a18d-793b5bad11ee/03-three-firefox.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0672e51-26ff-428b-a18d-793b5bad11ee/03-three-firefox.png" width="800" height="497" sizes="100vw" caption="i3 with firefox window. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0672e51-26ff-428b-a18d-793b5bad11ee/03-three-firefox.png'>Large preview</a>)" alt="i3 with firefox window" >}}

You can also change the layout of the windows. Instead of having all the window visible on the screen, you can stack them on each other and go through them with a simple keystroke. If you need some “normal” floating windows, you can configure them too.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/501d6fdc-6bf4-44a1-a49f-1fe89ce89faa/04-three-firefox-stacked.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/501d6fdc-6bf4-44a1-a49f-1fe89ce89faa/04-three-firefox-stacked.png" width="800" height="498" sizes="100vw" caption="i3 with firefox windows stacked. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/501d6fdc-6bf4-44a1-a49f-1fe89ce89faa/04-three-firefox-stacked.png'>Large preview</a>)" alt="i3 with firefox windows stacked" >}}

The goal of i3 is to simplify the management of all your windows. Instead of using your mouse to move them and resize them each time you open new ones, you can use keystrokes to do the same operation *only when you need to*.

Does it look too complicated? I was efficient with i3 two days after trying it. I’m no genius; if I could do it, you can do it, too.

The cherry on the cake: like every tool described in this article, **you can customize i3 and its keystrokes** as your heart’s content.

The only drawback of i3: it’s not available for macOS. But there are great **alternatives**, like the tiling windows manager [Amethyst](https://forum.zettelkasten.de/discussion/1518/tiling-window-managers-on-macos) or [Divvy](https://mizage.com/divvy/).

{{% ad-panel-leaderboard %}}

## Level Up Your Terminal With URxvt, tmux, And tmuxp

The terminal is the interface giving you access to the shell. Even if the shell is the real deal, we can make it easier to use with a couple of tools.

### The Path of Simplicity With URxvt

I like simplicity, and that’s partly why I love the development environment I describe in this article. Speaking of which, [URxvt](https://wiki.archlinux.org/title/Rxvt-unicode) is one of the simplest terminals you can find. It’s also fast and reliable. In six years, I never saw it crashing or even slowing down. It does what it’s supposed to do: allowing you to use the shell. No more, no less.

### The Terminal Multiplexer With tmux

Even if I like the simplicity of URxvt, I also like having a good terminal multiplexer I can rely upon, like [tmux](https://github.com/tmux/tmux/wiki).

What’s a terminal multiplexer? It **lets you open sessions containing multiple shells**. These sessions are persisted in the background: even if your terminal crashes or if you close it by accident, your shells won’t disappear. You can recover them in another terminal whenever you want (as if nothing happened).

This is useful on your local computer, but it’s even better on a remote server. You can, for example, connect to a server via SSH, run a script, close your SSH connection and your terminal on your local machine, and go home. Because your shell is still running on your server thanks to tmux, your script will still run, too.

That’s not all: tmux is a bit of a jack-of-all-trades, in a good sense. You can **use it to open multiple windows containing multiple panes** in one terminal. You can think of a window as the entire terminal, and a pane as a shell taking a percentage of the window.

Does it remind you of i3? It follows the same principles, but it can only create new shells. That’s why many users who are happy with i3 don’t see any point in using tmux. Personally, I like to use both.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e9cca52-6e0c-499b-8196-c643bec0d7c8/05-tmux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e9cca52-6e0c-499b-8196-c643bec0d7c8/05-tmux.png" width="800" height="497" sizes="100vw" caption="Tmux with 4 windows and 4 panes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e9cca52-6e0c-499b-8196-c643bec0d7c8/05-tmux.png'>Large preview</a>)" alt="Tmux with 4 windows and 4 panes" >}}

As always, you can manipulate tmux’s windows and panes with your keyboard, and you can configure tmux itself following your craziest wishes.

### tmuxp

Let’s imagine that you want to use tmux for the disrupting application you’re developing right now. You need first to open a terminal. Then, you need to create as many tmux’s windows as you need and divide these windows with the panes you want. 

**Remember**: *A pane represents a shell. In each of these shells, you can then run all the CLIs you need for a specific project: for example, running a docker container, or displaying some logs.*

But you can also automate all of that, and it’s where **the real power of tmux** &mdash; in the context of a development environment &mdash; really shines. Using another CLI called [tmuxp](https://tmuxp.git-pull.com/quickstart.html), you can write down in a YAML configuration file what windows, panes, and whatever command you want. Then, you can load this configuration and create automatically your customized tmux session.

I have one of these configuration files for each of my projects. It saves me a lot of time and energy. As I was saying above, this is one of the major benefits of using the shell.

{{% ad-panel-leaderboard %}}

## Editor Plus Shell Equals IDE

Since the shell is so powerful, why not have an editor directly running in it? Why not use [Vim](https://www.vim.org/)?

Like Arch Linux, Vim has the reputation to be hard to learn. It’s more subtle: it’s pretty easy to be productive with it, but it takes a long time to master. If you run Linux and you have Vim installed, you can **learn the basics in 20 minutes** by running `vimtutor` in your shell.

Vim offers many functionalities which can be extended further with countless plugins. Additionally, you can directly interact with your shell using Vim, using whatever CLI you want directly in your editor. It will transform Vim into a full-blown IDE.

Vim has another big advantage: you can use it to develop in many programming languages. I don’t like to switch between different IDEs each time I need to program in PHP, Golang, or Clojure. The interface is different, I need to configure each of these editors separately, and I can’t really save the configurations somewhere to use it again when I reinstall these tools. 

With Vim, I can code in any language I want while **staying in the same editor**. Like VS Code, you can use LSPs (Language Server Providers) to enable auto-completion, linting, and automatic refactoring for the most common programming languages (and even more esoteric ones).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab59a287-fe7c-48c5-afcd-ec9f62880901/06-vim.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab59a287-fe7c-48c5-afcd-ec9f62880901/06-vim.png" width="800" height="542" sizes="100vw" caption="Vim in action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab59a287-fe7c-48c5-afcd-ec9f62880901/06-vim.png'>Large preview</a>)" alt="Vim in action" >}}

Vim is also fast. It doesn’t require many resources to run. I often have 6 or 7 instances of the editor open at all times on my old computer &mdash; without any problems. In comparison, I used IntelliJ IDEs for years and, when I was opening two of them, my whole system was beginning to slow down. It’s really practical when I work on different projects at the same time, like a bunch of microservices, for example.

Should I add that **Vim is highly configurable**? Instead of having many functionalities directly in your IDE (including some you’ll never use), you can choose what you exactly need and discard what you don’t.

## A Set Of Coherent Keystrokes

If Arch Linux is the bedrock of my Mouseless Development Environment, then i3, Zsh, tmux, and Vim are the workbenches for my creative needs. It gives me a level of comfort I’ve never experienced with any other tools.

But you might wonder why you should use all these new tools and their keystrokes when you can already use the shortcuts for the tools you already know?

Well, **the shortcuts of most applications out there are often meaningless**. It’s a soup of keys that have no relations with each other. As a result, they are hard to remember, and they can be quite different from one tool to another.

The tools I describe in this article are meant to fit nicely with each other. You can almost use the same keystroke for each of them. Only one key will differ, for the system to know what tool you want to act on. It makes the different keystrokes way easier to remember.

Additionally, Vim was designed to have keystrokes that make sense by creating a simple language that you can rely upon. For example, in order to delete a word, you can hit `daw`. To delete a paragraph, it’s `dap`. Since many CLIs are based on Vim’s keystrokes, **learning Vim will open the door to many other CLIs**.

## Installing Automatically Your Mouseless Development Environment

Installing Arch Linux manually is good to learn a lot about Linux-based systems, but it gets old when you need to do it each time you want to install your system on a new computer. That’s why [I’ve created my own scripts to install my whole Mouseless Development Environment](https://github.com/Phantas0s/ArchInstall). They install Arch Linux as well as all of the [tools I use with their configurations](https://github.com/Phantas0s/.dotfiles). When I need to use a new computer, I can simply run these scripts, and voila!

## Are You Ready To Be A Mouseless Developer?

Because of the flexibility, I have with my development environment, I can also switch tools easily. For example, if I don’t want to use tmux anymore, I can replace it with another terminal multiplexer. If I don’t like i3’s status bar or my application launcher, I can replace them, too.

As you might have guessed, **configuring this kind of system needs some time, motivation and effort**. That’s why I wrote a book called “[Building Your Mouseless Development Environment](https://themouseless.dev)”. It describes in detail how to configure all the tools, how to create scripts to install the whole system with one command, and how to customize everything for your personal needs. If you don’t know much about the Linux shell, it lets you build a custom project to get familiar with it.

If you’re interested, you’ll find a [sample of the book here](https://themouseless.dev/content/building_mouseless_environment_sample.pdf) as well as its entire table of content.

I think the best way to find out if you’d like this kind of system is simply to try it. I can guarantee you one thing: you’ll learn a lot along the way!

### Further Reading on Smashing Magazine

- “[I Used The Web For A Day With Just A Keyboard](https://www.smashingmagazine.com/2018/07/web-with-just-a-keyboard/),” Chris Ashton
- “[A Complete Guide To Mechanical Keyboards](https://www.smashingmagazine.com/2020/05/complete-guide-mechanical-keyboards/),” Ben Frain
- “[Making A Strong Case For Accessibility](https://www.smashingmagazine.com/2021/07/strong-case-for-accessibility/),” Todd Libby
- “[Accessibility In Chrome DevTools](https://www.smashingmagazine.com/2020/08/accessibility-chrome-devtools/),” Umar Hansa

{{< signature "vf, yk, il" >}}
