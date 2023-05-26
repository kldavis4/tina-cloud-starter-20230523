---
title: How To Improve And Refine Your WordPress Theme Development Process
slug: wp-theme-development-process
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/685f4963-b432-4318-8646-b95c889bc40a/wordpress-blue-illu.jpg
date: 2013-02-21T12:20:46.000Z
author: siobhan-mckeown
description: >-
  There is so much to learn about WordPress theme development. The Internet is
  home to hundreds of articles about building WordPress themes, to countless
  theme frameworks that will help you get started, and to endless WordPress
  themes, some of which are beautiful and professional but not a few of which
  are (to be honest) a bit crappy.
categories:
  - WordPress
  - Themes
  - Techniques (WP)
---
There is so much to learn about WordPress theme development. The Internet is home to hundreds of articles about building WordPress themes, to countless theme frameworks that will help you get started, and to endless WordPress themes, some of which are beautiful and professional but not a few of which are (to be honest) a bit crappy.

Rather than write another article on building a WordPress theme (which would be silly, really, since any theme I build would fall into the “crappy” category), <strong>I’ve asked some of the top theme designers and developers</strong> to share some tips and techniques to help you improve and refine your theme development and design process.</p>

<figure><a href="/wp-content/uploads/2013/01/splash.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-108219" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c1da4d-8cbd-483b-8230-64837d6fb929/splash.jpg" alt="splash" width="500" height="332" /></a></figure>

