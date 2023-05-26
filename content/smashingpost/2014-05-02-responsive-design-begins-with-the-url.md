---
title: Responsive Design Begins With The URL
slug: responsive-design-begins-with-the-url
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/090594b4-d0e6-4149-9150-795126303dba/03-lazy-load-500.jpg
date: 2014-05-02T22:13:13.000Z
author: davidmarland
description: >-
  The BBC’s Programmes website is huge, and is intended to be a rolling archive
  of everything that the BBC broadcasts on television and radio. Originally
  released in 2007, it now has pages for over
  1.6 million episodes, but that’s barely half of the story. Surrounding those
  episodes is a wealth of content, including clips, galleries, episode guides,
  character profiles and much more, plus Programme’s newly responsive home
  pages.
categories:
  - Design
  - Responsive Design
  - Content Strategy
  - Information Architecture
---
The BBC’s Programmes website is huge, and is intended to be a rolling archive of everything that the BBC broadcasts on television and radio. Originally released in 2007, it now has <a href="https://www.bbc.co.uk/programmes">pages</a> for over 1.6 million episodes, but that’s barely half of the story. Surrounding those episodes is a wealth of content, including clips, galleries, episode guides, character profiles and much more, plus Programme’s newly responsive <a href="https://www.bbc.co.uk/programmes/b006q2x0">home pages</a>.

