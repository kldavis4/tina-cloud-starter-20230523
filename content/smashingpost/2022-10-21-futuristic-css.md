---
title: 'Futuristic CSS'
slug: futuristic-css
author: sacha-greif
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57790dc2-f3f7-474d-b84e-531a37a1aa5e/futuristic-css.jpg
date: 2022-10-21T12:00:00.000Z
summary: >-
  In this article, Sacha Greif tries to anticipate future CSS trends and takes a look at some far-fetched and futuristic CSS features that might one day make their way to the browser.
description: >-
  In this article, Sacha Greif tries to anticipate future CSS trends and takes a look at some far-fetched and futuristic CSS features that might one day make their way to the browser.
categories:
  - CSS
  - Tools
  - Guides
  - Techniques
---

I run the yearly State of CSS survey, asking developers about the CSS features and tools they use or want to learn. The survey is actually open right now, so [go take it](https://survey.devographics.com/survey/state-of-css/2022?source=smashing_magazine_futuristic_css)!

The goal of the survey is to help anticipate future CSS trends, and the data is also used by browser vendors to inform their roadmap. 

This year, Lea Verou pitched in as lead survey designer to help select which CSS features to include. But even though we added many new and upcoming features (some of which, like [CSS nesting](https://caniuse.com/css-nesting), aren’t even supported yet), some features were so far off, far-fetched, and futuristic (or just plain made-up!) that we couldn’t in good conscience include them in the survey. 

But it’s fun to speculate. So today, let’s take a look at some CSS features that might one day make their way to the browser… or not!

## CSS Toggles

The CSS checkbox hack has been around for [over ten years](https://css-tricks.com/the-checkbox-hack/), and it still remains the only way to achieve any kind of “toggle effect” in pure CSS (I actually used it myself recently for [the language switcher on this page](https://sachagreif.com/work-with-me/)).

But what if we had *actual* toggles, though? What if you could handle tabs, accordions, and more, all without writing a single line of JavaScript code?

That’s exactly what Tab Atkins and Miriam Suzanne’s [CSS Toggles](https://tabatkins.github.io/css-toggle/) proposal wants to introduce. The proposal is quite complex, and the number of details and edge cases involved makes it clear that this will be far from trivial for browser vendors to implement. But hey, one can dream, and in fact, an experimental implementation [recently appeared in Chrome Canary](https://twitter.com/yisibl/status/1581324896310681600)!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8cb3f85-97c3-4bff-b343-ccbd60a0032d/3-futuristic-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8cb3f85-97c3-4bff-b343-ccbd60a0032d/3-futuristic-css.png" width="800" height="500" sizes="100vw" caption="CSS Toggles running in Chrome Canary. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8cb3f85-97c3-4bff-b343-ccbd60a0032d/3-futuristic-css.png'>Large preview</a>)" alt="CSS Toggles running in Chrome Canary" >}}

## CSS Switch Function

A major trend in recent years &mdash; not only in CSS but in society at large &mdash; has been recognizing that we’ve often done a poor job of serving the needs of a diverse population. In terms of web development, this translates into building websites that can adapt not only to different devices and contexts but also to different temporary or permanent disabilities such as color blindness or motion sickness. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf67cb23-9587-476f-a8fa-25f6958e2cc2/4-futuristic-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf67cb23-9587-476f-a8fa-25f6958e2cc2/4-futuristic-css.png" width="800" height="617" sizes="100vw" caption="You can alter the look and feel of Mac OS thanks to its accessibility options, and you can also do the same to websites thanks to media queries such as <code>prefers-reduced-motion</code> or <code>prefers-color-scheme</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf67cb23-9587-476f-a8fa-25f6958e2cc2/4-futuristic-css.png'>Large preview</a>)" alt="You can alter the look and feel of Mac OS thanks to its accessibility options, and you can also do the same to websites thanks to media queries such as ‘prefers-reduced-motion’ or ‘prefers-color-scheme’" >}}

The result is that we often need to target these different conditions in our code and react to them, and this is where Miriam Suzanne’s [`switch` proposal](https://css.oddbird.net/rwd/switch/) comes in:

<pre><code class="language-css">.foo {
  display: grid;
  grid-template-columns: switch(
    auto /
     (available-inline-size &gt; 1000px) 1fr 2fr 1fr 2fr /
     (available-inline-size &gt; 500px) auto 1fr /
   );
}
</code></pre>

While the initial proposal focuses on testing `available-inline-size` as a way to set up grid layouts, one can imagine the same `switch` syntax being used for many other scenarios as well, as a complement to media and container queries. 

{{% feature-panel %}}

## Intrinsic Typography

[Intrinsic typography](https://css-tricks.com/intrinsic-typography-is-the-future-of-styling-text-on-the-web/) is a technique coined by Scott Kellum, who developed the type-setting tool [Typetura](https://typetura.com/). In a nutshell, it means that instead of giving the text a specific size, you let it set its own size based on the dimensions of the element containing it: 

<blockquote>Instead of sizing and spacing text for each component at every breakpoint, the text is given instructions to respond to the areas it is placed in. As a result, intrinsic typography enables designs to be far more flexible, adapting to the area in which it is placed, with far less code.</blockquote>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd59246-ada5-427a-8220-0b2f4c528b2b/5-futuristic-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd59246-ada5-427a-8220-0b2f4c528b2b/5-futuristic-css.png" width="800" height="509" sizes="100vw" caption="Typetura’s typographic controls. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd59246-ada5-427a-8220-0b2f4c528b2b/5-futuristic-css.png'>Large preview</a>)" alt="Typetura’s typographic controls" >}}

This goes beyond what the already quite useful [Utopia Type Scale Calculator](https://utopia.fyi/type/calculator) can offer, as it only adapts based on viewport dimensions &mdash; not container dimensions. 

The only problem with Typetura is that it currently requires a JavaScript library to work. As is often the case, though, one can imagine that if this approach proves popular, it’ll [make its way to native CSS](https://github.com/w3c/csswg-drafts/issues/6245) sooner or later. 

We can already achieve a lot of this today (or pretty soon, at least) with [container query units](https://ishadeed.com/article/container-query-units/), which lets you reference a container’s size when defining units for anything inside it. 

## Sibling Functions

It’s common in Sass to write loops when you want to style a large number of items based on their position in the DOM. For example, to progressively indent each successive item in a list, you could do the following:

<pre><code class="language-css">@for $i from 1 through 10 {
  ul:nth-child(#{$i}) {
    padding-left: #{$i &#42; 5px}
  }
}
</code></pre>

This would then generate the equivalent of 10 CSS declarations. The obvious downside here is that you end up with ten lines of code! Also, what if your list has more than ten elements?

An elegant solution currently in the works is [the `sibling-count()` and `sibling-index()` functions](https://github.com/w3c/csswg-drafts/issues/4559). Using `sibling-index()`, the previous example would become:

<pre><code class="language-css">ul &gt; li {
  padding-left: calc(sibling-index() &#42; 5px); 
}
</code></pre>

It’s an elegant solution to a common need!

{{% ad-panel-leaderboard %}}

## CSS Patterns

A long, long time ago, I made a little tool called [Patternify](http://www.patternify.com/) that would let you draw patterns and export them to base64 code to be dropped inline in your CSS code. My concept was to let you use patterns inside CSS but with [CSS Doodle](https://css-doodle.com/). Yuan Chuan had the opposite idea: what if you used CSS to *create* the patterns?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3fd70f-49e0-4059-94f4-df2c84ae5f44/2-futuristic-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3fd70f-49e0-4059-94f4-df2c84ae5f44/2-futuristic-css.png" width="800" height="509" sizes="100vw" caption="CSS Doodle: a deceptively powerful tool with a simple syntax. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3fd70f-49e0-4059-94f4-df2c84ae5f44/2-futuristic-css.png'>Large preview</a>)" alt="CSS Doodle: a deceptively powerful tool with a simple syntax" >}}

Now pure-CSS pattern-making [has been around for a while](https://projects.verou.me/css3patterns/#) (and recently got more elaborate with the introduction of [conic gradients](https://css-tricks.com/background-patterns-simplified-by-conic-gradients/)), but Yuan Chuan definitely introduced some key new concepts, starting with the ability to randomize patterns or easily specify a grid. 

Obviously, CSS Doodle is probably far more intricate than a native pattern API would ever need to be, but it’s still fun to imagine what we could do with just a few more pattern-focused properties. The [`@image` proposal](https://github.com/w3c/csswg-drafts/issues/6807) might be a step in that direction, as it gives you tools to define or modify images right inside your CSS code. 

## Native HTML/CSS Charts

Now we’re really getting into wild speculation. In fact, as far as I know, no one else has ever submitted a proposal or even blogged about this. But as someone who spends a lot of their time working on [data visualizations](https://2021.stateofcss.com/), I think native HTML/CSS charts would be amazing!

Now, most charts you’ll come across on the web will be rendered using SVG or sometimes Canvas. In fact, this is the approach we use for the surveys through the DataViz library [Nivo](https://nivo.rocks/). 

The big problem with this, though, is that neither SVG nor Canvas are really responsive. You can scale them down proportionally, but you can’t have the same fine-grained control that something like CSS Grid offers. 

That’s why some have tried to lay out charts using pure HTML and CSS, like [charting library `Charts.css`](https://chartscss.org/).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55914b8f-bbc3-42eb-b905-5f8a2ebde89d/6-futuristic-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55914b8f-bbc3-42eb-b905-5f8a2ebde89d/6-futuristic-css.png" width="800" height="509" sizes="100vw" caption="<code>Charts.css</code>: creating charts with only HTML and CSS. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55914b8f-bbc3-42eb-b905-5f8a2ebde89d/6-futuristic-css.png'>Large preview</a>)" alt="Charts.css: creating charts with only HTML and CSS" >}}

The problem here becomes that once you go past simple blocky bar charts, you need to use a lot of hacks and complex CSS code to achieve what you want. It can work, and libraries like `Charts.css` do help a lot, but it’s not easy by any means. 

That’s why I think having native chart elements in the browser could be amazing. Maybe something like:

<pre><code class="language-html">&lt;linechart&gt;
  &lt;series id="series&#95;a"&gt;
    &lt;point x="0" y="2"/&gt;
    &lt;point x="1" y="4"/&gt;
    &lt;point x="2" y="6"/&gt;
  &lt;/series&gt;
  &lt;series id="series_b"&gt;
    &lt;point x="0" y="6"/&gt;
    &lt;point x="1" y="4"/&gt;
    &lt;point x="2" y="2"/&gt;
  &lt;/series&gt;
&lt;/linechart&gt;
</code></pre>

You would then be able to control the chart’s spacing, layout, colors, and so on by using good old CSS &mdash; including media and container queries, to make your charts look good in every situation.

Of course, this is something that’s already possible through web components, and many are experimenting in this direction. But you can’t beat the simplicity of pure HTML/CSS. 

## And Also…

Here are a couple more quick ones just to keep you on your toes:

### Container Style Queries

You might already know that container queries let you define an element’s style based on the width or height of its containing element. [Container style queries](https://www.w3.org/TR/css-contain-3/#container-style-query) let you do the same, but based on that container’s &mdash; you guessed it &mdash; style, and there’s actually already an experimental implementation for it in Chrome Canary. 

As [Geoff Graham points out](https://css-tricks.com/early-days-of-container-style-queries/), this could take the form of something like:

<pre><code class="language-css">.posts {
  container-name: posts;
}

@container posts (background-color: #f8a100) {
  /&#42; Change styles when `posts` container has an orange background &#42;/
  .post {
    color: #fff;
  }
}
</code></pre>

This is a bit like `:has()`, if `:has()` lets you select based on styles and not just DOM properties and attributes, which, now that I think about it, might be another cool feature too!

### Random Numbers

People have tried to simulate a random number generator in CSS for a long time (using the [“Cicada Principle” technique](https://lea.verou.me/2020/07/the-cicada-principle-revisited-with-css-variables/) and [other hacks](https://uxdesign.cc/creating-randomness-with-pure-css-a990dafcd569)), but having true built-in randomness would be great. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9d4458-59ce-4497-b08b-fbdadfac383d/1-futuristic-css.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9d4458-59ce-4497-b08b-fbdadfac383d/1-futuristic-css.png" width="800" height="509" sizes="100vw" caption="Using the ‘Cicada Principle’ technique to simulate random patterns. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9d4458-59ce-4497-b08b-fbdadfac383d/1-futuristic-css.png'>Large preview</a>)" alt="Using the Cicada Principle technique to simulate random patterns" >}}

A **CSS random number generator** would be useful not just for pattern-making but for any time you need to make a design feel a little more organic. There is [a fairly recent proposal](https://github.com/w3c/csswg-drafts/issues/2826#issuecomment-1204305712) that suggests a syntax for this, so it’ll be interesting to see if we ever get CSS randomness!

### Grid Coordinates Selector

What if you could target grid items based on their position in a grid or flexbox layout, either by styling a specific row or column or even by targeting a specific item via its `x` and `y` coordinates? 

It might seem like a niche use case at first, but as we use Grid and Subgrid more and more, we might also need new ways of targeting specific grid items. 

### Better Form Styling

Styling form inputs has traditionally been such a pain that many UI libraries decide to abstract away the native form input completely and recreate it from scratch using a bunch of `div`s. As you might imagine, while this might result in nicer-looking forms, it usually comes at the cost of accessibility. 

And while things have been getting better, there’s certainly still a lot we could improve when it comes to forming input styling and styling native widgets in general. The new [`<selectmenu>` element](https://hidde.blog/custom-select-with-selectmenu/) proposal is already a great start in that direction.

### Animating To Auto

We’ve all run into this: you want to animate an element’s height from `0` to, well, however big it needs to be to show its contents, and that’s when you realize CSS doesn’t let you animate or transition to `auto`. 

There are [workarounds](https://css-tricks.com/using-css-transitions-auto-dimensions/), but it would still be nice to have this fixed at the browser level. For this to happen, we’ll also need to be able to use `auto` inside `calc`, for example `calc(auto / 2 + 200px / 2)`.

{{% ad-panel-leaderboard %}}

## Predicting The Future

Now let’s be real for a second: the chances of any of these features being implemented (let alone supported in all major browsers) are slim, at least if we’re looking at the next couple of years.  

But then again, people thought the same about `:has()` or native CSS nesting, and it does look like we’re well on our way to being able to use those two &mdash; and many more &mdash; in our code sooner than later. 

So let’s touch base again five years from now and see how wrong I was. Until then, I’ll keep charting the course of CSS through our yearly surveys. And I hope you’ll help us by [taking this year’s survey](https://survey.devographics.com/survey/state-of-css/2022?source=smashing_magazine_futuristic_css)!

*Thanks to Lea Verou and Bramus Van Damme for their help with this article.*

{{< signature "vf, yk, il" >}}
