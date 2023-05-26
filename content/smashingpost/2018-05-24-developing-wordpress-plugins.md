---
title: 'Lessons Learned While Developing WordPress Plugins'
slug: developing-wordpress-plugins
author: jakub-mikita
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b13115d5-6c5c-4c46-8b32-8458b9f6ad5f/lessons-learned-while-developing-wordpress-plugins.png
date: 2018-05-24T13:30:28+02:00
summary: >-
  Good plugin development and support lead to more downloads. More downloads mean more money and a better reputation. Read on to learn how you can develop good-quality products with these seven golden rules.
description: >-
  Good plugin development and support lead to more downloads. More downloads mean more money and a better reputation. Read on to learn how you can develop good-quality products with these seven golden rules.
categories:
  - Plugins
  - WordPress
---
<p>Every WordPress plugin developer struggles with tough problems and code that’s difficult to maintain. We spend late nights supporting our users and tear out our hair when an upgrade breaks our plugin. Let me show you how to make it easier.</p>

<p>In this article, I’ll share my five years of experience developing WordPress plugins. The first plugin I wrote was a simple marketing plugin. It displayed a call to action (CTA) button with Google’s search phrase. Since then, I’ve written <a href="https://profiles.wordpress.org/kubitomakita#content-plugins">another 11 free plugins</a>, and I maintain almost all of them. I’ve written around 40 plugins for my clients, from really small ones to one that have been maintained for over a year now.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Measuring Performance With Heatmaps</h4>
<p>Heatmaps can show you the exact spots that receive the most engagement on a given page. Find out why they’re so efficient for your marketing goals and how they can be integrated with your WordPress site. <a href="https://deploy-preview-3132--smashing-prod.netlify.com/2018/03/heatmaps-track-links-wordpress/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

<p>Good development and support lead to more downloads. More downloads mean more money and a better reputation. This article will show you the lessons I’ve learned and the mistakes I’ve made, so that you can improve your plugin development.</p>

{{% feature-panel %}}

## 1. Solve A Problem

<p>If your plugin doesn’t solve a problem, it won’t get downloaded. It’s as simple as that.</p>

<p>Take the <a href="https://wordpress.org/plugins/advanced-cron-manager/">Advanced Cron Manager</a> plugin (8,000+ active installations). It helps WordPress users who are having a hard time debugging their cron. The plugin was written out of a need &mdash; I needed something to help myself. I didn’t need to market this one, because people already needed it. It scratched their itch.</p>

<p>On the other hand, there’s the <a href="https://wordpress.org/plugins/insector/">Bug &mdash; fly on the screen</a> plugin (70+ active installations). It randomly simulates a fly on the screen. It doesn’t really solve a problem, so it’s not going to have a huge audience. It was a fun plugin to develop, though.</p>

<p>Focus on a problem. When people don’t see their SEO performing well, they install an SEO plugin. When people want to speed up their website, they install a caching plugin. When people can’t find a solution to their problem, then they find a developer who writes a solution for them.</p>

<p>As David Hehenberger attests in his <a href="https://fatcatapps.com/plugin-success/">article about writing a successful plugin</a>, need is a key factor in the WordPress user’s decision of whether to install a particular plugin.</p>

<p>If you have an opportunity to solve someone’s problem, take a chance.</p>

## 2. Support Your Product

<blockquote>“3 out of 5 Americans would try a new brand or company for a better service experience. 7 out of 10 said they were willing to spend more with companies they believe provide excellent service.”<br /><br />&mdash; Nykki Yeager</blockquote>

<p>Don’t neglect your support. Don’t treat it like a must, but more like an opportunity.</p>

<p>Good-quality support is critical in order for your plugin to grow. Even a plugin with the best code will get some support tickets. The more people who use your plugin, the more tickets you’ll get. A better user experience will get you fewer tickets, but you will never reach inbox 0.</p>

<p>Every time someone posts a message in a support forum, I get an email notification immediately, and I respond as soon as I can. It pays off. The vast majority of my good reviews were earned because of the support. This is a side effect: Good support often translates to 5-star reviews.</p>

