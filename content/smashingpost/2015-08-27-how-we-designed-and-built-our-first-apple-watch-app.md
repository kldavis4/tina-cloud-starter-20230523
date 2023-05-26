---
title: How We Designed And Built Our First Apple Watch App
slug: how-we-designed-and-built-our-first-apple-watch-app
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2debd18-5175-41fe-8add-5bc674fa5c48/00-excerpt-opt.png'
date: 2015-08-27T20:25:30.000Z
author: alex-komarov
description: >-
  One sunny morning in the summer of 2014, I was sitting in a café having just
  finished an hour-long call with my remote team. Scheduling that call had been
  a messy exercise: we live in different time zones and it was hard to find a
  time that worked for everyone. I wanted to make dealing with **time zone
  differences** less painful.

  I had some free time on my hands, so I pulled my notebook out and started
  playing around with an **iWatch app** idea. Yeah, you read that right — 2014
  and iWatch, before a watch had ever been announced.
categories:
  - Coding
  - Mobile
  - Apps
  - Devices
  - iOS
---
One sunny morning in the summer of 2014, I was sitting in a café having just finished an hour-long call with my remote team. Scheduling that call had been a messy exercise: we live in different time zones and it was hard to find a time that worked for everyone. I wanted to make dealing with **time zone differences** less painful.

I had some free time on my hands, so I pulled my notebook out and started playing around with an **iWatch app** idea. Yeah, you read that right — 2014 and iWatch, before a watch had ever been announced.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

<ul>
 	<li><a title="Read 'Intimate And Interruptive: Designing For The Power Of Apple Watch'" href="https://www.smashingmagazine.com/2015/10/intimate-interruptive-designing-power-apple-watch/" rel="bookmark">Intimate And Interruptive: Designing For The Power Of Apple Watch</a></li>
 	<li><a title="Read 'myMail App Case Study: Developing For Apple Watch Without The Device'" href="https://www.smashingmagazine.com/2015/08/mymail-app-case-study/" rel="bookmark">Developing For Apple Watch Without The Device</a></li>
 	<li><a title="Read 'How To Think Like An App Designer'" href="https://www.smashingmagazine.com/2015/04/thinking-like-an-app-designer/" rel="bookmark">How To Think Like An App Designer</a></li>
 	<li><a title="Read 'Designing For Smartwatches And Wearables To Enhance Real-Life Experience'" href="https://www.smashingmagazine.com/2015/02/designing-for-smartwatches-wearables/" rel="bookmark">Designing For Smartwatches And Wearables </a></li>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c82aa60e-c255-40f4-94c3-fda31fd3be59/01-first-drawing-opt-small.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c82aa60e-c255-40f4-94c3-fda31fd3be59/01-first-drawing-opt-small.png" alt="A sketch I made the day it all started" /></a><figcaption>A sketch I made the day it all started. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c82aa60e-c255-40f4-94c3-fda31fd3be59/01-first-drawing-opt-small.png">View large version</a>)</figcaption></figure>

{{% feature-panel %}}

<p>Since it was early August 2014, we had no idea what shape an iOS watch would take, let alone its name. But we learned a month later, when <a href="https://itunes.apple.com/us/podcast/apple-special-event-september/id275834665?i=318848187&amp;mt=2">Apple announced</a> the new wrist-worn device it had been secretly working on: Apple Watch. We started with the problem — making time zones easier to handle — and learned a lot along the way, including a surprise we received at the very end. It’s a story with an unexpected ending.</p>

## Our Screwed-Up Way Of Measuring Time

<p>The way people measure time is screwed up, and there’s little we can do about it. Most of us have ten fingers. We count to ten in pre-school. One meter is one hundred centimeters, there are a hundred pennies in a dollar, and so on. Our brains have been trained for and are constantly reminded of the decimal system. In fact, many of us don’t think there’s any other way to count: 9+9 is always 18. Until we start measuring time.</p>

