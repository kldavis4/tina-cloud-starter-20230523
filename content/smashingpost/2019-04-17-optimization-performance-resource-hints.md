---
title: 'Optimizing Performance With Resource Hints'
slug: optimization-performance-resource-hints
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b750ed15-447d-4ef4-ac42-1a6452563c27/optimizing-performance-resource-hints.png
date: 2019-04-17T12:30:16+02:00
summary: >-
  Many performance optimizations can be made when we can predict what users might do before they actually do it. Resource Hints are a simple but effective way that web developers can help the browser to stay one step ahead of the user and keep pages fast.
description: >-
  Many performance optimizations can be made when we can predict what users might do before they actually do it. Resource Hints are a simple but effective way that web developers can help the browser to stay one step ahead of the user and keep pages fast.
categories:
  - Browsers
  - Performance
  - Optimization
---
Modern web browsers use all sorts of techniques to help improve page load performance by guessing what the user may be likely to do next. The browser doesn’t know much about our site or application as a whole, though, and often the best insights about what a user may be likely to do come from us, the developer.

Take the example of paginated content, like a photo album. We know that if the user is looking at a photo in an album, the chance of them clicking the 'next' link to view the following image in the album is pretty high. The browser, however, doesn’t really know that of all the links on the page, that’s the one the user is most likely to click. To a browser, all those links carry equal weight.

What if the browser could somehow know where the user was going next and could fetch the next page ahead of time so that when the user clicks the link the page load is much, much faster? That’s in principal what Resource Hints are. They’re **a way for the developer to tell the browser about what’s likely to happen in the future** so that the browser can factor that into its choices for how it loads resources.

All these resource hints use the `rel` attribute of the `<link>` element that you’ll be familiar with finding in the `<head>` of your HTML documents. In this article we’ll take a look at the main types of Resource Hints and when and where we can use them in our pages. We’ll go from the small and subtle hints through to the big guns at the end.

{{% feature-panel %}}

## DNS Prefetching

A DNS lookup is the process of turning a human-friendly domain name like `example.com` into the machine-friendly IP address like `123.54.92.4` that is actually needed in order to fetch a resource.

Every time you type a URL in the browser address bar, follow a link in a page or even load a resource like an image from a different domain, the browser needs to do a DNS lookup to find the server that holds the resource we’ve requested. For a busy page with lots of external resources (like perhaps a news website with loads of ads and trackers), there might be dozens of DNS lookups required per page.

The browser caches the results of these lookups, but they can be slow. One performance optimization technique is to reduce the number of DNS lookups required by organizing resources onto fewer domains. When that’s not possible, you can warn the browser about the domains it’s going to need to look up with the `dns-prefetch` resource hint.

<div class="break-out">

 <pre><code class="language-html">&lt;link rel="dns-prefetch" href="https://images.example.com"&gt;
</code></pre>
</div>

When the browser encounters this hint, it can start resolving the `images.example.com` domain name as soon as possible, even though it doesn’t know how it’ll be used yet. This enables the browser to get ahead of the game and do more work in parallel, decreasing the overall load time.

### When Should I Use `dns-prefetch`?

