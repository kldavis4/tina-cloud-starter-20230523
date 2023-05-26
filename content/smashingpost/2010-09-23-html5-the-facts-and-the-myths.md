---
title: 'HTML5: The Facts And The Myths'
slug: html5-the-facts-and-the-myths
image: null
date: 2010-09-23T12:30:38.000Z
author: bruce-lawson
description: >-
  You can't escape it. Everyone's talking about HTML5\. it's perhaps the most
  hyped technology since people started putting rounded corners on everything
  and using unnecessary gradients. In fact, a lot of what people call HTML5 is
  actually just old-fashioned DHTML or AJAX. Mixed in with all the information
  is a lot of misinformation, so here, JavaScript expert Remy Sharp and Opera's
  Bruce Lawson look at some of the myths and sort the truth from the common
  misconceptions.

  Once upon a time, there was a lovely language called **HTML**, which was so
  simple that writing websites with it was very easy. So, everyone did, and the
  Web transformed from a linked collection of physics papers to what we know and
  love today. Most pages didn't conform to the simple rules of the language
  (because their authors were rightly concerned more with the message than the
  medium), so every browser had to be forgiving with bad code and do its best to
  work out what its author wanted to display.
categories:
  - Coding
  - HTML5
  - HTML
---
You can't escape it. Everyone's talking about HTML5. it's perhaps the most hyped technology since people started putting rounded corners on everything and using unnecessary gradients. In fact, a lot of what people call HTML5 is actually just old-fashioned DHTML or AJAX. Mixed in with all the information is a lot of misinformation, so here, JavaScript expert Remy Sharp and Opera's Bruce Lawson look at some of the myths and sort the truth from the common misconceptions.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/html5-and-the-future-of-the-web/)
*   [Road Map To Coding With HTML5: Tutorials and Guidelines](https://www.smashingmagazine.com/coding-with-html5-tutorials-guidelines/)

## First, Some Facts

Once upon a time, there was a lovely language called HTML, which was so simple that writing websites with it was very easy. So, everyone did, and the Web transformed from a linked collection of physics papers to what we know and love today.

{{% feature-panel %}}

Most pages didn't conform to the simple rules of the language (because their authors were rightly concerned more with the message than the medium), so every browser had to be forgiving with bad code and do its best to work out what its author wanted to display.

In 1999, the W3C decided to discontinue work on HTML and move the world toward XHTML. This was all good, until a few people noticed that the work to upgrade the language to XHTML2 had very little to do with the real Web. Being XML, the spec required a browser to stop rendering if it encountered an error. And because the W3C was writing a new language that was better than simple old HTML, it deprecated elements such as <code>&lt;img&gt;</code> and <code>&lt;a&gt;</code>.

A group of developers at Opera and Mozilla disagreed with this approach and presented a <a href="https://www.w3.org/2004/04/webapps-cdf-ws/papers/opera.html">paper to the W3C in 2004</a> arguing that, "We consider Web Applications to be an important area that has not been adequately served by existing technologies… There is a rising threat of single-vendor solutions addressing this problem before jointly-developed specifications."

The paper suggested seven design principles:

1.  Backwards compatibility, and a clear migration path.
2.  Well-defined error handling, like CSS (i.e. ignore unknown stuff and move on), compared to XML's "draconian" error handling.
3.  Users should not be exposed to authoring errors.
4.  Practical use: every feature that goes into the Web-applications specifications must be justified by a practical use case. The reverse is not necessarily true: every use case does not necessarily warrant a new feature.
5.  Scripting is here to stay (but should be avoided where more convenient declarative mark-up can be used).
6.  Avoid device-specific profiling.
7.  Make the process open. (The Web has benefited from being developed in the open. Mailing lists, archives and draft specifications should continuously be visible to the public.)

The paper was rejected by the W3C, and so Opera and Mozilla, later joined by Apple, continued a mailing list called Web Hypertext Application Technology Working Group (WHATWG), working on their proof-of-concept specification. The spec <a href="https://www.hixie.ch/specs/html/forms/web-forms">extended HTML4 forms</a>, until it grew into a spec called Web Applications 1.0, under the continued editorship of Ian Hickson, who left Opera for Google.

In 2006, the W3C realized its mistake and decided to resurrect HTML, asking WHATWG for its spec to use as the basis of what is now called HTML5.

Those are the historical facts. Now, let's look at some hysterical myths.</p>

## The Myths

### “I Can't Use HTML5 Until 2012 (or 2022)”

This is a misconception based on the projected date that HTML5 will reach the stage in the W3C process known as Candidate Recommendation (REC). The <a href="https://wiki.whatwg.org/wiki/FAQ#When_will_we_be_able_to_start_using_these_new_features.3F">WHATWG wiki</a> says this:
<blockquote>For a spec to become a REC today, it requires two 100% complete and fully interoperable implementations, which is proven by each successfully passing literally thousands of test cases (20,000 tests for the whole spec would probably be a conservative estimate). When you consider how long it takes to write that many test cases and how long it takes to implement each feature, you’ll begin to understand why the time frame seems so long.</blockquote>

So, by definition, the spec won't be finished until you can use <em>all of it</em>, and in two browsers.

Of course, what really matters is the bits of HTML5 that are already supported in the browsers. Any list will be out of date within about a week because the browser makers are innovating so quickly. Also, much of the new functionality can be replicated with JavaScript in browsers that don't yet have support. The <code>&lt;canvas&gt;</code> property is in all modern browsers and will be in Internet Explorer 9, but it can be faked in old versions of IE with the <a href="https://excanvas.sourceforge.net/">excanvas library</a>. The <code>&lt;video&gt;</code> and &lt;<code>audio&gt;</code> properties can be faked with Flash in old browsers.

HTML5 is designed to degrade gracefully, so with clever JavaScript and some thought, all content should be available on older browsers.</p>

### “My Browser Supports HTML5, but Yours Doesn't”

There's a myth that HTML5 is some monolithic, indivisible thing. It's not. It's a collection of features, as we've seen above. So, in the short term, you cannot say that a browser supports everything in the spec. And when some browser or other does, it won't matter because we'll all be much too excited about the next iteration of HTML by then.

What a terrible mess, you're thinking? But consider that CSS 2.1 is not yet a finished spec, and yet we all use it each and every day. We use CSS3, happily adding <code>border-radius</code>, which will soon be supported everywhere, while other aspects of CSS3 aren't supported anywhere at all.

Be wary of browser "scoring" websites. They often test for things that have nothing to do with HTML5, such as CSS, SVG and even Web fonts. What matters is what you need to do, what's supported by the browsers your client's audience will be using and how much you can fake with JavaScript.</p>

### HTML5 Legalizes Tag Soup

HTML5 is a lot more forgiving in its syntax than XHTML: you can write tags in uppercase, lowercase or a mixture of the two. You don't need to self-close tags such as <code>img</code>, so the following are both legal:

<pre><code class="language-markup tmp-xml">&lt;img src="nice.jpg" /&gt;
&lt;img src="nice.jpg"&gt;</code></pre>

You don't need to wrap attributes in quotation marks, so the following are both legal:

<pre><code class="language-markup tmp-xml">&lt;img src="nice.jpg"&gt;
&lt;img src=nice.jpg&gt;</code></pre>

You can use uppercase or lowercase (or mix them), so all of these are legal:

<pre><code class="language-markup tmp-xml">&lt;IMG SRC=nice.jpg&gt;
&lt;img src=nice.jpg&gt;
&lt;iMg SrC=nice.jpg&gt;</code></pre>

This isn't any different from HTML4, but it probably comes as quite a shock if you're used to XHTML. In reality, if you were serving your pages as a combination of text and HTML, rather than XML (and you probably were, because Internet Explorer 8 and below couldn't render true XHTML), then it never mattered anyway: the browser never cared about trailing slashes, quoted attributes or case—only the validator did.

So, while the syntax appears to be looser, the actual parsing rules are much tighter. The difference is that there is no more <a href="https://en.wikipedia.org/wiki/Tag_soup">tag soup</a>; the specification describes exactly what to do with invalid mark-up so that all conforming browsers produce the same DOM. If you've ever written JavaScript that has to walk the DOM, then you're aware of the horrors that inconsistent DOMs can bring.

This error correction is no reason to churn out invalid code, though. The DOM that HTML5 creates for you might not be the DOM you want, so ensuring that your HTML5 validates is still essential. With all this new stuff, overlooking a small syntax error that stops your script from working or that makes your CSS unstylish is easy, which is why we have <a href="https://html5.validator.nu/">HTML5 validators</a>.

Far from legitimizing tag soup, HTML5 consigns it to history. Souper.</p>

### “I Need to Convert My XHTML Website to HTML5”

Is HTML5's tolerance of looser syntax the death knell for XHTML? After all, the working group to develop XHTML 2 was disbanded, right?

True, the XHTML 2 group was disbanded at the end of 2009; it was working on an unimplemented spec that competed with HTML5, so having two groups was a waste of W3C resources. But XHTML 1 was a finished spec that is widely supported in all browsers and that will continue to work in browsers for as long as needed. Your XHTML websites are therefore safe.</p>

### HTML5 Kills XML

Not at all. If you need to use XML rather than HTML, you can use <a href="https://mathiasbynens.be/notes/xhtml5">XHTML5</a>, which includes all the wonders of HTML5 but which must be in well-formed XHTML syntax (i.e. quoted attributes, trailing slashes to close some elements, lowercase elements and the like.)

Actually, you can't use <em>all</em> the wonders of HTML5 in XHTML5: <code>&lt;noscript&gt;</code> won't work. But <a href="https://www.wait-till-i.com/2005/06/21/six-javascript-features-we-do-not-need-any-longer/">you're not still using that</a>, are you?

### HTML5 Will Kill Flash and Plug-Ins

The <code>&lt;canvas&gt;</code> tag allows scripted images and animations that react to the keyboard and that therefore can compete with some simpler uses of Adobe Flash. HTML5 has native capability for playing video and audio.

Just as when CSS Web fonts weren't widely supported and Flash was used in <a href="https://www.mikeindustries.com/blog/sifr">sIFR</a> to fill the gaps, Flash also saves the day by making HTML5 video backwards-compatible. Because HTML5 is designed to be "fake-able" in older browsers, the mark-up between the video tags is ignored by browsers that understand HTML5 and is rendered by older browsers. Therefore, embedding fall-back video with Flash is possible using the old-school <code>&lt;object&gt;</code> or <code>&lt;embed&gt;</code> tags, as pioneered by Kroc Camen is his article “<a href="https://camendesign.com/code/video_for_everybody">Video for Everybody!”</a> (see the screenshot below).

<a href="https://camendesign.com/code/video_for_everybody"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1688db4a-6be5-4d41-8e93-d4985cd2a56a/ipad.jpg" alt="Screenshot" width="500" height="388" /></a>

But not all of Flash's use cases are usurped by HTML5. There is no way to do digital rights management in HTML5; browsers such as Opera, Firefox and Chrome allow visitors to save video to their machines with a click of the context menu. If you need to prevent video from being saved, you'll need to use plug-ins. Capturing input from a user's microphone or camera is currently only possible with Flash (although a <code>&lt;device&gt;</code> element is being specified for "post-5" HTML), so if you're keen to write a Chatroulette killer, HTML5 isn't for you.</p>

### HTML5 Is Bad for Accessibility

A lot of discussion is going on about the accessibility of HTML5. This is good and to be welcomed: with so many changes to the basic language of the Web, ensuring that the Web is accessible to people who cannot see or use a mouse is vital. Also vital is building in the solution, rather than bolting it on as an afterthought: after all, many (most?) authors don't even add alternate text to images, so out-of-the-box accessibility is much more likely to succeed than relying on people to add it.

This is why it's great that HTML5 adds native controls for things like sliders (<code>&lt;input type=range&gt;</code>, currently supported in Opera and Webkit browsers) and date pickers (<code>&lt;input type=date&gt;</code>, Opera only)—see Bruce's <a href="https://people.opera.com/brucel/demo/html5-forms-demo.html">HTML5 forms demo</a>)—because previously we had to fake these with JavaScript and images and then add keyboard support and <a href="https://dev.opera.com/articles/view/introduction-to-wai-aria/">WAI-ARIA roles and attributes</a>.

The <code>&lt;canvas&gt;</code> tag is a different story. It is an Apple invention that was reverse-engineered by other browser makers and then retrospectively specified as part of HTML5, so there is no built-in accessibility. If you're just using it for eye-candy, that's fine; think of it as an image, but without any possibility of alternate text (some additions to the spec have been suggested, but nothing is implemented yet). So, ensure that any information you deliver via <code>&lt;canvas&gt;</code> supplements more accessible information elsewhere.

Text in a <code>&lt;canvas&gt;</code> becomes simply pixels, just like text in images, and so is invisible to assistive technology and screen readers. Consider using the W3C graphics technology <a href="https://en.wikipedia.org/wiki/Scalable_Vector_Graphics">Scalable Vector Graphics</a> (SVG) instead, especially for things such as dynamic graphs and animating text. SVG is supported in all the major browsers, including IE9 (but not IE8 or below, although the <a href="https://code.google.com/p/svgweb/">SVGweb</a> library can fake SVG with Flash in older browsers).

The situation with <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> is promising. Although not fully specified (and so not yet implemented in any browsers), a new <code>&lt;track&gt;</code> element has been included in the HTML5 spec that allows timed transcripts (or karaoke lyrics or captions for the deaf or subtitles for foreign-language media) to be associated with multimedia. It <span class="removed_link" title="https://people.opera.com/philipj/2010/07/21/html5-video-webinar/demos/track.html">can be faked in JavaScript</span>. Alternatively (and better for search engines), you could include transcripts directly on the page below the video and use <a href="https://people.opera.com/brucel/demo/video/multilingual-synergy.html">JavaScript to overlay captions</a>, synchronized with the video.</p>

### “An HTML5 Guru Will Hold My Hand as I Do It the First Time”

If only this were true. However, the charming Paul Irish and lovely Divya Manian will be as good as there for you, with their <a href="https://html5boilerplate.com/">HTML5 Boilerplate</a>, which is a set of files you can use as templates for your projects. Boilerplate brings in the JavaScript you need to style the new elements in IE; pulls in jQuery from the Google Content Distribution Network (CDN), but with fall-back links to your server in case the CDN server is down.

<a href="https://html5boilerplate.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a884e66c-6798-4e22-9282-17c63b842efd/html5-boiler.jpg" alt="HTML5 Boiler Plate" width="500" height="321" /></a>

It adds mark-up that is adaptable to iOS, Android and Opera Mobile; and adds a CSS skeleton with a comprehensive reset style sheet. There's even an <em>.htaccess</em> file that serves your HTML5 video with the right MIME types. You won't need all of it, and you're encouraged to delete the stuff that's unnecessary to your project to avoid bloat.</p>

## Further Resources

HTML5 is a massive topic. Here are a few hand-picked links. Disclosure: the authors have their fingers in some of these pies.

*   [W3C Specification: HTML5 (Edition for Web Authors)](https://dev.w3.org/html5/spec-author-view/) Just the stuff for those who write websites (as opposed to those who write browsers).
*   HTML5 Demos and Examples Demos of the HTML5 APIs that are implemented in browsers.
*   [HTML5 Doctor](https://www.html5doctor.com) Short, focused articles, "helping you implement HTML5 today."
*   [html5-shims](https://code.google.com/p/html5-shims/wiki/LinksandResources) Scripts that fake HTML5 functionality in older browsers.</p>

### About the Authors

Remy and Bruce are two developers who have been playing with HTML5 since Christmas 2008: experimenting, participating in the mailing list and generally trying to help shape the language as well as learn it.

<img loading="lazy" decoding="async"  style="float: left;padding: 0 15px 12px 0" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a4f0010-30be-48a2-bbf5-9f9b5f666e2f/book-m.jpg" alt="Screenshot" width="240" height="160" />

<a href="https://twitter.com/brucel">Bruce</a> evangelizes Open Web Standards for <a href="https://www.opera.com/developer">Opera</a>. <a href="https://twitter.com/rem">Remy</a> is a developer, speaker, blogger and contributing author for jQuery Cookbook (O'Reilly). He runs his own Brighton-based development company called Left Logic, coding and writing about JavaScript, jQuery, HTML5, CSS, PHP, Perl and anything else he can get his hands on. Together, they are the authors of Introducing HTML5, the first full-length book on HTML5 (New Riders, July 2010).

{{< signature "al" >}}

