---
title: 'iPhone Apps Design Mistakes: Disregard Of Context'
slug: iphone-apps-design-mistakes-disregard-of-context
image: null
date: 2009-11-15T08:28:25.000Z
author: alex-komarov
description: >-
  The **iPhone** will always be part of a much bigger picture. How well you address human and environmental factors will greatly determine the success of your product. All too often, iPhone developers create products in isolation from their customers. In order to create really appealing applications, developers must stop focusing only on the mechanisms of the apps. Zoom out: understand the person using the application, as well as the complex environmental factors surrounding that person.
categories:
  - Mobile
  - Apps
  - iOS
  - iPhone
  - Design Patterns
---

To better understand the context of these design challenges, we’ll highlight several levels of human and environmental factors.

## Level 1: You Are Here. To Create An App That Customers Love, Zoom Out

**Level 1:** The app itself.  
This is how many developers view their apps. As a developer, you have a vision of what your product should look like and why customers will turn their attention to it. However, if you observe your product so closely, you may put it in the wrong context and design it for the wrong purposes and for the wrong users. This is why you need to zoom out.

![My App](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3cade88-0e7a-409e-98e9-9c9b51113898/myapp.jpg)

{{% feature-panel %}}

**Level 2:** A _person_ is using this app.  
That person has specific goals and challenges. In the section below we’ll start by exploring some of the most prominent -- and most ignored -- human factors pertaining to the iPhone. We'll discuss basic physical ergonomics, visual limitations and common design mistakes.

![A person using the app](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bf40790-72a9-41a1-a193-0a2f591e857f/person.jpg)

**Level 3:** That person is using this app in a specific environment.  
Step back and you'll see that the app is a part of a complex social environment. It plays but a relatively small role in communication between people and helping people accomplish bigger goals. This is where the social components comes into play: networking, community, social-driven websites and applications and many other things create the environment -- or the context — in which the application will be used.

![Crowd](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/408af9dd-20c4-4596-b2a5-c981e5c11744/crowd.jpg)

**Level 4:** The environment is part of a greater culture.  
Your ability to address the unique needs of different cultures will affect the success of your product. Ignoring them is too expensive, especially if your app sells worldwide. Here it is important to understand that the environment is a part of global networking. You need to be aware of cultural differences, traditions and metaphors in order to create an application that will not only gain popularity in certain local circles, but will also have a global success.

![Globe](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8b464a-2d42-4a5d-80c7-b9d9f0b17010/globe.jpg)

## Level 2: Understand The Person's Needs And Limitations

![Woman using app](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bd3d1f6-460e-4dac-a5f4-d942f6a3a867/person2.jpg)

"Measure twice and cut once": an effective strategy indeed. For you, the iPhone app developer, this means that you have to step back and answer these questions before you start coding:

*   Who will be using your application?
*   What are the capabilities of that person?
*   What are the limitations of that person?

Answering these questions will broaden your perspective and prepare you to address your customer’s needs. A whole Human Factors profession is dedicated to just that.</p>

### Basic Physical Ergonomics

Here are a couple of the most important physical-, cognitive- and ergonomic-related truths about the iPhone.

**1\. Our fingers are not mouse pointers.**  
Remember this property of our fingertips: their surface area is not equal to one pixel. In many applications, tappable objects are way too small, making the interface frustrating to use. Here's one example: in iFitness, different muscle groups are indicated with red pins. Tapping a pin brings up the name of that muscle. And if you tap the name, you get a list of exercises that develop that muscle.

![iFitness](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d325a9a-e521-450e-bd37-c55bf82c5ead/ifitness2.jpg)

The pins are twice as small as those used in the Google Maps app. Tapping the pin you want is very hard, because the surface of your fingertip covers an area of three or more pins. You end up tapping repeatedly on the area, enabling random pins, wishing you could sharpen your finger. After more than a few tries, you get lucky and hit the right one.

![Pins in iFitness](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90faa1a7-16f1-476a-bb82-8f85902822e8/ifitness3d.png)  
_Which of these pins will be activated when you tap on it?_

Here are some ways to solve these ergonomic challenges:

1.  Make buttons and other tappable objects bigger.
2.  If making a button bigger is impossible, then enlarge the clickable area to be bigger then the button itself.
3.  Reduce the number of options on each screen, and make the selection process sequential (e.g. Arm Muscles → Biceps).
4.  Implement multi-touch gestures within the interface. For example, selecting a muscle group in iFitness would be made easier by introducing a two-finger zoom feature.

