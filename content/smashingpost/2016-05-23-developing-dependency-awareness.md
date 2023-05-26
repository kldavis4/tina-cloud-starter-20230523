---
title: Developing Dependency Awareness
slug: developing-dependency-awareness
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f5c99d4-993c-4437-8368-9aa6dd8d3545/john-houbolt-opt.jpg
date: 2016-05-23T16:06:23.000Z
author: aarongustafson
summary: >-
  Dependencies are everywhere. They’re unavoidable. They aren’t inherently bad, but if you don’t consider the possibility a given dependency might not be met, you run the risk of frustrating your users.
description: >-
  Dependencies are everywhere. They’re unavoidable. They aren’t inherently bad, but if you don’t consider the possibility a given dependency might not be met, you run the risk of frustrating your users.
categories:
  - Coding
  - CSS
  - JavaScript
  - jQuery
---
I’m sure you’ve heard the proverb, “A chain is only as strong as its weakest link,” probably many times. Its written origin dates back to the 18th century, but I wouldn’t be surprised if it was much, much older. And though the work we do has little to do with actual chains, this proverb is every bit as relevant to us.

Remember <a href="https://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/">when Azer Koçulu unpublished more than 250 of his modules from npm</a> (Node Package Manager)? If that name doesn’t ring a bell, perhaps this function name will: <code>left-pad</code>. In case you’re still scratching your head wondering what the heck I’m talking about, Azer removed a bunch of functions from the canonical library of reusable Node.js code and, in doing so, brought thousands of projects to their knees, including high-profile ones like Babel and React. You see, each of these larger libraries included his <code>left-pad</code> module as a dependency. When that dependency was no longer available, building and deploying these projects became impossible.

And <code>left-pad</code> was only eleven lines of JavaScript that added padding to the left side of a string. Dependencies are a huge cause for concern.

But perhaps you’re not a Node.js user. If that’s the case, do you like jQuery? How about CDNs? The jQuery CDN? Well, here’s a little story about that.

Late on the night of January 25, 2014 the parental filter used by Sky Broadband – one of the UK’s largest internet service providers (ISPs) – began classifying <a href="https://code.jquery.com">code.jquery.com</a> as a “malware and phishing” website. The jQuery CDN is at that URL. No big deal – jQuery is only the JavaScript library that nearly three-quarters of the world’s top 10,000 websites rely on to make their web pages work.

With that domain so sadly mischaracterized, Sky’s firewall leapt into action and began protecting their customers from this malicious code. All of a sudden, huge swaths of the web abruptly stopped working for each and every Sky Broadband customer who had not explicitly opted out of this protection. To put it another way: any site that relied on a version of jQuery hosted by the jQuery CDN to load content or enable users to do things was dead on arrival.

In this particular instance, the weak link wasn’t jQuery <i>per se</i>; it was the CDN. You see, as a dependency, jQuery existed externally from the HTML documents and required a separate request (assuming it wasn’t already in the cache). Any such request was being denied by Sky’s firewall, so the file was never delivered. The dependency was not met and brought numerous sites to their knees.

<strong>Networks are fickle beasts</strong> and firewalls aren’t the only things that can cause a request to be denied or go unanswered. Mobile networks, for example, rely on transmission through the air via various wavelengths. Depending on the topography of the region, surrounding buildings, the materials they are made of, and even other networks, your user might venture into (or even reside within) a dead zone where mobile coverage is spotty or non-existent. Or there’s the oft-referenced tunnel scenario, which can cause a mobile connection to be dropped.

Similarly, slow networks can often give the impression of lost connectivity. Mobile networks often suffer from high latency, meaning requests and responses can be delayed. Hotel Wi-Fi and other public hotspots are also often crippled by transfer speed caps or high usage. On numerous occasions, I’ve waited <em>several minutes</em> for a page to load. Sometimes that page is even the “Join this network” splash screen.

To combat the issues brought about by high-latency networks, it became a best practice to <strong>embed your CSS and JavaScript in pages</strong> aimed at mobile devices. While this approach increased the size of the HTML files being delivered, it mitigated the risk of the network causing your site to break by minimizing external dependencies. Interestingly, this practice has come back in vogue, with many folks recommending we <a href="https://www.filamentgroup.com/lab/performance-rwd.html">embed critical CSS and JavaScript to reduce rendering times</a> and <a href="https://css-tricks.com/data-uris/">embedding graphics using data URIs</a>.

