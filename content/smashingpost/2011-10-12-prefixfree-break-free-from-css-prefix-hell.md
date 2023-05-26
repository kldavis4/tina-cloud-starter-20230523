---
title: 'PrefixFree: Break Free From CSS Prefix Hell'
slug: prefixfree-break-free-from-css-prefix-hell
image: null
date: 2011-10-12T12:24:04.000Z
author: lea-verou
description: >-
  **Editor's note:** This article is the first piece in our new series
  introducing new, useful and freely available tools and techniques presented
  and released by active members of the Web design community. Lea Verou is
  well-known for her experiments with CSS and JavaScript and in this post she
  presents her recent tool, **prefixfree** which will hopefully help you break
  free from the CSS prefix hell.

  [![prefixfree](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606cb0af-fa8d-47d5-81fd-abe9a5b69b20/prefixfree-main.jpg)](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/)

  The code I write in my live demo slides and presentations doesn’t have any
  prefixes, even for things like `@keyframes` or the `transition` property,
  which aren’t yet supported anywhere prefix-less. To be able to do this, I
  wrote a script that detects the prefix of the current browser and adds it
  where needed. Recently, I thought, why not adapt the script to process all of
  the CSS code on a page, so that the CSS in my style sheets is as elegant as
  the code in my demos? Shortly after, prefixfree was born.
categories:
  - Coding
  - Tools
  - CSS3
---
<em>This article is the first piece in our new series introducing new, useful and freely available tools and techniques presented and released by active members of the Web design community. Lea Verou is well-known for her experiments with CSS and JavaScript and in this post she presents her recent tool, prefixfree, which will hopefully help you break free from the CSS prefix hell.</em>

### So What's the Problem With Prefixes?

I’m sure we all agree that CSS3 is pretty cool and that it enables us to do things that were previously impossible. But those of us who use CSS3 a lot have surely experienced prefix hell, as seen in the snippet below (from a real style sheet!):

<pre><code class="language-css">.download {
   position: absolute;
   top: 1em;
   left: -1.5em;
   width: 6em;
   height: 6em;
   padding: 1em 0;
   background: #80A060;
   background-image: -webkit-linear-gradient(transparent, rgba(0,0,0,.3));
   background-image: -moz-linear-gradient(transparent, rgba(0,0,0,.3));
   background-image: -o-linear-gradient(transparent, rgba(0,0,0,.3));
   background-image: -ms-linear-gradient(transparent, rgba(0,0,0,.3));
   background-image: linear-gradient(transparent, rgba(0,0,0,.3));
   color: white;
   line-height: 1;
   font-size: 140%;
   text-align: center;
   text-decoration: none;
   text-shadow: .08em .08em .2em rgba(0,0,0,.6);
   -webkit-border-radius: 50%;
   -moz-border-radius: 50%;
   border-radius: 50%;
   -webkit-box-shadow: .1em .2em .4em -.2em black;
   -moz-box-shadow: .1em .2em .4em -.2em black;
   box-shadow: .1em .2em .4em -.2em black;
   -webkit-box-sizing: border-box;
   -moz-box-sizing: border-box;
   box-sizing: border-box;
   -ms-transform: rotate(15deg);
   -webkit-transform: rotate(15deg);
   -moz-transform: rotate(15deg);
   -o-transform: rotate(15deg);
   -ms-transform: rotate(15deg);
   transform: rotate(15deg);
   -webkit-animation: none;
   -moz-animation: none;
   animation: none;
}</code></pre>

