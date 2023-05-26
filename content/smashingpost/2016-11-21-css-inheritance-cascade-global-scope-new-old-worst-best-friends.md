---
title: 'CSS Inheritance, The Cascade And Global Scope: Your New Old Worst Best Friends'
slug: css-inheritance-cascade-global-scope-new-old-worst-best-friends
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b468a3c3-2ca4-4eae-abc0-3e89ab57e204/rainbow-slinky-opt.png
date: 2016-11-21T22:04:16.000Z
author: heydon-pickering
description: >-
  I'm big on [modular design](https://www.smashingmagazine.com/2016/06/designing-modular-ui-systems-via-style-guide-driven-development/). I've long been sold on dividing websites into components, not pages, and amalgamating those components dynamically into interfaces. Flexibility, efficiency and maintainability abound.
categories:
  - Tools
  - CSS
  - Techniques
---
But I don't want my design to _look_ like it's made out of unrelated things. I'm making an interface, not a surrealist photomontage. As luck would have it, there is already a technology, called CSS, which is designed specifically to solve this problem. Using CSS, I can propagate styles that cross the borders of my HTML components, **ensuring a consistent design with minimal effort**.

*   inheritance,
*   the cascade (the "C" in CSS).

Despite these features enabling a <a href="https://en.wikipedia.org/wiki/Don't_repeat_yourself">DRY</a>, efficient way to style web documents and despite them being the very reason CSS exists, they have fallen remarkably out of favor. From CSS methodologies such as <a href="https://www.smashingmagazine.com/2013/02/the-history-of-the-bem-methodology/">BEM</a> and Atomic CSS through to programmatically encapsulated CSS modules, many are doing their best to sidestep or otherwise suppress these features. This gives developers more control over their CSS, but only an autocratic sort of control based on frequent intervention.

{{% feature-panel %}}

I'm going to revisit inheritance, the cascade and scope here with respect to modular interface design. I aim to show you how to leverage these features so that your CSS code becomes more concise and self-regulating, and your interface more easily extensible.

## Inheritance And `font-family`

Despite protestations by many, CSS does not only provide a global scope. If it did, everything would look exactly the same. Instead, CSS has a global scope and a local scope. Just as in JavaScript, the local scope has access to the parent and global scope. In CSS, this facilitates <strong>inheritance</strong>.

For instance, if I apply a <code>font-family</code> declaration to the root (read: global) <code>html</code> element, I can ensure that this rule applies to all ancestor elements within the document (with a few exceptions, to be addressed in the next section).</p>

<pre><code class="language-css">
html {
  font-family: sans-serif;
}

/*
This rule is not needed ↷
p {
  font-family: sans-serif;
}
*/
</code></pre>

Just like in JavaScript, if I declare something within the local scope, it is not available to the global — or, indeed, any ancestral — scope, but it is available to the child scope (elements within <code>p</code>). In the next example, the <code>line-height</code> of <code>1.5</code> is not adopted by the <code>html</code> element. However, the <code>a</code> element inside the <code>p</code> does respect the <code>line-height</code> value.</p>

<pre><code class="language-css">
html {
  font-family: sans-serif;
}

p {
  line-height: 1.5;
}

/*
This rule is not needed ↷
p a {
  line-height: 1.5;
}
*/
</code></pre>

The great thing about inheritance is that you can establish the basis for a consistent visual design with very little code. And these styles will even apply to HTML you have yet to write. Talk about future-proof!

### The Alternative

There are other ways to apply common styles, of course. For example, I could create a <code>.sans-serif</code> class…

<pre><code class="language-css">
.sans-serif {
  font-family: sans-serif;
}
</code></pre>

… and apply it to any element that I feel should have that style:

<pre><code class="language-html">
&lt;p class="sans-serif"&gt;Lorem ipsum.&lt;/p&gt;
</code></pre>

This affords me some control: I can pick and choose exactly which elements take this style and which don't.

