---
title: 'How To Create An Engaging And Useful Chatbot'
slug: create-engaging-useful-chatbot
author: marli-mesibov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/884aba47-5322-4856-be9f-33008ae4eed7/create-engaging-useful-chatbot.jpg
date: 2021-01-28T12:00:00.000Z
summary: >-
  What makes a good chatbot experience? Most people think of witty responses and machine learning, but the basis of a chatbot UX is actually rooted in content strategy. Learn how to develop a chatbot that sounds human and engages people.
description: >-
  What makes a good chatbot experience? Most people think of witty responses and machine learning, but the basis of a chatbot UX is actually rooted in content strategy. Learn how to develop a chatbot that sounds human and engages people.
categories:
  - UX
  - Design
  - Chatbots
---

Capital One. Adobe. Even Dominos has one. They’re chatbots, and they’re quickly becoming ubiquitous. A poor chatbot simply says “I’m sorry, I don’t understand” on repeat (or worse “error”.) A good chatbot feels almost-human, and helps answer questions so you don’t need to make a phone call or search the FAQ page.

But what makes a good chatbot experience? What are the [table stakes](https://www.uxbooth.com/articles/discovering-table-stakes-delighters/) that people expect from a chatbot, and what ruins that experience? In this article we’ll answer those questions and identify what you as a content designer can do to make your chatbot successful.

## What Makes A Chatbot Unique?

A chatbot is a program that replicates human conversation. Most chatbots use decision trees to create a conversation. They either recognize key words and respond accordingly, or they allow the end-user to select from options to direct the conversation.

Equally important to defining what a chatbot is, is identifying what it isn’t. Let’s dig into what a chatbot is &mdash; and clear up what it isn’t.

### A Chatbot Is A Form Of Conversational Design

Chatbots replicate human conversations, and most chatbots use [decision trees](https://towardsdatascience.com/decision-trees-in-machine-learning-641b9c4e8052) to do so. They either recognize key words and respond accordingly, or they allow the end-user to select from options to direct the conversation.

Conversational design broadly refers to any **conversation-like content**, whether that comes through headers and text on a webpage, voice UI such as Google Home and Alexa, or chatbots. As such, chatbot content is one *type* of conversational design, but the two are not one-and-the-same. A chatbot is also not a human interacting through a chat interface (that is sometimes called “live chat”). It is specifically a computerized system.

Why does this matter? When design and engineering teams are determining the best way to communicate with their audiences, they are likely to use shorthand. I frequently hear designers say “then we [the company] will tell them [the audience] to confirm their password.” In this case, the designer may be referring to “telling” the audience via text on a page, or they may be implying a chatbot will appear to inform the audience. Early on in the concepting phase it may not matter what form of conversational design the team has in mind, but ultimately the content team will be responsible for significantly more work if the end result is a chatbot. With that in mind, it’s useful to clarify what form of conversational design the team has in mind.

One example of non-chatbot conversational design is a **conversational UI**. [Oscar Insurance](https://www.hioscar.com/) has a conversational UI, which they develop with a few best practices:

- The headers are complete sentences.
- Forms have help text with specific instructions (instead of examples).
- Copy is written in the 2nd person, referring to the audience as “you”.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb590508-d13f-4e98-8130-a18bfb32a3b0/5-designing-voice-chatbot.png" width="800" height="569" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb590508-d13f-4e98-8130-a18bfb32a3b0/5-designing-voice-chatbot.png" sizes="100vw" caption="Oscar Insurance uses a conversational UI, though it is not a chatbot. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb590508-d13f-4e98-8130-a18bfb32a3b0/5-designing-voice-chatbot.png'>Large preview</a>)" alt="HiOscar’s Personalized Plan form. Header: Health insurance made for you. One field title is “Household annual income” and the help text is “Enter your income pre-tax.” Another field title is “Tax household size” and the help text is “Enter your tax household size." >}}

Voice UI can also “speak” to the audience, and if the team is considering that then they are either building a competitor to Alexa, Google Home, and Siri, or they are (more likely) building an [app that these systems can download](https://www.amazon.com/alexa-skills/b?ie=UTF8&node=13727921011). Again, these may sound the same from a concepting perspective, but the requirements are vastly different. Voice UI has no visual design, and no ability to trigger or prompt the end-user into action. This is in stark contrast to a phone app, which may launch notifications without the end-user first opening the app.

### A Chatbot Can Answer (Many) Questions

It may sound from this description as though chatbots are the perfect answer &mdash; they can launch notifications, they incorporate a visual UI, and they are conversational! Certainly, the popularity of chatbots is in part due to these benefits. But this can create an assumption that human conversation is the best way to connect with end-users. Sometimes that’s true &mdash; but not always!

In Michael J Metts’ Button talk “[Sorry, I Can’t Help WIth That](https://speakerdeck.com/mjmetts/sorry-i-cant-help-with-that-content-strategy-for-chatbots)” he said a company must know what its goal is, and then determine if a chatbot will help fulfill that goal. This is a fantastic approach: a chatbot is a solution, and should be employed when it is *the solution to a problem.*

Customer service and sales are typically good goals for chatbots to fulfill. In both cases the problem may be “how might our customer service team respond quickly to common questions” or “how might our sales team help customers learn about a product or service in a quick and easy manner, without using significant employee time?” In these cases a chatbot can help people get the answers they want without needing to call and wait on hold.

However, if the problem is “how might our hospital more accurately diagnose health issues” or “how might our bank more quickly help employees find lost paychecks from their employers” a chatbot may not be appropriate. A human physician is much more accurate than a chatbot, and the end-users will pick up on that. Equally, a bank’s chatbot is unlikely to be able to connect to the numerous employers’ payroll systems required to track down paychecks. While the end-user might think they want answers from a chatbot, they’ll quickly lose trust when the chatbot can’t answer their questions.

In short, a **chatbot is not a good way to handle nuances** or extremely complicated situations, because of the numerous opportunities for human error. There are simply too many variables for “quick” and “accurate” to be accomplished in these situations.

{{% feature-panel %}}

### A Chatbot Is Not An Algorithm

Never forget that a **chatbot is only as good as its content**. Yes, a chatbot is controlled by an algorithm, and can be bolstered by machine learning. But before machine learning can begin, the chatbot needs a set of rules, and needs content to speak. That’s the role of the content designer, UX writer, or content strategist to define.

We see this frequently in conversations around AI ethics. Voice assistants and chatbots are frequently identified as [sexist](https://news.un.org/en/story/2019/05/1038691) and [racially biased](https://civic.mit.edu/2019/01/24/how-automated-tools-discriminate-against-black-language/). They are not biased because the design and engineering team made a conscious choice to make them so. They are biased because they “reflect the biases in the viewpoints of the teams that built it,” to quote AI ethicist Josie Young [in her TED talk](https://www.ted.com/talks/josie_young_why_we_need_to_design_feminist_ai).

For those of us building chatbots, this means we need to be **consciously anti-sexist and anti-racist**. We need to build chatbots thoughtfully, and not connect machine learning until after we have content designed that we want the AI to learn from. As with so many things, *what* a chatbot does is only half the story. It may “answer questions” &mdash; but what questions, and how? It may “direct people to their next steps” &mdash; but what are the appropriate next steps, and how does the chatbot respond when something goes wrong? In other words, what will make a true impact is *how* the chatbot accomplishes the things it does.

## Best Practices For Engaging Chatbots

If your team is building a chatbot, hopefully you’ve already done a lot of the upfront work.

- You’ve decided that a chatbot is the right solution.
- You’ve identified the technological constraints, such as what system you’ll be using.
- You’re looking into what capabilities will be available in that system, such as autocorrect or a built-in thesaurus of synonyms.

Now is when some executives say “plug it in and make it work!” and you must say “plug what in?!” As noted, your chatbot is not just an algorithm, and you have some content to design. It’s time to build the content for your chatbot. Let’s explore five best practices to make your chatbot humanesque:

1. Define your actions.
2. Separate your response types.
3. Embrace your robot-self.
4. Create a tone for each scenario.
5. Design for errors.

### 1. Define Your Actions

Since a chatbot is not a magical solution to all things, you need to **focus your work on specific user flows** that people can accomplish with your chatbot. For example, let’s say you are building a chatbot for a company like FedEx or USPS, you may list out sample user flows like “track a package” and “update mailing address.” That means if an end-user asks the chatbot for help tracking a package, it may respond “what is the tracking number.” But the chabot should know its limitations. Perhaps one of the goals is “build trust.” Therefore if an end-user says “someone committed mail fraud in my name” the chatbot might express condolences and quickly transfer the end-user to a live customer service agent. Because the goal was to “build trust,” the team building the chatbot should recognize that anything involving sensitive information should be handled by a human &mdash; even if there is no technical or legal limitation.

There’s no one right way to go about this. Most organizations have some form of value propositions or design principles, which will help to identify the goal of the chatbot. There are also likely some requirements already defined. Therefore the goal can come from a cursory look at the requirements, and the requirements will become more specific after the goal is defined.

In an [interview with Mike Bunner](https://silvercloudinc.com/blog/franklin-mint-fcu-banking-chatbot), VP, Director of Digital Marketing at [Franklin Mint Federal Credit Union](https://www.fmfcu.org/), Bunner said that without the chatbot, “our call center would be getting 3x the normal amount of calls.” Their goal could be assumed to be “decrease customer service hours.” This connects nicely to their chatbot’s initial prompt, which suggests “popular topics” that it can help with &mdash; likely these popular topics are the most common reasons people call the customer service team. In the same interview Bunner said the bot pulls its content directly from the member support content. Like many organizations, Franklin Mint had lots of helpful content, but had trouble getting people to view it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18b919df-302e-4d80-a2ce-3c1d2dcd30ac/4-designing-voice-chatbot.png" width="800" height="376" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18b919df-302e-4d80-a2ce-3c1d2dcd30ac/4-designing-voice-chatbot.png" sizes="100vw" caption="Franklin Mint’s chatbot helps answer common questions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18b919df-302e-4d80-a2ce-3c1d2dcd30ac/4-designing-voice-chatbot.png'>Large preview</a>)" alt="The Franklin Mint chatbot asking “Hello, how can I help you? Here are our most popular topics: STIMULUS PAYMENTS INFO; Checking and Savings; Mobile Banking App Guide; Home Equity & Mortgages; Auto, Personal, & Student Loans; Digital Wallets - Try it Today!”" >}}

### 2. Separate Your Response Types

When you think of a chatbot you likely think of one of two things:

1. A chatbot that responds to anything an end-user types, picking up on what they want through key words and phrases.
2. A chatbot that follows a series of decision trees, asking the end-user to select from a few options and then bringing them through a user flow.

Chatbots can do one or both of these, and it’s important to know what you’re aiming for. In fact, even if you intend to focus on decision trees, there’s the possibility of a user going off-script. With that in mind, consider how you want the chatbot to respond. If someone says “Help” or “Talk to a human” how will you route them?

As you think through the chatbot’s word associations, remember that **words have context**. When an end-user is editing their profile and they type in “phone number” they likely want to see where to edit their phone number. But if they’ve typed in something the chatbot doesn’t recognize, the chatbot said “I don’t understand” and then the end-user types in “phone number” they may be looking for a customer service line. This is an opportunity for engineering and content strategy to collaborate to create a well-designed and well-built bot.

This sort of thoughtful planning will come across in the end product. Adobe’s chatbot, for example, fails here. It begins by asking the end-user to freetype, but after getting a response the bot asks the end-user to select one of three options. As a user, I’m left wondering why I was asked to type if the bot couldn’t understand a simple keyword like “Adobe products”.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a4b8385-39d9-4e36-98f7-e9d32e557428/1-designing-voice-chatbot.png" width="800" height="515" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a4b8385-39d9-4e36-98f7-e9d32e557428/1-designing-voice-chatbot.png" sizes="100vw" caption="Adobe’s chatbot asks how they can help, but doesn’t recognize keywords. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a4b8385-39d9-4e36-98f7-e9d32e557428/1-designing-voice-chatbot.png'>Large preview</a>)" alt="User free-typing “What are the adobe products” and the Adobe chatbot responding “I want to make sure I understand clearly. Which of these categories best describes your issue? Troubleshoot a product issue; Explore plans and pricing; Something else.”" >}}

### 3. Embrace Your Robot-Self

Once you know what your chatbot can do, it’s time to think about *how* it will do it. First and foremost: don’t pretend that your chatbot is a human. In research with a former client, the client found that over 80% of people were comfortable interacting with a chatbot, and they liked when a chatbot had a name and personality. But those same people quickly lost faith in the bot and the organization when the chatbot pretended to be human.

One conversation with a client revolved around whether people would speak with a chatbot if they knew speaking to a human was an option. Testing found that yes, they would! In fact, reassuring end-users that a human being is available (as needed) actually increased the comfort they had in speaking to the chatbot.

The team at Hopelab had similar results when they built [Vivibot, a chatbot for teens with cancer](https://hopelab.org/product/vivibot/). Teens and young adults would often avoid confiding in their parents or health professionals. But Hopelab found that a chatbot removed some barriers. In their [peer-reviewed randomized controlled study](https://www.prnewswire.com/news-releases/hopelabs-vivibot-the-first-chatbot-designed-for-young-adult-cancer-survivors-can-improve-mental-well-being-of-users-300951573.html) they were able to show that Vivibot not only provided valuable emotional support, but also improved anxiety.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad95e71d-744d-4456-b0da-917a3e0af11a/6-designing-voice-chatbot.png" width="800" height="427" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad95e71d-744d-4456-b0da-917a3e0af11a/6-designing-voice-chatbot.png" sizes="100vw" caption="Vivibot first explains that she is a chatbot, but still uses emojis and exclamation points as part of her personality. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad95e71d-744d-4456-b0da-917a3e0af11a/6-designing-voice-chatbot.png'>Large preview</a>)" alt="“Vivibot (that’s me) is a chatbot created for young people dealing with life beyond cancer. If that doesn’t sound like you, that’s okay - we can still chat! Although I’ve been designed by real people, I’m not a real person or a substitute for getting help from a therapist or other health care professional. I’m not an emergency or crisis service. If you’re hurt or involved in a potentially life-threatening situation, please call 911. Last thing: while I won’t understand what you type, I will do my best to help you learn some new skills (and meet some of my friends along the way). That’s enough from me. Let’s start chatting!”" >}}

Vivibot is an interesting chatbot example for several reasons. First, the bot is not intended for one-off solutions, but rather as an ongoing emotional support tool. This means the bot needed to have a variety of responses, so as to avoid sounding repetitive. Second, as a health-related bot, Vivibot needed to address sensitive subjects. She needed to be as transparent as possible, never defaulting to a generic “sounds good” for fear of alienating the people who rely on her when they don’t feel comfortable confiding in humans.

Imagine if Vivibot came across as insensitive? Emily Cummins, a writer with a piece on [The Worst Chatbot Fails](https://www.netomi.com/the-worst-chatbot-fails-and-how-to-avoid-them), shows an example where UX Magazine’s “UX Bear” asks “how would you describe the term *bot* to your grandma?” Emily responded “my grandma is dead,” and got back a thumbs up. This is a slightly confusing response from UX Bear, but would be potentially devastating from Vivibot.

In the near future we may see more states pass laws about bots pretending to be human, [as California has](https://www.pcmag.com/news/california-law-bans-bots-from-pretending-to-be-human). While it may seem unnecessary for the Chat Bears of the world, it’s clearly important for influential or sensitive topics, be they politics or healthcare.

{{% ad-panel-leaderboard %}}

### 4. Create A Tone For Each Scenario

When content strategists create a “voice and tone”, the two are different things. A **voice** is like a brand personality. It identifies how a company sounds, no matter what. The **tone**, however, will differ depending on the situation. The voice may be “friendly” but friendly sounds different in an error message than in a success message.

A chatbot should have a different voice from a company. It can say things like “oh no!” or “I’m happy for you.” when your company can’t. To that end, the first step of creating a chatbot voice is to develop a list of words your chatbot says. It’s important that a chatbot respond to the end-user, to let them know they’ve been heard. That means chatbots spend a lot of time saying things like “Got it” or “I understand” and you need to know what those agreement tokens sound like. Does your chatbot say “yes” or “yeah” or both? “Ok” or “okay”? “Great” or “I understand”? Parameters will help your chatbot sound consistent, such that the chatbot doesn’t respond “okie smokie” and then later “I appreciate your time,” but you’ll also need enough agreement tokens that your chatbot doesn’t sound overly robotic.

In Domino’s chatbot, the bot alternates agreement tokens like “great” and “got it”, but when it can’t understand the response it has no error token. The redundancy of the question “What city is that address in” (with no reference to the fact that it hadn’t understood my response) initially made me think the bot was broken.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2902a879-b56b-4add-b780-54477d5ac369/designing-voice-chatbot-8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2902a879-b56b-4add-b780-54477d5ac369/designing-voice-chatbot-8.png" width="800" height="339" sizes="100vw" caption="Dominos repeats the same question over and over if it doesn’t understand the answer. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2902a879-b56b-4add-b780-54477d5ac369/designing-voice-chatbot-8.png'>Large preview</a>)" alt="Chatbot [Dom]: Got it! Is this being delivered to a house, or to an apartment? Me: House. Dom:Great. What’s your street address? Me: 123 sesame street. Dom: What’s the zip code there? Me: 10010. Dom: What city is that address in? Me: New York. Dom: What city is that address in? Me: NY. Dom: What city is that address in?" >}}

### 5. Design For Errors

Chatbots, like other UIs, only have **one chance to make a first impression**. If the experience isn’t smooth and simple, people won’t return. With that in mind, a chatbot needs to have well written error messages. An error message from a chatbot may be as simple as saying “I don’t understand. Can you tell me again what you want?”, but it can also do far more.

For example, if your chatbot is an MVP, your error message may say something like “I can’t help you with that [feature] today, but ask me again in a few weeks.” Alternatively, if the end-user is asking for something the chatbot will never offer, suggest an alternative like “you can call customer service for help with that.”

Assuming you allow for free typing, there will also be the risk of someone typing a word or phrase your chatbot doesn’t understand. In that case, your chatbot may ask for clarification, or even say “I don’t understand”. But make sure you don’t leave your end-user in a loop! If the chatbot can’t understand after two or three tries, offer to put the end-user in touch with a human.

That said, error planning goes far beyond a simple “I don’t understand” or “I can’t help with that”. A well-built chatbot considers how end-users view the tasks they want to complete. Take for example a payroll system, which might use a chatbot to help employees check on their upcoming paychecks, tax deductions, and other requested pre-tax deductions. In a system like this, the chatbot is likely able to answer questions such as:

- When is my next paycheck scheduled to be sent to me?
- I want to set up direct deposit.
- When can I change my 401k deductions?

It’s possible the payroll system is connected to some of the employee’s benefits &mdash; for example, it may have a flow built to allow the employee to change deductions. But the payroll chatbot team should be aware that employees may come to them with related questions and issues, such as:

- What benefits do I have available if I go on sick leave?
- I need to change my 401k allocations.
- I didn’t receive my last paycheck.

It’s unlikely that the payroll system is also the benefits system. But the chatbot team needs to know that employees don’t think in terms of capabilities. They think in terms of needs. “I need to take care of my 401k” may mean going to one system to set up the deductions, and another system to change the allocations. If the chatbot says nothing but “I can’t help with that” in response, then the chatbot has failed. Our hypothetical payroll system could instead build goodwill by explaining the system to a member and recommending they speak to their HR representative.

[Webflow’s Customer Support chatbot](https://university.webflow.com/support) does an excellent job of not only defining what it can do, but telling the user upfront: “[I]f I'm unable to solve a problem for you, a member of our Support team will get back to you by email. Note: We don't provide support by phone or live chat at the moment, as we've found it most impactful to help you via email.” You may not think of this as an error message, because it’s really about solving the problem before it ever becomes an error.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07aaab2a-1e8e-4bb1-9e29-ee292cc04c64/8-designing-voice-chatbot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07aaab2a-1e8e-4bb1-9e29-ee292cc04c64/8-designing-voice-chatbot.png" width="800" height="571" sizes="100vw" caption="Webflow’s chatbot clarifies immediately that if the bot gets stuck, the support team will respond via email. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07aaab2a-1e8e-4bb1-9e29-ee292cc04c64/8-designing-voice-chatbot.png'>Large preview</a>)" alt="Hello! I'm the Webflow Support Assistant — if I'm unable to solve a problem for you, a member of our Support team will get back to you by email. Note: We don't provide support by phone or live chat at the moment, as we've found it most impactful to help you via email." >}}

Internally, this means the team should define user flows from the end-user’s perspective, not just from the technical standpoint of what is possible. If Webflow had only considered things from their own perspective, they wouldn’t have thought to clarify what they *don’t* do. They would merely have solved the problems they could, and potentially left users wondering why (for example) they couldn’t find a phone number to call.

{{% ad-panel-leaderboard %}}

## Bringing Humanity To Your Chatbot

Of course a chatbot is not a person. But it’s also not a second-choice option to a person. A chatbot can help people easily get answers to their questions, it can help them connect when they’re feeling vulnerable, and it can simplify complex processes. It is, like so many tools, a perfect solution to many potential problems.

As the creators of these chatbots, that means we have an important mission! We must create appropriate responses, humanesque tones, and helpful user flows. We must write content to respond to people in different moods, and with diverse needs &mdash; anticipating their next steps and guiding them appropriately. Most of all, we must create transparent and trustworthy bots, so that the people interacting with them can trust the information they provide.

Just remember: Define your actions, so that your chatbot accomplishes a business goal and a user need. Build out a script for your chatbot and decide if your chatbot will respond to off-script requests. Embrace your robot self and *never* pretend to be a human. Create a tone for each scenario. And lastly, make sure your chatbot can handle errors smoothly.

Your chatbot is a program, not a human. Still, **a well-designed program can bring happiness and ease to your audience**! With these five steps,your chatbot will be capable of a near-human connection with your end-user. Now it’s your turn: follow these best practices and let us know how your audience responds to your bot.

{{< signature "cc, vf, yk, il" >}}