<p>We count hours using a duodecimal (base 12) numbering system. And count minutes using a sexagesimal (base 60) system. Our brain is trained to think that 9+9=18. But in the world of time, 9+9=6. It’s unnatural.</p>

<p>We’re using systems and techniques that are thousands of years old. The role of time in society has changed, the technology has changed, yet the imperfect system lives on. This system makes time-related calculations very hard — more so when you have to hop over 12 while counting. Most people, including me, can’t do these calculations quickly and reliably.</p>

## Our Original Problem: Time Zones

<p>We wanted to solve a headache our new world of interconnectivity created. With the internet and mobile, communication has become really easy; so easy that people all over the world can now chat, work, and play as if they’re in the same room. Except they aren’t: the earth is still round, it still spins, and that creates <strong>the problem of time zones</strong>.</p>

<p>While some people are sipping their morning coffee, others have to run off to collect their kids from school, and some are already asleep.</p>

<p>Our team and our clients are distributed across five continents. We have to deal with a half-dozen time zones on a daily basis, which can be a nightmarish experience: calls in the middle of the night, frustration, missed deadlines, broken communication, lost opportunities.</p>

<blockquote><strong>Pop Quiz:</strong> Is there any reasonable time for a phone call between US West Coast, Eastern Europe, and Australia? Answer: No, there isn’t. Someone always has to suffer.</blockquote>

<p><strong>We wanted to make time zones easier for ourselves.</strong> Multiple clocks began appearing on our dashboards, we scheduled meetings in advance, and we started using the calendar more smartly. But even with multiple clock faces, for instance, you could see the current time, but it was still tricky to predict what 8pm locally meant for everyone else across the world.</p>

<ul>
   <li>If you wanted to call someone come (your) morning, would they still be awake wherever they are?</li>
   <li>Would your iOS developer in Russia be available to answer questions if you needed to pull them into your conference call between Australia and the US West Coast at 3pm Pacific?</li>
</ul>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01ff65b7-ef7d-46db-b013-0ec5d8f440f4/03-24-hour-app-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a5f64a0-6af8-4e3b-9d6e-986585b88481/03-24-hour-app-opt-small.png" alt="Author’s dashboard with multiple time zones and names of people who live in these timezones." /></a><figcaption>Author’s dashboard with multiple time zones and names of people who live in these time zones. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01ff65b7-ef7d-46db-b013-0ec5d8f440f4/03-24-hour-app-opt.png">View large version</a>)</figcaption></figure>

## First Solution: World Clock App For Mac OS X

<p>To solve this time zone problem, we started with a World Clock app for Mac OS X. It allows you to quickly convert time by dragging a shadow over a world map. While you drag, all clocks will adjust their time according to the position of the shadow. To find a suitable time, just keep dragging until one of the clocks shows the time you want.</p>
<figure class="video-container"><iframe loading="lazy" width="500" height="353"]https://vimeo.com/136205638" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>World Clock for Mac OS X in action.</figcaption></figure>

We loved using the app ourselves and were blown away by how well it was received in the Mac community. (At one point we reached #9 top paid app in the US.)</p>

### World Clock Widget

<p>For some people the World Clock app was too dense. They just wanted to convert times quickly. Having an entire window with clocks was overwhelming. So we made a separate app that added a Notification Center widget to your Mac. The World Clock widget also received a warm welcome. People then began asking for an iPhone version. But making one wasn’t as straightforward as we thought it would be.</p>
<figure class="video-container"><iframe loading="lazy" width="318" height="308"]https://vimeo.com/136312851" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>World Clock widget for Mac OS X in action.</figcaption></figure>

### Struggle With The Mobile Version

