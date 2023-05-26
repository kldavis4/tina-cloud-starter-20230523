---
title: 'Why Perceived Performance Matters, Part 1: The Perception Of Time'
slug: why-performance-matters-the-perception-of-time
author: denys-mishunov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/158f1525-3e45-4706-9343-0499ab509693/09-clock-opt-small1.png
date: 2015-09-25T05:11:10.000Z
description: >-
  Those of us who consider ourselves developers, including me, are very
  task-oriented. We like to be **guided towards optimal results**, and we find
  ourselves uncomfortable when there is no clear path to follow. That is why we
  all want to know how to do things; we like step-by-step tutorials and how-tos.
  However, such guidelines are based on certain theories, deep knowledge and
  experience.

  For this reason, I will not provide you, the reader, with a structured answer
  to the question of how to make a website faster. Instead, I aim to provide you
  with the **reasons and theories for why things function in certain way**. I
  will use examples that are observable in the offline world and, using
  principles of psychology, research and analysis in psychophysics and
  neuroscience, I will try to answer some “Why?” questions.
categories:
  - UX
  - Design
  - Psychology
  - UX
---
Those of us who consider ourselves developers, including me, are very task-oriented. We like to be <strong>guided towards optimal results</strong>, and we find ourselves uncomfortable when there is no clear path to follow. That is why we all want to know how to do things; we like step-by-step tutorials and how-tos. However, such guidelines are based on certain theories, deep knowledge and experience.</p>

## <span class="rh">Further reading</span> on Smashing:

*   [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)
*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

For this reason, I will not provide you, the reader, with a structured answer to the question of how to make a website faster. Instead, I aim to provide you with the <strong>reasons and theories for why things function in certain way</strong>. I will use examples that are observable in the offline world and, using principles of psychology, research and analysis in psychophysics and neuroscience, I will try to answer some “Why?” questions, like:

*   Why do time and performance matter?
*   Why don’t we like to wait?
*   Why does faster not always mean better in the online world?

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9aefcfd-c914-43fd-b675-e9a85f2688eb/00-alice-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb53ad71-fef2-46eb-87ad-ddaa07687be6/00-alice-opt-small.png" alt="Deconstructing Performance" width="500" height="264" /></a><figcaption>“Alice: How long is forever? White Rabbit: Sometimes, just one second.” — Lewis Carroll. "Alice's Adventures in Wonderland."</figcaption></figure>

In addition to these, <strong>we will cover psychological aspects</strong> of some practical cases, like performance optimization of an existing project, how to deal with the better performance of a competitor’s website and how to make users barely notice any waiting for your services. Hopefully, after understanding these “Why?” basics, you will be ready to look outside of some structured “box” the next time you are involved in an optimization process and will make your very own conscious path towards an optimal result.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a86c5841-a2a4-4126-a214-8ef838718556/01-tree-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0891e1c4-59cf-4530-941d-3e045c376181/01-tree-opt-small.png" alt="Every how-to, tutorial, guideline has a simple question &quot;Why?&quot; at its roots" /></a><figcaption>Every how-to, tutorial and guideline has a simple “Why?” at its root. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a86c5841-a2a4-4126-a214-8ef838718556/01-tree-opt.png">View large version</a>)</figcaption></figure>

## Basic Concepts

“Well, I never heard it before, but it sounds uncommon nonsense,” says the Mock Turtle in <em>Alice’s Adventures in Wonderland</em>. So, first things first. Let us settle on basic terminology and principles. In the following paragraphs, I will define the main concepts that you will find throughout the article.

Time can be analyzed from two different points: objective and psychological. When we talk about time that can be measured with a stopwatch, we’re talking about <strong>objective time</strong> or <strong>clock time</strong>. Objective time, though, is usually different from how users perceive time while waiting for or interacting with a website, app, etc. When we talk about the user’s perception of time, we mean <strong>psychological time</strong> or <strong>brain time</strong>. This time is of an interest to psychologists, neuroscientists and odd individuals like me.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b150d5c-4531-4e0a-b13a-21a86414df84/02-perception-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd555806-1878-4ee0-941e-09865ef783cf/02-perception-opt-small.png" alt="Psychological Time in our brain usually differs from Objective Time on the clock" /></a><figcaption>Psychological time in our brain usually differs from objective time on the clock. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b150d5c-4531-4e0a-b13a-21a86414df84/02-perception-opt.png">View large version</a>)</figcaption></figure>

