---
title: 10 Requirements For Making Home Page Carousels Work For End Users (If Needed)
slug: ten-requirements-for-making-home-page-carousels-work-for-end-users
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93f79a7-c9ea-47d8-b88c-c4ed774a543c/1-williams-sonoma-opt.png
date: 2016-07-06T16:05:40.000Z
author: christian-holst
summary: >-
  Are home page carousels actually helpful to users? Or are they simply popular because they are an easy tool for solving internal discussions in large organizations about who gets to put their banner on the home page? The short answer is that home page carousels *can* work, but in practice the vast majority of implementations perform poorly with end users.
description: >-
  Are home page carousels actually helpful to users? Or are they simply popular because they are an easy tool for solving internal discussions in large organizations about who gets to put their banner on the home page? The short answer is that home page carousels *can* work, but in practice the vast majority of implementations perform poorly with end users.
categories:
  - UX
  - Usability
  - Design Patterns
  - Web Design
  - Best Practices
---
At the Baymard Institute, we’ve conducted large-scale usability tests for the past seven years of both desktop and mobile e-commerce websites. The tests show that home page carousels *can* perform decently with end users *if* they adhere to 10 implementation requirements. As importantly, implementation should differ from desktop to mobile.

Note that these findings deviate slightly from the more black-and-white answer of “never use a carousel” that you’ll often get on websites such as *[Should I Use A Carousel?](https://shouldiuseacarousel.com)*.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/223b0c4e-f43c-4bf3-ad74-0b6e875d2474/1-williams-sonoma-large.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93f79a7-c9ea-47d8-b88c-c4ed774a543c/1-williams-sonoma-opt.png" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/223b0c4e-f43c-4bf3-ad74-0b6e875d2474/1-williams-sonoma-large.png">View large version</a>)</figcaption></figure>

Now, let me underscore that user testing has not shown that even a perfectly implemented carousel is a “home page savior” that will positively disrupt performance like no other design. There are alternatives to a home page carousel that both perform well and are vastly easier to implement (we’ll present the best one at the end of the article).

Considering that most carousel implementations (including ones created by several plugins) lack many of these 10 usability details (making them downright harmful to the UX), one can understand why strong wording is often used in discussions about carousels. But saying that home page carousels should never be used doesn’t fully align with our seven years of large-scale usability testing — at least in an e-commerce context.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [An Exploration Of Carousel Usage On Mobile E-Commerce Websites](https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/)
*   [Dropbox’s Carousel Design Deconstructed](https://www.smashingmagazine.com/2014/08/dropbox-carousel-design-deconstructed-part-1/)
*   [A Definitive Guide To The Android Carousel Design Pattern](https://www.smashingmagazine.com/2013/02/android-carousel-design-pattern/)
*   [How To Poison The Mobile User](https://www.smashingmagazine.com/2016/10/how-to-poison-the-mobile-user/)

In this article, then, we’ll go over the 10 implementation details we’ve found that are required to make home page carousels perform acceptably with end users. We’ll outline how and why mobile and desktop implementations should differ and, lastly, suggest a simpler, problem-free alternative to home page carousels.

(If you don’t have the resources to implement all 10 requirements, then our recommendation would align with that of most others: Don’t use a home page carousel, but rather use the alternative design suggested at the end.)

{{% feature-panel %}}

## Home Page Carousels In Practice

<p>Carousels are hugely popular on e-commerce websites — especially on the home page. In fact, the “<a href="https://baymard.com/homepage-and-category-usability/benchmark/site-reviews">Homepage &amp; Category</a>” benchmark we conducted of 50 top-grossing US e-commerce websites reveals that 52% of e-commerce websites have a carousel on their desktop home page. Our “<a href="https://baymard.com/mcommerce-usability/benchmark/mobile-site-reviews">Mobile E-Commerce</a>” usability benchmark reveals that carousels are equally popular on mobile websites: 56% of mobile e-commerce websites have one on the home page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff15cde-65b3-4ee0-b1a3-ef1e9b37dfed/2-drugstore-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50ce8ea3-923b-448a-ab54-59b0410ecfab/2-drugstore-opt.jpg" /></a><figcaption>Carousels can only ever be as good as their content. “Whoa, that’s some pretty aggressive ads they show here,” a test subject complained when landing on <a href="https://baymard.com/ecommerce-search/benchmark/site-reviews/195-drugstore-com">Drugstore.com</a>. “This disturbs my concentration.” In particular ad-looking content is problematic and doesn’t take advantage of the carousel’s main strength of setting a good visual first impression. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff15cde-65b3-4ee0-b1a3-ef1e9b37dfed/2-drugstore-large.jpg">View large version</a>)</figcaption></figure>

I should stress that the focus of this article is not on carousel content itself, but rather on how to make a home page carousel more user-friendly through design and interactive features. If the content of a carousel isn’t relevant, well curated and of high quality, then the user experience will be bad, regardless of how optimized the interface and logic are. And if the content looks like advertising, our testing and eye-tracking studies reveal that most users will simply ignore the content due to banner blindness, regardless of how relevant it might be to them.

One of the main upsides observed with home page carousels is that they are an easy way to include large and bespoke imagery. We saw during testing that large and custom images on the home page give users a good first impression of the website — increasing the time spent after landing on a new website, before they make their initial snap judgement of whether to stay or leave. In other words, we see that large bespoke imagery often reduces home page bounce rates while also reflecting positively on the website and brand.

With that being said, we also observed how implementation details can quickly turn a carousel into a frustrating and potentially harmful user experience. In this article, we’ve divided the 10 implementation requirements into 4 groups:

*   Slide sequence and destinations
*   Auto-rotation logic on desktop
*   Two functions of carousel controls
*   The differences on touch devices

## 1. Slide Sequence And Destinations

Most users won’t see all of the slides in a home page carousel, even one that auto-rotates. They simply don’t stick around the home page long enough, and certainly not at the top of the page.

During testing, our subjects would typically move on to another page or scroll past the carousel long before the carousel had cycled through all of the slides. And that was in the case of auto-rotating carousels — obviously, fully manual carousels revealed only the first slide, until test subjects actively changed slides.

<p>This means that the sequence of slides is important because the initial slide will get vastly more exposure than later ones. In an auto-rotating carousel, it’s not uncommon for the first slide to get more than 50% of clicks (see “Site 2” section of Erik Runyon’s “<a href="https://erikrunyon.com/2013/07/carousel-interaction-stats/">Carousel Interaction Stats</a>”). Another crucial implication is that one cannot assume that users will see any particular slide.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6fad3a8-79bc-4f63-9f76-22a51107e9c2/3-toysrus-1-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b969827-64e7-47b1-b45f-234f055e9058/3-toysrus-1-opt.jpg" /><br>
</a><figcaption>When testing the <a href="https://baymard.com/homepage-and-category-usability/benchmark/site-reviews/136-toys-r-us">Toys’R’Us</a> mobile website, the only way to access the “gift finder” was through a slide in the home page carousel. This made it extremely difficult for test subjects to find it (especially because it wasn’t the first slide), despite actively looking for it. Ultimately, the carousel’s placement ended up being a major contributor to several website abandonments. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6fad3a8-79bc-4f63-9f76-22a51107e9c2/3-toysrus-1-large.jpg">View large version</a>)</figcaption></figure>

<p>None of this is a problem in and of itself — a user not seeing all of the carousel slides isn’t an issue as long as the carousel isn’t the only way to access the website’s features and isn’t relied on to indicate the website’s <a href="https://baymard.com/blog/inferring-product-catalog-from-homepage">diversity of products</a>. However, many of the test websites in our “Homepage &amp; Category” and “Mobile E-Commerce” usability studies promoted only certain offers and website features in their carousel slides (product wizards, gift finders, etc.), which proved highly problematic because most subjects never saw those slides (having already moved on from the home page); therefore, subjects never learned about these otherwise helpful tools, despite several of them having actively looked for them. So, while promoting such features in carousel slides can be a great idea, this shouldn’t be the only way to access them.</p>

### Takeaways

*   Choose the sequence of slides carefully, putting the most important content on the first slide.
*   Use the carousel as an additional highlight of important website features and information, never as the only path to important content.

## 2. Auto-Rotation Logic On Desktop

<p>Auto-rotating a carousel spreads exposure of content across the slides and underscores that this is indeed a carousel. In fact, while manual carousels have measly click rates of 1 to 2% (the only statistic cited on <a href="https://shouldiuseacarousel.com">Should I Use A Carousel?</a>), <a href="https://erikrunyon.com/2013/07/carousel-interaction-stats/">Erik Runyon found</a> that auto-rotating carousels can be decent, with 8 to 10% click rates (see his section “Site 2”). A word of caution, though: Like any animating graphics, auto-rotation takes attention away from static content, thus setting the bar even higher for the quality and curation of the carousel’s content.</p>

If, based on these considerations, you decide that auto-rotation is appropriate, three details have proven to be crucial to performance, so much so that if you cannot adhere to them, then don’t implement auto-rotation or a carousel at all:

*   Slides shouldn’t rotate too quickly.
*   Auto-rotation should pause on hover.
*   Auto-rotation should permanently stop after any active user interaction.

### Slides Shouldn’t Rotate Too Quickly

If a carousel rotates too quickly, users will not have enough time to investigate slides of interest. This can make users feel uneasy, as they try to rush through a slide’s text before it rotates. Of course, auto-rotating too slowly will have the opposite effect, boring users with slides that are of little interest to them.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6312b192-33ee-4aeb-9e59-03a845b4fdcf/4-pottery-barn-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0a3426e-0468-4a77-8627-9e4855e70b53/4-pottery-barn-opt.jpg" /></a><figcaption>While test subjects adored the large beautiful imagery in Pottery Barn’s home page carousel, many of them felt the slides changed too quickly, giving them too little time to inspect the content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6312b192-33ee-4aeb-9e59-03a845b4fdcf/4-pottery-barn-large.jpg">View large version</a>)</figcaption></figure>

<p>The amount of text in a slide should largely determine the duration of a slide’s visibility. If it’s just a short heading, 5 to 7 seconds proved to be appropriate in our tests, whereas longer durations were needed for more text-heavy slides. (Nielsen Norman Group recommends 1 second <a href="https://www.nngroup.com/articles/designing-effective-carousels/">per 3 words</a> for auto-rotating slides.) One consequence of this is that you might need to assign unique durations to individual slides, showing some slides longer than others.</p>

### Auto-Rotation Must Always Pause on Hover (42% Don’t)

<p>There’s often a corelation between a user’s mouse position and their focus on the page (see page 29 of “<a href="https://research.microsoft.com/en-us/um/people/ryenw/proceedings/WISI2007.pdf">Web Information Seeking and Interaction</a>,” PDF). Therefore, a slide being hovered over is certainly an indicator that the user might be interested in reading it, and the carousel should pause.</p>

An even more important reason to pause auto-rotation when the user’s mouse hovers over a slide is to prevent the carousel from rotating to the next slide just as the user clicks to open the one they want. During usability testing, we frequently observed subjects try to click on a slide, only for the carousel to auto-rotate a few milliseconds before the click, causing them to end up on an entirely different page.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/728007a9-feaf-485d-a469-485f7768fd8e/5-blue-nile-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa0d23e1-91f8-4bb2-a2bc-5ba35a960826/5-blue-nile-opt.jpg" /></a><figcaption>“If my mouse is above this, then it should really pause,” a subject explained when browsing <a href="https://baymard.com/checkout-usability/benchmark/top-100/48-blue-nile">Blue Nile</a>, “because otherwise I risk clicking the wrong slide just as it changes, like it just did, and I’ll get the wrong page. So, pause.” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/728007a9-feaf-485d-a469-485f7768fd8e/5-blue-nile-large.jpg">View large version</a>)</figcaption></figure>

If the user notices that they’ve landed on the wrong page, they’ll usually find it “a little annoying”, forcing them to go back to the home page and find the slide they wanted to open and click again. However, we’ve also seen instances where a subject didn’t realize what had happened and began browsing the unintended landing page, obviously finding it of extremely low relevance.

<p>Pausing auto-rotation on hover is crucial, therefore, to avoid sending users on detours or potentially even misleading them. Unfortunately, in our <a href="https://baymard.com/homepage-and-category-usability/benchmark/page-types/homepage">home page benchmarking</a>, we found that, of the desktop e-commerce websites that have a home page carousel, 42% currently do not pause auto-rotation when the user hovers with their mouse.</p>

Auto-rotation may resume once the user’s mouse leaves the slide (i.e. is no longer hovering over the carousel), assuming that the user hasn’t otherwise interacted with the carousel.

### Auto-Rotation Should Permanently Stop After Any Active User Interaction

If the user has interacted with the carousel beyond hovering over it (for example, by actively changing a slide using the carousel’s controls), then auto-rotation should permanently stop — even when the user isn’t hovering.

When a user actively changes a slide by clicking the carousel’s next or previous button or slide indicator, the selection is likely to be intentional and should not be changed if the user decides to check out other parts of the home page, before (potentially) returning to their selected slide.

A click is fundamentally different from a hover, which at best can be used to gauge user focus. A click is an active user request and is a strong indicator of interest and intent. Therefore, permanently stop auto-rotation once the user actively interacts with the carousel, because they might have intentionally set the carousel to a particular slide.

## 3. Carousel Controls Need To Perform Two Functions

Clear controls help users to contextualize a carousel’s content and stay in control. During testing, we saw that slider controls must perform two functions: indicate the current slide among the set, and allow users to navigate back and forth. A surprisingly large number of slider designs do only one of these.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fabbb69-7973-424f-bad4-ac4c0ef3f6e4/6-officedepot-large.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ce3deef-d912-4034-b7c6-db8c3e85b497/6-officedepot-opt.png" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fabbb69-7973-424f-bad4-ac4c0ef3f6e4/6-officedepot-large.png">View large version</a>)</figcaption></figure>

Indicating the current slide among the set was observed to serve several purposes:

*   It indicates that there are additional slides beyond the current one, helping to communicate that this is a carousel with more content. This supports the user’s exploration of subsequent slides.
*   It indicates how many slider the carousel contains. We’ve seen that users are more likely to look through an entire carousel when they are told up front how much content there is.
*   It indicates that the carousel has hit the last slide and is cycling back to the beginning.

The conventional way to indicate slides is with a series of dots. A word of caution on the design and placement of the dots: Laying small dots over top a large colorful image will usually cause discoverability issues. Placing the dots outside of the image slides is the easiest way to avoid contrast issues.

The second component of slider controls enables users to go back and forth between slides. The conventional design is simple arrows. However, we’ve observed that arrow controls are overlooked by users, due to a combination of being too small and not contrasting well enough when laid over a colorful image. Therefore, ensure that next and previous controls are of a decent size and that contrast is sharp enough.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d41c4daa-ed19-472b-9ec0-2258f97e8f4a/7-nike-large-84x84.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51f855cc-097c-430b-8d9a-2a120cdab506/7-nike-opt.png" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d41c4daa-ed19-472b-9ec0-2258f97e8f4a/7-nike-large-84x84.png">View large version</a>)</figcaption></figure>

If you want to experiment with arrows, consider a design that clarifies their function by showing a slice of the following slide, as seen on Amazon below.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59ae51b8-2a6c-441d-b1a1-113a85b9c7e2/8-amazon1-large.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e99383d-a0e0-404f-8eaf-036067cb94c2/8-amazon1-opt.png" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59ae51b8-2a6c-441d-b1a1-113a85b9c7e2/8-amazon1-large.png">View large version</a>)</figcaption></figure>

