---
title: CSS-Driven Internationalization In JavaScript
slug: css-driven-internationalization-in-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c71637e-d98c-4365-94fd-d6a8be08971e/js-screen-preview-opt.jpg
date: 2014-06-23T21:23:45.000Z
author: maksim-chemerisuk
description: >-
  Writing front-end code often requires developers to address the problem of
  internationalization at some level. Despite the [current
  standard](https://www.w3.org/TR/its20/), which introduces a bunch of new tags,
  simply adding support for different languages in a JavaScript plugin is still
  complicated. As a result, for any new project, you have to build a solution
  from scratch or adapt various existing APIs from other plugins that you use.

  In this article, I’ll describe my approach with
  [better-dom](https://github.com/chemerisuk/better-dom) to solve the
  internationalization problem. Since the last article about this, “[Writing a
  Better JavaScript Library for the
  DOM](https://www.smashingmagazine.com/2014/01/13/writing-a-better-javascript-library-for-the-dom/),”
  I’ve revisited the concept to solve the issues raised through feedback.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
---
Writing front-end code often requires developers to address the problem of internationalization at some level. Despite the <a href="https://www.w3.org/TR/its20/">current standard</a>, which introduces a bunch of new tags, simply adding support for different languages in a JavaScript plugin is still complicated. As a result, for any new project, you have to build a solution from scratch or adapt various existing APIs from other plugins that you use.

In this article, I’ll describe my approach with <a href="https://github.com/chemerisuk/better-dom">better-dom</a> to solve the internationalization problem. Since the last article about this, “<a href="https://www.smashingmagazine.com/2014/01/13/writing-a-better-javascript-library-for-the-dom/">Writing a Better JavaScript Library for the DOM</a>,” I’ve revisited the concept to solve the issues raised through feedback.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2014/12/how-to-conduct-website-localization/#further-reading-on-smashingmag)

*   [Don’t Get Lost In Translation: How To Conduct Website Localization](https://www.smashingmagazine.com/2014/12/how-to-conduct-website-localization/)
*   [<span class="headline">Should You Ask The User Or Their Browser?</span>](https://www.smashingmagazine.com/2012/07/12-commandments-software-localization/)
*   [12 Commandments Of Software Localization](https://www.smashingmagazine.com/2012/07/12-commandments-software-localization/)

The solution was originally intended to be a set of <strong>internationalization APIs for plugins, extensions, etc.</strong> It doesn’t rely heavily on the better-dom library, so it could be adapted to any existing JavaScript library.

{{% feature-panel %}}

## A Typical Solution To The Problem

Different APIs exist for changing languages in JavaScript. Most of them contain three main functions:

1.  The first function registers a localized string by key and language.
2.  The second sets a localized string for a particular element.
3.  The third is used to change the current language.

Let’s look at an example based on the Validator plugin from the jQuery Tools library. The plugin supports the localization of validation errors via JavaScript. Default error messages are stored in the <code>$.tools.validator.messages</code> object.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705e2214-dc88-4ff3-aca1-2feb74029666/01-messages-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937dfaaf-8d83-4440-b3a5-9f7f6e310f07/01-messages-opt-500.gif" alt="01-messages-opt-500" width="500" height="133" /></a><figcaption>Default error messages are stored in the <code>$.tools.validator.messages</code> object. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/705e2214-dc88-4ff3-aca1-2feb74029666/01-messages-opt.gif">View large version</a>)</figcaption></figure>

For keys, the plugin uses CSS selectors (to simplify the code). If you want to provide error messages in other languages, you would use the <code>$.tools.validator.localize</code> method, as follows:

<pre><code class="language-javascript">
$.tools.validator.localize("fi", {
	":email" : "Virheellinen s&amp;auml;hk&amp;ouml;postiosoite",
	":number" : "Arvon on oltava numeerinen",
	"[max]" : "Arvon on oltava pienempi, kuin $1",
	"[min]" : "Arvon on oltava suurempi, kuin $1",
	"[required]" : "Kent&amp;auml;n arvo on annettava"
});
</code></pre>

This method populates for Finnish localization. The <code>$.tools.validator.messages</code> object would look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d8a470-f7b1-4e99-b8a8-691e18930da4/02-messages-fi-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0174d01-c243-4aaf-af59-1af178f03d3f/02-messages-fi-opt-500.gif" alt="02-messages-fi-opt-500" width="500" height="162" /></a><figcaption>The <code>$.tools.validator.messages</code> object populated for Finnish localization (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0d8a470-f7b1-4e99-b8a8-691e18930da4/02-messages-fi-opt.gif">View large version</a>)</figcaption></figure>

Now, if you want to use the Finnish localization in your form, then you need to change the default language (English) via the <code>lang</code> configuration option:

<pre><code class="language-javascript">
$("#myForm").validator({lang: "fi"});
</code></pre>

The plugin implements the typical solution that we have at present. Having looked at approaches similar to this one, I found several common shortcomings:

1.  **Obtrusive** You have to add a JavaScript function call if the current page’s language is different from the default (usually English) used in a plugin.
2.  **Ineffective** To change a language dynamically, you have to call a particular function and then touch the DOM of every related element to update the `innerHTML`, depending on the new language.
3.  **Hard to maintain** Every plugin has its own set of APIs.

The first shortcoming is the most critical. If your project has a lot of components, switching to the non-default language on initial page load for every plugin will be painful. If the project fetches data using AJAX calls, then the same steps would have to be done for future content as well. Let’s try to solve all of these shortcomings. First, we need to go through the technical stuff.

### The `:lang` Pseudo-Class

Remember the <code>:lang</code> pseudo-class from CSS2? It’s rarely used, but when I first read about it <a href="https://www.w3.org/TR/CSS21/selector.html#lang">in the specification</a>, I was curious what the standard’s authors intended to solve with it:
<blockquote>If the document language specifies how the human language of an element is determined, it is possible to write selectors in CSS that match an element based on its language.</blockquote>

A typical example cited in the specification is the symbol for quotations. The symbol varies between languages. To address this for the <a href="https://www.w3.org/TR/html-markup/q.html"><code>&lt;q&gt;</code> element</a> (which marks up a short quotation, usually wrapped in quotation marks), we can use the <code>:lang</code> pseudo-class:

<pre><code class="language-css">
:lang(fr) &gt; q { quotes: '« ' ' »' }
:lang(de) &gt; q { quotes: '»' '«' '\2039' '\203A' }
</code></pre>

An important difference between the <code>:lang</code> pseudo-class and a simple attribute selector like <code>[lang=fr]</code> is that the latter matches only elements that have the <code>lang</code> attribute. Therefore, the <code>:lang</code> pseudo-class is always safer than the attribute variant because it works properly even if the <code>:lang</code> attribute has not been set on an element.

The example above illustrates how to <strong>change the representation of content according to the current language using CSS</strong>. This is important because it enables us to <strong>put the logic related to changing the language into CSS</strong>.

The example of the symbol for quotation marks is nice, but it addresses a small number of cases and so can’t be used in typical scenarios — ordinary strings are usually very different in different languages. We need a trick that allows us to change an element’s content <em>completely</em>.</p>

### Changing an Element’s Content With CSS

Browsers that support the CSS2 specification introduced pseudo-elements, which, rather than describing a particular state like pseudo-classes, enable us to style certain parts of a document.

Note that Internet Explorer 8 has a known issue in its implementation in that it does not support the double-colon syntax for defining pseudo-elements. The problem was fixed in Internet Explorer 9, so if you need to support version 8, make sure to use the single-colon syntax for any pseudo-element.

The real gems are <code>::before</code> and <code>::after</code>, which enable you to add extra content before or after an element’s <code>innerHTML</code>. They might look simple, but they have a ton of use cases that solve problems in a very clean way.

Let’s start with the basics. Both <code>::before</code> and <code>::after</code> introduce a CSS property, <code>content</code>. This new property defines what content to prepend or append to an element’s <code>innerHTML</code>. The value of the <code>content</code> attribute may be any of the following:

*   text string (but not an HTML string),
*   image,
*   counter,
*   attribute value(s).

Our main interest is adding a text string. Imagine we have CSS like this:

<pre><code class="language-css">
#hello::before {
   content: "Hello ";
}
</code></pre>

If the element with the ID of <code>hello</code> contains the string <code>world</code>, then the browser would display <code>Hello world</code>.</p>

<pre><code class="language-markup">
&lt;p id="hello"&gt;world&lt;/p&gt;
</code></pre>

We could rewrite our CSS using the <code>attr</code> function:

<pre><code class="language-css">
#hello::before {
   content: attr(id) " ";
}
</code></pre>

Then, the element would display <code>hello world</code> in lowercase, because the <code>id</code> attribute has a lowercased string value.

Now, imagine that the <code>hello</code> element didn’t have any inner content. We could change its representation completely using CSS. This becomes handy when we use the trick in combination with the <code>:lang</code> pseudo-class:

<pre><code class="language-css">
#hello::before {
   content: "Hello";
}
#hello:lang(de)::before {
   content: "Hallo";
}
#hello:lang(ru)::before {
   content: "Привет";
}
</code></pre>

