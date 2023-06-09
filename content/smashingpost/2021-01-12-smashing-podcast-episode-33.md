---
title: 'Smashing Podcast Episode 33 With Charlie Gerard: What Is Machine Learning?'
slug: smashing-podcast-episode-33
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4106551a-7866-462a-9f4c-70281654cdbe/smashing-podcast-episode-33.png
date: 2021-01-12T05:00:00.000Z
summary: >-
  In this episode, we’re talking about Machine Learning. What sort of tasks can we put it to within a web development context? Drew McLellan talks to expert Charlie Gerard to find out.
description: >-
  In this episode, we’re talking about Machine Learning. What sort of tasks can we put it to within a web development context? Drew McLellan talks to expert Charlie Gerard to find out.
categories:
  - Smashing Podcast
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re talking about Machine Learning. What sort of tasks can we put it to within a web development context? I spoke with expert Charlie Gerard to find out.

<iframe src="https://share.transistor.fm/e/1e8b2eb7/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- [Practical Machine Learning in JavaScript: TensorFlow.js for Web Developers](https://www.apress.com/gp/book/9781484264171)
- Charlie [on Twitter](https://twitter.com/devdevcharlie)
- Charlie’s [personal site](https://charliegerard.dev)


### Weekly Update

- [A Practical Introduction To Dependency Injection](https://www.smashingmagazine.com/2020/12/practical-introduction-dependency-injection/)  
*written by Jamie Corkhill*
- [Towards An Ad-Free Web: Diversifying The Online Economy](https://www.smashingmagazine.com/2021/01/towards-ad-free-web-diversifying-online-economy/)  
*written by Frederick O’Brien*
- [Should The Web Expose Hardware Capabilities?](https://www.smashingmagazine.com/2021/01/web-expose-hardware-capabilities/)  
*written by Noam Rosenthal*
- [How To Make More Money Selling Shopify Apps In 2021](https://www.smashingmagazine.com/2021/01/selling-shopify-apps-2021/)  
*written by Suzanne Scacca*
- [Getting Started With The GetX Package In Flutter Applications](https://www.smashingmagazine.com/2021/01/getx-package-flutter-applications/)  
*written by Kelvin Omereshone*

## Transcript

<p><a href="https://twitter.com/devdevcharlie"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539e934a-1136-4316-835b-edb1e378c569/charlie-gerard-200x200.jpg" width="200" height="200" alt="Photo of Charlie Gerard" /></a><span class="smashing-tv-host">Drew McLellan:</span> She’s a senior front-end developer at Netlify, a Google Developer expert in web technologies and a Mozilla tech speaker. In her spare time, she explores the field of human computer interaction, and builds interactive prototypes using hardware, machine learning and creative coding. She regularly speaks at conferences and writes blog posts to share the things she learns. And most recently, is the author of the book, Practical Machine Learning in JavaScript for Apress.

<span class="smashing-tv-host">Drew:</span> So we know she’s a front-end expert, but did she once to escape from jail using a metal file she’d crocheted out of dreams. My smashing friends, please welcome, Charlie Gerard. Hi Charlie. How are you?

<span class="smashing-tv-speaker">Charlie Gerard:</span> I am smashing.

<span class="smashing-tv-host">Drew:</span> I wanted to talk to you today about machine learning, which might seem like a little bit of a strange topic for a podcast that focuses mainly on the sort of browser end of web development. I tend to think of machine learning as something that happens in giant data centers or laboratories with people with white coats on. It’s definitely a bit of a sort of buzzword these days. What on earth do we actually mean when we say machine learning?

<span class="smashing-tv-speaker">Charlie:</span> So in general, the standard definition would be it’s giving the ability for computers to generate predictions without being told what to do. Hopefully, this will make sense when we keep talking about it, but that’s the kind of generic conversation definition. You don’t really tell algorithms or models to go and search for certain things. They learn through data that you give it and it can then generate predictions.

<span class="smashing-tv-host">Drew:</span> So rather than having to specifically code for certain circumstances, you kind of create a generic case where the software can learn how to do that stuff itself?

<span class="smashing-tv-speaker">Charlie:</span> Yeah, exactly.

<span class="smashing-tv-host">Drew:</span> That sounds almost a little bit creepy. It’s kind of verging on that artificial intelligence sort of side of things. Do you need to be a hardcore math nerd or a data scientist to do this? Or is there stuff out there like established algorithms and things that you can call on to get started?

<span class="smashing-tv-speaker">Charlie:</span> Yeah. So luckily you don’t need to be a hardcore math nerd or a data scientist. Otherwise, I would definitely not be talking about this. But there are algorithms that have already been figured out and tools already available that allow you to use these algorithms without having to write everything from scratch yourself. So if we use the front-end ecosystem as a comparison, you can use web APIs, like the navigator to get user media when you want to have access to the webcam or the microphone.

<span class="smashing-tv-speaker">Charlie:</span> And you don’t have to know how that API was actually implemented under the hood. What matters is that you know what this API is good for and how to use it, if you want. Then later on you can go and look into the source code of your favorite browser to know how it really works, but it’s really not useful in the first place. And it can be useful if you want to write your own algorithm later on. But to be really honest, it’s highly unlikely that you’ll want to do this.

<span class="smashing-tv-host">Drew:</span> Okay. So it’s a bit like the way you can write CSS to position an element on a page. You don’t care how the browser is actually doing that. You just write some CSS and the browser takes care of it.

<span class="smashing-tv-speaker">Charlie:</span> Yeah. When you get started, it’s mostly something like that.

<span class="smashing-tv-host">Drew:</span> That’s good. That’s more sort of my level of data science.

<span class="smashing-tv-speaker">Charlie:</span> Me too.

<span class="smashing-tv-host">Drew:</span> So what are the sort of problems that you can put machine learning to? What sort of things is it good for?

<span class="smashing-tv-speaker">Charlie:</span> It depends what you want to do in the first place, because when you want to build a certain thing, I would advise to first think about the type of problem that you want to learn that will then help you pick an algorithm that you can use to fix or to find a solution to your problem. So in general, I would start by thinking about the type of problem that I’m trying to solve, and there’s three main ones. I think there’s probably a bit more, but in general, for what I’ve been trained to do and what I’ve read, there’s three main ones that are mentioned.

<span class="smashing-tv-speaker">Charlie:</span> If you want me to go into this, there’s supervised learning, unsupervised learning and reinforcement learning. You also have so many supervised, but to be honest, I don’t really know that much about it because I’ve been able to build my projects with the three first ones.

<span class="smashing-tv-host">Drew:</span> Supervised, unsupervised and reinforcement, did you say?

<span class="smashing-tv-speaker">Charlie:</span> Yeah, reinforcement learning.

<span class="smashing-tv-host">Drew:</span> Okay. So what is supervised learning? Can you give us an example of what that means?

<span class="smashing-tv-speaker">Charlie:</span> Supervised learning, it’s when your dataset is made of features and labels and you feed that to an algorithm. So if we take an example that hopefully most people will be able to relate to, it’s, if you have a house and you want to sell it, and you want to figure out at what price you’re going to sell your house or your car, actually, by the way, it would be the same thing. And you would use a data set of houses in the same environment or the same type of houses and knowing their price on the market, you would be able to use the features of your own house; so how many rooms and does it have a garden and which neighborhood is it in? And things like that.

<span class="smashing-tv-speaker">Charlie:</span> These are the features and the label would be the price, and using all of these data sets of houses already around you, you are able to use a machine learning algorithm that’s going to kind of learn the correlation between the features of your house and the prices on the market, to then get the features of your house and being able to generate a price out of that. So the most important thing is in supervised learning, you have a bunch of features and a label as well, so you’re able to actually draw a correlation between the two.

<span class="smashing-tv-host">Drew:</span> You would, you would feed the model with a vast set of data about houses in this example, where you know their price and then you know all these features about them. Say bedrooms and what have you, like square footage, and I guess location would be another sort of thing that might be factored in?

<span class="smashing-tv-speaker">Charlie:</span> Yeah. So that’s one of the problems with machine learning is that you can have a lot of features and some of are not actually going to be as efficient as others as well. So you could have, for example, the color of your house, might actually have no correlation with the price, but you can give a bunch of features and the model will itself find correlation between the two. You can then tweak your dataset, if you want, and remove the color, or you realize that the size of the garden doesn’t matter or things like that.

<span class="smashing-tv-speaker">Charlie:</span> So in general, even if you feed your data set to a model, you won’t have a perfect prediction the first time. Usually you tweak a few different things and you see. You kind of tweak it until it gets to a prediction that you think is pretty accurate.

<span class="smashing-tv-host">Drew:</span> And then once that model is created, or say you created it using data from one city, could you then take that and feed it... would you need to feed it data from another city? Would you be able to pick it up and use it elsewhere once that training is done or is it then specific to that data set or how would that work?

<span class="smashing-tv-speaker">Charlie:</span> I think it would be specific to the data set. So it means that you can create another data set with the same, let’s say format. If you have an Excel Spreadsheet with different columns, you would be able to keep the same label and features, but you would have to replace it with the values of that city. But in general, it means that gathering the data set can take a lot of time as well, but if you already know what you did for the city of Paris, for example, and that the structure of your data set is the same, but you replace the values, it’s a bit faster and you can regenerate the model.

<span class="smashing-tv-speaker">Charlie:</span> You shouldn’t reuse the same model, if your data is different because the prices of the houses in Paris is different than a small city in Australia, for example. So you wouldn’t want to have wrong data because the core of your data set at first was not exactly the same.

<span class="smashing-tv-host">Drew:</span> We talk a lot about sort of models with machine learning. So the model is kind of like the end result of all the analysis of the data set. And it’s then used to make subsequent predictions. That’s what the model is, yeah?

<span class="smashing-tv-speaker">Charlie:</span> Yes, it’s exactly that. It’s a model so it’s a bit like a function to which you’re going to feed new inputs that it’s never seen before, but based on what it’s learned on the training step. it would be able to output a prediction.

<span class="smashing-tv-host">Drew:</span> So supervised learning, then it makes this predictive model from labels on features. What is unsupervised learning?

<span class="smashing-tv-speaker">Charlie:</span> So unsupervised is a little bit of the same concept, but you remove the labels. So in this case, you can think that our problem of selling a house, wouldn’t really be unsupervised learning problem, because if you only know features about the houses around you, but you don’t have a price as a label, you can’t really predict a price. It won’t even know what a price is.

<span class="smashing-tv-speaker">Charlie:</span> So unsupervised is more when you have a set of data and you only have features about it. You can generate more of trends or clusters of things together. You wouldn’t use unsupervised learning if you want a particular output, if you have a certain question, like, "What’s the price of this?" That’s not a really good use of unsupervised, but it’s more, if you want to cluster entities together, it could be people or things like that.

<span class="smashing-tv-speaker">Charlie:</span> So usually, a use case for that is recommendations like Amazon recommendations or Spotify recommendations, like, "People like you also listen to this," and it’s more around that where the features is in this case would be... well, they have data about you, so they know what you listen to, which country usually you’re in, or how many times a day do you listen to something? So using these features about people, they can then put you in the same cluster or the same kind of listeners, or the same kind of people who buy certain things on Amazon. And using that kind of unsupervised learning, they can know what to advertise to you or what to recommend that you should listen to based on people like you. So it’s more that kind of problems.

<span class="smashing-tv-host">Drew:</span> Okay, so this is all making a lot more sense to me now as a a web developer, because these sorts of uses that we’ve talked about, house pricing and recommendations and serving ads and things, at the end of the day, these are all sorts of things that we have to deal with and features that we might want to put into a site or a product, or what have you. So we’ve got the, the different types of learning based on subject matter that we’re looking to predict. Are there other sorts of applications that we can put this too with? Are there sort of good examples that that people have created that might use of this?

<span class="smashing-tv-speaker">Charlie:</span> Yeah. There’s so many examples. That’s why, when I talk about predicting the price of a house, maybe it’s not something that relates to you. Maybe it’s not really that exciting, but there’s actually so much more that you can do. There’s really good examples around. I think the first one that I saw was around a dynamically generated art texts for images. So of course it’s something that you can do yourself when you add an image to a site.

<span class="smashing-tv-speaker">Charlie:</span> But what if you have a site that actually has really tons of images, and instead of doing manually, you could feed each image to a machine learning algorithm, and it would generate an art text that of what that image is about, and maybe the only human step would be to verify that this is correct, but it would really allow you to focus your time on building the application.

<span class="smashing-tv-speaker">Charlie:</span> And you would still make your website accessible by having art text for images, but it would be kind of generated by a machine. So that’s one of the example that I saw when I got started into this, but you also have a prototype of filtering not safe for work content. And I was thinking that would actually be quite good in a Chrome extension, you could have a Chrome extension that every time that you open a webpage, you would just check that what’s on the page is kind of safe content.

<span class="smashing-tv-speaker">Charlie:</span> For example, if you have kids using your laptop or things like that, you could then just hide the images or replace these images with pandas, if you want or something. But it’s that kind of application where you can use machine learning to kind of automatically do things for you so that you don’t have to worry about certain tasks, or you can just use your brain power to do other things.

<span class="smashing-tv-speaker">Charlie:</span> But then there’s even more advanced with an example of gesture recognition, using the webcam that then was communicating with Amazon Alexa and voice recognition and all that stuff. So you can really merge together a lot of different technologies with voice and webcam and machine learning for just recognition and being able to interact with different technologies, but in a new way. So it can really go quite fun.

<span class="smashing-tv-host">Drew:</span> That’s quite fascinating, because we’ve looked at sort of analyzing data models as such, and now we’re thinking about looking at image content and analyzing the content of images using machine learning, which is quite interesting. I guess that’s the sort of feature that Facebook has, if somebody posts a picture that they think might be gory or show an injury or something, and it blurs it out, and then you have to just click to reveal it. That sort of thing, obviously, Facebook can’t have teams of moderators looking at every image that gets uploaded.

<span class="smashing-tv-speaker">Charlie:</span> I hope they don’t.

<span class="smashing-tv-host">Drew:</span> That would be an endless task.

<span class="smashing-tv-speaker">Charlie:</span> That’s not a great job neither.

<span class="smashing-tv-host">Drew:</span> I used to work on a free ads website where people could post ads. And there was a lot of moderation involved in that, that even me, as the web developer, had to get involved in, just going through, looking at all these images saying, "Yes, no, yes, no."

<span class="smashing-tv-speaker">Charlie:</span> I did that a bit as well. I wish that at that time there had been machine learning, just a little utility tool just to do that for me, and now it’s there. So that’s pretty cool.

<span class="smashing-tv-host">Drew:</span> Yeah, that’s really great. And it’s quite exciting then thinking about live input from a webcam and being able to sort of analyze that in real time, so that you can do gesture based interactions. Is that...

<span class="smashing-tv-speaker">Charlie:</span> Yeah, so at core it actually uses more image classification, because your webcam, an image is a set of pixels, but then as you make certain gestures, you can train a model to recognize that your right hand is up and maybe you would control the mouse like this, or it would look at the coordinate of your hand and the screen, and you would follow the mouse. You could really do whatever you want. You could maybe have color recognition.

<span class="smashing-tv-speaker">Charlie:</span> You can do really fun things. One a prototype that I built, that I kind of gave up on that at some point, but I built a little... I wanted it to be a Chrome extension, but that didn’t work. I built a little desktop app with Electron. Also in JavaScript where I could browse a webpage just by tilting my head. So it would recognize that when I tilt my head down, then it scrolls down, and when I go up, it goes up. It was just these kind of little experiments where I was thinking, "Well, if I can then turn it into a Chrome extension, it could be useful for some people."

<span class="smashing-tv-speaker">Charlie:</span> Even if you’re just eating in front of your computer and you’re reading the news and I don’t want my keyboard to be dirty, then I can just tilt my head, but then also hopefully, for accessibility, could actually help people navigate a certain webpages or things like that. There’s a lot of tools available and it’s about the idea that you can come up with observing the situation around you, and how could you solve some of these problems with using machine learning?

<span class="smashing-tv-host">Drew:</span> For machine learning, we often think of languages, Python. I think that’s where a lot of the sort of development seems to happen first. But as web developers, we’re obviously more comfortable with JavaScript generally. Is machine learning something that we can realistically expect to do. I mean little fun examples are one thing, but is it actually useful for real work in JavaScript?

<span class="smashing-tv-speaker">Charlie:</span> Well, I mean, I think so, but then I know that most of the things that I do are prototypes, but I think that then it depends on the situation that you’re in at work. There are ways to implement machine learning as a developer in your day-to-day job. But what I really like about JavaScript is the fact that if you’re already a front-end dev, you don’t have to go and learn a new ecosystem or a new set of tools or a new syntax, a new language. You are already in your environment that you work in every day.

<span class="smashing-tv-speaker">Charlie:</span> Usually when you learn that type of stuff, you kind of have to start on your own time, if it’s not your day-to-day job and everybody’s time is precious and you don’t have that much of it. So if you can remove some barriers and stay in the same ecosystem that you know, then I think that’s pretty good, but also you can start... the power to me of JavaScript is that you can start by building a small prototype to convince people that maybe there’s an idea that needs to be investigated, and by being able to spin up something quickly in JavaScript, you can validate that your idea is right.

<span class="smashing-tv-speaker">Charlie:</span> Then either you can get buy-in from leadership to spend more time or more money, or you can then give that then to Python developers, if you want to build it in Python. But to me, this ability to validate quickly an idea is super important. Especially, maybe if you work for a startup and everything goes fast and you’re able to show that’s something is worth looking into, I think that’s pretty important.

<span class="smashing-tv-speaker">Charlie:</span> And also the fact that there’s really a big ecosystem of tools and there’s more and more frameworks and applications of machine learning. In JavaScript, it’s not only on a webpage that we can add machine learning. As I was saying before, you can build Chrome extensions and desktop apps with Electron, and mobile apps with React Native, and hardware and IoT with frameworks like Johnny-Five.

<span class="smashing-tv-speaker">Charlie:</span> So with the language that you already know, you actually have access to a huge ecosystem of different platforms that you can run kind of the same experiment on. And I think that, to me, that’s pretty amazing. And that’s where I see the real power of doing machine learning in JavaScript. And as it gets better, maybe you can really integrate it in, in the applications that we build everyday.

<span class="smashing-tv-host">Drew:</span> JavaScript is everywhere, isn’t it?

<span class="smashing-tv-speaker">Charlie:</span> Yes.

<span class="smashing-tv-host">Drew:</span> For better or for worse, it’s everywhere. Who would have thought it? This sounds great but it also sounds like kind of a lot of work. And I think about the data sets and things, how on earth do you get started with doing these sorts of tasks?

<span class="smashing-tv-speaker">Charlie:</span> There’s at the moment, at least with TensorFlow.JS, there’s three things that you can do with the framework. And let’s say the simplest one is importing an existing pre-trained model. So there’s a few of them, there’s different models that have been trained with different datasets, and I would recommend to start with this because you, you can learn the really basics of how to actually even use the framework itself, and what you can do with these models.

<span class="smashing-tv-speaker">Charlie:</span> So you have certain image recognition models that have been trained with different images. Some of them are better for object recognition. Some of them are better for people recognition, and by understanding what models to use, we can then be free to build whatever you want in the constraint of that model.

<span class="smashing-tv-speaker">Charlie:</span> But I think to me, that’s a good way to get started. I still use pre-trained models for a lot of my experiments because it’s also, why would you reinvent the wheel if it’s already there? Let’s just use the tools that were given. Then when you want to go, maybe a step further, you can do what is called transfer learning, when you retrain an important model. So you still use one of the pre-trained models, but then you’re given the opportunity to retrain it live with your own samples.

<span class="smashing-tv-speaker">Charlie:</span> For example, if you wanted to use an image classification where you have different people, then you want to do gesture classification, maybe. If your model, for example, is trained with people who always have, I don’t know, their right hand up or something, but for your application, you want the left hand, you could retrain that model with your samples of the left hand, and then you would have a model that is already quite trained to recognize right hand, but then you would add your own sample and you can retrain that quite quickly in the browser, depending on the amount of new input data that you give it, it takes a bit of time, but in a few seconds you have a retrained model that is very good at recognizing these two gestures that you can then use in, in your app.

<span class="smashing-tv-speaker">Charlie:</span> So that’s like usually the second step. And then a third step that is a bit more complex is when you do everything in the browser. So you write your own model from scratch and you train it in the browser and you really train and run and generate the model, everything in the browser. But in general, the only application that I’ve seen for this is building visualizations. When you want to visualize the process of a model being trained and the number of steps that it’s taking, how long it’s taking, and you can see the accuracy going up or down, depending on the features that you pick and the parameters that you tweak.

<span class="smashing-tv-speaker">Charlie:</span> So I haven’t really played with that one because I haven’t found an application for me that I wanted to build with, but the two first steps of only using the pre-trained model or retraining it with my own samples is where personally I’ve seen. I’ve had fun with that.

<span class="smashing-tv-host">Drew:</span> So typically is going to be a case of creating the model beforehand, sort of offline as it were, and then the browser then uses that trained model, or maybe adds a little bit to, it does a little bit of retraining, but generally, that model is going to be established before it gets put into use in the user’s browser?

<span class="smashing-tv-speaker">Charlie:</span> In general, yes. Then you can definitely create your own model. If you do it, I wouldn’t recommend to train it in the browser, but you can do it in NodeJS as well. If you know, a little bit of NodeJS. I’ve definitely created my own models, but I usually run it in NodeJS because it’s a bit more performant. And then I use the generated model that I created then in the browser.

<span class="smashing-tv-host">Drew:</span> What tools are there available to do this with JavaScript? You mentioned TensorFlow JS but what’s that, where’s that? Is that from Google?

<span class="smashing-tv-speaker">Charlie:</span> Yes. At first Google had the TensorFlow tool in Python and now, for the past, maybe couple of years, maybe a bit more they made the JavaScript version, so it tends to flow with JS. But there’s also ML5 JS that’s a little bit of an abstraction on top. So if you are a bit confused or if TensorFlow JS looks a bit scary with some of the vocabulary that they use in their documentation, you can use ML5 JS that has most of the same features, but let’s say that the API or the Syntax is a little bit more beginner friendly.

<span class="smashing-tv-speaker">Charlie:</span> You can start with ML5, see if you like machine learning, or if you think about a cool application, and then if maybe you have some blockers in ML5 or the framework doesn’t have certain things that you want to do, you can then move on to TensorFlow JS if you want. And if you really are not interested in really writing your own code but you just want to use tools that are already there, there are some APIs from Amazon, Google, and Microsoft to do image recognition or voice recognition as well. So if you’re more interested in seeing what it can do, but you don’t want to spend too much time writing the code, you can ping some APIs and try some of their tools as well.

<span class="smashing-tv-host">Drew:</span> That’s quite interesting. So you could maybe use the browser to catch input from a webcam or a microphone or what have you, and then send that up to Amazon, Microsoft or whoever and then just let them do the hard work?

<span class="smashing-tv-speaker">Charlie:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> And then you just benefit from the results.

<span class="smashing-tv-speaker">Charlie:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> That sounds like a nice, tempting way just to get started with the ideas. It sounds great but what problems can we apply this to in the front end? We’ve talked about a few little things, but are there other ways we could put this to use?

<span class="smashing-tv-speaker">Charlie:</span> There’s a lot of ways. If I start with image classification, yes you could. You could use images from the web or from the webcam on your phone. If you just use your website on your phone and you can take pictures and recognize objects, and either do… A small thing that I built was around recycling, where if I don’t really know where to put certain objects in which bin, we have the yellow bin, the green, it depends on the countries. They have different colors, but sometimes I’m not really good at knowing where to actually throw things so you could build little tools like this that, live can recognize two objects in front of you and then classify them and you can build certain things like this.

<span class="smashing-tv-speaker">Charlie:</span> Otherwise, you have text classification where earlier this year, I used one of the TensorFlow GS model to look at comments written on, GitHub issues and GitHub PRs to then classify and say, “Hey, if it is a toxic comment, then you have a little bot that says, “Hey, maybe you shouldn’t have written this,” or, “Careful, it’s a bit toxic. We want this to be a safe space.”” So you can use text classification like that.

<span class="smashing-tv-speaker">Charlie:</span> There’s sound classification if you want, where when Apple released their new watch, OS, they had something to recognize the sound of running water, to tell people, to wash their hands for 20 seconds with the COVID pandemic, but you can do that in JavaScript as well. And that the thing that was really interesting, I was watching some of the videos and I was like, “Oh, I know how to do that in JavaScript.”

<span class="smashing-tv-speaker">Charlie:</span> And I built a little prototype. I don’t know if it runs on the Apple watch. Maybe. I don’t have one, but I know it runs on my phone and my laptop. And then that can start some ideas for other people as well, where a friend of mine, Ramón Huidobro, @hola_soy_milk on Twitter. He’s been in a lot of online conferences this year. And one of his problem is that when he claps to applaud somebody, then he doesn’t have the time to add the clap emoji on the chat as well. And what he wanted to do is listen to the sound of his claps and that would send automatically clap emojis in the chat.

<span class="smashing-tv-speaker">Charlie:</span> And it’s little things like this that if you want maybe an application really more useful in your day-to-day job is around predictive prefetching. That’s also using machine learning in the front end where looking at the analytics of your website. So which pages are usually looked at after which, and things like this. You can prefetch resources in advance based on the page that is most likely to be visited after. That’s something that I’ve been wanting to look into this whole year, but I didn’t have the time, but that allows you to really improve the performance and the UX of your page. And you don’t request resources that you’re not going to need, so that can really improve, and that’s an application of machine learning as well.

<span class="smashing-tv-speaker">Charlie:</span> So you can do fun stuff, or you can do more useful things, but there’s no wrong application, there can be wrong applications. I take it back, but I’m just saying that if you’re really getting started into it, there’s nothing wrong with starting with something fun, and then I can spin up a few ideas of something that you can do on the job as well.

<span class="smashing-tv-host">Drew:</span> I guess the really useful thing here is knowing that these things are possible. And actually just creative ways of solving problems that we can do on our own. Traditionally we built things by moderation of user submitted content, and it’s been fairly primitive and we’ve basically had to have human beings look at stuff and make decisions about it. But with access to machine learning, in that example, we could hand more of that over and then just have humans look at the edge cases, for example, things that didn’t have a convincing match.

<span class="smashing-tv-host">Drew:</span> Of course that’s going to then be, it’s a bit of time up front to develop that thing and get it in place, but then you think of the savings of not having human beings manually checking stuff. What things can you see this being put to use for in the future as the technology improves?

<span class="smashing-tv-speaker">Charlie:</span> To me, maybe in the future, I think as models get smaller to load and they get more performant and we probably improve the datasets that they’re trained with. I’m hoping to be able to see tools that are more helpful. I mean, personally, I’m interested in that tiny machine learning models that can run on microcontrollers to build stuff. But if we stay in more of the front-end world, I’m hoping about maybe better voice recognition because I feel like we’re used to navigating the web with a track pad or a keyboard, but at the moment, there is still a voice recognition, but it’s not always super accurate, or it’s not accurate with accents, for example. And I’m hoping that as we develop better models that smaller people won’t be so scared to add it to their website because it won’t impact the performance that badly.

<span class="smashing-tv-speaker">Charlie:</span> I’m interested in using machine learning in stuff like predictive prefetching so that we can build smarter websites that improve the experience on a spectrum, because for the users, it’s better because the page is going to load faster, therefore performance in general of your site, it’s better. But also let’s say if we think about sustainability, not requesting useless resources is helping as well, the carbon footprint of your website. But then there’s also the carbon footprint of machine learning models. That’s not very good. So maybe let’s not talk about this. I would think for the future, I’m just hoping to have models that are maybe more performant or smaller so that people will be more likely to give it a try, because let’s say there’ll be less blockers for people to go into this, but let’s see.

<span class="smashing-tv-host">Drew:</span> Are there known limitations and constraints that we should be aware of before embarking on a machine learning project?

<span class="smashing-tv-speaker">Charlie:</span> Yeah. There are. I think, no matter if you’re doing it in JavaScript or Python, there are limits. I think if you do want to build something, that’s very customed, that there is no pre-trained model for, one of the limits is that you might need quite a lot of data and not everybody has that. So if you’re doing something on your own as a side project, and you can’t find the data set, it would actually take you quite a long time to get one that would allow you to generate good predictions. You can build a small data set, but you will not be able to push it to production or something if you don’t actually have a data set that’s consistent enough. So I think the amount of data that you need, training the models can take a lot of time.

<span class="smashing-tv-speaker">Charlie:</span> That depends on the amount of data that you feed it, but depending on the application that you want to will build it with, you have to be aware that it can take a lot of time. I remember when I got started and I was doing it in Python and I wanted to… I forgot what I wanted to do, but my model was running for, it was training for eight hours. And at the end it told me that it failed because of something. And I was like, “You’re telling me that at the end, after eight hours,” so it can be a bit frustrating and it can still be experimental and you have to be comfortable with it not being a pure science, not everything is always accurate.

<span class="smashing-tv-speaker">Charlie:</span> At the moment, as some of the models are still, they can be a few megabytes, if you are building something that you know, is most likely going to be seen on a mobile screen, you might want to take into consideration that, well, you don’t want to load all that data over 4G network. You might want to warn people that they should be on Wi-Fi or the battery use, or the type of phones can’t really handle all of this as well. And then more seriously in terms of liability, you do have to understand why your model predicted certain things. And that can be difficult because the model is a black box. It’s a function that you don’t really know what’s inside. You know what it predicted and based on what you’re building, if it makes certain decisions about, I don’t know, who gets a loan or who goes to prison, based on whatever, you want to be able to explain how you got to that decision.

<span class="smashing-tv-speaker">Charlie:</span> If you decided to use machine learning to kind of abstract some of the work, so it wouldn’t be done by people. That can be quite dangerous, so you have to know what you’re doing, and in the end, just remember that it’s not perfect. I think people sometimes assume that because we talk about artificial intelligence is just as smart as people, but no, it’s still computers. It’s still data that is given to them and they make up some predictions and somehow we just trust it, which is scary. But yeah, that’s some of the limitations.

<span class="smashing-tv-host">Drew:</span> Yes. I guess it may seem like it’s intelligent, but it is still artificial. There’ve been some quite high profile cases in recent times particularly around some of the machine learning stuff with image recognition that have raised issues of bias in machine learning, for example, a model only detecting humans if they have light skin. Are there ethical considerations that we should be making here?

<span class="smashing-tv-speaker">Charlie:</span> To me, that sounds like a really interesting side of machine learning. And that’s also why, before I was saying that, remember that it’s not perfect. Sometimes I feel like people think that the machine just happens to be right and know all the things by itself, but it’s still something that we program. And when an algorithm products or generates a biased result, the algorithm just generated things based on the data that it was given before. So an algorithm itself or a model is not going to know the difference in society between light-skinned people or dark-skinned people. It doesn’t know and it doesn’t care. The only thing that it knows is that I got given pictures of certain people and I’m just going to generate based on what I know.

<span class="smashing-tv-speaker">Charlie:</span> And the data set that is given to the algorithm is in general generated by us, by people. Maybe it’s not the developer using the model, but at some point somebody put together a data set. And I think it’s important to remember that we are responsible for making sure that the predictions generated are as fair as possible and as unbiased as possible. And that creates interesting questions then, because then you can go into, “Well, what is fair for people?” or if we think about my example of the GitHub action that I created to look at toxic comments, well, maybe what I think is toxic is not the same thing as what other people think is toxic.

<span class="smashing-tv-speaker">Charlie:</span> It’s interesting. There’s a really interesting collection of videos by MIT media lab around the ethics and governance of artificial intelligence, and I find that fascinating because it’s not about telling people, “Oh, you’re a bad person because you used in algorithm that’s biased,” or, “You’re a bad person because you produced a model that’s biased.” Its more about raising certain questions and helping you realize, “Well, actually, maybe I could be better,” because that surface that, “Yes, I forgot to add diverse people to my data set. Let me fix that.” It’s not really about say, “Let’s not use that model ever again.” Just retrain it. Realize that, “Oh, I forgot this. I can retrain it and we can make it better.” And that’s something that I definitely think is interesting.

<span class="smashing-tv-speaker">Charlie:</span> And you have companies really trying to improve on that. When the issue of Google who was translating certain neutral languages into gendered languages, and all of a sudden engineer was male and cook was female. Now they know they’ve really reworked on that and it’s a lot more unbiased and they use the ‘they’ pronoun as well. They also really try to make it better, but then you have also weird stuff where I think IBM had created a data set called Diversity in Faces, that was supposed to be one of the very few that I said that actually had a diverse spectrum of people. But when I tried to find it to use it, it’s not available anymore. So I’m like, “Oh, you had this good initiative. You try to do better than a lot of other people, and now people are going to actually use it.” I don’t know, but I think the question is really fascinating because he can really help us improve. And then we improve the tool as well that we’re using.

<span class="smashing-tv-host">Drew:</span> I guess it pays just to be really careful to be balanced and be diverse when selecting data for training models. I guess that’s what it comes down to, isn’t it?

<span class="smashing-tv-speaker">Charlie:</span> Yeah. Well, I mean, you’re building a tool for the public, in general, right? If it’s a tool that everybody can use, so it should reflect everybody really, or you should be really clear and say, “This tool can only be used by these people because the model was trained that way, but it’s not really what we should do.” I understand that sometimes it if you’ve never thought about it, it can be I don’t know, you can see it as a burden. I hate that people would think of it that way, but it’s also, if you spent all this time, maybe writing your own algorithm or generating your own model and doing all of this work, you can’t tell me that finding a diverse data set is the hardest part. I don’t think it would be. So I’m hopeful, and I think as more people raise concerns about this, and I think people are watching this space, which is really good because if companies don’t do it, they’ll do it if we tell them that it’s not right. And if you want the adoption of machine learning models, you have to make sure that everybody can use them.

<span class="smashing-tv-host">Drew:</span> Of the various tools that are available for doing machine learning in JavaScript, you’ve worked a lot with TensorFlow JS and you’ve written a book about it. Tell us about your book.

<span class="smashing-tv-speaker">Charlie:</span> Yes, I did. I did write a book this year about TensorFlow JS. So to help JavaScript developers learn more about machine learning and understand it better. And I think the main goal of this book was to help people dive into machine learning, but making it less scary, because I know that at first I thought about machine learning as this big thing, completely different from the web development that I would never understand anything about. I didn’t think that I would have to write my own algorithms and really understand math. And as I’ve dived into this over the past two and a half years, I realized that it’s not really like that. And I was hoping that writing this book could help people realize as well that they can do it and what can be done.

<span class="smashing-tv-speaker">Charlie:</span> And there’s also a few projects that you can really put in practice what you’re learning, but it was really aimed at people who haven’t really looked into ML yet, or who just are curious to learn more. I’m not really diving into the algorithms like the source code of the algorithms, but it’s really more telling people, trying to understand what an algorithm does and which one to use and for what. A bit of what we just talked about, but it’s explaining contents in a clear way, so hopefully it’s less scary and people want to hopefully dive a bit more into it.

<span class="smashing-tv-host">Drew:</span> So it’s called Practical Machine Learning In JavaScript and is available from Apress, and we’ll link it up in the show notes. So I’ve been learning all about machine learning today. What have you been learning about lately, Charlie?

<span class="smashing-tv-speaker">Charlie:</span> Let’s say a thing that I’m diving into that is related to machine learning or I will use machine learning with it, but it’s digital signal processing that I want to use with machine learning. As we’ve talked about the fact that machine learning needs a lot of data, if you want to build your own models, sometimes you have to filter your data to actually get the right prediction. And if we think about it, let’s think about noise canceling headphones. In your day-to-day life, you have a lot of noise around you. Let’s say you’re trying to watch a video on the train and there’s people talking around you, and there’s a sound of the train. And what you want to focus on is the sound of the video.

<span class="smashing-tv-speaker">Charlie:</span> With digital signal processing, that would be a little bit like your noise canceling headphones, where there’s some noise around that you don’t care about. So there’s some data that you don’t want to listen to, and the noise canceling headphones allow you to focus on the sound coming from the video on your phone, so that you can really truly listen and focus on that. What I’m doing with digital signal processing is that I have a bunch of data from a piece of hardware, like an Arduino, but I know that there’s a lot of it that I might not care about. I want to filter out the things that I don’t care about, so that then I can feed that to a model and get better predictions about gestures or things like that. So you have your data signal that you can either transform or filter.

<span class="smashing-tv-speaker">Charlie:</span> It’s like when you use the web API to get sound from your microphone, you can either see the arrays of numbers on your dev tools, or you can transform it into a spectrogram to see the picture of the sound. And that’s a little bit of that. To have a better prediction for gestures based on hardware data, I can transform that signal. I’ve been wanting to do this for a couple of years, but it’s something that I know nothing about. It takes time to learn, but now that I know a bit more about the machine learning side, I can learn the digital processing side and I’m getting there. I like this moment where I’m like, “Oh, I start to get it because I spent all this time on it.” And yeah, that’s, that’s really interesting. I’m going to have you going a bit.

<span class="smashing-tv-host">Drew:</span> Charlie you’re such a nerd. If you dear listener would like to hear more from Charlie, you can find her on Twitter, where she’s @devdevcharlie and her personal website includes links to lots of our experiments and projects, and it’s really worth checking out at charliegerard.dev. Her book Practical Machine Learning In JavaScript is available now, and we’ll link to that in the show notes. Thanks for joining us today. Charlie, did you have any parting words?

<span class="smashing-tv-speaker">Charlie:</span> Remember to have some fun. We talked a lot today about fun stuff, and then practical stuff, but if you’re willing to look into this, remember to have some fun, no matter what you decide to build.

{{< signature "il" >}}
