---
title: Designing Voice Experiences
slug: designing-voice-experiences
image: null
date: 2017-05-03T16:05:06.000Z
author: lyndon-cerejo
description: >-
  Voice-based interfaces are becoming commonplace. Voice assistants such as Siri
  and Cortana have been around for a few years, but this past holiday season,
  voice-driven devices from Amazon and Google made their way into millions of
  homes.

  Recent analysis from VoiceLabs estimates that 24.5 million voice-driven
  devices will be shipped this year, almost four times as many as last year. As
  experience designers, we now have the opportunity to design voice experiences
  and interfaces!
categories:
  - Coding
  - Mobile
  - Accessibility
  - UI
---
Recent [analysis from VoiceLabs](https://voicelabs.co/2017/01/15/the-2017-voice-report/) estimates that 24.5 million voice-driven devices will be shipped this year, almost four times as many as last year. As experience designers, we now have the opportunity to design voice experiences and interfaces!

<p>A new interface does not mean that we have to disregard everything we have successfully applied to previous interfaces; we will need to adapt our process for the nuances of voice-driven interfaces, including conversational interactions and the lack of a screen. We will look at how a typical genie in a bottle works, discuss <strong>the steps involved in designing voice experiences</strong>, and illustrate these steps by designing a voice app for Alexa (or Skill, as Amazon calls it).<p>

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Enhancing User Experience With The Web Speech API'" href="https://www.smashingmagazine.com/2014/12/enhancing-ux-with-the-web-speech-api/" rel="bookmark">Enhancing User Experience With The Web Speech API</a></li>
<li><a title="Read 'Guidelines For Designing With Audio'" href="https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/" rel="bookmark">Guidelines For Designing With Audio</a></li>
<li><a title="Read 'Experimenting With speechSynthesis'" href="https://www.smashingmagazine.com/2017/02/experimenting-with-speechsynthesis/" rel="bookmark">Experimenting With speechSynthesis</a></li>
<li><a title="Read 'What Is User Experience Design? Overview, Tools And Resources'" href="https://www.smashingmagazine.com/2010/10/what-is-user-experience-design-overview-tools-and-resources/" rel="bookmark">What Is User Experience Design? Overview, Tools And Resources</a></li>
</ul>

{{% feature-panel %}}

## Understanding Voice Interfaces

Just as mobile apps run on an OS and a device, three layers have to work together to enable voice interactions:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d987971d-b5e7-4d8d-aaee-a591e16348a0/voice-interface-stack-500w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d987971d-b5e7-4d8d-aaee-a591e16348a0/voice-interface-stack-500w-opt.png" alt="Layers of Voice User Interface" width="500" height="" /></a><figcaption>The layers that enable voice interactions</figcaption></figure>

<ol>
 	<li>voice app (Amazon Skills and Actions for Google);</li>
 	<li>artificial intelligence platform (Amazon Alexa, Google Assistant, Apple Siri, Microsoft Cortana);</li>
 	<li>device (Echo, Home, smartphones, computers).</li>
</ol>

Each layer uses the one below and supports the one above it. The voice interface lies in the upper two layers, both of which reside in the cloud, not on the device itself.

Let's peek under the hood to see how these layers work together, using the Alexa Jeopardy! Skill as an example.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37758b06-bfb0-4837-bb66-6c4f48b13108/voice-interface-stack-example-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ccf81eb-43b6-4529-b27e-229b501ad77a/voice-interface-stack-example-780w-opt.png" alt="How voice interfaces work - Jeopardy skill example" width="780" height="813" /></a><figcaption>The layers that enable voice interactions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37758b06-bfb0-4837-bb66-6c4f48b13108/voice-interface-stack-example-large-opt.png">View large version</a>)</figcaption></figure>

Voice-driven devices such as the Amazon Echo and Google Home are constantly listening, waiting for a wake word ("Alexa…" or "OK, Google…") to jump into action. Once activated, the device sends the audio that follows to the AI platform in the cloud ("… play Jeopardy!"). The platform uses a combination of <a href="https://en.wikipedia.org/wiki/Speech_recognition">automatic speech recognition</a> (ASR) and <a href="https://en.wikipedia.org/wiki/Natural_language_understanding">natural language understanding</a> (NLU) to decipher the user's intent (to start a trivia game) and send it to the supporting app (Jeopardy! J6 Skill on Alexa). The app processes the request and responds through text (and a visual if applicable). The platform converts the text to speech and plays it through the device ("Welcome to Jeopardy J6. Here are today's clues…"). All this in matter of seconds.</p>

## Building Voice Experiences

Last year, Mark Zuckerberg took on a personal challenge to <a href="https://www.facebook.com/notes/mark-zuckerberg/building-jarvis/10154361492931634">build a simple AI</a> to run his home. He did, called it Jarvis and gave it the <a href="https://www.facebook.com/zuck/videos/10103353413344571/">voice of Morgan Freeman</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c878ec-09cf-42b4-b8d3-9ba003475e07/zuckerberg-freeman-500w-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c878ec-09cf-42b4-b8d3-9ba003475e07/zuckerberg-freeman-500w-opt.jpg" alt="Mark Zuckerberg introduces Morgan Freeman to the AI that uses his voice" width="500" height="" /></a><figcaption>Mark Zuckerberg introduces Morgan Freeman to the AI that uses his voice. (Image: <a href="https://www.facebook.com/photo.php?fbid=10103410869691591&amp;set=pb.4.-2207520000.1486318705.&amp;type=3&amp;theater">Mark Zuckerberg</a>)</figcaption></figure>

The rest of us who don't have the ability or resources to do the same can get away with building voice apps that run on complex AI platforms that have already been built. This frees us to only have to worry about the design and development of the voice app, that too with a simplified development process. <a href="https://developer.amazon.com/alexa-skills-kit">Amazon</a> and <a href="https://developers.google.com/actions/">Google</a> have provided open access to templates, code, and detailed step-by-step instructions to build different types of voice apps, to the point that even non-developers could develop an app in around an hour!

Their investment in simplifying app development is paying off, with <a href="https://voicebot.ai/2017/02/28/amazon-alexa-now-has-10k-skills-including-europe/">thousands of new voice apps being launched every month</a>. The growth in voice apps brings back memories of the '90s web gold rush, as well as the explosion of mobile apps that followed the launch of app stores.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb424b50-f1f6-4976-8257-4165fce759a8/alexa-skills-category-may-2017-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a7525a-4923-48e1-8df0-9017beade73b/alexa-skills-category-may-2017-780w-opt-copy.png" alt="Breakdown of Alexa Skills by category as of May 2017" width="780" height="550" /></a><figcaption>Breakdown of Alexa Skills by category as of May 2017. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb424b50-f1f6-4976-8257-4165fce759a8/alexa-skills-category-may-2017-large-opt.png">View large version</a>)</figcaption></figure>

In a crowded voice marketplace, good design is what will differentiate your voice app from the hundreds of other similar apps.</p>

## Designing Voice Experiences

Designing a good voice user experience is a five-step process that should take place before starting development. Though jumping straight into development might be tempting, the time spent getting the design right is time well spent.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3024c044-fd4d-4129-9bc0-dbe057430e2d/designing-voice-experiences-steps-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f608811-f19f-46b4-b284-ec0d067d4716/designing-voice-experiences-steps-780w-opt.png" alt="Steps in designing voice experiences" width="780" height="290" /></a><figcaption>The steps in designing voice experiences (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3024c044-fd4d-4129-9bc0-dbe057430e2d/designing-voice-experiences-steps-large-opt.png">View large version</a>)</figcaption></figure>

