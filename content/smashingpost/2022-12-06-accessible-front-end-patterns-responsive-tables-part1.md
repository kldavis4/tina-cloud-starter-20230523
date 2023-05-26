---
title: 'Accessible Front-End Patterns For Responsive Tables (Part 1)'
slug: accessible-front-end-patterns-responsive-tables-part1
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a082e68-4b7b-47df-ab6a-f1b9105b491e/accessible-front-end-patterns-responsive-tables-part1.jpg
date: 2022-12-06T12:00:00.000Z
summary: >-
  There is no universal solution for making every kind of table responsive and usable on smaller screens, so we have to rely on various patterns, which Adrian explains in this two-part series.
description: >-
  There is no universal solution for making every kind of table responsive and usable on smaller screens, so we have to rely on various patterns, which Adrian explains in this two-part series.
categories:
  - Accessibility
  - UI
  - UX
  - Usability
---

Tables allow us to organize data into **grid-like format of rows and columns**. Scanning the table in one direction allows users to search and compare the data while scanning in the other direction lets users get all details for a single item by **matching the data to their respective table header** elements. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee609bea-f7ca-4fc7-9f32-388109253cc9/1-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee609bea-f7ca-4fc7-9f32-388109253cc9/1-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="589" sizes="100vw" caption="A table example from <a href='https://www.discogs.com/'>Discogs</a>, which is used to compare various release versions of the record by country, year of release, catalog number, and so on. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee609bea-f7ca-4fc7-9f32-388109253cc9/1-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="A screenshot of the table example from Discogs" >}}

Tables often rely on having **enough screen space** to communicate these data relations effectively. This makes designing and developing more complex responsive tables somewhat of a challenge. There is **no universal, silver-bullet solution for making the tables responsive** as we often see with other elements like accordions, dropdowns, modals, and so on. It all depends on the main purpose of the table and how it’s being used.

If we fail to consider these factors and use the wrong approach, we can potentially make usability worse for some users.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8962abce-13f4-4020-8a3f-a38de20e01d6/2-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8962abce-13f4-4020-8a3f-a38de20e01d6/2-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="619" sizes="100vw" caption="A previous example shown on a small screen. Without a table head element, the data is difficult to parse and compare. This table could be better implemented using a different approach. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8962abce-13f4-4020-8a3f-a38de20e01d6/2-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="A screenshot of the table example from Discogs shown on a small screen" >}}

In this article, we’re going to be strictly focused on various ways we can make tables on the web responsive, depending on the data type and table use-case, so we’re not going to cover table search, filtering, and other similar functionalities. 

