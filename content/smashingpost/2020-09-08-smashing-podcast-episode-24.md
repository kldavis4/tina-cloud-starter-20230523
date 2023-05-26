---
title: 'Smashing Podcast Episode 24 With Cassie Evans: What Is SVG Animation?'
slug: smashing-podcast-episode-24
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adb20148-edfd-4320-b248-4e7d4d4faa63/smashing-podcast-episode-24.png
date: 2020-09-08T05:00:00.000Z
summary: >-
  We’re talking about SVG Animation. How can vector images, JavaScript and CSS all work together to provide engaging motion graphics? Drew McLellan talks to SVG expert Cassie Evans to find out.
description: >-
  We’re talking about SVG Animation. How can vector images, JavaScript and CSS all work together to provide engaging motion graphics? Drew McLellan talks to SVG expert Cassie Evans to find out.
categories:
  - Smashing Podcast
  - SVG
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

Today we’re talking about SVG Animation. How can vector images, JavaScript and CSS all work together to provide engaging motion graphics? I spoke to SVG expert Cassie Evans to find out.

<iframe src="https://share.transistor.fm/e/49386a44/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [The SVG Animation Masterclass](https://smashingconf.com/online-workshops/workshops/cassie-evans/) with Smashing Conference
- Cassie on [Twitter](https://twitter.com/cassiecodes)
- Cassie’s [personal website](https://www.cassie.codes/)

### Weekly Update

- “[How To Do More With Vue Router](https://www.smashingmagazine.com/2020/08/vue-router-features/)”  
*by Timi Omoyeni*
- “[Building React Apps With Storybook](https://www.smashingmagazine.com/2020/09/building-react-apps-storybook/)”  
*by Abdulazeez Adeshina*
- “[Everything Developers Need To Know About Figma](https://www.smashingmagazine.com/2020/09/figma-developers-guide/)”  
*by Jurn van Wissen*
- “[4 Ways To Creatively Use Icons In Your Mobile Apps](https://www.smashingmagazine.com/2020/09/icons-mobile-apps/)”  
*by Suzanne Scacca*
- “[Building A Component Library With React And Emotion](https://www.smashingmagazine.com/2020/08/component-library-react-emotion/)”  *by Ademola Adegbuyi*

## Transcript

<p><a href="https://twitter.com/cassiecodes"><img loading="lazy" decoding="async" style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62c177e1-a711-4547-ac2c-16d7737cd5bb/cassie-evans-200x200.jpg" width="200" height="200" alt="Photo of Cassie Evans" /></a><span class="smashing-tv-host">Drew McLellan:</span> She is a front end developer and speaker with a background in graphic design and motion design. She got started with coding back in the days of MySpace and Neopets and is on a mission to make the web more whimsical again. She currently works at Clearleft in Brighton UK, and can usually be found tinkering with SVGs on CodePen. So we know she’s a skilled developer and SVG expert, but did you know she was National Junior Wing Walking Champion for three years in a row? My smashing friends, please welcome Cassie Evans. Hello Cassie. How are you?</p>

<span class="smashing-tv-speaker">Cassie Evans:</span> I’m smashing, thank you.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you today about one of your passions, which is SVG, and in particular the animation side of things. I think most people listening to this podcast will have heard of Scalable Vector Graphics in some shape or form. I know I’ve used them heavily with things like logos and icons in recent years, but let’s not assume. So for anyone who isn’t really up to speed with SVG, what makes it different from other ways of adding graphics to a webpage?

<span class="smashing-tv-speaker">Cassie:</span> So, a lot of the clue’s in the name, of course. So, SVG stands for Scalable Vector Graphic. So, these are first the images that can be any size. You can make them really, really small or really, really big, and they’ll retain image quality and won’t get pixelated like JPEGs or PNGs.

<span class="smashing-tv-speaker">Cassie:</span> You can also make them really, really small, so small in file size. So, everyone’s kind of added a PNG to their site that’s a million megabytes and seen what that does to page load. So, you can add all sorts of cool illustrations and stuff to your site without impacting on performance too badly, and also you can animate them so that’s the most exciting bit. With JPEGs or PNGs, if you wanted to animate them or move bits of them around, you’d have to cut them out into little pieces or kind of layer them on top of each other, whereas with SVGs you’ve got actual elements in the SVG. It’s got a DOM structure just like HTML does.

<span class="smashing-tv-host">Drew:</span> So, I guess in a world of mobile devices with different screen sizes and different pixel densities and sort of constrained data connections, SVG really is a format that’s more suited to the modern web than the old graphic styles. Is that fair?

<span class="smashing-tv-speaker">Cassie:</span> Yes, definitely.

<span class="smashing-tv-host">Drew:</span> Most images are of course sort of binary based, but SVG is totally view sourcable, isn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yeah. So, that’s really exciting because you can actually right click and view source on an SVG and you can traverse around the DOM and kind of see what you’ve got and kind of get to learn it that way, which I find that really great. It feels a lot like the old web, like being able to go to a website and view source on it and see how it’s put together.

<span class="smashing-tv-host">Drew:</span> SVG kind of feels more sort of native and integrated into the web than things like maybe Canvas or even back in the day Flash, which of course flash was scalable vector graphics, wasn’t it? In its own way. And those technologies feel very much like a black box that’s encased on the page that you can’t sort of get in or out of. SVG is a lot more integrated isn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yeah. It’s funny that you’d say that because I always refer to Canvas as a black box when people are asking whether they should use Canvas or SVG for something. I think a lot of the time, obviously it depends on the use case, but one of the things with Canvas is if you don’t have JavaScript for some reason, if your code fails, you end up with a little black box with nothing in it. So you could create this crazy infographic, all sorts of things going on inside this Canvas element, and then you just lose it all. Whereas SVG, it’s a lot more aligned with progressive enhancement, so you can have an animated SVG, maybe that’s animating using JavaScript, but then without JavaScript you will still have the illustration. You’ll still have the SVG there.

<span class="smashing-tv-host">Drew:</span> And SVG isn’t new to the web, is it? It’s been around for quite a while.

<span class="smashing-tv-speaker">Cassie:</span> It has, yes. It’s been around for longer than I’ve been doing stuff on the web.

<span class="smashing-tv-host">Drew:</span> And it certainly seems to be coming into its own a lot more with things like animation, like you’ve been saying, but also as we were mentioning, the way that it scales just makes it perfectly suited when we’re designing sites that might be viewed on a retina display with double the pixel density, or need to be delivered over a mobile connection where you want things to be as performant as possible. So we know SVG has got a DOM, you mentioned that. Does that mean that the things in it can be manipulated with code?

<span class="smashing-tv-speaker">Cassie:</span> Yes, so that’s the most exciting thing. You can get at SVG elements and you can animate them and move them around just like you can with HTML DOM elements, and it also means from an accessibility perspective, SVG has a DOM so you can traverse that DOM if you’re using a screen reader or something, so you can make SVG graphics very accessible to screen readers.

<span class="smashing-tv-host">Drew:</span> Yes, so I was going to ask about the situation with accessibility because classically, graphical stuff on a page is one of the most difficult things to make accessible. So are there sort of attributes that you can add to hint? Can you use the ARIA stuff in SVG or how does that work?

<span class="smashing-tv-speaker">Cassie:</span> Yeah. You can use ARIA labelledby, but you also have title and description tags that you can put inside an SVG.

<span class="smashing-tv-host">Drew:</span> That’s incredible and in terms of sort of motion preferences, because that’s something that we’ve seen recently with a media query in CSS to see that the user prefers reduced motion and you can change your animations and things based on that, is that something you can do in SVG or does it have to be implemented a little bit more manually?

<span class="smashing-tv-speaker">Cassie:</span> Well with SVG people often talk about SVG animation like it’s its own separate kind of special thing and of course we used to have SMIL. We still do have SMIL technically. It was getting deprecated, but it’s actually not being deprecated anymore. It’s just not really as widely used and not worked on anymore, but we used to have SMIL and that was what most people refer to as SVG animation. Whereas now, SVG animation could mean any of those things. It could mean SMIL, it could mean CSS animation, or it could mean animating using JavaScript or a JavaScript animation library. So, there’s lots of different options but with CSS animation and JavaScript animation the option to use prefers reduced motion is there and should definitely be used.

<span class="smashing-tv-host">Drew:</span> So you mentioned CSS animation and of course there’s a certain amount that we can do, like with HTML elements and CSS animation, to create graphics and motion on a page. SVG just like blows that out of the water in terms of flexibility doesn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yeah, definitely. I think people make amazing things with just CSS, like Lynn Fisher makes really amazing things. There’s all sorts of people making crazy CSS only illustrations, but it takes a lot of time and the handover for that is pretty impossible. Like if you imagine a designer giving you an illustration and asking you to recreate that in a CSS, that would be a large ticket. So SVG kind of makes it a lot more feasible to have these interdisciplinary teams and pass things over from one person to another. So you can have an illustrator or a designer create an illustration in a vector graphics program like Illustrator, and then they can pass that SVG over to a developer who can animate it.

<span class="smashing-tv-host">Drew:</span> And I suppose that would fit quite well into people’s established workflows. We’re using things like Git, because SVG is text-based, isn’t it? So presumably, committing SVGs into Git you get all that ability to diff and merge and all those sort of powerful features that you get with other text-based stuff. Is that right?

<span class="smashing-tv-speaker">Cassie:</span> Yeah, exactly.

<span class="smashing-tv-host">Drew:</span> So it’s kind of like, well I say kind of like, it absolutely is graphics expressed as code.

<span class="smashing-tv-speaker">Cassie:</span> Yes.

<span class="smashing-tv-host">Drew:</span> Isn’t it? SVG?

<span class="smashing-tv-speaker">Cassie:</span> It is.

<span class="smashing-tv-host">Drew:</span> And it’s quite a lot like HTML in its syntax. It’s another XML based language, isn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yep.

<span class="smashing-tv-host">Drew:</span> So it has tags and attributes and nested children and all that sort of stuff that your average web developer is going to be used to.

<span class="smashing-tv-speaker">Cassie:</span> I think that that’s what I love the most about SVG is I’m really into creative coding and also teaching people, and I found that teaching people who are more of a creative leaning, they sometimes get a little thrown off when you immediately jump in with JavaScript or Python or something like that for creative coding, but without fail I’ve managed to get anyone that I taught on board with SVG because it’s got this really approachable entry points because it does look like HTML. So, you can give someone with an understanding of HTML and how to build websites SVG, and it looks the same, but it’s the graphics instead of documents and then you can animate that with CSS to start off with which is also a little bit more comfortable, and then you can kind of progress to animating it with JavaScript. So it’s a really good learning curve.

<span class="smashing-tv-host">Drew:</span> And of course it can be dynamic. It’s not just a case of creating motion. You can actually make the properties of it dynamic. So, one of the interesting things I’ve seen SVG used for, and it’s a grand term, but like data visualization, DataViz, and drawing graphs and charts and of course things like dashboards that we seem to have everywhere these days. SVG is sort of perfect for that isn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yes, definitely. SVG is great for DataViz. All the way from kind of small DataViz up to D3 which is very well known DataViz library that uses SVG under the hood. But you could also just, if you’ve got a little bit of data that you wanted to show on a web page, you could create a chart in a graphics editing program and then you could just use JavaScript to change those values and kind of change how your graph looks. So you don’t have to go all in with a massive database library. You can kind of just start off small.

<span class="smashing-tv-host">Drew:</span> Obviously sort of traditional graphs and charts and things are just sort of the tip of the iceberg when it comes to ways that SVG can help with data visualization. I saw you had an interesting project that you did at Clearleft with your solar panels on the roof. Can you tell us a little bit about that?

<span class="smashing-tv-speaker">Cassie:</span> That project was actually meant to be me learning D3 and then I got very distracted. We have some solar panels on the roof of our office, which I miss thoroughly actually it’s been so long, but yeah we’ve got some solar panels on the roof and I found out shortly after starting working at Clearleft that we had an API that was attached to the solar panels that you could hook into. So I was like...

<span class="smashing-tv-host">Drew:</span> Amazing.

<span class="smashing-tv-speaker">Cassie:</span> Right. I need this to be my side project, and I had a little look at what we got back from the API and amongst the data there was the amount of CO2 saved and they measured the amount of CO2 in trees.

<span class="smashing-tv-host">Drew:</span> Okay.

<span class="smashing-tv-speaker">Cassie:</span> So I was immediately like, wow, well we’re going to have to plot this somehow, but I want to measure it in trees because that’s such an interesting way of plotting this. So, all of my D3 aspirations went out of the window and I sat down in illustrator and recreated an illustration of our office building and created a jungle of trees and plants and stuff, and then I’m looking at how much CO2 we have saved and then kind of growing in these plants and vines and stuff. Yeah, it’s great. It’s really good to check back occasionally as well and just see how much the jungle’s grown.

<span class="smashing-tv-host">Drew:</span> It’s an amazingly creative way of visualizing that data, whereas if you were relying on traditional software for creating graphs and charts and things, there’s never going to be a function to create an office building with trees on top. That that just doesn’t exist, but then using JavaScript and using SVG to be able to generate those graphics and using the JavaScript to manipulate them to adjust the values that are being shown, you can come up with something completely new in a completely novel way of communicating an idea to the person using the site. So, we know we can hand codes the markup for SVGs, which me as a developer, I think that sounds great because I can go in and I can be very precise, but that is probably a technical skill that isn’t going to suit everybody, particularly those whose strengths being more visually creative than actual coding. So are there other ways to author SVGs or do you have to just do it by hand and in a text editor?

<span class="smashing-tv-speaker">Cassie:</span> I think I wrote a hamburger icon once just from the top of my head and I was super proud of myself, but the rest of the time I create SVGs in Illustrator or other alternatives. Affinity designer is really good. Illustrator has obviously the Adobe pricing structure, which can be a little bit out of people’s budgets, but Affinity Designer is like a once off purchase and it’s pretty good actually, and the SVG markup that you get out of it is good which is the most important thing. But yeah, I don’t think there’s anyone apart from, it’s a guy called Blake Bowen on the GreenSock forums, and I think that he could probably hand write SVG path data, but I don’t think it’s a thing that everyone can do. I don’t think that it’s a thing that we should be aspiring to do. It’s quite verbose.

<span class="smashing-tv-host">Drew:</span> So being a lightweight by using a dedicated graphics tool to author SVGs, it’s a perfectly valid route.

<span class="smashing-tv-speaker">Cassie:</span> It’s fine. Choose your battles.

<span class="smashing-tv-host">Drew:</span> Are there any tools out there that are free for filtering SVGs or is it all commercial?

<span class="smashing-tv-speaker">Cassie:</span> I think Inkscape is free, but yeah, I would really recommend Affinity Designer. I think for the kind of cheaper tier, I think it’s worth paying a little bit of money towards these tools because it can be quite frustrating working with clunky vector graphics tooling.

<span class="smashing-tv-host">Drew:</span> In terms of the output, the SVG output that you get from these tools, is it all the same? Do they all just basically generate the same SVG or some better than others?

<span class="smashing-tv-speaker">Cassie:</span> Yeah, that’s a very good question. I find Illustrator is a lot better than other tools, but it’s not something that should hold you back or make you feel like you need to spend that money. So at the end of the day you’ll get some markup out, some editors you might need to do a little more tweaking than others but most of them you will get workable SVG code out of it.

<span class="smashing-tv-host">Drew:</span> I’ve found personally when I’ve tried to create SVGs, and I’m not graphically skilled, that I get varying results depending on how I actually draw something in say Illustrator. Presumably when it comes to thinking about how something’s going to be animated, it matters more how you construct your shapes in the editors. Is that fair?

<span class="smashing-tv-speaker">Cassie:</span> Yeah, definitely. Also SVG has an implicit drawing order, so it’s not like HTML. So with HTML, you can use that index to kind of move things around and put things underneath or on top of other things, whereas with SVG the order that it is in the code will be the order that it is displayed on the web page. So that’s something to kind of keep in mind when you’re drawing out an SVG is getting your layers in the right order and then anything that you want to move as one unit you should wrap in a group and anything that you want to move separately from something else you need to make sure that it’s actually a separate shape.

<span class="smashing-tv-host">Drew:</span> Yeah, so I mean by getting your layers in order there you’re literally talking about the layers palette in Illustrator and dragging the things around before you export, is that right? Just getting them in the correct order and then exporting.

<span class="smashing-tv-speaker">Cassie:</span> Yes.

<span class="smashing-tv-host">Drew:</span> And once you have exported it are there tools that will help sort of optimize or, because I know with PNGs, there’s a whole load of things I use to cut all the craft out of the file and reduce the file size. Are there’s similar things for SVG?

<span class="smashing-tv-speaker">Cassie:</span> Yeah. There’s a tool called SVGOMG, which I use a lot, which is great and you can use that for batch processing. There’s terminal commands for it, but you can also, there’s a Gooey in the browser, which I really like for large illustrative SVGs because I think it’s nice to build it into, say your build process, if you’re dealing with a huge load of icons that you all want processed in the same way, but if you’re dealing with an illustrative SVG, it’s nice to be able to use the gooey because you can flip between the code view and the visual view and you can just make sure that the things that you’re changing in the settings aren’t visually affecting your SVG in a negative way and aren’t affecting the code in a way that you don’t want it to.

<span class="smashing-tv-host">Drew:</span> Presumably these tools, things like Illustrator, are great for creating graphics, but they’re not going to help us at all with animation are they? That all happens once we get the SVG and put it into a webpage.

<span class="smashing-tv-speaker">Cassie:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> So what does that process look like? I mean, obviously it’s difficult to talk about animation too much on an audio podcast, but in terms of just the sort of process you’d go through. You put your SVG into a page, what happens then? How do you address parts of it or what do you do to start working with it?

<span class="smashing-tv-speaker">Cassie:</span> So it’s very similar to animating HTML DOM elements in that you need to be able to target the elements themselves. So that would involve putting classes or IDs on them so that you can target them, and then you can either use CSS for animation. There are some issues with transforms with CSS that are still kind of being ironed out a little bit. So I tend to recommend CSS for experimenting and playing with SVG animation. When it comes to SVG animation and production I will usually recommend GreenSock, which is a JavaScript animation library, and yeah, well with GreenSock and with CSS you basically just get the SVG elements and then do stuff to them.

<span class="smashing-tv-host">Drew:</span> So do you have full access to interacting with the complete range of JavaScript APIs and things like scroll events and mouse events and resizing and intersection and that whole browser environment presumably you’ve got at your disposal, to then have your animation interact with and respond to.

<span class="smashing-tv-speaker">Cassie:</span> Yeah. So anything that you would use in normal JavaScript, so like mouse events or scrolling, that kind of thing, you can look for that and then do things to your SVG on those events. You’ve also got SVG specific methods and stuff, like get PATHlink I think is one, stuff like that so there’s specific SVG methods that you can kind of play around with.

<span class="smashing-tv-host">Drew:</span> So you could do things for example, like start an animation as an SVG comes into view on the page if it’s scrolled out of place and stop it when it gets scrolled away and restart it if it comes back into view and that sort of thing.

<span class="smashing-tv-speaker">Cassie:</span> Yeah. There’s actually a new GreenSock plugin called ScrollTrigger and previously I think a lot of people have used ScrollMagic for scroll animations, but that was a different library to GreenSocks, so they had no kind of affiliation with each other so you were just mashing together two different libraries, one that did animation and one that did scroll events. Whereas GreenSock have now just made a scrolling plugin that works with GreenSock and it has one event listener. One scroll listener. Yeah. So it’s very, very performance and I’ve played around with it recently and it’s great. It’s really easy to use.

<span class="smashing-tv-host">Drew:</span> Is that automatically buffered so you’re not completely overrun with scroll events being fired at your code and all those sorts of traditional problems?

<span class="smashing-tv-speaker">Cassie:</span> Yeah all of the traditional problems, they’re kind of doing all the heavy lifting in the background for you, which is good.

<span class="smashing-tv-host">Drew:</span> Fantastic. Would GreenSock be the tool then, the sort of library, that you’d recommend people to start using if they were looking at SVG animation?

<span class="smashing-tv-speaker">Cassie:</span> Yes, definitely. Mostly because GreenSock, it’s the only animation library out there that handles SVG transforms consistently cross-browser and that isn’t just something that they do that they’re not focusing on anymore. It’s a constant effort from their part so they’re constantly kind of looking for SVG bugs and fixing things. So it’s very reliable. Definitely.

<span class="smashing-tv-host">Drew:</span> What is the sort of cross-browser situation like with SVG? Is it fairly reliable or are you constantly having to deal with inconsistencies across different browsers and platforms?

<span class="smashing-tv-speaker">Cassie:</span> If you are animating with GreenSock then you don't. If you are animating with CSS, yeah there’s quite a few inconsistencies. It’s mostly to do with how transforms are handled. So with HTML DOM elements transforms are measured from the center of them, and with SVG transforms are measured from the top left hand corner, but in some browsers it’s the top left hand corner of the element itself, and in other browsers it’s the top left hand corner of the SVG view box parent. So you can end up, if you’re rotating things around in some browsers, they might end up going in a different trajectory than others.

<span class="smashing-tv-host">Drew:</span> That sounds like most of the animation I’ve ever tried to script. Things going in unexpected directions. We’re used to sort of traditional animation tools, having things like easing options, ease in ease out and that sort of stuff. Presumably that’s something that GreenSock then brings to the table.

<span class="smashing-tv-speaker">Cassie:</span> Yeah. GreenSocks got a lot of really good easing equations that you can use. Yeah, and they’ve got a great ease visualizer so you can have a little look at how will the eases work.

<span class="smashing-tv-host">Drew:</span> That’s really useful, and again that’s something I always struggle with. It’s like, I know I should do something. It shouldn’t just move linearly from A to B, but what do I do? So yeah, being able to visualize stuff is really handy.

<span class="smashing-tv-speaker">Cassie:</span> When I started making animations I made a lot of space animations because I hadn’t quite figured out how easing worked yet, so in space everything does move linearly because it’s just floating around. It doesn’t have gravity to contend with, so I made lots of rockets, planets bobbing around and it was fine.

<span class="smashing-tv-host">Drew:</span> I mean I guess you, being such an SVG enthusiast, you probably see people they’re putting SVG to all sorts of creative uses. What sort of things, just to get the juices flowing, what sort of things have you seen people do with SVGs that has been particularly impressive or creative?

<span class="smashing-tv-speaker">Cassie:</span> I think one of the things that I love with SVG is the fact that you don’t just have to use it for illustrative SVG animations by themselves because it is XML based markup, just like HTML. You can kind of mix it in with the HTML DOM. So, I think it’s a bit of a nerdy thing, but my favorite examples of SVG animation are when people mix SVG animation with semantic DOM elements, so when you have a button that is a proper button but it’s got some SVG icon illustration in it so that when you click that button something joyful happens, and I love that because it’s this perfect marriage of kind of whimsical joyfulness and proper semantic DOM elements.

<span class="smashing-tv-host">Drew:</span> You’ve said in the past that front end development has become very serious in recent times. Has all the fun gone out of the web Cassie?

<span class="smashing-tv-speaker">Cassie:</span> That’s a very serious question. Has all the fun gone out of the way.

<span class="smashing-tv-host">Drew:</span> Because things used to be a lot more fun, but maybe not as efficient and have we got too serious with it?

<span class="smashing-tv-speaker">Cassie:</span> Yeah. I think efficiency is a real killer when it comes to adding these little enhancements on. I find that in my day job at Clearleft, I quickly realized that if I wanted to have animations as an extra thing, as like another ticket or something, it was very hard to get sign off on that. It was always the thing that if the project starts being a little bit cramped on time, it’s the first thing to go. But I think that once you’ve got a good understanding of animation and SVG you can just sneak things in to start off with. So when you’re building a component and you see an opportunity for a little bit of animation and you can just add it in and it gets easier because then people start seeing the possibilities and people start realizing that the clients really like that kind of thing, and then you can kind of get a little bit more time to work on it.

<span class="smashing-tv-host">Drew:</span> It is the sort of thing that can just really elevate an experience beyond unsatisfactory or unsatisfying sort of boring transaction to something that gives the user just a little bit of joy and gives her a whole sort of perception of quality and some brand personality as well, I think with animation. There’s a...

<span class="smashing-tv-speaker">Cassie:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> There’s a lot in terms of brand personality that can be put across with those sort of little touches.

<span class="smashing-tv-speaker">Cassie:</span> But I think this is something that a lot more people are realizing now as well, not just with SVG and animation, but personality in general, and I think that there’s a lot more weight that’s being given to copy that’s written well and has a bit of personality and illustrations that aren’t just from a stock library that are unique to that company or that person and animations are a big part of that. And I think that I personally feel like we’re seeing more of these websites nowadays and I think that we went through, and are probably still going through a little bit of efficiency first period, but I think as with anything people start getting bored of that and it does seem like a lot of websites suggest being churned out by some corporate mega machine and people are starting to push back, I think. Max Bock made a site recently called the whimsical web and it’s got a lot of personal sites on there that are really joyful for various different reasons and I think we’re starting to see a lot more of that.

<span class="smashing-tv-host">Drew:</span> Is it possible to go too far with adding animation and sort of too much personality perhaps to a site?

<span class="smashing-tv-speaker">Cassie:</span> Yes. Definitely. I’m not a huge fan of websites that are very, very, whizbang. Like websites that are animation first. You get to the page and everything’s moving and you’re trying to read text as you’re scrolling, but it’s moving while you’re trying to read it. I’m not a fan of that. I really like looking at animation as an enhancement and I think that’s why SVG, I think is so great because you can kind of build an otherwise quite sensible website, but you can have these little whimsical touches throughout it.

<span class="smashing-tv-host">Drew:</span> And it’s crucial, isn’t it, as we mentioned before, the accessibility sort of aspect of things that it is possible to create a nicely accessible SVG, even if it has sort of content, if you’re locked in there, it’s not locked. It’s accessible to screen readers and then hopefully to everyone who visits the site. As I say, it’s hard on a podcast to really get into the practicalities of, well, we can’t show animation or anything, but you’re running an online workshop with Smashing Conference all about SVG, aren’t you?

<span class="smashing-tv-speaker">Cassie:</span> Yes, I am.

<span class="smashing-tv-host">Drew:</span> It’s the SVG animation MasterClass and that starting on October the eighth and it’s quite an unusual format. It’s two hours on Thursdays and Fridays. That’s an unusual way to do things, isn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yeah. I’m actually really happy about that because I’ve done a version of this workshop before. I spent a large part of 2019 putting it together. It was my baby, my passion project, and then I had quite a few workshops booked in and then the situation happened and all of them got canceled. So I got the opportunity to run it twice before the situation, and it was really great but it was a lot of content and it was a full day workshop. About eight hours and you could tell by the end of it people’s brains are just switching off because you’re sitting in a room trying to absorb information for eight hours. So I’m quite excited about this format because it means that I could divide it up into sections that kind of work by themselves and it gives people a chance to learn that and process it a little bit and let it sink in before they get the next load of information. So I think we’re going to get some really interesting things at the end of it just because people have had more time to absorb.

<span class="smashing-tv-host">Drew:</span> So it’s a Thursday and a Friday, a Thursday and a Friday, and then a Thursday to finish it off with two hours on each of those days followed by Q and A. I think that’s right, isn’t it?

<span class="smashing-tv-speaker">Cassie:</span> Yes.

<span class="smashing-tv-host">Drew:</span> Q and A on each session. What would those attending expect to learn? What should their expectations be in terms of what skills they might pick up?

<span class="smashing-tv-speaker">Cassie:</span> So it’s more angled towards the animation coding side of SVG animation. So we’ll cover a little bit of getting SVGs out of a graphics editor, and then the whole process from getting the code out through to starting to work with it. So optimizing and adding the right classes and structuring it properly, and then we’ll work on animating SVGs. So we’ll be using CSS. We’ll also be using GreenSock, which is the animation library that I mentioned, and we’ll be covering what I kind of refer to as SVG super powers. So this is stuff that it's, aside from the animation, it’s the things that you can do with SVG.

<span class="smashing-tv-speaker">Cassie:</span> So that’s like clipping, and masking, and stroke animation, and filters, and all of that stuff is just so important to understand with SVG because it unlocks all of these kinds of super powers that you can play with. And we’ll also look at performance and accessibility, and also a bunch of the kind of little tips that I’ve picked up and learned along the way. So, little handy tips that I find useful for my workflow, handy tips that help with flashes of unstyled content before you start animating. Little tips like that.

<span class="smashing-tv-host">Drew:</span> That sounds really useful. I looked just before we started our interview and there are still some early bird places available, which is great. So if people are quick they might still catch those and you can register at smashingconf.com. There’s actually a number of different master classes that are being run at the moment and there are early bird deals and bundled deals on some of them as well. So there’s things like JAMstack, CSS layout with Rachel Andrew, Vue.js, web performance, GraphQL, loads of different Masterclasses and you can find all those at smashingconf.com. So I’ve been learning all about SVG. What have you been learning about lately Cassie?

<span class="smashing-tv-speaker">Cassie:</span> Oh, I’ve been recently learning quite a lot about Eleventy. I did a little site redesign recently using Eleventy and I’ve also been doing Andy Bell’s Eleventy from scratch course. So I’m getting quite into static site generators in general at the moment.

<span class="smashing-tv-host">Drew:</span> That’s great. I think we’re all getting into static site generators more as time goes on.

<span class="smashing-tv-speaker">Cassie:</span> It’s the future.

<span class="smashing-tv-host">Drew:</span> If you dear listener, would like to hear more from Cassie you can of course sign up for this animation Masterclass with Smashing Conf, but also you can find her on Twitter where she’s @Cassiecodes and her personal website is cassie.codes and that links to her CodePen, which is a great place to explore. Thanks for joining us today Cassie. Do you have any parting words?

<span class="smashing-tv-speaker">Cassie:</span> I would like to say that Smashing and I are offering for free tickets to my workshop. So they are diversity tickets that are going out to anyone that’s underrepresented in tec or going through a tough financial time at the moment. So you can apply for that on the webpage about my workshop and I hope to see you there.


{{< signature "il" >}}
