---
title: 'Useful Front-End Boilerplates And Starter Kits'
slug: useful-frontend-boilerplates-starter-kits
author: cosima-mielke
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/598e7f3e-9dca-4922-b17d-76089efab46f/25-frontend-boilerplates-starter-kits.png
date: 2021-06-10T15:00:00.000Z
description: >-
  We don’t need to write everything from scratch every single time. With boilerplates and starter kits, we can set up our projects faster, and get to work immediately.
summary: >-
  We don’t need to write everything from scratch every single time. With boilerplates and starter kits, we can set up our projects faster, and get to work immediately. We’ve also just recently covered [CSS auditing tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/), [CSS generators](https://www.smashingmagazine.com/2021/03/css-generators/), [accessible front-end components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/) and [VS code extensions](https://www.smashingmagazine.com/2021/05/useful-vs-code-extensions-web-developers/) &mdash; you might find them useful, too.
categories:
  - Guides
  - Tools
  - Workflow
  - Templates
  - Round-Ups
  - Best Practices
last_updated: 2021-07-28T13:30:00.000Z
---

Today, we’re shining the spotlight on **boilerplates and starter kits** for all kinds of projects, from static site templates and React/Vue starter kits to favicon and accessibility templates and emergency site templates. This collection is by no means complete, but rather a selection of things that the team at Smashing found useful and hope will make your day-to-day work more productive and efficient.

If you’re interested in more tools like these ones, please do [take a look at our lovely email newsletter](https://www.smashingmagazine.com/the-smashing-newsletter), so you can get tips like these drop right into your inbox!

### Table of Contents

Below you’ll find quick jumps to specific boilerplates and guides you may need. Scroll down for a general overview or [skip the table of contents](#accessibility).

<ul class="toc-components">
  <li><a href="#accessibility-boilerplate">accessibility</a></li>
  <li><a href="#asp-net-boilerplate">ASP.NET</a></li>
  <li><a href="#browser-extensions-boilerplate">browser extensions</a></li>
  <li><a href="#modern-cross-browser-extensions-boilerplate">cross-browser extensions</a></li>
  <li><a href="#modern-css-resets-and-their-alternatives">CSS resets</a></li>
  <li><a href="#css-boilerplates-and-snippets">CSS snippets</a></li>
  <li><a href="#color-themes-for-your-dev-environment">dev environment themes</a></li>
  <li><a href="#bootstrap-your-dotfiles">dotfiles</a></li>
  <li><a href="#electron-boilerplate">Electron</a></li>
  <li><a href="#emergency-site-kit">emergency site</a></li>
  <li><a href="#how-to-favicon-in-2021">favicon</a></li>
  <li><a href="#a-boilerplate-for-forms">forms</a></li>
  <li><a href="#all-in-one-front-end-boilerplates">full front-end stack</a></li>
  <li><a href="#github-template-guidelines">GitHub template</a></li>
  <li><a href="#create-gitignore-files-for-your-git-repositories">gitignore</a></li>
  <li><a href="#hackathon-starter">hackathon template</a></li>
  <li><a href="#html-boilerplate-explained">HTML boilerplate</a></li>
  <li><a href="#mobile-first-boilerplates">mobile first</a></li>
  <li><a href="#html5-boilerplate">HTML5 boilerplate</a></li>
  <li><a href="#boilerplates-for-responsive-html-emails">HTML emails</a></li>
  <li><a href="#a-complete-guide-to-html-code-lt-head-gt-code">HTML <code>&lt;head&gt;</code></a></li>
  <li><a href="#php-boilerplates">PHP</a></li>
  <li><a href="#create-projects-from-cookiecutters">project setup</a></li>
  <li><a href="#quick-snippets">quick snippets</a></li>
  <li><a href="#react-boilerplates">React</a></li>
  <li><a href="#a-snippet-for-loading-responsive-webp-images">responsive images</a></li>
  <li><a href="#saas-boilerplate">SaaS</a></li>
  <li><a href="#static-site-boilerplate">static site</a></li>
  <li><a href="#style-guide-boilerplates">style guide</a></li>
  <li><a href="#typographic-starter-kit">typography starter kit</a></li>
  <li><a href="#vs-code-snippets-to-streamline-your-workflow">VS Code snippets</a></li>
  <li><a href="#vue-boilerplates">Vue.js</a></li>
  <li><a href="#wordpress-plugin-boilerplate-generator">WordPress plugins</a></li>
  <li><a href="#wordpress-starter-theme">WordPress starter</a></li>
</ul>

## Accessibility Boilerplate

To prevent accessibility from becoming an afterthought, it is a good idea to already lay the foundation when beginning a web project. So if you’re looking for a boilerplate solution to kickstart your project responsibly, the [Accessibility Boilerplate](https://github.com/jbmoelker/a11y-boilerplate) is for you.

{{< rimg href="https://github.com/jbmoelker/a11y-boilerplate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c78092d4-4c33-4d97-a46a-98cc0dc8253e/1-frontend-boilerplates-starter-kits.png" width="700" height="454" sizes="100vw" caption="A sensible default template that is easily accessible by search engines and assistive technologies." alt="A sensible default template that is easily accessible by search engines and assistive technologies" >}}

The template uses plain old semantic markup to correctly structure your content, making it easily accessible by search engines and assistive technologies. The HTML5 syntax is further enhanced with ARIA roles and Microdata. An oldie but goodie.

In case you need a little bit of help with WAI-ARIA, this [collection of accessible snippets](https://atom.io/packages/accessible-snippets) will sure come in handy. The snippets include all WAI-ARIA attributes and descriptions to help make your content more accessible. To help you resolve existing accessibility errors, Jacob Lett put together a [collection of snippets](https://bootstrapcreative.com/web-accessibility-evaluation-tool-code-snippets/) for reducing redundant title text, dealing with empty links used for JavaScript behavior, and bringing meaning to visual elements like icons.

## ASP.NET Boilerplate

The [ASP.NET Boilerplate](https://aspnetboilerplate.com/) uses familiar tools to provide you with a solid developer experience when building modern web applications. Based on domain-driven design, it provides a strong infrastructure and development model for modularity, multi-tenancy, caching, background jobs, data filters, setting management, domain events, unit and integration testing, and everything else you’ll need to have more time to focus on your business code. Startup templates help you get started &mdash; either with an Angular single-page application or classic MVC & jQuery architecture.

{{< rimg href="https://aspnetboilerplate.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1b50e28-90cf-4585-b8be-fc7c3573b1ab/2-frontend-boilerplates-starter-kits.png" width="800" height="460" sizes="100vw" caption="The <a href='https://aspnetboilerplate.com/'>ASP.NET Boilerplate</a> automates common software development tasks by convention." alt="The ASP.NET Boilerplate automates common software development tasks by convention." >}}

Another fully-fledged boilerplate is the [ASP.NET Core Hero Boilerplate](https://codewithmukesh.com/project/aspnet-core-hero-boilerplate/). It enables you to run a single line of CLI on your Console to get a complete implementation. The template includes both WebAPI and MVC. A perfect starting point to learn about various essential packages and architecture.

## Browser Extensions Boilerplate

Do you plan to build a browser extension? The [Browser Extension Webpack Boilerplate](https://github.com/fstanis/webextensions-webpack-boilerplate) has got your back. Designed for creating WebExtensions API-based browser extensions using Webpack, the extensions are, in theory, compatible with Chrome, Chromium, Firefox, Firefox for Android, Opera, and Microsoft Edge. Actual compatibility will depend on the APIs you used.

## Modern Cross-Browser Extensions Boilerplate

Things that seem trivial in the web development world can turn out to be surprisingly hard in a web extension context. Especially when it comes to cross-browser extensions. To give you the experience you know from building cross-browser web apps when developing cross-browser web extensions, Cezar Augusto built [`extension-create`](https://github.com/cezaraugusto/extension-create).

{{< rimg href="https://github.com/cezaraugusto/extension-create" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07d98ed-6836-41f5-a6ff-5009121a7b60/3-frontend-boilerplates-starter-kits.png" width="800" height="559" sizes="100vw" caption="Create cross-browser extensions with no build configuration. (<a href=''>Large preview</a>)" alt="Create Cross-Browser Extensions with no build configuration" >}}

`extension-create` helps you develop cross-browser extensions with built-in support for module import/exports, auto-reload, and more. There’s no build configuration necessary: To create an extension, a new browser instance (for now, Chrome) will open up, and you’re ready to dive right in. Each command and major feature works as a standalone module which is particularly useful if you have your extension setup but want to benefit from specific features, such as the browser launcher with default auto-reload.

## Modern CSS Resets And Their Alternatives

With CSS browser compatibility issues being much less likely today, CSS resets have mostly become redundant. However, there are instances when a modern CSS reset might still make sense. Box sizing, body styles, links, fluid image styles, fonts, and a `@media` query for reduced motion, these are things you might want to reset, [as Andy Bell shows](https://piccalil.li/blog/a-modern-css-reset). A modern reset of sensible defaults, so to say.

{{< rimg href="https://necolas.github.io/normalize.css/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a8e4374-a465-4ec4-917f-89c285dd72cb/4-frontend-boilerplates-starter-kits.png" width="700" height="394" sizes="100vw" caption="Unlike many CSS resets, <a href='https://necolas.github.io/normalize.css/'>Normalize.css</a> preserves useful defaults. (<a href=''>Large preview</a>)" alt="Normalize.css" >}}

Another modern alternative to CSS resets is [Normalize.css](https://necolas.github.io/normalize.css/). It normalizes styles for a wide range of elements, corrects bugs and browser inconsistencies, improves usability with subtle modifications, and it uses detailed comments to explain what code does.

## CSS Boilerplates And Snippets

Are you embarking on a smaller project or do you feel that a larger framework is overkill for your needs? [Barebones](https://acahir.github.io/Barebones/) only styles a handful of standard HTML elements and CSS Grid, and, as it turns out, that’s often more than enough to get started. With its approximately 400 lines, the boilerplate is light as a feather, and there’s no compiling or installing necessary to get you started.

{{< rimg href="https://acahir.github.io/Barebones/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcf7f136-478e-4621-b2b9-e40d4a348366/5-frontend-boilerplates-starter-kits.png" width="800" height="456" sizes="100vw" caption="Thanks to CSS Variables, <a href='https://acahir.github.io/Barebones/'>Barebones</a> maintains independence from additional tools and simplifies theming and rebranding, while CSS Grid gives you flexibility and power when it comes to layouts." alt="Meet Barebones" >}}

The [CSS snippet collection](https://www.30secondsofcode.org/css/p/1) by *30 seconds of code* contains utilities and interactive examples for CSS3. Whether it’s custom checkboxes, menu overlays, or button animations, the collection has got you covered with useful snippets for layouts, styling and animating elements, and handling user interactions. *CodeMyUI* also features a collection of [pure CSS code snippets for user interfaces](https://codemyui.com/tag/pure-css/) &mdash; some of them with quite fancy effects.

## Color Themes For Your Dev Environment

Have you ever wished for a streamlined color theme across your entire development environment? One that you feel is pleasant for the eyes and that stays the same when you switch from your code editor to the terminal across to Slack? [themer](https://themer.dev/) helps you achieve just that.

{{< rimg href="https://themer.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc4fdf7e-d95c-4514-85e7-9d6e0cca4a04/6-frontend-boilerplates-starter-kits.png" width="800" height="526" sizes="100vw" caption="A streamlined color theme for your terminal, editor, and apps." alt="A streamlined color theme for your terminal, editor, and apps" >}}

*themer* takes a set of colors and generates themes for your development environment based on them. You can either start with a pre-built color set or create one from scratch by entering two main shades for background color and foreground text and accent colors for syntax highlighting, errors, warnings, and success messages. Once you’re happy with the result, you can download the themes you want to generate from the palette &mdash; different terminals and text editors are supported, just like Slack, Alfred, Chrome, Prism, and other tools and services. To make the color coordination complete, there are matching wallpapers based on your theme, too.

{{% feature-panel %}}

## Bootstrap Your Dotfiles

[Dotbot](https://github.com/anishathalye/dotbot) helps you install dotfiles with just one short command, even on a freshly installed system. It is designed to be lightweight and self-contained (no external dependencies or installation required) and can be used as a replacement for any other tool you were using to manage your dotfiles. Dotbot uses YAML or JSON-formatted configuration files to let you specify how you set your dotfiles and it knows how to link files and folders, create folders, execute shell commands, and clean directories of broken symbolic links. User plugins are supported for custom commands.

{{< rimg href="https://github.com/anishathalye/dotbot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/863cb268-356a-48e2-8ab1-956334603cee/7-frontend-boilerplates-starter-kits.png" width="700" height="438" sizes="100vw" caption="Bootstrap your dotfiles with <a href='https://github.com/anishathalye/dotbot'>Dotbot</a>." alt="Bootstrap your dotfiles with Dotbot" >}}

If you want to dive deeper into dotfiles, the [Awesome Dotfiles](https://github.com/webpro/awesome-dotfiles) list features helpful articles and tutorials, as well as example dotfile repos and frameworks, tools, and more.

## Electron Boilerplate

A minimalist [boilerplate application for Electron runtime](https://github.com/szwacz/electron-boilerplate) comes from Jakub Szwacz. To provide you with an easy-to-understand base that you can build upon, it only includes the bare minimum of tooling and dependencies that are needed for a fully-functional Electron environment. The boilerplate doesn’t impose any front-end technologies on you, so you are free to pick your favorite.

## Emergency Site Kit

In case of emergency, many organizations need a quick way to publish critical information. However, existing CMS websites are often unable of handling sudden traffic spikes and, depending on the kind of emergency, the local network infrastructure might even be damaged, leaving people with poor mobile connections out. Max Boeck’s [Emergency Site Kit](https://github.com/maxboeck/emergency-site) is here to provide people with the information they need in such cases, no matter the circumstances.

{{< rimg href="https://github.com/maxboeck/emergency-site" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b54b96f-4861-42b2-b63b-46b23977f6b4/8-frontend-boilerplates-starter-kits.png" width="800" height="509" sizes="100vw" caption="Quickly publish an emergency site with maximum resilience." alt="Quickly publish an emergency site with maximum resilience" >}}

The kit helps you quickly publish a simple website that is fast, accessible, and that can withstand large amounts of traffic. Built on the rule of least power, it uses simple technologies to ensure maximum resilience: The static files are optimized for first roundtrip, there’s only basic styling and one critical request, and service workers ensure offline support. One for the bookmarks.

## How To Favicon In 2021

Sometimes, it’s a good idea to re-evaluate best practices. When it comes to favicons, for example &mdash; particularly given the fact that front-end developers have to deal with more than 20 static PNG files to display a simple favicon these days. To make the process more straightforward, Andrey Sitnik came up with a smarter [solution that requires just five icons](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs) and one JSON file to fit most modern needs.

{{< rimg href="https://css-tricks.com/how-to-favicon-in-2021/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b9d0ebf-5a21-4fac-9794-130735756183/9-frontend-boilerplates-starter-kits.png" width="700" height="402" sizes="100vw" caption="A hassle-free solution for favicons." alt="A hassle-free solution for favicons" >}}

Inspired by Andrey’s approach, Chris Coyier went even a step further and went ultra-minimalist for the CSS Tricks favicon. He explains how it works in his post “[How to Favicon in 2021](https://css-tricks.com/how-to-favicon-in-2021/)”. An SVG concept to get your favicons ready for dark mode is also included.

## A Boilerplate For Forms

Let’s be honest, forms can be a pain. Luckily, there’s a little HTML and CSS boilerplate to change that: [Boilerform](https://boilerform.hankchizljaw.com/). Providing baseline BEM-structured CSS and appropriate attributes on elements, the little boilerplate gives your forms a head start.

{{< rimg href="https://boilerform.hankchizljaw.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa3ebed-2954-4e65-9f59-d5c47600a119/10-frontend-boilerplates-starter-kits.png" width="800" height="508" sizes="100vw" caption="Take the pain away from working with forms." alt="Take the pain away from working with forms" >}}

Designed to be straightforward to implement, you can, in its most basic form, drop a CSS file into your head with a short snippet and wrap your elements in a `boilerform` wrapper. To give you more control, there’s also a Sass and Patterns Library to work with. Whether it’s a contact form, card payment, or user signup, Boilerform has got you covered.

## All-In-One Front-End Boilerplates

The [Modern Front-End Development Boilerplate](https://github.com/yashilanka/Modern-Web-Boilerplate) is an all-in-one starter kit to develop, build, and deploy your next web project. Features include multiple front-end SCSS frameworks, an easy-to-manage folder structure, a centralized place to manage project-related settings like images, fonts, and JavaScript, hassle-free font-face generation, an integrated backup feature, and much more.

{{< rimg href="https://github.com/yashilanka/Modern-Web-Boilerplate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b930a5f2-5d73-4259-b46d-f48bdb6360a4/11-frontend-boilerplates-starter-kits.png" width="800" height="324" sizes="100vw" caption="Everything you need to develop, build, and deploy your next project in one package." alt="Everything you need to develop, build, and deploy your next project in one package" >}}

Another modern front-end boilerplate comes from the team at digital product studio tonik: the [HTML Frontend Boilerplate](https://github.com/tonik/html-frontend-boilerplate) is a modern solution for building fast, organized, and standardized web apps and sites.

## GitHub Template Guidelines

No matter if it’s a private repository you share with your team or an open-source tool intended for the community: the first thing people usually see of your project is the Readme on GitHub. But what goes into the Readme that actually provides value to the user? Cezar Augusto put together [guidelines for building GitHub templates](https://github.com/cezaraugusto/github-template-guidelines). Handy!

{{< rimg href="https://github.com/cezaraugusto/github-template-guidelines" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d0800c1-bcef-437b-8879-7a8d3cf080c2/12-frontend-boilerplates-starter-kits.png" width="700" height="277" sizes="100vw" caption="A template for user-friendly GitHub repositories." alt="A template for user-friendly GitHub repositories" >}}

## Create .gitignore Files For Your Git Repositories

Another little detail that can be automated to save you some precious time are `.gitignore` files. [gitignore.io](https://toptal.com/developers/gitignore) does exactly that. The site has a graphical and a command line method of creating `.gitignore` files for your operating system, programming language, or IDE.

{{< rimg href="https://toptal.com/developers/gitignore" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea92811-def1-44fc-aafc-7dfcbbbfd0c9/13-frontend-boilerplates-starter-kits.png" width="800" height="445" sizes="100vw" caption="No matter if you prefer the command line or a graphical interface, <a href='https://toptal.com/developers/gitignore'>gitignore.io</a> saves you time when creating .gitignore files." alt="No matter if you prefer the command line or a graphical interface, gitignore.io saves you time when creating .gitignore files" >}}

You can either enter the system and language you want to ignore directly on the site or copy the snippet that fits your shell from the documents to create an alias and, finally, the .gitignore file with the help of the command line.

## Hackathon Starter

If you have ever attended a hackathon, you know how much time it takes to get a project started: Once you’ve decided what to build, you need to pick a programming language, a web framework, a CSS framework, and you need to set up an initial project that team members can contribute to.

{{< rimg href="https://github.com/sahat/hackathon-starter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c59a3a-f1c1-480a-973a-ad1016191805/14-frontend-boilerplates-starter-kits.png" width="800" height="562" sizes="100vw" caption="A kickstarter for Node.js applications." alt="A kickstarter for Node.js applications" >}}

[Hackathon Starter](https://github.com/sahat/hackathon-starter) is here to help you set the base for your Node.js web applications so that you can focus on what really matters: the hackathon project itself. The boilerplate features local authentication with email and password, authentication via Twitter, Facebook, Google, GitHub, LinkedIn, and Instagram, flash notifications, MVC project structure, account management, API examples, and much more to help you get started.

## HTML Boilerplate Explained

How do you start a new project? Do you copy the HTML structure of the last site you built or maybe a boilerplate from HTML5 Boilerplate? Manuel Matuzović usually does the same, but recently, he encountered a situation where copying and pasting wasn’t an option: To document the structure he and his team are using at work, he had to understand the choices that have been made.

{{< rimg href="https://www.matuzo.at/blog/html-boilerplate/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7e65eee-dbc5-463b-b742-7546c6b948c6/15-frontend-boilerplates-starter-kits.png" width="700" height="459" sizes="100vw" caption="A boilerplate with detailed explanation of what does what." alt="A boilerplate with detailed explanation of what does what" >}}

The task took up quite some time to research, so Manuel [published the boilerplate](https://www.matuzo.at/blog/html-boilerplate/) on his blog for everyone to use, along with detailed explanations for each line of code so that you know exactly what you’re dealing with. A great opportunity to dive deeper into the underlying structure of a page. 

{{% ad-panel-leaderboard %}}

## Mobile-First Boilerplates

Do you need a lightweight, mobile-first boilerplate that includes only the essentials? Then Kraken might be for you. [Kraken](https://cferdinandi.github.io/kraken/) is not supposed to be a finished product but rather a starting point that you can adapt to any project. The base structure is a fully-fluid, single column layout, and an object-oriented approach to CSS lets you mix, match, and reuse classes throughout a project.

{{< rimg href="https://cferdinandi.github.io/kraken/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a770f68c-f513-4b6c-9a3a-0fb28dea45f5/16-frontend-boilerplates-starter-kits.png" width="800" height="259" sizes="100vw" caption="<a href='https://cferdinandi.github.io/kraken/'>Kraken</a> is built to be flexible and modular, with performance and accessibility in mind." alt="Kraken is built to be flexible and modular, with performance and accessibility in mind" >}}

Another great little helper if you feel you don’t need all the utility of larger frameworks is [Skeleton](https://getskeleton.com/). It only styles a handful of standard HTML elements and includes a grid. The boilerplate gets by with only 400 lines and there’s no installation and zero compiling necessary to get started.

## HTML5 Boilerplate

One of the most popular (if not the most popular) boilerplate to help you build fast, robust, and adaptable web apps or sites, is [HTML5 Boilerplate](https://html5boilerplate.com/). It bundles up the combined knowledge and effort of 100s of developers in one little package.

{{< rimg href="https://html5boilerplate.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f4f2ff9-b8ce-4247-b2eb-b5bbd838ff56/17-frontend-boilerplates-starter-kits.png" width="800" height="347" sizes="100vw" caption="A professional template for building fast, robust, and adaptable web apps and sites." alt="A professional template for building fast, robust, and adaptable web apps and sites" >}}

What’s in it? A lean, mobile-friendly HTML template, with optimized Google Analytics snippet, a placeholder touch device icon, and docs with extra tips and tricks. The boilerplate also includes Normalize.css, a modern, HTML5-ready alternative to CSS resets, and further base styles, helpers, media queries, and print styles. Perfect to give your project a head-start.

An alternative worth looking into is Igor Agapov’s Modern HTML Starter Template](https://github.com/harryheman/modern-html-starter-template) which was built with a focus on performance.

## Boilerplates For Responsive HTML Emails

We all know about the challenges that come with formatting HTML emails. A handy boilerplate for sending out nicely formatted messages while avoiding some of the major pitfalls comes from Sean Powell: [HTML Email Boilerplate](https://htmlemailboilerplate.com/).

{{< rimg href="https://htmlemailboilerplate.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d529087b-bb40-4537-ba88-e0b96bb9144c/18-frontend-boilerplates-starter-kits.png" width="700" height="383" sizes="100vw" caption="Avoid common pitfalls with a boilerplate for responsive emails." alt="Avoid common pitfalls with a boilerplate for responsive emails" >}}

Sean’s template is available in two versions &mdash; with and without comments &mdash; and consists of a header with global styles and a body section with more specific fixes and guidance to use where needed in your design. Whether you want to create your own template based on the snippets or cherry-pick the ones that fix your specific rendering issues, the boilerplate has got you covered.

Another email boilerplate worth looking into is Mark Robbins’ [Good Email Code template](https://www.goodemailcode.com/email-code/template), a simple stripped-back template that you can use for every email you send. If you’re interested in learning why each part of the code is where it is, Mark breaks it down in more detail.

Developed to help you build responsive HTML emails with confidence, the [Email Framework](https://emailframe.work/) provides you with pre-built grid options for responsive/fluid and hybrid layouts as well as with common components. The framework supports over 60 email clients and has been thoroughly tested using Litmus.

Last but not least, for those occasions when all you need is a simple responsive HTML template with a clear call-to-action button, you might also want to check out [Lee Munroe’s template](https://github.com/leemunroe/responsive-html-email-template). It’s tested on all major email clients, on mobile, desktop, and web. Happy emailing!

## A Complete Guide To HTML <code>&lt;head&gt;</code>

The head of a web page can get quite full, especially in large pages. But what do you actually need? And how to organize the head to prevent implications on performance? Josh Buchea put together a [handy guide](https://htmlhead.dev/) that dives deep into HTML `<head>` elements.

{{< rimg href="https://htmlhead.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38785e23-c8bb-47d7-89d3-54840a98a714/19-frontend-boilerplates-starter-kits.png" width="700" height="434" sizes="100vw" caption="A free guide to HTML5 head elements" alt="A free guide to HTML5 head elements" >}}

The guide covers everything from the recommended minimum and including elements for how a document should be rendered to links and references, favicons, social media, just like browser-depended information for things like smart app banners or “add to homescreen” features. A nice bonus: The guide is available in 11 languages. One for the bookmarks.

## PHP Boilerplates

If you’re looking for a simple yet powerful PHP framework with a very small footprint, [CodeIgniter](https://codeigniter.com/) has got you covered. CodeIgniter encourages MVC without forcing it on you, it has exceptional performance, and comes with built-in protection against CSRF and CSS attacks. There’s nearly zero configuration required to get you up and running.

{{< rimg href="https://codeigniter.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38ad5a08-167d-49bf-9e5c-c07c2a233bbe/20-frontend-boilerplates-starter-kits.png" width="800" height="451" sizes="100vw" caption="A lightweight, simple, and powerful PHP boilerplate." alt="A lightweight, simple, and powerful PHP boilerplate" >}}

A PHP framework that was also built with simplicity, performance, and security in mind is the [PHP Microsite Boilerplate](https://phpmicrosite.jenskuerschner.de/). As the name implies, it is perfect for building a rather small website without complex code structure. Key features include easy routing, intelligent serviceworker cache, and it’s SEO-optimized, and prepared for Accelerated Mobile Pages as well as for Progressive Web Apps.

Combining a well-thought-out developer experience with powerful features and an expressive, elegant syntax, [Laravel](https://laravel.com/) is also worth taking a closer look at. Whether you are new to PHP or a seasoned developer, Laravel was built to grow with you. Guides and tutorials help you get started while robust tools for dependency injection, unit testing, queues, real-time web events, and more will ease your life as you’re progressing.

Another handy resource to help you make full use of PHP’s mighty powers is [Symfony](https://symfony.com/). It includes a set of 50 reusable PHP components for your applications just like a framework for web projects that puts an end to repetitive coding tasks. The Symfony community counts more than 600,000 people from across the globe, all committed to helping PHP surpass the impossible.

## Create Projects From Cookiecutters

A command-line utility that creates projects from cookiecutters (i.e, project templates)? [Cookiecutter](https://github.com/cookiecutter/cookiecutter) does just that. It takes a source directory tree, copies it into your new project, and replaces all the names that are surrounded by templating tags `{{` and `}}` with names it finds in cookiecutter.json. These can be file names, directory names, and strings inside files. This enables you to bootstrap a new project from a standard form, skipping all the mistakes that are often involved when starting a new project. Project templates can be in any language or markup format and you can use both local cookiecutters or remote ones from Git or Mercurial repos.

{{< rimg href="https://github.com/cookiecutter/cookiecutter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc7ad4c1-6ef2-4c48-a8e1-27a0fb8747fe/21-frontend-boilerplates-starter-kits.png" width="607" height="145" sizes="100vw" caption="Create package projects from package project templates." alt="Create package projects from package project templates" >}}

## Quick Snippets

Sometimes you come across a small tip that turns out to be true gold: Maybe it’s a solution to a problem you’ve been tinkering with for some time or a short code snippet that makes your workflow a lot more efficient. The site [QuickSnippets](https://quicksnippets.dev/) collects little nuggets like these.

{{< rimg href="https://quicksnippets.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f09be36-81e8-4187-a3ea-5fd806cdd72f/22-frontend-boilerplates-starter-kits.png" width="800" height="463" sizes="100vw" caption="Precious snippets to improve your workflow." alt="Precious snippets to improve your workflow" >}}

Currently, the collection features almost 1,300 snippets by 296 authors to help you in your everyday work. The snippets cover everything from browsers, tools, and editors to CSS, HTML, JavaScript, Laravel, PHP, React, UI/UX, and Vue.js. A treasure chest just waiting to be opened.

## React Boilerplates

When it comes to React, there are several community-created boilerplates out there that are bound to save you time. One of them is the [React Boilerplate](https://github.com/react-boilerplate/react-boilerplate). The highly-scalable, offline-first foundation was created with a focus on performance, best practices, and developer experience and shines with features such as quick scaffolding, instant feedback, predictable change management, and internationalization support, among other things.

{{< rimg href="https://github.com/react-boilerplate/react-boilerplate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff35a189-94ae-48a7-9658-0593a8dae5b3/23-frontend-boilerplates-starter-kits.png" width="800" height="346" sizes="100vw" caption="Build scalable, performant, cross-platform apps." alt="Build scalable, performant, cross-platform apps" >}}

Another boilerplate worth looking into comes from the team at Infinite Red: [Ignite](https://github.com/infinitered/ignite) is the culmination of five years of constant React Native development and was created for both Expo and bare React Native. It comes with a CLI, component/model generators, and more.

The [Electron React Boilerplate](https://electron-react-boilerplate.js.org/) is another great foundation for scalable cross-platform apps. Fast iteration, incremental typing, and code optimization and minification out of the box are the three pillars it’s built upon.

The [React Starterkit](https://github.com/kriasoft/react-starter-kit) by Konstantin Tarkus is a front-end starter kit using React, Relay, GraphQL, and JAMstack architecture. It’s optimized for serverless deployment to CDN edge locations and comes pre-configured with CSS-in-JS styling, code quality tools like ESLint, Prettier, TypeScript, and Jest, as well as VSCode snippets and settings to make your workflow more efficient.

Speaking of VS Code: The [React + Redux Snippets](https://marketplace.visualstudio.com/items?itemName=aakashns.react-power-snippets) extension makes sure you always have the snippets you need available in your editor. It’s designed taking maximum advantage of code completion &mdash; perfect for power users.

Last but not least, if you want to use the best of all worlds to create your own, unique React boilerplate, [Leonardo Maldonado’s tutorial](https://www.freecodecamp.org/news/a-complete-react-boilerplate-tutorial-from-zero-to-hero-20023e086c4a/) is for you. He takes you step by step through building your own boilerplate from scratch with the main dependencies used in the React community today.

## A Snippet For Loading Responsive WebP Images

It has always been complicated to load images in the best sizes and formats, and with new image formats like WebP and AVIF gaining popularity, things don’t get any easier. If you want to ship WebP already today, you’ll need a loading strategy that also providess a fallback for browsers that don’t support the new format yet. Stefan Judis [shows how to do it](https://www.stefanjudis.com/snippets/a-picture-element-to-load-correctly-resized-webp-images-in-html/).

{{< rimg href="https://www.stefanjudis.com/snippets/a-picture-element-to-load-correctly-resized-webp-images-in-html/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33fc1d3d-8f82-4b00-bd58-68f940bdd408/24-frontend-boilerplates-starter-kits.png" width="700" height="465" sizes="100vw" caption="What do you need to consider when loading WebP images?" alt="A Snippet For Loading Responsive WebP Images" >}}

Stefan’s solution for loading a responsive WebP image uses the `picture` element, and even though it it involves quite a lot of lines of code, it’s worth it as the snippet not only loads the image in the best format but also the best sizes. One for the bookmarks.

Also, in case you missed it, Stefan has started publishing his [Web Weekly newsletter](https://www.stefanjudis.com/newsletter/) this year. Every Monday, you’ll find a colorful mix of resources all around frontend, productivity and web development learnings paired with handy tools and GitHub projects in your inbox. Stefan’s goal: make it the best email to start your week.

## SaaS Boilerplate

User authentication, cookie sessions, subscription payments, billing management, team management, GraphQL API, transactional emails &mdash; when you’ve built a SaaS product before, you know how much time it takes to make all the different tools involved play well together to offer the functionality you need. To change that, Max Stoiber created [Bedrock](https://bedrock.mxstbr.com/).

{{< rimg href="https://bedrock.mxstbr.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/598e7f3e-9dca-4922-b17d-76089efab46f/25-frontend-boilerplates-starter-kits.png" width="800" height="520" sizes="100vw" caption="Jumpstart your SaaS products with Bedrock." alt="Jumpstart your SaaS products with Bedrock" >}}

The modern full-stack Next.js and GraphQL boilerplate combines the best tools the JavaScript ecosystem has to offer into one solid foundation for your SaaS product. No need to master all of the technologies involved, if you know Next.js and GraphQL, you can start coding almost immediately.

## Static Site Boilerplate

Automated build processes, a local development server, production minification and optimizations, and the latest standards for static websites. Eric Alli’s [Static Site Boilerplate](https://staticsiteboilerplate.com/) uses the latest tech to make the process of building static websites more straightforward.

{{< rimg href="https://staticsiteboilerplate.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7da320ae-1a66-4624-ad56-a0edd5244d7f/26-frontend-boilerplates-starter-kits.png" width="800" height="525" sizes="100vw" caption="The Static Site Boilerplate utilizes the latest tech to make building static sites more straightforward. (<a href=''>Large preview</a>)" alt="The Static Site Boilerplate utilizes the latest tech to make building static sites more straightforward" >}}

The built-in development server will get you up and running in seconds, your HTML, styles, and scripts will be automatically linted, changes to files are monitored in real time, images are compressed for your production build, and sitemap.xml and robots.txt files are automatically included with your production build. A real timesaver.

{{% ad-panel-leaderboard %}}

## Style Guide Boilerplates

What do you need to consider when building a style guide that, well, works? Brad Frost’s [Styleguide Guide](https://bradfrost.github.io/style-guide-guide/) takes you step by step through each and every section and what goes into it &mdash; from the homepage to guidelines, styles, components, utilities, page templates, downloads, and even support, and contributions. A very complete overview.

{{< rimg href="https://bjankord.github.io/Style-Guide-Boilerplate/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55bb1663-1b6b-4827-a469-3cc67b4c066d/27-frontend-boilerplates-starter-kits.png" width="800" height="622" sizes="100vw" caption="Promote consistency and modular thinking with a style guide." alt="Promote consistency and modular thinking with a style guide" >}}

Brett Jankord’s [Style Guide Boilerplate](https://bjankord.github.io/Style-Guide-Boilerplate/) is a great starting point for crafting living styleguides. You can create a directory for it on your site to see how your live site’s CSS affects the base elements and start customizing the patterns and modules to your liking.

## Typographic Starter Kit

Do you need a little bit of help with typography? Not in terms of aesthetic design choices, but regarding markup? The typographic starter kit [Typeplate](https://typeplate.com/) has got your back. It defines proper markup with extensible styling for common typographic patterns.

{{< rimg href="https://typeplate.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47c31fb8-b2f3-48dd-ae71-5e332de4c175/28-frontend-boilerplates-starter-kits.png" width="800" height="509" sizes="100vw" caption="Typeplate helps you implement common typographic patterns." alt="<a href='https://typeplate.com/'>Typeplate</a> helps you implement common typographic patterns" >}}

Typeplate is available as a stripped-down Sass or CSS library of your choosing (including Bower and CDNJS) and is primarily concerned with technically implementing design patterns, not their looks: from typographic scale and word-wrap to indenting, hyphenation, small and drop capitals, small print, code blocks, quotes, footnotes, lists, and more.

## VS Code Snippets To Streamline Your Workflow

Are you using VS Code? We came across some useful extensions that handle the React, Vue, and Angular snippets you might need to type frequently for you. For Vue, be sure to check out [Sarah Drasner’s extension](https://marketplace.visualstudio.com/items?itemName=sdras.vue-vscode-snippets). It was built for real-world use and focuses on developer ergonomics instead of cataloguing API definitions.

{{< rimg href="https://marketplace.visualstudio.com/items?itemName=sdras.vue-vscode-snippets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d687c3aa-58ca-4d53-b88e-69907dc41a58/29-frontend-boilerplates-starter-kits.png" width="700" height="347" sizes="100vw" caption="Automate the things you type frequently." alt="Automate the things you type frequently" >}}

Burke Holland provides you with a collection of [essential React snippets and commands](https://marketplace.visualstudio.com/items?itemName=burkeholland.simple-react-snippets) that he selected from his day-to-day React use. And if you’re looking for Angular snippets, John Papa has got you covered. His extension adds [snippets for Angular for TypeScript and HTML](https://github.com/johnpapa/vscode-angular-snippets) to your VS Code setup.

Speaking of VS Code setup: Have you heard of the “[VS Code Can Do That Workshop](https://burkeholland.gitbook.io/vs-code-can-do-that/)” already? From customizing the editor to using Git and source control, it features eight exercises to enhance your VS Code skills. 

## Vue Boilerplates

Do you plan to build a Progressive Web App with Vue.js? [Vuesion](https://vuesion.github.io/docs/en/) has got your back. Described as the “most complete boilerplate for production-ready PWAs”, Vuesion focuses on performance, development speed, and best practices. The code is all yours, ready to be modified and build upon, so that you can implement the things you actually need, without being limited by the template itself.

If you’re looking for a solution to achieve a consistent user experience across your applications, [CION](https://cion.visualjerk.de/) might be for you. The design system utilizes design tokens, a living styleguide with integrated code playgrounds, and reusable components for common UI tasks. A great starting point that can be extended to your project’s needs.

To improve prototyping in Vue, there’s the prototyping tool [OverVue](https://www.overvue.org/). It allows developers to dynamically create and visualize a Vue application, implementing a real-time intuitive tree display of component hierarchy and a live-generated code preview. The resulting boilerplate can be exported as a template for further development.

{{< rimg href="https://www.overvue.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdd64c0c-be33-4cff-b224-d00a0e0d6a06/30-frontend-boilerplates-starter-kits.png" width="700" height="444" sizes="100vw" caption="Prototype-driven development with Vue.js." alt="Prototype-driven development with Vue" >}}

Have you ever tinkered with the idea of using Vue to power a blog? Ben Hong did, and created a dev environment to help you do the same. Optimized for blogging, the [VuePress Blog Boilerplate](https://vuepress-blog-boilerplate.bencodezen.io/) includes default features like RSS feed generation, a list of recent posts, etc. The minimal setup and Markdown-centered project structure help you focus on writing, and, thanks to the Vue-powered engine, you can use Vue components in Markdown and develop your theme in Vue, too.

For handy Vue snippets, little tips, tricks, useful directives, and nice practices, be sure to also check out [Vue Snippets](https://www.vuesnippets.com/) collection. A small but mighty collection.

## WordPress Plugin Boilerplate Generator

No one likes to repeat unnecessary tasks. That’s why WordPress developer Enrique Chavez built the [WordPress Plugin Boilerplate Generator](https://wppb.me/). Every time he started working on a new plugin, he found himself renaming file names, packages, subpackages. The generator automates the task.

{{< rimg href="https://wppb.me/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5d909d8-c4df-4132-b259-6f6c367e8034/31-frontend-boilerplates-starter-kits.png" width="800" height="493" sizes="100vw" caption="No more renaming file names when building a WordPress plugin." alt="No more renaming file names when building a WordPress plugin" >}}

All you need to do is type your plugin details in a short form containing plugin name, slug, uri, autor name, email, and uri, and the generator will generate a ZIP file for you with the correctly-named file structure. A great little timesaver.

## WordPress Starter Theme

Do you plan to build your own WordPress theme? The starter theme [Underscores](https://underscores.me/) helps you get started. It’s not meant to be used as a parent theme but as a stable base to kickstart your theme development adventures.

{{< rimg href="https://underscores.me/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f1e4dc7-5f7c-471f-ac2f-b90055fc41ad/32-frontend-boilerplates-starter-kits.png" width="800" height="427" sizes="100vw" caption="A robust base for your own WordPress themes." alt="A robust base for your own WordPress themes" >}}

Underscores comes with only minimal CSS so that there’s less stuff getting in your way when building your own theme. It shines with lean, well-commented HTML5, a helpful 404 template, an optional sample custom header implementation, custom template tags that keep your code clean, a mobile-friendly dropdown, and some other nifty features.

{{< signature "vf, il" >}}
