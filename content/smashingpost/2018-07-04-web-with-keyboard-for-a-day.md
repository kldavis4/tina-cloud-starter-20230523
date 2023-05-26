---
title: 'I Used The Web For A Day With Just A Keyboard'
slug: web-with-just-a-keyboard
author: chrisbashton
image: >-
  null
date: 2018-07-04T13:30:05+02:00
summary: >-
  Many of us are taught to make sure our sites can be used via keyboard. Why is that, and what is it like in practice? Chris Ashton did an experiment to find out.
description: >-
  Many of us are taught to make sure our sites can be used via keyboard. Why is that, and what is it like in practice? Chris Ashton did an experiment to find out.
categories:
  - Accessibility
  - Usability
  - UX 
---
This article is part of a series in which I attempt to use the web under various constraints, representing a given demographic of user. I hope to raise the profile of difficulties faced by real people, which are avoidable if we design and develop in a way that is sympathetic to their needs. Last time, [I used the web for a day without JavaScript](https://www.smashingmagazine.com/2018/05/using-the-web-with-javascript-turned-off/). Today, I forced myself to navigate the web using just my keyboard.

## Who Uses The Keyboard To Navigate?

Broadly, there are three types of keyboard users:

- Mobility-impaired users who struggle to use a mouse,
- Vision-impaired users who are unable to see clickable elements in the page,
- Power users who are able to use a mouse but find it quicker to use a keyboard.

### How Many Users Are We Talking?

I’ve trawled the web for statistics on keyboard usage, and I couldn’t find a thing. Seriously. Not *one* study.

Most keyboard accessibility guidance sites simply take for granted that "many users" rely on keyboards to get around. Anyone trying to get an approximate number is usually preachily dismissed with "stats don’t matter &mdash; your site should be accessible, period."

Yes, it *is* true that the scale of non-mouse usage is a moot point. If you can make a change that empowers even one user, it is a change worth making. But there are plenty of stats available around things like color blindness, browser usage, connection speeds and so on &mdash; why the caginess around keyboard statistics? If the numbers are as prevalent as sites seem to suggest, surely having them would enable a stronger business case and make defending keyboard accessibility to your stakeholders easier.

{{% feature-panel %}}

The closest thing to a number I can find is an [article on PowerMapper](https://www.powermapper.com/blog/website-accessibility-disability-statistics/), which suggests that 7% of working-age adults in the US, UK, and Canada have “severe dexterity difficulties.” This would make them “unlikely to use a mouse, and rely on the keyboard instead.”

Users with severe visual disabilities use software called a [screen reader](https://www.rnib.org.uk/information-everyday-living-using-technology-beginners-guides/beginners-guide-assistive-technology), which is software that reads out content on the screen as synthesized speech. Like sighted users, non-sighted users want to be able to scan pages for interesting information, so the screen reader has keyboard shortcuts for navigating via headings and links, and relies on keyboard focusable elements for interaction.

<blockquote>“People who are blind need full keyboard access. Period.”<br /><br />&mdash; David Macdonald, co-editor of Using WAI ARIA in HTML5</blockquote>

These same users also have screen readers on their mobile devices, where they use swipe gestures instead of keyboard presses to ‘tab around’ content. So whilst they’re not literally using a keyboard, they do require the site to be keyboard-accessible as the screen reader technology hooks into the same tab ordering and event listeners as if they were using a keyboard. It’s worth noting that only [about two-thirds to three-quarters of screen reader users are blind](https://adrianroselli.com/2017/02/not-all-screen-reader-users-are-blind.html), meaning the rest might use a combination of screen-reader and magnification techniques.

[2.3% of American people (of all ages)](https://nfb.org/blindness-statistics) have a visual disability, not all of which would necessarily warrant the use of a screen reader. In 2016, Addy Osmani estimated actual screen reader usage to be [around 1 to 2%](https://medium.com/@addyosmani/accessible-ui-components-for-the-web-39e727101a67). If we factor these users in with our mobility-impaired users and our power users, keyboard usage adds up to a sizeable percentage of the global audience. Therefore, caring about keyboard accessibility is not just doing the right thing morally (and legally &mdash; many countries require websites to be [accessible by law](https://www.w3.org/WAI/policies/)), but it also makes good business sense.

With all of that in mind, what is the state of the web today? Time to find out!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0595e057-c51d-4503-9491-b7abc61e73ba/laptop-coasters-touchpad.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0595e057-c51d-4503-9491-b7abc61e73ba/laptop-coasters-touchpad.jpg" sizes="100vw" caption="I placed coasters over my touchpad to avoid temptation in using the keyboard for this experiment. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0595e057-c51d-4503-9491-b7abc61e73ba/laptop-coasters-touchpad.jpg'>Large preview</a>)" alt="Laptop with coasters positioned over the touchpad to make using the touchpad impossible" >}}

## The Experiment

What does everyone do when they have a day’s worth of intimidating work ahead of them? Procrastinate! I headed over to [youtube.com](https://youtube.com/). I had a specific video in mind and was grateful to find I wouldn’t need to tab into the main search box, as it is focussed on page load by default.

### The `autofocus` Attribute

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/591dcc69-814f-497e-ab57-b5f7655b9bb7/youtube-search-bar.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/591dcc69-814f-497e-ab57-b5f7655b9bb7/youtube-search-bar.png" sizes="100vw" caption="YouTube homepage with search bar already in focus (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/591dcc69-814f-497e-ab57-b5f7655b9bb7/youtube-search-bar.png'>Large preview</a>)" alt="YouTube homepage with search bar already in focus" >}}

I assumed this would be focussed with JavaScript on window load, but it’s actually handled by the browser with an [`autofocus` attribute on the input element](https://www.w3schools.com/tags/att_input_autofocus.asp).

As a sighted keyboard user, I found this extremely useful. As a blind screen reader user, I’m not sure whether I’d like it or not. The [consensus seems to be that judicious use of `autofocus` is OK](https://github.com/nvaccess/nvda/issues/6796), in cases where the sole purpose of the page is to interact with a form (e.g. Google landing page, or a site contact form).

### Default Focus Styles

I searched for some *Whose Line Is It Anyway?* goodness, and couldn’t help noticing that YouTube hadn’t defined any custom `:focus` styles, instead relying on the browser’s native styling to visually indicate which elements I was tabbing through.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d24eca7-0746-4e3b-bcdb-f27071e9dbd1/whose-line-chrome.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d24eca7-0746-4e3b-bcdb-f27071e9dbd1/whose-line-chrome.png" sizes="100vw" caption="Chrome focus styling &mdash; the famous blue outline. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d24eca7-0746-4e3b-bcdb-f27071e9dbd1/whose-line-chrome.png'>Large preview</a>)" alt="Chrome focus styling — the famous blue outline." >}}

I’ve always been under the impression that not all browsers define their own `:focus` state, so you <em>have</em> to define your own custom styling. I decided to put this to the test and see which browsers neglect to implement a default style, but to my surprise, I couldn’t find one. Every browser I tested had its own native implementation of `:focus`, although each varied in style.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6fd391-5d64-4921-a636-a9e1b5ad4743/whose-line-firefox.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6fd391-5d64-4921-a636-a9e1b5ad4743/whose-line-firefox.png" sizes="100vw" caption="Firefox focus styling &mdash; a dotted outline. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6fd391-5d64-4921-a636-a9e1b5ad4743/whose-line-firefox.png'>Large preview</a>)" alt="Firefox focus styling &mdash; a dotted outline." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d537f67-29b9-4301-aba9-2412db5b5f53/whose-line-safari.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d537f67-29b9-4301-aba9-2412db5b5f53/whose-line-safari.png" sizes="100vw" caption="Safari focus styling &mdash; similar to Chrome but the blue halo is not as thick. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d537f67-29b9-4301-aba9-2412db5b5f53/whose-line-safari.png'>Large preview</a>)" alt="Safari focus styling &mdash; similar to Chrome but the blue halo is not as thick." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b054af-8713-4063-a892-165bcfcb34b1/whose-line-opera.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b054af-8713-4063-a892-165bcfcb34b1/whose-line-opera.png" sizes="100vw" caption="Opera focus styling is <em>identical</em> to Chrome, as they are both built on the Blink browser engine. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b054af-8713-4063-a892-165bcfcb34b1/whose-line-opera.png'>Large preview</a>)" alt="Opera focus styling is identical to Chrome, as they are both built on the Blink browser engine." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/495ed04b-ca97-46e6-85b4-f64a741d22a7/whose-line-edge.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/495ed04b-ca97-46e6-85b4-f64a741d22a7/whose-line-edge.png" sizes="100vw" caption="The focus styling in Edge is much the same as in Firefox. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/495ed04b-ca97-46e6-85b4-f64a741d22a7/whose-line-edge.png'>Large preview</a>)" alt="The focus styling in Edge is much the same as in Firefox." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eed9fe87-f0c7-4a98-901e-0cda283a0b26/whose-line-ie11.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eed9fe87-f0c7-4a98-901e-0cda283a0b26/whose-line-ie11.png" sizes="100vw" caption="IE11 underlines the link with a dotted line. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eed9fe87-f0c7-4a98-901e-0cda283a0b26/whose-line-ie11.png'>Large preview</a>)" alt="IE11 underlines the link with a dotted line." >}}

I even went quite far back in time:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f27d71e-8e49-47c6-bf97-eedd2bfe8ae9/whose-line-ie7-on-xp.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f27d71e-8e49-47c6-bf97-eedd2bfe8ae9/whose-line-ie7-on-xp.png" sizes="100vw" caption="IE7 focus styling (on XP) looks much the same as today’s Firefox implementation! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f27d71e-8e49-47c6-bf97-eedd2bfe8ae9/whose-line-ie7-on-xp.png'>Large preview</a>)" alt="IE7 focus styling (on XP) looks much the same as today’s Firefox implementation!" >}}

If you’d like to see more, there is [a comprehensive screenshot collection of different elements in browser native states](https://allyjs.io/tests/focus-outline-styles/).

What this tells me is that you can reasonably assume *every* browser comes with some basic `:focus` styling. It is OK to let the browser do the work. What you’re risking is inconsistency: all browsers style elements subtly differently, and some are so subtle that they’re not particularly visually accessible.

It is possible to disable the default browser focus styles &mdash; by setting `outline: none` on your element &mdash; but you should do this *only if you implement your own* styled alternative. [Heydon Pickering recommends this approach](https://www.heydonworks.com/article/shrinking-button-outlines), citing the unclear or ugly defaults used by some browsers. If you do decide to roll out your own styles, be sure to use more than just colour as a modifier: Add an outline or an underline or some other visual indicator to support users with color-blindness.

Many sites suppress default focus styles but fail to provide custom styles, leading to inaccessible experiences. If your site is using [Eric Meyer’s CSS reset](https://www.tjvantoll.com/2013/01/28/stop-messing-with-the-browsers-default-focus-outline/), it could be inaccessible; this commonly used file resets the default `:focus` styles but instructs the developer to write their own, and many fail to spot the instructions.

Some people argue that it can be confusing to the user if you disable the browser defaults, as they lose the visual affordance of the focus state they’re used to and instead have to learn what your site’s focus state looks like. On the other hand, some argue that the browser defaults are ugly, or even confusing to the non-keyboard user.

Why confusing? Well, check out this [animated carousel format on the BBC](https://www.bbc.co.uk/news/uk-politics-43492937). There are two navigation buttons &mdash; next, and previous &mdash; and it’s useful to the keyboard user that the focus remains on them throughout the narrative. But to the mouse user, it can be quite confusing that the clicked button is still ‘focussed’ after moving the cursor away.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4795db1b-5898-4249-bada-319354440749/bbc-brexit-carousel.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4795db1b-5898-4249-bada-319354440749/bbc-brexit-carousel.gif" width="600" height="594" alt="BBC animated carousel format" /></a><figcaption>BBC animated carousel format (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4795db1b-5898-4249-bada-319354440749/bbc-brexit-carousel.gif">Large preview</a>)</figcaption></figure>

### The `:focus-visible` CSS Selector

If you want the best of both worlds, you may want to explore the CSS4 [`:focus-visible` pseudo-class](https://developer.paciellogroup.com/blog/2018/03/focus-visible-and-backwards-compatibility/), which will let you provide different focus styling depending on context. `:focus-visible` styling only targets elements that have been focussed with keyboard, not with mouse click. This is super cool, though is currently only natively supported in Firefox. It can be enabled in Chrome by turning on the ‘Experimental Web Platform Features’ flag.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea3ff200-166b-4d79-b5b6-ea5ebf37f313/focus-visible.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea3ff200-166b-4d79-b5b6-ea5ebf37f313/focus-visible.gif" width="600" height="271" alt="The button is green when I tab to it via keyboard, and red when I click on it." /></a><figcaption>The button is green when I tab to it via keyboard, and red when I click on it. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea3ff200-166b-4d79-b5b6-ea5ebf37f313/focus-visible.gif">Large preview</a>)</figcaption></figure>

## YouTube Videos And Keyboard Accessibility

YouTube does a great job with its video player &mdash; every part of the player is keyboard navigable. I like how the volume controls slide out when you tab focus away from the mute icon, in contrast to sliding out when hovering over the mute icon.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4116eb-9522-4fb6-af6a-de3b7d937236/youtube-1.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4116eb-9522-4fb6-af6a-de3b7d937236/youtube-1.gif" width="588" height="232" alt="youtube" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4116eb-9522-4fb6-af6a-de3b7d937236/youtube-1.gif">Large preview</a></figcaption></figure>

What I didn’t like was that helpful labels, such as the ‘Mute’ text that appears when hovering over the mute icon, don’t get shown on focus.

Another area that lets YouTube down is that it suppresses some focus styling. Here was me trying to tab to the ‘Show more’ button.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0df9c252-ca91-4c0b-8f9e-281349cd54af/youtube-missing-focus.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0df9c252-ca91-4c0b-8f9e-281349cd54af/youtube-missing-focus.gif" width="600" height="340" alt="I try to tab to the “Show more” button via the video author avatar, title and links in the description, but end up tabbing to the “Add comment” section by accident." /></a><figcaption>I try to tab to the “Show more” button via the video author avatar, title and links in the description, but end up tabbing to the “Add comment” section by accident. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0df9c252-ca91-4c0b-8f9e-281349cd54af/youtube-missing-focus.gif">Large preview</a>)</figcaption></figure>

I accidentally tabbed right past the ‘Show more’ button because I couldn’t see any `:focus` styling applied, whether custom or native. I figured out that the native styling was being overridden with `outline-width`:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1928fa64-b5f0-4784-ac5a-5f004b40a480/youtube-focus-code.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1928fa64-b5f0-4784-ac5a-5f004b40a480/youtube-focus-code.gif" width="600" height="243" alt="Unchecking the outline-width: 0 rule enabled the blue border native Chrome focus styling." /></a><figcaption>Unchecking the <code>outline-width: 0</code> rule enabled the blue border native Chrome focus styling. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1928fa64-b5f0-4784-ac5a-5f004b40a480/youtube-focus-code.gif">Large preview</a>)</figcaption></figure>

## GitHub Keyboard Accessibility

OK, work time. Where better to work than at the home of code, [github.com](https://github.com/)?

I noticed three things about GitHub: One great, one reasonable, and one bad. 

First, the good.

### ‘Skip To Content’ Link

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/095fb8a3-354b-40b9-a266-c119b171afd5/github-landing-view.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/095fb8a3-354b-40b9-a266-c119b171afd5/github-landing-view.png" sizes="100vw" caption="GitHub landing view… keep an eye on this corner (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/095fb8a3-354b-40b9-a266-c119b171afd5/github-landing-view.png'>Large preview</a>)" alt="GitHub landing view… keep an eye on this corner" >}}

GitHub offers a `Skip to content` link, which skips over the main menu.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c61ac9-3570-4dc2-a248-3447b0faf043/skip-to-content-link-appears.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c61ac9-3570-4dc2-a248-3447b0faf043/skip-to-content-link-appears.png" sizes="100vw" caption="After tabbing once, a wild <code>Skip to content</code> link appears! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c61ac9-3570-4dc2-a248-3447b0faf043/skip-to-content-link-appears.png'>Large preview</a>)" alt="After tabbing once, a wild Skip to content link appears!" >}}

If you hit <kbd>ENTER</kbd> while focussed on the ‘Skip to content’ link, you skip all of the menu items at the top of the page and can start to tab within the main area of content, saving time when navigating. This is a common accessibility pattern that is super useful for both keyboard and screen reader users. [Around 30% of screen reader users](https://webaim.org/projects/screenreadersurvey7/#skip) will use a skip link if you provide one.

Alternatively, some sites choose to [place the main content first in the reading order](https://webaim.org/techniques/skipnav/#altorders), above the navigation. This approach has fallen out of fashion as it breaks the guideline of making your [DOM content match the visual order](https://www.w3.org/TR/WCAG20-TECHS/C27.html) (unless your navigation visually appears at the bottom). And whilst this approach means we don’t need a ‘Skip navigation’ link at all, we’d probably want a ‘Skip *to* navigation’ link in its place.

### Tab To See Content

One feature I noticed working differently to the ‘non-keyboard’ version was the code breakdown indicator.

Using the mouse, you can click the colored bar underneath any repository to view a proportional breakdown of the different programming languages used in the repo. Using the keyboard, you can’t actually navigate to the colored bar, but the languages come into view automatically when you tab past the end of the meta information.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8642b6df-40ff-4214-8528-689847346670/github-code-breakdown.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8642b6df-40ff-4214-8528-689847346670/github-code-breakdown.gif" width="600" height="38" alt="I tab through to the code language breakdown, before showing how it’s done with a mouse." /></a><figcaption>I tab through to the code language breakdown, before showing how it’s done with a mouse. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8642b6df-40ff-4214-8528-689847346670/github-code-breakdown.gif">Large preview</a>)</figcaption></figure>

This doesn’t really seem necessary &mdash; I would happily tab to the colored bar and hit <kbd>ENTER</kbd> on that &mdash; but this different behavior doesn’t cause any harm either.

### Invisible Links

One problematic thing I came across was that there was an “invisible” link after tabbing past my profile picture at the top right. My tab order would tab to the picture, then to this invisible link, and then to the ‘Watch’ button on the repo (see gif below). I had no idea what the invisible link did, so when I recognized I was on it, I hit <kbd>ENTER</kbd> and was promptly logged out!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c8a473-592c-4914-a028-6c01c912eaab/github-logout.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c8a473-592c-4914-a028-6c01c912eaab/github-logout.gif" width="600" height="401" alt="Beware of clicking invisible links." /></a><figcaption>Beware of clicking invisible links. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c8a473-592c-4914-a028-6c01c912eaab/github-logout.gif">Large preview</a>)</figcaption></figure>

On closer inspection, it looks like I’ve navigated to a “screenreader only” form (`sr-only` is a common screen reader class name) which has the ‘Sign out’ feature.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67bfbed1-83af-49ac-86f9-64e6dd8a5802/browser-screenreader-only.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67bfbed1-83af-49ac-86f9-64e6dd8a5802/browser-screenreader-only.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67bfbed1-83af-49ac-86f9-64e6dd8a5802/browser-screenreader-only.png'>Large preview</a>" alt="screenreader only" >}}

This sign-out link is *in addition* to the sign-out link on your profile dropdown menu:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4834f55a-196a-4d1c-a481-40a3dda599cc/sign-out-link-dropdown-menu-space.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4834f55a-196a-4d1c-a481-40a3dda599cc/sign-out-link-dropdown-menu-space.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4834f55a-196a-4d1c-a481-40a3dda599cc/sign-out-link-dropdown-menu-space.png'>Large preview</a>" alt="sign out link in dropdown menu" >}}

I’m not sure that two separate HTML sign-out links are necessary, as a screen reader user should be able to trigger the drop-down and navigate to the main sign-out link. And if we *wanted* to keep the separate link, I would recommend applying a `:focus` styling to the screen-reader content so that sighted users don’t accidentally trigger logging themselves out!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0b02414-e0f6-4611-8bae-bc0e80b3fad9/example-screen-reader-text-focus-styling.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0b02414-e0f6-4611-8bae-bc0e80b3fad9/example-screen-reader-text-focus-styling.png" sizes="100vw" caption="Example screen-reader text focus styling. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0b02414-e0f6-4611-8bae-bc0e80b3fad9/example-screen-reader-text-focus-styling.png'>Large preview</a>)" alt="Example screen-reader text focus styling." >}}

## How To Make A ‘Skip To Content’ Shortcut

So how do we recreate that ‘Skip to content’ shortcut? It’s pretty simple to implement, but can be deceptively tricky to get perfect &mdash; so here is what I consider to be the Holy Grail of skip links solutions.

‘Skip link’ is alternatively called ‘Skip navigation’, ‘Skip main navigation’, ‘Skip navigation links’, or ‘Skip to main content’. [‘Skip to main content’ is probably the clearest](https://webaim.org/techniques/skipnav/) as it tells you where you are navigating to, rather than what you are skipping over.

The shortcut link should ideally appear straight after the opening `<body>` tag. It *could* appear later in the DOM, even after the footer, provided you have a `tabindex="1"` attribute to force it to become the first interactive element in the tab order. However, using tabindex with a number greater than zero is generally bad practice and will often result in a warning when using validation tools such as [Lighthouse](https://developers.google.com/web/tools/lighthouse/).

It’s not foolproof to rely on `tabindex`, as you may have more than one link with `tabindex="1"`. In these cases, it is the *first* link that would get the tab focus first, not any later links. [Read more about using the tabindex attribute here](https://developer.paciellogroup.com/blog/2014/08/using-the-tabindex-attribute/), but remember that you’re always better off physically moving your link to the beginning of the DOM to be safe.

<pre><code class="language-html">&lt;a class="screen-reader-shortcut" href="#main-content"&gt;
  Skip to main content
&lt;/a&gt;
</code></pre>

The ‘Skip to main content’ link has limited use to sighted users, who can already skip the navigation by using their eyes. So, whilst some sites keep the skip link visible at all times, the convention nowadays is to keep the link hidden until you tab into it, at which point it is in focus and gains the styling applied by the `:focus` pseudo selector.

<div class="break-out">

<pre><code class="language-css">.screen-reader-shortcut {
  position: absolute;
  top: -1000em;
}

.screen-reader-shortcut:focus {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
  /* ...and now any nice styling you want to apply... */
  padding: 1em;
  background-color: rgb(114, 105, 105);
  color: white;
  text-decoration: none;
}
</code></pre></div>

So, what are we actually skipping to? What is `#main-content`? It can really be anything:

1.  **Inline content**  
i.e. the id of your `h1` tag: `<h1 id="main-content">`.
2.  **Container**  
e.g. the id of the container around your main content such as `<main id="main-content">`.
3.  **Sibling anchor**  
You can link to a named tag just above your main content, e.g. `<a name="main-content"></a>`. This approach is usually described in older tutorials &mdash; I wouldn’t recommend it these days.

For maximum compatibility across all screen readers, I’d recommend linking to the `h1` tag. This is to ensure that the content gets read out as soon as you’ve used the skip link. Linking to containers can lead to funny behavior, e.g. the screen reader starting to read out *all* the content inside the container.

Your `#main-content` should also have a `tabindex` of `-1`, to ensure that it is programmatically focussable. Some screen readers may not obey the skip link otherwise.

<div class="break-out">

<pre><code class="language-html">&lt;h1 id="main-content" tabindex="-1"&gt;This is the title of the page&lt;/h1&gt;
</code></pre></div>

One last consideration: legacy browser support. If you have enough users on IE9 or below, you may need to apply [a small JavaScript fix](https://www.nczonline.net/blog/2013/01/15/fixing-skip-to-content-links/) to your skip links to ensure that the focus does actually shift as expected and your users successfully skip your navigation.

{{% ad-panel-leaderboard %}}

### Why Are We Reinventing The Wheel?

It seems crazy that as web developers we have to implement this ‘skip navigation’ hack on all of our sites as a rule. You would think we could let the standards do the work.

Since HTML5, we’ve had semantic elements such as `<main>`, `<nav>` and `<header>`. Prior to that, we had [ARIA landmarks](https://www.washington.edu/accessibility/web/landmarks/) such as `role="main"`, `role="navigation"` and `role="banner"` respectively. In the current landscape of the web, best practice dictates that you need both, i.e. `<main role="main">`, which is a horrid violation of the DRY principle, but there we go.

With all this semantic richness, you’d hope that browsers would start natively supporting navigation via these landmark areas, for example by exposing a keyboard shortcut for users to tab straight into the `<main>` section of a web page. No such luck &mdash; there is no native support at the moment. Your best bet is to use the [Landmark Navigation via Keyboard extension](https://matatk.agrip.org.uk/landmarks/) for Chrome, Opera or Firefox.

Screen reader users, however, <em>can</em> start navigating directly to these landmark regions. For example, on VoiceOver on Mac, you can hit <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>U</kbd> to bring up the Landmarks Menu and go to the ‘main’ landmark, which is a quick and consistent shortcut to get to the main content. Of course, this relies on sites marking up their documents correctly.

Here is a good starting point for your site if you’d like it to be navigable via landmark regions:

<div class="break-out">

<pre><code class="language-html">&lt;body&gt;
  &lt;header role="banner"&gt;
    &lt;!-- Logo and things can go here --&gt;
    &lt;nav role="navigation"&gt;
      &lt;!-- Site navigation links go here --&gt;
    &lt;/nav&gt;
  &lt;/header&gt;

  &lt;main role="main"&gt;
    &lt;!-- Main content lives here - including our h1 --&gt;
  &lt;/main&gt;

  &lt;footer role="contentinfo"&gt;
    &lt;!-- Copyright statement, etc --&gt;
  &lt;/footer&gt;
&lt;/body&gt;
</code></pre></div>

All this markup is thirsty work. Time for a coffee.

## Pact Coffee

I remember seeing a flyer for [pactcoffee.com](https://www.pactcoffee.com/)… let’s go and take a look!

### Cookie Banner

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eaae0b0-64cd-4d81-bcc9-0ae6b263a84e/cookie-policy-pact.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eaae0b0-64cd-4d81-bcc9-0ae6b263a84e/cookie-policy-pact.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eaae0b0-64cd-4d81-bcc9-0ae6b263a84e/cookie-policy-pact.png'>Large preview</a>" alt="Screenshot of Pact website with cookie policy banner fixed to bottom of viewport" >}}

The ‘Cookie policy’ banner is one of the first things you notice here, and dismissing it is almost an instinctive reflex for the sighted mouse user. Some screen reader users may not care about it (if you’re blind, you wouldn’t know it’s there until you reach it), but as a sighted user, you see it, you want to kill it, and in the case of this site, you need to tab past ALL OF THE OTHER LINKS before you can dismiss it.

I used the [ChromeLens accessibility extension](https://chrome.google.com/webstore/detail/chromelens/idikgljglpfilbhaboonnpnnincjhjkd?hl=en) to trace the tab order of the page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bcbb13a-2c27-4991-a653-54478344e3fb/pact-tab-order.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bcbb13a-2c27-4991-a653-54478344e3fb/pact-tab-order.gif" width="1100" height="688" alt="I have to tab through every single link in the page before I can dismiss the cookie banner" /></a><figcaption>I have to tab through every single link in the page before I can dismiss the cookie banner. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bcbb13a-2c27-4991-a653-54478344e3fb/pact-tab-order.gif">Large preview</a>)</figcaption></figure>

This can be fixed by either moving the notice to the top of the document (it can still be anchored to the bottom visually with CSS), or by adding a `tabindex="1"` to the OK button. I would suggest applying this fix to any content where the expectation is that the user will want to dismiss it.

### More Invisible Links

Like on GitHub, I found myself tabbing to an off-screen element whose purpose wasn’t clear. It turned out to be a ‘See less…’ toggle that sits *behind* the ‘See more…’ card.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca490936-d907-4708-a4b3-cfd5332f6bb1/pact.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca490936-d907-4708-a4b3-cfd5332f6bb1/pact.gif" width="600" height="298" alt="Tabbing from See more to a hidden area to another See more button." /></a><figcaption>Tabbing from ‘See more’, to a hidden area, to another ‘See more’ button. What’s that mystery hidden area? Oh, it’s the ‘See less’ button “on the other side”. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca490936-d907-4708-a4b3-cfd5332f6bb1/pact.gif">Large preview</a>)</figcaption></figure>

This is because the ‘hidden’ area isn’t really hidden, it’s just rotated 180 degrees, using:

<pre><code class="language-css">transform: rotateY(180deg);
</code></pre>

…which means the ‘See less…’ button is still part of the tab order. This can be fixed by applying a `display: none` until the application is ready to trigger the rotation:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eedb9704-bc4c-4def-8cfb-96cf1eb64256/pact-fix.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eedb9704-bc4c-4def-8cfb-96cf1eb64256/pact-fix.gif" width="600" height="363" alt="Applying display: none to the ‘See less…’ link takes it out of the tab order and makes for a less confusing keyboard experience." /></a><figcaption>Applying <code>display: none</code> to the ‘See less…’ link takes it out of the tab order and makes for a less confusing keyboard experience. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eedb9704-bc4c-4def-8cfb-96cf1eb64256/pact-fix.gif">Large preview</a>)</figcaption></figure>

Coffee ordered. It's now time to carry on with my research.

## IT World

I was doing some research for this article and came across a similar experiment to my own; [Kevin Purdy browsed the web for seven days using only his keyboard](https://www.itworld.com/article/2826902/enterprise-software/7-days-using-only-keyboard-shortcuts--no-mouse--no-trackpad--no-problem-.html). I find it ironic that I was unable to read his article under the same constraints!

The problem was a full-page cookie banner, requiring me to "Update Privacy Settings" or accept the default cookie settings. No matter how many times I tabbed, I could not focus in on the cookie banner and dismiss it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6947a6b2-782c-4fae-9890-a9ac5f1e7a00/it-world-tabbing.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6947a6b2-782c-4fae-9890-a9ac5f1e7a00/it-world-tabbing.gif" width="600" height="348" alt="gif showing that fast tabbing through the page never reaches the popup modal buttons" /></a><figcaption>Holding down <code>TAB</code> didn’t help. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6947a6b2-782c-4fae-9890-a9ac5f1e7a00/it-world-tabbing.gif">Large preview</a>)</figcaption></figure>

I dug into the source code to find out what was going on. For a moment, I thought it might be our arch nemesis, the `outline` CSS property.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a806eb23-e5b0-4ea5-852b-71ba5bcbc1c5/itworld-culprit.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a806eb23-e5b0-4ea5-852b-71ba5bcbc1c5/itworld-culprit.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a806eb23-e5b0-4ea5-852b-71ba5bcbc1c5/itworld-culprit.png'>Large preview</a>" alt="itworld culprit" >}}

Inspecting the "Update Privacy Setting" link, I can see an `outline: 0` as I suspected. So perhaps I *am* focussing on the buttons, but there is no visual feedback when that happens?

I tried setting the state to `:hover` to see if I was missing out on any styling as a keyboard user:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/425d7529-ea92-45de-8ffc-a3122ac3157e/itworld-force-focus.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/425d7529-ea92-45de-8ffc-a3122ac3157e/itworld-force-focus.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/425d7529-ea92-45de-8ffc-a3122ac3157e/itworld-force-focus.png'>Large preview</a>" alt="itworld force focus" >}}

Sure enough, the link turned a nice, obvious orange colour on hover &mdash; something I never saw on focus:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bcaa3c-e9ce-469a-84cb-6effcf50bcd2/itworld-hover.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bcaa3c-e9ce-469a-84cb-6effcf50bcd2/itworld-hover.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29bcaa3c-e9ce-469a-84cb-6effcf50bcd2/itworld-hover.png'>Large preview</a>" alt="itworld hover" >}}

Hoorah! Cracked it! I never saw the `:focus` state because custom styling was only being applied on `:hover`. I must have skipped past the buttons without even noticing, right?

Wrong. Even when I hack the CSS locally, I could not see any focus styling, meaning I wasn’t even getting as far as tabbing into the cookie modal. Then I realised… the link was missing a `href` attribute:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/714fc08c-b200-42a5-aacd-337c6e9c90ef/itworld-markup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/714fc08c-b200-42a5-aacd-337c6e9c90ef/itworld-markup.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/714fc08c-b200-42a5-aacd-337c6e9c90ef/itworld-markup.png'>Large preview</a>" alt="itworld markup" >}}

*That* was the real culprit. The `outline: 0` wasn’t the problem &mdash; the browser was never going to tab to the link because it wasn’t a valid link!

From the [HTML 5.2 specification](https://www.w3.org/TR/html5/single-page.html#the-a-element):

<blockquote>The destination of the link(s) is given by the href attribute, which must be present and must contain a valid non-empty URL potentially surrounded by spaces. If the href attribute is absent, then the element does not define a link.</blockquote>

Giving the links a href attribute &mdash; even if it’s just `#` &mdash; would make them valid links and would add them to the tab order of the page.

Funnily enough, later on that day, I was sent [an article on PC World](https://www.pcworld.com/article/3124486/hardware/microsofts-fpga-powered-supercomputer-can-translate-wikipedia-faster-than-you-can-blink.html) to read and I encountered *exactly* the same problem.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/532de85b-5927-4460-9994-53c2ad4ee5e9/popup-pcworld.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/532de85b-5927-4460-9994-53c2ad4ee5e9/popup-pcworld.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/532de85b-5927-4460-9994-53c2ad4ee5e9/popup-pcworld.png'>Large preview</a>" alt="popup on pcworld site" >}}

It seems that both sites were using the same Consent Management Platform (CMP). I [did a little digging and deduced that it was affecting a number of sites](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/issues/45) owned by the same company, and have since contacted them directly with a suggested fix.

## Kinetico

My kitchen tap is leaking and I’ve been meaning to get it replaced. I saw an ad in the local paper for [kinetico.co.uk](https://www.kinetico.co.uk/), so thought I’d take a look.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/628ea5a1-9680-4a9f-85d8-6a6825a3c6b3/kinetico.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/628ea5a1-9680-4a9f-85d8-6a6825a3c6b3/kinetico.gif" width="600" height="323" alt="It’s impossible to navigate to the nested menu items via a keyboard." /></a><figcaption>It’s impossible to navigate to the nested menu items via a keyboard. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/628ea5a1-9680-4a9f-85d8-6a6825a3c6b3/kinetico.gif">Large preview</a>)</figcaption></figure>

I couldn’t navigate to the ‘Kitchen Taps’ section, as the link was tucked away behind a ‘Salt & Cartridges’ parent link which only shows its child links on hover. It’s interesting that the site is forward-thinking enough to provide a ‘Skip to Content’ link (seen briefly in the gif above) but was unable to create an accessible menu!

Here is where the menu goes wrong &mdash; it only shows the sub menu when the parent menu item is being hovered over:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb57d856-e82d-498e-88fb-6730e8f76a04/kinetico-displays-menu-on-hover.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb57d856-e82d-498e-88fb-6730e8f76a04/kinetico-displays-menu-on-hover.png" sizes="100vw" caption="" alt="Kinetico’s menu displays submenus on hover" >}}

Fixing it is easier said than done. In most cases, you can just "double up" your selector to apply to focus too:

<pre><code class="language-css">li:hover .nav_sub_menu,
li:focus .nav_sub_menu {
}
</code></pre>

But this doesn’t work in this case because whilst the `<li>` element is hoverable, it isn’t focusable. It’s the <em>link</em> inside the `<li>` that is focusable. But the submenu isn’t inside the link, it’s <em>next</em> to it, so we need to apply the sibling selector to show the submenu when the link is in focus.

<pre><code class="language-css">li:hover .nav_sub_menu,
a:focus + .nav_sub_menu {
}
</code></pre>

This tweak means we can see our submenu when we tab to the parent menu item on the keyboard. But what happens when you try to tab into the submenu?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b745bec-e739-4084-8c4f-26ea60ea81ec/funny-tab-behaviour-menus.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b745bec-e739-4084-8c4f-26ea60ea81ec/funny-tab-behaviour-menus.gif" width="600" height="229" alt="We can never tab to the ‘Frozen food’ child link of ‘Browse by Type’." /></a><figcaption>We can never tab to the ‘Frozen food’ child link of ‘Browse by Type’. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b745bec-e739-4084-8c4f-26ea60ea81ec/funny-tab-behaviour-menus.gif">Large preview</a>)</figcaption></figure>

When we tab from the parent menu item, the focus shifts to the first link in the child menu as expected. But this moves focus *away* from the parent menu link, meaning the submenu gets hidden and the child menu items are removed from the tab order again!

This is a problem that can be solved with `:focus-within`, which lets you apply styling to a parent element if it *or any of its child elements* has the focus. So, in this case, we have to triple up:

<div class="break-out">

<pre><code class="language-css">li:hover .nav_sub_menu, /* hover over parent menu item, show child menu */
a:focus + .nav_sub_menu, /* focus onto parent menu item, show child menu */
.nav_sub_menu:focus-within { /* focus onto child menu item, keep showing child menu  */
}
</code></pre></div>

Our menu is now fully keyboard-accessible through pure CSS. I love creative CSS solutions, but a word of warning here: quite a lot "CSS-only" solutions in the wild fall down when it comes to keyboard navigation. Avoiding JavaScript doesn't necessarily make a site more accessible.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0af620d-ebc0-414a-8d43-c2c66f832c9f/funny-tab-behaviour-menus-fixed.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0af620d-ebc0-414a-8d43-c2c66f832c9f/funny-tab-behaviour-menus-fixed.gif" width="600" height="262" alt="We can now tab through all the submenu items." /></a><figcaption>We can now tab through all the submenu items. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0af620d-ebc0-414a-8d43-c2c66f832c9f/funny-tab-behaviour-menus-fixed.gif">Large preview</a>)</figcaption></figure>

In fact, a JS-driven menu might be a better shout in this case, as browser support for this solution is still quite poor. `:focus-within` can currently only be used in Chrome, Firefox, and Safari. Even in Chrome, I found it to be incompatible with the `display: none` logic used to show/hide the child menu; I had to hide my menu items by setting `opacity: 0` instead.

OK, I’m done for the day. It’s now time to wind down with a bit of social media.

## Facebook

Facebook does an incredible job here, providing a masterclass in keyboard accessibility.

On the very first <kbd>TAB</kbd> press, a hidden menu opens up, providing shortcuts to the most popular sections of the current page and links to other popular pages.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c98c519-5e95-4d52-95d9-985856d80d19/facebook-hidden-menu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c98c519-5e95-4d52-95d9-985856d80d19/facebook-hidden-menu.png" sizes="100vw" caption="Facebook hidden menu exposing accessibility options (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c98c519-5e95-4d52-95d9-985856d80d19/facebook-hidden-menu.png'>Large preview</a>)" alt="Facebook hidden menu exposing accessibility options" >}}

When you cycle through the page sections using the arrow keys, those sections are highlighted visually so that you can see where you would be tabbing to.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb992fe-e166-4caa-8282-db3f916ee684/navigate-facebook-option.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb992fe-e166-4caa-8282-db3f916ee684/navigate-facebook-option.png" sizes="100vw" caption="When I focus on the ‘Navigate Facebook’ option in the dropdown, the corresponding section is highlighted in blue. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb992fe-e166-4caa-8282-db3f916ee684/navigate-facebook-option.png'>Large preview</a>)" alt="When I focus on the ‘Navigate Facebook’ option in the dropdown, the corresponding section is highlighted in blue" >}}

The most useful feature is that Facebook provides a <kbd>OPT</kbd> + <kbd>/</kbd> (or <kbd>ALT</kbd> + <kbd>/</kbd>) shortcut to get back to the menu at any time, making use of the [aria-keyshortcuts attribute](https://www.maxability.co.in/2018/03/aria-keyshortcuts-property/).

<div class="break-out">

<pre><code class="language-html">&lt;div class="a11y-help"&gt;
  Press opt + / to open this menu
&lt;/div&gt;

&lt;div aria-label="Navigation Assistant" aria-keyshortcuts="Alt+/" role="menubar"&gt;
  &lt;a class="screen-reader-shortcut" tabindex="1" href="#main-content"&gt;
    Skip to main content
  &lt;/a&gt;
&lt;/div&gt;
</code></pre></div>

Unlike the ‘skip to main content’ link, which is built on top of native anchoring technology and "just works", the `aria-keyshortcuts` attribute requires the author to implement all the keyboard behavior, so you’re going to have to write some custom JavaScript if you want to use this.

Here is some JS which hides and shows the `menubar` area, which is a useful starting point:

<div class="break-out">

<pre><code class="language-javascript">const a11yArea = document.querySelector('*[role="menubar"]');
document.addEventListener('keydown', (e) => {
  if (e.altKey && e.code === 'Slash') {
    a11yArea.style.display = a11yArea.style.display === 'block' ? 'none' : 'block';
  }
});
</code></pre></div>

## Summary

This experiment has been a mixed bag of great keyboard experiences and poor ones. I have three main takeaways.

### Keep It Stylish

By *far* the most common keyboard accessibility issue I’ve faced today is a lack of focus styling for tabbable elements. Suppressing native focus styles without defining any custom focus styles makes it extremely difficult, even impossible, to figure out where you are on the page. Removing the outline is such a common faux pas that there’s even [a site dedicated to it](https://www.outlinenone.com/).

Ensuring that native or custom focus styling is visible is the single most impactful thing you can do in the area of keyboard accessibility, and it’s often one of the easiest; a simple case of doubling up selectors on your existing `:hover` styling. If you only do one thing after reading this article, it should be to search for `outline: 0` and `outline: none` in your CSS.

### Semantics Are Key

How many times have you tried opening a link in a new tab, only for your *current* window to get redirected? It happens to me every now and again, and annoying as it is, I’m lucky that it’s one of the only usability issues I tend to face when I use the web. Such issues arise from misusing the platform.

Let’s look at this code here:

<pre><code class="language-html">&lt;span onclick="window.location = 'https://google.com'"&gt;Click here&lt;/span&gt;
</code></pre>

An able, sighted user would be able to click on the  `<span>` and be redirected to Google. However, because this is a `<span>` and not a link or a button, it doesn’t automatically have any focusability, so a keyboard or screen reader would have no way of interacting with it.

Keyboard-users are standards-reliant users, whereas the able, sighted demographic is privileged enough to be able to interact with the element despite its non-conformance.

Use the native features of the platform. Write good, clean HTML, and use validators such as [https://validator.w3.org](https://validator.w3.org/) to catch things like missing `href` attributes on your anchors.

### Content Is Key

You may be required to display cookie notices, subscription forms, adverts or adblock notices.

Do what you can to make these experiences unobtrusive. If you can't make them unobtrusive, at least make them dismissible.

Users are there to see your content, not your banners, so put these dismissible elements first in your DOM so that they can be quickly dismissed, or fall back to using `tabindex="1"` if you can't move them.

Finally, support your users in getting to your content as quickly as they can, by implementing the Holy Grail of ‘skip to main content’ links.

Stay tuned for the next article in the series, where I will be building upon some of these techniques when I use a screen reader for a day.

{{< signature "rb, ra, il" >}}