<strong>Performance optimization</strong> is a process of improving the delivery speed of services, feedback or any other type of response action in order to meet a user’s expectation.

We will call the form of communication that occurs when users have to wait for a response from a system a <strong>human-to-computer</strong> style. On the other hand, when a system barely has any delay in response, we will call that a <strong>human-to-human</strong> style, similar to the regular conversations we have in real life.

A <strong>performance budget</strong>, as <a title="Tim Kadlec's personal site." href="https://timkadlec.com/">Tim Kadlec</a> <a title="'Setting a Performance Budget' blog post by Tim Kadlec" href="https://timkadlec.com/2013/01/setting-a-performance-budget/">defines it</a>, “is just what it sounds like: you set a budget on your page and do not allow the page to exceed that.” For the purpose of this article, we will consider the performance budget to be directly connected to time — for example, loading a page, responding to a user’s input, etc.

Armed with these definitions, let’s go down the rabbit hole.</p>

## Part 1: Objective Time

<blockquote>Now, here, you see, it takes all the running you can do, to keep in the same place. If you want to get somewhere else, you must run at least twice as fast as that!

The Red Queen in Lewis Carroll’s <em>Through the Looking-Glass</em></blockquote>

As we defined it earlier, objective time is time that can be measured with a clock. In this first article in our series, we will discuss how to use this time more efficiently for our projects.</p>

## “Remember That Time Is Money”

This phrase, credited to Benjamin Franklin in his <em>Advice to a Young Tradesman</em>, still proves true in our contemporary world. According to a <a href="https://blog.radware.com/applicationdelivery/applicationaccelerationoptimization/2015/03/new-findings-sotu-spring-2015/">recent study</a>, it takes only 3 seconds for a visitor to abandon a website. For every 1 second of improvement, Walmart experienced an increase in conversions of up to a 2% on its website. When auto-parts retailer AutoAnything cut loading times in half, it experienced a 13% increase in sales. Users value their time, and a <strong>human-to-human</strong> style of communication is increasingly expected.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57cb7c39-d0f5-4b40-8670-b3b5b687dfab/03-human-to-human-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c294a62-8790-44e9-bf99-6e08a99d4490/03-human-to-human-opt-small.png" alt="A human-to-human style of communication is increasingly expected from online systems" /></a><figcaption>A human-to-human style of communication is increasingly expected from online systems. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57cb7c39-d0f5-4b40-8670-b3b5b687dfab/03-human-to-human-opt.png">View large version</a>)</figcaption></figure>

New ways of communication require a new way of thinking in the design and development of online systems. In the web industry, we have been talking about speed and performance for quite a while. We’ve been emphasizing the importance of fast communication, and we’re always trying to reach certain goals in seconds, kilobytes, frames per second and so on. As a result, we know how to make our websites fast using technology. Furthermore, we keep getting advice from leading developers and companies about preferred times in user-to-website interactions. In November 2014, Dimitri Glazkov, Jochen Eisinger and Chris Harrelson, in their “<a title="State of Blink video presentation" href="https://www.youtube.com/watch?v=Ku3znd7JNIk">State of Blink</a>” keynote about the Blink rendering engine, suggested a <a href="https://goo.gl/T2kgmG">platform success model</a> based on interaction times.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93008ef5-cf3a-4f90-8e11-b9186d8ff236/04-success-model-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7aa894d-5725-43b7-a1d4-d823a582fe02/04-success-model-opt-small.png" alt="Platform success model" /></a><figcaption><a href="https://goo.gl/T2kgmG">Platform success model from Google</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93008ef5-cf3a-4f90-8e11-b9186d8ff236/04-success-model-opt.png">View large version</a>)</figcaption></figure>

