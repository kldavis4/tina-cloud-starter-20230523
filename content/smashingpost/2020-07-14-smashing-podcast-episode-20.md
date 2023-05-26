---
title: 'Smashing Podcast Episode 20 With Marcy Sutton: What Is Gatsby?'
slug: smashing-podcast-episode-20
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e64187b-19bf-4a24-9965-2969096756d6/smashing-podcast-episode-20.png
date: 2020-07-14T05:00:00.000Z
summary: >-
  We’re talking about Gatsby. What is it and how does it fit into your web development stack? Drew McLellan talks to expert Marcy Sutton to find out.
description: >-
  We’re talking about Gatsby. What is it and how does it fit into your web development stack? Drew McLellan talks to expert Marcy Sutton to find out.
categories:
  - Smashing Podcast
  - Gatsby
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

Today, we’re talking about Gatsby. What is it and how does it fit into your web development stack? Drew McLellan talks to expert Marcy Sutton to find out.

<iframe src="https://share.transistor.fm/e/5f38933c/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [Gatsby](https://www.gatsbyjs.org)
- Marcy on [Twitter](https://twitter.com/marcysutton)
- Marcy’s [personal website](https://marcysutton.com)

### Weekly Update

- “[Make Your Sites Fast, Accessible And Secure With Help From Google](https://www.smashingmagazine.com/2020/07/web-dev-live-google-event-2020/)”  
*by Dion Almaer*
- “[Understanding Plugin Development In Gatsby](https://www.smashingmagazine.com/2020/07/understanding-plugin-development-gatsby/)”  
*by Aleem Isiaka*
- “[Creating Tiny Desktop Apps With Tauri And Vue.js](https://www.smashingmagazine.com/2020/07/tiny-desktop-apps-tauri-vuejs/)”  
*by Kelvin Omereshone*
- “[Removing Panic From E-Commerce Shipping And Inventory Alerts](https://www.smashingmagazine.com/2020/07/ecommerce-shipping-inventory-alerts/)”  
*by Suzanne Scacca*
- “[CSS Transitions In Vuejs And Nuxtjs](https://www.smashingmagazine.com/2020/07/css-transitions-vuejs-nuxtjs/)”  
*by Timi Omoyeni*

## Transcript

<p><a href="https://twitter.com/marcysutton"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59225f0c-cfc0-40b5-9180-a4e9485f6e38/marcy-sutton-200x200.jpg" width="200" height="200" alt="Photo of Marcy Sutton" /></a><span class="smashing-tv-host">Drew McLellan:</span> She is the lead engineer on the Developer Relations team at Gatsby. Previously, she worked on the open source axe-core accessibility testing library, and has also worked as an accessibility engineer at Adobe. She’s passionate about improving the web for people with disabilities and often speaks about it at conferences. In 2016, O'Reilly gave her web platform award for a work in accessibility.</p>

<span class="smashing-tv-host">Drew:</span> She also co-leads the accessibility Seattle and NW Tech Women Meetups in a local region. So, we know she’s a skilled engineer and an accessibility expert. But did you know she wants to send it Angel Falls in a barrel? My smashing friends please welcome Marcy Sutton.

<span class="smashing-tv-speaker">Marcy Sutton:</span> Hello.

<span class="smashing-tv-host">Drew:</span> Hello. Marcy. How are you?

<span class="smashing-tv-speaker">Marcy:</span> I’m smashing. How are you?

<span class="smashing-tv-host">Drew:</span> I’m very good. Thank you. I wanted to talk to you today about Gatsby. Because it came up in a conversation I was having on a previous episode about learning React with Mina Markham. I realized I was in danger of doing the typical man on the internet thing of giving an opinion on something that I had no direct experience of. So that’s not how we do things at Smashing.

<span class="smashing-tv-host">Drew:</span> And I want to make sure that we properly cover Gatsby. And what better way to do it than to talk somebody who knows it inside and out. So, presuming that perhaps I’ve heard the name Gatsby. But I’ve got no idea where it fits into the stack when building website. What exactly is Gatsby.

<span class="smashing-tv-speaker">Marcy:</span> Gatsby is a website generator, it currently uses React. But it will create a static website for you that then will rehydrate into a full React web application. So you really get the best of both worlds with fast builds that you’re compiling HTML files that will load fast for users. And then you get all of this enhancement with JavaScript to make really interactive dynamic web apps.

<span class="smashing-tv-speaker">Marcy:</span> So, it’s really exciting space to be in. And I’ve been working on the learning side with documentation and now on the Devrel team, I’m focused on making it as good as it can be, knowing accessibility challenges with JavaScript and just trying to fix it from the inside out.

<span class="smashing-tv-host">Drew:</span> Many of us will be familiar, I guess, with the concept of a static site generator. And Gatsby seems to broadly fit into that role. But to me, it seems like it goes a lot further than the most SSG’s do. And most site generators are front-end code agnostic. It seems that with Gatsby, you end up with Gatsby code running as part of your site. Is that a fair assessment? And if so, what sort of things is Gatsby actually doing in your front-end?

<span class="smashing-tv-speaker">Marcy:</span> Yes, I’d say the biggest piece of that is client side routing. So, Gatsby right now is using reach router under the hood. It does kind of its own implementation. But that is the piece that when you load your static site for the first time, there are HTML files there. So, if the user turns JavaScript off for some reason, your site should still be there, still have content.

<span class="smashing-tv-speaker">Marcy:</span> But if JavaScript is enabled, that’s when this hydration step happens where, when you use links in your Gatsby site, it will go pre-fetch resources from that page, so it will load faster. So, that is all enabled with this JavaScript layer that Gatsby gives you. And so beyond that, it really depends kind of what you’re using in your site will end up in that JavaScript bundle.

<span class="smashing-tv-speaker">Marcy:</span> But for things that use a lot of interactivity, like accessible interfaces, that’s a good place to be. For me, I really enjoy having JavaScript available to me at all times, and having my markup just be in a good spot. I know it’s a matter of preference, whether you want your HTML and your JavaScript and your CSS all kind of neatly coupled and there’s room for variations within building Gatsby

<span class="smashing-tv-speaker">Marcy:</span> You don't always have to use something like CSS and JS. But it’s really about getting the power of that dynamic JavaScript layer, available to you while you’re writing your website. It’s not like this add on in a separate file.

<span class="smashing-tv-host">Drew:</span> When I think of how a static site generator usually works, I’m thinking of content in perhaps Markdown files. And the generator runs across that content and merges it with templates and creates 10s, hundreds, thousands of HTML files, which are the pages of your website. When I think of a React site or app, I’m thinking more about single page experience where the interfaces be created by React on the fly. So, you’re saying Gatsby does both of those? It’s creating all the pages and also enhancing it with JavaScript?

<span class="smashing-tv-speaker">Marcy:</span> It is, yes. Gatsby will use Node.js at build time, it will go over your React components and compile them into HTML files. Which honestly, the first time I looked at Gatsby I wouldn't turn JavaScript off and was like, "All right, are there other pages here, what is this?" And I was so happy that Gatsby works that way by default. It will create built files from your react components, which is awesome.

<span class="smashing-tv-speaker">Marcy:</span> I have explored more progressive enhancement approaches since it’s in JavaScript. Like what if you want to output something progressively enhanced for users, where if they do have JavaScript turned off, you don't want all this broken code that assumes JavaScript is there. So there are some quirks with it. But you can work around that kind of thing at least for your core user flows where you want someone to still be able to buy something, you might need to add some support and for those use cases.

<span class="smashing-tv-speaker">Marcy:</span> But I’ve been pleasantly surprised that the way that Gatsby rolls that out by default. And so, it is a choice that they made to build sites that way, and we’re always evaluating it. Is it still the best way? What do we need to do to give our users what they’re asking for? So, we’re doing some explorations internally, ongoing just to make sure Gatsby is doing the best job it can at building a website.

<span class="smashing-tv-speaker">Marcy:</span> So keeping bundle sizes small, and making sure that for making trade offs for what we say is performant code with pre-fetching. Like, do we have the data to back that up? That’s the kind of thing as a developer advocate that I’m super interested in, is making sure that what we’re packaging and bundling on websites is actually needed and will really make the best Gatsby site it can make.

<span class="smashing-tv-host">Drew:</span> You mentioned performance there, and there’s a big focus on performance. It certainly seems from the way that Gatsby presents itself. Is that a true feature of Gatsby or is it just the nature of JAMstack websites?

<span class="smashing-tv-speaker">Marcy:</span> I think it can be a nature of JAMstack websites. Ultimately, it’s going to come down to what you’re bundling on your website. So, no matter what framework or tool you’re using, we still have to be thoughtful in what we’re putting in those bundles for end users. But Gatsby really aims to give you good defaults. Not only for performance, but for accessibility as well.

<span class="smashing-tv-speaker">Marcy:</span> But that always takes evaluation, we always have to make sure that if we’ve added something, that it’s still performant. But yeah, getting that initial payload of static files, they load fast. Much faster than classic WordPress site that I used to have. But then enhancing it with JavaScript. There are some trade offs there for sure.

<span class="smashing-tv-speaker">Marcy:</span> But it works really well, lots of people, they really like their Gatsby sites. So, it’s been fun to get to work on it full time, and learn the ins and outs of a JavaScript framework like Gatsby.

<span class="smashing-tv-host">Drew:</span> What sort of performance features just Gatsby actually put into place to speed up your sites?

<span class="smashing-tv-speaker">Marcy:</span> Well, with the pre-fetching for links, this client said routing stuff, I’d say that’s probably the biggest one. Making it really easy to generate a progressive web app. So, having some offline capabilities, you can sort of pick and choose what you want in terms of offline and PWA type stuff. But they really make that part of the initial experience, like a lot of the starter example sites that you might start from have examples of using a manifest, and kind of making that modern version of your website.

<span class="smashing-tv-speaker">Marcy:</span> Really, it’s like not shipping code that you don't need. That’s a big part of it. Caching, that’s really the pre-fetching for links. That’s what I would say is the biggest piece of it.

<span class="smashing-tv-host">Drew:</span> So this is where the site is actually anticipating where the user is going to go. Is it as intelligent as that or does it pre-fetch everything on the page or?

<span class="smashing-tv-speaker">Marcy:</span> No, it’s based on user interaction. So, if the user scrolls down the View port, there’s something pre-fetching that happens there. If you hover over links, it will kind of estimate that there’s a pretty good chance that you might go to that page. We’ve been talking internally, well, I guess, open source to about whether that pre-fetching should happen on keyboard focus too, so that intersection of accessibility and performance is very interesting.

<span class="smashing-tv-speaker">Marcy:</span> There’s some trade offs there like should a keyboard user who can't use the mouse and is tabbing through every link to navigate, should that really be fetching content for every single one of those because a mouse user might be a bit more selective about where they put their mouse cursor. So, those conversations I find extremely fascinating.

<span class="smashing-tv-speaker">Marcy:</span> And trying to think of what data do we need to validate these assumptions too. So yeah, it’s been super interesting to look at those defaults and what improvements can we make and really checking like how much data is that fetching? Is that really a good thing? Just to speed it up a little bit? Or is it fast enough without that? Are there alternative solutions that we could use as part of the fun of working on a framework because being able to evaluate all those trade offs.

<span class="smashing-tv-host">Drew:</span> This is pre-fetching something that users just get for free in their site. So do they have to do any work to implement it?

<span class="smashing-tv-speaker">Marcy:</span> You do get it for free using Gatsby link. So it’s a component that comes with Gatsby and when you use that, it outputs anchor tags. So your HTML is real HTML and you’ve leveraged the web platform in that way. But in your React components, you are working directly with the Gatsby link component. And that has all of those mechanisms for... It looks at whatever your future HREF will be, for that link of where you want to go to and it will go and grab resources from that link and preload them.

<span class="smashing-tv-speaker">Marcy:</span> And it’s only internal to your site. So it’s not going off and trying to fetch things on other websites. But it seems to work pretty well. I know some users are actively looking for ways, like you actually have to opt out of some of these things. At least routing, not using the pre-fetching. You just use regular anchor tags. And then you don't really get that functionality. It’s pretty easy to use something else. But some of the discussions we’re having are around client side routing, and how to make that the best it can be. And so, that’s a really interesting space too.

<span class="smashing-tv-host">Drew:</span> How closely do you have to work within the Gatsby ecosystem in terms of if I wanted to have my own link component? Would that be completely fine, I wouldn't be fighting against Gatsby to do that sort of thing?

<span class="smashing-tv-speaker">Marcy:</span> No, you could slot in whatever components you want, as long as they work with the React runtime. That’s really the beauty of it. Anything you could put in a React app, you could put in a Gatsby app. There’s even a pre-React plugin. So, there are some alternatives to working with Gatsby. But I love how you can pull in whatever, off the shelf components that you want to use or write your own.

<span class="smashing-tv-speaker">Marcy:</span> And I think that flexibility is what people really enjoy. There is the caveat of it uses the React runtime. And so, you have to be okay with using react or using this pre-React plugin. But personally, I really like react and JSX for working with accessibility and templates, especially with React hooks. So, being able to use the hut in my Gatsby site is just so cool. I really like it.

<span class="smashing-tv-host">Drew:</span> And how’s the process of building a Gatsby site that’s presumably a node module that you can just install and you would do a build like you would with any other static site generator?

<span class="smashing-tv-speaker">Marcy:</span> Yes. There is a CLI that you install globally. And I guess it’s whether you want to install it globally. That’s what we recommend, because then you can run it from any directory on your computer, but it will pull down whatever you need to build a Gatsby site. And then you can add on, say you wanted to use WordPress as a headless CMS or some other content source.

<span class="smashing-tv-speaker">Marcy:</span> You can install packages, plugins to make that work, and then integrate it with your site. There’s also some starters and themes that you can use to get up and running quicker. I’ve used those if I want to test out something or start a site rapidly for a specific integration like Drupal or prismic or whichever CMS or eCommerce solution or something I want to use.

<span class="smashing-tv-speaker">Marcy:</span> There’s lots of examples. So you’re not always tinkering with trial and error trying to figure it out, but it’s sort of these building blocks that you can piece together and create... It’s what we call the content mesh. And so, you can use these best in breed integrations to create a site instead of, if I had a classic WordPress site, the authoring experience and working with teams is really great.

<span class="smashing-tv-speaker">Marcy:</span> But there were shortcomings in the front end, like how it would work on a mobile device. What else? If I wanted an eCommerce solution? I think there’re some things that are easier to do these days, but being able to pick whichever kind of best solutions you want for authentication, or whatever that modern thing is, you’re like, "I wish I could use that." With Gatsby, you can pull a lot of these things together and make this content mesh way of building that’s pretty refreshing.

<span class="smashing-tv-speaker">Marcy:</span> Especially when you can still use those integrations like WordPress and still work with teams. So, we’re pretty excited about this new way of working where you can pick all the technologies that you’ve like, or that work for your team.

<span class="smashing-tv-host">Drew:</span> One of the big features that Gatsby has tout strongly is this ability to pull in data or content from a variety of different sources. You mentioned things like WordPress and Drupal, and what have you. Traditionally, if I was using something like Jekyll or Eleventy, or something like that, I would need to wire up that myself to interact with API's, perhaps pull content down and write it into markdown files or JSON files, and then have the generator work with those files.

<span class="smashing-tv-host">Drew:</span> So it would be a sort of two step process, could use something like source bit, which we covered on a previous episode that does that sort of thing? Do I understand rightly that Gatsby has just this native ability to consume different sources in a way that other static site generators, just don't?

<span class="smashing-tv-speaker">Marcy:</span> I think what makes Gatsby really strong in this area is its GraphQL data layer, and the plugin ecosystem. So, chances are someone has already written a plugin for whatever data source you’d be looking to build. And if not, there’s probably something close. But using GraphQL, is kind of the under workings of it. The layer that makes all of these integrations possible is using GraphQL.

<span class="smashing-tv-speaker">Marcy:</span> And so, there’s lots of possibilities for what you could pull in and we try to make it easy to write plugins too. So it’s been really neat learning about how to write a plugin, and the AST or Abstract Syntax Tree that it creates and kind of learning about how all that works has been really cool. But yeah, I’d say, there are a lot of things off the shelf that you could pick up without having to write it all yourself, which is pretty awesome.

<span class="smashing-tv-speaker">Marcy:</span> And it’s nice to have the flexibility to pull in markdown. Say your developers want to write their blog content markdown, but the marketing team is really not happy with that, you could combine content sources, and source them from multiple places. I’ve seen people sourcing things from other GitHub repos, and they use a get plugin to pull in markdown content that way. Lots of flexibility.

<span class="smashing-tv-host">Drew:</span> And I guess you’ve got the option then of writing your own plugins to pull from a custom data source. Say you’ve got some legacy system and you want to put a nice, shiny new website on the front of it. You could write a plugin that would get the data out in whatever format that is needed and translate it into something that gets bigger than work with?

<span class="smashing-tv-speaker">Marcy:</span> You could yes. And so, plugins enable that. And then there’s this abstraction on top of that, which we call Gatsby themes. And those are not only user interface code, but they could be GraphQL queries, configurations that set up a plugin, so it’s like a plugin with usage kind of bundled together. And you can distribute those themes on NPM.

<span class="smashing-tv-speaker">Marcy:</span> And then, their version and you can pull them in. And that whole API is really interesting too for teams who say you have multiple repos, and you want to pull data into those, it would be very repetitive to have the same queries in all of these repos in the same code. So, to dry things up a bit and not repeat yourself so much. You can use these abstractions called themes, to sort of distribute around that logic or code that would enable that source plugin. So, there’s these kind of layers of abstractions that you can build on top of it that we’ve heard that teams are really getting a lot out of right now.

<span class="smashing-tv-host">Drew:</span> So a theme in the Gatsby world isn't a look and feel like it would be with CMS like WordPress.

<span class="smashing-tv-speaker">Marcy:</span> Yeah, I mean, it can but that’s not all that it is. So, naming things is very hard. But themes I’ve really enjoyed learning about just the flexibility and being able to, yes, you could include some user interface code. But there could be some query language code that goes in there as well. But the fact that it’s kind of bundled together, makes it easy to distribute. Yeah, it’s been a really neat abstraction that it’s been cool to see what people are building and what themes they’re shipping, and all that.

<span class="smashing-tv-host">Drew:</span> Yeah, I can imagine it would lead to some fairly innovative uses of Gatsby. Have you seen anything that’s been, in particular that caught your eye that customers are doing this particularly creative?

<span class="smashing-tv-speaker">Marcy:</span> Yeah. Well, in terms of themes, I mean, one of the first ones I read about there’s a case study on the Gatsby blog, I think from Apollo. And they wrote a documentation site using Gatsby themes and that used a get source plugin. And so, it really kind of decouples your sourcing, and your content, making it so that teams can pull in a theme to use across multiple repos.

<span class="smashing-tv-speaker">Marcy:</span> I’d say that’s the most interesting to me just because of what I can envision it enabling like, past teams I was on where we had to source content, we were just so like limited and where that code could live and how repeatable it could be. And so, seeing a solution now where teams are like, "Oh, this works great." And that was even last summer, or like that was a case study a while ago.

<span class="smashing-tv-speaker">Marcy:</span> So since then, API’s have been improving, and there’s a whole team working on Gatsby themes. And I know they are rolling out some big improvements in the next few weeks. So, I don't want to steal their thunder, but there’s some neat stuff coming with themes. They’ve been overhauling some of the blog themes like the core themes that we offer from Gatsby.

<span class="smashing-tv-speaker">Marcy:</span> I know they’re using it internally to build some of our own product announcement, or product improvements that will be announced here in the next couple of weeks. So, lots of cool stuff going on with Gatsby themes, and people selling their own themes and starters. I think that’s really interesting too.

<span class="smashing-tv-host">Drew:</span> There’s a bit of a marketplace springing up around Gatsby.

<span class="smashing-tv-speaker">Marcy:</span> There is, Yeah.

<span class="smashing-tv-host">Drew:</span> Is there any sort of online training and those sorts of things if somebody wants... If somebody decided that they were really going to get into Gatsby and they needed to learn it quick? Are there run places they can go with that sort of information is available?

<span class="smashing-tv-speaker">Marcy:</span> A ton of it? Yes. There’s definitely the Gatsby Doc’s site, which is gatsbyjs.org/doc's. And we have tutorials, and I’ve been doing live streams almost every week for Gatsby stuff. There are a ton of educators who have Gatsby material on YouTube and various learning platforms. Egghead, I think some of my teammates from Gatsby have egghead videos as well.

<span class="smashing-tv-speaker">Marcy:</span> So, there is a ton of stuff out there. I would say check the dates on it if you find something. We’re always actively updating the Gatsby Doc's, some of the older third party videos and things that may, check the dates on those because we can't monitor every single learning resource for update. It’s hard to keep up with our own staff.

<span class="smashing-tv-speaker">Marcy:</span> Because there’s just so much with how many content sourcing options and use cases. It’s a very broad space. But there’s so much learning material out there, and a ton of ways to get started that you can sort of try and find things like depending on where you are on your learning spectrum. Are you at the beginning stages, are you coming from other technologies and you just need to learn about like what is this React thing.

<span class="smashing-tv-speaker">Marcy:</span> You can sort of pick and choose which materials will work for you based on where you’re at. I’ve been doing a course recently through live streams called Gatsby Web Creators, where we went all the way from beginner HTML, CSS and JavaScript through to creating our first Gatsby site. We just completed that on Friday. And so, it’s been really neat to go all the way back to the beginning.

<span class="smashing-tv-speaker">Marcy:</span> And because a lot of materials with Gatsby, it uses React. So, it’s a pretty big jump to get started with that. So, I really wanted to go back and take the steps to get all the way through to building things with React and Gatsby. So that was really neat. And I’m excited to continue on that route, so that there is more beginner material and more things to help people understand how to build a site with Gatsby because a lot of those skills are portable to other frameworks.

<span class="smashing-tv-host">Drew:</span> One of the big questions that is going to come up for anybody who’s thinking about building sort of client project sites using Gatsby, one of the big questions that’s going to come up is about managing content and putting stuff in front of a client. You mentioned already how Gatsby can connect to different content management systems. Is that the primary method that you would put in place to deal with that question? Or does Gatsby have anything in its ecosystem that would enable people to edit content in any way?

<span class="smashing-tv-speaker">Marcy:</span> Yeah, I would say having a CMS or something can make those team relationships work a lot better. I’ve been in those use cases where the dev teams like, "Just learn HTML." And you see this glaze over from the client of like, "No, I can't believe you just said that." So having a system where people can do their best work in whatever ways suits them best, is super, super important.

<span class="smashing-tv-speaker">Marcy:</span> Like you just can't handle marketer GitHub, and might work some of the time but not all the time. And so, having like a preview and build infrastructure makes that better, and that’s where the Gatsby cloud product space kind of enters into the fray. There are ways to do preview. Without the paid cloud side and Gatsby cloud does have a free tier for personal projects, so it’s not all paid.

<span class="smashing-tv-speaker">Marcy:</span> But we have this, like the open source and the product ecosystem kind of come together so that Gatsby can as a founding organization, make enough money to keep the open source framework, keep that healthy, and keep our community rolling along with that. So, that’s kind of where this open source commercial side comes together, and really enabling some of these workflows that teams need.

<span class="smashing-tv-speaker">Marcy:</span> Some things like getting fast previews, getting builds out the door fast and deployed. And so, there are solutions on the Gatsby cloud side specifically, and then wherever there is an open source way to make Gatsby work like with a preview server or something, we try to document that and make sure our community knows what’s what and how to serve those team needs.

<span class="smashing-tv-speaker">Marcy:</span> Yeah, I would say like, you need some way to preview your CMS changes because it’s like that instant gratification. You don't want to be waiting an hour for a build to see some content.

<span class="smashing-tv-host">Drew:</span> So that’s interesting. The Gatsby cloud service gives you that ability to use a headless CMS service, where you’re just working with the content, but you’ve got no visualization of what it would look like in your site enables you to get a preview of how that would work. Is that right?

<span class="smashing-tv-speaker">Marcy:</span> It is, yeah. And so, it’s part of the trade off of decoupling, your headless CMS, which may have had, like WordPress, you could just look up the front end, but we’re giving it a new front end, and potentially pulling in other sources and other things that WordPress doesn't know about. And so, decoupling it in that way makes sense. But you still, as a team member, you have to be able to do your work in the speed that you’re rapidly used to.

<span class="smashing-tv-speaker">Marcy:</span> And so, that is where Gatsby preview, Gatsby builds come in to give that front end back to teams so they can collaborate, they can make decisions, get something shipped. So that has sprung up in the last year, getting more features and improvements in all the time and that we’ve heard from some teams that are really starting to see speed increases.

<span class="smashing-tv-speaker">Marcy:</span> And as we figure out like, "Okay, if this build is going slow, why is that?" It’s usually because the site is really, really big. So we’ve been focused a lot on improvements for large sites, and really improving those team, collaborative workflows. It’s a big focus of the team right now.

<span class="smashing-tv-host">Drew:</span> So Gatsby cloud is, I guess at its heart is a hosting service. Is it a CDN for deploying your Gatsby sites with a load of Gatsby specific functionality and features around it?

<span class="smashing-tv-speaker">Marcy:</span> I would call it more of a continuous delivery product because it’s not an actual CDN. It integrates with CDNs like Fastly, Netlify. There’s a lot of different providers that you can hook up and some of them for free. You can do a lot for free, which is pretty awesome. I just did it the other day in our last Gatsby web creators session, we use Gatsby cloud and Netlify to build our site.

<span class="smashing-tv-speaker">Marcy:</span> And it enables you to make Gatsby sites faster specifically, because it does have those improvements. It only has to build one type of site. So, there’re some improvements that Gatsby cloud can make, that no other platform can make because they are trying to like support all of these different types of websites and they do them all very well.

<span class="smashing-tv-speaker">Marcy:</span> But for Gatsby, if that’s all you’re building, and there’s quite a few agencies, who are all in on Gatsby, and they want to make it as fast as they can. So, that’s where Gatsby cloud can make some performance improvements specifically for Gatsby, because it doesn't have to worry about any other platforms.

<span class="smashing-tv-host">Drew:</span> So, Gatsby cloud would do your build, and it would then just deploy it to something like Netlify or presumably a whole range of different places.

<span class="smashing-tv-speaker">Marcy:</span> Yep. Yep, it will. And so, it’s the piece of Netlify that it would be using then as it’s uploading these built packages. Built files. It’s not using their builds, so the builds are happening on Gatsby clouds infrastructure, and that’s where some a lot of speed increases can happen. And then there’s still that upload step to get it out to a CDN, whichever one you’ve chosen.

<span class="smashing-tv-speaker">Marcy:</span> But yeah, it seems like teams are really loving this ability to see. I mean, it’s functionality that you would have missed. And so, that’s a necessary thing to add back in, is to be able to do these collaborative previews and get sign offs and all of that.

<span class="smashing-tv-host">Drew:</span> So, Gatsby cloud is provided as a service from Gatsby the company, and there’s Gatsby the open source project as well. Is this a similar sort of relationship to like WordPress and automatic have, where you’ve got a commercial entity developing an open source product?

<span class="smashing-tv-speaker">Marcy:</span> I would say so yeah, like Drupal. There’s precedent in tech to have these founding organizations where it’s kind of a virtuous cycle. And we’re working on publishing some governance documentation right now to make sure that, that’s super clear to our community, how we make decisions. But the entire goal is to keep Gatsby sustainable, so that it can continue to be an open source project that people can use it with ever even getting into Gatsby cloud.

<span class="smashing-tv-speaker">Marcy:</span> You could use other solutions with it if you want. And so, we need like enough business to sustain, like the people working on it. And so, I’m kind of in between, like I float in between the open source and commercial side and trying to make sure that we’re prioritizing things. I mean, as you could imagine, we’re juggling a lot of things with how broad the spaces like, we all have our niche use cases that we like, feel really strongly about, we need to do for our jobs.

<span class="smashing-tv-speaker">Marcy:</span> That adds up to be a lot of niche use cases. So, we try to juggle and prioritize and really listen to our community about what hurts right now, what’s painful, what’s going well. And so, that’s been an interesting journey to get for me personally to get back into devREL and really be listening to the community about, how can we make us be even better?

<span class="smashing-tv-host">Drew:</span> And is there a big community around Gatsby lots and lots of people using it?

<span class="smashing-tv-speaker">Marcy:</span> There are a lot of people using it, a lot of contributors. So for a lot of folks, it might be their first time contributing to open source like coming over to our docks and joining us for Hacktoberfest and things like that. And so, it has been really neat to see what a big community Gatsby does have, especially with things like accessibility and trying to make sure that frameworks do all they can out of the box for free.

<span class="smashing-tv-speaker">Marcy:</span> And so, there’s this, I don't know, subset or intersection of accessibility and Gatsby and that’s my happy place. But the broader community, a lot of people learn React or learn web development through Gatsby. And so, that’s really neat to see a progression through our community, and hopefully we get people to come contribute, even if it’s an issue or something of like, "Hey, this link was broken or this part of the docks was confusing to me or it’s outdated."

<span class="smashing-tv-speaker">Marcy:</span> Like even just telling a framework or a project that you use, that something could be better is a great way to contribute, because you can help us gain insight into the things that could use improvement. So that’s a great way to contribute.

<span class="smashing-tv-host">Drew:</span> You mentioned accessibility and of course, people will know you as being an accessibility expert. And they might be surprised to see you working with sort of fully featured front end framework like React, thinking that perhaps the two don't really go together. Is that always the case at JavaScript heavy front ends are worth less accessible?

<span class="smashing-tv-speaker">Marcy:</span> Well, I wish it weren't the case. But I think the data has shown that a lot of websites that do use front end frameworks are less accessible than those that don't. A project that comes to mind is the Web a Million. And actually, I have a blog post, I’m refreshing the Gatsby site to see if my blog post has launched yet. But webbing through the web a million this project, they used their automated wave tool to crawl the top 1 million home pages and evaluate them for some accessibility violations.

<span class="smashing-tv-speaker">Marcy:</span> And it was really depressing results. Like they’ve run it twice now I think, and I think it got worse. So, it’s not great, but I don't think you can really point to any one framework because there’s plenty of sites that don't use frameworks that have lots of accessibility problems. So, it’s kind of a broader industry issue, a really society.

<span class="smashing-tv-speaker">Marcy:</span> And so, for me working on a full featured web framework, I saw as an opportunity to try and get more accessibility awareness in the mainstream. And so, that was an intentional move on my part to go and try to make an impact on a lot of sites like working on one site is cool. You can solve some really interesting problems. For me, I wanted to advocate accessibility much more broadly and try to make frameworks the best they can be from the inside.

<span class="smashing-tv-speaker">Marcy:</span> So even if something is rough right now, trying to play that long game of like, "Okay, what web standards things can we talk about? What framework improvements can we make so that if this is kind of rough, like not just give up on it." So, even if I know it's... I don't know, JavaScript is some folks enemy I feel like I like it. You need some JavaScript to make accessible user interfaces, you just do.

<span class="smashing-tv-speaker">Marcy:</span> So, I am trying to like straddle those viewpoints and do the right thing while listening to my activist colleagues and friends kind of out there like pushing us forward as an industry. And then on the inside, I can be the messenger and the person that could try and reconcile some of those huge trade offs and ethical questions about What are we building?

<span class="smashing-tv-speaker">Marcy:</span> So, it’s challenging, but I really like it, because I have an impact to make on the web. And so, web framework. Lots of people are building Gatsby sites. So, seems like a good place to try and make an impact.

<span class="smashing-tv-host">Drew:</span> You mentioned briefly that Gatsby uses React at the moment. Is there a possible future where Gatsby might work with other frameworks, might receive a view version of Gatsby?

<span class="smashing-tv-speaker">Marcy:</span> I would love that. I’ve certainly talked about it. There is a pre React plug in, as I mentioned earlier. So you can swap that out. I think a big part of what we are talking about is sustainability of projects, trying to make the right call, these aren't easy choices to make. It’s not just like rip it out and start over. There’s a lot of concerns that go along with that. It goes deep.

<span class="smashing-tv-speaker">Marcy:</span> So, it’s something we’re actively talking about. And I don't really have anything specific to share right now. But we do have some internal meetings coming up soon to talk about that sort of thing. So, it’s being discussed, and I would love to have a view flavor, that’d be amazing. But as you can imagine there’s some interesting challenges that come along with that, and we want to make sure it’s the right move so that we’re not like, I don't know, going down a path and having it not work for whatever reason, then we’re maintaining two frameworks, like how do we make that actually realistic in terms of what we can maintain and make succeed for an open source community?

<span class="smashing-tv-host">Drew:</span> So I’ve been learning all about Gatsby. What have you been learning about lately Marcy?

<span class="smashing-tv-speaker">Marcy:</span> Well, I wish it was better but work life balance. I’ve been learning about, for me, unfortunately, I’m in like a burnout cycle. And so, I feel like I’m continually learning the lesson of how to be productive, especially this year in 2020. There’s just like one thing after another. So, trying to get really clear focus on where I want to go in my career, what makes me happy?

<span class="smashing-tv-speaker">Marcy:</span> How can I sustain, and we’re talking about sustainability. Like how can I sustain my own life after a career of really pushing hard on accessibility in particular like, "Okay, how can I kind of take a little step back and make sure that what I am putting out there, what I am doing is meaningful, worth the energy." See, a lot of my lessons have been kind of that intersection of work and life and trying to make the most of the time that’s been... I don't know about you, but it’s been pretty stressful for a lot of people including me.

<span class="smashing-tv-host">Drew:</span> It’s been very, very stressful. We are at very difficult times, isn't it?

<span class="smashing-tv-speaker">Marcy:</span> Yeah, yeah. I mean, we have so much to be thankful for in this industry, having opportunities and skills that you can apply. Seeing a lot of layoffs in our industry, really trying to make decisions that reflect where we’re at and not just going through the motions. So that was a big motivator for Gatsby web creators was, "Wow, there’s a lot of school age kids not in school this year, it would be really cool to see an outcome of turning some kids' eyes onto web development."

<span class="smashing-tv-speaker">Marcy:</span> Like when I was in seventh grade, and someone came to a class of mine to talk about photojournalism. I was like, "I want to be a photojournalist." So that actually did work. I got some feedback from someone that said, "My seventh grader’s learning from you, and now they’re really excited about code." So, that was a really good thing to spend some energy on, in a time where like, that wasn't something I would have necessarily thought of before being in these circumstances in 2020.

<span class="smashing-tv-speaker">Marcy:</span> So, really trying to be like nimble and make choices that kind of reflect where I want to go and what’s happening.

<span class="smashing-tv-host">Drew:</span> If you the listener would like to hear more from Marcy, you can find her on Twitter where she’s @marcysutton and find all her latest goings on, on her personal website, marcysutton.com. And of course you can find out how to get started with Gatsby from Gatsbyjs.org. Thanks for joining us today Marcy, do you have any parting words?

<span class="smashing-tv-speaker">Marcy:</span> Make the most of it wherever that might be.

{{< signature "il" >}}
