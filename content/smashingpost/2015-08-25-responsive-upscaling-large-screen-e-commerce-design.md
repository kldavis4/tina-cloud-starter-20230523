---
title: 'Responsive Upscaling: Large-Screen E-Commerce Design'
slug: responsive-upscaling-large-screen-e-commerce-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3980cbf-0726-4a01-8559-8118d56035ed/responsive-upscaling-04-f8ede362c3d3a5f17359353e84956d92.jpg
date: 2015-08-25T18:57:27.000Z
author: christian-holst
description: >-
  The responsive design revolution is truly upon us (if it hasn’t already
  happened!), and even though e-commerce websites haven’t picked up **responsive
  design** quite as aggressively as in other industries, it’s becoming
  increasingly popular.
categories:
  - UX
  - Design
  - E-Commerce
  - UX
  - Responsive Design
---
The responsive design revolution is truly upon us (if it hasn’t already happened!), and even though e-commerce websites haven’t picked up <strong>responsive design</strong> quite as aggressively as in other industries, it’s becoming increasingly popular.

So far, most of the responsive design thinking has revolved around covering the range of experiences from mobile to desktop. Yet little attention has been paid to the opportunities for expanding that range beyond the standard desktop screen, to create an experience optimized for modern <strong>large-scale displays</strong>. Consider this:

1.  Only **18%** of the [50 leading US e-commerce websites](https://baymard.com/ecommerce-product-lists/benchmark/site-reviews) that we benchmarked earlier this year optimize their design for large monitors (yet 94% of those websites have a design optimized for mobile devices).
2.  Approximately **three-quarters** of e-commerce sales still happen on PCs, not mobile devices (see [here](https://marketingland.com/mobile-drives-nearly-half-e-commerce-traffic-pc-still-rules-sales-report-118629), [here](https://www.vicimediainc.com/desktop-reigns-supreme-in-ecommerce-traffic-and-revenue/) and [here](https://www.internetretailer.com/2015/06/08/mobile-shopping-accounts-larger-share-online-sales)).
3.  About **one third** of those users visit on screens wider than 1350 pixels (see [here](https://www.w3counter.com/globalstats.php), [here](https://gs.statcounter.com/#all-resolution-ww-monthly-201505-201505-bar) and [here](https://css-tricks.com/screen-resolution-notequalto-browser-window/)). (Note: There is, of course, a difference between screen and browser width — the actual number of users with a browser this wide will be lower. We recommend that you [track browser sizes](https://www.labnol.org/internet/browser-windows-size/26872/) in your web statistics for the most accurate picture of how significant this segment is on your website.)

Based on these statistics, crafting an <strong>optimized experience for users with large screens</strong> should seem well worth the effort. In fact, designing for big screens might turn out to be the next frontier of responsive e-commerce design.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2014/02/create-client-side-shopping-cart/#further-reading-on-smashingmag)

*   [Fundamental Guidelines Of E-Commerce Checkout Design](https://www.smashingmagazine.com/2011/04/fundamental-guidelines-of-e-commerce-checkout-design/)
*   [The Current State Of E-Commerce Filtering](https://www.smashingmagazine.com/2015/04/the-current-state-of-e-commerce-filtering/)
*   [UI Patterns For Mobile Apps: Search, Sort And Filter](https://www.smashingmagazine.com/2012/04/ui-patterns-for-mobile-apps-search-sort-filter/)
*   [Reducing Abandoned Shopping Carts In E-Commerce](https://www.smashingmagazine.com/2014/10/reducing-abandoned-shopping-carts/)
*   [A Little Journey Through (Small And Big) E-Commerce Websites](https://www.smashingmagazine.com/2013/12/e-commerce-websites-showcase/)

{{% feature-panel %}}

In this article, we’ll explore how e-commerce designers could use <strong>responsive upscaling</strong> to craft a tailored experience for users with big screens. We’ll cover one core principle, along with 11 ideas for upscaling different parts of the e-commerce experience to deal with the various usability challenges observed during our e-commerce usability studies. This article was <a href="https://baymard.com/blog/responsive-upscaling">originally published</a> by the Baymard Institute.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7900fc52-2d75-4099-b961-2a0415399bf5/01-ikea-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25422e6a-48fd-450c-8195-34566209b61c/01-ikea-opt-small.jpg" alt="IKEA’s results page" /></a><figcaption>Many e-commerce sites don't make use of available space on larger screens. The result: often a lot of white space surrounding a rather crammed search results page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7900fc52-2d75-4099-b961-2a0415399bf5/01-ikea-opt.jpg">View large version</a>)</figcaption></figure>

Notice all of the white space surrounding IKEA’s rather crammed search results page. During our <a href="https://baymard.com/research/ecommerce-product-lists">e-commerce product list</a> study, it became clear that in aesthetically driven product verticals, such as home decor, users need large thumbnails to accurately evaluate products. Utilizing the extra screen space to provide that is one of many “responsive upscaling” ideas for e-commerce websites to consider.

The extra screen real estate afforded by large screens is typically <strong>left unused</strong> as vast seas of white, while the actual page content is crammed into a tight design optimized to fit a laptop screen. At a very minimum, content could be given a little more breathing room, with some additional white space between elements on large-sized monitors.

Yet “responsive upscaling” can be taken much further, to provide a <strong>superior experience</strong> for users on large monitors by using the extra space to provide larger images, additional product columns, better page context and easier access to relevant website actions (filtering and sorting, “Add to Cart” buttons, etc.).</p>

## Core Principle Of Responsive Upscaling: Same Content, Different Packaging

There are fundamentally <strong>two ways</strong> to utilize the extra space: insert additional content on the page (i.e. content that’s only available at the large-scale resolutions), and present existing page content in a different way (i.e. reposition elements, change their layout, scale up, etc.).

You’ll notice that all of the examples in this article illustrate how existing page <strong>content can be presented differently</strong> (sometimes dramatically so). This is because inserting entirely new page content that’s available only at the large-scale resolutions <em>generally</em> isn’t a good idea. There are exceptions, of course, but generally speaking, if content isn’t important enough to show in the "regular" desktop view, then it most likely isn’t important enough to be shown on bigger screens either.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0176ac7-5683-4af1-9804-b7e8fcac918d/02-devices-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b90788-5fc4-4499-982e-410f90cdcb9d/02-devices-opt-small.png" alt="02-devices-opt-small" /></a><figcaption>Show the same content for all devices but “package” it differently. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0176ac7-5683-4af1-9804-b7e8fcac918d/02-devices-opt.png">View large version</a>)</figcaption></figure>

A bigger screen <a href="https://bradfrost.com/blog/mobile/content-parity/">doesn’t mean</a> that the user suddenly wants a cramped layout which is difficult to scan, nor does a smaller screen <a href="https://www.lukew.com/ff/entry.asp?1732">mean</a> that the user would never request any kind of information that they've seen on the site before. Therefore, show the same content, but “package” it differently so that it is optimized for the screen it is being displayed on.

Unimportant content should never be added to the page just because there’s room for it on the page. Likewise, important content should never be left out just because screen real estate is limited (see our test findings in “<a href="https://baymard.com/blog/content-on-mobile-vs-desktop">How Should Your Mobile and Desktop Sites Differ?</a>,” which documents this principle). The only time new page content should be inserted at large-scale resolutions is when that content somehow makes sense only on larger displays but not on regular screens.

So, as a general rule, a <strong>warning bell</strong> should ring when new page content is being added at large-scale resolutions. A few times it will be justified, but most often the content either will be too unimportant to show at regular screens sizes and therefore ought to be excluded from the large-scale versions too or will be actually <em>important</em> and therefore should be included on the page regardless of screen size. Obviously, important content might need to be presented very differently depending on the available space, but it should be available in some shape or form in all versions of the design.</p>

## Ideas For Responsive Upscaling On An E-Commerce Website

Keeping with this principle of avoiding new content and instead presenting existing content differently, let’s look at some of the many ways <strong>responsive upscaling</strong> might work on an e-commerce website.

All of the following examples have been illustrated by layering <strong>drawings</strong> onto screenshots of <a href="https://www.wayfair.com">Wayfair.com</a>. Now, Wayfair’s desktop design currently isn’t responsive at all (i.e. the page doesn’t scale and the layout doesn’t rearrange based on browser size), neither “up” nor “down” — the page’s width stays fixed regardless of the user’s viewport. It is, therefore, a good case for illustrating how the different types of pages on an e-commerce website could be optimized for users with large screens.

In a real implementation of these examples, other page elements would likely realign and possibly scale, too (especially page elements such as the header and footer), but for the purpose of these basic illustrations, the elements are simply shifted around a little. The examples should be seen as <strong>inspiration</strong>, and some will obviously be more appropriate to you than others, depending on your website’s product verticals and objectives.</p>

### Inlining Sign-Up Overlay

Sign-up overlays can be made less obtrusive on large screens by ditching the overlay and instead permanently placing the dialog alongside other “above-the-fold” content. This will make the sign-up dialog <strong>less intrusive</strong> because it won’t block out the whole page, yet it will still keep the dialog highly visible because it will still be shown immediately upon page load (because it’s placed above the fold).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae7d0eb2-39da-4ab5-82c7-a9ab8246b7e8/03-sigup-overlay-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11069c17-320e-441d-8606-a5d4436de024/03-sigup-overlay-opt-small.jpg" alt="A sign-up overlay dialog repositioned as inline page content placed above the fold" /></a><figcaption>A sign-up overlay dialog repositioned as inline page content placed above the fold. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae7d0eb2-39da-4ab5-82c7-a9ab8246b7e8/03-sigup-overlay-opt.jpg">View large version</a>)</figcaption></figure>

Now, users uninterested in the sign-up will obviously find this dialog <strong>easier to ignore</strong> because they won’t have to actively dismiss it anymore. However, during our usability studies, most of the test subjects simply closed traditional overlay dialogs without ever reading their content, often referring to these overlays as “popups” (see “<a href="https://baymard.com/blog/avoid-these-ecommerce-graphics#dont-show-overlay-dialogs-on-page-load">Avoid These 5 Types of E-Commerce Graphics</a>”). It’s a kind of overlay blindness. Those users might actually be more likely to read the sign-up dialog when it is placed inline above the page fold instead, because on seeing the element, they won’t spend all of their attention trying to find a way to dismiss it.</p>

### Header and Footer Shortcuts

The most popular links from the header (for example, account and ordering links for signed-in users) and footer (customer service and FAQ links) could be displayed in a box on the home page when there’s room for them. Obviously, the links should still be accessible in their <strong>original positions</strong> within the header menus and footer sections. On large screens, these shortcuts would simply <em>also</em> be available directly on the home page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c39d0010-752e-4e13-b619-f23b6525f573/04-header-footer-links-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3774e8b-e30e-4603-bd54-6700b8b64793/04-header-footer-links-opt-small.jpg" alt="Popular header and footer links displayed in a link shortcuts box on the home page" /></a><figcaption>Popular header and footer links displayed in a link shortcuts box on the home page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c39d0010-752e-4e13-b619-f23b6525f573/04-header-footer-links-opt.jpg">View large version</a>)</figcaption></figure>

This is a good example of content remaining available on the page but being displayed differently. It’s not new content, but rather existing content being <strong>displayed differently</strong>, to optimize the experience for users on large screens. In this particular case, the color of the link shortcuts box should probably be lightly faded to make it appear secondary to other content.</p>

### Inlining Carousel Slides

Home page carousels are fraught with usability issues and must be implemented very carefully to work at all (see the <a href="https://baymard.com/blog/homepage-carousel">eight carousel requirements</a> observed in our test studies). On larger screens, the carousel could, of course, simply scale up, making the shown slide all that much bigger. However, if the slides are square or even just reasonably tall, then scaling up the carousel slide could actually end up pushing the rest of the page’s content <strong>outside of the viewport</strong> on large monitors — decreasing the home page overview despite the increased viewport! A solution to this is turning the carousel slide into a multi-column view, with two or three slides being shown at once.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e642685d-c0a5-4a63-a09e-3398b2cb16b6/05-carousel-slider-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0fb3ab0-031d-4812-9110-d4ac52a4b918/05-carousel-slider-opt-small.jpg" alt="A set of carousel slides is turned into a multi-column layout" /></a><figcaption>A set of carousel slides is turned into a multi-column layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e642685d-c0a5-4a63-a09e-3398b2cb16b6/05-carousel-slider-opt.jpg">View large version</a>)</figcaption></figure>

If the total number of slides matches the number of columns, then the problematic <strong>interactive features</strong> of the carousel could even be hidden away in favor of a static multi-column layout of the slides. If there are more slides than columns, then they will, of course, still need slide rotation features or a grid representation with rows.</p>

### Inlining Filled Cart

Most e-commerce vendors hope for one of two actions to follow when a user adds an item to their cart: The user goes looking for more items to add to their cart, or they buy the item in their cart. Continuing to browse for other products is obviously great for revenue, but it also means that <strong>buyer’s remorse</strong> is more likely to set in — especially if the user has a <a href="https://baymard.com/blog/ecommerce-search-report-and-benchmark">hard time</a> navigating the website while searching for additional products.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82d8859-73a0-4ee9-a47c-070d4cd2edc5/06-filled-cart-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d7e441f-3875-4dcc-b548-6c8c3b9625db/06-filled-cart-opt-small.jpg" alt="The regular drop-down cart is inlined when the user has added one or more items" /></a><figcaption>The regular drop-down cart is inlined when the user has added one or more items. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82d8859-73a0-4ee9-a47c-070d4cd2edc5/06-filled-cart-opt.jpg">View large version</a>)</figcaption></figure>

By inlining the regular drop-down cart (available from the page header), the vendor gives the user an overview of the items already in their cart — reminding them of the great products they have already found (which, of course, they should most definitely purchase before leaving!). This gives the user <strong>easy access</strong> to the checkout process and thus helps to close the sale.

Furthermore, during our study of <a href="https://baymard.com/research/homepage-and-category-usability">home page and category</a> navigation, users were frequently observed to <strong>reopen</strong> their cart simply to glance at the names of previously added items. For instance, they might reopen the cart to see the model name of the camera they just added in order to find a matching camera case. Permanently displaying the cart will make it easier for users to find matching items, because it enables direct comparison between the product list currently being browsed and the items in the cart.</p>

### Additional Product Columns

One of the most obvious ways of utilizing the extra screen real estate in grid-based product lists is to <strong>rearrange the products</strong> so that they appear across additional columns. This can greatly increase the number of products visible on the screen. In the example above, the user goes from being able to see six products in their viewport to seeing ten.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a16321c7-cf6d-49d0-b27c-e2f3a6041093/07-product-columns-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2128352c-a9cc-441c-ab61-adb878be5f18/07-product-columns-opt-small.jpg" alt="The product list grid reflows to fit additional columns on large displays" /></a><figcaption>The product list grid reflows to fit additional columns on large displays. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a16321c7-cf6d-49d0-b27c-e2f3a6041093/07-product-columns-opt.jpg">View large version</a>)</figcaption></figure>

This approach can <strong>significantly optimize the product list view</strong> on large screens, but do it with care. If the number of product columns is excessive, then the grid will ultimately become <em>more</em> difficult to scan because users will drown in information and their eyes will have trouble travelling from one line to the next (there’s a reason text has an <a href="https://baymard.com/blog/line-length-readability">optimal line length</a>).

Therefore, restrict your products to <strong>five to eight columns</strong> (depending on size of list items and product vertical) to keep users from getting lost in a sea of information.</p>

### Larger Product List Images

The other obvious way to take advantage of extra viewport space in product lists is to <strong>scale up each list item</strong> to fit the user’s screen. For example, you could significantly increase the size of product thumbnails, allowing users to inspect the aesthetics of each product in much greater detail. This has palpable benefits in visually driven product verticals because it maximizes the amount of visual information conveyed, making it much easier for users to identify products to their liking.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b18102c-da2e-40d4-b195-3d9d426d74e8/08-larger-product-images-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe3cba3-d326-4f6a-ac45-14730fab6e69/08-larger-product-images-opt-small.jpg" alt="The product list items are scaled up to provide higher-resolution images, maximizing the amount of visual information conveyed" /></a><figcaption>The product list items are scaled up to provide higher-resolution images, maximizing the amount of visual information conveyed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b18102c-da2e-40d4-b195-3d9d426d74e8/08-larger-product-images-opt.jpg">View large version</a>)</figcaption></figure>

However, discretion is once again advised, because simply scaling up images will often result in a vast increase in <strong>list item height</strong> (assuming that aspect ratios are maintained), which can actually greatly reduce the number of products on screen. Notice in the illustration above how the second row of columns has been pushed almost entirely out of view.

The tradeoff when scaling images up in product lists, therefore, is an increase in the level of <strong>visual detail</strong> available about each product, at the cost of limiting the user’s overview of available products due to the lower number of products that can fit in the viewport.</p>

### Scaling and Rearranging Product Lists

By combining the two previous approaches as the user’s screen widens — that is, by both adding columns and increasing the size of each list item — we get the best of both worlds. Visual information about each product is increased, yet the overview is maintained because the <strong>product grid rearranges to show an additional column</strong> whenever the list items reach a height threshold.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa145e18-faac-4a93-8af9-947994d49a42/09-scaling-rearranging-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bc75933-ec94-4ec7-80f7-0321273d9a67/09-scaling-rearranging-opt-small.jpg" alt="The product list items are both scaled up and rearranged into additional columns" /></a><figcaption>The product list items are both scaled up and rearranged into additional columns. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa145e18-faac-4a93-8af9-947994d49a42/09-scaling-rearranging-opt.jpg">View large version</a>)</figcaption></figure>

This way, <strong>list items can grow</strong> to show additional visual information about each product, without ever growing so tall as to compromise the total number of products that fit on the screen. Indeed, because of the additional columns, the number of products in the viewport will increase. Thus, both the total number of shown products <em>and</em> their individual resolution improves.</p>

### Sticky Filters

Another way to utilize extra screen space is to permanently <strong>attach filtering and sorting tools</strong> to the user’s viewport via a “sticky” element. This will give the user additional context about the products they’re currently viewing and easy access to manipulate the criteria for the product list.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9bb344-ab7e-4fc9-8531-5214d3da3110/10-sticky-filters-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92d086a3-5ce9-40f6-bba2-fad21bd82c55/10-sticky-filters-opt-small.jpg" alt="Filtering tools can be repositioned into sidebars that stick to the edge(s) of the user’s screen" /></a><figcaption>Filtering tools can be repositioned into sidebars that stick to the edge(s) of the user’s screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9bb344-ab7e-4fc9-8531-5214d3da3110/10-sticky-filters-opt.jpg">View large version</a>)</figcaption></figure>