<p>We solved the time-conversion problem for big screens, but everything we tried for smaller devices never felt quite right. We noticed others started trying solve this problem for mobile as well. (For example <a href="https://miranda-app.com">Miranda</a> and <a href="https://jaredsinclair.com/timezones/">TimeZones</a>). While the apps looked sexy and well thought-out, they were still too complicated.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c7cb49-737e-4e87-8b18-98abbd5f4cc2/06-24-hours-ios-concepts-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/981c3b0f-9a93-44b1-843c-5d251f6b7c03/06-24-hours-ios-concepts-opt-small.png" alt="“24 hours” for iOS concept" /></a><figcaption>“24 hours” for iOS concept. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c7cb49-737e-4e87-8b18-98abbd5f4cc2/06-24-hours-ios-concepts-opt.png">View large version</a>)</figcaption></figure>

To be honest, we didn’t have any better ideas, so we put the iOS World Clock concept in the bottom drawer and focused on other projects. And then something interesting happened.</p>

<p>At <a href="https://minimuminc.com">Minimum</a> we sometimes use <em>the principle of intensifying the conflict:</em> make the contradiction 10, 100, 1000 times more intense than the original problem. This forces us to look at the problem in a completely different way and often helps us find unusual solutions.</p>

<p><strong>Example:</strong> We need to make cars use less gas → We need to make cars use zero gas.</p>

### “Wrist-First” Approach Distilled Our Thinking

<p>We were stuck until <a href="https://moto360.motorola.com">Moto 360</a> came along, and Apple Watch rumors started to leak. That’s when I started playing around with a wrist-worn version of our World Clock Mac OS X app. The original problem of shrinking our Mac app to the size of an iPhone <em>intensified:</em></p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627c5651-77a8-4e47-a4a6-2d2e6f44b4f6/07-shrinking-mac-app-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66984fde-c629-4821-a790-f3b11d788770/07-shrinking-mac-app-opt-small.png" alt="07-shrinking-mac-app-opt-small" /></a><figcaption>From the Mac to the Apple Watch. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/627c5651-77a8-4e47-a4a6-2d2e6f44b4f6/07-shrinking-mac-app-opt.png">View large version</a>)</figcaption></figure>

It became abundantly clear that we couldn’t just massage the app to fit a tiny watch screen. <strong>All our iPhone concepts were compromises.</strong> Cut a corner here, nudge a thing or two there. Maybe it will fit, maybe it won’t, maybe it will still be useful… That’s why it didn’t feel right. Compromises never do. There had to be something simpler.</p>

## Second Solution: “24 Hours” App For iPhone And Apple Watch

<p>Ironic cliché: the solution was staring at us the entire time. Have a look at the icon of our World Clock Mac app. Multiple hands on one clock face can elegantly show times at different locations with minimal user interaction. That made sense. The only problem was the twelve-hour clock face: if we see a hand pointing at 3 o’clock, is it 3am or 3pm?</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb15cc80-dcd2-464c-87bd-69ea4a80ecc3/08-world-clock-icon-opt.png" alt="World Clock Mac icon" /><figcaption>World Clock Mac icon.</figcaption></figure>

To avoid confusion we decided to use a 24-hour clock face: the top half for day, the bottom for night. Easy, clear and obvious.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ec67cb3-3f62-4299-8d08-bf184b496b14/09-24-hour-face-concept-opt-small.png" alt="24-hour clock face concept for “24 hours” app" /><figcaption>24-hour clock face concept for “24 hours” app.</figcaption></figure>

### The Trade-Off

<p><em>Remember, our goal was not to reinvent the clock</em> or make a better one; we just wanted to make telling and converting international times easier. We decided that using a 24-hour face was a fair trade-off: it’s not as familiar as a 12-hour clock face. People would have to get used to it, but they’d have a much easier way of telling and converting times once they did. We decided this was fair.</p>

<p>Was it the right decision? We hope so. Let us know what you think <a href="https://itunes.apple.com/us/app/24-hours-global-time-simplified./id969635117?mt=8">in comments</a> after you’ve had a chance to play with the app.</p>

### Prototyping Phase 1: Before Apple Watch Release

