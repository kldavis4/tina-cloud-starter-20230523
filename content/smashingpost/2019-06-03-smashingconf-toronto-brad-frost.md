---
title: 'When Do We Need A Design System? An Interview With Brad Frost'
slug: building-design-systems-interview-brad-frost
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/059869b2-e17f-4cc2-8a81-6731e00fced8/smashingconf-toronto-brad-frost-new-spaker.png
date: 2019-06-03T12:30:59+02:00
summary: >
  The web is wonderfully diverse and unpredictable because of wonderfully diverse people shaping it. In this new series of short interviews, we talk to interesting people doing interesting work in our industry and sharing what they’ve learned.
description: >
  The web is wonderfully diverse and unpredictable because of wonderfully diverse people shaping it. In this new series of short interviews, we talk to interesting people doing interesting work in our industry and sharing what they’ve learned.
categories:
   - Interviews
   - Business
   - Design Systems
   - Workflow
   - Teams
disable_ads: true
---
Design systems have been around for quite some time. We’ve even <a href="https://www.smashingmagazine.com/printed-books/design-systems/">published a book on design systems</a>, yet just as they can be difficult to maintain, how do we know when we actually need one in the first place?

Design systems are a wonderful yet intricate tool. They provide us with a solid ground to stand on as we tackle the increasingly diverse and fast-moving digital landscape. However, like most things in our field, the hard part of design systems isn’t specific design tools or code frameworks; it’s wrangling people and all their quirks.

