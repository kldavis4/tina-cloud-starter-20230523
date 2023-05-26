---
title: 'Mixing Tangible And Intangible: Designing Multimodal Interfaces Using Adobe XD'
slug: mixing-tangible-intangible-multimodal-interfaces-adobe-xd
author: nickbabich
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da77c5a8-d1bf-4fa6-93b0-3d7443861df1/2-designing-multimodal-interfaces-using-adobe-xd-800w.png
date: 2018-12-18T15:00:04+01:00
summary: >-
  We’re at the dawn of a UI revolution. Not only will multimodal interfaces give users more power, but they will also change the way users interact with systems. In this article, you can learn how to build your own multimodal UI using Adobe XD.
description: >-
  We’re at the dawn of a UI revolution. Not only will multimodal interfaces give users more power, but they will also change the way users interact with systems. In this article, you can learn how to build your own multimodal UI using Adobe XD.
categories:
  - UX
  - UI
  - Design
disable_ads: true
disable_panels: true
---
<p>(This article is kindly sponsored by Adobe.) User interfaces are evolving. Voice-enabled interfaces are challenging the long dominance of graphical user interfaces and are quickly becoming a common part of our daily lives. Significant progress in automatic speech recognition (APS) and natural language processing (NLP), together with an impressive consumer base (millions of mobile devices with built-in voice assistants), have influenced the rapid development and adoption of voice-based interface.</p>

<p>Products that use voice as the primary interface are becoming more and more popular. In the US alone, 47.3 million adults have access to a smart speaker (that’s <a href="https://techcrunch.com/2018/03/07/47-3-million-u-s-adults-have-access-to-a-smart-speaker-report-says/">one fifth of the US adult population</a>), and the number is growing. But voice interfaces have a bright future not only in personal and home use. As people become accustomed to voice interfaces, they will come to expect them in a <a href="https://techcrunch.com/2017/11/29/amazon-is-putting-alexa-in-the-office/">business context as well</a>. Just imagine that soon you’ll be able to trigger a conference-room projector by saying something like, “Show my presentation”.</p>

<p>It’s evident that human-machine communication is rapidly expanding to encompass both written and spoken interaction. But does it mean that future interfaces will be voice-only? Despite some science-fiction portrayals, voice won’t completely replace graphical user interfaces. Instead, we’ll have a synergy of voice, visual and gesture in a new format of interface: a voice-enabled, multimodal interface.</p>

<p>In this article, we’ll:</p>

<ul>
<li>explore the concept of a voice-enabled interface and review different types of voice-enabled interfaces;</li>
<li>find out why voice-enabled, multimodal user interfaces will be the preferred user experience;</li>
<li>see how you can build a multimodal UI using Adobe XD.</li>
</ul>

## The State Of Voice User Interfaces (VUI)

<p>Before diving into the details of voice user interfaces, we must define what voice input is. Voice input is a human-computer interaction in which a user speaks commands instead of writing them. The beauty of voice input is that it’s a more natural interaction for people &mdash; users are not restricted to a specific syntax when interacting with a system; they can structure their input in many different ways, just as they would do in human conversation.</p>

<p>Voice user interfaces bring the following benefits to their users:</p>

<ul>
<li><strong>Less interaction cost</strong><br />Although using a voice-enabled interface does involve an interaction cost, this cost is smaller (in theory) than that of learning a new GUI.</li>
<li><strong>Hands-free control</strong><br />VUIs are great for when the users hands are busy &mdash; for example, while driving, cooking or exercising.</li>
<li><strong>Speed</strong><br />Voice is excellent when asking a question is faster than typing it and reading through the results. For example, when using voice in a car, it is faster to say the place to a navigation system, rather than type the location on a touchscreen.</li>
<li><strong>Emotion and personality</strong><br />Even when we hear a voice but don’t see an image of a speaker, we can picture the speaker in our head. This has an opportunity to improve user engagement.</li>
<li><strong>Accessibility</strong><br />Visually impaired users and users with a mobility impairment can use voice to interact with a system.</li>
</ul>

### Three Types Of Voice-Enabled Interfaces

