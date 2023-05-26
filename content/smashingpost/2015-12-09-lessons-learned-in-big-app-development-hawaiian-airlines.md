---
title: 'Lessons Learned In Big App Development, A Hawaiian Airlines Case Study'
slug: lessons-learned-in-big-app-development-hawaiian-airlines
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d8325b-40e1-4e5f-bd67-6cc19b05d980/angular-performance-panel-500px-opt.jpg
date: 2015-12-09T02:16:32.000Z
author: coryshaw
description: >-
  Having spent over two years making it, we just pressed the “Ship” button on
  the new [Hawaiian Airlines website](https://www.hawaiianairlines.com/). It has
  been the **biggest project of my career**, and I’ve worked with the most
  talented team I’ve ever worked with.

  Everything was rebuilt from the ground up: hardware, features, back-end APIs,
  front end, and UX and design. It was a **rollercoaster ride like no other**,
  but we have prevailed and built what I believe to be one of the best
  airline-booking experiences on the web. Yes, humble, I know!
categories:
  - Coding
  - JavaScript
  - UX
  - Case Studies
---
Having spent over two years making it, we just pressed the “Ship” button on the new <a href="https://www.hawaiianairlines.com/">Hawaiian Airlines website</a>. It has been the <strong>biggest project of my career</strong>, and I’ve worked with the most talented team I’ve ever worked with. Everything was rebuilt from the ground up: hardware, features, back-end APIs, front end, and UX and design. It was a <strong>rollercoaster ride like no other</strong>, but we have prevailed and built what I believe to be one of the best airline-booking experiences on the web. Yes, humble, I know!

Join me while I reflect on some of the <strong>mistakes we made</strong>, the tools we used, the workflows and guidelines we followed, and even some of the custom tools we built, all while growing a UI development team from one (yours truly) to over ten people to get the job done.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2016/02/transforming-lufthansa-brand-style-guides-implementation-strategy/#further-reading-on-smashingmag)

*   [The State Of Airline Websites 2015: Lessons Learned](https://www.smashingmagazine.com/2015/11/airline-websites-2015-front-end-performance-ux-lessons-learned/)
*   [How To Design Style Guides For Brands And Websites](https://www.smashingmagazine.com/2010/07/designing-style-guidelines-for-brands-and-websites/)
*   [How To Make An Effective Style Guide](https://www.smashingmagazine.com/2014/02/effective-style-guides-with-adobe-fireworks/)
*   [Transforming Lufthansa’s Brand Strategy: A Case Study](https://www.smashingmagazine.com/2016/02/transforming-lufthansa-brand-style-guides-implementation-strategy/)

<strong>Full disclosure:</strong> Our company, <em>User Kind</em>, is a vendor for Hawaiian Airlines, and all opinions expressed here are my own. This article and the information herein has been shared with the explicit permission and generosity of Hawaiian Airlines.

{{% feature-panel %}}

## Humble Beginnings

When I came aboard this project as a UI developer, Hawaiian Airlines had already hired another <a href="https://www.nurun.com">agency</a> to rethink the UX and design of the existing 10-year-old website. That agency delivered a <strong>500+ pages wireframe document</strong>, a handful of beautiful annotated Photoshop mockups and a front-end style guide. Seeing these deliverables immediately got me excited about the project and some of the fun UI development challenges that lay ahead.</p>

### Flight Hop

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12565481-2722-4135-8be4-21da8522dae9/flighthop-898px-opt.jpg"><img title="Flight Hop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16eedcf3-7eaa-4bd9-9c85-f46e024db0b8/flighthop-500px-opt.jpg" alt="Flight Hop" /></a><figcaption>The “hops” between stops are dynamic and represent the duration of that flight relative to the total flight time. Seemed like a fun thing to build using SVG or canvas. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12565481-2722-4135-8be4-21da8522dae9/flighthop-898px-opt.jpg">View large version</a>)</figcaption></figure>

### Travel Goals

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e63c248-f290-4d3d-b86e-2cab8c69a8f4/travel-goals-898px-opt.jpg"><img title="Travel Goals" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b61ee48-de43-4823-b78b-c3a06e0c8ad8/travel-goals-500px-opt.jpg" alt="Travel Goals" /></a><figcaption>When I saw this, I envisioned the orange progress bar and plane icon animating across the screen, while the “miles to go” number counted down. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e63c248-f290-4d3d-b86e-2cab8c69a8f4/travel-goals-898px-opt.jpg">View large version</a>)</figcaption></figure>

### Price Chart

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c85cf43-d309-47be-9e15-c9db5a8ebe92/price-chart-989px-opt.jpg"><img title="Price Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1897b3a3-fad0-4469-ac6d-5e195019a196/price-chart-500px-opt.jpg" alt="Price Chart" /></a><figcaption>The price chart calculates a relative height for each day, based on the data at hand, fast-forwarding through months while making AJAX calls, and readjusting bar heights based on new data. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c85cf43-d309-47be-9e15-c9db5a8ebe92/price-chart-989px-opt.jpg">View large version</a>)</figcaption></figure>

## The Front-End Sandbox

Around the time I was getting started, a large back-end team of 40 or so developers were ramping up on rebuilding all of their service APIs. Knowing that there was a tsunami of UI work to do, no back-end APIs for the front end to consume yet, and a hard deadline staked in the ground, we got to work.

Because the back-end stack was still being defined and built behind a private network, we started with a <strong>lightweight front-end sandbox</strong> to begin building UI components.

Here’s what the stack of tools and workflow looked like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e4e0d0d-08fe-4bfd-bf9e-4b809449a6ed/sandbox-stack-2320px-opt.png"><img title="Sandbox Dev Stack" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fcf4225-3289-4451-b180-25ca6dca3f86/sandbox-stack-500px-opt.jpg" alt="Sandbox Dev Stack" /></a><figcaption>Stack of tools and workflow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e4e0d0d-08fe-4bfd-bf9e-4b809449a6ed/sandbox-stack-2320px-opt.png">View large version</a>)</figcaption></figure>

### Dynamic Templates Fed by Static Data

While working in the sandbox environment, we used AngularJS to create dynamic templates based on a static JSON, which would eventually be replaced with live endpoints once we delivered the code. Sometimes the back-end folks would send us a JSON file generated from real flight data, and other times we would just define it ourselves if the data didn’t exist yet.

Using static JSON data worked OK for a while, but once we started building some of the more complex UI components, we quickly ran into a problem: <strong>multiple data states</strong>.

Take flight results, for example. You have one-way, round-trip and multi-city flight results, each with up to four layovers, overnight flights and multiple airlines. You can even travel back in time if you fly across the right time zones at the right time!

Given the thousand-line JSON files, hand-tweaking the JSON to test other states was a chore and prone to human error.

We needed a better way to build and test all of these different states in the sandbox. So, Nathan set out to solve this problem and came up with what we call the “data inspector”:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbb8375-77e6-4bd4-af29-703c3e534c99/data-inspector-2836px-opt.png"><img title="Data Inspector" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af47cc14-4076-4ef9-8a65-02fbc341ab50/data-inspector-500px-opt.jpg" alt="Data Inspector" /></a><figcaption>We used the data inspector to simulate live data in the static sandbox environment. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbb8375-77e6-4bd4-af29-703c3e534c99/data-inspector-2836px-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85513399-ae2d-4d93-be91-f08166af45a7/data-inspector-stack-2366px-opt.png"><img title="Data Inspector Stack" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db6c4293-adfc-4d29-91c2-9cd13e5fa59e/data-inspector-stack-500px-opt.jpg" alt="Data Inspector Stack" /></a><figcaption>The data inspector used PouchDB to handle localStorage, which also allowed us to sync up to a lightweight CouchDB server so that we could share data states between team members. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85513399-ae2d-4d93-be91-f08166af45a7/data-inspector-stack-2366px-opt.png">View large version</a>)</figcaption></figure>

Armed with the data inspector, we were able to prepare the front-end code so that it was production-ready when we delivered it to be hooked up to live data. As a bonus, designers and product owners could use this tool on the demo Heroku website to ensure that everything looked as intended across states.</p>

### Tossing Code Over the Fence

Spoiler alert: <strong>Don’t ever do this!</strong>

When it came time to integrate the front-end code with back-end services, we had to toss it over the fence to the folks who were integrating it in a totally different environment (.NET) with completely different tools (Visual Studio and Team Foundation Server), tucked securely behind a private network in Hawaii.

While this worked OK initially, it quickly became a nightmare. Product folks would request changes to the UI; we would make those changes in the sandbox, then toss it back over. Code changes would then have to be <strong>hand-merged</strong> because we had Git on one side and Team Foundation Server on the other. With different file and folder structures, these two repositories didn’t play nice together.

We quickly put an end to this and worked with the IT team to get access into the walled paradise. However, this process set us back <strong>months</strong> of productivity, as we switched to a completely different development stack, got VPN access, learned a different toolset and set up our virtual machines to match what the back-end team was using.

From then on, we’ve worked directly with the back-end teams to build and integrate the UI code, using the scrum process in two-week sprints, and things have gone a lot smoother since.

In the short term, the sandbox gave us a huge head start. We got to use a bunch of modern tools and workflows that we were all familiar with. It made us really efficient. Given the circumstances, it might have been the right move, but we waited way too long to rip off the bandage and hop over the fence once it was ready.</p>

### Sandbox Learnings

*   If you’re using Git, choose a branching model carefully on day one, and ensure that it fits your team, project and workflow.
*   If your Git branching strategy is done right, then reverting or cherry-picking features over the timeline of your project should be a cheap and easy task.
*   If building the front end of an app with real data and endpoints isn’t possible, then figure out a way to make it possible. (Mocked-up endpoints would have been better.)
*   Avoid multiple teams working across multiple environments at all costs, even if it causes delays up front.
*   Establish your tools, workflows and environment early on, and ensure that everyone on the team uses them.
*   Had we taken a more forward-thinking approach, it would have given us a big leg up in the long run, and we would’ve avoided the mid-project slump altogether.</p>

## CSS And LESS

In the beginning of this project, we adopted the <a href="https://ianstormtaylor.com/oocss-plus-sass-is-the-best-way-to-css/">methodology</a> that keeping the HTML light, with very few CSS classes, while using LESS’ <code>:extend</code> heavily was the way to go.

It’s nice because when your design changes in the future, your HTML won’t be full of a lot of CSS classes, and you shouldn’t have to touch it. Simply update your LESS styles, and change your <code>:extend</code>s.

Most elements in the HTML had either no class or a single defining class:

<pre><code class="language-markup">&lt;section class="my-section"&gt;
   &lt;h1&gt;Title&lt;/h1&gt;
   &lt;p&gt;Some Text&lt;/p&gt;
&lt;/section&gt;
</code></pre>

Then, in our LESS, we’d have styles like this:

<pre><code class="language-css">.my-section {
   h1:extend(.header-uppercase-1){};
   p:extend(.bodycopy-sans-3){};
}
</code></pre>

The net result of this method is a <em>lot</em> of selectors in the CSS output. After a year of coding, our CSS output got unwieldy, with thousands of lines of this:

<pre><code class="language-css">.ha-modal .help-template h2,
.ha-modal .help-template h3,
.ha-modal .help-template h3:first-child,
.ha-help.collapsable-block h4,
.tooltip-block h4,
.traveler-lg .name,
address h4,
.ha-cms-teaser-sidebar .heading,
[ha-calendar] .ha-calendar-month,
.ha-modal#locationModal .destinations-container .standard-location .heading,
[ha-alert] .alert .alert-content .alert-content-primary,
[ha-avatar] .avatar .name,
[ha-avatar] .avatar.small .name,
[ha-tooltip] .ha-tooltip h4,
[ha-global-alert] .global-alert .alert-content .alert-content-primary,
[ha-promo-tile-other-small] .promo-tile.tile-small .headline,
[ha-promo-tile-other-large] .promo-tile .headline,
[ha-child-nav-tile] .child-nav-tile .page-title,
.navtray-content-inner--stackedlistwrap .stackedlist-li-title,
.lte-ie7 .navtray-content-inner--stackedlistwrap .stackedlist-li-title,
.ha-flight-hop .departure-city,
.ha-flight-hop .arrival-city,
.ha-receipt .trip,
.ha-my-trip-itinerary .trip-header span.segment-city,
.ha-my-trip-itinerary .segment .check-in .status,
.ha-my-trip-itinerary .segment .check-in .status:before,
.ha-my-trip-itinerary .segment .check-in .status.green:before,
.ha-my-trip-itinerary .segment .check-in .status.red:before,
.ha-my-trip-itinerary .segment .check-in .status.yellow:before,
.ha-flight-status .flight-info .flight-number,
.ha-flight-status .flight-info .flight-route,
.ha-print-confirmation .reservation-code-title,
.ha-my-trips-itinerary-details .trip-header span.segment-city,
.ha-my-trips-eticket-receipt .trip-header span.segment-city,
.ha-my-trips-itinerary-details .segment .segment-header .col,
.ha-my-trips-eticket-receipt .segment .segment-header .col,
.ha-my-trips-itinerary-details .segment .leg .leg-details .status,
.ha-my-trips-eticket-receipt .segment .leg .leg-details .status,
.ha-my-trips-itinerary-details .segment .leg .leg-details .status:before,
.ha-my-trips-eticket-receipt .segment .leg .leg-details .status:before,
.ha-my-trips-itinerary-details .left-heading .trip-locations,
.ha-my-trips-eticket-receipt .left-heading .trip-locations,
.ha-book-flight-results .segment .selected-flight-info,
.select-class-wrapper a,
.ha-book-flight-results .discount-applied .credit-applied {
  font-style: normal;
  font-size: 0.9375em;
  font-family: "helvetica-neue", "HelveticaNeueLT Std", "HelveticaNeue", "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-weight: bold;
  text-transform: none;
  line-height: 1.4;
  letter-spacing: 0.02em;
}
</code></pre>

Fun fact: Did you know that Internet Explorer 9 and below will stop processing a given CSS file once it reaches 4095 selectors? Heavy use of <code>:extend</code> put us way over that limit early on. Figuring out why the website looked totally messed up in Internet Explorer 8 and 9 took a bit of debugging and research. We ended up using a Gulp task to break up the CSS files for old versions of the browser.

This ended up being really bad. It bloated our CSS with an output that made it difficult to debug styles in the inspector.</p>

### Mixins vs. Extend

When our CSS output started exceeding 100 KB in size, a question arose. What would output a smaller style sheet: more styles (using <code>@mixin</code>) or more selectors (using <code>:extend</code>)?.

I’ll let <a href="https://jakealbaugh.com/">Jake</a> explain:
<blockquote>“After testing it out, we discovered that, despite <code>:extend</code> outputting significantly less CSS, Gzip compression of the redundant mixin styles could actually translate into a similar if not smaller file size. What puts this idea over the top is that transitioning to mixins would make the DOM inspector CSS much more legible. We would no longer have 200 unrelated selectors grayed out for that <code>h1</code> you’re trying to debug (which can make the inspector lag and reduce legibility). We did a small Gzip test comparing a small-scale mixin-ed style sheet versus an <code>:extend</code>-ed style sheet, and the mixin version actually came out on top.”</blockquote>

So, we did a big overhaul to change all <code>:extend</code>s to <code>@mixins</code>. (We covered 80% with a simple script, the rest by hand.)

Thus, this…

<pre><code class="language-css">.my-section {
   h1:extend(.header-uppercase-1){};
   p:extend(.bodycopy-sans-3){};
}</code></pre>

… became this:

<pre><code class="language-css">.my-section {
   h1 {.header-uppercase-1}
   p {.bodycopy-sans-3}
}</code></pre>

This discovery was an improvement, but the bloated CSS could have been avoided altogether if we had adopted an entirely different framework…

### OOCSS and BEM

Looking back on all of this, our CSS would have reduced in size and our development productivity would have increased if we had established a pattern with more defining classes in the markup (<a href="https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/">OOCSS</a> and/or <a href="https://css-tricks.com/bem-101/">BEM</a>).

Here are the pros of OOCSS and BEM:

*   Style sheets are smaller, flatter and easier to maintain.
*   Troubleshooting and development of styles are more efficient:
    *   Source maps can tell you where to find the source LESS code.
    *   Modifying styles in the browser (for experimenting) is easier because they will appear as different syles.
    *   The DOM will tell you what the custom class is versus what the global classes are.
    *   You can more easily break out specific style sheets to serve only what a page or section needs (rather than a lot of classes being downloaded that the page doesn’t refer to).

And here are the cons of OOCSS and BEM:

*   The HTML is more wieldy, with a lot of CSS classes.
*   You’ll have less flexibility to make CSS-only changes down the road.
*   When the design changes, you’ll likely need to modify the HTML classes.

In hindsight, OOCSS and BEM clearly would have been ideal frameworks to approach a project of this size.</p>

### CSS Learnings

*   Agree on a general approach across the team, or adopt an OOCSS-esque approach, like BEM.
*   Use a linter like Jacob Gable’s [LESS Lint Grunt plugin](https://github.com/jgable/grunt-lesslint) to keep your LESS and CSS inline with your patterns.
*   Stay away from using `:extend`s as much as possible on a big project. The way it works is smart, but the output is confusing and difficult to debug.
*   Use classes that are flat and reusable throughout the project, and continually analyze existing classes when creating new ones.</p>

## AngularJS

When I came aboard this project, I had a lot of experience with jQuery, jQuery Mobile and vanilla JavaScript, but I hadn’t touched AngularJS or similar JavaScript frameworks. The <a href="https://stackoverflow.com/questions/14994391/thinking-in-angularjs-if-i-have-a-jquery-background">paradigm shift</a> to AngularJS was a struggle for me at first; but, as many others have experienced, once I got over the learning curve, I fell in love.</p>

### Custom UI Components

What makes AngularJS a great solution for a big project like the Hawaiian Airlines website is the amount of flexibility it gives you to create custom UI components.

All of that flexibility means that there are a lot of ways to skin the AngularJS cat. In the beginning, we skinned it in ways that made our code difficult to test and difficult to reuse in different contexts. We’d have a directive that depended on some parent scope variable, and when that didn’t exist, the directive would break. We learned pretty quickly that if you don’t have an isolate scope in your directive, you’re asking for trouble.

Over the course of the project, we learned to think about AngularJS directives more as self-contained web components with an API.

AngularJS directives should be very self-centered. They shouldn’t know or care about the world they live in, so long as their basic needs are met, as defined by an API in the form of element attributes:

<pre><code class="language-markup">&lt;custom-component-thing
   type="type1"
   data="{object}"
   default-airport-code="HNL"
   excluded-airport-codes="['OGG', 'DEN']"
   show-partner-airlines="true"
   on-departure-airport-select="select(departureAirportCode)"
   on-return-airport-select="select(returnAirportCode)"&gt;
&lt;/custom-component-thing&gt;</code></pre>

In the example above, the data you feed this directive via the attributes tells it how to behave and exposes a way to pull data back out of it, yet completely isolates its inner workings and template that renders to the DOM.</p>

### AngularJS Performance

While AngularJS magically data-binds everything defined on <code>$scope</code> two ways, this magic doesn’t come for free. For every item on <code>$scope</code>, a listener is created that detects changes to it. When changes are detected, it goes through and updates everywhere else it is used. Each time AngularJS loops through all of the items on <code>$scope</code>, we call that a digest cycle. The more stuff you have attached to <code>$scope</code>, the harder it has to work and the slower your digest cycle becomes.

In a big application such as Hawaiian Airline’s flight results, we started <strong>noticing laggy performance on tablets and slow desktop computers</strong>. Upon investigation, we realized that the page had over 5,000 watchers, and the digest cycle was taking several hundred milliseconds!

With a new problem and awareness of AngularJS’ performance, Nathan and <a href="https://github.com/blndspt">Scott</a> set out and built a handy <a href="https://github.com/blndspt/ngPerformance">tool to monitor AngularJS performance</a>, and they open-sourced it.

This tool ended up being key in troubleshooting and taming AngularJS performance across the website. Check it out: You can <a href="https://www.hawaiianairlines.com/?performance=true">see AngularJS performance data on the live website</a> by adding <code>?performance=true</code> to any page’s URL.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7fef10b-838d-4960-9998-1f0185373d5f/angular-performance-panel-1258px-opt.png"><img title="AngularJS Performance Panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d8325b-40e1-4e5f-bd67-6cc19b05d980/angular-performance-panel-500px-opt.jpg" alt="AngularJS Performance Panel" /></a><figcaption>The performance panel gave us valuable insight into the number of watchers and overall performance of a given page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7fef10b-838d-4960-9998-1f0185373d5f/angular-performance-panel-1258px-opt.png">View large version</a>)</figcaption></figure>

In conjunction with the performance tool, we used <a href="https://github.com/Pasvaz/bindonce">AngularJS’ <code>bind-once</code></a> directive to ensure that we have watchers only on data that needed to change.

As a result, we brought our watchers from over 5,000 <strong>down to under 500</strong>, and we saw a nice bump in responsiveness on tablets and slow devices.</p>

### AngularJS Learnings

*   With great power comes great responsibility. Make sure you understand the inner workings of your chosen framework so that you harness it for good and not evil.
*   AngularJS has taught me an entirely different way to think about constructing a UI, such as breaking components down to their bare reusable essence, and avoiding DOM manipulation via jQuery altogether.
*   Think of directives as web components that expose an API into them, and keep your scope isolated from the outside world to avoid bugs and headaches.</p>

## Custom Form Controls

Booking travel online basically consists of a complex set of forms. So, designing beautiful custom form controls seemed obvious, and everyone (me included) was excited about it.

Looking back, if I had to pick the single most painful thing we did on this project, it would be the custom form controls.

You might not realize it, but those form controls that come out of the box in your browser do a lot of heavy lifting:

*   They ensure that people with accessibility challenges can still use them.
*   They keep track of `focus`, `blur`, `active`, `inactive` states.
*   They allow the user to cycle through all fields using the “Tab” key.
*   They figure out how and where to place dropdown menus based on the page’s scroll position.
*   They allow the user to type up to several letters to jump to an item in a dropdown menu.
*   They auto-scroll dropdown menu items for long lists.

When we decided to roll our own form controls, we took on the burden of reinventing the wheel and supporting all of the requirements above.

We ended up with a solution that uses AngularJS to hide the native HTML of select dropdowns, checkboxes and radio buttons, and replaces them with alternate markup for which we had full control over styling.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40cee291-6454-4750-b9f8-6729c9ce461e/custom-form-controls-1498px-opt.png"><img title="Old Form Controls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cb875e-efd0-422e-a519-afbc82445266/custom-form-controls-500px-opt.jpg" alt="Old Form Controls" /></a><figcaption>This is what our custom form controls looked like. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40cee291-6454-4750-b9f8-6729c9ce461e/custom-form-controls-1498px-opt.png">View large version</a>)</figcaption></figure>

While this approach gave us OCD-level control over every pixel, it ended up causing <strong>all kinds of obscure bugs and accessibility issues</strong> in complex situations, which we spent countless hours patching.

In the end, we decided to scrap these custom form controls in favor of their native counterparts. We realized that, while we couldn’t achieve the pixel perfection of a pure custom solution, we could get 99% of the way there just by using background images and pseudo-selectors on the native input HTML. In the case of &lt;select&gt; dropdown menus, we just styled the default look of the select menu and let the browser handle the look and feel of the actual dropdown of the select menu. For checkboxes and radios, we hid the default control off screen and then styled the label via pseudo-selectors.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6587251e-ee13-4fcb-90e0-fca382fede87/new-form-fields-1934px-opt.png"><img title="New Form Controls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eefa4b2-65b3-430c-877d-cfdf6f9f7812/new-form-fields-500px-opt.jpg" alt="New Form Controls" /></a><figcaption>These new form controls use 100% native code and achieve a nearly identical look (minus the native dropdown menu). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6587251e-ee13-4fcb-90e0-fca382fede87/new-form-fields-1934px-opt.png">View large version</a>)</figcaption></figure>

<a href="https://inorganik.net/">Jamie</a> made <a href="https://codepen.io/inorganik/pen/QjqzwG">a Codepen</a> of these new form fields as a proof of concept.</p>

### Custom Form Controls Learnings

*   Rolling your own form controls, especially for dropdown menus, on a project of this size and complexity is not worth the hassle. The only thing you’ll gain is shiny controls.
*   Do what you can with native form code, and avoid replacing it with custom markup.
*   Try using background images, SVGs and pseudo-selectors to achieve the look you want.</p>

## Pattern Consistency

With a code base this big, pattern consistency becomes really important. Big code bases should look as though a single person developed it. In practice, this is easier said than done.

Anytime we developers code something, we can look back almost immediately and realize how we could have done it better. That’s just human nature. There’s always this temptation to change and improve one’s patterns. It’s a healthy but dangerous instinct.

I would argue that pattern consistency across a big code base is more important than doing something different in one place, even if you know the solution is five times better.

Think of it like the user experience of your code. Once you learn one pattern, you would expect it to look and work the same way everywhere else. If it doesn’t, then you’ll get bogged down in a costly spiral of troubleshooting and debugging in order to learn how the foreign pattern works — and you’ll then have to keep track of more than one pattern in your head.

When patterns are all over the map, you end up with steep learning curves and unproductive developers across the team or, even worse, individual developers who hold all of the knowledge of the patterns they’ve worked on.</p>

### UI Docs

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51444432-16ac-4e81-ae47-c94b0c6cc87b/ui-docs-1344px-opt.png"><img title="UI documentation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/067f66fe-8653-4ad6-9410-bfab996e8e63/ui-docs-500px-opt.jpg" alt="UI documentation" /></a><figcaption>The UI documentation provides information about global styles, AngularJS directives and patterns. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51444432-16ac-4e81-ae47-c94b0c6cc87b/ui-docs-1344px-opt.png">View large version</a>)</figcaption></figure>