**2\. We’re not superheroes, unfortunately.**  
App designers need to take vision limitations into account. Mobile phones tend to be used in places with worse lighting conditions than computers. Think about those people who will be using your app on a bumpy bus or train or walking down a sunny street. Even if the technology is useful and perfectly executed, people will be reluctant to use the app if they find it hard to see what's going on. Here are a few examples of potentially useful apps that do not account for vision limitations.

_TweetDeck_

![Tweet Deck](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142fb25d-8c22-4918-96ca-8cd253ece61f/tweetdeck.png)

_Fish-tycoon_

![Fish-tycoon](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c756e3-8ef7-406a-8675-cb6d90abba05/fish-tycoon.jpg)

Here are some ways to avoid these mistakes:

1.  Choose only the elements that are absolutely necessary. Make them bigger, and get rid of everything else. If needed, create additional screens with fewer options.
2.  Remember that pixel dimensions on the iPhone are smaller than those on your computer screen. So, screenshots viewed on your computer's iPhone emulator look larger than they would on the iPhone itself, even though the resolution is the same.

![iPhone vs. Simulator](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48dc2428-24a0-4ef7-bfc0-0700b4566d42/iphone-vs-simulator-dpi.jpg)  
_The author holds an iPhone (163 ppi) in front of Apple Cinema's 30-inch display (~100 ppi). Your iPhone screen layout may look fine on a computer emulator, but don’t be fooled: it will appear much smaller on the iPhone because of its smaller pixel dimensions._

## Level 3: Understand The Challenges Specific To The User’s Environment

![Crowd](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/408af9dd-20c4-4596-b2a5-c981e5c11744/crowd.jpg)

### Goals and Environment

**Your app will usually play a relatively small role in helping the user achieve a bigger goal.** The better you understand what goals people have and what they need to achieve them, the better you can design your app to satisfy those needs. Mobile phones are often used in loud, distracting environments. A simple stroll through town brings plenty of noisy distractions (cars, dogs, mail carriers, etc.). Consider the following examples. Which voice memo app would do a better job?

<table width="50%" border="0">
  <tr>
    <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d2028c7-3af9-491e-8c0c-f1f665309578/apple-voice-memos.png" width="320" height="480" alt="Apple Voice Memos" /></td>
    <td>&nbsp;</td>
    <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d27c5177-b97a-4c8e-9a56-2ef429392114/italk.png" width="320" height="480" alt="iTalk" /></td>
  </tr>
  <tr>
    <td align="center"><strong>Apple Voice Memos</strong></td>
    <td><strong>vs.</strong></td>
    <td align="center"><strong>iTalk</strong></td>
  </tr>
</table>

Although Apple Voice Memos looks nice, iTalk addresses the average user's goals and environment much better. Think about it: why would someone prefer to record a voice memo over writing a note? The audio format has fewer advantages than simple text. You can’t scan, edit or enhance audio files as easily as you can text. In most scenarios, text is a much more convenient format in which to exchange information.

So, **why** and, more importantly, **when** would people use voice memos? When they are not able to type. The most common time is probably while driving.

