---
title: 'Useful VS Code Extensions For Front-End Developers'
slug: useful-vs-code-extensions-web-developers
author: cosima-mielke
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c5dbb73-94e1-486f-9daa-351699faaa2d/peacock-extension.png
date: 2021-05-27T13:30:00.000Z
summary: >-
  Meet useful Visual Studio Code extensions for web developers: little helpers to minimize slow-downs and frustrations, and boost developer’s workflow along the way. Recently, we’ve also covered [CSS auditing tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/), [CSS generators](https://www.smashingmagazine.com/2021/03/css-generators/) and [accessible front-end components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/) &mdash; you might find them useful, too.
description: >-
  Meet useful Visual Studio Code extensions for web developers: little helpers to minimize slow-downs and frustrations, and boost developer’s workflow along the way. With auto log messages, auto code formatting, file utils, file labels, code snippets, highlight brackets, tags, indents and workspaces, onboarding and remote SSH.
categories:
  - Guides
  - Tools
  - Workflow
  - Templates
  - Round-Ups
  - Best Practices
---

We spend so much time in our **text editors**, and every now and again we encounter those little frustrating issues that slow us down. Perhaps finding the right file takes too long, or finding a matching closing bracket becomes a long-winded adventure on its own.

Let’s fix all these annoyances for good. In this post, we look into **useful VS Code extensions for front-end development**, from fine productivity boosters to advanced debugging helpers.

### Table of Contents

Below you’ll find quick jumps to specific extensions that you might need. Scroll down for a general overview. Or [skip the table of contents](https://www.smashingmagazine.com/2021/05/useful-vs-code-extensions-web-developers/#automating-log-messages).

<ul class="toc-components">
<li><a href="#automating-log-messages">automate log messages</a></li>
	<li><a href="#keeping-bundle-size-under-control">bundle size</a></li>
	<li><a href="#code-archeology-toolbox">code archeology</a></li>
	<li><a href="#code-formatting-automated">code formatting</a></li>
	<li><a href="#code-screenshots-the-fancy-way">code screenshots</a></li>
	<li><a href="#useful-code-snippets-react-vue-typeScript-jquery">code snippets (React, Vue, TypeScript)</a></li>
	<li><a href="#write-your-own-code-snippets">custom snippets</a></li>
	<li><a href="#human-friendly-comments">comments</a></li>
	<li><a href="#chrome-debugging-inside-vs-code">debugging</a></li>
	<li><a href="#devtools-for-vscode-extension">DevTools</a></li>
	<li><a href="#file-management-utils-for-vs-code">file utils</a></li>
	<li><a href="#adding-tags-to-files-in-your-editor">file tags and labels</a></li>
	<li><a href="#folder-icons-in-vs-code">folder icons</a></li>
	<li><a href="#monospaced-fonts-for-coding">fonts for coding</a></li>
	<li><a href="#git-supercharged">Git</a></li>
	<li><a href="#git-history-in-vs-code">Git history</a></li>
	<li><a href="#highlight-annotations-in-your-code">highlight annotations</a></li>
	<li><a href="#highlighting-matching-brackets-and-tags">highlight brackets and tags</a></li>
	<li><a href="#revealing-harmful-characters">highlight harmful characters</a></li>
	<li><a href="#highlighting-indentation">highlight indents</a></li>
	<li><a href="#visualizing-stacking-contexts">highlight stacking contexts</a></li>
	<li><a href="#custom-colors-to-tell-workspaces-apart">highlight workspaces</a></li>
	<li><a href="#intellisense-ai-assisted-development-features">IntelliCode</a></li>
	<li><a href="#recording-guided-onboarding-for-your-codebase">onboarding</a></li>
	<li><a href="#from-github-to-vs-code-in-one-second">open GitHub fast</a></li>
	<li><a href="#pets-for-your-vs-code">pets</a></li>
	<li><a href="#speed-up-javascript-typescript-prototyping">rapid JS/TS prototyping</a></li>
	<li><a href="#use-a-remote-machine-as-your-dev-environment">remote SSH access</a></li>
	<li><a href="#compile-sass-in-real-time">Sass compilation</a></li>
	<li><a href="#tips-and-tricks-nobody-bothered-to-tell-you">tips and tricks</a></li>
</ul>

## Automating Log Messages

When it comes to log messages, the [turbo-console-log](https://github.com/Chakroun-Anas/turbo-console-log) extension has got your back. It automates the operation of writing meaningful log messages and inserts them automatically.

{{< rimg href="https://github.com/Chakroun-Anas/turbo-console-log" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86117b46-413f-45f6-9844-597aedfaa732/15-useful-vs-code-extensions.png" width="700" height="454" sizes="100vw" caption="Insert meaningful log messages automatically, with <a href='https://github.com/Chakroun-Anas/turbo-console-log'>turbo-console-log</a>." alt="Insert meaningful log messages automatically" >}}

All you need to do is select the variable which you want to debug, press <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>L</kbd>, and the log message will be inserted in the next line. Keyboard shortcuts let you comment, uncomment, or delete all log messages from the current document.

## Keeping Bundle Size Under Control

We all know that performance matters, but in practice, it can be quite a challenge not to lose it out of sight when you’re in the flow of writing code. To keep your bundle size under control, the [Import Cost](https://github.com/wix/import-cost) extension lets you immediately know if you’re importing a hefty package into your project.

{{< rimg href="https://github.com/wix/import-cost" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b80c0489-6d8b-40cc-a93c-d0ce4591110a/12-useful-vs-code-extensions.png" width="800" height="136" sizes="100vw" caption="Keep your bundle size under control, with <a href='https://github.com/wix/import-cost'>import-cost</a>." alt="Keep your bundle size under control" >}}

Import Cost isn’t a bundle analysis tool but was built with the idea to help you find possible **performance bottlenecks** before you ship them to your users. To do so, it gives you instant feedback by displaying the size of an imported third-party library as you’re importing it, right next to your line of code. A handy little helper.

## Code Formatting, Automated

When writing code, a lot of time goes into formatting. [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) automates the task for you. It removes all original styling and ensures that the outputted code conforms to a consistent style.

{{< rimg href="https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83e743ec-2b55-40e6-b1cc-2bcf32314391/13-useful-vs-code-extensions.png" width="800" height="316" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode'>Prettier</a>, a quite opinionated (but friendly) code formatter that formats code as you press Save." alt="An opinionated code formatter that formats code as you press ‘save’" >}}

Prettier parses your code and **re-formats it with its own rules**, taking the maximum line length into account and wrapping the code when necessary. You decide if you want to apply it to all languages or alternatively you can define the ones you prefer to format manually. Also a great solution for teams who struggle finding a common style guide.

## Useful Code Snippets (React, Vue, TypeScript, jQuery)

Are you tired of typing the **snippets** you frequently need over and over again, always from scratch? Here are some handy little helpers to ease the job. For Vue, be sure to check out Sarah Drasner’s [Vue.js VS Code Snippets extension](https://marketplace.visualstudio.com/items?itemName=sdras.vue-vscode-snippets). It was built for real-world use and focuses on developer ergonomics instead of cataloguing API definitions.

Burke Holland provides you with a collection of [essential React snippets and commands](https://marketplace.visualstudio.com/items?itemName=burkeholland.simple-react-snippets) that he selected from his day-to-day React use. And if you’re looking for Angular snippets, John Papa has got you covered. His extension adds [snippets for Angular for TypeScript and HTML](https://github.com/johnpapa/vscode-angular-snippets) to your VS Code setup.

{{< rimg href="https://marketplace.visualstudio.com/items?itemName=sdras.vue-vscode-snippets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ff02aef-a105-4121-91cc-af9d03cf28da/vs-code-snippets.png" width="800" height="316" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=sdras.vue-vscode-snippets'>Vue.js VSCode Snippets</a>, by Sarah Drasner, a goldmine of Vue.js code snippets." alt="Vue.js VSCode Snippets" >}}

These two might also come in handy: The [JavaScript code snippets extension](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets) by Charalampos Karypidis contains snippets in ES6 syntax and supports both JavaScript and TypeScript. And, last but not least, Don Jayamanne’s [jQuery code snippets](https://marketplace.visualstudio.com/items?itemName=donjayamanne.jquerysnippets) feature over 130 jQuery snippets. Once installed, just type `jq` to get a list of all of them.

Speaking of snippets: If you prefer a **good snippets library** over defining them yourself from scratch, these collections have got your back:

- [Accessibility Snippets](https://github.com/intuit/accessibility-snippets)
- [ES7 React/Redux/GraphQL/React-Native](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
- [CSS](https://marketplace.visualstudio.com/items?itemName=joy-yu.css-snippets)
- [CSS Grid](https://marketplace.visualstudio.com/items?itemName=ohansemmanuel.css-grid-snippets)
- [HTML](https://marketplace.visualstudio.com/items?itemName=abusaidm.html-snippets)
- [Node.js](https://marketplace.visualstudio.com/items?itemName=chris-noring.node-snippets)
- [JavaScript (ES6)](https://marketplace.visualstudio.com/items?itemName=jmsv.JavaScriptSnippetsStandard)
- [Angular 10](https://marketplace.visualstudio.com/items?itemName=Mikael.Angular-BeastCode)
- [Vue.js + TypeScript](https://marketplace.visualstudio.com/items?itemName=LissetteIbnz.vscode-vue-typescript-sfc-snippets)
- [WordPress](https://marketplace.visualstudio.com/items?itemName=wordpresstoolbox.wordpress-toolbox)
- [WordPress Gutenberg](https://marketplace.visualstudio.com/items?itemName=BenjaminZekavica.wordpress-gutenberg-snippets)
- [PHP](https://marketplace.visualstudio.com/items?itemName=hakcorp.php-awesome-snippets)
- [PHP Tools](https://marketplace.visualstudio.com/items?itemName=DEVSENSE.phptools-vscode)
- [Svelte](https://marketplace.visualstudio.com/items?itemName=fivethree.vscode-svelte-snippets)
- [TensorFlow](https://marketplace.visualstudio.com/items?itemName=vahidk.tensorflow-snippets)


## Write Your Own Code Snippets

There are a lot of code snippet plugins for different languages out there, but have you ever wondered how to define **your own snippets** in VS Code? Maurice Borgmeier summarized [everything you need to know](https://mauricebrg.com/article/2020/12/make_your_own_custom_code_snippets_in_visual_studio_code.html) to get started.

{{< rimg href="https://www.freecodecamp.org/news/definitive-guide-to-snippets-visual-studio-code/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/453a9c10-1f13-4d76-9937-3521382370a5/custom-snippets-opt.png" width="800" height="316" sizes="100vw" caption="Everything you need to know about <a href='https://www.freecodecamp.org/news/definitive-guide-to-snippets-visual-studio-code/'>code snippets in VS Code</a>, a thorough guide by Rob O’Leary." alt="VS Code Code Snippets" >}}

Another [great article](https://www.freecodecamp.org/news/definitive-guide-to-snippets-visual-studio-code/) on the topic comes from Rob O’Leary. He dives deeper into when and why to use snippets, takes a closer look at different types of snippets, how VS Code handles them, and, last but not least, how to write your own, of course.


## Code Screenshots, The Fancy Way

Let’s be honest, taking good-looking screenshots of code can be a challenge. [Polacode](https://marketplace.visualstudio.com/items?itemName=pnp.polacode) is here to change that.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=pnp.polacode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/842b0f9b-f49e-4d10-9269-cc2ef34ea2ad/polacode.png" width="700" height="300" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=pnp.polacode'>Polacode</a> lets you take and edit screenshots of your code directly in VS Code" alt="Polaroid for your code" >}}

Described as "Polaroid for your code", Polacode lets you **take and edit screenshots** of your code directly in VS Code. You can resize the code’s container by dragging the corner and use commands to control the image appearance. A great solution to make the code you’ve spent so many hours on shine in the best light &mdash; in blog posts or presentations, for example.

## Human-Friendly Comments

How do you handle comments? If your code requires a lot of explanations, it might be a good idea to make those usually grayed-out **comments** more human-friendly, so that it’s easier to see at a glance if a comment alerts you of a deprecated method, for example, or if it’s a todo your teammate left for you.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1c1941-2e52-4ed6-a192-8bfcf743d31a/6-useful-vs-code-extensions.png" width="800" height="478" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments'>Better Comments</a> helps you categorize annotations into alerts, queries and todos." alt="Improve your code commenting" >}}

The VS Code extension [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments) helps you do just that, categorizing annotations into alerts, queries, todos, highlights, and more. Commented-out code can also be styled to make it clear it shouldn’t be there.

{{% feature-panel %}}

## Chrome Debugging Inside VS Code

Do you use Chrome and find yourself switching back and forth between the browser and your editor when debugging? Then you might want to give the [VS Code Chrome debugger](https://code.visualstudio.com/blogs/2016/02/23/introducing-chrome-debugger-for-vs-code) a try. It helps you debug client-side JavaScript code that runs in Chrome directly from VS Code.

{{< rimg href="https://code.visualstudio.com/blogs/2016/02/23/introducing-chrome-debugger-for-vs-codes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d2443a6-a085-4749-a7bc-a8621949eae0/14-useful-vs-code-extensions.png" width="700" height="436" sizes="100vw" caption="Debug Chrome without leaving the editor, with <a href='https://code.visualstudio.com/blogs/2016/02/23/introducing-chrome-debugger-for-vs-codes'>Chrome Debugger for VS Code</a>." alt="Debug Chrome without leaving the editor" >}}

The debugger connects to Chrome over its Chrome Debugger protocol where it maps files loaded in the browser to the files you have open in VS Code. So without leaving the editor, you can **set breakpoints in your source code**, set up variables to watch, and see the full call stack when debugging. A little tool to make your debugging routine more straightforward.

## DevTools For VSCode Extension

Wouldn’t it be cool to have DevTools integrated into your code editor so that you don’t need to switch back and forth between the two? If you’re using VSCode and Edge, a small extension makes it possible.

{{< rimg breakout="true" href="https://github.com/microsoft/vscode-edge-devtools" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507cc8bc-2a9d-48ad-991c-496360e58164/4-useful-vs-code-extensions.png" width="700" height="395" sizes="100vw" caption="<a href='https://github.com/microsoft/vscode-edge-devtools'>DevTools inside VS Code</a>: Microsoft Edge Developer Tools for Visual Studio Code." alt="Microsoft Edge Developer Tools for Visual Studio Code" >}}

The [extension](https://github.com/microsoft/vscode-edge-devtools) shows the browser’s Elements and Network tool inside VSCode, giving you the ability to see the runtime HTML structure, alter styling and layout, **perform diagnostics**, and debug your project &mdash; without leaving the editor. By the way, Rachel Weil shared some handy DevTools tips for working with Chromium-based browsers like Edge and Chrome at SmashingConf San Francisco a few weeks ago. Be sure to tune into the [recording](https://vimeo.com/488915874) to take your DevTools skills to the next level.

## File Management Utils for VS Code

A lot of time is usually spent on organizing and managing files. [File Utils](https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils) makes the task more convenient.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449abb1e-9c38-4d4d-b8cf-5f2ebfc9e92f/file-utils.png" width="700" height="235" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils'>File Utils</a>, an extension that enables you to create, duplicate, move, rename, and delete files and directories." alt="File Utils, Extension enables you to create, duplicate, move, rename, and delete files and directories" >}}

The extension enables you to **create, duplicate, move, rename**, and delete files and directories with just a handful of commands. It also supports brace extension which automatically generates arbitrary strings strings to set up your document structure.

## Adding Tags To Files In Your Editor

In large projects, finding one specific variant of a component, or just the right file requires you to know the file that you are actually looking for. But what if you could **add bookmarks or labels** to specific files, so you could find them faster?

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=mehullakhanpal.file-ops" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bb0e6cc-1680-47e2-8739-d7388264db2d/2-useful-vs-code-extensions.png" width="700" height="546" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=mehullakhanpal.file-ops'>File Ops</a> allows you to add tags to files in your VS Code." alt="Adding Tags to Files In Your Editor" >}}

[File Ops VS Code Extension](https://marketplace.visualstudio.com/items?itemName=mehullakhanpal.file-ops) allows you to **tag and alias files**, and then quickly switch between them. You can also quickly list all tags just in case you lose track of them, view all files from the current directory and switch between .css and .js files in the same folder. You can also take a look at the [video](https://www.youtube.com/watch?v=ze9KtYe3f48) explaining how it all works. Now that will come in handy! 

## Folder Icons In VS Code

**Custom file and folder icons** in VS Code? Yes, please! To help you maneuver your workspace more easily, even if a lot of files and folder are involved, the VS Code Icons Team released an [extension that brings icons to your editor](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons). From “access” to “zip”, “Android” to “www”, the collection is sure to have the file and folder icons you need.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08c75003-7455-425e-9b54-701664d3bd38/12-vs.png" width="700" height="378" sizes="100vw" caption="You can adjust icons for VS Code files and folders to make them a bit more distinguishable. With <a href='https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons'>VSCode Icons</a>." alt="Icons for your VS Code files and folders" >}}

The project-specific icons toggle feature and project auto-detection will **automatically detect** the type of project you have opened in your workspace and prompt you to toggle the icons accordingly. It’s also possible to use custom icons, if you prefer.

{{% ad-panel-leaderboard %}}

## Monospaced Fonts For Coding

Programming fonts are certainly the workhorses in typography. They need to offer great readability, enable quick text scanning, and prevent eye strain even when a developer looks at the code for hours. To help you find a **programming font** that meets your needs, Chris Coyier curates [*Coding Fonts*](https://coding-fonts.css-tricks.com/), a selection of more than 30 (mostly free) monospaced fonts that all match this criteria.

{{< rimg breakout="true" href="https://coding-fonts.css-tricks.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2591991-4bb6-4c32-b78d-1d020aa4a524/5-useful-vs-code-extensions.png" width="700" height="456" sizes="100vw" caption="<a href='https://coding-fonts.css-tricks.com/'>Monospace Coding Fonts</a> for your pleasant coding experience." alt="Monospace Coding Fonts" >}}

To make the decision easier, each font comes with a short description, an overview of all characters, and HTML, CSS, and JavaScript code examples in both day and night mode. Mostafa Gaafar maintains a similar [list of fonts for developers](https://devfonts.gafi.dev/) with the option to also view the code examples in different color schemes. To add custom fonts to VS Code, you’ll need to [define the font in “Settings”](https://dev.to/solexy79/installing-a-new-font-for-vs-code-in-three-3-simple-steps-13a5).

## Git Supercharged

A useful extension to supercharge the Git capabilities built into VS Code is [GitLens](https://github.com/eamodio/vscode-gitlens). To better understand the code you’re working on, GitLens lets you glimpse into whom, why, and when a line or code block was changed.

{{< rimg breakout="true" href="https://github.com/eamodio/vscode-gitlens" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d84c863-d40f-4055-8730-86a689d3c935/11-useful-vs-code-extensions.png" width="800" height="423" sizes="100vw" caption="Seamlessly navigate and explore Git repositories in VS Code with <a href='https://github.com/eamodio/vscode-gitlens'>GitLens</a>." alt="Seamlessly navigate and explore Git repositories in VS Code" >}}

The extension **visualizes code authorships** at a glance, helps you seamlessly navigate and explore Git repositories, gain valuable insights via comparison commands, and more. Everything you need to know about your codebase right at your fingertips, without leaving the editor.

## Git History In VS Code

Viewing and searching git log along with the graph and details, viewing a previous copy of the file you’re working on, **searching the history**, comparing branches and commits &mdash; these are just a few of the features that the [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory) extension offers to streamline your workflow.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ae03994-3294-4c07-b0dd-9b307aa1d1dc/git-graph-opt.png" width="700" height="395" sizes="100vw" caption="Comfortably navigate back in the future with <a href='https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory'>Git History</a>." alt="Take full advantage of Git’s powers right in your editor" >}}

Speaking of Git: Another VS Code extension worth taking a closer look at when working with Git is [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph): It lets you view a Git graph of your repository and easily perform Git actions from the graph.

## Code Archeology Toolbox

It can be hard to read a block of code and immediately understand its code context. Why did one of your teammates write it in such a way? [Watermelon](https://www.watermelontools.com/) is here to help.

{{< rimg breakout="true" href="https://www.watermelontools.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22dc012f-5cb8-4a0c-88a8-589b0a68a11b/watermelon-opt.png" width="800" height="437" sizes="100vw" caption="<a href='https://www.watermelontools.com/'>Watermelon</a> points you to the most relevant part of your project’s GitHub history." alt="Watermelon" >}}

The VSCode extension indexes the most relevant pieces of information from GitHub and Jira for a given block of code, to help you understand and debug code faster by being pointed to the most relevant part of passive documentation. A powerful helper that can save you lots of hours trying to figure out what happens in a codebase.

## Highlight Annotations In Your Code

Do you sometimes forget to review the to-dos you’ve added while coding? The [TODO Highlight](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) extension reminds you that there are notes or things that need your attention before you publish to production.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bebcbc-fb2e-4390-80dc-2a669a590ada/todo-highlight-opt.png" width="800" height="516" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight'>TODO Highlight</a> allows you to get reminded of to-dos before publishing to production." alt="Get reminded of to-dos before you publish to production" >}}

The keywords `TODO` and `FIXME` are preconfigured, but you can **customize the configuration** to your liking if you prefer. A command highlights the open comments for you right in your code or as a list of all annotations. A great little reminder.

## Highlighting Matching Brackets And Tags

An intense coding session strains the eyes, so anything that helps cater for more visual clarity is a welcome helper. To take your syntax highlighting to the next level when working with VS Code, you might want to check out the [Bracket Pair Colorizer](https://github.com/CoenraadS/Bracket-Pair-Colorizer-2). The extension identifies matching brackets &mdash; in colors you define.

{{< rimg href="https://github.com/CoenraadS/Bracket-Pair-Colorizer-2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7239a1ca-5139-4fb8-979a-53cd485db8e9/8-useful-vs-code-extensions.png" width="800" height="439" sizes="100vw" caption="Easily highlight matching tags wih <a href='https://github.com/CoenraadS/Bracket-Pair-Colorizer-2'>Bracket Pair Colorizer</a>. A real time-saver." alt="Highlight matching tags" >}}

Now that you’ve got full control over your brackets, another little detail to watch out for are matching opening and closing tags. VS Code does already come with a [tag matching feature](https://twitter.com/jaredpalmer/status/1385938591323414529?s=21), but it is rather basic. The [Highlight Matching Tag](https://github.com/vincaslt/vscode-highlight-matching-tag) extension does the work more thoroughly, **matching tags anywhere** &mdash; from tag attributes to inside strings &mdash; and even highlighting the path from tag to tag in the status bar. Extensive styling options let you customize how tags are highlighted. HTML and JSX are officially supported.

## Revealing Harmful Characters

Zero-width spaces and non-joiners, non-breaking spaces, left and right double quotation marks &mdash; when coding, some characters can be harmful because they are invisible or looking like legitimate ones. [Gremlins Tracker](https://marketplace.visualstudio.com/items?itemName=nhoizey.gremlins) finds them for you.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=nhoizey.gremlins" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fcaf01d-01b2-4fa5-aef2-a1be750b381e/18-useful-vs-code-extensions.png" width="700" height="418" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=nhoizey.gremlins'>Gremlins Tracker</a> tracks zero-width spaces, non-joiners and all the wird characters." alt="Gremlins Tracker reveals characters that could be harmful" >}}

Gremlins Tracker uses a color scheme to alert you of harmful, potentially harmful, and less **harmful characters**. Lines that include such a character are marked with a Gremlins icon, and moving the cursor over the character gives you a hint of the potential issue. If you like, you can add new gremlins characters or override them for a specific language.

## Highlighting Indentation

Indentation is key to ensure your code can be scanned quickly. A handy little plugin that makes indentations even more readable is [Indent-Rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow). It **colorizes the indentation** in front of your text alternating four different colors on each step and marking those lines where the indentation is not a multiple of the tab size.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb96c0dd-7635-45d1-8956-51cc90ae3369/9-useful-vs-code-extensions.png" width="800" height="478" sizes="100vw" caption="Make indentation a bit more readable with <a href='https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow'>Indent-Rainbow</a>." alt="Make indentation more readable" >}}

While error highlighting is useful, there are instances where it might get in your way. When dealing with RegEx patterns, for example. Luckily, Indent-Rainbow lets you turn off error highlighting on those, just like on comment lines, and, if you like, you can even skip it for entire languages.

## Visualizing Stacking Contexts

Do you have difficulties spotting **stacking contexts** when using `z-index`? You’re not alone! If you sometimes find yourself setting a `z-index` to a billion on an element and it’s not moving forward in your stacking order, [CSS Stacking Contexts](https://marketplace.visualstudio.com/items?itemName=felixfbecker.css-stacking-contexts) is for you.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=felixfbecker.css-stacking-contexts" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3345bd1e-3597-4026-88fd-85167adddddc/16-useful-vs-code-extensions.png" width="800" height="409" sizes="100vw" caption="Visualize CSS stacking contexts without the hassle, with <a href='https://marketplace.visualstudio.com/items?itemName=felixfbecker.css-stacking-contexts'>CSS Stacking Contexts</a>." alt="Stacking contexts without the hassle" >}}

The extension makes stacking contexts visible in CSS and SCSS so that you can confidently use small values when writing `z-index` declarations. Additionally, it will also tell you when a `z-index` declaration has no effect and offer quick fixes.

## Custom Colors To Tell Workspaces Apart

If you frequently have multiple VS Code instances open and struggle to tell them apart, [Peacock](https://marketplace.visualstudio.com/items?itemName=johnpapa.vscode-peacock) might be worth taking a closer look at: the extension subtly changes the **color theme of your workspace**.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=johnpapa.vscode-peacock" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c5dbb73-94e1-486f-9daa-351699faaa2d/peacock-extension.png" width="800" height="441" sizes="100vw" caption="Subtly change the color of your workspace to distinguish between them in VS Code, with <a href='https://marketplace.visualstudio.com/items?itemName=johnpapa.vscode-peacock'>Peacock</a>." alt="Subtly change the color of your workspace" >}}

But it’s not only when working on multiple projects at once where Peacock shines. It also comes in handy when using VS Live Share or VS Code’s Remote features and you quickly want to identify your editor.

## IntelliSense: AI-Assisted Development Features

The [IntelliCode](https://visualstudio.microsoft.com/services/intellicode/) extension provides AI-assisted development features for Python, TypeScript/JavaScript and Java developers in Visual Studio Code, with insights based on understanding your code context combined with **machine learning**.

{{< rimg href="https://visualstudio.microsoft.com/services/intellicode/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d61c23d1-ba5a-4d59-adaa-0c45635c873d/intellisense-extention.png" width="700" height="308" sizes="100vw" caption="Why not enhance your development with a sparkle of AI? <a href='https://visualstudio.microsoft.com/services/intellicode/'>IntelliCode</a> is here to help." alt="Enhance your development workflow with AI" >}}

Providing AI-assisted IntelliSense, the extension shows you **recommended auto-completion items** for your code context at the top of the completions list. When it comes to overloads, it doesn’t cycle through the alphabetical list of member but presents you the most relevant one first. No more hunting through the list yourself.

## Recording Guided Onboarding For Your Codebase

A large codebase can feel intimidating. [CodeTour](https://github.com/microsoft/codetour) attempts to change that. The extension allows you to **record and play back guided walkthroughs** of your codebases, directly within the editor. Think of it as a table of contents that makes it easier to onboard or re-board to new project or feature area, to visualize bug reports, or understand the context of a code review.

{{< rimg breakout="true" href="https://github.com/microsoft/codetour" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95981981-1d77-48fe-bdfd-a026696a0941/7-useful-vs-code-extensions.png" width="800" height="509" sizes="100vw" caption="Onboarding, the easy way: to record and play back guided tours of your codebase. That's <a href='https://github.com/microsoft/codetour'>Codetour</a>." alt="Record and play back guided tours of your codebases" >}}

To create a code tour, you can annotate lines of code (Markdown is supported) and navigate as many files as you need, and the recorder captures the sequence. The tours can be checked into a repo or exported to a “tour” file so that anyone can replay it without having to clone any code. Handy!

## From GitHub To VS Code, In One Second

Once you’ve discovered a snippet of code on GitHub, what if you want to start working with it in your project immediately? Instead of cloning the repo and finding that file that you need, you can use [Github1s](https://github1s.com/). Just add `1s` after `github` in the URL, press Enter, and the repo, or a single file, will **open straight in VS Code**.

{{< rimg breakout="true" href="https://github1s.com/s" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab355b6b-7325-4504-adb4-66f5ee15a3c3/1-useful-vs-code-extensions.png" width="700" height="408" sizes="100vw" caption="From GitHub to VS Code, in one second. That's <a href='https://github1s.com/s'>Github1s</a>." alt="From GitHub To VS Code, In One Second" >}}

You can also use a bookmarklet to quickly switch between *github.com* and *github1s.com*, access private repositories and there are plenty of browser extensions that are listed on the [project page](https://github1s.com/) as well. If you need an alternative, [Gitpod](https://www.gitpod.io/) is a slightly more advanced option, which also allows you to start an online development environment, run parallel workspaces and work on the codebase collaboratively.

## Pets For Your VS Code

Ever wanted to pep up your VS code editor? Well, how about adding a cat, dog, snake, rubber duck or even good ol’ Clippy? All you need to do is [install vscode-pets](https://marketplace.visualstudio.com/items?itemName=tonybaloney.vscode-pets) and run the `vscode-pets.start` command in order to see the panel. Once you’ve chosen a pet, its fur color and size, lean back and watch them interact with you!

{{< rimg href="https://marketplace.visualstudio.com/items?itemName=tonybaloney.vscode-pets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f751e0d-6b03-43f1-8cee-8cf07f2281e2/3-useful-vs-code-extensions.png" width="700" height="400" sizes="100vw" caption="Ever wanted to pep up your VS code editor? Or play catch in VS Code? You can do just that with <a href='https://marketplace.visualstudio.com/items?itemName=tonybaloney.vscode-pets'>VS Code Pets</a>." alt="Pets For Your VS Code" >}}

From **throwing a ball and playing catch** with your pet (run `vscode-pets.throw-ball`) to adding additional pets (run `vscode-pets.spawn-pet`), you’re coding workflow is bound to be anything but boring! The creator, [Anthony Shaw](https://twitter.com/anthonypjshaw), is open for [ideas and discussion](https://github.com/tonybaloney/vscode-pets/issues) and welcomes feedback anytime.

{{% ad-panel-leaderboard %}}

## Speed Up JavaScript / TypeScript Prototyping

If you’re looking for a way to speed up your JavaScript prototyping process, [Quokka](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode) is for you. The rapid prototyping playground lives in your editor and gives prototyping, learning, and testing JavaScript and TypeScript a speed boost.

{{< rimg breakout="true" href="https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4fc1fbc-826b-4cb7-aaa5-f14de0409a34/quokka-opt.png" width="700" height="438" sizes="100vw" caption="<a href='https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode'>Quokka</a>, a helpful little tool for rapid prototyping in JavaScript and TypeScript." alt="Quokka introduces a rapid prototyping playground in your VS Code setup" >}}

Runtime values are updated and displayed in your IDE next to your code, as you type. To get you up and running right away, there’s **no config required**, all you need to do to start experimenting is opening a new Quokka file. Happy prototyping!

## Use A Remote Machine As Your Dev Environment

There’s a variety of reasons why you might want to use a remote machine with an SSH server as a development environment. Because you need faster or more specialized hardware than your local machine, for example, or to **debug an application running somewhere else**, such as a customer site or an application in the cloud. To simplify development and troubleshooting, the [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) extension helps you do just that.

The extension runs commands and other extensions directly on the **remote machine**, so you won’t need any source code on your machine. Instead, you can open any folder on the remote machine and work with it just as you normally would, taking full advantage of VS Code’s full feature set. Handy!

## Compile Sass In Real Time

A real-time Sass compiler with live browser reload? [Live Sass extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass) has got you covered. It helps you compile/transpile your SASS/SCSS files to CSS files in real time.

Features include **customizing the file location** of the exported CSS as well as its style and extension name, there’s a quick status bar control, you can exclude specific folders in the settings, and autoprefix is supported, too.

## Tips And Tricks Nobody Bothered To Tell You

Are you really making full use of the powerful features VS Code has to offer? Burke Holland and Sarah Drasner claim you don’t, so to change that, they [share all the best things about VS Code that nobody ever bothered to tell you](https://www.vscodecandothat.com/).

{{< rimg breakout="true" href="https://www.vscodecandothat.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1c1941-2e52-4ed6-a192-8bfcf743d31a/6-useful-vs-code-extensions.png" width="800" height="478" sizes="100vw" caption="<a href='https://www.vscodecandothat.com/'>VS Can Do That?</a> Tips and tricks that help you make full use of the powerful features that VS Code has to offer." alt="Tips and tricks that help you make full use of the powerful features that VS Code has to offer." >}}

From automatically updating HTML `img` tags with the correct size of the image to using font ligatures for better readability when coding or log points to log information out from your application, “VS Code Can Do That?!” features **36 valuable tips** that’ll make your workflow even more efficient.

## Wrapping Up

There are *literally* hundreds of VS Code extensions out there, and we hope that some of the ones listed here will prove to be useful in your day-to-day work &mdash; and most importantly help you avoid some time-consuming, routine tasks. Happy coding, everyone!

### Further Reading

- [CSS Auditing Tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/)
- [CSS Generators](https://www.smashingmagazine.com/2021/03/css-generators/)
- [SVG Generators](https://www.smashingmagazine.com/2021/03/svg-generators/)
- [HTML Email Tools and Templates](https://www.smashingmagazine.com/2021/04/complete-guide-html-email-templates-tools/)
- [Vanilla JavaScript Code Snippets](https://www.smashingmagazine.com/2021/04/vanilla-javascript-code-snippets/)
- [Accessible Front-End Components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/)
- Also, [subscribe to our newsletter](https://www.smashingmagazine.com/the-smashing-newsletter/) to not miss the next ones.

{{< signature "vf, il" >}}
