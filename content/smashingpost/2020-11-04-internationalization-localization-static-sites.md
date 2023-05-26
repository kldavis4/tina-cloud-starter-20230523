---
title: 'Internationalization And Localization For Static Sites'
slug: internationalization-localization-static-sites
author: sam-richard
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fa4ff93-f46c-402d-8426-d990d88c7a8b/internationalization-localization-static-sites.png
date: 2020-11-04T11:30:00.000Z
summary: >-
  Internationalization and localization is more than just writing your content in multiple languages. You need a strategy to determine what localization to send, and code to do it. You need to be able to support not just different languages, but different regions with the same language. Your UI needs to be responsive, not just to screen size, but to different languages and writing modes. Your content needs to be structured, down to the microcopy in your UI and the format of your dates, to be adaptable to any language you throw at it. Doing all of this with a static site generator, like Eleventy, can make it even harder, because you may not have a database, nonetheless a server. It can all be done, though, but it takes planning.
description: >-
  Internationalization and localization is more than just writing your content in multiple languages. You need a strategy to determine what localization to send, and code to do it. You need to be able to support not just different languages, but different regions with the same language. 
categories:
  - Accessibility
  - Usability
  - Internationalization
  - Static Generators
---

Internationalization and localization is more than just writing your content in multiple languages. You need a strategy to determine what localization to send, and code to do it. You need to be able to support not just different languages, but different regions with the same language. Your UI needs to be responsive, not just to screen size, but to different languages and writing modes. Your content needs to be structured, down to the microcopy in your UI and the format of your dates, to be adaptable to any language you throw at it. Doing all of this with a static site generator, like Eleventy, can make it even harder, because you may not have a database, nonetheless a server. It can all be done, though, but it takes planning.

