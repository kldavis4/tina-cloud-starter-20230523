---
title: Help Us Help WordPress
slug: help-us-help-wordpress
image: null
date: 2012-08-08T08:15:49.000Z
author: shane-pearlman
description: >-
  This is a personal request from your user, a rallying cry from a compatriot. I personally love WordPress. I make my living from it. The average user, though, couldn’t care less about it.
categories:
  - WordPress
  - Community
---
They just want to run their business, tell their family history, organize their church, share their photos or live their life online with a minimum of impedance. In its evolution from simple blogging tool to CMS, framework and software ecosystem, <strong>WordPress is losing its way</strong>. It needs us to help bring it back and cultivate simple genius.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53da68c1-d13e-461c-b251-95fb25481654/featured-image.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53da68c1-d13e-461c-b251-95fb25481654/featured-image.png" alt="Usability for WordPress by Modern Tribe" width="500" height="275" /></a>

My agency married WordPress in 2007. We’d been dating for a number of years but were still seeing others: some serious flirtation with Joomla, a blind date with Drupal, a summer romance with CMSMS, even a steady five-year stint with a custom CMS that we lovingly named Rocinante (after Don Quixote’s loyal steed).</p>

{{% feature-panel %}}

We tied the knot with WordPress for one single reason: about six to nine months after most of our projects, we would get the fateful call. “The only person who really understands how to use the website you built just left the company, and we need someone to train us!” It was almost inevitable, except on WordPress. No one ever called for help after a WordPress project except to share their excitement and book the next project. They just figured it out. It was easy and obvious and beautiful. Our clients loved it, and that was something you could grow a business on.

Then, <strong>WordPress started to grow up</strong>. New features like the menu manager, theme editor and sidebar widgets made WordPress more robust but more complicated. The ecosystem of plugins exploded. WordPress plugins are harder to use than they should be. Ask your users. We did. It was quite illuminating and a hint embarrassing. We decided to act on <a href="https://managewp.com/5-things-wordpress-doesnt-get-right">Tom Ewe’s call to arms</a> and lead by example:
<blockquote>"I find it astonishing that WordPress developers haven’t worked harder to create usability guidelines for plugin development. Even experienced WordPress users are often left guessing as to where they should go to work with a new plugin.

One of the key drivers of WordPress’ success has been plugins, and yet they are not actually that easy to use. They appear as being stapled onto WordPress, as opposed to integrating seamlessly. Surely there should be some common usability rules when it comes to plugin development?"

<em>— <a href="https://managewp.com/5-things-wordpress-doesnt-get-right">Tom Ewe</a></em></blockquote>

Recommended reading: [WordPress Essentials: How To Create A WordPress Plugin](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/)

## We Lack Conventions, And This Is Why It's A Problem

Three weeks ago, we brought on Joyce to our customer team at <a href="https://tri.be" rel="nofollow">Modern Tribe</a>. She’s smart, she has a real power-user’s/light themer’s grasp of WordPress, and she had never used our free WordPress.org-hosted plugin, <a href="https://wordpress.org/extend/plugins/the-events-calendar/" rel="nofollow">The Events Calendar</a>, nor any other of our add-ons. She came back after looking them over and said, “This is far harder to set up than it should be.” I asked her whether she had read the new user primer or the set-up instructions. “No, I didn’t. I bet most of your users don’t either.” I had to admit that Joyce was probably right. Rather than try to list all of the things that she thought might or might not work, she pointed me to Steve Krug’s SxSW talk “<span class="removed_link" title="https://schedule.sxsw.com/2011/events/event_IAP8293">Rocket Surgery Made Easy</span>.” I couldn’t turn it off. I’ll boil it down to a few paragraphs for you, but if you develop a plugin or theme or have a product business, this is a <em>must</em> hear.