<p>How do you design for a product that doesn’t exist yet? Since we started before Apple Watch was ever announced, we decided to prototype on an iPhone. We agreed on using a circular clock face for our prototype so we could scale it down for a smaller screen should an “iWatch” be released. This would fit a rectangular or circular watch face — since we had no idea which it might be.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/938043ff-443f-46a3-b5ad-0ac653e06a1f/10-early-whiteboard-sketches-opt-small.png" alt="Early whiteboard sketches of “24 hours”" /><figcaption>Early whiteboard sketches of “24 hours”.</figcaption></figure>

The first thing we wanted to test was our interaction model. The idea was that a user would rotate the clock hands in a circular swipe motion to convert time. But would that be comfortable to use? We created two interaction options.</p>

<ol>
<li>A user rotates the clock face itself while panning in a circular motion (clock hands stay put).</li>
<li>A user rotates the clock hands while the face stays put.</li>
</ol>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e67c23a1-ea83-4dcc-841d-1f556311c3f5/12-prototype-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0156ca0-41c1-4b00-aa15-b9a58ff29d7f/12-prototype-opt-small.png" alt="“24 hours” prototype with rotating clock face (the original build of the app was lost)." /></a><figcaption>“24 hours” prototype with rotating clock face (the original build of the app was lost). (<a href="">View large version</a>)</figcaption></figure>

Although the face seemed easier to reach and rotate, especially with one thumb, we felt rotating the hands made more sense. We’re used to clock hands being mobile while clock faces stay put. Familiar often equals intuitive.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c319bb10-c2ce-44da-a6aa-0024b4dc9554/13-map-view-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93178d27-d4a1-420f-83f7-3cc17108ac6c/13-map-view-opt-small.png" alt="Map view makes one-thumb interactions easier" /></a><figcaption>Map view makes one-thumb interactions easier. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c319bb10-c2ce-44da-a6aa-0024b4dc9554/13-map-view-opt.png">View large version</a>)</figcaption></figure>

To make interactions with one thumb even easier, we decided to add a map view below the clock face: it illustrates the geography of the cities, shows night and day, and pans left and right with one thumb. We felt we’d landed on a good solution. And then September rolled around.</p>

### External Factor #1: iPhone 6 Is Released

<p>iPhone 6 was beautiful — and black. We liked how the screen became virtually indistinguishable from the hardware, so we decided to switch our gamma to black to support this effect.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c3e50a-3a2e-4795-8b5a-f460bf7a300b/14-colour-switch-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/743dc7a9-0242-49d6-be67-f63d52553654/14-colour-switch-opt-small.png" alt="14-colour-switch-opt-small" /></a><figcaption>Switching to black. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c3e50a-3a2e-4795-8b5a-f460bf7a300b/14-colour-switch-opt.png">View large version</a>)</figcaption></figure>

### External Factor #2: Apple Watch Gets Announced

<p>We were really happy about the Watch when we finally saw it. (Who wouldn’t be?) We were glad we’d started planning an app for it so early, and felt prepared to make something awesome by the time Apple Watch went on sale. But it was hard to stop calling it <em>iWatch</em>.</p>

<p>Our most important takeway was that Apple Watch would have a rectangular-shaped screen. That clarified a lot in our plans. We carefully examined every piece of UI we could find in the keynote, press reviews and Apple’s website. Among other things, we noticed its native world clock:</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e11ca581-6fed-442f-9393-1b9089830d23/15-world-clock-feature-opt.png" alt="Images from Apple’s website showcasing Apple Watch world clock feature" /><figcaption>Images from Apple’s website showcasing Apple Watch world clock feature.</figcaption></figure>

Seeing that was good news: it didn’t come close to what we were trying to achieve. You couldn’t see more than two times at once, and <em>it was impossible to convert time</em> (or even compare times) at different locations.</p>

#### Using The Crown

