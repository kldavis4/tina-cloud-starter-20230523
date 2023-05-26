---
title: 'Why I Moved From A Square To A Circle Calculator Interface Design'
slug: why-i-moved-from-a-square-to-a-circle-calculator-interface-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55033db3-34dc-4b79-8116-86e36adc7e98/02-iphones-preview-opt.jpg
date: 2016-01-11T20:13:45.000Z
author: cygopinath
summary: >- 
  Usually, Numeric keypad Design is an inversion of the Calculator Layout, but why? Nowadays the users experience most of digital products using gestures, not only buttons. Would numbers positioned clockwise be a better experience? In this article, we invite you to challenge the typical calculator layout and to redesign what could be the future of numbers interactions.
description: >-
  As digital calculators become popular, pressing buttons is’t our only way to interact with numbers anymore. We use gestures, so what would be the most ergonomic arrangement for human fingertips?
categories:
  - Mobile
  - Interfaces
  - Interaction Design
---
They’re probably the most familiar interfaces on the planet: the **numeric keypads on our mobile phones and calculators**. Yet very few notice that the keypads’ design has remained unchanged for nearly half a century in the face of evolving global design norms and conventions. Even fewer users notice another startling design feature: the phone’s keypad is the inverted version of the calculator’s.

This article explores the roots of this disparity and proposes a better solution. We will discuss how to simplify and adapt a traditional numeric interface to a minimalist design norm by taking advantage of modern touch&ndash;driven modes of human&ndash;mobile interaction. We'll also tackle the design logic behind developing a new interface for the basic calculator.  

Look at the two images below. Does anything strike you?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0fbedb4-aee0-4d82-8a41-2490d523a38b/01-two-numpads-preview-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0fbedb4-aee0-4d82-8a41-2490d523a38b/01-two-numpads-preview-opt.jpg" width="384" height="293" alt="calculator interface and keypad interface side by side" /></a>
<figcaption>Most users do not even notice that the keypads of the calculator and phone are inversions of each other. </figcaption></figure>

Did you notice that the **two keyboards are flipped opposites of each other**? Though both keypads have zero at the bottom, the remaining numbers go from bottom to top on the calculator, and top to bottom on the phone.

I was intrigued. Surely both designs could not be ergonomically equal? Who decided that the two devices needed different keyboards? Why? And how come no one has challenged the arrangement so far?

More critically, I wondered if either keypad **was even relevant to users** who interact with their apps in ways unimaginable barely ten years ago, using swipes, touches, taps, and force presses. With Apple upending skeuomorphism (the design concept of making software objects resemble their real&ndash;life counterparts) I felt it was time, as a designer and developer, to challenge the numeric keypad design orthodoxy and ask the unasked question: why should a 2015 calculator keypad look, feel and work like an 1960s Casio calculator?

The answers to this question finally led to my radical redesign of the calculator interface in my app, *Calcuta*.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d77f68e-2bfa-4eb1-821e-e6efd2e9fe8a/02-iphones-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55033db3-34dc-4b79-8116-86e36adc7e98/02-iphones-preview-opt.jpg" width="600" height="600" alt="Smart phone and smart watch showing Calcuta's radical keypad" /></a><figcaption>Though radial keypads, such as the one in Calcuta (above) were better rated by users, Bell Laboratories stayed with the standard square layout in its touchtone phones, perhaps to give users a familiar experience.</figcaption></figure>

It became apparent early in the design process that **there is no logical or self&ndash;evident way to arrange ten digits within a rectangular space**. Alphabets can be laid out according to their frequency of usage on a QWERTY keyboard, but numbers follow no such patterns. With any number equally likely to be pressed, what would be the most logical and ergonomic arrangement for human fingertips?

**Isolating the zero in its own line** allowed the remaining nine numbers to be arranged in a three&ndash;by&ndash;three square. It may have seemed logical to Casio to arrange the remaining numbers from bottom to top.

