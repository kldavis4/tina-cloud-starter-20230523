---
title: 'Smashing Podcast Episode 15 With Phil Smith: How Can I Build An App In 10 Days?'
slug: smashing-podcast-episode-15
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7961c791-d61e-442d-9653-566a9cfd91bf/smashing-podcast-episode-15.png
date: 2020-05-05T05:00:00.000Z
summary: >-
  In this episode of the Smashing Podcast, we’re talking about building apps on a tight timeline. How can you quickly turn around a project to respond to an emerging situation like COVID-19? Drew McLellan talks to Phil Smith to find out.
description: >-
  In this episode of the Smashing Podcast, we’re talking about building apps on a tight timeline. How can you quickly turn around a project to respond to an emerging situation like COVID-19? Drew McLellan talks to Phil Smith to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode of the Smashing Podcast, we’re talking about building apps on a tight timeline. How can you quickly turn around a project to respond to an emerging situation like COVID-19? Drew McLellan talks to Phil Smith to find out.

<iframe src="https://share.transistor.fm/e/c428e943/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [CardMedic](https://www.cardmedic.com)
- [React Native](https://reactnative.dev)
- [React Native for Web](https://github.com/necolas/react-native-web)
- [Expo](https://expo.io)
- [Apiary](https://apiary.io)
- Phil’s company [amillionmonkeys](https://www.amillionmonkeys.co.uk)
- Phil’s [personal blog](https://monkeyphil.co) and [Twitter](https://twitter.com/monkeyphil)

### Weekly Update

- “[Getting Started With Nuxt](https://www.smashingmagazine.com/2020/04/getting-started-nuxt/),”  
*by Timi Omoyeni*
- “[Implementing Dark Mode In React Apps Using styled-components](https://www.smashingmagazine.com/2020/04/dark-mode-react-apps-styled-components/),”  
*by Blessing Krofegha*
- “[How To Succeed In Wireframe Design](https://www.smashingmagazine.com/2020/04/wireframe-design-success/),”  
*by Anton Suprunenko*
- “[Mirage JS Deep Dive: Understanding Mirage JS Models And Associations (Part 1)](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/),”  
*by Kelvin Omereshone*
- “[Readability Algorithms Should Be Tools, Not Targets](https://www.smashingmagazine.com/2020/05/readability-algorithms-tools-targets/),”  
*by Frederick O’Brien*

## Transcript

<p><a href="https://twitter.com/monkeyphil"><img loading="lazy" decoding="async"  style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c7e2de-3724-4430-b725-211223f9ee09/phil-smith-200x200px.jpg" width="200" height="200" alt="Photo of Phil Smith" /></a><span class="smashing-tv-host">Drew McLellan:</span> He is director of the full-stack web development studio amillionmonkeys, where he partners with business owners and creative agencies to build digital products that make an impact. He’s worked on projects for the BBC, AirBnB, Sky Cinema, Pearson, ITV, and Sussex Wildlife Trust to name but a few and works right across the stack with React, Vue, Laravel, Gatsby and more. Hailing from Brighton on the UK South coast, he’s also an author for Smashing Magazine, writing recently about the Alpine JavaScript framework. So, we know he’s a skilled developer and communicator, but did you know he can solve a Rubik’s Cube in six seconds using only his feet? My Smashing friends, please welcome Phil Smith.</p>

<span class="smashing-tv-host">Drew:</span> Hi, Phil. How are you?

<span class="smashing-tv-speaker">Phil Smith:</span> I’m smashing, Drew.

<span class="smashing-tv-host">Drew:</span> We’re in the thick of this crisis of COVID-19 and I think one of the interesting ways that we’re placed as designers and developers and technologists is to be in this position where we can still work and we can still do our jobs. And the work that we do is often based around providing access to information or enabling people to communicate, which is, I think, very relevant in a situation like this. I was interested to look at how those skills could be put to use to help in a time of crisis and then I saw your blog post, Phil, about how you had been doing something just like that. What have you been working on? How did this all start?

<span class="smashing-tv-speaker">Phil:</span> It’s a very crazy story. About three weeks ago I was catch up with some friends and we’re feeling very glum about the whole situation. We’ve got two kids who we’re trying to homeschool while keeping this business going. And I was feeling a bit down about not doing that very well and not doing my job very well and the prospects of seeing friends and things like that. And then I had a chat with my wife who said, "Look, you just need to pick yourself up a bit, really." And the same day, a chap called David got in touch via Wired Sussex, which is a kind of tech group in and around Brighton. And he said he had a friend who’d built a website which was around flashcards for medical practitioners who are caring for patients suffering with COVID.

<span class="smashing-tv-speaker">Phil:</span> He was looking for a developer to turn this website into an app and add a few features. And they wanted it done very, very quickly and they had essentially no money. And I dwelled on it for not very long and I’ve been building apps and have the experience of doing back-end and front-end development and it just felt like this was ... It felt like a significant moment, really, where I was having a bit of a crisis and this incredible opportunity came round and this need and I could actually contribute something. So, I got in touch with David. There was a lot of back and forth. And then I spoke to Rachel, who is the founder of CardMedic. She’s currently in America, so there’s this weird time difference that we’ve got to deal with every day. But she was really keen and very trusting of me. I spoke to her husband who’s a bit more tech-savvy and then we set to work.

<span class="smashing-tv-speaker">Phil:</span> Essentially, it was ... There were a few features that she wanted added but this was really about actually building ... The existing site is on Squarespace, so it needed a new back-end built and an API and then an app that calls on the API and a few nice features added. Yeah. People might have seen the app or they can download it. It’s ridiculously simple. It was really just about ... It wasn’t about there’s loads of learning to be done, it was just about there’s quite a lot of work to do. I just need to get it done. I had a bit of client work to do but tried to put that off as much as possible and did a lot of late nights and got it churned out in about 10 days, I think it took, from starting to getting it on the App Store.

<span class="smashing-tv-host">Drew:</span> Just in the briefest terms, what is the app and how do medics use it?

<span class="smashing-tv-speaker">Phil:</span> One of the strange medical nuances of COVID is because of the way it’s grown, there are lots of people caring for patients who have COVID who have no experience in respiratory illness and they may well be looking after patients whose first language is their first language because of the rate that it’s grown and because of these issues like them dealing with it in care homes and things like that. What the app does is it’s a kind of flashcard system whereby if there’s a particular subject you need to speak to a patient about ... That might be about something like someone’s having difficulty breathing ... Then there would be a flashcard which explains to the patient why they’re having difficulty breathing and what the practitioner is going to do about that.

<span class="smashing-tv-speaker">Phil:</span> The app can also read the script aloud and we’re currently in 10 languages, which is all machine-translated at the minute. Yeah. But that’s the basics of the app.

<span class="smashing-tv-host">Drew:</span> That’s sounds incredibly important, incredibly useful for people working under this pressured situation out in the field. With the quick turnaround that was needed for this project for obvious reasons, how did you go about breaking it down and deciding what needed to be there for launch and what you could deal with and add later?

<span class="smashing-tv-speaker">Phil:</span> Rachel had lots of feature requests that she wanted to add to the app. What we agreed from the outset was the first version, which is the version that is now available ... The things that would ship are all the functionality on the existing site. That is translation into different languages, read-aloud, the text to speech, and then a list of cards alphabetically. And the one that we wanted to add, which we felt fitted into the things we wanted to launch with was a card where practitioners could take a photo of their face and then show it to their patients along with a kind of introductory text because you’ll be wear ... A lot of these people are wearing PPE and they’re just losing ... Caring for people and they don’t know what their faces look like.

<span class="smashing-tv-speaker">Phil:</span> We agreed, actually, to get this thing to ship as soon as possible they are the only features that would make V1. And anything else, we’d park and then we’d prioritize. And we’re kind of going through that process now of saying, "Okay, what do we want to deal with next?" The interesting side of this has been that as we’ve shipped, actually lots of people have come forward with their own suggestions. And Rachel, who’s never done this before, is balancing the things that she thinks the app needs with the things that other people are saying the app needs and we’re trying to balance what is most important, here.

<span class="smashing-tv-host">Drew:</span> It can be a great eye-opener, can’t it? Shipping early and then listening to feedback rather than spending a lot of time in development building loads and loads of features and then getting it in front of users.

<span class="smashing-tv-speaker">Phil:</span> What’s been funny as well is when we got in the App Store last Friday ... Yeah, about midnight on Friday and then The Guardian ran a piece on Saturday. Great. So, we got loads of coverage really quickly and there was quite a lot of feedback from people who aren’t practitioners and that is difficult for Rachel, I think, to deal with of, "Okay, where are these constructive ideas by practitioners and where are these interesting things but actually aren’t going to make a difference in this crisis?"

<span class="smashing-tv-host">Drew:</span> This is a native mobile app that’s built largely with what we usually think of as web technologies. What was the stack and what was each part of that stack responsible for?

<span class="smashing-tv-speaker">Phil:</span> Sit tight. Here we go. The first thing, I think, I did was I have an A3 pad and I mapped out data models and what I thought the data structure would look like. I then ... I use a thing, and I don’t know how I ended up using it, but it’s called Apiary. I don’t even know you pronounce it. You know how you pronounce it.

<span class="smashing-tv-host">Drew:</span> Might be Apurree?

<span class="smashing-tv-speaker">Phil:</span> Yeah. One of those. I think Oracle bought it a few years ago, so I think it’s quite a big outfit now. Anyway, that allows you to write API documentation and it gives you a kind of mock API. I did that first of all. I think this is the first thing that I’ve ever done which is multilingual as well. Certainly, it’s the first API I’ve been multilingual so I had to do a bit of research and suss out ... And part of the reason I decided with this, to do the documentation and the mock API, was just to play with a few ideas about how the API could be structured if it was multilingual.

<span class="smashing-tv-speaker">Phil:</span> I settled on what I wanted the API to look like and then started to build a back-end using Laravel. I use Laravel for ... I do both front-end and back-end. Everything back-end I do, I use Laravel. It’s just incredible. The speed at which you can build a proper back-end is just ... And a really good back-end. It’s fast, it’s incredibly clever, what it does, and if it wasn’t for Laravel, I ... I’m sure there are other things out there, maybe I’d learn Ruby or something, but it just allows me to get stuff done very quickly.

<span class="smashing-tv-speaker">Phil:</span> For example, in the back-end you create one of these flashcards and then you send it off to get the audio transcription and to get it translated into other languages. And the APIs that we use for both those services are quite heavily throttled; you can only do so many requests a second. And the thought of having to deal with calling on other APIs and throttling requests and things like that ... The thought of doing that without Laravel ... I have no idea how I’d do it. But with Laravel, you read the documentation, hunt down a couple of tutorials and you’re away.

<span class="smashing-tv-speaker">Phil:</span> The back-end was probably 90% done within three days, I’d say. I got all of that set up and then really turned my attention ... There’s an admin interface whereby Rachel and others can go in and edit content and update content and add translations and get new audio files. But really, the primary purpose of the backend is the API. Once all the back-end was set up, I focused my attention on the app, which is entirely built using React Native. And that compiled down to both an IOS and Android app.

<span class="smashing-tv-speaker">Phil:</span> Rachel doesn’t have an iPhone and I am completely in on the Apple ecosystem and partly for that reason, but partly because it’s just an amazing tool set, I’m using Expo, which is a collection of tools that wrap around React Native to help with speedy development. There’s an Expo app and what it allows you to do is when you’re in the development phase, completely bypass the App Store by just sending a JavaScript bundle to their servers and when users download the Expo Client on their phone, they can download that JavaScript bundle and load the app within the Expo Client. Does that make sense?

<span class="smashing-tv-host">Drew:</span> It does, yeah.

<span class="smashing-tv-speaker">Phil:</span> Yep. Expo was really the key thing in ensuring this app could be developed really swiftly because it meant every couple of hours I could build something and Rachel could be seeing it where the thought of doing a whole build and getting it to the App Store and go by the Google ecosystem, there’s no way you could do that every couple of hours. It just wouldn’t ... You’d spend more time building than actually developing the app. Expo was crucial in that process.

<span class="smashing-tv-host">Drew:</span> Expo’s the tool that you’re using as part of your development workflow to enable you to do that in the development phase but it’s not something you go into production with? Is that right?

<span class="smashing-tv-speaker">Phil:</span> Exactly. It’s used in development phase but it also handles the build process. Using the CLI, it will build a package that you can then upload to the Play Store or to the App Store. It looks after all the authentication and keys and certificates and all the side of things which has traditionally been such a headache and incredibly daunting as well. And that has made ... I think that has put a lot of people off app development. Getting all these certificates is so difficult and actually, Expo just makes that incredibly easy.

<span class="smashing-tv-host">Drew:</span> How did you go about constructing things on the React side?

<span class="smashing-tv-speaker">Phil:</span> I have a starter framework. I’ve developed a pattern of how I construct apps. I use Redux as state management and that, although it’s not prescriptive, there’s a rough structure that goes alongside that. Yeah, I don’t quite know how much detail to go into, but there’s a lot of stateless components at the end of it, which I’m getting into and I appreciate the advantages of that.

<span class="smashing-tv-speaker">Phil:</span> One other thing that’s worth mentioning is I’m really getting into typing this year or trying to discipline myself to do it. I decided although it would take ... I’m not great at it, so I knew it would take me longer to build the app with TypeScript but it felt a lot safer doing that because intelligence in my editor around TypeScript just meant that I wasn’t making mistakes as often. And I’ve fallen foul of that in the past where I’ve not used TypeScript and I’m getting lots of red screens where things are undefined and I’ve just avoided that and managed it. And that hopefully means now I can add features without risk of breaking stuff that is in there already.

<span class="smashing-tv-host">Drew:</span> And have you done a lot of work with React Native before?

<span class="smashing-tv-speaker">Phil:</span> Yep. I’ve built quite a few things in React Native. It’s nice now because it’s really settled down. And this goes with the whole react ecosystem now. Now I think hooks are being adopted a lot more widely and all those ... That big latest batch of changes, everything feels like it’s settling a bit now and it’s worth learning those things and implementing them. Yeah, it’s great. It’s great.

<span class="smashing-tv-host">Drew:</span> Just thinking about your workflow, you were saying you started with mocking up an API at the back-end. You then built a Laravel app to ... The API was what your Laravel app was exposing to the mobile app, is that right?

<span class="smashing-tv-speaker">Phil:</span> Exactly. Really, the documentation and the mock API was just to give me a standard to work toward. That is what I wanted to get to. And I also ... I sometimes find that, actually, I’d quite like to work on the app now and not on the back-end and that allowed me to switch to work on the app when the back-end wasn’t in place. So, that was another reason for doing that.

<span class="smashing-tv-host">Drew:</span> And I suppose that’s a workflow that larger teams could use and could lean on where you might have different people developing the back-end and a mobile app. If you have a mock API to start with, then both teams can work inwards towards that API at the same time.

<span class="smashing-tv-speaker">Phil:</span> That’s how I first came across this idea because, actually, it meant that if I was building a back-end then someone else could develop the mobile app.

<span class="smashing-tv-host">Drew:</span> How do you balance under time pressure? How do you create a balance between moving quickly and relying on technologies that you are familiar with and you know you can work quickly and you know that will do the job ... How do you balance that between what might traditionally be a longer R&D phase where you workout, actually, what is the really best technology for this job? Is it a case of just going with what you know will do a good job and you can ship quickly?

<span class="smashing-tv-speaker">Phil:</span> That is a good question. I think as soon as the project was mentioned to me, I thought I know exactly how I’m going to build all of this. And if I didn’t have kids and I sat in a dark room, I think I could have probably turned it all around in about five days if I’d have been working on it solid, solid, solid because the requirements were very much in line with my experience of building apps. I’ve built similar kind of things where it calls on an API, stores the results in state and presents them. I’m now at a position where there’s some bits where I’m like, "Okay, I need to go back and refactor that."

<span class="smashing-tv-speaker">Phil:</span> Like I’ve spoke about typing tin, but actually the types can be quite loose in the app and that needs to be tightened up. And on the back-end, there aren’t many tests and now we’re starting to roll the back-end out because lots of people have come forward and said, "Actually, this is a great resource. I’d like to volunteer my services to translate this into my native language." The back-ends being used by more people so I’m just thinking, hang on, I need a few more tests in here to make sure that nothing can break because there are people using this in production now.

<span class="smashing-tv-speaker">Phil:</span> I think I answered your question. Essentially, there was no decision making. I just had to get it out there as quickly as possible.

<span class="smashing-tv-host">Drew:</span> Did at any point you consider making this as a progressive web app?

<span class="smashing-tv-speaker">Phil:</span> We did. Just before this all kicked off there came an announcement which I didn’t fully consume. There was some announcement which I read on Jeremy Keith’s blog which made me nervous about progressive web apps. I really love the technology and the idea behind it, but I just didn’t sense it was far enough along yet. And I don’t sense it’s in people’s psyche quite enough whereas telling people to go to the App Store and download the app, everyone knows how to do that. It just felt like the safest bet was to get the app done.

<span class="smashing-tv-host">Drew:</span> I find sometimes that people are more familiar with the concept of an app than they are with the concept of a website.

<span class="smashing-tv-speaker">Phil:</span> Yeah, my sense, as well, was it just felt too early to place all our eggs in one basket with the progressive web app. I’m sure it will get there. I really hope it will get there because it feels a much better solution to that, but I don’t think we’re quite there yet.

<span class="smashing-tv-host">Drew:</span> You presumably build React projects for the web as well as React Native projects. Is this something that you could take that code base from React Native and move it to the web at some point in the future? How different are those two different environments?

<span class="smashing-tv-speaker">Phil:</span> One of the interesting developments in React Native over the past few years is Nicholas Geiger built a package called React Native Web, which ... How React Native works is it’s React and then you have different clients. And the traditional clients are IOS and Android but Nicholas Geiger’s built this package whereby one of the clients is web. So, you’re building a React Native app but it spits out HTML and JavaScript. And actually, I think I’m right in saying the Twitter website, I think, is built using React Native Web or one of the Twitter ... I’m pretty sure the Twitter website is using React Native Web. And it’s really good. Unfortunately, one of the packages we use doesn’t transfile down to React Native Web.

<span class="smashing-tv-speaker">Phil:</span> However, I think my job for next week is going to be to ditch that package so that we can use React Native Web. And the reason I want to use that is because the website is still currently powered by Squarespace but I would like to use Squarespace for all the marketing stuff but for the actual flashcards, I would like to be using exactly the same code base as a mobile app and call in on the same API so that we can have consistency across the board.

<span class="smashing-tv-host">Drew:</span> I was going to ask, actually, how the website fits into this. The same functionality is potentially going to be available or already is available via the website?

<span class="smashing-tv-speaker">Phil:</span> Some of the functionality is available on the website. That was actually built in View. On the website, we just inject some JavaScript and that was a lot easier to do with View because it’s just a load of script tags. There’s no transfiling, there’s no funny business, and it was just very quick. And I was very confident that I could get that working quite quickly. Yeah, the website is done like that but hopefully by this time next week we’ll have built that with React Native Web.

<span class="smashing-tv-host">Drew:</span> You mentioned that the app needed to be multi-lingual and your flashcards are available in different languages. What was the process of doing that and making that possible?

<span class="smashing-tv-speaker">Phil:</span> The Squarespace site uses a plug-in by a company called Weglot which I was quite impressed by, actually. You essentially set up a load of sub domains and point those sub domains at the Weglot server and that, then, fetches the corresponding page of the English translation and translates it on the fly. And it’s seemingly very reliable and they have said for this service they’re not going to charge anything. And they have got an API as well as that service that they offer to Squarespace. When a card is updated, we post all that data to Weglot along with a list of translations that are active and Weglot sends us back a translation. I think it is larger than a wrapper around Google Translate and a few other services.

<span class="smashing-tv-speaker">Phil:</span> We’re really hopefully that a professional translation service are going to take this on. Yeah. I’ll probably post something about that on my blog this week and that will be on the CardMedic website. But yeah, a professional translation service have said they’ll do it and they’ll do 10 languages. And then we’ve had a load of other people come forward and say they’re really happy to translate it to their languages. So, I’m building this editor feature whereby people who are ... Quite a few people have come forward from Hungary and they can see a list of articles that have yet to receive a Hungarian translation and they can just pick them off and once they’re done, we’ll be able to push those new languages live.

<span class="smashing-tv-host">Drew:</span> And another API you mentioned that you made yourself was one for text to speech. How did that work?

<span class="smashing-tv-speaker">Phil:</span> The website uses a service called SiteSpeaker. Again, I think this might be a wrapper around Google text to speech services, but you send them a string of text and the language the text is in and the voice that you want, because you can have different voices, and it sends you back an audio file. I think it dumps it on S3 or something, sends you back a URL. There’s been some tricky bits around that, around how particular characters are encoded, especially when you get to foreign languages. That gets really difficult. But I think that is working pretty well now.

<span class="smashing-tv-host">Drew:</span> One of the things that you mentioned as part of the basic requirements for version one was the ability to search for a flashcard. How are you handling the search within the app? Is that happening in the client or does that happen back on the server?

<span class="smashing-tv-speaker">Phil:</span> That happens in the client and is ridiculously simple. And I’m sure there’s a much better way of doing searches than seeing if one string is included in another string. I think, again, that might be developed because for example, if you’re searching for breathing almost every article on there comes up and it probably needs to be a bit more sophisticated. But at the minute, it’s doing the job.

<span class="smashing-tv-host">Drew:</span> That’s how search always starts.

<span class="smashing-tv-speaker">Phil:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> The simplest possible solution and then you work out from there when you find the problems.

<span class="smashing-tv-speaker">Phil:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> The Laravel back-end, how is that hosted?

<span class="smashing-tv-speaker">Phil:</span> That is on Digital Ocean. Again, Digital Ocean has launched a COVID relief program, so they have put a load of credit on our account to cover the cost of this, which is great. I don’t think we’re paying for any service and we’re using a lot of services on there. The server was built using Forge, which is a service built by the founder of Laravel, Taylor Otwell, which spins up new Digital Ocean droplets and services on S3 and a few other hosting packages. It does all the stuff, in my eyes, that a sys admin would do like scheduling and cron jobs and upgrading and deployment. It just makes it so simple. I’d be lost without that.

<span class="smashing-tv-host">Drew:</span> It sounds like that architecture of this app is making a lot of use of external services and APIs, which is a nice modern way to go. Given more time to investigate different options, do you think it’s the sort of app that could have been built with a serverless approach?

<span class="smashing-tv-speaker">Phil:</span> It could have. One of the funny things about it is it’s not very demanding on the server. The jobs that do need to be done, like going to the text to speech, that’s intensive process but we’re not actually doing that process. We’re just calling API and it’s somebody else’s problem. There’s quite a lot of request to the server, but we cache ... Everyone’s getting the same content so we just cache the API and flush the cache once every hour, I think. So there isn’t actually a lot of load on the server. It is not the cheapest droplet but it’s not far off the cheapest droplet and it’s doing fine. It probably could have been serverless but, again, I think that ecosystem isn’t quite ... Well, I don’t know enough about it to be able to churn that out in this amount of time.

<span class="smashing-tv-host">Drew:</span> Would you have done anything differently, looking back at the project now, about the way the technology came together? The choices that you made? Would you have done anything differently if you could do it over?

<span class="smashing-tv-speaker">Phil:</span> I wish we’d use React Native Web from the start. I kind of tried to do that after the fact and realized that actually, that was going to be really difficult. I wish I’d used React Native Web from the start and played closer attention to that. I don’t think I’d have changed anything on the back-end side of things. I wish I had more time to have done it. I feel there are some bits I could have done better. And I maybe wish I could have got a designer involved. A lot of it is from a UI framework, the app itself, and there are some screens which I’m less happy with than others. And the screen I’m least happy with is the one that The Guardian decided to feature on their homepage over the weekend, so that was a bit annoying.

<span class="smashing-tv-host">Drew:</span> Once an app is ready, you think about getting it into the hands who need it. From a web project point of view, that’s just deploying to a server of a CDN. With Native apps, it’s a little bit more complex than that, isn’t it? You need to know about the App Stores, about developer accounts and all that sort of business. Is that something you’ve done a lot of before? And how did that process go?

<span class="smashing-tv-speaker">Phil:</span> Expo handle a lot of the difficult technical side of that and the documentation on the Expo site is incredible. If you’re just getting into this and you’re thinking oh, yeah, I’m a front-end dev, I think I could build an app, then you should just dive into Expo and give it a whirl because even if you don’t ship, it will take you through the whole process and explains everything really clearly. And I don’t know how they do it, but their documentation, they always manage to keep up to date with the Play Store and the App Store. So when the UI changes in ... What’s it called? App Store Connect ... Then actually, the Expo documentation is updated, which just makes everything so much easier because you just follow their instructions and it all works great.

<span class="smashing-tv-speaker">Phil:</span> One of the biggest stress and difficulty with the whole project came about getting approval in the App Stores. We shipped ... We first submitted the app to the Apple App Store last Thursday. Yeah, last Thursday. So, eight days ago as we’re recording this. And it was pretty promptly rejected with a very, very stern rejection notice saying, "Don’t try this again." And it pointed us to a document which they published but I had not read saying, "We’re only going to release COVID apps from registered companies." And this is all on my developer account at the time. And my heart sank and I thought, "Oh God. I’ve spent a lot of time on this and this woman, Rachel, has spent loads of time on it and it’s not going to happen."

<span class="smashing-tv-speaker">Phil:</span> I then calmed down a bit and we rushed through her developer account for her company. Thankfully, she was ... CardMedic is a registered trademarked company, so we rushed through a developer account, made the application on her account and it was approved straight away. Getting the Android app published has been the same process but drawn out over 10 days and they sent us a really harsh rejection notice, whereas Apple’s was like, "We don’t know who you are. You’re some bloke with a funny company name. Why on earth are you talking about COVID?" Which I kind of understand.

<span class="smashing-tv-speaker">Phil:</span> The Google rejection notice was talking about profiteering from the pandemic and saying the app was insensitive and it was just very, very scary. And I was quite disheartened but I wrote a very firm appeal to their rejection and said, "Look, we’re reputable. We got a letter from a consultant at the hospital. The app was on The Guardian and The Beeb last weekend and has also featured on Government UK this week." We sent the Play Store links to those articles and they approved the app this morning. But yeah, that had been the biggest stress of the project because you obviously can’t phone up Tim Cook and say, "Hey, where’s my app?" You just kind of ... Especially with Google, you just submit the app and you can put in some supporting notes but there’s no dialogue. So, that was quite stressful but we’ve done it now. It’s in.

<span class="smashing-tv-host">Drew:</span> You’ve managed to get the app developed in about 10 days and it sounds like the reception has been pretty good, being featured on news outlets and going down quite well with its potential users. What are the next steps? Where does it go from here?

<span class="smashing-tv-speaker">Phil:</span> The next steps are getting the translations better. We really want to incorporate some features which will help people who have some kind of learning difficulty. I think I’d likely involve adding illustrations to particular cards. There’s this key card which shows your headshot and says, "Hi, my name is Phil. I’m a doctor at UCH," and so forth. That page currently isn’t translated because, obviously, it’s unique to everyone. So I want to sort out how I’m going to do that without ... Because we need to do that presuming that the person is offline when they’re viewing that screen, so that’s a little bit challenging but I’m sure I’ll sort that out. And then there’s a whole load more cards to add over the weekend as we hear of more use cases and more stories about it. So, we’re getting some new cards written, which will help in those scenarios and we’ll hopefully get those on the app soon.

<span class="smashing-tv-host">Drew:</span> It sounds like very valuable work to be doing and people can, of course, find out more about the app by going to CardMedic.com. I’ve been learning about building apps rapidly. What have you been learning about lately, Phil?

<span class="smashing-tv-speaker">Phil:</span> I have been learning about how to make the perfect pulled pork because it was my birthday this week and we’re having a virtual Zoom party tomorrow night, so I currently have two very large cuts of pork barbecuing and they’ve done five hours and they’ve got about 12 hours to go.

<span class="smashing-tv-host">Drew:</span> That sounds delicious. If I wasn’t vegetarian ...

<span class="smashing-tv-speaker">Phil:</span> Yeah. The pulled halloumi isn’t quite as tasty, I’m afraid.

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Phil, you can follow him on Twitter where he’s @MonkeyPhil and his personal blog is MonkeyPhil.co. You can find examples of his work and hire him to work on your projects at AMillionMonkeys.co.uk. Thanks for joining us today, Phil. Do you have any parting words?

<span class="smashing-tv-speaker">Phil:</span> I think I’d really encourage people if they are front-end web developers to at least explore building apps in React Native. If you’ve got experience in React and you’re willing to read a lot of documentation, actually the process is nowhere near as daunting as you’d imagine.

{{< signature "il" >}}
