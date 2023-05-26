---
title: 'Smashing Podcast Episode 3 With Jina Anne: What Are Design Tokens?'
slug: smashing-podcast-episode-3
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4a75941-2926-42f0-bb09-8e1b328e67be/smashing-podcast-episode-3.png
date: 2019-11-19T05:00:00.000Z
summary: >-
  What are Design Tokens and how are they used? In this episode of the Smashing Podcast, Drew McLellan talks to Design Systems expert Jina Anne.
description: >-
  What are Design Tokens and how are they used? In this episode of the Smashing Podcast, Drew McLellan talks to Design Systems expert Jina Anne.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode of the Smashing Podcast, we’re talking about Design Tokens. What are they, what problem do they solve, and how can they be used within an existing Design System? Drew McLellan talks to someone who is much more than a token expert: Jina Anne.

<iframe src="https://share.transistor.fm/e/f8df456f/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

 - “[What Are Design Tokens?](https://css-tricks.com/what-are-design-tokens/),” *by Robin Rendle*
 - “[Design Tokens For Dummies](https://uxdesign.cc/design-tokens-for-dummies-8acebf010d71),” *by Louis Chenais*
 - “[Style Dictionary](https://amzn.github.io/style-dictionary/),” *a build system for creating cross-platform styles.*
 - “[Theo](https://github.com/salesforce-ux/theo),” *an abstraction for transforming and formatting Design Tokens.*
 - “[W3C Design Tokens Community Group](https://www.w3.org/community/design-tokens/),” *proposed and run by the community.*

## Transcript

<p><a href="https://twitter.com/jina"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c20c86-9a27-496d-a3a7-169765d967bc/smashing-podcast-3-jina-anne.png" width="200" height="200" alt="Photo of Jina Anne" /></a><span class="smashing-tv-host">Drew:</span> She’s a design systems advocate and coach. While at Amazon, she was senior design systems lead and she was lead designer on the Lightning Design System at Salesforce, while at Apple she led the CSS architecture and style guide for the Apple Online Store. She’s worked with GitHub, Engine Yard, and the Memphis Brooks Museum of Art and more. She founded and organizes Clarity, the first design systems conference, and is on the Sass core team where she leads the brand design and website for Sass. When it comes to design systems, you’d be hard pushed to find anyone more qualified, but did you know that she’s never seen a sidewalk? My smashing friends, please welcome Jina Anne. Hello, Jina.</p>

<span class="smashing-tv-speaker">Jina Anne:</span> Hello.

<span class="smashing-tv-host">Drew:</span> How are you?

<span class="smashing-tv-speaker">Jina Anne:</span> I'm smashing.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you today about design tokens, which I think is a phrase many of us have probably heard passed about, but we perhaps aren’t sure what it means. But before we get to that, I guess we should talk a little bit about design systems. I mean, design systems are your thing, right?

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah. It rules everything around me. Yeah.

<span class="smashing-tv-host">Drew:</span> I think that there’s something that we’re seeing is becoming increasingly common in projects and people are making them public and seems to be a real movement around design systems. But I think there are plenty of organizations that don’t have them in place still. What problem does a formalized design system solve from your point of view?

<span class="smashing-tv-speaker">Jina Anne:</span> It can solve many problems. I think some of the more common problems that people seek to solve is around maintainability and consistency. That usually has to do with design debt or in some cases code debt, some cases both. I also look at it as a... Like, it’s not just about the code or the design, but also the problems around how people work together. So, I look at it as a way to also solve some of the issues around communication and workflow process and so on.

<span class="smashing-tv-host">Drew:</span> Are design systems then something exclusively that are useful to really big teams and big organizations?

<span class="smashing-tv-speaker">Jina Anne:</span> I don’t think so. I’ve seen them work really well with smaller teams or sometimes even with a lone designer. They definitely help with larger teams for sure, but they are definitely not exclusive to large teams. In fact, I think if you see yourself perhaps growing at some point to be a large team, then having the system in place already will help you do that more efficiently.

<span class="smashing-tv-host">Drew:</span> What did you think are the sort of symptoms that somebody might be looking for if they’re working and they’re still having problems? What do those problems look like that might be solved by putting a design system in place?

<span class="smashing-tv-speaker">Jina Anne:</span> There’s a few, duplication of efforts, duplication of code. You might have a breakdown in communication where things just aren’t being built the way they’re expected to be built. It could come down to things that aren’t documented well, so people don’t really quite know what the best thing is to use or where to look. Yeah, there are all sorts of signs.

<span class="smashing-tv-host">Drew:</span> I guess design systems are generally a concept, rather than a specific technical solution. In your work, you must see people using all sorts of different tools to achieve design systems.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> What are some of the more common ways that people actually go about it?

<span class="smashing-tv-speaker">Jina Anne:</span> I think the most common ways are having a component library done in code and often cases you’ll see it in it like a React library or an Angular library, whatever, platform you’re using. There’s usually also a website associated with it that will display those components. Then you’ll usually see perhaps like a Sketch or a Figma library as well.

<span class="smashing-tv-speaker">Jina Anne:</span> But one of the things that I like to stress to people is that if you look at that website that displays your documentation and your components, that website is not actually your design system. It’s a representation of your design system. So, I think a lot of people spend a lot of time on making this gorgeous, beautiful website and it’s fine. They’re nice to look at and they’re nice to share and they help a lot with communicating what you’re doing and even with recruiting.

<span class="smashing-tv-speaker">Jina Anne:</span> But it’s the system itself that it represents that I want people to spend their love and care into, so thinking through what’s going into that website, like the content and how you’ve organized things, how you’ve named things, the things that you’re systemizing, so, yeah. I think a lot of people think about the artifacts, like the deliverables, but really it’s a lot more than that. It’s a lot of process and workflow as well.

<span class="smashing-tv-host">Drew:</span> Is it exclusively web projects that the design system would help with?

<span class="smashing-tv-speaker">Jina Anne:</span> Not at all. It is the most common, I believe, from, at least, what I’ve seen, but design systems definitely can cover many things. In the digital space, you have native platforms, but even outside the digital space, I think a lot of people talk about design systems in a digital product space. But they’ve been around for ages for traditional medias and real-world scenarios. If you have seen the NASA graphic standards manual from like the '70s, that was a design system. It just was across all the different like rockets and spacesuits and all that, instead of digital products.

<span class="smashing-tv-host">Drew:</span> So, I guess, there must be some overlap between things, traditional things like brand guidelines and that sort of documentation that I think probably people are familiar with in all sorts of walks of life. There must be a crossover between that sort of documentation of a system and a more modern concept of a design system.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah, I believe so. I think a lot of people forget that it’s all about branding. The whole reason any of this even started and why we want to display these things in a uniform or unified way is all about the brand because brand isn’t just logos. It’s how people use and experience your company’s service or product or whatever it is that you offer. So, yeah, absolutely.

<span class="smashing-tv-host">Drew:</span> So, I’ve got a design system in place, I mean an organization. We’ve done a whole lot of work. We’ve got a design system. There are creatives within the organization working in maybe, like you mentioned, Figma or Sketch. We’ve got web designers using that in a CSS. Perhaps we’ve got a mobile team doing like Android and iOS development, building apps. Loads of people working with a design system contributing into it and consuming stuff from it. Where do design tokens come in? What problem do they solve?

<span class="smashing-tv-speaker">Jina Anne:</span> Ooh, yes. Let me first take it back to a story. When I first joined at Salesforce, I was actually part of a small project team. It was a different product, it’s like a productivity tool like tasks and notes and things like that. We were only three designers and I was the only one that, I guess, I wouldn’t say brave enough, but maybe interested enough to work with the Android designs. The other two designers, I think, just weren’t quite as interested. So, I was basically the main designer on our Android app. Then I also did a lot of design for iOS app and, of course, the web application as well and the marketing website, so lots of different projects in play.

<span class="smashing-tv-speaker">Jina Anne:</span> With the website, since I like to design and code, it was pretty straightforward. I could go ahead and build the buttons and typography and everything that we needed for the web application or the marketing website, document it in code and deliver that.

<span class="smashing-tv-speaker">Jina Anne:</span> However, with both the Android and iOS app, I don’t really know how to code for that and so I wasn’t able to deliver the same thing. So, I was having to do a ton of redlines specs, which, if you’re not familiar with redlines, it’s essentially where you are specking out every single spacing, font size, color, anything to indicate how to build it for the engineer. I would do these for many, many, many screens and, of course, a lot of those screens had variations because maybe you’re showing what happens when you clicked that button or when a certain state happens. So, doing this across many, many screens and then saving those up to Dropbox and then documenting it in a Wiki. That was the process that I was having to do at the time.

<span class="smashing-tv-speaker">Jina Anne:</span> I usually think about things in a CSS way, like especially the C in CSS, so I usually think, "Oh, well, font sizes should only need to be declared one time because it’s going to cascade everywhere." But I found that with certain engineers that I’ve worked within the past, if you don’t spec it, and I guess with native it works a little differently, they’re not going to build it and so I would have to be very explicit and name pretty much everything per screen. I was just like, "Oh, why is it like this?" Then any time we made any changes, I had to go back through and change all those screens again. It was not fun at all.

<span class="smashing-tv-speaker">Jina Anne:</span> Fast forward to when I moved over to the core team of Salesforce, I had been working in the Sass website and I’ve been playing around with using a YAML file to store the data for colors, typography, spacing and so on and was looping over that data to create the style guide, as well as the Sass variables in the classes. The reason I did that was we open-sourced the Sass website and I wanted people to be able to contribute to the design as well. But I didn’t want to make it a tedious process where you had to update the style guide along with any colors that you’re adding and so doing it this way, just kind of automated that process.

<span class="smashing-tv-speaker">Jina Anne:</span> I showed that to the team at Salesforce and then that kind of is where the concept of design tokens spawned off of. So they built a tool called Theo and there’s other tools out now that do the same thing like Style Dictionary. But the idea of it is you have this automated tool that takes the data that you give it and generates the code. You might think, "Well, that might be over-engineering variables. Why not just use variables?"

<span class="smashing-tv-speaker">Jina Anne:</span> Well, the idea is, as you alluded to earlier, like native platforms just take those attributes in a totally different way and so trying to scale design to Android and iOS, whatever other platforms that get Salesforce. We had some people on Java, we had some people on React yet, some people on Angular, PHP, not just internally at Salesforce, but also externally with all our partners and customers that were building their own applications. So, this was a way to store our visual information as data and then, in an automated way, generate the variables or the XML data you needed or the JSON data, whatever format that particular platform looked for.

<span class="smashing-tv-speaker">Jina Anne:</span> Then what was great about it was we found, let’s say a color doesn’t pass contrast ratios. I didn’t have to then notify the Android team and the iOS team and the web team. I just made that change and then they would get that change automatically the next time that they would pull in the latest. So, it just really helped streamline a lot of that and helped us be able to take off some of the burdens of updating visual designs from the engineers and that let us do that.

<span class="smashing-tv-host">Drew:</span> So, instead of being sort of variables within one particular code base, within your own React codebase or within your PHP or within your Java or wherever, they’re like variables across an entire organization? Is that fair to say?

<span class="smashing-tv-speaker">Jina Anne:</span> Correct. Correct. Then what’s cool is things like colors, for example, like transparent colors, you do that differently in Android, like eight-digit hex, instead of RGBA like you would with web. So that tool that you use, if you’re using one that is built to think through all this, does that transformation for you. So, rather than saying RGBA 50 comma, 40 comma, whatever the color, you can just say color background card or something like that. It’s really more of a named entity now and then you can all be speaking the same language, even though it might render a different syntax.

<span class="smashing-tv-host">Drew:</span> Right. So, although variables kind of the nuts and bolts of how it might be implemented, the idea is kind of much bigger than just what you’d think of as just variables. I mean, I guess in a way like RSS could be called just variables. But, actually, the way it enables us to distribute blog content and podcasts and everything has a much wider impact than just the core technology that’s there.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah, I think that’s actually a really good metaphor. I do see a lot of people when they use it or talk about it in their own design system website, they’re usually only talking about like Sass variables or CSS variables. I think that’s why there’s this confusion, like, "Well, isn’t that just variables?" It's, like, "Why are we renaming it?" But it is that much broader application of it with a whole process around it. It even gets into like how you distribute those variables across components, like on a global level or on an individual component level. You can have multi-layers and so on. It can get pretty interesting.

<span class="smashing-tv-host">Drew:</span> So, I suppose as well as helping in the maintenance, you mentioned being able to change a color in one central location and then have everything that is, using those design tokens, be able to pick it up when the next build or next refresh from the system, presumably this has the potential to enable all sorts of other interesting things. I know a lot of people make sort of white-labeled products. It’s the same core product, but it’s customized with different design tweaks for different and things. So, using design tokens could actually be a solution for those sorts of applications as well, the need to span more than just one particular codebase.

<span class="smashing-tv-speaker">Jina Anne:</span> Right. Yeah. So, that was definitely a use case at Salesforce. We have a lot of, I don’t know why I'm still using present tense, but we had a lot of customers that wanted to be able to brand their UI that they were using. So, we had this concept of certain variables that we wanted to actually be seen more as like a constant, like maybe it’s an error color versus colors that were meant to be configured, like brandable colors. So, for some people’s needs that can get interesting, too, white labeling or offering any sort of theming, dark mode or night mode, even offering a feature, which you may have seen in Gmail, but it’s like that comfortable, cozy, compact spacing density. So, there are all sorts of extra stuff that you can get with it across multiple products very quickly, which is really nice.

<span class="smashing-tv-host">Drew:</span> It is really an extension of core principles of programming where you make sure that you’ve really defined things once in one place, so you don’t have multiple instances so it’s easy to update. But it is looking at that as a much, much bigger idea than just one small element of a product, looking at it across everything and centralizing that.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah, so we definitely looked at these as our source of truth. However, in case anybody is worried about like, "Well, Android does things differently than iOS," or you might have some concerns there. Depending on how you’ve architected things, you can still solve for those use cases. So, we would have a global token set that all our products would basically import in, but then we made them in a way where you could either alter it for that particular context or extend it, like offer maybe additional tokens that only that particular context needs. So, you can still give the fine-tune experience that you need to give to each of those context, while bringing in the most common shared things.

<span class="smashing-tv-host">Drew:</span> On a technical level, how would this actually work? Is there like a common file format the different systems share? Is there like an established standard for how you declare your design tokens?

<span class="smashing-tv-speaker">Jina Anne:</span> It’s interesting that you asked that. There’s actually a community group formed through... W3C has all these community groups. It’s not really exactly a working group, but it’s still like an initiative across various people that are in this space trying to come up with a recommendation of what those standards could be. Even how people store their data can change. Like it could be YAML, it could be JSON, it could even be a spreadsheet. Then what you export would be different because you might be using Sass, you might be using LESS, you might be using some sort of XML base system. We actually don’t want to tell you which of those things to use because depending on our use case, you might need to use spreadsheets instead of JSON or YAML or you might need to use XML instead of Sass or LESS or even CSS variables. That’s because everybody’s products are so different and have different needs.

<span class="smashing-tv-speaker">Jina Anne:</span> But what we can standardize on is around the tooling to generate these things. The reason we want to try to come to some sort of standard is because so many design tools are starting to implement this, InVision, Adobe, Figma. All these tools are looking at design tokens because there is a need to not just make this a code-based thing, but make this a design tool-driven thing as well. We don’t want to do it in a way where those tools don’t feel like they can innovate. We want them to be able to innovate, but at least offer some sort of standards so that new tool-makers can get into this space and already have sort of an established understanding of how to set that up. So, while we’re not going to get strict on your format of what file format you’re using or what tool you’re using, we’re going to more try to standardize on like the internal process and basically the API of it.

<span class="smashing-tv-host">Drew:</span> Because like I said, once that API has been defined, the tooling can spring up around it that speaks with that API for whatever tools that people want to use. So, somebody could write up a Java library that speaks that API, and then anything that’s using Java could make use of it and so on. Are there any tools currently that support design tokens in any way?

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah. On the code side, I mentioned already Theo and Style Dictionary. There’s also one called Diez, D-I-E-Z. That’s kind of newer to the space and it’s taking it beyond, just like doing the transformation process, but kind of treating design tokens as a component in a way and so that’s cool.

<span class="smashing-tv-speaker">Jina Anne:</span> Then on the design side, InVision already has it in their DSM tool, which is their Design System Manager tool. The last I looked at it, it was just colors and typography, but I do know when I... I talked to Evan, who is one of the main folks behind that product. He did tell me other things like spacing should be coming into play, if it’s not already. I haven’t looked at it super recently. I know there are newer tools that are really catching my eye, like modules and interplay. Both of those are code-driven design tools.

<span class="smashing-tv-speaker">Jina Anne:</span> Then I’ve been told that it’s supposed to come into some of the stuff that Figma and Adobe are doing, so I'm not sure if I'm revealing secrets. I don’t think I am. I think it’s all stuff they’ve talked about publicly. But, yeah, I'm really excited because I think while it was something that we were doing really just making our design system work easier, it’s kind of almost accidentally created a path for bringing design tools and code cluster together. That’s really exciting to me.

<span class="smashing-tv-host">Drew:</span> The makers of these various tools, are they working with the design tokens community group?

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah, a lot of them have joined. Since I'm a chair member, I get to see by email, everybody who joins. It sends me a notice. What’s cool is not only just seeing all these design tool people joining, but also seeing big companies. I saw like Google and Salesforce and all that, so it’s really exciting. Because I think it shows that this really matters to where a lot of people are doing on a large scale and small scale and that’s pretty cool.

<span class="smashing-tv-host">Drew:</span> So, if I was sort of listening to this and thinking about my own projects, thinking, "Ah, yes, design tokens are absolutely the answer to all these problems that I'm having," where would I go to find out more to start learning and start maybe using design tokens?

<span class="smashing-tv-speaker">Jina Anne:</span> It’s a really good question. There are a few articles and I can send you some links to include with this, but I think one of the first articles, which I wish I had written, but Nathan Curtis wrote and that he actually kind of helped bring attention to them. I think he inspired a lot of people to start using them, so he kind of discusses what they are and how to use them, his recommended way.

<span class="smashing-tv-speaker">Jina Anne:</span> I don’t like the title of this next article I'm going to mention, but it’s called Design Tokens for Dummies. I'm not a fan of using that terminology, but it is a pretty well thought-through article that goes to pretty much everything about them. There was a CSS Tricks article by Robin Randall recently that just explains really what they are. I did a All You Can Learn Library session for Jared Spool a while back, but it is a membership-based thing so you would have to have access to that to see it. I know there’s been a lot of presentations and stuff, but there’s not like an official book to it yet. But that’s perhaps something I'm working on. It’s like one of two books I'm working on, actually.

<span class="smashing-tv-host">Drew:</span> So, if I'm a toolmaker or I work for maybe a big organization that’s having these sorts of problems and they’ve got some ideas about maybe contributing to the process of designing how the standard works, is the design tokens community group something that I could get involved in?

<span class="smashing-tv-speaker">Jina Anne:</span> Absolutely. I think you’ll want a GitHub because that’s where all of the public discussions and notes and things are happening. Then on the W3C community group website, you can create an account there. Having that account enables you to join other community groups as well. But then, yeah, at that point once you’ve created your account there and... I think it asks if you have any affiliations, like if you work for a big company or anything like that, just so it’s transparent, like if you have any, I wouldn’t say necessarily bias, but like a certain interest. It just helps everybody understand where you’re coming from. Anyway, at that point, yeah, you join and you’re pretty much in.

<span class="smashing-tv-host">Drew:</span> It’s quite an open process then.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> What’s in the future for design tokens? What’s coming down the line?

<span class="smashing-tv-speaker">Jina Anne:</span> I'm really excited about what’s going on with the community group. Kaelig’s been doing most of the leading of it. He’s the co-chair with me and I really love seeing his passion behind this. My particular interests in this are really around the education of it. So, kind of similarly to the work I’ve been doing with the Sass community, I kind of want to do a little bit of that for the design token community, like talk through how to educate people on what this is and not just make it an API doc, but also like where to get started, how to get into this. That’s something I'm interested in project-wise.

<span class="smashing-tv-speaker">Jina Anne:</span> I'm also really keen to see where this evolves, especially with all these design tool companies getting involved. Then a lot of people mostly think about design tokens as a visual abstraction, but really what it came from was the same technology that you used for localizing content. You wrap things in strings and then you can pass through different stuff, so bringing it back to its roots. I’d love to see the application of this apply in different ways, like interactions and content. I'm not really super keen on AR/VR-type stuff, but how does it maybe manifest there? Yeah, really just seeing it kind of go beyond just like the visual layer of what we see.

<span class="smashing-tv-host">Drew:</span> I guess that’s the beauty of having an open process like the W3C community group, is that people who do have specialisms in things like AR and VR can contribute to the conversation and bring their expertise to it as well.

<span class="smashing-tv-speaker">Jina Anne:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> I’ve been learning a lot about design tokens today. What have you been learning about lately?

<span class="smashing-tv-speaker">Jina Anne:</span> I'm always trying to learn something, but I’ve actually been occasionally taking some cocktail classes. Yeah. I'm not really with the interest of becoming a bartender, but more of just having an appreciation for cocktails. What’s cool about these classes is they’re beyond just making cocktails. They actually talk about business practices and ethical practices, the hygiene of your bar, all sorts of stuff like that, so it’s been really fascinating because I think I have like this weird fantasy of one-day leaving tech and maybe going into that. Let’s see.

<span class="smashing-tv-host">Drew:</span> Do you have a favorite cocktail?

<span class="smashing-tv-speaker">Jina Anne:</span> Manhattan.

<span class="smashing-tv-host">Drew:</span> It’s good. It’s good.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> You can’t go wrong with a Manhattan.

<span class="smashing-tv-speaker">Jina Anne:</span> I have been ordering a lot of Old Fashioneds lately so that would probably be number two.

<span class="smashing-tv-host">Drew:</span> Do you have a favorite bourbon?

<span class="smashing-tv-speaker">Jina Anne:</span> Ooh. The first one that came to mind is Angel’s Envy. It’s like finished in port barrels that have kind of this slightly port-like essence to it. Their rye is really good, too. It’s like finished in rum barrels, so it almost has like a banana bread-like flavor to it.

<span class="smashing-tv-host">Drew:</span> This is a direction I wasn’t expecting to go in today.

<span class="smashing-tv-speaker">Jina Anne:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> Was there anything else you’d like to talk about design tokens?

<span class="smashing-tv-speaker">Jina Anne:</span> My take is, just like with design systems, people are going to use them in different ways and also there might be people out there that don’t even need to use this. If you just have like an editorial website that is pretty straightforward, maybe all you really need are CSS variables and that’s it. There’s no need to over-engineer things.

<span class="smashing-tv-speaker">Jina Anne:</span> This is really more for people that really need to scale or if you have a theming context then maybe. But, yeah, it’s really not meant for everyone. So, just because it’s becoming kind of a hot thing to talk about, you might not need to even bother with it.

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Jina, you can follow her on Twitter where she’s @Jina, or find her and all her projects on the web at sushiandrobots.com. Thanks for joining us today, Jina. Do you have any parting words?

<span class="smashing-tv-speaker">Jina Anne:</span> Design systems are for people.

{{< signature "dm, ra, il" >}}
