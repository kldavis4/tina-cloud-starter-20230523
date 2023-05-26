---
title: "Progress Trackers in Web Design: Examples and Best Practices"
slug: progress-trackers-in-web-design-examples-and-best-design-practices
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70d8c2cf-3fb5-49aa-8c0a-7bb369c1abac/trackers.jpg
date: 2010-01-15T10:52:16.000Z
author: tom-kenny
summary: >-
  In this article, we will look at various uses of progress trackers and see how they’ve been implemented, what they are doing well, and what they are not doing well.
description: >-
  In this article, we will look at various uses of progress trackers and see how they’ve been implemented, what they are doing well, and what they are not doing well.
categories:
  - Inspiration
  - Showcases
  - Web Design
---

When designing a large website, especially one that contains a store, you may be required to design a system for ordering online, or a multi-step process of another sort. Walking users through this process by making it easy and intuitive is key to helping increase conversion rates. Any frustration along the way may cause them to leave and pursue other options. **Progress trackers** are designed to help users through a multi-step process and it is vital that such trackers be well designed in order to keep users informed about what section they are currently on, what section they have completed, and what tasks remain.

## What are Progress Trackers?

You may not be familiar with the term ’progress tracker’, also called a ’progress indicator’ &mdash; but chances are good that you have encountered one at one time or another. They are used in online stores when placing an order, signing up to an online product or service, or even when booking a holiday online. Progress trackers guide the user through a number of steps in order to complete a specified process.

<figure>
  <a href="https://www.game.co.uk/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8a03185-fbbe-47f2-bf18-753ff84b0fd5/game-pr.gif" alt="Progress Tracker Example" width="548" height="54" />
  </a>
  <figcaption>An example of a progress tracker at <a href="https://www.game.co.uk">Game</a>
  </figcaption>
</figure>

## The Difference Between Progress Trackers and Breadcrumbs

