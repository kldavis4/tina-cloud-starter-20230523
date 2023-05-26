---
title: What Sci-Fi Tells Interaction Designers About Gestural Interfaces
slug: sci-fi-interaction-designers-gestural-interfaces
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17cf7310-8942-4a71-83ad-6a6b2936df94/firefly-2002-screenshot-opt.jpg
date: 2013-03-01T12:28:51.000Z
author: chris-noessel
description: >-
  One of the most famous interfaces in sci-fi is gestural — the precog scrubber
  interface used by the Precrime police force in Minority Report. Using this
  interface, Detective John Anderton uses gestures to “scrub” through the
  video-like precognitive visions of psychic triplets.
categories:
  - UX
  - Interfaces
  - Design Patterns
---
One of the most famous interfaces in sci-fi is gestural — the precog scrubber interface used by the Precrime police force in Minority Report. Using this interface, Detective John Anderton uses gestures to “scrub” through the video-like precognitive visions of psychic triplets. After observing a future crime, Anderton rushes to the scene to prevent it and arrest the would-be perpetrator.

This interface is <strong>one of the most memorable things</strong> in a movie that is crowded with future technologies, and it is one of the most referenced interfaces in cinematic history. (In a quick and highly unscientific test, at the time of writing, we typed <code>[sci-fi movie title] + “interface”</code> into Google for each of the movies in the survey and compared the number of results. “Minority Report interface” returned 459,000 hits on Google, more than six times as many as the runner-up, which was “Star Trek interface” at 68,800.)

## <span class="rh">Further Reading</span> on SmashingMag:

*   [To Use Or Not To Use: Touch Gesture Controls For Mobile Interfaces](https://www.smashingmagazine.com/2017/02/touch-gesture-controls-mobile-interfaces/)
*   [<span class="headline">In-App Gestures And Mobile App User Experience</span>](https://www.smashingmagazine.com/2016/10/in-app-gestures-and-mobile-app-user-experience/)
*   [Browser Input Events: Can We Do Better Than The Click?](https://www.smashingmagazine.com/2015/03/better-browser-input-events/)
*   [To Use Or Not To Use: Touch Gesture Controls For Mobile Interfaces](https://www.smashingmagazine.com/2017/02/touch-gesture-controls-mobile-interfaces/)
*   [Retro Futurism At Its Best: Designs and Tutorials](https://www.smashingmagazine.com/2009/06/retro-futurism-at-its-best-designs-and-tutorials/)

It’s fair to say that, to the layperson, the Minority Report interface is synonymous with “gestural interface.” The primary consultant to the filmmakers, John Underkoffler, had developed these ideas of gestural control and spatial interfaces through his company, Oblong, even before he consulted on the film. The real-world version is a general-purpose platform for multiuser collaboration. It’s available commercially through his company at nearly the same state of the art as portrayed in the film.

{{% feature-panel %}}

Though this article references Minority Report a number of times, <strong>two lessons are worth mentioning up front</strong>.

<img loading="lazy" decoding="async" class="115090" title="Make It So Figure 5.6a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/391c8191-1e43-4dc0-b362-4571565531f4/mis-ch05-012.jpg" alt="Minority Report (2002)" width="500" height="209" />

<img loading="lazy" decoding="async" class="115091" title="MIS Figure 5.6b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faaecd2b-dbdd-4988-bb37-5dd3fc0db914/mis-ch05-013.jpg" alt="Minority Report (2002)" width="500" height="209" /><br>
<em>Figures 5.6a–b: Minority Report (2002)</em>

### Lesson: A Great Demo Can Hide Many Flaws.

Hollywood rumor has it that Tom Cruise, the actor playing John Anderton, needed continual breaks while shooting the scenes with the interface because it was exhausting. Few people can hold their hands above the level of their heart and move them around for any extended period. But these rests don’t appear in the film — <strong>a misleading omission for anyone who wants to use a similar interface</strong> for real tasks.

Although a film is not trying to be exhaustively detailed or to accurately portray a technology for sale, demos of real technologies often suffer the same challenge. The usability of the interface, and in this example its gestural language, can be a misleading though highly effective tool to sell a solution, because it doesn’t need to demonstrate every use exhaustively.</p>

### Lesson: A Gestural Interface Should Understand Intent.

The second lesson comes from a scene in which Agent Danny Witwer enters the scrubbing room where Anderton is working and introduces himself while extending his hand. Being polite, Anderton reaches out to shake Witwer’s hand. The computer interprets Anderton’s change of hand position as a command, and Anderton watches as his work slides off of the screen and is nearly lost. He then disregards the handshake to take control of the interface again and continue his work.

<img loading="lazy" decoding="async" class="115092" title="MIS Figure 5.7a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b17ecb2-b6c2-41a7-9a1e-20257d459336/mis-ch05-014.jpg" alt="Minority Report (2002)" width="500" height="208" />

<img loading="lazy" decoding="async" class="115093" title="MIS Figure 5.7b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c17e8dbe-6d18-4fca-ae18-7e675bf1a1e3/mis-ch05-015.jpg" alt="Minority Report (2002)" width="500" height="208" />

<img loading="lazy" decoding="async" class="115094" title="MIS Figure 5.7c" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0717e093-7898-480a-8003-cc2de50ba58e/mis-ch05-016.jpg" alt="Minority Report (2002)" width="500" height="208" />

<img loading="lazy" decoding="async" class="115095" title="MIS Figure 5.7d" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc7ea32f-72e1-4bc9-a06a-316c08a36581/mis-ch05-017.jpg" alt="Minority Report (2002)" width="500" height="208" /><br>
<em>Figures 5.7a–d: Minority Report (2002)</em>

One of the main problems with gestural interfaces is that the user’s body is the control mechanism, but the user intends to control the interface only part of the time. At other times, the user might be reaching out to shake someone’s hand, answer the phone or scratch an itch. <strong>The system must accommodate different modes</strong>: when the user’s gestures have meaning and when they don’t. This could be as simple as an on/off toggle switch somewhere, but the user would still have to reach to flip it.

Perhaps a pause command could be spoken, or a specific gesture reserved for such a command. Perhaps the system could watch the direction of the user’s eyes and regard the gestures made only when he or she is looking at the screen. Whatever the solution, the signal would be best in some other “channel” so that this shift of intentional modality can happen smoothly and quickly without the risk of issuing an unintended command.</p>

### Gesture Is a Concept That Is Still Maturing.

What about other gestural interfaces? What do we see when we look at them? A handful of other examples of gestural interfaces are in the survey, dating as far back as 1951, but the bulk of them appear after 1998 (Figure 5.8).

<img loading="lazy" decoding="async" class="115132" title="MIS 5.8a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7996cae0-82ba-474f-88c7-cdb988197e07/mis-ch05-0181.jpg" alt="Chrysalis (2007)" width="500" height="281" />

<img loading="lazy" decoding="async" class="115097" title="MIS Figure 5.8b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28bbc5d8-91c2-4fad-a56a-8fec85fc6109/mis-ch05-019.jpg" alt="Lost in Space (1998)" width="500" height="214" />

<img loading="lazy" decoding="async" class="115099" title="MIS Figure 5.8c" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0dc4f44-eece-42b1-8685-bf68874e2545/mis-ch05-021.jpg" alt="The Matrix Reloaded (2003)" width="500" height="212" />

<img loading="lazy" decoding="async" class="115100" title="MIS Figure 5.8d" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2f360b6-653e-4626-aab9-d6dd28d4b5e5/mis-ch05-022.jpg" alt="Sleep Dealer (2008)" width="500" height="281" /><br>
<em>Figure 5.8a–d: Chrysalis (2007); Lost in Space (1998); The Matrix Reloaded (2003); Sleep Dealer (2008)</em>

Looking at this group, we see an input technology whose role is still maturing in sci-fi. A lot of variation is apparent, with only a few core similarities among them. Of course, these systems are used for a variety of purposes, including security, telesurgery, telecombat, hardware design, military intelligence operations and even offshored manual labor.

Most of the interfaces let their users interact with no additional hardware, but the Minority Report interface requires its users to don gloves with lights at the fingertips, as does the telesurgical interface in Chrysalis (see Figure 5.8a). We imagine that this was partially for visual appeal, but it certainly would make tracking the exact positions of the fingers easier for the computer.</p>

## Hollywood’s Pidgin

Although none of the properties in the survey takes pains to explain exactly what each gesture in a complex chain of gestural commands means, we can look at the cause and effect of what is shown on screen and piece together a basic gestural vocabulary. Only seven gestures are common across properties in the survey.</p>

### 1. Wave to Activate

The first gesture is waving to activate a technology, as if to wake it up or gain its attention. To activate his spaceship’s interfaces in The Day the Earth Stood Still, Klaatu passes a flat hand above their translucent controls. In another example, Johnny Mnemonic waves to turn on a faucet in a bathroom, years before it became common in the real world (Figure 5.9).

<img loading="lazy" decoding="async" class="115101" title="MIS Figure 5.9a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d6c2593-5fd3-451d-9333-cce3c016532d/mis-ch05-023.jpg" alt="Johnny Mnemonic (1995)" width="500" height="279" />

<img loading="lazy" decoding="async" class="115102" title="MIS Figure 5.9b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1346b81-fc32-4b5e-93c1-fee132fd10af/mis-ch05-024.jpg" alt="Johnny Mnemonic (1995)" width="500" height="279" />

<img loading="lazy" decoding="async" class="115103" title="MIS Figure 5.9c" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0c0e0b0-9007-4514-82ce-95528bed6d3c/mis-ch05-025.jpg" alt="Johnny Mnemonic (1995)" width="500" height="279" /><br>
<em>Figure 5.9a–c: Johnny Mnemonic (1995)</em>

### 2. Push to Move

To move an object, you interact with it in much the same way as you would in the physical world: fingers manipulate; palms and arms push. Virtual objects tend to have the resistance and stiffness of their real-world counterparts for these actions. Virtual gravity and momentum may be “turned on” for the duration of these gestures, even when they’re normally absent. Anderton does this in Minority Report as discussed above, and we see it again in Iron Man 2 as Tony moves a projection of his father’s theme park design (Figure 5.10).

<img loading="lazy" decoding="async" class="115104" title="MIS Figure 5.10a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08adcc77-a9ea-4a87-9ce7-009241f3b5e6/mis-ch05-026.jpg" alt="Iron Man 2 (2010)" width="500" height="216" />

<img loading="lazy" decoding="async" class="115105" title="MIS Figure 5.10b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1b2f741-1902-45db-84ed-220a69fe2093/mis-ch05-027.jpg" alt="Iron Man 2 (2010)" width="500" height="216" /><br>
<em>Figure 5.10a–b: Iron Man 2 (2010)</em>

### 3. Turn to Rotate

To turn objects, the user also interacts with the virtual thing as one would in the real world. Hands push opposite sides of an object in different directions around an axis and the object rotates. Dr. Simon Tam uses this gesture to examine the volumetric scan of his sister’s brain in an episode of Firefly (Figure 5.11).

<img loading="lazy" decoding="async" class="115106" title="MIS Figure 5.11a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eece19a2-8437-4c01-889a-f9c4167ca5ff/mis-ch05-028.jpg" alt="Firefly, “Ariel” (Episode 9, 2002)" width="500" height="282" />

<img loading="lazy" decoding="async" class="115107" title="MIS Figure 5.11b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b66a4e1f-9430-49a8-b6bc-ace3e6b10935/mis-ch05-029.jpg" alt="Firefly, “Ariel” (Episode 9, 2002)" width="500" height="282" /><br>
<em>Figure 5.11a–b: Firefly, “Ariel” (Episode 9, 2002)</em>

### 4. Swipe to Dismiss

Dismissing objects involves swiping the hands away from the body, either forcefully or without looking in the direction of the push. In Johnny Mnemonic, Takahashi dismisses the videophone on his desk with an angry backhanded swipe of his hand (Figure 5.12). In Iron Man 2, Tony Stark also dismisses uninteresting designs from his workspace with a forehanded swipe.

<img loading="lazy" decoding="async" class="115108" title="MIS Figure 5.12a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3a3decf-784b-4163-812b-963ba48aa945/mis-ch05-030.jpg" alt="Johnny Mnemonic (1995)" width="500" height="279" />

<img loading="lazy" decoding="async" class="115109" title="MIS Figure 5.12b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80ee0754-15ee-405f-aae2-7a0421211844/mis-ch05-031.jpg" alt="Johnny Mnemonic (1995)" width="500" height="279" />

<img loading="lazy" decoding="async" class="115110" title="MIS Figure 5.12c" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36e479e8-e1d0-4d91-93e1-84533a3e041b/mis-ch05-032.jpg" alt="Johnny Mnemonic (1995)" width="500" height="279" /><br>
<em>Figure 5.12a–c: Johnny Mnemonic (1995)</em>

### 5. Point or Touch to Select

Users indicate options or objects with which they want to work by pointing a fingertip or touching them. District 9 shows the alien Christopher Johnson touching items in a volumetric display to select them (Figure 5.13a). In Chrysalis, Dr. Brügen must touch the organ to select it in her telesurgery interface (Figure 5.13b).

<img loading="lazy" decoding="async" class="115133" title="MIS 5.13a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7eebfa3-980c-430d-9b6d-e24b54aa2f2c/mis-ch05-0331.jpg" alt="District 9 (2009)" width="500" height="272" />

<img loading="lazy" decoding="async" class="115112" title="MIS Figure 5.13b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f4dd02a-1785-4eeb-a1dc-20ece4dc8dfc/mis-ch05-034.jpg" alt="Chrysalis (2007)" width="500" height="281" /><br>
<em>Figure 5.13a–b: District 9 (2009), Chrysalis (2007)</em>

### 6. Extend the Hand to Shoot

Anyone who played cowboys and Indians as a child will recognize this gesture. To shoot with a gestural interface, one extends the fingers, hand and/or arm toward the target. (Making the pow-pow sound is optional.) Examples of this gesture include Will’s telecombat interface in Lost in Space (see Figure 5.8c), Syndrome’s zero-point energy beam in The Incredibles (Figure 5.14a) and Tony Stark’s repulsor beams in Iron Man (Figure 5.14b).

<img loading="lazy" decoding="async" class="115113" title="MIS Figure 5.14a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a489877-1337-4561-befd-4f968023a351/mis-ch05-035.jpg" alt="The Incredibles (2004)" width="500" height="210" />

<img loading="lazy" decoding="async" class="115114" title="MIS Figure 5.14b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94412251-67d8-4c80-8c8d-a6a5e592731a/mis-ch05-036.jpg" alt="Iron Man (2008)" width="500" height="212" /><br>
<em>Figures 5.14a–b: The Incredibles (2004), Iron Man (2008)</em>

### 7. Pinch and Spread to Scale

Given that there is no physical analogue to this action, its consistency across movies comes from the physical semantics: to make a thing bigger, indicate the opposite edges of the thing and drag the hands apart. Likewise, pinching the fingers together or bringing the hands together shrinks virtual objects. Tony Stark uses both of these gestures when examining models of molecules in Iron Man 2 (Figure 5.15).

Though there are other gestures, the survey revealed no other strong patterns of similarity across properties. This will change if the technology continues to mature in the real world and in sci-fi. More examples of it may reveal a more robust language forming within sci-fi, or reflect conventions emerging in the real world.

<img loading="lazy" decoding="async" class="115115" title="MIS Figure 5.15a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f4afa06-06c4-4e2a-abf4-3fb8f906ca89/mis-ch05-037.jpg" alt="Iron Man 2 (2010)" width="500" height="216" />

<img loading="lazy" decoding="async" class="115116" title="MIS Figure 5.15b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/568410b8-4537-4f4a-8642-13536cf1ecd1/mis-ch05-038.jpg" alt="Iron Man 2 (2010)" width="500" height="216" /><br>
<em>Figures 5.15a–b: Iron Man 2 (2010)</em>

### Opportunity: Complete the Set of Gestures Required.

In the real world, users have some fundamental interface controls that movies never show but for which there are natural gestures. An example is volume control. Cupping or covering an ear with a hand is a natural gesture for lowering the volume, but because volume controls are rarely seen in sci-fi, the actual gesture for this control hasn’t been strongly defined or modeled for audiences. The first gestural interfaces to address these controls will have an opportunity to round out the vocabulary for the real world.</p>

### Lesson: Deviate Cautiously From the Gestural Vocabulary.

If these seven gestures are already established, it is because they make intuitive sense to different sci-fi makers and/or because the creators are beginning to repeat controls seen in other properties. In either case, the meaning of these gestures is beginning to solidify, and a designer who deviates from them should do so only with good reason or else risk confusing the user.</p>

## Direct Manipulation

An important thing to note about these seven gestures is that most are transliterations of physical interactions. This brings us to a discussion of direct manipulation. When used to describe an interface, direct manipulation refers to a user interacting directly with the thing being controlled — that is, with <strong>no intermediary input devices or screen controls</strong>.

For example, to scroll through a long document in an “indirect” interface, such as the Mac OS, a user might grasp a mouse and move a cursor on the screen to a scroll button. Then, when the cursor is correctly positioned, the user clicks and holds the mouse on the button to scroll the page. This long description seems silly only because it describes something that happens so fast and that computer users have performed for so long that they forget that they once had to learn each of these conventions in turn. But they are conventions, and each step in this complex chain is a little bit of extra work to do.

But to scroll a long document in a direct interface such as the iPad, for example, users put their fingers on the “page” and push up or down. There is no mouse, no cursor and no scroll button. In total, scrolling with the gesture takes less physical and cognitive work. <strong>The main promise of these interfaces</strong> is that they are easier to learn and use. But because they require sophisticated and expensive technologies, they haven’t been widely available until the past few years.

In sci-fi, gestural interfaces and direct manipulation strategies are tightly coupled. That is, it’s rare to see a gestural interface that isn’t direct manipulation. Tony Stark wants to move the volumetric projection of his father’s park, so he sticks his hands under it, lifts it and walks it to its new position in his lab. In Firefly, when Dr. Tam wants to turn the projection of his sister’s brain, he grabs the “plane” that it’s resting on and pushes one corner and pulls the other as if it were a real thing. Minority Report is a rare but understandable exception because the objects Anderton manipulates are video clips, and video is a more abstract medium.

This coupling isn’t a given. It’s conceptually possible to run Microsoft Windows 7 entirely with gestures, and it is not a direct interface. But the fact that gestural interfaces erase the intermediaries on the physical side of things fits well with erasing the intermediaries on the virtual side of things, too. So, <strong>gesture is often direct</strong>. But this coupling doesn’t work for every need a user has. As we’ve seen above, direct manipulation does work for gestures that involve physical actions that correspond closely in the real world. But, moving, scaling and rotating aren’t the only things one might want to do with virtual objects. What about more abstract control?

As we would expect, this is where gestural interfaces need additional support. Abstractions by definition don’t have easy physical analogues, and so they require some other solution. As seen in the survey, one solution is to add a layer of graphical user interface (GUI), as we see when Anderton needs to scrub back and forth over a particular segment of video to understand what he’s seeing, or when Tony Stark drags a part of the Iron Man exosuit design to a volumetric trash can (Figure 5.16). These elements are controlled gesturally, but they are not direct manipulation.

<img loading="lazy" decoding="async" class="115117" title="MIS Figure 5.16a" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aac2cf99-226e-4867-b598-8841e2b7b5ba/mis-ch05-039.jpg" alt="Minority Report (2002)" width="500" height="209" />

<img loading="lazy" decoding="async" class="115118" title="MIS Figure 5.16b" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8dd2776-6449-427b-92f7-c6c1494b9d89/mis-ch05-040.jpg" alt="Iron Man (2008)" width="500" height="212" />

<img loading="lazy" decoding="async" class="115119" title="MIS Figure 5.16c" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6a6317d-f828-4b5e-bfef-07e56fd810fb/mis-ch05-041.jpg" alt="Iron Man (2008)" width="500" height="212" /><br>
<em>Figure: 5.16a–c Minority Report (2002), Iron Man (2008)</em>

Invoking and selecting from among a large set of these GUI tools can become quite complicated and place a DOS-like burden on memory. Extrapolating this chain of needs might very well lead to a complete GUI to interact with any fully featured gestural interfaces, unlike the clean, sparse gestural interfaces that sci-fi likes to present. The other solution seen in the survey for handling these abstractions is the use of another channel altogether: voice.

In one scene from Iron Man 2, Tony says to the computer, “JARVIS, can you kindly vacuform a digital wireframe? I need a manipulable projection.” Immediately JARVIS begins the scan. Such a command would be much more complex to issue gesturally. Language handles abstractions very well, and humans are pretty good at using language, so <strong>this makes language a strong choice</strong>.

Other channels might also be employed: GUI, finger positions and combinations, expressions, breath, gaze and blink, and even brain interfaces that read intention and brainwave patterns. Any of these might conceptually work but may not take advantage of the one human medium especially evolved to handle abstraction — language.</p>

### Lesson: Use Gesture for Simple, Physical Manipulations, and Use Language for Abstractions.

Gestural interfaces are engaging and quick for interacting in “physical” ways, but outside of a core set of manipulations, gestures are complicated, inefficient and difficult to remember. For less concrete abstractions, designers should offer some alternative means, ideally linguistic input.</p>

## Gestural Interfaces: An Emerging Language

Gestural interfaces have enjoyed a great deal of commercial success over the last several years with the popularity of gaming platforms such as Nintendo’s Wii and Microsoft’s Kinect, as well as with gestural touch devices like Apple’s iPhone and iPad. The term “natural user interface” has even been bandied about as a way to try to describe these. But the examples from sci-fi have shown us that <strong>gesturing is “natural” for only a small subset of possible actions</strong> on the computer. More complex actions require additional layers of other types of interfaces.

Gestural interfaces are highly cinemagenic, rich with action and graphical possibilities. Additionally, they fit the stories of remote interactions that are becoming more and more relevant in the real world as remote technologies proliferate. So, despite their limitations, <strong>we can expect sci-fi makers to continue to include gestural interfaces</strong> in their stories for some time, which will help to drive the adoption and evolution of these systems in the real world.

<em>This post is an excerpt of </em>Make It So: Interaction Design Lessons From Science Fiction<em> by Nathan Shedroff and Christopher Noessel (Rosenfeld Media, 2012). You can read more analysis on the <a href="https://scifiinterfaces.wordpress.com">book’s website</a>.</em>

{{< signature "al" >}}