After quite a few years of the “2-second loading time” recommendation, the <a href="https://goo.gl/T2kgmG">platform success model</a> technically sets the limit on page-loading time to 1 second. Usually, the average developer or project manager is satisfied with an explanation like, “Longer times affect rankings in search results.” But what recommendations are these explanations based on? How much freedom do we have in setting certain time-based goals or a performance budget? And, what is even more interesting than simple numbers, can we be creative with these durations, playing with them to deliver better experiences to our users? These are the main questions we will cover in this article.</p>

<a name="performance-budget"></a>

## Choosing A Performance Budget

As defined earlier, a performance budget is a limit that we set on certain time-related operations of an online system and that we do not allow the system to exceed. Usually, human-to-human conversations involve quite short time intervals between a question being asked and a response being given by the interlocutor. In psychology, we should keep four important spans of time in mind when dealing with short time durations:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d9bd13c-25c9-4f75-98f6-a0b1c02530d8/05-time-spans-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5485b6fb-6552-4112-ae95-add9b1b5e86c/05-time-spans-opt-small.png" alt="Psychological time durations" /></a><figcaption>Psychological time durations (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d9bd13c-25c9-4f75-98f6-a0b1c02530d8/05-time-spans-opt.png">View large version</a>)</figcaption></figure>

*   **0.1 to 0.2 seconds** [Research](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/biae.clemson.edu/bpc/bp/Lab/110/reaction.htm#Mean%20Times "Mean Reaction Times. 'A Literature Review on Reaction Time' by Robert J. Kosinski, Clemson University") points to this interval as the range of the maximum acceptable response time to simulate **instantaneous** behavior — an interval within which users barely, if at all, notice a delay.<sup>[1](#endnote1 "This is the reaction time of the average person to a simple stimulus, such as catching a falling pen or jerking one's hand away from a hot cup. This is probably the most important time we should keep in mind.")</sup>
*   **0.5 to 1 seconds**.  This is the maximum response time for **immediate** behavior. This interval is usually the response time from an interlocutor in a human-to-human conversation.<sup>[2](#endnote2 "According to G.A. Miller, most adults can store five to nine simple items in their short-term memory. Research — confirmed by a number of experiments, in particular the one by M. Greene and A. Oliva of MIT — shows that 'the processing of complex natural images and visual object recognition' takes no more than a tenth of a second. This means that short-term memory processing of five to nine items such as this should take about 0.5 to 0.9 seconds. Hence, 1 second is considered to be the maximum time for the user's flow of thought to stay uninterrupted.")</sup> Delays within this interval are noticeable but easily tolerated by most users. During this time, the user must receive an indication that their command (such as their click of a button or link) has been accepted, assuming that the signal was not already sent during the previous interval.
*   **2 to 5 seconds**.  Psychologist [Mihaly Csikszentmihalyi](https://en.wikipedia.org/wiki/Mihaly_Csikszentmihalyi) defines a **flow** or **optimal experience** as a state when people experience concentration, absolute absorption in an activity and deep enjoyment.<sup>[3](#endnote3 "While optimal experience time fluctuates according to subjective parameters, for most tasks that the average user faces on the web, the time of concentration falls between 2 to 5 seconds. This is why, for some years, we operated with 2 seconds as the optimal page-loading time.")</sup>
*   **5 to 10 seconds**.  According to the [National Center for Biotechnology Information at the US National Library of Medicine](https://www.statisticbrain.com/attention-span-statistics/), the average attention span of a human being dropped from 12 seconds in 2000 to 8.25 seconds in 2015\. Guess what? That is 1 second less than the attention span of a goldfish! As a simplification — and to emphasize our superiority to the goldfish — we consider 10 seconds as the absolute maximum time of a user’s **attention span**.<sup>[4](#endnote4)</sup> The user would still be focused on their task but would become easily distracted. This is the time for the system to engage the user in the process; if this is not done, then the user will most probably be lost forever.

Now, if we apply these time definitions to the aforementioned <a href="#success-model">platform success model</a> suggested by the Blink team, we can translate its emphasis on a 1-second loading time and a 0.1-second response time into more human-to-human language:

*   The loading page should happen **immediately**.
*   Users should get feedback from a given action **instantly**.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea28e25-39b0-417e-bbb9-454549ce3e56/06-loading-feedback-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc556c2d-a9f9-43a3-9eee-60973cd202ae/06-loading-feedback-opt-small.png" alt="Load pages immediately, and give feedback on any given action instantly." /></a><figcaption>Load pages <strong>immediately</strong>, and give feedback on a given action <strong>instantly</strong>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea28e25-39b0-417e-bbb9-454549ce3e56/06-loading-feedback-opt.png">View large version</a>)</figcaption></figure>

Humans have inner stopwatches that have been tuned well since our cave-dwelling ancestors. Hence, you can safely rely on the time spans above when choosing a performance budget for your next web project. But time on its own is useless unless put into some context. Consider an example. What do you think about in response to the statement, “A process will take 10 seconds to complete.” Take your time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8afba17e-f2ff-4758-984e-29f6d3e93465/07-process-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8211a5ff-2534-4eba-8832-597b279818f6/07-process-opt-small.png" alt="A process will take 10 seconds to complete" /></a><figcaption>“A process will take 10 seconds to complete.” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8afba17e-f2ff-4758-984e-29f6d3e93465/07-process-opt.png">View large version</a>)</figcaption></figure>

Done? I’ll bet the first thing you thought was, “What process?” Your brain iterated over possible options based on your life experience, current lines of thinking, mood and so on. Then, once your brain settled on a dominant guess, it evaluated your expectations about that process’ duration against the declared 10 seconds.

That being said, most often we don’t pick a random time duration on its own, but rather choose time in a certain context. First, the context could be set by our own constraints, such as a <strong>need for performance optimization</strong> in order to meet users’ expectation of a human-to-human style of communication. Secondly, the context might also be set by competitors; in this case, we’re dealing with a <strong>chase-the-leader</strong> scenario to reach the performance level set by others. We will look at both scenarios below.</p>

<a name="20-percent"></a>

## The Need for Performance Optimization: The 20% Rule

Here is a situation that most of us can relate to to some extent. Your customer says that the search function of your website is slow. Your measurements show an average of 5 seconds to render search results. After employing some optimization techniques, you bring it down to 4.5 seconds. Happily (well, as happily as one could possibly be with a 4.5-second rendering time), you send an email to the customer with this information. All you get in return is, “Doesn’t look any faster to me.” That usually hurts. Let’s try to understand why the customer did not notice any difference.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09591821-08c2-4b4a-a051-d88952dcbaa8/08-search-optimisation-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6387aa8e-09bf-4ab4-8467-a416ba705437/08-search-optimisation-opt-small.png" alt="Sometimes half of a second is just not enough" /></a><figcaption>Users will not necessarily notice your optimizations, so it is too early for a party. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09591821-08c2-4b4a-a051-d88952dcbaa8/08-search-optimisation-opt.png">View large version</a>)</figcaption></figure>

In 1834, one of the founders of experimental psychology, <a title="E.H. Weber in Encyclopaedia Britannica" href="https://www.britannica.com/biography/Ernst-Heinrich-Weber">Ernst Heinrich Weber</a>, postulated a law that defines <strong>difference threshold</strong> or a <strong>just noticeable difference</strong> (JND) as the minimum difference in stimulation (weight, light, etc.) that a person can detect most of the time. Later, Weber’s student <a title="G.T. Fechner in Encyclopaedia Britannica" href="https://www.britannica.com/biography/Gustav-Theodor-Fechner">Gustav Theodor Fechner</a> applied the law to the measurement of sensations, setting the basis for the science of <a href="https://www.britannica.com/science/psychophysics">psychophysics</a>. This work by Weber and Fechner is known to us as the <strong>Weber-Fechner Law</strong>. The law is still regarded by many scientists as arguably the most important tool in understanding perception.

Time is not an exception to the Weber-Fechner Law. Practical experiments in psychophysics show that time intervals are prone to a JND of between 7% to 18% on average for shorter periods (with a duration of less than 30 seconds). Based on this, a good rule of thumb is to simplify the Weber-Fechner Law into a <strong>20% rule</strong>. That is, in order for users to barely see a difference in time duration, it has to be changed by a minimum of 20%.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3f3769c-7bbe-4963-b7b7-a6fa8f27b4d0/09-clock-opt-small.png" alt="20% Rule" /><br>
<figcaption>The Weber-Fechner Law can be simplified into a 20% rule for short time durations.</figcaption></figure>

Let’s go back to our example of a client noticing no difference in the rendering of search results after our optimizations. Originally, the search results were returned in 5 seconds. Using the 20% rule, we can tell that, for the user to even notice the difference, the new search results should be at least 1 second faster:

<pre><code>5 seconds × 0.2 = 1 second</code></pre>

That is why the client simply did not notice the 0.5-second improvement.

We’re talking about performance optimization, but this technique works in the opposite direction. If, for example, you are developing a feature that slows down your web page, you could apply the 20% rule to determine whether the performance decrease will be noticed by users at all. Allowing our code to be a bit slower without harming the user experience is called <strong>regression allowance</strong>.</p>

<strong>Note:</strong> When we talk about 20%, we are talking about a “just noticeable” difference. “<strong>Noticeable</strong>” does not mean “<strong>meaningful</strong>.” In order for users to appreciate your performance optimization, you should go well beyond this threshold.

But what do you do when a competitor comes to market with significantly better performance for a comparable feature? What if a 20% regression allowance relative to the competitor’s time is not even technically approachable for us? In this case, we should at least aim for what G. Moore, in his book <a title="The book by G.A. Moore" href="https://www.dealingwithdarwin.com/"><em>Dealing with Darwin</em></a>, calls <strong>neutralization</strong>.</p>

<a name="neutralization"></a>

## Neutralization, Or Chasing The Leader

Time neutralization occurs when the time difference between two services is noticeable but does not influence the user’s preference of one service over another. In this case, reliability, usability and other <strong>quality</strong>-related factors of the service play a much more significant role. In other words, time neutralization is a good position to be in when you have better services than competitors.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f287c88a-691b-4200-8e70-4344b800cf0d/10-chasing-the-leader-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41b30c4d-150c-419c-8c9b-e67996f1adf4/10-chasing-the-leader-opt-small.png" alt="Chasing the leader might be tough" /></a><figcaption>What to do when your competitors deliver the same functionality but much more quickly? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f287c88a-691b-4200-8e70-4344b800cf0d/10-chasing-the-leader-opt.png">View large version</a>)</figcaption></figure>

