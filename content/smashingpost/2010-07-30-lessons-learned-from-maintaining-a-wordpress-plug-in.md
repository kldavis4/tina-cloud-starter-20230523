---
title: Lessons Learned From Maintaining A WordPress Plugin
slug: lessons-learned-from-maintaining-a-wordpress-plug-in
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278956f7-956a-4bfc-b852-f26748ca01d0/wordpress-17.gif
date: 2010-07-30T15:04:28.000Z
author: joost-de-valk
description: >-
  Recently I released a WordPress plugin for Google Analytics that adds a tracking code and dozens of various pieces of meta data to blogs. Since the release of version 4, I've updated it 6 times, to the point where it's now at version 4.0.6\. In this article I would like to share with you my experiences in maintaining this and other WordPress plug-ins and common good practices that I've distilled from that work.
categories:
  - WordPress
  - Plugins
  - Maintenance
---
The updates that I released had a couple of purposes, ranging from bug fixes to new features and fixes in documentation. While all of these are nice to talk about, the bug fixes are the ones you'll learn the most from, so let's start by going through these.

## Website and Account Configuration

Almost as soon as I released the plugin, people who updated were telling me that it worked wonderfully, and others were telling me that it didn't work for them. Turns out I hadn't tested the plugin with a Google Analytics account that has only one website registered; I expected the websites to be an array. Fixing this bug was easy, but determining that this was the problem took a while.

{{% feature-panel %}}

Being able to log into a few hosts of people who gave me access to their back end <em>and</em> FTP so that I could test my fix proved invaluable. This enabled me to release 4.0.1 within an hour of the 4.0 release.

Another mistake I made was forcing everyone to reconfigure the plugin. I assumed it wouldn't be too much work for people, and it wanted to be sure the settings were clean, but it turns out quite a few people didn't want to reconfigure. With 4.0.2, I came up with a way to inherit some of the settings and clean up the mess I made, and in 4.0.4 I made a change that I will add to all of my plugins:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43107acb-092d-48cf-a70b-1d28d9979515/re-authenticate.png"><img loading="lazy" decoding="async" class="size-medium wp-image-54976" title="re-authenticate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07f2f88b-deb8-4852-a780-988c2b3fa58f/analytics1.png" alt="" width="500" height="310" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43107acb-092d-48cf-a70b-1d28d9979515/re-authenticate.png">Large view</a></em>

<strong>Good practice #1:</strong> Don't assume <em>anything</em> about people's websites and external accounts.</p>

### Versioning Option Arrays

As a seasoned WordPress developer, I store all of the options for my plugin in one option in the database, which is basically a big array. Why I hadn't ever added a version number to these options is a mystery to me. Doing so makes it possible to do some very cool things: I can now add new features and set a default for these new features as soon as a user upgrades; I can show the user different messages based on the version they had before they upgraded; and more.

<strong>Good practice #2:</strong> Add a version number to your option arrays.

I'm still not using the WordPress option API stuff (check out <a href="https://planetozh.com/blog/2009/05/handling-plugins-options-in-wordpress-28-with-register_setting/">this post</a> by Ozh to learn all about it), which I probably should, but for now I find it easier to handle the saving and validation of options myself.</p>

### Don't Release Too Soon

If you've got a bug that's bugging a lot of your plugin's users, you'll probably want to release a bug fix as soon as possible. I know I do. This caused an issue with my 4.0.3 release, though, because I didn't properly test some of the code I introduced, causing me to have to release 4.0.4 just two hours later to fix a stupid mistake I'd made with booleans. Nothing is as painful as 500 people downloading a version of your plugin that doesn't actually work.

<strong>Good practice #3:</strong> Test, test, test before you release, even when you're in a hurry.

### Know Which Version People Are On

Over the past two weeks, I've been helping several people who <em>said</em> they were on the latest version of my plugin but in fact were not. To remedy this, I've started outputting the version number in the comment that the plugin outputs before the tracking code. Problem is, if people run a plugin such as <a href="https://wordpress.org/extend/plugins/w3-total-cache/">W3 Total Cache</a> (which everyone should use by the way) or anything else that minifies their output, that comment will get lost.