Any opportunity for control is seductive, but there are clear issues. Not only do I have to manually apply the class to any element that should take it (which means knowing what the class is to begin with), but in this case I've effectively forgone the possibility of supporting dynamic content: Neither WYSIWYG editors nor Markdown parsers provide <code>sans-serif</code> classes to arbitrary <code>p</code> elements by default.

That <code>class="sans-serif"</code> is not such a distant relative of <code>style="font-family: sans-serif"</code> — except that the former means adding code to both the style sheet <em>and</em> the HTML. Using inheritance, we can do less of one and none of the other. Instead of writing out classes for each font style, we can just apply any we want to the <code>html</code> element in one declaration:

<pre><code class="language-css">
html {
  font-size: 125%;
  font-family: sans-serif;
  line-height: 1.5;
  color: #222;
}
</code></pre>

## The `inherit` Keyword

Some types of properties are not inherited by default, and some elements do not inherit some properties. But you can use <code>[property name]: inherit</code> to force inheritance in some cases.

For example, the <code>input</code> element doesn't inherit any of the font properties in the previous example. Nor does <code>textarea</code>. In order to make sure all elements inherit these properties from the global scope, I can use the universal selector and the <code>inherit</code> keyword. This way, I get the most mileage from inheritance.</p>

<pre><code class="language-css">
* {
  font-family: inherit;
  line-height: inherit;
  color: inherit;
}

html {
  font-size: 125%;
  font-family: sans-serif;
  line-height: 1.5;
  color: #222;
}
</code></pre>

Note that I've omitted <code>font-size</code>. I don't want <code>font-size</code> to be inherited directly because it would override user-agent styles for heading elements, the <code>small</code> element and others. This way, I save a line of code and can defer to user-agent styles if I should want.

Another property I would not want to inherit is <code>font-style</code>: I don't want to unset the italicization of <code>em</code>s just to code it back in again. That would be wasted work and result in more code than I need.

Now, everything either inherits or is <em>forced</em> to inherit the font styles I want them to. We've gone a long way to propagating a consistent brand, project-wide, with just two declaration blocks. From this point onwards, no developer has to even think about <code>font-family</code>, <code>line-height</code> or <code>color</code> while constructing components, unless they are making exceptions. This is where the cascade comes in.

## Exceptions-Based Styling

I'll probably want my main heading to adopt the same <code>font-family</code>, <code>color</code> and possibly <code>line-height</code>. That's taken care of using inheritance. But I'll want its <code>font-size</code> to differ. Because the user agent already provides an enlarged <code>font-size</code> for <code>h1</code> elements (and it will be relative to the <code>125%</code> base font size I've set), it's possible I don't need to do anything here.

However, should I want to tweak the font size of any element, I can. I take advantage of the global scope and only tweak what I need to in the local scope.</p>

<pre><code class="language-css">
* {
  font-family: inherit;
  line-height: inherit;
  color: inherit;
}

html {
  font-size: 125%;
  font-family: sans-serif;
  line-height: 1.5;
  color: #222;
}

h1 {
  font-size: 3rem;
}
</code></pre>

If the styles of CSS elements were encapsulated by default, this would not be possible: I'd have to add <em>all</em> of the font styles to <code>h1</code> explicitly. Alternatively, I could divide my styles up into separate classes and apply each to the <code>h1</code> as a space-separated value:

<pre><code class="language-html">
&lt;h1 class="Ff(sans) Fs(3) Lh(1point5) C(darkGrey)"&gt;Hello World&lt;/h1&gt;
</code></pre>

Either way, it's more work and a styled <code>h1</code> would be the only outcome. Using the cascade, I've styled <em>most</em> elements the way I want them, with <code>h1</code> just as a special case, just in one regard. The cascade works as a filter, meaning styles are only ever stated where they add something new.</p>

## Element Styles

We've made a good start, but to really leverage the cascade, we should be styling as many common elements as possible. Why? Because our compound components will be made of individual HTML elements, and a screen-reader-accessible interface makes the most of semantic markup.

To put it another way, the style of "atoms" that make up your interface "molecules" (to use <a href="https://www.smashingmagazine.com/atomic-design-workflow/">atomic design</a> terminology) should be largely addressable using element selectors. Element selectors are low in <a href="https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/">specificity</a>, so they won't override any class-based styles you might incorporate later.

