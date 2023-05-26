---
title: 'Smashing Podcast Episode 29 With Leslie Cohn-Wein: How Does Netlify Dogfood The Jamstack?'
slug: smashing-podcast-episode-29
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80d0a370-c369-4cb6-a6ba-8af572c66bc3/smashing-podcast-episode-29.png
date: 2020-11-17T05:00:00.000Z
summary: >-
  We’re asking what it looks like to dogfood the Jamstack at Netlify. Can you deploy an entire app to a CDN? Drew McLellan talks to Netlify Staff Engineer Leslie Cohn-Wein to find out.
description: >-
  We’re asking what it looks like to dogfood the Jamstack at Netlify. Can you deploy an entire app to a CDN? Drew McLellan talks to Netlify Staff Engineer Leslie Cohn-Wein to find out.
categories:
  - Smashing Podcast
  - Jamstack
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re asking what it looks like to dogfood the Jamstack at Netlify. Can you deploy an entire app to a CDN? Drew McLellan talks to Netlify Staff Engineer Leslie Cohn-Wein to find out.

<iframe src="https://share.transistor.fm/e/128bfb76/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- Leslie’s [personal site](https://leslie.dev)
- Leslie [on Twitter](https://twitter.com/lesliecdubs)
- [Netlify](https://netlify.com)

### Weekly Update

- [A Dive Into React And Three.js Using react-three-fiber](https://www.smashingmagazine.com/2020/11/threejs-react-three-fiber/)  
*written by Fortune Ikechi*
- [Best Practices For E-Commerce UI Design](https://www.smashingmagazine.com/2020/11/best-practices-ecommerce-ui-design/)  
*written by Suzanne Scacca*
- [Authenticating React Apps With Auth0](https://www.smashingmagazine.com/author/nefe-emadamerho-atori/)  
*written by Nefe Emadamerho-Atori*
- [From The Experts: Global Digital Accessibility Developments During COVID-19](https://www.smashingmagazine.com/2020/11/global-digital-accessibility-developments-during-covid/)  
*written by Robin Christopherson*
- [What’s New In Vue 3?](https://www.smashingmagazine.com/2020/11/new-vue3-update/)  
*written by Timi Omoyeni*

## Transcript

<p><a href="https://twitter.com/lesliecdubs"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/192022ad-300a-4e8e-bb4d-626100fcb5fc/leslie-cohn-wein-250x250.jpeg" width="200" height="200" alt="Photo of Leslie Cohn-Wein" /></a><span class="smashing-tv-host">Drew McLellan:</span> She’s an award winning frontend specialist originally from Austin, but now living in Dallas, Texas, via a stint in New York city. During that time working for agencies, she built sites for clients, such as Nintendo, WorldPride, and Jerry Seinfeld. She’s now a staff frontend engineer at Netlify, where amongst other things, she works at building out the application customers use to manage their service and deployments. So, we know she’s an accomplished frontend engineer, but did you know, when living in New York city, she served as an assistant chili cook-off judge three years in a row. And that one’s actually true. My smashing friends, please welcome Leslie Cohn-Wein. Hi, Leslie. How are you?</p>

<span class="smashing-tv-speaker">Leslie Cohn-Wein:</span> I’m smashing.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you today about how Netlify sort of eats its own dog food, to use that charming expression, when it comes to building on the Jamstack. I should put this in context a little bit by saying that up until a few months ago, we worked together on the same team at Netlify. And when I got there, the development process was actually really foreign to me, even after 20 years as a developer. I thought it was just really fascinating and well worth exploring a bit, with a wider audience. I should probably point out that we’re talking about this because it makes a genuinely interesting case study and it’s not a sponsored big ad for Netlify. Everyone should check out Vercel. But I think there’s a lot of valuable things that can be learned from discussing it, particularly from a Jamstack point of view. Because Netlify is a really big proponent of the Jamstack approach and the service is sort of offered to the customer and is built around that idea of building Jamstack projects. But the service is also built using those principles itself. Isn’t it?

<span class="smashing-tv-speaker">Leslie:</span> It is, yeah. A lot of people sort of think of that Jamstack architecture as static sites, but we’re really dogfooding what it means to build a Jamstack app with the Netlify frontend. Because it’s a React app that is a full Jamstack app that we deploy Netlify on Netlify so... Yeah, we’re really trying it out and pushing the limits of what’s possible.

<span class="smashing-tv-host">Drew:</span> I think there’s sometimes this idea that Jamstack is great for just static sites, as you say, and the API aspect comes in if you want to send a form to an email address and you can just do something easy like that, but you can possibly build a whole web app that way. But, you are doing that aren’t you?

<span class="smashing-tv-speaker">Leslie:</span> Yeah, absolutely. Our app, talking specifically about what you see you if you login at app.netlify.com, is powered by... we’ve got an internal REST API, but the frontend, like I said, is pure Jamstack. So, we have our own build step, we watch the app as it builds in the app, and we deploy on our own system.

<span class="smashing-tv-host">Drew:</span> So, when there are a backend process involved, and there’s always going to be some sort of level of backend processes, you know, persisting data or, in Netlify’s case, starting off with a deployment or what have you, that backend just kind of gets built as a series of APIs that can then be consumed by the frontend?

<span class="smashing-tv-speaker">Leslie:</span> Yeah, so there’s a couple of different models of how you can make this work. In most cases, in our app, we use client-side fetching with React, right? So, we serve sort of a static shell of the app and then we fetch the user’s information from our internal REST API at the request time. Jamstack is interesting because there’s some things you can pre-build, and we try and rely on that when we can. And then when we’re talking about some of the more dynamic data, we’ll use that client-side fetching in order to make sure that we’re pulling in the freshest data.

<span class="smashing-tv-host">Drew:</span> I think it surprised me, when I started working on the app, just how much is being achieved in the frontend, particularly when it comes to interacting with external APIs and things. I know that when Netlify interacts with your Git provider, so it goes to GitHub and gets a list of list of repos, that’s all happening between your browser and GitHub. And apart from maybe the... going through a server-less function that’s putting some secrets on the request or something lightweight like that, most of that is just happening in a Jamstack-y sort of way. It’s not going through a Netlify sort of core backend infrastructure. So, that’s quite fascinating. That really is going so much further beyond just a static site with a few API calls to do little things. That’s that real core functionality, isn’t it, that’s being implemented in the browser?

<span class="smashing-tv-speaker">Leslie:</span> Absolutely. It really pushes, I think, that concept of what a frontend developer engineer is, right? And it’s something that pushes me, as a frontend engineer to be better and to think more about those sorts of... the API layer, which is not something that I’ve traditionally have been as close to. I work more in UI and colors and design systems, and so it really... I actually have found that working on a Jamstack app at scale, has pushed me to be a better developer.

<span class="smashing-tv-host">Drew:</span> Being a frontend developer isn’t knowing CSS back to front, although that’s part of it. It is not knowing HTML back to front, but though that’s part of it. It’s also straying into this territory that was traditionally the preserve of a backend engineer, which is quite interesting. Does Netlify use new server-side rendering for-

<span class="smashing-tv-speaker">Leslie:</span> Not that I’m aware of.

<span class="smashing-tv-host">Drew:</span> So, it’s all just literally done, as you say, you serve a shell, and then it gets populated with requests back to different API end points to sort of populate it all.

<span class="smashing-tv-speaker">Leslie:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> And you say it’s a React app?

<span class="smashing-tv-speaker">Leslie:</span> Yes. Yes. React. We use React Redux right now, and right now we’re PostCSS, but we’re experimenting with our CSS architecture as well.

<span class="smashing-tv-host">Drew:</span> Aren’t we all? So, you build the app in React and then you deploy it on Netlify?

<span class="smashing-tv-speaker">Leslie:</span> Yes. Maybe my favorite part of that whole process is the magic of Deploy Previews, which we get through Netlify. So, what happens is, you’ll... you’re working in GitHub, you push up your PR. So, you open up your PR in GitHub, and that is going to automatically create a build of your Deploy Preview of the app. So, we actually use Deploy Previews of the app itself to test out, to make sure everything is working the way it should. We run our tests. That’s what we use to manually verify during code review. So, we have sort of all of that continuous deployment set up right from GitHub.

<span class="smashing-tv-speaker">Leslie:</span> And then one of the other cool things that we have set up is that we actually have a couple of different Netlify sites that are pulling from the same repository where our app lives. So, we have both our app, we’ve got an instance of Storybook that has sort of our UI components for the app. So, we have both our app itself, we’ve got the Storybook UI components, and we have basically a Netlify site that shows our Storybook UI. And then we also have a third site that runs a webpack bundle analyzer. So, it’s a visual UI that gives you a tree map, visualization of all of the apps bundles, and we can sort of gauge their size, and it’s just a reminder for us to double-check sort of. As every deploy of the app goes out, we can check and make sure we’re not doing anything weird with our bundle size there. So, all three of those sites get generated in one Pull Request of the app. So, you’ll get links to preview, your Deploy Previews essentially, of both the app Storybook and to that app profile for us to check through.

<span class="smashing-tv-host">Drew:</span> And with the Deploy Previews, that essentially kind of becomes your staging environment, does it?

<span class="smashing-tv-speaker">Leslie:</span> Exactly. We don’t really run a traditional staging environment, because we really trust that our Deploy Previews are essentially what is going to go live when we hit that merge button and kick off the official build of our main branch in our main app. So, I love that we can rely on Deploy Previews as the staging environment. We really trust that it’s going to match production. We’re building it with all of the production variables, everything that... environment variables, all of that stuff gets built in the Deploy Preview. So, it’s pretty much like a no worry situation. As long as your Deploy Preview is working, you know that the app is going to work as well.

<span class="smashing-tv-host">Drew:</span> And I guess, as an organization, if your Deploy Preview isn’t matching what gets put live, then that’s a service issue that Netlify wants to resolve. So, it actually works out quite nicely from that point of view. So, you’ve reviewed a Deploy Preview, everything looks great, the PR gets merged. What happens then?

<span class="smashing-tv-speaker">Leslie:</span> So, because Netlify runs all of our continuous deployment, essentially we have it all hooked up so that any merge into our main branch will automatically kick off an official production deploy with the app. So, typically if you’re the developer who has merged your own PR, you’ll pop into the actual... you have to make sure, double check your tabs, because if you have a Deploy Preview of the app open and the app, you got to make sure... you usually want to follow along in the real app. So, you got to check your tab. But, yeah, in the app, you usually go in, you can watch the build logs for that merge that you just kicked off, so it’s all automatic. And then as soon as those build logs complete, and the site is live, all you have to do is refresh your browser window and you’ll see whatever you had just deployed, should be updated in the app.

<span class="smashing-tv-host">Drew:</span> And let’s say you catch a problem once it’s gone live, what do you do then?

<span class="smashing-tv-speaker">Leslie:</span> That’s a very good question. And maybe one of my favorite things about using Netlify even before I worked at Netlify, this was like a little bit of magic to me, because Netlify has sort of baked in, what we call, rollbacks. So, essentially every deploy on Netlify... because we’re using this Jamstack architecture, every deploy is atomic. So, what that means is you have this full history of every sort of deploy you’ve ever made on a site, and you can instantly roll back to any one of those. So, if we accidentally deploy a bug or something is broken, the first thing that we usually do is we actually stop that continuous integration. So, we’ll go in and it’s just one button in the Netlify UI that you say, "Stop auto publishing," and what that will do is it stops that connection with GitHub. So, if my teammate is suddenly also merging their PR, we’re not going to re-introduce the bug, nothing like that is going to happen.

<span class="smashing-tv-speaker">Leslie:</span> So, we stop all those auto deployments. And then all I have to do is go back into my deploys list and find the last working deploy, hit one more button that says, "Publish this one," and it goes live. So, what that does, is it takes that pressure off to be able to really go back, look at the code, figure out what actually happened. Sometimes that means doing a Git revert on your main branch and getting the main branch back where it needed to be. And sometimes it’s a hot fix or you go off on a branch and you get it fixed and you don’t really even need to worry about reverting in Git. And then, when you’re ready to go back, you make sure everything’s working on your Deploy Preview of the app, and you can just reset all that stuff back up. So, as soon as you start those auto deployments, you’re basically back in business.

<span class="smashing-tv-host">Drew:</span> So, I’ve spotted a problem here.

<span class="smashing-tv-speaker">Leslie:</span> Uh oh.

<span class="smashing-tv-host">Drew:</span> You’re using Netlify to deploy changes to the Netlify app. What if the bug that you’ve deployed stops you rolling back? What do you do then?

<span class="smashing-tv-speaker">Leslie:</span> I have nightmares. No. Actually, we have a couple of ways that could handle that. So, if we take down the app and we can’t use the UI to go through this process, our Deploy Previews actually run against our production API. So, what that means is, even if the app isn’t working, we still have those atomic deploys. So, if you have a link from GitHub, perhaps from an old or recent PR, and you have that Deploy Preview URL, you could actually access the Deploy Preview of the app and make whatever change you need, go back and publish an older deploy from the Deploy Preview. And it’s still hitting our production API, so that will still affect the app, and then that will bring the app back up. It’s like sort of exploding brain emoji there, but it’s one way to do it. We could also publish an older deploy from some of our backend systems. We could get our backend engineers to publish that for us. Or you can always use Git to revert and try and push that up, but it’s a little bit scary because you can’t watch what you’re doing.

<span class="smashing-tv-host">Drew:</span> I guess you just need a very clear mind to manage that situation.

<span class="smashing-tv-speaker">Leslie:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> But it’s totally recoverable from, it sounds like it.

<span class="smashing-tv-speaker">Leslie:</span> Yeah. Well, and once you’ve published your working deploy, all the pressure’s off. That’s really the nicest part. And I found this working in agencies as well. Being able to roll back was really a lifesaver to... It also makes you less worried about publishing new changes. If you break something, it takes a second to roll it back, which fits very nicely with the sort of move quickly and get things out model.

<span class="smashing-tv-host">Drew:</span> Definitely. I think typically this sort of whole workflow works best when you’re dealing with really small changes. I mean, ideally you want to create a branch, implement a small change, raise a PR, and then get that merged back as quickly as possible. Which obviously works fine for tweaks and bug fixes and little things, but it doesn’t work so well for major feature work when that feature might take weeks or maybe even months from it starting to it being ready to deploy. How do you manage that sort of process?

<span class="smashing-tv-speaker">Leslie:</span> Yeah, that’s a great question. So, we’ve recently started using feature flags a little bit more. Before I go talk a little bit more about how we do that, I’ll talk about what we used to do. So, before we were using feature flags, I think everyone’s sort of familiar with the idea of the long running feature branch. We all sort of hate them, right? But we would work on our smaller PRs. We would merge each of those individually, after code review, into this longer running feature branch. So, you would just basically have all of your new feature in one place, you could have one Deploy Preview that you can test that new feature with. Sometimes this model sort of required coordinated deployments across other teams. So, when we were ready to say, "Okay, this feature branch, we’re ready to merge it and get it live," occasionally that meant, "Okay, you got to make sure backend’s already deployed their change," so whatever API work that we’re doing in our feature is ready to go. If there are docs on our doc site that need to go live at the same time as the feature, you sort of have to coordinate and hit the buttons at the same time.

<span class="smashing-tv-speaker">Leslie:</span> This model is... it worked for us, but you’re right, that it wasn’t maybe the smoothest. It’s actually sort of funny, our co-founder and CEO at Netlify, Matt Biilmann, actually launched our analytics feature using this process onstage at Jamstack Conf London last year. So, he used our lock deploys feature to basically take the Deploy Preview of the new feature of analytics and publish it live on stage. So, that was pretty cool.

<span class="smashing-tv-speaker">Leslie:</span> But, like you said, it’s... you have a little less confidence. Everything is still sort of hidden in this Pull Request. It becomes a bit unwieldy. Someone has to approve that final Pull Request that usually is quite large. That’s a little overwhelming. So, nowadays we’re mostly using feature flags. We use a service called LaunchDarkly, which lets us basically wrap our new feature UI with these flags, so that we can keep continuously merging code, even if the UI isn’t something we want customers to see. So, you just make sure in the production environment that your feature flag is off, we can deploy the code, merge it, and no one... assuming that you’re a general user, you’re not going to see that new UI.

<span class="smashing-tv-host">Drew:</span> So, a feature flag is basically just like a switch in the code that says, "If this feature is enabled, use this new code, otherwise use this old code."

<span class="smashing-tv-speaker">Leslie:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> Does that mean that you get sort of a messy code base with all these forks in place? How do you deal with that?

<span class="smashing-tv-speaker">Leslie:</span> Yeah, I think that’s... anyone who uses feature flags probably is used to this sort of battle of when do you clean up the feature flags? How long do you leave them there? We’ve sort of landed on about two weeks after a major feature gets released, is we have reminders. Luckily, LaunchDarkly actually recently set up a feature that will notify Slack. So, you can hook it up with Slack, and it’ll just tell you, "Hey, your feature flag has been... You’ve been live in production for two weeks. It’s about time to go make sure you clean up your flag in the code."

<span class="smashing-tv-speaker">Leslie:</span> So, we do try and, and clean it up pretty quickly, but it is, in that time in between, it is nice to know the flag is still there. Even if you’ve released the feature, it means that again, with one click, you can go in and toggle that flag back off it there is a bug, if there is something that pops up. So, we like to leave them in for a little bit, just while the feature is really baking, while people are getting used to it, to make sure there aren’t any major issues. But then we do try and go back into the code and it is a bit of cleanup, so it’s not an ideal process, but usually removing the flag doesn’t take very long, you’re just deleting a couple of lines of code.

<span class="smashing-tv-host">Drew:</span> So, I guess the simplest approach to implementing a feature flag could just be a... like a config variable in your app that says, "This feature is on or off," but then you, you need some way to make sure that it’s on for the right people and off for the right people. And I guess that’s where a service like LaunchDarkly comes in, because it takes that... I mean, it takes basically what is switching on and off a variable to an extreme level, doesn’t it?

<span class="smashing-tv-speaker">Leslie:</span> Yes. Yes. That’s exactly it. So, there are ways we could have, even without LaunchDarkly, basically set up a config variable ourselves that we sort of manage on our end. One of the things I love about LaunchDarkly is that there are different environments. So, what we can do is essentially turn on a feature flag for our Deploy Previews. So, anyone who’s viewing internally at Netlify, a Deploy Preview of the app can have access to the new feature, can test it out, but then again, as soon as it goes live in production, that flag is off. So, there’s very little... again, you sort of have to check your tab and make sure you’re aware of sort of what segment you’re in, because you don’t want to surprise yourself and think you’ve launched something that you didn’t, you have to be a little bit careful there. But, in general, it works quite well, and LaunchDarkly lets you also do these selective rollouts. So, you can roll out a feature to some percentage of your code base or to a specific user segment, people with a specific type of plan or a specific type of user. So, it allows you a lot more control over who you’re sort of releasing to.

<span class="smashing-tv-host">Drew:</span> Yeah. That can be really powerful, I guess, particularly with new features or features that you might be expecting to resolve an issue. Maybe you’re enhancing a feature to make it more understandable, you can maybe try it with 10% of the users and see if they’re experiencing the same problems and...

<span class="smashing-tv-speaker">Leslie:</span> Exactly. It’s a great way to get feedback as well, yeah.

<span class="smashing-tv-host">Drew:</span> I guess using LaunchDarkly in this way, rather than rolling your own solution, is kind of another aspect of the Jamstack approach, isn’t it? It is just using an API that gives you this functionality without having to worry about how you implement that yourselves and how to develop that and how to maintain it and keep that so that you can just outsource it, say, "Right, we’re going to use this API and everything else is taken care of."

<span class="smashing-tv-speaker">Leslie:</span> Yep. Yep, exactly.

<span class="smashing-tv-host">Drew:</span> So, this approach enables you to be committing small bits of new features to production essentially, but they’re just sort of hidden behind the flag. And then when everything is ready to go, you can just flip the flag and you can quickly switch it back again if something goes wrong.

<span class="smashing-tv-speaker">Leslie:</span> Yep, exactly. It makes our launches a little bit less exciting. It used to be you’re pressing these big buttons and there’s all this code that’s getting merged and you’re watching your build logs and it’s this moment of anticipation. And now it’s you hop on a Zoom call, you click one button, and it’s live.

<span class="smashing-tv-host">Drew:</span> Yeah. I think the last feature launch, I worked on an Netlify, we used this approach. And it had been weeks of work for a whole team of people, and we got on a Zoom call to coordinate the release, and everyone confirmed that their parts were ready. And then I flipped the feature flag and turned it on for all users, and that was it.

<span class="smashing-tv-speaker">Leslie:</span> Done.

<span class="smashing-tv-host">Drew:</span> And it was over in a few minutes and it was really anticlimactic.

<span class="smashing-tv-speaker">Leslie:</span> Yeah, it’s sort of sad.

<span class="smashing-tv-host">Drew:</span> There was no sweaty palms, there was nothing, which of course is exactly what you want, isn’t it? That’s how you know you’ve got a robust process, if turning something on for everybody is just not a big deal.

<span class="smashing-tv-speaker">Leslie:</span> Exactly. And if you got to roll it back, again, it’s just that simple, it’s that one click. It relieves some of that pressure, anxiety.

<span class="smashing-tv-host">Drew:</span> So, presumably, I mean, not all changes are going to be just frontend changes. Sometimes there are going to be backend changes, and presumably they have their own feature flags as well in most backend systems. So, you mentioned docs as well. Is there a way to coordinate all of this together? Does everybody just flip their flags at the same time? Or how does that work?

<span class="smashing-tv-speaker">Leslie:</span> Yeah. So, this is an area that we’re sort of actively working on across the teams right now at Netlify, is working towards a solution that would allow us to perhaps tie everything to one single flag in LaunchDarkly, that all of our systems are using, all of our code bases are using. So, in an ideal world, we would be able to flip a flag and say, "Okay, this is toggling on the new API end point that is also being consumed on the frontend with this new UI that is wrapped in a feature flag, as well as this portion of the doc site, that has new information about this new feature." And you flip that one flag in it impacts all of those repositories. We’re not quite there yet. We’re working through that, but I’m excited to see sort of if we’re able to get all of that coordinated and working.

<span class="smashing-tv-host">Drew:</span> Netlify, as a service is very much sort of tailored to building sites in this way. Does the work that you and your team are doing using the product, actually influenced the product development at all?

<span class="smashing-tv-speaker">Leslie:</span> I’d say that it definitely does. Everyone always says you are not your user, which I think is true most of the time, except sometimes when you are your user. Which is funny at Netlify because I think most of the people on the frontend team in particular, are people who have used Netlify before as a product. And certainly because we’re using Netlify to deploy Netlify we run into the same challenges that I think some of our users do. So, in some ways, if we run into a problem, we’ll try and bring it up to the rest of the company. We’ll mention it in an engineering call or we’ll pull in our CTO and say, "Hey, this is something that we’re struggling with. Is there something we could build into the product that would make this easier for us and for all of our users who are deploying similar things that we are?" So, it’s sort of a unique position to be in, but it’s fun to see how the product roadmap gets developed.

<span class="smashing-tv-host">Drew:</span> I guess there’s probably few people out there using Netlify quite as intensively as Netlify does itself.

<span class="smashing-tv-speaker">Leslie:</span> Yeah. Yeah. I think that’s about right. I stare at Netlify both when I’m building it and when I’m deploying it, so I’m pretty familiar with it.

<span class="smashing-tv-host">Drew:</span> And then at the weekend you work on a side project and you find yourself back in Netlify again.

<span class="smashing-tv-speaker">Leslie:</span> Yeah. That’s actually very true. Yeah. Yes. yes, indeed.

<span class="smashing-tv-host">Drew:</span> Do you have any examples of like how the product direction has been influenced at all by the work that the team’s done?

<span class="smashing-tv-speaker">Leslie:</span> Yeah. So, we’ve pretty recently launched a new sort of landing dashboard for the app that we’re calling The Team Overview. So, it used to be when you logged into Netlify you’d land on the site’s page, which would just basically be a long list of your sites. And we wanted to give people a little bit more of a mission control area where they can sort of see a lot of important information at a glance, get access to things that are going to be most useful to them. And so, that was a new feature that we built. In the initial iteration, we’re trying to get it out quickly, we have a little card on that UI that links to your latest builds. It shows you any build across your whole team, should show up in that card.

<span class="smashing-tv-speaker">Leslie:</span> And at first, we actually hadn’t linked those up to the build... the display log itself. So, it was just a list where you could check it out. You could click into the builds page to get a sort of similar view. But I was actually working on something over the weekend, a personal site, and I had this team overview turned on and I was annoyed because I realized I logged into Netlify and I wanted to go check out this build that was happening of my project, and I couldn’t just click on it and get right to it. I had to click into the builds page and then click again. So, the next day at work, I went in and added that change and linked up those builds because it was bothering me. So, that was one example of sort of just realizing by using the product, that there was a very small opportunity to improve it. And we took that.

<span class="smashing-tv-speaker">Leslie:</span> But we do have some other examples, too. Probably a little bit more impactful. One is that we sort of added this form detection feature. So, a little bit of background, if you’re not familiar, Netlify forms is a feature in Netlify that lets you build a frontend form. And Netlify sort of does all the backend work of managing submissions. It’s sort of like your database for your form that you’ve built on your frontend. It means you don’t have to write any server-side code or a whole lot of extra JavaScript to manage form submissions. Really any site that you deployed to Netlify, as your build is happening, our build bots are parsing your site’s HTML at deploy time to basically detect if you’ve got a Netlify form that Netlify needs to pay attention to and manage. And this form detection, the build bot’s looking for that, is enabled by default.

<span class="smashing-tv-speaker">Leslie:</span> But what that means is that, as you can imagine, that eats up a little bit of your build time because the bots have to go and look for this extra step. So, the Netlify app itself, actually, we’re not using, we don’t have any Netlify forms on the app right now. So, this is a step that basically is adding a little bit to our build time, but it doesn’t necessarily need to happen. So, Netlify actually built a new feature that allows any user to disable that form detection. What that means is you can turn that setting off in your site settings, the build bots realize that there’s nothing they need to look for, so you save that little bit of extra processing time in the builds.

<span class="smashing-tv-host">Drew:</span> I guess that’s great in terms of productivity, because things just complete a little bit quicker.

<span class="smashing-tv-speaker">Leslie:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> But also, as a metered service, enables you to get more out of the sort of allowances that you’ve got.

<span class="smashing-tv-speaker">Leslie:</span> Yep. Exactly. And so, this was something that we also heard from some of our users and customers, and it was something we sort of noticed as well. It was, "Well, we don’t need this extra step in our own product. So, is there a way, something we could give to all of our users to make everyone’s life a little easier, make everyone’s build a little faster if they’re not using this feature?"

<span class="smashing-tv-host">Drew:</span> Is there a danger... I mean, you say that you’re not your user, but with Netlify you often are your user. Is there a danger that, with the intensity that you use the product, that you might overlook the sort of users who are only using it very lightly and everything might get too complex and too advanced, and it’d just become very difficult to get started with?

<span class="smashing-tv-speaker">Leslie:</span> That’s that’s a great question. We also have really built out our user research function at Netlify and our data science function, and I think, overall we trust them a lot more than my anecdotal experience using and deploying the app. But I think all of that data sort of comes together to allow us to get a better picture of who’s using Netlify, what type of user are we speaking to? There are people with different types of needs. We’ve got folks on our starter teams who are managing blogs and personal sites, and we’ve got huge enterprises as well, who are launching big marketing campaigns and big web apps, not so dissimilar from Netlify itself. So, it’s exciting to sort of see the user base grow and to think about all these use cases and to figure out how we can cater to all of those users. And certainly using more of our research functionality to lean on understanding who those users are, not just our internal experience.

<span class="smashing-tv-host">Drew:</span> Tell me, Leslie, about the screenshot service that Netlify has in place? Because I found that really interesting.

<span class="smashing-tv-speaker">Leslie:</span> Yeah. In the UI we have... when you deploy a site on Netlify, in the UI, we have a little screenshot that shows you typically what the homepage of the site you felt looks like. It’s actually funny we brought this up, because I was listening to Chris Coyier his episode on Serverless not so long ago, and he was talking about how they do screenshots in CodePen as well, which is actually not so dissimilar to how Netlify does it. But basically we run Puppeteer to capture that screenshot of the user site, and the way that it’s all run is that it’s set up with a Netlify function. So, this is again, an example of us dogfooding our own product. So, essentially we use this end point that is a Netlify function inside our own app to return the URL of that image of the screenshot, that then we can serve that up in the app.

<span class="smashing-tv-host">Drew:</span> So Netlify functions are Netlify’s implementation of a Serverless function, aren’t they? Where you basically just drop a JavaScript file into a designated folder as part of your source, and then that becomes available to be executed as a cloud function.

<span class="smashing-tv-speaker">Leslie:</span> Yes, exactly.

<span class="smashing-tv-host">Drew:</span> Super smart, isn’t it?

<span class="smashing-tv-speaker">Leslie:</span> Yeah. It’s brilliant. This is one of those areas where it really pushes me as a frontend engineer to really be more of this JavaScript or Serverless engineer, and think a little bit more about how you’re basically writing like an internal API end point for yourself when you create one of these Serverless functions. So, it’s exciting because there’s so much you can do, but that can make it a little intimidating also because there’s so much you can do.

<span class="smashing-tv-host">Drew:</span> I sort of find it funny how it’s like... that’s seemingly a core piece of functionality for Netlify, displaying images alongside your site of what it looks like, yet, it’s just implemented with another Netlify feature. And you wonder how far you go before it all disappears in on itself in a big cloud of smoke.

<span class="smashing-tv-speaker">Leslie:</span> Yeah. Yeah.

<span class="smashing-tv-host">Drew:</span> This sounds like a really nice way to be working, and a very modern way to we’re working, but it can’t be without its challenges, can it?

<span class="smashing-tv-speaker">Leslie:</span> Absolutely not. I think I’ve spoken a little bit about what it means sort of as a frontend engineer pushing into sort of some new areas just for me to be thinking about in terms of Serverless and how can we leverage this in the product? I think for me, mastering that sort of back of the frontend side has been an exciting challenge, but certainly there’s a lot to learn there. An example of that in our app right now, is that we use Cypress for end-to-end testing of some of the critical flows in our app, and right now we have that set up so that the Cypress end-to-end tests are running on our Deploy Previews in Pull Requests using a GitHub action. So, we use the GitHub action to run those Cyprus tests against the Deploy Previews of the app.

<span class="smashing-tv-speaker">Leslie:</span> Which is really cool, but there’s probably a better way to do this than actually using a GitHub action. I actually think that we could use a Netlify Serverless function because those can be triggered on certain events, like a deploy succeeded event. So, there’s an opportunity there for us to actually leverage again, Netlify, a little bit more, instead of relying on some of these other tools that maybe we’re more familiar with or more comfortable using. So, in terms of challenges, I think it’s opening our minds to what this sort of new model of development allows us to do and trying to leverage it.

<span class="smashing-tv-host">Drew:</span> Yes, there’s so many different ways on there to... with the tooling that’s available, to be able to attack a particular problem. At Smashing, we probably shouldn’t say there’s more than one way to skin a cat.

<span class="smashing-tv-speaker">Leslie:</span> Yikes.

<span class="smashing-tv-host">Drew:</span> What’s interesting about the workflow as well, is that it’s really intensively Git based, which I think suits... it’s really developer friendly, isn’t it? As a frontend engineer, something that’s Git based kind of just feels like home. So, is that all great or are there any problems that come in with that?

<span class="smashing-tv-speaker">Leslie:</span> I think as a developer Git is wonderful. I think in general it solves big, big problems and I’m very happy to have it. But, because we rely on it so heavily and as our internal team has grown as well, you end up having the same problems that Git has when you’re talking about Netlify in this workflow, right? So, you end up with a bug on your main branch, yes, it’s really easy to roll back the app itself, we talked through what that looks like, and then go in the code and fix it. But what if someone else on your team is working from a broken version of that main branch? Everyone’s going to have to rebase, everyone’s going to have to communicate, or at least be aware of what happened. And so, it’s not so much a Jamstack problem or a Netlify problem, but more of just the age old, how do you coordinate on a team of human beings and how do you use the technology to do that properly?

<span class="smashing-tv-host">Drew:</span> And of course, as you add more tools and infrastructure in around what you’re doing, then you’ve got the problem of everything taking a long time to run. I mean, you mentioned Cypress is one thing. I know Cypress is a real headache with the amount of time those end-to-end tests can take to run. Is there other challenges around that growing build time?

<span class="smashing-tv-speaker">Leslie:</span> Yeah, I think that’s one of the other things that Jamstack... You’re introducing this build time, which for developers is not great. I always try and think about it as what I sort of eat up in that build time, my users are saving in the performance of what they’re getting. So, I always try to keep that in mind when I’m frustrated about how long something is taking to build, but certainly I think that’s an area of opportunity and a challenge, is figuring out how to keep those build times fast, how to make sure that we can deploy as quickly as possible. Some of it is this sort of tension between wanting to run all your tests, wanting to make sure that you don’t deploy a build if a test fails, but at the same time, then you’ve got to run all those tests.

<span class="smashing-tv-speaker">Leslie:</span> So, it’s this constant sort of back and forth between wanting to keep the build times fast, while also making sure that you feel like you’re doing your due diligence before you actually deploy something. And we’re playing around with some ideas here as well about potentially moving our Cypress tests to be running against production and having some alerting setup that would let us know after the fact, if something had failed. Which is sort of an interesting model, too. So yeah, stay tuned.

<span class="smashing-tv-host">Drew:</span> I certainly know that, yes, the dangers of growing build times, just from a developer point of view, from productivity point of view, that if something takes too long to run, you context switch, you start working on something else, and then it just... you lose all the momentum, and maybe you forget to go back and find out whether the build succeeded because you’re then so far into the next task.

<span class="smashing-tv-speaker">Leslie:</span> Yeah, definitely.

<span class="smashing-tv-host">Drew:</span> So, I guess this isn’t the ultimate workflow as it stands at the moment. There must be further we can take it. What sort of opportunities might lie ahead for this way of working?

<span class="smashing-tv-speaker">Leslie:</span> Yeah. So, I think for me, and Netlify in particular, is sort of the thought of collaboration for larger teams. I mean, I know a lot of developers are sort of... have used Netlify for side projects and other things that they’re working on, on their own, but thinking about how it can be leveraged on larger teams, like mine. As we get larger and we’re growing, more of us are in the app, more of us are using Netlify to deploy our own services, and so everything from even more robust audit logs so that you can go and see who changed this site setting, or who was the last person to deploy something. I think having the ability to organize your sites within your Netlify dashboard, even knowing... assigning someone to a build is sort of an interesting idea to me. Could that be helpful if I knew that my teammate had worked on this build, but then I realized they had to roll it back? And maybe I’m just aware of who’s managing that process could be a really useful thing within Netlify itself.

<span class="smashing-tv-speaker">Leslie:</span> And one thing that I’ve seen sort of thrown around a little bit is perhaps the ability to link to a specific log line in build log. So, for debugging, if you have your build log of your Deploy Preview, and there’s an error that got thrown, either from Netlify or from your own code, it’d be nice to be able to link directly to that log line. So, that’s sort of a fun, small improvement that I’ve been thinking about a bit. And that’s not even to say we have some new features at Netlify as well, that are pretty exciting. Edge handlers and background functions. I’m still trying to wrap my head around what they all do and exactly how they work, but I know that edge handlers are going to give us the opportunity to do some things with localized content, which could be... have some interesting implications for features we could build in the Netlify app as well.

<span class="smashing-tv-host">Drew:</span> Yeah, it’s really exciting. I think there are all sorts of people within the Jamstack community who are pushing this the whole thing forward. But I think Netlify, as a service, is one that is really behind it and doing exciting things. And, as I say, I didn’t want this to be a big ad for Netlify, but I think you and I both really love the service, so it is exciting to talk about isn’t it? If listeners want to get more engaged with learning how to build Jamstack sites or want to get more into this ecosystem, is there a good place to go to learn this stuff?

<span class="smashing-tv-speaker">Leslie:</span> I feel like it’s exploding right now. I would certainly point you to the Netlify blog. We try and post some tips and tricks there and announce new features as well. I would give a shout out too, to Learn With Jason. My coworker, Jason Lengstorf does sort of a live stream show, and he does cover... he covers a range of topics, but does some Jamstack specific ones as well. And it’s a fun hour of live coding and picking that out. Twitter, I think, is huge, too. So check out Jamstack hashtag.

<span class="smashing-tv-host">Drew:</span> Good advice. So, we’ve been learning all about how Netlify builds Netlify on Netlify. What have you been learning about, Leslie?

<span class="smashing-tv-speaker">Leslie:</span> Oh, that’s always a big question. I mentioned Cypress before, we’ve been working through some of our processes around exactly how we want to run our end-to-end tests, and so I would say that, in general, I’ve been thinking a lot about that workflow. So, less about the technology itself, but more about what workflows exist for end-to-end testing on the frontend, and what makes sense sort of in this Jamstack model. So, that’s been a fun sort of side tangent. And then, on the CSS side of things, we talked a bit about CSS architecture, and I’m starting to get my hands dirty with Tailwind, which has been a fun and exciting and lots to learn and lots of class names to memorize and... Yeah.

<span class="smashing-tv-host">Drew:</span> That’s exciting stuff. If you, dear listener, would like to hear more from Leslie, you can find her on Twitter where she’s @lesliecdubs, and her personal site is leslie.dev. Thanks for joining us today, Leslie, did you have any parting words?

<span class="smashing-tv-speaker">Leslie:</span> Have a great day?



{{< signature "il" >}}
