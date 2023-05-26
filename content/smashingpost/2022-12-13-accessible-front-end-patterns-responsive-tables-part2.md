---
title: 'Accessible Front-End Patterns For Responsive Tables (Part 2)'
slug: accessible-front-end-patterns-responsive-tables-part2
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4ceadc-3a08-4ff7-ae9e-4e44b1054feb/accessible-front-end-patterns-responsive-tables-part2.jpg
date: 2022-12-13T15:00:00.000Z
summary: >-
  There is no universal solution for making every kind of table responsive and usable on smaller screens, so we have to rely on various patterns, which Adrian explains in this two-part series.
description: >-
  There is no universal solution for making every kind of table responsive and usable on smaller screens, so we have to rely on various patterns, which Adrian explains in this two-part series.
categories:
  - Accessibility
  - Responsive Design
---

In [Part 1](https://www.smashingmagazine.com/2022/12/accessible-front-end-patterns-responsive-tables-part1/), we explored general patterns of creating responsive and accessible tables depending on the design, use case, and data complexity. In this article, we’ll cover a few more **complex and more specific examples**, check out how we can **improve performance** on larger tables, and cover some **JavaScript libraries that can further enhance** tables with various functionalities like pagination, filtering, search, and others.

**A quick note on accessibility before we start**: *The following examples lean more toward the design aspect of responsiveness compared to the [previous article](https://www.smashingmagazine.com/2022/12/accessible-front-end-patterns-responsive-tables-part1/). I’ve used the same approach to accessibility as I did in the examples from the previous article. Still, as these are more complex and specific examples, further testing and adjustments might be required for these use cases, and I strongly encourage them.*

That being said, let’s dive into the examples.

## Working With Complex Enterprise Tables

Enterprise data tables display a large amount of complex data across lots of columns, and they rely on searching and filtering to quickly find the data we’re looking for. We’re not going to cover those actions in this article because they do not affect responsiveness and only serve to reduce the number of displayed rows. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5cf89c6-548c-4915-9e32-da3f4b280560/1-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5cf89c6-548c-4915-9e32-da3f4b280560/1-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="513" sizes="100vw" caption="Searching, filtering, ordering, and other table enhancements would help users scan through this complex table which contains various data types in various formats. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5cf89c6-548c-4915-9e32-da3f4b280560/1-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="An example of a complex table which contains various data types in various formats" >}}

The responsive patterns that we covered in the previous article won’t completely solve the UX issue here. The stacking and accordion pattern, for this case, might be too clunky for mobile use, and the scrolling pattern would make the table unusable and difficult to scan.

[Lalatendu Satpathy suggests in his article](https://uxdesign.cc/data-table-for-enterprise-ux-cb48fb9fdf1e) about designing enterprise tables to use the stacking context but display only the critical data that the user will most likely want to search for.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aadfed48-b46f-4ffe-b4fa-067e466237f7/2-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aadfed48-b46f-4ffe-b4fa-067e466237f7/2-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="657" sizes="100vw" caption="Some fields are hidden, and the table layout is simplified to critical data to allow for easier scanning. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aadfed48-b46f-4ffe-b4fa-067e466237f7/2-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="A table where some fields are hidden and the layout is simplified to critical data to allow for easier scanning" >}}

Once users have found a row they were looking for, either by scanning, searching, or filtering, they can open up the details view by tapping the row.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa334f3d-820b-41b4-ba0e-1eb5b3ac731b/3-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa334f3d-820b-41b4-ba0e-1eb5b3ac731b/3-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="629" sizes="100vw" caption="Off-canvas element contains a complete view of the row data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa334f3d-820b-41b4-ba0e-1eb5b3ac731b/3-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="Off-canvas element contains a complete view of the row data" >}}

Notice how we’re utilizing the limited screen space to the fullest extent for each operation &mdash; we’re showing as many data rows as possible, which contain only primary information, and then we are using an off-canvas element, a full-page element to display all data for a single row.

We’re using the recommended markup for the table element and ARIA labels that we’ve covered in the [previous article](https://www.smashingmagazine.com/2022/12/accessible-front-end-patterns-responsive-tables-part1/), so let’s focus on the off-canvas element. First, let’s create a hidden off-canvas element and add empty elements where we’ll append row data for the row that has been clicked on.

<div class="break-out">

<pre><code class="language-html">&lt;aside id="offcanvas" class="offcanvas" aria-hidden="true"&gt;
  &lt;header class="offcanvas-header"&gt;
    &lt;button tabindex="-1" onclick="closeOffcanvas()" aria-label="Return to table"&gt;&lt;!-- ... --&gt;&lt;/button&gt;
&lt;/header&gt;
  &lt;div&gt;&lt;strong id="slot-1"&gt;&lt;/strong&gt;&lt;/div&gt;
  &lt;h1 id="slot-2"&gt;&lt;/h1&gt;
  &lt;dl&gt;
    &lt;dt&gt;Available stock&lt;/dt&gt;
    &lt;dd id="slot-3"&gt;&lt;/dd&gt;
   &lt;!-- ... --&gt;
  &lt;/dl&gt;
&lt;/aside&gt;</code></pre>
</div>

We’re using CSS to make sure that this element only displays on smaller viewports. On larger viewports, even though the off-canvas element could be activated, it won’t be displayed. Alternatively, we could have also used JavaScript’s match media element to prevent the function from running.

<pre><code class="language-css">@media screen and (max-width: 1260px) {
  .offcanvas {
    display: block;
  }
}
</code></pre>

Let’s move onto the row click handle function, which populates off-canvas element slots and applies an active class. We are populating the off-canvas slots by iterating over columns and using an index to target the id-s. Additionally, we are removing the `aria-hidden` attribute and moving the focus onto the element. We can also use [focus trapping](https://css-tricks.com/focus-management-and-inert/#aa-focus-trapping) to prevent the user from leaving the off-canvas element while it’s opened.

<pre><code class="language-javascript">function openAndPopulateAside() {
  if(offcanvas.classList.contains("offcanvas-active")) {
    return;
  }
  
  const row = window.event.target.closest("tr");
  const columns = Array.from(row.children);

  columns.forEach(function (child, i) {
    const id = `slot-${i + 1}`;
    document.getElementById(id).innerHTML = child.innerHTML;
  });
 
  offcanvas.classList.add("offcanvas-active");
  offcanvas.removeAttribute("aria-hidden",);
  offcanvas.querySelector("button").tabIndex = undefined;
  offcanvas.focus();
}
</code></pre>

We also need to have a way to close the off-canvas element and undo the changes we applied when we activated the modal.

<pre><code class="language-javascript">function closeOffcanvas() {
  offcanvas.setAttribute("aria-hidden", "true");
  offcanvas.classList.remove("offcanvas-active");
  offcanvas.querySelector("button").tabIndex = -1;
  document.getElementById("table-wrapper").focus();
}
</code></pre>

In these examples, we’re relying on additional elements outside of tables (like our off-canvas element) to help us make full use of the available screen space to fully display table data. Check out the following CodePen example and see how these elements work together to improve table UX on smaller screens.

{{< codepen height="480" theme_id="light" slug_hash="oNyaLZj" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Enterprise table [forked]](https://codepen.io/smashingmag/pen/oNyaLZj) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}  

{{% feature-panel %}}

## Adapting A Table For Vertical And Horizontal Scanning On Smaller Viewports

Following the suit of the previous example, we’ll focus even more on the two user actions when scanning tables: **vertical scanning** (searching for data) and **horizontal scanning** (reading column data for the selected row).

[Joe Winter covers this approach in his article](https://uxdesign.cc/designing-a-complex-table-for-mobile-consumption-nom-7472f7b11fe6), where he designed a mobile view for a very complex data table.

<blockquote>“The game changer in this project was the realization that users don’t need to view a large data set all at once. By focusing on the discrete steps of how information is consumed, we were able to limit the presented content to the absolutely relevant.”<br /><br />&mdash; Joe Winter</blockquote>

Let’s break down those steps and see what we’re going to build:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf4bdbb-e193-4b8a-9117-00546d640a28/4-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf4bdbb-e193-4b8a-9117-00546d640a28/4-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="586" sizes="100vw" caption="Table which compares review scores from different review sites for recently released video games. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf4bdbb-e193-4b8a-9117-00546d640a28/4-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="Table which compares review scores from different review sites for recently released video games" >}}

Comparing this to the previous example, the only primary column is the title & platform column. We cannot pick any other column to include for comparison since they are equally important and depend on user preference. Using a stacked column approach is also not an option, as we want users to compare the review scores to different games and between the review sites. This table is also too complex for a scrollable table, as both the primary column and table headers are equally important. It would take too much screen space if we used the fixed-column approach.

Let’s tackle this problem with the approach described in Joe Winter’s article. First, **let’s focus on vertical scanning**.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7afc4bdb-21dd-4221-813a-7cd9d984a06d/5-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7afc4bdb-21dd-4221-813a-7cd9d984a06d/5-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="604" sizes="100vw" caption="This view allows user to choose their preferred review site and compare scores between various games (vertical scanning). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7afc4bdb-21dd-4221-813a-7cd9d984a06d/5-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="A view with vertical scanning" >}}

Let’s give users **an option to choose the additional column** they’ll use for comparison &mdash; their preferred review game review site. We’ll use a `select` element in this case, but tabs and other similar controls work well. We can **store their preference in local storage** if we want to keep track of user preferences and store it for future use.

<pre><code class="language-html">&lt;form&gt;
  &lt;label for="filter"&gt;Review site&lt;/label&gt;&nbsp;
  &lt;select onchange="filterChange()" id="filter"&gt;
    &lt;option value="1"&gt;GameSpot&lt;/option&gt;
    &lt;option value="2"&gt;IGN&lt;/option&gt;
    &lt;option value="3"&gt;Dexerto&lt;/option&gt;
    &lt;option value="4"&gt;GameInformer&lt;/option&gt;
    &lt;option value="5"&gt;VG247&lt;/option&gt;
  &lt;/select&gt;
&lt;/form&gt;
</code></pre>

<div class="break-out">

<pre><code class="language-javascript">const allBodyRows = document.querySelectorAll("tbody &gt; tr");
const mainHeadCols = document.querySelectorAll("thead &gt; tr:last-child &gt; th");

function filterChange() {
  const value = parseInt(select.value);

  mainHeadCols.forEach(function (col, i) {
    const colIndex = i + 1;

    // Skip the first (primary column).
    if (i == 0) {
      return;
    }

    if (colIndex === 1 || colIndex === value + 1) {
      col.classList.remove("hidden");
    } else {
      col.classList.add("hidden");
    }
  });

  allBodyRows.forEach(function (row) {
    const cols = row.querySelectorAll("td");

    cols.forEach(function (col, i) {
      const colIndex = i + 1;

      if (colIndex === value) {
        col.classList.remove("hidden");
      } else {
        col.classList.add("hidden");
      }
    });
  });
}</code></pre>
</div>

Next, we’ll implement the same off-canvas element as we did in the previous example to cover the horizontal scanning, where we display all column data for a selected row.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d8580c9-49f1-4bff-b000-fc79c2b41537/6-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d8580c9-49f1-4bff-b000-fc79c2b41537/6-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="580" sizes="100vw" caption="Single row view allows user to compare review scores for a single game between different review sites (horizontal scanning). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d8580c9-49f1-4bff-b000-fc79c2b41537/6-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="Single row view with horizontal scanning" >}}

We’ll use a very similar function and go through the same motions of opening, populating, and closing the off-canvas element.

<pre><code class="language-javascript">function openAndPopulateAside() {
  const row = this.window.event.target.closest("tr");
  const columns = Array.from(row.children);

  columns.forEach(function (child, i) {
    const id = `slot-${i + 1}`;
    document.getElementById(id).innerHTML = child.innerHTML;
  });
 
  offcanvas.classList.add("offcanvas-active");
  offcanvas.removeAttribute("aria-hidden");
  offcanvas.querySelector("button").tabIndex = undefined;
  offcanvas.focus();
}

function closeOffcanvas() {
  offcanvas.setAttribute("aria-hidden", "true");
  offcanvas.classList.remove("offcanvas-active");
  offcanvas.querySelector("button").tabIndex = -1;
  document.getElementById("table-wrapper").focus();
}
</code></pre>

We’ve improved upon the previous example by giving users an option to select an additional primary column alongside the “Title & Platform” so users can select which column will be used for comparison between the rows.

{{< codepen height="480" theme_id="light" slug_hash="BaVqLMg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Horizontal / Vertical scanning [forked]](https://codepen.io/smashingmag/pen/BaVqLMg) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}  

{{% ad-panel-leaderboard %}}

## Transforming A Calendar Table Into A List & Map On Smaller Viewports

Another interesting use case for tables is a calendar. You’ve probably seen and even used those apps out there. Calendars can be represented by a table element, but how can we make them responsive? 

For **simple use-cases** where calendars have just a presentational role, we can scale down the dimensions as much as we need. We covered a similarly simple example in the [previous article](https://www.smashingmagazine.com/2022/12/accessible-front-end-patterns-responsive-tables-part1/), where we used fluid spacing and fluid typography to scale down the dimensions on smaller screens.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/927658d1-b1b3-414a-aea9-2e16ea39c2cf/7-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/927658d1-b1b3-414a-aea9-2e16ea39c2cf/7-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="512" sizes="100vw" caption="<a href='https://www.calendar-365.com/2022-calendar.html'>Calendar-365</a> uses table HTML elements to create calendar tables. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/927658d1-b1b3-414a-aea9-2e16ea39c2cf/7-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="Calendar-365 which uses table HTML elements to create calendar tables" >}}

But what about more **complex calendars used for planning and schedule**? They can contain a variable amount of information within the cells, and scaling them down for mobile is not always viable.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e352be6-562c-49c1-b48c-9cfdce8c6a10/8-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e352be6-562c-49c1-b48c-9cfdce8c6a10/8-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="446" sizes="100vw" caption="This project has each day divided into 1-hour slots. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e352be6-562c-49c1-b48c-9cfdce8c6a10/8-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="An example of a complex calendar where each day is divided into 1-hour slots" >}}

We could either use the stacking pattern or scrolling pattern, but they’re not ideal for this calendar project. User needs to see their schedule for today and at least for the next day and have a general overview (a summary) for a wider timespan.

We can divide the large calendar app into two elements on the smaller screens:

- **List element**: the schedule for today and the next day;
- **Table element**: general, high-level, 5-day overview.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6284fa3e-f1ec-4d71-8ffa-aab3a6edd224/9-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6284fa3e-f1ec-4d71-8ffa-aab3a6edd224/9-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="572" sizes="100vw" caption="Both elements represent individual user actions when using a calendar on mobile. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6284fa3e-f1ec-4d71-8ffa-aab3a6edd224/9-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="A large calendar app divided into two elements: a list element and a table element " >}}

There are too many differences between the large screen and small screen views, so there is no smart way of using CSS to transform between the two. We need to duplicate the element and make sure to hide the inactive element with CSS. This will also hide it from screen readers and make the element not accessible with the keyboard.

<pre><code class="language-html">&lt;figure class="table-wrapper"&gt;
  &lt;figcaption id="caption"&gt;
    &lt;h1&gt;Consultation schedule&lt;/h1&gt;
  &lt;/figcaption&gt;

  &lt;table aria-labelledby="caption" class="table-full"&gt;
    &lt;!-- ... --&gt;
  &lt;table&gt;

  &lt;ol class="list"&gt;
    &lt;!-- ... --&gt;
  &lt;/ol&gt;

  &lt;table aria-labelledby="caption" class="table-map"&gt;
    &lt;!-- ... --&gt;
  &lt;/table&gt;
&lt;/figure&gt;
</code></pre>

<pre><code class="language-css">@media screen and (min-width: 960px) {
  .table-map, .list {
    display: none;
  }
}

@media screen and (max-width: 959px) {
  .table-full {
    display: none;
  }
}
</code></pre>

These two views can be easily generated with JavaScript or JavaScript frameworks like React and Svelte, but also with static HTML generators.

{{< codepen height="480" theme_id="light" slug_hash="yLERVNg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Table to list + map [forked]](https://codepen.io/smashingmag/pen/yLERVNg) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}} 

## Performance Optimization For Large & Complex Data Tables

Complex tables and a large amount of data displayed within them might result in browser performance issues. With complex enterprise tables, it’s easy for a DOM tree to grow very large and slow down the browser, rendering the page barely usable or completely unusable. Lighthouse will throw a warning if the body element contains more than 800 nodes and [an error if it contains more than 1400 nodes](https://web.dev/dom-size/#how-the-lighthouse-dom-size-audit-fails).

For example, let’s say that we have an enterprise table consisting of 60 rows and 12 columns, so we have **at least 780 DOM elements** already (720 table cells + 60 table row elements). We’ve got close to the point where **Lighthouse would throw a warning**, and we’re a bit less than halfway to reaching the recommended upper limit. And that is without counting the other elements on the page!

How can we deal with rendering large tables and avoiding performance issues on large data tables?

### Pagination

One solution would be to implement pagination on a table and limit how many rows are being rendered. Many JavaScript libraries like [Tabulator](https://tabulator.info/) and UI component libraries like [Material UI](https://mui.com/material-ui/api/table-pagination/) offer this feature out of the box.

We only need to make sure to take table dimensions into account when setting the options for how many data rows are visible per page to avoid the aforementioned issue.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6489e2b-881a-4901-bf30-1519f9420848/10-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6489e2b-881a-4901-bf30-1519f9420848/10-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="269" sizes="100vw" caption="React component library <a href='https://mui.com/material-ui/api/table-pagination/'>Material UI (MUI)</a> offers a paginated table component and virtualization (which we’ll cover next) out of the box. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6489e2b-881a-4901-bf30-1519f9420848/10-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="A paginated table component" >}}

However, **pagination is not an ideal fit for all tables** and data types. Sometimes we just want to display the whole table and allow users to scroll the entire data table without restrictions or interruptions. What can we do if we need to display the whole table regardless of the number of rows and columns?

### Virtualization

We can use [virtualization](https://www.patterns.dev/posts/virtual-lists/). We **keep the entire table data in memory but dynamically render table rows and columns that are currently visible** to the user. We update the state while the user is scrolling and interacting with the table, all the while maintaining the illusion that every row and column is present by changing inner dimensions to compensate for missing elements.

This can be seen in the example below, where we render out only a handful of rows in DOM out of a total of 100,000 rows! Notice the inlined height style attribute on the second `tr` element.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/035f231a-c28a-480a-9edb-347d2a36f813/11-accessible-front-end-patterns-responsive-tables-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/035f231a-c28a-480a-9edb-347d2a36f813/11-accessible-front-end-patterns-responsive-tables-part2.png" width="800" height="269" sizes="100vw" caption="<a href='https://clusterize.js.org/'>Clusterize.js</a> library renders visible rows only and dynamically adds additional vertical space for rows that are not currently rendered. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/035f231a-c28a-480a-9edb-347d2a36f813/11-accessible-front-end-patterns-responsive-tables-part2.png'>Large preview</a>)" alt="Clusterize.js library renders visible rows only and dynamically adds additional vertical space for rows that are not currently rendered" >}}

The same approach can be used for large lists and various other HTML elements. There are some specialized virtualization libraries like [Clusterize.js](https://clusterize.js.org/) if you’re looking to implement just that in your project, but many popular JavaScript table libraries like [Tabulator](https://tabulator.info/) and component libraries support this out of the box.

If you want to read more about the effectiveness of table virtualization, [Robert Cooper of Basedash published a case study](https://www.basedash.com/blog/how-virtualization-increased-our-table-performance-by-500-percent) on how table virtualization introduced significant improvements to their React project.

<blockquote>The root cause of the problem was that we were trying to render the entire table at once, even if most of the data for the table was off the screen/viewport. Also, the React code for rendering a single table cell was quite inefficient, so when we needed to render thousands of table cells on initial load, all those inefficiencies compounded. (…)<br /><br /> Overall, after implementing both virtualization and improvements to our table cell, we were able to speed up table load times by 4-5x in most cases and over 10x in extreme cases. All while increasing the default page size from 50 rows to 100.</blockquote>

Depending on the approach you choose, either by implementing virtualization yourself or by using an existing library, make sure to **test if the solution is accessible** for your use-case &mdash; both for keyboard navigation and for assistive devices.

### CSS approach

Interestingly enough, there is a non-JS way to optimize table render performance. We can try to apply `CSS contain: strict` to the table element to signal that the massive table won’t affect the style or layout of any other elements on the page. 

This is exactly how [Johan Isaksson improved the performance](https://medium.com/@johan.isaksson/how-i-made-googles-data-grid-scroll-10x-faster-with-one-line-of-css-78cb1e8d9cb1) (on his machine) of Google Search Console, which wasn’t using virtualization at the time, after experiencing issues browsing a table with 500 rows (which resulted in over 16,000 DOM elements being rendered).

However, this is not a universal and perfect solution, and depending on your use case, it [might cause visual bugs](https://css-tricks.com/almanac/properties/c/contain/#aa-strict), especially if you are dealing with a dynamic table that can be filtered, search, and reordered.

<blockquote>As the “strictest” of the containment values, this value should be used with careful consideration. This is due to the dimension requirements it imposes on the contained element. With these requirements, this containment value does offer the most potential performance benefits of containment.</blockquote>

If you are working with dynamic tables, which is often the case with enterprise data, you’d want to **either use pagination or virtualization**, depending on the design and use case, to create fully optimized complex data tables that perform optimally.

{{% ad-panel-leaderboard %}}

## JavaScript Libraries For Enhancing Tables

Additional table features like searching, filtering, ordering, and others can improve table UX even on smaller screens by allowing users to easily scan the table and quickly find the information that they’re looking for. There are so many JavaScript-based solutions out there, both specialized and as part of a larger UI components library, and I’d like to highlight some of them here.

[Tabulator](https://tabulator.info/) is a zero-dependency vanilla JavaScript library for enhancing tables with a plethora of aforementioned functionalities and more. It also features separate NPM packages for React, Angular, and Vue. If you are working on a project that heavily features tables and requires lots of features and interactions, Tabulator can do a lot of heavy lifting for you.

As for the framework-specific libraries, I’ve only used [react-table](https://react-table-v7.tanstack.com/), which worked wonderfully on the projects I’ve worked on. It’s fully implemented with React hooks, so it’s fully customizable and doesn’t enforce any markup, design, or HTML structure.

As for table virtualization specifically, [Clusterize.js](https://clusterize.js.org/) is a solid vanilla JS solution that works well and has been recently updated in the last year at the time of writing. As for the framework-specific library, there is [react-virtualized](https://github.com/bvaughn/react-virtualized), but it [hasn’t been updated](https://github.com/bvaughn/react-virtualized/issues/1778) for a while so make sure to test if it fits your use case before committing to using it on your project.

Keep in mind that you should always consult [Bundlephobia](https://bundlephobia.com/) to see package size and dependencies, and make sure to check out the package repository to see if the package is currently being maintained and if the issues raised are being actively addressed. 

## Conclusion

Creating responsive and accessible tables requires a careful and thoughtful approach, so the table remains usable even on smaller screen sizes. In this article, we’ve covered some highly specific use cases and approaches like an enterprise data table and a calendar. Large & complex data tables may introduce performance issues due to the DOM tree growing too large, so we need to use either pagination or table virtualization to avoid the potential issues. In conclusion, make sure that, regardless of the design and use case, your tables are responsive, usable, accessible, and performant on various types of devices and screen sizes.

### References

- “[Design better data tables](https://medium.com/nextux/design-better-data-tables-4ecc99d23356)”, Andrew Coyle
- “[How I made Google’s data grid scroll 10x faster with one line of CSS](https://medium.com/@johan.isaksson/how-i-made-googles-data-grid-scroll-10x-faster-with-one-line-of-css-78cb1e8d9cb1)”, Johan Isaksson
- “[Designing a complex table for mobile consumption (nom)](https://uxdesign.cc/designing-a-complex-table-for-mobile-consumption-nom-7472f7b11fe6)”, Joe Winter
- “[Designing better data tables for enterprise UX](https://uxdesign.cc/data-table-for-enterprise-ux-cb48fb9fdf1e)”, Lalatendu Satpathy
- “[Avoid an excessive DOM size](https://web.dev/dom-size/#how-the-lighthouse-dom-size-audit-fails)”, web.dev
- “[How virtualization increased our table performance by 500%](https://www.basedash.com/blog/how-virtualization-increased-our-table-performance-by-500-percent)”, Robert Cooper
- “[List Virtualization](https://www.patterns.dev/posts/virtual-lists/)”, patterns.dev

{{< signature "yk, il" >}}
