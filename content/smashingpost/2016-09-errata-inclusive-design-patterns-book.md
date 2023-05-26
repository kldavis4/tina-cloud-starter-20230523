---
title: Errata Inclusive Design Patterns Book
slug: errata-inclusive-design-patterns-book
image: null
date: 2016-09-11T19:16:07.000Z
author: heydon-pickering
description: ''
categories: []
---

Mistakes happen to all of us, but we cannot undo mistakes that are caught in a printed book. So let's collect the errata of the [Inclusive Design Patterns book](https://shop.smashingmagazine.com/products/pre-release-inclusive-design-patterns-by-heydon-pickering) below:

**Page 83**

<p>The class <code>.visually-hidden</code> has one line of CSS missing which is <code>white-space: nowrap;</code>. The white-space property forces the content to <a href="https://medium.com/@jessebeach/beware-smushed-off-screen-accessible-text-5952a4c2cbfe#.aagksd6j2">render on one line</a>. Thefore, the whole CSS for <code>.visually-hidden</code> should read:

<pre><code>.visually-hidden {
	position: absolute;
	width: 1px;
	height: 1px;
	overflow: hidden;
	clip: rect(1px, 1px, 1px, 1px);
	white-space: nowrap;
}</code></pre>

<p><strong>Page 148</strong></p>
<p>The <code>getFragmentId</code> has a typo. <code>I’d</code> should be <code>id</code>.</p>

<p>On the same page, in the query selector too, the <code>id</code> has become <code>I'd</code> and there is no opening square bracket while selecting the element.</p>

<p><strong>Page 174</strong>:</p> 

<pre><code class="language-css">menu.hidden = !expanded;</code></pre> 

<p>should be 

<pre><code class="language-css">menu.hidden = expanded;</code></pre> 

<p>Otherwise this would require two clicks to open the menu from its default closed state.</p>

<p><strong>Page 272</strong>: The code sample appears to be missing the top portion of the form:</p>

<pre><code class="language-markup">
        &lt;input type="text" id="username" name="username" placeholder="e.g. HotStuff666">
        &lt;label for="password">Choose a password&lt;/label>
        &lt;input type="password" id="password" name="password">
        &lt;button type="submit">Register&lt;/button>
    &lt;/fieldset>
</form></code></pre> 

should be

<pre><code class="language-markup">&lt;form id="register">
    &lt;fieldset>
        &lt;legend>Registration&lt;/legend>
        &lt;label for="email">Your email address&lt;/label>
        &lt;input type="text" id="email" name="email">
        &lt;label for="username">Choose a username&lt;/label>
        &lt;input type="text" id="username" name="username" placeholder="e.g. HotStuff666">
        &lt;label for="password">Choose a password&lt;/label>
        &lt;input type="password" id="password" name="password">
        &lt;button type="submit">Register&lt;/button>
    &lt;/fieldset>
&lt;/form>&lt;/li></code></pre>

**Page 276**:

 

<pre><code class="language-markup">&lt;label for="password">Choose a password&lt;label>
&lt;input type="text" id="password" name="password">
&lt;label>&lt;input type="checkbox" id="showPassword"> show password&lt;/label></code></pre> 

should be

 

<pre><code class="language-markup">&lt;label for="password">Choose a password&lt;/label>
&lt;input type="password" id="password" name="password">
&lt;label>&lt;input type="checkbox" id="showPassword"> show password&lt;/label></code></pre> 

Otherwise the password will be visible with the "show password" checkbox unchecked.

Please let us know in the comments if you have found any further errata. Thank you! :-)