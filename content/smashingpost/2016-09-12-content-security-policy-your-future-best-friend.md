---
title: 'Content Security Policy, Your Future Best Friend'
slug: content-security-policy-your-future-best-friend
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d730469-4ea6-407c-8d89-55e633e4a2c0/csp-smashing3-300x250.jpg
date: 2016-09-12T19:19:14.000Z
author: nicolashoffmann
summary: >-
  The benefits of using a “content security policy” are many. Most importantly, it will stop your users from suffering any unsolicited scripts or content or XSS vulnerabilities on your website. In this article, Nicolas Hoffmann will introduce you to this technology, and he’ll explain why <strong>awareness</strong> is the most important advantage of CSP for website maintainers.
description: >-
   The benefits of using a “content security policy” are many. In this article, Nicolas Hoffmann will introduce you to this technology, and he’ll explain why <strong>awareness</strong> is the most important advantage of CSP for website maintainers.
categories:
  - Coding
  - Tools
  - Security
---
A long time ago, my personal website was attacked. I do not know how it happened, but it happened. Fortunately, the damage from the attack was quite minor: A piece of JavaScript was inserted at the bottom of some pages. I updated the FTP and other credentials, cleaned up some files, and that was that.

One point made me mad: At the time, there was no simple solution that could have informed me there was a problem and — more importantly — that could have protected the website’s visitors from this annoying piece of code.

A solution exists now, and it is a technology that succeeds in both roles. Its name is content security policy (CSP).

## <a id="What_is_CSP_8"></a>What Is A CSP?

The idea is quite simple: By sending a CSP header from a website, you are telling the browser what it is authorized to execute and what it is authorized to block.

Here is an example with PHP:

<pre><code class="language-php"><br>
<span class="hljs-preprocessor">&lt;?php</span>
    header(<span class="hljs-string">"Content-Security-Policy: &lt;your directives&gt;"</span>);
<span class="hljs-preprocessor">?&gt;</span>
</code></pre>

### <span class="rh">Further Reading</span> on SmashingMag:

- [10 Ways To Beef Up Your Website’s Security](https://www.smashingmagazine.com/2010/06/10-ways-to-beef-up-your-websites-security/)
- [Common Security Mistakes in Web Applications](https://www.smashingmagazine.com/2010/10/common-security-mistakes-in-web-applications/)
- [Web Security: Are You Part Of The Problem?](https://www.smashingmagazine.com/2010/01/web-security-primer-are-you-part-of-the-problem/)

{{% feature-panel %}}

### <a id="Some_directives_20"></a>Some Directives

You may define global rules or define rules related to a type of asset:

<pre><code class="language-php">
default-src 'self' ;
     # self = same port, same domain name, same protocol =&gt; OK
</code></pre>

The base argument is <code>default-src</code>: If no directive is defined for a type of asset, then the browser will use this value.

<pre><code class="language-php">
script-src 'self' www.google-analytics.com ;
     # JS files on these domains =&gt; OK
</code></pre>

In this example, we’ve authorized the domain name <code>www.google-analytics.com</code> as a source of JavaScript files to use on our website. We’ve added the keyword <code>'self'</code>; if we redefined the directive <code>script-src</code> with another rule, it would override <code>default-src</code> rules.

If no scheme or port is specified, then it enforces the same scheme or port from the current page. This prevents mixed content. If the page is <code>https://example.com</code>, then you wouldn’t be able to load <code>https://www.google-analytics.com/file.js</code> because it would be blocked (the scheme wouldn’t match). However, there is an exception to allow a scheme upgrade. If <code>https://example.com</code> tries to load <code>https://www.google-analytics.com/file.js</code>, then the scheme or port would be allowed to change to facilitate the scheme upgrade.

<pre><code class="language-php">
style-src 'self' data: ;
     # Data-Uri in a CSS =&gt; OK
</code></pre>

In this example, the keyword <code>data:</code> authorizes embedded content in CSS files.

Under the CSP level 1 specification, you may also define rules for the following:

*   `img-src` valid sources of images
*   `connect-src` applies to XMLHttpRequest (AJAX), WebSocket or EventSource
*   `font-src` valid sources of fonts
*   `object-src` valid sources of plugins (for example, `<object>`, `<embed>`, `<applet>`)
*   `media-src` valid sources of `<audio>` and `<video>`

CSP level 2 rules include the following:

*   `child-src` valid sources of web workers and elements such as `<frame>` and `<iframe>` (this replaces the deprecated `frame-src` from CSP level 1)
*   `form-action` valid sources that can be used as an HTML `<form>` action
*   `frame-ancestors` valid sources for embedding the resource using `<frame>`, `<iframe>`, `<object>`, `<embed>` or `<applet>`.
*   `upgrade-insecure-requests` instructs user agents to rewrite URL schemes, changing HTTP to HTTPS (for websites with a lot of old URLs that need to be rewritten).

For better backwards-compatibility with deprecated properties, you may simply copy the contents of the actual directive and duplicate them in the deprecated one. For example, you may copy the contents of <code>child-src</code> and duplicate them in <code>frame-src</code>.

CSP 2 allows you to whitelist paths (CSP 1 allows only domains to be whitelisted). So, rather than whitelisting all of <code>www.foo.com</code>, you could whitelist <code>www.foo.com/some/folder</code> to restrict it further. This does require CSP 2 support in the browser, but it is obviously more secure.

### <a id="An_example_66"></a>An Example

I made a simple example for the Paris Web 2015 conference, where I presented a talk entitled “<a href="https://rocssti.net/en/example-csp-paris-web2015">CSP in Action</a>.”

Without CSP, the page would look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a85e4457-477e-4f52-a224-6427d6aee1d4/csp-smashing1b.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b0a88ff-d511-4bd7-bf29-888621cdc6ab/csp-smashing1b-500.jpg" alt="This page without CSP, ugly and defaced" width="500" height="238" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a85e4457-477e-4f52-a224-6427d6aee1d4/csp-smashing1b.jpg">View large version</a></figcaption></figure>

Not very nice. What if we enabled the following CSP directives?

<div class="break-out">

<pre><code class="language-php"><br>
<span class="hljs-preprocessor">&lt;?php</span>
    header(<span class="hljs-string">"Content-Security-Policy: 
      default-src 'self' ;
      script-src 'self' www.google-analytics.com stats.g.doubleclick.net ; 
      style-src 'self' data: ;
      img-src 'self' www.google-analytics.com stats.g.doubleclick.net data: ;
      frame-src 'self' ;"</span>);
<span class="hljs-preprocessor">?&gt;</span>
</code></pre>
</div>

What would the browser do? It would (very strictly) apply these directives under the primary rule of CSP, which is that <strong>anything not authorized in a CSP directive will be blocked</strong> (“blocked” meaning not executed, not displayed and not used by the website).

By default in CSP, <strong>inline scripts and styles are not authorized</strong>, which means that every <code>&lt;script&gt;</code>, <code>onclick</code> or <code>style</code> attribute will be blocked. You could authorize inline CSS with <code>style-src 'unsafe-inline' ;</code>.

In a modern browser with CSP support, the example would look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7602c16-3001-4c6c-a31a-30dc9a230069/csp-smashing5.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a86237dd-3295-44d5-a9fa-9affe06f2a6c/csp-smashing5-500.jpg" alt="This page with CSP, really better" width="500" height="181" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7602c16-3001-4c6c-a31a-30dc9a230069/csp-smashing5.jpg">View large version</a></figcaption></figure>

What happened? The browser applied the directives and rejected anything that was not authorized. It sent these notifications to the console:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8bafc1-4e43-4724-91ed-14fe95477f89/csp-smashing2.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e91757-4ce4-4b83-903c-38671207b0ec/csp-smashing2-500.jpg" alt="CSP notifications" width="500" height="140" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8bafc1-4e43-4724-91ed-14fe95477f89/csp-smashing2.jpg">View large version</a></figcaption></figure>

If you’re still not convinced of the value of CSP, have a look at Aaron Gustafson’s article “<a href="https://www.aaron-gustafson.com/notebook/more-proof-we-dont-control-our-web-pages/">More Proof We Don’t Control Our Web Pages</a>.”

Of course, you may use stricter directives than the ones in the example provided above:

*   set `default-src` to `'none'`,
*   specify what you need for each rule,
*   specify the exact paths of required files,
*   etc.

## <a id="More_information_on_CSP_108"></a>More Information On CSP

### <a id="Support_110"></a>Support

CSP is not a nightly feature requiring three flags to be activated in order for it to work. CSP levels 1 and 2 are candidate recommendations! <a href="https://caniuse.com/#feat=contentsecuritypolicy">Browser support for CSP level 1</a> is excellent.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee839078-dc74-4ad6-9082-c951e3103949/csp-smashing3.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d730469-4ea6-407c-8d89-55e633e4a2c0/csp-smashing3-300x250.jpg" alt="CSP Level 1 support on Can I Use" width="500" height="265" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee839078-dc74-4ad6-9082-c951e3103949/csp-smashing3.jpg">View large version</a></figcaption></figure>

The <a href="https://caniuse.com/#feat=contentsecuritypolicy2">level 2 specification is more recent</a>, so it is a bit less supported.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b79107-609f-4607-96f8-6cc8499c91c3/csp-smashing4.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcb533e9-71b6-433a-9372-65f1d4e48be6/csp-smashing4-500.jpg" alt="CSP Level 2 support on Can I Use" width="500" height="299" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b79107-609f-4607-96f8-6cc8499c91c3/csp-smashing4.jpg">View large version</a></figcaption></figure>

CSP level 3 is an early draft now, so it is not yet supported, but you can already do great things with levels 1 and 2.

### <a id="Other_considerations_122"></a>Other Considerations

CSP has been designed to reduce cross-site scripting (XSS) risks, which is why enabling inline scripts in <code>script-src</code> directives is not recommended. Firefox illustrates this issue very nicely: In the browser, hit <code>Shift</code> + F2 and type <code>security csp</code>, and it will show you directives and advice. For example, here it is used on Twitter’s website:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5616dbd5-f273-4f25-a698-8ad26c4d24e9/csp-smashing6b.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dc57c3c-9b43-47ff-9bdf-0e02fd92cb4b/csp-smashing6b-500.jpg" alt="CSP display on Firefox" width="500" height="173" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5616dbd5-f273-4f25-a698-8ad26c4d24e9/csp-smashing6b.jpg">View large version</a></figcaption></figure>

Another possibility for inline scripts or inline styles, if you really have to use them, is to create a hash value. For example, suppose you need to have this inline script:

<pre><code class="language-javascript">
&lt;script&gt;alert(<span class="hljs-string">'Hello, world.'</span>);<span class="xml"><span class="hljs-tag">&lt;/<span class="hljs-title">script</span>&gt;</span>
</span>
</code></pre>

You might add <code>'sha256-qznLcsROx4GACP2dm0UCKCzCG-HiZ1guq6ZZDob_Tng='</code> as a valid source in your <code>script-src</code> directives. The hash generated is the result of this in PHP:

<div class="break-out">

<pre><code class="language-php"><br>
<span class="hljs-preprocessor">&lt;?php</span>
    <span class="hljs-keyword">echo</span> base64_encode(hash(<span class="hljs-string">'sha256'</span>, <span class="hljs-string">"alert('Hello, world.');"</span>, <span class="hljs-keyword">true</span>));
<span class="hljs-preprocessor">?&gt;</span>
</code></pre>
</div>

I said earlier that CSP is designed to reduce XSS risks — I could have added, “… and reduce the risks of unsolicited content.” With CSP, you have to <strong>know where your sources of content</strong> are and <strong>what they are doing on your front end</strong> (inline styles, etc.). CSP can also help you force contributors, developers and others to respect your rules about sources of content!

Now your question is, “OK, this is great, but how do we use it in a production environment?”

## <a id="How_to_use_it_in_the_real_world_147"></a>How To Use It In The Real World

The easiest way to get discouraged with using CSP the first time is to test it in a live environment, thinking, “This will be easy. My code is bad ass and perfectly clean.” Don’t do this. I did it. It’s stupid, trust me.

As I explained, CSP directives are activated with a CSP header — there is no middle ground. You are the weak link here. You might forget to authorize something or forget a piece of code on your website. CSP will not forgive your oversight. However, two features of CSP greatly simplify this problem.

### <a id="reporturi_153"></a>report-uri

Remember the notifications that CSP sends to the console? The directive <code>report-uri</code> can be used to tell the browser to send them to the specified address. Reports are sent in JSON format.

<pre><code class="language-php">
report-uri /csp-parser.php ;
</code></pre>

So, in the <code>csp-parser.php</code> file, we can process the data sent by the browser. Here is the most basic example in PHP:

<pre><code class="language-php"><br>
<span class="hljs-variable">$data</span> = file_get_contents(<span class="hljs-string">'php://input'</span>);

    <span class="hljs-keyword">if</span> (<span class="hljs-variable">$data</span> = json_decode(<span class="hljs-variable">$data</span>, <span class="hljs-keyword">true</span>)) {
     <span class="hljs-variable">$data</span> = json_encode(
      <span class="hljs-variable">$data</span>,
      JSON_PRETTY_PRINT | JSON_UNESCAPED_SLASHES
      );
     mail(EMAIL, SUBJECT, <span class="hljs-variable">$data</span>);
    }
</code></pre>

This notification will be transformed into an email. During development, you might not need anything more complex than this.

For a production environment (or a more visited development environment), you’d better use a way other than email to collect information, because there is no auth or rate limiting on the endpoint, and CSP can be <em>very</em> noisy. Just imagine a page that generates 100 CSP notifications (for example, a script that display images from an unauthorized source) and that is viewed 100 times a day — you could get 10,000 notifications a day!

A service such as <a href="https://report-uri.io/">report-uri.io</a> can be used to simplify the management of reporting. You can see <a href="https://github.com/nico3333fr/CSP-useful/tree/master/report-uri">other simple examples for report-uri</a> (with a database, with some optimizations, etc.) on GitHub.

### <a id="ReportOnly_181"></a>report-only

As we have seen, the biggest issue is that there is no middle ground between CSP being enabled and disabled. However, a feature named <code>report-only</code> sends a slightly different header:

<pre><code class="language-php"><br>
<span class="hljs-preprocessor">&lt;?php</span>
    header(<span class="hljs-string">"Content-Security-Policy-Report-Only: &lt;your directives&gt;"</span>);
<span class="hljs-preprocessor">?&gt;</span>
</code></pre>

Basically, this tells the browser, “Act as if these CSP directives were being applied, but do not block anything. Just send me the notifications.” It is a great way to test directives without the risk of blocking any required assets.

With <code>report-only</code> and <code>report-uri</code>, you can <strong>test CSP directives with no risk</strong>, and you can <strong>monitor in real time</strong> everything CSP-related on a website. These two features are really powerful for deploying and maintaining CSP!

## <a id="Conclusion_195"></a>Conclusion

### <a id="Why_CSP_is_cool_197"></a>Why CSP Is Cool

CSP is most important for your users: They don’t have to suffer any unsolicited scripts or content or XSS vulnerabilities on your website.

The most important advantage of CSP for website maintainers is <strong>awareness</strong>. If you’ve set strict rules for image sources, and a script kiddie attempts to insert an image on your website from an unauthorized source, that image will be blocked, and you will be notified instantly.

Developers, meanwhile, need to know exactly what their front-end code does, and CSP helps them master that. They will be prompted to refactor parts of their code (avoiding inline functions and styles, etc.) and to follow best practices.

### <a id="How_CSP_could_be_even_cooler_205"></a>How CSP Could Be Even Cooler

Ironically, CSP is <em>too</em> efficient in some browsers — it creates bugs with bookmarklets. So, <strong>do not update your CSP directives to allow bookmarklets</strong>. We can’t blame any one browser in particular; all of them have issues:

*   [Firefox](https://bugzilla.mozilla.org/show_bug.cgi?id=866522)
*   [Chrome (Blink)](https://bugs.chromium.org/p/chromium/issues/detail?id=233903)
*   [WebKit](https://bugs.webkit.org/show_bug.cgi?id=149000)

Most of the time, the bugs are false positives in blocked notifications. All browser vendors are working on these issues, so we can expect fixes soon. Anyway, this should not stop you from using CSP.

## <a id="Other_resources_articles_215"></a>Other Resources And Articles

### <a id="General_informations_217"></a>General Information

*   [Content Security Policy Quick Reference Guide](https://content-security-policy.com/), Foundeo
*   “[Content Security Policy Level 2](https://www.w3.org/TR/CSP/),” W3C
*   “[An Introduction to Content Security Policy](https://www.html5rocks.com/en/tutorials/security/content-security-policy/),” HTML5 Rocks
*   [SecurityHeaders.io](https://securityheaders.io/), Scott Helme
*   [CSP Useful, a Collection of Scripts, Thoughts About CSP](https://github.com/nico3333fr/CSP-useful), Nicolas Hoffmann, GitHub
*   [CSP Validator](https://cspvalidator.org/)
*   “[Upgrade Insecure Requests](https://www.w3.org/TR/upgrade-insecure-requests/),” W3C
*   “[CSP Cheat Sheet](https://scotthelme.co.uk/csp-cheat-sheet/),” Scott Helme

### <a id="Dropbox_series_on_their_CSP_policies_228"></a>Dropbox’s Series on Its CSP Policies

*   “[[CSP] On Reporting and Filtering](https://blogs.dropbox.com/tech/2015/09/on-csp-reporting-and-filtering/)”
*   “[[CSP] Unsafe-Inline and Nonce Deployment](https://blogs.dropbox.com/tech/2015/09/unsafe-inline-and-nonce-deployment/)”
*   “[[CSP] The Unexpected Eval](https://blogs.dropbox.com/tech/2015/09/csp-the-unexpected-eval/)”
*   “[[CSP] Third Party Integrations and Privilege Separation](https://blogs.dropbox.com/tech/2015/09/csp-third-party-integrations-and-privilege-separation/)”

### <a id="GitHub_CSP_policies_234"></a>GitHub’s CSP policies

*   “[GitHub’s CSP journey](https://githubengineering.com/githubs-csp-journey/)”

### <a id="Other_237"></a>Other Companies

*   “[We Said We’d Be Transparent: WIRED’s First Big HTTPS Snag](https://www.wired.com/2016/05/wired-first-big-https-rollout-snag/),” Wired
*   “[Content Security Policy for Single Page Web Apps](https://corner.squareup.com/2016/05/content-security-policy-single-page-app.html),” Square

### <a id="About_reporting_241"></a>About Reporting

*   “[Twitter's CSP Report Collector](https://oreoshake.github.io/csp/twitter/2014/07/25/twitters-csp-report-collector-design.html),” Neil Matatall, GitHub

### <a id="Example_of_directives_246"></a>Examples of Directives

*   [Collection of Examples](https://github.com/nico3333fr/CSP-useful/tree/master/csp-for-third-party-services), Nicolas Hoffmann, GitHub

### <a id="About_future_of_CSP_250"></a>The Future of CSP

*   “[Making CSP Great Again!](https://speakerdeck.com/mikispag/making-csp-great-again-michele-spagnuolo-and-lukas-weichselbaum)” (slides), Michele Spagnuolo and Lukas Weichselbaum
*   “[Content Security Policy Level 3](https://www.w3.org/TR/CSP3/),” W3C
*   “[Content Security Policy](https://github.com/w3c/webappsec-csp/),” W3C, GitHub

{{< signature "ds, il, al" >}}

