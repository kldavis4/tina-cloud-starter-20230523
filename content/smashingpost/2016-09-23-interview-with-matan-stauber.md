---
title: Stretching The Limits Of What’s Possible
slug: interview-with-matan-stauber
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b4e5c4c-7780-45f1-afe8-ee640e003282/histography-opt.png
date: 2016-09-23T18:36:36.000Z
author: cosima-mielke
description: >-
  **Designing with “big data”** is a challenging task. Matan Stauber, however,
  took it to the next level. With an impressive outcome. Having studied Visual
  Communication at _Bezalel Academy of Art and Design_, Israel's national school
  of art, Matan realized a very ambitious final project: an interactive timeline
  of our galaxy's history — 14 billion years, from the Big Bang to today.

  We talked to Matan about _Histography_, about the idea behind it, and how he
  managed to bring it to life. An interview about stretching the limits of
  what's possible.
categories:
  - Design
  - Interviews
---
**Designing with "big data"** is a challenging task. Matan Stauber, however, took it to the next level. With an impressive outcome. Having studied Visual Communication at _Bezalel Academy of Art and Design_, Israel's national school of art, Matan realized a very ambitious final project: an interactive timeline of our galaxy's history — 14 billion years, from the Big Bang to today.

We talked to Matan about [Histography](https://histography.io/), about the idea behind it, and how he managed to bring it to life. An interview about stretching the limits of what's possible.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaee4a16-22ba-4849-9a0a-797579016f8f/matan-stauber-large.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b815dec5-09eb-426b-95d5-a9c6d32a8d82/matan-stauber.jpg" width="200" height="200" alt="Matan Stauber" align="right" style="margin: 0 0 1.5em 1.5em" /></a></figure>

**Q: Matan, what's the idea behind Histography and how did it come to be?**

**Stauber:** Timelines are one of the most popular ways of visualizing history, but they are limited to a specific time period. Histography is an interactive timeline that allows viewers to explore all of history, across **14 billion years of history**, all the way back to the Big Bang. The site draws historical events from Wikipedia and self-updates daily with newly recorded events. Every dot in Histography represents a historic event, along with videos, articles, and images. Viewers can adjust to any time range, from decades to billions of years, and even compare historic events using different categories, such as war and inventions in the Middle Ages.

{{% feature-panel %}}

For a while before creating Histography, I was interested in Wikipedia and how a redesign of it could look like. One of the features I had in mind was a view where all of Wikipedia's events are arranged on a historical timeline. Since Wikipedia contains events from every time period we know (from this current year to the Big Bang), a timeline of all Wikipedia events is a timeline of all history as we know it. I found this concept to be so exciting that it quickly became the brief for the entire project.

<figure><a href="https://histography.io/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9c369d4-ff3d-41d7-97ca-b64f642fe335/histography-website-small-opt.png" width="500" height="286" alt="Screenshot of the Histography website" /></a><figcaption><a href="https://histography.io/">Histography</a> visualizes all of known history in an interactive timeline. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c81fa9c6-735d-45c0-812b-53af30a76d22/histography-website-large-opt.png">View large version</a>)</figcaption></figure>

**Q: How does Histography work from a technical perspective?**

**Stauber:** I created a system that scans Wikipedia, searching for historic events, indexing them, and trying to determine how important each one is. For every event the system then asks Google for an image, YouTube for a video, and Wikipedia for an article.

Imagine telling a person: "Go to every Wiki page you can find. Every time you come across a date and you think it's a historic event, write it down. For each of them go to Google and ask for a photo and to YouTube and see if there is a relevant video, and give each one a rating score of 1–100\. Events with a Wiki page will get a higher score as events without. Longer and popular articles will get higher scores as short and unpopular ones."

The reason behind the rating system is that there were a lot of very niche historic events that are probably not relevant to most people. My first experience with Histography was exploring for a very long time before I could find events I could relate to. The solution was to **promote the more "important" events**, the ones people are writing and talking about. You can't really tell, but every time you move your cursor, the system tries to pick the more interesting event out of the events in the radius around your cursor.

{{< vimeo id="182397647" caption="As you hover over the dots, Histography picks the most interesting event from the radius around your cursor." >}}

**Q: Could you explain what is going on behind the scenes the moment a user has selected a timeframe?**

**Stauber:** Every time you select a timeframe, the system constructs a new graph layout. Each column in this new layout **can represent anything between months to millions of years** (depends on how big your selected timeframe is).

The next step is that each of the thousands of dots on the screen gets its own new location. Every millisecond or so, the system runs through all of the dots and moves each of them slightly closer to their new location. This is what drives the animation. Because each dot has it's own speed, it feels as if the particles come flying in, not like a robotic movement.

When I started thinking about how to design such a timeline, one that can support billions of years and thousands of events, the main concern was proportions. The series "The Cosmos" once calculated that if you place all of the galaxy's history on a one-year calendar, all of human history will fill the last second of that calendar. I knew that in order to create a timeline of all history, it cannot be limited to a specific period. It will need to be able to show events on different scales and to **allow people to focus on a single year as well as billions of them**. Trying to answer that required many different design concepts and explorations — from 3D timelines to Matryoshka-type designs, and going back to the drawing book time after time.

<figure><div class="aspect-ratio"><iframe loading="lazy" src="https://player.vimeo.com/video/182394549" frameborder="0" allowfullscreen></iframe></div><figcaption>A nice detail: When you change the timeframe, new events, represented by dots, come flying in dynamically.</figcaption><figure>

<p><strong>Q: Please describe the process of building this mammoth project: Where did you start? What were the first steps you took?</strong></p>

<p><strong>Stauber:</strong> It started by trying to map all the different types of existing timelines, if it's in a printed newspaper or displayed in a museum. I wanted to know what binds timelines to a specific period and what I can do differently so a timeline of all history would be possible.</p>
<p>The next step was taking a notebook and starting to draw ideas and concepts. Most of them were useless, but every once in a while there was a drawing that made me think "Oh, this might actually work."</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39d1d89f-13a8-47d8-a16b-29909746d9ff/timeline-concept-sketch-2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc161690-535e-46c6-8d97-a5453cd37a01/timeline-concept-sketch-2-small-opt.png" width="500" height="332" alt="Timeline concept sketch" /></a><figcaption>How does one build a timeline of all of history? Matan tinkered with a lot of concepts before settling on one. Here one of his early sketches. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39d1d89f-13a8-47d8-a16b-29909746d9ff/timeline-concept-sketch-2-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b449e4d-1db1-41d1-aa85-5abc7c412893/histography-live-timeline-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f331a324-067f-43d7-a59c-e0f6417bcff6/histography-live-timeline-small-opt.png" width="500" height="97" alt="The timeline in use on Histography" /></a><figcaption>The timeline now in use on Histography. It lets you select a timeframe yourself, or you can choose a certain period, e.g. the Iron Age. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b449e4d-1db1-41d1-aa85-5abc7c412893/histography-live-timeline-large-opt.png">View large version</a>)</figcaption></figure>

<strong>Q: What were the challenges you had to master along the way?</strong></p>

<p><strong>Stauber:</strong> A big problem was navigation. How do you navigate between billions of years to a specific one? The slider at the bottom of the page allows viewers to adjust the time period they would like to see. You could jump to a specific period, like the Iron Age, or choose a custom one. It's designed in a way that the <strong>"sensitivity" of it changes</strong> as you move from one period to another. For example, if you are looking at -3.7 billion years and move the slider a bit, the next one would be -3.6 billion (100 million years). But if you are looking at 1937, the next one would be 1938 (one year). It's basically an exponential function, the further you are in time, the shorter the steps will be.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa8e1fe7-2598-4a1b-824d-9f1c28c6a5dc/slider-sensitivity-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be7f8a81-072e-4e97-a3a5-27dd38a30467/slider-sensitivity-small-opt.png" width="500" height="219" alt="Sensitive sliders" /></a><figcaption>To make navigating through 14 billion years of history as convenient as possible, Matan made the slider sensitive. Here a sketch of the concept. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa8e1fe7-2598-4a1b-824d-9f1c28c6a5dc/slider-sensitivity-large-opt.png">View large version</a>)</figcaption></figure>