<p>Depending on how voice is used, it could be one of the following types of interfaces.</p>

#### Voice Agents In Screen-First Devices

<p>Apple Siri and Google Assistant are prime examples of voice agents. For such systems, the voice acts more like an enhancement for the existing GUI. In many cases, the agent acts as the first step in the user’s journey: The user triggers the voice agent and provides a command via voice, while all other interactions are done using the touchscreen. For example, when you ask Siri a question, it will provide answers in the format of a list, and you need to interact with that list. As a result, the user experience becomes fragmented &mdash; we use voice to initiate the interaction and then shift to touch to continue it.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1001ed2-af4d-4fef-b066-859ab2a8f708/1-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1001ed2-af4d-4fef-b066-859ab2a8f708/1-designing-multimodal-interfaces-using-adobe-xd.png" sizes="70vw" caption="Siri executes a voice command to search for news, but then requires users to touch the screen in order to read the items. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1001ed2-af4d-4fef-b066-859ab2a8f708/1-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="Siri executes a voice command to search for news, but then requires users to touch the screen in order to read the items." >}}

#### Voice-Only Devices

<p>These devices don’t have visual displays; users rely on audio for both input and output. Amazon Echo and Google Home smart speakers are prime examples of products in this category. The lack of a visual display is a significant constraint on the device’s ability to communicate information and options to the user. As a result, most people use these devices to complete simple tasks, such as playing music and getting answers to simple questions.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd97ffd-be51-4570-89c1-d89209d2045c/11-designing-multimodal-interfaces-using-adobe-xd.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee446347-1514-48f5-befd-0628e9b1d510/11a-designing-multimodal-interfaces-using-adobe-xd.jpg" sizes="70vw" caption="Amazon Echo Dot is a screen-less device. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd97ffd-be51-4570-89c1-d89209d2045c/11-designing-multimodal-interfaces-using-adobe-xd.jpg'>Large preview</a>)" alt="Amazon Echo Dot is a screen-less device." >}}

#### Voice-First Devices

<p>With voice-first systems, the device accepts user input primarily via voice commands, but also has an integrated screen display. It means that voice is the primary user interface, but not the only one. The old saying, “A picture is worth a thousand words” still applies to modern voice-enabled systems. The human ​brain​ has incredible​ ​image​-​processing​ abilities &mdash; we​ ​can​ ​understand​ ​complex​ ​information​ ​faster​ ​when we​ ​see​ ​it​ ​visually. Compared to voice-only devices, voice-first devices allow users to access a larger amount of information and make many tasks much easier.</p>

<p>The Amazon Echo Show is a prime example of a device that employs a voice-first system. Visual information is gradually incorporated as part of a holistic system &mdash; the screen is not loaded with app icons; rather, the system encourages users to try different voice commands (suggesting verbal commands such as, “Try ‘Alexa, show me the weather at 5:00 pm’”). The screen even makes common tasks such as checking a recipe while cooking much easier &mdash; users don’t need to listen carefully and keep all of the information in their heads; when they need the information, they simply look at the screen.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e3742fd-2682-4278-aa95-089b706de8ac/9-designing-multimodal-interfaces-using-adobe-xd.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57478c2f-c3d0-41e2-afca-f1e32f6bfa22/9a-designing-multimodal-interfaces-using-adobe-xd.jpg" sizes="70vw" caption="Amazon Echo Show is basically an Amazon Echo speaker with a screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e3742fd-2682-4278-aa95-089b706de8ac/9-designing-multimodal-interfaces-using-adobe-xd.jpg'>Large preview</a>)" alt="Amazon Echo Show is basically an Amazon Echo speaker with a screen." >}}

## Introducing Multimodal Interfaces

<p>When it comes to using voice in UI design, don’t think of voice as something you can use alone. Devices such as Amazon Echo Show include a screen but employ voice as the primary input method, making for a more holistic user experience. This is the first step towards a new generation of user interfaces: multimodal interfaces.</p>

<p>A multimodal interface is an interface that blends voice, touch, audio and different types of visuals in a single, seamless UI. Amazon Echo Show is an excellent example of a device that takes full advantage of a voice-enabled multimodal interface. When users interact with Show, they make requests just as they would with a voice-only device; however, the response they receive will likely be multimodal, containing both voice and visual responses.</p>

