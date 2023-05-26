---
title: 'jQuery Plugin Checklist: Should You Use That jQuery Plug-In?'
slug: jquery-plugin-checklist-should-you-use-that-jquery-plug-in
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82b10f0e-3fde-4742-af20-57c7c36262fa/jquery-02.jpg
date: 2010-08-26T09:42:54.000Z
author: jon-raasch
description: >-
  jQuery plug-ins provide an excellent way to save time and streamline
  development, allowing programmers to avoid having to build every component
  from scratch. But plug-ins are also a wild card that introduce an element of
  uncertainty into any code base. A good plug-in saves countless development
  hours; a bad plug-in leads to bug fixes that take longer than actually
  building the component from scratch.
categories:
  - Coding
  - jQuery
  - Plugins
---
jQuery plug-ins provide an excellent way to save time and streamline development, allowing programmers to avoid having to build every component from scratch. But plug-ins are also a wild card that introduce an element of uncertainty into any code base. A good plug-in saves countless development hours; a bad plug-in leads to bug fixes that take longer than actually building the component from scratch.

Fortunately, one usually has a number of different plug-ins to choose from. But even if you have only one, figure out whether it's worth using at all. The last thing you want to do is introduce bad code into your code base.</p>

## Do You Need A Plug-In At All?

The first step is to figure out whether you even need a plug-in. If you don't, you’ll save yourself both file size and time.</p>

### 1. Would Writing It Yourself Be Better?

If the functionality is simple enough, you could consider writing it yourself. jQuery plug-ins often come bundled with a wide variety of features, which might be overkill for your situation. In these cases, writing any simple functionality by hand often makes more sense. Of course, the benefits have to be weighed against the amount of work involved.

{{% feature-panel %}}

For example, jQuery UI's [accordion](https://docs.jquery.com/UI/Accordion) is great if you need advanced functionality, but it might be overkill if you just need panels that open and close. If you don't already use jQuery UI elsewhere on your website, consider instead the native jQuery `slideToggle()` or `animate()`.</p>

### 2. Is It Similar to a Plug-In You're Already Using?

After discovering that a particular plug-in doesn't handle everything you need, finding another plug-in to cover loose ends might be tempting. But including two similar plug-ins in the same app is a sure path to bloated JavaScript.

Can you find a single plug-in that covers everything you need? If not, can you extend one of the plug-ins you have to cover everything you need? Again, in deciding whether to extend a plug-in, weigh the benefits against the development time involved.

