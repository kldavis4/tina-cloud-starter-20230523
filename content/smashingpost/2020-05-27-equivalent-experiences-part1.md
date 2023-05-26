---
title: 'Equivalent Experiences: What Are They?'
slug: equivalent-experiences-part1
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4839dd34-25b9-4086-b69f-44e87faed54e/equivalent-experiences-part1.png
date: 2020-05-27T11:30:00.000Z
summary: >-
  An equivalent experience is one that has been deliberately conceived of and built to be able to be used by the widest possible range of people. To create an equivalent experience, you must understand all the different ways people interact with technology, as well as common barriers they experience.
description: >-
  An equivalent experience is one that has been deliberately conceived of and built to be able to be used by the widest possible range of people. To create an equivalent experience, you must understand all the different ways people interact with technology.
categories:
  - Accessibility
  - UX
---

If you spend enough time interacting with digital accessibility practitioners, you may encounter the phrase “equivalent experience.” This saying concisely sums up a lot of the philosophy behind accessibility work.

Our industry tends to place a lot of focus on *how*, often at the expense of *why*. For accessibility-related concerns, it is vital to learn about the history, and lived experiences of disabled people as a context for understanding the need for design and code created with access in mind.

This is the first of two articles on the topic of equivalency, and how it relates to digital accessibility. It will help us define what an equivalent experience is. Once we have a common understanding established, I’ll then discuss how to go about implementing equivalent experiences for common accessibility-related issues.

## The State Of Things

The truth of the matter is that even though we live in a multi-device world full of smartphones, augmented reality, voice assistants, and IoT smart sensors, our default is still predominately:

- Visual,
- large screen,
- fast connection,
- powerful computer and display,
- male,
- white,
- wealthy,
- young,
- Western,
- technologically-literate,
- and abled.

This is reflective of the biases that are inherent in how we design, develop and grow products.

The previous list may not be the most comfortable thing to read. If you haven’t closed the browser tab already, take a moment to consider your daily workflows, as well as who your coworkers are, and you’ll begin to understand what I’m getting at.

At its core, delivering an equivalent experience is ultimately about preserving *intent* &mdash; with the intent being the motivating force behind creating a website or web app and all the content and features it contains.

This translates to making the meaning behind every interaction, every component, every photo or illustration, every line of code being understandable by the widest range of people, regardless of their device or ability.

{{% feature-panel %}}

## Prior Art