Again, getting back to our example of search results taking 5 seconds to appear, assume that a competitor comes to the market with a very similar search service: the same functionality, the same results and the same feel. The problem is that their search results are revealed in 2 seconds, not 5. Applying the 20% rule to our 5 seconds would not make sense in this scenario. We’re not competing with our own time; rather, we have to match the competitor’s. We can make a couple of logical assumptions here:

1.  We cannot decrease the search response time to 2 seconds. (If it were that easy, we probably would have done it already.)
2.  If 2 seconds is out of reach, the next best solution would be to use the 20% rule of regression allowance relative to the competitor’s time: 2 seconds + 20% = 2.4 seconds.

At 2.4 seconds, users will not notice any difference between our search results and the competitor’s. But if we cannot achieve 2 seconds, then 2.4 seconds is probably also out of reach.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7f44fb3-bd29-4700-85dd-36274a7a33c6/11-chasing-the-leader-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9241b656-268e-40e2-9f9c-2350c91659d4/11-chasing-the-leader-opt-small.png" alt="We can match neither 2 seconds directly, nor a 20% regression allowance of competitors’ time" /></a><figcaption>We can match neither the 2 seconds directly nor a 20% regression allowance of the competitor’s time. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7f44fb3-bd29-4700-85dd-36274a7a33c6/11-chasing-the-leader-opt.png">View large version</a>)</figcaption></figure>

