---
title: 'Smashing Podcast Episode 8 With Stephanie Stimac And Aaron Gustafson: What’s New In Microsoft Edge?'
slug: smashing-podcast-episode-8
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd50d204-cb8c-4e20-b5d9-41ae8fb59ac9/smashing-podcaststephanie-stimac-aaron-gustafson.png
date: 2020-01-28T05:00:00.000Z
summary: >-
  We’re taking a look at the brand new version of Microsoft Edge and its Chromium-based rendering engine. What does that change mean for web developers, and how does the death of Microsoft’s own rendering engine impact the web? Drew McLellan talks to Microsoft’s Aaron Gustafson and Stephanie Stimac to find out.
description: >-
  We’re taking a look at the brand new version of Microsoft Edge and its Chromium-based rendering engine. What does that change mean for web developers, and how does the death of Microsoft’s own rendering engine impact the web? Drew McLellan talks to Microsoft’s Aaron Gustafson and Stephanie Stimac to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode of the Smashing Podcast, I’m talking to Microsoft’s Aaron Gustafson and Stephanie Stimac to find out more about the brand new version of Microsoft Edge and how it’s affecting web developers worldwide as well as its impact on the web.

<iframe src="https://share.transistor.fm/e/72a4177b/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- *The Web We Want* [website](https://webwewant.fyi) and [Twitter](https://twitter.com/webwewantfyi)
- [Stephanie](https://twitter.com/seaotta) and [Aaron](https://twitter.com/aarongustafson) on Twitter

### Weekly Update

- “[The Mythical Mythical Man-Month](https://www.smashingmagazine.com/2020/01/mythical-man-month/),”  
*by John Foreman*
- “[Recreating The Arduino Pushbutton Using SVG And &lt;lit-element&gt;](https://www.smashingmagazine.com/2020/01/recreating-arduino-pushbutton-svg/),”  
*by Uri Shaked*
- “[How To Pass Data Between Components In Vue.js](https://www.smashingmagazine.com/2020/01/data-components-vue-js/),”  
*by Matt Maribojoc*
- “[A Complete Guide To WordPress Multisite](https://www.smashingmagazine.com/2020/01/complete-guide-wordpress-multisite/),”  
*by Manish Dudharejia*
- “[How To Empower Design Teams By Measuring Value](https://www.smashingmagazine.com/2020/01/empower-design-teams-by-measuring-value/),”  
*by Dave Cunningham*

## Transcript

<div>
<p><img style="float:right;margin-top:1em;margin-left:1.5em;margin-bottom:1em;border-radius:11px;max-width:50%" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d710d8-5cc8-4c6a-a1ed-f74a1820543e/smashing-podcaststephanie-stimac-aaron-gustafson.jpg" width="400" alt="A photo of Aaron Gustafson on the left, and Stephanie Stimac on the right" /><span class="smashing-tv-host">Drew McLellan:</span> She’s a program manager and user researcher with the Microsoft Edge Developer Experiences Team where amongst other things she connects with web developers to identify problems in the web platform that they need solutions for to improve their day to day workflows... He’s a web standards advocate, again with Microsoft, where he works closely with the Edge Browser Team as well as working with partners on progressive web apps and takes a focus on cross platform compatibility... Together, they’re part of <em>The Web We Want</em> Team, which is a cross-browser vendor project to open a dialogue with web developers to help shape the future development of the web platform.</p>
</div>

<span class="smashing-tv-host">Drew:</span> So we know they’re both from Microsoft, they’re both dedicated to making the web better for all of us, but did you know their most recent <em>Web We Want</em> meet up was hosted in a hot air balloon outside the Earth’s atmosphere before jumping back down to earth in the style of Felix Baumgartner.

<span class="smashing-tv-host">Drew:</span> My Smashing Friends, please welcome Stephanie Stimac and Aaron Gustafson.

<span class="smashing-tv-host">Drew:</span> Hello Stephanie, hello Aaron, how are you?

<span class="smashing-tv-speaker">Aaron Gustafson:</span> I’m smashing.

<span class="smashing-tv-speaker">Stephanie Stimac:</span> I am also smashing.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you today about some very interesting developments that have been going on with the Microsoft Edge browser. I guess most of us will know that Edge is traditionally the Windows 10 browser that replaced the much beloved Internet Explorer. Probably the first thing that we should note is the Edge isn’t exclusive to Windows 10 anymore, is it?

<span class="smashing-tv-speaker">Aaron:</span> Correct.

<span class="smashing-tv-speaker">Stephanie:</span> You can find Edge on Windows 10 and Mac OS. And then I’m not sure if it’s available on Windows Seven yet.

<span class="smashing-tv-speaker">Aaron:</span> Yeah, I believe it’s available on Windows Seven and Windows Eight now as well. And then of course there’s the mobile clients too for iOS and for Android.

<span class="smashing-tv-host">Drew:</span> So pretty much every modern platform.

<span class="smashing-tv-speaker">Stephanie:</span> Yep.

<span class="smashing-tv-speaker">Aaron:</span> Except for Linux, hopefully coming soon.

<span class="smashing-tv-host">Drew:</span> So even Linux desktop users can get in on the action.

<span class="smashing-tv-speaker">Aaron:</span> Eventually, that’s the hope.

<span class="smashing-tv-host">Drew:</span> Fantastic. So as far as I understand it, and correct me if I’m wrong here, but Edge was technically a continuation of the Internet Explorer code base, is that fair to say?

<span class="smashing-tv-speaker">Aaron:</span> Yeah, when Edge first started, it was basically kind of rip out all of the stuff that we realized was just kind of lagging around, things that had been proprietary and stuff like that. All of the old browser helper objects and activeX stuff and things like that. So it was massively gutted. It was kind of a chance for the team to really get rid of a lot of the legacy baggage and focus on the standard stuff. And so it was a continuation of the old Triton engine, but kind of refactored and made into the Edge HTML engine.

<span class="smashing-tv-host">Drew:</span> So it was like a massive home renovation inside the code base.

<span class="smashing-tv-speaker">Aaron:</span> Yeah, take it to the studs.

<span class="smashing-tv-host">Drew:</span> So I guess the biggest change that I want to talk about with the very newest version of Edge is that even more of those sort of older guts have been ripped out and replaced. And there’s a new rendering engine that’s been installed. Now I’m a little conscious of using jargon and people who aren’t maybe so familiar with the workings of browsers might not be completely happy with, what do we mean by a rendering engine. I think some of us who’ve been around and working on the web a long time will have picked up that information, even if we’re not working directly with the internals of browsers. But somebody who’s perhaps newer to web development might not understand, what do we mean by a rendering engine. So, what is a rendering engine inside a browser? And which bits aren’t a rendering engine?

<span class="smashing-tv-speaker">Aaron:</span> Well, there’s a bunch of different parts to a browser. The rendering engine is what we typically think of when we’re talking about what’s being actually painted to the screen and sort of the interactive layer of things. And so in the Chromium world, that is the Blink rendering engine.

<span class="smashing-tv-speaker">Aaron:</span> And then there’s the WebKit rendering engine, which is what runs Safari. And that was based on the KHTML rendering engine, which ran Konquerer back in the early days.

<span class="smashing-tv-speaker">Aaron:</span> The Trident rendering engine I mentioned before was the one on Internet Explorer for Windows. Tantek Celik had made the Tasman rendering engine as part of the team that was working on IE5 for Mac.

<span class="smashing-tv-speaker">Aaron:</span> So there are all these different rendering engines out there. And in fact I think there was a new one that Peter Paul Cox was just talking about called Flow. That’s like a multi-threaded rendering engine that’s based on SVG or something like that. And there’s a forthcoming browser for that that was designed for set top boxes, really low powered devices.

<span class="smashing-tv-speaker">Aaron:</span> But yeah, the rendering engines, taking all of your information and painting it to the screen. And then you’ve got your sort of underlying JavaScript engines as well. So v8 in the case of the kind of Chromium stack. And there are a bunch of different ones for that as well.

<span class="smashing-tv-host">Drew:</span> So when we say that the old rendering engine Trident, that came from IE and has been in Edge has been replaced. We’re actually talking about the bit that paints stuff to the screen and also associated things like the JavaScript engine. Is that fair?

<span class="smashing-tv-speaker">Aaron:</span> Yeah, in the case of the new Edge version, basically none of the underpinnings of old Edge are there. The Chromium project is an open source project that runs Chrome and Brave and a bunch of other, Opera and such. And that project includes the rendering engine, it includes the JavaScript engine, it includes all of the UI. It also includes the build process and all of that sort of stuff for actually creating the browser.

<span class="smashing-tv-speaker">Aaron:</span> And so we basically have the Chromium project, became the basis for the new Edge. And so we had to go through the process of making it look like Edge and adding in the functionality that we needed in terms of synchronization, using Microsoft accounts, all of that sort of stuff.

<span class="smashing-tv-speaker">Aaron:</span> So the new Edge does not share any lineage in kind of the traditional sense with the old Edge, which was Edge HTML, which inherited from Trident and so on and so forth. And you can keep going all the way back to Mosaic for most of these.

<span class="smashing-tv-speaker">Aaron:</span> But yeah, so now the new Edge is Chromium, which is based on WebKit before it, which is based on KHTML and so on and so forth. So it’s a completely different lineage than the previous one.

<span class="smashing-tv-host">Drew:</span> So, I mean, that’s a massive change isn’t it, for Microsoft to no longer have a browser that’s originated in its own code. But is actually taking an open source project and creating its own browser from that. Which I guess is similar to what Apple did back in the day with WebKit. What, was it KHTML they ... ?

<span class="smashing-tv-speaker">Aaron:</span> Yeah, it was Konqueror was the ... with a K.

<span class="smashing-tv-host">Drew:</span> Yes, Konquerer, so they took that open source project and that became Safari. And so Microsoft is doing a similar thing with the Chromium project and has made Edge out of it?

<span class="smashing-tv-speaker">Aaron:</span> Correct.

<span class="smashing-tv-host">Drew:</span> If I’m sat down in front of Edge as a web developer, what that I’m looking at is unique to Edge, what would I be seeing that I wouldn’t see if I was sat down in front of Chrome for example?

<span class="smashing-tv-speaker">Stephanie:</span> A lot of the features right now in this first stable release are consumer focused. So, there’s Collections which is coming out, which is a pretty cool way to pull stuff from the web into individual collections, hence the name. And you’re able to take that data and kind of put it into a side pane and then export it out to Word and Excel I believe. I’ve been using it for design projects and other things. It’s just cool for gathering resources.

<span class="smashing-tv-speaker">Stephanie:</span> And then one of the other features for Enterprise customers, and it’s only available on Windows, is IE mode. So that will actually render Internet Explorer within a tab in Edge for people who still need those pages that rely on old technology. So that’s pretty cool.

<span class="smashing-tv-speaker">Stephanie:</span> And then in terms of developer tooling, everything right now is the same. I know we have some stuff upcoming that is going to get ported up to Chromium, but there’s a cool 3D DOM viewer that’s in the works and the team’s been iterating on. And there are some other tools that don’t exist in Chrome yet that are coming. So that’s exciting.

<span class="smashing-tv-host">Drew:</span> So that’s a big deal for web developers, isn’t it? Because I think typically people get used to using a set of developer tools in their browser of choice and quite often frankly that is Chrome these days for a lot of web developers. So to be able to go across to Edge and find a very similar set of developer tools has to be quite a draw, do you think?

<span class="smashing-tv-speaker">Aaron:</span> Yeah, I think so. I mean it’s the sort of thing where you’re going to have the exact same tool set. We’re built on top of Chromium, including all of the dev tooling. We have been making a lot of investments in, as Stephanie was talking about, with the 3D DOM viewer. We’ve been making a lot of investments in terms of improving the overall accessibility of the dev tools, adding new tools into it, working on internationalization of the dev tools.

<span class="smashing-tv-speaker">Aaron:</span> And as Stephanie mentioned, the vast majority of the work that we’re doing, basically anything that is not UI specific to Edge or that involves our sync platform or things like that, all of that is being up streamed into Chromium. So the fixes that we make, the improvements that we make for accessibility are going to make Chrome better, are going to make Brave better, Opera better. They’re even going to make Electron better.

<span class="smashing-tv-speaker">Aaron:</span> So, it’s really neat to be kind of part of that larger ecosystem. And to be able to have impact beyond our own browser. And so dev tools has been an area we’ve been making a lot of investment. We’ve been doing a lot of work with partners in the Chrome team on progressive web apps as well. And trying to figure out what do progressive web apps, or what should they look like in desktop environments, because a lot of the focus has been on mobile.

<span class="smashing-tv-speaker">Aaron:</span> And then there’s also been a lot of work between the Dev Tools Team and the folks working on VS Code to make those tools work better together. So that you can basically access the dev tools from the browser from within VS code while you’re debugging your pages. And everything is kind of connected, like being able to click on a style rule in the Edge dev tools actually it will take you to that line in VS code in your style sheet. Which is mind blowing, it’s really cool stuff.

<span class="smashing-tv-host">Drew:</span> That sounds really exciting. I know VS Code is something that seems to be gaining an awful lot of traction in the web development community. I think it’s actually brought a lot of people back to Microsoft Tools who might have drifted away over the years. Certainly feels like a different era of Microsoft, as does this sort of embracing of open source and the new version of Edge. It all seems quite exciting and quite refreshing from a web development point of view.

<span class="smashing-tv-host">Drew:</span> Also from that point of view it seems like this is a really great convenience for web developers because if some of the major browsers, Chrome and Edge in particular and you mentioned Brave and Opera, what have you, are all using the same rendering engine, presumably that cuts down on masses of compatibility problems and browsers that don’t need to be tested in lots of different places. It should all just work the same, is that fair?

<span class="smashing-tv-speaker">Stephanie:</span> Yep.

<span class="smashing-tv-host">Drew:</span> Amazing.

<span class="smashing-tv-speaker">Aaron:</span> That’s the dream, right?

<span class="smashing-tv-host">Drew:</span> That is always the dream. It does raise a little bit of a concern though doesn’t it in the reduction of sort of healthy competition in the marketplace. Whereas we had Microsoft pushing their browser forward, Google pushing their browser forward. Apple hopefully ideally pushing their browser forward, Opera and all the other players. And that sort of creates this atmosphere of healthy competition where everyone’s trying to keep up with each other and trying to make improvements. If a lot of big players are all using the same rendering engine does that healthy competition suffer?

<span class="smashing-tv-speaker">Aaron:</span> This is something that I definitely have, having been a long time web standards person, kind of struggle a bit with, I don’t think ... I totally get the business justification for it. From Microsoft’s standpoint it made a lot of sense. And from a front end dev perspective it’s nice to not have to cater to a bunch of different engines.

<span class="smashing-tv-speaker">Aaron:</span> I mean, on the whole, those of us who’ve been working on the web for a long time, have certainly seen a lot of convergence in terms of rendering. We don’t have as many problems as we had say back in the Netscape 4.7 days where we had just like, you know, I knew companies that were creating unique style sheets for each different browser which was just untenable.

<span class="smashing-tv-speaker">Aaron:</span> But I think what’s kind of different now is that back in the original browser wars you had all of these proprietary engines and everybody was kind of in a game of one-upsmanship in terms of trying to ship new platform features and new JavaScript features. Or in the case of Microsoft reverse engineering JavaScript in order to create J Script and trying to figure out how to fit it all together.

<span class="smashing-tv-speaker">Aaron:</span> But now we have the ability to actually work together in open source projects and still have the dialogue and still, I don’t know, fights not the right word, but to have serious discussions about the impact of different approaches. And to disagree with each other. And to really work on making specs really good. And to also have competing approaches to the underlying code within the context of say a Chromium project or WebKit or something of that nature or Mozilla in the Firefox space.

<span class="smashing-tv-speaker">Aaron:</span> So yes, on one hand we did lose another rendering engine. And I felt that same pain when Opera decided to go to Chromium. But I do feel somewhat heartened being inside Microsoft and seeing how committed we are to actually participating in the Chromium project in a meaningful way. And not just kind of sitting back and just accepting everything that comes downstream from Chromium, but actually kind of vetting what’s going into the platform and participating in that.

<span class="smashing-tv-speaker">Aaron:</span> So I’m a little bit heartened by that and feel like we’re not just there to take from that project and just accept whatever gets passed down by all of the different people who have a stake in that project. But to actually be collaborating in there as well.

<span class="smashing-tv-speaker">Aaron:</span> I think we still need to figure out what this means for standards bodies in terms of interoperable implementations. Because basically if you’ve got some browsers that decide they don’t want to implement something, they can totally stop something from becoming a standard. Even if all of the developers in the world wanted it.

<span class="smashing-tv-speaker">Aaron:</span> And it may not be anything like where they don’t agree with it. They just may not have the bandwidth to build the feature. Everybody’s pressed for staff and such.

<span class="smashing-tv-host">Drew:</span> I guess really the collaboration on the web as a platform has just moved locations from everybody agreeing to implement things the same in their individual code bases to some major players working together on the same code base essentially.

<span class="smashing-tv-host">Drew:</span> I mean, you mentioned briefly disagreements and obviously that’s something that could be a concern, I guess, in any open source project. But do we know how that will work, if developers from Google, for example, want to implement a feature and developers from Microsoft really don’t want to see that implemented. Do they just fight it out over GitHub issues?

<span class="smashing-tv-speaker">Aaron:</span> I mean, a lot of this stuff does happen in the open, either on GitHub issues or in the Crbug, which is the bug tracker for Chromium. I am not a browser engineer so I don’t know all of the details of the internals, but I believe there are a lot of things that we can basically turn off if we don’t want them.

<span class="smashing-tv-speaker">Aaron:</span> And I know Google has been working on sort of cleaning up or doing some housekeeping within the Chromium project to extract more of the Google related services and such up to the layer of converting it from Chromium to Chrome.

<span class="smashing-tv-speaker">Aaron:</span> And so we have a similar process taking Chromium and turning it into Edge. And obviously, we wouldn’t want to check in the design of the Edge UI for instance. Or the Collections thing, which is more of a UI user focus thing that Stephanie was mentioning, we’re not up streaming those into Chromium. Those exist in kind of the UI portion.

<span class="smashing-tv-speaker">Aaron:</span> So, as far as I understand it, as features come out of Chromium we have the ability to kind of turn off certain things that we may or may not like. And I know Brave does the same sort of thing because they have a much different approach to privacy than say Google does. And we may have a slightly different take than either of them or what have you.

<span class="smashing-tv-speaker">Aaron:</span> So I think there’ll be kind of things that happen at different points. Some of which will be kind of where the project gets converted into the browser from the open source project. Some of it will be within the standards organizations or interest groups within the standards organizations and so on.

<span class="smashing-tv-host">Drew:</span> And I guess it works the other way as well, doesn’t it? You mentioned a browser not having enough engineers on hand to develop a particular feature, traditionally the way things have worked within standards bodies is that we need multiple different implementations before something is accepted as part of the standard. Obviously that needs to be figured out if there aren’t that many implementations available to actually test with.

<span class="smashing-tv-host">Drew:</span> But, for example, if Microsoft wanted to implement a feature and Google decided that they just didn’t have the resources to implement that feature, it wasn’t high enough on their priority list, well, potentially they’re going to get it for free anyway because it just gets up streamed into the open source project. And then they can access it and all their users benefit without any of their engineers particularly needing to spend a significant time developing that.

<span class="smashing-tv-host">Drew:</span> I mean, if Mozilla decided that they were going to do the same with Firefox and just adopt the Chromium project, do you think that would be a problem for the web?

<span class="smashing-tv-speaker">Stephanie:</span> I mean, I would say yeah, because then we’re in this browser monoculture and honestly, I love Firefox. Firefox has some great tooling that Chromium doesn’t have. That would be, I think, really terrible to lose. And it’s kind of nice to have sort of an independent browser out there still fighting for the open web. I mean, we’re fighting for the open web too, but I think what Firefox is doing is still important.

<span class="smashing-tv-speaker">Aaron:</span> I mean, I kind of wonder what would happen if, let’s say, whether it’s Chromium or whether it’s WebKit or some fork of an existing open source project, what if a standards body kind of controlled the rendering engine and the JavaScript engine. And all of the browser makers were contributing to the development and kind of the ongoing creation of that. Would that necessarily be a bad thing or would it be a good thing? I don’t know. I don’t know what the answer is to that, but it’s kind of an interesting prospect that if ... Browsers are not inexpensive and inconsequential to build, and especially rendering engines. It’s going to be probably relatively unlikely that we’re going to see a whole lot of new rendering engines and big investments in that area. Because so many companies have shifted to focusing on their services.

<span class="smashing-tv-speaker">Aaron:</span> With Apple, with all of its iCloud and its whole ecosystem. And Mozilla has been doing some similar things with their acquisition of Pocket and such. And then certainly there’s the Google suite of products, the Microsoft suite of products, etc. And Brave is focused around privacy and the basic attention token and that sort of thing. Everybody kind of has their little ecosystem of things.

<span class="smashing-tv-speaker">Aaron:</span> And so, I don’t know that there’s going to be a whole lot of interest in building out a new rendering engine and a new JavaScript engine to challenge the ones that are there. So, it’s kind of a question of will there continue to be kind of a consolidation. And if more people are actively interested in the ongoing development, and kind of having those difficult conversations about where the engine is going and where the web platform is going, could that be a good thing, I don’t know. It’s kind of an interesting thought experiment though.

<span class="smashing-tv-host">Drew:</span> It really is. The new Edge sounds really exciting. I’ve been playing around a little bit with the betas and enjoying that. How long do you think it will take for this new version to roll out to the world? Because it's, I mean, only just been released this month, hasn’t it, we’re January 2020.

<span class="smashing-tv-speaker">Aaron:</span> Yep, January 15th, it went to general audience basically. So, we’ve had the Canary dev and beta versions. Gosh, when did we start rolling this out, Stephanie, do you remember?

<span class="smashing-tv-speaker">Stephanie:</span> I’m going to say six months ago, but I honestly, I’m just throwing that out there. I feel like I’ve been using Canary as my daily driver for what feels like months.

<span class="smashing-tv-speaker">Aaron:</span> Yeah, I think we’re kind of skewed because we started using it internally for a bit before we started to open it up to the public. But yeah, I think I want to say we started sharing it at Build last year, which would have been May, I think is when the Canary, and maybe the diversion route, I don’t remember if beta was out then. But yeah, the fully stable version came out on the 15th.

<span class="smashing-tv-host">Drew:</span> So, you’re both involved in a project called <em>The Web We Want</em>, which is a sort of initiative between lots of different browser makers, is that right?

<span class="smashing-tv-speaker">Stephanie:</span> Yeah, so <em>The Web We Want</em>, I think Aaron started it last June or so and we started talking about it. And yeah, <em>The Web We Want</em> is basically an initiative and Aaron and I have been the primary ones kind of running it, but we’ve had interest from other browser vendors and folks who work on those teams.

<span class="smashing-tv-speaker">Stephanie:</span> And it’s basically just a way to gather feedback from developers about problems that they’re having on the web. Because we, as people who build the browser, can kind of focus on those new shiny things that we want to implement. But developers, as we’ve come to see through this initiative, there’s a lot of stuff that they’re still struggling to build that isn’t native in the browser. That probably should have been solved by now, but hasn't.

<span class="smashing-tv-speaker">Stephanie:</span> And so that’s kind of what the initiative is all around, finding out what those problem areas are and then taking those back to browsers and standards bodies if it’s that sort of problem.

<span class="smashing-tv-host">Drew:</span> So, what sort of form does that take? Is it something you do in person or is it all online?

<span class="smashing-tv-speaker">Stephanie:</span> So, we have two components to it. So you can go to webwewant.fyi and you can fill out a form with your problem and your use case that you’ve encountered on the web. And then Aaron and I have been, I think we went, well, I think we’ve hosted six or seven events within a conference or a meet up.

<span class="smashing-tv-speaker">Stephanie:</span> And so the form that that takes is we usually have a 45 minute to hour long session at a conference we’re partnering with. And we give people who have submitted their problems that they’ve encountered on the web a chance to present those to a panel of judges who are usually industry experts.

<span class="smashing-tv-speaker">Stephanie:</span> And in between we usually have four or five of those problems presented during a session. And in between each of those we have our panel of judges kind of talk about the problem space that’s being presented. And whether or not it’s an interesting problem space. Or if they think it would be useful for browser vendors to go work on that.

<span class="smashing-tv-speaker">Stephanie:</span> And then at the end of that session we have our judges pick what they think is the most pressing problem to go and fix. And we also have an audience component, so the audience for the session also gets to vote on what they think is the most pressing thing that browser vendors should go fix.

<span class="smashing-tv-speaker">Stephanie:</span> And then we take that data back to our teams. And we’re currently in the process of figuring out how to disperse that out among the different browser teams.

<span class="smashing-tv-host">Drew:</span> Are there any sort of standouts, suggestions that you remember that have particularly stuck with you?

<span class="smashing-tv-speaker">Stephanie:</span> So, there’s been a couple, the one that keeps sticking out for me though is HTML Controls keep coming up. And that’s sticking out for me because I’m working on a talk right now that involves HTML Controls and how just not being able to style them or extend them is an issue. And so it’s kind of cool to see that feedback reiterated even more.

<span class="smashing-tv-speaker">Stephanie:</span> There’s been some really interesting, there was one for a source view order or source order viewer in the dev tools that had to do with, I believe, seizes grid content and seeing, because you can kind of move things out of order, and having that kind of identify how things flow through the DOMs. So, I think that would be a really cool thing to get implemented in the dev tools.

<span class="smashing-tv-speaker">Aaron:</span> Yeah, there’s been a lot of accessibility related submissions which has been really neat. Another one that was dev tools and accessibility related was actually, rather than sort of relegating accessibility testing to its own part of the, was it the audits tab, I think it’s where it currently, like lighthouse does some accessibility testing, or you could use web hint or accessibility insights and such.

<span class="smashing-tv-speaker">Aaron:</span> The idea of this is to actually start capturing some of the low hanging fruit in terms of accessibility errors and bubbling that up in the console for instance. So, if it sees that you have some images that are missing alt text or some really tiny fonts or not enough contrast, it could actually throw those as errors in the console. And that tends to be where a lot of developers are checking to see if their stuff is operating properly. So that would make it a little bit more obvious to folks that they have accessibility issues that they need to address.

<span class="smashing-tv-speaker">Aaron:</span> And you could see some similar ways to incorporate that into the Dom viewer or the CSS inspector tools where it could flag something as being too low contrast or highlight an element as having some accessibility issue that’s known. That sort of thing would be pretty interesting.

<span class="smashing-tv-speaker">Stephanie:</span> Yeah, I want to piggyback off that. There was actually a really interesting one presented at View Source in Amsterdam last year. It was around the browser automatically fixing certain types of accessibility issues for you. And just with color and contrast or maybe certain fonts being unreadable. And the proposal and the case study presented was really, really well thought out. But it also kind of poses this interesting question of if the browser starts to fix things for you as a developer, are you going to write bad code because you don’t have to worry about it.

<span class="smashing-tv-speaker">Stephanie:</span> So it was interesting because the ideas that he put forward and kind of demoed were really cool. But that’s kind of what does that mean for developers so, are they going to get lazy. So, I’ve seen some cool stuff come out of it.

<span class="smashing-tv-host">Drew:</span> So I guess it’s still pretty early days, isn’t it, for the initiative. So I guess we’ve not seen anything go as far as actually reaching even early development stages with any browsers. Do you know what that process will look like, you said you were still sort of trying to figure it out, is that right?

<span class="smashing-tv-speaker">Aaron:</span> Yeah, we’re all still trying to figure it out, but we do have the right people involved. We’ve got folks from Mozilla and from Google and from Igalia as well, they were the ones who did a lot of the grid work and they’re very familiar with how all of this standard stuff works. In fact, I think they’re doing Methanol right now, doing the implementation for WebKit.

<span class="smashing-tv-speaker">Aaron:</span> So yeah, we’ve got a bunch of people on board that are keen to work on this and keen to see it be successful. And the W3C is paying attention to it as well, which is cool.

<span class="smashing-tv-speaker">Stephanie:</span> So, for us right now, we’ve taken the, I think we have 12 top, we took the winners from each event last year, and I’ve kind of bucketed them out into their specific categories. So some are dev tools focused, some are HTML, web platform focused. And then I can’t remember what the third category was, it was just kind of general.

<span class="smashing-tv-speaker">Stephanie:</span> And so on the Edge side we’re starting to at least look into, I’ll have a couple of Twitter surveys going out actually hopefully sometime soon to help gather more feedback to validate that these are problem spaces that we should invest time in. And then hopefully we’ll go from there. So I’m hoping sometime this year we’ll start to see some sort of progress. But it is a little bit slow at the moment.

<span class="smashing-tv-host">Drew:</span> It’s great because the web actually is a very collaborative platform. And I think as a web developer just building sites on the day to day, you forget that there’s actually ways to feed back into the process and ways to make your voice heard. And I think this sounds like a really great, easy way to make your voice heard.

<span class="smashing-tv-host">Drew:</span> If any of our listeners wanted to come along to a <em>Web We Want</em> session, are there any coming up?

<span class="smashing-tv-speaker">Stephanie:</span> There are a couple, so let me pull up my list here. So, well, Open Source Festival in Lagos, Nigeria. Aaron and I won’t be there, but they’re actually running that event independently.

<span class="smashing-tv-speaker">Stephanie:</span> And then I will be at SF HTML5 in San Francisco at the end of March. I believe that’s free, but don’t quote me on that. I have to check. So if you’re in the San Francisco area, we’re running it there.

<span class="smashing-tv-speaker">Stephanie:</span> And then SmashingConf San Francisco in April. We will be running it there.

<span class="smashing-tv-speaker">Stephanie:</span> And hopefully TBD, still looking at SmashingConf Austin.

<span class="smashing-tv-speaker">Stephanie:</span> And I believe that’s all we have on the calendar right now. But, going to do a little plug here, if you run a conference or a meet up and would like this community focused session to be run there, please reach out because it’s really cool.

<span class="smashing-tv-host">Drew:</span> Of course, the SmashingConfs are the best ones to go to we think here.

<span class="smashing-tv-speaker">Stephanie:</span> Yes, yes they are.

<span class="smashing-tv-host">Drew:</span> So, to me that sounds all really, really exciting. And I’m heartened to see all the big browser makers actually coming together and backing that sort of initiative to get out and to talk to web developers, talk to the people who are actually solving these sort of everyday problems, building websites and apps for their clients and for their companies.

<span class="smashing-tv-host">Drew:</span> I think it’s really important to actually listen to the people who are at the coalface doing the work.

<span class="smashing-tv-host">Drew:</span> I normally ask at the sort of end of these episodes, what have you been learning lately? Because we’re all about learning stuff here at Smashing, but really with <em>Web We Want</em>, I think you must be learning all these things all the time by speaking to web developers. So I really think we’ve covered masses there.

<span class="smashing-tv-host">Drew:</span> Is there anything else that you wanted to mention about <em>Web We Want</em> or about the new version of Edge that we hadn’t talked about?

<span class="smashing-tv-speaker">Aaron:</span> I just think if folks have ideas, even just the germ of an idea, some cow path that you think should be paved for the web, reach out to us, let us know. We’re happy to also work with you on kind of refining the submission. So, in a lot of cases we’ll get a submission that’s kind of a germ of an idea. It’s not perfectly articulated or anything like that. And we work with those authors to make sure that we kind of capture what it is that they’re looking to put out there. So, don’t worry about your grammar or your spelling or anything like that. It’s not like we just post it up as soon as you send it, we’ll look at it, review it.

<span class="smashing-tv-speaker">Aaron:</span> And in some cases people have suggested things that actually exist, in which case we tell them, hey, you can actually do that and here’s a way to do that. So we can, it’s a little bit of stack overflow as well. Because he can tell you if there’s something that you can do that already with standards.

<span class="smashing-tv-speaker">Aaron:</span> But yeah, I mean, we want any and all ideas on how we can improve the web. Hopefully they’re actionable ideas. In some cases we get like, the web is too hard. And it’s like, you know, I feel you, but, you know, not something browser vendors can really solve.

<span class="smashing-tv-speaker">Aaron:</span> But yeah, I mean, we want to know what is it that you’re doing, where you’re running into problems. We have the kind of saying, if you could wave a magic wand and fix something on the web, what would it be?

<span class="smashing-tv-speaker">Aaron:</span> And yeah, so you can can hit us up via the forum. Stephanie mentioned webwewant.fyi. Or we’re webwewantfyi on Twitter. Yeah, please reach out.

<span class="smashing-tv-speaker">Stephanie:</span> I will also pile on just to talk something about Edge that also, the team is super hungry and eager to get feedback from all of our users. So if you’re in Edge and there’s something you don’t like or there’s something you love, there’s a little feedback icon you can click. All of the teams see that feedback and are looking at it. And if you have a problem are very proactive and engaging. And you can always ping MS Edge Dev on Twitter if you have a problem and it hasn’t been addressed yet. So trying to be super proactive and really build a browser that not only developers want to use, but the world.

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Aaron or Stephanie, you can follow them on Twitter where he’s @AaronGustafson and she’s @seaotta. You can find <em>The Web We Want</em> at webwewant.fyi.

<span class="smashing-tv-host">Drew:</span> Thank you for joining us today Aaron and Stephanie, do you have any parting words?

<span class="smashing-tv-speaker">Stephanie:</span> Thanks.

<span class="smashing-tv-speaker">Aaron:</span> Adios.

{{< signature "dm, ra, il" >}}