Reducing dependencies improves the likelihood that your site will be usable by the greatest number of people in the widest variety of scenarios. Even knowing this, however, it’s easy to overlook the most basic dependencies our projects have, undermining their resilience in the process. To illustrate this point, consider the humble submit button.

{{% feature-panel %}}

## Not All Buttons Are Created Equal

There are several ways you could mark up a submit button. The simplest uses the <code>input</code> element:

<pre><code class="language-markup">&lt;input type="submit" value="Sign Up"&gt;</code></pre>

Another option is the <code>button</code> element:

<pre><code class="language-markup">&lt;button type="submit"&gt;Sign Up&lt;/button&gt;
</code></pre>

I prefer <code>button[type=submit]</code> over <code>input[type=submit]</code> because the button’s text can be enhanced with other semantic elements like <code>em</code> and <code>strong</code>, but that’s a subject for another day.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2987a6c-760f-4d6b-b0f0-38a8e2081f63/01-button-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/139490e0-3528-4fc4-b149-0d8bc027a63e/submit-this-form-button-250px-opt.png" alt="A seemingly simple HTML button" width="250" height="58" /></a><figcaption>A seemingly simple HTML button. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2987a6c-760f-4d6b-b0f0-38a8e2081f63/01-button-opt.png">View large version</a>)</figcaption></figure>

Another option we often see on the web uses an anchor (<code>a</code>):

<pre><code class="language-markup">&lt;a href="#"&gt;Sign Up&lt;/a&gt;
</code></pre>

Like <code>button</code> above, the <code>a</code> element can contain other markup, which is handy.

For the purposes of this discussion, the final markup pattern I’m going to talk about uses a division element (<code>div</code>):

<pre><code class="language-markup">&lt;div&gt;Sign Up&lt;/div&gt;
</code></pre>

This is a markup pattern that was popularized by Gmail and has become pretty common in the single-page apps space.

If we subscribe to common wisdom, these are all valid options for coding buttons. They <em>can</em> be, but how they get there is far more complicated. Let’s dissect each and see where we end up.

### I Value Your `input`

An <code>input[type=submit]</code> is about as simple as you can get. Visually, it looks like a button, even in a text-based browser. Assistive technology sees this element as a button. It’s capable of receiving focus and it can be activated via the mouse, touch, and the keyboard (using either the space bar or <kbd>Enter</kbd> key). And finally, and most importantly, using this markup creates a button capable of submitting whatever form contains it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f32826-df8b-437b-b032-d3e80546aa8d/02-text-browser-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20bcbc4a-e40b-446e-9621-e921a0f2ce8a/02-text-browser-opt-preview.png" alt="A submit button rendered as text in the Lynx browser. When the cursor is on the button, text informs you it can be used to submit the form using the &lt;code&gt;&lt;kbd&gt;&lt;/code&gt;Enter key." width="500" height="67" /></a><figcaption>A submit button rendered as text in the Lynx browser. When the cursor is on the button, text informs you it can be used to submit the form using the <kbd>Enter</kbd> key. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f32826-df8b-437b-b032-d3e80546aa8d/02-text-browser-opt.png">View large version</a>)</figcaption></figure>

You get all of this functionality for free. The <code>input[type=submit]</code> has no dependencies apart from a browser supporting HTML forms, which they all do (forms were introduced in HTML 2.0).

### Cute As a `button`

A <code>button[type=submit]</code> has exactly the same feature-set with the same number of dependencies: zero, zilch, nada. Sure, you can spice up the design with a little CSS or hijack the form submission to post the form asynchronously with JavaScript, but those are enhancements to the basic design and functionality you get out of the box with these elements.

{{% ad-panel-leaderboard %}}

### Anchors Away!

The <code>a</code> element is a different story altogether. First off, by default, an <code>a</code> is rendered as inline text with an underline; you will need to involve CSS to make it look like a button. That’s dependency #1. By default, assistive technology will see this <code>a</code> as a generic element because it’s an anchor link to nowhere; you will need to use <a href="https://www.w3.org/TR/wai-aria/roles#button">the <code>role</code> attribute</a> to expose it as a button. That’s dependency #2.

<pre><code class="language-markup">&lt;a href="#" role="button"&gt;Sign Up&lt;/a&gt;
</code></pre>

