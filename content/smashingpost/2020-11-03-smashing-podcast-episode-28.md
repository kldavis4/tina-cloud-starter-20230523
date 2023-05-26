---
title: 'Smashing Podcast Episode 28 With David Darnes: What Is Eleventy?'
slug: smashing-podcast-episode-28
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aecb98e2-49b3-44ef-b943-5427d5ee7b84/smashing-podcast-episode-28.png
date: 2020-11-03T05:00:00.000Z
summary: >-
  We’re talking about Eleventy. What is it and how does it fit into your Jamstack workflow? Drew McLellan talks to David Darnes to find out.
description: >-
  We’re talking about Eleventy. What is it and how does it fit into your Jamstack workflow? Drew McLellan talks to David Darnes to find out.
categories:
  - Smashing Podcast
  - Eleventy
  - Static Generators
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode of The Smashing Podcast, we’re talking about Eleventy. What is it and how does it fit into your Jamstack workflow? I spoke to David Darnes to find out.

<iframe src="https://share.transistor.fm/e/fb5981c3/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- David Darnes [on Twitter](https://twitter.com/DavidDarnes)
- David’s [personal site](https://darn.es/)
- [Eleventy](https://www.11ty.dev/)
- [Eleventy documentation](https://11ty.dev/docs/)
- Andy Bell’s [Learn Eleventy From Scratch](https://piccalil.li/course/learn-eleventy-from-scratch/)
- [11ty Rocks!](https://11ty.rocks) - a collection of Eleventy starters, projects, plugins, and resources created by Stephanie Eckles
- [Build An Eleventy (11ty) Site From Scratch](https://egghead.io/playlists/build-an-eleventy-11ty-site-from-scratch-bfd3) course, also by Stephanie Eckles

### Weekly Update

- “[Introducing Framer Motion](https://www.smashingmagazine.com/2020/10/introduction-to-framer-motion/)”  
*written by Nefe Emadamerho-Atori*
- “[Authentication In Vue.js](https://www.smashingmagazine.com/2020/10/authentication-in-vue-js/)”  
*written by Precious Ndubueze*
- “[How We Run Online Workshops](https://www.smashingmagazine.com/2020/10/how-we-run-smashing-online-workshops/)”  
*written by Vitaly Friedman*
- “[How To Build A GraphQL Server Using Next.js API Routes](https://www.smashingmagazine.com/2020/10/graphql-server-next-javascript-api-routes/)”  
*written by Ibrahima Ndaw*
- “[The Principles Of Visual Communication](https://www.smashingmagazine.com/2020/10/principles-visual-communication/)”  
*written by Elizabeth Lin*

## Transcript

<p><a href="https://twitter.com/DavidDarnes"><img loading="lazy" decoding="async" style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2d85497-356c-4c68-ae6a-9cd30000a0d0/david-darnes-200x200.jpg" width="200" height="200" alt="Photo of David Darnes" /></a><span class="smashing-tv-host">Drew McLellan:</span> He’s a freelance designer, front-end developer, and writer based in Bristol, U.K. With over 11 years professional experience, he’s built up skills in design, UI development, and front-end development, working with names such as Ghost, Stackbit and BaseKit. In his spare time, he also shares his knowledge by writing articles and contributing to open source projects such as Anchor CMS and the Alembic theme for Jekyll. So we know he knows his way around web technologies. But did you know he once crossed the Sahara on the back of tortoise while reciting the complete works of Shakespeare? My Smashing friends, please welcome, David Darnes. Hi Dave, how are you?</p>

<span class="smashing-tv-speaker">David Darnes:</span> I’m smashing, thank you for asking.

<span class="smashing-tv-host">Drew:</span> I know you not only as a friend from the local tech scene here in the wonderful city of Bristol, where we both live, but as someone with a rich background working with different types of publishing tools. We mentioned your experience contributing to Anchor CMS, you recently did a load of work with Ghost, you’ve worked on things for Jekyll, but you’re also somebody who’s really embedded in the JAMstack space. You’ve worked with Stackbit and I’ve seen projects you’ve done around Netlify integrations and right there at the intersection of JAMstack and publishing tools, we’ve got Static Site Generator. It’s no surprise that this is something that’s relevant to your interests.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you a bit about Static Site Generator that seems to be taking the space by storm, or I’d like to think maybe it’s a quiet, reserved takeover, but that is Eleventy. It seems to be everywhere. Where’s it sprung up from?

<span class="smashing-tv-speaker">David:</span> I’m not going to be the oracle of knowledge on the origins of it or anything, but it’s a labor of love, I would describe, from Zach Leatherman. It didn’t catch my eye until maybe a couple of years ago, but it’s in the same realm as Jekyll. Jekyll is a longstanding Static Site Generator which predates JAMstack as a concept anyway. JAMstack being JavaScript, APIs, and Markup to signify the JAM. Recently someone said, "Yeah, but Jekyll doesn’t fit into that JAMstack thing, because it’s not JavaScript." I was like, "Oh, that’s a good point."

<span class="smashing-tv-speaker">David:</span> Eleventy does use JavaScript and more than just accurately being a definition of JAMstack, it’s also a very speedy and much more, I would say, approachable Static Site Generator over Jekyll. However, it does have the similarities of Jekyll, with the templating language and the structure, albeit more flexible. I think that’s a pretty good description of Eleventy itself, I would say.

<span class="smashing-tv-host">Drew:</span> You mentioned things like Jekyll, which is implemented in Ruby, is it?

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> And we’ve got Hugo in Go, there’s Gatsby which is a React Stack, but Eleventy is just pretty much plain JavaScript, isn’t it?

<span class="smashing-tv-speaker">David:</span> Yeah. I think that’s one of the features, I would say. One of the features is that you can write regular JavaScript in there. I do that all the time when I struck up at Eleventy project, I write a bit of no JavaScript in the configuration file. If I want to source from an API or get the Fetch API and sling it about and try and work out, I sync a way until I get something to come back to me. One of the things I need to be better at is working out how that stuff works.

<span class="smashing-tv-host">Drew:</span> That means that Eleventy fits in really neatly into existing JAMstack tooling. If you’re already building those projects, adopting Eleventy into it is going to be quite a natural fit?

<span class="smashing-tv-speaker">David:</span> I would definitely say so. I would say that it fits it... It may be too hard to say this, but I feel like it fits it to a T. I feel that that is quite the definition of a part of a JAMstack tool set. I’m going to say that like JAMstack, that would include other things. So an API could be a CMS of some kind that you’re using Eleventy to source that content from, but definitely I’d say Eleventy fits into that realm.

<span class="smashing-tv-speaker">David:</span> It also fits to somebody who wants to get somewhere precisely rather than... I was thinking of Synology earlier today is, there’s a lot of frameworks that will be like a flight to somewhere. So you fly to like Glasgow, but you want to go to Edinburgh. You want to be somewhere specific. You want to be in a specific town. A big framework would fly you there and then you would have to spend time getting taxis and meandering to exactly what you need.

<span class="smashing-tv-speaker">David:</span> Eleventy is much more like a precise journey to that almost exact location. You will have to do a little bit more work. You might not be able to get a flight straight over there, but it’s going to get you economically to that point more precisely. I think the analogy needs ironing out, but I think it has a substance.

<span class="smashing-tv-host">Drew:</span> You must have worked with other Static Site Generator. Obviously, we mentioned Jekyll. What’s your experience been in the past with other similar systems?

<span class="smashing-tv-speaker">David:</span> I’ve used Gatsby as part of a framework, a part of a live project to quite large site. So I’ve used Jekyll and I have used... I’ve tried Next.js and I’ve tried create some out and Nuxt as well. I should probably say Nuxt and Next, like at the same time, really, because they have similarities. Of course, they would because they’re looking at each other essentially, but they are both very good. I enjoy those ones the most out of the ones that are a bit more like JavaScript intense. I had a lot of fun using them albeit briefly.

<span class="smashing-tv-speaker">David:</span> I think Gatsby and Jekyll would be the ones that I’ve used the strongest in live projects. I would like to use Hugo, because I hear it is extremely fast, like generating stuff. That would be really cool to try out.

<span class="smashing-tv-host">Drew:</span> Yes, that seems to be one of the attributes of Go as a language because there seems to be incredibly efficient and performance out on that all important build step. Do we need another Static Site Generator? Are we reinventing the wheel again and again and again? What does Eleventy do that’s different from all these others? Why on earth would we entertain learning yet another?

<span class="smashing-tv-speaker">David:</span> That’s a great question. With a lot of Static Site Generators, why do we need another in the space? As with many like open source projects, there’s some that are built with the intention to be an open source project there and off. Some of them do really well and some of them not so much. You can tell that there was a little bit of a not hollow incentive, but like the goals of the project didn’t have focus.

<span class="smashing-tv-speaker">David:</span> From what I’ve read and heard is that Zach created this because he needed to build this tooling and it came to be like perfect for his needs. That need is actually a need of a lot of other people. So it fit into that realm. I think that’s how that came to be.

<span class="smashing-tv-speaker">David:</span> There are a lot of Static Site Generators bubbling up and servicing. I liked the variety because the variety means that people who have done... You never know, there’s people out there that just doing Go. They don’t know any JavaScript, they don’t know anything else. If they know Go, then Hugo might be right for them.

<span class="smashing-tv-speaker">David:</span> For like Eleventy, I felt like I know that the typical JavaScript, HTML, and CSS, and that seems very comfortable to me. That’s my safe space. Eleventy fits that area for me really well more so than Jekyll did, I have to say. Like Jekyll, the plugins are a little bit cumbersome to work with. I think Eleventy brings something a little bit more what I was hoping for as a Static Site Generator.

<span class="smashing-tv-speaker">David:</span> It’s a little bit more vanilla in terms of its structure over things like Jekyll. Yeah, I’d say it’s not perfect. I understand that there’re issues with it... Or not issues, but things that people would like out of it, but it doesn’t quite achieve that. But I think it’s got an ND appeal to it. I think that’s why it’s growing fairly quickly.

<span class="smashing-tv-host">Drew:</span> You make an important point about matching the technologies that you’re already using. If you’re building something Go, you might use Hugo as a Static Site Generator because it’s just going to be the tool set that you’re familiar with. If you’re building stuff using React, then you might choose Gatsby because that’s all React.

<span class="smashing-tv-speaker">David:</span> Exactly. Yeah.

<span class="smashing-tv-host">Drew:</span> Having something that is just doing a straightforward JavaScript and just neatly drops into that ecosystem. If you’re writing JavaScript all day, then you’re going to feel right at home and you’re going to be more productive in using it.

<span class="smashing-tv-speaker">David:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> The basic job of a Static Site Generator is to take a bunch of content, which is usually been authored outside of the tool later in... SSGs don’t deal with altering the content. They accept it from somewhere, often that Markdown files, isn’t it?

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> They then go through some templating and turn that into a set of HTML pages. It doesn’t always have to be just Markdown files so does it to these things work with?

<span class="smashing-tv-speaker">David:</span> No, I would say Markdown has become the default API for content on a lot of Static Site Generator. Some of them you can, out of the box, not use Markdown or there can’t be compatible with Markdown, but 99% of the time, Markdown files are content source. However, I find, personally, Eleventy to be really compatible with external CMS. CMS is that have an API of some kind.

<span class="smashing-tv-speaker">David:</span> As you mentioned before, I worked at Ghost and Ghost has a headless option. It could be used in an entirely headless CMS, which means I can pull all the content out of my Ghost installation and feed that directly to Eleventy and construct all the content and API is inside of the templating language to just render pages, render content, render pretty much anything, like get the images out there as well.

<span class="smashing-tv-speaker">David:</span> There’re all ways to pull through content. There’s lots of different CMSs out there, even more so than how many stacks are generators and those CMSs can be pulled into Eleventy pretty comfortably. I wouldn’t say easily, you need a little bit of JavaScript knowledge, of course. But it’s very typical, I would say, to pull in that content using the Fetch API or some JavaScript API that the ecosystem has.

<span class="smashing-tv-speaker">David:</span> Again, Ghost has its own like JavaScript API that you can use to pull the content through. So yeah, you could use all sorts of CMS. Again, you could use WordPress.

<span class="smashing-tv-host">Drew:</span> Yes, because that has a headless mode now, doesn’t it? I guess you could use any CMS that has an API that lets you retrieve content from it?

<span class="smashing-tv-speaker">David:</span> Yeah. You could even use them together. You could use a combination of them. It almost kind of you going back into a, not a monolith project, but you’re using lots of services to pull them together to use them as their strongest parts and then, products and pages and posts and they could be all sourced from all sorts of places.

<span class="smashing-tv-host">Drew:</span> Yeah, so you could have marketing team maintaining a blog in Ghost or in WordPress and you could have some technical documentation being written just in modern files and you can mix and match any of these just a case of how you put that, build step together inside Eleventy. How do you feed the content into Eleventy? You don’t have to write out Markdown files and point it at it. There’s certainly a more sophisticated way than that.

<span class="smashing-tv-speaker">David:</span> For the Markdown files, conveniently, Eleventy will just take those Markdown files. It will see it and go, "Well, let’s mark down," and it’ll start working HTML out of that one. Whereas for an API, to begin with, you would use probably something like node-fetch to pull through that content from an API endpoint, you’d get back like a big blob of like JSON, for which then you can turn that into a JavaScript object and all of those little endpoints and bits of data.

<span class="smashing-tv-speaker">David:</span> Then for example, if it’s posts or pages, that is effectively a collection of things, a collection of blog posts or a collection of pages. Inside of Eleventy, there is a concept of collections. What you can do is in the main Eleventy JavaScript file is say, "Hey, these posts are a collection and I want to treat them like a collection. So please, add them to Eleventy’s internals, and let me iterate through them using the default template in language," and Eleventy is none jokes, but you can use all sorts of different templates in languages in there. Then you can start iterating them over them with a full loop of some kind, and then you can construct pages out of those.

<span class="smashing-tv-speaker">David:</span> It does require a little bit of knowledge and you have to dig around in the documentation. Thankfully, on top of the documentation, there are lots of people that are creating lots of open source projects for which you can cheekily copy and paste a few bits, if you’re like me, but probably read it a little bit to understand what’s going on. But there’s lots of resources out there.

<span class="smashing-tv-speaker">David:</span> The collections thing, I think, is a really powerful tool because when I’ve been using it, I can pull in a collection from anywhere that’s like an array. So the square brackets, you pull it through, you start creating collections and I’m starting to creating like single pages. So like single post pages or single regular pages or product pages. I’m rendering all of those single HTML files and creating collection list views so I can click through to those pages. Suddenly, your site map is now being constructed in not very many moves. It’s very powerful.

<span class="smashing-tv-host">Drew:</span> It seems to strike something of a balance using it in that way with content sourced from a CMS. It strikes a balance between the robustness and speed of a static site and having a nice to work with content editing suite of tools that less technical people in an organization, who may be altering content, would be more comfortable using.

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> It’s a quite an interesting option to be able to do that, to be able to pull in different sources of data. I guess that would really suit people as well, who are working with legacy systems as long as they can get to it with an API of some sort, as long as they can make some issue to be requesting. Even if that’s in RSS or whatever, that would all be workable with.

<span class="smashing-tv-host">Drew:</span> You talked a little bit there about templating and the fact that Eleventy has different templating engine options. Historically, lots of systems can be quite opinionated about which templating language that they use. Often actually, a lot of the functionality that you have within SSG comes from the templating engine. Eleventy isn’t particularly opinionated to do that?

<span class="smashing-tv-speaker">David:</span> No, I have to say it’s as close as unopinionated as you could get. A bit of a personal view, but I struggled to see any framework or anything that can be unopinionated because, in order to create something, you have to have an opinion on how you want to do something. It’s kind of oxymoron. I’m sure people could correct me on that.

<span class="smashing-tv-speaker">David:</span> But yeah, you can switch to whatever templating language you feel most comfortable with. We were just talking about languages that you are comfortable with. Eleventy appeals to that in a sense with what templating languages use inside your HTML, or heck even your CSS, if you want. For me, I just went straight to the nunjucks because nunjucks is the default templating language inside of Eleventy.

<span class="smashing-tv-speaker">David:</span> That means I can use the dot HTML extension and leave it as it is. Now, I’m just going to confuse people even more and say, you can name that however you want. Anyway, you can have real fun with it. But you can use handlebars. I think you can just use regular JavaScript templating and iterate through it like that. Handlebars quite popular, Liquid as well. I can’t think of all of them off the top of my head, but if you set it all up in the configuration, you can just pick however you want it.

<span class="smashing-tv-speaker">David:</span> I’d say, I’m a real big fan of just templating languages in general. It wasn’t too long ago when I found out that you could use twig inside of WordPress and that blew my mind. I was like, "Oh, thank goodness. I don’t have to handle a for loop inside of PHP." Again, I think something a little bit more comfortable and understandable, more readable as well. Yeah, Eleventy has lots of different templating options and it should appeal to people who are comfortable with those different ones.

<span class="smashing-tv-host">Drew:</span> Yeah. Just looking at the documentation for Eleventy that it’s not just a case of, there is a default templating language. If you’re really determined, you can switch it out with something else. There is a great big list of options that you can choose from. You mentioned Liquid, Handlebars, mustache, JavaScript, template literals, just HTML, and all sorts. Ones that I recognize, EJS, Haml, Pug, who knows.

<span class="smashing-tv-speaker">David:</span> Pug?

<span class="smashing-tv-host">Drew:</span> Pug.

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> I’m presuming that’s still a templating language

<span class="smashing-tv-speaker">David:</span> Yeh, I think it used to be called Jade, didn’t it? Then they renamed it because something else was called Jade. So they had to change the name or vice versa.

<span class="smashing-tv-host">Drew:</span> There we go, Pug. That’s quite fun. The community around open source tools can be really important content in setting the tone for what it’s like to learn and to get help when you need it. You mentioned that there were a people building stuff. What’s the community like around Eleventy?

<span class="smashing-tv-speaker">David:</span> All I can answer is from my personal point of view. Other experiences it could vary and I would want to strengthen that community, but I’ve found it to be really strong and really welcoming and encouraging. People are really keen to like want people to have a go with stuff because for a lot of people, Eleventy could be that little extra step from taking a single "flat HTML file" and turning it into something more rich.

<span class="smashing-tv-speaker">David:</span> It could be somebody that, "Oh, I have this HTML file and this is my portfolio site. I want to put my GitHub projects on there, but how do I keep it in sync with my GitHub account?" Well, API pull it through with Eleventy and people are creating example projects of that all the time. There’s lots of different blog templates and there’s lots of people working hard to give people starting points for it, whether it be really quite intense and complex starters. Write down to something really base level.

<span class="smashing-tv-speaker">David:</span> Well, in my opinion, base level. Things like for doing CSS compiling and like really low level stuff to sort out your JavaScript bundles and things like that, right up to, you want to get all the best scores at your lighthouse and you want to have like image resizing and you want all of those powerful tooling and you want to just hit a button and get started with it. They might hit like that deploy to Netlify button probably, and have a site running within a few minutes.

<span class="smashing-tv-speaker">David:</span> So yeah, back to the community part... I got veered off then, but yeah, I would say the community is really strong and encouraging. I’d like to think Zach’s attitude towards the community is permutating into the rest of it. He has a good heart, I would say.

<span class="smashing-tv-host">Drew:</span> I’d agree with that. You mentioned starting points and things, there seems to be quite an ecosystem of different sorts templates and starting points and things with Eleventy. Is it all based on just publishing blog type stuff, or is there anything more advanced in there?

<span class="smashing-tv-speaker">David:</span> I would be inclined to say that probably is probably too many blog template starters. I think that’s a symptom of a lot of Static Site Generators. I think Gatsby suffers from that quite hard. There’s a lot of the blog template starters, which is useful and everything, but there’s a lot of dev bloggers who can do all sorts and start from wherever they want. There’s lots of starting points for them to get going with things and they can get involved with code as much as they like.

<span class="smashing-tv-speaker">David:</span> It would be nice to see some more variation in the community. Like maybe some more e-commerce ones and some more starting points from people who are creating real life projects. You could accuse me as well of making starters that are very much for blogging and things like that. I could probably help in that sense to make more e-commerce starters and things like that. But I’ve seen quite a lot of them.

<span class="smashing-tv-speaker">David:</span> There’s a performance blog template starter at that I’ve been working with, and that is very powerful, but again, that’s a blog templating starter. I think there’s a lot out there, but there’s quite a few are focused on blogging and portfolios to flight that it’d be good to see more wider market. This is how WordPress came to be, WeCommerce and all of that sense where it does all sorts of different things and it’s used on a very commercial level.

<span class="smashing-tv-speaker">David:</span> Maybe when 1.0 of Eleventy drops, some gear change will happen. Don’t quote me on that.

<span class="smashing-tv-host">Drew:</span> That’s an interesting point actually, because Eleventy has been out for quite a while now, but it’s still 0.11 of the moment.

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> Is there any inkling that one might be on the horizon or is that an academic at this point?

<span class="smashing-tv-speaker">David:</span> I follows Zach on Twitter and I see some tweets every of flirtatious idea of 1.0 dropping. That is one of the things that makes me a bit reserved to use it on like commercial projects, because, when I see 1.0 applied to a project, I see that the developers or the people that are on the project think it’s good enough to be 1.0.

<span class="smashing-tv-speaker">David:</span> So if Zach puts 1.0 on it, he thinks it’s good enough to be used in a commercial sense. That’s how I see it. That doesn’t stop me from using it for all different projects out there, but it just gives me a little bit of reservation and yeah, it almost sounds like I’m being a detriment to saying it’s a bad thing of Eleventy. I think we’re just waiting for 1.02 to land so we can use that as a bit more of official thing and bring it up in client meetings to say, "Oh, there’s this thing called Eleventy. It’s a stable project. It’s for commercial use. It’s something we can use."

<span class="smashing-tv-speaker">David:</span> That is to say there has been a React dependency once in a while that wasn’t version 0.1, and yet we still used it on like live stuff because he was like, "That’s the only way I’ve seen anyone else do it."

<span class="smashing-tv-host">Drew:</span> I guess that’s the convention is net with semantic versioning that while some things at zero point, whatever, the API could just change all the time. It’s almost like every release could be like emerging version.

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> In practice, probably, Eleventy I think is one of those that is much more stable than that. Perhaps what we’re actually experiencing here is more like version one point whatever, with enough by one error.

<span class="smashing-tv-speaker">David:</span> Yes. That’s more the case.

<span class="smashing-tv-host">Drew:</span> But, in terms of structuring projects, and this might take us a little bit away from Eleventy in particular, but it does apply. There are different ways you can build your tool chain with Static Site Generator. You can do things like run Eleventy locally, generate a whole load of HTML files. You can commit those HTML files to a rebound and publish that.

<span class="smashing-tv-host">Drew:</span> If you’re using a hosting provider that has the capability to run a build process, you just commit your source content and then have that build process run up on your hosting. How do you typically do that? Are there pros and cons of doing it either way?

<span class="smashing-tv-speaker">David:</span> That’s a good question actually, because one of the cons... If people are already listening, who already used a lot of Static Site Generator, they’ll probably know about platforms like Netlify and Vercel that do the build processing automatically. Any change to the code base will mean that a rebuild will happen.

<span class="smashing-tv-speaker">David:</span> I was about to say one of the drawbacks to that is that the process just disappears into the realm of hosting and the deployment system. Now, I can watch that build process happen, but the client can’t watch that because, it’ll be like the matrix is they won’t see blonde and brunette and stuff like that. They’ll just see a lot of like characters happening and they might understand some of the wording, but really they want to see the change. They want to see, aka, a preview of something happening.

<span class="smashing-tv-speaker">David:</span> There is a detriment to that as opposed to having almost a build process locally to them that automatically regenerates that. There are CMSs out there that can do that and there’s also Static Site Generator that can do that as well and build that process in. I believe Next.js has a preview option, which means that you can pull the API content straight through and see it immediately.

<span class="smashing-tv-speaker">David:</span> There is a drawback to that, but I would say there’s more of a drawback to doing it, the manual method of rebuilding it locally, and then pushing up your directory of HTML, CSS, and JavaScript, and just slinging a big blob of it at SFTP server. That is to say that I have done it. I have had to do it for certain reasons. I do remember using Sage to host stuff and that’s the state co-hosting platform, but it didn’t have a deployment light build process. I don’t think it has either now.

<span class="smashing-tv-speaker">David:</span> So what I would do is build it and then throw it at Sage and just host it there, which was really useful for prototype development. So I would be building stuff with JAMstack principles and creating prototypes with that, build it, throw it up to a Sage domain and then share it with my team and share it with like QA people to understand what’s going on.

<span class="smashing-tv-speaker">David:</span> There are pros and cons, I guess there are different purposes. The manual process is good for people who are in the code. I wanted you to understand, I wanted to keep an eye on everything and control the dials more. Then the build process or having it all automatically done with things like Netlify and Vercel means that they can automate the whole thing. Not only that use things like build hooks to automatically regenerate the sites when the client makes content change on something like WordPress.

<span class="smashing-tv-speaker">David:</span> The content change happens and then a build process has begun on Netlify and it will rebuild the entire site. For example, like Eleventy will rebuild and the new content will appear there.

<span class="smashing-tv-host">Drew:</span> I guess, doing it the manual way gives you the ability if you are pulling in content from systems that might just exist on a private network, or might not have APIs that are publicly accessible. That need to be then done offline, wouldn’t it?

<span class="smashing-tv-speaker">David:</span> Yes.

<span class="smashing-tv-host">Drew:</span> You couldn’t do that in the cloud if those APIs weren’t available?

<span class="smashing-tv-speaker">David:</span> No, that is true. You probably have local credentials that you would only be able to access from your machine. That was a good point. I guess, that’s a bit more of a layer of security and the publishing processes is a bit more officialized. I wouldn’t be surprised that larger platforms, like, I could see things like The Guardian, as something that needs to go published.

<span class="smashing-tv-speaker">David:</span> Having a single published button seems a little bit too powerful and having like a publishing process that gets approved by developers and editors because the site is so reliant on the web, there would be content, people were working together to get that up there. So, yeah, that is a good point.

<span class="smashing-tv-host">Drew:</span> One of attributes of Static Site Generator that have caused me to migrate projects to different platforms in the past has been the speed of that build step. The time it takes to process all your content into HTML pages. How does Eleventy fare on that front? Is it quick? Is it slow?

<span class="smashing-tv-speaker">David:</span> I would say it is one of the quickest, definitely one of the fastest. It’s hugely faster than Jekyll. I’m sorry, Jekyll. I love you. But I’ve got a project somewhere that is 10 minutes to rebuild, and it’s not a particularly large amount of content. You’ll see the difference if you’re coming from Jekyll. By the way, if I haven’t made it clear, if you’re coming from Jekyll and you want to look at something newer, I definitely suggest looking at Eleventy as your next Static Site Generator. But it’s not the fastest.

<span class="smashing-tv-speaker">David:</span> I would say Hugo is the fastest running on Go. Eleventy is based on JavaScript. So it’s only going to be as fast as JavaScript itself. I guess the familiarity of JavaScript is how it would beat it in terms of like Hugo, there’s a bit more of a smaller community with Hugo. That’s how you would trumpet in that sense, but on pure speed, Eleventy is just behind it.

<span class="smashing-tv-speaker">David:</span> But I think that’s a nice place to be in, to be one of the fastest. I know other Static Site Generators and generative tools or frameworks out there much slower in processing a large amount of content. If you’re looking for something that generates documentation, as you would know, documentation sheets can be massive and Eleventy would happily digest that and turn into a site.

<span class="smashing-tv-host">Drew:</span> Ingest, I think?

<span class="smashing-tv-speaker">David:</span> Ingest, yes.

<span class="smashing-tv-host">Drew:</span> Ingest, yeah. I guess, JavaScript is a good place to be. It’s a good bet to make. If you’re looking for speed, because in terms of the ecosystem, there’s a lot of effort all the time in improving the engines and making it run faster because so many people are depending on JavaScript so much these days.

<span class="smashing-tv-host">Drew:</span> You mentioned large sets of content. Sometimes you see things like while sorts was publishing tools, but Static Site Generator CMSs that provide a really good demo of workflow and speed and everything when they’ve just got 20 build posts in them. Then as the content in a volume grows over time, they just get completely bogged down and they don’t scale and they don’t respond linearly to large amounts of content. Have you got any experience with big content sets in Eleventy or know if people have been working that way with it?

<span class="smashing-tv-speaker">David:</span> That’s a great question because I haven’t actually used it myself with large content sets. But I do know that there are fast quotes of build times for thousands of pages at at a time. I would caveat in that saying, and I don’t know how contrived those pages are. There could be just a couple of paragraphs or something like that, nothing too complex.

<span class="smashing-tv-speaker">David:</span> I would say that, in my experience, I’ve used Gatsby and other generative tools that I have large content sets. I would say Eleventy leads it in the dust, quite measurably, which is the same to things like Gatsby that fall behind because they’re doing so much other stuff going on. One of the great things about Eleventy is that, if you have a project that just has some HTML files in it, it’ll do it. It’ll just go through them and it will just output it and do its thing.

<span class="smashing-tv-speaker">David:</span> You can be very low level, you can be very high level with it. Whereas on a Gatsby project, the benefit is having all of those features and tooling in there, but it’s also a detriment as well. You’ve already slow because you’re doing all of these magical things and now I’ve got to undo it. Again, it’s that starting point that you want to go with. But I would say it’s very fast. I would need citation needed for actual build examples.

<span class="smashing-tv-host">Drew:</span> But what’s the documentation like with Eleventy? Is it pretty comprehensive?

<span class="smashing-tv-speaker">David:</span> I find it all right to navigate. I understand I’ve seen a few comments about people having trouble getting around the documentation and I see their gripes. I’m not the source on like the best documentation there is. But as part of my job, I do a lot of content for documentation sites. I’ve done it for Ghost and I did it for Anchor CMS and I did it for BaseKit as well, like building out the template and documentation there.

<span class="smashing-tv-speaker">David:</span> In comparison, I think it still requires a little bit of navigating and a little bit of understanding of how Eleventy works itself before you get around and find your way around. I personally have had struggles where I’m going, "Where is this? I’ve seen this before on this page and it is there."

<span class="smashing-tv-speaker">David:</span> There is lots of content and there are lots of references to external projects and examples and articles and all different things. So there’s lots out there. But I think the documentation just needs a little bit of improvement and things. That’s not directed at Zach because it’s an open source project. The documentation is there for everybody to contribute to, myself included.

<span class="smashing-tv-speaker">David:</span> Everybody can improve that over time, especially with a community like that, I could see that documentation really shining. But I would say, it’s there. All the documentation is there for you to use, but it does require a little bit of navigating.

<span class="smashing-tv-host">Drew:</span> I think that it’s a fairly common problem as never documentation that everybody thinks in different ways and would expect to find things in different ways. So it’s almost impossible to structure a set of documentation that’s going to be perfect for everyone. You have to choose which shape it’s going to be. I hope it will work well from most of the people and will be acceptable to those who look at the problem in the other way.

<span class="smashing-tv-speaker">David:</span> Definitely.

<span class="smashing-tv-host">Drew:</span> Is there a sort of an ideal project that would be suited to Eleventy, like down to the ground? If somebody came to you and said, "I’ve got this type of project," and you think, "Yes, Eleventy is the solution for that." What is that type of project?

<span class="smashing-tv-speaker">David:</span> I think one of the best types of projects for Eleventy is a front of house website. A front of house website would be the... A lot of people call it like the .com, the site that people go to, to find out about a company or a product or something like that. The contract example would be the contact page, about us page, and home page and all the classics.

<span class="smashing-tv-speaker">David:</span> But definitely a front of house website, possibly the documentation and the blog, as well as you grow that site, Eleventy will grow with that. You can add your blog being sourced from wherever. You can have your documentation, again, being sourced from somewhere else. I’m about to do a few projects that are with Eleventy and using it on front of house sites, but I think it’s a really ideal use for it.

<span class="smashing-tv-speaker">David:</span> That is to say, it’s not that it can’t do those other things. You could do a PWA, like an entire application, whether if you want to. But for me, like that front of house websites, like promotional sites that show people, companies like services, and you do like a nice pricing page and stuff like that, you can source all that content there. I think that those types of sites are really good candidates for Eleventy.

<span class="smashing-tv-host">Drew:</span> What would be the best way of somebody to get started with Eleventy? What should they do if they think it sounds good? Where do they go?

<span class="smashing-tv-speaker">David:</span> I guess they would go to Eleventy, whichever way it’s spelled, 11ty.dev. I would definitely go there and check that out. I would also hit up a few articles. I know that there is Eleventy From Scratch by Andy Bell. That is a good content source. That’s a premium course for you to learn Eleventy.

<span class="smashing-tv-speaker">David:</span> I would also check out, I think there’s a few others. I need to strike them out. Can we put those in the show notes or something that would be-

<span class="smashing-tv-host">Drew:</span> Yes, definitely. Yeah.

<span class="smashing-tv-speaker">David:</span> I’ll find the ones that I’ve been looking at.

<span class="smashing-tv-host">Drew:</span> Fantastic. You mentioned that you’ve got some projects coming up that you’d be using Eleventy. You’ve recently gone freelance, haven’t you? What projects and work are you hoping to take on?

<span class="smashing-tv-speaker">David:</span> Is this my opportunity to plug?

<span class="smashing-tv-host">Drew:</span> It is.

<span class="smashing-tv-speaker">David:</span> Thank you, Drew. Thank you. So yes, I have recently become full freelance and my intentions are to work on frontend development and documentation and content, as well as a piece of design. I do have some design background. Some, I have a degree, but what do degrees mean now? So yes, it’s a myriad of those three areas.

<span class="smashing-tv-speaker">David:</span> I do quite a lot of front end development with Eleventy and Jekyll and I’ve done a fair bit of WordPress and things like that. Lots of different front end projects, and I will stretch to the full stack characteristics if needs be, as a lot of devs end up doing under there, whether they want to or not.

<span class="smashing-tv-speaker">David:</span> I do that and I do documentation for content. So content for documentation, I should say, quite a loving experience with different site builders and building out the documentation for that.

<span class="smashing-tv-speaker">David:</span> I’ve also done a lot of articles for various different platforms. I’ve written for Touch Plus and I’ve written for Siteleaf, which is another headless CMS for Jekyll. That’s a pretty good CMS. I have actually, in the past, done some video courses. It’s been been a little while. It’s the origin of this microphone is doing a few video to video courses and stuff like that, which is really cool. That kind of stuff that’s what I’m trying to do.

<span class="smashing-tv-host">Drew:</span> That’s great. Exciting times. I’ve been learning all about Eleventy. What have you been learning about lately, Dave?

<span class="smashing-tv-speaker">David:</span> Oh, well, I’ll be honest. I’ve been learning a bit of Eleventy as well. I’m not there yet. Like I said, I’m not the fountain of knowledge on it. But it’s great to just jump into... I’m working with Eleventy and I find something that I want to know more about and I jump into the docks. It’s interesting how many little tips and tricks are in there. I really enjoy that.

<span class="smashing-tv-speaker">David:</span> I’ve been learning. Yeah, I’ve been trying to get my head around Hugo is the template in language, quite different, but it’s quite cool. It’s quite cool. I like it and I want to learn more of that. I’ve also been doing a bit more about build plugins for Netlify. I did a build plugin, which means that you can add stuff into the build process on Netlify as platform. That’s quite cool. I’ve been learning a bit more of that.

<span class="smashing-tv-speaker">David:</span> I’ve been learning a bit more node and well, I guess I’ve been learning how to make coffee as well. I’m a bit coffee obsessed. So in my spare time, I try and learn how the best way to do it. Then I sip it and I go, "Hmm, that tastes like coffee. I must have done it right." I’m quite proud of myself because I’ve got to the step where I don’t need to add sugar to my own coffee. So it tastes okay. Before I was doing it so badly I had add sugar to mask the bad bits.

<span class="smashing-tv-host">Drew:</span> Amazing. If you, dear listener, would like to hear more from Dave, you can find him on Twitter, where he’s @daviddarnes and his personal website. You can see his work and hire him to work on your projects. It’s at D-A-R-N.es. Thanks for joining us today, Dave. Do you have any parting words?

<span class="smashing-tv-speaker">David:</span> All I say is, thank you Drew for inviting me onto the show and please feel free to tweet me about all sorts of stuff. Please, correct me if I said anything wrong. I love to learn. Thank you.



{{< signature "il" >}}
