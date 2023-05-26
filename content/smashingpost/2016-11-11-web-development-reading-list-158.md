---
title: >-
  Web Development Reading List #158: Form Usability, Vue.js, And Unfolding
  Critical CSS
slug: web-development-reading-list-158
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1554328-fcc3-4383-8d74-be2826459e92/wdrl-158-opt.png'
date: 2016-11-11T21:05:34.000Z
author: anselm-hannemann
description: >-
  These days, I’ve been pondering **what purpose we as developers have in our
  world**. I’m not able to provide you with an answer here, but instead want to
  encourage you to think about it, too. Do you have an opinion on this? Are we
  just pleasing other people’s demands? Or are we in charge of advising the
  people who demand solutions from us if we think they’re wrong? A challenging
  question, and the answer will be different for everyone here. If you want to
  let me know your thoughts, I’d be happy to hear them.

  Bear with me, this week’s list is a large one. Too many good resources popped
  up, explaining technical and design concepts, how to use new JavaScript
  methods to write smarter applications, and sharing lessons learned from CSS
  Grid Layouts and tips to take care of your happiness.
categories:
  - Web Development Reading List
---
These days, I’ve been pondering <strong>what purpose we as developers have in our world</strong>. I’m not able to provide you with an answer here, but instead want to encourage you to think about it, too. Do you have an opinion on this? Are we just pleasing other people’s demands? Or are we in charge of advising the people who demand solutions from us if we think they’re wrong? A challenging question, and the answer will be different for everyone here. If you want to let me know your thoughts, I’d be happy to hear them.

