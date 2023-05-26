---
title: Adopting A Responsive WordPress Theme Is More Than Install-And-Go
slug: adopting-a-responsive-wordpress-theme-is-more-than-install-and-go
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3bdb484-195a-44aa-84ae-c8a0948956c8/w.jpg'
date: 2012-07-26T09:08:45.000Z
author: ben-gremillion
description: >-
  As iOS, Android, and Windows 8 take the Web to smaller screens, designers are
  adopting techniques to make their websites usable on handheld devices.
categories:
  - WordPress
  - Themes
  - Techniques (WP)
---
[Responsive Web designs](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/) present different formatting and layout to suit the device on which their pages are displayed. Browsers choose the appropriate styles on page load, freeing website owners from having to maintain different sets of pages for different display scenarios.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/333eb4f1-82f2-4a7a-a659-ea08419c45b0/responsive-wp-teaser.png"><img loading="lazy" decoding="async" class="106539" title="Adopting A Responsive WordPress Theme Is More Than Install-And-Go" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/333eb4f1-82f2-4a7a-a659-ea08419c45b0/responsive-wp-teaser.png" alt="Adopting A Responsive WordPress Theme Is More Than Install-And-Go" width="500" height="300" /></a>

The most common responsive method is to use CSS media queries to serve different style sheets (or parts of style sheets) based on the number of pixels available. Most often, this is applied to handheld devices such as smartphones, but it could be applied to 13-inch laptops, 30-inch TVs or Kindle-sized readers. Responsive designs respond to their environment.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Become A Top WordPress Developer](https://www.smashingmagazine.com/2012/08/how-to-become-a-top-wordpress-developer/)
*   [Common WordPress Malware Infections](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)
*   [Writing Unit Tests For WordPress Plugins](https://www.smashingmagazine.com/2012/03/writing-unit-tests-for-wordpress-plugins/)
*   [Inside The WordPress Toolbar](https://www.smashingmagazine.com/2012/03/inside-the-wordpress-toolbar/)

{{% feature-panel %}}

## No Shortage Of Quick Fixes

The term “responsive design” is only two years old, but website owners can choose today from many mobile and widescreen themes for popular content management systems. Third-party developers have created paid and free themes that adapt based on browser width for WordPress, Drupal, Joomla and ExpressionEngine.

Recommended reading: [What To Consider When Choosing WordPress Themes](https://www.smashingmagazine.com/2014/12/what-to-consider-when-choosing-a-wordpress-theme/)

Designers handy with CSS can also find a <a href="https://responsive.gs/">few</a> <span class="removed_link" title="https://goldengridsystem.com/">do</span>-<span class="removed_link" title="https://www.columnal.com/">it</span>-<a href="https://www.designinfluences.com/fluid960gs/">yourself</a> <a href="https://www.smashingmagazine.com/2012/03/19/gridpak-the-responsive-grid-generator/">frameworks</a>. But responsive themes are as varied as the problems they are meant to solve. Not all are created with the same technique, features or attention to detail. Aesthetics aside, how should someone choose a theme?

## How Do Responsive Themes Perform?

Large themes cause delays for both the Web server and the end user. Servers require more time to fetch each additional file, and the milliseconds add up. For users, though, sluggishness comes from the number of kilobytes total, not just the number of files.

Aside from using media queries, many themes use variations of techniques to respond to browsers. I’ve tested <a href="https://wordpress.org/extend/themes/">40 responsive themes on WordPress.com</a>, comparing them to the stock <a href="https://wordpress.org/extend/themes/twentyeleven">Twenty Eleven</a> and <a href="https://wordpress.org/extend/themes/twentyten">Twenty Ten</a> themes.

<img loading="lazy" decoding="async" class="106418" title="Chart Responsive Themes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c728ecfb-c2b0-4bc3-ab41-ad1d72871567/wp-theme-size-requsts.png" alt="Chart comparing kilobytes to files used for responsive themes." width="550" height="362" /><br>
<em>The weight of each theme and supporting files in kilobytes.</em>

The chart above shows that:

*   The number of files that a theme loads and the theme’s weight in kilobytes have no direct relationship;
*   With few exceptions, most themes make 25 requests or fewer;
*   WordPress’ stock themes perform very well, but a few other themes provide responsive capability _and_ better performance.

Bear in mind that these are empty themes, measured before any content or modifications have increased their load. Because data costs money for people who are accessing the Web through cellular networks, themes that require fewer downloads per page load are more likely to earn repeat visits. Of the themes sampled:

*   Only one theme did not use CSS media queries. This theme’s unusual method was to detect page width with jQuery and then change the `body` class, which in turn would change the layout with animated transitions. The extra time taken to load and implement JavaScript compromised the goal of responsiveness.
*   More than half had three break points: mobile (480 pixels or less), medium (481 to 1024 pixels) and wide (1025 pixels or more). The medium-sized layouts were most often measured with percentages, ems or `min-` and `max-width`, rather than strictly by number of pixels.
*   Left-to-right layouts on wide screens always became top-to-bottom layouts on mobile. That is, the left-most column in a widescreen layout would always appear at the top of the page in a mobile layout, regardless of its width or the type of content. Likewise, right-hand columns would become footers in mobile layouts. This means that the content in your left-most column should not discourage users from scrolling down when it’s formatted for mobile devices.
*   All mobile designs had 10 to 20 pixels of horizontal margin. None deliberately allowed horizontal scrolling or used app-simulating frameworks such as jQuery Mobile.
*   None provided in-page navigation.
*   Two themes used `select` lists for navigation in their mobile layouts. None used multi-level navigation.
*   Loading a page with three paragraphs of placeholder text, the themes averaged 306.57 KB per page load and 25.4 resources retrieved (including images, CSS files, JavaScript files and the like).
*   The lightest theme weighed only 57.11 KB before the content itself (text and images) loaded. The largest weighed 1382.4 KB before the content loaded.

Recommended reading: [Are You Getting Cheated When Buying A WordPress Theme?](https://www.smashingmagazine.com/2015/11/ripped-off-buying-wordpress-themes/)

Remember that screen width does not necessarily equal browser width. Most themes are not built on the assumption that users will have their browser windows open as big as possible; rather, their layouts are designed for screen widths well under common sizes.

<img loading="lazy" decoding="async" class="106419" title="Theme Resolution Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b72bec19-855d-4072-a003-75f877b2fc20/wp-theme-resolution-chart.png" alt="Chart comparing common screen sizes to frequently-used web layouts." width="550" height="490" /><br>
<em>Most themes are well under the most common screen widths. The wider the screen, the less likely a user will expand their browser to fill it.</em>

As seen in the graph above, most themes will use <code>max-width</code> media queries to resize layouts when browsers reach 1280, 800, 767 and 480 pixels wide. But most screens surveyed by <a href="https://lifehacker.com/5428806/whats-your-screen-resolution">Lifehacker</a>, <a href="https://gs.statcounter.com/#resolution-ww-monthly-201105-201205">StatCounter</a> and <a href="https://www.w3counter.com/globalstats.php">W3 Counter</a> start at 1280 pixels wide.</p>

## Picking A Theme That Reflects Your Priorities

Making a website responsive is more than about varying the number of columns on a page. The same critical questions emerge for all mobile-friendly websites, regardless of CMS.

*   **Does the project merit a mobile layout?** Increasingly, the answer is yes. But the march towards mobile doesn’t mean that every website should follow suit. Pages that contain complicated tables, multi-month calendars, detailed images, complex navigation and other content unsuitable for small screens could negate any benefit offered by responsive designs. “Can I?” and “should I?” are two different questions.
*   **Would the website benefit from mobile-first thinking?** Designing a website to be mobile forces the content editors to answer hard questions. A screen measuring 320 pixels wide has no room for excess. This brings the design into focus, forcing you to eliminate distractions from whatever the website is meant to convey.
*   **How many steps do we need?** Responsively designed websites often rely on the width of the device on which they’re being viewed. But there’s more to it than asking “Mobile or not?” Responsive designs must address not only how a website handles on narrow screens, but also when wide becomes too wide. But a better option would be to consider using a [device-agnostic approach to Web design](https://www.smashingmagazine.com/2012/03/22/device-agnostic-approach-to-responsive-web-design/) focusing on content rather than device properties.
*   **How do the layout and formatting change?** Deciding which elements on a given page users should see first, second and third will affect how the widescreen layout functions. For example, the font in headings in the widescreen layouts could be three, four or five times larger than the body copy, whereas giant headings are cumbersome on tiny screens.
*   **What should a mobile page _not_ show?** Multiple columns encourage a hierarchy of information: primary content that is unique to each page, and secondary content (often relegated to sidebars) that appears on more than one page. But mobile design makes multiple columns difficult to pull off. If the secondary content is unnecessary, how should it disappear? If it’s important, how does one design it without letting pages run longer than users are willing to scroll? (A good rule of thumb is that if an element does not support the page’s title, then it is not primary content.)

Recommended reading: [A Guide To The Options For WordPress Theme Development](https://www.smashingmagazine.com/2013/03/a-guide-to-wordpress-theme-options/)

## Think Beyond The Theme

Having a responsive theme does not guarantee a good mobile user experience.

Designing for mobile is not just about cutting material, but also about planning for limited attention. By nature of the medium, mobile users absorb information in limited chunks. Long pages can work if they’re divided into phone screen-sized sections. Unlike widescreen users, mobile users are more inclined to scroll down “below the fold” (i.e. below what they first see when the page loads).

Consider higher-contrast colors for mobile — particularly, the contrast between the body text and the background — for improved legibility outdoors.

Extensive navigation bars with sublevels and sub-sublevels are impractical on mobile devices. Offering search functionality, creating pages dedicated to navigation, and flattening the website’s structure are common solutions; anything that reduces the number of taps between pages helps.</p>

## When To Consider A Separate Mobile Website

Responsive designs do more than make a website work well on a variety of screen sizes; they also force the owner to make their website easier, more focused and faster. But they’re a tool, not a requirement. Adaptive layouts and media queries aren’t always the best answer for mobile design problems. When big content simply doesn’t fit on small screens, maintaining a supplemental website would outweigh the benefit of having one website that serves many audiences. The key is to create a companion website that carries essential information organized for mobile use — and then find out what mobile users are missing.

Your website could warrant a separate mobile version if:

*   You find yourself creating duplicate pages for mobile users on the same website;
*   Short pages that look great on mobile phones don’t take advantage of large screens;
*   You plan to phase out the widescreen layout in favor of a more streamlined user experience.

Recommended reading: [Why We Shouldn't Make Separate Mobile Websites](https://www.smashingmagazine.com/2012/04/why-we-shouldnt-make-separate-mobile-websites/)

## Other Resources

You may be interested in the following articles and related resources:

- [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)
https://www.smashingmagazine.com/2014/07/responsive-web-design-should-not-be-your-only-mobile-strategy/)
- [You May Be Losing Users If Responsive Web Design Is Your Only Mobile Strategy](
https://www.smashingmagazine.com/2014/07/responsive-web-design-should-not-be-your-only-mobile-strategy/)
- [Giving Our Clients The Best Deal In Mobile](https://www.smashingmagazine.com/2012/10/give-clients-best-deal-mobile/)

