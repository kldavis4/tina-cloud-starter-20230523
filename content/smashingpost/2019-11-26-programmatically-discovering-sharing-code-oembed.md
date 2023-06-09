---
title: 'Programmatically Discovering Sharing Code With oEmbed'
slug: programmatically-discovering-sharing-code-oembed
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326588d3-f5ce-40dd-a743-c45672bfc031/programmatically-discovering-sharing-code-oembed.png
date: 2019-11-26T11:00:00.000Z
summary: >-
  Many sites have hosted media and content that can be shared elsewhere by the use of some HTML embed code. What happens if you just have the URL of the item and need to find an embeddable version of the media without human intervention? That is where oEmbed comes in.
description: >-
  Many sites have hosted media and content that can be shared elsewhere by the use of some HTML embed code. What happens if you just have the URL of the item and need to find an embeddable version of the media without human intervention? That is where oEmbed comes in.
categories:
  - API
  - Media
---
The web is full of services that host rich content such as videos, images, music and podcasts, maps and graphs, and all manner of different delights. Chances are, when you add your content to a site, it will offer you a way to embed that content in a web page somewhere else.

Sites like YouTube have their own embeddable player that is popular to use in blog posts and even product pages. Soundcloud has code for embedding their music player in your band’s website. Charity fundraisers might upload the route of their big race to a site like Strava, and want to share it on their fundraising site to show their sponsors.

All this is done by finding that _Share_ option on the hosting site and copying out some code that is normally a mix of HTML and JavaScript. That code can then usually be pasted into the destination page, and the hosting site will present a rich representation of the content for all your friends, customers and contacts to see.

So far, so good, and this covers the option for the manual embedding of content pretty well. There is a distinct second use-case however, where the outcome is the same but the route to it is very different.

{{% feature-panel %}}

## Sharing Programmatically

Let’s imagine you’re building an app or site that accepts content from a user. That could be something as simple as a basic intranet page for staff to share news with coworkers, or something massive like a whole social network where people can sign up and start posting.

In both cases, you need to work out what to do if the user adds a URL as part of that content. You can imagine the scenario:

<pre><code class="language-bash">Check out this video! https://youtu.be/jw7bRnFbwAI
</code></pre>

At this point, as a publishing system, you need to figure out what to do. The first option is to do nothing, and just leave the URL as plain text. That’s not a brilliant idea, as users will generally want to click on the URL and plain text won’t help them get to the page at the other end.

The second option is to turn it into a link. That’s a good solid next step, as users can follow the link and get to the content. But in doing so, they leave your site and might not come back in a hurry.

The best user experience might be to be able to fetch the player for that content and embed it right there instead of just the URL. That would enable users to experience the content right within your site, much like they would on Facebook, for example.

This poses the problem. Given a URL, how can I turn that into the HTML/JavaScript embed code needed to show a rich player on the page?

If it’s a known site like YouTube, I could write some code that uses the YouTube API to fetch the video information and get or build the embed code that way. I could do the same for other video services like Vimeo and VIVO. I can write code to recognize Flickr and Instagram URLs and use their APIs to fetch nice embeddable versions of photographs. And the same for Twitter and tweets. But this is sounding like a lot of work!

What would be ideal is if there was a standardized way of getting from a URL of a piece of content to a block of embed code to show that content on a page. If you’ve been paying attention, you’ll realize that the answer to that is oEmbed.

## The Origin Of oEmbed

