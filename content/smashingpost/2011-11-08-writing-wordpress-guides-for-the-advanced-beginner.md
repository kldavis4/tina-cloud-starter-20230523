---
title: Writing WordPress Guides For The Advanced Beginner
slug: writing-wordpress-guides-for-the-advanced-beginner
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54ca4ae5-dd60-4ccc-bc57-b16a67d7c50b/wp-beginner-illu.jpg
date: 2011-11-08T15:59:58.000Z
author: scott-meaney
description: >-
  Creating WordPress tutorials is a fantastic way to help build the WordPress
  community and to increase your Web traffic. That’s no secret. Just Google
  “wordpress tutorial” and you’ll see hundreds of results. The complete novice
  will find scores of well-written tutorials clearly demonstrating the basics of
  the WordPress dashboard and of activating the default template, in simple
  jargon-free language.
categories:
  - WordPress
  - Themes
  - Tutorials
  - Plugins
  - Guides
---
Creating WordPress tutorials is a fantastic way to help build the WordPress community and to increase your Web traffic. That’s no secret. Just Google “wordpress tutorial” and you’ll see hundreds of results. The complete novice will find scores of well-written tutorials clearly demonstrating the basics of the WordPress dashboard and of activating the default template, in simple jargon-free language.

<a href="https://www.smashingmagazine.com/2011/11/08/writing-wordpress-guides-for-the-advanced-beginner/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2948f20c-aedd-46ab-92ce-a4ecc79bb3aa/howtosplash500.jpg" alt="howtosplash550" width="500" height="363" /></a>

