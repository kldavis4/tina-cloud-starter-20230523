---
title: 'Why Are We Talking About CSS4?'
slug: css4-pros-cons-discussion
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/588996d8-bbd2-440c-9389-43f9c45be54f/css4-pros-cons-discussion.png
date: 2020-03-04T11:30:00.000Z
summary: >-
  Around the web and within the CSS Working Group, there has been some discussion about whether we should specify a version of CSS &mdash; perhaps naming it CSS4. In this article, Rachel Andrew rounds up some of the pros and cons of doing so, and asks for your feedback on the suggestion.
description: >-
  Around the web and within the CSS Working Group, there has been some discussion about whether we should specify a version of CSS &mdash; perhaps naming it CSS4. In this article, Rachel Andrew rounds up some of the pros and cons of doing so, and asks for your feedback on the suggestion.
categories:
  - CSS
  - Browsers
---

There has been some discussion recently about whether there should be a CSS4, as in a defined "next version" of CSS. In this article, I take a look at the discussions around this, the pros and cons of creating a feature release for CSS, and the potential problems in deciding what goes into it.

I’m using the term **CSS4** as that is how the discussion was started, and not attempting to discuss what the naming should actually be, should this approach be taken forward. Bikeshedding naming is an excellent distraction from the discussion of whether we should do this at all, so I will use CSS4 as a placeholder for the version of CSS we are proposing to define, and CSS5 for the next one along the line.

## The Issue

