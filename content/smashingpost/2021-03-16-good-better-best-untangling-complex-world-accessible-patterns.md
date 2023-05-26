---
title: 'Good, Better, Best: Untangling The Complex World Of Accessible Patterns'
slug: good-better-best-untangling-complex-world-accessible-patterns
author: carie-fisher
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef0d9c66-0c79-456e-b799-9df8e4692a8b/good-better-best-untangling-complex-world-accessible-patterns.jpg
date: 2021-03-16T12:00:00.000Z
summary: >-
  How do we know which patterns are good, better, best when it comes to accessibility? Is it better to use an established pattern/library or create new ones? With the myriad of choices available, we can quickly become caught up in a web of confusion on this topic.
description: >-
  How do we know which patterns are good, better, best when it comes to accessibility? Is it better to use an established pattern/library or create new ones? With the myriad of choices available, we can quickly become caught up in a web of confusion on this topic.
categories:
  - Usability
  - UX
  - Accessibility
---

Marc Benioff memorably stated that the only constant in the technology industry is change. Having worked in tech for over 15 years, I can confirm this. Fellow tech dinosaurs can attest that the way the web worked in the early days is drastically different than many of us could have even imagined.

While this constant change in the technology industry has led to innovation and advancements we see today, it has also introduced the concept of choice. While choice &mdash; on the surface &mdash; may seem like an inherently positive thing, it does not always equal rainbows and roses. The influx of technological change also brings the splintering of coding languages and the never-ending flavors of programming “hotness.” Sometimes this abundance of choice turns into [overchoice](https://en.wikipedia.org/wiki/Overchoice) &mdash; a well-studied cognitive impairment in which people have difficulty making a decision due to having too many options.

In this article, we will attempt to untangle the complex world of accessible patterns &mdash; one step at a time. We will kick things off by reviewing current accessible patterns and libraries, then we will consider our general pattern needs and potential restrictions, and lastly, we will walk through a series of critical thinking exercises to learn how to better evaluate patterns for accessibility.

## What A Tangled Web We Weave

Overchoice has crept its way into all aspects of technology, including the patterns and libraries we use to build our digital creations &mdash; from the simple checkbox to the complex dynamic modal and everything in between. But how do we know which pattern or library is the right one when there are so many choices? Is it better to use established patterns/libraries that users encounter every day? Or is it better to create brand new patterns for a more delightful user experience?

With the myriad of options available, we can quickly become paralyzed by the overabundance of choices. But if we take a step back and consider why we build our digital products in the first place (i.e. the end-user) doesn’t it make sense to choose the pattern or library that can add the most value for the largest number of people?

If you thought choosing a pattern or library was an already daunting enough process, this might be the point where you start to get worried. But no need to fret &mdash; choosing an accessible pattern/library isn’t rocket science. Like everything else in technology, this journey starts with a little bit of knowledge, a huge heaping of trial and error, and an understanding that there is not just one perfect pattern/library that fits every user, situation, or framework.

How do I know this? Well, I have spent the past five years researching, building, and testing different types of accessible patterns while working on the [A11y Style Guide](https://a11y-style-guide.com/style-guide/), [Deque’s ARIA Pattern Library](https://dequeuniversity.com/library/), and evaluating popular [SVG patterns](https://cariefisher.com/a11y-svg/). But I have also reviewed many client patterns and libraries on every framework/platform imaginable. At this point in time, I can say without qualms that there is an innate hierarchy for pattern accessibility that starts to develop when you look long enough. And while there are occasionally patterns to avoid at all costs, it isn’t always so clear-cut. When it comes to accessibility, I would argue most patterns fall into gradients of good, better, best. The difficult part is knowing which pattern belongs in what category.

{{% feature-panel %}}

## Thinking Critically About Patterns

So how do we know which patterns are good, better, best when it comes to accessibility? It depends. This often invoked phrase from the digital accessibility community is not a cop-out but is shorthand for “we need more context to be able to give you the best answer.” However, the context is not always clear, so when building and evaluating the accessibility of a pattern, some fundamental questions I ask include:

*   Is there already an established accessible pattern we can use?
*   What browsers and assistive technology (AT) devices are we supporting?
*   Are there any framework limitations or other integrations/factors to consider?

Of course, your specific questions may vary from mine, but the point is you need to start using your critical thinking skills when evaluating patterns. You can do this by first observing, analyzing, and then ranking each pattern for accessibility before you jump to a final decision. But before we get to that, let’s first delve into the initial questions a bit more.

### Is There Already An Established Accessible Pattern?

Why does it seem that with each new framework, we get a whole new set of patterns? This constant reinvention of the wheel with new pattern choices can confuse and frustrate developers, especially since it is not usually necessary to do so.

Don’t believe me? Well, think about it this way: If we subscribe to the [atomic design system](https://bradfrost.com/blog/post/atomic-web-design/), we understand that several small “atoms” of code come together to create a larger digital product. But in the scientific world, atoms are not the smallest component of life. Each atom is made of many subatomic particles like protons, neutrons, and electrons.

That same logic can be applied to our patterns. If we look deeper into all the patterns available in the various frameworks that exist, the core subatomic structure is essentially the same, regardless of the actual coding language used. This is why I appreciate [streamlined coding libraries with accessible patterns](https://www.webaxe.org/web-accessible-code-library-design-systems-patterns/) that we can build upon based on technological and design needs.

**Note**: *Some great reputable sources include [Inclusive Components](https://inclusive-components.design), [Accessible Components](https://www.scottohara.me/code/), and the [Gov.UK Design System](https://design-system.service.gov.uk/get-started/), in addition to the [list of accessible patterns](https://www.smashingmagazine.com/the-smashing-newsletter/smashing-newsletter-issue-289/) Smashing Magazine recently published (plus a more detailed list of patterns and libraries at the end of the article).*

### What Browsers And Assistive Technology (AT) Devices Are We Supporting?

After researching a few base patterns that might work, we can move on to the question of browser and assistive technology (AT) device support. On its own, browser support is no joke. When you add in AT devices and [ARIA specifications](https://www.deque.com/blog/much-ado-about-aria/) to the mix, things begin to get tricky...not impossible, just a lot more time, effort, and thought-process involved to figure it all out.

But it’s not *all* bad news. There are some fabulous resources like [HTML5 Accessibility](https://stevefaulkner.github.io/HTML5accessibility/) and [Accessibility Support](https://a11ysupport.io/) that help us build a greater understanding of current browser + AT device support. These websites outline the different HTML and ARIA pattern sub-elements available, include open source community tests, and provide some pattern examples &mdash; for both desktop and mobile browsers/AT devices.

### Are There Any Framework Limitations Or Other Integrations/Factors To Consider?

Once we have chosen a few accessible base patterns and factored in the browser/AT device support, we can move on to more fine-grained contextual questions around the pattern and its environment. For example, if we are using a pattern in a content management system (CMS) or have legacy code considerations, there will be certain pattern limitations. In this case, a handful of pattern choices can quickly be slashed down to one or two. On the flip side, some frameworks are more forgiving and open to accepting any pattern, so we can worry less about framework restrictions and focus more on making the most accessible pattern choice we can make.

Besides all that we have discussed so far, there are many additional considerations to weigh when choosing a pattern, like performance, security, search engine optimization, language translation, third-party integration, and more. These factors will undoubtedly play into your accessible pattern choice, but you should also be thinking about the people creating the content. The accessible pattern you choose must be built in a robust enough way to handle any potential limitations around editor-generated and/or user-generated content.

## Evaluating Patterns For Accessibility

Code often speaks louder than words, but before we jump into all of that, a quick note that the following pattern examples are not the only patterns available for each situation, nor is the one deemed “best” in the group the best option in the entire world of accessible patterns.

For the pattern demos below, we should imagine a hypothetical situation in which we are comparing each group of patterns against themselves. While this is not a realistic situation, running through these critical thinking exercises and evaluating the patterns for accessibility should help you be more prepared when you encounter pattern choice in the real world.

### Accessible Button Patterns

The first group of patterns we will review for accessibility are ubiquitous to almost every website or app: buttons. The first button pattern uses the [ARIA button role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/button_role) to mimic a button, while the second and third button patterns use the [HTML `<button>` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button). The third pattern also adds `aria-describedby` and [CSS to hide things visually](https://css-tricks.com/inclusively-hidden/).

{{< codepen height="480" theme_id="light" slug_hash="KKNEjKR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Accessible Button Patterns](https://codepen.io/smashingmag/pen/KKNEjKR) by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

#### Good: `role="button"`

<pre><code class="language-svg">&lt;a role="button" href="[link]"&gt;Sign up&lt;/a&gt;
</code></pre>

#### Better: `<button>`

<pre><code class="language-svg">&lt;button type="button"&gt;Sign up&lt;/button&gt;
</code></pre>

#### Best: `<button>` + `visually hidden` + `aria-describedby`

<div class="break-out">

 <pre><code class="language-svg">&lt;button type="button" aria-describedby="button-example"&gt;Sign up&lt;/button&gt;
&lt;span id="button-example" class="visually-hidden"&gt; for our monthly newsletter&lt;/span&gt;
</code></pre>
</div>

While the first patterns seem simple at first glance, they do evoke some accessibility questions. For example, on the first button pattern, we see ARIA `role="button"` is used on the “good” pattern instead of an HTML `<button>` element. Thinking in terms of accessibility, since we know the HTML `<button>` element was introduced in HTML4, we can reasonably speculate that it is fully supported by the latest versions of all the major browsers and will play nicely with most AT devices. But if we dig deeper and look at the accessibility support for [ARIA role="button"](https://a11ysupport.io/tech/aria/button_role) we see a slight advantage from an assistive technology perspective, while the [HTML `<button>` element](https://a11ysupport.io/tech/html/button_element) is missing some areas of browser + AT coverage, especially when we consider voice control support.

So then why isn’t the ARIA pattern in the “better” category? Doesn’t ARIA make it more accessible? Nope. In fact, in cases like this, accessibility professionals often recite the first rule of ARIA &mdash; [don’t use ARIA](https://www.w3.org/TR/using-aria/#rule1). This is a tongue-in-cheek way of saying use HTML elements whenever possible. ARIA is indeed powerful, but in the wrong hands, it can do more harm than good. In fact, the [WebAIM Million report](https://webaim.org/projects/million) states that “pages with ARIA present averaged 60% more errors than those without.” As such, you must know what you are doing when using ARIA.

Another strike against using ARIA in this situation is that the button functionality we need would need to be built for the `role="button"` pattern, while that functionality is already pre-baked into the `<button>` element. Considering the `<button>` element also has 100% browser support and is an easy pattern to implement, it edges slightly ahead in the hierarchy when evaluating the first two patterns. Hopefully, this comparison helps bust the myth that adding ARIA makes a pattern more accessible &mdash; oftentimes the opposite is true.

The third button pattern shows the HTML `<button>` element coupled with `aria-describedby` linked to an ID element that is visually hidden with CSS. While this pattern is slightly more complex, it adds a lot in terms of context by creating a relationship between the button and the purpose. When in doubt, anytime we can add more context to the situation, the better, so we can assume if coded correctly, it is the best pattern when comparing only these specific button patterns.

{{% ad-panel-leaderboard %}}

### Accessible Contextual Link Patterns

The second group of patterns we will review are contextual links. These patterns help give more information to AT users than what is visible on the screen. The first link pattern utilizes CSS to visually hide the additional contextual information. While the second and third link patterns add ARIA attributes into the mix: [`aria-labelledby`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-labelledby_attribute) and [`aria-label`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute), respectively.

{{< codepen height="480" theme_id="light" slug_hash="VwmRJYv" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Accessible Link Patterns](https://codepen.io/smashingmag/pen/VwmRJYv) by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

#### Good: `visually-hidden`

<div class="break-out">

 <pre><code class="language-svg">&lt;p&gt;“My mother always used to say: The older you get, the better you get, unless you’re a banana.” &mdash; Rose (Betty White)&lt;a href="[link]"&gt;Read More&lt;span class="visually-hidden"&gt; Golden Girl quotes&lt;/span&gt;&lt;/a&gt;&lt;/p&gt;
</code></pre>
</div>

#### Better: `visually-hidden` + `aria-labelledby`

<div class="break-out">

 <pre><code class="language-svg">&lt;p&gt;“I'm either going to get ice cream or commit a felony...I'll decide in the car.” &mdash; Blanche (Rue McClanahan)&lt;a href="[link]" aria-labelledby="quote"&gt;Read More&lt;/a&gt;&lt;span class="visually-hidden" id="quote"&gt;Read more Golden Girl quotes&lt;/span&gt;&lt;/p&gt;
</code></pre>
</div>

#### Best: `aria-label`

<div class="break-out">

 <pre><code class="language-svg">&lt;p&gt;“People waste their time pondering whether a glass is half empty or half full. Me, I just drink whatever’s in the glass.” &mdash; Sophia (Estelle Getty)&lt;a href="[link]" aria-label="Read more Golden Girls quotes"&gt;Read More&lt;/a&gt;&lt;/p&gt;
</code></pre>
</div>

While all three of the contextual link patterns look the same, when we inspect the code or test them with AT devices, there are some obvious differences. The first pattern uses a CSS technique to hide the content visually for sighted users but still renders the hidden content to non-sighted AT users. And while this technique _should_ work in most cases, there is no real relationship formed between the link and the additional information, so the connection is tentative at best. As such, the first link pattern is an OK choice but not the most robust link pattern of the three.

The next two link patterns are a bit more tricky to evaluate. According to the [ARIA specs from the W3C](https://www.w3.org/TR/wai-aria/#aria-label) “The purpose of `aria-label` is the same as that of `aria-labelledby`. It provides the user with a recognizable name of the object.” So, in theory, both attributes should have the same basic functionality.

However, the specs also point out that user agents give precedence to `aria-labelledby` over `aria-label` when deciding which accessible name to convey to the user. Research has also shown issues around [automatic translation and aria-label attributes](https://adrianroselli.com/2019/11/aria-label-does-not-translate.html). So that means we should use `aria-labelledby`, right?

Well, not so fast. The same ARIA specs go on to say “If the interface is such that it is not possible to have a visible label on the screen (or if a visible label is not the desired user experience), authors *should* use `aria-label` and *should not* use `aria-labelledby`.” Talk about confusing &mdash; so which pattern should we choose?

If we had large-scale translation needs, we might decide to change the visual aspect and write out the links with the full context displayed (e.g. “<em>Read more about this awesome thing</em>”) or decide to use `aria-labelledby`. However, let’s assume we did not have large-scale translation needs or could address those needs in a reasonable/accessible way, and we didn’t want to change the visual &mdash; what then?

Based on the current ARIA 1.1 recommendations (with the promise of [translation of aria-label in ARIA 1.2](https://w3c.github.io/aria/#translatable-states-and-properties)) plus the fact that `aria-label` is a bit easier for devs to implement versus `aria-labelledby`, we could decide to weight `aria-label` over `aria-labelledby` in our pattern evaluation. This is a clear example of when context weighs heavily in our accessible pattern choice.

{{% ad-panel-leaderboard %}}

### Accessible `<svg>` Patterns

Last, but certainly not least, let’s investigate a group of SVG image patterns for accessibility. SVGs are a visual representation of code, but code nonetheless. This means an AT device might skip over a non-decorative SVG image unless the `role="img"` is added to the pattern.

Assuming the following SVG patterns are informational in nature, a `role="img"` has been included in each. The first SVG pattern uses the `<title>` and `<text>` in conjunction with CSS to visually hide content from sighted users. The next two SVG patterns involve the `<title>` and `<desc>` elements, but with an `aria-labelledby` attribute added to the last pattern.

{{< codepen height="480" theme_id="light" slug_hash="poNYXvK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Accessible SVG Patterns](https://codepen.io/smashingmag/pen/poNYXvK) by <a href="https://codepen.io/cariefisher">Carie Fisher</a>.{{< /codepen >}}

#### Good: `role="img"` + `<title>` + `<text>`

<div class="break-out">

 <pre><code class="language-svg">&lt;svg xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" version="1.1" role="img" x="0px" y="0px" viewBox="0 0 511.997 511.997" style="enable-background:new 0 0 511.997 511.997;" xml:space="preserve"&gt;
    &lt;title&gt;The first little pig built a house out of straw.&lt;/title&gt;
    &lt;text class="visually-hidden"&gt;Sadly, he was eaten by the wolf.&lt;/text&gt;...
&lt;/svg&gt;
</code></pre>
</div>

#### Better: `role="img"` + `<title>` + `<desc>`

<div class="break-out">

 <pre><code class="language-svg">&lt;svg xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" version="1.1" role="img" x="0px" y="0px" viewBox="0 0 511.997 511.997" style="enable-background:new 0 0 511.997 511.997;" xml:space="preserve"&gt;
    &lt;title&gt;The second little pig built a house out of sticks.&lt;/title&gt;
    &lt;desc&gt;Sadly, he too was eaten by the big, bad wolf.&lt;/desc&gt;...
&lt;/svg&gt;
</code></pre>
</div>

#### Best: `role="img"` + `<title>` + `<desc>` + `aria-labelledby="[id]"`

<div class="break-out">

 <pre><code class="language-svg">&lt;svg xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" version="1.1" role="img" aria-labelledby="pig3house pig3wolf" x="0px" y="0px" viewBox="0 0 511.997 511.997" style="enable-background:new 0 0 511.997 511.997;" xml:space="preserve"&gt;
    &lt;title id="pig3house"&gt;The third little pig built a house out of bricks.&lt;/title&gt;
    &lt;desc id="pig3wolf"&gt;Thankfully he wasn't eaten by the wolf.&lt;/desc&gt;...
&lt;/svg&gt;
</code></pre>
</div>

Let’s first look at the first pattern using `<title>` and `<text>` and visually hidden CSS. Unlike previous visibly hidden text in patterns, there _is_ an inherent relationship between the `<title>` and `<text>` elements since they are grouped under the same SVG element umbrella. However, this relationship is not very strong. In fact, if you look back at my [research on SVG patterns](https://cariefisher.com/a11y-svg/), we see that only 3 out of 8 browser/AT combinations heard the complete message. (Note: Pig pattern #1 is equivalent to light bulb pattern #7.)

This is true though the working [W3C SVG specs define the `<text>` element](https://www.w3.org/TR/SVG2/text.html#Introduction) as “a graphics element consisting of text…the characters to be drawn are expressed as character data. As a result, text data in SVG content is readily accessible to the visually impaired.” This first pattern is OK, but we can do better.

The second pattern removes the `<text>` element and replaces it with a `<desc>` element. The [W3C SVG specs](https://www.w3.org/TR/SVG2/struct.html#DescriptionAndTitleElements) state:

<blockquote><p>“The <code>&lt;title&gt;</code> child element represents a short text alternative for the element... and the <code>&lt;desc&gt;</code> element represents more detailed textual information for the element such as a description.”</p></blockquote>

Meaning the `<title>` and `<desc>` elements in SVGs can be used similarly to image alternative text and long description options found traditionally in `<img>` elements. After adding the `<desc>` element to the second SVG, we see similar browser/AT support with 3 out of 8 combinations hearing the complete message. (Note: Pig pattern #2 is equivalent to light bulb pattern #10.) While these test results seem to mirror the first pattern, the reason this pattern gets a bump into the “better” category is it is slightly easier to implement code-wise and it [impacts more AT users](https://webaim.org/projects/screenreadersurvey8), as it worked on JAWS, VoiceOver desktop, and VoiceOver mobile, while the first pattern supported less popular browser/AT combinations.

The third pattern again uses the `<title>` and `<desc>` elements but now has an `aria-labelledby` plus ID added into the mix. According to the same SVG tests, adding this additional piece of code means we can fully support 7 out of 8 browser/AT combinations. (Note: Pig pattern #3 is equivalent to light bulb pattern #11.) Out of the three SVG patterns, this third one is the “best” since it supports the most AT devices. But this pattern does have a draw-back in using some browser/AT combinations; you will hear duplicate image title/description content for this pattern. While potentially annoying to users, I’d argue it is generally better to hear duplicated content than none at all.

## Closing Thoughts

While we all certainly value choice in tech, I wonder if we’ve come to a point in time where the overabundance of options has left us paralyzed and confused about what to do next? In terms of picking accessible patterns, we can ask straight-forward questions around pattern/library options, browser/AT device support, framework limitations, and more.

With the right data in hand, these questions are easy enough to answer. However, it becomes a bit more complicated when we go beyond patterns and really consider the people using them. It is then that we realize the impact our choices have on our users’ ability to succeed. As Prof. George Dei eloquently states:

<blockquote><p>“Inclusion is not bringing people into what already exists &mdash; it is making a new space, a better space for everyone.”</p></blockquote>

By taking a bit more time to critically think about patterns and choose the most accessible ones, we will undoubtedly create a more inclusive space to reach more users &mdash; on their terms.

### Related Resources

#### Tools

- [Accessibility Support](https://a11ysupport.io/), [Michael Fairchild](https://twitter.com/mfairchild365), a11ysupport.io
- [HTML5 Accessibility](https://stevefaulkner.github.io/HTML5accessibility/), [Steve Faulkner](https://twitter.com/stevefaulkner)

####  Pattern Libraries

- [Accessibility Project](https://www.a11yproject.com/resources/)
- [Accessibility Style Guide](https://a11y-style-guide.com/style-guide/)
- [Accessible Components](https://www.scottohara.me/code/), [Scott O’Hara](https://twitter.com/scottohara)
- [Accessible `drag-and-drop` List Reorder Plugin](https://schne324.github.io/dragon-drop/demo/), [Harris Schneiderman](https://twitter.com/theHarrisius)
- [Deque’s ARIA Pattern Library](https://dequeuniversity.com/library/)
- [Deque’s Accessible React Library](https://cauldron.dequelabs.com/)
- [GOV.UK Design System](https://design-system.service.gov.uk/)
- [Inclusive Components](https://inclusive-components.design/), [Heydon Pickering](https://twitter.com/heydonworks)
- [U.S. Web Design System (USWDS)](https://designsystem.digital.gov/documentation/developers/)
- [Web Accessibility Tutorials](https://www.w3.org/WAI/tutorials/)

{{< signature "vf, il" >}}
