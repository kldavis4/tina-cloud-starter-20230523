---
title: 'Protecting Your Site With Feature Policy'
slug: feature-policy
author: rachel-andrew
image: >-
  //res.cloudinary.com/indysigner/image/upload/v1544084120/Social-preview-image/rachel-andrew-protecting-site-feature-policy.png
date: 2018-12-12T11:30:30+02:00
summary: >-
  Feature Policy can help protect your site from third parties using APIs that have security and privacy implications, and also from your own team adding outdated APIs or poorly optimized images. Find out how.
description: >-
  Feature Policy can help protect your site from third parties using APIs that have security and privacy implications, and also from your own team adding outdated APIs or poorly optimized images. Find out how.
categories:
  - API
  - Security
  - Browsers
---
One of the web platform features highlighted at the recent Chrome Dev Summit was Feature Policy, which aims to “allow site authors to selectively enable and disable use of various browser features and APIs.” In this article, I'll take a look at what that means for web developers, with some practical examples.

In his [introductory article](https://developers.google.com/web/updates/2018/06/feature-policy) on the Google Developers site, Eric Bidelman describes Feature Policy as the following:

<blockquote>“The feature policies themselves are little opt-in agreements between developer and browser that can help foster our goals of building (and maintaining) high-quality web apps.”</blockquote>

The specification has been developed at Google by as part of the Web Platform Incubator Group activity. The aim of Feature Policy is for us, as web developers, to be able to state our usage of a web platform feature, explicitly to the browser. By doing so, we make an agreement about our use, or non-use of this particular feature. Based on this the browser can act to block certain features, or report back to us that a feature it did not expect to see is being used.

Examples might include:

1. I am embedding an iframe and I do not want the embedded site to be able to access the camera of my visitor;
2. I want to catch situations where unoptimized images are deployed to my site via the CMS;
3. There are many developers working on my project, and I would like to know if they use outdated APIs such as `document.write`.

All of these things can be tracked, blocked or reported on as part of Feature Policy.

## How To Use Feature Policy

In order to use Feature Policy, the browser needs to know two things: which feature you are creating a policy for, and how you want that feature to be handled.

<pre><code class="language-html">Feature-Policy: &lt;directive&gt; &lt;allowlist&gt;
</code></pre>

The `<directive>` is the name of the feature that you are setting the policy on.

{{% feature-panel %}}

The current list of features (sourced from <a href="https://www.youtube.com/watch?v=igHvSUrLqXc">the presentation given at Chrome Dev Summit</a>) are as follows:

- accelerometer
- ambient-light-sensor
- autoplay
- camera
- document-write
- encrypted-media
- fullscreen
- geolocation
- gyroscope
- layout-animations
- lazyload
- legacy-image-formats
- magnetometer
- midi
- oversized-images
- payment
- picture-in-picture
- speaker
- sync-script
- sync-xhr
- unoptimized-images
- unsized-media
- usb
- vertical-scroll
- vr

The `<allowlist>` details how the feature can be used &mdash; if at all &mdash; and takes one or more of the following values.

- `*`  
The most liberal policy, stating that the feature will be allowed in this document, and any iframes whether from this domain or elsewhere. May only be used as a single value as it makes no sense to enable everything and also pass in a list of domains, for example.
- `self`  
The feature will be available in the document and any iframes, however, the iframes must have the same origin.
- `src`  
Only applicable when using an iframe `allow` attribute. This allows a feature as long as the document loaded into it comes from the same origin as the URL in the iframe's src attribute.
- `none`  
Disables the feature for the document and any nested iframes. May only be used as a single value.
- `<origin(s)>`  
The feature is allowed for specific origins; this means that you can specify a list of domains where the feature is allowed. The list of domains is space separated.

There are two methods by which you can enable feature policies on your site: You can send an HTTP Header, or use the `allow` attribute on an iframe.

### HTTP Header

Sending an HTTP Header means that you can enable a feature policy for the page or entire site setting that header, and also anything embedded in the site. Headers can be set for your entire site at the web server or can be sent from your application.

For example, if I wanted to prevent the use of the geolocation API and I was using the NGINX web server, I could edit the configuration files for my site in NGINX to add the following header, which would prevent any document in my site and any iframe embedded in from using the geolocation API.

<pre><code class="language-html">add_header Feature-Policy "geolocation none;";</code></pre>

Multiple policies can be set in a single header. To prevent geolocation and vibrate but allow `unsized-media` from the domain *example.com* I could set the following:

<pre><code class="language-html">add_header Feature-Policy "vibrate none; geolocation none; unsized-media https://example.com;";</code></pre>

### The `allow` Attribute On iFrames

If we are primarily concerned with what happens with the content in an iframe, we can use Feature Policy on the iframe itself; this benefits from slightly better browser support at the time of writing with Chrome and Safari supporting this use.

If I am embedding a site and do not want that site to use geolocation, camera or microphone APIs then my iframe would look like the following example:

<div class="break-out">

<pre><code class="language-html">&lt;iframe allow=&quot;geolocation &#39;none&#39;; camera &#39;none&#39;; microphone &#39;none&#39;&quot;&gt;</code></pre></div>

You may already be familiar with the individual attributes which control the content of iframes `allowfullscreen`, `allowpaymentrequest`, and `allowusermedia`. These can be replaced by the Feature Policy `allow` attribute, and for browser compatibility reasons you can use both on an iframe. If you do use both attributes, then the most restrictive one will apply. The Google article shows an example of an iframe that uses `allowfullscreen` &mdash; meaning that the iframe is allowed to enter fullscreen, but then a conflicting Feature Policy of `fullscreen none`. These conflict, so the most restrictive policy wins and this iframe would not be allowed to enter fullscreen.

<div class="break-out">

<pre><code class="language-html">&lt;iframe allowfullscreen allow=&quot;fullscreen &#39;none&#39;&quot; src=&quot;...&quot;&gt;</code></pre></div>

The iframe element also has a `sandbox` attribute designed to manage support for many features. This feature was also added to Content Security Policy with a `sandbox` value which disables all sandbox features, which can then be opted back into selectively. There is some crossover between sandbox features and those controlled by Feature Policy, and Feature Policy does not seek to duplicate those values already covered by sandbox. It does, however, address some of the limitations of sandbox by taking a more fine-grained approach to managing these policies, rather than one of turning everything off globally as one large policy set.

{{% ad-panel-leaderboard %}}

### Feature Policy And Reporting API

Feature Policy violations can be reported via the [Reporting API](https://w3c.github.io/reporting/), which means that you could develop a comprehensive set of policies tracking feature usage across your site. This would be completely transparent to your users but give you a huge amount of information about how features were being used.

## Browser Support For Feature Policy

Currently, [browser support](https://caniuse.com/#feat=feature-policy) for Feature Policy is limited to Chrome, however, in many cases where you are using Feature Policy during development and when previewing sites this is not necessarily a problem.

Many of the use cases I will outline below are usable right now, without causing any impact to site visitors who are using browsers without support.

## When To Use Feature Policy

I really like the idea of being able to use Feature Policy to help back up decisions made when developing the site. Decisions which may well be written up in documents such as a performance budget, or as part of a GDPR audit, but which then become something we have to remember to preserve through the life of the site. This is not always easy when multiple people work on a site; people who perhaps weren't involved during that initial decision making, or may simply be unaware of the requirements. We think a lot about third parties managing to somehow impact our site, however, sometimes our sites need protecting from ourselves!

### Keeping An Eye On Third Parties

You could prevent a third-party site from accessing the camera or microphone using a feature policy on the iframe with the `allow` attribute. If the reason for embedding that site has nothing to do with those features, then disabling them means that the site can never start to ask for those. This could then be linked with [your processes for ensuring GDPR compliance](https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/). As you audit the privacy impact of your site, you can build in processes for locking down the access of third parties by way of feature policy &mdash; giving you and your visitors additional security and peace of mind.

This usage *does* rely on browser support for Feature Policy to block the usage. However, you could use Feature Policy reporting mode to inform you of usage of these APIs if the third party changed what they would be doing. This would give you a very quick heads-up &mdash; essentially as soon as the first person using Chrome hits the site.

### Selectively Enabling Features

We also might want to selectively enable some features which are normally blocked. Perhaps we wish to allow an iframe loading content from another site to use the geolocation feature in the browser. Chrome by default blocks this, but if you are loading content from a trusted site you could enable the cross-origin request using Feature Policy. This means that you can safely turn on features when loading content from another domain that is under your control.

### Catching Use Of Outdated APIs And Poorly Performing Features

Feature Policy can be run in a report-only mode. It can then track usage of certain features and let you know when they are found on the site. This can be useful in many scenarios. If you have a very large site with a lot of legacy code, enabling Feature Policy would help you to track down the places that need attention. If you work with a large team (especially if developers often pull in some third party libraries of code), Feature Policy can catch things that you would rather not see on the site.

{{% ad-panel-leaderboard %}}

### Dealing With Poorly Optimized Images

While most of the articles I've seen about Feature Policy concentrate on the security and privacy aspects, the features around image optimization really appealed to me, as someone who deals with a lot of content generated by technical and non-technical users. Feature Policy can be used to help protect the user experience as well as the performance of your site by preventing overly large &mdash; or unoptimized images &mdash; being downloaded by visitors.

In an ideal world, your CMS would deal with image management, ensuring that images were sensibly resized, optimized for the web and the context they will be displayed in. Real life is rarely that ideal world, however, and so sometimes the job of resizing and optimizing images is left to content editors to ensure they are not uploading huge images to the web. This is particularly an issue if you are using a static CMS with no content management layer on top of it. Even as a technical person, it is very easy to forget to resize that giant screenshot or camera image you popped into a folder as a placeholder.

Currently behind a flag in Chrome are features which can help. The idea behind these features is to highlight the problematic images so that they can be fixed &mdash; without completely breaking the site.

The `unsized-media` feature policy looks for images or video which do not have a size set in the HTML or CSS. When an unsized media element loads, it can cause the content on the page to reflow.

In order to prevent any unsized media being added to the site, set the following header. Media will then be displayed with a default size of 300&times;150 pixels. You will see your site loading with small media, and realize you have a problem to fix.

<pre><code class="language-html">Feature-Policy: unsized-media 'none'
</code></pre>

[See a demo](https://feature-policy-demos.appspot.com/unsized-media.html?on) (needs Chrome Canary with Experimental Web Platform Features on).

The `oversized-images` feature policy checks to see that images are not much large than their container. If they are, a placeholder will be shown instead. This policy is incredibly useful to check that you are not sending huge desktop images to your mobile users.

<pre><code class="language-html">Feature-Policy: oversized-images 'none'
</code></pre>

[See a demo](https://feature-policy-demos.appspot.com/oversized-images.html?on) (needs Chrome Canary with Experimental Web Platform Features on).

The `unoptimized-images` feature policy checks to see if the data size of images in bytes is no more than 0.5x bigger than its rendering area in pixels. If this policy is enabled and images violate it, a placeholder will be shown instead of the image.

<pre><code class="language-html">Feature-Policy: unoptimized-images 'none'
</code></pre>

[See a demo](https://feature-policy-demos.appspot.com/unoptimized-images.html?on) (needs Chrome Canary with Experimental Web Platform Features on).

## Testing And Reporting On Feature Policy

Chrome DevTools will display a message to inform you that certain features have been blocked or enabled by a Feature Policy. If you have enabled Feature Policy on your site, you can check that this is working.

Support for Feature Policy has also been added to the [Security Headers](https://securityheaders.com) site, which means you can check for these along with headers such as Content Security Policy on your site &mdash; or other sites on the web.

There is a [Chrome DevTools Extension](https://chrome.google.com/webstore/detail/feature-policy-tester-dev/pchamnkhkeokbpahnocjaeednpbpacop) which lets you toggle on and off different Feature Policies (also a great way to check your pages without needing to configure any headers).

If you would like to get into integrating your Feature Policies with the Reporting API, then there is further information in terms of how to do this [here](https://github.com/WICG/feature-policy/blob/master/reporting.md).

### Further Reading And Resources

I have found a number of resources, many of which I used when researching this article. These should give you all that you need to begin implementing Feature Policy in your own applications. If you are already using Content Security Policy, this seems an additional logical step towards controlling the way your site works with the browser to help ensure the security and privacy of people using your site. You have the added bonus of being able to use Feature Policy to help you keep on top of performance-damaging elements being added to your site over time.

- [Feature Policy Specification](https://wicg.github.io/feature-policy/)
- [Introducing Feature Policy](https://developers.google.com/web/updates/2018/06/feature-policy)
- [View from Chrome Dev Summit](https://www.youtube.com/watch?v=igHvSUrLqXc)
- [Feature Policy on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Feature-Policy)
- [Can I Use Feature Policy](https://caniuse.com/#feat=feature-policy)
- [Feature Policy Demos](https://feature-policy-demos.appspot.com/)
- [Set up Feature-Policy, Referrer-Policy and Content Security Policy headers in Nginx](https://fearby.com/article/set-up-feature-policy-referrer-policy-and-content-security-policy-headers-in-nginx/)

{{< signature "il" >}}
