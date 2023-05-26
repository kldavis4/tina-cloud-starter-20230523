---
title: 'Optimizing Google Fonts Performance'
slug: optimizing-google-fonts-performance
author: danny-cooper
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31184344-7761-4ebe-81ed-4b1d920eda76/danny-cooper-google-fonts-sharing-card.png
date: 2019-06-20T11:00:16+02:00
summary: >-
  Google Fonts are easy to implement, but they can have a big impact on your page load times. Let’s explore how we can load them in the most optimal way.
description: >-
  Google Fonts are easy to implement, but they can have a big impact on your page load times. Let’s explore how we can load them in the most optimal way.
categories:
  - Fonts
  - Optimization
  - Performance
  - Guides
---
<p>It’s fair to say Google Fonts are popular. As of writing, they have been viewed over <a href="https://fonts.google.com/analytics">29 trillion</a> times across the web and it’s easy to understand why &mdash; the collection gives you access to over 900 beautiful fonts you can use on your website for free. Without Google Fonts you would be limited to the handful of “<a href="https://fontsplugin.com/web-safe-system-fonts/">system fonts</a>” installed on your user’s device.</p>

<blockquote>System fonts or ‘Web Safe Fonts’ are the fonts most commonly pre-installed across operating systems. For example, Arial and Georgia are packaged with Windows, macOS and Linux distributions.</blockquote>

<p>Like all good things, Google Fonts do come with a cost. Each font carries a weight that the web browser needs to download before they can be displayed. With the correct setup, the additional load time isn’t noticeable. However, get it wrong and your users could be waiting up to a few seconds before any text is displayed.</p>

## Google Fonts Are Already Optimized

<p>The Google Fonts API does more than just provide the font files to the browser, it also performs a smart check to see how it can deliver the files in the most optimized format.</p>

<p>Let’s look at Roboto, GitHub tells us that the regular variant weighs 168kb.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470e4f56-094d-4116-b621-d806b30bced7/github-file-size.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470e4f56-094d-4116-b621-d806b30bced7/github-file-size.jpg" sizes="100vw" caption="168kb for a single font variant. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470e4f56-094d-4116-b621-d806b30bced7/github-file-size.jpg'>Large preview</a>)" alt="Roboto Regular has a file size of 168kb" >}}

<p>However, if I request the same font variant from the API, I’m provided with this <a href="https://fonts.gstatic.com/s/roboto/v19/KFOmCnqEu92Fr1Mu72xKKTU1Kvnz.woff2">file</a>. Which is only 11kb. How can that be?</p>

<p>When the browser makes a request to the API, Google first checks which file types the browser supports. I’m using the latest version of Chrome, which like most browsers supports WOFF2, so the font is served to me in that highly compressed format.</p>

<p>If I change my user-agent to Internet Explorer 11, I’m served the font in the WOFF format instead.</p>

<p>Finally, if I change my user agent to IE8 then I get the font in the EOT (Embedded OpenType) format.</p>

<blockquote>Google Fonts maintains 30+ optimized variants for each font and automatically detects and delivers the optimal variant for each platform and browser.<br /><br />&mdash; Ilya Grigorik, <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization#reducing_font_size_with_compression">Web Font Optimization</a></blockquote>

<p>This is a great feature of Google Fonts, by checking the user-agent they are able to serve the most performant formats to browsers that support those, while still displaying the fonts consistently on older browsers.</p>

{{% feature-panel %}}

### Browser Caching

<p>Another built-in optimization of Google Fonts is browser caching.</p>

<p>Due to the ubiquitous nature of Google Fonts, the browser doesn’t always need to download the full font files. SmashingMagazine, for example, uses a font called ‘Mija’, if this is the first time your browser has seen that font, it will need to download it completely before the text is displayed, but the next time you visit a website using that font, the browser will use the cached version.</p>

<blockquote>As the Google Fonts API becomes more widely used, it is likely visitors to your site or page will already have any Google fonts used in your design in their browser cache.<br /><br />&mdash; FAQ, <a href="https://developers.google.com/fonts/faq#will_web_fonts_slow_down_my_page">Google Fonts</a></blockquote>

<p>The Google Fonts browser cache is set to expire after one year unless the cache is cleared sooner.</p>

<p><strong>Note:</strong> <em>Mija isn’t a Google Font, but the principles of caching aren’t vendor-specific.</em></p>

## Further Optimization Is Possible

<p>While Google invests great effort in optimizing the delivery of the font files, there are still optimizations you can make in your implementation to reduce the impact on page load times.</p>

### 1. Limit Font Families

<p>The easiest optimization is to simply use fewer font families. Each font can add up to 400kb to your page weight, multiply that by a few different font families and suddenly your fonts weigh more than your entire page.</p>
 
<p>I recommend using no more than two fonts, one for headings and another for content is usually sufficient. With the right use of font-size, weight, and color you can achieve a great look with even one font.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e496f6c-7cab-40e6-95d6-7efe1de59a68/single-font-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e496f6c-7cab-40e6-95d6-7efe1de59a68/single-font-example.jpg" sizes="100vw" caption="Three weights of a single font family (Source Sans Pro). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e496f6c-7cab-40e6-95d6-7efe1de59a68/single-font-example.jpg'>Large preview</a>)" alt="Example showing three weights of a single font family (Source Sans Pro)" >}}

