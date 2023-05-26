---
title: True Lies Of Optimistic User Interfaces
slug: true-lies-of-optimistic-user-interfaces
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87765cf3-5aa6-4906-8176-b4f4a51ef508/optimistic-ui1-preview-opt.png
date: 2016-11-15T19:58:59.000Z
author: denys-mishunov
description: >-
  Three user interfaces (UIs) go to a pub. The first one orders a drink, then
  several more. A couple of hours later, it asks for the bill and leaves the pub
  drunk. The second UI orders a drink, pays for it up front, orders another
  drink, pays for it and so on, and in a couple of hours leaves the pub drunk.

  The third UI exits the pub already drunk immediately after going in — it knows
  how the pubs work and is efficient enough not to lose time. Have you heard of
  this third one? It is called an "optimistic UI.
categories:
  - UX
  - User Interaction
  - UX
  - UI
---
Three user interfaces (UIs) go to a pub. The first one orders a drink, then several more. A couple of hours later, it asks for the bill and leaves the pub drunk. The second UI orders a drink, pays for it up front, orders another drink, pays for it and so on, and in a couple of hours leaves the pub drunk. The third UI exits the pub already drunk immediately after going in — it knows how the pubs work and is efficient enough not to lose time. Have you heard of this third one? It is called an "optimistic UI."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8081fa16-60dc-488f-8f83-5e6fc3018f44/optimistic-ui-large-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b6e8004-86c9-4b07-ae83-9fe8d114bdc3/optimistic-ui-650-opt.png" alt="optimistic ui" title="Optimistic UI – True Lies" width="650" height="428" /></a><figcaption>Optimistic UI design is not about looking at the web through rose-colored glasses — at least not <strong>only</strong> about it. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8081fa16-60dc-488f-8f83-5e6fc3018f44/optimistic-ui-large-opt-1.png">View large version</a>)</figcaption></figure>

