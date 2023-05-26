---
title: 'A Designer’s Guide To Better Decisions'
slug: designers-guide-better-decisions
author: eric-olive
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5cd5d74-2a79-40d2-8145-b0d7946b37f8/eric-olive-designer-guide.png
date: 2019-04-29T12:30:16+02:00
summary: >-
  Design involves decisions, and those decisions are often flawed because our brains are wired for survival. The same brain features that literally helped us survive in the wild do not serve us well in the 21st-century workplace. Learn why we often fall into four common decision traps and how to avoid them.
description: >-
  Design involves decisions, and those decisions are often flawed because our brains are wired for survival. Learn why we often fall into four common decision traps and how to avoid them.
categories:
  - Workflow
  - UX
  - Business
  - Design
---
Nearly everyone has experienced frustration while using a website, mobile app, or web application. In these moments, we might wonder “What were they thinking?” followed by “They sure were not thinking about making this easy for me.” One reason we encounter such frustrating moments is that the process of making sound and user-friendly decisions is difficult.

In this article, we’ll identify four decision-related traps that impede good design and offer techniques for avoiding these traps. These decision traps are based on research conducted by psychologists, neuroscientists, molecular biologists, and behavioral economists including several cited in this article.

Too many design decisions occur in isolation, are based on gut feel, or are not carefully examined. **The web offers many examples of poor design decisions**. For instance, let’s take a look at the example below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c90d1dc1-78b0-46b8-8317-ccc9f74a3815/help-text-field.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c90d1dc1-78b0-46b8-8317-ccc9f74a3815/help-text-field.png" sizes="100vw" caption="<em>On the left:</em> Are they asking for city, state, or country? <em>On the right:</em> This tooltip does not answer the user’s question. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c90d1dc1-78b0-46b8-8317-ccc9f74a3815/help-text-field.png'>Large preview</a>)" alt="A field in a form asking users to enter the place of birth. And Hover text that says: 'Please enter the place of birth of your parent.'" >}}

At first glance, it seems quite straightforward: type the place of birth in the text field. A moment’s reflection, however, raises a question. Should we type the country, state, or city? It’s not clear. Clicking the question mark icon displays the help text shown below, to the right. The problem? The text does not answer the question; it simply restates the original request about entering the place of birth.

The design shown above violates a basic tenet of user experience (UX) immortalized by the title of Steven Krug’s famous book *Don’t Make Me Think*. Sure, it’s an amusing title, but he’s serious. The entire field of user experience is based on the idea of reducing the user’s cognitive load:

<blockquote>“Just like computers, human brains have a limited amount of processing power. When the amount of information coming in exceeds our ability to handle it, our performance suffers.”<br /><br />&mdash; <a href="https://www.nngroup.com/articles/minimize-cognitive-load/">Kathryn Whitenton</a></blockquote> 

In other words, when a design requires users to guess or think too hard about something as simple as one text entry, users will often make mistakes (costing your organization time and money) or abandon the task altogether.

Lightening the user’s cognitive load means increasing our own cognitive load as designers. We *do* have to think, hard and carefully. Essential to this effort is learning how to make good design decisions.

{{% feature-panel %}}

There are four common decision traps that we often fall into. I’ll explain how you can avoid them.

<ol>
	<li><a href="#availability-heuristic">Availability Heuristic</a></li>
	<li><a href="#focalism-bias">Focalism Bias</a></li>
	<li><a href="#optimism-bias">Optimism Bias</a></li>
	<li><a href="#overconfidence-bias">Overconfidence Bias</a></li>
</ol>

## 1. Availability Heuristic

A heuristic is a mental shortcut that helps us make decisions quickly. These mental shortcuts are essential in certain situations. For example, if a car veers into your lane, you must act quickly; you don’t have time to review several options.

Unfortunately, heuristics become a flaw when making decisions in situations where many factors and participants must be considered. One such flaw is the availability heuristic, which involves **an incomplete examination of current and past information**.

A particularly distressing example of the availability heuristic in the design space is the software on the Boeing 737 Max. As of this writing, it appears that this software contributed to the tragedy of the downed airplanes. People around the world have asked how to prevent such tragedies in the future.