<p>A great way to ensure contrast is to detect the brightness of the area of the image where the controls are to appear, and then change the controls’ colors accordingly. Kenneth Cachia at Google even made a free script for this very purpose, called <a href="https://www.kennethcachia.com/background-check/index.html">BackgroundCheck</a>. (But don’t copy the rest of his carousel because it violates several of our other 10 requirements.)</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c78a5a9-e09b-4079-a59f-c9e22089806b/9-backgroundcheck-large.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/728b976e-9249-4d7f-b982-3d3fbdc4da55/9-backgroundcheck-opt.png" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c78a5a9-e09b-4079-a59f-c9e22089806b/9-backgroundcheck-large.png">View large version</a>)</figcaption></figure>

While the conventional design pattern for carousel controls is a series of dots to indicate the current slide among the set, and arrows for moving back and forth, other designs will achieve the same goals. One design worth highlighting is the “table of contents” seen in Amazon’s carousel below.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/127883ab-00b7-48ef-9d2c-13b1a561821f/10-amazon-2-large.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb21a6e6-7c90-4a61-8864-ee3508b701fb/10-amazon-2-opt.png" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/127883ab-00b7-48ef-9d2c-13b1a561821f/10-amazon-2-large.png">View large version</a>)</figcaption></figure>

<p>The table of contents is a particularly interesting pattern because it addresses two of the biggest weaknesses of conventional dots and arrows. First, it combines the indication of the current slide and the manual slide controller into a single UI component. Secondly, it provides information scent, showing users a snippet of what’s coming up next, thereby allowing users to jump between slides in a meaningful way. <a href="https://www.youtube.com/watch?v=Y-FMTPsgy_Y&amp;t=60m49s">Luke Wroblewski shares</a> that Amazon has found that this pattern performs well.</p>

