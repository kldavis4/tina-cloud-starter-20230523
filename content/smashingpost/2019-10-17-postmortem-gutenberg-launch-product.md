---
title: 'Postmortem Of Gutenberg The Launch, So We Can Embrace Gutenberg The Product'
slug: postmortem-gutenberg-launch-product
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7679d76c-1962-46d1-80cb-b0052c964356/postmortem-gutenberg-launch.png
date: 2019-10-17T12:30:59+02:00
summary: >-
  Even though Gutenberg is currently at its best ever, many people still do not welcome it into their projects, due to the frustrating experience suffered when it was launched with WordPress 5.0. This is unfortunate, because, as a product, Gutenberg is outstanding. Let's do a postmortem of what went wrong with the launch of Gutenberg, as to allow ourselves to embrace Gutenberg as the product.
description: >-
  A postmortem of what went wrong with the launch of Gutenberg, as to allow ourselves to embrace Gutenberg as the product.
categories:
  - WordPress
  - Coding
---
After 10 months of being released as WordPress's new default editor, Gutenberg is still shrugged off by a sizable amount of people from the web development community, who frequently cite as reasons to disregard it its lack of accessibility support (even though [major accessibility improvements have taken place](https://make.wordpress.org/core/2019/08/14/whats-new-in-gutenberg-14-august/)), how slow it is (even though it is running much faster now), and several other grievances. This pessimistic reaction to Gutenberg is most evident in online articles demonstrating Gutenberg's capabilities which, instead of eliciting a positive reaction from the readers, they mostly attract contempt (as reflected in a stream of negative comments).

Many people seem to be angry "at Gutenberg" (we will see in a while what Gutenberg actually is), expressing that Gutenberg should never have happened or, at least, never have been integrated to WordPress core as its default experience, or at least not so soon. Different people have different reasons to be opposed to Gutenberg, with some of their reasons being more personally significant than others. For instance, some people have seen their livelihoods jeopardized, having worked hard to specialize on a certain solution which, due to Gutenberg's arrival, is in peril of disappearing (such as anyone working with this brand or that brand of page builders). I can truly understand why these people are angry at Gutenberg, and I sympathize with them.

However, I do also believe that being endlessly angered by Gutenberg and dismissing the whole of it &mdash; without even considering if it may be worth using after all &mdash; is not a sensible approach. When it was initially launched, I was quite opposed to Gutenberg, thinking that it was not ready, and this stance lasted for several months. However, I have lately found myself using Gutenberg more and more, and I can even claim that, nowadays, I'm actually enjoying it. While at the beginning I was a bit angered "at Gutenberg" myself too, I let my anger go away, and now I can actually benefit from it.

