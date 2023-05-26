---
title: 'Smashing Podcast Episode 47 With Sara Soueidan: Why Does Accessibility Matter?'
slug: smashing-podcast-episode-47
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81bf4897-467c-4f52-a253-ed207834c9a1/smashing-podcast-episode-47.png
date: 2022-05-31T05:00:00.000Z
summary: >-
  In this episode of the Smashing Podcast, we ask why accessibility really matters and why it is so important to get it right. Smashing’s Vitaly Friedman talks in-depth to Sara Soueidan to find out.
description: >-
  In this episode of the Smashing Podcast, we ask why accessibility really matters and why it is so important to get it right. Smashing’s Vitaly Friedman talks in-depth to Sara Soueidan to find out.
categories:
  - Smashing Podcast
  - Accessibility
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Storyblok
  link: https://www.storyblok.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb5f98-1b75-4f2a-9e13-b5a2fbe1a71d/storyblok-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href= “https://www.storyblok.com/”>Storyblok</a>, a friendly headless CMS with a visual editor, nested components, and customizable content blocks for websites and apps. <em>Thank you!</em>
---

In this episode of the Smashing Podcast, we ask why accessibility really matters and why it is so important to get it right. Smashing’s Vitaly Friedman talks in-depth to Sara Soueidan to find out.

<iframe src="https://share.transistor.fm/e/1f94c5aa/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

### Show Notes