Fixed content effectively makes the space available for the main content smaller. Therefore, whenever fixing content to the edges of the viewport, do so only on a screen axis that has enough space to keep the fixed content from consuming too much room across that axis. For instance, <strong>don’t fix content to the top or bottom of the screen</strong> without applying a viewport height rule (for example, a height-based <code>@media</code> query) that checks that sufficient space is available.

However, with appropriate checks in place, the sticky filtering sidebar could even be rearranged to occupy multiple columns, with the tools distributed across two or three columns. If the <a href="https://baymard.com/blog/horizontal-filtering-sorting-design">filtering toolbar is horizontal</a>, you could attach it to the top of the screen if the viewport is sufficiently high, or if the horizontal space is plentiful, you could reposition it into a sidebar upon scroll. Browser height can similarly be used to dynamically adjust <a href="https://baymard.com/blog/truncation-design">truncation thresholds</a> for filtering values, increasing the number of filtering values displayed before truncation sets in as the screen height goes up.</p>

### Recently Viewed Items

During testing, when the subjects landed on a product page and decided the product wasn’t for them after all, they would either continue browsing or leave the website. Making it easy for the user to do the former is obviously in the vendor’s interests. By <strong>displaying suggestions</strong> for <a href="https://baymard.com/blog/product-page-suggestions">alternative and supplementary products</a> or a list of recently viewed items in the sidebar above the page fold, you instantly show users an escape route should they decide that the product they’re currently looking at isn’t for them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7613805e-05c1-436d-b9b2-0871cdeded44/11-recently-viewed-items-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7613805e-05c1-436d-b9b2-0871cdeded44/11-recently-viewed-items-opt-small.jpg" alt="Product suggestions or a list of recently viewed items may be placed in a sidebar for easy cross-product navigation" /></a><figcaption>Product suggestions or a list of recently viewed items may be placed in a sidebar for easy cross-product navigation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7613805e-05c1-436d-b9b2-0871cdeded44/11-recently-viewed-items-opt-small.jpg">View large version</a>)</figcaption></figure>

