---
title: 'Monthly Web Development Update 10/2018: The Hurricane Web, End-To-End-Integrity, And RAIL'
slug: monthly-web-development-update-10-2018
author: anselm-hannemann
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44b5ff8-cd70-4a9e-b14c-0f4883acf9e1/ipfs-opt.png
date: 2018-10-19T15:19:58+02:00
summary: >-
  What happened in the web dev world in the past four weeks? In his monthly reading list, Anselm summarized everything you need to know — from browser news to valuable techniques, tools, and lessons learned.
description: >-
  What happened in the web dev world in the past four weeks? In his monthly reading list, Anselm summarized everything you need to know — from browser news to valuable techniques, tools, and lessons learned.
categories:
  - Web Development Reading List
---
<p>With the latest studies and official reports out this week, it seems that to avoid an irreversible climate change on Planet Earth, we need to act drastically within the next ten years. This rose a couple of doubts and assumptions that I find worth writing about.</p>
<p>One of the arguments I hear often is that<a href="https://helloanselm.com/writings/70percent-co2-emissions-from-100-companies"> we as individuals cannot make an impact</a> and that climate change is “the big companies’ fault”. However, we as the consumers are the ones who make the decisions what we buy and from whom, whose products we use and which ones we avoid. And by choosing wisely, <strong>we can make a change</strong>. By talking to other people around you, by convincing your company owner to switch to renewable energy, for example, we can transform our society and economy to a more sustainable one that doesn’t harm the planet as much. It will be a hard task, of course, but we can’t deny our individual responsibility.</p>
<p>Maybe we should take this as an occasion to rethink <a href="https://helloanselm.com/writings/paring-down-your-life">how much we really need</a>. Maybe <a href="https://helloanselm.com/writings/morning-in-the-forest">going out into nature</a> helps us reconnect with our environment. Maybe <a href="https://helloanselm.com/writings/building-a-bed">building something from hand and with slow methods</a>, trying to understand the materials and their properties, helps us grasp how valuable the resources we currently have are — and what we would lose if we don’t care about our planet now.</p>
## News
<ul>
<li><a href="https://developers.google.com/web/updates/2018/10/nic70">Chrome 70 is here</a> with Desktop Progressive Web Apps on Windows and Linux, public key credentials in the Credential Management API, and named Workers.</li>
<li><a href="https://www.postgresql.org/about/news/1894/">Postgres 11 is out</a> and brings more robustness and performance for partitioning, enhanced capabilities for query parallelism, Just-in-Time (JIT) compilation for expressions, and a couple of other useful and convenient changes.</li>
<li>As the new macOS Mojave and iOS 12 are out now, Safari 12 is as well. <a href="https://developer.apple.com/safari/whats-new/">What’s new in this version</a>? A built-in password generator, a 3D and AR model viewer, icons in tabs, web pages on the latest watch OS, new form field attribute values, the Fullscreen API for iOS on iPads, font collection support in WOFF2, the <code>font-display</code> loading CSS property, Intelligent Tracking Prevention 2.0, and a couple of security enhancements.</li>
<li>Google’s decision to force users to log into their Google account in the browser to be able to access services like Gmail <a href="https://blog.cryptographyengineering.com/2018/09/23/why-im-leaving-chrome/">caused a lot of discussions</a>. Due to the negative feedback, <a href="https://www.blog.google/products/chrome/product-updates-based-your-feedback/">Google promptly announced changes for v70</a>. Nevertheless, this clearly shows the interests of the company and in which direction they’re pushing the app. This is unfortunate as Chrome and the people working on that project shaped the web a lot in the past years and brought the ecosystem “web” to an entirely new level.</li>
<li><a href="https://blogs.windows.com/msedgedev/2018/10/04/edgehtml-18-october-2018-update/">Microsoft Edge 18 is out</a> and brings along the Web Authentication API, new autoplay policies, Service Worker updates, as well as CSS masking, background blend, and overscroll.</li>
</ul>
{{% feature-panel %}}
## General
<ul>
<li>Max Böck wrote about the <a href="https://mxb.at/blog/hurricane-web/">Hurricane Web</a> and what we can do to keep users up-to-date even when bandwidth and battery are limited. Interestingly, CNN and NPR provided text-only pages during Hurricane Florence to serve low traffic that doesn’t drain batteries. It would be amazing if we could  move the default websites towards these goals — saving power and bandwidth — to improve not only performance and load times but also help the environment and make users happier.</li>
</ul>
## UI/UX
<ul>
<li>In episode 42 of their podcast, the Nori team elaborates <a href="https://nori.com/podcast/42-the-designers-role-in-reversing-climate-change-with-michael-leggett-jacob-farny-of-nori">what designers can do to help reverse climate change</a>. The discussed content can be transferred to developers as well, so don’t be afraid to tune in despite the title.</li>
<li>Denislav Jeliazkov explains <a href="https://uxplanet.org/creating-meaningful-micro-interactions-99cbde1fbee7">the importance of micro-interactions</a> and how they can be designed well to make a difference between your and your competitor’s app.</li>
<li>Jeremy Cherry on <a href="https://medium.com/journey-group/creating-users-not-addicts-73e1774297c7">why we should create users and not addicts for our products</a> and how UX can easily affect people’s health.</li>
<li>Shawn Park shares <a href="https://uxdesign.cc/how-and-why-i-redesign-my-portfolio-every-year-bf3bba3833fc">what he learned from redesigning his website each year</a> for six years in a row and why he feels that this is an important step to improve your skills.</li>
<li>Jonas Downey wrote about <a href="https://m.signalvnoise.com/how-youre-being-manipulated-by-software-7ad939e46852">how we’re constantly manipulated by software’s ‘User Experience’ design</a> and why the only option we have is to vote against these patterns with our wallet and pay for software that doesn’t try to manipulate us in a way that affects our privacy, security, or mindset.</li>
<li><a href="https://www.behance.net/gallery/70151099/The-Best-Contemporary-Free-Fonts">The Best Contemporary Free Fonts</a> is a great collection of freely available fonts on Behance.</li>
</ul>
<figure><a href="https://uxdesign.cc/how-and-why-i-redesign-my-portfolio-every-year-bf3bba3833fc"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f3aca15-5dd0-4804-ad4a-982ab53e6aee/portfolio-redesign-opt.png" width="800" height="473" alt="Redesign portfolio website" /></a><figcaption>Shawn Parks shares the <a href="https://uxdesign.cc/how-and-why-i-redesign-my-portfolio-every-year-bf3bba3833fc">lessons he learned from redesigning his portfolio</a> every year. (<a href="https://uxdesign.cc/how-and-why-i-redesign-my-portfolio-every-year-bf3bba3833fc">Image credit</a>)</figcaption></figure>
## Accessibility
<ul>
<li>Accessibility is about more than making your website accessible for people with physical impairments. We shouldn’t forget that <a href="https://alistapart.com/article/designing-for-cognitive-differences">designing for cognitive differences</a> is essential, too, if we want to serve our sites to as many people as possible.</li>
<li>Amy Leak <a href="https://medium.com/@amyalexandraleak/should-you-use-alt-text-or-a-caption-48311e259ded">shows some great examples of how to write good text alternatives</a>.</li>
</ul>
## Tooling
<ul>
<li><a href="https://trix-editor.org/">Trix is a rich open-source text editor</a> by Basecamp. If you’re using Ruby already, this might be a great choice for any content editing field in your application.</li>
</ul>
## Privacy
<ul>
<li>Guess what? Our simple privacy-enhancing tools that delete cookies are useless <a href="https://youbroketheinternet.org/trackedanyway">as this article shows</a>. There are smarter ways to track a user via TLS session tracking, and we don’t have much power to do anything against it. So be aware that someone might be able to track you regardless of how many countermeasures you have enabled in your browser.</li>
<li>Josh Clark’s comment on university research about <a href="https://bigmedium.com/ideas/links/google-data-collection-research.html">Google’s data collection</a> is highlighting the most important parts about how important Android phone data is to Google’s business model and what type of information they collect even when your smartphone is idle and not moving location.</li>
</ul>
{{% ad-panel-leaderboard %}}
## Security
<ul>
<li>Brendan McMillion from Cloudflare shares how they <a href="https://blog.cloudflare.com/e2e-integrity/">ensure end-to-end integrity for their IPFS</a> (a distributed, decentralized web protocol) gateway. A very interesting insight into the future of the web.</li>
</ul>
<figure><a href="https://blog.cloudflare.com/e2e-integrity/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d44b5ff8-cd70-4a9e-b14c-0f4883acf9e1/ipfs-opt.png" width="800" height="492" alt="End-to-End Integrity with IPFS illustrated with cats and dogs" /></a><figcaption>Cloudflare’s <a href="https://blog.cloudflare.com/e2e-integrity/">IPFS gateway</a> allows a website to be end-to-end secure while maintaining the performance and reliability benefits of being served from their edge network. (<a href="https://blog.cloudflare.com/e2e-integrity/">Image credit</a>)</figcaption></figure>
## Web Performance
<ul>
<li>Shubham Kanodia explains how we can <a href="https://www.smashingmagazine.com/2018/10/smart-bundling-legacy-code-browsers/">serve legacy code only to legacy browsers by using smart bundling techniques</a>.</li>
<li>In his in-depth guide to debugging performance issues, Nolan Lawson shares how we can <a href="https://nolanlawson.com/2018/09/25/accurately-measuring-layout-on-the-web/">accurately measure layout performance on the web</a> and how the rendering pipeline of modern browsers works.</li>
<li>Philip Walton explains his <a href="https://philipwalton.com/articles/idle-until-urgent/"><em>Idle until urgent</em></a> principle for optimizing the load and paint performance of websites.</li>
<li>How can we build a website that’s working well and is fast on low-tech devices while using as little resources as possible? The Low-Tech Magazine wanted to find out and <a href="https://solar.lowtechmagazine.com/2018/09/how-to-build-a-lowtech-website/">built their website following a crazy approach to save resources</a>. Neat additional fun fact: The website goes offline when there’s not enough sun to power the 2.5 Watt solar panel that powers the server.</li>
<li>The new Google <a href="https://developers.google.com/web/fundamentals/performance/rail">Web Fundamentals guide to measuring performance with the RAIL model</a> is out. Very useful when you want to analyze or debug performance.</li>
</ul>
<figure><a href="https://developers.google.com/web/fundamentals/performance/rail"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f4e44ba-43af-4b57-ab9c-542988e8375a/rail-opt.png" width="800" height="289" alt="Illustration of the RAIL model" /></a><figcaption>The four parts of the <a href="https://developers.google.com/web/fundamentals/performance/rail">RAIL performance model</a>: Response, Animation, Idle, Load. (<a href="https://developers.google.com/web/fundamentals/performance/rail">Image credit</a>)</figcaption></figure>
## HTML &amp; SVG
<ul>
<li>As people can now browse the web on their Apple Watch, Marcus Herrmann shares insights into <a href="https://marcus.io/blog/websites-on-apple-watch">how we can optimize our sites for the device</a>.</li>
<li>Modal windows usually include a lot of custom JavaScript, CSS, and HTML code. Now we have the <code>&lt;dialog&gt;</code> element which brings us most functionality out of the box, including accessibility. Chris Manning wrote an <a href="https://www.viget.com/articles/the-dialog-element/">introduction to the dialog element and how we can use and polyfill it</a>.</li>
</ul>
## JavaScript
<ul>
<li>Willian Martins shares <a href="https://www.smashingmagazine.com/2018/10/taming-this-javascript-bind-operator/">the secrets of JavaScript’s <code>bind()</code></a> function, a widely unknown operator that is so powerful and allows us to invoke <code>this</code> from somewhere else into named, non-anonymous functions. A different way to write JavaScript.</li>
<li>Everyone knows what the “9am rush hour” means. Paul Lewis uses the term to <a href="https://medium.com/@aerotwist/the-9am-rush-hour-2d7ae687efd5">rethink how we build for the web</a> and why we should try to avoid traffic jams on the main thread of the browser and outsource everything that doesn’t belong to the UI into separate traffic lanes instead.</li>
</ul>
## CSS
<ul>
<li>Michelle Barker explains why <a href="https://css-irl.info/negative-grid-lines/">negative grid lines can come in very handy</a>.</li>
<li>Do you know the <a href="https://bitsofco.de/understanding-the-difference-between-grid-template-and-grid-auto/">differences between CSS Grid’s <code>grid-template</code> and <code>grid-auto</code></a>? Ire Aderinokun explains them.</li>
<li>Rachel Andrew wrote about <a href="https://www.smashingmagazine.com/2018/10/flexbox-use-cases/">the use cases for Flexbox</a> now that we have CSS Grid Layout and shares advice on when to use which.</li>
</ul>
<figure><a href="https://css-irl.info/negative-grid-lines/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cd39b1b-12bc-4bfe-81da-4b8baaee7579/negative-grid-lines-opt.png" width="800" height="401" alt="An item placed inside a grid using negative grid lines" /></a><figcaption>Did you know you can <a href="https://css-irl.info/negative-grid-lines/">use negative grid line numbers</a> to position Grid items with CSS? (<a href="https://css-irl.info/negative-grid-lines/">Image credit</a>)</figcaption></figure>
{{% ad-panel-leaderboard %}}
## Work &amp; Life
<ul>
<li>Do you have a hobby? Well, when was the last time you enjoyed it and had enough time for it? Tim Wu reflects on how  <a href="https://www.nytimes.com/2018/09/29/opinion/sunday/in-praise-of-mediocrity.html">the pursuit of excellence has infiltrated and corrupted the world of leisure</a>.</li>
<li>Here is a primer for employees on <a href="https://medium.com/@climateActTech/a-guide-for-employees-how-to-make-your-tech-company-sustainable-b0c93522620c">how to make your tech company adopt stronger sustainability practices</a> and positions.</li>
<li>We’ve all heard a lot about how David Heinemeier Hansson from Basecamp thinks differently about work, employment, and success. <a href="https://www.atrium.co/blog/dhh-competition-startups/">This interview summarizes</a> the “Basecamp way” and the challenges which are linked to it.</li>
<li>Seth Godin ponders about Apple’s and Amazon’s net ‘value’ of a trillion dollars and <a href="https://seths.blog/2018/09/profitable-difficult-or-important/">why the profit of a company doesn’t matter but the importance of its work</a>.</li>
<li>“The tech industry is growing at an exponential rate influencing society to the point that we are seeing the biggest shift, perhaps ever, in man-kind. Some tech services actually have billions of users. You read that right, not thousands, not millions, but BILLIONS of human beings using them regularly. It would be arrogant not to say that these services are forming our society and shaping our norms while their only objective was to keep the growth curve… growing.” — Anton Sten in “<a href="https://www.antonsten.com/my-responsibilities/">What about <em>my</em> responsibilities?</a>”</li>
<li>You’re working hard to finish that project in expectation that it’ll feel so good and relaxing when it’s live. Itamar Turner-Trauring shares why this way of thinking is wrong and <a href="https://codewithoutrules.com/2018/09/27/avoiding-burnout/">how we can avoid burning out</a>.</li>
<li>Leo Babauta on <a href="https://zenhabits.net/behind/">why we feel that we’re always behind on work</a> and some strategies to avoid these feelings and work happily instead.</li>
<li>Most companies (and developers as well) only praise the positive aspects of working remotely, <a href="https://blog.doist.com/mental-health-and-remote-work-1b77616f6945">only a few talk about the challenges and negative consequences</a> such as a higher risk of feeling isolated, facing anxiety or even depression.</li>
</ul>
## Going Beyond…
<ul>
<li>In the Netherlands, there’s now <a href="https://www.theguardian.com/environment/2018/oct/09/dutch-appeals-court-upholds-landmark-climate-change-ruling">a legal basis that prescribes CO2 emissions to be cut by 25% by 2020</a> (that’s just a bit more than one year from now). I love the idea and hope other countries will be inspired by it — Germany, for example, which currently moves its emission cut goals farther and farther into the future.</li>
<li>David Wolpert explains <a href="https://blogs.scientificamerican.com/observations/why-do-computers-use-so-much-energy/">why computers use so much energy</a> and how we could make them vastly more efficient. But for that to happen, we need to understand the thermodynamics of computing better.</li>
<li><a href="https://m.signalvnoise.com/you-know-whats-cool-turning-down-twenty-billion-dollars-bbdc2ea63ae5">Turning down twenty billion dollars is cool</a>. Of course, it is. But the interesting point in this article about the Whatsapp founder who just told the world how unhappy he is having sold his service to Facebook is that it seems that he believed he could keep the control over his product.</li>
</ul>
<p>One more thing: I’m very grateful for all of you who helped raise <a href="https://wdrl.info/donate">my funding level for the Web Development Reading List to 100%</a> this month. I never got so much feedback from you and so much support. Thank you! Have a great month!</p>
<p><em>—Anselm</em></p>
{{< signature "cm" >}}