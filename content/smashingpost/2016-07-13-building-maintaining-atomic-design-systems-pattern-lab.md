---
title: How To Make And Maintain Atomic Design Systems With Pattern Lab 2
slug: building-maintaining-atomic-design-systems-pattern-lab
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886e1c37-07f2-45ab-9cf4-89c74d716c26/pattern-lab-2-image-16-opt.png
date: 2016-07-13T22:42:24.000Z
author: bradfrost
description: >-
  The benefits of UI design systems are now well known. They lead to more
  cohesive, consistent user experiences. They speed up your team’s workflow,
  allowing you to launch more stuff while **saving huge amounts of time and
  money in the process**. They establish a common vocabulary between
  disciplines, resulting in a more collaborative and constructive workflow.

  They make browser, device, performance, and accessibility testing easier. And
  they serve as a solid foundation to build upon over time, helping your
  organization to more easily adapt to the ever-shifting web landscape. This
  article provides a detailed guide to building and maintaining **atomic design
  systems** with Pattern Lab 2.
categories:
  - Coding
  - Style Guides
  - Generators
  - Static Generators
  - Design Systems
  - Pattern Libraries
---
The benefits of UI design systems are now well known. They lead to more cohesive, consistent user experiences. They speed up your team’s workflow, allowing you to launch more stuff while <strong>saving huge amounts of time and money in the process</strong>. They establish a common vocabulary between disciplines, resulting in a more collaborative and constructive workflow.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75a65a52-cb15-4094-8fd6-6a9124b6fa64/pattern-lab-2-image-0-opt.png" width="500" height="192" alt="Pattern Lab" title="Making And Maintaining Atomic Design Systems With Pattern Lab 2" /></figure>

They make browser, device, performance, and accessibility testing easier. And they serve as a solid foundation to build upon over time, helping your organization to more easily adapt to the ever-shifting web landscape.

