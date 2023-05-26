---
title: 'Why Performance Matters, Part 3: Tolerance Management'
slug: performance-matters-part-3-tolerance-management
author: denys-mishunov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43095f26-d6ec-4cdc-ac9e-6fc9d116b4f0/skeleton-opt.png
date: 2015-12-10T17:08:21.000Z
description: >-
  When technical performance optimizations reach certain limits, psychology and
  **perception management** might help us to push the limits further. Waiting
  can consist of **active** and **passive phases**; for the user to perceive a
  wait as a shorter one, we increase the active phase and reduce the passive
  phase of the wait. But what do we do when the event is a purely passive wait,
  with no active phase at all? Can we push the limits even further?

  Waits without an active phase happen quite often in the offline world: waiting
  in a checkout line to the till, waiting for a bus, queuing in an amusement
  park, and so on. It is widely accepted that the longer the user has to wait,
  [the more negative the
  reaction](https://www.emeraldinsight.com/doi/abs/10.1108/08876049510100281) to
  the wait. User reaction to a wait online is **no different from that in the
  offline world**. Studies based on the analysis of more than a thousand cases
  identify [14 distinct types of waiting situations on the
  web](https://www.emeraldinsight.com/doi/abs/10.1108/10662240510590379). Being
  dependent on our users' loyalty, we cannot leave them facing a passive wait.
categories:
  - Coding
  - Psychology
  - Performance
  - Workflow
---
When technical performance optimizations reach certain limits, psychology and **perception management** might help us to push the limits further. Waiting can consist of **active** and **passive phases**; for the user to perceive a wait as a shorter one, we increase the active phase and reduce the passive phase of the wait. But what do we do when the event is a purely passive wait, with no active phase at all? Can we push the limits even further?

## <span class="rh">Further reading</span> on Smashing:

*   [Perceived Performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
*   [Perception Management](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/)
*   [Preload: What is it good for?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [Progressive Enhancement](https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/)
*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43095f26-d6ec-4cdc-ac9e-6fc9d116b4f0/skeleton-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e836a24-66de-43df-af76-1dd15773359f/skeleton-500px-opt.png" /></a><figcaption>What can we do when there is no active wait at all? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43095f26-d6ec-4cdc-ac9e-6fc9d116b4f0/skeleton-opt.png">View large version</a>)</figcaption></figure>

Waits without an active phase happen quite often in the offline world: waiting in a checkout line to the till, waiting for a bus, queuing in an amusement park, and so on. It is widely accepted that the longer the user has to wait, [the more negative the reaction](https://www.emeraldinsight.com/doi/abs/10.1108/08876049510100281) to the wait. User reaction to a wait online is **no different from that in the offline world**. Studies based on the analysis of more than a thousand cases identify [14 distinct types of waiting situations on the web](https://www.emeraldinsight.com/doi/abs/10.1108/10662240510590379). Being dependent on our users' loyalty, we cannot leave them facing a passive wait.

{{% feature-panel %}}

This three-part series explores the perception of time that has also an effect on observed performance. The [first part](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/) explored objective time and some techniques for managing it. We reviewed the ideas behind several widely adopted industry standards, such as page-loading time and system response time. [Part 2](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/) reviewed the [preemptive start](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#preemptive-start) and [early completion](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#early-completion) techniques which, by dealing with active and passive wait, allow us to manage a user’s perception of time.

This part finally discusses **pure passive waiting on the web**, how we can deal with it and what can be done to keep user satisfaction high even when the service cannot be delivered fast enough. In addition to the studies on waiting online, our analysis will employ the psychology of waiting lines, customer satisfaction and other tools applicable to offline waiting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eff336aa-2a8f-4348-8415-d29621579999/line-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe9e1487-6450-494c-85a7-9058a885be12/line-500px-opt.png" alt="line" /></a><figcaption>The psychology of waiting lines and other studies applicable in the offline world will help us better understand online waiting. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eff336aa-2a8f-4348-8415-d29621579999/line-opt.png">View large version</a>)</figcaption>
</figure>

## Psychological Time: Tolerance Management

In the first half of the 20th century, building managers received complaints about long waiting times for elevators. The managers were perplexed because there was no easy technical solution. To solve the issue, some expensive and time-consuming engineering had to be considered. From this point [the stories vary](https://www3.sympatico.ca/karasik/GF_evolution_of_legend.html), but someone (designers say a designer, engineers argue that it was an engineer) came up with the idea of tackling the problem from a different, non-technical point of view.

The solution, much simpler and less expensive was found: **install mirrors in the elevators** and floor-to-ceiling mirrors in the lobby. After installing the mirrors, the number of complaints dropped to nearly zero without any change in the objective time. Why?

<blockquote>
<p>“White Rabbit: Oh! Won’t she be savage if I’ve kept her waiting!”</p>
<p>&mdash; Lewis Carroll, <cite>Alice’s Adventures in Wonderland</cite></p>
</blockquote>

I'm sure most of you can guess the answer. Simply put, the solution replaced the pure _passive_ wait that people experienced while waiting for an elevator with an _active_ one by engaging people with looking at themselves (and in surreptitiously looking at others). It didn’t try to convince people that the wait was shorter, didn’t do anything to the objective time or event markers. Instead, people were shifted into the active phase right from the beginning of the wait to its end. In so doing, people were much more **tolerant** of the wait.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c16659-5ca1-4000-bc5f-08b994af60a8/skyscrapers-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97ca3c8a-ae2d-4f10-989d-3bacd6807b15/skyscrapers-500px-opt.png" alt="skyscrapers" /></a><figcaption>Who came up with the idea of installing mirrors in elevators? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c16659-5ca1-4000-bc5f-08b994af60a8/skyscrapers-opt.png">View large version</a>)</figcaption></figure>

Now it's time to get all the way down the rabbit hole of the waiting problem. Let’s face it, it’s not always easy to convince a user that a wait is shorter than it really is. Nevertheless, [waiting need not have a negative effect on consumers’ evaluations](https://www.sciencedirect.com/science/article/pii/S1094996899702252) of websites if the waiting time is _well managed_. So why are people so intolerant of waiting?

In 1985, David Maister conceptualized [eight “propositions”](https://davidmaister.com/articles/the-psychology-of-waiting-lines/) (that have been confirmed in experiments by [P. Johns and E. Peppiatt](https://www.emeraldinsight.com/doi/abs/10.1108/09564239610149957), [P. Jones and M. Dent](https://getinfo.de/en/search/id/BLCP%3ACN004938800/), and others) concerning the psychology of waiting. Although [Davis and Heineke](https://www.emeraldinsight.com/doi/abs/10.1108/01443579410056777) and E. Peppiatt supplemented the list with two more propositions later, for simplicity's sake we will call all of the propositions **Maister's list**. You will find the list along with the possible recommendations on how we can deal with corresponding propositions in the table below.</p>

<table class="break-out article-table three-columns">
	<caption>Eight propositions from D. Maister concerning the psychology of waiting, with two additional propositions from M. Davis, J. Heineke and E. Peppiatt.</caption>
	<tr>
		<th width="10%"></th>
		<th width="45%">Proposition</th>
		<th width="45%">Recommendation/comment</th>
	</tr>
	<tr>
		<td>P1</td>
		<td><strong>Occupied time feels shorter than unoccupied time.</strong></td>
		<td>Balance between <em>active</em> and <em>passive</em> phases discussed in <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">part 2</a>. This is also how the elevator problem was solved.</td>
	</tr>
	<tr>
		<td>P2</td>
		<td><strong>People want to get started (pre-process waits feel longer than in-process waits).</strong></td>
		<td><a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#early-completion">Early completion</a> and <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#preemptive-start">preemptive start</a> techniques from part 2.</td>
	</tr>
	<tr>
		<td>P3</td>
		<td><strong>Anxiety makes waits seem longer.</strong></td>
		<td>Very subjective and hard to manage in the online world where there is no real contact with the user.</td>
	</tr>
	<tr>
		<td>P4</td>
		<td><strong>Uncertain waits are longer than known, finite waits.</strong></td>
		<td></td>
	</tr>
	<tr>
		<td>P5</td>
		<td><strong>Unexplained waits are longer than explained waits.</strong></td>
		<td></td>
	</tr>
	<tr>
		<td>P6</td>
		<td><strong>Unfair waits are longer than equitable waits.</strong></td>
		<td>Meet users’ expectations: match your waiting times to those of competitors or at least <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#neutralization-or-chasing-the-leader">neutralize the waiting time of your services</a> if you cannot reduce the wait otherwise.</td>
	</tr>
	<tr>
		<td>P7</td>
		<td><strong>The more valuable the service, the longer the customer will wait.</strong></td>
		<td>Increasing the value of your services is beyond the scope of this article.</td>
	</tr>
	<tr>
		<td>P8</td>
		<td><strong>Solo waits feel longer than group waits.</strong></td>
		<td>We can assume that most of the users are ‘queuing’ alone in front of their computers, hence we have no management control over this proposition.</td>
	</tr>
	<tr>
		<td>P9</td>
		<td><strong>Uncomfortable waits feel longer than comfortable waits.</strong></td>
		<td>Definition of “comfortable” is very broad and prone to subjective evaluations.</td>
	</tr>
	<tr>
		<td>P10</td>
		<td><strong>New or infrequent users feel they wait longer than frequent users.</strong></td>
		<td>As in P6, here we should meet users’ expectations considering a hypothetical user who comes to the site for the first time.</td>
	</tr>
</table>

P3, P8, P9 and P10 are either subjects for a much broader application than front-end development is capable of, or are altogether out of reach for management of a website. Hence, P4 and P5 are the only propositions that miss the management tools in this psychology of waiting puzzle. These two tell us that one of the main reasons people feel unhappy about waiting is **uncertainty** of different nature: how long will the wait take? What is going on now? Is the result worth the wait? To answer these questions, **tolerance management** steps in.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d02fd72-71b1-4b0a-9dc7-58b595efba3e/passive-wait-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/981f587f-ceb3-4c21-a021-4e33ea305305/passive-wait-500px-opt.png" /></a>
	<figcaption>Users feel agitated and frustrated about uncertain waits. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d02fd72-71b1-4b0a-9dc7-58b595efba3e/passive-wait-opt.png">View large version</a>)</figcaption>
</figure>

### Show Me Your Progress

<blockquote>
<p>“I wonder how many miles I've fallen by this time?” she said aloud. “I must be getting somewhere near the centre of the earth.”</p>
<p>&mdash; Lewis Carroll, <cite>Alice’s Adventures in Wonderland</cite></p>
</blockquote>

To partially resolve the uncertainty and provide information about the waiting time and current state of a process, good ol’ progress indicators are at our disposal. User researcher [Steven C. Seow](https://www.amazon.com/Designing-Engineering-Time-Psychology-Perception/dp/0321509188) suggests dividing progress indicators into two main groups: **dynamic** (those updating information with time); and **static** (unchanging over time). Each of these can be split into two subgroups: _determinate_ (projects completion by work units, time or some other measure); and _indeterminate_ (does not project completion).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79fd2c83-a82e-42ce-9c32-993b91c35abe/progress-indicators-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/999e2657-d2c3-4531-96e1-7aa3e1617bcc/progress-indicators-500px-opt.png" /></a><figcaption>Different types of progress indicators. Mind the classes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79fd2c83-a82e-42ce-9c32-993b91c35abe/progress-indicators-opt.png">View large version</a>)</figcaption></figure>

Now the question becomes _when to use these_. Obviously, if we show a class A indicator for every action the user performs, it will get very annoying very fast. So, we need some guidelines. When we talked about [performance budgets](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#choosing-a-performance-budget) in part 1 we defined some static time intervals. Let me remind you of those while mapping them to appropriate indicators.</p>

<ul>
	<li><a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#endnote1">Instantaneous (0.1–0.2s)</a></br> Obviously, we do not need to show an indicator for something that is perceived to be instantaneous.</li>
	<li><a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#endnote2">Immediate (0.5–1s)</a></br>One second is the maximum time of a user’s uninterrupted flow of thought. Showing any complex indicator within this interval would introduce an interruption of this flow. But usually it does no harm to display a simple indicator without textual information. Indicators of class D, like spinners or very basic progress bard (simplified class A), are natural enough to avoid breaking a user’s flow of thought, while subtly indicating that the system is responding.</li>
	<li><a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#endnote3">Optimal experience</a></br>Within this interval, we must give users an indication of input or a request being processed and that the system is responding. Again, the optimal indicator would be a class D or a simplified class A indicator – there is no need to draw a user’s attention to additional information.
		<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487ffa11-26fe-4be4-882c-ec98ca8b3e7b/github-opt.png" /><figcaption>Some, like <a href="https://github.com/">GitHub</a> (left) and <a href="https://www.flickr.com/">Flickr</a>, incorporate logos into the spinners or loaders shown during the optimal experience or even shorter intervals.</figcaption></figure></li>
	<li><strong>Attention span (5–10s)</strong><br/>This is the frontier of the user’s tolerance threshold and requires a more complete solution. For events within this interval or longer, we have to show more information than just a general ‘working on it’ indicator: users need to know how much longer they have to wait. Therefore, we should show a dynamic indicator of class A or B where the advance of the process is clear.
		<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c40288a-17ef-40ca-997a-697098d234bb/progress-bar-opt.png" /><figcaption>A progress indicator for durations longer than five seconds can be a simple progress bar with a percentage or more advanced information providing current status while mid-process.</figcaption></figure></li>
</ul>

To summarize these recommendations we could formulate our guidelines as simply as follows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19aea3f1-eb17-4062-b5b1-1857e8098b97/indicators-web-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c06860f-c886-4489-8b86-9a4e40c8c439/indicators-web-500px-opt.png" /></a><figcaption>Guidelines for progress indicators on the web. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19aea3f1-eb17-4062-b5b1-1857e8098b97/indicators-web-opt.png">View large version</a>)</figcaption></figure>

*   **For events lasting 0.5–1s**, showing an indicator of class D (spinner) or simplified class A (progress bar) is advised on a case-by-case basis.
*   **For events lasting for 1–5s**, a class D (spinner) or simplified class A indicator (progress bar) is required.
*   **For events longer than 5s**, a dynamic indicator of class A or B is recommended

It is common for progress indicators to combine different classes or combinations targeted at different propositions in Maister's list.</p>

<figure>
	<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b2353a1-67a1-4dab-af30-8308905b855b/momondo-opt.png" alt="momondo" />
	<figcaption><a href="https://www.momondo.com/">momondo.com</a> combines indicators of class D (spinner) and class B (updating current status without projecting completion).</figcaption><br>
</figure>

<figure>
	<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e08fd8c-9b94-49cc-a7a2-83c840c621fc/slack-opt.gif" alt="slack" />
	<figcaption><a href="https://slack.com/downloads">Slack app</a> has two levels of progress indicators. The second one adds emotional component to the process by offering users a positive message.</figcaption><br>
</figure>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8314b0d6-30c4-4bfc-b94b-ef52eb030100/uio-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10bda6ce-443a-4da0-b949-efdf8e3ceb28/uio-500px-opt.png" alt="uio" /></a>
	<figcaption>Some, like Outlook-powered webmail at the University of Oslo, combine a spinner with information about what is going on at a particular moment. Even though in most cases this information is artificial and does not reflect real actions (the text is being updated based purely on the elapsed waiting time), it is not necessarily a bad thing if it helps users tolerate the wait. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8314b0d6-30c4-4bfc-b94b-ef52eb030100/uio-opt.png">View large version</a>)</figcaption>
</figure>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a97586f3-9de0-4873-8144-5c4f275fbc0d/littlebigroom-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3feb16e-53af-4c65-bb3c-b6be69961fa9/littlebigroom-500px-opt.png" alt="littlebigroom" /></a>
	<figcaption><a href="https://www.little-big-room.com/">Little Big Room</a> is a lovely site that sets the mood, reduces anxiety (P3 in the Maister’s list) and sets up a comfortable feeling (P9) for further waits on the site with its page loading indicator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a97586f3-9de0-4873-8144-5c4f275fbc0d/littlebigroom-opt.png">View large version</a>)</figcaption>
</figure>

Note that in cases when you use other distracting tools (like animation) during the whole wait, there might be no need for an additional progress indicator: users’ are already busy processing the animation, thereby tolerating the wait more easily by default.

Progress indicators are capable of providing enough information to neutralize uncertainty in accordance with P4 and P5\. But can we do better than just indicating loading? Can we address multiple propositions simultaneously? We certainly can.</p>

### Tolerance Beyond Progress Indicators

<blockquote>
	Alice said nothing: she had never been so much contradicted in her life before, and she felt that she was losing her temper.<br />
	— Lewis Carroll, <cite>Alice’s Adventures in Wonderland</cite><br>
</blockquote>

Let’s get to a quite interesting service: [tripmydream.com](https://tripmydream.com/en). Users can find flights and hotel packages all over the world for a predefined budget. After the basic operations like choosing the theme of your trip and desired dates, the user sets the budget for the trip and gets to the search page.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccab8b89-d4fa-4d62-abfa-ea7dd65d6c6a/tmd-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdd810ac-4ac8-429a-833a-583e51db4004/tmd-500px-opt.gif" alt="tmd" /></a>
	<figcaption>The search page at tripmydream.com employs quite a few techniques for tolerance management. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccab8b89-d4fa-4d62-abfa-ea7dd65d6c6a/tmd-opt.gif">View large version</a>)</figcaption>
</figure>

From a performance point of view, searching for a flight and hotel combination all over the world to match a predefined budget is not a lightweight task at all. According to the DevTools, the results for my particular search kept coming in for as long as two minutes. Let’s examine what is done for tolerance management in this case.

First of all, the [early completion](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#early-completion) technique mentioned in [part 2](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/): the first results are rendered as soon as there are any that match the search criteria. But early completion alone is not enough: the first possible result was rendered after almost ten seconds of waiting.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e010e21-e144-4e21-b056-1829ffc21287/tmd-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb74020c-87b9-4e85-9c41-a38856019d95/tmd-1-500px-opt.png" alt="tmd" /></a>
	<figcaption>The early completion technique alone does not save tripmydream.com: the first search results are rendered only after about ten seconds. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e010e21-e144-4e21-b056-1829ffc21287/tmd-1-opt.png">View large version</a>)</figcaption>
</figure>

Earlier, we reasoned that a dynamic progress indicator should be shown for such long-lasting processes. For tripmydream.com, this is the complex indicator of class B consisting of the orange progress bar and the “Analyzing” block right below the bar.</p>

<figure>
	<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/566d78b9-8e51-4902-b253-7bf8e5941508/tmd-2-opt.png" alt="tmd" />
	<figcaption>The progress bar and “Analyzing” block together comprise a complex progress indicator of class B. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/566d78b9-8e51-4902-b253-7bf8e5941508/tmd-2-opt.png">View large version</a>)</figcaption>
</figure>

Finally, let's address the illustrated character at the bottom. The character is aimed at coping with P9 (uncomfortable waits feel longer than comfortable waits): usually, smiling cartoonish characters evoke emotions related to light-hearted childhood memories, setting up more comfortable feelings while dealing with the wait. The character might even partially solve P8 (solo waits feel longer than group waits) for those of us who spend more time with virtual friends in front of the computer than with real people. Keep in mind, though, that the use of a cartoon character should not contradict users’ expectations of the service: such a character on a banking website, for example, would be inappropriate.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3886e9f7-1bd6-4fb2-8a6f-b0d7cd85c0ac/tmd-cartoon-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3109175-e445-4a44-b368-ffeb8493ef0e/tmd-cartoon-500px-opt.png" alt="tmd cartoon" /></a>
	<figcaption>Cartoon characters can help make a wait more tolerable. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3886e9f7-1bd6-4fb2-8a6f-b0d7cd85c0ac/tmd-cartoon-opt.png">View large version</a>)</figcaption>
</figure>

Overall, early completion helps manage a user’s acceptance of waiting time in accordance with P1 and P2; the complex progress indicator deals with P4 and P5; and the cartoon character at the bottom attempts to deal with P9 and P8\. Quite a handful of harmful propositions are under control here!

But not everything is smooth with the cartoon character on this page: it not only soothes, but also communicates, providing the user with **additional textual information**. And here we have a problem. Because the character and the corresponding text in this element are changed to another character every six seconds or so, most of the time users have no time to read the full text.<sup>[1](#endnote1)</sup>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc92d616-35b3-439f-8f3d-481c7d20aedf/norway-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236ad8b1-01e6-4c54-b94c-fae3c4234637/norway-500px-opt.png" alt="norway" /></a>
	<figcaption>If you place text next to a drawing, make sure you provide enough time for users to read it. Removing text while users are reading builds up frustration rather than managing tolerance. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc92d616-35b3-439f-8f3d-481c7d20aedf/norway-opt.png">View large version</a>)</figcaption>
</figure>

There are many good and bad examples of tolerance management on the web. But we will take a look at two which try to achieve the same result with a different approach.

[SlideShare](https://www.slideshare.net/) and [Speaker Deck](https://speakerdeck.com/) are arguably the two most popular services for uploading presentation slides online. Services like these are very useful for speakers to share their slides after an event with a wider audience. Both of these services have their own supporters based on aesthetics or for historical reasons, but for a user, the services are quite similar in functionality. What interests us in particular is the process of uploading presentation files to these services.

From a technical point of view, the process is the same in both cases: a user chooses a file, uploads it, writes the title and other meta information, then clicks a button to publish the presentation. From a psychological point of view, the process is also the same: uploading a file is a pure passive wait because the user has no control over the uploading process. Neither has the user options other than cancelling the upload altogether. But the **interfaces for this process differ** between SlideShare and Speaker Deck.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb964ee-ad7b-408c-a1ec-13dcd8057ef1/slideshare-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8874ec89-bfb0-42e6-b61d-c6a76a6125e0/slideshare-500px-opt.png" alt="SlideShare vs. Speaker Deck" /></a>
	<figcaption>SlideShare (top) and Speaker Deck have rather different interfaces for the same operation of uploading slides. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb964ee-ad7b-408c-a1ec-13dcd8057ef1/slideshare-opt.png">View large version</a>)</figcaption>
</figure>

The good part first. Looking at these screenshots we can see how the services employ tolerance management for the process of uploading a file: the form suggests filling out the meta information not after, but _while_ the file is being uploaded, thereby catering for P1 (occupied time feels shorter than unoccupied time) and P2 (people want to get started) propositions in Maister’s list. Instead of keeping the user passively waiting, the user’s brain is instantly triggered into the active phase by the suggestion of filling out this form.

But can you spot the difference between the two? I am sure you can: the two different progress indicators on Speaker Deck. And this is where things get out of control. The second progress indicator not only adds some confusion to the interface, it also significantly slows down the process as perceived by the user. With SlideShare, my presentation file had been uploaded the moment I finished filling out the form, hence I didn’t feel any delay or passive wait. But with Speaker Deck, even though my file had been uploaded comparably fast (the first progress indicator), I still **had to wait for the second process to finish** before my slides could be visible. And even if I could click the **Save the Details** button, it does exactly that – only saves the details while my presentation is still being processed. The situation gets worse because nothing in the interface tells the user what to expect after the “processing” is finished: will a user get any benefit that is _worth the wait_?

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/924c495b-04c5-4c76-ad78-59d11aa78a32/speakerdeck-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f0b477d-5b8c-44d2-b160-e52010837059/speakerdeck-500px-opt.png" alt="Speaker Deck processing a file" /></a>
	<figcaption>Speaker Deck keeps processing the slides for much longer than it takes a user to fill out the form with presentation details, eliminating any positive effects of the tolerance management. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/924c495b-04c5-4c76-ad78-59d11aa78a32/speakerdeck-opt.png">View large version</a>)</figcaption>
</figure>

In this comparison, SlideShare shows **impressive use of the tolerance management technique**: users barely notice the passive wait while uploading files to the service. On the other hand, the same functionality at Speaker Deck, while employing the same technique at first, eliminates its success further in the process.

With tolerance management at hand, we could extend [the performance optimization strategy](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#conclusion-for-now), provided in part 2, to get the full picture of basic techniques for managing objective time, perception and tolerance in our projects.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d31a3b74-f078-457f-8246-2c01b8545cfb/conclusion-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278a7120-b548-49e8-a4bc-e4069117e6ce/conclusion-500px-opt.png" /></a></figure>

<blockquote>
<p><a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#part-1-objective-time">Part I: Objective time management</a></p>
		<ul>
			<li><a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#the-need-for-performance-optimization-the-20-rule">The 20% rule</a>: to beat your own performance.</li>
			<li><a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/#neutralization-or-chasing-the-leader">Neutralization</a>: to level the competition.</li>
		</ul>

<p><a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">Part II: Perception management</a></p>
		<ul>
			<li><a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#preemptive-start">Preemptive start</a>: keep the user in the active phase for as long as possible before switching to the passive wait.</li>
			<li><a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#early-completion">Early completion</a>: give the user something to work with by switching from a passive to active wait as soon as possible.</li>
		</ul>

<p><a href="#tolerance-management">Part III: Tolerance management</a></p>
<p>Anything that helps your users stay away from the harmful influence of the uncertain wait. Consider <a href="#progress-indicators">progress indicators</a>, switching fully to an active wait, or <a href="#beyond-indicators">combining multiple techniques at once</a>.</p>
</blockquote>

But, be it objectively or psychologically, should we make everything as fast as possible? As you can guess, this is not yet the end.</p>

## Easy, Tiger!

“Are there moments when intentionally adding a few extra seconds—however artificial—creates a better experience?” asks Stephen P. Anderson in his article “[Wait for It …](https://uxmas.com/2013/wait-for-it)”. Let’s figure this out.

Last year, [discussion about a placebo progress bar](https://www.youtube.com/watch?feature=youtu.be&v=gpBWwl-Ngak&app=desktop) on the website of South Africa's [First National Bank](https://www.fnb.co.za/) made [respected minds claim it to be some sort of nonsense](https://twitter.com/brad_frost/status/505183790621536257). But let’s not rush to judgement.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d685f290-f338-4f19-801c-4bc26253d5bc/placebo-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47e49500-86f5-4edb-bc80-77014901e1e3/placebo-500px-opt.png" /></a>
	<figcaption>A placebo progress bar on the website of First National Bank raised a lot of controversy. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d685f290-f338-4f19-801c-4bc26253d5bc/placebo-opt.png">View large version</a>)</figcaption>
</figure>

First of all, as [William J. McEwen writes](https://www.amazon.com/Married-Brand-Consumers-Bond-Brands/dp/1595620052/), “Faster can be better – but only when speed is exactly what the customer wants. Not all customers want to complete every contact with a company at lightning speed.” Do you like it when a bank website hurries you? The website provides an _online interface_ to the _offline interactions_ that a user can relate to in real life. Users have **expectations** about these operations and usually these interactions with banks do not happen at the speed of light.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8735b05e-c1d9-44d2-a860-1d34f7b8fd6f/not-so-fast-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08c8dbaf-de9a-4596-822b-376e2c5c70b3/not-so-fast-500px-opt.png" /></a>
	<figcaption>Not everything should be as fast as possible. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8735b05e-c1d9-44d2-a860-1d34f7b8fd6f/not-so-fast-opt.png">View large version</a>)</figcaption>
</figure>

Second, by adding this progress indicator, the bank tries to cultivate a particular **emotional design quality**: the idea of a complex product with many benefits. “A lot of things that are really valuable take time,” says Darrell Worthy, an assistant professor of psychology at Texas A&M University. This echoes Maister’s P7: the more valuable the service, the longer the customer will wait. The bank is not serving fast food; it is not expected to deliver results instantly. Simply by delaying its response to an average user (that is, without developer tools and a hunger for sensation), the bank tries to manage users’ expectations, building the _perceived value_ of the service. By the way, progress indicators on [Little Big Room](https://www.little-big-room.com/) mentioned above, similar to the progress indicator at First National Bank, are not connected to any real process as well: they manage expectation and have a function different from simple progress indication.

This brings us to the following point – as long as you don’t introduce a genuinely new way of interaction or operation, your users already have certain expectations of it. Sometimes, speeding up a process confounds those expectations and puts the user out of countenance, significantly reducing the perceived value of your service. In the long run, this might be more destructive than a slower process.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54cb4d12-6199-4a10-8eda-8a50b68df9b0/bed-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c813d0a-47ec-4f58-b8a1-4c462491f600/bed-500px-opt.png" /></a>
	<figcaption>In some cases speeding up a process significantly reduces the perceived value of your service. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54cb4d12-6199-4a10-8eda-8a50b68df9b0/bed-opt.png">View large version</a>)</figcaption>
</figure>

"Everything's got a moral, if only you can find it,” said the Duchess in <cite>Alice’s Adventures in Wonderland</cite>. And this article humbly tries to communicate its own lesson. The performance and speed of our projects are very important, without a doubt. But they have to meet users’ expectations and needs before we slake our thirst for speed. A good developer knows how to make a website faster; an excellent developer knows when and why to do so. Know your users, know your tools and deliver your best.</p>

<figure>
	<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10fcbd99-6c47-4a27-8bb4-7803794c24eb/finish-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97b91faa-b80b-42dc-a6dd-bb7f18c83792/finish-500px-opt.png" alt="" /></a>
	<figcaption>Everything comes to an end. And here's the end event marker of this article.</figcaption><br>
</figure>

### Endnotes

<a name="endnote1"></a><sup>1</sup> According to a number of studies like the ones by [M. Masson et al](https://link.springer.com/article/10.3758%2FBF03196973) and [K. Rayner](https://www.ncbi.nlm.nih.gov/pubmed/9849112), the reading speed for an average reader (native English speaker reading in English) is around 250 words per minute, or about 4 words per second. The graphical elements shown randomly at tripmydream.com contain 16–24 words; this means that to read and, most importantly, understand the textual information, an average user would need 4–6 seconds. And indeed, the pictures change every 6 seconds on average.

But these studies review reading speed for texts isolated from other distracting elements. Owing to [saccadic suppression](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2787621/) (the fact that we do not perceive information during an eye movement), the more elements on the page, the more time users need to process and understand the information.

Moreover, [P. Carroll et al](https://link.springer.com/chapter/10.1007%2F978-1-4612-2852-3_27) found that when presented with a captioned drawing, users tend to focus more on the drawing than on the caption, hence it requires more time to process textual information provided together with a drawing. This means that: a) being a supportive element, the illustrated character unnecessarily drags the user’s attention away from other more important elements, diluting their effect; and b) to read and understand the textual information coming with the drawings, users need more than six seconds. There is a risk in changing the picture during the reading process; instead of managing tolerance, this builds up frustration.

{{< signature "ml, al, vf" >}}

