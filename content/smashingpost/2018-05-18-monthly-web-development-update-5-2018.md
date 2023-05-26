---
title: 'Monthly Web Development Update 5/2018: Browser Performance, Iteration Zero, And Web Authentication'
slug: monthly-web-development-update-5-2018
author: anselm-hannemann
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b118420-4523-43de-ada3-3e4d74c02287/page-previews-opt.png
date: 2018-05-18T13:51:17+02:00
summary: >-
  What has happened in the web community in the past four weeks? Anselm Hannemann summarized everything that’s new and important in one handy reading list.
description: >-
  What has happened in the web community in the past four weeks? Anselm Hannemann summarized everything that’s new and important in one handy reading list.
categories:
  - Web Development Reading List
---
<p>As developers, we often talk about performance and request browsers to render things faster. But when they finally do, we demand even more performance.</p>
<p>Alex Russel from the Chrome team now shared <a href="https://twitter.com/slightlylate/status/996195317493129216">some thoughts on developers abusing browser performance</a> and explains <strong>why websites are still slow even though browsers reinvented themselves</strong> with incredibly fast rendering engines. This is in line with <a href="https://alistapart.com/article/the-slow-death-of-internet-explorer-and-future-of-progressive-enhancement">an article by Oliver Williams</a> in which he states that we’re focusing on the wrong things, and instead of delivering the fastest solutions for slower machines and browsers, we’re serving even bigger bundles with polyfills and transpiled code to every browser.</p>
<p>It certainly isn’t easy to break out of this pattern and keep bundle size to a minimum in the interest of the user, but we have the technologies to achieve that. So <strong>let’s explore non-traditional ways</strong> and think about the actual user experience more often — <em>before</em> defining a project workflow instead of afterward.</p>

<div class="c-felix-the-cat"><h4>Front-End Performance Checklist 2021</h4><p>To help you cater for fast and smooth experiences, Vitaly Friedman summarized everything you need to know to optimize your site’s performance in one handy checklist.</p>
<p><a href="https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/" class="btn btn--small btn--green">Jump to a related article&nbsp;↬</a></p></div>

{{% feature-panel %}}

## News
<ul>
<li><a href="https://developer.mozilla.org/en-US/Firefox/Releases/60">Firefox 60 is out</a> and brings ECMAScript Modules, as well as the Web Authentication API.</li>
<li><a href="https://developers.google.com/web/updates/2018/04/nic66">Chrome 66 is now stable</a>, introducing some important updates regarding audio. After a <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=835767">bug caused by the newly-introduced user protection against background-autoplay</a> was revealed that caused severe issues with WebRTC clients, <a href="https://twitter.com/DasSurma/status/996521366156464133">Chrome has announced to revert the autoblocking, though, and delay it until Chrome 70</a> (coming in fall), so that developers have more time to adapt their codebase.</li>
<li>With Chrome 66 already released and the newest Firefox version coming up next, two major browsers are now distrusting all Symantec certificates that were issued before June 2016 — and trust me when I’m saying there are a lot of sites that still haven’t changed their affected certificates and, thus, will be out of reach for users now (Chrome) or very soon (Firefox).</li>
<li><a href="https://blog.github.com/2018-05-01-github-pages-custom-domains-https/">Github Pages now offers HTTPS support for custom domains</a>. Previously, HTTPS was only available for <code>*.github.io</code> subdomains or via third-party providers such as Cloudflare.</li>
<li>Chrome 67 is coming up soon and will <a href="https://developers.google.com/web/updates/2018/04/chrome-67-deps-rems">deprecate a few things before removing support entirely two versions later</a>, among them HTTP-Based Public Key Pinning (HPKP) and AppCache on non-secure contexts.</li>
<li>The <a href="https://blogs.windows.com/msedgedev/2018/04/30/edgehtml-17-april-2018-update/">Windows 10 April update brought EdgeHTML 17</a> with mute tabs, autofill forms, a new “print website” mode to save resources, Service Workers and Push Notifications. Variable Fonts, Screen Capture in RTC via the Media Capture API, Subresource Integrity (SRI), and support for the <code>Upgrade-Insecure-Requests</code> header have also been added. Quite a step forward!</li>
<li><a href="https://medium.com/npm-inc/announcing-npm-6-5d0b1799a905">npm version 6 is here</a> with some important security improvements. From now on, you not only have a new <code>npm audit</code> command to audit your depenencies for vulnerabilities, but npm will do this automatically and report back during dependency installs. The new version also comes with <code>npm ci</code> to make CI tasks faster and a couple of other improvements.</li>
<li><a href="https://nodejs.org/en/blog/release/v10.0.0/">Node 10 is out</a> with generators and async function support, full support for N-API and support for the Inspector protocol. It will become the next long-term support version in October.</li>
<li>Microsoft’s coding best practices tool <a href="https://medium.com/sonarwhal/sonarwhal-is-v1-4262a2f887c9">sonarwhal is now available in the first stable version</a>.</li>
</ul>