Use `dns-prefetch` when your page uses resources from a different domain, to give the browser a head start. [Browser support is really great](https://caniuse.com/#search=dns-prefetch), but if a browser doesn’t support it then no harm done &mdash; the prefetch just doesn’t happen.

Don’t prefetch any domains you’re _not_ using, and if you find yourself wanting to prefetch a large number of domains you might be better to look at why all those domains are needed and if anything can be done to reduce the number.

## Preconnecting

One step on from DNS prefetching is _preconnecting_ to a server. Establishing a connection to a server hosting a resource takes several steps:

- **DNS lookup** (as we’ve just discussed);
- **TCP handshake**  
A brief "conversation" between the browser and server to create the connection.
- **TLS negotiation on HTTPS sites**  
This verifies that the certificate information is valid and correct for the connection.

This typically happens once per server and takes up valuable time &mdash; especially if the server is very distant from the browser and network latency is high. (This is where globally distributed CDNs really help!) In the same way that prefetching DNS can help the browser get ahead of the game before it sees what’s coming, pre-connecting to a server can make sure that when the browser gets to the part of the page where a resource is needed, the slow work of establishing the connection has already taken place and the line is open and ready to go.

<pre><code class="language-html">&lt;link rel="preconnect" href="https://scripts.example.com"&gt;
</code></pre>

### When Should I Use `preconnect`?

Again, [browser support is strong](https://caniuse.com/#search=preconnect) and there’s no harm if a browser doesn’t support preconnecting &mdash; the result will be just as it was before. Consider using preconnect when you know for sure that you’re going to be accessing a resource and you want get ahead.

Be careful not to preconnect and then not use the connection, as this will both slow your page down and tie up a tiny amount of resource on the server you connect to too.

## Prefetching The Next Page

The two hints we’ve looked at so far are primarily focussed on resources within the page being loaded. They might be useful to help the browser get ahead on images, scripts or fonts, for example. The next couple of hints are concerned more with navigation and predicting where the user might go _after_ the page that’s currently being loaded.

The first of these is prefetching, and its link tag might look like this:

<div class="break-out">

 <pre><code class="language-html">&lt;link rel="prefetch" href="https://example.com/news/?page=2" as="document"&gt;
</code></pre>
</div>

This tells the browser that it can go ahead and fetch a page in the background so that it’s ready to go when requested. There’s a bit of a gamble here because you have to preempt where you think the user will navigate next. Get it right, and the next page might appear to load really quickly. Get it wrong, and you’ve wasted time and resources in downloading something that isn’t going to be used. If the user is on a metered connection like a limited mobile phone plan, you might actually cost them real money.

When a prefetch takes place, the browser does the DNS lookup and makes the server connection we’ve seen in the previous two types of hint, but then goes a step further and actually requests and downloads the files. It stops at that point, however, and the files are not parsed or executed and they are in no way applied to the current page. They’re just requested and kept ready.

You might think of a prefetch as being a bit like adding a file to the browser’s cache. Instead of needing to go out to the server and download it when the user clicks the link, the file can be pulled out of memory and used much quicker.

{{% ad-panel-leaderboard %}}

### The `as` Attribute

In the example above, you can see that we’re setting the `as` attribute to `as="document"`. This is an optional attribute that tells that browser that what we’re fetching should be handled as a document (i.e. a web page). This enables the browser to set the same sort of request headers and security policies as if we'd just followed a link to a new page.

There are lots of possible values for the `as` attribute by enabling the browser to handle different types of prefetch in the appropriate way.

<table>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">Value of <code>as</code></th>
            <th>Type of resource</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>audio</code></td>
            <td>Sound and music files</td>
        </tr>
        <tr>
            <td><code>video</code></td>
            <td>Video</td>
        </tr>
        <tr>
            <td><code>Track</code></td>
            <td>Video or audio WebVTT tracks</td>
        </tr>
        <tr>
            <td><code>script</code></td>
            <td>JavaScript files</td>
        </tr>
        <tr>
            <td><code>style</code></td>
            <td>CSS style sheets</td>
        </tr>
        <tr>
            <td><code>font</code></td>
            <td>Web fonts</td>
        </tr>
        <tr>
            <td><code>image</code></td>
            <td>Images</td>
        </tr>
        <tr>
            <td><code>fetch</code></td>
            <td>XHR and Fetch API requests</td>
        </tr>
        <tr>
            <td><code>worker</code></td>
            <td>Web workers</td>
        </tr>
        <tr>
            <td><code>embed</code></td>
            <td>Multimedia <code>&lt;embed&gt;</code> requests</td>
        </tr>
        <tr>
            <td><code>object</code></td>
            <td>Multimedia <code>&lt;object&gt;</code> requests </td>
        </tr>
        <tr>
            <td><code>document</code></td>
            <td>Web pages</td>
        </tr>
    </tbody>
</table>
<p><em>The different values that can be used to specify resource types with the `as` attribute.</em></p>

### When Should I Use `prefetch`?

Again `prefetch` has [great browser support](https://caniuse.com/#search=prefetch). You should use it when you have a reasonable amount of certainty of the user might follow through your site if you believe that speeding up the navigation will positively impact the user experience. This should be weighed against the risk of wasting resources by possibly fetching a resource that isn’t then used.

## Prerendering The Next Page

With `prefetch`, we’ve seen how the browser can download the files in the background ready to use, but also noted that nothing more was done with them at that point. Prerendering goes one step further and executes the files, doing pretty much all the work required to display the page except for actually displaying it.

This might include parsing the resource for any _subresources_ such as JavaScript files and images and prefetching those as well.

<div class="break-out">

 <pre><code class="language-html">&lt;link rel="prerender" href="https://example.com/news/?page=2"&gt;
</code></pre>
</div>

This really can make the following page load feel instantaneous, with the sort of snappy load performance you might see when hitting your browser’s _back_ button. The gamble is even greater here, however, as you’re not only spending time requesting and downloading the files, but executing them along with any JavaScript and such. This could use up memory and CPU (and therefore battery) that the user won’t see the benefit for if they end up not requesting the page.

### When Should I Use `prerender`?

[Browser support](https://caniuse.com/#search=prerender) for `prerender` is currently very restricted, with really only Chrome and old IE (not Edge) offering support for the option. This might limit its usefulness unless you happen to be specifically targeting Chrome. Again it’s a case of "no harm, no foul" as the user won’t see the benefit but it won’t cause any issues for them if not.

{{% ad-panel-leaderboard %}}

## Putting Resource Hints To Use

We’ve already seen how resource hints can be used in the `<head>` of an HTML document using the `<link>` tag. That’s probably the most convenient way to do it, but you can also achieve the same with the `Link:` HTTP header.

For example, to prefetch with an HTTP header:

<div class="break-out">

 <pre><code class="language-bash">Link: &lt;https://example.com/logo.png&gt;; rel=prefetch; as=image;
</code></pre>
</div>

You can also use JavaScript to dynamically apply resource hints, perhaps in response to use interaction. To use an example from the W3C spec document:

<pre><code class="language-javascript">var hint  = document.createElement("link");
hint.rel  = "prefetch";
hint.as   = "document";
hint.href = "/article/part3.html";
document.head.appendChild(hint);
</code></pre>

This opens up some interesting possibilities, as it’s potentially easier to predict where the user might navigate next based on how they interact with the page.


## Things To Note

We’ve looked at four progressively more aggressive ways of preloading resources, from the lightest touch of just resolving DNS through to rending a complete page ready to go in the background. It’s important to remember that these hints are just that; they’re hints of **ways the browser could optimize performance**. They’re not directives. The browser can take our suggestions and use its best judgement in deciding how to respond.

This might mean that on a busy or overstretched device, the browser doesn’t attempt to respond to the hints at all. If the browser knows it’s on a metered connection, it might prefetch DNS but not entire resources, for example. If memory is low, the browser might again decide that it’s not worth fetching the next page until the current one has been offloaded.

The reality is that on a desktop browser, the hints will likely all be followed as the developer suggests, but be aware that it’s up to the browser in every case.

### The Importance Of Maintenance

If you’ve worked with the web for more than a couple of years, you’ll be familiar with the fact that if something on a page is unseen then it can often become neglected. Hidden metadata (such as page descriptions) is a good example of this. If the people looking after the site can’t readily see the data, then it can easily become neglected and drift out of date.

This is a real risk with resource hints. As the code is hidden away and goes pretty much undetected in use, it would be very easy for the page to change and any resource hints to go un-updated. The consequence of say, prefetching a page that you don’t use, means that the tools you’ve put in place to improve the performances of your site are then actively harming it. So having good procedures in place to key your resource hints up to date becomes really, _really_ important.

### Resources

- “[Resource Hints specification](https://www.w3.org/TR/resource-hints/),” W3C
- “[Speed Up Next-Page Navigations With Prefetching](https://addyosmani.com/blog/prefetching/),” Addy Osmani

{{< signature "il" >}}