One of our most valuable assets on the front end that helped us maintain pattern consistency (and, as a bonus, prevented my instant messenger from blowing up with questions all day long) was the <strong>UI documentation</strong> that we built and maintained throughout the project.

We used Yeoman to generate the scaffolding of new AngularJS directives, which in turn generated a demo page for that directive that we could build from. So, most of our documentation was created during the development of the component; it practically built and maintained itself.

We built the documentation directly into the local and development environments, so that anyone working on the project could access and maintain it anytime.</p>

### Code Reviews

This project moved so fast that each person barely had time to get their own work done, let alone pay attention to what their peers were doing. Our <strong>pattern consistency degraded over time</strong> as a result.

To combat this later in the project, we started doing <strong>peer code reviews</strong>. Before merging code into the main repository, a developer would request a review from a handful of peers, and they would not check in or merge their code until at least one team member had reviewed and approved it. At first, this workflow slowed things down a bit, but the result was that our patterns aligned, we caught bugs, and knowledge of the code was better disseminated.</p>

### Guidelines

While <a href="https://jshint.com/">JSHint</a> helps with enforcing some JavaScript standards and the UI documentation helped as a general reference, a higher level of consistency is still missing in the front-end code base. Looking back, it would have been helpful to establish some <a href="https://github.com/airbnb/javascript">detailed guidelines</a> for the JavaScript, HTML and CSS that could be referenced and followed throughout the project, and to enforce as much as possible via Grunt tasks.</p>

