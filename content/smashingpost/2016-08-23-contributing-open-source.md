---
title: 'I Contributed To An Open-Source Editor, And So Can You'
slug: contributing-open-source
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394a5d09-1464-435e-a73e-91d1049b9283/editor-500px-preview-opt.png
date: 2016-08-23T17:20:47.000Z
author: christian-heilmann
description: >-
  A few months ago, Jason Grigsby’s [post about autocompletion in
  forms](https://cloudfour.com/thinks/autofill-what-web-devs-should-know-but-dont/)
  made the rounds. I loved the idea of allowing users to fill in their credit
  card details by taking a picture of their card. What I didn’t love was
  learning [all of the possible values for autofill by
  heart](https://html.spec.whatwg.org/multipage/forms.html#autofill). I’m
  getting lazy in my old age.

  Lately, I’ve gotten spoiled from using an editor that does intelligent
  autocompletion for me, something that in the past only massive complex IDEs
  offered. Opening my editor of choice, I created an `input` element and added
  an `autocomplete` attribute, only to find that the code completion offered me
  the state of `on` or `off`. Disappointing.
categories:
  - Coding
  - Open Source
  - Community
---
A few months ago, Jason Grigsby’s <a href="https://cloudfour.com/thinks/autofill-what-web-devs-should-know-but-dont/">post about autocompletion in forms</a> made the rounds. I loved the idea of allowing users to fill in their credit card details by taking a picture of their card. What I didn’t love was learning <a href="https://html.spec.whatwg.org/multipage/forms.html#autofill">all of the possible values for autofill by heart</a>. I’m getting lazy in my old age.

Lately, I’ve gotten spoiled from using an editor that does intelligent autocompletion for me, something that in the past only massive complex IDEs offered. Opening my editor of choice, I created an <code>input</code> element and added an <code>autocomplete</code> attribute, only to find that the code completion offered me the state of <code>on</code> or <code>off</code>. Disappointing.

What I wanted was the following:

<figure><img style="filter: url('#toggleGifsIndicatorFilter');" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/305c6968-644f-4702-81e2-37bc5602f9fc/autocomplete.gif" alt="All possible values for autocomplete offered by this editor" width="500" height="" /><br>
<figcaption>All possible values for <code>autocomplete</code> offered by this editor</figcaption></figure>

The great thing about our development environments these days is that we build the tools we use in the technologies that we use them to write. Yes, this sounds confusing — we’ve reached code Inception. <a href="https://nodejs.org/en/">Node.js</a> allows us to run JavaScript on the back end, and with <a href="https://electron.atom.io/">Electron</a> we can create installable applications for all platforms using HTML, CSS and JavaScript.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [So You’ve Decided To Open-Source A Project At Work](https://www.smashingmagazine.com/2013/12/open-sourcing-projects-guide-getting-started/)
*   [A Short Guide To Open Source Licenses](https://www.smashingmagazine.com/2010/03/a-short-guide-to-open-source-and-similar-licenses/)
*   [How To Start An Open-Source Project](https://www.smashingmagazine.com/2013/01/starting-an-open-source-project/)
*   [The Case For Open-Source Design](https://www.smashingmagazine.com/2010/09/the-case-for-open-source-design-can-design-by-committee-work/)

<a href="https://atom.io/">Atom</a> was the first editor to use this technology and to allow for contributions by being open source, closely followed by Microsoft’s <a href="https://code.visualstudio.com/">Visual Studio Code</a>.

Almost all of the other editors in use allow us to write extensions, plugins or snippet collections in various formats. I deliberately didn’t want to write a plugin or extension, but rather wanted to add this functionality to the core of the editor. Plugins, extensions and snippets have their merits; for example, they are easy to update. The problem is that they need to be found and installed per user. I considered autocompletion too important and wanted to hack the editor itself instead.

Both Atom and Visual Studio Code are available on GitHub and come with instructions on how to extend them. The challenge is that this can feel daunting. I’m here today to show you that it isn’t as tough as you might think. Visual Studio Code is my current editor, and it features amazing autocompletion. That’s what I wanted to tackle.

Extensible and customizable tools are nothing new. Most of what we use can be extended in one way or another, whether in the form of add-ons, plugins or specialist languages. The first editor I used in anger was Allaire and Macromedia’s <a href="https://en.wikipedia.org/wiki/Macromedia_HomeSite">HomeSite</a>, which had funky languages like <a href="https://en.wikipedia.org/wiki/VTML">VTML</a>, <a href="https://www.ulitzer.com/node/41695">WIZML</a> and JScript, the Windows version of JavaScript at the time. I wrote a lot of extensions and toolbars for that editor, which very much boosted the productivity of my company back then.

Thankfully, these days, companies understand that offering specialist languages is time wasted, when the web stack has grown to become much more interesting to build applications with.

If you download Visual Studio Code now, you will see that my autocomplete feature is a part of it. And here is how I did that.</p>

## 1\. Complain

My first step was to go to <a href="https://github.com/Microsoft/vscode/">Visual Studio Code’s GitHub repository</a> and <a href="https://github.com/Microsoft/vscode/issues/7142">file an issue</a> requesting this feature for the editor. This could also be your final step if you don’t want to do it yourself. Someone else who is looking for something to do for the project might find your complaint and tackle it for you. In my case, I wanted to find out more.</p>

## 2\. Fork The Code

Instead of just filing an issue, I went to the GitHub repository and forked the code. I used my personal account for this. You don’t need to be affiliated with Microsoft or get added to a special group. The repository is public and open. Everybody is welcome. There is even a <a href="https://opensource.microsoft.com/codeofconduct/">code of conduct for contributions</a>, which means that people should be playing nice. I downloaded the code to my hard drive and followed the instructions on how to build the editor locally.</p>

## 3\. Get The Development Workflow In Place

Visual Studio Code is written in Node.js and TypeScript. The development flow starts with a script provided by the team, which gives me a development version of Visual Studio Code running next to the one I am using. A script running on the command line ensures that my changes are captured and that every time I save my code, the development version of the editor restarts and I can test the changes. All of this is nicely documented, from <a href="https://github.com/Microsoft/vscode/wiki/How-to-Contribute#build-and-run-from-source">building and running the code from source</a> to <a href="https://github.com/Microsoft/vscode/wiki/How-to-Contribute#development-workflow">setting up the development workflow</a>. And it is independent of platform — you get instructions for Windows, Linux and Mac OS X.

You can see what this looks like on my computer in the following screenshot. The large-view editor (1) is the one I use to code the other; the one on the right (3) is the development edition; and on the bottom (2) is the script creating the new version of the development edition. Writing an editor in an editor does feel odd, but you get used to it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf64253c-cb85-4406-9698-6534ecb2b59b/editor-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394a5d09-1464-435e-a73e-91d1049b9283/editor-500px-preview-opt.png" alt="Figure 2" width="500" height="279" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf64253c-cb85-4406-9698-6534ecb2b59b/editor-large-preview-opt.png">View large version</a>)</figcaption></figure>

Don’t get discouraged if all of this doesn’t work for you on the first go. I hit a few snags and had to turn to Google and StackOverflow for solutions. The Node.js community was very helpful.</p>

## 4\. Write The Functionality

Next, I was ready to go all in and use TypeScript to write some clever code. I understood that this is where a lot of people throw in the towel, considering it too tough to continue.

My biggest issue was that I had no idea where to begin with this functionality. So, I did what we all do: I did a full text search for <code>autocomplete</code> in the whole project. Using this highly scientific approach, I found an <code>htmlTags.ts</code> file full of tag definitions and arrays of attribute values. I looked up the <code>input</code> element and found this:

<pre><code class="lang-markup">input: new HTMLTagSpecification(
        nls.localize('tags.input', 'The input element represents a typed data field, usually with a form control to allow the user to edit the data.'),
        ['accept', 'alt', 'autocomplete:o', 'autofocus:v', 'checked:v', 'dirname', 'disabled:v', 'form', 'formaction', 'formenctype:et', 'formmethod:fm', 'formnovalidate:v', 'formtarget', 'height', 'inputmode:im', 'list', 'max', 'maxlength', 'min', 'minlength', 'multiple:v', 'name', 'pattern', 'placeholder', 'readonly:v', 'required:v', 'size', 'src', 'step', 'type:t', 'value', 'width']),
</code></pre>

That <code>autocomplete:o</code> looked interesting, so I checked where <code>o</code> is defined. Here’s what I found:

<pre><code class="lang-javascript">var valueSets: IValueSets = {

…

    o: ['on', 'off'],

…

}
</code></pre>

That looked like what was happening when I added an <code>autocomplete</code> attribute. To change that, I went to the <a href="https://html.spec.whatwg.org/multipage/forms.html#autofill">standard definition of possible autocomplete values</a> and copied them.

I created a new value set named <code>inputautocomplete</code> and pasted in the values:

<pre><code class="lang-javascript">var valueSets: IValueSets = {

…

    inputautocomplete: ['additional-name', 'address-level1', 'address-level2', 'address-level3', 'address-level4', 'address-line1', 'address-line2', 'address-line3', 'bday', 'bday-year', 'bday-day', 'bday-month', 'billing', 'cc-additional-name', 'cc-csc', 'cc-exp', 'cc-exp-month', 'cc-exp-year', 'cc-family-name', 'cc-given-name', 'cc-name', 'cc-number', 'cc-type', 'country', 'country-name', 'current-password', 'email', 'family-name', 'fax', 'given-name', 'home', 'honorific-prefix', 'honorific-suffix', 'impp', 'language', 'mobile', 'name', 'new-password', 'nickname', 'organization', 'organization-title', 'pager', 'photo', 'postal-code', 'sex', 'shipping', 'street-address', 't].sort()el-area-code', 'tel', 'tel-country-code', 'tel-extension', 'tel-local', 'tel-local-prefix', 'tel-local-suffix', 'tel-national', 'transaction-amount', 'transaction-currency', 'url', 'username', 'work'],

…

}
</code></pre>

I then went to all of the definitions of elements that support <code>autocomplete</code> and replaced the <code>o</code> with my own <code>inputautocomplete</code>:

<pre><code class="lang-markup">input: new HTMLTagSpecification(
        nls.localize('tags.input', 'The input element represents a typed data field, usually with a form control to allow the user to edit the data.'),
        ['accept', 'alt', 'autocomplete:inputautocomplete' … ]),
</code></pre>

I saved my changes; the script rebuilt the editor; I tried the development version of the editor; and <code>autocomplete</code> worked the way I wanted it to.

## 5\. Send A Pull Request

That was that. I committed my changes to Git (<a href="https://code.visualstudio.com/docs/editor/versioncontrol">inside Visual Studio Code</a>), went to GitHub and added a pull request. A few days later, I got a comment saying that my pull request went through and that what I did would be part of the next build.</p>

## 6\. Be Baffled

Frankly, I didn’t think this was amazing enough to warrant a change to the core of the editor. I just wanted to play around. Many of you might think the same about the work you do. And that’s the thing: We’re wrong. Contributing to open-source projects doesn’t require you to be an amazing developer. Nor does it require you to be famous or part of the in-crowd. Sometimes all you need to do is look at something, analyze it and find a way to improve it.

It is up to us to make the tools we use better. If you see a way to contribute to an open-source project, don’t be shy. You might be the one who comes up with an idea so obvious and so simple that others have overlooked it. You might be the one who makes something more usable or nicer to look at. We all have skills to contribute. Let’s do more of that.

{{< signature "al" >}}

