---
title: 'Making Accessibility Simpler, With Ally.js'
slug: making-accessibility-simpler
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f735e00-89f1-40ae-9724-0f3d1d3e2a83/01-ally-js-logo-opt.png
date: 2015-12-12T02:08:41.000Z
author: rodney-rehm
description: >-
  I’ve been a web developer for 15 years, but I’d never looked into
  accessibility. I didn’t know enough people with (serious) disabilities to
  properly understand the **need for accessible applications** and no customer
  has _ever_ required me to know what ARIA is. But I got involved with
  accessibility anyway – and that’s the story I’d like to share with you today.

  At the Fronteers Conference in October 2014 I saw Heydon Pickering give a talk
  called “Getting nowhere with CSS best practices”. Among other things, he made
  a case for using WAI-ARIA attributes like `aria-disabled="true"` instead of
  classes like `.is-disabled` to express application state. It struck me then
  and there that I was missing out on a few well-prepared standards, simply
  because ARIA belongs to that accessibility space that I had no idea of.
categories:
  - Coding
  - JavaScript
  - Accessibility
---
I’ve been a web developer for 15 years, but I’d never looked into accessibility. I didn’t know enough people with (serious) disabilities to properly understand the <strong>need for accessible applications</strong> and no customer has <em>ever</em> required me to know what ARIA is. But I got involved with accessibility anyway – and that’s the story I’d like to share with you today.