<p>Multimodal products are more complex than products that rely only on visuals or only on voice. Why should anyone create a multimodal interface in the first place? To answer that question, we need to step back and see how people perceive the environment around them. People have five senses, and the combination of our senses working together is how we perceive things. For example, our senses work together when we are listening to music at a live concert. Remove one sense (for example, hearing), and the experience takes on an entirely different context.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aba62fd-5916-4a73-957f-cfedfb8d300f/13-designing-multimodal-interfaces-using-adobe-xd.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aba62fd-5916-4a73-957f-cfedfb8d300f/13-designing-multimodal-interfaces-using-adobe-xd.jpg" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aba62fd-5916-4a73-957f-cfedfb8d300f/13-designing-multimodal-interfaces-using-adobe-xd.jpg'>Large preview</a>)" alt="Our senses work together when we are listening to music at a live concert. Remove one sense (for example, hearing), and the experience takes on an entirely different context." >}}

<p>For too long, we’ve thought about the user experience as exclusively either visual or gestural  design. It’s time to change this thinking. Multimodal design is a way to think about and design for experiences that connect our sensory abilities together.</p>

<p>Multimodal interfaces feel like ​a more​ ​human​ ​way​ for ​user​ ​and​ machine to communicate. They open up new opportunities for deeper interactions. And today, it’s much easier to design multimodal interfaces because the technical limitations that in the past constrained interactions with products are being erased.</p>

### The Difference Between A GUI And Multimodal Interface

<p>The key difference here is that multimodal interfaces like Amazon Echo Show sync voice and visual interfaces. As a result, when we’re designing the experience, the voice and visuals are no longer independent parts; they are integral parts of the experience that the system provides.</p>

### Visual And Voice Channel: When To Use Each

<p>It’s important to think about voice and visuals as channels for input and output. Each channel has its own strengths and weaknesses.</p>

<p>Let’s start with the visuals. It’s clear that some information is just easier to understand when we see it, rather than when we hear it. Visuals work better when you need to provide:</p>

<ul>
<li>a long lists of options (reading a long list will take a lot of time and be difficult to follow);</li>
<li>data-heavy information (such as diagrams and graphs);</li>
<li>product information (for example, products in online shops; most likely, you would want to see a product before buying) and product comparison (as with the long list of options, it would be hard to provide all of the information using only voice).</li>
</ul>

<p>For some information, however, we can easily rely on verbal communication. Voice might be the right fit for the following cases:</p>

<ul>
<li>user commands (voice is an efficient input modality, allowing users to give commands to the system quickly and bypassing complex navigation menus);</li>
<li>simple user instructions (for example, a routine check on a prescription);</li>
<li>warnings and notifications (for example, an audio warning paired with voice notifications during driving).</li>
</ul>

<p>While these are a few typical cases of visual and voice combined, it’s important to know that we can’t separate the two from each other. We can create a better user experience only when both voice and visuals work together. For example, suppose we want to purchase a new pair of shoes. We could use voice to request from the system, “Show me New Balance shoes.” The system would  process your request and visually provide product information (an easier way for us to compare shoes).</p>

## What You Need To Know To Design Voice-Enabled, Multimodal Interfaces

<p>Voice is one of the most exciting challenges for UX designers. Despite its novelty, the fundamental rules for designing voice-enabled, multimodal interface are the same as those we use to create visual designs. Designers should care about their users. They should aim to reduce friction for the user by solving their problems in efficient ways and prioritize clarity to make the user’s choices clear.</p>

<p>But there are some unique design principles for multimodal interfaces as well.</p>

### Make Sure You Solve The Right Problem

<p>Design should solve problems. But it’s vital to solve the right problems; otherwise, you could spend a lot of time creating an experience that doesn’t bring much value to users. Thus, make sure you’re focused on solving the right problem. Voice interactions should make sense to the user; users should have a compelling reason to use voice over other methods of interaction (such as clicking or tapping). That’s why, when you create a new product &mdash; even before starting the design &mdash; it’s essential to conduct user research and determine whether voice would improve the UX.</p>

