---
title: 'Coding Q&A: CSS Performance, Debugging, Naming Conventions'
slug: css-performance-debugging-naming-conventions
image: null
date: 2013-01-22T15:06:34.000Z
author: chris-coyier
description: >-
  Howdy folks! Welcome to another round of Smashing Magazine CSS Q&A — the final
  one, as of now. One more time, we'll answer the best questions which you sent
  us about CSS.
categories:
  - Coding
  - CSS
  - Performance
---
Howdy folks! Welcome to another round of Smashing Magazine CSS Q&A — the final one, as of now. One more time, we'll answer the best questions which you sent us about CSS.

It was a great experience to run this Q&A with you - thanks a lot for sharing all your questions with us! We hope we answered them at the best possible, and we'll surely be back with new and exciting Q&A rounds in the future. Enjoy Chris' last round on CSS performance, best practices on CSS class naming, and more!

## CSS Performance

Vitaly asks:

<blockquote>
<p>"Could you recommend some rules of thumb or general tips on how to improve the performance of CSS? What are your general thoughts on the performance issues of CSS? Would you recommend the tips from <a href="https://speakerdeck.com/jonrohan/githubs-css-performance">Jon Rohan’s talk</a>?"</p>
</blockquote>

{{% feature-panel %}}

Most of the time, I don’t think you should even bother thinking about the performance of your CSS. However, you should absolutely be thinking about the overall performance of your website.

The first thing to check is your website’s response time. You’ll see that is the very first thing in the “Network” tab of Chrome’s Developer Tools. If that’s, say, a second or more, that’s pretty slow, and you should work to get that down. That means server-side caching, faster servers, more efficient servers or more servers.

