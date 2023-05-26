---
title: 'Breaking It Down To The Bits: How The Internet, DNS, And HTTPS Work'
slug: breaking-it-down-to-the-bits-how-the-internet-dns-and-https-work
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8159d5b-08c4-4a17-ae48-7f7d31a46ed4/breaking-it-down-to-the-bits-opt.png
date: 2016-02-04T23:27:22.000Z
author: cosima-mielke
description: >-
  _Smashing Magazine is known for lengthy, comprehensive articles. But what about something different for a change? What about shorter, concise pieces with useful tips that you could easily read over a short coffee break? As an experiment, this is one of the shorter *Quick Tips*-kind-of articles — shorter posts prepared and edited by our editorial team.
categories:
  - DNS
  - Performance
  - Resources
  - HTTPS
  - Backend
---
<em>Smashing Magazine is known for lengthy, comprehensive articles. But what about something different for a change? What about <strong>shorter, concise pieces with useful tips and bits</strong> that you could easily read over a short coffee break? As an experiment, this is one of the shorter <strong>"Quick Tips"</strong>-kind-of articles — shorter posts prepared and edited by our editorial team. What do you think? Let us know in the comments! —Ed.</em>

The Internet is the foundation of our craft. But what do we actually <strong>know about its underlying technology</strong>? How do DNS, networks and HTTPS work? What happens in the browser when we type a URL in the address bar?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Effective Strategy For Choosing Right Domain Names](https://www.smashingmagazine.com/2009/05/the-effective-strategy-for-choosing-right-domain-names/)
*   [10 Tools For Finding, Registering And Managing Domain Names](https://www.smashingmagazine.com/2009/08/10-tools-find-register-manage-domain-names/)
*   [Get Creative With Your Domain Name](https://www.smashingmagazine.com/2009/07/get-creative-with-your-domain-names/)

As web professionals, we all should have at least a basic knowledge of the building blocks that make up the web. The following resources are a good place to start your journey into the — not-so-dark — matter of networks and protocols:

{{% feature-panel %}}

<figure class="fwi"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a8cab97-575e-42f9-a1b0-b3fd3c4863bd/how-the-internet-works-opt.png" alt="If we want to build high performance applications, we have to understand how the individual bits are delivered." /><br>
<figcaption>If we want to build high performance applications, we have to understand how the individual bits are delivered. Image credit: <a href="https://webhostinggeeks.com/guides/dns/">Web Hosting Geeks</a>.</figcaption></figure>

*   What happens behind the scenes when a user requests a website? If you always wanted to understand, but haven’t gotten around to yet, Web Hosting Geeks provides a [comprehensive overview over the DNS](https://webhostinggeeks.com/guides/dns/) (Domain Name System), the cornerstone for how we use the Internet.
*   Ilya Grigorik’s book [High Performance Browser Networking](https://chimera.labs.oreilly.com/books/1230000000545/index.html) is your gateway to the network. Its guiding principle: it’s essential to know how the individual bits are delivered in order to build high performance applications. To help developers get on track, the book dissects how the HTTP protocol works and investigates new networking capabilities in the browser — HTTP/2 improvements included. You can read the book online, for free.
*   Speaking of HTTPS, mixed content is often a problem. The HTTPS-Only Standard by U.S. Standards explains why browsers block mixed content and what you can do to [improve your migration strategy](https://https.cio.gov/mixed-content/) and detect mixed content on your site. [Mixed Content Scan](https://github.com/bramus/mixed-content-scan) can help you find issues on your site, and you can use [report-uri.io](https://report-uri.io/) to [set up an endpoint](https://scotthelme.co.uk/fixing-mixed-content-with-csp/) that would be pinged once a mixed content issues is discovered — and reported to you automatically.

As web designers and developers, we invest a lot of time in staying on top of the latest techniques. Nevertheless, we should also remember to focus on the more general aspects of the web every once in a while. Once we have a working knowledge of the technology that keeps the Internet together, we can <strong>see our design decisions in a broader context</strong>, and, thus, build better products.

{{< signature "cm, vf" >}}

