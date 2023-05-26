---
title: 'Monthly Web Development Update 4/2019: Design Ethics And Clarity Over Style'
slug: monthly-web-development-update-4-2019
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f080ddcf-bc9e-4dce-b2a5-3a45ba35041e/simplify-design.png
date: 2019-04-12T14:44:48+02:00
summary: >-
  From browser news to UI/UX advice and handy tips, tricks, and tools, Anselm Hannemann summarized the latest resources to help you master your daily front-end and design challenges.
description: >-
  From browser news to UI/UX advice and handy tips, tricks, and tools, Anselm Hannemann summarized the latest resources to help you master your daily front-end and design challenges.
categories:
  - Web Development Reading List
---
“[‘Ethics’ and Ethics](https://ia.net/topics/ethics-and-ethics)” is more than a typical article. It’s a detailed essay exploring what the term ‘ethics’ really means, how its meaning changed in recent times, and how diffusion of responsibility makes it hard to address and fix problems in big organizations.

Implementing design ethics, tech ethics, or business ethics as individual responsibilities might seem like a quick and easy solution, however, it’s not a very effective one as they all lack context when they don’t have support from other people who provide the foundation for their work. Only if a company’s business analysts, bookkeepers, investors, PR, marketing and sales people, as well as the CEO themself all contribute to building an ethical product, it will become successful. And because such an undertaking requires so many people to be on board, it’s rarely seen out in the wild.

How much effort and good will it takes to build a company that follows an ethical approach, is illustrated in the book *It doesn’t have to be crazy at work* by Basecamp’s Jason Fried and David Heinemeier Hansson. It helps us understand why it’s so much easier to build a non-ethical company and why even if a couple of people in a team strive for better ethics, the product or company won’t reflect this individual path yet. To help us do better, Oliver Reichenstein, the author of the article which I mentioned in the beginning, also shares a very interesting approach: designers might want to start to consider philosophy to encourage ethical thinking and advocate for values and ethics in their everyday work.

## News

- We heard the announcement some months ago, and now the first builds are out: Microsoft’s new Chromium-based Edge browser is here. So [what does that mean for front-end developers](https://css-tricks.com/edge-goes-chromium-what-does-it-mean-for-front-end-developers/)?
- [Safari 12.1](https://webkit.org/blog/8718/new-webkit-features-in-safari-12-1/) is included in macOS Mojave 10.14.4 and iOS 12.2 and with it, all users get Dark Mode for the Web, Intelligent Tracking Prevention 2.1, Payment Request API improvements, WebRTC improvements, Intersection Observer support, Web Share API, color input, and `<datalist>` support.
- [Firefox 66 has been released](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/66). From now on, autoplaying sounds will be blocked by default, and the Touch Bar on macOS is supported, too.

{{% feature-panel %}}

## General

- *[Humane by Design](https://humanebydesign.com/)* is an essential resource about focusing your design decisions on user well-being. It provides ideas and helpful resources about transparency, empowering people, fostering inclusiveness, showing respect, and making thoughtful decisions. A valuable website for any project or product you are in charge of or work on.
- What does it look like when you [try to use a browser just ten years old today](https://www.smashingmagazine.com/2019/03/web-on-internet-explorer-ie8/)? The browser’s start page returns a 404 error, Google works but returns a no-script version — not deliberately but because JavaScript errors out —, YouTube doesn’t work without even showing an error, and creating accounts at any of the big services isn’t a pleasant experience at all. This article is not only enlightening but also reveals a lot of details we can take care of to make our web projects more sustainable and available for more people, regardless of which browser they use.

## UI/UX

- “[Good design is about clarity over style](https://twitter.com/johnmaeda/status/1106148197959901185).” [Matthias Ott explores this statement](https://matthiasott.com/notes/clarity-and-style) and why many designers still like to ignore this advice and create shiny but cluttered or unclear interfaces.
- Taras Bakusevych shows examples of how we can [simplify our designs](https://uxplanet.org/how-to-simplify-your-design-69d97fde11b9) and what simplicity means after all.
- [Public Sans](https://public-sans.digital.gov/) is an open-source sans-serif font, licensed under SIL Open Font and made by the people of U.S. Web Design System.
- Patents are everywhere, but we often forget that design patterns can also be patented. Christie Tang collected some of the [most prominent patterns that we cannot use](https://medium.com/@christiet/ui-ux-patterns-you-literally-cannot-design-design-patents-from-tech-companies-21ae9643dc9e) because global players like Apple, Facebook, or Samsung hold patents on them.

{{< rimg href="https://uxplanet.org/how-to-simplify-your-design-69d97fde11b9" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f080ddcf-bc9e-4dce-b2a5-3a45ba35041e/simplify-design.png" sizes="100vw" caption="When designing a product, there are quite some pitfalls that can make a simple task overly complicated. Taras Bakusevych summarized <a href='https://uxplanet.org/how-to-simplify-your-design-69d97fde11b9'>what you need to watch out for</a>. (<a href='https://uxplanet.org/how-to-simplify-your-design-69d97fde11b9'>Image credit</a>)" alt="Eight pitfalls that complicate a design" >}}

## Web Performance

- [Chrome 73](https://www.chromestatus.com/feature/5164259990306816) now supports `imagesrcset` and `imagesizes` attributes on `link rel=preload` elements.

## Tooling

- [Spectral](https://stoplight.io/blog/introducing-spectral/) is a flexible open-source JSON linter with out-of-the-box support for the OpenAPI specification and, as such, promotes consistency in API designs.

{{% ad-panel-leaderboard %}}

## Privacy

- This article explains [why all your Alexa traffic is analyzed](https://www.bloomberg.com/news/articles/2019-04-10/is-anyone-listening-to-you-on-alexa-a-global-team-reviews-audio?srnd=technology-vp) and probably listened to by someone who works on the product software to help the voice-activated assistant respond to commands.

## JavaScript

- Jeremy Mikkola wrote a great list of [rules for autocomplete](https://jeremymikkola.com/posts/2019_03_19_rules_for_autocomplete.html).
- Jeremy Wagner explores [responsible JavaScript](https://alistapart.com/article/responsible-javascript-part-1), how frameworks often force us into unsustainable patterns, and the difference between web apps and websites.

{{< rimg href="https://alistapart.com/article/responsible-javascript-part-1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88c40087-cd2b-4515-a430-4cf231934433/responsible-javascript-opt.png" sizes="100vw" caption="JavaScript can be a performance liability and, thus, we need to use it responsibly. Jeremy Wagner <a href='https://alistapart.com/article/responsible-javascript-part-1'>shares tips for doing so</a>. (<a href='https://alistapart.com/article/responsible-javascript-part-1'>Image credit</a>)" alt="Illustration of a fire extingisher extinguishing matches" >}}

## Work & Life

- Vicky Carmichael shares [how to improve the tech event experience for marginalized people](https://blog.tito.io/posts/improving-the-tech-event-experience-for-marginalised-people) and how to move from the traditional “underrepresented group thinking” towards a more inclusive approach. A lot of the tips that make events more inclusive can be applied to a company as well.
- Charlotte Cowles on [how freelancing fuels anxiety about money](https://www.thecut.com/2019/02/why-freelancing-creates-anxiety-about-money.html), the stress you feel when you value time like money, and, finally, some tricks to escape the trap.

## Going Beyond…

- It’s impossible to reach everyone, even for giants like Google or Facebook. Seth Godin on [why reaching almost no one is fine](https://seths.blog/2019/03/almost-no-one-3/) if you ask yourself *which no one*. Your smallest viable audience holds you to account. It forces a focus and gives you nowhere to hide.
- Google Maps is one of the products most of us use daily. And yet it’s the one product by Google that doesn’t make money — yet. As it seems, [its makers are now trying to include ads into Maps](https://www.bloomberg.com/news/articles/2019-04-10/google-flips-the-switch-on-its-next-big-money-maker-maps?srnd=technology-vp) to bring more profits to Alphabet.
- George Monbiot wrote an article on “[how the media let malicious idiots take over](https://www.theguardian.com/commentisfree/2019/mar/22/political-monsters-media-jacob-rees-mogg-platforms)”. To make it clearer, let me quote the following paragraph:
<blockquote>“If our politics is becoming less rational, crueller and more divisive, this rule of public life is partly to blame: the more disgracefully you behave, the bigger the platform the media will give you. If you are caught lying, cheating, boasting or behaving like an idiot, you’ll be flooded with invitations to appear on current affairs programmes. If you play straight, don’t expect the phone to ring.”</blockquote>
- Mallen Baker explains why the environment is [too important to leave to environmentalists](https://quillette.com/2019/03/16/the-environment-is-too-important-to-leave-to-environmentalists/) and what we can do to make our lives worth living and create a surrounding that works for humans.
- It’s hard to believe in theory, but in practice, it’s very easy to make unethical choices, deliberately. This article asks [what drives people to make unethical choices](https://www.fastcompany.com/90320892/this-is-what-drives-people-to-make-unethical-choices). Sticking to your own ethical beliefs is hard when society is embracing something different — at least that’s what we tend to see from the filtered media and social media bubble. However, if we talk to people directly, I think it’s different. Many people share the same ethical beliefs and would condemn unethical behavior if it would be transparent and public. The private/unseen is what makes it easier for people to go beyond their values, supercharged by the allurement of money or getting a higher status and reputation in society.

{{< signature "cm" >}}