<p>The Apple Watch crown really excited us. We couldn’t imagine a better user interface for a world-clock app: people are already used to twisting the crown to rotate watch hands. What could be simpler! Only now there would be more than two hands.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2c79c9c-5b70-445a-a6cd-698d0319df9c/16-sketch-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d361315d-b041-4900-b591-30d7334f41cf/16-sketch-opt-small.png" alt="16-sketch-opt-small" /></a><figcaption>Sketch made September 10, 2014. (Author lives in Australia so it was September 9 in California.) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2c79c9c-5b70-445a-a6cd-698d0319df9c/16-sketch-opt.jpg">View large version</a>)</figcaption></figure>

Apple Watch also started to influence our iOS version. (Note “+” and calendar buttons in the corners.)</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7ec93b8-4419-40e8-8ba2-a49553592eaa/17-apple-watch-influences-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8296964a-765d-432b-aacc-a534b52204a6/17-apple-watch-influences-opt-small.png" alt="17-apple-watch-influences-opt-small" /></a><figcaption>Influences from Apple Watch appear in the iOS version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7ec93b8-4419-40e8-8ba2-a49553592eaa/17-apple-watch-influences-opt.png">View large version</a>)</figcaption></figure>

### First Tests With External Users

<p>Bad news: almost everyone looked at the iOS prototype above and assumed that the clock face they saw was a normal 12-hour face clock. After looking closer they would notice that numbers 12 and number 6 repeat twice. That would get them completely confused. Clearly, we needed to make our 24-hour face different, to make it obvious and self-explanatory. At least we hoped so.</p>

<p>With a 12-hour clock face it would have been incredibly hard to differentiate between AM or PM for any given time. Jakarta and Palo Alto would appear to be only two hours apart on 12-hour face, even though the time difference between these two cities is 14 hours.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97feb79d-bd6d-4d40-a046-9c57a3e93985/18-night-day-opt.jpg" alt="A sketch for our 24-hour clock face with day and night differentiated" /><figcaption>A sketch for our 24-hour clock face with day and night differentiated.</figcaption></figure>

To make our 24-hour clock face look different from a 12-hour one, we decided to put more stress on the difference between night and day. We debated this for a while, until I found this interesting and beautiful artifact that somewhat validated our design idea:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df507bbe-1d20-431a-820a-b049eecceb6b/19-globe-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae2cbe15-1120-4338-b66b-ce86a2b4bdb1/19-globe-opt-small.png" alt="A globe with a 24-hour clock face" /></a><figcaption>A globe with a 24-hour clock face. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df507bbe-1d20-431a-820a-b049eecceb6b/19-globe-opt.jpg">View large version</a>)</figcaption></figure>

Adding night/day separation not only helped us make our clock face more distinguishable from a 12-hour face, it made our overall UI more obvious and self-evident. This modification changed our users’ reactions during subsequent tests. Now when they saw the app for the first time, they realized immediately they were dealing with an unusual clock. That made them pay more attention in the beginning, and allowed them to quickly grasp the app’s core concept.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/091c0919-c582-438a-9b18-4430a23c18e3/20-24-hour-clock-face-night-day-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd60dc4f-4a3b-470f-91f6-f4c53bae515b/20-24-hour-clock-face-night-day-opt-small.png" alt="24-hour clock face with and without night and day separation" /></a><figcaption>24-hour clock face with and without night and day separation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/091c0919-c582-438a-9b18-4430a23c18e3/20-24-hour-clock-face-night-day-opt.png">View large version</a>)</figcaption></figure>

We made a few more prototypes to ensure we definitely wanted to rotate the clock’s hands and not the face. With the night/day separation, rotating the clock face felt strange and made us dizzy. We were definitely going ahead with moving hands.</p>
{{< vimeo id="136205584" caption="Rotating face belongs in a flight simulator, not on someone’s phone or watch." >}}

### Challenges Of The Tiny Apple Watch

<p>Since we started prototyping before an Apple Watch even existed, our original plan was to scale down our iOS design. But the Apple Watch turned out to be tiny. We couldn’t just shrink our existing UI.</p>