Recently, having discussed <a href="https://vimeo.com/184659742">psychological performance optimization</a> at a number of conferences dedicated to both front-end development and UX, I was surprised to see how little the topic of optimistic UI design is addressed in the community. Frankly, the term itself is not even well defined. In this article, we will find out what concepts it is based on, and we will look at some examples as well as review its psychological background. After that, we will review the concerns and main points regarding how to maintain control over this UX technique.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The User Is The Anonymous Web Designer](https://www.smashingmagazine.com/2010/10/the-user-is-the-anonymous-web-designer/)
*   [<span class="headline">Designing Card-Based User Interfaces</span>](https://www.smashingmagazine.com/2016/10/designing-card-based-user-interfaces/)
*   [<span class="headline">Conversational Interfaces: Where Are We Today?</span>](https://www.smashingmagazine.com/2016/07/conversational-interfaces-where-are-we-today-where-are-we-heading/)

{{% feature-panel %}}

But before we begin, truth be told, no single thing could be called an "optimistic UI." Rather, it is the mental model behind the implementation of an interface. Optimistic UI design has its own history and rationale.</p>

## Once Upon A Time

A long while ago — when the word "tweet" applied mostly to birds, Apple was on the verge of bankruptcy and people still put fax numbers on their business cards — web interfaces were quite ascetic. And the vast majority of them had not even a hint of optimism. An interaction with a button, for example, could follow a scenario similar to the following:

1.  The user clicks a button.
2.  The button is triggered into a disabled state.
3.  A call is sent to a server.
4.  A response from the server is sent back to the page.
5.  The page is reloaded to reflect the status of the response.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e759f9-31ac-4524-a939-4a7314a97eee/old-ui-large-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db8f14f-18fb-44c9-8f58-b59e0d21ee02/old-ui-650-opt.png" alt="" width="650" height="360" /></a><figcaption>In the old days, interfaces were nowhere nearly as optimistic. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46e759f9-31ac-4524-a939-4a7314a97eee/old-ui-large-opt-1.png">View large version</a>)</figcaption></figure>

This might look quite inefficient in 2016; however, surprisingly enough, the same scenario is still used in a lot of web pages and applications and is still a part of the interaction process for many products. The reason is that it is predictable and more or less error-proof: The user knows that the action has been requested from the server (the disabled state of the button hints at this), and once the server responds, the updated page clearly indicates the end of this client-server-client interaction. The problems with this kind of interaction are quite obvious:

*   The user has to wait. By now, we know that even the shortest delay in the server's response time has a [negative effect on the user's perception](https://blog.radware.com/applicationdelivery/applicationaccelerationoptimization/2013/12/mobile-web-stress-the-impact-of-network-speed-on-emotional-engagement-and-brand-perception-report/) of the entire brand, not only on this particular page.
*   Every time the user gets a response to their action, it is presented in quite a destructive way (a new page loads, instead of the existing one being updated), which breaks the context of the user's task and might affect their [train of thought](https://en.wikipedia.org/wiki/Train_of_thought). Even though we are not necessarily talking about [multitasking](https://www.apa.org/research/action/multitask.aspx) in this case, any switch of mental context is unpleasant. So, if an action is not inherently meant to switch contexts (online payment is a good example of when a switch is natural), switching would set up an unfriendly tone of dialogue between user and system.</p>

## Good Not-So-Old Days

Then, the so-called Web 2.0 arrived and provided new modes of interaction with web pages. The core of these were XMLHttpRequest and AJAX. These new modes of interaction were complemented by "spinners": the simplest form of progress indicator, the sole purpose of which was to communicate to the user that the system is busy performing some operation. Now, we did not need to reload the page after getting a response from the server; we could just update a part of the already-rendered page instead. This made the web much more dynamic, while allowing for smoother and more engaging experiences for users. The typical interaction with a button could now look like this:

1.  The user clicks a button.
2.  The button is triggered into a disabled state, and a spinner of some kind is shown on the button to indicate the system is working.
3.  A call is sent to the server.
4.  A response from the server is sent back to the page.
5.  The visual state of the button and the page are updated according to the response status.

This new interaction model addressed one of the aforementioned problems of the old method of interaction: The update of the page happens without a destructive action, keeping the context for the user and engaging them in the interaction much better than before.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcdc6fb6-fb45-4824-883f-0a27bb09ac26/spinner-ui-large-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbd63811-a11c-436b-bad2-935c7c60d0b3/spinner-ui-650-opt.png" alt="" width="650" height="360" /></a><figcaption>XMLHttpRequest and spinners solved one of the issues of the old methods of interaction: a destructive switch of context after the server's response. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcdc6fb6-fb45-4824-883f-0a27bb09ac26/spinner-ui-large-opt-1.png">View large version</a>)</figcaption></figure>

This kind of interaction pattern has been widely used everywhere in digital media. But one issue remains: Users still have to wait for a response from the server. Yes, we can make our servers respond faster, but no matter how hard we try to speed up the infrastructure, users still have to wait. Again, users do not like to wait, to put it mildly. For example, <a href="https://www.techradar.com/news/world-of-tech/roundup/consumers-dump-slow-websites-1080742">research shows</a> that 78% of consumers feel negative emotions as a result of slow or unreliable websites. Moreover, <a href="https://www.marketwired.com/press-release/tealeaf-announces-new-mobile-transaction-research-conducted-harris-interactive-shows-1419058.htm">according to a survey</a> conducted by Harris Interactive for Tealeaf, 23% of users confess to cursing at their phones, 11% have screamed at them, and a whole 4% have actually thrown their phone when experiencing a problem with an online transaction. Delays are among those problems.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c225eef6-c683-475d-975c-33dee2d632a1/cursing-phone-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bb58513-041f-40c1-8138-d6d533730423/cursing-phone-650-opt.png" alt="" width="650" height="410" /></a><figcaption>About 78% of consumers feel negative emotions as a result of slow or unreliable websites. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c225eef6-c683-475d-975c-33dee2d632a1/cursing-phone-large-opt.png">View large version</a>)</figcaption></figure>

Even if you show some kind of progress indicator while the user waits, unless you are very <a href="https://dribbble.com/shots/1901531-Loading">creative with the indicator</a>, nowadays that is simply not enough. For the most part, people have gotten accustomed to spinners indicating a system's slowness. Spinners are now more associated with <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">purely passive waiting</a>, when the user has no option other than either to wait for the server's response or to close the tab or application altogether. So, let's come up with a step to improve this kind of interaction; let's look at this concept of an optimistic UI.</p>

