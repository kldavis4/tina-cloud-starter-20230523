---
title: 'Introducing RAIL: A User-Centric Model For Performance'
slug: rail-user-centric-model-performance
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dee7fcc2-a3b4-4091-bc30-9b68fb3703dc/rail-intro.png'
date: 2015-10-02T16:40:10.000Z
author: paulirishpaullewis
description: >-
  There’s no shortage of **performance advice**, is there? The elephant in the
  room is the fact that it’s **challenging to interpret**: Everything comes with
  caveats and disclaimers, and sometimes one piece of advice can seem to
  actively contradict another. Phrases like “The DOM is slow” or “Always use CSS
  animations” make for great headlines, but the truth is often far more nuanced.
categories:
  - Coding
  - Performance
  - Strategy
---
There’s no shortage of <strong>performance advice</strong>, is there? The elephant in the room is the fact that it’s <strong>challenging to interpret</strong>: Everything comes with caveats and disclaimers, and sometimes one piece of advice can seem to actively contradict another. Phrases like “The DOM is slow” or “Always use CSS animations” make for great headlines, but the truth is often far more nuanced.

Take something like loading time, the most common performance topic by far. The problem with loading time is that some people measure <a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index">Speed Index</a>, others go after first paint, and still others use <code>body.onload</code>, <code>DOMContentLoaded</code> or perhaps some other event. It’s rarely consistent. When it comes to other ways to measure performance, you’ve probably seen enough JavaScript benchmarks to last a lifetime. You may have also heard that 60 FPS matters. But when? All the time? Seems unrealistic.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)
*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

Very few of us have unlimited time to throw at optimization work, far from it, and we need criteria that help us decide what’s important to optimize (and what’s not!). When all is said is done, we want and need clear guidance on what “performant” means <strong>to our users</strong>, because that’s who we’re building for.

{{% feature-panel %}}

On the Chrome team, we’ve been thinking about this, and we’ve come up with a model to put the user right back in the middle of the performance story. We call it the <strong>RAIL</strong> model.

If you want the <strong>TL;DR</strong> on RAIL to share with your team, here you go!