<p>We skipped every odd digit on the clock face, made the type more legible, and, most importantly, abbreviated all city/time zone names to three letters. (We started with airport codes. If there wasn’t one available, we abbreviated using the first letter, the second consonant and the third consonant. Yekaterinburg would be YKT, Winnemucca would be WNN, Ubud UBD, and so on.)</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c20ea0aa-0618-4737-9730-fc90839ee9be/22-shrinking-ui-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2e000fb-9171-45aa-b5e7-dbf5dd3d18cf/22-shrinking-ui-opt-small.png" alt="Shrinking UI is never a good strategy when porting your product to smaller devices" /></a><figcaption>Shrinking UI is never a good strategy when porting your product to smaller devices. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c20ea0aa-0618-4737-9730-fc90839ee9be/22-shrinking-ui-opt.png">View large version</a>)</figcaption></figure>

We’ve spent a ridiculous amount of time trying to find the best way to display information between the night and day edges. We’re not ecstatic about the result yet, but we feel it’s reasonably good. (We’re open to your ideas!) Let us know in comments if you have any other ideas for us to try. Here are some of our iterations:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f240685-b9a0-492d-9234-cc519db70c8a/23-finding-best-way-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a2735cc-d9f4-49f0-935c-e1022960d636/23-finding-best-way-opt-small.png" alt="Trying to find the best way to present information between night and day" /></a><figcaption>Trying to find the best way to present information between night and day. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f240685-b9a0-492d-9234-cc519db70c8a/23-finding-best-way-opt.jpg">View large version</a>)</figcaption></figure>

### Prototyping Without Apple Watch

<p>Since the Apple Watch wasn’t out in the world yet, we strapped iPhones to our wrists. This prototype had the correct Apple Watch measurements. Playing with the prototypes was fun. At one point we got carried away with additional functions: adding clocks, a map, calendar events — all of which can theoretically be done on your Apple Watch.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfa3d264-5eb6-4034-a5f1-d2ad474bf891/24-trying-on-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68051124-a99a-419f-8cf5-738306a46b26/24-trying-on-opt-small.jpg" alt="“Trying on” Apple Watch" /></a><figcaption>“Trying on” Apple Watch. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfa3d264-5eb6-4034-a5f1-d2ad474bf891/24-trying-on-opt.jpg">View large version</a>)</figcaption></figure>

### The Release Of The Apple Watch Kit

<p>Around December 2014, Apple’s Watch Kit was released, and it was very limited. I mean, very. That’s when we found out that all animations would have to be generated on a paired iPhone, and then sent to Apple Watch frame by frame. We didn’t find any sign of crown control or any kind of gesture support. We assumed Apple would make these available later. We moved forward with a few iterations.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ead532fa-24e4-46ef-9f9a-e6acfe3e6936/25-iteration-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3f820d-6e3b-4f40-a5f7-462d84b3d1a1/25-iteration-opt-small.png" alt="25-iteration-opt-small" /></a><figcaption>Iterations on the UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ead532fa-24e4-46ef-9f9a-e6acfe3e6936/25-iteration-opt.png">View large version</a>)</figcaption></figure>

#### Converting Time

<p>When a user twisted the crown, or spun the clock hands, time would shift from “Now” to the future or the past.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab0857da-b833-4b84-ac04-66fd332674e3/26-converted-time-state-ui-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dfe99f6-9143-4a63-b780-43cf65657488/26-converted-time-state-ui-opt-small.png" alt="26-converted-time-state-ui-opt-small" /></a><figcaption>Converted time state UI without accounting for color blindness. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab0857da-b833-4b84-ac04-66fd332674e3/26-converted-time-state-ui-opt.png">View large version</a>)</figcaption></figure>

#### Accounting For Color Blindness

<p>This future/past addition created a new problem: green and red wouldn’t work very well for people who have color blindness. If you were color-blind, red and green could become yellow and gray; you could still distinguish between the two, so you could tell whether you converted time forward or backwards, but we felt that it wasn’t elegant and could be confusing.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaaf9467-78f5-4725-adcd-b55ce12c1860/27-color-blindness-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e274bb2-cffa-4f36-8f4e-8931c73b97cf/27-color-blindness-opt-small.png" alt="Accounting for color blindness in “24 hours” for Apple Watch" /></a><figcaption>Accounting for color blindness in “24 hours” for Apple Watch. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaaf9467-78f5-4725-adcd-b55ce12c1860/27-color-blindness-opt.png">View large version</a>)</figcaption></figure>

