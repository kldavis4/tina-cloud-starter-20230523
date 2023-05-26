---
title: 'Smashing Podcast Episode 50 With Marko Dugonjic: Can You Change A UX Dinosaur?'
slug: smashing-podcast-episode-50
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe39337d-f1ba-40b2-adf2-ab97b12257a6/smashing-podcast-episode-50.png
date: 2022-08-09T08:00:00.000Z
summary: >-
  In this episode, we ask how you can affect change to UX design in large organizations stuck in their ways. Vitaly talks to Marko Dugonjić to find out.
description: >-
  In this episode, we ask how you can affect change to UX design in large organizations stuck in their ways. Vitaly talks to Marko Dugonjić to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Storyblok
  link: https://www.storyblok.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50cb5f98-1b75-4f2a-9e13-b5a2fbe1a71d/storyblok-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.storyblok.com/">Storyblok</a>, a friendly headless CMS with a visual editor, nested components, and customizable content blocks for websites and apps. <em>Thank you!</em>
---

In this episode, we ask how you can affect change to UX design in large organizations stuck in their ways. Vitaly talks to Marko Dugonjić to find out.

<iframe src="https://share.transistor.fm/e/14ab24b3/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

### Show Notes

- Marko [on Twitter](https://twitter.com/markodugonjic)
- [TypeTester](https://www.typetester.org)

#### Weekly Update

- [Article vs. Section : How To Choose The Right One](https://www.smashingmagazine.com/2022/07/article-section-elements-accessibility/) *written by Olushuyi Olutimilehin*
- [Testable Frontend: The Good, The Bad And The Flaky](https://www.smashingmagazine.com/2022/07/testable-frontend-architecture/) *written by Noam Rosenthal*
- [Fluid Sizing Instead Of Multiple Media Queries?](https://www.smashingmagazine.com/2022/08/fluid-sizing-multiple-media-queries/) *written by Ruslan Yevych*
- [Migration From jQuery to Next.js: A Guide](https://www.smashingmagazine.com/2022/08/migration-jquery-next-js-guide/) *written by Sam Robbins*
- [Rethinking Authentication UX](https://www.smashingmagazine.com/2022/08/authentication-ux-design-guidelines/) *written by Vitaly Friedman*

### Transcript

<p><a href="https://twitter.com/markodugonjic"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ad2e949-818e-4a8c-9986-f7741aa7a6b0/marko-dugonjic-200x200.jpg" width="200" height="200" alt="Photo of Marko Dugonjić" /></a> <span class="smashing-tv-host">Vitaly Friedman:</span> For him, everything started with a passionate love for CSS and typography in early 2000s. He used to be a front-end developer and UX designer, then moved to the role of user experience director. Working with plenty of clients, such as Deutsche Telekom, SGS, Hrvatski Telekom, Font Bureau, L, National Geographics, and so many others. He also built a tool called Typetester, which has gained quite a momentum in the 2000s and even beyond that, allowing designers and developers to test their topography in the browser.

<span class="smashing-tv-host">Vitaly:</span> Now, five years ago, he moved from Zagreb, Croatia, where he's originally from, to Sacramento, California, where he now is working as a Director of User Experience at SymSoft Solutions. So we know he's an expert in UX, but did you know that he has been an avid fan of Acapulco Beaver's Handball team from Zagreb since the age of seven and remains one up until today? My Smashing friends, please welcome Marko Dugonjic. Hello, Marko. How are you doing today?

<span class="smashing-tv-speaker">Marko:</span> Great... I mean smashing, I guess.

<span class="smashing-tv-host">Vitaly:</span> Excellent. That's wonderful to hear. It's interesting because we have these conversations every now and again, talking about the meaning of life and so many other things. But one thing that really excites me, and I think it deserves a bit of attention, I have this incredible story of how you actually just fell in love with the web many, many years ago, where you used to do something very, very different. And look at you now, work on enterprise applications for a pretty fancy company. Can you tell us a bit of that backstory?

<span class="smashing-tv-speaker">Marko:</span> Sure. It's a weird story in a way, but maybe it'll give someone an idea about how to start with completely different expectations about your career in life and end up in, as you said, in California. And so my story really began when I tried to build a website for, believe it or not, my dogs, my kennel because I used to breed dogs. And at that time, my full-time job was as a fitness trainer.

<span class="smashing-tv-speaker">Marko:</span> So as I was working with people who would have rehabilitation needs or any type of permanent or temporary disability, I also learned about how people who don't have the visual ability to use the web by listening to the web pages. And so one thing led to another, and I was thinking about, "I have this website for my dogs. Is this even accessible?"

<span class="smashing-tv-speaker">Marko:</span> And so what do you do in early 2000s? You find a web forum where real web professionals reside, and you start asking questions about how to improve the accessibility of your website. And it was really just my hobby website, and it's almost something that I've built out of my front-end or front page software, Microsoft FrontPage. I don't know if you remember that one.

<span class="smashing-tv-host">Vitaly:</span> Who doesn't, Marko? Who doesn't?

<span class="smashing-tv-speaker">Marko:</span> And I don't know how, but I never used tables for layout, but I did. And this is probably the first time after almost 20 years that I'm saying it, "I didn't use tables, but I did use a bunch of frames." It was a frameset that pretty much I used to create the header and the sidebar, and the footer. So I had four frames on that page.

<span class="smashing-tv-speaker">Marko:</span> And of course, it didn't validate and everything was really horrible from [inaudible 00:03:45] perspective. But I was hoping that the web design community would help me. And I started researching and learned about CSS positioning, and that was the first thing that I fixed. And then, I learned about Internet Explorer because at the time, I was using Mozilla. I don't know what was even before Firefox. Maybe Phoenix or something like that.

<span class="smashing-tv-host">Vitaly:</span> There was Netscape Navigator, of course.

<span class="smashing-tv-speaker">Marko:</span> Netscape Navigator, yeah. I knew about it, but I think I onboarded with the Mozilla type of browser. But what happened is that at some point, the web forums really weren't enough for, I guess, my obsession with making things perfect. So I started reading web standards from the W3C website, and I read the specs because I thought, "This is probably what every web professional does." And so this is how I learned about accessibility and web standards and all the stuff.

<span class="smashing-tv-speaker">Marko:</span> So that was 2002, 2003. And then one thing led to another, again. I was participating in these web communities, and eventually, people from what today is called Human Design Agency from Zagreb, had a call just like this one. And they said, "Hey, would you like to be paid for what you know?" And I was like, "What are you talking about? I'm a fitness trainer."

<span class="smashing-tv-speaker">Marko:</span> But they did convince me, and then I joined that incredible team. We just had so much fun back in the day. And stayed with them for a couple of years, then moved on to an in-house position, and everything else is pretty much standard. But I think that moment when I realized, "I know something that somebody's willing to pay for," was incredible for me. Again, at that time, it was still almost like a hobby to me. But soon enough, it became a profession.

<span class="smashing-tv-host">Vitaly:</span> Right. And then, of course, you also ended up having your own studio, which then eventually, after a couple of years, moved you to this decision of maybe it's a time to move to or try to move to the US. How did that happen?

<span class="smashing-tv-speaker">Marko:</span> Well, I think what has always been following me is that I didn't really have any general plan. I knew what I wanted to do day-to-day. I knew what I felt about projects and work and skills and all that stuff, but I didn't really have a general plan of moving from this company to another company and then to that company. It was really about maybe selecting good projects, and good people to work with.

<span class="smashing-tv-speaker">Marko:</span> And so when I had my studio, we became pretty international. And you know that we also collaborated on a couple of projects in Europe. And for me, it was really for the past couple of years in Croatia; it was really just 100% international. And so one of our clients, and through a good friend, Christina Portner, who also participated in some of the Smashing activities, I think she gave a talk and had a couple of articles for you guys.

<span class="smashing-tv-host">Vitaly:</span> That's right.

<span class="smashing-tv-speaker">Marko:</span> She introduced me to Savita Faruki, who owns SymSoft Solutions with her husband. And it's a nice, small, family-run business. And looking at the projects that they had and still have, it just made sense for me to move over here, and so I accepted the offer that they extended to me after that visit. Where I really didn't plan to get employed, but we were just discussing some of the collaboration and maybe working on some projects together, but it ended up being me becoming a director of the user experience here at SymSoft.

<span class="smashing-tv-host">Vitaly:</span> Right. That's an interesting story, and also chose a journey that one can take from one place to a very different place. Now you've been all around UX for now 15 or 20 years now. I don't even know. Who counts at this point anymore at this point? And of course, you've seen quite a lot of stuff happening in terms of just UX, I would say.

<span class="smashing-tv-host">Vitaly:</span> We've been fighting, as you could probably find thousands of articles stating that we need to have a seat at the table. And it seems like now, at this point in 2022, we have a pretty solid seat at a table. Do you think that we are in a place where we wanted to be 15 years ago? Is there still something missing? Where do you see us as a community and just as an industry, I guess, in terms of the state of UX today?

<span class="smashing-tv-speaker">Marko:</span> So I think the there's a couple of things right in there. It's an interesting and also complex topic. So I think we do have a seat at a table; however, the horizon is now different. Because as you travel, you just discover other things are behind the horizon. And so once you climb that first peak, then you reveal more peaks to climb. So I think this is where we are right now.

<span class="smashing-tv-speaker">Marko:</span> And a huge thing that nobody really talks about is that even IT or digital as a whole has had that problem in the past, of the seat at the table. And so we just now joined the crowd of people who might have better access to decision-making, but it's still not at the level where we can really immediately influence any decision, especially in big companies and enterprises.

<span class="smashing-tv-speaker">Marko:</span> Obviously, this is where I work at. Startups and younger companies are slightly different there. But enterprises or anything massive, like big insurance companies or big telecoms or financial institutions, or the government, 90% of my clients are now the government... these organizations have been around for years and hundreds of years, even.

<span class="smashing-tv-speaker">Marko:</span> So old ways and things that led to the success that they have right now are not necessarily something that you have to change, but very often, you can also change them by applying correct organizational change management principles. So I would say the challenge that we have nowadays is just general organizational change management. That's a hot topic.

<span class="smashing-tv-speaker">Marko:</span> And again, it's not just the UX people. I think it's the technologies in general or anyone who just have this new way of managing things. I would say digital marketers as well. So all of us, we have to sit at the table, but there's just this huge job of driving and steering the organization into whatever is next, whatever is the future.

<span class="smashing-tv-host">Vitaly:</span> Right. That's interesting. Maybe we should dive into this a little bit more in a little bit more detail. Just because, of course, we read and see and hear a lot of articles around UX, and many of them are very much focused on traditional, I would say, good all startups, digital products, and so on and so forth.

<span class="smashing-tv-host">Vitaly:</span> But at the same time, I find it quite difficult to even find case studies about enterprise UX. So maybe you could actually share those insights about if you do have this situation where you might have a seat at the table, but you actually need to change the organization. And organizations of that size are usually very reluctant to those changes, and people don't like to change their habits quickly.

<span class="smashing-tv-host">Vitaly:</span> So what would be then your process to make it all a reality, to establish a user-centric approach in a relatively tight and conservative and maybe even quite dated, let's say, environment?

<span class="smashing-tv-speaker">Marko:</span> Well yeah, sure. I wouldn't say necessarily that the organization is resistant to change or that people are not willing to change. Just, I would say the volume or the size of the organization is really your biggest enemy because you can influence only so many people in your immediate circle in the organization. And then some organizations are lucky enough to have a big enough UX team or, more broadly digital team that would also have a bunch of developers, solution architects, business analysts, and any type of role that you can think of in IT.

<span class="smashing-tv-speaker">Marko:</span> So it's just a matter of how many people you can touch within the organization with the new principles, how many people are actually in a UX type of project, user-centered service, something like that. So the change doesn't happen in the way of infecting people. You cannot just spread the UX type of virus to people, and they'll all get it. It requires a lot of effort. It requires a custom-tailored approach to communication.

<span class="smashing-tv-speaker">Marko:</span> Someone who has a desk job and is in departments that are understaffed, for that matter, they don't necessarily have enough bandwidth or capacity. And it has nothing to do with the personal preference of the individual person, but just the organizational structure is such that you don't have access maybe, to everyone that you would like to. And of course, it would require a lot of, a lot of time out of the regular day-to-day desk job for people to even get educated.

<span class="smashing-tv-speaker">Marko:</span> So I think the biggest enemy is the size of the organization. So you have to strategically pick and choose your champions within the organization. People who, whoever shows up on your open office or office hours, whatever you call it, meeting, that's a good champion. Even if they have low maturity in UX, these are people who have the intent to change something. And so strategically picking and choosing people, and then helping them become almost like a mentor within the organization to the people around them. And maybe you'll have that department embracing more of an interactive approach to understanding end customers.

<span class="smashing-tv-speaker">Marko:</span> I think this is the way to go. But again, I don't think people should be discouraged with that because even 1% improvement in the business process or in conversions or in optimization is... Vitaly, you and I work with web performance and conversions and E-commerce and all the stuff, and 1% can be a huge improvement.

<span class="smashing-tv-host">Vitaly:</span> Of course. I'm wondering, though, just what your way of dealing with a situation is when you have people in front of you, maybe higher up the ladder in senior management, who just have a very different view on things. Who very strongly look, of course, at their data and their KPIs, at their business metrics, and try to move them.

<span class="smashing-tv-host">Vitaly:</span> And how would you then, in a case where you, again, have to work with a company that might not have a user-centric approach at all and maybe don't think about the customer experience as much as they think about the financial benefit by the end of the year? How would you then argue in those kinds of environments about the role of UX or the importance of UX, or the importance of customer experience?

<span class="smashing-tv-speaker">Marko:</span> Well, I think the best way to sell something is to show them with a live example, with a practical example. And you also know that whenever we would come to an organization and say, "Hey, let's see what's the problem there." And you and I worked with a major German retailer couple of years back, and they were saying, "Hey, mobile is not performing really well. Desktop is much better." And then we realized that the average visit to a mobile E-commerce solution that they had was about 50 years or something like that.

<span class="smashing-tv-speaker">Marko:</span> And so once you start showing off these numbers and say, "This website is now faster," or, "This software will shorten the time from idea to conversion," just, I think performance is such an easy-to-use tool to convince people to invest into it, that it's just unbelievable... Because you can measure the before and offer, and this is something that my team at SymSoft always does. We always do the baseline measurement, whether that's the conversion rates, satisfaction, whatever, you name it, seconds to load.

<span class="smashing-tv-speaker">Marko:</span> And then we test and retest and retest and retest, and then you have hard facts that you can actually tie back to dollar value. And this is how you convince people that this is a good investment. And again, just starting small; almost like when you work with a new chemical that's dangerous, on your car or whatever... they say, "Hey, try somewhere where it won't mess anything up, like in a corner that nobody sees." And so we can also pick a pilot project, a really small case study, prove that it works, and then scale it up to something larger.

<span class="smashing-tv-host">Vitaly:</span> Would you say that it's important to have a buy-in at this point? Or would you say, "Just go ahead, experiment. Build a little prototype, maybe even a little bit in your spare time," just to convince that this is working? Or do you think that commitment from management and green light and approval is critical here?

<span class="smashing-tv-speaker">Marko:</span> So I would say that, and again, this is my experience. I don't necessarily think this is something that happens in every organization... But for me, whatever worked, whenever I was proactive and more on the side of, "Hey, let me do something in my spare time," or, "Let me finish the main task earlier so that I can actually work on the fun stuff."

<span class="smashing-tv-speaker">Marko:</span> Also, signaling to the management that you are proactive, that you are self-driven, that you are self-motivated, that you're not waiting for someone to approve, that you're not waiting to be served or approved or given the space. So I think management definitely likes people who are just thinking that way.

<span class="smashing-tv-speaker">Marko:</span> And so you basically have two benefits. You don't have to ask anyone for permission; you can figure out what is the scope and what is space available for you and just decide to do it. And then, if it doesn't work, you are not even embarrassed. Nobody needs to know. But if it works out, if it's a nice prototype, if it's a nice concept, you can definitely present it to the upper management.

<span class="smashing-tv-speaker">Marko:</span> And then again, you get double credit. You create something fun, but you also show that you care and that you are proactive and self-driven, and all these qualities that everybody ever always writes on the job posts, I guess.

<span class="smashing-tv-host">Vitaly:</span> Right. Well, you did mention scope, and of course, it's a wonderful keyword for me because, of course, I can almost hear the voices in the back asking about how to deal with scope creep. I mean, you are working with very different organizations and, well, of really big size. And eventually, I'm sure there will be situations where late changes come in, poor specifications are in there, communication issues, delays, and all of that.

<span class="smashing-tv-host">Vitaly:</span> So what would be your way to prevent things like this from happening, where you're missing deadlines because of the scope creep or poor estimates? What's your process in there to make sure that we don't get in trouble for delays and maybe underestimating the effort needed?

<span class="smashing-tv-speaker">Marko:</span> That's really a great topic. I think there are two things in there. So definitely, if we underestimate, it's completely on us, and there's no... That's very clear. It's on us. We should have had our due diligence before the discovery stage of the project when we were estimating. But these things happen, I guess, in the beginning for everyone, until you have enough experience to move from a one-page contract into a 50-page contract.

<span class="smashing-tv-speaker">Marko:</span> And my friend, Eva Lucas from NetGAN, from Croatia, he said once to me, "Hey, we started with one page for a contract. Now we have 70 pages," or something like that. So as you are more experienced, you just put more things in the contract and you, I guess, put more things into researching and estimating, and you probably track your hours, and you know how much time for each feature is required. So as you grow more mature in the field, there's less surprising when it comes to estimates.

<span class="smashing-tv-speaker">Marko:</span> Now, the second topic, which is the scope creep, usually in enterprise organizations, they already have this type of... they mitigate that with, again, other contractual clauses. Maybe something that you can communicate early on is the unanticipated effort budget. So that might be 10 or 20% of the budgets that's allocated to the project, that we don't have to spend, but this is our contingency plan.

<span class="smashing-tv-speaker">Marko:</span> And then another thing that's very, very useful, and this is what my director of project management always enforces, is regular meetings. Every week, we have at least weekly meetings. If not, daily stand-ups with the project management on the client side. And we have a really detailed status report that we carry over week after week after week. And we update it, and share it with everyone.

<span class="smashing-tv-speaker">Marko:</span> And we are not really afraid to raise any old risks. So whenever we see that there's a delay in reviewing and providing feedback, we will put it out in the status report, change the green light to yellow light, and just say to everyone, "Hey, we think that this is something that can get out of control."

<span class="smashing-tv-host">Vitaly:</span> Yeah. So that's a very interesting point for me as well because I was working with a company where this turned out to be quite a helper. So really having a more clear overview, I guess, of what our expectations are, what the process is going to be, when we expect some feedback and what kind of feedback we expect as well. And one thing that was really critical and useful at this point was to actually explain to clients that late changes are expensive.

<span class="smashing-tv-host">Vitaly:</span> Late changes are difficult to implement, and they are expensive because if you're coming from a very different industry and you're expecting a product to be delivered, you might not know just how expensive, how difficult it is to actually make those changes later on because you don't have this technical knowledge necessary. So explaining this early on, having this clear communication channel is indeed, I think, quite useful in many ways actually.

<span class="smashing-tv-host">Vitaly:</span> From my end, I think, and one thing I actually definitely wanted to cover today is, because this is something that comes up quite a bit and most recently is... you've been, again, in this industry for quite some time and you had your own head where you had your own agency, and now you are working for a company. What do you think, especially for people who might have just a few years of experience in UX... looking back, what do you think would be the right way to just guarantee personal growth in the company? Negotiate salary, get more ownership, all those things.

<span class="smashing-tv-host">Vitaly:</span> How would you say, what would you recommend maybe to people listening to this today, if they want to maybe improve their salary, maybe grow over time, maybe take more leadership position? What skills would be required, and what would be the right strategy to get where you want to be?

<span class="smashing-tv-speaker">Marko:</span> That's a great question. And so maybe from a manager position now, I can talk about people that I had in my teams, and what qualifies a successful UX designer or professional in general is, it's always, I guess people who are able to manage-up are more successful. Managing-up meaning that understanding that your supervisor or whoever you report to also has their life and their problems and their different, different tasks. And just understanding your overall environment, it's leading peer-to-peer.

<span class="smashing-tv-speaker">Marko:</span> So the understanding is that if you're in UX, there's another person at the same level in your organization in frontend or backend or marketing or project management. So just being aware of who's above, below, on the side from you and just understanding that these are also people. And then, what can you do to really move everyone, together, forward? And so this is, I guess, the attitude, being proactive, something that we talked about a few minutes ago.

<span class="smashing-tv-speaker">Marko:</span> Just not asking for permission because it's not true that you need weeks and weeks to create a concept. Maybe you can just catch something and say, "Hey..." You wake up one morning, and you don't necessarily have to open up your company laptop or anything like that. But just put it on a Post-it, and when it's office time, you just can say, "Hey, I have this idea. Let's do this."

<span class="smashing-tv-speaker">Marko:</span> And that really cost you nothing, I mean, you had that idea anyway. But you're building up your muscle of generating and communicating, and suggesting. And of course, it goes without saying, if you hear crickets every time you have an idea in your company, you should just change the company. But if you have a good environment and receipting environment where you can voice your ideas, that's a great place to be.

<span class="smashing-tv-speaker">Marko:</span> And so what happened is that, once you build up your credit and you look like someone who cares, not necessarily about the company... and I don't want to fool myself thinking that people want to stay here forever, but caring about the quality of work, caring about your teammates, caring about leaving some kind of impact after you leave. And there's another topic that we can also talk about. What do you do when you decide to leave the company? So are you that type of person who thinks about these moments?

<span class="smashing-tv-speaker">Marko:</span> And so once you have that, then salary negotiations are just straightforward because you opened up the communications channels, and then you can just come and sit and say, "Hey, what about the raise?" And then we can talk about that. But if your communication is completely blocked and you're just doing whatever you're told, and you're checking out the tickets, then that conversation about the salary is just difficult because you didn't really create an environment where you have this dialogue anyway, in the first place.

<span class="smashing-tv-speaker">Marko:</span> So I think practicing talking to your boss, good times or bad times, and just not necessarily sharing everything that's happening in your life, but just having this more proactive, I guess, communication. When nothing's really happening, you can just drop by and say, "Hey, this is what I'm working on. It's nothing special, but here it is." And then maybe having this regular cadence.

<span class="smashing-tv-speaker">Marko:</span> And if you don't have one-on-ones, and by the way, which is something that you should have with your boss... because that cadence in one-on-ones really allows you the space at some point to say, "Hey, I would like to work on something else." Or "I would like to have a better impact." Or, "I would like to have a better salary." Or, "Hey, I'm actually looking for a new job. Can you support me while I'm looking for something else?" Just being fair, I guess, to the people that you're working with. So that would be my advice about negotiating salary and these types of things.

<span class="smashing-tv-host">Vitaly:</span> Yeah. I think that many people are struggling with finding themselves in companies where there is just no culture for this kind of feedback. I mean, in some good companies, you will likely have maybe 360-degree feedback or 360-view feedback, whatever it is called, where you get feedback from everyone. And then you would have a dedicated time to bring up any issues with your manager once every three months, four months, two months, six months, I don't know...

<span class="smashing-tv-host">Vitaly:</span> But this is probably an important part to have or an important asset, I guess, to have at least. I think that many people just are afraid maybe a little bit to ask these questions, to bring this up, because I think that it might create a wrong attitude around them and that they're there in the company for the money alone. But I mean, looking at inflation rates happening right now around the world, it's probably important to have that conversation later or earlier. Right?

<span class="smashing-tv-speaker">Marko:</span> Yeah, definitely.

<span class="smashing-tv-host">Vitaly:</span> So maybe also building up on top of that, there're quite a few conversations happening in Europe, at least around salaries. And of course, everybody's looking at salaries in San Francisco thinking about, "Wow! Those salaries. This is incredible compared to the pay you get in Europe. Even if you're living in London or in Berlin, it's just much, much, much higher in San Francisco."

<span class="smashing-tv-host">Vitaly:</span> You happen to be in Sacramento, in California, and you happen to have moved from Croatia to the US, and shared the story about how you did that. So now being there, can you tell us maybe a little bit more about how different everything is for you? So do you feel like the culture, the way companies are run, the way people are working together that it's influenced you in some way, surprised you in some way, disappointed you in some way? What was your experience overall in these five years?

<span class="smashing-tv-speaker">Marko:</span> That's a good question. I think looking back, what really was new for me is how people over here are really focused. Organizations, not necessarily individuals, really focus on processes and repeatability of the process. So if you have certain steps, we can talk about the process... In design, we have double-diamond or triple-I or 5-Ds, or design sprint or design thinking.

<span class="smashing-tv-speaker">Marko:</span> And the reason for all of that, which is not very common in Europe... In Europe, we have a problem and solution. These are two steps that we have in Europe or have had in Europe. But here, it has to be detailed a little more with applicable tools and a decision-making diagram. So this is different over here. When it comes to San Francisco or Sacramento, I think in Sacramento, what happens is that we have a government here, so I'm not in a position to compare our environment in the projects to maybe the Bay Area, where there's a lot of just private companies and startups.

<span class="smashing-tv-speaker">Marko:</span> And there's a start difference even here. A two-hour drive from San Francisco. So I would even think, and this is completely my personal opinion, that Sacramento is closer just to the rest of the US than to San Francisco, compared to Europe. But another thing that's really different here is that the whole communication piece is just much more intentional because a lot of people are landing in California specifically from all over the world, and then you have a mix of cultures. And this is something that I definitely didn't think about when I was working in Europe, however internationally, but still, Europe, which is super tiny, by the way, as a piece of land.

<span class="smashing-tv-speaker">Marko:</span> And then we didn't have so many differences in the sense of just different cultural backgrounds, different educational backgrounds, how people have just different school systems in the first place. And so all of these people come over here, they're talented, they have certain talents; otherwise, they couldn't make it here. But then you have these different communication styles, and you have cultures that are just very generally speaking...

<span class="smashing-tv-speaker">Marko:</span> Far Eastern countries have high context conversations. And then you go more to the west; you have low context, which means that you have to always reiterate what the last conversation was. While in some cultures, it's implied. Everybody knows what we were talking about in the last meeting. So just these types of, I guess, communications skills that we develop now are really... that was really eye-opening.

<span class="smashing-tv-speaker">Marko:</span> I think especially Croatia for that matter, compared to California, is super monocultural. It's just unbelievable... That contrast is just super visible for me now, mowing from one to another.

<span class="smashing-tv-host">Vitaly:</span> Right. So having moved to the US now, do you feel like at any point you could consider moving back?

<span class="smashing-tv-speaker">Marko:</span> I think so, yeah. That's not off the table. I think what we like here, my family and me, and this was really a more collective move, not just necessarily for projects or work, is the access to nature here is just incredible. The way you can consume nature in California specifically is just unbelievable. It's just geared towards families. And over here, everybody's outside all the time, which is our family style anyway. So these are some of the fun things over here.

<span class="smashing-tv-speaker">Marko:</span> The good thing about Europe is that everything is very close. The furthest away is, I don't know, Spain from Croatia, which is a two to three-hour airplane flight. And, of course, I can fly to LA to visit Disney Land or something like that, but it's a drag to even think about the distances over here. So these are some of the differences that we notice. But again, I wouldn't say it's different or better; it's just, I guess, down to every person's personal preferences.

<span class="smashing-tv-host">Vitaly:</span> Right. Okay. Well, now, if you actually could recommend something to yourself when you were breeding dogs back, what? 20, 25-ish, 22 years ago, when you were just starting out with UX and all of that, well frontend and all that... what would you recommend to yourself?

<span class="smashing-tv-speaker">Marko:</span> I guess I would enjoy it more. I would joy the ride more. I was lucky enough to meet really, really great people along the way. I mean, such as yourself included.

<span class="smashing-tv-host">Vitaly:</span> Oh, that's very kind of you.

<span class="smashing-tv-speaker">Marko:</span> Yeah. But also coworkers and other speakers and just professionals. I think at certain points; I could have enjoyed it more, I guess. Just being more relaxed and having more faith in the future that things will work out the way they actually eventually did. So I guess, just more patience.

<span class="smashing-tv-host">Vitaly:</span> Okay. That sounds good. So we've been learning about UX in this episode of Smashing Podcast. So what have you been learning about lately, Marko? Any podcasts, books, TV shows, anything that drew your attention?

<span class="smashing-tv-speaker">Marko:</span> Well yeah, that's a good point. And you know me, I'm all over the place. Right? So I think lately-

<span class="smashing-tv-host">Vitaly:</span> You surely are, Marko. You definitely are.

<span class="smashing-tv-speaker">Marko:</span> ... lately, I'm really into mental health and just on all levels. So personal level, family level, organizational level. Just thinking about all the consequences of COVID, and just remote versus in-person. This is something that I'm really thinking about, not necessarily as something that we have to deal with right now, but what will be the outcomes in the years to come? So just getting ready for that, I guess.

<span class="smashing-tv-host">Vitaly:</span> All right. Well, I'm very much excited to actually meet you in person after all these years. In four days, we're going to meet in San Francisco for SmashingConf San Francisco. This is going to be very exciting. Quality time, family quality time, isn't it?

<span class="smashing-tv-speaker">Marko:</span> Yeah. It's going to be smashing.

<span class="smashing-tv-host">Vitaly:</span> That's kind. If you, dear listener, would like to hear more from Marko, you can find him on Twitter, where he's @Markodugonjic. And you can also check on Typetester, which is still kicking and still around, on typetester.org. Well, thanks so much for joining us today, Marko. Do you have any parting words of wisdom that will be staying with people listening to this, I don't know, decades from now?

<span class="smashing-tv-speaker">Marko:</span> No. Yeah. Thank you for having me. This is so exciting. And I think the best advice that I can have is to keep reading Smashing Magazine.

{{< signature "il" >}}
