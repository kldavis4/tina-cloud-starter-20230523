---
title: 'Designing For The Future With Voice Prototypes'
slug: future-design-voice-prototypes
author: nickbabich
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cab4235a-a92b-4d11-b90d-69356e5d67a9/nick-babich-voice-prototypes.png
date: 2019-05-02T12:30:16+02:00
summary: >-
 Human-machine communication is rapidly expanding to encompass both written and spoken interaction, and it’s essential to be ready to design for both visual and voice. Since prototyping for voice is new for many designers, it may be unclear as to where to start and what process to follow.
description: >-
  It’s essential to be ready to design for both visual and voice. Since prototyping for voice is new for many designers, it may be unclear as to where to start and what process to follow.
categories:
  - UX
  - Usability
  - Accessibility
  - Voice
disable_ads: true
disable_panels: true
---
(This article is kindly sponsored by Adobe.) Voice-enabled interfaces are challenging the long dominance of graphical user interfaces and are quickly becoming a common part of our daily lives. According to a survey run by Adobe, [76 percent](https://files.acrobat.com/a/preview/1732fe74-8a8e-4438-8153-c5ef5ae15f63) of smart speaker owners increased their usage of voice assistants over the last year.

In this article, I’ll share a flow that you can use to create voice-based experiences. But before we dive into the specific recommendations on how to design for voice, it’s important to understand the user expectations about it.

## Why Do People Expect More From Voice?

Voice User Interfaces (VUIs) not only introduce a change in a way people interact with machines, but they also **raise the bar for the quality of interaction**. When people interact with GUI’s and have troubles with them, they often blame themselves, but when people interact with VUIs and are unable to complete a task, they blame the system.

Why is that? Well, talking is the most naturally convenient medium for communication between people, and people are confident in their talking skills. This can have a direct influence on the retention rate: A 2017 report by Voicelabs states there’s only a [6 percent chance](https://voicebot.ai/2017/09/20/voice-app-retention-doubled-9-months-according-voicelabs-data/) a user will be active in the second week after downloading a voice application.

## Design Process

Many designers think that designing voice-based experiences is completely different from graphical user interfaces. That’s not true.

Designing voice-based experiences is not a new direction in UX design; it’s a next natural step. It’s possible to adapt the design process that we use for visual interfaces for voice-based products.

There are five steps should take place before starting development a voice product:

<ol>
	<li><a href="#research">Research</a></li>
	<li><a href="#define">Define</a></li>
	<li><a href="#create">Create</a></li>
	<li><a href="#test">Test</a></li>
	<li><a href="#refine">Refine</a></li>
</ol>

The great thing about this process is that it can be applied to all types of voice interfaces, whether it is a voice-enabled, voice-only or voice-first.

### 1. Research

Similar to any other digital product we design, we need to apply user-first design in the context of voice user interfaces. The goal of user research is to understand the needs and behaviors of the target user. The information you gather during this step will be a foundation for product requirements.

#### Identify The Target Audience

Defining and researching the target audience of a product should be one of the first steps in the design process.

Here’s what to focus on during this step:

- Look at the current experience and how the users are solving their problem now. By **identifying pain points**, you’ll find the cases where voice can benefit your users.
- **User language**. The exact phrases that a target user uses when they speak with other people. This information will help us to design a system for different utterances.

### 2. Define

During this step, we need to shape our future product and define its capabilities.

#### Define Key Scenarios Of Interaction

Scenarios come before specific ideas for app &mdash; they’re a way to think about the reasons someone might have to use a VUI. You need design scenarios that have high value for your target users. If you have many scenarios and do not know which ones are important and which are not, create use case matrix to evaluate each individual scenario. The matrix will tell you what scenarios are primary, what are secondary what are nice-to-haves.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d189fcd9-cb1a-4f88-bdd2-5220456daf5d/1-designing-with-voice-prototypes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d189fcd9-cb1a-4f88-bdd2-5220456daf5d/1-designing-with-voice-prototypes.png" sizes="100vw" caption="Applying use case matrix to voice interactions. Image: <a href='https://medium.muz.li/voice-user-interfaces-vui-the-ultimate-designers-guide-8756cb2578a1'>Justin Baker</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d189fcd9-cb1a-4f88-bdd2-5220456daf5d/1-designing-with-voice-prototypes.png'>Large preview</a>)" alt="voice interactions use cases" >}}

#### Make Sure Key Scenarios Work With Voice

There should be a compelling reason to use voice. Users should be able to solve the problem faster or more efficiently using voice than any of the alternative experiences.

A few common cases when voice interaction might be preferable for users:

- When user’s hands are busy (while driving or cooking);
- When using voice is an easier and more natural way to interact (for example, it’s much easier to tell your smart speaker to "Play Jazz" rather than jump to a media center and select the right option using a GUI).

Your goal for this step is to identify both common and specific cases that your users will benefit from. It’s also important to consider the limitations of voice interactions. For example, selecting from a long list of menu items is problematic with voice interactions. A good rule of thumb is to keep choices short and to the point &mdash; 3 selections maximum. If you find you have more than 3, it’s best to reframe the scenario.

### 3. Create

With voice prototypes, it’s important to start at the drawing board. The first step is to tackle the voice user flows of your experience, which is the basis from which all user interaction will map back to.

#### Use Storyboards

Storyboards visualize interactions and flows in context and make them feel more realistic.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcadb21-32dd-4db3-8cd9-214edbfd4e6b/4-designing-with-voice-prototypes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcadb21-32dd-4db3-8cd9-214edbfd4e6b/4-designing-with-voice-prototypes.png" sizes="100vw" caption="A storyboard that illustrate the flow. Image: <a href='https://www.bbc.co.uk/rd/blog/2017-06-voice-ui-user-interface-children-drama'>BBC</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcadb21-32dd-4db3-8cd9-214edbfd4e6b/4-designing-with-voice-prototypes.png'>Large preview</a>)" alt="storyboard" >}}

#### Write Dialogues

Dialogues are the building blocks of voice user flows. For each key scenario that the voice app will support, start creating conversational dialogues between the user and the app.
Strive to make interacting with the app as familiar as having a regular conversation with a real person. Human conversation is complex; it often has many twists and turns. It will be important to take this into account when working through your scenarios and writing dialogues.

A few general recommendations for creating great dialogues:

- **Reduce the number of steps it takes to complete a task.**  
Try to eliminate unnecessary information and questions wherever possible. Design should solve the user’s problem with the minimum number of steps. Remember that the longer it takes to complete the task, the less enjoyable the experience becomes. No one likes products that drain on their valuable time, and this is especially true for repetitive tasks. Your app should provide a delightful user experience whether it’s the first time a user completes the task, or it’s the 100th time this month.
- **Don’t teach “commands”.**  
Given how hard discovery can be in voice, some designers try to teach users commands so they know what to say. Don’t do that. Phrasing should be natural and intuitive, so users will know what to say in particular situations.
- **Be brief with your questions and responses.**  
It’s relatively easy to overload users with too much information when you use long sentences. Try to simplify messages to their essence wherever possible. Users enjoy concise and well-defined information from VUI.
Think about what information is primary, and what information is secondary. Follow the principle of Maximum of Quantity which says that a speaker provides the listener as much information as is necessary to advance the perceived purpose of the interaction but not too much.

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/wuDP_eygsvs" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

Here is a dialogue that doesn’t follow the principle of Maximum of Quantity:

<blockquote><strong>User</strong>: “Where’s a good place to go for pizza?”<br /><br /><strong>System</strong>: “I have five places for you. The first one is “Pizza & Pasta” is located on 1300-1398 Diamond St San Francisco, 15 minutes away from you, open from 8:00 AM till 8:00 PM, the second is “Italy” which is located on 4100-4148 20th St San Francisco, 1 hour away from you, open from 9:00 AM till 6:00 PM,...”</blockquote>

The dialogue tries to present all options in a single turn. It’s better to try to narrow down the list by asking a clarifying question:

<blockquote><strong>User</strong>: “Where’s a good place to go for pizza?”<br /><br /><strong>System</strong>: “There are several pizza restaurants in the area &mdash; would you like to walk, or drive?”</blockquote>

#### Handle Errors

No matter how good your VUI will be, one thing is for sure: things will go wrong. And you need to design for those situations. Graceful handling of errors is one of the biggest challenges you'll face when designing for voice and it’s vital to start thinking about it right at the time when you write your dialogues.

Here are a few common cases that can cause error states:

- **Misspellings**  
Some users can mispronounce words and the natural language processing system won’t understand the request.
- **Ambiguity**  
Even between humans, speech is sometimes ambiguous. For example, someone might say “Good” and that could be defined as ‘Yes, I agree’ or just be an indication that they're listening.
- Cases when **the system is unable to provide valuable information for users**. For example, the user wants to book a flight, but the system doesn’t have relevant options.

In all cases, the dialogue shouldn’t end up in a dead end; the system should provide valuable options. Always try to get the dialog back on track.

Let’s check out the first example:

<blockquote><strong>User</strong>: “Book me a flight from San Diego to Dallas on Monday.”<br /><br /><strong>System</strong>: “I couldn’t find any flights from San Diego to Dallas on Monday.”</blockquote>

It’s evident that users face a dead end. However, it’s relatively easy to modify the dialog to provide some options for users:

<blockquote><strong>User</strong>: “Book me a flight from San Diego to Dallas on Monday.”<br /><br /><strong>System</strong>: “I couldn’t find any flights from San Diego to Dallas on Monday. Would you like to search for another date?”</blockquote>

Another example for food ordering app:

<blockquote><strong>User</strong>: “What’s the ZIP code for delivery?”<br /><br /><strong>System</strong>: “Hmm, 811415”<br /><br /><strong>User</strong>: “This ZIP is invalid. Try again.”</blockquote>

Not only the word “Invalid” is too technical, but it also doesn’t help get the user back on track. It’s better to offer a user a hint so they can understand what they should do next:

<blockquote><strong>System</strong>: “What’s the ZIP code for delivery?”<br /><br /><strong>User</strong>: “Hmm, 811415”<br /><br /><strong>System</strong>: “This ZIP is longer than expected. It should be five digits, not six.“<br /><br /><strong>User</strong>: “81415”</blockquote>

#### Reflect Your Unique Identity

All voices project a persona whether you plan for one or not. Don’t leave your VUI persona to chance, reflect your unique brand and identity in dialogues you write. Imagine how your ideal employee should interact with customers and try to reflect it in the wording of your dialogues.

Tone of voice has [measurable impacts](https://www.nngroup.com/articles/tone-voice-users/) on users’ perceptions of a product. That’s why it’s important to consider the emotional needs of your users when choosing a tone.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b349ad9-8c5b-40d6-9c37-60c186a6213b/2-designing-with-voice-prototypes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b349ad9-8c5b-40d6-9c37-60c186a6213b/2-designing-with-voice-prototypes.png" sizes="100vw" caption="A product’s tone of voice can be expressed as a function of the 4 tone dimensions. Image: <a href='https://www.nngroup.com/articles/tone-voice-users/'>NNGroup</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b349ad9-8c5b-40d6-9c37-60c186a6213b/2-designing-with-voice-prototypes.png'>Large preview</a>)" alt="" >}}

#### Bake Empathy In Interactions

Voice interfaces should take user emotions into account. People like not only friendly people but also friendly computers. For example, when someone wants to book a ticket for a flight and provides information about a trip, the system might respond ‘Sounds like a fun trip!’ The response should be slightly different each time to prevent a feeling of interaction with a machine.

#### Confirm When A Task Has Been Completed

It’s vital to think about where in the conversation flow the users need confirmations. Usually, people expect a final confirmation at the end of a dialogue. For example, when a user schedules an event, they might want to hear the “The event is on your calendar now.”
Another typical scenario is a checkout flow &mdash; let the user know that the transaction has been successfully recorded.

Use explicit confirmation for important actions and implicit for routine tasks. For example, if you ask your Alexa to send money to your friend, a user probably wants to hear “The [amount of money] was sent to [name of the person]” rather than just “OK.” At the same time, when you ask Alexa to turn off the lights in a garage, hearing “The lights in the garage are off” all the time might be too much, so be sure to test confirmations carefully to find out what confirmations your users feel is critical in order to feel successful with the VUI.

#### Leverage Context

A good conversational system keeps track of the dialog, memorizing all previous turns and of previous interactions. A solid system will use this information to create a better experience for users by offering a more personalized experience.

For example, when a user orders pizza, the system might remind them about their previous order:

<blockquote><strong>User</strong>: “I want to order a pizza.”<br /><br /><strong>System</strong>: “Last time you ordered Quattro Formaggio from Pizza & Pasta. Do you want to order it again?”<br /><br /><strong>User</strong>: “Yay, I do!”</blockquote>

#### Cover Alternate Phrases

People can use different words to describe the same thing, and it’s vital to take this moment into account when designing your VUI. For each voice user flow that you designed in the previous step, think about the different ways users could phrase those requests. Consider word variations and synonyms that they might use.

Depending on the capabilities of your voice product, the number of utterances that users can vocalize when interacting with VUI can easily run into the hundreds, making the task of mapping them out really complex. Fortunately, there are special tools available to help you with that. For example, if you design apps for Alexa, you can use <a href="https://www.makermusings.com/2015/07/21/defining-utterances-for-the-alexa-skills-kit/">Amazon Echo Utterance Expander</a> for that purpose.

#### Test Your Dialogues

Now when you have all your dialogues written, it’s time to start testing them. Why? Because the way we speak is far less formal than the way we write. To make sure you design dialogues that sound natural, it’s vital to test them before moving to prototyping.
Two simple techniques will help you do it:

- Record and play audio with your dialogs. You’ll hear nuances of words and sentences that just aren’t natural.
- Role play conversations to make sure they're natural and intuitive. A technique called ‘[Wizard of Oz](https://en.wikipedia.org/wiki/Wizard_of_Oz_experiment)’ will help you quickly identify the problems in your dialogues. If you’re Mac user, you can use a tool called [Say Wizard](https://github.com/bensauer/saywizard) to make things easier.

#### Prototype Your App

Now that we’ve written, mapped and tested our dialogues we can finally move on to designing and prototyping the experience. [Adobe XD](https://bit.ly/smvoiceprototypesxd) makes it easy for designers to create a working prototype for voice-enabled Amazon or Google apps and test it with real users. The tool allows you to prototype the actual voice inputs and outputs for the app.
A typical interaction consists of user input and system responses:

- To design user requests, we need to create voice triggers. To add a new voice trigger, drag a connector from an element in one artboard to another. When the attributes menu opens, select `Voice` from Trigger menu and add your utterance in the Command field.
- `Speech Playback` will simulate the response of the voice app. To add Speech Playback, you need to select Time as the `Trigger` and set the action to `Speech Playback`.

{{< vimeo id="295154444" caption="Prototyping with Voice in Adobe XD" >}}

Adobe XD allows you to prototype for voice-first products like the Amazon Echo Show, and voice-only products such as Google Home.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">A few folx have asked about voice-only prototypes in <a href="https://twitter.com/hashtag/adobexd?src=hash&amp;ref_src=twsrc%5Etfw">#adobexd</a> - below I made a quick prototype of a Google Home timer in XD using:<br><br>🔸Vector file from Illustrator to XD<br>🔸Auto Animate for the lights  <br>🔸Voice Command as trigger <br>🔸Speech Response <br><br>...no screen, no problem 😉 <a href="https://t.co/pz3pEvZVmZ">pic.twitter.com/pz3pEvZVmZ</a>&mdash; Susse Sønderby (@SusseSonderby) <a href="https://twitter.com/SusseSonderby/status/1054758504945328128?ref_src=twsrc%5Etfw">October 23, 2018</a></blockquote>

<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
Last but not least, if you design Amazon Alexa Skill for Amazon Echo Show or Amazon Echo Spot, XD provides a VUI kit for those devices. You can <a href="https://adobe.ly/xdvoiceuikit">download it here</a>. This VUI kit provides all the building blocks you need to get started building an Alexa skill.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c56b89-2504-41b1-910a-a490fabc1569/3-designing-with-voice-prototypes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c56b89-2504-41b1-910a-a490fabc1569/3-designing-with-voice-prototypes.png" sizes="100vw" caption="VUI kit for Amazon Echo Show and Spot. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c56b89-2504-41b1-910a-a490fabc1569/3-designing-with-voice-prototypes.png'>Large preview</a>)" alt="" >}}

### 4. Test

Testing is a mandatory part of the design process. Without testing, you can’t say whether your app will work for your users or not.

#### Test Your Prototypes With Target Users

Conduct usability testing sessions with representatives from your target audience, and observe how users interact with your app. Track the tasks completion rate and CSAT (Customer Satisfaction Score). If possible, try to record a video for each session.

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/eD4x4gj4u2Y" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

#### Use Test Simulators

Both <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/testing-an-alexa-skill#h2_servicesim">Amazon</a> and <a href="https://developers.google.com/actions/tools/simulator">Google</a> provide testing tools that let you test your Skill or Action in simulation of the hardware devices and their settings. This testing will give you a good feel for the voice experience in the real world.

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/OHZWVEEIkFI" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

### 5. Refine

Refine the voice application after sending it to the market.

#### Collect Analytics

Once you’ve rolled out your app, you should track how the app is being used with analytics. Here are some of the key metrics to keep an eye out for are:

- Intents and utterances,
- User engagement metrics,
- Behavior flows.

Most of the metrics you need you will find within your *Skill developer* account without any additional coding.

## Conclusion

Human-computer interaction has never been about graphical user interfaces. First and foremost, it has always been about communication. It’s evident that **voice will be a natural way for the new generation of users to interact with technology**, and as a designer, you should be ready for these new challenges and the opportunities they unlock for new ways of looking at interaction design.

*This article is part of the UX design series sponsored by Adobe. Adobe XD tool is made for a [fast and fluid UX design process](https://bit.ly/smvoiceprototypesxd), as it lets you go from idea to prototype faster. Design, prototype and share — all in one app. You can check out more inspiring projects created with [Adobe XD on Behance](https://www.behance.net/galleries/adobe/5/XD), and also [sign up for the Adobe experience design newsletter](https://adobe.ly/2yKueO8) to stay updated and informed on the latest trends and insights for UX/UI design.*

{{< signature "yk, il" >}}