Blue and red for forward and backwards seemed to work much better in the case of a color-blind person using the app: for all three kinds of color blindness, blue remained mostly blue, and red was either gray or still red. Either one did a good job illustrating that a user had moved to the past.</p>

<p>Progressing from new concept to completed design:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1571ea9d-6aee-4ecb-a33a-d30faf75186e/28-progressing-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d886dd20-3cb3-4ca4-8ee3-d5dc2106b5a8/28-progressing-opt-small.png" alt="28-progressing-opt-small" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1571ea9d-6aee-4ecb-a33a-d30faf75186e/28-progressing-opt.png">View large version</a>)</figcaption></figure>

Accounting for various iPhones screen sizes and getting ready to ship:</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d14412b7-2da8-4b0f-b6e2-7e53d6b9801d/29-various-sizes-opt.png" alt="29-various-sizes-opt" /><figcaption></figcaption></figure>

### Working Around Apple Watch Kit Constraints

<p>Here’s how we saw our “perfect” product at the time:</p>
<figure class="video-container"><iframe loading="lazy" width="500" height="281" src="https://www.youtube.com/watch?v=9i6QPFRwODI" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<figure class="video-container"><iframe loading="lazy" width="500" height="281" src="https://www.youtube.com/watch?v=VFbidKX0cOM" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

#### Crown Wasn’t Yet Available To Third-Party Developers

<p>Newer versions of Watch Kit didn’t show any sign of crown control, so we had to come up with something that would work in the meantime. We decided to try swiping/panning gestures:</p>

<figure class="video-container"><iframe loading="lazy" width="500" height="281" src="https://www.youtube.com/watch?v=UofrNRTOKpU" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<p>We quickly realized that swiping also wasn’t yet available to third-party developers. We played around with more ideas: how about we add back and forward buttons so a user can just tap to control the app? It hurt our eyes, but it seemed better than nothing:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba1987d-e6e3-4d10-a85b-0daaf6ca1956/30-color-blindness-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88156add-8b03-4c59-bb0d-e0cab9f0c30b/30-color-blindness-opt-small.png" alt="Adding forward and backward buttons to the UI" /></a><figcaption>Adding forward and backward buttons to the UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba1987d-e6e3-4d10-a85b-0daaf6ca1956/30-color-blindness-opt.png">View large version</a>)</figcaption></figure>

### Time To Ship Something

<p>We realized that Watch Kit probably wouldn’t be updated soon enough for us to fully realize the potential of our concept in time. We needed to ship something before Apple Watch went on sale so we worked with what was available. That’s what you sign up for when you are trying to be among the first delivering a product on a completely new platform.</p>

<p>[<strong>Update:</strong> <a href="https://www.apple.com/au/watchos-2-preview/?cid=wwa-au-kwg-watch-com">Watch OS 2.0</a>, announced on WWDC in June 2015, allows crown-control for third-party apps.]</p>

<p>Next, we built our prototype on Apple Watch. However, we couldn’t quite make it as smooth as we wanted it to be: at the time, frame animations couldn’t be generated and transferred from an iPhone to Apple Watch quickly enough. This caused lags and slow reactions to touch:</p>
<figure class="video-container"><iframe loading="lazy" width="500" height="375" src="https://www.youtube.com/watch?v=dvS7nGRvZ4s" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<p>Eliminating animations didn’t seem to improve things. The app was still too slow to react on user interaction:</p>
<figure class="video-container"><iframe loading="lazy" width="500" height="281" src="https://www.youtube.com/watch?v=S6G3NaIu2dU" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

### Shipping

