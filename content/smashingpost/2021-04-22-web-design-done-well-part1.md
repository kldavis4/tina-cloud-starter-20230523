---
title: 'Web Design Done Well: The Ordinary Made Extraordinary'
slug: web-design-done-well-part1
author: frederick-o-brien
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/991d819c-d174-4d53-b92f-4981f9da4d84/web-design-done-well-part1.jpg
date: 2021-04-22T14:00:00.000Z
summary: >-
  Sometimes it’s the little things in web life that make us look twice. From carousels to documentation to cookie disclaimers, here are some sites taking the mundane and sprinkling in a little magic.
description: >-
  Sometimes it’s the little things in web life that make us look twice. From carousels to documentation to cookie disclaimers, here are some sites taking the mundane and sprinkling in a little magic.
categories:
  - Design
  - User Experience
  - Accessibility
  - Web Design
  - CSS
---

Great ideas in web design come so thick and fast that it can be easy to miss them if you’re not careful. This series is a small antidote to that, piecing together splashes of inspiration that caught our eye. Whether it’s a mind-bending new feature or simply an old trick delivered with new elegance, they share the quality of making us think a little differently.

I recently wrote a piece lauding [the work of Saul Bass in the world of web design](https://www.smashingmagazine.com/2021/02/saul-bass-teach-web-design/). One of his great gifts was making even the tiniest details beautiful. It is in that same spirit we kick off this series by honing in on website trends and features we’ve grown accustomed to being dull. As you’ll see, they needn’t be. The trick is often in the execution. Just about anything can be beautiful. Why aim for anything less?

{{< refs >}}
    <h4 style="margin-top: 1.25em">Part Of: Web Design Done Well</h4>
    <ul>
    <li><strong>Part 1: The Ordinary Made Extraordinary</strong></li>
    <li><a href="https://www.smashingmagazine.com/2021/06/web-design-done-well-audio/">Part 2: Making Use Of Audio</a></li>
    <li><a href="https://www.smashingmagazine.com/2021/09/web-design-done-well-excellent-editorial/">Part 3: Excellent Editorial</a></li>
    <li>Also, <a href="/the-smashing-newsletter/">subscribe to our newsletter</a> to not miss the next ones.</li>
</ul>
{{< /refs >}}

## Glasgow International’s Pages Within Pages

We’re used to plenty of scrolling these days, but [the Glasgow International festival website](https://glasgowinternational.org/) has found a simple, clever way to scratch that itch while keeping pages short:

{{< rimg href="https://glasgowinternational.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/139771eb-a769-4458-a850-4f9685ce1351/5-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="376" sizes="100vw" caption="On desktop, the <a href='https://glasgowinternational.org/'>Glasgow International</a> homepage lines up its three main sections side by side and allows them to be scrolled through independently of each other. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/139771eb-a769-4458-a850-4f9685ce1351/5-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="the Glasgow International festival website" >}}

On mobile, the same three sections form one big column. It’s a savvy solution to the mobile/desktop relationship, and a pretty stylish one too. (Shout out to the ‘Support’ button, which starts spinning when you hover on it.)

The CSS behind this is suitably simple. The three sections sit inside a flex container, with all three sharing the values of `overflow-y: auto;` and `height: 100vh;` so that they always fit the desktop viewport. The really nice touch here is using `scrollbar-width: auto;` to remove the sidebar. Because the columns take up the whole screen you intuitively work out the way the page works as soon as you move your mouse.

{{% feature-panel %}}

## Kenta Toshikura’s Dimension-Bending Portfolio

A recent site of the week on Awwwards, this [portfolio website by Japanese frontend developer Kenta Toshikura](https://kentatoshikura.com/) is simply breathtaking:

{{< rimg href="https://kentatoshikura.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02172e03-5137-4cb0-bcf9-f68b816aa350/7-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="600" sizes="100vw" caption="The landing page’s 3D carousel on <a href='https://kentatoshikura.com/'>Kenta Toshikura</a>’s homepage is so elegantly done that you almost think it possible to fall through the screen and into an alternate CSS dimension. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02172e03-5137-4cb0-bcf9-f68b816aa350/7-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="portfolio website by Japanese frontend developer Kenta Toshikura" >}}

If in doubt, the tendency is to lean towards flat, modular arrangements, but maybe we should be **thinking in three dimensions** a little more often. This is a fantastic example of lateral thinking transforming what could easily have been a column of boxes into something truly memorable. 

We may not all be equipped to do something quite this fancy (I’m certainly not) but it’s well worth remembering that web pages aren’t blank canvases so much as they are windows into alternate dimensions.  

## Stripe Documentation Is The Teacher We All Want

Documentation is all too often one of the first casualties of the Web’s mile-a-minute pace. It needn’t be. I have no qualms calling [Stripe](https://stripe.com/docs)’s documentation beautiful:

{{< rimg breakout="true" href="https://stripe.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04af1cd-b23b-40fd-9072-d7d12494f4ab/3-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="376" sizes="100vw" caption="The instructions on <a href='https://stripe.com/'>Stripe.com</a> are accompanied by fully fledged code previews, with different lines highlighted depending on the section you’re reading. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f04af1cd-b23b-40fd-9072-d7d12494f4ab/3-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="Stripe’s documentation website" >}}

I’m sure most of us have ground through enough bad documentation to appreciate the effort put into this approach. Clear, hierarchical navigation for the content, bite-sized step-by-step-copy, and of course the code snippets. Dynamic previews of code across multiple platforms and languages is above and beyond, but then why shouldn’t it be? 

There are few things more valuable &mdash; and more elusive &mdash; than quality learning resources. Stripe shows there is **a world of possibilities** online beyond the standard words on a page. I’ve shared this before (and I’ll share it again) but [Write the Doc’s documentation guide](https://www.writethedocs.org/guide/) is a smashing resource for presenting informative content in useful, dynamic ways. 

## Max Böck’s Technicolor Dream

There is an awful lot to like about [Max Böck’s personal website](https://mxb.dev/), but for the purposes of this piece, I’m honing in on color schemes. Most websites have one color scheme.

{{< rimg breakout="true" href="https://mxb.dev/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c47b3c5-01d4-4701-a031-a5446332ce79/4-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="376" sizes="100vw" caption="A small but growing number are branching out into a dark mode, bringing their tally up to two. <a href='https://mxb.dev/'>Max Böck</a> has ten. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c47b3c5-01d4-4701-a031-a5446332ce79/4-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="Max Böck’s personal website" >}}

Light and dark is the new normal, but as Böck himself writes in [his blog post about the theme switcher](https://mxb.dev/blog/color-theme-switcher/), only Siths deal in absolutes. Through the magic CSS custom properties the site switches between **color schemes** seamlessly. For a full breakdown of how it works I heartily recommend reading the full post linked above. And for further reading on custom properties *Smashing* has plenty too:

- “[How To Configure Application Color Schemes With CSS Custom Properties](https://www.smashingmagazine.com/2020/08/application-color-schemes-css-custom-properties/)” by Artur Basak
- “[A Strategy Guide To CSS Custom Properties](https://www.smashingmagazine.com/2018/05/css-custom-properties-strategy-guide/)” by Michael Riethmuller

The themes are named after *Mario Kart 64* tracks, if you were wondering. Except Hacker News. That’s named after [Hacker News](https://news.ycombinator.com/), with the marvellous touch of adding ‘considered harmful’ to the end of every single Böck blog post title.

It’s a fun twist on the traditional light/dark dichotomy, and also speaks to just **how fluid sites can be nowadays**. The same groundwork could allow you to adjust color schemes depending on where people are visiting the site from, for example. 

{{% ad-panel-leaderboard %}}

## Overpass Sells Sales

Sales isn’t exactly a sector that screams innovation, but credit where credit is due. [Overpass](https://www.overpass.com/)’s carousels bounce and shrink and expand so smoothly that it almost feels like you’re interacting with something tactile, like a rubber band.

{{< rimg breakout="true" href="https://www.overpass.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f74fb9f-1313-4362-984e-def1c2e5bfa6/2-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="376" sizes="100vw" caption="<a href='https://www.overpass.com/'>Overpass</a>’s website is colorful, fast, and dynamic. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f74fb9f-1313-4362-984e-def1c2e5bfa6/2-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="Overpass’s website" >}}

Here, both the [`touch-action`](https://developer.mozilla.org/en-US/docs/Web/CSS/touch-action) and [`translate3d()`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate3d()) CSS functions are used to great effect, making the cards container something that can be effectively dragged around the screen. In the event of the container being grabbed, all cards use [`scale(0.95)`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/scale()) to recede ever so slightly until the user lets go. It gives the carousel a lovely sense of depth and lightness.

The audio clips are a nice touch. **Multimedia integration** has been a running theme in these examples. Always lay the accessibility groundwork, but be bold. At this stage the only real limits are those of our imaginations. 

## E-Commerce Meets Long Form Storytelling On Mammut

From Steve Jobs to Seth Godin, it is often said **marketing is a storytelling game**. This is something that a lot of e-commerce websites seem to have forgotten, each serving up page after page of glossy products floating in front of perfect white backgrounds. You can almost hear the sucking sound of conversion funnels trying to draw you in.

It’s refreshing then to see a company like [Mammut going all in on storytelling](https://eiger-extreme.mammut.com/en) to sell its hiking products. Their long-form expedition articles are as immersive as the finest *New York Times* feature, with audio clips, maps, and, naturally, stunning photography. Mammut gear features heavily, of course, but it’s done in a way that’s tasteful. More importantly than that, it’s *authentic*.

{{< rimg breakout="true" href="https://eiger-extreme.mammut.com/en" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e11d26fc-d5e8-4df1-a442-a76d0ddcd240/6-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="376" sizes="100vw" caption="<a href='https://eiger-extreme.mammut.com/en'>Mammut</a> puts human experience front and center. Yes, they still want to sell you stuff, but they also want to celebrate the adventures that stuff can be a part of. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e11d26fc-d5e8-4df1-a442-a76d0ddcd240/6-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="Mammut’s website" >}}

Although there is some super slick styling going on here that’s not why I’ve included it. In a way it’s incredible just how impersonal much of the Web feels these days, with e-commerce being a particularly egregious offender.

This is the kind of thing people would share even if they had no interest in buying mountaineering gear. It’s superb content. Instagram influencer posts look like child’s play compared to this. Do those prompts to shop take you to the aforementioned squeaky clean e-commerce checkout? Naturally. But, by God do they earn it. Not everyone has the resources for something this cutting edge, but it shows that **e-commerce doesn’t have to be sterile and lifeless**.  

{{% ad-panel-leaderboard %}}

## Axeptio Makes Its Cookies Palatable

You can’t swing a cat without hitting a disclaimer pop-up these days. It’s bizarre, then, that so many of them are so ugly. More often than not, they feel tacked on and graceless. Now, to be fair, that’s because they are tacked on and graceless, but some genuinely are just there to Improve Your Browsing Experience™.

Instead of treating its **cookie pop-up** like a bad odour, web consent solution provider [Axeptio](https://www.axeptio.eu/en/home) walks the walk by making them look stylish, and even rather charming. With [GDPR](https://www.smashingmagazine.com/2021/03/state-gdpr-2021-cookie-consent-designers-developers/) (and [basic decency](https://www.smashingmagazine.com/2020/02/ethical-design-handbook-prerelease/)) to think about, it’s essential to weave ethical design into a website’s fabric.

{{< rimg breakout="true" href="https://www.axeptio.eu/en/home" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbe14307-f3a2-4188-a14b-a54872b6b031/1-websites-inspiring-us-to-think-differently-part-1.png" width="800" height="376" sizes="100vw" caption="<a href='https://www.axeptio.eu/en/home'>Axeptio</a> shows a great example of data transparency. No walls of legal jargon, no near-impossible opt-out system &mdash; just clear info on what the data is being used for.  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbe14307-f3a2-4188-a14b-a54872b6b031/1-websites-inspiring-us-to-think-differently-part-1.png'>Large preview</a>)" alt="Axeptio’s website" >}}

A lovely touch is that it doesn’t actually pop up until users start moving around the site. Why bother people if they’re not even interested in the content? Notice as well that they’ve dropped the **boilerplate cookie** lingo in favor of something more conversational.

Granted, this may not make the mundane ‘extraordinary’ exactly, but it does **make it a whole lot classier**. It’s a small touch, but one which makes an excellent first impression. Without even touching my mouse, I already have a sense of Axeptio’s attention to detail and commitment to quality. A blocky ‘We care about your privacy’ pop-up would have given a very different impression. 

As far as cookies and pop-ups are necessary, we may as well own them. The same applies to other unsexy staples of the modern web. Do legal consent forms, email signups, and privacy pages have to be ugly and evasive, or do we just **need to think a little differently**? Share your thoughts below!

{{< signature "vf, yk, il" >}}