The first thing you should do is style all of the elements that you know you're going to need:

<pre><code class="language-css">
a { … }
p { … }
h1, h2, h3 { … }
input, textarea { … }
/* etc */
</code></pre>

The next part is crucial if you want a consistent interface without redundancy: Each time you come to creating a new component, <strong>if it introduces new elements, style those new elements with element selectors</strong>. Now is not the time to introduce restrictive, high-specificity selectors. Nor is there any need to compose a class. Semantic elements are what they are.

For example, if I've yet to style <code>button</code> elements (as in the previous example) and my new component incorporates a button element, this is my opportunity to style button elements <strong>for the entire interface</strong>.</p>

<pre><code class="language-css">
button {
  padding: 0.75em;
  background: #008;
  color: #fff;
}

button:focus {
  outline: 0.25em solid #dd0;
}
</code></pre>

Now, when you come to write a new component that also happens to incorporate buttons, that's one less thing to worry about. You're not <strong>rewriting</strong> the same CSS under a different namespace, and there's no class name to remember or write either. CSS should always aim to be this effortless and efficient — it's designed for it.

Using element selectors has three main advantages:

*   The resulting HTML is less verbose (no redundant classes).
*   The resulting style sheet is less verbose (styles are shared between components, not rewritten per component).
*   The resulting styled interface is based on semantic HTML.

The use of classes to exclusively provide styles is often defended as a "separation of concerns." This is to misunderstand the W3C's <a href="https://www.w3.org/TR/html-design-principles/#separation-of-concerns">separation of concerns</a> principle. The objective is to describe structure with HTML and style with CSS. Because classes are designated exclusively for styling purposes and they appear within the markup, you are technically <strong>breaking with</strong> separation wherever they're used. You have to change the nature of the structure to elicit the style.

Wherever you don't rely on presentational markup (classes, inline styles), your CSS is compatible with generic structural and semantic conventions. This makes it trivial to extend content and functionality without it also becoming a styling task. It also makes your CSS more reusable across different projects where conventional semantic structures are employed (but where CSS 'methodologies' may differ).</p>

### Special Cases

Before anyone accuses me of being simplistic, I'm aware that not all buttons in your interface are going to do the same thing. I'm also aware that buttons that do different things should probably look different in some way.

But that's not to say we need to defer to classes, inheritance <em>or</em> the cascade. To make buttons found in one interface look fundamentally dissimilar is to confound your users. For the sake of accessibility <em>and</em> consistency, most buttons only need to differ in appearance by label.</p>

<pre><code class="language-html">
&lt;button&gt;create&lt;/button&gt;

&lt;button&gt;edit&lt;/button&gt;

&lt;button&gt;delete&lt;/button&gt;
</code></pre>

Remember that style is not the only visual differentiator. Content also differentiates visually — and in a way that is much less ambiguous. You're literally spelling out what different things are for.

There are fewer instances than you might imagine where using style alone to differentiate content is necessary or appropriate. Usually, style differences should be supplemental, such as a red background or a pictographic icon accompanying a textual label. The presence of textual labels are of particular utility to those using voice-activation software: Saying "red button" or "button with cross icon" is not likely to elicit recognition by the software.

I'll cover the topic of adding nuances to otherwise similar looking elements in the "Utility Classes" section to follow.</p>

## Attributes

Semantic HTML isn't just about elements. Attributes define types, properties and states. These too are important for accessibility, so they need to be in the HTML where applicable. And because they're in the HTML, they provide additional opportunities for styling hooks.

For example, the <code>input</code> element takes a <code>type</code> attribute, should you want to take advantage of it, and also <a href="/2014/07/the-wai-forward/#aria-invalid">attributes such as <code>aria-invalid</code></a> to describe state.</p>

<pre><code class="language-css">
input, textarea {
  border: 2px solid;
  padding: 0.5rem;
}

