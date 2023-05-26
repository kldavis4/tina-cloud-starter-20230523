---
title: 'Designing Complex Responsive Tables In WordPress'
slug: designing-complex-responsive-tables-wordpress
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71269050-cf33-4fc3-8445-d90bf3393315/21-designing-responsive-tables-in-wordpress.png
date: 2019-09-24T13:00:59+02:00
summary: >-
  Back in the day when we didn’t have responsive tables, it wouldn’t have been a problem to display a complex table on mobile the same way you would on desktop. Visitors knew that they’d need to pinch to zoom in, then scroll left and right, to consume all the data within it. But we don’t have any excuse for creating poor experiences like that today. Here’s what you need to know about designing complex tables for your mobile visitors in WordPress.
description: >-
  We don’t have any excuse for creating poor experiences today. Here’s what you need to know about designing complex tables for your mobile visitors in WordPress.
categories:
  - WordPress
  - Responsive Design
disable_ads: true
disable_panels: true
---
<p>(This is a sponsored article.) Mobile devices can be problematic for displaying complex tables and charts that would otherwise stretch the entire width of a laptop or desktop screen. This may leave some of you wondering whether it’s even worth showing tables to mobile and tablet visitors of your website.</p>

<p>But that doesn’t make sense. In many cases, a table isn’t some stylistic choice for displaying content on a website. Tables are critical elements for gathering, organizing and sharing large quantities of complex and valuable data. Without them, your mobile visitors’ experience will be compromised.</p>

<p>You can’t afford to leave out the data. So, what do you do about it?</p>

<p>This requires a more strategic solution. This means understanding what purpose the data serves and then designing the <a href="https://www.smashingmagazine.com/2019/02/complex-web-tables/">complex web table</a> in a way that makes sense for mobile consumption.</p>

<p>A WordPress table plugin called <a href="https://wpdatatables.com/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19">wpDataTables</a> has made light work of designing both desktop and mobile compatible tables, so I’ve included examples of these complex tables throughout this post. Keep reading to explore the possibilities.</p>

## The Most Common Use Cases For Tables On The Web

<p>There’s a lot of value in <a href="https://www.smashingmagazine.com/2019/01/table-design-patterns-web/">presenting data in a table format</a> on a website.</p>

<p>Your writers could probably find a way to tackle each data point one-by-one or to provide a high-level summary of the data as a whole. However, when data is handled this way, your visitors are left with too much work to do, which will only hinder the decision-making process.</p>

<p>On the other hand, <strong>tables are great for organizing large quantities of data</strong> while also giving visitors an easier way to sift through the data on their own.</p>

<p>As such, your visitors would greatly benefit from having complex data sets presented as tables &mdash; across a wide variety of use cases, too.</p>

### Feature Lists

<p>There are a couple of ways to use tables to show off product features.</p>

<p>For e-commerce sites, the product inventory is broken up by its most pertinent features, allowing visitors to filter their results based on what’s most important to them:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/products-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f814faf-3730-4921-95d2-ef76f7cef49e/14-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="e-Commerce sites can use product tables to quickly list out all products and their key features. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/products-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f814faf-3730-4921-95d2-ef76f7cef49e/14-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="e-commerce product tables" >}}

<p>This would be great for any large vendor that has dozens or hundreds of similar-looking products they want customers to be able to filter and sort through.</p>

<p>You could also use a table to compare your product’s features directly against the competition’s. This would be better for a third-party marketplace where vendors sell their goods.</p>

<p><a href="https://www.amazon.com/">Amazon</a> includes these kinds of tables:</p>

{{< rimg breakout="true" href="https://www.amazon.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68039550-0e3f-4d0e-8952-4090f91e2bb1/8-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Marketplace sites use side-by-side competitor tables to simplify decision-making. (Image source: <a href='https://www.amazon.com/'>Amazon</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68039550-0e3f-4d0e-8952-4090f91e2bb1/8-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Side-by-side competitor tables" >}}

<p>By displaying the data in this format, customers can quickly do a side-by-side comparison of similar products to find the one that checks off all their requirements.</p>

### Pricing Tables

<p>If you’re designing a website where services or memberships are sold instead of products, you can still use tables to display the information.</p>

<p>You’ll find a good example of this on the <a href="https://buzzsumo.com/">BuzzSumo</a> website:</p>

{{< rimg breakout="true" href="https://buzzsumo.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650503f6-3b04-4f5c-b8f8-d7b71b60144e/20-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Companies that sell services, like BuzzSumo, use tables to display pricing and features. (Image source: <a href='https://buzzsumo.com/'>BuzzSumo</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650503f6-3b04-4f5c-b8f8-d7b71b60144e/20-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Service-based companies list prices in tables" >}}