The inverted ten&ndash;key numeric keypad made its appearance in 1957 when Tadao Kashio, founder of Casio, released the world’s first electromechanical desktop calculator, the Casio 14&ndash;A. However, the layout of the ten digits was apparently decided quite arbitrarily by Kashio-san. When Bell Laboratories, exploring keypad design for its first touchtone telephones, asked Casio about the logic behind its numeric keypad, they apparently received a “big shrug”.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a2fdcdf-67a5-4e97-8717-99af4a6c2408/03-casioa14-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/414b918f-27d2-4462-a333-c36dbb74692a/03-casioa14-preview-opt.jpg" width="800" height="800" alt="old picture showing layout of keys on Casio’s ten-key numeric keypad" /></a><figcaption>The layout of keys on Casio’s ten-key numeric keypad, launched in 1957, was decided quite arbitrarily. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a2fdcdf-67a5-4e97-8717-99af4a6c2408/03-casioa14-opt.jpg">Large Preview</a>)</figcaption></figure>

Casio’s numeric keypad went unquestioned and unchallenged for decades, appearing on ever sleeker models of calculators, including miniaturized wristwatch devices.  

{{% feature-panel %}}

## How The Calculator Was Belled

In November 1963, Bell Laboratories introduced the world’s first touch&ndash;tone telephone, the Western Electric Model WE 1500, with a keypad that vertically flipped Casio’s design, although zero remained at the bottom. The design change apparently emerged from research conducted by Dr Alphone Chapanis and his assistant Mary C Lutz in the 1950s.

Chapanis designed a **test that examined where people expected to find numbers on keys**, and administered it to 300 people divided into three age groups, and divided further depending on whether they were technologically naive or sophisticated. Six different arrangements of keys were tested. Overwhelmingly &mdash; and not surprisingly &mdash; people preferred an arrangement where the numbers increased from top left to bottom right.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/977800b2-284e-4c96-a235-130090ad9e19/04-we1500-touchtone-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c997eae0-3030-4a69-adc4-388132b07c77/04-we1500-touchtone-preview-opt.jpg" width="800" height="800" alt="Old dial phone from Bell Laboratories' WE 1500" /></a><figcaption>Bell Laboratories' WE 1500, the world’s first touch-tone telephone, launched in 1963, vertically flipped Casio’s numeric keypad design, although zero remained at the bottom. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/977800b2-284e-4c96-a235-130090ad9e19/04-we1500-touchtone-opt.jpg">Large Preview</a>)</figcaption></figure>

[Numberphile](https://www.numberphile.com/videos/keypad_layout.html) dug up a little&ndash;known research paper from the July 1960 issue of the *Bell System Technical Journal*, which listed the 18 different keypad designs their engineers had field&ndash;tested. Among them: “the staircase” (II&ndash;B in the image below); “the ten&ndash;pin” (III&ndash;B, reminiscent of bowling&ndash;pin configurations); “the rainbow” (II&ndash;C); and various other versions that mimicked the circular logic of the existing rotary dialing technology.

The winner (IV&ndash;A) probably felt the most familiar to users. But was it the most ergonomic and aesthetic?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80dfc736-0c8a-4f57-bf4e-e451d3e63d61/05-17designs-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72525137-ec8d-4ecb-91d6-ea4d3f5f6b3d/05-17designs-preview-opt.jpg" width="800" height="1156" alt="Layout of six groups of numeric keypads, in many different displays such as semi circle, full circle with the 0 in the middle, cross shape and so on" /></a><figcaption>Though the radial design scored higher in ease of use and error rate, Bell Laboratories went ahead with the square numeric keypad. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80dfc736-0c8a-4f57-bf4e-e451d3e63d61/05-17designs-opt.jpg">Large Preview</a>)</figcaption></figure>

Numberphile’s Sarah Wiseman noted, "They did compare the telephone layout and the calculator layout, and they found the calculator layout was slower."

But there is another, more worldly&ndash;wise story also on the grapevine. Bell Labs was apparently concerned that its switching exchanges might not be able to **keep up with users who typed too fast**. To slow them down just a tad, they deliberately inverted the keyboard, while keeping the zero at the bottom, to make it a little less familiar to users.  

## If It Ain’t Broke, Why Fix It?

The mobile calculator’s design has always vexed me. From a design point of view, it has several demonstrably serious flaws.

