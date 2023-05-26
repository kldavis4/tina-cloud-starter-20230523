---
title: 'What We Wished For'
slug: internet-explorer-what-we-wished-for
author: mat-marquis
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9b482c8-6fc1-48d4-97ae-da5d9c323e61/sharing-card-marquis.png
date: 2018-12-24T14:30:46+01:00
summary: >-
  An old cliché says that “may you get everything you wish for” makes for a particularly insidious curse. With Edge soon making the switch to Chrome’s rendering engine &mdash; well, for better or worse, a bitter wish is coming true.
description: >-
  An old cliché says that “may you get everything you wish for” makes for a particularly insidious curse. With Edge soon making the switch to Chrome’s rendering engine &mdash; well, for better or worse, a bitter wish is coming true.
categories:
  - Opinion Column
  - Browsers
  - Usability
  - Internet Explorer
---
I think we’re headed for trouble, though I can’t say for sure. Trouble &mdash; trouble I *know*. The on-ramp to it, though; I’ve only heard about that. I’ve only been doing this for ten years. I missed all the lead-up the last time around. What I can say for sure &mdash; what I know from experience &mdash; is that I’ve never had a wish made in anger come true without regretting it.

Ten years (I don’t mind saying) is a pretty long time. Back when I first truth-stretched my way into a web design internship, good ol’ Internet Explorer was already a laughingstock.

<blockquote>“If you notice that a piece of your content appears and disappears, and sections of the page only get half-drawn, these are good indications that an element requires a layout. [...] A <code>hasLayout</code> fix involves nothing more than declaring a CSS property that causes an element to gain a layout, when it wouldn’t ordinarily have a layout by default.”<br /><br />&mdash; <a href="https://www.sitepoint.com/internet-explorer-haslayout-property/">The Internet Explorer hasLayout Property</a></blockquote>

I hated IE. I feel like I can cop to that now. I tried not to; I really, sincerely did. I’d tell people it was *fun* to support, if you can believe it.

As all the other browsers got easier and easier to deal with, I attempted to convince myself that there was at least still a *challenge* to quirky old IE. That even became something of a point of pride: I had gotten so good at fixing obscure IE issues that I’d learned to dodge them during the course of my everyday development, leaving nothing (well, less) to dread come the big “open it up in IE and see what broke” phase.

{{% feature-panel %}}

It’s fun, in a way. *Fun*. That was the lie I told myself.

<pre><code class="language-css">/* Fixes #2588: When Windows Phone 7.5 (Mango) tries
to calculate a numeric opacity for a select (including
"inherit") without explicitly specifying an opacity on
the parent to give it context, a bug appears where
clicking elsewhere on the page after opening the select
will open the select again. */</code></pre>
<p>&mdash; <a href="https://github.com/jquery/jquery-mobile/blob/591f10c0e00e2a90fc00055d32cc0a0448ebf65c/css/structure/jquery.mobile.forms.select.css#L14">jQuery Mobile source</a></p>

I hated it. I full-on, bad-jokes-in-a-conference-talk hated IE, in every one of its incarnations. I hated it every bit as much everybody else did.

<blockquote>“Internet Explorer 6 has a puzzling bug involving multiple floated elements; text characters from the last of the floated elements are sometimes duplicated below the last float. ... The direct cause is nothing more than ordinary HTML comments, such as, <code>&lt;!-- end left column --&gt;</code>, sandwiched between floats that come in sequence.”<br /><br />&mdash; <a href="https://www.positioniseverything.net/explorer/dup-characters.html">Explorer 6 Duplicate Characters Bug</a></blockquote>

A waste of my goddamned time is what it was. All those hours I spent hunched over a janky virtual machine—reload, wait, throw a nonsense fix at a nonsense bug, reload, *crash*, open IE again, wait, double-check that caching wasn’t a factor, reload, wait, and repeat. I could have been doing so much more with my time &mdash; I could have *learned* so much more.