When comparing two durations (2 and 5 seconds, in our case), we’ll find a “magical” psychological threshold between them. Time durations longer than this threshold will be perceived by the user as being closer to 5 seconds. Time durations shorter than that threshold will be perceived as being closer to 2 seconds. Surprisingly, <a title="'Basic Temporal Discrimination Procedures' by M.MacInnis, P.Guilhardi" href="https://www.brown.edu/Research/Timelab/archive/Pdf/2006-03.pdf">studies in animal timing</a>, particularly those conducted by R. Church, M. MacInnis, P. Guilhardi and others at Brown University, show that this threshold is not simply the average of the two durations. This threshold proved to be predictable and is found at the <strong>geometric mean</strong>, instead of an arithmetical one. Research with human subjects confirm the same finding.

From mathematics, we might remember that the geometric bisection between two numbers can be found using the following formula:

<pre><code>√(A × B)</code></pre>

Applying this formula to our numbers, we get:

<pre><code>√(2 × 5) ≈ 3.2 seconds</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/930b5a8c-4a9c-4005-a30a-c914ee9ceb26/12-geometric-mean-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/439a0c7f-226a-424b-8bf6-7c1e789153bb/12-geometric-mean-opt-small.png" alt="The threshold of the difference between two times can be found through the geometric mean of the two" /></a><figcaption>Geometric bisection as an illustration of neutralization (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/930b5a8c-4a9c-4005-a30a-c914ee9ceb26/12-geometric-mean-opt.png">View large version</a>)</figcaption></figure>