Our element <code>hello</code> will now change according to the current web page’s language — no need to call any function to change its representation according to the current web page’s language. The localization is handled by the value of the <code>lang</code> attribute on the <code>&lt;html&gt;</code> element and several extra CSS rules. This is what I call <i>CSS-driven internationalization</i>.

## CSS-Driven Internationalization: Improved!

Since publishing the original idea, I’ve heard several people complain that those rules could add a lot of CSS. Because my initial goal was to use it for small JavaScript plugins, I didn’t even think it could be used widely on the page. However, the philosophy of CSS is to contain the presentation logic, and I was trying to use it to store various multilingual strings, which actually belong to the web page’s content. It didn’t seem right.

After some thinking, I developed an improved version that solves this issue. Instead of putting text strings into CSS, I use the <code>attr</code> function to read a language-specific <code>data-i18n-*</code> attribute that contains a localized string. This restricts the number of CSS rules we can add: one rule per new language.

Let’s rewrite the localization of the <code>hello</code> element above with this improved method. This time, let’s give our web page some global CSS to support German and Russian, in addition to English:

<pre><code class="language-css">
/* English (default language)*/
[data-i18n]::before {
   content: attr(data-i18n);
}
/* German */
[data-i18n-de]:lang(de)::before {
   content: attr(data-i18n-de);
}
/* Russian */
[data-i18n-ru]:lang(ru)::before {
   content: attr(data-i18n-ru);
}
</code></pre>