I was certain that it didn’t just hold back my work, and it didn’t just hold the web back, but it held *me* back, as a developer. On that second point, I guess I wasn’t entirely wrong &mdash; all the obscure IE 6-7 browser bug knowledge I accumulated is all useless now. All I have to show for it are an involuntary flinch at the word “filter,” an inscrutable preference for `padding` over `margin`, and a deep-seated but largely unfounded fear of `z-index`.
​
<blockquote>“...extra whitespace causes the wrong styles to be picked up if the actual class name is a substring (or superstring) of some other class name.”<br /><br />&mdash; <a href="https://old.macedition.com/cb/ie5macbugs/substringbug.html">IE5/Mac whitespace parsing bug</a></blockquote>

I wished it would go away. Uninstalled by a clever and widespread virus, banned by law, Microsoft finally deciding to cut their shoddy rendering engine’s losses and switching to Firefox’s rendering engine, Gecko &mdash; *whatever* &mdash; just *make it go away*. But... no. The web kept evolving and we developers beat on, boats against the current, borne back ceaselessly into the past.

Chrome came along, Firefox kept getting better, new features kept rolling out, the exciting and endless possibilities presented by the advent of responsive web design spread out before us, and also (quick aside) remember that you’ll only have a couple of days to make it all more-or-less work in old IE, so don’t get *too* carried away.
​
<blockquote>“IF you are using IE8, AND you are using the CSS ordered list numbering approach described above, AND the HTML that has the classes that use the <code>counter-reset</code> and <code>counter-increment</code> CSS attributes is HIDDEN when the page loads, THEN whenever that hidden HTML is displayed, ALL of the automatic numbers will be ZERO, BUT ONLY IF THE CSS <code>:hover</code> PSEUDO-CLASS IS USED ON THAT PAGE!”<br /><br />&mdash; <a href="https://fairwaytech.com/2012/02/the-ie8-hover-bug-the-most-awesome-ie-bug-ever/">The IE8 “hover” Bug: The Most Awesome IE Bug Ever?</a></blockquote>

It’s hard to imagine experiencing that kind of frustration nowadays, at least for us relatively-old-timers. Not to say that there isn’t an incredible amount of work involved in tuning things up cross-browser these days, too &mdash; I know all too well that there is. But it’s tough not to feel the occasional pang of, “back in *my* day, all *we* had were floats, and *let me tell you about IE’s double margin bug*,” when you hear about a little difference in how CSS Grid works from one browser to another.

{{% ad-panel-leaderboard %}}

I was wrong; I want to be clear on that point. Not wrong for being frustrated. I don’t think anyone should be blamed for being frustrated with those old browser bugs, same as I don’t think anyone should be blamed for their frustration with any aspect of web development *now*. No, I was wrong for the conclusion that anger brought me to: the desire to see Trident burned to the ground and the earth where it once stood salted. 

I suspect that only one dramatically-ironic thing grows out of that salted earth: those same frustrations, born anew, for a new generation of web developers. When I started my career, scant few years after the browser wars, those seeds had already taken root. Because, for a time &mdash; a time before my own &mdash; we web developers cursed Netscape the same way. The weaker, buggier, inarguably *worse* browser. But Internet Explorer &mdash; developers *loved* that browser. And they wished those *other* browsers &mdash; the *bad* browsers &mdash; would just *go away*: uninstalled by a clever and widespread virus, banned by law, Netscape finally deciding to cut their shoddy rendering engine’s losses and switch to IE’s rendering engine, Trident &mdash; *whatever* &mdash; just *make it go away*. Those inscrutable Internet Explorer bugs didn’t happen by coincidence or negligence. They came about because Internet Explorer had *won*, and we loved it for winning.

See, our frustration and our anger lied to us, as they usually do. They told us that supporting those other, *worse* browsers didn’t just hold back our work, and didn’t just hold the web back, but it held *us* back, as developers. A waste of our goddamned time is what it was. So, we told ourselves that it wasn’t only for *our* own good, but for the good of *the entire web*.

We weighed IE just a little more heavily. We gave it just a little more say in our decisions. And so, holding so many chips, Microsoft played their cards accordingly &mdash; who could blame them? Everyone built websites for them first, and the others second. Their word wasn’t *law*, but it was certainly more than *suggestion*. Sure, they deviated from web standards here and there (just a little bit), but after all, wasn’t something implemented by The Biggest Browser a sort of *de facto* standard anyway? Besides, supporting the better, faster, easier browser was doing the web itself a service! Together with Microsoft, we were pushing the web forward! Everybody wins.