According to the [New York Times](https://www.nytimes.com/2009/07/28/technology/28texting.html?pagewanted=1&_r=1)' summary of the Virginia Tech Transportation Institute's findings, drivers who text have a 23-times greater risk of a collision than drivers who don’t text. Which application would be easier to use in this case? The one with the big shiny mic and the record button that is small and hard to reach (especially for right-handed people)? Or the one with the red record button half the size of the screen? Certainly the latter.

Confirming for the user that the recorder is activated is important, too. Which interface communicates the device's status more clearly? Where do you tap when you’re done?

  <table width="50%" border="0">
  <tr>
    <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d6c8ca5-c7c0-48b2-a3ce-a6c34c763c2c/voice-memos-active.jpg" width="320" height="480" alt="Voice Memos Active" /></td>
    <td>&nbsp;</td>
    <td><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62822bbe-8c50-4ae4-b88c-acca0119c475/italk-active.jpg" width="320" height="480" alt="iTalk active" /></td>
  </tr>
  <tr>
    <td align="center"><strong>Apple Voice Memos</strong></td>
    <td><strong>vs.</strong></td>
    <td align="center"><strong>iTalk</strong></td>
  </tr>
</table> 

Based on which design works better overall, iTalk wins. Apple Voice Memo looks great when you're checking it out on a friend's phone but performs poorly in a real-world context.</p>

### Mobile Phones, Networking and Community

The mobile phone is, without a doubt, a social tool. The greater the number of people involved, the more engaging the experience is. Think about it: if you were the only one with a phone, it wouldn’t be very useful. YouTube, Facebook and Twitter are driven by the understanding that we are social beings -- we want to share! Imagine how dramatically designs that foster greater social interaction could change the mobile world.

With the seemingly endless ways to capture and share information, many people feel overwhelmed with information. To help them cope, designers must exploit the iPhone's platform to make their applications as efficient as possible. Here are some inspiring examples:

_Bump_

![bump](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a45fc09-c13c-48c2-807e-466b0acba0aa/bump.jpg)

"Bump makes swapping contact information and photos as simple as bumping two phones together. No typing, no searching a list for the right person, no mistakes." (iTunes Store description)

_Mover_

![Mover App](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00063a9c-d516-4873-a2f6-41fabe65b023/mover-app.jpg)

"Ever wished you could send something to the iPhone right next to you? Do it with style with Mover."

<em>Loopt</em>
![Loopt](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f303e92-0e2c-46ba-ac3b-2664ba5d40d8/ipodtouch-map-0.jpg)

"Loopt transforms your mobile phone into a social compass to discover and navigate the world around you. Use Loopt to see who's around, what to do, and where to go."

How Loopt works (video):

## Level 4: The Environment Is Part Of A Greater Culture.

![Globe](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8b464a-2d42-4a5d-80c7-b9d9f0b17010/globe.jpg)

Your ability to address the unique needs of different cultures will affect the success of your product. Ignoring them is too expensive, especially if your app sells worldwide. Design should adapt to regional challenges. Jacob Nielsen, a leading usability expert, gives us an illustration of this:

<blockquote><p>
“In Sweden, the Automatic Teller Machines have very large buttons. I hadn't noticed this particular design element on previous visits, which have usually been in warmer months. In 1996 I was in Stockholm in February and immediately realized why the ATM buttons are so big: you can press them wearing thick gloves.”
</p></blockquote>

Such insights are gained only by understanding the product in its real-world context. Here is the graphic designer's point of view:

<blockquote><p>
"... Understanding the object in context moves graphic design from a purely formal arena to a social and political one."<br />&mdash;<a href="https://www.hellerbooks.com/docs/books2.html">Steven Heller</a> and Karen Pomeroy in "Design Literacy," Allworth Press, New York, 1997.
</p></blockquote>

More wisdom from Nielsen:

<blockquote><p>
“A system must match the user's cultural characteristics. This goes beyond simply avoiding offensive icons; it must accommodate the way business is conducted and the way people communicate in various countries.”
</p></blockquote>

Apple studied American users and addressed their goals. That's why the iPhone is so popular in US. But it hasn’t succeeded in Japan. The handset is selling so poorly there that they are [giving them away for free](https://www.wired.com/gadgetlab/2009/02/why-the-iphone/).</p>

## Conclusion: Excellence Comes From Hard Work

**Designing a great app isn’t a simple task.** Jacob Nielsen recently asserted that "[the mobile user experience is still miserable](https://www.useit.com/alertbox/mobile-usability.html)." Extracting user insights from testing is a challenge. People have difficulty telling you what they want; they usually only know it when they see it. But developers don't have to tackle user research alone. Interaction designers are trained to find relevant user groups, talk to customers and read between the lines. They understand how real-world context affects an application's design.

It takes a lot of leg work, but your efforts to understand user needs will be rewarded. The forefront of mobile technology is an exciting place to be.</p>

## Related posts

Please consider our related articles:

*   [iPhone design mistakes: Over-Design](https://www.smashingmagazine.com/2009/07/21/iphone-apps-design-mistakes-overblown-visuals/ "iPhone design mistakes: Overdesign")
*   [iPhone App Design Trends](https://www.smashingmagazine.com/2009/10/09/iphone-app-design-trends/)
*   [How to Create Your First iPhone Application](https://www.smashingmagazine.com/2009/08/11/how-to-create-your-first-iphone-application/)

_Special thanks to Larissa Itomlenskis._

{{< signature "al" >}}

