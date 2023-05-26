---
title: Laying The Groundwork For Extensibility
slug: laying-the-groundwork-for-extensibility
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea09bc4d-c94e-4d7b-97e8-5907a5de06a1/illu-extensibility.jpg
date: 2013-11-13T14:01:55.000Z
author: extensible-web-manifesto-team
description: >-
  The Web has succeeded at interoperability and scale in a way that no other
  technology has before or since. Still, **the Web remains far from “state of
  the art”**, and it is being increasingly threatened by walled gardens. The Web
  platform often lags competitors in delivering new system and device
  capabilities to developers.
categories:
  - Coding
  - JavaScript
  - Opinion Column
  - HTML5
  - HTML
  - API
---
The Web has succeeded at interoperability and scale in a way that no other technology has before or since. Still, <strong>the Web remains far from “state of the art”</strong>, and it is being increasingly threatened by walled gardens. The Web platform often lags competitors in delivering new system and device capabilities to developers. Worse, it often hobbles new capabilities behind either high- or low-level APIs, forcing painful choices (and workarounds) on developers.

Despite browser versions being released much faster, new capabilities still take a long time to materialize, and often do so in forms that are at best frustrating and at worst nearly useless to large swathes of the developer community for solving real-world needs.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Making A Better Internet](https://www.smashingmagazine.com/2012/09/make-better-internet-story-three-acts/)
*   [HTML APIs: What They Are And How To Design A Good One](https://www.smashingmagazine.com/2017/02/designing-html-apis/)
*   [How To Design Better JavaScript APIs](https://www.smashingmagazine.com/2012/10/designing-javascript-apis-usability/)
*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)

The best recent improvements to the platform have been the result of collaborative discussions between developers and browser vendors. Sometimes these lead to big new features. More often than not, they lead to small changes that make existing systems suitable for a wider range of uses. In the absence of an intellectual framework for making these changes, we get <strong>a hodgepodge approach to design</strong>, where good ideas are not carried through and discredited patterns live on far longer than they should.

{{% feature-panel %}}

Building on the successes of tight collaboration between Web developers and browser-makers, folks who have iterated on proposals and straddled both sides of the line (including this article’s authors, <a href="https://twitter.com/wycats">Yehuda Katz</a>, <a href="https://twitter.com/dglazkov">Dimitri Glazkov</a>, <a href="https://twitter.com/ErikArvidsson">Erik Arvidsson</a>, <a href="https://twitter.com/littlecalculist">Dave Herman</a> and others) have taken a longer look at what gives Web features longevity and utility.

<a href="https://www.flickr.com/photos/opensourceway/7496803526/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ba639e5-45dc-44f6-8cea-6f1f5e548a1e/image-4.png" alt="image-4" width="500" height="281" /></a><br>
<em>The result of collaborative discussions between developers and browser vendors lead to small changes that make existing systems suitable for a wider range of uses. (<a href="https://www.flickr.com/photos/opensourceway/7496803526/">Image source</a>)</em>

Over a decade of JavaScript library work, the progressive-enhancement revolution, the advent of polyfills, and the effort to birth the “Web Components” and “Shadow DOM” specifications have taught us surprising lessons: In every period, being able to use features in both high- and low-level forms has always been desirable.

HTML is great, until it isn’t. And JavaScript-only has predictable (and thankfully, now acknowledged) drawbacks.

Thinking that there is a “right way” to build new Web features is seductive. Just define The Way To Do It™ and make all standard-bearers comply, right? Turns out, it’s not that simple. New proposals are organic and stem from needs, not from pure speculation. Low-level needs demand low-level solutions. <strong>HTML elements and CSS rules aren’t natural fits for all work.</strong> And the existence of JavaScript creates a need for new APIs near the language level.

The process of introducing new features is usually an either-or proposition (i.e. either declarative features or low-level APIs) in the short run. But in the long run, nearly all features need expression in both domains. Moreover, we have to realize that proposals for new standards are hard work. The people doing that hard work are generally trying to do the right thing and can’t wait forever to ship features. A pragmatic, realistic approach to increasing the power and quality of Web APIs is needed, one that doesn’t presuppose infinite time, effort or understanding on the part of participants — just goodwill and a willingness to build bridges.

To support this goal, <strong>the standards process needs an intervention</strong>.

<a href="https://extensiblewebmanifesto.org">The Extensible Web Manifesto</a> is a document that we have drafted to build consensus among standards participants around a few core ideas:

*   High-level APIs and markup should provide direct extension points via JavaScript.
*   Where the platform already provides high-level systems, related low-level additions should be used to explain how the high-level bits would have been written in terms of these new lower-level APIs.
*   When adding new raw power to the platform, prefer lower-level to higher-level APIs because they enable experimentation and iteration ahead of broad adoption.

The core insight is that the Web has come this far on the back of largely declarative, largely high-level features: HTML elements for forms, CSS for layout and styling, and <code>&lt;a&gt;</code> for defining relationships between documents. While each of these adds APIs, little effort has been made so far to explain how they do their work and how they relate to each other.

While you can almost sense the many strata of APIs below Web features, they go <strong>unnamed</strong>, <strong>unexplained</strong>, <strong>unconnected and unavailable to you</strong> when the system doesn’t do exactly what you need.

<a href="https://www.flickr.com/photos/opensourceway/5537457153/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32e9112a-5b3e-4ca9-925b-401229177cd6/image-2.png" alt="image-2" width="500" height="281" /></a><br>
<em>It's vital to know how APIs work and how they're connected to each other. (<a href="https://www.flickr.com/photos/opensourceway/5537457153/">Image source</a>)</em>

For example:

*   The HTML5 `canvas` element defines a programmatic 2-D bitmap API, while the long-standing `img` element is, not coincidentally, a way of rendering 2-D bitmap content. It’s easy to imagine that we could explain how JavaScript loads, unpacks and finally renders image content using the `canvas` API. Very strange that they’re separate elements and that the `img` element doesn’t have the `canvas` API, no?
*   Asking for camera access with `<input type="file" accept="image/*;capture=camera">` as well as with `getUserMedia()` is possible, but the form element version isn’t explained in the HTML specification in terms of `getUserMedia()` (which, admittedly, was added later — but no one has bothered to connect them yet).
*   That’s better than the [Geolocation API](https://www.html5rocks.com/en/tutorials/geolocation/trip_meter/). There’s currently no way to do that with an `input` element. It’s a valuable feature entirely disconnected from markup.
*   Neither HTML nor the [Web Audio API](https://dvcs.w3.org/hg/audio/raw-file/tip/webaudio/specification.html) explains how the `audio` tag works, despite the Web Audio API clearly being capable of providing the `audio` element’s implementation.

This isn’t to pick on or single out any of the hard-working developers and authors who have poured their lives into building consensus and software to introduce these capabilities. Indeed, <strong>we are grateful for their accomplishments</strong>.

The high-order bit is that the job isn’t done when both declarative and script-driven versions of a feature appear. Building a platform that’s resilient and adaptive for the long haul hinges on giving developers the confidence to take what they learn about one area and apply it evenly across the system. And that means <strong>explaining how the system works</strong> and drawing connections between the pieces.

In the case of many low-level APIs without high-level equivalents (such as Geolocation), their duty to “explain themselves” ends at the point where they have exposed a good API to JavaScript. “Good” here could mean being idiomatic and not introducing more platform magic than necessary. But when there are also declarative versions, or when only high-level versions exist, then the question looms large: How does that thing work? What are the layers below it? What APIs are required to make it go? How would you explain that API in mostly-JavaScript terms, appealing as little as possible to magical new platform APIs?

In an earlier time, attempting such a sweeping cultural change might have been foolish. Starting at a declarative level was undoubtedly a good idea. However, explaining even a bit of the underlying magic goes a long way: Exposing a DOM tree JavaScript opened new worlds to developers and bolstered the competitiveness of the platform. It also enabled the community to adapt through experimentation and enabled libraries to compete. This allows valuable, popular API ideas to potentially be standardized. <strong>The community can do it faster and with less risk </strong>than browser vendors and standards organizations can.

The answers aren’t always obvious, but the process of asking “How does that work?” is often more fruitful than it first appears. Details come into focus and missing explanations are uncovered, layer by layer. At each layer, it’s tempting to throw up our collective hands and say “It’s too hard” to explain all the stuff down there. Throw it all out. Start over. At least we won’t make the same mistakes, right?

Perhaps. But we’d also be starting from zero. Zero users, zero developers and zero useful content. The Web is the open, extensible, multi-vendor, universal platform of our lifetime. <strong>Small, meaningful changes to the Web can have an outsized impact</strong> relative to the effort involved. It’s a straightforward way to do a great deal of good. Encouraging layering, bit by bit, doesn’t mean giving up or “slowing down.” Just the opposite: It’s our only credible hope of making a Web that’s worthy to succeed the Web we have today.

<a href="https://www.flickr.com/photos/opensourceway/5319988695/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/caac4683-10d5-4f27-ba5d-2c1d3b20e894/image-1.png" alt="image-1" width="500" height="281" /></a><br>
<em>Always keep in mind to "make things better" as much as you can. (<a href="https://www.flickr.com/photos/opensourceway/5319988695/">Image source</a>)</em>

{{< signature "al, ea, il" >}}

