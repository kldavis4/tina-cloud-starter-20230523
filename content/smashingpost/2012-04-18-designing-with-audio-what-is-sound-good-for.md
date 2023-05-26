---
title: 'Designing With Audio: What Is Sound Good For?'
slug: designing-with-audio-what-is-sound-good-for
image: >-
  https://www.smashingmagazine.com/general/2013/08/15/168593-revision-108/attachment/shortcode-menu-2/attachment/buds/
date: 2012-04-18T11:39:08.000Z
author: karen-kaushansky
description: >-
  Our world is getting louder. Consider all the beeps and bops from your
  smartphone that alert you that something is happening, and all the feedback
  from your appliances when your toast is ready or your oven is heated, and when
  Siri responds to a question you’ve posed. Today our technology is expressing
  itself with sound, and, as interaction designers, we need to consider how to
  deliberately design with audio to create harmony rather than cacophony.
categories:
  - UX
  - Design
  - UI
  - Interaction Design
  - Web Audio
---
Our world is getting louder. Consider all the beeps and bops from your smartphone that alert you that something is happening, and all the feedback from your appliances when your toast is ready or your oven is heated, and when Siri responds to a question you’ve posed.

Today our <strong>technology is expressing itself with sound</strong>, and, as interaction designers, we need to consider how to deliberately design with audio to create harmony rather than cacophony. The cacophony is beautifully captured in <a href="https://vimeo.com/35873217">Chris Crutchfield’s video</a>, in which he interprets the experience of receiving email, SMS texts, phone calls, Facebook messages and tweets all at the same time:

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Guidelines For Designing With Audio](https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/)
*   [<span class="headline">How To Create A Responsive 8-Bit Drum Machine</span>](https://www.smashingmagazine.com/2016/08/how-to-create-a-responsive-8-bit-drum-machine-using-web-audio-svg-and-multitouch/)
*   [How To Increase Workflow And Reduce Stress With Nature Sounds](https://www.smashingmagazine.com/2015/10/increase-workflow-reduce-stress-with-nature-sounds/)
*   [Are You Giving Your Users Positive Feedback?](https://www.smashingmagazine.com/2012/07/are-giving-users-positive-feedback/)

In this article, we’ll explore some of the uses of audio, where we might find it and when it is useful. This is meant not as a tutorial but rather as a discussion of some basics on using audio feedback.

{{% feature-panel %}}

Audio is a form of feedback that can be used either in combination with other forms, such as haptics, visual displays and LEDs, or on its own. We have to weigh several factors when designing feedback mechanisms: the scenario, the device and the interaction, where and how the device will be used, whether the user has a screen or display, whether the device has physical buttons or a touchscreen, where the user is relative to the device, and so on.

For every action of the user, a good experience will include feedback that the action has been registered; for example, pressing a number key on a mobile phone would play a sound and show the number being pressed. Audio is particularly useful when there is no screen or when looking at the screen is not possible or not desirable (such as when users want to multitask). It’s interactive, <strong>creating a dialog with the user</strong>. It is also particularly good at providing feedback as “shared audio,” a form of feedback that reaches multiple people at once, such as a PA system or a citywide emergency warning system.

Audio is not always warranted. Something that makes noise repeatedly when other feedback would suffice is annoying. Audio that is private and intended for you but is heard by others is embarrassing, such as when your phone rings and announces a “Call from Sexy Neighbor.” Audio design has many ins and outs, but let’s start with some common uses of audio feedback.</p>

## Where We Find Audio

Many of us who work on interaction, mobile, device or game design have already discovered the importance of designing audio — audio is everywhere.

<a href="https://www.flickr.com/photos/renneville/2908748583/sizes/l/in/photostream/"><img loading="lazy" decoding="async" class="111767" title="Ear buds" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb7c4cd3-0afb-4a76-ac45-3477da7ebcba/buds.jpg" alt="Ear buds" width="500" height="340" /></a><br>
<em>(Image credit: <a href="https://www.flickr.com/photos/renneville/2908748583/sizes/l/in/photostream/">Fey Ilyas</a>)</em>

### Mobile

Much of the Web is moving to mobile, which of course entails smaller screens and people on the go. But besides creating mobile-specific websites, there are ways to <strong>augment the mobile experience with audio</strong> when people aren’t looking at or can’t interact with the screen. A great example is GPS and turn-by-turn navigation systems that speak directions (either as part of a dedicated device or from a smartphone app). While audio isn’t yet native to mobile websites and apps, it is native to smartphones to indicate new email, incoming text messages and calendar events.</p>

### Gaming

For those who play video games, audio is integral to <strong>setting the mood, environment and situation</strong>, and it engages the user tremendously. First-person shooter games such as Halo and Call of Duty rely on audio feedback to show cause and effect — for example, the sound of a gun shooting and the moment of impact on the enemy. Or consider Wii Sports: the smash of the ball in tennis, the crack of the bat in baseball, and the cheer of fans all help to blur the line between the very physical game and the digital world.</p>

### Consumer Devices

As more appliances become smarter and connected, they might have more to say. Today a set of beeps tells you that the refrigerator door is open, but in the future you can expect notifications that the milk has gone bad or that you need to pick up eggs if you want to make that cake for your spouse’s birthday on Tuesday.

More and more of our everyday devices use audio feedback: a Bluetooth headset tells you who is calling, Nike+ tells you your current distance travelled and pace, and cars beep to help you park.

### Speech Recognition and Robots

Voice interaction such as Siri’s is <strong>revolutionizing the way people interact</strong> with their iPhone and will help to change future interactions with all devices and information sources. People are beginning to talk to their devices and expect some audio feedback in return. Siri is just the start; we’re starting to see speech recognition in Xbox Kinect, Samsung TVs and more. Audio feedback is a natural way to let the user know that the system or device has heard them, is processing their request and so on.

Think of your favorite robots — HAL, Wall-E or any of the personal robotic devices that are emerging. These robots are developing human characteristics, with sounds being one of the strongest ways to <strong>deliver emotion</strong>. <a href="https://www.willowgarage.com/pages/people/leila-takayama-research-scientist">Leila Takayama</a> of Willow Garage has talked about the “design challenge in communicating internal robot states and requests to effectively reach the robot’s assigned goals.” Willow Garage has created a set of sound libraries for communication between people and robots that might help make robots “more appealing.” Then there are other robots that speak English and other languages, such as the new Autom weight-loss coach. <a href="https://spectrum.ieee.org/automaton/robotics/home-robots/autom-robotic-weight-loss-coach-now-available-for-preorder">Studies have shown</a> that people who use Autom stick with their diet and exercise routines for twice as long as people who use traditional weight-loss methods, perhaps partly because of its human-like interactions.</p>

## Why Use Audio?

There are numerous principles to determine why and when to use audio in designing interactions for devices. Being conscious about adding sound to a device is the first step in designing it right. The point is to do it deliberately, not as an afterthought, so that <strong>the audio means something</strong> and is not annoying. Here are some of the many scenarios in which you should consider using audio.</p>

### Instructions and Information

Audio is used to give instructions, especially where there is no screen or where looking at a screen would be difficult, unsafe or impossible. Again, think turn-by-turn directions. Or it can be used to augment visuals. The parking machine below obviously has visual instructions for entering a credit card, but they weren’t sufficient to get people to enter it correctly.

Audio can be used to offer information, either <strong>when no screen is available</strong> or when certain details would be better captured as audio. The Jambox by Jawbone tells the user when they need to recharge the battery. The Leapfrog LeapPad takes this one step further by specifying the type of batteries it needs!

### Feedback and Interaction

As mentioned, audio is used as a <strong>feedback mechanism</strong> when the user takes action. This could be feedback for when the user pushes a button, such as when turning on a Jambox speaker, or to tell a driver that they are getting close to a parked car.

It’s also used to allow for interaction and conversation with our devices. We’re used to interacting with speech-recognition systems when we call an airline or a bank, and now sending a text message with your voice from a Windows phone is just as easy. The audio from these services and devices create a dialog that enables users to get things done.</p>

### Personalization and Customization

Audio allows for <strong>personalization of a device</strong>, helping to engage users and create an emotional attachment. Siri learns its user’s name and uses it in its replies, adding a personal connection to the interaction. Garmin and TomTom let users download all kinds of voices to their GPS devices, from Bert and Ernie to Star Wars characters to <a href="https://www.tomtom.com/en_us/products/voices/kitt/index.jsp">Kitt from Knight Rider</a>, with the goal of creating more engaging experiences. Jawbone device owners can download different languages and characters to their Bluetooth headset and speaker, with the device volunteering such responses as, “A bombshell is whispering in my ear… And yes, I’m blushing.”

Audio also helps to establish personality and to <strong>humanize a device</strong>. Ford and other electric vehicle manufacturers are dealing with a <a href="https://www.govtrack.us/congress/bill.xpd?bill=h111-734">proposed bill</a> that would require electric vehicles to make some sound to ensure pedestrian safety. Ford has asked the public to vote on four different sounds that would essentially shape the personality of its cars. Here’s one of them:

In another example, to show the power of talking devices, <a href="https://www.radiolab.org/2011/may/31/furbidden-knowledge/">Radio Lab reported</a> on an experiment that pitted a hamster against a Barbie doll and a Furby (the popular furry electronic talking robot) to see how long kids could hold each of them upside down. While all of the five kids in the experiment could hold Barbie upside down “almost forever,” they treated Furby much more like the living hamster than the Barbie. Why? Well, when you hold Furby upside down, he says, “Me scared,” giving human-like characteristics to the toy. The kids said afterwards that they “didn’t want him to be scared.”

## Conclusion

Audio is everywhere, and there are <strong>good reasons to use it</strong>: to instruct, enhance and engage and to personalize experiences. But if poorly designed or used inappropriately, it can detract from the experience and be annoying. We’ve covered the why and the where of audio. Next time, we’ll review some guidelines and principles on the ins and out of designing with audio.

{{< signature "al" >}}