I’m not saying that prefixes are bad. <a href="https://www.alistapart.com/articles/prefix-or-posthack/">We need them.</a> But the reality is that, in most cases, they cause maintenance troubles, they bloat CSS files, and they make it harder to tweak values (because you have to do it up to five times).

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Guide To CSS Pseudo-Classes And Pseudo-Elements](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
*   [Variables: The Backbone Of CSS Architecture](https://www.smashingmagazine.com/2016/01/variables-in-css-architecture/)
*   [Scaling Down The BEM Methodology For Small Projects](https://www.smashingmagazine.com/2014/07/bem-methodology-for-small-projects/)
*   [Flexbox Is As Easy As Pie – Designing CSS Layouts](https://www.smashingmagazine.com/2013/05/centering-elements-with-flexbox/)

### A Solution: prefixfree

The code I write in my live demo slides and presentations doesn’t have any prefixes, even for things like <code>@keyframes</code> or the <code>transition</code> property, which aren’t yet supported anywhere prefix-less. To be able to do this, I wrote a script that detects the prefix of the current browser and adds it where needed. Recently, I thought, why not adapt the script to process all of the CSS code on a page, so that the CSS in my style sheets is as elegant as the code in my demos? Shortly after, <a href="https://leaverou.github.com/prefixfree/">prefixfree</a> was born.

<a href="https://leaverou.github.com/prefixfree/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606cb0af-fa8d-47d5-81fd-abe9a5b69b20/prefixfree-main.jpg" alt="prefixfree" width="500" height="197" /></a>

The script essentially does everything in JavaScript’s power to allow you to <strong>completely forget about vendor prefixes</strong>. It processes linked style sheets (except the ones in <code>@import</code> rules), embedded style sheets, inline styles, even CSS added afterwards (such as in new elements, CSSOM property changes and lookups). And if, in rare cases, you want to use a different definition for a different engine (for example, because one’s implementation is buggy), you can still use prefixed CSS.

The good thing about <em>prefixfree</em> is that once the browser vendors drop their prefixes for CSS3 properties, you can just remove the script and your CSS will still work. Your code will continue to be valid CSS3 (so valid that it will even pass a CSS validator). Your code does not depend on it (unlike CSS preprocessors); rather, it functions more like a polyfill, smoothing out browser differences for the time being.

Another useful feature is that the script <strong>auto-detects which properties need prefixing</strong>. Its code has no property list. It detects which properties are supported and which of them are supported <em>only</em> with a prefix. Values, selectors and @rules are based on predefined lists, but they are still prefixed <em>only</em> when needed. No browser sniffing is involved; everything is based on feature detection.

<a href="https://leaverou.github.com/prefixfree/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ab36c8d-a70f-4b3f-bebf-251ce29c5bc5/prefixfree-500px.jpg" alt="prefixfree" width="500" height="346" /></a>

Unlike <a href="https://prefixr.com/">other solutions</a>, <em>prefixfree</em> adds the current prefix at runtime, so the user downloads a much smaller CSS file. Some might argue that pre-processed CSS is faster because no client-side processing is involved. To some extent, this is true, but in my experiments there was no significant lag. With the borderline exception of Opera, it was hardly noticeable.

Also, there are a few server-side solutions, but there are two main issues with those. Firstly, the file size of the CSS file is still huge, as it has to contain all the prefixes (and the unprefixed versions). And secondly, the server-side script has to maintain lists of properties at all times, because they cannot be automatically detected, like with <em>prefixfree</em>.

So, what does the rule above become with <em>prefixfree</em>? It becomes this beauty:

<pre><code class="language-css">.download {
   position: absolute;
   top: 1em;
   left: -1.5em;
   width: 6em;
   height: 6em;
   padding: 1em 0;
   background: #80A060;
   background-image: linear-gradient(transparent, rgba(0,0,0,.3));
   color: white;
   line-height: 1;
   font-size: 140%;
   text-align: center;
   text-decoration: none;
   text-shadow: .08em .08em .2em rgba(0,0,0,.6);
   border-radius: 50%;
   box-shadow: .1em .2em .4em -.2em black;
   box-sizing: border-box;
   transform: rotate(15deg);
   animation: none;
}</code></pre>

### Isn't It Something That's Better Done Server-Side?

This is a valid argument, and there are advantages and disadvantages to both approaches. Using a server-side script means that:

*   It has to be updated very, very often as browser support changes and prefixes aren't needed any more. PrefixFree automatically detects what needs a prefix and what doesn't.
*   All the prefixes need to be downloaded, which adds lots of bloat. In a medium size stylesheet, that's far more bloat than the size of prefixfree.js.
*   In cases of preprocessors like LESS and SASS, you depend on their proprietary syntax, so you can't just remove the script after a few years.

However, there are some benefits to doing it on the server-side:

*   It takes longer to download, but the user doesn't see the un-CSS3-ed version of the style at all. With PrefixFree there will be a tiny delay.
*   It will work the same even when JavaScript is disabled. Although, with PrefixFree, if the JS is disabled, the user will just see the design without some CSS3, but it will still be perfectly functional. If your CSS is written correctly, _the design should be functional without CSS3 anyway_.

Personally, I think it boils down to a matter of personal decision and whether the advantages are more important for you than the disadvantages.</p>

### Download the Script on GitHub!

You can <a href="https://leaverou.github.com/prefixfree">download prefixfree from GitHub</a>. The minified version is less than 5 KB, which becomes less than 2 KB after Gzip’ing. Please keep in mind that it’s still a very early beta and might have bugs. You can <a href="https://github.com/LeaVerou/prefixfree">help fix them</a>, or at least report them in the <a href="https://github.com/LeaVerou/prefixfree/issues">issues tracker</a>. Have fun!

{{< signature "al" >}}

