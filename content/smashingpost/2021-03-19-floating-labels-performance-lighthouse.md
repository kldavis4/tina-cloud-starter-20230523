---
title: 'Gone Floating Labels And Green Lighthouse Scores'
slug: floating-labels-performance-lighthouse
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/751299ac-ac15-488c-b771-c7d221f2d894/1-smashing-login.png
date: 2021-03-19T13:30:00.000Z
summary: >-
  Wondering what’s happenin’ at Smashing? Well, we’ve been busy. Here’s a little story of how we removed floating labels, improved performance on mobile, and launched a <a href='https://www.smashingmagazine.com/2021/03/css-generators/'>new series of articles</a>. Oh, and how you can contribute to Smashing, too.
description: >-
  Wondering what’s happenin’ at Smashing? Well, we’ve been busy. Here’s a little story of how we removed floating labels, improved performance on mobile, and launched a <a href='https://www.smashingmagazine.com/2021/03/css-generators/'>new series of articles</a>. Oh, and how you can contribute to Smashing, too.
categories:
  - Smashing
  - Performance
  - Usability
  - Case Studies
  - Core Web Vitals
disable_ads: true
disable_newsletterbox: true
---

There is always something happening behind the scenes at Smashing. Over the last months, we’ve been continuously working around [the performance of the site](https://www.smashingmagazine.com/2021/01/smashingmag-performance-case-study/), but we’ve also [removed floating labels](https://twitter.com/smashingmag/status/1367518953443106817) from our forms, redesigned our error messages, revamped our [Membership dashboard](https://www.smashingmagazine.com/membership/), refactored and adjusted our responsive tables and worked with new authors on a bunch of new articles that will be published on the site over the next months. So, here’s your monthly Smashing update.

## Floating Labels Are Gone

After we’ve published Adam Silver’s piece on why [floating labels are a bad idea](https://www.smashingmagazine.com/2021/02/material-design-text-fields/), we’ve seen a huge discussion on Twitter and in the comments about them. Surely you can save quite a bit of vertical space with them, but the cost of it has plenty of **accessibility and autofill issues**. Ironically, at the moment of publishing that article in late February, we still had floating labels used in most of our forms, and we wanted to explore if removing them would actually help us improve the overall experience on the site.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b87600-a204-403f-b87f-8a6fe2bc0a10/3-smashing-update-march2021.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b87600-a204-403f-b87f-8a6fe2bc0a10/3-smashing-update-march2021.png" width="800" height="820" sizes="100vw" caption="With floating labels, we ran into the same issues with autofill &mdash; over and over again. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b87600-a204-403f-b87f-8a6fe2bc0a10/3-smashing-update-march2021.png'>Large preview</a>)" alt="A screengrab of the sign-in page on Smashing Magazine, showing issues faced with floating labels and autofill" >}}

So we’ve **removed the floating labels** and redesigned input fields, placing the labels above the input field, just like Adam has suggested. We also used the opportunity to add some subtle adjustments to our actual forms, and we are still working on it. But the result looked better already.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e817af5-a9e4-4596-a01b-827cad2f89ab/1-smashing-update-march2021.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e817af5-a9e4-4596-a01b-827cad2f89ab/1-smashing-update-march2021.png" width="800" height="796" sizes="100vw" caption="No floating labels in use. Autofilled value looks fine, too! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e817af5-a9e4-4596-a01b-827cad2f89ab/1-smashing-update-march2021.png'>Large preview</a>)" alt="A screengrab of the same sign-page as above but with no floating labels in use" >}}

After a few days of refinements, we’ve stumbled upon styling issues with **autofill**. We wanted to adjust the font-size and the font used with autofill with the **`:-webkit-autofill` CSS** [pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) &mdash; it matches when an `<input>`  element has its value auto-filled by the browser &mdash; but it’s not supported across a range of browsers, and frankly caused quite a bit of a hassle when an auto-filled value is validated once the visitor leaves an input field.

In fact, we had to look into various cases for the form design:

- What happens when **no data is provided** at all?
- What happens when we **retrieve the data from localStorage** and plug it automatically in the input fields, but then autofill hasn’t been activated?
- What happens when **some values are auto-filled**, but others aren’t?
- What happens with **inline validation**, and when do we validate?
- What happens if some auto-filled input fields have **errors**?
- How should the input values appear on `:active` and on `:focus`?

Frankly, this turned out to be quite a rabbit hole, and we are still looking into all these issues at the moment. Given that a vast majority of our readers &mdash; wonderful people like you &mdash; are using autofill, it’s worth spending time designing an experience around it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb993f3-53dd-4806-b8ef-881e8a35f94b/2-smashing-update-march2021.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb993f3-53dd-4806-b8ef-881e8a35f94b/2-smashing-update-march2021.png" width="800" height="486" sizes="100vw" caption="Web forms redesigned, with a few subtle adjustments &mdash; and without floating labels. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb993f3-53dd-4806-b8ef-881e8a35f94b/2-smashing-update-march2021.png'>Large preview</a>)" alt="A screenshot of customer details and shopping address fill-in form created without floating labels" >}}

After a bit of refinements, around 2 weeks after the initial article by Adam was published, we **pushed the changes live**. We did manage to resolve plenty of accessibility issues and layout issues on mobile just by removing floating labels. But we can’t really say just yet whether it had any impact on the business metrics &mdash; well, we’ll need to wait for a big book release to see that.

## Green Scores in Lighthouse on Mobile

Working around improving **performance** was an ongoing journey on SmashingMag for a while. At the end of last year, we noticed that we’ve seen quite a drop in performance in 2020, so we rolled up our sleeves and got to work. By [changing the delivery of CSS and JavaScript](https://www.smashingmagazine.com/2021/01/smashingmag-performance-case-study/) we landed in the green score area for most pages on the site in desktop view; yet the performance on **mobile was still quite low**, averaging between the Lighthouse scores of 60-70 for most articles.

The final prompt for a more aggressive optimization was the **“Core Web Vitals” dashboard** in the Google Search Console. On February 19th, over 3590 articles were flagged with a poor CLS score (>0.25) &mdash; on desktop and on mobile. We first thought that it could be related to the cookie banner adjustments we made recently, but it turned out it was a Google Search Update that seemed to be more aggressively penalizing us for a high CLS.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d974619a-7970-4059-b3d2-8290a0e22efd/4-smashing-update-march2021.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d974619a-7970-4059-b3d2-8290a0e22efd/4-smashing-update-march2021.png" width="800" height="476" sizes="100vw" caption="On February 19th, most of our articles landed in the red zone. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d974619a-7970-4059-b3d2-8290a0e22efd/4-smashing-update-march2021.png'>Large preview</a>)" alt="A screenshot of a report showing poor URLs that need improvement as well as good URLs from DEc 2020 until March 2021" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b6d9100-e6b9-4ba1-a5f8-8e668e07503f/5-smashing-update-march2021.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b6d9100-e6b9-4ba1-a5f8-8e668e07503f/5-smashing-update-march2021.png" width="800" height="510" sizes="100vw" caption="Over 3590 articles &mdash; all flagged as pages with poor performance, despite all our improvements over the months. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b6d9100-e6b9-4ba1-a5f8-8e668e07503f/5-smashing-update-march2021.png'>Large preview</a>)" alt="Poor result showing 3.59K" >}}

So [we’ve turned to Twitter](https://twitter.com/smashingmag/status/1367781894327312388) to ask the community if anybody had further suggestions around what we could do. The feedback was *fantastic* from people all over the world &mdash; with some thorough reviews submitted via Twiter’s DMs, and general thoughts by people on what we could do.

[Patrick Meenan](https://twitter.com/patmeenan) has suggested to [delay the service worker install](https://twitter.com/patmeenan/status/1367849616457228294), which we implemented the same day. Apparently, the service worker was installing and activating before LCP and was causing contention.

[Gael Metais](https://twitter.com/gaelmetais) suggested to **more aggressively subset web fonts** and look into caching issues with our AVIF files. The next day we subset the fonts and pushed them live. We couldn’t fix the [AVIF](https://caniuse.com/avif) issue quickly due to the way media management is running currently, but then [Barry Pollard](https://twitter.com/tunetheweb) suggested to test if using base64-encoding for images would help.

Base64-encoding seemed like a slightly odd concept in the world of HTTP/2, but we’ve decided to build a small prototype to test whether it helps. So, did it? Oh yes, it surely did.

We were very surprised by early results. After a few iterations, we ended up serving our **LCP author profile photos** in a slightly convoluted but quite effective way:

<pre><code class="language-markup">&lt;picture&gt;
  &lt;source type="image/avif" srcset="data:image/avif;base64,AAA..."&gt;
  &lt;img src="https://.../author.jpg"
    loading="eager"
    decoding="async"
    width="200"
    height="200"
    alt=""&gt;
&lt;/picture&gt;
</code></pre>

- If a browser supports AVIF, it gets a base64-encoded string of the AVIF image (no browser request).
- If a browser doesn’t support AVIF, it gets a JPEG file (properly cached),
- The content negotiation happens via `<picture>` + `srcset` in the browser.

This would be working only for the LCP author profile photos on the homepage and on article pages. At the moment, around **35% of our mobile traffic is on iOS**, so those users wouldn’t be getting the images faster, but encoding a large JPEG image only, or encoding both AVIF and JPEG files would unnecessarily bloat HTML which we wanted to avoid.

We then adjusted our build to generate base64-strings for AVIF files automatically during the build time (if author images are available as AVIF images). That also makes it easy for us to remove it when we don’t need it any longer.

Additionally, we removed duplicates and redundancies with the [YellowLab.Tools](https://yellowlab.tools/result/fwhc79rb1p/rule/heavyFonts), refactored some CSS based on reports from [CSS auditing tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/), and adjusted our browserslist config to *reduce* optimizations for IE10 and IE11.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512cfdee-6def-4306-85c7-adf8d89757db/7-smashing-update-march2021.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512cfdee-6def-4306-85c7-adf8d89757db/7-smashing-update-march2021.png" width="800" height="616" sizes="100vw" caption="Green score on mobile, for the homepage and for the article pages. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512cfdee-6def-4306-85c7-adf8d89757db/7-smashing-update-march2021.png'>Large preview</a>)" alt="A screenshot of a PageSpeed Insights result showing a green score on mobile (for the homepage and for the article pages)" >}}

Overall we have:

- reduced the web fonts payload by 38%,
- reduced the size of critical CSS by 14%,
- reduced the size of JS files by 8%,
- (probably) increased the size of HTML by around 1%,

The impact was quite noticeable! For the first time in years, we’ve found our way to the green score zone of **90–95 on mobile**, while also making our rounds around **96–100 on desktop**. And that with a React application running in the background and plenty of scripting happening behind the scenes.

Still quite a bit of work to do, especially in the JavaScript world, but we seem to be on the right track &mdash; plus we are just about to implement [f-mods](https://docs.google.com/document/d/1PW-5ML5hOZw7GczOargelPo6_8Zkuk2DXtgfOtJ59Eo/edit) with the kind and generous help of [Simon Hearne](https://simonhearne.com/2021/layout-shifts-webfonts/).

And the best bit: all the credit goes to the incredible **community** and generous, passionate, and kind folks who have been sending us suggestions and pointers via Twitter. For that, we are very grateful &mdash; that’s the true strength and kindness of people in the community. Thank you! ❤️

## New Article Series on Smashing

We were busy not only with performance and UX optimizations though. You probably visit the site because of the articles we publish, and so we’ve been experimenting with something new.

In March, we started working on a **new series of articles** dedicated to tools and resources that can help you as a designer or developer get better at your work. You could see them as good old-fashioned round-ups, but we take time to prepare pieces with pointers that you can use every now and again *over time*.

{{< rimg breakout="true" href="https://www.smashingmagazine.com/2021/03/css-generators/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbcd32ee-03ed-477c-b28d-282866bd0dba/2-css-generators-full.png" width="800" height="357" sizes="100vw" caption="An overview of CSS generators, recently published here on SmashingMag. In action: a <a href='https://9elements.github.io/fancy-border-radius/'>border-radius organic cell</a>." alt="An example showing a border-radius organic cell" >}}

We’ve started out with tooling around CSS, but please expect more similar pieces around everything else front-end. We hope to keep you on your toes with them, so get ready! And here are the first articles we’ve published so far:

- [CSS Auditing Tools](https://www.smashingmagazine.com/2021/03/css-auditing-tools/)
- [CSS Generators](https://www.smashingmagazine.com/2021/03/css-generators/)

We've also been reaching out to [invite new authors](https://twitter.com/smashingmag/status/1372118371651756037) and smart folks like you to work on **interesting case studies** from your ongoing projects. So please [reach out to us](https://twitter.com/smashingmag/status/1372118371651756037) if you’ve been working on an interesting and challenging project recently &mdash; be it around accessibility, CSS/JS, performance, migration, refactoring or pretty much anything else. No worries if you’ve never written before &mdash; we are here to help and guide you.

Also, if you have released an **open-source tool** and would love to draw more attention to it, please let us know as well and we’d love to have you presenting your project here in the magazine as well. And, of course, if you have any feedback, please leave the comments here and let us know what you think!

## New Online Workshops on Smashing


<p><a href="https://smashingconf.com/online-workshops/"><img loading="lazy" decoding="async" style="float:right;margin-top:1em;margin-left:1.5em;margin-bottom:1em;border-radius:11px;max-width:50%" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5106a8c-a9a1-4599-8cb6-38e5c892fd60/online-workshops-spring.svg" width="200" alt="Smashing Online Workshops" /></a>Almost a year ago, we started running our very own <a href="https://smashingconf.com/online-workshops/">online workshops</a>, and each and every one has been an incredible experience to our entire team. With wonderful attendees from all over the world coming together to learn together, so many ideas have been brought to life &mdash; especially in the live design and coding sessions.</p>

<p>Here’s a brief overview of the workshops that we have planned for the <strong>next months</strong>:</p>

<table class="tablesaw break-out">
<thead>
<tr>
<th>Dates</th>
<th>Workshop</th>
<th>Speaker</th>
<th>Topic</th>
</tr>
</thead>
<tbody>
  <tr>
    <td>March 30&ndash;31</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-navigation/">Designing The Perfect Navigation</a></td>
    <td>Vitaly Friedman</td>
    <td class style="background-color: #fff2cc">UX, Design</td>
  </tr>
  <tr>
    <td>April 8&ndash;16</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/nathan-curtis-kevin-powell/">Architecting Design Systems</a></td>
    <td>Nathan Curtis &amp; Kevin Powell</td>
    <td class style="background-color: #d6f4ff">Workflow &amp; Code</td>
  </tr>
  <tr>
    <td>April 20 &ndash; May 5</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/harry-roberts-april">Web Performance</a></td>
    <td>Harry Roberts</td>
    <td class style="background-color: #d6f4ff">Workflow, Code</td>
  </tr>
  <tr>
    <td>April 22 &ndash; May 6</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-april/">Smart Interface Design Patterns</a></td>
    <td>Vitaly Friedman</td>
    <td class style="background-color: #fff2cc">UX, Design</td>
  </tr>
  <tr>
    <td>May 3&ndash;11</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-april/">Make Design Systems People Want to Use</a></td>
    <td>Dan Mall</td>
    <td class style="background-color: #d6f4ff">Workflow, Code</td>
  </tr>
  <tr>
    <td>May 6&ndash;14</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/joe-leech-may">Psychology For UX and Product Design</a></td>
    <td>Joe Leech</td>
    <td class style="background-color: #fff2cc">UX, Design</td>
  </tr>
  <tr>
    <td>May 20 &ndash; June 4</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/ivan-akulov">The React Performance</a></td>
    <td>Ivan Akulov</td>
    <td class style="background-color: #d6f4ff">Workflow, Code</td>
  </tr>
  <tr>
    <td>May 25 &ndash; June 8</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/lea-verou">Dynamic CSS</a></td>
    <td>Lea Verou</td>
    <td class style="background-color: #d6f4ff">Workflow, Code</td>
  </tr>
  <tr>
    <td>June 9&ndash;23</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-frontend-june">New Adventures In Front-End 2021</a></td>
    <td>Vitaly Friedman</td>
    <td class style="background-color: #d6f4ff">Workflow, Code</td>
  </tr>
  <tr>
    <td>July 8&ndash;22</td>
    <td><a href="https://smashingconf.com/online-workshops/workshops/stephanie-eckles">Level-Up With Modern CSS</a></td>
    <td>Stephanie Eckles</td>
    <td class style="background-color: #d6f4ff">Workflow, Code</td>
  </tr>
</tbody>
</table>

Ah, we also have <a href="https://smashingconf.com/online-workshops/bundles">workshop bundles</a> from which you can choose 3, 5 or even 10 tickets for the workshops of your choice &mdash; ongoing, upcoming or the ones happening in the future. Also, feel free to [subscribe here](https://smashingconf.com/online-workshops/#get-notified) if you’d like to be the first to be notified when new workshops come up. Plus, you get access to **early-bird tickets** as well.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bfc9761-4262-4bc9-ad1a-6ee831cd61ad/topple-virtual-conference.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bfc9761-4262-4bc9-ad1a-6ee831cd61ad/topple-virtual-conference.png" width="800" height="491" sizes="100vw" caption="Everybody is friendly and kind at <a href='https://smashingconf.com/online-workshops/'>Smashing Online Workshops</a> &mdash; no matter where we all are located in the world! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bfc9761-4262-4bc9-ad1a-6ee831cd61ad/topple-virtual-conference.png'>Large preview</a>)" alt="Topple the Smashing Mascot having a virtual event with other cool cats online" >}}

## Our Free Meet-Up:: Join Smashing Meets!

<p><a href="https://smashingconf.com/meets-actions/"><img loading="lazy" decoding="async" style="float:right;margin-top:1em;margin-left:1.5em;margin-bottom:1em;border-radius:11px;max-width:50%" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6575af88-f4c8-4301-8d4b-f394ca19b1d6/meets-actions.svg" width="200" alt="Smashing Meets On April 27, 2021" /></a>On April 27, you can <a href="https://hopin.com/events/smashing-meets-actions-speak-louder-april-27">join us live on Smashing Meets</a>, a friendly and inclusive, online meetup for people who work on the web. This “<em>Actions Speak Louder</em>” edition features three amazing sessions where our experts will design and code live &mdash; to help an amazing NGO get a better site.</p>

<p><strong>Smashing Meets is free</strong> for everybody, so please tell your friends and colleagues to join in! Of course, we’d love it if you join our community and become a member. A <a href="https://www.smashingmagazine.com/membership/">Smashing Membership starts</a> at only 3 USD a month. You get access to all digital Smashing Books, webinars and receive many freebies and friendly discounts to events, services, and products. 🎪</p>

## Smashing Podcast: Tune In And Get Inspired

Last year, we’ve published a new [Smashing Podcast](https://podcast.smashingmagazine.com/episodes) episode every two weeks, and the feedback has been *awesome*! With over 56k downloads (just over a thousand per week, and growing!), we’ve had 34 guests on the podcast with different backgrounds and <em>so</em> much to share!

If you don’t see a topic you’d like to hear and learn more about, please don’t hesitate to reach out to host [Drew McLellan](https://twitter.com/drewm) or <a href="https://twitter.com/SmashingPod">get in touch via Twitter</a> anytime &mdash; we’d love to hear from you!

<table class="break-out">
  <tbody>
    <tr>
      <td>1. <a href="https://www.smashingmagazine.com/2019/11/smashing-podcast-episode-1/">What Is Art Direction?</a></td>
      <td>2. <a href="https://www.smashingmagazine.com/2019/11/smashing-podcast-episode-2/">What’s So Great About Freelancing?</a></td>
    </tr>
    <tr>
      <td>3. <a href="https://www.smashingmagazine.com/2019/11/smashing-podcast-episode-3/">What Are Design Tokens?</a></td>
      <td>4. <a href="https://www.smashingmagazine.com/2019/12/smashing-podcast-episode-4/">What Are Inclusive Components?</a></td>
    </tr>
    <tr>
      <td>5. <a href="https://www.smashingmagazine.com/2019/12/smashing-podcast-episode-5/">What Are Variable Fonts?</a></td>
      <td>6. <a href="https://www.smashingmagazine.com/2019/12/smashing-podcast-episode-6/">What Are Micro-Frontends?</a></td>
    </tr>
    <tr>
      <td>7. <a href="https://www.smashingmagazine.com/2020/01/smashing-podcast-episode-7/">What Is A Government Design System?</a></td>
      <td>8. <a href="https://www.smashingmagazine.com/2020/01/smashing-podcast-episode-8/">What’s New In Microsoft Edge?</a></td>
    </tr>
    <tr>
      <td>9. <a href="https://www.smashingmagazine.com/2020/02/smashing-podcast-episode-9/">How Can I Work With UI Frameworks?</a></td>
      <td>10. <a href="https://www.smashingmagazine.com/2020/02/smashing-podcast-episode-10/">What Is Ethical Design?</a></td>
    </tr>
    <tr>
      <td>11. <a href="https://www.smashingmagazine.com/2020/03/smashing-podcast-episode-11/">What Is Sourcebit?</a></td>
      <td>12. <a href="https://www.smashingmagazine.com/2020/03/smashing-podcast-episode-12/">What Is Conversion Optimization?</a></td>
    </tr>
    <tr>
      <td>13. <a href="https://www.smashingmagazine.com/2020/04/smashing-podcast-episode-13/">What Is Online Privacy?</a></td>
      <td>14. <a href="https://www.smashingmagazine.com/2020/04/smashing-podcast-episode-14/">How Can I Run Online Workshops?</a></td>
    </tr>
    <tr>
      <td>15. <a href="https://www.smashingmagazine.com/2020/05/smashing-podcast-episode-15/">How Can I Build An App In 10 Days?</a></td>
      <td>16. <a href="https://www.smashingmagazine.com/2020/05/smashing-podcast-episode-16/">How Can I Optimize My Home Workspace?</a></td>
    </tr>
    <tr>
      <td>17. <a href="https://www.smashingmagazine.com/2020/06/smashing-podcast-episode-17/">What’s New In Drupal 9?</a></td>
      <td>18. <a href="https://www.smashingmagazine.com/2020/06/smashing-podcast-episode-18/">How Can I Learn React?</a></td>
    </tr>
    <tr>
      <td>19. <a href="https://www.smashingmagazine.com/2020/06/smashing-podcast-episode-19/">What Is CUBE CSS?</a></td>
      <td>20. <a href="https://www.smashingmagazine.com/2020/07/smashing-podcast-episode-20/">What Is Gatsby?</a></td>
    </tr>
    <tr>
      <td>21. <a href="https://www.smashingmagazine.com/2020/07/smashing-podcast-episode-21/">Are Modern Best Practices Bad For The Web?</a></td>
      <td>22. <a href="https://www.smashingmagazine.com/2020/08/smashing-podcast-episode-22/">What Is Serverless?</a></td>
    </tr>
    <tr>
      <td>23. <a href="https://www.smashingmagazine.com/2020/08/smashing-podcast-episode-23/">What Is Next.js?</a></td>
      <td>24. <a href="https://www.smashingmagazine.com/2020/09/smashing-podcast-episode-24/">What Is SVG Animation?</a></td>
    </tr>
    <tr>
      <td>25. <a href="https://www.smashingmagazine.com/2020/09/smashing-podcast-episode-25/">What Is RedwoodJS?</a></td>
      <td>26. <a href="https://www.smashingmagazine.com/2020/10/smashing-podcast-episode-26/">What’s New In Vue 3.0?</a></td>
    </tr>
    <tr>
      <td>27. <a href="https://www.smashingmagazine.com/2020/10/smashing-podcast-episode-27/">What Is TypeScript?</a></td>
      <td>28. <a href="https://www.smashingmagazine.com/2020/11/smashing-podcast-episode-28/">What Is Eleventy?</a></td>
    </tr>
    <tr>
      <td>29. <a href="https://www.smashingmagazine.com/2020/11/smashing-podcast-episode-29/">How Does Netlify Dogfood The Jamstack?</a></td>
      <td>30. <a href="https://www.smashingmagazine.com/2020/12/smashing-podcast-episode-30/">What Is Product Design?</a></td>
    </tr>
    <tr>
      <td>31. <a href="https://www.smashingmagazine.com/2020/12/smashing-podcast-episode-31/">What Is GraphQL?</a></td>
      <td>32. <a href="https://www.smashingmagazine.com/2020/12/smashing-podcast-episode-32/">Review Of The Year 2020</a></td>
    </tr>
    <tr>
      <td>33. <a href="https://www.smashingmagazine.com/2021/01/smashing-podcast-episode-33/">What Is Machine Learning?</a></td>
      <td>34. <a href="https://www.smashingmagazine.com/2021/01/smashing-podcast-episode-34/">What’s The State Of Web Performance?</a></td>
    </tr>
    <tr>
      <td>35. <a href="https://www.smashingmagazine.com/2021/02/smashing-podcast-episode-35/">What’s Next For HTML Controls?</a></td>
      <td class style="background-color: #FFFBD7"><em>We’ll be back with the second season on April 6!</em></td>
    </tr>
  </tbody>
</table>

## And Finally... Our Friendly Smashing Email Newsletter

With our [Smashing Newsletter](https://www.smashingmagazine.com/the-smashing-newsletter/), we aim to bring you **useful, practical tidbits** and share some of the helpful things that folks are working on in the web industry. There are *so* many talented folks out there working on brilliant projects, and we’d appreciate it if you could help spread the word and give them the credit they deserve! Also, [by subscribing](https://www.smashingmagazine.com/the-smashing-newsletter/), there are no third-party mailings or hidden advertising, and your support really helps us pay the bills. ❤️
### JavaScript, Bundlers, Frameworks

- [What’s The Right Bundling Tool?](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-292/#a1)
- [Picking The Right JavaScript Framework](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-292/#a2)
- [<code>this</code> vs. <code>that</code>](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-292/#a3)
- [JavaScript Operator Lookup](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-292/#a5)
- [Strategies For Migrating To TypeScript](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-292/#a6)
- [The JavaScript Developer’s Reading List](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-292/#a7)

### CSS Techniques and Tools

- [What Does 100% Mean?](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a1)
- [The Surprising Things That CSS Can Animate](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a2)
- [Creating Randomness With Pure CSS](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a3)
- [Building Robust And Modern One-Line Layouts](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a5)
- [Auditing CSS](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a6)
- [Advanced CSS Selectors](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a7)
- [Improving Contrast With An Overlay](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-291/#a8)

### Email Productivity and Meetings

- [Encoding Code Reviews With Feedback
Ladders](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-290/#a1)
- [Making Time For What Really Matters](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-290/#a2)
- [Making Email Better](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-290/#a3)
- [Sync Color Themes For Your Dev
Environment](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-290/#a5)
- [Collecting  Feedback From Clients](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-290/#a6)
- [How To Write A Job Ad](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-290/#a7)

### Front-End Accessibility

- [Accessible Modals](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a1)
- [Accessible Tabs](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a2)
- [Implementing App-Wide Keyboard Navigation](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a3)
- [Find And Fix Accessibility Issues](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a5)
- [Support User Preferences With <code>prefers-reduced-&#42;</code>](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a6)
- [Accessible Autocomplete](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a7)
- [Making Icon Links Accessible](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/#a8)

## That’s A Wrap!

Phew, thanks for reading all the way till the end! We are a small team with just over 15 passionate and dedicated people scattered all over the world, and we do our best to help you and our wonderful community get better at our work. So **thanks for sticking around** for so long!

Frankly, we can’t wait to see you online and in person, but one thing is for certain: we *sincerely* appreciate you being smashing month after month, and for that, we are eternally grateful. And of course, we’ll keep you updated about our updates &mdash; for sure! ;-) (But you can always [subscribe to our newsletter](https://www.smashingmagazine.com/the-smashing-newsletter/), too!)

*Stay smashing, everyone!*

{{< signature "cm, il" >}}