<p>Start with creating a user journey map. Analyze the journey map and find places where including voice as a channel would benefit the UX.</p>

<ul>
<li>Find places in the journey where users might encounter friction and frustration. Would using voice reduce the friction?</li>
<li>Think about the context of the user. Would voice work for a particular context?</li>
<li>Think about what is uniquely enabled by voice. Remember the unique benefits of using voice, such as hands-free and eyes-free interaction. Could voice add value to the experience?</li>
</ul>

### Create Conversational Flows

<p>Ideally, the interfaces you design should require zero interaction cost: Users should be able to fulfill their needs without spending extra time on learning how to interact with the system. This happens only when voice interaction resemble a real conversation, not a system dialog wrapped in the format of voice commands. The fundamental rule of a good UI is simple: Computers should adapt to humans, not the other way around.</p>

<p>People rarely have flat, linear conversations (conversations that only last one turn). That’s why, to make interaction with a system feel like a live conversation, designers should focus on creating conversational flows. Each conversational flow consists of dialogs &mdash; the pathways that occur between the system and the user. Each dialog would include the system’s prompts and the user’s possible responses.</p>

<p>A conversational flow can be presented in the form of a flow diagram. Each flow should focus on one particular use case (for example, setting an alarm clock using a system). For most dialogs in a flow, it’s vital to consider error paths, when things go off the rails.</p>

<p>Each voice command of the user consists of three key elements: intent, utterance and slot.</p>

<ul>
<li><strong>Intent is the objective of the user’s interaction with a voice-enabled system.</strong><br />An intent is just a fancy way of defining the purpose behind a set of words. Each interaction with a system brings the user some utility. Whether it’s information or an action, the utility is in intent. Understanding the user’s intent is a crucial part of voice-enabled interfaces. When we design VUI, we don’t always know for sure what a user’s intent is, but we can guess it with high accuracy.</li>
<li><strong>Utterance is how the user phrases their request.</strong><br />Usually, users have more than one way to formulate a voice command. For example, we can set an alarm clock by saying “Set alarm clock to 8 am”, or “Alarm clock 8 am tomorrow” or even “I need to wake up at 8 am.” Designers need to consider every possible variation of utterance.</li>
<li>Slots are variables that users use in a command. Sometimes users need to provide additional information in the request. In our example of the alarm clock, “8 am” is a slot.</li>
</ul>

### Don’t Put Words In The User’s Mouth

<p>People know how to talk. Don't try to teach them commands. Avoid phrases like, “To send a meeting appointment, you need to say ‘Calendar, meetings, create a new meeting’.” If you have to explain commands, you need to reconsider the way you’re designing the system. Always aim for natural language conversation, and try to accommodate diverse speaking styles).</p>

### Strive For Consistency

<p>You need to achieve consistency in language and voice across contexts. Consistency will help to build familiarity in interactions.</p>

### Always Provide Feedback

<p>Visibility of system status is one of the <a href="https://www.nngroup.com/articles/ten-usability-heuristics/">fundamental principles of good GUI design</a>. The system should always keep users informed of what is going on through appropriate feedback within a reasonable time. The same rule applies to VUI design.</p>

<ul>
<li><strong>Make the user aware that the system is listening.</strong><br />Show visual indicators when the device is listening or processing the user’s request. Without feedback, the user can only guess whether the system is doing something. That’s why even voice-only devices such as Amazon Echo and Google Home give us nice visual feedback (flashing lights) when they are listening or searching for an answer.</li>
<li><strong>Provide conversational markers.</strong><br /><a href="https://developer.amazon.com/fr/designing-for-voice/what-alexa-says/#use-conversation-markers">Conversational markers</a> tell the user where they’re at in the conversation.</li>
<li><strong>Confirm when a task is completed.</strong><br />For example, when users ask the voice-enabled smart home system “Turn off the lights in the garage”, the system should let the user know that the command has been successfully executed. Without confirmation, users will need to walk into the garage and check the lights. It defeats the purpose of the smart home system, which is to make the user’s life easier.</li>
</ul>