This was exactly the problem [Leah Culver](https://leahculver.com) had while working on Pownce (a truly innovative social networking site that was the Betamax to Twitter’s VHS). Pownce wanted to embed rich representations of content into a user’s update stream, but didn’t want to limit support to only the services they’d specifically written code to integrate with. At dinner with colleague Mike Malone, as well as [Cal Henderson](https://www.iamcal.com) (who led engineering at Flickr &mdash; one of the major providers of such content at the time) and [Richard Crowley](https://rcrowley.org), they together hashed out an idea for an open standard for getting embed code from a URL. Henderson went away and drafted something up based on the discussion, and oEmbed was born.

## Using oEmbed

Here’s how it works.

It starts with the URL that points to a single item of content. That might be a YouTube video, an image, or whatever. Typically this will have been provided by a user of your site or app as part of some content they wish to publish. The first step is to fetch the content of the page at that URL, which should be an HTML page.

If the site hosting the content supports oEmbed, in the `<head>` section of that page there should be a `link` element with an `oembed` content type:

<div class="break-out">

 <pre><code class="language-json">&lt;link rel="alternate" type="application/json+oembed"
  href="https://youtube.com/oembed?url=https%3A%2F%2Fyoutu.be%2Fjw7bRnFbwAI&format=json"
  title="Inclusive Components with Heydon Pickering" /&gt;
</code></pre>
</div>

**A note about XML:** *oEmbed supports responses in both XML and JSON format. For this article, I’m only considering JSON, because we’re not savages. If you’re in the unfortunate position to need to work with XML, be aware that it is a supported format with the oEmbed spec, although you may find that some providers only offer JSON responses.*

{{% ad-panel-leaderboard %}}

This link tag as the `rel` attribute set to `alternate` and a `type` set to either `application/json+oembed` or `text/xml+oembed`. It’s this attribute that clues us into the fact that the URL given in the `href` is actually an oEmbed API endpoint for retrieving the details of the content.

That URL will have usually two parameters: `url` and `format`.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Parameter</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>url</code> (required)</td>
      <td>The URL-encoded web address of the content item</td>
    </tr>
    <tr>
      <td><code>format</code></td>
      <td>The format you’d like the response in. One of either <code>json</code> or <code>xml</code></td>
    </tr>
  </tbody>
</table>

<p><em>Common URL parameters for the initial consumer request</em></p>

The [full specification](https://oembed.com) goes into much more detail here (and you should reference that if creating your own implementation) but these are the two parameters you’ll likely see the most.

So, we’ve got a URL, fetched the page, found an oEmbed link tag with another URL for an API endpoint. Next, we request that new URL, and that returns all the information the service has to provide about that piece of content.

<div class="break-out">

 <pre><code class="language-json">{
        "author_name": "Smashing Magazine",
        "width": 480,
        "title": "Smashing TV: Inclusive Components with Heydon Pickering (Nov 7th 2019)",
        "provider_name": "YouTube",
        "height": 270,
        "html": "&lt;iframe width=\"480\" height=\"270\" src=\"https://www.youtube.com/embed/jw7bRnFbwAI?feature=oembed\" frameborder=\"0\" allow=\"accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture\" allowfullscreen&gt;&lt;/iframe&gt;",
        "provider_url": "https://www.youtube.com/",
        "thumbnail_url": "https://i.ytimg.com/vi/jw7bRnFbwAI/hqdefault.jpg",
        "type": "video",
        "thumbnail_height": 360,
        "author_url": "https://www.youtube.com/channel/UCSDtqcJ8ZXviPrEcj1vuLiQ",
        "version": "1.0",
        "thumbnail_width": 480
}
</code></pre>
</div>

Now we’re talking! The response gives us lots of information about the content. The `version` should for the foreseeable future be `1.0`, which is the current version of the oEmbed spec. The other information returned depends largely on the value of `type`.

## Response Types

The value of the `type` key in the response tells you what sort of media you’re going to be embedding.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Value of <code>type</code></th>
      <th>What to expect</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>photo</code></td>
      <td>A static photo that offers a <code>url</code>, <code>width</code> and <code>height</code> that can be used for a basic <code>img</code> tag</td>
    </tr>
    <tr>
      <td><code>video</code></td>
      <td>A video player, with <code>html</code> specifying the code required to embed a player on a page, although with a <code>width</code> and <code>height</code></td>
    </tr>
    <tr>
      <td><code>link</code></td>
      <td>The best way to deal with this content is just to provide a link after all. The response might have other useful information like a title, but it should just be linked up.</td>
    </tr>
    <tr>
      <td><code>rich</code></td>
      <td>Some sort of rich content player, which just like the video type returns <code>html</code>, <code>width</code> and <code>height</code></td>
    </tr>
  </tbody>
</table>

Aside from dedicated video content, the more common type you’re likely to see in the wild is `rich`. Even Flickr itself, while still sending a `photo` response, also supplies `html` for a rich embeddable 'player' for the image, too.

Most of the time, embedding the content in your site is just a case of using the code provided as the `html` value.

## A Note On Security

One thing you might be rightly cautious of is taking an HTML response and embedding it programmatically into a page you host. Without the human step to double-check the code you’re pasting in, there is always potential for that code to be malicious. As such you should take appropriate steps to mitigate the risk.

That might include filtering the URLs to make sure the schemes and domains match those expected, and sandboxing code into an iframe on a different, cookieless domain. You should access the situation in which you’re using the code and make sure that you’re not exposing your self to undue risk.

{{% ad-panel-leaderboard %}}

## Getting Started

As important as it is to understand the process when using oEmbed, the reality is that most common languages have libraries available that abstract away the process and make it relatively simple.

For example, the npm packaged [oembed](https://www.npmjs.com/package/oembed) provides a very simple interface for making a request based on the content URL and getting the oEmbed response back in return.

First install the package into your project:

<pre><code class="language-bash">npm i oembed
</code></pre>

And then request the URL. Here I’m using the URL of a presentation on Notist that I gave about oEmbed. How very meta.

<pre><code class="language-javascript">const oembed = require('oembed');
const url = 'https://noti.st/drewm/ZOFFfI';

oembed.fetch(url, { maxwidth: 1920 }, function(error, result) {
    if (error)
        console.error(error);
    else
        console.log("oEmbed result", result);
});
</code></pre>

And the response:

<div class="break-out">

 <pre><code class="language-json">{ 
        type: 'rich',
        version: '1.0',
        title: 'Understanding oEmbed',
          author_name: 'Drew McLellan',
        author_url: 'https://noti.st/drewm',
        provider_name: 'Notist',
        provider_url: 'https://noti.st',
        cache_age: 604800,
        thumbnail_url: 'https://on.notist.cloud/slides/deck4179/large-0.png',
        thumbnail_width: 1600,
        thumbnail_height: 900,
        html:
           '&lt;p data-notist="drewm/ZOFFfI"&gt;View &lt;a href="https://noti.st/drewm/ZOFFfI"&gt;Understanding oEmbed&lt;/a&gt; on Notist.&lt;/p&gt;&lt;script async src="https://on.notist.cloud/embed/002.js"&gt;&lt;/script&gt;',
        width: 960,
        height: 540 
}
</code></pre>
</div>

If you wanted to do the same in PHP, a handy package called [embed/embed](https://packagist.org/packages/embed/embed) is available to install via Composer.

<pre><code class="language-php">composer require embed/embed
</code></pre>

And then in your PHP project:

<pre><code class="language-php">use Embed\Embed;

$info = Embed::create('https://noti.st/drewm/ZOFFfI');

$info-&gt;title; // "Understanding oEmbed"
$info-&gt;authorName; // "Drew McLellan
$info-&gt;code; // "&lt;p data-notist="drewm/ZOFFfI"&gt; ... &lt;/script&gt;"
</code></pre>

As you can see, with the use of a library the process becomes very simple and you can quickly get from a URL to the embed code, ready to show a rich representation of the user’s content.

## Conclusion

oEmbed is a very elegant solution to a very specific problem. You’d be forgiven for thinking that only a few engineers working on big social networks would benefit from this, but in reality, publishing systems where a user might enter a URL are surprisingly common. Find me one back-end engineer who at some point hasn’t needed to build some kind of CMS. We may not think of it in the same terms, but if you accept user input, you should be thinking about what to do if that input contains URLs.

Now that you know about oEmbed (sorry) you’ve got no excuse not to give some serious consideration to how you handle URLs in your future projects. 

* [oEmbed specification](https://oembed.com)
* [oembed](https://www.npmjs.com/package/oembed) for NodeJS 
* [embed/embed](https://packagist.org/packages/embed/embed) for PHP
* “[Announcing OEmbed: An Open Standard for Embedded Content](https://blog.leahculver.com/2008/05/announcing-oembed-an-open-standard-for-embedded-content.html),” Leah Culver

{{< signature "ra, il" >}}
