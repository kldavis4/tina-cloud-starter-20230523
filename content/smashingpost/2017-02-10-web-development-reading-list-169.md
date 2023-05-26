---
title: >-
  Web Development Reading List #169: TLS At Scale, Brotli Benefits, And Easy
  Onion Deployments
slug: web-development-reading-list-169
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84dc894e-04aa-4e4c-bdc9-320369dd920d/wdrl-169-opt.png'
date: 2017-02-10T19:26:25.000Z
author: anselm-hannemann
description: >-
  **Everyone here can have a big impact on a project**, on someone else. I get
  very excited about this when I read stories like the one about an intern at
  Google who did an experiment that saves tons of traffic, or when I get an
  email from one of my readers who now published an awesome complete beginner’s
  guide to front-end development.

  We need to recognize that our industry depends on people who share their
  open-source code and we should support them and their projects that we heavily
  rely on. Finally, we also need to understand that these people perhaps don’t
  want a job as an employee at some big company but remain independent instead.
  So if you make money with a project that uses open-source libraries or other
  resources, maybe Valentine’s Day might be an occasion to show your
  appreciation and make the author a nice present.
categories:
  - Web Development Reading List
---
We need to recognize that our industry depends on people who share their open-source code and [we should support them and their projects](https://twitter.com/substack/status/829802572508639232) that [we heavily rely on](https://twitter.com/jashkenas/status/829817619410780160). Finally, we also need to understand that these people perhaps don’t want a job as an employee at some big company but remain independent instead. So if you make money with a project that uses open-source libraries or other resources, maybe Valentine’s Day might be an occasion to show your appreciation and make the author a nice present.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Next Generation Server Compression With Brotli](https://www.smashingmagazine.com/2016/10/next-generation-server-compression-with-brotli/)
*   [Why You Should Stop Installing Your WebDev Environment Locally](https://www.smashingmagazine.com/2016/04/stop-installing-your-webdev-environment-locally-with-docker/)
*   [Getting Ready For HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)

## General

*   So here’s something that helps beginners to start with web development and advanced devs to recap some of their knowledge: Oliver James wrote “[HTML & CSS Is Hard (But It Doesn’t Have To Be)](https://internetingishard.com/html-and-css/)”, a friendly web development tutorial for complete beginners.

{{% feature-panel %}}

<figure><a href="https://internetingishard.com/html-and-css/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046b8287-6908-45e5-b820-bef727d4d5ff/html-and-css-is-hard-opt.png" width="800" height="551" alt="HTML And CSS Is Hard, But It Doesn’t Have To Be" /></a><figcaption>Oliver James’ <a href="https://internetingishard.com/html-and-css/">complete guide to web development</a> covers everything from the absolute basics to Flexbox and responsive images. (<a href="https://internetingishard.com/html-and-css/">Image credit</a>)</figcaption></figure>

## Tools & Workflows

*   With the [Enterprise Onion Toolkit](https://github.com/alecmuffett/eotk), you can finally deploy HTTP and HTTPS onion sites at scale. While the project is still in its early days, the tool makes it easy to provide access to your web service via a hidden Tor service, which in some countries can be essential for journalists and activists.
*   [Rembrandt.js](https://rembrandtjs.com/) is an image comparison tool based on node-canvas running on a server or in the client. Great for visual regression testing, for example.</p>

## Security

*   Two engineers at Etsy recently shared [how they offer their merchants TLS-certificates for their custom domains on the Etsy-platform](https://codeascraft.com/2017/01/31/how-etsy-manages-https-and-ssl-certificates-for-custom-domains-on-pattern/). The tricky part here is scale: How to store the massive amount of certificates in a secure way? How to negotiate the connection?
*   The latest Docker release offers a great solution to store your secrets securely in containers. The [Docker Secrets Management](https://blog.docker.com/2017/02/docker-secrets-management/) is a solid approach to do so.

<figure><a href="https://codeascraft.com/2017/01/31/how-etsy-manages-https-and-ssl-certificates-for-custom-domains-on-pattern/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dc666b9-59b4-4047-8f2f-0c4d90886478/how-etsy-manages-certificates-opt.png" width="800" height="503" alt="How Etsy Manages HTTPS AND SSL Certificates For Custom Domains" /></a><figcaption>Two Etsy devs share <a href="https://codeascraft.com/2017/01/31/how-etsy-manages-https-and-ssl-certificates-for-custom-domains-on-pattern/">how they manage HTTPS and SSL certificates</a> for custom domains on Etsy. (<a href="https://codeascraft.com/2017/01/31/how-etsy-manages-https-and-ssl-certificates-for-custom-domains-on-pattern/">Image credit</a>)</figcaption></figure>

## Privacy

*   Facebook collects data about you in hundreds of ways, across numerous channels. It’s very hard to opt out, but reading [this article by Vicki Boykis](https://veekaybee.github.io/facebook-is-collecting-this/) on what they collect, you’ll learn to better understand the risks of the platform so you can choose to be more restrictive with your Facebook usage.</p>

## Web Performance

*   During her internship at Google last year, Anamaria Cotîrlea integrated Brotli into the Google Play app store, [saving Google 1.5 petabytes of traffic each day](https://students.googleblog.com/2017/02/intern-impact-brotli-compression-for.html?m=1).</p>

## Going Beyond…

*   In only 1 1⁄2 months a gigantic crack developed in the Antarctic ice shelf, and [it’s likely to break apart in the next few months](https://www.nytimes.com/interactive/2017/02/07/science/earth/antarctic-crack.html?smid=pl-share), setting free about 2,300 square miles of ice into the sea. But the key is not this tiny piece of ice but the much bigger ice shelves that’ll follow. A video captured by the NASA back in November [shows the crack in detail](https://www.nasa.gov/feature/goddard/2016/nasa-nears-finish-line-of-annual-study-of-changing-antarctic-ice).
*   If you haven’t read “Nineteen Eighty-Four (1984)” by George Orwell yet, here’s your chance: The entire book is available for free as [PDF](https://ia600201.us.archive.org/8/items/NINETEENEIGHTY-FOUR1984ByGeorgeOrwellPDFAudioBook/1984.pdf) and [Audio](https://archive.org/details/NINETEENEIGHTY-FOUR1984ByGeorgeOrwellPDFAudioBook/1984-01.mp3) versions. I personally recommend it to everyone who is only slightly interested in one of these topics: social change, politics, technology.

_And with that, I’ll close for this week. If you like what I write each week, please [support me with a donation](https://wdrl.info/donate) or share this resource with other people. You can learn more [about the costs of the project here](https://wdrl.info/costs/). It’s available via email, RSS and online._

_— Anselm_

