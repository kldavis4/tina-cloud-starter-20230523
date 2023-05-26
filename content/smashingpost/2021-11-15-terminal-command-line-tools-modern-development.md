---
title: 'Powerful Terminal And Command-Line (CLI) Tools For Modern Web Development'
slug: powerful-terminal-commandline-tools-modern-web-development
author: louis-lazaris
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2d3081a-5a36-4763-9b94-13bf7d1cb5d6/powerful-terminal-commandline-tools-modern-web-development.jpg
date: 2021-11-15T13:00:00.000Z
summary: >-
  What’s your favorite command-line tool? Today, Louis Lazaris shares a collection of relevant command-line apps and utilities that he has personally come across in the past few years.
description: >-
  What’s your favorite command-line tool? In this post, Louis Lazaris shares a collection of relevant command-line apps and utilities that he has personally come across in the past few years. If there’s a useful one that hasn’t been mentioned and one you use regularly, please do share it in the comments.
categories:
  - Coding
  - Tools
  - Round-Ups
  - Techniques
---

Many modern programmers, including front-end and full-stack developers, work daily with the command line. Even those who are relatively new to web development are picking up command-line skills early and finding practical tools and utilities to enhance their productivity in the terminal.

This post presents a categorized list of many command-line apps I’ve personally discovered over the past few years. Some of them are relatively new, others have been around for a while. So I hope something in this roundup will interest you and help you get stuff done when working in the terminal.

You can jump to a category using the navigation below:

- [Terminal Apps](#terminal-apps)
- [Terminal Utilities and Enhancements](#terminal-utilities-and-enhancements)
- [Command-line Scripting and Frameworks](#command-line-scripting-and-frameworks)
- [Productivity Tools for the Terminal](#productivity-tools-for-the-terminal)

## Terminal Apps

This section features terminals, multiplexers, console emulators, mobile terminals, and command-line workspaces that you can use to replace the default terminal app on your system.

### `tmux`

[`tmux`](https://github.com/tmux/tmux) is a popular terminal multiplexer for Unix-like operating systems that lets you easily switch among several programs in a single terminal, with the ability to “detach” a session (while still running in the background) or “reattach” it to a different terminal.

{{< rimg breakout="true" href="https://github.com/tmux/tmux" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5982e51-254c-4834-8f4f-4afd3663cf5c/1-terminal-and-cli-tools.png" width="694" height="480" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5982e51-254c-4834-8f4f-4afd3663cf5c/1-terminal-and-cli-tools.png'>Large preview</a>)" alt="tmux" >}}

### `iTerm2`

[`iTerm2`](https://iterm2.com/), the successor to iTerm, is a replacement for your Terminal on macOS that includes features like split panes, robust search, autocomplete, instant replay, along with a whole slew of configuration options.

{{< rimg breakout="true" href="https://iterm2.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49202387-c48e-452a-8cbd-a053540528d0/2-terminal-and-cli-tools.png" width="800" height="285" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49202387-c48e-452a-8cbd-a053540528d0/2-terminal-and-cli-tools.png'>Large preview</a>)" alt="iTerm2" >}}

### Mosh

[Mosh](https://mosh.org/) is a remote terminal app (or mobile shell) for interactive SSH usage that includes several useful features for those who need to do terminal-based tasks over weak WiFi, cellular networks, or other less-reliable connections.

{{< rimg breakout="true" href="https://mosh.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09da513-8d82-44a6-9d0b-8e15eebf00ba/3-terminal-and-cli-tools.png" width="800" height="380" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09da513-8d82-44a6-9d0b-8e15eebf00ba/3-terminal-and-cli-tools.png'>Large preview</a>)" alt="Mosh" >}}

### Zellij

[Zellij](https://zellij.dev/) is a terminal workspace that has the base functionality of a terminal multiplexer (similar to tmux) but includes features that allow users to extend it and create a personalized environment via panes/tabs and plugins.

{{< rimg breakout="true" href="https://zellij.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55161bed-d69a-435e-ab95-7e147631314a/4-terminal-and-cli-tools.png" width="800" height="377" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55161bed-d69a-435e-ab95-7e147631314a/4-terminal-and-cli-tools.png'>Large preview</a>)" alt="Zellij" >}}

### Hyper

[Hyper](https://hyper.is/) is an Electron-based terminal app for Mac, Windows, or Linux that’s built with web technologies (HTML/CSS/JS). Includes dozens of themes and plugins and is built on speed and stability.

{{< rimg breakout="true" href="https://hyper.is/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21c74aa7-e4b6-4b8c-b655-ff95c0fbbc78/5-terminal-and-cli-tools.png" width="800" height="418" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21c74aa7-e4b6-4b8c-b655-ff95c0fbbc78/5-terminal-and-cli-tools.png'>Large preview</a>)" alt="Hyper" >}}

### `cmder`

[`cmder`](https://cmder.net/) is a portable console emulator for Windows that was built due to the lack of a good option in this area for Windows users.

{{< rimg breakout="true" href="https://cmder.net/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfd043f0-ffcf-4668-bb46-3a104830b3d5/6-terminal-and-cli-tools.png" width="800" height="394" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfd043f0-ffcf-4668-bb46-3a104830b3d5/6-terminal-and-cli-tools.png'>Large preview</a>)" alt="cmder" >}}

### a-Shell

[a-Shell](https://holzschu.github.io/a-Shell_iOS/) is an iOS app that offers a ‘terminal in your pocket’ with files/directory control, compatibility with Apple Shortcuts, multiple windows, and lots more.

{{< rimg breakout="true" href="https://holzschu.github.io/a-Shell_iOS/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e95b053-f85f-4cf1-9476-0404fa36799d/7-terminal-and-cli-tools.png" width="800" height="388" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e95b053-f85f-4cf1-9476-0404fa36799d/7-terminal-and-cli-tools.png'>Large preview</a>)" alt="a-Shell" >}}

### Eternal Terminal

[Eternal Terminal](https://eternalterminal.dev/) is another remote terminal app inspired by other similar, popular projects.

{{< rimg breakout="true" href="https://eternalterminal.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/077f5b6d-bd3a-44e3-9590-30e185e02c11/8-terminal-and-cli-tools.png" width="800" height="229" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/077f5b6d-bd3a-44e3-9590-30e185e02c11/8-terminal-and-cli-tools.png'>Large preview</a>)" alt="Eternal Terminal" >}}

### Ten Hands

[Ten Hands](https://tenhands.app/) is a terminal app for Mac, Linux, and Windows that is billed as the simplest way to organize and run command-line tasks, useful for those who run similar daily tasks on multiple projects.

{{< rimg breakout="true" href="https://tenhands.app/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/216d5520-62ad-4a4e-9172-602d067bcf5b/9-terminal-and-cli-tools.png" width="800" height="247" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/216d5520-62ad-4a4e-9172-602d067bcf5b/9-terminal-and-cli-tools.png'>Large preview</a>)" alt="Ten Hands" >}}

### eDEX-UI

[eDEX-UI](https://github.com/GitSquared/edex-ui) is a fullscreen, cross-platform terminal emulator and system monitor heavily inspired by science fiction movie UIs, in particular, the Tron: Legacy film.

{{< rimg breakout="true" href="https://github.com/GitSquared/edex-ui" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/651c07c0-12eb-427c-a39b-6602254acd4c/10-terminal-and-cli-tools.png" width="800" height="453" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/651c07c0-12eb-427c-a39b-6602254acd4c/10-terminal-and-cli-tools.png'>Large preview</a>)" alt="eDEX-UI" >}}

### Tabby

[Tabby](https://tabby.sh/), formerly “Terminus”, is a customizable cross-platform terminal app for local shells, SSH, serial, and Telnet connections that includes support for features like split panes, smart tabs, customizable hotkeys, and lots more.

{{< rimg breakout="true" href="https://tabby.sh/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae3a0cd-8c4a-4c24-8b40-b7ac10cc5c6a/11-terminal-and-cli-tools.png" width="800" height="396" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae3a0cd-8c4a-4c24-8b40-b7ac10cc5c6a/11-terminal-and-cli-tools.png'>Large preview</a>)" alt="Tabby" >}}

### Fish Shell

[Fish Shell](https://fishshell.com/) is another option for a command-line shell for Linux, macOS, and Windows that includes auto-suggest, tab completions, 24-bit color, web-based configuration, syntax highlighting, among other practical features.

{{< rimg breakout="true" href="https://fishshell.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4813717a-16e1-4e11-bd2c-9383de050dfd/12-terminal-and-cli-tools.png" width="800" height="201" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4813717a-16e1-4e11-bd2c-9383de050dfd/12-terminal-and-cli-tools.png'>Large preview</a>)" alt="Fish Shell" >}}

{{% feature-panel %}}

## Terminal Utilities And Enhancements

Once you’ve got your primary workspace, you’ll want to enhance it with various tools, utilities, themes, and so forth. This section includes some useful tools to make your terminal experience more enjoyable.

### Oh My Zsh

[Oh My Zsh](https://ohmyz.sh/) is an open-source, community-driven framework for managing your configuration for Z Shell (or Zsh, a popular Unix shell). It comes bundled with thousands of helpful functions, helpers, 300+ plugins, 140+ themes, and more. Works best on macOS or Linux, but can also be used on Windows using something like Cygwin or WSL2.

{{< rimg breakout="true" href="https://ohmyz.sh/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcfae738-6a51-471e-847d-d99a3fd87c88/13-terminal-and-cli-tools.png" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcfae738-6a51-471e-847d-d99a3fd87c88/13-terminal-and-cli-tools.png'>Large preview</a>)" alt="Oh My Zsh" >}}

### Fig

[Fig](https://github.com/withfig/autocomplete) adds VSCode-style autocomplete to your existing terminal and includes support for existing CLI tools like Git, npm, Kubernetes, Docker, AWS, Google Cloud, and more.

{{< rimg breakout="true" href="https://github.com/withfig/autocomplete" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4f0596e-9e3b-4326-822b-c02e7282e475/14-terminal-and-cli-tools.png" width="780" height="351" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4f0596e-9e3b-4326-822b-c02e7282e475/14-terminal-and-cli-tools.png'>Large preview</a>)" alt="Fig" >}}

### `fzf`

[`fzf`](https://github.com/junegunn/fzf) is a fast, portable, fuzzy finder for the command line that lets you run fuzzy search queries with a comprehensive feature set.

{{< rimg breakout="true" href="https://github.com/junegunn/fzf" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9faeaec-4be8-4381-8e14-cdc719ad4c44/15-terminal-and-cli-tools.png" width="800" height="453" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9faeaec-4be8-4381-8e14-cdc719ad4c44/15-terminal-and-cli-tools.png'>Large preview</a>)" alt="fzf" >}}

### Shell History

[Shell History](https://loshadki.app/shellhistory/) (not free) is a macOS app that integrates with Bash, Zsh, or Fish and allows you to easily backup and sync via iCloud and organize your shell history in “notebooks”.

{{< rimg breakout="true" href="https://loshadki.app/shellhistory/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a53bdef8-bf63-4ab7-b5fd-661fb2497e71/16-terminal-and-cli-tools.png" width="800" height="353" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a53bdef8-bf63-4ab7-b5fd-661fb2497e71/16-terminal-and-cli-tools.png'>Large preview</a>)" alt="Shell History" >}}

### `htop`

[`htop`](https://htop.dev/) is an interactive process viewer, originally Linux-only but now cross-platform, that aims to improve on the Linux `top` command by providing extra features when viewing running processes.

{{< rimg breakout="true" href="https://htop.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16fa5760-3e28-4a53-9f02-4b03bcb704f0/17-terminal-and-cli-tools.png" width="800" height="169" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16fa5760-3e28-4a53-9f02-4b03bcb704f0/17-terminal-and-cli-tools.png'>Large preview</a>)" alt="htop" >}}

### GitHub CLI

[GitHub CLI](https://cli.github.com/), in case you missed it, is the official cross-platform command-line interface for GitHub, bringing pull requests, issues, and other GitHub-related tasks to your terminal.

{{< rimg breakout="true" href="https://cli.github.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6541476-c15d-4b56-ae1f-28cf859393df/18-terminal-and-cli-tools.png" width="800" height="344" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6541476-c15d-4b56-ae1f-28cf859393df/18-terminal-and-cli-tools.png'>Large preview</a>)" alt="GitHub CLI" >}}

### Streamhut

[Streamhut](https://streamhut.io/) lets you share your terminal in real-time without installing anything. Simply run one of two commands (depending on your setup), useful for live terminal sessions in team collabs, interviews, or teaching.

{{< rimg breakout="true" href="https://streamhut.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9af5ba0-109b-458a-8c7e-f9376652625a/19-terminal-and-cli-tools.png" width="800" height="212" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9af5ba0-109b-458a-8c7e-f9376652625a/19-terminal-and-cli-tools.png'>Large preview</a>)" alt="Streamhut" >}}

### `icdiff`

[`icdiff`](https://www.jefftk.com/icdiff) is a terminal-based file diff tool that makes good use of colors to present diffs in a more practical, visual manner.

{{< rimg breakout="true" href="https://www.jefftk.com/icdiff" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22dff93-6b69-4893-83ee-b97fb9c084fd/20-terminal-and-cli-tools.png" width="800" height="352" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22dff93-6b69-4893-83ee-b97fb9c084fd/20-terminal-and-cli-tools.png'>Large preview</a>)" alt="icdiff" >}}

### `>\_TerminalSplash`

[`TerminalSplash`](https://terminalsplash.com/), as the name suggests, is like Unsplash, but for terminal themes. Choose from more than 200 user-submitted themes or submit your own.

{{< rimg breakout="true" href="https://terminalsplash.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca2a2088-c92b-4ff7-a6bb-d2c9c4013457/21-terminal-and-cli-tools.png" width="800" height="257" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca2a2088-c92b-4ff7-a6bb-d2c9c4013457/21-terminal-and-cli-tools.png'>Large preview</a>)" alt="TerminalSplash" >}}

### Terminalizer

[Terminalizer](https://terminalizer.com/) is a customizable and cross-platform terminal recorder that lets you record terminal sessions then share them as animated GIFs or via a web player.

{{< rimg breakout="true" href="https://terminalizer.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a417129-efee-4e61-9641-201c77374dcb/22-terminal-and-cli-tools.png" width="800" height="277" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a417129-efee-4e61-9641-201c77374dcb/22-terminal-and-cli-tools.png'>Large preview</a>)" alt="Terminalizer" >}}

### Asciinema

[Asciinema](https://asciinema.org/) is another popular option for terminal recording and sharing, but not available for Windows. The cool thing about this one is that the recorded output is not a video but a plain text animation of the terminal session, meaning you can select and copy/paste items from recordings.

{{< rimg breakout="true" href="https://asciinema.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/889299ec-c998-47c6-b1d6-59350637cfee/23-terminal-and-cli-tools.png" width="800" height="314" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/889299ec-c998-47c6-b1d6-59350637cfee/23-terminal-and-cli-tools.png'>Large preview</a>)" alt="Asciinema" >}}

### `gtop`

[`gtop`](https://github.com/aksakalli/gtop) is another enhancement on the `top` command that provides a system monitoring dashboard for your terminal. Require Node.js and includes partial support on Windows.

{{< rimg breakout="true" href="https://github.com/aksakalli/gtop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d325fba4-8a92-4751-a43e-ec5a8d53e4c7/24-terminal-and-cli-tools.png" width="800" height="297" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d325fba4-8a92-4751-a43e-ec5a8d53e4c7/24-terminal-and-cli-tools.png'>Large preview</a>)" alt="gtop" >}}

### `DevDash`

[`DevDash`](https://thedevdash.com/) is a highly configurable terminal dashboard for developers and creators. You can customize it to display information from sources like Google Analytics, GitHub, Feedly, shell command output, and more.

{{< rimg breakout="true" href="https://thedevdash.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81d01ac2-f073-45a0-9301-20b835645ef9/25-terminal-and-cli-tools.jpg" width="800" height="253" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81d01ac2-f073-45a0-9301-20b835645ef9/25-terminal-and-cli-tools.jpg'>Large preview</a>)" alt="DevDash" >}}

### Honorable mentions:

- [`ora`](https://github.com/sindresorhus/ora)  
An elegant terminal spinner.
- [`tiny-care-terminal`](https://github.com/notwaldorf/tiny-care-terminal)  
A little dashboard that tries to take care of you when you’re using your terminal.
- [`theme.sh`](https://github.com/lemnos/theme.sh)  
A shell script that lets you set your terminal theme that includes 270+ preloaded themes.

{{% ad-panel-leaderboard %}}

## Command-Line Scripting And Frameworks

Some numerous libraries and frameworks allow you to build and maintain your own command-line apps and utilities. Below you’ll find a few of those for Bash, JavaScript, and more.

### Command And Conquer (cac)

[Command And Conquer](https://github.com/cacjs/cac), also called cac, is a lightweight JavaScript framework for building command-line apps. For example, it’s been used to build several Node.js-based scaffolding tools.

{{< rimg breakout="true" href="https://github.com/cacjs/cac" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b96e436-e427-4f30-99b1-ade2b68548d9/26-terminal-and-cli-tools.png" width="800" height="289" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b96e436-e427-4f30-99b1-ade2b68548d9/26-terminal-and-cli-tools.png'>Large preview</a>)" alt="Command And Conquer" >}}

### `zx`

[`zx`](https://github.com/google/zx) is a popular alternative to Bash from engineers at Google that allows you to write command-line apps using JavaScript with an easy-to-use API that allows you to call executables and get their output, handle errors, and more.

{{< rimg breakout="true" href="https://github.com/google/zx" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/530b52be-d2d4-48ff-be28-6ab717d76dbc/27-terminal-and-cli-tools.png" width="798" height="527" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/530b52be-d2d4-48ff-be28-6ab717d76dbc/27-terminal-and-cli-tools.png'>Large preview</a>)" alt="zx" >}}

### `present`

[`present`](https://github.com/vinayak-mehta/present) is a Markdown-based presentation tool for the terminal that includes colors and effects and allows you to play pre-recorded playable code blocks as slides.

{{< rimg breakout="true" href="https://github.com/vinayak-mehta/present" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f605c062-bae2-42a0-bbdb-00cda134658b/28-terminal-and-cli-tools.png" width="800" height="205" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f605c062-bae2-42a0-bbdb-00cda134658b/28-terminal-and-cli-tools.png'>Large preview</a>)" alt="present" >}}

### Bach

[Bach](https://bach.sh/) is a Bash testing framework that can be used to test scripts that contain dangerous commands like `rm -rf /` and also includes APIs (e.g. `@mock`, `@ignore`, `@mockallto`, etc.) to mock commands.

{{< rimg breakout="true" href="https://bach.sh/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de1f9af-b086-4c21-8a30-2685ef9ec88a/29-terminal-and-cli-tools.png" width="800" height="387" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de1f9af-b086-4c21-8a30-2685ef9ec88a/29-terminal-and-cli-tools.png'>Large preview</a>)" alt="Bach" >}}

### `CLUI`

[`CLUI`](https://github.com/replit/clui) is a JavaScript API with utilities to allow you to build command-line interfaces with context-aware autocomplete into your apps (i.e. terminal-like applications that users interact with).

{{< rimg breakout="true" href="https://github.com/replit/clui" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e2fa228-42ad-4ca6-9d54-06ccabf2ec62/30-terminal-and-cli-tools.png" width="800" height="427" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e2fa228-42ad-4ca6-9d54-06ccabf2ec62/30-terminal-and-cli-tools.png'>Large preview</a>)" alt="CLUI" >}}

### `ShellCheck`

[`ShellCheck`](https://www.shellcheck.net/) is a shell extension to help you find bugs in your shell scripts.

{{< rimg breakout="true" href="https://www.shellcheck.net/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84155770-bd84-48b0-be43-8b7945b11cce/31-terminal-and-cli-tools.png" width="800" height="323" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84155770-bd84-48b0-be43-8b7945b11cce/31-terminal-and-cli-tools.png'>Large preview</a>)" alt="ShellCheck" >}}

### Honorable Mentions

- [`Bashō`](https://bashojs.org/)  
Lets you write complex shell tasks using plain JavaScript and it mixes well with shell commands and scripts.
- [`import`](https://import.sh/)  
A fast and easy-to-use module system for Bash and other Unix shells.
- [`Bash Infinity`](https://github.com/niieani/bash-oo-framework)  
A modular and lightweight library and boilerplate framework for writing tools using Bash.

{{% ad-panel-leaderboard %}}

## Productivity Tools For The Terminal

Finally, this category puts together a small sampling of command-line utilities and programs that help with various productivity-related tasks like keeping stuff organized, sharing files, and more.

### Dash Dash

[Dash Dash](https://dashdash.io/) is an online documentation site that presents the Unix man pages (i.e. manual pages) in a more palatable format, to help those less familiar with the terminal learn to use the command line.

{{< rimg breakout="true" href="https://dashdash.io/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a433284c-00cd-47cb-8cc9-057290fed6c2/32-terminal-and-cli-tools.png" width="800" height="436" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a433284c-00cd-47cb-8cc9-057290fed6c2/32-terminal-and-cli-tools.png'>Large preview</a>)" alt="Dash Dash" >}}

### `nb`

[`nb`](https://xwmx.github.io/nb/) is a command-line tool with features that include local web note‑taking, bookmarking, archiving, and encryption. Storage is in plain text, includes Git-based versioning, wiki-style linking, color themes, and lots more.

{{< rimg breakout="true" href="https://xwmx.github.io/nb/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91afb66b-dee3-495d-8edf-5556cf4659f7/33-terminal-and-cli-tools.png" width="800" height="436" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91afb66b-dee3-495d-8edf-5556cf4659f7/33-terminal-and-cli-tools.png'>Large preview</a>)" alt="nb" >}}

### `Rclone`

[`Rclone`](https://rclone.org/) is an open-source command-line program that allows you to manage files on 40+ cloud storage services (Amazon S3, Dropbox, Google Drive, Azure, etc.). It includes cloud equivalents for familiar Unix commands and other features.

{{< rimg breakout="true" href="https://rclone.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7d74416-924f-46c4-907a-3dd5e75ab063/34-terminal-and-cli-tools.png" width="800" height="217" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7d74416-924f-46c4-907a-3dd5e75ab063/34-terminal-and-cli-tools.png'>Large preview</a>)" alt="Rclone" >}}

### `navi`

[`navi`](https://github.com/denisidoro/navi) is an interactive cheatsheet tool for your terminal. In addition to other features, you can browse through cheatsheet repositories, import cheatsheets, or add your own.

{{< rimg breakout="true" href="https://github.com/denisidoro/navi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a208d63b-aea2-42ad-994c-f1cd26b47fda/35-terminal-and-cli-tools.png" width="800" height="400" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a208d63b-aea2-42ad-994c-f1cd26b47fda/35-terminal-and-cli-tools.png'>Large preview</a>)" alt="navi" >}}

### Taskbook

[Taskbook](https://github.com/klaussinani/taskbook) is a fast command-line tool that lets you organize tasks, boards, and notes in your terminal, with features like search/filter, custom storage location, and a simple and user-friendly syntax.

{{< rimg breakout="true" href="https://github.com/klaussinani/taskbook" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57dd369b-4097-432f-8bf4-4f81fdf196d5/36-terminal-and-cli-tools.png" width="800" height="508" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57dd369b-4097-432f-8bf4-4f81fdf196d5/36-terminal-and-cli-tools.png'>Large preview</a>)" alt="Taskbook" >}}

### Project Explorer

[Project Explorer](https://github.com/sdras/project-explorer) is a CLI tool that lets you build a tree visualization of any project. This would come in handy when bringing on new team members or when inheriting a new project.

{{< rimg breakout="true" href="https://github.com/sdras/project-explorer" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0190fb8-9613-4af8-937f-6fe2a50cfc24/37-terminal-and-cli-tools.png" width="800" height="260" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0190fb8-9613-4af8-937f-6fe2a50cfc24/37-terminal-and-cli-tools.png'>Large preview</a>)" alt="Project Explorer" >}}

### `transfer.sh`

[`transfer.sh`](https://transfer.sh/) is a fast and easy-to-use app for sharing files via the command line. Includes support for services like Amazon S3, Google Drive, Storj, and the local file system.

{{< rimg breakout="true" href="https://transfer.sh/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f27e50-7c8b-4107-8179-a04abe5568b7/38-terminal-and-cli-tools.png" width="800" height="519" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f27e50-7c8b-4107-8179-a04abe5568b7/38-terminal-and-cli-tools.png'>Large preview</a>)" alt="transfer.sh" >}}

### Honorable Mentions

- [`ack`](https://beyondgrep.com/)  
A code-searching tool, similar to grep but optimized for programmers searching large trees of source code.
- [`goto`](https://github.com/iridakos/goto)  
A shell utility with auto-complete support to navigate to aliased directories.
- [`bashupload`](https://bashupload.com/)  
Upload files (up to 50GB) via the command line to easily share between servers, desktops, and mobile devices.
- [`copyfiles`](https://github.com/calvinmetcalf/copyfiles)  
A command-line utility that adds extra features to copying files in your terminal.

## What’s Your Favourite Command-Line Tool?

As mentioned, this wasn’t meant to be an exhaustive list, but merely a big collection of relevant command-line apps and utilities that I’ve personally come across in the past few years.

If you’ve built something yourself or if there’s one you use regularly that supercharges your terminal experience, feel free to drop it in the comments!

{{< signature "vf, yk, il" >}}
