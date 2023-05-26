---
title: 'Introducing LiveStyle: Better, Stronger And Smarter CSS Live Reload'
slug: release-livestyle-css-live-reload
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad3c02b8-2786-4c30-a2d7-6b847d80049f/emmet-livestyle-preview-opt.png
date: 2013-08-08T09:59:01.000Z
author: sergey-chikuyonok
description: >-
  Tools for live CSS editing aren't new these days. You may already be familiar
  with tools like [LiveReload](https://livereload.com/),
  [CodeKit](https://incident57.com/codekit/) and [Brackets](https://brackets.io/).
  So, why would someone ever need to create yet another tool and even call it a
  "live CSS editor of the new generation"?
categories:
  - Coding
  - Tools
  - Workflow
  - CSS
  - JavaScript
---
_In the past, we featured some exciting tools and libraries: [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/), [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/), [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/), [GuideGuide](https://www.smashingmagazine.com/2012/01/03/guideguide-free-plugin-for-dealing-with-grids-in-photoshop/), [Gridpak](https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/), [JS Bin](https://www.smashingmagazine.com/2012/07/23/js-bin-built-for-sharing-education-and-real-time/) and [CSSComb](https://www.smashingmagazine.com/2012/10/02/csscomb-tool-sort-css-properties/). All of them have been developed and released by active members of the Web design community as open-source projects. Today, we present **LiveStyle**, a plugin for live bi-directional (editor ↔ browser) CSS editing of the new generation! — Ed._</em>

Tools for live CSS editing aren't new these days. You may already be familiar with tools like [LiveReload](https://livereload.com/), [CodeKit](https://incident57.com/codekit/) and [Brackets](https://brackets.io/). So, why would someone ever need to create yet another tool and even call it a "live CSS editor of the new generation"?

The tool I'd like to introduce to you today is [Emmet LiveStyle](https://livestyle.emmet.io/). This plugin takes a completely different approach on updating CSS. Unlike other live editors, it doesn't simply replace a whole CSS file in a browser or an editor, but rather _maps changes_ from one CSS file to the other.

In order to better understand how LiveStyle works, let us first take a look at the current state of live edit tools.</p>

## A State Of Live Edit Tools

Most live reload/edit tools work in a pretty simple manner: They look out for CSS files in a special folder and update the Web browser once something has been changed. So users have to edit the CSS file and save it before they can preview the changes. Not exactly a "live" update, but this simplicity has its own benefits. You can use these tools together with preprocessors so your webpage gets updated automatically whenever you save your LESS or SASS file.

{{% feature-panel %}}

About a year ago, a new breed of live editing tools appeared. Editors like [Brackets](https://brackets.io/) and [WebStorm](https://www.jetbrains.com/webstorm/) integrate with Web browsers (more specifically, with Google Chrome) directly and allow you to see updates instantly, e.g. without saving a file. They send the updated file content to the browser every time you change something. But in order to use live edit, they require a special built-in Web server to be used to properly map your local files with browser URLs.

Getting changes from DevTools back into your CSS file is not so popular. There are a few tools like [Tin.cr](https://tin.cr/) that allow you to save your DevTools changes back to the file (the Chrome Dev team introduced [Chrome Workspaces](https://www.youtube.com/watch?v=kVSo4buDAEE) recently for this very same purpose).

Summing up, to use these tools for **truly live development** (deliver updates from editor to browser _and_ vice versa), you have to:

*   Use the same CSS files in your text editor and Web browser.
*   Keep your files in a local file system.
*   In some cases, use a special tooling Web server.

All of these tools work just fine once you've started your project development, but what happens when your website goes into production? What if you concatenate and minify your CSS code for better performance and UX? Most of these tools become pretty much useless:

*   You can't use the tooling Web server because you need to use your own one for backend/CMS.
*   You can't get the DevTools changes back into your file since (concatenated and minified) CSS within browser is not the same as your source code.
*   In some large projects, you can't use a local file system — your files might be in your private sandbox on the dev server.

So, you don't have much options now, right? If you ask me, there are two things that must be eliminated:

1.  Any middleware between the browser and editor. The editor should be able to talk to the browser directly, without using any files or Web servers.
2.  Full CSS content swapping. The browser or editor must receive only the updated sections, not the entire source.

To solve these issues, LiveStyle was created. Unlike other tools, it does not work directly with files, nor does it replace them in the browser or editor. It _maps changes_ from one source to the other.</p>

## How LiveStyle Works

Imagine you're editing a CSS file and I ask you, "What did you just change?"

Your answer could be: "On line 2, I replaced the characters from 12 to 16 with the word `red`." But I'm pretty sure your answer will rather end up being: "In the `body` selector, I changed the `background` property value to `red`." In other words, instead of _describing how bytes_ were changed within the text file, you would _describe how the structure of the CSS file_ was changed.

But the thing is, if you pass this very same information to another developer, i.e. "in `body`, change `background` value to `red`," he can perform the very same changes in _his own CSS file_ and get the very same result!

This is exactly how LiveStyle works. Whenever you update a CSS source, it performs structural comparisons with the previous state and creates a special patch that describes how the CSS structure was changed. This patch is then transmitted to all clients and is applied to the associated CSS source.

This approach gives you the following benefits:

*   You can associate two completely different CSS sources for live editing. For example, you can take a minified and concatenated CSS source in a browser, associate it with one of the source CSS modules in an editor, and use them for fully bi-directional live editing.
*   You don't need to keep your files in a local file system. You can simply open it directly from the FTP, your fancy network mount, or whatever. If a file can be opened by a text editor, you can use it for live editing as well.
*   You can even create new, untitled files and use them for live editing right away!
*   You don't need a special Web server, code snippet or file watcher, everything works in the editor and browser.

Here's a demo video demonstrating how this approach works in real life:

In the video above, I used the Facebook main page to demonstrate the power of LiveStyle. There's no doubt it's one of the largest and complex websites on the planet and I don't have access to either the Facebook server nor its CSS source. But I need just a few clicks to start the live CSS editing. Imagine how easy it is for you to do the very same for your own website!

## Installation

Currently, LiveStyle works in Google Chrome, WebKit Nightly (for iOS apps live editing) and Sublime Text. The installation process is pretty straightforward:

1.  Install the "LiveStyle" plugin from the Package Control in Sublime Text.
2.  Install the [extension for Google Chrome](https://chrome.google.com/webstore/detail/diebikgmpmeppiilkaijjbdgciafajmg).

The WebKit extension can be installed directly from Sublime Text, just pick `Tools` → `Install LiveStyle for WebKit extension` menu item, or run the `LiveStyle: Install WebKit extension` command from the Command Palette.

That’s it! Now you can start using LiveStyle to tweak your websites. If you have any trouble with the LiveStyle installation or need any further assistance, please go to the [official installation guide](https://livestyle.emmet.io/install/).</p>

## Using LiveStyle

To start with the live CSS editing, simply follow these four easy steps:

1.  Start Sublime Text and open a CSS file or create new one.
2.  Start your Chrome browser and go to the page you wish to edit.
3.  Open DevTools, go to the LiveStyle panel and check the **Enable LiveStyle for current page** option.
4.  Once enabled, you'll see a list of the external style sheets on the left and a list of editor files on the right. Simply pick the editor file that should be associated with the browser and you are done!

Note that the editor's files list is automatically updated every time you create, open or close files within the editor.

> **Important**: You must keep DevTools open during your live editing session and for every window (in multi-view mode). You don't have to be on the LiveStyle panel all of the time, but DevTools must remain open otherwise the incoming updates won't be applied.

## New Workflows

LiveStyles' CSS patching concept introduces a number of workflows you can use in your development process:

### Simple Mode

This one's a basic one-to-one live editing mode. Simply associate any external CSS file in the browser and the editor, and start editing. All your editor changes will be automatically reflected in the browser and your DevTools updates will be reflected in the editor.

If your browser file is large enough, your editor updates may take some time to apply. If you want to speed things up or you don't have any external style sheets on your page, you can create a new style sheet by pressing the `Add file` button and using it for live updates.</p>

### Multi-View Mode

Multi-view mode is ideal for tweaking responsive Web designs. Open multiple windows of the same page and resize them for your RWD breakpoints. **DevTools must be open for each window**, otherwise it won't apply any updates.

In multi-view mode:

*   All editor updates will be applied to all windows.
*   All DevTools updates will be applied to the editor and all other windows with the same page.
*   All LiveStyle panel updates (like file associations) will be automatically applied to all other windows with the same page.</p>

### Multi-Site Mode

This mode is useful if your Web project has different versions of desktop and mobile websites but shares the same CSS code base.

Just like in the "multi-view mode", you need to open a few windows with your website's versions and associate your browser CSS files in the LiveStyle panel _with the same editor file_. LiveStyle will use this editor file as a reference to patch your browser files with incoming updates, even from DevTools.</p>

### Designer Mode

This mode is for designers who work on large projects and don't have direct access to the CSS sources. (Please note that this is an experimental mode and is subject to change!)

Imagine you spot an error on your production website. Instead of asking the developer to spend some time with you to fix these issues, you can fix them by yourself and send the developer a patch so he can apply it later to the original source.

All LiveStyle updates are recorded into the "Patch history", available in the LiveStyle DevTools panel. A new patch history entry is created automatically every time you open or refresh a Web page. Click on the "Patch history" pop-up entry to apply recorded patches and click on the red icon on the right to download it.

So, all you have to do is to tweak the layout in DevTools and download the most recent patch history entry. You can send the downloaded patch to the developer so he can apply it to original CSS source.

Note that in this mode _you don't need Sublime Text extension at all_; you just need the DevTools extension.</p>

## Behind The Scenes

I'm pretty sure anyone who's tech savvy is interested in how LiveStyle works and what lessons I learned from this project.</p>

### How LiveStyle Patches CSS

When you edit styles in DevTools, you see that properties in selectors are modified accordingly: Existing selectors are updated and absent ones are created — even whole CSS selectors are automatically created (and I really hope this is the only thing you see).

But did you notice there's no CSS formatting configuration step? You didn't have to open any preferences file to specify that you don't need space after a colon and all your properties should be written in single lines.

That's because LiveStyle tries to match your coding style as close as possible. Whenever it needs to insert something in the document, it analyzes your personal coding style and automatically creates formatting rules for you.

This is also possible due to the original Emmets' `cssEditTree` component. This module provides a DOM-like interface for CSS modifications, e.g. `rule.value('background', 'red')`, `rule.add('padding', '10px')`, but also keeps track of CSS token positions and inherits formatting rules for newly created properties. You can actually create an Emmet extension and reuse this module to automate your CSS modification tasks (for example, like in the [Update Image Size action](https://docs.emmet.io/actions/update-image-size/)).</p>

### Performance

As described earlier, LiveStyle doesn't simply swap CSS content, it parses CSS into a tree, compares it with its previous state and generates a special patch. On the other end, it also has to parse CSS, locate proper place to patch, analyze your coding style and then create patched CSS source. And everything must be done after each keystroke which means that LiveStyle should be fast — _blazingly fast_.

I had to use some advanced tricks to make this possible; I had to optimize for Garbage Collector, optimize for JIT, optimize function inlining and even multi-threading programming.</p>

### JavaScript Optimization

LiveStyle is written entirely in JavaScript. Thanks to Google DevOps, we have a brilliant V8 JavaScript engine (powers Chrome and PyV8, used to run JS in Sublime Text) and DevTools for debugging JS performance.

V8 can run JavaScript very fast, but it's not a magic box. We have to obey some rules to make it work that way.

The very first thing we need to be able to start optimization is a working product, covered by unit tests. "Premature optimization is the root of all evil", you know.

Once we have our product up and running, start using Profiler to determine slow parts of your code. Chrome and Firefox have awesome built-in profiles and many tutorials on how to use them, so this shouldn't be a problem.

Among other things, the great performance boost was achieved by replacing array iterators like [`Array.forEach`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) with plain loops in critical parts of the performance. This technique is called "[Inlining](https://en.wikipedia.org/wiki/Inline_expansion)". Plain loops are much faster than native implementations of `Array.forEach` and some libraries like [Lo-Dash](https://lodash.com) use the very same technique to run faster. Despite the fact that I've heavily used Lo-Dash in LiveStyle, I did use plain loops in performance-critical parts since every function call has its own small performance penalty.

As soon as all parts were optimized, the slowest process was the _garbage collection_ (GC). GC is a process of removing unneeded data from memory. In JavaScript, we don't have direct access to the garbage collector so we can't, for example, delay its execution and explicitly call it again later. The only thing we can do here is to avoid producing so much garbage.

Consider the following example:

<pre><code class="language-css">
function getSize(obj) {
    return {
        width:  obj.left - obj.right,
        height: obj.bottom - obj.top
    };
}

var size = getSize(parent);
child.style.width  = size.width;
child.style.height = size.height;
</code></pre>

In this example, we use the `getSize()` function as the utility method to calculate width and height from the given object. While this example is pretty simple, it actually produces a lot of garbage; If we called the `getSize()` method, say, 10,000 times, it will generate 10,000 objects that are not required for further program execution, so they must be collected by the GC.

A better implementation of the `getSize()` function may look like this:

<pre><code class="language-css">var _size = {};
function getSize(obj) {
    _size.width  = obj.left - obj.right;
    _size.height = obj.bottom - obj.top;
    return _size;
}
</code></pre>

In this example, even if the `getSize()` function is called 100,000 times, only one object will be created in the memory — which greatly reduces GC calls.

I achieved a huge performance boost with all of these manipulations, and it still wasn't the end. Now, we can make our app run even faster with the help of the just-in-time (JIT) compiler.

Since LiveStyle parses CSS, it creates a lot token objects that should be accessed by the patcher very often. I analyzed my code and saw that these token objects are modified during runtime, e.g. new properties were added to some of these objects.

V8's JIT optimizer has a so-called "Hidden Class" feature, a special assembly that optimizes access to properties of similar objects. And every time we add a new property to an existing object, we break this optimization.

So I made my general optimization: I rewrote part of LiveStyle's engine so token objects could be automatically created with all of the properties required in advance and that these objects can be reused across different parts of the app, which reduces garbage collection in general.

About a half of this enormous performance boost was achieved by optimizing JS for V8 internals. In order to demonstrate how much the LiveStyle performance boost was optimized, here are some numbers from my MacBook Air:

*   Creating patch from 15 Kb CSS source: `18 ms`
*   Applying patch on 584 Kb CSS source: `212 ms`

Pretty good I'd say, assuming that most live reload tools need a 1-second timeout before reloading the browser after a CSS file has been changed.</p>

## Future Plans

During the first days of public beta testing, LiveStyle proved that its patching algorithm is pretty stable and solid. There have been no reports of broken CSS or invalid results. In fact, LiveStyle actually helped some people to find bugs in their CSS. And there's still a lot of work left to do: Support more browsers and editors and, of course, add preprocessors support.

In the demo video above, you saw how the live bi-directional SCSS editing is done. The editor changes in SCSS are instantly reflected in the browser's CSS, and browser changes in plain CSS are instantly pushed into the right places of SCSS. But this is just an experiment demonstrating how powerful LiveStyle can be. For real-world usage, it basically requires a new SCSS processor to be written.

So, I hope you'll find LiveStyle useful and spread the word! If the community support is strong enough, I'll try my best to find funding for further development. **LiveStyle is currently free** during public beta testing, but will be available for a small fee after its official release.

If you experience any issues with LiveStyle or have any suggestions, feel free to create a ticket at [plugin repo](https://github.com/emmetio/livestyle-sublime/issues). Thanks!

### Further Reading

*   [Writing Fast, Memory-Efficient JavaScript](https://www.smashingmagazine.com/2012/11/05/writing-fast-memory-efficient-javascript/)
*   [Performance Tips For JavaScript In V8](https://www.html5rocks.com/en/tutorials/speed/v8/)
*   [Using Web Workers](https://developer.mozilla.org/en-US/docs/Web/Guide/Performance/Using_web_workers)

{{< signature "il" >}}

