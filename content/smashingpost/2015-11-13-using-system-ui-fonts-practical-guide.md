---
title: 'Using UI System Fonts In Web Design: A Quick Practical Guide'
slug: using-system-ui-fonts-practical-guide
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc246ff9-d8cd-4f51-9836-ce2528cdc5f0/01-modern-system-fonts.png
date: 2015-11-13T00:45:22.000Z
author: marcinwichary
description: >-
  For perhaps the first time since the original Macintosh, we can get excited
  about using system UI fonts. They’re an interesting, **fresh alternative to
  web typography** — and one that doesn’t require a web-font delivery service or
  font files stored on your server. How do we use system UI fonts on a website,
  and what are the caveats?

  System UI fonts being amazing kind of snuck up on us. Google has been toiling
  away at Roboto with great success (including regular updates), Apple made a
  splash with San Francisco, and Mozilla asked renowned type designer Erik
  Spiekermann to create Fira Sans.
categories:
  - Typography
  - Fonts
  - CSS
---
For perhaps the first time since the original Macintosh, we can get excited about using system UI fonts. They’re an interesting, <strong>fresh alternative to web typography</strong> — and one that doesn’t require a web-font delivery service or font files stored on your server. How do we use system UI fonts on a website, and what are the caveats?

System UI fonts being amazing kind of snuck up on us. Google has been toiling away at <a href="https://www.google.com/design/spec/style/typography.html">Roboto</a> with great success (including <a href="https://www.fastcodesign.com/3033126/roboto-rebooted-why-google-plans-to-update-its-font-like-the-rest-of-its-products">regular updates</a>), Apple made a splash with <a href="https://developer.apple.com/fonts/">San Francisco</a>, and Mozilla asked renowned type designer Erik Spiekermann to create <a href="https://mozilla.github.io/Fira/">Fira Sans</a>. Last but not least, let us not forget about Microsoft. It was Microsoft that restarted conversations about system UI fonts with its original Windows Phone design language (née Metro), which relied heavily on typography in general, and on a font named <a href="https://en.wikipedia.org/wiki/Segoe">Segoe</a> in particular.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc246ff9-d8cd-4f51-9836-ce2528cdc5f0/01-modern-system-fonts.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/945657ad-92ed-4af4-9e77-84db319013c5/01-modern-system-fonts-preview.png" alt="System Fonts - The latest generation of system UI fonts and their allegiances" width="500" height="203" /></a><figcaption>The latest generation of system UI fonts and their allegiances. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc246ff9-d8cd-4f51-9836-ce2528cdc5f0/01-modern-system-fonts.png">View large version</a>)</figcaption></figure>