[aria-invalid] {
  border-color: #c00;
  padding-right: 1.5rem;
  background: url(images/cross.svg) no-repeat center 0.5em;
}
</code></pre>

A few things to note here:

*   I don't need to set `color`, `font-family` or `line-height` here because these are inherited from `html`, thanks to my use of the `inherit` keyword. If I want to change the main `font-family` used application-wide, I only need to edit the one declaration in the `html` block.
*   The border color is linked to `color`, so it too inherits the global color. All I need to declare is the border's width and style.
*   The `[aria-invalid]` attribute selector is unqualified. This means it has better reach (it can be used with both my `input` and `textarea` selectors) and it has minimal specificity. Simple attribute selectors have the same specificity as classes. Using them unqualified means that any classes written further down the cascade will override them as intended.

The BEM methodology would solve this by applying a modifier class, such as <code>input--invalid</code>. But considering that the invalid state should only apply where it is communicated accessibly, <code>input--invalid</code> is necessarily redundant. In other words, the <code>aria-invalid</code> attribute <em>has</em> to be there, so what's the point of the class?

### Just Write HTML

My absolute favorite thing about making the most of element and attribute selectors high up in the cascade is this: The composition of new components becomes <strong>less a matter of knowing the company or organization's naming conventions and more a matter of knowing HTML</strong>. Any developer versed in writing decent HTML who is assigned to the project will benefit from inheriting styling that's already been put in place. This dramatically reduces the need to refer to documentation or write new CSS. For the most part, they can just write the (meta) language that they should know by rote. Tim Baxter also makes a case for this in <a href="https://alistapart.com/article/meaningful-css-style-like-you-mean-it">Meaningful CSS: Style It Like You Mean It</a>.</p>

## Layout

So far, we've not written any component-specific CSS, but that's not to say we haven't styled anything. All components are compositions of HTML elements. It's largely in the order and arrangement of these elements that more complex components form their identity.

Which brings us to layout.

Principally, we need to deal with flow layout — the spacing of successive block elements. You may have noticed that I haven't set any margins on any of my elements so far. That's because margin should not be considered a property of elements but a property of the context of elements. That is, they should only come into play where elements meet.

Fortunately, the <a href="https://developer.mozilla.org/en/docs/Web/CSS/Adjacent_sibling_selectors">adjacent sibling combinator</a> can describe exactly this relationship. Harnessing the cascade, we can instate a uniform default across <em>all</em> block-level elements that appear in succession, with just a few exceptions.</p>

<pre><code class="language-css">
* {
  margin: 0;
}

* + * {
  margin-top: 1.5em;
}

body, br, li, dt, dd, th, td, option {
  margin-top: 0;
}
</code></pre>

The use of the extremely low-specificity <a href="https://alistapart.com/article/axiomatic-css-and-lobotomized-owls">lobotomized owl selector</a> ensures that <em>any</em> elements (except the common exceptions) are spaced by one line. This means that there is default white space in all cases, and developers writing component flow content will have a reasonable starting point.

In most cases, margins now take care of themselves. But because of the low specificity, it's easy to override this basic one-line spacing where needed. For example, I might want to close the gap between labels and their respective fields, to show they are paired. In the following example, any element that follows a label (<code>input</code>, <code>textarea</code>, <code>select</code>, etc.) closes the gap.</p>

<pre><code class="language-css">
label {
  display: block
}

label + * {
  margin-top: 0.5rem;
}
</code></pre>

Once again, using the cascade means only having to write specific styles where necessary. Everything else conforms to a sensible baseline.

Note that, because margins only appear between elements, they don't double up with any padding that may have been included for the container. That's one more thing not to have to worry about or code defensively against.

Also, note that you get the same spacing whether or not you decide to include wrapper elements. That is, you can do the following and achieve the same layout — it's just that the margins emerge between the <code>div</code>s rather than between labels following inputs.</p>