## Optimistic UI

As mentioned, an optimistic UI is nothing more than a way of handling human-computer interaction. To understand the main ideas behind it, we will stick with our "user clicks a button" scenario. But the principle will be the same for pretty much any kind of interaction that you might want to make optimistic. <a href="https://books.google.com/books?id=mYicAQAAQBAJ&amp;lpg=PA503&amp;dq=%22hopeful+and+confident+about+the+future%22&amp;pg=PA503&amp;redir_esc=y#v=onepage&amp;q=%22hopeful%20and%20confident%20about%20the%20future%22&amp;f=false">According to the Oxford English Dictionary</a>:
<blockquote><strong>op-ti-mis-tic</strong>, <em>adj.</em> hopeful and confident about the future.</blockquote>

Let's begin with the "confident about the future" part.

What do you think: How often does your server return an error on some user action? For example, does your API fail often when users click a button? Or maybe it fails a lot when users click a link? Frankly, I don't think so. Of course, this might vary based on the API, server load, level of error-handling and other factors that you, as the front-end developer or UX specialist, might not be willing to get involved in. But as long as the API is stable and predictable and the front end properly communicates legitimate actions in the UI, then the number of errors in response to actions initiated by the user will be quite low. I would go so far as to state that they should never go above 1 to 3%. This means that in 97 to 99% of cases when the user clicks a button on a website, the server's response should be success, with no error. This deserves to be put in a better perspective:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1efc3269-df7f-427e-89b7-33e8d15e7724/failure-success-man-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af4b8870-31e7-4b59-9070-082fad8bb730/failure-success-man-650-opt.png" alt="" width="650" height="533" /></a><figcaption>Optimistic UIs are based on the assumption that when the user clicks a button, the server should return a success response in 97 to 99% of cases. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1efc3269-df7f-427e-89b7-33e8d15e7724/failure-success-man-large-opt.png">View large version</a>)</figcaption></figure>

Think about it for a moment: If we were 97 to 99% certain about a success response, we could be confident about the future of those responses — well, at least much more confident about the future than Schrödinger's cat was. We could write a whole new story about button interaction:

1.  The user clicks a button.
2.  The visual state of the button is triggered into success mode instantly.

That's it! At least from the user's point of view, there is nothing more to it — no waiting, no staring at a disabled button, and not yet another annoying spinner. The interaction is seamless, without the system crudely stepping in to remind the user about itself.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6d472f1-41db-47c6-8c08-a71654aca153/optimistic-ui1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63fcb5c0-14d9-401a-9194-7bee4e4db8ce/optimistic-ui1-650-opt.png" alt="" width="650" height="292" /></a><figcaption>An optimistic UI interaction has no place for either a disabled button or a spinner. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6d472f1-41db-47c6-8c08-a71654aca153/optimistic-ui1-large-opt.png">View large version</a>)</figcaption></figure>

From the developer's point of view, the complete cycle looks like this:

1.  The user clicks a button.
2.  The visual state of the button is triggered into success mode instantly.
3.  The call is sent to the server.
4.  The response from the server is sent back to the page.
5.  In 97 to 99% of cases, we know that the response will be success, and so we don't need to bother the user.
6.  Only in the case of a failed request will the system speak up. Don't worry about this for now — we will get to this point later in the article.

Let's look at some examples of optimistic interactions. You are probably familiar with "like" buttons, as found on Facebook and Twitter. Let's take a look at the latter.

It starts, obviously enough, with the click of the button. But note the visual state of the button when the user is no longer pressing or hovering over the button. It switches to the success state instantly!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e5c32f-f0d8-4ee9-8c3c-ee3218843a3a/twitter1-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e5c32f-f0d8-4ee9-8c3c-ee3218843a3a/twitter1-preview-opt.png" alt="" width="351" height="69" /></a><figcaption>After the like button is clicked, Twitter instantly updates it to the success state visually.</figcaption></figure>

