---
title: 'Monthly Web Development Update 1/2019: Rethinking Habits And Finding Custom Solutions'
slug: monthly-web-development-update-1-2019
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da96259d-3363-481b-aa7b-cbb76de1e34d/password-less-authentication-opt.png
date: 2019-01-18T12:40:24+01:00
summary: >-
  Anselm is back with a new edition of his Monthly Web Development Update. A reading list to help you rethink existing systems and habits and find the solution that really fits your product.
description: >-
  Anselm is back with a new edition of his Monthly Web Development Update. A reading list to help you rethink existing systems and habits and find the solution that really fits your product.
categories:
  - Web Development Reading List
---
What could be better than starting the new year with some new experiments? Today I figured it was time to rethink JavaScript tooling in one of my projects. And since we wrote everything in plain ECMAScript modules already, I thought it would be easy to serve them natively now and remove all the build and transpilation steps. Until I realized that — although we wrote most code ourselves — we have a couple of third-party dependencies in there and, of course, not all of them are ECMAScript modules. So for now, I have to give up my plans to remove all the build steps and continue to bundle and transpile things, but I’ll try to figure out a better solution to modernize and simplify our tooling setup while providing a smaller bundle to our users.

Another experiment: Just a few weeks ago I had to build a simple “go to the top of the page” button for a website. I used `requestAnimationFrame` and similar stuff to optimize event handling, but today I found a way nicer and more efficient solution that uses `IntersectionObserver` to toggle the button on the viewport. You will find that article in the JavaScript section below. The reason I wanted to share these little stories is because I believe that the most important thing is that we **review our habits and current solutions** and see whether there are better, newer, simpler ideas that could improve a product. Keep playing, keep researching, and be sure to rethink existing systems from time to time.

## News