### Pattern Consistency Learnings

*   Changing patterns for the better is a good thing, but only if it can be done across the entire code base in one fell swoop and clearly communicated to the team.
*   Code reviews help to align patterns, catch bugs and spread learning.
*   UI documentation is a great reference for everyone involved. The next time around, I would look into creating a [living style guide](https://www.smashingmagazine.com/2015/04/an-in-depth-overview-of-living-style-guide-tools/) — self-generated and self-maintained from the source code, via a tool like [KSS](https://warpspire.com/kss/styleguides/).
*   Document and enforce detailed JavaScript, HTML and CSS style guides, similar to [Airbnb’s for JavaScript](https://github.com/airbnb/javascript), [Google’s for JavaScript](https://github.com/google/styleguide), [GitHub’s for CSS](https://primercss.io/) and [Google’s for CSS and HTML](https://github.com/google/styleguide).
*   Use Grunt or Gulp tools wherever possible to automate the enforcement of patterns.

*   Style sheets are smaller, flatter and easier to maintain.
*   Troubleshooting and development of styles are more efficient:
    *   Source maps can tell you where to find the source LESS code.
    *   Modifying styles in the browser (for experimenting) is easier because they will appear as different syles.
    *   The DOM will tell you what the custom class is versus what the global classes are.
    *   You can more easily break out specific style sheets to serve only what a page or section needs (rather than a lot of classes being downloaded that the page doesn’t refer to).

And here are the cons of OOCSS and BEM:

*   The HTML is more wieldy, with a lot of CSS classes.
*   You’ll have less flexibility to make CSS-only changes down the road.
*   When the design changes, you’ll likely need to modify the HTML classes.

In hindsight, OOCSS and BEM clearly would have been ideal frameworks to approach a project of this size.</p>

### CSS Learnings

*   Agree on a general approach across the team, or adopt an OOCSS-esque approach, like BEM.
*   Use a linter like Jacob Gable’s [LESS Lint Grunt plugin](https://github.com/jgable/grunt-lesslint) to keep your LESS and CSS inline with your patterns.
*   Stay away from using `:extend`s as much as possible on a big project. The way it works is smart, but the output is confusing and difficult to debug.
*   Use classes that are flat and reusable throughout the project, and continually analyze existing classes when creating new ones.</p>

## AngularJS

When I came aboard this project, I had a lot of experience with jQuery, jQuery Mobile and vanilla JavaScript, but I hadn’t touched AngularJS or similar JavaScript frameworks. The <a href="https://stackoverflow.com/questions/14994391/thinking-in-angularjs-if-i-have-a-jquery-background">paradigm shift</a> to AngularJS was a struggle for me at first; but, as many others have experienced, once I got over the learning curve, I fell in love.</p>

### Custom UI Components

What makes AngularJS a great solution for a big project like the Hawaiian Airlines website is the amount of flexibility it gives you to create custom UI components.

All of that flexibility means that there are a lot of ways to skin the AngularJS cat. In the beginning, we skinned it in ways that made our code difficult to test and difficult to reuse in different contexts. We’d have a directive that depended on some parent scope variable, and when that didn’t exist, the directive would break. We learned pretty quickly that if you don’t have an isolate scope in your directive, you’re asking for trouble.

Over the course of the project, we learned to think about AngularJS directives more as self-contained web components with an API.

AngularJS directives should be very self-centered. They shouldn’t know or care about the world they live in, so long as their basic needs are met, as defined by an API in the form of element attributes:

<pre><code class="language-markup">&lt;custom-component-thing
   type="type1"
   data="{object}"
   default-airport-code="HNL"
   excluded-airport-codes="['OGG', 'DEN']"
   show-partner-airlines="true"
   on-departure-airport-select="select(departureAirportCode)"
   on-return-airport-select="select(returnAirportCode)"&gt;
&lt;/custom-component-thing&gt;</code></pre>

In the example above, the data you feed this directive via the attributes tells it how to behave and exposes a way to pull data back out of it, yet completely isolates its inner workings and template that renders to the DOM.</p>

### AngularJS Performance

While AngularJS magically data-binds everything defined on <code>$scope</code> two ways, this magic doesn’t come for free. For every item on <code>$scope</code>, a listener is created that detects changes to it. When changes are detected, it goes through and updates everywhere else it is used. Each time AngularJS loops through all of the items on <code>$scope</code>, we call that a digest cycle. The more stuff you have attached to <code>$scope</code>, the harder it has to work and the slower your digest cycle becomes.

In a big application such as Hawaiian Airline’s flight results, we started <strong>noticing laggy performance on tablets and slow desktop computers</strong>. Upon investigation, we realized that the page had over 5,000 watchers, and the digest cycle was taking several hundred milliseconds!

With a new problem and awareness of AngularJS’ performance, Nathan and <a href="https://github.com/blndspt">Scott</a> set out and built a handy <a href="https://github.com/blndspt/ngPerformance">tool to monitor AngularJS performance</a>, and they open-sourced it.

This tool ended up being key in troubleshooting and taming AngularJS performance across the website. Check it out: You can <a href="https://www.hawaiianairlines.com/?performance=true">see AngularJS performance data on the live website</a> by adding <code>?performance=true</code> to any page’s URL.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7fef10b-838d-4960-9998-1f0185373d5f/angular-performance-panel-1258px-opt.png"><img title="AngularJS Performance Panel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d8325b-40e1-4e5f-bd67-6cc19b05d980/angular-performance-panel-500px-opt.jpg" alt="AngularJS Performance Panel" /></a><figcaption>The performance panel gave us valuable insight into the number of watchers and overall performance of a given page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7fef10b-838d-4960-9998-1f0185373d5f/angular-performance-panel-1258px-opt.png">View large version</a>)</figcaption></figure>

In conjunction with the performance tool, we used <a href="https://github.com/Pasvaz/bindonce">AngularJS’ <code>bind-once</code></a> directive to ensure that we have watchers only on data that needed to change.

As a result, we brought our watchers from over 5,000 <strong>down to under 500</strong>, and we saw a nice bump in responsiveness on tablets and slow devices.</p>

### AngularJS Learnings

*   With great power comes great responsibility. Make sure you understand the inner workings of your chosen framework so that you harness it for good and not evil.
*   AngularJS has taught me an entirely different way to think about constructing a UI, such as breaking components down to their bare reusable essence, and avoiding DOM manipulation via jQuery altogether.
*   Think of directives as web components that expose an API into them, and keep your scope isolated from the outside world to avoid bugs and headaches.</p>

## Custom Form Controls

Booking travel online basically consists of a complex set of forms. So, designing beautiful custom form controls seemed obvious, and everyone (me included) was excited about it.

Looking back, if I had to pick the single most painful thing we did on this project, it would be the custom form controls.

You might not realize it, but those form controls that come out of the box in your browser do a lot of heavy lifting:

*   They ensure that people with accessibility challenges can still use them.
*   They keep track of `focus`, `blur`, `active`, `inactive` states.
*   They allow the user to cycle through all fields using the “Tab” key.
*   They figure out how and where to place dropdown menus based on the page’s scroll position.
*   They allow the user to type up to several letters to jump to an item in a dropdown menu.
*   They auto-scroll dropdown menu items for long lists.

When we decided to roll our own form controls, we took on the burden of reinventing the wheel and supporting all of the requirements above.

We ended up with a solution that uses AngularJS to hide the native HTML of select dropdowns, checkboxes and radio buttons, and replaces them with alternate markup for which we had full control over styling.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40cee291-6454-4750-b9f8-6729c9ce461e/custom-form-controls-1498px-opt.png"><img title="Old Form Controls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cb875e-efd0-422e-a519-afbc82445266/custom-form-controls-500px-opt.jpg" alt="Old Form Controls" /></a><figcaption>This is what our custom form controls looked like. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40cee291-6454-4750-b9f8-6729c9ce461e/custom-form-controls-1498px-opt.png">View large version</a>)</figcaption></figure>

While this approach gave us OCD-level control over every pixel, it ended up causing <strong>all kinds of obscure bugs and accessibility issues</strong> in complex situations, which we spent countless hours patching.

In the end, we decided to scrap these custom form controls in favor of their native counterparts. We realized that, while we couldn’t achieve the pixel perfection of a pure custom solution, we could get 99% of the way there just by using background images and pseudo-selectors on the native input HTML. In the case of &lt;select&gt; dropdown menus, we just styled the default look of the select menu and let the browser handle the look and feel of the actual dropdown of the select menu. For checkboxes and radios, we hid the default control off screen and then styled the label via pseudo-selectors.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6587251e-ee13-4fcb-90e0-fca382fede87/new-form-fields-1934px-opt.png"><img title="New Form Controls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eefa4b2-65b3-430c-877d-cfdf6f9f7812/new-form-fields-500px-opt.jpg" alt="New Form Controls" /></a><figcaption>These new form controls use 100% native code and achieve a nearly identical look (minus the native dropdown menu). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6587251e-ee13-4fcb-90e0-fca382fede87/new-form-fields-1934px-opt.png">View large version</a>)</figcaption></figure>