I’m not the first person to discuss this topic (and hopefully not the last). Speaker, trainer, and consultant [Nicolas Steenhout](https://twitter.com/vavroom) is one such advocate. His great post, [*Accessibility is about people, not standards*](https://incl.ca/accessibility-people-not-standards/), is well worth reading.

If you’re the kind of person who is into podcasts, his [A11y Rules](https://a11yrules.com/) has a wonderful series called [Soundbites](https://a11yrules.com/series/a11y-rules-soundbite/). It features “short discussions with people with disabilities about the barriers they encounter on the web.” These insightful interviews also touch on what this article discusses.

## What Isn’t An Equivalent Experience?

Showing examples of what something is not can be a way to help define it. For equivalent experiences, an example would be a web app geared towards use by the general public not having a mobile breakpoint.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/653ca6a6-8e95-4f75-8968-8f177ff6158b/equivalent-experiences-wage-works.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/653ca6a6-8e95-4f75-8968-8f177ff6158b/equivalent-experiences-wage-works.png" sizes="100vw" caption="It’s not difficult to imagine a situation where I’d want to adjust my work benefits while on the go. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/653ca6a6-8e95-4f75-8968-8f177ff6158b/equivalent-experiences-wage-works.png'>Large preview</a>)" alt="The Dashboard view for WageWorks’ non-responsive website being viewed on an iPhone. Prompts to order commuting benefits are present, but are really tiny as it is assuming I’m viewing this on a laptop or desktop" >}}

With this example, everyone using a device with a small display is forced to pinch, pan, and zoom to get what they need. Here, the burden is placed on anyone whose only crime was using a smartphone.

Most likely, whoever conceived of, designed, and developed this didn’t stop to think about circumstances other than their own. In this sort of (unfortunately still all too common) scenario, I all but guarantee that the web app looks *great* on the laptops or desktops of the designers and developers who made it.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">A designer saying, “it has enough contrast for me and my ‘old’ eyes” is the same as when a dev says, “works on my machine.”<br><br>The thing is though, we don’t design or develop for ourselves.<br><br>So, are we really ok with saying, “you don’t matter” to folks who are not like us? <a href="https://twitter.com/hashtag/a11y?src=hash&amp;ref_src=twsrc%5Etfw">#a11y</a></p>&mdash; Heather (@_hmig) <a href="https://twitter.com/_hmig/status/1207662539837968384?ref_src=twsrc%5Etfw">December 19, 2019</a></blockquote>

People using a smartphone to access this website are victims of circumstance. The extra effort someone needs to do to get it to work indirectly communicates that they weren’t a priority, and therefore not valued. If you’ve used the web for any significant portion of time, I'm willing to bet this, or a similar experience has happened to you.

This example is also a hop, skip, and a jump away from another common, yet serious accessibility issue we often don’t consider: screen zooming:

### Screen Zooming

Screen zooming is when someone is prevented from being able to zoom their displays and make text larger—many native mobile apps are guilty of this. When you disallow this sort of behavior, you’re telling prospective users that unless they have vision similar to you, you aren’t interested in them being able to use your app.

For this scenario, a gentle reminder that we will all get older, and with aging comes a whole host of vision-related concerns. A question you should be asking yourself is if [your future self will be capable of using the things your present self is making](https://uxmag.com/articles/we-re-just-temporarily-abled). A follow-up question is if you’re also asking the people you’re managing this.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I just had my eyes dilated, so I can’t read any text that isn’t comically large. I don’t know how to use a screen reader. I’ll be fine in a few hours, but this has been a fascinating journey into how well third-party iOS apps respect text size accessibility settings!<br><br>(Thread)</p>&mdash; Em Lazer-Walker (@lazerwalker) <a href="https://twitter.com/lazerwalker/status/1222620721932722176?ref_src=twsrc%5Etfw">January 29, 2020</a></blockquote>

## Accessible Experiences Aren’t Necessarily Equivalent Ones

This might be a little difficult of a concept to grasp at first. Let’s use this [Rube Goldberg machine](https://en.m.wikipedia.org/wiki/Rube_Goldberg_machine) made by Joseph Herscher to pass the pepper to his dinner guest to compare:

<figure class="video-container break-out"><iframe loading="lazy" src="https://www.youtube.com/embed/XwaH-qT4Rm0" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

To pass the pepper, the machine, sends it through an elaborate system of weights, counterweights, ramps, rolling objects, catapults, guillotines, burners, timers, carousels, etc. &mdash; all constructed from commonly found kitchen items. While this setup will *technically* ensure the pepper is passed, it is an annoying, overwrought, time-intensive process.

Many digital experiences are a lot like a Rube Goldberg machine when it comes to accessibility. Since [accessibility issues are so prevalent](https://webaim.org/projects/million/), many forms of assistive technology provide a large suite of features to allow their user to work around common obstacles.

Unfortunately, discovering obstacles, and then figuring out and activating the appropriate combination of features to overcome them can take a disproportionate amount of time and effort.

To say it another way: A simple click on a button for an abled person may take far more time and effort for a disabled person, depending on how the button has been made.

{{% ad-panel-leaderboard %}}

### Chilling Effects

Frustratingly, the extra time and effort a disabled person has to put into operating a technically accessible experience may feed back into their disability condition(s). For example, the presence of a [motor control disability](https://webaim.org/articles/motor/) such as arthritis may make the overall experience even more taxing.

[Cognitive accessibility concerns](https://webaim.org/articles/cognitive/) are also another important thing to consider. What may seem easy to understand or intuitive to use for one person may not be for another. This is especially prevalent in situations where there is:

- Specialized domain knowledge,
- education on a new concept,
- and/or [a lack of common affordances](https://thomasbyttebier.be/blog/the-best-icon-is-a-text-label) for how the user interface operates.

Cognitive accessibility isn’t an abstract concern, either. Poor user interface design that ignores the circumstances of the end user and dumps too much [cognitive load](https://en.m.wikipedia.org/wiki/Cognitive_load) onto them can have [very real, very serious consequences.](https://features.propublica.org/navy-uss-mccain-crash/navy-installed-touch-screen-steering-ten-sailors-paid-with-their-lives/)

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f5b6a55-6913-4cec-ba1e-34383fe88308/equivalent-experiences-pro-publica-collision-course.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f5b6a55-6913-4cec-ba1e-34383fe88308/equivalent-experiences-pro-publica-collision-course.png" sizes="100vw" caption="The military is full of examples of poor interfaces being forced on people who don’t have a choice in the matter. It’s also one of the origins of Inclusive Design thinking. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f5b6a55-6913-4cec-ba1e-34383fe88308/equivalent-experiences-pro-publica-collision-course.png'>Large preview</a>)" alt="Screenshot of the ProPublica featured called, “Collision Course: The Navy Installed Touch-screen Steering Systems To Save Money. Ten Sailors Paid With Their Lives.” The intro paragraph reads, “When the USS John S. McCain crashed in the Pacific, the Navy blamed the destroyer’s crew for the loss of 10 sailors. The truth is the Navy’s flawed technology set the McCain up for disaster.” In the background are two large touchscreens with complicated-looking virtual dials, sliders, and other widgets. The touchscreens are placed in front of a ship’s window, with a foggy, stormy sea outside." >}}

### Compounding Effects

These factors are not mutually exclusive. Proponents of [Spoon Theory](https://en.m.wikipedia.org/wiki/Spoon_theory) know that inaccessible experiences conspire to sap a person’s mental and physical energy, leaving them exhausted and demotivated. Worse, these sorts of scenarios are often more than just a person perpetually operating at a diminished capacity.

Frustrating digital experiences can lead to a person abandoning them outright, [i](https://link.springer.com/article/10.3758/BF03192765)[nternalizing the system’s fault](https://alistapart.com/article/paint-the-picture-not-the-frame/) as their own personal failure. This abandonment may also translate to a person’s willingness and ability to operate other digital interfaces. In other words: the more we turn people away, the more they’ll stop trying to show up.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">“Nobody has complained before” is a silly excuse for not caring about accessibility. You’re right, they didn’t complain. They left.</p>&mdash; Vote blue, no matter who. (@karlgroves) <a href="https://twitter.com/karlgroves/status/1071482532762394624?ref_src=twsrc%5Etfw">December 8, 2018</a></blockquote>

## Don’t Take My Word For It

To make the abstract immediate, I [reached out on Twitter](https://twitter.com/ericwbailey/status/1221822162274832390) to ask people about their experiences using assistive technology to browse the web.

I also took [a purposely loose definition of assistive technology](https://twitter.com/ericwbailey/status/1221828942266556416). All-too-often we assume the term “accessible” only means “works in a screen reader.” The truth of the matter is that assistive technology is [so much more than that](https://mitpress.mit.edu/books/mismatch).

The way the web is built &mdash; its [foundational principles and behaviors](https://webfoundation.org/about/vision/history-of-the-web/) &mdash; make it extraordinarily adaptable. It’s us, the people who build on and for the web, who [break that](https://www.htmhell.dev/). By failing to consider these devices and methods of interacting with web content, we implicitly drift further away from equivalency.

### Consistency

For some, assistive technology can mean specialized browser extensions. These micro-apps are used to enhance, augment, and customize a browsing experience to better suit someone’s needs.

[Damien Senger](https://raccoon.studio/), digital designer, uses a browser extension called [Midnight Lizard](https://midnight-lizard.org/) to enforce a similar experience across multiple websites. This helps them “to focus on the content directly and to limit having too big differences between websites. It is also helping me to avoid too harsh color contrasts that are really uncomfortable.“

Damien also writes, “Often websites are really difficult to read for me because either of the lack of consistency in the layout, too narrow lines or just not enough balance between font size and line height. Related to that, color can create a lot of unhelpful distraction and I am struggling when too harsh contrast is nearby text.”

<blockquote><strong>How To Maintain Equivalency</strong><br /><ul>
    <li>A <a href="https://cariefisher.com/a11y-content/">larger font size and comfortable line height</a> goes a long way towards making content pleasant to read. </li>
    <li><a href="https://www.viget.com/articles/color-contrast/">A well-considered color palette with good contrast ratios</a> helps to keep the reader immersed in your content.</li>
    <li>Consistent application of color can also help communicate what elements can be interacted with, so long as it is <a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html">not just the color alone</a> that indicates interactivity.</li>
    <li>Ensure that text content is written using text (not presented as an image), allowing it to be read aloud, restyled, and reformatted.</li>
    <li>Use <a href="https://medium.com/@mandy.michael/building-websites-for-safari-reader-mode-and-other-reading-apps-1562913c86c9">semantic HTML, sectioning elements, and structured microdata</a> to allow your content to adapt to specialized reading modes and browser extensions.</li>
    <li>Understand that branding includes how something behaves, responds, and reacts in addition to how it looks.</li>
</ul>
</blockquote>

In addition, Damien also augments their browsing experience by using ad blocking technology “not only for ads but to block animations or content that are too distracting for my [ADHD](https://en.m.wikipedia.org/wiki/Attention_deficit_hyperactivity_disorder).”

It’s not too difficult to imagine why distracting and annoying your users is a bad idea. In the case of ads, the industry is unregulated, meaning that [rules to prohibit](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure.html) ADHD, migraine, and/or seizure-triggering animations aren’t honored. Through this lens, an ad blocker is a form of consumer self-defense.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I&#39;ll say it again: Telling users their access isn&#39;t as important as your bottom line is a BAD take. Ads are fine as long as they don&#39;t create a barrier by moving! <a href="https://twitter.com/hashtag/ADHD?src=hash&amp;ref_src=twsrc%5Etfw">#ADHD</a> <a href="https://twitter.com/hashtag/A11y?src=hash&amp;ref_src=twsrc%5Etfw">#A11y</a> <a href="https://twitter.com/hashtag/PSH?src=hash&amp;ref_src=twsrc%5Etfw">#PSH</a> <a href="https://twitter.com/hashtag/WCAG?src=hash&amp;ref_src=twsrc%5Etfw">#WCAG</a> <a href="https://t.co/i6mifI0JRE">https://t.co/i6mifI0JRE</a></p>&mdash; Shell Little 🧜‍♀️ (@ShellELittle) <a href="https://twitter.com/ShellELittle/status/1233148895498141699?ref_src=twsrc%5Etfw">February 27, 2020</a></blockquote>

[Kenny Hitt](https://twitter.com/hittsjunk) also chimes in about ads: “…regardless of the platform, the thing that annoys me most are websites with ads that essentially cause the site to constantly auto update. This prevents me as a screen reader user from reading the content of those websites.”

Again, a lack of regulation means the user must take measures into their own hands to keep the experience equivalent.

<blockquote><strong>How To Maintain Equivalency</strong><br />
    <ul>
        <li>Avoid <a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html">scripts that refresh the page automatically</a>.</li>
        <li><a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html">Avoid flashing and strobing animation</a>, especially animations that are known seizure triggers.</li>
        <li>Provide methods to pause any and all animation.</li>
        <li>Use the <a href="https://css-tricks.com/introduction-reduced-motion-media-query/"><code>prefers-reduced-motion</code> media query</a> to disable animation, if requested.</li>
        <li>Don’t use scripts that try to detect ad blocking.</li>
        <li>If a modal is used to inform someone about a newsletter signup, cookie policy, or that they’re using an ad blocker, ensure that <a href="https://www.scottohara.me/blog/2019/03/05/open-dialog.html">the modal traps focus and can be dismissed using a keyboard</a>.</li>
    </ul>
</blockquote>

### Opportunity

A lack of an equivalent experience translates directly to lost opportunity. Many individuals I spoke with mentioned that they’d abandon a digital experience that was inaccessible more often than not.

[Brian Moore](https://twitter.com/bmoore123) mentions, “there are web sites where I like their products a lot but won’t buy them because the site itself is such a struggle, and attempts to reach out have met with either silence or resistance to taking any action.”

Brian cites [the Fluance website](https://www.fluance.com/) as the most recent example. The bugs present in its shopping user flows prevents him from buying high-end consumer audio equipment.

Fluance’s entire web presence exists to sell products. While updating a website or web app to be accessible can be an effort-intensive process, it would definitely be in Fluance’s best interest to make sure its checkout user flow is as robust as it could be.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0e7838e-5dab-4c7e-985f-49eee7b3308c/equivalent-experiences-fluance.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0e7838e-5dab-4c7e-985f-49eee7b3308c/equivalent-experiences-fluance.png" sizes="100vw" caption="Those lost sales add up. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0e7838e-5dab-4c7e-985f-49eee7b3308c/equivalent-experiences-fluance.png'>Large preview</a>)" alt="Screenshot of the Fluance website, showing their Signature Series Surround Sound Home Theater 7.1 Channel Speaker System priced at $1,609.99 USD" >}}

Opportunity isn’t limited to just e-commerce, either. As [more and more services digitize](https://themarkup.org/2020/04/21/blind-users-struggle-with-state-coronavirus-websites), we paradoxically push more people out of being to live in the society that relies on these digitized services—people with [protected rights](https://www.w3.org/WAI/policies/). Again, this shift away from an equivalent experience is the culprit.

[Justin Yarbrough](https://twitter.com/FatElvis04) was “applying for an accessibility-related job with the Arizona Department of Economic Security over the summer, where they wanted me to take an assessment. The button to start the assessment was a clickable `div`. They wound up waving the assessment requirement for the position.”

[Jim Kiely](https://brainiacdevs.com/) tells me about his brother, who “has stopped paying his water bill online because the city water website [doesn’t] work well with a screen reader and high contrast.”

Personally, I have friends who have been prevented from submitting résumés to multiple sites because their job application portals were inaccessible.

<blockquote><strong>How To Maintain Equivalency</strong><br />
    <ul>
        <li>Use semantic markup (the <code>button</code> element for buttons, the anchor element for links, <code>input</code> and <code>label</code> elements for forms, etc.).</li>
        <li>Perform an initial <a href="https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/#the-fourth-myth">test of your user flows using assistive technology</a> to make sure they make sense.</li>
        <li>View your website or web app using <a href="https://a11yproject.com/posts/operating-system-and-browser-accessibility-display-modes/#high-contrast-mode">High Contrast Mode</a> and <a href="https://a11yproject.com/posts/operating-system-and-browser-accessibility-display-modes/#inverted-colors-mode">inverted colors</a> to make sure interactive content is being displayed properly.</li>
        <li>Use actual <a href="https://medium.com/seek-blog/four-things-we-learnt-from-facilitating-usability-testing-sessions-with-blind-users-2298dac58ae2">assistive technology users to test your user flows</a>.</li>
        <li>Demand third-party vendors to sign off on the accessibility of their product, including a <a href="https://en.m.wikipedia.org/wiki/Voluntary_Product_Accessibility_Template">Voluntary Product Accessibility Template (VPAT)</a>.</li>
    </ul>
</blockquote>

{{% ad-panel-leaderboard %}}

### Adaptability

[Soren Hamby](https://linktr.ee/uxicorn), product marketing manager and design advocate, writes of their experiences using screen magnification software and screen reading capabilities. Soren has “varying levels of vision so [they] tend to not always need the same level of accommodation.”

Of note, Soren mentions their struggles with grocery delivery apps, specifically “the carts often only read the quantities rather than the item name. It’s much easier to order with a sighted person.”

There are three things to consider here:

First is the surface-level acknowledgment that the app operates differently for different people, the main point this article is driving at.

Second is the fact that Soren uses [multiple forms of assistive technology](https://ericwbailey.design/writing/truths-about-digital-accessibility.html#assistive-technology-may-be-augmented-by-other-assistive-technology), with the mix a shifting combination depending on a combination of their task at hand and how well the digital interface meets their access needs.

<blockquote><strong>How To Maintain Equivalency</strong><br />
    <ul>
        <li>Make sure that <a href="https://adrianroselli.com/2020/01/my-priority-of-methods-for-labeling-a-control.html">the labels for your interactive controls</a> are relevant and concise.</li>
        <li>Incorporate disability scenarios and conditions into your <a href="https://alistapart.com/article/crafting-a-design-persona/">design personas</a>.</li>
        <li>Avoid using <a href="https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units#Absolute_length_units">absolute length units</a>. (No, <a href="https://www.24a11y.com/2019/pixels-vs-relative-units-in-css-why-its-still-a-big-deal/">seriously</a>.)</li>
        <li>Avoid setting maximum widths and heights.</li>
        <li>Avoid using fixed and sticky-scrolling components, especially larger-sized ones.</li>
        <li>Test your layouts by zooming and/or increasing your default type size to make sure that content does not get obscured.</li>
    </ul>
</blockquote>

This brings us to our third and most important point:

### Autonomy

Having to rely on the help of a sighted person to order groceries is not ideal. For many, the acquiring, preparation, and consuming of food can be highly personal acts. Being forced to incorporate outside assistance into this process is far different than willingly inviting someone in to share an experience. The same notion applies to every other digital product, as well.

Kenny also mentions grocery apps: “…my local Kroger grocery store has started an app redesign in June 2019 that is breaking accessibility with their app.” In discussing this regression, he goes on to elaborate, “Because I can’t financially change to another business, I won’t let it drop. Kroger is going to discover that I don’t stop with a problem. Persistence in solving problems is a requirement for any disabled person if you want to succeed in the world.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fd581ee-315c-458d-bfd3-4e5f429edf50/equivalent-experiences-kroger.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fd581ee-315c-458d-bfd3-4e5f429edf50/equivalent-experiences-kroger.png" sizes="100vw" caption="This app looks great, provided you can see it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fd581ee-315c-458d-bfd3-4e5f429edf50/equivalent-experiences-kroger.png'>Large preview</a>)" alt="Three screenshots from the redesigned Kroger app, including the home section, shop section, and weekly ads." >}}

### Equality

Kroger would be wise to listen to Kenny’s feedback. The grocery company [Winn-Dixie was recently successfully sued](https://www.forbes.com/sites/legalnewsline/2017/06/13/first-of-its-kind-trial-goes-plaintiffs-way-winn-dixie-must-update-website-for-the-blind/#3f669f4e1b38) for not being operable with a screen reader. The lawsuit argued that the grocer’s website was heavily integrated with their physical stores, and therefore violated [the Americans with Disabilities Act (ADA)](https://en.m.wikipedia.org/wiki/Americans_with_Disabilities_Act_of_1990).

Another recent case involves [the Domino’s Pizza franchise](https://slate.com/technology/2019/09/supreme-court-dominos-web-accessibility-visually-impaired.html). Taken all the way to the Supreme Court, the ruling clearly and unambiguously states that preventing someone from using a website or app, simply because they used screen reading software, is unconstitutional.

For both cases, the cost to implement fixes were far cheaper than going to court—something to think about the next time you’re deciding where to order pizza.

Despite some [ugly misconceptions](https://www.lflegal.com/2019/10/dominos-comments/) about the ruling, the evidence is clear: in the United States, there is now legal precedent for private companies to be sued for violating [civil rights](https://marcysutton.com/accessibility-is-a-civil-right) via an inaccessible digital experience. [Europe](https://ec.europa.eu/social/main.jsp?catId=1202) and [some parts of Asia](https://www.levelaccess.com/accessibility-regulations/japanese-industrial-standard/) have similar laws, as well.

<blockquote><strong>How To Maintain Equivalency</strong><br />
    <ul>
        <li>Understand that technical decisions can have legal consequences.</li>
        <li>Honor the law and don’t create circumstances that lead to discrimination.</li>
        <li>Familiarize yourself with the <a href="https://www.w3.org/WAI/standards-guidelines/wcag/">Web Content Accessibility Guidelines (WCAG)</a>.</li>
        <li>Add accessibility requirements to your <a href="https://www.productplan.com/glossary/acceptance-criteria/">acceptance criteria</a>.</li>
        <li>Add manual and automated <a href="https://a11yproject.com/checklist/">accessibility checks</a> to your design and development workflows.</li>
    </ul>
</blockquote>

### Reactivity

Another way to maintain an equivalent experience &mdash; one that is often not thought about &mdash; is to give reports about accessibility issues the same weight and concern as other software bugs.

Reported accessibility issues are [oftentimes downplayed and ignored](https://twitter.com/MarcoInEnglish/status/1262684564926971904/), or are sent to someone ignorant of the issue and/or powerless to fix it.

Kenny, who started using a computer with a screen reader in 1984 says, “When I run into accessibility issues nowadays, I’ll try reporting it, when I get the usual response from the feedback of the person not caring, I just give up and walk away. If [the response] comes from somebody in marketing who doesn’t understand accessibility, I just give up and go away. There’s no point in trying to teach these people about accessibility.”

Kenny’s view is shared by many others in the disability community. Remember what I said about compounding effects earlier.

Brian reports that,

<blockquote>“If I find significant issues with a site, I do report it. Depending on who I talk to it ranges from ‘here’s what doesn’t work’ to all kinds of technical detail about why if I can get to the right people.”</blockquote>

Getting it to the right people is key. Another part of equivalent experience is handling feedback in a timely and constructive way, much as how you would with any other issue with your product or service.

Responding to an accessibility issue is easy:

- Thank the person for taking the time and effort to report the issue.
- Acknowledge the issue and identify what person or team will be handling it.
- Ask clarifying questions as needed.
- Offer potential workarounds, with the understanding that they’re only temporary until the underlying issue is addressed.
- Offer to involve them in the process, including notifying them when the issue has been fixed.

Being open, honest, and transparent about your bug fixing process goes a long way to establishing trust in a population that has historically and routinely been overlooked.

Also know that assigning someone to mind an email address to conduct tasks on behalf of an assistive technology user is not an appropriate, effective, or sustainable solution. Remember the concerns surrounding autonomy discussed earlier.

<blockquote><strong>How To Maintain Equivalency</strong><br />
    <ul>
        <li><a href="https://www.w3.org/WAI/planning/statements/">Create an accessibility statement</a>, including known issues, a tentative timeline for their fixes, and easy to discover contact information.</li>
        <li>Ensure that anyone customer-facing (quality assurance, customer support, marketing, etc.) are trained on protocol for accessibility-related issue reporting.</li>
        <li>Quantify accessibility-related issues, both internal and reported.</li>
        <li>Be on the lookout for patterns and trends with discovered accessibility issues, as they represent learning opportunities.</li>
        <li>Understand that not all platforms to <a href="https://a11y.reviews/#online-surveys">collect feedback</a> are created equal.</li>
    </ul>
</blockquote>

## Motivation

We’ve covered actual people’s everyday frustrations, as well as civil rights and the current legal landscape. If these don’t motivate you, allow me to present another factor to consider: profit.

There are two provoking studies I’d like to call attention to, but they are by no means the only studies performed in this space.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d00186e9-04ca-4e70-baac-f9dd25d2c5a5/equivalent-experiences-purchasing-power-click-away.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d00186e9-04ca-4e70-baac-f9dd25d2c5a5/equivalent-experiences-purchasing-power-click-away.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d00186e9-04ca-4e70-baac-f9dd25d2c5a5/equivalent-experiences-purchasing-power-click-away.png'>Large preview</a>)" alt="The cover page of The Purchasing Power of Working-Age Adults With Disabilities report placed over a screenshot of the Click Away Pound Survey homepage" >}}

First is [the Click Away Pound Survey](https://clickawaypound.com/), a survey conducted in both 2016 and 2019 to “explore the online shopping experience of people with disabilities and examine the cost to business of ignoring disabled shoppers.”

The survey discovered that more than 4 million people abandoned a retail website because of the access barriers they found. These people represent 17.1 billion pounds (&#126;$21.1 billion USD) in lost potential revenue.

Second is the [The Purchasing Power of Working-Age Adults With Disabilities (PDF)](https://www.air.org/system/files/downloads/report/Hidden-Market-Spending-Power-of-People-with-Disabilities-April-2018.pdf), conducted in 2018 by the American Institutes for Research. This study discovered that there is an estimated $490 billion in disposable income amongst disabled working-age adults. That’s billion with a capital B.

There are two of the (many) takeaways from these studies I’d like to highlight:

First is that from a historical perspective, the web is still very much new. On top of that, [its ubiquity is even more recent](https://css-tricks.com/what-the-web-still-is/#article-header-id-7), meaning that use by the general population is a small sliver of the amount of time it’s been around.

Second is that the general population contains [many people who are disabled](https://ericwbailey.design/writing/truths-about-digital-accessibility.html#a-person-who-could-benefit-from-assistive-technology-may-not-be-using-it), and that their needs are not being met. These unmet needs represent **billions of dollars of potential revenue**.

This is a gigantic market that we, as an industry, are only now becoming aware of. Rather than approaching accessibility with a mindset of risk aversion, why not use this learning as a great way to view your current and future business opportunities?

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Complying with the ADA is by definition the legally required minimum for accessibility. It doesn&#39;t account for a good user experience, usability, and innovation. Unless you strive for the minimum all the time, compliance is not enough.<a href="https://t.co/qOYw6ji23u">https://t.co/qOYw6ji23u</a></p>&mdash; mikey is at home (@mikeyil) <a href="https://twitter.com/mikeyil/status/1235592641376591873?ref_src=twsrc%5Etfw">March 5, 2020</a></blockquote>

## Let’s Not Stop Here

Too often we think of accessibility as a problem to be solved, rather than a way of looking at the world. Equivalent experiences necessitate that we [question our assumptions and biases](https://twitter.com/rianrietveld/status/1227569523584307201) and think about experiences outside of our own. It can be an uncomfortable thing to think about at first, but it’s all in the service of making things usable for all.

As web professionals, it is our job, and our privilege to ensure that the experiences we deliver are equivalent. In the second part, we’ll investigate how to do just that.

### Further Reading

- “[WCAG Primer](https://tetralogical.com/articles/wcag-primer/),” Tetra Logical
- “[The Web Accessibility Basics](https://marcozehe.de/2015/12/14/the-web-accessibility-basics/),” Marco Zehe’s Accessibility Blog
- “[Web Accessibility Checklist: 15 Things To Improve Your Website Accessibility](https://websitesetup.org/web-accessibility-checklist/),” WebsiteSetup.org
- “[The Importance Of Manual Accessibility Testing: Call The Professionals](https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/#call-the-professionals),” Eric Bailey, Smashing Magazine
- “[Taking Accessibility Beyond Compliance](https://www.24a11y.com/2019/taking-accessibility-beyond-compliance/),” Dennis Deacon, 24 Accessibility
- “[Videos Of People With Disabilities Using Tech](https://axesslab.com/tech-youtubers/),” Hampus Sethfors, Axess Lab
- “[Web Accessibility Perspectives: Explore The Impact And Benefits For Everyone](https://www.w3.org/WAI/perspective-videos/),” Web Accessibility Initiative (WAI), W3C

*Thank you to Brian Moore, Damien Senger, Jim Kiely, Justin Yarbrough, Kenny Hitt, and Soren Hamby for sharing their insights and experiences.*

<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

{{< signature "ra, il" >}}
