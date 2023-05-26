---
title: 'CSS Grid Challenge: Winners and Templates'
slug: css-grid-challenge-2017-winners
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a750d2ef-811b-4453-b88a-89597e3f36a3/the-deck-500w-opt.png
date: 2017-10-06T20:55:18.000Z
author: cosima-mielke
description: >-
  [CSS
  Grid](https://www.smashingmagazine.com/2017/06/building-production-ready-css-grid-layout/)
  is becoming the **new layout standard** for the web, and we are all still
  experimenting with what we can achieve with it.
categories:
  - CSS
  - CSS Grid
---
One of the main reasons behind the idea of the [CSS Grid Challenge](https://www.smashingmagazine.com/2017/09/the-css-grid-challenge-join-in/) was to have some starting points for layouts, and **show what can be achieved with CSS Grids today**. Well, we received some many great submissions that it was really hard to choose _the_ one winner — there are so many submissions who deserve to win first place.

While the [browser support](https://caniuse.com/?feat=css-grid#feat=css-grid) for CSS Grid is really good already, it isn't supported in the older browser versions. That's why we challenged you to implement fallbacks for browsers that don't support CSS Grid just yet, and most of the submissions were doing fine in that regard. [Falling back to floats and Flexbox](https://www.smashingmagazine.com/2017/07/enhancing-css-layout-floats-flexbox-grid/) isn't hard, but still not all submissions were providing fallbacks for browsers that don't support CSS Grid. We had to deduct some points in these cases, unfortunately.

So without a further ado, let's look at the submissions which we think are the most impressive ones:

## ? The Winner Of The CSS Grid Challenge 2017 Is... James Clarke!

James Clarke’s CSS-only [The Deck](https://www.hi.agency/deck/) ([download the template](https://smashingmagazine.com/provide/css-grid-challenge/deck-css-grid-template.zip), ZIP, 1.3MB) is particularly well suited for a linear narrative that you might find in presentations or marketing pages. What we think was particularly interesting is the cross-horizontal way to navigate between the different pages. Also, we like the use of lots of whitespace, so that the focus of each page remains perfectly obvious.

{{% feature-panel %}}

**Please keep in mind**: This template isn't keyboard-accessible and we're working with James to improve it.

<figure><a href="https://www.hi.agency/deck/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/315d9597-46b6-440f-8704-a4bb4a10d251/the-deck-opt.png" alt="The Deck by James Clarke" /></a><figcaption><a href="https://www.hi.agency/deck/">View the submission</a></figcaption></figure>

On smaller devices, the template turns into a regular layout, and it falls back graciously on browsers that don't support CSS Grid. Ladies and Gents, a big round of applause for the winner of the CSS Grid challenge!

{{< vimeo id="237045078" >}}

Insights from James himself:

<blockquote>"As CSS grid layout is new technology and sits atop many other advances that have been built into CSS, I chose to limit myself to see what I could build with HTML and CSS alone. I elected to rebuild an old website from about 10years ago that was built using the then-popular "MooTools" javascript library. That library opened up the ease of cross-browser javascript development at the time, and the advance in CSS's capabilities seemed to offer a similar possibility.

The result of my efforts I call "Deck". It is a format that is particularly well suited to the sort of linear narrative that you might find in a power-point presentation, or marketing pages. The standard these days is a long-scrolling page. That format works well of course, but it is undifferentiated, and we've been stuck with it for years now. I wanted to explore something a bit different, in hopes of finding a new way."

<strong>Features</strong>: CSS only, no javascript. All interactions flow from native browser functions and CSS pseudo-selectors like :checked, :target.

<strong>CSS Grid Layout</strong>: horizontal and vertical positioning, source re-ordering, adaptation to different viewports.

<strong>Progressive-enhancement, responsive layouts</strong>: Smaller screen devices and older browsers receive a format catered to their needs and technologies.

<strong>Touch friendly</strong>: All UI functions play well with touch-screen laptops/tablets/phones.

<strong>Back/Forward button navigation</strong>: Back and forward buttons remain functional where browser support exists (current issues with MS Edge repainting when not initiated by javascript 'hash-change' event).
</blockquote>

## But Wait... There's More!

We received a number of really impressive submissions and so we decided to give out a silver as well as a bronze medal, too!

### ? Second Place: Frida Nyvall

The second place goes to [The Daily Prophet](https://redonion.se/cssgrid/), a fictional newspaper for wizards built with Grid. It's a great example for multi-column layouts that respond to smaller screen sizes. You can tell that the creator put a lot of effort into building this page with its subtle animations, using CSS Shapes, and a very thoughtful transformation of layout throughout all the different screen sizes. The only downside here is that the submission is not working in browsers that don't support CSS Grid.

<figure><a href="https://redonion.se/cssgrid/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f8bf9e-507c-4047-8871-59f41df6f0ee/daily-prophet-opt.png" alt="A screenshot of the Daily Prophet, a phantasy, multi-column layout website built with CSS Grid" /></a><figcaption>A screenshot of the Daily Prophet, a phantasy, multi-column layout website built with CSS Grid. Go to the project: <a href="https://redonion.se/cssgrid/">link</a></figcaption></figure>

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/236890867" width="640" height="600" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>Click to see how the site transforms over various screen sizes.</figcaption>

### ? Third Place: Victor Janin

The third place goes to [Victor Janin](https://codepen.io/victorjanin/full/oGYvjK/): A great example of a demo that moves elements around in the grid from mobile to desktop. Victor's aim was to better accommodate the needs of the user in each viewport, and we think he did a brilliant job doing that! The CodePen code doesn’t include all the prefixes and adjustments for Edge and IE but [this live page](https://victorjan.in/boarding/) has all the prefixes and works on Edge and IE 11 in place. The content is available down to IE8.

<figure><a href="https://codepen.io/victorjanin/full/oGYvjK/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90af835a-02d0-48d7-8aa2-324438daf9ef/21-victor-janin-opt.png" width="800" height="482" alt="CSS Grid by Victor Janin" /></a><figcaption><a href="https://codepen.io/victorjanin/full/oGYvjK/">View on CodePen</a></figcaption></figure>

{{< vimeo id="237044635" >}}

The winners have already been contacted. For those who didn't receive an email from us — please stay tuned! We'll be launching another challenge very soon!

## Other Submissions

Again, we're sorry that we only had to choose a limited amount of winners, and want to thank everyone who participated in this challenge — **we sincerely appreciate your time and efforts**! Another round of applause for the rest of the talented participants and their submissions:

### Sam Beckham

Sam Beckham is a fan of Penguin Books and their marber grid. His CSS take on the subject lets you change the colors, font sizes, and everything else you fancy on individual books using BEM notation. You can also view a version that works in IE8 (apart from the SVGs) [here](https://codepen.io/samdbeckham/pen/MEKYPd?editors=1100).

<figure><a href="https://codepen.io/samdbeckham/pen/Naxxgy?editors=1100"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a6d2da-fa60-4b89-9a34-0af93dc9e411/10-sam-beckham-opt.png" width="800" height="387" alt="CSS Grid by Sam Beckham" /></a><figcaption><a href="https://codepen.io/samdbeckham/pen/Naxxgy?editors=1100">View on CodePen</a></figcaption></figure>

### Ren Aysha

A thumbnail presentation with CSS Grid, inspired by Polygon.com's bevel treatment on some of their thumbnails. Older browsers get a fallback with a conservative thumbnail look instead. Apart from her contest submission, you’ll find more CSS Grid experiments on [Ren’s CodePen](https://codepen.io/collection/nvggZM/).

<figure><a href="https://codepen.io/rrenula/pen/VMWMWx"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9405019-e0d1-4632-8d22-de357e7e0ccb/27-ren-aysha-opt.png" width="800" height="440" alt="CSS Grid by Ren Aysha" /></a><figcaption><a href="https://codepen.io/rrenula/pen/VMWMWx">View on CodePen</a></figcaption></figure>

### Trang B. Nguyen

This layout features some lovely sea creatures, a bottom navigation, as well as an different way to navigate through the various sections of the site. Also, it falls back really good in browsers that don't support CSS Grid.

See the Pen [CSS Grid Layout](https://codepen.io/Trangbnguyen/pen/GMNQGN/) by Trang B. Nguyen ([@Trangbnguyen](https://codepen.io/Trangbnguyen)) on [CodePen](https://codepen.io).

<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/236898210" width="640" height="400" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe><figcaption>Click to see how the layout behaves on bigger screens.</figcaption>

### Charles Wong

Beethoven’s “Ode to Joy” as a responsive sheet music page. It consists of two CSS grid layouts - one for positioning the bars within the rows of sheet music, and one for positioning musical notes within the bars. Charles shares more insights into the project [here](https://sejikco.github.io/CssGridSheetMusic/).

<figure><a href="https://github.com/Sejikco/CssGridSheetMusic"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd116076-c96f-495c-a6a7-31bb01ec18cc/15-charles-sejikco-opt.png" width="800" height="531" alt="CSS Grid by Charles Sejikco" /></a><figcaption><a href="https://github.com/Sejikco/CssGridSheetMusic">View on Github</a></figcaption></figure>

### Dannie Vinther

A Marvel poster made with CSS and Clip-path. A sprinkle of JavaScript helps avoid layout reflow when images are fully loaded.

<figure><a href="https://codepen.io/dannievinther/pen/EvVggR"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e0257c0-68fd-4153-bfe0-3a1a567295ed/02-dannie-vinther-opt.png" width="800" height="428" alt="CSS Grid by Dannie Vinther" /></a><figcaption><a href="https://codepen.io/dannievinther/pen/EvVggR">View on CodePen</a></figcaption></figure>

### Erik Davidsson

<p>A great one for football fans! A layout featuring the upcoming football game between FC Barcelona and Real Madrid. Erik brought it to life with many different techniques with fallbacks to make the website usable in older browsers such as IE8 and IE9.</a><br>
<figure><a href="https://erikdson.github.io/smashing-grid-challenge/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cfd8efe-8467-40c7-9b5e-20b81b97ac2d/36-erik-davidsson-opt.png" width="800" height="436" alt="CSS Grid by Erik Davidsson" /></a><figcaption>(<a href="https://erikdson.github.io/smashing-grid-challenge/">CodePen</a>) (<a href="https://github.com/erikdson/smashing-grid-challenge">GitHub</a>)</figcaption></figure>

### Mathieu

Inspired by [Justin Avery’s CodePen](https://codepen.io/justincavery/pen/yaRLYE/), Mathieu submitted a dynamic periodic table built with CSS Grid.

<figure><a href="https://github.com/pulsardev/mendelable"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16490f98-9d56-4789-96de-14cfa6a74d1a/06-mathieu-opt.png" width="800" height="444" alt="CSS Grid by Mathieu" /></a><figcaption><a href="https://github.com/pulsardev/mendelable">View on Github</a></figcaption></figure>

### Amy DeVoogd

Inspired by the works of Jen Simmons and Rachel Andrew, [Spacebar](https://amydevoogd.github.io/product-showcase/) is a product showcase for a completely invented product that Amy branded and designed, i.e. all imagery is copyright-free.

<figure><a href="https://amydevoogd.github.io/product-showcase/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c63079d6-3aca-4807-84c3-014ad3f6ffc0/space-bar-2-opt.jpg" width="500" height="567" alt="CSS Grid by Amy DeVoogd" /></a><figcaption><a href="https://github.com/amydevoogd/product-showcase">View on GitHub</a></figcaption></figure>

### Ieva Ozolīte

A mobile-first semantic web page for a [band poster](https://www.swissted.com/products/the-cure-at-canterbury-odeon-1979). Quite impressive for a first experiment with CSS Grid, don't you agree?

<figure><a href="https://codepen.io/IevaOzolite/pen/xdaVJq"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be3ae757-7fc3-43cb-83de-051ba0d57909/25-ieva-ozolite-opt.png" width="800" height="535" alt="CSS Grid by Ieva Ozolīte" /></a><figcaption><a href="https://codepen.io/IevaOzolite/pen/xdaVJq">View on CodePen</a></figcaption></figure>

{{< vimeo id="237070377" >}}

### Ethan Horger

The goal here was to try out a blog entry layout that Ethan has always wanted to try, in which the author's bio would always be displayed on the top-left of the article, legal notices at the bottom, and some kind of quote or supplemental material pinned in the middle of the article. With CSS Grid, the layout degrades to using floats in IE 8 and 9, and doesn't maintain the article quote in the middle of the article, but is otherwise fully readable.

<figure><a href="https://codepen.io/wing-zero/pen/MEvaBQ"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d9ea131-a8aa-4947-9f6e-495916b10ec1/44-ethan-horger-opt.png" width="800" height="416" alt="CSS Grid by Ethan Horger" /></a><figcaption><a href="https://codepen.io/wing-zero/pen/MEvaBQ">View on CodePen</a></figcaption></figure>

### Tanya Syrygina

Tanya Syrygina used Grid to built a fresh, card-style blog layout.

<figure><a href="https://codepen.io/TanyaS/pen/OxWwew"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87281af0-ea4e-40ac-80d4-cad4f52d5893/17-tanyia-syryngina-opt.png" width="800" height="462" alt="CSS Grid by Tanya Syrygina" /></a><figcaption><a href="https://codepen.io/TanyaS/pen/OxWwew">View on CodePen</a></figcaption></figure>

### Nelson Leite

For an e-commerce project, Nelson Leite needed to showcase a product listing with some other content in the middle of the products, displayed differently. His solution: CSS Grid.

<figure><a href="https://codepen.io/nelsonleite/full/aygNVv/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b26f50f6-ee9a-4ee0-8395-5b17bad48f92/11-nelson-leite-opt.png" width="800" height="485" alt="CSS Grid by Nelson Leite" /></a><figcaption><a href="https://codepen.io/nelsonleite/full/aygNVv/">View on CodePen</a></figcaption></figure>

### Robert Mion

Robert Mion combined CSS Grid and Flexbox to build a responsive supermarket add.

<figure><a href="https://codepen.io/beginnr/full/brbKWX/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93316a6-46d5-452b-a258-faf8c6ec71c5/03-robert-mion-opt.png" width="800" height="563" alt="CSS Grid by Robert Mion" /></a><figcaption><a href="https://codepen.io/beginnr/full/brbKWX/">View on CodePen</a></figcaption></figure>

### Arturo Ríos

A CSS Grid that can be used comfortably in full-screen mode comes from Arturo Ríos.

<figure><a href="https://codepen.io/arturios/full/Evzzyx/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/027e72f9-4513-46d1-809d-6f7cb67d363c/05-arturo-rios-opt.png" width="800" height="453" alt="CSS Grid by Arturo Ríos" /></a><figcaption><a href="https://codepen.io/arturios/full/Evzzyx/">View on CodePen</a></figcaption></figure>

### Bob Mitro

A simple, responsive blog theme based on CSS Grid layout.

<figure><a href="https://getpublii.com/themes/demo/starter/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f8e0e6-708e-43e6-95e5-f4e048dcc49a/07-bob-mitro-opt.png" width="800" height="567" alt="CSS Grid by Bob Mitro" /></a><figcaption><a href="https://getpublii.com/themes/demo/starter/">View demo</a></figcaption></figure>

### Kev Bonett

Kev Bonnet created a mobile-first e-commerce template with fallback to Flexbox, then fallback to basic 2-column inline-block.

<figure><a href="https://codepen.io/basherkev/pen/PjKQKM"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69e19d15-2c3d-4a6d-83f4-1e3e4b6aa113/08-kev-bonnet-opt.png" width="800" height="475" alt="CSS Grid by Kev Bonett" /></a><figcaption><a href="https://codepen.io/basherkev/pen/PjKQKM">View on CodePen</a></figcaption></figure>

### Sven Rothe

Sven Rothe’s grid has equal heights over several rows. So if you add more content in a tile in the first row, the second row will increase, too.

<figure><a href="https://codepen.io/w3work/pen/PKvNKa"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1632db5-b43e-4d89-b4dd-c280266214ff/09-sven-rothe-opt.png" width="800" height="355" alt="CSS Grid by Sven Rothe" /></a><figcaption><a href="https://codepen.io/w3work/pen/PKvNKa">View on CodePen</a></figcaption></figure>

### Ismail Ghallou

With his To-Do app layout, Ismail Ghallou proves that CSS Grid can handle even the weirdest layouts. And it’s responsive, too.

<figure><a href="https://codepen.io/Smakosh/pen/BwQBpW"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f7565d7-c5a9-4cf9-b403-ac2fa5715476/13-ismail-ghallou-opt.png" width="800" height="475" alt="CSS Grid by Ismail Ghallou" /></a><figcaption><a href="https://codepen.io/Smakosh/pen/BwQBpW">View on CodePen</a></figcaption></figure>

### Juan Garcia

A page of a video game platform comes from Juan Garcia.

<figure><a href="https://codepen.io/-J0hn-/full/xLvKLx"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2681dc75-294d-4db3-8c93-3aeb45f20d17/16-juan-garcia-opt.png" width="800" height="524" alt="CSS Grid by Juan Garcia" /></a><figcaption><a href="https://codepen.io/-J0hn-/full/xLvKLx">View on CodePen</a></figcaption></figure>

### Mark McMurray

A multi-column layout as a CV requires it is a perfect CSS Grid project as Mark McMurray proves.

<figure><a href="https://codepen.io/requestingmark/full/eGWprx/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3d7cc82-85b5-4993-9cf4-e1ff33aa7f7f/19-mark-mc-murray-opt.png" width="800" height="501" alt="CSS Grid by Mark McMurray" /></a><figcaption><a href="https://codepen.io/requestingmark/full/eGWprx/">View on CodePen</a></figcaption></figure>

### Marissa Douglass

Ever thought of building an interactive cookbook with CSS Grid? Marissa Douglass did.

<figure><a href="https://codepen.io/mdouglass/pen/aLwKKL"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1708c4e-dd4c-432c-9ab0-d346dbdfa89d/29-marissa-douglass-opt.png" width="800" height="439" alt="CSS Grid by Marissa Douglass" /></a><figcaption><a href="https://codepen.io/mdouglass/pen/aLwKKL">View on CodePen</a></figcaption></figure>

### Melissa Bogemanns

A photo showcase made with CSS Grid. Available as [.zip](https://www.dropbox.com/s/qftfb4cvyvcdcwc/css_grid_layout.zip?dl=0) (6MB)

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cc3784b-8562-4d39-a407-d8deef1f235b/22-melissa-bogemanns-opt.png" width="800" height="486" alt="CSS Grid by Melissa Bogemanns" /><figcaption></figcaption></figure>

### Tyler Argo

Tyler Argo re-built the Google Play Store layout from scratch using CSS Grid with fallbacks. It works all the way back to IE9 and is even more responsive than the original site.

<figure><a href="https://codepen.io/argo49/pen/jGbXBp?editors=1100"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6da96dc7-f331-4a58-be4b-e80693bc2fae/32-tyler-argo-opt.png" width="800" height="430" alt="CSS Grid by Tyler Argo" /></a><figcaption><a href="https://codepen.io/argo49/pen/jGbXBp?editors=1100">View on CodePen</a></figcaption></figure>

### Mauricio Mantilla

This layout is based on a [website](https://cerosetenta.uniandes.edu.co/) that was designed by the company where Mauricio works at. He took part of the layout, which is based on Packery (Masonry) and port it to grid with just a few lines of CSS Grid.

<figure><a href="https://codepen.io/Mantish/full/Oxgbbq"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50507a68-b448-4af9-bf28-3f352526965a/34-mauricio-mantilla-opt.png" width="800" height="454" alt="CSS Grid by Mauricio Mantilla" /></a><figcaption><a href="https://codepen.io/Mantish/full/Oxgbbq">View on CodePen</a></figcaption></figure>

### Katherine Kato

A portfolio website layout made with CSS Grid and Flexbox as a fallback.

<figure><a href="https://codepen.io/kathykato/pen/JrJwrY"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c483af7-13cf-4579-bb79-77e5020b5640/31-katherine-kato-opt.png" width="800" height="568" alt="CSS Grid by Katherine Kato" /></a><figcaption><a href="https://codepen.io/kathykato/pen/JrJwrY">View on CodePen</a></figcaption></figure>

### Donny Truong

A minimalistic blog layout comes from Donny Truong.

<figure><a href="https://www.visualgui.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd74545e-dc13-46a9-b76b-57b5eb40e8dd/18-donny-truong-opt.png" width="800" height="510" alt="CSS Grid by Donny Truong" /></a><figcaption><a href="https://www.visualgui.com/">View demo</a></figcaption></figure>

### Anenth Vishnu

A responsive app layout based on Grid.

<figure><a href="https://codepen.io/Anenth/full/wrKmNd/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35f1bc0b-6d56-413c-b9c2-f98418d190b6/12-anenth-vishnu-opt.png" width="800" height="482" alt="CSS Grid by Anenth Vishnu" /></a><figcaption><a href="https://codepen.io/Anenth/full/wrKmNd/">View on CodePen</a></figcaption></figure>

### Amy Carney

A basic layout (with IE fallbacks and web accessibility in mind) that may be useful for getting projects started or migrated.

<figure><a href="https://codepen.io/digilou/pen/wrwJGV"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bdbe597-cca0-49e2-8608-71a39be473c0/45-amy-carney-opt.png" width="800" height="429" alt="CSS Grid by Amy Carney" /></a><figcaption><a href="https://codepen.io/digilou/pen/wrwJGV">View on CodePen</a></figcaption></figure>

### Nurçin Özer

Nurçin Özer submitted a basic blog layout.

<figure><a href="https://codepen.io/nurcin/pen/WZNbbq"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63a91eeb-4772-49f4-b2e4-becb5027ec7f/01-nurcin-oezer-opt.png" width="800" height="534" alt="CSS Grid by Nurçin Özer" /></a><figcaption><a href="https://codepen.io/nurcin/pen/WZNbbq">View on CodePen</a></figcaption></figure>

### Remy Oleszczuk

Inspired by the BBC SPORT landing page.

<figure><a href="https://codepen.io/remyo/full/rGjZML/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b9c573-626b-4cde-a323-e346f5d79889/37-remy-oleszczuk-opt.png" width="800" height="450" alt="CSS Grid by Remy Oleszczuk" /></a><figcaption><a href="https://codepen.io/remyo/full/rGjZML/">View on CodePen</a></figcaption></figure>

### Patryk Kalwas

<figure><a href="https://codepen.io/kalwas/pen/VMbNxz"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bce5cae7-6ffa-4d52-bce3-be1fa037a383/23-patryk-kalwas-1-opt.png" width="800" height="487" alt="CSS Grid by Patryk Kalwas" /></a><figcaption><a href="https://codepen.io/kalwas/pen/VMbNxz">View on CodePen</a></figcaption></figure>

### Jesús Olazagoitia

<figure><a href="https://codepen.io/goiblas/pen/pWwRLa"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f3aab85-f1b1-410e-927f-ff19c0b8ad34/26-jesus-olazagoitia-opt.png" width="800" height="414" alt="CSS Grid by Jesús Olazagoitia" /></a><figcaption><a href="https://codepen.io/goiblas/pen/pWwRLa">View on CodePen</a></figcaption></figure>

### Dóra Pölöskei

<figure><a href="https://codepen.io/dododesign/pen/xXrJme"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2abb03a5-5a78-4681-aa3e-db1a50b7a2e6/35-dora-poloskei-opt.png" width="800" height="415" alt="CSS Grid by Dóra Pölöskei" /></a><figcaption><a href="https://codepen.io/dododesign/pen/xXrJme">View on CodePen</a></figcaption></figure>

### Vivek Singh

<figure><a href="https://codepen.io/viiv3k/pen/eGEOqR"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d328653-d876-4b73-95ca-66b9989b032e/39-vivek-singh-opt.png" width="800" height="402" alt="CSS Grid by Vivek Singh" /></a><figcaption><a href="https://codepen.io/viiv3k/pen/eGEOqR">View on CodePen</a></figcaption></figure>

### Pranjal Nadhani

<figure><a href="https://codepen.io/pranjalnadhaniUC/pen/MEpGMj"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7222abc2-6f7b-42a1-93b0-5626cb366ea6/40-pranjal-nadhani-opt.png" width="800" height="486" alt="CSS Grid by Pranjal Nadhani" /></a><figcaption><a href="https://codepen.io/pranjalnadhaniUC/pen/MEpGMj">View on CodePen</a></figcaption></figure>

### Mathias Herrebaut

<figure><a href="https://codepen.io/m_herrebaut/pen/pWdErd"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d687116-f570-4359-b429-c4e741b2cfe6/46-mathias-herrebaut-opt.png" width="800" height="592" alt="CSS Grid by Mathias Herrebaut" /></a><figcaption><a href="https://codepen.io/m_herrebaut/pen/pWdErd">View on CodePen</a></figcaption></figure>

### Noel Tekiri

<figure><a href="https://sicontis.tk/301-days/projects/css-grid-01/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ef6689f-916e-4729-9dce-758d23cac5be/42-noel-tekiri-opt.png" width="800" height="512" alt="CSS Grid by Noel Tekiri" /></a><figcaption><a href="https://sicontis.tk/301-days/projects/css-grid-01/">View in action</a></figcaption></figure>

### Aurélie Deschacht

<figure><a href="https://www.dropbox.com/s/aiixb5gk9su4gbo/CSS%20GRID.zip?dl=0"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dd96f1c-475a-4fe6-bc10-70a52c5ecea7/41-aurelie-deschat-opt.png" width="800" height="535" alt="CSS Grid by Aurélie Deschacht" /></a><figcaption><a href="https://www.dropbox.com/s/aiixb5gk9su4gbo/CSS%20GRID.zip?dl=0">Download project ZIP file</a></figcaption></figure>

### Jonathan Harrell

<figure><a href="https://jonathan-harrell.com/experiment/contextual-callouts-with-css-grid/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1778a88f-f9c8-49d9-a00e-cb103f079009/43-jonathan-harrell-opt.png" width="800" height="485" alt="CSS Grid by Jonathan Harrell" /></a><figcaption><a href="https://jonathan-harrell.com/experiment/contextual-callouts-with-css-grid/">View in action</a></figcaption></figure>

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Name</th>
<th>Submission</th>
</tr>
</thead>
<tbody>
<tr>
<td>Amy DeVoogd</td>
<td><a href="https://amydevoogd.github.io/product-showcase/">Preview template</a></td>
</tr>
<tr>
<td>Anenth</td>
<td><a href="https://codepen.io/Anenth/full/wrKmNd/">Preview template</a></td>
</tr>
<tr>
<td>Tyler Argo</td>
<td><a href="https://codepen.io/argo49/pen/jGbXBp?editors=1100">Preview template</a></td>
</tr>
<tr>
<td>Arturo Ríos</td>
<td><a href="https://codepen.io/arturios/full/Evzzyx/">Preview template</a></td>
</tr>
<tr>
<td>Aurélie Deschacht</td>
<td><a href="https://www.dropbox.com/s/aiixb5gk9su4gbo/CSS%20GRID.zip?dl=0">Download template</a></td>
</tr>
<tr>
<td>Kev Bonett</td>
<td><a href="https://codepen.io/basherkev/pen/PjKQKM">Preview template</a></td>
</tr>
<tr>
<td>Bob Mitro</td>
<td><a href="https://getpublii.com/themes/demo/starter/">Preview template</a></td>
</tr>
<tr>
<td>Amy Carney</td>
<td><a href="https://codepen.io/digilou/pen/wrwJGV">Preview template</a></td>
</tr>
<tr>
<td>Dannie Vinther</td>
<td><a href="https://codepen.io/dannievinther/pen/EvVggR">Preview template</a></td>
</tr>
<tr>
<td>Donny Truong</td>
<td><a href="https://www.visualgui.com/">Preview template</a></td>
</tr>
<tr>
<td>Dóra Pölöskei</td>
<td><a href="https://codepen.io/dododesign/pen/xXrJme">Preview template</a></td>
</tr>
<tr>
<td>Erik Davidsson</td>
<td><a href="https://erikdson.github.io/smashing-grid-challenge/">Preview template</a></td>
</tr>
<tr>
<td>Ethan Horger</td>
<td><a href="https://codepen.io/wing-zero/pen/MEvaBQ">Preview template</a></td>
</tr>
<tr>
<td>Jonathan Harrell</td>
<td><a href="https://jonathan-harrell.com/experiment/contextual-callouts-with-css-grid/">Preview template</a></td>
</tr>
<tr>
<td>Ieva Ozolīte</td>
<td><a href="https://codepen.io/IevaOzolite/pen/xdaVJq">Preview template</a></td>
</tr>
<tr>
<td>Ismail Ghallou</td>
<td><a href="https://codepen.io/Smakosh/pen/BwQBpW">Preview template</a></td>
</tr>
<tr>
<td>Jesús Olazagoitia</td>
<td><a href="https://codepen.io/goiblas/pen/pWwRLa">Preview template</a></td>
</tr>
<tr>
<td>Juan Garcia</td>
<td><a href="https://codepen.io/-J0hn-/full/xLvKLx">Preview template</a></td>
</tr>
<tr>
<td>Katherine Kato</td>
<td><a href="https://codepen.io/kathykato/pen/JrJwrY">Preview template</a></td>
</tr>
<tr>
<td>Marissa Douglass</td>
<td><a href="https://codepen.io/mdouglass/pen/aLwKKL">Preview template</a></td>
</tr>
<tr>
<td>Mathias Herrebaut</td>
<td><a href="https://codepen.io/digilou/pen/wrwJGV">Preview template</a></td>
</tr>
<tr>
<td>Mauricio Mantilla</td>
<td><a href="https://codepen.io/Mantish/full/Oxgbbq">Preview template</a></td>
</tr>
<tr>
<td>Melissa Bogemanns</td>
<td><a href="https://www.dropbox.com/s/qftfb4cvyvcdcwc/css_grid_layout.zip?dl=0">Download template</a></td>
</tr>
<tr>
<td>Robert Mion</td>
<td><a href="https://codepen.io/beginnr/full/brbKWX/">Preview template</a></td>
</tr>
<tr>
<td>Nelson Leite</td>
<td><a href="https://codepen.io/nelsonleite/full/aygNVv/">Preview template</a></td>
</tr>
<tr>
<td>Patryk Kalwas</td>
<td><a href="https://codepen.io/kalwas/pen/VMbNxz">Preview template</a></td>
</tr>
<tr>
<td>Pranjal Nadhani</td>
<td><a href="https://codepen.io/pranjalnadhaniUC/pen/MEpGMj">Preview template</a></td>
</tr>
<tr>
<td>Mathieu</td>
<td><a href="https://pulsardev.github.io/mendelable/">Preview template</a></td>
</tr>
<tr>
<td>Nurçin Özer</td>
<td><a href="https://codepen.io/nurcin/pen/WZNbbq">Preview template</a></td>
</tr>
<tr>
<td>Remy Oleszczuk</td>
<td><a href="https://codepen.io/remyo/full/rGjZML/">Preview template</a></td>
</tr>
<tr>
<td>Ren Aysha</td>
<td><a href="https://codepen.io/rrenula/pen/LzLXYJ">Preview template</a></td>
</tr>
<tr>
<td>Mark McMurray</td>
<td><a href="https://codepen.io/requestingmark/full/eGWprx/">Preview template</a></td>
</tr>
<tr>
<td>Sven Rothe</td>
<td><a href="https://codepen.io/w3work/pen/PKvNKa">Preview template</a></td>
</tr>
<tr>
<td>Sam Beckham</td>
<td><a href="https://codepen.io/samdbeckham/pen/Naxxgy?editors=1100">Preview template</a></td>
</tr>
<tr>
<td>Charles Sejikco</td>
<td><a href="https://github.com/Sejikco/CssGridSheetMusic">Preview template</a></td>
</tr>
<tr>
<td>Tanya Syrygina</td>
<td><a href="https://codepen.io/TanyaS/pen/OxWwew">Preview template</a></td>
</tr>
<tr>
<td>Noel Tekiri</td>
<td><a href="https://sicontis.tk/301-days/projects/css-grid-01/">Preview template</a></td>
</tr>
<tr>
<td>Trang Nguyen</td>
<td><a href="https://codepen.io/Trangbnguyen/pen/GMNQGN/">Preview template</a></td>
</tr>
<tr>
<td>Vivek Singh</td>
<td><a href="https://codepen.io/viiv3k/pen/eGEOqR">Preview template</a></td>
</tr>
</tbody>
</table>

## Getting Started With CSS Grid

Last but not least, before you dive right into the challenge, here are some helpful resources to kick-start your CSS Grid adventure.</p>

### Resources and References

Ever thought of building an interactive cookbook with CSS Grid? Marissa Douglass did.

<figure><a href="https://codepen.io/mdouglass/pen/aLwKKL"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1708c4e-dd4c-432c-9ab0-d346dbdfa89d/29-marissa-douglass-opt.png" width="800" height="439" alt="CSS Grid by Marissa Douglass" /></a><figcaption><a href="https://codepen.io/mdouglass/pen/aLwKKL">View on CodePen</a></figcaption></figure>

### Melissa Bogemanns

A photo showcase made with CSS Grid. Available as [.zip](https://www.dropbox.com/s/qftfb4cvyvcdcwc/css_grid_layout.zip?dl=0) (6MB)

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cc3784b-8562-4d39-a407-d8deef1f235b/22-melissa-bogemanns-opt.png" width="800" height="486" alt="CSS Grid by Melissa Bogemanns" /><figcaption></figcaption></figure>

### Tyler Argo

Tyler Argo re-built the Google Play Store layout from scratch using CSS Grid with fallbacks. It works all the way back to IE9 and is even more responsive than the original site.

<figure><a href="https://codepen.io/argo49/pen/jGbXBp?editors=1100"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6da96dc7-f331-4a58-be4b-e80693bc2fae/32-tyler-argo-opt.png" width="800" height="430" alt="CSS Grid by Tyler Argo" /></a><figcaption><a href="https://codepen.io/argo49/pen/jGbXBp?editors=1100">View on CodePen</a></figcaption></figure>

### Mauricio Mantilla

This layout is based on a [website](https://cerosetenta.uniandes.edu.co/) that was designed by the company where Mauricio works at. He took part of the layout, which is based on Packery (Masonry) and port it to grid with just a few lines of CSS Grid.

<figure><a href="https://codepen.io/Mantish/full/Oxgbbq"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50507a68-b448-4af9-bf28-3f352526965a/34-mauricio-mantilla-opt.png" width="800" height="454" alt="CSS Grid by Mauricio Mantilla" /></a><figcaption><a href="https://codepen.io/Mantish/full/Oxgbbq">View on CodePen</a></figcaption></figure>

### Katherine Kato

A portfolio website layout made with CSS Grid and Flexbox as a fallback.

<figure><a href="https://codepen.io/kathykato/pen/JrJwrY"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c483af7-13cf-4579-bb79-77e5020b5640/31-katherine-kato-opt.png" width="800" height="568" alt="CSS Grid by Katherine Kato" /></a><figcaption><a href="https://codepen.io/kathykato/pen/JrJwrY">View on CodePen</a></figcaption></figure>

### Donny Truong

A minimalistic blog layout comes from Donny Truong.

<figure><a href="https://www.visualgui.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd74545e-dc13-46a9-b76b-57b5eb40e8dd/18-donny-truong-opt.png" width="800" height="510" alt="CSS Grid by Donny Truong" /></a><figcaption><a href="https://www.visualgui.com/">View demo</a></figcaption></figure>

### Anenth Vishnu

A responsive app layout based on Grid.

<figure><a href="https://codepen.io/Anenth/full/wrKmNd/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35f1bc0b-6d56-413c-b9c2-f98418d190b6/12-anenth-vishnu-opt.png" width="800" height="482" alt="CSS Grid by Anenth Vishnu" /></a><figcaption><a href="https://codepen.io/Anenth/full/wrKmNd/">View on CodePen</a></figcaption></figure>

### Amy Carney

A basic layout (with IE fallbacks and web accessibility in mind) that may be useful for getting projects started or migrated.

<figure><a href="https://codepen.io/digilou/pen/wrwJGV"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bdbe597-cca0-49e2-8608-71a39be473c0/45-amy-carney-opt.png" width="800" height="429" alt="CSS Grid by Amy Carney" /></a><figcaption><a href="https://codepen.io/digilou/pen/wrwJGV">View on CodePen</a></figcaption></figure>

### Nurçin Özer

Nurçin Özer submitted a basic blog layout.

<figure><a href="https://codepen.io/nurcin/pen/WZNbbq"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63a91eeb-4772-49f4-b2e4-becb5027ec7f/01-nurcin-oezer-opt.png" width="800" height="534" alt="CSS Grid by Nurçin Özer" /></a><figcaption><a href="https://codepen.io/nurcin/pen/WZNbbq">View on CodePen</a></figcaption></figure>

### Remy Oleszczuk

Inspired by the BBC SPORT landing page.

<figure><a href="https://codepen.io/remyo/full/rGjZML/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b9c573-626b-4cde-a323-e346f5d79889/37-remy-oleszczuk-opt.png" width="800" height="450" alt="CSS Grid by Remy Oleszczuk" /></a><figcaption><a href="https://codepen.io/remyo/full/rGjZML/">View on CodePen</a></figcaption></figure>

### Patryk Kalwas

<figure><a href="https://codepen.io/kalwas/pen/VMbNxz"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bce5cae7-6ffa-4d52-bce3-be1fa037a383/23-patryk-kalwas-1-opt.png" width="800" height="487" alt="CSS Grid by Patryk Kalwas" /></a><figcaption><a href="https://codepen.io/kalwas/pen/VMbNxz">View on CodePen</a></figcaption></figure>

### Jesús Olazagoitia

<figure><a href="https://codepen.io/goiblas/pen/pWwRLa"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f3aab85-f1b1-410e-927f-ff19c0b8ad34/26-jesus-olazagoitia-opt.png" width="800" height="414" alt="CSS Grid by Jesús Olazagoitia" /></a><figcaption><a href="https://codepen.io/goiblas/pen/pWwRLa">View on CodePen</a></figcaption></figure>

### Dóra Pölöskei

<figure><a href="https://codepen.io/dododesign/pen/xXrJme"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2abb03a5-5a78-4681-aa3e-db1a50b7a2e6/35-dora-poloskei-opt.png" width="800" height="415" alt="CSS Grid by Dóra Pölöskei" /></a><figcaption><a href="https://codepen.io/dododesign/pen/xXrJme">View on CodePen</a></figcaption></figure>

### Vivek Singh

<figure><a href="https://codepen.io/viiv3k/pen/eGEOqR"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d328653-d876-4b73-95ca-66b9989b032e/39-vivek-singh-opt.png" width="800" height="402" alt="CSS Grid by Vivek Singh" /></a><figcaption><a href="https://codepen.io/viiv3k/pen/eGEOqR">View on CodePen</a></figcaption></figure>

### Pranjal Nadhani

<figure><a href="https://codepen.io/pranjalnadhaniUC/pen/MEpGMj"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7222abc2-6f7b-42a1-93b0-5626cb366ea6/40-pranjal-nadhani-opt.png" width="800" height="486" alt="CSS Grid by Pranjal Nadhani" /></a><figcaption><a href="https://codepen.io/pranjalnadhaniUC/pen/MEpGMj">View on CodePen</a></figcaption></figure>

### Mathias Herrebaut

<figure><a href="https://codepen.io/m_herrebaut/pen/pWdErd"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d687116-f570-4359-b429-c4e741b2cfe6/46-mathias-herrebaut-opt.png" width="800" height="592" alt="CSS Grid by Mathias Herrebaut" /></a><figcaption><a href="https://codepen.io/m_herrebaut/pen/pWdErd">View on CodePen</a></figcaption></figure>

### Noel Tekiri

<figure><a href="https://sicontis.tk/301-days/projects/css-grid-01/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ef6689f-916e-4729-9dce-758d23cac5be/42-noel-tekiri-opt.png" width="800" height="512" alt="CSS Grid by Noel Tekiri" /></a><figcaption><a href="https://sicontis.tk/301-days/projects/css-grid-01/">View in action</a></figcaption></figure>

### Aurélie Deschacht

<figure><a href="https://www.dropbox.com/s/aiixb5gk9su4gbo/CSS%20GRID.zip?dl=0"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dd96f1c-475a-4fe6-bc10-70a52c5ecea7/41-aurelie-deschat-opt.png" width="800" height="535" alt="CSS Grid by Aurélie Deschacht" /></a><figcaption><a href="https://www.dropbox.com/s/aiixb5gk9su4gbo/CSS%20GRID.zip?dl=0">Download project ZIP file</a></figcaption></figure>

### Jonathan Harrell

<figure><a href="https://jonathan-harrell.com/experiment/contextual-callouts-with-css-grid/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1778a88f-f9c8-49d9-a00e-cb103f079009/43-jonathan-harrell-opt.png" width="800" height="485" alt="CSS Grid by Jonathan Harrell" /></a><figcaption><a href="https://jonathan-harrell.com/experiment/contextual-callouts-with-css-grid/">View in action</a></figcaption></figure>

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Name</th>
<th>Submission</th>
</tr>
</thead>
<tbody>
<tr>
<td>Amy DeVoogd</td>
<td><a href="https://amydevoogd.github.io/product-showcase/">Preview template</a></td>
</tr>
<tr>
<td>Anenth</td>
<td><a href="https://codepen.io/Anenth/full/wrKmNd/">Preview template</a></td>
</tr>
<tr>
<td>Tyler Argo</td>
<td><a href="https://codepen.io/argo49/pen/jGbXBp?editors=1100">Preview template</a></td>
</tr>
<tr>
<td>Arturo Ríos</td>
<td><a href="https://codepen.io/arturios/full/Evzzyx/">Preview template</a></td>
</tr>
<tr>
<td>Aurélie Deschacht</td>
<td><a href="https://www.dropbox.com/s/aiixb5gk9su4gbo/CSS%20GRID.zip?dl=0">Download template</a></td>
</tr>
<tr>
<td>Kev Bonett</td>
<td><a href="https://codepen.io/basherkev/pen/PjKQKM">Preview template</a></td>
</tr>
<tr>
<td>Bob Mitro</td>
<td><a href="https://getpublii.com/themes/demo/starter/">Preview template</a></td>
</tr>
<tr>
<td>Amy Carney</td>
<td><a href="https://codepen.io/digilou/pen/wrwJGV">Preview template</a></td>
</tr>
<tr>
<td>Dannie Vinther</td>
<td><a href="https://codepen.io/dannievinther/pen/EvVggR">Preview template</a></td>
</tr>
<tr>
<td>Donny Truong</td>
<td><a href="https://www.visualgui.com/">Preview template</a></td>
</tr>
<tr>
<td>Dóra Pölöskei</td>
<td><a href="https://codepen.io/dododesign/pen/xXrJme">Preview template</a></td>
</tr>
<tr>
<td>Erik Davidsson</td>
<td><a href="https://erikdson.github.io/smashing-grid-challenge/">Preview template</a></td>
</tr>
<tr>
<td>Ethan Horger</td>
<td><a href="https://codepen.io/wing-zero/pen/MEvaBQ">Preview template</a></td>
</tr>
<tr>
<td>Jonathan Harrell</td>
<td><a href="https://jonathan-harrell.com/experiment/contextual-callouts-with-css-grid/">Preview template</a></td>
</tr>
<tr>
<td>Ieva Ozolīte</td>
<td><a href="https://codepen.io/IevaOzolite/pen/xdaVJq">Preview template</a></td>
</tr>
<tr>
<td>Ismail Ghallou</td>
<td><a href="https://codepen.io/Smakosh/pen/BwQBpW">Preview template</a></td>
</tr>
<tr>
<td>Jesús Olazagoitia</td>
<td><a href="https://codepen.io/goiblas/pen/pWwRLa">Preview template</a></td>
</tr>
<tr>
<td>Juan Garcia</td>
<td><a href="https://codepen.io/-J0hn-/full/xLvKLx">Preview template</a></td>
</tr>
<tr>
<td>Katherine Kato</td>
<td><a href="https://codepen.io/kathykato/pen/JrJwrY">Preview template</a></td>
</tr>
<tr>
<td>Marissa Douglass</td>
<td><a href="https://codepen.io/mdouglass/pen/aLwKKL">Preview template</a></td>
</tr>
<tr>
<td>Mathias Herrebaut</td>
<td><a href="https://codepen.io/digilou/pen/wrwJGV">Preview template</a></td>
</tr>
<tr>
<td>Mauricio Mantilla</td>
<td><a href="https://codepen.io/Mantish/full/Oxgbbq">Preview template</a></td>
</tr>
<tr>
<td>Melissa Bogemanns</td>
<td><a href="https://www.dropbox.com/s/qftfb4cvyvcdcwc/css_grid_layout.zip?dl=0">Download template</a></td>
</tr>
<tr>
<td>Robert Mion</td>
<td><a href="https://codepen.io/beginnr/full/brbKWX/">Preview template</a></td>
</tr>
<tr>
<td>Nelson Leite</td>
<td><a href="https://codepen.io/nelsonleite/full/aygNVv/">Preview template</a></td>
</tr>
<tr>
<td>Patryk Kalwas</td>
<td><a href="https://codepen.io/kalwas/pen/VMbNxz">Preview template</a></td>
</tr>
<tr>
<td>Pranjal Nadhani</td>
<td><a href="https://codepen.io/pranjalnadhaniUC/pen/MEpGMj">Preview template</a></td>
</tr>
<tr>
<td>Mathieu</td>
<td><a href="https://pulsardev.github.io/mendelable/">Preview template</a></td>
</tr>
<tr>
<td>Nurçin Özer</td>
<td><a href="https://codepen.io/nurcin/pen/WZNbbq">Preview template</a></td>
</tr>
<tr>
<td>Remy Oleszczuk</td>
<td><a href="https://codepen.io/remyo/full/rGjZML/">Preview template</a></td>
</tr>
<tr>
<td>Ren Aysha</td>
<td><a href="https://codepen.io/rrenula/pen/LzLXYJ">Preview template</a></td>
</tr>
<tr>
<td>Mark McMurray</td>
<td><a href="https://codepen.io/requestingmark/full/eGWprx/">Preview template</a></td>
</tr>
<tr>
<td>Sven Rothe</td>
<td><a href="https://codepen.io/w3work/pen/PKvNKa">Preview template</a></td>
</tr>
<tr>
<td>Sam Beckham</td>
<td><a href="https://codepen.io/samdbeckham/pen/Naxxgy?editors=1100">Preview template</a></td>
</tr>
<tr>
<td>Charles Sejikco</td>
<td><a href="https://github.com/Sejikco/CssGridSheetMusic">Preview template</a></td>
</tr>
<tr>
<td>Tanya Syrygina</td>
<td><a href="https://codepen.io/TanyaS/pen/OxWwew">Preview template</a></td>
</tr>
<tr>
<td>Noel Tekiri</td>
<td><a href="https://sicontis.tk/301-days/projects/css-grid-01/">Preview template</a></td>
</tr>
<tr>
<td>Trang Nguyen</td>
<td><a href="https://codepen.io/Trangbnguyen/pen/GMNQGN/">Preview template</a></td>
</tr>
<tr>
<td>Vivek Singh</td>
<td><a href="https://codepen.io/viiv3k/pen/eGEOqR">Preview template</a></td>
</tr>
</tbody>
</table>

## Getting Started With CSS Grid

Last but not least, before you dive right into the challenge, here are some helpful resources to kick-start your CSS Grid adventure.</p>

### Resources and References

*   [Grid Garden](https://cssgridgarden.com/): A game for learning CSS Grid
*   [GridBugs](https://github.com/rachelandrew/gridbugs): A community-curated list of bugs, incomplete implementations and interop issues
*   [Awesome CSS Grid](https://github.com/valentinogagliardi/awesome-css-grid): A manually curated list of CSS resources
*   [Grid by Example](https://gridbyexample.com/): Examples, videos and other information to help you learn CSS Grid Layout
*   [Rachel Andrew's Grid Guide](https://www.smashingmagazine.com/2016/11/css-grids-flexbox-box-alignment-new-layout-standard/): the complete guide to Box Alignment, Flexbox, and Grid
*   [CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout): Examples, references and guides by the Mozilla team
*   [Chrome CSS Grid Highlighter](https://github.com/ademilter/chrome-css-grid-highlighter): a little Chrome extension that highlights CSS grids.</p>

### Demos

*   [Jen Simmons’ CSS Grid Demos](https://labs.jensimmons.com/): Demos and examples of how Grid works
*   [CSS Grid Layout on CodePen](https://codepen.io/collection/XRRJGq/): A collection of layouts built with CSS Grid

### Tutorials

*   [Building Production-Ready CSS Grid Layouts Today](https://www.smashingmagazine.com/2017/06/building-production-ready-css-grid-layout/) by Morten Rand-Hendriksen
*   [Progressively Enhancing CSS Layout](https://www.smashingmagazine.com/2017/07/enhancing-css-layout-floats-flexbox-grid/) by Manuel Matuzović
*   [Getting Started With CSS Grid](https://hackernoon.com/getting-started-with-css-grid-layout-8e00de547daf) by Chris Brandrick

### Talks

{{< vimeo id="212961112" >}}

<figure class="fwi"><div style="position:relative;height:0;padding-bottom:56.25%"><iframe loading="lazy" src="https://www.youtube.com/embed/7kVeCqQCxlk?ecver=2" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></figure></figure>

### Inspiration

Finally, to get your ideas flowing, some inspiring CodePen experiments that illustrate the magic of CSS Grid:

<figure><a href="https://codepen.io/hbuchel/pen/qOxGzW"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68b53db1-b92c-4f98-ad1b-f13c29e537c8/01-grid-magazine-opt.png" width="800" height="476" alt="Responsive Magazine Layout" /></a><figcaption><a href="https://codepen.io/hbuchel/pen/qOxGzW">Responsive Magazine Layout</a> by Heather Buchel</figcaption></figure>

<figure><a href="https://codepen.io/nategreen/pen/GpRLXY"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039bc7fb-2b90-45aa-bb58-adf263bdac24/02-grid-minimalistic-opt.png" width="800" height="460" alt="Minimalistic CSS Grid Layout" /></a><figcaption><a href="https://codepen.io/nategreen/pen/GpRLXY">Minimalistic CSS Grid Layout</a> by Nate Green</figcaption></figure>

<figure><a href="https://codepen.io/tutsplus/pen/pNgZpj"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4163e9b5-d6b5-4170-91e1-ab33e91a7587/04-grid-comic-opt.png" width="800" height="478" alt="CSS Grid Layout and Comics" /></a><figcaption><a href="https://codepen.io/tutsplus/pen/pNgZpj">CSS Grid Layout and Comics</a> by Envato Tuts+</figcaption></figure>

<figure><a href="https://codepen.io/Kseso/pen/xqNdmO"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aa8d053-c9b7-4189-b844-5b7d037bdfbe/05-grid-hexagonal-opt.png" width="800" height="439" alt="Auto Hexagonal CSS Grid Layout" /></a><figcaption><a href="https://codepen.io/Kseso/pen/xqNdmO">Auto Hexagonal CSS Grid Layout</a> by Kseso</figcaption></figure>

<figure><a href="https://codepen.io/primalivet/pen/ryjKmV"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/560d422e-118b-4c86-adad-b7cecdc483c0/06-grid-fallback-opt.png" width="800" height="469" alt="CSS Grid Layout with @support Flexbox Fallback" /></a><figcaption><a href="https://codepen.io/primalivet/pen/ryjKmV">CSS Grid Layout with @support Flexbox Fallback</a> by Gustaf Holm</figcaption></figure>

<figure><a href="https://codepen.io/g12n/pen/PPpGvL"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df3ba450-a9a3-49be-a224-03be84e3de8c/09-grid-image-areas-opt.png" width="800" height="453" alt="Image Areas in CSS Grid Layout" /></a><figcaption><a href="https://codepen.io/g12n/pen/PPpGvL">Image Areas in CSS Grid Layout</a> by Michael Gehrmann</figcaption></figure>

<figure><a href="https://codepen.io/jensimmons/pen/aNjXLz"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34fb87db-ec24-471a-9042-1e353ce7df7b/10-grid-mondrian-opt.png" width="800" height="459" alt="Mondrian Art in CSS Grid" /></a><figcaption><a href="https://codepen.io/jensimmons/pen/aNjXLz">Mondrian Art in CSS Grid</a> by Jen Simmons</figcaption></figure>

<figure><a href="https://tympanus.net/Development/GridLayoutSlideshow/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c53ee1b-165b-450d-9101-e0a2f735158b/tympanus-opt-v2.jpg" width="800" height="476" alt="CSS Grid Layout Slideshow" /></a><figcaption><a href="https://tympanus.net/Development/GridLayoutSlideshow/">CSS Grid Layout Slideshow</a> by Manoela Ilic</figcaption></figure>

## Are You Ready For The Next Challenge?

That's right! There will be more challenges coming up very soon, and even more prizes to win! Keep an eye on the magazine or [follow us on Twitter](https://twitter.com/smashingmag) so you don't miss out next time.

{{< signature "ms, vf, il" >}}