Note that the code above doesn’t contain any string constant: The CSS rules are generic.

Now, instead of putting localized text strings into CSS, let’s add several custom language-specific <code>data-*</code> attributes that contain the appropriate values. Our <code>hello</code> element should look like the following, which will display different content according to the current web page’s language:

<pre><code class="language-markup">
&lt;p id="hello" data-18n="Hello" data-i18n-de="Hallo" data-i18n-ru="Привет"&gt;&lt;p&gt;
</code></pre>

That’s it! We’re left with minimal extra CSS, which describes only the global logic for changing an element’s <strong>representation</strong> according to the current language, and our <strong>localized strings are fully HTML</strong>.</p>

## Building A High-Level API

In better-dom, there are two functions to support CSS-driven internationalization: <code>$Element.prototype.i18n</code> and <code>DOM.importStrings</code>. The first function changes the localized string for a particular element. To keep it simple, I usually use the English strings as keys and default values. It makes the JavaScript more readable and easier to understand. For instance:

<pre><code class="language-javascript">
myelement.i18n("Hello");
</code></pre>

This sets a localized <code>Hello</code> string as the inner content of <code>myelement</code>, where <code>myelement</code> is an instance of the <code>$Element</code> class, which happens to be a wrapper type for a native DOM element in better-dom. The line above does several things behind the scenes:

