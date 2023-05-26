---
title: 'Smashing Podcast Episode 37 With Adam Argyle: What Is VisBug?'
slug: smashing-podcast-episode-37
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e26ce3b7-49e1-45d7-8411-ecc5b2d696cd/smashing-podcast-episode-37.jpg
date: 2021-05-18T05:00:00.000Z
summary: >-
  In this episode, we’re talking about VisBug. What is it, and how is it different from the array of options already found in Chrome DevTools? Drew McLellan talks to its creator Adam Argyle to find out.
description: >-
  In this episode, we’re talking about VisBug. What is it, and how is it different from the array of options already found in Chrome DevTools? Drew McLellan talks to its creator Adam Argyle to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re talking about VisBug. What is it, and how is it different from the array of options already found in Chrome DevTools? Drew McLellan talks to its creator Adam Argyle to find out.

<iframe src="https://share.transistor.fm/e/e5abba67/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [VisBug sandbox and playground](https://visbug.web.app)
- Adam on [Twitter](https://twitter.com/argyleink)
- Adam’s [personal site](https://nerdy.dev)
- [VisBug on YouTube](https://t.co/bVWVxz4QcL?amp=1)
- [VisBug 101](https://medium.com/dev-channel/visbug-101-749f26a485c8)

### Weekly Update

- [The Conference Platform We Use For Our Online Events: Hopin](https://www.smashingmagazine.com/2021/05/smashingconf-conference-platform-hopin/) by Amanda Annandale
- [A Primer On CSS Container Queries](https://www.smashingmagazine.com/2021/05/complete-guide-css-container-queries/) by Stephanie Eckles 
- [Frustrating Design Patterns That Need Fixing: Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/) by Vitaly Friedman
- [Tree-Shaking: A Reference Guide](https://www.smashingmagazine.com/2021/05/tree-shaking-reference-guide/) by Átila Fassina
- [How We Improved Our Core Web Vitals](https://www.smashingmagazine.com/2021/05/core-web-vitals-case-study/) by Beau Hartshorne

## Transcript

<p><a href="https://twitter.com/argyleink"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48b398db-d094-45ac-aaf2-d2321f2a0c32/adam-argyle-opt.jpg" width="200" height="200" alt="Photo of Adam Argyle" /></a><span class="smashing-tv-host">Drew McLellan:</span> He’s a bright, passionate, punk engineer with an adoration for the web, who prefers using his skills for best in class UI and UX, and empowering those around him. He’s worked at small and large companies, and is currently a developer advocate working at Google on Chrome. He’s a member of the CSS working group and the creator of VisBug, a design debugging tool. So we know he knows his way around design and UX, but did you know he owns more pairs of flip flops than any living biped? My smashing friends, please welcome Adam Argyle.</p>

<span class="smashing-tv-speaker">Adam Argyle:</span> Hello.

<span class="smashing-tv-host">Drew:</span> Hi Adam, how are you?

<span class="smashing-tv-speaker">Adam:</span> Oh, I am smashing, you know it.

<span class="smashing-tv-host">Drew:</span> That’s good to hear. So I wanted to talk to you today about your project, VisBug, and generally, about the concept behind design debugging and how it might fit into project workflows. I mean, we’ve had developer focused browser debugging tools for a long time, I mean, probably more than a decade now. But those are obviously very much focused on code. So what is different about VisBug? And what’s the sort of problem that it’s trying to solve?

<span class="smashing-tv-speaker">Adam:</span> Awesome. Yeah, the main problem that it’s rooted in is, as a front-end engineer I work with designers all the time, and I always loved this moment where we sat down and I’d be like, "Okay. I’m making the final touches. We’ve got another day or two until we deploy. So designer, sit down, and would you critique this? I want you to open up my local host version on your browser and on your phone, or whatever, and talk to me about what you see."

<span class="smashing-tv-speaker">Adam:</span> And after doing this for many years and always loving this interaction, I kind of started to feel guilty after a while because of how common and simple the tasks were. They’d be like, "One pixel down here. Five pixels margin here." And it was always nits and nudges, and nits and nudges to spacing and type. I mean, rarely was it like, "Ooh, hold on minute while I spend 30 minutes changing some angular, or whatever, to adjust my DOM so that the DOM can support your request," or whatever.

<span class="smashing-tv-speaker">Adam:</span> It was usually tiny stuff. And then I ended up making a survey, and I surveyed all these designers at Google. And I was like, "When you open up DevTools, what do you do?" And it kind of was resounding that they just need basics. And so it was born out of, I was like, "This should be easier. You shouldn’t have to pop the hood on the Ferrari, move a chunk of engine, just to change the color of the car seats. That’s not fair. You should just be able to touch the car’s seats and change the color, just like a design tool." I was like, "Something could facilitate this workflow." And I was like, "Okay, I guess I’ll hack on something to see if I can create the solution."

<span class="smashing-tv-speaker">Adam:</span> And that’s how it all started. It really started with spacing and then typography. And once I had a selection mechanism down that emulated design tools it was like, "Well what else can I do?" And it just kept going from there. But yeah, born in that moment.

<span class="smashing-tv-host">Drew:</span> So the idea is that the client asks you to make the logo bigger, and VisBug helps the browser behave more like a design tool for making those sorts of tweaks. So closer to something like Illustrator, or Photoshop, or Figma, or any of these types of things.

<span class="smashing-tv-speaker">Adam:</span> Yeah. That use case is a good one too. Because you could be a with a client and they say, "Oh, we love this," this is so classic, "we love the design, but that color blue is hard for us." And you’re like, "Really?" This is like, people can submit a form and you can make money, but you want to talk to me about blue right now? And usually it would create a whole cycle. The PM would go, "Okay, we’ll take down your request and then we’ll send it to design."

<span class="smashing-tv-speaker">Adam:</span> But if the designer’s there and it’s their browser that’s showing it they’d be like, "Okay. Well I’ll just click the thing and change the color." And you can nip an entire cycle of work by just prototyping the change there in the browser. So it is. It’s most effective against an existing product, right? Because it’s a debugging tool. It’s not necessarily a generation tool. It doesn’t create a site for you. It can, but it’s kind of awkward.

<span class="smashing-tv-host">Drew:</span> So technically it’s an extension that you install in a Chrome browser. Is that right?

<span class="smashing-tv-speaker">Adam:</span> Yep. And it’s an extension. When you launch it it downloads a JavaScript file that says, "Here’s a custom element called VisBug." And then you put the DOM element, vis-bug on the page. And poof, I just take that moment and turn it into a toolbar, and start to listen to events on the page. I listen to your hover events, and I listen to your click events. And I try to do my best to intercept them, and not compete with your main page.

<span class="smashing-tv-speaker">Adam:</span> But yeah, that’s the essence of... The only reason it’s an extension is just so it’s easy to put on your page. Although at this point it does have some settings now that come with you across browsers. But it’s still mostly, 99.9%, a custom element with no dependencies. I think I like a color library I use, and it’s otherwise just all vanilla. Yeah.

<span class="smashing-tv-host">Drew:</span> I guess that’s how Firebug sort of started out, wasn’t it? As a Firefox extension back in the day.

<span class="smashing-tv-speaker">Adam:</span> Yep. That’s why it’s called VisBug. It’s very much inspired by Firebug but for visual designers.

<span class="smashing-tv-host">Drew:</span> Ah. There we go. I mean, this isn’t perhaps the ideal format, being an audio podcast, to talk about a visual tool. But run us through, if you will, some of the sort of tools and the options that VisBug gives you.

<span class="smashing-tv-speaker">Adam:</span> Absolutely. So one of the first things that VisBug does, and you can also, if you are at home or at a computer, you can go to visbug.web.app, and try VisBug without the extension, right?

<span class="smashing-tv-host">Drew:</span> Ah.

<span class="smashing-tv-speaker">Adam:</span> It’s a web component, so I’ve loaded up a webpage for you here at visbug.web.app that looks like it’s got a whole bunch of art boards, and then of course, VisBug preloaded. And the goal of this site is to let you play, and explore, and delete. I think the delete key is one of the most satisfying tools to begin with. You’re like, "What can I do to a page?" And you’re like, "Well I can destroy it."

<span class="smashing-tv-speaker">Adam:</span> And I made it so that you can hold delete, it will find the next... Which is pretty difficult on a delete. You delete something and it selects the next sibling. So it’ll select the next sibling forever. If you hold delete until you delete the whole... Anyway, very satisfying. Hit refresh and it all comes back. But the first tool that VisBug ships with, so when you just launch it, is the guides tool. And I used to literally hold up paper to my screen, or I would go get a system extension that would allow me to sort of mark things and create lines.

<span class="smashing-tv-speaker">Adam:</span> Because, yeah, alignment becomes very optical at a certain point for a lot of designers, right? They don’t want, necessarily, mathematical alignment, right? This is why typography has optical kerning. It’s not math kerning. This is human kerning. And so the guides tool is rooted in that a lot of nits that happen from a designer are zooming in on stuff, checking alignment. Is the spacing good?

<span class="smashing-tv-speaker">Adam:</span> So that’s the second thing that the guides tool does. When you launch it and you just hover on stuff you’ll see the element that you’re hovered on gets a little box around it. And then dashed guides show up, just like rulers would normally do. And just like in Sketch and Zeplin where you sort of hover and you get these guides, it’s the same concept, just live on your page. And if you click something, and then hover to a new destination, you get measuring tools. And the measuring tools are in pixels, and they’re calculated... So visually, how many pixels are between it. Not what did someone say. It’s not adding up all the spacing, it’s just you click this thing and it’s this far away from that other box.

<span class="smashing-tv-speaker">Adam:</span> And I think that becomes really helpful, because you can hold shift and continue clicking, and essentially verify that you have equal spacing between five icons. And it’s just a couple of clicks. Don’t have to know code, just launch VisBug, hover, click, click, click, and you get to see that, "Oh look it is. Yeah. 15 pixels between each of these." Or sometimes you get something that’s kind of annoying, you’ll click in a box and then click its parent box and you’ll realize that its top distance is nine and the bottom one is eight. And you go, "How will I center this? It is somehow in between." And shakes fist.

<span class="smashing-tv-speaker">Adam:</span> But at least you’re able to see it nice and easily with the guides tool. So yeah, that’s the guides tool.

<span class="smashing-tv-host">Drew:</span> I’ve definitely been there, with holding up bits of paper to the screen. And also, the other trick that I would use is to open another browser window and use the edge of the window to align items. And then you sort of try and keep everything in the right place so that as you make code change and refresh it’s all still lining up. Yeah, not an ideal way of working, so.

<span class="smashing-tv-speaker">Adam:</span> Not an ideal way of working. Yep. And there’s the next... So, oh, and the first version of that was very loose. It didn’t snap, it just held up a crosshair, which is a feature that I’ll add back later. So some users are like, "Hey, I love the snapping, it’s just like my design tools. But what if I want a loose measurement? Or I want to do a letter, I want to measure a letter, not its letter box?" And so, well, this guides tool could very easily be changed to having a modifier key.

<span class="smashing-tv-speaker">Adam:</span> So here’s where VisBug gets a little kind of different, but also hopefully familiar, is it’s very heavy on hotkey modifiers. So just like if you watch a pro designer, they’re very much hotkey savvy. And they’re hitting hotkeys here, zooming in, hitting hotkeys over there, and just doing all their nudging from their keyboard. And so VisBug is very keyboard-centric in the way that you change things.

<span class="smashing-tv-speaker">Adam:</span> It’s also because VisBug allows multiple selections, and it can change 100 items’ spacing at the same time. And it does so relatively. So anyway, it has a couple interesting quirks, but the keyboard in a modifier concept is really important. And you can hold option, or shift, or command in a lot of the tools and get something different, or get a new sort of feature in there.

<span class="smashing-tv-host">Drew:</span> So it’s one of those tools where it really pays to learn the keyboard shortcuts.

<span class="smashing-tv-speaker">Adam:</span> It does. And so when you launch VisBug and you hover over one of the tool icons, you’ll get a breakdown. It throws out a little flyout menu, it says the hotkey for choosing this tool, and it tells you what it can do, and what interactions to do in order to get them. So the guides tool says, "Element guides, just hover. Measure something, click, and then hover something new. Sticky measurements are shift plus click so they’ll persist."

<span class="smashing-tv-speaker">Adam:</span> And these guides are really nice too for screenshotting. So if you’re reviewing a PR, even as just a front-end engineer, or maybe a designer reviewing a PR, this can be a really powerful way for you to get in there and, yeah, have some high fidelity inspection. Which kind of leads us into the next tool. Do you want to hear about the next tool?

<span class="smashing-tv-host">Drew:</span> Yeah, sure. Let’s go for it.

<span class="smashing-tv-speaker">Adam:</span> Awesome. The next one is the inspect tool. And this one is like... Designers usually, they don’t want all of the CSS, right? When they expect with... I almost said Firebug, but the Chrome DevTools, you get the full list, right? I selected this H1 and so here’s everything all the way back to the browser style sheet. And the designer’s like, "The browser what? The browser has a style sheet?"

<span class="smashing-tv-host">Drew:</span> Down at the murky bottom of that scrolling panel.

<span class="smashing-tv-speaker">Adam:</span> The murky bottom, right?

<span class="smashing-tv-host">Drew:</span> Yeah.

<span class="smashing-tv-speaker">Adam:</span> It’s like you peeled back all the layers and then you’re like, "Ooh, I don’t like these layers anymore." And the inspect tool here, it says, "Ah, designers, I know what you want. It’s just the border color." Basically, only show me something if it’s unique, so don’t just cover me with CSS properties. And I’m really mostly interested in color, typography, and spacing. So I’m going to look at margins, line heights, font family’s really important, right? There’s a whole extension just to tell you what the font family is on a page.

<span class="smashing-tv-speaker">Adam:</span> In VisBug that’s just a line item in the inspect tool. So you just launch VisBug, hit inspect, and hover on any typography and it’ll tell you the font family. So yeah, it tries to make a designer focused in what it surfaces, yeah.

<span class="smashing-tv-host">Drew:</span> So that tool is not showing any inherited styles. Is that right?

<span class="smashing-tv-speaker">Adam:</span> That is correct. Unless they are inherited and unique. So if they... A text color or something, if the text color isn’t literally the word inherit, it will tell you that it’s a computed value, that it’s something interesting.

<span class="smashing-tv-host">Drew:</span> Yeah, that’s a really useful just... Yes. Helps you focus on the things that are just literally applying to that one instance of something, which is obviously what you wanted to change. I mean, I guess this could be really useful, all these tools would be really useful in, sort of as you mentioned, getting stakeholder feedback. And sort of working interactively with a client.

<span class="smashing-tv-host">Drew:</span> I guess it would work equally well over screen sharing, as we have to do these days, more and more. You don’t have to be sat at a computer with someone, you could be sat on the other end of a call and share your browser and do it that way. I guess it’d be quite an effective way of getting feedback when a client can’t point at the screen and say-

<span class="smashing-tv-speaker">Adam:</span> Definitely.

<span class="smashing-tv-speaker">Adam:</span> It’s always magical when you turn the live webpage into what looks like a Zeplin artboard. Someone’s like, "What... Did we just go somewhere new?" And you’re like, "No, this is your product. We’re just interacting with it very visually." Yeah, it can be really nice.

<span class="smashing-tv-host">Drew:</span> Are there any other interesting use cases that you’ve seen VisBug put to or that have occurred to you might be interesting?

<span class="smashing-tv-speaker">Adam:</span> Yeah. So, yeah, there’s so many it’s kind of hard to start. Oh, one that’s important is developer to developer communication. VisBug works on the calculated values. So it doesn’t look at your authored values. And that can be really nice, because you’re sort of measuring and inspecting the absolute end result into the way that the pixels got calculated on the screen. And that can be really nice, to have a conversation that way, as you’re working on the results, as opposed to the authoring side.

<span class="smashing-tv-speaker">Adam:</span> And you can go back towards like, "Okay, well how did we go wrong in the authoring side if this is what we got visually?" Which also kind of plays into, the next tool is the accessibility inspect tool. So the inspect tool makes it easy just to see the styles on an element, and it breaks them down in a very designer-friendly way. The accessibility tool helps you inspect all of the elements on a page, and it surfaces any accessible properties it has, which makes it, I’m hoping, easier to go verify that something is done.

<span class="smashing-tv-speaker">Adam:</span> So a PR... And things often get created. So this is, again, developer to developer, designer developer, you’re reviewing interfaces. It’s just so critical. If you’re looking at an interface and you’re curious, VisBug has a use case for you there. There’s also use cases where you can sort of prototype in the browser. So we talked about one where it’s like, the client wanted to try blue. Okay, that’s a pretty easy scenario.

<span class="smashing-tv-speaker">Adam:</span> But there’s other ones too. If you hit command D on VisBug you’ll duplicate an element. And it doesn’t care what you’re duplicating. So you could duplicate a header, go add some spacing between the two headers, and go make a variant live in the browser. You double click the header text and it becomes an editable text field, and you go try a new headline out and go see how the headline fits. Go adjust some spacing and you just saved yourself all this developer work, finding a source file and all that sort of stuff, and you’re just...

<span class="smashing-tv-speaker">Adam:</span> So yeah, it can help you explore and verify. It’s kind of a weird... I mean, it’s a lot of the things DevTools does, right? It comes in after you’re done, it doesn’t actually give you source code very often, it’s not very often that you copy code out of DevTools. You might copy a key value pair. Like, "Oh, I changed this style." But yeah, anyway.

<span class="smashing-tv-host">Drew:</span> Mm-hmm (affirmative). Yeah. I can think of sort of particularly visual cases where you might want to, you mentioned, duplicating items. You might want to take a whole section of the page and duplicate it to simulate what it would be like if there was a lot more content than you were expecting.

<span class="smashing-tv-speaker">Adam:</span> Yes. That’s the chaos testing use case.

<span class="smashing-tv-host">Drew:</span> Yeah.

<span class="smashing-tv-speaker">Adam:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> Which is something that we all have to deal with, designing with sort of CMS-based systems and all those sorts of fun tasks.

<span class="smashing-tv-speaker">Adam:</span> Yep, that’s a really crucial use case too. Because I do that one for... Yeah, headlines, like I said. You just double click some text and I just go slam the keyboard. Blah, blah, blah, blah, and hit a bunch of spaces, blah, blah. And I’m like, "Okay, how’d the layout do? Oh, it did good. Okay, good, I can move on to the next thing. What happens if I duplicate this four times? Is there still space between everything? Does it flow next to the next item?"

<span class="smashing-tv-speaker">Adam:</span> It can be really nice for that simulation of the, yeah, content chaos. Really short title, really long titles, has no friends, has a million friends. How do you handle these use cases in the UI? Yep.

<span class="smashing-tv-host">Drew:</span> So it works with any browser-based content. So PWAs as well as regular webpages?

<span class="smashing-tv-speaker">Adam:</span> Yes, it does. So if you have Spotify installed, I do this all the time, I’ve got Spotify installed and I’ll just be like, "Spotify, you look like you’re an impossible app to inspect." But guess what? VisBug don’t care. VisBug overlays all your stuff, inspects all the typography. I made a light theme for... Oh, I have a tweet somewhere where I made a light theme of Spotify.

<span class="smashing-tv-speaker">Adam:</span> Oh, this was another use case, sorry, for prototyping color. I can create a light theme on the product itself without having to go mess with a bunch of sticker sheets, right? So there’s this important even mentality, I’d love VisBug to help folks get into which is, use your product as a playground. Use that as... It’s so real. It’s more real than your design comps are. So spend some more time in there. I think you’ll find that you can make more effective design decisions working on your actual product.

<span class="smashing-tv-host">Drew:</span> And the case of accessibility as well is particularly interesting, because often, particularly these days, we’re working very much in component libraries, and looking at small components of a page. And spending less time looking at all those integrated together to create the sort of views that a customer actually interacts with. And it gets really difficult to keep an eye on those sort of finer details like accessibility things, attributes, that aren’t visible on the page.

<span class="smashing-tv-host">Drew:</span> It’s very difficult to keep an eye on things that aren’t visible. So this is where tooling can really, really help to be able to inspect something and see that, yes, it’s got the correct roles on it and it’s-

<span class="smashing-tv-speaker">Adam:</span> It does. That’s the exact use case. I want a PM to be able to go verify this stuff. I want a designer to be able to go look at accessibility and not have to pop open the tools, find the DOM node, it’s all crunched up in the elements panel and looking weird. That it just says, "Here’s the area attributes, here’s the title if it exists." There’s also some other accessibility tools to. VisBug ships with the search icon. The search icon has multiple ways to interact with it.

<span class="smashing-tv-speaker">Adam:</span> So first it queries the page. So if you know the element type or the element class name that you want you can just search it, so you don’t have to find it with the mouse. But that also has slash commands in it. So there’s plugins in VisBug, and they’ll execute scripts on the page. So if you’ve ever had a bookmark that you’ve saved three or four... You’re like, "I’m going to use this one because it highlights all the borders and shows me my boxes." It’s like a debug trick or something.

<span class="smashing-tv-speaker">Adam:</span> It’s probably a VisBug plugin. So you launch VisBug, hit slash, and you’ll get autocomplete, and it’ll show you all the different plugins. And there’s some accessibility ones that are really nice that overlay errors, and various things like that. So I agree. Accessibility should be more accessible. That’s just lame to say. But it needs to be closer to the tool belt. And I think sometimes it’s too far away, and maybe that’s why it gets missed. So I’m hoping if it’s a little more up front, and center, and easier that it gets checked more. Yeah.

<span class="smashing-tv-host">Drew:</span> And it’s interesting you say that VisBug works with the sort of computed values of things, so like colors. So does that mean that if you have several layered elements that have different levels of opacity that you’d be able to measure the exact color that is being rendered on the screen rather than-

<span class="smashing-tv-speaker">Adam:</span> Ooh.

<span class="smashing-tv-host">Drew:</span> ... looking at the individual elements and trying to somehow work it out?

<span class="smashing-tv-speaker">Adam:</span> That’s a really good question. So I think, if I’m understanding the question right, which this is a classic difficulty in the front-end is, yeah, how do you know if you have a half opaque text word, what is its color over gray versus over white? And how do you know its contrast? Right now, we don’t know. So VisBug knows the color, and it’ll say, "50% gray," or whatever the color is that you have there. But it doesn’t know anything smarter than that. It’s not able to...

<span class="smashing-tv-speaker">Adam:</span> I think what you’d have to do in that case is create a canvas, paint all the layers on there, and then use an eyedropper or a... So you’d render it in canvas, make them all smashed together into a single painted layer, and then go pluck the single pixel value out to see what its actual end computed gray is after it’s been layered on the other stuff.

<span class="smashing-tv-speaker">Adam:</span> I think someone specced it, or maybe I have it as a GitHub issue that it would be nice. Because VisBug could facilitate this, 100%. VisBug, behind the scenes, I’ve already done with text metrics, where you hover on things and it gives you crazy rad information about the fonts. It’s almost too much info, like x height, and cap height, but it goes even more. And it’s like, "Ooh, I’m kind of turned off at a certain point." So I have to figure out how to find the signal versus noise there.

<span class="smashing-tv-speaker">Adam:</span> But yeah, I like this thought process, because we should have a tool that does that. And if we know how to compute it, we can teach VisBug to do it, and that would be a really cool feature to have, opacity relevant calculated color. Love it.

<span class="smashing-tv-host">Drew:</span> Yeah, I mean, it’s the sort of standard case of having text against a background where you’re not sure if the contrast is enough to pass the accessibility requirements. And perhaps it’s not, perhaps it’s too low contrast and you want to then tweak the values until you get it just to the point where the contrast is good, but it’s not drifted too far away from what the client initially wanted in terms of brand colors and things.

<span class="smashing-tv-speaker">Adam:</span> I call that bump, bump until you pass.

<span class="smashing-tv-host">Drew:</span> Yeah.

<span class="smashing-tv-speaker">Adam:</span> Because that’s what it feels like. I’m like, "Ooh, I’m a little short on the score." So it’s like, I’ll go to my HSL lightness and I’ll just bump, bump, bump, and watch the little numbers tick up until it’s like, "Ding," I got a green check mark. I’m like, "Okay, cool." And yeah, sometimes, some of that color is not cool. So, have you studied much of the 3.0 perceptual accessibility work that’s going on? So that we’ll no longer have AA or AAA, we’ll have on number and it includes things like font thinness. So if it’s a thin font it will get a lower score, if it’s a thick font it goes... Because there’s a lot that goes into contrast.

<span class="smashing-tv-host">Drew:</span> Yeah, no, I hadn’t seen any of that, but that sounds-

<span class="smashing-tv-speaker">Adam:</span> Anyway, it’s a really cool thing to explore.

<span class="smashing-tv-host">Drew:</span> That sounds fascinating, yes. I’ll have to find someone to talk to about that. That’s another episode. So, I mean, I’m sure some developers might argue that everything that VisBug is doing you can just do through the CSS panel in DevTools. And I think that’s sort of fair but probably misses the point, in that, yes, you are manipulating CSS when you’re making changes, but it’s putting a sort of designer-focused user interface on top rather than a developer-focused interface. Is that a fair characterization of it?

<span class="smashing-tv-speaker">Adam:</span> That’s a really fair one. And honestly, the best ideas graduate out of VisBug into DevTools. And they already have. So VisBug, if you hit command option C on any element it takes every computed style, at least that’s unique. Again, so it’s like, we’ll do ones that we’re not just going to give you all these inherited properties. But puts them all on your clipboard, and you can go paste that style somewhere else, in a style sheet, in a CodePen, and literally recreate the element in a couple clicks.

<span class="smashing-tv-speaker">Adam:</span> And those sort of interactions have made their way into DevTools, into that elements panel. There’s other things, though, that haven’t, which is, the DevTools is a single node inspection only tool. And VisBug follows the design tool mantra which is, no, I should be able to multiselect. I need to be able to bulk edit, bulk inspect. And so I use VisBug all the time for spacing. Because I can highlight multiple elements and see margin collapsing.

<span class="smashing-tv-speaker">Adam:</span> In DevTools you can’t ever see it, because you can only see one node at a time most of the time, although there’s way to show multiple margins, but it’s not the same. And so, yeah, it has these niche use cases that can be really fun like that. Another one is, if you highlight a... Let’s say you have a typography system and you have H1 through H7, like in a storybook or something like that, you can highlight all of them in VisBug, hold shift, just click all of them. Boop, boop, boop, boop, go to the typography tool and hit up or down, and it makes a relative change to each of them.

<span class="smashing-tv-speaker">Adam:</span> So each of them will nudge up one or down one. And that’s just not something that DevTools makes very easy. And so, yeah, it has some superpowers like that, because it’s a little more agnostic. And it’s prepared to always iterate on an array. Yeah.

<span class="smashing-tv-host">Drew:</span> So what was the origin of VisBug? And now is it just a personal project? Or is it a Google project? Or what’s the status of it?

<span class="smashing-tv-speaker">Adam:</span> Yeah. So first, status is, it is a Google project. Its primary goal is to be a place to prototype and explore before things go into DevTools. At least from the Google side of things. But from my personal side of things I still see it as a place to go bake in the common tasks, or to bake in some optimizations to get through common tasks. And just to give a wider audience a way to look into the DOM.

<span class="smashing-tv-speaker">Adam:</span> I really think that the DevTools is super powerful, but it’s very intimidating. Just one tab in it can take a career to learn. I’m still learning things in DevTools, and I use them all the time. And so yeah, this is kind of a different audience in some ways. It’s more of the beginners, the folks coming in, or maybe even folks like PMs, managers, that don’t ever intend to code but are interested in the output. And so it kind of gives them, yeah, just light tooling to get into there.

<span class="smashing-tv-host">Drew:</span> It’s an interesting point you bring up, because I personally often find that I struggle to find a comfortable workflow in managing all these sort of DevTools. And you’ve got all these little claustrophobic panels, and you can detach them into another window, but then you’re having to keep track of two different windows. And once you’ve got a few browser windows open you can’t... You focus one and you don’t know which DevTools belongs to it.

<span class="smashing-tv-host">Drew:</span> And then within the panels themselves, it’s kind of a sort of a bit of a Wild West of user interface conventions. You’ll scroll and things’ll start doing strange things that you didn’t expect. And in terms of user experience I feel like it’s all just a big mess.

<span class="smashing-tv-speaker">Adam:</span> It is. Yeah.

<span class="smashing-tv-host">Drew:</span> Do you think that’s unavoidable? Can it be better?

<span class="smashing-tv-speaker">Adam:</span> I definitely have thoughts here. And yeah, I think a good... So let’s say you have a listener right now that’s like, "I’m pretty savvy with the DevTools. I don’t think they’re that crazy." I’d say, "Okay, go open up Android Studio or Xcode. Begin a project, and go look at the DevTools, go look at the output. How familiar do you feel right now?" Probably very foreign. You’re looking at that going, "This is garbage. Why do they do this? Why is this panel over here?" And your mind starts to race with all these questions why and confusion.

<span class="smashing-tv-speaker">Adam:</span> And it’s like, well that’s how everyone feels the first time they open DevTools. So you got to really kind of be empathetic to that.

<span class="smashing-tv-host">Drew:</span> Is it inevitable that... Can we do better? Or is this just the sort of natural order of things?

<span class="smashing-tv-speaker">Adam:</span> So here’s my current take on this, is I think complexity is really easy to find yourself getting into. And DevTools is one of those things, they’re just naturally complex. There’s no good UI to facilitate a lot of these things. A lot of these things get built by devs. And I think devs building tools for devs is fine, because you’re going to have... If it’s the only way, or if it’s even if it’s a good way, you’re going to learn it, and you’ll get good at it, and you’ll get comfy with it.

<span class="smashing-tv-speaker">Adam:</span> And all DevTools are kind of weird, because they’re made for their weird use cases, right? Development is weird. Let’s just be honest. We make invisible cogs and invisible two by fours, and we build houses, basically, with invisible, virtual parts. So yeah, we need weird tools to go inspect these things, and to tell us what they’re outputting.

<span class="smashing-tv-speaker">Adam:</span> Now, that being said, what VisBug does, and what I’ve been kind of slowly moving things into DevTools as, is smaller tools that are more focused as opposed to a big tool that claims to do a lot. I think it’s hard for things to do a lot really well. And this is classic argument, right? This is all stars, specialists versus generalists. Neither are always going to be perfect.

<span class="smashing-tv-speaker">Adam:</span> But what VisBug is trying to do is, it has made specialists. So the guides tool just does guides. And that tool never leak into the other tools of the page. And so I’m trying to do that more with DevTools, where DevTools wants to help designers more, which is something VisBug has helped inspire DevTools to see. And the way that I keep introducing things is, instead of making a grid editor, for example, where you can... "Full power of grid in one overlay," right? "You can add tracks, remove tracks, blah, blah, blah."

<span class="smashing-tv-speaker">Adam:</span> And I’m like, "That sounds really cool and also really complex." I’m like, "Grid is crazy, there’s no way we’re going to build a GUI for that." So I’m like, "Why don’t we just handle grid template columns first, and the ability to manage the tracks in there, almost like they’re chips? What if we could just add, and edit, and delete them?" They’re much more physical and less of string. I’m like, "Well what we’ve done is, we’ve created a micro-experience that solves one problem really well and then doesn’t leak anywhere else, and it’s also really naïve. It’s a naïve tool."

<span class="smashing-tv-speaker">Adam:</span> So and a good example of that is the angel tool in DevTools. Have you seen that tool yet?

<span class="smashing-tv-host">Drew:</span> No, I haven’t.

<span class="smashing-tv-speaker">Adam:</span> Any angle... So this is, I’m calling these type components. So their CSS is typed, and the angle is a type, and many CSS properties will take a type value of angle. And what I was like... Well, angles, those are just a wheel like a clock. Why don’t we give someone a GUI so that if they click an angle they can change an angle and snap it to 45, snap it to 90, there’s common interactions with just this unit of angle.

<span class="smashing-tv-speaker">Adam:</span> And we made a tool for it. And it’s super cool. It looks great, the interaction is great, keyboard accessible the whole nine, and that’s an example where I think you can make small focused things that have big impact, but don’t necessarily solve some big problem. And yeah, you’ll have another tool like Webflow that’s trying to create entire design tool and facilitate all your CSS.

<span class="smashing-tv-speaker">Adam:</span> So, yeah, I don’t know the right answer, but I do know that an approachability factor comes in when things do less. And so it just kind of makes it a little easier. Like VisBug, you might only know three tools on it. You only use the guides, the margin tool, and then the accessibility inspect tool. Maybe you never use the move tool or the opposition tool. Just, yeah.

<span class="smashing-tv-host">Drew:</span> I mean, talking of design tools, we’ve seen a big rise in the last few years of tools. Things like Figma, which are great for originating new design work in the browser. Is there overlap there with what Figma is doing and what VisBug is trying to do?

<span class="smashing-tv-speaker">Adam:</span> There’s definitely overlap. I think they come at it from different directions. One of the things that I’m frustrated with Figma at is not something that VisBug could solve. And I think that design these days, even with the powerful tools and the Flexbox-like layouts that we have, I still think we start wrong when we draw a box on a canvas of a certain size. I’m like, "Sorry, that’s just not the web. You’re already not webby."

<span class="smashing-tv-speaker">Adam:</span> Nothing is very content-focused. If I just drop a paragraph into Figma, it gives it some default styles and I’m like, "Why doesn’t it do what the web does? Put it in one big long line." You’re like, "Contain it somehow," right? And so I don’t know. I think that Figma is empowering people to be expressive, limitless... What is the phrase I like to use? Yeah, okay, it’s expression-centric. That’s where I think VisBug and a lot of debug tooling is...

<span class="smashing-tv-speaker">Adam:</span> So yeah, one is empowering expression, and the other one is empowering inspection and augmentation. You need both, I think. I think that in one cycle of a product you’re in full expression. You need to not have any limiters. You need it to feel free, create something exciting, something unique. But then as your product evolves and as more teammates get added, and just the thing grows and solidifies, you’ll exit a phase of expression and into a phase of maintenance, and augmentation, and editing.

<span class="smashing-tv-speaker">Adam:</span> At which point your Figma files do two things, they get crusty, because your product is more... Well, it’s real. Your product has made changes, and design decisions, because it’s now in the medium. And so your file starts to look crusty. And then your file also just is constantly chasing production. And that’s just a pain in the butt. And so VisBug is sort of waiting. So in the expression phase VisBug’s like, "I can’t help you very much. I’m just sort of, I’m not that powerful at expression."

<span class="smashing-tv-speaker">Adam:</span> But then as you have a real product you can inspect it. And yeah, it can inspect anything. It has no limits. It goes into shadow DOM and everything. So yeah, I think they’re just different mentalities for different phases of products, yeah.

<span class="smashing-tv-host">Drew:</span> So in VisBug if you have made a whole lot of changes, maybe you’re sat with a client and you’ve tweaked some spacing, and you’ve changed some colors, and you’ve got it looking exactly how the client wants, they’re happy. They obviously now think that all the work has been done.

<span class="smashing-tv-speaker">Adam:</span> It’s done.

<span class="smashing-tv-host">Drew:</span> Which of course, it’s not. We understand that. But what is the path? What is the developer journey from that point to... I mean, I presume that it’s not practical to save or export, because there’s no way to map what you’re doing in the browser with those source files that originated that look. But what’s the journey? How do you save, or export, or is it, I guess, taking a screenshot? Or what do you do?

<span class="smashing-tv-speaker">Adam:</span> Yeah, there’s a couple paths here. And I want to reflect quickly on what we do in DevTools. So let’s say, DevTools, we made a bunch of changes, there is the changes tab in DevTools, I don’t think very many people know about it, which will surface your source file changes, and some other changes in there that you could go copy paste.

<span class="smashing-tv-speaker">Adam:</span> And yeah, this becomes a hard thing with all these tools that are editing code output, they don’t have any knowledge of source or authoring files. I mean, maybe they have source maps, but I think that’s a really interesting future. If we get to something where the calculated output could be mapped all the way back to the uncompiled source, that’d be really cool. But until then, VisBug does do similar to what you do in DevTools. Where you just copy paste the sort of pieces.

<span class="smashing-tv-speaker">Adam:</span> But I will share some fun ways to sort of make it even better. So one thing, let’s say you made a header change, color change, and a change over here. You can go to the inspect tool, and when you hover on something it will show you a delta. It’ll say, "Local modifications." And if you hold shift you can create multiple sticky pinned inspections. And so you’ll go to your header, you’ll click it, you’ll hold shift, click your other little box, and hold shift to click another little box. And now you have tool tips showing what you changed over the actual items in the page, take a screenshot, and ship it to a dev.

<span class="smashing-tv-speaker">Adam:</span> And they can sort of say, "Okay, I see you changed margin top to 20 pixels. I don’t use pixels or margin top in my CSS. So I’ll go ahead and change to margin block start two RAM, thank you and bye bye." And that’s kind of nice, is that the editor didn’t have to care or know about the system details, they just got to say something visually and screenshot it. So that workflow is nice. It’s pretty hands off and creates a static asset which is fine for a lot of changes.

<span class="smashing-tv-speaker">Adam:</span> But if you had a lot of changes and you really changed the page and you wanted to save it, there is another extension called... Let’s see. Page, single file. Single file will download the entire current page as a single file HTML element, at which point you could drag that right into Netlify and get yourself a hosted version of your prototype.

<span class="smashing-tv-speaker">Adam:</span> Because what VisBug does is, it writes its styles in line on the DOM notes themself. So save file comes with it all. And I’ve got a tweet where I went to GitHub and I made... I just totally tweaked the whole site, and it looked cool. And I was like, "All right, save file." And I saved it, opened it up in a new tab, just dragged it into the new tab and I was like, "Well this is really cool." Because VisBug’s been wanting a feature like this for a while. But it’s a whole other extension’s responsibility, is taking those third party assets, dealing with all the in line... And anyway, so it’s really nice that that exists.

<span class="smashing-tv-speaker">Adam:</span> And so you can deliver a file, if you want to, or host it somewhere, and share multiple links to multiple versions of production. You modified production and then shipped it into netlify, and someone can go inspect it, and it’s still responsive at that point too, right? At that point it’s not a static comp you’re sharing, it’s still the live, responsive... Anyway, it’s exciting. I mean, there’s a future here that’s, I think, really, really interesting and not far away.

<span class="smashing-tv-speaker">Adam:</span> It’s just like we’re a little still stuck, as designers, in our expression land. We’re just too happy expressing. And we’re dipping our toes into design systems, but even those I think are starting to get a little heavy for designers. And they’re like, "Ooh, maybe it’s too much system now." And like, "Ugh, I’m getting turned off. I liked making pretty stuff. And it’s a whole new job if you’re doing design ops," or whatever. So...

<span class="smashing-tv-host">Drew:</span> I like the fact that VisBug takes an approach of not being another DevTools panel, because the interface, it embeds a toolbar on top of your page just like a design toolbar. I guess that was a deliberate move to make it more familiar to people who are familiar with design tools.

<span class="smashing-tv-speaker">Adam:</span> Yep. If you’ve used Paint or Photoshop, they all come that way. And so it was the sort universal thing, that if I put a toolbar on the left that floated over your content, almost everyone’s going to be like, "Well I’ll go hover on these and see what my options are. And here’s my tools. And I get to go play." And it made a really nice, seamless interaction there. I do have a really exciting almost finished enhancement to this.

<span class="smashing-tv-speaker">Adam:</span> So, it’s so cool to me, but I don’t know if everyone else is going to be as excited. And this’ll be a mode that you can change in your extension settings, is how do you want to overlay the page? Because right now VisBug puts a toolbar right on the browser page, which the page is rendered normal, and I know this is going to be weird to say that, but okay, so you scroll the page, and the content, and the body is width to width in the browser, right? So it’s filling the little viewport.

<span class="smashing-tv-speaker">Adam:</span> I have a mod where, when you launch VisBug it takes the whole HTML document and shrinks it into an artboard. It looks like an artboard. It’s floating on a shadow on a gray space. You can infinitely pan around it. So you can scroll away from your page canvas, and what it lets you do is, see, let’s say you have a page that’s really long, and you want to measure something from the top to the bottom, well you can do that right now, but you’d kind of lose context as you go.

<span class="smashing-tv-speaker">Adam:</span> Well in this new VisBug zoom scenario, you hold option or alt on your keyboard, you use the mouse wheel, or you hit plus minus with your command and you can zoom your webpage as if it’s an artboard. And I try to make it as seamless as it is. So you’re going in and out, and you scroll down, you go in and out, measure from the... And VisBug just doesn’t care. It keeps drawing computed overlays, you can change spacing.

<span class="smashing-tv-speaker">Adam:</span> Because I think it’s really important, as a designer to see the bird’s eye of your page live. Animations are still playing, y’all. Scrollable areas are still scrollable, right? It’s really cool. You’re like, "My whole page in one view." Anyway, so it’s almost done. It’s in-

<span class="smashing-tv-host">Drew:</span> Sounds trippy.

<span class="smashing-tv-speaker">Adam:</span> It’s very trippy. And it’s in, I just need to make sure it works cross browser, because it’s doing some, obviously, some tricky things to make your live page feel that way. But yeah.

<span class="smashing-tv-host">Drew:</span> Amazing. Is it... I mean, I presume that VisBug is fairly regularly updated and is being progressed. What is it that we might expect to see in the future?

<span class="smashing-tv-speaker">Adam:</span> Yep, that’s definitely one of the features I’m working on there. I have a feature where... So, when you click something you get an overlay with what looks like handles, right? And it’s sort of an illusion, it’s supposed to make you feel comfortable. And the intent is to eventually have those handles be draggable. But I have some fundamental things I have to solve first, like elements in the browser don’t have a width. So if you just start grabbing the width I have to do work to make that illusion feel right.

<span class="smashing-tv-speaker">Adam:</span> And you might not even get the results you want, because it could be a block level element that you’re pulling the width smaller, and you’re not getting reflow of an item next to it. And you might be wondering why. So I have prototypes where you can drag corners, drag elements around. But I really need to focus on how the design tools are doing this. They always have this toggle button. And it’s like... See, what’s the toggle called?

<span class="smashing-tv-speaker">Adam:</span> But it’s basically like shrink... I call it shrink wrap. Shrink wrap my element, it’s the width of this element is the width of its content, versus here’s the width of my element, stick something in it. So I need something like that in the browser, overlayed on the element so that you could choose between these and maybe even something that let’s you choose between block and inline, so that you could get the results that you want.

<span class="smashing-tv-speaker">Adam:</span> But ultimately the goal here is that VisBug does not want to be entirely keyboard-driven. I want you to be able to drag spacing. If you see 12 margin spacing on top, you should be able to reach in and grab it, whereas right now you have to hit up on the keyboard to specify the top side of the box needs an addition of margin.

<span class="smashing-tv-speaker">Adam:</span> And so yeah, I have a couple of quirks to work out, in terms of strategy. But it’s very much a goal to make it even closer to design tools. And maybe even I will bend in that. It’s like, well, if you want to change the width and you’re going to get a weird design, there’s always ways to get out of it with VisBug, like the position tool really lets you escape the flow. So flow is ruining your idea, the position tool lets you escape.

<span class="smashing-tv-speaker">Adam:</span> And so there’s... If someone was to get really savvy with VisBug they would blow people’s minds, because it’s sort of unlimited, and it’s like, what can you bring to the table? It has an expression element to it. There is definitely expressive tactics. But anyway, so long story short is, the illusion is, I just want to make it smaller and smaller and smaller. I want the illusion to just be like, "Wow, I’m really feeling like a design tool."

<span class="smashing-tv-speaker">Adam:</span> And then, yeah, some enhancements to exporting would be nice. But also, enhancement to exporting for DevTools would be nice, and that doesn’t really stop us. So I don’t know. There’s a ton of issues, definitely go vote on them. I think one of the next big features I’d love to do is green lines. So instead of just showing accessibility overlays on hover to really indicate some things with green lines, and expose more, and surface more information, and I don’t know. Yeah.

<span class="smashing-tv-host">Drew:</span> Sort of thinking about the process of building a Chrome extension like this, I mean, presuming it’s all implemented in JavaScript, how much like regular web development is it? Building a Chrome extension.

<span class="smashing-tv-speaker">Adam:</span> That’s good question. It’s... Phew, this is hard one. It’s quirky. First off, the environment that you get to launch your code in isn’t the browser. They don’t really give you full access there. You can, if you really get tricky with it, which VisBug had to graduate into, this even trickier scenario. So right now, I used to execute in the... This is going to get so fuzzy so fast.

<span class="smashing-tv-speaker">Adam:</span> Because there’s multiple sandboxes for your extension, for privacy issues. And they make it hard to execute scripts on the actual page, right? Because you don’t want someone submitting your form when you launch the thing or something, submitting it to themselves or whatever. It could be really destructive. So it has some quirks like that. There’s a bridge you have to pass over. And one of them that’s been plaguing VisBug is, VisBug used to use...

<span class="smashing-tv-speaker">Adam:</span> So it’s all custom elements, and custom elements allow you to pass rich data to them as property. So you’re saying like, customelement.foo=myrichobject, full of arrays or whatever. And the custom element just gets that as some data on the node itself. But since I’m in this weird little sandbox world, if I try to set something unique like that on my object, essentially it’s filtered out. They’ve established that certain things can’t... So I can pass a string to my custom element, but I can’t pass it a rich object.

<span class="smashing-tv-speaker">Adam:</span> But yeah, other than little quirks like that, once you get the flow down, and if you spend the time to get a rollup scenario, which is going to be an hour or so of work so that you give LiveReload in your thing, it can become pretty natural. I think Firefox has, honestly, the best extension development experience if you’re savvy with the CLI you can spin something up with one command, and it installs it, gives you these LiveReload features, and gives you debugging tools. It kind of holds your hand through it, it can be really nice.

<span class="smashing-tv-speaker">Adam:</span> But ultimately, it’s a little quirky. That’s why I do a lot of the work on that demo site that looks like a bunch of artboards, because I don’t really need a real webpage most of the time, to do VisBug testing, as long as I’ve got artboards that simulate various issues, or have accessible things to look at, and sort of give me the content I need to see. I do a lot of the work right there in the browser as if it’s just a normal web application. So VisBug’s dev experience is really easy, unless you’re trying to test it across browser, and then it just gets kind of messy and whatever.

<span class="smashing-tv-host">Drew:</span> That’s really interesting insights. So I’ve been learning all about VisBug today, what have you been learning about lately, Adam?

<span class="smashing-tv-speaker">Adam:</span> I am still improving my wok skills. So I want to be a wok man, and I’m not talking the ’90s cassette player. I’m want to flip veggies and have them kind of catch fire a little bit in the air, cover them with some delicious spices, and just really sear up that garlic and make it crispy delicious. And then put it on a little bed of rice and slide it towards you and see what you think.

<span class="smashing-tv-speaker">Adam:</span> So I’m excited for summer right now, because that means I get to whip out the wok and get back into that fast-paced, hot cooking environment, and it’s really fun.

<span class="smashing-tv-host">Drew:</span> Amazing. That sounds delicious. If you, dear listener, would like to hear more from Adam you can follow him on Twitter where he’s @argyleinc, and find his personal website at nerdy.dev. If you want to give VisBug a try, you can find it in the Chrome Web Store, and you can try out the sandbox version at visbug.web.app. Thanks for joining us today Adam. Did you have any parting words.

<span class="smashing-tv-speaker">Adam:</span> No, you were really nice. This was really sweet. Thanks for having me on, I really appreciate it.

{{< signature "il" >}}