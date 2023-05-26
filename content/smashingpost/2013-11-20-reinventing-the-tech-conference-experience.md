---
title: Reinventing The Tech Conference Experience
slug: reinventing-the-tech-conference-experience
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1d66d9c-9f3e-430f-a788-237dc12689a4/illu-conf.jpg'
date: 2013-11-20T14:06:52.000Z
author: wesley-hales
description: >-
  If you had to name one thing that could have been better at the last
  conference or meetup you attended, what would it be? I bet you’d say that the
  **content or the interaction could have been better in some way**. I created
  [Onslyde](https://onslyde.com/#!/home) to solve this problem. It’s a free
  service and [open-source project](https://github.com/onslyde) that (hopefully)
  will make public speaking easier and conferences better.
categories:
  - Coding
  - Techniques
  - Conferences
  - Presentations
---
If you had to name one thing that could have been better at the last conference or meetup you attended, what would it be? I bet you’d say that the <strong>content or the interaction could have been better in some way</strong>. I created Onslyde to solve this problem. It’s a free service and <a href="https://github.com/onslyde">open-source project</a> that (hopefully) will make public speaking easier and conferences better.

The motivation for the project came from my own speaking engagements in the tech industry. I wanted to see how many people in the audience actually agreed or disagreed with what I was saying. I also wanted to leverage their experience and knowledge to create a better learning environment.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Upcoming Web Design Conferences](https://www.smashingmagazine.com/web-tech-front-end-ux-conferences/)
*   [How To Plan And Run A Great Conference Experience](https://www.smashingmagazine.com/2014/08/plan-and-run-a-great-conference/)
*   [Taking A Closer Look At Tech Conferences](https://www.smashingmagazine.com/2014/10/taking-a-closer-look-at-tech-conferences/)
*   [Smashing Conferences and Workshops](https://www.smashingmagazine.com/smashing-workshops/)

<strong>Presentations today are mostly unidirectional</strong>, with a single presenter giving information to the audience. But it doesn’t have to be that way. Now, with the ubiquity of mobile devices, everyone in the room can contribute to the conversation and make it better. Many books have been written on the topic of collective wisdom. In <a href="https://en.wikipedia.org/wiki/The_Wisdom_of_Crowds"><em>The Wisdom of Crowds</em></a>, James Surowiecki states:
<blockquote>"… a diverse collection of independently deciding individuals is likely to make certain types of decisions and predictions better than individuals or even experts."</blockquote>

{{% feature-panel %}}

For the past year, I have been putting this thesis to the test, enabling people to interact with and change the content that I deliver. It’s been a lot of fun and work, and now you get to see the result.</p>

## Ratings And Feedback

When we look at current systems of rating and feedback at conferences, most of them are reactive, meaning that participants rate the session after it’s over. This is why most <strong>people don’t even rate sessions, unless they are asked or forced to</strong> by the doorkeeper. Those who do rate sessions might not care to be accurate (giving all 5s or 4s and then hurrying to the coffee line). Other attendees might have enjoyed the majority of the talk, but then got upset by the last slide or by the way the speaker ended the talk.

If these people decided to rate the presentation, how many stars do you think they would give? Perhaps 3 or 4 stars because of their anger at the end, but who really knows? Without context, a low rating doesn’t tell the speaker which part of the talk an attendee didn’t like.

Real-time feedback gives context to a rating, making traditional feedback unnecessary. Conference organizers and speakers no longer have to rely solely on Twitter hash tags and reactive ratings to see how well things went. We can now visualize exactly how the audience felt at any millisecond of a presentation.</p>

### Real-Time Ratings With Onslyde

Giving a presentation that allows for real-time feedback is like riding a bicycle down a really steep hill for the first time. You have no idea whether you will crash and burn or come out with an adrenaline-filled scream at the other end. And it’s just as much fun for the audience.

With Onslyde, <strong>you get an accurate measure from the audience while you’re speaking</strong>. If you see that a lot of people are disagreeing with what you’re saying, you can adapt: Ask audience members for their thoughts, or maybe move on to another topic. When you’re presenting, actually seeing how the audience collectively feels in real time and then responding accordingly is a very cool experience.

The worst thing a presenter can do is tell the audience something it already knows or say something totally wrong. The audience wants to be intrigued and entertained by you. But too many speakers seem to think this requires GIFs of cats. Well, I don’t want to spoil anyone’s fun but I’m an adult now, and I don’t go to thousand-dollar conferences to look at funny pictures of cats. I do want to be able to challenge you, engage with the content and tell you when you’re wrong.

So, let’s talk about how the audience indicates whether you’re right or wrong. Onslyde’s remote control gives audience members between two and four ways to interact, depending on the type of session. It works for both normal presentations and panel discussions.

For presentations:

*   Any slide can be agreed or disagreed with.
*   Presenters can poll the audience by asking a question and giving two answers to choose from.
*   Remote devices are updated with content for each slide.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/521582c8-38ab-4895-8a7c-7e86edb7eb59/pres-remote-opt.png"><img loading="lazy" decoding="async" class="130231" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024e35e8-3cca-461b-bc9c-5aab3dd85514/pres-remote-250-opt.png" alt="pres-remote-250-opt" width="250" height="486" /></a>

For panel discussions:

*   Anyone (either panelist or audience member) can be agreed or disagreed with.
*   Votes are on a rolling average, meaning that they expire after 15 seconds (or a time specified by the moderator).
*   Any audience member can request to speak. This option will add them to a queue on the main screen.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d483d3ba-ce65-46ac-9e0c-567d5a88ec3c/panel-remote-opt1.png"><img loading="lazy" decoding="async" class="130234" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fcce840-05c2-4304-9359-b30c8897d357/panel-remote-250-opt.png" alt="panel-remote-250-opt" width="250" height="486" /></a>

<strong>All remote devices receive real-time updates</strong> based on the slide or current speaker. In individual presentations, the speaker can specify content or images to send to all remotes per slide. For example, if a bulleted list is on the current slide, you could send it to the remotes by adding <code>class="send"</code> to the markup:

<pre><code class="language-markup">
&lt;section class="slide"&gt;
    &lt;ul class="send"&gt;
    &lt;li&gt;Onslyde makes you a better presenter.&lt;/li&gt;
    &lt;/ul&gt;
&lt;/section&gt;
</code></pre>

We’ll go over the technical details in the next section. For now, note how easy it is to broadcast markup to everyone’s remotes.

<a href="https://edgeconf.com/">Edge Conf</a>, hosted at Google’s New York office in October 2013, was the first time ever when the audience participated in real time (via Onslyde) during an entire conference.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c02f7aa-9ec0-4884-b82f-7028dd6f24ae/edge1-panel-detail-large-opt.png"><img loading="lazy" decoding="async" class="130237" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87903181-c2a8-402a-a9d1-c794f9fe0a37/edge1-panel-detail-500-opt.png" alt="edge1-panel-detail-500-opt" width="500" height="479" /></a>

### What If There’s No Wi-Fi?

At this point, you might be thinking that this is a cool idea, but what about the 99% of conferences that have shaky or no Wi-Fi connectivity?

A presentation will work with or without an Internet connection; however, with no connection, it will just be like a normal presentation, and the audience would not be able to interact.

If you have a smartphone with a tetherable data plan, <strong>you can tether your laptop and enable Onslyde to connect from a mobile phone</strong>. It might sound crazy, but the lightweight messages that are sent across the wire still allow the presentation to run smoothly.

Even if Wi-Fi at a conference is unstable, the audience can always connect to the presentation with their mobile device’s data plan. I’ve personally given six or seven presentations with Onslyde and haven’t run into any issues so far.

Below you can see the network statistics from a talk I gave earlier this year. Even though the conference had stable Wi-Fi, attendees were connecting through their mobile data plan:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6824d42-ab74-4e54-9d11-bf7d873b5167/visits-by-provider-opt.png"><img loading="lazy" decoding="async" class="130242" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6824d42-ab74-4e54-9d11-bf7d873b5167/visits-by-provider-opt.png" alt="visits-by-provider-opt" width="426" height="388" /></a>

Some have suggested <a href="https://github.com/onslyde/onslyde/issues/32">bringing SMS into the picture</a>, as a fallback. This would enable attendees to vote by sending text messages to the server. If you have other ideas, please leave them in the comments!

## Building An Interactive Presentation

The Onslyde framework plugs into any HTML-based presentation system. For now, it supports presentations written with the following:

*   RevealJS,
*   Impress.js,
*   [Bespoke.js](https://markdalgleish.com/projects/bespoke.js/),
*   plain HTML.

Currently, there is no nice WYSIWYG tool for building a slide deck. A tiny bit of HTML knowledge is required to build a presentation, but that’s it — no JavaScript or other programming. This is good because you don’t have to log into the system to edit your deck minutes before going on stage. <strong>You can change the markup at any time</strong>, and you will be ready to present after refreshing the browser.

The following use cases show how to add interactive elements to a presentation.</p>

### Audience Members Vote on (i.e. Agree or Disagree With) Any Slide

This comes out of box, no set-up required. Onslyde is built around “slide groups.” “Agree” and “Disagree” votes can only be given once in a slide group. This lets you focus on a particular topic with multiple slides and not be bombarded with votes on each screen.

<pre><code class="language-markup">
&lt;section class="slide-group"&gt;
    &lt;section class="slide"&gt;
        &lt;p&gt;Onslyde makes you a better presenter.&lt;/p&gt;
    &lt;/section&gt;
&lt;/section&gt;
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d61c1d2f-990f-4b51-98ac-f0b770652715/buttons-opt.png"><img loading="lazy" decoding="async" class="130245" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d61c1d2f-990f-4b51-98ac-f0b770652715/buttons-opt.png" alt="buttons-opt" width="300" height="273" /></a><br>
<em>The buttons above will become active once the presenter moves to a new slide group.</em>

### Ask Unlimited Questions With Two Answers

To create an onscreen poll, use the following markup:

<pre><code class="language-markup">
&lt;section class="slide-group"&gt;

    &lt;section class="slide" data-option="master"&gt;
        &lt;h3 class="send"&gt;
        What is your favorite JavaScript framework?
        &lt;/h3&gt;
    &lt;/section&gt;

    &lt;section class="slide" data-option="jquery"&gt;
        &lt;div class="send"&gt;
        Time to talk about jQuery!
        &lt;/div&gt;
    &lt;/section&gt;

    &lt;section class="slide" data-option="querySelector"&gt;
        &lt;div class="send"&gt;
        Let’s go into more detail about core JavaScript!
        &lt;/div&gt;
    &lt;/section&gt;

&lt;/section&gt;
</code></pre>

By adding the markup above to your presentation, the bar chart in the following image will be automatically created and populated as votes are submitted:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f402fd3-d460-44d0-af69-a8c2f4ec5464/favorite-javascript-framework-large-opt.png"><img loading="lazy" decoding="async" class="130247" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/641ea877-a598-46ef-8cc5-2d6e298aece6/favorite-javascript-framework-500-opt.png" alt="favorite-javascript-framework-500-opt" width="500" height="391" /></a>

The buttons at the top will illuminate on the remote controls, and attendees may start voting:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35729b7d-5b18-42c7-800f-e6dbef6e7336/start-voting-opt.png"><img loading="lazy" decoding="async" class="130251" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35729b7d-5b18-42c7-800f-e6dbef6e7336/start-voting-opt.png" alt="start-voting-opt" width="235" height="300" /></a>

### Send Content to All Devices at Any Time

Notice how the remote control’s image shows the title of the poll? As mentioned, this is because we added <code>class="send"</code> to the parent element of the heading.

<pre><code class="language-markup">
&lt;section class="slide"&gt;
    &lt;h3 class="send"&gt;
    What is your favorite JavaScript framework?
    &lt;/h3&gt;
…
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84ccd8ae-21f6-4322-9a0a-eb57251ca0ce/start-voting-2-opt.png"><img loading="lazy" decoding="async" class="130253" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84ccd8ae-21f6-4322-9a0a-eb57251ca0ce/start-voting-2-opt.png" alt="start-voting-2-opt" width="219" height="300" /></a><br>
<em>The sent markup will appear below the button options.</em>

You can also send something completely different than what is shown by the projector. Instead of sending the title of the poll, you could send the names of other JavaScript libraries for attendees to research:

<pre><code class="language-markup">
&lt;section class="slide"&gt;
    &lt;h3&gt;
    What is your favorite JavaScript framework?
    &lt;/h3&gt;

    &lt;div class="none"&gt;
        &lt;ul class="send"&gt;
        &lt;li&gt;Zepto&lt;/li&gt;
        &lt;li&gt;xui&lt;/li&gt;
        &lt;li&gt;…&lt;/li&gt;
        &lt;/ul&gt;
    &lt;/div&gt;
</code></pre>

### Raffle or Giveaway: Random Selection of Audience Member

To me, one of the funnest parts of this tool is giving away swag at the end of a talk. You can randomly select anyone who is connected by adding the following link to your slide deck:

<pre><code class="language-markup">
&lt;a href="javascript:onslyde.slides.roulette()"&gt;Pick a winner&lt;/a&gt;
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e5560c-1602-4b5c-a12c-f7b54eb1e51e/winner-opt.png"><img loading="lazy" decoding="async" class="130256" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e5560c-1602-4b5c-a12c-f7b54eb1e51e/winner-opt.png" alt="winner-opt" width="154" height="300" /></a>

Just place the link on the final slide and click it at the end of your talk. Everyone’s mobile device will flash red; then, the winner’s will turn yellow. Continue clicking to pick more people at random.</p>

## Best Practices

The easiest way to get started with each feature is to focus on how you want the audience to interact with you and your content. Here are some good rules of thumb that I have learned using this tool:

*   **Start each presentation with a poll on the first or second slide.**.  This allows the audience to get their device ready, get connected and start giving their opinion. It’s fun to pose a controversial question about your presentation topic and watch the votes pour in.
*   Polls can solicit a “Yes” or “No” feeling from the audience or go deeper. If you ask a question like, “Which JavaScript framework do you use?” and then give options for “AngularJS” or “Backbone”, you will be able to fork the slides. This is why preparing the slides beforehand is more rewarding. Onslyde will detect the majority vote, and when you go to the next slide, the losing slides will be removed from the presentation (temporarily) and only the slides from the winning option will be shown.</p>

## Getting Started

Presentations can be created at onslyde.com. And the <a href="https://github.com/onslyde/server">open-source back end</a> that manages a presentation’s feedback is hosted on GitHub. Anyone can run the server and host their own instance of the entire Onslyde stack if they wish.

All of the features mentioned are integrated in each demo to show use cases. To begin your first presentation, go to the “Getting Started” section, where you will have the option to run a demo presentation or sign in and create a private one.

<img loading="lazy" decoding="async" class="130258" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cf54964-2542-4647-a54e-a9235db0bfee/onslyde.getting-started-500-opt" alt="onslyde.getting-started-500-opt" width="500" height="327" /><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97cd663d-ff37-41b3-9aad-ba74eb95b81c/onslyde.getting-started-opt">Large view</a>)</em>

After you’ve signed in, the “Getting Started” page will give you options for setting up a poll. After hitting the “Preview” button, you must save the HTML to your computer in order to edit and present the slides.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9238ce98-6a30-4bf9-b3dd-5419940a72e7/setting-up-large-opt.png"><img loading="lazy" decoding="async" class="130263" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06fb0017-56c8-4b02-8933-3b90310ff637/setting-up-500-opt.png" alt="setting-up-500-opt" width="500" height="290" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9238ce98-6a30-4bf9-b3dd-5419940a72e7/setting-up-large-opt.png">Large view</a>)</em>

An Onslyde presentation can be run anywhere. Essentially, it’s the same as saving a Keynote or PowerPoint presentation on your computer. Just click on the HTML file and run it from a Web browser — no need to install anything or run it from a server.</p>

### Regarding Keynote and PowerPoint

For those of you who use non-HTML slide decks, such as Keynote and PowerPoint, there are plans to create a <a href="https://github.com/onslyde/onslyde/issues/31">transparent overlay</a> on top of Windows and Mac OS X. This will allow presenters to use any presentation tool and to collect feedback in real time.</p>

## Understanding Audience Feedback

After your talk is over, you can view the analytics for your session. The votes for each slide are recorded so that you can track your performance at a fine-grained level.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b674e03f-9667-43c5-a00f-9e3e278e0734/chart1-large-opt.png"><img loading="lazy" decoding="async" class="130267" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b0d9cf-a42a-4274-93f4-f53ba7ca017c/chart1-500-opt.png" alt="chart1-500-opt" width="500" height="252" /></a>

For questions that the audience voted on, each option is recorded, along with the “Agree” and “Disagree” votes for each poll.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2305814-1048-4e80-9adc-2a61e41f9981/chart2-large-opt.png"><img loading="lazy" decoding="async" class="130270" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e83253a-f32f-44b6-a50f-e234740dc967/chart2-500-opt.png" alt="chart2-500-opt" width="500" height="226" /></a>

The other important pieces of data come from Google Analytics, including engagement times and what kinds of devices and mobile networks were used.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7c7ab06-1c57-4f90-a7e9-276ddb638097/analytics-large-opt.png"><img loading="lazy" decoding="async" class="130294" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9291ed5-171d-4f5a-b5e2-f58b56543a69/analytics-500-opt.png" alt="analytics-500-opt" width="500" height="549" /></a><br>
<em>Google Analytics showed that real-time feedback was provided not just from the people in the room. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7c7ab06-1c57-4f90-a7e9-276ddb638097/analytics-large-opt.png">Large view</a>)</em>

From the above image, we can see that 281 iOS devices and approximately 113 Android devices were used at Edge Conf. Because the event was streamed live, over twice as many unique devices appeared as there were people in the room — people were participating and providing real-time feedback <strong>as they watched the live stream from their home or office</strong> around the world!

One other cool piece to this analytics puzzle is mapping voting times to the video. Edge Conf was streamed live, and the videos were subsequently added to YouTube. After finding a reference point in the video and calculating the starting time, we were able to map the charts to the videos. If you clicked on any data point from a session, the video would skip to that voting period. Try it out for yourself.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c343bc71-c1b6-43c7-8c7c-e533d387167f/voting-period-large-opt.png"><img loading="lazy" decoding="async" class="130278" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d85e34-1939-44d3-8507-4636e14e3abb/voting-period-500-opt.png" alt="voting-period-500-opt" width="500" height="286" /></a><br>
<em>We were able to map the voting times to the conference videos. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c343bc71-c1b6-43c7-8c7c-e533d387167f/voting-period-large-opt.png">Large view</a>)</em>

## Conclusion

As we’ve seen, so much more valuable data can be pulled from the conferences we attend. Not only can we get an accurate snapshot of how speakers performed and how audience members felt, but <strong>we can change the learning experience for everyone</strong>.

This project is a use case for the mobile Web and a playground for the new technologies that are available to modern Web browsers, such as WebSockets and WebRTC. Many other companies and conferences provide similar services using native apps and proprietary hardware, but the convenience of opening a Web browser and being exposed to a new level of education and interaction is immeasurable.

Many thanks to <a href="https://twitter.com/triblondon">Andrew Betts</a> for helping me with this article and providing great feedback. He is also responsible for most of the features in the Onslyde panel and remote interfaces.

{{< signature "al, ea" >}}

