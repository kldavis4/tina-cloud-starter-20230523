---
title: 'Monthly Web Development Update 11/2018: Just-In-Time Design And Variable Font Fallbacks'
slug: monthly-web-development-update-11-2018
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89d8ff95-a007-4bcb-9eca-93900d681324/color-palette-opt.png
date: 2018-11-23T14:00:24+01:00
summary: >-
  Major updates, new tools, valuable lessons learned. In his monthly reading list, Anselm summarizes everything that’s new and important to know for web developers this November.
description: >-
  Major updates, new tools, valuable lessons learned. In his monthly reading list, Anselm summarizes everything that’s new and important to know for web developers this November.
categories:
  - Web Development Reading List
---
How much does design affect the perception of our products and the users who interact with them? To me, it’s getting clearer that design makes all the difference and that unifying designs to a standard model like the Google Material Design Kit doesn’t work well. By using it, you’ll get a decent design that works from a technical perspective, of course. But you won’t create a unique experience with it, an experience that lasts or that reaches people on a personal level.

Now think about which websites you visit and if you enjoy being there, reading or even contributing content to the service. In my opinion, that’s something that Instagram manages to do very well. **Good design fits your company’s purpose** and adjusts to what visitors expect, making them feel comfortable where they are and enabling them to connect with the product. Standard solutions, however, might be nice and convenient, but they’ll always have that anonymous feel to them which prevents people from *really* caring for your product. It’s in our hands to shape a better experience.

## News

