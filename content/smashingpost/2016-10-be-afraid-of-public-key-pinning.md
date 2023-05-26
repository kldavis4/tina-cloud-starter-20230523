---
title: Be Afraid Of HTTP Public Key Pinning (HPKP)
slug: be-afraid-of-public-key-pinning
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73b6f04a-f7e7-4e4e-bcba-68da1e233ca7/your-connection-is-not-private.png
date: 2016-10-26T17:32:07.000Z
author: mathiasbiilmannchristensen
description: >-
  Between October 21st and 25th, Smashing Magazine became **completely
  unavailable** for a majority of visitors. Visiting Smashing Magazine would
  give most returning visitors with a modern browser a security warning message
  like this:


  Some people would get a slightly different screen because of Smashing
  Magazine's [Service Worker](https://www.smashingmagazine.com/serviceWorker.js)
  kicking in, and showing a placeholder "You're Offline" message, but the
  underlying cause was the same: **HTTP Public Key Pinning**.
categories:
  - Security
  - SSL
---

Between October 21st and 25th, Smashing Magazine became <strong>completely unavailable</strong> for a majority of visitors. Visiting Smashing Magazine would give most returning visitors with a modern browser a security warning message like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73b6f04a-f7e7-4e4e-bcba-68da1e233ca7/your-connection-is-not-private.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45169965-f3ef-4eef-b05b-56adde473d37/your-connection-is-not-private-500px-opt.png" alt="A security warning message stating that your connection is not private" width="500" height="336" /></a><figcaption>The warning message most of Smashing Magazine's visitors were seeing.</figcaption></figure>

Some other visitors would get a slightly different screen because of Smashing Magazine's <a href="https://www.smashingmagazine.com/2016/02/making-a-service-worker/">Service worker</a> kicking in, and showing a placeholder "You're Offline" message, but the underlying cause was the same: <strong>HTTP Public Key Pinning</strong>.

Smashing Magazine used to send an HTTP header with each response that looked like this:

<pre><code class="language-bash">Public-Key-Pins: 
pin-sha256="8RoC2kEF47SCVwX8Er+UBJ44pDfDZY6Ku5mm9bSXT3o=";
pin-sha256="78j8kS82YGC1jbX4Qeavl9ps+ZCzb132wCvAY7AxTMw=";
pin-sha256="GQGOWh/khWzFKzDO9wUVtRkHO7BJjPfzd0UVDhF+LxM=";
max-age=31536000; includeSubDomains
</code></pre>

Sites such as <a href="https://securityheaders.io/">securityheaders.io</a> encourage setting and at <a href="https://www.netlify.com">Netlify</a>, we often get questions from clients on how to setup public key pinning. In theory, this header can be a strong weapon against the threat of "Man in the middle attacks." These are attacks where someone would impersonate Smashing Magazine with a false certificate somehow generated via a Certificate Authority that your browser already trusts.

The key pinning header above tells browsers to refuse to accept any certificate that hasn't been signed with one of the three keys indicated in the header for one year after visiting the site. Not just for <code>www.smashingmagazine.com</code>, but also for all other subdomains.

### When Key Pinning Goes Wrong

Key pinning protects against a relatively rare attack that's very hard to pull off and that's not a major threat scenario against a content-driven website like Smashing Magazine, but it does so at the cost of potentially causing major — in the worst case even catastrophic — outages.

For Smashing Magazine this happened when they were updating their expiring SSL certificate. They created a new wildcard certificate, added the digest of the new private key to the Public-Key-Pins header and rolled out the new certificate with a header looking like this:

<pre><code class="language-bash">Public-Key-Pins: 
pin-sha256="35L+K6PY5ynTu15SYPrT8KXp5TRH8kzP46mYLpv9k30=";
pin-sha256="78j8kS82YGC1jbX4Qeavl9ps+ZCzb132wCvAY7AxTMw=";
pin-sha256="GQGOWh/khWzFKzDO9wUVtRkHO7BJjPfzd0UVDhF+LxM=";
max-age=31536000; includeSubDomains
</code></pre>

Have you spotted the problem?

The old header had told <strong>visitors</strong> to Smashing Magazine that their browser should <strong>never</strong> accept any certificate that wasn't listed in the old key pinning headers for the next 365 days. Adding the new certificate to the key pinning headers does nothing for this and the moment this went live, all previous visitors with a browser that had pinned the <em>old</em> certificate were now completely unable to visit Smashing Magazine!

Even worse, this could not simply be rolled back since the old certificate had <strong>expired</strong>!

### Moral Of The Story

Consider really carefully if key pinning is worth it for your site. If you're running a major bank or a secure site for whistleblowers, you'll no doubt want to do anything you can to avoid possible man in the middle attacks.

However, if you're running a content-driven website, it's just never worth it to use a security technique that could potentially take your whole site down close to permanently! Going offline is a much more severe threat than getting exposed to a sophisticated man-in-the-middle attack.

If you really think you need public key pinning, consider at least setting a <code>max-age</code> that's low enough that you can survive it if something goes wrong. And do hold on to those precious pinned keys as if your life depended on it. Once you pin, there's no going back if you make a mistake!

In a <a href="https://www.smashingmagazine.com/how-to-issue-a-new-ssl-certificate-with-an-old-ssl-key/">follow-up article</a>, I'll elaborate how to issue a <em>new</em> certificate that is using the keys of the <em>old</em> expired SSL certificate. Thanks for reading!

<em>(ms)</em>