Making it easy for users to navigate from one product to the next can be essential to their product-finding abilities. Of course, <a href="https://baymard.com/blog/featured-products-category-link">product categories</a> could similarly be promoted, although be mindful of the <strong>user flow</strong> — is the user being sent <a href="https://baymard.com/blog/ecommerce-breadcrumbs">back and forth</a> between product lists and product pages, or can they go from one product to the next?

Sometimes the former is attractive because it gives the user a more coherent overview of the website’s offerings, but obviously the back-and-forth flow also introduces a lot more friction. Therefore, make sure the paths you suggest in promoted elements strike a sensible balance between category and product page destinations.</p>

### Sticky Product Page Summary

Product pages can be long. They can contain <a href="https://baymard.com/blog/ux-product-image-categories">images</a>, descriptions, specifications, customer reviews, suggestions for <a href="https://baymard.com/blog/product-page-suggestions">alternative and supplementary products</a>, FAQs, etc.

All of our usability studies have shown that more information is almost always better (so long as the content is of good quality — that is, useful, trustworthy and reasonably accurate). Yet it also means that the user can sometimes end up very <strong>far away</strong> from the core context of the product (i.e. the name, price, any possible variations and the “Buy” button). To provide a permanent context and <strong>always keep the “Buy” button within reach</strong>, put a sticky product summary in the extra space on large screens, attaching it to the edge of the viewport as the user scrolls down the page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0427f0a1-0fdf-415c-8e22-5e1666350fe8/12-sticky-product-page-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f84fa4bc-26ff-43bf-896e-0692bbb6c2de/12-sticky-product-page-opt-small.jpg" alt="A sticky product summary and “Add to Cart” button are attached to the top of the user’s screen as they scroll down long product pages" /></a><figcaption>A sticky product summary and “Add to Cart” button are attached to the top of the user’s screen as they scroll down long product pages. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0427f0a1-0fdf-415c-8e22-5e1666350fe8/12-sticky-product-page-opt.jpg">View large version</a>)</figcaption></figure>

