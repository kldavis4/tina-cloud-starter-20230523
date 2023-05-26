---
title: 'JS Bin: Built For Sharing, Education And Real-Time Rendering'
slug: js-bin-built-for-sharing-education-and-real-time
image: null
date: 2012-07-23T14:53:27.000Z
author: remy-sharp
description: >-
  This is our sixth article in a series that introduces the latest useful and
  freely available tools and techniques, developed and released by active
  members of the Web design community. The first article covered
  [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/);
  the second introduced
  [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/),
  a responsive framework; the third presented
  [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/),
  a library for Gmail-like client-side drafts. The fourth shared a free plugin
  called
  [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/)
  with us, and in the fifth we've announced Erskine's responsive grid generator
  [Gridpak](https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/).
categories:
  - Coding
  - Tools
  - Frameworks
---
<em>This is our sixth article in a series that introduces the latest useful and freely available tools and techniques, developed and released by active members of the Web design community. The first article covered <a href="https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/">PrefixFree</a>; the second introduced <a href="https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/">Foundation</a>, a responsive framework; the third presented <a href="https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/">Sisyphus.js</a>, a library for Gmail-like client-side drafts. The fourth shared a free plugin called <a href="https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/">GuideGuide</a> with us, and in the fifth we've announced Erskine's responsive grid generator <a href="https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/">Gridpak</a>.</em>

## What Is JS Bin?

<a href="https://jsbin.com/">JS Bin</a> is one of the very first public paste bins with the output rendered live in your browser and available to share and edit with the completed output. Released back in 2008, JS Bin is now on its third iteration and after a long and thorough development finally includes some of the original features I wanted to build JS Bin with. It’s completely free to use all its features and open source, and it’s <a href="https://github.com/remy/jsbin">available on Github</a>.

<a href="https://jsbin.com/"><img title="JS Bin: Built For Sharing, Education And Real-Time" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9299d8e-ad5a-41e3-88fd-5c105dc0a276/jsbin-500px-fp.gif" alt="JS Bin: Built For Sharing, Education And Real-Time" width="498" height="400" /></a><br>
<em><a href="https://jsbin.com/">JS Bin</a>, a collaborative JavaScript debugging tool with advanced features.</em>

Essentially, JS Bin exists for two main reasons: a) creating test and debug cases, and collaboratively debugging those cases, and b) to teach and learn from. JS Bin is a collaborative JavaScript debugging tool. It allows you to edit and test JavaScript and HTML (reloading the URL also maintains the state of your code). Once you’re happy you can save, and send the URL to a peer for review or help. They can then make further changes saving anew if required.

{{% feature-panel %}}

## What’s New?

In both current and previous versions, the UX has been a big part of the update. <a href="https://twitter.com/yandle">Danny Hope</a> volunteered his UX experience to this open source project and collaborated very closely with me, allowing us to instantly try out UX ideas, see them in action and decide whether they worked or not.

Again in the spirit of open source collaboration, the project needed to be upgraded from entirely PHP (and not great PHP code!) to Node.js. <a href="https://twitter.com/ac94">Aron Carroll</a> worked for the last few months in his spare time converting the existing JS Bin logic entirely to JavaScript. So as of today, JS Bin is 100% JavaScript.

This move to <strong>Node allows us to introduce two new useful features</strong>:

1.  CodeCasting
2.  Live remote rendering

Both techniques use EventSource and a little technique that I call The Spike.

The key difference between the old and the new JS Bin is that <em>as you type - JS Bin is saving</em>. Means, as soon as your first key stroke lands, you’ve got your own URL. You keep typing, it keeps saving. If you want to stop saving against that version, just create a milestone and live saving will be applied to the new revision.</p>

### CodeCasting

Say you’re running a demonstration or a workshop, and you want all the participants attending to see the code being updated and to see the output of the JavaScript, CSS and HTML, in <em>real-time</em> as you type. With the new JS Bin, you don’t have to be on the same connection, just visit the same URL. Instead of ending the URL with <code>/edit</code>, add <code>/watch</code> and they become voyeurs to your live coding. I’d love to see this live at a conference.</p>

