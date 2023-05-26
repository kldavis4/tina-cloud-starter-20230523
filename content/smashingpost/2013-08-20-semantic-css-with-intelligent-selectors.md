---
title: Semantic CSS With Intelligent Selectors
slug: semantic-css-with-intelligent-selectors
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4476bd03-4bbc-4457-9e9a-96425187be31/illu-selectors.jpg'
date: 2013-08-20T08:40:52.000Z
author: heydon-pickering
description: >-
  “Form ever follows function. This is the law.” So said the architect and
  “father of skyscrapers” Louis Sullivan. For architects not wishing to crush
  hundreds of innocent people under the weight of a colossal building, this rule
  of thumb is pretty good.
categories:
  - Coding
  - CSS
  - HTML
  - Semantics
---
“Form ever follows function. This is the law.” So said the architect and “father of skyscrapers” <a href="https://en.wikipedia.org/wiki/Louis_Sullivan">Louis Sullivan</a>. For architects not wishing to crush hundreds of innocent people under the weight of a colossal building, this rule of thumb is pretty good. In design, you should <strong>always lead with function</strong>, and allow form to emerge as a result. If you were to lead with form, making your skyscraper look pretty would be easier, but at the cost of producing something pretty dangerous.

So much for architects. What about front-end architects — or “not real architects,” as we are sometimes known? Do we abide by this law or do we flout it?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [CSS Specificity And Inheritance](https://www.smashingmagazine.com/2010/04/css-specificity-and-inheritance/)
*   [Sneak Peek Into The Future: CSS Selectors, Level 4](https://www.smashingmagazine.com/2013/01/sneak-peek-future-selectors-level-4/)
*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)

With the advent of <a href="https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/">object-oriented CSS</a> (OOCSS), it has become increasingly fashionable to “<a href="https://nicolasgallagher.com/about-html-semantics-front-end-architecture/">decouple presentation semantics from document semantics</a>.” By leveraging the undesignated meanings of <a href="https://www.w3.org/TR/CSS2/selector.html#class-html">classes</a>, it is possible to manage one’s document and the <em>appearance</em> of one’s document as curiously separate concerns.

{{% feature-panel %}}

<img loading="lazy" decoding="async" class="127260" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68c14009-2635-4b9b-bfb6-4660fcee5e95/art-overthink1-mini.png" alt="Overthinking how a functional thing should look." width="499" height="226" />

In this article, <strong>we will explore an alternative approach to styling Web documents</strong>, one that marries document semantics to visual design wherever possible. With the use of “intelligent” selectors, we’ll cover how to query the extant, functional nature of semantic HTML in such a way as to reward well-formed markup. If you code it right, you’ll get the design you were hoping for.

If you are like me and have trouble doing or thinking about more than one thing at a time, I hope that employing some of these ideas will make your workflow simpler and more transferable between projects. In addition, the final section will cover a more reactive strategy: We’ll make a CSS bookmarklet that contains intelligent <strong>attribute selectors</strong> to test for bad HTML and report errors using pseudo-content.</p>

## Intelligent Selectors

With the invention of style sheets came the possibility of physically separating document code from the code used to make the document presentable. This didn’t help us to write better, more standards-aware HTML any more than the advent of the remote control resulted in better television programming. It just made things more convenient. By being able to style multiple elements with a single selector (<code>p</code> for paragraphs, for instance), consistency and maintenance became significantly less daunting prospects.

<img loading="lazy" decoding="async" class="127051" style="height: auto;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/712bd26a-1cf9-4ce1-b212-10b5d1f7ac4f/art-remote-mini.png" alt="television remote reading DRIVEL" />

The <code>p</code> selector is an example of an intelligent selector in its simplest form. The <code>p</code> selector is intelligent because it has innate knowledge of semantic classification. Without intervention by the author, it already knows how to identify paragraphs and when to style them as such — simple yet effective, especially when you think of all of the automatically generated paragraphs produced by <abbr title="What You See Is (sort of) What You Get">WYSIWYG</abbr> editors.

So, if that’s an intelligent selector, what’s an unintelligent one? Any selector that requires the author to <strong>intervene and alter the document</strong> simply to elicit a stylistic nuance is an unintelligent selector. The <code>class</code> is a classic unintelligent selector because it is not naturally occurring as part of semantic convention. You can name and organize classes sensibly, but only with deliberation; they aren’t smart enough to take care of themselves, and browsers aren’t smart enough to take care of them for you.

Unintelligent selectors are time-intensive because they require styling hooks to be duplicated case by case. If we didn’t have <code>p</code> tags, we’d have to use unintelligent selectors to manufacture paragraphs, perhaps using <code>.paragraph</code> in each case. One of the downsides of this is that the CSS isn’t portable — that is, you can’t apply it to an HTML document without first going through the document and adding the classes everywhere they are required.

<img loading="lazy" decoding="async" class="127235" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/261518bb-6ed0-4e64-a0e2-f1ae8f242930/art-paragraph-500-mini.png" alt="class selector called paragraph" width="500" height="107" />

Unintelligent selectors at times seem necessary, or at least easier, and few of us are willing to rely entirely on intelligent selectors. However, some unintelligent selectors can become “plain stupid” selectors by creating a <strong>mismatch</strong> between document structure and presentation. I’ll be talking about the alarming frequency with which the unintelligent <code>.button</code> selector quickly becomes plain stupid.</p>

### Vive la Différence

Intelligent selectors are not confined just to the basic elements offered to us in HTML’s specification. To build complex intelligent selectors, you can defer to combinations of <strong>context and functional attribution</strong> to differentiate basic elements. Some elements, such as <code>&lt;a&gt;</code>, have a multitude of functional differences to consider and exploit. Other elements, such as <code>&lt;p&gt;</code>, rarely differ in explicit function but assume slightly different roles according to context.

<pre><code class="language-css">
header p {
   /* styles for prologic paragraphs */
}

footer p {
   /* styles for epilogic paragraphs */
}
</code></pre>

Simple descendent selectors like these are extremely powerful because they enable us to visually disclose different types of the same element without having to physically alter the underlying document. This is the whole reason why style sheets were invented: to facilitate physical separation without breaking the conceptual reciprocity that should exist between document and design.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1536a336-5ba8-4a92-a8bf-af3e89776da2/art-heirarchy-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e57fa0c-3066-491a-b635-ba7cf8b7ae13/art-heirarchy-500-mini.png" alt="a semantic heirarchy of needs: what it is, how it functions, where it is" width="500" height="485" /></a>

Inevitably, some adherents of OOCSS <a href="https://www.impressivewebs.com/when-to-avoid-descendant-selector/">treat the descendent selector with some suspicion</a>, with the more zealous insisting on markup such as the example below, found in BEM’s “<a href="https://bem.info/method/definitions/">Definitions</a>” documentation.

<pre><code class="language-markup">
&lt;ul class="menu"&gt;
  &lt;li class="menu__item"&gt;…&lt;/li&gt;
  &lt;li class="menu__item"&gt;…&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

I won’t cover contextual selectors any further because, unless you have a predilection for the kind of overprescription outlined above, I’m sure you already use them every day. Instead, we’ll concentrate on differentiation by function, as described in attributes and by <strong>attribute selectors</strong>.</p>

## Hyperlink Attributes

Even those who advocate for conceptual separation between CSS and HTML are happy to concede that some attributes — most attributes besides classes and custom data attributes, in fact — have an important bearing on the internal functioning of the document. Without <code>href</code>, your link won’t link to anything. Without <code>type</code>, the browser won’t know what sort of <code>input</code> to render. Without <code>title</code>, your <code>abbr</code> could be referring to either the British National Party or <em>Banco Nacional de Panama</em>.

Some of these attributes may improve the semantic detail of your document, while others are needed to ensure the correct rendering and functioning of their subject elements. If they’re not there, they should be, and if they are there, why not make use of them? You can’t write CSS without writing HTML.</p>

### The rel Attribute

The <code>rel</code> attribute emerged as a standard for <a href="https://blog.whatwg.org/the-road-to-html-5-link-relations#what">link relations</a>, a method of describing some specific purpose of a link. Not all links, you see, are functionally alike. Thanks to WordPress’ championing, <code>rel="prev"</code> and <code>rel="next"</code> are two of the most widely adopted values, helping to describe the relationship between individual pages of paginated blog content. Semantically, an <code>a</code> tag with a <code>rel</code> attribute is still an <code>a</code> tag, but we are able to be more specific. Unlike with classes, this specificity is semantically consequential.

The rel attribute should be used where appropriate because it is vindicated by HTML’s <a href="https://en.wikipedia.org/wiki/Functional_specification">functional specification</a> and can therefore be adopted by various user agents to enhance the experience of users and the accuracy of search engines. How, then, do you go about styling such links? With simple attribute selectors, of course:

<pre><code class="language-css">
[rel="prev"] {
  /* styling for "previous links" */
}

[rel="next"] {
  /* styling for "next" links */
}
</code></pre>

Attribute selectors like these are supported by all but the most archaic, <abbr title="IE6">clockwork browsers</abbr>, so that’s no reason not to use them anywhere the attributes exist. In terms of specificity, they have the same weight as classes. No woe there either, then. However, I recall it being suggested that we should decouple document and presentation semantics. I don’t want to lose the <code>rel</code> attributes (Google has <a href="https://googlewebmastercentral.blogspot.co.uk/2011/09/pagination-with-relnext-and-relprev.html">implemented them</a>, for one thing), so I’d better put <strong>an attribute that means nothing</strong> on there as well and style the element via that.

<pre><code class="language-markup">
  &lt;a href="/previous-article-snippet/" rel="prev" class="prev"&gt;previous page&lt;/a&gt;
</code></pre>

The first thing to note here is that the only part of the element above that does not contribute to the document’s semantics is the class. The class, in other words, is the only thing in the document that has nothing functionally to do with it. In practice, this means that the class is the only thing that <strong>breaks with the very law of separation that it was employed to honor</strong>: It has a physical presence in the document without contributing to the document’s structure.

OK, so much for abstraction, but what about maintenance? Accepting that we’ve used the <code>class</code> as our styling hook, let’s now examine what happens when some editing or refactoring has led us to remove some attributes. Suppose we’ve used some pseudo-content to place a left-pointing arrow before the <code>[rel="prev"]</code> link’s text:

<pre><code class="language-css">
.prev:before {
  content: '2190'; /* encoding for a left-pointing arrow ("←") */
}
</code></pre>

<img loading="lazy" decoding="async" class="127226" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf27a01-f26f-4b9f-967e-b1d41325d557/art-previous-500-mini.png" alt="previous link with arrow" width="500" height="76" />

Removing the class will remove the pseudo-content, which in turn will remove the arrow (obviously). But without the arrow, nothing remains to elucidate the link’s extant <code>prev</code> relationship. By the same token, removing the <code>rel</code> attribute will leave the arrow intact: The class will continue to manage presentation, all the time disguising the <strong>nonexistence of a stated relationship</strong> in the document. Only by applying the style directly, via the semantic attribute that elicits it, can you keep your code and yourself honest and accurate. Only if it’s really there, as a function of the document, should you see it.

## Attribute Substrings

I can imagine what you’re thinking: “That’s cute, but how many instances are there really for semantic styling hooks like these on hyperlinks? I’m going to have to rely on classes at some point.” I dispute that. Consider this incomplete list of functionally disimilar hyperlinks, all using the <code>a</code> element as their base:

*   links to external resources,
*   links to secure pages,
*   links to author pages,
*   links to help pages,
*   links to previous pages (see example above),
*   links to next pages (see example above again),
*   links to PDF resources,
*   links to documents,
*   links to ZIP folders,
*   links to executables,
*   links to internal page fragments,
*   links that are really buttons (more on these later),
*   links that are really buttons and are toggle-able,
*   links that open mail clients,
*   links that cue up telephone numbers on smartphones,
*   links to the source view of pages,
*   links that open new tabs and windows,
*   links to JavaScript and JSON files,
*   links to RSS feeds and XML files.

That’s a lot of functional diversity, all of which is understood by user agents of all sorts. Now consider that in order for all of these specific link types to function differently, they must have mutually differential attribution. That is, in order to function differently, they must be written differently; and if they’re written differently, <strong>they can be styled differently.</strong>

In preparing this article, I created a proof of concept, named <a href="https://heydonworks.com/auticons-icon-font/">Auticons</a>. Auticons is an <a href="https://sixrevisions.com/resources/free-icon-fonts/">icon font</a> and CSS set that styles links automatically. All of the selectors in the CSS file are attribute selectors that invoke styles on well-formed hyperlinks, <strong>without the intervention of classes</strong>.

<a href="https://www.heydonworks.com/auticons-icon-font"><img loading="lazy" decoding="async" class="127052" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82392cb7-962e-421f-9243-ad5c6cf3e3b0/art-auticons-mini.png" alt="art_auticons" width="500" height="195" /></a>

In many cases, Auticons queries a <em>subset</em> of the <code>href</code> value in order to determine the function of the hyperlink. Styling elements according to the way their attribute values begin or end or according to what substring they contain throughout the value is possible. Below are some common examples.</p>

### The Secure Protocol

Every well-formed (i.e. absolute) URL begins with a <a href="https://en.wikipedia.org/wiki/URI_scheme">URI scheme</a> followed by a colon. The most common on the Web is <code>http:</code>, but <code>mailto:</code> (for SMTP) and <code>tel:</code> (which refers to telephone numbers) are also prevalent. If we know how the <code>href</code> value of the hyperlink is expected to begin, we can exploit this semantic convention as a styling hook. In the following example for secure pages, we use the <code>^=</code> comparator, which means “begins with.”

<pre><code class="language-css">
a[href^="https:"] {
   /* style properties exclusive to secure pages */
}
</code></pre>

<img class="127058" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78120c55-0c37-4494-b8ad-3a6311b5cc02/art-secure-500-mini.png" alt="a link to a secure page with a lock icon" width="500" height="76" />

In Auticons, links to secure pages become adorned with a padlock icon according to a specific <strong>semantic pattern</strong>, identifiable within the <code>href</code> attribute. The advantages of this are as follows:

*   Links to secure pages — and only secure pages — are able to resemble links to secure pages by way of the padlock icon.
*   Links to secure pages that cease to be true links to secure pages will lose the `https` protocol and, with it, the resemblance.
*   New secure pages will adopt the padlock icon and resemble links to secure pages automatically.

This selector becomes truly intelligent when applied to <strong>dynamic content</strong>. Because secure links exist as secure links even in the abstract, the attribute selector can anticipate their invocation: As soon as an editor publishes some content that contains a secure link, the link resembles a secure one to the user. No knowledge of class names or complex HTML editing is required, so even simple <a href="https://daringfireball.net/projects/markdown/syntax#link">Markdown</a> will create the style:

<pre><code class="language-markup">
[Link to secure page](https://payment.example.com/)
</code></pre>

Note that using the <code>[href^="https:"]</code> prefix is not infallible because not all HTTPS pages are truly secure. Nonetheless, it is only as fallible as the browser itself. Major browsers all render a padlock icon natively in the address bar when displaying HTTPS pages.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6275cf9-4cef-4223-8a64-ebaa226ff360/paypal-500-mini.png" alt="PayPal secure page" width="500" height="61" />

### File Types

As promised, you can also style hyperlinks according to how their <code>href</code> value ends. In practice, this means you can use CSS to indicate what <strong>type of file</strong> the link refers to. Auticons supports <code>.txt</code>, <code>.pdf</code>, <code>.doc</code>, <code>.exe</code> and many others. Here is the <code>.zip</code> example, which determines what the <code>href</code> ends with, using <code>$=</code>:

<pre><code class="language-css">
[href$=".zip"]:before,
[href$=".gz"]:before {
   content: 'E004'; /* unicode for the zip folder icon */
}
</code></pre>

### Combinations

You know how you can get all <strong>object-oriented</strong> and use a selection of multiple classes on elements to build up styles? Well, you can do that automatically with attribute selectors, too. Let’s compare:

<pre><code class="language-css">
/* The CSS for the class approach */

.new-window-icon:after {
   content: '[new window icon]';
}

.twitter-icon:before {
  content: '[twitter icon]';
}

/* The CSS for the attribute selector approach */

[target="_blank"]:after {
   content: '[new window icon]';
}

[href*="twitter.com/"]:before {
  content: '[twitter icon]';
}
</code></pre>

(Note the <code>*=</code> comparator, which means “contains.” If the value string contains the substring <code>twitter.com/</code>, then the style will be honored.)

<pre><code class="language-markup">
&lt;!-- The HTML for the class approach --&gt;

&lt;a href="https://twitter.com/heydonworks" class="new-window-icon twitter-icon"&gt;@heydonworks&lt;/a&gt;

&lt;!-- The HTML for the attribute selector approach --&gt;

&lt;a href="https://twitter.com/heydonworks" target="_blank"&gt;@heydonworks&lt;/a&gt;
</code></pre>

<img loading="lazy" decoding="async" class="127057" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33358569-f12d-4b1f-a25c-134566c9e7f9/art-twitter-500-mini.png" alt="A twitter link with icons to show that it goes to twitter and is external" width="553" height="86" />

Any content editor charged with adding a link to a Twitter page now needs to know only two things: the URL (they probably know the Twitter account already) and how to open links in new tabs (obtainable from a quick Google search).</p>

### Inheritance

Some unfinished business: What if we have a link that does not match any of our special attribute selectors? What if a hyperlink is just a plain old hyperlink? The selector is an easy one to remember, and performance fanatics will be pleased to hear that it couldn’t be any terser without existing at all.

<img loading="lazy" decoding="async" class="127053" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e0af618-2c62-473c-b099-f99104da6a63/art-a-mini.png" alt="A basic anchor selector (a)" width="200" height="219" />

Flippancy aside, let me assure you that inheritance within the cascade works with attribute selectors just as it does with classes. First, style your basic <code>a</code> — perhaps with a <code>text-decoration: underline</code> rule to keep things accessible; then, progressively enhance further down the style sheet, using the attribute selectors at your disposal. Browsers such as Internet Explorer (IE) 7 do not support pseudo-content at all. Thanks to inheritance, at least the links will still look like links.

<pre><code class="language-css">
a {
  color: blue;
  text-decoration: underline;
}

a[rel="external"]:after {
   content: '[icon for external links]';
}
</code></pre>

## Actual Buttons Are Actual

In the following section, we’ll detail the construction of our CSS bookmarklet for reporting code errors. Before doing this, let’s look at how plain stupid selectors can creep into our workflow in the first place.

Adherents of <abbr title="Object Oriented CSS">OOCSS</abbr> are keen on classes because they can be reused, as components. Hence, <code>.button</code> is preferable to <code>#button</code>. I can think of one better component selector for button styles, though. Its name is easy to remember, too.

<img loading="lazy" decoding="async" class="127236" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a222cba-d0c9-4389-9a0f-4edad9bf6334/art-button-mini.png" alt="button element selector" width="410" height="117" /><br>
<blockquote>The <code>&lt;button&gt;</code> element represents a button.

– <a href="https://www.w3.org/wiki/HTML/Elements/button">W3C Wiki</a></blockquote>

<a href="https://topcoat.io/">Topcoat</a> is an OOCSS BEM-based <abbr title="User Interface">UI</abbr> framework from Adobe. The CSS for Topcoat’s various button styles is <strong>more than 450 lines</strong> if you include the comment blocks. Each of these comment blocks suggests applying your button style in a manner similar to this introductory example:

<pre><code class="language-markup">
   &lt;a class="topcoat-button"&gt;Button&lt;/a&gt;
</code></pre>

This example is not a button. No, sir. If it were a button, it would be marked up using <code>&lt;button&gt;</code>. In fact, in every single browser known to man, if it were marked up as a button and no author CSS was supplied, you could count on it looking like a button by default. It’s not, though; it’s marked up using <code>&lt;a&gt;</code>, which makes it a hyperlink — a hyperlink, in fact, that lacks an <code>href</code>, meaning it isn’t even a hyperlink. Technically, it’s just a <a href="https://www.w3.org/wiki/HTML/Elements/a">placeholder</a> for a hyperlink that you haven’t finished writing yet.

<img loading="lazy" decoding="async" class="127474" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf5992a-9bf0-4028-8043-4297fe1d6f42/shark-dog-mini.jpg" alt="Dog in a shark costume" width="500" height="375" /><br>
<em>A dog in a shark costume does not a shark make. (Image: <a href="https://www.flickr.com/photos/youngandwithit/">reader of the pack</a>)</em>

The examples in Topcoat’s CSS are only examples, but the premise that the class defines the element and not the HTML is deceptive. No amount of class name modification via "meaningful hyphenation" can make up for this invitation to turn your unintelligent selector into a plain stupid one and to just <strong>code stuff wrong</strong>.

<strong>Update:</strong> Since writing this article, Topcoat.io has replaced these examples with &lt;button&gt; examples. This is great! However, I still have my reservations about the way the examples expound the use of the <code>.is-disabled</code> class while omitting the proper <code>disabled</code> attribute. To hear both sides, find my conversation with the Topcoat representative in the comments. For further examples of OOCSS-facilitated web standards mishaps, look no further than <a href="https://semantic-ui.com/elements/button.html">semantic-ui.com</a>. The "standard button" in their examples is a &lt;div&gt; containing an empty &lt;i&gt;.</p>

### See No Evil, Hear No Evil

<blockquote>"If it looks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck."</blockquote>

A link that resembles a button and triggers button-like JavaScript events is, to many, a button. However, this only means that it has passed the first two stages of the “duck test.” For all users to be able to apply inductive reasoning and discern the button as such, it must also quack like one. Because it remains a link, it will be announced by screen readers as “link,” meaning that your allegorical skyscraper is not wheelchair-accessible. Avoiding this kind of unnecessary confusion for assistive technology users is not a pursuit of semantic perfection but a responsibility we should undertake for real benefit.

Nonetheless, some will insist on using <code>a</code> as the basis of their buttons. Hyperlinks are (slightly) easier to restyle consistently, after all. If <code>a</code> is the element of choice, then there is only one way to make it a close-to-true button in the accessibility layer. You guessed it: You must apply another meaningful attribute in the form of a <a href="https://www.w3.org/WAI/intro/aria">WAI ARIA</a> role. To ensure that a hyperlink element looks like a button for good reason, apply only the following attribute selector.

<pre><code class="language-css">
[role="button"] {
   /* semantic CSS for modified elements that are announced as “button” in assistive technologies */
}
</code></pre>

## Quality Assurance With Attribute Selectors

<blockquote>"CSS gives so much power to the <code>class</code> attribute, that authors could conceivably design their own “document language” based on elements with almost no associated presentation (such as DIV and SPAN in HTML) and assigning style information through the “class” attribute. Authors should avoid this practice since the structural elements of a document language often have recognized and accepted meanings."

– “<a href="https://www.w3.org/TR/CSS2/selector.html#class-html">Selectors</a>,” CSS Level 2, W3C</blockquote>

The reason we have two elements — <code>a</code> and <code>button</code> — is to semantically demarcate two entirely different types of functional interaction. While the hyperlink denotes a means to go somewhere, the button is intended as the instigator of an event or action. One is about traversal, the other about transformation. One facilitates disengagement, the other engagement.

To make sure we don’t do anything too daft and get our links and buttons muddled up, we will now build a CSS bookmarklet that uses intelligent attribute selectors to test the validity and quality of the two respective elements.

Inspired partly by <a href="https://meyerweb.com/eric/tools/css/diagnostics/">Eric Meyer’s post</a> and taking a few cues from <a href="https://github.com/diagnosticss/diagnosticss">DiagnostiCSS</a>, this style sheet will combine attribute selectors and the <code>:not</code> selector (or <a href="https://dev.w3.org/csswg/selectors3/#negation">negation pseudo-class</a>) to highlight problems in the HTML. Unlike these other two implementations, it will write an error to the screen using pseudo-content. Each error will be written in <strong style="font-family: 'comic sans ms', cursive !important;">Comic Sans</strong> against a <span style="background: pink;">pink background</span>.

By connecting function directly to form, we see that ugly markup results in ugly CSS. Consider this the revenge of an abused document, exacted on its designer. To try it out, drag <code>revenge.css</code> to your bookmarks, and click the bookmark to trigger it on any page that you fancy. <strong>Note:</strong> It won't currently work for pages that are served over https.
<div style="text-align: center; padding-top: 30px;"><a style="font-size: 2em; padding: 1em; background: pink; font-family: 'comic sans ms', cursive; color: #000;" title="REVENGE.CSS" href="https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/">REVENGE.CSS</a><br>
<em>Drag to your bookmarks bar.</em></div>

### Rule 1

<blockquote>"If it’s a hyperlink, it should have an <code>href</code> attribute."</blockquote>

<pre><code class="language-css">
a:not([href]):after {
   content: 'Do you mean for this to be a link or a button, because it does not link to anything!';
   display: block !important;
   background: pink !important;
   padding: 0.5em !important;
   font-family: 'comic sans ms', cursive !important;
   color: #000 !important;
   font-size: 16px !important;
}
</code></pre>

<strong>Notes</strong>: In this example, we are testing not the attribute’s value, but whether the attribute exists in the first place — that is, whether <code>[href]</code> matches any element with an <code>href</code> attribute. This test is only appropriate on hyperlinks, hence the <code>a</code> prefix. The rule reads like, “For every <code>a</code> element that is not also an <code>[href]</code> element, append some pseudo-content with an error notice.”

### Rule 2

<blockquote>"If it’s a hyperlink and has an <code>href</code> attribute, it should have a valid value."</blockquote>

<pre><code class="language-css">
a[href=""]:after, a[href$="#"]:after, a[href^="javascript"]:after {
   content: 'Do you mean for this link to be a button, because it does not go anywhere!';
   /*... ugly styles ...*/
}
</code></pre>

<strong>Notes:</strong> If the <code>href</code> is empty, ends in a <code>#</code> or is using JavaScript, it’s probably being used as a button without the correct <code>button</code> element. Note that I am using “starts with <code>javascript</code>.” Standard practice for voiding <code>href</code>s is to use <code>javascript:void(0)</code>, but we can’t depend on that always being written in the same way (with or without a space after the colon, for example).</p>

### Rule 3

<blockquote>"If it uses a button class, it should be a button — at least in the accessibility layer."</blockquote>

<pre><code class="language-css">
.button:not(button):not([role="button"]):not([type="button"]):not([type="submit"]):not([type="reset"]):after,
.btn:not(button):not([role="button"]):not([type="button"]):not([type="submit"]):not([type="reset"]):after,
a[class*="button"]:not([role="button"]):after {
   content: 'If you are going to make it look like a button, make it a button, damn it!';
   /*... ugly styles ...*/
}
</code></pre>

<strong>Notes:</strong> In this example, we’re demonstrating how you can chain negation when testing for attributes. Each selector reads like this: “If the element has a class that says it’s a button but it’s not a <code>button</code> element <em>and</em> it doesn’t have the correct role to make it a button in the accessibility layer <em>and</em> it’s not an input being used as a button, then… well, you’re lying.” I’ve had to use <code>[class*="button"]</code> to catch the many Topcoat class variations (62 in total!) that fail to enforce actual buttons on hyperlinks. I’ve noticed that some authors use <code>button-container</code> and the like on parent elements, which is why the <code>a</code> qualifier is included to avoid false positives. You may recognize the <code>.btn</code> class from Twitter Bootstrap, which (if you’ve read the <a href="https://twitter.github.io/bootstrap/components.html#buttonDropdowns">component’s documentation</a> carefully) you’ll know is also unsure about whether links or buttons are buttons.</p>

### Rule 4

<blockquote>"If it is an <code>a</code> element with <code>role="button"</code>, then it should link to somewhere when JavaScript is off."</blockquote>

<pre><code class="language-css">
a[role="button"]:not([href*="/"]):not([href*="."]):not([href*="?"]):after {
   content: 'Either use a link fallback, or just use a button element.';
   /*... ugly styles ...*/
}
</code></pre>

<strong>Notes</strong>: We can be fairly sure that <code>href</code>s that do not include one of <code>/</code>, <code>.</code> (usually to precede a file extension) or <code>?</code> (to start a query string) are probably bogus. Getting links to act as buttons and <code>return: false</code> when JavaScript is on is fine — fine, that is, if they have a page to go to when JavaScript is off. In fact, it’s the only legitimate reason I can think of not to use <code>&lt;button&gt;</code> instead.</p>

### Rule 5

<blockquote>"You can’t disable a hyperlink."</blockquote>

<pre><code class="language-css">
a.button[class*="disabled"]:after,
a.btn.disabled:after,
a[class*="button"][class*="disabled"]:after {
   content: 'You cannot disable a hyperlink. Use a button element with disabled="disabled".';
   /*... ugly styles ...*/
}
</code></pre>

<strong>Notes:</strong> Even ancient user agents understand the <code>disabled</code> attribute, so use it with an appropriate element in a compliant way. You can concatenate attribute selectors just as you can concatenate classes: In the last of the three selectors, we’re saying, “If it’s a link that contains the substring <code>button</code> <em>and</em> the substring <code>disabled</code>, then print an error message.” Twitter Bootstrap uses the second form, <code>.btn.disabled</code>, in its style sheet, but not with the <code>a</code> prefix. We’ll only consider it an error if used on hyperlinks.</p>

### Rule 6

<blockquote>"Buttons in forms should have explicit types."</blockquote>

<pre><code class="language-css">
form button:not([type]):after {
    content: 'Is this a submit button, a reset button or what? Use type="submit", type="reset" or type="button"';
}
</code></pre>

<strong>Notes</strong>: We need to determine whether <code>button</code>s within forms have explicit types, because <a href="https://stackoverflow.com/questions/932653/how-to-prevent-buttons-from-submitting-forms">some browsers</a> will treat any <code>button</code> in this context without a specified type as <code>type="submit"</code>. We want to be absolutely sure that the form won’t submit if our button has a different purpose.</p>

### Rule 7

<blockquote>"Both hyperlinks and buttons should have some sort of content or an ARIA label."</blockquote>

<pre><code class="language-css">
a:empty:not([aria-label]):not([aria-labelledby]):after,
button:empty:not([aria-label]):not([aria-labelledby]):after,
button:not([aria-label]):not([aria-labelledby]) img:only-child:not([alt]):after,
a:not([aria-label]):not([aria-labelledby]) img:only-child:not([alt]):after {
   content: 'All buttons and links should have text content, an image with alt text or an ARIA label';
   /*... ugly styles ...*/
}
</code></pre>

<strong>Notes</strong>: Buttons and links that don’t include any kind of direction for their usage — in either textual or graphical form — are pretty bogus. These final two selectors are perhaps the most complex I’ve ever written. For the hyperlink version, the selector reads something like this: “If it is a hyperlink that does not have either an <code>aria-label</code> attribute or an <code>aria-labelledby</code> attribute and it contains <em>only</em> an image as content but this image does not have an <code>alt</code> attribute, then write the ugly error message.” Also, note the use of the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/:empty"><code>:empty</code> selector</a>. Arguably, no element that is not self-closing should ever be left empty.

Ten points to the first person using <strong>revenge.css</strong> who can tell me where I’ve broken my own rule in this very article. Trust me, the error is definitely there.</p>

## Conclusion

The reason I use the kinds of selectors and patterns described above is not to try something different or to have something new to write about. Attribute selectors aren’t, by themselves, anything new anyway. IE 6 is the <a href="https://www.quirksmode.org/css/selectors/">only browser</a> that doesn’t support them. The reason I use them is because I simply do not have the time or mental capacity to “do” HTML and CSS in parallel. My brain just isn’t good enough for that. The reason I style my page headers with <code>[role="banner"]</code> and not <code>.page-header</code> is because that’s the only way I’ll know — upon seeing the intended visual effect — that I’ve put the <a href="https://blog.paciellogroup.com/2013/07/enabling-landmark-based-keyboard-navigation-in-firefox/">navigable landmark</a> in place. How else does one keep track? You can’t just leave it to testing, because then it’s usually too late.

<strong>There’s no such thing as semantic CSS.</strong> There’s only semantic HTML and its visible form. In this article I have tried to demonstrate that, by coupling the function and form of Web pages directly, you can create mechanisms for reward and punishment. On the one hand, you can set up selectors that invoke visual motifs only when the suitable markup is used. On the other hand, you can query the markup for bad patterns and erode the visual design as a commitment to the underlying ugly truth.

It’s true that not all the styling hooks in your arsenal will likely ever be uniformly semantic or intelligent. Classes are often desirable as polyfills for much needed elements or attributes that have yet to be standardized. That’s how <code>.footer</code> became <code>&lt;footer&gt;</code> and <code>type="text"</code> (with a bunch of JavaScript) became <code>type="url"</code>. Other times, they are helpful for doing non-semantic layout scaffolding with <a href="https://unsemantic.com/">grid frameworks</a> and the like.

However, if you are committed to giving CSS its own completely separate logic, then you are bound to create unnecessary arguments between form and function. In this eventuality, only constant vigilance can protect against inaccessibility and invalidity. To make matters worse, trying to manufacture pseudo-semantics purely with classes makes it easy to fall into one of those interminable discussions over <a href="https://css-tricks.com/semantic-class-names/">what makes a semantic class name</a>. You’ll start spending less time using the remote to control the TV and more time just sitting there, contemplating the remote control held in your hand.

Life is too short.

{{< signature "al" >}}

