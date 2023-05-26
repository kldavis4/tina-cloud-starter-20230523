---
title: 'Smashing Podcast Episode 43 With Matthew Phillips: What Is Astro?'
slug: smashing-podcast-episode-43
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/475de692-46fc-4058-af10-3736770698d5/smashing-podcast-episode-43.jpg
date: 2021-11-04T18:00:00.000Z
summary: >-
  In this episode, we’re talking about Astro. Will this modern static site builder launch you into the stratosphere? Drew McLellan talks to developer Matthew Phillips to find out.
description: >-
  In this episode, we’re talking about Astro. Will this modern static site builder launch you into the stratosphere? Drew McLellan talks to developer Matthew Phillips to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re talking about Astro. Will this modern static site builder launch you into the stratosphere? Drew McLellan talks to developer Matthew Phillips to find out.

<iframe src="https://share.transistor.fm/e/7feb492c/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

### Show Notes

- [Astro](https://astro.build)
- Matthew’s [personal site](https://matthewphillips.info)
- Matthew [on Twitter](https://twitter.com/matthewcp)

#### Weekly Update

- [Optimizing Next.js Applications With Nx](https://www.smashingmagazine.com/2021/10/optimizing-nextjs-applications-nx/) written by Melvin Kosisochukwu
- [Eye-Tracking In Mobile UX Research](https://www.smashingmagazine.com/2021/10/eye-tracking-mobile-ux-research/) written by Mariana Macedo
- [How To Build An Amazon Product Scraper With Node.js](https://www.smashingmagazine.com/2021/10/building-amazon-product-scraper-nodejs/) written by Robert Sfichi
- [50 Resources And Tools To Turbocharge Your Copywriting Skills](https://www.smashingmagazine.com/2021/10/resources-tools-turbocharge-copywriting-skills/) written by Freya Giles
- [Creating A Magento PWA: Customizing Themes vs. Coding From Scratch](https://www.smashingmagazine.com/2021/11/magento-pwa-customizing-themes-coding/) written by Alex Husar

### Transcript

<p><a href="https://twitter.com/matthewcp"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f19a730b-169d-44cb-9214-4b4019c2b5f2/matthew-phillips-250x250.jpeg" width="200" height="200" alt="Photo of Matthew Phillips" /></a><span class="smashing-tv-host">Drew McLellan:</span> He’s an engineer at Skypack and a major contributor to a new project called Astro, which aims to combine performance best practices with the developer experience improvements we see from component based approaches. So we know he knows all about Astro, but did you know he can fit 18 whole lemons in his mouth? My smashing friends, please welcome Matthew Phillips. Hi, Matthew, how are you?

<span class="smashing-tv-speaker">Matthew Phillips:</span> I’m smashing.

<span class="smashing-tv-host">Drew:</span> That’s good to hear. I wanted to talk to you today about Astro, but before we do, why don’t you tell us a little bit about your background and how you’ve got to where you are today?

<span class="smashing-tv-speaker">Matthew:</span> Yeah, well, I’ve been working on front-end web development for a long time, probably six or seven years. The previous company, I was one of the maintainers of canjs, front end framework. Worked on that full-time open source for about three years I think. Also did quite a bit of consulting, different large and small companies on front end. And so I have a lot of experience in the front end. I had a big interest in web components and wrote various libraries surrounding web components. One’s called Haunted, may have heard of that, some people might have,

<span class="smashing-tv-speaker">Matthew:</span> and Fred, who’s the owner of Skypack, who started Skypack and worked on the Snowpack project, I knew him because he worked for Google on the Polymer project, which is a web component project. So I knew him just through the industry and I was thinking about changing jobs, looking to reset a little bit and they were hiring. So I jumped aboard, very interested. And have also a big background in ES modules and just module loading in general and that’s what they were working on at the time. So it was just good fit and so I decided to join aboard.

<span class="smashing-tv-host">Drew:</span> So you’ve really got your teeth into the back of the back end side of things, is that a fair assessment?

<span class="smashing-tv-speaker">Matthew:</span> I think so. I’m not super up to data on all the terminology, but I think that’s right.

<span class="smashing-tv-host">Drew:</span> That sounds about right to me. So I’m hearing a lot of buzz about Astro and that it’s some sort of static site generator, but I think that that term possibly under sells what it’s doing. What exactly is Astro and what is the problem that it’s solving for us?

<span class="smashing-tv-speaker">Matthew:</span> Right. Yeah. I mean, Astro is a static site generator. It’s kind of hard to explain how Astro came about, but I don’t know if that’d be helpful to go there, but what Astro is in general is, it’s a stack site generator that allows you to use components in any framework that you’re familiar with, whether it be View or React, Svelte, anything really you can bring your own framework and have that workflow that a lot of people enjoy while still generating purely static HTML and CSS.

<span class="smashing-tv-host">Drew:</span> So instead of using something like Handlebars or one of those traditionally server side templating languages, you can use your own reactive framework, essentially React or View or Svelte or whatever to act as the templating system for your static site generator. Is that-

<span class="smashing-tv-speaker">Matthew:</span> Yeah, it’s kind of, if you’ve heard of 11ty, but it’s kind of a halfway between something like 11ty or a more traditional static site generator where you’re using some templating language that is built for basically string concatenation in something front end, more front end driven static site generator like Gatsby, for example, it’s kind of a halfway between there. We wanted the developer experience, component usage, component usage is very useful. It’s very useful to be able to compose things in small chunks and there’s not a great way to do that in the more traditional templating engines that exist.

<span class="smashing-tv-speaker">Matthew:</span> So people, I think, gravitate towards these component based frameworks just because they’re so composable and the appeal to it doesn’t necessarily, it’s not necessarily, "Hey, I want this thing to be interactive in the client always." It’s just, "I want to compose things in small parts." And so yeah, we’re kind of a halfway between that, but we still want to generate this ideal static content. And I think there’s a lot of people who, like I said, they gravitate towards the framework way of doing things, but they’re not super happy with what it actually produces because, I’m writing a blog or I’m writing a marketing page or something like that, I don’t need all this Java script, but I’m kind of used to it and it builds well.

<span class="smashing-tv-speaker">Matthew:</span> So, I guess that’s kind of the problem you’re trying to solve is, we love, as people with... We have a lot of people in our community and on the team with a background in, I guess you would say the front of the front end, and they really want this plain HTML and CSS output, so it’s a way to balance those two desires, I guess.

<span class="smashing-tv-host">Drew:</span> So I guess it would be great for teams who are maybe building some sort of product in React or View or what have you, and then it comes to their marketing site and their document and their blog and all those things that actually they want to be really well SEO optimized and really faster load and really low overhead and would be ideal as static HTML and CSS pages, but they could still use their normal workflows and all the tools they’re used to to develop those.

<span class="smashing-tv-speaker">Matthew:</span> Yeah. Those workflows, those are super important. I think a lot of people can be a little critical from the outside. Like, "Oh, why did you build this thing this way? Why did you use React or whatever to build this landing page?" But these are teams and they’re spending a lot of time building websites or building internal tools or whatever it is they’re building and it takes a lot of effort to like, "Oh, we’re going to switch to a totally different context and use Jekyll or something else," and you got to get people up to speed.

<span class="smashing-tv-speaker">Matthew:</span> So I think those workflows are really, really important. And I read articles all the time where this team’s like, "Oh yeah, we use React. So we built our marketing site in React too." And if we can allow people to still use those normal workflows, but produce better output for what you’re actually trying to build, then I think that’s a huge win.

<span class="smashing-tv-host">Drew:</span> There’s a massive difference, isn’t there, between somebody just working solo on interesting projects that take their fancy and they might say, "Oh, okay, the ideal technical solution for this particular thing is this. And the ideal solution for this other thing is that," and there’s no real cost for them switching around. But when you’re talking about a team, if you take on the ideal solution for something that isn’t part of your normal tool kit, then you are almost bringing in technical debt into the team because somebody needs to keep their skills up to date with that other thing in order to keep it moving forward. So yeah. That’s really interesting.

<span class="smashing-tv-host">Drew:</span> Of course, one of the big things people worry about with these JavaScript heavy frameworks, React and all the others, is the weight of the JavaScript. So, I mean I guess performance is a big factor when it comes to the performance is a big reason that somebody might choose to use Astro. Is that right?

<span class="smashing-tv-speaker">Matthew:</span> Oh yeah, absolutely. So Astro does not add any JavaScripts by default. You can add your own script tags obviously and you can do anything you can do in HTML, but by default, thought of the other kind of component based frameworks, we don’t actually add any JavaScript for you unless you specifically tell us to. And I think that’s one thing that we really got right early. And it was kind of an accident actually, is that we were just building this thing and we just didn’t put in the part to make the JavaScript get loaded. We just didn’t write that part. We just wrote the part that generated the HTML and we’re like, "Oh, we actually like this better."

<span class="smashing-tv-speaker">Matthew:</span> So anyway, so what we wind up doing is we use a technique called partial hydration. I don’t know if you’re familiar with that, but essentially it’s a way to, you have a component and we only want to hydrate the part that actually is needed in the client. So if you’re familiar with more of a traditional SPA, single page app approach, usually have one component, which is your app component and it’s just nested a thousand components inside of it. Right? And some of those components are actually interactive, right? There could be a dropdown or there could be some type of form with validation, whatever it may be. Those are the parts that actually need to run in the client, but just the way the SPA architecture works, you got to run all the code for the entire thing for it to work at all.

<span class="smashing-tv-speaker">Matthew:</span> So partial hydration is, generally speaking, it’s a way to figure out what are the parts that actually matter, the parts that actually need to run in the client, and just only seeing that JavaScript. So one of the members of our team, Nate Moore, worked on this project called Microsite, which it was a Preact server rendering project, Preact. And what it would do is you would tell it, "Okay, this component needs to actually run in the client," and it would add the JavaScript for that. So he had worked on this partial hydration idea before and we just adopted that. He joined our team and we adopted that approach.

<span class="smashing-tv-speaker">Matthew:</span> So one thing that Astro does that’s unique is you tell it how you want it to hydrate in the client, and what I mean by that is there are different ways you can hydrate. Astro always loads JavaScript lazily, meaning that we don’t add a script tag for your component in the head or something like that. We don’t do that. Instead we have an in-line script that loads the JavaScript. And so you can load, I think there’s four different ways now, you can load on page load. So that’s the load event that exists in browsers, you can load on idle. So there’s a browser API called requestIdleCallback, and what that will do is it will let you know basically when the CPU is idle, when the browser’s not busy doing work, so you can load that way. And you can load on visibility, which means that, for example, maybe you have a component that’s far down in the page, you wait until the user scrolls that component into view, and then we load the JavaScript.

<span class="smashing-tv-speaker">Matthew:</span> And then lastly, there’s one called media and that’s based on media queries. So the use case for that is that, let’s say, you have some component that only runs on mobile, for example, and I’m sure you’ve seen the sidebars that you can click into view. Those types of things, usually a lot of times, don’t exist on desktop so you can set a media query and it will only load that component when it matches that media query.

<span class="smashing-tv-speaker">Matthew:</span> So anyways, those are the four ways to hydrate. So I think one thing that we did well is that we force you to choose which one of those things to do. So it makes the developer stop and think about, what it is the best way to load this code? Do I really need this code? Does this component need to run right away? Oh no, this thing only exists down the page. Let’s make this be visible.

<span class="smashing-tv-host">Drew:</span> So yes, I guess there’s all sorts of trade offs between each type. I guess if something’s only going to load when the browser is idle, then you don’t have control over if that’s going to happen in time for whatever sort of interaction that you want.

<span class="smashing-tv-speaker">Matthew:</span> Yeah. You would do that for maybe lower priority things, I guess. I mean it’s usually pretty safe, especially in Astro sites. Idle happens much quicker. You think about something that’s built as a SPA where there’s a lot of stuff going on, it’s rendering stuff and doing all this and maybe idle takes a little bit longer, but yeah, there’s definitely trade offs to all these. But I think the key thing is that we didn’t do anything magical really. I mean, it’s not like we figured out some crazy way to get performance. We just make you think about, what is the performance characteristics of what I’m building? And how should it load? And do I really need this thing to be in the browser at all? Or is this just happening one time when you’re building the site?

<span class="smashing-tv-host">Drew:</span> Yeah. I guess a lot of developers forget that the fastest site is one with no JavaScript on it. And so if you could just reduce the amount of JavaScript that is loading and passing, then it’s going to be quicker by default. So Astro renders all your JavaScript out to static HTML and CSS, and you can bring your own framework is something that it’s sort of described as, be that React or View or what have you. Does that mean Astro needs to have support for all of these frameworks? Or is it built in such a way that actually it really doesn’t matter what the JavaScript is that it’s dealing with?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. There are little, we call plugins for these frameworks. So we’ve written a bunch of them already. If you just MPM install Astro, I think you get React, View, Svelte, Preact. I think it’s just those four. And I know we also have written our own plugins for Solid.JS, which is a newer framework, and Lit, LitElement, We have one for that as well. So they’re actually pretty easy to write. Every framework has a different way to render to HTML. So that’s what these plugins do is that you give them a component, or Astro gives them a component, and then they just render that thing to HTML.

<span class="smashing-tv-host">Drew:</span> I was going to ask, yes, because all the frameworks have their own mechanism, don’t they for rendering out? So these plugins essentially enable Astro to hook into those rendering methods and-

<span class="smashing-tv-speaker">Matthew:</span> Yeah, exactly. That’s all they do, is that... Yeah. Yeah.

<span class="smashing-tv-host">Drew:</span> That’s excellent. So I’m presuming that Astro isn’t going to be able to take an existing, say React single page application and turn it into a static site. I’m guessing you actually need to build your site in a particular way with Astro in mind in the first place. Is that right?

<span class="smashing-tv-speaker">Matthew:</span> Kind of. I mean definitely it’s better to start from a position where you are thinking about it as a static site, but you certainly can take a React, like I said, one, you have your app component, you can put that in Astro and you can say client load, which that says to load this thing in the client, and then you get your SPA. So you can actually build a SPA on top of Astro and then maybe pluck things out over time, you’re like, "Oh wait, this header doesn’t need to be run on the client, let me grab that out of my SPA and put it in the Astro file." Do it that way.

<span class="smashing-tv-host">Drew:</span> So I’ve seen the documentation refer to the approach of islands rather than one big land mass. So can you explain that to us? What does that mean?

<span class="smashing-tv-speaker">Matthew:</span> Yeah, it gets back to what I was talking about before with the partial hydration is that, instead of having, like I said, one big SPA that is your entire application and everything derives from that, instead you have these small what we call islands of interactivity. I think Jason Miller of Google came up with this terminology. So you might have your top navigation bar and that’s an island, and then you might have a tabs island with some content, and you have those sorts of things. So they’re like mini apps within your page.

<span class="smashing-tv-host">Drew:</span> Okay. So you might have essentially a component which renders your main navigation and then a second component next to it, which is showing your number of items in your cart, for example, and you could pick different approaches to when those are hydrated. So the navigation would probably be just rendered out to HTML and not really interactive, it’s just links. And the cart component would actually be more interactive, would be running on the client and updating as you add things to your cart, or whatever the scenario would be.

<span class="smashing-tv-speaker">Matthew:</span> Yeah, exactly. And like you said, it’s a good point is that you can choose different ways to hydrate each of those. Some of those you maybe don’t need to hydrate at all, some of them you need to hydrate immediately, some of them you might need to hydrate in visibility because you have these different islands, you can think about them individually and what’s the best way to actually load them. Something like a cart, you probably want to do pretty early, because you want the user to see that cart number show up pretty quickly.

<span class="smashing-tv-host">Drew:</span> So when a component loads, one that we want to be fully hydrated, when that hydration process occurs in the browser, what’s going on under the hood there? Is the whole initial JavaScript that would’ve loaded when the page loaded in the traditional architecture, is that whole bundle then downloaded and instantiated at that point? Or is there something more clever going on?

<span class="smashing-tv-speaker">Matthew:</span> No, that’s exactly how it works. Like I said, we didn’t really do anything magical, it’s just very pretty straightforward. You say that you want something to load on idle, we load it on idle. What we do is we inject our own little script in specifically for that component, and, for example, for idle there’s a API called requestIdleCallback, window.requestIdleCallback, when that gets called by the browser, we import your JavaScript and that’s basically it. And then we render it. Each framework has a different way to render components on the client and so we have that code that actually does the rendering. And then from there, you’re inside of the framework component. Anything that you do, if it’s a View component, anything you do with View, it all just happens inside of there.

<span class="smashing-tv-host">Drew:</span> And so you’re still leaning on the traditional tools like Webpack and what have you to do your bundling for that to make sure that you’re only loading one instance of React and all those sorts of things?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. We use Snowpack. Our team were the creators of Snowpack. Fred created initially, but that’s a more modern tool than something like Webpack, and what that does is that gives you basically a dev server that compiles things on demand. So instead of getting one giant bundle of your entire "app", each file gets compiled individually in Dev, and then when you deploy that production, of course it all gets bundled in an optimized sort of way. Yeah.

<span class="smashing-tv-host">Drew:</span> One of the nice things about static site generators is that they’re generally very simple. You’re taking some markdown files or whatever it is and rendering them out to HTML, and there’s not really too much to go wrong there. Is there more inherent risk with the complexity of what Astro is doing that you could make a change to your code, create a new component or whatever, and suddenly find that Astro won’t build because there’s an incompatibility? Is that a risk?

<span class="smashing-tv-speaker">Matthew:</span> That’s a really good question. I mean, yeah. I guess anytime you add another layer of obstruction, there’s a possibility of incompatibilities. The biggest thing is that you’re working with a framework and you got to make sure your framework version matches the plugin, the React plugin or whatever it is that you’re using, but we keep all those things up to date. So I haven’t seen a lot of issues around incompatibilities, and what’s great about Astro in particular, one of the things I love about it is our community is very passionate and we have people, because we chose this big tent, bring your own framework approach, we have people in our Discord who are Svelte specialists. They’re very good at that. They’re very good at View. And if you have any questions, something that you don’t know how to do, you can go there and ask the question and there’s probably someone that can help you.

<span class="smashing-tv-speaker">Matthew:</span> So I know that there in the past, there’s been issues where certain features of View didn’t work right, and that’s because our plugin didn’t implement something correctly, and we have people that fix that stuff very quickly.

<span class="smashing-tv-host">Drew:</span> So there’s quite an active community. You say it was around a Discord server?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. Yeah. We have a Discord and a lot of people on there, people that contribute to documentation, people that help with support questions, and very vibrant community. Yeah.

<span class="smashing-tv-host">Drew:</span> Well, what’s the maturity of Astro like I mean, how long has it been going and are people using it in production?

<span class="smashing-tv-speaker">Matthew:</span> Yeah, there’s definitely a lot of people using it in production. The idea of Astro, as we’ve been talking about is a way to make building multiple page apps, bringing that architecture back, taking the new modern way people build things with components and component frameworks, but getting rid of the SPA part of it, which I think causes a lot of problems in sites that don’t need to be SPAs.

<span class="smashing-tv-speaker">Matthew:</span> So we trying to marry the new way of building things with what we think is a better architecture for a lot of websites. So our first approach to that was to build a static site generator, but the technology behind Astro doesn’t necessarily have to just generate static sites, we just thought that was the best way to go. And in doing that, we targeted a certain kind of website. We targeted people who are building blogs or people who are building marketing pages, these sorts of things, maybe even getting into e-commerce a little bit.

<span class="smashing-tv-speaker">Matthew:</span> So we’ve really been focused on getting that story right, so a lot of the people who have built stuff in the production, there’s tons of people who have built blogs and deployed those. And we’ve gotten some marketing sites and stuff like that as well. So I think that area is definitely maturing. Probably the next thing we’ll go after, and it might be a little while, but eventually we’ll get into e-commerce. More things actually need to be dynamically rendered on the server. You can’t currently do that with Astro, but we’re definitely going to get there.

<span class="smashing-tv-speaker">Matthew:</span> We’re currently gearing up towards our 1.0 release. We have a few things left to iron out. The initial implementation of Astro was hacky in some regards, and there are things that were not great about it. So some people in the team have been rebuilding our Astro compiler and we’re gearing up towards 1.0. I can’t give a definite date, but by the end of the year, we’re hoping to get that out. So that would be the point where we consider it, obviously 1.0 is a big milestone and we consider it ready for everybody, people who are very cautious about adopting new tools would be able to definitely get into it by then.

<span class="smashing-tv-host">Drew:</span> And how many people are working on the core of Astro? I mean, obviously there’s the community around it, but I imagine there’s a more core team of people working on it.

<span class="smashing-tv-speaker">Matthew:</span> Yeah. At Skypack, we have four people. Well, yeah, four people working on it.

<span class="smashing-tv-host">Drew:</span> So is Skypack the main sponsor of it as a project?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. So Skypack was, or is, a CDN for loading JavaScript. What you can do is you can load any packages that get published MPM, you can load them directly in the browser using Skypack. And when we started working on Astro, what we were really trying to do, we were trying to figure out a way to help people who were using Skypack to find a way, people wanted to host their content, host their own JavaScript on Skypack, And we’re looking for ways to do that. And we kind of fell into Astro out from that. We were like, "Well, we really need to know about how the person builds their website to better optimize the loading of everything."

<span class="smashing-tv-speaker">Matthew:</span> So we’re like, "Well maybe we could build a little thing to where you can put your components together and we know about these components, so we know exactly what JavaScript you need." And we’re working on optimizations as what Astro grew out of, but then Astro has taken off to a bigger extent than I think we really even anticipated. So, we’re kind of seeing that Astro is maybe the future of the company, so we’re building the business around Astro now. Still TBD on what that means exactly, but that’s kind of the direction we’re going.

<span class="smashing-tv-host">Drew:</span> It sounds like the future is pretty bright for Astro. Are there features that you’ve still not got to or that you plan to add in the future or you’re hoping to add?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. So one big one that we had at the very, very beginning and then we took out for reasons that, more than I can get into, but components in markdown. This is something, if you’ve heard of MDX, people are very passionate about this. They want to be able to use components within their markdown files. MDX is not MDX file, but that’s something that we currently don’t have. It’s something that we know that people are definitely excited about and we’re actually working on it right now. So, that’s something we should have very soon. In Astro, you can already have a .md file as your page, that way you’re writing a blog post, you do it in a markdown file instead of in .astro file. But soon you’ll be able to use .MDC, which when you do that, you’ll be able to write mark down, but you’ll also be able to put components inside of that.

<span class="smashing-tv-host">Drew:</span> That sounds like it would be great for things like documentation sites, for example, where you might have loads of documentation in markdown format, because it’s primarily text, but then want to throw in something interactive to help explain a concept or-

<span class="smashing-tv-speaker">Matthew:</span> Examples.

<span class="smashing-tv-host">Drew:</span> Examples. Yeah. So things like blogs, things like marketing sites, possibly documentation, those sorts of things are all good to go and a great use for Astro right now?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. If you run npm init astro, it runs our generator and the generator has a bunch of different example starter templates essentially. We have one for blog. We have one for blog with multiple authors. So if you have multiple people working on a blog together. We have a portfolio. Astro is very good for portfolio websites. And then we do have one for docs as well. So all of those things that we’ve been talking about, there’s already starter templates for all of those.

<span class="smashing-tv-host">Drew:</span> Where’s the best place right now for somebody to learn more about Astro if they want to get started with it?

<span class="smashing-tv-speaker">Matthew:</span> I think docs.astro.build is probably the best place. Or if you just go to astro.build, there’s also a link to it. But that gives you our getting started documents, documentation. I think we have translations in a dozen languages already. And yeah, then I think there’s lots of links to jump on Discord and start asking questions.

<span class="smashing-tv-host">Drew:</span> And that Discord is the best place to go if somebody is a developer and wants to get involved, maybe, implementing a plugin for a different framework that you’ve not covered or maybe even contributing in a more heavyweight way?

<span class="smashing-tv-speaker">Matthew:</span> Oh yeah, we have a channel specifically for people who want to start contributing. That’s definitely a great place. If you’re more comfortable on GitHub, we have lots of people there as well.

<span class="smashing-tv-host">Drew:</span> Well, that’s fantastic. Is there anything else we should know about Astro?

<span class="smashing-tv-speaker">Matthew:</span> It’s the best and everyone should start using it.

<span class="smashing-tv-host">Drew:</span> Tell us briefly a bit more about Snowpack, because that sounds really interesting. From the perspective of people who might be familiar with some of these older tools like Webpack, what are the key differences with how Snowpack approaches the job?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. I mean, Snowpack comes from more of the perspective, and Vite is another tool that’s very similar to Snowpack. They both do a very similar thing. Where they approach it from, you really wanted to approach it from your loading modules in the browser, the browser has a native way to load modules now, you can do a script type equals module and it can load any module that has import and export statements. However, what most people write in their modules is they import from different packages on MPM and the browser doesn’t have any way to load stuff off of MPM. It doesn’t know about that kind of thing. So what Snowpack does essentially is it does, it does know about, if you import React, it’s going to turn that React import into a URL that the browser can understand. So it’s all it does, is it translate the JavaScript or type script or whatever, the JSX, whatever it is that you write, which is not compatible with the browser and makes it compatible. That’s essentially what they do.

<span class="smashing-tv-host">Drew:</span> Sorry. Is that where Skypack then comes in, because it’s loading that React module from Skypack?

<span class="smashing-tv-speaker">Matthew:</span> Yeah. Well, it can. Snowpack Doesn’t do that by default. It does a more traditional local environment. So you’re still going to do your MPM install and do all that sort of thing. There is a way to turn on a Skypack integration. That’s still something that we’re trying to figure out the best way. Like I said, we came at this from the approach of, we wanted to make Skypack better for users, and make it easier to use Skypack. And we fell into Astro because of that. So I think we’re going to probably, at some point, get back to integrating things more tightly, but that would be the ideal, right? I think is that when you, I don’t know, I’m just thinking off the top of my head here, but when you deploy your website, maybe we translate all those React URLs to instead come from Skypack, that way they’re well cached and all that sort of thing.

<span class="smashing-tv-host">Drew:</span> Yeah. So-

<span class="smashing-tv-speaker">Matthew:</span> TBD on that.

<span class="smashing-tv-host">Drew:</span> I’ve been learning all about Astro. What have you been learning about lately Matthew?

<span class="smashing-tv-speaker">Matthew:</span> Oh, well, I mean I’m always learning lots of stuff. I think lately, the Astro compiler, it was originally, it’s all JavaScript and they’ve been rewriting it in Go. So Go programming language. I’ve used Go before, but it’s been quite a while so I’ve been relearning that as I play around with the new compiler.

<span class="smashing-tv-host">Drew:</span> Yeah. There seems to be a trend in all sorts of parts of the ecosystem of JavaScript tools being replaced by Go versions just for the performance.

<span class="smashing-tv-speaker">Matthew:</span> Yeah. Yeah.

<span class="smashing-tv-host">Drew:</span> As our projects get bigger and bigger and our build times get longer and longer, everyone’s looking for the next way to speed it up.

<span class="smashing-tv-speaker">Matthew:</span> Yeah. That’s exactly, that was it. I mean, we knew that we needed to rewrite it anyways and we’re like, "Why not just go for the speed boost as well?"

<span class="smashing-tv-host">Drew:</span> Yeah. Yeah. If you, dear listener, would like to hear more from Matthew, you can find him on Twitter where he’s @matthewcp or his personal website, which is matthewphillips.info. You can find out how to get started with astro at astro.build. Thanks for joining us today. Matthew. Did you have any parting words?

<span class="smashing-tv-speaker">Matthew:</span> No. Go download Astro and yeah, join Discord and talk to us.

{{< signature "il" >}}