Usually, that’s not the problem with slow websites. That’s the 20% in the [80/20 rule](https://www.stevesouders.com/blog/2012/02/10/the-performance-golden-rule/). The other 80% is front-end-related stuff.

In the vast majority of situations, doing any of the following things would take less effort and have a far greater impact on performance than CSS optimizations:

*   Remove one resource (JavaScript file, CSS file or image) from the page (i.e. concatenate them).
*   Ensure that the resources are compressed and Gzip’ed.
*   Ensure that your assets have expires headers that are set far out.
*   Host assets on a content delivery network (CDN).

You can learn more about these things in [this slide deck](https://speakerdeck.com/chriscoyier/lets-do-a-bunch-of-simple-stuff-to-make-websites-faster) that I’ve put together.

If you’re already doing all of these things and you’re still having problems, that’s where [Jon Rohan’s tips](https://speakerdeck.com/jonrohan/githubs-css-performance) can help. Simpler HTML and simpler CSS selectors can make a difference in page-rendering speed.

I just wouldn’t expect huge gains on an “average” website. Remember that for the GitHub “dif” pages in question here, the developers were able to remove thousands and thousands of elements and simplify kinda nasty selectors (such as tag-qualified classes) to achieve their 37% increase in rendering speed. Most of us aren’t in that position.</p>

## Naming Classes

Christoph Rumpel asks:

<blockquote>
<p>"I would love to hear your opinion and some best practices on CSS class naming. Do you use BEM styles, or do you have your own convention? I am now looking for the best way to keep my CSS code simple, performant and reusable. Please let me know your thoughts on that topic and especially on how you would name nested containers and on what to consider when using selectors."</p>
</blockquote>

I’ve just heard the saying, “There are only two hard things in computer science: cache invalidation and naming things.” Apparently it’s a quote by Phil Karlton that has been turned into an adage. By “naming things” is meant that moment when it’s up to you to choose a name for something. Any name would technically work, but a poorly chosen name will cause confusion and likely haunt your project moving forward. A good name will make for more understandable code and make things easier for all.

HTML class names (yes, we’re [supposed to](https://tantek.com/2012/353/b1/why-html-classes-css-class-selectors) call them HTML classes, not CSS classes) are absolutely one of those things with which naming is important. It’s commonly taught that a class name like `leftSidebar` or `bigRed` is bad because it describes the desired look (which could change), rather than the content it contains (which is less likely to).

For myself, I just do my best to describe the content it contains. The best scenario is one in which I’ve identified a pattern and then named that pattern. Then I choose the most semantic element possible to go with the content and roll with it. For instance, a row of icons with numbers beside them might become `class="stats"`. Here are a couple of classes from my currently open project:

<pre><code class="language-markup tmp-html">&lt;section class=&quot;pen-grid group&quot;&gt;

&lt;div class=&quot;single-pen&quot;&gt;

&lt;header class=&quot;collection-header&quot;&gt;

&lt;img class=&quot;user-avatar&quot;&gt;

&lt;span class=&quot;views&quot;&gt;</code></pre>

These have served me well so far. I can understand what these elements are from either the HTML or the CSS.

Regarding wrappers, if a wrapper is needed solely for design reasons, I’ll often use a div (which has no semantic meaning) and apply `-wrap` to whatever other class name makes sense, so that I know it’s purely for design. No shame in that, if you ask me.</p>

## Debugging Preprocessed CSS

Andrea Verlicchi asks:

<blockquote><p>"I’ve read you’re a great fan of Sass/SCSS, like me. But most colleagues don’t use it because they are concerned about debugging the page, meaning they can’t just inspect the page and easily get the line of CSS where the rules are declared. How would you answer that concern?"</p></blockquote>

The way this pans out in my life is this: it doesn’t matter. My CSS structure is so organized and I know my text editor well enough that I can quickly jump to the CSS that I need without the help of line numbers in the developer tools.

However, I can understand that not all situations are like this. Seeing line numbers might be especially helpful when working with less familiar code or with code that you haven’t written. You’ll be happy to know that Sass supports source maps, and recent versions of [Chrome support source maps](https://bricss.net/post/33788072565/using-sass-source-maps-in-webkit-inspector), so you’ll be matching up line numbers in no time. If you use Compass, add this to your `config.rb` file:

<pre><code class="language-php">sass_options = { :debug_info =&gt; true }</code></pre>

Now you’ll get proper line-number mapping:

![source-maps-on](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c340251-5323-4995-b447-80ddb3a24271/source-maps-on.png)

If you’re still on Firebug, then FireSass is essentially the same.

## Staying Up To Date

Rouzbeh Sarrafieh asks:

<blockquote><p>"How does a novice/intermediate developer such as myself, who only does HTML and CSS and uses jQuery plugins, not get overwhelmed with all of the new things constantly being popularized and used so widely these days? From Gzip’ing and minifying CSS to using GitHub, CodePen and Sass and optimizing for all of the new resolutions and screen sizes with media queries, while implementing best practice techniques that seem to be changing at such a rapid pace &mdash; it all seems like so much to learn without having the time when you have a full-time job."</p></blockquote>

It certainly can be overwhelming. The bad news is that being in Web design and development has gotten more complicated over time, and it’s not showing any signs of getting any simpler. The good news is that you don’t need to know every little thing in order to be a good Web worker, and many of the most important skills are timeless.

Are you good at understanding problems and figuring out solutions? Then you’ll be useful forever. Are you good at holding your customers’ hands, figuratively speaking, and making them feel comfortable through the creation of their website? Then you’ll be useful forever. Do you have good taste? Then you’ll be useful forever.

The rest you can figure out bit by bit, as you need it. I feel like my generic advice of “[Just build websites](https://justbuildwebsites.com/)” is relevant here. If you’ve read a bit about preprocessors and want to give them a try, then take a day and try it out on the next website you build. The same goes for anything you feel is newfangled or that you feel behind on. You don’t have to do it all at once.

For an overview of just some of the tools in my workflow, here’s a <span class="removed_link" title="https://www.futureinsights.com/home/top-free-videos-of-2012-1.html">talk you can watch</span>. The slides for that, as well as another one specifically about staying up to date on Web technology, [are available here](https://css-tricks.com/slides-from-some-recent-presentations/).</p>

## When To @extend

Ross Lavery asks:

<blockquote><p>"Could you provide some insight on when you prefer using Sass @extend (requiring a “semantic” class of some sort to be added to the markup so that it can have @extend added to its style definition) versus simply adding a “non-semantic” class to the markup numerous times. I’ve been struggling with which direction to go in, and <a href="https://github.com/csswizardry/inuit.css/issues/38">Harry Roberts seems to prefer</a> avoiding @extend for the most part, because it means coming up with a “semantic” name for something that would have otherwise just required a class in the first place. I’ve had the same thought myself &mdash; having to just make up a silly name for a container for the sake of then extending a placeholder in Sass. Feels a bit backwards really."</p></blockquote>

I wouldn’t pigeonhole `@extend` as being just a way to have semantic class names by extending non-semantic ones. Certainly it can be used that way, and, honestly, I have no big problem with that. I would think of it more generically, like: “Gosh I wish this class had the same stuff as this other class.” There are any number of reasons why that could be useful.

For instance, say you have this pattern on your website of a user avatar, user name and user location. It has some layout variations depending on how it is being used and on which page. You could have a class name like `class="user-meta"` for the most common variation, and then add classes to it (e.g. `class="user-meta user-meta-small"`), where the second class would override things set in the first class in order to get what you need. But that setting and overriding process is tedious and fragile compared to just setting what you want to begin with. Instead, you could have your `.user-meta-small` @extend a base class for all `user-meta` variations, and set what it needs on top of the base. The result is more efficient CSS (no setting and resetting) _and_ more efficient HTML (one class instead of two).

Talking about this stuff so generically is difficult, though, and can lead to silly philosophical arguments. If you don’t like this, don’t do it. Naming is such a personal thing that as long as you have a system and aren’t often fighting yourself, you’re probably doing fine.

{{< signature "al" >}}