1.  **The keypad was not designed for the small rectangular screens of today’s mobile phones.** It has never been reviewed for its synergy with gestures and modern modes of user interaction with mobiles.
2.  **Most calculators offer little or no feedback to users.** For instance, if they are interrupted in the middle of a calculation, they have no intuitive way of knowing the last thing typed. There is no way to verify if a mistake was made, a number omitted, an extra number typed, or the wrong operator punched. If a mistake is suspected or detected, the entire calculation has to be keyed in again. In these respects, most mobile calculators repeat the weaknesses of old handheld calculators.
3.  **Memory operations, which still mimic the way physical, handheld calculators used to work, are often opaque and confusing.** There is a plethora of Ms: M, M+, M–, MC, MR, MS. There is also no clear way to know what’s stored in memory, or how it has been altered by operations that change memory contents.
4.  **Though many calculators now include a delete key, this merely adds to the clutter.** Some calculators allow deletion by swiping, but this is often a hidden feature, so users, unaware of its existence, simply retype the entire calculation.
5.  **Some calculators include the digital equivalent of a roll of paper tape**, familiar to anyone who has seen a credit card machine print a slip after the transaction is authorized. But this once again mimics a long&ndash;gone mechanical reality. As a user, I would wish to correct mistakes more intuitively and with less effort.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85149eed-45eb-4623-84bd-a2c7685806b1/06-papertape-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3584c4a-5a89-4918-b6f0-5874d38ae829/06-papertape-preview-opt.jpg" width="640" height="1136" alt="screen with calculator app using an analogy to paper tape" /></a><figcaption>Many calculators use the visual analogy of the paper tape, familiar to anyone who has watched a credit card machine print out a bill after the transaction is authorized. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85149eed-45eb-4623-84bd-a2c7685806b1/06-papertape-opt.jpg">Large Preview</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

## Redesigning The Calculator

My design process began with a close study of Bell Laboratories’ 17 keypad designs. An asterisk next to the design number indicated 'significantly shorter keying time'; a dagger meant 'significantly lower error rate'; and a double dagger indicated 'significantly more preferred.' Designs II&ndash;A, IV&ndash;A and IV&ndash;B all scored an asterisk for ease of keying; only VI&ndash;B scored a double dagger. I noticed, however, that **the only design that rated an asterisk and a dagger was I&ndash;C, a radial design**. The radial design scored against square design I&ndash;A, which was part of the same Group I.

The redesign involved four steps.  

### 1. Reinventing The Numeric Keypad

**Problem:** The original Casio numeric keypad had physical buttons mounted on a panel, and square buttons on a rectangular grid was a logical way to use available space. The buttons on a calculator are punched in. What should the keypad look like on a handheld device sensitive to touch and without physical buttons?

**Design:** I strung the numbers together in a radial garland. This made them available sequentially along a circle, and also easily accessible to the user’s thumb. The radial arrangement instantly made the numbers visible as a group, and also opened up the screen space.

In the radial garland, I included the decimal buttons, and the clear/reset button <kbd>C/AC</kbd>.  

**Color:** Every color needed a purpose. The numeric radial was the single most important element in the design and needed maximum visibility. I chose a vivid blue, and a night black background to set it off. The C/AC button had to be visible distinctly from the numbers, so I picked a signature orange for that button.  

**Position:** I expected to have more elements above the radial than below, so I positioned the numeric keypad slightly south of centre for balance.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67dab1c8-abd0-4cd3-a4be-f99e40d5591c/07-classicm-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a68251-1484-4150-a187-fd16bc90de1d/07-classicm-preview-opt.png" width="750" height="1334" alt="calculator radical layout using a centered circle to place the numbers clockwise." /></a><figcaption>The redesign separates the numeric keypad from the operators logically. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67dab1c8-abd0-4cd3-a4be-f99e40d5591c/07-classicm-opt.png">Large Preview</a>)</figcaption></figure>

### 2. Resectoring The Screen Real Estate Logically

**Problem**: Software calculators typically divide the screen into two parts: a display area and a keypad area. Within the keypad, numbers, operators, modifiers, and memory buttons are distributed whimsically and can vary from phone to phone. What is a logical, visually sensible arrangement for the different elements of a numeric keypad?

**Solution**: The most frequently used primary operators are +, −, × and ÷. Two modifiers usually included in basic calculators but used less frequently are % and ±. I placed the primary operators in a clear row above the calculator radial, and the two modifiers in a clear line below the radial.  

**Display**: I allocated the top of the display to the numeric display, after opting to switch off the standard iPhone status display strip. The main display area included the current number or current result on the right, while on the left was a single M indicating temporary memory. Unlike in other calculators, I added a secondary display area where the user’s operations are mirrored. This provides live feedback to users, so they can notice errors in real time. The secondary display area under the M can display the current contents of memory, and can be toggled off in the settings.  