Before we get into that, Mark Forrester, cofounder of <a href="https://woothemes.com">WooThemes</a>, has shared some insight into his firm’s development process. Given WooThemes’ success, no doubt we can all learn something from it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[How To Get The Most Out Of A Premium WordPress Theme](https://www.smashingmagazine.com/2013/02/get-the-best-out-of-premium-wordpress-theme/)</span>
*   <span>[Powerful WordPress Tips And Tricks](https://www.smashingmagazine.com/2013/09/powerful-wordpress-tips-and-tricks/)</span>
*   <span>[WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)</span>
*   <span>[How To Improve The Deployment Of WordPress Websites](https://www.smashingmagazine.com/2013/04/wordpress-deployment-survey/)</span>

{{% feature-panel %}}

## A Peek Into Woo

Whether you work in a large theme shop or are a lone designer, you can <strong>learn plenty</strong> from another designer or developer’s workflow.
<ol>
 	<li>A theme at WooThemes starts life on the <a href="https://ideas.woothemes.com">ideas board</a>, through specifications provided by the community or based on a concept that’s emerged from customer research. It is designed either in house or by an industry-leading designer who is hired on contract.</li>
 	<li>The theme is then meticulously designed in Photoshop. All of the major elements are styled and the pages constructed <strong>before any code is touched</strong>. Mark recommends <a href="https://photoshopetiquette.com/">Photoshop Etiquette</a> for guidelines on structuring your design file. He says, “The better the Photoshop file, the easier the theme build.”</li>
 	<li>Once the design is approved, it’s assigned to a developer, who works from WooThemes’ base theme. This includes the templates that come with every WooTheme, along with basic styling. The base theme has a responsive layout, and the CSS is managed using <a href="https://lesscss.org/">LESS</a>, which Mark strongly recommends.</li>
 	<li>Theme development is managed with <a href="https://trello.com/">Trello</a>, and milestones are set with <a href="https://teamgantt.com/">TeamGantt</a>.</li>
 	<li>Once the theme is finalized, the developer creates a demo for the website that is populated with dummy content and that tests almost every element of the design.</li>
 	<li>The team sets about beta testing the theme. A list of bugs, tweaks and solutions is compiled, a hackathon is scheduled, and everything is completed by the developer.
<figure><a href="/wp-content/uploads/2013/01/woo_athena.png"><img loading="lazy" decoding="async" title="Larger view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18a82e13-7c80-4662-8074-a2eae155d42f/woo-athena.png" alt="A hackathon is scheduled." width="500" /></a></figure></li>
 	<li>For WooThemes’ own redesign (which is awesome — congrats, guys!), the team started to use <a href="https://www.bugherd.com/">BugHerd</a>, which helped them gather user feedback and track it directly in the pages.</li>
 	<li>All revisions are included in the change log for easy reference. A strict numbering convention distinguishes between bug fixes and new features.
<figure><a href="/wp-content/uploads/2013/01/woo_canvas.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a55e3e4b-9fe1-497c-9da8-4574543926f1/woo-canvas.png" alt="A strict numbering convention distinguishes between bug fixes and new features." width="500" /></a><figcaption><a href="/wp-content/uploads/2013/01/woo_canvas.png">Larger view</a>.</figcaption></figure></li>
</ol>
That’s a lot of process right there. Creating a WooTheme theme is about much more than knocking out a few lines of code. Here’s what Mark has to say:
<blockquote>"When we create and edit our themes it is not simply diving into the code. We have to carefully consider our community of users and how any code might impact their usage, and the template files’ customization ability."</blockquote>

Apart from workflow, what else can be learned from professional theme designers and developers?

## Develop Locally

If you’re not developing locally, then now’s the time to start. Here’s what <a href="https://chriscoyier.net/">Chris Coyier</a> has to say about it:
<blockquote>"Designers and developers who work mostly on WordPress sites are, in my experience, the worst offenders of the “just do it live” development system. FTP commandos, if you will. I know — I was one for a lot of years. I suspect it’s the case because there are quite a few requirements to run a WordPress site locally: an Apache server running PHP and a MySQL database.

These things aren’t preinstalled on most computers like they are on most servers. Even if you get over those hurdles, setting up a workflow between local and live isn’t trivial."</blockquote>

Luckily for you, Chris is going to show you a better way. Developing locally is easy to get started with.</p>

### Step 1: Set Up MAMP

### Step 2: Get Off FTP

Developing locally has so many benefits. In particular, you’ll be able to do the following:

*   Have a record of everything that has ever changed and when it changed.
*   Roll back mistakes.
*   Become more efficient by using text-editor features such as “Find in Project.”
*   Work on major redesigns without worrying about screwing up a live website.</p>

### Alternative Tools for a Local Server

*   [XAMPP](https://www.apachefriends.org/en/xampp.html), Apache Friends
*   “[Install WordPress Locally on Windows With XAMPP](https://wpmu.org/install-wordpress-locally-on-windows-with-xampp/),” Siobhan McKeown, WPMU.org
*   “[Configuring a Local Apache/PHP/MySQL Dev Environment in OS X](https://rzen.net/development/local-develoment-in-osx/),” Brian Richards
*   [WampServer](https://www.wampserver.com/en/)

## Use Live Reload

When you’re developing a theme, switching to the browser and reloading the page gets old pretty fast. That’s why Drew Strojny, founder of <a href="https://thethemefoundry.com/">The Theme Foundry</a> and the guy behind WordPress’ gorgeous new <a href="https://wordpress.org/extend/themes/twentytwelve">Twenty Twelve</a> default theme, uses <a href="https://livereload.com/">LiveReload</a>:
<blockquote>"LiveReload is a great little application that works through a browser extension. LiveReload automatically reloads your page when a file has been changed in your project.

This is a huge productivity boon when you’re editing and tweaking a WordPress theme. All those small page refreshes add up to a big chunk of time saved at the end of the day. Not to mention, your fingers get a much needed break!"</blockquote>

The Theme Foundry loves LiveReload so much that it’s built support for it into <a href="https://forge.thethemefoundry.com">Forge</a>, its free command-line toolkit for bootstrapping and developing WordPress themes.</p>

## Use Git

Git is a distributed version-control system that is popular among developers all over the world. The great thing about Git is that you can quickly create a branch, make changes within that branch and then test those changes without affecting the master version. It’s what The Theme Foundry uses for every project:
<blockquote>"Quite honestly, we’d be lost without it. Git makes branching cheap and easy. You can experiment quickly with different ideas without worrying about getting lost. Think of it like the trail of pebbles left by Hansel and Gretel to help them find their way back home.

Git gives you the power to leave nicely annotated pebbles along your development path. If you see something interesting and wander off the trail, but then later change your mind, you can always get back to where you started."</blockquote>

### Learning Git

*   [Git Immersion](https://gitimmersion.com/)
*   [Think Like (a) Git](https://think-like-a-git.net/)
*   [tryGit](https://try.github.com/levels/1/challenges/1)

## Clean Up Your Source Code

Messy source code is a developer’s nightmare. It makes finding things difficult, and it makes it extremely difficult for anyone else to work with it. That’s why <a href="https://perishablepress.com/">Jeff Starr</a>, WordPress editor here at Smashing Magazine, recommends <strong>keeping your template files and code clean</strong>.
<blockquote>"When designing WordPress themes, I like to keep template files and code well organized and tidy. For publicly released themes, keeping things squeaky clean lets ’em know you really care. Here are some tips for dazzling source code and markup:"</blockquote>

*   **Indent nested lines.**.  At the very least, source code should be readable by anyone who wants to work on the theme. If nothing else, take a few moments to properly indent your code.
*   **Indent tabs always.**.  Instead of tediously single-spacing your code, keep things consistent with tab spacing, which is faster and easier for everyone to work with.
*   **Be consistent with formatting.**.  When jumping in to edit a theme, almost nothing is worse than finding poorly formatted code. If you’re going to release your theme to the public, take the time to format consistently. For example, don’t mix tabs and single spaces; use the same number of tabs for similarly indented lines; and basically clean up your mess before rolling it out.
*   **Be consistent with details.**.  Sure, you could write either `something()` or `something();` (note the terminating `;`), but by being consistent with such details, you further improve the readability, accuracy and general appeal of your code.
*   **Include concise, descriptive comments.**.  Use `//` (for single-line comments) and `/**/` (for multiple-line comments) to add concise and meaningful comments to your code. But don’t overdo it — getting carried away and adding too many comments is easy, which is arguably worse than having too few comments. A general rule of thumb is to be concise and let the code speak for itself.
*   **Mind your line breaks.**.  Don’t break lines of code unless you have good reason to do so. For example, don’t put every inline HTML tag on its own line; don’t break apart SQL queries; and so forth. When you do need to break a line, do it where it makes the most sense, such as after opening brackets, between block-level HTML elements and after array items.
*   **Take advantage of the hierarchy.**.  Keep code simple and manageable by moving repeated sections of code to their own template files. For example, instead of including an entire loop in five different theme files, simply place it in a file named `loop.php` and include it as needed. Doing so will improve the usability of your source code and reduce the amount of work required to make sweeping changes.
*   **Keep it simple.**.  Keep your theme files as clean as possible by using default template tags and functionality wherever feasible. If and when you do need to include some majorly awesome piece of custom-scripting genius, do it via the theme’s `functions.php` file, rather than dumping it into, say, `sidebar.php`.
*   **Meta-organize it.**.  When scanning the source code of your theme files, a person should be able to recognize the various sections easily. Use tab indents and line breaks consistently to distinguish between template features, conditional functionality and other logically associated segments.
*   **Strive for clean markup.**.  Perhaps the best way to make a good impression with your publicly released theme is to ensure that the HTML output is clean and well organized. After installing a theme, a user can easily gauge the level of attention to detail by taking a quick look at the source code. You want your users to see nothing but [beautiful HTML markup](https://css-tricks.com/what-beautiful-html-code-looks-like/).
*   **Check your sanity.**.  Step back and look at the source code. Is it clean, well organized and complete? Does white space follow the closing `/>` tag? Do comments outweigh the actual code? Doing a quick check for formatting can help you catch things that you may have missed while throwing down in the thick of it.

Jeff adds:
<blockquote>"In addition to clean, well-organized code, I also like to include a proper <code>readme.txt</code> file. Descriptive and helpful readme files are a win-win: developers decrease the number of support requests, while users are able to make it work the first time."</blockquote>

## Tweak Your CSS In The Browser

Many of today’s Web browsers have built-in tools for improving and tweaking a design, debugging and development. <a href="https://rafaltomal.com/">Rafal Tomal</a>, lead designer at <a href="https://www.copyblogger.com/">Copyblogger Media</a>, chooses Chrome Developer Tools to quickly edit a theme’s CSS. In his own words, Rafal explains how to do it:
<blockquote>"Editing CSS code in big and complex themes can be difficult and annoying, especially if you are working on someone else’s theme and you don’t know the code structure at all.

Every modern popular browser has a built-in “developer tools” panel, which will help you quickly find the CSS code of a particular element. Also, many plugins are available (like <a href="https://getfirebug.com/">FireBug</a>) that offer more advanced functionality.

I prefer Google’s Chrome Developer Tools because it’s fast and very simple to use. All CSS changes you make are <strong>automatically visible</strong> on your website. Of course, none of these changes are saved in the file. Once you refresh it, you’ll lose them.

It’s very helpful if you need to quickly test some CSS changes or find a particular element in the code. Then, you can edit the CSS file in your editor and apply the changes.

To use it, first open the Developer Tools window by right-clicking your mouse on any element on the website that you want to edit, and then choose “Inspect element” (or press <code>Control + Shift + I</code> on Windows or <code>Command + Option + I</code> on Mac at any time):"</blockquote>

<figure><a href="/wp-content/uploads/2013/01/sp1.jpg"><img loading="lazy" decoding="async" title="Larger view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfd6e8c6-f382-4bc4-99f9-adcfab63bb12/sp1.jpg" alt="Screenshot Chrome Inspect Element" width="500" /></a></figure>

&nbsp;

<figure><a href="/wp-content/uploads/2013/01/chrome.jpg"><img loading="lazy" decoding="async" title="Larger view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6f6041f-52bc-4149-ae1b-ffc39b64030a/chrome.jpg" alt="Screenshot Chrome Developer Tools" width="500" /></a><figcaption>Inspecting elements and making your CSS changes visible through Google’s Chrome Developer Tools.</figcaption></figure>

<strong>Here is a guideline on how the Developer Tools can help you edit a WordPress theme:</strong>

1.  Click on any tag in the code view to see its CSS code on the right side. Click the small black arrow to expand the nested elements (you can also use the arrows on your keyboard). You can add attributes to the tags, remove entire nodes, copy them, etc.
2.  Use this tool to click on any element on your current website and see its CSS code in the Developer Tools.
3.  Click to open Developer Tools in a new window.
4.  Uncheck boxes to disable particular CSS declarations.
5.  Click on any CSS value or property to edit it. Click after the `{` or before the `}` to add a CSS declaration.
6.  Right-click on an image’s URL to quickly copy the path or open the background image in a new tab.
7.  Click to preview the entire CSS file and the particular element’s code. This is very helpful if multiple CSS files are loaded in one theme (for example, because of external plugins).
8.  Click to add a new style rule.
9.  The currently selected element in Developer Tools highlights the area on your live website and shows its dimensions.

Editing the theme’s CSS is much easier when you can quickly find the place you need to modify.

These tips on what you can do with Developer Tools are, of course, very simple. Learn more about it on Google’s <a href="https://developers.google.com/chrome-developer-tools/">Chrome Developer Tools</a> website.</p>

### Other In-Browser Editing Resources

*   [Firebug](https://getfirebug.com/)
*   “[Using Firebug to Troubleshoot and Customize CSS](https://www.studiopress.com/tips/using-firebug.htm),” Andrea Rennick, StudioPress

## Use A Preprocessor

A CSS preprocessor turns code written in the preprocessed language into standard old CSS. This optimizes your workflow and can shave hours off development time. It also provides you with more functionality, such as variables and nested rules. At The Theme Foundry, Drew uses <a href="https://sass-lang.com/">Sass</a> in all of his theme development:
<blockquote>"They help keep your style sheets <a href="https://en.wikipedia.org/wiki/Don't_repeat_yourself">DRY</a>, extensible and easy to manage. Once you start using these languages, you’ll realize how repetitive and tedious it is to write plain old CSS."</blockquote>

The Theme Foundry uses preprocessors such as Sass and LESS during development. Then it compiles them to normal CSS, which can be minified in a production environment. Drew includes the Sass files in themes sold through the Theme Foundry so that the files can be customized with a tool such as <a href="https://compass-style.org/">Compass</a>.</p>

### Preprocessor Resources

*   “[Sass and LESS: An Introduction to CSS Preprocessors](https://www.vanseodesign.com/css/css-preprocessors/),” Steven Bradley, Vanseo Design
*   “[Musings on Preprocessing](https://css-tricks.com/musings-on-preprocessing/),” Chris Coyier, CSS-Tricks
*   “[Using LESS With WordPress](https://www.noeltock.com/web-design/wordpress/using-less-with-wordpress/),” Noel Tock

## Use A Starter Theme

A few years ago, everyone was using a theme framework as the starting point of their theme development. The framework would come with loads of functionality for the designer or developer to use. More recently, there has been a move towards starter themes.

A starter theme kicks off your development with the bare bones of what you need to make a powerful theme. <a href="https://hugobaeta.com/">Hugo Baeta</a>, a designer at Automattic, uses <a href="https://underscores.me/">Underscores</a> (_s for short) for all of his theme development. I asked Hugo why he uses a starter theme:
<blockquote>"It cuts down my development time greatly. I’m not a native developer, and with the way WordPress is growing, some things are not so simple to achieve anymore. Especially with the use of functions and actions, it starts to go beyond my skill set with PHP. _S provides all that — or at least the most commonly used features — so the designer doesn’t have to think about it, or spend time researching.

It’s an amazing time-saver. If I’m doing a simple blog theme, I can code it up in a couple of days easily. Some people might say that using a starter theme forces you to learn the way it is marked up first, which is true. But if you’ve ever had to deal with Twenty Eleven or Twenty Twelve, the markup is quite similar."</blockquote>

<strong>Underscores comes with the following features to streamline your development:</strong>

*   Lean, well-commented, modern HTML5 templates;
*   A 404 template;
*   A sample custom header implementation in `inc/custom-header.php`, which can be activated by uncommenting one line in `functions.php` and adding the code snippet found in the comments of `inc/custom-header.php` to your `header.php` template;
*   Custom template tags in `inc/template-tags`, which keep your templates clean and neat and prevent code duplication;
*   Sample theme options in `/inc/theme-options/`, which can can be activated by uncommenting one line in `functions.php`;
*   Some small tweaks in `/inc/tweaks.php`, which can improve your theming experience and which can be activated by uncommenting one line in `functions.php`;
*   Keyboard navigation for image attachment templates (the script can be found in `js/keyboard-navigation.js` and is enqueued from the image attachment template, `image.php`);
*   A script at `js/small-menu.js` that makes your menu a toggled drop-down for small screens (such as phones) and ready for CSS artistry (it’s enqueued in `functions.php`);
*   Five sample CSS layouts in `/layouts` (two sidebars on the left, two sidebars on the right, a sidebar on either side of your content, and two-column layouts with sidebars on either side);
*   Organized starter CSS in `style.css`, which will help you get your design off the ground quickly;
*   The GPL license in `license.txt`.</p>

### Other Starter Themes

*   [BootstrapWP](https://bootstrapwp.rachelbaker.me/)
*   [Bones](https://themble.com/bones/)
*   Boilerplate

## Break Rank

Some final advice from <a href="https://happytables.com">happytables</a> founder <a href="https://noeltock.com">Noel Tock</a>:
<blockquote>"WordPress themes have long been stuck in their ways when it comes to layout. We’ve come to always expect a header, traditional navigation, content, sidebar(s) and a footer. Starter themes, frameworks and various tutorials also encourage us to use this outdated structure.

By continually trying to fill containers like marking items off a checklist, we neglect the most important parts of the website."</blockquote>

<figure><a href="/wp-content/uploads/2013/01/layouts.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad73fe5-010a-4174-9dc3-819d33a0eede/layouts.jpg" alt="Break the layout rank." width="500" height="328" /></a></figure>

<strong>My advice and challenge is straightforward.</strong> Tackle the following goals the next time you start a theme:

*   Design for real content. Lorem Ipsum, placeholders and other fluff will only pollute your concepts.
*   Bring your content to life through relevant and appropriate typography. Figuring this out early on will help you set the mood for the rest of the process.
*   Finally, give your theme room to breath by enabling it to coexist with all devices from the start.

The Web of tomorrow will not be about your widgetized areas or complicated navigation, but about the consumption of real and valuable content. Build for it instead of burying it.</p>

## Conclusion

Designing and developing a theme can take a lot of time, and it is based on a lot of learning. Hopefully, these techniques will help you refine your workflow, saving you time and making you more efficient. Got any more design or development techniques? We’d love to hear about them in the comments! And be sure to check out the resources and helpful tools below.</p>

### Resources

*   [Trello](https://trello.com/)
*   [BugHerd](https://www.bugherd.com/)
*   [MAMP](https://www.mamp.info/en/index.html)
*   [XAMPP](https://www.apachefriends.org/en/xampp.html)
*   [LiveReload](https://livereload.com/)
*   [Forge](https://forge.thethemefoundry.com)
*   [Sass](https://sass-lang.com/)
*   [LESS](https://lesscss.org/)
*   [Compass](https://compass-style.org/)
*   [Photoshop Etiquette](https://photoshopetiquette.com/)

{{< signature "al" >}}