<p>When you provide excellent support, people start to trust you and your product. And a plugin is a product, even if it’s completely free and open-source.</p>

<p>Good support is more complex than about writing a short answer once a day. When your plugin gains traction, you’ll get several tickets per day. It’s a lot easier to manage if you’re proactive and answer customers’ questions before they even ask.</p>

<p>Here’s a list of some actions you can take:</p>

<ul>

<li>Create an FAQ section in your repository.</li>

<li>Pin the “Before you ask” thread at the top of your support forum, highlighting the troubleshooting tips and FAQ.</li>

<li>Make sure your plugin is simple to use and that users know what they should do after they install it. UX is important.</li>

<li>Analyze the support questions and fix the pain points. Set up a board where people can vote for the features they want.</li>

<li>Create a video showing how the plugin works, and add it to your plugin’s main page in the WordPress.org repository.</li>

</ul>

<p>It doesn’t really matter what software you use to support your product. The WordPress.org’s official support forum works just as well as email or your own support system. I use WordPress.org’s forum for the free plugins and my own system for the premium plugins.</p>

## 3. Don’t Use Composer

<p>Composer is package-manager software. A repository of packages is hosted on packagist.org, and you can easily download them to your project. It’s like NPM or Bower for PHP. Managing your third-party packages the way Composer does is a good practice, but don’t use it in your WordPress project.</p>

<p>I know, I dropped a bomb. Let me explain.</p>

<p>Composer is great software. I use it myself, but not in public WordPress projects. The problem lies in conflicts. WordPress doesn’t have any global package manager, so each and every plugin has to load dependencies of their own. When two plugins load the same dependency, it causes a fatal error.</p>

<p>There isn’t really an ideal solution to this problem, but Composer makes it worse. You can bundle the dependency in your source manually and always check whether you are safe to load it.</p>

<p>Composer’s issue with WordPress plugins is still not solved, and there won’t be any viable solution to this problem in the near future. The problem was raised many years ago, and, as you can read in <a href="https://wptavern.com/a-narrative-of-using-composer-in-a-wordpress-plugin">WP Tavern’s article</a>, many developers are trying to solve it, without any luck.</p>

<p>The best you can do is to make sure that the conditions and environment are good to run your code.</p>

## 4. Reasonably Support Old PHP Versions

<p>Don’t support very old versions of PHP, like 5.2. The security issues and maintenance aren’t worth it, and you’re not going to earn more installations from those older versions.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b13115d5-6c5c-4c46-8b32-8458b9f6ad5f/lessons-learned-while-developing-wordpress-plugins.png" sizes="100vw" caption="The <a href='https://wordpress.org/plugins/notification/'>Notification</a> plugin’s usage on PHP versions from May 2018. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b13115d5-6c5c-4c46-8b32-8458b9f6ad5f/lessons-learned-while-developing-wordpress-plugins.png'>Large preview</a>)" alt="" >}}

<p>Go with PHP 5.6 as a minimal requirement, even though official support will be <a href="https://php.net/supported-versions.php">dropped by the end of 2018</a>. WordPress itself <a href="https://wordpress.org/about/requirements/">requires PHP 7.2.</a></p>

<p>There’s a movement that <a href="https://deliciousbrains.com/legacy-php-version-support/">discourages support of legacy PHP versions</a>. The Yoast team released the <a href="https://github.com/Yoast/whip">Whip library</a>, which you can include in your plugin and which displays to your users important information about their PHP version and why they should upgrade.</p>

<p>Tell your users which versions you do support, and make sure their website doesn’t break after your plugin is installed on too low a version.</p>

## 5. Focus On Quality Code

<p>Writing good code is tough in the beginning. It takes time to learn the “SOLID” principles and design patterns and to change old coding habits.</p>

<p>It once took me three days to display a simple string in WordPress, when I decided to rewrite one of my plugins using better coding practices. It was frustrating knowing that it should have taken 30 minutes. Switching my mindset was painful but worth it.</p>