Krug argues that hiring usability experts is unnecessary (heck, let’s be honest: most of us don't do it anyway). The real value of a usability test is in getting together (ideally with sushi) and observing the experience, not hearing an expert’s interpretation. Within 15 minutes of watching the first user try to use our plugin, a handful of long-running arguments were resolved and some incredibly simple hurdles were exposed. I’ll walk you through the process that we followed for a remote usability test of The Events Calendar.</p>

Recommended reading: [A Process For Professional WordPress Development](https://www.smashingmagazine.com/2012/03/process-professional-wordpress-development/)

### Our Remote Usability Test: Step-By-Step

*   Total time invested: 6 hours
*   Set-up: 1 hour
*   Testing: 3.25 hours
*   Notes: 0:45 minutes
*   Team review: 1 hour

<ol>
 	<li>Find three participants. We had enough users and visitors that a blog post generated about 15 willing offers. We gave away a free copy of The Events Calendar Pro in exchange for participation. Make sure that the criteria for participation are explicit. Krug insists that you really don’t need more than three users, and that turned out to be spot on. By the third user, we were accurately guessing where they would fail. Schedule the test to last about 30 minutes to an hour, depending on the tasks, and give yourself time in between to clean up your notes and deal with other details.</li>
 	<li>Think of some process or features you want to explore. We were curious to see how first-time users experience our core Events plugin. With that in mind, we made a series of nine steps that we knew were pretty common for setting up the calendar. Make sure to write them out, and give goal-based instructions, not actual steps. Think, “Create a new event,” rather than “Click the new events menu to make an event.”<a href="/wp-content/uploads/2012/07/test-steps.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86511502-6a54-4d6f-919d-d91a4b8d1416/test-steps.png" alt="Steps for Testing The Events Calendar 1st Time User Experience" width="500" height="320" /></a>
Here are the steps we chose for our usability test to explore the first-time user’s experience.</li>
 	<li>Set up a domain with WordPress and your plugin or theme on it. If you are testing a plugin, decide whether the problem or feature set that you defined in step 2 is best served by a fairly vanilla build (for example, 2011 theme + minimal plugins + no content) or by a more real-world build (perhaps use your demo content if you have one or a user’s website backup). Configure the whole website precisely for the first step. Run through it once entirely to make sure you haven’t forgotten anything obvious.</li>
 	<li>Back up the database of the website so that you can restore between tests.</li>
 	<li>Grab a copy of <a href="https://join.me">Join.me</a> or your favorite screen-sharing or VoIP tool (such as <a href="https://www.gotomeeting.com">GoToMeeting</a> or <a href="https://www.adobe.com/products/adobeconnect.html">Adobe Connect</a>). We found that Skype just wasn’t stable enough to carry us through the screen-sharing portion of our test run. Join.me functioned amazingly well, except for an issue with voice echo caused by laptop sound cards during one test. The fact that it was free was appealing. Make sure that both screen-sharing and voice are available in whatever set-up you choose and can be recorded together. We used <a href="https://www.telestream.net/screen-flow/">ScreenFlow</a> to record the test so that it could be reviewed later.</li>
 	<li>Do a quick test run with someone on your team (or your mom), and make sure that the kinks are worked out.</li>
 	<li>Get the whole team ready and present. Do whatever you can to get people to participate. Everyone on our team who participated was blown away by the experience. Buy them fancy snacks or digital beer. Fire up a chat session if your team is remote (one that the test participant is not privy to) so that your team can chat freely. If you are co-located, make sure the team is not in the room where the test is taking place. Twelve people hovering over someone’s shoulder will unnerve even the most confident person.<a href="/wp-content/uploads/2012/07/skype-chat.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1746d5d-c619-4690-bfb1-e135e247a444/skype-chat.png" alt="Discussing test as it happens with the team" width="500" height="230" /></a>
Discussing the user’s choices and challenges with the developers in real time.</li>
 	<li>The introduction and set-up are key. <a href="https://www.sensible.com/downloads-rsme.html">Krug has a great script</a> that we just followed. The first key: explain to the participant that the plugin is being tested, not them. There is no wrong or stupid choice. If something is hard or confusing, it’s our fault and we apologize. Secondly, encourage the participant to speak out loud and share their thoughts; i.e. provide a guided monologue. Give them a copy of the steps (paste them into the chat session or email them beforehand), and read them through together once.</li>
 	<li>Read a step. Watch. Shut up (bite tongue). The goal is to watch them as if you weren’t there, so don’t help them. This can get crazy awkward, but observing the various choices they make in trying to accomplish a goal becomes very informative. Consistently ask questions to get them to speak out loud, such as “What are you thinking?” and “What did you expect?”<a href="/wp-content/uploads/2012/07/user2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b903852-19bf-4125-83fb-adc0898bd14d/user2-crop.png" alt="Watching user 2 during the usability test." width="500" height="270" /></a>
Observing user 2 figure out where to add events to her menu. (<a href="/wp-content/uploads/2012/07/user2.png">Large version</a>)</li>
 	<li>Have the moderator and the people observing take notes on what they see, and discuss together.</li>
 	<li>Once all of the steps were completed, we asked a bunch of probing questions. We were surprised by how much two users employed the admin bar, so we asked more about that. We were curious why no one clicked the tutorials, despite having the answer in the title. And on and on.
<figure><a href="/wp-content/uploads/2012/07/tutorials.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cad1d497-de15-4344-a75b-d4ed2c6865ed/tutorials-minified.png" alt="Changed tutorials from a blog loop to an organized page." width="500" height="218" /></a><figcaption>Usability has to do with more than what’s in a plugin’s admin settings. We probed why none of the users took advantage of the tutorials. It turned out that a blog loop has no useful organization, so we made a quick page to group the posts by topic. (<a href="/wp-content/uploads/2012/07/tutorials.png">Large version</a>)</figcaption></figure></li>
 	<li>Time to pay the participant in money, karma or free goods and get ready for the next test. Reset the website’s database.</li>
 	<li>Take some time to condense your notes. Ask everyone who observed to pick the three most important things that can quickly be fixed based on the test. The goal is <em>not</em> to do a redesign; we are looking for quick course corrections. Then we test again in a new cycle.
<figure><a href="/wp-content/uploads/2012/07/user1-notes.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68ec7e9-bea8-44a1-b7e4-3684be05482c/user1-notes-crop.png" alt="Notes from test of user 1." width="500" height="417" /></a><figcaption>Notes were broken down into observations, user recommendation and bugs. (<a href="//www.smashingmagazine.com/wp-content/uploads/2012/07/user1-notes.png">Large version</a>)</figcaption></figure></li>
</ol>

### Findings From Our Tests

A number of our major debates were instantly answered. For example, we had had a prolonged disagreement about the placement of the menu item for the plugin’s settings. The majority of the development team felt that it belonged in WordPress’ main “Settings” tab because that is a de facto standard. A minority of developers and all of the community team thought that putting it in the submenu for the Events custom post type would be more intuitive.

Recommended reading: [Guide To WordPress Coding Standards](https://www.smashingmagazine.com/2012/07/guide-wordpress-coding-standards/)

Both sides had great arguments. For the test, we put it in the WordPress settings, and then we watched three users in a row fail to find it there in a reasonable timeframe. One found it from the top admin toolbar (we put it there, too), one eventually looked in WordPress’ “Settings,” and one gave up despite looking right at it three times. Standards are great, but we all had to admit that functionality has to supersede a poor standard. We explored putting it in both places, but ultimately we decided to move it to the Events menu for now due to technical limitations.

<a href="/wp-content/uploads/2012/07/settings-menu.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b03b16e-335b-4699-b0c5-9ea49a49d7d0/settings-menu.png" alt="Moved settings to events cpt menu from general WordPress settings menu." width="500" height="350" /></a>
We moved the “Settings” menu item from WordPress’ general “Settings” menu to the menu for the Events custom post type, which is where our users expect to find it, despite WordPress’ standards.

We also saw how hard a time users had finding the events calendar on the front end of the website, despite it being in five locations. By seeing where people looked for it, we came up with a game plan that took five minutes to implement, and we hope it will make it a whole lot more intuitive.

<a href="/wp-content/uploads/2012/07/view-calendar.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef65fba2-71ff-4046-b560-e93678f71852/view-calendar.png" alt="Added view calendar links throughout the plugin." width="500" height="419" /></a>
We added “View calendar” links to the admin bar at the top of the “Events” menu and in the settings.

The usability test was so valuable that Paul, one of the developers, asked if we could do it every month. Usability testing has, without a doubt, provided the best feedback we have ever gotten on our product, it cost very little, and it has now been added to the monthly production schedule. We will be testing these updates next week to see if they truly did improve the experience.

I’m continually amazed by a community’s ability to reach the same conclusion at the same time. Last week, Dave Martin <a href="https://make.wordpress.org/ui/2012/06/22/hey-everyone-my-name-is-dave-martin">posted for the first time</a> to the core UX team’s blog:
<blockquote>I’m just getting my feet wet, and quite honestly haven’t a clue where to get started, so I thought I’d set up a quick user test (I’m a big fan of user testing). I set up a temporary WP install, and ran a user from usertesting.com through a couple scenarios.</blockquote>

Check out the video. It almost hurts to watch her struggle. I can’t tell you how grateful I am to see the core team paying attention as well and engaging quickly. It is a great start.</p>

## Call For WordPress Human Interface Guidelines

The average website has over five plugins installed (according to PressTrends) and often a theme options panel. For a great experience to continue throughout the website as people actually experience it, we need to establish strong standards for the rest of the community to follow.

I am calling all WordPress plugin developers and themers. You don’t need to guess what your users might want or how they will experience your product. <strong>Just watch them.</strong> We know it: if we focus on usability, stability and then value, we can make products that users will line up for.

To the core WordPress team and the community at large: Let’s get together and <strong>create WordPress human interface guidelines</strong> for those who contribute by providing plugins and themes for the world to use. <a href="https://developer.apple.com/library/ios/#documentation/userexperience/conceptual/mobilehig/Introduction/Introduction.html">Apple gave us a rock</a> and upon it built a foundation that few can deny. Google finally <a href="https://developer.android.com/guide/practices/ui_guidelines/index.html">got around to it with Ice Cream Sandwich</a>, and I expect to see drastic improvement in the wild west that is the Android application landscape. Help us help WordPress.

In the words of Matt Mullenweg when he saw Dave’s first post:
<blockquote>Thank you very much for this, I think more frequent and more transparent testing will allow us to make much better informed product and UX decisions. If we do this right we should see the videos get better and better (shorter and less confusion) from release to release.</blockquote>

Code is poetry. So should be your user’s experience.

{{< signature "al" >}}

&nbsp;

