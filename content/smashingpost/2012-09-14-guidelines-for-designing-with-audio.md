---
title: Guidelines For Designing With Audio
slug: guidelines-for-designing-with-audio
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98e409ce-3906-4740-be7c-92c5c49718b3/earphones-mug-relax-opt.jpg
date: 2012-09-14T11:37:40.000Z
author: karen-kaushansky
description: >-
  As [we’ve
  seen](https://www.smashingmagazine.com/2012/04/18/designing-with-audio-what-is-sound-good-for/),
  audio is used as a feedback mechanism when users interact with many of their
  everyday devices, such as mobile phones, cars, toys and robots. There are many
  subtleties to designing with audio in order to create useful, non-intrusive
  experiences. Here, we’ll explore some guidelines and principles to consider
  when designing with audio.
categories:
  - UX
  - UI
---
As [we’ve seen](https://www.smashingmagazine.com/2012/04/18/designing-with-audio-what-is-sound-good-for/), audio is used as a feedback mechanism when users interact with many of their everyday devices, such as mobile phones, cars, toys and robots. There are many subtleties to designing with audio in order to create useful, non-intrusive experiences. Here, we’ll explore some guidelines and principles to consider when designing with audio.

While I won’t cover this here, audio is a powerful tool for designing experiences for accessibility, and many of the guidelines discussed here apply. Both Android phones and iPhones already have accessibility options that enable richer experiences with gestural and audio input and audio output.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing With Audio: What Is Sound Good For?](https://www.smashingmagazine.com/2012/04/designing-with-audio-what-is-sound-good-for/)
*   [<span class="headline">How To Create A Responsive 8-Bit Drum Machine</span>](https://www.smashingmagazine.com/2016/08/how-to-create-a-responsive-8-bit-drum-machine-using-web-audio-svg-and-multitouch/)
*   [How To Increase Workflow And Reduce Stress With Nature Sounds](https://www.smashingmagazine.com/2015/10/increase-workflow-reduce-stress-with-nature-sounds/)
*   [Are You Giving Your Users Positive Feedback?](https://www.smashingmagazine.com/2012/07/are-giving-users-positive-feedback/)

First, who designs audio? Certainly, the audio producers and game designers who bring gaming to life. There’s also the world of voice user interface designers — those who design interactive voice response telephone systems for banks, airlines, etc. Then there are mobile, toy and interaction designers who have some of this expertise or who work closely with audio engineers and producers to create the right experience for their devices.

{{% feature-panel %}}

If audio might play a part in your design, here are some considerations to make once you have determined that the user’s device has a speaker and can play audio, and is either network-connected or has enough memory to store audio on the device.</p>

## Audio Design Guidelines

### Choose the Right Type of Audio

Audio can be non-verbal sounds, sometimes called “earcons,” or can be words, sometimes called prompts, and choosing the right type is important. Meaning can be embedded in an earcon in such a way that a short non-intrusive sound can represent something much larger. Think of the [sound that confirms](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbb4dd03-0b08-49c5-8938-1ef8d7971867/iphone-textshort.wav) that a text message has been sent on an iPhone: the sound effectively represents the action by suggesting motion and movement away from the user. Another example is the parking-assist system in a car; the intensity and pitch of sounds create a sense of urgency to let the driver know their distance from the nearest car.

<iframe loading="lazy" width="500" height="330" src="https://www.youtube.com/embed/KFxugwnzXGw" frameborder="0" allowfullscreen></iframe>

Embedding meaning in a single sound allows for quick and efficient feedback; sounds are shorter than verbal prompts and can be less intrusive. The AOL email notification “[You’ve got mail](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf780b3-9ccc-432d-a754-fea765690091/yougotmail.wav)” is a great example of the opposite — an incredibly annoying notification that makes most of us want to throw a hammer at the computer. (But if the AOL sound has made you nostalgic, check out “[13 Tech Sounds You Don’t Hear Anymore](https://gizmodo.com/5918715/13-tech-sounds-you-dont-hear-anymore).”)

But only so much information can be embedded in a sound. Sometimes words are the best way to communicate an idea. If that is the case with your product (say you are delivering instructions, alerts or dynamic information such as turn-by-turn navigation), then there are ways to design these smartly. You’ll also need to consider whether to localize the experience, with all of the implications that entails. A talking toy sold in multiple countries will probably need to have audio feedback in the language of each country, and this will require some thought on the scalability of audio feedback.</p>

### Embed Meaning in Audio Earcons

So, how can sounds be designed in such a way that the user intuitively knows what they mean? Some research is out there to guide novice earcon designers, such as work done by Blattner et al in “[Earcons and Icons: Their Structure and Common Design Principles](https://www.daimi.au.dk/~dsound/DigitalAudio.dir/Papers/Earcons_and_Icons.pdf)” (PDF). Blattner comments on [W.W. Gaver’s mappings](https://dl.acm.org/citation.cfm?id=1453246) of earcons into symbolic, nomic and metaphorical sounds:

<blockquote>
<p>Symbolic mappings rely on social convention such as applause for approval, nomic representations are physical such as a door slam, and metaphorical mappings are similarities such as a falling pitch for a falling object.</p>
</blockquote>

Blattner goes on to say that if a good mapping can be found, then the earcon will be more easily learned and remembered. Earcons that take advantage of a pre-existing relationships enable users to associate sounds with meaning with minimal or no training.

Designing sound is complex, and audio designers will want to consider pitch, timbre, loudness, duration and direction to create the right sound. For details on how these should be considered in earcon design, consult “[Auditory Interfaces: A Design Platform](https://www.jld.se/dsounds/auditoryinterfaces.pdf)” (PDF).</p>

### Design in Context

Whether you are designing earcons or prompts, consider the particular context of the user, both physically and emotionally. If you are designing audio instructions or information, consider these factors:

*   Is there a way to differentiate between a novice user (i.e. someone who needs more hand-holding) and an expert user? This could be done by keeping track of the number of interactions that the user has with the device, and tailoring an audio experience for first-time users, while playing shortened prompts to expert users.
*   If the device has a screen, do you know whether the user will rely on visual feedback to complete their task? If so, audio might be a secondary feedback mechanism or might not be needed at all. Audio could be tailored specifically for these situations by playing less or different audio. Knowing where the device is in relation to the user could be done with certain sensors or accelerometers or derived from how the interaction was initiated. For example, if an interaction with Siri on the iPhone 4S was initiated from a Bluetooth headset, then the user’s phone is likely not available for visual feedback, so providing rich audio feedback becomes essential.
*   Many other contexts warrant tailoring the audio experience. With GPS, for example, you can determine whether the user is driving (using their speed). Sometimes the current state of the device is relevant and can indicate the proximity of the user or their level of engagement: Is the user listening to music? Have they recently interacted with the device? Have the swiped their credit card? Etc.</p>

### Consider the “Non-Use Cases”

Designers always talk of use cases, but for devices that “talk,” being aware of the non-use cases is also important, situations in which playing audio wouldn’t make sense. Alerts or information being shouted out from a device with no warning or context can be alarming. The example below shows a moving walkway that repeats its warning over and over, even when no one is nearby.

<iframe loading="lazy" width="500" height="330" src="https://www.youtube.com/embed/h5wA7lzV6dk" frameborder="0" allowfullscreen></iframe>

You will often want to give the user control over whether to play audio at all, through the settings. For example, on a Windows Phone, a user can set whether an incoming text message is read aloud automatically only when connected to a Bluetooth headset, when connected to any headset, always or never.</p>

### It’s Not Just What You Say But How You Say It

Designing prompts is part art and part science. Many good speech-recognition and voice user interface design books are out there with details. We’ll look at one example here and some of the problems with the design. Taken from an early version of the Ford Sync’s in-car speech recognition, this [audio clip](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753e2394-dcf4-4012-9ae6-4099578ff46b/usb-help-artist.wav) instructs the driver on how to ask for a particular music artist, but it does it very poorly; the pace, voice and grouping of words are just not clear enough.

Some design guidelines:

*   Use language that users understand. Stay away from lingo, jargon and technical terms that would make sense to the company but not to the end user.
*   Do not overload the user with too much information at once.
*   Limit the number of audio menu options. Audio is linear, time-sensitive and transient, unlike the Web and other visual feedback media in which users can take time to read, process and select. Research has shown that remembering more than five options from an audio menu is hard. Users will often listen to all choices before picking one, so a long list will limit their ability to remember them all.
*   When writing prompts that require users to make a choice, structure them so that the menu option comes before the action; for example “For y, press x,” instead of “Press x for y.” The user will more easily be able to identify the option they want and listen more attentively for the action.</p>

### Decide Between Recorded Prompts and Text-to-Speech

Another decision to make is whether to prerecord the audio with a voice actor or use text-to-speech (TTS). Prerecorded audio provides the most natural reading of text in most cases, but there are many considerations to make before implementing it. How many things must be recorded? Will the audio content change? How much storage is available?

Over the years, TTS has improved dramatically and in some cases does a great job of reading back audio. TTS engines should be evaluated based on the task at hand: Are multiple languages needed? Multiple voices? Is the type of information to be read back specialized? Evaluating various implementations is also important: Is the device connected, in which case the TTS engine could be cloud-based, or will the TTS engine need to be embedded in the device? Reactions to TTS vary; some users say that TTS impairs the experience so much that they avoid using it, while others barely notice it.

Here are two examples:

*   [The Talking Alarm](https://itunes.apple.com/us/app/the-talking-alarm/id496971715?mt=8) is an alarm clock app for the iPhone that reads back different types of information to wake you up. Listen to it [reading the date and time and a horoscope](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9405c2a-f911-4341-85dc-83a2c39b51b1/talkingalarm.wav).
*   [Dial2Do](https://www.dial2do.com/) uses TTS for its hands-free assistant. Listen to it [read the following email](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9c318ad-411b-4164-9dce-0774ed8ddc95/dial2do-short.wav):

[![TTS Email](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bce0c46-3d22-46a7-85cb-2e9350628206/ttsemail-small3.jpg "TTS Email")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bce0c46-3d22-46a7-85cb-2e9350628206/ttsemail-small3.jpg)

### Recording Prompts

If you are able to record all prompts with an actor, choose a voice and personality that fits your brand and the experience. Best to recruit talent with a personality in mind, and have them record a representative script to evaluate how they would come across in the device.

There are many subtleties to be aware of when recording prompts. Voice user interface designers spend time directing voice actors to make sure that the prompts elicit the right spoken response from users. The following prompt can mean different things depending on how it’s read: “Would you like departures _<pause>_ or arrivals?” would steer users to say “departures” or “arrivals.” A slightly different reading, “Would you like departures or arrivals?”, could be misinterpreted by users as requiring a yes or no response.

Prompts can be recorded even when some of the prompts need to change dynamically, such as when reading back the time or a phone number. In these cases, you would record shorter prompts and then concatenate them together during playback. To make these readings sound natural instead of robotic, record as large a chunk of the prompt as possible.</p>

## Summary

The most important consideration when designing with audio is to ensure that it enhances the experience and does not interfere or distract. If you are considering designing with audio, hopefully you are now armed with some helpful information to get you started on designing a great experience.

{{< signature "al" >}}

