---
title: Advanced Power Tips For WordPress Theme Developers
slug: advanced-power-tips-for-wordpress-template-developers
image: null
date: 2009-11-25T14:49:26.000Z
author: jacob-goldman
description: >-
  Back in July, [Power Tips for WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/) presented 8 basic techniques for adding popular features to the front end of a WordPress-powered website. The premise was that WordPress has become an elegant, lightweight content management solution that offers the _fundamentals_ out of the box,
  atop a modular core that offers incredible potential in the hands of a capable developer.
categories:
  - WordPress
  - PHP
  - Templates
  - Techniques (WP)
---
WordPress does not try to be an "everything to everyone" CMS right out of the box. Many systems do an average job incorporating 99% of what the potential CMS market <em>might</em> need, even if the last 15-20% is used only by a fraction of the market and adds considerably to the system’s overall "heft" (or bloat).

At the other end of the spectrum are completely custom solutions that are finely tailored to exact needs, at the cost of reinventing wheels like polished content editing with media management and version control.</p>

The self-proclaimed WordPress "code poets" have, alternatively, focused on doing an A+ job with the “fat middle”: the 80-85% of features that almost everyone needs, and coupling those with a first rate framework and API that enables capable developers to add in almost any niche or "long tail" feature.

In fact, the core WordPress framework is so capable that a handful of <a title="WordPress frameworks" href="https://www.smashingmagazine.com/2009/05/27/wordpress-theme-development-frameworks/">"intermediary" frameworks</a> that sit on top of it have already emerged.

{{% feature-panel %}}

That previous "Power Tips" entry scratched the surface, covering a handful of API calls mixed in with some simple PHP code and configuration tips intended to help beginner WordPress template developers kick their game up a notch. This article takes power tips to the next level, expanding on some of the topics in the first article, and <strong>introducing more advanced techniques and methods for customizing not only the front end, but the <em>content management</em> (or back end) experience</strong>.</p>

## Multiple Column Content Techniques

The average blog or website has a single, clearly defined block of space for a given page's or post's unique content. But <strong>there are plenty of creative websites that don’t conform to this simple notion of "one unique block" per page</strong>. A creative online portfolio layout might feature a screenshot and project description in a left column, and a list of technologies used in a right column. Both the left and right column are unique to each portfolio page.

Here's a screenshot from an in-development website project, built on WordPress. The "projects" area features portfolio-like layouts of green building projects throughout the state. In addition to a specially designed gallery visualization, note that the individual project profile has two distinct columns.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19110" title="Rhode Island Green Building Council - 2 Column Layout" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78c7cf6d-7e48-4e98-a2e9-80e5fb4878cd/rigbc-2-column.jpg" alt="Rhode Island Green Building Council - 2 Column Layout" width="500" height="478" />

