---
title: Useful JavaScript Libraries and jQuery Plugins
slug: useful-javascript-libraries-jquery-plugins
image: null
date: 2012-09-27T02:04:38.000Z
author: vitaly-friedman
description: >-
  If you have a problem and need a solution for it, chances are high that a
  JavaScript library or jQuery plugin exists that was created to solve this very
  problem. Such libraries are always great to have in your bookmarks or in your
  local folders, especially if you aren't a big fan of cross-browser debugging.
categories:
  - Coding
  - JavaScript
  - jQuery
---
If you have a problem and need a solution for it, chances are high that a JavaScript library or jQuery plugin exists that was created to solve this very problem. Such libraries are always great to have in your bookmarks or in your local folders, especially if you aren't a big fan of cross-browser debugging.

A JavaScript library isn't always the best solution: it should never be a single point of failure for any website, and neither should a website rely on JavaScript making the content potentially inaccessible. Progressive enhancement is our friend; sometimes JavaScript won't load properly, or won't be supported — e.g. users of mobile devices might run into <a href="https://www.igvita.com/2012/07/19/latency-the-new-web-performance-bottleneck/">latency issues</a> or <a href="https://www.slideshare.net/stoyan/javascript-performance-patterns">performance issues</a> with some JavaScript-libraries. Often large all-around JavaScript libraries such as jQuery might be an overkill, while tiny JavaScript micro-libraries could serve as good, "light" alternatives for a particular problem. We'll present some of them today.

In this two-part overview, we feature <strong>some of the most useful JavaScript and jQuery libraries</strong> which could be just the right solutions for your common problems. You might know some of these libraries, but you probably don't know all of them. In either case, we hope that this overview will help you find or rediscover some tools that you could use in your next projects.

Due to the length of this post, we've split it into two parts for your convenience:

*   **Part 1: Web Forms, Typography, Time-Savers and Images**
*   [Part 2: Text, Tables, Lists and Useful Development Tools](https://www.smashingmagazine.com/useful-javascript-libraries-jquery-plugins-part-2/)

{{% feature-panel %}}

### Quick Overview:

Below you'll find a brief overview and links to the libraries and tools featured in this post. They are supposed to help you find just the right tool quickly without browsing the whole page.

*   **Web Forms:** forms framework - [auto-saving drafts](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/) - [file upload](https://github.com/blueimp/jQuery-File-Upload) (and [resuming large downloads](https://github.com/23/resumable.js)) - [select boxes](https://ivaynberg.github.com/select2/) - [modal boxes](https://labs.voronianski.com/jquery.avgrund.js/) - form accordion - [dynamic labels](https://github.com/remybach/jQuery.superLabels) - [drop-down with images](https://designwithpc.com/Plugins/ddSlick) - [tooltips](https://projects.nickstakenburg.com/tipped) - [extended input](https://textextjs.com/) - [form validation](https://rickharrison.github.com/validate.js/) - credit card validation ([alternative](https://www.egrappler.com/jquery-credit-card-validation-plugin-smart-validate/)) - [email check](https://github.com/Kicksend/mailcheck) - [password complexity](https://github.com/danpalmer/jquery.complexify.js)
*   **Web Typography:** repairing vertical baseline - [align text to a grid](https://github.com/ftlabs/ftcolumnflow) - [responsive measure](https://jbrewer.github.com/Responsive-Measure/) - [fixing widows](https://artequalswork.com/posts/on-widows.php) - [fluid line height](https://nicewebtype.com/notes/2012/02/03/molten-leading-or-fluid-line-height/) - [scalable headlines](https://fittextjs.com/) (or smart headlines) - [Lettering.js](https://letteringjs.com/) - [Kerning.js](https://kerningjs.com/)
*   **Little Time-Savers:** [exchange rates and currency](https://josscrowcroft.github.com/money.js/) - [date/time formatting](https://momentjs.com/) - [relative timestamps](https://pragmaticly.github.com/smart-time-ago/) - [number and currency formatting](https://josscrowcroft.github.com/accounting.js/) - [cookies.js](https://github.com/ScottHamper/Cookies) - [zip.js](https://gildas-lormeau.github.com/zip.js/) - [extra string methods](https://stringjs.com/) - [countdown.js](https://countdownjs.org/) - [sticky content](https://viget.com/inspire/jquery-stick-em) - [Google Maps](https://hpneo.github.com/gmaps/) - interactive maps - [progress bar](https://widgets.better2web.com/loader/) - [favicon notifications](https://lipka.github.com/piecon/) (or [Notificon](https://github.com/makeable/Notificon))
*   **Images, Maps, Graphs:** [world maps](https://jvectormap.com/) - [subway map](https://www.kalyani.com/2010/10/subway-map-visualization-jquery-plugin/) - [Google maps](https://hpneo.github.com/gmaps/) - open source maps - [SVG fallback](https://twostepmedia.co.uk/svgeezy/) - [gauges](https://www.justgage.com/) - [graphs](https://arborjs.org/) - [timeline](https://timeline.verite.co/) - [Retina display](https://retinajs.com/) - [magnifying glass](https://thecodeplayer.com/walkthrough/magnifying-glass-for-images-using-jquery-and-css3) - [interactive graphs](https://code.shutterstock.com/rickshaw/) - [plots](https://www.flotcharts.org/) - [time visualization](https://square.github.com/cubism/)

## Web Forms and Input Validation

#### [Select2 jQuery Plugin](https://ivaynberg.github.com/select2/)

A jQuery-plugin for replacement and enhancement of <code>&lt;select&gt;</code>-boxes. The plugin supports search, remote data sets, and infinite scrolling of results. Users can just start typing what they’re looking for. Non-matching entries are removed from the view, and options can be selected using “Enter” or a mouse click. The plug-in works with standard select input fields as well as with multiple selects and <code>optgroup</code>. It also has support for <code>selected</code>, <code>disabled</code> and default text (HTML5’s <code>placeholder</code> attribute). The plug-in is based on <a href="https://github.com/harvesthq/chosen/">Chosen</a>, an alternative solution which is currently available in jQuery, MooTools and Prototype flavors and as a Drupal 7 module.

<figure><a href="https://ivaynberg.github.com/select2/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f272c7af-5977-4e04-aef2-3f88e58b81db/select2.gif" alt="JavaScript Library" width="500" height="279" /></a></figure>

#### jQueryCoreUISelect

Another cross-browser solution to enhance the <code>&lt;select&gt;</code> element with jQuery and CSS. Requires jQuery 1.6 or higher. It provides full customization, support of <code>optiongroup</code>, automatic calculations, keyboard support, callback functions and is compatible with mobile devices.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2009713b-2eed-4099-9457-dbfd064ab55c/select.png" alt="jQueryCoreUISelect" width="500" height="300" /></figure>

#### [Sisyphus.js](https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/)

This script allows Gmail-like auto-saving of drafts. It stores form data to the HTML5 local storage of the user’s browser and restores it when the user reloads or reopens the page or opens the page in a new tab. The data is cleared from local storage when the user submits or resets the form.

<figure><a href="https://www.smashingmagazine.com/2011/12/05/sisyphus-js-client-side-drafts-and-more/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bddb98e-482c-43ea-adcd-425bb7706f82/sisyphus-js.jpg" alt="Sisyphus.js" width="500" height="289" /></a></figure>

#### jQuery Credit Card Validator

This library attaches to the input event (with a fallback to the keyup event) and so every time a number in the input field changes, it calls a validation function. When a card is recognized, the credit card type is highlighted; and if the credit card number is correct, it is highlighted with a green checkmark as well. The plugin supports American Express, Diners Club, Discover Card, JCB, Laser, Maestro, MasterCard, Visa and Visa Electron. You might want to consider <a href="https://davidwalsh.name/validate-credit-cards">credit cards JavaScript validator</a> and the <a href="https://www.egrappler.com/jquery-credit-card-validation-plugin-smart-validate/">Smart Validate Credit Card Validation plugin</a>.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d84639c9-ec5b-4e80-96f4-f13290198930/jquery-creditcard.jpg" alt="JavaScript Library" width="499" height="398" /></figure>

#### [TextExt](https://textextjs.com/)

This library allows you to transform HTML text into input fields, without resorting to code inflation. The plugin inserts aesthetic as well as practical input possibilities, e.g. Tags, Ajax, Focus and others.

<figure><a href="https://textextjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8db7fc90-ba4f-473e-90ba-b34c280ad3cc/textext.jpg" alt="TextExt" width="499" height="300" /></a></figure>

#### [Avgrund: Better Modal Boxes](https://labs.voronianski.com/jquery.avgrund.js/)

A jQuery plugin for displaying a depth illusion between popup and page. The <a href="https://github.com/hakimel/avgrund/">original script by Hakim El Hattab</a> uses CSS transitions and transformations, and the plugin gracefully degrades in those that do not support transitions and transforms. MIT licensed.

<figure><a href="https://labs.voronianski.com/jquery.avgrund.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a73a1a9e-8b2e-47de-91bb-6bda59b5edbf/modal.png" alt="Avgrund: Better Modal Boxes" width="498" height="313" /></a></figure>

#### [VisualSearch.js](https://documentcloud.github.com/visualsearch/)

This library enhances ordinary search boxes with the ability to autocomplete faceted search queries. You can specify the facets for completion, along with the completable values for any facet. You can retrieve the search query as a structured object, so you don't have to parse the query string yourself.

#### Ideal Forms Framework

A very comprehensive jQuery plugin for building and validating responsive HTML5 forms. It provides keyboard support, customizable input types, "on the spot" validation, localization and HTML5 <code>placeholder</code> polyfill. Supported in IE8+, Chrome, Firefox, Opera, iOS5+, Android 4.0+.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a6b9920-83f3-4391-9d57-930a0a85c4e8/ideal-forms.png" alt="Ideal Forms Framework" width="498" height="307" /></figure>

#### [Mailcheck](https://github.com/Kicksend/mailcheck)

With this JavaScript spell-checker you can suggests another domain when the user misspells it in an email address. Mailcheck helps effectively reducing sign up typos. While it already includes some domains, you can easily supply your own.

<figure><a href="https://github.com/Kicksend/mailcheck"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29beb562-dff6-44be-9d4e-98c4d38f6eb1/mailcheck.gif" alt="Mailcheck" width="503" height="274" /></a></figure>

#### [Validate.js](https://rickharrison.github.com/validate.js/)

A lightweight JavaScript form validation library. You can validate form fields using over a dozen rules and set custom messages; the library doesn't have any dependencies and you can define your own validation callbacks for custom rules. Works in all major browsers (even IE6!).

<figure><a href="https://rickharrison.github.com/validate.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d476c8a1-6dae-4a8c-bb31-ff622f55b4d7/validate-js.jpg" alt="JavaScript Library" width="500" height="273" /></a></figure>

#### [jQuery File Upload](https://github.com/blueimp/jQuery-File-Upload)

File Upload widget with multiple file selection, drag&amp;drop-support, progress bars and preview images. It supports cross-domain, chunked and resumable file uploads and client-side image resizing. Works with any server-side platform (PHP, Python, Ruby on Rails, Java, Node.js, Go etc.) that supports standard HTML form file uploads.

<figure><a href="https://github.com/blueimp/jQuery-File-Upload"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cee9406-8276-47ce-82aa-1d3434f036e6/fileupload-jquery.jpg" alt="JavaScript Library" width="500" height="332" /></a></figure>

#### [Grumble.js](https://jamescryer.github.com/grumble.js/)

This jQuery plugin provides tool tips without being limited to cardinal directions. A <em>grumble</em> can be rotated around a given element at any angle, all 360 degrees and at any distance — with CSS. Works in Internet Explorer 6+ and modern browsers. Also, check <a href="https://projects.nickstakenburg.com/tipped">Tipped</a>, a larger library of various designs and implementations of tooltips with an extensive API.

<figure><a href="https://jamescryer.github.com/grumble.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22534814-2a0b-4590-8f61-387bd0361705/grumble-js.jpg" alt="Grumble.js" width="500" height="309" /></a></figure>

#### [Dialogs for Twitter Bootstrap](https://bootboxjs.com/)

A small JavaScript library which allows you to create dialog boxes using Twitter's Bootstrap modals, without having to worry about creating, managing or removing any of the required DOM elements or JS event handlers. You might want to check out the <a href="https://www.dangrossman.info/2012/08/20/a-date-range-picker-for-twitter-bootstrap/">Date Range Picket for Bootstrap</a> as well as a growing library of <a href="https://bootsnipp.com/">HTML Snippets for Twitter Bootstrap</a>.

<figure><a href="https://bootboxjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6203718e-e600-4ef7-95a0-a25b8f987c4f/bootbox.jpg" alt="JavaScript Library" width="500" height="184" /></a></figure>

#### [ddSlick](https://designwithpc.com/Plugins/ddSlick)

Prashant Chaudhary has realeased a free lightweight jQuery plugin that lets you create a custom drop-down that can include images, a short description, along with your usual text and value. It also supports callback functions on selection. You could use <a href="https://azadcreative.com/2012/01/bulletproof-css3-dropdown-navigation-menu/">CSS3 Drop-Downs</a> as well.

<figure><a href="https://designwithpc.com/Plugins/ddSlick"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cef3581d-8394-4a01-aa18-6a14e4c37b70/ddslick.jpg" alt="ddSlick" width="499" height="341" /></a></figure>

#### [noty](https://needim.github.com/noty/)

This jQuery plugin makes it easy to create alert, success, error, warning, information and confirmation messages. The notification can be positioned anywhere on the page and you can customize the text, animation, speed and buttons easily.

<figure><a href="https://needim.github.com/noty/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fae60a99-8ceb-4df3-87d8-d61eb42d4d2d/noty1.jpg" alt="noty" width="500" height="218" /></a></figure>

#### [jQuery.complexify.js](https://github.com/danpalmer/jquery.complexify.js)

Complexify helps you to accurately gauge the quality of a user's password to give them visual feedback, and to enforce a minimum level of security.

<figure><a href="https://github.com/danpalmer/jquery.complexify.js"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28346827-2584-45f2-b364-652e094db636/complexify.png" alt="JavaScript Library" width="423" height="288" /></a></figure>

#### Numberfy

With Numberfy you can integrate native support for line numbers in your website's text areas. On every key press in the text area, the text area’s current value is split into lines. This script will not work in IE due to a bug in the text-wrap properties.

#### FormAccordion

A jQuery plugin for easily hiding and revealing related form fields conditionally.

#### [jQuery.superLabels](https://github.com/remybach/jQuery.superLabels)

You can use the library to give your forms a fade-out label. This implementation makes the label slide across the field when gaining focus and fade out when a value is entered. A fallback is provided as well.

#### [cryptico](https://github.com/wwwtyro/cryptico)

An encryption system utilizing RSA and AES for JavaScript.</p>

## Web Typography Libraries and Plugins

#### Baseline.js

A jQuery plugin for restoring baselines thrown off by odd image sizes. To use it, you just call the plugin passing the height of your baseline as a variable. You can also define multiple baselines for different responsive breakpoints.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e8460d1-abbc-44a8-ab91-e81eacff581b/baseline-js.png" alt="Baseline.js" width="500" height="302" /></figure>

#### [FTColumnflow](https://github.com/ftlabs/ftcolumnflow)

Developed by the development team of Financial Times, this library is essentially a polyfill that fixes the inadequacies of CSS column layouts. With the library, you can provide configurable column widths, gutters and margins, define elements spanning columns, keep-with-next to avoid headings at the bottom of a column, group columns into pages and standardize line height to align text baseline to a grid.

<figure><a href="https://github.com/ftlabs/ftcolumnflow"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ff192dd-3a8b-4fca-863e-68c46ca8b301/financialtimes.gif" alt="FTcolumnflow" width="500" height="375" /></a></figure>

#### [Responsive Measure jQuery Plugin](https://jbrewer.github.com/Responsive-Measure/)

A simple script that allows you to pass in a selector (ideally the container where your primary content will go), which generates the ideal font size needed to produce the ideal measure for your text. The script also generates a resolution-independent font-scale based on the ideal font-size. Created by Josh Brewer.

<figure><a href="https://jbrewer.github.com/Responsive-Measure/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf874ac6-2f03-4177-834f-247909d64a14/responsive-measure.gif" alt="Baseline.js" width="498" height="289" /></a></figure>

#### [The Widow Tamer](https://artequalswork.com/posts/on-widows.php)

The Widow Tamer is a small JavaScript library that automatically "fixes" typographic widows. It's designed to work with responsive sites, fixing widows as it finds them on resize or orientation change.

<figure><a href="https://artequalswork.com/posts/on-widows.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41214d44-9884-4db7-b0b5-a1cf56685cf0/widow-tamer.gif" alt="JavaScript Library" width="500" height="304" /></a></figure>

#### [Fluid Line-Height](https://nicewebtype.com/notes/2012/02/03/molten-leading-or-fluid-line-height/)

With his article, Tim Brown inspired developers to release tools that adjust <code>line-height</code> for optimum readability on responsive websites. The so-called <em>molten-leading</em> binds the height of the line to an element's minimum and maximum width. jQuery-minLineHeight is a jQuery plugin that works similarly with minimum and maximum width association.

<figure><a href="https://nicewebtype.com/notes/2012/02/03/molten-leading-or-fluid-line-height/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef1cc126-930a-4dc3-9308-dd9f5755e853/molten-leading.gif" alt="Nice Web Type" width="500" height="195" /></a></figure>

#### [FitText.js](https://fittextjs.com/)

This jQuery plugin helps you create scalable headlines that fill the width of a parent element in your fluid or responsive layouts. You might want to check out <a href="https://fittextjs.com/">Lettering.js</a> as well to get a complete down-to-the-letter control of letters in your projects.

<figure><a href="https://fittextjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2b4fe68-589f-4e13-b498-3d86597b9d2b/fittextjs1.jpg" alt="FitText.js" width="500" height="267" /></a></figure>

#### [Kerning.js](https://kerningjs.com/)

This library lets you kern, style, transform, and scale your Web type with CSS rules, automatically. You can adjust pairings, introduce font conditionals and augment properties.

<figure><a href="https://kerningjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f30a5c2d-ebd2-4e63-88de-366c4c0ddf17/kerningjs1.gif" alt="Kerning.js" width="500" height="212" /></a></figure>

#### SlabText.js

The script splits headlines into rows before resizing each row to fill the available horizontal space. The ideal number of characters to set on each row is calculated by dividing the available width by the pixel font-size – the script then uses this ideal character count to split the headline into word combinations that are displayed as separate rows of text.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/675203ab-4b58-4988-b411-398516f788dc/slabtextjs1.gif" alt="Nice Web Type" width="500" height="353" /></figure>

## Little Time-Savers

#### [money.js: Open-Source Exchange Rates and Currency Conversion](https://josscrowcroft.github.com/money.js/)

Joss Crowcroft has created an <em>Open Source Exchange Rates API</em>, which provides up-to-date, flexible and portable currency-conversion data that can be used in any application, framework or language (not just JavaScript). It has no access fees, no rate limits, no nasty XML: just free, hourly updated exchange rates in JSON. Joss also built <em>money.js</em>, a JavaScript currency conversion library that can be easily integrated in any website. A demo playground and detailed documentation are provided on the website, and the source code is available on GitHub.

<figure><a href="https://josscrowcroft.github.com/money.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e134a87b-2344-4557-bff3-52d998709e23/money-js.gif" alt="JavaScript Library" width="500" height="246" /></a></figure>

#### [Accounting.js: Easier Number and Currency Formatting](https://josscrowcroft.github.com/accounting.js/)

This simple, tiny JavaScript library will solve your currency and numbers-related formatting hassles, and it even includes optional Excel-style column rendering to line up symbols and decimals. It will make all of your numbers and currencies look much more uniform and professional.

<figure><a href="https://josscrowcroft.github.com/accounting.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f08742a7-16e2-4d8c-8305-5d4c22441b3e/accounting-js.gif" alt="JavaScript Library" width="500" height="246" /></a></figure>

#### [Moment.js: Format Dates And Times](https://momentjs.com/)

<em>Moment.js</em> is a lightweight JavaScript library which lets you format, parse and manipulate dates. You can add or subtract dates from one another, as well as parse things like Unix Timestamps. Display options include formatted dates, time from now, difference, time from another moment, native date and support for leap years.

<figure><a href="https://momentjs.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4664b225-7395-4eff-90ca-4158f63171f7/moment-js.gif" alt="JavaScript Library" width="500" height="279" /></a></figure>

#### [Smart Time Ago](https://pragmaticly.github.com/smart-time-ago/)

This little jQuery library provides you with an intelligent way of updating relative timestamps in your documents. <em>Smart Time Ago</em> checks and updates every 60 seconds the relative time, within a scope which you specify at the start. It checks the newest time in your scope and tunes the checking time interval to a proper value. The tool can be used as a jQuery plugin, or - if using node - can be installed from npm.

<figure><a href="https://pragmaticly.github.com/smart-time-ago/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93fa6c1e-a3b4-4034-bb59-65cee91d31c1/js-libraries-102.jpg" alt="Smart Time Ago" width="500" height="300" /></a></figure>

#### [sortByTimeAgo.js](https://github.com/cjstewart88/sortByTimeAgo)

A little JavaScript library that takes an array of objects with <code>TimeAgo</code> properties and sorts them from newest to oldest.

#### [Piecon](https://lipka.github.com/piecon/)

Piecon is a tiny JavaScript library for dynamically generating progress pie charts in your favicons. It has been tested to work in Chrome 15+, Firefox 9+ and Opera 11+.

<figure><a href="https://lipka.github.com/piecon/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6913c4bd-a105-4e89-8212-a1abecbdeb17/piecon.jpg" alt="Piecon" width="500" height="126" /></a></figure>

#### [Notificon: Favicon Notifications and Alerts](https://github.com/makeable/Notificon)

Matt Williams' <em>Notificon</em> is a JavaScript library for creating favicon alerts and notifications. Instead of having to create a number of favicons and serving them to the client, you can specify a label and a favicon (the default being the current favicon), and it will generate a favicon notification for you. The script currently works with Chrome 6+, Firefox 2+ and Opera, but it's a nice little add-on for browsers that support it.

#### [jQuery Stick ‘em: Make Content Sticky on Scroll, to a Point](https://viget.com/inspire/jquery-stick-em)

A problem: some of the images in the layout are very tall, so by the time you scrolled down to the bottom of the images, you would have to scroll back up just to read the description of the images or navigation items. The solution: make the content sticky as you are scrolling. This library solves this problem.

<figure><a href="https://viget.com/inspire/jquery-stick-em"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f7a7426-a3fc-4200-82f9-4084328c538e/viget2.jpg" alt="jQuery Stick 'em" width="500" height="280" /></a></figure>

#### [Countdown.js](https://countdownjs.org/)

Human descriptions for a span of time are often fuzzier than a computer naturally computes. For example, how long does "in 1 month" mean? We casually talk about four weeks, but in fact there is only one month in a year which is four weeks long. <em>Countdown.js</em> tackles this problem by producing an accurate and intuitive description of timespans which are consistent as time goes on.

#### [geolib](https://github.com/manuelbieh/geolib)

A small library to provide some basic geo functions like distance calculation, conversion of decimal coordinates to sexagesimal and vice versa.

<figure><a href="https://github.com/manuelbieh/geolib"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8e9b957-ef77-4aa4-bd85-71ba9f77b149/geolib.jpg" alt="Geolib.js" width="500" height="286" /></a></figure>

#### [Cookies.js](https://github.com/ScottHamper/Cookies)

Cookies.js is a small client-side JavaScript library that makes managing cookies easy. It caches cookie values, making sequential reads faster, supports AMD / CommonJS loaders and is supported in Chrome, Firefox 3+, Safari 4+, Opera 10+ and Internet Explorer 6+.

#### [firstImpression.js](https://www.ravelrumba.com/blog/firstimpression-js-library-detecting-new-visitors/)

firstImpression.js is a micro-library (1 Kb minified) that answers the simple question, “Has this user visited this site before?” The detection doesn’t require much logic, so the majority of the code is just a plain JavaScript port of the popular <a href="https://github.com/carhartl/jquery-cookie">jquery.cookie</a> plugin.

#### [Chirp.js: Tweets on Your Website](https://lab.rog.ie/chirp/)

A lightweight templating JavaScript library that enables you to display tweets on your website. Client-side caching is available; and you can set if you'd like to show retweets and replies, too.

<figure><a href="https://lab.rog.ie/chirp/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/914d24ab-6936-4533-a3fe-78b4f791e1b8/chirp-js.png" alt="Chirp.js: Tweets on your website" width="500" height="293" /></a></figure>

#### [simpleWeather jQuery Plugin](https://monkeecreate.github.com/jquery.simpleWeather/)

A simple jQuery plugin to display the weather information for any location. The data is pulled from the public Yahoo! Weather feed via the YQL API.

#### [zip.js](https://gildas-lormeau.github.com/zip.js/)

A JavaScript library to zip and unzip files. <em>zip.js</em> provides a low-level API for writing and reading large zip files (up to 4GB with File Writer API). Works with Chrome, Firefox, Safari 6 and (unfortunately) Internet Explorer 10+. With Safari 5 and IE9, you must disable Web Workers and use a <a href="https://bitbucket.org/lindenlab/llsd/raw/7d2646cd3f9b/js/typedarray.js">Typed Array polyfill</a>.

#### [string.js](https://stringjs.com/)

A library that provides extra String methods to normalize text strings and manipulate them.</p>

## Images, Maps, Graphs and Visualization Libraries

#### [jVectorMap](https://jvectormap.com/)

jVectorMap is a jQuery plugin that renders SVG and VML vector maps in browsers ranging from the ancient Internet Explorer 6 to modern browsers. jVectorMap uses JavaScript, CSS, HTML, SVG or VML, and no Flash or any other proprietary browser plugin is required.

<figure><a href="https://jvectormap.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c35d1238-1bb5-4a0c-a5c5-f26eee03aea8/js7.png" alt="JavaScript Library" width="500" height="300" /></a></figure>

#### [Subway Map Visualization jQuery Plugin](https://www.kalyani.com/2010/10/subway-map-visualization-jquery-plugin/)

If you often deal with government projects, university departments or any websites of sophisticated organizations, every now and again you'll be asked to design a nice visualization that would explain the various divisions, structures and internal hierarchy of those organizations. Where do you start? Well, creating a Subway Map-alike visualization is an option worth considering.

<figure><a href="https://www.kalyani.com/2010/10/subway-map-visualization-jquery-plugin/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8ca8bf8-af99-4621-a4f1-c9251cc229fe/nl-12.jpg" alt="JavaScript Library" width="500" height="300" /></a></figure>

#### [GMaps.js](https://hpneo.github.com/gmaps/)

This library allows you to easily use Google Maps in your projects. Extensive documentation or large amount of code aren't required anymore. You might want to check out <a href="https://gmap3.net/">Gmap3 jQuery plugin</a> as well.

<figure><a href="https://hpneo.github.com/gmaps/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65c47f88-f510-4824-8bcf-105452fff5c7/gmaps.jpg" alt="GMaps.js" width="500" height="299" /></a></figure>

#### Leaflet: Open-Source Interactive Maps With JavaScript

A library for creating tile-based interactive maps for desktop and mobile browsers. An easy-to-use API is available, and the tool emphasizes usability, performance, flexibility and excellent browser support. The library offers a variety of map layers, including tiles, markers, pop-ups, image overlays and GeoJSON. It supports panning on both mobile and desktop browsers, double-tap zoom on mobile browsers (plus multi-touch zoom on iOS) and more. On iOS, hardware acceleration is enabled, and Leaflet has a modular structure that lets you reduce the size of the library to make it even faster. The project is open source and available for further development and forking on GitHub.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8138844-1e29-42b4-a8c6-bcf6803ebcf6/leaflet.jpg" alt="JavaScript Library" width="495" height="280" /></figure>

#### [SVGeezy: a JavaScript plugin for SVG fallbacks](https://twostepmedia.co.uk/svgeezy/)

A JavaScript library which detects SVG images on your website and automatically "looks" for a standard image fallback for those older, less capable browsers. Created by Ben Howdle and Jack Smith.

<figure><a href="https://twostepmedia.co.uk/svgeezy/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09ef10a7-6d64-470e-8976-d8c382e9c9b8/svg.png" alt="SVGeezy - a JS plugin for SVG fallbacks" width="500" height="242" /></a></figure>

#### [Retina.js](https://retinajs.com/)

A script that checks each image on your website, when it's loaded by a user, and replaces low-resolution image with their high-resolution equivalent, if available. It's assumed that you use Apple's high resolution modifier (<code>@2x</code>) to designate high resolution versions of images.

#### [JustGage](https://www.justgage.com/)

A JavaScript library for generating and animating gauges. Based on Raphaël library for vector drawing, it’s resolution-independent and works in all modern browsers.

<figure><a href="https://www.justgage.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf516bc-8b81-4515-be09-5ea3bb5a16e6/gauge.gif" alt="JustGage" width="500" height="303" /></a></figure>

#### [arbor.js](https://arborjs.org/)

A graph visualization library for building trees with connected nodes of data. Arbor.js is essentially a layout algorithm with abstractions for graph organization and screen refresh handling.

<a href="https://arborjs.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09067e8-79a2-4b28-b67e-eae658662940/atlas.gif" alt="Arbor.js" width="500" height="286" /></a>

#### [Timeline: Generate Timelines To Visualize Data](https://timeline.verite.co/)

This library is supposed to pull in media from different sources. It has built-in support for pulling in data from Twitter, YouTube, Flickr, Vimeo, Google Maps and SoundCloud—and more will be included in the near future. You can easily fill in data from a Google spreadsheet, or use a more detailed method such as JSON to create your time-line. You can also host it on your website by using the Timeline jQuery plugin. The library is available on <a href="https://github.com/VeriteCo/Timeline">GitHub</a>, or as <a href="https://wordpress.org/extend/plugins/timeline-verite-shortcode/">WordPress plugin</a>.

<figure><a href="https://timeline.verite.co/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b389fd7-4154-4c27-a65b-8ded1dccac9a/nl-61.jpg" alt="JavaScript Library" width="499" height="300" /></a></figure>

#### [Unicon](https://github.com/filamentgroup/unicon)

Unicon is a Grunt.js task that makes it easy to manage icons and background images for all devices, preferring HD (retina) SVG icons but also provides fallback support for standard definition browsers, and old browsers alike. From a CSS perspective, it's easy to use, as it generates a class referencing each icon, and doesn't use CSS sprites.

#### [Foresight.js](https://github.com/adamdbradley/foresight.js)

This device recognition library, gives websites the ability to gauge the users device capabilities before the image is requested from the server. Judging display resolution and network speed, it customizes the img src attribute to optimize the websites image resolution to the individual users hardware.

#### [A Magnifying Glass With CSS3 And jQuery](https://thecodeplayer.com/walkthrough/magnifying-glass-for-images-using-jquery-and-css3)

This technique achieves an aesthetically pleasing visual effect. The CSS3 <code>box-shadow</code> and <code>border-radius</code> properties are used to create the magnifying glass itself, while jQuery is used to detect the cursor coordinates and mouse movements and present the larger image. And when your cursor moves off the image, the magnifying glass elegantly fades away. The included tutorial makes it very easy to learn and understand how to achieve this effect. The technique includes both a small and a large image in the markup, so optimizing the technique to load a larger image on demand might be a good idea.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078394f1-023f-4c05-8d1a-24d8987a14c2/nl-2.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078394f1-023f-4c05-8d1a-24d8987a14c2/nl-2.jpg" alt="JavaScript Library" width="500" height="300" /></a></figure>

#### [Rickshaw](https://code.shutterstock.com/rickshaw/)

This free and open source JavaScript toolkit provides the elements which you need to create interactive graphs, such as renderers, legends, hovers and range selectors. Rickshaw is based on D3, graphs are drawn with standard SVG and styled with CSS.

<figure><a href="https://code.shutterstock.com/rickshaw/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03fb7d38-8d0c-417d-8a93-7ccba2de269f/js-libraries-111.jpg" alt="Rickshaw" width="500" height="300" /></a></figure>

#### [Flot: Plotting for jQuery](https://www.flotcharts.org/)

A JavaScript plotting library for jQuery, supports Internet Explorer 6+, Chrome, Firefox 2+, Safari 3+ and Opera 9.5+. You can use different types of graphs, use multiple axes, annotate a chart, update graphs with AJAX, provide support for zooming and interaction with the data points, use stacked charts, theresholding the data, apply pie charts and plot prerendered images.

<figure><a href="https://www.flotcharts.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59524058-62ce-4152-954a-f8bc7b33e1d9/flotjs.jpg" alt="Flot.js" width="500" height="320" /></a></figure>

#### [Chronoline.js](https://stoicloofah.github.com/chronoline.js/)

<em>Chronoline.js</em> is a library that allows you to create a chronology time-line out of events on a horizontal timescale. From a list of dates and events, it can generate a graphical representation of schedules, historical events, deadlines, and more.

<figure><a href="https://stoicloofah.github.com/chronoline.js/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c86ff7-ccb9-4e44-92e8-c7a954114f3a/js13.png" alt="JavaScript Library" width="500" height="300" /></a></figure>

#### [Cubism](https://square.github.com/cubism/)

This D3 plugin helps you to visualize time series and construct better real-time dashboards, pulling data from Graphite, Cube and other sources. Cubism scales and reduces server load by pulling only the most recent values. Cubism can scale easily to hundreds of metrics updating every ten seconds. Cubism’s horizon charts allow you to see many more metrics at-a-glance space than standard area charts.

<figure><a href="https://square.github.com/cubism/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/981d54ea-ae10-46f0-a6ea-6b000ea54b91/js-libraries-112.jpg" alt="Cubism" width="500" height="300" /></a></figure>

#### [Envision.js](https://www.humblesoftware.com/envision)

An alternative library for creating fast, dynamic and interactive HTML5 visualizations.

<figure><a href="https://www.humblesoftware.com/envision"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a4d9f5a-4d7e-4545-b337-78ba044ba716/js9.png" alt="JavaScript Library" width="500" height="300" /></a></figure>

#### [Data Visualization JavaScript Libraries](https://selection.datavisualization.ch)

A growing, curated collection of data visualization JavaScript libraries that make it easier to create meaningful and beautiful data visualizations. If you haven't one a useful data visualization library in the list above, you'll definitely find the right one in this overview.

<figure><a href="https://selection.datavisualization.ch"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c5ac8d-1762-468e-b3ce-f32c84245c9b/dataviz.png" alt="Data Visualization JavaScript Libraries" width="500" height="338" /></a></figure>

## Last Click

#### [jQuery Fundamentals](https://jqfundamentals.com/)

This HTML book is designed to get you comfortable working through common problems you'll be called upon to solve using jQuery. You can read the content and try the various interactive examples. Each chapter will cover a concept and give you a chance to try example code related to the concept. Written by Rebecca Murphey and recently updated by her and the rest of the gang at Bocoup.

<figure><a href="https://jqfundamentals.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01b0ee96-ec06-4b8d-a8c7-bf7fb9eee977/jquery-fundamentals.gif" alt="JavaScript Library" width="500" height="296" /></a></figure>

#### [JavaScript Patterns Collection](https://shichuan.github.com/javascript-patterns/)

A JavaScript pattern and anti-pattern collection that covers function patterns, jQuery patterns, jQuery plugin patterns, design patterns, general patterns, literals and constructor patterns, object creation patterns, code reuse patterns, DOM and browser patterns.

<figure><a href="https://shichuan.github.com/javascript-patterns/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ca04ad8-dfd3-46b9-b2fe-830c477610f4/js-patterns.gif" alt="JavaScript Library" width="500" height="249" /></a></figure>

#### [JavaScript Garden](https://bonsaiden.github.com/JavaScript-Garden/)

A growing collection of documentation about the most quirky parts of the JavaScript programming language. It gives advice to avoid common mistakes and subtle bugs, as well as performance issues and bad practices, that non-expert JavaScript programmers may encounter on their endeavors into the depths of the language.

<figure><a href="https://bonsaiden.github.com/JavaScript-Garden/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59e2a359-5d10-4db0-bb41-c7d397ebc74b/javascript-garden.gif" alt="JavaScript Library" width="500" height="301" /></a></figure>

## Useful JavaScript and jQuery Libraries: Two Parts

Due to the length of this resource, it was split into two parts:

*   **Part 1: Web Forms, Typography, Time-Savers and Images**
*   [Part 2: Text, Tables, Lists and Useful Development Tools](https://www.smashingmagazine.com/useful-javascript-libraries-jquery-plugins-part-2/)