There's a solution for that, too: I'd already wrapped the script in <code>&lt;CDATA&gt;</code> tags, to help with Strict XHTML validation. Minifying will not occur within those CDATA tags, so I moved my "branding" comment to the CDATA section, and I can now always see, first, that my plugin is active and, secondly, which version of the plugin they're using.

<strong>Good practice #4:</strong> Make sure you can see which version of your plugin people are running.</p>

### URLs in WordPress

One of these things that can generate pretty awful bugs is a blog's URL. Whether it's due to people running their entire blog on <code>https</code> or "simply" running their blog in a sub-directory, it can cause headaches. It did for me in version 4.0.2 when I added URL sanitization: all relative URLs in posts and text widgets starting with a <code>/</code> were made absolute, in order to properly track these URLs. Tiny issue: I forgot about blogs in sub-directories, so a tiny portion of people would end up with links that used to go to <code>/home</code> but that now went to <code>https://example.com/blog/home</code>. I know, that was stupid; but that's why I'm telling you: so you don't make the same mistake.

<strong>Good practice #5:</strong> Make sure all URLs you use will work in <em>all</em> circumstances, whether WordPress is in a sub-directory, on a subdomain or just in the root.</p>

### Writing to the Root Directory

Somewhat related to the last issue, although I encountered this while developing my WordPress SEO plugin, not the Google Analytics plugin: if you write a file — say, an XML site map file — to the root of a website, and the website is actually a WordPress multi-site installation, things can go horribly wrong.

Check out the following scenario:

1.  User 1 writes and publishes a post on `example.com/blog-1/`.
2.  An updated XML site map for `example.com/blog-1/` is generated, and `example.com/sitemap.xml` is updated.
3.  User 2 writes and publishes a post on `example.com/blog-2/`.
4.  An updated XML site map for `example.com/blog-2/` is generated and `example.com/sitemap.xml` is overwritten.

See what just happened? The XML site map now contains only the posts from <code>blog-2…</code> This is exactly why the <em>wp-content</em> directory was created. There's hardly ever a need to put a file in the root of an installation, and by not doing so, you make it far easier to run your plugin in a multi-site/WordPress MU environment.

<strong>Good practice #6:</strong> If you're generating files, generate them in the <em>wp-content</em> directory of your blog. Do <em>not</em> write files to the root directory unless you absolutely, positively have to. And if you do have to do it, make sure it doesn't go wrong when your plugin is active on multiple blogs in the same multi-site instance.</p>

### Rethink Your Filters

On the day that I released 4.0, I got quite a few feature requests, ranging from very simple to somewhat more complex. One that came in quite rapidly and caught my eye happened to be quite simple: the user wanted the same outbound link that in my plugin tracks the content of an article to track in text widgets. Because I don't use text widgets that much, it never occurred to me to do this. It was a valuable lesson, though:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61c79087-df80-4115-8990-82d82e9d8d92/conversation.png"><img loading="lazy" decoding="async" class="size-medium wp-image-54977" title="feature request" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ddda0db-c108-43ff-915c-ce74b35a6517/excitign.png" alt="feature request" width="500" height="374" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61c79087-df80-4115-8990-82d82e9d8d92/conversation.png">Large view</a></em>

<strong>Good practice #7:</strong> If you're filtering content, try to filter it in as many places as you can, so that users get consistent results all over WordPress.</p>

## Never Assume

It's true for everything, I guess, but especially true for WordPress developers: never assume. The seven best practices above mostly boil down to abandoning all assumptions about states, URLs and locations, and even about people knowing which version of a plugin they're using. Take all these matters into your own hands; your plugin will be the better for it!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [WordPress Essentials: How To Create A WordPress Plugin](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/)
*   [How To Deploy WordPress Plugins With GitHub Using Transients](https://www.smashingmagazine.com/2015/08/deploy-wordpress-plugins-with-github-using-transients/)
*   [How To Use Autoloading And A Plugin Container In WordPress Plugins](https://www.smashingmagazine.com/2015/05/how-to-use-autoloading-and-a-plugin-container-in-wordpress-plugins/)
*   [How Commercial Plugin Developers Are Using The WordPress Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)

{{< signature "al" >}}

