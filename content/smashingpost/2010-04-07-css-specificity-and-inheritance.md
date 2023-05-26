---
title: CSS Specificity And Inheritance
slug: css-specificity-and-inheritance
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80957ac4-7fde-4078-b0dd-9763645f25b8/css-tricks-illu-101.jpg
date: 2010-04-07T13:34:54.000Z
author: inayaili-de-leon
description: >-
  CSS’ barrier to entry is extremely low, mainly due to the nature of its
  syntax. Being clear and easy to understand, the syntax makes sense even to the
  inexperienced Web designer. It's so simple, in fact, that you could style a
  simple CSS-based website within a few hours of learning it.
categories:
  - Coding
  - CSS
  - Essentials
---
CSS’ barrier to entry is extremely low, mainly due to the nature of its syntax. Being clear and easy to understand, the syntax makes sense even to the inexperienced Web designer. It's so simple, in fact, that you could style a simple CSS-based website within a few hours of learning it.

But <strong>this apparent simplicity is deceitful</strong>. If after a few hours of work, your perfectly crafted website looks great in Safari, all hell might break loose if you haven’t taken the necessary measures to make it work in Internet Explorer. In a panic, you add hacks and filters where only a few tweaks or a different approach might do. Knowing how to deal with these issues comes with experience, with trial and error and with failing massively and then learning the correct way.