Let's see what's happening in the "Network" tab of our browser's developer tools at this very moment.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04e402f5-1874-4791-8b11-85a5aff28b59/twitter2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e59681ee-e808-4750-b5ba-ccf2318cf314/twitter2-preview-opt.png" alt="" width="500" height="156" /></a><figcaption>The visual state of the button is updated independent of the server request, which is still in progress. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04e402f5-1874-4791-8b11-85a5aff28b59/twitter2-large-opt.png">View large version</a>)</figcaption></figure>

The "Network" tab shows that the server request has been sent but is still in progress. The "likes" counter number has not been incremented yet, but with the change in color, the interface is clearly communicating success to the user, even before having gotten a response from the server.

After a successful response is received from the server, the counter is updated, but the transition is much subtler than the instant color change. This provides the user with a smooth, uninterrupted experience, without any perceived waiting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a871729b-7d45-4fcc-a3d9-b38d9625d384/twitter3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fdea739-1912-4e21-ab48-8ab227b63f2d/twitter3-preview-opt.png" alt="" width="500" height="178" /></a><figcaption>While the like button is visually in success mode, the counter is updated only after the server response confirms success. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a871729b-7d45-4fcc-a3d9-b38d9625d384/twitter3-large-opt.png">View large version</a>)</figcaption></figure>

Another example of optimistic interaction is seen on Facebook, with its own like button. The scenario is quite similar, except that Facebook updates the counter instantly, together with success color of the button, without waiting for the server's response.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddf97bb3-fdf1-45b7-82e2-5eaf054a9fa4/fb-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddf97bb3-fdf1-45b7-82e2-5eaf054a9fa4/fb-preview-opt.png" alt="" width="500" height="" /></a><figcaption>Facebook employs the same optimistic interaction as Twitter, except that it updates the counter instantly along with the button's visual state.</figcaption></figure>

One thing to note here, though. If we look at the server's response time, we'll see that it is a little over <strong>1 second</strong>. Considering that the <a href="https://developers.google.com/web/fundamentals/performance/rail?hl%3Den%23response_respond_in_under_100ms">RAIL model recommends</a> <strong>100 milliseconds</strong> as the optimal response time for a simple interaction, this would normally be way too long. However, the user does not perceive any wait time in this case because of the optimistic nature of this interaction. Nice! This is another instance of <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/"><strong>psychological</strong> performance optimization</a>.

But let's face it: There is still that 1 to 3% chance that the server will return an error. Or perhaps the user is simply offline. Or, more likely, perhaps the server returns what is technically a success response but the response contains information that has to be further processed by the client. As a result, the user will not get a failure indicator, but we cannot consider the response a success either. To understand how to deal with such cases, we should understand why and how optimistic UIs work psychologically in the first place.

## The Psychology Behind Optimistic UIs

So far, I have not heard anyone complain about the aforementioned optimistic interactions on the major social networks. So, let's say that these examples have convinced us that optimistic UIs work. But why do they work for users? They work simply because people hate waiting. That's it, folks! You can skip to the next part of the article.

But if you're still reading, then you are probably interested in knowing why it is so. So, let's dig a bit deeper into the psychological ground of this approach.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa917814-3133-463c-964f-28be12bc860c/psychology-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c3df465-bd45-4e14-9ada-e909df3ed4ca/psychology-650-opt.png" alt="" width="650" height="581" /></a><figcaption>Brain studies help us to understand the psychology behind why optimistic UIs work. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa917814-3133-463c-964f-28be12bc860c/psychology-large-opt.png">View large version</a>)</figcaption></figure>

An optimistic UI has two basic ingredients that are worth psychological analysis:

*   the fast response to the user's action;
*   the handling of potential failures on the server, on the network and elsewhere.</p>

### Fast Response to User Action

