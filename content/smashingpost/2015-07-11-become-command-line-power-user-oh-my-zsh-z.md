---
title: Become A Command-Line Power User With Oh My ZSH And Z
slug: become-command-line-power-user-oh-my-zsh-z
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ebbd491-0226-4e2c-86f5-377acd7bdd1a/02-agnoster-opt-small.png
date: 2015-07-11T08:35:42.000Z
author: wes-bos
description: >-
  The command line is increasingly becoming a part of every web developer's
  workflow. With tools like Grunt, Gulp and Bower leveraging the increase in
  productivity that comes with working in the command line, we are seeing it
  become a much more **friendly and comfortable place for beginners** and
  experts alike.

  This article provides insight into some of the best tools to use in your
  day-to-day workflow in the command line and gets you started with a totally
  customized setup.
categories:
  - Coding
  - Workflow
---
The command line is increasingly becoming a part of every web developer's workflow. With tools like Grunt, Gulp and Bower leveraging the increase in productivity that comes with working in the command line, we are seeing it become a much more **friendly and comfortable place for beginners** and experts alike.

This article provides insight into some of the best tools to use in your day-to-day workflow in the command line and gets you started with a totally customized setup. Also, please make sure to check out my [series on how to become a command-line power user](https://commandlinepoweruser.com/), available for free, of course.</p>

<figure><br>
<div class="aspect-ratio"><iframe loading="lazy" src="https://player.vimeo.com/video/133209811" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>
</figure>

## Getting The Right Terminal

Before we can start using ZSH, Z and related tools, getting the right terminal application up and running would be extremely helpful. The default Terminal and Powershell applications on OS X and Windows leave much to be desired.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [VI Editor / Linux Terminal Cheat Sheet (PDF)](https://www.smashingmagazine.com/2010/05/vi-editor-linux-terminal-cheat-sheet-pdf//)
*   [Introduction To Linux Commands](https://www.smashingmagazine.com/2012/01/introduction-to-linux-commands/)
*   [Advanced WordPress Management With WP-CLI](https://www.smashingmagazine.com/2015/09/wordpress-management-with-wp-cli/)
*   [How To Develop An Command Line Application Using Node.js](https://www.smashingmagazine.com/2017/03/interactive-command-line-application-node-js/)

For **OS X users**, [iTerm 2](https://www.iterm2.com/) is recommended as a replacement for OS X’s default Terminal. iTerm 2 introduces some features that are missing in the regular terminal, including commands you would regularly use in your text editor. This includes pane splitting, custom color schemes, paste history, fine-grained control over hotkeys, together with [dozens](https://www.iterm2.com/features.html) of other handy preferences that you will find useful as you become more comfortable in the terminal.

On **Windows** we have the built-in PowerShell. Most users find this quite different to the interface of the typical UNIX servers used to host websites; it's also rarely addressed in online tutorials. For this reason, it's recommended to use an emulator that provides a closer experience to a real UNIX command line, like Linux and OS X do.

You have a couple of options here. The easiest would be to install Cmdr, which provides Git integration, custom prompt and color schemes out of the box. For most, this will be more than enough to get started with all major web development tooling. It cannot, however, do any of the ZSH and Z that we will be exploring below.

For a full-blown UNIX emulation, there is [Cygwin](https://www.cygwin.com/) which allows us to run all UNIX commands as well as to work with Oh My ZSH. It's not for the faint of heart, but if you are fairly comfortable with Windows, it might be worth trying out. Alternatively there is the all-in-one [OH MY CYGWIN](https://github.com/haithembelhaj/oh-my-cygwin), which might speed up your installation process.</p>

## Use ZSH and Oh My ZSH

When you start a terminal application, whether it be on your server or your local computer, it is running a shell called **Bash**. Bash is by far the most popular shell and comes with pretty much every UNIX-based operating system. There are, however, alternatives to Bash that make using the terminal faster and more comfortable for web developers.

One of the most popular shells with web developers is the Z shell, or ZSH. Along with that, we use a ZSH framework named [Oh My ZSH](https://ohmyz.sh/).

Installing Oh My ZSH is very simple. Simply run the following command and restart your terminal:

<pre><code class="language-bash">
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
</code></pre>

Now, each time you start a terminal session, you will be using ZSH rather than the default Bash!

## ZSH Settings

Before jumping into the next few sections, we need to know about ZSH settings. These are stored in a `.zshrc` file located in your home directory. It's a hidden file, so you might not see it in your home directory, but you can view it by running `open ~/.zshrc` from the terminal. Swap out `open` with your favorite editor command, such as `nano`, `subl` or `vim`.

Now, we aren't making any changes to this file just yet, but leave it open. Whenever you make a change to this file, you need to **source** it in order for the changes to take effect in your terminal. To do this, you can either close the current tab and open a new one or run the `source ~/.zshrc` command from the terminal.</p>

## Terminal Customization

Customizing what your terminal looks like is one of the best things you can do. Not only does it make you look like a bad-ass coder, but it can greatly improve readability via different colors. It can also improve productivity by displaying important information related to file path, Git status and more!

### Prompts

Prompts are the line(s) of text shown when you are about to type something into the terminal. Your prompt provides useful information related to your project, such as the current version of Ruby, Node.js and so on, the current status of your Git repository, the outcome of the last run task, as well as the current working directory.

You can customize your path into oblivion, but chances are that someone has created a prompt that already suits your needs.

Your ZSH theme is set in the few lines of your `.zshrc` file. Look for something like `ZSH_THEME="robbyrussel"` — this is the default theme that comes with ZSH. I recommend setting this to `ZSH_THEME="random"`, which will randomly assign a theme each time you open a new terminal tab or run `source ~/.zshrc`. Run this a few times until you find one you like; you can find the current theme name by running `echo $ZSH_THEME`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8edca4f2-ae08-4e00-a428-cba0c2f07c9f/01-cobald2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ff0d7e1-3e48-4ebe-840d-7272b635fef0/01-cobald2-opt-small.png" alt="oh my zsh" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8edca4f2-ae08-4e00-a428-cba0c2f07c9f/01-cobald2-opt.png">View large version</a>)</figcaption></figure>

You can browse all the ZSH themes and prompts in the [wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/themes). Because there are hundreds of themes, not all of them come with ZSH by default. Any you want will need to be downloaded and placed in `~/.oh-my-zsh/themes`; Because this is a hidden directory, you can access it by running `open ~/.oh-my-zsh/themes`.

Here are a few popular themes:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c47073f2-7591-4627-a79d-1613b8ce3a34/02-agnoster-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ebbd491-0226-4e2c-86f5-377acd7bdd1a/02-agnoster-opt-small.png" alt="02-agnoster-opt-small" /></a><figcaption><a href="https://github.com/robbyrussell/oh-my-zsh/wiki/themes#agnoster">Agnoster</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c47073f2-7591-4627-a79d-1613b8ce3a34/02-agnoster-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbde88b-7dd3-4ca6-98a7-240f7a5e13be/03-cobalt2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0c7ddae-8990-4ca7-be7e-b9d8ea75d14c/03-cobalt2-opt-small.png" alt="03-cobalt2-opt-small" /></a><figcaption><a href="https://github.com/wesbos/Cobalt2-iterm">Cobalt2</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbbde88b-7dd3-4ca6-98a7-240f7a5e13be/03-cobalt2-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91fe9503-0b9c-45cf-bd72-6992cb94d271/04-bira-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f3ae40f-5841-4f76-ba5f-07bdbe64d041/04-bira-opt-small.png" alt="04-bira-opt-small" /></a><figcaption><a href="https://github.com/robbyrussell/oh-my-zsh/wiki/themes#bira">Bira</a>  (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91fe9503-0b9c-45cf-bd72-6992cb94d271/04-bira-opt.png">View large version</a>)</figcaption></figure>

**Note:** Many of these themes require a patched font to display the arrows and Git icons. You can [download the fonts on GitHub](https://github.com/powerline/fonts); then, make sure to set them in your iTerm2 settings.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2b0d27-a8dd-45d6-b88c-8b2f3f17bf0a/05-bira-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2964ef3-4397-4096-9164-4f13bb501243/05-bira-opt-small.png" alt="05-bira-opt-small" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2b0d27-a8dd-45d6-b88c-8b2f3f17bf0a/05-bira-opt.png">View large version</a>)</figcaption></figure>

### Color Schemes

Now, the prompts define the standard color to be used, but we’ll use iTerm2 themes to customize what those colors actually look like. By default, the themes come with your basic red, green, yellow and blue, but we can tweak those to be the exact variants that we want.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e426488-31eb-44a0-9a68-4f77dd3d3c46/06-schemes-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2097bbec-2a92-4463-88cf-b3f7c7fb5eb7/06-schemes-opt-small.png" alt="06-schemes-opt-small" /></a><figcaption>You can think of these colors as variables we can tweak. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e426488-31eb-44a0-9a68-4f77dd3d3c46/06-schemes-opt.png">View large version</a>)</figcaption></figure>

You can edit the colors or even make your own theme in “Preferences” → “Profiles” → “Colors,” or grab one of the existing themes already out there.

The ZSH Cobalt2 prompt also comes with an [iTerm2 theme](https://github.com/wesbos/Cobalt2-iterm), and you can find [hundreds of them](https://github.com/search?q=iterm+extension%3Aitermcolors&ref=searchresults&type=Repositories&utf8=%E2%9C%93) with a GitHub search; Bastien Dejean’s repository in particular houses a few interesting ones.</p>

## File Tabbing

So, now that our terminal is looking great, what can we actually do with ZSH and related tools? Probably one of the most useful features of ZSH is that it enables us to list and tab through files and folders. If you have ever tried to perfectly spell the name of a file, struggled with the case or fought with an impossibly long list of folders with spaces in it, you know the pain and limitations of Bash.

Folder and file tabbing works with any terminal command: `cd`, `trash`, `cp`, `open`, `subl`, etc. But for the purposes of this tutorial, let's use `cd` for folders and `open` for files.

Go ahead and type `cd` (note the space after `cd`), and hit the “Tab” key **twice**. You can now use your arrow keys to move over, up and down through the files and folders. To select a folder, hit “Return.” You can now hit “Tab” and “Tab” again to discover subdirectories or hit “Return” to run the command.</p>

<figure><br>
<div class="aspect-ratio"><iframe loading="lazy" src="https://player.vimeo.com/video/132812873" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>
</figure>

This also works for completing file and folder names. Let's say I've got two folders, `css/` and `/Capitalize`. If I type `cd c` and then hit “Tab” twice, I'll be able to cycle through all of the folders that start with C. You'll noticed it's case-insensitive. This is extremely helpful when you have many files with similar names.</p>

{{< vimeo id="132812871" >}}

Finally, this also works with command names whose names you might not totally remember. For example, if you’re working with MongoDB, 13 commands are associated with it: `mongod`, `mongodump`, `mongoexport`, `mongofiles mongoimport` and so on

By typing `mong` and hitting “Tab,” you'll see all available commands that start with `mong`.</p>

<figure><br>
<div class="aspect-ratio"><iframe loading="lazy" src="https://player.vimeo.com/video/132812872" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>
</figure>

## ZSH Plugins

ZSH allows you to extend built-in functionality by adding plugins, and it actually ships with a bunch of fantastic ones. To enable a plugin, open your `.zshrc` file and scroll down until you see the spot where active plugins are defined. To add a new one, just type the name between the parentheses, making sure to include a space between each name.</p>

<pre><code class="language-bash">
plugins=(git cloudapp node npm bower brew osx extract z)
</code></pre>

Once you’ve added a plugin, you'll need to either run `source ~/.zshrc` or open a new tab.

Some recommended ones are:

*   **git**
    Enabled by default with Oh My Zsh, this enables Git aliases, tab completion and descriptions of all Git commands.
    `git` + `tab`
*   **cloudapp**
    Enables uploading of files to CloudaApp right from the command line.
    `cloudapp Archive.zip`
*   **node**
    Opens the Node.js API for your current version in your browser.
    `node-docs http`
*   **npm**
    Adds autocompletion to npm, displaying all npm commands.
    `npm` + `tab`
*   **bower**
    Adds autocompletion for Bower commands.
    `bower` + `tab`
*   **brew**
    Adds autocompletion and descriptions for all Brew commands.
    `brew` + `tab`
*   **osx**
    Enables a number of [Finder commands](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins#osx) that are accessible via the terminal.
*   **extract**
    Unzip all types of compressed files.
*   **z**
    More on this in the next section!

View the entire list of plugins on the [Oh-My-ZSH wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins).</p>

## Using Z To Jump To “Frecent” Folders

Z isn't part of Oh My ZSH, but it's the perfect companion for anyone who heavily uses the command line. The idea behind Z is that it builds a list of your most frequent and recent — “Frecent” — folders and allows you to jump to them quickly in one command, rather than having to tab through a nested folder structure.

To install it, make sure Z is included in the plugins list from above. While this works for most, some users have trouble getting this to work. If that is the case, download [download Z](https://github.com/rupa/z/blob/master/z.sh) and put it in your home directory so that it's located at `~/z.sh`. Then, in your `.zshrc` file, include the following and then source your `.zshrc` file again.</p>

<pre><code class="language-bash">
# include Z, yo
. ~/z.sh
</code></pre>

Once it is installed, continue with your regular traversing of directories with your `cd` command. Z is watching where you frequently and recently have been, and is building a weighted list of directories.

After a few hours of moving around, you can use the `z` command followed by a word that is in your directory. It uses fuzzy matching to figure out what folder you are trying to get to, and it's almost always right!

*   `z styles` might bring you to `~/Dropbox/projects/0202-coffee-shop/styles`.
*   `z pizza` might bring you to `~/Dropbox/projects/0300-pizza/`.
*   `z pizza styles` might bring you to `~/Dropbox/projects/0300-pizza/styles`.
*   `z 303` might bring you to `~/Dropbox/projects/0303/candy-store/`.

For a full list of advanced Z commands, visit the [GitHub repository](https://github.com/rupa/z), or watch the Command Line Power User video on Z.</p>

## More, More, More!

As developers, we know how important it is to sharpen our tools and continually add new ones to our workflow. The command line is one of the best tools you can master as a developer. With this article, we are just scratching the surface of what we can do with the command line. Check out [Command Line Power User](https://CommandLinePowerUser.com) for all 11 free videos about getting comfortable with the command line.

{{< signature "al" >}}

