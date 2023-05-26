---
title: 'Smashing Podcast Episode 19 With Andy Bell: What Is CUBE CSS?'
slug: smashing-podcast-episode-19
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d9af01a-86dc-43ee-8ff0-cb81d50cf681/smashing-podcast-episode-19.png
date: 2020-06-30T05:00:00.000Z
summary: >-
  We’re talking about CUBE CSS. What is it, and how does it differ from approaches such as BEM, SMACSS, and OOCSS? Drew McLellan talks to its creator, Andy Bell, to find out.
description: >-
  We’re talking about CUBE CSS. What is it, and how does it differ from approaches such as BEM, SMACSS, and OOCSS? Drew McLellan talks to its creator, Andy Bell, to find out.
categories:
  - Smashing Podcast
  - CSS
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

Today, we’re talking about CUBE CSS. What is it, and how does it differ from approaches such as BEM, SMACSS, and OOCSS? I spoke to its creator, Andy Bell, to find out.

<iframe src="https://share.transistor.fm/e/48300fa4/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [CUBE CSS](https://piccalil.li/cube-css/)
- [Piccalilli](https://piccalil.li)
- [Learn Eleventy From Scratch](https://piccalil.li/course/learn-eleventy-from-scratch/) - save 40%!
- [Andy Bell](https://twitter.com/hankchizljaw) and [Piccalilli](https://twitter.com/piccalilli_) on Twitter

**Note**: *Listeners of the Smashing Podcast can save a whopping 40% on Andy’s [Learn Eleventy From Scratch](https://piccalil.li/course/learn-eleventy-from-scratch/) course using the code `SMASHINGPOD`.*

### Weekly Update

- “[What Vitruvius Can Teach Us About Web Design](https://www.smashingmagazine.com/2020/06/vitruvius-web-design/)”  
*by Frederick O’Brien*
- “[An Introduction To SWR: React Hooks For Remote Data Fetching](https://www.smashingmagazine.com/2020/06/introduction-swr-react-hooks-remote-data-fetching/)”  
*by Ibrahima Ndaw*
- “[How Web Designers Can Help Restaurants Move Into Digital Experiences](https://www.smashingmagazine.com/2020/06/web-designers-help-restaurants-digital-experiences/)”  
*by Suzanne Scacca*
- “[A Practical Guide To Testing React Applications With Jest](https://www.smashingmagazine.com/2020/06/practical-guide-testing-react-applications-jest/)”  
*by Adeneye David Abiodun*
- “[Django Highlights: Wrangling Static Assets And Media Files (Part 4)](https://www.smashingmagazine.com/2020/06/django-highlights-wrangling-static-assets-media-files-part-4/)”  
*by Philip Kiely*

## Transcript

<p><a href="https://twitter.com/hankchizljaw"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1bed031-d5bd-4aaf-884e-b0f4a1e20d84/andy-bell-200x200.jpg" width="200" height="200" alt="Photo of Andy Bell" /></a><span class="smashing-tv-host">Drew McLellan:</span> He is an educator and freelance web designer based in the U.K. and has worked in the designer web industries for well over a decade. In that time he’s worked with some of the largest organizations in the world, like Harley-Davidson, BSkyB, Unilever, Oracle, and the NHS. Alongside Heydon Pickering, he’s the co-author of Every Layout, as well as running Front-End Challenges Club which is focused on teaching front-end development best practice via short, fun challenges.</p>

<span class="smashing-tv-host">Drew:</span> His latest venture is Piccalilli, a website newsletter with tutorials and courses to help you level up as a front-end developer and designer. So we know he’s an experienced developer and educator, but did you know he was the first person allowed to compete at Crufts with a panda?

<span class="smashing-tv-host">Drew:</span> My Smashing friends, please welcome, Andy Bell. Hi, Andy, how are you?

<span class="smashing-tv-speaker">Andy Bell:</span> I’m smashing, thanks. How are you?

<span class="smashing-tv-host">Drew:</span> I’m very good, thank you very much. Now I wanted to talk to you today about something that you posted on your site, Piccalilli, about a CSS methodology that you’ve developed for yourself over recent years. First of all, I guess we should probably explore what we mean by a CSS methodology because that could mean different things to different people. So when you think of the CSS methodology, what is it to you?

<span class="smashing-tv-speaker">Andy:</span> That’s a good, hard question to start with, Drew. Appreciate that, thank you!

<span class="smashing-tv-host">Drew:</span> Welcome!

<span class="smashing-tv-speaker">Andy:</span> It’s a tricky one. So, for context, I’ve used BEM for a long time, and that is Block Element Modifier. That’s been around for a long time. The way that I look at a CSS methodology is, it’s not a framework, it’s an organization structure. That’s how I like to see it. It’s like a process almost. It’s like you’ve got a problem that you need to solve with CSS and you use the methodology to solve it for you and keep things predictable and organized. BEM’s just legendary for that because it’s been wildly successful.

<span class="smashing-tv-speaker">Andy:</span> Then you could almost qualify things like the style components and that sort of thing. You can almost say that they’re methodology orientated even though they’re a bit more framework entwined, but still, it’s a methodology of breaking things into tiny molecules. So essentially that’s what I’m trying to do with CUBE CSS as well. A thinking structure, I think I described it as.

<span class="smashing-tv-host">Drew:</span> So it’s an application of process for how you architect and you write CSS, and it’s not so much anything that’s based on tools or any other sort of technology, it’s just a sort of work flow. So there’s lots of different approaches out there. You mentioned BEM. There’s SMACSS, OOCSS, Atomic CSS. And then you’ve got these sort of unusual lovechild approaches like ABEM. Have you seen that one?

<span class="smashing-tv-speaker">Andy:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> Why publish your own?

<span class="smashing-tv-speaker">Andy:</span> Yeah, yeah. Why make your own? That’s a very good question. I think those who know me well know I like to sail against the tide a lot. It’s mainly because I tend to do lots of varied projects as well, in varied teams. So it’s very hard, I’ve found, to work with BEM with a traditional developer because they’re used to using CSS for what CSS is all about: the cascade, et cetera, and that’s why I sort of stole that from the language.

<span class="smashing-tv-speaker">Andy:</span> On the other flip side is that less structured methodologies, it’s harder to work with a programmer, JS sort of person because they like structure and organization and small components, which is understandable working with the language that they work in.

<span class="smashing-tv-speaker">Andy:</span> So I found myself in these positions where I was working with different types of people, different types of projects where one methodology wasn’t quite working. Over the years, I’ve just been playing around with this idea of how things go, and then there’s the stuff me and Heydon did, Every Layout, which sort of enforced the big part of it, which is the C, the composition part, and then I’ve just sort of evolved it very rapidly over the last six months.

<span class="smashing-tv-speaker">Andy:</span> The only reason I wrote an article about it was because I was just doing this course and I thought I’d better write some supplementary material to go with it so people understand it, and it’s absolutely blown up. So maybe we’re not over methodologies quite yet, Drew.

<span class="smashing-tv-host">Drew:</span> So the course material that you’ve been putting together actually uses CUBE CSS as its methodology, does it?

<span class="smashing-tv-speaker">Andy:</span> Yeah. So a good 50% of the course is actually front-end, even though it’s a course unlimited. It’s so, so deeply entwined in the way that we build the front-end that I couldn’t just say, "Oh, by the way, this is how I write a nice CSS," and then leave it. I know people like to get into the detail, so I was like, what I’ll do is, I’ll write this post that’s really long and really detailed and then if someone wants to skill up and really understand what we’re doing, then they can do, and the rest is from there. And here we are today, Drew, sitting and chatting about it.

<span class="smashing-tv-host">Drew:</span> So if somebody already understands BEM and is maybe already using BEM, as an example, because that’s probably one of the widest adopted methodologies, isn’t it? So if they’ve already got an understanding of BEM and they’re coming to CUBE, is that something that they would find easy to adopt? Are there many similarities or is it completely different?

<span class="smashing-tv-speaker">Andy:</span> Yeah. I’d say going from BEM to CUBE is probably a smooth transition, especially the way I like to still write the CSS for CUBE. So the majority of stuff’s happening at a higher level. So it’s happening at the cascade level and it’s happening global CSS, using the utilities to do a lot of the stuff. But when you come into the nuts and bolts of it, it’s very BEM-like components, blocks and elements. The only thing that’s sort of different from BEM is, instead of having modifiers, we use this thing called exceptions instead which is, instead of using CSS classes, it turns to data attributes, which I think gives a nice bit of separation and a real exception, which is what a modifier should be.

<span class="smashing-tv-speaker">Andy:</span> Part of the reason why I’ve sort of sailed away from BEM was because I found the way I was working with it, especially in design systems, was modifiers were dominated and it became a problem because it was like, what is the role of my block at this point? Because if I’m modifying it to the point where it’s unrecognizable regularly, then is this methodology still working how it’s supposed to work?

<span class="smashing-tv-speaker">Andy:</span> Then there’s the whole design token stuff, the stuff that Jina did with the Lightning Design System which we’ve all started adopting now. The utility class stuff really started to make sense with that approach. So I just sort of smushed all the things I like about other people’s work and slotted into my own instead.

<span class="smashing-tv-host">Drew:</span> You talk about with BEM, the sort of modifier approach kind of getting out of control. Was that one of the main pain points with BEM that CUBE tries to address?

<span class="smashing-tv-speaker">Andy:</span> Yeah, absolutely. I do like the modifier approach with BEM, it does make sense. What I like about BEM is something that I still do, is the double underscore for an element, and then there’s the double dash for a modifier. I like that way of organizing things. It was just a case of okay, well, a lot of the modifiers I can actually account for with utility classes and then the other bits...

<span class="smashing-tv-speaker">Andy:</span> So the example I use in the article is, imagine you’ve got a card and then the card is flipped, so the content appears before the image. So then that makes sense, to see display: flex and then you reverse it, reverse the order. That makes sense, to have an exception rule for that because it’s an exception of the card’s default state, and that’s how I like to see it. It’s like an affected state on that component, is what an exception is, and that makes sense.

<span class="smashing-tv-speaker">Andy:</span> With a lot of the stuff that I’ve done more recently, the modern front-end stack with reactive JavaScript, there’s a lot of state changing and it’s makes sense to handle it appropriately between CSS and JavaScript because they are becoming more and more entwined with each other, whether you like it or not. It’s a common language for them. As you can see by my face, very much not, but there you go. You’re probably thinking, "Actually, I’ve been working with react quite a lot recently, so I’m the other way round." So I can see that as well.

<span class="smashing-tv-host">Drew:</span> So let’s get into CUBE then. So CUBE stands for Composition Utility Block Exception. Is that right?

<span class="smashing-tv-speaker">Andy:</span> Yeah. That’s the one.

<span class="smashing-tv-host">Drew:</span> What on Earth does that mean?

<span class="smashing-tv-speaker">Andy:</span> Oh, mate, you should have heard it before! I was doing a talk last year. I did a talk, and it was called Keeping it Simple with CSS that scales, and in there I sort of introduced an earlier version of it called CBEUT, which was Cascade Block Element Utility Token. It was rubbish. I hated the name of it. I did it a couple of times, this talk last year, and I really didn’t like the name. Then when I came to doing this stuff this year, I thought, "I really need to think about what it actually is and what it’s called." I think CUBE is a little less rubbish. I think that’s the best way I can describe it.

<span class="smashing-tv-speaker">Andy:</span> But then, names are always rubbish for these things, aren’t they? I mean, like BEM, what a rubbish name that is! But we all do it. Look at Jamstack: that’s a terrible name as well, isn’t it?

<span class="smashing-tv-host">Drew:</span> My lips are sealed!

<span class="smashing-tv-speaker">Andy:</span> Your boss is going, "What?" It’s true. It’s just the way it is, isn’t it, in our industry.

<span class="smashing-tv-host">Drew:</span> It seems that a lot of the CSS methodologies try and work around some of the features of CSS, things like the cascade. My understanding from what I read is, CUBE tries to make use of those sort of features and properties of CSS.

<span class="smashing-tv-speaker">Andy:</span> Yeah. A good analogy for it is SCSS, like Sass, is an extension of the natural CSS language, isn’t it? You’re pretty much right in CSS still. So CUBE CSS is like that. So it’s an extension of CSS. So we should still write CSS, as CSS should... well, it’s supposed to be written. Let’s be honest, that how it’s supposed to be written, is the name gives it away: Cascading Style Sheets. So it’s embracing that again because what I’ve found is that I’ve gone all the way down to the micro-optimization level. I’ve been down the path that I see a lot of people going down recently where... and I’ve mentioned this in the article as well, where I can see... there’s some evidence of it recently. I’ve spotted people have been creating spacer components and stuff like that, and I understand that problem, I’ve been in that situation.

<span class="smashing-tv-speaker">Andy:</span> The way I fixed it was, instead of drilling down and trying to micro-optimize, I actually started thinking about things on a compositional level instead because it doesn’t matter how small your components are, at some point they’re going to be pages, they’re going to be views. You cannot avoid that, that’s how it’s going to be. So instead of trying to say, "Right, I need these tiny little helpers to do this layout," you say, "Right, I’ve got a contact page view, or a product page view, and that’s a skeletal layout composition. Then inside of that I can slot whatever components I want in there." We’ve got things like Grid and Flexbox now which make that much more achievable, and you can essentially put whatever you want inside of the skeletal layout, it doesn’t matter. Then the components should, at that point, behave how you want them to behave, with or without container queries.

<span class="smashing-tv-host">Drew:</span> This is the composition part of CUBE where you’re looking at things at more of a macro level, looking at how components can be composed into a view to create the sort of pages that you need to create for a site or an app or what have you.

<span class="smashing-tv-speaker">Andy:</span> So it’s creating rules, essentially. It’s like guidance. It’s trying to get guidelines for something. It’s not like a strict rules, like, you should do this, you should do that. That’s essentially what you’re doing with the browser, with this methodology, is you’re saying... you’re not forcing it to do anything. You’re saying, "Look, ideally, if you could lay it out like this, that would be great, but I understand that that might not be the case so here’s some bounds and some upper and lower levels that we can work with. Do what you can, and cheers." Then you just chuck some components at it and let it just do what it does. You add enough control in there for it to not look rubbish.

<span class="smashing-tv-speaker">Andy:</span> So a good example would see... we do a layout in Every Layout called the switcher, which essentially will in-line items until a certain point where the calculation that works out how wide it should will just stack them on top of each other. But because we add margin to the in-line and the block, it works, regardless of what the state of it is, it still looks fine. That’s the idea, is that we’re not telling the browser to say, "You must layer this three column grid out." We’re saying, "If you can layer a three column grid out, do it. Otherwise, just stack and space instead." So it’s that sort of methodology, of letting the browser do its job really.

<span class="smashing-tv-host">Drew:</span> Many of the different approaches that have come along for CSS over the last few years have very much focused on the component level of dealing with everything like it’s a component. CUBE doesn’t downplay that component aspect so much, it just gives this extra concept over the top of taking those components and composing them into bigger layouts, rather than just saying the layout’s just another component.

<span class="smashing-tv-speaker">Andy:</span> Yeah, that’s a good point, yeah. I think the thing to say about components is they’re important, especially in modern front-end stuff. We do a lot of component stuff, system stuff. But the way I see a component is, it’s a collection of rules that extend what’s already been done.

<span class="smashing-tv-speaker">Andy:</span> The point I make in the article is, by the time you get down to the block level, most of your styling has actually been done, and really what your component is doing is dotting the Is and crossing the Ts and it’s saying, "Right, in this context..." So for a card, for example, make the image have a minimum height of X, and add a bit of padding here. Do this, that and the other. Put a button here. It’s just sort of additional rules on top of what’s already been inherited from the rest of the CSS. I think that’s probably the best way to describe it.

<span class="smashing-tv-speaker">Andy:</span> Whereas in BEM, the component is the source of truth. Until you put that class on the element, nothing has been applied at that point, and that method works. I just found I wrote more CSS by doing that, and more repetitive CSS, which I don’t like doing.

<span class="smashing-tv-host">Drew:</span> Would you consider the typography and the colors and the vertical rhythms, spacing, and all of that, is all that part of the idea of composition in this model?

<span class="smashing-tv-speaker">Andy:</span> Yeah. In a global CSS, yeah, absolutely. The vertical rhythm especially, and the flow. We did an article on that at 24 ways, didn’t we, a couple of years ago, the flow and rhythm component. That was a sort of abstract from this approach as well, where you set a base component which essentially uses the lobotomized owl selector. I don’t know how I’m going to describe that on the radio, but we will. We’ll just put, I think, in the show notes about the Heydon article or something. But essentially that, it selects child elements... sorry, sibling elements.

<span class="smashing-tv-speaker">Andy:</span> So it says, "Right, every element that follows element X have margin top of CSS costs and property value," and then the beauty of that is then you can set that CSS custom property value on a compositional context as well. So you can say, "Right, in this component, if there’s some flow on the go, we’ll set flow space to actually be two rem because we want it to be nice and beefy, the wide space." Then in another one you might say, "Actually, I want flow space to be half a rem because I want it to be tight." This is all happening, all the control is coming from a higher level and then what you’re doing is, you’re adding contextual overrides rather than reinventing it each time, reinventing the same thing over and over again.

<span class="smashing-tv-host">Drew:</span> So that’s the C, Composition. Next we’ve got U, which is Utility. So what do we mean by utility?

<span class="smashing-tv-speaker">Andy:</span> So it’s a class that does one job, and it does it really well. That could be an implementation of a design token which... it’s an abstract of properties. Usually it’s colors or typography styles, sizing, and rules like that. The idea is you generate utility classes that apply those. So you’ve got a utility that will apply background primary, which is like the primary color, and then color primary, which is the text color. Then you might generate some spacing tokens for marginal padding, and all those sorts of things. They just do one job. They just add that one spacing rule, that one color rule, and that’s it.

<span class="smashing-tv-speaker">Andy:</span> But then you’ve got other utilities as well. So a good example is a wrapper utility. What that will do is, it will put a maximum width on an element and then it will put left and right auto margin to sit it in the middle of the thing. So it’s just got one job, and it’s just doing it efficiently and well.

<span class="smashing-tv-speaker">Andy:</span> So you’ve got your global styles, you’ve done a lot of your typography settings and a lot of your flooring space. Your composition’s then giving context and layout. Then utilities are applying tokens directly to elements to give them those styling that you need. So like a heading, for example, you’re saying, "I want this to be this size and I want it to have this lead in, and I want it to have this measure." Then at that point... this is what I was saying about the blocks... then you go further down the stack, and you’ve already done most of the work at the point.

<span class="smashing-tv-speaker">Andy:</span> So they give you this really efficient way of working, and because HTML sort of streams down the pipe as well, it’s really nice to abstract the workload onto HTML rather than CSS as well, I’ve found. I used to really get into utility classes, like in this sort of old curmudgeon style of, "Oh, separation of concerns," but I actually think it’s a really decent way of working. I mention in the article that I actually like Tailwind CSS. I think it does work, and I really like using it for product typing because I can really put something out really quick. But I think it just goes a little bit too far, does Tailwind, whereas I like to rain it in when it goes beyond just applying a single rule on a class. So that’s it, I think. Do you?

<span class="smashing-tv-host">Drew:</span> So, yeah, you talk in the article a lot about design tokens, which is something that we’ve talked about on the Smashing Podcast with Jina Anne back in episode three, I think it was. So it sounds like design tokens are a really fundamental aspect.

<span class="smashing-tv-speaker">Andy:</span> Yeah. Oh, God, yeah. I remember so vividly when Jina was doing the Lightning Design System stuff because I was building a design system at the time, or something that resembled a design system, and we were struggling to get executive approval of it. When the Lightning Design System came out, I literally just sent them link after link and I said, "This is what we’re doing. We’re building a design system. This is what Salesforce are currently using it for." I remember her work at the time actually helped me to get stuff through the door.

<span class="smashing-tv-speaker">Andy:</span> Then the design token stuff has always stuck with me as being a really good way of applying these rules. Because I’m a designer by trade, so I can just sort of see that organization and the ability to organize and create a single source of truth being really useful because it’s something we’ve not really had in digital design, especially in the Adobe era of working with Photoshop and stuff, we just didn’t have that luxury. We had it in print with the Pantone Book but we didn’t have it in digital with random hex codes all over the shop.

<span class="smashing-tv-speaker">Andy:</span> So it’s just great. I love that level of control. Actually, I think it aids in creativity because you’re not thinking about unimportant stuff anymore, you’re just thinking about what you’re doing with it.

<span class="smashing-tv-host">Drew:</span> Does the implementation of those design tokens matter particularly with the approach? Is it always CSS custom properties?

<span class="smashing-tv-speaker">Andy:</span> I think that’s a really important point with CUBE. Some of the responses I’ve had, people have struggled with this a little bit. There’s no mention of technology in it whatsoever. The only technology that’s consistent is CSS. You can do it however you want. You could do all this with whatever CSS and JS things people are doing now, or you could it with just Vanilla CSS. You could do it with Sass. I do it with Sass. Less, if that’s what you’re still doing. All these available technologies, post CSS, all these things. You can do however you want to do it, it doesn’t matter.

<span class="smashing-tv-speaker">Andy:</span> The idea is that if you follow those sort of constructs, you’ll be fine. That’s the idea behind it. It’s a very loose and not strict as some of the methodologies are. I’ve seen it with BEM especially, people get really ingrained in the principles of BEM to the point where it’s like you’re not even solving the problem anymore. I think that you’ve got to be flexible. I said it in this talk last year. I was like, "If you stick to your guns too tightly, you can actually cause problems for yourself in the long run because you try and follow a certain path, and you know it’s not working anymore." You should always be flexible and work with a system rather than working to the letter to it.

<span class="smashing-tv-host">Drew:</span> So the B, the B is Block. You’ve talked about this idea, that by the time you get down to the block level, most of everything should be in place, and then the block level styling is only really concerned with the actual very detail of a particular component. Generally, is the concept of a block similar to what people will be familiar with?

<span class="smashing-tv-speaker">Andy:</span> Oh, absolutely, yeah. So imagine your BEM component and take all the visual stuff out of it, and that’s what you’re left with, essentially, the block. This is what I struggled to articulate when I first started thinking of this methodology. A block is actually really a C, it’s a composition, but that makes it really difficult because you’re into recursive territory there and I think people’s brains would explode. But really that’s what a block is, it’s actually another compositional layer but more of a sort of strict context, so like your card, your button, your carousel, if that’s what you like doing still, and all that sort of stuff.

<span class="smashing-tv-speaker">Andy:</span> It’s like a specific thing, a component, and then inside of there you’re setting specific rules for it to follow, really ignoring the rest so you’re not... You might apply tokens in the blocks, and I do do that still, but really it’s more layout orientated, is a block, as far as I work with them, or at least taking the token and applying it in a specific way, like a button hover status, stuff like that. So really your block should be tiny by the time you get down to them, they shouldn’t be really doing much at all.

<span class="smashing-tv-host">Drew:</span> So it could be as small as a hyperlink.

<span class="smashing-tv-speaker">Andy:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> But it could also be a compound collection of other blocks?

<span class="smashing-tv-speaker">Andy:</span> Yeah. Like a module sort of thing. You could definitely do that. Because, again, that goes back to the sort of compositional aspect of it, is that whatever goes in it shouldn’t matter. The good example of that is like the card. So the content of a card is, say, like a heading, a summary and a button. You shouldn’t really be specifically targeting those three elements. You should be saying, "Look, anything that happens to find itself in content, have some flow rules in there and have some sort of compositional layout rules," and then it doesn’t matter what you put in there. You might decide that you want to put an image in that content thing and it should just work, it should just look fine.

<span class="smashing-tv-speaker">Andy:</span> That’s the whole point of working with CSS. It’s a very forgiving way of working with CSS. You’re making your life a lot easier by being less rigid because when stuff accidentally finds itself in something, which it will, it doesn’t look horrific as it could do if you were being more specific about things, is what I’ve found.

<span class="smashing-tv-host">Drew:</span> I definitely need a lot of forgiveness around my CSS!

<span class="smashing-tv-speaker">Andy:</span> I know you do!

<span class="smashing-tv-host">Drew:</span> Cheers! So that’s the B. The last thing is E: E is Exception. Now we’re not talking about error messages, are we?

<span class="smashing-tv-speaker">Andy:</span> No, no. It’s a sort of-

<span class="smashing-tv-host">Drew:</span> We’re not talking about JavaScript exceptions.

<span class="smashing-tv-speaker">Andy:</span> Yeah, yeah. There should be none of that at this point. I should hope not anyway, otherwise you really are in the woods at that point: I don’t think I’m going to be able to help you! The whole idea of this is... so you’ve created the context with your block, and an exception is exactly that, it’s like an exception to the rule: so a flipped card, or it might be a ghost button. So you know those buttons that have just got a border and a transparent background? That would be an exception because a button has probably got a solid background color and then the label color. So it’s creating a sort of distinct state of variation.

<span class="smashing-tv-speaker">Andy:</span> The reason why I do this with data attributes instead of classes, and the reason why that is is because a) I think it’s nice to have a distinction. So when you’re scanning through lots of HTML, you can see data, hyphen something, you’re like, "Right, okay, something has definitely changed on this element." The other thing is that it’s very nice to give JavaScript access to that state, and vice versa as well. So I really like applying state with data attributes in JavaScript. I think that is essentially what they’re for, a sort of communication layer. The harmony between them seems to work really well.

<span class="smashing-tv-speaker">Andy:</span> So a good example is, say you’ve got a status message and then JavaScript will add data state is either success, error or information, or something. You can then hook into that with your exception styles in CSS. So you know that’s an exception of the status component and it’s going against its default state. So it’s just a really handy way of working with things. It’s predictable on both ends: it’s predictable on the CSS end, and it’s predictable on the JavaScript end as well.

<span class="smashing-tv-host">Drew:</span> I guess it’s quite nice that something that class names don’t give you is a property and value. So if you want to have something like that which is the state, and it can either be success or failure or warning or what have you, you can specifically address that state property and flip its value. Whereas with a big long list of class names, if you’re manipulating that in JavaScript, for example, you’re going to have to look at each one of them and add that business logic in there that says, "I can only set one of these," and what happens if two of those classes are applied to the same element? You can’t get that with a data attribute, it only has one value.

<span class="smashing-tv-speaker">Andy:</span> Yeah. That’s a good way of saying that, yeah. It is very helpful, I’ve found, to work like that.

<span class="smashing-tv-host">Drew:</span> That’s quite interesting. I don’t think I’ve seen any other methodologies that take that approach. Is that completely unique to CUBE, doing that?

<span class="smashing-tv-speaker">Andy:</span> It might be. I don’t really pay much attention to other stuff, which I should do. Someone else is probably doing that. I’ll tell you now, it’s been the most controversial aspect of it. Some people really did not like the idea of using data attributes. The thing is as well, and how I respond, is, do what you want. We’re not telling you to do things in a certain way, it’s just suggestions. If you want to do exceptions to CSS classes, like modifiers, then knock yourself out. The CUBE police aren’t going to come knocking at your door. It’s absolutely fine.

<span class="smashing-tv-speaker">Andy:</span> The CUBE thing is a thinking thing, it’s a structure. You apply that structure however you want to apply it, with what tooling you want, or whatever technology you want. As long as you keep things consistent, that’s the important thing.

<span class="smashing-tv-host">Drew:</span> So there’s no such thing as pure CUBE?

<span class="smashing-tv-speaker">Andy:</span> The way I write it is pure CUBE, Drew. Everyone else is just a fake, it’s just a weak immitation.

<span class="smashing-tv-host">Drew:</span> Apart from to you, no-one can say, "That isn’t textbook CUBE."

<span class="smashing-tv-speaker">Andy:</span> No, that’s it. No-one can dispute that really, can they? So, yeah, I’ll go with that. Gives you a bit of clout or something, I think, something like that.

<span class="smashing-tv-host">Drew:</span> Can you mix and match a CUBE approach with other methodologies? Can you use bits of BEM?

<span class="smashing-tv-speaker">Andy:</span> Yeah, I reckon so. I’ve been thinking about it a little bit because I’m going to do some more stuff on it soon because it’s become quite popular, so people will want more work. One thing I’m going to look at is how to approach using the CUBE methodology with something existing.

<span class="smashing-tv-speaker">Andy:</span> So there’s two opposite ends of the scale. A good question that people have asked is: "How does this work with every layout, the other stuff?" I’m like, basically, every layout is the C. That’s what every layout is, it’s the compositional layer. Then someone else asked, "Well, how would this work with something like Atomic Web Design, like their stuff that Brad Frost did? It’s like, well, you could break those pieces up and apply them at each level. Atomic Design goes all the way down into the micro detail. It’s abstracting that into using, right, okay, well I can apply this with utilities, so the molecules, I think. I can apply that with the utilities, and it’s translating what you know already into this slightly different structure of working.

<span class="smashing-tv-speaker">Andy:</span> Really, it’s a renaming for a lot of things. I’ve not invented anything here, I’ve just sort of, like I say, I’ve just stolen things that I like. I love the way that some of the Atomic Design stuff is thought about. That’s really some smart work. And BEM. The stuff Harry did, the Inverted Triangle CSS, I thought that was really cool. So I’ve just sort of nicked bits that I like from each one of them and sort of stitched them all together into this other hybrid thing, approach. More to come, I think.

<span class="smashing-tv-host">Drew:</span> Can the CUBE approach be applied to existing projects that already have CSS in place or is it something you really need to start on a fresh project with?

<span class="smashing-tv-speaker">Andy:</span> That very much depends. So if you’ve got like a bootstrap job and it’s just got thousands of lines of custom CSS, that I’ve definitely been involved in before, then I think you might be trying to put a fire out with a bottle of water at that point. But if you... say, for instance, if you’ve got a rough BEM setup and it’s gone a bit layer-y, you could use CUBE to refactor and actually pull it back into shape again.

<span class="smashing-tv-speaker">Andy:</span> It depends, the answer to that one. But it’s doable, as with everything. If you really want it to work, Drew, you can do it if you want, can’t you? The world is our oyster!

<span class="smashing-tv-host">Drew:</span> Especially if your BEM site’s gone layer-y.

<span class="smashing-tv-speaker">Andy:</span> Yeah. Nothing worse than a layer-y BEM site!

<span class="smashing-tv-host">Drew:</span> I’ve noticed in the examples that you’ve given... and I’ve got an eagle eye, I’ve seen you’ve been doing this for a while... a lot of your class values in the HTML attribute are wrapped in square brackets.

<span class="smashing-tv-speaker">Andy:</span> Oh, God, yeah. Tell you what, Drew-

<span class="smashing-tv-host">Drew:</span> What is that about? What is that about?

<span class="smashing-tv-speaker">Andy:</span> I’ll tell you what, if there’s ever one thing that I’ve done in my whole career that’s just been absolutely outrageously controversial... and you follow me on Twitter, you’ve seen what comes out of my mouth... it’s those bloody brackets! My, God! People either love them or hate them. They’re Marmite, they are.

<span class="smashing-tv-speaker">Andy:</span> The reason I do them is a grouping mechanism. So if you look at the way that they’re structured, the way I do it is, block at the start and then I’ll do a utilities after that. Then what I might do is, in between a block group and a utility group, there might be another block class. So a good example of that would be... we’ll go back to the card again. But then say that there’s a specific block called a CTA, like a call to action. You might have that applied to the card as well, and then your utilities are enforcing the design attributes, so the colors and all that business. So then you’ve got three groups of stuff.

<span class="smashing-tv-speaker">Andy:</span> When you come to it, if you’ve got that order in your head each time, you know, okay, right, this first group’s blocks. Oh, that’s looks like another block. I’ve got that one. Then it’s like, right, they’re definitely utility classes. Then what I might even do is, if there’s a lot of design token implementation, have that in a separate group. So it’s just very clear what each group is doing, and there’s a separation inside of the classes there as well. I’ve found it really helpful. Some people find it incredibly offensive. It’s definitely a do it if you want to do it. Definitely you don’t have to do it.

<span class="smashing-tv-speaker">Andy:</span> It’s quite funny, when I published that article, so many people finished halfway through to ask me, "What is it with these brackets?" I was like, "Did you finish the article? Because there’s a big section at the end where it explains exactly what they’re doing," to the point where I actually had to write a bit in the middle of the article of, "If the brackets are essentially doing your head in, click here and I’ll skip you all the way down to that explanation bit so you can just read about them." It can be quite controversial.

<span class="smashing-tv-speaker">Andy:</span> When I’ve worked on really, really complex front-ends... and we did a little bit of stuff together, didn’t we, last year?

<span class="smashing-tv-host">Drew:</span> Yeah.

<span class="smashing-tv-speaker">Andy:</span> You’ve seen the sort of design implementation on that project that we were on. It requires that sort of grouping because there’s just so much going on at the time, there’s so much different stuff happening. I’ve just found it really, really useful over the years, and also get lots of questions about it, to the point where I was almost going to write just one page on my website that I could just fire people to to answer the question for them.

<span class="smashing-tv-host">Drew:</span> Slash, what’s with the brackets?

<span class="smashing-tv-speaker">Andy:</span> Yeah. Slash, brackets. Have you seen that new Hey Email thing that’s just come out? They’ve bought a domain of itsnotatypo.com, just to answer the whole Imbox, like im with an M rather than an in. Basically, I was like, "I think I need to do that," like, whatswiththebrackets.com, and just do a one-pager about it.

<span class="smashing-tv-host">Drew:</span> It strikes me that the approach with brackets actually could be something that might be useful when using things like Tailwind or something that has a lot of classes because that can-

<span class="smashing-tv-speaker">Andy:</span> Yeah. Oh, God, yes.

<span class="smashing-tv-host">Drew:</span> You have classes that are addressing your break points and what have you, and then you’ll have things that are for layout, things that are for color or type, or what have you. So it might also be a useful way of dealing in situations like that.

<span class="smashing-tv-speaker">Andy:</span> I’d definitely agree with that. A good analogy... not analogy. A good bit of info about Tailwind is that I actually quite like Tailwind. I’ve used that on very big projects. The one thing that really opened my eyes to Tailwind though was when I saw a junior developer try to work out what was going on, and it was really, really eye-opening because they just didn’t have a clue what was happening.

<span class="smashing-tv-speaker">Andy:</span> I think that’s one problem I’ve found with these sort of over-engineered approaches, which I think it’s fair to say Tailwind is, is that there’s a certain skill level that is required to work with it. I know the industry tends to have an obsession with seniority now, but there’s still people that are just getting into the game that we need to accommodate, and I think having stuff that’s closer to the language itself is more helpful in those situations because they’re probably learning material that is the language as it is. So I think it’s just a bit more helpful. Especially having a diverse team of people as well. Just food for thought for everyone.

<span class="smashing-tv-host">Drew:</span> People might look at all the different methodologies that are out there and say, "This is evidence that CSS is terrible and broken, that we need... all these problems have to be solved by hacking stuff on top. We need tools to fix bits of CSS. We need strict procedures for how we implement it, just to get it to work." Should the platform be adapting itself? Do we need new bits of CSS to try and solve these problems or are we all right just hacking around and making up funny acronyms?

<span class="smashing-tv-speaker">Andy:</span> I think the power of CSS, I think, is its flexibility. So if you’re going to program CSS, a lot of the knowledge is less of the syntax and more of the workings of a browser and how it works. I think that might be a suggestion, that the problem is that people might not have learnt CSS quite as thoroughly as they thought they might have learnt it, who created these problems. I’ve seen that in evidence myself. I spotted a spacing mechanism that had been invested, which was very complicated, and I thought, "This person has not learnt what padding is because padding would actually fix this problem for them, understanding how padding works and the box model." That’s not to be snidey about it.

<span class="smashing-tv-speaker">Andy:</span> We work in an industry now that moves at an even faster pace than it has done previously and I think there’s a lot less time for people to learn things in detail. But, on that front, I think CSS still does have work to do in terms of the working group, who I think do a bloody good job. A great, shining example of their work was the Grid spec which was just phenomenal. The way that rolled out in pretty much every browser on day one, I thought that was so good.

<span class="smashing-tv-speaker">Andy:</span> But we’ve got more work to do, I think, and I think maybe the pace might need to increase a little, especially with stuff like container queries, we all love talking about them. Stuff like that I think would help to put CSS in a different light with people, I think. But I think CSS is brilliant, I love it. I’ve never had a problem with it in lots of years really. I do find some of the solutions a bit odd, but there you go.

<span class="smashing-tv-host">Drew:</span> What’s the response been like to CUBE since you published the article?

<span class="smashing-tv-speaker">Andy:</span> Mind-blowing. I honestly published it as just supporting material, and that’s all I expected it to be, and it’s just blown up all over the place. A lot of people have been reading it, asking about it, been really interested about it. There’s definitely more to come on it.

<span class="smashing-tv-speaker">Andy:</span> I did say in the article, I said, "Look, if people are actually quite interested in this, I’ll expand on this post and actually make some documentation." I’ve got bits of documentation dotted around all over the place, but to sort of centralize that, and then I was thinking of doing some workshops and stuff. So there’s stuff to go. It’s how Every Layout started as well. We both had these scattered ideas about layout and then we sort of merged them together. So something like that, I suppose, will come in the future.

<span class="smashing-tv-host">Drew:</span> Are there any downsides that you’re aware of to using CUBE? Are there problems that it doesn’t attempt to solve?

<span class="smashing-tv-speaker">Andy:</span> Yeah. This accent, Drew, it just won’t go way, no matter what I do! In all seriousness, I think CUBE’s got as close as I can get to being happy with the front-end, which is saying a lot, I think. You never know, things might change again. This has evolved over more recent years. Give it another five years, I’ll probably be struggling with this and trying something else. I think that’s the key point, is to just keep working on yourself and working on what you know and how you approach things.

<span class="smashing-tv-speaker">Andy:</span> This definitely won’t work for everyone as well, I know that for a fact. I know that from my comments. I don’t expect it to work for everyone. I don’t expect anything to work for everyone. It’s the same with JavaScript stuff: some people like the reactive stuff and some people don't. It is what it is. We’re all people at the end of the day, we all have different tastes. It’s all about communicating with your teammates at the end of the day, that’s the important thing.

<span class="smashing-tv-host">Drew:</span> I know you as a very talented designer and developer and you, like many of us, you’re just working on real projects all day, every day. But you’ve recently started publishing on this site, Piccalilli, which is where the CUBE CSS introduction article was. So Piccalilli is kind of a new venture for you, isn’t it? What’s it all about?

<span class="smashing-tv-speaker">Andy:</span> Very kind of you to say, Drew. You’ve actually worked with me, so that’s high praise. But the Piccalilli thing is an evolution. So I’m a freelancer. I do client work, but I think this has become apparent with the pandemic, that that is not the most sustainable thing in the world in some industries. I think freelancing can be very, very tough, as a developer and designer. It’s something that I’ve been doing it for so long now, 10 years... well, 12 years now actually.

<span class="smashing-tv-speaker">Andy:</span> I fancied doing something a bit different and applying the knowledge that I’ve got and actually sharing it with people. I’ve always been very open and sharing, and I wanted to formalize that. So I created Piccalilli to write tutorials, but mainly for courses that I’m producing: that’s the main meat and potatoes. And then there’s the newsletter which is... people are really enjoying the newsletter because I share cool things I’ve found on the internet every week. That’s the backbone of it. It’s just going really well. That’s essentially where I want to see myself doing more and more full-time, as the years go on, I think.

<span class="smashing-tv-host">Drew:</span> So what’s coming next for Piccalilli? Have you got anything that you’ve got coming out?

<span class="smashing-tv-speaker">Andy:</span> Thanks for the door open there, Drew! By the time this recording goes out, the first course will be live: Learn Eleventy From Scratch, and that’s where we learn how to build a Gatsby website! No, you learn how to build an Eleventy site. So you start off with a completely empty directory, there’s nothing in it, it’s empty, and then at the end of it you’ll finish up with this really nice-looking agency site. We learn all sorts in it. You learn how to really go to town with Eleventy. We pull remote data in from places. We use CUBE CSS to build a really nice front-end for it.

<span class="smashing-tv-speaker">Andy:</span> If you want to get into the Jamstack and you want to get into static site generators, or just how to build a nice website, it’s just a really handy course, I hope, for that. It’s currently being edited within an inch of its life as we’re talking. It’s going to be cool, I hope, and useful. But that’s an accumulation of a lot of stuff I’ve been doing over the last couple of years. So it should be fun.

<span class="smashing-tv-speaker">Andy:</span> So buy it, and I’ll do a discount code, do like smashingpod for 40% off, and you can get it when it comes out.

<span class="smashing-tv-host">Drew:</span> Amazing. We’ll link that up. Have you figured out how to spell Piccalilli reliably yet?

<span class="smashing-tv-speaker">Andy:</span> I was on with Chris and Dave with the ShopTalk Show and I said on there, "If there’s ever one thing you want to hire me for it’s to write Piccalilli by hand first time without even thinking about it," because I’ve written that word so many times that I just know exactly how to spell it off by heart. So the answer to your question is yes.

<span class="smashing-tv-host">Drew:</span> Well, I’m still struggling, I’ll tell you that much!

<span class="smashing-tv-speaker">Andy:</span> It is hard. Oh, God. I totally empathize. It took me a long time to learn how to spell it but it’s one of those words in our vocabulary. This year I’m trying to spell necessary without making a spelling mistake!

<span class="smashing-tv-host">Drew:</span> So I’ve been learning all about CUBE CSS. What have you been learning about lately, Andy?

<span class="smashing-tv-speaker">Andy:</span> Do you know what? This is going to surprise you, Drew. MySQL is what I’ve been learning about recently. So, basically, Piccalilli is totally self-published. It’s an Eleventy site but it’s got an API behind it, and that’s got a MySQL database behind it. The stuff that gives people content that they’ve purchased requires some pretty hefty querying. So I’ve just actually properly invested in some MySQL... especially the difference between joins, which I didn’t actually realize there was a difference between each type of join. So that’s been really useful and it’s resulted in some pretty speedy interactions with the database.

<span class="smashing-tv-speaker">Andy:</span> I used to run this thing called Front-End Challenges Club and when I first launched it it just collapsed and died on itself because MySQL was shoddy to say the least. So I’ve really been learning how to do that because I’m not a backend person at all, I’m a pixel-pusher. So it’s definitely not in my remit. That’s more your neck of the woods, isn’t it? I find it really cool, MySQL. I actually really like writing it. It’s a really nice, instructional language, isn’t it?

<span class="smashing-tv-host">Drew:</span> It is, it’s great. I learnt SQL at school.

<span class="smashing-tv-speaker">Andy:</span> Wow!

<span class="smashing-tv-host">Drew:</span> We’re talking like 20 years ago now.

<span class="smashing-tv-speaker">Andy:</span> Did they have computers in those days?

<span class="smashing-tv-host">Drew:</span> They did, yeah. We had to wind-

<span class="smashing-tv-speaker">Andy:</span> Did you have to write it by hand?

<span class="smashing-tv-host">Drew:</span> We had to wind them up! We did. But, I tell you, for a developer, it’s akin to learning your times tables: one of those things that seems like a bit of a chore but once you’re fluent, it just becomes useful time and time again.

<span class="smashing-tv-speaker">Andy:</span> Yeah. For sure. There’s really tangible differences as well. You really see the difference in speed. I really like working with Node because that’s really fast but Node and MySQL is just... not a very common choice, but I think it’s a pretty good choice. I think it works really, really well. So I’m happy with that. As you know, I don’t like writing PHP. So that’s never going to be an option.

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Andy, you can follow him on Twitter where he’s at hankchizljaw. You can find Piccalilli at piccalil.li, where you’ll also find the article describing CUBE CSS, and we’ll also add links to all of those in the show notes, of course.

<span class="smashing-tv-host">Drew:</span> Thanks for joining us today, Andy. Did you have any parting words?

<span class="smashing-tv-speaker">Andy:</span> Stay safe, and wear your mask.

{{< signature "il" >}}
