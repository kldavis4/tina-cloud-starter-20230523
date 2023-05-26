---
title: 'Equivalent Experiences: Thinking Equivalently'
slug: equivalent-experiences-part2
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa9e210-0f75-4e54-b273-705c55bc36a2/equivalent-experiences-part2.png
date: 2020-06-05T12:00:00.000Z
summary: >-
  Constructing an equivalent experience may mean changing the way you think about development and design, and potentially reevaluating your existing work. In this article, we’ll address common accessibility issues, and how to best go about improving them so everyone can effortlessly access your content.
description: >-
  Constructing an equivalent experience may mean changing the way you think about development and design, and potentially reevaluating your existing work. In this article, we’ll address common accessibility issues, and how to best go about improving them so everyone can effortlessly access your content.
categories:
  - Accessibility
  - Design
  - UX
---

This is the second of two articles on the topic of how digital accessibility is informed by equivalency. [Previously](https://www.smashingmagazine.com/2020/05/equivalent-experiences-part1/), we have learned about the underlying biases that inform digital product creation, what isn’t an equivalent experience, the compounding effects of inaccessible design and code, and powerful motivating forces for doing better.

In this article, I will discuss learning how to embrace an equivalent, inclusive mindset. I will also provide practical, robust ways to improve your websites and web apps by providing solutions to common, everyday barriers cited by the people I interviewed.

## Setting A Standard

[The Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/) outlines in painstaking detail how to craft accessible digital experiences. While a long and dense document, it is incredibly comprehensive &mdash; to the point where it’s been [codified as an international standard](https://www.iso.org/standard/58625.html). For over 10 years, we’ve had a globally agreed upon, canonical definition of what constitutes as usable.

### How Would I?

If you need a little help constructing the initial mental framework the WCAG gets at, a question I always ask myself when making something is, “How would I use this if…” It’s a question that gets you to check [all the biases](https://en.m.wikipedia.org/wiki/List_of_cognitive_biases) that might be affecting you in the moment.

Examples could be:

<ul>
	<li>How would I use this if...</li>
	<ul>
		<li>...I can’t see the screen?</li>
		<li>...I can’t move my arms?</li>
		<li>...I’m sensitive to flashing and strobing animation?</li>
		<li>...English isn’t my primary language?</li>
		<li>...I have a limited budget for bandwidth?</li>
		<li>...I’ve set a large default type size?</li>
		<li>...and so on.</li>
	</ul>
</ul>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Focus on these four parameters to improve usability of your web design:<br><br>1. Visual - make it easy to see<br>2. Auditory - make it easy to hear<br>3. Motor - make it easy to interact with<br>4. Cognitive - make it easy to understand<br><br>→ Accessibility goals are also usability goals.</p>&mdash; Alex 🌚 (@alexmuench) <a href="https://twitter.com/alexmuench/status/1222844524671664129?ref_src=twsrc%5Etfw">January 30, 2020</a></blockquote>

### A Gentle Introduction

If you’re looking for a more approachable resource for how to dig into what the WCAG covers, the [Inclusive Design Principles](https://inclusivedesignprinciples.org/) would be a great place to start. The seven principles it describes all map back to [WCAG success criterion](https://www.w3.org/WAI/WCAG21/Understanding/conformance#levels).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce7e445-5059-4193-b3d0-1a1854d3be32/equivalent-experiences-inclusive-design-principles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce7e445-5059-4193-b3d0-1a1854d3be32/equivalent-experiences-inclusive-design-principles.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce7e445-5059-4193-b3d0-1a1854d3be32/equivalent-experiences-inclusive-design-principles.png'>Large preview</a>)" alt="Screenshot of the top portion of the Inclusive Design Principles website. It includes a simple illustration of three hot air balloons floating in front of a cloud and sun. It also has the intro paragraph, “These Inclusive Design Principles are about putting people first. It’s about designing for the needs of people with permanent, temporary, situational, or changing disabilities — all of us really.” The contributors are listed as Henny Swan, Ian Pouncey, Heydon Pickering, and Léonie Watson" >}}

{{% feature-panel %}}

## Learn From The People Who Actually Use It

You don’t have to take my word for it. Here are some common issues cited by the people I interviewed, and how to fix them:

### Wayfinding

#### Headings

Heading elements are incredibly important for maintaining an equivalent, accessible experience.

When [constructed with skill and care](https://webdesign.tutsplus.com/articles/the-importance-of-heading-levels-for-assistive-technology--cms-31753), heading elements allow screen reader users to quickly determine the contents of a page or view and navigate to content relevant to their interests. This is equivalent to [how someone might quickly flit around](https://www.nngroup.com/articles/how-people-read-online/), scrolling until something that looks pertinent comes into view.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5b4856e-480c-4d79-8b0e-b80db474c4df/equivalent-experiences-headings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5b4856e-480c-4d79-8b0e-b80db474c4df/equivalent-experiences-headings.png" sizes="100vw" caption="The <a href='https://www.learningapps.co.uk/moodle/xertetoolkits/play.php?template_id=1309#page1'>HeadingsMap browser extension</a> lets you view a page’s heading hierarchy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5b4856e-480c-4d79-8b0e-b80db474c4df/equivalent-experiences-headings.png'>Large preview</a>)" alt="A graphic showing how nested heading elements correspond to the layout of a design for a site called SkyList. The first level heading is “Types of Clouds,” which maps to the page’s h1 element. The three h2 heading elements read, “High,” “Mid-level,” and “Low.” Each of these headings is represented in the design as a shaded area. Within each area are card designs, including an image placeholder, a title, and a paragraph placeholder. The h3 heading elements for the High section cards are “Cirrus,” “Cirrostratus,” and “Cirrocumulus.” The h3 heading elements for the Mid-level section cards are “Altocumulus,” “Altostratus,” and “Nimbostratus.” The h3 heading elements for the Low section cards are “Cumulus,” “Stratus,” “Cumulonimbus,” and “Stratocumulus.”" >}}

[Justin Yarbrough](https://twitter.com/FatElvis04) voices poorly-authored heading elements as a concern, and he’s not alone.

[WebAIM’s screen reader survey](https://webaim.org/projects/screenreadersurvey8/#finding) cites headings as the most important way to find information. This survey is well-worth paying attention to, as it provides valuable insight into how disabled people actually use assistive technology.

#### Landmarks

In addition to heading elements, another way to determine the overall structure and layout are [landmarks](https://www.scottohara.me/blog/2018/03/03/landmarks.html). Landmarks are roles implicitly described by [HTML sectioning elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Content_sectioning), used to help describe the overall composition of the main page or view areas.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f207bf7-1ceb-48d5-9446-362508657077/equivalent-experiences-landmarks.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f207bf7-1ceb-48d5-9446-362508657077/equivalent-experiences-landmarks.png" sizes="100vw" caption="These are five of the eight landmark HTML elements and the roles using them create. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f207bf7-1ceb-48d5-9446-362508657077/equivalent-experiences-landmarks.png'>Large preview</a>)" alt="A ‘holy grail’ layout showing a header element row stretching across three columns. Below that is another row with three columns, using nav, main, and aside elements. Below that is a third and final column-stretching row  using the footer element. Each element is also labeled with its corresponding landmark." >}}

Here’s what Justin has to say:

<blockquote>“If I’m just trying to find the main content, I’ll first try the <kbd>Q</kbd> JAWS shortcut key to see if a <code>main</code> region’s set up. If not, I’m just more or less stuck trying to scan the page to find it arrowing through the page.”</blockquote>

Much as how we might use a layer group name of “primary nav” in our design file, or a class name of `c-nav-primary` in our CSS, it’s important we also use a [`nav` sectioning element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav) to describe our main site navigation (as well as any other navigation the page or view contains).

Doing so ensures intent is carried all the way through from conception, to implementation, to use. The same notion carries through for [the other HTML sectioning elements that create landmarks](https://www.w3.org/TR/wai-aria-practices/examples/landmarks/HTML5.html) for assistive technology.

### Labeled Controls

[Brian Moore](https://twitter.com/bmoore123) tells us about “form fields with no label or at least one that isn’t programmatically associated so it doesn’t read anything.”

It’s another [frustratingly common problem](https://webaim.org/projects/million/#labels).

Providing a valid `for`/`id` attribute pairing creates a programmatic association between [form inputs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Forms) and [the label that describes what it does](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label). And when I say `label`, I mean the `label` element. Not a clickable `div`, a [placeholder](https://www.smashingmagazine.com/2018/06/placeholder-attribute/), `aria-label`, or some other [brittle and/or overwrought solution](https://www.matsuko.ca/blog/stop-using-material-design-text-fields/). `label` elements are a tried-and-true solution that enjoys [wide and deep support](https://a11ysupport.io/tech/html/label_element) for accessibility.

In addition, a `label` element should not be used by itself, say for a label on a diagram. This might seem counter-intuitive at first, but please bear with me.

<div class="break-out">

 <pre><code class="language-css">&lt;!-- Please do this --&gt;
&lt;label for="your-name"&gt;Your name&lt;/label&gt;
&lt;input type="text" id="your-name" name="your-name" autocomplete="name"&gt;

&lt;!-- Don’t do this --&gt;
&lt;label for="eye"&gt;Cornea&lt;/label&gt;
&lt;label for="eye"&gt;Pupil&lt;/label&gt;
&lt;label for="eye"&gt;Lens&lt;/label&gt;
&lt;label for="eye"&gt;Retina&lt;/label&gt;
&lt;label for="eye"&gt;Optic Nerve&lt;/label&gt;
&lt;img id="eye" alt="A diagram of the human eye." src="parts-of-the-eye.png" /&gt;
</code></pre>
</div>

The same kinds of assistive technology that let a person jump to headings and landmarks also allow them to jump to input labels. Because of this, there is the expectation that when a `label` element is present, there is also a corresponding input it is associated with.

### Alternative Descriptions

If you have low or no vision, and/or have difficulty understanding an image, [HTML’s alt attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-alt) (and not [the title attribute](https://developer.paciellogroup.com/blog/2013/01/using-the-html-title-attribute-updated/)) provides a mechanism to understand what the image is there for. The same principle applies for providing captions for video and audio content like [podcasts](https://thisten.co/).

[Kenny Hitt](https://twitter.com/hittsjunk) mentions that when:

<blockquote>“…someone posts something on Twitter, if it’s just an unlabeled image, I don’t even take the time to participate in the conversation. When you start every conversation by asking what’s in the picture, it really derails things.”</blockquote>

[Up until last week](https://twitter.com/TwitterA11y/status/1265689579371323392), the only way for Twitter to [provide alternative descriptions for its images](https://adrianroselli.com/2016/03/twitter-has-alt-text-with-some-caveats.html) was to enable an option buried away in the subsection of a preference menu. Compare this to a platform like [Mastodon](https://joinmastodon.org/), where the feature is enabled by default.

<figure class="video-container break-out"><iframe loading="lazy" src="https://www.youtube.com/embed/EXYPYXZq7uI" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

[Soren Hamby](https://linktr.ee/uxicorn), mentions [Stitcher](https://www.stitcher.com/), a popular podcast app. “The onboarding was a lot of themed graphics, but the alt text for each one was ‘unselected’ and for the same image with a check over it was selected. I think it would be reasonable for them to say ‘sci-fi genre selected’ […] it’s such a small thing but it makes all the difference.”

Ensuring that alternate description content is concise and descriptive is just as important as including the ability to add it. [Daniel Göransson](https://twitter.com/danielgoransson), a developer for [Axess Lab](https://axesslab.com/), has a [great article on how to write them effectively](https://axesslab.com/alt-texts/).

Robust, accessible features can also be part of evaluation criteria, as well as a great method for building customer loyalty. Soren mentions that they are “often the deciding factor, especially between services.” In particular, they cite Netflix’s audio descriptions.

{{% ad-panel-leaderboard %}}

### ARIA

One topic Daniel Göransson’s article on alternative descriptions mentions is to not over-describe things. This includes information like that it is an image, who the photographer is, and keyword stuffing.

The same principle applies for [Accessible Rich Internet Applications (ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/). ARIA is a set of attributes designed to extend HTML to fill in the gaps between interactive content and assistive technology. When ARIA is used to completely replace HTML, it oftentimes leads to an over-described experience.

Brian explains: “There seems to be a perception that more ARIA fixes accessibility and it can help, but too much either reads wrong things or just talks way too much. If on screen text of one or two words is good enough for everyone else, it is good enough for screen reader users too. We don’t need whole sentence or two descriptions of buttons or links i.e ‘link privacy policy’ is far better than something like ‘this link will open our privacy policy, this link will open in a new window’ when the on screen link text is ‘privacy policy.’”

[The First Rule of ARIA Use](https://www.w3.org/TR/using-aria/#rule1) advises us to only use it when a native element won’t suffice. [You don’t need to describe what your interactive component is](https://adrianroselli.com/2019/10/stop-giving-control-hints-to-screen-readers.html) or how it works, the same way you don’t need to include the word “image” in your alternative description.

Provided that you use the appropriate native HTML element, assistive technology will handle all of that for you. Do more, more robustly, with less effort? Sounds great to me!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbac946-6e41-4cb5-b10f-f7bc7b9ee2bf/equivalent-experiences-code-to-at-diagram.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbac946-6e41-4cb5-b10f-f7bc7b9ee2bf/equivalent-experiences-code-to-at-diagram.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbac946-6e41-4cb5-b10f-f7bc7b9ee2bf/equivalent-experiences-code-to-at-diagram.png'>Large preview</a>)" alt="A code sample of an anchor element wrapping an image, with an alt description that reads, “A cat wearing a party hat.” Arrows from the HTML elements and attributes point towards how everything combines to create a phrase spoken aloud by a screen reader. The phrase reads, “Link. Image. A cat wearing a party hat." >}}

Unlike most of HTML, CSS, and JS, the success of implemented ARIA is contextual, variable, and largely invisible. In spite of this, we seem to be [slathering ARIA onto everything](https://css-tricks.com/aria-spackle-not-rebar/) without bothering to check not only if it actually works, but also [what the people who actually use it think of it](https://www.gatsbyjs.org/blog/2019-07-11-user-testing-accessible-client-routing/).

[Support for ARIA](https://a11ysupport.io/) is fragmented across operating systems, browsers, and assistive technology offerings, all their respective versions, and every possible permutation of all three. Simply put, writing ARIA and trusting it will work as intended isn’t enough.

If misconfigured and/or over-applied, [ARIA can break](https://a11yproject.com/posts/aria-has-perfect-support/). It may not report actual functionality, announce the wrong functionality, and (accurately or inaccurately) over-describe functionality. Obviously, these experiences aren’t equivalent.

[Representation matters](https://en.m.wikipedia.org/wiki/Nothing_About_Us_Without_Us). To get a better understanding of how the ARIA code you wrote actually works, I recommend hiring people to tell you. Here are four such services that do exactly that:

- [Accessible360](https://accessible360.com/)
- [AccessWorks (by Knowbility)](https://access-works.com/)
- [Fable Tech Labs](https://www.makeitfable.com/)
- [Perkins School For The Blind](https://www.perkins.org/services/other)

{{% ad-panel-leaderboard %}}

### Contrast

#### Color Contrast

Color contrast is another common issue, one whose severity often seems to be downplayed. If I could wager a guess, it’s because it’s easy to forget that other people’s vision might be different than your own. Regardless, it is a concern that affects [a wide swath of the global population](https://www.who.int/news-room/fact-sheets/detail/blindness-and-visual-impairment), and we should treat the issue with the seriousness it deserves.

The Click-Away Pound Survey tells us that out of the top issues faced by users with access needs, contrast and legibility weighs in as the fifth most significant issue. On top of that, it has *increased* as a concern, going from 44% of respondents in 2016 to 55% in 2019.

We live in an age where there’s more color contrast checking resources than I can count. Products like [Stark](https://www.getstark.co/) can help designers audit their designs before it is translated into code. Tools like [Eightshape’s Contrast Grid](https://contrast-grid.eightshapes.com/) and [Atul Varma’s Accessible color palette builder](https://toolness.github.io/accessible-color-matrix/) let you craft your design systems with robust, accessible color combinations out of the gate.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0c224c0-8588-491d-b641-bffb0cfe1928/equivalent-experiences-side-by-side-comparison.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0c224c0-8588-491d-b641-bffb0cfe1928/equivalent-experiences-side-by-side-comparison.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0c224c0-8588-491d-b641-bffb0cfe1928/equivalent-experiences-side-by-side-comparison.png'>Large preview</a>)" alt="A side-by-side comparison demonstrating acceptable and bad color contrast ratios. The first example shows black text on a dark yellow background, with a passing contrast ratio of 9.89:1. The second example shows light gray text on a light blue background, with a failing contrast ratio of 2.13:1. The text for both examples reads, “The lighting collection ranges from timeless classics to contemporary designs that make for perfect additions to any home and space.”" >}}

The somewhat ironic thing about color contrast is how, ah, visible it is. While some of the previous accessibility issues are invisible—hidden away as the underlying code—contrast is a pretty straightforward issue.

Mostly, contrast is a binary scenario, in that you either can or cannot see content. So, the next time you check your website or webapp with an automated accessibility checker such as [Deque’s axe](https://www.deque.com/axe/), don’t be so quick to downplay the color contrast errors it reports.

#### High Contrast

There are technology solutions for situations where even satisfactory color contrast ratios isn’t sufficient—namely, [inverted colors mode](https://a11yproject.com/posts/operating-system-and-browser-accessibility-display-modes/#inverted-colors-mode) and [High Contrast Mode](https://a11yproject.com/posts/operating-system-and-browser-accessibility-display-modes/#high-contrast-mode). Many participants I interviewed mentioned using these display modes during their daily computer use.

Provided you use semantic HTML, both of these modes [don’t need much effort on the development end of things](https://www.gwhitworth.com/blog/2017/04/how-to-use-ms-high-contrast/) to work well. The important bit is to check out what you’re building in these two modes to make sure everything is working as intended.

## Striving For Perfection

To quote [Léonie Watson](https://tink.uk/),

<blockquote>“Accessibility doesn’t have to be perfect, it just needs to be a little bit better than yesterday.”</blockquote>

By understanding both why, and how to improve your digital accessibility experiences in ways that directly address common barriers, you’re able to provide meaningful and enjoyable experiences to all.

### Further Reading

- [Accessibility For Teams](https://accessibility-for-teams.com/) (a project by [Peter van Grieken](https://twitter.com/petervangrieken))
- “[One Of My Favourite Accessibility Testing Tools: The Tab Key](https://www.matuzo.at/blog/testing-with-tab/),” Manuel Matuzović
- “[These Are The Web Accessibility Standards Designers Need To Know](https://thenextweb.com/syndication/2020/03/14/these-are-the-web-accessibility-standards-designers-need-to-know-syndication/),” Yichen He, The Next Web
- “[Web Accessibility Standards: An Overview For Designers](https://uxdesign.cc/web-accessibility-standards-an-overview-for-designers-1a4d39f2fe5e),” Yichen He, UX Collective
- “[What A Year Of Learning And Teaching Accessibility Taught Me](https://www.24a11y.com/2019/what-a-year-of-learning-and-teaching-accessibility-taught-me/),” Sara Soueidan , 24 Accessibility

*Thank you to Brian Moore, Damien Senger, Jim Kiely, Justin Yarbrough, Kenny Hitt, and Soren Hamby for sharing their insights and experiences.*

<script defer  src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

{{< signature "ra, il" >}}