This sticky product summary can basically be a slightly modified version of the product’s list item design; or, if it’s attached to the horizontal axis of the user’s screen, it can take on a more slender aesthetic. Either way, the intent is to give the user a <strong>permanent product context</strong>, enabling them to see the name, price and any variations, even if they’re deep down in customer reviews. And, of course, always keep that “Add to Cart” button within easy reach when the user is reading that rave review from a happy customer.</p>

### Sticky Order Summary and Customer Support

During checkout, plenty of horizontal space will be unused because the pages tend to be very focused and because <a href="https://baymard.com/blog/avoid-multi-column-forms">multi-column forms</a> can cause major usability issues during checkout. On large screens, this vast sea of white space can be appropriated by an <strong>order summary</strong> and customer support details. The order summary would be a constant element throughout the checkout experience and serve as a constant reminder of the products the user is only moments away from owning.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89054e7d-f1d6-467b-bec4-a6ed2c26978c/13-sticky-order-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7b1bfb-acca-4b9a-b3ca-6778f8ed7ac9/13-sticky-order-opt-small.jpg" alt="Order summary and customer support features are displayed in a sidebar when there’s room for it on the screen" /></a><figcaption>Order summary and customer support features are displayed in a sidebar when there’s room for it on the screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89054e7d-f1d6-467b-bec4-a6ed2c26978c/13-sticky-order-opt.jpg">View large version</a>)</figcaption></figure>

