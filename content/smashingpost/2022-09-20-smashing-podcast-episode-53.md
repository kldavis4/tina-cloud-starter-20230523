---
title: 'Smashing Podcast Episode 53 With Rémi Parmentier: Can HTML Email Use Modern CSS?'
slug: smashing-podcast-episode-53
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eaf789d-a932-4d1f-a811-3406e0c63644/smashing-podcast-episode-53.png
date: 2022-09-20T13:00:00.000Z
summary: >-
  In this episode of the Smashing Podcast, we’re talking about HTML email. Do we still have to design like we would for IE5? Vitaly talks to expert Rémi Parmentier to find out.
description: >-
  In this episode of the Smashing Podcast, we’re talking about HTML email. Do we still have to design like we would for IE5? Vitaly talks to expert Rémi Parmentier to find out.
categories:
  - Smashing Podcast
---

In this episode of The Smashing Podcast, we’re talking about HTML email. Do we still have to design like we would for IE5? Vitaly talks to expert Rémi Parmentier to find out.

<iframe src="https://share.transistor.fm/e/7db059e9/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

### Show Notes

- Rémi Parmentier [on Twitter](https://twitter.com/HTeuMeuLeu)
- [Can I Email?](https://www.caniemail.com)

#### Weekly Update

- [Meet “Smart Interface Design Patterns Checklists”](https://www.smashingmagazine.com/2022/09/smart-interface-design-checklist-cards-release/) *written by* Vitaly Friedman
- [Making Sense Of WAI-ARIA: A Comprehensive Guide](https://www.smashingmagazine.com/2022/09/wai-aria-guide/) *written by* Kate Kalcevich
- [JavaScript APIs You Don’t Know About](https://www.smashingmagazine.com/2022/09/javascript-api-guide/) *written by* Juan Diego Rodríguez 
- [Accessibility In Times Of Headless](https://www.smashingmagazine.com/2022/09/accessibility-times-headless/) *written by* Josefine Schaefer
- [Rethinking Star Ratings For Readers](https://www.smashingmagazine.com/2022/09/rethinking-star-ratings-readers/) *written by* Matt Athanasiou

### Transcript

<p><a href="https://twitter.com/HTeuMeuLeu"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a9109d9-00d0-4aba-a8b1-b7a704ad0119/remi-parmentier-profile-200x200-opt.jpg" width="200" height="200" alt="Photo of Rémi Parmentier" /></a> <span class="smashing-tv-host">Vitaly Friedman:</span> He’s an email and web developer based in the north of France, near Lille and goes by HTeuMeuLeu on the internet. He works in his own small web development agency, Tilt Studio, since 2008. And he also runs workshops, gives talks, and writes articles on his blog all around HTML emails. Now Rémi also likes collecting Game Boy consoles and listening to, Sufjan Stevens. My Smashing friends, please welcome Rémi Parmentier. Hello, Rémi. How are you doing today?

<span class="smashing-tv-speaker">Rémi Parmentier:</span> I’m smashing.

<span class="smashing-tv-host">Vitaly:</span> Oh, that’s so wonderful to hear, Rémi. I don’t know when we know we saw each other maybe, I don’t know, 27 years ago now?

<span class="smashing-tv-speaker">Rémi:</span> Ah, yeah, that feels like it. Yeah, I think we met in person for the first and last time in Smashing conference in Freiberg in 2019, I think.

<span class="smashing-tv-host">Vitaly:</span> I think so. This seems like it was a very, very long time ago.

<span class="smashing-tv-speaker">Rémi:</span> Yeah, it’s not even this decade, so.

<span class="smashing-tv-host">Vitaly:</span> Yeah, no. So Rémi, this is coming here maybe the questions from the audience, coming already. So if it was 27 years ago, was it the same back then, writing TL emails, like it is today? Or have things changed since then?

<span class="smashing-tv-speaker">Rémi:</span> You are already teasing me. No, I would say things have changed somehow. There are differences like mobile emails, we do responsive emails nowadays, that wasn’t the case 27 years ago. So, yeah, there are lots of differences like this.

<span class="smashing-tv-host">Vitaly:</span> Yeah. So it’s always interesting for me because there is an ongoing joke about HTML emails and people who have to do HTML emails and people who are forced to do emails. And you love to do HTML emails.

<span class="smashing-tv-speaker">Rémi:</span> Yeah.

<span class="smashing-tv-host">Vitaly:</span> You have to explain yourself, Rémi.

<span class="smashing-tv-speaker">Rémi:</span> Yeah, I don’t know how it came to be exactly, but I wouldn’t have had the repulsion that most web developers have these days when they get asked to code an HTML email.

<span class="smashing-tv-speaker">Rémi:</span> And I think one of the reason might be that I’m old and so when I started at my very first gig in a web agency, it was around 2006. And back then emails were coded pretty much the same way that webpages were coded. So we use tables for layouts for webpages and so did we for HTML email. So it wasn’t so different back then. And so it’s just that with time, we saw that web evolved to something different. To as a semantic web first with a growing introduction of CSS and growing use of CSS for layouts. And then we got responsive web. And nowadays we’ve got all sorts of web applications and stuff like this. And yeah, it’s true that emails didn’t catch on to all of these steps, at least not at the same ease, at the same timeframe than the web did.

<span class="smashing-tv-speaker">Rémi:</span> But I feel like somehow it’s catching up every now and then. And we do get to use nice and modern stuff, as well, in HTML emails. So yeah, I really like HTML emails. And I think one part of it is that’s whenever I stumble upon a really weird the bug or behavior or something that’s really maddening for the normal person, I like to just dig in and try to figure things out, try to understand why this happens this way, why things are this way? And so I think that’s really an interesting niche of HTML development nowadays.

<span class="smashing-tv-host">Vitaly:</span> But it’s probably keeps you... I don’t know, it keeps you on your toes and keeps you awake at night, thinking about all this incredible, wonderful bugs happening in, I don’t know, in Microsoft Outlook and, God for a forbid, Lotus Notes. Are you still testing Lotus Notes?

<span class="smashing-tv-speaker">Rémi:</span> No, no, no. I haven’t tested that for years now, so.

<span class="smashing-tv-host">Vitaly:</span> Okay. That makes me a bit happier at this point. But every time I think about HTML emails, I do remember your wonderful talk where you say that, well, we actually have to think about email development as being a slightly different way, a slightly different mindset that is required to actually get it right. And I remember you speaking about thinking in the Email Geek, which really takes a slightly different turn, I guess, or perspective on what it even means to be designing and developing emails. So if somebody’s very, let’s say unfamiliar, with this territory, if you had to explain how building, designing HTML emails is different from a regular website... I mean, it’s hard to say regular... From websites and applications. Regular always has a little of undertone in it. How are they actually different? And what are some of the important skills that are absolutely required to even make sense of building and designing for HTML email?

<span class="smashing-tv-speaker">Rémi:</span> Yeah, so I think the differences can fall down to two things. The first may be the email client’s landscape. So we’ve got tons of email clients existing and used by people all around the world, while in the browsers nowadays we pretty much sadly have only one browser, which is Chrome and Chromium used by Edge and WebKit used by Safari, which is very similar, as well. And unfortunately, there’s not much diversity in the browser world right now. And so that’s actually a good thing that I enjoy about the email space is that we have got a lot of diversity, tons of email clients. And of course, the bad part of this is that each client comes with its own bugs and quirks and weird behaviors and features that you might not expect and that can be surprising. But I think it’s really the same thing to have such an environment with so many difference email clients.

<span class="smashing-tv-speaker">Rémi:</span> And the second thing that’s really pretty different, I think, is people, it’s users. And on the web, even if you don’t really know beforehand who will visit your websites, you can know it afterwards. If you use any sorts of analytics or if you just look at your server statistics, you will know how many pages, were viewed, how many people came to your website and such. On the email world, it’s really hard to have such statistics because we cannot use JavaScript for this and we cannot use server stats because emails are never on our own server. They’re on the email service server, so we need to rely on invisible tracking pixels. But these are not really reliable because not everyone display images in emails and sometimes you have got image proxying like in Gmail or Apple Mail and so you end up with statistics that are very biased and I think kind of wrong because you miss a lot of the population.

<span class="smashing-tv-speaker">Rémi:</span> So you don’t really know who is opening your emails and how and when. And so you can’t really design and code an email with the expectations that, "Oh, okay. I know that my user base is 90% Apple Mail so I don’t need to care about Outlook." You can’t really do this. So you need to have a more extended view and be really humble and realize that you won’t be able to code for everyone, but you need to do it as good as you can, get close to this. Because you really don’t know who’s going to open your emails.

<span class="smashing-tv-host">Vitaly:</span> But despite all of that, despite all this unpredictability, and I remember you mentioning in your session at... Also, one thing that actually quite happens quite a bit, and that’s something that we just don’t have on regular web pages or applications is that email clients also change the way HTML email works. They add links, they change links, they obfuscate things, they change markup for security and privacy reasons. And all those things are very often out of control. And not to mention all the different quirks that go in all the different email clients, as well.

<span class="smashing-tv-host">Vitaly:</span> But despite all of that, I’m very surprised, every now and again, to see an enormous, I would even say extraordinary level of creativity when it comes to what people turn HTML emails into. I don’t know, from shopping cart experiences within an email, to games and everything else.

<span class="smashing-tv-host">Vitaly:</span> What are some of the most impressive things that you saw built within HTML email?

<span class="smashing-tv-speaker">Rémi:</span> I think it has to be an email made quite a few years ago now. That was an email called Superman Request and it’s actually a mini game. I think it calls this a Night Beat adventure and it’s a choose-your-own-path game where you’re a small character that adventures in the land of tables and TDs and you need to find your path to the best emails. And it’s really such a clever use of all the CSS possibilities with checked input and radio buttons and things like this. That one really blew my mind at the time and it’s still stuck in my mind. Because not only is this really clever in the first place, but it also, I guess, took a huge amount of time and patience to do something like this. Yeah, that was really impressing.

<span class="smashing-tv-host">Vitaly:</span> Yeah, I think you mentioned this at some point as well. It looked absolutely incredible just to be able to do that in an email. It’s just something out of control. For me personally, it was, I think when Mark Robbins, I think, he was giving a presentation once. He’s working in one of the email companies.

<span class="smashing-tv-speaker">Rémi:</span> Yes, he’s working in Salesforce now.

<span class="smashing-tv-host">Vitaly:</span> Salesforce now. All right. And I remember him giving a talk about the HTML email and it all felt very natural. And then in the end of the session he showed that this was actually within HTML email where the entire presentation and slides and highlighting and everything. That was very, very impressive.

<span class="smashing-tv-host">Vitaly:</span> One thing though that really keeps impressing me, I guess, about these things is that there seem to be differences even within the same platform. So if I look at Outlook and outlook.com, if I look at Gmails across different devices and gmail.com, if look, I look at Yahoo web mail and Yahoo applications, it seems like even although they have the same vendor, basically, they operate differently.

<span class="smashing-tv-host">Vitaly:</span> So could you maybe shed a bit of light? Are they often very different or what should we as developers and keep in mind when we are, let’s say, dealing with Gmail? Because are there 50,000 versions of Gmail or is it just a few?

<span class="smashing-tv-speaker">Rémi:</span> So maybe they’re not that much. But yeah, there are a few differences and valuations across what we can call a family of email clients, so as you said, like Gmail or Outlook. And it’s not always clear why this is, but perhaps one of the most annoying at the moment is in Gmail. For example, you will get a different level of CSS support whether you are using the desktop web mail, which usually has the best CSS support across Gmail clients, versus if you’re using the mobile apps. And even if you’re using the mobile apps, you would get a different level of CSS supports, whether you are using Gmail address or whether you’re using third-party email address, like if you’re using your outlook.com email address inside the Gmail app on Android or iOS.

<span class="smashing-tv-speaker">Rémi:</span> In that case, you will get what is perhaps the worst CSS support possible. Because Gmail, I think for security purposes, strips a lot of styles and a lot of things. It doesn’t support style tags, it doesn’t support media queries. So you end up with a really bare and really raw HTML with just a few styles, just what you need to get your colors and a few things like this in there. But it’s a really minimalistic approach that you need to get your email to look good in that kind of circumstances. Yeah.

<span class="smashing-tv-host">Vitaly:</span> Yeah. So it’s always such a story and you probably can hear the very disappointed voices from the dark corners of the internet talking about, "What’s the deal with Outlook?"

<span class="smashing-tv-host">Vitaly:</span> We’ve been making fun of Outlook for, I don’t know how many years now, and I don’t know when it was a 2012 or '11 or maybe even earlier than that where there was a big switch to use the Microsoft Word rendering engine, I heard. And it stayed like this, well, since then, if I’m not mistaken.

<span class="smashing-tv-speaker">Rémi:</span> Yeah, exactly.

<span class="smashing-tv-host">Vitaly:</span> So, Rémi, what are we going to do about this? Is there any, I don’t know, any help in sight, Are we just going to have to deal with Word rendering engine forever?

<span class="smashing-tv-speaker">Rémi:</span> So this is actually a very hot topic at the moment because something is happening at Microsoft. They might have heard all the complaints for the years and it looks like they are doing something. So as you mentioned in 2007, Microsoft decided to move Outlook on Windows from Internet Explorer rendering engine to Word rendering engine.

<span class="smashing-tv-speaker">Rémi:</span> And this has been really the bane of all email developers because Word is really terrible at rendering HTML and CSS. Not only does it just support very limited CSS features and HTML, but oftentimes it does it really wrong. So it doesn’t calculate weight from images correctly in CSS or it doesn’t... A lot of stuff happening that’s really intimidating for a web developer. So what’s changing at the moment is that just a few months ago, I think it was last month or just month before, Microsoft released is the first public beta version of Outlook on Windows, using Edge rendering engine.

<span class="smashing-tv-speaker">Rémi:</span> So they’re making a brand new Outlook on Windows and it’s basically just a web app, embedded as a desktop application. So now it’s going to mean to fix almost all the problems that Outlook had created in the first place. So it’s staying better for now, but I’m in good faith that Microsoft is really committed to push this to their end users and see how things go from there. And if they deploy this as the real update and replacement of the actual Outlook versions running on Word, it’s going to be a really big change because this means that we may no longer need to use tables for layouts. Because the only reason we use tables in HTML emails is because of the Outlook on Windows, because Word doesn’t really understand anything else than tables for layouts. So that’s really what we can out now is that Microsoft is going to push all this update and that all of the users are going to move to it. And yeah, that’s really what we need to do.

<span class="smashing-tv-host">Vitaly:</span> Well, I can hear a lot of enthusiasm and hope and I don’t know, I would say excitement about this. This seems like a very interesting move that we should probably be really watching out for, so that’s neat.

<span class="smashing-tv-host">Vitaly:</span> But given the scenario then, so with tables or without, what do you think then would be... Maybe actually looking back, look at your work specifically, how would you go around building HTML emails? So there are many solutions out there, obviously there are plenty of templates, very different kinds of templates, there’s also MGML and so on and so forth.

<span class="smashing-tv-host">Vitaly:</span> I’m wondering where do you stand in terms of what it takes, so what does it mean to be building HTML emails today? Is it still cool to be, I don’t know, coding HTML emails from scratch or do other particular templates that are normalizing things across email clients? What’s your take on this?

<span class="smashing-tv-speaker">Rémi:</span> So I’m definitely in from scratch camp right here. But I’m also there in for the web, as well. I like to do things from scratch.

<span class="smashing-tv-speaker">Rémi:</span> I think that a way to see this is that it’s not so different from the web. If you were to code a website, would you use something like Bootstrap or maybe start with a WordPress default theme and build your website from there on? Or would you rather build something from scratch? And so yeah, that’s really a way to see things. And both approaches can be good. It really depends on the time that you have, the knowledge that you have, and the will and patience that you have, as well.

<span class="smashing-tv-speaker">Rémi:</span> So yeah, I really, usually myself, I prefer to cut everything from scratch. But for any newcomers then if it’s good for them to start from an already made template that they found from their ESP, then go for it and maybe start learning from there and see how you can improve things from there and see what problems you encounter with the default templates and see how you can improve things and build something better from there. That’s a good approach as well.

<span class="smashing-tv-host">Vitaly:</span> Right. And in your case, where would you start? Are starting with... I mean obviously, I guess, I assume. I don’t know if I should be assuming that or not.

<span class="smashing-tv-host">Vitaly:</span> Will you be starting with HTML tables, or what is your take? Do you then build mobile first, desktop first, or how does it work for you?

<span class="smashing-tv-speaker">Rémi:</span> Yeah, so for a few in the years now, I think the start I approach in the email development industry and community has been more about doing things fluid, or hybrid, as we go them. So this means that we’re going to build the layouts that can adjust to any screen sizes with our media queries first. So by just using divs for example, a div is responsive by default. If you don’t set any fixed weight from it’ll adjust to your window’s size. And then from there, you can use media queries, whether targeting mobile or targeting desktop to improve things. So that’s really what we call progressive enhancements and graceful degradation. So that’s the whole mindset here, I think, is really important in the email world.

<span class="smashing-tv-speaker">Rémi:</span> So yeah, the approach regarding table and my approach at least, has been more to put the tables in conditional comments for Outlook because that’s really only Outlook that needs them. And then for other clients, use divs and use regular HTML semantics like H1, H2 tags, paragraphs, and such to create your elements and lay them out. And but I’ve been coding like this for, I don’t know, for how long, but for quite long now, and it’s still working well. So I think that’s a really valued approach, as well.

<span class="smashing-tv-host">Vitaly:</span> Oh, interesting. So that means that basically... Am correct to assume that you then would be having one markup specifically for Outlook, and then the rest will be getting the good old div or even potential section article. Is it even viable as well there?

<span class="smashing-tv-speaker">Rémi:</span> So regarding some of the semantics like article or editor and photo tags, it’s usually not appropriate because your email might get included in a more complex application like Gmail. And Gmail is web mail and its HTML itself. So when Gmail inserts your HTML newsletter in its interface, you end up with Gmail’s HTML code all around your own HTML code. So then the semantic might not make sense there. And on top of that, Gmail specifically doesn’t support these tags, so you need to find a proper fallback for years.

<span class="smashing-tv-speaker">Rémi:</span> But as far as Outlook is concerned, as the idea is not that much to create a separate, isolated code for the whole email, but more to add small chunks of code just for Outlook, that will say, "Okay, I’m going to open a table for Outlook right now." And then I will have the rest of my concerns come on for both Outlook and other email clients. And then at the end of my email or of my blog, I will just add another block I’ve got just for Outlook that will say, "Okay, I’m closing the table that I opened." And that’s it for tables and just for Outlook.

<span class="smashing-tv-host">Vitaly:</span> Okay. Is it actually still a good idea to inline styles in email?

<span class="smashing-tv-speaker">Rémi:</span> Yes. Yeah, it is because even though lot of clients do support style tags and even Outlook on Windows, actually, that’s something often surprising to people. It’s usually a good idea because some clients don’t support style tag. So earlier, I mentioned the Gmail apps on mobile when you don’t use the Gmail accounts. So this is what we Email Geeks often call GANGA, for Gmail apps with non-Gmail accounts.

<span class="smashing-tv-host">Vitaly:</span> This is quite an acronym word right there.

<span class="smashing-tv-speaker">Rémi:</span> Yeah, I love this acronym. And so in GANGA, you don’t get style tag support, so you need to inline your style there. So it’s really a good way to make sure that in these very restrictive conditions, at least your email looks properly styled for text and for font sizes and such and such things.

<span class="smashing-tv-speaker">Rémi:</span> But you can have some of your styles in separate style texts. And, in fact, that’s what we can do for responsive emails. When we use media queries, we cannot inline media queries, so we do have to use style tags. So we do a bit of both.

<span class="smashing-tv-speaker">Rémi:</span> And regarding inline styles, it’s also important because whenever you’re going to reply to an email or forward an email, which is something very unique to emails, some of this is really not something that happens on websites... Email clients, and that’s pretty much the case for all email clients, will really remove all the style tags of your code when you do this. And so if you don’t have in an inline style, suddenly your emails will look like something completely broken. So it’s always safer to have at least a bare minimum of times inline so that your emails looks good in this, when it happens.

<span class="smashing-tv-host">Vitaly:</span> Right. What about the font phase, by the way? So when we’re talking about embedding fonts, obviously, these font need to live somewhere. You’re not going to attach them to the email. And then sometimes I see that there are code errors appearing where you’re trying to fetch fonts from one place and then it doesn’t know where it’s going to be loaded from. So you cannot just, let’s say, whitelist a couple of domains and call it a day. So it needs to be just public to everyone.

<span class="smashing-tv-speaker">Rémi:</span> Yeah.

<span class="smashing-tv-host">Vitaly:</span> Right. What is a common way to deal with this?

<span class="smashing-tv-speaker">Rémi:</span> So, yeah. But that’s a very specific problem. And this happened to me a few times, especially when working with clients who have their own phones hosted on their own server, but they’re using CORS rules for security, so the font cannot be called from a specific web mail. I think in the end, it kind of falls apart because it then is working okay, because CORS restrictions like this do not apply to email applications.

<span class="smashing-tv-speaker">Rémi:</span> So for example, Apple Mail does support font face, and it doesn’t behave to CORS rules. So even if you have CORS restrictions, your fonts will still be available in Apple Mail. And for font face, Apple Mail is really just one of the few that supports it because there’s almost no web mail, so no Gmail, no outlook.com that supports font face like this no Yahoo, either. And there’s just I think a few international or local email clients that do support font face in that case.

<span class="smashing-tv-speaker">Rémi:</span> So yeah, whenever you are using font face, you need to realize that not a lot of people might see your fonts and because it might be stripped from the email clients, like Gmail or outlook.com. And you might have CORS errors like this. So it’s always a question of progressive enhancement and graceful degradation just... I like to use font face in emails when it’s part of the design and it’s a great enhancement, but you always need to realize that that’s not going work for 100% of your subscribers. So just you always have to think about what happens if it doesn’t work.

<span class="smashing-tv-host">Vitaly:</span> Right. What do you think in general about things like MGML. Do you use anything like that, sort of a templating language for writing coding, I would say, faster and still distant HTML emails? Or maybe using something else? What’s your take on it?

<span class="smashing-tv-speaker">Rémi:</span> So yeah, MGML is very popular and it’s always interesting to see. And the fun fact, I was actually hired as a consultant by Mailjet when we launched MGML in 2015 or '16, I think. And so I worked with them to make sure that the HTML output by MDML is on par with our industry standards and just works well in all environments, including Outlook. And so it’s really fun to see that still up to this day it holds up pretty well, and even though I know there has been updates to MGML and such. But the basic way of doing things, which is mobile first, has been holding well across all these years.

<span class="smashing-tv-speaker">Rémi:</span> And so I don’t use MGML myself, but I do use a few of our tools. And this year, in particular, I’ve been really digging into Parcel, which is an online code editor dedicated to HTML emails. And so there are a lot of fun stuff in it, to really help you code emails maybe faster. There’s components, there are styles inlining, and you can send tests to your inbox from the editor. So that’s really great.

<span class="smashing-tv-speaker">Rémi:</span> And I’ve also been walking with Mazo, which is a node framework to build HMTL emails, as well. I kind see it like JQL or Ivanti, which is not so much that it impose a way to code to you, but you can bring your own code and it just helps you output things easier and faster and do all sorts of small routines that like styles inlining or things like this.

<span class="smashing-tv-speaker">Rémi:</span> So yeah, I think over the past few years, we are really starting to see tools appearing like this and really catching on across email developers. So you can... Yeah. Yeah, I think that’s a good sign of maturity among the-

<span class="smashing-tv-host">Vitaly:</span> Right, and while they’re talking about sending emails to yourself from Parcel, which I think is actually pretty cool, what would be then your strategy to test and debug emails? So do you literally send it to yourself via email and then you check on your phone, let’s say, if it looks okay, and then you go back to the editor, and then you fix, and then you resend it? Or is there any other way or approach to do that? What’s your take?

<span class="smashing-tv-speaker">Rémi:</span> Yeah, that’s usually my first approach, it’s just testing and sending to myself. And by sending to myself, I mean sending to the dozens and dozens of email addresses that I’ve created pretty much everywhere so that I can see how email code behaves in different email clients.

<span class="smashing-tv-host">Vitaly:</span> What a fun place it is for all those email addresses to be in. Probably tons of different tests and spam and everything else coming together in one, fun place.

<span class="smashing-tv-speaker">Rémi:</span> Yeah. That would be a weird thing if these email inboxes were ever to leak as part of, I don’t know, any data leak. People would be wondering, "What is this inbox doing exactly? There’s been 20 emails just this past hour about this thing. I’m not sure why."

<span class="smashing-tv-speaker">Rémi:</span> But on top of that, we’ve got the chance to have email screenshot tools. So that’s kind of like browser stack for email. So where you just copy your HTML email code, just send your HTML email to, and then you will get screenshots on many, many different email clients. So you will get a quick preview of what your email looks like on Apple Mail, on iOS, on Gmail, on Outlook, on Windows, and all of this in just a few clicks. And it’s really a good way to make sure, as well, that your code works well in all these different environments.

<span class="smashing-tv-host">Vitaly:</span> And of course there is, CanIEmail.com, but which you wonderfully announced during the SmashingConf Freiburg. What was it like two years ago?

<span class="smashing-tv-speaker">Rémi:</span> Yeah, that was in Freiburg in 2019. So that’s already almost three years now.

<span class="smashing-tv-host">Vitaly:</span> Yeah. I mean, maybe you can also talk a bit about this and maybe any new features that are coming up and what it is. But for me personally, this is just a really ultimate great resource to just find out how well particular feature is supported. Think about it CanIUse.com, just for email?.

<span class="smashing-tv-speaker">Rémi:</span> That really was the idea. And I think that’s part of this sentiment that the email community is maturing and growing, is that we’ve got places like this where not only can we learn more publicly about what email clients do, what do they support and such things, but we can also contribute to it. And that was really, I think, the missing part. Because before that, we had a few websites that gave you the state of support for a few CSS properties in a few email clients, but it was most of the time just part of blog articles that were really outdated or on website that you couldn’t really interact with.

<span class="smashing-tv-speaker">Rémi:</span> So the idea with CanIEmail was really to make this available and open source and so that anyone can contribute to it. And if you see that an email client doesn’t support something, then you can report it on website and so everyone benefits from it, from them. So it’s really a great knowledge base that everyone can benefit from.

<span class="smashing-tv-host">Vitaly:</span> Yeah. Yeah, sure. Well, I do have to ask a question. I ask it every single time and I know what your answer is going to be like, but I do want to be... Oh, well these things have changed and I want you just to explain to our wonderful listeners here why we are where we are.

<span class="smashing-tv-host">Vitaly:</span> Now, obviously again, there is this large conversation about HTML email being such an outdated thing and HTML tables and everything and all of that. But we have this incredible, growing bloom of CSS features, grid, container queries, cascade layers. CSS is blooming like never. But when we are looking at this HTML email, we should be probably a bit of skeptical, I guess, of when we even would be able to use those things and do so reliably, and if it’s even an option at all.

<span class="smashing-tv-host">Vitaly:</span> So I’m wondering, and I think that many people are, should we be expecting at some point now in the future, at any point, really some sort of inter... Oh, this is a very difficult word... Interoperability sanitization around HTML emails and the features that are supported across Yahoo and Outlook. And with Edge moving, oh, well, not moving... It’s Outlook moving to Edge, no Edge moving into Outlook, That’s probably the better way of putting this.

<span class="smashing-tv-host">Vitaly:</span> Is it happening? Are we getting there or-

<span class="smashing-tv-speaker">Rémi:</span> So that’s a very interesting question because this is also a hot topic in the email world. Because I think it was just last month, there’s a new group that was formed in the past year that was announced and that’s called the Email Markup Consortium, so EMC for short. And basically, it’s a bunch of email developers and marketers and designers like me, who decided to gather together and try to really get things down to make email betters for everyone. So that means better for developers, with more standardizations and more uniformity across email clients. And also better for users because if email clients get support for all your roles, for example, or all your properties, then we can make some parts of emails more accessible for people who need it. And same thing goes for some things related to performance. If we get support to picture tags and responsive images, we could deliver more efficient and more performance email because we can have smaller image sizes and things like this.

<span class="smashing-tv-speaker">Rémi:</span> So this is really a work in progress. And I haven’t done much of it. So I think it’s mostly Marc Robbins and Alice Li, and I’m sorry I forgot his name, but a few people who are really active in the Email Geeks community. I think they are the main core members, but there are also a lot of members around who will contribute to the launch of this. And so now, it’s really about trying to catch the email clients’ developers attention and get them to improve things. And the good news is that there’s already been a few email clients that said they were interested in doing things better. So I know that there’s been a German email clients like this.

<span class="smashing-tv-speaker">Rémi:</span> So yeah, it’s really something new. So I’m really eager to see where this can go because there’s been attempts to improve things in the past, but that have never really caught on or that fell flat after a few months. So I know that this group has been around for a year secretly and trying to get things done, so it’s really great to see that now this is public and I’m really eager to see where this will lead. And hopefully it will lead to better standards and uniformity across email clients.

<span class="smashing-tv-host">Vitaly:</span> Oh, this does sound very exciting and it almost makes me feel like the future of HTML email is bright. However, I should probably curb my enthusiasm a little bit just because I don’t think we should be expecting, I don’t know, CSS sub grid and React or JavaScript getting into the world of HTML email anytime soon. Or am I wrong there?

<span class="smashing-tv-speaker">Rémi:</span> As for JavaScript, I think it’s nothing something you should expect and it’s really not something you should want because first, do you really want your emails to have flashy carousel and things like this? I’m not sure about that.

<span class="smashing-tv-host">Vitaly:</span> I mean, you can also do this with CSS and interactive, I don’t know.

<span class="smashing-tv-speaker">Rémi:</span> Yeah, yeah. But I’m not fully sure about this. But the main problem with JavaScript is really security because if you let any single line of JavaScript inside an email client, then some actors could really get your whole inbox and just download all your data and things like this with what you even knowing it. So there’s really a great danger with JavaScript. And so you should never expect full JavaScript support in email clients. But as for you mentioned a sub grid, and I think this is something that I haven’t heard of it exactly, but I think this is something we should expect in the next release of Apple Mail because if I’m not wrong, it’s coming in the next Safari.

<span class="smashing-tv-host">Vitaly:</span> Safari 16, yes.

<span class="smashing-tv-speaker">Rémi:</span> Yeah, iOS 16. And usually every time Apple adds some new features in WebKits and Safari, Apple Mail also benefits from it. So this is something that should come in Apple Mail this fall. So in some way if you really need to use CSS sub grids, you should be able to do it by the end of the year. But you just need to remind yourself that it will only work in Apple Mail from now. So, yeah.

<span class="smashing-tv-host">Vitaly:</span> But at the same time, I mean, you dismiss a wonderful, beautiful carousel just like that. However, I do remember vividly this time, maybe for a very brief period of time, while there was a huge excitement about this notion of interactive emails. And I think that still is, where you had AMP for Email?

<span class="smashing-tv-speaker">Rémi:</span> Yeah, AMP for email.

<span class="smashing-tv-host">Vitaly:</span> And you have all the beautiful carousels and everything else that you ever wanted, without having to write a single line of JavaScript because it would be just embedded into the platform and then you could reuse one of those components. Do you think that this is still a thing or where are we going with this?

<span class="smashing-tv-speaker">Rémi:</span> So yeah, interactive emails is still a thing and everyone talks about it every now and then. But there’s really two approaches to it. So the most traditional one is to use CSS and to ask CSS to use small interactions possible in CSS, like with the checked pseudo selector or hover pseudo selector. And from there you can do things where if you hover specific zone and some other content will appear, so you can do some image swap on hover or stuff like this. And we’ve checked, you can do much more detailed interactions where if you click on something, something else will appear on your email and you can do these sorts of things. So this is quite limitating because you are just limitating with these two sorts of interactions. But it does some decent support, like in Outlook.com, you can do things like this in Yahoo desktop one mail, as well. And Gmail does support hover interactions, as well. So that’s always interesting to do this for Gmail.

<span class="smashing-tv-speaker">Rémi:</span> But the hover approach, as you mentioned, was that Google announced a few years ago now AMP for email, and the idea was to bring the AMP JavaScript framework into the world of HTML emails, which is an interesting thought in the first place. But I think now it’s been quite a few years now that they did this, and I think now looking back that it was probably not the best approach to have because the way they did this is that they added a new mine type inside your email. So when you send an HTML email, you are not just really sending an HTML file to people, you’re sending an email code that’s actually a multi part code where there is a plain text version of the email, the HTML part, and all sorts of editor saying who you are sending your email to and things like this.

<span class="smashing-tv-speaker">Rémi:</span> And what Google did with AMP for email is that they brought a whole new AMP for email section in the email code like this. But this meant that if you wanted to send an AMP for email, then still if you want to send now an AMP for email email, for your ESP, or your email sending service, to support this specific mine types or else you cannot go code this and send it. So this was the whole email industry was really, really eager to look at who is going to support this and who will not. And a few years after, right now, it looks like most email providers and services didn’t really support this. So, for example, MailChimp doesn’t support this, so a lot of famous email services do not support AMP for email. So you cannot send for AMP for email easily.

<span class="smashing-tv-speaker">Rémi:</span> And I think another respect that makes AMP for email quite difficult is that even if you manage to send an AMP for email email, you need to get whitelisted from each clients that supports AMP for email. So if you want to send an AMP for email, you need to get whitelisted from Google so that people using Google desktop one mail will see it, and you need to get whitelisted from mail dot ?? that also supports it. And so it’s quite a difficult process, in my opinion. And it’s also quite opposite to the basic nature of email, which is a very open standard. Anyone can send email, any email clients can read email. So they try to act around the email format to get interactivity inside it, but I think that made things more difficult.

<span class="smashing-tv-speaker">Rémi:</span> So yeah, I still think that that can be exciting uses. I don’t know if you’ve ever used Google Docs and received an email where someone commented on your Google Docs and you can, inside Gmail, answer in the email, it’s an AMP for email email and you can answer right from your Gmail inbox to the comment that was left on your document. I think that’s an amazing use of AMP for email. But it’s hard to see how this could be made more popular. And, yeah, it’s hard to imagine this catching on and to find good uses like this for more traditional emails.

<span class="smashing-tv-host">Vitaly:</span> Well, maybe as we’re wrapping up here this point, I do have to ask one question that has been bothering me for a while. If there was a dream feature that you’d love HTML email to have, something that could be appearing in all the email clients everywhere tomorrow, if you just desired that to be in there, what would that feature be?

<span class="smashing-tv-speaker">Rémi:</span> So I think it wouldn’t necessarily be an HTML CSS feature, but I’d love to see something like reactions for emails, like you’ve got on Slack or on GitHub issues or just on messages on iOS and Android. And that would be a fun feature and I think that could spare a lot of emails because every time you need to just send an email to them saying "So, okay, I got this," you could just send a reaction and that would be way faster. But again, this would require a lot of standardization and implementation. So I think we are not really very hit at all.

<span class="smashing-tv-host">Vitaly:</span> If you, dear listener, would like to hear more from Rémi, you can find him on Twitter where he is HTeuMeuLeu, or we’ll have to put that link in the notes. And on his website at HTeuMeuLeu.com, as well. But also at SmashingConf, he often runs HTML email workshops. We will be discussing when the next one is coming up.

<span class="smashing-tv-host">Vitaly:</span> Do you have any parting words with our wonderful audience, Rémi, for today? We’ve been learning today all about HTML email, but what have you been learning from this session or in general? What are the parting words you’d like to hand over for people who might be excited to join this dark side of the world and design and build a HTML email together with you?

<span class="smashing-tv-speaker">Rémi:</span> Well, I hope that I convinced a few of you that yeah, email development is a thing and it can be. If you’re frustrated with how a website works nowadays, join us. It’s really fun in here. And yeah, there’s a whole community, as well. So yeah, feel free to reach me and just join us. There are dozens of us.

<span class="smashing-tv-host">Vitaly:</span> Of course. And if you are, dear friends, interested in the community of HTML Email Geeks, as far as I understood. Rémi, please correct me if I’m wrong. There are Email Geeks, there is a Slack channel. And you can also talk to Rémi and I’m sure that he’ll be very happy to point you to the group where all the cool kids talking about HTML emails hang out.

<span class="smashing-tv-speaker">Rémi:</span> Absolutely.

{{< signature "il" >}}