## 4. Everything Is Different On Touch Devices

During our years-long usability study of mobile e-commerce websites, we’ve seen that home page carousels have vastly different requirement on touch devices than on desktop devices — so different that all of the interaction logic outlined for desktop (in section 2 above) is invalidated on mobile. Moreover, new requirements apply. We particularly observed the following three implementation details to be important on touch devices:

*   The lack of hover invalidates the use of auto-rotation.
*   Always support swipe gestures.
*   Optimize the carousel’s artwork for mobile screens.

### Lack of Hover Invalidates the Use of Auto-Rotation (31% Get It Wrong)

First, auto-rotating slides is only a good idea if the user’s device supports the hover state. This is crucial because the hover state enables us to infer a user’s potential interest in a given slide.

We can use the hover state as an indication that the user is interested in a slide’s content and might want to open the slide after reading its text. Thus, auto-rotation should be temporarily paused to allow the user to finish reading the text and avoid accidentally clicking on the wrong slide.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/398d8cf8-fd2c-4ce5-a070-e01b172c2aa0/11-toysrus-2-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1de3ceb-11cd-4f50-b7db-871cdd4ebdaf/11-toysrus-2-opt.jpg" /></a><figcaption>Here, a subject on <a href="https://baymard.com/homepage-and-category-usability/benchmark/site-reviews/136-toys-r-us">Toys’R’Us</a>’ mobile website noticed an interesting slide, “Spring Into Summer Mega Sale,” and reached to tap the screen. Unfortunately the carousel auto-rotated milliseconds earlier, diverting him to a “Bike Blast” sale. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/398d8cf8-fd2c-4ce5-a070-e01b172c2aa0/11-toysrus-2-large.jpg">View large version</a>)</figcaption></figure>