We will discuss and apply each step to design a voice app, which could easily be developed using one of many <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/content/alexa-skills-developer-training#templates">Skill templates for Alexa</a>.</p>

## 1. Discover

The design journey begins with the question, "How will this voice app provide value to my users?" This question applies whether you are developing a standalone voice app (like our example) or whether your voice app is just one of many touchpoints for your customers. Take into consideration why and where people use voice apps. People use voice interfaces because of the benefits of hands-free interaction, the speed of interaction and the ease of use, primarily using it at home or in the car, as shown in Mary Meeker's <a href="https://www.kpcb.com/blog/2016-internet-trends-report">2016 Internet Trends Report</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8e811e6-fdcf-45ad-91b0-b13e8b982c0b/voice-reasons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6d125ef-e255-4be6-87b4-927a8cb3e95d/voice-reasons-780w-opt.png" alt="Top reasons to use voice interfaces" width="780" height="383" /></a><figcaption>Top reasons to use voice interfaces (callouts by author) (Source: <a href="https://www.kpcb.com/blog/2016-internet-trends-report">KPCB</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8e811e6-fdcf-45ad-91b0-b13e8b982c0b/voice-reasons-large-opt.png">View large version</a>)</figcaption></figure>

The key is to find consistent user needs that are easier or more convenient through a voice app rather than a phone or a computer. Some examples include banks providing account information or a moviegoer finding new movies playing nearby.