Through this article, I will attempt to change the narrative under which Gutenberg is most commonly depicted. I will enumerate what went wrong in the past, and describe what Gutenberg has been and what it is, from which I can give a leap of faith to present Gutenberg in a favorable light. I will also argue that Gutenberg already is a positive force, and as such, it deserves being given another chance (if you haven't done so yet).

{{% feature-panel %}}

## What Gutenberg Actually Is

From my point of view, the most important reason why Gutenberg is not more widely accepted is that, when people talk about Gutenberg, they equal it to not one but actually two entities (which are confused with each other), namely:

1. Gutenberg, the launch;
2. Gutenberg, the product.

Gutenberg as "the product" is the plugin/functionality itself. Gutenberg as "the launch" was the process that involved the initial development and release of Gutenberg, possibly starting when WordPress founder Matt Mullenweg introduced Gutenberg to the wider audience in June 2017 during WordCamp Europe 2017, and ending in early December 2018 when WordPress 5.0 was released with Gutenberg merged into it. 

(Once the launch was over, a new stage started which continues until today: The "Gutenberg continuous delivery cycle". However, this stage is very different from "Gutenberg the launch", as there have been no serious issues with it, and as such it doesn't produce any misconception towards "Gutenberg the product". For this reason, there is no need to talk about it in this article.) 

We must distinguish between the two entities, "the launch" and "the product". As such, from now on, I hope that when we refer to "Gutenberg" it invariably means "Gutenberg the product", and if we want to reference "Gutenberg the launch" then we must explicitly name it (possibly using any of its variations, such as "Gutenberg's initial development/release" or similar phrases). Most importantly, we must refrain from mixing the launch and the product in the same bag: Mentioning any factor that contributed to Gutenberg's disappointing launch as a reason to not use Gutenberg in our projects should be phased out, and Gutenberg as a product should be judged only against its own qualities. This is being fair to Gutenberg the product.

I believe that, while "Gutenberg the launch" has been justly criticized, the constant scorn aimed at Gutenberg the product has been unfair (even if it were justified), and that Gutenberg the product is, itself, a victim from the stained reputation conferred to the name "Gutenberg" during its frustrating launch. For instance, when [searching for "Gutenberg"](https://wordpress.org/plugins/search/gutenberg/) in the WordPress plugin directory, because the algorithm deciding the plugin ranking factors in the plugins' rating, Gutenberg appears only around the 10th position. However, many of the 1-star ratings would not have taken place if Gutenberg had not been merged into core; had it been initially released as a plugin only, and waited until the most important bugs and issues (such as the lack of accessibility) had been resolved before merging to core, then its rating would today be higher.

If we are able to split apart the two entities (the launch and the product) and deal with them separately, then, on one side, we can do a postmortem of what went wrong during Gutenberg's launch and feed this knowledge into the current continuous delivery cycle, so that the same mistakes will not be repeated (indeed, this seems to be happening already, as I will describe below); on the other side, we can allow ourselves to appreciate Gutenberg as a product, add it to our stacks, and hopefully benefit from it.

I will do exactly this, from my own point of view.

## What Went Wrong During The Launch Of Gutenberg

In a single sentence, the team leading the process messed it up (that's the polite way to say it).

WordPress 5.0 with Gutenberg merged into it was launched in early December 2018, just before WordCamp US. Launching it then was the wrong decision, for a very simple reason: Gutenberg was not yet ready. In particular, the accessibility situation was very dire, with Gutenberg being almost useless through accessibility devices such as screen readers, effectively making anyone depending on such devices unable to use the WordPress editor. And because the WordPress community is very vocal in protecting the rights of everyone (literally everyone) to be able to access the Internet, this rushed launch was not well received.

Matt Mullenweg (who was leading the release process) may have had good reasons to be adamant about launching on that date, which could have, for instance, made sense from a business perspective. However, it certainly did not make sense from a community perspective. Indeed, many community members felt betrayed, complaining that they had to hurry to test their clients' sites even though they were on holiday. We can safely say that, for many people, such a premature launch was perceived as a wreck (even if the software was working properly, so no Y2K actually happened), which created unnecessary discontent, and which could have perfectly been avoided by either postponing the launch, or by first releasing Gutenberg as a plugin to be merged into core at a later, more stable stage. 

Was the pain, frustration and disappointment inflicted in the community really worth the cost? I believe most people will say it was not. I absolutely think it was not. In my opinion, these kind of situations in which an action is taken against the will of the majority of the community members must be avoided in the future (unless there are really good reasons for it, even if not everyone agrees on them; if that was the case concerning Gutenber's launch I do not know, since I'm unaware of any really good reason to justify it).

In his presentation during that same WordCamp US, Matt Mullenweg did acknowledge that mistakes were made during the launch of Gutenberg, and that he had learned the lesson so that these mistakes will hopefully not be repeated. I reckon we can accept his apology and trust that his decisions will be the right ones next time (even though [new quarrels on equally-important topics have taken place since then](https://wptavern.com/wordpress-poised-to-begin-implementing-proposal-to-auto-update-older-sites-to-4-7)). However, the damage is already done: A wound has opened up which may take time to heal, so the community will be less trustful until confidence in the WordPress leadership is fully restored.

{{% ad-panel-leaderboard %}} 

## Why Things Seem To Be Much Better Now

Now comes the good news: The state of affairs appears to have mostly taken a positive direction, with the improvements listed below already happening.

### Improved Communication

One of the loudest complaints about the Gutenberg launch was the lack of communication by the leadership. Because no proper channels to manage the project and communicate its decisions were put in place (at least not in a comprehensive manner), it was difficult to have an accurate picture of the overall situation. (For instance, information by different authors or teams was published through different avenues, including unofficial ones such as personal blogs.)

This concern has been greatly improved. In particular, the amount of information in the [make blogs](https://make.wordpress.org/) (where the different communities interact to take decisions concerning WordPress for different areas, such as core, accessibility, design, internationalization, and others) and the frequency with which the information is updated have been increased, and every team holds a regular [Slack-based meeting](https://make.wordpress.org/meetings/) (mostly taking place on a weekly or biweekly basis) in which anyone with a WordPress.org user account can participate. As [experienced by some community members](https://mailchi.mp/masterwp/issue-1786605?e=f77d7bf66c), it is now possible to reliably follow the developments on some topic, and have enough information to be able to become involved. 

The fallout from Gutenberg's launch also prompted Matt Mullenweg to [expand WordPress's leadership](https://make.wordpress.org/updates/2019/01/16/expanding-wordpress-leadership/) with two new roles: an Executive Director, to oversee and direct all contributor teams in their work to build and maintain WordPress, and a Marketing & Communications Lead, to lead the marketing team and oversee improving WordPress.org, related websites, and all its outlets (unfortunately, the person assigned to this role [quit not long after](https://joost.blog/why-im-stepping-down-from-my-wordpress-marketing-role/), so somebody else must be found to take over this position).

### Triage Team Formed To Tackle Open Issues

During the initial development phase of Gutenberg, several people complained that existing bugs, which had accumulated into the thousands, should be fixed before venturing out into adding new functionality to WordPress. 

In March this year, [a triage team was formed](https://make.wordpress.org/core/2019/03/01/introducing-the-wordpress-triage-team/) to clean up the open issues in the [WordPress Trac bug tracker](https://core.trac.wordpress.org/). This is hard work that has been needed for many years. If ever finished, WordPress would then have the chance to switch from Trac to a more modern bug tracker, such as GitHub.

### Accessibility Is Steadily Becoming A Non-Issue

Accessibility issues are being tackled in every new Gutenberg release, with version 6.3 providing the [lionshare of improvements](https://make.wordpress.org/core/2019/08/14/whats-new-in-gutenberg-14-august/). At the current pace of improvement, the most outstanding accessibility issues (as reported in the [Gutenberg Accessibility Audit](https://wpcampus.org/2019/05/gutenberg-audit-results/)) should soon be a part of the past.

{{% ad-panel-leaderboard %}} 

## Judging Gutenberg On Its Own Merits

Now that we have split Gutenberg the launch from Gutenberg the product, we can proceed to analyze Gutenberg as a product and decide if it is worth adding to our application stack, based solely on its own merits and shortcomings. Many people do rightfully point out Gutenberg's problems as the reason to not trust it (instead of focusing on the failed launch). However, Gutenberg has been improving by leaps and bounds, and many of the criticized issues may have been solved or may be on the brink of being solved. As such, the negative assessments should have a date of expiry and be re-evaluated. If we can give Gutenberg a new try and see where it stands nowadays, we may appreciate that, after all, it is not so bad. In my opinion, Gutenberg deserves a warmer welcome than it currently gets.

I am amazed that Gutenberg is still being compared to the previous way of editing content in WordPress (mainly through the tinymce, but also shortcodes, widgets, and others), arguing that it is more difficult to code through Gutenberg. This may be true, but it is also missing the point: Gutenberg is not here to provide a new way to code our application, producing the same features as in the past; instead, it is here to greatly enhance what can be done, offering to add features to our applications that could only be dreamt of in the past. Also, Gutenberg is not another page builder. Indeed, comparing Gutenberg to [Divi](https://www.elegantthemes.com/gallery/divi/) or [Beaver Builder](https://www.wpbeaverbuilder.com/) is similarly missing the point, because it is like comparing a Victorinox to a regular knife: Yes, you can do site/page building with Gutenberg (actually not yet, but it is already a [work in progress](https://make.wordpress.org/core/2019/09/05/defining-content-block-areas/)), but that is just one of its many uses; there are several other uses which are initially hidden, but once you pull them up from their compartment and understand how they work, a new world of possibilities will be revealed. Below, I will describe some of these new possibilities that Gutenberg brings to the table.

First, let's discuss what's not so great about Gutenberg. The one thing where I believe Gutenberg can be truly considered detrimental is in the [steep curve of learning of React](https://snook.ca/archives/javascript/difficulty-with-react) (which is the JavaScript library Gutenberg is coded with). WordPress has always been very inclusive, enabling people from any background (not only coders, but also non-techies such as bloggers, marketing people, salesmen, and the like) to create a theme or plugin or launch a site. This is beyond doubt not the case anymore, and it is unfair to expect everyone to have to learn React to create a Gutenberg block (this is not necessarily the case, since we can also create blocks using other JavaScript libraries, and even without using JavaScript, such as through [ACF blocks](https://www.advancedcustomfields.com/blog/acf-5-8-introducing-acf-blocks-for-gutenberg/), however using React is the most logical option if only because Gutenberg is coded with it). The only argument that could justify this disadvantage is [if it makes the experience better for the user](https://adactio.com/journal/13333). Let's see if this can be considered the case.

As I argued in a <a href="https://www.smashingmagazine.com/2018/11/implications-blocks-blobs/">previous article of mine</a>, the block-based architecture from Gutenberg radically changes the way in which applications are built: Instead of thinking in HTML code, we can now think in terms of components as the unit for building the website. This architecture is more maintainable and resilient, since each component (or block) can be independently developed and tested, and because it is easily reusable it can lower down the cost of developing several applications. Indeed, the recent popularity of JavaScript libraries such as Vue and React can be greatly attributed to their support for components. It is a great feature that developers love and which, I believe, once you start coding with, there is no turning back.

In this same article, I also describe how Gutenberg could support the “<a href="https://www.programmableweb.com/news/cope-create-once-publish-everywhere/2009/10/13">Create Once, Publish Everywhere” strategy</a> (also known as “COPE”), enabling to produce a single source of truth of content to feed to all of our applications, for whichever medium or platform they run on: web, email/newsletters, iOS/Android apps, VR/AR, home-assistants (like Amazon Alexa), and others. Because it makes the overall content management much simpler, COPE also enables to lower the costs of producing content for different platforms. When I first wrote my article, I was theorizing that it could be done. However, <a href="https://leoloso.com/posts/my-1st-wp-plugin/">I have recently implemented COPE for WordPress</a>, and it works like a charm! (Stay tuned for another article in which I explain how it works in detail.)

The combination of COPE and the WordPress APIs ([WP REST API](https://developer.wordpress.org/rest-api/), [WPGraphQL](https://www.wpgraphql.com/), and my own [PoP API](https://github.com/leoloso/PoP)) will provide one compelling reason for managing all of our content, for all of our applications, through WordPress. The other compelling reason will be Gutenberg's ease of use (which is not fully here yet, but at the current pace of development, will arrive sooner than later), enabling the end-user to create elaborate content in a very simple way.

We already have access to great new features, such a real-time preview of how the content looks like, copy/pasting from Google Docs with perfect formatting, creation of intricate grid layers with nested elements inside, and many others. We can also expect new blocks to deliver utterly-unexpected features we have never imagined. My bet is that, through Gutenberg, WordPress is poised to become the digital assets manager of the web. (I’ve already written an article which will soon be published here on Smashing Magazine concerning this topic and my justification for this bold statement.)

In addition, Gutenberg allows to reuse code with other CMSs or frameworks (such as [for Drupal](https://www.drupal.org/project/gutenberg) and [for Laravel](https://github.com/VanOns/laraberg)), so that coding for WordPress needs not to be restricted to WordPress anymore, once again allowing us to lower the cost to develop a library that needs to run in as many systems as possible (for instance, a company providing an integration of its API for many different platforms and languages, such as [Stripe](https://stripe.com/), could benefit from it). Currently, only the client-side code (JavaScript and CSS) seems to be re-used, however, the server-side PHP code can also be re-used. (I will, once again, soon publish an article on Smashing explaining how to do just this.)

These features are already a reality, and we can expect Gutenberg to provide many more compelling reasons for its existence in the years to come (according to Matt Mullenweg, Gutenberg has currently implemented only some 10% of its potential). 

We can finally attempt to reach a verdict on Gutenberg the product: My stance is that it establishes a higher barrier of entry to WordPress, which is regrettable, however, it also is a beautifully engineered piece of software which grants real new powers to WordPress and, due to WordPress's prominence, to the web development world in general. And between this trade-off between costs and benefits, I believe that having Gutenberg as part of WordPress is more worth it than not. I hope you can agree with my opinion or, if not, at least the reasons against it can be based solely on the characteristics of Gutenberg as a product.

## Conclusion

Gutenberg is currently at its best &mdash; having started to provide delightful user experiences that were not possible with WordPress before. However, not everyone is aware of this fact because not everyone can get down to embracing Gutenberg. This is an unfortunate circumstance because Gutenberg (as the product) should not be faulted for the mistakes that took place during the launch of Gutenberg. If we are able to split these two entities apart and treat each of them independently, we can then convincingly ask people to **give Gutenberg another chance**, suggesting that Gutenberg as a product is worth having, even if Gutenberg the launch was a failed process.

In this article, I did a postmortem of the failed Gutenberg launch, based on my own understanding of the events. Carrying out such a postmortem can help the community and the leadership make sure that those unfortunate mistakes do not happen again. After the postmortem, I proceeded to evaluate Gutenberg based on its own merits and declared my stance: I believe that Gutenberg is a great tool to have, and the WordPress community can certainly benefit from it. And because it will only be getting better and better, Gutenberg could even inaugurate a new golden era for WordPress.

{{< signature "dm, yk, il" >}}
