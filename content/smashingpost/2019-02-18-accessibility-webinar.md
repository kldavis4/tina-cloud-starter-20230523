---
title: 'How A Screen Reader User Accesses The Web: A Smashing Video'
slug: accessibility-webinar
author: bruce-lawson
image: >-
  https://res.cloudinary.com/indysigner/image/upload/v1550254365/Webinars/leonie-watson-screenreader-webinar.png
date: 2019-02-18T14:00:32+01:00
summary: >-
  In this Smashing TV webinar recording, join Léonie Watson (a blind screen reader user) as she explores the web, and find out about some unexpected properties of HTML elements that not only have a huge impact on accessibility, but also turn out to be pretty good for performance, too.
description: >-
  In this Smashing TV webinar, join us with Léonie Watson as she explores the web alongside some unexpected properties of HTML elements that have a huge impact on accessibility and performance.
categories:
  - Accessibility
  - Membership
  - Events
  - Smashing TV
disable_ads: true
disable_panels: true
---
Two weeks ago, I had the pleasure of hosting a [Smashing TV](https://www.smashingmagazine.com/smashing-tv/) webinar with Léonie Watson on [how a screen reader user accesses the web](https://www.smashingmagazine.com/smashing-tv/how-a-screen-reader-user-surfs-the-web/). In the talk, Léonie showed some big-name sites, such as BBC, sites nominated by Members (including my own!), Smashing Magazine itself, and the popular third-party service Typeform, because so many of us (including us at Smashing) just assume that the popular services have been checked for accessibility. Throughout, Léonie explained how the sites' HTML was helping (or hindering) her use of the sites.

We felt that the webinar was so valuable that we would open it up so that it’s free for everybody to use. Hopefully, it will serve as a resource for the whole web development community to understand how &mdash; and *why* &mdash; semantic markup matters.

<figure class="video-container"><iframe loading="lazy" width="560" height="315" src="https://www.youtube.com/embed/OUDV1gqs9GA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></figure>

## What We Learned

I was pleased that my [personal site](https://brucelawson.co.uk/)’s use of HTML5 landmark regions (`main`, `nav`, `header`, `footer`, etc) helped Léonie form a mental model of the structure of the page. Although I’ve always been scrupulous to avoid link text like "click here" because [WCAG guidelines](https://www.w3.org/TR/WCAG21/#link-purpose-in-context) require “The purpose of each link can be determined from the link text alone”, it hadn’t occurred to me before that because I have hundreds of weekly “Reading List” articles, it’s impossible for a screen reader user to tell one from the other when navigating by headings. Since the webinar, I’ve made each new reading list’s heading unique by including its number in the heading (“Reading List 222”).

We also learned that being technically accessible is good, but even better is to be *usably* accessible. The Smashing Team learned that before Léonie can read her own article on our site, there’s loads of preamble (author bio, email sign-up form) that she can’t easily skip over. We’re correcting this at the moment. There’s also an issue with our quick summaries; Léonie gets no indication when the summary has finished and the article proper has begun. Sighted users get a dividing line, but what can we do for non-sighted users?

After the webinar, Léonie suggested using a semantic HTML element and a sprinkling of ARIA:

<pre><code class="language-html">&lt;section aria-label="Summary"&gt;
&lt;/section&gt;
</code></pre>

This is announced as "Summary region start" and “Summary region end”, and can be skipped over if desired.

## Thank You!

We'd like to thank Léonie for giving the webinar, and also our magnificant Smashing Magazine members whose support allows us to commission such content, pay our contributors fairly, and reduce advertising on the site.

_Shameless plug: if you enjoyed this webinar, why not consider [becoming a Member](https://www.smashingmagazine.com//membership) yourself? There are around three webinars a month free, Smashing eBooks and discounts galore. It costs around two cups of coffee a month, and you can cancel anytime._

{{< signature "ra, il" >}}