- Yes, [Firefox 63 is here](https://hacks.mozilla.org/2018/10/firefox-63-tricks-and-treats/), but what does it bring? Web Components support including Custom Elements with built-in extends and Shadow DOM. `prefers-reduced-motion` media query support is available now, too, Developer Tools have gotten a font editor to make playing with web typography easier, and the accessibility inspector is enabled by default. The `img` element now supports the `decoding` attribute which can get `sync`, `async`, or `auto` values to hint the preferred decoding timing to the browser. Flexbox got some improvements as well, now supporting `gap` (`row-gap`, `column-gap`) properties. And last but not least, the Media Capabilities API, Async Clipboard API, and the `SecurityPolicyViolationEvent` interface which allows us to send CSP violations have also been added. Wow, what a release!
- [React 16.6 is out](https://reactjs.org/blog/2018/10/23/react-v-16-6.html#reactlazy-code-splitting-with-suspense) &mdash; that doesn’t sound like big news, does it? Well, this minor update brings `React.lazy()`, a method you can use to do code-splitting by wrapping a dynamic import in a call to `React.lazy()`. A huge step for better performance. There are also a couple of other useful new things in the update.
- The latest Safari Tech Preview 68 brings `<input type="color">` support and changes the default behavior of links that have `target="_blank"` to get the `rel="noopener"` as implied attribute. It also includes the new `prefers-color-scheme` media query which allows developers to adapt websites to the light or dark mode settings of macOS.
- From now on, PageSpeed Insights, likely still the most commonly used performance analysis tool by Google, [is now powered by project Lighthouse](https://blog.chromium.org/2018/11/pagespeed-insights-now-powered-by.html) which many of you have already used additionally. A nice iteration of their tool that makes it way more accurate than before.

{{% feature-panel %}}

## General

- Explore structured learning paths to discover everything you need to know about building for the modern web. [web.dev](https://web.dev/learn) is the new resource by the Google Web team for developers.
- No matter how you feel about Apple Maps (I guess most of us have experienced moments of frustration with it), but [this comparison about the maps data](https://www.justinobeirne.com/new-apple-maps) they used until now and the data they currently gather for their revamped Maps is fascinating. I’m sure that the increased level of detail will help a lot of people around the world. Imagine how landscape architects could make use of this or how rescue helpers could profit from that level of detail after an earthquake, for example.

{{< rimg href="https://web.dev/learn" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4fe5120-add8-42e3-8ce6-c628d39a5f79/webdev-opt.png" sizes="100vw" caption="From fast load times to accessibility &mdash; <a href='https://web.dev/learn'>web.dev</a> helps you make your site better." alt="Web.dev" >}}

## HTML &amp; SVG

- Andrea Giammarchi wrote a polyfill library for Custom Elements that allows us to [extend built-in elements in Safari](https://medium.com/@WebReflection/extending-built-in-elements-9dce404b75b4). This is super nice as it allows us to extend native elements with our own custom features &mdash; something that works in Chrome and Firefox already, and now there’s this little polyfill for other browsers as well.
- Custom elements are still very new and browser support varies. That’s why this [html-parsed-element](https://github.com/WebReflection/html-parsed-element) project is useful as it provides a base custom element class with a reliable `parsedCallback` method.

## JavaScript

- Leonardo Maldonado compiled a [collection of JavaScript concepts that are very useful to know for developers](https://github.com/leonardomso/33-js-concepts). The list includes both videos and articles so you can choose your preferred way of learning.
- When a video doesn’t work on a website anymore and you’re using Service Workers, the [problem might be the Range request](https://philna.sh/blog/2018/10/23/service-workers-beware-safaris-range-request/). Phil Nash debugged this weird issue on his page and explains how you can do too.

## UI/UX

- How do you build a color palette? Steve Schoger from RefactoringUI shares a [great approach that meets real-life needs](https://refactoringui.com/previews/building-your-color-palette/).
- Matthew Ström’s article “[Just-in-time Design](https://matthewstrom.com/writing/just-in-time-design.html)” mentions a solution to minimize the disconnection between product design and product engineering. It’s about adopting the Just-in-time method for design. Something that my current team was very excited about and I’m happy to give it a try.
- [HolaBrief](https://www.holabrief.com/) looks promising. It’s a tool that improves how we create design briefs, keeping everyone on the same page during the process.
- Mental models are explanations of how we see the world. Teresa Man wrote about how we can apply [mental models to product design](https://heydesigner.com/blog/mental-models-in-product-design/) and why it matters.
- Shelby Rogers shares how we can build [better 404 error pages](https://www.smashingmagazine.com/2018/11/the-101-course-on-crafting-404-pages/).

{{< rimg href="https://refactoringui.com/previews/building-your-color-palette/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89d8ff95-a007-4bcb-9eca-93900d681324/color-palette-opt.png" sizes="100vw" caption="Steve Schoger looks into <a href='https://refactoringui.com/previews/building-your-color-palette/'>color palettes that really work</a>. (<a href='https://refactoringui.com/previews/building-your-color-palette/'>Image credit</a>)" alt="Building Your Color Palette" >}}

## Tooling

- The color palette generator [Palx](https://palx.jxnblk.com/dc143f) lets you enter a base hex value and generates a full color palette based on it.

## Security

- This neat Python tool is a [great XSS detection utility](https://github.com/s0md3v/XSStrike).
- Svetlin Nakov wrote a book about *[Practical Cryptography for Developers](https://cryptobook.nakov.com/)* which is available for free. If you ever wanted to understand or know more about how private/public keys, hashing, ciphers, or signatures work, this is a great place to start.
- Facebook claimed that they’d reveal who pays for political ads. Now VICE researched this new feature and [posed as every single of the current 100 U.S. senators](https://news.vice.com/en_us/article/xw9n3q/we-posed-as-100-senators-to-run-ads-on-facebook-facebook-approved-all-of-them) to run ads ‘paid by them’. Pretty scary to see how one security failure that gives users more power as intented can change world politics.

{{% ad-panel-leaderboard %}}

## Privacy

- I don’t like linking to paid, restricted articles but [this one made me think](https://www.wsj.com/articles/your-smartphones-location-data-is-worth-big-money-to-wall-street-1541131260) and you don’t need the full story to follow me. When Tesla announced that they’d ramp up model 3 production to 24/7, a lot of people wanted to verify this, and a company that makes money by providing geolocation data captured smartphone location data from the workers around the Tesla factories to confirm whether this could be true. Another sad story of how easy it is to track someone without consent, even though this is more a case of mass-surveillance than individual tracking.

## Web Performance

- Addy Osmani shares a performance case study of Netflix to improve Time-to-Interactive of the streaming service. This includes switching from React and other libraries to plain JavaScript, prefetching HTML, CSS, and (React) JavaScript and the usage of React.js on the server side. Quite interesting to see [so many unconventional approaches](https://medium.com/dev-channel/a-netflix-web-performance-case-study-c0bcde26a9d9) and their benefits. But remember that what works for others doesn’t need to be the perfect approach for your project, so take it more as inspiration than blindly copying it.
- Harry Roberts explains all the details that are important to know about [CSS and Network Performance](https://csswizardry.com/2018/11/css-and-network-performance/). A comprehensive collection that also provides some very interesting tips for when you have `async` scripts in your code.
- I love the tiny [ImageOptim app](https://imageoptim.com/) for batch optimizing my images for web distribution. But now there’s an impressive [web app called “Squoosh”](https://squoosh.app/) that lets you optimize images perfectly in your web browser and, as a bonus, you can also resize the image and choose which compression to use, including mozJPEG and WebP. Made by the Google Chrome team.

## CSS

- Oliver Schöndorfer shows how we can [serve a Variable Font to modern browsers while providing a fallback web font for older browsers](https://www.zeichenschatz.net/typografie/implementing-a-variable-font-with-fallback-web-fonts.html). This is especially interesting as Oliver goes deep into optimizing the fallback font and adjusting it via CSS in order to match the variable font as closely as possible in case a font swap happens during page load.
- Andy Clarke shows [what’s needed to redesign a product and website to support bright and dark modes](https://stuffandnonsense.co.uk/blog/redesigning-your-product-and-website-for-dark-mode) which were introduced to several Operating Systems recently and will soon be supported via media queries by various browsers.
- While `background-clip` is not super new, it hasn’t been very useful due to the lack of browser support. But as Sime Vidas shows, [CSS Background Clip is now widely supported](https://webplatform.news/issues/2018-11-02), giving us great opportunities to enhance the text styling on our websites.

{{< rimg href="https://stuffandnonsense.co.uk/blog/redesigning-your-product-and-website-for-dark-mode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27951bb8-be6b-44cd-bf70-e1941f39a725/dark-mode-opt.png" sizes="100vw" caption="How to design for dark mode while maintaining accessibility, readability, and a consistent feel for your brand? Andy Clarke shares some <a href='https://stuffandnonsense.co.uk/blog/redesigning-your-product-and-website-for-dark-mode'>valuable tips</a>. (<a href='https://stuffandnonsense.co.uk/blog/redesigning-your-product-and-website-for-dark-mode'>Image credit</a>)" alt="Redesigning your product and website for dark mode" >}}

{{% ad-panel-leaderboard %}}

## Work &amp; Life

- Stig Brautaset wrote about [why he nearly failed to get into his job as a submarine sonar operator](https://www.brautaset.org/articles/2018/submarine-sonar-hiring.html) due to a silly hiring rule and how he made the best out of the situation and succeeded. A valuable lesson that shows that you shouldn’t stick too much to guidelines and rules when it comes to hiring people but trust your gut and listen to their stories instead.
- In “[People, Not Robots: Bringing the Humanity Back to Customer Support](https://m.signalvnoise.com/people-not-robots-bringing-the-humanity-back-to-customer-support-1d68855bf6e0),” Kristin Aardsma shares why it’s important to rethink how customer support works.
- Marcus Wermuth reflects on why [becoming a manager is not a promotion but a career change](https://open.buffer.com/maker-to-manager/).

## Going Beyond…

- Neil Stevenson on [Steve Jobs, creativity and death](https://medium.com/ideo-stories/putting-a-dent-in-the-universe-steve-jobs-creativity-and-death-d0a5b0755ece) and why this is a good story for life. Although copying Steve Jobs is likely not a good idea, Neil provides some different angles on how we might want to work, what to do with our lives, and why purpose matters for many of us.
- Ryan Broderick reflects on what we did by inventing the internet. He concludes that all that radicalism in the world, those weird political views are all due to the invention of social media, chat software and the (not so sub-) culture of promoting and embracing all the bad things happening in our society. Remember 4chan, Reddit, and similar services, but also Facebook et al? They contribute and embrace not only good ideas but often stupid or even harmful ones. “[This is how we radicalized the world](https://www.buzzfeednews.com/article/ryanhatesthis/brazil-jair-bolsonaro-facebook-elections)” is a sad story to read but well-written and with a lot of inspiring thoughts about how we shape society through technology.
- I’m sorry, this is another link about Bitcoin’s energy consumption, but it shows that [Bitcoin mining alone could raise global temperatures above the critical limit (2°C) by 2033](https://motherboard.vice.com/en_us/article/neganb/bitcoin-mining-could-raise-global-temperatures-by-2-c). It’s time to abandon this inefficient type of cryptocurrency. Now.
- Wilderness is something special. And our planet has less and less of it, as [this article](https://www.nature.com/articles/d41586-018-07183-6) describes. The map reveals that only very few countries have a lot of wilderness these days, giving rare animals and species a place to live, giving humans a way to explore nature, to relax, to go on adventures.
- We definitely live in exciting times, but it makes me sad when I read that in the last forty years, [wildlife population declined by 60%](https://www.worldwildlife.org/press-releases/wwf-report-reveals-staggering-extent-of-human-impact-on-planet). That’s a pretty massive scale, and if this continues, the world will be another place when I’m old. Yes, when *I* am old, a lot of animals I knew and saw in nature will not exist anymore by then, and the next generation of humans will not be able to see them other than in a museum. It’s not entirely clear what the reasons are, but climate change might be one thing, and the ever-growing expansion of humans into wildlife areas probably contributes a lot to it, too.

{{< signature "cm, il" >}}