<pre><code class="language-html">
&lt;form&gt;
  &lt;div&gt;
    &lt;label for="one"&gt;Label one&lt;/label&gt;
    &lt;input id="one" name="one" type="text"&gt;
  &lt;/div&gt;
  &lt;div&gt;
    &lt;label for="two"&gt;Label two&lt;/label&gt;
    &lt;input id="two" name="two" type="text"&gt;
  &lt;/div&gt;
  &lt;button type="submit"&gt;Submit&lt;/button&gt;
&lt;/form&gt;
</code></pre>

Achieving the same result with a methodology such as <a href="https://acss.io/">atomic CSS</a> would mean composing specific margin-related classes and applying them manually in each case, including for <code>first-child</code> exceptions handled implicitly by <code>* + *</code>:

<pre><code class="language-html">
&lt;form class="Mtop(1point5)"&gt;
  &lt;div class="Mtop(0)"&gt;
    &lt;label for="one" class="Mtop(0)"&gt;Label one&lt;/label&gt;
    &lt;input id="one" name="one" type="text" class="Mtop(0point75)"&gt;
  &lt;/div&gt;
  &lt;div class="Mtop(1point5)"&gt;
    &lt;label for="two" class="Mtop(0)"&gt;Label two&lt;/label&gt;
    &lt;input id="two" name="two" type="text" class="Mtop(0point75)"&gt;
  &lt;/div&gt;
  &lt;button type="submit" class="Mtop(1point5)"&gt;Submit&lt;/button&gt;
&lt;/form&gt;
</code></pre>

Bear in mind that this would only cover top margins if one is adhering to atomic CSS. You'd have to prescribe individual classes for <code>color</code>, <code>background-color</code> and a host of other properties, because atomic CSS does not leverage inheritance or element selectors.</p>

<pre><code class="language-html">
&lt;form class="Mtop(1point5) Bdc(#ccc) P(1point5)"&gt;
  &lt;div class="Mtop(0)"&gt;
    &lt;label for="one" class="Mtop(0) C(brandColor) Fs(bold)"&gt;Label one&lt;/label&gt;
    &lt;input id="one" name="one" type="text" class="Mtop(0point75) C(brandColor) Bdc(#fff) B(2) P(1)"&gt;
  &lt;/div&gt;
  &lt;div class="Mtop(1point5)"&gt;
    &lt;label for="two" class="Mtop(0) C(brandColor) Fs(bold)"&gt;Label two&lt;/label&gt;
    &lt;input id="two" name="two" type="text" class="Mtop(0point75) C(brandColor) Bdc(#fff) B(2) P(1)"&gt;
  &lt;/div&gt;
  &lt;button type="submit" class="Mtop(1point5) C(#fff) Bdc(blue) P(1)"&gt;Submit&lt;/button&gt;
&lt;/form&gt;
</code></pre>

Atomic CSS gives developers direct control over style without deferring completely to inline styles, which are not reusable like classes. By providing classes for individual properties, it reduces the duplication of declarations in the stylesheet.

However, it necessitates direct intervention in the markup to achieve these ends. This requires learning and being commiting to its verbose API, as well as having to write a lot of additional HTML code.

Instead, by styling arbitrary HTML elements and their spacial relationships, CSS 'methodology' becomes largely obsolete. You have the advantage of working with a unified design system, rather than an HTML system with a superimposed styling system to consider and maintain separately.

Anyway, here's how the structure of our CSS should look with our flow content solution in place:

1.  global (`html`) styles and enforced inheritance,
2.  flow algorithm and exceptions (using the lobotomized owl selector),
3.  element and attribute styles.

We've yet to write a specific component or conceive a CSS class, but a large proportion of our styling is done — that is, if we write our classes in a sensible, reusable fashion.</p>

## Utility Classes

The thing about classes is that they have a global scope: Anywhere they are applied in the HTML, they are affected by the associated CSS. For many, this is seen as a drawback, because two developers working independently could write a class with the same name and negatively affect each other's work.</p>

<a href="https://css-tricks.com/css-modules-part-1-need/">CSS modules</a> were recently conceived to remedy this scenario by programmatically generating unique class names tied to their local or component scope.</p>

<pre><code class="language-html">
&lt;!-- my module's button --&gt;
&lt;button class="button_dysuhe027653"&gt;Press me&lt;/button&gt;

