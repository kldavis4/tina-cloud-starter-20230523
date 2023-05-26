---
title: 'The Rise Of Intelligent Conversational UI'
slug: rise-intelligent-conversational-ui
author: burke-holland
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26d209f-fd5f-417e-92e6-9479dac38632/github-bot.png
date: 2018-04-05T13:00:48+02:00
summary: >-
  Conversational UI is not a new concept. Technologies such as *Natural Language Processing* are key to delivering great a conversational UI, and we're finally to the point where everyone can use it, regardless of skill level.
description: >-
  Conversational UI is not a new concept. Technologies such as *Natural Language Processing* are key to delivering great a conversational UI, and we're finally to the point where everyone can use it, regardless of skill level.
categories:
  - UI
  - Graphic Design
  - Interfaces
  - Chatbots
  - User Interaction
---
For a long time, we’ve thought of interfaces strictly in a visual sense: buttons, dropdown lists, sliders, carousels (please no more carousels). But now we are staring into a future composed not just of visual interfaces, but of conversational ones as well. Microsoft alone reports that three thousand new bots are built every week on their [bot framework](https://dev.botframework.com/?WT.mc_id=luis-smashing-buhollan). Every. Week.

The importance of Conversational UI cannot be understated, even if some of us wish it wasn’t happening.

The most important advancement in Conversational UI has been **N**atural **L**anguage **P**rocessing (NLP). This is the field of computing that deals not with deciphering the exact words that a user said, but with parsing out of it their actual intent. If the bot is the interface, NLP is the brain. In this article, we’re going to take a look at why NLP is so important, and how you (*yes, you!*) can build your own.

## Speech Recognition vs. NLP

Most people will be familiar with Amazon Echo, Cortana, Siri or Google Home, all of which have an interface that is primarily conversational. They are also all using NLP.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c5bc3d5-bb83-44de-a481-1b87be2d4c87/intelligent-assistants.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c5bc3d5-bb83-44de-a481-1b87be2d4c87/intelligent-assistants.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c5bc3d5-bb83-44de-a481-1b87be2d4c87/intelligent-assistants.png'>Large preview</a>" alt="" >}}

Aside from these intelligent assistants, most Conversational UIs have nothing to do with voice at all. They are text driven. These are the bots we chat with in Slack, Facebook Messenger or over SMS. They deliver high quality gifs in our chats, watch our build processes and even manage our pull requests.

{{% feature-panel %}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26d209f-fd5f-417e-92e6-9479dac38632/github-bot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26d209f-fd5f-417e-92e6-9479dac38632/github-bot.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f26d209f-fd5f-417e-92e6-9479dac38632/github-bot.png'>Large preview</a>" alt="" >}}

Conversational UIs built on text are nice because there is no speech recognition component. The text is already parsed.

When it comes to a verbal interaction, the fundamental problem is not recognizing the speech. We’ve mostly got that one down.

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/JUM3uuAqBV0" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

OK, so maybe it’s not perfect. I still get voicemails every day like a game of *Mad Libs* that I never asked to play. iOS just sticks a blank line in whenever they don’t know what exactly was said.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbc2b2fa-6dc0-404e-9f76-7fa159941250/bad-voicemail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbc2b2fa-6dc0-404e-9f76-7fa159941250/bad-voicemail.png" sizes="60vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbc2b2fa-6dc0-404e-9f76-7fa159941250/bad-voicemail.png'>Large preview</a>" alt="" >}}

Google, on the other hand, just tries to guess. Like this one from my father. I have absolutely no idea what this message is actually trying to say other than “Be Safe” which honestly sounds like my mom, and not my dad. I have a hard time believing he ever said that. I don’t trust the computer.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/502ff828-f384-4d5a-9820-969b47e0832b/google-voice.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/502ff828-f384-4d5a-9820-969b47e0832b/google-voice.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/502ff828-f384-4d5a-9820-969b47e0832b/google-voice.png'>Large preview</a>" alt="" >}}

I’m picking on voice mail transcriptions here, which might be the hardest speech recognition to do given how degraded the audio quality is.

Nevertheless, speech recognition *is* largely a solved problem. It’s even built right into Chrome and it works remarkably well.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ed9098e-781f-4e09-aad8-b1d9ae9f5be1/chrome-speech.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ed9098e-781f-4e09-aad8-b1d9ae9f5be1/chrome-speech.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ed9098e-781f-4e09-aad8-b1d9ae9f5be1/chrome-speech.png'>Large preview</a>" alt="" >}}

After we solved the problem of speech recognition, we started to use it everywhere. That was unfortunate because speech recognition on it’s own doesn’t do us a whole lot of good. Interfaces that rely soley on speech recognition require the user to state things a precise way and they can only state the limited number of exact words or phrases that the interface knows about. This is not natural. This is not how a conversation works.

Without NLP, Conversational UI can be true nightmare.

## Conversational UI Without NLP

We’re probably all familiar with automated phone menus. These are known as **I**nteractive **V**oice **R**esponse systems &mdash; or IVRs for short. They are designed to take the place of the traditional operator and automatically transfer callers to the right place without having to talk to a human. On the surface, this seems like a good idea. In practice, it’s mostly just you waiting while a recorded voice reads out a list of menu items that “may have changed.”

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b642c61-61bc-490e-9eba-db290977df5c/scream.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b642c61-61bc-490e-9eba-db290977df5c/scream.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b642c61-61bc-490e-9eba-db290977df5c/scream.png'>Large preview</a>" alt="" >}}

A [2011 study from New York University](https://www.interactions.com/press-releases/consumer-study-finds-overwhelming-dissatisfaction-with-ivr/) found that 83% of people feel IVR systems “provide either no benefit at all, or only a cost savings benefit to the company.” They also noted that IVR systems “score lower than any other service option.” People would literally rather do anything else than use an automated phone menu.

NLP has changed the IVR market rather significantly in the past few years. NLP can pick a user’s intent out of anything they say, so it’s better to just let them say it and then determine if you support the action.

Check out how AT&T does it.

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/ihYCDzqFZ54" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

AT&T has a truly intelligent Conversational UI. It uses NLP to let me just state my intent. Also, notice that I don't have to know what to say. I can fumble all around and it still picks out my intent.

AT&T also uses information that it already has (my phone number) and then leverages text messaging to send me a link to a traditional visual UI, which is probably a much better UX for making a payment. NLP drives the whole experience here. Without it, the rest of the interaction would not be nearly as smooth.

NLP is powerful, but more importantly, it is also accessible to developers everywhere. You don’t have to know a thing about Machine Learning (ML) or Artificial Intelligence (AI) to use it. All you need to how to do is make an AJAX call. Even I can do that!

## Building An NLP Interface

So much of Machine Learning still remains inaccessible to developers. Even the best YouTube videos on the subject quickly become hard to follow with subjects like *Neural Networks* and *Gradient Descents*. We have, however, made significant progress in the field of Language Processing, to the point that it’s accessible to developers of nearly any skill level.

Natural Language Processing differs based on the service, but the overall idea is that the user has an intent, and that intent contains entities. That means exactly nothing to you at the moment, so let’s work up a hypothetical Home Automation bot and see how this works.

## The Home Automation Example

In the field of Natural Language Processing, the canonical “Hello World” is usually a Home Automation demo. This is because it helps to clearly demonstrate the fundamental concepts of NLP without overloading your brain.

A Home Automation Bot is a service that can control hypothetical lights in a hypothetical house. For instance, we might want to say “Turn on the kitchen lights”. That is our intent. If we said “Hello”, we are clearly expressing a different intent. Inside of that intent, there are two pieces of information that we need to complete the action:

1. The ‘Location’ of the light (kitchen)
2. The desired state of the lights ‘Power’ (on/off)

These (Location, Power) are known as entities.

When we are finished designing our NLP interface, we are going to be able to call an HTTP endpoint and pass it our intent: “Turn on the kitchen lights.” That endpoint will return to us the intent (Control Lights) and two objects representing our entities: Location and Power. We can then pass those into a function which actually controls our lights…

<pre><code class="language-javascript">function controlLights(location, power) {
  console.log(`Turning ${power} the ${location} lights`);

  // TODO: Call an imaginary endpoint which controls lights
}
</code></pre>

There are a lot of NLP services out there that are available today for developers. For this example, I’m going to show the [LUIS](https://www.luis.ai/home?WT.mc_id=luis-smashing-buhollan) project from Microsoft because it is free to use.

LUIS is a completely visual tool, so we won’t actually be writing any code at all. We’ve already talked about Intents and Entities, so you already know most of the terminology that you need to know to build this interface.

The first step is to create a “Control Lights” intent in LUIS.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417710b9-4bae-45ec-8a5b-a941476feb28/control-lights.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417710b9-4bae-45ec-8a5b-a941476feb28/control-lights.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417710b9-4bae-45ec-8a5b-a941476feb28/control-lights.png'>Large preview</a>" alt="" >}}

Before I do anything with that intent, I need to define my Location and Power entities. Entities can be different types &mdash; kind of like types in a programming language. You can have dates, lists and even entities that are related to other entities. In this case, Power is a list of values (on, off) and Location is a simple entity, which can be any value.

It will be up to LUIS to be smart enough to figure out exactly *what* the Location is.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fa12dd0-4290-47a6-9c84-f8b8e2e24615/create-entities.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fa12dd0-4290-47a6-9c84-f8b8e2e24615/create-entities.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fa12dd0-4290-47a6-9c84-f8b8e2e24615/create-entities.png'>Large preview</a>" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77fdc4d6-1ba1-4178-8833-76388bb395f5/power-entity.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77fdc4d6-1ba1-4178-8833-76388bb395f5/power-entity.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77fdc4d6-1ba1-4178-8833-76388bb395f5/power-entity.png'>Large preview</a>" alt="" >}}

Now we can begin to train this model to understand all of the different ways that we might ask it to control the lights in a different location. Let’s think of all the different ways that we could do that:

- Turn off the kitchen lights;
- Turn off the lights in the office;
- The lights in the living room, turn them on;
- Lights, kitchen, off;
- Turn off the lights (no location).

As I feed these into the Control Lights intent as utterances, LUIS tries to determine where in the intent the entities are. You can see that because Power is a discreet list of values, it gets that right every time.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78d7d128-e147-4cc0-8f0e-0f4d3e7ee4b1/control-lights-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78d7d128-e147-4cc0-8f0e-0f4d3e7ee4b1/control-lights-1.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78d7d128-e147-4cc0-8f0e-0f4d3e7ee4b1/control-lights-1.png'>Large preview</a>" alt="" >}}

But it has no idea what a Location even is. LUIS wants us to go through this list and tell it where the Location is. That’s done by clicking on a word or group of words and assigning to the right entity. As we are doing this, we are really creating a machine learning model that LUIS is going to use to statistically estimate what qualifies as a Location.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/547ee534-5a9a-4dec-92b6-3e1da83d4994/control-lights-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/547ee534-5a9a-4dec-92b6-3e1da83d4994/control-lights-2.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/547ee534-5a9a-4dec-92b6-3e1da83d4994/control-lights-2.png'>Large preview</a>" alt="" >}}

When I’m done telling LUIS where in these utterances all the locations are, my dashboard looks like this…

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a33cba90-397a-4ce1-b46b-e68d068980fa/control-lights-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a33cba90-397a-4ce1-b46b-e68d068980fa/control-lights-3.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a33cba90-397a-4ce1-b46b-e68d068980fa/control-lights-3.png'>Large preview</a>" alt="" >}}

Now we train the model by clicking on the “Train” button at the top. Do you feel like a data scientist yet?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af4d62e0-7158-474d-86b6-c52df146a151/training-luis.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af4d62e0-7158-474d-86b6-c52df146a151/training-luis.gif" width="800" alt="" /></a></figure>

Now I can test it using the test panel. You can see that LUIS is already pretty smart. The Power is easy to pick out, but it can actually pick out Locations it has never seen before. It's doing what your brain does &mdash; using the information that it has to make an educated guess. Machine Learning is equal parts impressive and scary.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/833d086a-fd5c-407a-9964-d248dda99331/scary-impressive.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/833d086a-fd5c-407a-9964-d248dda99331/scary-impressive.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/833d086a-fd5c-407a-9964-d248dda99331/scary-impressive.png'>Large preview</a>" alt="" >}}

If we try hard enough, we can fool the AI. The more utterances we give it and label, the smarter it will get. I added 35 utterances to mine before I was done and it is close to bullet proof.

So now we get to the important part, which is how we actually use this NLP in an app. LUIS has a “Publish” menu option which allows us to publish our model to the internet where it’s exposed via a single HTTP endpoint. It will look something like this…

<div class="break-out">

<pre><code class="language-bash">https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/c4396135-ee3f-40a9-8b83-4704cddabf7a?subscription-key=19d29a12d3fc4d9084146b466638e62a&amp;verbose=true&amp;timezoneOffset=0&amp;q=</code></pre></div>

The very last part of that query string is a `q=` variable. This is where we would pass our intent.

<div class="break-out">

<pre><code class="language-bash">https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/c4396135-ee3f-40a9-8b83-4704cddabf7a?subscription-key=19d29a12d3fc4d9084146b466638e62a&amp;verbose=true&amp;timezoneOffset=0&amp;q=turn on the kitchen lights</code></pre></div>

The response that we get back looks is just a JSON object.

<pre><code class="language-javascript">{
  "query": "turn on the kitchen lights",
  "topScoringIntent": {
    "intent": "Control Lights",
    "score": 0.999999046
  },
  "intents": [
    {
      "intent": "Control Lights",
      "score": 0.999999046
    },
    {
      "intent": "None",
      "score": 0.0532306843
    }
  ],
  "entities": [
    {
      "entity": "kitchen",
      "type": "Location",
      "startIndex": 12,
      "endIndex": 18,
      "score": 0.9516622
    },
    {
      "entity": "on",
      "type": "Power",
      "startIndex": 5,
      "endIndex": 6,
      "resolution": {
        "values": [
          "on"
        ]
      }
    }
  ]
}
</code></pre>

Now this is something that we can work with as developers! This is how you add NLP to any project &mdash; with a single REST endpoint. Now you’re free to create a bot with some real brains!

[Brian Holt](https://www.twitter.com/holtbt) used the browser speech API and a LUIS model to create a voice powered calculator that is running right inside of CodePen. Chrome is required for the speech API.

{{< codepen height="480" theme_id="light" slug_hash="JMwQYg" default_tab="result" user="btholt" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/btholt/pen/JMwQYg/">Voice Calculator</a> by Brian Holt (<a href="https://codepen.io/btholt">@btholt</a>) on <a href="https://codepen.io">CodePen</a>. {{< /codepen >}}

## Bot Design Is Still Hard

Having a smart bot is only half the battle. We still need to account for any of the actions that our system might expose, and that can lead to a lot of different logical paths which makes for messy code.

Conversations also happen in stages, so the bot needs to be able to intelligently direct users down the right path without frustrating them or being unable to recover when something goes wrong. It needs to be able to recover when the conversation dies midstream and then starts again. That’s a whole other article and I’ve included some resources below to help.

When it comes to language understanding, the AI platforms are mature and ready to use today. While that won’t help you perfectly design your bot, it will be a key component to building a bot that people don’t hate.

### Great UI Is Just Great UI

**A final note:** As we saw from the AT&amp;T example, a *truly* smart interface combines great speech recognition, Natural Language Processing, different types of conversational UI (speech and text) and even a visual UI. In short, great UI is just that &mdash; great UI &mdash; and it is not a zero sum game. Great UIs will leverage all of the technology available to provide the best possible user experience.

*Special thanks to [Mat Velloso](https://twitter.com/matvelloso) for his input on this article.*

### Further Resources:

- “[Principles Of Bot Design](https://docs.microsoft.com/en-us/bot-framework/bot-service-design-principles?wt.mc_id=luis-smashing-buhollan),” Microsoft Azure (*Doc written by Mat Velloso, Kamran Iqbal, and Robert Standefer*)
- “[Conversational Design Essentials: Tips For Building A Chatbot](https://www.smashingmagazine.com/2016/12/conversational-design-essentials-tips-for-building-a-chatbot/),” Anton Skorniakov, Smashing Magazine
- “[Language Understanding Tutorials](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/?WT.mc_id=luis-smashing-buhollan),” LUIS, Microsoft Azure

{{< signature "rb, ra, yk, il" >}}