Meanwhile, <strong>customer support</strong> features can be moved up from their common footer position to make them readily available should the user run into trouble during the checkout process. If you’re worried about being overrun in customer support, then you can more selectively promote details based on the cart’s order value and how far into the checkout process the user is and whether they have run into validation errors.</p>

## Responsive Upscaling For E-Commerce

It’s striking how few e-commerce vendors currently optimize their website’s design for large screens. Even the 18% of leading e-commerce vendors that do offer an optimized large-screen experience have really only taken the first small steps in that direction. Given the <strong>large segment</strong> of users with big screens, responsive upscaling is an area ripe with potential.

When implementing responsive upscaling, keep in mind the <strong>core principle</strong> of “same content, different packaging.” Either a piece of content will be important to all users, or it won’t be important enough to bother users on large monitors with either; just because a user has more space on their screen doesn’t mean they want a barrage of low-quality content. Instead, explore ways to present existing page content differently in order to create a better experience for users with big screens.

The 11 ideas covered in this article are all based on this principle of same content, different packaging — taking existing page content and scaling or repositioning it, sometimes significantly, other times subtly:

1.  inlining sign-up overlay
2.  header and footer shortcuts
3.  inlining carousel slides
4.  inlining filled cart
5.  additional product columns
6.  larger product list images
7.  scaling and rearranging product lists
8.  sticky filters
9.  recently viewed items
10.  sticky product page summary
11.  sticky order summary and customer support

Do you have other ideas for optimizing e-commerce websites for larger monitors? Share them in the comments section. It’s time to optimize the e-commerce experience for big-screen users, too.

{{< signature "vf, al, ml" >}}