<strong>Q: What techniques and tools did you use to build Histography? Were there any existing libraries you could rely on to ease the job or did you have to build everything from scratch?</strong></p>

<p><strong>Stauber:</strong> A lot of notebook sketches. I like designing in Bohemian Sketch and Adobe Illustrator. The Code in Histography is CSS, Javascript and WebGL (running on Pixi) for all events flying in on the screen. <a href="https://www.pixijs.com/">Pixi.js</a> is a great library for 2D graphics using the powerful WebGL. The rest is mostly made from scratch. I'd say that I recommend using WebGL only when you have complex graphics. For most projects, CSS will give you great results in a shorter time.</p>

<p><strong>Q: How long did the project take to build?</strong></p>

<p><strong>Stauber:</strong> Histography was created in four months (end to end) as my final student project at the Bezalel Academy of Arts and Design.</p>

<p><strong>Q: Did Histography turn out as you expected it or were there sacrifices you had to make?</strong></p>

<p><strong>Stauber:</strong> One idea that I really liked and had to sacrifice was having another view that can present all of the historic events on a global map. When doing data visualization, there is sometimes a gap between the ideas we have and the actual data. In this case, the data just didn't contain location for most of the historic events I had.</p>

<p><strong>Q: Were there things you wish you'd done differently, both in terms of design and code?</strong></p>