Like a true button, an <code>a</code> is inherently capable of receiving focus, so you’re good there. One issue, however, is that <code>a</code> elements can only be activated via the <kbd>Enter</kbd> key, whereas true buttons can also be activated by the space bar; you’ll need to use JavaScript to listen for a space bar keypress. That’s dependency #3. Finally, an <code>a</code> can’t submit a form, which means you’ll need to involve JavaScript for that as well. That brings the total number of dependencies for this pattern to four, involving additional markup, CSS, and JavaScript.

### The Vanilla Box

The final pattern I mentioned used a <code>div</code>, but could just as easily be a <code>span</code> or some other element with no (or few) browser default styles applied to it. This markup pattern has all of the dependencies of the <code>a</code> tag, and it brings a few of its own. On the CSS end of things, you’ll probably want to render it as an <code>inline-block</code> element and you’ll definitely need to give it a <code>cursor</code> pointer to make it appear interactive for sighted users (although it won’t actually be until JavaScript kicks in).

Unlike the <code>a</code> element, a <code>div</code> (or <code>span</code>, etc.) is not focusable. To add it to the default tab order of the page, you’d need to assign it a <code>tabindex</code> of <code>0</code>:

<pre><code class="language-markup">&lt;div role="button" tabindex="0"&gt;Sign Up&lt;/div&gt;
</code></pre>

While not a dependency in the same sense that CSS, JavaScript, and ARIA are (which we’ll get to in a moment), this additional markup is a dependency in the development process because you need to remember to add it. Failing to do so makes the <code>div</code> completely inaccessible to keyboard users.

## Button Dependencies At A Glance

Since that was a substantial amount of information to follow, here’s a quick overview of the default state of affairs.

<figure class="break-out">
<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist" style="width: 200px;">Pattern</th>
<th>Display</th>
<th>Semantics</th>
<th>Focusable?</th>
<th>Activate By</th>
<th>Submits Forms</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>input<br />[type=submit]</code></td>
<td>Button</td>
<td>Button</td>
<td>Yes</td>
<td>Mouse, touch, <kbd>Enter</kbd> key, spacebar</td>
</ul>
</td>
<td>Yes</td>
</tr>
<tr>
<td><code>button<br />[type=submit]</code></td>
<td>Button</td>
<td>Button</td>
<td>Yes</td>
<td>
Mouse, touch, <kbd>Enter</kbd> key, spacebar
</td>
<td>Yes</td>
</tr>
<tr>
<td><code>a</code></td>
<td>Link</td>
<td>Named Generic</td>
<td>Yes</td>
<td>Mouse, touch, <kbd>Enter</kbd> key
</td>
<td>No</td>
</tr>
<tr>
<td><code>div</code></td>
<td>Block</td>
<td>Not exposed</td>
<td>No</td>
<td>Nothing</td>
<td>No</td>
</tr>
</tbody>
</table>
<figcaption>Button coding patterns and their default capabilities</figcaption>
</figure>

Now let’s look at the same patterns through the lens of dependencies required to achieve button-ness.

<figure class="break-out">
<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Pattern</th>
<th>Display</th>
<th>Semantics</th>
<th>Focus</th>
<th>Activation</th>
<th>Form Submission</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>input<br />[type=submit]</code></td>
<td>None</td>
<td>None</td>
<td>None</td>
<td>None</td>
<td>None</td>
</tr>
<tr>
<td><code>button<br />[type=submit]</code></td>
<td>None</td>
<td>None</td>
<td>None</td>
<td>None</td>
<td>None</td>
</tr>
<tr>
<td><code>a</code></td>
<td>CSS</td>
<td>ARIA</td>
<td>None</td>
<td>JavaScript</td>
<td>JavaScript</td>
</tr>
<tr>
<td><code>div</code></td>
<td>CSS</td>
<td>ARIA</td>
<td>HTML</td>
<td>JavaScript</td>
<td>JavaScript</td>
</tr>
</tbody>
</table>
<figcaption>Button coding patterns and required dependencies</figcaption>
</figure>

While it may appear on the surface that these approaches are similar, by using either of the latter two patterns (<code>a</code> and <code>div</code>), we are greatly increasing the number of dependencies our button requires to do its one and only job: enable users to submit a form.

Some of you may be wondering why this is such a big deal. After all, everyone has CSS and JavaScript at least, right? Well, no. Not necessarily. You could probably argue that most users today have access to a browser that has some amount of CSS and JavaScript support, but that is by no means a thumbs up to depend on it being there when you need it.

Here are a few things that can cause your CSS dependency to remain unmet:

