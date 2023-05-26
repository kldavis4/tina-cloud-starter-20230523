---
title: 'The DAU Of Hip-Hop: Designing For Authenticity (A Case Study)'
slug: the-dau-of-hip-hop-designing-for-authenticity
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1989b76-998e-4467-af9a-b37fe32eeae1/04-uncool-preview-opt.png
date: 2016-06-23T17:02:59.000Z
author: benjaminhersh
description: >-
  In the tech industry, many of us came of age during hip-hop's rise as a
  dominant art form. Its spirit of individualism, bravado, and constant
  reinvention makes it impossible for us not to admire. Our thought leaders
  craft [mixtapes](https://genius.com/artists/The-blind-mc) and pour millions of
  dollars into [apps that decode rap
  lyrics](https://genius.com/Marc-andreessen-why-andreessen-horowitz-is-investing-in-rap-genius-annotated).

  The founders of my former company rapped to celebrate every corporate
  milestone. We’re compelled to [quantify](https://poly-graph.co/vocabulary.html)
  what we love about it, and to somehow technologize it the same way Instagram
  did photography. Many have tried, myself included, but capturing hip-hop’s
  alluring qualities in an app is no simple task.
categories:
  - Mobile
  - Workflow
  - Process
  - Apps
---
In the tech industry, many of us came of age during hip-hop's rise as a dominant art form. Its spirit of individualism, bravado, and constant reinvention makes it impossible for us not to admire. Our thought leaders craft <a href="https://genius.com/artists/The-blind-mc">mixtapes</a> and pour millions of dollars into <a href="https://genius.com/Marc-andreessen-why-andreessen-horowitz-is-investing-in-rap-genius-annotated">apps that decode rap lyrics</a>.

The founders of my former company rapped to celebrate every corporate milestone. We’re compelled to <a href="https://poly-graph.co/vocabulary.html">quantify</a> what we love about it, and to somehow technologize it the same way Instagram did photography. Many have tried, myself included, but capturing hip-hop’s alluring qualities in an app is no simple task.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Authentic Design](https://www.smashingmagazine.com/2013/07/authentic-design/)
*   [Finding Better Mobile Analytics](https://www.smashingmagazine.com/2016/10/finding-better-mobile-analytics/)
*   [Design Better And Faster With Rapid Prototyping](https://www.smashingmagazine.com/2010/06/design-better-faster-with-rapid-prototyping/)
*   [100 Obscure and Remarkable CD Covers](https://www.smashingmagazine.com/2009/05/100-obscure-and-remarkable-cd-covers/)

I am here to talk about <strong>the unique challenges of designing a hip-hop app</strong> as I led design for one of the few successful apps in this space. This article shares insights from our research and design process, and the lessons we learned about the DAU of hip hop.

{{% feature-panel %}}

<strong>DAU</strong> (noun) Daily active users (DAU) is one of the ways to measure success in an internet product. DAU measures the “stickiness” of an online product — how many unique users interact with a product daily.</p>

<strong>Hip-hop</strong> (noun) If you got to ask, you ain’t got it.

I should warn you: this is not strictly an article about technical innovations. My focus is how an awareness of complex cultural issues can be critical for good app design.</p>

## The Underwhelming World Of Rap Apps

A few years ago I joined <a href="https://www.smule.com/">Smule</a> and became lead product designer for <a href="https://itunes.apple.com/us/app/autorap-by-smule/id524299475?mt=8"> AutoRap</a>. AutoRap works like this: you speak into your iPhone, and the app fits your words into a beat to create an instant rap song. It had enjoyed modest success as a novelty app, but had yet to live up to Smule’s goal of a collaborative musical platform. It was my job to reframe it as a tool people would use to make music together.

I looked around and <strong>found an unexpected profusion of rap apps</strong> with similar aspirations and seemingly no traction. I stopped counting at 20, but there are dozens more. Most of them fall into two groups: rap-insider apps, and tech-insider apps.

Rap-insider apps, like Rap Wars and Verses MC, overflow with enthusiasm for the genre but rarely prioritize technical execution. They tend to be buggy and lack functional clarity – one representative app has 20 different options at its top level of navigation. These options include tools to write lyrics, battle other people live, browse rankings, watch YouTube videos, and hang out in a “Cypher Video Lounge.”

Across these apps we also see frequent use of photorealistic microphone interfaces, seeking to capture real-world experiences in all of their richness and complexity, rather than adapting and simplifying them for mobile phones. There is much to appreciate, but it’s not difficult to see why these apps haven’t connected with larger audiences.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03adb426-50f1-48cb-9efa-798af34ad4b9/01-rap-insider-images-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ba81653-9e2c-49ad-8935-06e97b58d3f6/01-rap-insider-images-preview-opt.jpg" alt="Left to Right: Rap Wars and Verses MC" width="500" height="211" /></a><figcaption>Rap Wars (left) and Verses MC. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03adb426-50f1-48cb-9efa-798af34ad4b9/01-rap-insider-images-opt.jpg">View large version</a>)</figcaption></figure>

Tech-insider apps often look professionally designed and developed, display innovative technology, and completely miss the point.

Rhymeo stands out for its polished execution. It’s what it sounds like – an app that records you rhyming as a montage of pictures drifts by, and gives you a rhyming dictionary to make it easy. It wins on high-concept features and usability, but limits rapping to a rote exercise in rhyming at eerie stock photos. For an app dedicated to improvising music, it can feel a bit soulless. It includes an attractive Instagram-ish feed, but one can only listen to so many spoon-fed “rich” rhymes in one session.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c70d95-6b07-4c98-8e2a-d419b42cd3dd/02-tech-insider-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/634d24da-6ce1-485c-a8c1-c33208fd106b/02-tech-insider-preview-opt.png" alt="Left to Right: Rhymeo, Choke, and Rap Chat" width="500" height="328" /></a><figcaption>L–R: Rhymeo, Choke, and Rap Chat. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c70d95-6b07-4c98-8e2a-d419b42cd3dd/02-tech-insider-opt.png">View large version</a>)</figcaption></figure>

Choke lets you send out pre-written rap lyrics for friends to read aloud to see who “chokes” while delivering their lines. It looks nice, but for all of its slick minimalism and animations, there’s no real-life analog for this in hip-hop culture. It treats rapping as a cheap bar trick, and this comes across as out of touch.

RapChat delivers rap recordings in SMS-like format, and takes its inspiration directly from traditional messaging apps. This is a wasted opportunity, because it could have been imagined in a way that echoes real-life rap battles or cyphers, where participants take turns contributing verses. There is little in the app's original design to suggest that the developer was particularly invested in hip-hop. Its primary colors and utilitarian design would be appropriate for a voice memo app or text editor, but don’t inspire a great rapping performance. To their credit, they did improve their design substantially since the screenshot above was taken.

At this time, AutoRap lived somewhere in the tech-insider category. Its lush production value expressed genuine admiration for rap, but obviously came from a tech-savvy outsider’s perspective.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00a0667b-c09f-4630-8cd9-6f70ae277f9b/03-ar-old-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78ebbf79-30bb-45d3-93dd-a6b9182c5374/03-ar-old-preview-opt.png" alt="AutoRap in 2013" width="500" height="253" /></a><figcaption>AutoRap in 2013. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00a0667b-c09f-4630-8cd9-6f70ae277f9b/03-ar-old-opt.png">View large version</a>)</figcaption></figure>

The design mimicked what the original designers saw as hip-hop culture, but it didn’t accentuate the right details to appear authentic. I showed the app to someone active in the Bay Area rap scene and he recoiled, saying, “That’s not hip-hop, that’s just gangsta.” In other words, it played off of cheesy gang stereotypes at the expense of the music.</p>

## The Problem With Inauthenticity

AutoRap’s novelty attracted a wide range of people, but our demographic analysis generally pointed towards young men as the core. We never collected any data on race or ethnicity, but based on my personal interactions with the community, it’s safe to say that the representative power user was a black teenager, someone for whom most rap apps would seem like a presidential candidate abusing emoji to appear relatable.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1035e310-09ed-4d5e-8b89-11e49d181f8f/04-uncool-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1989b76-998e-4467-af9a-b37fe32eeae1/04-uncool-preview-opt.png" alt="Lame guys" width="500" height="396" /></a><figcaption>Don't be like these guys. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1035e310-09ed-4d5e-8b89-11e49d181f8f/04-uncool-opt.jpg">View large version</a>)</figcaption></figure>

It’s not surprising that the tech community might not have its finger on the pulse of black youth culture. Besides the well-publicized <a href="https://medium.com/@marksluckie/what-it-s-actually-like-to-be-a-black-employee-at-a-tech-company-e32bb222818b#.gylnzoqah">lack of black voices within companies</a>, there is an undeniable disconnect between the tech economy and people living outside of it. SoMa, the neighborhood that is home to most of San Francisco’s startups, feels strangely insulated from Oakland just across the bay, much less the gritty Tenderloin neighborhood across Market Street. Spending long hours at luxurious offices with catered meals, and living with other techies a short commute away from work, there are few opportunities to interact meaningfully with the artistic community, older people, poor people, or nearly anyone anywhere else in the world.

Isolation, intentional or not, fosters social blinders that can <strong>limit our ability to design for a broad audience</strong>. Tech understands cash, fame, and speed, but struggles to grasp the value of gifts, friendship or creative expression. I don’t want to moralize about my city’s culture war, so much as to say that isolationism is the wrong mindset from which to design great products for other people, especially those with different value systems.

Inauthenticity isn’t just a matter of sounding lame in front of teenagers. It can also raise serious ethical questions when it comes to appropriating the art form of a marginalized community. It’s only human for a developer to make an app inspired by music they love, but without an eye for authenticity it can come across like Tom Cruise starring in a Miles Davis biopic. Worse, rap sometimes emerges as a punchline to the app’s central conceit. “It’s like SMS, but with raps. How droll.” Even well-intended portrayals might inadvertently evoke racial stereotypes that many people outside of Silicon Valley would not appreciate. At a time when artists like Iggy Azalea routinely come under fire for using caricatured black mannerisms in a stage persona, it behooves us to tread lightly and treat our source material with respect.</p>

## Gonzo User Research

All of this led to a dilemma. I wanted to make a hip-hop app that would feel authentic, but I was (and still am) just another techie in San Francisco without personal connection to that world. My first step was to thoroughly review the history of rap music. I watched hours of YouTube videos of cyphers and battles, listened to several new albums a day for weeks, and read as much as I could. I also started rapping myself, albeit very poorly. A co-worker and I visited a cypher in Redwood City, where local teenagers would get together after school, go around in a circle, and take turns freestyling. We took detailed notes on how they improvised with each other, where they drew inspiration from, and what the music really meant to them.

I posted an ad on Craigslist: “Rappers Wanted.” Several rappers in the Bay Area volunteered to visit our office and give in-depth interviews with the team. We got one veteran rapper from Oakland who knew some big names from the 90s, and some younger aspirational rappers at the start of their careers. We would sit down with them and just talk casually about their music for an hour or two. We went in without scripts or questionnaires, or any of the usual paperwork or tools for design research. We just talked.

Significant insights emerged from these interviews, revealing important themes that rap apps typically miss. The rappers we spoke to most valued the strength of their individual creative voice. Rhyming and following a beat are important skills, but only when used in the service of self-expression. Tupac spits from the gut with absolute sincerity. GZA raps from his head. Doom is pure flow. Some rappers like Lil B and Young Thug produce music with meta-trite or unintelligible lyrics but still succeed by force of personality and the uniqueness of their sound. Everyone has to find their own message and style.

Developing a personal style can take years. Aspiring rappers spend vast sums of money on the equipment necessary to produce their art. Very rarely do they make it back, or even expect to. Rapping is also a deeply social activity, and many people use it as a way of bonding with their friends in a collaborative, supportive atmosphere. It’s everything the apps tend to miss.

When we showed our rapper consultants the existing app, they responded with a general tone of bemusement, and found polite ways to say that the app wasn’t quite for them. You may recall this quote from earlier: “That’s not hip-hop, that’s just gangsta.” We hadn't planned on a major redesign, but that moment of candor inspired us revisit the app’s identity on a broader scale.

## (Re)Designing The Definitive Rap App

We redesigned some of the tech to make the rapper’s voice feel more alive as they speak. The initial version used a visualizer composed of elaborate floral shapes that unfurled to audio input along predetermined patterns. It evoked the ornate flourishes of blackletter gang tattoos and the playful opulence of a rapper who insists on using gold-plated credit cards. It embodied a perception of rap as gaudy and entertaining, but neither expressive nor sophisticated under its surface.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f49cade-ce47-4810-bd80-4b4075cccea3/05-comparison-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d24b7d1-c0fc-417b-b5eb-1e6337c01430/05-comparison-preview-opt.png" alt="Visualizer Comparison" width="500" height="378" /></a><figcaption>AutoRap's recording screens, old (left) and new. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f49cade-ce47-4810-bd80-4b4075cccea3/05-comparison-opt.png">View large version</a>)</figcaption></figure>

We wanted to replace it with something simpler, but more modern and sincere. We created an equalizer that bubbles up and down responsively to visualize the full audio spectrum of a user’s voice. Each person’s voice takes on a unique shape, and it gives a sense of immediate, intimate feedback that your words are being heard.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27ed08d7-9e8f-4993-9c51-26df9123a80d/06-art-comparison-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58601cbc-3784-4bae-926c-17cbc8dc29a6/06-art-comparison-preview-opt.png" alt="Raw energy vs modern sophistication: the album art influences of AutoRap's old (left) and new (right) designs" width="500" height="122" /></a><figcaption>Raw energy vs. modern sophistication: the album art influences of AutoRap's old (left) and new designs. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27ed08d7-9e8f-4993-9c51-26df9123a80d/06-art-comparison-large-opt.png">View large version</a>)</figcaption></figure>

We stripped away the dense patterns and gold highlights in favor of a sleek look inspired by trends in contemporary hip-hop cover art. We wanted to portray hip-hop as it portrays itself. Hip-hop has moved from street crime to haute couture, art collection, and tech entrepreneurship. Oversized gold jewelry still has its place, but taste and sophistication have become equally important markers of success.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d57133d7-e18e-4ac9-8b6b-5c22f4fb5410/07-comparison-songbook-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16a40821-c83d-40ef-8fb4-55a22db96f69/07-comparison-songbook-preview-opt.png" alt="AutoRap Songbook Redesign" width="500" height="379" /></a><figcaption>Finding a more sophisticated look. Old (left) and new. (<a>View large version</a>)</figcaption></figure>

For copywriting and general branding purposes, we needed to give the app a strong voice. I drew up a tongue-in-cheek graph of famous rappers, plotted by their production value and lyrical complexity. The graph became useful in highlighting the generation of rappers we wanted to emulate most strongly. It became clear that the app needed to make the user feel like Kanye West: creative, bold, and a true individual in every sense. We wrote all of our copy in ALL CAPS, worked in wordplay and pop culture references at every opportunity, and when in doubt, asked ourselves what Kanye would say.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d7f393-32d6-4e7a-af36-3ea2a9ea3a42/08-rapgrid-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/064bb00e-764a-421e-8bb4-28fdcbc59b34/08-rapgrid-preview-opt.png" alt="A less than scientific look at rap music. Please don't take this seriously" width="500" height="355" /></a><figcaption>A less than scientific look at rap music. Please don't take this seriously. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d7f393-32d6-4e7a-af36-3ea2a9ea3a42/08-rapgrid-opt.png">View large version</a>)</figcaption></figure>

We downplayed the technical wizardry of the app and instead emphasized a sense of ownership over your music. We accomplished this through a suite of simple features like the ability to customize your song titles and make album art with a quick selfie; we later added the ability to remix your recording to different beats for greater creative control. Whereas most apps take it for granted that recordings exist as abstract digital entities, we packaged them as loosely skeuomorphic vinyl records that can be scratched and rewound with a touch – some<i>thing</i> delightful that you have just created.

Unlike apps like Rap to Beats, Rhymeo, or Choke, which give users rhyming dictionaries and scripts, we made the decision to never, under any circumstances, tell the user what to say. Once you start recording, you enter a word-free zone to avoid contaminating your flow. This makes the app intimidating to some, but it means that whatever you say is your own. AutoRap will act as your recording studio, producer and marketer, but you need to bring your own message. Compared to similar apps, AutoRap users generate an incredible amount of interesting and diverse original content, from buoyant <a href="https://www.smule.com/recording/midi-mafia-charger/237956304_59666803">swagger</a> to bawdy humor and <a href="https://www.smule.com/recording/midi-mafia-da-woods/189698290_60994360">flirtation.</a>

We did several rounds of user testing, including one intense session with a group of students at a local school. Much to our relief, everyone’s face lit up when they used the app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd4c3276-2066-42e4-aaa2-5ba43273f4c7/09-metrics-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96581b22-510c-437e-acaa-cf9c39ffe3a1/09-metrics-preview-opt.jpg" alt="Sparklines tracking key metrics in the months after the redesign. Labels are hidden for NDA compliance." width="500" height="140" /></a><figcaption>Sparklines tracking key metrics in the months after the redesign. Labels are hidden for NDA compliance. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd4c3276-2066-42e4-aaa2-5ba43273f4c7/09-metrics-opt.jpg">View large version</a>)</figcaption></figure>