The new responsive home pages, known as “brand” pages, join the schedule and A–Z lists in a broader responsive rebuild. 39% of users (and growing) now use mobile and tablet devices to visit these pages; so, making the pages <strong>responsive was the best way to serve a great experience to everybody</strong> while keeping the website maintainable.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Introduction To URL Rewriting](https://www.smashingmagazine.com/2011/11/introduction-to-url-rewriting/)
*   [The 3 Fundamental Principles Of Technical SEO](https://www.smashingmagazine.com/2015/11/technical-seo-2015-wiring-websites-organic-search/)
*   [Technical SEO 2015: Wiring Websites for Organic Search](https://www.smashingmagazine.com/2015/11/technical-seo-2015-wiring-websites-organic-search/)
*   [Which Responsive Design Framework Is Best?](https://www.smashingmagazine.com/2017/03/which-responsive-design-framework-is-best/)

This article is a case study of the responsive rebuild of the BBC’s Programmes pages, and it actually begins back in 2007, at the conception of the project.

{{% feature-panel %}}

## URLs

The core principle in creating a potentially enormous website that will last forever is to <strong>get the information architecture right in the first place</strong>. This involves knowing your data objects and how they fit together. It should also determine the URL structure, which for Programmes is the most important aspect. Take the URL for Top Gear’s home page:

<pre><code class="language-markup">
https://www.bbc.co.uk/programmes/b006mj59
</code></pre>

After the domain name comes the word “programmes,” which is a simple, unchanging English word. It is intended to describe the object, and is not a brand or product name. Plurals are used so that the URL can be hacked backwards to retrieve an index.

Next is the programme identifier. Note the lack of hierarchy and the lack of a title. Titles change over time, and many programmes do <a href="https://www.bbc.co.uk/programmes/a-z/by/reddwarf/all">not have a unique title</a>, which would cause a clash. Hierarchies also change — a one-off pilot could be commissioned for a full series. Understanding your objects allows you to recognize what is permanent. In this case, nothing is particularly guaranteed to be permanent, so a simple ID is used instead. Users aren’t expected to type these URLs, though. They will usually arrive through a search engine or by typing in a friendly redirect that has been read out on air, such as <a href="https://www.bbc.co.uk/programmes/b006mj59">bbc.co.uk/topgear</a>. But the key principle of a permanent URL is that inward links are trusted to be shareable and work forever. <a href="https://www.w3.org/Provider/Style/URI.html">Cool URIs don’t change.</a>

<strong>A clear information architecture defines the URL scheme</strong>. A piece of content is given a clear canonical home, where appropriate. Links and aggregations between them then clearly appear.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28aafeb1-0f54-44f1-8b92-505489e5e1f3/01-url-scheme.jpg"><img title="A clear information architecture defines the URL scheme." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c27efb-0f91-4b58-bca8-974e9165732b/01-url-scheme-500.jpg" alt="A clear information architecture defines the URL scheme." width="500" height="546" /></a><br>
<em>A clear information architecture defines the URL scheme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28aafeb1-0f54-44f1-8b92-505489e5e1f3/01-url-scheme.jpg">Large preview</a>)</em>

It is clear how the data will be sliced before any wireframes are drawn or code is written. The black lines are direct links, while the red lines are shortcuts that we’ll add later.

On the brand page, we display the following information about the programme:

*   Summary (image and synopsis)
*   Can the user watch or listen to it now?
*   When will it be on TV or the radio?
*   How does one buy it?
*   Clips from the programme
*   Galleries from the programme
*   Editorially curated links to content (promotions)
*   Textual supporting content
*   Related links

This is a lot of content for a responsive page. Page loading could become excessive on low-end devices, so a priority needs to be determined.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79be5452-9da1-411a-80a0-c45a54436c77/02-page-load-priority.jpg"><img title="Loading priority should be determined for sites with large amounts of content." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c392127-1f19-446a-81f3-733b0aa12819/02-page-load-priority-500.jpg" alt="Loading priority should be determined for sites with large amounts of content." width="500" height="492" /></a><br>
<em>Loading priority should be determined for sites with large amounts of content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79be5452-9da1-411a-80a0-c45a54436c77/02-page-load-priority.jpg">Large preview</a>)</em>

<a href="https://www.craigbailey.net/content-is-king-by-bill-gates/">Content is king</a>, so hiding it on smaller screens is not acceptable. If any content could be sacrificed on mobile, then question whether it truly belongs on the desktop to begin with. The user journey remains the same, regardless of the device being used.

However, even though content may not be sacrificed on mobile, it doesn’t have to be present in its full form all the time. <strong>A simple link to the content might suffice</strong>, and because we have already defined a URL structure, most of the content already has somewhere to link to. Therefore, the block of “clips” on the brand page will, by default, link to this:

<pre><code class="language-markup">
/programmes/:id/clips    
</code></pre>

This is Web-friendly and the minimum viable product. If no more work was done, we’d still have something that works. <strong>The next phase is to see whether any enhancement can be made</strong>. We can use JavaScript to determine screen size (and possibly other factors) and then decide whether to load some shortcuts. By default, just a link is shown, but with enough space and if JavaScript is available, the link would be replaced with a carousel of the first six clips. These first six are the same six from <code>/clips</code>; this lazy-loaded content is simply a shortcut (the red lines from earlier).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6050e0-4b83-4ff5-8696-614e6c714662/03-lazy-load.jpg"><img title="Different states of lazy loading content." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/090594b4-d0e6-4149-9150-795126303dba/03-lazy-load-500.jpg" alt="Different states of lazy loading content." width="349" height="600" /></a><br>
<em> Different states of lazy loading content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6050e0-4b83-4ff5-8696-614e6c714662/03-lazy-load.jpg">Large preview</a>)</em>

JavaScript can be used to lazy-load content fairly often, but we have rules:

*   It may not be used for core content or for the user journey of the page.
*   It may be used only where a URL exists for the content, never for `href="#"`.

The top area of the page (which shows what the object is and how to watch it) is the core user journey of the brand page, so it is not lazy-loaded. Clips, galleries and recommendations are lazy-loaded, but promotions are not because they do not have URLs of their own. You could argue that promotions could be surfaced at the following URL:

<pre><code class="language-markup">
/programmes/:pid/promotions    
</code></pre>

But promos are not really “consumable content.” A user wouldn’t click a link to see all promos in this context, so promos are not lazy-loaded.</p>

## Images

Images are always a challenge in responsive Web design, and they were for us, too. Some of our <a href="https://www.bbc.co.uk/programmes/a-z/by/a">long aggregation pages</a> contain a lot of images, which need to be displayed at sizes appropriate to the device. The total download size of these long pages can be over 1 MB, mostly due to the images.

Therefore, <strong>we decided to tackle images in the same way that we tackle content</strong>, by asking whether a given page is the canonical home of the image. If it is, then the image must be there. If it isn’t, such as on the aggregation pages, then the image isn’t there by default. We then load in the most appropriate-sized image for the container with JavaScript. Additionally, <strong>only images currently in the viewport are loaded</strong>. As the page is scrolled, images that are about to appear are pulled in. This technique saves a lot of bandwidth on initial page loading, vastly improving response times for users, especially on small devices and when the user doesn’t scroll far. A useful library that uses a similar technique is used on BBC’s responsive News pages and is available in the open-source <a href="https://github.com/BBC-News/Imager.js/">Imager.js</a>.

At first, the implementation of this technique made the page jump around a lot as the user scrolled down and the images appeared. To work around this when the page first loads and the JavaScript kicks in, we load an old-fashioned spacer PNG, which has a 16:9 ratio and occupies the spaces of the images that will be filled in later. This is one extra download request for a small file that is used throughout the page. Using an inline base64-encoded PNG might have been preferable, but we discovered that Windows Phone devices do not display the holding image in the correct ratio, rendering it as a 1:1 square, so we had to use a standard PNG.

The techniques so far suggest a lot of use of JavaScript. This is true because it is loaded and runs on every page, but it is used with a light touch. <strong>JavaScript is not a requirement for any page</strong> (except for the playback of media), and it doesn’t do any particularly heavy lifting. Lazy-loaded content calls a <a href="https://www.bbc.co.uk/programmes/b00jd68z/clips.inc"><code>.inc</code> partial URL</a>, which returns HTML that is simply dropped into the page. The JavaScript barely does any DOM construction because the elements are constructed by server-side code, reusing the same partials.

Templating frameworks such as <a href="https://handlebarsjs.com/">Handlebars</a> could construct the DOM elements from a JSON source, but why fight the pre-parser? Browsers are extremely efficient at parsing and rendering HTML quickly, so we wouldn’t add complexity for such a simple use case. The website works and is stable without JavaScript — no need to overdo it.

## CSS

Building a large website that is maintainable requires a CSS strategy, or else it would balloon out of proportion. We decided to follow the <a href="https://bem.info/">BEM methodology</a> to create reusable blocks of CSS. The blocks might be granular and generic (for typography and grids) or more modular (for whole objects). The CSS is built up from <a href="https://www.bbc.co.uk/programmes/styleguide">Programmes’ style guide</a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acb71629-2cbf-4719-ac40-e34e22488986/04-programme-object.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a43c325-b145-41c2-b62e-c0c10e41af98/04-programme-object-500.jpg" alt="04-programme-object-500" width="500" height="101" /></a><br>
<em>An example of BBC's programm styleguide. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acb71629-2cbf-4719-ac40-e34e22488986/04-programme-object.jpg">Large preview</a>)</em>

This is the Programmes object. It is a server-side-generated partial and is used in multiple locations around the website. It has several variations, depending on the container that it needs to go in or the content that is available at a given time. The options are demonstrated on the corresponding <a href="https://www.bbc.co.uk/programmes/styleguide/programme-object">page of the style guide</a>, where they can be built and tested, ready to be dropped (hopefully) flawlessly anywhere in the application.

This method of building reusable CSS gives rise to some extra markup in the page, with some particularly long examples:

<pre><code class="language-markup">
&lt;div class="grid bpw2-thirteen-twentyfourths bpe-thirteen-twentyfourths grid--bounded"&gt;
</code></pre>

However, because these are generated by server-side code, they are usually easily updatable. These blocks tend to be repeated throughout the page, but <a href="https://en.wikipedia.org/wiki/Gzip">Gzip</a> compresses the markup extremely well. This CSS framework makes for a very reusable system. Programmes’ <code>global.css</code> file is included on every page and handles everything related to layout, all at just 15.4 KB (after Gzip’ing), which speeds up the creation of new pages. We can throw together some simple list-based pages, such as <a href="https://www.bbc.co.uk/programmes/b006mj59/recommendations">recommendations</a>, within minutes, without having to write any new CSS and by reusing the same Programmes object partial. This also enforces consistency across pages.

<strong>All objects are built to be touch-first, but not touch-dependent</strong>. The <a href="https://www.bbc.co.uk/programmes/styleguide/stream">stream</a>, which can be seen on the <a href="https://www.bbc.co.uk/programmes/p01nb93y">season page</a>, has an overflowing <code>div</code> in order to support native scrolling and automatic touch capabilities. However the arrow buttons (note not <code>&lt;a&gt;</code> tags) are still present for old devices and for people who wish to use a keyboard and mouse. The detection of touch does not necessarily mean that the user is touching to navigate, so mouse hovering is always supported.

<strong>Touch-first also means large hit areas</strong>. The Programmes object above has an overlaid link to make the whole object clickable, even though it will sometimes have multiple links within it.

After we launched this feature, we were informed by a user that in Windows high-contrast mode, all Programmes objects disappeared. We discovered that in high-contrast mode, Internet Explorer 9 forces the background of all links to be solid black, effectively obscuring the object. To overcome this across the board, we had to force the background color to be transparent with RGBa, and we set the opacity of the overlaid link to <code>0</code>, which allowed the object underneath to show through.

<pre><code class="language-css">
.block-link__overlay-link {
   top: 0;
   right: 0;
   bottom: 0;
   left: 0;
   overflow: hidden;
   text-indent: 200%;
   white-space: nowrap;
   background: rgba(0, 0, 0, 0); // IE 9 fix
}

// Increased specificity so that it trumps ".block-link a"
a.block-link__overlay-link {
   position: absolute;
   z-index: 0;
   // The next line is needed because all elements have a solid-black
   // background in high-contrast mode
   opacity: 0;
}
</code></pre>

At present, the <strong>BBC still receives a lot of traffic from Internet Explorer 8</strong>, which does not support media queries. We had to decide, then, what to show these users. The first option would be just to show the mobile version of the website to them, suitably scaled up but with nothing complex happening. This was not acceptable as the usage numbers are still too high, especially among the editorial staff. Therefore, we came up with a workaround.

We build our CSS using <a href="https://sass-lang.com/">Sass</a>, which fits very well with the modular structure, allowing partials to be organized in a clear folder structure. Wherever we use media queries, we can abstract them into breakpoints using Sass and then name them. In our main file, we then decide which breakpoints to pull in and whether to wrap them in media queries. The Sass component for handling this is available as <a href="https://github.com/BPScott/breakup">Breakup</a>. This means we can have two files: <code>global.css</code> and <code>global-ie.css</code>. The <code>global-ie.css</code> file gets all of the base and desktop breakpoints, without media queries, meaning that it is a fixed 1008-pixel page. We then decide which CSS to serve using IE conditional comments:

<pre><code class="language-markup">
&lt;!--[if (gt IE 8)|!(IE)]&gt;&lt;!--&gt;
        &lt;link rel="stylesheet" href=”path/to/styles/global.css" /&gt;&lt;!-- Also contains print --&gt;
    &lt;!--&lt;![endif]--&gt;
    &lt;!--[if (lt IE 9)&amp;(!IEMobile)]&gt;
        &lt;link rel="stylesheet" href="path/to/styles/global-ie.css" /&gt;
        &lt;link rel="stylesheet" href="path/to/styles/print.css" media="print" /&gt;
    &lt;![endif]--&gt;
</code></pre>

It also extends to the print CSS, because we can wrap that in media queries for newer browsers, too, which saves an extra download.</p>

## Limitations

Our responsive design still has a few limitations in its capabilities. We are keen to see a native solution for <a href="https://www.smashingmagazine.com/2013/06/25/media-queries-are-not-the-answer-element-query-polyfill/">element queries</a> to fix a few minor icon-sizing issues without the need for polyfills. At the moment, we can only make decisions based on the whole window size.

<img title="Roughly same-sized images should ideally get the same-sized icons." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fb58183-5e3f-4eb4-b373-67eb2e7752fc/05-same-size-icons.jpg" alt="Roughly same-sized images should ideally get the same-sized icons." width="460" height="331" /><br>
<em>Roughly same-sized images should ideally get the same-sized icons.</em>

There are also a few situations in which the markup order isn’t ideal on all devices. Improvements such as CSS grid layout will enable us to interlace modules at different screen sizes.</p>

## Conclusion

By building a website on which the <a href="https://www.craigbailey.net/content-is-king-by-bill-gates/">content is king</a>, starting with a clear information architecture and well-defined URLs, we have built a framework that we are proud to maintain. Using a sound URL scheme and building pages with semantic markup give us many benefits for free (or at least partially for free):

*   permanence,
*   stability,
*   optimization for search engines (linkability),
*   accessibility,
*   shareability.

By progressively enhancing, we could still build an interface that is attractive and information-dense where appropriate. We will continue to adapt with new responsive features as they become available and once visits from old browsers decline enough that we can move ahead. Reusable content components and CSS make that easier to do, thus making it possible to look after such a large website as it continues to grow every day.

{{< signature "al, ml" >}}