- Joseph Medley shows us [the deprecations and removals in Chrome 72](https://developers.google.com/web/updates/2018/12/chrome-72-deps-rems), which include blocking popups during page unload via `window.open`, HTTP-Based Public Key Pinning, and deprecation of TLS 1.0 and TLS 1.1.

## UI/UX

- What Jesse Weaver is writing about here doesn’t sound like big news, but he shows how quickly we’re tempted to adopt a product strategy that works for others for our own products. Jesse shares why that’s not a good idea and [why you should always try to find your own, custom solutions](https://medium.com/s/user-friendly/emulation-is-not-a-product-strategy-cfecdbffce96).

## Web Performance

- Jack Lenox explores [how heavily website performance affects our planet’s climate](https://www.smashingmagazine.com/2019/01/save-planet-improving-website-performance/) and the effect which performance has for your visitors — beyond better load times.
- Tim Kadlec explains why [performance is an ethical point](https://timkadlec.com/remembers/2019-01-09-the-ethics-of-performance/) as it can include or exclude people, increase or reduce waste of energy, network traffic, and time.

## JavaScript

- How do we provide a “back to top” button? Well, here’s a very performance-oriented, efficient [approach that uses an Intersection Observer](https://m.signalvnoise.com/how-to-back-to-top-button-without-scroll-events/) to show and hide the button.
- Ackermann Yuriy describes how we can [use FIDO2 and the Web Authentication API to log in users](https://medium.com/@herrjemand/introduction-to-webauthn-api-5fd1fb46c285) without passwords.
- Chrome is currently working on an API called `getInstalledRelatedApps` that lets you [detect if a user has your native app installed](https://developers.google.com/web/updates/2018/12/get-installed-related-apps). This could be useful to not show them the app banners by default anymore or to let them open a specific product feature in the app directly from your website.
- Harry Wolff shows how we can [use `React.lazy` and suspense to split up the code in JavaScript apps](https://hswolff.com/blog/react-lazy-and-suspense/). This is important to reduce the original load size of the application bundle and can make a huge difference for the performance and UX of a website.

{{< rimg href="https://medium.com/@herrjemand/introduction-to-webauthn-api-5fd1fb46c285" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da96259d-3363-481b-aa7b-cbb76de1e34d/password-less-authentication-opt.png" sizes="100vw" caption="Passwordless authentication? The <a href='https://medium.com/@herrjemand/introduction-to-webauthn-api-5fd1fb46c285'>WebAuthn API</a> makes it possible. (<a href='https://medium.com/@herrjemand/introduction-to-webauthn-api-5fd1fb46c285'>Image credit</a>)" alt="Infographic showing how authentication and verification work without a password" >}}

## CSS

- Una Kravets wrote a great piece on [using Houdini and the Paint API for CSS](https://blog.logrocket.com/new-horizons-in-css-houdini-and-the-paint-api-8b307cf387bb). She demonstrates it at the example of a customized text-decoration underline style that isn’t available in standard CSS.
- Eric Portis explains the concept of the `intrinsicsize` HTML attribute that will — hopefully soon — help us [provide jank-free image loads in browsers](https://24ways.org/2018/jank-free-image-loads/) by hinting the expected dimensions of the images to the browser before it has parsed them.
- Scott Jehl updated the open-source [custom appearance `select` module](https://github.com/filamentgroup/select-css), and in this blog post he describes [how we can style `select` today](https://www.filamentgroup.com/lab/select-css.html).
- Chris Coyier summarized [how to style a web component](https://css-tricks.com/styling-a-web-component/) and decide whether we want it to inherit global styles or start from scratch.

{{< rimg href="https://blog.logrocket.com/new-horizons-in-css-houdini-and-the-paint-api-8b307cf387bb" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1ef9642-5a33-4566-9ac0-1eac0c34f3e3/houdini-and-paint-api-opt.png" sizes="100vw" caption="Una Kravet’s “<a href='https://blog.logrocket.com/new-horizons-in-css-houdini-and-the-paint-api-8b307cf387bb'>super underline</a>” example uses randomly generated underlines for each element. Made possible with Houdini and the Paint API. (<a href='https://blog.logrocket.com/new-horizons-in-css-houdini-and-the-paint-api-8b307cf387bb'>Image credit</a>)" alt="An example text with randomly generated underlines." >}}

## Work &amp; Life

- “Feeling a sense of accomplishment is an important part of our sense of self-worth. Beating up on yourself because you think you could have accomplished more can dent your confidence and self-esteem and leave you feeling depleted at the end of the day.” Lisa Evans [shares what we can do to avoid falling into that trap](https://www.fastcompany.com/90288901/5-ways-to-feel-more-accomplished-at-the-end-of-each-day).
- Itamar Turner-Trauring shares his thoughts on how to [get a job with a good work-life balance](https://codewithoutrules.com/2019/01/09/worklife-balance-silicon-valley/) when you’re competing against people who are willing to work long hours.
- Is it a good idea to provide healthcare and treatment based on digital products like apps? And if so, what are the requirements, the standards for this? [How can we ensure this is done ethically correct](https://www.antonsten.com/prescribed-tech/)? How do we set the limits, the privacy boundaries, how far do we allow companies to go with experiments here? Would personalized content be fine? Is it okay to share data collected from our devices with healthcare providers or insurances? These are questions we will have to ask ourselves and find an individual answer for.
- This article about [how Millenials became the burnout generation](https://www.buzzfeednews.com/article/annehelenpetersen/millennials-burnout-generation-debt-work) hit me hard this week. I see myself in this group of people described as “Millenials” (I do think it affects way more people than just the 20-year-olds) and I could relate to so many of the struggles mentioned in there that I now think that these problems are bigger than I ever imagined. They will affect society, politics, each individual on our planet. Given that fact, it’s crazy to hear that most people today will answer that they don’t have a friend they could talk to about their fears and anything else that disturbs them while two decades ago the average answer was still around five. Let’s assure our friends that we’re there for them and that they can talk to us about tough things. 2019 should be a year in which we — in our circle of influence — make it great to live in a human community where we can think with excitement and happiness about our friends, neighbors, and people we work with or talk to on the Internet.
- We all try to accommodate so many things at the same time: being successful and productive at work, at home, with our children, in our relationships, doing sports, mastering our finances, and some hobbies. But we blindly ignore that it’s impossible to manage all that on the same level at the same time. We feel regret when we don’t get everything done in a specific timeframe such as at the end of a calendar year. Shawn Blanc argues that [we should celebrate what we did do instead of feeling guilty for what we didn’t do](https://shawnblanc.net/2019/01/regret-vs-celebration/).

{{% ad-panel-leaderboard %}}

## Going Beyond…

- There are words, and then there are words. Many of us know how harmful “just” can be as a word, how prescriptive, how passively aggressive it is. Tobias Tom challenges whether “should” is a useful word by examining the implicit and the result of using it in our daily language. [Why “should” can be harmful to you](https://tobiastom.name/articles/should) and to what you want to achieve.
- “We all know what we stand for. The trick is to state our values clearly — and to stand by them,” [says Ben Werdmuller](https://werd.io/2019/values-values-values) and points out how important it is to think about your very own red line that you don’t want to cross regardless of external pressure you might face or money you might get for it.
- Exciting news for climate improvement this week: A team of arborists has [successfully cloned and grown saplings from the stumps of some of the world’s oldest and largest coast redwoods](https://e360.yale.edu/digest/arborists-have-cloned-ancient-redwoods-from-their-massive-stumps), some of which were 3,000 years old and measured 35 feet in diameter when they were cut down in the 19th and 20th centuries. Earlier this month, 75 of the cloned saplings were planted at the Presidio National Park in San Francisco. What makes this so special is the fact that these ancient trees can sequester 250 tons of carbon dioxide from the atmosphere over their lives, compared to 1 ton for an average tree.
- The ongoing technological development and strive to build new services that automate more and more things make it [even more critical to emphasize human connection](https://www.fastcompany.com/90289814/the-importance-of-human-brands). Companies that show no effort in improving things for their clients, their employees, or the environment will begin to struggle soon, Ryan Paugh says.
- We usually don’t expect much nice news about technology inventions from the car industry and their willingness to share it with others. But Toyota now has decided to [share their automated safety system ‘Guardian’ with competitors](https://www.forbes.com/sites/alanohnsman/2019/01/08/toyota-offers-ai-enabled-crash-avoidance-tech-to-rivals-amid-auto-safety-push-at-ces/#33c7137c3dfa). It uses self-driving technology to keep cars from crashing. “We will not keep it proprietary to ourselves only. But we will offer it in some way to others, whether that’s through licensing or actual whole systems,” says Gill Pratt from the company.

Thank you for reading! I’m happy to be back with this new edition of my Web Development Update in 2019 and grateful for all [your ongoing support](https://wdrl.info/donate). It makes me happy to hear that so many people find this resource helpful. So if you enjoyed it, please feel free to share it with people you know, give me feedback, or support it with a small amount of money. *—Anselm*

{{< signature "cm" >}}