<a href="https://inorganik.net/">Jamie</a> made <a href="https://codepen.io/inorganik/pen/QjqzwG">a Codepen</a> of these new form fields as a proof of concept.</p>

### Custom Form Controls Learnings

*   Rolling your own form controls, especially for dropdown menus, on a project of this size and complexity is not worth the hassle. The only thing you’ll gain is shiny controls.
*   Do what you can with native form code, and avoid replacing it with custom markup.
*   Try using background images, SVGs and pseudo-selectors to achieve the look you want.</p>

## Pattern Consistency

With a code base this big, pattern consistency becomes really important. Big code bases should look as though a single person developed it. In practice, this is easier said than done.

Anytime we developers code something, we can look back almost immediately and realize how we could have done it better. That’s just human nature. There’s always this temptation to change and improve one’s patterns. It’s a healthy but dangerous instinct.

I would argue that pattern consistency across a big code base is more important than doing something different in one place, even if you know the solution is five times better.

Think of it like the user experience of your code. Once you learn one pattern, you would expect it to look and work the same way everywhere else. If it doesn’t, then you’ll get bogged down in a costly spiral of troubleshooting and debugging in order to learn how the foreign pattern works — and you’ll then have to keep track of more than one pattern in your head.

When patterns are all over the map, you end up with steep learning curves and unproductive developers across the team or, even worse, individual developers who hold all of the knowledge of the patterns they’ve worked on.</p>