At the <em>Fronteers Conference</em> in October 2014 I saw <a href="https://heydonworks.com/">Heydon Pickering</a> give a talk called “<a href="https://fronteers.nl/congres/2014/sessions/heydon-pickering-getting-nowhere-with-css-best-practices">Getting nowhere with CSS best practices</a>”. Among other things, he made a case for using <a href="https://w3c.github.io/aria/aria/aria.html">WAI-ARIA</a> attributes like <code>aria-disabled="true"</code> instead of classes like <code>.is-disabled</code> to express application state. It struck me then and there that I was missing out on a few well-prepared standards, simply because ARIA belongs to that accessibility space that I had no idea of.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)
*   [Accessibility: Improving The UX For Color-Blind Users](https://www.smashingmagazine.com/2016/06/improving-ux-for-color-blind-users/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [Accessibility: Improving The UX For Color-Blind Users](https://www.smashingmagazine.com/2016/06/improving-ux-for-color-blind-users/)

After talking to Heydon a bit more I finally understood that ARIA could help me write web applications without having to <a href="https://en.wikipedia.org/wiki/Parkinson's_law_of_triviality">bike-shed</a> class names for various states (is the thing disabled, is it visible, is it still loading…). The discussion did not touch on accessibility at all – we were simply talking about how to make web development a tiny bit simpler.

{{% feature-panel %}}

I decided I needed to dig into ARIA – honestly not because I deeply cared about accessibility, but because I had no intention of reinventing the wheels they already had. One of the first things you’ll learn when looking at ARIA is that <strong>supporting keyboard navigation is fundamental</strong>. And the first step to understanding keyboard navigation is to understand what <em>focus</em> is. And this is where I tripped, because nobody knew (in detail) which elements could receive focus and which could not.

Having had a bit of experience testing browser compatibility (“<a href="https://www.smashingmagazine.com/2013/04/26/css3-transitions-thank-god-specification/">CSS3 Transitions: Thank God We Have A Specification!</a>”), I decided I would spend some time investigating. An ebook covering my findings is in the works and will be ready to make you lose focus in early 2016. But more importantly, the JavaScript variant of that book is available today:

<figure><a href="https://allyjs.io"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb9ed8fc-58eb-46af-96ad-f3ab049fb01a/allyjs-logo-opt.png" alt="Making Accessibility Simpler" /></a><figcaption><a href="https://allyjs.io">ally.js</a> is a JavaScript library to help modern web applications with accessibility concerns by making accessibility simpler.</figcaption></figure>

## ally.js Highlights

Before we get into why and how this project came to be, here’s a short list of things it can help you with:

*   ally.js fixes browser bugs concerning `:focus` in [Internet Explorer](https://allyjs.io/api/fix/pointer-focus-children.html) and [WebKit](https://allyjs.io/api/fix/pointer-focus-parent.html).
*   ally.js provides high-level tools to [disable interactive elements](https://allyjs.io/api/maintain/disabled.html) and [hide entire branches](https://allyjs.io/api/maintain/hidden.html) of the DOM from screen readers.
*   ally.js provides a simple way to [prevent browsers from scrolling an element into view](https://allyjs.io/api/when/focusable.html) when it’s about to be focused.
*   ally.js helps styling `:focus` by providing a [`:focus-within` polyfill](https://allyjs.io/api/style/focus-within.html) and the ability to [distinguish mouse focus from keyboard focus](https://allyjs.io/api/style/focus-source.html).
*   ally.js not only helps you understand which elements are [focusable](https://allyjs.io/api/query/focusable.html) and which are [keyboard-focusable](https://allyjs.io/api/query/tabbable.html), but also the [tabbing order](https://allyjs.io/api/query/tabsequence.html).

ally.js includes a few shims and a polyfill but does not have any major dependencies. It’s designed to be compatible: UMD, AMD, CommonJS, ES6, modules or bundled – <a href="https://allyjs.io/getting-started.html">it’s your choice</a>.</p>

### Show Me Some Code!

When making your application keyboard accessible, it is important to hide elements from the keyboard that can currently not be interacted with. This may be the case when a modal dialog is visible, or the off-screen menu is shown. We can easily disable <em>everything</em> outside of our dialog:

<pre><code class="language-javascript">// disable everything that is not a child of #our-dialog
var handle = ally.maintain.disabled({
  filter: '#our-dialog',
});
// re-enable everything that we disabled previously
handle.disengage();
</code></pre>

The same principle is true for any content (not just the interactive kind) to <strong>make sure screen reader users don’t get lost</strong>. We can easily hide <em>everything</em> outside of our dialog:

<pre><code class="language-javascript">// hide everything that is not a child of #our-dialog by adding aria-hidden="true"
var handle = ally.maintain.hidden({
  filter: '#our-dialog',
});
// re-enable everything that we disabled previously
handle.disengage();
</code></pre>

Sometimes we need to act on specific keys like <kbd>Enter</kbd> and <kbd>Escape</kbd>:

<pre><code class="language-javascript">
var handle = ally.when.key({
  enter: function(event) {
    // handle the enter event
  },
  escape: function(event, disengage) {
    // handle the escape event…
    disengage();
  },  
});
// stop listening for keys
handle.disengage();
</code></pre>

## Motivation

Let’s have a look at why I thought it was necessary to create something new in the first place. While there are various reasons, these are the important ones:

1.  Many (especially older) articles sport code examples and approaches that are not easily comprehensible and promote coding practices that by today’s standards would be considered harmful.
2.  Even the good articles usually only focus on accessibility, ignoring everything else that’s relevant to creating compelling websites and applications.
3.  Literally no articles and resources _share_ code. There doesn’t seem to be much collaboration (on code) outside of individual projects, leading to the same thing being coded over and over again.
4.  Many problems don’t seem well understood, or not considered a problem to begin with.
5.  In a few aspects accessibility feels undeterministic. In virtually all cases concerning semantics we’re in a state that feels like the early 2000s: you might have created something conforming to standards, but that doesn’t mean it works everywhere – or even anywhere at all.

In the end I felt like we were missing a proper toolbox. Like <a href="https://jquery.com/">jQuery</a> is to conquering the DOM without having to care much about browser compatibility, be they gaping holes or subtle bugs. Like <a href="https://d3js.org/">D3</a> is to conquering interactive data visualization. Or like RaphaelJS was to conquering SVG only a few years ago. I couldn’t find anything similar that would do the heavy lifting for accessibility, at least nothing comprehensive and framework-independent.</p>

## Execution

I have a few principles that guide the way I work:

1.  If you don’t understand the problem, you’re not creating solutions. Research is key.
2.  Start small, build over time.
3.  Complex solutions don’t change the world. Simplicity is key.
4.  One person can only do so much. Collaboration is key.</p>

### Research Is Key

Before you can write a single line of code to do something, you should have a pretty good idea what that line of code is supposed to do. If you only solve the problem at hand, you’re likely missing the bigger picture. Without the bigger picture in front of you, <strong>creating lasting solutions</strong> is incredibly hard, if not next to impossible.

Once I realized that neither I nor the internet was able to answer the simple question of which elements can take focus, there was only one option left: rolling up my sleeves and figuring out what browsers actually do. This led to a <a href="https://allyjs.io/data-tables/focusable.html">compatibility table</a> detailing what browsers consider focusable, a <a href="https://allyjs.io/tests/focus-outline-styles/index.html">comparison of focus styles</a> and <a href="https://github.com/medialize/ally.js/blob/master/issues.md#issues-filed">a slew of filed bugs</a>.</p>

### Start Small

Throughout the past 14 months I managed to keep <strong>focus on keyboard navigation</strong>. Not losing myself – or the library – in too much of ARIA’s semantics. Doing one thing and not starting anything new until you’re done isn’t easy, especially not while you’re learning a dozen new tricks a day.

Starting small also meant limiting browser scope. I didn’t need older Internet Explorer and Android browsers, so version 1.0.0 doesn’t support anything below IE10 and Android 4.4. Version 1.1.0 will add support for IE9, a reasonable second step.</p>

### Simplicity Is Key

If you want people to use your tools, you need to make sure that your <strong>tool makes sense to them</strong>, preferably without requiring a degree in rocket science. But how do you hide a tool’s internal complexity to make it seemingly simple?

*   Provide a consistent and memorable API.
*   Provide documentation that not only explains how to use a feature, but why it’s necessary in the first place.
*   Meticulously expose all edge cases in the documentation to prevent people from having to debug _your_ code.
*   Make consuming your tool a breeze. AMD and CommonJS can be generated from ES6\. Modules can be bundled and exposed as [UMD](https://github.com/umdjs/umd/#umd-universal-module-definition).
*   Provide tutorials that explain how your tool’s features work together to solve particular problems.
*   Provide ways to quickly experiment with your tool’s features without having to install the internet first.</p>

### Collaboration Is Key

I’ve mustered all my spare time in the past 14 months and threw it at my open source projects. I’m not going to lie to you: it was rough and I’m certain I won’t be able to keep this up. To prevent a one-man-show failure the project will need to find and involve like-minded folks. But collaboration is a multifaceted topic.

The <strong>core contributors</strong> are people who spend time on the project on a regular basis. This is the rarest form of contribution, as it takes the highest commitment. Because of that I’m incredibly happy to welcome <a href="https://twitter.com/marcysutton">Marcy Sutton</a> on board! In <em>many</em> ways Marcy has <em>much more</em> experience in the accessibility world than I do, so her addition to the team is our first big win. To make sure more people can chime in, everything we do is <a href="https://allyjs.io/contributing/index.html">documented</a>.

It’s quite common for people to submit smaller patches to source code and documentation. Because a single person is likely to only contribute a handful of changes, we like to call them <strong>drive-by contributors</strong>. For them it is important to be able to make their changes quickly and safely. That’s why all of the documentation pages have convenient links to open issues, edit pages and point to related resources (source files, documentation, tests).

And then there’s the group of people who aren’t contributing to the project’s code, more so to its success. The <strong>integrators</strong> are very important people, as they’re taking charge in amping up other projects by adding ally.js features to them. Currently we’re talking with the folks of <a href="https://jqueryui.com/">jQuery UI</a> and Angular’s <a href="https://docs.angularjs.org/api/ngAria">ngAria</a> about how to best support their efforts by offloading things to ally.js. A few people from the React community have already voiced an interest as well.

Everything we do within the ally.js space has the intention of improving the status quo for <em>everyone</em>, even and especially for people <em>not</em> using the library. The browser bugs we’re filing and the discussion around improving our web standards are all based on the research we’re doing to improve the library. However you won’t be surprised to find the library moving <em>much</em> quicker than web standards at large.</p>

## The Future

Of the three columns of accessibility – keyboard support, semantics, and flexible UI – ally.js currently only covers the first. With the insights Marcy brings with her (and maybe a few more minds) we intend to dive into the semantics pillar. Understanding ARIA is one thing, but understanding what browsers and screen readers actually do with it is quite a different story.

We’ll be looking at providing simple APIs for ARIA for your imperative needs. We’ll investigate options to automate enforcing semantics like these “<a href="https://www.sitepoint.com/tips-accessible-svg/">Tips for Creating Accessible SVG</a>” at runtime and within your build process.

We’ll be looking at how to enhance your use of ARIA by providing you with extended keyboard support for common widgets (like the <a href="https://www.w3.org/WAI/PF/aria-practices/#Listbox">listbox</a>).</p>

## Conclusion

You can care about accessibility issues without being affected by a disability yourself. In <em>many</em> ways, making your apps and sites accessible benefits <em>everyone</em>. <a href="https://allyjs.io">ally.js</a> helps you accomplish that.

ally.js is positioning itself as a <strong>center for collaborating on accessibility-related features</strong>, by providing low-level tools to other libraries and frameworks as well as high-level functions to developers. If we start working together we might just get somewhere…

{{< signature "vf, ml, og" >}}

