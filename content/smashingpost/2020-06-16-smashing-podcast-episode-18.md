---
title: 'Smashing Podcast Episode 18 With Mina Markham: How Can I Learn React?'
slug: smashing-podcast-episode-18
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40d5e249-9475-4406-927b-c538707ff760/smashing-podcast-episode-18.png
date: 2020-06-16T05:00:00.000Z
summary: >-
  In this episode of the Smashing Podcast, we’re talking about learning React. What’s React like to work with, and how can experienced developers get started? Drew McLellan chats to Mina Markham to find out.
description: >-
  In this episode of the Smashing Podcast, we’re talking about learning React. What’s React like to work with, and how can experienced developers get started? Drew McLellan chats to Mina Markham to find out.
categories:
  - Smashing Podcast
  - React
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode of the Smashing Podcast, we’re talking about learning React. What’s React like to work with, and how can experienced developers get started? I spoke to Mina Markham to find out.

<iframe src="https://share.transistor.fm/e/e4efb82f/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [Mina Markham](https://twitter.com/minamarkham) on Twitter
- Mina’s [personal website](https://mina.codes)

### Weekly Update

- [From Static Sites To End User JAMstack Apps With FaunaDB](https://www.smashingmagazine.com/2020/06/static-sites-jamstack-apps-faunadb/) by Bryan Robinson
- [Is Your Website Stressing Out Visitors?](https://www.smashingmagazine.com/2020/06/website-stressing-out-visitors/) by Suzanna Scacca
- [Mirage JS Deep Dive: Understanding Timing, Response And Passthrough (Part 3)](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/) by Kelvin Omereshone
- [Building A Facial Recognition Web Application With React](https://www.smashingmagazine.com/2020/06/facial-recognition-web-application-react/) by Adeneye David Abiodun
- [Internationalization In Vue With The Vue I18n Plugin](https://www.smashingmagazine.com/2020/06/internationalization-vue-i18n/) by Timi Omoyeni

## Transcript

<p><a href="https://twitter.com/MinaMarkham"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cad0a9e-8f27-424b-b2df-a71dd12603ee/mina-markham-200x200.jpg" width="200" height="200" alt="Photo of Mina Markham" /></a><span class="smashing-tv-host">Drew McLellan:</span> She is a front-end architect, conference speaker and organizer, and lover of design systems. Her work on the Pantsuit patent library for Hillary Clinton’s Hillary for America presidential campaign marked a watershed for design systems within the industry and was featured on publications, such as Wired, Fast Company, and Communication Arts. Like many of us, she writes code for a living, currently as a senior engineer at Slack. So we know she’s a talented and forward thinking developer, but did you know she was once mistaken for Patrick Swayze? My smashing friends, please welcome Mina Markham. Hi Mina. How are you?</p>

<span class="smashing-tv-speaker">Mina Markham:</span> I’m smashing.

<span class="smashing-tv-host">Drew:</span> Good to hear. Now, sometimes on the Smashing Podcast, we talk to people about the subject that they’re best known for. And sometimes it’s fun just to talk about something a bit tangential. Now, I could chat to you all day about pattern libraries, design systems, the amazing work you’ve done in that particular area, and I could talk to you about subjects that you’ve perhaps spoken about, events, such as the Event Apart, things like art direction. And we could obviously talk about CSS until the cows come home. But you tweeted a few days ago, and I realized that we’re actually both in the same boat in that we’re both experienced front-end engineers and we’re both recently started working with React. So before we get onto React itself, where were you coming to up to this point? Had you been working with other libraries and frameworks for JavaScript development?

<span class="smashing-tv-speaker">Mina:</span> No, actually I’ve been doing mostly vanilla JavaScript for a while. And before that, of course I got into JavaScript. Let me rephrase that. I started working with Java script using jQuery because it made the most sense to me. It was something that was very easily for me to parse to figure out what was happening. And then from there I backtracked to doing just vanilla, plain JavaScript, ESX, and I hadn’t really gotten too much into the framework wars. I had no, like I had no favorite. I had no dog in the fight. I was like, "For you, React, whatever. I don’t really care." But times change.

<span class="smashing-tv-host">Drew:</span> And in this sort of way of working with vanilla JavaScript, because I’ve done a lot of that myself as well. I’ve worked with various frameworks. I’ve done a lot with jQuery back in the day. I worked with YUI, Yahoo User Interface Library. Had you felt many of the pain points that something like React’s architecture tries to address?

<span class="smashing-tv-speaker">Mina:</span> I don’t think I ever had. I spent most of my career making websites versus web apps and things like that. So everything I did was pretty static up to a certain extent. So I never really had to deal with state management, things like that. So the pain points that React attempts to solve I had never really applied to the kind of work that I did.

<span class="smashing-tv-host">Drew:</span> Generally speaking, what’s the sort of nature of the projects that you’ve with React so far?

<span class="smashing-tv-speaker">Mina:</span> It was actually only been the one project, which I’m currently working on and I can’t give away too many details because public company and all that good stuff.

<span class="smashing-tv-host">Drew:</span> Of course.

<span class="smashing-tv-speaker">Mina:</span> But essentially what I’m trying to do is I’m trying to use React to, it’s a very interactive sort of product where I need people to be able to enter in and save data at a certain state and then manipulate it and generate something else with said data. And that’s just something that it’s not simple DOM manipulation at that point. It really is a lot of more complex, front-end manage of data and managing the state of said data. So there really was no other alternative but to use some kind of library that attempts to solve that problem. I knew I wouldn’t be able to get past with just plain JavaScript. I contemplated maybe handling somethings on the server side, but again, due to the very interactive nature of what I’m working with, it need to be in the client. And so we already use React at Slack for various other things. And so I was like, "Okay, well we just should go ahead and adopt the same thing that the rest of the parent the companies are using and go from there."

<span class="smashing-tv-host">Drew:</span> One of the things that I’m always seems to be a pain point with people picking up React is getting to grips with the tool chain that’s needed to get things working, Webpack being an obvious elephant in the room. Have you had to do much configuration of the tool chain or like me if you had the luxury of teammates doing it for you?

<span class="smashing-tv-speaker">Mina:</span> Oh, I love the infrastructure team at Slack the data. The front-end infrastructure team at Slack, they handled all of that. I didn’t have to think about it. It was great. Because I tried to learn React before in the past. Usually the way I learn best is by actually working and implementing on things. And we use React to build a lot of hillaryclinton.com back in 2016. So it’s not like I’ve never worked with people who use it. It’s just my work never directly needed me to get involved. But that code base was very complex and very sophisticated, and there was so much happening that there’s such a barrier to entry to try to learn anything in there if you didn’t already know how React and Redux and all of that works, which I didn't. So I wasn’t really effective in learning in that environment.

<span class="smashing-tv-speaker">Mina:</span> Luckily, here I do have people to like take away a little bit more of the complex bits of it. I don’t have to worry about the Webpack config at all. That’s been set up. That’s been tried and tested and ready to go. I am in a similar boat where we also use Redux in addition to React, which I didn’t realize were two different things. I didn’t know which part handled which. Dropping into a code base like that, it was a little disorienting because I didn’t realize that they were all the same thing. I had people who were seasoned React developers telling me, "Oh, we also are using Redux, which makes it a little bit harder for you to really learn what React all can do if you’re starting from scratch." And I never quite knew what they meant by that because I didn’t know what they were talking about.

<span class="smashing-tv-speaker">Mina:</span> To answer your original question, I am still having a little bit more of a little bit barrier to entry, because it’s not just learning React. I’m having to learn React and also how to use the Redux store. So those two things at the same time can be a little much.

<span class="smashing-tv-host">Drew:</span> Yeah, I’ve found exactly the same thing coming into an existing code base as my first React project that uses Redux. And I think as is the nature of any of these sort of technologies when they’re young, they iterate really quickly, and what’s best practice at one point, 6 months later has moved on and there’s a different way of doing things. And when you have a code base that spans many years, you can sometimes have different styles of implementing things in there. It doesn’t always keep sync. And of course, if you’re following a tutorial or whatever to learn, you’re reading books, you’re using resources, they will be in the most modern version of how to do things. And that doesn’t necessarily nit to what you see when you look at an existing, mature product. Is that something you’d experienced at all, or have you managed to keep your code base really up to date?

<span class="smashing-tv-speaker">Mina:</span> I think that is something that I definitely have been experiencing. When I tried to learn how to do React on my own, I looked at various tutorials and things like that. And I noticed, or at least people have told me who have worked who have been working with me that some of the things that we do or kind of anti-pattern or not quite how things work now, because this code base is slightly, well mature us relative, but it’s a few years old. And so there are some ways that I guess are easier to do things than the way we’re doing them currently because this was written years ago. So it’s a little bit of a treadmill trying to keep up with current times and make sure I want to do things the best way, but also I don’t want to break an established code base because I want to play around with stuff.

<span class="smashing-tv-host">Drew:</span> Obviously, one of the things with React that people like you and I are coming to it, it can feel a bit jarring as this whole thing with JSX. Are you using JSX in your project?

<span class="smashing-tv-speaker">Mina:</span> We are. I am using JSX.

<span class="smashing-tv-host">Drew:</span> Have you made peace with that?

<span class="smashing-tv-speaker">Mina:</span> I fell like a little small piece of me dies every time I open one of those files. It still feels sacrilege to put my HTML in the JavaScript file. I know that’s kind of revolutionary and the whole point, but it just feels off to me that I’m writing my markup in a JavaScript file. I’ve made peace with it, but every time I do it, I’m just like, "..." Separation concerns, it is a thing. I’d like it back, please.

<span class="smashing-tv-host">Drew:</span> It’s a valid point, isn’t it? My background when I was starting to work more seriously with JavaScript, and this was probably when I was back at Yahoo, things were very much on the model of server rendered HTML pages and then taking a progressive enhancement approach, layering JavaScript on top to enhance the interface. And if the state of something in the interface needed to change, your code had to know about all the parts of the interface that it needed to update, which obviously leads you to a tightly coupled approach with these big monolithic views where the code you write needs to know about all the other code around it. And I guess that doesn’t really lend itself to a componentized approach which you would take when working with a pattern library or a design system, which is more to your area of particular expertise. I guess, React lends itself more to that approach, does it?

<span class="smashing-tv-speaker">Mina:</span> I think it does, especially with the being able to couple the very specific CSS to one JSX or one React component. And so that way it makes it much easier to separate or only take what you need for the library and leave the rest, whereas a pattern library or design system that attempts to do something more monolithic with just one big style CSS file or something like that, it does make it a lot difficult. You kind of have to take it all or nothing. So I do appreciate that React allows us to do more individualized, more componentized way of development, even if I still wish there was a way for me to do truly separate my presentation layer and my content layer from my interactivity layer. But maybe that’s just me being a little bit old school in that sense.

<span class="smashing-tv-host">Drew:</span> I definitely feel the pain there. The idea is that, come and correct me if I’m wrong, my understanding is that rather than separating the technologies, the CSS, and the JavaScript, and the HTML, it’s separating the functionality. So everything that is one component all exist together-

<span class="smashing-tv-speaker">Mina:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> ... which I guess is useful if that component then is no longer needed. You can just delete it, and it’s gone, and it doesn’t leave a footprint around your app. That’s not always the case with CSS though. How are you working with CSS with React? Have You looked at things like styled-components or anything like that?

<span class="smashing-tv-speaker">Mina:</span> No, we haven't. I’ve heard of styled-components, but I’ve never quite really investigated them very fully to be perfectly honest. So the way that we’re working with CSS with React is we write Less, and we just have a Less file attached to each individual component that gets imported into that component. And then it gets bonded up via Webpack and served to the client.

<span class="smashing-tv-host">Drew:</span> Are you using a system like BEM or something to turn namespace?

<span class="smashing-tv-speaker">Mina:</span> Yeah. We’re using BEM for namespacing, although the adherence to it is kind of varied depending on who’s writing what. But we try to use a BEM namespacing pattern to make it a little bit clearer what the purpose of each individual class and component is.

<span class="smashing-tv-host">Drew:</span> And does that seem to be working successfully for you?

<span class="smashing-tv-speaker">Mina:</span> I think so. Occasionally it kind of has the same old problem of I sometimes don’t know how to name something. After a while daily things has always and will always be a difficult thing for master. So that’s the only issue I have with is I occasionally I have no idea what I should call a particular component.

<span class="smashing-tv-host">Drew:</span> Definitely. That’s a constant battle, isn’t it, how to out the name things?

<span class="smashing-tv-speaker">Mina:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> I always end up when working on a new feature or something like that, you give a component and all the classes and everything the name that the feature has got at the moment. And then by the time you come to launch, it’s been renamed something else. So you have references to the old name in the code and the interface has the new name. And ...

<span class="smashing-tv-speaker">Mina:</span> I try to always name things based on the function or the purpose of it versus things that are a little bit more ephemeral, because it’s less likely that the actual purpose of this component will change. I forgot to mention, but in addition to using BEM, I guess we use BEMITs if you’re familiar with that. It’s basically the ITCSS plus BEM, both of which were created by Harry Roberts. So I use Hungarian notation to denote whether or not something is a component, versus a layout object, versus like a larger pattern comprised of multiple components. And then from there we use the BEM convention to signify like the block element and all that.

<span class="smashing-tv-host">Drew:</span> And have you had to do much refactoring and deleting of components and things in your code base and had to deal with the issue of CSS getting left behind?

<span class="smashing-tv-speaker">Mina:</span> Yeah. So the non-React part of my job, of maintaining slack.com is that’s all just a bunch of Less files that are being compiled for CSS. And I guarantee you, there’s a lot of zombie code in there, because we definitely iterate above things a lot in the time I’ve been there. And we don’t always have time to go back and do the cleanup versus when we redesign a page or something. So it’s overdue for an audit, I’ll say that.

<span class="smashing-tv-host">Drew:</span> This is something that we’ve just been looking at in our React project, looking at how we approach CSS. At the moment, we have a few big, global CSS files for the whole of the app, and we do get this situation where our bundle size is just growing, and growing, and growing and never gets any smaller, even though things do get removed. So we’ve been looking at things like styled-components, Tailwind as well is another option that we’re really seriously considering. Have you looked at tailwind much?

<span class="smashing-tv-speaker">Mina:</span> I haven’t looked at it a lot. I’ve been curious about it, but again, I’ve never really had time to dig in to actually see if it’s something that I want to try to bring into our code base.

<span class="smashing-tv-host">Drew:</span> I was actually quite surprised, because like you, I’m a bit old school with how to do these things. I like nice separation of concerns. And I like to write my CSS in CSS, and of course the approach with Tailwind is you have all these class names, which feel a bit like inline styles that you’re applying. And if it feels dirty.

<span class="smashing-tv-speaker">Mina:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> And I volunteered within the team, we each which took a technology to investigate if they’d be a good fit for our problems, and I volunteered to look at Tailwind because I was absolutely certain I was going to hate it.

<span class="smashing-tv-speaker">Mina:</span> No, no.

<span class="smashing-tv-host">Drew:</span> But it turns out I actually think it solves a lot of problems. I was quite impressed.

<span class="smashing-tv-speaker">Mina:</span> Yeah. I’ve sort of come around to a similar way of thinking, because I in the past would much prefer to have one class comprise all of the styles I needed for a particular component and not do a class per property, as I believe Tailwind does or languages like it do. For the similar reasons, it felt very much like, "Well, I’m just running inline CSS at this point. Why would I do this?" But as I’ve been developing more and more, inside of our Slack design system, I created a bunch of what I call utility classes that do things like add a bit of margin with a pattern. I’ve noticed that more and more, I’m using those classes in addition to the component classes. So I’m like, "Okay, well maybe I should revisit this whole to doing a CSS as a one declaration at a time." I don’t know if I’d go that far, but it’s definitely worth considering.

<span class="smashing-tv-host">Drew:</span> Computing seems to flip flop in terms of trends between thin clients and fat clients solutions. We started with mainframes with terminals, and then the PC era with windows and office and all these sort of big applications. And they were all getting really slow, and than the web came along, and that was just a browser, and all the work was being done on the server. And it was all fast and snappy again. And now we’ve gone back to putting all that work back in the browser with everything being done with JavaScript, things like React and the JAMstack approach where we’re back to a sort of fat client. I sometimes worry that we’re asking too much of the browser. Is this a mistake? Are we asking too much of the browser trying to do all this stuff in React?

<span class="smashing-tv-speaker">Mina:</span> I want to say yes with the caveat of, again, my experience is very much contained to mostly static websites. I don’t do a lot of product development. So maybe in that realm, this makes more sense. But from my perspective, I feel like we’re a lot of the times using a hatchet when we just need a butter knife. I don’t know why we need put all this in the browser, put so much work and so much pressure on the client. I feel like we could do this much simpler. One of the things that always made me a little hesitant to use React, or I say hesitant, but what I mean when it made me viscerally angry and I actively opposed, was when I would go to a website and literally nothing would render because there was one error or something, Like, "Really? The entire page is broken because one function broke down?"

<span class="smashing-tv-speaker">Mina:</span> It just kind of annoyed me that a lot of times it was an all or nothing approach. One of the talks that I gave at AEA in the past and other places in the past was talking about how to include progressive enhancement and not just your development, but also of art direction and design of sites. And I would point out specifically examples of websites that didn’t do progressive enhancement or any kind of graceful degradation. It was like either you have the JavaScript running in the browser or you get absolutely nothing. And it would be like just a simple site that represent information about the history of web design, which was one of the sites actually talked about, the history of web design from like 1990 until now. It was a beautiful website with lots of timelines, animation of things. But it also could have been rendered statically with just a list. There were steps in between showing nothing and showing that beautifully enhanced experience that I think got lost because of the way we’ve been approaching modern web development now.

<span class="smashing-tv-host">Drew:</span> So would you say there are absolutely some categories of projects that suit a solution like React and some where it really shouldn’t be used and you should be using more traditional methods?

<span class="smashing-tv-speaker">Mina:</span> I think that if your site particularly is mostly static, it was just serving up information, I guess I don’t understand why you need a project like React to render something that doesn’t have a lot of interaction beyond just DOM manipulation. I guess I don’t see what benefit you get from that. Again, I may not be working on the appropriate projects. I may not just have seen or found that use case, but I’m having a hard time seeing if it’s just mostly static site, presenting content, not a lot interaction, not a lot of interaction beyond manipulated DOM and doing animations. I don’t see how having a React library helps you accomplish that goal.

<span class="smashing-tv-host">Drew:</span> It’s interesting because I’m not bad talking it because I haven’t actually used it, but I see a lot of Gatsby projects and Gatsby being a static site generator that uses a React front-end in it. And I see all the examples of the themes and things they have available are all content based sites, or blogs, and a recipe site, and a portfolio, and these sort of things. And there’s something I think actually that this isn’t necessarily the right fit for something like React. Why isn’t this being statically rendered and then progressively enhance?

<span class="smashing-tv-speaker">Mina:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> It’s not software.

<span class="smashing-tv-speaker">Mina:</span> Yeah. I haven’t actually used Gatsby either. I’ve heard plenty of great things about it, but that’s probably one of the examples I would think of where I’m like, "Okay, I guess I’m just not seeing why that tool is necessary to do that particular job." Again, I don’t know. Maybe it’s just because more people are comfortable writing in React when they are writing new something else, and it’s just providing a tool that meets people where they are. I’ve heard great things about static site generators that use React for people who have used them and love them, but it’s not a use case that I would have immediately been like, "Oh, that makes sense."

<span class="smashing-tv-host">Drew:</span> It seems like there’s always been this battle between what we would call a website and what you might call a web app. And the chasm between the two seems to be getting wider, and wider, and wider, whereas a progressive enhancement approach tries to bridge the gap by taking something static and adding JavaScript and adding interactivity. It seems that things like React are ideally suited for software that you’re running in the browser. Would you agree with that?

<span class="smashing-tv-speaker">Mina:</span> I would definitely agree with that because it feels like it’s was built for that type of environment; it was built for running software. It was built by Facebook for Facebook. So it was built for a product. It was built for running whatever you call a web app in the browser and not necessarily for the type of work that, as I mentioned, I’m used to doing. So I think in those scenarios, it definitely makes a lot of sense to use it if you’re building a more complex, more sophisticated piece of software that’s meant to run inside of a browser. But if you’re building a marketing site or whatever, I guess I would still struggle to see why it will be necessary there.

<span class="smashing-tv-host">Drew:</span> So are we giving people permission to still build decent, statically rendered websites?

<span class="smashing-tv-speaker">Mina:</span> I would love to see more of that happen. I feel like that’s kind of gotten lost and it’s sort of lost its, if it ever was cool or whatever. I feel like we’ve lost that part of web development. It’s so funny: you and I both said that we’re kind of old school, and I laugh at that because I’ve actually been doing web development for, what, six years now? How am I old school? It hasn’t been that long for me. And yet somehow I’m part of the old guard who doesn’t like new and shiny things. I don’t get it.

<span class="smashing-tv-host">Drew:</span> So in fact React has actually existed for the whole time that you’ve been a web developer.

<span class="smashing-tv-speaker">Mina:</span> Maybe I just have an old soul. I don’t know.

<span class="smashing-tv-host">Drew:</span> I think that’s probably the case. I’ve not looked personally at, there are service side rendered approaches you can take with React apps. Have you experienced any of those?

<span class="smashing-tv-speaker">Mina:</span> I haven’t experienced any them. I briefly looked into them for the project I’m currently working on, because I feel like there’s parts of the operation that would work better on a server versus in the clients. But I think because of my limited knowledge and the fact that the code base is a little more complicated than I can understand, I wasn’t quite able to figure out how to make that part work. I would love to figure it out eventually, but I spent a day digging into it. I was like, "You know what? I’m not grokking this away I need to be. So I’m just going to back up and take a different route."

<span class="smashing-tv-host">Drew:</span> Yeah. I think we’ve all been there.

<span class="smashing-tv-speaker">Mina:</span> Yeah. I went down a path. I was like, "Oh, this is dark and scary. Let’s reverse. Let’s reverse."

<span class="smashing-tv-host">Drew:</span> Step away from the code.

<span class="smashing-tv-speaker">Mina:</span> Yes.

<span class="smashing-tv-host">Drew:</span> So you’ve been very diplomatic and polite about React so far. I sense that there’s some tension bubbling under the surface a bit. Come on. Tell us what you really feel.

<span class="smashing-tv-speaker">Mina:</span> I have been polite and diplomatic, mostly because the Reacts fan base can be a little mean sometimes, and I would rather not have them come for me. So please, React is great. It’s wonderful. Use it for what you want to use it for. I kid, but even that tweet that you mentioned at the beginning of this podcast where I think what you said is that I don’t hate it. I don’t love it, but I don’t hate it. Even that statement, I got people, there was no vitriol, but it was more they where ready to leap to the defense and say, "Well, I love it because X, Y, Z." I’m like, "I didn’t say it was bad. I just said that I’m meh about the whole thing." But apparently being meh is not okay. I have to love it.

<span class="smashing-tv-speaker">Mina:</span> So that’s why I probably have been a bit more diplomatic than I would ordinarily be, just because I don’t want people to think that I’m bad mouthing it, because I’m not. It has a place in more web development. It serves a function. It does its job well. People love it. It’s just not a tool that I’ve ever had or wanted to use until now.

<span class="smashing-tv-host">Drew:</span> Yeah. Things can get very tribal, can’t they, with people feeling like they have to take one side or another, and you’re either absolutely for something or absolutely against something? And I’m not sure it serves a good purpose, and I don’t think it really moves us forward as an industry and as a community to do that.

<span class="smashing-tv-speaker">Mina:</span> Yeah. It’s really odd. It’s fascinating to watch from just a sociological standpoint, but it’s often just really like weird to observe. It’s like I’m not allowed to just be, like I said, neutral about certain things. I have to have a strong opinion, which is I don’t think healthy. What’s the term, "Strong opinions, loosely held?" That’s kind of the way I go about things. I feel strongly about certain things, but it’s not like you can’t change my mind. Where I feel like some people, their identity gets wrapped up into certain aspects of it ,that if you are not for whatever they’ve chosen to identify with, it’s a personal slight versus just, I don’t care about this particular topic, or tool, or whatever.

<span class="smashing-tv-host">Drew:</span> Yes. I don’t know if it’s made worse by the fact that we all are sort of tending to specialize a lot more in particular parts of the stack. And I know there are people who are React developers. They would call themselves a React developer because that’s what they work in. And they wouldn’t necessarily write any vanilla Java script or wouldn’t use Vue or whatever. React is their world. So I guess it almost feels like an attack on their entire career to say, "I don’t like React." Well, they’re really invested in making you like React or whatever the technology may be.

<span class="smashing-tv-speaker">Mina:</span> I will admit to being one of those people in the past. Actually, probably it was mostly about SASS, I believe. I was very much on the team of doing SASS as a preprocessor and all other preprocessors are trash. I don’t want to talk about them. I don’t want to deal with them. And I realized that was a very narrow way to look at things. Use the appropriate tool for the job. Whatever makes you more productive, that’s the right tool. It doesn’t really matter what it is.

<span class="smashing-tv-host">Drew:</span> Are there any technologies that we work with that don’t have that sort of tribal feel? Is there anything that people are just happy to use or not use? I can’t think of anything.

<span class="smashing-tv-speaker">Mina:</span> Wow. No one has opinions about markup, actually.

<span class="smashing-tv-host">Drew:</span> No.

<span class="smashing-tv-speaker">Mina:</span> I feel like no one has opinions about like actual HTML and just markup, just like, "It’s there." They use it. But people have strong opinions about CSS and how it’s either terrible or wonderful, and the preprocessor wars that don’t really happen all that much anymore, and then of course, all of the tribalism within the various JavaScript libraries.

<span class="smashing-tv-host">Drew:</span> So you would say your journey so far with React is still just, "It’s a tool. It does its job?"

<span class="smashing-tv-speaker">Mina:</span> It went from a curiosity to active and visceral dislike because of how prevalent it was and how I unnecessary I thought that that prevalence was to meh. I’m now with meh, which again does not mean I hate it. It just means ...

<span class="smashing-tv-host">Drew:</span> I think that’s a good place to be. I think we’re probably all sort of stronger as technologists if we understand the value of a particular technology for its purpose. We can evaluate what is good for what circumstance and pick the right tool for the job.

<span class="smashing-tv-speaker">Mina:</span> Yeah. And that’s kind of where I’ve arrived at this point in my career where I don’t get really invested in any particular language, or technology, or whatever, because it’s like, "Just whatever tool is most appropriate for what you’re trying to do, then use that." I’ve learned that there’s a place for everything; there’s a time and a place to do everything. And up until recently, there was no real time or place for me to use this React librarian, and now there is.

<span class="smashing-tv-host">Drew:</span> I think that’s a good place to be. So I’ve been learning all about React lately as you have in the day job. Is there anything else that you’ve been learning about lately?

<span class="smashing-tv-speaker">Mina:</span> I’ve actually learned ironically, which is I think another language that has originated at Facebook, I’ve been doing a lot of Hack development, mostly because that’s what I use at Slack, at my day job. Learning Hack paved the way for me to get more comfortable using React because they follow very similar patterns, except one is server side and one’s not. So that, along with just in general, I’ve been learning more about the back-end and how that works for various different reasons. And I’ve been stretching myself for the past couple years and getting more and more outside of my comfortable zone. Design systems, libraries, that’s very much my world, and I feel very good and comfortable in that world. But I’m stepping outside of it and doing a lot more server side logic, and API development, and data modeling, and all of that. I’ve been doing a lot on that for the past year as well.

<span class="smashing-tv-host">Drew:</span> I find that the more I understand about the whole stack about back-end stuff in front-end stuff, each one helps my knowledge of the other. I find I write better front-end code by having written back-end code and understanding-

<span class="smashing-tv-speaker">Mina:</span> Yeah. I think I feel the same way. Now that I have a better idea of, like we said, the whole stack of how we get from the data to the end client. I find that I’m thinking about the entire pipeline no matter what part I’m actually working in. I’m thinking about what’s the best way to structure this API so that when I get to the template, I don’t have to do so much manipulating of the data that I receive on that end of it. It’s definitely made me overall a better engineer, I feel like it

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Mina, you can follow her on Twitter where she’s @MinaMarkham and find her personal site at mina.codes. Thanks for joining us today, Mina. Do you have any parting words?

<span class="smashing-tv-speaker">Mina:</span> Have a smashing night?

<span class="smashing-tv-host">Drew:</span> Great.

{{< signature "il" >}}