<p>Why was it so hard? Because you start writing code that seems at first to be overkill and not very intuitive. I kept asking myself, “Is this really needed?” For example, you have to separate the logic into different classes and make sure each is responsible for a single thing. You also have to separate classes for the translation, custom post type registration, assets management, form handlers, etc. Then, you compose the bigger structures out of the simple small objects. That’s called <a href="https://php-di.org/doc/understanding-di.html#understanding-with-an-example">dependency injection</a>. That’s very different from having “front end” and “admin” classes, where you cram all your code.</p>

<p>The other counterintuitive practice was to keep all actions and filters outside of the constructor method. This way, you’re not invoking any actions while creating the objects, which is very helpful for unit testing. You also have better control over which methods are executed and when. I wish I knew this before I wrote a project with an infinite loop caused by the actions in the constructor methods. Those kinds of bugs are hard to trace and hard to fix. The project had to be refactored.</p>

<p>The above are but a few examples, but you should get to know the <a href="https://www.youtube.com/watch?v=Ib-gxqF6Wuk">SOLID principles</a>. These are valid for any system and any coding language.</p>

<p>When you follow all of the best practices, you reach the point where every new feature just fits in. You don’t have to tweak anything or make any exceptions to the existing code. It’s amazing. Instead of getting more complex, your code just gets more advanced, without losing flexibility.</p>

<p>Also, format your code properly, and make sure every member of your team follows a standard. Standards will make your code predictable and easier to read and test. <a href="https://codex.wordpress.org/WordPress_Coding_Standards">WordPress has its own standards</a>, which you can implement in your projects.</p>

## 6. Test Your Plugin Ahead Of Time

<p>I learned this lesson the hard way. Lack of testing led me to release a new version of a plugin with a fatal error. Twice. Both times, I got a 1-star rating, which I couldn’t turn into a positive review.</p>

<p>You can test manually or automatically. Travis CI is a continuous testing product that integrates with GitHub. I’ve built a <a href="https://github.com/BracketSpace/Notification/blob/develop/.travis.yml">really simple test suite</a> for my Notification plugin that just checks whether the plugin can boot properly on every PHP version. This way, I can be sure the plugin is error-free, and I don’t have to pay much attention to testing it in every environment.</p>

<p>Each automated test takes a fraction of a second. 100 automated tests will take about 10 minutes to complete, whereas manual testing needs about 2 minutes for each case.</p>

<p>The more time you invest in testing your plugin up front, the more it will save you in the long run.</p>

<p>To get started with automated testing, you can use the WP-CLI \\`wp scaffold plugin-test\\` command, which <a href="https://developer.wordpress.org/cli/commands/scaffold/plugin-tests/">installs all of the configuration</a> you need.</p>

## 7. Document Your Work

<p>It’s a cliche that developers don’t like to write documentation. It’s the most boring part of the development process, but a little goes a long way.</p>

<p>Write self-documenting code. Pay attention to variable, function and class names. Don’t make any complicated structures, like cascades that can’t be read easily.</p>

<p>Another way to document code is to use the “doc block”, which is a comment for every file, function and class. If you write how the function works and what it does, it will be so much easier to understand when you need to debug it six months from now. WordPress Coding Standards covers this part by forcing you to write the doc blocks.</p>

<p>Using both techniques will save you the time of writing the documentation, but the code documentation is not going to be read by everyone.</p>

<p>For the end user, you have to write high-quality, short and easy-to-read articles explaining how the system works and how to use it. Videos are even better; many people prefer to watch a short tutorial than read an article. They are not going to look at the code, so make their lives easier. Good documentation also reduces support tickets.</p>

## Conclusion

<p>These seven rules have helped me develop good-quality products, which are starting to be a core business at <a href="https://bracketspace.com">BracketSpace</a>. I hope they’ll help you in your journey with WordPress plugins as well.</p>

<p>Let me know in the comments what your golden development rule is or whether you’ve found any of the above particularly helpful.</p>

{{< signature "il, ra, yk" >}}

