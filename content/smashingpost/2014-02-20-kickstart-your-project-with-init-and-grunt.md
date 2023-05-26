---
title: Kickstart Your Project With INIT And Grunt
slug: kickstart-your-project-with-init-and-grunt
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48e47aaf-672a-4407-adbf-60ea655f2c53/toolset-grunt-bower-opt-2.png
date: 2014-02-20T10:50:26.000Z
author: anselm-hannemann
description: >-
  Whenever you start a project, you have to repeat certain tasks and set up
  certain structures: create new folders, choose a framework, set up your
  development tasks. But configuring settings once and reusing them would be
  simpler. An easy way to achieve this is by using some kind of generator — for
  example, [Yeoman Generator](https://yeoman.io/generators.html) — or tools such
  as INIT, which can perfectly coexist with and even be used through a
  generator.
categories:
  - Coding
  - Workflow
  - Frameworks
  - Optimization
---
Whenever you start a project, you have to repeat certain tasks and set up certain structures: create new folders, choose a framework, set up your development tasks. But <strong>configuring settings once and reusing them</strong> would be simpler. An easy way to achieve this is by using some kind of generator — for example, Yeoman Generator — or tools such as INIT, which can perfectly coexist with and even be used through a generator.

You might already have used Yeoman Generator’s <a href="https://github.com/yeoman/generator-webapp">Web app</a>. It kickstarts a project, hooking into <a href="https://html5boilerplate.com/">HTML5 Boilerplate</a> and adding things like Compass, Sass Bootstrap, a preview server with LiveReload, CoffeeScript, JSLint, Bower and more. While it’s a good starting point to automate your initial configuration of a project, you will likely need to adapt it extensively to your needs.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Get Up And Running With Grunt](https://www.smashingmagazine.com/2013/10/get-up-running-grunt/)
*   [Building With Gulp](https://www.smashingmagazine.com/2014/06/building-with-gulp/)
*   [How To Harness The Machines: Being Productive With Task Runners](https://www.smashingmagazine.com/2016/06/harness-machines-productive-task-runners/)
*   [Meet ImageOptim-CLI, A Batch Compression Tool](https://www.smashingmagazine.com/2013/12/imageoptim-cli-batch-compression-tool/)

Keep in mind that it is intended for Web apps, so the lack of a build workflow might trouble you if you try to build a whole Web page architecture with it.

{{% feature-panel %}}

As is customary in the open-source world, you can extend Yeoman any way you like, modifying the available generators to your needs. But what exactly would you put in a custom generator? Have you thought about a good workflow and about which tools provide the most convenience?

## Introducing INIT

First, allow me to introduce <a href="https://use-init.com/">INIT</a>. Based on the popular HTML5 Boilerplate project, INIT <strong>adds modern tools</strong> — such as Sass, Grunt, RequireJS and Karma (for automated testing) — and is easy to customize and extend. You no longer have to worry about those few things that you have to do manually — or that you forget to do at all.

<a href="https://use-init.com"><img loading="lazy" decoding="async" class="131067" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfe86b88-5575-49d3-bb7b-8862ea4a595c/init-opt.png" alt="init-opt" width="500" height="268" /></a><br>
<em>INIT is a set of tools that provide a sensible workflow and structure on which to base your Web projects.</em>

You no longer have to copy a project’s default files or download dependencies that you use in most projects, such as jQuery, Modernizr and Normalize. INIT works on Mac OS X, Windows and Linux and supports all major browsers, including Internet Explorer 8 and nearly all mobile browsers.

INIT also <strong>provides a staging workflow.</strong> As you develop a page, you’ll want to refer to unminified CSS; after deployment, however, you’ll want to point to the versioned, minified CSS file; this project takes care of that. It also acts as a static file generator because it supports HTML concatenation out of the box.

For more details on INIT’s workflow philosophy and set of features, see The Nitty Gritty’s “<span class="removed_link" title="https://thenittygritty.co/reducing-boilerplate-code-front-end-init">Reducing Boilerplate Code in Front-End Projects</span>.”

INIT has a slightly different set of helpers than Yeoman’s Web app generator, including a workflow structure that is easy to extend and customize.

While Yeoman’s Web apps conduct simple testing, via Mocha and PhantomJS, INIT uses the more capable Jasmine test suite and Karma to run tests. INIT doesn’t expect you to need CoffeeScript, Compass or LiveReload, so it doesn’t install those by default. But should you need them, you can easily add them via <a href="https://github.com/search?q=%40use-init+init-">plugins</a>.

INIT does require a few dependencies to be installed on your machine:

*   [Node.js](https://nodejs.org/) The technical foundation of Grunt
*   [Bower](https://bower.io/) To manage front-end dependencies
*   [Grunt.js and Grunt CLI](https://gruntjs.com/) To run INIT tasks

<a href="https://www.smashingmagazine.com/2011/07/26/modern-version-control-with-git-series/">Git is also recommended</a> as a versioning system. To set up a new instance of INIT, grab the <a href="https://use-init.com/#download">project’s code</a>, extract the archive, and run the following in your command line:
<pre class="language-bash"><code>git init
npm install -g grunt-cli
npm install
git add .
git commit -m 'Initial commit'
</code></pre>

This <strong>will install everything you need to run the Grunt tasks automatically</strong>. It will also create a <code>components</code> folder that holds all vendor dependencies managed by <a href="https://bower.io/">Bower</a>.

<img class="130706 " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc5dbe9e-9543-445a-8be2-9bba0b9de956/init-npm-install.gif" alt="Animated gif showing a shell with the install process" width="644" height="363" /><br>
<em>Installing INIT in the command line</em>

Now that INIT is installed, we can take a closer look at what it brings to the table.

## Folders, Files And Build Strategies

We can divide the file structure into four parts: configuration files, development files, tests, and the folder for the ready-to-use distribution files.</p>

### Configure Your Editor And Code Settings

INIT sets up some decent guidelines to ensure that your code is consistent. The principal settings for the code editor are configured in the <a href="https://editorconfig.org/"><code>.editorconfig</code></a> file:
<pre class="language-bash"><code>
[*]
end_of_line = lf
indent_style = tab
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[.htaccess]
indent_style = space
indent_size = 4

[*.json]
indent_style = space
indent_size = 2
</code></pre>

Choose whether to use tabs or spaces for indentation, the character set, and the end of line style for the various file types. <strong>INIT has common defaults but can be easily adapted.</strong> If your editor recognizes EditorConfig files, then those configurations will be applied to your project automatically. The EditorConfig file is supported via a plugin in such apps as Sublime Text, WebStorm, Vim, Emacs, TextMate and more; a full list and links can be found on the <a href="https://editorconfig.org/">official website</a>.

INIT configures a few other things, too. For example, the <code>.gitignore</code> file contains all of the directories and files that should be excluded from Git versioning, and the <code>.jshintrc</code> file contains all of the rules that should be applied when JSHint tests your code.

Finally, the <code>.htaccess</code> file includes <a href="https://github.com/h5bp/server-configs-apache">Apache Server Configs</a>. If you use another server, please check the <a href="https://github.com/h5bp/server-configs">official repository maintained by H5BP</a>. The server configuration file can reduce bandwidth by sending out Gzip’d files to the client and by setting cache headers so that files are cached in the browser. It also configures security settings to safeguard your website from common attack vectors.

Lastly, you can set up redirects for your domain, which is incredibly useful for preventing duplicate content from appearing in search engines and for when you change the website’s domain.</p>

### Configure the Automated Helper Tasks

When talking about automated tasks earlier, I mentioned <a href="https://gruntjs.com/">Grunt</a>. It automates tasks that you usually run manually during the development phase of a project. The following are some of the tasks built into INIT:

*   JSHint and RequireJS
*   Sass parsing
*   Modernizr custom build
*   Image optimization via ImageMin
*   Concatenation, minification and versioning of files
*   Karma unit tests

Plenty more may be added to a project; INIT just provides the most useful and frequently used tasks to save you time. The official documentation contains a demonstration of <a href="https://github.com/use-init/init/blob/master/docs/extend.md">how to add LiveReload and SVG-Min</a> as tasks. A couple of other <a href="https://github.com/search?q=%40use-init+init-">official plugins</a> will save you even more time.</p>

### The Build Process

To use all of these tasks and benefit from the tools, you can run a couple of predefined Grunt tasks in the command line. These Grunt commands run several subtasks that we can use to build the page or run unit tests:

*   `grunt dev` This checks your JavaScript code through JSHint, compiles the Sass files and builds your static pages.
*   `grunt build` This optimizes images, creates a custom Modernizr build and runs Karma tests, among other things. This is the task you use to generate the production files.
*   `grunt travis` This runs unit tests via Karma in your continuous integration tool (in our case, [Travis CI](https://travis-ci.org/)).
*   `grunt watch` This runs the `dev` task every time you save a source file, so that you don’t have to constantly switch between browser, editor and command line.

<img loading="lazy" decoding="async" class="130904" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/094bb67e-8b2d-486a-baf4-0322268b459e/init-grunt.gif" alt="Animated gif showing the development build process running grunt in the Terminal" width="644" height="363" />

The terminal will tell you whether something has gone wrong, like whether the JavaScript has a syntax error or Sass couldn’t find a mixin.</p>

## Automated Tests: Make Sure You’re Doing It Right

The sooner you find an error, the cheaper it will be to fix. All of us at some point have spent at least half an hour hunting down a missing comma or trying to figure out why that one CSS property doesn’t work. These manual tasks could be done much more quickly by little programs.

JSHint, for instance, complains when we screw up JavaScript syntax by checking against common rules. Jasmine enables us to write unit tests to verify code. <a href="https://karma-runner.github.io/">Karma</a> runs those tests in the browser.

These automated unit tests <strong>ensure that the code works fine</strong>. While they don’t replace manual testing by you, they do add a layer of quality assurance and save you time by reporting problems as soon as they are introduced. There are almost no limits to writing unit tests. To learn about writing advanced unit tests, read Guido Kessels’ article “<a href="https://net.tutsplus.com/tutorials/javascript-ajax/advanced-unit-testing-techniques-in-javascript/">Advanced Unit Testing Techniques in JavaScript</a>”.

By default, INIT uses Jasmine as a test engine and uses Karma to run tests, which are both easier to handle than Mocha. But if you don’t like Jasmine or Karma, you can use any <a href="https://stackoverflow.com/questions/300855/javascript-unit-test-tools-for-tdd">other tool</a> that has a Grunt task.</p>

## Static Website Generator

A small static website generator is built into INIT by default that you can use right away.

In <code>pages.json</code>, you can set up the HTML files to generate. The pieces used to construct those files are usually stored in the templates directory. <strong>To tell INIT how to assemble things, you would declare a target</strong>, name its source pieces and specify a file to save the result to:
<pre class="language-javascript"><code>{
  "index": {
    "src": [
      "templates/header.html",
      "templates/index.html",
      "templates/footer.html"
    ],
    "dest": "temp/index.html"
  }
}</code></pre>

So that you don’t have to start from scratch, INIT comes with a preconfigured <code>index.html</code> file that you can customize.

This system enables you to work with multiple distinct files, which in the end will make up the HTML that you view in the browser. This is handy if you’re creating multiple files that all use the same header, footer and navigation. You can share content between the “static” pages without having to maintain duplicate files.</p>

## Customize!

INIT gives you a solid tool set to start projects more efficiently. It optimizes images and minifies code so that you don’t have to worry about those tasks.

But while it is a solid starting point for new projects, I encourage you to <strong>adapt it to your habits and coding workflow</strong>. If it’s missing some tools you like, add them; if you don’t need some tools that it does have, remove them. Adapt it to be your ideal framework.

I’ve used INIT for some large projects and use it now for most of my projects, configuring it to what I (and the development team) actually need, which varies from project to project. The static file generator makes it easy for me to work independently of the back-end team, while still being able to show clients my progress right in the browser.</p>

## An Outlook

We are working on a number of plugins to extend INIT’s feature set. You can <a href="https://github.com/use-init">find the plugins on GitHub</a>.

INIT is not meant to replace Yeoman. In fact, you can use INIT via Yeoman. A <a href="https://github.com/use-init/generator-init">Yeoman generator</a> is available — <code>generator-init</code> — so you can simply build your own INIT instance using <code>npm install -g yo</code> and <code>npm install -g generator-init</code>.

I’d love to hear feedback, feature requests, ideas and insights on how you use INIT. Please let me know here in the comments, or <a href="https://github.com/use-init/init/issues">file a bug in GitHub</a>.

{{< signature "al, ea, il" >}}