<p>Even though there’s less data to compile, you can see how the structure of the table and the stacking of the services side-by-side really help visitors make a more well-informed and <em>easier</em> buying decision.</p>

### Catalogs

<p>A catalog is useful for providing visitors with an alphabetized or numerically ordered list. You might use one to organize a physical or digital inventory as this example demonstrates:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/catalog-of-books/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04cdcfcd-fd81-4e9e-be91-a8d04c16bdb5/17-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Catalog tables make it easier for users to find what they’re looking for. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/catalog-of-books/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04cdcfcd-fd81-4e9e-be91-a8d04c16bdb5/17-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Catalog tables" >}}

<p>This would be good for bookstores, libraries and websites that have their own repository of reference material or content.</p>

<p>You might also use a catalog to help customers improve the accuracy of their orders:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/catalog-of-drivers/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79931a34-9c04-411d-bda5-ff8eeac4d99e/6-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Catalog tables can be used to aid shoppers with order accuracy. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/catalog-of-drivers/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79931a34-9c04-411d-bda5-ff8eeac4d99e/6-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Catalogs for order accuracy" >}}

<p>This type of table provides customers with key specifications of available products to ensure they’re ordering the right kinds of parts or equipment.</p>

### Best Of Lists

<p>There are tons of resources online that provide rundowns of the “Top” winners or “Best Of” lists. Tables are a useful way to summarize the findings of the article or report before readers scroll down to learn more.</p>

<p>This is something that websites like <a href="https://www.pcmag.com/">PC Mag</a> (and, really, any tech or product review site) do really well:</p>

