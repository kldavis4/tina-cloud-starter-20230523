---
title: 'Using Ethics In Web Design'
slug: using-ethics-in-web-design
author: mortenrandhendriksen
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b14c66a-7eb3-4d5a-a82c-dcc341020eba/ethics-of-web-design-image3.png
date: 2018-03-22T16:30:06+01:00
summary: >-
  Developers and designers need to initiate a conversation about the ethics of web design, i.e. how do we define and measure goodness and rightness in the digital realm? It's important to discuss responsibilities, decisions, and consequences.
description: >-
  Developers and designers need to initiate a conversation about the ethics of web design, i.e. how do we define and measure goodness and rightness in the digital realm? It's important to discuss responsibilities, decisions, and consequences.
categories:
  - Ethics
  - Opinion Column
  - Design
  - UX
---
Every design decision is a decision made on behalf of other people, those we often refer to as "end-users." As the creators of designed experiences used by people all over the world, it is our responsibility to think carefully about how our decisions impact the person on the other end of the conversation. Even small and seemingly insignificant decisions can have enormous implications, and ethics can help ensure the longevity of our designs and help us carve paths to better futures for everyone.

Earlier this month, a friend reached out with a question:

<blockquote>How hard would it be to use the processing power of computers visiting their site to mine for cryptocurrencies?</blockquote>