When we talk about optimistic UI design, we're talking about an optimal response time in human-computer interaction. And recommendations for this type of communication have been around since as far back as 1968. Back then, Robert B. Miller published his seminal piece "<a href="https://www.computer.org/csdl/proceedings/afips/1968/5072/00/50720267.pdf">Response Time in Man-Computer Conversational Transactions</a>" (PDF), in which he defines as many as 17 different types of responses a user can get from a computer. One of those types Miller calls a "response to control activation" — the delay between the depressing of a key and the visual feedback. Even back in 1968, it should have not exceeded 0.1 to 0.2 seconds. Yes, the <a href="https://developers.google.com/web/fundamentals/performance/rail">RAIL model</a> is not the first to recommend this — the advice has been around for about 50 years. Miller notes, though, that even this short delay in feedback might be far too slow for skilled users. This means that, ideally, the user should get acknowledgement of their action within <strong>100 milliseconds</strong>. This is getting into the range of one of the fastest unconscious actions the human body can perform — an eye blink. For this reason, the 100-millisecond interval is usually perceived to be instant. "Most people blink around 15 times a minute and a blink lasts on average 100 to 150 milliseconds," <a href="https://www.ucl.ac.uk/media/library/blinking">says Davina Bristow</a>, of University College London's Institute of Neurology, adding that this "means that overall we spend at least 9 days per year blinking."

Because of its instant <strong>visual</strong> response (even before the actual request has finished), an optimistic UI is one of the examples of the <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">early-completion</a> techniques used in psychological performance optimization. But the fact that people like interfaces that respond in the blink of an eye should not come as a surprise to most of us, really. And it's not hard to achieve either. Even in the old days, we disabled buttons instantly after they were clicked, and this was usually enough to acknowledge the user's input. But a disabled state in an interface element means <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">passive waiting</a>: The user cannot do anything about it and has no control over the process. And this is very frustrating for the user. That's why we skip the disabled state altogether in an optimistic UI — we communicate a positive outcome instead of making the user wait.</p>

### Handling Potential Failure

Let's get to the second interesting psychological aspect of optimistic UI design — the handling of potential failure. In general, plenty of information and articles are available on how to handle UI errors in the best possible way. However, while we will see how to handle failure later in this article, what matters most in an optimistic UI is not how we handle errors, but when we do it.

Humans naturally organize their activity into clumps, terminated by the completion of a subjectively defined purpose or sub-purpose. Sometimes we refer to these clumps as a "<a href="https://en.wikipedia.org/wiki/Train_of_thought">train of thought</a>," a "<a href="https://www.unco.edu/cebs/psychology/kevinpugh/motivation_project/resources/flow6.pdf">flow of thought</a>" (PDF) or simply a "<a href="https://en.wikipedia.org/wiki/Mihaly_Csikszentmihalyi%23Flow">flow</a>." The flow state is characterized by peak enjoyment, energetic focus and creative concentration. During a flow, the user is completely absorbed in the activity. A <a href="https://twitter.com/tameverts/status/783800032436695040">tweet by Tammy Everts</a> nicely illustrates this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b329a72-4074-45a6-9bfc-edc873319910/tammy-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9df3fdf-8acd-41c8-ab3f-207de50db886/tammy-preview-opt.png" alt="" width="500" height="472" /></a><figcaption>Sometimes, spotting a person in a flow state is pretty easy. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b329a72-4074-45a6-9bfc-edc873319910/tammy-large-opt.png">View large version</a>)</figcaption></figure>

On the web, the durations of such clumps of activity are much shorter. Let's revisit Robert B. Miller's work for a moment. The response types he cites include:

*   a response to a simple inquiry of listed information;
*   a response to a complex inquiry in graphic form;
*   a response to "System, do you understand me?"

He ties all of these to the same <strong>2-second</strong> interval within which the user should get the relevant type of response. Without digging deeper, we should note that this interval also depends on a person's <a href="https://www.simplypsychology.org/working%20memory.html">working memory</a> (referring to the span of time within which a person can keep a certain amount of information in their head and, more importantly, be able to manipulate it). To us, as developers and UX specialists, this means that within 2 seconds of interacting with an element, the user will be in a flow and focused on the response they are expecting. If the server returns an error during this interval, the user will still be in "dialogue" with the interface, so to speak. It's similar to a dialogue between two people, where you say something and the other person mildly disagrees with you. Imagine if the other person spent a long time nodding in agreement (the equivalent of our indication of a success state in the UI) but then finally said "no" to you. Awkward, isn't it? So, an optimistic UI must communicate failure to the user within the 2 seconds of the flow.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b9cd01d-beed-4d7d-9d29-a0d467daaf5b/optimistic-ui2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45438159-096b-4352-8dd0-2d469d160d99/optimistic-ui2-650-opt.png" alt="" width="650" height="403" /></a><figcaption>An optimistic UI must clearly yet carefully communicate failure to the user. Most importantly, it should happen within the 2 seconds of the user's flow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b9cd01d-beed-4d7d-9d29-a0d467daaf5b/optimistic-ui2-large-opt.png">View large version</a>)</figcaption></figure>