*   The browser doesn’t support CSS.
*   The user disabled CSS for performance reasons.
*   The user is applying a user style sheet (which trumps your rules) to improve accessibility or for some other personal preference.
*   A networking issue caused the external CSS to be unavailable.
*   The selector you are using is too advanced for the browser.
*   The rules are contained in a media query and the browser doesn’t support them or the query doesn’t apply.

On the JavaScript side of things, there are some similar potential blockers and some other things to consider:

*   The browser doesn’t support JavaScript.
*   JavaScript was disabled by the user.
*   A networking issue caused the JavaScript to be unavailable.
*   A firewall blocked requests for JavaScript.
*   A browser plugin blocked the JavaScript download or execution.
*   A third-party JavaScript error caused the JavaScript program to stop.
*   A bug in your code caused the JavaScript program to stop.
*   The browser failed a feature detection test and exited the program early.
*   The user is still waiting for the browser to download, parse, and execute your JavaScript program.

Even ARIA is not without pitfalls. If the browser and assistive technology are not in sync in terms of their level of support, weird things can happen. Another potential issue is if the ARIA <code>role</code> is understood and applied, but the JavaScript is not available to make the <code>a</code> or <code>div</code> function like a true button, your users will be pretty frustrated when it seems like they should be able to use a button and they can’t.

<em>Note: I’ve put together <a href="https://s.codepen.io/aarongustafson/debug/qZQzmO">a demo of these different markup patterns</a> that enables you to view them in a few different scenarios. Feel free to have a play.</em>

{{% ad-panel-leaderboard %}}

## Hope For The Best, Plan For The Worst

We don’t control where our web-based products go or how our users access them. All we can do is imagine as many less-than-perfect scenarios as possible and do our best to ensure our creations will continue to do what they’re supposed to do. One of the easiest ways to do that is to be aware of and limit our dependencies.

Do you only have a few enhancements you want to add to your site using JavaScript? Don’t bother with a JavaScript library. <a href="https://vanilla-js.com/">Vanilla JavaScript is often the best choice.</a> If it’s code that only pertains to a single page, consider embedding it before the closing <code>body</code> tag.

Do you have a hard dependency on jQuery or some other JavaScript library? Go ahead and use a public CDN to include it – since that will give you a performance boost – but fall back to a local copy if that one’s not available. The <a href="https://html5boilerplate.com/">HTML5 Boilerplate</a> does this quite elegantly:

<div class="break-out">

 <pre><code class="language-markup">&lt;script src="https://code.jquery.com/jquery-{{JQUERY_VERSION}}.min.js"&gt;&lt;/script&gt;
&lt;script&gt;window.jQuery || document.write('&lt;script src="js/vendor/jquery-{{JQUERY_VERSION}}.min.js"&gt;&lt;\/script&gt;')&lt;/script&gt;
</code></pre>
</div>

In this simple code example, the first <code>script</code> element requests whichever jQuery version you require from the jQuery CDN. The second <code>script</code> element – which executes after the first one is evaluated – checks to make sure jQuery is available. If it isn’t, then another <code>script</code> element is inserted into the document, referencing a local copy on the server.

Of course, it’s possible that the browser might fail to retrieve both copies of jQuery, so any plugins or jQuery-dependent code you write should also test for the jQuery object before attempting to do anything:

<pre><code class="language-javascript">(function(window){
  // Do we have jQuery?
  if(! 'jQuery' in window){ return; }
  // Phew! It’s safe to use jQuery now.
}(this));
</code></pre>

And, of course, you should always assume there’s going to be a scenario where a user doesn’t get your JavaScript enhancements at all, whether jQuery-based or otherwise. Have a fallback that uses HTML and the server. It may seem old-school, but it will ensure your users can sign up for your service, buy your products, or post photos of their kittens, no matter what.

<strong>Dependencies are everywhere</strong>. They’re unavoidable. They aren’t inherently bad, but if you don’t consider the possibility a given dependency might not be met, you run the risk of frustrating your users. You might even drive them into the arms of your competition. So be aware of dependencies. Address them proactively. And do everything you can to build a baseline experience with no dependencies at all and then use them to enhance the experience as they are met.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Better Dependency Management In Team-Based WordPress Projects](https://www.smashingmagazine.com/2014/03/better-dependency-management-team-based-wordpress-projects-composer/)
*   [Webpack: A Detailed Introduction](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [How To Harness The Machines: Being Productive With Task Runners](https://www.smashingmagazine.com/2016/06/harness-machines-productive-task-runners/)

{{< signature "rb, ml, og, il" >}}
