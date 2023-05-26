---
title: How Commercial Plugin Developers Are Using The WordPress Repository
slug: commercial-plugin-developers-wordpress-repository
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1831c77-31cd-41ee-9de0-2a3867a7940c/wordpress-11.png
date: 2012-01-13T15:54:50.000Z
author: siobhan-mckeown
description: >-
  A few weeks ago I wrote about how you can put together a [great readme.txt for
  the WordPress plugin
  directory.](https://www.smashingmagazine.com/2011/11/23/improve-wordpress-plugins-readme-txt/)
  In addition to using a WordPress readme as a tool to help out your users, you
  can use it to promote your commercial products and services.
categories:
  - WordPress
  - Plugins
---
A few weeks ago I wrote about how you can put together a <a href="https://www.smashingmagazine.com/2011/11/23/improve-wordpress-plugins-readme-txt/">great readme.txt for the WordPress plugin directory.</a> In addition to using a WordPress readme as a tool to help out your users, you can use it to promote your commercial products and services. While commercial theme developers are already promoted on WordPress.org, this promotion isn’t extended to commercial plugin developers.

But restrictions often lead to creativity, and developers have had to get a bit creative in figuring out how to monetize the WordPress repository. API keys, complementary plugins and lite versions are just a few of the ways that plugin developers are exploiting the WordPress plugin directory for commercial benefit.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Making A WordPress Plugin That Uses Service APIs](https://www.smashingmagazine.com/2016/03/making-a-wordpress-plugin-that-uses-service-apis/)
*   [WordPress Essentials: How To Create A WordPress Plugin](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/)
*   [Guide To WordPress Coding Standards](https://www.smashingmagazine.com/2012/07/guide-wordpress-coding-standards/)

<img loading="lazy" decoding="async"  title="WordPress Repository Plugins" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bd22f46-4725-48fe-9ad3-9b0466d2d6de/siobhan-plugins-new.jpg" alt="WordPress plugins graphic" width="500" height="383" /><br>
<em>(Image: Bowe Frankema)</em>

{{% feature-panel %}}

## What’s Allowed?

Back in 2009, Mark Jaquith <a href="https://wpdevel.wordpress.com/2009/08/31/agenda-for-20090903-dev-chat-discus/">posted this</a> on the WordPress development blog:
<blockquote>Plugins that merely exist as placeholders for a plugin hosted elsewhere (like a “requirements check” plugin) are out, but “lite” versions, etc are in. The goal is to have the directory be free-to-download plugins. A placeholder for a premium plugin is against that spirit.</blockquote>

He goes on to say:
<blockquote>If your plugin is actually a plugin, not just an advertisement or a placeholder for a plugin hosted elsewhere, you’re fine, as far as this rule is concerned.</blockquote>

Related to this, <a href="https://wordpress.org/support/topic/plugin-that-integrates-with-a-must-pay-for-service">Matt Mullenweg posted</a> on the WordPress.org support forums:
<blockquote>There are plenty of plugins that tie into third-party services, for example Google AdSense, and some of them have no free versions. That’s totally fine as long as the plugin is totally GPL.</blockquote>

I emailed Matt to see if anything has changed since he posted this, and he directed me to WordPress.org’s “<a href="https://wordpress.org/extend/plugins/about/guidelines/">Detailed Plugin Guidelines</a>.”

Briefly, if you’re a <strong>commercial</strong> plugin developer, here’s what you need to keep in mind if you’re planning to use the repository:

*   The plugin **must be GPLv2**. (Explicitly state this in your license. If you don’t, it will be assumed that your plugin is GPLv2.)
*   **Trialware** is not allowed.
*   **Upselling** is allowed (but not by being annoying or disabling features after a time period).
*   **Serviceware** is allowed, even for paid services (i.e. a plugin that serves to interface with a third-party service). The service must be doing something substantive, not just providing keys or licenses.
*   **No phoning home** without the user’s consent. This includes:
    *   No unauthorized collection of **user data**;
    *   No remote **images or scripts** (everything must be part of the plugin);
    *   **Banners and advertising** text should not be included in the plugin;
    *   **Advertising spam** is not allowed.
*   No sending **executable code via a third-party system** (unless of a service-client model).
*   **External links** may not be included on the user’s public website.
*   No hijacking the **admin page**.
*   No **sponsored links** in the readme.
*   WordPress.org reserves the right to **edit the guidelines and to arbitrarily disable or remove** a plugin for any reason whatsoever.

Adhering to these guidelines is a delicate balance, and not everyone who tries to monetize the repository is successful at it, as the people behind <span class="removed_link" title="https://pluginsponsors.com/">Plugin Sponsors</span> recently found out.

That said, let’s look at some models whereby developers have managed to create synergy between free plugins and paid plugins or services.</p>

## The API Key

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f18928b3-4e75-46c2-a001-8ceb86ed034b/antispam.jpg" alt="A car licence plate reading No Spam" width="500" height="300" /><br>
<em>No one likes spam. (Image: <a href="https://www.flickr.com/photos/51035555243@N01/362270357/">Thomas Hawk</a>)</em>

<strong>Who’s doing it?</strong>

*   [Akismet](https://wordpress.org/extend/plugins/akismet/)
*   [Scribe SEO](https://wordpress.org/extend/plugins/scribe/)
*   [YoLink](https://wordpress.org/extend/plugins/yolink-search/)
*   [WPMU DEV Anti-Splog](https://wordpress.org/extend/plugins/anti-splog/)

If you’ve installed WordPress, then you’ve met Akismet. Akismet is the anti-spam plugin that comes bundled with WordPress. It’s free for non-commercial use, but if you are using it for a commercial website, then you have to pay for it. The whole Akismet issue pops up every so often in the <a href="https://www.wptavern.com/is-akismet-still-free">WordPress blogosphere</a>. Many people feel that a <a href="https://wpmu.org/should-akismet-really-ship-with-wordpress/">commercial plugin shouldn’t be bundled</a> in WordPress, although I don’t plan to get into that debate here.

Whatever you think of it, providing an API key for a service is a viable way to create a WordPress plugin, host it in the WordPress repository, and yet <strong>charge for the service</strong> that it provides. Another plugin provider that adopts this model is <a href="https://www.yolink.com/yolink/">YoLink</a>, a search service that offers advanced search functionality for websites. Personal websites (i.e. without advertising) that have fewer than 5,000 monthly visitors per year can use it for free; after that, the pricing varies.

“We’ve found that once a user has ample time to test-drive the plugin on their site, they come to realize its value and upgrade to a paid subscription,” says Joe Pagliocco of YoLink. “We are seeing this most often with commercial sites looking for additional flexibility and indexed pages.”

However, you <strong>don’t even have to offer a free version</strong> of your service to get a plugin with an API key into the repository. Scribe, a popular service from Copyblogger, is a plugin that integrates with your WordPress website. In order to use Scribe, you have to sign up for an API key, which is a minimum of $17 per month. While the plugin is GPLv2 and free, the service is not. This approach might <a href="https://wordpress.org/support/topic/plugin-scribe-seo-commercial-junk">make some people hate you</a>, but it is still a viable way to make money from a plugin in the directory.

<strong>Pro:</strong> You’re able to offer a plugin that provides a service and make money from it.

<strong>Con:</strong> People might hate you for it.</p>

## Upgrades And Support Forum

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d427b17a-358b-47b5-be39-b94604f6a4c3/jigoshop.jpg" alt="Jigoshop e-commerce plugin" width="500" height="300" /><br>
<em>Jigoshop offers a commercial-level e-commerce plugin — for free!</em>

<strong>Who’s doing it?</strong>

*   [Jigoshop](https://jigoshop.com/)
*   [WP eCommerce](https://getshopped.org/)

Jigoshop is a free e-commerce plugin, available in the WordPress repository. It includes everything that you need to run an e-commerce website. If you like the plugin (and many people do), then you can pay for <a href="https://jigoshop.com">premium upgrades</a> and <a href="https://jigoshop.com/support/">support</a>. Premium upgrades include MailChimp integration, BuddyPress integration and various advanced payment gateways.

I spoke with Dan Thornton at Jigoshop, and he said that they had considered going down the lite/premium route, but because the <strong>free version was embraced so quickly</strong>, they didn’t want to duplicate their work. By including all of the standard payment gateways in the free version, they made it possible for a small business to get a store up and running and then invest its money in extending the store’s features and functionality, rather than have to pay for all of the bits and pieces up front.

When Jigoshop launched earlier this year, it got a lot of promotion throughout the WordPress community purely because it is a totally free, fully-functioning e-commerce solution. “If we’d gone for a different business model,” says Dan, “we couldn’t have afforded the marketing and advertising to match the recommendations and promotion that we’re grateful to have had from users, designers and developers.”

<strong>Pro:</strong> Massive community of developers has gathered around Jigoshop, adding their own expertise to the product.

<strong>Con:</strong> A fully-functional GPL plugin is open to being forked by bigger players on the scene.

## The Lite Plugin

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6defb445-901e-468a-b816-f8bc47416d55/dietcoke.jpg" alt="Bottles of Diet Coke" width="500" height="300" /><br>
<em>Do you like your plugins with less calories? (Image: <a href="https://www.flickr.com/photos/niallkennedy/505176492/">Niall Kennedy</a>)</em>

<strong>Who’s doing it?</strong>

*   [WPMU DEV](https://premium.wpmudev.org/)
*   [Event Espresso](https://eventespresso.com/)
*   [Cart66](https://cart66.com/)

This is probably one of the most common ways to use the repository to up-sell, and it can be a great option for a variety of plugins. Basically, you restrict the features in the free version and offer a paid version for people who want more features. Putting a lite version of a plugin in the repository is fine, provided it is GPL and adheres to the “Detailed Plugin Guidelines.”

<a href="https://premium.wpmudev.org/">WPMU DEV</a>, a shop for WordPress plugins, has a number of lite versions of its commercial plugins in the repository. It offers lite versions of its Google Maps, eCommerce, Chat, Wiki and Membership plugins, among others. In theory, these plugins should be adequate for the average WordPress user who wants the given functionality on their website, while the commercial versions are available for those who need even more functionality.

I asked James Farmer, of WPMU DEV, what he holds back for his members. “We started holding back quite a bit,” he says. “Now we hold back very little. It’s really just the extended stuff and extra support, etc, that premium users get.”

With little functionality being held back for members, I asked James why they bother including free plugins in the repository. “I suppose you could say to ‘give back,’” he says. “But really, it’s just about business: if folks get to try our plugins for free (and the WordPress.org repository is the best place to get them to do that), then a proportion of them will be keen on our full offerings… At least that’s the plan.”

<strong>Pro:</strong> Give back to the community while maintaining your business model.

<strong>Con:</strong> Have to split your support base across WordPress.org and your own website.</p>

## Complementary Plugins

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb6d289d-f339-464d-b750-7e04b6962b54/shoes.jpg" alt="Rows of shoes" width="500" height="300" /><br>
<em>Some things just work better in pairs. (Image: <a href="https://www.flickr.com/photos/martin_hartland/347033446/">Martin Hartland</a>)</em>

<strong>Who’s doing it?</strong>

*   [WP Types & Views](https://wp-types.com/)

Two new plugins on the WordPress scene are taking a different approach. Developed by <a href="https://www.onthegosystems.com/">OnTheGoSystems</a> (the folks behind the popular <a href="https://wpml.org">WPML</a>), <a href="https://wordpress.org/extend/plugins/types/">Types</a> is a plugin for creating custom post types, while <a href="https://wp-types.com/home/views-create-elegant-displays-for-your-content/">Views</a> is a plugin for displaying content. Drupal users will recognize similarities between Views and a <a href="https://drupal.org/project/views">certain Drupal module</a>.

Types is free and can be found in the WordPress repository. Views, on the other hand, is a commercial plugin available through the developer’s website. Types is a fully-functional plugin, and if all you’re interested in is creating custom post types and taxonomies and custom fields, then you might stop there. But Views is used to display the content in complex ways by querying the WordPress database for you. And, of course, the <strong>Types readme.txt tells you all about what you can do with Views</strong>, to tempt you into grabbing the complementary commercial plugin.

OnTheGoSystems developed Types and Views hand in hand, and it markets them that way, too. Views needs Types to create content, and Types is made better when Views displays it. A synergy between the two fuels the business model. “Types complements Views,” says Amir Helzer, CEO of OnTheGoSystems, “by making it easy to create and manage custom data. Marketing 101 says that when you want to promote your product, you work to turn its complements into commodities. This is what Types does. It makes creating of custom data into a non-issue, so that people can concentrate on its display (via Views).”

<strong>Pro:</strong> Exploit a ready-made market for your commercial plugin.

<strong>Con:</strong> The market might decide that it only wants your free plugin.</p>

## Offer Commercial Themes

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11ea2196-55de-4669-bc91-8830717ca733/shoppingtrolley.jpg" alt="Shopping cart" width="500" height="300" /><br>
<em>There’s big business in WordPress e-commerce. (Image: <a href="https://www.flickr.com/photos/thristian/4778865993/">Thristian</a>)</em>

<strong>Who’s doing it?</strong>

*   [WooThemes](https://www.woothemes.com/)

The plugin directory isn’t being used just by commercial plugin developers. If you run a successful commercial theme shop, then it’s perfectly within your power to give away a functional WordPress plugin for free, dedicate a team of developers to it, and then let the money roll in as <strong>people look for commercial themes to power your plugin</strong>. That’s what WooThemes has done with <a href="https://www.woothemes.com/woocommerce/">WooCommerce</a>.

You can get WooCommerce from the WordPress repository for free; and with more than 30,000 downloads since launch, it’s proving to be a pretty popular e-commerce solution. What it’s really got going for it, though, is the large collection of dedicated e-commerce themes that work with the plugin.

While already successful as a commercial theme shop, WooThemes was keen to test its legs in the freemium waters. E-commerce seems like a perfect fit for it: free core functionality, while charging for design. I asked Adii Pienaar, WooThemes’ founder, what effect WooCommerce has had on its business. He says, “WooCommerce has been quite a diversification for us on two fronts. First, it diversifies our revenue models and allows us to include the freemium model, which means a higher volume of users. Secondly, it has added a whole new class of products to our offering. To that extent, we’ve already seen a bump in our overall revenue, and our WooCommerce-related revenues are already establishing themselves as a firm chunk of that pie.”

To follow this model, Adii suggests that you develop a great core product and then monetize add-ons to that core. Because the core is free, you get high-volume adoption, and you need only monetize a certain percentage of it to be profitable.

<strong>Pro:</strong> Great way to expand your current market.

<strong>Con:</strong> Works best if you’re already backed by a strong brand.</p>

## Installation And Set-Up Services

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/033be949-8bf2-418d-bf02-cf3d182373f1/plumber.jpg" alt="A Lego plumber" width="500" height="300" /><br>
<em>Everyone needs a bit of help sometimes. (Image: <a href="https://www.flickr.com/photos/carolbrowne/3444237986/in/photostream/">Carol Browne</a>)</em>

<strong>Who’s doing it?</strong>

*   [s2Member](https://www.s2member.com/)

s2Member is powerful membership plugin. In fact, it’s so powerful that a dedicated installation service runs alongside it. Simplicity in a plugin is always a bonus, but out of necessity some plugins end up being seriously complex. That isn’t a bad thing, but it can get confusing for less advanced WordPress users. From my own experience, membership plugins can be extensive and pretty difficult for users to set up.

A great way to monetize a plugin like this is to offer an installation service alongside it. To set up s2Member, you can employ <a href="https://www.s2installs.com/">s2Installs</a>. This is the team of developers behind s2Members, and they can install and set it up for you, as well as provide custom coding to extend the plugin to fit your needs. What better way to set up and extend a plugin than by employing its own developers to do it?

This is a really good model in which everyone can access the plugin for free, while commercial help is available for people who aren’t able to use the plugin to its full extent.

<strong>Pro:</strong> You are the best person to provide set-up, installation and customization of your plugin, so capitalize on it!

<strong>Con:</strong> Only works with big plugins. Might not work so well with your Google +1 button.</p>

## Is It Really Worth It?

Now that we’ve looked at some of the models, you might be wondering if this is actually worth it. Many commercial plugin developers, including those of popular plugins such as <a href="https://www.gravityforms.com/">Gravity Forms</a>, don’t adopt the freemium model and yet are still incredibly successful. In fact, a number of the plugin developers I spoke with said that the amount of traffic they get from the repository is minimal, not to mention other developers who don’t want a whole lot to do with WordPress.org. Some feel that the tightrope that has been set up for commercial plugin developers who want to use the repository is too precarious and not something they want to put effort into. <a href="https://wordpress.org/extend/themes/commercial/">Commercial themes are supported on WordPress.org</a>, but there is nothing similar for plugin developers. Most of the developers I spoke with felt that a commercial plugin page will probably never appear on WordPress.org.

That said, if you are going down the freemium route, then using the WordPress repository is definitely a viable option, provided that you do actually use GPLv2 and provide some kind of useful service. The WordPress plugin directory will always be the best way to get your product into WordPress’ back end.

Like everything, the WordPress plugin directory has its upsides and downsides, and it’s not a one-size-fits-all solution. But in addition to directly promoting your product and services, having a plugin in the repository has a load of indirect benefits:

*   **Self-promotion and branding**.  You might not be making a living off of your plugin, but you will be making a living off of yourself. A great example of this is [Yoast](https://yoast.com/), which is available for free in the plugin directory; while its developer doesn’t make any money from it directly, his business is built on his SEO expertise.
*   **Networking**.  Having a plugin in the directory helps you to connect with other people in the WordPress community. People will be like, “Oh, you’re the guy who made _that_ plugin. I love that!” The more popular your plugin, the more people will be interested in you.
*   **Custom work**.  Offering a plugin means that someone out there might want your plugin to be customized, and they might be willing to pay for it.
*   **Job leads and opportunities**.  You never know who is looking in the repository. Some big-wig might love your plugin and could be hiring. You could also use it as part of your CV, letting potential employers check out your code before even getting shortlisted.
*   **Kudos**.  Everyone loves a plugin developer — and if they don’t, they should!
*   **Giving back**.  Part of being a member of an open-source community is finding a way to give back. After all, we get the software that we build our livelihoods on for free. A free plugin in the directory is a great way to give back, especially if it’s a good one!

Of course, it’s not all happiness and sparkles. There are some aspects to having a plugin in the repository that put some developers off:

*   **Double the support**.  If you offer support on your own website, too, then you’ll have to keep on top of two support forums.
*   **Unreasonable support expectations**.  It’s sad, but some WordPress users feel that developers who give their plugins away for free should be at the beck and call of users. This leads to flaming in forums, hostile emails, angry tweets and the occasional midnight phone call.
*   **Keeping up with WordPress**.  WordPress has a fast development cycle, with around two to three major releases a year (along with security updates and the like). Maintaining a plugin can become quite a chore, as is apparent from all of the orphaned plugins in the repository.
*   **#17 in the “Detailed Plugin Guidelines”** This states that WordPress.org can revise the guidelines and arbitrarily disable or remove plugins whenever it feels like it. This arbitrariness does put people off.</p>

## A Commercial Plugin Shop?

It has long been fabled that Automattic might create some sort of WordPress app store where commercial plugin developers can sell their plugins to users straight from the WordPress dashboard. This will likely remain a fable, with no whisper from Automattic that anything of the sort is planned. Of course, there are places where you can purchase commercial WordPress plugins, such as <a href="https://wpplugins.com">WPPlugins</a> and <a href="https://codecanyon.net/">Code Canyon</a>, but neither of these has the advantage of delivering plugins directly from the WordPress dashboard.

<a href="https://plugpress.com">PlugPress</a> tried a different approach. It created an “app store” plugin that WordPress users could install from the WordPress directory and then use to browse commercial plugins and themes. It uploaded the plugin to the WordPress repository and announced that it was live, and then the plugin was removed.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="78211" title="Screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2df3d6d-58fb-49cf-9717-05d0d4e13f01/plugpress.jpg" alt="Although Google indexes PlugPress as being in the WordPress repository, the link is now dead" />

It’s a pretty clear signal that this type of store plugin won’t be allowed in the WordPress repository.

Amir Helzer (who we met earlier) has another approach. He <a href="https://wpml.org/2011/06/alternative-repo-for-commercial-plugins-and-themes/">posted a few months ago</a> on the WPML blog about an alternative repository for commercial plugins and themes. His premise is similar to the approach taken in the Linux world. Every theme and plugin author can become their own repository. So Theme Forest could have a repository, as could Mojo Themes, as could whoever else. A central plugin would enable WordPress users to select commercial sources from which to search for themes or plugins. This would essentially make commercial plugins available in the dashboard and enable people to easily upgrade. It’s a novel idea, but given PlugPress’ swift exit from the repository, you won’t be seeing this in the WordPress directory anytime soon.</p>

## Conclusion

I firmly believe that <strong>placing restrictions on something spurs greater creativity</strong>, and the models above demonstrate how commercial plugin developers are thinking outside the box to use a directory that is essentially for free plugins. If it were simply a matter of a WordPress app store, then all of us would be in danger of buying plugins that aren’t very good (Apple’s App Store, anyone?). Plugin developers think creatively, which can only be a good thing for end users. Astute plugin developers will always find ways to use the WordPress plugin repository to promote their products, and I hope that their plugins are the better for it.

Developers are undoubtedly creating synergy between their commercial products and the repository in other ways. If you know of any, we’d love to hear about them in the comments!

### Further Resources

*   Looking for a service to sell your plugins? Try [WPPlugins](https://wpplugins.com) or [Code Canyon](https://codecanyon.net/).
*   “[Plugin Repository and Commercial Plugins](https://www.wptavern.com/plugin-repository-and-commercial-plugins),” WordPress Tavern A discussion about commercial plugins in the repository.
*   “[How to Improve Your WordPress Plugin’s Readme.txt](https://www.smashingmagazine.com/2011/11/23/improve-wordpress-plugins-readme-txt/),” Siobhan McKeown An article by me, right here on Smashing Magazine.

{{< signature "al" >}}

