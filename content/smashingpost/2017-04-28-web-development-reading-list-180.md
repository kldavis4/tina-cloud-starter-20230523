---
title: >-
  Web Development Reading List #180: DNS Over HTTPS, HAProxy Performance, And
  Decentralized AI
slug: web-development-reading-list-180
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac553473-dac6-43fa-a6fa-680a529d6a1a/wdrl-180-opt.png'
date: 2017-04-28T17:47:33.000Z
author: anselm-hannemann
description: >-
  We all have fears and doubts. It’s not different for you than for me. Over the
  last weeks, “well-known” people on Twitter started to share mistakes they made
  in life or their careers. I think it’s very helpful to read that **we all make
  mistakes**.

  We all have to learn and improve, and people who are on a stage at an event
  for the 100th time are still known to be extremely nervous. Let’s realign our
  views, our expectations and, instead of being afraid of making mistakes, try
  to improve our knowledge and let others learn from the things that didn’t go
  as expected.
categories:
  - Web Development Reading List
---
We all have to learn and improve, and people who are on a stage at an event for the 100th time are still known to be extremely nervous. Let’s realign our views, our expectations and, instead of being afraid of making mistakes, try to improve our knowledge and let others learn from the things that didn’t go as expected.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [How To Choose The Right Face For A Beautiful Body](https://www.smashingmagazine.com/2012/05/how-to-choose-the-right-face-for-a-beautiful-body/)
*   [Algorithm-Driven Design: How Artificial Intelligence Is Changing Design](https://www.smashingmagazine.com/2017/01/algorithm-driven-design-how-artificial-intelligence-changing-design/)
*   [Moving From Photoshop And Illustrator To Sketch: A Few Tips For UI Designers](https://www.smashingmagazine.com/2017/04/photoshop-illustrator-sketch-ui/)

## Concept & Design

*   The Airbnb Design team published a new tool called [react-sketchapp](https://github.com/airbnb/react-sketchapp). It’s a library that allows you to [write React components that render to Sketch documents](https://airbnb.design/painting-with-code/), providing a super useful data exchange between developers and designers.

{{% feature-panel %}}

<figure><a href="https://github.com/airbnb/react-sketchapp"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b42b62aa-f51d-4c2e-8f54-3b60259520df/react-sketchapp-opt.png" width="800" height="560" alt="React-Sketchapp" /></a><figcaption>Using React to write Sketch files? <a href="https://github.com/airbnb/react-sketchapp">React-sketchapp</a> makes it possible. (<a href="https://github.com/airbnb/react-sketchapp">Image credit</a>)</figcaption></figure>

## Tools & Workflows

*   Caddy, an HTTP/2 server that has automatic HTTPS built in, was [released in version 0.10](https://caddyserver.com/blog/caddy-0_10-released) and brings man-in-the-middle (MITM) attack detection and HTTP/2 Server Push.
*   Kenneth Auchenberg published a new tool called “[Remote Debug iOS WebKit Adapter](https://github.com/RemoteDebug/remotedebug-ios-webkit-adapter).” It lets you [debug Safari and other WebViews remotely](https://medium.com/@auchenberg/hello-remotedebug-ios-webkit-adapter-debug-safari-and-ios-webviews-from-anywhere-2a8553df7465) on iOS via Developer Tools in Chrome, Firefox, and even in Microsoft’s VS Code.
*   [secureoperator](https://github.com/fardog/secureoperator) is a proxy for DNS that uses [Google’s DNS over HTTPS](https://developers.google.com/speed/public-dns/docs/dns-over-https) technology. A nice experiment that brings security to a still weak bridge. And while technologies to add security to the DNS do already exist (DANE and DNSSEC, for example), they’re not as widespread and not free of weak points. However, using DNS via Google also means trusting a third party that could intercept the requests at any time. One thing is for certain, according to their [privacy policy](https://developers.google.com/speed/public-dns/privacy), they do store logs with your IP address and other information.
*   Due to its improvements over MySQL and independence from Oracle, MariaDB is getting lots of traction at the moment. However, there are certain [differences in how MariaDB/MySQL and PostgreSQL handle data](https://www.cybertec.at/why-favor-postgresql-over-mariadb-mysql/). If you take a closer look, you’ll notice that running into weird miscalculations or errors is much more likely with MariaDB/MySQL while PostgreSQL will return a strict fail if a value doesn’t match a field type.</p>

## Security

*   Clémentine Maurice and other researchers found a way to [steal data from the CPU cache shared by two Virtual Machines](https://www.theregister.co.uk/2017/03/31/researchers_steal_data_from_shared_cache_of_two_cloud_vms/). This was demonstrated on Amazon Web Services but affects all Virtual Machine-based environments. Clear evidence that we still have little idea of how secure or insecure cloud environments actually are.</p>

## Privacy

*   Amazon announced “Echo Look”, an improved Alexa [device that does not only listen to a room’s activity but also has a camera](https://motherboard.vice.com/en_us/article/amazon-echo-look-bedroom-camera) to see what’s happening. The purpose? To give you a style check. And as you would expect from Amazon, they say they store the captured data for an indefinite amount of time in their cloud. I bet that a lot of people will buy this device despite of this, even those who claim to care about their privacy.</p>

## Web Performance

*   Sachin Malhotra shares how they [fine tuned HAProxy to achieve 2 million concurrent SSL connections](https://medium.freecodecamp.com/how-we-fine-tuned-haproxy-to-achieve-2-000-000-concurrent-ssl-connections-d017e61a4d27) at ‘Hike’.</p>

## HTML & SVG

*   Stuart Frisby from Booking.com shares [what they learned from using system fonts](https://booking.design/implementing-system-fonts-on-booking-com-a-lesson-learned-bdc984df627f) and the improvements they made to a default stack which many of us are using.

<figure><a href="https://booking.design/implementing-system-fonts-on-booking-com-a-lesson-learned-bdc984df627f"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3dc9d3a-6c58-4feb-98dc-02448c1c4d57/booking-font-choice-opt.png" width="800" height="482" alt="Booking.com font choices" /></a><figcaption>Booking.com provides valuable insights into how they <a href="https://booking.design/implementing-system-fonts-on-booking-com-a-lesson-learned-bdc984df627f">reconsidered their long-established font choices</a> to improve readability. (Image credit: <a href="https://booking.design/implementing-system-fonts-on-booking-com-a-lesson-learned-bdc984df627f">Cătălin Bridinel</a>)</figcaption></figure>

## JavaScript

*   J. Renée Beach shares how to [manage focus and blur in a composite widget made in React](https://medium.com/@jessebeach/dealing-with-focus-and-blur-in-a-composite-widget-in-react-90d3c3b49a9b).</p>

## Going Beyond…

*   Jonathan Taplin wrote an essay about [the tech moguls dominating the free market today](https://www.nytimes.com/2017/04/22/opinion/sunday/is-it-time-to-break-up-google.html?_r=0) and why it’s important that we as consumers are aware of the huge influence monopolies have not only on our lives but on politics, too.
*   The outdoor clothing manufacturer Patagonia [started to sell used clothing for little money](https://python.sh/2017/4/patagonia-begins-selling-used-clothing). An unusual move for such a company as it undermines its traditional business model of selling new clothes.
*   Iterating on their already existing, centralized AI technology, Google researchers shared [their vision of federated machine learning](https://research.googleblog.com/2017/04/federated-learning-collaborative.html). This basically means that every Google device will contribute to the training data by locally processing the information — a much more efficient and less costly approach for Google. The technology is already being tested on Android via Google’s software keyboard. Let’s see how this will work out when it comes to dealing with fake news, spam content or violence promotion in Google’s search results.
*   Mastodon is a relatively new social microblogging network, aiming to replace Twitter. It uses a federated approach, which means everyone can create an instance that shares data with other instances. But it’s not as easy as one would initially think. By providing an instance, you suddenly become responsible for the content of other people, which can be a pretty nasty experience [as this story shows](https://cherubini.casa/why-i-shut-down-wizards-town-and-left-mastodon-6d4e631346b3).

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