### UI Docs

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51444432-16ac-4e81-ae47-c94b0c6cc87b/ui-docs-1344px-opt.png"><img title="UI documentation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/067f66fe-8653-4ad6-9410-bfab996e8e63/ui-docs-500px-opt.jpg" alt="UI documentation" /></a><figcaption>The UI documentation provides information about global styles, AngularJS directives and patterns. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51444432-16ac-4e81-ae47-c94b0c6cc87b/ui-docs-1344px-opt.png">View large version</a>)</figcaption></figure>

One of our most valuable assets on the front end that helped us maintain pattern consistency (and, as a bonus, prevented my instant messenger from blowing up with questions all day long) was the <strong>UI documentation</strong> that we built and maintained throughout the project.

We used Yeoman to generate the scaffolding of new AngularJS directives, which in turn generated a demo page for that directive that we could build from. So, most of our documentation was created during the development of the component; it practically built and maintained itself.

We built the documentation directly into the local and development environments, so that anyone working on the project could access and maintain it anytime.</p>

### Code Reviews

This project moved so fast that each person barely had time to get their own work done, let alone pay attention to what their peers were doing. Our <strong>pattern consistency degraded over time</strong> as a result.

To combat this later in the project, we started doing <strong>peer code reviews</strong>. Before merging code into the main repository, a developer would request a review from a handful of peers, and they would not check in or merge their code until at least one team member had reviewed and approved it. At first, this workflow slowed things down a bit, but the result was that our patterns aligned, we caught bugs, and knowledge of the code was better disseminated.</p>

