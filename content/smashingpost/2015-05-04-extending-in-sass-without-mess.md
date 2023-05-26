---
title: Extending In Sass Without Creating A Mess
slug: extending-in-sass-without-mess
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c300031e-ed73-47d3-93cc-3e1187ff3a2c/excerpt-sass.jpg'
date: 2015-05-04T20:45:10.000Z
author: davidkhourshid
summary: >-
  The `@extend` directive is nothing to fear, and it’s very versatile. Understanding how `@extend` works and keeping the guidelines above in mind will enable you to use `@extend` to its full advantage.
description: >-
  The `@extend` directive is nothing to fear, and it’s very versatile. Understanding how `@extend` works and keeping the guidelines above in mind will enable you to use `@extend` to its full advantage.
categories:
  - Coding
  - Workflow
  - Optimization
  - Preprocessors
---
The `@extend` directive in Sass is a powerful directive that facilitates the sharing of rules and relationships between selectors. However, it can produce undesirable side effects if it is not carefully implemented. Thankfully, there are many strategies for using `@extend` effectively that can prevent these side effects and produce clean, organized CSS.

By examining `@extend` in detail and exploring these various strategies, you can accurately predict exactly **what happens when you use `@extend`**, and make more informed decisions about when to use a `@mixin` and when to use `@extend`, to ensure optimal organization and to restrict unused styles in your style sheets.

The `@extend` directive in Sass is a powerful directive that facilitates the sharing of rules and relationships between selectors. However, it can produce undesirable side effects if it is not carefully implemented.