Unfortunately, after the first few “Hello World!” tutorials, they are in for a bit of a learning curve. Suddenly, the guides start to skip a lot of details, assuming that the reader “already knows this stuff.” Others are simply written exclusively for advanced WordPress users.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)
*   [50 Free Resources That Will Improve Your Writing Skills](https://www.smashingmagazine.com/2009/06/50-free-resources-that-will-improve-your-writing-skills/)
*   [The Immersive Web And Design Writing](https://www.smashingmagazine.com/2012/10/the-immersive-web-and-design-writing/)

{{% feature-panel %}}

So, where does a new developer go after square one?

In this article, we’ll explore how to create clear easy-to-navigate tutorials, and tailor them to the underserved “advanced beginner” Web developer. The entire goal of this article is to make sure we see many more tutorials written for budding new coders who are ready to jump to the next level.</p>

## Who Exactly Is An “Advanced Beginner”?

Advanced beginners are people who generally understand how WordPress works but don’t fully understand how to implement its concepts. They are stuck in that awkward stage where a “For Dummies” book has nothing new to offer but raw code is still vaguely confusing. In your tutorials, you should strive to eliminate this common “tough it out” phase.

For our purposes, let’s assume that we are writing for someone who has a reasonably good grasp on the following:

*   Can read and write XHTML and CSS, but probably sits with a cheat sheet open to get through those tricky spots;
*   Knows little to nothing about PHP;
*   Can navigate the WordPress dashboard and has basic knowledge of image resizing and editing;
*   Understands the basic idea and principles of WordPress, but not necessarily how to execute them;
*   Appreciates the simplicity of WordPress templates but wants to learn how to create or tweak their own.</p>

## Admitting That WordPress Can Be Tough

We all need to stop pretending that WordPress is this magical dirt-simple Web development solution. Yes, using it is much easier than designing a custom CMS, but for new users looking to get under the hood, the tool can still be daunting and complicated.

For the average coder who is still just getting a grip on fundamental CSS, even the strange-looking batch of official WordPress folders that come in the installation ZIP file can be intimidating.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/947c2518-c99a-48ac-a01f-350a1ca73247/wpfiles.png"><img class="104086" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/947c2518-c99a-48ac-a01f-350a1ca73247/wpfiles.png" alt="" width="550" height="525" /></a><br>
<em>This is way more confusing for a beginner than seeing a simple HTML file, a CSS file and some images.</em>

When you refer to a file such as <em>style.css</em> or an image, be sure to tell readers exactly where to look and where to save these files.</p>

## Basic Guide-Writing Principles

Before we delve into WordPress-specific tips, let’s go over some basic principles for any tutorial.

### Keep It Tidy

Readers have sought your advice because they are confused. Don’t add to their troubles with a cluttered how-to article. Use plenty of bullet points, and keep paragraphs short. If you’re tackling a complex idea, split it up into sections.

Take the format of Smashing Magazine’s articles. Articles are broken up so that each sub-topic has its own section. This simplifies the navigation, makes the content more visually appealing and clearly guides the reader through the process.</p>

### Make Sure Readers Are Fully Prepared

Any good tutorial includes all of the resources it recommends. Don’t just say “make a blue image” — give it to them. Otherwise you risk over-complicating things for the reader. Provide sample files, and explain that your lesson will deal exclusively with these readily available resources. You wouldn’t want them to suddenly have to read a Photoshop tutorial when they’re only interested in learning how to customize their header.

<a href="https://net.tutsplus.com/tutorials/wordpress/how-to-create-a-wordpress-theme-from-scratch/"><img class="104087" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53af5a56-5ecc-4d9f-9694-b3dfb2b61c59/filesincluded.png" alt="" width="550" height="384" /></a><br>
<em><a href="https://net.tutsplus.com/tutorials/wordpress/how-to-create-a-wordpress-theme-from-scratch/">This tutorial</a> includes everything a reader needs to get started, including a visual demo and easily accessible sample files.</em>

### Define Your Goal

The best tutorials focus on a single topic. Plan the article before writing it. You shouldn’t explain every aspect of CSS and WordPress on every page of your website. What will readers get from this particular tutorial? A nice neat list at the top of the article should clearly define its parameters.</p>

### List the Prerequisite Skills

A tutorial should always list any skills that the reader will be expected to have. Instead of cluttering an otherwise focused guide with extraneous detail, provide links that direct readers to where they should go to learn about particular topics. This will help new developers who are nearly clueless, while keeping the article clearly focused for more advanced readers.</p>

## Tips Specifically For WordPress Guides

Now that we’ve discussed some fundamental organizational skills that will make any tutorial clear and easy to follow, let’s delve into some WordPress-related areas that many guides seem to miss.</p>

### Taming the Codex

The WordPress Codex is a powerful tool that can give your tutorial a much-needed jolt of clarification. Just be aware that to newbie designers, the Codex can seem like a massive labyrinth of articles, with each topic requiring that you read several earlier lessons in order to fully grasp. As the experienced coder, you need to show that, when used properly, the Codex presents the cleanest example of a concept.

<a href="https://codex.wordpress.org/"><img class="104083" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e9681c6-e4ca-4ca0-9668-bd8c1d265355/codex.png" alt="" width="550" height="372" /></a><br>
<em><a href="https://codex.wordpress.org/">The Codex</a> is one of the most useful tools available to a WordPress developer.</em>

Don’t just say “Check the Codex” and drop in a link. Your readers need context. Your main goal in writing a tutorial that refers to the Codex should be to eliminate the reader’s need to plunge into its depths. Tell them what they can expect to read on the page, illustrating exactly how they can use the particular lesson you’re linking to.

It might even be to your benefit to point readers to a “beginner’s guide” to understanding the codex. <a href="https://lorelle.wordpress.com/2005/10/28/a-guide-to-the-wordpress-codex-the-online-manual-for-wordpress-users/">Here is my favorite.</a>

### Keep Them On Target, Visually

The most important thing to do to keep readers on track is to provide constant updates throughout the article on what they should be seeing in their own implementation. For example, if your tutorial is multiple pages, always start with an illustration of the finished product. After each milestone, provide a “Here’s what you should be seeing right now” example. Whenever possible, include working samples of the project or its parts for the reader to experiment with. (These functional samples might have to be run from the author’s server or a third-party website.)

A WordPress project could very easily require coding between a few files. If someone isn’t following closely enough, they could miss something simple that wildly alters their results. Your milestone examples will give readers up-to-the-minute feedback on where they are going wrong. It’s the best way to make sure you aren’t losing anyone.</p>

### Make Your Code Selectable

This is crucial to any WordPress tutorial. If you are explaining a concept in code, allow the reader to copy and paste the examples whenever possible. For curious readers, nothing is worse than wanting to test a sample line of code, only to realize that they have to fully type it out. This principle seems self-evident, but many guides simply explain an idea and say, “Add this code,” alongside a screenshot of the finished style sheet. If the reader misses one semicolon, all their work will be worthless. That’s infuriating.

While there may be some merit to having the reader actually write out the code, most people probably won’t see it that way. They are much more likely to seek out another tutorial, one that doesn’t force them to constantly rewrite code that they don’t yet understand.</p>

### Be Wary of PHP

While it’s a necessary part of WordPress, remember that to someone just getting their footing with something as relatively basic as CSS, PHP code can look like someone fell asleep at the keyboard. Too many tutorial providers assume that their readers understand even the first thing about PHP. This is often not the case.

In the likely event that you are explaining low-level PHP to readers, be mindful that they might be confused. Give a short description of exactly what is happening in the code. As always, provide a link to a relevant PHP tutorial.</p>

### Clarifying Custom Widgets

Admittedly, this recommendation is pretty specific, but bear with me. When I was getting started, one of the most infuriating things about WordPress tutorials was when they said, “Write a quick widget with this code…”

Now, once a reader has created their first widget, it becomes completely obvious that most of the time all they’ll need to do is drag the “Text Widget” and add some basic HTML code to it. But first they need to get past this initial step. Remember that to someone looking with fresh eyes, they may not understand your shorthand.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c19bc9b-0bdf-4fd8-b56f-f28c3745825f/textwidget.png"><img class="104085" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c19bc9b-0bdf-4fd8-b56f-f28c3745825f/textwidget.png" alt="" width="550" height="374" /></a><br>
<em>The blank text widget is a simple yet potentially deceptive name for a powerful tool.</em>

So, I always like to see a description such as, “Use the ‘Text’ widget to create this option. You can simply add raw HTML into the blank box and drag it to your sidebars. This will then work just like any other widget.”

### Always Provide Documentation for Video Tutorials

Without a doubt, video is a massive help for confused developers. It provides detail-rich, play-by-play instruction that carefully guides the viewer through the concepts in the tutorial. Just be sure to accompany the video with detailed textual documentation. Otherwise, people will repeatedly have to rewind and squint at the screen just to copy your instructions. That’s an easy way to lose fans.

Treat the video as an aid, not as the main event. <a href="https://lifehacker.com/5790955/how-to-make-a-web-site-the-complete-guide/">This tutorial on Lifehacker</a>, though not specifically for WordPress, illustrates this principle perfectly.</p>

### Update Your Tutorial As Needed

Keep your guides relevant and dynamic. Too often, tutorial writers will clarify major points in the comments section of their page, while the tutorial itself remains static. Or they just ignore the page entirely, leaving now-irrelevant guides to linger on the Internet.

Keeping in touch with your audience is wonderful, but giving new readers the best possible experience is also important. Don’t expect people to comb through two years’ worth of comments to find your changes.

Make sure your supplemental links remain relevant. Nothing is worse than reading a tutorial from 2007 and seeing the words “With a simple change, it should look like <a href="https://www.example.com/">this</a>!” Surely in 2007 that link was perfect, but if it leads to an unrelated page in 2011, it will undermine your entire article.</p>

### Tell Them Where to Code

Make sure that newbies are tweaking code in the right place. Point out that, in general, they shouldn’t edit files from within the WordPress dashboard. That leaves little room for error, and if the coder isn’t careful, they could lose hours of progress.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48259883-15c9-4a9a-ac0c-f50f03c7a466/coda.png"><img class="104084" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48259883-15c9-4a9a-ac0c-f50f03c7a466/coda.png" alt="" width="550" height="455" /></a><br>
<em>A brief glimpse at the SFTP- and FTP-enabled one-stop code editor, Coda.</em>

Instead, teach them to use an SFTP- or FTP-enabled editor, such as Coda or <a href="https://www.adobe.com/products/dreamweaver.html">Dreamweaver</a>. It’s a safer, fixable way to correct any mistakes that arise.</p>

### Teach Them How to Test

This last point is just a personal preference that I wish more people would do. One of the best things about basic HTML and CSS is that you can easily test them locally by simply reloading the browser. When you jump into WordPress, this testing process becomes significantly more complicated. Advanced beginners will likely be lost once they realize that they can’t test by simply dragging their WordPress creations into a browser. This leads many new coders to test their unfinished creations on production websites.

Tutorial writers should stress the importance of not testing WordPress changes on a live website. Explain the myriad benefits of designing on a risk-free local server. Just point the reader to one of the many existing server guides, and briefly mention the pitfalls of testing code on a live website. Michael Doig’s article “<a href="https://michaeldoig.net/4/installing-wordpress-locally-using-mamp.htm">Installing WordPress Locally Using MAMP</a>” is one of the most useful set-up guides.</p>

## Conclusion

Whether you’re writing a tutorial about WordPress or anything else, clarity is paramount. Put yourself in the reader’s shoes. WordPress is built on the efforts of a wonderfully helpful community that is full of excellent tutorials and experts. But, as in any community, this has resulted in some confusing jargon and common shortcuts.

These can overwhelm new developers. Tutorial writers should avoid unnecessary jargon and always explain any references and functions that they use, no matter how basic they seem. Remember that, as the guide, your knowledge is likely far beyond that of your readers. What is obvious to you could be brand new to them.

By making your tutorials easier to understand, you’ll greatly increase your own Web traffic and enrich the greater WordPress community.</p>

### Other Resources

Here are a few tutorials that are easy to follow and that adhere to many of the points mentioned here.

*   “[Complete WordPress Theme Guide,” Web Designer Wall](https://webdesignerwall.com/tutorials/complete-wordpress-theme-guide) A great tutorial to help people get started in coding. Plus, it features an eloquent section on installing WordPress locally.
*   “[How to Make a Website: The Complete Beginner’s Guide](https://lifehacker.com/5790955/how-to-make-a-web-site-the-complete-guide),” Lifehacker An excellent blog across the board, Lifehacker has created some absolutely phenomenal video tutorials. The documentation makes this ones an expertly designed guide.
*   “[CSS Techniques: Using Sliding Doors with WordPress Navigation](https://wphacks.com/sliding-doors-wordpress-navigation-css-technique/),” WP Hacks WP Hacks is a great resource for WordPress designers. This piece is well organized and demonstrates the correct way to present code in a tutorial.
*   “[Installing WordPress Locally Using MAMP,”](https://michaeldoig.net/4/installing-wordpress-locally-using-mamp.htm) Michael Doig This is the excellent guide to setting up WordPress using MAMP that I mentioned earlier.
*   “[How to Create a WordPress Theme from Scratch,”](https://net.tutsplus.com/tutorials/wordpress/how-to-create-a-wordpress-theme-from-scratch/) Nettuts+ Nettuts+ is always a great source of tutorials. In this one, you’ll see how to present all relevant resources in a tutorial.

{{< signature "al" >}}

