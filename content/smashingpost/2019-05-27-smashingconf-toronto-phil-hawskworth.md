---
title: 'Demystifying JAMstack: An Interview With Phil Hawskworth'
slug: demystifying-jamstack-interview-phil-hawskworth
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94a4476c-de5b-4f51-aec1-7f2ab09dac9e/phil-hawksworth-smashingconf-toronto.png
date: 2019-05-27T13:00:59+02:00
summary: >
  The web is wonderfully diverse and unpredictable because of wonderfully diverse people shaping it. In this new series of short interviews, we talk to interesting people doing interesting work in our industry and sharing what they’ve learned.
description: >
  The web is wonderfully diverse and unpredictable because of wonderfully diverse people shaping it. In this new series of short interviews, we talk to interesting people doing interesting work in our industry and sharing what they’ve learned.
categories:
   - Interviews
   - Business
   - Jamstack
disable_ads: true
---
Some of you might have heard of JAMstack, and perhaps even about [how to switch from WordPress to Hugo](https://www.smashingmagazine.com/2019/05/switch-wordpress-hugo/), but is JAMstack a viable option for any kind of project?

I spoke with Phil Hawksworth, a front-end engineer who (after 9 years of working at agencies has returned to working on a standalone product) is now focusing on developing strategies for JAMstack technologies to make building for the web simpler, faster, and more secure. Phil will also be co-hosting [JAM_stack ldn](https://jamstackconf.com/london/), a conference dedicated to static site generators, serverless and JAMstack in London, on July 9–10.

<figure class="video-container break-out"><iframe loading="lazy" src="https://www.youtube.com/embed/OvrWeF5dYqY" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<p><span class="smashing-tv-host">Vitaly:</span> So hello and welcome to one of our conversations with our speakers at Smashing Conf and generally nice people. You might remember those times when FTP was a big thing and maybe actually you’re still deploying why FTP is a perfectly safe space so you don't have to worry about that. But changes are high that you’re not using FTP anymore and instead move to Git based workflows, and probably continuous deployment. All this fancy whistles and bells. And so today I’m very happy to welcome Phil Hawksworth who is actually working at Netlify, Developer relationships [inaudible 00:10:00]. Hello Phil. How are you doing today?

<p><span class="smashing-tv-speaker">Phil:</span> I’m great, how are you doing Vitaly? It’s nice to see you.

<p><span class="smashing-tv-host">Vitaly:</span> Aw, I’m doing great. It’s always pleasure to see you. You’re like a sunshine streaming Netlify and Jump Stack and everything.

<p><span class="smashing-tv-speaker">Phil:</span> I try. I’m not even branded up, what a missed opportunity.

<p><span class="smashing-tv-host">Vitaly:</span> That’s okay, that’s okay. But you have to tell me, so that gem or jen or jeet, like, jem? Is it jem?

<p><span class="smashing-tv-speaker">Phil:</span> Jam. It’s jam. It’s all about the jam.

<p><span class="smashing-tv-host">Vitaly:</span> It’s all jam. So the JAMstack. For developers or designers, actually never heard the term before. If you wanted to maybe sum up what it is and why it’s good and what are the benefits of it in the first place. Why would you ever want to move from your traditional, good old stack to JAMstack. Maybe you could sum it up briefly.

<p><span class="smashing-tv-speaker">Phil:</span> Let me see if I can try because it’s tempting just to say, JAMstack, the JAM stands for Javascript, APIs and mockup. But that in itself doesn't really explain very much, just knowing what it stands for. So really, JAMstack is all about a way of deploying and serving websites that don't rely on an origin server, they don't rely on requests hitting an active server all the time.

<p><span class="smashing-tv-speaker">Phil:</span> So you might be more familiar with stacks like the LAMP stack which was Linux, Apache, MySQL, and PHP, that was the kind of stack that was serving your site there. With JAMstack, it gets a bit different because we’ve kind of moved up a level, away from the server and closer to the browser so it’s thinking a lot about getting in a browser as fast as possible and then using technologies in the browser to enhance and augment it later on. So JAMstack is all about pre-rendering sites, getting it into the browser, and then maybe enhancing it, augmenting it, the experience with Javascript running in your browser, maybe making requests to APIs and that kind of thing.

<p><span class="smashing-tv-speaker">Phil:</span> So that’s the model, trying to get away from having a server that you need to maintain because I know maintaining a server is difficult. I don't know about you but I’ve got lots of sites that kind of went away when I just turned my back on them for a few years. I needed to upgrade PHP which meant I needed to upgrade the version of Linux which I’ve done once in a blue moon. So maintaining servers is difficult so the idea of the JAMstack is to try and make it as simple as possible to serve sites as static assets and then make the most out of all the APIs and inabilities in the browser to do augmentation and do more things with them there.

<p><span class="smashing-tv-host">Vitaly:</span> Right, makes sense. Well, in fact, we moved to JAMstack 2 years ago or so now.

<p><span class="smashing-tv-speaker">Phil:</span> Two years?

<p><span class="smashing-tv-host">Vitaly:</span> Yeah, it was quite a journey for us. And of course, we learned a few lessons along the way. But I’m wondering, would you say that essentially every project could benefit somehow from moving or moving some parts of it to JAMstack or like, where do you see its limitations? Is it something that potentially every developer could use in a project or is it something that’s kind of dedicated to a particular group of websites or a group of projects?

<p><span class="smashing-tv-speaker">Phil:</span> Yeah, I mean, it’s tempting to say, oh yeah, you can use it for everything but I think you should be careful saying that about any technology. You know, you really need to kind of pick the use cases and make sure it’s tailored well. I would say the first instinct when you think about a JAMstack site and maybe think about something which is served as static assets, maybe directly from a CDN. You might think, well that’s only good for sites that don't change very often, they’re quote on quote, static, they don't change. But in actual fact, that’s not really the case because so many tools exists now that can reduce the friction in deploying things.

<p><span class="smashing-tv-speaker">Phil:</span> You can deploy many many times a day, or many times an hour if you want and actually make things feel a lot more dynamic than they might have done before. So some of those use cases where you think they wouldn't be appropriate; those actually come into the fold as well. The time that it gets challenging, perhaps though, is when we’re creating sites that have many many pages, many hundreds of thousands or many millions of pages because the JAMstack model really makes a lot of sense when you can pre-generate your site so you might be using a static site generator. Those have really in vogue at the moment; those are really really popular.

<p><span class="smashing-tv-speaker">Phil:</span> But of course, they have to do a piece of work every time they deploy an update so if you have a site, maybe like a newspaper site, that has many millions of pages, the work that is required to re-generate that can be quite, you know, that can take a long time so that’s when you start bumping into some of the limitations of where JAMstack can be, kind of, simply used. You can start to get a bit crafty and start to work around that if, you know, you’re very very crafty but it definitely introduces some challenges.

<p><span class="smashing-tv-speaker">Phil:</span> One of the things I’m starting to see from a variety of different static site generators like Gatsby for instance or React Static, and also Hugo. The teams behind those static site generators are starting to explore ways that you can do progressive generation of the pages so in other words, you don't re-deploy the entire site or regenerate the entire site every time something changes but try and find ways to do incremental builds. It’s kind of a challenging problem to overcome but there’s work being done on that at the moment so that will help to try and break down that barrier as well. But, certainly at the moment, finding ways to use a JAMstack site for a website that has many millions of pages or many hundreds of thousands of pages, that’s where it can be a little bit challenging right now.

<p><span class="smashing-tv-host">Vitaly:</span> Oh, that’s interesting. So actually the idea of being then to serve a div of the state that you have and essentially that whatever you have to build, like a new portal has to be kind of paged into it so it’s interesting to see this happening. Because you also, just recently, I think two weeks ago, there was an article by Jason Pamental coming up where the idea was actually very similar where you would actually load the fonts, and then you load the first page that you need and then you load the second and then you actually merge them in a way to create a new font, like also incremental font loading.

<p><span class="smashing-tv-speaker">Phil:</span> Interesting.

<p><span class="smashing-tv-host">Vitaly:</span> That would be really interesting to explore that.

<p><span class="smashing-tv-speaker">Phil:</span> Yeah, and it’s not just so much of the loading, it’s the generation-

<p><span class="smashing-tv-host">Vitaly:</span> The generation, the build out.

<p><span class="smashing-tv-speaker">Phil:</span> Yeah, exactly.

<p><span class="smashing-tv-host">Vitaly:</span> I understand. But what do you think are kind of the common challenges that most developers have? Well, I mean, let me move back first. If you have never worked on JAMstack before and you are very much comfortable and happy with your LAMP stack and you wanted to maybe explore the possibility and advantages like security and performance of JAMstack. How would you actually start? What would you move, what does it mean to workflow change?

<p><span class="smashing-tv-speaker">Phil:</span> So, the changes to the workflow can actually be quite profound because you are taking away a lot of the infrastructure that you'd normally depend on and say actually we can do away with that and start deploying things directly to a CDN. But in terms of how someone might get started experimenting with this, chances are they might be using some of the aspects of this already. You know, even on kind of traditional ways of building things for the web.

<p><span class="smashing-tv-speaker">Phil:</span> If you think about how you might build something on the LAMP stack, chances are in your PHP there, you’re doing things like writing a template that grabs data from a data source, in this case, the MySQL database or some kind of database, rendering those things into view and then getting them served. And that’s kind of similar to how static site generators work. They have templates, they grab data from somewhere that might be kind of structured data in files or it might be hitting some kind of database or a content API. Either way, it’s grabbing data, combining that data with templates, generating views and the only difference is that it’s not doing that on demand, it’s doing that ahead of time. So, some of the logical steps in that kind of cognitive steps for a developer might not actually be that huge.

<p><span class="smashing-tv-speaker">Phil:</span> The biggest change is in thinking about how you deploy things. Because really what you’re deploying is your built, rendered assets entirety every time you want to do a deployment. That starts to bring things like the management of the content and the management of the code all into the same place so that things like the vision control across all of those things together. So it starts to be a slightly different way of thinking about how you might develop and manage sites and the content within it. So there are a few changes there. But the nice thing is, a lot of static site generators can be quite straight forward to start experimenting with and the nice thing is you don't need a ton of infrastructure to do this. So the nice thing is that you can really start to build things out right on your local machine. You’re running a static site generator right on your machine and you can get a really good sense of what the outcome is going to be without needing to lean on lots of other infrastructure.

<p><span class="smashing-tv-speaker">Phil:</span> So that kind of first step, the on ramp, can be quite shallow for you to start to say, "well, I’ll try this particular set of tools. I can run them locally." And you’ll have good confidence that when you deploy the output of that somewhere, that will be exactly the same where you deploy it as it would be locally. That’s one of the things that I love about rendering things that are static because you’re not depending on lots of infrastructure and moving parts to serve them. You can look at them on the static server on your own machine and think, "yeah, this is how it will work when it goes off to a CDN."

<p><span class="smashing-tv-host">Vitaly:</span> Mm-hmm (affirmative);And also the infrastructure when we look, for example, into the way we build single [inaudible 00:10:07], and there is a huge number of options of what you could do. For the server, for the client, and everything in between.

<p><span class="smashing-tv-speaker">Phil:</span> Yeah.

<p><span class="smashing-tv-host">Vitaly:</span> And so, I think, in our case because we are kind of building out a skeleton and it’s serving straight through CDI with content and all and enhance with Javascript. It was actually quite reasonable and quite, I wouldn't say easy but it made sense to move to that kind of set up. Because in the end, it’s just content that leaves on the page. It’s just HTML with a few comment areas and search box and a few other things. But if you’re moving towards really standalone application, maybe even financial application, online banking, this kind of thing. Do you think still that JAMstack would be a good option to consider there if you’re having something that requests a lot of logic? Does it need a server or not?

<p><span class="smashing-tv-speaker">Phil:</span> Well, I hate to trot out the old phrase, "it depends." But it kind of does depend a little bit. With that said, there are lots of applications which work just as well being a Javascript application as actually having a service side component to them. I say that with a certain amount of caution because I’m a little bit old school when it comes web development and I really like getting things into the browser as HTML as much as possible and then having a really high watermark from where you progressively enhance from. So I don't personally like doing everything in Javascript and just shipping an empty body tag and then running everything through Javascript.

<p><span class="smashing-tv-speaker">Phil:</span> With that said, there are sometimes where that’s perfectly acceptable. If you’re thinking about a certain kind of application which, of course, would heavily depend on Javascript and you know your audience. That can be completely reasonably. There are things that have been shipped recently. I’m thinking actually of something that shipped to Google IO for, as an example, the chrome team put together a game which was very heavily Javascript and that worked beautifully served statically. There are plenty of use cases where that can work.

<p><span class="smashing-tv-speaker">Phil:</span> Going back to your financial example, I used to work, my very first job actually, was putting numbers on screens for traders to trade off using web technologies and this was before web sockets, it was before Ajax, it was before anything really that was useful to help you do that and it’s kind of challenging but more recently, you would do a lot of that kind of thing in Javascript and that makes perfect sense. You can start to make secure requests to APIs right from the browser. There’s plenty of models now for doing authentication and authorization directly from your browser. So in many ways, this can simplify the stack for financial institutions that want to build some of these things out because the way that they can decouple some of these things can make them much more manageable. So I'd certainly think that the JAMstack model could perfectly work in that scenario as well.

<p><span class="smashing-tv-host">Vitaly:</span> Okay, so maybe coming back now to explore that world of JAMstack and front end. What are you most excited about these days, Phil? If you look at JAMstack and front end in general, is it something that’s really keeps you awake at night where you wake up in the morning hoping that yes, I’m going to work on that someday. One day I will get it done. Do you have [crosstalk 00:13:33]

<p><span class="smashing-tv-speaker">Phil:</span> Yeah, and this is the kind of thing where your answer can be different day by day because it feels like this world moves so quickly. And that in itself is one of the things that excites me so much. Now that we’re starting to see the browser APIs start to really progress and the kinds of things we can do directly in the browser without having to implement them ourselves. That’s kind of exciting to me. I’m still very much a duffer when it comes to SVGs. I should explain the word duffer, if anyone who’s not English and watching this, it means a fool. It means I’m way behind the curve.

<p><span class="smashing-tv-speaker">Phil:</span> But I find myself really wanting to do more with SVGs and animations are kinds of things I’m just way behind on and I want to play with that. But things like the browser APIs whether that’s things for offline or for improving performance and particularly at the moment the way the font loading seems to be getting more and more accessible so that we can start to really create things that visually are very rich and closer to what we might want to make with typography. I’m a bit of a nerd for that stuff, I like that kind of stuff so I want to play more and more with that.

<p><span class="smashing-tv-host">Vitaly:</span> So Phil, talking about JAMstack conf in London. Can you also explain in a few words like what is it going to be about, what’s the focus and who is it for and what is your role there? Just behind the scenes, taking care of the content and all. What is your role there?

<p><span class="smashing-tv-speaker">Phil:</span> So I’ve had the fun part of the job. So I’ve had the opportunity to go out and find speakers and find interesting content so I’m really excited about how the programs come together. We’ve got people like Chris Coia who’s going to talk about empowering front end developers and how much we can do with front end technologies now based on this JAMstack model. We’ve got people like Jake Archibald and Surma from the Google Chrome team who are going to talk about things like performance in the front end and ways that we can really drive very performance experiences either with static hosting or infrastructure or code that runs right in the browser.

<p><span class="smashing-tv-speaker">Phil:</span> We’re also going to have Yuna Kravitz talking about things to do with CSS and Houdini and all of those kinds of things. And much much more besides. We’ll also be talking about things to do with the cultural change that a JAMstack model can have on your organization and on your projects so it really reaches all over the place. So I’m kind of excited about that. I’ll get the chance also to introduce all of these people because they’ve let me go wild and be the MC as well so that means I get to talk to these people and ask a few questions and those kinds of things. So I think it should be very interesting for anyone who is interested in front end development and also new models of delivering projects on the web in a really efficient way.

<p><span class="smashing-tv-host">Vitaly:</span> Oh, so you do like the spotlight on stage, huh?

<p><span class="smashing-tv-speaker">Phil:</span> I’m an attention seeker. You should know that by now, Vitaly.

<p><span class="smashing-tv-host">Vitaly:</span> Oh, actually I always thought you were very humble and nice and kind person, apparently I was-

<p><span class="smashing-tv-speaker">Phil:</span> It’s an act, it’s an act.

<p><span class="smashing-tv-host">Vitaly:</span> Okay, that’s fine. Phil, we’ll meet in a few, oh actually, tomorrow.

<p><span class="smashing-tv-speaker">Phil:</span> I’ll see you soon for another event but otherwise I’ll see you in July, July the ninth and tenth.

<p><span class="smashing-tv-host">Vitaly:</span> [inaudible 00:16:52] So with this in mind, thank you Phil and signing off. Bye bye everyone.

<p><span class="smashing-tv-speaker">Phil:</span> See you soon.

## That’s A Wrap!

We’re looking forward to welcoming Phil at [SmashingConf Toronto 2019](https://www.smashingconf.com/toronto-2019/), with a live session on JAMstack. We’d love to see you there as well!

Please let us know if you find this series of interviews useful, and whom you’d love us to interview, or what topics you’d like us to cover and we’ll get right to it!

{{% feature-panel %}}

{{< signature "ra, il" >}}
