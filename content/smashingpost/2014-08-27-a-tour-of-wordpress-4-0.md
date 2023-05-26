---
title: A Quick Tour Of WordPress 4.0
slug: a-tour-of-wordpress-4-0
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f066c6f-4ff5-49a6-b047-b5c343f63f3a/wordpress-media-grid-opt.jpg
date: 2014-08-27T20:32:45.000Z
author: daniel-pataki
description: >-
  Today, WordPress has released the first [release
  candidate](https://wordpress.org/news/2014/08/wordpress-4-0-release-candidate/)
  (RC) for the upcoming 4.0 version. According to the official [version
  numbering](https://make.wordpress.org/core/handbook/how-the-release-cycle-works/version-numbering/),
  WordPress 4.0 is no more or less significant than 3.9 was or 4.1 will be. That
  being said, a new major release is always a cause for excitement! Let's take a
  look at the new features the team at WordPress has been working on for us.

  Since I've always used WordPress in English, it took me a while to realize how
  important internationalization is. [29% of all WordPress.com
  installations](https://en.wordpress.com/stats/) use a non-English language
  which is _huge_ and not that far from a quarter of all installations. Version
  4.0 makes it much easier to get WordPress to speak your language. In fact, the
  first installation screen asks you to choose your native tongue. Nice!
categories:
  - WordPress
  - Tools
  - Plugins
  - Optimization
  - Techniques (WP)
---
Today, WordPress has released the first <a href="https://wordpress.org/news/2014/08/wordpress-4-0-release-candidate/">release candidate</a> (RC) for the upcoming 4.0 version. According to the official <a href="https://make.wordpress.org/core/handbook/how-the-release-cycle-works/version-numbering/">version numbering</a>, WordPress 4.0 is no more or less significant than 3.9 was or 4.1 will be. That being said, a new major release is always a cause for excitement! Let's take a look at the new features the team at WordPress has been working on for us.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Secrets Of High-Traffic WordPress Blogs](https://www.smashingmagazine.com/2012/09/secrets-high-traffic-wordpress-blogs/)
*   [<span class="headline">Do-It-Yourself Caching Methods With WordPress</span>](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)

## Installation Language

Since I've always used WordPress in English, it took me a while to realize how important internationalization is. <a href="https://en.wordpress.com/stats/">29% of all WordPress.com installations</a> use a non-English language which is <em>huge</em> and not that far from more than a quarter of all installations. Version 4.0 makes it much easier to get WordPress to speak your language. In fact, the first installation screen asks you to choose your native tongue. Nice!

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bd82cea-48e0-4667-8054-8cdc5464f669/language-selector-opt.png" alt="language-selector-opt" width="394" height="524" /></figure>

This is a big step up from either having to download in your own language, or grabbing language files manually and modifying the config.</p>

## Embed Previews For URLs

Embedding content into posts has also become a much nicer process. One of my irks with the visual editor used to be that it wasn't visual enough. Not that long ago, you just got a grey box in place of a gallery or other media/embed items. The "Smith" release took care of galleries and 4.0 is taking care of a host of other items. If you paste a YouTube URL in text mode, it will render as a video in visual mode. How handy is that?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/663b4f22-50bf-4812-bc59-30f275e432e9/embedding-urls-opt-500x477.png" alt="embedding-urls-opt" width="500" height="477" /></figure>

I find this a lot more pleasing to work with — I see exactly what I'm going to get. The media modal's insert from the URL feature is getting the same upgrade. As soon as you've entered a URL, the video will load — playable and all! The good news is that it works with all the services you'd expect, from Vimeo to Twitter, Hulu and Flickr. Scott Taylor (who is a core contributor working on this) has kindly gathered some test URLs. I recommend checking out <a href="https://core.trac.wordpress.org/ticket/28195#trac-change-15-1401220623215447">Trac ticket</a> to find out more in this regard.</p>

## Media Section Grid

The media section now has a grid view by default. This isn't a groundbreaking coding feat by any measure, but it does introduce a sleeker UI which is perhaps a glimpse of what is coming up in the future.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f066c6f-4ff5-49a6-b047-b5c343f63f3a/wordpress-media-grid-opt.jpg" alt="media-grid-opt" width="500" height="382" /></figure>

While this is a minor change, it does give you a way better overview of your media files than the default view of 20 images in a list.</p>

## Plugin Discovery And Installation

In my opinion, the plugin "Add New" page got a much needed makeover. The top navigation looks a lot like the new navigation in the media section — another indication of a slightly more modern interface creeping into the system. Plugins in the list view are displayed in a much more visual fashion, and it looks like it's time for developers to start making thumbnails! While the plugin details screen could use a makeover as well, I'm sure this is a work in progress and will be explored further.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd316cb8-5c73-4bfe-80f4-13bdbbba6a19/jetpack-plugin-opt-500x224.png" alt="Jetpack-Plugin-opt" width="500" height="224" /></figure>

## Better Post Editing

One feature I'm particularly happy with is how the editor height has been changed to use screen real estate better. Mark Jaquith <a href="https://core.trac.wordpress.org/ticket/28328">painted a great picture</a> of the problem:
<blockquote>"The post editor feels like it has been relegated to a box of medium importance on the edit/compose screen."</blockquote>

## UI Improvements For Widget Customization

It's great that widgets have been included in the theme customizer. Usually, if you had more than five to six widgets, things became a bit too crowded. Fortunately, the new WP version has now put all widgets into a sub-section of the customization screen. This essentially minimizes them when not needed — a welcome UI improvement for sure!

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff540f1-14ce-4c53-995e-ee6bdc0f3a4b/widgets-in-customizer-opt.png" alt="Widgets-in-Customizer-opt" width="301" height="263" /></figure>

## Join The Fun

As always, the latest development versions can be tried out pretty easily. By installing the <a href="https://wordpress.org/plugins/wordpress-beta-tester/">WordPress Beta Tester</a> plugin you can update to the latest beta builds or nightlies and play around with the brand new features.

If you happen to find any bugs, you can add them to the <a href="https://core.trac.wordpress.org/">WordPress Trac</a> and you can even fix them and contribute to the core! WordPress is a community project, and every little bit helps!

## Conclusion

While I agree that WordPress 4.0 isn't the same leap as 3.0 was, I disagree with this being a problem. Instead of adding more and more features, the team is consolidating existing features and working hard to bring us a better user experience.

The features above will actually affect how I use the day-to-day features of WordPress in a positive way. While I may not be able to post from my Google Glass (partly because I don't have one), the ability to use WordPress better is far more important.

{{< signature "il" >}}

&nbsp;