### Avoid Long Sentences

<p>When designing a voice-enabled system, consider the way you provide information to users. It’s relatively easy to <a href="https://www.ncbi.nlm.nih.gov/pubmed/12821413">overwhelm users with too much information</a> when you use long sentences. First, users can’t retain a lot of information in their short-term memory, so they can easily forget some important information. Also, audio is a slow medium &mdash; most people can read much faster than they can listen.</p>

<p>Be respectful of your user’s time; don’t read out long audio monologues. When you’re designing a response, the fewer words you use, the better. But remember that you still need to provide enough information for the user to complete their task. Thus, if you cannot summarize an answer in a few words, display it on the screen instead.</p>

### Provide Next Steps Sequentially

<p>Users can be overwhelmed not only by long sentences, but also their number of options at one time. It’s vital to break down the process of interaction with a voice-enabled system into bite-sized chunks. Limit the number of choices the user has at any one time, and make sure they know what to do at every moment.</p>

<p>When designing a complex voice-enabled system with a lot of features, you can use the technique of progressive disclosure: Present only the options or information necessary to complete the task.</p>

### Have A Strong Error-Handling Strategy

<p>Of course, the system should prevent errors from occurring in the first place. But no matter how good your voice-enabled system is, you should always design for the scenario in which the system doesn’t understand the user. Your responsibility is to design for such cases.</p>

<p>Here are a few practical tips for creating a strategy:</p>

<ul>
<li><strong>Don’t blame the user.</strong><br />In conversation, there are no errors. Try to avoid reponses like, “Your answer is incorrect.”</li>
<li><strong>Provide error-recovery flows.</strong><br />Provide an option for back-and-forths in a conversation, or even to exit the system, without losing important information. Save the user’s state in the journey, so that they can re-engage with the system right from where they left off.</li>
<li><strong>Let users replay information.</strong><br />Provide an option to make the system repeat the question or answer. This might be helpful for complex questions or answers where it would be hard for the user to commit all of the information to their working memory.</li>
<li><strong>Provide stop wording.</strong><br />In some cases, the user will not be interested in listening to an option and will want the system to stop talking about it. Stop wording should help them do just that.</li>
<li><strong>Handle unexpected utterances gracefully.</strong><br />No matter how much you invest in the design of a system, there will be situations when the system doesn’t understand the user. It’s vital to handle such cases gracefully. Don’t be afraid to let the system admit a lack of understanding. The system should communicate what it has understood and provide helpful reprompts.</li>
<li><strong>Use analytics to improve your error strategy.</strong><br />Analytics can help you identify wrong turns and misinterpretations.</li>
</ul>

### Keep Track Of Context

<p>Make sure the system understands the context of the user’s input. For example, when someone says that they want to book a flight to San Francisco next week, they might refer to “it” or “the city” during the conversational flow. The system should remember what was said and be able to match it to the newly received information.</p>

### Learn About Your Users To Create More Powerful Interactions

<p>A voice-enabled system becomes more sophisticated when it uses additional information (such as user context or past behavior) to understand what the user wants. This technique is called intelligent interpretation, and it requires that the system actively learn about the user and be able to adjust their behavior accordingly. This knowledge will help the system to provide answers even to complex questions, such as "What gift should I buy for my wife’s birthday?"</p>

### Give Your VUI A Personality

<p>Every voice-enabled system has an emotional impact on the user, whether you plan for it or not. People associate voice with humans rather than machines. According to <a href="https://www.jwtintelligence.com/trend-reports/speak-easy-global-edition/">Speak Easy Global Edition research</a>, 74% of regular users of voice technology expect brands to have unique voices and personalities for their voice-enabled products. It’s possible to build empathy through personality and achieve a higher level of user engagement.</p>

<p>Try to reflect your unique brand and identity in the voice and tone you present. Construct a persona of your voice-enabled agent, and rely on this persona when creating dialogs.</p>

### Build Trust

<p>When users don’t trust a system, they don’t have the motivation to use it. That’s why building trust is a requirement of product design. Two factors have a significant impact on the level of trust built: system capabilities and valid outcome.</p>