For example, jQuery lightbox is a nice way to enable pop-up photos in a gallery, and [simpleModal](https://www.ericmmartin.com/projects/simplemodal/) is a great way to display modal messages to users. But why would you use both on the same website? You could easily extend one to cover both uses. Better yet, find one plug-in that covers everything, such as [Colorbox](https://colorpowered.com/colorbox/).</p>

### 3. Do You Even Need JavaScript?

In some situations, JavaScript isn't needed at all. CSS pseudo-selectors such as `:hover` and CSS3 transitions can cover a variety of dynamic functionality much faster than a comparable JavaScript solution. Also, many plug-ins apply only styling; doing this with mark-up and CSS might make more sense.

For example, plug-ins such as [jQuery Tooltip](https://bassistance.de/jquery-plugins/jquery-plugin-tooltip/) are indispensable if you have dynamic content that requires well-placed tooltips. But if you use tooltips in only a few select locations, using pure CSS is better ([see this example](https://sixrevisions.com/css/css-only-tooltips/)). You can take static tooltips a step further by animating the effect using a CSS3 transition, but bear in mind that the animation will work only in certain browsers.</p>

## Avoid Red Flags

When reviewing any plug-in, a number of warning signs will indicate poor quality. Here, we'll look at all aspects of plug-ins, from the JavaScript to the CSS to the mark-up. We'll even consider how plug-ins are released. None of these red flags alone should eliminate any plug-in from consideration. You get what you pay for, and because you're probably paying nothing, you should be willing to cut any one a bit of slack.

If you're fortunate enough to have more than one option, these warning signs could help you narrow down your choice. But even if you have only one option, be prepared to forgo it if you see too many red flags. Save yourself the headache _ahead_ of time.</p>

### 4. Weird Option or Argument Syntax

After using jQuery for a while, developers get a sense of how most functions accept arguments. If a plug-in developer uses unusual syntax, it stands to reason that they don't have much jQuery or JavaScript experience.

Some plug-ins accept a jQuery object as an argument but don't allow chaining from that object; for example, `$.myPlugin( $('a') );` but not `$('a').myPlugin();` This is a big red flag.

A green flag would be a plug-in in this format…

    $('.my-selector').myPlugin({
     opt1 : 75,
     opt2 : 'asdf'
    });

… that also accepts…

    $.myPlugin({
     opt1 : 75,
     opt2 : 'asdf'
    }, $('.my-selector'));

### 5. Little to No Documentation

Without documentation, a plug-in can be very difficult to use, because that is the first place you look for answers to your questions. Documentation comes in a variety of formats; proper documentation is best, but well-commented code can work just as well. If documentation doesn't exist or is just a blog post with a quick example, then you might want to consider other options.

Good documentation shows that the plug-in creator cares about users like you. It also shows that they have dug into other plug-ins enough to know the value of good documentation.</p>

### 6. Poor History of Support

Lack of support indicates that finding help will be difficult when issues arise. More tellingly, it indicates that the plug-in has not been updated in a while. One advantage of open-source software is all of the eye-balls that are debugging and improving it. If the author never speaks to these people, the plug-in won't grow.

When was the last time the plug-in you're considering was updated? When was the last time a support request was answered? While not all plug-ins need as robust a support system as the [jQuery plug-ins website](https://plugins.jquery.com/), be wary of plug-ins that have never been modified.

A documented history of support, in which the author has responded to both bug and enhancement requests, is a green flag. A support forum further indicates that the plug-in is well supported, if not by the author then at least by the community.</p>

### 7. No Minified Version

Though a fairly minor red flag, if the plug-in's creator doesn't provide a minified version along with the source code, then they may not be overly concerned with performance. Sure, you could minify it yourself, but this red flag isn't about wasted time: it's about the possibility that the plug-in contains far worse performance issues.

On the other hand, providing a minified, packed and [gzipped](https://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression/) version in the download package is an indication that the author cares about JavaScript performance.</p>

### 8. Strange Mark-Up Requirements

<p>If a plug-in requires mark-up, then the mark-up should be of high quality. It should make <a href="https://blue-anvil.com/archives/guide-to-semantic-mark-up/">semantic sense</a> and be flexible enough for your purposes. Besides indicating poor front-end skills, strange mark-up makes integration more difficult. A good plug-in plugs into just about any mark-up you use; a bad plug-in makes you jump through hoops.

<p>In certain situations, more rigid mark-up is needed, so be prepared to judge this on a sliding scale. Basically, the more specific the functionality, the more specific the mark-up needed. Completely flexible mark-up that descends naturally from any jQuery selector is the easiest to integrate.</p>

### 9. Excessive CSS

<p>Many jQuery plug-ins come packaged with CSS, and the quality of the style sheets is just as important as the JavaScript. An excessive number of styles is a sure sign of bad CSS. But what constitutes "excessive" depends on the purpose of the plug-in. Something very display-heavy, such as a lightbox or UI plug-in, will need more CSS than something that drives a simple animation.</p>

<p>Good CSS styles a plug-in's content effectively while allowing you to easily modify the styles to fit your theme.</p>

### 10. No One Else Uses It

<p>With the sheer volume of jQuery users, most decent plug-ins will probably have something written about them, even if it's a "50 jQuery [fill in the blank]" post. Do a simple Google search for the plug-in. If you get very few results, you might want to consider another option, unless the plug-in is brand new or you can verifiy that it is written by a professional.</p>

<p>Posts on prominent blogs are great, and posts by prominent jQuery programmers are even better.</p>

## Final Assessment

<p>After you've given the plug-in the third degree, the only thing left to do is plug it in and test how well it performs.</p>

### 11. Plug It In and See

<p>Probably the best way to test a plug-in is to simply plug it on the development server and see the results. First, does it break anything? Make sure to look at JavaScript in the surrounding areas. If the plug-in includes a style sheet, look for layout and styling errors on any page that applies the style sheet.</p>

<p>Additionally, how does the plug-in perform? If it runs slowly or the page lags considerably when loading, it might be important to consider other options.</p>

### 12. Benchmarking With JSPerf

<p>To take your performance review to the next level, run a benchmark test using <a href="https://web.archive.org/web/20160131082743/https://jsperf.com:80/">JSPerf</a>. <a href="https://en.wikipedia.org/wiki/Benchmark_(computing)">Benchmarking</a> basically runs a set of operations a number of times, and then returns an average of how long it took to execute. JSPerf provides an easy way to test how quickly a plug-in runs. This can be a great way to pick a winner between two seemingly identical plug-ins.</p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c603da8-ad0f-4f10-b3e1-337822f78fd2/jsperf.png" alt="jsPerf screenshot" title="jsPerf" width="500" height="133" class="56927" /><br />
<em>An example of a performance test run in jsPerf.</em></p>

### 13. Cross-Browser Testing

<p>If a plug-in comes with a lot of CSS, make sure to test the styling in all of the browsers that you want to support. Bear in mind that CSS can be drawn from external style sheets or from within the JavaScript itself.</p>

<p>Even if the plug-in doesn't have any styling, check for JavaScript errors across browsers anyway (at least in the earliest version of IE that you support). jQuery's core handles most cross-browser issues, but plug-ins invariably use some amount of pure JavaScript, which tends to break in older browsers.</p>

### 14. Unit Testing

<p>Finally, you may want to consider taking cross-browser testing even further with <a href="https://en.wikipedia.org/wiki/Unit_testing">unit tests</a>. Unit testing provides a simple way to test individual components of a plug-in in any browser or platform you want to support. If the plug-in's author has included unit tests in their release, you can bet that all components of the plug-in will work across browsers and platforms.</p>

<p>Unfortunately, very few plug-ins include unit test data, but that doesn't mean you can't perform your own test using the <a href="https://docs.jquery.com/QUnit">QUnit plug-in</a>.</p>

<p>With minimal set-up, you can test whether the plug-in methods return the desired results. If any test fails, don't waste your time with the plug-in. In most cases, performing your own unit tests is overkill, but QUnit helps you determine the quality of a plug-in when it really counts. For more information on how to use QUnit, <a href="https://net.tutsplus.com/tutorials/javascript-ajax/how-to-test-your-javascript-code-with-qunit/">see this tutorial</a></p>

<p><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1117d9e-3c6d-4a7b-9df0-a54b98422f0f/qunit-example.png" alt="QUnit screenshot" title="QUnit Test" width="500" height="333" loading="lazy" decoding="async" class="56928" /><br />
<em>An example of a unit test run in QUnit.</em></p>

## Conclusion

<p>When assessing the quality of a jQuery plug-in, look at all levels of the code. Is the JavaScript optimized and error-free? Is the CSS tuned and effective? Does the mark-up make semantic sense and have the flexibility you need? These questions all lead to the most important question: will this plug-in be easy to use?</p>

<p>jQuery core has been optimized and bug-checked not only by the core team but by the entire jQuery community. While holding jQuery plug-ins to the same standard would be unfair, they should stand up to at least some of that same scrutiny.</p>

## Related Posts

<p>You may be interested in the following related posts:</p>
<ul>
<li><a href="https://www.smashingmagazine.com/2010/08/04/commonly-confused-bits-of-jquery/">Commonly Confused Bits Of jQuery</a></li>
<li><a href="https://www.smashingmagazine.com/2010/06/15/spice-up-your-website-with-jquery-goodness/">Spicing Up Your Website With jQuery Goodness</a></li>
<li><a href="https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/">jQuery and JavaScript Coding: Examples and Best Practices</a></li>
<li><a href="https://www.smashingmagazine.com/2010/04/27/45-useful-jquery-techniques-and-plugins/">45 Useful jQuery Techniques and Plugins</a></li>
</ul>

{{< signature "al" >}}

