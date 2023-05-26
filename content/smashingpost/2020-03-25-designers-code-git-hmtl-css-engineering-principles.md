---
title: 'How Should Designers Learn To Code? Git, HTML/CSS, Engineering Principles (Part 2)'
slug: designers-code-git-hmtl-css-engineering-principles
author: paul-hanaoka
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d88baaa8-a961-4d2a-ab69-13c5990079d6/designers-code-git-hmtl-css-engineering-principles.png
date: 2020-03-25T14:00:00.000Z
summary: >-
  In [Part 1](https://www.smashingmagazine.com/2020/03/designers-code-terminal-text-editors-part-1/), Paul explained the basics of the terminal, shared a few productivity hacks to get you started, and how to choose a code editor. In this part, he’ll continue with the topics of version control (Git), HTML and CSS, semantic code, and a brief introduction to some key engineering principles.
description: >-
  In [Part 1](https://www.smashingmagazine.com/2020/03/designers-code-terminal-text-editors-part-1/), Paul explained the basics of the terminal, shared a few productivity hacks to get you started, and how to choose a code editor. In this part, he’ll continue with the topics of version control (Git), HTML and CSS, semantic code, and a brief introduction to some key engineering principles.
categories:
  - Tools
  - Workflow
  - Design
---

Literally, [tomes](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/) have been written on version control. Nevertheless, I will start by sharing a brief explanation and other introductory content to whet your appetite for further study. 

*Version control* ([not to be confused with *version history*](https://www.abstract.com/blog/version-history-version-control/)) is basically a way for people to collaborate in their own environments on a single project, with a single main source of truth (often called the “master” branch). 

I’ll go over today is the bare minimum you’ll need to know in order to download a project, make a change, and then send it to master.

*There are [many types](https://en.wikipedia.org/wiki/Version_control) of version control software and many tools for managing and hosting your source code (you may have heard of GitLab or Bitbucket). Git and GitHub are one of the more common pairs, my examples will reference GitHub but the principles will apply to most other source code managers.*

**Aside**:

- *For a more comprehensive and technical introduction, see [Tobias Gunther’s article](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/).*
- *If you prefer a more hands-on approach, [GitHub has an excellent step-by-step guide](https://guides.github.com/activities/hello-world/).*

<div class="c-felix-the-cat">
<h4 class="h3">Collecting Data, The Powerful Way</h4>
<p>Did you know that CSS can be used for collecting statistics? Indeed, there's even a CSS-only approach for tracking UI interactions using Google Analytics. <a href="https://www.smashingmagazine.com/2014/10/css-only-solution-for-ui-tracking/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## Your First Contribution

Before doing these steps, you’ll need a few things set up:

1. A [GitHub](https://github.com/join) account,
2. [Node and NPM installed](https://blog.teamtreehouse.com/install-node-js-npm-mac) on your computer,
3. A high tolerance for pain or a low threshold for asking others for help.

### Step 1: Fork (Get A Copy Of The Code On Your GitHub Account)

On GitHub, you will fork *(fork = create a copy of the code in your account; in the following illustration, the blue, orange, red, and green lines show forks)* the repository (repo) in question.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0fca56-aa6f-48bb-9608-12800110d89d/1-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb358ddf-c45f-419c-a1d4-758874fd5d78/1-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="By creating branches off of the master, it’s possible for multiple people to contribute to different areas of a project and then merge their work together. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de0fca56-aa6f-48bb-9608-12800110d89d/1-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

You do this by navigating to [the repo in GitHub](https://github.com/liferay-design/liferay.design) and clicking the “Fork” button, currently at the top right-hand corner of a repo. This will be the “origin” &mdash; your fork on your GitHub account.

As an example, navigating to [https://github.com/yourGitHubUsername/liferay.design](https://github.com/yourGitHubUsername/liferay.design) should show your fork of the Liferay.Design repo.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0852a45-02a9-4e4a-8342-6311e4258ab6/7-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0852a45-02a9-4e4a-8342-6311e4258ab6/7-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="This is victorvalle’s GitHub fork. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0852a45-02a9-4e4a-8342-6311e4258ab6/7-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

### Step 2: Clone (Download The Code To Your Computer)

In your terminal, navigate to where you’d like to store the code. Personally, I have a `/github` folder in my `/user` folder &mdash; it makes it easier for me to organize it this way. If you’d like to do that, here are the steps &mdash; after typing these commands into your terminal window, press the <kbd>↵</kbd> key to execute:

<div class="break-out">

<pre><code class="language-bash">cd ~/             ## you'll usually start in your root directory, but just in case you don't this will take you there
mkdir github      ## this creates a "github" folder — on OSX it will now be located at users/your-username/github
cd github         ## this command navigates you inside the github folder</code></pre>
</div>

Now that you’re in the `/github` folder, you will clone (download a copy of the code onto your computer) the repo.

<pre><code class="language-bash">clone https://github.com/yourGitHubUsername/liferay.design</code></pre>
   
Once you enter this command, you’ll see a bunch of activity in the terminal &mdash; something like this:

<pre><code class="language-bash">Cloning into 'liferay.design'...
remote: Enumerating objects: 380, done.
remote: Total 380 (delta 0), reused 0 (delta 0), pack-reused 380
Receiving objects: 100% (380/380), 789.24 KiB | 2.78 MiB/s, done.
Resolving deltas: 100% (189/189), done.
</code></pre>

### Step 3: Install (Get It Running On Your Machine)

Navigate into the `/project` folder. In this case, we’ll enter `cd liferay.design`. Most projects will include a *README.md* file in the `/root` folder, this is typically the starting place for installing and running the project. For our purposes, to install, enter `npm install`. Once it’s installed, enter `npm run dev`.

Congratulations! You now have the site available on your local computer &mdash; typically projects will tell you where it’s running. In this case, open up a browser and go to `localhost:7777`.

### Step 4: Commit (Make Some Changes And Save Them)

A commit is a collection of changes that you make; I’ve heard it described as saving your progress in a game. There are many opinions on how commits should be structured: mine is that you should create a commit when you’ve achieved one thing, and if you were to remove the commit, it wouldn’t completely break the project (within reason).

If you aren’t coming to a repo with a change in mind, a good place to go is the ‘Issues’ tab. This is where you can see what needs to be done in the project.

If you do have an idea for some change, go ahead and make it. Once you’ve saved the file(s), here are the steps required to create a commit:

<div class="break-out">

<pre><code class="language-bash">git status                                         ## this will print out a list of files that you've made changes in
git add path/to/folder/or/file.ext                 ## this will add the file or folder to the commit
git commit -m 'Summarize the changes you've made'  ## this command creates a commit and a commit message</code></pre>
</div>

**Tip**: *The best recommendation I’ve ever seen for commit messages is from Chris Breams’s “[How To Write A Git Commit Message](https://chris.beams.io/posts/git-commit/)”. A properly formed Git commit subject line should always be able to complete the following sentence: “If applied, this commit will [your subject line here].” For more info on commits, check “[Why I Create Atomic Commits In Git](https://dev.to/cbillowes/why-i-create-atomic-commits-in-git-kfi)” by Clarice Bouwer.*

### Step 5: Push (Send Your Changes To Your Origin)

Once you’ve made some changes on your computer, before they can be merged into the master branch (added to the project), they need to be moved from your local to your remote repo. To do this, enter `git push origin` in the command line.


### Step 6: Pull Request (Ask For Your Changes To Be Merged Into Upstream)

Now that your changes have gone from your fingers to your computer, to your remote repository &mdash; it’s now time to ask for them to be merged into the project via a pull request (PR).

The easiest way to do this is by going to your repo’s page in GitHub. There will be a small message right above the file window that says “This branch is X commits ahead repo-name:branch” and then options to “Pull request” or “Compare”. 

Clicking the “Pull request” option here will take you to a page where you can compare the changes and a button that says “Create pull request” will then take you to the “Open a pull request” page where you’ll add a title and include a comment. Being brief, but detailed enough in the comment, will help project maintainers understand your proposed changes.

There are CLI tools like [Node GH](https://nodegh.io/) (GitHub also recently released [a beta of their CLI tool](https://cli.github.com/)) that allow you to initiate and manage pull requests in the terminal. At this point you may prefer to use the web interface, and that’s great! So do I.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6750237-a47a-4bd2-8635-cf2e37a7b75a/6-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6750237-a47a-4bd2-8635-cf2e37a7b75a/6-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="The ‘Pull request’ and ‘Compare’ options will appear once your fork has diverged from the upstream repo. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6750237-a47a-4bd2-8635-cf2e37a7b75a/6-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

### Bonus Step: Remote (Link All The Repos)

At this point, we have three repository references:

1. `upstream`:  the main repo that you’re tracking, often it’s the repo that you forked;
2. `origin`:  the default name of the remote that you clone;
3. `local`:  the code that is currently on your computer.

So far, you have #2 and #3 &mdash; but #1 is important because it’s the primary source. Keeping these three things in-line with each other is going to help the commit history stay clean. This helps project maintainers as it eliminates (or at least minimizes) merge conflicts when you send pull requests (PR’s) and it helps you get the latest code and keep your local and origin repositories up-to-date.

{{% ad-panel-leaderboard %}}

### Set An Upstream Remote

To track the upstream remote, in your terminal enter the following:

<div class="break-out">

<pre><code class="language-css">git remote add upstream https://github.com/liferay-design/liferay.design</code></pre>
</div>

Now, check to see what remotes you have available &mdash; enter `git remote -v` into your terminal, you should see something like:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e51fc5e1-1cf1-4da9-a8ac-bf7d55305b29/5-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e51fc5e1-1cf1-4da9-a8ac-bf7d55305b29/5-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="<code>origin</code> and <code>upstream</code> are the most common labels for remotes &mdash; ‘origin’ is your fork, ‘upstream’ is the source. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e51fc5e1-1cf1-4da9-a8ac-bf7d55305b29/5-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

<div class="break-out">

<pre><code class="language-javascript">origin   https://github.com/yourGitHubUsername/liferay.design (fetch)
origin    https://github.com/yourGitHubUsername/liferay.design (push)
upstream  https://github.com/liferay-design/liferay.design (fetch)
upstream  https://github.com/liferay-design/liferay.design (push)</code></pre>
</div>

This will allow you to quickly get the latest version of what is upstream &mdash; if you haven’t worked in a repo in a long time and don’t have any local changes that you want to keep, this is a handy command that I use:

<pre><code class="language-css">git pull upstream master && git reset --hard upstream/master</code></pre>

[GitHub Help is a great resource for this](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/configuring-a-remote-for-a-fork) and many other questions you might have.

## HTML And CSS: Starting With Semantics

On the web, there is an endless supply of resources for learning HTML and CSS. For the purposes of this article, I’m sharing what I would recommend based on ~~the mistakes I made~~ how I first learned to write HTML and CSS. 

### What Are HTML And CSS?

Before we get any further, let’s define HTML and CSS.

HTML stands for HyperText Markup Language. 

Hypertext:

<blockquote><strong>“Hypertext</strong> is text displayed on a <a href="https://en.wikipedia.org/wiki/Computer_display">computer display</a> or other <a href="https://en.wikipedia.org/wiki/Electronic_devices">electronic devices</a> with references (<a href="https://en.wikipedia.org/wiki/Hyperlinks">hyperlinks</a>) to other text that the reader can immediately access.”<br /><br />&mdash; “Hypertext” on <a href="https://en.wikipedia.org/wiki/Hypertext">Wikipedia</a></blockquote>

Markup Language:

<blockquote>“…a system for <a href="https://en.wikipedia.org/wiki/Annotation">annotating</a> a <a href="https://en.wikipedia.org/wiki/Document">document</a> in a way that is <a href="https://en.wikipedia.org/wiki/Syntax_(logic)">syntactically distinguishable</a> from the text.”<br /><br />&mdash; “Markup Language” on <a href="https://en.wikipedia.org/wiki/Markup_language">Wikipedia</a></blockquote>

In case you also don’t know what a lot of those words mean &mdash; briefly put, HTML is the combination of references (links) between *documents* on the web, and *tags* that you use to give structure to those documents. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27ad60d8-9636-4806-a770-ddabeb324e64/3-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27ad60d8-9636-4806-a770-ddabeb324e64/3-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="There’s an HTML5 tag for pretty much any basic element &mdash; otherwise you can always use a <code>div</code>! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27ad60d8-9636-4806-a770-ddabeb324e64/3-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

For a thorough introduction to HTML and CSS, I highly recommend the [Introduction to HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML) and [CSS first steps](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps), both on the *Mozilla Developer Network (MDN)* web docs. That, along with the excellent articles that websites such as [CSS Tricks](https://css-tricks.com/), [24 Ways](https://24ways.org/) and countless of others provide, contain basically everything you’ll ever need to reference with regards to HTML/CSS.

There are two main parts of an **HTML** document: the `<head>` and the `<body>`. 
- The `<head>` contains things that aren’t displayed by the browser &mdash; metadata and links to imported [stylesheets](https://www.w3.org/TR/REC-html40/present/styles.html) and scripts.
- The `<body>` contains the actual content that will be rendered by the browser. To render the content, the browser reads the HTML, provides a base layer of styles depending on the types of tags used, adds additional layers of styles provided by the website itself (the styles are included in/referenced from the `<head>`, or are inline), and that is what we see in the end. (Note: There is often also the [additional layer of JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) but it’s outside of the scope of this article.)

**CSS** stands for Cascading Style Sheets &mdash; it is used to extend the HTML by making it easier to give documents a custom look and feel. A style sheet is a document that tells the HTML what elements should look like (and how they should be positioned) by setting rules based on tags, classes, IDs, and other selectors. *Cascading* refers to the method for determining which rules in a sheet take priority in the inevitable event of a rule conflict.

<blockquote>“‘Cascading’ means that styles can fall (or cascade) from one style sheet to another, enabling multiple style sheets to be used on one HTML document.”<br /><br />&mdash; <a href="https://css.maxdesign.com.au/selectutorial/advanced_cascade.htm">Cascade — Max Design</a></blockquote>

CSS often gets a bad reputation &mdash; in sites with lots of style sheets it can quickly become unwieldy, especially if there aren’t documented, consistent methods used (more on that later) &mdash; but if you use it in an organized fashion and following all the best practices, CSS can be your best friend. Especially with the [layout capabilities](https://www.smashingmagazine.com/2018/05/guide-css-layout/) that are now available in most modern browsers, CSS is not nearly as necessary to hack and fight as it once was.

Rachel Andrew wrote a great guide, [How To Learn CSS](https://www.smashingmagazine.com/2019/01/how-to-learn-css/) &mdash; and one of the best things to know before you start is that:

<blockquote>“You don’t need to commit to memorizing every CSS Property and Value.”<br /><br />&mdash; Rachel Andrew</blockquote>

Instead, it’s far more vital to learn the **fundamentals** &mdash; [selectors](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors), [inheritance](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance), [the box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model), and most importantly, [how to debug your CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Debugging_CSS) code (hint: you will need the [browser developer tools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools)).

<p>Don’t worry about memorizing the syntax for the <code>background</code> property, and don’t worry if you forget about how exactly to align stuff in Flexbox (the <a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">CSS Tricks Guide to Flexbox</a> is possibly one of my top-10 most visited pages, ever!); Google and Stack Overflow are your friends when it comes to CSS properties and values.</p>

<p class="c-pre-sidenote--left">Some code editors even <a href="https://code.visualstudio.com/docs/editor/intellisense">have built-in autocomplete</a> so you don’t even need to search on the web in order to be able to figure out all the possible properties of a border, for example.</p><p class="c-sidenote c-sidenote--right">One of my favorite new features in Firefox 70 is the <a href="https://hacks.mozilla.org/2019/10/firefox-70-a-bountiful-release-for-all/#developertools">inactive CSS rules indicator</a>. It will save you hours of time trying to figure out why a style isn’t being applied.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b1c7302-d01f-4869-b491-bb5cdc6c9e84/4-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b1c7302-d01f-4869-b491-bb5cdc6c9e84/4-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="Kids these days have it so easy! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b1c7302-d01f-4869-b491-bb5cdc6c9e84/4-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

## Semantics

Let’s start with **semantic code**. Semantics refers to the meanings of words, semantic code refers to the idea that there is meaning to the markup in any given language.

<p class="c-pre-sidenote--left">There are many reasons why semantics are important. If I could summarize this, I would say that if you learn and use semantic code, it will make your life a lot easier because you will get a lot of things for free &mdash; and who doesn’t like free stuff?</p><p class="c-sidenote c-sidenote--right">For a more complete introduction to semantic code, see <a href="https://boagworld.com/dev/semantic-code-what-why-how/">Paul Boag’s brief blog post on the topic</a>.</p>

Semantics gives you many benefits:

1. **Default styles**  
For example, using a headline tag `<h1>` for the title of your document will make it stand out from the rest of the document’s contents, much like a headline would. 
2. **Accessible content**  
[Your code will be accessible by default](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML), meaning it will work with [screen readers](https://alistapart.com/article/semantics-to-screen-readers/) and will be easier to [navigate with a keyboard](https://web.dev/use-semantic-html/).
3. **SEO benefits**  
Semantic markup is easier for a machine to read, which makes it [more accessible to search engines](https://dev.to/yashints/let-s-talk-seo-10-tips-you-should-know-4n6k).
4. **Performance benefits**  
[Clean HTML is the foundation](https://www.oreilly.com/library/view/designing-for-performance/9781491903704/ch04.html) for a high-performing site. And clean HTML will also likely lead to cleaner CSS which means less code overall, making your site or app faster.

**Note:** *For a more in-depth look into semantics and HTML, [Heydon Pickering](https://twitter.com/heydonworks) wrote “[Structural Semantics: The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)” which I highly recommend reading.*

## Engineering Principles And Paradigms: The Basics

### Abstraction

There are tons of applications, tangents, and levels we could explore over the concept of abstraction &mdash; too many for this article which is intended to give you a brief introduction into concepts so that you are aware of them as you continue to learn.

Abstraction is a foundational engineering paradigm with a wide variety of applications &mdash; for the purposes of this article, abstraction is separating form from function. We’ll apply this in three areas: tokens, components, and the Don’t Repeat Yourself principle.

#### Tokens

If you’ve used a modern design tool for any length of time, you’ve probably encountered the idea of a **token**. Even Photoshop and Illustrator now have this idea of shared styles in a centralized library &mdash; instead of hard-coding values into a design, you use a token. If you’re familiar with the concept of CSS or SASS variables, you’re already familiar with tokens.

One layer of abstraction with tokens is to assign a name to a color &mdash; for example, `$blue-00` can be mapped to a hex value (or an HSL value, or whatever you want) &mdash; let’s say `#0B5FFF`. Now, instead of using the hex value in your stylesheets, you use the token value &mdash; that way if you decide that `blue-00` is actually `#0B36CE`, then you only have to change it in a single place. This is a nice concept.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e93dd0c-6186-431c-a40c-40f7a7161b66/2-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e93dd0c-6186-431c-a40c-40f7a7161b66/2-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png" sizes="100vw" caption="Tokens for colors in the Lexicon Alerts component helps keep things DRY. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e93dd0c-6186-431c-a40c-40f7a7161b66/2-how-should-designers-learn-to-code-git-hmtl-css-engineering-principles.png'>Large preview</a>)" alt="" >}}

If you take this same paradigm of abstraction and go a layer further, you can *token-ception* &mdash; and assign a variable to a functional value. This is particularly useful if you have a robust system and want to have different themes within the system. A functional example of this would be assigning a variable like `$primary-color` and map that to `$blue-00` &mdash; so now you can create markup and instead of referencing blue, you’re referencing a functional variable. If you ever want to use the same markup, but with a different style (theme), then you only need to map `$primary-color` to a new color, and your markup doesn’t need to change at all! Magic! 

#### Components

In the past 3-4 years, the idea of components and [componentization](https://en.wikipedia.org/wiki/Component-based_software_engineering) has become more relevant and accessible to designers. The concept of symbols ([pioneered by Macromedia/Adobe Fireworks](https://www.smashingmagazine.com/2012/06/developing-a-design-workflow-in-adobe-fireworks/#creating-and-using-symbols), later [expanded by Sketch](https://www.smashingmagazine.com/2017/04/symbols-sketch/), and then taken to the next level by Figma and Framer), is now more widely available in most design tools (Adobe XD, InVision Studio, Webflow, and many others). Componentization, even more than tokens, can separate the form of something from the function of it &mdash; which helps to improve both the form and the function.

One of the more notable early examples is [Nicole Sullivan’s media object component](https://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/). At first glance you might not realize that a whole page is essentially composed of a single component, rendered in different ways. In this way, we can re-use the same markup (form), modifying it slightly by passing in options or parameters, and styles &mdash; and have it provide a variety of value (function).

#### Don’t Repeat Yourself

**DRY** ([Don’t Repeat Yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)) is one of my favorite principles &mdash; creating things that can be reused over and over is one of the small victories you can have when coding.

While you often can’t ([and arguably shouldn’t](https://dev.to/wuz/stop-trying-to-be-so-dry-instead-write-everything-twice-wet-5g33)) strive to apply the DRY principle 100% of the time, every time &mdash; it’s at least beneficial to be aware of this so that as you’re working, you can consider how you can make whatever you’re working on more reusable. 

**A note on the Rule of Three:** A corollary to the DRY principle is the rule of three &mdash; essentially, once you re-use (copy/paste) something three times, you should rewrite it into a reusable component. Like the [Pirate’s Code](https://www.youtube.com/watch?v=k9ojK9Q_ARE), it’s more of a guideline than a hard and fast rule, and can vary from component to component and from project to project.  

{{% ad-panel-leaderboard %}}

## CSS And Styling Methodologies: Atomic vs. BEM

There are a lot of different ways to organize and write CSS code &mdash; Atomic and BEM are only two of the many that you’re likely to come across. You don’t have to “pick” a single one, nor do you have to follow them exactly. Most of the teams I’ve worked with usually have their own unique blend, based on the project or technology. It is helpful to be familiar with them so that over time, you can learn which approach to take depending on the situation.

All of these approaches go beyond “just” CSS and styling, and can often influence the tooling you use, the way you organize your files, and potentially the markup.

### Atomic CSS

Not to be confused with Atomic Web Design &mdash; atomic (perhaps more aptly referred to as “functional”) CSS, is a methodology that essentially favors using small, single-purpose classes to define visual functions. A few notable libraries:

1. [Atomic CSS](https://acss.io/) by [Steve Carlson](https://github.com/src-code);
2. [Tachyons](https://tachyons.io/) by [Adam Morse](https://mrmrs.cc/);
3. [Tailwind CSS](https://tailwindcss.com/) by [Adam Wathan](https://github.com/adamwathan).

What I like about this method is that it allows you to quickly style and theme things &mdash; one of the biggest drawbacks is that your markup can get pretty cluttered, pretty fast.

Check [John Polacek’s article on CSS-tricks](https://css-tricks.com/lets-define-exactly-atomic-css/) for a full introduction to Atomic CSS.

### BEM

The BEM philosophy is a great precursor to a lot of the modern JavaScript frameworks like Angular, React, and Vue.

<blockquote>“BEM (Block, Element, Modifier) is a component-based approach to web development.”<br /><br />&mdash; <a href="https://en.bem.info/methodology/quick-start/">BEM: Quick Start</a></blockquote>

Basically, everything that can be reused is a block. Blocks are comprised of elements, something that can’t be used outside of a block, and potentially other blocks. Modifiers are things that describe the status of something or the way it looks or behaves.

Personally, I like the theory and philosophy of BEM. What I do not like is the way that things are named. Way too many underscores, hyphens, and it can feel unnecessarily repetitive (`.menu`, `.menu__item`, etc).

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/06/bem-for-beginners/">BEM For Beginners</a> written by Inna Belaya</em></p>

## Thank U, Next(.js)

After you have sufficiently mastered these topics, don’t worry, there is still plenty to learn. Some suggestions:

1. **Functional and object-oriented programming**  
We touched on it lightly, but there’s plenty more to learn beyond CSS.
2. **Higher-level languages and frameworks**  
Typescript, Ruby, React, Vue are the next things you’ll tackle once you have a strong grasp of HTML and CSS.
3. **Querying languages and using data**  
Learning about GraphQL, MySQL, REST APIs will take your coding ability to the next level.

## Conclusion: Designers Who Code != Software Engineers

Hopefully, this article has shown you that learning to code isn’t as difficult as you may have previously thought. It can take a lot of time, but the amount of resources available on the internet is astounding, and they’re not decreasing — quite the opposite! 

One significant point that I want to emphasize is that “coding” is not the same as “software engineering” &mdash; being able to fork a repo and copy/paste in code from Stack Overflow can get you a long way, and while most, if not all, software engineers that I know have done that &mdash; you must use your new-found skills with wisdom and humility. For everything you can now access with some engineering prowess, there is that much more that you don’t know. While you may think that a feature or style is easy to accomplish because &mdash; “Hey, I got it working in devtools!” or “I made it work in Codepen.” &mdash; there are many engineering processes, dependencies, and methods that you probably don’t know that you don’t know. 

All of that is to say &mdash; don’t forget that we are still designers. Our primary function is to add business value through the lens of understanding customer or user problems and synthesizing them with our knowledge of design patterns, methods, and processes. Yes, being a “designer who writes code” can be very useful and will expand your ability to add this value &mdash; but we still need to let engineers make the engineering decisions.

## Anything Amiss?

There’s a good chance that something in this post was obscure, obtuse, and/or obsolete and I’d love the opportunity to make it better! Please leave a comment below, [DM me](https://twitter.com/messages/compose?recipient_id=46027705), or [@mention](https://twitter.com/compose/tweet) me on Twitter so I can improve.

### Further Reading

1. [Coding Bootcamps vs. Computer Science Degrees: What Employers Want and Other Perspectives](https://medium.com/bits-and-behavior/coding-bootcamps-vs-computer-science-degrees-what-employers-want-and-other-perspectives-4058a67e4f15) (Kyle Thayer)
2. [How To Start Using Sketch And Framer X](https://www.smashingmagazine.com/2019/06/start-using-sketch-framer-x/) (by Martina Pérez, *Smashing Magazine*)
3. [Introduction To Linux Commands](https://www.smashingmagazine.com/2012/01/introduction-to-linux-commands/) (by Paul Tero, *Smashing Magazine*)
4. [Become A Command-Line Power User With Oh My ZSH And Z](https://www.smashingmagazine.com/2015/07/become-command-line-power-user-oh-my-zsh-z/) (by Wes Bos, *Smashing Magazine*)
5. [A list of the common cmd.exe and Unix commands that you can use in PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/learn/using-familiar-command-names?view=powershell-7) (*Microsoft Docs*) 
6. [regular-expressions.info](https://www.regular-expressions.info) (by Jan Goyvaerts)
7. [regexone.com](https://regexone.com) (learn regular expressions with simple interactive exercises)
8. [Batch Resizing Using Command Line and ImageMagick](https://www.smashingmagazine.com/2012/09/resizing-bash-script-batch-resizing-using-command-line/) (by Vlad Gerasimov, *Smashing Magazine*) 
9. [Shortcuts And Tips For Improving Your Productivity With Sublime Text](https://www.smashingmagazine.com/2016/06/shortcuts-and-tips-for-improving-your-productivity-with-sublime-text/) (by Jai Pandya, *Smashing Magazine*) 
10. [Visual Studio Code Can Do That?](https://www.smashingmagazine.com/2018/01/visual-studio-code/) (by Burke Holland, *Smashing Magazine*) 
11. [Why version history is not version control](https://www.abstract.com/blog/version-history-version-control/) (by Josh Brewer)
12. [Modern Version Control With Git](https://www.smashingmagazine.com/2011/07/modern-version-control-with-git-series/) (by Tobias Günther, *Smashing Magazine*)
13. “[Hello World](https://guides.github.com/activities/hello-world/)” (a GitHub step-by-step guide)
14. [How to Install Node.js and NPM on a Mac](https://blog.teamtreehouse.com/install-node-js-npm-mac) (by Dave McFarland)
15. [How to Install Node.js and NPM on Windows](https://phoenixnap.com/kb/install-node-js-npm-on-windows) (by Dejan Tucakov)
16. [Why I Create Atomic Commits In Git](https://dev.to/cbillowes/why-i-create-atomic-commits-in-git-kfi) (by Clarice Bouwer)
17. [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/) (by Chris Breams)
18. [Semantic code: What? Why? How?](https://boagworld.com/dev/semantic-code-what-why-how/) (by Paul Boag)
19. [Structural Semantics: The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/) (by Heydon Pickering, *Smashing Magazine*)
20. [Designing for Performance: Chapter 4. Optimizing Markup and Styles](https://www.oreilly.com/library/view/designing-for-performance/9781491903704/ch04.html) (by Lara C. Hogan, *O’Reilly Media*)
21. [The media object saves hundreds of lines of code](https://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/) (by Nicole Sullivan)
22. [Let’s Define Exactly What Atomic CSS is](https://css-tricks.com/lets-define-exactly-atomic-css/) (by John Polacek, *CSS Tricks*)
23. [BEM For Beginners: Why You Need BEM](https://www.smashingmagazine.com/2018/06/bem-for-beginners/) (by Inna Belaya, *Smashing Magazine*)
24. [Javascript for Cats: An Introduction for New Programmers](https://jsforcats.com/)
25. [Roadmap.sh: Frontend Developer](https://roadmap.sh/frontend)
26. [Functional Programming vs OOPS : Explain Like I'm Five](https://dev.to/nijeesh4all/functional-programming-vs-oops--explain-x-like-im-five-2fnc)
27. [Why, How, and When to Use Semantic HTML and ARIA](https://css-tricks.com/why-how-and-when-to-use-semantic-html-and-aria/) (by Adam Silver, *CSS Tricks*)
28. [HTML Semantics](https://www.smashingmagazine.com/ebooks/html-semantics/) (an eBook by *Smashing Magazine*)
29. [The Fundamentals - HTML + CSS](https://syntax.fm/show/158/the-fundamentals-html-css) (on *Syntax.fm*)
30. [Cascade and inheritance](https://www.westciv.com/style_master/academy/css_tutorial/advanced/cascade_inheritance.html) (*westciv.com*)
31. [CSS Tricks](https://css-tricks.com/) (by Chris Coyier)
32. [Getting Started With CSS Layout](https://www.smashingmagazine.com/2018/05/guide-css-layout/) (by Rachel Andrew, *Smashing Magazine*)
33. [Introduction to HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML) (MDN web docs)
34. [CSS first steps](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps) (MDN web docs)
35. [JavaScript First Steps](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps) (MDN web docs)
36. [24 Ways](https://24ways.org/) (by Drew McLellan)

{{< signature "mb, yk, il" >}}