<p>Building trust starts with setting user expectations. Traditional GUIs have a lot of visual details to help the user understand what the system is capable of. With a voice-enabled system, designers have fewer tools to rely on. Still, it’s vital to make the system naturally discoverable; the user should understand what is and isn’t possible with the system. That’s why a voice-enabled system might require user onboarding, where it talks about what the system can do or what it knows. When designing onboarding, try to offer meaningful examples to let people know what it can do (examples work better than instructions).</p>

<p>When it comes to valid outcomes, people know that voice-enabled systems are imperfect. When a system provides an answer, some users might doubt that the answer is correct. this happens because users don’t have any information about whether their request was correctly understood or what algorithm was used to find the answer. To prevent trust issues, use the screen for supporting evidence &mdash; display the original query on the screen &mdash; and provide some key information about the algorithm. For example, when a user asks, “Show me the top five movies of 2018”, the system can say, “Here are top five movies of 2018 according to the box office in the US”.</p>

### Don’t Ignore Security And Data Privacy

<p>Unlike mobile devices, which belong to the individual, voice devices tend to belong to a location, like a kitchen. And usually, there are more than one person in the same location. Just imagine that someone else can interact with a system that has access to all of your personal data. Some VUI systems such as Amazon Alexa, Google Assistant and Apple Siri can recognize individual voices, which adds a layer of security to the system. Still, it <a href="https://www.youtube.com/watch?v=JQAc1UhUA2s">doesn’t guarantee</a> that the system will be able to recognize users based on their unique voice signature in 100% of cases.</p>

<p>Voice recognition is continually improving, and it will be hard or nearly impossible to imitate a voice in the near future. However, in the current reality, it’s vital to provide an additional authentication layer to reassure the user that their data is safe. If you design an app that works with sensitive data, such as health information or banking details, you might want to include an extra authentication step, such as a password or fingerprint or face recognition.</p>

### Conduct Usability Testing

<p>Usability testing is a mandatory requirement for any system. <a href="https://www.smashingmagazine.com/2017/11/improve-user-testing/">Test early, test often</a> should be a fundamental rule of your design process. Gather user research data early on, and iterate your designs. But testing multimodal interfaces has its own specifics. Here are two phases that should be taken into account:</p>

<ul>
<li><strong>Ideation phase</strong><br />Test drive your sample dialogs. Practice reading sample dialogs out loud. Once you have some conversational flows, record both sides of the conversation (the user’s utterances and the system’s responses), and listen to the recording to understand whether they sound natural.</li>
<li><strong>Early stages of product development (testing with lo-fi prototypes)</strong><br />Wizard of Oz testing is well-suited to testing conversational interfaces. Wizard of Oz testing is a type of testing in which a participant interacts with a system that they believe is operated by a computer but is in fact operated by a human. The test participant formulates a query, and a real person responds on the other end. This method gets its name from the book <em>The Wonderful Wizard of Oz</em> by Frank Baum. In the book, an ordinary man hides behind a curtain, pretending to be a powerful wizard. This test allows you to map out every possible scenario of interaction and, as a result, create more natural interactions. <a href="https://github.com/bensauer/saywizard/">Say Wizard</a> is a great tool to help you run a Wizard of Oz voice-interface test on macOS.</li>

{{< vimeo id="238944539" caption="Designing For Voice: The ‘Wizard Of Oz’ Method (Watch on <a href='https://vimeo.com/238944539'>Vimeo</a>)" >}}

<li><strong>Later stages of product development (testing with hi-fi prototypes)</strong><br />In usability testing of graphical user interfaces, we often ask users to speak out loud when they interact with a system. For a voice-enabled system, that’s not always possible because the system would be listening to that narration. So, it might be better to observe the user’s interactions with the system, rather than ask them to speak out loud.</li>
</ul>

## How To Create A Multimodal Interface Using Adobe XD

<p>Now that you have a solid understanding of what a multimodal interface is and what rules to remember when designing them, we can discuss how to make a prototype of a multimodal interface.</p>