If you have competitors who already have voice apps, take into consideration what they are doing and the reviews and feedback their apps have received in the app marketplace (such as <a href="https://www.amazon.com/b?ie=UTF8&amp;node=13727921011">Amazon's Alexa Skill Store</a>). The aim is not to blindly imitate, but to be aware of the capabilities bar that has been set, as well as user expectations.

(At the time of writing this, there were over 1,500 "knowledge and trivia" Alexa Skills, making it the most crowded Skill categories on Amazon. However, there wasn't a single trivia skill catering to the area of user experience. To illustrate the voice design process, we will create a UX design skill, for our readers to test their knowledge or maybe even to learn something new.)

## 2. Define

During this step, we will define the personality of our app and the capabilities it will have.
### Personality

When designing voice interfaces, we don't have access to many of the visual elements we use in web and mobile interfaces to show a personality. The personality has to come through the voice and tone of verbal interactions. And unlike Zuckerberg, who hears Freeman's soothing voice, we are constrained to hearing the default voice of the device. That makes tone and wording crucial in conveying the personality we want to convey.

The good news is that most of the groundwork in this area should have already been completed and documented in a corporate brand guide or website style guide (hint: look for the "tone of voice" section). Leverage those guidelines for your voice app, as well to maintain a consistent personality across channels and touchpoints.

When I think of personality and tone, the Virgin Group immediately comes to mind. They clearly define who they are and how they convey that to users. For Virgin America, the ideal tone is "hip, easygoing, informal, playful and tongue in cheek," and it comes across clearly in all their communication.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b543392-1e17-461c-b545-e5a8a70f2234/virgin-brand-personality-730w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b543392-1e17-461c-b545-e5a8a70f2234/virgin-brand-personality-730w-opt.png" alt="Virgin America brand personality" width="731" height="" /></a><figcaption>Virgin America's brand personality (Source: <a href="https://vxbrandguidelines.com/">Virgin America</a>)</figcaption></figure>

If you've ever asked Alexa to sing or tried any of the numerous <a href="https://turbofuture.com/consumer-electronics/200-Amusing-Amazon-Echo-Easter-Eggs">Alexa Easter Eggs</a>, then you'll know she has a personality of her own. Curious, I reached out to the team responsible for her personality, and here's what they had to say:
<blockquote>When architecting Alexa's voice, we tried to give her a personality that reflects the attributes we value most at Amazon. We wanted her to feel helpful, humble and smart, while still maintaining a sense of fun. This is an ongoing process, and we expect the voice of Alexa will evolve as more developers focus on making her smarter.</blockquote>

Personality can also be reflected in the app's name, icon and description that are displayed to users in the app directory listing, as well as in the name used to invoke the app (the invocation name). So, make sure it shines through while publishing your app.

For our UX Design skill, we could take a straightforward or a funny approach, and that would be reflected in the wording of our quiz' Q&amp;A options.

An example of a <strong>normal tone</strong> would be:
<blockquote>Which UX design principle favors simplicity over complexity?
<ol>
 	<li>Occam's Razor</li>
 	<li>Hick's Law</li>
 	<li>Aesthetic-usability effect</li>
 	<li>Satisficing</li>
</ol>

</blockquote>

And an example of a <strong>funny tone</strong> would be:
<blockquote>Apparently, there's a UX design principle that favors simplicity over complexity. Really! Can you guess what it's called?
<ol>
 	<li>Occam's Razor: The best a UX guy can get.</li>
 	<li>Hick's Law: Sounds like something a UX bumpkin would come up with.</li>
 	<li>Aesthetic-usability effect: That's some fancy UX jargon.</li>
 	<li>Satisficing: I can't get no satisficing… apologies to the Rolling Stones.</li>
</ol>

</blockquote>

Yeah, let's stick with normal.
### Capabilities

This is where you carefully think of the functionality that will be valuable for your voice app's users. Revisit your work from the first step to identify the capabilities that are core or related to your business. Sometimes offering core capabilities is a no-brainer — such as a bank offering information on balance, transactions and due dates. Others offer value in the form of related features, such as Tide's stain-removal guide voice app, or Glad's (makers of food storage and trash bags) voice apps, one of which helps users to remember where they stored their leftovers, or the other one that allows users to check which items should be recycled or disposed of in the trash.

If you did a similar exercise when going from web to mobile, that can serve as a starting point. For voice capabilities, consider what capabilities would benefit your users on a voice-driven device in a shared space. If a Skill has security or privacy implications, consider adding a level of protection (the Capital One Alexa Skill allows users to create a personal key for account access). While you may end up with a laundry list of functionality that would work over voice, start with one to five core capabilities, and use voice analytics to update and improve after launch.

The core capabilities of a UX design Skill could be:
<ol>
 	<li>provide a UX design principle on demand;</li>
 	<li>quiz the user (single player) on a random UX principle;</li>
 	<li>quiz the user (single player) on multiple UX principle, and keep score;</li>
 	<li>hold a UX quiz competition with multiple players.</li>
</ol>

Because we are building this UX design Skill using Amazon's Skill templates, our choices are currently restricted to either the first (fact skill template) or third (trivia skill template) option above. Assuming that our research has shown that our users would find a quiz more valuable than just hearing a UX principle recited, our core capability will be to quiz the user on UX principles and to keep score.</p>

## 3. Detail Conversation Flow

Now that you have shortlisted the capabilities of your voice app, start focusing on the detailed conversation flow that the app will have with its users. Human conversation is complex; it often has many twists and turns and may pivot anytime, with people often jumping from one topic to another. Voice AI platforms still have a long way to go to match that level of complexity, so you have to teach your Skill how to respond to users.

Your voice app can only support the capabilities you have defined in the previous step, but users always have the ability to ask the app anything and in any format. Detailing a conversation flow allows you to respond to the user, or to drive the conversation towards what the app can do for the user.

For each capability that the voice app will support, start creating conversational dialogues between the user and the app, similar to dialogues in a screenplay. As you write these dialogues, remember the personality as well as voice and tone characteristics. Start creating and curating the actual content for your voice app; for our quiz, this would mean building the list of quiz questions.

Begin with the "happy path" — a conversational flow in which the voice app can respond to the user's request without any exceptions or errors. Then, move on to detailing the conversational flow for exceptions (in which the user does not provide complete information) and errors (in which the voice app does not understand or cannot do what the user is asking).

Because the conversation will be heard and not read, a good practice is to read it out loud to see if it sounds like a natural spoken conversation, and to check that it conveys the tone of voice you've intended.

If your voice app needs to supplement the conversation with content displayed on the phone app, design these interactions together, so that they appear seamless to the user. For instance, Tide's stain-removal Skill informs the user that they could also refer to the stain-removal steps in the Alexa app, in addition to hearing the instructions. This may soon be required if the <a href="https://www.engadget.com/2016/11/29/amazon-touchscreen-speaker-leak/">rumors of a touchscreen on the new Echo</a> are true.

Here is a sample dialogue for the happy path our UX design Skill's core capability:
<blockquote><strong>User</strong>: "Alexa, start the UX design quiz."

<strong>Alexa</strong>: "I will ask you five questions, with multiple choice answers. Try to get as many right as you can. Just say the number of the answer. Let's begin. Question 1…"

<strong>User</strong>: [responds correctly]

<strong>Alexa</strong>: "That's correct! Your score is 1. Here's question 2…"

<strong>User</strong>: [responds incorrectly]

<strong>Alexa</strong>: "Oops, that's the wrong answer. The correct answer is [correct answer]. Your score is 1. Here's question 3…"

…

<strong>Alexa</strong> (at the end of five questions): "That's correct! You got four out of five questions correct. Thank you for playing!"</blockquote>

## 4. Describe Alternate Phrases

People don't always use the same words to say the same thing, and voice apps need to be taught that. Phrase-mapping is an exercise to teach voice apps to accommodate variation in the way users phrase their requests.

For each conversational path that you detailed in the previous step, think about the different ways users could word those requests. Then break down the wording of each request, and identify word variations and synonyms that they might use, taking into account any regional variations and dialects. You will have your hands full if your voice app deals with sweetened carbonated beverages (soda, pop, coke, tonic, soft drink, fizzy drink), long sandwiches (sub, grinder, hoagie, hero, poor boy, bomber, Italian sandwich, baguette) or athletic footwear (sneakers, shoes, gym shoes, sand shoes, jumpers, tennis shoes, running shoes, runners, trainers).

Make this list of variations as complete and exhaustive as possible, so that your voice app can understand user requests. Alexa needs these variations in the form of "utterances" and recommends providing "… <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/defining-the-voice-interface#h2_sample_utterances">as many representative phrases as possible</a>." Depending on the capabilities of your voice app, the number of utterances could easily run into the hundreds, but there are ways to <a href="https://www.makermusings.com/2015/07/21/defining-utterances-for-the-alexa-skills-kit/">simplify the generation of utterances</a>.

Here's a sample phrase-mapping for a capability of our UX design quiz. Alexa's AI platform does a good job of translating user intent for Skills based on their templates. However, if you make changes (like we changed "trivia game" to "quiz"), then these phrases will have to be added.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b65650-2c5f-4ae0-b3e8-c298193a29e3/phrase-mapping-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee08b13-edbf-4026-96fb-9352057fc6ff/phrase-mapping-780w-opt.png" alt="Sample phrase mapping" width="780" height="437" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b65650-2c5f-4ae0-b3e8-c298193a29e3/phrase-mapping-large-opt.png">View large version</a></figcaption></figure>

## 5. Refine

The final step in the design process is to validate and refine the voice application before spending time and effort on development. During the "detail" step, reading the conversation flows aloud helped to make sure that they sounded natural and conversational. The current step involves testing the voice interface with users.

The simplest way to test is using the Wizard of Oz technique, with a person playing the role of the voice-driven device and responding to the user based on the voice interface script. Another option is to use prototyping software such as <a href="https://www.sayspring.com/">SaySpring</a> to create and test interactive prototypes.

If your voice app is being built using code templates (as our app is), then it might be easier to create the app and test it using testing tools provided by <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/testing-an-alexa-skill#h2_servicesim">Amazon</a> and <a href="https://developers.google.com/actions/tools/web-simulator">Google</a> within the Skill development area (as shown below), or in test mode on an actual device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aec9c9da-dd67-4f78-92d1-b10365529a6c/alexa-simulator-500w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aec9c9da-dd67-4f78-92d1-b10365529a6c/alexa-simulator-500w-opt.png" alt="Alexa skill simulator" width="500" height="" /></a></figure>

This testing will give you a good feel for the voice experience in the real world, including handling of errors, repetitive responses, and unnatural, forced or machine-like replies.</p>

## Develop

Now that the voice experience has been designed, it is time to move to the build-test-submit phase. Each platform has detailed guides and tutorials to help anyone build and test skills, including <a href="https://developer.amazon.com/alexa-skills-kit#Ready%20to%20start%3F">Alexa Skills Kit</a>, <a href="https://developers.google.com/actions/develop/conversation">Develop Actions for Google</a>, and <a href="https://developer.microsoft.com/en-us/cortana">Cortana</a>, which offers to reuse your custom Alexa skill code!

Think about your feedback loop and the analytics that will help you to understand usage of your voice app. You can get Skill metrics (users, sessions, utterances, intents) within your developer account without any additional coding, but advanced analytics are available through free services such as <a href="https://voicelabs.co/">VoiceLabs</a> (I could not get it to work, probably due to my lack of coding skills or the lack of a <em>VoiceLabs for Dummies</em> setup guide).

After you finish building and testing your voice app, the last step is a <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/publishing-an-alexa-skill">streamlined submission process</a>. Because the Alexa Skill marketplace has rapidly grown, discovering new and useful apps is getting difficult. Until Amazon improves this, use visible elements of your voice app listing to help users find and try your Skill, including a catchy and relevant skill icon, name and description.

The companion skill that was built as an illustration can be taken for a test drive on the Amazon Alexa Skill store: <a href="https://www.amazon.com/dp/B06X6FHKSL">UX Design Quiz</a>

## Guiding Principles

Here are a few guiding principles for designing voice experiences. More principles and detailed do's and don'ts are offered by <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-voice-design-best-practices">Amazon</a> and <a href="https://developers.google.com/actions/design">Google</a>.
### Onboard the User and Help Them Get Started

Introduce the app and the ways the user can engage with it.
<blockquote>Welcome to UX Design Quiz. I will ask you five questions about UX design and see how many you get right. You can ask me to repeat a question or pause if you need to. Would you like to start a new quiz?</blockquote>

### Keep conversation exchanges brief to reduce cognitive load.

With a voice user interface, the user has to use their short-term memory while interacting with the voice app. So, keep it short and sweet.
<blockquote><strong>Alexa</strong>: "This principle is attributed to a 14th-century logician and Franciscan friar and is named after the village in the English county of Surrey where he was born. In a nutshell, it states that simplicity is better than complexity. This problem-solving principle can easily be applied to user experience design, by going for the simpler design solution. What is this principle called?
<ol>
 	<li>Your first option is Occam's Razor, sometimes known as Ockham's razor, or the law of parsimony.</li>
 	<li>Your next option is Hick's Law, also known as the Hick-Hyman Law.</li>
 	<li>Your next option is the aesthetic-usability effect.</li>
 	<li>Your last option is called "satisficing," not to be confused with "satisfying" or "sacrificing."</li>
</ol>

Please say A, B, C, or D to make your selection."

<strong>User</strong>: "Huh?! Alexa, repeat. On second thought, end quiz!"</blockquote>

### Examples Work Better Than Instructions

<blockquote>Instruction: "Please say your date of birth in the month/day/year format."

Example: "Please say your date of birth, like April 15, 1990."</blockquote>

### Delight Without Interfering With the Task

This is a balancing act. Too much and it gets tiresome quickly.
### Use Explicit Confirmations for Important Actions, and Implicit for Less Risky

If you ask Alexa to turn off the lights, you can see it happen and do not need a verbal confirmation, although she sometimes confirms with a short "OK."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c167abce-d184-4397-95e9-dfc030041947/leftover-skill-feedback-570w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c167abce-d184-4397-95e9-dfc030041947/leftover-skill-feedback-570w-opt.png" alt="Don't interfere, reduce repetitiveness" width="570" height="" /></a><figcaption>User feedback for the Glad Leftover Skill highlights two principles above.</figcaption></figure>

### Design for Failure

Things will go wrong: design for those situations. Examples include unintelligible questions or information, incomplete information, silence or requests that cannot be handled. Acknowledge, and give the user options to recover.
### Respect the User's Privacy and Security

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12ee61f9-b097-404c-8310-2eb2955e4737/bank-skill-feedback-500w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12ee61f9-b097-404c-8310-2eb2955e4737/bank-skill-feedback-500w-opt.png" alt="Respect user privacy and security" width="500" height="" /></a><figcaption>User feedback for a bank Skill highlights issues with security, despite passing <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-security-testing">Alexa Skill Security requirements</a>.</figcaption></figure>

## Conclusion

<blockquote>Anytime you're dealing with trying to interact with a human, you have to think of humans as very advanced operating systems. Your highest goal is to try to emulate them.

– K.K Barrett, Her movie production designer, Wired, 2014</blockquote>

If you haven't seen the movie Her, take a couple of hours to watch this futuristic movie about a lonely writer who develops a relationship with an operating system. While it is science fiction, in today's world, voice experiences are increasing with the adoption of standalone voice-driven devices, such as the Amazon Echo family and Google Home. Developing a voice app is a relatively simple, template-driven process, with IKEA-like instructions provided by Amazon and Google in an attempt to establish their platforms. Though jumping into development may be tempting, a good voice user experience doesn't just happen; it has to be designed, going through the steps described in this article.

Please use the comments area to share any other feedback, tips and resources with other readers.</p>

## Resources

### AI Platform Tools

<ul>
 	<li><a href="https://developer.amazon.com/alexa-skills-kit">Alexa Skills Kit</a>, Amazon</li>
 	<li><a href="https://developers.google.com/actions/">Actions for Google</a></li>
 	<li>"<a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-voice-design-best-practices">Alexa Skills Kit Voice Design Best Practices</a>," Amazon</li>
 	<li><a href="https://developers.google.com/actions/design">Actions for Google design resources</a></li>
</ul>

### Tone of Voice

<ul>
 	<li>"<a href="https://www.nngroup.com/articles/tone-voice-users/">The Impact of Tone of Voice on Users' Brand Perception</a>," Kate Meyer, Nielsen Norman Group</li>
 	<li>"<a href="https://www.smashingmagazine.com/2012/08/finding-tone-voice/">Finding Your Tone of Voice</a>," Robert Mills, Smashing Magazine</li>
 	<li>"<a href="https://www.distilled.net/tone-of-voice/">Finding Your Brand's Voice</a>," Harriet Cummings, Distilled</li>
</ul>

### Phrases and Dialects

<ul>
 	<li>"<a href="https://www.nytimes.com/interactive/2013/12/20/sunday-review/dialect-quiz-map.html">How Y'all, Youse and You Guys Talk</a> (interactive quiz), New York Times</li>
 	<li><a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/defining-the-voice-interface">Defining the Voice Interface</a> (and Alexa utterances), Amazon</li>
 	<li>"<a href="https://www.makermusings.com/2015/07/21/defining-utterances-for-the-alexa-skills-kit/">Defining Utterances for the Alexa Skills Kit</a>" (including <a href="https://www.makermusings.com/amazon-echo-utterance-expander/">the tool</a>), Maker Musings</li>
</ul>

### Prototyping and Testing

Here's a sample phrase-mapping for a capability of our UX design quiz. Alexa's AI platform does a good job of translating user intent for Skills based on their templates. However, if you make changes (like we changed "trivia game" to "quiz"), then these phrases will have to be added.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b65650-2c5f-4ae0-b3e8-c298193a29e3/phrase-mapping-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ee08b13-edbf-4026-96fb-9352057fc6ff/phrase-mapping-780w-opt.png" alt="Sample phrase mapping" width="780" height="437" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b65650-2c5f-4ae0-b3e8-c298193a29e3/phrase-mapping-large-opt.png">View large version</a></figcaption></figure>

## 5. Refine

The final step in the design process is to validate and refine the voice application before spending time and effort on development. During the "detail" step, reading the conversation flows aloud helped to make sure that they sounded natural and conversational. The current step involves testing the voice interface with users.

The simplest way to test is using the Wizard of Oz technique, with a person playing the role of the voice-driven device and responding to the user based on the voice interface script. Another option is to use prototyping software such as <a href="https://www.sayspring.com/">SaySpring</a> to create and test interactive prototypes.

If your voice app is being built using code templates (as our app is), then it might be easier to create the app and test it using testing tools provided by <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/testing-an-alexa-skill#h2_servicesim">Amazon</a> and <a href="https://developers.google.com/actions/tools/web-simulator">Google</a> within the Skill development area (as shown below), or in test mode on an actual device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aec9c9da-dd67-4f78-92d1-b10365529a6c/alexa-simulator-500w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aec9c9da-dd67-4f78-92d1-b10365529a6c/alexa-simulator-500w-opt.png" alt="Alexa skill simulator" width="500" height="" /></a></figure>

This testing will give you a good feel for the voice experience in the real world, including handling of errors, repetitive responses, and unnatural, forced or machine-like replies.</p>

## Develop

Now that the voice experience has been designed, it is time to move to the build-test-submit phase. Each platform has detailed guides and tutorials to help anyone build and test skills, including <a href="https://developer.amazon.com/alexa-skills-kit#Ready%20to%20start%3F">Alexa Skills Kit</a>, <a href="https://developers.google.com/actions/develop/conversation">Develop Actions for Google</a>, and <a href="https://developer.microsoft.com/en-us/cortana">Cortana</a>, which offers to reuse your custom Alexa skill code!

Think about your feedback loop and the analytics that will help you to understand usage of your voice app. You can get Skill metrics (users, sessions, utterances, intents) within your developer account without any additional coding, but advanced analytics are available through free services such as <a href="https://voicelabs.co/">VoiceLabs</a> (I could not get it to work, probably due to my lack of coding skills or the lack of a <em>VoiceLabs for Dummies</em> setup guide).

After you finish building and testing your voice app, the last step is a <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/publishing-an-alexa-skill">streamlined submission process</a>. Because the Alexa Skill marketplace has rapidly grown, discovering new and useful apps is getting difficult. Until Amazon improves this, use visible elements of your voice app listing to help users find and try your Skill, including a catchy and relevant skill icon, name and description.

The companion skill that was built as an illustration can be taken for a test drive on the Amazon Alexa Skill store: <a href="https://www.amazon.com/dp/B06X6FHKSL">UX Design Quiz</a>

## Guiding Principles

Here are a few guiding principles for designing voice experiences. More principles and detailed do's and don'ts are offered by <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-voice-design-best-practices">Amazon</a> and <a href="https://developers.google.com/actions/design">Google</a>.
### Onboard the User and Help Them Get Started

Introduce the app and the ways the user can engage with it.
<blockquote>Welcome to UX Design Quiz. I will ask you five questions about UX design and see how many you get right. You can ask me to repeat a question or pause if you need to. Would you like to start a new quiz?</blockquote>

### Keep conversation exchanges brief to reduce cognitive load.

With a voice user interface, the user has to use their short-term memory while interacting with the voice app. So, keep it short and sweet.
<blockquote><strong>Alexa</strong>: "This principle is attributed to a 14th-century logician and Franciscan friar and is named after the village in the English county of Surrey where he was born. In a nutshell, it states that simplicity is better than complexity. This problem-solving principle can easily be applied to user experience design, by going for the simpler design solution. What is this principle called?
<ol>
 	<li>Your first option is Occam's Razor, sometimes known as Ockham's razor, or the law of parsimony.</li>
 	<li>Your next option is Hick's Law, also known as the Hick-Hyman Law.</li>
 	<li>Your next option is the aesthetic-usability effect.</li>
 	<li>Your last option is called "satisficing," not to be confused with "satisfying" or "sacrificing."</li>
</ol>

Please say A, B, C, or D to make your selection."

<strong>User</strong>: "Huh?! Alexa, repeat. On second thought, end quiz!"</blockquote>

### Examples Work Better Than Instructions

<blockquote>Instruction: "Please say your date of birth in the month/day/year format."

Example: "Please say your date of birth, like April 15, 1990."</blockquote>

### Delight Without Interfering With the Task

This is a balancing act. Too much and it gets tiresome quickly.
### Use Explicit Confirmations for Important Actions, and Implicit for Less Risky

If you ask Alexa to turn off the lights, you can see it happen and do not need a verbal confirmation, although she sometimes confirms with a short "OK."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c167abce-d184-4397-95e9-dfc030041947/leftover-skill-feedback-570w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c167abce-d184-4397-95e9-dfc030041947/leftover-skill-feedback-570w-opt.png" alt="Don't interfere, reduce repetitiveness" width="570" height="" /></a><figcaption>User feedback for the Glad Leftover Skill highlights two principles above.</figcaption></figure>

### Design for Failure

Things will go wrong: design for those situations. Examples include unintelligible questions or information, incomplete information, silence or requests that cannot be handled. Acknowledge, and give the user options to recover.
### Respect the User's Privacy and Security

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12ee61f9-b097-404c-8310-2eb2955e4737/bank-skill-feedback-500w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12ee61f9-b097-404c-8310-2eb2955e4737/bank-skill-feedback-500w-opt.png" alt="Respect user privacy and security" width="500" height="" /></a><figcaption>User feedback for a bank Skill highlights issues with security, despite passing <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-security-testing">Alexa Skill Security requirements</a>.</figcaption></figure>

## Conclusion

<blockquote>Anytime you're dealing with trying to interact with a human, you have to think of humans as very advanced operating systems. Your highest goal is to try to emulate them.

– K.K Barrett, Her movie production designer, Wired, 2014</blockquote>

If you haven't seen the movie Her, take a couple of hours to watch this futuristic movie about a lonely writer who develops a relationship with an operating system. While it is science fiction, in today's world, voice experiences are increasing with the adoption of standalone voice-driven devices, such as the Amazon Echo family and Google Home. Developing a voice app is a relatively simple, template-driven process, with IKEA-like instructions provided by Amazon and Google in an attempt to establish their platforms. Though jumping into development may be tempting, a good voice user experience doesn't just happen; it has to be designed, going through the steps described in this article.

Please use the comments area to share any other feedback, tips and resources with other readers.</p>

## Resources

### AI Platform Tools

<ul>
 	<li><a href="https://developer.amazon.com/alexa-skills-kit">Alexa Skills Kit</a>, Amazon</li>
 	<li><a href="https://developers.google.com/actions/">Actions for Google</a></li>
 	<li>"<a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-voice-design-best-practices">Alexa Skills Kit Voice Design Best Practices</a>," Amazon</li>
 	<li><a href="https://developers.google.com/actions/design">Actions for Google design resources</a></li>
</ul>

### Tone of Voice

<ul>
 	<li>"<a href="https://www.nngroup.com/articles/tone-voice-users/">The Impact of Tone of Voice on Users' Brand Perception</a>," Kate Meyer, Nielsen Norman Group</li>
 	<li>"<a href="https://www.smashingmagazine.com/2012/08/finding-tone-voice/">Finding Your Tone of Voice</a>," Robert Mills, Smashing Magazine</li>
 	<li>"<a href="https://www.distilled.net/tone-of-voice/">Finding Your Brand's Voice</a>," Harriet Cummings, Distilled</li>
</ul>

### Phrases and Dialects

<ul>
 	<li>"<a href="https://www.nytimes.com/interactive/2013/12/20/sunday-review/dialect-quiz-map.html">How Y'all, Youse and You Guys Talk</a> (interactive quiz), New York Times</li>
 	<li><a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/defining-the-voice-interface">Defining the Voice Interface</a> (and Alexa utterances), Amazon</li>
 	<li>"<a href="https://www.makermusings.com/2015/07/21/defining-utterances-for-the-alexa-skills-kit/">Defining Utterances for the Alexa Skills Kit</a>" (including <a href="https://www.makermusings.com/amazon-echo-utterance-expander/">the tool</a>), Maker Musings</li>
</ul>

### Prototyping and Testing

<ul>
 	<li><a href="https://www.sayspring.com/">SaySpring</a>
"Free prototyping software for voice"</li>
 	<li><a href="https://echosim.io/">Echosim.io</a>
"Alexa Skill Testing Tool"</li>
 	<li>"<a href="https://developers.google.com/actions/tools/web-simulator">Web Simulator</a>," Actions for Google</li>
</ul>

### Report, Book and Movie

<ul>
 	<li>"<a href="https://voicelabs.co/2017/01/15/the-2017-voice-report/">The 2017 Voice Report by VoiceLabs</a>"</li>
 	<li><a href="https://shop.oreilly.com/product/0636920050056.do"><em>Designing Voice User Interfaces: Principles of Conversational Experiences</em></a>, Cathy Pearl, O'Reilly Media</li>
 	<li><a href="https://www.imdb.com/title/tt1798709/">Her</a> (movie)</li>
</ul>

{{< signature "da, vf, yk, al, il" >}}