<p><strong>Stauber:</strong> Not differently, but there are many sides to Histography I would like to expand. For example, all the data I'm using comes from the English Wikipedia (which is the biggest data source) and in many ways this information represents the Western view of history. I would love to see how a Chinese or Arab Histography looks like.</p>

<p><strong>Q: Did you have any inspiration for this project?</strong></p>

<p><strong>Stauber:</strong> I'll typically try to find inspiration outside the field I'm currently working on. If I'm doing graphic design, I'll look at industrial design, architecture and such. In the case of Histography, some of the things that really opened the way I think about history came from natural history museums and history-related exhibitions.</p>

<p><strong>Q: Where do you see information design heading?</strong></p>

<p><strong>Stauber:</strong> There is a lot of discussion about "big data" and for a good reason: We have never harvested and stored such a vast amount of information and never in history was this information so accessible to the general public. The question is: <strong>What can we do with all of this data?</strong> I think we will see more and more projects trying to find ways to make information on large scales more approachable.</p>

<p><strong>Q: Are there any examples of data visualization you can point us at that inspire you or which, in your opinion, get things right?</strong></p>

<p><strong>Stauber:</strong> There is a great project called "<a href="https://number27.org/wefeelfine">We Feel Fine</a>" by Jonathan Harris that scans Twitter for tweets starting with "I feel&hellip;". The result is an interactive map of human emotion from all around the globe. </p>

<p><strong>Q: Last, but not least: Do you have a piece of advice you'd like to share with our readers?</strong></p>

<p><strong>Stauber:</strong> Big data and infographics in general, like other areas of design, are about storytelling. <strong>It's about the story of your data</strong>, and as such, it has to be coherent. A common mistake is to try to communicate too many ideas. There are too many infographics that are beautiful but simply too complex to understand. My advice would be to think of the first glimpse of your project and what story it tells.</p>

<p><em>Thank you, Matan, for offering us a deeper look into your work! We're already curious what you will come up with in the future.</em></p>

{{< signature "il" >}}

