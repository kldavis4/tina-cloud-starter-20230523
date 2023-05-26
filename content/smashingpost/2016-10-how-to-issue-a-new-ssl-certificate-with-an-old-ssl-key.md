---
title: How To Issue A New SSL Certificate With An Old SSL Key
slug: how-to-issue-a-new-ssl-certificate-with-an-old-ssl-key
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2b32f04-dd8f-4586-bb9a-071118c19c27/dev-tools-cert-expired-opt.png
date: 2016-10-27T18:00:16.000Z
author: mathiasbiilmannchristensen
description: >-
  There was obviously a lot of confusion about how [HTTP Public Key
  Pinning](https://www.smashingmagazine.com/be-afraid-of-public-key-pinning/)
  (HPKP) worked. In the middle of the incredibly hectic process of running a
  major conference, it's the last kind of issue anybody wants to have to deal
  with. In today's article, I'd like to explain how to issue a new certificate
  that uses the keys of the **old expired SSL certificate**.
categories:
  - Security
  - SSL
---

There was obviously a lot of confusion about how <a href="https://www.smashingmagazine.com/be-afraid-of-public-key-pinning/">HTTP Public Key Pinning</a> (HPKP) worked. In the middle of the incredibly hectic process of running a major conference, it's the last kind of issue anybody wants to have to deal with. In today's article, I'd like to explain how to issue a new certificate that uses the keys of the <strong>old expired SSL certificate</strong>.

### Getting Back To Normal

The truth is that there was no surefire way out of this without some users still seeing issues, but here are the steps I helped Smashing Magazine to take to get back to a normal situation.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/ "Read 'Getting Ready For HTTP/2: A Guide For Web Designers And Developers'")
*   [World Wide Web, Not Wealthy Western Web](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/ "Read 'World Wide Web, Not Wealthy Western Web (Part 1)'")
*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/ "Read 'HTTPS Everywhere With Nginx, Varnish And Apache'")
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/ "Read 'A Look At The Modern WordPress Server Stack'")

#### 1. Procure the original private key for the expired certificate

At first, their web host claimed that the copy they had required a password that they were not aware of. Fortunately, you don't just use the key when generating the certificate. The web server doing the TLS termination also needs a copy of the private key, and on servers the private key is rarely password protected since this requires manually typing the password every time the server is restarted for any reason.

We got the web host to find the old key on the web server and with that key in hand we were ready for the next step.

#### 2. Add the old key to the new public key pinning headers

Running this OpenSSL command generates the Base64 encoded digest of the key that will tell browsers to pin it:

<pre><code class="language-markup">
openssl rsa -in my-key-file.key -outform der -pubout | openssl dgst -sha256 -binary | openssl enc -base64
</code></pre>

With this digest in hand, I told Smashing Magazine to update their headers to:

<pre><code class="language-bash">
Public-Key-Pins: 
pin-sha256="35L+K6PY5ynTu15SYPrT8KXp5TRH8kzP46mYLpv9k30="; 
pin-sha256="8RoC2kEF47SCVwX8Er+UBJ44pDfDZY6Ku5mm9bSXT3o="; 
pin-sha256="78j8kS82YGC1jbX4Qeavl9ps+ZCzb132wCvAY7AxTMw="; 
pin-sha256="GQGOWh/khWzFKzDO9wUVtRkHO7BJjPfzd0UVDhF+LxM="; 
max-age=86400; includeSubDomains
</code></pre>

Two changes here — I brought the <code>max-age</code> down to one day instead of a full year. Having a <code>max-age</code> of a year for public key pinning means that losing the private keys used to generate the certificates can permanently shut down your site completely for a year. Bad idea!

The other change was to include the digest for the old certificate. We needed to do this because a group of visitors that had visited the site after the new certificate went live, but didn't have the old certificate pinned, would now get the same SSL errors if Smashing simply switched certificates again. So we pushed this out and gave them a few hours to make a second visit and get the old digest as well.

#### 3. Generate a new certificate from the old key

The penultimate step was to generate a new certificate from the old key. To generate an SSL certificate you first need a "Certificate Request." You'll never want to share your private key with the certificate provider. Instead, you use it to sign a certificate request like this:

<pre><code class="language-bash">
openssl req -new -sha256 -key my-key-file.key -out my-certificate-request.csr
</code></pre>

During the certificate request generation, you'll be asked about various questions. The most important is the "Common Name" of the certificate which determines what domain it will be valid for.

Once you have a CSR, you can use it to order a certificate from any provider.

#### 4. Change the certificate

Armed with the new certificate signed with the old key, we could finally put a certificate live that would work again for the vast majority of visitors. Some unlucky souls may have visited while the new certificate with the new key pinning header was live, without coming back while both key pining headers were in place. These will simply be unable to access Smashing Magazine until they clear their key pinning cache or use another browser.

After losing out on thousands of visitors, Smashing Magazine was back online and the people behind it could go back to focusing on a fantastic <a href="https://smashingconf.com/">conference</a> in Barcelona.

<em>(vf, ms, il)</em>