---
title: 'CSS Container Queries: Use-Cases And Migration Strategies'
slug: css-container-queries-use-cases-migration-strategies
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d6d809b-0c1a-4074-9eeb-8509dc4d383f/css-container-queries-use-cases-migration-strategies.jpg
date: 2021-05-24T11:30:00.000Z
summary: >-
  CSS Container queries bring media queries closer to the target elements themselves and enables them to adapt to virtually any given container or layout. In this article, we’re going to cover CSS container query basics and how to use them today with progressive enhancement or polyfills.
description: >-
  CSS Container queries bring media queries closer to the target elements themselves and enables them to adapt to virtually any given container or layout. In this article, we’re going to cover CSS container query basics and how to use them today with progressive enhancement or polyfills.
categories:
  - CSS
  - Layouts
  - Migration
---

When we write [media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#targeting_media_features) for a UI element, we always describe how that element is styled depending on the screen dimensions. This approach works well when the responsiveness of the target element media query should only depend on viewport size. Let’s take a look at the following responsive page layout example.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c417bb96-14a2-4369-ba8f-6ca20a7f267e/1-introduction-to-container-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c417bb96-14a2-4369-ba8f-6ca20a7f267e/1-introduction-to-container-queries.jpg" width="800" height="500" sizes="100vw" caption="Responsive page layout example. The left image shows the desktop layout at 1280px viewport width and the right image shows the mobile layout at 568px viewport width. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c417bb96-14a2-4369-ba8f-6ca20a7f267e/1-introduction-to-container-queries.jpg'>Large preview</a>)" alt="Responsive page layout example. The left image shows the desktop layout at 1280px viewport width and the right image shows the mobile layout at 568px viewport width." >}}

However, responsive Web Design (RWD) is not limited to a page layout &mdash; the individual UI components usually have media queries that can change their style depending on the viewport dimensions.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed3582ee-9039-44a9-9e02-54d52bb86eea/2-introduction-to-container-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed3582ee-9039-44a9-9e02-54d52bb86eea/2-introduction-to-container-queries.jpg" width="800" height="500" sizes="100vw" caption="Responsive product card component example. The left image shows a component at 720px viewport width and the right image shows component layout at 568px viewport width. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed3582ee-9039-44a9-9e02-54d52bb86eea/2-introduction-to-container-queries.jpg'>Large preview</a>)" alt="Responsive product card component example. The left image shows a component at 720px viewport width and the right image shows component layout at 568px viewport width." >}}

You might have already noticed a problem with the previous statement &mdash; individual UI component layout often does not depend exclusively on the viewport dimensions. Whereas page layout is an element closely tied to viewport dimensions and is one of the topmost elements in HTML, UI components can be used in different contexts and containers. If you think about it, the viewport is just a container, and UI components can be nested within other containers with styles that affect the component’s dimensions and layout.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baabd695-5d97-4ef2-b03b-c1233c3c3039/3-introduction-to-container-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baabd695-5d97-4ef2-b03b-c1233c3c3039/3-introduction-to-container-queries.jpg" width="800" height="542" sizes="100vw" caption="Example of page layout with the same product card UI component in the top section 3-column grid and the bottom section list. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baabd695-5d97-4ef2-b03b-c1233c3c3039/3-introduction-to-container-queries.jpg'>Large preview</a>)" alt="Example of page layout with the same product card UI component in the top section 3-column grid and the bottom section list." >}}

Even though the same product card component is used in both the top and bottom sections, component styles not only depend on the viewport dimensions but also depend on the context and the container CSS properties (like the grid in the example) where it’s placed.

Of course, we can structure our CSS so we support the style variations for different contexts and containers to address the layout issue manually. In the worst-case scenario, this variation would be added with style override which would lead to code duplication and specificity issues.

<pre><code class="language-css">.product-card {
    /* Default card style */
}

.product-card--narrow {
   /* Style variation for narrow viewport and containers */
}

@media screen and (min-width: 569px) {
 .product-card--wide {
     /* Style variation for wider viewport and containers */
  }
}</code></pre>

However, this is more of a workaround for the limitations of media queries rather than a proper solution. When writing media queries for UI elements we are trying to find a “magic” viewport value for a breakpoint when the target element has minimum dimensions where the layout doesn’t break. In short, **we are linking a “magical” viewport dimension value to element dimensions value**. This value is usually different from than viewport dimension and is prone to bugs when inner container dimensions or layout changes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0243e298-c59f-4e6f-8d23-9cef217a3cb9/4-introduction-to-container-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0243e298-c59f-4e6f-8d23-9cef217a3cb9/4-introduction-to-container-queries.jpg" width="800" height="417" sizes="100vw" caption="Example of how media query cannot be reliably linked to element dimensions. Various CSS properties can affect element dimensions within a container. In this example, container padding is different between the two images. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0243e298-c59f-4e6f-8d23-9cef217a3cb9/4-introduction-to-container-queries.jpg'>Large preview</a>)" alt="Example of how media query cannot be reliably linked to element dimensions. Various CSS properties can affect element dimensions within a container. In this example, container padding is different between the two images." >}}

The following example showcases this exact issue &mdash; even though a responsive product card element has been implemented and it looks good in a standard use-case, it looks broken if it’s moved to a different container with CSS properties that affect element dimensions. Each **additional use-case requires additional CSS code** to be added which can lead to duplicated code, code bloat, and code that is difficult to maintain.

{{< codepen height="480" theme_id="light" slug_hash="eYvWVxz" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Product Cards: Various Containers](https://codepen.io/smashingmag/pen/eYvWVxz) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

This is one of the issues that container queries attempting to fix. **Container queries extend existing media queries** functionality with queries that depend on the target element dimensions. There are three major benefits of using this approach:

- Container query styles are applied depending on the dimensions of the target element itself. UI components will be able to adapt to any given context or container.
- Developers won’t need to look for a “magic number” viewport dimension value that links a viewport media query to a target dimension of UI component in a specific container or a specific context.
- No need to add additional CSS classes or media queries for different contexts and use-cases.

<blockquote>“The ideal responsive website is a system of flexible, modular components that can be repurposed to serve in multiple contexts.”<br /><br />&mdash; “<a href="https://alistapart.com/article/container-queries-once-more-unto-the-breach/#section1">Container Queries: Once More Unto the Breach</a>,” Mat Marquis</blockquote>

Before we dive deep into container queries, we need to check out the browser support and see how we can enable the experimental feature in our browser.

## Browser Support

Container queries are an [experimental feature](https://caniuse.com/css-container-queries), available currently in [Chrome Canary](https://www.google.com/chrome/canary/) version at the time of writing this article. If you want to follow along and run the CodePen examples in this article you’ll need to enable container queries in the following settings URL.

<pre><code class="language-markup">chrome://flags/#enable-container-queries</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6a0d41-c879-437f-9a45-7abf5a0e867e/5-introduction-to-container-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6a0d41-c879-437f-9a45-7abf5a0e867e/5-introduction-to-container-queries.png" width="800" height="329" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6a0d41-c879-437f-9a45-7abf5a0e867e/5-introduction-to-container-queries.png'>Large preview</a>)" alt="Container queries" >}}

In case you are using a browser that doesn’t support container queries, an image showcasing the intended working example will be provided alongside the CodePen demo.

{{% feature-panel %}}

## Working With Container Queries

Container queries are not as straightforward as regular media queries. We’ll have to add an extra line of CSS code to our UI element to make container queries work, but there’s a reason for that and we’ll cover that next.

### Containment Property

CSS `contain` property has been added to the majority of modern browsers and has a decent [75% browser support](https://caniuse.com/mdn-css_properties_contain) at the time of writing this article. The `contain` property is mainly used for performance optimization by hinting to the browser which parts (subtrees) of the page can be treated as independent and won’t affect the changes to other elements in a tree. That way, if a change occurs in a single element, the [browser will re-render](https://developers.google.com/web/fundamentals/performance/rendering) only that part (subtree) instead of the whole page. With `contain` property values, we can specify which types of containment we want to use &mdash; `layout`, `size`, or `paint`.

There are many [great articles](https://www.smashingmagazine.com/2019/12/browsers-containment-css-contain-property/) about the `contain` property that outline available options and use-cases in much more detail, so I’m going to focus only on properties related to container queries.

What does the CSS contentment property that’s used for optimization have to do with container queries? For container queries to work, the browser needs to know if a change occurs in the element’s children layout that it should re-render only that component. The browser will know to apply the code in the container query to the matching component when the component is rendered or the component’s dimension changes.

We’ll use the `layout​` and `style​` values for the `contain​` property, but we’ll also need an [additional value](https://github.com/oddbird/css-sandbox/blob/main/src/rwd/query/explainer.md#proposed-solutions) that signals the browser about the axis in which the change will occur.

- `inline-size`  
Containment on the inline axis. It’s expected for this value to have significantly more use-cases, so it’s being implemented first.
- `block-size`  
Containment on block axis. It’s still in development and is not currently available.

One minor downside of the `contain` property is that our layout element needs to be a child of a `contain` element, meaning that we are adding an additional nesting level.

<pre><code class="language-html">&lt;section&gt;
  &lt;article class="card"&gt;
      &lt;div class="card__wrapper"&gt;
          &lt;!-- Card content --&gt;       
      &lt;/div&gt;
  &lt;/article&gt;
&lt;/section&gt;</code></pre>
   

<pre><code class="language-css">.card {
   contain: layout inline-size style;
}

.card__wrapper {
  display: grid;
  grid-gap: 1.5em;
  grid-template-rows: auto auto;
  /* ... */
}</code></pre>

Notice how we are not adding this value to a more distant parent-like `section` and keeping the container as close to the affected element as possible.

<blockquote>“Performance is the art of avoiding work and making any work you do as efficient as possible. In many cases, it’s about working with the browser, not against it.”<br /><br />&mdash; “<a href="https://developers.google.com/web/fundamentals/performance/rendering">Rendering Performance</a>,” Paul Lewis</blockquote>

That is why we should correctly signal the browser about the change. Wrapping a distant parent element with a `contain` property can be counter-productive and negatively affect page performance. In worst-case scenarios of misusing the `contain` property, the layout may even break and the browser won’t render it correctly.

{{% ad-panel-leaderboard %}}

### Container Query

After the `contain` property has been added to the card element wrapper, we can write a container query. We’ve added a `contain` property to an element with `card` class, so now we can include any of its child elements in a container query.

Just like with regular media queries, we need to define a query using `min-width` or `max-width` properties and nest all selectors inside the block. However, we’ll be using the `@container` keyword instead of `@media` to define a container query.

<pre><code class="language-css">@container (min-width: 568px) {
  .card__wrapper {
    align-items: center;
    grid-gap: 1.5em;
    grid-template-rows: auto;
    grid-template-columns: 150px auto;
  }

  .card__image {
    min-width: auto;
    height: auto;
  }
}</code></pre>

Both `card__wrapper` and `card__image` element are children of `card` element which has the `contain` property defined. When we replace the regular media queries with container queries, remove the additional CSS classes for narrow containers, and run the CodePen example in a browser that supports container queries, we get the following result.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5cb077f-164a-42fb-87c5-f77c9f1db99d/6-introduction-to-container-queries.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5cb077f-164a-42fb-87c5-f77c9f1db99d/6-introduction-to-container-queries.gif" width="800" height="410" alt="In this example, we’re not resizing the viewport, but the &lt;section&gt; container element itself that has resize CSS property applied. The component automatically switches between layouts depending on the container dimensions." /></a><figcaption>In this example, we’re not resizing the viewport, but the &lt;section&gt; container element itself that has resize CSS property applied. The component automatically switches between layouts depending on the container dimensions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5cb077f-164a-42fb-87c5-f77c9f1db99d/6-introduction-to-container-queries.gif">Large preview</a>)</figcaption></figure>

{{< codepen height="480" theme_id="light" slug_hash="PopmQLV" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Product Cards: Container Queries](https://codepen.io/smashingmag/pen/PopmQLV) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Please note that **container queries currently don’t show up in Chrome developer tools**, which makes debugging container queries a bit difficult. It’s expected that the proper debugging support will be added to the browser in the future.

You can see how container queries allow us to create more robust and reusable UI components that can adapt to virtually any container and layout. However, proper browser support for container queries is still far away in the feature. Let’s try and see if we can implement container queries using progressive enhancement.

### Progressive Enhancement & Polyfills

Let’s see if we can add a fallback to CSS class variation and media queries. We can use [CSS feature queries](https://caniuse.com/css-featurequeries) with the `@supports` rule to detect available browser features. However, we [cannot check for other queries](https://github.com/w3c/csswg-drafts/issues/6175), so we need to add a check for a `contain: layout inline-size style` value. We’ll have to assume that browsers that do support `inline-size` property also support container queries.

<pre><code class="language-css">/* Check if the inline-size value is supported &#42;/
@supports (contain: inline-size) {
  .card {
    contain: layout inline-size style;
  }
}

/* If the inline-size value is not supported, use media query fallback &#42;/
@supports not (contain: inline-size) {
    @media (min-width: 568px) {
       /&#42; ... &#42;/
  }
}

/&#42; Browser ignores @container if it’s not supported &#42;/
@container (min-width: 568px) {
  /&#42; Container query styles &#42;/
}</code></pre>

However, this approach might lead to duplicated styles as the same styles are being applied both by container query and the media query. If you decide to implement container queries with progressive enhancement, you’d want to use a CSS pre-processor like SASS or a post-processor like PostCSS to avoid duplicating blocks of code and use CSS mixins or another approach instead.

{{< codepen height="480" theme_id="light" slug_hash="zYZwRXZ" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Product Cards: Container Queries with progressive enhancement](https://codepen.io/smashingmag/pen/zYZwRXZ) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Since this container query spec is still in an experimental phase, it’s important to keep in mind that the spec or implementation is prone to change in future releases.

Alternatively, you can use polyfills to provide a reliable fallback. There are two JavaScript polyfills I’d like to highlight, which currently seem to be actively maintained and provide necessary container query features: 

- [`cqfill` by Jonathan Neal](https://github.com/jsxtools/cqfill)    
JavaScript polyfill for CSS and PostCSS
- [`react-container-query` by Chris Garcia](https://github.com/react-container-query/react-container-query)  
Custom hook and component for React

### Migrating From Media Queries To Container Queries

If you decide to implement container queries on an existing project that uses media queries, you’ll need to refactor HTML and CSS code. I’ve found this to be the fastest and most straightforward way of adding container queries while providing a reliable fallback to media queries. Let’s take a look at the previous card example.

<pre><code class="language-html">&lt;section&gt;
      &lt;div class="card__wrapper card__wrapper--wide"&gt;
          &lt;!-- Wide card content --&gt;       
      &lt;/div&gt;
&lt;/section&gt;

/* ... */

&lt;aside&gt;
      &lt;div class="card__wrapper"&gt;
          &lt;!-- Narrow card content --&gt;        
      &lt;/div&gt;
&lt;/aside&gt;</code></pre>

<pre><code class="language-css">.card__wrapper {
  display: grid;
  grid-gap: 1.5em;
  grid-template-rows: auto auto;
  /* ... */
}

.card__image {
  /* ... */
}

@media screen and (min-width: 568px) {
  .card__wrapper--wide {
    align-items: center;
    grid-gap: 1.5em;
    grid-template-rows: auto;
    grid-template-columns: 150px auto;
  }

  .card__image {
    /* ... */
  }
}
</code></pre>

First, wrap the root HTML element that has a media query applied to it with an element that has the `contain` property.

<pre><code class="language-html">&lt;section&gt;
  &lt;article class="card"&gt;
      &lt;div class="card__wrapper"&gt;
          &lt;!-- Card content --&gt;        
      &lt;/div&gt;
  &lt;/article&gt;
&lt;/section&gt;</code></pre>

<pre><code class="language-css">@supports (contain: inline-size) {
  .card {
    contain: layout inline-size style;
  }
}</code></pre>

Next, wrap a media query in a feature query and add a container query.

<pre><code class="language-css">@supports not (contain: inline-size) {
    @media (min-width: 568px) {
    .card__wrapper--wide {
       /* ... */
    }

    .card__image {
       /* ... */
    }
  }
}


@container (min-width: 568px) {
  .card__wrapper {
     /* Same code as .card__wrapper--wide in media query */
  }

  .card__image {
    /* Same code as .card__image in media query */
  }
}</code></pre>

Although this method results in some code bloat and duplicated code, by using SASS or PostCSS you can avoid duplicating development code, so the CSS source code remains maintainable.

Once container queries receive proper browser support, you might want to consider removing `@supports not (contain: inline-size)` code blocks and continue supporting container queries exclusively.

Stephanie Eckles has recently published a great article on container queries covering various [migration strategies](https://www.smashingmagazine.com/2021/05/complete-guide-css-container-queries/#case-study-upgrading-smashing-magazine-s-article-teasers). I recommend checking it out for more information on the topic.

{{% ad-panel-leaderboard %}}

## Use-Case Scenarios

As we’ve seen from the previous examples, container queries are best used for highly reusable components with a layout that depends on the available container space and that can be used in various contexts and added to different containers on the page. 

Other examples include (examples require a browser that supports container queries):

- [Modular components like cards, form elements, banners, etc.](https://codepen.io/aafmisra/pen/yLgRprY)
- [Adaptable layouts](https://codepen.io/shadeed/pen/ExZEEjZ?editors=0100)
- [Pagination with different functionalities for mobile and desktop](https://codepen.io/shadeed/pen/VwPQORy?editors=0100)
- [Fun experiments with CSS resize](https://codepen.io/jh3y/pen/poeyxba)

## Conclusion

Once the spec has been implemented and widely supported in browsers, container queries might become a game-changing feature. It will allow developers to write queries on component level, moving the queries closer to the related components, instead of using the distant and barely-related viewport media queries. This will result in more robust, reusable, and maintainable components that will be able to adapt to various use-cases, layouts, and containers.

As it stands, container queries are still in an early, experimental phase and the implementation is prone to change. If you want to start using container queries in your projects today, you’ll need to add them using progressive enhancement with feature detection or use a JavaScript polyfill. Both cases will result in some overhead in the code, so if you decide to use container queries in this early phase, make sure to plan for refactoring the code once the feature becomes widely supported.

### References

- “[Container Queries: A Quick Start Guide”](https://www.oddbird.net/2021/04/05/containerqueries/) by David A. Herron
- “[Say Hello To CSS Container Queries](https://ishadeed.com/article/say-hello-to-css-container-queries/),” Ahmad Shadeed
- “[CSS Containment In Chrome 52](https://developers.google.com/web/updates/2016/06/css-containment),” Paul Lewis
- “[Helping Browsers Optimize With The CSS Contain Property](https://www.smashingmagazine.com/2019/12/browsers-containment-css-contain-property/),” Rachel Andrew

{{< signature "vf, yk, il" >}}