When building out [chromeOS.dev](https://chromeos.dev), we knew that we needed to make it available to a global audience. Making sure that our codebase could support multiple locales (language, region, or combination of the two) without needing to custom-code each one, while allowing translation to be done with as little of that system’s knowledge as possible, would be critical to making this happen. Our content creators needed to be able to focus on creating content, and our translators on translating content, with as little work as possible to get their work into the site and deployed. Getting these sometimes conflicting set of needs right is the heart of what it takes to internationalize codebases and localize sites.

Internationalization (i18n) and localization (l10n) are two sides of the same coin. Internationalization is all about how, in our case, software, gets designed so that it can be adapted for multiple languages and regions without needing engineering changes. Localization, on the other hand, is about actually adapting the software for those languages and regions. Internationalization can happen across the whole website stack; from HTML, CSS, and JS to design considerations and build systems. Localization happens mostly in content creation (both long-form copy and microcopy) and management.

**Note**: *For those curious, i18n and l10n are types of abbreviations known as [numeronyms](https://en.wikipedia.org/wiki/Numeronym). A11y, for accessibility, is another common numeronym in web development.*

{{% feature-panel %}}

## Internationalization (i18n)

When figuring out internationalization, there are generally three items you need to consider: how to figure out what language and/or region the user wants, how to make sure they get content in their preferred localization, and how to adapt your site to adjust to those differences. While implementation specifics may change for dynamic sites (that render a page when a user requests it) and static sites (where pages are built before getting deployed), the core concepts should stay the same.

### Determining User’s Language And Region

The first thing to consider when figuring out internationalization is to determine how you want users to access localized content. This decision will become foundational to how you set up other systems, so it’s important to decide this early and ensure that the tradeoffs work well for your users.

Generally, there are three high-level ways of determining what localization to serve to users:

1. Location from IP address;
2. [`Accept-Language`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) header or [`navigator.languages`](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/languages);
3. Identifier in URL.

Many systems wind up combining one, two, or all three, when deciding what localization to serve. As we were investigating, though, we found issues with using IP addresses and `Accept-Language` headers that we thought were significant enough to remove from consideration for us:

*   A user’s preferred language often doesn’t correlate to their physical location, which IP address provides. Just because someone is physically located in America, for instance, does not mean that they would prefer English content.
*   Location analysis from IP addresses is difficult, generally unreliable, and may [prevent the site from being crawled by search engines](https://support.google.com/webmasters/answer/182192#:~:text=Do%20not%20use%20IP%20analysis%20to%20adapt%20your%20content).
*   `Accept-Language` headers are often [never explicitly set](https://www.w3.org/International/questions/qa-accept-lang-locales#:~:text=Many%20users%20never%20change%20the%20defaults%20for%20Accept-Language), and only provide information about language, not region. Because of its limitations, this may be helpful to establish an initial guess about language, but isn’t necessarily reliable.

For these reasons, we decided that it would be better for us to not try and infer language or region before a user lands on our site, but rather have strong indicators in our URLs. Having strong indicators also allows us to assume that they’re getting the site in the language they want from their access URL alone, provides for an easy way to share localized content directly without concern of redirection, and provides a clean way for us to let users switch their preferred language.

There are three common patterns for building identifiers into URLs: 

1. Provide different domains (usually [TLDs](https://en.wikipedia.org/wiki/Top-level_domain) or [subdomains](https://en.wikipedia.org/wiki/Subdomain) for different regions and languages (e.g. `example.com` and `example.de`, `en.example.org` and `de.example.org`);
2. Have localized sub-directories for content (e.g. `example.com/en` and `example.com/de`);
3. Serve localized content based on URL parameters (e.g. `example.com?loc=en` and `example.com?loc=de`). 

While commonly used, URL parameters are [generally not recommended](https://support.google.com/webmasters/answer/182192#:~:text=URL%20parameters) because it’s difficult for users to recognize the localization (along with a number of analytics and management issues). We also decided that different domains weren’t a good solution for us; our site is a [Progressive Web App](https://web.dev/what-are-pwas/) and every domain, including TLDs and subdomains, are considered a [different origin](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy#Definition_of_an_origin), effectively requiring a separate PWA for each localization.

We decided to use subdirectories, which provided a bonus of us being able to localize on language only (`example.com/en`) or language and region (`example.com/en-US` and `example.com/en-GB`) as needed while maintaining a single PWA. We also decided that every localization of our site would live in a subdirectory so one language isn’t elevated above another, and that all URLs, except for the subdirectory, would be identical across localizations based on the authoring language, allowing users to easily change localizations without needing to translate URLs.

### Serving Localized Content

Once a strategy for determining a user’s language and region has been determined, you need a way to reliably serve them the right content. At a minimum, this will require some form of stored information, be it in a cookie, some local storage,  or part of your app’s custom logic. Being able to keep a user’s localization preferences is an important part of i18n user experience; if a user has identified they want content in German, and they land on English content, you should be able to identify their preferred language and redirect them appropriately. This can be done on the server, but the solution we went with for chromeOS.dev is hosting and server setup agnostic: we used [service workers](https://web.dev/service-worker-mindset/). The user’s journey is as follows:

*   A user comes to our site for the first time. Our service worker isn’t installed.
*   Whatever localization they land on we set as their preferred language in [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API). For this, we presume they’re landing there through some means, either social, referral, or search, that has directed them based on other localization contexts we don’t have. If a user lands without a localization set, we set it to English, as that’s our site’s primary language. We also have a language switcher in our footer to allow a user to change their language. At this point, our service worker should be installed.
*   After the service worker is installed, we intercept all URL requests for site [navigation](https://web.dev/handling-navigation-requests/). Because our localizations are subdirectory based, we can readily identify what localization is being requested. Once identified, we check if the requested page is in a localized subdirectory, check if the localized subdirectory is in a list of supported localizations, and check if the localized subdirectory matches their preferences stored in IndexedDB. If it’s not in a localized subdirectory or the localized subdirectory matches their preferences, we serve the page; otherwise we do a 302 redirect from our service worker for the right localization.

We bundled our solution into [Workbox](https://developers.google.com/web/tools/workbox) plugin, [Service Worker Internationalization Redirect](https://github.com/chromeos/static-site-scaffold-modules/tree/master/modules/service-worker-i18n-redirect). The plugin, along with its [preferences sub-module](https://github.com/chromeos/static-site-scaffold-modules/blob/master/modules/service-worker-i18n-redirect/preferences.js), can be combined to set and get a user’s language preference and manage redirection when combined with Workbox’s `registerRoute` method and filtering requests on `request.mode === 'navigate'`.

A full, minimal example looks like this:

#### Client Code

<div class="break-out">

 <pre><code class="language-javascript">import { preferences } from 'service-worker-i18n-redirect/preferences';
window.addEventListener('DOMContentLoaded', async () => {
  const language = await preferences.get('lang');
  if (language === undefined) {
    preferences.set('lang', lang.value); // Language determined from localization user landed on
  }
});
</code></pre>
</div>

#### Service Worker Code

<div class="break-out">

 <pre><code class="language-javascript">import { StaleWhileRevalidate } from 'workbox-strategies';
import { CacheableResponsePlugin } from 'workbox-cacheable-response';
import { i18nHandler } from 'service-worker-i18n-redirect';
import { preferences } from 'service-worker-i18n-redirect/preferences';
import { registerRoute } from 'workbox-routing';

// Create a caching strategy
const htmlCachingStrategy = new StaleWhileRevalidate({
  cacheName: 'pages-cache',
  plugins: [
    new CacheableResponsePlugin({
      statuses: [200],
    }),
  ],
});

// Array of supported localizations
const languages = ['en', 'es', 'fr', 'de', 'ko'];

// Use it for navigations
registerRoute(
  ({ request }) => request.mode === 'navigate',
  i18nHandler(languages, preferences, htmlCachingStrategy),
);
</code></pre>
</div>

With the combination of the client-side and service worker code, users’ preferred localization will automatically get set when they hit the site the first time and, if they navigate to a URL that isn’t in their preferred localizations, they’ll be redirected.

### Adapting Site User Interface

There is a lot that goes into properly adapting user interfaces, so while not everything will be covered here, there are a handful of more subtle things that can and should be managed programmatically.

#### Blockquote Quotes

A common design pattern is having blockquotes wrapped in quotation marks, but did you know what gets used for those quotation marks varies with localization? Instead of hard-coding, use [`open-quote` and `close-quote`](https://developer.mozilla.org/en-US/docs/Web/CSS/content#:~:text=/*%20Language-%20and%20position-dependent%20keywords%20*/) to ensure the correct quotes are used for the correct language.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44b56f1c-a21d-4ab4-8ac0-24b23fffc0e2/english-quote-internationalization-localization-static-sites.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44b56f1c-a21d-4ab4-8ac0-24b23fffc0e2/english-quote-internationalization-localization-static-sites.jpg" sizes="100vw" caption="<code>open-quote</code> and <code>close-quote</code> for <code>lang=“en”</code> appear as two superscript commas facing inward towards the text, with the first pair inverted. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44b56f1c-a21d-4ab4-8ac0-24b23fffc0e2/english-quote-internationalization-localization-static-sites.jpg'>Large preview</a>)" alt="Blockquote from the style guide, using open-quote, close-quote for the quotes at the start and end, on a page with lang=”en”" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6a94c5-b9f8-4319-9ea5-7d38e29a928e/french-quote-internationalization-localization-static-sites.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6a94c5-b9f8-4319-9ea5-7d38e29a928e/french-quote-internationalization-localization-static-sites.jpg" sizes="100vw" caption="<code>open-quote</code> and <code>close-quote</code> for <code>lang=“fr”</code> appear as a pair of chevrons with their openings facing inward towards the text. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6a94c5-b9f8-4319-9ea5-7d38e29a928e/french-quote-internationalization-localization-static-sites.jpg'>Large preview</a>)" alt="Blockquote from our style guide, using open-quote, close-quote for the quotes at the start and end, on a page with lang=”fr”" >}}

#### Date And Number Format

Both [dates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString) and [numbers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString) have a method, `.toLocaleString` to allow formatting based on a localization (language and/or region). Browsers that support these ship with all localizations available, making it readily usable there, but Node.js doesn’t. Fortunately, the [full-icu](https://www.npmjs.com/package/full-icu) module for Node allows you to use all of the localization data available. To do so, after installing the module, run your code with the `NODE_ICU_DATA` environment variable set to the path to the module, e.g. `NODE_ICU_DATA=node_modules/full-icu`.

#### HTML Meta Information

There are three areas in your HTML tag and headers that should be updated with each localization:

- The page’s language,
- Writing direction,
- Alternative languages the page is available in.

The first to go on the `html` element with the `dir` and `lang` properties respectively, e.g. `<html lang="en" dir-"ltr">` for US English. Properly setting these will ensure content flows in the right direction and can allow browsers to understand what language the page is in, allowing additional features like translating the content. You should also include [`rel="alternate"`](https://support.google.com/webmasters/answer/189077) links to let search engines know that a page has been fully translated, so including `<link href="/es" rel="alternate" hreflang="es">` on our English landing page will let search engines know that this has a translation it should be on the lookout for.

#### Intrinsic Design

Localizing content can present design challenges as different translations will take up a varying amount of room on the page. Some languages, like German, have longer words requiring more horizontal space or more forgiving text wrapping. Other languages, like Arabic, have taller typefaces requiring more vertical space. Fortunately, there are a number of CSS tools for making spacing and layout responsive to not just the viewport size, but to the content as well, meaning they better adapt to multiple languages.

There are a number of [CSS units](https://developer.mozilla.org/en-US/docs/Web/CSS/length) specifically designed for working with content. There are the `em` and `rem` units representing the [calculated font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size#Ems) and root font-size, respectively. Swapping fixed-size `px` values for these units can go a long way in making a site more responsive to its content. Then there’s the `ch` unit, representing the [inline size](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties/Basic_concepts#Block_and_inline_dimensions) of the 0 (zero) glyph in a font. This allows you to tie things like `width`, for instance, directly to the [content it contains](https://meyerweb.com/eric/thoughts/2018/06/28/what-is-the-css-ch-unit/).

These units can then be combined with existing, powerful CSS tools for layout, specifically [flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) and [grid](https://css-tricks.com/snippets/css/complete-guide-grid/), to components that adapt to their size, and layouts adapt to their content. Enhancing those with [logical properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties) for  borders, margins, and padding instead of physical physical properties makes those layouts and components automatically adapt to [writing mode](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes), too. The power of [intrinsic web design](https://aneventapart.com/news/post/designing-intrinsic-layouts-aea-video) (coined by [Jen Simmons](https://twitter.com/jensimmons), content-aware units, and logical properties allows for interfaces to be designed and built so they can adapt to any language, not just any screen size.

{{% ad-panel-leaderboard %}}

## Localization (l10n)

The most obvious form localization takes is translating content from one language to another. In more subtle forms, translations not only happen by language, but region it’s spoken, for instance, English spoken in American versus English spoken in the United Kingdom, South Africa, or Australia. To be successful here, understanding what to translate and how to structure your content for translation is critical to success.

### Content Strategy

There are some parts of a software project that are important to localize, and some that aren’t. CSS class names, JavaScript variables, and other places in your codebase that are structural, but not user-facing, probably don’t need to be localized. Figuring out what needs to be localized, and how to structure it, comes down to content strategy.

Content strategy has a lot of definitions, but here it means the structure of content, microcopy (the words and phrases used throughout a project not tied to a specific piece of content), and the connections thereof. For more detailed information on content strategy, I’d recommend [Content Strategy for Mobile](https://abookapart.com/products/content-strategy-for-mobile) by Karen McGrane and [Designing Connected Content](https://www.peachpit.com/store/designing-connected-content-plan-and-model-digital-9780134763385) by Carrie Hane and Mike Atherton.

For chromeOS.dev, we wound up codifying [content models](https://github.com/chromeos/chromeos.dev/wiki/Content-Models) that describe the structure of our content. Content models aren’t just for long-form article-like content; a content model should exist for any entity that a user may specifically want from you, like an author, document, or even reusable media assets. Good content models include individually-addressable pieces, or chunks, of a larger conceptual piece, while excluding chunks that are tangentially related or can be referenced from another content model. For instance, a content model for a blog post may include a title, an array of tags, a reference to an author, the date published, and the body of the post, but it shouldn’t include the string for breadcrumbs, or the author’s name and picture, which should be its own content model. Content models don’t change from localization to localization; they are site structure. An instance of a content model is tied to a localization, and those instances can be localized. 

Content models only cover part of what needs to be localized, though. The rest—your “Read More” buttons, your “Menu” title, your disclaimer text—that’s all microcopy. Microcopy needs structure, too. While content models may feel natural to create, especially for template-driven sites, microcopy models tend to be less obvious and are often overlooked accidentally by writing what’s needed directly in a template.

By building content and microcopy models and enforcing them—through a content management system, linting, or review—you’re able to ensure that localization can focus on localizing.

### Localize Values, Not Keys

Content and microcopy models usually generate structures akin to objects in a codebase; be it database entries, JSON object, YAML, or [Front Matter](https://jekyllrb.com/docs/front-matter/). Don’t localize object keys! If you have your Search text microcopy located in a `microcopy` object at `microcopy.search.text`, don’t put it in a `microcopie` object at `microcopie.chercher.texte`. Keys in modules should be treated as localization-agnostic identifiers so they can be reliably used in reusable templates and relied upon throughout a codebase. This also means that object keys shouldn’t be displayed to end-users as content or microcopy.

{{% ad-panel-leaderboard %}}

## Static Site Setup

For chromeOS.dev, we used [Eleventy](https://www.11ty.dev/) (11ty) with [Nunjucks](https://mozilla.github.io/nunjucks/) as our static site generator, but these recommendations for setting up a static site generator should be applicable to most static site generators. Where something is 11ty specific, it will be called out.

### Folder Structure

Static site generators that compile based on folder structure are particularly good at supporting the subdirectory i18n method. 11ty also supports a data cascade with global data and a means of generating pages from data through [pagination](https://www.11ty.dev/docs/pagination/), so combining these three concepts yields a basic folder structure that looks like the following:

<pre><code class="language-bash">.
└── pages
   ├── _data
   ├── _generated
   └── {{locale-code}}
      ├── {{locale-code}}.11tydata.js
      ├── _data
      └── [...content]
</code></pre>

At a top-level, there’s a directory to hold the pages for a site, here called `pages`. Nested inside, there’s a `_data` folder containing global data files. This folder is important when talking about helpers next. Then, there’s a `_generated` folder. We have a number of pages that, instead of having their own content, are generated from existing content, small amounts of microcopy, or a combination of both. Think home a home page, a search page, or a blog section’s landing page. Because these pages are highly templated, we store the templates  in the `_generated` folder and build them from there instead of having individual HTML or Markdown files for each. These folders are prefixed with an underscore to indicate that they don’t output pages directly underneath them, but rather are used to create pages elsewhere.

Next, l10n subdirectories! Each directory should be named for the [BCP47 language tag](https://en.wikipedia.org/wiki/IETF_language_tag) (more commonly, locale code) for the localization it contains: for instance, `en` for English, or `en-US` for American English. In the chromeOS.dev codebase, we often refer to these as  __locales__, too. These folders will become the localization subdirectories, segmenting content to a localization. 11ty’s [data cascade](https://www.11ty.dev/docs/data-cascade/) allows for data to be available to every file in a directory and its children if the file is at the root of a directory and named the same as the directory (called [directory data files](https://www.11ty.dev/docs/data-template-dir/)). 11ty uses an object returned from this file, or a function that returns an object, and injects it into the variables made available for templating, so we have access to data here for all content of that localization.

To aid in maintainability of these files, we wrote a helper called [`l10n-data`](https://github.com/chromeos/static-site-scaffold-modules/blob/master/modules/static-site-scaffold/lib/l10n-data.js), part of our [static site scaffolding](https://github.com/chromeos/static-site-scaffold-modules/tree/master/modules/static-site-scaffold), that takes advantage of this folder structure to build a cascade of localized data, allowing data to be localized piecemeal. [It does this](https://github.com/chromeos/chromeos.dev/blob/trunk/pages/en/en.11tydata.js) by having data stored in a locale-specific data directory, `_data` directory in it (loaded into the directory data file). If you look in our [English locale data directory](https://github.com/chromeos/chromeos.dev/tree/trunk/pages/en/_data), for instance, you’ll see microcopy models like `locale.json` which defines the language code and writing direction that will then be rendered into our HTML, `newsletter.yml` which defines the microcopy needed for our newsletter signup, and a `microcopy.yml` file which includes general microcopy used in multiple places throughout the site that doesn't fit into a more specific file. Everywhere any of this microcopy gets used, we pull it from this data made available through 11ty injecting data variables into our templates to use.

Microcopy tends to be the hardest to manage, while the rest of the content is mostly straight forward. Put your content, often Markdown files or HTML, into the localized subfolder. For static site generators that work on folder structure, the file name and folder structure of the content will typically map 1:1 to the final URL for that content, so a Markdown file at `en/web/pwas.md` would output to a URL `en/web/pwa`. Following our “values, not keys” principle of localization, we decided that we wouldn’t localize content file names (and therefore paths), making it easier for us to keep track of the same file’s localization status across locales and for users to know they’re on the right page between different locales.

### I18n Helpers

In addition to content and microcopy, we found we needed to write a number of helpers modules to make working with localized content easier. 11ty has a concept called a [filter](https://www.11ty.dev/docs/filters/) that allows content to be modified before being rendered. We wound up building four of them to help with i18n templating.

The first is a [date filter](https://github.com/chromeos/static-site-scaffold-modules/blob/master/modules/static-site-scaffold/lib/11ty/l10n.js#L19-L21). We standardized on having all dates across our content written as a [YAML date value](https://yaml.org/type/timestamp.html) because we mostly write them in YAML and they become available in our templates as a full UTC timestamp. When using the `full-icu` module and config, the date string (content being changed), along with the locale code for the content being rendered, can be passed directly to `Date.toLocaleString` (with optional formatting options) to render a localized date. `Date.toLocaleDateString` can optionally be used instead if you just want the date portion when no formatting options are passed in, instead of the full localized date and time.

The second filter is something we called [`localURL`](https://github.com/chromeos/static-site-scaffold-modules/blob/master/modules/static-site-scaffold/lib/11ty/l10n.js#L23-L31). This takes a local URL (content being changed) and the locale the URL should be in, and swaps them. It changes, for example, `/en/linux` to `/es/linux`.

The final two filters are about retrieving localized information from locale code alone. The third leverages the [iso-639-10](https://www.npmjs.com/package/iso-639-1) module to transform a [locale code into language name](https://github.com/chromeos/static-site-scaffold-modules/blob/master/modules/static-site-scaffold/lib/11ty/l10n.js#L33-L34) in the native language. This we use primarily for our language selector. The fourth uses the [iso-i18n-countries](https://www.npmjs.com/package/i18n-iso-countries) module to retrieve a [list of countries in that language](https://github.com/chromeos/chromeos.dev/blob/trunk/lib/filters/countries.js). This we use primarily for building forms with country lists.

In addition to filters, 11ty has a concept called [collections](https://www.11ty.dev/docs/collections/) which is a grouping of content. 11ty makes a number of collections available by default, and can even build collections off of tags. In a multilingual site, we found that we wanted to build custom collections. We wound up building a number of [helper functions](https://github.com/chromeos/chromeos.dev/blob/trunk/lib/helpers/collections.js) to build collections based on localization. This allows us to do things like have location-specific tag collections or site section collections without needing to filter in our templates against all content on our site.

Our final, and most critical, helper was our [site global data](https://github.com/chromeos/chromeos.dev/blob/trunk/pages/_data/site.js). Relying on the locale-code based subdirectory structure, this function dynamically determines what localizations the site supports. It builds a global variable, `site`, which includes the `l10n` property, containing all of the microcopy and localization-specific content from `{{locale-code}}.11tydata.js`. It also contains a `languages` property that lists all of the available locales as an array. Finally, the function outputs a JavaScript file detailing what languages are supported by the site and individual files for each entry in `{{locale-code}}.11tydata.js`, keyed per localization, all designed to be imported by our browser scripts. The heavy lifting of this file ties our static site to our front-end JavaScript with the single source of truth being the localization information we already need. It also allows us to programmatically generate pages based on our localizations by looping over `site.l10n`. This, combined with our localization-specific collections, let us use 11ty’s [pagination](https://www.11ty.dev/docs/pagination/) to create localized home and news landing pages without maintaining separate HTML pages for each.

## Conclusion

Getting internationalization and localization right can be difficult; understanding how different strategies and affect complexity is critical to making it easier. Pick an i18n strategy that is a natural fit for static sites, subdirectories, then build tools off that to automate parts of i18n and i10n from the content being produced. Build robust content and microcopy models. Leverage service workers for server-agnostic localization. Tie it all together with a design that’s responsive not just to screen size, but content. In the end you’ll have a site that your users of all locales will love that can be maintained by authors and translators as if it were a simple single-locale site.

{{< signature "ra, il" >}}