In practice, this means that auto-rotation isn’t appropriate for mobile websites or touch devices simply because it lacks a hover state to invoke the critical pause in rotation. Without a way to infer the user’s focus on the page, it is impossible to know whether the user is reading a particular slide or is about to click on the current slide. Auto-rotation could invoke a slide change just milliseconds before the user clicks the carousel, causing them to open the wrong page — as observed numerous times in our mobile usability study.

<p>The <a href="https://baymard.com/mcommerce-usability/benchmark/mobile-site-reviews">mobile e-commerce</a> usability benchmark we conducted revealed that, while 56% of mobile e-commerce websites have a home page carousel, 31% of mobile websites have one that auto-rotate, and 25% have a manual home page carousel. In other words, close to half of mobile websites with a carousel have the beginnings of an acceptable implementation because their mobile carousels don’t auto-rotate.</p>

### Always Support Swipe Gestures (12% Don’t)

<p>Secondly, support key touch gestures — particularly swiping, because users have come to expect that this is how “galleries” are navigated on touch devices. This doesn’t mean you shouldn’t implement traditional carousel interface controls, such as next and previous buttons and slide indicators; however, we found that carousel controls should be provided in addition to swipe gesture support. Our mobile e-commerce benchmark revealed that 12% of mobile websites don’t support swipe gestures for their image galleries in general (although compliance is higher than for <a href="https://baymard.com/blog/mobile-image-gestures">image zoom gestures</a> on product pages, which 40% don’t fully support).</p>