A more commonplace layout might feature an obvious, primary block of page content, but also feature a sidebar element that is unique to the current page: maybe a quote from a customer about a specific product or service. The <a href="https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/">"Power Tips" article</a> offered a method to associate sidebar elements with multiple pages using custom fields and page IDs (tip #6). That approach isn't very effective or efficient for designs with a 1:1 relationship between sidebars and pages (where each page has a unique sidebar element).

<a href="https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19111" title="Sidebar HTML elements - using page IDs and custom fields" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b52393f-d66b-47a1-8e4a-ca2520fd8f4b/sidebars.jpg" alt="Sidebar HTML elements - using page IDs and custom fields" width="500" height="206" /></a>

Yes, the developer could <a href="https://wordpress.org/extend/plugins/mce-table-buttons/">add table buttons to the WordPress editor</a>, and let content authors fend for themselves: a solution prone to problematic layouts and bad output relied upon far too often. Here are a few simple options that keep layout in the hands of the template developer while making content management easier and problem-free.</p>

### Short, simple, and HTML free? No worries.

Before we delve into solutions that assume a need for HTML formatting in this second content block, let’s review a more basic solution. If the second column does not need to be formatted – or maybe <em>should not</em> be formatted by the editor for design reasons – then a simple custom field will do the trick. In the case of a simple sidebar element, like a customer quote, this may be just the trick.

There are already <a href="https://www.kriesi.at/archives/how-to-use-wordpress-custom-fields">great tutorials</a> and <a href="https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/">useful custom fields hacks</a> that walk through the WordPress custom fields feature, so if you are not familiar with the basic idea behind custom fields, start there. Let’s go ahead and create a custom field named "sidebar_content" (also known as the "key"), and put some simple content in there. Just to shake things up, let's assume we <em>do </em>need a very basic HTML feature for our content authors, who know nothing about HTML: line and paragraph breaks. Let's also assume that we want to format this sidebar content on the front end with some of the basic automatic niceties we get when we output post content, like curly quotation marks.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19114" title="Custom field with sidebar_content key" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36df9981-03d9-4812-93d8-6b1d248b9dfb/sidebar-custom-field.gif" alt="Custom field with sidebar_content key" width="500" height="236" />

Here’s how we can output this in any template file, using the <a href="https://codex.wordpress.org/Plugin_API/Filter_Reference/the_content">"the_content" filter</a> to apply the WordPress content filter to our custom field. That filter converts single line breaks to break tags, double line breaks to paragraphing tags, and even transforms simple quotation marks to curly quotes!

<pre><code class="language-php">$sidebar_content = get_post_meta($post-&gt;ID, "sidebar_content", true);

if ($sidebar_content) {
   echo '&lt;div id="sidebar_content"&gt;';
   echo apply_filters("the_content", $sidebar_content);
   echo '&lt;/div&gt;';
}</code></pre>

Of course, we can make this even more intuitive for the content authors by creating a new meta field box for sidebar content instead of relying on the generic "custom fields" box… which will be covered later in this article!

### Using the More Tag for… More

The WordPress editor has a button "more tag" button that is primarily intended to separate "above the fold" content from "below the fold" content. If you are not already familiar with the "more" divider, <a title="WordPress more divider" href="https://codex.wordpress.org/Customizing_the_Read_More">read up on that</a> first.

If the pages or posts that need a two column layouts <em>also </em>rely on traditional more separation, this tip will most likely not be effective, unless one of the columns is also the intended "above the fold" content. However, most instances where a two column layout is desirable don't overlap with a traditional above / below the fold need. It is fairly rare, for instance, for pages (vs. posts) to actually make <em>any </em>use of the more tag. So let’s start taking advantage of that feature!

<strong>The basic idea is that content above the more divider will represent one block of HTML content, while content below the divider will represent a second block</strong> (be it a sidebar element or column).

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19133" title="Enabled two columns using the more divider" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1dd19ff-bc7a-4b39-8eac-e067bf89fe4c/sidebar-using-more-tag.gif" alt="Enabled two columns using the more divider" width="500" height="286" />

Here is how to retrieve content above and below the more divider as separate blocks of HTML content in the corresponding page template file.

<pre><code class="language-php">global $more;

$more = 0;
echo '&lt;div id="column_one"&gt;';
the_content(’);
echo '&lt;/div&gt;':

$more = 1;
echo '&lt;div id="column_two"&gt;';
the_content(’,true);
echo '&lt;/div&gt;';</code></pre>

The global "more" variable lets WordPress know whether or not the content is being rendered in an "above the fold" (or "teaser") only view. By passing an empty string to <a href="https://codex.wordpress.org/Template_Tags/the_content">"the_content"</a>, we prevent a "read more" link from showing up below the HTML content. And, for column two, we pass a second parameter to "the_content" – <em>true</em> – which instructs WordPress to output the content without the teaser.

If the intent is to output the second block of content outside of the loop in another template element, such as a sidebar, this approach is a bit trickier. One option would be to store the second block of content in a uniquely named variable, declare it as a global variable in the sidebar, and – if there is any content inside the variable – output a new block. An alternative could involve checking which page template is in use with the <a href="https://codex.wordpress.org/Conditional_Tags#Is_a_Page_Template">"is_page_template" function</a>, and, if the two column template is in use, calling "the_content" with the second parameter set to true, as in the example above.</p>

### The Plug-in Solution: Adding a Second HTML Content Block to the Editor

The ideal solution, of course, might be a second HTML editor field on the WordPress page or post editor. Unfortunately, no such plug-in existed… until recently! While writing this article, we decided it was time such a solution did exist, and so the author of this article is happy to present a free, open source plug-in that combines some savvy understanding of how TinyMCE works (hint: it's as simple as a class name) with the custom meta box tutorial covered later in this article, and a little bit of extra customization and polish thrown into the mix.

<strong><a href="https://wordpress.org/extend/plugins/secondary-html-content/">Secondary HTML Content</a> adds a second HTML editor to pages, posts, or both</strong> (customizable with a simple settings panel). You can output the content in a sidebar with an included widget, or integrate it more tightly with the template by using "the_content_2" and "get_the_content_2" functions.

<a href="https://wordpress.org/extend/plugins/secondary-html-content/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19137" title="Secondary HTML Content for WordPress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bdd1d7c-01ec-48c1-a293-c54888598da7/secondary-html.jpg" alt="Secondary HTML Content for WordPress" width="480" height="529" /></a>

## Associating Pages with Post Content: Reloaded

<a href="https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/">"Power Tips"</a> covered the basic foundation for associating different WordPress pages with different post categories. <strong>The basic premise was that many sites require, effectively, different post "feeds" on different pages.</strong> For instance, there may be a company blog, but there may also be an independent news feed.

This continuation offers specific tips that extend the core concept introduced in part 1, making it easier to have multiple page / category associations, preventing entrance into the "real" category archive, and ensuring that individual post views retain a visual and architectural association with their parent "category page" layout.

Be sure to <a href="https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/">read part 1</a> before proceeding.</p>

### A Review of the Basics & the Two Fundamental Approaches

At the heart of the category / page association (covered in part one) was:

*   A matching of the "page slug" with the "category slug."
*   Using "[query_posts](https://codex.wordpress.org/Template_Tags/query_posts)" and the category parameter to exclude standalone page categories from the primary feed
*   Using a dedicated page template with "query_posts" and the "category name" parameter to create a page featuring a feed for a single category.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19139" title="WordPress category / page slug relationship" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea8afc8-0b45-4c51-afcc-e6c7a5044483/wp-cat-config.gif" alt="WordPress category / page slug relationship" width="500" height="333" />

Before delving into the tips that extend those ideas, it is important to make a distinction between two common but fundamentally different use cases for page / category association. The more <strong>typical use case, which the first part was tailored to, is a website that has a primary feed, like a blog, but also has one or two distinct feeds</strong>, most often for a formal news or press feed.

<strong>The second use case is a bit more esoteric: there is <em>no</em> primary feed</strong>. The site has many pages, and many (but not all) of those top level pages are individual feeds of posts. The example, at the end of this power tip, <a href="https://www.m62.net"><em>m62.net</em></a>, is one such use case. Another common use case might be – again – a portfolio centric website.

Let’s say we want to create "Joe’s Portfolio", and Joe wants to feature 4 distinct areas of expertise. Each area of expertise should be a top level page, say, <em>joes-portfolio.com/web-design</em>, <em>joes-portfolio.com/graphic-design</em>, etc. Joe wants to have a little write-up about each service area at the top of the page, followed by a feed of case studies. Why a feed instead of sub-pages? Maybe Joe wants prospects to be able to subscribe to an RSS feed for each area of expertise; maybe he wants to easily cross-tag case studies based on industry; maybe he plans to update frequently and doesn’t want a huge page sitemap or wants visitors to page through a date-organized collection of case studies. There are many reasons to use posts instead of pages.

The following tips provide solutions for both use cases.</p>

### Automatically Determining the Page / Category Association

Part one suggested that a unique page template be created for any page associated with a category. That page template would then query for posts using a hardcoded category name or category ID. If there are only one or two standalone "category pages", this is an efficient and effective solution.

However, if there are many page / category associations, as in use case #2 (no primary feed), the process of manually creating page templates for each association is tedious to build and maintain, and not realistic if content editors who don't program need to be able to create more page / category associations on demand.

An alternative would be to <a href="https://codex.wordpress.org/Pages#Creating_Your_Own_Page_Templates">create a generic page template</a>, let’s say "template-category-connector.php", that is assigned to all pages associated with a category, and <em>automatically </em>determines the right category to query.

The following code performs the matching and executes the post query. The magic happens by taking advantage of our matching page and category slugs. Once again, if the website does not use permalinks, an alternative approach will be required (one permalink-free alternative could involve a custom field with the associated category ID).

<pre><code class="language-php">$cat = get_category_by_slug($post-&gt;post_name);
query_posts('cat='.$cat-&gt;term_id);</code></pre>

That’s all there is to it... just proceed on with the <a href="https://codex.wordpress.org/The_Loop"> post loop</a> to output the applicable category's posts. Note that the template should probably check for an actual return value from line 1, and output a graceful error in the event there is no match.</p>

### Handling Entry into the "Real" Category Archive

Now that there is a dedicated page layout that handles the category feed, we will want to be make certain that the visitor doesn’t land on WordPress' default category "archive" view. For instance, when using permalinks with the default "category base" value, the archive view for a category with a top level category assigned a “web-design” slug would be: <em>mysiteurl.com/category/web-design</em>. However, the intent is for visitors to view this category at our top level page: <em>mysiteurl.com/web-design</em>.

<strong>By combining the WordPress category template file with some smart redirects, we can prevent entry into the default category archive.</strong> Out of the box, the <a href="https://codex.wordpress.org/Template_Hierarchy#Category_display">WordPress template system</a> allows developers to create global category archive templates as well as templates for individual category archives.

If we are in use case #1 – a site with a traditional blog feed and a standalone news feed on a "press releases" page – we will want to use the latter solution. Let's say, as in part one, the category ID for "press releases" is 5. We create a template file in our theme folder named <em>category-5.php</em>. Under use case #2 (no primary feed), we will want to redirect <em>all</em> category archive traffic, in which case we need to work with the <em>category.php</em> template file.

A few lines of code in either template file will redirect visitors to the right place. We'll also pass <a href="https://www.checkupdown.com/status/E301.html">HTTP error / redirect code "301"</a> – which will tell search engines to <em>permanently</em> redirect their link to the right location. Note that this particular code assumes we are using a permalink configuration. Line 2 can be modified to accomodate that situation.

<pre><code class="language-php">$destination = get_bloginfo('url');
$destination .= str_replace('/'.get_option('category_base').'/','/',$_SERVER['REQUEST_URI']);
wp_redirect($destination, 301);</code></pre>

In effect, that code removes the category base ("/category" by default) from the overall relative URL, and <a href="https://codex.wordpress.org/Function_Reference/wp_redirect">safely redirects</a> the visitor to the page with the matching slug. Of course, if the site falls under use case #1 (one or two stand alone feeds), the line three could dropped into a specific category template (i.e. <em>category-5.php</em>) with a hardcoded absolute URL for the redirect destitation.</p>

### Hiding Standalone Categories from the Category List & Primary Site Feed

In the first use case (only isolating one or two categories from a primary feed), <strong>it may be necessary to prevent isolated categories or the posts within those categories from appearing in some common theme elements that would traditionally include them</strong>.

Consider the example from part one: a site with a traditional blog and a standalone press release feed. Assume the owners of the site want the RSS feed for the blog to be persistently available throughout the site (typically manifesting itself as an RSS icon in the browser location bar), but don’t want the press release items included in that primary feed. By default, the WordPress primary feed is available at “/feed”, and includes all published posts, regardless of category or any other post property.

<a href="https://www.smashingmagazine.com/feed"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19147" title="Smashing Magazine - Primary Feed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d7887e5-c43d-4028-aefb-e9168651bda5/smashingmag-feed.gif" alt="Smashing Magazine - Primary Feed" width="500" height="212" /></a>

To exclude categories from the primary RSS feed, we need to <a href="https://codex.wordpress.org/Function_Reference/add_filter">filter</a> the WordPress function that retrieves the posts. Let’s again assume that the category ID for Press Releases is 5. The following code should be placed in the template's <a href="https://codex.wordpress.org/Theme_Development#Theme_Functions_File">"functions.php" file</a>.

<pre><code class="language-php">add_filter('pre_get_posts','exclude_press');

function exclude_press($query) {
   if($query-&gt;is_feed &amp;&amp; !$query-&gt;is_category) $query-&gt;set('cat','-5');
}</code></pre>

To summarize, we use the "pre_get_posts" filter to modify the post query before it executes. Within a new filter - named "exclude_press" - a conditional confirms that the post query <em>is </em>for a feed, and that the query is <em>not </em>for an individual category. If the check pans out, the query is modified to exclude category 5 before execution.

The notion of globally filtering the post query may have broader implications depending on the site's unique requirements. With some smart conditional checking, the filter could be extended to prevent the category from appearing anywhere except within the category or isolated post view. But be careful when extending the filter, and be sure to consider all possible views, including administrative views!

The category list is another frequently used site element that isolated categories should, in most cases, be excluded from. If the template <a href="https://codex.wordpress.org/Template_Tags/wp_list_categories">calls the category list in only one or two places by code</a> (as opposed to using the categories widget), <a href="https://codex.wordpress.org/Template_Tags/wp_list_categories#Include_or_Exclude_Categories">excluding categories</a> from the list is straight forward.

<pre><code class="language-php">wp_list_categories('exclude=5');</code></pre>

However, if the categories widget is in use, or the category list is used throughout the template, an alternative approach is required. Enter the "list_terms_exclusions" filter. Again, the following code should be placed in the "functions.php" template file.

<pre><code class="language-php">add_filter('list_terms_exclusions', 'filter_press');

function filter_press($exclusions) {
   $exclusions .= " AND t.term_id != 5 ";
   return $exclusions;
}</code></pre>

The return value of a "terms exclusions" filter is tacked onto the "where" clause in the SQL query that retrieves the terms. Without digging too deep here, the reason for discussing "terms" as opposed to, say, "categories" is because WordPress <em>abstracts</em> a variety of different taxonomies (link categories, post categories, tags, custom taxonomies, etc) into a unified database model that handles <em>all</em> taxonomies. Calls to "get categories", "get tags", and so forth, are all referring back to general "terms" behind the scenes. Ever wonder why category, tag, and other IDs tend to jump around? They are all being added to the same table. Assuming a fairly clean install, try adding a new post category, and note the ID. Then add a tag, and note its ID... one greater than the new post category.

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19149" title="Abstract term structures" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bf88817-2cdf-47c8-867f-2b18966584b2/term-taxonomies.gif" alt="Abstract term structures" width="482" height="166" />

### Retaining the Page Layout for Post Views within a Category Page

One of the most common challenges to tackle with page / category association is retaining a sense that the visitor is still within the "category page" hierarchy - and not a global feed hierarchy - when a visitor is reading an individual post. Part one hinted at this challenge under “The devil is in the details,” and started to suggest a path that incorporated using the "in_category" function. <strong>We will explain how to use "in_category" within templates, as well as how to trick functions that reference the original query object into thinking that they are "within" the category page.</strong>

Let's start with case #1, and building on the example in the first article, assume we only need to contend with one isolated feed, "Press Releases" (category ID 5).

Say the theme has a sidebar template that lists post categories when rendering the blog part of the site, and when rendering a standalone page, shows a page list instead. Here’s an extremely simplified version of what that might look inside the sidebar template file.

<pre><code class="language-php">if (is_page())
{
   wp_list_pages();
}
else
{
   wp_list_categories();
}</code></pre>

Of course, there may be alternative widget sets for pages or posts, and there is likely to be more than just one element in the sidebar. But the concept should hold. Now going back to the example, the theme should render posts in category 5 (Press Releases) as if the visitor were on a page (not the blog). Leveraging the "in_category" check, the code above would now like the following:

<pre><code class="language-php">if (is_page() || in_category(5))
{
   wp_list_pages();
}
else
{
   wp_list_categories();
}</code></pre>

Note that if there are multiple categories whose posts should resemble page output, the "in_category" function should be passed an <em>array</em> of IDs, like so:

<pre><code class="language-php">in_category(array(5,7));</code></pre>

The need for a "in category" check is probably moot in case #2 (multiple page/category associations, without a primary feed): the template is probably structured to output the same elements on pages and posts from the get go. In other words, everything is handled as if it is a page since there <em>is no</em> primary feed. However, the following tip – that dynamically looks up the faux parent page ID (the page associated with the category) – is necessary for the next part of this tip. Just amend the code to check if "faux_parent_page" has a valid value: if it does, then the post is inside an isolated category associated with a page.

Once again, this approach to dynamically seeking the faux parent page (the category page) depends on taking advantage of the matching permalink structure between post categories and pages that is at the heart of this association. If the site is unable to use permalinks, a more complex alternative look up of the faux parent page will be necessary.

<pre><code class="language-php">foreach(get_the_category() as $category) {
   $faux_parent_path = '/'.get_category_parents($category, FALSE, '/', TRUE);
}
$faux_parent_page = get_page_by_path($faux_parent_path)-&gt;ID;</code></pre>

Now that we have the ID of the category's associated page, we can trick "black box" theme elements that determine page or post properties on their own (by referencing the post query) into thinking they are actually working with the category page.

The most common use case is <strong>page navigation</strong>. Whether its breadcrumbs, a top level page menu that should retain "current" (on) states, or a side navigation menu that should display the current section, there are many "black box" navigation functions that need to be tricked into rendering themselves as if on the category page.

Let's use a simple top level page list, which should maintain proper "current_page", "current_page_parent" (and so on) classes when on a post under a category page. Here's what that simple function might look like before our changes:

<pre><code class="language-php">wp_list_pages('depth=1');</code></pre>

Of course, posts do not normally have parent pages, so there will be no "current" classes assigned to that output when reading a post. Here is how to trick that function into thinking it is rendering the navigation for the "parent" category page.

<pre><code class="language-php">//retrieve faux parent page dynamically… can skip and hard code in case 1
foreach(get_the_category() as $category) {
   $faux_parent_path = '/'.get_category_parents($category, FALSE, '/', TRUE);
}
$faux_parent_page = get_page_by_path($faux_parent_path)-&gt;ID;

//reset the post query as if on the faux parent page
query_posts('page_id='.$faux_parent_page);

//execute our "faked out" function
wp_list_pages('depth=1');

//reset the query back to the initial state
wp_reset_query();</code></pre>

If there are multiple elements that need be "tricked," a best practice would be to put the "faux parent page" retriever at the top of the template, and declare it a global in any template files that need it. This would avoid repeated look ups of the faux parent page.</p>

### An Example: Seeing it All Put Together

### Retaining the Page Layout for Post Views within a Category Page

One of the most common challenges to tackle with page / category association is retaining a sense that the visitor is still within the "category page" hierarchy - and not a global feed hierarchy - when a visitor is reading an individual post. Part one hinted at this challenge under “The devil is in the details,” and started to suggest a path that incorporated using the "in_category" function. <strong>We will explain how to use "in_category" within templates, as well as how to trick functions that reference the original query object into thinking that they are "within" the category page.</strong>

Let's start with case #1, and building on the example in the first article, assume we only need to contend with one isolated feed, "Press Releases" (category ID 5).

Say the theme has a sidebar template that lists post categories when rendering the blog part of the site, and when rendering a standalone page, shows a page list instead. Here’s an extremely simplified version of what that might look inside the sidebar template file.

<pre><code class="language-php">if (is_page())
{
   wp_list_pages();
}
else
{
   wp_list_categories();
}</code></pre>

Of course, there may be alternative widget sets for pages or posts, and there is likely to be more than just one element in the sidebar. But the concept should hold. Now going back to the example, the theme should render posts in category 5 (Press Releases) as if the visitor were on a page (not the blog). Leveraging the "in_category" check, the code above would now like the following:

<pre><code class="language-php">if (is_page() || in_category(5))
{
   wp_list_pages();
}
else
{
   wp_list_categories();
}</code></pre>

Note that if there are multiple categories whose posts should resemble page output, the "in_category" function should be passed an <em>array</em> of IDs, like so:

<pre><code class="language-php">in_category(array(5,7));</code></pre>

The need for a "in category" check is probably moot in case #2 (multiple page/category associations, without a primary feed): the template is probably structured to output the same elements on pages and posts from the get go. In other words, everything is handled as if it is a page since there <em>is no</em> primary feed. However, the following tip – that dynamically looks up the faux parent page ID (the page associated with the category) – is necessary for the next part of this tip. Just amend the code to check if "faux_parent_page" has a valid value: if it does, then the post is inside an isolated category associated with a page.

Once again, this approach to dynamically seeking the faux parent page (the category page) depends on taking advantage of the matching permalink structure between post categories and pages that is at the heart of this association. If the site is unable to use permalinks, a more complex alternative look up of the faux parent page will be necessary.

<pre><code class="language-php">foreach(get_the_category() as $category) {
   $faux_parent_path = '/'.get_category_parents($category, FALSE, '/', TRUE);
}
$faux_parent_page = get_page_by_path($faux_parent_path)-&gt;ID;</code></pre>

Now that we have the ID of the category's associated page, we can trick "black box" theme elements that determine page or post properties on their own (by referencing the post query) into thinking they are actually working with the category page.

The most common use case is <strong>page navigation</strong>. Whether its breadcrumbs, a top level page menu that should retain "current" (on) states, or a side navigation menu that should display the current section, there are many "black box" navigation functions that need to be tricked into rendering themselves as if on the category page.

Let's use a simple top level page list, which should maintain proper "current_page", "current_page_parent" (and so on) classes when on a post under a category page. Here's what that simple function might look like before our changes:

<pre><code class="language-php">wp_list_pages('depth=1');</code></pre>

Of course, posts do not normally have parent pages, so there will be no "current" classes assigned to that output when reading a post. Here is how to trick that function into thinking it is rendering the navigation for the "parent" category page.

<pre><code class="language-php">//retrieve faux parent page dynamically… can skip and hard code in case 1
foreach(get_the_category() as $category) {
   $faux_parent_path = '/'.get_category_parents($category, FALSE, '/', TRUE);
}
$faux_parent_page = get_page_by_path($faux_parent_path)-&gt;ID;

//reset the post query as if on the faux parent page
query_posts('page_id='.$faux_parent_page);

//execute our "faked out" function
wp_list_pages('depth=1');

//reset the query back to the initial state
wp_reset_query();</code></pre>

If there are multiple elements that need be "tricked," a best practice would be to put the "faux parent page" retriever at the top of the template, and declare it a global in any template files that need it. This would avoid repeated look ups of the faux parent page.</p>

### An Example: Seeing it All Put Together

A great example of a WordPress-powered CMS that pushes use case #2 to its limits can be seen at the home of <em>m62 visual communications</em>, at <a href="https://www.m62.net/">https://www.m62.net</a>.

<a href="https://www.m62.net/powerpoint-templates/pharmaceutical-templates/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19151" title="m62 - pharmacy category" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b7f2b2-95bf-4237-b637-b13340021d2a/m62-pharm.gif" alt="m62 - pharmacy category" width="500" height="392" /></a>

All of the navigation items across the top (Presentation Theory, PowerPoint Slides, etc) are pages associated with post categories. The sub-navigation on the right contains sub-pages that are also associated with sub-categories. For example, in the screenshot above (<a href="https://www.m62.net/powerpoint-templates/pharmaceutical-templates/">available here</a>), the visitor is on the "Pharmaceutical Templates" page (faux category), which is a child of the "PowerPoint Templates" page (also a faux category). The content starting with "Download free" (below the page title) is the content from the "Pharmaceutical Templates" page. The posts below the "Next Steps" bar, titled "Latest in Pharmaceutical Templates", are the posts inside that category. The applicable related category is automatically discovered by the WordPress template, populating the category name "Latest in X" and recent posts. Now let's look at one of the posts inside that category.

<a href="https://www.m62.net/powerpoint-templates/pharmaceutical-templates/atoms-template/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="19152" title="m62 post with faux parent page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10b33049-fce0-45dd-8031-2c4ea6e65181/m62-post.gif" alt="m62 post with faux parent page" width="500" height="371" /></a>

Using the tips outlined above, the individual post retains the feel of being within the "Pharmaceutical Templates" page, right down to the breadcrumb navigation and "current" states in the navigation.

But not only does <em>m62.net</em> use category / page associations for most top and second level navigation items, it actually extends the concept to tags. The 5 "tabs" on the top right actually represent post tags, and each has a "tag page."

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Power Tips for WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)
*   [10 Useful WordPress loop hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks for WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](../2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)