Armed with the psychology of how to handle failure in an optimistic UI, let's finally get to those 1 to 3% of failed requests.</p>

## The Pessimistic Side Of Optimistic UI Design

By far, the most common remark I hear is that optimistic UI design is a kind of black pattern — cheating, if you will. That is, by employing it, we are lying to our users about the result of their interaction. Legally, any court would probably support this point. Still, I consider the technique a prediction or hope. (Remember the definition of "optimistic"? Here is where we allow some room for the "hopeful" part of it.) The difference between "lying" and "predicting" is in how you treat those 1 to 3% of failed requests. Let's look at how Twitter's optimistic "like" button behaves offline.

First, in line with the optimistic UI pattern, the button switches to the success state right after being clicked — again, without the user pressing or hovering over the button any longer, exactly as the button behaves when the user is online.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01c0b548-7753-4987-b2cb-80247a8823cb/twitter-offline1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d98e79ec-59aa-49ee-b2ad-78013632f355/twitter-offline1-preview-opt.png" alt="" width="500" height="91" /></a><figcaption>When offline, Twitter's like button is still visually updated after being clicked. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01c0b548-7753-4987-b2cb-80247a8823cb/twitter-offline1-large-opt.png">View large version</a>)</figcaption></figure>

But because the user is offline, the request fails.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36a8517-2e1e-485c-ae41-602ac966b213/twitter-offline2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194ff94e-9e17-4375-bfa0-0208c6fee615/twitter-offline2-preview-opt.png" alt="" width="500" height="167" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36a8517-2e1e-485c-ae41-602ac966b213/twitter-offline2-large-opt.png">View large version</a>)</figcaption></figure>

So, as soon as possible within the user's flow, the failure should be communicated. Again, 2 seconds is usually the duration of such a flow. Twitter communicates this in the subtlest way possible, simply by reverting the button's state.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1fbdd7-9985-4688-841d-9a60a787a8b6/twitter-offline3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3b2b26e-f197-4441-afb7-6485c74d698e/twitter-offline3-preview-opt.png" alt="" width="500" height="151" /></a><figcaption>After the failed request, Twitter subtly reverts the visual state of the like button, without any visual fuss. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd1fbdd7-9985-4688-841d-9a60a787a8b6/twitter-offline3-large-opt.png">View large version</a>)</figcaption></figure>

The conscientious reader here might say that this failure-handling could be taken one step further, by actually notifying the user that the request could not be sent or that an error has occurred. This would make the system as transparent as possible. But there is a catch — or, rather, a series of issues:

*   Any sort of notification that appears suddenly on screen would switch the user's context, prompting them to analyze the reason behind the failure, a reason that would probably be presented in the error message.
*   As with any error message or notification, this one should guide the user in this new context by providing actionable information.
*   That actionable information would set yet another context.

OK, by now we can all agree that this is getting a bit complicated. While this error-handling would be reasonable for, say, a large form on a website, for an action as simple as clicking a like button, it's overkill — both in terms of the technical development required and the working memory of users.

So, yes, we should be open about failure in an optimistic UI, and we should communicate it as soon as possible so that our optimism does not become a lie. But it should be proportional to the context. For a failed like, subtly reverting the button to its original state should be enough — that is, unless the user is liking their significant other's status, in which case the thing better work all the time.</p>

### Extreme Pessimism

One other question might arise: What happens if the user closes the browser tab right after getting a success indicator but before the response is returned from the server? The most unpleasant case would be if the user closes the tab before a request has even been sent to the server. But unless the user is extremely nimble or has the ability to slow down time, this is hardly possible.

If an optimistic UI is implemented properly, and interactions are applied only to those elements that never wait longer than 2 seconds for a server response, then the user would have to close the browser tab within that 2-second window. That's not particularly difficult with a keystroke; however, as we've seen, in 97 to 99% of cases, the request will be successful, whether the tab is active or not (it's just that a response won't be returned to the client).

