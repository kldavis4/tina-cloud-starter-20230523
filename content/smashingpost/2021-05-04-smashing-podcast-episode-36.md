---
title: 'Smashing Podcast Episode 36 With Miriam Suzanne: What Is The Future Of CSS?'
slug: smashing-podcast-episode-36
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07c22e99-6bd0-4012-9227-b494596b6bc7/smashing-podcast-episode-36.jpg
date: 2021-05-04T05:00:00.000Z
summary: >-
  In this episode, we’re starting our new season of the Smashing Podcast with a look at the future of CSS. What new specs will be landing in browsers soon? Drew McLellan talks to expert Miriam Suzanne to find out.
description: >-
  In this episode, we’re starting our new season of the Smashing Podcast with a look at the future of CSS. What new specs will be landing in browsers soon? Drew McLellan talks to expert Miriam Suzanne to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re starting our new season of the Smashing Podcast with a look at the future of CSS. What new specs will be landing in browsers soon? Drew McLellan talks to expert Miriam Suzanne to find out.

<iframe src="https://share.transistor.fm/e/70c7cb07/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [Miriam Suzanne](https://twitter.com/TerribleMia) on Twitter
- Miriam’s [personal website](https://www.miriamsuzanne.com)
- [Cascade Layers is a Working Draft](https://css.oddbird.net/layers/explainer/)
- [Container Queries](https://css.oddbird.net/rwd/query/explainer/)
- [Scope](https://css.oddbird.net/scope/explainer/)

### Weekly Update

- [Web Design Done Well: The Ordinary Made Extraordinary (Part 1)](https://www.smashingmagazine.com/2021/04/web-design-done-well-part1/) written by Frederick O’Brien
- [A Guide To Newly Supported, Modern CSS Pseudo-Class Selectors — Smashing Magazine](https://www.smashingmagazine.com/2021/04/guide-supported-modern-css-pseudo-class-selectors/) written by Stephanie Eckles
- [How To Bake Layers Of Accessibility Testing Into Your Process — Smashing Magazine](https://www.smashingmagazine.com/2021/04/bake-layers-accessibility-testing-process/) written by Kate Kalcevich and Mike Gifford
- [Understanding Easing Functions For CSS Animations And Transitions — Smashing Magazine](https://www.smashingmagazine.com/2021/04/easing-functions-css-animations-transitions/) written by Adrian Bece
- [The Humble <img> Element And Core Web Vitals — Smashing Magazine](https://www.smashingmagazine.com/2021/04/humble-img-element-core-web-vitals/) written by Addy Osmani

## Transcript

<p><a href="https://twitter.com/TerribleMia"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/011ee1b6-bd40-4efc-bda5-ca85976ed1cb/miriam-suzanne-250x250.jpg" width="200" height="200" alt="Photo of Miriam Suzanne" /></a><span class="smashing-tv-host">Drew McLellan:</span> She’s an artist, activist, teacher and web developer. She’s a co-founder of OddBird, a provider of custom web applications, developer tools, and training. She’s also an invited expert to the CSS Working Group and a regular public speaker and author sharing her expertise with audiences around the world. We know she knows CSS both backwards and forwards, but did you know she once won an egg and spoon race by taking advantage of a loophole involving macaroni? My smashing friends, please welcome Miriam Suzanne. Hi, Miriam. How are you?</p>

<span class="smashing-tv-speaker">Miriam Suzanne:</span> I’m smashing, thank you.

<span class="smashing-tv-host">Drew:</span> That’s good to hear. I wanted to talk to you today about some of the exciting new stuff that’s coming our way in CSS. It feels like there’s been a bit of an acceleration over the last five years of new features making their way into CSS and a much more open and collaborative approach from the W3C with some real independent specialists like yourself, Rachel Andrew, Lea Verou and others contributing to the working group as invited experts. Does it feel like CSS is moving forward rapidly or does it still feel horribly slow from the inside?

<span class="smashing-tv-speaker">Miriam:</span> Oh, it’s both, I think. It is moving quite fast and quite fast is still sometimes very slow because there’s just so many considerations. It’s hard to really land something everywhere very quickly.

<span class="smashing-tv-host">Drew:</span> It must feel like there’s an awful lot of work happening on all sorts of different things and each of them edging forward very, very slowly, but when you look at the cumulative effect, there’s quite a lot going on.

<span class="smashing-tv-speaker">Miriam:</span> Yeah, exactly, and I feel like I don’t know what kicked off that change several years ago, whether it was grid and flexbox really kicked up interest in what CSS could be, I think, and there’s just been so much happening. But it’s interesting watching all the discussions and watching the specs. They all refer to each other. CSS is very tied together. You can’t add one feature without impacting every other feature and so all of these conversations have to keep in mind all of the other conversations that are happening. It’s really a web to try to understand how everything impacts everything else.

<span class="smashing-tv-host">Drew:</span> It feels like the working group very much always looking at what current practice is and seeing what holes people are trying to patch, what problems they’re trying to fix, often with JavaScript, and making a big messy ball of JavaScript. Is that something that’s a conscious effort or does it just naturally occur?

<span class="smashing-tv-speaker">Miriam:</span> I would say it’s very conscious. There’s also a conscious attempt to then step back from the ideas and say, "Okay, this is how we’ve solved them in JavaScript or using hacks, workarounds, whatever." We could just pave that cow path, but maybe there’s a better way to solve it once it’s native to CSS and so you see changes to things like variables. When they move from preprocessors like Sass and Less to CSS, they become something new. And that’s not always the case, sometimes the transition is pretty seamless, it’s more just take what’s already been designed and make it native. But there’s a conscious effort to think through that and consider the implications.

<span class="smashing-tv-host">Drew:</span> Yeah, sometimes a small workaround is hiding quite a big idea that could be more useful in itself.

<span class="smashing-tv-speaker">Miriam:</span> And often, hiding overlapped ideas. I was just reading through a lot of the issues around grid today because I’ve been working on responsive components, things like that, and I was like, "Okay, what’s happening in the grid space with this?" And there’s so many proposals that mix and overlap in really interesting ways. It can be hard to separate them out and say, "Okay, should we solve these problems individually or do we solve them as grouped use cases? How exactly should that be approached?"

<span class="smashing-tv-host">Drew:</span> I guess that can be, from the outside, that might seem like a frustrating lack of progress when you say, "Why can’t this feature be implemented?" It’s because when you look at that feature, it explodes into something much bigger that’s much harder to solve.

<span class="smashing-tv-speaker">Miriam:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> Hopefully, solving the bigger problem makes all sorts of other things possible. I spent a lot of my career in a position where we were just sort of clamoring for something, anything, new to be added to CSS. I’m sure that’s familiar to you as well. It now seems like it’s almost hard to keep track of everything that’s new because there’s new things coming out all the time. Do you have any advice for working front-enders of how they can keep track of all the new arrivals in CSS? Are there good resources or things they should be paying attention to?

<span class="smashing-tv-speaker">Miriam:</span> Yeah, there are great resources if you really want a curated, a sense of what you should be watching. But that’s Smashing Magazine, CSS-Tricks, all of the common blogs and then various people on Twitter. Browser implementers as well as people on the working group as well as people that write articles. Stephanie Eckles comes to mind, ModernCSS. There’s a lot of resources like that. I would also say, if you keep an eye on the release notes from different browsers, they don’t come out that often, it’s not going to spam your inbox every day. You’ll often see a section in the release notes on what have they released related to CSS. And usually in terms of features, it’s just one or two things. You’re not going to become totally overwhelmed by all of the new things landing. They’ll come out six weeks to a couple of months and you can just keep an eye on what’s landing in the browsers.

<span class="smashing-tv-host">Drew:</span> Interesting point. I hadn’t thought of looking at browser release notes to find this stuff. Personally, I make efforts to follow people on Twitter who I know would share things, but I find I just miss things on Twitter all the time. There’s lots of cool stuff that I never get to see.

<span class="smashing-tv-host">Drew:</span> In that spirit, before we look too far into the future into what’s under development at the moment, there are quite a few bits of CSS that have already landed in browsers that might be new to people and they might be pretty usable under a lot of circumstances. There are certainly things that I’ve been unaware of.

<span class="smashing-tv-host">Drew:</span> One area that comes to mind is selectors. There’s this "is" pseudo-class function, for example. Is that like a jQuery "is" selector, if you remember those? I can barely remember those.

<span class="smashing-tv-speaker">Miriam:</span> I didn’t use jQuery enough to say.

<span class="smashing-tv-host">Drew:</span> No. Now even saying that, it’s so dusty in my mind, I’m not even sure that was a thing.

<span class="smashing-tv-speaker">Miriam:</span> Yeah, "is" and "where", it’s useful to think of them together, both of those selectors. "Is" sort of landed in most browsers a little bit before "where", but at this point I think both are pretty well-supported in modern browsers. They let you list a number of selectors inside of a single pseudo-class selector. So you say, ":is" or ":where" and then in parentheses, you can put any selectors you want and it matches an element that also matches the selectors inside. One example is, you can say, "I want to style all the links inside of any heading." So you can say "is", H1, H2, H3, H4, H5, H6, put a list inside of "is", and then, after that list say "A" once. And you don’t have to repeat every combination that you’re generating there. It’s sort of a shorthand for bringing nesting into CSS. You can create these nested "like" selectors. But they also do some interesting things around specificity... Sorry, what were you going to say?

<span class="smashing-tv-host">Drew:</span> I guess it’s just useful in making your style sheet more readable and easy to maintain if you’re not having to longhand write out every single combination of things.

<span class="smashing-tv-speaker">Miriam:</span> Right. The other interesting thing you can do with it is you can start to combine selectors. So you can say, "I’m only targeting something that matches both the selectors outside of "is" and the selectors inside of "is"". It has to match all of these things." So you can match several selectors at once, which is interesting.

<span class="smashing-tv-host">Drew:</span> Where does "where" come into it if that’s what "is" does?

<span class="smashing-tv-speaker">Miriam:</span> Right. "Where" comes into it because of the way that they handle specificity. "Is" handles specificity by giving you the entire selector gets the specificity of whatever is highest specificity inside of "is." "Is" can only have one specificity and it’s going to be the highest of any selector inside. If you put an "id" inside it, it’s going to have the specificity of an "id." Even if you have an "id" and a class, two selectors, inside "is", It’s going to have the specificity of the "id."

<span class="smashing-tv-speaker">Miriam:</span> That defaults to a higher specificity. "Where" defaults to a zero specificity, which I think is really interesting, especially for defaults. I want to style an audio element where it has controls, but I don’t want to add specificity there, I just want to say where it’s called for controls, where it has the controls attribute, add this styling to audio. So a zero-specificity option. Otherwise, they work the same way.

<span class="smashing-tv-host">Drew:</span> Okay. So that means with a zero specificity, it means that, then, assuming that somebody tries to style those controls in the example, they’re not having to battle against the styles that have already been set.

<span class="smashing-tv-speaker">Miriam:</span> That’s right, yeah. There’s another interesting thing inside of both of those where they’re supposed to be resilient. Right now, if you write a selector list and a browser doesn’t understand something in that selector list, it’s going to ignore all of the selectors in the list. But if you do that inside of "is" or "where", if an unknown selector is used in a list inside of "is" or "where", it should be resilient and the other selectors should still be able to match.

<span class="smashing-tv-host">Drew:</span> Okay, so this is that great property of CSS, that if it doesn’t understand something, it just skips over it.

<span class="smashing-tv-speaker">Miriam:</span> Right.

<span class="smashing-tv-host">Drew:</span> And so, you’re saying that if there’s something that it doesn’t understand in the list, skip over the thing it doesn’t understand, but don’t throw the baby out with the bathwater, keep all the others and apply them.

<span class="smashing-tv-speaker">Miriam:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> That’s fascinating. And the fact that we have "is" and "where" strikes me as one of those examples of something that sounds like an easy problem. "Oh, let’s have an "is" selector." And then somebody says, "But what about specificity?"

<span class="smashing-tv-speaker">Miriam:</span> Right, exactly.

<span class="smashing-tv-host">Drew:</span> How are we going to work that out?

<span class="smashing-tv-speaker">Miriam:</span> Yeah. The other interesting thing is that it comes out of requests for nesting. People wanted nested selectors similar to what Sass has and "is" and "where" are, in some ways, a half step towards that. They will make the nested selectors easier to implement since we already have a way to, what they call "de-sugar" them. We can de-sugar them to this basic selector.

<span class="smashing-tv-host">Drew:</span> What seems to me like the dustiest corners of HTML and CSS are list items and the markers that they have, the blitz or what have you. I can remember, probably back in Frontpage in the late ’90s, trying to style, usually with proprietary Microsoft properties, for Internet Explorer back in the day. But there’s some good news on the horizon for lovers of markers, isn’t there?

<span class="smashing-tv-speaker">Miriam:</span> Yeah, there’s a marker selector that’s really great. We no longer have to remove the markers by saying... How did we remove markers? I don’t even remember. Changing the list style to none.

<span class="smashing-tv-host">Drew:</span> List style, none. Yup.

<span class="smashing-tv-speaker">Miriam:</span> And then people would re-add the markers using "before" pseudo-element. And we don’t have to do that anymore. With the marker pseudo-element, we can style it directly. That styling is a little bit limited, particularly right now, it’s going to be expanding out some, but yeah, it’s a really nice feature. You can very quickly change the size, the font, the colors, things like that.

<span class="smashing-tv-host">Drew:</span> Can you use generated content in there as well?

<span class="smashing-tv-speaker">Miriam:</span> Yes. I don’t remember how broad support is for the generated content, but you should be able to.

<span class="smashing-tv-host">Drew:</span> That’s good news for fans of lists, I guess. There’s some new selectors. This is something that I came across recently in a real-world project and I started using one of these before I realized actually it wasn’t as well supported as I thought, because it’s that new. And that’s selectors to help when "focus" is applied to elements. I think I was using "focus within" and there’s another one, isn’t there? There’s-

<span class="smashing-tv-speaker">Miriam:</span> "Focus visible."

<span class="smashing-tv-host">Drew:</span> What do they do?

<span class="smashing-tv-speaker">Miriam:</span> Browsers, when they’re handling "focus", they make some decisions for you based on whether you’re clicking with a mouse or whether you’re using a keyboard to navigate. Sometimes they show "focus" and sometimes they don’t, by default. "Focus visible" is a way for us to tie into that logic and say, "When the browser thinks focus should be visible, not just when an item has focus, but when an item has focus and the browser thinks focus needs to be visible, then apply these styles." That’s useful for having outline rings on focus, but not having them appear when they’re not needed, when you’re using a mouse and you don’t really need to know. You’ve clicked on something, you know that you’ve focused it, you don’t need the styling there. "Focus visible" is really useful for that. "Focus within" allows you to say, "Style the entire form when one of its elements has focus," which is very cool and very powerful.

<span class="smashing-tv-host">Drew:</span> I think I was using it on a dropdown menu navigation which is-

<span class="smashing-tv-speaker">Miriam:</span> Oh, sure.

<span class="smashing-tv-host">Drew:</span> ... a focus minefield, isn’t it?

<span class="smashing-tv-speaker">Miriam:</span> Mm-hmm (affirmative).

<span class="smashing-tv-host">Drew:</span> And "focus within" was proven very useful there until I didn’t have it and ended up writing a whole load of JavaScript to recreate what I’d achieved very simply with CSS before it.

<span class="smashing-tv-speaker">Miriam:</span> Yeah, the danger always with new selectors is how to handle the fallback.

<span class="smashing-tv-host">Drew:</span> One thing I’m really excited about is this new concept in CSS of aspect ratio. Are we going to be able to say goodbye to the 56% top padding hack?

<span class="smashing-tv-speaker">Miriam:</span> Oh, absolutely. I’m so excited to never use that hack again. I think that’s landing in browsers. I think it’s already available in some and should be coming to others soon. There seems to be a lot of excitement around that.

<span class="smashing-tv-host">Drew:</span> Definitely, it’s the classic problem, isn’t it, of having a video or something like that. You want to show it in like a 16 by 9 ratio, but you want to set the dimensions on it. But maybe it’s a 4 by 3 video and you have to figure out how to do it and get it to scale with the right-

<span class="smashing-tv-speaker">Miriam:</span> Right, and you want it to be responsive, you want it to fill a whole width, but then maintain its ratio. Yeah, the hacks for that aren’t great. I use one often that’s create a grid, position generated content with a padding top hack, and then absolute position the video itself. It’s just a lot to get it to work the way you want.

<span class="smashing-tv-host">Drew:</span> And presumably, that’s going to be much more performance for the layout engines to be able to deal with and-

<span class="smashing-tv-speaker">Miriam:</span> Right. And right away, it’s actually a reason to put width and height values back on to replaced elements like images, in particular, so that even before CSS loads, the browser can figure out what is the right ratio, the intrinsic ratio, even before the image loads and use that in the CSS. We used to strip all that out because we wanted percentages instead and now it’s good to put it back in.

<span class="smashing-tv-host">Drew:</span> Yes, I was going to say that when responsive web design came along, we stripped all those out. But I think we lost something in the process, didn’t we, of giving the browser that important bit of information about how much space to reserve?

<span class="smashing-tv-speaker">Miriam:</span> Yeah, and it ties in to what Jen Simmons has been talking about lately with intrinsic web design. The idea with responsive design was basically that we strip out any intrinsic sizing and we replace it with percentages. And now the tools that we have, flex and grid, are actually built to work with intrinsic sizes and it’s useful to put those all back in and we can override them still if we need to. But having those intrinsic sizes is useful and we want them.

<span class="smashing-tv-host">Drew:</span> Grid, you mentioned, I think sort of revolutionized the way we think about layout on the web. But it was always sort of tempered a little bit by the fact that we didn’t get subgrid at the same time. Remind us, if you will, what subgrid is all about and where are we now with support?

<span class="smashing-tv-speaker">Miriam:</span> Yeah. Grid establishes a grid parent and then all of its children layout on that grid. And subgrid allows you to nest those and say, "Okay, I want grandchildren to be part of the grandparent grid." Even if I have a DOM tree that’s quite a bit nested, I can bubble up elements into the parent grid, which is useful. But it’s particularly useful when you think about the fact that CSS in general and CSS Grid in particular does this back and forth of some parts of the layout are determined based on the available width of the container. They’re contextual, they’re outside-in. But then also, some parts of it are determined by the sizes of the children, the sizes of the contents, so we have this constant back and forth in CSS between whether the context is in control or whether the contents are in control of the layout. And often, they’re intertwined in very complex ways. What’s most interesting about subgrid is it would allow the contents of grid items to contribute back their sizing to the grandparent grid and it makes that back and forth between contents and context even more explicit.

<span class="smashing-tv-host">Drew:</span> Is that the similar problem that has been faced by container queries? Because you can’t really talk about the future of CSS and ask designers and developers what they want in CSS without two minutes in somebody saying, "Ah, container queries, that’s what we want." Is that a similar issue of this pushing and pulling of the two different context to figure out how much space there is?

<span class="smashing-tv-speaker">Miriam:</span> Yeah, they both are related to that context-content question. Subgrid doesn’t have to deal with quite the same problems. Subgrid actually works. It is actually able to pass those values both directions because you can’t change the contents based on the context. We sort of cut off that loop. And the problem with container queries has always been that there’s a potential infinite loop where if we allow the content to be styled based on its context explicitly, and you could say, "When I have less than 500 pixels available, make it 600 pixels wide." You could create this loop where then that size changes the size of the parent, that changes whether the container query applies and on and on forever. And if you’re in the Star Trek universe, the robot explodes. You get that infinite loop. The problem with container queries that we’ve had to solve is how do we cut off that loop.

<span class="smashing-tv-host">Drew:</span> Container queries is one of the CSS features that you’re one of the editors for, is that right?

<span class="smashing-tv-speaker">Miriam:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> So the general concept is like a media query, where we’re looking at the size of a viewport, I guess, and changing CSS based on it. Container queries are to do that, but looking at the size of a containing element. So I’m a hero image on a page, how much space have I got?

<span class="smashing-tv-speaker">Miriam:</span> Right. Or I’m a grid item in a track. How much space do I have in this track? Yeah.

<span class="smashing-tv-host">Drew:</span> It sounds very difficult to solve. Are we anywhere near a solution for container queries now?

<span class="smashing-tv-speaker">Miriam:</span> We are very near a solution now.

<span class="smashing-tv-host">Drew:</span> Hooray!

<span class="smashing-tv-speaker">Miriam:</span> There’s still edge cases that we haven’t resolved, but at this point, we’re prototyping to find those edge cases and see if we can solve all of them. But the prototypes we’ve played with so far surprisingly just work in the majority of cases, which has been so fun to see. But it’s a long history. It’s sort of that thing with... Like we get "is" because it’s halfway to nesting. And there’s been so much work over the last 10 years. What looks like the CSS Working Group not getting anywhere on container queries has actually been implementing all of the half steps we would need in order to get here. I came on board to help with this final push, but there’s been so much work establishing containment and all these other concepts that we’re now relying on to make container queries possible.

<span class="smashing-tv-host">Drew:</span> It’s really exciting. Is there any sort of timeline now that we might expect them to get into browsers?

<span class="smashing-tv-speaker">Miriam:</span> It’s hard to say exactly. Not all browsers announce their plans. Some more than others. It’s hard to say, but all of the browsers seem excited about the idea. There’s a working prototype in Chrome Canary right now that people can play with and we’re getting feedback through that to make changes. I’m working on the spec. I imagine dealing with some of the complexity in the edge cases. It will take some time for the spec to really solidify, but I think we have a fairly solid proposal overall and I hope that other browsers are going to start picking up on that soon. I know containment, as a half step, is already not implemented everywhere, but I know Igalia is working to help make sure that there’s cross-browser support of containment and that should make it easier for every browser to step up and do the container queries.

<span class="smashing-tv-host">Drew:</span> Igalia are an interesting case, aren’t they? They were involved in a lot of the implementation on Grid initially, is that right?

<span class="smashing-tv-speaker">Miriam:</span> Yes. I understand they were hired by Bloomberg or somebody that really wanted grids. Igalia is really interesting. They’re a company that contributes to all of the browsers.

<span class="smashing-tv-host">Drew:</span> They’re sort of an outlier, it seems. All the different parties that work on CSS, is mostly, as you’d expect, mostly browser vendors. But yes, they’re there as a sort of more independent developer, which is very interesting.

<span class="smashing-tv-speaker">Miriam:</span> A browser vendor vendor.

<span class="smashing-tv-host">Drew:</span> Yes. Definitely. Another thing I wanted to talk to you about is this concept that completely twisted my mind a little bit while I started to think about it. It’s this concept of cascade layers. I think a lot of developers might be familiar with the different aspects of the CSS cascade thing, specificity, source order, importance, origin. Are those the main ones? What are cascade layers? Is this another element of the cascade?

<span class="smashing-tv-speaker">Miriam:</span> Yeah. It is another element very much like those. I think often when we talk about the cascade, a lot of people mainly think of it as specificity. And other things get tied into that. People think of importance as a higher specificity, people think of source order as a lower specificity. That makes sense because, as authors, we spend most of our time in specificity.

<span class="smashing-tv-speaker">Miriam:</span> But these are separate things and importance is more directly tied to origins. This idea of where do styles come from. Do they come from authors like us or browsers, the default styles, or do they come from users? So three basic origins and those layer in different ways. And then importance is there to flip the order so that there’s some balance of control. We get to override everybody by default, but users and browsers can say, "No, this is important. I want control back." And they win.

<span class="smashing-tv-speaker">Miriam:</span> For us, importance acts sort of like a specificity layer because normal author styles and important author styles are right next to each other so it makes sense that we think of them that way. But I was looking at that and I was thinking specificity is this attempt to say... It’s a heuristic. That means it’s a smart guess. And the guess is based on we think the more narrowly targeted something is, probably the more you care about it. Probably. It’s a guess, it’s not going to be perfect, but it gets us partway. And that is somewhat true. The more narrowly we target something, probably the more we care about it so more targeted styles override less targeted styles.

<span class="smashing-tv-speaker">Miriam:</span> But it’s not always true. Sometimes that falls apart. And what happens is, there’s three layers of specificity. There’s id’s, there’s classes and attributes, and there there’s elements themselves. Of those three layers, we control one of them completely. Classes and attributes, we can do anything we want with them. They’re reusable, they’re customizable. That’s not true of either of the other two layers. Once things get complex, we often end up trying to do all of our cascade management in that single layer and then getting angry, throwing up our hands, and adding importance. That’s not ideal.

<span class="smashing-tv-speaker">Miriam:</span> And I was looking at origins because I was going to do some videos teaching the cascade in full, and I thought that’s actually pretty clever. We, as authors, often have styles that come from different places and represent different interests. And what if we could layer them in that same way that we can layer author styles, user styles, and browser styles. But instead, what if they’re... Here’s the design system, here’s the styles from components themselves, here’s the broad abstractions. And sometimes we have broad abstractions that are narrowly targeted and sometimes we have highly repeatable component utilities or something that need to have a lot of weight. What if we could explicitly put those into named layers?

<span class="smashing-tv-speaker">Miriam:</span> Jen Simmons encouraged me to submit that to the working group and they were excited about it and the spec has been moving very quickly. At first, we were all worried that we would end up in a z-index situation. Layer 999,000 something. And as soon as we started putting together the syntax, we found that that wasn’t hard to avoid. I’ve been really excited to see that coming together. I think it’s a great syntax that we have.

<span class="smashing-tv-host">Drew:</span> What form does the syntax take on, roughly? I know it’s difficult to mouth code, isn’t it?

<span class="smashing-tv-speaker">Miriam:</span> It’s an "@" rule called "@layer." There’s actually two approaches. You can also use, we’re adding a function to the "@import" syntax so you could import a style sheet into a layer, say, import Bootstrap into my framework layer. But you can also create or add to layers using the "@layer" rule. And it’s just "@layer" and then the name of the layer. And layers get stacked in the order they’re first introduced, which means that even if you’re bringing in style sheets from all over and you don’t know what order they’re going to load, you can, at the top of your document, say, "Here are the layers that I’m planning to load, and here’s the order that I want them in." And then, later, when you’re actually adding styles into those layers, they get moved into the original order. It’s also a way of saying, "Ignore the source order here. I want to be able to load my styles in any order and still control how they should override each other."

<span class="smashing-tv-host">Drew:</span> And in its own way, having a list, at the top, of all these different layers is self-documenting as well, because anybody who comes to that style sheet can see the order of all the layers.

<span class="smashing-tv-speaker">Miriam:</span> And it also means that, say, Bootstrap could go off and use a lot of internal layers and you could pull those layers in from Bootstrap. They control how their own layers relate to each other, but you could control how those different layers from Bootstrap relate to your document. So when should Bootstrap win over your layers and when should your layers win over Bootstrap? And you can start to get very explicit about those things without ever throwing the "important" flag.

<span class="smashing-tv-host">Drew:</span> Would those layers from an imported style sheet, if that had its own layers, would they all just mix in at the point that the style sheet was added?

<span class="smashing-tv-speaker">Miriam:</span> By default, unless you’ve defined somewhere else previously how to order those layers. So still, your initial layer ordering would take priority.

<span class="smashing-tv-host">Drew:</span> If Bootstrap, for example, had documented their layers, would you be able to target a particular one and put that into your layer stack to change it?

<span class="smashing-tv-speaker">Miriam:</span> Yes.

<span class="smashing-tv-host">Drew:</span> So it’s not an encapsulated thing that all moves in one go. You can actually pull it apart and...

<span class="smashing-tv-speaker">Miriam:</span> It would depend... We’ve got several ideas here. We’ve built in the ability to nest layers that seemed important if you were going to be able to import into a layer. You would have to then say, "Okay, I’ve imported all of Bootstrap into a layer called frameworks," but they already had a layer called defaults and a layer called widgets or whatever. So then I want a way to target that sublayer. I want to be able to say "frameworks widgets" or "frameworks defaults" and have that be a layer. So we have a syntax for that. We think that all of those would have to be grouped together. You couldn’t pull them apart if they’re sublayered. But if Bootstrap was giving you all those as top level layers, you could pull them in at the top level, not group them. So we have ways of doing both grouping or splitting apart.

<span class="smashing-tv-host">Drew:</span> And the fact that you can specify a layer that something is imported into that doesn’t require any third-party script to know about layers or have implemented it, presumably, it just pulls that in at the layer you specify.

<span class="smashing-tv-speaker">Miriam:</span> Right.

<span class="smashing-tv-host">Drew:</span> That would help with things pretty much like Bootstrap and that sort of thing, but also just with the third party widgets you’re then trying to fight with specificity to be able to re-style them and they’re using id’s to style things and you want to change the theme color or something and you having to write these very specific... You can just change the layer order to make sure that your layers would win in the cascade.

<span class="smashing-tv-speaker">Miriam:</span> Yup. That’s exactly right. The big danger here is backwards compatibility. It’s going to be a rough transition in some sense. I can’t imagine any way of updating the cascade or adding the sort of explicit rules to the cascade without some backwards compatibility issues. But older browsers are going to ignore anything inside a layer rule. So that’s dangerous. This is going to take some time. I think we’ll get it implemented fairly quickly, but then it will still take some time before people are comfortable using it. And there are ways to polyfill it particularly using "is." The "is selector gives us a weird little polyfill that we’ll be able to write. So people will be able to use the syntax and polyfill it, generate backwards-compatible CSS, but there will be some issues there in the transition.

<span class="smashing-tv-host">Drew:</span> Presumably. And you’re backwards-compatible to browsers that support "is."

<span class="smashing-tv-speaker">Miriam:</span> That’s right. So it gets us a little farther, but not... It’s not going to get us IE 11.

<span class="smashing-tv-host">Drew:</span> No. But then that’s not necessarily a bad thing.

<span class="smashing-tv-speaker">Miriam:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> It feels like a scoping mechanism but it’s not a scoping mechanism, is it, layers? It’s different because a scope is a separate thing and is actually a separate CSS feature that there’s a draft in the works for, is that right?

<span class="smashing-tv-speaker">Miriam:</span> Yeah, that’s another one that I’m working on. I would say, as with anything in the cascade, they have sort of an overlap. Layers overlap with specificity and both of them overlap with scope.

<span class="smashing-tv-speaker">Miriam:</span> The idea with scope, what I’ve focused on, is the way that a lot of the JavaScript tools do it right now. They create a scope by generating a unique class name, and then they append that class name to everything they consider within a scope. So if you’re using "view" that’s everything within a view component template or something. So they apply it to every element in the HTML that’s in the scope and then they also apply it to every single one of your selectors. It takes a lot of JavaScript managing and writing these weird strings of unique ids.

<span class="smashing-tv-speaker">Miriam:</span> But we’ve taken the same idea of being able to declare a scope using an "@scope" rule that declares not just the root of the scope, not just this component, but also the lower boundaries of that scope. Nicole Sullivan has called this "donut scope", the idea that some components have other components inside of them and the scope only goes from the outer boundaries to that inner hole and then other things can go in that hole. So we have this "@scope" rule that allows you to declare both a root selector and then say "to" and declare any number of lower boundaries. So in a tab component it might be "scope tabs to tab contents" or something so you’re not styling inside of the content of any one tab. You’re only scoping between the outer box and that inner box that’s going to hold all the contents.

<span class="smashing-tv-host">Drew:</span> So it’s like saying, "At this point, stop the inheritance."

<span class="smashing-tv-speaker">Miriam:</span> Not exactly, because it doesn’t actually cut off inheritance. The way I’m proposing it, what it does is it just narrows the range of targeted elements from a selector. So any selector you put inside of the scope rule will only target something that is between the root and the lower boundaries and it’s a targeting issue there. There is one other part of it that we’re still discussing exactly how it should work where, the way I’ve proposed it, if we have two scopes, let’s call them theme scopes. Let’s say we have a light theme and a dark theme and we nest them. Given both of those scopes, both of them have a link style, both of those link styles have the same specificity, they’re both in scopes. We want the closer scope to win in that case. If I’ve got nested light and dark and light and dark, we want the closest ancestor to win. So we do have that concept of proximity of a scope.

<span class="smashing-tv-host">Drew:</span> That’s fascinating. So scopes are the scope of the targeting of a selector. Now, I mentioned this idea of inheritance. Is there anything in CSS that might be coming or might exist already that I didn’t know about that will stop inheritance in a nice way without doing a massive reset?

<span class="smashing-tv-speaker">Miriam:</span> Well, really, the way to stop inheritance is with some sort of reset. Layers would actually give you an interesting way to think about that because we have this idea of... There’s already a "revert" rule. We have an "all" property, which sets all properties, every CSS property, and we have a "revert" rule, which reverts to the previous origin. So you can say "all revert" and that would stop inheritance. That would revert all of the properties back to their browser default. So you can do that already.

<span class="smashing-tv-speaker">Miriam:</span> And now we’re adding "revert layer", which would allow you to say, "Okay I’m in the components layer. Revert all of the properties back to the defaults layer." So I don’t want to go the whole way back to the browser defaults, I want to go back to my own defaults. We will be adding something like that in layers that could work that way.

<span class="smashing-tv-speaker">Miriam:</span> But a little bit, in order to stop inheritance, in order to stop things from getting in, I think that belongs more in the realm of shadow DOM encapsulation. That idea of drawing hard boundaries in the DOM itself. I’ve tried to step away from that with my scope proposal. The shadow DOM already is handling that. I wanted to do something more CSS-focused, more... We can have multiple overlapping scopes that target different selectors and they’re not drawn into the DOM as hard lines.

<span class="smashing-tv-host">Drew:</span> Leave it to someone else, to shadow DOM. What stage are these drafts at, the cascade layers and scope? How far along the process are they?

<span class="smashing-tv-speaker">Miriam:</span> Cascade layers, there’s a few people who want to reconsider the naming of it, but otherwise, the spec is fairly stable and there’s no other current issues open. Hopefully, that will be moving to candidate recommendation soon. I expect browsers will at least start implementing it later this year. That one is the farthest along because for browsers, it’s very much the easiest to conceptualize and implement, even if it may take some time for authors to make the transition. That one is very far along and coming quickly.

<span class="smashing-tv-speaker">Miriam:</span> Container queries are next in line, I would say. Since we already have a working prototype, that’s going to help a lot. But actually defining all of the spec edge cases... Specs these days are, in large part, "How should this fail?" That’s what we got wrong with CSS 1. We didn’t define the failures and so browsers failed differently and that was unexpected and hard to work with. Specs are a lot about dealing with those failures and container queries are going to have a lot of those edge cases that we have to think through and deal with because we’re trying to solve weird looping problems. It’s hard to say on that one, because we both have a working prototype ahead of any of the others, but also it’s going to be a little harder to spec out. I think there’s a lot of interest, I think people will start implementing soon, but I don’t know exactly how long it’ll take.

<span class="smashing-tv-speaker">Miriam:</span> Scope is the farthest behind of those three. We have a rough proposal, we have a lot of interest in it, but very little agreement on all the details yet. So that one is still very much in flux and we’ll see where it goes.

<span class="smashing-tv-host">Drew:</span> I think it’s amazing, the level of thought and work the CSS Working Group are putting into new features and the future of CSS. It’s all very exciting and I’m sure we’re all very grateful for the clever folks like yourself who spend time thinking about it so that we get new tools to use. I’ve been learning all about what’s coming down the pike in CSS, what have you been learning about lately, Miriam?

<span class="smashing-tv-speaker">Miriam:</span> A big part of what I’m learning is how to work on the spec process. It’s really interesting and I mean the working group is very welcoming and a lot of people there have helped me find my feet and learn how to think about these things from a spec perspective. But I have a long ways to go on that and learning exactly how to write the spec language and all of that. That’s a lot in my mind.

<span class="smashing-tv-speaker">Miriam:</span> Meanwhile, I’m still playing with grids and playing with custom properties. And while I learned both of those, I don’t know, five years ago, there’s always something new there to discover and play with, so I feel like I’m never done learning them.

<span class="smashing-tv-host">Drew:</span> Yup. I feel very much the same. I feel like I’m always a beginner when it comes to a lot of CSS.

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Miriam, you can find her on Twitter where she’s @TerribleMia, and her personal website is miriamsuzanne.com. Thanks for joining us today, Miriam. Do you have any parting words?

<span class="smashing-tv-speaker">Miriam:</span> Thank you, it’s great chatting with you.

{{< signature "il" >}}