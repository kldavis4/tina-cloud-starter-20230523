---
title: 'The More You Fail, The Greater Your Success: A User-Centered Design Case Study'
slug: the-more-you-fail-the-greater-your-success
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baa48522-ad1b-4e92-b3c1-6d4cb64f5374/05-build-opt-small.jpg
date: 2014-12-02T18:00:38.000Z
author: mattreamer
description: >-
  This article will be an **introdrction to the human-centered design process**.
  I’ll tell a personal story in which I built a challenged family member a
  device to help them communicate more efficient and effortlessly and I’ll share
  lessons I learned from the failures and successes along the way.
categories:
  - UX
  - Communication
  - UX
  - Case Studies
  - Interaction Design
---
Jeffrey Zeldman once said, “Usability is like love. You have to care, you have to listen, and you have to be willing to change. You’ll make mistakes along the way, but that’s where growth and forgiveness come in.” If you think of design as a tool it becomes a much more powerful skill set and by putting the user first you can transform your product into something truly remarkable.

This article will be an introduction to the human-centered design process. I’ll tell a personal story in which I built a challenged family member a device to help them communicate more efficient and effortlessly and I’ll share lessons I learned from the failures and successes along the way.</p>

## The Learning

Dustin is my 30-year-old brother. He was born with little to no oxygen in his body and underwent two open-heart surgeries before his 10th birthday. He is also autistic. As a result of those health issues combined with the autism, he is not able to speak. Many wrongly confuse his silence with a lack of knowledge and understanding. But Dustin knows what’s going on. He probably has more thoughts than you and me; he just can’t express them fully.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca5f9b57-3d15-4e02-8574-208a460506b2/01-my-brother-opt.jpg" alt="My brother and me when we were children." width="500" height="323" /><figcaption>My brother and me when we were children. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>)</figcaption></figure>

{{% feature-panel %}}

Growing up, I have always seen how much Dustin has struggled to communicate a simple word to anyone in our family, much less a random stranger. He makes only a few sounds, and only one person on Earth mildly understands what he’s trying to say — a magnificent woman I call Mom. I can only imagine the way he feels when she is not at his side to speak for him. So, I’ve always said that if a genie were to grant me three wishes, I would need just one: to make my brother “normal.” But, as time has passed and Dustin and I have gotten older, I have come to realize that “normal” does not exist, and if it does, then maybe he is a bit more normal than me.

Fast forward 20 years, to my last year of graduate school. I was six months away from moving across the country. With this knowledge I had, I wanted to design a tool that would help my brother to communicate his needs and that would relieve a little stress on my family as a whole.

Using my skills as an experience designer and having worked in web development, I planned to build Dustin a web app that would live on an iPad. In its simplest form, he would be able to tap the picture associated with his immediate need, and that tap gesture would trigger an audio file to speak the need to my parents. Simple, right? Everything was set, so I began sketching away and looking for inspiration to get started.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49d16c81-22ba-4a59-9be5-209cd0e9da2e/02-sketches-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5cf66f2-3b14-4b0a-877a-8da2faee7630/02-sketches-opt-small.jpg" alt="A couple of pages of the early sketch concepts for this tool." width="500" height="344" /></a><figcaption>A couple of pages of the early sketch concepts for this tool. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49d16c81-22ba-4a59-9be5-209cd0e9da2e/02-sketches-opt.jpg">View large version</a>)</figcaption></figure>

Little did I know that I hadn’t been thinking about how Dustin would actually utilize the functionality of the app. One night at my parents’ house for dinner, the idea popped into my head. Dustin grabbed my phone and started tapping randomly. As I watched him continue to struggle with the phone, I realized that I had already failed. My idea was already dead. That was when I grasped the true importance of a discovery phase in any project.</p>

### Lesson 1: Know the End User Inside Out