Understanding a few often overlooked concepts is also important. The concepts may be hard to grasp and look boring at first, but understanding them and knowing how to take advantage of them is important.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)
*   [!important CSS Declarations: How and When to Use Them](https://www.smashingmagazine.com/2010/11/the-important-css-declaration-how-and-when-to-use-it/)
*   [Challenging CSS Best Practices](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/)

{{% feature-panel %}}

Two of these concepts are <strong>specificity</strong> and <strong>inheritance</strong>. Not very common words among Web designers, are they? Talking about <code>border-radius</code> and <code>text-shadow</code> is a lot more fun; but specificity and inheritance are fundamental concepts that any person who wants to be good at CSS should understand. They will help you create clean, maintainable and flexible style sheets. Let’s look at what they mean and how they work.

The notion of a "<strong>cascade</strong>" is at the heart of CSS (just look at its name). It ultimately determines which properties will modify a given element. The cascade is tied to three main concepts: importance, specificity and source order. The cascade follows these three steps to determine which properties to assign to an element. By the end of this process, the cascade has assigned a <strong>weight</strong> to each rule, and this weight determines which rule takes precedence, when more than one applies.</p>

## 1\. Importance

Style sheets can have a few different sources:

1.  **User agent** For example, the browser’s default style sheet.
2.  **User** Such as the user’s browser options.
3.  **Author** This is the CSS provided by the page (whether inline, embedded or external)

By default, this is the order in which the different sources are processed, so the author’s rules will override those of the user and user agent, and so on.

There is also the <code>!important</code> declaration to consider in the cascade. This declaration is used to balance the relative priority of user and author style sheets. While author style sheets take precedence over user ones, if a user rule has <code>!important</code> applied to it, it will override even an author rule that also has <code>!important</code> applied to it.

Knowing this, let’s look at the final order, in <strong>ascending order of importance</strong>:

1.  User agent declarations,
2.  User declarations,
3.  Author declarations,
4.  Author `!important` declarations,
5.  User `!important` declarations.

This flexibility in priority is key because it allows users to override styles that could hamper the accessibility of a website. (A user might want a larger font or a different color, for example.)

## 2\. Specificity

Every CSS rule has a <strong>particular weight</strong> (as mentioned in the introduction), meaning it could be more or less important than the others or equally important. This weight defines which properties will be applied to an element when there are conflicting rules.

Upon assessing a rule's importance, the cascade attributes a specificity to it; if one rule is more specific than another, it overrides it.

If two rules share the same weight, source and specificity, <strong>the later one is applied</strong>.</p>

### 2.1 How to Calculate Specificity?

There are <strong>several ways to calculate</strong> a selector’s specificity.

The quickest way is to do the following. Add 1 for each element and pseudo-element (for example, <code>:before</code> and <code>:after</code>); add 10 for each attribute (for example, <code>[type=”text”]</code>), class and pseudo-class (for example, <code>:link</code> or <code>:hover</code>); add 100 for each ID; and add 1000 for an inline style.

Let’s calculate the specificity of the following selectors using this method:

*   `**p.note**` 1 class + 1 element = 11
*   `**#sidebar p[lang="en"]**` 1 ID + 1 attribute + 1 element = 111
*   `**body #main .post ul li:last-child**` 1 ID + 1 class + 1 pseudo-class + 3 elements = 123

A similar method, described in the W3C's specifications, is to start with a=0, b=0, c=0 and d=0 and replace the numbers accordingly:

*   a = 1 if the style is inline,
*   b = the number of IDs,
*   c = the number of attribute selectors, classes and pseudo-classes,
*   d = the number of element names and pseudo-elements.

Let’s calculate the specificity of another set of selectors:

*   `**<p style="color:#000000;">**` a=1, b=0, c=0, d=0 → 1000
*   `**footer nav li:last-child**` a=0, b=0, c=1, d=3 → 0013
*   `**#sidebar input:not([type="submit"])**` a=0, b=1, c=1, d=1 → 0111 _(Note that the negation pseudo-class doesn’t count, but the selector inside it does.)_

If you’d rather learn this in a <strong>more fun way</strong>, Andy Clarke drew a clever <a href="https://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html">analogy between specificity and Star Wars</a> back in 2005, which certainly made it easier for Star Wars fans to understand specificity. Another good explanation is "CSS Specificity for Poker Players," though slightly more complicated.

<img loading="lazy" decoding="async" class="37633" title="CSS: Specificity Wars" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce864ef8-6f75-4bbf-8bcf-26b3ea3a6627/starwars.jpg" alt="CSS: Specificity Wars" width="500" height="300" /><br>
<em>Andy Clarke's CSS Specificity Wars chart.</em>

Remember that non-CSS presentational markup is attributed with a specificity of 0, which would apply, for example, to the <code>font</code> tag.

Getting back to the <code>!important</code> declaration, keep in mind that using it on a shorthand property is the same as declaring all of its sub-properties as <code>!important</code> (even if that would revert them to the default values).

If you are using imported style sheets (<code>@import</code>) in your CSS, you have to declare them before all other rules. Thus, they would be considered as coming before all the other rules in the CSS file.

Finally, if two selectors turn out to have the same specificity, <strong>the last one will override</strong> the previous one(s).</p>

### 2.2 Making Specificity Work For You

If not carefully considered, specificity can come back to haunt you and lead you to unwittingly transform your style sheets into a complex hierarchy of unnecessarily complicated rules.

You can follow a few <strong>guidelines</strong> to avoid major issues:

*   When starting work on the CSS, use generic selectors, and add specificity as you go along;
*   Using advanced selectors doesn’t mean using unnecessarily complicated ones;
*   Rely more on specificity than on the order of selectors, so that your style sheets are easier to edit and maintain (especially by others).

A good rule of thumb can be found in Jim Jeffers’ article, “<a href="https://donttrustthisguy.com/2010/03/07/the-art-and-zen-of-writing-css/">The Art and Zen of Writing CSS</a>”:
<blockquote>Refactoring CSS selectors to be less specific is exponentially more difficult than simply adding specific rules as situations arise.</blockquote>

## 3\. Inheritance

A succinct and clear explanation of inheritance is in the <a href="https://www.w3.org/TR/css3-cascade/">CSS3 Cascading and Inheritance module</a> specifications (still in “Working draft” mode):
<blockquote cite="https://www.w3.org/TR/css3-cascade/#inheritance">Inheritance is a way of propagating property values from parent elements to their children.</blockquote>

Some CSS properties are inherited by the children of elements by default. For example, if you set the <code>body</code> tag of a page to a specific font, that font will be inherited by other elements, such as headings and paragraphs, without you having to specifically write as much. This is the magic of inheritance at work.

The CSS specification determines whether each property is inherited by default or not. <strong>Not all properties are inherited</strong>, but you can force ones to be by using the <code>inherit</code> value.</p>

### 3.1 Object-Oriented Programming Inheritance

Though beyond the scope of this article, CSS inheritance shouldn’t be confused with object-oriented programming (OOP) inheritance. Here is the definition of <a href="https://en.wikipedia.org/wiki/Inheritance_(computer_science)">OOP inheritance from Wikipedia</a>, and it makes clear that we are <em>not</em> talking about the same thing:
<blockquote>In object-oriented programming (OOP), inheritance is a way to form new classes […] using classes that have already been defined. Inheritance is employed to help reuse existing code with little or no modification. The new classes […] inherit attributes and behavior of the pre-existing classes. …</blockquote>

### 3.2 How Inheritance Works

When an element inherits a value from its parent, it is inheriting its computed value. What does this mean? Every CSS property goes through a four-step process when its value is being determined. Here’s an excerpt from the <a href="https://www.w3.org/TR/CSS2/cascade.html#value-stages">W3C specification</a>:
<blockquote>The final value of a property is the result of a four-step calculation: the value is determined through specification (the "specified value"), then resolved into a value that is used for inheritance (the "computed value"), then converted into an absolute value if necessary (the "used value"), and finally transformed according to the limitations of the local environment (the "actual value").</blockquote>

In other words:

1.  **Specified value** The user agent determines whether the value of the property comes from a style sheet, is inherited or should take its initial value.
2.  **Computed value** The specified value is resolved to a computed value and exists even when a property doesn’t apply. The document doesn’t have to be laid out for the computed value to be determined.
3.  **Used value** The used value takes the computed value and resolves any dependencies that can only be calculated after the document has been laid out (like percentages).
4.  **Actual value** This is the value used for the final rendering, after any approximations have been applied (for example, converting a decimal to an integer).

If you look at any CSS <strong>property’s specification</strong>, you will see that it defines its initial (or default) value, the elements it applies to, its inheritance status and its computed value (among others). For example, the <code>background-color</code> specification states the following:
<blockquote>Name: background-color
Value: &lt;color&gt;
Initial: transparent
Applies to: all elements
Inherited: no
Percentages: N/A
Media: visual
Computed value: the computed color(s)</blockquote>

Confusing? It can be. So, what do we need to understand from all this? And why is it relevant to inheritance?

Let’s go back to the first sentence of this section, which should make more sense now. <em>When an element inherits a value from its parent, it inherits its computed value</em>. Because the computed value exists even if it isn’t specified in the style sheet, a property can be inherited even then: the initial value will be used. So, you can make use of inheritance even if the parent doesn’t have a specified property.</p>

### 3.3 Using Inheritance

The most important thing to know about inheritance is that it’s there and how it works. If you ignore the jargon, inheritance is actually very straightforward.

Imagine you had to specify the <code>font-size</code> or <code>font-family</code> of every element, instead of simply adding it to the <code>body</code> element? That would cumbersome, which is why inheritance is so helpful.

Don’t break it by <strong>using the universal selector</strong> (<code>*</code>) with properties that inherit by default. Bobby Jack wrote an interesting post about this on his Five-Minute Argument blog. You don’t have to remember all of the properties that inherit, but you will in time.

Rarely does a CSS-related article not bring some kind of bad news about Internet Explorer. This article is no exception. IE supports the <code>inherit</code> value only from version 8, except for the <code>direction</code> and <code>visibility</code> properties. Great.</p>

## 4\. Using Your Tools

If you use tools like Firebug or Safari’s Web Inspector, you can see how a given cascade works, which selectors have higher specificity and how inheritance is working on a particular element.

For example, here below is <strong>Firebug</strong> in action, inspecting an element on the page. You can see that some properties are overridden (i.e. crossed out) by other more specific rules:

<img loading="lazy" decoding="async" class="37631" title="Firebug showing properties being overridden due to higher specificity" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deb72421-cfc5-427a-990f-003625036460/firebug.png" alt="Firebug showing properties being overridden due to higher specificity" width="399" height="329" /><br>
<em>Firebug in action, informing you how specificity is working.</em>

In the next shot, <strong>Safari’s Web Inspector</strong> shows the computed values of an element. This way, you can see the values even though they haven’t been explicitly added to the style sheet:

<img loading="lazy" decoding="async" class="37632" title="Safari Web Inspector showing computed values" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c1429c5-234e-4309-9847-c3d4e8b4e2f5/safari.png" alt="Safari Web Inspector showing computed values" width="474" height="278" /><br>
<em>With Safari's Web Inspector (and Firebug), you can view the computed values of a particular element.</em>

## 5\. Conclusion

Hopefully this article has opened your eyes to (or has refreshed your knowledge of) CSS inheritance and specificity. We encourage you to read the articles cited below, as well as <a href="https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/">Smashing Magazine’s previous article on the topic</a>.

Even if you don’t think about them, these issues are present in your daily work as a CSS author. Especially in the case of specificity, it’s important to know how they affect your style sheets and how to plan for them so that they cause only minimal (or no) problems.</p>

## Resources And Further Reading

*   [Assigning Property Values, Cascading, and Inheritance](https://www.w3.org/TR/CSS2/cascade.html), W3C
*   [CSS3: Cascading and Inheritance](https://www.w3.org/TR/css3-cascade/), W3C
*   [Selectors Level 3: Calculating a Selector's Specificity](https://www.w3.org/TR/css3-selectors/#specificity), W3C
*   [The Cascade](https://reference.sitepoint.com/css/cascade), SitePoint
*   [Inheritance and Cascade](https://maqentaer.com/devopera-static-backup/http/dev.opera.com/articles/view/28-inheritance-and-cascade/index.html), Dev.Opera
*   [CSS Inheritance](https://dorward.me.uk/www/css/inheritance/), Dorward Online
*   [Cascading Order and Inheritance in CSS](https://monc.se/kitchen/38/cascading-order-and-inheritance-in-css), David's Kitchen
*   [Understanding Style Precedence in CSS: Specificity, Inheritance, and the Cascade](https://www.vanseodesign.com/css/css-specificity-inheritance-cascaade/), Van SEO Design
*   [Specifics on CSS Specificity](https://css-tricks.com/specifics-on-css-specificity/), CSS-Tricks
*   [Link Specificity](https://meyerweb.com/eric/css/link-specificity.html), meyerweb.com
*   [Redundancy vs. Dependency](https://www.mezzoblue.com/archives/2005/01/20/redundancy_v/), mezzoblue

{{< signature "al" >}}

