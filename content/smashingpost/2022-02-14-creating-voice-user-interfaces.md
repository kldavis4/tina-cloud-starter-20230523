---
title: 'Everything You Want To Know About Creating Voice User Interfaces'
slug: voice-user-interfaces-guide
author: nickbabich-glebkuznetsov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1470bd2f-c151-4408-8f43-0a7d76a67249/voice-user-interfaces-guide.jpg
date: 2022-02-14T13:30:00.000Z
summary: >-
  Creating voice user interfaces requires a lot of design expertise in various areas such as conversation design, interaction design, visual and motion design. This article covers the most critical aspects of designing for voice user interfaces &mdash; designing the conversation and designing visual interfaces.
description: >-
  Voice is a powerful tool that we can use to communicate with each other. This article covers the most critical aspects of designing for voice user interfaces: designing the conversation and designing visual interfaces.
categories:
  - UI
  - Voice
  - User Experience
---

Voice is a powerful tool that we can use to communicate with each other. Human conversations inspire product designers to create voice user interfaces (VUI), a next-generation of [user interfaces](https://www.smashingmagazine.com/category/ui) that gives users the power to interact with machines using their natural language.

For a long time, the idea of controlling a machine by simply talking to it was the stuff of science fiction. Perhaps most famously, in 1968 Stanley Kubrick released a movie called *2001: A Space Odyssey*, in which the central antagonist wasn’t a human. HAL 9000 was a sophisticated artificial intelligence controlled by voice.

{{< youtube id="Wy4EfdnMZ5g" caption="HAL 9000, a voice assistant from the movie “2001: A Space Odyssey”. (<a href='https://www.youtube.com/watch?v=Wy4EfdnMZ5g'>Watch video on YouTube</a>)" >}}

Since then the progress in natural language processing and machine learning has helped product creators introduce less murderous voice user interfaces in various products &mdash; from mobile phones to smart home appliances and automobiles.

## A Brief History Of Voice Interfaces

If we go back to the real world and analyze the evolution of VUI, it’s possible to define three generations of VUIs. The first generation of VUI is dated to the 1950s. In 1952, Bell Labs built a system called Audrey. The system derived its name from its ability to decode digits &mdash; Automatic Digit Recognition. Due to the tech limitations, the system could only recognize the spoken numbers of “0” through “9”. Yet, Audrey proved that VUIs could be built.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7fcffc0-91a0-4683-9761-e2667ed29748/9-creating-voice-user-interfaces.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7fcffc0-91a0-4683-9761-e2667ed29748/9-creating-voice-user-interfaces.jpg" width="800" height="418" sizes="100vw" caption="1952 Bell Labs Audrey. The photo shows only input and output controls but doesn’t show supportive electronics. (Image credit: <a href='https://computerhistory.org/blog/audrey-alexa-hal-and-more/'>Computerhistory</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7fcffc0-91a0-4683-9761-e2667ed29748/9-creating-voice-user-interfaces.jpg'>Large preview</a>)" alt="Bell Labs Audrey with input and output controls." >}}

The second generation of VUIs dates to the 1980s and 1990s. It was the era of Interactive voice response (IVR). One of the first IVRs was developed in 1984 by Speechworks and Nuance, mainly for telephony, and they revolutionized the business. For the first time in history, a digital system could recognize human voice-over calls and perform the tasks given to them. It was possible to get the status of your flight, make a hotel booking, transfer money between accounts using nothing more than a regular landline phone and the human voice.

{{< youtube id="A8BVjgjA5Ek" breakout="true" caption="What is IVR? (Video credits: <a href='https://www.youtube.com/watch?v=A8BVjgjA5Ek'>YouTube</a>)" >}}

The third (and current) generation of VUIs started to get traction in the second decade of the 21st century. The critical difference between the 2nd and 3rd generations is that voice is being coupled with AI technology. Smart assistants like Apple Siri, Google Assistant, and Microsoft Cortana can understand what the user is saying and offer suitable options. This generation of VUIs is available in various types of products &mdash; from mobile phones to car human-machine interfaces (HMIs). They are fast becoming the norm.

{{< vimeo id="671156958" caption="Voice coupled with AI technology. (Video credit: <a href='https://dribbble.com/shots/5987739-EV-battery-charging-status'>Gleb Kuznetsov</a>)" breakout="true" >}}

{{% feature-panel %}}

## Six Fundamental Properties Of VUI Design

Before we move to specific design recommendations, it’s essential to state the basic principles of good VUI design. 

### 1. Voice-first Design

You need to design hands-free and eyes-free user interfaces. Even when a VUI device has a screen, we should always design for voice-first interactions. While the screen can complement the voice interaction, the user should be able to complete the operation with minimum or no look at the screen. 

Of course, some tasks become inefficient or impossible to complete by voice alone. For example, having users listen and browse through search results by voice can be tedious. But you should avoid creating an action that relies on users interacting with a screen alone. If you design one of those tasks, you need to consider an experience where your users start with voice and then switch to a visual or touch interface. 

### 2. Natural Conversation

The interaction with VUI shouldn’t feel like an interaction with a robot. The conversation flow should be user-centric (resembling natural human conversation). The user shouldn’t have to remember specific phrases to get the system to do what they want to do. 

It’s important to use everyday language and invite users to say things in the ways they usually do. If you notice that you have to explain commands, it’s a clear indication that something is wrong with your design and you need to go back to the drawing board and redesign it. 

### 3. Personalization

Personalization is more than just saying “Welcome back, %username%”. Personalization is about knowing genuine user needs and wants and adapting information to them. VUI gives product designers a unique opportunity to individualize the user’s entire interaction. The system should be able to recognize new and returning users, create user profiles and store the information the system collects in it. The more the system learns about users, the more personalized experience it should offer. Product designers need to decide what kinds of information to collect from users to personalize the experience.

### 4. Tone Of Voice

Voice is more than just a medium of interaction. In a few seconds, we listen to the other person’s voice; we create an impression on that person &mdash; a sense of gender, age, education, intelligence, trustworthiness, and many other characteristics. We do it intuitively, just by listening to a voice. That’s why it’s vital to give your VUI a personality &mdash; create the right brand persona that matches brand values. A good persona is specific enough to evoke a unique voice and personality.

{{< youtube id="tUbB_FbIqPw" breakout="true" caption="Create a brand persona talk by Wally Brill. (Video credits: Google)" >}}

### 5. Context Of Use

You need to understand where and how the voice-enabled product will be used. Will it be used by one person or shared between many people? In public or private areas? How noisy is the environment? The context of use will impact many product design decisions you will make. 

### 6. Sense Of Trust

Trust is a foundational principle of good user experience &mdash; user engagement is built on a foundation of trust. Good interaction with the voice user interface should always lead to the buildup of trust.

Here are a few things product designers can do to achieve this goal:

- **Never share private data with anyone.**  
Be careful to verbalize sensitive data such as medical data because users might not be alone. 
- **Avoid offensive content.**  
Introduce offensive or sensitive changes by age and region/country.
- **Try to avoid purely promotional content.**  
Don’t mention products or brand names out of the context because users may perceive it as promotional content. 

{{% ad-panel-leaderboard %}}

## Design Recommendations

When it comes to designing VUI, it’s possible to define two major areas:

1. [Conversational Design](#designing-the-conversation)
2. [Visual Design](#visual-design)

### 1. Designing The Conversation

At first glance, the significant difference between GUI and VUI is the interaction medium. In GUI, we use a keyboard, mouse, or touch screen, while for VUI, we use voice. However, when we look closer, we will see that the fundamental difference between the two types of interfaces is an interaction model. With voice, users can simply ask for what they want instead of learning how to navigate through the app and learn its features. **When we design for voice, we design conversational interactions.**

#### Learn About Your Users

Conversations with a computer should not feel awkward. Users should be able to interact with a voice user interface as they would with another person. That’s why the process of conversation design should always start with learning about the users. You need to find answers to the following questions:

- Who are your users?  
(Demographics, psychological portrait)
- How are they familiar with voice-based interactions? Are they currently using voice products?  
(Level of tech expertise) 

#### Understand Problem Space And Define Key Use Cases

When you know who your users are, you need to develop a deep understanding of user problems. What are their goals? Build empathy maps to identify users’ key pain points. As soon as you understand the problem space, it will be easier for you to anticipate features that users want and define specific use cases. (What can a user do with the voice system?)

Think about both the problem your user is trying to solve and how the voice user interface can help the user solve this problem. Here are a few questions that can help you with that:

- What are the key user’s tasks? (Learn about user needs/wants.)
- What situations trigger these tasks? (In what context users will interact with the system.)
- How are users completing these tasks today? (What is the user journey?)

It’s also vital to ensure that a voice user interface is the right solution for the user problem. For example, voice UI might work well for the task of finding a nearby restaurant while you’re on the road, but it might feel clunky for tasks like browsing restaurant reviews. 

#### Write Dialog Flow

At its core, conversation design is about the flow of the conversation. Dialog flow shouldn’t be an afterthought; instead, it should be the first thing you create because it will impact development.

Here are a few tips for creating a foundation for your dialog flow:

- **Start with a sample dialog that represents the happy path.**  
The happy path is the simplest, easiest path to success a user could follow. Don’t try to make sample dialog perfect at this step.
- **Focus on the spoken conversation.**  
Try to avoid situations when you write dialog differently than people speak it. It usually leads to well-structured but longer and more formal dialogs. When people want to solve a particular task, they are more to the point when they speak. 
- **Read a sample dialog aloud to ensure that it sounds natural.**  
Ideally, you should invite people who don’t belong to the design team and collect feedback. 

The sample dialog will help you identify the context of the conversation (when, where, and how the user triggers the voice interface) and the common utterances and responses.

After you finish writing sample dialogs, the next thing to do is add various paths (consider how the system will respond in numerous situations, adding turns in conversations, etc.). It doesn’t mean that you need to account for all possible variations in dialogs. Consider the Pareto principle (80% of users will follow the most common 20% of possible paths in a discussion) and define the most likely logical paths a user can take.

{{< youtube id="wuDP_eygsvs" breakout="true" caption="Conversation design principles. (Video credits: <a href='https://www.youtube.com/watch?v=wuDP_eygsvs'>Google</a>)" >}}

It’s also recommended to recruit a conversation designer &mdash; a professional who can help you craft natural and intuitive conversations for users.

#### Design For Human Language

The more an interface leverages human conversation, the fewer users have to be taught how to use it. Invest in user research and learn the vocabulary of your real or potential users. Try to use the same phrases and sentences in the system’s response. It will create a more user-friendly conversation. 

- **Don’t teach commands.**  
Let users speak in their own words.
- **Avoid technical jargon.**  
Let users interact with the system naturally using the phrases they prefer.

#### The UserAlways Starts The Conversation

No matter how sophisticated the voice-based system is, it should never start the conversation. It will be awkward if the system reaches the user with a topic they don’t want to discuss. 

#### Avoid Long Responses

When you design system responses, always take a cognitive load into account. VUI users aren’t reading, they are listening, and the longer you make system responses, the more information they have to retain in their working memory. Some of this information might not be usable for the user, but there is no way to fast-forward responses to skip forward. 

Make every word count and design for brief conversations. When you’re scripting out system responses, read them aloud. The length is probably good if you can say the words at a conversational pace with one breath. If you need to take an extra breath, rewrite the responses and reduce the length. 

#### Minimize The Number Of Options In System Prompts

It’s also possible to minimize the cognitive load by reducing the number of options users hear. Ideally, when users ask for a recommendation, the system should offer the best possible option right away. If it’s impossible to do that, try to provide the three best possible options and verbalize the most relevant one first. 

#### Provide Definitive Choices

Avoid open-ended questions in system responses. They can cause users to answer in ways that the system does not expect or support. For example, when you design an introduction prompt, instead of saying “Hello, its company ACME, what do you want to do?” you should say, “Hello, its company ACME, you can do [Option A], [Option B] or [Option C].”

#### Add Pauses Between The Question And Options

Pauses and punctuation mimic actual speech cadence, and they are beneficial for situations when the system asks a question and offers a few options to choose from.

Add a 500-millisecond pause after asking the question. This pause will give users enough time to comprehend the question.

#### Give Users Time To Think

When the system asks the user something, they might need to think about answering the question. The default timeout for users to respond to the request is 8-10 seconds. After that timeout, the system should repeat the request or re-prompt it. For example, suppose a user is booking a table at a restaurant. The sample dialog might sound like that:

<blockquote><strong>User</strong>: “Assistant, I want to go to the restaurant.”<br /><br /><strong>System</strong>: “Where would you like to go?”<br /><br />(No response for 8 seconds)<br /><br /><strong>System</strong>: “I can book you a table in a restaurant. What restaurant would you like to visit?”</blockquote>

#### Prompt For More Information When Necessary

It’s pretty common for users to request something but not provide enough details. For example, when users ask the voice assistant to book a trip, they might say something like, “Assistant, book a trip to sea.” The user assumes that the system knows them and will offer the best possible option. When the system doesn’t have enough information about the use it should prompt for more information rather than offer an option that might not be relevant. 

<blockquote><strong>User</strong>: “I’d like to book a trip to the seashore.”<br /><br /><strong>System</strong>: “When would you like to go?”</blockquote>

#### Never Ask Rhetorical Or Open-ended Questions

By asking rhetorical or open-ended questions, you put a high cognitive load on users. Instead, ask direct questions. For example, instead of asking the user “What do you want to do with your invitation?” you should say “You can cancel your invitation or reschedule it. What works for you?”

#### Don’t Make People Wait In Silence

When people don’t hear/see any feedback from the system they might think that it’s not working. Sometimes the system needs more time to proceed with the user request, but it doesn’t mean that users should wait in absolute silence/without any visual feedback. At least, you should offer some audition signal and pair it with visual feedback.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca5fc2bf-0214-4824-87b5-7549f6eac313/7-creating-voice-user-interfaces.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca5fc2bf-0214-4824-87b5-7549f6eac313/7-creating-voice-user-interfaces.gif" width="498" height="279" alt="mazon Echo visual feedback" /></a><figcaption>Amazon Echo visual feedback. (Image credit: <a href='https://tenor.com/view/amazon-echo-gif-10675034'>Tenor</a>)</figcaption></figure>

#### Minimize User Data Entry 

Try to reduce the number of cases when users have to provide phone numbers, street addresses, or alphanumeric passwords. It can be difficult for users to tell voice system strings of numbers or detailed information. This is especially true for users with speech impediments. Offer alternative methods for inputting this kind of information, such as using the companion mobile app.

#### Support Repeat 

Whether users are using the system in a noisy area or they’re just having issues understanding the question, they should be able to ask the system to repeat the last prompt at any time.

#### Feature Discoverability

Feature discoverability can be a massive problem in voice-based interfaces. In GUI, you have a screen that you can use to showcase new features, while in voice user interfaces, you don’t have this option. 

Here are two techniques you can use to improve discoverability:

- Solid onboarding. A first-time user requires onboarding into the system to understand its capabilities. Make it practical &mdash; let users complete some actions using voice commands. 
- The first encounter with a particular voice app, you might want to discuss what is possible.

#### Confirm User Requests

People enjoy a sense of acknowledgment. Thus, let the user know that the system hears and understands them. It’s possible to define two types of confirmation &mdash; implicit and explicit confirmation.

Explicit confirmations are required for high-risk tasks such as money transfers. These confirmations require the user’s verbal approval to continue.

<blockquote><strong>User</strong>: “Transfer one thousand dollars to Alice.”<br /><br /><strong>System</strong>: “You want to transfer one thousand dollars to Alice Young, correct?”</blockquote>

At the same time, not every action requires the user’s confirmation. For example, when a user asks to stop playing music, the system should end the playback without asking, “Do you want to stop the music?”

#### Handle Error Gracefully

It’s nearly impossible to avoid errors in voice interactions. Loosely handled error states might affect a user’s impression of the system. No matter what caused the error, it’s important to handle it with grace, meaning that the user should have a positive experience from using a system even when they face an error condition. 

- **Minimize the number of “I don’t understand you” situations.**   
Avoid error messages that only state that they didn’t understand the user correctly. Well-designed dialog flow should consider all possible dialog branches, including branches with incorrect user input.   
- **Introduce a mechanism of contextual repairs.**  
Help the system situation when something unexpected happens while the user is speaking. For example, the voice recognition system failed to hear the user due to the loud noise in the background.
- **Clearly say what the system cannot do.**  
When users face error messages like “I cannot understand you” they start to think whether the system isn’t capable of doing something or they incorrectly verbalize the request. It’s recommended to provide an explicit response in situations when the system cannot do something. For example, “Sorry, I cannot do that. But I can help you with [option].”
- **Accept corrections.**  
Sometimes users make corrections when they know that system got something wrong or when they decided to change their minds. When users want to correct their input, they will say something like “No,” or “I said,” followed by a valid utterance.

#### Test Your Dialogs

The sooner you start testing your conversation flow, the better. Ideally, start testing and iterating on your designs as soon as you have sample dialogs. Collecting feedback during the design process exposes usability issues and allows you to fix the design early. 

The best way to test if your dialog works is to act it out. You can use techniques like *Wizard of Oz*, where one person pretends to be a system and the other is a user. As soon as you start practicing the script, you will notice whether it sounds good or bad when spoken aloud.

Remember, that you should prevent people from sharing non-verbal cues. When we interact with other people, we typically use non-verbal language (eye gaze, body language). Non-verbal cues are extremely valuable for conveying information, but unfortunately, VUIs systems cannot understand them. When testing your dialogs, try to sit test participants back to back to avoid eye contact.

The next part of testing is observing real user behavior. Ideally, you should observe users who use your product for the first time. It will help you understand what works and what doesn’t. Testing with 5 participants will help you reveal most of your usability issues.

{{% ad-panel-leaderboard %}}

### 2. Visual Design

A screen plays a secondary role in voice interactions. Yet, it’s vital to consider a visual aspect of user interaction because high-quality visual experiences create better impressions on users. Plus, visuals are good for some particular tasks such as scanning and comparing search results. The ultimate goal is to design a more delightful and engaging multimodal experience.

#### Design For Smaller Screens First

When adapting content across screens, start with the smallest screen size first. It will help you prioritize what the most important content is.

When targeting devices with larger screens, don’t just scale the content up. Try to take full advantage of the additional screen real estate. Put attention on the quality of images and videos &mdash; imagery shouldn’t lose its quality as they scale up.

#### Optimize Content For Fast Scanning

As was mentioned before, screens are very handy for cases when you need to provide a few options to compare. Among all content containers, you can use, cards are the one that works the best for fast scanning. When you need to provide a list of options to choose from, you can put each option on the card. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee70ebd-f29f-4147-9c5f-6ae1c827a948/4-creating-voice-user-interfaces.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee70ebd-f29f-4147-9c5f-6ae1c827a948/4-creating-voice-user-interfaces.jpg" width="800" height="623" sizes="100vw" caption="Nest Hub uses cards as content containers. (Image credit: <a href='https://store.google.com/us/product/google_nest_hub_max?hl=en-US'>Google</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee70ebd-f29f-4147-9c5f-6ae1c827a948/4-creating-voice-user-interfaces.jpg'>Large preview</a>)" alt="Nest Hub uses cards" >}}

#### Design With A Specific Viewing Distance In Mind

Design content so it can be viewed from a distance. The viewing range of small screen voice-enabled devices should be between 1-2 meters, while for large screens such as TVs, it should be 3 meters. You need to ensure that font size and the size of imagery and UI elements that you will show on the screen are comfortable for users.

Google [recommends](https://developers.google.com/assistant/interactivecanvas/design) using a minimum font size of 32 pt for primary text, like titles, and a minimum of 24pt for secondary text, like descriptions or paragraphs of text.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6301594e-f8f9-4133-879e-d032d83ae1ad/10-creating-voice-user-interfaces.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6301594e-f8f9-4133-879e-d032d83ae1ad/10-creating-voice-user-interfaces.png" width="800" height="577" sizes="100vw" caption="A typical context of use for Echo Show, Amazon voice-first device. (Image credit: <a href='https://www.amazon.com/echo-show-10/dp/B07VHZ41L8'>Amazon</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6301594e-f8f9-4133-879e-d032d83ae1ad/10-creating-voice-user-interfaces.png'>Large preview</a>)" alt="In the picture, Echo Show stands on a kitchen table next to a chopping board with some food on it." >}}

#### Learn User Expectations About Particular Device

Voice-enabled devices can range from in-vehicle to TV devices. Each device mode has its own context of use and set of user expectations. For example, home hubs are typically used for music, communications, and entertainment, while in-car systems are typically used for navigation purposes. 

**Further Reading**: [*Designing Human-Machine Interfaces For Vehicles Of The Future*](https://www.smashingmagazine.com/2021/12/designing-human-machine-interfaces-future-vehicles/)

#### Hierarchy Of Information On Screens

When we design website pages, we typically start with page structure. A similar approach should be followed when designing for VUI &mdash; decide where each element should be located. The hierarchy of information should go from most to least important. Try to minimize the information you display on the screen &mdash; only required information that helps users do what they want to do.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/338b1af5-6e08-41c3-adf8-a9cf24f0768f/11-creating-voice-user-interfaces.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/338b1af5-6e08-41c3-adf8-a9cf24f0768f/11-creating-voice-user-interfaces.jpg" width="800" height="" sizes="100vw" caption="Clear visual hierarchy of information on the Portal, voice-first device by Sber. (Image credit: <a href='https://sberdevices.ru/sberportal/'>Sber</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/338b1af5-6e08-41c3-adf8-a9cf24f0768f/11-creating-voice-user-interfaces.jpg'>Large preview</a>)" alt="Clear visual hierarchy of information on the Portal, voice-first device by Sber." >}}

### Keep The Visual And Voice In Sync

There shouldn’t be a significant delay between voice and visual elements. The graphical interface should be truly responsive &mdash; right after the user hears the voice prompt; the interface should be refreshed with relevant information. 

Motion language plays a significant part in how users comprehend information. It’s essential to avoid hard cuts and use smooth transitions between individual states. When users are speaking, we should also provide visual feedback that acknowledges that the system is listening to the user.

{{< vimeo id="671868902" caption="Clear hierarchy of information of voice file manager. (Video credit: <a href='https://dribbble.com/glebich'>Gleb Kuznetsov</a>)" breakout="true" >}}

### Accessible Design

A well-designed product is inclusive and universally accessible. Visual impairment users (people with disabilities such as blindness, low vision, and color blindness) shouldn’t have any problems interacting with your product. To make your design accessible, follow [WCAG guidelines](https://www.w3.org/TR/WCAG21/).

- Ensure that text on the screen is legible. Ensure your text has a high enough contrast ratio. The text color and contrast meet AAA ratios.
- Users who rely on screen readers should understand what is displayed on the screens. Add descriptions to imagery.
- Don’t design screen elements that flicker, flash, or blink. Generally, everything that flashes more than three flashes per second can cause users with motion sickness headaches. 

**Related Reading**: [*How A Screen Reader User Accesses The Web*](https://www.smashingmagazine.com/2019/02/accessibility-webinar/)

## Conclusion

We are at the dawn of the next digital revolution. The next generation of computers will give users a unique opportunity to interact with voice. But the foundation for this generation is created today. It’s up to designers to develop systems that will be natural for users. 

### Recommended Related Reading

- “[Alexa Design Guide](https://developer.amazon.com/en-US/docs/alexa/alexa-design/get-started.html),” Amazon Developer Documentation 
- “[Conversation Design Process](https://developers.google.com/assistant/conversation-design/learn-about-conversation),” Google Assistant Docs
- “[Designing Voice User Interfaces: Principles Of Conversational Experiences](https://www.amazon.com/Designing-Voice-User-Interfaces-Conversational/dp/1491955414),” Cathy Pearl (2017)
- “[Applying Built-In Hacks Of Conversation To Your Voice UI ](https://www.youtube.com/watch?v=wuDP_eygsvs),” James Giangola (video)
- “[Creating A Persona: What Does Your Product Sound Like? ](https://www.youtube.com/watch?v=tUbB_FbIqPw),” Wally Brill (video)
- “[Voice Principles](https://voiceprinciples.com),” *a collection of resources created by Clearleft.*

{{< signature "vf, yk, il" >}}