No wonder that the idea of using those fonts is spreading through the web world as well. Whether you want your website to feel more like an app, to draw clearer lines between the content and user interface, or to <strong>use modern, beautiful fonts with zero latency</strong>, you might be interested in using system UI fonts on your website.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Tools And Resources For A More Meaningful Web Typography</span>](https://www.smashingmagazine.com/2016/03/meaningful-web-typography/)
*   [Guide to CSS Font Stacks: Techniques and Resources](https://www.smashingmagazine.com/2009/09/complete-guide-to-css-font-stacks/)
*   [Whitespace Characters in Unicode & HTML](https://www.smashingmagazine.com/2015/10/space-yourself/#all-together-now)
*   [Balancing Line Length And Font Size In RWD](https://www.smashingmagazine.com/2014/09/balancing-line-length-font-size-responsive-web-design/)

{{% feature-panel %}}

But it’s not as easy as it could be. That’s because the CSS support is <strong>curiously schizophrenic</strong>.

(Nomenclature note: I am using “system UI font” here to refer to the font that the user interface of the operating system is rendered in — distinct from a “system font,” a traditional name for any local or platform font that is already present on the user’s system and that doesn’t need to be included in the website’s payload.)

## Two Approaches to system fonts

Currently, there are two approaches to making your website use the system UI font for its typography.</p>

### Approach A

Approach A is to use the “magical” shorthand CSS property:

<pre><code class="language-css">font: menu;
</code></pre>

A <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/font">few of these shorthand properties</a> have existed for the longest time (<code>caption</code>, <code>icon</code>, <code>menu</code>, <code>message-box</code>, <code>small-caption</code>, <code>status-bar</code>), yet I have never seen them being commonly used.

Approach A has its drawbacks:

*   It **doesn’t return a correct font on iOS**, nor in many Android browsers.
*   It’s a shorthand, which means it **overrides the font size** (although that can be reset), and it cannot be combined with and does not fall back to anything else.
*   Until December 2015 in Firefox on Mac OS X, it **doesn’t use the “smart” properties of San Francisco** (which switches from San Francisco Text to San Francisco Display automatically for text over 20 pixels and adjusts letter spacing).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d237c343-5439-4331-b233-4827caa891bd/02-history-mac.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39fb63e1-f657-4440-ba82-fbe5fc8b6518/02-history-mac-preview.png" alt="System Fonts - Mac OS X system UI fonts over the ages: from Chicago in 1984, through Charcoal and Lucida Grande, to San Francisco on a high-resolution display in 2015" width="500" height="285" /></a><figcaption>Mac OS X system UI fonts over the ages: from Chicago in 1984, through Charcoal and Lucida Grande, to San Francisco on a high-resolution display in 2015. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d237c343-5439-4331-b233-4827caa891bd/02-history-mac.png">View large version</a>)</figcaption></figure>

### Approach B

Approach B is to list fonts by name:
<pre class="language-css"><code>font-family: -apple-system, BlinkMacSystemFont, 
    "Segoe UI", "Roboto", "Oxygen", 
    "Ubuntu", "Cantarell", "Fira Sans", 
    "Droid Sans", "Helvetica Neue", sans-serif;</code>
</pre>

This, too, has its drawbacks:

*   You’ll have to **maintain the list** (and its order). Perhaps system UI fonts won’t change as often as they did in the last few years — but in any case, this is not future-proof.
*   The list targets the most popular browsers and operating systems, but it **doesn’t target all of them**.
*   It doesn’t yet work in Firefox on Mac OS X El Capitan, resulting in Neue Helvetica being shown, rather than San Francisco. (This is slated to be fixed in December 2015.)
*   This solution is prone to naming conflicts, which led to a very interesting [bug with the system font on Medium](https://medium.com/@mwichary/system-shock-6b1dc6d6596f). Also, for example, Oxygen ([KDE’s UI font](https://www.google.com/fonts/specimen/Oxygen)) is the name of [another font](https://www.identifont.com/show?HYN) that people can install, which can lead to [surprises](https://twitter.com/zipboing/status/659744396431261696). Also, if you are a developer and happen to have installed Roboto or Fira Sans on your machine, then this font declaration might use one of those instead of the system’s actual UI font.
*   Mac OS 10.0 to 10.9 uses Lucida Grande as the system UI font. Mac OS 10.10 uses Neue Helvetica. However, all versions of Mac OS X have both of these fonts installed. Because the `font-family` declaration works by sequentially going through the list of fonts to find the first one installed, choosing Lucida Grande on some platforms and Neue Helvetica on others is impossible. The first available one listed in the declaration will always be chosen.</p>

## Other Approaches

You might be inclined to combine approach A with approach B to get the best of both worlds. Unfortunately, this is not easy because the <code>font</code> and <code>font-family</code> properties are <strong>mutually exclusive</strong> — one will just override the other. Perhaps media queries can come to the rescue, but that’s hacky.

You might also imagine sending different CSS values from the server, depending on the user agent (for example, sending only <code>font-family: "Fira Sans", sans-serif;</code> if we know the browser is running on Firefox OS), or doing it via JavaScript. But this seems cumbersome and hard to maintain, and it still doesn’t solve all of our problems.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dfb4d9a-fdd1-49d5-bc44-b3941f93587f/03-two-sites.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48cd641e-d475-4e25-9890-739d69aaf703/03-two-sites-preview.png" alt="You can use the system UI font just for the user interface (on the left, medium.com) or for the entire website (on the right, colepeters.com). Note, however, that many system UI fonts are not optimized for longer content." /></a><figcaption>You can use the system UI font just for the user interface (on the left, <a href="https://medium.com/">Medium</a>) or for the entire website (on the right, <a href="https://colepeters.com/">Cole Peters</a>). Note, however, that many system UI fonts are not optimized for longer content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dfb4d9a-fdd1-49d5-bc44-b3941f93587f/03-two-sites.png">View large version</a>)</figcaption></figure>

## What To Do Today?

I work at Medium, and currently we use approach B:
<pre class="language-css"><code>font-family: -apple-system, BlinkMacSystemFont, 
    "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", 
    "Fira Sans", "Droid Sans", "Helvetica Neue", 
    sans-serif;</code>
</pre>

We chose this approach because it seems to have fewer major problems. (Approach A fails in mobile browsers in ways that are unacceptable. Approach B fails, too, but less often and with fewer consequences. Your mileage may vary.)

You and I can make this even better together. The box below uses the declaration above and should render in your system’s UI font. If it doesn’t or if you have any thoughts, please leave a comment!
<blockquote style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif; font-style: inherit;">This should be rendered in your system’s UI font.
The quick brown fox jumps over the lazy dog.</blockquote>

## Details Of Approach B

If you are interested in the details, let’s work through how this list got to look the way it does:
<pre class="language-css"><code>font-family:
/* 1 */ -apple-system, BlinkMacSystemFont,
/* 2 */ "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans",
/* 3 */ "Helvetica Neue", sans-serif;</code>
</pre>

The first grouping is CSS properties that map to the system’s UI font. That covers a lot of ground, and there is no chance that these fonts will be mistaken for something else:

*   `-apple-system` targets San Francisco in Safari on Mac OS X and iOS, and it targets Neue Helvetica and Lucida Grande on older versions of Mac OS X. It properly selects between San Francisco Text and San Francisco Display depending on the text’s size.
*   `BlinkMacSystemFont` is the equivalent for Chrome on Mac OS X.

The second grouping is for known system UI fonts:

*   `Segoe UI` targets Windows and Windows Phone.
*   `Roboto` targets Android and newer Chrome OS’. It is deliberately listed after Segoe UI so that if you’re an Android developer on Windows and have Roboto installed, Segoe UI will be used instead.
*   `Oxygen` targets KDE, `Ubuntu` targets… well, you can guess, and `Cantarell` targets GNOME. This is beginning to feel futile because some Linux distributions have many of these fonts.
*   `Fira Sans` targets Firefox OS.
*   `Droid Sans` targets older versions of Android.
*   Note that we don’t specify San Francisco by name. On both iOS and Mac OS X, San Francisco isn’t obviously accessible, but rather exists as a “hidden” font.
*   We also don’t specify San Francisco using `.SFNSText-Regular`, the internal PostScript name for San Francisco on Mac OS X. It only works in Chrome and is less versatile than `BlinkMacSystemFont`.

The third grouping is our fallback fonts:

*   `Helvetica Neue` targets pre-El Capitan versions of Mac OS X. It is listed close to the end because it’s a popular font on other non-El Capitan computers.
*   `sans-serif` is the default sans-serif fallback font.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40a421da-9acb-4feb-a806-c1e3b2afe24a/04-history-win.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e0ebd26-a1e8-4e48-95b5-dd2b4a7fedaa/04-history-win-preview.png" alt="The evolution of Windows’ system UI font is even more drastic than Mac OS X’s — from monospaced bitmapped fonts in Windows 1.0 in 1985 to the high-resolution Segoe UI in Windows 10." /></a><figcaption>The evolution of Windows’ system UI font is even more drastic than Mac OS X’s — from monospaced bitmapped fonts in Windows 1.0 in 1985 to the high-resolution Segoe UI in Windows 10. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40a421da-9acb-4feb-a806-c1e3b2afe24a/04-history-win.png">View large version</a>)</figcaption></figure>

Here are the currently known problems with this approach:

*   In Firefox on Mac OS X, San Francisco has tighter letter spacing than on Safari and Chrome.
*   It doesn’t render Lucida Grande on pre-Yosemite versions of Mac OS X, falling back to Neue Helvetica. And it might not match the correct font on less popular operating systems or more complicated configurations.

## The Future

There’s still work to do. Everything we’ve covered works only for Western typography. Also, if you want to adjust the padding or line height according to the UI font that your website is using, then you’ll have to use the hybrid approach above or else <a href="https://www.bramstein.com/writing/detecting-system-fonts-without-flash.html">detect the font after rendering</a>.

Still, the early results are already good enough. Hopefully, in the future, all of this will become less complicated. If any of this is important to you, please <a href="https://www.smashingmagazine.com/2011/09/help-the-community-report-browser-bugs/">tell browser vendors!</a>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/380fe834-38f5-47fe-a8c8-deb700353f5a/05-recent-mac-os.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2016f829-e678-41c0-91c3-9d22a7878497/05-recent-mac-os-preview.png" alt="The last three versions of Mac OS X use three different system UI fonts: Lucida Grande on Mac OS 10.9 (Mavericks); a special version of Neue Helvetica on Mac OS 10.10 (Yosemite); and a special version of San Francisco on Mac OS 10.11 (El Capitan). It’s safe to assume that future versions will continue using San Francisco." /></a><figcaption>The last three versions of Mac OS X use three different system UI fonts: Lucida Grande on Mac OS 10.9 (Mavericks); a special version of Neue Helvetica on Mac OS 10.10 (Yosemite); and a special version of San Francisco on Mac OS 10.11 (El Capitan). It’s safe to assume that future versions will continue using San Francisco. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/380fe834-38f5-47fe-a8c8-deb700353f5a/05-recent-mac-os.png">View large version</a>)</figcaption></figure>

## Further Reading

*   “[I Left My System Fonts in San Francisco](https://furbo.org/2015/07/09/i-left-my-system-fonts-in-san-francisco/),” Craig Hockenberry
*   [System Shock: A Story of a 25-Year-Old Font Coming Back With a Vengeance](https://medium.com/@mwichary/system-shock-6b1dc6d6596f),” Marcin Wichary, Medium

<em>Thanks to John Daggett, Michael Duggan, Kenneth Ormandy and Emil Eklund for their help with this article.</em>

{{< signature "vf, al" >}}

