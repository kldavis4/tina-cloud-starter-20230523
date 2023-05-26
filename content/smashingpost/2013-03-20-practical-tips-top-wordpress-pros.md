---
title: Practical Tips From Top WordPress Pros
slug: practical-tips-top-wordpress-pros
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f012832-3f0b-4a08-be78-c875a0fbb64d/wp-10.jpg
date: 2013-03-20T12:51:16.000Z
author: siobhan-mckeown
description: >-
  Recently I shared with you some advice from the WordPress community to
  beginners. But what about if starting out is already a dim and distant memory?
  What if you're already so **immersed in the world of WordPress** that you
  dream of trac and bore your partner with talk of the latest thing you've
  achieved with custom post types?
categories:
  - WordPress
  - Techniques (WP)
---
Recently I shared with you some <a href="https://www.smashingmagazine.com/2013/02/01/wordpress-community-offers-advice-beginners/">advice from the WordPress community to beginners</a>. But what if starting out is already a dim memory? What if you’re already so <strong>immersed in the world of WordPress</strong> that you dream of Trac and you bore your partner with talk of your latest achievement with custom post types?

Below are some tips from WordPress pros from across the community. Many of the tips cover development, but there’s also advice on business, running your website and, of course, getting involved with the community.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af7a65b7-6dc7-4360-bfe9-453cb57ce8b2/wordpress-start-image.jpg"><img loading="lazy" decoding="async" class="108643" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af7a65b7-6dc7-4360-bfe9-453cb57ce8b2/wordpress-start-image.jpg" alt="Wordpress-start-image" width="500" height="357" /></a><br>
<em>Image: <a href="https://www.flickr.com/photos/oakleyfamily/4919659112">Phil Oakley</a></em>

## Tips For Developers

### Use Everything WordPress Has To Offer

