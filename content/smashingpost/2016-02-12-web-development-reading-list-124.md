---
title: 'Web Dev. Reading List #124'
slug: web-development-reading-list-124
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9d41c9-ce63-47b7-a828-ccfee704c190/vector-networks-opt.png
date: 2016-02-12T21:57:24.000Z
author: anselm-hannemann
description: >-
  I often think about our responsibility as web developers. I compare our job to
  a health worker, to a craftsman, and I realize that we have a pretty easy job
  in most cases. Usually, nobody’s life will be affected if a website is not
  available for a couple of minutes or hours.

  But there are some cases where this could happen. People start coding app
  interfaces for health application with web technologies, people start
  connecting health services to the web, and people also rely on websites for
  their own safety. And that’s why I think **we should feel responsible for our
  users**. And by making choices that are ethical and user-centered, we create a
  better web for everyone.
categories:
  - Web Development Reading List
---
I often think about our responsibility as web developers. I compare our job to a health worker, to a craftsman, and I realize that we have a pretty easy job in most cases. Usually, nobody’s life will be affected if a website is not available for a couple of minutes or hours.

But there are some cases where this could happen. People start coding app interfaces for health application with web technologies, people start connecting health services to the web, and people also rely on websites for their own safety. And that’s why I think <strong>we should feel responsible for our users</strong>. And by <a href="https://ethicalweb.org/">making choices that are ethical and user-centered, we create a better web for everyone</a>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Conversational Interfaces: Where Are We Today?</span>](https://www.smashingmagazine.com/2016/07/conversational-interfaces-where-are-we-today-where-are-we-heading/)
*   [How Do You Design Interaction?](https://www.smashingmagazine.com/2014/07/how-do-you-design-interaction/)
*   [Useful Ideas And Guidelines For Good Web Form Design](https://www.smashingmagazine.com/2011/06/useful-ideas-and-guidelines-for-good-web-form-design/)
*   [Forms On Mobile Devices: Modern Solutions](https://www.smashingmagazine.com/2010/03/forms-on-mobile-devices-modern-solutions/)

## News

*   Announced in December, [Adobe Animate CC is finally here](https://blogs.adobe.com/animate/animate-cc-is-here/). It replaces Edge Animate and Flash Professional and is now the new tool for web animation.
*   [Firefox changed the behavior of the Cache API](https://www.fxsitecompat.com/en-CA/docs/2016/cache-api-now-rejects-unsuccessful-responses/), following a specification change to fix confusion about the API storing `4xx` and `5xx` responses from `fetch()`. This is no longer the case, and, starting from Firefox 46, only responses with a `2xx` code are cached now.
*   It seems that [the behavior of the JavaScript function `window.innerWidth/Height` has changed](https://www.quirksmode.org/blog/archives/2016/02/chrome_change_b.html) in Chrome 48\. This is especially interesting because Chrome now behaves differently than all other browsers: it’s now reporting back the dimensions of the layout viewport instead of the dimensions of the visual viewport, making it a copy of `document.documentElement.clientWidth/Height`.</p>

## General

*   Andy Budd reflects on how we solved so many things in theory in web development and even got the right solutions for a great user experience. But the biggest problem still remains: [companies need to spend months of work on a relaunch of their web projects just to repeat it every 4 to 5 years](https://www.andybudd.com/archives/2016/02/we_won_the_moral_argument_but_did_we_los/). That given, it’s not surprising that they don’t want to put so much effort into a project that lasts so short.</p>

## Tools

*   Here are [five great and ten useful tips for working in Sketch](https://medium.com/sketch-app-sources/5-very-special-10-sketch-tips-3d63802280bc) to make you more productive with the tool.

<figure class="fwi"><a href="https://medium.com/sketch-app-sources/5-very-special-10-sketch-tips-3d63802280bc"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb135541-e64f-416d-8742-76b028faa674/sketch-tips-opt.png" alt="Sketch tips" /></a><figcaption><a href="https://medium.com/sketch-app-sources/5-very-special-10-sketch-tips-3d63802280bc">Fifteen tips</a> make you more efficient and productive with Sketch.</figcaption></figure>

{{% feature-panel %}}

*   Do you write Bash scripts? In case you do, [Bash Infinity](https://invent.life/project/bash-infinity-framework/) is a modern boilerplate for bash that you can use if you have complex scripts and want some helper utilities.
*   Jack Franklin explores how we can [build better JavaScript bundles with Rollup](https://javascriptplayground.com/blog/2016/02/better-bundles-rollup). Rather than excluding dead code, it includes only live code (aka ‘tree-shaking’). That's only possible when using ES6 modules, though.
*   I’m a big fan of using SVG via a spritesheet and the `<use>` element. Now Kitty Giraudel published a simple Bash script that stacks your SVG symbol files into a spritesheet you can use: [spritesh](https://dev.edenspiekermann.com/2016/02/10/introducing-spritesh/).
*   Creating vector shapes can sometimes be a pain with common tools like Illustrator, Sketch, or Inkscape. Now Figma, a new app coming out soon, introduces [a feature called Vector Networks](https://medium.com/figma-design/introducing-vector-networks-3b877d2b864f) and, well, it’s amazing. It basically provides a mesh for each shape and maintains the shape in a clever way while you move parts of it. A real time-saver.

<figure class="FWI"><a href="https://medium.com/figma-design/introducing-vector-networks-3b877d2b864f"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9d41c9-ce63-47b7-a828-ccfee704c190/vector-networks-opt.png" alt="Vector Networks" /></a><figcaption>Figma’s innovative <a href="https://medium.com/figma-design/introducing-vector-networks-3b877d2b864f">Vector Networks</a> concept could save you a lot of time when creating vector shapes.</figcaption></figure>

*   Samantha Geitz wrote a great article on how you can [use Webpack to create an easy build process](https://blog.tighten.co/unpacking-webpack), not only for your JavaScript but also your CSS and images. For simple projects, it might even replace Gulp or Grunt.</p>

## Privacy

*   Unfortunately, it now seems to be common sense that [by not turning off your cell phone entirely you’re consenting to being tracked](https://www.deepdotweb.com/2016/02/11/turning-your-phone-on-is-consenting-to-being-tracked/). At least, that is how the police and secret services think about this and that’s how they act. This is a worrying step towards total surveillance, and I’m seriously considering leaving my smartphone at home more often and turning it off more often.</p>

## Web Performance

*   I’ve already mentioned BPG here. Radu-S. Amarie now explores the possibilities of the image format in a blog post. He shares [why BPG could and should replace gif images](https://eek.stfi.re/why-bpg-will-replace-gifs-and-not-only/) and probably also the current mp4-instead-of-gif hackery used on many websites to save data.</p>

## Accessibility

*   Sometimes you have an image that is only presentational but included with an `<img>` element. In such cases, instead of not providing an `alt`-attribute at all (which causes screenreaders to assume an alternative text from the file name), you can [add an empty `alt=""` and screen readers will omit the element](https://www.paciellogroup.com/blog/2016/02/short-note-on-use-of-alt-and-the-title-attribute/).</p>

## JavaScript

*   Nolan Lawson explains [how to think about databases in front-end development architectures](https://nolanlawson.com/2016/02/08/how-to-think-about-databases/). His article covers the goals of a database, the difference between memory and storage, and also provides a case study.
*   Dr. Axel Rauschmayer explains why [it’s impossible in modern web development to know everything](https://www.2ality.com/2016/02/js-fatigue-fatigue.html) and why it matters to focus on doing fewer things but doing them right.
*   We’re constantly talking about ECMAScript 2015 and using it in our projects. This always implies the usage of a transpiler like Babel, which certainly comes at a cost. Sam Saccone now evaluated [the cost of transpiling ES2015 in 2016](https://github.com/samccone/The-cost-of-transpiling-es2015-in-2016). Some interesting numbers that you might want to consider for upcoming projects.</p>

## CSS / Sass

*   While [Flexbox is great](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/ "Flexbox Is As Easy As Pie") for many things and even gives us the possibility to change the visual order of items, the feature also comes with a few issues. One of them is that not all browsers treat accessibility for screen reading the same way for this feature. Also, if you do not take care of it, the keyboard and focus order will be broken as well. Léonie Watson explains how you can [fix keyboard navigation and accessibility while reodering with Flexbox](https://tink.uk/flexbox-the-keyboard-navigation-disconnect/).</p>

## Work & Life

*   To run a remote team, you need to [set some rules to work together and have the team stick to them](https://www.netguru.co/blog/10-commandments-of-running-a-remote-team). Wiktor Schmidt shares the rules he created for Netguru, where they work remotely in a lot of places around the world.</p>

## Going beyond…

*   You know, we’ve been talking a lot about the weather last year. Now we have [an analysis and a world map of the warmth of 2015](https://www.ncdc.noaa.gov/sotc/global/201513). And in fact, it was the hottest year since the recording of weather data.
*   While it’s not a new study, it’s interesting to [read this research paper](https://eric.ed.gov/?id=EJ962881) tackling the question [if kids are too busy](https://web.extension.illinois.edu/cook/downloads/42013.pdf) (PDF) and face stress due to discretionary activities, overscheduling, and packed after-school patterns. The result? Kids want to decide on activities with their parents, kids spending a lot of time in front of a screen ask for more free time (because screen time is not), and a lot of homework creates a lot of stress. Maybe it’s not the worst idea to spend more quality time with kids at home or outside but not in front of a screen.
*   James Victore runs a great video series on YouTube and as its episodes are usually pretty short it might be worth subscribing to them. This one answers a question by a young student asking how to do meaningful work that helps other people: [How to Change the World](https://www.youtube.com/watch?v=XvK4tK99WQg).
*   Germany achieved something unique this month: The U.S. granted permission to build a room where [representatives from the German parliament can gain an insight into the TTIP documents](https://www.theregister.co.uk/2016/02/10/surreal_world_of_the_ttip/?mt=1455173994705). The fun thing about it? They need to sign a statement that they will not share anything they read in that locked(!) room without internet access. There is no way that anything of the documents’ content will leak to the public, which again makes me worried about the agreement — there likely is a good reason why no one else is supposed to read it.

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via E-Mail, RSS and online.

<em>Thanks and all the best,
Anselm</em>

