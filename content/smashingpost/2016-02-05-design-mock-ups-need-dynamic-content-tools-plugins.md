---
title: 'Design Mock-Ups Need Dynamic Content: Tools And Plugins'
slug: design-mock-ups-need-dynamic-content-tools-plugins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc4d232-b5a8-453c-a52f-048e9f8d0772/dynamic-content-opt.png
date: 2016-02-05T20:37:49.000Z
author: vitaly-friedman
description: >-
  Nothing is perfect on the web. We can't make sure that our websites always
  work as intended, but we can try our best to design resilient and flexible
  websites that aren't _that_ easy to break — both in terms of interface
  design and security. Yet neither
  resilience nor flexibility are usually reflected in our deliverables and
  mock-ups.
categories:
  - Tools
  - Design
  - Resources
  - Content Strategy
---
<strong>Nothing is perfect on the web.</strong> We can't make sure that our websites always work as intended, but we can try our best to design resilient and flexible websites that aren't <em>that</em> easy to break — both in terms of <a href="https://scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack">interface design</a> and <a href="https://httpsecurityreport.com/best_practice.html">security</a>. Yet still neither resilience nor flexibility are usually reflected in deliverables and mock-ups.</p>

<figure><a href="https://vimeo.com/120804557"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a0521b9-843b-4af3-ba78-deafcc42170e/designing-using-data-opt.png" alt="Designing Using Data" /></a><figcaption><a href="https://vimeo.com/120804557">Designing Using Data</a>, in which Sarah Parmenter discusses how to design with content structure alone.</figcaption></figure>

In practice, mock-ups usually represent a <strong>perfect experience in a perfect context</strong> with perfect data which doesn't really exist. A good example for it are “optimal" usernames which are perfectly short, fit on a single line on mobile and wrap nicely, or perfect photography that allows for perfectly legible text overlays. It's not realistic. We need to work with <a href="https://bradfrost.com/blog/post/designing-with-dynamic-content/">dynamic content</a> in our prototypes, with both average and extremes being represented.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Optimizing Your Design For Rapid Prototype Testing](https://www.smashingmagazine.com/2015/12/optimizing-your-design-for-rapid-prototype-testing/)
*   [Content-First Prototyping](https://www.smashingmagazine.com/2016/05/content-first-prototyping/)
*   [Content Prototyping In Responsive Web Design](https://www.smashingmagazine.com/2011/09/content-prototyping-in-responsive-web-design/)
*   [Resurrecting User Interface Prototypes](https://www.smashingmagazine.com/2010/05/resurrecting-user-interface-prototypes-without-creating-zombies/)

{{% feature-panel %}}

Now, of course usually we don't have the content when we're designing, but it's enough to have the <a href="https://vimeo.com/120804557">content structure</a> (video) to design an experience around it. It's extremely helpful to know whether you should be expecting regular text paragraphs or many tabbed widgets or quite a few complex tables or a complex magazine layout with pullquotes and indented ads. This knowledge alone helps guide design decisions.

In all of those cases, a good strategy would be to use <a href="https://github.com/Heydon/forceFeed">Forcefeed.js</a> to populate our content areas with random content — sometimes too lengthy, sometimes too short, often with accent characters and perhaps even emojis.</p>

<figure><a href="https://github.com/marmelab/gremlins.js"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91909c97-3e3b-4ab4-8415-9fce2c6ce434/unleashing-gremlins-content-test.gif" width="500" height="332" /></a><figcaption><a href="https://github.com/marmelab/gremlins.js">Gremlins.js</a> helps you check the robustness of websites by "unleashing a horde of undisciplined gremlins".</figcaption></figure>

Another tool is <a href="https://github.com/marmelab/gremlins.js">Gremlins.js</a>, a monkey testing library that helps you check the robustness of web applications by "unleashing a horde of undisciplined gremlins", i.e. it generates random data strings and types them in all over the place to test how a website responds. If you want to have a more controlled testing, you can also use the <a href="https://css-tricks.com/prefilling-forms-custom-bookmarklet/">Prefill Forms Bookmarklet</a> which allows you to predefine a set of templates to be submitted into forms to test its resilience.</p>

<figure><a href="https://css-tricks.com/prefilling-forms-custom-bookmarklet/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bd9d759-1c49-4a13-bd95-332dd7079041/cast.gif" /></a><figcaption><a href="https://css-tricks.com/prefilling-forms-custom-bookmarklet/">Prefill Forms Bookmarklet</a> lets you plug in pre-defined content snippets to check your web forms.</figcaption></figure>

We need to craft future-proof experiences, too. What if your interface design would need to be translated into other languages? While Chinese might be perfectly short and concise, German might turn out to create awkwardly long interface components, ranging from buttons to navigation. In this case, something as simple as <a href="https://blog.jquery.com/2015/04/23/announcing-globalize-1-0/">jQuery Globalize plugin</a>, or <a href="https://github.com/kristof/sketch-i18n">Sketch i18n plugin</a> could be helpful.

You can define dynamic variables for your content and "plug them in" quickly, to verify that the layout doesn't break when the language changes. For Sketch, you can also use <a href="https://sketch.land/content/">Content Generation Plugins</a>, ranging from importing financial data to random user profile images. And if you use Photoshop, <a href="https://stackoverflow.com/questions/700792/automate-photoshop-to-insert-text-from-file">there are ways to insert content into Photoshop from a text file</a>, too. Also, <a href="https://labs.invisionapp.com/craft">Craft</a> is a free plugin suite for Sketch and Photoshop that lets you design with real data, too.

We use these little helpers all the time, and they prove to be great tools to build websites that are <strong>prepared for everything</strong> that comes their way. They also reflect reality much better than perfect mock-ups with perfect heights and perfect names and email addresses ever would. Stay resilient — that's the true power of the web.

{{< signature "vf, cm" >}}

