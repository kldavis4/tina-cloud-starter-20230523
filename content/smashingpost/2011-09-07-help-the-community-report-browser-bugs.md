---
title: 'Help The Community! Report Browser Bugs!'
slug: help-the-community-report-browser-bugs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b554ab8e-bfb3-4328-b5a0-d4b4491f8cf7/reporting-bugs.jpeg
date: 2011-09-07T09:07:29.000Z
author: lea-verou
summary: >-
  You might think that reporting the bug would be pointless. Read this post to know how to identify a bug, learn why you should bother reporting bugs, and become part of making the Web a better place.
description: >-
  You might think that reporting the bug would be pointless. Read this post to know how to identify a bug, learn why you should bother reporting bugs, and become part of making the Web a better place.
categories:
  - Coding
  - CSS
  - JavaScript
  - Browsers
  - Bugs
---

You’re developing a new website and have decided to use some CSS3 and HTML5, now that many of the new specifications are gaining widespread support. As you’re coding the theme and thinking of how much easier these new technologies are making your job, you decide to stop for a while and test in other browsers, feeling a bit guilty for getting carried away and having forgotten to do so for a while. “Please work,” you whisper to your computer, while firing up all of the browsers you have installed. Browser A, check. You smile, feeling a bit relieved. Browser B, check. Your smile widens, and you start to feel better already. Browser C, “FFFFUUUUUUUUUUU…!”

Sound familiar? You might be surprised to hear that this is not necessarily your fault. With the competition in the browser market these days and the fast pace at which the new specifications are developing, browser makers are implementing new stuff in a hurry, sometimes without properly testing it. CSS3 and HTML5 are much more complex than their predecessors. The number of possible combinations of new features is huge, which leads to the most common cause of bugs: two (or more) things that weren’t tested together. As a result, **developers these days stumble upon browser bugs much more frequently** than they used to.

{{% feature-panel %}}

## Why Should I Bother Reporting Bugs?

**If you don’t, perhaps no one else will.** Maybe the bug you’ve discovered is so rare that no one else will stumble on it. Or maybe they will, but they won’t know how to report it. They might think that it’s their fault, just as you originally did. Besides, if you’ve used these new technologies in a way that triggers the bug now, you will likely do so again in the future as well, so you would directly benefit from the bug getting fixed. And in the process, you’d be helping thousands of other developers avoid the frustration you’ve faced.

You might think that reporting the bug would be pointless, because it would take ages to fix, and would take even longer for users to upgrade to the fixed version. However, for all browsers except Internet Explorer (IE), this is not true anymore. Users of Firefox, Opera, Safari and Chrome upgrade really quickly these days, because the software pushes them to do so or (in the case of Chrome) doesn’t even give them a choice. Also, some bugs get fixed quite quickly, especially the ones that come with a decent report. Keep reading, and your own bug reports will likely fall in this latter category.

## Making A Reduction

The first step is to reduce the problem to its bare minimum. If it turns out to be a browser bug, you will need to include this “reduction” in your bug report. Also, this will help you figure out a potential workaround until the browser vendor fixes it. Even if it’s not actually a browser bug, doing this will help you realize what you did wrong and fix it. Lastly, it’s a valuable aid in debugging in general.

Here is the process I follow to create reductions:

1.  Make a copy of your project. If it includes server-side code, then first save the rendered page locally; the rest of the process will be identical from this point on.
2.  Start removing CSS and JavaScript files. Eventually, you’ll find that removing one makes the problem go away. Add that one back and remove the others (except any files it depends on). In some rare cases, you might find that the bug persists even after removing all CSS and JavaScript code. In these cases, the bug is more than likely HTML-related.
3.  Now you need to find the exact code in the file that triggers the problem. Start commenting out parts of the code until the problem goes away (being careful not to introduce any new problems in the process). I find that the quickest way to do this is like doing a binary search: first, comment out around half of the code; if the bug persists, then remove that code and comment out half of the remaining code, and so on; if the bug disappears, then remove the uncommented code and proceed with that. You might find that deleting and undoing is quicker than commenting and uncommenting. Sometimes you have to do this process twice in the same file, because some bugs can be reproduced only with a particular combination of different code parts.
4.  Put the remaining CSS and JavaScript code inline by transferring it from the external file to a `<style>` or `<script>` element in the HTML document. This will make the reduction even simpler because it will be contained in only one file.
5.  Now, simplify the HTML. For example, if it’s a CSS bug, then remove everything that CSS rules don’t apply to. If the rules apply to a nested element, try applying them to the `<body>` instead and see whether the bug reproduces. If it is, then remove all of the `<body>`’s descendants.
6.  Change the document’s `<title>` to something relevant to the bug. Check the whole thing carefully for details that you wouldn’t want other people to see, because you usually can’t edit it after attaching it to your bug report. (I learned this the hard way.)

