---
title: 'Smashing Podcast Episode 40 With Mike Cavaliere: What Is Chakra UI For React?'
slug: smashing-podcast-episode-40
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e981ad2c-0679-4935-b19f-39d1ca96823e/smashing-podcast-episode-40.jpg
date: 2021-06-29T05:30:00.000Z
summary: >-
  In this episode, we’re talking about Chakra UI. What is it and how can it help with your React projects? Drew McLellan talks to expert Mike Cavaliere to find out.
description: >-
  In this episode, we’re talking about Chakra UI. What is it and how can it help with your React projects? Drew McLellan talks to expert Mike Cavaliere to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Wix
  link: https://www.wix.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc3245af-20d9-4039-9a49-8ab431a0b8fd/wix-logo.svg
  description: >-
    This episode has been kindly supported by our dear friends at <a href="https://www.wix.com/" style="text-shadow: none;">Wix</a> who are known to give you the freedom to create, design, manage and develop your web presence exactly the way you want. <em>Thank you!</em>
---

In this episode, we’re talking about Chakra UI. What is it and how can it help with your React projects? Drew McLellan talks to expert Mike Cavaliere to find out.

<iframe src="https://share.transistor.fm/e/725f560d/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [Chakra UI](https://chakra-ui.com)
- Mike [on Twitter](https://twitter.com/mcavaliere)
- Mike’s [personal website](https://mikecavaliere.com)
- [Cut Into The Jamstack](https://www.cutintothejamstack.com) book

### Weekly Update

- [Designing With Code: A Modern Approach To Design](https://www.smashingmagazine.com/2021/06/design-code-modern-approach-development-challenges/)  
*written by Mikołaj Dobrucki*
- [Automating Screen Reader Testing On macOS Using Auto VO](https://www.smashingmagazine.com/2021/06/automating-screen-reader-testing-macos-autovo/)  
*written by Cameron Cundiff*
- [The Rise Of Design Thinking As A Problem Solving Strategy](https://www.smashingmagazine.com/2021/06/design-thinking-problem-solving-strategy/)  
*written by Josh Singer*
- [How To Run A UX Audit For A Major EdTech Platform](https://www.smashingmagazine.com/2021/06/ux-audit-edtech-platform-case-study/)  
*written by Mark Lankmilier*
- [Creating A Multi-Author Blog With Next.js](https://www.smashingmagazine.com/2021/06/creating-multi-author-blog-nextjs/)  
*written by Dom Habersack*

## Transcript

<p><a href="https://twitter.com/mcavaliere"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f9eda70-2e28-4ae6-9790-7a3e8d288469/mike-cavaliere-200x200x.jpg" width="200" height="200" alt="Photo of Mike Cavaliere" /></a><span class="smashing-tv-host">Drew McLellan:</span> He’s a Senior Software Engineer for an agency called Echobind. He’s been writing code for two decades, and using JavaScript the whole time. He loves the Jamstack, and his new book, Cut Into The Jamstack, teaches the reader how to build a software as a service app from scratch. We know he knows his way around the Jamstack, but did you know he once got lost in the peanut butter aisle? My smashing friends, please welcome Mike Cavaliere. Hi, Mike. How are you?

<span class="smashing-tv-speaker">Mike Cavaliere:</span> I am absolutely smashing today.

<span class="smashing-tv-host">Drew:</span> That’s good to hear. I wanted to talk to you today about a project that I’d really not heard of, somehow, until I came across it in your Jamstack book. I’m not sure how I’d missed it because it seems to be maturing and well documented and a real... Just a great project. I’m hoping that today we can talk about it, and I can catch up to find out what I should’ve known all along. I’m talking about Chakra UI, of course. Tell me, what is Chakra UI? What space is it in, and what problem is it solving for us?

<span class="smashing-tv-speaker">Mike:</span> Chakra UI is a UI framework for React or UI toolkit, I guess they phrase it as. In any application stack, nowadays you don’t want to invent a UI from scratch. You want to grab some toolkit. That’s been the case for a while.

<span class="smashing-tv-speaker">Mike:</span> Chakra UI is a great approach on a React UI toolkit. There’s a number of perks to it, but one is that it’s... For one, it’s robust. That means it’s got just every UI element that you could imagine. It’s got switches. It’s got wrappers around grids. It’s got all types of things form elements.

<span class="smashing-tv-speaker">Mike:</span> It’s made to be very composable, so that everything used style props. Your components, they’re great right out of the box. You can drop them and use them as is. But if you want to make a tweak, it’s very easy to pass in some style properties. They’re fully accessible. The accessibility, which everybody talks about but always forgets to implement or it takes a little effort to implement, it’s built in for you.

<span class="smashing-tv-speaker">Mike:</span> It’s not uncommon for me to put together something with Chakra UI and get a very good Lighthouse score. Actually, I was just checking the Cut Into The Jamstack website today, and the accessibility score is very high. It’s also very fully themeable. You can set theme configuration from beginning. There’s just a long list of perks to it.

<span class="smashing-tv-speaker">Mike:</span> It makes it very fast to develop, which was what originally attracted me to it. Echobind, we use it internally. But for me, I don’t have design sense. A little bit, but I’m not a designer by any means. I can grab components from Chakra and alter things ever so slightly to make it consistent and things just look good out of the box. You’re able to develop fast. Developer experience is great. It’s just awesome on so many levels.

<span class="smashing-tv-speaker">Mike:</span> Last thing I’ll say before I keep rambling about it. But it also has a lot of React Hooks that are helpers for very common functionality things that come along with these elements that you’re using. For example, on dark mode. There’s built in hooks for using lighter dark mode that just very obtrusively let you toggle colors in your theme.

<span class="smashing-tv-speaker">Mike:</span> There’s another one for used disclosure which is for toggling things like modules. Which you always need an on, off state. But the Hook just simplifies that even more so you can focus on the things that the framework can’t infer automatically. I’ll cut it off there, because that was a lot.

<span class="smashing-tv-host">Drew:</span> That’s really good. Just so I’ve got my understanding right, first of all it’s Shakra not Chakra? Shakra?

<span class="smashing-tv-speaker">Mike:</span> I wouldn’t be the expert on that. I’ve been saying Shakra just because of yoga. But we’ll have to ask the founders to double-check.

<span class="smashing-tv-host">Drew:</span> It’s an off the shelf design system that you can drop in to build the UI for your project.

<span class="smashing-tv-speaker">Mike:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> It’s specifically for React projects.

<span class="smashing-tv-speaker">Mike:</span> Yeah. There is a Chakra Vue project out there. I’m not a Vue person very much but I know that it does exist. There may be for other frames as well, but I’m very, very React focused so I’ve been using the Chakra default React one.

<span class="smashing-tv-host">Drew:</span> Yes. I’ve been familiar with React in the past. I’ve used React when I worked at Netlify. Now I do everything in Vue. That was one of the first things I looked at. Oh, is there a Vue? This looks good. Is there a Vue version of it? I found a Vue version of it and it seems to be quite a way behind. I think it’s on 0.9 or something, rather than 1.6 or whatever the current React version is. I’m not sure how current that is.

<span class="smashing-tv-host">Drew:</span> We’ve got fairly outdated frameworks out there. Things like Foundation UI, Bootstrap, Bulma. They’ve been around for a long time and they’re a previous generation of framework, it would seem. Then we’ve got some more modern approaches. I think a lot of listeners will be familiar with Tailwind and the Tailwind UI project. Where does Chakra UI fall amongst that landscape? It’s closer to something that Tailwind might... An approach that tailwind might take. Is that correct?

<span class="smashing-tv-speaker">Mike:</span> I think so. Admittedly, I’ve been meaning to really dig into Tailwind a lot more just because it’s so popular right now. But I can’t speak intelligently on the ins and outs of Tailwind itself and how... My sense is that Chakra and Tailwind are alternative approaches. You grab for one, not both at the same time, obviously.

<span class="smashing-tv-speaker">Mike:</span> I don’t yet know what the pros and cons are for both. I’ve just been so enamored with Chakra that I just keep using it by default. I’m like, "Okay, I know this really well now. I love it. I’ll get to learn the other one later." But Tailwind obviously, extremely popular. I think Tailwind has their base framework in a UI toolkit. Is that fair?

<span class="smashing-tv-host">Drew:</span> Right. Yeah.

<span class="smashing-tv-speaker">Mike:</span> Okay. This would probably be more on par with the UI toolkit of Tailwind. On the Chakra homepage, they do have a comparison on why you might want to reach for one or the other, but I don’t have it internalized.

<span class="smashing-tv-host">Drew:</span> Yeah. That’s good. As we mentioned, for React projects and the way that manifests itself rather than some of these more traditional design systems which give you a whole load of class names to put on your HTML and you have to use some HTML structure, put the right classes on it. That’s the way you get the UI manifesting in your project. With Chakra, because it’s based on React, it’s giving you a whole load of components for each of those elements. You can just import into your project. Those components encapsulate their own markup and styling, do they?

<span class="smashing-tv-speaker">Mike:</span> Yeah. You won’t actually have to write a class using Chakra. I haven’t. I don’t even know if it’s possible. The whole React paradigm is a component composition and properties. Encapsulation of components means you pass certain properties into the component. In Chakra, you have this notion of a theme which is a global paradigm. There’s a default theme and it’s got values for color and spacing and certain units for all common things.

<span class="smashing-tv-speaker">Mike:</span> You can customize that theme. It customizes it globally. You can augment it however you need to. When you call the component itself, for example, a text input. An input component. That’s going to have default colors and border radius and padding and margin as defined by the theme. When you want to style it further, if you don’t want to do it on a global basis, for example, when I specify bottom margins, I do it on a case by case basis. I don’t do it at that a global level because that can lead to catastrophe. You just pass it as a prompt.

<span class="smashing-tv-speaker">Mike:</span> There are shortcut prompts. If I have an input component I just say, MB equals, and then a value and it’ll apply the margin bottom. Or they have MX and MY for vertical and horizontal. Or you could just specify M and pass in the string as you would the margin CSS property. There’s no class names. It does the class names all dynamically and obfuscates that away from the user.

<span class="smashing-tv-host">Drew:</span> Yes. I think that’s where the comparison with Tailwind must come in. Because the way Tailwind works, is it gives you a whole load of classes. If you want to increase the margin, there’s a class that you can put on to increase the margin. It sounds actually you’re taking that same... It’s a different implementation, but the same approach to how its architected. We’re actually using props and you’re passing a prop in to adjust those things.

<span class="smashing-tv-host">Drew:</span> How easy is it to customize a design? Is it a case of just being able to tweak colors and margins and padding and make it look a little bit different? Or can you actually really brand up a theme with Chakra?

<span class="smashing-tv-speaker">Mike:</span> Oh, you can do whatever the heck you want. It’s great. You could style at the component level or the theme level. It just depends on how creative you want to be with it. I’ve managed to take some components and do some wild things with them. Part of what makes it really styleable is that these components are pretty atomic.

<span class="smashing-tv-speaker">Mike:</span> Using the text box example again, if you want a text box, your component is just that. You can style everything around it or you can style the text box itself. Or you can change the theme. Setting the colors to rebrand everything globally.

<span class="smashing-tv-speaker">Mike:</span> I actually tweeted the creator of Chakra UI, Seg, saying they should put a gallery on the site because it’s really great. You can create some beautiful designs with it. They’re very varied and you might not know on the surface there. I don’t know if Chakra UI has any tells that make it obvious that you’re using a Chakra UI for your site.

<span class="smashing-tv-speaker">Mike:</span> I’ve seen some pretty nice stuff with it. But you can do anything with it. I’ve done static websites. The Cut Into The Jamstack homepage is done with it. Just as one example. We’ve used it at Echobind plenty. I can’t remember if we’ve used that for echobind.com. But certainly many of our clients sites. Then the app that I’ve been building, JamShots, it’s an app. It doesn’t have marketing pages yet. But it’s all just UI and all that UI is built using Chakra.

<span class="smashing-tv-speaker">Mike:</span> One other thing just while I’m praising Chakra is that, there’s another website that I’ve been using a lot lately, and I use in... I’m going to introduce into the book as well. Chakratemplates.net. Chakra-templates.net. It’s a common design patterns that whoever’s contributing is finding a hero unit or a pricing unit. They just have to copy and pastable Chakra code.

<span class="smashing-tv-speaker">Mike:</span> I use that entirely for the book homepage because it just saved me so much time in developing it. It’s like, oh, you have a pricing model. Let me copy and paste that. Let me just adjust the style props a little bit so that everything’s consistent on my site. That’s it. It’s just another thing that is separate from Chakra itself, but it just, it’s such a time saver because you need these things on so many websites and who wants to reinvent the wheel every time.

<span class="smashing-tv-host">Drew:</span> It sounds it can be a real time-saver, not only for personal projects where you want to roll something out quickly, but in an agency context.

<span class="smashing-tv-speaker">Mike:</span> Oh, yes. Absolutely.

<span class="smashing-tv-host">Drew:</span> Does that apply equally to app interfaces as well as marketing sites? Does it skew one way or the other or is it just generally useful whatever you’re building?

<span class="smashing-tv-speaker">Mike:</span> I’d say it’s both. It definitely is. I’ve used it for both. Our company has used it for both. We build, I’d say we lean heavily towards building full stack applications and mobile applications. We definitely have a lot more need for UI than marketing stuff. Although we sometimes build that as well. It’s useful for both.

<span class="smashing-tv-speaker">Mike:</span> There is something on the site that they do mention, like when would you not want to use Chakra? They do say that because of the way it simplifies this interface CSS. There might be challenges when you have a lot of data on screen. If you’re creating tons and tons of DOM elements and doing a lot of real-time updates, you might or might not run into performance challenges.

<span class="smashing-tv-speaker">Mike:</span> I haven’t seen a performance issue ever. But I also haven’t built something that was so data intensive in real-time. It’s concern. If I was going to build an app like that, I’d probably want to spike up two different approaches anyway, just to see how they perform with a whole lot. But yeah. It’s universally useful for both of those cases.

<span class="smashing-tv-host">Drew:</span> I guess there’s always a trade-off, isn’t there with technology choices? Something that makes it really, really simple. Really quick to implement. The trade-off might be once you’re creating a 1,000 data points or whatever on a page, that method of working is not going to perform well and slows you down.

<span class="smashing-tv-host">Drew:</span> Yes. I think that’s fair. I tend to find in technology choices, the most important thing is just to know. Just to know what the trade-offs are and what the limitations are. None of them are good or bad. You just need to find an appropriate balance for your own situation.

<span class="smashing-tv-host">Drew:</span> As you’d expect to find with a design system of this kind, it comes with components for typography. For layout. Then down to nitty-gritty of buttons and form elements and there’s an icon library. There’s pretty much everything that you’d expect to see on a design systems’ kitchen sink page. You’ve got everything there. It all seems pretty modern to me. I noted that the layout grid component actually uses CSS grid, which is always nice to see. It’s not just gives some flex box.

<span class="smashing-tv-speaker">Mike:</span> Oh, yeah. Totally.

<span class="smashing-tv-host">Drew:</span> Is it generally very flexible to work with? Do you find that the layout elements you’re able to build any type of UI that you need to?

<span class="smashing-tv-speaker">Mike:</span> Yeah. Yeah. Absolutely. What’s great about it is they, in some cases provide more than one level of abstraction. In the case of CSS grid, they have a simple grid which is like, okay. You want to drop it in and here’s your grid. You just put stuff inside of it and you specify, I think the number of columns or something like that. Then you’ve got a grid.

<span class="smashing-tv-speaker">Mike:</span> But if you need to have a bit more flexibility over in the behavior of the grid, then you’ve got a generic grid component, which is probably... The simple grid component probably wraps the other grid component. It’s just another facade on top of itself.

<span class="smashing-tv-speaker">Mike:</span> That approach towards composition of components, it’s a valuable paradigm in the React world because of the same thing. If you have a component that is very versatile and has a lot of props to it, well then, there might be a set of use cases that you want to use the component one way for fairly commonly. You just wrap it with another component with static or pre-specified props for the more robust components.

<span class="smashing-tv-speaker">Mike:</span> They use that approach really well in Chakra. I haven’t run into anything that I can’t do with it yet. I’m sure it’s out there somewhere. Or something that’s just a little more of hassle to do. But it generally hasn’t happened yet. Not that I can think of at least.

<span class="smashing-tv-host">Drew:</span> Well, one of the things I was really pleased to see and something that you mentioned earlier as well, is there seems to be this quite strong focus on accessibility.

<span class="smashing-tv-speaker">Mike:</span> Yes.

<span class="smashing-tv-host">Drew:</span> Certainly in the promotional information. Is that born out in the code itself? Do they practice what they preach? Is it actually got good accessibility built in?

<span class="smashing-tv-speaker">Mike:</span> I think so. The closest I’ve done to putting it to the test is running Lighthouse against it. It consistently provides high scores for accessibility. I typically will use Chakra Next.js. Next.js is performance right at the box. It’s quite often that you’ll see high scores and everything. I just tweeted today about how the book’s homepage has three out of the four Lighthouse scores. There’s accessibility, best practices, performance and one fourth one. I’m not thinking right now.

<span class="smashing-tv-speaker">Mike:</span> Everything but performance came out close to 100%. The performance part is on me just because I put a lot on the page and I haven’t optimized it yet. It tends to do that. The accessibility scores in Lighthouse are great whenever I use Chakra UI.

<span class="smashing-tv-host">Drew:</span> That’s great. You mentioned they’re using server-side rendering and what have you. Things like Next and Gatsby and what I have you, is absolutely no problem, is it? There aren’t any hurdles to be aware of using Chakra with those?

<span class="smashing-tv-speaker">Mike:</span> Oh, no. Not at all. I haven’t used it. I tend to focus on Next.js. I haven’t plugged into Gatsby or any of the other SSR tools. But as long as the framework, it doesn’t have anything that would block it from using it as such, then it should be fine.

<span class="smashing-tv-speaker">Mike:</span> For React, Chakra provides a context API provider. A theme provider so that when you... In my Next.js apps for example, you have a... Next.js has a underscore app JS or TS file that just wraps every page in the application. You just plug the theme provider in there and Chakra does the rest of the work and it just becomes available everywhere. There’s a no hurdles to adding into Next.js certainly. But I imagine not to Chakra either.

<span class="smashing-tv-host">Drew:</span> Does Chakra use TypeScript? I believe it does, doesn’t it?

<span class="smashing-tv-speaker">Mike:</span> It supports it. Yep.

<span class="smashing-tv-host">Drew:</span> It supports it. That’s a big plus for people who use TypeScript already in their projects. Is there any downsides to that if people aren’t already using TypeScript?

<span class="smashing-tv-speaker">Mike:</span> I don’t think so. I use TypeScript by default in all my projects, and so does Echobind. But when I do things on a personal level, I use... I like to say sprinkle of TypeScript. Typescript is extremely valuable in reducing errors by creating static types. There’s a carrier for it though, where depending on your knowledge of it, TypeScript can be a real hurdle.

<span class="smashing-tv-speaker">Mike:</span> My minimum threshold for... The strictness of TypeScript that I use is fairly low simply because you can get a lot of value out of TypeScript with basic typing. It will prevent a lot of common mishaps. When you go into the more advanced typing, if you’re not super comfortable with that stuff, it can really slow you down and frustrate you.

<span class="smashing-tv-speaker">Mike:</span> That’s just to say same thing with Chakra and TypeScript. I tend to use a light amount of TypeScript, at least in the beginning until I’m really fleshing out and stabilizing a project. But it presents no challenges in using Chakra, either with or without TypeScript. It’s great with. I love it with, but you can certainly use it without as well.

<span class="smashing-tv-host">Drew:</span> Yeah. I find with TypeScript that you get 80% of the benefits, as you say, with just with a few types. If you get too far down the rabbit hole, you end up with a script that’s mostly TypeScript. Then a bit of JavaScript to the bottom.

<span class="smashing-tv-speaker">Mike:</span> Or you spend so much time trying to figure out the right way to type something and your brain blows up. That’s how you just put any or unknown. You shortcut it. Which I advocate for in cases like that. If it’s taking too much time for you to get something done, then there is a lever you can pull.

<span class="smashing-tv-host">Drew:</span> The Chakra documentation seems to be really well pitched, I thought, with... It has an overview of each component. Then it really usefully includes any technical notes about the design considerations that were made when implementing that component. Which, as a front end engineer, I think that’s great. They’re talking my language. I understand. I know what the component is doing slightly under the hood.

<span class="smashing-tv-host">Drew:</span> That’s just from my perspective, browsing the documentation without a real project that I’m working on. When you’re actually working on a project and deep in the weeds of it, just the documentation hold up? Is it as useful as it seems?

<span class="smashing-tv-speaker">Mike:</span> Oh yeah. Absolutely. My perspective is a little different. I don’t always need to know what’s going on under the hood, but I feel I can infer usually. If I’m looking at a box component, I’m just looking at the docs now while we’re talking for refresher. If I look at a box component, I’m like, "Okay. That’s probably a div by default. I see it passing in the gradient properties, whatever."

<span class="smashing-tv-speaker">Mike:</span> I can get some sense of what’s going on in the hood without fully understanding their magic to translate CSS. Translate the props to CSS. But the documentation is great in that it’s very linear. It’s very consistent. It lists everything with examples. A little copy and paste.

<span class="smashing-tv-speaker">Mike:</span> It just uses really good white space so looking at the page doesn’t seem overwhelming. You can find what you need easily. Their search is great too. Their search is helpful. 90% of the time, I think that’s what I’m going in there for. May be going in there and seeing if a component exists to do something. It usually does. And stumbling across something else that was useful that I didn’t know about. Or just refreshing myself on some of the principles. I can always pretty much find what I need here.

<span class="smashing-tv-host">Drew:</span> The only thing that I didn’t like about the docs from glancing around was the number of ads on it. On every page for their commercial offering of Chakra UI Pro.

<span class="smashing-tv-speaker">Mike:</span> I hadn’t seen them. Interesting. I’ve seen it. I’ve definitely seen it. But I’m not seeing it right now. Oh yeah. Okay. There’s Chakra UI Pro. I guess I filtered it out mentally. I hear you. At least it’s not too big and in your face.

<span class="smashing-tv-host">Drew:</span> It’s not too big. It’s just in the wrong place. It’s just where you’re looking for the information. Which I guess is why they’ve done it. That’s worth mentioning in considering the ecosystem and everything around the project is there’s a pro set of components that is... I guess it’s equivalent to some of the stuff that’s in Tailwind UI that’s there. Marketing pages and here are components and more of these composed sections of pages and entire pages and layouts and things. That you, is available from the makers of Chakra, but as a commercial offering.

<span class="smashing-tv-speaker">Mike:</span> Yeah. Just taking a quick glance at it now. Some of these are actually available. Or versions of them are available for free like Chakra templates. It’s Chakra templates, I guess, is the open source solution to Chakra Pro or the open-source competitor. I’m sure you’re going to get a ton by paying for this. It looks Chakra Pro is extremely robust and reasonably priced if you have a paying professional need for these. There’s a couple of options for your project, it looks like.

<span class="smashing-tv-host">Drew:</span> Yeah. It sounds there’s quite an ecosystem built up around it. Do you know how long the project’s been going and what following there is? Is it in widespread use in the React community?

<span class="smashing-tv-speaker">Mike:</span> I want to say yes. I don’t know to what degree. I’d be curious to just see what’s the, I guess, market share of Tailwind versus Chakra nowadays. I do know Chakra got an award relatively recently. GitNation React Award for the most impactful project to the community. I’d say it’s pretty big and pretty well embraced. With good reason, which is great. People are definitely enjoying it. I’m not the only one.

<span class="smashing-tv-host">Drew:</span> One thing that’s always worth thinking about when bringing a dependency into your project is what happens when you need to update that dependency.

<span class="smashing-tv-speaker">Mike:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> Chakra is being improved all the time, I imagine. Is it a case of once you’ve imported it and built with it, you leave it locked on a certain version? Or is it generally safe to keep updated? Is it relatively stable in terms of the design and things of your site not changing as Chakra updates?

<span class="smashing-tv-speaker">Mike:</span> It has been so far. Yeah. Mainly, I’d say that’s because of the progress of development. They’re on version 1.6.3 right now. A number of months ago, they went from zero to one. That was the only time they had breaking changes. Since then, they’ve just been constantly doing feature releases and bug fixes.

<span class="smashing-tv-speaker">Mike:</span> For the last at least couple of months, everything’s been just additions. Additions and fixes. There’s no breaking changes involved. I don’t know what the roadmap looks like, but I imagine it’ll continue to be so. Every time I’ve upgraded it, one of these minor versions, it’s been fine. I’ve never seen something break from it. But when they came out with 1.0, there were some breaking changes. I don’t remember it being catastrophic though.

<span class="smashing-tv-host">Drew:</span> Do you know what the situation is with bundle sizes and the ability to tree shake Chakra? Does it add a lot of weight to your project or things are only imported as you use them?

<span class="smashing-tv-speaker">Mike:</span> I don’t recall off hand, honestly. I probably should know that. I haven’t noticed it adding a lot of weight. Mainly because you are importing the components individually. Not importing all of Chakra or anything like that. I’d say it’s in line having support for tree shaking, but I haven’t put it to the test. So far, I haven’t had things that had enormous weight coming specifically from it, though.

<span class="smashing-tv-host">Drew:</span> Yeah. That’s always an important consideration, isn’t it?

<span class="smashing-tv-speaker">Mike:</span> Yep.

<span class="smashing-tv-host">Drew:</span> Is there anything else we should know about Chakra UI before we dive right in and use it on a project?

<span class="smashing-tv-speaker">Mike:</span> No. It’s great. There’s pretty active community too. I see updates often. I’m looking at the documentation now and seeing components I hadn’t seen before. I see there’s a lot of feature addition going on. That’s great.

<span class="smashing-tv-host">Drew:</span> Yeah. That is great. You’ve got a book out called Cut Into The Jamstack, which is a preview release. A beta release at the moment. You’re self-publishing that. Is that right?

<span class="smashing-tv-speaker">Mike:</span> Yeah. Yeah. I am. It was my first attempt at a technical book. I just want to get it out there without committing to something like, it’s formal, I guess. I’m also somebody who likes informality, especially when creating things. It gives me the ability to do it my way by doing it like that.

<span class="smashing-tv-host">Drew:</span> The book literally walks the reader through building a software as a service app.

<span class="smashing-tv-speaker">Mike:</span> Yep.

<span class="smashing-tv-host">Drew:</span> All on the Jamstack. Why was it you decided to write this now and to take this approach with the book?

<span class="smashing-tv-speaker">Mike:</span> Good question. I’ve been coding for some 20 years now and I think I attempted to write a book a while back and it just didn’t quite take shape. I’m at a point in my career where I really want to share more knowledge. I’ve been using it for so many years and I feel the itch to really put more of it out there and help others.

<span class="smashing-tv-speaker">Mike:</span> Around October of last year, I had this... I wanted to put something out there that was product. An ebook felt like a really good way to start. I’m really passionate about Next.js and the things you can do with it. I use the term Jamstack and I consider Next.js as part of the Jamstack because it has a static site generation as a default.

<span class="smashing-tv-speaker">Mike:</span> But I think it’s one thing that doesn’t get talked about enough, in my opinion, or could use some more explanation is building software as a service applications with it. Because the Jamstack isn’t just for websites. It works really well for content driven websites because of being static and snappy and SEO friendly.

<span class="smashing-tv-speaker">Mike:</span> But there’s so much rich functionality there, especially in Next.js where Vercel had their Next.js Conference yesterday and they’re releasing more and more amazing features in there. I’m passionate about building software as a service. Software websites are great, but software is meant to do things.

<span class="smashing-tv-speaker">Mike:</span> This stack to me is very much the future of software as a service development. It reminds me of what Ruby on Rails was when it came out. It was an evolution, in a matter of speaking. It automated and simplified a lot of things that you used to have to do manually. It sped up the pace of development, and it increased the quality of it.

<span class="smashing-tv-speaker">Mike:</span> Next.js and the Jamstack and Vercel and Chakra UI, they’re all producing things that simplify a lot of things for you. Next.js, it simplifies a lot of speed related issues and accessibility related issue. Instanalization. Those are all, routing is done for you. You don’t have to worry about client side or service side routing. It’s automatic. Chakra UI does that with accessibility and theming. These tools put together, they just... The developer experience gets really great and everything just... It gives you freedom to really create software.

<span class="smashing-tv-speaker">Mike:</span> To answer your question. The reason I put out a book now is because of the right time of me really wanting to put something out there and with the Jamstack ecosystem starting to come to fruition and growing. It also gave me a chance to write more code into Jamstack, which, I just love it.

<span class="smashing-tv-host">Drew:</span> I think, as you say, it’s easy to get on board with the idea of Jamstack when you’re thinking about websites and typically lightweight websites. But taking that next step into thinking about how you can use the approach to build a full web application, it’s much harder. It’s a bigger hurdle, I think, to get over if you’re used to thinking in the server side mindset.

<span class="smashing-tv-speaker">Mike:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> It’s a much bigger jump to see, okay. I can put my authentication out to a service-

<span class="smashing-tv-speaker">Mike:</span> Yes.

<span class="smashing-tv-host">Drew:</span> ... and I can... I guess for the readers, from the reader’s point of view of your book, just by going through and building this example, following along with you, it’s probably a great way to get over that hurdle to just help gently shift your mindset into, okay. This is how I could do all these things, but on the Jamstack. Would you agree with that?

<span class="smashing-tv-speaker">Mike:</span> Yeah. That’s what I’m hoping. I do think it does. That’s really what it’s intended. I was signing a talk recently, a conference talk that... Part of my motivation for the topic and the way I decided to teach in this book is that, I could teach you one programming language. A framework, but it feels better to introduce you to the stack in a hands-on manner because, every developer who’s got a lot of experience is good at going for documentation and Googling and using stack overflow. Why would I waste your time teaching that to you?

<span class="smashing-tv-speaker">Mike:</span> I want to give you a quick, deep dive into the stack and what I can do with it. You’re going to pick up the what’s great about each of the individual pieces. NextOFF and Prisma. Next.js and Chakra. I’ll link you to documentation just to save you a couple of clicks. But you’re going to see through an interactive example, how these pieces connect together. You’re also going to get an understanding of the hard parts.

<span class="smashing-tv-speaker">Mike:</span> One thing I’m going into depth in, for example, is this feature that I’m building for asynchronous multi-file upload. Next.js has a front end and a backend to it. Though in the front of the front end and the back of the front end, if you use that analogy, you’ve got the React layer. Then you’ve got the node layer. There’s these API routes.

<span class="smashing-tv-speaker">Mike:</span> If you want to do multi-file upload with that and use a service, I use Cloudinary in the book. But if you use an API service for your image and media uploads which you should, there’s a lot of moving pieces there. There is the client side, which the user interacts with. There’s the API requests to the Cloudinary or the other provider. But then you have to make multiple API requests to make it efficient. You have to do some signing against Cloudinary, which you need an API call for.

<span class="smashing-tv-speaker">Mike:</span> You need to take that sign and you need to do the upload, which goes from the browser and circumvents your API and goes directly to Cloudinary. Then you need to save that in your database, which uses your front end backend of the front end. There’s many pieces and Next.js... In the Next.js community, there isn’t an open source plugin for that yet. Which I may extract out of the app now that have built it and put it into one because other people are going to have this.

<span class="smashing-tv-speaker">Mike:</span> Anyway, all that’s just to say that, I think that’s something really valuable to teach to people. Even if you’re a senior engineer, for a few dollars, you get all this wrapped up for you with a bow on it to be like, okay. This is a series of tools that worked really well together for building SaaS apps with a stack. This hurdle, I don’t have to figure out a solution for writing custom. Here’s an approach that works.

<span class="smashing-tv-speaker">Mike:</span> I just, I take a lot of joy in trying to prevent people from having to reinvent the wheel. Even though it’s fun to reinvent the wheel, if you wanted to just ship something, the more you can reduce that, the better,

<span class="smashing-tv-host">Drew:</span> That sounds very, very helpful. The book is in beta now. If people buy it now, do they get updates as it improves?

<span class="smashing-tv-speaker">Mike:</span> Yep. Yeah. It’s immensely discounted. It’s $10 now. When I finish, it will be 30. Whoever gets it now, will just get updates for the life of the book.

<span class="smashing-tv-host">Drew:</span> Fantastic.

<span class="smashing-tv-speaker">Mike:</span> I’ve got another one coming up in probably a couple of weeks. Yeah. Yeah. It’s already 107 pages and it’s got a source-code repo that will be shipped with it. That comes along with it now. It’s already like you can do... In the first 107 pages, it goes through setup to build a new first full stack page to building a CRUD for photo galleries. Create, Read, Update, Delete. So the front end and backend components. Then shipping a deployment to railway and Vercel. It’s pretty practical right away. Then the further, other couple of 100 pages are going to be more in depth with the coding topics.

<span class="smashing-tv-host">Drew:</span> Great. That’s available now at cutintothejamstack.com.

<span class="smashing-tv-speaker">Mike:</span> Yep. That’s it.

<span class="smashing-tv-host">Drew:</span> I’ve been learning all about Chakra UI. What have you been learning about lately, Mike?

<span class="smashing-tv-speaker">Mike:</span> I’ve been digging deeper on the stack. It constantly teaches me new things. One example is just with the Vercel Conference yesterday. The Next.js Conf. Next.js 11 is now out and it’s just got a ton of great things with it. There’s a real-time collaboration tool built in so when you ship a preview deploy, you can have people commenting on it and moving their mouse around the screen, even it looks like.

<span class="smashing-tv-speaker">Mike:</span> In addition, their performance is getting better and better. Next.js’ image component, which I use heavily now is going to have automatic placeholders. It’s going to be even more streamlined. I’m constantly learning the better and better ways to do things in this stack. There are always more. It seems like.

<span class="smashing-tv-host">Drew:</span> Always. Always more to learn. If you dear listener would like to hear more from Mike, you can follow him on Twitter where he’s @mcavaliere, and his personal website is mikecavaliere.com. The book Cuts Into The Jamstack, which amongst other things shows a practical implementation of Chakra UI, is again at cutintothejamstack.com. Thanks for joining us today. Mike. Did you have any parting words?

<span class="smashing-tv-speaker">Mike:</span> Nope. Thanks so much for having me, Drew, and keep smashing out there. Maybe I should rephrase that.

{{< signature "il" >}}