{{< rimg breakout="true" href="https://www.pcmag.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36a90758-3a0a-4933-b788-0cae65543a42/1-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="PC Mag organizes a summary of best-of reviews in a table format. (Image source: <a href='https://www.pcmag.com/'>PC Mag</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36a90758-3a0a-4933-b788-0cae65543a42/1-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Best-of reviews table" >}}

<p>This helps readers get a sense for what’s to come. It also allows those who are short on time to make a faster decision.</p>

### Directory Tables

<p>Directory websites have ever-growing and regularly updated lists of data. These are your real estate listing sites, travel sites, professional directories and other sites containing high volumes of complex data that really shouldn’t be consumed without a filterable table.</p>

<p>Case in point: this list of available apartments:</p>

{{< rimg href="https://wpdatatables.com/showcase/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2badf96e-f22a-4888-8aaa-3b76b835fff8/10-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption=" Directory websites that change often need tables to keep listings organized. (Image source: <a href='https://wpdatatables.com/showcase/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2badf96e-f22a-4888-8aaa-3b76b835fff8/10-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Directory website table" >}}

<p>This makes it much easier for visitors to see all options in a single glance, rather than have to go one-by-one through individual entries that matched a search query.</p>

### General Data

<p>There are other data lists that are just too complex to handle as loose text. Sports data, for instance, should always be presented in this format:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/premier-league-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e1d80bb-95a4-419d-88d8-c99bc071fad0/3-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Basic statistics, like for sports teams, should never be presented as loose data.  (Image source: <a href='https://wpdatatables.com/documentation/table-examples/premier-league-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e1d80bb-95a4-419d-88d8-c99bc071fad0/3-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Sports statistics table" >}}

<p>You can see how this keeps all data in one place and in a searchable list. Whether visitors are looking for their home team’s stats, or want to compare the performance of different teams from their fantasy sports league, it’s all right there.</p>

## How To Design Complex Responsive Tables

<p>Regardless of what type of data you’re tasked with presenting on a website, the goal is to do so in a clear fashion so visitors can take quicker action.</p> 

<p>Now, it’s time to figure out how to best format this data for mobile visitors.</p>

### Delete, Delete, Delete

<p>If your client has pulled their data from an automated report, they may not have taken time to clean up the results. So, before you start any design work on the table, I would suggest reviewing the data they’ve given you.</p>

#### First, ask yourself: Is there enough data that it warrants a table?

<p>If it’s a simple and small enough list, it might make more sense to ditch the table.</p>

#### Then, go over each column: Is each of these useful?

<p>You may find that some of the columns included aren’t necessary and can be stripped out altogether.</p>

<p>You may also find that some columns, while an essential part of each item’s individual specifications list, won’t help visitors make a decision within the table. This would be the case if the column contains an identical data point for every item.</p>

#### Finally, talk to your writer or data manager: Is there any way to shorten the columns?

<p>The table’s labels and data may have been written in full, but your writer may have a way to simplify the responses without compromising on comprehension.</p>

<p>When possible, have them work their magic to shrink up the text so that columns don’t take up as much space and more can be revealed on mobile. Don’t just do this for mobile users either. Even on desktop and tablet screens where more screen real estate is available, the shortening of labels can help conserve space.</p>

<p>It may be as simple as changing the word “Rank” to the number symbol (#) and abbreviating “Points” as “Pts”.</p>

{{< rimg breakout="true" href="https://wpdatatables.com/documentation/table-examples/premier-league-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca065ac-c552-4916-ae58-161c972b3130/7-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Designers and writers need to work together to create smaller tables. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/premier-league-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca065ac-c552-4916-ae58-161c972b3130/7-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Make data smaller" >}}

<p>While it might not seem like one word will make much of a difference, it adds up the more complex and lengthier your tables are.</p>

### Start With Two Columns

<p>By default, mobile tables should always start with two columns. It’s about all the screen’s width will allow for without compromising the readability of the data within, so it’s best to start with the basics.</p>

<p>When you contrast a full-screen table on desktop against its counterpart on mobile, you can see how easy it is to identify the two columns to include. For example, a mobile statistics table includes a column for item type and one for the profits earned from each:</p>

{{< rimg breakout="true" href="https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71269050-cf33-4fc3-8445-d90bf3393315/21-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="It’s a good idea to design responsive tables with two columns to start. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71269050-cf33-4fc3-8445-d90bf3393315/21-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Mobile table with two columns" >}}

<p>This doesn’t mean that all other data is lost on mobile. You just need to let visitors know how they can expand the table’s view.</p>

<p>In this example, when visitors select the eyeball icon above the table, they have the option to add more columns to the table:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b9247c-a2ea-4e9f-8e34-a58a2b3e8a46/11-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption=" If visitors want to scroll right, give them column view options. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b9247c-a2ea-4e9f-8e34-a58a2b3e8a46/11-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Column view options" >}}

<p>In allowing for this option on mobile, your visitors can control how they consume data while also selecting only the data points that are most important to them.</p>

<p>The result will then look like this:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6056dbb-84e2-4eaa-a9e1-839dd246270f/9-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption=" An example of a mobile table with additional columns. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6056dbb-84e2-4eaa-a9e1-839dd246270f/9-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Mobile table with more than two columns" >}}

<p>While users will have to scroll right to see the rest of the table, the control they wield over column views helps keep this a reasonable task. With just one scroll right, they’ll see the rest of the table:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc8baed-1c9a-40b7-84dc-7c58cd664bc9/12-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Even with more columns on mobile, horizontal scrolling is kept to a minimum. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/statistics-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bc8baed-1c9a-40b7-84dc-7c58cd664bc9/12-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Horizontal scrolling on mobile" >}}

<p>This is a good option to have for lists of products where the side-by-side comparison is useful in expediting the decision-making process.</p>

### Use An Accordion For Standalone Entries

<p>There’s another option you can include which will give visitors more control over how they view table content.</p>

<p>For this example, we’ll look at a list of available cryptocurrencies:</p>

{{< rimg breakout="true" href="https://wpdatatables.com/documentation/table-examples/cryptocurrencies-rank-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d13a7b26-5a7c-468f-850d-75e3568dbb49/13-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Data lists (as opposed to product comparison) lists can use expandable accordions. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/cryptocurrencies-rank-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d13a7b26-5a7c-468f-850d-75e3568dbb49/13-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Expandable accordions for mobile tables" >}}

<p>As you can see, the default here is still to only show two columns. In this case, though, a click of the plus-sign (+) will reveal a new way to view the table:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/cryptocurrencies-rank-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b2daf99-73c8-4c74-b395-f4f37fae84e1/15-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="An example of what an expanded row looks like on mobile tables. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/cryptocurrencies-rank-table/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b2daf99-73c8-4c74-b395-f4f37fae84e1/15-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Expanded row on mobile" >}}

<p>When open, all of the data that would otherwise force visitors to scroll right is now visible within a single screenful.</p> 

<p>While you can certainly include an expandable accordion in any responsive table you create, it would be best suited to ones where a direct side-by-side comparison between products or services isn’t necessary.</p>


### Keep Vertical Scrolling To A Minimum

<p>Just as you want to prevent your visitors from having to scroll past the horizontal boundaries of the mobile website’s pages, you should limit how much vertical scrolling they have to do as well.</p>

<p>Data consumption, in general, isn’t always an easy task, so the more you can minimize the work they have to do to get to it, the better.</p>

<p>One way to limit how much vertical scrolling your visitors do is by breaking a table with dozens or hundreds of rows into pages.</p>

{{< rimg breakout="true" href="https://wpdatatables.com/documentation/table-examples/monthly-summary-report-temperature/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394fe314-39ce-48f8-8cd6-f0e0345efde3/5-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="An example of how to shrink an extra-large table down to a couple columns and multiple pages. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/monthly-summary-report-temperature/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394fe314-39ce-48f8-8cd6-f0e0345efde3/5-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="A table of annual temperatures on desktop and mobile" >}}

<p>Just remember to make it easy for visitors to scroll through the pages. A well-designed set of pagination controls either at the top or bottom of the table would be useful:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/monthly-summary-report-temperature/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae2c658-6c24-43f9-aec6-8c4278373a9e/19-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Use pagination at the bottom of tables to decrease vertical scrolling. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/monthly-summary-report-temperature/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae2c658-6c24-43f9-aec6-8c4278373a9e/19-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Responsive table pagination" >}}

<p>This would be especially useful for a handful of pages. Anything more than that and the pagination process may become tedious.</p>

<p>You can also include a table search function directly above it:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/monthly-summary-report-temperature/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cca79073-b5d8-4c11-9fd7-578902705a0f/2-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Above-the-table search helps reduce the work of scrolling on mobile. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/monthly-summary-report-temperature/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cca79073-b5d8-4c11-9fd7-578902705a0f/2-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Mobile table search function" >}}

<p>This allows for a quick shortcut when your users have a good idea of what they’re looking for and want to jump straight to it.</p>

### Include Both Filtering And Sorting For Larger Data Sets

<p>So, let’s say that you have a very extensive list of data. You don’t want to force users to scroll through dozens of table pages, but you also can’t afford to remove any of the data sets. It’s all pertinent.</p>

<p>In that case, you’re going to hand some of the control back to your visitors. This way, their choices will determine how much of the table they end up seeing.</p>

<p>Let’s use this list of mutual funds as an example:</p>

{{< rimg breakout="true" href="https://wpdatatables.com/documentation/table-examples/top-mutual-funds/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/240b07bb-9d63-4a9b-b36e-853417a28787/16-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="An example of a complex table on mobile. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/top-mutual-funds/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/240b07bb-9d63-4a9b-b36e-853417a28787/16-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Complex table example" >}}

<p>The image above is the default view visitors would see if they scrolled immediately to the table. However, they might find it to be intimidating and decide that filtering out bad results will improve the view:</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/top-mutual-funds/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ada549f-60b2-489c-9541-b1088738b3ca/4-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Filtering allows users to greatly narrow down how many rows are displayed on mobile. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/top-mutual-funds/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ada549f-60b2-489c-9541-b1088738b3ca/4-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Table filters" >}}

<p>What’s nice about including filters on mobile tables is that they function the same way your mobile contact forms do. So, visitors should have an easy time filling in and moving between fields, which will get them quicker to the results they want to see.</p>

<p>Another way to improve how their results are displayed is by using the sorting feature. When they click on the top label of any column, it will automatically sort the column in descending order. Another click will reverse it.</p>

{{< rimg href="https://wpdatatables.com/documentation/table-examples/top-mutual-funds/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886a5ac2-7341-44b1-b402-86f8ff6c8b92/18-designing-responsive-tables-in-wordpress.png" sizes="100vw" caption="Sorting allows users to see results in descending/ascending order. (Image source: <a href='https://wpdatatables.com/documentation/table-examples/top-mutual-funds/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19'>wpDataTables</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886a5ac2-7341-44b1-b402-86f8ff6c8b92/18-designing-responsive-tables-in-wordpress.png'>Large preview</a>)" alt="Table sorting" >}}

<p>These two features are a must-have for any table you build, though they’re especially important for mobile visitors that don’t have as much time or attention to give to your tables.</p>

## Wrapping Up

<p>You’re here because you want a better way to present complex tables to your mobile visitors.</p>

<p>The key to doing this right is by first familiarizing yourself with the kinds of tables you can create. Even if mobile devices limit how much can be seen at first glance, that doesn’t make it impossible to share that kind of data with them.</p>

<p>Next, you need to build user control into your tables, so that visitors can decide what they see and how they see it.</p>

<p>And, finally, you’d do well to find a tool built specifically for this complex task. For those of you building websites with WordPress, <a href="https://wpdatatables.com/?utm_source=smashingmagazine.com&utm_medium=content&utm_campaign=sep19">wpDataTables</a> is a WordPress table plugin that’s able to create responsive tables and charts. It doesn’t matter how large your data set, or what use case it’s for, it will enable you to quickly and effectively organize and display responsive tables on your WordPress website.</p>

{{< signature "ms, yk, il" >}}