### Guidelines

While <a href="https://jshint.com/">JSHint</a> helps with enforcing some JavaScript standards and the UI documentation helped as a general reference, a higher level of consistency is still missing in the front-end code base. Looking back, it would have been helpful to establish some <a href="https://github.com/airbnb/javascript">detailed guidelines</a> for the JavaScript, HTML and CSS that could be referenced and followed throughout the project, and to enforce as much as possible via Grunt tasks.</p>

### Pattern Consistency Learnings

*   Changing patterns for the better is a good thing, but only if it can be done across the entire code base in one fell swoop and clearly communicated to the team.
*   Code reviews help to align patterns, catch bugs and spread learning.
*   UI documentation is a great reference for everyone involved. The next time around, I would look into creating a [living style guide](https://www.smashingmagazine.com/2015/04/an-in-depth-overview-of-living-style-guide-tools/) — self-generated and self-maintained from the source code, via a tool like [KSS](https://warpspire.com/kss/styleguides/).
*   Document and enforce detailed JavaScript, HTML and CSS style guides, similar to [Airbnb’s for JavaScript](https://github.com/airbnb/javascript), [Google’s for JavaScript](https://github.com/google/styleguide), [GitHub’s for CSS](https://primercss.io/) and [Google’s for CSS and HTML](https://github.com/google/styleguide).
*   Use Grunt or Gulp tools wherever possible to automate the enforcement of patterns.</p>

## Conclusion

On a project of this size and scale, it was really hard to see the forest for the trees until we looked back from the other side. We made plenty of mistakes throughout the project. Some we recovered from gracefully; with others, our efforts were too little too late, and we have to live with them.

A wise person once said that making mistakes is a rite of passage to success. It makes us better. More importantly, learning from each other is how we get better as a community, so that history doesn’t repeat itself.

What really matters in the end is how well a website works and the experience people have while using it. And we’ve ended up with something we’re all really proud of, an experience that makes you want to sink your toes in the sand, sip on a Mai Tai and get lobstered by the sun.

I hope this story helps you start your next big project and arms you with the foresight to go forth and conquer.

{{< signature "vf, ml, al, jb" >}}