<p>Prototyping is a fundamental part of the design process. Being able to bring an idea to life and share it with others is extremely important. Until now, designers who wanted to incorporate voice in prototyping had few tools to rely on, the most powerful of which was a flowchart. Picturing how a user would interact with a system required a lot of imagination from someone looking at the flowchart. With Adobe XD, designers now have access to the medium of voice and can use it in their prototypes. XD seamlessly connects screen and voice prototyping in one app.</p>

### New Experiences, Same Process

<p>Even though voice is a totally different medium than visual, the process of prototyping for voice in Adobe XD is pretty much the same as prototyping for a GUI. The Adobe XD team integrates voice in a way that will feel natural and intuitive for any designer. Designers can use voice triggers and speech playback to interact with prototypes:</p>

<ul>
<li>Voice triggers start an interaction when a user says a particular word or phrase (utterance).</li>
<li>Speech playback gives designers access to a text-to-speech engine. XD will speak words and sentences defined by a designer. Speech playback can be used for many different purposes. For example, it can act as an acknowledgment (to reassure users) or as guidance (so users know what to do next).</li>
</ul>

<p>The great thing about XD is that it doesn’t force you to learn the complexities of each voice platform.</p>

<p>Enough words &mdash; let’s see how it works in action. For all of the examples you’ll see below, I’ve used artboards created using <a href="https://adobe.ly/xdvoiceuikit">Adobe XD UI kit for Amazon Alexa</a> (this is a link to download the kit). The kit contains all of the styles and components needed to create experiences for Amazon Alexa.</p>

<p>Suppose we have the following artboards:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2736e0-ea20-4a9b-9af8-26f20b6b2ae5/5-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2736e0-ea20-4a9b-9af8-26f20b6b2ae5/5-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2736e0-ea20-4a9b-9af8-26f20b6b2ae5/5-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="example of an artboard" >}}

<p>Let’s go into prototyping mode to add in some voice interactions. We’ll start with voice triggers. Along with triggers such as tap and drag, we are now able to use voice as a trigger. We can use any layers for voice triggers as long as they have a handle leading to another artboard. Let’s connect the artboards together.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cf12a8f-a9fc-45dd-addc-b78dc0cbc797/7-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cf12a8f-a9fc-45dd-addc-b78dc0cbc797/7-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="Connecting artboards together. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cf12a8f-a9fc-45dd-addc-b78dc0cbc797/7-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="Connecting artboards together" >}}

<p>Once we do that, we’ll find a new “Voice” option under the “Trigger”. When we select this option, we’ll see a “Command” field that we can use to enter an utterance &mdash; this is what XD will actually be listening for. Users will need to speak this command to activate the trigger.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe06c8ad-e8d0-4eca-94cf-8b8e81843fa6/3-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe06c8ad-e8d0-4eca-94cf-8b8e81843fa6/3-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="Setting a voice trigger in Adobe XD. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe06c8ad-e8d0-4eca-94cf-8b8e81843fa6/3-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="Setting a voice trigger in Adobe XD." >}}

<p>That’s all! We’ve defined our first voice interaction. Now, users can say something, and a prototype will respond to it. But we can make this interaction much more powerful by adding speech playback. As I mentioned previously, speech playback allows a system to speak some words.</p>

<p>Select an entire second artboard, and click on the blue handle. Choose a “Time” trigger with a delay and set it to 0.2s. Under the action, you’ll find “Speech Playback”. We’ll write down what the virtual assistant speaks back to us.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fc7d629-fd2b-4bfa-8a50-2005b0a2c020/12-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fc7d629-fd2b-4bfa-8a50-2005b0a2c020/12-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fc7d629-fd2b-4bfa-8a50-2005b0a2c020/12-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="Using the Command option to enter an utterance or speak a command to activate the trigger" >}}

<p>We’re ready to test our prototype. Select the first artboard, and clicking the play button in the top right will launch a preview window. When interacting with voice prototyping, make sure your mic is on. Then, hold down the spacebar to speak the voice command. This input triggers the next action in the prototype.</p>

### Use Auto-Animate To Make The Experience More Dynamic

<p>Animation brings a lot of benefits to UI design. It serves clear functional purposes, such as:</p>

