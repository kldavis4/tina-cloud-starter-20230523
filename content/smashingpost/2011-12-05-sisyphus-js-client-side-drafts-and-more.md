---
title: Auto-Save User’s Input In Your Forms With HTML5 And Sisyphus.js
slug: sisyphus-js-client-side-drafts-and-more
image: null
date: 2011-12-05T15:31:47.000Z
author: alexander-kaupanin
description: >-
  Have you ever been filling out a long form online or writing an eloquent and spirited comment when suddenly the browser crashes? Or perhaps you closed the browser tab accidentally, or your Internet connection cuts off, or the electricity goes down (and, being ever obedient to Murphy’s Law, you had no backup power supply). If not, then you’re lucky. But no one is protected from such minor catastrophes.
categories:
  - Coding
  - JavaScript
---
This article is the third in our new series that introduces new, useful and freely available tools and techniques, developed and released by active members of the Web design community. The first article covered [PrefixFree](https://www.smashingmagazine.com/2011/10/12/prefixfree-break-free-from-css-prefix-hell/); the second introduced [Foundation](https://www.smashingmagazine.com/2011/10/25/rapid-prototyping-for-any-device-with-foundation/), a responsive framework that helps you build prototypes and production code. This time, we’re presenting Sisyphus.js, a library developed by Alexander Kaupanin to provide Gmail-like client-side drafts and a bit more.

### What Problem Needs Solving?

Have you ever been filling out a long form online or writing an eloquent and spirited comment when suddenly the browser crashes? Or perhaps you closed the browser tab accidentally, or your Internet connection cuts off, or the electricity goes down (and, being ever obedient to Murphy’s Law, you had no backup power supply). If not, then you’re lucky. But no one is protected from such minor catastrophes.

[![screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcd8ef39-49f8-4577-a029-2d15ec67dc87/make-everything-better.jpg)](https://www.flickr.com/photos/bjornmeansbear/5081930704/sizes/m/in/set-72157624427149887/)  
_(Image: [Kristian Bjornard](https://www.flickr.com/photos/bjornmeansbear/5081930704/sizes/m/in/set-72157624427149887/))_

Imagine the storm of emotions felt by a user who had to add just a bit more information before submitting a form and then loses all data. Horrible, huh? Now, if only there was a way to recover that data, rather than undertake a [Sisyphean](https://en.wikipedia.org/wiki/Sisyphus) pursuit.

{{% feature-panel %}}

### Existing Solutions

One common solution is to write one’s comments in a local document, saving the file periodically, and then copying and pasting the text into the form once it’s complete. Some forms also allow you to save your draft by clicking a button, but not all forms have this feature, and it’s not the most convenient solution. The product that does this best is Gmail, with its auto-save feature for drafts: just type away, and all of the content is stored automatically, without you even needing to press a button.

After releasing Sisyphus.js, I learned of Lazarus, an extension for Firefox and Chrome that helps to recover form data. But browser plugins lead to an even bigger problem: distribution. Some users don’t have a clue what a browser extension is — many users don’t, in fact, which makes this approach inadequate on a large scale.

The people with a direct line to users are Web developers themselves. So, addressing the problem of user input at the stage of development seems more practical than expecting users to add to their skyscraper of extensions.</p>

## A Solution: Sisyphus.js

Implementing Gmail-like auto-saving of drafts is not straightforward at all. I wanted the solution to be simple and easy to use, which would rule out the use of server-side magic.

The result is an unassuming script that stores form data to the local storage of the user’s browser and restores it when the user reloads or reopens the page or opens the page in a new tab. The data is cleared from local storage when the user submits or resets the form.</p>

### How to Use It

Implementing Sisyphus.js is pretty simple. Just select which forms you’d like to protect:

<pre><code class="language-javascript">$('#form1, #form2').sisyphus();</code></pre>

Or protect all forms on the page:

<pre><code class="language-javascript">$('form').sisyphus();</code></pre>

The following values are the defaults but are customizable:

<pre><code class="language-javascript">{
customKeyPrefix: ’,
timeout: 0,
onSave: function() {},
onRestore: function() {},
onRelease: function() {}
}</code></pre>

Let’s break these options down:

*   `customKeyPrefix`  
    An addition to key in local storage details in order to store the values of form fields.
*   `timeout`  
    The interval, in seconds, after which to save data. If set to `0`, it will save every time a field is updated.
*   `onSave`  
    A function that fires every time data is saved to local storage.
*   `onRestore`  
    A function that fires when a form’s data is restored from local storage. Unlike `onSaveCallback`, it applies to the whole form, not individual fields.
*   `onRelease`  
    A function that fires when local storage is cleared of stored data.

Even after Sisyphus.js has been implemented in a form, you can apply it to any other form and the script won’t create redundant instances, and it will use the same options. For example:

<pre><code class="language-javascript">// Save form1 data every 5 seconds
$('#form1').sisyphus( {timeout: 5 } );

…

// If you want to protect second form, too
$('#form2').sisyphus( {timeout: 10} )

// Now the data in both forms will be saved every 10 seconds</code></pre>

Of course, you can change options on the fly:

<pre><code class="language-javascript">var sisyphus = $('#form1').sisyphus();

…

// If you decide that saving by timeout would be better
$.sisyphus().setOptions( {timeout: 15} );

…

// Or
sisyphus.setOptions( {timeout: 15} );</code></pre>

### Usage Details

**Requirements:** Sisyphus.js requires jQuery version 1.2 or higher.

**Browser support:**

*   Chrome 4+,
*   Firefox 3.5+,
*   Opera 10.5+,
*   Safari 4+,
*   IE 8+,
*   It also works on Android 2.2 (both the native browser and Dolphin HD). Other mobile platforms have not been tested.

**Download the script:** [Sisyphus.js and the demo](https://simsalabim.github.com/sisyphus/) are hosted on GitHub; the minified version is about 3.5 KB. A [road map](https://github.com/simsalabim/sisyphus/issues?labels=feature) and [issue tracker](https://github.com/simsalabim/sisyphus/issues?labels=) are also available.

{{< signature "al" >}}