Side note: Don’t rely exclusively on swipe gestures on the desktop either, because they are not obvious. Desktop websites need clickable carousel controls as well.

### Optimize Artwork for Mobile

One thing we frequently observed when reviewing mobile websites with a home page carousel is that artwork from the desktop website is reused. This isn’t a problem so long as one ensures that any text in the slides remains legible when scaled down to a tiny mobile screen held in portrait mode. Occasionally, when benchmarking and auditing mobile websites (in particular, responsive websites), even the mobile websites of companies beyond the $100-million online sales mark, we see that artwork created for desktop is simply scaled down and reused on mobile.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7100d6-4ac3-4625-9c4c-fe1e4c761fbc/12-neiman-marcus-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd06e7fa-e140-48c9-b899-ec53c6939f10/12-neiman-marcus-opt.jpg" /><br>
</a><figcaption><a href="https://baymard.com/homepage-and-category-usability/benchmark/site-reviews/130-neiman-marcus">Neiman Marcus</a> simply scales down its desktop carousel artwork and uses it directly in its mobile home page carousel. As seen on the right, this makes some of the text barely legible because it wasn’t designed for the small mobile screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7100d6-4ac3-4625-9c4c-fe1e4c761fbc/12-neiman-marcus-large.jpg">View large version</a>)</figcaption></figure>