So, this problem might arise only for those 1 to 3% who get a server error. Then again, how many of those rush to close the tab within 2 seconds? Unless they're in a tab-closing speed competition, I don't think the number will be significant. But if you feel this is relevant to your particular project and might have negative consequences, then employ some tools to analyze user behavior; if the probability of such a scenario is high enough, then limit optimistic interaction to non-critical elements.

I intentionally haven't mentioned cases in which a request is artificially delayed; these do not generally fall under the umbrella of optimistic UI design. Moreover, we have spent more than enough time on the pessimistic side of things, so let's summarize some main points about implementing a good optimistic UI.</p>

## Rules Of Thumb

I sincerely hope this article has helped you to understand some of the main concepts behind optimistic UI design. Perhaps you're interesting in trying out this approach in your next project. If so, here are some things to keep in mind before you begin:

*   A prerequisite to everything we've talked about so far: Make sure the API you're relying on is stable and returns predictable results. Enough said.
*   The interface should catch potential errors and problems _before_ a request is sent to the server. Better yet, totally eliminate anything that could result in an error from the API. The simpler a UI element is, the simpler it will be to make it optimistic.
*   Apply optimistic patterns to simple binary-like elements for which nothing more than a success or failure response is expected. For example, if a button click assumes a server response such as "yes," "no" or "maybe" (all of which might represent success to varying degrees), such a button would be better off without an optimistic pattern.
*   Know your API's response times. This is crucial. If you know that the response time for a particular request never goes below 2 seconds, then sprinkling some optimism over your API first is probably best. As mentioned, an optimistic UI works best for server response times of less than 2 seconds. Going beyond that could lead to unexpected results and a lot of frustrated users. Consider yourself warned.
*   An optimistic UI is not just about button clicks. The approach could be applied to different interactions and events during a page's lifecycle, including the loading of the page. For example, [skeleton screens](https://www.lukew.com/ff/entry.asp?1797) follow the same idea: You predict that the server will respond with success in order to fill out placeholders to show to the user as soon as possible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4c95d14-ef9b-485d-b04d-fb2791e9480b/finish-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c9aab24-f3fa-4c42-9eb2-0c439033a318/finish-650-opt.png" alt="" width="650" height="287" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4c95d14-ef9b-485d-b04d-fb2791e9480b/finish-large-opt.png">View large version</a>)</figcaption></figure>

Optimistic UI design is not really a novelty on the web, nor is it a particularly advanced technique, as we have seen. It is just another approach, another mental model, to help you manage the <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/">perceived performance</a> of your product. Being grounded in the psychological aspects of human-computer interaction, optimistic UI design, when used intelligently, can help you to build better, more seamless experiences on the web, while requiring very little to implement. But, in order to make the pattern truly effective and to keep our products from lying to users, we must understand the mechanics of optimistic UI design.</p>

### Resources

*   "[Response Time in Man-Computer Conversational Transactions](https://theixdlibrary.com/pdf/Miller1968.pdf)" (PDF), Robert B. Miller, Fall Joint Computer Conference, 1968
*   "[Introducing RAIL: A User-Centric Model for Performance](https://www.smashingmagazine.com/2015/10/rail-user-centric-model-performance/)," Paul Irish, Paul Lewis, Smashing Magazine, 2015
*   "[Mobile Web Stress: The Impact of Network Speed on Emotional Engagement and Brand Perception](https://blog.radware.com/applicationdelivery/applicationaccelerationoptimization/2013/12/mobile-web-stress-the-impact-of-network-speed-on-emotional-engagement-and-brand-perception-report/)," Tammy Everts, Radware Blog, 2013
*   [_Applications of Flow in Human Development and Education_](https://www.springer.com/gp/book/9789401790932), Mihaly Csikszentmihalyi, 2014
*   "[Mobile Design Details: Avoid the Spinner](https://www.lukew.com/ff/entry.asp?1797)," Luke Wroblewski, 2013
*   "[Why Performance Matters, Part 2: Perception Management](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/)," Denys Mishunov, Smashing Magazine, 2015

{{< signature "rb, al, il" >}}