&lt;!-- their module's button --&gt;
&lt;button class="button_hydsth971283"&gt;Hit me&lt;/button&gt;
</code></pre>

Ignoring the superficial ugliness of the generated code, you should be able to see where disparity between independently authored components can easily creep in: Unique identifiers are used to style similar things. The resulting interface will either be inconsistent or be consistent with much greater effort and redundancy.

There's no reason to treat common elements as unique. You should be styling the type of element, not the instance of the element. Always remember that the term "class" means "type of thing, of which there may be many." In other words, all classes should be utility classes: reusable globally.

Of course, in this example, a <code>.button</code> class is redundant anyway: we have the <code>button</code> element selector to use instead. But what if it was a special type of button? For instance, we might write a <code>.danger</code> class to indicate that buttons do destructive actions, like deleting data:

<pre><code class="language-css">
.danger {
  background: #c00;
  color: #fff;
}
</code></pre>

Because class selectors are higher in specificity than element selectors and of the same specificity as attribute selectors, any rules applied in this way will override the element and attribute rules further up in the style sheet. So, my danger button will appear red with white text, but its other properties — like padding, the focus outline, and the margin applied via the flow algorithm — will remain intact.</p>

<pre><code class="language-html">
&lt;button class="danger"&gt;delete&lt;/button&gt;
</code></pre>

Name clashes may happen, occasionally, if several people are working on the same code base for a long time. But there are ways of avoiding this, like, oh, I don't know, first doing a text search to check for the existence of the name you are about to take. You never know, someone may have solved the problem you're addressing already.</p>

### Local Scope Utilities

My favorite thing to do with utility classes is to set them on containers, then use this hook to affect the layout of child elements within. For example, I can quickly code up an evenly spaced, responsive, center-aligned layout for any elements:

<pre><code class="language-css">
.centered {
  text-align: center;
  margin-bottom: -1rem; /* adjusts for leftover bottom margin of children */
}

.centered &gt; * {
  display: inline-block;
  margin: 0 0.5rem 1rem;
}
</code></pre>

With this, I can center group list items, buttons, a combination of buttons and links, whatever. That's thanks to the use of the <code>&gt; *</code> part, which means that any immediate children of <code>.centered</code> will adopt these styles, in this scope, but inherit global and element styles, too.

And I've adjusted the margins so that the elements can wrap freely without breaking the vertical rhythm set using the <code>* + *</code> selector above it. It's a small amount of code that provides a generic, responsive layout solution by setting a local scope for arbitrary elements.

My tiny (93B minified) <a href="https://github.com/Heydon/fukol-grids">flexbox-based grid system</a> is essentially just a utility class like this one. It's highly reusable, and because it employs <code>flex-basis</code>, no breakpoint intervention is needed. I just defer to flexbox's wrapping algorithm.</p>

<pre><code class="language-css">
.fukol-grid {
  display: flex;
  flex-wrap: wrap;
  margin: -0.5em; /* adjusting for gutters */
}

.fukol-grid &gt; * {
  flex: 1 0 5em; /* The 5em part is the basis (ideal width) */
  margin: 0.5em; /* Half the gutter value */
}
</code></pre>

<figure><img loading="lazy" decoding="async" class="275111 size-full" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00e4c130-b5d5-450d-a718-a62647bee69b/logo-fukol.png" alt="css inheritance" width="299" height="152" /><br>
<figcaption>Fukol's distinctive logotype</figcaption></figure>

Using BEM, you'd be encouraged to place an explicit "element" class on each grid item:

<pre><code class="language-html">
&lt;div class="fukol"&gt; &lt;!-- the outer container, needed for vertical rhythm --&gt;
  &lt;ul class="fukol-grid"&gt;
    &lt;li class="fukol-grid__item"&gt;&lt;/li&gt;
    &lt;li class="fukol-grid__item"&gt;&lt;/li&gt;
    &lt;li class="fukol-grid__item"&gt;&lt;/li&gt;
    &lt;li class="fukol-grid__item"&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>

