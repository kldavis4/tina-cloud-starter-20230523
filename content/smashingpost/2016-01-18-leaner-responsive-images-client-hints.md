---
title: 'Leaner Responsive Images With Client Hints'
slug: leaner-responsive-images-client-hints
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9d339a-b604-4684-9460-a2f871327c8c/rwd-images-opt-1.png
date: 2016-01-18T20:54:09.000Z
author: jon-arne
summary: >-
  Developers have no reason not to explore Client Hints. The key benefits are more maintainable responsive image tags, fewer image bytes transferred and, ultimately, happier end users. This article will focus on how to address responsive images issues, with a little help from the web server and Client Hints, the new way for the browser to request images with specific properties.
description: >-
  Learn how to address responsive images issues, with help from the web server and Client Hints, a new way for the browser to request images with specific properties.
categories:
  - Coding
  - Mobile
  - Performance
---
**Responsive images** have been around long enough for most of us to have taken them for a spin, or at least to have learned from the experiences of those who have. Beyond doubt, the [responsive images](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) specification is a great win for the web. However, quite a few reports from the front lines suggest that responsive images **can become pretty ugly**.

The good news is that there is a fix! No, not throwing JavaScript at the challenge, but by asking the web server for a helping hand. Enter **Client Hints**, an initiative spearheaded by Google that is already available in browsers (Chrome and Opera) and that is super&ndash;simple to use. Let’s see how Client Hints can reduce both image size and verbosity of the responsive images markup.