*   It determines the current set of registered languages.
*   For each language, it reads a string with the key `Hello` in the internal storage of registered localizations, and it uses the value to set an appropriate `data-i18n-*` attribute for the element.
*   It cleans up the element’s `innerHTML` to prevent a weird result from displaying.

You can see the source code of <code>$Element.prototype.i18n</code> on GitHub. The goal of this <code>i18n</code> method is to update our custom language-specific <code>data-*</code> attributes. For example:

<pre><code class="language-markup">
&lt;p id="hello"&gt;&lt;p&gt;
</code></pre>

After the call, this empty element would become the following, if we have registered all of the localized strings for German and Russian:

<pre><code class="language-markup">
&lt;p id="hello" data-i18n="Hello" data-i18n-de="Hallo" data-i18n-ru="Привет"&gt;&lt;p&gt;
</code></pre>

Additionally, the <code>i18n</code> method supports an optional second argument, a key-value map of the variables:

<pre><code class="language-javascript">
// Use {varName} in the string template to define
// various parts of a localized string.
myelement.i18n("Hello {user}", {user: username});

// Use array and {varNumber} to define a numeric
// set of variables.
myelement.i18n("Hello {0}", [username]);
</code></pre>

To register a localized string, use the static method <code>DOM.importStrings</code> to pass three arguments:

*   the target language,
*   the localized string key (usually just an English string),
*   the localized string value.

For the example above, before invoking the i18n method, we would need to make the following calls:

<pre><code class="language-javascript">
DOM.importStrings("de", "Hello {user}", "Hallo {user}");
DOM.importStrings("ru", "Hello {user}", "Привет {user}");

DOM.importStrings("de", "Hello {0}", "Hallo {0}");
DOM.importStrings("ru", "Hello {0}", "Привет {0}")
</code></pre>

Behind the scenes, <code>DOM.importStrings</code> is going through a couple of steps. First, it checks whether the target language has been registered. If not, it adds a global CSS rule:

<pre><code class="language-css">
[data-i18n-{lang}]:lang({lang})::before {
   content: attr(data-i18n-{lang});
}
</code></pre>

Then, it saves a localized string, the key-value pair, in internal storage. You can see the source code of <code>DOM.importStrings</code> on GitHub.

With <code>DOM.importStrings</code>, we can also override existing English strings. This could be useful if you need to adapt strings to your needs without changing the source code:

<pre><code class="language-javascript">
DOM.importStrings("en", "Hello {user}", "Hey {user}");
DOM.importStrings("en", "Hello {0}", "Hey {0}");
</code></pre>

As you can see, these helpers free us from having to write boilerplate code and enable us to use CSS-driven internationalization on our web pages very easily.</p>

## Advantages Of CSS-Driven Internationalization

Let’s review the list of issues identified in the first part of the article.</p>

### Is It Unobtrusive?

With the original solution, we said you had to add a JavaScript function call if the current page’s language was different from the default (usually English) used in the plugin. A big advantage of CSS-driven internationalization is that it uses the <code>:lang</code> pseudo-class to switch to the target language. This means that having an appropriate value of the <code>lang</code> attribute on the <code>&lt;html&gt;</code> element is enough to choose the localized string that you need.

Therefore, with CSS-driven internationalization, you do not need to make any calls on page load, even if the web page’s language is different from the default language. So, it’s unobtrusive.</p>

### Is It Effective?

To change a language dynamically, you had to call a particular function and then touch the DOM of every related element to update the <code>innerHTML</code>, depending on the new language. Now, the representation of an element is handled by the <code>::before</code> pseudo-element. To switch to another language dynamically at a global level, just change the <code>lang</code> attribute of the <code>&lt;html&gt;</code> element (using native APIs, for example). Or, to localize the language change, just change the <code>lang</code> attribute of a particular subtree.

Also, you don’t need to update the <code>innerHTML</code> of all related elements in order to change the current language dynamically. This is handled by CSS. So, our code is now more effective.</p>

### Is It Easy to Maintain?