## General
<ul>
<li>Oliver Williams wrote about how important it is that we  <a href="https://alistapart.com/article/the-slow-death-of-internet-explorer-and-future-of-progressive-enhancement">rethink how we’re building websites and implement “progressive enhancement”</a> to make the web work great for everyone. After all, it’s us who make the experience worse for our users when blindly transpiling all our ECMAScript code or serving tons of JavaScript polyfills to those who already use slow machines and old software.</li>
<li><a href="https://twitter.com/philhawksworth/status/990890920672456707">Ian Feather reveals that around 1% of all requests for JavaScript on BuzzFeed time out</a>. That’s about 13 million requests per month. A good reminder of how important it is to provide a solid fallback, progressive enhancement, and workarounds.</li>
<li>The new GDPR (General Data Protection Regulation) directive is coming very soon, and while our inboxes are full of privacy policy updates, one thing that’s still very unclear is which services can already provide so-called DPAs (Data Processing Agreements). Joschi Kuphal <a href="https://tollwerk.github.io/data-processing-agreements/">collects services that offer a DPA</a>, so that we can easily look them up and see how we can obtain a copy in order to continue using their services. You can help by contributing to this resource <a href="https://github.com/tollwerk/data-processing-agreements">via Pull Requests</a>.</li>
</ul>
## UI/UX
<ul>
<li>Jared M. Spool summarized <a href="https://medium.com/@jmspool/users-dont-hate-change-they-hate-our-design-choices-86151866eff4">why users sometimes hate the design choices we make</a> but not change or redesigns overall.</li>
<li>Big news comes from Adobe regarding their Xd prototyping product: From now on, <a href="https://theblog.adobe.com/may-2018-update-adobe-xd/">the software will be free for anyone with the new Starter Plan</a>. The only differences to paid plans are limited storage, only one shared prototype (but as many non-shared as you want), and only the free Typekit library. The Xd team also improved the Sketch and Photoshop integrations, and you can now swap symbols, paste to multiple artboards, and protect design specs with a password, too.</li>
<li>Mei Zhang teaches us <a href="https://blog.prototypr.io/product-design-principles-in-a-single-card-2f6023419a87">better product design principles</a> with one single product card.</li>
</ul>
<figure><a href="https://blog.prototypr.io/product-design-principles-in-a-single-card-2f6023419a87"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98c70925-74ef-47b1-a0d5-8f070a4f784c/product-design-principles-opt.png" width="800" height="577" alt="Product design principles" /></a><figcaption>How to create a consistent, harmonious user experience when designing product cards? Mei Zhang <a href="https://blog.prototypr.io/product-design-principles-in-a-single-card-2f6023419a87">shares some valuable tips</a>. (<a href="https://blog.prototypr.io/product-design-principles-in-a-single-card-2f6023419a87">Image credit</a>)</figcaption></figure>
## Security
<ul>
<li>This month, a <a href="https://doublepulsar.com/hijack-of-amazons-internet-domain-service-used-to-reroute-web-traffic-for-two-hours-unnoticed-3a6f0dda6a6f">hijack of parts of Amazon’s Route 53 DNS service</a> allowed the attackers to control and potentially intercept the traffic of the customers who use the service. This once again <a href="https://blog.cloudflare.com/bgp-leaks-and-crypto-currencies/">shows how vulnerable the vital part of the Internet, the DNS, is</a>.</li>
<li>The latest Firefox version comes with <a href="https://www.engadget.com/2018/05/09/mozilla-firefox-passwords-web-authentication-support/">Web Authentication API support</a> — a big step towards eliminating passwords. The API lets you log in via a hardware key like YubiKey if the browser and the web service both support the new technology. Notably, Chrome 67 beta is shipping the API as well already. Their team has written a <a href="https://developers.google.com/web/updates/2018/05/webauthn">technical implementation guide</a>.</li>
<li>Starting from Firefox 60, we will be able to specify the <a href="https://tools.ietf.org/html/draft-ietf-httpbis-rfc6265bis-02#section-5.3.7"><code>same-site</code> attribute</a> for Cookies. This will allow a web application to advise the browser that cookies should only be sent if the request originates from the website the cookie came from. Read more details <a href="https://blog.mozilla.org/security/2018/04/24/same-site-cookies-in-firefox-60/">in the announcement blog post</a>.</li>
</ul>
## Privacy
<ul>
<li>The <a href="https://gdprchecklist.io/">GDPR Checklist</a> is another helpful resource for people to check whether a website is compliant with the upcoming EU directive.</li>
<li>Bloomberg published a story about the <a href="https://www.bloomberg.com/news/features/2018-05-10/inside-the-brotherhood-of-pi-hole-ad-blockers">open-source privacy-protection project pi-hole</a>, why it exists and what it wants to achieve. I use the software daily to keep my entire home and work network tracking-free.</li>
</ul>
<figure><a href="https://gdprchecklist.io/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b8057f0-4d2e-4b7e-adc4-6d1a1f43c003/gdpr-checklist-opt.png" width="800" height="463" alt="GDPR Compliance Checklist" /></a><figcaption>Achieving GDPR Compliance shouldn’t be a struggle. The <a href="https://gdprchecklist.io/">GDPR Compliance Checklist</a> helps you see clearer. (<a href="https://github.com/privacyradius/gdpr-checklist">Image credit</a>)</figcaption></figure>

