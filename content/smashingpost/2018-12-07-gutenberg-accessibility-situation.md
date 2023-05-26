---
title: 'What Can Be Learned From The Gutenberg Accessibility Situation?'
slug: gutenberg-accessibility-situation
author: andy-bell
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dd5f574-b39f-486c-9177-c97132bcab6f/gutenberg-situation-sharing-image.png
date: 2018-12-07T11:30:08+01:00
summary: >-
  WordPress has a brand new content editor called “Gutenberg” that is going to shape WordPress for years to come. In this article, Andy Bell explains why it’s a movement and not just a new editor.
description: >-
  WordPress has a brand new content editor called “Gutenberg” that is going to shape WordPress for years to come. In this article, Andy Bell explains why it’s a movement and not just a new editor.
categories:
  - WordPress
  - Accessibility
  - Plugins
---
So far, Gutenberg has had a very mixed reception from the WordPress community and that reception has become increasingly negative since a hard deadline was set for the [5.0 release](https://make.wordpress.org/core/5-0/), even though many considered it to be incomplete. A hard release deadline in software is usually fine, but there is a glaring issue with this particular one: what will be the main editor for a platform that [powers about 32% of the web](https://wordpress.org/about/features/) isn’t fully accessible. This issue has been raised many times by the community, and it’s been effectively brushed under the carpet by Automattic’s leadership &mdash; at least it comes across that way.

Sounds like a messy situation, right? I’m going to dive into what’s happened and how this sort of situation might be avoided by others in the future.

## Further Context

For those amongst us who haven’t been following along or don’t know much about WordPress, I’ll give you a bit of context. For those that know what’s gone on, you can skip straight to the main part of the article.

WordPress powers around 32% of the web with both the open-source, self-hosted CMS and the [wordpress.com](https://wordpress.com) hosted blogs. Although WordPress, the CMS software is open-source, it is heavily contributed to by [Automattic](https://automattic.com/), who run wordpress.com, amongst other products. Automattic’s CEO, [Matt Mullenweg](https://ma.tt/) is also the co-founder of the WordPress open source project. 

It’s important to understand that WordPress, the CMS is not a commercial Automattic project &mdash; it is open source. Automattic do however make lots of decisions about the future of WordPress, including the brand new editor, [Gutenberg](https://wordpress.org/gutenberg/). The editor has been available as a plugin while it’s been in development, so WordPress users can use it as their main editor and provide feedback &mdash; a lot of which has been negative. Gutenberg is shipping as the default editor in the 5.0 major release of WordPress, and it will be the *forced* default editor, with only the download of the Classic Editor preventing it. This forced change has had a *mixed* response from the community, to say the least. 

I’ve personally been very positive about Gutenberg with my [writing](https://medium.com/@hankchizljaw/gutenberg-a-javascript-developers-perspective-601786ab8be4), [teaching](https://css-tricks.com/guides/learning-gutenberg/) and [speaking](https://gutentalk.hankchizljaw.io), as I genuinely think it’ll be a positive step for WordPress in the long run. As the launch of WordPress 5.0 has come ever closer, though, my concerns about accessibility have been growing. The accessibility issues are being “fixed” as I write this, but the handling of the situation has been incredibly *poor,* from Automattic. 

I invite you to read this [excellent, ever-updating Twitter thread](https://twitter.com/aardrian/status/1049655699956015105) by [Adrian Roselli](https://adrianroselli.com). He’s done a very good job of collecting information and providing expert commentary. He’s covered all of the events in a very straightforward manner.

Right, you’re up to speed, so let’s crack on.

{{% feature-panel %}}

## What Happened?

For as long as the [Gutenberg plugin](https://en-gb.wordpress.org/plugins/gutenberg/) has been available to install, there have been accessibility issues. Even when I very excitedly installed it and started hacking away at custom blocks back in March, I could see there was a *tonne* of issues with the basics, such as focus management. I kept telling myself, “This editor is very early doors, so it’ll all get fixed before WordPress 5.” The problem is: it didn’t. (Well, mostly, anyway.)

This situation was bad as it is, but two key things happened that made it worse. The accessibility lead, [Rian Rietveld](https://rianrietveld.com/), [resigned](https://rianrietveld.com/2018/10/09/i-have-resigned-the-wordpress-accessibility-team/) in October, citing political and codebase issues. The second thing is that Automattic set a hard deadline for WordPress 5’s release, regardless of whether accessibility issues were fixed or not.

Let me just illustrate how bad this is. As cited in [Rian’s article](https://rianrietveld.com/2018/10/09/i-have-resigned-the-wordpress-accessibility-team/): after an accessibility test round in March, the results indicated so many accessibility issues, **most testers refused to look at Gutenberg again***.* We know that the situation has gotten a lot better since then, but there are [still a tonne of open issues](https://github.com/WordPress/gutenberg/issues?q=is%3Aopen+is%3Aissue+label%3AAccessibility), even now.

I’ve got to say it how I see it, too. There’s clearly a cultural issue at Automattic in terms of their attitude towards accessibility and how they apparently compensate people who are willing to fix them, with a strange culture of free work, even from “outsiders”. Frankly, the company’s CEO, Matt Mullenweg’s attitude absolutely stinks &mdash; especially when he appears to be [holding a potential professional engagement hostage](https://twitter.com/photomatt/status/1062475366462308355) over someone’s personal blog decision: 

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">That&#39;s too bad was about to reach out to work with Deque on the audits.</p>&mdash; Matt Mullenweg (@photomatt) <a href="https://twitter.com/photomatt/status/1062475366462308355?ref_src=twsrc%5Etfw">November 13, 2018</a></blockquote>
<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Allow me to double-down on the attitude towards accessibility for a moment. When a big company like Automattic decides to prioritize a deadline they pluck out of thin air over enabling people with impairments to use the editor that they will be *forced* to use it is absolutely shocking. Even more shocking is the message that it sends out that accessibility compliance is not as important as flashy new features. Ironically, there’s clearly commercial undertones to this decision for a hard deadline, but as always, free work is expected to sort it out. You’d expect a company like Automattic to fix the situation that they created with their own resource, right? 

You’ll probably find it shocking that a [crowd funding campaign](https://wpcampus.org/2018/11/fundraising-for-wpcampus-gutenberg-accessibility-audit/) has been put together to get an accessibility audit done on Gutenberg. I know [I certainly do](https://twitter.com/hankchizljaw/status/1067537359523250176). You heard me correctly, too. The Gutenberg editor, which is a product of Automattic’s influence on WordPress who (as a company) were [valued at over](https://www.recode.net/2014/5/5/11626458/wordpress-parent-automattic-has-raised-160-million-now-valued-at-1-16) [**$1 Billion**](https://www.recode.net/2014/5/5/11626458/wordpress-parent-automattic-has-raised-160-million-now-valued-at-1-16) [in 2014](https://www.recode.net/2014/5/5/11626458/wordpress-parent-automattic-has-raised-160-million-now-valued-at-1-16) are not paying for a much-needed accessibility audit. They are instead sitting back and waiting for everyone else to pay for it. Well, at least they were, until Matt Mullenweg [*finally*](https://ma.tt/2018/11/a-gutenberg-faq/) [committed to funding an audit on 29 November](https://ma.tt/2018/11/a-gutenberg-faq/).

{{% ad-panel-leaderboard %}}

## How Could This Mess Be Avoided? 

Enough dragging people over coals (for now) and let us instead think about how this could have been avoided. Apart from the cultural issues that seem to de-prioritize accessibility at Automattic, I think the design process is mostly at fault in the context of the Gutenberg editor. 

A lot of the issues are based around complexity and cognitive load. Creating blocks, editing the content, and maneuvering between blocks is a nightmare for visually impaired and/or keyboard users. Perhaps if accessibility was considered at the very start of the project, the process of creating, editing and moving blocks would be a lot simpler and thus, not a cognitive overload. The problem now is that accessibility is a fix rather than a *core feature.* The cognitive issues will continue to exist, albeit improved. 

Another very obvious thing that could have been done differently would be to provide help and training on the JS-heavy codebase that was introduced. A lot of the accessibility fixing work seems to have been very difficult because the accessibility team had no React developers within it. There was clearly a big decision to utilize modern JavaScript because Mullenweg told everyone to [“Learn JavaScript Deeply”](https://www.youtube.com/watch?v=KrZx4IY1IgU). At that point, it would have made a lot of sense to help people who contribute a lot to WordPress *for free* to also learn JavaScript deeply so that they could have been involved way earlier in the process. I even saw this as an issue and made learning modern JavaScript and React a core focus in a [tutorial series](https://css-tricks.com/guides/learning-gutenberg/) I co-authored with [Lara Schenck](https://notlaura.com/).

I’m convinced that some foresight and investment in processes, planning, and people would have prevented a *tonne* of the accessibility issues from existing at all. Again, this points at issues with attitude from Automattic’s leader, in my opinion. He’s had the attitude that ignoring accessibility is *fine* because Gutenberg is a fantastic, empowering new editor. While this is true, it can’t be labeled as truly empowering if it prevents a huge number of users from managing content &mdash; in some cases, [even doing their jobs](https://twitter.com/jensimmons/status/1052582742452568065). A responsible CEO in this position would probably write an incredibly apologetic statement that addressed the massive oversights. They would probably also postpone the hard deadline set until **every** accessibility issue was fixed. At the very least, they wouldn’t force the new editor on every single WordPress user.

{{% ad-panel-leaderboard %}}

## Wrapping Up

I’ve got to add to this article that I am a *massive* WordPress fan and can see some unbelievably good opportunities for managing content that Gutenberg provides. It’s not just a new editor &mdash; it is a movement. It’s going to shape WordPress for years to come, and it should allow more designers and front-end developers into the ecosystem. This should be welcomed with open arms. Well, if and when it is fully accessible, anyway.

There are also a lot of *incredible* people working at Automattic and on the WordPress core team, who I have heaps of respect and love for. I know these people will help this situation come good in the end and will and do welcome this sort of critique. I also know that lessons will be learned and I have faith that a mess like this won’t happen again.

Use this situation as a warning, though. You simply can’t ignore accessibility, and you should study up and integrate it into the entire process of your projects as a priority. 

{{< signature "dm, ra, il" >}}