- Sara’s [personal website](https://www.sarasoueidan.com/)
- Sara on [Twitter](https://twitter.com/SaraSoueidan)
- [Practical Accessibility Online Course](https://practical-accessibility.today/) (coming soon)

#### Weekly Update

- “[Kubernetes For Frontend Developers](https://www.smashingmagazine.com/2022/05/kubernetes-front-end-developers/)” *written by Benjamin Ajibade*
- “[The Ultimate Free Solo Blog Setup With Ghost And Gatsby](https://www.smashingmagazine.com/2022/05/ultimate-free-solo-blog-setup-ghost-gatsby/)” *written by Greg Dickens*
- “[Lesser-Known And Underused CSS Features In 2022](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/)” *written by Adrian Bece*
- “[Understanding Weak Reference In JavaScript](https://www.smashingmagazine.com/2022/05/understanding-weak-reference-javascript/)” *written by Frank Joseph*
- “[Manage Accessible Design System Themes With CSS Color-Contrast()](https://www.smashingmagazine.com/2022/05/accessible-design-system-themes-css-color-contrast/)” *written by Daniel Yuschik*

### Transcript

<p><a href="https://twitter.com/SaraSoueidan"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0009b96-9568-4c6e-bf4f-9896906b336d/sara-soueidan-250px-opt.png" width="200" height="200" alt="Photo of Sara Soueidan" /></a> <span class="smashing-tv-host">Vitaly:</span> She’s an independent web user interface and design systems engineer, author, speaker, and trainer based in Lebanon. She worked with companies and agencies all around the world from Netflix, and Telus, and the Royal Schiphol Group at Amsterdam airport, just to name a few, where she built digital products with focus on accessibility performance and of course cutting edge tech.

<span class="smashing-tv-host">Vitaly:</span> Now, she also writes beautiful and very comprehensive, very, very comprehensive articles all around front-end SVG accessibility on her wonderful blog. And she’s also working, which might be a rumor; we’ll find out on her very own video course on web accessibility. So, in all, she’s an expert in creating accessible and beautiful interfaces.

<span class= “smashing-tv-host”>Vitaly:</span> But did you know that she loves tea, drawings, and birds and has raised more than a dozen of them throughout her life? So, I shouldn’t be surprised to hear the birds chirping when we have a call just now. My smashing friends, please welcome Sara Soueidan. Hello, Sara, how are you?

<span class="smashing-tv-speaker">Sara:</span> I am smashing. How are you?

<span class="smashing-tv-host">Vitaly:</span> That’s wonderful. I don’t know. I feel like coffee today. I had already three, and I feel like I should get forth, but you’re not big on coffee, are you?

<span class="smashing-tv-speaker">Sara:</span> No. I have my matcha sitting right next to me right now.

<span class="smashing-tv-host">Vitaly:</span> Okay. That would be a very surprising start to the conversation. But what is your favorite tea, if I may ask?

<span class="smashing-tv-speaker">Sara:</span> My favorite tea, if we’re not counting matcha as tea, even though it is actually tea, but if... okay. So, I’d say it’s either a matcha or ginger tea. I love ginger.

<span class="smashing-tv-host">Vitaly:</span> Okay. Now, dear friends, if you ever want to ship any gifts to Sara, you know what to ship. Now, staying on the topic of food and drinks, and beverages, it’s interesting, Sara, because I know we’ve known each other for, I don’t know how many years now. And we even shared pizzas on very different occasions in various parts of the world, that surely counts for something.

<span class= “smashing-tv-host”>Vitaly:</span> And one thing that really astonishes me when I think about our conversations and I think about you as a personality and just the incredible work that you put on the web, it’s just incredibly difficult for me to find many people who are more passionate about accessibility as you are.

<span class= “smashing-tv-host”>Vitaly:</span> So, maybe you could give us a bit of a background of where this genuine empathy and excitement about accessibility comes from. Where did it all start, Sara? Where?

<span class="smashing-tv-speaker">Sara:</span> Do you want the long version answer or the short version answer?

<span class="smashing-tv-host">Vitaly:</span> The very long answer, if I can.

<span class="smashing-tv-speaker">Sara:</span> Are you sure?

<span class="smashing-tv-host">Vitaly:</span> No.

<span class="smashing-tv-speaker">Sara:</span> Yes.

<span class="smashing-tv-host">Vitaly:</span> Okay. But make a choice, whatever works for you works for me.

<span class="smashing-tv-speaker">Sara:</span> Okay. So, if you want some background, I’ve always been the kind of person who loves helping people, even if they don’t directly ask for it. So, I’m just going to give you a quick example. Back when I was in college, I think it was my second year in college or in university, and it was the start of the year, and everyone was in the university, and we were registering and doing all the necessary paperwork that we needed to do to start going to class.

<span class="smashing-tv-speaker">Sara:</span> And there were a lot of people, basically. And there was this one old man, he was standing in the middle of the crowd, and he was carrying a few papers in his hand and a pen. And he looked absolutely clueless. I could tell from his facial expressions that he was lost. He had no idea what he was supposed to do.

<span class="smashing-tv-speaker">Sara:</span> So, I approached him and I asked him... I always do this, by the way. I’m not sure if this is a good thing or a bad thing, but I tend to do this with strangers a lot. So, I said, “Is there anything I can help you with?” He looked at me, and he said, “I have no idea basically how to fill the paperwork in.”

<span class="smashing-tv-speaker">Sara:</span> He was there to register his son, who couldn’t be there. So, he was registering him instead, and he didn’t know how to do it. And I know how difficult it can be the first time. Because my first time, when I went to college for the first time, in the first year, it took me four days to register because there was no one there to help you.

<span class= “smashing-tv-speaker”>Sara:</span> You can either find your way on your own, or you would just have to ask people. And if you don’t ask anyone, you’re just kind of stand there like that old man did. So, I asked him if I could help him, and he welcomed my help. I took the paperwork. I took the pen. I started asking him questions and filling in the paperwork for him.

<span class= “smashing-tv-speaker”>Sara:</span> And then, when I finished, I told him exactly where to go next, exactly what to do. And I basically just helped him as much as I could. I do this with a lot of people. I don’t know; I think it’s just part of who I am. Helping people makes me feel amazing.

<span class= “smashing-tv-speaker”>Sara:</span> Even the smallest acts of anything that you do in your daily life makes them meaningful and gives them purpose. So, to know that I have contributed a positive thing, no matter how small, into someone else’s life is wonderful. And I want my work to have a purpose, as well.

<span class= “smashing-tv-speaker”>Sara:</span> So, when I started my career as a developer, I think it was in 2013, and this is something that I’m sharing for the first time, I went through a few years where I felt like what I was doing wasn’t very meaningful, to be honest. So, I was just doing what I was doing just to make some money, make a living, and that was it.

<span class= “smashing-tv-speaker”>Sara:</span> But I would get designs someone made and turn them into something that worked, which is nice because I love doing that. But as always, I kept asking myself for years like, “What good is this contributing to the world?” I wanted to feel like the code that I’m writing can make a difference. And it took some time for me to finally get there.

<span class= “smashing-tv-speaker”>Sara:</span> So, I started changing my path, so to speak, by choosing the clients that I wanted to work with. I started choosing clients that did meaningful things in the world. That way, if I help them create a website to expand the reach, it meant that I was contributing to something good in this world, as well.

<span class= “smashing-tv-speaker”>Sara:</span> And I even expressed that on my Hire Me page, where I’m explicitly clear that I’m looking to do something meaningful in the world. So, there is that. And on the other hand, I’ve always been fascinated with design, in general. I’ve never taken a design class in my life, not in university, not outside of university, but I’ve always been interested in design because of how it directly impacted people’s lives.

<span class="smashing-tv-speaker">Sara:</span> You can maybe start to see connection here. So, I’m going to give an example from the adjacent design field. Many people who have been following me for years know that I’m fascinated and very passionate towards interior design. And the best thing I’ve ever read about interior design is that interiors should be designed around how we live.

<span class="smashing-tv-speaker">Sara:</span> So, how do you decide what you put in the kitchen, for example? How do you decide how much space you give a certain feature or piece of furniture in the house? The answer is based on how often it is needed by the people who will live in this house.

<span class= “smashing-tv-speaker”>Sara:</span> A great interior designer will sit down with their client and ask them questions like, “How do you start your day? What does your typical day look like? What do you do when you wake up in the morning? Do you work from home? Do you like having people over? Do you like entertaining? What are your hobbies?”

<span class= “smashing-tv-speaker”>Sara:</span> And the answers to all these questions they asked creates the framework and guides the interior design decisions of the house that the client will live in. The house is designed and built around the client’s lives, not the other way around.

<span class="smashing-tv-speaker">Sara:</span> And I love that because if design isn’t about people, then it is selfish, right? Then, you’re not really designing for people anymore. And accessibility and inclusive design in general, but accessibility is not the same as inclusive design. Accessibility design is all about people.

<span class="smashing-tv-speaker">Sara:</span> There is no room for selfishness, in my opinion. So, what you design and build either works for the user or it doesn’t. And if it doesn’t, then it needs to change because what good is anything that you built for people if they can’t use it?

<span class= “smashing-tv-speaker”>Sara:</span> So, connecting these two things, I love design, and I love designing for people, and I love helping people. So, when I first learned about accessibility, and I found out that some of the work that I was building prior to that was possibly creating barriers to access for people.

<span class="smashing-tv-speaker">Sara:</span> I felt horrible. And I started feeling more responsibility, and I started digging more into accessibility and learning more about it. And what I love the most about it is it makes me feel more like a designer. Why? Because, well, I do believe that all of us, we are designers, one way or another.

<span class= “smashing-tv-speaker”>Sara:</span> And the work that we do and the decisions that I make as a design engineer when I write code, these decisions have a direct impact on the user experience, and that makes me a designer. So, every decision that I make has a direct impact on the experience and the inclusivity and accessibility of the interfaces I built.

<span class= “smashing-tv-speaker”>Sara:</span> A decision such as, for example, what HDML element I choose to use, how do I apply the styles because CSS affects semantics, which affect accessibility, which development strategy I follow, which is a progressive enhancement or something else. Whether I use platform features or a third-party library, which library do I choose?

<span class="smashing-tv-speaker">Sara:</span> How does it perform? All of these things, they impact your work, and eventually, the user experience. And design should be about people. Accessibility is about people, which means that it gives code purpose. It gives the work that I do purpose, which brings me back... the first thing that I mentioned, I want to feel like what I’m doing has a purpose and is actually beneficial for people.

<span class= “smashing-tv-speaker”>Sara:</span> And this is why I love accessibility, in general, because it is a concrete, practical type of design, something either works or it doesn’t. And there is no room for bad decisions because it’s about the user, not about you. So yeah, I’m passionate about accessibility because-

<span class="smashing-tv-host">Vitaly:</span> I could tell. Yeah, that’s incredible to hear. And actually, a few things that have really connected the dots for me, as well, because when I think about the work that I’m doing, as well, I feel like... we don’t even notice that sometimes, but all these minor decisions about the labeling of navigation and the way we design navigation, and the way we make buttons to look like buttons.

<span class="smashing-tv-host">Vitaly:</span> All those things can have tremendous impact. We might feel like, “Okay, we’re just moving pixels around.” And we’re just making things a little bit more nice, right? But I think that the right significant decisions that we end up, that we use to really help somebody in different situations, complete the task, to find information that they need, and so on.

<span class= “smashing-tv-host”>Vitaly:</span> And one thing that really comes up in my mind every time we have this conversation is that you often identify yourself with a design engineering role. And I see that some teams are moving towards that role now. Where in the past, it was just a developer, and then it was just a designer, and then it was a front-end developer and backend developer.

<span class="smashing-tv-host">Vitaly:</span> And if you have an interface designer, you have to use the experience designer. So, maybe you could share a little bit of light on how you see design engineering as a role. And maybe many of our listeners now actually are design engineers without even knowing that. So, how would you define it? And do you think that companies actually understand what it means?

<span class= “smashing-tv-speaker”>Sara:</span> I have actually an essay, not just an article, an essay that is all about just defining the role of a design engineer. And from my point of view, I even have a domain name that I purchased just to put that on it. If I try to describe it with just a few words because I already gave a super long answer to the previous question-

<span class="smashing-tv-host">Vitaly:</span> That was a wonderful answer. It wasn’t long at all.

<span class="smashing-tv-speaker">Sara:</span> Thank you. Okay. So, as design engineers, we specialize in implementing designs. That is the general description, right? We specialize in implementing designs, but then, of course, there is how you implement it. So, I like to label myself as an inclusive design engineer, which is something that I’m doing on my new website, which is not public yet.

<span class= “smashing-tv-speaker”>Sara:</span> So, an inclusive design engineer is someone who, in my opinion, uses accessibility and progressive enhancement as a framework to build inclusive interfaces. But, as a design engineer, in general, is someone who works directly with designers, hopefully, because this is what I think the role should be.

<span class= “smashing-tv-speaker”>Sara:</span> We should be working directly with designers, helping them make decisions and informing design decisions with our accessibility and code knowledge, basically, because they complement each other. We write HDML. We write CSS. We write presentational JavaScript, mostly.

<span class="smashing-tv-speaker">Sara:</span> And with a strong focus on accessibility, hopefully, because that should be part of every design engineer’s job. And then, of course, the strategy that you choose and the frameworks that you use, and I’m not talking about CSS frameworks or JavaScript frameworks here, but like I said, this... let me just call it the strategy.

<span class= “smashing-tv-speaker”>Sara:</span> Strategies that you use and what exactly you focus on, and how you do your job as a design engineer probably differs between people because like I said, I’m a progressive enhancement advocate, others are maybe not. So, we would differ in these small details.

<span class= “smashing-tv-speaker”>Sara:</span> But a design engineer is someone who works with designers, helps inform design decisions and makes sure that designs are implemented in a way that hopefully works for as many users as possible.

<span class="smashing-tv-host">Vitaly:</span> Right. So then, as a design engineer, at this point, how would you then actually work? So, what would your process be like? So, when you think about implementing a particular design, do you break it down into components? Do you think about navigation landmarks first?

<span class="smashing-tv-host">Vitaly:</span> How do you actually start building things? What is your maybe mindset in that framework of getting accessible results? Maybe you could describe it a little bit.

<span class="smashing-tv-speaker">Sara:</span> Okay. So, when you say that you divide the... you not divide, basically looked at the design and then start thinking in components, that very much depends on the process that you work with the designer. So, if I’m working with someone who has handed over a design, like an entire page, the process is different from when I’m working with the designer, like I did with Yan Persy.

<span class= “smashing-tv-speaker”>Sara:</span> I’ve mentioned him multiple times on Smashing Hour, by the way, because working with him was one of my favorite ways of working with the designers because he didn’t have like a full finished design for me to implement. We worked in tandem. We worked together. And he changed some of the things in the design.

<span class="smashing-tv-speaker">Sara:</span> So, for example, he wasn’t using a responsive type scale like we do in front-end development now using CSS variables and viewport units, et cetera. So, we had this discussion, and then he shifted the way the design process went. It was different.

<span class= “smashing-tv-speaker”>Sara:</span> So, we both started building the site in terms of components, and then assembling those components into what we called slices back then, and then assembling the slices into the entire website. So, how I start from whether it’s components or not, depends on the process that I work with the designer.

<span class= “smashing-tv-speaker”>Sara:</span> But then, if I get a little bit more technical, like if I have a component that I want to build, how do I go about doing that in layers, I would say? Again, progressive enhancement, the first thing that I think about is how does this work? How does this look like?

<span class="smashing-tv-speaker">Sara:</span> How does someone perceive this if JavaScript is disabled? And what happens if there is no style? So, I just start with the bare minimum, HTML, because HTML defines the semantics. The semantics give meaning to the content that I’m creating.

<span class="smashing-tv-speaker">Sara:</span> So, which HTML elements do I need to tell the user what this thing is to give semantics? If HDML already contains an element that represents this component or this element that I’m building, I use that. If not, then I start to thinking about ARIA attributes; which ARIA attributes do I need?

<span class="smashing-tv-speaker">Sara:</span> How much ARIA do I need? ARIA is... it’s not an enhancement; it’s necessary for a lot of dynamic and interactive components. But I always try to think of it as a last resort, not a first one, so always semantic HTML first. How much can I get done with just semantic HTML?

<span class="smashing-tv-speaker">Sara:</span> How accessible is it? Do I need something? Do I need to polyfill some semantics using ARIA? If I do, then I start thinking about that. And then applying CSS, and how does CSS affect these semantics? Does it? Does it not?

<span class= “smashing-tv-speaker”>Sara:</span> Do I have to do something extra to make sure that something remains accessible after I style it? Like, for example, if you stripped away the default list styles on list elements, which is something you probably... and many people probably already know by now, if you set list style to none, for example, on an unordered list, then Safari or WebKit, WebKit, in general, is going to remove the semantics of the list.

<span class="smashing-tv-speaker">Sara:</span> And VoiceOver is not going to announce that anymore. So, what do I do in that case? Do I need those semantics? Do I go into the HTML and add them again using a role attribute or not? So, I think about this stuff in layers. Start with HTML semantics. Do I need ARIA? How do I style this? And then, interactivity is always the last layer that I think about and that I build into components.

<span class="smashing-tv-host">Vitaly:</span> Right. Makes sense. It’s interesting what you’re saying that it’s a process. It doesn’t seem like a simple process, especially when you think about like literally implementing quite a complex interface, which may also have all kinds of different views and maybe single page application in the back and so on.

<span class= “smashing-tv-host”>Vitaly:</span> And one thing that I’m struggling with when I’m doing work with clients and trying to make things more inclusive and interfaces maybe a bit more usable is that very often web accessibility is still seen as this little thing. Like, “Okay, that’s just semantics.” “Okay, so we’re going to use buttons for buttons.”

<span class="smashing-tv-host">Vitaly:</span> But it’s actually much, much, much more than that. And I’m wondering, what do you think... like, where do we actually stand in terms of accessibility today? It’s very hard for me, personally, for example, to imagine a new project being released without even considering accessibility.

<span class="smashing-tv-host">Vitaly:</span> I think that might have been possible maybe a decade ago. I think today, it would be very difficult to imagine a brand new project that’s going to be advertised everywhere on posters that is not accessible at all, some parts accessible, but maybe not everything.

<span class= “smashing-tv-host”>Vitaly:</span> So, what do you think, has accessibility not become just the natural part of every design implementation process, or are we way, way, way, far away from this yet?

<span class="smashing-tv-speaker">Sara:</span> I think we are not too far, but we’re still far. So, there is definitely a lot more awareness on accessibility. I hope so, at least, because I only follow like less than 250 people on Twitter. And most of the people in my circle are people who either work with accessibility or care about accessibility.

<span class= “smashing-tv-speaker”>Sara:</span> So, if I were to judge the current situation based on my little circle, I would say that accessibility is doing great, and people care about it a lot. And they work to make their content more accessible. But I can’t speak for everyone because I know that this isn’t the case for everyone.

<span class="smashing-tv-speaker">Sara:</span> I know that there are still many developers who just simply don’t care. Because with accessibility, you either care or you don’t care; this is it. If you don’t care, then you are basically not doing any accessibility work at all.

<span class= “smashing-tv-speaker”>Sara:</span> And then, on the other hand, those that do care about accessibility and try to implement it in their work, some of them are finding difficulty because they get lost in all of the resources out there, and where should they go? Where do they start? This is why I’m creating the accessibility course now, to hopefully help with that a little bit.

<span class= “smashing-tv-speaker”>Sara:</span> So, we are definitely doing much better than we did like five years ago, let me say, five. But I don’t think we’re just exactly there yet. No. I think it’s going to take more time.

<span class="smashing-tv-host">Vitaly:</span> Yeah. But then, I also hear developers telling me all the time, “Well, hold on. But the platform is evolving so beautifully at this point. We have not only the wonderful CSS feature coming along, but also we have these incredible things that common UI components, like input type date for a date picker, the dialogue for models, details, and summary for accordions.”

<span class= “smashing-tv-host”>Vitaly:</span> And very often, what I find is that they just use those things, and they think that, “Okay, well, since these are native components available on the platform, they surely are accessible.” And then, come eye along, and then there is trouble. I’m wondering, at this point, what would you say in this position?

<span class="smashing-tv-host">Vitaly:</span> Like, those things, would you recommend to use them ever? Or where are there? Ideally, it would be a very nice idea and situation where we ended up with all those native components just available out of the box, beautiful, accessible, inclusive, and all of that. Are we there yet?

<span class="smashing-tv-speaker">Sara:</span> No.

<span class="smashing-tv-host">Vitaly:</span> Are we again, far away from it?

<span class="smashing-tv-speaker">Sara:</span> No. No. We’re definitely not there yet. I know that the dialogue element, for example, has been pretty... I don’t want to say completely inaccessible, but it has had a lot of accessibility issues for years now. And I think it only started getting better this year. And then, input type equal date, I rarely ever used it because, to be honest, I don’t think that it offers the best usability anyway, even if it is accessible, which I think it’s... I don’t know.

<span class="smashing-tv-speaker">Sara:</span> I haven’t used it in a very long time, so I can’t even tell if it’s fully accessible or not. But I think the last I heard was that it wasn’t and that it was a usability nightmare. So, even if something is technically accessible, that doesn’t mean that it’s going to be usable. Definitely a lot of tests.

<span class= “smashing-tv-speaker”>Sara:</span> And I like this quote by my friend, Scott O’Hara, that he said in one of his talks. He said, “Technology and user expectations change rapidly. And we should always test to ensure not only emerging patterns work correctly but try untrue patterns continue to work as we expect.”

<span class="smashing-tv-speaker">Sara:</span> This is me, now, continuing. Sometimes even something that you know works may stop working as you expect. Browsers may create new heuristics, for example. And the way they... not interpret, the way they present something because the user may change on any day.

<span class= “smashing-tv-speaker”>Sara:</span> Also, a note about details and summary, which is something that I had a discussion about today, details and summary are not the best choice for an accordion. They can be used for an accordion, but even they... like, when you choose any component, the first thing you have to think about is the semantics.

<span class="smashing-tv-speaker">Sara:</span> What are the semantics that are going to be conveyed? Because the semantics determine the non-visual interface for a non-sighted user, for a screen reader, for a user, for example, assuming they’re a non-sighted screen reader, the user.

<span class="smashing-tv-speaker">Sara:</span> Details in summary, they have their own quirks when it comes to semantics. So, the summary has a button roll, which means that it is conveyed as a button to assistive technologies. And buttons eat up the semantics of the elements inside of them.

<span class= “smashing-tv-speaker”>Sara:</span> So, if you have a heading, which is what you would normally have in an accordion, and if you put that inside of a summary, then the heading is not going to be conveyed as a heading anymore. Of course, there are exceptions because sometimes browsers try to quote, fix our misuse of ARIA or our misuse of semantics.

<span class= “smashing-tv-speaker”>Sara:</span> And they try to help stream users by conveying things that we may have broken as developers, but it doesn’t mean that all browsers do that. So, definitely, always, you need to test. And if details in summary, for example, if you use that, and if the headings are not exposed as headings, and then the user cannot use those headings to navigate, for example, anymore.

<span class="smashing-tv-speaker">Sara:</span> So, even if something is technically accessible, yes, they can access the contents of summary. Yes, they can access the contents of the details. But you have to think about what semantics you are conveying and how they affect the usability of the interface and sometimes maybe navigation, so there are a lot of things to keep in mind.

<span class="smashing-tv-host">Vitaly:</span> Yeah. So, it’s interesting that you brought up the testing for accessibility at this point. Because when we run our workshops, and every now and then, we... in my workshop, I tend to just explain to people how security works. And I always ask the same question. And for the last, I don’t know, two, three, four years, maybe now, I’ve been asking the same question.

<span class="smashing-tv-host">Vitaly:</span> So, who is hearing this VoiceOver for the very first time? And these are usually designers or developers coming to those workshops. And very often, you would see a vast majority of people hearing things for the very first time. So, maybe you could also share a bit of light in how do you actually test accessibility?

<span class="smashing-tv-host">Vitaly:</span> Do you always have screen reader or VoiceOver on or maybe any other tools? Could you also, maybe, run us through the process of testing your components for accessibility?

<span class="smashing-tv-speaker">Sara:</span> Okay. So, there are quite a few things that I like to use, and I’m going to mention them in no particular order; definitely browser DevTools to inspect the accessibility tree because you can get a lot of insight on the accessibility of the elements and components that you’re building from the accessibility tree.

<span class= “smashing-tv-speaker”>Sara:</span> Because basically, the accessibility tree is the accessibility... contains the accessibility information that the browser has created for assistive technologies to announce. So, when you look at the accessibility tree, you can get an idea of how an element is going to be announced by a screen reader that accesses and gets that information from the browser via the accessibility API, of course.

<span class="smashing-tv-speaker">Sara:</span> So, the dev tools for accessibility tree. There are a lot of extensions that I like to use, for example, to see the document outline on a page or to see the landmarks on a page. If I’m doing an accessibility audit, I would definitely use an automated testing tool such as asking DevTools, for example.

<span class="smashing-tv-speaker">Sara:</span> As far as screen reader go, definitely like... you cannot just test on one screen reader. And I have been guilty of this. I mean, I’m not like preaching something that I don’t practice now, but I know that I didn’t practice this before. I don’t have access to a windows machine.

<span class= “smashing-tv-speaker”>Sara:</span> So, I recently... not recently, like a few months ago, I started using Nvidia A on my windows virtual machine. And I also recently got a license for JAWS because JAWS is not free, but Nvidia is free. So, I used VoiceOver with Safari on iOS. Sometimes I test on other browsers, as well, just because sometimes, maybe a VoiceOver using may be using another browser.

<span class="smashing-tv-speaker">Sara:</span> But generally speaking, VoiceOver and Safari are the best combination, and users typically know that. And on windows, I test Nvidia A with Firefox, Nvidia A with Chrome. And the narrator is also built into Windows, so I use that for testing as well.

<span class="smashing-tv-speaker">Sara:</span> And JAWS is the most popular screen meter according to the WebAIM screen reader, user survey. So yes, you have to test using multiple screen readers and browser combinations because just like you cannot test your website only on one browser.

<span class= “smashing-tv-speaker”>Sara:</span> Like say, you’ve built a website, and you want to test, if everything is working as expected, all your CSS and stuff, you don’t just test it on one browser, right? You test it on most modern browsers and possibly even on IE if you still have to support that. Just like you test on multiple browsers, you also have to test on multiple screen readers, if you can. So, this is what I do, in general.

<span class="smashing-tv-host">Vitaly:</span> Yeah. So, you also mentioned in one of the Smashing Hours that tool.

<span class="smashing-tv-speaker">Sara:</span> Assistive labs.

<span class="smashing-tv-host">Vitaly:</span> Assistive labs, which is like browsers tech for screen readers, which is really need to see, as well. And I think, for me, it’s really this really interesting world of other browsers, I would say because we tend to focus a lot on what are some of the fancy new features we get in Firefox and in Chrome, and in Safari.

<span class= “smashing-tv-host”>Vitaly:</span> Just in general, would you say that the development of screen readers is... the frequency of updates, is it similar or is it something like maybe there is a new version coming up every six months or only just once a year, because we have this comparability, right, stuff happening across browsers.

<span class= “smashing-tv-host”>Vitaly:</span> So, as much as it used to where you’re using Firefox or Chrome, or Safari, or Edge, at this point, do you see that it’s also moving in the world of screen readers towards this comparability mode... not mode, compatibility across different screens readers? Or is it... maybe you could share just a bit of light about that world and that universe of screen readers?

<span class="smashing-tv-speaker">Sara:</span> To be honest, I’ve never dug that deep into it. So, I haven’t been monitoring, for example, screen reader updates, like how often Nvidia is updated and how often JAWS is updated. But I do know that even if JAWS or Nvidia is updated, not all screen reader users are going to update their software because they’re aware of... a lot of things may break for them.

<span class= “smashing-tv-speaker”>Sara:</span> And if they already have an environment that works, nobody wants to break something that works for them. So, I know that many screen reader users do not update their software as often as we may think that they do.

<span class="smashing-tv-host">Vitaly:</span> Right. Well, of course, talking about browsers, at this point, I do have to bring out the wonderful notion of wonderful CSS. And obviously, I do have some questions about CSS, as well. And one thing that I definitely have to ask, and I know what your answer is going to be, but I still like hearing it every single time.

<span class="smashing-tv-host">Vitaly:</span> So, I am going to bring this up. I have a feeling... well, I know that you have or maybe don’t have strong feelings about CSS methodologies or frameworks, or JavaScript frameworks for that matter. Do you have any favorites, or do you not? Do you always just work with what the project requires?

<span class="smashing-tv-host">Vitaly:</span> How do you pick your battles? Would you ever use any framework or CSS framework library Tailwind, CSS and JS; I don’t know. I mean, a short, no would suffice.

<span class="smashing-tv-speaker">Sara:</span> I can’t just say no, because it depends on the project. If I’m working with a team and everyone on the team is using Tailwind, then I will definitely be using Tailwind with them. But I’ve never had to do that yet. And I’ve been super lucky with... actually, I would even say privileged with the projects that I’ve worked on so far.

<span class="smashing-tv-speaker">Sara:</span> So, no, I don’t use any CSS frameworks. I prefer not to use them because they come with a lot of... and I’m not, not talking specifically about any particular framework here. Most of them come with a lot of overhead. And for me personally, I feel that trying to remove all the unnecessary CSS or learn something or learn it from... it’s just so much faster for me to build something from scratch, literary.

<span class= “smashing-tv-speaker”>Sara:</span> Like, I have some CSS that I’ve created over the years that I moved from one project to the other, and of course, I constantly update that, and I used that. It’s like a mini, tiny framework that I used. Like, there are some utility classes that I used in there.

<span class= “smashing-tv-speaker”>Sara:</span> Some settings, I called them these settings files for setting up the type scale and the tokens for theming and all that stuff. But I would definitely rather not use a CSS framework. I don’t have super strong feelings about them. I personally used a combination of BEM ITCSS and utility classes in my work.

<span class="smashing-tv-speaker">Sara:</span> And I only add as much CSS as I need. So, if I need a utility class, I add it to the utility class list that I have. If not, I don’t just add it just in case I’m going to need it. I’m super minimal when it comes to writing CSS.

<span class="smashing-tv-host">Vitaly:</span> Right. Sorry, can you hear the voices of the wonderful people on the remote corners of the internet asking for that little framework that you have created to be open source, maybe?

<span class="smashing-tv-speaker">Sara:</span> I will. I do plan on doing that. Yes. The course has taken up most of my time. My website has been neglected. My blog has literally been abandoned for months, and I’m going to do... like, even the website that I’m using, I built the course website from scratch using 11T.

<span class="smashing-tv-speaker">Sara:</span> I’m even considering sharing that as a framework, if anyone wants to use it someday. So, a lot of stuff that I have on my to-do list, but I’m postponing all of it until after the course is released because I need to get this done.

<span class="smashing-tv-host">Vitaly:</span> Right. So, maybe let’s just jump into the course. I think that we’ve been speaking about it a couple of times already, but I could not be more excited to actually get this course finally released. Well, do you think you could actually share a bit of insight about what’s going to be about, when it’s going to be released, and where wonderful people listening to this show can subscribe to updates to actually get it when it does get released?

<span class="smashing-tv-speaker">Sara:</span> Okay. Updates, subscription, e-mail, newsletter on practical-accessibility.today, that is the website for where the course is going to be hosted currently. It just includes an overview of what the course is about and a link to subscribe to the newsletter.

<span class= “smashing-tv-speaker”>Sara:</span> But hopefully next month, when the backend is finally ready... because we’re doing everything from scratch, and I hired a friend of mine to build the backend and all the payment stuff into it. Once that is finished, the website is going to be updated with more details about the course. So, I’m going to introduce the course in a short video.

<span class="smashing-tv-speaker">Sara:</span> There’s going to be a more detailed table of contents. I haven’t shared a table of contents yet because it keeps changing a lot. Like, even yesterday I added a new section or a new chapter in between two other chapters. So, if I had shared the table of contents before, it wouldn’t have been super accurate.

<span class="smashing-tv-speaker">Sara:</span> So hopefully, in a month... I think during the next Smashing Hour, I’m going to be making an important update on the course.

<span class="smashing-tv-host">Vitaly:</span> Oh, that’s cool. That’s nice. That’s nice. Can I ask you just on that point? I find it so difficult to record videos. I always see like, “Oh, no, no, no. I shouldn’t have said that.” I should brief rewind back, and then I should re-edit and then I should change.

<span class= “smashing-tv-host”>Vitaly:</span> And then, I keep going all the time, and it takes me, I don’t know, hours to just record 10 or 15 minutes of stuff. Is it the same for you? Or do you just go?

<span class="smashing-tv-speaker">Sara:</span> I’m already worried about this because I haven’t recorded anything final yet. I’ve only done a few, so like some testing and editing stuff. I’m starting with a course in reverse, actually. I’m not recording first. I’m going to give more details about the process and everything later, once it’s finished.

<span class= “smashing-tv-speaker”>Sara:</span> But I’ve decided to do things in a different way so that when it’s time to do the recordings and the editings, I hope will hopefully have eased things for myself, so that they don’t take as much time. And something that I need to keep reminding myself of is because I’m a perfectionist, and that sometimes is a bad thing.

<span class= “smashing-tv-speaker”>Sara:</span> I’m just going to assume that I’m on stage in a conference and just like, I can’t edit every single word I say on stage. I’m going to try to just ignore some things in the videos. That’s going to be super difficult, especially because I know that I can edit them, but it’s definitely going to take some self-discipline to do that.

<span class="smashing-tv-host">Vitaly:</span> Yeah. So, it’s impossible for me. I always say like, “Oh, no, no, no, of course, I can go back,” and surely I can come back. So, in the end, it just takes hours. But I think that we all cannot wait for the video course to be finally released and get our hands on the videos.

<span class="smashing-tv-host">Vitaly:</span> This is very, very exciting. Maybe talking about excitement, I know that there are so many wonderful new features coming to the web. I don’t know when it’s coming. Is it like Chrome 103 something, where we should be expecting the :has() pseudo-class coming in, container queries coming in? It’s like Christmas is coming early.

<span class="smashing-tv-speaker">Sara:</span> The year of CSS.

<span class="smashing-tv-host">Vitaly:</span> Yeah, the year of CSS. So, maybe you could just share a bit of light about what are you excited about at this point? What is the thing that keeps you awake at night where you think, “Oh, if it only was available today, I would use it all over in my projects.” What would that be? Or what are you most excited about these days in CSS?

<span class="smashing-tv-speaker">Sara:</span> Well, CSS doesn’t keep me up at night, but I do look forward to things like definitely subgrid. I know that I was one of the people who started requesting container queries years ago, and then we finally got them. But then, at this point, we were already doing a lot of intrinsic responsive design already and using flexbox and CSS grid to create responsive components that don’t require container queries anymore.

<span class= “smashing-tv-speaker”>Sara:</span> Although, I mean, they are still important, and I will definitely still be using them. But probably what I’m personally more excited about is cascade layers and subgrid because almost every single project that I’ve used, especially since I worked on the Prismic Slices Project in 2019, that project changed the way I started building websites, at least for me.

<span class="smashing-tv-speaker">Sara:</span> It influenced the work that we did on the ?? website with Yan. And it also influences now, my own work on my website, for example. Instead of thinking of either pages or small components, there is this middle ground, which is slices.

<span class= “smashing-tv-speaker”>Sara:</span> And layout within slices always... like I’ve always wanted the ability to inherit the grit on the parent container of the parent container into the child. And so, subgrid is going to be one of the things that I will probably need even more than container queries in my work.

<span class= “smashing-tv-speaker”>Sara:</span> Cascade layers, I wouldn’t say that I need it, but the way it allows me to organize my CSS, the same way the CSS is organized inside of my head, so to speak, that is one of the reasons why I’m excited about it as well.

<span class="smashing-tv-host">Vitaly:</span> Okay. And then, maybe just a few final questions to finally wrap up, just because I’m very, very curious, so I’m sure you have a couple of books lying around at this point; how do you organize your books? Are they organized by topic? Are they organized by color? I met some people doing that. How do you organize them?

<span class="smashing-tv-speaker">Sara:</span> By color, but not like the rainbow style color that other people do.

<span class="smashing-tv-host">Vitaly:</span> Okay. How many pencils or pens do you have on your table most of the time?

<span class="smashing-tv-speaker">Sara:</span> Probably two, like one or two.

<span class="smashing-tv-host">Vitaly:</span> And how many screens?

<span class="smashing-tv-speaker">Sara:</span> You mean for work?

<span class="smashing-tv-host">Vitaly:</span> Yes.

<span class="smashing-tv-speaker">Sara:</span> Right now, just two, the laptop and an external display, 32-inch.

<span class="smashing-tv-host">Vitaly:</span> Okay. Because for me, moving to a secondary display was really a deal-breaker, so it’s just incredible. And then finally, one thing that I do want to ask, and it’s totally unrelated, is, do you happen to have a printer?

<span class="smashing-tv-speaker">Sara:</span> No, I haven’t had one in more than two decades, I think.

<span class="smashing-tv-host">Vitaly:</span> Yeah. Now, I feel just lonely because every time I bring this up, because I just got a printer, like what, two months ago. And I’m very proud of this because this is like me having a printer like the first time in two decades, seems like I’m the only person who’s buying printers at this point. That makes me very, very sad.

<span class= “smashing-tv-speaker”>Sara:</span> I mean, you’ve lived in Germany, right, and you still do a lot of printed paperwork there, so you need it.

<span class="smashing-tv-host">Vitaly:</span> Yes, indeed. You’re absolutely right. Well, okay, now we know that. All right. So, we’ve been learning a little bit about what it means to design and create more accessible interfaces today; what have you been learning about lately, Sara? Maybe one interesting insight or one unusual thing that you’ve learned recently, which really changed your views, maybe it’s just something that somebody said to you, which has influenced your work or just the way you’re thinking about design or about development, anything in that department?

<span class="smashing-tv-speaker">Sara:</span> Nothing that big, but a lot of small detail.

<span class="smashing-tv-host">Vitaly:</span> Like what?

<span class="smashing-tv-speaker">Sara:</span> There is super technical thing.

<span class="smashing-tv-host">Vitaly:</span> Okay. So, when it comes to implementation of accessible components, and things like that.

<span class="smashing-tv-speaker">Sara:</span> Yeah. There are a lot of things that I learned from digging really deep into specifications. And I love that because my go-to resource to learn about almost anything starting with CSS and other things, is to go to the specifications first. And there’s so much I’ve learned from that recently.

<span class="smashing-tv-host">Vitaly:</span> All right. Excellent. Well, so, if you, dear listener, would like to hear more from Sara, you can follow her on Twitter, which is @SaraSoueidan. And also, find all her work on her website at [sarasoueidan.com/](https://www.sarasoueidan.com/).

<span class="smashing-tv-host">Vitaly:</span> And also, don’t forget to subscribe to [practical-accessibility.today](https://practical-accessibility.today/), which as we’ve heard today will be released soon. So, this is something I’m very, very much looking forward to.

<span class="smashing-tv-speaker">Sara:</span> In the summer, hopefully. That’s what I’m aiming for.

<span class="smashing-tv-host">Vitaly:</span> Well, that’s fantastic news one way or the other. Well, thanks so much for joining us today, Sara. Do we have any parts in words?

<span class="smashing-tv-speaker">Sara:</span> Thank you for having me. Today is Global Accessibility Awareness Day. So, if there is something or one thing that you can do today, I would say go either learn something new about accessibility. Or, if you already have the knowledge, fix something on your own website or on somebody else’s website, like open a PR, or fix an issue that exists somewhere out there. Spread the word on accessibility, and subscribe to my newsletter.

{{< signature "il" >}}