### Live remote rendering

Ever wanted to check the output on multiple platforms: Firefox, Chrome, IE, iPads, Androids, Windows Phone, even a Boot 2 Gecko phone? Maybe all at a once? Maybe without ever hitting refresh?

JS Bin can do this. Simply point the device or browser to your full preview URL (basically removing <code>/edit</code> from the URL) and any changes you make <em>as you type</em> will cause the target device to refresh its content.

The URL structure even has a shortcut, if you’re registered, you can always point the URL to <a href="https://jsbin.com/rem/last">https://jsbin.com/[username]/last</a> and it’ll pull up the last bin you’ve worked on. Along with live remote rendering, I’ve been working with the Adobe Shadow team and they’ve gone ahead and built compatibility with JS Bin directly in to Shadow.

### How the live stuff works

Now, that's an interesting question! And it has a quite simple answer. A while back I tried out a <a href="https://en.wikipedia.org/wiki/Comet_(programming)">comet</a> PHP based version of CodeCasting which was way, way more complicated. It worked, but releasing wasn’t possible as my server couldn’t take more than just a few concurrent sessions. The move to Node years later fixes that.

As you type, the tool sends an Ajax save request (after an idle time of 200ms). On the server side, this triggers an event which says “the bin with <em>this</em> url has just changed”. Now, when viewing the CodeCasting URL or the live remote rendering, each user is connected to the Spike application. It listens for the event that says that a bin has changed, and when that happens, it just finds all the users watching a particular URL and sends them the updated panel (so we only send the CSS panel if the CSS panel changed).

An <a href="https://html5doctor.com/server-sent-events/">EventSource</a> maintains a persistent connection with the server and is listening for those events in the browser. When the event is received, depending on the content type, it’ll either inject the content live, or refresh the page providing users with the latest version of the code.</p>

## Other Important Features

There’s a whole lot more to the new release of JS Bin, and I intend to release screencasts on these features on the <a href="https://twitter.com/js_bin">@js_bin</a> on Twitter.

Some of these features were always part of JS Bin, but hidden inside of the "beta" access - which required a clunkly console command. Now JS Bin 3 adds the much needed UI to do simple things like login to remember your history of bins.

*   Login to remember your history
*   Your full history on a single page with live previews on hover
*   An API to control default settings (useful if you’re preparing a teaching session)
*   Processors, so you can use Markdown, CoffeeScript and LESS, amongst others
*   CSS panel
*   Console panel
*   Support for more libraries (including Bootstrap, Backbone, etc)
*   Native support in [Adobe Shadow](https://labs.adobe.com/technologies/shadow/) (you can point your browser to JS Bin and Adobe Shadow will render the live output automatically)
*   "Edit from your editor and render remotely" feature. You’ll have to [see it](https://youtube.com/watch?v=mY56fNmn2cE) to believe it (idea and code by [@wookiehangover](https://twitter.com/wookiehangover))
*   Our badass robot mascot: [Dave](https://twitter.com/js_bin), the JS Bin Bot (stickers will be made!)

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8a8a759-80ae-4404-b075-2aa896af93d0/jsbin-logo.png" alt="Dave, JS Bin Bot mascot" /><br>
<em>Dave, the JS Bin Bot mascot, created by @yoheis (of PhoneGap fame).</em>

Also, I'd like to add GitHub support, export your history, hosting of static assets <a href="https://github.com/remy/jsbin/blob/master/TODO.md">and further features</a> to the upcoming versions of JS Bin in the nearest future.</p>

## Hack, Play, Share & Get Involved

I’m really excited to share this updated version of JS Bin. Watch out for the twitter account <a href="https://twitter.com/js_bin">@js_bin</a> because it will be posting tips and screencasts, and do <a href="https://github.com/remy/jsbin/issues">send your feedback</a> with issues, ideas or just to tell us where you’re using JS Bin!

