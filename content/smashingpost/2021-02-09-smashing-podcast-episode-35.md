---
title: 'Smashing Podcast Episode 35 With Stephanie Stimac & Melanie Richards: What’s Next For HTML Controls?'
slug: smashing-podcast-episode-35
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2abd63c8-da4b-4ddb-8d7c-d9f0de8ed0db/smashing-podcast-episode-35.png
date: 2021-02-09T05:00:00.000Z
summary: >-
  In this episode, we’re talking about HTML controls. Why are they so hard to style, and how might that change in the future? Drew McLellan talks to Microsoft’s Stephanie Stimac and Melanie Richards to find out.
description: >-
  In this episode, we’re talking about HTML controls. Why are they so hard to style, and how might that change in the future? Drew McLellan talks to Microsoft’s Stephanie Stimac and Melanie Richards to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re talking about HTML controls. Why are they so hard to style, and how might that change in the future? Drew McLellan talks to Microsoft’s Stephanie Stimac and Melanie Richards to find out.

<iframe src="https://share.transistor.fm/e/3ced21a0/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- Stephanie’s [website](https://stephaniestimac.com) and [Twitter](https://twitter.com/seaotta)
- Melanie’s [website](https://melanie-richards.com) and [Twitter](https://twitter.com/soMelanieSaid)
- [Open UI](https://open-ui.org) project

### Weekly Update

- [Dynamic Static Typing In TypeScript](https://www.smashingmagazine.com/2021/01/dynamic-static-typing-typescript/) written by Stefan Baumgartner
- [Things You Can Do With CSS Today](https://www.smashingmagazine.com/2021/02/things-you-can-do-with-css-today/) written by Andy Bell
- [How To Port Your Web App To Microsoft Teams](https://www.smashingmagazine.com/2021/02/port-web-app-microsoft-teams/) written by Tomomi Imura & Daisy Chaussee
- [Designing Better Tooltips For Mobile User Interfaces](https://www.smashingmagazine.com/2021/02/designing-tooltips-mobile-user-interfaces/) written by Eric Olive
- [Improving Your Team’s Communication In The Age Of Remote Work](https://www.smashingmagazine.com/2021/02/improve-team-communication-age-remote-work/) written by Obed Parlapiano

## Transcript

<p><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3886e4f1-acc4-4385-8b21-39a82e15a42a/stephanie-melanie-300x300.jpg" width="200" height="200" alt="Photo of Stephanie Stimac and Melanie Richards" /><span class="smashing-tv-host">Drew McLellan:</span> My first guest is a program manager for Microsoft Edge developer experiences, but prefers to think of herself as a designer, front-end developer and developer advocate for Microsoft Edge. My second guest is also a program manager for Microsoft Edge focused on the web platform. She too has a background in web design and front end development. She loves designing and building fun things for the web and is currently doubling in 3D art.

<span class="smashing-tv-host">Drew:</span> So we know that they’re both experienced web developers working hard to move the web platform forward, but did you know together they won the Kentucky Derby dressed as a pantomime horse? My smashing friends, please welcome Stephanie Stimac and Melanie Richards. Hi Stephanie. Hi Melanie. How are you?

<span class="smashing-tv-speaker">Stephanie Stimac:</span> I am smashing.

<span class="smashing-tv-speaker">Melanie Richards:</span> I’m also simply smashing.

<span class="smashing-tv-host">Drew:</span> It’s been probably about a year Stephanie, since we last had you on the podcast, and you have the dubious honor of being our first ever return guest. At that point a year ago, Edge was transitioning over to a chromium rendering engine.

<span class="smashing-tv-host">Drew:</span> Melanie, I’m guessing that that transition was a big deal for your team on web platform as well. How have things been over the last year? Has the transition been smooth and successful?

<span class="smashing-tv-speaker">Stephanie:</span> I think so. So I think Gavin, we talked last, we were just rolling out our stable version across some platforms. And now we’re on Linux as well, and there’s been just so much good reception from the developer community, people are excited to use Edge, so the reception has been really great and I know for developer experiences. We’ve been working on some fun stuff that’s coming up still soon, but it’s been really good.

<span class="smashing-tv-host">Drew:</span> That’s amazing. I didn’t realize that Edge was also available on Linux now, because it’s been on the Mac for a while as well, which is great to be able to run a page on a Mac. I mean, windows obviously being the sort of dominant desktop operating system. The role is the primary browser on that platform is sort of fairly immense.

<span class="smashing-tv-host">Drew:</span> And there’s been a bit of a spotty history when it comes to Microsoft and it’s browsers, I think we can be honest about that. Sometimes leading the way and then maybe stumbling for a little bit and getting left behind. But we all know as developers the pain that comes from such an important browse not being up to par. So it’s great to see that now it’s a really first-class experience for users, but also for developers too with edge, with all sorts of development tools and at a really first-class experience in that regard as well.

<span class="smashing-tv-speaker">Melanie:</span> Yeah, it’s been wonderful for us on the team, because we’ve had kind of a true opportunity to help push the web forward a little bit more. When we were kind of building on top of edge HTML, there were some areas where we had to play catch up on certain APIs.

<span class="smashing-tv-speaker">Melanie:</span> And now that we’re collaborating and bringing new ideas into the chromium code base and to standards, it becomes a lot easier to say, okay, what’s next? How can we solve problems for developers and for our users? So, it’s kind of been a joy collaborating with folks across the different companies on this one.

<span class="smashing-tv-host">Drew:</span> It feels very natural that it should be a collaborative experience and that’s kind of what the web is designed to be, right?

<span class="smashing-tv-speaker">Melanie:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> So, I wanted to talk to you both today about HTML controls. And that term itself, I guess is wrapped up in quite a bit of sort of platform specification jargon. What do we mean in practical terms when we’re talking about HTML controls and what are the sort of problems that designers and developers might counter with them on an everyday project?

<span class="smashing-tv-speaker">Melanie:</span> Yeah, so primarily we’re thinking about form controls that enable user input in some fashion. So you have your Slack, your radio, checkbox, buttons, this extends also to the video player and controls as well.

<span class="smashing-tv-speaker">Melanie:</span> So I think something that a lot of us have experienced as far as participants in this customizable controls effort have experienced personally, is sort of wrestling with getting these controls to fit the brand and the user experience that we’re going after for our particular user base.

<span class="smashing-tv-speaker">Melanie:</span> So, there’s things that seem like they should be fairly trivial, just getting the right colors in select options. And the fact that you have to just completely recreate a control in order to do that, to align to your branding, which is something that a lot of projects require that is so challenging.

<span class="smashing-tv-speaker">Melanie:</span> I saw a tweet a couple months back when we were talking about this with some other browser vendors. Someone was saying, Oh, you want icons in your select options, you have one problem. So you recreate the select and now you have 37 problems.

<span class="smashing-tv-speaker">Melanie:</span> There’s so many things that you have to manage as a designer developer, getting the accessibility right, and there’s so many different dimensions of that, the semantics, the keyboard interactions, high contrast, supporting different color schemes, that sort of thing. And we find that folks are just recreating these all over the place, several different frameworks even within the same company, a lot of developer designer energy being put into this and it’s like, okay, what if we could just make it easier to use the things out of the box and build on top of those and not have to recreate the wheel here?

<span class="smashing-tv-host">Drew:</span> I think there was this sort of concept with early implementation of form controls, that they should look like they’re native to the operating system. Which you can kind of understand from a view of wanting consistency across the user experience for the whole of the operating system.

<span class="smashing-tv-host">Drew:</span> We’ve all used desktop apps, particularly cross-platform ones that implement their own controls rather than using the native ones and that experience can be really horrible. So you can see where that thinking has come from. But I think it’s sort of almost a false promise that there is a consistent experience, because the controls in a webpage never really behaved in the same way as the controls in native applications and operating system, they never really functioned like native controls. So it was sort of a coat of paint, but not really providing the same user experience. Was it?

<span class="smashing-tv-speaker">Stephanie:</span> Right. So yeah, I’ve dived into the history of controls a little bit, and I think in the beginning they did behave like native platform controls, because in the early days of the web, it was the underlying operating system that was sort of rendering those controls.

<span class="smashing-tv-speaker">Stephanie:</span> And then this idea that developers wanted more control over functionality and style. I was reading a blog post from I think, 2001, and so like CSS had finally just been standardized and was sort of embraced as the main styling language and people were trying to style controls and just have more control over controls.

<span class="smashing-tv-speaker">Stephanie:</span> And that led to, I think, and even today that’s led to a huge sort of, I think, discrepancy in the way that they function. Like Melanie said that you have people recreating form controls from scratch, and they may not mimic native form controls at all their functionality. So you’ll have a select that maybe behaves differently on one website than another one.

<span class="smashing-tv-speaker">Stephanie:</span> So the experience can be pretty jarring. And I think even across different platforms too, we have native controls that don’t behave the same way, they behave differently on different platforms. So it does create sort of this interesting problem space for developers when you’re thinking about user experience.

<span class="smashing-tv-host">Drew:</span> When you think about all the things that run on the web platform, sort of banking and healthcare services and emergency response, governments, e-commerce, global economies basically are running on top of the web platform these days, through various ways of means. And that’s all built on top of a few HTML controls from 25 years ago, pretty much, they’ve been the same for decades. And they’re pretty terrible really, aren’t they? They’re basic.

<span class="smashing-tv-host">Drew:</span> But how did we get to this point where they got so left behind, and nobody sort of touched them for so long? How have we got to the point on the web platform where sort of the weakest link is input controls?

<span class="smashing-tv-speaker">Melanie:</span> Yeah, I think that’s a pretty big challenge, something that we think about quite a lot as browser vendors and as participants in standards is web compatibility. This comes up all the time, you’re thinking about, Oh, should we make this change to CSS or should we tweak this a little bit?

<span class="smashing-tv-speaker">Melanie:</span> And maybe it makes a lot of logical sense for the way people are building today. It makes a lot of logical sense for developer ergonomics, but someone goes, Hey, wait a second, if we make that change, these millions of sites are going to blow up in unexpected ways. There’s just an example on some of these controls where people are applying CSS styles that have no effect today.

<span class="smashing-tv-speaker">Melanie:</span> So if we said, okay, actually we’re going to allow this or that property on a certain control, now, some of these sites are going to do very funky things. So I think because controls are involved in such mission critical flows as you kind of pointed out, people are a little bit nervous about changing something so fundamental to the web in a way that is backwards compatible and won’t break anything.

<span class="smashing-tv-speaker">Melanie:</span> So we kind of have to think about the controls problem in an additive way. And some of the other challenges here are that every browser has kind of implemented their controls under the hood in a different fashion. So some are kind of doing something that’s a little bit orthogonal to the operating system, some are still leaning quite heavily on the operating system, and that can change for the same browser in different platforms. So you have to kind of take all those things into account.

<span class="smashing-tv-speaker">Melanie:</span> I think it’s a tough problem, but I am feeling the winds of change here, everybody recognizes, okay, we need to go and solve this problem, it’s going to take a long time, It’s going to be hard, but let’s try.

<span class="smashing-tv-speaker">Stephanie:</span> To add on top of that too, so I’ve been sitting in on our meetings with Melanie and the open UI initiative that’s sort of leading the standardization of controls. And I don’t think people realize either, like Melanie said, it’s a huge undertaking. And there are some meetings we have that get into such granular detail about the way a select behaves, just to a level that even kind of blows my mind at how specific these problems are that we have to think about. So it is a huge undertaking.

<span class="smashing-tv-host">Drew:</span> There was an effort, wasn’t there? With HTML5 to improve things a little bit, and there were some new types for the input element and there was some basic validation capability and the constraint validation API, but it was kind of a subtle evolution, not a revolution, was it successful, do you think?

<span class="smashing-tv-speaker">Melanie:</span> I think that effort did add some necessary capabilities to the web platform, but I think there’s some feeling about the type attribute, maybe we should go a different way in the future, but that type of attribute does a lot. You kind of inherit a lot of behaviors from the base input class that maybe isn’t applicable to that particular element. Maybe there’s a different way to do this and have more purpose-built specific elements so that’s kind of what we’re looking at.

<span class="smashing-tv-host">Drew:</span> I think of things like the way that data input works currently with HTML5 or I say works, doesn’t work maybe. You have to sort of just look at the fact that every single site is building custom calendar controls rather than using that native date picker, because the date picker isn’t serving that need. And you kind of have to conclude that some of these native methods have just completely failed.

<span class="smashing-tv-speaker">Melanie:</span> Right. And the date picker is such an interesting one, because I feel there’s two buckets as to why people recreate those. In some cases it’s like, yeah, I want it to basically function as a date picker does, but I really need it to be style to match my own branding. And that day picker control is doing a lot of work, there’s a lot of stuff going on in this one tiny little pop-up world.

<span class="smashing-tv-speaker">Melanie:</span> And then on the other side of the house, you have airline websites, right? Where they’re trying to do something that’s different, that can’t be supported by that date picker control where you’re really looking at range, I can cross different months and that sort of thing. So yeah, that one’s a tricky one, there’s a lot of different use cases packed into one control.

<span class="smashing-tv-host">Drew:</span> How can we avoid new sort of falling into that trap again in the future? obviously that’s an example of something that was too complex, obviously very complex to implement, because some rendering engines didn’t even try and others that did try had varying levels of success. How do we avoid falling into that trap in the future? Can we?

<span class="smashing-tv-speaker">Melanie:</span> Yeah. It’s an interesting question, so I think some of the proposals that we’ve made around customizable controls are meant to offer folks a little bit more flexibility with the inbuilt controls, more control over those, if you will.

<span class="smashing-tv-speaker">Melanie:</span> So just kind of break down our basic proposal here, we imagine there’s a couple different solutions for customizable controls, and the right solution sort of depends on the use case and the particular control and how complex it is really. So the different kind of buckets are, we want to have some sort of standardized internal structure to the controls, so named parts basically. And we can create pseudo elements that can target the specific parts.

<span class="smashing-tv-speaker">Melanie:</span> So Greg Whitworth over at Salesforce actually has a proposal that he’s pulling over around a pseudo element for the checkbox and radio indicators, so looking forward to that kind of coming online in that bucket. Then we also looking at name slots, so let’s say that you’re a web developer, the base control mostly works for you, but you just want to replace one little piece of the control.

<span class="smashing-tv-speaker">Melanie:</span> So maybe the button you part of a select, for example. You can just swap out that name to slot. And then if you really want to go truly custom, you can actually completely replace the shadow domino control with the attached added method.

<span class="smashing-tv-speaker">Melanie:</span> And so the idea here is that the developer would have control over the view of the control, and they would still rely on the controller code coming from the web platform to kind of hook up things between the model, so certain data points in the control and the view, so they wouldn’t have to kind of do that underlying logic themselves.

<span class="smashing-tv-speaker">Melanie:</span> So, those are the kind of strategies that we have as far as being able to leverage what’s already been done but really customize it to your use case.

<span class="smashing-tv-host">Drew:</span> So that’s sort of getting around this problem that a lot of controls are just kind of a black box on there that’s inserted into the page and you can’t do anything much with it. Replaced elements, is that the right terminology?

<span class="smashing-tv-speaker">Melanie:</span> Yes.

<span class="smashing-tv-host">Drew:</span> Yes. So, there’s no way then with CSS or with JavaScript to actually target bits inside it, it’s just a box and you can’t get into it. So the idea here that you’re describing is structuring controls so they’re much more like something that we might build ourselves, with different levels of containers and items in it, so that each of those individual bits can be targeted.

<span class="smashing-tv-host">Drew:</span> And then some of them might be named, and so you could keep the basic control but swap out the slots. So if you had a file upload control, you might be able to swap the button with a button of your own choosing, but keep the general functionality implemented by the web platform, am I understanding that right?

<span class="smashing-tv-speaker">Melanie:</span> Yeah, that’s absolutely correct, yeah. We want to make it easier to kind of reach directly into that control and kind of take the pieces you need and update the pieces that you need as well.

<span class="smashing-tv-host">Drew:</span> Yeah, that sounds really exciting. But to play devil’s advocate as is my job sometimes, do we really need HTML controls at all? And I think at the number of forms that are being submitted with JavaScript using the fetch API, you can gather some data and make a post request or what have you. And you can take any element and turn on content editable and have the user be able to type in some text or what have you. Do we need native form controls or should we just go rogue and build it all ourselves?

<span class="smashing-tv-speaker">Melanie:</span> Pardon me, that carries a whole lot about accessibility is like "ahhh!", Hopefully that screech doesn’t sound too awful on the mic here, but. I think I’m a huge fan of the semantic web, right? And having things that are truly built for their purpose. Again, there’s a lot of things that you have to get right so that people who are using assistive technologies, for example, really know what they’re interacting with and their assistant technologies know how to inputs their actions and their data into that control as well.

<span class="smashing-tv-speaker">Melanie:</span> And so, clarity over the items that you’re working with really decreases if you kind of just throw a content editable on everything. And then, I feel like JavaScript is eating the world and here’s where I start getting nervous about going into controversial territory and just say the word JavaScript and people are like, what? Pop out of the woodwork.

<span class="smashing-tv-speaker">Melanie:</span> But people can just say, well JavaScript in their browsers or content can be kind of ingested into other environments. And so I still feel it’s super important to work with HTML, work declaratively, don’t necessarily depend on JavaScript for everything, provide a progressively enhanced experience, so.

<span class="smashing-tv-host">Drew:</span> I think when you look at the difference between how different controls are rendered on a desktop web page, versus the experience in a mobile browser, think of something like a select control, the interface is completely different on a mobile device, isn’t it? It’s not just whatever the developers built with divs and CSS on the page, the browser just completely takes that over and gives you a different experience.

<span class="smashing-tv-host">Drew:</span> That’s more appropriate to the device in question. So I think that’s definitely sort of a glimpse into the predicament that those who are using assistive technologies face when they come up against using things that are completely custom and not based on real solid HTML elements.

<span class="smashing-tv-speaker">Melanie:</span> Right. And it’s tricky if you are a person who’s interacting with the same basic control from site to site, but you have to like relearn how to use that control, because this website decided to use arrow keys to traverse through these items. And this site decided to use tab keys or the tab key. And it’s like, come on, that’s such heavy cognitive overload for folks who are just trying to go about their day.

<span class="smashing-tv-host">Drew:</span> Definitely, there’s awful a lot to think about when you go rogue, isn’t there? In terms of accessibility, keyboard use, focus, all these sorts of things that really add an awful lot of code to something that could be quite simple and you could just put the right elements in and get on with your day.

<span class="smashing-tv-host">Drew:</span> It’s a real frustration for us developers to try and style the form elements to make them work in the way we want to. And I get the feeling that just about every designer and developer would want to have better native controls. Is that something that you’ve seen in your own research into the developer community Stephanie?

<span class="smashing-tv-speaker">Stephanie:</span> So, yeah, we’ve actually seen that in the developer community. So about a year and a half ago, Greg Whitworth, who is at Salesforce and leading the open UI initiative, ran a survey on Twitter with about 1400 respondents to sort of find out if this controls pain point was... Or I’m sorry, I guess it’s two and a half years ago now 2020 was a blur.

<span class="smashing-tv-speaker">Melanie:</span> By this time.

<span class="smashing-tv-speaker">Stephanie:</span> Yeah. And he was trying to dive deep to see if this controls area was something that web platform team should go invest in. And the biggest reason for developers making their own controls or rebuilding them from scratch was, because they couldn’t change the appearance sufficiently, I think that was about like a third of developers. And then, I think about another third said, because of browser inconsistencies and I think you can assume that that probably has to do with the parents also. So that’s a lot of developer hours being spent rebuilding these things just to change the appearance.

<span class="smashing-tv-speaker">Stephanie:</span> And so Greg sort of identified that, yes, this was a pain point and being the PM that I am, I sort of wanted to find out how big of a pain point it was for developers. So I did my own sort of impromptu gorilla research on Twitter and asked people, how painful is this for you? And I got about 250 responses to this tweet.

<span class="smashing-tv-speaker">Stephanie:</span> And I had asked, what would you rather do than style a select menu? And responses ranged from I would rather chew on glass or boil my toes in lava than attempt to style a native select element to... I’d rather have to build the site and have it be compatible with IE6. So this is a huge, huge pain point for developers. So it’s been a pretty consistent theme that developers aren’t happy with what is there. So.

<span class="smashing-tv-host">Drew:</span> There’s been a bit of an effort from the various browsers to have a little bit of a design refresh lately of some of the form controls and try and take some of the opinion out of the design. We have lots of sort of gradients and things going on, didn’t we, in all sorts, which I guess is a primary reason for people wanting to style them in the first place. To try and get a bit of a more neutral look that doesn’t clash at least with their site’s design. Was that something that edge was involved in? I know that it happened in Chrome, was it driven by chromium or was that just Chrome doing it, or how has that worked?

<span class="smashing-tv-speaker">Melanie:</span> I think that’s actually a prime example of some of the cross-company collaboration we’ve been able to do since moving to chromium. So actually on the Microsoft edge side, all of us PMs on the platform are taking just the review of, okay, here’s all the features that we have in our current edge HTML based browser. What’s kind of the situation over in chromium land?

<span class="smashing-tv-speaker">Melanie:</span> At the time I was working on accessibility, so this looks like collaborating with chromium on bringing support for UI automation that accessibility API over to chromium, force colors, windows high contrast support, support for other system settings, but over in controls land, the team was kind of looking at, what our controls look like today, what are our requirements? What is the situation in chromium?

<span class="smashing-tv-speaker">Melanie:</span> So for the Microsoft edge browser, we run in a lot of contexts where there are touch capabilities, so there’s a lot of PCs that have touch screens, for example. And so, touch capability is really important to our form controls, they have to work well for a larger pointer, which is your finger.

<span class="smashing-tv-speaker">Melanie:</span> And we have this kind of fluent design system, so we were just feeling that there were ways to kind of push the controls a little bit more to align to our aesthetic, our touch requirements, our accessibility requirements, that sort of thing. And it actually ended up working out perfectly because we talked to the folks over at Google and they’re like, yeah, we’d love to kind of update, refresh the controls and make them feel more modern.

<span class="smashing-tv-speaker">Melanie:</span> So it was really tight collaboration between the companies to land on something that works for our aesthetic, their aesthetic, the aesthetic of other browsers that are also building on top of chromium. Find something that’s a good middle ground there and then it’s extensible. So yeah, lots of collaboration, it’s still ongoing actually, we’re actually just doing work on the controls refresh for Android, for example, so, lots of cool stuff to do.

<span class="smashing-tv-host">Drew:</span> So, sort of looking at further ahead than a design refresh. Are there plans for any sort of new native components coming up?

<span class="smashing-tv-speaker">Melanie:</span> Oh, yeah. Funny that you should ask, because we actually just published an explainer just the other day, for a new pop-up element that I’m very excited about. So I had kind of mentioned that we had proposed a couple of different capabilities for customizable controls. We sent an intent to prototype in the chromium project with a customizable select, ITPs as they call them are just kind of like, Hey, I’m going to play around the code base, kind of like push on my ideas, see if they’re like truly feasible in implementation. And that kind of happens in parallel to some of the standardization efforts.

<span class="smashing-tv-speaker">Melanie:</span> So we filed an ITP for the customizable select, but part of what we needed, we’re talking about reaching into the shadow dome, reaching into the control, we needed something that worked really well for the list box pop up portion of the select control. And we also kind of talk to some of our partners in different design frameworks and found that there was a more generalized need for a pop-up that can be rendered on the top layer, consistently it can break out of any kind of bounding boxes.

<span class="smashing-tv-speaker">Melanie:</span> We find that a lot of the times developers are kind of just like stuffing, they’re like divvy pop-ups in the bottom of the body, because they’re trying to get around these rendering problems, especially because they can’t actually directly control all the context in which their components show up, because there’s component library. So, we kind of took a look at some of these problems and came up with the pop-up proposal.

<span class="smashing-tv-speaker">Melanie:</span> And so this is for any kind of top layer UI that pops up and has light dismiss behaviors. So, the item should close on escape or loss of focus, things like that. And it’s really designed for transient UI, right? So you can only have one pop-up available at a time, unless there’s an ancestry chain, you can have popups inside popups and there’s different use cases for that.

<span class="smashing-tv-speaker">Melanie:</span> So yeah, this is a really early proposal, we’re really excited about it. But we’d love feedback from the community, we have it posted on the Microsoft edge explainers repo. We’re getting so many great questions, which is really exciting to me to just see people engaged with the idea and really pushing on the details and looking at us browser vendors to get things right. So, super excited about that, please check it out and let us know what you think.

<span class="smashing-tv-host">Drew:</span> And the stage that’s at, I’ve seen the explainer, which is a document which describes it all. Is that the state of that, there’s no sort of experiments and codes to play around with. It’s more a conceptual, what if we did this sort of stage, is that right?

<span class="smashing-tv-speaker">Melanie:</span> It is conceptual, but we do also have an intention prototype filed on that one as well. And so that is something that a couple of our close collaborators and Google are helping us with, kind of tinkering with the code right now, so that’s kind of exciting just validating our ideas as we make a proposal to the broader community.

<span class="smashing-tv-host">Drew:</span> That’s really exciting, I’ve literally just been working on a project at work that is a really key pop-up in our product interface. And the amount of work that’s involved in making sure that it sort of traps focus correctly and as you were saying, do we then allow somebody to interact with a tab or with arrow keys, or all the tiny details of interaction that are involved in that, making sure it appears at the writers that index above all the things that it should be in front of, what happens if somebody scrolls and then they hit the bottom of the scroll?

<span class="smashing-tv-host">Drew:</span> All these sorts of tiny, tiny, subtle bits of interaction that are... they’re not individually, they’re not difficult to code for, but the sum of them is a lot of work and the potential for bugs to creep in there and improve complete usability problem for some segments of your audience. To have that such a common thing implemented potentially as part of the web platform, it’s going to be a massive time saver for everyone, isn’t it?

<span class="smashing-tv-speaker">Melanie:</span> I’m so glad to hear that, that would be a great time saver for you, because yeah, that’s exactly what I’m kind of thinking, it’s like, oh, okay, it’s 20 minutes here, 30 minutes there, but multiply that by every single developer who has to do that, and then maybe you miss something and you get a very upset ticket in your feedback channel. So.

<span class="smashing-tv-host">Drew:</span> So is the idea that then something like a popup would be a building block for then a customized select control where it would be the options sort of section?

<span class="smashing-tv-speaker">Melanie:</span> Yes, absolutely. That’s one of the cases where we kind of imagine this showing up and it’s worth mentioning that the pop-up control that we’re kind of putting forward is meant to be a base that you can build on top of, because there’s many different types of pop-up UI and your use case might differ a little bit from your neighbor next to you.

<span class="smashing-tv-speaker">Melanie:</span> But it’s worth mentioning we think that there are some classes of top layer UI that actually could warrant their own additional element to pop up, because the paradigms there are a little bit different from the popup that we’re proposing. And it’s a very well-trodden path, a lot of people are rebuilding this control.

<span class="smashing-tv-speaker">Melanie:</span> But we’re trying to find the right balance here between pushing the platform forward and not wanting to flood it with new elements either.

<span class="smashing-tv-host">Drew:</span> Yeah. I mean, that’s an important point, isn’t it? Because we sort of want to be confident that the things that are being added to the platform are an evergreen requirement and not just a current interaction fad. I mean, if you sort of think back to five years ago where every website had an enormous carousel on it, we could have at that point decided, oh right, the web platform needs an enormous carousel control built into it.

<span class="smashing-tv-host">Drew:</span> Could have built that, and then once something’s in the platform, it stays forever, right? Basically we don’t take things out, they’ve got to keep working forever. And if people then aren’t using them, then it just becomes technical debt. So is there a way we can safeguard against that to make sure that these things are evergreen and not just a fad?

<span class="smashing-tv-speaker">Melanie:</span> There’s a lot of different stakeholders in web standards and I think a lot of these things happen naturally, there do tend to be pretty strong headwinds against adding a new element, because there is this fear of making the wrong choices and having the big forever or capturing something that’s a fleeting sort of problem.

<span class="smashing-tv-speaker">Melanie:</span> So I think what’s key here is to look at the problems that have been around for the longest time, right? And just listen to the various different stakeholders and what they have to say about the proposal that you’ve made and make sure that we have the best insights from everybody in the industry, all working together towards the best solution.

<span class="smashing-tv-speaker">Stephanie:</span> So, thinking of new elements and sort of what would be put into the platform. So Chrome, I believe is working on a toggle switch element. I believe there’s a prototype up for that, but that’s an element that they have in the works, which is one of those elements that sort of makes sense, that is something that’s sort of fundamental that gets used across so many websites that just, again, that makes sense that there should be a native element for that.

<span class="smashing-tv-host">Drew:</span> That’s exciting to hear as well, because the work in sort of progressively enhancing a checkbox, for example, to become a toggle switch is... Yeah, yeah, it’s something that’s best avoided if you can. But a toggle switch as an interface device makes a lot of sense for a lot of cases of turning something on or off and being a yes, no choice. So having that sort of thing as a fundamental part of the web platform would be terrific.

<span class="smashing-tv-host">Drew:</span> When we think about all the existing controls that are out there that potentially have problems, can they be fixed? I mean, we can’t throw them away. Well, I guess we could come up with alternatives that new sites could start to use in their place, but can we rescue the current ones? Is there a way that we can keep backwards compatibility and still move them forward?

<span class="smashing-tv-speaker">Melanie:</span> Yeah. So I think that’s an interesting question that it encompasses a broad range, right? I depends on what the issue is, I think, look, browser vendors are not perfect either, we have bugs, we should fix the bugs. So there’s plenty of those items. But again there are some things that are very difficult for compat and just keeping the web working if we just change things underneath people.

<span class="smashing-tv-speaker">Melanie:</span> So for example when we were working through the controls refreshing chromium, some of the designers were like, Oh, what if we make these check boxes in these radius this size? And we’re like, yeah, that’s better for usability, but the problem is they’ve been a certain size on the web forever for everyone and bad things will happen if we change that.

<span class="smashing-tv-speaker">Melanie:</span> So, it’s frustrating a little bit sometimes, because you can imagine a better way of doing something, but you don’t want to break everyone. So I think it depends. That’s probably the eventual answer to every question in web development, isn’t it?

<span class="smashing-tv-host">Drew:</span> It depends. I think about things like the select element over the multiple attributes, so you can have not select multiple items in the list. I mean, putting to one side how it looks by default in most browsers, the interaction model for that control is from a different era of computing, isn’t it? So much so that it’s rarely used because a typical web user doesn’t know how to interact with it. Can we address things like that? Is that something that can be fixed?

<span class="smashing-tv-speaker">Melanie:</span> That’s a hard question. I believe there’s a lot of creative people in this space come up with some really interesting ideas. I have to think a little bit about that one, because I agree even as a user that I find that interaction pattern a little bit challenging. So yeah, back to the drawing board I guess.

<span class="smashing-tv-host">Drew:</span> So, it depends.

<span class="smashing-tv-speaker">Melanie:</span> Oh man. I’m just going to answer every question that you have from now on with that.

<span class="smashing-tv-host">Drew:</span> So, Stephanie mentioned open UI a little bit earlier. What is open UI?

<span class="smashing-tv-speaker">Stephanie:</span> So open UI is an initiative under the YCG, and it is focused on standardizing controls. And so I think not... So controls are standardized, but it’s only their function. So I think that’s where the root of a lot of this problem comes from is back 25 years ago when the initial controls were introduced into the first HTML 2.0 Specification. Their parts weren’t standardized, it was just this form is supposed to complete this function or serve this purpose and that’s sort of what was standardized.

<span class="smashing-tv-speaker">Stephanie:</span> And so that is sort of the problem, different browser engines choose to render their controls or build them differently under the hood. And so we can’t give developers access to the different parts, sort of in a compatible way at the moment. And so open UI at its core is sort of driving that initiative to define, so first select, what is a select comprised of? What are the different parts? And drive that work forward.

<span class="smashing-tv-speaker">Stephanie:</span> And so Greg Whitworth is again driving a lot of that work, but it’s an open initiative, so we’ve had quite a few people from the developer community join in on that and are sort of helping to drive that work with Greg and the rest of the team. And so, yeah, at it’s core it’s just trying to find the different parts of the controls and sort of pave the way to get those into an actual standard specification and eventually into browsers.

<span class="smashing-tv-host">Drew:</span> So, this was the internal structure that Melanie was talking about just before of being able to identify different slots and then putting names to the different parts that make up a control so they can be targeted and replaced or styled or whatever, but it’s just making sure that that is consistent across different browsers, standardizing it, working out where they are or should be, and then hopefully that gets implemented and we can start using controls with a lot more precision than we can currently.

<span class="smashing-tv-speaker">Stephanie:</span> Yeah, that’s exactly right.

<span class="smashing-tv-host">Drew:</span> And does open UI attempt to address how controls will look?

<span class="smashing-tv-speaker">Melanie:</span> No, that’s outside of the purview of the open UI efforts. So, we’re looking at, if we have an MVC model of controls looking at the M and the C I suppose you can say.

<span class="smashing-tv-speaker">Stephanie:</span> Just to add to that too, sort of standardizing the way they look, like Melanie said, yeah, that’s not really... When you have different companies like Microsoft or the different browsers, Firefox and Chrome and Microsoft, they are different companies with different design languages as well. So even our default styles I think are going to be reflective of the company or the browser. So.

<span class="smashing-tv-host">Drew:</span> I think that’s ideal from sort of a development point of view, because if the browser vendors have to implement this new spec, it’s been agreed on, they’re going to implement it. And the first thing they going want do is to use that to style the control themselves to match the language of the browser.

<span class="smashing-tv-host">Drew:</span> And any inflexibility or potential problems that might appear down the road for end users are going to appear for the browser developers as they’re implementing that themselves. So it’s a good initial stress test. Can this select box be made to look like it should in edge, made like it should in Chrome and so on.

<span class="smashing-tv-speaker">Melanie:</span> Yeah, I also feel like I’m trying to get all the different browser engines to agree on a style or even just standards group on what this thing should look like would be a... I think that conversation would go on forever, quite frankly.

<span class="smashing-tv-host">Drew:</span> And could potentially stifle innovation as well. I think it’s positive that different competing products can compete on the user experience level by bringing their own innovation and hopefully what the specifications will enable us to do is to do that in a way that isn’t going to impact an end user... end web developer who wants to then restyle those controls themselves. It gives everybody the flexibility that they need.

<span class="smashing-tv-speaker">Melanie:</span> Right. Yeah. It’s even just a challenge, even as we’re talking about standardizing the internals of a control, you have to do it in such a way that it could be implemented in a different fashion, or there’s a little bit of room for variety or as you said innovation. So, that is a challenging requirement of this work stream.

<span class="smashing-tv-host">Drew:</span> What’s the process of sort of between getting these early ideas? Things that the open UI project might write up. How do we get those to start to become part of a future web specification and then ultimately implemented in browsers. Are we looking at decades of work here? Or, I mean, it’s not going to be a month, is it?

<span class="smashing-tv-speaker">Melanie:</span> I wish. Just kidding, actually, it’s so funny, I was thinking about this the other day, it’s like, as a web developer, your timescale is so much shorter than web standards, it’s like, I would love to have this for this thing that I’m trying to push out next month or whatever, but you actually probably should want us to take a while, because that means that will be very considered in the decisions that the web standards industry makes.

<span class="smashing-tv-speaker">Melanie:</span> So, yeah, I think this is going to be... We’re looking at a couple of years at least to fully go through all the controls. As far as process goes, that’s sort of a little bit of a moving target, the folks who are involved in open UI, some of the chairs and a couple other folks are actually working on a process document for how this sort of works.

<span class="smashing-tv-speaker">Melanie:</span> But I think generally speaking, you can think as open UI as sort of the connective tissue that tells the full story between efforts that might land and what we do, so the living document for HTML or the CSS working group over at the W3C. The open UI group can tell the full story in between these desperate pieces. And then can also provide a maturation ground. So when you’re trying to get work into the HTML spec, that group goes off of PRs, rather than sitting in a room and chatting about it.

<span class="smashing-tv-speaker">Melanie:</span> And so the expectation is the PR should be fairly mature when you make it against that spec. So, perhaps open UI can be the place where you gain that maturity in the idea.

<span class="smashing-tv-host">Drew:</span> And the ideas can be thrashed out before they’re then taken onto the next level of being proposed to the actual specification.

<span class="smashing-tv-speaker">Melanie:</span> Yeah, absolutely.

<span class="smashing-tv-host">Drew:</span> So how can people get involved in this process to offer feedback? I mean, for example, I know personally I’ve done a lot of content management system development work and that they tend to be very form heavy. And so my individual perspective might be different from somebody who builds online games, and the web has to work for all those use cases. So I guess it’s really important to get lots of points of view into the process. How would people get involved with that?

<span class="smashing-tv-speaker">Stephanie:</span> There’s a couple of different ways that you can go, or you can either get involved in open UI, again, that group is... If you go to open-ui.org I believe, you can find out how to get involved in that and sort of actually be involved in the process of defining control structures and helping us do research, or you could provide feedback on the explainers, so there’s the customizing controls, CY explainer on GitHub under the Microsoft edge explainers repo.

<span class="smashing-tv-speaker">Stephanie:</span> And then also the pop-up explainer that Melanie mentioned. You can open issues or you can just tweet at me or Melanie and there’s some good... I’ve seen some good conversations with the pop-up explainer I think, Melanie’s Twitter feed, so.

<span class="smashing-tv-host">Drew:</span> So getting involved in the web platform could be as simple as sending a tweet?

<span class="smashing-tv-speaker">Stephanie:</span> Yes.

<span class="smashing-tv-host">Drew:</span> Amazing.

<span class="smashing-tv-speaker">Melanie:</span> We’re all human beings over here so.

<span class="smashing-tv-host">Drew:</span> What a time to be alive. So I’ve been learning about the future of HTML controls today. What have you both been learning about lately?

<span class="smashing-tv-speaker">Stephanie:</span> Well, so I’m writing a new talk for dual screen devices and talking about design considerations and I tend to go into the history of, like I’ve done with HTML controls. I like to dive into history and see where we’ve come from and so I’ve been looking at foldable devices and how... There were prototypes in 2008 of actual foldable devices, and so I’ve been diving into that and learning about that for my next talk.

<span class="smashing-tv-speaker">Melanie:</span> I feel like I have too many plates spinning at all times to start learning new things, but in addition to this controls work I’m also focused on the pricey space in the web platform, so very different space actually, which is very interesting. But learning a lot right now about identity and federated off use cases as that relates to privacy.

<span class="smashing-tv-speaker">Melanie:</span> So that’s been super interesting, collaborating with folks who have a lot of depth of expertise there. And outside of the web platform, I don’t know, always doing different stuff. You mentioned doing three arts, I’m taking, Devon Ko’s 3D for Designers course that’s been fun. Learning a little bit of Japanese. So working through my Kanji lessons. So doing fiber arts and then I was like, what if I learn Python? I’m like, no, no, no. I can’t add more things to this list.

<span class="smashing-tv-host">Drew:</span> Rein it in. That’s amazing. If you dear listener would like to hear more from our guests, you can find Stephanie on Twitter where she’s @seaotta with an A and her personal site is stephaniestimac.com.

<span class="smashing-tv-host">Drew:</span> Melanie can be found on Twitter where she’s @soMelanieSaid, and her website is Melanie-richards.com. And the open UI course is open-ui.org. Thank you both for joining me today. Do you have any parting words?

<span class="smashing-tv-speaker">Stephanie:</span> I have to say I’m excited about the controls work that Melanie is leading, and there’s just some good stuff coming in. So I hope developers get involved and are as excited as we are.

<span class="smashing-tv-speaker">Melanie:</span> Major plus one to that. Thanks so much for having us on today.

{{< signature "il" >}}