### 2. Exclude Variants

<p>Due to the high-quality standard of Google Fonts, many of the font families contain the full spectrum of available font-weights:</p>

<ul>
  <li>Thin (100)</li>
  <li>Thin Italic (100i)</li>
  <li>Light (300)</li>
  <li>Light Italic (300i)</li>
  <li>Regular (400)</li>
  <li>Regular Italic (400i)</li>
  <li>Medium (600)</li>
  <li>Medium Italic (600i)</li>
  <li>Bold (700)</li>
  <li>Bold Italic (700i)</li>
  <li>Black (800)</li>
  <li>Black Italic (800i)</li>
</ul>

<p>That’s great for advanced use-cases which might require all 12 variants, but for a regular website, it means downloading all 12 variants when you might only need 3 or 4.</p>

<p>For example, the Roboto font family weighs ~144kb. If however you only use the Regular, Regular Italic and Bold variants, that number comes down to ~36kb. A 75% saving!</p>

<p>The default code for implementing Google Fonts looks like this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet"&gt;
</code></pre>
</div>

<p>If you do that, it will load only the ‘regular 400’ variant. Which means all light, bold and italic text will not be displayed correctly.</p>

<p>To instead load all the font variants, we need to specify the weights in the URL like this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Roboto:100,100i,300,300i,400,400i,500,500i,700,700i,900,900i" rel="stylesheet"&gt;
</code></pre>
</div>

<p>It’s rare that a website will use all variants of a font from Thin (100) to Black (900), the optimal strategy is to specify just the weights you plan to use:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Roboto:400,400i,600" rel="stylesheet"&gt;
</code></pre>
</div>

<p>This is especially important when using multiple font families. For example, if you are using Lato for headings, it makes sense to only request the bold variant (and possibly bold italic):</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Lato:700,700i" rel="stylesheet"&gt;
</code></pre>
</div>

### 3. Combine Requests

<p>The code snippet we worked with above makes a call to Google’s servers (<code>fonts.googleapis.com</code>), that’s called an HTTP request. Generally speaking, the more HTTP requests your web page needs to make, the longer it will take to load.</p>

<p>If you wanted to load two fonts, you might do something like this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Open+Sans:400,400i,600" rel="stylesheet"&gt;
&lt;link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet"&gt;
</code></pre>
</div>

<p>That would work, but it would result in the browser making two requests. We can optimize that by combining them into a single request like this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Roboto|Open+Sans:400,400i,600" rel="stylesheet"&gt;
</code></pre>
</div>

<p>There is no limit to how many fonts and variants a single request can hold.</p>

{{% ad-panel-leaderboard %}}

### 4. Resource Hints

<p>Resource hints are a feature supported by modern browsers which can boost website performance. We are going to take a look at two types of resource hint: ‘<a href="https://caniuse.com/#feat=link-rel-dns-prefetch">DNS Prefetching</a>’ and ‘<a href="https://caniuse.com/#feat=link-rel-preconnect">Preconnect</a>’.</p>

<p><strong>Note:</strong> <em>If a browser doesn’t support a modern feature, it will simply ignore it. So your web page will still load normally.</em></p>

#### DNS Prefetching

<p>DNS prefetching allows the browser to start the connection to Google’s Fonts API (<code>fonts.googleapis.com</code>) as soon as the page begins to load. This means that by the time the browser is ready to make a request, some of the work is already done.</p>

<p>To implement DNS prefetching for Google Fonts, you simply add this one-liner to your web pages <code>&lt;head&gt;</code>:</p>

<pre><code class="language-html">&lt;link rel="dns-prefetch" href="//fonts.googleapis.com"&gt;
</code></pre>

#### Preconnect

<p>If you look at the Google Fonts embed code it appears to be a single HTTP request:</p>

<div class="break-out">

<pre><code class="language-html">&lt;link href="https://fonts.googleapis.com/css?family=Roboto:400,400i,700" rel="stylesheet"&gt;
</code></pre>
</div>

<p>However, if we visit that URL we can see there are three more requests to a different URL, <a href="https://fonts.gstatic.com">https://fonts.gstatic.com</a>. One additional request for each font variant.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4655b9f4-3218-4e35-abec-113bd3b12302/google-fonts-css.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4655b9f4-3218-4e35-abec-113bd3b12302/google-fonts-css.jpg" sizes="100vw" caption="(<a href='https://fonts.googleapis.com/css?family=Roboto:400,400i,700'>View source</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4655b9f4-3218-4e35-abec-113bd3b12302/google-fonts-css.jpg'>Large preview</a>)" alt="Source code of a Google Fonts Request" >}}

<p>The problem with these additional requests is that the browser won’t begin the processes to make them until the first request to <code>https://fonts.googleapis.com/css</code> is complete. This is where Preconnect comes in.</p>

