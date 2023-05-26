---
title: Getting Started With bbPress
slug: getting-started-with-bbpress
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61422c55-dd39-4d79-9f43-454e2bd29469/bb-press-illu.jpg'
date: 2011-11-15T15:55:25.000Z
author: thord-daniel-hedengren
description: >-
  Forums have been around forever, so it should come as no surprise that several
  plugins for the popular publishing platform WordPress provide this feature, as
  well as support for integrating other forum software. One project, however,
  has a special place in the WordPress community, and that is bbPress. This is
  the software created by WordPress founder, Matt Mullenweg, as a lightweight
  system for the Wordpress.org support forums. In true open-source fashion, the
  bbPress project was born (at [bbpress.org](https://bbpress.org), of course) as
  a lightweight standalone alternative for forums.

  [![bbpress-logo](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f4f4524-04cc-4088-8885-47c90431305d/bbpress-logo.png)](https://www.smashingmagazine.com/2011/11/15/getting-started-with-bbpress/)

  The problem is that the project never really kept up the pace; and while the
  WordPress community wanted to use it, and bbPress saw some promising spurts of
  development, it never really caught up to the alternatives. Most of us who
  needed a forum went either with a plugin alternative that integrated perfectly
  or with forum software such as [Vanilla](https://vanillaforums.org).
categories:
  - WordPress
  - Plugins
---
Forums have been around forever, so it should come as no surprise that several plugins for the popular publishing platform WordPress provide this feature, as well as support for integrating other forum software. One project, however, has a special place in the WordPress community, and that is bbPress.

This is the software created by WordPress founder, Matt Mullenweg, as a lightweight system for the Wordpress.org support forums. In true open-source fashion, the bbPress project was born (at <a href="https://bbpress.org">bbpress.org</a>, of course) as a lightweight standalone alternative for forums.

<a href="https://www.smashingmagazine.com/2011/11/15/getting-started-with-bbpress/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f4f4524-04cc-4088-8885-47c90431305d/bbpress-logo.png" alt="bbpress-logo" width="500" height="250" /></a>

The problem is that the project never really kept up the pace; and while the WordPress community wanted to use it, and bbPress saw some promising spurts of development, it never really caught up to the alternatives. Most of us who needed a forum went either with a plugin alternative that integrated perfectly or with forum software such as <a href="https://vanillaforums.org">Vanilla</a>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">A Beginner’s Guide To Creating A WordPress Website</span>](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)
*   [How To Create Tabs On WordPress Settings Pages](https://www.smashingmagazine.com/2011/10/create-tabs-wordpress-settings-pages/)
*   [How To Contribute To WordPress](https://www.smashingmagazine.com/2013/05/contributing-to-wordpress/)
*   [Diary Of A WordCamp](https://www.smashingmagazine.com/2012/05/diary-of-a-wordcamp/)

{{% feature-panel %}}

The Facebook-inspired community plugin <a href="https://buddypress.org">BuddyPress</a> changed all that. BuddyPress, which adds groups and other membership functionality to a blog, started to ship with bbPress integrated in it. Perhaps unknowingly, some WordPress bloggers who had community features powered by BuddyPress were actually running a version of bbPress, which is enabled in the BuddyPress interface. It worked — and continues to work — great actually; because although bbPress, as standalone forum software, is way behind the competition in terms of features, sometimes all you need is a lightweight alternative, which was the idea behind bbPress all along.

bbPress 2.0 changed it all again, because bbPress has now been officially reborn as a plugin for WordPress, something that had been in the works for quite some time. This is where we stand today, with a fresh release of the first version of the bbPress plugin. In the coming weeks (or right now, depending on when you’re reading this), the plugin will get proper documentation and more support for cool functionality. That shouldn’t stop you from giving it a go right away, because getting started and taking advantage of its core functionality is easy enough.

Before we move on, we need to clear up some nomenclature:

*   bbPress is a plugin for WordPress, and is sometimes referred to as bbPress 2.0 for clarity.
*   bbPress 1.0 is a standalone forum that integrates with WordPress (and the BuddyPress plugin) but does not reside in WordPress’ core.
*   BuddyPress is a separate plugin for WordPress that integrates with the bbPress plugin.
*   BuddyPress still ships with bbPress, but you can connect to your bbPress plugin forums if you want to.

Yes, it’s all a bit messy.</p>

## Getting bbPress Up And Running

Installing bbPress is easy, because it’s available <a href="https://wordpress.org/extend/plugins/bbpress/">in Wordpress’ plugin directory</a>. Either install it from within WordPress, using the “Add new plugin” feature, or via FTP if you prefer to (or must) upload plugins. Then, activate the plugin, and you’re all set!

Well, not quite. You’ll want to look at some settings before starting to use the forums.

<img class="aligncenter size-full wp-image-98403" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd73b93f-93e3-47a7-a3a7-a7ca908625a6/sm-bbpress-settings.png" alt="" width="550" height="441" /><br>
<em>bbPress settings.</em>

You’ll notice a new “Forums” menu under “Settings” in the admin area, along with the brand new sections “Forums,” “Topics” and “Replies,” all sporting bee-inspired icons.

Let’s look at the “Forums” settings pane first, shown above. Here you have an assortment of settings for your forums, such as whether to allow anonymous posts, how long posters should be able to edit their posts, and how many topics to show per page.

The “Archive” and “Single Slugs” settings are important. These define the URLs of your forums, the posts, and the tags for posts. Choose something that fits your set-up; if you’re running an English-language website, then the default settings will probably do, but you can fine tune to your needs. Remember to go to Settings → Permalinks after making any change to the slugs, and rebuild the permalink structure by clicking the “Save Changes” button on that page. If you ever have problems viewing the forums, give this a shot because it might be an issue with the permalinks, and rebuilding them might help. Also, make sure to press the “Save” button in Settings → Forums.

Where are your forums, then? Well, you’ll already know that from the Settings → Forums page, because they are located at the base slug assigned for the forums. By default, it would be <code>forums</code>, so you’d find them at <code>yourdomain.com/forums/</code>. Do yourself a favor and use pretty permalinks, because although bbPress will work without them, the URLs will look so much better if they’re pretty. That Google will thank you is just a bonus (note: an actual thank-you from Google is not guaranteed).

<img class="aligncenter size-full wp-image-98402" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b08a97f-0cfd-4236-8f94-54fd26596070/sm-bbpress-noforums.png" alt="" width="550" height="348" /><br>
<em>The forums page, without any forums unfortunately.</em>

There we go: all set up and ready to go. Too bad there aren’t any forums, nor posts… yet!

## Managing bbPress Forums

Getting bbPress set up and ready to go is a breeze, but if you actually want some action in your brand new forums, then you’ll need to create a forum. This is easily done under “Forums” in the admin area. Just click “New Forum,” and you’ll get a familiar-looking screen to create a forum.

<img class="aligncenter size-full wp-image-98398" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6aec653-481a-43af-a179-68a15f512682/sm-bbpress-createforum.png" alt="" width="550" height="251" /><br>
<em>Create a forum.</em>

This is pretty self-explanatory. The one thing you’ll need to be careful with is the box in the top-right corner. These are the settings that enable you to control whether a forum is open or closed, whether it is a forum or a category, and who should see it. When you have created multiple forums, the “Parent” and “Order” options will show up, allowing you to nest forums (much like “Pages”) and sort them (also like Pages).

To make a long story short, with a few forums created, users will soon be able to post in your forums. Depending on your settings, they may need to sign up, but that’s a different matter and depends on what kind of website you’re running.

<img class="aligncenter size-full wp-image-98400" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06e035d7-ec5e-4710-9244-a64fc5b8e176/sm-bbpress-forums.png" alt="" width="550" height="277" /><br>
<em>A forums page.</em>

Managing “topics,” which are new posts, and “replies,” which are replies to topics, is easy enough. These show up under their respective sections in the WordPress admin area, and they behave much like posts and comments. That’s no surprise because bbPress has the same model as standard posts and Pages, using custom post types. This will also make it easy to style the bbPress forum should you want to, something we’ll look at more closely later.

Finally, one thing to know when running bbPress on a non-English website: localization projects are on GlotPress, and you can get a translation by using the options at the bottom of the entry for your selected language. You’ll need to upload these to the <code>wp-content/plugins/bbpress/bbp-languages/</code> folder, and the file should be called <em>bbpress-sv_SE.mo</em>, where <em>sv_SE</em> should be swapped for your language of choice. Hopefully, we’ll be able to store these files in the <code>wp-content/languages/</code> folder later, but this doesn’t work for me right now.</p>

### Extending bbPress

Although bbPress is now a WordPress plugin and not a standalone system, you’ll find plugins that extend its functionality. Quite a few actually: for displaying the latest posts in widgets, adding signatures and whatnot.

Your starting point for bbPress-related plugins is the <a href="https://bbpress.org/plugins/">plugins section of the bbPress website</a> and, of course, the WordPress plugin directory (<a href="https://wordpress.org/extend/plugins/search.php?q=bbpress">begin with a search</a>).

One thing, though: make sure any plugin you choose is made for bbPress 2.0 (i.e. the plugin version). Older plugins made for the 1.x branch will not work.

## BuddyPress And bbPress

BuddyPress, the plugin that enables you to create your own Facebook-like community on a WordPress website, work just great with bbPress. That should come as no surprise because the plugin still ships with the forum component (bbPress) built in. But this forum component is for enabling forums for your BuddyPress groups. Groups are exactly what they sound like: members can join them, even create their own (depending on your settings), and discuss various topics in them. With forums enabled for groups, every group will get a forum. This is still true with BuddyPress 1.5, despite there being a standalone bbPress plugin now. If you want forums for your BuddyPress-powered groups, then either choose an existing bbPress installation or install one in the BuddyPress settings. And yes, this is a bit confusing.

<img class="aligncenter size-full wp-image-98397" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e67592c-a6a4-4a18-872b-845ea564122a/sm-bbpress-buddypress-forum1.png" alt="" width="550" height="185" /><br>
<em>The settings page for BuddyPress forums.</em>

With bbPress 2.0 and the shift from standalone forum software to WordPress plugin, you can rest assured that BuddyPress and bbPress still work well enough together. The option for installing forums site-wide is on the settings page for the BuddyPress forum, and it actually installs the bbPress plugin, rather than rely on the built-in forum component in the BuddyPress plugin. BuddyPress and the bbPress plugin integrate nicely out of the box, but not for group forums. Instead, your posts in the forums will show up in the BuddyPress activity stream; surely we’ll see some cool plugins in the future that leverage both BuddyPress and the bbPress plugin, tying the two even closer together.

All in all, there is no reason not to combine bbPress with BuddyPress if you need more community features than just a forum on your website.</p>

## Making bbPress Look Good

While your forums will work well out of the box, as you no doubt have gathered from the screenshots earlier in this article, you might want to make bbPress better suit the look of your website. You’ve already seen the default styles of bbPress, which you can tweak easily enough: just add CSS to your theme’s style sheet!

Doing this is easy: just inspect the code of the forums with your favorite Web inspector (such as <a href="https://getfirebug.com/">Firebug</a> or the built-in inspector in Chrome or Safari), and find the classes that you’ll need to style the forums.

<img class="aligncenter size-full wp-image-98401" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75d67eb2-3d0c-429f-a34a-58d5fe7052a5/sm-bbpress-markup.png" alt="" width="550" height="284" /><br>
<em>The <code>ul.bbp-forums</code> class gives you control.</em>

If you want more control, perhaps to break from the default layout of the forums, you can add additional template files to your WordPress theme. The bbPress plugin is already compatible with <a href="https://wordpress.org/extend/themes/twentyten">Twenty Ten</a>, the previous default theme. In the <code>bbpress</code> folder, look at the files in <code>bbp-themes/bbp-twentyten/</code> and you’ll get an idea what you can do. Simply changing the theme to Twenty Ten (instead of Twenty Eleven, which was shown earlier in this article) will give us something different and more attuned to our theme.

<img class="aligncenter size-full wp-image-98405" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c69fa32-3502-4c80-83f3-254cfabf0c54/sm-bbpress-twentyten.png" alt="" width="550" height="376" /><br>
<em>We get a different look when using Twenty Ten.</em>

How you style the forums will depend on how much you want to deviate from the default look and feel. If everything is where it should be, then you’ll be able to make the forums looks good and fit your theme just by adding styles to your theme’s style sheet. But if you want to move things around a lot, then you’ll probably have to create your own template files. Consult the files in the <code>bbpress/bbp-themes/bbp-twentyten/</code> folder to get an idea of what can be done, while we wait for bbPress to publish proper documentation. Because forums are really just a custom post type, you’ll likely be able to find your way around if you’ve worked with them before.</p>

## Three Websites That Use bbPress

Want to see some bbPress forums in action, other than bbPress.org itself or Twenty Ten and Twenty Eleven themes with the plugin activated?

### Wordpress.org

<img class="aligncenter size-full wp-image-98404" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3d18e2e-75aa-47ca-a5ab-214ba7973c8d/sm-bbpress-show-wordpress-org.png" alt="" width="550" height="284" /><br>
<em><a href="https://wordpress.org/support/">WordPress Forums</a></em>

While using bbPress on Wordpress.org might not exactly qualify as eating one’s own dog food, this is where it started after all.</p>

### Dropbox

<img class="aligncenter size-full wp-image-98399" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38bd9f62-c9b1-4cb2-8254-1640e8566d47/sm-bbpress-dropbox.png" alt="" width="550" height="284" /><br>
<em><a href="https://forums.dropbox.com">Dropbox Forums</a></em>

The syncing service Dropbox has been using bbPress forums for quite some time, with a pretty simple, standard look. This is just the standalone version, and it shows that bbPress is ready for prime time.</p>

### WPCandy

<img class="aligncenter size-full wp-image-98406" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8578f56-c34c-4bb8-ab89-663663b4cca6/sm-wpcandy.png" alt="" width="550" height="284" /><br>
<em><a href="https://wpcandy.com/discussions">Discussions on WPCandy</a></em>

The forums section of WPCandy is a great example of how bbPress can be easily integrated in an existing WordPress theme.</p>

## What’s Next?

Personally, I’m thrilled to see bbPress become a WordPress plugin. We’ve seen plugins that add forum features to WordPress in the past, but I haven’t been comfortable running any of them, to be honest. Whenever I’ve needed forums, I’ve used software such as the excellent Vanilla. Some people have suggested the BuddyPress plugin, but that’s a bit much if all you need is a simple forum for discussions.

With bbPress 2.0, this isn’t an issue anymore, and although documentation isn’t available yet, getting started is easy enough. You’ll probably want to add features to your forums, and that’s easy with additional plugins. And because bbPress is really just a custom post type for your WordPress website, using actual registered users, you can use existing plugins to achieve things such as moderator privileges and whatnot. We can anticipate a boom of bbPress-compatible plugins in the near future that will make our forums even better and more interesting.

For now, let’s play with what we have, which is usually more than enough.

{{< signature "al" >}}

