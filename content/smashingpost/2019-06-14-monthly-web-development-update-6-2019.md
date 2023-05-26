---
title: 'Monthly Web Development Update 6/2019: Rethinking Privacy And User Engagement'
slug: monthly-web-development-update-6-2019
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57b55e1c-933a-4102-81d7-5355366ec672/tech-diet-opt.png
date: 2019-06-14T14:30:00+02:00
summary: >-
  For his monthly reading list, Anselm Hannemann summarized what has happened in the web development world in the past few weeks. From browser news and UI/UX to privacy, tooling, work and life.
description: >-
  For his monthly reading list, Anselm Hannemann summarized what has happened in the web development world in the past few weeks. From browser news and UI/UX to privacy, tooling, work and life.
categories:
  - Web Development Reading List
---
Last week I read about the web turning into a dark forest. This made me think, and I’m convinced that [there’s hope in the dark forest](https://helloanselm.com/writings/hope-in-the-dark-forest). Let’s stay positive about how we can contribute to making the web a better place and stick to the principle that each one of us is able to **make an impact** with small actions. Whether it’s you adding Webmentions, removing tracking scripts from a website, recycling plastic, picking up trash from the street to throw it into a bin, or cycling instead of driving to work for a week, we all can make things better for ourselves and the people around us. We just have to do it.

## News

- Safari went ahead by introducing their new Intelligent Tracking Protection and making it the new default. Now Firefox followed, [enabling their Enhanced Tracking Protection by default](https://blog.mozilla.org/blog/2019/06/04/firefox-now-available-with-enhanced-tracking-protection-by-default/), too.
- [Chrome 75](https://developers.google.com/web/updates/2019/06/nic75) brings support for the Web Share API which is already implemented in Safari. Latency on canvas contexts has also been improved.
- The [Safari Technology Preview Release 84](https://webkit.org/blog/9170/safari-technology-preview-84-with-safari-13-features-is-now-available/) introduced [Safari 13 features](https://developer.apple.com/documentation/safari_release_notes/safari_13_beta_release_notes): warnings for weak passwords, dark mode support for iOS, support for aborting Fetch requests, FIDO2-compliant USB security keys with the Web Authentication standard, support for “Sign In with Apple” (for Safari and WKWebView). The Visual Viewport API, ApplePay in WKWebView, screen sharing via WebRTC, and an API for loading ES6 modules are also supported from now on.
- There’s an important update to Apple’s AppStore review guidelines that [requires developers to offer “Sign In with Apple”](https://developer.apple.com/news/?id=06032019j) in their apps in case they support third-party sign-in once the service is available to the public later this year.
- [Firefox 67 is out now](https://hacks.mozilla.org/2019/05/firefox-67-dark-mode-css-webrender/) with the Dark Mode CSS media query, WebRender, and side-by-side profiles that allow you to run multiple instances parallelly. Furthermore, enhanced privacy controls are built in against crypto miners and fingerprinting, as well as support for AV1 on Windows, Linux, and macOS for videos, `String.prototype.matchAll()`, and dynamic imports.

{{% feature-panel %}}

## General

- The web relies on so many open-source projects, and, yet, here’s [what it looks like to live off an open-source budget](https://staltz.com/software-below-the-poverty-line.html). Most authors are below the poverty line, forced to live in cheaper countries or not able to make a living at all from their public service of providing reliable, open software for others who then use it commercially.
- We all know that annoying client who ignores your knowledge and gets creative on their own. As a developer, Holger Bartel experienced it dozens of times; now he [found himself in the same position](https://foobartel.com/articles/of-logos-a-cucumber-and-craftmanship), having ordered a fine drink and then messed it up.

## UI/UX

- With so many dark patterns built into the software and websites we use daily, Fabricio Teixeira and Caio Braga call for a [tech diet](https://essays.uxdesign.cc/tech-diet/) for users.

{{< rimg href="https://essays.uxdesign.cc/tech-diet/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57b55e1c-933a-4102-81d7-5355366ec672/tech-diet-opt.png" sizes="100vw" caption="“Dark patterns try to manipulate users to engage further, deeper, or longer on a site or app. <a href='https://essays.uxdesign.cc/tech-diet/'>The world needs a tech diet</a>, and designers can help make it a reality. (<a href='https://essays.uxdesign.cc/tech-diet/'>Image credit</a>)" alt="Facebook, Instagram, Twitter, and Netflix Nutrition Facts." >}}

## CSS

- The CSS feature for truncating multi-line text has been [implemented in Firefox](https://webplatform.news/issues/2019-05-17). `-webkit-line-clamp: 3;`, for example, will truncate text at the end of line three.

## Security

- Aaron Parecki wrote a [step-by-step guide on setting up “Sign In with Apple”](https://developer.okta.com/blog/2019/06/04/what-the-heck-is-sign-in-with-apple).
- Many services handle DDoS protection for you these days. But how would you build it on your own? It’s certainly possible, [as this (a bit dated but still applicable) article shows](https://javapipe.com/blog/iptables-ddos-protection/).

## Privacy

- Anil Dash tries to find an answer to the question if [we can trust a company in 2019](https://anildash.com/2019/06/04/can-you-trust-a-company-in-2019/).
- Kevin Litman-Navarro analyzed over 150 privacy policies and [shares his findings in a visual story](https://www.nytimes.com/interactive/2019/06/12/opinion/facebook-google-privacy-policies.html). Not only does it take about 15 minutes on average to read a privacy policy, but most of them require a college degree or even professional career to understand them.
- Our view on privacy hasn’t changed much since the 18th century, but the circumstances are different today: Companies have a wild appetite to store more and more data about more people in a central place — data that was once exclusively accessible by state authorities. We should [redefine what privacy, personal data, and consent are](https://idlewords.com/2019/06/the_new_wilderness.htm), as Maciej Cegłowski argues in “The new wilderness.”
- The people at WebKit are very active when it comes to developing clever solutions to protect users without compromising too much on usability and keeping the interests of publishers and vendors in mind at the same time. Now they introduced “[privacy preserving ad click attribution for the web](https://webkit.org/blog/8943/privacy-preserving-ad-click-attribution-for-the-web/),” a technique that limits the data which is sent to third parties while still providing useful attribution metrics to advertisers.

{{< rimg href="https://www.nytimes.com/interactive/2019/06/12/opinion/facebook-google-privacy-policies.html" sizes="100vw" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e2ccfcb-ee6d-4ae7-b483-c0d8d0e0df6e/privacy-policy-opt.png" caption="Most privacy policies on the web are harder to read than Stephen Hawking’s “A Brief History Of Time,” <a href='https://www.nytimes.com/interactive/2019/06/12/opinion/facebook-google-privacy-policies.html'>as Kevin Litman-Navarro found out</a> by examining 150 privacy policies. (<a href='https://www.nytimes.com/interactive/2019/06/12/opinion/facebook-google-privacy-policies.html'>Image credit</a>)" alt="An overview of how hard privacy policies are to read and how much time it requires to do so. Most privacy policies are college and professional career level. Only one is comprehensible on a Middle School level." >}}

## Accessibility

- Brad Frost describes a great way to [reduce motion on websites](https://bradfrost.com/blog/post/reducing-motion-with-the-picture-element/) (of animated GIFs, for example), using the `picture` element and its media query feature.

## Tooling

- The [IP Geolocation API](https://ipgeolocationapi.com/) is an open-source real-time IP to Geolocation JSON API with detailed countries data integration that is based on the Maxmind Geolite2 database.
- Pascal Landau wrote a step-by-step tutorial on how to [build a Docker development setup for PHP projects](https://www.pascallandau.com/blog/structuring-the-docker-setup-for-php-projects/), and yes, it contains everything you might need to apply it to your own projects.

## Work &amp; Life

- Roman Imankulov from Doist shares insights into [decision-making in a flat organization](https://doist.com/blog/decision-making-flat-organization/).
- As a society, we’re overworked, have too many belongings, yet crave for more, and companies only exist to grow indefinitely. This is how we kick-started climate change in the past century and this is how we got more people than ever into burn-outs, depressions, and various other health issues, including work-related suicides. Philipp Frey has a bold theory that breaks with our current system: A research by Nässén and Larsson suggests that a 1% decrease in working hours could lead to a 0.8% decrease in GHG emissions. Taking it further, the paper suggests that [working 12 hours a week would allow us to easily achieve climate goals](https://autonomy.work/wp-content/uploads/2019/05/The-Ecological-Limits-of-Work-final.pdf), if we’re also changing the economy to not entirely focus on growth anymore. An interesting study as it explores new ways of working, living, and consuming.
- Leo Babauta shares a method that helps you [acknowledge when you’re tired](https://zenhabits.net/tired-2/). It’s hard to accept, but we are humans and not machines, so there are times when we feel tired and our batteries are low. The best way to recover is realizing that this is happening and focusing on it to regain some energy.
- Many of us are trying to achieve some minutes or hours of “deep work” a day. Fadeke Adegbuyi’s “[The Complete Guide to Deep Work](https://doist.com/blog/complete-guide-to-deep-work/)” shares valuable tips to master it.

{{% ad-panel-leaderboard %}}

## Going Beyond…

- People who live a “zero waste” life are often seen as extreme, but this is only one point of view. [Here’s the other side](https://zerowastechef.com/2018/11/22/im-not-extreme-consumerism-is/) where one of the “extreme” persons reminds us that it used to be normal to go to a farmer’s market to buy things that aren’t packed in plastic, to ride a bike, and drink water from a public fountain. Instead, our consumerism has become quite extreme and needs to change if we want to survive and stay healthy.
- Sweden wants to become climate neutral by 2045, and now they presented an interesting [visualization of the plan](https://www.fastcompany.com/90360041/sweden-is-working-hard-to-go-carbon-neutral-this-visualization-shows-exactly-how-its-happening). It’s designed to help policymakers identify and fill in gaps to ensure that the goal will be achieved. The visualization is open to the public, so anyone can hold the government accountable.
- Everybody loves them, many have them: AirPods. However, [they are an environmental disaster](https://www.vice.com/en_us/article/neaz3d/airpods-are-a-tragedy), as this article shows.
- [The North Face tricking Wikipedia](https://www.fastcompany.com/90357051/the-north-face-tricking-wikipedia-is-advertisings-dark-side) is advertising’s dark side.
- The New York Times published a guide which helps us [understand our impact on climate change based on the food we eat](https://www.nytimes.com/interactive/2019/04/30/dining/climate-change-food-eating-habits.html). This is not about going vegan but how changing eating habits can make a difference, both to the environment and our own health.

{{< signature "cm" >}}