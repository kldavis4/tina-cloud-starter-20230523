---
title: 'Smashing Podcast Episode 11 With Eduardo Bouças: What Is Sourcebit?'
slug: smashing-podcast-episode-11
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48f3c4f8-dce3-4202-adf0-b08418fe572f/smashing-podcast-episode-11.png
date: 2020-03-10T10:30:00.000Z
summary: >-
  In this episode of the Smashing Podcast, we’re talking about an interesting open-source tool called Sourcebit. How can it help our content workflow with JAMstack sites? Drew McLellan speaks to developer Eduardo Bouças to find out.
description: >-
  In this episode of the Smashing Podcast we’re talking about an interesting open-source tool called Sourcebit. How can it help our content workflow with JAMstack sites? Drew McLellan speaks to developer Eduardo Bouças to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode of the Smashing Podcast, we’re talking about an interesting open-source tool called Sourcebit. How can it help our content workflow with JAMstack sites? I spoke to developer Eduardo Bouças to find out.

<iframe src="https://share.transistor.fm/e/d8cce66f/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [Sourcebit](https://github.com/stackbithq/sourcebit)
- [Video of Sourcebit in action](https://www.youtube.com/watch?v=BrZbWMXB4TQ)
- Eduardo on [Twitter](https://twitter.com/eduardoboucas) and [his website](https://eduardoboucas.com)

### Weekly Update

- “[Inspired Design Decisions: Neville Brody Design Cannot Remain Neutral](https://www.smashingmagazine.com/2020/03/inspired-design-decisions-neville-brody/),”
*by Andy Clarke*
- “[When You Find A Good Idea, Look For A Better One](https://www.smashingmagazine.com/2020/03/ideas-prototypes-tips-design-process/),”
*by Tony Kim*
- “[Why Are We Talking About CSS4?](https://www.smashingmagazine.com/2020/03/css4-pros-cons-discussion/),”
*by Rachel Andrew*
- “[Introducing Alpine.js: A Tiny JavaScript Framework](https://www.smashingmagazine.com/2020/03/introduction-alpinejs-javascript-framework/),”
*by Phil Smith*
- “[Avoid Keyboard Event-Related Bugs In Browser-Based Transliteration](https://www.smashingmagazine.com/2020/03/keyboard-event-related-bugs-browser-based-transliteration/),”
*by Sandamal Siripathi*

## Transcript

<p><a href="https://twitter.com/eduardoboucas"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34afccf1-3001-419b-80cf-9b2f5593d82a/eduardo-boucas-300x300.jpg" width="200" height="200" alt="Photo of Eduardo Bouças" /></a><span class="smashing-tv-host">Drew McLellan:</span> He’s a web developer, technologist, writer and occasional public speaker with a strong track record of working on open source projects. He works as a software engineer on the JAMstack site management platform, Stackbit, and develops open source tools such as Staticman, Speedtracker, and Sourcebit. So we know he’s an expert in the modern web platform. But did you know he’s deathly allergic to Wednesday? My Smashing friends please welcome Eduardo Boucas. Hi, Eduardo, how are you?</p>

<span class="smashing-tv-speaker">Eduardo Bouças:</span> I’m Smashing.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you today about a tool that I know you’ve been working on called Sourcebit. I know you do a lot of work both at the day job Stackbit, and personally in your own time, around sort of tooling with sort of what we now call JAMstack sites. So before we talk about what Sourcebit does itself, perhaps you can tell us a bit about the sort of scenario with the JAMstack site that might lead to somebody needing a tool like Sourcebit.

<span class="smashing-tv-speaker">Eduardo:</span> Sure. So to go back in time a little bit when I started using a static site generator. My first encounter with a JAMstack was with Jekyll, as I’m sure many people are as well. And when I started using Jekyll for my site, the authoring experience was a bit cumbersome. So it involved manually editing Markdown files on my local machine and then pushing them to get repo and then the thing would get integrated and built. And that’s still a workflow that exists today and that many people use and it makes sense for a lot of people in a lot of organizations. But, first of all, it doesn’t scale very well if you have like a larger team and especially if you have people from less technical backgrounds who may not be comfortable with Markdown or with using Git or with that whole pushing to a GitHub repo workflow.

<span class="smashing-tv-speaker">Eduardo:</span> And so it makes a lot of sense, in my opinion to couple a static site generator with what is now these days called a headless or a decoupled CMS. So if you come from a more traditional web development background where you might use something like WordPress, a headless CMS is something that behaves in a very similar way. So you still have this interface where you can author your content, and you have a nice WYSIWYG editor and media management and everything.

<span class="smashing-tv-speaker">Eduardo:</span> But the output of such a platform is not a fully formatted HTML page. And instead, the content is exported in a way in a format that is agnostic of any technology or any tech stack. And so that content is, it’s possible to integrate that content with your static site generator. And that’s why I think it makes a lot of sense to couple a headless CMS with a static site generator because you kind of get the best of both worlds in the sense that you get the performance, the security and the simplicity of using a static site generator, but at the same time, you still get kind of a rich authoring experience by using a nice editorial interface.

<span class="smashing-tv-speaker">Eduardo:</span> And even though it makes a lot of sense to couple those two tools together, it’s not particularly straightforward to integrate them. Especially if you’re using a more traditional file based static site generator, such as Jekyll or Hugo, where everything has to live as a file. So how do you take that content that lives in this headless CMS? And how do you translate that into files that your static site generator can understand and process?

<span class="smashing-tv-speaker">Eduardo:</span> As you said, I’m super passionate about creating tools for developers and particularly creating tools that allows developers to use the JAMstack paradigm with as little friction as possible. And that’s where source that comes in. That’s why I’m super passionate about this project in particular. So the idea is, that Sourcebit allows you to connect to any API based data source such as a headless CMS, you sort of tell it where your content lives, you help it make some sense of the structure of your content. And then Sourcebit takes care of sucking all that content down and writing it into the files with the formats into location static site generator is expecting. So that’s kind of the idea behind Sourcebit.

<span class="smashing-tv-host">Drew:</span> So rather than having authors work directly with markdown files, that your static site generator turns to a site, you’ve got your authors working with another tool, a headless CMS, maybe something like Contentful or even WordPress, and then Sourcebit is the bit in between that gets that content from where it’s been authored, and translates it in a way into a format that the static site generator can turn into a static site?

<span class="smashing-tv-speaker">Eduardo:</span> Exactly, yeah. And the way that it could, kind of see two different ways of using the tool that can help developers. One is making Sourcebit part of your deployment routine. So if you’re using a hosting platform like Netlify, for example, and you configure your deploy commands to be a Hugo build, is it the build command for Hugo or something said, so the command that generates the static files for Hugo, you would also have another command as part of that routine. That would be something like Sourcebit fetch. And so at build time, Sourcebit will go pull all the other data, generate all the files that Hugo needs. And then the whole deployment will already use those files and deploy all the content that is coming from the CMS. So that’s kind of one possible use case for Sourcebit.

<span class="smashing-tv-speaker">Eduardo:</span> The other one is to use Sourcebit in a local development workflow. So you can run Sourcebit with something that we call the watch mode. And so Sourcebit keeps looking for changes in the remote data source, so in this case, headless CMS. And so whenever you publish an article or you change an entry into CMS Sourcebit will acknowledge that and it will regenerate all the files for you locally. And so what that means for a developer working locally is that you can have your CMS window next to your Jekyll or Hugo site, running locally, and then you can see changes happening in real time. You change something on the CMS and then you can see that change being reflected on the local side, which I find super useful. So those are kind of the two ways that you could get use Sourcebit.

<span class="smashing-tv-host">Drew:</span> So I guess for all that to work Sourcebit has to know about both the system that the content’s stored in and the way that the static site generator needs the files organized in the file system. How do those two things work?

<span class="smashing-tv-speaker">Eduardo:</span> Sourcebit is a plugin-based architecture. So the idea is that you’re going to have different types of plugins that will accomplish different tasks. We have something that we call the source plugins, which are solely responsible for connecting to a data source like Contentful, for example, and they will connect to that data source, they will pull content and they will normalize that content into a format that is kind of agnostic of data source such that if you want to connect multiple data sources, so you’re using WordPress and Contentful, and Sanity, for example, all the content from those data sources will be normalized into a format that is kind of standardized across the board. So the responsibility of the source plugins will be to just that, to connect to a data source, normalize the content and put them into a bucket of data.

<span class="smashing-tv-speaker">Eduardo:</span> And then you have another type of plugin which we call a target plugin. And the target plugin has no knowledge whatsoever about where the data is coming from, but it knows about a particular piece of software that is expecting that data for example, you might have a target plugin for Hugo a target plugin for Jekyll. So the target plug in will be responsible for writing that data into specific format and the specific locations that the static site generated is expecting.

<span class="smashing-tv-speaker">Eduardo:</span> And then you might have other types of plugins that don’t know about the source and don’t know about destination. They’re just responsible for kind of massaging the data and doing all sorts of transformations in between. So that’s kind of the way that the tool is organized. And I think the benefit of that approach is that each plugin is only concerned about a specific area. So if you are, let’s say that you’re maintaining the source plugin for Contentful, you don’t ever need to worry about what static site generators will be supported. You just worry about maintaining that specific plugin that we take care of making sure that it can be plugged in into any combination of static site generators or different outputs that you want to use.

<span class="smashing-tv-host">Drew:</span> So is it possible to have multiple sources running at once and use a Sourcebit more like a content aggregator to pull them from lots of different sources at once?

<span class="smashing-tv-speaker">Eduardo:</span> Yes, yes, it’s totally possible. And that’s why we kind of use that principle of normalizing the data, because you might have as many data sources as you want. And then when a plugin comes in to kind of transform that data, it doesn’t really care where the data comes from, everything is treated the same. So it’s totally possible to do that. You can configure as many source plugins as you want. And so it’ll pull data from as many places as you want.

<span class="smashing-tv-host">Drew:</span> Yeah, that could be quite interesting. Could you think of a corporate website might have a blog in there, it might have copy from marketing, it might have job openings coming from an HR system. And you could potentially configure Sourcebit to pull that into one location before generating the site, which is quite an exciting prospect, I think.

<span class="smashing-tv-speaker">Eduardo:</span> Yeah, yeah. And CMS is are just one possible data source that you might use this tool with. For example, one of my colleagues that started was creating a source plugin that pulls data from Reddit, for example. And that’s just one very simple example of one possible data source. So as you say, it could get quite interesting because you might be pulling data from a CMS, might be pulling data from Reddit, Twitter or an HR platform and it just all comes down together nicely. So, yeah, it’s a possible use case for it for sure.

<span class="smashing-tv-host">Drew:</span> What sort of plugins exist at the moment for different sources?

<span class="smashing-tv-speaker">Eduardo:</span> So we launched the first kind of public version of the tool last week. And we launched with a two source plugins and two target plugins. So the source plugins are for Contentful and Sanity. And the target plugins are for Jacqueline and Hugo. We will keep working on your plugins internally at Stackbit. But our goal is for the community to eventually take ownership of the tool as well like this is a fully open source MIT license project. And so we would love to see people creating their plugins and building stuff with Sourcebit that we haven’t even thought of. So, that’s the ultimate goal. We’ve been in touch with people from different CMS companies who are interested in building their plugins as well. So we’re in constant contact with them. So hopefully we’ll see a nice ecosystem of plugins somewhat soon.

<span class="smashing-tv-host">Drew:</span> How complex is it to develop a plugin if you’ve got a completely custom system that you know that you need to integrate with? Is it a very involved difficult task to develop plugin or is it easier than that?

<span class="smashing-tv-speaker">Eduardo:</span> I’m a bit biased to answer that. I like to think that it’s simple and I’ve tried my best to make the process simple and also very well documented. So we have one of the repositories that we make available is kind of a sample plugin, where we have a fully annotated source code for a plugin. So we have comments on every possible function that you might implement outlining the arguments that it receives, how you can use this function to get data from this etc. So hopefully that’ll be a very useful resource. We also have documentation pages where we kind of outline the anatomy of a plugin, like how it pulls data where it’s supposed to push that into. So hopefully, it’s a fairly straightforward process.

<span class="smashing-tv-speaker">Eduardo:</span> But different systems will present different challenges. So I’m sure there will be suggestions and feature requests from someone in the community saying, "I want to integrate with this system. So I kind of need a way of doing this." And we’ll be more than happy to kind of accommodate those requests and kind of work with the community to make the plugin architecture better over time.

<span class="smashing-tv-host">Drew:</span> And it’s all written in, I presume is JavaScript node?

<span class="smashing-tv-speaker">Eduardo:</span> It is. It is.

<span class="smashing-tv-host">Drew:</span> I noticed that you mentioned earlier briefly that you can run Sourcebit with a watch flag, and it will help you to have a sort of live updating workflow. Is that something that needs to be implemented by the source plugin, or is that general system? Is it a polling mechanism or are you listening for sort of hooks and things from the source system?

<span class="smashing-tv-speaker">Eduardo:</span> The core application is very lean, and it’s not opinionated at all. So it’s up to each Source plugin to kind of implement that functionality. All the core application does on that front is it tells the plugin what are the kind of the options that the user asked for. So in the two plugins that we launched with, so we have one for Contentful, and one for Sanity, the way that the watch mode is implemented in each of them is very different. For example, in Contentful we have, as I mentioned, a polling mechanism in a regular interval of time, like poll for changes whereas for Sanity, we have like a running web socket that is constantly listening for changes and respond to the changes. But basically, the idea is that the source plugin implements its own listening mechanism and it’s responsible for telling the core application that I have new content please update yourself. That’s kind of the domain idea.

<span class="smashing-tv-host">Drew:</span> That sounds like quite a flexible system then that should cope with lots of different sources and different types of system.

<span class="smashing-tv-speaker">Eduardo:</span> Yes. I was just going to say like still on that topic of flexibility, one thing that I wanted to mention as well is Sourcebit is configured using a JavaScript file. So if something similar to what you would do with some like web pack, for example, although a bit simpler. And so you have the option to configure each of the plugins on that file manually. But we also offer this commandline interface, where basically each plugin is able to tell the core application the set of questions that it needs to ask the user in order to configure itself. So basically, when you run npx create-sourcebit, it can create everything from scratch for you.

<span class="smashing-tv-speaker">Eduardo:</span> So it pulls a list of all the available plugins to have the option to sit on a source plugin for Contentful and the target plugin for Jekyll, for example. And then based on the plugins that you choose, it then asks you a series of questions that will ultimately lead to a fully configured JavaScript file. So for example, for Contentful it’ll ask you for your credentials, like how do I access your Contentful account? And then it will actually pull all the content types from Contentful. And it’ll ask you okay, I found this content type called blog posts. What is this? Is this like a page? Is this a data object? And if it’s a page, where should I store this? What kind of fields should I use for the layout for the content?

<span class="smashing-tv-speaker">Eduardo:</span> I think it’s a very user friendly way of configuring the whole project. So hopefully, by the end of this configuration process, you can just run a command and you can pull the content straight away without having to mess around with JavaScript files.

<span class="smashing-tv-host">Drew:</span> So that configuration process answering those questions, then writes the JavaScript configuration file for you, which you can then presumably just commit into your source control and distribute to other developers on your project or into your build process for running live. You mentioned a third type of plugin distinct from the source and the target that works on data in this agnostic format in the middle. What sort of scenarios do you imagine that being used for?

<span class="smashing-tv-speaker">Eduardo:</span> We created a plugin that is responsible for transforming assets. So to give you an example, let’s say that I’m using Contentful, and you have images embedded as part of a blog post. And by default, if you just pull that data from Contentful, the images will be using a live URL from like Contentful CDN which is a totally viable option if that’s what you want to use. But you might want to instead, serve the images alongside the content. So have them in your repo and served from whatever service you’re using to serve to site as well. And so that plugin in specific, it will look for any assets that are using, it will pull those assets down, download them basically to your repo or to your local file system which it can then push.

<span class="smashing-tv-speaker">Eduardo:</span> And it will replace any URLs in your files that reference that remote URL, it’ll replace those with references to the local files instead. So basically, when you push the site, you push the content and the assets and everything will just work seamlessly. So, that’s one example of kind of a transformation plugin that is not pulling. It’s not specific to a data source and it’s not specific to a static site generator. It just transforms things in between.

<span class="smashing-tv-host">Drew:</span> You mentioned that there are target plugins for Jekyll and Hugo, are there any that you’re expecting to see in the near future?

<span class="smashing-tv-speaker">Eduardo:</span> Well, I’m a big fan of Eleventy. So I’m really hoping to see an Eleventy plugin coming out fairly soon. And then I guess there are some static site generators that already have their own kind of plugin ecosystem. So I’m curious to see if people will still find a need to have a source plugin for those types of static site generators. Like another possible way that you can use Sourcebit by the way, is if you’re using something like Next.js, so like any node based static site generator. You don’t necessarily need a target plugin, you can just require Sourcebit as an NPM module, and you can run the all the mechanisms for fetching data. You can just run those as in memory functions and get your content available as part of your Next.js pages. To answer your question, I guess for those we won’t see target plugins specifically, but we can already use Sourcebit in that way. In terms of next source plugins, I would expect to see Eleventy and maybe a few other kind of file based static site generators in the near future.

<span class="smashing-tv-host">Drew:</span> This is all quite exciting stuff, I think. Is it just you working on it in terms of development or is there a bigger team?

<span class="smashing-tv-speaker">Eduardo:</span> I’ve been kind of the main developer working on it, but it’s a team effort. So it’s something that a bunch of people at Stackbit identified as a problem. And we’ve been working together on kind of specification and the right way to approach this. I just happen to be the guy pressing the keys to make it happen.

<span class="smashing-tv-host">Drew:</span> And I guess Sourcebit actually can be very useful for Stackbit customers, which is Stackbits motivation for developing and contributing this but obviously, it’s going to be useful to a much wider audience than just Stackbit customers.

<span class="smashing-tv-speaker">Eduardo:</span> Yeah, we have big plans for Sourcebit internally. It’ll really help us achieve our mission in terms of making JAMstack, accessible to as many people as possible, but we wanted to make sure that we share this particular project with the community because we feel that it’ll help a lot of people regardless of whether they’re interested in using Stackbit or not. So that’s why it’s a fully open source project.

<span class="smashing-tv-host">Drew:</span> That’s great. Is there anything else you’d like to tell us about Sourcebit?

<span class="smashing-tv-speaker">Eduardo:</span> No. I would just love people to try it out. I’m sure we can share links to like the repo and stuff like that. There’s a YouTube video in the main repository, that shows how the experience is like when using Sourcebit with a headless CMS and a static site generator. So it kind of gives you an idea of what it’s like to use the CLI and the whole interactive setup process, and I would just love people to try it out. And get in touch if they think it could be improved or it’s terrible, or it’s great, or it’s helping them. So yeah, I would love to hear from people.

<span class="smashing-tv-host">Drew:</span> That’s great. We’ll link that all from the show notes, but also Sourcebit be found at github.com/stackbithq/sourcebit. So I’ve been learning all about Sourcebit today, what have you been learning about lately?

<span class="smashing-tv-speaker">Eduardo:</span> I’ve been super interested in learning about Serverless. And I’ve actually been trying to learn as much as possible about it for the past few months. It’s a concept that I’m super interested in. It’s one of those seismic changes in how you approach development. And I’m super interested in kind of the use cases that it has and kind of the different ways of rethinking how you build an application for Serverless. So that’s something that I’ve been trying to read about as much as possible and just playing around and trying, like side projects. Yeah, it’s an area I’m super passionate about.

<span class="smashing-tv-host">Drew:</span> It’s very interesting, isn’t it? Quite a shift in how you have to think about projects?

<span class="smashing-tv-speaker">Eduardo:</span> Definitely, definitely. There’s a metaphor, and I don’t want to ramble about Serverless here, which is that a metaphor that I think is really helpful is to think about Serverless as kind of using Uber as opposed to owning a car, like it forces you to, you still have a car, like the term Serverless maybe is a bit misleading because you still have a server, but if you have a car, you might just leave your stuff in the car because you know it’s going to be there the next day, whereas if you’re using at Uber, it forces you to rethink and to acknowledge that every day you’re going to get a new car with different people driving it, and it just have to adapt your way around that fact. So, that metaphor really helped me wrap my head around the whole Serverless paradigm.

<span class="smashing-tv-host">Drew:</span> Yes, I had not heard that before, that’s quite an interesting way of looking at it. If you, dear listener, would like to hear more from Eduardo, you can follow him on Twitter, where he’s @Eduardoboucas. And you can find his web development periodical build times at Eduardoboucas.com. Thanks for joining us today. Eduardo. Do you have any parting words?

<span class="smashing-tv-speaker">Eduardo:</span> No, not really. Just first of all, thank you so much for having me. It’s been a pleasure. And by the way that weird pronunciation for my last name, maybe I should say that it's, if you want to find my Twitter handle and website the surname is B-O-U-C-A-S. Boucas is another weird Portuguese pronunciation if you want to find, it’s Eduardoboucas. So, yeah, thank you so much for having me. It’s been a pleasure.

<span class="smashing-tv-host">Drew:</span> Thank you so much.

{{< signature "dm, ra, il" >}}