Thankfully, there are many strategies for using `@extend` effectively that can prevent these side effects and produce clean, organized CSS.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Atomic Design With Sass](https://www.smashingmagazine.com/2013/08/other-interface-atomic-design-sass/)
*   [Smarter Grids With Sass And Susy](https://www.smashingmagazine.com/2015/07/smarter-grids-with-sass-and-susy/)
*   [Sassy Z-Index Management For Complex Layouts](https://www.smashingmagazine.com/2014/06/sassy-z-index-management-for-complex-layouts/)

By examining <code>@extend</code> in detail and exploring these various strategies, you can:

{{% feature-panel %}}

*   accurately predict exactly **what happens when you use `@extend`**,
*   and make more informed decisions about when to use a `@mixin` and when to use `@extend`, to ensure optimal organization and to restrict unused styles in your style sheets.</p>

## What Happens When You Use `@extend`?

<a href="https://sass-lang.com/documentation/file.SASS_REFERENCE.html#extend">Sass’ <code>@extend</code> directive</a> does much more than group extended selectors together, as the documentation suggests. Two main things happen when you <code>@extend</code> a selector:

*   the **target “[simple selector](https://dev.w3.org/csswg/selectors-4/#simple)”** is identified;
*   **constraints are formed** on the target selector using:
    *   the selector that’s doing the extending,
    *   and the selector that’s being extended.

Let’s break this down with an example. Consider the following code:

<div class="break-out">

<pre><code class="language-scss">.foo.bar { color: green; }

.ancestor .descendant { @extend .bar; } // .bar is being extended
</code></pre></div>

*   The target simple selector is identified as `.descendant`.
*   Two constraints are formed:
    *   `.bar` (and whatever extends it) must have the class `.foo` to be green,
    *   `.descendant` must be a descendant of `.ancestor`.

Using this information, the <code>@extend</code> directive produces this ruleset:

<pre><code class="language-scss">.foo.bar, .ancestor .foo.descendant { color: green; }
</code></pre>

The target selector <code>.descendant</code> now fulfills the constraint requirements: It has a class of <code>.foo</code>, and it is an ancestor of <code>.ancestor</code>.

Some common <code>@extend</code> scenarios are listed below. Notice the constraints (requirements) implicitly placed on the target selector and how these constraints are fulfilled in the outputted CSS:

<div class="break-out">

<pre><code class="language-scss">// Extending a selector with an ancestor
.first { color: green; }
.second { @extend .first; }
.ancestor .first { background: white; }

// CSS
.first, .second { color: green; }
.ancestor .first, .ancestor .second { background: white; }

// Extending a selector with a descendant
.first .descendant { color: green; }
.second { @extend .first; }

// CSS
.first .descendant, .second .descendant { color: green; }

// Extending a selector within a compound selector
.one.two { color: green; }
.three { @extend .one; }

// CSS
.one.two, .two.three { color: green; } 

// Extending a selector using a complex selector
.foo.bar { color: green; }
.complex .selector { @extend .bar; }

// CSS
.foo.bar, .complex .foo.selector { color: green; }

// Alternating ancestors
.ancestor-1 .foo { color: green; }
.ancestor-2 .bar { @extend .foo; }

// CSS
// Notice how the ancestors switch places to 
// maintain the general ancestral constraints
.ancestor-1 .foo,
.ancestor-1 .ancestor-2 .bar,
.ancestor-2 .ancestor-1 .bar {
  color: green;
}

// Combinator with common ancestor
.foo.bar + .sibling { color: green; }
.foo .descendant { @extend .sibling; }

// CSS
// Notice how .foo is repeated to preserve
// constraint of .foo.bar
.foo.bar + .sibling,
.foo .foo.bar + .descendant {
  color: green;
}
</code></pre></div>

There are a few takeaways from the examples above:

*   **Extending obeys selector constraints.**.  In the last example, `.descendant` is a sibling of `.foo.bar`, not `.foo`. It’s also a descendant of `.foo`, and since `.foo` can’t be both an ancestor and a sibling, it is outputted twice to maintain those respective constraints.
*   **Ancestor and descendant selectors are prone to permutation explosion.**.  Ancestors (in the form of `.ancestor .descendant`) can be anything from parents to grandparents and beyond. When selectors with ancestors extend other selectors with ancestors, all of these permutations must be accounted for.
*   **Extending is a one-way operation.**.  When `.bar` extends `.foo`, `.bar` is intimately aware of the relationships between `.foo` and its selectors, but not the other way around. And yes, selectors can reciprocally `@extend` each other.</p>

## Why Use `@extend`?

The <code>@extend</code> and <code>@mixin</code> directives are not exactly the same. Whereas a <code>@mixin</code> outputs rules that can be copied for multiple selectors and customized via parameters, <code>@extend</code> uses the mechanism described above for rule-sharing that allows it to serve three main purposes:

*   **inheritance** of rulesets between selectors that can be overridden by the extending selector;
*   **traits**, or shareable rulesets;
*   **relationships** between selectors that are maintained when a selector with a defined relationship is extended via combinators (for example, `>`, `+`, `~`, etc.).

## Strategies And Guidelines For `@extend`

Now that we know how to use <code>@extend</code> and what exactly causes selector explosion, let’s look at some strategies we can implement to properly share styles across selectors.</p>

### Use and Extend `%placeholder` Selectors.

Sass includes a special type of selector called the placeholder selector that is quite literally <a href="https://sass-lang.com/documentation/file.SASS_REFERENCE.html#placeholder_selectors_">meant to be used with <code>@extend</code></a>. These are very versatile selectors in that they:

*   **can be extended**, of course;
*   **are ignored in CSS output**, which can prevent unnecessary output;
*   **can be dynamically declared** just like any other selector in Sass, meaning you can `%do-#{$this}`, which gives it a leg up on non-dynamic mixins.

When you <code>@extend %placeholders</code>, the explosive side effects are lessened because you have one less shared selector to combine with in the final CSS output.</p>

### Extend a Selector as Few Times as Possible.

Consider the following example of <strong>inheritance</strong> by extending a parent (placeholder) selector:

<pre><code class="language-scss">// Don't do this:

%button {
  // … parent button styles
}

.button {
  @extend %button;
  // … button styles
}

.button-primary {
  @extend %button;
  // … primary button styles
}

.button-secondary {
  @extend %button;
  // … secondary button styles
}

// CSS - we want to avoid this:
.button, .button-primary, .button-secondary {
  // button styles
}

.button-primary { /* … */ }
.button-secondary { /* … */ }
</code></pre>

When extending the same selector multiple times, ask yourself, What do all these extending selectors have in common? Then, you can <strong>limit how often a selector is extended</strong> by refactoring using a <strong>common selector</strong>, such as <code>.button.primary</code>, instead of <code>.button-primary</code>, so that the only extension is <code>.button { @extend %button; }</code>.</p>

### Extend Traits Selectively, and Consider Mixins for Short Traits.

The previous strategy can be difficult to accomplish with <strong>traits</strong>, which by definition can be shared among many selectors that are otherwise unrelated. Traits, in general, <strong>do not have hierarchical constraints</strong>; that is, they (usually) are agnostic to the relationship between the selector using it and other selectors. Therefore, they <strong>can be used with <code>@extend</code> or <code>@mixin</code></strong>.

I would (personally) choose to <code>@extend</code> a trait with many rules. The outputted CSS <strong>will group unrelated selectors with the trait ruleset</strong>, although this isn’t a huge concern — style sheet maintenance occurs in your <code>.sass</code> or <code>.scss</code> files, not your <code>.css</code> files, and there are few performance trade-offs, in general.

On the other hand, I would use <code>@mixin</code> for rulesets that are terse and frequently used, such as <code>clearfix</code>. Extending it would cause the CSS to output a large number of selectors for this small trait. Using it as a mixin will make the outputted CSS much more readable, and repetition is OK because the ruleset is small.

So, here are some general guidelines for using traits:

*   **Extend traits that have long rulesets or are infrequently used.**.  This keeps your outputted CSS DRY and helps to group rulesets in your CSS for increased clarity in browser debugging.
*   **Mixin traits that are more generalized, short and frequently used.**.  You can `@extend` these types of traits, but you’re more at risk of selector explosion.
*   **Stick repeated rulesets in a `%placeholder` trait or a `@mixin`.** This is just a general good practice to keep your SCSS as DRY as possible.</p>

### Use `@extend` for Relationships.

This is one of the most important uses of <code>@extend</code>. Relationships between selectors in your style sheets can get quite complex, and <code>@extend</code> is the perfect tool for the job — <strong>you cannot express relationships with <code>@mixin</code> alone.</strong> A relationship between selectors is expressed with a <a href="https://dev.w3.org/csswg/selectors-4/#combinator">combinator</a>, such as <code>&gt;</code>, <code>+</code>, <code>~</code> or the white space ancestor combinator. Many different types of relationship can exist in CSS, even not-so-obvious ones:

*   `.parent > .child`
*   `.ancestor .descendant`
*   `.sibling ~ .sibling`
*   `.sibling + .adjacent-sibling`
*   `.sibling + * ~ .non-adjacent-sibling`
*   `.parent > * > .grandchild`
*   `.parent > * .non-child-descendant`
*   `.uncle ~ * > .nephew`
*   `* + *`, the any-adjacent-sibling relationship, or the [lobotomized owl selector](https://alistapart.com/article/axiomatic-css-and-lobotomized-owls)

CSS enables us to define styles for selectors based on their relationships with other selectors. These relationship-defining selectors that use combinators are called <strong>complex selectors</strong>, and they have higher specificity than their standalone simple or compound selector parts. Styles defined as a relationship, therefore, have greater prevalence than styles defined in standalone selectors.

The following strategies address how to extend with relationships in depth.</p>

### Define Relationships via Placeholders, Not Classes.

Remember what happens when you have two ancestral relationships (such as <code>.foo .bar {…} .baz .qux { @extend .bar; }</code>)? Being aware that multiple extended ancestral relationships are prone to selector explosion, we should <strong>always define our relationships once</strong>, and keep them one-sided. And what better place to define relationships than in <code>%placeholder</code> selectors, to reduce CSS output?

Let’s say you want buttons to be styled a little differently in modals, and you want a little space between adjacent buttons. Here’s how that relationship would look like using placeholders:

<pre><code class="language-scss">%button {
  // … button styles

  + %button {
    margin-left: 1rem;
  }
}

%modal {
  // … modal styles

  %button {
    // … modal-specific button styles
  }
}

// "Exported" classes
.button { @extend %button; }
.modal { @extend %modal; }
</code></pre>

Notice that two relationships are defined: the sibling <code>%button + %button</code> relationship and the ancestral <code>%modal %button</code> relationship. These relationships are <strong>defined only once</strong> in the placeholders, and the outputted CSS is exactly what we’d expect:

<pre><code class="language-scss">.button { /* … button styles */ }
.button + .button { margin-left: 1rem; }

.modal { /* … modal styles */ }
.modal .button { /* … modal-specific button styles */ }
</code></pre>

### Represent One Selector Per Placeholder in Relationships.

This follows the first strategy: Extend a selector as few times as possible. When writing markup and CSS selectors, having as few selectors represent an entity as possible will prevent selector explosion, even if it means you have to add a semantic class to the markup to eliminate selectors.

<pre><code class="language-scss">%button { // … button styles }

// Avoid this:
button, input[type="button"], input[type="submit"], .button {
  @extend %button;
}

// Try this instead, and add the class .button
// for every type of button in the HTML
.button {
  @extend %button;
}
</code></pre>

### Be Wary of Descendant and General Sibling Combinators.

These two combinators — <code>.ancestor .descendant</code> and <code>.sibling ~ .general-sibling</code>, respectively — are the most prone to selector explosion. Why? Their constraints are <strong>less strict</strong> than other combinators. A descendant can be a child, grandchild, etc. A general sibling can be adjacent, one ahead, two ahead, etc.

If two complex selectors <em>both</em> have descendant or general sibling combinators, then all possibilities must be accounted for in the outputted CSS. That’s why you should make sure that <strong>only the extendee or extender</strong> has a descendant or general sibling combinator, not both. Following the guidelines above on extending only from <code>%placeholders</code> is a good way to enforce this.

<pre><code class="language-scss">%modal {
  // … modal styles

  // Relationship: a %button that is a descendant of %modal
  %button { /* … modal-button styles */ }
}

// Don't do this!
.modal {
  @extend %modal;

  // This is unnecessary - the relationship
  // is already defined!
  .button { @extend %button; }
}

// Do this - keep it simple!
.modal { @extend %modal; }
.button { @extend %button; }
</code></pre>

### Have Separate Placeholders for Modifiers.

By having separate <code>%placeholders</code> to represent modified components, you can extend without the risk of confounding compound and/or complex selectors. For example, <code>@extend %button%active;</code> is risky, but <code>@extend %button-active;</code> is not.

<pre><code class="language-scss">%button {
  // … button styles

  &amp;-active { // same as %button-active
    // … active button styles
  }

  &amp;-disabled {
    // … disabled button styles
  }
}

.button {
  @extend %button;

  &amp;.active { @extend %button-active; }
  &amp;:disabled { @extend %button-disabled; }
}
</code></pre>

### Use `@extend` Inside Similar Media Queries.

You’re probably thinking, “I thought that using <code>@extend</code> in media queries is currently not possible.” This is partially true, but also slightly misleading. The truth is that you can only extend a selector in the <em>same</em> media query, and, for all intents and purposes, this is sufficient.

What is important, however, is that your selectors are <strong>meaningful</strong>, in that you can declare them with proper intent. If you are trying to extend an outside selector inside a media query, that’s a clear conflict of interests — one selector’s intent is to be generally applied, while the other’s intent is to be applied only within the current media context.

For instance, the SCSS below will not work because of the media query restriction and, more importantly, because the <strong>intent is not clear</strong>:

<pre><code class="language-scss">%panel {
  display: block;
  float: left;
  width: 100%;
  // … other panel styles
}

%panel-half { width: 50%; }

.panel {
  @extend %panel;

  &amp;.half { @extend %panel-half; }
}

// This will NOT work and will throw this error:
// You may not @extend an outer selector from within @media.
// You may only @extend selectors within the same directive.
@media (max-width: 700px) {
  .panel-mobile {
    @extend %panel;

    &amp;.half { @extend %panel-half; }
  }
}
</code></pre>

So, what went wrong here? In defining <code>%panel</code>, the intent was, “This panel should have this styling in general,” whereas we were trying to export <code>.panel-mobile</code> as “This panel should have this styling only in this media query context.” This is a clear miscommunication.

The solution to this is to match extendee intent with extender intent, especially regarding <code>@media</code> queries. In other words, if you want an extender to carry certain styling only for a specific media query, it should extend only within the same <code>@media</code> query or, alternatively, break out of the <code>@media</code> query with <code>@at-root</code>.

Let’s see how we can revise our code with the above two suggestions:

<div class="break-out">

<pre><code class="language-scss">// Solution 1: Extend within the same media query
%panel { /* … */ }
%panel-half { /* … */ }

// Define extendees with the same intent as extenders
@media (max-width: 700px) {
  %panel-mobile { /* … */ }
  %panel-mobile-half { /* … */ }
}

.panel {
  @extend %panel; 

  &amp;.half { @extend %panel-half; }
</code></pre></div>

The following strategies address how to extend with relationships in depth.</p>

### Define Relationships via Placeholders, Not Classes.

Remember what happens when you have two ancestral relationships (such as <code>.foo .bar {…} .baz .qux { @extend .bar; }</code>)? Being aware that multiple extended ancestral relationships are prone to selector explosion, we should <strong>always define our relationships once</strong>, and keep them one-sided. And what better place to define relationships than in <code>%placeholder</code> selectors, to reduce CSS output?

Let’s say you want buttons to be styled a little differently in modals, and you want a little space between adjacent buttons. Here’s how that relationship would look like using placeholders:

<pre><code class="language-scss">%button {
  // … button styles

  + %button {
    margin-left: 1rem;
  }
}

%modal {
  // … modal styles

  %button {
    // … modal-specific button styles
  }
}

// "Exported" classes
.button { @extend %button; }
.modal { @extend %modal; }
</code></pre>

Notice that two relationships are defined: the sibling <code>%button + %button</code> relationship and the ancestral <code>%modal %button</code> relationship. These relationships are <strong>defined only once</strong> in the placeholders, and the outputted CSS is exactly what we’d expect:

<pre><code class="language-scss">.button { /* … button styles */ }
.button + .button { margin-left: 1rem; }

.modal { /* … modal styles */ }
.modal .button { /* … modal-specific button styles */ }
</code></pre>

### Represent One Selector Per Placeholder in Relationships.

This follows the first strategy: Extend a selector as few times as possible. When writing markup and CSS selectors, having as few selectors represent an entity as possible will prevent selector explosion, even if it means you have to add a semantic class to the markup to eliminate selectors.

<pre><code class="language-scss">%button { // … button styles }

// Avoid this:
button, input[type="button"], input[type="submit"], .button {
  @extend %button;
}

// Try this instead, and add the class .button
// for every type of button in the HTML
.button {
  @extend %button;
}
</code></pre>

### Be Wary of Descendant and General Sibling Combinators.

These two combinators — <code>.ancestor .descendant</code> and <code>.sibling ~ .general-sibling</code>, respectively — are the most prone to selector explosion. Why? Their constraints are <strong>less strict</strong> than other combinators. A descendant can be a child, grandchild, etc. A general sibling can be adjacent, one ahead, two ahead, etc.

If two complex selectors <em>both</em> have descendant or general sibling combinators, then all possibilities must be accounted for in the outputted CSS. That’s why you should make sure that <strong>only the extendee or extender</strong> has a descendant or general sibling combinator, not both. Following the guidelines above on extending only from <code>%placeholders</code> is a good way to enforce this.

<pre><code class="language-scss">%modal {
  // … modal styles

  // Relationship: a %button that is a descendant of %modal
  %button { /* … modal-button styles */ }
}

// Don't do this!
.modal {
  @extend %modal;

  // This is unnecessary - the relationship
  // is already defined!
  .button { @extend %button; }
}

// Do this - keep it simple!
.modal { @extend %modal; }
.button { @extend %button; }
</code></pre>

### Have Separate Placeholders for Modifiers.

By having separate <code>%placeholders</code> to represent modified components, you can extend without the risk of confounding compound and/or complex selectors. For example, <code>@extend %button%active;</code> is risky, but <code>@extend %button-active;</code> is not.

<pre><code class="language-scss">%button {
  // … button styles

  &amp;-active { // same as %button-active
    // … active button styles
  }

  &amp;-disabled {
    // … disabled button styles
  }
}

.button {
  @extend %button;

  &amp;.active { @extend %button-active; }
  &amp;:disabled { @extend %button-disabled; }
}
</code></pre>

### Use `@extend` Inside Similar Media Queries.

You’re probably thinking, “I thought that using <code>@extend</code> in media queries is currently not possible.” This is partially true, but also slightly misleading. The truth is that you can only extend a selector in the <em>same</em> media query, and, for all intents and purposes, this is sufficient.

What is important, however, is that your selectors are <strong>meaningful</strong>, in that you can declare them with proper intent. If you are trying to extend an outside selector inside a media query, that’s a clear conflict of interests — one selector’s intent is to be generally applied, while the other’s intent is to be applied only within the current media context.

For instance, the SCSS below will not work because of the media query restriction and, more importantly, because the <strong>intent is not clear</strong>:

<pre><code class="language-scss">%panel {
  display: block;
  float: left;
  width: 100%;
  // … other panel styles
}

%panel-half { width: 50%; }

.panel {
  @extend %panel;

  &amp;.half { @extend %panel-half; }
}

// This will NOT work and will throw this error:
// You may not @extend an outer selector from within @media.
// You may only @extend selectors within the same directive.
@media (max-width: 700px) {
  .panel-mobile {
    @extend %panel;

    &amp;.half { @extend %panel-half; }
  }
}
</code></pre>

So, what went wrong here? In defining <code>%panel</code>, the intent was, “This panel should have this styling in general,” whereas we were trying to export <code>.panel-mobile</code> as “This panel should have this styling only in this media query context.” This is a clear miscommunication.

The solution to this is to match extendee intent with extender intent, especially regarding <code>@media</code> queries. In other words, if you want an extender to carry certain styling only for a specific media query, it should extend only within the same <code>@media</code> query or, alternatively, break out of the <code>@media</code> query with <code>@at-root</code>.

Let’s see how we can revise our code with the above two suggestions:

<pre><code class="language-scss">// Solution 1: Extend within the same media query
%panel { /* … */ }
%panel-half { /* … */ }

// Define extendees with the same intent as extenders
@media (max-width: 700px) {
  %panel-mobile { /* … */ }
  %panel-mobile-half { /* … */ }
}

.panel {
  @extend %panel; 

  &amp;.half { @extend %panel-half; }

  // This WILL work!
  @media (max-width: 700px) {
    &amp;-mobile {
      @extend %panel-mobile;

      &amp;.half { @extend %panel-mobile-half; }
    }
  }
}
</code></pre>

<pre><code class="language-scss">// Solution 2: Break out of '@media' with '@at-root'
%panel {
  display: block;
  float: left;
  // … other panel styles
}

// Separation of intent
%panel-full { width: 100%; }
%panel-half { width: 50%; }

@media (max-width: 700px) {
  %panel-mobile-full { width: 100%; }
  %panel-mobile-half { width: 50%; }
}

.panel {
  @extend %panel;

  &amp;.half { @extend %panel-half; }

  @media (max-width: 700px) {
    &amp;-mobile, &amp;-mobile-half {
      // General panel styling intent is maintained
      @at-root (without: media) { @extend %panel; }
    }

    &amp;-mobile {
      @extend %panel-mobile-full;

      &amp;.half { @extend %panel-mobile-half; }
    }
  }
} 
</code></pre>

### Use `@extend` With `:matches()` in the Future.

Sometimes, it’s difficult to adhere to the guideline that you should <code>@extend</code> a selector as few times as possible. Take the HTML headings, for instance: <code>h1, h2, h3, h4, h5, h6</code>. There are six of them, and they all can’t be selected with a single simple selector. One solution would be to give them all a class of <code>.heading</code>, but if you’re building for the future, there’s a better way.

Enter <a href="https://dev.w3.org/csswg/selectors-4/#matches-pseudo">CSS 4’s <code>:matches()</code> pseudoselector</a>. This selector allows you to somewhat mimic <code>@extend</code> functionality in native CSS, without the selector explosion (which we’ve learned how to avoid). The best part is, Sass plays nicely with <code>:matches()</code> and related pseudoselectors. Let’s style our headings to demonstrate:

<pre><code class="language-scss">// With :matches()
:matches(%heading) {
  // … heading styles
}

// Relationship: any heading that is a descendant of %section-foo
%section-foo :matches(%heading) { /* … */ }

h1, h2, h3, h4, h5, h6 {
  @extend %heading;
}

.section-foo { @extend %section-foo; }

// CSS output - much better than this selector explosion:
// .section-foo h1, .section-foo h2, .section-foo h3, .section-foo h4, .section-foo h5, .section-foo h6
.section-foo :matches(h1, h2, h3, h4, h5, h6) {
  // … section-foo heading style
}
</code></pre>

Today, you’ll have to use <code>:-webkit-any()</code> and <code>:moz-any()</code> in place of <code>:matches()</code> in WebKit browsers and Firefox, respectively, until they natively support <code>:matches()</code>. With Internet Explorer, you’re out of luck (no surprise there). This is a good guideline to keep in the back of your mind until CSS 4 is implemented in all modern browsers.</p>

## Conclusion

The <code>@extend</code> directive is nothing to fear, and it’s very versatile. Understanding how <code>@extend</code> works and keeping the guidelines above in mind will enable you to use <code>@extend</code> to its full advantage — reducing CSS output and keeping relationships intact, no matter what exported selectors (classes, attributes, etc.) you use. Make wise use of both the <code>@mixin</code> and <code>@extend</code> directives — they’re meant to coexist in your well-organized style sheets.

{{< signature "rb, al, ml" >}}