Bear with me, this week’s list is a large one. Too many good resources popped up, explaining technical and design concepts, how to use new JavaScript methods to write smarter applications, how to use CSS Grid Layouts, and how to take care of your happiness.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [An Extensive Guide To Web Form Usability](https://www.smashingmagazine.com/2011/11/extensive-guide-web-form-usability/)
*   [Web Form Design: Showcases And Solutions](https://www.smashingmagazine.com/web-form-design-showcases-and-solutions/)
*   [CSS Grid, Flexbox, Box Alignment: New System For Web Layout](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-and-box-alignment-our-new-system-for-web-layout/)
*   [How To Use Analytics To Build A Smarter Mobile Website](https://www.smashingmagazine.com/2014/03/how-to-use-analytics-to-build-a-smarter-mobile-website/)

## News

*   The [Safari Technology Preview 17](https://webkit.org/blog/7071/release-notes-for-safari-technology-preview-17/) adds support for Custom Elements v1, `rel=noopener`, and stylesheet loading via a link element inside Shadow DOM subtrees. Furthermore, preloading behavior was changed — it now matches iOS where resources like images get less priority when loading.
*   Already available in Nightly Builds, the feature to [emulate throttled network connections](https://blog.nightly.mozilla.org/2016/11/07/simulate-slow-connections-with-the-network-throttling-tool/) in Firefox’s Developer Tools will soon be added to the stable release, too.</p>

## General

*   Matthias Beitl has written a well-thought-out essay on [how we got into the “JavaScript wars”](https://cssence.com/blog/2016-11-the-javascript-wars), the paradigm shift, and an overtime improvement.</p>

## Concept & Design

*   Erika Hall explains in her recent Beyond Tellerand talk why we are trying so hard to measure things and collect data and [why this doesn’t mean we get better insights or make better decisions](https://vimeo.com/190883361).
*   Something that’s easily forgotten when thinking about form usability is how placing labels can matter when a user zooms into a page. For example, we need to consider that [placing labels above items means users who zoom in won’t lose context](https://mobile.twitter.com/elizallen_/status/794993023688077314).
*   How do you design a simple, usable registration form for a tax reform? @jelumalai [explains the process from a designer’s perspective](https://medium.com/@ux_je/simplifying-the-gst-registration-process-a-designers-perspective-e30e38fbbd26), diving deep into the challenge of asking for a lot of information while maintaining a clear workflow for the user.

{{% feature-panel %}}

<figure><a href="https://medium.com/@ux_je/simplifying-the-gst-registration-process-a-designers-perspective-e30e38fbbd26"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a965c562-5e4c-48c1-b558-08c14632f24b/form-ux-opt.png" alt="Simplifying a tax form" width="650" height="463" /></a><figcaption>How can you master the balancing act between asking for a lot of information and keeping a form as simple and usable for the user? <a href="https://medium.com/@ux_je/simplifying-the-gst-registration-process-a-designers-perspective-e30e38fbbd26">@jelumalai shares his lessons learned</a>. (Image credit: <a href="https://medium.com/@ux_je/simplifying-the-gst-registration-process-a-designers-perspective-e30e38fbbd26">@jelumalai</a>)</figcaption></figure>

## Tools & Workflows

*   [FormLinter](https://formlinter.com/) checks your form for usability issues. If you want to know more about what it does and how it works, [Ben Orenstein’s announcement post](https://robots.thoughtbot.com/announcing-formlinter) will give you some insights.</p>

## Accessibility

*   Stefan Judis explains [when to use and when not to use `aria-selected`](https://www.stefanjudis.de/aria-selected-and-when-to-use-it.html). Applying it to the current active navigation item, for example, isn’t correct, but applying it to the current active tab in a `tablist`, on the other hand, would be.</p>

## JavaScript

*   Mike Street shows how to [build a web app with Vue.js 2 using Vue-router](https://www.liquidlight.co.uk/blog/article/building-a-vue-v2-js-app-using-vue-router/). A good primer if you’re new to Vue.js.
*   [JavaScript’s `requestIdleCallback` method](https://hacks.mozilla.org/2016/11/cooperative-scheduling-with-requestidlecallback/) will soon come to Firefox 52\. If you don’t want to wait, good news: It can already be tested in Nightly Builds and is also supported in Chrome where it adds great value to scheduling tasks in cooperation with the browser environment.
*   Patricia Garcia shares her story of [how she managed to help fight Ebola in Africa with JavaScript](https://medium.com/net-magazine/fighting-ebola-with-javascript-26b48da8f84a). A great example of how to scale offline application design and why well-thought-out concepts matter to build a properly working solution.</p>

## CSS/Sass

*   Oliver Williams shares [what he learned about CSS Grid Layout](https://css-tricks.com/things-ive-learned-css-grid-layout/). Once you realize that it’s designed to be used alongside Flexbox and not as a replacement, you’ll slowly grasp how powerful the new technology really is.
*   JP de Vries shares the challenges of [unfolding critical CSS](https://medium.com/markuptips/unfolding-critical-css-91619401b4e) and why most websites are better off without it.

<figure><a href="https://css-tricks.com/things-ive-learned-css-grid-layout/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c62fe8cb-44a5-469b-8076-eaec08af7f1e/css-grid-layout-opt.png" alt="CSS Grid Layout" width="650" height="427" /></a><figcaption>To help you make sense of it all, Oliver Williams shares his <a href="https://css-tricks.com/things-ive-learned-css-grid-layout/">lessons learned about CSS Grid Layout</a>. (Image credit: <a href="https://css-tricks.com/things-ive-learned-css-grid-layout/">Iliver Williams</a>)</figcaption></figure>

## Work & Life

*   Mike Monteiro gave an impactful talk at this year’s Beyond Tellerrand conference in Berlin. “[Let Us Now Praise Ordinary People](https://vimeo.com/190834270)” opens our eyes to how we can change the world and why we need to get over-hyped startups that only claim to change something to actually do meaningful work. If I can make you watch one thing this week, take 45 minutes, sit back and listen to Mike Monteiro.
*   [selfcare.tech](https://selfcare.tech/) wants to help developers take better care of their health. It shows some great methods for solving common problems every one of us will face at some point.</p>

## Going Beyond…

*   [These solar panels are certainly a cool invention](https://futurism.com/these-solar-panels-can-pull-drinking-water-straight-from-the-air/): They can pull drinking water straight from the air, up to 5 liters per day per panel. A very nice way to source water when you don’t have traditional water resources.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}

