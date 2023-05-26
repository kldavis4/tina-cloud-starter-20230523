---
title: 'State Of CSS Survey: Influence The Future Of CSS'
slug: state-css-survey-2022
author: lea-verou
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b32b88-9b48-4c44-95f3-d51b26923bde/state-css-survey-2022.jpg
date: 2022-10-24T19:00:00.000Z
summary: >-
  The annual survey for anyone who writes CSS, [State of CSS](https://stateofcss.com/en-us/?source=smashing_magazine_css_survey), is nearing the end of its response period for 2022. The survey is available in many different languages and all questions are optional. [Join in the survey](https://survey.devographics.com/survey/state-of-css/2022?source=smashing_magazine_css_survey) &mdash; it will only take a few minutes.
description: >-
  The annual survey for anyone who writes CSS, [State of CSS](https://stateofcss.com/en-us/?source=smashing_magazine_css_survey), is nearing the end of its response period for 2022. The survey is available in many different languages and all questions are optional.
categories:
  - CSS
  - Events
---

This year, I joined the team and [helped design the survey together with the community](https://lea.verou.me/2022/07/help-design-the-state-of-css-survey-2022/) which led to a [number of improvements](https://lea.verou.me/2022/10/state-of-css-2022-now-open/). If you write CSS frequently, investing a few minutes to fill it in could come back to you hundredfold, since implementers make decisions on what to work on based on the developer pain points identified through the survey every year. In fact, Chrome is funding work on the survey for this very reason.

## Past Surveys

So, how did past surveys help web developers? Let’s look at the impact in Chrome, as described to us by [Nicole Sullivan](https://twitter.com/stubbornella), Product Manager for Chrome at Google:

<blockquote>“I showed the <a href="https://2019.stateofcss.com/opinions/#missing-features?source=smashing_magazine_css_survey">‘Missing features’ section</a> to my team before the pandemic and we got to work on it. Several things on that list are underway.”</blockquote>

Indeed, literally everything in that list is now being worked on or finished unless there was no (stable) specification for it:

- ✅ **Container queries**  
Size queries have [shipped in Chrome 106](https://caniuse.com/css-container-queries) , style queries behind a flag.
- ✅ **Parent selector/:has selector**  
[Shipped in Chrome 105](https://caniuse.com/css-has).
- ✅ **Nesting**  
Currently underway, delayed a bit due to discussions in the CSS Working Group about last minute changes to the syntax.
- 🟡 **Functions**  
No specification to implement yet, but is being worked on in the CSS WG.
- ✅ **Scoping**  
Experimental implementation in Chrome 105 behind a flag.
- 🟡 **Mixins**  
No specification to implement yet, but ideas are being explored in the CSS WG.
- ✅ **Subgrid**  
Implementation underway.

Let’s look at the [corresponding section in the 2020 results](https://2020.stateofcss.com/en-US/opinions/#currently_missing_from_css?source=smashing_magazine_css_survey?source=smashing_magazine_css_survey). A lot of overlap, but some additional items:

- ✅ **Form elements styling**  
Work is underway on a [stylable &lt;selectmenu> element](https://hidde.blog/custom-select-with-selectmenu/) to replace &lt;select>, and an [experimental implementation exists in Chrome](https://open-ui.org/prototypes/selectmenu) behind a flag.
- 🟡 **Conditional logic**  
No specification to implement, but several proposals are being explored in in the CSS WG.
- ✅ **Masonry layout**  
[Already worked on](https://www.smashingmagazine.com/native-css-masonry-layout-css-grid/), experimental implementation in Firefox Nightly.

The [2021 corresponding section](https://2021.stateofcss.com/en-US/opinions/#currently_missing_from_css_wins?source=smashing_magazine_css_survey) includes roughly the same items, with one new thing: **color functions**. And lo and behold, the color functions for which there is a stable specification are being implemented in Chrome as we speak, and Chrome has funded specification work on the rest. 

And it’s not just Chrome. The focus of [Interop 2022](https://web.dev/interop-2022/) was largely shaped by these results.

{{< rimg breakout="true" href="https://2020.stateofcss.com/en-US/opinions/#currently_missing_from_css?source=smashing_magazine_css_survey" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea87f3fc-d587-446b-a80b-524d55f245ec/currently-missing-from-css.png" width="800" height="630" sizes="100vw" caption="(Image credit: <a href=''>State of CSS 2020 Opinions</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea87f3fc-d587-446b-a80b-524d55f245ec/currently-missing-from-css.png'>Large preview</a>)" alt="Currently missing from CSS" >}}

## What’s Next?

We’re taking on the world of styles and selectors to try and identify upcoming trends, and figure out what featurs and tools to learn next. What’s more, the survey results will also help browser vendors prioritize their roadmaps and work towards better compatibility between browsers. 

What do you want to see more of in CSS? Better typography? New responsive layout features? New features to improve maintainability? Layout? Components? Something else? The sky is the limit! Make sure to [share your CSS dreams with us in the survey](https://stateofcss.com/en-us/?source=smashing_magazine_css_survey), and they may well start coming true.

{{< signature "vf, il" >}}