We released the new design and saw a big lift in the number of recordings our users made. Our next step was to build out screens to feature rap songs from around the world. In addition to “like" and "share,” users can reply directly with their own impromptu raps inspired by what they heard. The original rapper can reply back, and before you know it there’s a rap battle under way. The app renders the audio from each reply together into a single seamless track, so that other people could listen in. We went on to create “rooms” for topical hashtags, modeled loosely after the real-world dynamics of a collaborative cypher. Extensive A/B testing increased the number of users who share their recordings to public screens. A network of small communities surfaced, comprising users who took the app seriously as a place to have creative fun and practice rapping with friends.</p>

## The Value Of Connecting To Your DAU

If you work in tech, I’m guessing you want to hear some numbers. As of now, about 50 million people worldwide have downloaded AutoRap. Every month our users start 7 million recording sessions. It’s well-rated in the App Store, and every now and then a song made with AutoRap goes viral. The app even makes a healthy amount of money. AutoRap has achieved a level of success well above every other app in this space. On the other hand, these metrics are only skin-deep, and have never impressed anyone I’ve spoken to outside of the tech industry. I doubt many of our users would care.

The real measure of AutoRap is whether it affords people meaningful creative access to the music they love. I see this as especially important for the members of our audience who the tech industry tends to chronically neglect or misunderstand. I have no way to quantify this aspect of the app, but it's only appropriate that the best way to gauge it is by listening to individual voices. To that end, I heard from one user that they couldn’t afford studio equipment to start their rap career, and AutoRap is letting them pursue their dream. Another said that the app helped them recover from surgery by keeping their spirits up. Every time I browse the app, I find new people pouring their souls into original pieces of music, often collaborating with other people they meet in the app. AutoRap is hardly a complete or finished project, but it is more than a novelty to many of its daily active users.

Looking back on this project, what stands out most is the value of approaching our users on their own terms and striving for authenticity. In other words, building empathy. Empathy has acquired buzzword status in tech, and often translates to a checkmark in someone’s process. This isn’t good enough. It’s important to break out of your comfort zone, especially in a place like SoMa, and speak directly, even intimately with other people who see the world differently.</p>

### Final Notes

I wrote in the first person as a matter of convenience. My collaborators deserve full credit: Oscar Corral for the visuals; Nick Kruge for the recording visualizer, vinyl, and ingenious animations throughout; Mike Allen for research and enthusiasm; and half a dozen engineers for giving the project life.

{{< signature "da, ml, og, il" >}}