For our 2- and 5-second results, 3.2 seconds is the threshold of neutralization. At this point, users will notice a difference, but the difference will be perceived as being unimportant to their choice of service. Factors such as the quality of the service and reliability will play a much more important role, but managing these is beyond the scope of this article.

With this, we finish our basic analysis of objective time. By now, we should have a good understanding of where <a href="#success-model">some widely adopted industry standards</a>, such as page-loading time and the response time for a system, come from. We also have a <a href="#performance-budget">guideline for setting a performance budget</a>, and we understand how to deal with time when we have to <a href="#20-percent">improve the performance of a website</a> or <a href="#neutralization">match that of a competitor’s</a>.

But as we have mentioned earlier, another kind of time usually matters much more to users than the kind measured with a stopwatch. Ladies and gentlemen, let’s meet in part 2 and talk about the psychological time.</p>

<figure><a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09cbe7e6-a99a-403a-8fc7-50fceecfedf6/13-to-be-continued-opt-small.png" alt="To be continued…" /></a></figure>

### Endnotes

<a name="endnote1"></a>

<sup>1</sup> This is the reaction time of the average person to a simple stimulus, such as catching a falling pen or jerking one's hand away from a hot cup. This is probably the most important time we should keep in mind.</p>

<a name="endnote2"></a>

<sup>2</sup> According to G.A. Miller, <a title="'The Magical Number Seven, Plus or Minus Two: Some Limits on Our Capacity for Processing Information' by George A. Miller" href="https://www.musanim.com/miller1956/">most adults can store five to nine simple items in their short-term memory</a>. <a title="'Throwing a glance at the neural code: rapid information transmission in the visual system.' by Tim Gollisch" href="https://www.ncbi.nlm.nih.gov/pubmed/19649155">Research</a> — confirmed by a number of experiments, in particular the one by Michelle R. Greene and <a title="Aude Oliva" href="https://cvcl.mit.edu/audeoliva.html">A. Oliva</a> of MIT — shows that “the processing of complex natural images and visual object recognition” takes no more than a tenth of a second. This means that short-term memory processing of five to nine items such as this should take about 0.5 to 0.9 seconds. Hence, 1 second is considered to be the maximum time for the user’s flow of thought to stay uninterrupted.</p>

<a name="endnote3"></a>

<sup>3</sup> While optimal experience time fluctuates according to subjective parameters, for most tasks that the average user faces on the web, the time of concentration falls between 2 to 5 seconds. This is why, for some years, we operated with 2 seconds as the optimal page-loading time.</p>

<a name="endnote4"></a>

<sup>4</sup> Of course, the state of focused attention in general spans far beyond 10 seconds and can reach 20 to 30 minutes. (This long-term attention is called “selective sustained attention.”) However, first, this time span is much more exposed to fluctuation due to different uncontrolled circumstances; secondly, not many website owners out there can brag about their website being actively used by the average user for more than a couple of minutes.

{{< signature "ah, ml, al" >}}