### 3. Substituting Gestures For Buttons

The only way to communicate with an old style Casio was by **pressing a button**, and this input method has by and large survived intact in modern software calculators. This has led to a proliferation of keys, including a delete button and several Ms, one for each memory action. How could a calculator take advantage of gestures?

Gestures added:

*   Swiping left or right in the main display area deletes numbers one at a time from right to left.
*   Tapping the number in the main display once adds it to memory. Tapping it twice subtracts it from memory.
*   The M button remains white when memory is empty, but turns red to indicate content.
*   Tapping M once when it has content adds the number in memory to the number in the display. Tapping it twice subtracts it from the display.
*   Swiping over the M erases the contents of memory.  

{{% ad-panel-leaderboard %}}

### 4. Enabling Easy Correction Of Errors At Any Time

**Problem**: Errors cannot be corrected on a manual calculator. Mimicking the Casio calculator interface effectively transfers these limitations to software calculators. The earliest attempts to rectify this introduced a paper tape-like feature, revealing previous operations on a continuous scrolling page. How could editing be made easy and elegant on a modern calculator?

**Edit history**: The single most radical feature in the calculator redesign is the Edit History page, revealed by swiping the screen to the left. The Edit History screen allows touch-based editing of numbers and operators, including deleting entire lines by swiping left. The calculation results are updated in real time.  

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55d417c5-d59f-4977-9a60-d1b9f658fc63/08-edit-history2-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d91940e-2b6e-4989-b6af-0cd1c5a28e25/08-edit-history2-preview-opt.png" width="750" height="1334" alt="Screen showing Calcuta's app on use" /></a><figcaption>Swiping the Calcuta screen left reveals the Edit History page where previous inputs can be corrected or deleted, entire lines deleted, and operators changed. Recalculations are instantaneous. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55d417c5-d59f-4977-9a60-d1b9f658fc63/08-edit-history2-opt.png">Large Preview</a>)</figcaption></figure>

## The Response And The Future

The word most consistently heard from users in response to the new interface is *delightful*. I believe there is room for a hard-working calculator that is also a pleasure to use. I am currently working to expand the app into a teaching tool that can inculcate a love of math in children and improve their numeracy. The clean interface is ideally suited to appealing to children.

I welcome your feedback, brickbats more than bouquets.  

### Resource Links

*   “[Expected Locations of Digits and Letters on Ten-Button Keysets](https://mrserge.lv/assets/expected-locations-of-digits-and-letters-on-ten-button-keysets.pdf)” (PDF) by Mary Champion Lutz (Bell Telephone Laboratories) and Alphonse Chapanis (Johns Hopkins University). The Journal of Applied Psychology. Vol 39, № 5, 1955.
*   “[Why Phone Keypads and Calculator/Keyboard Keypads are Arranged Differently](https://www.todayifoundout.com/index.php/2015/10/keypad-numbering-different-phones/)”
*   “[Human Factors](https://www.americanscientist.org/libraries/documents/20057611634_306.pdf.)” (PDF) by Henry Petowski. Reprinted from The Scientific American. 2000.
*   “[The 17 Designs That Bell Almost Used for the Layout of Telephone Buttons](https://www.theatlantic.com/technology/archive/2013/08/the-17-designs-that-bell-almost-used-for-the-layout-of-telephone-buttons/279237/)” by Megan Garber. The Atlantic, August 2013.
*   [Casio Wikipedia Article](https://en.wikipedia.org/wiki/Casio)
*   [Apple Human Interface Guidelines](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/)

### Further Reading on Smashing Magazine:

*   “[A User-Centered Approach To Web Design For Mobile Devices](https://www.smashingmagazine.com/2011/05/a-user-centered-approach-to-web-design-for-mobile-devices/),” Lyndon Cerejo
*   “[The Elements Of The Mobile User Experience](https://www.smashingmagazine.com/2012/07/elements-mobile-user-experience/),” Lyndon Cerejo
*   “[A Guide To Designing Touch Keyboards (With Cheat Sheet)](https://www.smashingmagazine.com/2013/08/guide-to-designing-touch-keyboards-with-cheat-sheet/),” Christian Holst
*   “[Beyond The Button: Embracing The Gesture-Driven Interface](https://www.smashingmagazine.com/2013/05/gesture-driven-interface/),” Thomas Joos

{{< signature "jb, og, nl" >}}