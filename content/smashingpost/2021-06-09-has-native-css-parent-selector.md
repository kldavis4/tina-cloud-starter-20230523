---
title: 'Meet <code>:has</code>, A Native CSS Parent Selector (And More)'
slug: has-native-css-parent-selector
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89aef48d-9be9-45df-a7f4-775168deb8dd/has-native-css-parent-selector.jpg
date: 2021-06-09T10:30:00.000Z
summary: >-
  What makes relational selector one of the most requested features and how are we, as developers, working around not having it? In this article, we’re going to check the early spec of the <code>:has</code> selector, and see how it should improve the CSS workflow once it’s released.
description: >-
  What makes relational selector one of the most requested features and how are we, as developers, working around not having it? In this article, we’re going to check the early spec of the <code>:has</code> selector, and see how it should improve the CSS workflow once it’s released.
categories:
  - CSS
  - Tools
  - Workflow
---

Parent selector has been on developers’ wishlist for [more than 10 years](https://remysharp.com/2010/10/11/css-parent-selector/) and it has become one of the most requested CSS features alongside container queries ever since. The main reason this feature wasn’t implemented all this time seems to be due to [performance concerns](https://snook.ca/archives/html_and_css/css-parent-selectors). The same was being said about the [container queries](https://www.smashingmagazine.com/2021/05/css-container-queries-use-cases-migration-strategies/) and those are currently being added to beta versions of browsers, so those performance seems to be no longer an issue. 

Browser render engines have improved quite a bit since then. The rendering process has been optimized to the point that browsers can effectively determine what needs to be rendered or updated and what doesn’t, opening the way for a new and exciting set of features.

[Brian Kardell has recently announced](https://bkardell.com/blog/canihas.html) that his team at Igalia is currently prototyping a `:has` selector that will serve as a parent selector, but it could have a much wider range of use-cases beyond it. The developer community refers to it as a **“parent selector”** and some [developers have pointed out](https://twitter.com/NOVALISTIC/status/1393506232107814915) that the name isn’t very accurate. A more fitting name would be a relational selector or relational pseudo-class [as per specification](https://drafts.csswg.org/selectors-4/#relational), so I’ll be referring to `:has` as such from now on in the article.

The team at Igalia has worked on some notable web engine features like [CSS grid](https://www.smashingmagazine.com/2020/01/understanding-css-grid-container/) and [container queries](https://www.smashingmagazine.com/2021/05/css-container-queries-use-cases-migration-strategies/), so there is a chance for `:has` selector to see the light of day, but there is still a long way to go.

What makes relational selector one of the most requested features in the past few years and how are the developers working around the missing selector? In this article, we’re going to answer those questions and check out the early spec of **`:has` selector** and see how it should improve the styling workflow once it’s released.

## Potential Use-Cases

The relational selector would be useful for **conditionally applying styles** to UI components based on the content or state of its children or its succeeding elements in a DOM tree. Upcoming relational selector prototype could extend the range and use-cases for existing selectors, improve the quality and robustness of CSS and reduce the need for using JavaScript to apply styles and CSS classes for those use-cases.

Let’s take a look at a few specific examples to help us illustrate the variety of potential use-cases.

### Content-Based Variations

Some UI elements can have **multiple variations** based on various aspects &mdash; content, location on the page, child state, etc. In those cases, we usually create multiple CSS classes to cover all the possible variations and apply them manually or with JavaScript, depending on the approach and tech stack.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0f8719-0588-4cf1-95bf-82413982d314/1-meet-has-native-css-parent-selector.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0f8719-0588-4cf1-95bf-82413982d314/1-meet-has-native-css-parent-selector.jpg" width="800" height="309" sizes="100vw" caption="Four card variations depending on the content. Parent card container layout depends on the content and the card image container is styled differently depending on if the image container has an image caption present or not. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0f8719-0588-4cf1-95bf-82413982d314/1-meet-has-native-css-parent-selector.jpg'>Large preview</a>)" alt="Four card variations depending on the content. Parent card container layout depends on the content and the card image container is styled differently depending on if the image container has an image caption present or not." >}}

Even when using CSS naming methodology like [BEM](https://getbem.com/), developers need to keep track of the various CSS classes and make sure to apply them correctly to the parent element and, optionally, to affected child elements. Depending on the number of variations, component styles can get out of hand quickly and become difficult to manage and maintain leading to bugs, so developers would need to document all variations and use-cases by using tools like [Storybook](https://storybook.js.org/).

With a relational CSS selector, developers would be able to write content checks directly in CSS and styles would be applied automatically. This would reduce the amount of variation CSS classes, decrease the possibility of bugs caused by human error, and selectors would be self-documented with the condition checks.

### Validation-Based Styles

CSS supports input pseudo-classes like `:valid` and `:invalid` to target elements that successfully validate and elements that unsuccessfully validate, respectfully. Combined with HTML input attributes like `pattern` and `required`, it enables native form validation without the need to rely on JavaScript.

However, targeting elements with `:valid` and `:invalid` is limited to targeting the element itself or its adjacent element. Depending on the design and HTML structure, input container elements or preceding elements like `label` elements also need some style to be applied.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa90717-11c2-426d-8175-cd8ffac54b6b/meet-has-native-css-parent-selector-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa90717-11c2-426d-8175-cd8ffac54b6b/meet-has-native-css-parent-selector-2.png" width="800" height="391" sizes="100vw" caption="Individual email input containers change styles based on the validity of the email input state. When all inputs are successfully validated, the submit button (located right after the final input container in the DOM) is enabled. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa90717-11c2-426d-8175-cd8ffac54b6b/meet-has-native-css-parent-selector-2.png'>Large preview</a>)" alt="Individual email input containers change styles based on the validity of the email input state. When all inputs are successfully validated, the submit button (located right after the final input container in the DOM) is enabled." >}}

The relational selector would extend the use-case for the input state pseudo-classes like `:valid` and `:invalid` by allowing the parent element or preceding elements to be styled based on the input validity.

This doesn’t apply only to those pseudo-classes. When working with an external API that returns error messages that are appended in the input container, there won’t be a need to also apply the appropriate CSS class to the container. By writing a relational selector with a condition that checks if the child message container is empty, appropriate styles can be applied to the container.

{{% feature-panel %}} 

### Children Element State

Sometimes a parent element or preceding element styles depend on the state of a target element. This case is different from the validation state because the state isn’t closely related to the validity of the input.

Just like in the previous example, `:checked` pseudo-class for checkbox and radio input elements is limited to targeting the element itself or its adjacent element. This is not limited to pseudo-classes like `:checked`, `:disabled`, `:hover`, `:visited`, etc. but to anything else that CSS selectors can target like the availability of specific element, attribute, CSS class, id, etc.

Relation selectors would extend the range and use-cases of CSS selectors beyond the affected element or its adjacent element.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a1654ca-1559-40ed-a9df-031390aee3b6/3-meet-has-native-css-parent-selector.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a1654ca-1559-40ed-a9df-031390aee3b6/3-meet-has-native-css-parent-selector.jpg" width="800" height="400" sizes="100vw" caption="When one or more checkboxes in the filter dropdown are checked, the button changes the icon to indicate the active filter state in the group. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a1654ca-1559-40ed-a9df-031390aee3b6/3-meet-has-native-css-parent-selector.jpg'>Large preview</a>)" alt="When one or more checkboxes in the filter dropdown are checked, the button changes the icon to indicate the active filter state in the group." >}}

### Selecting Previous Siblings

CSS selectors are limited by the selection direction &mdash; child descendant or following element can be selected, but not the parent or preceding element.

A relational selector could also be used as a **previous sibling selector**.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f556614-86a8-4999-91df-34ed199dba7f/4-meet-has-native-css-parent-selector.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f556614-86a8-4999-91df-34ed199dba7f/4-meet-has-native-css-parent-selector.png" width="800" height="546" sizes="100vw" caption="Floating label input example from Google Material UI. Label (previous sibling) is styled based on the input’s focus and value state. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f556614-86a8-4999-91df-34ed199dba7f/4-meet-has-native-css-parent-selector.png'>Large preview</a>)" alt="Floating label input example from Google Material UI. Label (previous sibling) is styled based on the input’s focus and value state." >}}

### Advanced `:empty` Selector

When working with dynamically loaded elements and using skeleton loaders, it’s common to toggle a loading CSS class on the parent element with JavaScript once the data is fetched and components are populated with data.

Relational selector could eliminate the need for JavaScript CSS class toggle function by extending the range and functionality of `:empty` pseudo-class. With relational selector, necessary conditions to display an element can be defined in CSS by targeting required data HTML elements and checking if it’s populated with data. This approach should work with deeply nested and complex elements.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c6c300b-0b0d-4872-a055-a0e78098ed65/5-meet-has-native-css-parent-selector.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c6c300b-0b0d-4872-a055-a0e78098ed65/5-meet-has-native-css-parent-selector.jpg" width="800" height="423" sizes="100vw" caption="Skeleton placeholder is shown on parent until all data containers (deeply nested paragraph elements) are populated with data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c6c300b-0b0d-4872-a055-a0e78098ed65/5-meet-has-native-css-parent-selector.jpg'>Large preview</a>)" alt="Skeleton placeholder is shown on parent until all data containers (deeply nested paragraph elements) are populated with data." >}}

{{% ad-panel-leaderboard %}}

## CSS `:has` Pseudo-Class Specification

Keep in mind that `:has` is [not supported in any browsers](https://caniuse.com/css-has) so the code snippets related to the upcoming pseudo-class won’t work. Relational pseudo-class is defined in selectors level 4 specification which has been updated since its initial release in 2011, so the specification is already well-defined and ready for prototyping and development.

That being said, let’s dive into the `:has` pseudo-class specification. The idea behind the pseudo-class is to apply styles to a selector if the condition (defined as a regular CSS selector) has been met.

<div class="break-out">

<pre><code class="language-css">/&#42; Select figure elements that have a figcaption as a child element &#42;/
figure:has(figcaption) { /&#42; ... &#42;/ }

/* Select button elements that have an element with .icon class as a child &#42;/
button:has(.icon) { /&#42; ... &#42;/ }

/* Select article elements that have a h2 element followed by a paragraph element &#42;/
article:has(h2 + p) { /&#42; ... &#42;/ }
</code></pre>
</div>

Similar to the other pseudo-classes like `:not`, relational pseudo selector consists of the following parts.

<pre><code class="language-css">&lt;target_element&gt;:has(&lt;selector&gt;) { /* ... */ }
</code></pre>

- `<target_element>`  
Selector for an element that will be targeted if condition passed as an argument to `:has` pseudo-class has been met. Condition selector is scoped to this element.
- `<selector>`  
A condition defined with a CSS selector that needs to be met for styles to be applied to the selector.

Like with most pseudo-classes, selectors can be chained to target child elements of a target element or adjacent element.

<div class="break-out">

<pre><code class="language-css">/&#42; Select image element that is a child of a figure element if figure element has a figcaption as a child */
figure:has(figcaption) img { /&#42; ... &#42;/ }

/&#42; Select a button element that is a child of a form element if a child checkbox input element is checked &#42;/
form:has(input[type="checkbox"]:checked) button { /&#42; ... &#42;/ }
</code></pre>
</div>

From these few examples, it is obvious how versatile, powerful and useful the `:has` pseudo-class is. It can even be **combined with other pseudo-classes** like `:not` to create complex relational selectors.

<div class="break-out">

<pre><code class="language-css">/&#42; Select card elements that do not have empty elements &#42;/
.card:not(:has(&#42;:empty)) { /&#42; ... &#42;/ }

/&#42; Select form element that where at least one checkbox input is not checked &#42;/
form:has(input[type="checkbox"]:not(:checked)) { /&#42; ... &#42;/ }
</code></pre>
</div>

The relational selector is not limited to the target element’s children content and state, but can also target adjacent elements in the DOM tree, effectively making it a “previous sibling selector”.

<div class="break-out">

<pre><code class="language-css">/&#42; Select paragraph elements which is followed by an image element &#42;/
p:has(+img) { /&#42; ... &#42;/ }

/* Select image elements which is followed by figcaption element that doesn't have a "hidden" class applied &#42;/
img:has(&#126;figcaption:not(.hidden)) { /&#42; ... &#42;/ }

/&#42; Select label elements which are followed by an input element that is not in focus &#42;/
label:has(&#126;input:not(:focus)) { /&#42; ... &#42;/ }
</code></pre>
</div>

In a nutshell, **relational selector anchors the CSS selection to an element with** `:has` **pseudo-class and prevents selection** to move to the elements that are passed as an argument to the pseudo-class.

<pre><code class="language-javascript">.card .title .icon -> .icon element is selected
.card:has(.title .icon) -&gt; .card element is selected

.image + .caption -&gt; .caption element is selected
.image:has(+.caption) -&gt; .image element is selected
</code></pre>

{{% ad-panel-leaderboard %}}

## Current Approach And Workarounds

Developers currently have to use various workarounds to compensate for the missing relational selector. Regardless of the workarounds and as discussed in this article, it’s evident how impactful and game-changing the relational selector would be once released.

In this article, we’ll cover two most-used approaches when dealing with the use-cases where relational selector would be ideal:

- CSS variation classes.
- JavaScript solution and jQuery implementation of `:has` pseudo-class.

### CSS Variation Classes For Static Elements

With CSS variation classes ([modifier classes](https://en.bem.info/methodology/css/#modifiers) in BEM), developers can manually assign an appropriate CSS class to elements based on the element’s content. This approach works for static elements whose contents or state won’t change after the initial render.

Let’s take a look at the following card component example which has several variations depending on the content. Some cards don’t have an image, others don’t have a description and one card has a caption on the image.

{{< codepen height="480" theme_id="light" slug_hash="jOBpeQo" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Card variations](https://codepen.io/smashingmag/pen/jOBpeQo) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

For these cards to have the correct layout, developers need to apply the correct modifier CSS classes manually. Based on the design, elements can have multiple variations resulting in a large number of modifier classes which sometimes leads to [creative HTML workarounds](https://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/) to group all those classes in the markup. Developers need to keep track of the CSS classes, maintain documentation and make sure to apply appropriate classes.

<pre><code class="language-css">.card { /* ... */}
.card--news { /* ... */ }
.card--text { /* ... */ }
.card--featured { /* ... */ }

.card__title { /* ... */ }
.card__title--news { /* ... */ }
.card__title--text { /* ... */ }

/* ... */
</code></pre>

### JavaScript Workaround

For more complex cases, when the applied parent element style depends on child state or element content that changes dynamically, developers use JavaScript to apply necessary styles to the parent element depending on the changes in the content or state. This is usually handled by writing a custom solution on a case-by-case basis.

{{< codepen height="480" theme_id="light" slug_hash="LYWBgXy" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Filter button state](https://codepen.io/smashingmag/pen/LYWBgXy) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

### Relational Selector In jQuery

Implementation of relational `:has` selector has existed in popular JavaScript library [jQuery](https://api.jquery.com/has-selector/#has1) since 2007 and it follows the CSS specification. Of course, the main limitation of this implementation is that the jQuery line needs to be manually attached invoked inside an event listener, whereas native CSS implementation would be a part of the browser render process and automatically respond to the page state and content changes.

The downside of the JavaScript and jQuery approach is, of course, reliance on JavaScript and jQuery library dependency which can increase the overall page size and JavaScript parsing time. Also, users that are browsing the Web with JavaScript turned off will experience visual bugs if fallback is not implemented.

<pre><code class="language-javascript">// This runs only on initial render
$("button:has(+.filters input:checked)").addClass("button--active");

// This runs each time input is clicked
$("input").click(function() {
  $("button").removeClass("highlight");
  $("button:has(+.filters input:checked)").addClass("highlight");
})
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="BaWPqqO" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Email inputs &mdash; valid / invalid](https://codepen.io/smashingmag/pen/BaWPqqO) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

## Conclusion

Similar to the container queries, `:has` pseudo-class will be a major game-changer when implemented in browsers. The relational selector will allow developers to write powerful and versatile selectors that are not currently possible with CSS. 

Today, developers are dealing with the missing parent selector functionality by writing multiple modifier CSS classes that needed to be applied manually or with JavaScript, if the selector depends on a child element state. The relational selector should reduce the amount of modifier CSS classes by allowing developers to write self-documented robust selectors, and should reduce the need for JavaScript to apply dynamic styles.

Can you think of more examples where parent selector or previous sibling selector would be useful? Are you using a different workaround to deal with the missing relational selector? Share your thoughts with us in the comments.

### References

- [“Why we don't have a parent selector”](https://snook.ca/archives/html_and_css/css-parent-selectors) by Jonathan Snook
- [“Can I :has”](https://bkardell.com/blog/canihas.html) by Brian Kardell
- [“Selectors Level 4”](https://drafts.csswg.org/selectors-4/#relational) by W3C
- [jQuery `:has` selector documentation](https://api.jquery.com/has-selector/#has1)

{{< signature "vf, yk, il" >}}