The first I heard of cryptocurrency mining (cryptojacking for short) through websites was a news story from September 2017 about [a script found on the website](https://www.theverge.com/2017/9/26/16367620/showtime-cpu-cryptocurrency-monero-coinhive) of a TV network called *Showtime*. Since then, similar scripts have appeared on everything from government websites to good old-fashioned blogs. Sometimes [the scripts are put there by hackers](https://www.wired.co.uk/article/browsealoud-ico-texthelp-cryptomining-how-cryptomining-work) (first documented by [Scott Helme](https://twitter.com/Scott_Helme/status/962684239975272450)), other times by the site developers themselves.

The most recent example is from the folks at [Salon](https://www.salon.com/) who are [testing out cryptojacking as an alternative revenue stream](https://arstechnica.com/information-technology/2018/02/salon-to-ad-blockers-can-we-use-your-browser-to-mine-cryptocurrency/) from visitors who use ad blockers:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6580d039-47c4-40da-8ee3-d4d3f58a2720/ethics-of-web-design-image1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6580d039-47c4-40da-8ee3-d4d3f58a2720/ethics-of-web-design-image1.png" sizes="100vw" caption="Salon.com FAQ page about ad blockers and cryptojacking. (<a href='https://www.salon.com/about/faq-what-happens-when-i-choose-to-suppress-ads-on-salon/'>Source</a>)" alt="Screenshot of Salon.com FAQ page" >}}

{{% feature-panel %}}

In response, I told my friend “this is an ethical question more than a practical one” and sent a series of questions back:

1. What world are you building for your visitors? What capabilities are you granting or enabling?
2. What kind of person do you become by doing this, and is that the kind of person you aspire to be?
3. Would you want every other person in your position to make the same decision you just made? Are you upholding your duties of care?
4. Does this improve the lives of everyone affected?

I created these questions as a basis of an ethical framework for design decisions. They enable us to think not just about [what, how, and why](https://www.ted.com/talks/simon_sinek_how_great_leaders_inspire_action) we do things but also _to what end_ and they remind us to put “ought” before “can” when decisions need to be made.

"Ethics" is the word du jour in tech, and it's for a good reason. As the connected age emerges into adulthood, we are coming to terms with the consequences of decisions made in garages and coffee shops and dorm rooms years ago; solutions built to keep us engaged are distorting our understanding of reality. Platforms built to connect us are becoming breeding grounds of hatred and division. It turns out that even small choices can have a monumental impact when amplified through a user base of billions.

It's about time that we, the people who build the web, initiate **a conversation about where we are and where we want to go**, about how we define and measure goodness and rightness in the digital realm, about responsibility, about decisions and consequences, about building something bigger than our own apps. **It is time we talk about the ethics of web design**.

In this article, we will cover:

- The current state of ethics in design and technology;
- The basic design ethics framework;
- How to evaluate consequences of our work;
- What norms and expectations are we establishing with our work;
- What type of person do we become in the process;
- What environments are we building for the end-user;
- The *Ethical Principles of Web Design* (checklist)

## Ethics And Design

Every design decision is a decision made on behalf of our users. As the creators of designed experiences used by people all over the world, it is our responsibility to think carefully about not just *how* we do something at a technical level or what goals we are trying to achieve for ourselves or our clients or companies, but *why* we do it and *how* our decisions impact the person on the other end of the conversation. With every decision, we have the shared opportunity and responsibility to think about the ethics of web design, not just as a high flying ideal about doing no harm or doing the right thing, but as **a fundamental part of our everyday process**.

Rather than a wet moralistic blanket covering the fires of creativity, I aim to show how ethics can be the hearth that makes our creative fires burn brighter, without burning down the house.

The good news is we are not heading into an unexplored wilderness. The world of ethics is well traveled and the cowpaths are all but paved. For centuries, philosophers have grappled with the same questions we now face in the tech industry: how to make decisions that bring more good than bad into the world, to whom and for what we are responsible, how to measure success not just in more wealth for ourselves but also in the betterment of life for everyone. Using their theories as our foundation, we can establish a framework for the ethics of web design that help us make better decisions for everyone both today and in the future.

{{% pull-quote %}}Ethics is not about making a list of good and bad acts, it’s about creating a method for evaluating each decision and each act from an ethical perspective.{{% /pull-quote %}}

## Ethical Principles In The Tech Community

Ethics can and should be [a core component of web design](https://medium.com/@monteiro/designs-lost-generation-ac7289549017) and [computer sciences in general](https://www.nytimes.com/2018/02/12/business/computer-science-ethics-courses.html). The challenge is that ethics is not a label, it’s a practice. In the tech community, ethical principles tend toward grand statements and nice sounding rules like “don’t be evil” or “do the right thing” without anchoring these rules in the solid foundation of an ethical framework. These rules provide an air of ethical decision making while laying the groundwork for moral relativism.

It’s easy enough to say “do no harm,” but if you don’t also define what you mean by “harm”, to whom this harm can be done, and who judges whether or not harm has been done, these words have little to contribute except to make us feel good. If we say we want to do good but don’t have clearly established definitions of what good is, how we judge whether something is good, and why we want to do good in the first place, we have effectively granted ourselves a license to do anything we want &mdash; a textbook example of subjective moral relativism.

On the flipside, if some industry or government body makes a list of good and bad acts and declares it the law of the web design lands without providing an ethical framework to make and test these judgments, the door is opened to authoritarian moralism and the inevitable stifling of creativity.

## We Need An Ethical Framework

<p class="c-pre-sidenote--left">Ethics can provide a framework for careful consideration of the decisions we make and their outcomes, and give us the tools to make better decisions and think more broadly about the implications of our work and actions. An ethical framework for web design should provide tools to objectively judge the value of individual decisions and actions based on agreed-upon principles. Rather than declare every decision or act of a certain type always good or bad, it should grant us the ability to see every decision in its context and judge it based not only on its intentions or outcomes but also on whether it should be a best practice, what virtues it promotes, and what capabilities it grants and enables for those affected.
I propose we use the lessons from four moral philosophies as the <a href="https://en.wikipedia.org/wiki/Pier_(architecture)#Bridge_piers">piers</a> of a bridge to carry future web designers over the ethical marshlands we find ourselves mired in.</p>

<p class="c-sidenote c-sidenote--right">In this context the term “web designer” is a broad umbrella covering anyone who makes decisions about the function, functionality, appearance, and interactivity of a web experience, and “web design” a term covering the craft and work of a web designer. Though we commonly think of a “web designer” as the person literally designing the appearance of what is displayed on a screen, the reality is everyone &mdash; from back-end developers through information architects, content strategists, UX and UI designers, even content creators &mdash; makes design decisions that impact the experience of the people who use our creations. Databases are designed. So are content models and navigation patterns and taxonomy structures and headlines.</p>

## Ethical Framework (The Short Version)

Before we dive in, let me give you the short version: a mnemonic device that will help you see where we’re going in this article and help you remember to check the *Ethical Principles of Web Design* every time a decision is made. I call it the "Bridge of Ethics":

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb14020-ab4a-42fd-8a35-e025d3861f1f/ethics-of-web-design-image2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb14020-ab4a-42fd-8a35-e025d3861f1f/ethics-of-web-design-image2.png" sizes="100vw" caption="The Ethical Bridge with its four piers: Capability Approach, Virtue Ethics, Deontology, and Consequentialism." alt="Illustration of a bridge with four piers" >}}

The *Bridge of Ethics* allows a designer to cross ethical marshlands by passing over four piers representing the four moral philosophies covered in this article. Each pier has central questions to be answered:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Capability Approach</th>
			<th>Virtue Ethics</th>
			<th>Deontology</th>
			<th>Consequentialism</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>What world are you building for the end-user? What capabilities are you granting or enabling?</td>
			<td>What type of person do you become in the process?</td>
			<td>What norms and expectations are you establishing? Are you upholding your duties of care?</td>
			<td>What are the consequences of your decision? Do they improve the common good of those affected?</td>
		</tr>
	</tbody>
</table>

When evaluating a new design decision, start from the left establishing what capabilities you grant or enable in the end-user and then move to the right. When evaluating an existing design or service, start from the right establishing the consequences created by the decision and move to the left.

With that image in your head, let’s get crackin’!

## A Practical Example To Lead The Way

To make sense of how the *Ethics of Web Design* would work in a real setting, I’ve built this article around a practical example which looks at how we can use ethics to tackle one of the hard problems of the web: Making money from publishing content online.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b14c66a-7eb3-4d5a-a82c-dcc341020eba/ethics-of-web-design-image3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b14c66a-7eb3-4d5a-a82c-dcc341020eba/ethics-of-web-design-image3.png" sizes="100vw" caption="" alt="'We Make Things' illustration" >}}

Meet Maiken and Kenneth, cat aficionados and online entrepreneurs. They have an online store where they sell products, some of their own creation, some as resellers. Now they want to set up a website where they share tips and tricks about their passion (cats) and earn a bit of passive income in the process.

Ever since web design and development became accessible to the masses, everyone from bloggers to website- and web service owners have tried to figure out how to turn online content into cold hard cash. The first, and most prominent way of doing this is through online advertising; placing ads throughout the site, either in dedicated areas or intermingled with the content, and charging the advertisers either based on impression (someone sees the ad), interaction (someone clicks the ad), or both.

Maiken and Kenneth see advertising as a possible revenue stream and want to implement advertising in an ethical way. This brings us to the first pier of the Bridge of Ethics:

## 1. Consequentialism: The Many Before The Few

The predominant ethical theory in most industries is [consequentialism](https://en.m.wikipedia.org/wiki/Consequentialism), more specifically [utilitarianism](https://en.m.wikipedia.org/wiki/Utilitarianism) ([more in-depth analysis](https://www.iep.utm.edu/util-a-r/)). In short, an act that benefits the majority is considered good even if a minority suffers as a result because the overall utility of the act is positive. To put an edge on it, in consequentialism the ends justify the means, and in utilitarianism, any act is considered good if the resulting benefits outweigh the costs.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da93ed9-a3cf-4131-b7d5-c70983d47d3a/ethics-of-web-design-image4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da93ed9-a3cf-4131-b7d5-c70983d47d3a/ethics-of-web-design-image4.png" sizes="100vw" caption="" alt="Illustration of web site banners pushing users to act" >}}

### Utilitarianism In The Tech Space

Consequentialist and Utilitarian ethics are woven into every aspect of the tech space. We find them in our decision making processes and procedures any time we base our decisions on their overall utility: “Will the majority of our users benefit from this new feature?” “Can this bug be ignored since it only impacts a small percentage of users?” “Can we make this decision on behalf of our users to reduce the complexity of the interface?”

From a business standpoint, this makes sense: If the majority of users are happy, the business thrives. But this approach also opens the door to implicit or explicit bias and discrimination: If the only thing that matters is maximizing utility, ignoring or causing harm to a minority becomes acceptable. This is further complicated by our inability to accurately predict the consequences of our decisions and look at a situation from a neutral position devoid of our own privilege and bias.

### Utilitarianism Puts Marginalized Groups On The Sidelines

A prime example of this is web accessibility. For decades web designers have used utilitarianism as an excuse for not building accessible web solutions. Arguments around complexity, cost, and “design limitations” are in reality judgments of utility: Web designers often conclude that the utility gained by people dependent on accessible solutions is outweighed by the utility of time-, cost-, and design efficiency gained by not considering accessibility.

And accessibility is not the only example. As an example, consequentialist ethics can be used to justify underserving or outright ignoring users of inexpensive technologies with older browsers on slower networks in rural areas and countries we can’t place on a map. Talk to any front-end web developer about Internet Explorer support, and you’ll see this in action.

### Different vantage points

When Maiken and Kenneth explore the ethics of placing advertisements on their website, they first need to look at their decision from the perspective of a consequentialist: Do the ads on the website maximize utility for the affected parties?

If we look at the ads in isolation, the answer is a resounding “no.” Very few people want to be exposed to ads, and those ads are often distracting, reduce performance, and “cheapen” the experience of visiting the site. If, on the other hand, we zoom out a bit, it can be argued that ads maximize utility because ads on a page pay for the content and access to it. The site owner pays the cost of content creation and hosting through ad revenues, the consumer pays for access by letting themselves be exposed to ads.

Does that mean Maiken and Kenneth have the consequentialist stamp of approval to put ads on their site? It depends.

### Consequentialism’s blind spot

When we use maximizing utility as a measure for the rightness or wrongness of an act, we have to remember consequentialism has a massive blind spot: The future. Considering only immediate consequences, or only consequences within ideal use cases, will invariably lead to unintended and often problematic events further down the road. In their book, *[Design for Real Life](https://abookapart.com/products/design-for-real-life)*, authors Eric Meyer and Sara Wachter-Boettcher provide multiple examples of this, including Facebook’s “Year In Review” feature [surfacing cheerful photos of Meyer’s daughter](https://meyerweb.com/eric/thoughts/2014/12/24/inadvertent-algorithmic-cruelty/) who passed away earlier that year. Unless we take steps to ensure we think beyond the immediate consequences of our decisions, bad things may well happen just beyond the horizon. This is exactly what happened when we made advertising the primary revenue model for the web.

When ad revenue is calculated from impressions and interactions (clicks), the value being traded is attention, a finite resource granted to the site by its visitors. The more attention the visitor gives a site, the more ad revenue the site owner receives. This creates an environment where the site owner will start building content and interactions with the explicit goal of keeping the attention of their visitors and expose them to ads. In theory, this seems like a good thing. We’d all like to believe better quality content gets more attention. The reality is not as rosy.

### How Utilitarianism Influenced Elections

Online ads are primarily served up by two companies: Google and Facebook. These companies share the same interest as the site owners: grabbing the attention of the visitors. To do this, social media sites and video sharing sites and search engines have created “personalized” streams where [algorithms figure out what type of content an individual is engaged by](https://www.theguardian.com/technology/2018/feb/02/how-youtubes-algorithm-distorts-truth) and subject them to more of the same content. You can see this for yourself: Go to YouTube and watch a video of something new, like a song by [Animals as Leaders](https://www.youtube.com/watch?v=NmfzWpp0hMc), and your recommended stream will suddenly skew toward jazz metal, a musical genre you might not even have known existed just a few minutes ago. Watch more videos, and Google pegs you as “fan of jazz metal” and “likely interested in non-standard guitars.”

To make this personalization as accurate as possible, advertising services use pervasive tracking and surveillance to follow users as they travel from site to site and create models of what type of content they are most likely to spend time looking at. The same services then use their other platforms (search, social media, video/photo sharing) to expose you to more of the same, whether that be jazz metal, cute cats, or partisan politics.

This phenomenon has a name: "[Filter bubble](https://en.wikipedia.org/wiki/Filter_bubble)." We were warned of these personalized echo chambers in which web users find vastly different content when making the same searches &mdash; skewed to their personal, political, and religious convictions [years ago](https://www.ted.com/talks/eli_pariser_beware_online_filter_bubbles).

In short, advertising as a revenue model for the web led to user tracking, filter bubbles, fake news, and eventually worldwide political upheaval.

With this in mind, does advertising pass the consequentialist test? Does it maximize utility? No. At least not the type of predatory advertising we see today.

That doesn’t mean Maiken and Kenneth can’t have advertising on their site; it just means they have to think carefully about what type of advertising they use. That’s where the first pier of the Bridge of Ethics, the *Consequentialist Principles of Web Design*, comes in:

### Using Consequentialism in Web Design

Consequentialist and Utilitarian ethics reminds us to consider the consequences of our actions and to measure their utility. When using consequentialism, we need to be aware of its shortcomings: It’s easy to imagine short-term consequences, much harder to see long-term consequences. And we can’t grant ourselves license to put the benefits of some users over the disadvantages of others, even when doing so maximizes utility. This is especially important when the benefits of a company or its shareholders are weighed against the disadvantages of marginalized users. Being cognizant of these issues we can draw on the best qualities of this theory:

#### The Consequentialist Principles Of Web Design:

1. Prioritize the increased utility for all over maximizing utility for the majority.
2. Provide sufficient remedies for those disadvantaged as a consequence of a decision.
3. Expect unexpected outcomes.
4. Favor iterative enhancements over permanent solutions.

To put these principles into practice, use a consequentialist checklist at the bottom of the article to guide decision-making processes.

When Maiken and Kenneth use these principles to evaluate advertising as a revenue model for their site, they are able to draw several conclusions:

- Ads disadvantage visitors by adding distraction and increasing load times, To avoid this, they must keep ads to a minimum, and place them in areas of the layout that do not distract the visitor from the content.
- Ad networks track user behavior not only on their site but on other sites. When someone visits a site, they do not have a reasonable expectation of being tracked by an ad network. For the visitor, utility is harmed by such software, in particular, because it contributes to trapping them in filter bubbles. Therefore, ad networks are not an option for this project.
- For full transparency, visitors need to know why they are being exposed to advertising on the site and what type of relationship the site owners have to the advertisers. A short blurb explaining why there are ads on the site (i.e. “we use ads to pay for hosting costs and to give you free content”) and clear indicators any time there is a relationship between the site owners and the advertisers are required.
- Direct marketing such as affiliate links must be marked as such. Any time the site owner financially benefits from a visitor clicking a button, they are incentivized to get the visitor to click that button. This can lead to misleading and coercive designs and content and must be avoided.

Based on this, Maiken and Kenneth realize that while they are able to use ads in an ethical way, eliminating ad networks as an option means doing direct ad sales and managing the ads on their own or hiring someone to do it for them. Either way, it adds time, complexity, and cost to the project, so they put ads on hold as they look for other less labor intensive options.

One new revenue model that pops up is using visitor computers to mine for cryptocurrencies. This brings us to the second pier of the Bridge of Ethics:

## 2. Deontology: The Rule Of Moral Duty

[Deontological Ethics](https://en.wikipedia.org/wiki/Deontological_ethics) (also known as ['Duty' or 'Obligation Ethics'](https://plato.stanford.edu/entries/ethics-deontological/)) judges the rightness or wrongness of an action based on defined rules. Compared to consequentialism, the moral judgment of an act in deontology is based on the act itself &mdash; not its consequence. If an act was performed in obligation to the rules, it is considered a good act even if the consequence is a bad one.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3d0447-b65e-44ef-9d26-13e501e49822/ethics-of-web-design-image5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3d0447-b65e-44ef-9d26-13e501e49822/ethics-of-web-design-image5.png" sizes="100vw" caption="" alt="Illustration of web site that is imploding" >}}

### Deontology In Web Design

Deontological ethics are found throughout our society and in our professional spaces. We choose not to harm others or steal their property because we have an obligation to follow rules of law and we believe others have that same obligation. We follow ethical protocols not to harass or assault our co-workers because we have an obligation to respect the freedom and security of person in all people, and we believe others have that same obligation.

A clear example of deontology in web design is web standards: There is no higher reason why we must follow web standards to create a web document, but we do so anyway because we have a duty of care; to the site owner who wants their message communicated to the visitor; to the visitor who wants the document to render properly in their browser; to the browser who wants to parse content it can understand; to the web community members who want to build new web documents without having to create separate solutions for each browser and device.

### Challenges of deontology

This example also illustrates the challenge of deontology. It rests on one key assumption: You don’t merely follow the rules because they exist, you follow them because you have a duty to do so and want everyone else to feel and act on that same duty. Which raises some obvious questions:

Who makes the rules? What authority do they have to impose those rules on us? And why do we have a duty to follow them? In web design, there are no clear answers, in large part because unlike other professions web design has no unified professional leadership or authority.

Another major problem is we can’t make rules for everything, and we especially can’t make rules for things that haven’t happened yet or things that are happening for the first time.

### Act as you want every other person to act in the same situation

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8785c2b1-fee6-4880-81b9-871977679dac/ethics-of-web-design-image6.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8785c2b1-fee6-4880-81b9-871977679dac/ethics-of-web-design-image6.jpg" sizes="100vw" caption="Immanuel Kant (Image source: <a href='https://commons.wikimedia.org/wiki/File:Immanuel_Kant_(painted_portrait).jpg'>Wikimedia Commons</a>)" alt="Portrait of Immanuel Kant" >}}

Deontological philosopher Immanuel Kant tried to resolve this issue with what’s known as [Kant’s Categorical Imperative](https://en.wikipedia.org/wiki/Categorical_imperative):

<blockquote>“Act only according to that maxim by which you can also will that it would become a universal law.”</blockquote>

In plain language, this translates to something like “every time you do something, do the thing   every person should do in the same situation.” For those familiar with the Golden Rule, _“Do to others what you want them to do to you”_, this will sound familiar, though it’s not exactly the same.

According to the categorical imperative, an act is only good if it can be a _universal law_, so even if a company is OK with users posting abusive content on their platform that does not mean allowing such content on all platforms is justified and should, therefore, be a universal law.

Kant invokes universality and obligation to grant each of us license to make moral judgments without having to agree to a predefined set of rules. The categorical imperative tells each individual actor to turn the spotlight on themselves and ask if their act is one they’d want every other person to perform in the same or similar situations, and relies on the obligation to ensure this principle is followed. In other words, it asks us to judge our actions not just on whether we think they are good and want others to do the same, but whether we think everyone should do it.

### Deontology’s Blind Spot

Back to our entrepreneurs. Maiken and Kenneth do the consequentialist test on [cryptojacking using the processing power of their visitors’ computers](https://www.theverge.com/2017/9/26/16367620/showtime-cpu-cryptocurrency-monero-coinhive) and conclude this revenue stream maximizes utility: visitors use a small bit of their power to pay for access to content, and everybody walks away a bit richer, in knowledge or digital coins. Implementing this feature is also relatively easy: Several solutions provide a range of options, from [ad-like banners where the visitor can press a button to mine coin](https://arstechnica.com/information-technology/2018/02/salon-to-ad-blockers-can-we-use-your-browser-to-mine-cryptocurrency/) on the site owner’s behalf to [hidden scripts that run in the background without the visitor’s knowledge](https://www.itworldcanada.com/article/canadian-websites-victimized-by-cryptominer-hack-of-third-party-supplier/401798).

The question isn’t whether they can do it, but whether every website ought to use this technology. There is also a question whether the couple upholds their duty of care to the visitor by mining coin on their computer. That’s where the second pier of the Bridge of Ethics, the *Deontological Principles of Web Design* comes in:

### Using Deontology In Web Design

Deontology enables us to create rules and systems to enforce those rules but falls short when new situations for which there are no rules occur or edge cases are encountered. Kant’s categorical imperative can be a partial buffer for these circumstances, but applying it is tricky and often results in using the Golden Rule instead which relies too heavily on the individual actor and their personal moral beliefs. Being cognizant of these issues we can draw on the best qualities of this theory:

### The Deontological Principles of Web Design

1. Follow existing rules, best practices, and guidelines.
2. Use the categorical imperative as a starting point to creating new rules.
3. When no rule exists, use the full ethical principles of web design to create new ones.
4. Uphold the duty of care: to the client, to the user, to the information, and to the future.

To put these principles into practice use, a deontological checklist at the bottom of the article to guide decision-making processes.
Using these principles, Maiken and Kenneth evaluate the ethics of cryptojacking on visitors’ computers as a revenue stream and draw some immediate conclusions:

- This approach is transactional, trading access to content for the usage of several limited resources including electricity, internet bandwidth, and processing power. If several sites did this simultaneously, the visitor would end up with higher power and internet bills and see a significant slowdown of the performance of their computer. In other words, if everyone did it, the internet would pretty much stop working. The categorical imperative is clear here: Unless you can turn your act into a universal law, it is not ethical.
- Even if they ignore the categorical imperative, they still have a duty of care to the visitor. Because this is a transaction, it is the duty of the site owners to clearly notify the visitor of what is happening and allow them to opt into the feature. This limits the usefulness of the feature as few people would say yes to using their processing power if they had a choice. Maiken and Kenneth could remedy this by making access contingent on opting in, [effectively creating a cryptojacking paywall similar to what Salon.com is testing](https://www.engadget.com/2018/02/13/salon-readers-choose-ads-or-crypto-mining/), but that would go against the premise of their site which is to share information with everyone. It also brings up issues around paywalls, something we’ll address later.

In their discussion, they also discover one of the key issues with deontology: The theory is appealing because we are surrounded by rules and know how to follow them. But unless these rules are defined, agreed upon, and followed and there are consequences when they are broken, deontology quickly leads us to moral relativism.

Without rules, enforced by an agreed upon authority, everyone can do anything they want. And even with rules and enforcement in place, people will bend or break them to get ahead. In other words, even if they decide cryptojacking is not ethical, [some content publishers](https://modernconsensus.com/people/media/salon-ceo-crypto-monero-miners-coinhive/) and [others think it’s perfectly acceptable](https://www.businessinsider.com/salon-hijack-your-laptop-to-mine-cryptocurrency-2018-2).

So, as the saying goes, if everyone else is doing it, why can’t they? This brings us to the third pier of the Bridge of Ethics:

## 3. Virtue Ethics: Aspirational Foundations

[Virtue Ethics](https://en.wikipedia.org/wiki/Virtue_ethics) is the oldest of the ethical traditions covered in this article, and likely also the one most foreign to our way of thinking about ethics on a day-to-day basis. Where consequentialism looks at the outcomes of actions and deontology looks at the act itself, virtue ethics looks at the _actors themselves_; their _reasons_ for performing the act and _what they become_ through the act.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf336265-5aa8-405b-a312-5e8443ac4bb0/ethics-of-web-design-image7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf336265-5aa8-405b-a312-5e8443ac4bb0/ethics-of-web-design-image7.png" sizes="100vw" caption="" alt="Premium membership rewards" >}}

### A Virtuous Person Is One Who Acts As Someone Who Holds These Virtues

To understand this, we first need to understand what a virtue is, a topic that supporters of virtue ethics have debated for thousands of years.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c9b9f0-b678-43d6-b558-1d4459585d1d/ethics-of-web-design-image8.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c9b9f0-b678-43d6-b558-1d4459585d1d/ethics-of-web-design-image8.jpg" sizes="100vw" caption="Socrates statue at the Louvre (Image source: <a href='https://commons.wikimedia.org/wiki/File:Socrates_statue_at_the_Louvre,_8_April_2013.jpg'>Wikimedia Commons</a>)" alt="Image of bust of Socrates" >}}

We can turn to ancient philosophy for some guidance here. Socrates argued that virtue is knowledge: the more knowledge you acquire, the more virtuous you become and the more likely you are to make the right decisions in any circumstance. Aristotle proposed a list of 18 moral and intellectual virtues including _courage, temperance, truthfulness, modesty, intelligence, logic, good sense, and theoretical and practical wisdom_. In the millennia since, philosophers have proposed other virtues and created other systems. In the book, *[Technology and the Virtues](https://global.oup.com/academic/product/technology-and-the-virtues-9780190498511?cc=ca&lang=en&)* (published in 2016), philosopher Shannon Vallor proposes 12 “[technomoral virtues](https://www.youtube.com/watch?v=5zqDx2q7oTY)”: *Honesty*, *Self-Control*, *Humility*, *Justice*, *Courage*, *Empathy*, *Care*, *Civility*, *Flexibility*, *Perspective*, *Magnanimity*, and *Technomoral Wisdom*.
The overall principle remains the same: A virtuous person is one who acts as someone who holds a defined set of virtues.

The question facing Maiken and Kenneth, about whether other people doing something gives them license or leave to do the same, is one of virtue. To answer it they need to dig deep and consider what type of people they want to be.

### Virtue Ethics In Web design

To understand virtue ethics in web design we need to answer the question “what makes a virtuous web designer?” To answer this, we first need to decide what virtues a web designer should aspire to. There is no one true answer here, but I believe there are some virtues most web designers can agree on:

- **Knowledge**  
Know the craft and keep your skills current and up to date.
- **Care**  
Uphold the duty of care to the client, the end-user, the content, and yourself.
- **Equity**  
Be fair, and ensure every end-user can access the same content.
- **Truthfulness**  
Be honest with clients, content, end-users, and yourself.
- **Courage**  
Take intelligent risks, push norms and boundaries, move the craft forward.
- **Collaboration**  
Share knowledge, and help lift the skills of your peers.
- **Openness**  
Be transparent, and value the opinions of others and yourself.
- **Access**  
Make everything you create accessible to anyone who may encounter it.
- **Resilience**  
Push forward and learn new things. Own your mistakes and learn from them.

Let’s for a moment assume these are the virtues of web design. How can Maiken and Kenneth use them to make a decision? How can they act as someone who has these virtues?

### Fake It 'till You Become It

Psychologist [Amy Cuddy has a famous talk](https://www.ted.com/talks/amy_cuddy_your_body_language_shapes_who_you_are) about how you can “fake it till you become it” which fits well here. If they have a clear idea of how a knowledgeable, caring, truthful, courageous, collaboratory, open, accessibility-focussed, and resilient person would act in that same situation, they’ll be able to do the same thing and move themselves a bit closer to that goal of being virtuous. The reality is a bit more complex because the interpretation of what exactly constitutes knowledge or care or truth or any of the other proposed virtues will vary from person to person.

In this case, Maiken and Kenneth need to consider whether they want to be the kind of people who mine cryptocurrency on a visitor’s computer, and more broadly, whether they think that person has the virtues they aspire to. In their case the answer is ‘no’ and the earlier question, if everyone else is doing it why can’t we, answers itself.

So what would be a virtuous way of generating revenue from their website? One option Maiken and Kenneth choose to explore is selling memberships. This approach seems more [egalitarian](https://en.wikipedia.org/wiki/Egalitarianism): people who have the means can pay for exclusive access, and the revenue from memberships can be used to cover the cost of limited access for everyone else. The question is if selling memberships builds the virtues the couple aspire to. That’s where the third pier of the Bridge of Ethics, the *Virtuous Principles of Web Design*, comes in:

### Using Virtue Ethics in Web Design

Virtue ethics is the most introspective of the three moral philosophies we have looked at so far. It grants us the tools to look at ourselves as actors and recognize that with each act we perform, we not only change the outside world but also ourselves. In that way, virtue ethics compliments and resolves some of the issues raised by consequentialism and deontology.

Where consequentialism looks squarely at the external outcomes of an act and deontology looks at your reasons for performing that act, virtue ethics looks at what you become by performing that act and uses your desire to become a more skilled and knowledgeable, more successful, and overall better person as its driving force. We can draw on the best qualities of this theory to lay the third pier of our ethical bridge:

#### Four virtuous principles of web design:

1. Define and share the virtues you aspire to hold and how they describe the virtuous web designer you want to be.
2. Act as this virtuous web designer would act, i.e. act as the web designer you want to be.
3. With every act, consider what person it turns you into.
4. Align every act with the virtues you aspire to hold.

To put these principles into practice, use a virtual ethics checklist at the bottom of the article to guide decision-making processes.

Maiken and Kenneth want to become better people and better business people through their actions, and that extends to how they collect revenue from the site they are building. Using the virtuous principles of web design they evaluate the ethics of selling memberships as a revenue model and draw some conclusions:

- The relevant virtues they aspire to are knowledge, care, equity, truthfulness, courage, collaboration, openness, access, and resilience. Any revenue model should help them move closer to these virtues.
- Memberships and paid subscriptions are typically used to create paywalls where paying members get access to exclusive content. This goes against the virtues of care, openness, and access because it literally excludes non-members, keeps content closed off from the public, and restricts access to only those who can pay. To promote the virtues the couple aspires to, this means membership cannot impact access to content which takes away much of the incentive to be a member in the first place.

One possible approach Maiken and Kenneth consider is offering memberships that grant members influence rather than access; the ability to suggest new topics or even submit their own content to be published on the site. However, this can easily impact equity as the system grants those with means more influence than those without. So while it is possible to set up a membership model that passes the virtue ethics test, its return will be limited unless visitors choose to become members to support the content rather than get exclusive privileges &mdash; which is a hard bargain.

### Looking At An Even Bigger Picture

Taking a step back from the question of memberships and looking at the bigger picture painted by the virtuous principles, we start to see a shift from the focus on the actor and the act to those acted upon and how they are impacted; a crucial aspect of the transaction our conversation has not yet addressed.

Consequentialism looks at outcomes divorced from the actor’s intent, deontology looks at the actor’s intent divorced from the outcome, and virtue ethics look at what the actor becomes as a result of their actions. The next question we need to ask is what about the end-user and how they are impacted. This brings us to the fourth and final pier in our ethical bridge:

## 4. Capability Approach: User-Centered Design

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50581224-712d-4553-8d2b-7708f1c87f86/ethics-of-web-design-image9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50581224-712d-4553-8d2b-7708f1c87f86/ethics-of-web-design-image9.png" sizes="100vw" caption="" alt="Brought to you by Awesome Corp" >}}

Web design is in almost every case [service design](https://www.nngroup.com/articles/service-design-101/): We build solutions for other people that they can use to achieve their goals. That’s why user experience design is such a big part of web design and why human-centered design is at the core of user experience and interaction design.

So, for our ethical framework for web design to be complete, the fourth and final pier must support the end-user to anchor our ethics in the human experience. For this, we turn to a modern theory that crosses the boundary between philosophy and economics called [Capability Approach](https://en.m.wikipedia.org/wiki/Capability_approach). The [Stanford Encyclopedia of Philosophy has a comprehensive primer](https://plato.stanford.edu/entries/capability-approach/) that includes this short introduction:

<blockquote>“The capability approach is a theoretical framework that entails two core normative claims: first, the claim that the freedom to achieve well-being is of primary moral importance, and second, that freedom to achieve well-being is to be understood in terms of people's capabilities, that is, their real opportunities to do and be what they have reason to value.”</blockquote>

Capability approach is often considered an offshoot of virtue ethics, but I feel it is different enough to be considered its own moral philosophy. What matters is not just what you do or why or how you do it, but also what future you enable the person at the other end of the transaction to build for themselves!

### Capability Approach In Web design

Capability Approach gives us a tool to justify our decisions based on the long-term outcomes the end-user experiences as a result. It also provides a foundation for following established best-practices like accessibility and [Resilient Web Design](https://resilientwebdesign.com/): If our goal is to always grant and enable capabilities in the end-user, the minimum requirement becomes the end-user having access and ability to use what we design in whatever way they can. Rather than giving everyone a bicycle, we give everyone the capability of transport by allowing them to choose the best solution. [Capability approach can also be found implicitly or explicitly in legislation around the right to data portability](https://www.smashingmagazine.com/2017/07/privacy-by-design-framework/), most notably under Europe’s [General Data Protection Regulation (GDPR)](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation).

{{% pull-quote %}}Making ethics part of our design process helps us build the world we all want to live in.{{% /pull-quote %}}

More widely, the Capability Approach in web design allows us to take a step back and consider why we do what we do. Every design decision we make carves a path our end-users follow into the future. The Capability Approach makes us think carefully about where that path leads and what happens to the people who interact with our creations when they follow us into that future. So in addition to asking what we are going to build, how we are going to build it, and why we are building it, we have to ask _to what end_: If we build this, what world do we build for the visitor in the process?

### Evaluating Sponsorship Models, A Capability Approach Example

In their quest for an ethical revenue model for the content on their site, Maiken and Kenneth have turned their attention to the tried and true sponsorship model, already well established in print and digital media as well as events. The sponsorship model exchanges funding for presence in some form (usually a large banner, a mention in audio and video clips, or “sponsored content”). In simple terms, sponsorship differs from advertising in that a sponsor pays an agreed upon sum of money up front for exposure to the audience whereas advertising typically pays on a per-impression or per-click basis.

To evaluate the ethical implications of sponsorships as a revenue model, they turn to the capability approach and ask what capabilities are granted or enabled on the positive side or prevented or removed on the negative side by accepting sponsorships.

They consider three sponsorship models:

1. Philanthropic sponsorship, i.e. “See a list of our sponsors/supporters on this page”
2. Passive sponsorship, i.e. “this article brought to you by…”
3. Active sponsorship, i.e. “And now, a word from our sponsor” aka advertorial content

The first one is the obvious preference, but it relies on companies and individuals being willing to give them money without exposure (something that rarely happens). Passive sponsorship is the most common of the three models. Here a company gets visible (or auditory) presence as a funder of the content being presented. This model works, but is only attractive to sponsors if the site has a large following and can claim to be “influential.”

Active sponsorship leaves the sponsor in charge of some content on the site. This is the more attractive option from the sponsor’s perspective and likely also where the most revenue can be collected. However, handing control of content to a sponsor has serious implications.

#### What Capabilities To Test For?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1f6c7c7-7252-452b-8528-9612fb63409b/ethics-of-web-design-image12.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1f6c7c7-7252-452b-8528-9612fb63409b/ethics-of-web-design-image12.jpg" sizes="100vw" caption="Left: Martha Nussbaum (<a href='https://commons.wikimedia.org/wiki/File:Martha_Nussbaum_wikipedia_10-10.jpg'>Image source</a>) Right: Amartya Sen (<a href='https://commons.wikimedia.org/wiki/File:Amartya_Sen_,_c2000_(4379246038).jpg'>Image source</a>)" alt="Image of Martha Nussbaum (left) and Amartya Sen (right)" >}}

To analyze these three sponsorship models, we first have to define what capabilities to test for. Here capability approach suffers the same challenge faced by deontology and virtue ethics: who decides what capabilities should be in focus and how to test the success of any decision or act in terms of capabilities granted and enabled.

Amartya Sen argues there is no one true list of capabilities because such a list would be too difficult to define. [Martha Nussbaum has proposed a list of 10 Central Capabilities](https://en.m.wikipedia.org/wiki/Capability_approach#Nussbaum's_central_capabilities) that though not complete or unchangeable should form the baseline for judgments. The list includes:

- Life
- Senses
- Imagination and Thought
- Practical Reason
- Control over one’s Environment (Political and Material)

Nussbaum suggests that a decision or act must be judged on whether it helps the recipient secure a minimum level of these ten capabilities.

Sen argues that when evaluating well-being, “[the most important thing is to consider what people are actually able to be and do](https://www.iep.utm.edu/sen-cap/).” He illustrates this by asking us to think of a bicycle. While a bicycle is considered a transportation tool for all people, the capability of actually using a bicycle for transportation changes from person to person and context to context. Just because someone has a bicycle does not mean they have the capability of transportation. In other words, to provide the capability of transportation to a person we first have to take into consideration that person’s ability to use different transportation methods. One size rarely fits all.

### Using Capability Approach In Web Design

The fourth pier of the Bridge of Ethics, the *Capability Approach Principles of Web Design*, focuses our attention on the end-user and their experience. The immediate value of the capability approach is its focus on the long-term outcomes of the end-user. Web designers build solutions for people, and every decision a web designer makes has a long-term impact on the people who interact with it. Thinking carefully about what capabilities each of our design decisions grant and enable, and choosing only those decisions that produce and increase the well-being of the end-user is a key component in a well-formed ethical design process. We can draw on the best qualities of this theory to lay the fourth and final pier of our ethical bridge:

#### The Capability Approach Principles Of Web Design

1. Define the capabilities you want to build in users, communities, and the world.
2. Design solutions that grant each user capabilities to (re)claim their agency.
3. Measure success by the functionings achieved and the increased well-being of every individual end-user.
4. With every decision, carve a path to the future you wish to live in.

To put capability approach principles into practice, use a checklist at the bottom of the article to guide decision-making processes.

Using the capability approach principles of web design, Maiken and Kenneth evaluate the ethics of various forms of sponsorships as a revenue model and draw some conclusions:

- Passive sponsorships (“this content/site brought to you by”), can be argued to grant the visitor agency because they have enough information to know the relationship between the site owners and the brands that appear on the site. This assumes there is clear messaging stating “brought to you by” or “sponsored by” or similar.
- The active sponsorship model (content made by the sponsors) can enable the same capabilities, though to a lesser degree, as long as this content is clearly marked as advertorial and the visitor can clearly differentiate it from other non-sponsored content.
- Failure to properly disclose sponsorship relationships is actively harmful to the visitor as it removes their agency. This is why regulators are [cracking down on in-kind sponsorships and lack of disclosure from social media influencers](https://www.wsj.com/articles/social-media-influencers-get-noticed-by-regulators-1513342801).
- So-called “content marketing,” the practice of creating content to build influence and drive customers toward a specific product or brand, can be considered harmful to the visitor as the content is designed to influence and even actively coerce them.

So can Maiken and Kenneth ethically use sponsorships as their revenue model? According to the capability approach, the answer is yes as long as it’s done in a way that clearly discloses all relationships and meets the visitor’s reasonable expectation of being presented with honest and unbiased content from the site owners (in other words, active sponsorships and content marketing content are out).

## Using The Ethical Principles Of Web Design In Production

At the start of this article, I introduced the image of a bridge held up by four ethical theories and explained you can travel across it in both directions. Now that we’ve covered all four piers of the bridge we are ready to look at how to use this bridge in our everyday decision making processes.

When evaluating existing solutions, it’s easiest to start on the right side and move your way back, documenting real-life consequences first, then considering what rules and best practices were used, what virtues were promoted, and what capabilities were granted or enabled. This is how we typically make decisions in our industry today, though we rarely make it past consequentialism.

### Put The User First

What I propose is a literal pivot; Evaluating every new decision by crossing the bridge from the left to the right. As we saw with Maiken and Kenneth, the capability approach shifted their focus from how they can make money ethically to how their revenue models impact their audience, the visitors. This is important because all our decisions, whether they be about server infrastructure or content management systems or front-end frameworks or content strategy or revenue models or social media sharing and integration need to put the end-user first, every time.

Starting with the capability approach, we first establish what capabilities we want to grant and enable in our visitors and end-users and define the future world we build for them with our solutions. Next, virtue ethics help us consider what type of professionals we become by building those solutions. Deontology reminds us to consider what best practices we establish and what duties of care we must uphold. And finally, consequentialism helps us map out short- and long-term consequences and reminds us to think carefully about how we measure utility and whether we are excluding people with our decisions.

This method puts the end-user and their experience at the center of every decision and keeps them in focus as we evaluate what those decisions do to ourselves, our craft, and the world as a whole.

### Every Design Decision Is A Decision Made On Behalf Of The End-User

So, where does this leave our friends Maiken and Kenneth? How will they monetize the content on their site? Based on the evaluations in this example, their most ethical option is a combination of philanthropic and passive sponsorship and a membership model. Opt-in cryptojacking and direct sales advertising are also possibilities, but their return on investment will likely be too low to be meaningful.

Here comes the tricky part: There’s a high likelihood you disagree with some or all of these conclusions. And that’s OK! One of the most interesting parts of ethics is apart from extreme cases, how people evaluate different decisions and acts will differ, often greatly. There is rarely one true answer to any ethical question, but ask a large enough group to evaluate the question and you’ll see a strong trend in one direction.

The question you’re most likely asking yourself now is “Doesn’t that make the whole thing pointless?” The answer is “no”, and here’s why:

The purpose of the *Ethical Principles of Web Design* is not to create an authoritative list of good and bad decisions for all to follow any more than the principles of UX instruct designers on the one true way to design a specific interaction. These principles are tools for us to use to facilitate careful and considerate thinking about the decisions we make. More often than not, using these principles will bring up questions that would otherwise have never been discussed, and many of them will not result in full or final answers. What they will do is remind you and everyone you interact with that every design decision is a decision made on behalf of the end-user, and every decision changes their world and builds their future in some small way.

### Better Futures For Everyone

Even small and seemingly insignificant decisions can have enormous implications, and though ethics often stand in the way of immediate rapid innovation, growth, and quick revenue, they help ensure the longevity of our designs and help us carve paths to better futures for everyone.

Being mindful of what we do is essential. It’s what gives us the power to create. Making ethics part of that process helps us build the world we all want to live in. Using the *Ethical Principles of Web Design*, you will be better equipped to make design decisions you can stand by today and in the future; decisions that help you build the future you want to live in along side every person you impact with your designs.

## The Ethical Principles Of Web Design (Checklist)

This checklist is a practical tool to be used alongside other design techniques like [Design Sprints](https://www.gv.com/sprint/) and [Journey Maps](https://www.nngroup.com/articles/customer-journey-mapping/). Use it, expand on it, and make it your own:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Theory</th>
			<th>Capability Approach</th>
			<th>Virtue Ethics</th>
			<th>Deontology</th>
			<th>Consequentialism</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>Mnemonic device</th>
			<td>What world / future are you building for the end-user?</td>
			<td>What type of person do you become in the process?</td>
			<td>What norms and expectations are you establishing?</td>
			<td>What are the consequences of your actions?</td>
		</tr>
		<tr>
			<th>Principles</th>
			<td>1. Define the capabilities you want to build in users, communities, and the world.<br /><br />2. Design solutions that grant each user capabilities to (re)claim their agency.<br /><br />3. Measure success by the <a href="https://en.wikipedia.org/wiki/Capability_approach#Functionings">functionings achieved</a> and the increased well-being of every individual end-user.<br /><br />4. With every decision, carve a path to the future you wish to live in.</td>
			<td>1. Define and share the virtues you aspire to hold and how they describe the virtuous web designer you want to be.<br /><br />2. Act as this virtuous web designer would act - ie act as the web designer you want to be.<br /><br />3. With every act, consider what person it makes you become.<br /><br />4. Align every act with the virtues you aspire to hold.</td>
			<td>1. Follow existing rules, best practices, and guidelines.<br /><br />2. Use the Categorical Imperative as a starting point to creating new rules.<br /><br />3. When no rule exists, use the full ethical principles of web design to create new ones.<br /><br />4. Uphold the Duty of Care: to the client, to the user, to the information, and to the future.</td>
			<td>1. Prioritize the increased utility for all over maximizing utility for the majority (no person left behind).<br /><br />2. Provide sufficient remedies for those disadvantaged as a consequence of a decision (every user matters).<br /><br />3. Expect unexpected outcomes (the future is unknown).<br /><br />4. Favor iterative enhancements over permanent solutions (never settle/all paths are open).</td>
		</tr>
		<tr>
			<th>Checklist</th>
			<td>1. What capabilities does this decision grant and/or enable in the end-user?<br /><br />2. Do these capabilities increase the functionings of the end-user, what they are capable, want to be capable, or should be capable to be and/or do?<br /><br />3. Does this decision lead the end-user on a path to a future where their well-being is improved?<br /><br />4. Does this decision grant agency to the end-user and leave them in control over their freedom and future?</td>
			<td>1. What virtues are relevant in this decision? Knowledge, care, courage, openness, other virtues or a combination of virtues?<br /><br />2. How will this decision move you closer to holding these virtues? What path are you laying down for yourself by making this decision?<br /><br />3. Is this decision the same as what the virtuous web designer you want to become would make?<br /><br />4. When you look back on this decision in the future, will you see it as a good and virtuous decision?<br /><br />5. Are you able to communicate how this decision will bring you closer to your ideal of being a virtuous web designer to someone else?</td>
			<td>1. Are there existing rules to be followed? Do you understand them and are they applicable in this situation?<br /><br />2. If no rule exists, can you create a new universal rule everyone should follow in the same or similar situation?<br /><br />3. Are you comfortable with your decision being published on the front page of a major newspaper?<br /><br />4. Have you sought confirmation from peers or subject matter experts?<br /><br />5. Are you upholding the Duty of Care to your client?<br /><br />6. Are you upholding the Duty of Care to the end-user?<br /><br />7. Are you upholding the Duty of Care to the content?<br /><br />8. Are you upholding the Duty of Care to yourself?</td>
			<td>1. Who benefits from this decision, and why?<br /><br />2. Who is disadvantaged by this decision, and why?<br /><br />3. How is utility/disadvantage from this decision measured?<br /><br />4. Who decides what utility/disadvantage ratio is acceptable?<br /><br />5. How are disadvantages created by this decision addressed and reduced / remedied?<br /><br />6. How flexible is this decision? Is there sufficient room for course corrections?<br /><br />7. Who and what are the outliers we have not considered?<br /><br />8. Assuming this decision has unintended consequences, what are they and how do we deal with them?</td>
		</tr>
	</tbody>
</table>

## Where To Start?

When I talk to people about ethics and the bridge I’ve described in this article, I often get responses such as “I see why it matters, but I don’t think this will fit into my/our process.” This is a fair critique. Decision making based on an ethical framework is not something we are used to doing, in web design or anywhere else in our lives. For the most part, ethics is something subconscious and unspoken; we “just know” or have a “gut feeling” whether something is right or wrong.

Formalizing a method for testing the ethics of a decision is a skill like any other, and it requires practice to become natural. The good news is you can lean on your own built-in ethical barometer (that “gut feeling” about the rightness or wrongness of an act) and use the simplified version of the bridge to get started. To apply the *Ethical Principles of Web Design* in your practice today, start with the mnemonic devices for each theory:

1. What world are you building for the end-user? What capabilities are you granting or enabling?
2. What type of person do you become in the process?
3. What norms and expectations are you establishing? Are you upholding your duties of care?
4. What are the consequences of your decision, and do they improve the common good for those affected?

As you’ve learned, these principles are not about creating a dogmatic list of right and wrong, but rather a toolkit to help you explore questions around the ethics of your decisions.

To help you explore each of these questions in more detail, you can use the checklist provided above.

Once asking these questions becomes second nature, dive deeper into the individual theories that make up the piers of the bridge and establish a deeper understanding of what ethics and moral philosophy are, and why it plays a role in all aspects of our lives.

To get you started, I’ve assembled a list of resources below. Some of the links are from the article, some are added as further reading.

In the end, ethics is a practice we all need to work on every day. To borrow a quote from [Robert M. Pirsig](https://en.wikipedia.org/wiki/Robert_M._Pirsig):

<blockquote>“The place to improve the world is first in one's own heart and head and hands, and then work outward from there.”</blockquote>

## Resources

### Capability Approach

- [Capability Approach, Wikipedia](https://en.wikipedia.org/wiki/Capability_approach)
- [The Capability Approach, Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/entries/capability-approach/)
- [Sen’s Capability Approach, Internet Encyclopedia of Philosophy](https://www.iep.utm.edu/sen-cap/)

### Virtue Ethics

- [Virtue Ethics, Wikipedia](https://en.wikipedia.org/wiki/Virtue_ethics)
- [Virtue Ethics, Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/entries/ethics-virtue/)
- [Virtue Ethics, Internet Encyclopedia of Philosophy](https://www.iep.utm.edu/virtue/)
- [Technology and the Virtues](https://global.oup.com/academic/product/technology-and-the-virtues-9780190498511?cc=ca&lang=en&), Shannon Vallor, Oxford University Press, 2016

### Deontology (Duty Ethics)

- [Deontological Ethics, Wikipedia](https://en.wikipedia.org/wiki/Deontological_ethics)
- [Kantianism, Wikipedia](https://en.m.wikipedia.org/wiki/Kantianism)
- [Deontological Ethics, Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/entries/ethics-deontological/)
- [Categorical Imperative, Wikipedia](https://en.wikipedia.org/wiki/Categorical_imperative)
- [Kant’s Moral Philosophy, Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/entries/kant-moral/)

### Consequentialist Ethics

- [Consequentialism, Wikipedia](https://en.m.wikipedia.org/wiki/Consequentialism)
- [Utilitarianism, Wikipedia](https://en.m.wikipedia.org/wiki/Utilitarianism)
- [Consequentialism, Internet Encyclopedia of Philosophy](https://www.iep.utm.edu/conseque/)
- [Consequentialism, Stanford Encyclopedia of Philosophy](https://plato.stanford.edu/entries/consequentialism/)
- [Act and Rule Utilitarianism, Internet Encyclopedia of Philosophy](https://www.iep.utm.edu/util-a-r/)

### Related Philosophy

- [Egalitarianism, Wikipedia](https://en.wikipedia.org/wiki/Egalitarianism)
- [Care Ethics, Stanford Encyclopedia of Philosophy](https://www.iep.utm.edu/care-eth/)
- [Four Causes (Aristotle and Heidegger), Wikipedia](https://en.m.wikipedia.org/wiki/Four_causes)

### Other Related Materials

- [Resilient Web Design, Jeremy Keith](https://resilientwebdesign.com/)
- [Design for Real Life, Eric Meyer, and Sara Wachter-Boettcher, A Book Apart](https://abookapart.com/products/design-for-real-life)
- [The Real World of Technology, Ursula M. Franklin, The 1989 CBC Massey Lectures](https://www.cbc.ca/radio/ideas/the-1989-cbc-massey-lectures-the-real-world-of-technology-1.2946845)
- [The Ethics of Running a Data Breach Search Service, Troy Hunt](https://www.troyhunt.com/the-ethics-of-running-a-data-breach-search-service/)
- [Should Data Scientists Adhere to a Hippocratic Oath? Wired Magazine](https://www.wired.com/story/should-data-scientists-adhere-to-a-hippocratic-oath)
- [How To Protect Your Users With The Privacy By Design Framework, Heather Burns, Smashing Magazine](https://www.smashingmagazine.com/2017/07/privacy-by-design-framework/)
- [How GDPR Will Change The Way You Develop, Heather Burns, Smashing Magazinie](https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/)
- [Design's Lost Generation, Mike Monteiro](https://medium.com/@monteiro/designs-lost-generation-ac7289549017)
- [Center for Humane Technology](https://humanetech.com/)

{{< signature "md, ra, hj, il" >}}