The rendering engine that powers Microsoft’s Edge browser today &mdash; EdgeHTML &mdash; is a fork of gnarly old Trident. It’s a stripped-down and *vastly* improved fork of Trident, for sure, but it isn’t, let’s say, universally judged on its own merit. The EdgeHTML team has always been working with a couple of disadvantages: the first was technical, in that it took a tremendous amount of time and effort to catch up with the likes of Safari, Firefox, and Chrome. The second was emotional. It was us &mdash; you and me &mdash; jaded from years of Internet Explorer, staring down a cheery blue lowercase “e” with cold disdain.

A few weeks ago, the Edge team announced that they’d soon be abandoning EdgeHTML in favor of Blink, the rendering engine that powers Chrome. With this change, the last few remaining embers of Trident will be snuffed out forever. The wish I’d shared with so many will finally be granted. Ironically timed &mdash; as it turns out &mdash; EdgeHTML was becoming a pretty solid rendering engine.

Blink is an open-source project led and governed by Google. It powers both Chrome and Opera, the latter of which similarly abandoned their home-grown rendering engine a few years ago.

By an overwhelming margin, Blink is (and will increasingly be) the way the web is experienced the world over. Blink is fast, stable, packed with modern features, and &mdash; by comparison to development for the still-evolving EdgeHTML &mdash; *painless*.

It may have happened too late to save us from those ancient IE bugs, but our work *will* be easier now that there’s one less rendering engine to support. You and I will lose a little more of our collective “but does it work cross-browser” burden. Our projects will go more smoothly, and the web will lose just a little more of what was once holding it back.

{{% ad-panel-leaderboard %}}

As stewards of the engine powering so very much of the web, well, Google’s word won’t be *law*, but certainly more than *suggestion*. And maybe over the course of the next few years, they’ll deviate from web standards here and there (whether intentionally or accidentally) in the tiniest of ways. But after all, isn’t something implemented by The Biggest Browser a sort of de facto standard itself? Besides, how could you argue? Favoring the better, faster, more powerful browser is doing the web itself a service, after all. Together with Google, we’ll be pushing the web forward. Everybody will win.

That is, as long as little standards deviations and tiny, nagging bugs don’t grow bigger over time &mdash; thanks to the twin forces of entropy and complacency. Unless the decisions we’ve made for the good of the web (hand-in-hand with a notoriously [privacy-hostile advertising company](https://news.bbc.co.uk/2/hi/technology/6740075.stm)) begin to feel a little darker, and a new bogeyman begins to take shape in our minds &mdash; unless we find that our old fears and frustrations have risen again (like a phoenix that renders a couple hundred pixels away from where it should and flickers in a weird way when you scroll).

It doesn’t take much imagination to see newer, more exciting rendering engines appearing over the next handful of years. It takes just as little imagination to see them failing due to lack of support, as we favor “the browser that everyone uses” &mdash; first by choice, and later perhaps in grudging service of “the bottom line.”

Again, though, I don’t know. I’ve never seen this happen with a rendering engine myself. I’ve just heard the whole story, and I only know first-hand how it ends. I know the ending from the ache of old psychic scars; from an involuntary flinch at some bits of code, and muscle-memory that compels me to avoid others. I know it from the jokes in conference talks that always felt a little tired, but still resonated just the same in a way I wouldn’t allow myself to admit and still spoke to a secret wish that I held deep in my heart. A bitter, hateful wish.

But hey, listen. Not anymore. Now, I mean &mdash; I would never. I really do love a good rendering engine bug, now. I do.

<blockquote>“CSS 3D transforms with <code>perspective()</code> are rendered inside out.”<br /><br />&mdash; <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=706231">bugs.chromium.org</a></blockquote>

I mean, that’s actually kind of a fun bug, right? Like, fun in a *way*. Y’know?

It’s fun.

*It’ll be fun*.

{{< signature "dm, ra, il" >}}