<ul>
<li>communicating the spatial relationships between objects (Where does the object come from? Are those objects related?);</li>
<li>communicating affordance (What can I do next?)</li>
</ul>

<p>But functional purposes aren’t the only benefits of animation; animation also makes the experience more alive and dynamic. That’s why UI animations should be a natural part of multimodal interfaces.</p>

<p>With “Auto-Animate” available in Adobe XD, it becomes much easier to create prototypes with immersive animated transitions. Adobe XD does all the hard work for you, so you don’t need to worry about it. All you need to do to create an animated transition between two artboards is simply duplicate an artboard, modify the object properties in the clone (properties such as size, position and rotation), and apply an Auto-Animate action. XD will automatically animate the differences in properties between each artboard.</p>

<p>Let’s see how it works in our design. Suppose we have an existing shopping list in Amazon Echo Show and want to add a new object to the list using voice. Duplicate the following artboard:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c285ad-8dcb-4e9b-8af6-a6324d4a66c5/4-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c285ad-8dcb-4e9b-8af6-a6324d4a66c5/4-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="Artboard: shopping list. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c285ad-8dcb-4e9b-8af6-a6324d4a66c5/4-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="Artboard: shopping list." >}}

<p>Let’s introduce some changes in the layout: Add a new object. We aren’t limited here, so we can easily modify any properties such as text attributes, color, opacity, position of the object &mdash; basically, any changes we make, XD will animate between them.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63315bab-554b-404d-96b9-2090a6fd8ff5/8-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63315bab-554b-404d-96b9-2090a6fd8ff5/8-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="Two artboards: our original shopping list and its duplicate with a new item. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63315bab-554b-404d-96b9-2090a6fd8ff5/8-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="Two artboards: our original shopping list and its duplicate with a new item." >}}

<p>When you wire two artboards together in prototype mode using Auto-Animate in “Action”, XD will automatically animate the differences in properties between each artboard.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/023abd09-537d-40ae-8e21-b6050acb06fc/6-designing-multimodal-interfaces-using-adobe-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/023abd09-537d-40ae-8e21-b6050acb06fc/6-designing-multimodal-interfaces-using-adobe-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/023abd09-537d-40ae-8e21-b6050acb06fc/6-designing-multimodal-interfaces-using-adobe-xd.png'>Large preview</a>)" alt="When you wire two artboards together in prototype mode using Auto-Animate in “Action”, XD will automatically animate the differences in properties between each artboard." >}}

<p>And here’s how the interaction will look to users:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf60f256-ba6a-4d64-80c3-95e929f33ff8/10-designing-multimodal-interfaces-using-adobe-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf60f256-ba6a-4d64-80c3-95e929f33ff8/10-designing-multimodal-interfaces-using-adobe-xd.gif" width=“600" height="375" alt="A GIF showing how the interaction will look to users" /></a></figure>

<p>One crucial thing that requires mentioning: Keep the names of all of the layers the same; otherwise, Adobe XD won’t be able to apply the auto-animation.</p>

## Conclusion

<p>We’re at the dawn of a user interface revolution. A new generation of interfaces &mdash; multimodal interfaces &mdash; not only will give users more power, but will also change the way users interact with systems. We will probably still have displays, but we won’t need keyboards to interact with the systems.</p>

<p>At the same time, the fundamental requirements for designing multimodal interfaces won’t be much different from those of designing modern interfaces. Designers will need to keep the interaction simple; focus on the user and their needs; design, prototype, test and iterate.</p>

<p>And the great thing is that you don’t need to wait to start designing for this new generation of interfaces. You can start today.</p>

*This article is part of the UX design series sponsored by Adobe. Adobe XD tool is made for a [fast and fluid UX design process](https://smashed.by/multimodal-interfaces), as it lets you go from idea to prototype faster. Design, prototype and share — all in one app. You can check out more inspiring projects created with [Adobe XD on Behance](https://www.behance.net/galleries/adobe/5/XD), and also [sign up for the Adobe experience design newsletter](https://adobe.ly/2yKueO8) to stay updated and informed on the latest trends and insights for UX/UI design.*

{{< signature "ms, ra, al, yk, il" >}}