Every plugin originally had to have its own set of APIs. A robust solution for internationalization should be a part of every serious library that touches the DOM. CSS-driven internationalization has been a part of my better-dom project since the beginning because I had to address this problem. I used it in <a href="https://github.com/chemerisuk/better-form-validation">better-form-validation</a> to customize the form-validation tooltips. Later, I used it in <a href="https://github.com/chemerisuk/better-dateinput-polyfill">better-dateinput-polyfill</a> and <a href="https://github.com/chemerisuk/better-prettydate">better-prettydate</a>. Having APIs for internationalization built into the core library reduces my boilerplate code and makes it more consistent, stabler and — you guessed it — easier to maintain.</p>

## Limitations Of CSS-Driven Internationalization

What about cons of CSS-driven internationalization?

### JavaScript

First, the solution depends on JavaScript. Putting localized strings into <code>data-*</code> attributes on static web pages isn’t a good idea because the markup would look weird, semantically speaking. Therefore, I’d recommend using a set of JavaScript APIs (like what’s described above) to make the concept workable.

Make sure to use it in parts of your pages that are not critical to SEO, because search engine crawlers will find the resulting markup difficult to index correctly. Remember that this solution was originally developed as a set of localization APIs for JavaScript plugins and extensions.</p>

### Pseudo-Elements

Some limitations also come from using the <code>::before</code> and <code>::after</code> pseudo-elements:

1.  The `content` property does not work on empty elements or on certain form elements, including `<input>` and `<select>`.
2.  The `content` property cannot display HTML tags.
3.  There is no way to localize the values of an HTML element’s attributes (such as `placeholder` and `title`).

As for the first limitation, the lack of support for empty elements is not a big problem. The elements do not contain any content, so there is nothing to localize. But the problem became real when I was working with the <code>&lt;input&gt;</code> element in better-dateinput-polyfill. To solve this, I hid the original element and added an extra <code>&lt;span&gt;</code> element as a wrapper that contained the localized string I needed to display. Not very elegant, but it worked.

The second and third limitations are easier to avoid for now. I have some ideas on how to solve them, but I don’t have use cases for them. An elegant solution is welcome, of course.</p>

## Solving Accessibility Problems

<span style="color: #e53b2c;">Update (24.06.2014)</span>: Several people have noted in the comments section below that using pseudo-elements to display localized strings has important accessibility problems. The first problem is that a content, generated via <code>::before</code> and <code>::after</code> is not selectable via mouse. The second is that such content is completely missed by screen readers. Therefore, I've improved the concept to address these issues and invite you to <a href="https://jsfiddle.net/mbtP8/3/">check out the demo</a>. It is not part of better-dom APIs yet, but it will be added in the nearest version.

The main difference is that instead of the pseudo-elements, the content is displayed inside of language-specific <code>&lt;span&gt;</code> elements. It is not possible to have several <code>&lt;span&gt;</code>s to be displayed at the same time because <code>&lt;span&gt;</code>s for non-current language are hidden via the <code>display:none</code> rule. Screen readers skip such hidden elements which is what we need exactly.

Using inner <code>&lt;span&gt;</code>s instead of pseudo-elements also fixes text selection via mouse and lack of being able to use HTML tags inside of localized strings. Nevertheless, problems with form elements and localization of attribute values still exist in the present.</p>

## Conclusion

Hopefully, a simple solution to the problem of internationalization in JavaScript will be added to the specification soon. Until then, we front-end developers will have to reinvent the wheel or adapt each other’s wheels.

While building this CSS-driven internationalization solution, I was actually inspired by ideas contained in the CSS2 specification itself. Maybe the authors already had it in mind. Who knows?

After several iterations, the solution solidified. Sure, it still has limitations. Yet its advantages, like being fully unobtrusive, will make your code substantially cleaner and easier to maintain. Hopefully, this article has helped you to understand what I did behind the scenes to achieve that.

Feel free to share your thoughts on the <a href="https://github.com/chemerisuk/better-dom">better-dom library GitHub</a> or in the comments section below.</p>

<em>Front page image credits: <a href="https://www.flickr.com/photos/89943077@N00/2378867408/">Dmitry Baranovskiy</a>.</em>

{{< signature "al, il" >}}