If you are interested in improving user experience (UX) for tables and other UI elements beyond just responsiveness, make sure to check out Smashing Magazine’s incredibly useful [Smart Interface Design Patterns workshop](https://smart-interface-design-patterns.com/), which covers best practices and guidelines for various UI components, tables included.

{{% feature-panel %}}

## Short Primer On Accessible Tables

Before diving into specific responsive table patterns, let’s quickly go over some best practices regarding design and accessibility. We’ll cover some general points in this section and other, more specific ones in later examples.

### Design And Visual Features

First, we need to ensure that users can easily scan the table and intuitively match the data to their respective table header elements. From the design perspective, we can ensure the following:

- Use **proper vertical and horizontal alignment** (“A List Apart” covers this in their [article](https://alistapart.com/article/web-typography-tables/#section5)).
- Design a table with **clear divisions and optimal spacing** between rows and cells.
- **Table header elements should stand out** and be styled differently from data cells.
- Consider using **alternate background color for rows or columns** (“zebra stripes”) for easier scanning.

### ARIA Roles

We want to include proper ARIA attributes to our table element and its descendants. Applying some CSS styles like `display: block` or `display: flex` (to create responsive stacked columns) may [cause issues in some browsers](https://adrianroselli.com/2018/02/tables-css-display-properties-and-aria.html#TheTable). In those cases, screen readers interpret the `table` element differently, and we lose the useful table semantics. By adding ARIA labels, we can fix the issue and retain the table semantics.

Including these roles in HTML manually could become tedious and prone to error. If you are **comfortable about using JavaScript** for adding additional markup, and you aren’t using a framework that generates static HTML files, you can use this handy little [JavaScript function](https://adrianroselli.com/2018/05/functions-to-add-aria-to-tables-and-lists.html#Table) made by Adrian Roselli to automatically add ARIA roles to table elements:

<pre><code class="language-javascript">function AddTableARIA() {
  try {
    var allTables = document.querySelectorAll("table");
    for (var i = 0; i &lt; allTables.length; i++) {
      allTables[i].setAttribute("role", "table");
    }
    var allRowGroups = document.querySelectorAll("thead, tbody, tfoot");
    for (var i = 0; i &lt; allRowGroups.length; i++) {
      allRowGroups[i].setAttribute("role", "rowgroup");
    }
    var allRows = document.querySelectorAll("tr");
    for (var i = 0; i &lt; allRows.length; i++) {
      allRows[i].setAttribute("role", "row");
    }
    var allCells = document.querySelectorAll("td");
    for (var i = 0; i &lt; allCells.length; i++) {
      allCells[i].setAttribute("role", "cell");
    }
    var allHeaders = document.querySelectorAll("th");
    for (var i = 0; i &lt; allHeaders.length; i++) {
      allHeaders[i].setAttribute("role", "columnheader");
    }
    // This accounts for scoped row headers
    var allRowHeaders = document.querySelectorAll("th[scope=row]");
    for (var i = 0; i &lt; allRowHeaders.length; i++) {
      allRowHeaders[i].setAttribute("role", "rowheader");
    }
    // Caption role not needed as it is not a real role, and
    // browsers do not dump their own role with the display block.
  } catch (e) {
    console.log("AddTableARIA(): " + e);
  }
}
</code></pre>

However, keep in mind the following **potential drawbacks** of using JavaScript here:

- Users might choose to browse the website with JavaScript turned off.
- The JavaScript file may not be downloaded or may be downloaded much later if the user is browsing the website on an unreliable or slow network.
- If this is bundled alongside other JavaScript code in the same file, an error in other parts of the file might prevent this function from running in some cases.

### Adding An a11y-Friendy Title

Adding a title next to the table helps both sighted users and users with assistive devices get a complete understanding of the content.

Ideally, we would include a `caption` element inside the `table` element as a first child. Notice how we can nest any HTML heading element as a child to maintain the title hierarchy.

<pre><code class="language-html">&lt;table&gt;
  &lt;caption&gt;
    &lt;h2&gt;Top 10 best-selling albums of all time&lt;/h2&gt;
  &lt;/caption&gt;

   &lt;!-- Table markup --&gt;
&lt;/table&gt;
</code></pre>

If we are using a wrapper element to make the table scrollable or adding some other functionality that makes the `caption` element not ideal, we can include the `table` inside a `figure` element and use a `figcaption` to add a title. Make sure to include a proper ARIA label on either the table element or a wrapper element and link it to a `figcaption` element:

<div class="break-out">

<pre><code class="language-html">&lt;figure&gt;
  &lt;figcaption id="caption"&gt;Top 10 best-selling albums of all time&lt;/figcaption&gt;
  &lt;table aria-labelledby="caption"&gt;&lt;!-- Table markup --&gt;&lt;/table&gt;
&lt;/figure&gt;
</code></pre>
</div>

<div class="break-out">

<pre><code class="language-html">&lt;figure&gt;
  &lt;figcaption id="caption"&gt;
    &lt;h2&gt;Top 10 best-selling albums of all time&lt;/h2&gt;
  &lt;/figcaption&gt;
  &lt;div class="table-wrapper" role="group" aria-labelledby="caption" tabindex="0"&gt;
    &lt;table&gt;&lt;!-- Table markup --&gt;&lt;/table&gt;
  &lt;/div&gt;
&lt;/figure&gt;
</code></pre>
</div>

There are **other accessibility aspects** to consider when designing and developing tables, like keyboard navigation, print styles, high contrast mode, and others. We’ll cover some of those in the following sections. For a **more comprehensive guide** on creating accessible table elements, make sure to check out [Heydon Pickering’s guide](https://inclusive-components.design/data-tables/) and [Adrian Roselli’s article](https://adrianroselli.com/2017/11/a-responsive-accessible-table.html) which is being kept up to date with the latest features and best practices.

{{% ad-panel-leaderboard %}}

## Bare-bones Responsive Approach

Sometimes we don’t have to make any major changes to our table to make it responsive. We just need to ensure the table width responds to the viewport width. That can be easily achieved with `width: 100%`, but we should also consider setting a dynamic `max-width` value, so our table doesn’t grow too wide on larger containers and becomes difficult to scan, like in the following example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b4d7d4-89f6-4735-b41f-ea99353e685f/3-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b4d7d4-89f6-4735-b41f-ea99353e685f/3-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="290" sizes="100vw" caption="The table responds to viewport size, and it looks good on small screens, but on wider screens, it becomes difficult to scan due to the unnecessary space between the columns. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b4d7d4-89f6-4735-b41f-ea99353e685f/3-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="A example of a table on a wide screen with big space between the columns" >}}

<pre><code class="language-css">table {
  width: fit-content;
}
</code></pre>

With the `fit-content` value, we ensure that the table doesn’t grow beyond the minimum width required to optimally display the table contents and that it remains responsive. 

The table responds to viewport size, and it looks good on small screens, but on wider screens, it becomes difficult to scan due to the unnecessary space between the columns.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eca8103-7278-4896-985b-5dc826f255f6/4-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eca8103-7278-4896-985b-5dc826f255f6/4-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="533" sizes="100vw" caption="By setting the width with <code>fit-content</code> value, we’ve fixed the above-mentioned issue. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eca8103-7278-4896-985b-5dc826f255f6/4-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table on a wide screen without big space between the columns" >}}

We can also ensure that the table `max-width` value always adapts to its content. We don’t have to rely on assigning a magic number for each table or wrap the table in a container that constrains the width to a fixed value.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec22d05-8c25-4850-82b7-a51d4086cb94/5-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec22d05-8c25-4850-82b7-a51d4086cb94/5-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="493" sizes="100vw" caption="By using <code>auto</code> or <code>max-content</code>, we get a maximum width value that adapts to table contents. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec22d05-8c25-4850-82b7-a51d4086cb94/5-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table on a wide screen with a maximum width value that adapts to table contents" >}}

This works well for simple tables that don’t require too much screen space to be effectively parsed and aren’t affected by `word-break`. We can even use [fluid typography and fluid spacing](https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/) to make sure these simple tables remain readable on smaller screens.

<pre><code class="language-css">/&#42; Values generated with Utopia https://utopia.fyi/type/calculator/ &#42;/

tbody {
  font-size: clamp(1.13rem, calc(0.35rem + 2.19vw), 1.75rem);
}

tbody td {
  padding-top: clamp(1.13rem, calc(0.35rem + 2.19vw), 1.75rem);
  padding-bottom:  clamp(2rem, calc(0.62rem + 3.9vw), 3.11rem);
}
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="yLEVLbX" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Responsive table - as is [forked]](https://codepen.io/smashingmag/pen/yLEVLbX) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

## Scrollbar Approach

On complex tables with multiple columns where we cannot rely on fluid sizing and `word-break` to keep the table readable, we want the table to stretch as far as it needs to display the content optimally and allow users to scroll the table horizontally, so the table remains usable.

{{< codepen height="480" theme_id="light" slug_hash="KKeNKvm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table - scrollbars with dynamic cropping [forked]](https://codepen.io/smashingmag/pen/KKeNKvm) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

By wrapping the table and applying `overflow: auto` on the wrapper element, we can add scrollbars to our table when there is not enough space on the screen for the table to fit.

This is useful on complex tables when we want to **keep the default table layout and hierarchy for clarity**and when we want to **allow users to compare the data between cells** and easily match them to table headers.

We can use a `figure` element to do so and add a `figcaption` for the table title or use another HTML container element with a heading for a title:

<pre><code class="language-html">&lt;figure&gt;
  &lt;figcaption id="caption"&gt;
    &lt;h1&gt;Countries with most population&lt;/h1&gt;
  &lt;/figcaption&gt;
  &lt;div class="table-wrapper" role="group" aria-labelledby="caption"&gt;
    &lt;table&gt;
      &lt;!-- Table contents --&gt;
    &lt;/table&gt;
  &lt;/div&gt;
&lt;/figure&gt;
</code></pre>

Either way, this configuration is **not usable for users who are using keyboard navigation** as the table element is not focusable. We can easily do that by adding a `tabindex` attribute to the table wrapper element or table element directly (if we aren’t using any wrappers).

<div class="break-out">

<pre><code class="language-html">&lt;div tabindex="0" class="table-wrapper" role="group" aria-labelledby="caption"&gt;
  &lt;table&gt;
     &lt;!-- Table contents --&gt;
  &lt;/table&gt;
&lt;/div&gt;
</code></pre>
</div>

### Using Shadows To Indicate Possible Scrolling Directions

Browser **scrollbars are controlled by the operating system**, meaning that **they might look and behave differently**, depending on the device. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539553b1-ed1d-41ec-9ed6-22fc3052fead/6-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539553b1-ed1d-41ec-9ed6-22fc3052fead/6-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="300" sizes="100vw" caption="Chrome browser on iOS: scrollbar is hidden by default. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539553b1-ed1d-41ec-9ed6-22fc3052fead/6-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table where a scrollbar is hidden" >}}

This is important to know because on some devices, like smartphones and tablets, scrollbars aren’t visible right away, and users might get the impression that the table is not scrollable.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c7d9e0e-9c8c-4b36-8afe-5ac1957f0fe7/7-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c7d9e0e-9c8c-4b36-8afe-5ac1957f0fe7/7-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="318" sizes="100vw" caption="Chrome browser on iOS: scrollbar displays when a user interacts with the element. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c7d9e0e-9c8c-4b36-8afe-5ac1957f0fe7/7-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table with a scrollbar displayed " >}}