WordPress’ core can do a lot for you, without you having to write a bunch of code. WordPress is much more powerful when you make use of its APIs and built-in functionality. “If you use WordPress as your framework,” says Trent Lapinski, “it will enable you to focus on developing an innovative plugin or theme.”

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[Using WP_Query In WordPress](https://www.smashingmagazine.com/2013/01/using-wp_query-wordpress/)</span>
*   [Powerful WordPress Tips And Tricks](https://www.smashingmagazine.com/2013/09/powerful-wordpress-tips-and-tricks/)
*   [WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)
*   <span>[Moving A WordPress Website Without Hassle](https://www.smashingmagazine.com/2013/04/moving-wordpress-website/)</span>

<a href="https://matty.co.za/">Matty Cohen</a> recommends always looking for and using functionality available within WordPress before creating a function from scratch. “Examples of this include, at the higher level, using the WordPress Settings API and, at the lower level, using the <code>media_handle_upload()</code> function to upload your files, rather than a custom upload routine.” Matty gives an example of this with his <a title="WooSlr " href="https://www.woothemes.com/products/wooslider/">WooSlider</a> plugin. In order to create a familiar and consistent experience for <a href="https://woothemes.com/">WooThemes</a> users, he did the following:

*   He used the Settings API for the settings screen.
*   He added a tab to the “Upload/Insert Media” popup for creating shortcodes. This interface uses a combination of the Settings API, custom form-creation logic, and some custom JavaScript to create the HTML output and the shortcode.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af825988-64b4-4748-b23b-06ed6d87df80/wooslider.jpg"><img loading="lazy" decoding="async" class="78211" title="wooslider" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af825988-64b4-4748-b23b-06ed6d87df80/wooslider.jpg" alt="Screenshot of WooSlider settings" width="500" /></a><br>
<em>WooSlider uses built-in WordPress functionality to make the user experience better.</em>

Making use of everything WordPress has to offer results in less coding for you and a better overall experience for users. But those aren’t the only benefits. <a href="https://amyhendrix.net/">Amy Hendrix</a> points out that the code you write will be future-proof. Writing your own scripts could eventually result in conflicts.</p>

### Use Hooks

<a href="https://codex.wordpress.org/Plugin_API#Hooks.2C_Actions_and_Filters">Hooks</a> are the means by which you hook into WordPress and add your own code without modifying core files. There are two types of hooks: actions and filters. Action hooks are places where you can insert and run code. Filters are used to manipulate output.

If you’re working with WordPress’ core and with plugins and themes, then you should be extending by making use of all of the hooks available. Adam Brown maintains a <a title="WordPress hooks database - action and filter hooks for wp plugin developers -- Adam Brown, BYU Political Science" href="https://adambrown.info/p/wp_hooks">list of all of the hooks</a> that have ever appeared in WordPress.</p>

### Implement Hooks

Create your own hooks. By implementing hooks in your plugins and themes, you create opportunities for other people to extend them and create add-ons. <a href="https://tri.be">Shane Pearlman</a> believes that by doing so, you “encourage plugin developers to make opportunities for the community to extend and also use them.”

Not only does this create opportunities for other developers, but you make life easier for yourself. “With a ‘well-hooked’ theme or plugin,” says <a href="https://codeforthepeople.com">Simon Wheatley</a>, “you can make adjustments between clients, or between sites on a multisite setup, a lot more easily than by effectively forking your own code for every scenario.”

### Write Secure Code

If you write plugins or themes, keeping the code secure is critical. How bad would you feel if your code was responsible for websites getting hacked? <a href="https://webdevstudios.com">Brad Williams</a> recommends learning <strong>how data validation pertains to WordPress</strong>. A detailed <a href="https://codex.wordpress.org/Data_Validation">page on data validation</a> can be found in the Codex; so, if you’re a developer, you have no excuse for writing insecure WordPress plugins and themes. Following the guidelines will ensure that your code is safe and secure from exploits and hacks. As <a href="https://ryanhellyer.net">Ryan Hellyer</a> points out, “Having a beautiful website which does exactly what a client requires is great, but it’s not so great when it gets injected with spam links and is de-indexed from search engines!”

### Follow Best Practices

Ryan Duff and Brad Williams highlight some best practices that developers should stick to:

*   Make sure the data that you’re passing is always being passed in the way it’s expected to. Setting a variable on an incorrect line could result in a trickle-down effect of error messages.
*   WordPress has [coding standards](https://codex.wordpress.org/WordPress_Coding_Standards "WordPress Coding Standards « WordPress Codex"), so stick to them. This will keep your code in a format that all WordPress developers will recognize, making bug tracking much easier!

### Embrace the Code Base

Both <a href="https://helenhousandi.com/">Helen Hou-Sandi</a> and <a href="https://10up.com/">Jake Goldman</a> of 10up recommend that you spend time looking at the code base. As Jake points out, “Relying on the Codex and Google searches for solving unique problems with WordPress is like trying to tune a car’s performance without ever looking under the hood.” <a href="https://rachelbaker.me/">Rachel Baker</a> also suggests looking at the change logs, and Silviu-Cristian Burcă points us to his advice in “<a href="https://scribu.net/wordpress/how-to-become-a-wordpress-guru.html">How to Become a WordPress Guru</a>.”

A good integrated development environment (IDE) for PHP — such as NetBeans, PhpStorm, phpDesigner or Vanilla Eclipse — will offer <strong>code auto-completion for WordPress functions</strong> and their arguments and will display documentation on functions inline. You’ll be able to easily jump to function and class declarations to study them. “Think the core code base is too scary?” asks Jake. “Pick a file in <code>wp-includes</code> and start reading — you might be surprised by how approachable it is, and how much you can learn."

Looking at the code, as Helen adds, also increases the likelihood that you’ll find a way to contribute code to the WordPress project. You’ll also become familiar with plugins and themes, understand how people do things properly, and recognize when they get it wrong.</p>

### Share Your Code

It’s in the nature of code in an open-source project to be shared, forked and iterated on. If you’re working on solutions, then share them with the community. “Share and publish your solutions, as a plugin, widget or theme,” says <a href="https://www.catiakitahara.com.br/">Cátia Kitahara</a>. “Not for every project, but with most of them, we end up with a solution that could be of use to many others. So, do it as a way of giving back to the community. I know it takes time to prepare something to be distributed through the repositories, but remember the time WordPress saves for us!”

You could put your code on <a href="https://github.com/">GitHub</a>, which <a href="https://ben.balter.com/">Ben Balter</a> recommends:
<blockquote>"GitHub’s got a very different culture, and the ability for anyone to submit a pull request is a real game changer. It really lowers the barrier to contribute, and democratizes the entire plugin authoring experience. As a bonus, use GitHub’s built-in wiki functionality to maintain your plugin’s documentation (especially FAQ), so that anyone, even non-technical users, can contribute.

Lastly, if you have plugin tests, integrate with Travis CI so that you can automatically test pull requests before merging. To help you get started, a handful of tools are out there, such as GitHub → WordPress.org deployment scripts and GitHub wiki → WordPress readme converters."</blockquote>

<a href="https://jumping-duck.com/">Eric Mann</a> points out that if you’ve built your project in isolation, then you’re likely missing out on different approaches. Sharing your code with people gives them the opportunity to point out how it can be improved. WordPress itself is built collaboratively and is the result of hundreds of minds looking at it from different perspectives. If you want your code to excel, you should be sharing it, too.</p>

### Use Custom Post Types

Taking advantage of custom post types for specific use cases is a great way to <strong>leverage WordPress</strong>. At the <a title="The Theme Foundry" href="https://thethemefoundry.com">Theme Foundry</a>, Drew Strojny has three custom post types: themes, stories and tutorials. This enables members of his team to quickly find and create content.

Drew recommends making custom post types even more flexible by adding custom meta data. This enables you to style your content and provides opportunities to reuse that meta data across your website. He provides the example of the meta data he uses with the “Story” post type in use on his “<a title="Stories — The Theme Foundry" href="https://thethemefoundry.com/stories/">Customer Stories</a>” page.

<a href="https://thethemefoundry.com/stories/"><img loading="lazy" decoding="async" class="78211" title="core team" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab38e683-b7f6-4f29-a4ca-e88e516b815d/themefoundry.jpg" alt="a screenshort of a theme foundry story" width="500" /></a><br>
<em>Theme Foundry uses custom post types to display customer stories.</em>

Four pieces of meta data are collected: “Location,” “Site title,” “URL” and “Theme name.” These are outputted as part of the post itself. But the meta data can also be used to output the latest story for a theme on the <a title="Portfolio — A WordPress theme by The Theme Foundry" href="https://thethemefoundry.com/wordpress/portfolio/">product page itself</a>.</p>

### Think of Your User

When you develop with WordPress, you’re usually producing something that will be used daily by the average WordPress user. So, the interface should fit their needs. Starting off with the user workflow and interface, while keeping code in mind, will make for a better experience for users. Helen Hou-Sandi points out the following:
<blockquote>"It is certainly harder to mold an interface to the unknown average user, but worth the effort. A user keeps coming back because they feel confident using your software, and the interface is a huge part of that comfort. Good code behind the scenes is good for the user, but unless they can see or feel the positive results, they may never know."</blockquote>

Andrea Rennick takes this even further, suggesting that “every so often, <strong>spend some time with a new user</strong>. It will open your eyes to the things you take for granted.” If you go to WordPress events, talk to novice users of your plugin to find out how they interact with it. If you run a WordPress business, spend some time with your newest members to see how they are getting on with your product. This sort of feedback is invaluable.</p>

### Provide Support

It’s not for punishment that new Automattic employees spend three weeks providing support, and that each team does a week of support every year. It keeps the people who write the code close to the people who use the product. It’s easy for developers to work in a bubble and forget about the users they are developing for. <strong>Stop seeing support as a chore</strong>; see it as an opportunity to stay in touch with the people who use WordPress. Andrea Rennick says this:
<blockquote>"I heartily believe everyone should spend a bit of time doing support, just to remember what it’s like being a new user. It can also open your eyes to potential issues in the software, in the UX, and just give a better sense of people’s expectations and assumptions."</blockquote>

Even if you’re in the enviable position of employing supporters to do most of the work, as long as you write code or create products for WordPress, take some time to answer support threads and to stay in touch with your users.</p>

### Tools

Developers have recommended a number of tools.

Use the <a href="https://github.com/Automattic/developer">Developer Tools</a> plugin from Automattic to eliminate all notices, especially deprecated notices. You’ll see a performance boost on websites that get a lot of traffic. <a href="https://zippykid.com">Vid Luther</a> points out that you slow down your side by 20 milliseconds for every notice your code throws out, and 40 milliseconds for every deprecated notice your code throws out. “Even if you have error reporting turned off,” says Vid, “it’s still shitty code.”

<a href="https://tri.be/">Timothy Wood</a> recommends using <a title="Sublime Text - Download" href="https://www.sublimetext.com/2">SublimeText2</a> as your development IDE. It’s cross-platform, lightweight and fast, and it improves code. “The goal of a good developer,” says Timothy, “is to be efficient in the code and to spend time using thought instead of (brute) code force.” He keeps a <a href="https://gist.github.com/3418928">list of SublimeText2 add-ons</a> that he finds useful.</p>

## Managing Your Website

### Keep Your Website Secure

Keeping your WordPress website secure is important. I wrote about this a few months ago, <a title="Common WordPress Malware Infections" href="https://www.smashingmagazine.com/2012/10/09/four-malware-infections-wordpress/">highlighting the types of attacks</a> that a website could come under. The little guys aren’t the only ones who get hit; huge websites are susceptible, too. Here are Dre Armeda’s top tips for keeping your website secure:

1.  Don’t leave outdated software on your server, including old installations that you no longer use. If it’s not in use, remove it. If it’s outdated and you need it, update it.
2.  Limit access. Not everyone needs to be an admin, and **not everyone needs FTP or SSH access**. Give folks enough access to do their job, nothing more. When they are done, remove access. This should include every account on the server that has access ranging from WordPress to the server.
3.  Managing passwords is key. Using 12345 is not a good idea. Use different passwords for your accounts, and use a lot of characters, including numbers, symbols and both cases. Using a password manager where possible is also wise.

You’re going to feel stupid if you work professionally with WordPress and you get hacked. “This applies to everyone,” says Dre, “and I think it is even more important for WordPress pros. You don’t want to be in a position where you’re hacked or infected with malware because you weren’t taking care of the common sense basics. Be a pro, be a leader. Minimize the risk of security issues for you and your users.”

### Back Up Your Website

Good backup practices are really important. What if your website is hacked or your server fails? <a href="https://wpbeginner.com">Syed Balkhi</a> recommends not simply relying on regular database backups either. Without all of your other data, such as images and plugins, your backup is incomplete. Syed recommends a service such as <a href="https://vaultpress.com/">VaultPress</a> or <a href="https://ithemes.com/purchase/backupbuddy/">BackupBuddy</a>. As <a href="https://envato.com">Collis Ta’eed</a> points out, you should “test regularly, and make sure you do a decent verification to ensure the backup is actually, completely, fully there and working. You don’t want to find out your backup wasn’t working… on the day you need it.”

## Running Your Business

### Collaborate in Business

<a href="https://wysija.com">Kim Gjerstad</a> points out that the WordPress economy is a bit of a gold rush right now. People are rushing in, setting up businesses and making money. People assume that they should keep ideas to themselves, otherwise people will steal them. In reality, once you start to scale your business, you should start collaborating. The only way to do this is to start talking to other developers and business people. “Nobody’s really going to steal your ideas,” says Kim. “It takes a year to two years to become profitable in many start-ups, so it’s not like your idea is going to be stolen overnight. Go find the right people; talk to the right people.”

Similar advice comes from <a href="https://page.ly">Josh Strebel</a>, who recommends collaborating regularly, but choosing your partners carefully.
<blockquote>"It is good practice to collaborate as often as possible to avoid the duplication of effort and gain a wider audience for your wares. However, be diligent about who you choose to hitch your wagon to. Not all partnerships are in the best interest of both parties from a public relations or economic viewpoint."</blockquote>

### Know Your Mobile Audience

More and more people are using portable devices to access the Internet. So, we can’t just build websites for big screens anymore. <a href="https://www.isaackeyet.com/">Isaac Keyet</a> is the lead for the <a href="https://make.wordpress.org/mobile/">WordPress.org Mobile Group</a>. He says:
<blockquote>"We constantly hear how important mobile is, and how people are using their portable devices more and more to access the Internet. But just how this happens varies widely from continent to continent, country to country. If you want to target developing countries, a responsive theme or app may not be enough — you may have to consider a very basic layout and/or a mobile site to gain full traction.

Other parts of this world do not speak English at all. If your site is not translated correctly, you’ll miss out. It’s a global world and mobile devices have democratized people’s ability to access the Internet."</blockquote>

### Reduce Support Load

In addition to providing support, make an effort to reduce your support load. To do this <a href="https://www.fredericktownes.com/">Frederick Townes</a> recommends consistency. “Cultivating success,” he says, “is the result of countless small (and sometimes large) victories that occur in aggregate and culminate in some outcome.”

By reducing your support load, you can <strong>spend more time creating value for customers</strong>. Frederick suggests the following ways to achieve this:

*   Create secure, well-documented and reliable code.
*   Pick the right tools for the job.
*   Remember that users don’t read manuals, so design usable interfaces with pointers, tooltips and captions.
*   Localize wherever possible.
*   Make FAQs and canned responses available.
*   Iterate on feature requests.
*   Nurture advocates who love your project and who will help others and figure out how to get new advocates.</p>

### Find a Niche

<a href="https://andrewnorcross.com/">Andrew Norcross</a> points out that WordPress has a lot of venues for people to use their skill set. Expand your own skills, while maintaining a strong focus. This could be in themes, plugins, front-end design, support, writing, etc. You could focus on developing with a particular framework, such as Genesis, or with the products of a particular theme shop, such as WooThemes. As <a href="https://www.bluelimemedia.com/">Christine Rondeau</a> puts it:
<blockquote>"Saying you build WordPress sites is like saying you build houses. It’s simply not clear enough, and you need to drill down and be really clear about your niche. It’s also important that your niche brings you joy; otherwise, there’s no point."</blockquote>

### Educate Your Clients

<a href="https://halfelf.org/">Mika Epstein</a> notes that one of the most common reasons she hears people give for why they can’t do the right thing is, “My client doesn’t want it.” Her reply is, “It’s time to educate your clients.” Don’t let your clients force you into making bad choices. Remember that you are the expert — that is why they are paying you.

Mika has two recommendations for dealing with clients in this situation:

*   Educate them on why what they’re doing is bad.
*   Make it easier for them to do the right thing for themselves.

By educating them and creating the right tools, you make it easier for them to avoid link scams, SEO black hats and other bad practices. This makes the Web better for everyone.</p>

## Get Involved In The Community

Whether you’re a beginner or a pro, getting involved in the community is a great way to hone your skills. <a href="https://thewpvalet.com">Mason James</a> suggests getting involved with <a href="https://core.trac.wordpress.org">Trac</a>. If something doesn’t work, report it! The more feedback is provided, the quicker the software will progress.

Communicate with other members of the community. <a href="https://pippinsplugins.com">Pippin Williamson</a> says that he loves a lot of different software, but most of them are just pieces of software, “whereas WordPress is a piece of software that keeps me involved with dozens (or hundreds) of the best people I’ve ever met. It’s this involvement that makes my usage and development work in WordPress so fulfilling.”

<a href="https://byotos.com">Paul Gibbs</a> notes that he has become a better developer because he has worked with the people who build the software. He recommends taking every opportunity to meet new people, to collaborate on projects and to talk to your audience and customers.

“WordPress,” says Paul, “gives you a sandbox in which to build your dreams.”

### Contribute

Once you become involved in the community, look at ways to contribute back to it. <a href="https://markoheijnen.com/">Marko Heijnen</a> says that the learning curve is big and that you’ll learn a lot from others. You’ll also become more tightly integrated in the community. “WordPress has a great karma currency,” says <span class="removed_link" title="https://logicalbinary.com/">Tammie Lister</span>. “From contributing to passing on what you learn, you’ll reap the rewards.”

<a href="https://en.wp.obenland.it/">Konstantin Obenland</a> points out that there are plenty of ways to get involved in WordPress. You don’t just have to get involved with core — you could contribute to the <a href="https://make.wordpress.org/themes/">Theme Review Team</a>, for instance, where you’ll enhance your knowledge of best practices. <a href="https://kovshenin.com/">Konstantin Kovshenin</a> says:
<blockquote>"Get involved. Follow WordPress development, read the trac, follow changesets, follow weekly dev chats. Study the core contributor handbook, help with beta testing, help reproduce trac issues, submit a patch, write a unit test, go to a WordPress event (meetups, WordCamps, etc.), organize a WordPress event, spread the word and knowledge, blog about your experiences."</blockquote>

## Learn

“You’re never too smart to learn,” says <a href="https://theandystratton.com/">Andy Stratton</a>. “In fact, the smartest people don’t know everything; they just know when to ask questions and learn.” WordPress is vast, and there is always more to learn. Andy suggests making a list of things you want to learn in one month, two months, six months and twelve months. “Speak at a WordCamp, build a custom widget, work with the HTTP API, create custom rewrite rules, etc. At least every three months, you should be able to say you’ve accomplished or learned something new.”

### Do Peer Review

“Peer review is one of the best things you can do for your development workflow,” says <a href="https://japh.com.au/">Japh Thomson</a>. Ask a trusted friend or colleague to look over your plugin, theme or functionality. Japh outlines the ways that this helps:

1.  Your reviewer could remind you of any best practices that you might not have been aware of or had forgotten about during the development process.
2.  Your reviewer could also let you know about a **better approach** that you hadn’t thought of.
3.  Your development will benefit just from your knowing that someone else is looking at your code!

Japh adds:
<blockquote>"If you think this is something that those holding the purse strings might consider an unnecessary expense, consider integrating it with other parts of the process — such as documentation, where the reviewer creates documentation as they review, and also knowledge sharing, so that at least one other developer on your team knows and understands the code you’ve written (you know, the whole “bus factor”)."</blockquote>

### Be Open to Criticism

Whoever you are, whatever profession you’re in, taking criticism can be hard — especially if you’ve worked really hard on something and someone points out its flaws and tells you that you’re doing it wrong. Yet the nature of an open-source community is for people to take what you’ve done and improve upon it. Kailey Lampert talks about this from the perspective of a developer:
<blockquote>"We can get to be really proud of code we’ve put a lot of time into. And we love it when someone agrees that our code is clever and clean. But believe it or not, sometimes we make mistakes, and people notice. It can be almost heartbreaking to hear someone tell you all the ways you could have made your code better. It may be tempting to never release code again for fear of being embarrassed, but with that attitude, how can we grow? Be humble, take the advice, learn from it, and make new mistakes next time."</blockquote>

### Read the News

There are a lot of ways to stay up to date on what’s happening with WordPress. <a href="https://zed1.com/journalized/">Mike Little</a> recommends subscribing to the <a href="https://make.wordpress.org">Make WordPress.org</a> blogs, and even the <a href="https://codex.wordpress.org/Mailing_Lists#Trac">Trac mailing list</a>. “Keep an eye on them, and learn what is coming up,” he says. “It may affect the work you are doing now, and certainly will in the future. If you are still writing the same code now that you were writing a year ago, you are out of date.”

By following other WordPress developers on Twitter and GitHub, you’ll find scripts and tools that others have written. <a href="https://www.jaredatchison.com/">Jared Atchison</a> has developed his own set of tools but finds that the tools others share often do it better. <a href="https://stephanis.info/">George Stephanis</a> and <a href="https://kpayne.me/">Kurt Payne</a> have some great suggestions on places you can tap into to get information:

*   Attend the weekly [#wordpress-dev](https://make.wordpress.org/core/weekly-developer-chats/) and [#wordpress-ui](https://make.wordpress.org/ui/) chats.
*   Sign up for the [wp-hackers](https://lists.automattic.com/mailman/listinfo/wp-hackers "wp-hackers Info Page") mailing list.
*   Read the core development [chat logs](https://irclogs.wordpress.org/).
*   Follow WordCamp hashtags.
*   Meet people face to face at [WordCamps](https://central.wordcamp.org/ "WordCamp Central | WordCamp is a conference that focuses on everything WordPress.") and [meetups](https://wordpress.meetup.com/ "WordPress Meetup Groups - WordPress Meetups").
*   CC (carbon copy) yourself on any [Trac](https://core.trac.wordpress.org/ "WordPress Trac") tickets that you’re interested in.

Staying up to date on WordPress will help you improve over time.

<a href="https://dougal.gunters.org/">Dougal Campbell</a> has this to say:
<blockquote>"If you stay isolated and develop in a vacuum, you are going to miss out on all sorts of useful discoveries. I try to keep myself on top of things, and I can’t tell you how many times I’ve seen a blog post or tweet that made me say, “I didn’t know about that function!”"</blockquote>

In addition to keeping up with what’s happening on WordPress, <a href="https://upthemes.com">Chris Wallace</a> stresses the importance of keeping up with new plugins. You need to know whether the plugins you use do what they do best. You never know when a new plugin will appear that surpasses all of its competitors.</p>

## Do What Makes You Happy

If you work with WordPress, then you’re probably in the happy position of being inundated with work. There is great demand for people with WordPress expertise, so make sure to <strong>get paid to do what you like doing</strong>. Market yourself to the types of clients who will provide you with work that makes you happy. <a href="https://boone.gorg.es/">Boone Gorges</a> talks about his experience:
<blockquote>"I’m passionate about education and academic institutions, and about building free social software that helps these kinds of organizations do their work better. So, first of all, I market myself to educational institutions, and tend to turn down most work outside of that area.

Then, I only take on projects that either will become standalone free software projects or will contribute back to a project like BuddyPress. This strategy helps me to make the most of my time, since I’m getting paid to do work that, in many cases, I would eventually have done in my free time."</blockquote>

Find clients in the field that you’re passionate about. In the end, you’ll be happier, and you’ll do work that you find rewarding.</p>

### Some Final Tips

Below are some final tips that didn’t quite fit elsewhere.

<a href="https://tinybit.co.jp/">Seisuke Kuraishi</a> says:
<blockquote>"Do ego searching. In most cases, people won’t come directly to you to tell you the problem with your plugin or theme."</blockquote>

<a href="https://danieldvork.in/">Daniel Dvorkin</a> says:
<blockquote>"Performance and ability to scale shouldn’t come after the fact. It’s a mentality you should have while developing. If you’re planning to make your code public, always assume that your code already needs to scale."</blockquote>

<a href="https://markjaquith.com/">Mark Jaquith</a> says:
<blockquote>"If you get a lot of comments, enable and learn the keyboard shortcuts for moderating comments. (This is a per-user option, so set this in your profile.) This will save you a lot of time!"</blockquote>

<strong>Tip</strong>: <em>If you happen to be searching for a helpful cheat sheet of WordPress keyboard shortcuts, here's one you can bookmark and even print out: "<a href="https://www.exhibithire.co.uk/other-resources/wordpress-keyboard-shortcuts">Wordpress Keyboard Shortcuts Cheat Sheet</a>".</em>

<a href="https://woothemes.com/">Magnus Jepson</a> says:
<blockquote>"Use a child theme when customizing a theme, and keep the parent theme updated, along with WordPress and all of your plugins. Minimize the number of plugins you have activated, and delete any inactive plugins for security reasons."</blockquote>

Got your own tips? Let us know in the comments!

{{< signature "al" >}}