I had a chance to speak with Brad Frost, author of the book [*Atomic Design*](https://atomicdesign.bradfrost.com/) that introduces a methodology to create and maintain effective design systems, and one of the speakers who I’m looking very much forward to bringing onto the stage at [SmashingConf Toronto](https://smashingconf.com/toronto-2019/) in just a few weeks.

<figure class="video-container break-out"><iframe loading="lazy" src="https://www.youtube.com/embed/Tsg7dbUDdqc" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<p><span class="smashing-tv-host">Vitaly:</span> Okay, so hello everyone and welcome again to one of those interviews where we’re talking to interesting people behind the scenes, doing the magic, sometimes silently, sometimes quite publicly, openly, and so today I’m happy to have with us our one and only Mr Frosty.

<p><span class="smashing-tv-host">Vitaly:</span> Hello, Mr Brad Frost, how are we doing today?

<p><span class="smashing-tv-speaker">Brad:</span> Hi, I’m doing great, thanks for having me Vitaly.

<p><span class="smashing-tv-host">Vitaly:</span> Oh it’s my pleasure. I’m looking forward to see and explore some of the things you’re going to cover in Toronto but most specifically, I’m kind of looking forward to see what’s going on in your head right now? What are you thinking of right now?

<p><span class="smashing-tv-speaker">Brad:</span> Oh my. What am I thinking of right now?

<p><span class="smashing-tv-host">Vitaly:</span> Yes.

<p><span class="smashing-tv-speaker">Brad:</span> I’m thinking about, uh, we’re doing a big design system for an airline, and so I am fixing an excessive [inaudible 00:01:07] and a date picker calendar widget.

<p><span class="smashing-tv-host">Vitaly:</span> Oh, that sounds&mdash;

<p><span class="smashing-tv-speaker">Brad:</span> That’s what I’m doing, like, literally right this second.

<p><span class="smashing-tv-host">Vitaly:</span> Okay, this sounds like it’s a lot of fun.

<p><span class="smashing-tv-speaker">Brad:</span> Yes, or something.

<p><span class="smashing-tv-host">Vitaly:</span> I heard rumors, maybe it’s just me, I don’t know, but I heard rumors that you’re involved in some way to design systems and atomic design and stuff, so I’m wondering, design systems, does every website need one really at this point of life?

<p><span class="smashing-tv-speaker">Brad:</span> I generally think so, yes. I mean, the degree of formality around the design system is probably not every website needs, but I think that every single website could benefit from component driven architecture, design, and development principles. Just as one example, my wife is a jeweler and also she just has a five pager kind of website and I was able to build that in four days, because I was following good reusable component based design and development. So the first template I had to make, I obviously had to build all of those components sort of from scratch, but then the second page template, I was able to reuse some of those and by the time I got to the third and forth and fifth template, I already had a lot of the building blocks in place, so those latter templates were able to roll off the assembly line a lot faster.

<p><span class="smashing-tv-speaker">Brad:</span> I think a lot of people will get in touch with me and ask me those kind of questions and say, well, I make these landing pages for a marketing company and people scan a QR code and go to these landing pages, and they have a shelf life of a month at most or something like that. It is like very short lived sort of websites, and they’re like, "Well, we could have used a design system," and I said, well yes, you’re making the same type of page over and over again, and so rather than rebuilding those pages with 100% effort each time, if you are to put in place a pattern, and you could be as clever as you want when it comes to skinding them or theming them or whatever and making them aesthetically unique. But they have to rebuild a big splashy new hero component or a button every single time, just doesn’t make sense.

<p><span class="smashing-tv-speaker">Brad:</span> Even for these things that at face value feel very ephemeral, or it’s just like a one-page landing page, surely I don’t need a design system from that? Yes, actually you can benefit from them, so again, I think that, that’s important. Any project could benefit from solid component-based design and development. The whole, "Do you need this big glossy website (like a material.io or lightning design system with a bunch of design principles and a bunch of documentation and stuff)"? Probably not, for those smaller sites, and that’s fine. But that doesn’t mean that you should just be thinking of things as individual screens or individual projects.

<p><span class="smashing-tv-host">Vitaly:</span> So Brad, one more thing though, when we talk about things like again, design systems and so on, I think that especially larger companies, they always desperately try to find case studies, like this company may be preferably our competitor, they build a design system or design a design system and they did magic for them. However, I’m not sure if there are any publicly available data or publicly available case studies which show that we did this, our conversion improved, our maintenance improved, we’re building faster and so on. Do you think there is anything of that thing or is it still something that has to be discovered and then you actually get to see the benefits of a design system, maybe months or even years ahead of time? Is it an investment or is it something you can measure efficiently?

<p><span class="smashing-tv-speaker">Brad:</span> Yes, great questions, and the questions around metrics, it’s definitely hard to come by, hard numbers, just because sort of unlike just doing a big redesign where you have one site and then you redesign and then launch the new site and then you’re able to look at the Google analytics and see whatever metrics you’re looking for, whether that’s page weight has gone down or time spent on site has increased, or whatever your metrics are, it’s easy to see that result.

<p><span class="smashing-tv-speaker">Brad:</span> Obviously, if you’re creating a design system, you should still be able to see some of those results as new projects launch and get out into the world. You should see those metrics going in the right direction. Obviously, that’s a sign that the design system is doing what it need to do, but it’s hard to pin down metrics and public case studies because so many of the metrics for the success of a design system are internally facing &mdash; right? So it’s not really about like the public website &mdash; well, of course, it is, but (and again you can track that stuff with Google Analytics and the rest of them) but a lot of it has to do with how fast the internal teams are working right?

<p><span class="smashing-tv-speaker">Brad:</span> How quickly you can get projects out the door and how many UI-related bugs are you fielding, what are your customer support centers getting as far as UI-related issues with respect to your website and stuff like that, so there’s a lot of metrics that are tuned towards how many jitterbugs are there around the UI and those should be trending downwards as the design system gets adopted. Or like how many customer service calls are you getting or support tickets around ("Oh, I’m using this browser and this thing is broken, and I can’t do that.")

<p><span class="smashing-tv-speaker">Brad:</span> It’s like those things should diminish over time. But because those are also internally facing things, not many companies publish that. There are a few examples though out in the wild, and a lot of them are wrapped up in case-study blog posts and things like that, but one of them that comes to mind is the Westpac design system. They’re gelled, their global experience language and they have some stats on their websites and stuff about how they were able to increase their velocity by 700% or whatever. So there’s stuff out there, but a lot of the stuff &mdash; if I’m honest &mdash; is pulling some numbers out of the air a little bit, just like looking at, "Here’s what we were doing before, we were able to launch projects in six months and now with the design system we’re able to launch them in six weeks." And so just putting some marketing spin on that and saying, "oh, we’re able to launch things five times faster," whatever that math works out to. So it’s just like putting a bow on it and stuff but that’s generally like the metrics that we want to follow as our people getting things out the door faster, is the overall code and design quality improved, are there less customer facing issues on the site and are our products, are people getting things done faster as a result of using a more consistent, cohesive user experience.

<p><span class="smashing-tv-host">Vitaly:</span> Yes, that makes sense. I’m curious though, so when it comes to specifics of a design system, it’s been very interesting because just recently I saw a project, and it’s also something that I explored sometime like in the past but every now and again you see people using interesting naming conventions in their design system. Like for three different sizes for different blogs, like the same media object, they would use something that’s memorable rather than something that’s functional. So they would use something like "momma bear", "papa bear", "baby bear", but would you say, when it comes to naming, what would you prefer to use, what would you rather recommend to avoid?

<p><span class="smashing-tv-host">Vitaly:</span> Because obviously, when you have "papa bear", "momma bear", "baby bear", how do you grow from there if you have a fourth part of the family, you need to find a really convenient name for that right? Is it better to use small, large, medium, like what patterns would you recommend to stay away from when naming things, what works for you best?

<p><span class="smashing-tv-speaker">Brad:</span> Yes, it’s a tough question that I think that every team faces. The short answer is, use whatever language makes sense for the team. You don’t want to introduce crazy, clever names if one person invented those names, and I was just thrusting them upon everybody else without their involvement, I guess. And I’ve seen that happen with atomic design, which is a naming convention that I created, but a lot of people will take that naming and adapt it or abandon it, or just call things or map them to whatever makes sense for their teams, like, "Oh, we call these things ‘components’, and we call these ‘smaller things’ or ‘modules’ or whatever, so we’re going to call it ‘elements’, ‘modules’, and ‘components’ instead of ‘atoms’, ‘molecules’, and ‘organisms’."

<p><span class="smashing-tv-speaker">Brad:</span> And I love that, I think that, that’s really important for teams to establish a language that makes sense with them and how they’re already thinking and stuff like that. You don’t want to get new and jazzy and inventive if that isn’t warranted or if people are just going to, "Wait, what is ‘momma bear’ again?" So that’s important, but you’re also talking about, it’s like what happens when it goes to naming things that might need some space in between? So things like t-shirt sizes. It’s like, yes, there’s ‘small’, ‘medium’, ‘large’, ‘extra large’ or whatever, but what if you need a ‘medium two’ or a ‘medium three’ and a ‘large two’ and stuff like that?

<p><span class="smashing-tv-speaker">Brad:</span> And so you end up wedging these things in between and that never really feels right. My colleague, Dan Mahr, recently talked about this with respect to typography sizes. A lot of different design systems and style guides and things will tend to call things, ‘H1’ through to ‘H6’ for the different heading styles. But even that’s a little misleading, because one it like time, a semantic meeting to a stylistic thing, which isn’t always great. But then two, there tends to be more than six styles not just for headings for body copy, but also some may be stylized text or a block quote or a pool quote, so he explored that in a recent post where he’s talking about the naming of the stuff.

<p><span class="smashing-tv-speaker">Brad:</span> For a project we’re working on now, where basically we have just ‘typography preset one’, ‘typography preset four’ and ‘five’ and ‘six’, and the first few are loosely mapped two sizes and things like that, but for a lot of them, as the system has grown, and we’re like, Oh we actually need an additional preset, and we need the ability to add even more, they just get thrown onto the pile as ‘typography preset eight’ and ‘nine’ and ‘ten’ &mdash; and those aren’t terribly intuitive names. It’s not like, "Oh, this is ‘baby bear’" or whatever, and "Oh, this is..." (you know, Dan was toying around with the names of X-men or whatever &mdash; you could get clever like that.) But ultimately, at the end of the day, we picked a convention in a system that scales in that, "here’s what happens when you need to add a new thing" and crucially &mdash; the crucial bit to any of this &mdash; is the documentation and the shared understanding of that stuff.

<p><span class="smashing-tv-speaker">Brad:</span> In our style guide, in our reference website for the design system, we have a typography page where we spell out, here’s what ‘typography preset one’ is, and here’s what characteristics it has and here’s what usage it should be used for. And it’s like, "Oh, here’s ‘typography preset eight’" which is more of like a kicker, really small eyebrow, you know what I’m talking about, it goes above a title that might be the category of the blog post or whatever, I don’t know, but it’s like a little stylized, so it’s upper case, it’s spaced out a little bit, it’s like a thinner font, it’s like an understated typographic thing.

<p><span class="smashing-tv-speaker">Brad:</span> Now, none of that says ‘typography preset eight’, it just comes with the usage, you have to understand, "Oh, that’s the ‘kicker styles’." But it can’t just be called ‘kicker style’ because we’re actually using it for a bunch of different things. We’re using it for a primary navigation, we’re using it for the eyebrows or the kickers above a title, but we’re also using it for a bunch of other things as well, which is why I think it’s important to establish more agnostic names, rather than tightly coupled to its usage names.

<p><span class="smashing-tv-host">Vitaly:</span> That makes sense, of course. I heard rumors that you might be doing or covering something along the lines of design systems in Toronto? May it be that I’m right or maybe I’m wrong? Maybe you’re even having a workshop in there &mdash; if I’m not mistaken?

<p><span class="smashing-tv-speaker">Brad:</span> Yes...

<p><span class="smashing-tv-host">Vitaly:</span> So I’m wondering, can you briefly describe maybe like within a minute or so, what you’re going to speak about, what is the session going to be like and also what the workshop is going to be like?

<p><span class="smashing-tv-speaker">Brad:</span> Yes. I’m super excited for Toronto and the gist of my session at the conference is going to be live in front of everyone, building a design system, so this is using what I call a workshop tool like Pattern Lab or Storybook to build out a design system, components as well as the screens that we’re building from those components, like live in a session. And that’s to demonstrate how that process works, how that component driven, so the design and development process works and how we iterate inside of this environment to build real pilot projects for the design system, as well as actually extracting the components from those projects.

<p><span class="smashing-tv-speaker">Brad:</span> So that’s the session, which I’m excited about and then the workshop is more of a deeper dive, there’s so many aspects to a design system initiative, and so basically the workshop is set up to go soup from nuts, from selling the design system to kicking the design system off, to planning what tools and technologies we’re going to use, what methodologies, what processes are we going to use, launching a design system, getting it into actual products, so deploying a design system, but then crucially maybe like the main bit is like, how do we maintain this over time? How do you set up your team structure? How do you set up your technology structure and infrastructure to support an ongoing living, breathing design system? So, that’s the workshop: it’s soups to nuts and how we build and maintain a design system?

<p><span class="smashing-tv-host">Vitaly:</span> That sounds pretty intriguing. So maybe then just the last one &mdash; the last question for you &mdash; and thank you so much for your time... I’m wondering if there were some lessons you learned the hard way, things that you would definitely not recommend to do when building or designing or creating or setting up our design system? What are some of the hard lessons you had to learn, things you definitely would recommend to stay away from?

<p><span class="smashing-tv-speaker">Brad:</span> There’s a bunch. I’ll say that one thing I’ve learned in consulting with a bunch of clients is, probably one of the biggest things (pitfalls we see teams falling into) is that they think that a design system is just the components and so I’ve worked with teams that they’ve spun up entire teams for, "Oh, this team is going to work on the buttons," and, "Oh, this team is going to work on the cards," and, "This team is going to work on the foreign fields" &mdash; it doesn’t work like that. You can’t just create these things in isolation and then cross your fingers and hope that they come together to form a cohesive experience.

<p><span class="smashing-tv-speaker">Brad:</span> Our big recommendation is, you have to start with real work, this is why pilot projects are so incredibly important. It’s like, you start with a real thing that really needs a built and then you use that as an opportunity to build your design system from. If your pilot project is the home page, you’re going to have a hero, you’re going to have some cars, you’re going to have a newsletter sign-up thing. You need to build all those in order to build the home page. And so through the lens of building out the home page, you’re able to extract those other components. So that’s my mistake to avoid is: don’t just build a design system in isolation. It has to be tied to the real products that your organization needs to produce.

<p><span class="smashing-tv-host">Vitaly:</span> Okay, that makes sense. Wow, Brad. I’m looking forward to your session. I’m wondering maybe you will be, I don’t know, building a design system for horoscopes, or maybe for, I don’t know, for something else? Is there a particular project you ever dreamed of, maybe like for NASA, design systems for NASA? No?

<p><span class="smashing-tv-speaker">Brad:</span> I mean that would be awesome. I don’t know, in my view I’ve never really thought of that in what would be like a dream client, I think that my sweet spot is where the technical ends of things but also the organizational end of things are both interesting. They have some interesting problems to solve, and so I love working with clients that are at that place where it’s like, "Oh, we need some technical heLp, but crucially we also need a lot of organizational or cultural help," so I’m being vague here but I love that sweet spot in between. The work itself is good and I have fun as a web developer swimming in those waters, but then I also really like helping teams establish better processes and cultures around design and development.

<p><span class="smashing-tv-host">Vitaly:</span> Yes, well listen Brad, your curiosity of things, in things, and seeing things through and also making things a bit better, so let’s make things a bit better in Toronto then.

<p><span class="smashing-tv-speaker">Brad:</span> I'd love it.

<p><span class="smashing-tv-host">Vitaly:</span> Alright, thank you. Thank you so much for taking the time, I’m looking forward to seeing you soon. And please say ‘hi’ to Louis as well.

<p><span class="smashing-tv-speaker">Brad:</span> Alright, hey, thanks for having me.

<p><span class="smashing-tv-host">Vitaly:</span> Of course, my pleasure! Okay, talk to you soon Brad, thank you.

<p><span class="smashing-tv-host">Vitaly:</span> Alright, so thank you so much to everybody for joining in. Let’s see, well, I hope I will see some of you in Toronto as well. It’s going to be an interesting conference with a couple of live sessions along the way. And please stay tuned, we’re going to have a couple of more interviews like this one and if you’re interested, please do let us know in the comments, or even ask the questions we should ask next time. With that in mind, signing off, and see you next time.

## That’s A Wrap!

Build a design system in less than an hour? That’s crazy, but not entirely impossible.

We’re looking forward to welcoming Brad at [SmashingConf Toronto 2019](https://www.smashingconf.com/toronto-2019/), with a live session on building design systems. He’ll demonstrate how to use Pattern Lab to simultaneously build both a design system’s front-end components and several screens of a real pilot project. We’d love to see you there as well!

Please do let us know if you find this series of interviews useful, and whom you’d love us to interview, or what topics you’d like us to cover and we’ll get right to it!

{{% feature-panel %}}

{{< signature "ra, il" >}}