Now that you have your reduction, examine the code. Is it actually correct? Browser makers can’t be held accountable for the way their products handle invalid code &mdash; except for HTML5 markup, which has strictly defined error-handling. Validating the code might help, but take its output with a grain of salt. (Note that CSS vendor prefixes *are* valid, even if the <a href="https://jigsaw.w3.org/css-validator/">CSS validator</a> disagrees.)

If you have some time and want to be extra nice, here are some other things you can do to make an even better reduction:

*   Test to see whether the bug is more general than the case you have discovered. For example, if you discovered that an engine doesn’t handle `border-radius: 50%` correctly, then test whether the same thing happens with other percentage-based values. Or if a CSS gradient from black to transparent does not display correctly, see whether the same thing happens when you use a transition from `background-color: transparent` to `background-color: black`; if it does, then that would mean the problem stems from general interpolation and is not limited to CSS gradients. Even if you find that it’s not more general than the case you originally stumbled on, do mention your experiments in the bug description, so that the developers don’t have to repeat them.
*   Try to find a workaround. Can you change or add something in the code to make the bug go away? This could be as easy as converting ems to pixels or as hard as [adding a whole new declaration](https://stackoverflow.com/questions/5401353/opera-inset-box-shadow/5403024#5403024). Be sure to mention the workaround in the bug report.
*   Make it function like a test case, or create an additional test case. These are the special kinds of reductions that QA engineers make for automated testing systems. Such tests show the color green in browsers that don’t have the bug and red in the ones that do. Other colors may be shown, but not red and green at the same time. This is an easy task with some bugs, and incredibly hard with others.

Sometimes the nature of the problem is quite obvious, so creating a simple test case from scratch is quicker. I’ve found <a href="https://jsfiddle.net">JsFiddle</a> to be an invaluable aid in this. However, bear in mind that browser vendors usually prefer that you upload your own simple HTML files rather than provide JsFiddle links. If you do decide to use JsFiddle, then uncheck the “Normalized CSS” setting, remove any JavaScript libraries (unless your bug needs them to be reproduced), and append <code>/show</code> to the URL, so that it leads only to your test case, without the rest of the JsFiddle UI.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc96eef-f9af-4bc0-81e6-097f6a2e45d0/screenshot-js-fiddle.jpg" width="220" height="201" /></figure>

If you don’t have the time to make a reduction, reporting the bug is still a good idea. A bad bug report is better than none at all, and the same goes for reductions. In this case, the browser developers will have to create the reduction themselves. The difference is that they’re burdened with doing this for many more bugs than you can imagine. You only have to do it for one: yours.

## Should I Report It?

There are many reasons why you might not need to report the problem as a bug after all:

*   It turns out it’s not really a bug,
*   It has already been fixed in the latest nightly build,
*   It has already been reported.

Let’s tackle these one by one.

### Is It Really A Bug?

In most cases, when you isolate the problem to a simple reduction, it’s fairly obvious whether it’s a browser bug or not. However, there are some caveats to this.

A while ago, I realized that even though <code>outline-color: invert</code> was in the CSS specification, it didn’t work in all browsers that support outlines. In particular, it didn’t work in Webkit browsers or Firefox. Those browsers didn’t drop the declaration, but just treated it as though it was <a href="https://www.w3.org/TR/css3-color/#currentcolor"><code>currentColor</code></a>. So, I went ahead, created <a href="https://jsfiddle.net/leaverou/yxjgC/">a reduction</a>, and filed bug reports with both browsers. After a while, I was informed that a footnote in the specification actually permits user agents to do this, so it wasn’t actually a bug. The moral of the story is to check the specification carefully &mdash; not just the table that is included in every CSS property, but the whole thing. Knowing these details will make you a better developer anyway.

On another occasion, I was reading the <a href="https://www.w3.org/TR/css3-background/">“CSS3 Backgrounds and Borders” module</a> and found that it allowed percentages to be used for <code>border-width</code>, unlike CSS 2.1. I tested it, and it didn’t work in any browser. So, I filed <a href="https://bugs.webkit.org/show_bug.cgi?id=58445">bug reports</a> in some of them, only to be informed that this was dropped in the “dev” version (i.e. the not-yet-published version) of the specification. The moral of this story is that, for specs still under development, don’t check the published specifications to determine whether your issue is actually a bug. Instead, look at <a href="https://dev.w3.org/">dev.w3.org</a>, where the most up-to-date versions of the specs reside.

Of course, in many cases, a bug is not really a bug or a lack of understanding of the spec, but just one of those stupid mistakes that we all do (aka brain farts). I remember once how distraught I was over my JavaScript not working at all in Safari, even though it gave no errors. After a while of struggling to make a reduction, I realized that I had previously disabled JavaScript in that browser to test how a website worked without it and had forgotten to enable it.

Likewise, a few days ago, my SVGs weren’t displaying as backgrounds in Firefox, even though they displayed when I opened them in new tabs. I then realized that I had two background images in the same declaration, the other one being a CSS gradient, and I had forgotten to add the <code>-moz-</code> version.

The one I’m most embarrassed about is when I actually reported a bug to Opera about pointer-events not working in <code>&lt;select&gt;</code> menus and was then informed that Opera hadn’t implemented pointer-events in HTML elements at all. D’oh!

In some rare cases, the bug is indeed a bug but not a browser bug. Specifications have their fair share of bugs, too. If the spec defines something other than what happens or if it defines something that conflicts with the rest of the spec, then it most likely has a bug. Such bugs should be reported in the relevant mailing list (<a href="https://lists.w3.org/Archives/Public/www-style/">www-style</a> for CSS) or the <a href="https://www.w3.org/Bugs/Public/">W3C bug tracker</a>. Even if this is the case, many of the guidelines mentioned below still apply.

{{% ad-panel-leaderboard %}}

### Is It Reproducible In The Latest Nightly Builds?

If you haven’t already installed the nightlies of browsers, you should. These are the latest (potentially unstable) versions of browsers. Download them from these links:

*   [IE 10 Platform Preview 2](https://ie.microsoft.com/testdrive/info/downloads/)
*   [Firefox Nightly](https://nightly.mozilla.org/)
*   [Opera Next](https://www.opera.com/browser/next/)
*   [Chrome Canary](https://tools.google.com/dlpage/chromesxs)
*   [Webkit Nightly Builds](https://nightly.webkit.org/)

Obviously, if your bug is not reproducible in the latest nightly of the browser, then you don’t have to report it. Just wait until the build propagates to a stable release. In other words, all you need is patience, young Padawan.

### Has It Already Been Reported?

If after checking the specifications and the latest nightly, you’re still confident that it is a bug, then you need to search whether it has already been reported. Your best bet is to use the search engine of the relevant bug tracker. Don’t forget to search all statuses, because the default on some bug-tracking systems is to search only confirmed and open bugs (excluding unconfirmed and fixed or otherwise closed ones).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faaaf378-a84e-4b7b-8437-af43f0362c5e/screenshot-specific-bug.jpg" width="400" height="170" /></figure>

Be vague in your search, especially if the bug affects a feature that’s not very popular. For example, for <a href="https://bugs.webkit.org/show_bug.cgi?id=24444">this Webkit bug</a>, a search for “<a href="https://bugs.webkit.org/buglist.cgi?query_format=specific&amp;order=relevance+desc&amp;bug_status=__all__&amp;product=&amp;content=input+file+multiple+dom+property">multiple file</a>” would show the bug, whereas a search for “<a href="https://bugs.webkit.org/buglist.cgi?query_format=specific&amp;order=relevance+desc&amp;bug_status=__all__&amp;product=&amp;content=input+file+multiple+dom+property">input file multiple dom property</a>” would not; I was inexperienced when I filed it and didn’t know the exact terminology at the time. If the bug tracker is public, sometimes searching on Google also helps (adding <code>site:url-of-bug-tracker</code> after your keywords).

If your issue has indeed been reported, **some bug trackers allow voting**. Mozilla’s Bugzilla gives every user a limited number of votes (the limit is in the thousands), which the user can use on any bug they wish. Also, Chrome’s bug tracker features a star in the top-left corner, which you can click to indicate that you consider the bug important. I’m not yet sure whether the developers take this into account, but voting certainly doesn’t hurt.

## Different Engines, Different Bug Trackers

Every browser has its own bug-tracking system (BTS).

*   [Internet Explorer](https://www.google.com/url?q=https%3A%2F%2Fconnect.microsoft.com%2FIE&sa=D&sntz=1&usg=AFQjCNE_bRQoc6sB7b_qgfeL_ZTOgyJg3w) ([new bug](https://connect.microsoft.com/IE/feedback/CreateFeedbackForm.aspx?FeedbackFormConfigurationID=4810&FeedbackType=1))
*   [Firefox](https://bugzilla.mozilla.org/) ([new bug](https://bugzilla.mozilla.org/enter_bug.cgi?format=__default__&product=Core&short_desc=))
*   [Opera wizard](https://bugs.opera.com/wizard/)
*   [Webkit](https://bugs.webkit.org/) ([new bug](https://bugs.webkit.org/enter_bug.cgi?product=WebKit))
*   [Chrome](https://www.chromium.org/for-testers/bug-reporting-guidelines) ([new bug](https://code.google.com/p/chromium/issues/entry))

Safari and Chrome share the same engine (Webkit), so bugs that can be reproduced in both should be reported in Webkit’s BTS. Chrome has its own BTS as well, intended for bugs that are reproducible only in it. Also, if you’re dealing with a JavaScript bug in Chrome, report it to the <a href="https://code.google.com/p/v8/issues/list">V8 bug tracker</a>.

You will need to create a free account to file bugs with any of these bug trackers (except Opera’s Wizard). But it’s a one-time thing, and it’s useful because it allows you to easily track bugs that you’ve reported.

All of the browsers’ bug trackers are public, with one exception: Opera’s. You can report Opera bugs through the public form I linked to above, but to access the BTS and to discuss your bug and monitor its progress, you will need to become an Opera volunteer (or an employee!) and sign an NDA. Volunteering is by invitation only, but if you submit a lot of good bug reports, there’s a good chance you’ll be invited.

## Filing A Good Bug Report

The most important part of a good bug report (and the one most commonly done wrong) is the reduction. Hopefully, you’ve done that already, so the hardest part is over with. The rest probably won’t take you more than five minutes.

### Providing A Good Summary

A good summary is the second-most important part of a bug report. Don’t be afraid to be verbose, if it actually adds something (don’t just babble). To take one from <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=531371">an actual report</a>,
<blockquote>“Background image disappears when <code>body{display:table}</code> is used (common CSS hack for correct centering + scrolling in Firefox)”</blockquote>

… is better than “Background image disappears when <code>body{display:table}</code> is used,” which in turn is better than “Disappearing background image.” Of course, all three are better than “CSS broke. Please fix!!!!11”

Sometimes you may want to add keywords to the beginning of the summary to make the report more findable. For example, if your bug is about CSS3 gradients, you could prepend the summary with “[css3-images].” To get an idea of the exact tags used in a module, look at other bug reports. It will usually be the same as the id of the specification, which is located at the end of its URL path. For example, for the CSS3 module “<a href="https://www.w3.org/TR/css3-background/">Backgrounds and Borders</a>,” the URL is <a href="https://www.w3.org/TR/css3-background/"><code>https://www.w3.org/TR/css3-background/</code></a>, and the spec’s id is <code>css3-background</code>. Also, these summary “tags” can be OS-specific. For example, if your bug is reproducible only in Mac OS X, then prepend your summary with “[Mac].” If the bug is about something that used to work fine in previous versions, then prepend your summary with “[Regression],” or add “regression” as a keyword if the BTS has such a feature.

### Categorizing The Bug

The category to which your bug belongs is usually quite obvious, provided you take a few seconds to check them all. For CSS bugs, these are the most common candidates:

*   Internet Explorer: “CSS and HTML”;
*   Firefox: “Style System (CSS),” all the “Layout” components;
*   Opera Wizard: “Web page problem”;
*   Webkit: “CSS, Layout and Rendering”;
*   Chrome: doesn’t let you categorize bugs (its developers do it for you).

John Resig suggests some <a href="https://ejohn.org/blog/a-web-developers-responsibility/">ways to categorize JavaScript bugs</a>.

### Other Fields

*   You can be as verbose in the “Description” field as you need to be. Explain the bug in detail (what you expected to see, what was actually displayed, etc.) and any interaction needed to reproduce it. Then mention any workarounds you found, how other browsers handle the case, and any other notable observations. But don’t start babbling about what you were doing when you discovered the bug, no matter how funny or interesting you think it is. QA time is precious; please don’t waste it with irrelevant detail.
*   The “Product” will usually be “Core.” If you have a choice between “Core” and the browser’s name, choose “Core,” because bugs filed under the browser’s name are usually for the UI.
*   Regarding “Platform” and “OS,” try to test in other operating systems if you can. (You do test your websites in different operating systems, right?) If the bug is reproducible in all OS’, then select “All.” If it’s reproducible in only one, then mention that in your description and/or summary.
*   Avoid changing the “Severity” or “Priority” fields, because you will tend to overestimate.
*   Most people who report bugs don’t fill in the “CC” field. But if you know someone who works for a given browser vendor, especially someone who frequently replies to similar bug reports (browse the reports if you’re not sure), then cc’ing them might help the bug get noticed more quickly. In some cases, this could mean the difference between a bug report getting noticed in a few days and one going unnoticed for months.
*   If you have the time to take a screenshot, by all means do so, especially if the bug is reproducible in only one OS.

### What Not To Do

Never, ever report multiple bugs in the same report. Handling these is very hard for browser developers. Think about it: what status should they assign to a report if they fix one bug, but the other turns out to be a duplicate? Or only one of the two turns out to be a bug? You get the idea.

I can understand that you might be frustrated from having had to deal with that bug, but being rude won’t help. Stay polite, and keep thoughts like “I can’t believe you can’t even get this right, you morons!” to yourself.

## Some Examples

### Example 1: Reducing The Original Problem, Realizing It Was Your Mistake

While developing <a href="https://tweeplus.com">twee+</a>, a handy little app for posting long tweets (and my entry in the 10K Apart contest), I found out that even though it worked in mobile Safari for reading, it crashed when you tried to make an edit. I had no idea what might have been causing this, so I made a copy and started reducing. After commenting out parts of the JavaScript, I found that if I removed the <code>onresize</code> event handler, the problem stopped occurring. And then it made total sense: I adjust the rows of the textarea when the user resizes the window. However, **in Mobile Safari, this triggered a resize event, resulting in a dreaded infinite loop**. So I removed the resize event handler for mobile. It’s not like the user can resize the window there anyway.

### Example 2: Making a Reduction From Scratch, Filing A Bug

A big part of <a href="https://fronteers.nl/congres/2011/workshops/css3-for-web-developers-lea-verou">my upcoming CSS3 workshop in Amsterdam</a> is hands-on challenges. Attendees will download my slide deck (which is essentially an HTML + CSS + JavaScript app) and try to solve some 5- or 10-minute challenges on everything taught. A challenge slide would look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03c868a3-e12c-4609-909b-d48fa95a4fa4/screenshot-show-solution-1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02f7dfba-8542-420a-b273-88f2c88901ee/screenshot-show-solution-1-500.jpg" width="500" height="292" /></a></figure>

I prepared a lot of the slides in Chrome. When I opened them in Firefox, I was greeted with this ugly sizing of the textarea:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40a17b72-b661-4535-b5aa-8bb00ffc5682/screenshot-show-solution-2.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a240332b-b415-489c-b23d-1d3560f4fcc5/screenshot-show-solution-2-500.jpg" width="500" height="307" /></a></figure>

In this case, I didn’t follow the reduction process laid out above, because I had a hunch that the bug was related to the way I sized the textarea. So, I fired up JsFiddle and made <a href="https://jsfiddle.net/leaverou/PTxSE/">this simple example</a>, in which the bug could still be reproduced. I then tested it in Opera and observed that it behaved like Firefox, so it was probably Webkit that was buggy. I tested it in the Webkit nightlies and saw that it hadn’t yet been fixed.

Before going any further, I tried to see whether the bug was more generic. Does it happen only with textareas or with all replaced elements? I went ahead and <a href="https://jsfiddle.net/leaverou/PTxSE/3/">tested <code>&lt;img&gt;</code></a> and <a href="https://jsfiddle.net/leaverou/PTxSE/4/"><code>&lt;input&gt;</code></a> and found that it happens only with form fields. I did another test to see whether it also happened with top/bottom rather than left/right. <a href="https://jsfiddle.net/leaverou/PTxSE/5/">It did not</a>. I also tested on Windows, and it’s reproducible there as well.

<a href="https://www.w3.org/TR/css3-box/#abs-replaced">The specification</a> confirmed that it was indeed a bug: “The used value of ‘<a href="https://www.w3.org/TR/css3-box/#width">width</a>’ and ‘<a href="https://www.w3.org/TR/css3-box/#height">height</a>’ is determined as for <a href="https://www.w3.org/TR/css3-box/#inline-replaced">inline replaced elements</a>.” After a bit of searching on Google, I found <a href="https://snook.ca/archives/html_and_css/absolute-position-textarea">this blog post</a>, which describes the bug but does not mention an official bug report. So, I searched Webkit’s bug tracker for “textarea absolute,” “textarea positioned” and “input positioned” and couldn’t find anything relevant. It was bug-reporting time!

I went ahead and created <a href="https://bugs.webkit.org/show_bug.cgi?id=67566">this bug report</a>. Let’s hope it goes well.

## What Happens Next?

At some point, usually after a few days or weeks, someone will modify your bug’s status. If it turns out to be a “duplicate,” don’t feel bad: it happens to the best of us, even employees of the browser vendors themselves. If the status gets “confirmed” (usually with the status “new”), this is a good indication that it is indeed a bug and that you did the right thing by reporting it. Last but not least, if the new status is “assigned,” it means someone is actively working on the issue (or plans to do so soon), so it has a high chance of getting fixed soon.

When your bug gets a status of “resolved,” check the “resolution” field. If it says “wontfix,” it means that they’re not planning to rectify the issue, for reasons usually stated in detail in an accompanying comment. The reason is usually either that it’s not a bug (in which case, the most appropriate resolution status is “invalid”) or that they just don’t want to work on it for the time being. If the latter, you could argue your case and explain why the bug is important, but don’t get your hopes up. Last but not least, if it’s “fixed,” you can congratulate yourself on doing your part to make the Web a better place.

### Other Resources

*   “[A Web Developer’s Responsibility](https://johnresig.com/blog/a-web-developers-responsibility/),” John Resig
*   “[Test Case Reduction](https://www.webkit.org/quality/reduction.html),” Webkit
*   “[The Most Important Field in a Bug Report: The Summary](https://dbaron.org/log/20100426-bug-summary),” David Baron
*   “[How to Submit Good Bug Reports](https://www.opera.com/support/bugs/),” Opera
*   “[How to Submit a Good Bug Report](https://connect.microsoft.com/IE/content/content.aspx?ContentID=16254),” Internet Explorer

*Thanks a lot to <a href="https://twitter.com/dstorey">David Storey</a>, <a href="https://nimbupani.com/">Divya Manian</a>, <a href="https://paulirish.com/">Paul Irish</a>, <a href="https://fantasai.inkedblade.net/">Elika Etemad</a> and <a href="https://oli.jp/">Oli Studholme</a> for their helpful tips and reviews.*

{{% ad-panel-leaderboard %}}

### Further Reading

*   [The Design Community Offers Its Favorite Bits of Advice](https://www.smashingmagazine.com/2011/03/the-design-community-offers-its-favorite-bits-of-advice/)
*   [Dear Web Design Community, Where Have You Gone?](https://www.smashingmagazine.com/2011/03/dear-web-design-community-where-have-you-gone/)
*   [High-Impact, Minimal-Effort Cross-Browser Testing](https://www.smashingmagazine.com/2016/02/high-impact-minimal-effort-cross-browser-testing/)
*   [The Principles Of Cross-Browser CSS Coding](https://www.smashingmagazine.com/2010/06/the-principles-of-cross-browser-css-coding/)

{{< signature "al, mrn" >}}