## Web Performance
<ul>
<li>Postgres 10 has been here for quite a while already, but I personally struggled to find good information on how to use all these amazing features it brings along. Gabriel Enslein now shares <a href="https://speakerdeck.com/genslein/postgres-10-performance-and-you">Postgres 10 performance updates</a> in a slide deck, shedding light on how to use the built-in JSON support, native partitioning for large datasets, hash index resiliency, and more.</li>
<li>Andrew Betts found out that a lot of websites are using outdated headers. He now shares <a href="https://www.fastly.com/blog/headers-we-dont-want">why we should drop old headers and which ones to serve instead</a>.</li>
</ul>
## Accessibility
<ul>
<li>Marcy Sutton shares how Wikipedia built their <a href="https://a11ywins.tumblr.com/post/173072286008/wikipedia-link-preview">new link preview feature in an accessible way</a> so that people can easily use the keyboard as well as a mouse to trigger the overlay. You can also read more on <a href="https://medium.com/freely-sharing-the-sum-of-all-knowledge/how-we-designed-page-previews-for-wikipedia-and-what-could-be-done-with-them-in-the-future-7a5fa6b07b96">how this feature was built</a> in this post by Wikipedia designer Nirzar Pangarkar.</li>
<li>Scott O'Hara explains the <a href="https://www.scottohara.me/blog/2018/05/05/hidden-vs-none.html">differences between <code>hidden</code> and <code>none</code> keywords in ARIA</a> and when we should use which.</li>
</ul>
<figure><a href="https://medium.com/freely-sharing-the-sum-of-all-knowledge/how-we-designed-page-previews-for-wikipedia-and-what-could-be-done-with-them-in-the-future-7a5fa6b07b96"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b118420-4523-43de-ada3-3e4d74c02287/page-previews-opt.png" width="800" height="572" alt="Page previews" /></a><figcaption>Page previews open possibilities in multiple areas, as <a href="https://medium.com/freely-sharing-the-sum-of-all-knowledge/how-we-designed-page-previews-for-wikipedia-and-what-could-be-done-with-them-in-the-future-7a5fa6b07b96">Nirzar Pangarkar explains</a>. (Image credit: <a href="https://medium.com/freely-sharing-the-sum-of-all-knowledge/how-we-designed-page-previews-for-wikipedia-and-what-could-be-done-with-them-in-the-future-7a5fa6b07b96">Nirzar Pangarkar</a>)</figcaption></figure>
## CSS
<ul>
<li>Rarely talked about for years, CSS tables are still used on most websites to show (and that’s totally the correct way to do so) data in tables. But as they’re not responsive by default, we always struggled when making them responsive and most of us used JavaScript to make them work on mobile screens. Lea Verou now found <a href="https://lea.verou.me/2018/05/responsive-tables-revisited/">two new ways to achieve responsive tables by using CSS</a>: One is to use <code>text-shadow</code> to copy text to other rows, the other one uses <code>element()</code> to copy the entire <code>&lt;thead&gt;</code> to other rows — I still try to understand how Lea found these solutions, but this is amazing!</li>
<li>Rachel Andrew wrote an article about <a href="https://www.smashingmagazine.com/2018/05/print-stylesheets-in-2018/">building and providing print stylesheets in 2018</a> and why they matter a lot for users even if they don’t own a printer anymore.</li>
<li>Osvaldas Valutis shares how to <a href="https://css-tricks.com/container-adapting-tabs-with-more-button/">implement the so-called “Priority Plus” navigation pattern mostly with CSS</a>, at least in modern browsers. If you need to support older browsers, you will need to extend this solution further, but it’s a great start to implement such a pattern without too much JavaScript.</li>
<li>Rachel Andrew shares <a href="https://www.rachelandrew.co.uk/archives/2018/04/27/grid-level-2-and-subgrid/">what’s coming up in the CSS Grid Level 2 and Subgrid specifications</a> and explains what it is, what it can solve, and how to use it once it is available in browsers.</li>
</ul>
## JavaScript
<ul>
<li>Chris Ashton “<a href="https://www.smashingmagazine.com/2018/05/using-the-web-with-javascript-turned-off/">used the web for a day with JavaScript turned off</a>.” This piece highlights the importance of thinking about possible JavaScript failures on websites and why it matters if you provide fallbacks or not.</li>
<li>Sam Thorogood shares how we can build a “<a href="https://dev.to/samthor/-native-undo--redo-for-the-web-3fl3">native undo &amp; redo for the web</a>”, as used in many text editors, games, planning or graphical software and other occasions such as a drag and drop reordering. And while it’s not easy to build, the article explains the concepts and technical aspects to help us understand this complicated matter.</li>
<li>There’s a new way to implement element/container queries into your application: <a href="https://github.com/stowball/eqio">eqio</a> is a tiny library using IntersectionObserver.</li>
</ul>
## Work &amp; Life
<ul>
<li>Johannes Seitz shares his thoughts about <a href="https://printhelloworld.de/posts/iteration-zero-architecture/">project management at the start of projects</a>. He calls the method “Iteration Zero”. An interesting concept to understand the scope and risks of a project better at a time when you still don’t have enough experience with the project itself but need to build a roadmap to get things started.</li>
<li>Arestia Rosenberg shares why her <a href="https://medium.com/@Arestia/my-1-piece-of-advice-to-freelancers-lean-into-the-moment-ed7e4195fa05">number one advice for freelancers is to ‘lean into the moment’</a>. It’s about doing work when you can and using your chance to do something else when you don’t feel you can work productively. In the end, the summary results in a happy life and more productivity. I’d personally extend this to all people who can do that, but, of course, it’s best applicable to freelancers indeed.</li>
<li><a href="https://blog.samaltman.com/productivity">Sam Altman shares a couple of handy productivity tips</a> that are not just a ‘ten things to do’ list but actually really helpful thoughts about how to think about being productive.</li>
</ul>
## Going Beyond&hellip;
<ul>
<li>Ethan Marcotte elaborates <a href="https://ethanmarcotte.com/wrote/kumiho/">on the ethical issues with Google Duplex</a> that is designed to imitate human voice so well that people don’t notice if it’s a machine or a human being. While this sounds quite interesting from a technical point of view, it will push the debate about fake news much further and cause more struggle to differentiate between something a human said or a machine imitated.</li>
<li><a href="https://thestoryoftelling.com/world-built-promises/">Our world is actually built on promises</a>, and here’s why it’s so important to stick to your promises even if it’s hard sometimes.</li>
<li>I bet that most of you haven’t heard of Palantir yet. The company is funded by Peter Thiel and is a data-mining company that has the intention to <a href="https://www.bloomberg.com/features/2018-palantir-peter-thiel/">collect as much data as possible about everybody in the world</a>. It’s known to collaborate with various law enforcement authorities and even has connections to military services. What they do with data and which data they have from us isn’t known. My only hope right now is that this company will suffer a lot from the EU GDPR directive and that the European Union will try to stop their uncontrolled data collection. Facebook’s data practices are nothing compared to Palantir it seems.</li>
<li>Researchers sound the alarm after an analysis showed that <a href="https://www.fastcodesign.com/90165365/smartphones-are-wrecking-the-planet-faster-than-anyone-expected">buying a new smartphone consumes as much energy as using an existing phone for an entire decade</a>. I guess I’ll not replace my iPhone 7 anytime soon — it’s still an absolutely great device and just enough for what I do with it.</li>
<li>Anton Sten shares his thoughts on <a href="https://www.antonsten.com/vanitymetrics/">Vanity Metrics</a>, a common way to share numbers and statistics out of context. And since he realized what relevancy they have, he thinks differently about most of the commonly readable data such as investments or usage data of services now. Reading one number without having a context to compare it to doesn’t matter at all. We should keep that in mind.</li>
</ul>

<p>We hope you enjoyed this Web Development Update. The next one is scheduled for Friday, June 15th. Stay tuned.</p>

{{< signature "cm" >}}