*   RAIL is a [model](#rail-perf-model) for breaking down a user’s experience into key actions (for example, tap, drag, scroll, load).
*   RAIL provides performance [goals](#rail-perf-goals) for these actions (for example, tap to paint in under 100 milliseconds).
*   RAIL provides a structure for thinking about performance, so that designers and developers can reliably target the highest-impact work.

Before diving into what RAIL involves and how it could be helpful in your project, let’s step back and look at where it comes from. Let’s start with every performance-minded person’s least favorite word in the whole wide world: “slow.”

## “Slow”

Is changing the DOM slow? What about loading a <code>&lt;script&gt;</code> in the <code>&lt;head&gt;</code>? JavaScript animations are slower than CSS ones, right? Also, does a 20-millisecond operation take too long? What about 0.5 seconds? 10 seconds?

<figure class="fwi"><a href="/wp-content/uploads/2015/09/img-slow.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bd84ae5-80d9-4ac4-8806-d0f239fa2079/rail-slow-cloud.png" alt="What does slow mean?" width="500" height="375" /></a><figcaption>What does slow really mean?</figcaption></figure>

While it’s true that different operations take different amounts of time to complete, it’s hard to say objectively whether something is slow or fast without the <em>context</em> of when it’s happening. For example, code running during idle time, in a touch handler or in the hot path of a game loop each has different performance requirements. Put another way, the people using your website or app have different <strong>performance expectations</strong> for each of those contexts. Like every aspect of UX, we build for our users, and what <em>they</em> perceive is what matters most. In fact, number one on <a href="https://www.google.com/about/company/philosophy/">Google’s ten things we know to be true</a> is “Focus on the user and all else will follow.”

Asking “What does slow mean?,” then, is really the wrong question. Instead, we need to ask “<strong>What does the user feel</strong> when they’re interacting with the things we build?”

## Putting The User In The Center Of Performance

Luckily for us, there’s long-standing academic HCI research on this topic, and you may have seen it before in <a href="https://www.nngroup.com/articles/response-times-3-important-limits/">Jakob Nielsen’s work on response time limits</a>. Based on those thresholds, and adding an extra one for animations (because it’s 2015 and we all love a bit of showbiz), we get the following:

*   **100 milliseconds**.  Respond to a user action within this time window and they will feel like the result is immediate. Any longer and that connection between **action and reaction** breaks.
*   **1 second**.  Within this window, things feel part of a natural and continuous progression of tasks. Beyond it, the user will lose focus on the task they were performing. For most users on the web, loading a page or changing views represents a task.
*   **16 milliseconds**.  Given a screen that is updating 60 times per second, this window represents the time to get a single frame to the screen (Professor Math says `1000 ÷ 60 = ~16`). People are exceptionally good at tracking motion, and they dislike it when their expectation of motion isn’t met, either through variable frame rates or periodic halting.

These perception thresholds are great because they give us the building blocks we need. What we need to do next is map them to reality. Let’s consider a typical interaction that our users have:

In that brief session were a number of distinct interactions:

*   waiting for the page to load,
*   watching an animation,
*   scrolling the page,
*   tapping an icon,
*   watching the navigation animate open,
*   waiting for the page to load,
*   watching an animation,
*   scrolling the page.

Labeling those actions from the video would give us something like this:

<figure class="fwi"><a href="/wp-content/uploads/2015/09/img-user-journey-breakdown.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d122b4da-40b5-4469-a24b-68ecc68a23b1/img-user-journey-breakdown.png" alt="A breakdown of the user's journey into RAIL segments" /></a><figcaption>(<a href="/wp-content/uploads/2015/09/02-user-journey-breakdown-opt.jpg">View large version</a>)</figcaption></figure>

Each of those color blocks represents a type of action, and you can see that there are four of them. And there are four letters in RAIL. Curious.

Here’s another user journey that we can break down and label, this time from <a href="https://voice-memos.appspot.com">Voice Memos</a>:

We can break down user interactions and categorize them into four distinct areas. At Google, we call these areas <strong>RAIL</strong>, and each comes with its own performance goals, which are based on the human perception thresholds we just saw.</p>

<figure class="fwi"><a href="/wp-content/uploads/2015/09/img-pauls.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fdff37f-4944-44a2-88db-eda4ce8cbfbf/rail-paul-irish-paul-lewis.png" alt="Pauls Irish and Lewis" /></a></figure>

## The RAIL Performance Model

RAIL stands for response, animation, idle and load.

These four distinct areas are a way to reason about the actions in your websites and apps. If you optimize based on each area’s performance goals (which we got from those perception thresholds), then your users will be very happy.</p>

<figure class="fwi"><a href="/wp-content/uploads/2015/09/img-rail.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbea4880-df37-4c72-892b-f55a913fc8e1/rail-response-animation-idle-load.png" alt="RAIL Performance Model" /></a></figure>

Let’s look at each one in detail.</p>

### 1. Response

If a user clicks on a button, you have to respond to their click before they notice any lag. This applies to any input, really, whether it’s toggling a form control or starting an animation. If it doesn’t happen in a reasonable window of time, then the <strong>connection between action and reaction breaks</strong> and the user will notice.

Response is all about input latency: the lag between the finger touching the glass and the resulting pixels hitting the screen. Have you ever tapped on something and it took so long to respond that you started wondering whether it registered your tap? That’s <em>exactly</em> the kind of thing we want to avoid!

Response’s primary interaction is:

*   **tapping** — when the user taps or clicks on a button or icon (for example, tapping a menu icon to open off-screen navigation).

To respond responsively, we would:

*   provide feedback in **less than 100 milliseconds** after initial input.
*   Ideally, the feedback would show the desired state. But if it’s going to take a long time, then a loading indicator or coloring for the active state will do. The main thing is to acknowledge the user so that they don’t start wondering whether their tap was registered.</p>

### 2. Animation

Animation is a pillar of modern apps, from scrolling to view transitions, and we must be judicious with what we do in this period of time, because the user will often be interacting directly and will really notice if the frame rate varies. However, the user expects very smooth feedback for more than what falls under the classic definition of animation.

Animation includes the following:

*   **visual animation**.  This includes entrance and exit animations, tweened state changes, and loading indicators.
*   **scrolling**.  This refers to when the user starts scrolling and lets go and the page is flung.
*   **drag**.  While we need to respond to the user’s interaction in under 100 milliseconds, animation might follow as a result, as when panning a map or pinching to zoom.

To animate properly, each frame of animation should be completed in <strong>less than 16 milliseconds</strong>, thereby achieving 60 FPS (<code>1 second ÷ 60 = 16.6 milliseconds</code>).</p>

### 3. Idle

Creating apps that respond and animate well often requires deferment of work. The <a title="True Lies Of Optimistic User Interfaces" href="https://www.smashingmagazine.com/2016/11/true-lies-of-optimistic-user-interfaces/">Optimistic UI</a> patterns leverage this technique to great effect. All sorts of work that must be completed likely does not <em>need</em> to happen within a critical time window in the same way as “response” or “load”: Bootstrapping the comments functionality, initializing components, searching and sorting data, and beaconing back analytics data are all non-essential items that we can do when the browser is idle.

To use idle time wisely, the work is grouped into blocks of about 50 milliseconds. Why? Should a user begin interacting, we’ll want to respond to them within the 100-millisecond response window, and not be stuck in the middle of a 2-second template rendering.</p>

### 4. Load

Page-loading time is a well-trodden area of performance. We’re most interested in getting the user to the <strong>first meaningful paint quickly</strong>. Once that’s delivered, the <strong>app must remain responsive</strong>; the user mustn’t encounter trouble when scrolling, tapping or watching animations. This can be super-challenging, especially when much of the work for a page shares a single thread.

To load pages quickly, we aim to deliver the first meaningful paint in under 1 second. Beyond this, the user’s attention starts to wander and the perception of dealing with the task at hand is broken. Reaching this goal requires prioritizing the <a href="https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=en">critical rendering path</a> and often deferring subsequent non-essential loads to periods of idle time (or lazy-loading them on demand).</p>

## Performance Goals

Performance is essentially the art of avoiding work. And when it’s unavoidable, make any work you do as efficient and well timed as possible.

With the stages of RAIL interaction laid out, let’s summarize the goals:
<table class="article-table four-columns"><br>
<tbody>
<tr>
<th>Response</th>
<th>Animation</th>
<th>Idle</th>
<th>Page Load</th>
</tr>
<tr>
<td>Tap to paint in <strong>less than 100 milliseconds</strong>.</td>
<td>Each frame completes in <strong>less than 16 milliseconds</strong>.</td>
<td>Use idle time to proactively schedule work.</td>
<td>Satisfy the “response” goals during full load.</td>
</tr>
<tr>
<td></td>
<td>Drag to paint in <strong>less than 16 milliseconds</strong>.</td>
<td>Complete that work in <strong>50-millisecond chunks</strong>.</td>
<td>Get first meaningful paint in <strong>1,000 milliseconds</strong>.</td>
</tr>
</tbody>
</table>

### A Note on Measurement

Here are a few handy tips on measuring your project’s performance profile:

*   Measuring these on a MacBook Pro or comparable machine (which many of us designers and developers have) won’t give a representative idea of your mobile users. Common phones can be over ten times slower than a desktop!
*   A **Nexus 4** is a good middle-of-the-road device to use.
*   **“Regular 3G”** is recommended for network throttling.
*   Also, look at your analytics to see what your users are on. You can then mimic the 90th percentile’s experience for testing.</p>

### What About Battery and Memory?

Delivering on all of the goals above but leaving the user with 10% battery and 0% available memory <em>isn’t</em> putting the user first.

We’re not yet sure how to quantify being a responsible citizen of the shared resources, but RAIL may some day get a B (for battery) and an M (for memory), turning into BLAIMR, PRIMAL or something else equally fun and memorable.</p>

## Business Impact Of RAIL

Many of us do what we do because we love building awesome things. We don’t work in a vacuum, though, and sometimes we have to make the business case to managers, stakeholders and clients to be able to prioritize performance as part of the user experience.

Luckily, many large companies have shared numbers that help us make our case:

*   Google: [2% slower = 2% less searching per user](https://assets.en.oreilly.com/1/event/29/Keynote%20Presentation%202.pdf)
*   Yahoo: [400 milliseconds faster = 9% more traffic](https://www.slideshare.net/stoyan/dont-make-me-wait-or-building-highperformance-web-applications#btnNext)
*   AOL: [Faster pages = more page views](https://assets.en.oreilly.com/1/event/29/The%20Secret%20Weapons%20of%20the%20AOL%20Optimization%20Team%20Presentation.pdf)
*   Amazon: [100 milliseconds faster = 1% more revenue](https://radar.oreilly.com/2008/08/radar-theme-web-ops.html)
*   Aberdeen Group: [1 second slower = 11% fewer page views, 7% less conversion](https://www.gomez.com/wp-content/downloads/Aberdeen_WebApps.pdf)
*   [Google uses website speed](https://googlewebmastercentral.blogspot.com/2010/04/using-site-speed-in-web-search-ranking.html) in search ranking.</p>

## Summary

The RAIL model is a lens to look at a user’s experience with a website or app as a journey comprising individual interactions. Once you know each interaction’s area, you will know what the user will perceive and, therefore, what your goals are.

Sometimes it takes extra effort, but if you’re kind to the user, they’ll be good to you.</p>

## Resources

If you want more information on RAIL and how to optimize your websites and apps, take a look at these.</p>

### Presentations on RAIL

*   “[Performance RAIL’s: The Art and Science of optimizing for Silicon and Wetware](https://docs.google.com/presentation/d/13AJe2Ip4etqA8qylrva7bEgu1_hAvsq_VQiVOAxwdcI/edit#slide=id.p19)” (slides), Ilya Grigorik, Google, May 2015
*   “[How Users Perceive the Speed of The Web](https://docs.google.com/presentation/d/1AwT2vVHzzlsIxEUS-z769awGa-hiHTwR0iWrkeX49Fk/edit#slide=id.g6f0232e78_056)” (slides), Paul Irish, FluentConf, April 2015
*   “[Performance on RAILs](https://www.youtube.com/watch?v=uJMA2n4RL6s)” (video), Paul Lewis, Nordic.js, September 2015

### Guidance and Documentation

*   “[Optimizing Performance](https://developers.google.com/web/fundamentals/performance/index.html),” _Web Fundamentals_, Google Developers
*   “[Browser Rendering Optimization](https://www.udacity.com/course/ud860)” (course), Udacity
*   “[Profile](https://developers.google.com/web/tools/profile-performance/index)” (performance), _Google Web Tools_, Google Developers
*   “[The RAIL Performance Model](https://developers.google.com/web/tools/profile-performance/evaluate-performance/rail?hl=en),” _Web Fundamentals_, Google Developers

### Performance Audits

*   [Performance Audit of theverge.com](https://docs.google.com/document/d/1Xv3qNROxPOOtau7V3UbHHJyA-5AmGC4s-hZKBe0Lx6U/edit#bookmark=id.uy1m8rhjr41h)” (July 2015)
*   [Performance Audit of imore.com](https://docs.google.com/document/d/1-Kdmub-7WfA45gSyG2GYQOyEkkjmG1gKq0zJwhrWbPA/edit)” (July 2015)
*   [Performance Audit of m.espn.com](https://docs.google.com/document/d/1yJoMEdFME04maB_hlGhARTeys-DdeHRqU7zn-z4CFcA/edit#heading=h.v23t53p6nkzl)” (April 2015)
*   [Performance Audit of squarespace.com](https://docs.google.com/document/d/15VSNoBP3OK64l5Jc_w63sgW88RUn3ve2qV7Jrrfc5A8/edit#heading=h.v23t53p6nkzl)” (April 2015)
*   [Performance Audit of cafepress.com](https://docs.google.com/document/d/1tsOXooeJhSwGmCRGisr98o1KBhqTvO9i49X_OSn7LXc/edit)” (April 2015)
*   [Performance Audit of CNET, Wikipedia and Time.com](https://docs.google.com/document/d/1K-mKOqiUiSjgZTEscBLjtjd6E67oiK8H2ztOiq5tigk/edit?pli=1#)” (February 2015)
*   [Performance Audit of Wikipedia Rich Editor](https://docs.google.com/document/d/1K-mKOqiUiSjgZTEscBLjtjd6E67oiK8H2ztOiq5tigk/edit?pli=1#heading=h.vwra8t2fwx8t)” (February 2015)

### Academic Research on Perceivable Performance

*   1968: “[Response Time in Man-Computer Conversational Transactions](https://theixdlibrary.com/pdf/Miller1968.pdf)” (PDF), Robert B. Miller, Fall Joint Computer Conference 1968
*   1991: “[Response Times: The 3 Important Limits](https://www.nngroup.com/articles/response-times-3-important-limits/),” Jakob Nielsen, Nielsen Norman Group
*   2004: “[A Study on Tolerable Waiting Time: How long Are Web Users Willing to Wait?](https://sighci.org/uploads/published_papers/bit04/BIT_Nah.pdf)” (PDF), Fiona Fui-Hoon Nah, _Behaviour and Information Technology_, 2004
*   2005: “[Interaction in 4-Second Bursts: The Fragmented Nature of Attentional Resources in Mobile HCI](https://www.interruptions.net/literature/Oulasvirta-CHI05-p919-oulasvirta.pdf)” (PDF), Antti Oulasvirta, Sakari Tamminen, Virpi Roto, and Jaana Kuorelahti, Interruptions in Human Computer Interaction
*   2006: “[Quantifying Interactive User Experience on Thin Clients](https://isr.cmu.edu/doc/tolia06-ieee.pdf)” (PDF), Niraj Tolia, David G. Andersen, and M. Satyanarayanan, The Internet Suspend/Resume Project, Carnegie Mellon
*   2012: “[Characterizing Web Use on Smartphones](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.366.1170&rep=rep1&type=pdf)” (PDF), Chad C. Tossell, Philip Kortum, Ahmad Rahmati, Clayton Shepard, Lin Zhong, Conference on Human Factors in Computing Systems 2012
*   2011: “[Playing With Tactile Feedback Latency in Touchscreen Interaction: Two Approaches](https://link.springer.com/chapter/10.1007%2F978-3-642-23771-3_42)” (PDF), Topi Kaaresoja, Eve Hoggan, Emilia Anttila, _Human-Computer Interaction: INTERACT 2011_

{{< signature "al" >}}