Finally, mobile users seem to have less patience for slow-loading carousels. This is likely because they usually can’t see anything other than the carousel on their screen, as opposed to the desktop, where the user can typically scan navigation menus and other content while they wait 1 to 5 seconds for the carousel’s content to load. So, along with ensuring legibility, ensure that the weight of the slide images is optimized for a mobile device’s bandwidth.

## The 10 Carousel Requirements

Beyond quality and relevance of content, the design and logic of a home page carousel would have to meet all 10 of the following requirements to avoid serious usability issues:

1.  All platforms: Sequence the slides carefully, because the first slide will get multiple times the exposure as subsequent slides.
2.  All platforms: The carousel should never be the only way to access a website’s features and content.
3.  Desktop: Only use auto-rotation when the diversion of attention away from other home page elements caused by the animated graphics is acceptable.
4.  Desktop: Rotate slides at a moderate pace — 5 to 7 seconds usually suffices for a slide with just a heading. If the amount of textual information differs between slides, a unique rotation time for each slide is usually called for (a detail almost never adhered to).
5.  Desktop: Pause auto-rotation on hover to avoid changing a slide that the user is likely reading or about to click.
6.  Desktop: Permanently stop auto-rotation after the user has clicked on the carousel’s interface controls.
7.  All platforms: Always indicate the current slide among the set, and allow users to navigate back and forth. Conventionally, this means using dots and arrows that are big enough and that contrast with the underlying image. On the desktop at least, this can be achieved in other ways, such as by using the “table of contents” design.
8.  Touch devices: Due to the lack of a hover state (and, therefore, a way to pause auto-rotation), never auto-rotate on mobile websites or for touch devices.
9.  Touch devices: Support swipe gestures, in addition to any other UI controls.
10.  Mobile devices: Ensure that the text in slides is still readable if you are scaling down artwork from the desktop.

<p>We can see now, with this long list of pitfalls, that most home page carousels perform poorly simply because they are implemented inadequately. For example, 42% of auto-rotating desktop carousels don’t pause on hover. Also, if we consider the most compelling example from <a href="https://shouldiuseacarousel.com">Should I Use A Carousel?</a>, borrowed from the <a href="https://www.nngroup.com/articles/auto-forwarding/">Nielsen Norman Group</a>, the carousel tested violates (at least) two of the most important rules: It’s the only way to access that content (violating rule 2), and it doesn’t pause auto-rotation on hover (rule 5) — in addition, the carousel is placed above the main navigation and header. (In a subsequent article, the Nielsen Norman Group offers a more <a href="https://www.nngroup.com/articles/designing-effective-carousels/">nuanced perspective</a> on carousels.)</p>

If all 10 requirements would be too much work for you or simply would not be worth the investment, then we’d recommend what most others advise: Don’t use a carousel at all. Instead, rely on the alternative presented below.

## An Alternative To Carousels

During our usability testing, we saw that a generally well-performing alternative to home page carousels is to simply display static “slides” as distinct sections on the home page.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bef7bab-f82f-430f-aa53-59a9f6f4be9d/13-llbean-large.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06b4eb7e-3630-4a07-803c-f6824b472093/13-llbean-opt.jpg" /><br>
</a><figcaption>Two versions of <a href="https://baymard.com/mcommerce-usability/benchmark/mobile-site-reviews/276-l-l-bean">L.L. Bean’s home page</a>: The left version relies on a troublesome carousel (violating rule 7: auto-rotation on mobile), whereas the newer version to the right uses the well-performing pattern of simply displaying all artwork directly on the home page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bef7bab-f82f-430f-aa53-59a9f6f4be9d/13-llbean-large.jpg">View large version</a>)</figcaption></figure>

Repurposing slides as static content sections scattered throughout the home page (according to importance) has a number of benefits:

*   It gets rid of auto-rotation and the carousel controls for changing slides, making it particularly well suited to mobile websites.
*   It aligns extremely well with how users interact with home pages. We observed during testing that 70% of mobile users perform an initial [scroll and scan of the home page](https://baymard.com/blog/mobile-homepage-usability) to figure out the type of website they’ve landed on. Promoting a handful of key paths, each with bespoke imagery, makes for a much more more scannable home page than a carousel slider (either manual or auto-rotated).
*   It is significantly cheaper to implement than a carousel that adheres to all 10 requirements. Granted, depending on the organization, updating the home page content might prove to be more expensive than replacing a carousel slide.
*   The organization will much more readily recognize the need for tight curation of content (as opposed to throwing a lot of content into a carousel simply because it can accommodate it).

{{< signature "al, il" >}}