Lea Verou and Roman Komarov have suggested using [“scrolling shadows”](https://lea.verou.me/2012/04/background-attachment-local/) to subtly indicate the scrolling direction using gradient background and `background-attachment` property. Using this property, we can set background gradient behavior when scrolling. We also use linear gradients as edge covers for shadows, so we gradually hide the shadow when the user has reached an edge and cannot scroll in that direction anymore.

<div class="break-out">

<pre><code class="language-css">.table-wrapper {
  overflow: auto;
  background: 
    linear-gradient(90deg, var(--color-background) 20%, rgba(255, 255, 255, 0)),
    linear-gradient(90deg, rgba(255, 255, 255, 0), var(--color-background) 80%) 
                    100% 0,
    radial-gradient(farthest-side at 0 0%, var(--color-shadow), rgba(0, 0, 0, 0)),
    radial-gradient(farthest-side at 100% 0%, var(--color-shadow), rgba(0, 0, 0, 0))
                    100% 0;
  background-repeat: no-repeat;
  background-size: 20% 200%, 20% 200%, 8% 400%, 8% 400%;
  background-attachment: local, local, scroll, scroll;
}
</code></pre>
</div>

{{< codepen height="480" theme_id="light" slug_hash="ExRNxpd" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table - scrollbars with background [forked]](https://codepen.io/smashingmag/pen/ExRNxpd) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Notice how shadows subtly hide and show as we scroll from one edge to another. And we added this nice effect with just a few additional CSS attributes without using JavaScript or additional HTML elements or wrappers.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/729f2187-5dea-4b98-a400-9acc64410ebc/8-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/729f2187-5dea-4b98-a400-9acc64410ebc/8-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="354" sizes="100vw" caption="The shadow appears and disappears depending the direction where user can scroll. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/729f2187-5dea-4b98-a400-9acc64410ebc/8-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table with a scrollbar with shadow" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c21cbde7-218e-42f7-bea7-c43c4f538ea7/9-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c21cbde7-218e-42f7-bea7-c43c4f538ea7/9-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="321" sizes="100vw" caption="On devices where scrollbars are hidden by default, the subtle shadow indicates that a table can be scrolled. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c21cbde7-218e-42f7-bea7-c43c4f538ea7/9-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table with a subtle shadow on the right side" >}}

Keep in mind that `background-attachment` property is [not supported on iOS Safari](https://caniuse.com/background-attachment) and a few other browsers, so make sure to either **provide a fallback or remove the background on unsupported browsers**. We can also provide helpful text next to the table to make sure users understand that the table can be scrolled.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b8c18c-76d5-4388-a31e-614037d744ed/10-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b8c18c-76d5-4388-a31e-614037d744ed/10-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="304" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b8c18c-76d5-4388-a31e-614037d744ed/10-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="An example of a table with a text that reads 'scroll for more'" >}}

### Forcing Table Cropping

We can also dynamically set the table column width to enforce table cropping mid-content, so the user gets a clear hint that the table is scrollable. I’ve created a simple function for this example. The last column will always get cropped to 85% of its size, and we’ll reduce the number of visible columns by one if we cannot show at least 5% of the column’s width.

<pre><code class="language-javascript">function cropTable(visibleCols) {
  const table = document.querySelector("figure");
  const { width: tableWidth } = table.getBoundingClientRect();
  const cols = table.querySelectorAll("th, td");
  const newWidth = tableWidth / visibleCols;

  // Resize columns to fit a table.
  cols.forEach(function(col) {
    // Always make sure that col is cropped by at least 15%.
    col.style.minWidth = newWidth + (newWidth &#42; 0.15) + "px";
  });

  // Return if we are about to fall below min column count.
  if (visibleCols &lt;= MIN&#95;COLS) {
    return;
  }

  // Measure a sample table column to check if resizing was successful.
  const { width: colWidth } = cols[0].getBoundingClientRect();

  // Check if we should crop to 1 column less (calculate new column width).
  if (colWidth &#42; visibleCols &gt; tableWidth + newWidth &#42; 0.95) {
    cropTable(visibleCols - 1);
  }
}
</code></pre>

This function might need to be adjusted to a more complex use case. Check the example below and see how the table column width responds to window resizing:

{{< codepen height="480" theme_id="light" slug_hash="xxzRxBB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table - scrollbars with dynamic cropping [forked]](https://codepen.io/smashingmag/pen/xxzRxBB) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

### Sticky Table Headers

As the user scrolls the table, either horizontally or vertically, **table header elements will become hidden**, and the user might start **having trouble matching the data to the headers**, depending on the table and data complexity. They would have to go back and forth and memorize the data order.

To avoid this issue, we can **make the table headers sticky** by applying `position: sticky` and making some style adjustments to fix the background color and borders. This is a great enhancement because `position: sticky` and style adjustments don’t affect the table style or layout if it’s not scrollable.

{{< codepen height="480" theme_id="light" slug_hash="QWxGWXq" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table - fixed table-heads + background [forked]](https://codepen.io/smashingmag/pen/QWxGWXq) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Combined with the aforementioned “scrolling shadows” effect, we’ve ensured that users can easily scan the table data and have proper scrolling indicators.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd98ee7-7acf-4146-9616-3e03a3102ea2/11-accessible-front-end-patterns-responsive-tables-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd98ee7-7acf-4146-9616-3e03a3102ea2/11-accessible-front-end-patterns-responsive-tables-part1.png" width="800" height="360" sizes="100vw" caption="A table with scrolling shadows with sticky table headers which remains visible on scroll. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd98ee7-7acf-4146-9616-3e03a3102ea2/11-accessible-front-end-patterns-responsive-tables-part1.png'>Large preview</a>)" alt="A table with scrolling shadows with sticky table headers which remains visible on scroll" >}}

{{% ad-panel-leaderboard %}}

## Stacking Approach (Rows To Blocks)

The stacking approach has been a **very popular pattern** for years. It involves converting each table row into a block of vertically stacked columns. This is a very useful approach for tables where **data is not comparable** or when **we don’t need to highlight the hierarchy** and order between items. 

For example, cart items in a webshop or a simple contacts table with details &mdash; these items are independent, and users primarily scan them individually and search for a specific item. 

As mentioned before, converting the table rows to blocks usually involves applying `display: block` on small screens. However, as Adrian Roselli has noted, applying a `display` property [overrides native table semantics](https://adrianroselli.com/2018/02/tables-css-display-properties-and-aria.html) and makes the element less accessible on screen readers. This discovery was jarring to me, as I’ve spent years crafting responsive tables using this pattern without realizing I was making them less accessible in the process.

It’s not all bad news, as Adrian Roselli notes the following [change for Chrome version 80](https://adrianroselli.com/2018/02/tables-css-display-properties-and-aria.html#Update4):

<blockquote>Big progress. Chrome 80 no longer drops semantics for HTML tables when the <code>display</code> properties <code>flex</code>, <code>grid</code>, <code>inline-block</code>, or <code>contents</code> are used. The new Edge (ChromiEdge) follows suit. Firefox still dumps table semantics for only <code>display: contents</code>. Safari dumps table semantics for everything.<br /><br />&mdash; Adrian Roselli</blockquote>

For this example, we’ll use `display: flex` instead of using `display: block` for our stacking pattern. This is not an ideal solution as other browsers might still drop table semantics, so make sure to test the accessibility on various browsers and devices.

<pre><code class="language-css">/&#42; Small screen width styles &#42;/
table, tbody, tbody tr, tbody td, caption {
  display: flex;
  flex-direction: column;
  width: 100%;
  word-break: break-all;
}
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="bGKBNNr" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table - stacked [forked]](https://codepen.io/smashingmag/pen/bGKBNNr) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

### Accordion

The stacking pattern might look nice initially and seems to be an elegant solution from a design perspective. However, depending on the table and data complexity, **this pattern might significantly increase page height**, and the user might have to scroll longer to reach the content below the table.

One improvement I found interesting was to **show the primary data column** (usually the first column) and **hide the less important data (other columns) under an accordion**. This makes sense for our example, as users would first look for a name by contact and then scan for their details in the row.

<pre><code class="language-html">&lt;tr&gt;
  &lt;td onclick="toggle()"&gt;
    &lt;button aria-label="Expand contact details"&gt;
      &lt;!-- Icon --&gt;
    &lt;/button&gt;
    &lt;!-- Main content--&gt;
  &lt;/td&gt;
  &lt;td&gt;&lt;!-- Secondary content--&gt;&lt;/td&gt;
  &lt;td&gt;&lt;!-- Secondary content--&gt;&lt;/td&gt;
  &lt;td&gt;&lt;!-- Secondary content--&gt;&lt;/td&gt;
&lt;/tr&gt;
</code></pre>

We’ll assume that the first table column contains primary data, and we’ll hide other columns unless a `row-active` class is applied:

<pre><code class="language-css">/&#42; Small screen width styles &#42;/

thead tr &gt; &#42;:not(:first-child) {
  display: none;
}

tbody,
tbody tr,
tbody td {
  display: flex;
  flex-direction: column;
  word-break: break-all;
}

tbody td:first-child {
  flex-direction: row;
  align-items: center;
}

tbody tr:not(.row-active) &gt; &#42;:not(:first-child) {
  max-width: 0;
  max-height: 0;
  overflow: hidden;
  padding: 0;
}
</code></pre>

Now we have everything in place for showing and hiding table row details. We also need to keep in mind the screen reader support and toggle the `aria-hidden` property to hide secondary info from screen readers. We don’t need to toggle the ARIA property if we’re toggling the element visibility with the `display` property:

<pre><code class="language-javascript">function toggle() {
  const row = this.window.event.target.closest("tr");
  row.classList.toggle("row-active");

  const isActive = row.classList.contains("row-active");

  if (isActive) {
    const activeColumns = row.querySelectorAll("td:not(:first-child)");
    activeColumns.forEach(function (col) {
      col.setAttribute("aria-hidden", "false");
    });
  } else {
    const activeColumns = row.querySelectorAll(`td[aria-hidden="false"]`);
    activeColumns.forEach(function (col) {
      col.setAttribute("aria-hidden", "true");
    });
}
</code></pre>

We’ll assign this function to the `onclick` attribute on our main table column elements to make the whole column clickable. We also need to assign proper ARIA labels when initializing and resizing the window. We don’t want incorrect ARIA labels applied when we resize the screen between two modes.

<pre><code class="language-javascript">function handleResize() {
  const isMobileMode = window.matchMedia("screen and (max-width: 880px)");
  const inactiveColumns = document.querySelectorAll(
    "tbody &gt; tr &gt; td:not(:first-child)"
  );

  inactiveColumns.forEach(function (col) {
    col.setAttribute("aria-hidden", isMobileMode.matches.toString());
  });
}

//On window resize
window.addEventListener("resize", handleResize);

// On document load
handleResize();
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="dyKOYVr" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table - accordion [forked]](https://codepen.io/smashingmag/pen/dyKOYVr) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

This approach significantly reduces table height on smaller screens compared to the previous example. The content below the table would now easily be reachable by quickly scrolling past the table.

## Toggleable Columns Approach

Going back to our scrollable table example, in some cases, we can **give users an option to customize the table** **view** by allowing them to show and hide individual columns, temporarily reducing table complexity in the process. This is useful for users that want to **scan or compare data only by specific columns**.

We’ll use a checkbox form and have them run a JavaScript function. We’ll only have to pass an index of the column that we want to toggle. We’ll have to hide both the columns in data rows in a table body and a table header element:

<pre><code class="language-javascript">function toggleRow(index) {
  // Hide a data column for all rows in the table body.
  allBodyRows.forEach(function (row) {
    const cell = row.querySelector(`td:nth-child(${index + 1})`);
    cell.classList.toggle("hidden");
  });

  // Hide a table header element.
  allHeadCols[index].classList.toggle("hidden");
}
</code></pre>

This is a neat solution if you want to avoid the stacking pattern and allow users to easily compare the data but give them options to reduce the table complexity by toggling individual columns. In this case, we’re using a `display` property to toggle the visibility, so we don’t have to handle toggling ARIA labels.

{{< codepen height="480" theme_id="light" slug_hash="RwJoWQb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Responsive table - column toggle [forked]](https://codepen.io/smashingmag/pen/RwJoWQb) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

## Conclusion

Table complexity and design depend on the use case and the data they display. They generally rely on having enough screen space to display columns in a way user can easily scan them. There is no universal solution for making tables responsive and usable on smaller screens for all these possible use cases, so we have to rely on various patterns.

In this article, we’ve covered a handful of these patterns. We’ve focused primarily on simple design changes with a scrolling table pattern and a stacking pattern and began checking out more complex patterns that involve adding some JavaScript functionality. 

In the next article, we’ll explore more specific and complex responsive table patterns and check out some responsive table libraries that add even more useful features (like **filtering** and **pagination**) to tables out of the box.

### References

- “[Tables, CSS Display Properties, And ARIA](https://adrianroselli.com/2018/02/tables-css-display-properties-and-aria.html)”, Adrian Roselli
- “[A Responsive Accessible Table](https://adrianroselli.com/2017/11/a-responsive-accessible-table.html)”, Adrian Roselli
- “[Functions To Add ARIA To Tables And Lists](https://adrianroselli.com/2018/05/functions-to-add-aria-to-tables-and-lists.html)”, Adrian Roselli
- [Data Tables](https://inclusive-components.design/data-tables/), Heydon Pickering
- “[Table Design Patterns On The Web](https://www.smashingmagazine.com/2019/01/table-design-patterns-web/)”, Chen Hui Jing
- “[Pure CSS Scrolling Shadows With background-attachment: local](https://lea.verou.me/2012/04/background-attachment-local/)”, Lea Verou
- [Tables Caption & Summary](https://www.dropbox.com/paper/ep/redirect/external-link?url=https%3A%2F%2Fwww.w3.org%2FWAI%2Ftutorials%2Ftables%2Fcaption-summary%2F&hmac=UIbB%2BWBJu82LS4Aq3j%2Bc2mDo5wZzKF50%2F7P%2F%2BdH%2Bu%2BM%3D), Web Accessibility Initiative
- [Tables Tips And Tricks](https://www.w3.org/WAI/tutorials/tables/tips/), Web Accessibility Initiative

{{< signature "yk, il" >}}