<p>Preconnect could be described as an enhanced version of prefetch. It is set on the specific URL the browser is going to load. Instead of just performing a DNS lookup, it also completes the TLS negotiation and TCP handshake too.</p>

<p>Just like DNS Prefetching, it can be implemented with one line of code:</p>

<pre><code class="language-html">&lt;link rel="preconnect" href="https://fonts.gstatic.com/" crossorigin&gt;
</code></pre>

<p>Just adding this line of code can <a href="https://www.cdnplanet.com/blog/faster-google-webfonts-preconnect/">reduce your page load time by 100ms</a>. This is made possible by starting the connection alongside the initial request, rather than waiting for it to complete first.</p>

### 5. Host Fonts Locally

<p>Google Fonts are licensed under a ‘Libre’ or ‘free software’ license, which gives you the freedom to use, change and distribute the fonts without requesting permission. That means you don’t need to use Google’s hosting if you don’t want to &mdash; you can self-host the fonts!</p>

<p>All of the fonts files are available on <a href="https://github.com/google/fonts">Github</a>. A <a href="https://github.com/google/fonts/archive/master.zip">zip file</a> containing all of the fonts is also available (387MB).</p>

<p>Lastly, there is a <a href="https://google-webfonts-helper.herokuapp.com">helper service</a> that enables you to choose which fonts you want to use, then it provides the files and CSS needed to do so.</p>

<p>There is a downside to hosting fonts locally. When you download the fonts, you are saving them as they are at that moment. If they are improved or updated, you won’t receive those changes. In comparison, when requesting fonts from the Google Fonts API, you are always served the most up-to-date version.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5250f760-5aaf-44a0-940b-d330ecaac79b/google-fonts-api-request.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5250f760-5aaf-44a0-940b-d330ecaac79b/google-fonts-api-request.jpg" sizes="100vw" caption="Google Fonts API Request. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5250f760-5aaf-44a0-940b-d330ecaac79b/google-fonts-api-request.jpg'>Large preview</a>)" alt="Google Fonts API Request showing a last modified date" >}}

<p><em>Note the <code>lastModified</code> parameter in the API. The fonts are regularly modified and improved.</em></p>

{{% ad-panel-leaderboard %}}

### 6. Font Display

<p>We know that it takes time for the browser to download Google Fonts, but what happens to the text before they are ready? For a long time, the browser would show blank space where the text should be, also known as the "FOIT” (Flash of Invisible Text).</p>

<p><strong>Recommended Reading</strong>: <em>“<a href="https://css-tricks.com/fout-foit-foft/">FOUT, FOIT, FOFT</a>” by Chris Coyier</em></p>

<p>Showing nothing at all can be a jarring experience to the end user, a better experience would be to initially show a system font as a fallback and then “swap” the fonts once they are ready. This is possible using the <a href="https://caniuse.com/#feat=css-font-rendering-controls">CSS <code>font-display</code> property</a>.</p>

<p>By adding <code>font-display: swap;</code> to the @font-face declaration, we tell the browser to show the fallback font until the Google Font is available.</p>

<div class="break-out">

<pre><code class="language-css">    @font-face {
    font-family: 'Roboto';
    src: local('Roboto Thin Italic'),
  url(https://fonts.gstatic.com/s/roboto/v19/KFOiCnqEu92Fr1Mu51QrEz0dL-vwnYh2eg.woff2)
  format('woff2');
    font-display: swap;
  }
</code></pre>
</div>

<p>In 2019 Google, announced they would add support for <a href="https://fontsplugin.com/google-fonts-font-display-swap/">font-display: swap</a>. You can begin implementing this right away by adding an extra parameter to the fonts URL:</p>

<pre><code class="language-html">https://fonts.googleapis.com/css?family=Roboto&display=swap
</code></pre>

### 7. Use the <code>Text</code> Parameter

<p>A little known feature of the Google Fonts API is the <code>text</code> parameter. This rarely-used parameter allows you to only load the characters you need.</p>

<p>For example, if you have a text-logo that needs to be a unique font, you could use the <code>text</code> parameter to only load the characters used in the logo.</p>

<p>It works like this:</p>

<pre><code class="language-html">https://fonts.googleapis.com/css?family=Roboto&text=CompanyName
</code></pre>

<p>Obviously, this technique is very specific and only has a few realistic applications. However, if you can use it, it can cut down the font weight by up to 90%.</p>

<p><strong>Note:</strong> <em>When using the <code>text</code> parameter, only the “normal” font-weight is loaded by default. To use another weight you must explicitly specify it in the URL.</em></p>

<pre><code class="language-html">https://fonts.googleapis.com/css?family=Roboto:700&text=CompanyName
</code></pre>

## Wrapping Up

<p><a href="https://trends.builtwith.com/widgets/Google-Font-API">With an estimated 53%</a> of the top 1 million websites using Google Fonts, implementing these optimizations can have a huge impact.</p>

<p>How many of the above have you tried? Let me know in the comments section.</p>

{{< signature "dm, yk, il" >}}
