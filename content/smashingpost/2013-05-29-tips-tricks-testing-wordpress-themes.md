---
title: Tips And Tricks For Testing WordPress Themes
slug: tips-tricks-testing-wordpress-themes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19182e3e-12a7-48bf-877f-15a8e5435e1d/wp-16.jpg
date: 2013-05-29T14:33:20.000Z
author: daniel-pataki
description: >-
  Whether you offer free or premium themes, testing should be a major part of
  your development process. By planning in advance, you can foster a development
  environment that deters some bugs by design and that helps you prevent others.
categories:
  - WordPress
  - Themes
  - Techniques
  - Techniques (WP)
---
Whether you offer free or premium themes, testing should be a major part of your development process. By planning in advance, you can foster a development environment that deters some bugs by design and that helps you prevent others. The aim of this article is to share some of the tricks I use personally during and after development to <strong>achieve a bug-free product</strong>.

This article is split into three distinct sections:

1.  Setting up,
2.  Development phase,
3.  Final testing.

This should give you a good overview of what you can do over the course of the development cycle. I invite everyone to chime in with their own tips in the comments. I’d be interested to hear your tips on testing WordPress themes!

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[The WordPress Community Offers Advice To Beginners](https://www.smashingmagazine.com/2013/02/wordpress-community-offers-advice-beginners/)</span>
*   <span>[How To Contribute To WordPress](https://www.smashingmagazine.com/2013/05/contributing-to-wordpress/)</span>
*   <span>[Schedule Events Using WordPress Cron](https://www.smashingmagazine.com/2013/10/schedule-events-using-wordpress-cron/)</span>
*   <span>[The WordPress Theme Customizer](https://www.smashingmagazine.com/2013/03/the-wordpress-theme-customizer-a-developers-guide/)</span>

{{% feature-panel %}}

## Setting Up

Setting up your environment correctly can go a long way to preventing bugs and helping you to find them more easily. For me, it all starts with version control.</p>

### Setting Up WordPress

You could do about a million things when setting up WordPress to ensure you make as few mistakes as possible. I always do a number of things:

*   **Using a network (WordPress Multisite)**.  While not much different, developing for a network installation does present some differences in methodology (especially with plugins). Because I use one network for the themes that I make, it is still useful, and I can make sure that the themes work properly on network installations as well.
*   **Custom table prefix**.  Installing a custom table prefix helps in two ways. First, it ensures that you don’t hardcode database queries. Secondly, it gives you an additional layer of security. Everyone knows that the default is `wp_`, so choosing `239Jd_23eKSmCM892_Vuhwedp` as your prefix is like adding a mini-password to your database.
*   **Enable debugging information**.  I’ve found that a _lot_ of sloppy developers leave undefined variables and other such nuisances all over the place. PHP might not complain about these by default, but they are annoying and could lead to other problems down the road. To make sure you don’t accidentally trigger notices, simply make sure that `WP_DEBUG` is set to `true` in `wp-config.php`.
*   **Disable WordPress script concatenation**.  A more obscure feature of WordPress is the option to disable script concatenation. Sometimes, when figuring out how WordPress does things, you’ll want to look at some of the built-in JavaScript files. If you set `define('CONCATENATE_SCRIPTS', false);` in the `wp-config.php` file, your scripts will be pulled in separately. Don’t forget to reenable it for production environments!
*   **Advanced query analysis**.  If you set the `define('SAVEQUERIES', true);` constant in `wp-config.php`, WordPress will save all of the queries performed into a variable. You’ll be able to access it by printing the `$wpdb->queries` variable.
*   **Disable the trash**.  Normally a great feature, the trash just gets in the way when you’re developing and creating and deleting pages and posts. Disable the trash by setting `define('EMPTY_TRASH_DAYS', 0 );` in `wp-config.php`.
*   **Test posts**.  Right off the bat, I usually import the test content from the “[Theme Unit Test](https://codex.wordpress.org/Theme_Unit_Test).” This test suite contains normal posts, posts without titles, posts without content, posts with and without featured images, sticky posts, posts with a load of categories and so on. It helps you to test fringe cases especially well, which is critical for all themes.

I also like to create 16 users with different roles. Unfortunately, I don’t have a script for this, but writing one wouldn’t be that difficult. You could create an array in a file and just feed it to the <code>wp_insert_user()</code> function in a loop. Something like this:

<pre><code class="language-php">
$users[0] = array(
  'first_name'   =&gt; 'Daniel',
  'last_name'    =&gt; 'Pataki',
  'user_login'   =&gt; 'danielpataki',
  'user_pass'    =&gt; 'mysupersecretpass',
  'user_email'   =&gt; 'mysupermail@mymail.com',
  'display_name' =&gt; 'Daniel',
  'description'  =&gt; 'Guitar-wielding Web developer',
  'role'         =&gt; 'administrator'
)

$users[1] = array(
  'first_name'   =&gt; 'Viki',
  'last_name'    =&gt; 'Makra',
  'user_login'   =&gt; 'viki',
  'user_pass'    =&gt; 'hersupersecretpass',
  'user_email'   =&gt; 'hersupermail@mymail.com',
  'display_name' =&gt; 'Viki',
  'description'  =&gt; 'Front-end developer and awesome admin handler',
  'role'         =&gt; 'editor'
)

foreach( $users as $user ){
  wp_insert_user( $user );
}
</code></pre>

I actually have a set of test emails for each user account I create, and I add avatars for each of them on <a href="https://gravatar.com">Gravatar</a>. You can grab a bunch of cool images by searching for <a href="https://graphicriver.net/search?utf8=%E2%9C%93&amp;term=avatars">avatars on ThemeForest</a>.

You can also use a plugin such as <a href="https://wordpress.org/extend/plugins/user-photo/">User Photo</a> or <a href="https://wordpress.org/extend/plugins/simple-local-avatars/installation/">Simple Local Avatars</a> to add the photos locally.</p>

### Version Control

Version control is one of the best things to come along since bacon. Whether you prefer Git, SVN, Mercurial or another system, you will be able to roll back to different versions and always have a backup of your work lying around.

Version control is supposedly most helpful with collaboration. While this is true, I’ve found that the order it brings to your coding practice is just as valuable. I highly recommend reading <a href="https://svnbook.red-bean.com/"><em>Version Control With Subversion</em></a> and/or <a href="https://git-scm.com/book"><em>Pro Git</em></a>. They both have a wealth of practical information about version control, both general and specific.</p>

## During Development

Here are some useful tips and tricks to follow during theme development.</p>

### “I’ll Do That Later.”

As a seasoned coder, I usually know my way around a coding task when one arises, but pushing myself to the end of such tasks is difficult. If I am implementing a map-based search tool, then the biggest tasks are to make sure that the form works and that when the user performs a search, it hooks into Google and the results are returned and displayed on the map and so on. Once those are done, then making sure that the form looks good, that administrators can define the map type to the user and so on are minor matters.

Previously, I would work through major features and then go back and touch up the details. The only problem with this is that it is <strong>the worst practice ever</strong>. You forget things; your code gets messy; then you can’t maintain it properly; and it becomes a giant headache.

My recommendation is to either develop a feature or not. Make sure that you’ve added all planned features and that they don’t just <em>kinda</em> work or have bugs that are “not big problems because they can easily be fixed later.”

If your code is extremely modular, you could, of course, separate the presentation from the functionality, but that’s a story for another article.</p>

### Modularity Is King

The best way to develop is to follow the lessons of object-oriented languages or object-oriented PHP. You can’t (or might not want to) code everything with classes, but the general philosophy is very helpful.

Widgets in WordPress are a great example. Using a pretty simple pattern, you can create the back-end form for a widget and make sure that it saves its data properly and that you can add the front-end code. Then, the widget will work anywhere, anytime.

You can apply the same principles to most coding tasks. Write code that is as independent as possible. Your code will remain clean and will do wonders for maintainability.</p>

### The Right Tools

The biggest speed boosts during development come from choosing the right development tools. Below is a list of apps and other tools that speed things up a lot for me.

<strong>LESS</strong>

Almost a no-brainer nowadays, <a href="https://lesscss.org/">LESS</a> or <a href="https://sass-lang.com/">Sass</a> should be in everyone’s tool belt. While not without <a href="https://blog.millermedeiros.com/the-problem-with-css-pre-processors/">criticism</a>, these tools help <em>way</em> more than they harm.

A quick note about LESS. Many people really hate the idea of using LESS for CSS. While their points are valid, I disagree. But it’s up to everyone to make their own choice. Ultimately, it comes down to preference.

<strong>CodeKit</strong>

I can’t even begin to explain how much I love <a href="https://incident57.com/codekit/">CodeKit</a>. It compiles my LESS to wherever I want it to, concatenates JavaScript files based on a file input, checks syntax, and does a ton of other stuff that I never even use.

One caveat is that it is Mac-only. A ton of alternatives are available, such as <a href="https://mixture.io/">Mixture</a>, <span class="removed_link" title="https://compass.handlino.com/">Compass</span> and <span class="removed_link" title="https://fireapp.handlino.com/">Fire.app</span>, but none that I know of with the feature set of CodeKit.

<strong>Snippets</strong>

I don’t know if I’m alone on this, but I’ve never found snippets to be particularly useful. Most things need to be customized so much that just writing them out from scratch would be easier. There are only two snippets that I use, but I use them so much that they have <strong>saved me at least a hundred hours by now</strong>. The two snippets are for printing a variable and outputting a long comment:

<pre><code class="language-php">
// Printing a variable:
echo '&lt;pre&gt;';
print_r();
echo '&lt;/pre&gt;';

// A long comment:
/*********************************************/
/*         This is a section of code.         */
/*********************************************/
</code></pre>

I’ve set this up in Coda 2, but you can use <a href="https://smilesoftware.com/TextExpander/index.html">TextExpander</a> and various other apps.

<strong>Thumbnail Regeneration</strong>

As you code, you might find that you need a different-sized image somewhere or that the design requirements have changed. In the former case, you should generate an image with the exact dimensions you need to conserve bandwidth. You can do so with the <code>add_image_size()</code> function, although images would not be processed retroactively.

I use the excellent <a href="https://wordpress.org/extend/plugins/regenerate-thumbnails/">Regenerate Thumbnails</a> plugin to address this problem. I’ll go into the “Media” section and regenerate thumbnails for a single media item, or the plugin can batch process them all. It might take a while if you have a lot of images, but it’s completely set-and-forget — you can just keep on working.

<strong>Switching Users</strong>

You’ll need to test different accounts to make sure users see only what they’re supposed to see, especially if you have role-specific functionality. <a href="https://lud.icro.us/wordpress-plugin-user-switching">User Switching</a> is a godsend, enabling you to switch back and forth between accounts with a single click.

<strong>Template Hierarchy</strong>

The “<a href="https://codex.wordpress.org/Template_Hierarchy">Template Hierarchy</a>” — and especially the diagram a bit further down on that page in the Codex — will help you to remember all of the pages you need to create. Are you sure you haven’t forgotten the <code>404.php</code> page? Have you created a separate <code>attachment.php</code> file for single attachment display? Never forget a file again with this handy chart!

<strong>Browser Development Tools</strong>

Learning how to use your browser’s development tools will make your life a lot easier. Being able to go into the DOM and look up styles will make fixing CSS problems a breeze. Going into the “Network” tab and looking at the AJAX response will help you debug AJAX calls in seconds, and using the features of the JavaScript debugger (such as break points) will help with JavaScript debugging.

<strong>WordPress Knowledge</strong>

Being able to perform complex tasks using database queries is a <em>huge</em> help. If you’ve created 200 test posts and want to delete all whose titles have two instances of the word “or,” that’s easy if you know how to query and manipulate data.

It also helps with “Oh, there’s a function for that?!” syndrome, which kicks in after you’ve spent an hour coding something, only to discover that WordPress has a function for it. Some examples are the <a href="https://codex.wordpress.org/Function_Reference/wp_mail"><code>wp_mail()</code></a> function, which lets you send email easily, the <code>wpautop()</code> function, which adds paragraph tags to text, and the <a href="https://codex.wordpress.org/Function_Reference/human_time_diff"><code>human_time_diff()</code></a> function, which formats dates into the “5 minutes ago” format.

Before attempting to code a small feature, I always search for it, just in case. Before coding a big feature, I search GitHub and other places to see whether anyone has done it before. Perhaps there is a cut-and-pasteable class or something similar.</p>

## Final Testing

Once you’re done, you realize you’re never done. There’s always that one last bug, that one feature that doesn’t work in IE 9, and other similar annoyances. To minimize bugs and maximize your sanity, try the tricks and tools below.</p>

### WordPress Theme Check

<a href="https://wordpress.org/extend/plugins/theme-check/">WordPress Theme Check</a> (maintained by WordPress’ own developers) is an extremely useful tool for ensuring that your theme is up to spec. The first thing Theme Forest does when you submit a theme is run this thing on it, and they will mercilessly reject your theme if they see errors.

The tool checks for legacy functions, incorrect text domains, hidden files, required functions and attributes, and much more. Using this plugin is the easiest way to make sure your theme is 100% WordPress-compliant.</p>

### CloudApp and FluffyApp

<a href="https://getcloudapp.com/">CloudApp</a> is a service that enables you to easily upload files. The reason I love it so is that it comes with a little app that can be configured to play nice with my screenshot-making procedure. On the Mac, I just press <code>Shift + Control + Command + 4</code> to take a screenshot, and then immediately press <code>Control + Option + C</code> (this shortcut can be reconfigured) and wait for the “ping,” which means the screenshot has been uploaded. A link to the screenshot is already in my clipboard, so I can paste it in an email, chat message or issue tracker.

If you’re on Windows, <a href="https://fluffyapp.com/">FluffyApp</a> does exactly the same thing. I’m sure you’ll love it!

### Bug-Management Workflow

I won’t go into particular bug-management tools because there are just so many. I personally use <a href="https://sprint.ly">Sprint.ly</a>, but hundreds of great services are available, such as <a href="https://sifterapp.com/">Sifter</a>, Lighthouse and <a href="https://www.redmine.org/">Redmine</a>.

More important than what you use is <em>how</em> you use it. One policy that has helped my team with our themes is that the person who fixes an issue may never mark it as closed or accepted. This ensures that the issue is properly tested and approved by someone who is able to see it more objectively.</p>

### Version-Control Methodology

Our version-control system gives us two other benefits. We make sure to commit after every bug is fixed; this enables us to keep track of repository changes much more easily. It also means we can roll back versions much more accurately and selectively.

We’ve tied our bug-management system to our version-control system, so that whenever we commit a change, we can close the issue right from the command line by typing, say, <code>Fixes #32</code>. This works in <a href="https://sprint.ly">Sprint.ly</a> and <a href="https://sifter.com">Sifter</a> for sure.</p>

### Good Documentation

While documentation might not seem directly related to testing, it is an excellent way to test a website. By writing documentation, you force yourself to go through the website’s features and make sure they work.

We found an astounding <a href="https://revaxarts-themes.com/documenter/">documentation generator</a>, which we use with all of our themes now. Aside from helping us write the documentation, it generates a beautiful format with no additional work on our end.</p>

### The More, The Merrier

One of the most important lessons I’ve learned is that <strong>a theme is never bug-free</strong>. If 100 people test the living daylights out of the theme, the 101st person (probably the first buyer) will find a bug on launch day. That’s just how it is.

You can minimize this and ensure that bugs are at least restricted to fringe cases by loosing as many people on your theme as possible. We’re all different, which means we use things differently and will find different bugs.

Another major benefit of this — one that I cannot stress enough — is that it allows for user experience testing. If only the people you work with have tested the theme, chances are you’ve missed something because you all think alike. A dropdown button might be dead obvious to all of you, but baffling to a regular user.

A great way to improve your theme is to actually sit and <strong>watch as people test your theme</strong>. I’ve made more changes than I can remember as a result of stupid things that have come up during testing — and I mean not that the people were stupid, but that I was stupid for designing those things the way I did. Remember, there is no such thing as a bad user, just a badly designed tool.</p>

### Make a Video Presentation

This sounds even weirder than documentation-based testing, doesn’t it? But I’ve found that making a presentation video about a theme is a great way to <strong>catch little things</strong>. Knowing that the first thing people will see is the video inadvertently forces you to get hung up on the tiniest problems.

The general routine for me here is that I’ll get 2 minutes into making the video, let out a huge sigh, stop the recording and go and fix something. I’ll then restart from scratch, get to 2 minutes and 15 seconds, and it all starts over.

The best method for me is to restart from the beginning after having stopped. I could instead just pause and resume, but when I start from scratch I’ll sometimes take a different approach, which uncovers more discrepancies and bugs.</p>

## Conclusion

I hope these tips have been helpful and that at least some of them are new to you. I think everyone does a lot of little things we could all learn from. I probably do 50 more useful things that I don’t even notice I’m doing.

I’d love to hear what you do to test both the quality and speed of your themes, so please share in the comments below!

### Further Reading

*   [How To Get The Most Out Of A Premium WordPress Theme](https://www.smashingmagazine.com/2013/02/08/get-the-best-out-of-premium-wordpress-theme/)
*   [How To Improve And Refine Your WordPress Theme Development Process](https://www.smashingmagazine.com/2013/02/21/wp-theme-development-process/)
*   [WordPress Essentials: The Definitive Guide To WordPress Hooks](https://www.smashingmagazine.com/2011/10/07/definitive-guide-wordpress-hooks/)

{{< signature "al" >}}