But there's no need. Only one identifier is required to instantiate the local scope. The items here are no more protected from outside influence than the ones in my version, targeted with <code>&gt; *</code> — <strong>nor should they be</strong>. The only difference is the inflated markup.

So, now we've started incorporating classes, but only generically, as they were intended. We're still not styling complex components independently. Instead, we're solving system-wide problems in a reusable fashion. Naturally, you will need to document how these classes are used in your comments.

Utility classes like these take advantage of CSS' global scope, the local scope, inheritance and the cascade simultaneously. The classes can be applied universally; they instantiate the local scope to affect just their child elements; they inherit styles <em>not</em> set here from the parent or global scope; <em>and</em> we've not overqualified using element or class selectors.

Here's how our cascade looks now:

1.  global (`html`) styles and enforced inheritance,
2.  flow algorithm and exceptions (using the lobotomized owl selector),
3.  element and attribute styles,
4.  generic utility classes.

Of course, there may never be the need to write either of these example utilities. The point is that, if the need does emerge while working on one component, the solution should be made available to all components. Always be thinking in terms of the system.</p>

### Component-Specific Styles

We've been styling components, and ways to combine components, from the beginning, so it's tempting to leave this section blank. But it's worth stating that any components not created from other components (right down to individual HTML elements) are necessarily over-prescribed. They are to components what IDs are to selectors and risk becoming anachronistic to the system.

In fact, a good exercise is to identify complex components ("molecules," "organisms") by ID only and try not to use those IDs in your CSS. For example, you could place <code>#login</code> on your log-in form component. You shouldn't have to use <code>#login</code> in your CSS with the element, attribute and flow algorithm styles in place, although you might find yourself making one or two generic utility classes that can be used in other form components.

If you <em>do</em> use <code>#login</code>, it can only affect that component. It's a reminder that you've moved away from developing a design system and towards the interminable occupation of merely pushing pixels.</p>

## Conclusion

When I tell folks that I don't use methodologies such as BEM or tools such as CSS modules, many assume I'm writing CSS like this:

<pre><code class="language-css">
header nav ul li {
  display: inline-block;
}

header nav ul li a {
  background: #008;
}
</code></pre>

I don't. A clear over-specification is present here, and one we should all be careful to avoid. It's just that BEM (plus OOCSS, SMACSS, atomic CSS, etc.) are not the only ways to avoid convoluted, unmanageable CSS.

In an effort to defeat specificity woes, many methodologies defer almost exclusively to the class selector. The trouble is that this leads to a proliferation of classes: cryptic ciphers that bloat the markup and that — without careful attention to documentation — can confound developers new to the in-house naming system they constitute.

By using classes prolifically, you also maintain a styling system that is largely separate from your HTML system. This misappropriation of 'separate concerns' can lead to redundancy or, worse, can encourage inaccessibility: it's possible to affect a visual style without affecting the accessible state along with it:

<pre><code class="language-html">
&lt;input id="my-text" aria-invalid="false" class="text-input--invalid" /&gt;
</code></pre>

In place of the extensive writing and prescription of classes, I looked at some other methods:

*   leveraging inheritance to set a precedent for consistency;
*   making the most of element and attribute selectors to support transparent, standards-based composition;
*   applying a code- and labor-saving flow layout system;
*   incorporating a modest set of highly generic utility classes to solve common layout problems affecting multiple elements.

All of these were put in service of creating a design <strong>system</strong> that should make writing new interface components easier and less reliant on adding new CSS code as a project matures. And this is possible not thanks to strict naming and encapsulation, but thanks to a distinct lack of it.

Even if you're not comfortable using the specific techniques I've recommended here, I hope this article has at least gotten you to rethink what components are. They're not things you create in isolation. Sometimes, in the case of standard HTML elements, they're not things you create at all. The more you compose components <em>from</em> components, the more accessible and visually consistent your interface will be, and with less CSS to achieve that end.

There's not much wrong with CSS. In fact, it's remarkably good at letting you do a lot with a little. We're just not taking advantage of that.

{{< signature "vf, al, il" >}}

