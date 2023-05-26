---
title: 'Web Development Reading List #139: jQuery 3, Web Payment API, And ES6 Tricks'
slug: web-development-reading-list-139
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20246880-ae4f-4306-8156-11a5f1e9f2d4/wdrl-139-opt.png'
date: 2016-05-27T17:28:25.000Z
author: anselm-hannemann
description: >-
  Finding our passion is a big challenge for all of us as human beings. At some
  point in life, we try to figure out what our purpose in this world is, what
  our future will look like. And for some of us, the answers we find to these
  questions are constantly changing.

  The **constant search to find answers lets us stay curious**, creative, vital
  — and if that’s missing, we need to find our passion again by exploring what
  things we like in our world, what makes us happy. Searching takes time, and we
  should invest that time — maybe by cutting down watching TV by an hour a week.
categories:
  - Web Development Reading List
---
Finding our passion is a big challenge for all of us as human beings. At some point in life, we try to figure out what our purpose in this world is, what our future will look like. And for some of us, the answers we find to these questions are constantly changing.

The <strong>constant search to find answers lets us stay curious</strong>, creative, vital — and if that’s missing, <a href="https://www.smashingmagazine.com/2015/05/rekindling-your-passion-for-web-design/">we need to find our passion again</a> by exploring what things we like in our world, what makes us happy. Searching takes time, and we should invest that time — maybe by cutting down watching TV by an hour a week.</p>

## <span class="rh">Further Reading</span> on SmashingMag

*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)

## News

*   We’re getting towards jQuery 3’s final steps now. [With the Release Candidate now available](https://blog.jquery.com/2016/05/20/jquery-3-0-release-candidate-released/), they also announced a new migration tool that people can use to make the transition from older jQuery versions to the new one.
*   Following Chrome and Firefox, [WebKit will block geolocation API requests](https://trac.webkit.org/changeset/200686) in future releases, except in HTTPS network contexts.</p>

## Generic

*   Cloudflare has constantly been under fire for displaying captchas and blocking various visitors, especially if they use Tor networks or special Virtual Private Networks. But this is about more than just a few users; [this article shares how many people are affected by Cloudflare’s firewalls](https://www.slashgeek.net/2016/05/17/cloudflare-is-ruining-the-internet-for-me/), especially if they live in Africa and Southeast Asia.</p>

## HTML & SVG

*   How convenient would it be if payment forms would just let you scan a credit card and fill out your invoice and delivery address? Despite most sites not using them, [there are web standards](https://html.spec.whatwg.org/multipage/forms.html#enabling-client-side-automatic-filling-of-form-controls) that define exactly this behavior and many browsers actually support it already. For example, Safari lets you scan a credit card if you define the field properly. Jason Grigsby gives you [a tutorial on how to properly format payment forms](https://blog.cloudfour.com/autofill-what-web-devs-should-know-but-dont/). Finally, we will get an entire [web payment API](https://w3c.github.io/browser-payment-api/specs/paymentrequest.html) that will offer developers a great way to build convenient checkout processes where the browser will autofill all information.
*   Using account registration pages on a mobile phone is annoying, especially if you need to enter a password. But there’s a way to make this more convenient for your users: [Safari provides an option to let users use the iCloud keychain to generate a password on demand](https://stackoverflow.com/questions/19959887/safari-autofill-trigger-password-suggestions-in-devise-registration-form/29594874).

{{% feature-panel %}}

<figure><a href="https://blog.cloudfour.com/autofill-what-web-devs-should-know-but-dont/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ac67d44-5b74-4199-bafe-bdef3e61ded4/autofill-cloudfour-opt.png" alt="Jason Grigsby shares how to build forms that support cross-browser autofill and how to take advantage of new features such as scanning credit cards." width="500" height="384" /></a><figcaption>Jason Grigsby shares <a href="https://blog.cloudfour.com/autofill-what-web-devs-should-know-but-dont/">how to build forms that support cross-browser autofill</a> and how to take advantage of new features such as scanning credit cards.</figcaption></figure>

## Accessibility

*   [Frend](https://frend.co/) is a dependency-free collection of accessible, modern front-end components. They are built with web standards as a priority and aim to avoid assumptions about tooling or environment.

<figure><a href="https://frend.co/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4890fdc9-38e2-4d05-8f17-12a0ea48d22e/frend-opt.png" alt="An accessible accordion component from Frend." width="500" height="366" /></a><figcaption>An accessible accordion component from <a href="https://frend.co/">Frend</a>. Each component in the collection is compliant, keyboard navigable, and properly interpreted by assistive technologies. (Image credit: <a href="https://frend.co/">Frend</a>)</figcaption></figure>

## JavaScript

*   [JavaScript variable hoisting can confuse people](https://bytearcher.com/articles/variable-hoisting-explained/), and this is actually the reason why many coding conventions have a rule that all variables need to be defined at the top of a function. ES6’s `let` and `const` however, will change this simply by working as one would expect it.
*   A great step towards element queries and better control over modules in our front-ends is coming to browsers now with the new [Resize Observer API](https://wicg.github.io/ResizeObserver/) that observes changes to an element’s size. This, together with the [Houdini](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/) project, could serve well for a custom element query polyfill. No browser supports this yet, but [all vendors consider it](https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/iHXS9S66bAw/BM1mV5BQAAAJ) and see it as a useful addition.
*   Dr. Axel Rauschmayer shares [six great ES6 tricks](https://www.2ality.com/2016/05/six-nifty-es6-tricks.html). How to make function parameters mandatory, for example.</p>

## CSS / Sass

*   The `will-change` property is still widely unknown and people don’t know exactly when and how to use it properly. Fortunately, the W3C took the effort to write up [how to use `will-change` well](https://drafts.csswg.org/css-will-change/#using).

And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.

<em>Thanks and all the best,
Anselm</em>