This article will not demonstrate the challenges of responsive images. Several other sources have [already](https://www.scientiamobile.com/page/responsive-images-specification-real-world-scenarios) [done](https://codepen.io/Tigt/post/when-responsive-images-get-ugly) [that](https://dev.opera.com/articles/responsive-images/). Instead, **we’ll focus on how to address the issues**, with a little help from the web server and a new way for the browser, or client, to request images with specific properties. Even if this is called “Client *Hints*”, it is pretty specific. Let’s dive in!

<figure><a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9d339a-b604-4684-9460-a2f871327c8c/rwd-images-opt-1.png" width="500" height="340" alt="Character measuring a box labeled Image" /><figcaption>Good old problem: responsive images. Image credit: <a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">Eric Portis</a>.</figcaption></figure>

## What Are Client Hints?

Client Hints is a new feature already available with [Chrome 46](https://youtu.be/X1F8GEiZf9o?t=122) and Opera 33. More browser vendors are following. It is an [initiative by Google](https://github.com/igrigorik/http-client-hints) (spearheaded by Ilya Grigorik), and, as its progress indicates, it is likely to be “a thing”. The initiative was also recently adopted by the [HTTP Working Group](https://tools.ietf.org/html/draft-ietf-httpbis-client-hints-00).

You can think of Client Hints as the missing link between the browser and the server when it comes to layout information. Instead of specifying every possible image breakpoint, pixel density and format in your responsive images markup, Client Hints **append the current setting to the HTTP request**, allowing the web server to pick the perfect fit &mdash; also known as [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation).

The current way of dealing with responsive images is typically to specify different image sources based on the receiving device’s pixel density, preferred image format and viewport size. If you go through the process of picking breakpoints and formats, your markup might end up something like this:

<figure><a href="https://twitter.com/brad_frost/status/599676745176997889"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4e8eec8-458f-418a-b17f-040d2c5f9e6f/01-bradfrost-twitter-opt.png" width="500" height="593" alt="Tweet from Brad Frost stating: I never want to make anything that even remotely resembles this." /></a><figcaption>Even relatively simple use cases can become quite complex using the responsive images syntax. The code shown here is from <a href="https://alistapart.com/article/responsive-images-in-practice">A List Apart</a>. (Source: <a href="https://twitter.com/brad_frost/status/599676745176997889">Brad Frost</a>)</figcaption></figure>

I think many of us agree with Brad on this.

To be fair, the example above include different crops of the image too. Which is something Client Hints alone can’t help you with. Still, crafting markup like this is *not* something a developer or designer should be [spending their time on](https://blog.cloudfour.com/responsive-images-101-part-9-image-breakpoints/). **We need an automated process**. Even if the server can generate dynamic markup automatically, client hints decouples the markup from the image which makes it easier to perform operations on the image without having to worry too much about the markup.

{{% feature-panel %}}

## Let The Web Server Know

Imagine if the web server knew the pixel density, the viewport size and also the actual size and format of an image. This is what Client Hints does! Browsers that support Client Hints **add a few HTTP headers to requests**. The [latest draft](https://igrigorik.github.io/http-client-hints/) mentions these hints:

*   `DPR` This stands for “device pixel ratio,” the ratio of physical pixels on the screen to CSS pixels.
*   `Viewport-Width` This is the width of the viewport in CSS pixels. (CSS pixels means the units used in CSS to describe a layout. A CSS width of 100 pixels would be 200 device pixels (DP) if the device pixel ratio (DPR) was 2.)
*   `Width` This is the actual width of an image in real physical pixels (similar to the `w` descriptor made famous by responsive images).
*   `Downlink` This is the client’s maximum download speed.
*   `Save-Data` This boolean indicates whether extra measures should be taken to reduce the payload.

`Downlink` and `Save-Data` are not available in Chrome just yet, but you can imagine their purpose. Let’s focus on the currently available hints. First, we have to tell the browser to send the hints.

## Enabling Client Hints In Your HTML

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb54a073-ec6f-457e-965e-eaab0c06241e/02-clienthints101-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/826ae69b-bed7-4992-b780-edf5e7ebe185/02-clienthints101-preview-opt.png" width="500" height=".184" alt="The Client Hints flow: 1. Enable client hints. 2. Client hints are added. 3. Server selects or generates an image. 4. Server responds. 5. Image rendered." /></a><figcaption>With a `&lt;meta&gt;` tag added, Client Hints are enabled and additional HTTP headers are sent with the request.</figcaption></figure>

You’ll have to opt in to enable Client Hints. The reason for this is that additional data shouldn’t be added to a request unless it is used for something. If it’s not used, it would work against the very purpose by adding data to the payload. Web servers can also advertise their support by adding an HTTP header to the HTML response which lists the hints accepted by the server:

<pre><code class="language-http">Accept-CH: DPR, Width, Viewport-Width
</code></pre>

If adding an HTTP header is not an option, you can also add this meta tag inside the `&lt;head&gt;` element in your markup:

<pre><code class="language-markup">&lt;meta http-equiv="Accept-CH" content="DPR,Width,Viewport-Width"&gt;
</code></pre>

That’s all we need. The browser will now append the `DPR`, `Width` and `Viewport-Width` headers to *all* subsequent requests generated from the HTML, including CSS, JavaScript and so on (with exception of `Width`, which, in practice, applies only to images).

Aside from images, Client Hints might be **useful if the CSS file contains breakpoints based on the viewport size** or device pixel ratio. Knowing the viewport size before the CSS is returned to the browser, the server can strip unqualified blocks from the CSS file before sending the response. That is another story. For now, let’s look at an example with images.

## Our Old Friend, `<img>`

Imagine we have a page with the image tag below. Let’s display the `flower.jpg` image at a width of 200 CSS pixels.

<pre><code class="language-markup">&lt;img src="flower.jpg" width="200"&gt; 
</code></pre>

With Client Hints enabled, the browser will send the following request to the server:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/490a2a97-5b5f-4c8f-ace9-544cf21e9cfe/03-headers1-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f357b7b-ae90-4f6d-ba76-9dbab4caa230/03-headers1-preview-opt.png" width="500" height="193" alt="list of http headers" /></a><figcaption>With just the meta tag added, the browser appends `DPR` and `Viewport-Width` to the request.</figcaption></figure>

The browser “hints” to the server that the requesting device has a pixel ratio of 2. As a bonus, we get the size of the viewport, too, since this is known by the browser at the time when the request is being made. Because the DPR is 2 and our page’s design need this image to be 200 pixels wide, we would like to serve an image that is 400 actual pixels wide (200 pixels &times; 2).

But we’re missing information about the intended display size, even if the `img` tag says `width="200"`. The [specification explains](https://github.com/igrigorik/http-client-hints/blob/master/browser_implementation_considerations.md#width) that the `sizes` attribute has to be set in order for the `Width` header to be sent. In the near future, the `width` attribute on the image element is likely to be included in the algorithm too, but for now, we’ll have to stick with `sizes`. The `sizes` attribute describes the layout and display size of the image. In the beginning, it might be less intimidating to think of it like the good old `width` attribute or like a CSS property:

<pre><code class="language-markup">&lt;img src="flower.jpg" sizes="200px"&gt;
</code></pre>

Using pixels might make it easier to “retrofit” existing markup, but using [relative units](https://www.w3.org/TR/css3-values/#relative-lengths) such as `vw` is recommended to make the page more “responsive”:

<pre><code class="language-markup">&lt;img src="flower.jpg" sizes="25vw"&gt;
</code></pre>

Now, the request for `flowers.jpg` will look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3aac5fd4-d138-4411-9dc0-91fcd627dcf9/04-headers2-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0059be9-fefc-433b-955b-02220bc48b74/04-headers2-preview-opt.png" width="500" height="220" alt="HTTP headers list with highlights to DPR, Viewport-width and Width" /></a><figcaption>With `sizes` attribute added in addition to the meta tag, `Width` is added to the request.</figcaption></figure>

The browser calculates the intended display size of the image based on the current size of the viewport and the device pixel ratio of the device in time for the preloader to fetch it. In the example above, the viewport (`Viewport-Width`) is 774 pixels wide . The `&lt;img&gt;` tag specifies that the image should cover 25% of the viewport size: 193.5 CSS pixels.

Because it’s a high density display, with a pixel ratio (`DPR`) of two, we multiply the CSS pixels by the pixel ratio and arrive at 387 actual pixels (`Width`). You might recognize this from how the selection process work with “regular” markup for responsive images with multiple image sources listed. The difference here is that the **information is appended to the HTTP request**, rather than an image source being picked from the `srcset` attribute.

{{% ad-panel-leaderboard %}}

## Mind. Blown.

What just happened? Basically, we boiled our verbose responsive images tag down to something that looks very familiar, but with the same responsive functionality. With the pixel ratio and width information, the server can now pick, or generate, the appropriate size of the requested image.

*   The `DPR` header takes care of resolution switching. We don’t need `srcset` with `x` descriptors in our markup.
*   The `Width` header tells the server the exact width of the image (relative to the viewport) that the browser need to fit in the layout.

Actually, we don’t need `srcset` at all. The `sizes` attribute is our new hero! Based on the relative value of `sizes`, the browser translates this into the actual size in physical pixels. Also, remember that media conditions can be applied if you want the image to have different sizes as the width of the viewport changes:

<pre><code class="language-markup">&lt;img src="flower.jpg" sizes="(min-width: 30em) 100vw, 50vw"&gt; 
</code></pre>

The `Width` header will, of course, reflect this, too. For a deeper dive, Jason Grigsby has written a great introduction to `sizes` [over on Cloud Four](https://blog.cloudfour.com/responsive-images-101-part-5-sizes/)

But what about `type`? Responsive images allows you to define different formats, or mime types, of an image by using the `type` attribute: `type="image/webp"`

Client Hints does not cover this, but its older brother, the `Accept` header, may contain valuable information.

<pre><code class="language-markup">Accept: image/webp,image/*,*/*;q=0.8  
</code></pre>

This example is from Chrome, which is nice enough to tell us that [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/) is preferred. Other browsers might just say `*/*` which basically means, “Send me anything.” In those cases, you could apply your own rules, or, even better, the server could implement more advanced device intelligence solutions to decide the best image format to return to the client.

## The Server Side of Client Hints

We could say that, with Client Hints, we’re moving the responsibility of selecting an image source from the browser to the server. This means, of course, that we need to implement some logic to act on the Client Hints server&ndash;side.

The bonus of involving the server is that, rather than just selecting the best match from a list of pre&ndash;generated image files like the browser does, the **server can generate the perfect fit on the fly**! On a small scale, this is quite achievable because we have all the information we need in the HTTP header.

However, if this task is a bit daunting and if performance is a priority, a few web services &mdash; image proxies, if you will &mdash; already support Client Hints. One of them is the free [ImageEngine](https://web.wurfl.io/#image-engine). Using ImageEngine, for example, we first have to “prefix” our images with the URL of the service.

If your image `src`’s URL is `https://example.com/image.jpg`, then we’d have to change the `src` to `https://[key].lite.imgeng.in/https://example.com/image.jpg`. `[key]` is the personal token you get when you sign up. As long as the meta tag is present and that `sizes` attribute is present in the image tags, we’re good to go. Looking at the response with cURL, we can see how the server responds:

<pre><code class="language-bash">$ curl -I https://try.imgeng.in/https://web.wurfl.io/assets/sunsetbeach.jpg -H "DPR: 2" -H "Width: 150" -H "Viewport-Width: 800"

HTTP/1.1 200 OK Content-Type: image/jpeg Vary: Width Content-DPR: 2 … 
</code></pre>

The request has a `DPR` of 2, a `Width` of 150 pixels and a `Viewport-Width` of 800. The server then responds with the `Content-DPR` header, whose purpose is to [confirm to the browser](https://igrigorik.github.io/http-client-hints/#confirming-selected-dpr) what the pixel ratio is of the returned image, so that the browser can fit it on the page correctly.

In the example above, the `Content-DPR` will always be the same as the `DPR` request header, because ImageEngine is scaling the inputted image to the exact value of `Width`. As a bonus, even if `Width` is not set, ImageEngine will fall back to `Viewport-Width` and then to screen size data from WURFL, a database of devices.

If you implement the server yourself, and you chose to mimic browser behavior by selecting the closest match from a set of pre-generated image sources, then the `Content-DPR` header might be a different number than the `DPR` hint from the client. The browser will make use of `Content-DPR` to scale the image to its display dimensions.

Also worth noting is the `Vary` header. The purpose of this header is to tell the client (the browser or proxy) that the **response from this URI will vary** according to the value of the `Width` header. This enables web proxies and content delivery networks to cache the image better &mdash; at least compared to caching based on the `User-Agent`.

## Non-Supporting Browsers

Before you run off and start implementing support for Client Hints, you should know that not all browsers support them. The last `&lt;img&gt;` tag above will likely mess up a page viewed in a browser that does not support Client Hints. So, what are our options?

Maybe a [JavaScript polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill)? In this case, we’d have to rely on cookies, not separate HTTP headers. Cookies would create problems for content delivery networks and cache proxies because the cookie value must be included in the cache key, which would likely lead to cache pollution. Further, and more importantly, the browser’s [preloader](https://www.stevesouders.com/blog/2013/04/26/i/) would not have any knowledge of the cookie’s value.

Until support for Client Hints has reached critical mass, the safest approach is to **combine hints with explicit &mdash; but relative &mdash; widths and heights** to make sure the layout doesn’t break. If the browser doesn’t send Client Hints, but the image server expects it, you need the layout to handle an oversized image if that is the default behavior of the image server. Moreover, to reduce the risk of serving too big an image to a non&ndash;supporting browser, an image optimization service is recommended, as described above. ImageEngine is useful because it handles mobile devices fairly well (although I’m biased here!). If a mobile device does not support Client Hints, then ImageEngine will never serve an image wider than that particular device’s screen.

{{% ad-panel-leaderboard %}}

## Performance

Aside from automation, the motivation for implementing Client Hints is, of course, image performance. It’s difficult to compose a fair test case, but to give an idea of how a Client Hints&ndash;based image request performs differently than a “regular” responsive images request, I’ve put together a [little demo](https://wurfl.github.io/smdemo.html) with the two scenarios. Below is a table showing the bytes transferred and the actual size of the image put on the wire at different viewports. The selected image breakpoints and viewport sizes in the demo are arbitrary.

Responsive images w/srcsetClient Hints with server scaling

<table class="tablesaw break-out">
<thead>
<tr>
<th>Viewport width</th>
<th>KBytes (w/srcset)</th>
<th>Actual width (pixels, w/srcset)</th>
<th>KBytes (w/client hints)</th>
<th>Actual width (pixels, w/client hints)</th>
</tr>
</thead>
<tbody>
<tr>
<td>320</td>
<td>39.6</td>
<td>480</td>
<td>16.1</td>
<td>288</td>
</tr>
<tr>
<td>480</td>
<td>39.6</td>
<td>480</td>
<td>28.6</td>
<td>432</td>
</tr>
<tr>
<td>800</td>
<td>81.7</td>
<td>768</td>
<td>63</td>
<td>720</td>
</tr>
<tr>
<td>1100</td>
<td>138</td>
<td>1024</td>
<td>113</td>
<td>990</td>
</tr>
<tr>
<td>1400</td>
<td>138</td>
<td>1024</td>
<td>186</td>
<td>1260</td>
</tr>
</tbody>
</table>

While the preselected image breakpoints span portions of the viewport’s size, Client Hints, along with an image server capable of resizing images, addresses the continuum of viewport sizes. **With Client Hints, we have surgical precision**. On average, the Client Hints approach serves 19% less data. If we exclude the 1400&ndash;pixel viewport, to which the responsive images approach serves too small an image (1024 pixels), then the data served is 32% less with Client Hints, which is substantial.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5e46a8e-5503-425c-911c-7b530fc7d616/05-wptsmdemox-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1a11154-976c-48b5-8b75-5edd86e77d02/05-wptsmdemox-preview-opt.png" width="510" height="87" alt="WebPagetest screen showing test results" /></a><figcaption>Full test result can be <a href="https://www.webpagetest.org/result/151117_DY_HEF/">viewed on WebPagetest</a></figcaption></figure>

The data sample in the chart above is too small to draw any conclusions, but it illustrates the purpose of Client Hints well. No surprises there. Worth noting, though, is the use of [DNS prefetching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Controlling_DNS_prefetching) for the external host name `try.imgeng.in`. Referring to the table above, the time it takes to download the bytes is as expected. Client Hints works as advertised.

## (Almost) Ready For Prime Time

While responsive images (`&lt;img&gt;`) element with `srcset` and `sizes`) implemented in markup only allows the browser to pick the closest match from a list of image resources, Client Hints enable the web server to serve an image tailored to the browser’s needs, which in most cases mean **less data and better image quality**. It does require some programming if you’re implementing server&ndash;side support by yourself; luckily, some content delivery networks and web services already support it.

The future of Client Hints looks promising. Adding hints about the user’s connection and instructions to reduce data traffic are [on the way](https://igrigorik.github.io/http-client-hints/#the-downlink-client-hint). With this information, the server can increase image compression, avoid serving high&ndash;density images or reduce the byte size of images in other ways.

As developers, **we have no reason not to start exploring Client Hints right now**. The key benefits are less verbose and more maintainable responsive image tags, fewer image bytes transferred and, ultimately, happier end users. Only a few steps are needed from you:

1.  add the meta tag to the `head` element,
2.  put the `sizes` attribute in your image tags.

Then make, or pick, your image server. I’ve mentioned the free [ImageEngine](https://web.wurfl.io/#image-engine) optimization service above, which supports Client Hints. The best way to find other services that support Client Hints is to stay tuned and [search on Google](https://www.google.com/webhp?q=image+optimizing+client+hints&amp;gws_rd=cr&amp;ei=hWtUVr3FGIWlsgHzuo_wAg#) (duh!), because this is a new thing and more providers are announcing support as we speak.

If you want to implement support for Client Hints yourself, the article “[Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)” is a great start. Also, the open&ndash;source imaging service [Thumbor is also considering Client Hints](https://github.com/thumbor/thumbor/issues/549).

### Further Reading on SmashingMag:

*   “[Preload: What Is It Good For?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/),” Yoav Weiss
*   “[Responsive Images Done Right: A Guide To `<picture>` And `srcset`](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/),” Eric Portis
*   “[Introducing The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/),” Nadav Soferman
*   “[Why Perceived Performance Matters](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/),” Denys Mishunov

{{< signature "al, nl" >}}