<p>At this point we decided to temporarily turn off the time-conversion feature on our Apple Watch version. Our iOS version would be used to its full potential while Apple Watch could be used to <em>just tell times</em> at different locations.</p>

<p>At this point it was mid-March 2015. The Apple Watch release was imminent, and we really wanted to be among the first people who made apps for it. So we uploaded the build to iTunes, clicked “Submit for Review,” and waited.</p>

<p>Here’s the final product we developed.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b10eb5e-a226-417d-ba7a-0cd88e9acd4d/31-apple-version-opt.png" alt="“24 hours” app for iPhone and Apple Watch" /><figcaption>“24 hours” app for iPhone and Apple Watch.</figcaption></figure>
{{< vimeo id="136205639" >}}

#### Unexpected Rejection

<p>The Apple team must have been on the lookout for apps that offer Apple Watch support because it didn’t take them long to reject our build:</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5639fae8-451d-4347-b850-0904a33e7da1/34-rejected-version-opt.png" alt="34-rejected-version-opt" /></figure>

<p>We’re used to rejections, but this one was pretty unusual and surprising: “Apps that contain a clock face, or a likeness of a clock [will be rejected].”</p>

<p>Long story short: after a bunch of back and forth with the review team we decided to put the Apple Watch version of our app on hold and released the iOS-only version for the time being.</p>

### Releasing iOS-only Version (For Now)

<p>We stripped our iOS app of Apple Watch support and submitted again. This time it was approved.</p>

<p>“24 Hours” is <a href="https://itunes.apple.com/us/app/24-hours-global-time-simplified./id969635117?mt=8">now available on iTunes</a>. We love it and use it every day. And we’re really interested to know what you think about it. I couldn’t imagine a better tool for convertingand viewing international times. Oh, wait, I can: an Apple Watch version of “24 Hours.”</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e98b68ca-1594-4026-94ad-ee5148634673/32-24-hour-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fc2e925-ba53-45d3-a5d2-de9c6e361e38/32-24-hour-app-opt-small.png" alt="32-24-hour-app-opt-small" /></a><figcaption>“24 Hours” is a simple and powerful world clock. No more counting across time zones, no more calling at odd hours of the night. “24 Hours” keeps track for you. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e98b68ca-1594-4026-94ad-ee5148634673/32-24-hour-app-opt.jpg">View large version</a>)</figcaption></figure>

## Final Thoughts

<p>As I mentioned before, when you are trying to bring something new to life, there are risks and uncertainties associated with it. It’s a part of the game. We were aware of these risks and decided to take a shot anyway. We don’t regret it. History shows us that Apple products become more open over time. A few examples from an iOS world:</p>

<ul>
   <li>iPhone 1 didn’t even have third-party apps when it was first released.</li>
   <li>You used to not be able to build custom keyboards for iOS.</li>
   <li>Swift wasn’t open source.</li>
   <li>There were no extensions and no APIs that now give third-party apps more control than ever before.</li>
</ul>

<p>We believe that Apple Watch will follow the same path: it will gradually become more open, allowing third-party developers to build apps that are greater than ever before. And when that happens, we will be ready.</p>

<p>P.S. During this time we did develop a successful Apple Watch app: <a href="https://itunes.apple.com/us/app/chat-center-universal-way/id886643270?ls=1&amp;mt=8">Chat Center</a>. Apple also gave us tremendous support with this, and it was approved. So in the end we did get one product in for the Apple Watch launch.</p>
{{< vimeo id="136205583" >}}

<p><em>Thank you to everyone who made “24 Hours” and our other world clock apps possible: <a href="https://twitter.com/alxndrustinov">Alexander Ustinov</a>, Graphic/UI designer; <a href="https://twitter.com/_Foboz">Misha Nikanorov</a>, iOS and Mac development; and Nikita Yermolayevs (advisor).</em></p>

<p><em>I also want to take this opportunity to thank the Apple Developer Relationship team for all their help and support.</em></p>

{{< signature "da, ml, og" >}}