In order to create these systems, we have to establish a <a href="https://www.smashingmagazine.com/2017/07/pattern-libraries-in-markdown/">Pattern Library in Markdown</a>. We need to break our interfaces down into smaller parts, but we simultaneously need to ensure those parts come together to form a beautiful and functional whole. "<a href="https://atomicdesign.bradfrost.com/chapter-2">Atomic design</a>" is a helpful mental model that helps us do just that, and Pattern Lab is a suite of tools that helps bring these atomic design systems to life.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Taking Pattern Libraries To The Next Level](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)
*   [Smart Responsive Design Patterns](https://www.smashingmagazine.com/2016/05/smart-responsive-design-patterns-or-when-off-canvas-isnt-good-enough/)
*   [An In-Depth Overview Of Living Style Guide Tools](https://www.smashingmagazine.com/2015/04/an-in-depth-overview-of-living-style-guide-tools/)
*   [Meet Inclusive Front-End Design Patterns](https://www.smashingmagazine.com/inclusive-design-patterns/)

{{% feature-panel %}}

After over two years of hard work, we’re happy to announce <a href="https://patternlab.io/">Pattern Lab 2</a>! Totally reimagined, Pattern Lab 2 is an open-source suite of tools to help you and your team <strong>create and maintain thoughtful UI design systems</strong>. At its core, it’s a static site generator that stitches together patterns and allows you to design with dynamic data.

A few highlights of the new version include:

*   A totally restructured core that supports more languages, templating engines, and data formats
*   Supporting Markdown for pattern documentation
*   Adding YAML support as well as JSON for managing dynamic data
*   Plugins to extend and enhance Pattern Lab’s functionality
*   A themable, extendable, redesigned frontend UI

But more than anything, Pattern Lab 2 has been designed and built so your team can effectively use it during every phase of your design system process, from the very beginning all the way through to its long-term maintenance.</p>

{{< vimeo id="174472797" >}}

<figcaption>Atomic design is atoms, molecules, organisms, templates, and pages working together to create effective interface design systems. And Pattern Lab is a suite of tools that helps your team make atomic design systems happen. (<a href="https://vimeo.com/174472797">Watch video on Vimeo</a>)</figcaption>
</figure>

## Pattern Lab At Project Start

Your team has been tasked with making a new application and underlying design system. Once upon a time, your teams’ UX designers might have holed up in a room to define the product by way of monolithic, heavily-annotated wireframes. Once approved, they’d get passed off to visual designers who would then apply color, typography, and texture to bring the wireframes to life. After <code>homepage_v9_final_forReview_jimEdits_05-12__FINAL.psd</code> finally gets approved, the designs are sent off to the frontend developers, who quickly burst into tears since the designs contain a slew of unrealistic layouts, improbable user content (every username is only 4 characters—how convenient!), and a potpourri of font faces and incongruent design patterns.

The throw-over-the-wall design process is dead and gone. Collaboration, iteration, and quick development are essential for tackling this ever-shifting, diverse web landscape. We need to get into the browser as soon as possible and test designs under real-world variables like responsiveness, performance, ergonomics, and motion. That’s why it’s critical to treat <a href="https://atomicdesign.bradfrost.com/chapter-4/#development-is-design">front-end development as a core part of the design process</a>, and why it’s so crucial to get designers and frontend developers working closely together. At the end of the day, we’re all working on the same UI.

Setting up an instance of Pattern Lab on Day 1 of your project can create a shared workshop — or laboratory, if you will — equipped with design and development tools, a watercooler, a whiteboard, and a microscope. It provides a place for each discipline to contribute their perspective to the living, breathing design system. In a real sense, Pattern Lab can serve as the hub of your design system project, minimizing the need to create overly verbose wireframes, red-lined static comps, and other clunky static artifacts.

Sounds great, right? Let’s walk through how you can spin up Pattern Lab on Day 1 of your project.

Pattern Lab 2 comes in both <a href="https://patternlab.io/download.html">PHP and Node flavors</a>. <em>Teams, choose your adventure!</em> Some projects yield a clear tech-stack choice. Others come down to team skillset or environmental precedence. Whichever the platform, Pattern Lab 2 is poised to help you and your team collaborate on building your new application and design system. Whatever your platform choice, know that with either version Pattern Lab will produce nearly identical results — much like cars of different makes and models all bring you to the same destination.</p>

### Installing Pattern Lab

Once the appropriate <a href="https://patternlab.io/docs/requirements.html#node">prerequisites are installed</a>, you’ll be ready to install Pattern Lab. Let’s take a look at how to install Pattern Lab Node, but keep in mind that <a href="https://patternlab.io/docs/installation.html#php">PHP instructions are also available and are similar.</a>

From your terminal window, navigate to a directory you’d like to install Pattern Lab into. Then type the following commands:

1.  `git clone https://github.com/pattern-lab/edition-node-gulp.git`
2.  `npm install`
3.  Once complete, `gulp patternlab:serve`

Running <code>npm install</code> will pull down the latest dependencies, and <code>gulp patternlab:serve</code> will generate and self-host Pattern Lab, opening the frontend in your default browser. And if you don’t wish to clone the git repository directly, you could alternatively <a href="https://github.com/pattern-lab/edition-node-gulp/releases/latest">download the latest release</a> and then perform steps 2 and 3.

With Pattern Lab up and running, your team now has a hub for which to design, develop, and review your soon-to-be-established design system.</p>

### Pattern Lab’s Filesystem

Pattern Lab compiles everything found in your project’s <code>/source</code> folder into static HTML files that live in the <code>/public</code> folder. This output can then be displayed or consumed individually or inside the style guide frontend. Let’s take a look at Pattern Lab’s filesystem and what lives inside of <code>source/</code>:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51f59401-44e9-45d0-9584-a610347f72f6/pattern-lab-2-image-1-opt.png" alt="Pattern Lab’s filesystem" /><figcaption>Pattern Lab’s filesystem</figcaption></figure>

*   `_annotations/` - where your team can define [living annotations](https://patternlab.io/docs/pattern-adding-annotations.html) to bolster your UI documentation
*   `_data/` - where the [global data](https://patternlab.io/docs/data-overview.html) used to render your patterns resides.
*   `_meta/` - where the [`<head>` and foot](https://patternlab.io/docs/pattern-header-footer.html) (which bookend all of your patterns) information resides.
*   `_patterns/` - where your [patterns](https://patternlab.io/docs/pattern-organization.html), pattern documentation, and pattern-specific data reside.
*   css - where your stylesheets can reside
*   images - where your images can reside
*   js - where your javascript can reside

It’s worth stressing that Pattern Lab doesn’t force any frontend conventions or production dependencies onto you. How you decide to structure your folders and which technologies you choose is totally up to you. If you want to call your folder <code>/stylesheets</code> instead of <code>/css</code> go for it! Want to use Sass? Nice! Love jQuery? Great! Hate it? That’s fine too! Pattern Lab simply exists to stitch your patterns together and gets out of the way of any frontend decisions you make. You can even configure how your <a href="https://patternlab.io/docs/pattern-managing-assets.html">assets are managed</a> as they travel from from <code>source/</code> to <code>public/</code>.</p>

### Choose Your Own Adventure: Naming Conventions and Configuration

Atomic design is a helpful mental model to think about constructing UI design systems, but it’s certainly <a href="https://atomicdesign.bradfrost.com/chapter-2/#whats-in-a-name">not rigid dogma</a>. It’s important to choose a nomenclature that helps your team speak the same language and do great work together.

Pattern Lab’s naming conventions, like most aspects of the software, are entirely configurable. While Pattern Lab <code>patterns/</code> folder defaults to “atoms”,”molecules”, “organisms”, “templates”, and “pages, you’re free to modify, remove, or add to your heart’s desire. For instance, if we were to recreate <a href="https://medium.com/ge-design/ges-predix-design-system-8236d47b0891#.f1gp6kch7">GE’s Predix design system’s taxonomy</a> — which consists of Principles, Basics, Components, Templates, Features, and Applications — we would structure Pattern Lab’s <code>/source/_patterns/</code> directory to be as follows:

<pre><code class="language-markup">
    /00-Principles/

    /01-Basics/

    /02-Components/

    /03-Templates/

    /04-Features/

    /05-Applications/
</code></pre>

Pattern Lab is designed to conform to your workflow, not the other way around.

## Establishing Design Direction

Even during the first days or hours of a project, everyone has something to contribute to your Pattern Lab. This is a time for exploring, figuring things out, and creating alignment. Each role conducts different activities, but their output and input is linked. Each is inflating a separate tire of the vehicle that will get you all to your destination.</p>

### Defining lo-fidelity IA in Pattern Lab

Early UX design work involves determining the application’s information architecture. Rather than immediately reaching for high-fidelity wireframe tools that tend to prematurely define layouts and technical functionality, it’s better to create lo-fi sketches that establish what goes on a particular screen and in what general order. This work can take the form of napkin sketches, bulleted lists, or spreadsheets. Since Pattern Lab supports basic markup, it’s possible to quickly translate these <a href="https://www.smashingmagazine.com/2016/02/create-content-wireframes-for-responsive-design/">content reference diagrams</a> into the browser right away. For the Pittsburgh Food Bank <a href="https://foodbank.bradfrostweb.com/timeline/">redesign</a>, we stubbed out the each template using this approach.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50a53353-1d3b-48eb-88ef-246bdae9953b/pattern-lab-2-image-2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d962634-2ff9-4602-a6f3-685226ba8249/pattern-lab-2-image-2-opt.png" alt="For the redesign of the Pittsburgh Food Bank website, wireframes were quickly translated from paper sketches into Pattern Lab using some dirt-simple markup and placeholder divs." /></a><figcaption>For the redesign of the Pittsburgh Food Bank website, wireframes were quickly translated from paper sketches into Pattern Lab using some dirt-simple markup and placeholder divs. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50a53353-1d3b-48eb-88ef-246bdae9953b/pattern-lab-2-image-2-large-opt.png">Large preview</a>)</figcaption></figure>

So the homepage template code, found in <code>/source/_patterns/templates/homepage.mustache</code> looks like this:

<pre><code class="language-markup">
{{&gt; organisms-header }}

&lt;div class="fpo"&gt;Mission Statement&lt;/div&gt;

&lt;div class="fpo"&gt;Campaign&lt;/div&gt;

&lt;div class="fpo"&gt;Get Help&lt;/div&gt;

&lt;div class="fpo"&gt;Give Help&lt;/div&gt;

&lt;div class="fpo"&gt;Learn&lt;/div&gt;

{{&gt; organisms-footer }}
</code></pre>

We’re including a header and footer pattern, and then simply stubbing out the content we’re anticipating to include on this page.</p>

### Capturing Visual Design Decisions

Early visual design work involves exploring typography, color palettes, and other aspects of the visual brand. Historically, designers might leap into creating high-fidelity, desktop-centric Photoshop mockups, designers now have helpful tools like <a href="https://styletil.es/">style tiles</a>, <a href="https://typecast.com/">Typecast</a> and <a href="https://danielmall.com/articles/rif-element-collages/">element collages</a> to establish visual design direction without resorting to premature, high-fidelity comps.

As decisions get made around color palettes and font pairings, Pattern Lab can capture the results of those design decisions, ensuring the design and development team aren’t unintentionally generating 50 shades of gray.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3262545a-72df-42f9-b932-888259c27f6e/pattern-lab-colors-large.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c8afc18-78fe-4751-892e-4cebf7496086/pattern-lab-colors-opt.jpg" alt="Pattern Lab documents color palettes and font families, and other visual design elements. Capturing these decisions early in a project ensures designers and developers use colors and typography consistently throughout the process." /></a><figcaption>Pattern Lab documents color palettes and font families, and other visual design elements. Capturing these decisions early in a project ensures designers and developers use colors and typography consistently throughout the process. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3262545a-72df-42f9-b932-888259c27f6e/pattern-lab-colors-large.jpg">Large preview</a>)</figcaption></figure>

### Becoming a Frontend Prep Chef in Pattern Lab

And then there’s frontend code. In these early stages of a project, frontend developers may be tempted to sit tight and wait for designers to come up with a direction before diving into code. But this type of thinking keeps designers and developers out of sync with each other and prevents true collaboration from happening.

Like prep chefs at a restaurant, developers have a huge opportunity to get to work <a href="https://atomicdesign.bradfrost.com/chapter-4/#frontend-prep-chef">prepping</a> the patterns and code that will ultimately become the final design system. In the early days of the project, developers can begin stubbing out patterns and and <a href="https://patternlab.io/docs/pattern-header-footer.html">importing</a> <a href="https://patternlab.io/docs/editing-source-files.html">assets</a> into Pattern Lab, getting things set up early so designers and developers can spend more time actually working together to design and build the UI.

Color palettes, real copy, and layout have yet to be established, but that shouldn’t stop developers from scaffolding the structures that support the content wireframes. Take a hero <a href="https://patternlab.io/docs/pattern-organization.html">pattern</a>, for example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f3d0b9b-18d9-4dc6-b55d-c80d2f8d59b9/pattern-lab-2-image-4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb61fd7-2413-47bf-bea4-aa775d329c1c/pattern-lab-2-image-4-opt.png" alt="A hero pattern may initially consist of blocky greys and lorem ipsum, which at this stage is more than OK. Taking the time to set things up early opens doors for true collaboration with designers." /></a><figcaption>A hero pattern may initially consist of blocky greys and lorem ipsum, which at this stage is more than OK. Taking the time to set things up early opens doors for true collaboration with designers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f3d0b9b-18d9-4dc6-b55d-c80d2f8d59b9/pattern-lab-2-image-4-large-opt.png">Large preview</a>)</figcaption></figure>

This pattern <a href="https://patternlab.io/docs/pattern-including.html">includes other patterns</a>, which is a powerful way to consume smaller interface elements into ever-larger structures. Here’s the markup for <code>block-hero.mustache</code>:

<pre><code class="language-markup">
&lt;a href="{{ url }}" class="c-block-hero"&gt;
    {{&gt; atoms-hero-img }}

    &lt;h2 class="c-block-hero__headline"&gt;{{ headline.medium }}&lt;/h2&gt;

&lt;/a&gt;&lt;!-- end c-block--hero--&gt;
</code></pre>

The double curly bracket code (<code>{{}}</code>) is <a href="https://mustache.github.io/">Mustache</a> templating code, which allows us to define dynamic content and include patterns inside one another. For example, the code <code>{{&gt; atoms-hero-img }}</code> tells Pattern Lab to look for an atom called “hero-img” and include it in the pattern. The hero unit itself can then be included in more complex patterns using the same include convention using the following: <code>{{&gt; molecules-hero }}</code>.

This Russian nesting doll approach to including patterns allows your codebase to stay nice and <a href="https://en.wikipedia.org/wiki/Don%27t_repeat_yourself">DRY</a>, meaning that if you make an edit to any particular pattern, anywhere that pattern is included will be updated automatically. This keep your designs and codebase in sync and consistent. And on top of all that, this continual build up of patterns can yield near-complete interfaces in short order!

## Rolling Up Our Sleeves

The information architecture has started to take shape, the initial aesthetic direction has been established, and nascent patterns have been stubbed out in Pattern Lab. Now the team can now collectively dive into building out the interface design system in earnest. Let’s discuss how to use Pattern Lab to turn a vague sense of direction into a beautiful, functional, thoughtful, and complete design system.</p>

### Designing with Dynamic Data

One important concept of atomic design is the differences between <a href="https://atomicdesign.bradfrost.com/chapter-2/#templates">templates</a> and <a href="https://atomicdesign.bradfrost.com/chapter-2/#pages">pages</a>. Templates define the underlying content structure of a UI, while pages are specific instances of those templates that replace that content structure with real representative content. Both are necessary to document content parameters while also showing the design patterns in action and populated with real content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08c6c22d-b6e4-47e9-8f88-ddaf5a54319c/pattern-lab-2-image-5-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25c28a7c-9df4-4bb1-bd45-e6c5482e70b1/pattern-lab-2-image-5-opt.png" alt="On the left, you can see the homepage template that exposes the UI’s underlying content structure. On the right, real representative content is poured into that content structure to articulate what users will see." /></a><figcaption>On the left, you can see the homepage template that exposes the UI’s underlying content structure. On the right, real representative content is poured into that content structure to articulate what users will see. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08c6c22d-b6e4-47e9-8f88-ddaf5a54319c/pattern-lab-2-image-5-large-opt.png">Large preview</a>)</figcaption></figure>

One of the most powerful Pattern Lab features is the ability to swap in different representative content into your UI patterns to ensure they can handle the dynamic nature of your content. What if your user doesn’t upload a profile picture? What if the user has 13 items in their shopping cart versus 2 items? What if one of those products has 14 potential variations? What if the blog post title contains 400 characters? Return user? First-time user? What if the article has no comments? Or what about when it has seven layers of nested comments? What if we need to display an urgent message on the dashboard when their account is hacked? Pattern Lab allows you to manipulate data to express any number of various UI states and variants of any template.</p>

### Page-Specific Data

Initial data in Pattern Lab is stored in a file called <code>/source/_data/data.json</code>, which contains the data that patterns will initially consume to be displayed in the style guide and template views. Your default <code>data.json</code> may look something like this:

<pre><code class="language-json">
{
   "headline" : {
        "short" : "Lorem ipsum dolor sit (37 characters)",
        "medium" : "Lorem ipsum dolor sit amet, consectetur adipiscing elit iopa. (76 characters)"
    },
    "url": "#",
    "imgHero" : {
        "src": "../../images/fpo_hero-opt.png",
        "alt": "Hero Image"
    },
    "imgLandscape" : {
        "src": "../../images/fpo_16x9-opt.png",
        "alt": "Landscape Image"
    },
    "mediaList": []
}
</code></pre>

You can reference these pieces of data in your patterns (i.e. including <code>{{ headline.short }}</code> in a pattern) to achieve results like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e889c20-870b-42b9-83a8-230bed9c63ff/pattern-lab-2-image-6-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eead5c4-4dbb-42d3-8eeb-e4bd0c737e8f/pattern-lab-2-image-6-opt.png" alt="A homepage template rendered in Pattern Lab and stubbed out with default data defined in data.json." /></a><figcaption>A homepage template rendered in Pattern Lab and stubbed out with default data defined in <code>data.json</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e889c20-870b-42b9-83a8-230bed9c63ff/pattern-lab-2-image-6-large-opt.png">Large preview</a>)</figcaption></figure>

At the page level, we want to replace those grayscale images and lorem ipsum placeholder text with real content. To accomplish this, we’ll make a new file right next to <code>/source/_patterns/pages/homepage.mustache</code> called <code>homepage.json</code>, where we can override the initial data defined in `data.json. That might look something like this:

<pre><code class="language-json">
"imgHero" : {
      "src": "../../images/sample/hero-forest.jpg",
      "alt": "Forest"
    },
    "headline" : {
        "medium" : "Track your hikes. Challenge your friends. Get out there and start exploring."
    },
    "toutList" : [
      {
        "url": "link.pages-blog-detail",
        "headline": {
            "short" : "Best winter hikes around the world"
        },
        "imgLandscape" : {
          "src": "../../images/sample/tout-winter-hiker.jpg",
            "alt": "Hiker with back pack walking in snow"
        }
      },
      {
        "url": "link.pages-login",
        "headline": {
            "short" : "Sign in to view your dashboard"
        },
        "imgLandscape" : {
          "src": "../../images/sample/tout-leaves.jpg",
            "alt": "Green Leaves"
        }
      },
      {
        "url" : "link.pages-about",
        "headline": {
            "short" : "Learn about our mission"
        },
        "imgLandscape" : {
          "src": "../../images/sample/tout-mountains.jpg",
            "alt": "Mountain"
        }
      }
    ]
</code></pre>

This results in a UI that looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8827eaa3-bde4-4f96-91cb-04424793dafc/pattern-lab-2-image-7-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4f4ab6f-1542-4e5a-acc5-4ea51cb2a7f6/pattern-lab-2-image-7-opt.png" alt="Pattern Lab takes the data defined in homepage.json"></a><figcaption>Pattern Lab takes the data defined in <code>homepage.json</code> and overrides the default data defined in <code>data.json</code> to render a UI that would be similar to what users would interact with. This stage is obviously important as it’s what the end user will likely see, but it also is critical for testing the resiliency of the underlying patterns that make up the UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8827eaa3-bde4-4f96-91cb-04424793dafc/pattern-lab-2-image-7-large-opt.png">Large preview</a>)</figcaption></figure>

### Pseudo-Patterns

Our design systems need to be flexible and adapt to the reality of the content that lives in our applications. We need to concurrently account for the best-case situations, the worst, and everything in between.

Expressing these UI variations in static design tools is an exercise in tediousness and redundancy, which may explain why they’re rarely designed. But Pattern Lab’s pseudo-pattern feature allows us to articulate (sometimes wildly) different scenarios with just a few changes to our data.

Let’s say we’re making a hike-tracking app whose dashboard displays a list of hiking statistics: elevation climbed, number of trails hiked, steps taken, and so on. For an active user who has been consistently inputting content into the app, the UI might look something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0d4ed4f-03a5-46dc-bad6-a5c1e3da23e6/pattern-lab-2-image-8-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0813f798-ab78-414b-b5b4-924c86b5a2d1/pattern-lab-2-image-8-opt.png" alt="Here’s a hypothetical dashboard for a fictitious hike-tracking app. Pattern Lab replaces default data with page-specific data to showcase what a user might see after logging in." /></a><figcaption>Here’s a hypothetical dashboard for a fictitious hike-tracking app. Pattern Lab replaces default data with page-specific data to showcase what a user might see after logging in. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0d4ed4f-03a5-46dc-bad6-a5c1e3da23e6/pattern-lab-2-image-8-large-opt.png">Large preview</a>)</figcaption></figure>

In <code>/source/_patterns/pages/dashboard.json</code>, our data would look something like this:

<pre><code class="language-json">
{
  "blockFeature":{
    "number":"4,500",
    "headline":{
      "short":"Feet of Elevation Gain"
    },
    "progress":{
      "max":"100",
      "progressValue":"100",
      "label":"Progress: 100%"
    }
  },
  "tileList":[
    {
      "number":"16",
      "headline":{
        "short":"National Parks"
      },
      "progress":{
        "max":"100",
        "progressValue":"20",
        "label":"Progress: 20%"
      }
    },
    {
      "number":"500",
      "headline":{
        "short":"Hikes"
      },
      "progress":{
        "max":"100",
        "progressValue":"40",
        "label":"Progress: 40%"
      }
    },
    {
      "number":"62,500",
      "headline":{
        "short":"Calories Burned"
      },
      "progress":{
        "max":"100",
        "progressValue":"60",
        "label":"Progress: 60%"
      }
    },
    {
      "number":"94,300,843",
      "headline":{
        "short":"Steps"
      },
      "progress":{
        "max":"100",
        "progressValue":"80",
        "label":"Progress: 80%"
      }
    }
  ],
  ...
}
</code></pre>

With this data, Pattern Lab is able to populate the UI with this user’s wealth of generated content.

However, this scenario may not be all that common. For every ambitious user who takes the time to populate every field and connect every available application, there are likely to be dozens of casual users who don’t fill in every blank and take advantage of all the app’s features. For that matter, at one point in every user’s journey, they are entirely new to the interface! Let’s articulate these important variations using Pattern Lab’s pseudo-pattern feature.

In our <code>/source/_patterns/pages/</code> directory, we can create a new pseudo-pattern called <code>dashboard~new-user.json</code>. This will create another instance of the page that inherits all the data from <code>dashboard.json</code>, but also allows us to further modify or extend the data. In the case of <code>dashboard~new-user.json</code>, we can override bits of a data to demonstrate what a new user experience might look like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb23662e-0f71-4ff4-9321-48e62838549c/pattern-lab-2-image-9-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcd0573e-2410-499a-8adc-bbed4017bde4/pattern-lab-2-image-9-opt.png" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb23662e-0f71-4ff4-9321-48e62838549c/pattern-lab-2-image-9-large-opt.png">Large preview</a>)</figcaption></figure>

And here’s the data we’re adding to the file to accomplish this UI:

<pre><code class="language-json">
{
  "blockFeature":{
    "styleModifier":"featured",
    "number":"0",
    "headline":{
      "short":"Feet of Elevation Gain"
    },
    "progress":{
      "max":"100",
      "progressValue":"0",
      "label":"Progress: 0%"
    },
    "overlay":{
      "overlayMessage":"Let's go on a hike and climb in elevation",
      "overlayAction":"Find a Hike"
    }
  },
  "tileList":[
    {
      "number":"0",
      "headline":{
        "short":"National Parks"
      },
      "progress":{
        "max":"100",
        "progressValue":"0",
        "label":"Progress: 0%"
      },
      "overlay":{
        "overlayMessage":"What National Parks have you visited?",
        "overlayAction":"Find a National Park"
      }
    },
    {
      "number":"0",
      "headline":{
        "short":"Hikes"
      },
      "progress":{
        "max":"100",
        "progressValue":"0",
        "label":"Progress: 0%"
      },
      "overlay":{
        "overlayMessage":"Been on a hike recently?",
        "overlayAction":"Log Your First Hike"
      }
    },
    {
      "number":"0",
      "headline":{
        "short":"Calories Burned"
      },
      "progress":{
        "max":"100",
        "progressValue":"0",
        "label":"Progress: 0%"
      },
      "overlay":{
        "overlayMessage":"Trying to stay healthy?",
        "overlayAction":"Track Calorie Count"
      }
    },
    {
      "number":"0",
      "headline":{
        "short":"Steps"
      },
      "progress":{
        "max":"100",
        "progressValue":"0",
        "label":"Progress: 0%"
      },
      "overlay":{
        "overlayMessage":"Counting steps?",
        "overlayAction":"Connect Your Fitbit"
      }
    }
  ]
}
</code></pre>

By overriding some of the values in <code>dashboard.json</code> we’re able to modify the content and turn on/off particular patterns.

In another instance, we may need to demonstrate what the UI looks like when there’s a security issue or some other problem with the user’s account. We can create the <code>dashboard~hacked.json</code> pseudo-pattern to create the following UI:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/090b2858-d571-435f-94ef-0ecf82c7cbe2/pattern-lab-2-image-10-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8160f1c-2e92-4eac-8403-cf5a43571590/pattern-lab-2-image-10-opt.png" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/090b2858-d571-435f-94ef-0ecf82c7cbe2/pattern-lab-2-image-10-large-opt.png">Large preview</a>)</figcaption></figure>

Most of the data from <code>dashboard.json</code> will stay the same, but we’ll add the following to create the error message:

<pre><code class="language-json">
{
    "alert" : {
        "alertClass" : "error",
        "alertText" : "On May 22nd, hackers from a hidden underground tunnel somewhere in Siberia hacked our servers and compromised all of our sensitive data. &lt;a href='#'&gt; Please reset your password immediately!&lt;/a&gt;"
    }
}
</code></pre>

### Pattern Parameters

There are times when using Pattern Lab that warrant full pseudo-patterns, as illustrated above. But sometimes you may need to tweak or override only a single data value within a pattern, leaving the rest to be handled by the other dynamic display patterns. For these instances, pattern parameters are your tool of choice. Pattern parameters are a simple mechanism for replacing variables in an included pattern. They are limited to replacing variables in the included pattern and <strong>only </strong>the included pattern. Consider this excerpt of the detail template:

<pre><code class="language-markup">
...
&lt;div class="l-sidebar"&gt;

    {{# latestPosts }}

    {{&gt; organisms-section-media-list }}

    {{/ latestPosts}}

    {{# featuredPeople }}

    {{&gt; organisms-section-media-list }}

    {{/ featuredPeople}}

&lt;/div&gt;&lt;!--end .l-sidebar--&gt;

...
</code></pre>

which is includes the section media list pattern.</p>

<pre><code class="language-markup">
&lt;section class="c-section"&gt;
    {{# sectionTitle}}
    &lt;h2 class="c-section__title"&gt;{{ sectionTitle }}&lt;/h2&gt;
    {{/ sectionTitle }}

    {{&gt; organisms-media-list }}

{{# textButton }}
    {{&gt; atoms-text-button }}
    {{/ textButton }}

{{# overlay }}
    {{&gt; molecules-overlay }}
    {{/ overlay}}
&lt;/section&gt;&lt;!--end section--&gt;
</code></pre>

As we’ve learned, <code>{{sectionTitle}}</code> for both the latestPosts and featuredPeople data blocks will populate from any companion .json present, with <code>/source/_data/data.json</code> as the global fallback. We are including a single pattern multiple times, however, and may want to quickly supply unique data to each pattern without having to create these keys in our .json. We can change the included section media lists to the following:

<pre><code class="language-markup">
...

&lt;div class="l-sidebar"&gt;

    {{# latestPosts }}

    {{&gt; organisms-section-media-list(sectionTitle: "The latest from the moleskine") }}

    {{/ latestPosts}}

    {{# featuredPeople }}

    {{&gt; organisms-section-media-list(sectionTitle: "Staff Hikers") }}

    {{/ featuredPeople}}

&lt;/div&gt;&lt;!--end .l-sidebar--&gt;

...
</code></pre>

These two organisms will now use the <code>sectionTitle</code> variable defined here when rendering. Pattern parameters are powerful, but are only supported by the PHP and Node Mustache PatternEngines. Other template languages provide better solutions to this problem. <a href="https://patternlab.io/docs/pattern-parameters.html">Check out the docs</a> to read the full skinny on parameters parameters.</p>

### styleModifiers

Often you’ll find yourself wishing to display stylistic variants of the same pattern, such as colored social media buttons or component states. An extension to the shorthand include syntax, <code>styleModifiers</code> supply additional classes to a pattern. Provided you construct a pattern <code>block-media</code> with <code>{{ styleModifier}}</code> within the class attribute:

<pre><code class="language-markup">
&lt;a href="{{ url }}" class="c-block-media c-block-media--{{ styleModifier }}"&gt;

    &lt;div class="c-block-media__media"&gt;

        {{&gt; atoms-square:c-block-media__img }}

    &lt;/div&gt;

    &lt;div class="c-block-media__body"&gt;

        &lt;h2 class="c-block-media__headline"&gt;{{ headline.short }}&lt;/h2&gt;

        &lt;p class="c-block-media__excerpt"&gt;{{ excerpt.medium }}&lt;/p&gt;

    &lt;/div&gt;&lt;!-- end c-block-media__body --&gt;

&lt;/a&gt;&lt;!-- end c-block-media --&gt;
</code></pre>

Including this pattern with a colon after the name sets the styleModifier:

<pre><code class="language-markup">
{{&gt; molecules-block-media:fullBleed }}
</code></pre>

would yield an anchor tag like this:

<pre><code class="language-markup">
&lt;a href="path/to/url" class="c-block-media c-block-media--fullBleed"&gt;
</code></pre>

<code>styleModifiers</code> can be combined to supply multiple classes, using pipe (|) as a delimiter.</p>

<pre><code class="language-markup">
{{&gt; molecules-block-media:fullBleed|is-lazyLoaded }}
</code></pre>

Between pseudo-patterns, pattern parameters, and <code>styleModifiers</code>, Pattern Lab makes it easier to demonstrate sometimes wildly different UI variations while keeping the underlying codebase DRY in the process.</p>

### Iterating in Style

A key element of a pattern-based workflow is embracing iteration and recognizing that patterns and the design will continue to evolve. <a href="https://atomicdesign.bradfrost.com/chapter-2/#the-part-and-the-whole">The parts will shape the whole, the whole will shape the parts</a>, and the interconnected system of components will emerge as a result of this process.

Another natural consequence of this process is that the point of production shifts from the hands of UX and visual designers into the hands of frontend developers much earlier. Rather than burning a lot of precious time creating a slew of high-fidelity comps and detailed wireframes, design work can move from static documents into browser where your team can sooner address the realities of the web.

With Pattern Lab as the watering hole for the whole team, designers can better understand how decisions made in one area affect other areas.</p>

### Viewport testing with ish.

It’s important for our components, as well as our pages, to be flexible across the entire resolution spectrum. Baking a viewport resizing tool like <a href="https://bradfrost.com/demo/ish/">ish.</a> into a pattern library ensures each element looks and functions beautifully at any screen size. Taking the time to craft fully flexible patterns will better prepare us for a future when <a href="https://www.smashingmagazine.com/2013/06/media-queries-are-not-the-answer-element-query-polyfill/">element queries</a> and <a href="https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/">web components</a> have fully matured (we can’t wait!).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769e7e4d-4619-421d-a8a0-a685d7af243b/pattern-lab-2-image-11-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39eb09ea-9074-476d-a55d-75335d2a1447/pattern-lab-2-image-11-opt.png" alt="ish. is a viewport testing tool baked into Pattern Lab that allows you to view patterns and pages across the entire resolution spectrum in a device-agnostic way." /></a><figcaption>ish. is a viewport testing tool baked into Pattern Lab that allows you to view patterns and pages across the entire resolution spectrum in a device-agnostic way. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769e7e4d-4619-421d-a8a0-a685d7af243b/pattern-lab-2-image-11-large-opt.png">Large preview</a>)</figcaption></figure>

By having these viewport tools baked right into the frontend environment, designers and developers can huddle around Pattern Lab to determine where to insert breakpoints into the design. Moreover, clients, QA, and other colleagues can pinpoint specific areas where the UI falls apart for whatever reason.</p>

## Ready To Launch

The project is coming together nicely, but before it can be launched into the world things need to be tightened up, cross-browser/device tested, and properly documented. Let’s talk about how Pattern Lab can help get your design system code and documentation ready for prime time!

### Approachable Pattern Documentation

Some patterns may present themselves as self-documenting, but a pattern often requires some context or additional information to make things crystal clear. Things like definitions. usage guidelines, considerations, resources, and example images can and should find their way into pattern documentation. Pattern Lab 2’s documentation uses Markdown with YAML front matter to create this documentation. The markdown file accompanies the pattern (for example, <code>media-object.md</code> must sit right beside <code>media-object.mustache</code>), and can be formatted like this:

<pre><code>---
title: Utility Colors
---
The utility color palette defines colors that are used to convey meaning such as success, error, warning, and information to the user. These colors should be used for things like alert messages, form validation, tooltips, and other kinds of messaging.</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/012aa616-d694-47d7-930c-57e38d6374d4/pattern-lab-2-image-12-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e37c42ae-edba-458f-b11f-38609220cbaf/pattern-lab-2-image-12-opt.png" alt="When a documentation markdown file sits next to a pattern, it will show up in Pattern Lab’s UI." /></a><figcaption>When a documentation markdown file sits next to a pattern, it will show up in Pattern Lab’s UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/012aa616-d694-47d7-930c-57e38d6374d4/pattern-lab-2-image-12-large-opt.png">Large preview</a>)</figcaption></figure>

Markdown documentation means that IAs, visual designers, content strategists, business folks, etc can more easily contribute to living documentation. Product owners could even stub in functionality notes for new patterns before the pattern is even created. <a href="https://patternlab.io/docs/pattern-documenting.html">Improvements are planned</a> to make pattern documentation more powerful, further making Pattern Lab an evergreen space for your team.</p>

### Lineage for Easier QA

When looking at various patterns in a library, the lack of context can make it difficult to discern where they actually get used. Defining and describing pattern characteristics is one thing, but there’s an opportunity to provide additional contextual information about your UI patterns.

Thanks to the Russian nesting doll nature of Pattern Lab, it can display what patterns make up any given component, and also show where that pattern is consumed in the design system.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b1b7b59-1240-42d0-9d9a-1f15b45fe400/pattern-lab-2-image-13-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70c65aa4-4955-451f-a498-5fa8efad2a19/pattern-lab-2-image-13-opt.png" alt="Pattern Lab’s pattern info panel links to whatever patterns make up any given component, and also links to everywhere those patterns are employed. In this example, the “section media list” pattern is comprised of the “media-list” organism, “text-button” atom, and “overlay” molecule. This particular pattern is included in the “blog-index”, “dashboard”, and “homepage” templates." /></a><figcaption>Pattern Lab’s pattern info panel links to whatever patterns make up any given component, and also links to everywhere those patterns are employed. In this example, the “section media list” pattern is comprised of the “media-list” organism, “text-button” atom, and “overlay” molecule. This particular pattern is included in the “blog-index”, “dashboard”, and “homepage” templates. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b1b7b59-1240-42d0-9d9a-1f15b45fe400/pattern-lab-2-image-13-large-opt.png">Large preview</a>)</figcaption></figure>

Thanks to this feature, designers and developers have contextual information that comes in handy when QAing and/or making changes to the design system. If we wanted to make changes to a particular pattern, like doubling the size of the image or adding an additional text element, we’d immediately know which patterns and templates would need re-tested and QA’d to ensure nothing breaks with the changes. The lineage feature also helps point out unused or underutilized patterns so that teams can weed them out of the pattern library.</p>

### Showing Progress with Pattern States

Taking the concept of pattern lineage a step further, you and your team can keep track of each pattern’s progress and how it affects the whole system. Pattern Lab’s pattern state feature can track progress of a pattern from development, through review, to completion. With pattern states, you’ll always be able to answer “Are all the patterns that comprise this template complete?”

To give your pattern a state, you add a <code>state</code> to the frontmatter in that pattern’s documentation file. For instance:

<pre><code class="language-markup">---
title: Block Media
state: inreview
---
The media block consists of...</code></pre>

Applying this status will present the pattern state in a couple places across Pattern Lab.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b08f225-4790-4b56-90fe-f973fa91e9b1/pattern-lab-2-image-14-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b449f42-a74c-4f8e-871c-a7cc36c182d4/pattern-lab-2-image-14-opt.png" alt="Patterns with states show up on the navigation to give an at-a-glance look at which patterns still need work and which are completed." /></a><figcaption>Patterns with states show up on the navigation to give an at-a-glance look at which patterns still need work and which are completed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b08f225-4790-4b56-90fe-f973fa91e9b1/pattern-lab-2-image-14-large-opt.png">Large preview</a>)</figcaption></figure>

It’s important to note that the state of a pattern can be influenced by the patterns it contains. Flagging a pattern like <code>{{&gt; molecule-media-block }}</code> as <code>inreview</code> will cause a ripple effect anywhere that pattern is included. This helps identify bottlenecks that need addressed in order to bring your design system home.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8908bf99-19a5-45bf-998a-1a96a5667fd9/pattern-lab-2-image-15-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b81f31-4e0f-4b69-9ef2-a9b4c84a6d7d/pattern-lab-2-image-15-opt.png" alt="Pattern states cause a ripple effect that shows up throughout the interface."></a><figcaption>Pattern states cause a ripple effect that shows up throughout the interface. If the <code>media-block</code> pattern is flagged as incomplete, then any pattern that includes it will also be flagged as incomplete. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8908bf99-19a5-45bf-998a-1a96a5667fd9/pattern-lab-2-image-15-large-opt.png">Large preview</a>)</figcaption></figure>

You can <a href="https://patternlab.io/docs/pattern-states.html">create your own pattern states</a> that match your team’s workflow. These methods of understanding the state of your patterns can help larger teams keep track of the airplane as it’s being built and flown at the same time.</p>

## Maintaining An Effective Design System

<blockquote>"The biggest existential threat to any system is neglect."

– Alex Schleifer, Airbnb</blockquote>

There is a very real risk that despite your team’s best intentions, your carefully-crafted design system and pattern library will slip into oblivion. “Never!” you exclaim, but unfortunately design system efforts fall into a state of disrepair for a number of reasons:

*   The level of effort required to keep pattern code up to speed with applications’ code bases is too high
*   The pattern library is thought of as mere documentation rather than as housing a living, breathing system.
*   The team fails to make the design system a key part of their workflow, and instead lets their process devolve into a series of hotfixes and ad hoc changes.
*   One discipline serves as gatekeepers to the pattern library, preventing it from becoming a helpful resource for every discipline
*   The pattern library isn’t visible or attractive
*   Many other factors (lack of funding, technology mismatches, lack of governance model, and more)

As Nathan Curtis <a href="https://medium.com/eightshapes-llc/a-design-system-isn-t-a-project-it-s-a-product-serving-products-74dcfffef935">rightly says</a>, making a design system isn’t just another project, but rather a product meant to serve your organization’s sites and apps. To create a system that serves your organization for years to come, your UI design system needs to be properly <a href="https://atomicdesign.bradfrost.com/chapter-5/">maintained</a>, serve as an essential resource for the organization to keep coming back to, and continue to be a core part of your team’s design and development workflow.

Pattern Lab has always been an effective tool for <em>creating</em> UI design systems, but has historically lacked in the <em>maintenance</em> department. Thankfully, that’s all changed with Pattern Lab 2. The new version has many features that helps you successfully document and maintain your pattern libraries while continuing to serve as a key tool in your pattern-driven design and development process.</p>

### Seeking the Holy Grail

It’s critical to reduce the amount of effort and friction required to keep both your pattern library and production environments up to date. The <a href="https://atomicdesign.bradfrost.com/chapter-5/#in-search-of-the-holy-grail">Holy Grail of design systems</a> is an environment where changes to patterns in a design system are automatically updated in both the pattern library and production environments.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c023870-8b32-447b-847d-b47b1b8a9f64/pattern-lab-2-image-16-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886e1c37-07f2-45ab-9cf4-89c74d716c26/pattern-lab-2-image-16-opt.png" alt="With a Holy Grail setup, changes to the design system are automatically updated in both production environments and the pattern library." /></a><figcaption>With a Holy Grail setup, changes to the design system are automatically updated in both production environments and the pattern library. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c023870-8b32-447b-847d-b47b1b8a9f64/pattern-lab-2-image-16-large-opt.png">Large preview</a>)</figcaption></figure>

The Holy Grail is often accomplished by using a frontend templating language to serve as the bridge between your pattern library and production environments. Pattern Lab 2’s architecture now makes it possible to choose the templating engine that’s right for your particular environment. As a result, you’re able to get closer to achieving the Holy Grail. For instance, the team at Phase2 Technology <a href="https://www.phase2technology.com/blog/introducing-pattern-lab-starter-8/">have successfully integrated Pattern Lab 2 into their Drupal builds</a> so that their clients’ pattern libraries and production builds are always in step with one another.
<blockquote>"By using the same templating engine, along with the help of the Component Libraries Drupal Module, the tool gives Drupal the ability to directly include, extend, and embed the Twig templates that Pattern Lab uses for its components without any template duplication at all!"

– Evan Lovely, Phase2 Technology</blockquote>

Currently Pattern Lab 2 supports the popular <a href="https://mustache.github.io/">Mustache</a> and <a href="https://twig.sensiolabs.org/">Twig</a> templating engines, but the decoupled nature of Pattern Lab 2’s editions (more on these in a bit) means that you can power Pattern Lab using the templating engine of your choice.</p>

### A Helpful Resource

Your pattern library and accompanying style guide should be something that your team comes back to reference again and again. While it may not make sense to immediately surface code snippets and pattern usage information during the initial design and development process, design system users will find themselves reaching for these things as they apply the design system to actual applications. Pattern Lab 2 now has more advanced config options that let you <a href="https://github.com/pattern-lab/patternlab-node/wiki/Configuration#defaultshowpatterninfo">switch on pattern info by default</a> to become a more helpful documentation and reference tool.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19fe7e5a-5115-428a-a95e-25ae93470402/pattern-lab-2-image-17-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18a0580d-e2f3-4f38-9d33-3ab5d2041ea9/pattern-lab-2-image-17-opt.png" alt="You can configure Pattern Lab to display or hide pattern info by default. At the beginning of a project, documentation might make sense to be tucked away, but once the design system is established it may make sense to surface that info." /></a><figcaption>You can configure Pattern Lab to display or hide pattern info by default. At the beginning of a project, documentation might make sense to be tucked away, but once the design system is established it may make sense to surface that info. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19fe7e5a-5115-428a-a95e-25ae93470402/pattern-lab-2-image-17-large-opt.png">Large preview</a>)</figcaption></figure>

In order for your design system to thrive across your entire organization, it should be <a href="https://atomicdesign.bradfrost.com/chapter-5/#make-it-approachable">approachable</a> and attractive. Pattern Lab 2 allows you to <a href="https://github.com/pattern-lab/patternlab-node/wiki/Configuration#defaultpatttern">create your own custom front page</a> for the component library, and also skin Pattern Lab’s (intentionally bare bones) default UI to better serve your brand.</p>

## Doing It All Again

There are some teams that need only to set up and maintain a single design system, but many of us work on multiple projects for multiple clients. Wouldn’t it be great to start new design system projects from a setup that’s tuned to your workflow and tool choices?

Pattern Lab 2 has been re-architected to achieve just that. No longer is Pattern Lab a standalone tool, but rather it’s an ecosystem built atop a core library. These changes will also make it easier for the Pattern Lab team to push out new features.</p>

### Pattern Lab Editions

Editions let teams and agencies bundle all the things that support their unique workflows with Pattern Lab. An Edition can become the starting point for all of your projects while teams share and update functionality. The Node version of Pattern Lab uses <a href="https://www.npmjs.com/">npm</a> to pull in separate components, while PHP version uses <a href="https://getcomposer.org/">Composer</a> to help you kick off your projects in a simple and standardized way.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a94b28a-7a20-4ff4-ae9f-e97ccee57340/pattern-lab-2-image-18-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bf96b04-cf5a-415f-bbc1-3bd1f1e3fc8b/pattern-lab-2-image-18-opt.png" alt="A Pattern Lab Edition consists of Pattern Lab’s core code, a PatternEngine containing your prefered templating engine, a StyleguideKit that is Pattern Lab’s frontend code, and a StarterKit, which includes the default patterns and frontend code you want to include inside Pattern Lab by default." /></a><figcaption>A Pattern Lab Edition consists of Pattern Lab’s core code, a PatternEngine containing your prefered templating engine, a StyleguideKit that is Pattern Lab’s frontend code, and a StarterKit, which includes the default patterns and frontend code you want to include inside Pattern Lab by default. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a94b28a-7a20-4ff4-ae9f-e97ccee57340/pattern-lab-2-image-18-large-opt.png">Large preview</a>)</figcaption></figure>

### Pattern Lab Core

Core is the guts of Pattern Lab and enables all of the other features. Because Core is standalone a team can update and stay current with the latest Pattern Lab features without disrupting the rest of their project.</p>

### StarterKits

Have a trusty set of boilerplate code that you start every project with? Perhaps a common set of basic patterns, Sass mix-ins, and JavaScript libraries that are your go-to tools? A StarterKit is perfect for bundling these assets together into a boilerplate that makes sure each project starts off on the right foot.</p>

<a href="https://github.com/pattern-lab/?utf8=%E2%9C%93&amp;query=starterkit-mustache">Several starterkits</a> alreadyexist to kick your project off, whether you’re looking for a blank start, begin with a demo that showcases Pattern Lab’s features, or start with a popular framework like Bootstrap, Foundation, or Material Design. And you can roll your own, which can be fully version-controlled so your team’s StarterKit can evolve along with your tools.</p>

<a href="https://github.com/pattern-lab/patternlab-node/wiki/Importing-Starterkits">Importing a starterkit</a> is only a few keystrokes away after installation. Eventually this feature will be built into a post-install phase like it is for Pattern Lab PHP via composer.</p>

### StyleguideKits

StyleguideKits are the front-end of Pattern Lab. We call this “The Viewer.” StyleguideKits allow agencies and organizations to develop custom, branded Pattern Lab UIs to show off their patterns.</p>

### PatternEngines

PatternEngines are the templating engines that are responsible for parsing patterns and turning them into HTML. PatternEngines give Pattern Lab Core the flexibility to render many different types of template languages. Current PatternEngines include Mustache and Twig, with others like Handlebars and Underscore in development. And there’s no stopping you from adding another templating engine to Pattern Lab.</p>

### Plugins

Plugins allow developers to extend Pattern Lab Core and other parts of the ecosystem. For example, the PHP version of Pattern Lab has a number of plugins like <a href="https://github.com/pattern-lab/plugin-php-reload">Browser Auto-Reload</a>, <a href="https://github.com/pattern-lab/plugin-php-data-inheritance">Data Inheritance</a>, and <a href="https://github.com/pattern-lab/plugin-php-faker">Faker</a>. Pattern Lab’s architecture allows developers to modify data at different stages, add their own commands or pattern rules, or change the front-end to modify and extend Pattern Lab’s capabilities

## Watch My Talk

<figure class="fwi"><div style="position:relative;height:0;padding-bottom:56.25%"><iframe loading="lazy" src="https://www.youtube.com/embed/wcAl0VXYBGE?ecver=2" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></figure></figure>

## Give Pattern Lab 2 A Try, And Get Involved

Creating pattern-driven user interfaces and sophisticated design systems is more important than ever. Pattern Lab 2 is well equipped to create and maintain atomic design systems, and can serve as a hub for your design system through every step of your team’s workflow.

If your team decides to <a href="https://patternlab.io/">download Pattern Lab 2</a> and give it a try, we’d love to hear from you! Join the conversation by asking questions on <a href="https://gitter.im/pattern-lab">Gitter</a>, open <a href="https://github.com/pattern-lab/">issues</a> if you’re struggling with something, and help <a href="https://github.com/pattern-lab/the-spec">propose &amp; discuss</a> new features.

And if you make cool things with Pattern Lab 2, please share your insights! <a href="https://styleguides.io">Styleguides.io</a> has over 150+ <a href="https://styleguides.io/examples.html">examples</a> of pattern libraries, so add your Pattern Lab to the mix. The beauty of the web and open source projects is that the entire community can learn from your experience and build upon that knowledge.

We’re excited to see what great things you create!

{{< signature "vf, il" >}}