Observe, research, test, repeat. A “day in the life” of your <a>end user persona</a> is a helpful exercise to do in the research or discovery phase. With persona mapping, you — the designer — choose one representative user and design to their daily needs. The user may be fictitious or real, but most of us use a fictitious persona who brings together attributes from a larger segment. Mapping out this persona’s daily routine during a 24-hour period will help us to pinpoint holes in their routine where your product would be most useful to them, and possibly also help us to find ways to improve other aspects of their daily life in the process. In web design, a day-in-the-life exercise can be beneficial when the budget or time for focus groups is limited. It provides opportunities for key findings on a product’s structure. Jeffrey Rubin identifies [a few usability objectives](https://www.w3.org/WAI/redesign/ucd):

*   **Usefulness**
    product enables user to achieve their goals — the tasks that it was designed to carry out and/or wants needs of user.
*   **Effectiveness (ease of use)**
    quantitatively measured by speed of performance or error rate and is tied to a percentage of users.
*   **Learnability**
    user’s ability to operate the system to some defined level of competence after some predetermined period of training. Also, refers to ability for infrequent users to relearn the system.
*   **Attitude (likeability)**
    user’s perceptions, feelings and opinions of the product, usually captured through both written and oral communication.</p>

<figure><img loading="lazy" decoding="async"  property="image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e9f6ebf-cf4f-4921-b22c-998a336fe37a/03-highscore-house-daily-routine-opt.jpg" alt="You need to understand your ideal user base, what makes them tick, their motivations, fears, influencers, etc." width="500" height="373" /><figcaption>You need to understand your ideal user base, what makes them tick, their motivations, fears, influencers, etc. (Image credit: <a href="https://www.instigatorblog.com/day-in-the-life/2011/04/26/">Ben Yoskovitz</a>)</figcaption></figure>

### Lesson 2: The Pivot

For a company to succeed, it should frequently test its product-related predictions or prototypes with users. This will help to validate or contradict any assumptions made during the previous design phases. In subsequent design phases, we use the insights and learning gathered during user testing to pivot the company’s business model or the product’s utility and features.

Pivoting is scary, but don’t be afraid. More often than not, when all of your research and testing is leaning towards it, pivoting the product is the best thing to do. All of the hard work you’ve put into the first round might seem like a waste at first, but think of it as an investment into a better and more user-centric product, one that will now better cater to its consumers and that will prolong the product’s life cycle.

Luckily, I was able to reign in my excitement and focus on the user quickly. As I did more research on autism spectrum disorder (ASD), I recognized behaviors in Dustin that I had always seen but never understood. The majority of people with ASD have difficulty processing everyday sensory information such as sounds, touch, sights and smells. This is usually called sensory integration difficulties, or sensory sensitivity. As the [National Autistic Society of the UK explains](https://www.autism.org.uk/sensory), it can profoundly affect a person’s life.

With that in mind, I began to observe Dustin and track his behaviors. I interviewed his closest caregivers at home, showed him different styles of icons (thanks, [NounProject](https://thenounproject.com/)) and tested colors, palettes and textures. I had to take many variables into consideration. The communication device had to be simple to use, be durable, be visually inviting, use some sort of icon language and have a texture similar to what he is used to in his everyday life. This was important because most people affected by autism prefer order and need a routine schedule.

Something else I had to keep in mind was that Dustin would not be the only user. Communication requires two parties. So, I started to view my mom not as a caregiver, but as a user. This revealed the struggles she has faced and enabled me to compare the needs of both end users and create something that bridges this communication barrier.</p>

<blockquote>
<p>“Dustin and I communicate pretty well, but that’s after 30 years of being together all day, every day. Sometimes it takes a few minutes of Dustin struggling to express what he wants or needs. I get scared and wonder what he would do if something happened to me? The way we communicate is strange and no one, not even your dad, gets it.”</p>
<p>&ndash; Missy Reamer (Mom)</p>
</blockquote>

Another factor was thrown my way. My mom mentioned that she was worried for the day when they might not be together, and even worried about the simple pleasure of a vacation. The device had to not only be able to communicate to my mom in a timely manner, but also be interchangeable for other caregivers upon request. To achieve this, I decided to use SMS or, as the general public calls it, text messaging. I had worked on previous projects using SMS, so I was familiar with programming it onto the Arduino board.

You might be wondering what an Arduino board is? It is a small microcontroller whose hardware is an open-sourced board designed around an 8-bit Atmel AVR microcontroller or a 32-bit Atmel ARM. In other words, these various boards serve different purposes but all generally enable you to build interactive objects that serve various functions through APIs and Arduino libraries.

Although there are multiple ways to supply the 5 volts needed to power an Arduino, the best method for my purpose was to connect it to a computer via USB, so that anyone with minimal computer skills would be able to easily plug it in and simply change or add a phone number connected to the device for the day, week, etc. Once I had completed the programming, it would become a simple plug-and-play device.

Now that I knew how the device would work, it was time to move on to the look and feel of the exterior. The surface of the device was blue, and the shell for the electronics was already made. I took it to my parents’ home to show it off to everyone, and Dustin seemed really uninterested and kind of turned off. Frustration set in. Come on, work with me here, Dustin!

Then, another pivotal moment. I noticed Dustin standing in front of the mirror staring at himself. Remembering back to our childhood, I know that he had always been drawn to shiny metallic things: the toy guns he used to play with, the micro machine cars that were strewn around the house, his obsession with new cars, the bouncy new balls he got out of the 25-cent machine. I was onto something. I showed him the metal top of a [project enclosure from RadioShack](https://www.radioshack.com/product/index.jsp?productId=2062285), and he loved it.

A metallic surface was the perfect answer because it is smooth to the touch and the all-white external shell is soft on his eyes. This was another lesson. If your product is changing as a result of user observation or feedback, then it’s changing for the better.</p>

### Lesson 3: Keep Asking “Why”

The more you ask yourself “Why” while designing an experience, the more successful it will be. “Why” is a powerful question that I’ve gotten into the habit of asking myself when designing experiences. “Why is this here?” “Why should it animate like this?” “Why does the end user care?” Why, why, why. Always have a reason for the design decisions you make.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96611ff4-d6f8-4dac-b051-448a872417a7/04-early-prototype-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44fb2f62-0367-4660-b125-e5a39520241f/04-early-prototype-opt-small.jpg" alt="This is an early prototype I worked on, until I realized it was a failure. Failure is a good thing, though." width="500" height="500" /></a><figcaption>This is an early prototype I worked on, until I realized it was a failure. Failure is a good thing, though. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96611ff4-d6f8-4dac-b051-448a872417a7/04-early-prototype-opt.jpg">View large version</a>)</figcaption></figure>

## The Build

At this point, the product had gone through quite an evolution. It started as a web app concept that requires the physical presence of a caregiver, and it evolved into a device with push buttons that sends text messages to the recipient in real time. Using an [Arduino Yun](https://arduino.cc/en/Main/ArduinoBoardYun?from=Products.ArduinoYUN) and the [Temboo library](https://www.temboo.com/arduino/yun/getting-started) allowed me to get free SMS service through a Wi-Fi connection. With the exterior shell for the electronics in place, it was time to roll out functionality for the SMS delivery. Sending an SMS requires some sort of trigger or button.

The choice of arcade buttons was on purpose because their large size would minimize errors and incorrect button hits. Having a tactility that is familiar to Dustin and comfortable for him was also important. Because he has always had a passion for and deep understanding of video games, the arcade-style buttons make perfect sense. On top of each button is an icon representing the six particular needs in his day-to-day life that stood out for my mom in my interview with her.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63700c19-8f3c-461a-9546-d8505667fabc/05-build-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baa48522-ad1b-4e92-b3c1-6d4cb64f5374/05-build-opt-small.jpg" alt="The build as it progressed and became powered by an Arduino Yun." width="500" height="281" /></a><figcaption>The build as it progressed and became powered by an Arduino Yun. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63700c19-8f3c-461a-9546-d8505667fabc/05-build-opt.jpg">View large version</a>)</figcaption></figure>

I had to keep in mind some other important factors, too. The product had to have all of the following:

*   a visual indication that a message was successfully sent,
*   a modular design that is easily mountable and moveable by my parents,
*   a push button that has an audible sound to signify its hit state,
*   5-volt low-energy consumption.</p>

<figure><a href="https://instagram.com/p/lFkeu-DnfS/?modal=true"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ef37f68-9606-4589-974c-baa697d044a4/instagram.jpg" alt="An early demo of the communication device I built for my brother." width="500" height="466" /></a><figcaption>An early demo of the communication device I built for my brother. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://instagram.com/p/lFkeu-DnfS/?modal=true">View video</a>)</figcaption></figure>

The requirements above are necessary, all for different reasons. Because it is a physical device with no screens, I had to create the simplest way to let Dustin know that an SMS has gone through successfully. This is where the red and green LED lights come in, as well as the recognizable sound that the arcade buttons trigger in their hit states. Still thinking of my parents as secondary users, I had to make sure that the device was low on energy consumption and easy to move because Dustin is not always in one place. In this process, known as future-proofing, the creator thinks of all possible scenarios in which the device might be used in future.</p>

### Lesson 4: The Future

If you always think five years ahead (or more), your iteration will be golden. Users of your product are forever evolving, as are their needs. If a product doesn’t iterate and evolve, then its relevance will fade away. My observation of the user (Dustin) operating this device over the next five years will be the basis for future iteration.

Learn from Blockbuster. A big brand let a little startup (heard of Netflix?) creep in their backyard, pitch a tent and camp out. Soon enough, that tent transformed into a shed, which then transformed into a guest house, and eventually the startup demolished the existing house and constructed its own — all this because Blockbuster did not evolve its product. Sorry, Blockbuster, I used to love you.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b90820-07ed-4bf1-9568-bbf2bdf0caaa/06-build-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f7fdbaa-6bbc-46df-b33c-c4b8360a9c10/06-build-opt-small.jpg" alt="The inside and outside of the shell prior to soldering." width="500" height="213" /></a><figcaption>The inside and outside of the shell prior to soldering. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b90820-07ed-4bf1-9568-bbf2bdf0caaa/06-build-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/599b5d02-dba2-4c1f-a56b-1d080667ec64/07-build-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e5e268-1dbe-4dcc-99f8-4f13ff81540c/07-build-opt-small.jpg" alt="The build as it progressed and became powered by an Arduino Yun." width="500" height="333" /></a><figcaption>The build as it progressed and became powered by an Arduino Yun. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/599b5d02-dba2-4c1f-a56b-1d080667ec64/07-build-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeca7434-0031-4dda-a486-da6501e86acf/08-build-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b8ee39c-9364-4453-8cc5-bab5e7bd46b1/08-build-opt-small.jpg" alt="The choice of arcade buttons was due to their large size, which minimizes error and incorrect button hits." width="500" height="333" /></a><figcaption>The choice of arcade buttons was due to their large size, which minimizes error and incorrect button hits. Having a tactility that Dustin is familiar and comfortable with was also important, and playing video games fills his spare time. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeca7434-0031-4dda-a486-da6501e86acf/08-build-opt.jpg">View large version</a>)</figcaption></figure>

Back to Dustin. The way the product stands now is not how it will remain, for this is a forever evolving experience and I plan to continue to further it. Future plans are to build a back-end CMS where, after my brother and parents have learned a mode of communication for certain needs together, they can swap the meanings and icons of particular buttons. If we do not have an icon that represents a particular need, we will quickly create an icon for it. This way, the library of icons will grow in an efficient and user-centered way. For a more personal experience, the user could upload a photo into a graphical OLED button for quick communication. Refinement of the construction of the device itself is also planned.

This device was designed and built just for my brother, but variations could help thousands of people who are challenged by speech or motor-function disabilities. In a world where we can customize our Nike’s for only $100, why does it cost upwards of a thousand dollars for someone with a life-altering disability to have what many fortunate people are born with, speech?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00b34843-8d48-4053-916f-378d31eb7abe/09-in-progress-web-site-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f2a85c4-f1eb-401e-ad84-907159da0379/09-in-progress-web-site-opt-small.jpg" alt="The website that is being built will hopefully house the future of this helpful and cheap product." width="500" height="236" /></a><figcaption>The website that is being built will hopefully house the future of this helpful and cheap product. (Image credit: <a href="https://iamtheream.io/dustinsWords.html">Matt Reamer</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00b34843-8d48-4053-916f-378d31eb7abe/09-in-progress-web-site-opt.png">View large version</a>)</figcaption></figure>

I think variations of this device could help many others. I anticipate creating dozens of use cases and design icons for future users to load onto their devices when connected via Bluetooth, micro-USB or Wi-Fi.</p>

{{< vimeo id="96746468" caption="<a href='https://vimeo.com/96746468'>Dustin’s SMS device</a>" >}}

## Conclusion

In designing this experience for Dustin, I’ve learned much more about him than I had previously known. Putting user-centered design truly into practice takes research, followed by iteration and testing. Iteration is the key to making any product, experience or service useful. But that experience means little without love: love for what you do and respect for who you are doing it for. I hope that this has inspired or at least has gotten you thinking about how you can push your skills to help the people around you, as well as shed some light on some basic principles of user experience design that are too often overlooked.

The source code and schematics for this project are available on [Github](https://github.com/iamtheream/brothersSmsDevice). Feel free to interpret this project in your own way to help someone you know.

To conclude, one of my favorite quotes, from author James Jesse Garrett:

<blockquote>
“User-centered design means understanding what your users need, how they think, and how they behave &mdash; and incorporating that understanding into every aspect of your process.”
</blockquote>

### Further resources

*   “[Ergonomics of human-system interaction: Human-centred design for interactive systems](https://www.iso.org/iso/catalogue_detail.htm?csnumber=52075),” ISO
    If you're interested in reading about this subject as a whole.

{{< signature "cc, al, ml" >}}

