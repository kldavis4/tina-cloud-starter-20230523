---
title: How To Improve Your WordPress Plugin's Readme.txt
slug: improve-wordpress-plugins-readme-txt
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d09fcde-2d46-45f1-9ff2-cb3c3c2b61e4/wordpress-grudge.jpg
date: 2011-11-23T15:52:44.000Z
author: siobhan-mckeown
description: >-
  If you’re a plugin developer and you just love to write code, then writing a
  _readme.txt_ file for a plugin in WordPress’ repository might be your idea of
  hell. When you’ve written all of that lovely code, why must you spend time
  writing about how to use it?
categories:
  - WordPress
  - Plugins
---
If you’re a plugin developer and you just love to write code, then writing a <em>readme.txt</em> file for a plugin in WordPress’ repository might be your idea of hell. When you’ve written all of that lovely code, why must you spend time writing about how to use it?

<a href="/2011/11/23/improve-wordpress-plugins-readme-txt/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8773460d-82eb-4543-8011-6b1be10b291e/readmeheader.jpg" alt="readmeheader" width="550" height="350" /></a>

Unfortunately, some plugin developers view writing a <em>readme.txt</em> file as the least important part of their job. So, we end up with things like the following:

*   [Descriptions with only one line](https://wordpress.org/extend/plugins/contact-form-plugin/),
*   [Descriptions with hardly any information](https://wordpress.org/extend/plugins/wordpress-tiniest-super-cache/),
*   [No translation into English](https://wordpress.org/extend/plugins/profitshare/),
*   [Typos](https://wordpress.org/extend/plugins/lite-cache/).</p>

## Why You Should Care About Your Readme.txt

A poorly written <em>readme.txt</em> does not necessarily indicate that the plugin is poorly written; the code could be mind-blowingly good. But it does give the impression of an overall lack of attention to detail and a lack of care for end users. You see, no one will notice if a readme file is particularly awesome, but they <strong>will notice if it’s bad</strong>.

{{% feature-panel %}}

You needn’t view the readme file as pain-in-the-butt homework that you’ve got to do after all the fun you’ve had with coding. A readme benefits <em>you</em>. Here’s how:

*   Gives you an opportunity to say **why your plugin is so good**,
*   Shows off your plugin’s **features**,
*   Makes it **easy for users** to install and use the plugin,
*   **Anticipates** support questions with a thorough FAQ,
*   **Links** to your website and other products,
*   **Upsells** your commercial services.

In this article, we’ll look at how to improve your WordPress readme file so that it benefits both your users and you.

But first, the mechanics.</p>

## Using (Quasi-)Markdown

<a href="https://daringfireball.net/projects/markdown/">Markdown</a> is a text-to-HTML conversion tool, developed by John Gruber and Aaron Schwartz, that is used for readme files of plugins in the WordPress repository.

You write the readme in Markdown, and Markdown will convert it to HTML for the WordPress directory page, but it will still look good in WordPress’ back end and when you peek at it in your favorite text editor.

Take a look at the directory page for <a href="#">Simple Twitter Connect</a>:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c949cde6-4b90-489b-8972-071574369de6/ss1.jpg" alt="Simple Twitter Connect's listing in the plugin directory" /></figure>

<em>Simple Twitter Connect’s listing in the WordPress plugin directory.</em>

Here’s how it appears when I download and extract the readme:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f68c18ca-9472-41d0-a4e0-e0d6bf6d375e/ss2.jpg" alt="Simple Twitter Connect's readme file" /></figure>

<em>Simple Twitter Connect’s readme file in Notepad.</em>

And here’s how it appears in WordPress’ back end:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ed5677-b4b4-479d-96fa-b961d95da8a6/ss3.jpg" alt="Simple Twitter Connect's listing on the Edit plugin page in the WordPress dashboard" /></figure>

<em>Simple Twitter Connect’s readme on the “Edit Plugin” page in the WordPress Dashboard.</em>

It is <strong>readable</strong> no matter what medium it is viewed in. Imagine how difficult reading the readme in a text editor would be if it was marked up in HTML. Markdown makes your readme clear, readable and semantic.

WordPress.org uses what <a href="https://markjaquith.wordpress.com/2007/03/16/plugin-directory/">Mark Jacquith describes as quasi-markdown</a>. It basically works like markdown, and much of the syntax is the same, but there are a few important differences, particularly in the headers.

To get you started with your WordPress readme, here’s a table containing the syntax that you’ll need.
<table id="testing" style="font-size: 0.75em;padding: 7px;border: 1px solid #ccc;border-collapse: collapse" border="0" width="500" cellspacing="0" cellpadding="6"><br>
<tbody>
<tr style="background: #e1e1e1">
<th>Syntax</th>
<th>Example</th>
<th width="280">Outputs as</th>
<th>Use for</th>
</tr>
<tr>
<td>=== foo ===</td>
<td>=== Plugin Name ===</td>
<td>&lt;h2&gt;Plugin Name&lt;/h2&gt;</td>
<td>Plugin name</td>
</tr>
<tr>
<td>== foo ==</td>
<td>==Description==</td>
<td>&lt;h3&gt;Description&lt;/h3&gt;</td>
<td>Tabbed section headings</td>
</tr>
<tr>
<td>= foo =</td>
<td>=Inline heading=</td>
<td>&lt;h4&gt;Inline heading&lt;/h4&gt;</td>
<td>Headings in the body of the readme</td>
</tr>
<tr>
<td>* foo</td>
<td>* list item, *list item</td>
<td>&lt;ul&gt;
&lt;li&gt;list item&lt;/li&gt;
&lt;li&gt;list item&lt;/li&gt;
&lt;/ul&gt;</td>
<td>Unordered list</td>
</tr>
<tr>
<td>1. foo, 2. foo</td>
<td>1. list item, 2. list item</td>
<td>&lt;ol&gt;
&lt;li&gt;list item&lt;/li&gt;
&lt;li&gt;list item&lt;/li&gt;
&lt;/ol&gt;</td>
<td>Ordered list</td>
</tr>
<tr>
<td>foo bar</td>
<td>You talking to me?</td>
<td>&lt;blockquote&gt;You talking to me?&lt;/blockquote&gt;</td>
<td>block quotes</td>
</tr>
<tr>
<td>*foo*</td>
<td>*emphasis*</td>
<td>&lt;em&gt;emphasis&lt;/em&gt;</td>
<td>Italics</td>
</tr>
<tr>
<td>**foo**</td>
<td>**bold**</td>
<td>&lt;strong&gt;bold&lt;/strong&gt;</td>
<td>Bold</td>
</tr>
<tr>
<td>'foo'</td>
<td>'wp-config.php'</td>
<td>wp-config.php</td>
<td>Any code you want to display (including shortcodes)</td>
</tr>
<tr>
<td>[link] (https://foobar.com "foobar")</td>
<td>[WordPress](https://wordpress.org/ "Your favorite software")</td>
<td>&lt;a href="https://wordpress.org/" title="Your favorite software"&gt;WordPress&lt;/a&gt;</td>
<td>Links</td>
</tr>
<tr>
<td>&lt;https://foobar.com&gt;</td>
<td>&lt;https://wordpress.org&gt;</td>
<td>&lt;a href="https://wordpress.org"&gt;
https://wordpress.org&lt;/a&gt;</td>
<td>Links</td>
</tr>
<tr>
<td>[youtube https://foobarvideo.com]</td>
<td>[youtube https://youtube.com/watch?v=CVmGBoPx6Ms]</td>
<td>&lt;div class='video'&gt;&lt;object width='532' height='325'&gt;&lt;param name='movie' value='https://youtube.com/v/ CVmGBoPx6Ms?fs=1'&gt;&lt;/param&gt; &lt;param name='allowFullScreen' value='true'&gt;&lt;/param&gt;&lt;param name='allowscriptaccess' value='never'&gt;&lt;/param&gt;&lt;embed src='https://youtube.com/v/ CVmGBoPx6Ms?fs=1' type='application/ x-shockwave-flash' allowscriptaccess='never' allowfullscreen='true' width='532' height='325'&gt;&lt;/embed&gt;&lt;/object&gt;&lt;/div&gt;</td>
<td>Video</td>
</tr>
</tbody>
</table>

Now that you know how to write in WordPress-flavored Markdown, let’s get started writing a readme.</p>

## Writing Your Readme.txt

Writing a readme is not hard, but putting a bit of <strong>thought</strong> into it beforehand does pay off.

*   What do you think end users will need in order to get optimal use from your plugin?
*   Do you need to include any special instructions or code snippets?
*   What problems do you anticipate users running into?
*   How can you make your plugin as attractive as possible?
*   In a saturated market, what makes your plugin stand out?

With a bit of thought, you can produce a useful readme that shows off the best aspects of your plugin.

When writing the readme, remember that if people are able to use your plugin properly, then they will be less likely to come knocking on your door asking for help.

Let’s look at each of the main readme sections to see what you can do to improve it. As a reference point, we’ll use the readme for <a href="#">Simple Twitter Connect</a>, which is concise, useful and well-formed.

## Plugin Header

The plugin’s header contains basic information about your plugin that the user will take in at a glance. This information will be displayed in the plugin’s directory as a quick reference for users.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efe75844-2afc-4b5f-8428-95dd079d23de/ss4.jpg" alt="the plugin header information in use in the plugin directory" /></figure>

Here’s what you’ll need to complete it:

*   **Contributors**.  Anyone who has contributed to the plugin. You should use a contributor’s user name from WordPress.org, linking it to their WordPress.org profiles, which list all of the contributor’s plugins. Unfortunately, many developers don’t mention their WordPress user name, which means they miss out on the opportunity to showcase the rest of their work.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8fffab-4bab-46e9-b49e-93081696cec8/ss5.jpg" alt="Contributor tag in the plugin directory linked to the contributor's page" /></figure>

<em>A contributor tag done right.</em>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fa7c4a2-8f5b-42cd-b087-b1ae57605b47/ss6.jpg" alt="plugin author listed in the directory that isn't a WP.org username" /></figure>

<em>A contributor tag done wrong.</em>

*   **Donate link**.  This is your chance to get a little something back from the WordPress community. If you don’t have a donate link, you aren’t giving people the opportunity to thank you!
*   **Tags**.  As on a blog, tags are used to categorize content. In a directory of 15,000+ WordPress plugins, **using tags effectively** makes it easy for people to find your plugin. Keep the tags relevant, and think of what people who need your plugin might be searching for. Some developers tag their plugins with words that are only tangentially related.

&nbsp;

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c593d4b5-a48b-4b6b-9277-0dc69e633e2f/ss7.jpg" alt="The WordPress.org listings for the twitter tag showing facebook plugins and an image gallery plugin" /></figure>

This listing for the Twitter tag isn’t helpful because it’s bloated with irrelevant content. As WordPress community members and contributors, we have a responsibility to keep the directory of plugins as intuitive as possible.

*   **Author URI**.  Your home page.
*   **Plugin URI**.  The plugin’s home page. Note that the Author URI and Plugin URI aren’t included in the [readme template provided by WordPress](https://wordpress.org/extend/plugins/about/readme.txt). Including them is definitely a good thing because they direct people to your respective home pages.
*   **Requires at least**.  This is the version of WordPress that your plugin requires. Some people don’t upgrade WordPress (some for valid reasons and some for dumb reasons). Tell them whether WordPress will work with their version.
*   **Tested up to**.  Another piece of important information. This tells people which version of WordPress your plugin has been tested up to.
*   **Stable tag**.  The stable tag tells WordPress which version of the plugin should appear in the directory. This should be in numeric format, which is much easier for WordPress to deal with. Aim for numbers like 1.5, 0.5 or whatever version you’re at. If your stable version is in the trunk in Subversion, then you can specify “trunk,” but that is the only time you should use words instead of numbers.

&nbsp;

Here’s what the header information for Simple Twitter Connect looks like:

<pre><code class="language-markup tmp-none">=== Simple Twitter Connect ===
Contributors: Otto42
Donate link: https://www.paypal.com/cgi-bin/webscr?cmd=_donations&amp;business=otto%40ottodestruct%2ecom
Tags: twitter, connect, simple, otto, otto42, javascript
Requires at least: 3.0
Tested up to: 3.2
Stable tag: 0.15</code></pre>

### Tips for Writing Header Information

*   Use WordPress.org user names for **contributors**.
*   Use a **number** for the stable tag.
*   Include **donation** link to make some cash.
*   Keep tags **relevant**.
*   **Test** with the most recent WordPress version.</p>

## The Short Description

The short description is what appears on the WordPress.org page that lists plugins.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d34bb393-e74d-46b8-b414-c2aa0d838c65/ss8.jpg" alt="Simple Twitter Connect's short description on the WordPress dashboard plugin page" /></figure>

It also appears in the user’s list of installed plugins:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a87fa8d-bde6-4f65-b17c-92b86d175f2d/ss9.jpg" alt="Simple Twitter Connect's short description on the WordPress dashboard plugin page" /></figure>

It’s your chance to craft a punchy 150-character description that will make people want to install your plugin.

Unfortunately, some people miss the mark:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b72fcfe0-1c19-4c38-9de0-26f1a5c8b903/shortdec1.jpg" alt="buddystream on the listings page without adequate short decription" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d11e53f0-0b62-4848-a860-fc33dd857c61/shortdec2.jpg" alt="A plugin short description written in chinese" /></figure>

I’m not sure what this one is all about:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e336b8e0-cf50-48e3-abe2-01ac30a4f3e8/shortdec3.jpg" alt="This short description drops down over four lines" /></figure>

None of these short descriptions tell you anything about what the plugin does. They’re totally useless in providing information to WordPress users.

Another problem is when developers do not add a short description at all. In that case, the 150 characters are excerpted from the long description. Check out the short description for <a href="https://wordpress.org/extend/plugins/simple-trackback-validation-with-topsy-blocker/">Simple TrackbackSimple Trackback Validation with Topsy Blocker</a>:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbf72bd5-87a9-4e03-b177-37f5e673f8ae/ss13.jpg" alt="Plugin's short description cut off mid-sentence" /></figure>

The short description cuts off in the middle of a word. We know that the plugin performs a test on trackbacks, but why? What for? How?

### Short Descriptions That Get It Right

*   [Yet Another Related Posts Plugin](https://wordpress.org/extend/plugins/yet-another-related-posts-plugin/) “Display a list of related entries on your site and feeds based on a unique algorithm. Templating allows customization of the display.”
*   [BuddyPress](https://wordpress.org/extend/plugins/buddypress/) “Social networking in a box. Build a social network for your company, school, sports team or niche community.”
*   [The Google+ Button](https://wordpress.org/extend/plugins/google/) “Adds the Google +1 button to your site so your visitors can vote to tell the world how great your site is!”

### Tips for Writing a Short Description

*   Stick to **under 150** characters.
*   Don’t rely on the text being pulled from the **long description**.
*   Tell people what the plugin **will do** for them.
*   **Don’t worry about technical details.** You can provide them in the long description.
*   Tell people whether the plugin has any **requirements** to work, such as a subscription.</p>

## Long Description

The long description is where you really go to town. You’ve hooked people with the short description; <strong>now it’s time to sell your plugin</strong>. Let’s check out the long description for Simple Twitter Connect:

<pre><code class="language-markup tmp-none">== Description ==
Simple Twitter Connect is a series of plugins that let you add any sort of Twitter functionality you like to a WordPress blog. This lets you have an integrated site without a lot of coding, and still letting you customize it exactly the way you’d like.

First, you activate and set up the base plugin, which makes your site have basic Twitter functionality. Then, each of the add-on plugins will let you add small pieces of specific Twitter-related functionality, one by one.

Bonus: Unlike other Twitter plugins for WordPress, this one helps you create your own Twitter application and identity, so your tweets from here show up as being from Your Blog, not from some plugin system. You’ll never see "posted by Simple Twitter Connect" in your tweet stream, you’ll see "posted by Your Blog Name". Great way to drive traffic back to your own site and to see your own Twitter userbase.

Requires WordPress 3.0 and PHP 5.

**Current add-ons**
* Login using Twitter
* Comment using Twitter credentials
* Users can auto-tweet their comments
* Tweet button (official one from twitter)
* Tweetmeme button
* Auto-tweet new posts to an account
* Manual Tweetbox after Publish
* Full @anywhere support
* Auto-link all twitter names on the site (with optional hovercards)
* Dashboard Twitter Widget

**Coming soon**
* More direct retweet button (instead of using Tweetmeme)
* (Got more ideas? Tell me!)

If you have suggestions for a new add-on, feel free to email me at otto@ottodestruct.com.
Want regular updates? Become a fan of my sites on Facebook!
https://www.facebook.com/apps/application.php?id=116002660893
https://www.facebook.com/ottopress
Or follow my sites on Twitter!
https://twitter.com/ottodestruct</code></pre>

What makes this a good example of a long description?

1.  The opening description is **clear and useful**. It tells you what the plugin does and how it works.
2.  The **key features stand out** (you can tell that the plugin creates your own Twitter app).
3.  The plugin’s **requirements** are listed.
4.  **Markdown** is used to break up the text into sections and lists, making it easier to read.
5.  All **current features** are listed.
6.  **Planned features** are listed.
7.  The developer has included **links** to his Facebook page and Twitter account.

A good long description is <strong>useful and relevant</strong>. It tells the user what the plugin does and how it does it, and it provide anything else that the developer feels is important. You can also use it to send users to your home page or social-media profiles.

Here are some other plugins with great long descriptions:

*   [EG Attachments](https://wordpress.org/extend/plugins/eg-attachments/)
*   [Google Maps All-in-One](https://wordpress.org/extend/plugins/wordpress-google-maps/)
*   [Next Gen Gallery](https://wordpress.org/extend/plugins/nextgen-gallery/)

### Tips for Writing a Long Description

*   Use Markdown to bring some **variety to the formatting**. For example, add headings to break up sections, use lists, and put important points in bold.
*   Be clear about the plugin’s **features**.
*   Include any **requirements**, such as other plugins that your plugin relies on, or specific PHP versions.
*   Link to any **extended documentation** on your website.
*   Don’t be afraid to **link** to your website or social profiles.
*   If you’ve got one, a **video** is a great demonstration tool.</p>

## Installation

The installation section should include everything that a person needs to get the plugin up and running correctly. Often, you can keep this brief. Check out the instructions for Simple Twitter Connect:

<pre><code class="language-markup tmp-none">1. Upload 'plugin-name.php' to the '/wp-content/plugins/' directory,
2. Activate the plugin through the 'Plugins' menu in WordPress.</code></pre>

For many plugins, this will suffice. But some plugins need detailed instructions. Check out the ones for these:

*   [WP Super Cache](https://wordpress.org/extend/plugins/wp-super-cache/installation/),
*   [WordPress MU Domain Mapping](https://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/installation/).

Users need mammoth instructions to set up both of these plugins. WP Super Cache requires you to look in your <code>.htaccess</code> file, and Domain Mapping needs you to move files to <code>/wp-content/</code> and to edit <em>wp-config.php</em>.</p>

### Tips for Writing Instructions

*   Be **brief**, a few lines if possible.
*   Include **everything the user needs** to install the plugin.
*   Make sure each step **logically** follows the preceding one.
*   Include any **code snippets** that the user might need.
*   Be **clear and concise**. This is the place for instructions, not sales.</p>

## FAQ

The FAQ (frequently asked questions) section is your opportunity to <strong>troubleshoot problems</strong> before they even get posted to WordPress’ support forums. OK, so a few people will probably never bother looking at the FAQ to see whether their question is addressed there, which is annoying, but at least you will be able to direct them to the FAQ.

Some FAQs, however, are <a href="https://wordpress.org/extend/plugins/flexo-facebook-manager/faq/">pretty lousy</a>. In fact, some plugins, <a href="https://wordpress.org/extend/plugins/network-publisher/">even popular ones</a>, lack any FAQ at all. This is a problem: if too many plugin developers don’t include an FAQ, then some WordPress users will assume that plugins normally don’t have one and will run straight to the support forums. This wastes the time of people who have taken the trouble to include an FAQ.

Let’s check out the FAQ for Simple Twitter Connect:

<pre><code class="language-markup tmp-none">&gt;== Frequently Asked Questions ==

= Whoa, what's with all these plugins? =
The principle behind this plugin is to enable small pieces of Twitter functionality, one at a time.

Thus, you have the base plugin, which does nothing except to enable your site for Twitter OAuth in general. It's required by all the other plugins.

Then you have individual plugins, one for each piece of functionality. One for enabling comments, one for adding Login, etc. These are all smaller and simpler, for the most part, because they don't have to add all the Twitter connections stuff that the base plugin adds.

= The comments plugin isn't working! =

You have to modify your theme to use the comments plugin.

In your comments.php file (or wherever your comments form is), you need to do the following.

1. Find the three inputs for the author, email, and url information. They need to have those ID's on the inputs (author, email, url). This is what the default theme and all standardized themes use, but some may be slightly different. You'll have to alter them to have these ID's in that case.

2. Just before the first input, add this code:
[div id="comment-user-details"]
[?php do_action('alt_comment_login'); ?]
(Replace the []'s with normal html greater/less than signs).

3. Just below the last input (not the comment text area, just the name/email/url inputs, add this:
[/div]

That will add the necessary pieces to allow the script to work.

Hopefully, a future version of WordPress will make this simpler.

= Twitter Avatars look wrong. =

Twitter avatars use slightly different code than other avatars. They should style the same, but not all themes will have this working properly, due to various theme designs and such.

However, it is almost always possible to correct this with some simple CSS adjustments. For this reason, they are given a special "twitter-avatar" class, for you to use to style them as you need. Just use .twitter-avatar in your CSS and add styling rules to correct those specific avatars.

= Why can't I email people who comment using Twitter? =

Twitter offers no way to get a valid email address for a user. So the comments plugin uses a fake address of the twitter's username @fake.twitter.com. The "fake" is the giveaway here.

= When users connect using Twitter on the Comments section, there's a delay before their info appears. =

Yes. In order to make the plugin more compatible with caching plugins like WP-Super-Cache, the data for a Twitter connect account is retrieved from the server using an AJAX request. This means that there will be a slight delay while the data is retrieved, but the page has already been loaded and displayed. Most of the time this will not be noticeable.

= Why does the settings screen warn me that I don't have a URL shortener plugin? =

Simple Twitter Connect does not implement a URL shortening service in favor of letting other plugins implement one for it. WordPress 3.0 includes a new shortlink method for plugins to implement this properly.

A shortener plugin should implement the "get_shortlink" filter for it to be detected. WordPress 3.0 will be required for this to work.

The WordPress.com stats plugin implements this, and it provides shortlinks to "wp.me" URLs. If you wish to use another shortener plugin, tell that plugin's author to implement this same standard, and the plugin will automatically be detected and used by Simple Twitter Connect.</code></pre>

That’s a pretty thorough FAQ! It’s useful because it anticipates any questions a user might have. It’s a <strong>pre-emptive strike</strong>: get in there with the answers before you see anxiety explosions in the support forums.

When writing support documentation such as an FAQ, aim at the lowest common denominator. A developer who is using your plugin likely won’t need an FAQ, and if they do, they’ll probably get the gist of it quickly and be able to implement it in an instant. There’s a rumor going around that WordPress is easy to use, which means that a lot of people who don’t know a whole lot about code will be fiddling around with it and break stuff. They are the people to whom you should be addressing your documentation, because they’ll be giving you the biggest headaches in the support forums.</p>

### Tips for Writing an FAQ

*   **Anticipate** issues and answer them in advance.
*   Deal with any **known conflicts** with old WordPress versions or other plugins.
*   If a problem **recurs** in the support forums, add it to your FAQ.
*   Use **Markdown** to highlight each question and follow it with an answer.
*   Include any **code snippets or shortcodes** that the user might need.
*   The FAQ is a **tool to help _you_**. Use it properly, and save some money on Aspirin.</p>

## Screenshots

Unfortunately, many developers think that screenshots are the realm of theme designers. Perhaps you assume that there’s nothing exciting or sexy to see in your plugin, so why bother providing screenshots? Check out the <a href="#screenshots/">screenshots for Simple Twitter Connect</a>. They show both the UI and the front end of the plugin, giving you an idea what it will be like before installing it.

Screenshots help users decide whether a plugin is right for them. As a developer, you might not think your UI is particularly interesting, but as an end user, I like to look at the settings before installing a plugin. It might not be a deal-breaker, but it does help me decide.

Here are some plugins with nice screenshots:

First, you activate and set up the base plugin, which makes your site have basic Twitter functionality. Then, each of the add-on plugins will let you add small pieces of specific Twitter-related functionality, one by one.

Bonus: Unlike other Twitter plugins for WordPress, this one helps you create your own Twitter application and identity, so your tweets from here show up as being from Your Blog, not from some plugin system. You’ll never see "posted by Simple Twitter Connect" in your tweet stream, you’ll see "posted by Your Blog Name". Great way to drive traffic back to your own site and to see your own Twitter userbase.

Requires WordPress 3.0 and PHP 5.

**Current add-ons**
* Login using Twitter
* Comment using Twitter credentials
* Users can auto-tweet their comments
* Tweet button (official one from twitter)
* Tweetmeme button
* Auto-tweet new posts to an account
* Manual Tweetbox after Publish
* Full @anywhere support
* Auto-link all twitter names on the site (with optional hovercards)
* Dashboard Twitter Widget

**Coming soon**
* More direct retweet button (instead of using Tweetmeme)
* (Got more ideas? Tell me!)

If you have suggestions for a new add-on, feel free to email me at otto@ottodestruct.com.
Want regular updates? Become a fan of my sites on Facebook!
https://www.facebook.com/apps/application.php?id=116002660893
https://www.facebook.com/ottopress
Or follow my sites on Twitter!
https://twitter.com/ottodestruct</code></pre>

What makes this a good example of a long description?

1.  The opening description is **clear and useful**. It tells you what the plugin does and how it works.
2.  The **key features stand out** (you can tell that the plugin creates your own Twitter app).
3.  The plugin’s **requirements** are listed.
4.  **Markdown** is used to break up the text into sections and lists, making it easier to read.
5.  All **current features** are listed.
6.  **Planned features** are listed.
7.  The developer has included **links** to his Facebook page and Twitter account.

A good long description is <strong>useful and relevant</strong>. It tells the user what the plugin does and how it does it, and it provide anything else that the developer feels is important. You can also use it to send users to your home page or social-media profiles.

Here are some other plugins with great long descriptions:

*   [EG Attachments](https://wordpress.org/extend/plugins/eg-attachments/)
*   [Google Maps All-in-One](https://wordpress.org/extend/plugins/wordpress-google-maps/)
*   [Next Gen Gallery](https://wordpress.org/extend/plugins/nextgen-gallery/)

### Tips for Writing a Long Description

*   Use Markdown to bring some **variety to the formatting**. For example, add headings to break up sections, use lists, and put important points in bold.
*   Be clear about the plugin’s **features**.
*   Include any **requirements**, such as other plugins that your plugin relies on, or specific PHP versions.
*   Link to any **extended documentation** on your website.
*   Don’t be afraid to **link** to your website or social profiles.
*   If you’ve got one, a **video** is a great demonstration tool.</p>

## Installation

The installation section should include everything that a person needs to get the plugin up and running correctly. Often, you can keep this brief. Check out the instructions for Simple Twitter Connect:

<pre><code class="language-markup tmp-none">1. Upload 'plugin-name.php' to the '/wp-content/plugins/' directory,
2. Activate the plugin through the 'Plugins' menu in WordPress.</code></pre>

For many plugins, this will suffice. But some plugins need detailed instructions. Check out the ones for these:

*   [WP Super Cache](https://wordpress.org/extend/plugins/wp-super-cache/installation/),
*   [WordPress MU Domain Mapping](https://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/installation/).

Users need mammoth instructions to set up both of these plugins. WP Super Cache requires you to look in your <code>.htaccess</code> file, and Domain Mapping needs you to move files to <code>/wp-content/</code> and to edit <em>wp-config.php</em>.</p>

### Tips for Writing Instructions

*   Be **brief**, a few lines if possible.
*   Include **everything the user needs** to install the plugin.
*   Make sure each step **logically** follows the preceding one.
*   Include any **code snippets** that the user might need.
*   Be **clear and concise**. This is the place for instructions, not sales.</p>

## FAQ

The FAQ (frequently asked questions) section is your opportunity to <strong>troubleshoot problems</strong> before they even get posted to WordPress’ support forums. OK, so a few people will probably never bother looking at the FAQ to see whether their question is addressed there, which is annoying, but at least you will be able to direct them to the FAQ.

Some FAQs, however, are <a href="https://wordpress.org/extend/plugins/flexo-facebook-manager/faq/">pretty lousy</a>. In fact, some plugins, <a href="https://wordpress.org/extend/plugins/network-publisher/">even popular ones</a>, lack any FAQ at all. This is a problem: if too many plugin developers don’t include an FAQ, then some WordPress users will assume that plugins normally don’t have one and will run straight to the support forums. This wastes the time of people who have taken the trouble to include an FAQ.

Let’s check out the FAQ for Simple Twitter Connect:

<pre><code class="language-markup tmp-none">&gt;== Frequently Asked Questions ==

= Whoa, what's with all these plugins? =
The principle behind this plugin is to enable small pieces of Twitter functionality, one at a time.

Thus, you have the base plugin, which does nothing except to enable your site for Twitter OAuth in general. It's required by all the other plugins.

Then you have individual plugins, one for each piece of functionality. One for enabling comments, one for adding Login, etc. These are all smaller and simpler, for the most part, because they don't have to add all the Twitter connections stuff that the base plugin adds.

= The comments plugin isn't working! =

You have to modify your theme to use the comments plugin.

In your comments.php file (or wherever your comments form is), you need to do the following.

1. Find the three inputs for the author, email, and url information. They need to have those ID's on the inputs (author, email, url). This is what the default theme and all standardized themes use, but some may be slightly different. You'll have to alter them to have these ID's in that case.

2. Just before the first input, add this code:
[div id="comment-user-details"]
[?php do_action('alt_comment_login'); ?]
(Replace the []'s with normal html greater/less than signs).

3. Just below the last input (not the comment text area, just the name/email/url inputs, add this:
[/div]

That will add the necessary pieces to allow the script to work.

Hopefully, a future version of WordPress will make this simpler.

= Twitter Avatars look wrong. =

Twitter avatars use slightly different code than other avatars. They should style the same, but not all themes will have this working properly, due to various theme designs and such.

However, it is almost always possible to correct this with some simple CSS adjustments. For this reason, they are given a special "twitter-avatar" class, for you to use to style them as you need. Just use .twitter-avatar in your CSS and add styling rules to correct those specific avatars.

= Why can't I email people who comment using Twitter? =

Twitter offers no way to get a valid email address for a user. So the comments plugin uses a fake address of the twitter's username @fake.twitter.com. The "fake" is the giveaway here.

= When users connect using Twitter on the Comments section, there's a delay before their info appears. =

Yes. In order to make the plugin more compatible with caching plugins like WP-Super-Cache, the data for a Twitter connect account is retrieved from the server using an AJAX request. This means that there will be a slight delay while the data is retrieved, but the page has already been loaded and displayed. Most of the time this will not be noticeable.

= Why does the settings screen warn me that I don't have a URL shortener plugin? =

Simple Twitter Connect does not implement a URL shortening service in favor of letting other plugins implement one for it. WordPress 3.0 includes a new shortlink method for plugins to implement this properly.

A shortener plugin should implement the "get_shortlink" filter for it to be detected. WordPress 3.0 will be required for this to work.

The WordPress.com stats plugin implements this, and it provides shortlinks to "wp.me" URLs. If you wish to use another shortener plugin, tell that plugin's author to implement this same standard, and the plugin will automatically be detected and used by Simple Twitter Connect.</code></pre>

That’s a pretty thorough FAQ! It’s useful because it anticipates any questions a user might have. It’s a <strong>pre-emptive strike</strong>: get in there with the answers before you see anxiety explosions in the support forums.

When writing support documentation such as an FAQ, aim at the lowest common denominator. A developer who is using your plugin likely won’t need an FAQ, and if they do, they’ll probably get the gist of it quickly and be able to implement it in an instant. There’s a rumor going around that WordPress is easy to use, which means that a lot of people who don’t know a whole lot about code will be fiddling around with it and break stuff. They are the people to whom you should be addressing your documentation, because they’ll be giving you the biggest headaches in the support forums.</p>

### Tips for Writing an FAQ

*   **Anticipate** issues and answer them in advance.
*   Deal with any **known conflicts** with old WordPress versions or other plugins.
*   If a problem **recurs** in the support forums, add it to your FAQ.
*   Use **Markdown** to highlight each question and follow it with an answer.
*   Include any **code snippets or shortcodes** that the user might need.
*   The FAQ is a **tool to help _you_**. Use it properly, and save some money on Aspirin.</p>

## Screenshots

Unfortunately, many developers think that screenshots are the realm of theme designers. Perhaps you assume that there’s nothing exciting or sexy to see in your plugin, so why bother providing screenshots? Check out the <a href="#screenshots/">screenshots for Simple Twitter Connect</a>. They show both the UI and the front end of the plugin, giving you an idea what it will be like before installing it.

Screenshots help users decide whether a plugin is right for them. As a developer, you might not think your UI is particularly interesting, but as an end user, I like to look at the settings before installing a plugin. It might not be a deal-breaker, but it does help me decide.

Here are some plugins with nice screenshots:

*   [Social Profiles Sidebar Widget](https://wordpress.org/extend/plugins/social-profiles-sidebar-widget/screenshots/)
*   [WP Page Navi](https://wordpress.org/extend/plugins/wp-pagenavi/screenshots/)
*   [Next Gen Gallery](https://wordpress.org/extend/plugins/nextgen-gallery/screenshots/)

### Tips for Putting Together Screenshots

*   Name screenshots as _screenshot-1.png_, _screenshot-2.png_, etc.
*   Include at least one screenshot of the **UI**, and one of what it does in the **front end** (if it does anything there).
*   Keep the size of the screenshot file **small**.</p>

## Other Notes

Including “Other Notes” is not essential. Many plugins don’t have them; Simple Twitter Connect doesn’t, for instance. But the section is useful if you have <strong>additional information</strong> that doesn’t necessarily fit in any other section.</p>

### Things You Can Include in “Other Notes”

*   [Credits](https://wordpress.org/extend/plugins/nextgen-gallery/other_notes/)
*   To-do list
*   [Localizations](https://wordpress.org/extend/plugins/yet-another-related-posts-plugin/other_notes/)
*   [Filters](https://wordpress.org/extend/plugins/wordpress-importer/other_notes/)
*   Set-up guide
*   Requirements
*   [External links](https://wordpress.org/extend/plugins/xhanch-my-twitter/other_notes/)
*   Upgrading information
*   [Licence](https://wordpress.org/extend/plugins/seo-automatic-links/other_notes/)

## Changelog

A changelog, as you would guess, is a <strong>log of all changes</strong> you’ve made to the plugin. It is an important part of the documentation and shouldn’t be ignored. A changelog may not make for the most exciting reading, but it is helpful. It tells a user what changes have been made to a plugin, and it makes clear why the user should update. It’s also useful for tracking the development of the plugin over time. A changelog gives a plugin <strong>context and history</strong>, and that can be important for people running big projects or important client websites.

Here’s a scenario: a user sees an alert in the admin area telling them that they need to update a plugin.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce5865d3-402b-44d2-8578-fa6c7e2f7218/ss14.jpg" alt="Update WP Touch notice" /></figure>

<em>This user needs to update WP Touch!</em>

The changelog shows the changes, so that the user can decide whether to update.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb10753d-8dd1-41d5-90d4-504f06eeb91a/ss15.jpg" alt="WP touch's changelog" /></figure>

<em>The changelog helps us decide.</em>

Maintaining some websites is a balancing act, and some administrators don’t want to upgrade unless absolutely necessary (say, for security updates or for new must-have features). Give them the information they need to be able to decide for themselves. If the update is minor, they might decide to save themselves the hassle and wait until something major arrives.

<a href="#changelog/">The changelog for Simple Twitter Connect</a> is lengthy, not surprisingly. You’ll see all of the minor and major changes that have been made. Being able to see this plugin’s history and development is so useful.</p>

### Tips for Writing the Changelog

*   **No change is insignificant**. Make sure to add every single change.
*   The changelog must have the most recent changes first.</p>

## **Upgrade Notice**

<div>The upgrade notice gives additional information to users who are about to upgrade. Although this doesn't appear in the WordPress plugin directory it's fed through to users on the WordPress Dashboard appearing both on wp-admin/update-core.php. Here's the upgrade notices for BuddyPress and Akismet in action:</div><br>
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd94ed2e-ea7b-4fbf-8094-b59128e71a99/upgradenotice1.png" alt="buddypress upgrade notice for 1.5.3" width="550" height="207" /></figure>

<div>This section is really helpful as it gives a user additional information they can use before they upgrade.</div>

### Tips for Writing Upgrade Notices

*   keep your upgrade notices short and descriptive. Aim to be informative.</p>

## Bonus - Adding a Banner Image

Since this article was published, WordPress have made it even easier for your to show off your plugin in the WordPress plugin directory. <a href="https://wpdevel.wordpress.com/2011/12/21/been-giving-a-lot-of-thought-to-how/">Matt announced that he had been looking for ways to give plugin authors more control over their plugin page on the directory</a>. The first step was introducing banner images for plugin pages. Check out the banner image on <a href="https://wordpress.org/extend/plugins/hello-dolly/">Hello Dolly</a>.

Note: WordPress.org are still experimenting with plugin pages so these may change.

To add a banner image to your plugin page:

*   Create a 772 x 250 pixel jpg or png (no GIFs)
*   Check it in to your plugin’s SVN directory with the path `assets/banner-772x250.(jpg|png)`. Note:  the `assets` directory is added to your plugin’s _root directory_, not the trunk
*   your banner image will appear on the next plugin directory refresh (happens every 15 minutes).</p>

## Conclusion

Underestimating the importance of the readme file does a disservice to your code and to the WordPress community; so, seeing so many plugin developers do just that is sad. Don’t fight the readme: embrace it. It’s an important part of your documentation. A good readme is useful, helping users get set up to use the plugin as effectively as possible. And it’s useful to you, the developer. The readme demonstrates your plugin and anticipates problems, and it’ll save you time and headaches with support requests.

Here are some useful resources to get your plugin ready for the WordPress repository:

*   [WordPress _readme.txt_ template](https://wordpress.org/extend/plugins/about/readme.txt) The _readme.txt_ template provided by WordPress.org. Download it and stick your readme text in it to get started.
*   [WordPress _readme.txt_ validator](https://wordpress.org/extend/plugins/about/validator/) Validating your readme before submitting it is helpful. This tool will flag any issues so that you can get it just right.
*   [WordPress Plugin Readme File Generator](https://sudarmuthu.com/wordpress/wp-readme) Feeling lazy? If you would prefer to fill in a form than write up a _readme.txt_ file, try this generator.
*   “[How to Publish to the WordPress Plugin Repository](https://wp.tutsplus.com/tutorials/how-to-publish-to-the-wordpress-plugin-repository/)” There’s more to publishing in the repository than writing a readme. This tutorial takes you through the steps to getting published.
*   “[How to Write a WordPress Plugin: 12 Essential Guides and Resources](https://wpmu.org/how-to-write-a-wordpress-plugin-12-essential-guides-and-resources/)” Haven’t even started writing your plugin yet? Check out this collection of plugin development resources.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Making A WordPress Plugin That Uses Service APIs](https://www.smashingmagazine.com/2016/03/making-a-wordpress-plugin-that-uses-service-apis/)
*   [How Commercial Plugin Developers Are Using The Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)

{{< signature "al" >}}