As we have detailed previously in [Breadcrumbs In Web Design: Examples And Best Practices](https://www.smashingmagazine.com/2009/03/17/breadcrumbs-in-web-design-examples-and-best-practices-2/), breadcrumbs are a way of enhancing navigation by revealing a user’s current location. Initially, breadcrumbs and progress trackers may seem very similar and in many ways they are, however, there are significant differences.

Breadcrumbs show you only where you have been (or what sections are above the current section in the application’s hierarchy), whereas progress trackers indicate a set path that a user follows to complete a specific task. Progress trackers show you not only where you are currently located, but also what steps you have previously taken, and what steps you are about to take.

<figure>
  <a href="https://coolspotters.com/musicians/michael-jackson/and/albums/thriller">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2306b0ff-f6eb-4f62-9101-db5bd63b98cb/breadcrumbs-pr.gif" alt="Breadcrumbs Example" width="550" height="31" />
  </a>
  <figcaption>Example of breadcrumbs at <a href="https://coolspotters.com">Coolspotters</a>
  </figcaption>
</figure>

Progress trackers are best used when there is a specific goal to achieve. They are synonymous with conversion and are used as a way of improving usability — which is key when [optimizing conversion rates](https://www.smashingmagazine.com/2009/05/15/optimizing-conversion-rates-its-all-about-usability/). Conversion is all about selling online so you will see a progress tracker in some form in almost every online store.

Now that we’ve reviewed what a progress tracker is, let’s look at situations that would require or even benefit from the implementation of a well-designed progress tracker.

{{% feature-panel %}}

## Uses of Progress Trackers

As mentioned previously, progress trackers can be used in a variety of contexts. The following three are the most common.

**1. Online Ordering**
By far the most common application of progress trackers is in conjunction with online purchasing, since this usually involves multiple steps.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c9c1ce6-9aaf-40af-a70f-1d94b34f0638/hmv-pr.gif" alt="HMV Online Order Progress Tracker" width="577" height="33" />
  <figcaption>The progress tracker used by HMV.
  </figcaption>
</figure>

<figure>
  <a href="https://www.etsy.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc23de15-7cf4-4702-b1d3-a1def5b27e80/etsy-pr.gif" alt="Etsy Progress Tracker" width="396" height="36" />
  </a>
  <figcaption>The progress tracker used at <a href="https://www.etsy.com">Etsy</a>.
  </figcaption>
</figure>

**2. Feature Tour Guides**
Progress trackers are also used to guide users through the features of online products and services, as demonstrated in the following examples:

<figure>
  <a href="https://searchinsidevideo.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a56e8531-90bf-49da-87b4-f644abb1d9be/searchinsidevideo-pr.gif" alt="Search Inside Video’s Progress Tracker" width="488" height="48" /></a>
  <figcaption>Progress tracker as used by <a href="https://searchinsidevideo.com">Search Inside Video</a>.
  </figcaption>
</figure>

<figure>
  <a href="https://www.flickr.com/tour/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d389da07-0fe5-41ff-96b9-0d6c2c9bd139/flickr.jpg" alt="Flickr’s tour page" width="596" height="43" /></a>
  <figcaption>
    <a href="https://www.flickr.com/tour/">Flickr’s tour page</a> provides a look at the features of their service.
  </figcaption>
</figure>

**3. Multi-Step Forms**
If a form requires a lot of user input, it may be best to split the form into multiple steps.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b416834-8bd9-4062-9659-b6fb3ae3a2a1/livestream-pr.gif" alt="Livestream’s Channel Creation Form" width="375" height="41" />
  <figcaption>Livestream’s progress tracker design.
  </figcaption>
</figure>

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbd5028a-51b3-4f5c-b224-57419b904006/buffalo-pr.gif" alt="Buffalo’s Project Planner Form" width="559" height="259" />
  <figcaption>The progress tracker used on Buffalo’s Project Planner form
  </figcaption>
</figure>

## Best Practices in Progress Tracker Design

**Indicating a Logical Progression**
Most progress trackers are designed to display the steps from left to right. In most lands, people read from left to right, so it makes sense that progress trackers follow that pattern. That isn’t enough though — there has to be something that informs the user that they are performing a multi-step process.

<figure>
  <a href="http://www.blockbuster.com">
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d340f2-a5ca-4e88-9d6d-f5e0905dd493/blockbuster-pr.gif" alt="Blockbuster’s progress tracker" width="598" height="29" /></a>
  <figcaption><a href="http://www.blockbuster.com">Blockbuster</a> have included both arrows and numbers in their progress </figcaption>tracker, thus clearly communicating a logical progression.
</figure>

**Keeping the User Informed of their Location**
One key aspect of good progress tracker design is keeping the user informed of where the user is in the process. This complements the logical progression because the user will know where they are in relation to where they have been, and what sections are to follow.

<figure>
  <a href="https://www.mrandmrssmith.com/">
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad0a1121-2372-4b00-96da-8a7cd4340624/mrandmrssmith-pr.gif" alt="Urban Original’s progress tracker" width="600" height="36" /></a>
  <figcaption><a href="https://www.mrandmrssmith.com/">Mr and Mrs Smith</a> indicates the user’s current location by </figcaption>clearly highlighting the current step and turning the arrow downwards.
</figure>

**Positioning**
Since progress trackers are a form of navigation, it is best to place them below the primary and secondary navigation (such as breadcrumbs) and above the content that the progress tracker relates to. Also, while a progress tracker can act as a page title, it is best to place the title of the current section underneath the progress tracker, to reinforce the current location.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6abb9b36-cadf-462f-b4e2-94bb91bb7cd0/gamestation.jpg" alt="Gamestation’s progress tracker" width="600" height="241" />
  <figcaption>Gamestation places their progress </figcaption>tracker clearly below the primary and secondary navigation.
  </figure>

{{% ad-panel-leaderboard %}}

## Implementations of Progress Trackers

**Plain Text**
Below is an example of a plain text progress tracker on [Media Temple’s website](https://mediatemple.net). One benefit of a plain text progress tracker is that it can be edited easily.

<figure>
  <a href="https://mediatemple.net"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/686e4014-1e3d-4fbb-9483-6475afd7dd7f/mediatemple-pr.gif" alt="Media Temple’s Progress Tracker" width="485" height="45" /></a>
</figure>

### Sprite-Based

[Sovereign](https://www.sovereign.com) uses the popular CSS sprites technique to build their progress tracker and reduce HTTP requests going through the online booking process.

<figure>
  <a href="https://www.sovereign.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fba1e244-0abb-4d7d-9650-62a7029d1ae8/sovereign-pr.gif" alt="Sovereign sprite image" width="518" height="240" /></a>
</figure>

## Design Mistakes to Avoid

**Indistinguishable from Breadcrumbs**
TypePad’s Design Assistant can be very easily confused with a breadcrumb navigation system.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35da0751-b337-4988-bbca-432e83c2347a/typepad.jpg" alt="TypePad Design Assistant" width="560" height="60" /></a>
</figure>

### Not Enough Information

[easyJet](https://easyjet.com)’s old progress tracker on their booking path was poorly executed. Although it gave you the total number of steps in the process, it didn’t indicate which steps you’ve completed or which were remaining.

<figure>
  <a href="https://easyjet.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bccb7a2-785b-4023-8bf0-be07248f7f0b/easyjet-pr.gif" alt="easyJet’s Old Booking Path" width="389" height="91" />
  </a>
</figure>

Their new progress tracker, launched within the last few weeks, is a big improvement, indicating current location, past steps, and steps to come. They now also make good use of the page title which has descriptive wording to complement the current progress tracker label.

<figure>
  <a href="https://easyjet.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52989631-add0-48b6-a644-8adc181dd767/easyjetnew-pr.gif" alt="Easyjet’s New Booking Path" width="515" height="81" />
  </a>
</figure>

### No Sense of Progression

[daniblack](https://www.daniblack.com) incorrectly uses a tab system for their progress tracker. The problem with this is that tabs don’t offer any visual representation of progress. The addition of numbers or arrows would give at least some sort of indication of progression in this example.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28aef6e4-15fe-4366-94aa-94a633ae0127/daniblack-pr.gif" alt="Progress tracker on daniblack" width="600" height="49" />
</figure>

{{% ad-panel-leaderboard %}}

## Progress Tracker Showcase

Now that we know what a progress tracker is, how it is used, and the best approach to its design, let’s look at a number of well-designed progress trackers currently in use.

[Battle.net](https://battle.net) uses the method of incrementally filling a bar as you progress through the steps in their sign-up form.

<figure>
  <a href="https://battle.net">
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/173075d0-3ceb-4035-a6df-8d4b37656f5c/battlenet.jpg" alt="Battle.net’s progress tracker" width="413" height="54" />
  </a>
</figure>

[Ikea](https://www.ikea.com)

<figure>
  <a href="https://www.ikea.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffb98b7e-26b9-45bf-8f47-014d951762b2/ikea-pr.gif" alt="Ikea’s progress tracker" width="600" height="60" />
  </a>
</figure>

[Amazon](https://www.amazon.com/) has a shopping trolley travelling across their progress tracker, leaving an orange line marking where it has been.

<figure>
  <a href="https://www.amazon.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fdf2528-2541-4f8b-9a14-71a32c1b0de3/amazon-pr.gif" alt="Amazon’s progress tracker" width="427" height="39" />
  </a>
</figure>

[Threadless](https://www.threadless.com/)

<figure>
  <a href="https://www.threadless.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdcabb5c-04d2-4505-939f-1b8c930010f5/threadless-pr.gif" alt="Threadless’ progress tracker" width="280" height="54" />
  </a>
</figure>

[Urban Originals](https://www.uo.com.au/)

<figure>
  <a href="https://www.uo.com.au/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dab7d24-05bc-48c1-b2ff-3d850b094262/urbanoriginals-pr.gif" alt="Urban Original’s progress tracker" width="594" height="35" />
  </a>
</figure>

[Firebox](https://firebox.com/)

<figure>
  <a href="https://firebox.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5634686-1a8a-4b28-b617-4721d020679a/firebox-pr.gif" alt="Firebox’s progress tracker" width="580" height="35" />
  </a>
</figure>

[Apple](https://www.apple.com/)

<figure>
  <a href="https://www.apple.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e52743-d464-472b-a407-12a93e9c7887/apple-pr.gif" alt="Apple’s progress tracker" width="593" height="40" />
  </a>
</figure>

[Vitradirect](https://www.vitradirect.com/)

<figure>
  <a href="https://www.vitradirect.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1e82b46-3f0f-41b3-8de0-f448a47aafbd/vitradirect-pr.gif" alt="Vitradirect’s progress tracker" width="576" height="65" />
  </a>
</figure>

[CafePress](https://www.cafepress.co.uk/)

<figure>
  <a href="https://www.cafepress.co.uk/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c6d1ff3-6386-497f-822f-4d18efd1692c/cafepress-pr.gif" alt="CafePress’s progress tracker" width="600" height="34" />
  </a>
</figure>

[Topshop](https://www.topshop.com/)

<figure>
  <a href="https://www.topshop.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0293d908-b074-4e47-8eb8-ad4037377c57/topshop-pr.gif" alt="Topshop’s progress tracker" width="501" height="30" />
  </a>
</figure>

[John Lewis](https://johnlewis.com/) uses an image of a truck travelling along their progress tracker.

<figure>
  <a href="https://johnlewis.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd9fbb2-9868-40e8-8d9f-c176e8892723/johnlewis-pr.gif" alt="John Lewis’s progress tracker" width="600" height="76" />
  </a>
</figure>

[Comet](https://comet.co.uk/) ticks off sections that have already been completed.

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd8b08f5-d518-4f94-89bd-c28ee081c2fd/comet-pr.gif" alt="Comet’s progress tracker" width="561" height="29" />
</figure>

[Boots](https://www.boots.com/)’ Progress tracker spans the width of the page.

<figure>
  <a href="https://www.boots.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/954681ca-bb68-4be1-9bf7-26124f0a59a2/boots-pr.gif" alt="Boots’ progress tracker" width="600" height="29" />
  </a>
</figure>

[Web MD](https://www.webmd.com/diet/weight-loss-surgery/weight-loss-surgery-health-check/default.htm) uses a progress bar and percentage values as a way of tracking progress on their health check questionnaires.

<figure>
  <a href="https://www.webmd.com/diet/weight-loss-surgery/weight-loss-surgery-health-check/default.htm">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d88549c6-b6b0-4e77-bc9c-85b682ebd04c/webmd-pr.gif" alt="Web MD’s progress tracker" width="582" height="19" />
  </a>
</figure>

[Argos](https://www.argos.co.uk/)

<figure>
  <a href="https://www.argos.co.uk/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f3e9b01-d7c2-43c0-8d03-b9e6d3190335/argos-pr.gif" alt="Argos’ progress tracker" width="600" height="60" />
  </a>
</figure>

[Altrec](http://www.altrec.com/)

<figure>
  <a href="http://www.altrec.com/">
    <img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/wp-content/uploads/2009/10/altrec_pr.gif" alt="Altrec’s progress tracker" width="490" height="56" />
  </a>
</figure>

[SurfRide](https://www.surfride.com)

<figure>
<a href="https://www.surfride.com">
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a56c10be-c545-42da-a35c-8324e044dea9/surfride-pr.gif" alt="SurfRide’s progress tracker" width="535" height="51" />
  </a>
</figure>

[Zumiez](https://www.zumiez.com)

<figure>
  <a href="https://www.zumiez.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/649fb651-43dd-42e0-95b0-3b29dab86fc4/zumiez-pr.gif" alt="Zumiez’s progress tracker" width="600" height="24" />
  </a>
</figure>

[Toys"R"Us](https://www.toysrus.com/)

<figure>
  <a href="https://www.toysrus.com/">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6cbc5f2-1ca6-4ed7-a557-00270a4fd042/toysrus-pr.gif" alt="Toys&quot;R&quot;Us’ progress tracker" width="599" height="58" />
  </a>
</figure>

[eBags](https://www.ebags.com)

<figure>
  <a href="https://www.ebags.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6aa1f5af-6965-4c2c-883f-3358500c064e/ebags-pr.gif" alt="eBags’ progress tracker" width="514" height="42" />
  </a>
</figure>

[Foot Locker](https://www.footlocker.com)

<figure>
  <a href="https://www.footlocker.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05927117-831c-4a5c-b7b4-acca0453e20f/footlocker-pr.gif" alt="Foot Locker’s progress tracker" width="600" height="29" />
  </a>
</figure>

[The Ultimate Green Store](https://www.theultimategreenstore.com)

<figure>
  <a href="https://www.theultimategreenstore.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa6a714-b604-47f3-8993-d68134301b3e/theultimategreenstore-pr.gif" alt="The Ultimate Green Store’s progress tracker" width="540" height="25" />
  </a>
</figure>

[Crate and Barrel](https://www.crateandbarrel.com)

<figure>
  <a href="https://www.crateandbarrel.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f8955f5-ca50-47f8-90c6-42164419614f/crateandbarrel-pr.gif" alt="Crate and Barrel’s progress tracker" width="516" height="37" />
  </a>
</figure>

[American Apparel](https://www.americanapparel.com)

<figure>
  <a href="https://www.americanapparel.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eee45fa-740e-4dcd-b711-021570c72836/americanapparel-pr.gif" alt="American Apparel’s progress tracker" width="575" height="22" />
  </a>
</figure>

[PC World](https://www.pcworld.co.uk)

<figure>
  <a href="https://www.pcworld.co.uk">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f95a522f-36a9-4a07-b550-64018db77937/pcworld-pr.gif" alt="PC World’s progress tracker" width="552" height="23" />
  </a>
</figure>

[Abel &amp; Cole](https://www.abelandcole.co.uk)

<figure>
  <a href="https://www.abelandcole.co.uk">
    <img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/wp-content/uploads/2009/10/abelandcole_pr.gif" alt="Abel and Cole’s progress tracker" width="600" height="57" />
  </a>
</figure>

[Ecco USA](http://www.eccousa.com)

<figure>
  <a href="http://www.eccousa.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5182deb-ae79-46de-9331-fbfae1525908/ecco-pr.gif" alt="Ecco USA’s progress tracker" width="291" height="28" />
  </a>
</figure>

[Design Public](https://www.designpublic.com)

<figure>
  <a href="https://www.designpublic.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1eb5a26-6a63-4a02-8d57-9e247194fe1f/designpublic-pr.gif" alt="Design Public’s progress tracker" width="333" height="34" />
  </a>
</figure>

[PETCO](https://www.petco.com)

<figure>
  <a href="https://www.petco.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1741158-08d7-4c96-ad00-99c74fed462d/petco-pr.gif" alt="PETCO’s progress tracker" width="375" height="18" />
  </a>
</figure>

[Football Fanatics](https://www.footballfanatics.com)

<figure>
  <a href="https://www.footballfanatics.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8b88b14-c258-4674-95c5-ed98c493525a/footballfanatics-pr.gif" alt="Football Fanatics’ progress tracker" width="357" height="34" />
  </a>
</figure>

[The Habitat Company](https://www.habitat.com)

<figure>
  <a href="https://www.habitat.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1194cf9f-4de0-4062-b0dc-15c0d60a741a/habitat-pr.gif" alt="The Habitat Company’s progress tracker" width="600" height="28" />
  </a>
</figure>

[Walton Garden Buildings](https://www.waltons.co.uk)

<figure>
  <a href="https://www.waltons.co.uk">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20b3a19c-3bfe-4b22-80c6-885e8bbaf400/walton-pr.gif" alt="Walton Garden Buildings’ progress tracker" width="600" height="48" />
  </a>
</figure>

[lookfantastic](https://www.lookfantastic.com) uses icons to visually enhance their progress tracker.

<figure>
  <a href="https://www.lookfantastic.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8510c9fa-7e6b-4a82-9260-913905551345/lookfantastic-pr.gif" alt="lookfantastic’s progress tracker" width="337" height="58" />
  </a>
</figure>

[B&amp;Q](https://www.diy.com)

<figure>
  <a href="https://www.diy.com">
    <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a83a8fa-dd40-4fc7-b49c-5c41dce00071/bq.gif" alt="B&amp;Q’s progress tracker" width="600" height="36" />
  </a>
</figure>

## Further Reading on SmashingMag:

You may be interested in the following related posts:

- [Showcase Of Modern Navigation Design Trends](https://www.smashingmagazine.com/2010/01/04/showcase-of-modern-navigation-design-trends/)
- [Designing “Coming Soon” Pages](https://www.smashingmagazine.com/2009/11/10/designing-coming-soon-pages/)
- [Call to Action Buttons: Examples and Best Practices](https://www.smashingmagazine.com/2009/10/13/call-to-action-buttons-examples-and-best-practices/)
- [Search Results Design: Best Practices and Design Patterns](https://www.smashingmagazine.com/2009/09/28/search-results-design-best-practices-and-design-patterns/)

{{< signature "lu, il" >}}