Part of the answer lies in avoiding quick fixes. [Airbus](https://www.nytimes.com/2019/03/23/business/boeing-737-max-crash.html), Boeing’s chief competitor, had refitted their A320 planes with larger engines. Boeing felt pressured to do the same leading to a variety of changes:

<blockquote>“The bigger engines altered the aerodynamics of the plane, making it more likely to pitch up in some circumstances.”</blockquote>

To compensate, Boeing added new software to the 737 Max:

<blockquote>This software “would automatically push the nose down if it sensed the plane pointing up at a dangerous angle. The goal was to avoid a stall. Because the system was supposed to work in the background, Boeing believed it didn’t need to brief pilots on it, and regulators agreed. Pilots weren’t required to train in simulators.”</blockquote>

The obvious and horrifying conclusion is that Boeing engineers and designers were placed under immense pressure to re-design the 737 Max at record speed resulting in a series of misjudgments. Less obvious, but equally troubling, is the likely role of the availability heuristic in these tragedies.

In short, the information used to make critical design decisions was not sufficient and resulted in tragedy.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d86fd35-85b2-4732-bd7b-760353dad152/availability-heuristic.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d86fd35-85b2-4732-bd7b-760353dad152/availability-heuristic.png" sizes="100vw" caption="The availability heuristic limits our perspective (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d86fd35-85b2-4732-bd7b-760353dad152/availability-heuristic.png'>Large preview</a>)" alt="Small red circle within a much larger blue circle" >}}

### Solution

One solution is for designers to identify their area of competence. Within this sphere their intuitions are likely to serve them well, explains author Rolf Dobelli in *The Art of Thinking Clearly*. For example, UX designers should feel comfortable making decisions about layout and interaction design issues like flow, navigation, and how much information to present at one time.

When designers face a decision outside their circle of competence, it’s worth taking time to apply hard, slow, rational thinking. For example, when designing cockpit software for jets, **designers would be well advised to work closely** with engineers and pilots to ensure that everything in the proposed user interface (UI) is precise, accurate, and provides the information pilots need *when* they need it.

We are all subject to the availability heuristic. Designers must strive to mitigate this heuristic by consulting a variety of subject matter experts (SMEs), not simply the programmers and engineers on their immediate teams. The downside risk is simply too high.

{{% ad-panel-leaderboard %}}

## 2. Focalism Bias

The availability heuristic hinders our ability to assess current and past information. The focalism bias concerns our ability to look forward. It refers to the inclination to concentrate on a single point when considering the future. As Harvard psychologist Daniel Gilbert explains in his book *Stumbling on Happiness*:

<blockquote>“It is difficult to escape the focus of our own attention &mdash; difficult to consider what it is we may not be considering.”</blockquote>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9a56c74-c55d-4da1-a4bc-adb069cc6cbd/focalism.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9a56c74-c55d-4da1-a4bc-adb069cc6cbd/focalism.jpg" sizes="100vw" caption="The focalism bias restricts our view of the future. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9a56c74-c55d-4da1-a4bc-adb069cc6cbd/focalism.jpg'>Large preview</a>)" alt="Camera lens showing a nature scene in focus" >}}

For example, while my colleagues and I were conducting UX research for a U.S. government agency, we discovered that caseworkers could not access information essential to processing applications for medical assistance.

As shown in the diagram below, these caseworkers literally had to stop in the middle of the application process in order to request critical information from another division. Typically, caseworkers had to wait 24 to 48 hours to receive this information.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894c99e1-0a03-4eb5-adf4-dedfb9f8cc57/diagram-caseworkers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894c99e1-0a03-4eb5-adf4-dedfb9f8cc57/diagram-caseworkers.png" sizes="100vw" caption="The focalism bias led to a delay, the opposite of the desired results. Our re-design resolved the issue. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/894c99e1-0a03-4eb5-adf4-dedfb9f8cc57/diagram-caseworkers.png'>Large preview</a>)" alt="Diagram listing many steps before re-design and fewer steps after re-design" >}}

Caseworkers found this delay stressful because it made it more difficult to meet a federal law requiring all applications to be processed within 10 days of receipt.

How did this happen? One reason, surprisingly, was the **emphasis on deadlines**. Through our observation and interviews, we learned that the system had been rushed into production to meet a project deadline (all too common) and to give caseworkers a way to process applications more efficiently.

The intentions were good, the goals made sense. Unfortunately, the focus on rushing a system into production to supposedly expedite the process had the opposite effect. Designers created a system that *delayed* the application process.

### Solution: Become An Active Problem Seeker

This idea may sound counterintuitive. Why would we look for problems? Don’t we already have enough to deal with? In truth, however, organizations that seek problems, such as Toyota, often demonstrate impressive performance. They’re called high-reliability organizations (HROs). Other examples include the U.S. Navy's aircraft carriers and air traffic control centers in the U.S., both of which have incredibly low error and failure rates.

As decision expert Michael Roberto of Bryant University explains, leaders of HROs do not wall themselves off from the possibility of failure. On the contrary, they **preoccupy themselves with failure**. For example, they:

<ul>
<li>Do not simplify explanations.</li>
<li>Remain sensitive and attentive to their front-line operations as we did while observing caseworkers.</li>
<li>Defer to those who have the local, specialized knowledge as opposed to those who simply have authority in the hierarchy. Again, we relied on the expertise of caseworkers on the ground.
</li>
<li>Commit to resilience, to the notion that you cannot prevent all small problems. Rather, the goal is to focus on fixing these small problems before they mushroom into large problems.</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bea7638d-1747-4d33-b044-a116e21507c1/active-problem-seeker.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bea7638d-1747-4d33-b044-a116e21507c1/active-problem-seeker.png" sizes="100vw" caption="Actively seeking problems leads to better decisions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bea7638d-1747-4d33-b044-a116e21507c1/active-problem-seeker.png'>Large preview</a>)" alt="Man standing on a mountain looking out with binoculars" >}}

Problems are not the enemy; hidden problems are because these hidden problems become serious threats down the road as we saw in the government agency examples outlined above. In both cases, earlier and additional contextual inquiry (observing users in their natural home or work environments) would likely have identified current problems and possible UI solutions to these problems.

<p class="c-pre-sidenote--left">For example, while conducting contextual inquiry for a large Mexican bank, I observed customers trying (and failing) to transfer money to family members who held accounts at different banks. Customers expressed frustration at this limitation because they wanted an easy way to send money to family members, especially those who lived far away.</p><p class="c-sidenote c-sidenote--right">While living in Mexico, I learned that loaning and giving money to family members is more common in Mexico than in the U.S., Canada, or parts of Western Europe.</p>

Given the deeply rooted Mexican tradition of supporting family members in financial need, I was initially surprised by this banking limitation. Upon reflection, however, I realized that this limitation was simply a hidden problem. When coding the banking web site, the developers were likely focused on security, paramount in all matters financial. They had not considered including a cross-bank transfer feature.

I identified this missing feature by conducting UX Research with banking customers in Mexico. This real-world example shows how critical it is to become an active problem seeker.

{{% ad-panel-leaderboard %}}

## 3. Optimism Bias

Focusing on a single point or problem impedes our ability to plan and design for the future. An equally troubling challenge is the optimism bias. We tend to imagine the best-case scenario.

<blockquote>“For example, we underrate our chances of getting divorced, being in a car accident, or suffering from cancer. We also expect to live longer than objective measures would warrant, overestimate our success in the job market, and believe that our children will be especially talented.”<br /><br />&mdash; <a href="https://www.sciencedirect.com/science/article/pii/S0960982211011912">Tali Sharot</a></blockquote>

In design culture, this bias sounds like this:

<blockquote>“Sure, this part of the UI is a bit clunky, but customers will get used to it, and then it won’t be an issue.”</blockquote>

In other words:

<blockquote>“We need to ship the product; we don’t want to deal with the cumbersome interaction.”</blockquote>

As anyone who has conducted a survey or usability test knows, this optimism is misplaced. Users and customers are easily frustrated and often show little patience when products and UIs are hard to use.

I witnessed this bias when designing a web application for financial advisers &mdash; 70% of whom were male. The client insisted on using a red font to emphasize certain numbers. Even after I explained that approximately 9% of males are color blind, she refused to change the font color. She reasoned that financial advisers would see the numbers in context. In other words, no problem. When I conducted multiple rounds of usability testing, however, two male advisers struggled to distinguish the numbers in red. They could read those numbers, but the figures did not stand out.

The reason for this type of wishful thinking is our tendency to see the future as a variant of the present. **We tend to assume that things will go on more or less as they have**. In the case of the financial application, because advisers had not complained before so my client assumed that they would not complain in the future. What she failed to grasp was the significance of changing the font to red.

As author [David DiSalvo](https://www.amazon.com/Makes-Brain-Happy-Should-Opposite/dp/1616144831/ref=sr_1_fkmrnull_1?keywords=What+Makes+Your+Brain+Happy+and+Why+You+Should+Do+the+Opposite&qid=1556268006&s=books&sr=1-1-fkmrnull) explains:

<blockquote>“We tend to simulate the future by re-constructing the past, and the re-construction is rarely accurate.”</blockquote>

### Solution: The Pre-Mortem Technique

That’s why it’s essential to resist this innate tendency by leveraging techniques like psychologist Gary Klein’s pre-mortem. The idea is to describe **a scenario in which the project failed to meet a specific goal** such as a revenue target, an increase in the percentage of new purchases, requests for more information, etc.

Here’s how it works. Before committing to a major initiative, the key stakeholder (often an executive) gathers everyone who is slated to participate. She outlines the key objective and explains “what went wrong.” The statement will sound something like this:

<blockquote>“Imagine that we have rolled out a new e-commerce mobile app at a cost of $3 million with a projected revenue of $10 million for the first year. At the end of one year, revenue is $1 million, a huge failure. Please take 20 minutes to write a history of this failure.”</blockquote>

This pre-mortem exercise:

<ul>
<li>Legitimizes doubt by providing a safe space for asking questions and expressing concerns about the decision.</li>
<li>Encourages even supporters of the decision to search for threats not previously considered.</li>
</ul>

An e-commerce mobile app is simply an example. The pre-mortem technique can be applied to nearly any project in any industry because it’s about expanding our perspective in order to identify what could realistically go wrong.

## 4. Overconfidence Bias

We unconsciously exaggerate our ability to accurately assess the present and predict the future. A study of patients who died in a hospital ICU compared the doctor’s diagnosis to the actual autopsy results. The doctors who were completely confident in their diagnosis were [wrong 40% of the time](https://www.amazon.com/Thinking-Fast-Slow-Daniel-Kahneman/dp/0374533555/ref=sr_1_1?keywords=Thinking+Fast+and+Slow&qid=1556267989&s=books&sr=1-1).

When designers fall prey to the overconfidence bias, they exaggerate their ability to understand how users think. The most common results are **information overload and confusing terminology** and controls (buttons, checkboxes, sliders, and so on).

For example, while evaluating a client’s tablet-based investment application targeted at lay people, my team and I immediately noticed that:

<ul>
<li>The screen where users would create a risk profile included extraneous information.</li>
<li>The phrase “time zone” would likely confuse users. The client intended the term to refer to the customer’s investment time horizon. Yet, “time zone” usually means the time in a country or region, such as the U.K. or South Africa.</li>
<li>Plus and minus controls exhibited low affordance meaning that it was hard to tell whether they could be tapped or were simply part of the display.</li>
</ul>

These observations were supported during a subsequent usability test when participants expressed confusion over these specific points. In short, the designers for this project had overestimated their ability to create an interface that users would understand.

### Solution

One solution is to conduct user research as we did with the tablet-based financial application outlined above. If such research is not possible, a second solution is to actively seek case studies beyond your immediate context. For example:

<ul>
<li>If you are designing an investment application, it might make sense to **refer to banking applications** to identify potential design challenges and what is already working well for customers.</li>
<li>If you are designing a tablet application to help nurse practitioners make a preliminary diagnosis, **look to other projects that are related** but outside your immediate context. Has your company developed a medical device UI for surgeons or ER doctors? What worked well for users? What did not?</li>
</ul>

Referring to other projects may sound like a no-brainer. Ask yourself, however, how often a systematic review of previous, related (but not identical) projects occurs within your organization. Remember, we are all subject to overconfidence.

## Conclusion

In this piece, we’ve identified four common decision traps and corresponding solutions:

<ol>
<li>The <strong>availability heuristic</strong> causes us to ignore potentially important current or past information when making decisions. The solution is to expand our perspective by reaching beyond our circle of competence. For designers, this often means consulting highly technical experts.</li>
<li>Closely related is the <strong>focalism bias</strong>, our tendency to concentrate on a single point when designing thus overlooking other, equally important factors. The solution is to actively seek problems in order to identify and address hidden problems now before they become even larger difficulties. </li>
<li>The <strong>optimism bias</strong> refers to our tendency to imagine the best-case scenario. The solution is the pre-mortem technique. In this exercise, we imagine that a design project has gone terribly wrong and discuss why and how this happened. As with active problem seeking, the idea is to identify issues before they occur or get worse.</li>
<li>In the design space, the <strong>overconfidence bias</strong> refers to exaggerating our ability to understand how users think and design accordingly. The solution is to conduct user research and seek case studies similar to the current design initiative.</li>
</ol>

The cognitive biases discussed here are not intended to criticize designers (I am one). Rather, they are scientific observations about human nature. While we can’t change our biology, we can remain mindful of this biology and apply the four solutions outlined in this article. In so doing, we will increase the chances of creating better, safer, and more engaging designs.

### Resources

- “[Minimize Cognitive Load To Maximize Usability](https://www.nngroup.com/articles/minimize-cognitive-load/),” Kathryn Whitenton, Nielsen Norman Group
- “[The Optimism Bias](https://www.sciencedirect.com/science/article/pii/S0960982211011912),” Tali Sharot, ScienceDirect
- “[Don’t Make Me Think](https://www.amazon.com/Dont-Make-Think-Revisited-Usability/dp/0321965515/ref=sr_1_1?keywords=Don%27t+Make+Me+Think&qid=1556267858&s=gateway&sr=8-1),” Steve Krug
- “[Stumbling On Happiness](https://www.amazon.com/Stumbling-Happiness-Daniel-Gilbert/dp/1400077427/ref=sr_1_1?keywords=Stumbling+on+Happiness&qid=1556267950&s=books&sr=1-1),” Daniel Gilbert
- “[The Art of Thinking Clearly](https://www.amazon.com/Art-Thinking-Clearly-Rolf-Dobelli/dp/0062219693/ref=sr_1_1?keywords=The+Art+of+Thinking+Clearly&qid=1556267967&s=books&sr=1-1),” Rolf Dobelli
- “[Thinking Fast And Slow](https://www.amazon.com/Thinking-Fast-Slow-Daniel-Kahneman/dp/0374533555/ref=sr_1_1?keywords=Thinking+Fast+and+Slow&qid=1556267989&s=books&sr=1-1),” Daniel Kahneman
- “[What Makes Your Brain Happy and Why You Should Do the Opposite](https://www.amazon.com/Makes-Brain-Happy-Should-Opposite/dp/1616144831/ref=sr_1_fkmrnull_1?keywords=What+Makes+Your+Brain+Happy+and+Why+You+Should+Do+the+Opposite&qid=1556268006&s=books&sr=1-1-fkmrnull),” David DiSalvo
- “[Why Great Leaders Don’t Take Yes For An Answer](https://www.amazon.com/Great-Leaders-Dont-Take-Answer/dp/0134392787/ref=sr_1_fkmrnull_1?keywords=Why+Great+Leaders+Don%E2%80%99t+Take+Yes+for+an+Answer&qid=1556268031&s=books&sr=1-1-fkmrnull),” Michael Roberto

{{< signature "ah, yk, il" >}}