A discussion around whether we should define a CSS4 has been raised in the community, and Jen Simmons then raised [a CSS Working Group issue](https://github.com/w3c/csswg-drafts/issues/4770) which neatly rounds up some of that existing debate. Outside of the actual issue that we are discussing, it is fantastic to see so many people who are not part of the CSS WG replying on this thread, and I hope that having commented once, people will be happy to come and comment on some of our other issues.

In order to understand why there is no CSS4, we need to look at a little bit of web platform history. The initial versions of CSS were as a single, monolithic specification. These specifications contained every possible CSS property and value. This worked well as there wasn’t a lot of CSS to detail. CSS1 mostly covered features for formatting text documents, additional features and clarifications were added to CSS2 and CSS2.1 however CSS was still a relatively small specification.

{{% feature-panel %}}

### CSS3

At the point the CSS Working Group began work on CSS3, it was decided to split the big spec into modules. These modules would each cover part of CSS. Not all of CSS was immediately placed into a new module. Many things remained defined in CSS2.1 as there were no changes or additions to them. For this reason, you will still find links to the CSS2 specification in modern modules, if the thing that is being referenced is still defined in CSS2. However, any new CSS is created in separate modules. This modularization continues today as new CSS is being created. For example, several of the features that make up the Box Alignment specification initially started life in the Flexbox spec. Once it became apparent that they could apply to other layout methods such as Grid Layout, they were moved into a new module to be defined for that other method too.

We stopped referring to new specifications as CSS3 Specifications, partly because it didn’t make a lot of sense. The way that modules are versioned is that the modules which were a progression of CSS2, for example Selectors, became a Level 3 module. Brand new CSS, for example CSS Grid Layout, did not exist at all in CSS2 and so start life as a Level 1 module. Some of those initial modules are now at Level 4 or even Level 5. Therefore, calling all new CSS _CSS3_ doesn’t map to the level numbers anymore, and is potentially rather confusing.

### Specification Maturity Levels

In addition to specification levels, each individual level goes through a staged process from the initial draft to becoming a W3C Recommendation, the steps in the process are referred to as [Maturity Levels](https://www.w3.org/2005/10/Process-20051014/tr#maturity-levels). A W3C Recommendation is what you might think of as a "web standard", however many of the things we use daily in our work are defined in specifications that are not at that maturity level yet. You can see the list of specifications and their status on the CSS WG [Current Work](https://www.w3.org/Style/CSS/current-work) page.

### Explaining The Missing CSS4

Many of us involved with the process saw the confusion about CSS3 or the apparent lack of progress to CSS4 and began to write articles, post videos, and try to help people understand a bit about how the process actually worked. That said, while it was important to share this information so that people teaching CSS would explain it correctly, I am not sure how much this information matters to the average web developer. What level a specification is at, or the internal W3C process of specification maturity, is far less important to a web developer than the issue of what CSS can actually be used in browsers.

- “[There Is No Such Thing As CSS4](https://www.xanthir.com/b4Ko0),” Tab Atkins-Bittner
- “[Why There Is No CSS4: Explaining CSS Levels](https://rachelandrew.co.uk/archives/2016/09/13/why-there-is-no-css4-explaining-css-levels/),” Rachel Andrew
- “[Where Is CSS4? When Is It Coming Out?](https://www.youtube.com/watch?v=Jtmkk6odggs),” Layout Land (video)

## What Are The Benefits Of Versioning CSS?

Looking through the responses to the issue, and the discussion around the web, there are certainly some potential benefits of having a clear version number for CSS.

As a writer of books and a producer of educational materials, I would probably benefit from CSS version numbers. It’s an excuse to publish an updated book that covers the latest and greatest version of CSS. On the other side of that, it is a way for the purchasers of books and courses to be sure that what they are buying is reasonably up to date - although the publishing date is arguably a better indication of that than anything else.

One thing we did lose by moving away from a version number of all of CSS, was the ability to do something like the [Acid Test](https://www.acidtests.org/). The Acid 1 Test tested for support of CSS1, Acid 2 for support of CSS2.1. These tests were reasonably well known and seen as a good benchmark for browser support of web standards. A version 3 test was developed, however, it tested for a range of features and was less tightly tied to the Level 3 CSS Modules than previous tests had been to CSS1 and 2.1. A definite line drawn around a set of features would allow for user agents to declare their level of support for those features.

[Some commenters on the issue](https://github.com/w3c/csswg-drafts/issues/4770#issuecomment-591847009) have mentioned that a version would allow them to push for dropping of older browser versions because they "don’t support CSS4".

<blockquote>“[...] perhaps CSS4 could help to push their mindset towards a more secure and better web. During pitch meeting, it’s hard to tell them we can’t support IE10 because we want CSS Variables and Grid Layout. Stakeholders do not know and do not care. They just want to support as many browsers as they could (very typical FOMO mindset) and they have the dollars to throw.<br /><br />However, if we could tell them we can’t support IE10 because it doesn’t have the latest CSS4 technology and throw them the "Are you sure you want your newly created website to be behind your competitors because of that?" question, that might ponder them (of course, on top of the fact that IE10 is completely obsolete and vulnerable).”</blockquote>

There is an argument that defining a version gives developers a clear set of things to learn. In opening the issue on the CSS WG Jen Simmons said,

<blockquote>“I see a lot of resistance to learning the CSS that came after CSS3. People are tired and overwhelmed. They feel like they’ll never learn it all, never catch up, so why try, or why try now? If the CSSWG can draw a line around the never-ending pile of new, and say 'Here, this. This part is ready. This part is done. This part is what you should take the time to learn. You can do this. It’s not infinite.' I believe that will help tremendously.”</blockquote>

{{% ad-panel-leaderboard %}}

## What Are The Problems Of Versioning CSS?

The first issue is that any collection of "ready for the primetime" CSS, is not as straightforward as selecting a set of specifications. Many specifications are partially implemented, with great support for some properties and none for others. There are features which many web developers would see as mature, sat in specifications still at Working Draft status alongside features which are still being debated and clarified in the Working Group.

If we take [Multiple-column Layout](https://www.smashingmagazine.com/2019/01/css-multiple-column-layout-multicol/) as an example. The majority of properties have had widespread browser implementation for many years. However, the [`column-span`](https://developer.mozilla.org/en-US/docs/Web/CSS/column-span) property has only recently been implemented in Firefox, and there are a number of features that have recently been clarified, such as [`column-fill`](https://developer.mozilla.org/en-US/docs/Web/CSS/column-fill).

We could decide to ignore specifications altogether and look at properties. That isn’t straightforward either due to the fact that we have partial implementations across layout methods. The [Box Alignment](https://drafts.csswg.org/css-align/) Properties are an excellent example. These are defined for all layout methods, where the property makes sense in that layout method. However support for Box Alignment is currently only seen in Grid and Flexbox. Therefore is [`justify-self`](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-self), which is defined for [block-level boxes, absolutely-positioned boxes, and grid items](https://drafts.csswg.org/css-align/#justify-self-property) stable? Yes in a Grid context, no in a Block Layout context.

[Box Sizing](https://drafts.csswg.org/css-sizing-3/) is another area, we have support for the [intrinsic sizing value](https://drafts.csswg.org/css-sizing-3/#sizing-values) `fit-content()` in CSS Grid Layout for track sizing, yet not as a value for `width`. Then, none of the intrinsic sizing keywords are implemented for `flex-basis` by [browsers other than Firefox](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis).

Finally, if we return to multicol, many of the problems people have with multicol are nothing to do with the properties themselves, but are to do with [poor support of fragmentation across browsers](https://www.smashingmagazine.com/2019/02/css-fragmentation/). This makes multicol seem to behave badly despite there being excellent support of the various properties. Disentangling all of these dependencies to come up with a set of features is going to be quite a difficult job.

### CSS Is Not Just For Web Browsers

As I and [one other commenter](https://github.com/w3c/csswg-drafts/issues/4770#issuecomment-591512088) have mentioned, **CSS is not just for web browsers**. There are a whole raft of user agents that take CSS and HTML and [output printed documents](/2015/01/designing-for-print-with-css/) by way of creating a print-ready PDF. They typically have excellent support for the Paged Media specification, fragmentation and so on. However, they often lag behind browsers in terms of implementing newer CSS, for example Grid Layout. How do they fit into CSS4?

### People Expect A Feature Release To Include Currently Non-Existent Features

Something interesting that has happened in the discussion on the issue, is that a number of people have commented saying that their expectations of a CSS4 are that it would contain certain features that _are not yet_ part of CSS at all. Joshua Lindquist, in [his excellent roundup of the comments](https://github.com/w3c/csswg-drafts/issues/4770#issuecomment-593188481) notes that,

<blockquote>“When discussing authors that do not keep up with the latest developments, I think this approach will be simple to understand. Everything will feel like it's brand new to them, even though some of these features, like Grid and Flexbox, have been in browsers for years.<br /><br />But anyone who does keep up will likely be confused about why there is a ‘new’ specification full of things that are actually old.”</blockquote>

### Who Would Decide What Makes The Cut?

Given the fact that the features that would make up CSS4 are not completely straightforward, someone is going to have to make the decision as to what is included.

The CSS Working Group has criteria for stability via the Maturity Levels already discussed. Once a spec has two implementations of each feature it can progress from Candidate Recommendation Status to become a Recommendation. However, as detailed above, it can take some time for that to happen, and while we are waiting for some features in a spec to have implementations, other may have widespread and stable browser support. If we were to say that CSS4 was only those specifications that were at Recommendation Status it would include:

- CSS Color Level 3
- CSS Namespaces
- Selectors Level 3
- CSS Level 2 Revision 1
- Media Queries
- CSS Style Attributes
- CSS Fonts Level 3
- CSS Writing Modes Level 3
- CSS Basic User Interface Level 3
- CSS Containment Level 1

So, no Grid, Flexbox, Box Alignment, and many more specifications that most of us are using.

If we are going to define a version of CSS, that is separate to the existing specification levels and maturity that we already have as part of the W3C process, then there needs to be a group with the time and resources to work on this. That group not only needs to define CSS4, but needs to do that as part of developing a framework to make these decisions this time, and for the next n versions of CSS. Otherwise, we will be having this discussion again in another two years, about the fact that no-one has shipped CSS5. I don’t believe the CSS Working Group is the right venue for that, even if only that there is other work that the WG needs to be doing to actually develop and define new CSS. There are already more jobs to be done than we have time to do. In addition, having another consideration when working on specifications will make decisions around each spec harder. Currently, we have situations where parts of a spec are marked as at-risk if their inclusion might prevent the spec from progressing to a Recommendation. It was for this reason that subgrid was bumped to Level 2 of Grid. If we have this additional level of abstraction, which doesn’t really fit into the process, will this just be another thing to consider and thus delay work on specifications?

{{% ad-panel-leaderboard %}}

## What Problem Are We Trying To Solve?

In many of the responses to this issue, web developers brought up browser support as being key to what should be included in a CSS4, and I think that the issue we face is less one of CSS versioning and more of web developers being clear as to which collection of features should generally be considered usable in their projects.

<blockquote>“One of the advantages of a CSS4 approach is that it signals two things. First, that there’s a significant bundle of new CSS features that have been developed after CSS3 and which are ready for use and second, that they are ready for use. Not experimental or implemented by Chrome but no one else, but ready for broad adoption.”<br /><br />&mdash; <a href="https://github.com/w3c/csswg-drafts/issues/4770#issuecomment-590441840">Rick Gregory</a></blockquote>

The fact that browser support comes up so frequently in this discussion makes me wonder if a better place to be defining this would be somewhere like MDN. MDN is already contributed to by all browser vendors, it already has support data for these features in a way that allows us to see partial implementations of things like Box Alignment. MDN is the documentation for the web platform, so we could sidestep the issue of print implementations, or any other implementations of CSS, scoping the feature set to the web alone.

I remain unconvinced that a CSS4, or whatever we choose to call a version of CSS, will actually make any difference to the perception of CSS outside of a relatively small community. Nor do I think it will help to solve the problems that web developers have in terms of convincing their bosses and clients to upgrade browsers. If Microsoft, who provides the software, is telling companies to upgrade and companies are not upgrading, I fail to see what the carrot of supporting CSS4 will do. And, I’ve been doing this a long time and know that back when we _did_ have versions of CSS, people still didn’t upgrade their browsers. However, I think it will make it easier to talk about a particular chunk of functionality in a less abstract way, but I think that it needs to happen outside of the CSS Working Group and the specification process, and be based on what is usable as opposed to what is well specified.

<blockquote>“However, I must agree with several others that major marketing versions only have meaning in a compatibility situation. If we announce that CSS5 is finally here, it must mean all major browsers have full or near-full support.<br /><br />Without this compatibility condition met, I think some developers will be cynical, and return to feature or module based thinking, the current status quo.”<br /><br />&mdash; <a href="https://github.com/fchristant">Ferdy Christant</a></blockquote>

## What Do You Think?

I wanted to bring the discussion to Smashing Magazine as I think that many of our readers won’t have noticed this discussion. I’d be interested in what you think. Are there ways in which declaring a version of CSS would help you, that I haven’t mentioned here? Would checking to see what was in this version be something you would do, or would you be more inclined to check Can I Use, or MDN to find out what is supported? Do you think the average web developer cares about this stuff? Let us know in the comments, [post to the original issue](https://github.com/w3c/csswg-drafts/issues/4770), or join the new [Community Group](https://www.w3.org/community/css4/) set up to discuss this.

{{< signature "il" >}}
