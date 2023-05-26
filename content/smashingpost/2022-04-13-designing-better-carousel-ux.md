---
title: '15 Guidelines For Better Carousels UX'
slug: designing-better-carousel-ux
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/729433dc-4cea-4eed-9128-0e9e6dbfe6db/designing-better-carousel-ux.jpg
date: 2022-04-13T12:00:00.000Z
summary: >-
  In this [series of articles](/category/design-patterns/), we highlight design patterns and techniques to design better interfaces. You can find more examples in [“Smart Interface Design Patterns”](https://smart-interface-design-patterns.com/), a 9h-video course with 100s of hand-picked examples, curated by Vitaly.
description: >-
  Carousels don’t have a good reputation, and rightfully so. But we can make them more useful. Best practices and guidelines to improve the carousel design with honest scrolling direction, labels, thumbnails and grouped prev/next-buttons.
categories:
  - Design Patterns
  - Usability
  - UX
  - Accessibility
---

**Carousels don’t have a good reputation**, and rightfully so. They have plenty of accessibility issues, they often exhibit low click-through rates, can be very disruptive when auto-advancing and people frequently scroll past through them. Add to it small progress dots with tiny tap areas, barely visible labels and a bit of parallax, and you have a quite troublesome design pattern in your hands.

Yet somehow carousels still manage to find their way to websites and applications. They often make a quite lavish appearance in image galleries and news items, on landing pages and on corporate websites &mdash; and especially for onboarding, testimonials, and product highlights.

<figure><a href="https://twitter.com/jackygilbertson"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="800" height="480" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png" sizes="100vw" alt="A person with short hair holds a phone looking at a product page on their mobile screen with an image of a watch while standing in front of merry-go-round horse carousel with children enjoying the ride"></a><figcaption class="op-vertical-bottom">Carousels come in various sizes and flavors. A <a href="https://dribbble.com/jackygilbertson">wonderful illustration</a> by <a href="https://twitter.com/jackygilbertson">Jacky Gilbertson</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4e433f-b19f-4ec3-8917-63497e0b7983/1-designing-better-carousel-ux.png">Large preview</a>)</figcaption></figure>

What should we keep in mind if we do need to design a carousel? How do we create a **better carousel experience** that helps people, rather than frustrates them? And how do we avoid common accessibility and usability failures that carousels usually entail? That’s exactly what this article is all about. 

### Table of Contents

The article is slightly lengthier as expected, so tighten up your seat belts — it’s going to be quite a journey.

- [Do Users Actually Use Carousels?](#do-users-actually-use-carousels)
- [Scrolling Direction](#indicate-an-honest-scrolling-direction)
- [Replace Progress Dots with Labels](#replace-progress-dots-with-labels)
- [Replace Progress Dots With A Horizontal Slider](#replace-progress-dots-with-a-horizontal-slider)
- [Indicate The Current Position](#always-indicate-the-current-position-of-the-carousel)
- [Prev/Next Buttons](#better-usability-of-prev-next-buttons)
- [How Far Should Prev/Next Buttons Jump?](#how-far-should-prev-next-buttons-jump)
- [Keep Prev/Next Buttons Close](#keep-prev-next-buttons-close)
- [Combine Tabs and Carousels](#combine-tabs-and-carousels)
- [Use Thumbnails Or Icons](#use-thumbnails-or-icons-to-encourage-click-throughs)
- [Dragging Alone Isn't Good Enough](#dragging-alone-isn-t-good-enough)
- [Add An Information Scent](#add-an-information-scent-to-the-carousel)
- [Add At Least 5–7s Delay](#avoid-auto-advancing-or-add-at-least-5-7s-delay)
- [Always Include A "Pause" Button](#always-include-a-pause-button-for-auto-advancing-carousels)
- [Alternatives to Carousels](#alternatives-to-carousels)

<!-- ## Not All Carousels Are The Same

When we think about carousels, we often dismiss them due to all the downsides that they have. However, as a pattern, **carousels can be quite effective**, especially when we want to highlight all features or options, but lack space to display them all at once. In a way, very much like accordions, carousels provide a way to show and hide some pieces of content &mdash; either manually or automatically. And that’s not something that many other components have.

Carousels come in various sizes and flavors. On mobile, we might be very much used to horizontal carousels where we are expected to swipe left and right to navigate between available options. On desktop, we’d be clicking through arrows pointing in either direction to get to the item of interest. Yet sometimes carousels are arranged vertically, allowing us to jump through sections of the page.

{{< rimg href="https://www.milliyet.com.tr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48eeeb2a-2a54-4e10-a33f-33a507905d33/2-designing-better-carousel-ux.png" width="800" height="589" sizes="100vw" caption="An exhibition of carousels, all in one screen: vertical, horizontal, with thumbnails, and a content slider. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48eeeb2a-2a54-4e10-a33f-33a507905d33/2-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of a Turkish website named Milliyet with vibrant colors and large font size" >}}

While we often see arrows indicating the direction of navigation, sometimes there are only progress dots giving us a clue of how many carousel slices are out there, and if we are lucky, we might see a number of the current slices updating as we interact with it. And sometimes (like on [Miliyet](https://www.milliyet.com.tr/) illustrated in the image on the top), we see numbers and thumbnails that provide a slightly better context to where the user is currently navigating.

In fact, there are plenty of options we can choose from when designing carousels:

- progress dots
- horizontal bar
- slice numbers
- slice thumbnails
- “prev” and “next” arrows
- auto-advancing
- steppers

The lines between the different variants of the carousels are blurry. But still, let’s explore these options one by one. -->

## Do Users Actually Use Carousels?

That’s a very fair question, and quite frequently the answer will be: [not really](https://shouldiuseacarousel.com/). In fact, it’s almost as if some users were **allergic** **towards carousels**. It’s common to see people noticing them, just to make sure they can dismiss them during the entire session. Not many people connect anything relevant with carousels since most of the time the content hidden in the carousel is either irrelevant or promotional &mdash; or annoying and distracting.

{{< rimg href="https://www.milliyet.com.tr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65456e0d-3524-4649-933f-8995616af871/0-many-carousels-at-once.jpg" width="765" height="496" sizes="100vw" caption="An exhibition of carousels, all in one screen: vertical, horizontal, with thumbnails, and a content slider. Notice that instead of dots, numbers are used consistently here. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48eeeb2a-2a54-4e10-a33f-33a507905d33/2-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of a Turkish website named Milliyet with vibrant colors and large font size" >}}

That’s not very surprising given how large some carousels actually are, sometimes taking up anything between **50 to 90% of the entire screen**. And because the content displayed in the carousels is rarely a reason why users end up on the site, it’s dismissed almost instinctively. Hence, users rarely click through the slides of carousels, especially if the very first slide isn’t enticing enough or has no connection with the task at hand.

Carousels definitely won’t help with drawing more attention to general promotions, internal news, or press releases which don’t get much interest anyway. Many higher education websites, public services and online banking (for example) would probably benefit from removing carousels, rather than adding them in.

{{< rimg href="https://www.milliyet.com.tr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f6a3ec5-fcb3-4387-88c2-9f524a921824/01-many-facets-of-the-carousel.jpg" width="765" height="496" sizes="100vw" caption="Carousels have many faces, one of them is a an auto-advancing carousel, sometimes used in onboarding. Designed by <a href='https://dribbble.com/shots/3938570-Landing-page-Banner-Animation'>Selecto</a> for a landing page. (<a href='https://dribbble.com/shots/3938570-Landing-page-Banner-Animation/attachments/10106543?mode=media'>Large preview</a>)" alt="Carousels have many faces, one of them is a circular carousel, sometimes used in onboarding." >}}

**Auto-advancing carousels** don’t solve the issues listed above either. Whenever *any* portion of the content on the page starts moving, many users will ignore it almost immediately. If you are lucky, users might be trapped exploring relevant content near the carousel, so they might get a glimpse of the second or third slide, but they will bundle all their strengths to ignore it until they move on to the next page.

More often though many people tend to just scroll past auto-advancing carousels, trying to get it out of the view and move on with their task. This is especially noticeable with **onboarding tutorials in mobile apps**, where the very first thing that users search for when facing an onboarding carousel is a precious “skip” button.

Carousels are also a poor choice when it comes to **content discovery**. If something important is presented in one of the later slides of a carousel, a vast majority of users will experience severe issues discovering it. Not surprising: if something is important, we should probably not hide it &mdash; this goes for the carousel just like it goes for the infamous hamburger navigation.

Finally, carousels also pose **severe accessibility issues** for keyboard and screen reader users who simply can’t use them properly without thorough development work. 

Does it mean that we should dismiss carousels for good and always abandon them at all costs? Not necessarily.

{{< rimg href="https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb9b6c93-1141-482c-a519-ec167fc45987/3-designing-better-carousel-ux.png" width="800" height="595" sizes="100vw" caption="In <a href='https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/'>effective carousels</a>, slide advancement interactions follow an exponential rate of decay. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb9b6c93-1141-482c-a519-ec167fc45987/3-designing-better-carousel-ux.png'>Large preview</a>)" alt="A graph showing decays in viewing incremental carousel slides through swipe (blue), arrows (green) and thumbnails (yellow)" >}}

**Carousels can be quite effective**, especially when we want to highlight all features or options, but lack space to display them all at once. There are a few contexts in which carousels perform fairly well though. This holds true especially if a carousel is meaningfully integrated into a task that a user is trying to complete. In such cases, click-through rates are usually relatively high: [users advance carousels at a roughly linear rate](https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/).

Carousels work when:

- users are exploring an appropriate option, or choose a pricing plan,
- users browse through testimonials, reviews, products or their features,
- users study product image galleries on eCommerce pages to understand the specifics of a product they are interested in purchasing,
- users want to preview an experience they want to book (hotel, vacation, museum, theatre, restaurants) &mdash; in cases when they want to see large **fullscreen images or videos**  while still being able to navigate between them back and forth,
- users explore content details as cards on mobile, swiping left and right.

In other words, carousels work when we **provide additional content within a specific, and relevant context**. All of these use cases are very typical for retail, tourism, product pages, galleries, related items, news stories and portfolios, among other things. That’s exactly where carousels shine.

Unfortunately, most of the time the ways we design carousels go very much against usability and accessibility, making carousels barely usable. Let’s explore a few techniques and strategies of how to change just that.

{{% feature-panel %}}

## Indicate An Honest Scrolling Direction

Carousels come in various sizes and flavors. This goes for controls as much as for the direction of these controls. Sometimes we might encounter progress dots, and sometimes arrows, and sometimes we are expected to swipe (especially on mobile). Either way, the **direction of the carousel’s control indicates expected movement** when navigating the carousel. In a way, it’s a signpost that users read to understand the mechanics of the interaction. It goes without saying that it’s in our best interest to not break these expectations.

{{< rimg href="https://youandoil.eu/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/030014be-6913-4ebc-8219-da7b7875b5c2/4-designing-better-carousel-ux.png" width="800" height="496" sizes="100vw" caption="<a href='https://youandoil.eu/'>You and Oil</a> feature a vertical slider to indicate a horizontal carousel. It’s probably not very obvious. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/030014be-6913-4ebc-8219-da7b7875b5c2/4-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the You and Oil website with a woman and man facing and smiling at each other" >}}

[You and Oil](https://youandoil.eu/) (pictured above) features a carousel with a slider aligned vertically. How would you expect the carousel to work? How would you navigate through the slides? You might be inclined to drag the handle across the track, but it doesn’t do anything. You might then be inclined to click on the numbers, but it doesn’t do anything either. To navigate the carousel, you need to drag the slider from right to left. That’s unlikely to be expected by most users though. To solve this, we could **flip the progress indicator by 90 degrees**, turn it into a horizontal slider and place it above or below the content area.

{{< rimg href="https://www.vangoghmuseum.nl/nl" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1125f076-51dd-42c7-9a87-2969d698fc9f/5-designing-better-carousel-ux.png" width="800" height="473" sizes="100vw" caption="<a href='https://www.vangoghmuseum.nl/nl'>Van Gogh Museum</a> hints at horizontal scrolling, but only vertical scrolling is supported. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1125f076-51dd-42c7-9a87-2969d698fc9f/5-designing-better-carousel-ux.png'>Large preview</a>)" alt="A glimpse of the Van Gogh’s museum website with two artworks shown and used in a carousel" >}}

The same problem appears on the [Van Gogh’s museum website](https://www.vangoghmuseum.nl/nl). The scrolling indicator is horizontal, yet one needs to **scroll vertically** to browse through available cards. Dragging the cards horizontally doesn’t seem to be supported. We could add **prev/next buttons above the cards** to help users navigate in a bit more predictable way.

If the carousel is moving horizontally, it’s only sensible to hint at expected behavior with a horizontal indicator. The same goes for vertical carousels in exactly the same way. It might sound a bit boring, but it will avoid quite a bit of confusion down the line.

## Replace Progress Dots with Labels

We are very much used to **progress dots** indicating the current position in carousels, but there are some good reasons why we might want to avoid them. For one, sometimes users desperately try to click on them, assuming that this is a supported interaction to navigate forwards and backward.

But because these dots are usually incredibly small, navigating via them &mdash; even if it’s supported &mdash; is slow and requires a lot of precision. Usually, this results in a feverish combination of rage clicks (or taps), mistakes, and unexpected jumps back and forth.

On the other hand, progress dots **aren’t a particularly effective way** to entice users to click through the carousel. They don’t communicate much; definitely not what each dot represents, nor what users should be expecting while sliding through the carousel. Progress indicators don’t convey any particular meaning (except the progress, that is), and thus aren’t very relevant to encouraging interaction.

{{< rimg href="https://www.platform-seven.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f4d32a4-8b68-40c5-a490-e7faf6f45c55/plattform-seven.jpg" width="764" height="484" sizes="100vw" caption="What do different symbols in the left sidebar represent? <a href='https://www.platform-seven.com/'>Platform Seven</a> requires a bit of exploration to understand how it works. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64a91f56-55be-4f28-b7c8-53a21b53b980/6-designing-better-carousel-ux.png'>Large preview</a>)" alt="A landing page that says Make Your mark On The World and colored blobs scattered on the page" >}}

On [Platform Seven](https://www.platform-seven.com/) (picture above), it might not be very obvious what you are supposed to do to move forward and backward. Also, dots have different shapes and states which is difficult to decipher. Here, various sections of the page are grouped and highlighted with white background. This might not be very obvious to some readers. Here, progress dots do communicate the **position in space**, but they don’t necessarily invite users to explore that space, nor provide the reasons to do so.

{{< rimg breakout="true" href="https://press.stripe.com/the-making-of-prince-of-persia" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf92049-cb64-4957-8d3c-0b69159e6254/7-designing-better-carousel-ux.png" width="800" height="471" sizes="100vw" caption="<a href='https://press.stripe.com/the-making-of-prince-of-persia'>Stripe Press</a> includes short horizontal lines, each representing a section on the site. The labels appear only on hover. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cf92049-cb64-4957-8d3c-0b69159e6254/7-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of a page introducing the book The Making Of Prince Of Persia: Jornals 1985-1993" >}}

The same problem also appears in regular navigation. [Stripe Press](https://press.stripe.com/the-making-of-prince-of-persia) doesn’t include a carousel but provides a navigation on the left. The design is outstanding, but hover is required to make sense of the sidebar navigation. Some sort of **additional context**, e.g. with labels or thumbnails, would probably help in discovery.

In general, it seems to be a good idea to **never use progress dots as the only way** for users to navigate the carousel.

{{< rimg breakout="true" href="https://www.creativedenmark.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bbcf0e8-621b-4ea3-ac0b-bbe63b994e5e/8-9-designing-better-carousel-ux.png" width="800" height="419" sizes="100vw" caption="Replacing progress dots with labels gives carousels more context. Example: <a href='https://www.creativedenmark.com'>Creative Denmark</a>.  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bbcf0e8-621b-4ea3-ac0b-bbe63b994e5e/8-9-designing-better-carousel-ux.png'>Large preview</a>)" alt="Desktop and Mobile compared side-by-side of the CreativeDenmark website as of April 2022" >}}

One way to **encourage navigation through the carousel** is by adding more context to it. This could be done by using **labels, thumbnails or video previews,** for example. [CreativeDenmark](https://www.creativedenmark.com/) highlights each slide of the carousel with a distinct section, which is labeled and includes a video preview on hover. Unfortunately, the carousel isn’t keyboard-accessible. On mobile, the labels are rotated by 90 degrees &mdash; quite unusual, but because labels are relatively short, it might work in this scenario.

{{< rimg breakout="true" href="https://www.laciteduvin.com/en" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bac00b0-8b7b-4822-a3ae-f90aafaa3547/10-designing-better-carousel-ux.png" width="800" height="454" sizes="100vw" caption="<a href='https://www.laciteduvin.com/en'>La Cité du Vin</a> adds labels to each section in the progress bar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bac00b0-8b7b-4822-a3ae-f90aafaa3547/10-designing-better-carousel-ux.png'>Large preview</a>)" alt="A carousel presented on the front page of a French website, La Cité du Vin" >}}

[La Cité du Vin](https://www.laciteduvin.com/en) replaces progress dots with **text labels** to explain what a user should be expecting in the carousel. Unfortunately, most labels are impossible to read without clicking on them.

{{< rimg breakout="true" href="https://circle.squarespace.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a702390-a61b-4b00-a9be-f68e9885a592/11-designing-better-carousel-ux.png" width="800" height="464" sizes="100vw" caption="<a href='https://circle.squarespace.com/'>Squarespace Circle</a> with labels placed next to each story on a circular auto-advancing carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a702390-a61b-4b00-a9be-f68e9885a592/11-designing-better-carousel-ux.png'>Large preview</a>)" alt="Squarespace’s landing page as of April 2022 showing a photo of a young Black woman named Aylin Marie smiling with a circular full-height carousel layered on top or in front of the Aylin’s half-body portrait" >}}

A circular full-height carousel on [Squarespace Circle](https://circle.squarespace.com/) uses labels to **highlight individual stories** of contributors. Jumping to a story with some context of what the story is going to be about is a bit more compelling than clicking through lifeless progress dots.

{{< rimg breakout="true" href="https://www.myswitzerland.com/en/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35b79250-e629-4a0c-b727-c46a901fc5d9/12-designing-better-carousel-ux.png" width="800" height="505" sizes="100vw" caption="<a href='https://www.myswitzerland.com/en/'>MySwitzerland</a> features a full-height carousel with video fragments in a auto-advancing carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35b79250-e629-4a0c-b727-c46a901fc5d9/12-designing-better-carousel-ux.png'>Large preview</a>)" alt="A landscape photo taken somewhere in Switzerland showing a cable car" >}}

Carousels don’t have to show only images — they can highlight video content as well. An example of a **carousel with video slices** is [MySwitzerland.com](https://www.myswitzerland.com/en/). The carousel is auto-advancing, with video segments showing one after another. Each video segment is represented by a label, placed within a mini-navigation at the bottom left. Plus, the website is fully accessible with the keyboard &mdash; and it’s visually stunning, too!

{{< rimg breakout="true" href="https://www.thalia.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2639f1b8-5c5f-4efd-880e-643c08072833/65-designing-better-carousel-ux.png" width="800" height="568" sizes="100vw" caption="Carousel at the bottom, complemented with text labels that indicate what a user should be expecting when navigating through the carousel. (Source: <a href='https://www.thalia.de/'>Thalia.de</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2639f1b8-5c5f-4efd-880e-643c08072833/65-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

Test what happens if you **replace progress dots with meaningful labels or key highlights**. Chances are high that carousels that used to have very poor click-through rates, suddenly will come to life. However, if your carousel has too many items, or labels are way too lengthy, there are alternative ways to encourage interaction.

## Replace Progress Dots With A Horizontal Slider

The useful feature of progress dots is that they indicate progress. However, we don’t need to rely on them alone to show where a user currently is. One option is to use a **horizontal slider** to indicate how far the overall list of options actually is. That’s what [Rolex](https://www.rolex.com/en-us) does, accompanying the slider with an arrow to move forward step-by-step. This might be perfectly enough &mdash; and avoid rage clicks/taps on the individual dots.

{{< rimg breakout="true" href="https://www.rolex.com/en-us" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9807f4c3-8bf6-456e-b654-10d1c4a06fb1/13-designing-better-carousel-ux.png" width="800" height="387" sizes="100vw" caption="A horizontal progress bar instead of progress dots in a carousel. On <a href='https://www.rolex.com/en-us'>Rolex.com</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9807f4c3-8bf6-456e-b654-10d1c4a06fb1/13-designing-better-carousel-ux.png'>Large preview</a>)" alt="A horizontal slider showing difference watch designs shown on the Roley website in April 2022" >}}

On [Tylko](https://tylko.com), a horizontal slider indicates the position in the carousel, with arrows pointing in both directions of movement. An interesting way to integrate user profiles, photos and **customization options** into one single component.

{{< rimg breakout="true" href="https://tylko.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57f4e8bf-a364-4767-b982-7c9a9089cc00/14-designing-better-carousel-ux.png" width="800" height="431" sizes="100vw" caption="On <a href='https://tylko.com'>Tylko</a>, examples are presented as a carousel, with customization options and user profiles combined in each slide. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57f4e8bf-a364-4767-b982-7c9a9089cc00/14-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the Tylko website as of April 2022 showing a horizontal slider at the bottom of the page" >}}

[Bugaboo](https://www.bugaboo.com/fr-fr) combines a progress slider with arrows located at the **bottom of the carousel**, along with hints that appear on hover. The carousel doesn’t auto-advance; the horizontal bar merely represents where the user currently is.

{{< rimg breakout="true" href="https://www.bugaboo.com/fr-fr/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b5f8710-bd9d-4299-9fb6-70a9f46264f8/15-16-designing-better-carousel-ux.png" width="800" height="426" sizes="100vw" caption="For its carousel, <a href='https://www.bugaboo.com/fr-fr/'>Bugaboo</a> uses a slider at the bottom of the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b5f8710-bd9d-4299-9fb6-70a9f46264f8/15-16-designing-better-carousel-ux.png'>Large preview</a>)" alt="A comparison of the desktop and mobile versions of the Bugaboo website presented side-by-side" >}}

## Always Indicate The Current Position of The Carousel

Adding a horizontal slider alone isn’t ideal though. Especially for longer carousels, it doesn’t convey enough information to indicate **where exactly the user currently is** in the carousel, and how far they have to go to make a full circle. We can invent various ways of showing progress &mdash; perhaps with percentages or a pie chart visualization, but probably the best one is the simplest one: numbers.
 
[Daphne Wilde](https://daphnewilde.com) uses a non-conventional sliding numbers indicator to show where a user currently is. Users can also click on the images in the carousel to jump through available options. While this interaction isn’t necessarily obvious, numbers are large and easy to click and — most importantly — difficult to mis-tap.

{{< rimg breakout="true" href="https://daphnewilde.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fee361b-5df7-4187-96c6-8db0ca42c47c/17-18-designing-better-carousel-ux.png" width="800" height="374" sizes="100vw" caption="How would you navigate this carousel? On <a href='https://daphnewilde.com'>Daphne Wilde</a>, users are expected to click on on numbers to move within the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fee361b-5df7-4187-96c6-8db0ca42c47c/17-18-designing-better-carousel-ux.png'>Large preview</a>)" alt="An example of a carousel using non-conventional sliding numbers on Daphne Wilde’s website in April 2022" >}}

The more complex our visualization of the progress is, the more issues it’s likely to bring up. [Vallourec](https://www.vallourec.com/) uses a pie chart indicator to highlight sub-sections individually while highlighting the section as well. Additionally, there is a bit of parallax-alike experience in place, combined with a vertical carousel.

{{< rimg breakout="true" href="https://www.vallourec.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57153ceb-0578-47ee-a743-07d78ba84d16/19-designing-better-carousel-ux.png" width="800" height="496" sizes="100vw" caption="<a href='https://www.vallourec.com'>Vallourec</a> with an unconventional pie chart that indicates the current state in the carousel. It might not be very obvious. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57153ceb-0578-47ee-a743-07d78ba84d16/19-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the Vallourec website in which a pie chart indicator needs to be used in order to be able to visit the sub-sections of the site" >}}

[Teatr Lalka](https://teatrlalka.pl/en/spektakle/rycerz-gwiazdy-wigilijnej), a puppet theater from Poland, with a creative, dynamic, and accessible approach to highlighting the position in the carousel (see the second image at the bottom). Each photo has a label, and it could potentially contain a short description, too. The entire website uses the metaphor of the puppet theater, with lovely transitions and animations. Beautifully designed, from start to finish.

{{< rimg breakout="true" href="https://teatrlalka.pl/en/spektakle/rycerz-gwiazdy-wigilijnej" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee9595cc-2a13-435d-992d-eed9e1e96547/20-designing-better-carousel-ux.png" width="800" height="474" sizes="100vw" caption="Carousels on <a href='https://teatrlalka.pl/en/spektakle/rycerz-gwiazdy-wigilijnej'>Teatr Lalka</a> include a dynamic layout and show the current position in the carousel with numbers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee9595cc-2a13-435d-992d-eed9e1e96547/20-designing-better-carousel-ux.png'>Large preview</a>)" alt="A Polish website, TeatrLalka, uses puppets as part of the website’s navigation" >}}

{{< rimg breakout="true" href="https://www.26may.ge/ka/ivanejavakhishvili" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd1d9e94-c45a-4daa-94af-18a31953de8e/21-designing-better-carousel-ux.png" width="800" height="439" sizes="100vw" caption="Nothing can beat the clarity of numbers. Point in case: <a href='https://www.26may.ge/ka/ivanejavakhishvili'>26may.ge</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd1d9e94-c45a-4daa-94af-18a31953de8e/21-designing-better-carousel-ux.png'>Large preview</a>)" alt="On the same website, numbers are used to guide the user through the gallery" >}}

[26day.ge](https://www.26may.ge/ka/ivanejavakhishvili), a website dedicated to 100 years of Georgia's first Democratic Republic, uses **numbers and transitions** to swipe through the images in the little image gallery. The buttons are located under the carousel, they are grouped, and there is a little indicator of the position in the carousel, too. Admittedly, some transitions are a little bit too heavy though, especially on the frontpage.

{{< rimg breakout="true" href="https://www.26may.ge/ka/ivanejavakhishvili" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6a8bac8-55e3-4ca3-acaf-215200e31d53/22-designing-better-carousel-ux.png" width="800" height="476" sizes="100vw" caption="<a href='https://www.26may.ge/ka/ivanejavakhishvili'>26may.ge</a> uses a carousel with grouped arrows and numbers indicating progress. It’s hard to misundertand it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6a8bac8-55e3-4ca3-acaf-215200e31d53/22-designing-better-carousel-ux.png'>Large preview</a>)" alt="Numbers and transitions shown in order to swipe through the images on the website’s image gallery" >}}

No visual representation of progress can beat the **clarity of numbers**. If you do use a horizontal slider as an indicator of progress, consider adding numbers to highlight how many items there are in total, and where the user currently is. Deciphering ranges and filled bars are tricky. For shorter carousels this might not be as necessary, but it probably won’t hurt either.

{{% ad-panel-leaderboard %}}

## Better Usability of Prev/Next Buttons

This might sound a bit obvious, but it’s worth emphasizing: always include **prev/next buttons** to your carousels. Progress dots don’t necessarily indicate how *exactly* a carousel is supposed to be used. They do assume that users will be swiping left and right on mobile, yet not every implementation of the carousel supports that — and it might be not obvious at all on desktop.

Plus, sometimes swiping is quite unpredictable, with users **underestimating their swiping speed and jumping too far**, just to have to slowly swipe back to make sure they don’t skip anything relevant. On desktop, navigation through prev/next buttons is much more common and hence expected. Having a simple navigation pattern that that helps users navigate through the carousel in single steps can be a big help.

{{< rimg breakout="true" href="https://www.arte.tv/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/922f6fa0-0944-4c01-bbb7-603d0ce67212/23-designing-better-carousel-ux.png" width="800" height="363" sizes="100vw" caption="A classic on <a href='https://www.arte.tv/'>Arte.tv</a>: a catalog of options with an arrow vertically centered on the edges of the carousel’s area. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/922f6fa0-0944-4c01-bbb7-603d0ce67212/23-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of Arte.tv’s website as of April 2022 showing four ArteKino Classics with an arrow shown on the right for the user to use in order to navigate and preview more of the Classic movies" >}}

## How Far Should Prev/Next Buttons Jump?

But then there are so many questions that appear about fine little details that go into prev/next buttons. For example, **by how many items should a carousel “jump”**? Should the user jump over all visible items that currently appear on their screen, or should the carousel slowly move one by one, requiring multiple taps to show new items? Or perhaps we should move by 2–3 items instead to make jumps more predictable?

When users feel that the movements of the carousel happen too quickly, they seem to have a hard time understanding **how far they have jumped through**. So they go back to verify that they didn’t miss anything relevant. While the movements step-by-step are slower, usually they cause fewer mistakes, and every now and again moving forward slowly is perfectly acceptable.

{{< rimg href="https://www.netflix.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d11c54ae-40f6-4e94-a1af-ce5ebe53276b/24-designing-better-carousel-ux.png" width="800" height="361" sizes="100vw" caption="The one that rules them all: the carousel on <a href='https://www.netflix.com/'>Netflix</a> jumps users by the entire visible list. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d11c54ae-40f6-4e94-a1af-ce5ebe53276b/24-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the movies presented on the Netflix website in April 2022 with three horizontal carousels" >}}

However, if users tend to browse **through many items (10+ items)** in a very lengthy carousel, jumping one by one is way too slow, and jumping by a couple of items is confusing since the beginning and the end of the list aren’t obvious with every jump. In that case, jumping by the **entire visible list** is probably going to bring better results. The final decision will ultimately lie with your studies on how your users actually navigate the carousel, and how far they browse in the list.

## Keep Prev/Next Buttons Close

Another question that comes up in conversations a lot is the **best position** of prev/next-buttons. We want to **minimize errors**, mistakes, and mishaps as far as possible, and usually, this means increasing tap sizes and adding enough distance between interactive elements. At the same time, we want to speed up navigation within the carousel as far as possible, and this means minimizing the distance between opposite actions: in our case, that’s **moving forward and moving backward**. 

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fbd8840-e909-4860-85ab-7990eacf246e/67-designing-better-carousel-ux.png" width="800" height="491" sizes="100vw" caption="Where should prev/next-buttons live, and what should it depend on? Examples: <a href='https://mediamarkt.de/'>Mediamarkt</a>, <a href='https://zalando.be/'>Zalando</a>, <a href='https://airbnb.com/'>AirBnB</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fbd8840-e909-4860-85ab-7990eacf246e/67-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

There is no shortage in available options. We could place the arrow above the carousel, **center them vertically/horizontally** on the carousel’s slices, or display them under the carousel. Additionally, we could group them and display them together, next to each other, or space them out, and show them on the opposite sides of the carousel.

{{< rimg breakout="true" href="https://www.artmuseumgr.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c79846f-af5b-4006-ba4f-3fb557966589/25-26-designing-better-carousel-ux.png" width="800" height="359" sizes="100vw" caption="A comparison of the desktop and mobile versions of the <a href='https://www.artmuseumgr.org/'>Gram Museum</a> website showing both buttons above the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c79846f-af5b-4006-ba4f-3fb557966589/25-26-designing-better-carousel-ux.png'>Large preview</a>)" alt="A comparison of the desktop and mobile versions of the Gram Museum website showing both left and right arrows above the carousel (both versions)" >}}

[Gram Museum](https://www.artmuseumgr.org/) displays prev/next buttons **above the carousel** &mdash; both on mobile and on desktop. They are a little bit small, and could probably be larger. The arrows are aligned to the edges of the carousel, rather than being grouped together.

{{< rimg href="https://stripe.com/en-de/jobs/life-at-stripe" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db5b7a69-31d1-4a7c-b14c-ea370e0e3fe8/27-designing-better-carousel-ux.png" width="800" height="" sizes="100vw" caption="<a href='https://stripe.com/en-de/jobs/life-at-stripe'>Stripe Life at Jobs</a>, with arrows centered vertically. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db5b7a69-31d1-4a7c-b14c-ea370e0e3fe8/27-designing-better-carousel-ux.png'>Large preview</a>)" alt="Stripe Life at Jobs" >}}

On [Stripe Life at Jobs](https://stripe.com/en-de/jobs/life-at-stripe), the arrows are placed on the carousel slices, **centered vertically**. In fact, that’s a very common decision, but depending on the audience you have, it can cause trouble. When arrows sit straight on the carousel slices, and because usually each slice is a link driving users to a landing page, users accidentally miss the hit target and end up clicking on the wrong page. This is critical when arrows don’t have enough padding.

{{< rimg href="https://www.galaxus.ch/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d90af1f2-bb25-43d1-91e6-5bd9529137f6/28-designing-better-carousel-ux.png" width="800" height="" sizes="100vw" caption="Arrows positioned on products can be trouble. Example: <a href='https://www.galaxus.ch/'>Galaxus.ch</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d90af1f2-bb25-43d1-91e6-5bd9529137f6/28-designing-better-carousel-ux.png'>Large preview</a>)" alt="Galaxus.ch website" >}}

[Galaxus](https://www.galaxus.ch/) shows a very common pattern for eCommerce sites. Products are displayed within the carousel, with prev/next buttons on both edges of the carousel. Also note "Alle anzeigen" link in the right upper corner which displays all products on a separate page.

{{< rimg breakout="true" href="https://casper.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/885365e2-e4bb-46fc-bc4d-377b1aa4287c/29-designing-better-carousel-ux.png" width="800" height="452" sizes="100vw" caption="The distance customers have to travel to change direction isn’t short, and requires re-calibration of fingers, mouse pointer or any other input device. Example: <a href='https://casper.com/'>Casper.com</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/885365e2-e4bb-46fc-bc4d-377b1aa4287c/29-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the Casper.com website taken in April 2022 where the previous and next buttons are both floating on the side of the page" >}}

The design on [Casper.com](https://casper.com/) might appear exactly the same as in previous examples, but here the prev/next buttons are **floating aside from clickable text and images**, making it harder for users to mis-tap. However, once customers need to change the direction of the movement, they need to travel all the way back to the other side of the carousel’s galaxy, and then back. That distance travelled might be wasteful and unnecessary.

{{< rimg breakout="true" href="https://www.allianz.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0578acde-870c-4dbb-a3dc-887269bd23d8/30-designing-better-carousel-ux.png" width="800" height="513" sizes="100vw" caption="<a href='https://www.allianz.de'>Allianz.de</a> groups arrows on both sides of the progress dots under he carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0578acde-870c-4dbb-a3dc-887269bd23d8/30-designing-better-carousel-ux.png'>Large preview</a>)" alt="A German insurance company, Allianz, uses a carousel at the bottom of the page with dots placed between the arrows to give the user an idea of how many pages there are to click through" >}}

The distance that customers need to travel on [Allianz.de](https://www.allianz.de/) is much shorter. Another common pattern is to display prev/next buttons **next to the progress dots**, under the carousel. The only potential issue is that some users might not understand that the visible sections are only a part of all available options and scroll down too quickly.

Notice the **grouping of prev/next buttons** in the last example. In fact, it seems to be a very good idea, as it aids users in navigation back and forth quickly without having to re-calibrate their mouse pointer or their fingers. Both options are close to each other, so **going back and forth is faster** than traveling all the way to another side of the carousel, and then back. Also, the option eliminates mishaps or misclicks. 

{{< rimg breakout="true" href="https://ritual.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca5d7716-7816-4c68-a3a3-5dd4f222f38a/32-designing-better-carousel-ux.png" width="800" height="387" sizes="100vw" caption="<a href='https://ritual.com'>Ritual.com</a> groups prev/next buttons and integrated them in the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca5d7716-7816-4c68-a3a3-5dd4f222f38a/32-designing-better-carousel-ux.png'>Large preview</a>)" alt="Another example with arrows being used to click through testimonials presented on the Ritual.com website" >}}

Arrows in use for testimonials on [Ritual.com](https://ritual.com), beautifully integrated into the design, with videos and text snippets appearing as the user is sliding between the slices of the carousel. The arrows are grouped, but since no progress dots are used, they are positioned closer to the images. With this approach, it’s critical that hit target areas for arrows are **large enough** to prevent mistakes.

With 62 CSS pixels in width and height, it’s more than generous for precise input. Users can focus on a particular area, slightly **detached from but connected to the the actual slides** of the carousel, and click through precisely and predictably. A great example.

{{< rimg breakout="true"  href="https://overpass.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ee90827-5c43-49e1-b3a5-080be7da5ab0/36-designing-better-carousel-ux.png" width="800" height="" sizes="100vw" caption="<a href='https://overpass.com/'>Overpass</a> with a vertical carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ee90827-5c43-49e1-b3a5-080be7da5ab0/36-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

We don’t have to group the buttons horizontally though. On [Overpass](https://overpass.com), the arrows live *within* the carousel, next to description and under the image. A vertical carousel could be an option, too.

**Which one to choose?** Test if grouping the buttons closely to each other will **reduce mistakes** when a carousel is used. The further away the buttons are from each other, the more time consuming and slow the carousel experience will appear to be. The remaining question is whether the buttons should live above the carousel, on it, or under the carousel. And this depends on the device the customer is using. 

## On Desktop, Buttons Live Above The Carousel

There is surely no universal solution, but in my experience, one ends up with fewer usability issues by placing buttons above the carousel. On the one hand, if the carousel lives all the way on the top of the page, we definitely want the prev/next buttons **to be noticed** early. If the buttons live under the carousel, they might not be noticed in time or not noticed at all, especially if carousel slices are very tall.

And if the buttons live right on the slides of the carousel, we end up with **visibility issues of arrows** as they might accidentally match the background color of the slide, and become invisible, or hard to decipher. Plus, users could accidentally jump to the wrong pages by clicking in just the wrong spot. We can solve all these issues with the buttons placed above the carousel.

{{< rimg breakout="true" href="https://ritual.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0213042-ccec-47e1-bce4-2708ec049960/33-designing-better-carousel-ux.png" width="800" height="461" sizes="100vw" caption="Everything is just about right on <a href='https://ritual.com'>Ritual.com</a>.  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0213042-ccec-47e1-bce4-2708ec049960/33-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the Science Team presented on the Ritual.com website with arrows shown on the top right so that users can see further team members" >}}

A good reference example to keep in mind is [Ritual.com](https://ritual.com) mentioned above. The buttons are large. They are grouped. The distance needed to switch directions is minimal. The buttons also live above the carousel on desktop, **leaving enough space for description** to appear under individual images. Swipe gestures are also supported. The buttons and every carousel’s slide are keyboard-accessible. It’s just infinitely more difficult to make mistakes with this design.


## On Mobile, Buttons Live Under The Carousel

What do we do on mobile then? Well, on mobile, displaying prev/next buttons above the carousel is problematic. Depending on the height of the carousel’s slices and the position on the screen, every time a user interacts with the buttons via touch, they might be **covering the content of the carousel** with their fingers. Even the navigation heading in the same direction might make it necessary to lift a finger every time they want to consume content.

On the other hand, vertically center the buttons on the carousel is also problematic because taps are very inaccurate on mobile. Admittedly, as humans, we are [much more precise in the center of the screen](https://www.uxmatters.com/mt/archives/2017/03/design-for-fingers-touch-and-people-part-1.php), but then we need large enough tap areas to avoid mistakes. And the larger tap areas are, the **more space we will be taking away** from our beloved carousels.

{{< rimg breakout="true" href="https://ritual.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55cc3354-e001-4844-8c1a-25adf452526f/34-35-designing-better-carousel-ux.png" width="800" height="768" sizes="100vw" caption="On mobile, arrows are located under the carousel on <a href='https://ritual.com'>Ritual.com</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55cc3354-e001-4844-8c1a-25adf452526f/34-35-designing-better-carousel-ux.png'>Large preview</a>)" alt="The mobile version of the Ritual.com website in which the left and right arrows have been moved to the bottom of the page underneath the carousel" >}}

The only viable option left is to **display prev/next-buttons under the carousel** (on mobile). However, we need to be very cautious about the height of the carousel’s slices: they should never take up more **45–50% of the screen**. This sounds like a magic number, but research shows that on mobile, we tend to interact with pages by [reading and swiping and scrolling in the center of the screen](https://www.uxmatters.com/mt/archives/2017/03/design-for-fingers-touch-and-people-part-1.php).

If a user scrolls down to explore the carousel, we should expect them to spot the prev/next buttons because they will be in view. Plus, every time a user interacts with the carousel, their **fingers will be far away** from the carousel, so we shouldn’t be expecting accidental clicks/taps. Problems solved.

In summary, as long as the prev/next buttons are **clearly detached from the content** of the carousels and have a large tap area, they can be centered vertically and live on the edges of the carousel. For faster navigation forwards and backwards, we can place the buttons above the carousel on desktop, and under the carousel on mobile. This is just the least likely option to produce accidental mistakes.

## Combine Tabs and Carousels

Usually, carousels are presenting content that users don’t have much control about. One way to make the carousel slightly more relevant is by **adding filters to the carousels**, allowing users to choose what exactly they’d love to see.

{{< rimg breakout="true" href="https://www.reuters.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2129a57a-c68b-46f8-8918-eefdcdbd30d7/38-designing-better-carousel-ux.png" width="800" height="" sizes="100vw" caption="<a href='https://www.reuters.com'>Reuters.com</a> combines filters and a carousel with arrows grouped in the right upper corner, above the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2129a57a-c68b-46f8-8918-eefdcdbd30d7/38-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

On [Reuters.com](https://www.reuters.com), cards, tabs and a carousel complement each other, with the prev/next buttons to control the carousel placed in the upper right corner of the section. A great way to encourage users to click through **topics of interest** and explore available options &mdash; and also jump straight to the category with the “See all World” button. On mobile, the arrows jump under the carousel.

{{< rimg breakout="true" href="https://www.bfs.admin.ch/bfs/en/home.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44dc5b69-4afe-4eaf-b3b0-029b04bb8ce6/40-designing-better-carousel-ux.png" width="800" height="382" sizes="100vw" caption="<a href='https://www.bfs.admin.ch/bfs/en/home.html'>Federal Statistical Office in Switzerland</a> uses tabs instead of progress dots or thumbnails. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44dc5b69-4afe-4eaf-b3b0-029b04bb8ce6/40-designing-better-carousel-ux.png'>Large preview</a>)" alt="An example of a carousel used in the form of tabs to switch to different topics and sub-categories of the site" >}}

[Federal Statistical Office in Switzerland](https://www.bfs.admin.ch/bfs/en/home.html) relies on tabs to change the slice of the carousel. Initially the carousel auto-advances, but once a user has chosen one of the topics, it stays still. The height of all slices is the same, so there are no visual jumps, and **no transitions** from one side to another. A calm, respectful and functional solution.

{{< rimg breakout="true" href="https://getcruise.com/technology" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6515b28e-8920-49e4-9e7e-a493dac5f8e9/41-42-designing-better-carousel-ux.png" width="800" height="355" sizes="100vw" caption="Horizontal slider on desktop, prev/next buttons on mobile: <a href='https://getcruise.com/technology'>Getcruise.com</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6515b28e-8920-49e4-9e7e-a493dac5f8e9/41-42-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

On [GetCruise.com](https://getcruise.com/technology), a tiny horizontal slider appears under the carousel, and the pointer changes to a custom indicator. The latter highlights that the area is draggable. In such a case, of course, the content area should be scrollable with a keyboard alone as well. On mobile, **two arrows appear above the carousel**, allowing users to jump between topics. No progress dots or sliders are in sight. This could work, too.

## Use Thumbnails Or Icons To Encourage Click-Throughs

The more relevant content we can display to encourage users to act on them, the higher click-through rates we should be expecting. Rather than using labels, [Weber Grill Original](https://www.weber.com/DE/de/start/) uses **thumbnails** to highlight their recipes. This is probably going to work better than lifeless dots.  

{{< rimg breakout="true" href="https://www.weber.com/DE/de/start/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbb3295-2d34-4287-a969-b0e7226bfb0a/43-designing-better-carousel-ux.png" width="800" height="454" sizes="100vw" caption="<a href='https://www.weber.com/DE/de/start/'>Weber</a> with thumbnails indicating slices of the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbb3295-2d34-4287-a969-b0e7226bfb0a/43-designing-better-carousel-ux.png'>Large preview</a>)" alt="The front page of Weber Grill’s website showing different recipes in German, in this particular case, Baumkuchen being the prominent one covering the entire page while other recipes are presented as much smaller images and function as part of the carousel" >}}

More of a tabbed navigation than a carousel: [Philips.de](https://www.philips.be/). Icons requires less space, but can be mysterious if not chosen properly. Text labels could be a good compliment to the design, and either way they need to be communicated to screen reader users. Unfortunately, the carousel is auto-advancing, and there is no way to pause or stop it &mdash; even when hovering or focusing on the individual slices.

{{< rimg breakout="true" href="https://www.philips.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b86f3eb7-9de4-43af-9524-13bff18a0137/44-designing-better-carousel-ux.png" width="800" height="462" sizes="100vw" caption="<a href='https://www.philips.de/'>Philips.de</a>, relying on icons for their carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b86f3eb7-9de4-43af-9524-13bff18a0137/44-designing-better-carousel-ux.png'>Large preview</a>)" alt="An example of a carousel taken from the Philips.de website using icons instead of standard left and right arrows" >}}

## Dragging Alone Isn’t Good Enough

While some implementations rely on progress indicators, others rely on prev/next buttons and others rely on thumbnails, there are plenty of implementations that heavily rely on a single mode of interaction: **dragging**. Surely users do understand how to drag items on the screen, yet making dragging accessible is nothing short of impossible.

{{< rimg breakout="true" href="https://leaddev.com/leadership-skills/being-available-secret-great-leadership" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4948926d-c9d4-45a7-aebf-03ccf2b5797c/45-designing-better-carousel-ux.png" width="800" height="357" sizes="100vw" caption="<a href='https://leaddev.com/leadership-skills/being-available-secret-great-leadership'>LeadDev</a>’s carousel for related articles combines a horizontal slider with a green pointer that indicates that the carousel can be dragged left and right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4948926d-c9d4-45a7-aebf-03ccf2b5797c/45-designing-better-carousel-ux.png'>Large preview</a>)" alt="The LeadDev website shows a different kind of carousel in which an icon is shown with both left and right arrows along with a horizontal bar underneath" >}}

We definitely need to support **swiping gestures** on mobile, but this shouldn’t be the only method to navigate the carousel. On [LeadDev](https://leaddev.com/leadership-skills/being-available-secret-great-leadership), related articles are highlighted with a horizontal bar and a large green icon that indicate that a user can scroll left and right. Adding arrows to jump left and right might help users be more precise in their jumps.

{{< rimg breakout="true" href="https://magasinsgeneraux.com/fr/espaces/passage" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d41cbd70-2c55-422a-94bf-24ffad495ed6/46-designing-better-carousel-ux.png" width="800" height="449" sizes="100vw" caption="On <a href='https://magasinsgeneraux.com/fr/espaces/passage'>Magasins Generaux</a>, the only way to browse the gallery is by dragging. This is inaccessible for keyboard users and screen reader users. <a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d41cbd70-2c55-422a-94bf-24ffad495ed6/46-designing-better-carousel-ux.png'>Large preview</a>)" alt="An example of a draggable icon to view the entire gallery on the given page" >}}

On [Magasins Generaux](https://magasinsgeneraux.com/fr/espaces/passage), the draggable icon is the only indicator that an image gallery is draggable. Admittedly, this isn’t a carousel, but unfortunately, the slides **aren’t keyboard-accessible**, and tabbing through the content brings users from the last link in the article to the footer. It should be possible to navigate to each image and announce its alternative text.

## Add An Information Scent to The Carousel

One of the common issues in the carousel is the **discoverability of slices** that are coming in late in the carousel. One way of ensuring that users understand that they didn’t see everything just yet, is by adding some sort of information sent to the last visible slides or upcoming slides.

{{< rimg breakout="true" href="https://web.archive.org/web/20190806035037/https://neufuntrois.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72851e8-880c-4b86-9752-745e3c038667/47-designing-better-carousel-ux.png" width="800" height="489" sizes="100vw" caption="<a href='https://web.archive.org/web/20190806035037/https://neufuntrois.com/'>Neufuntrois.com</a> used to have a lovely carousel, indicating previous and upcoming slices. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72851e8-880c-4b86-9752-745e3c038667/47-designing-better-carousel-ux.png'>Large preview</a>)" alt="An example taken from the Neufuntrois.com website in which different shapes and sizes are used in the carousel for the user to navigate through" >}}

[Neufuntrois.com](https://web.archive.org/web/20190806035037/https://neufuntrois.com/) is a beautiful restaurant website with different shapes used as carousel slices. Previous and next slides are cut off, making it very obvious to users that this content can be discovered.

Scroll back to the [previous section](#dragging-alone-isn-t-good-enough) and compare the first example to the second. You might find a **significant difference**. While the first example provides an information scent to the users, the second does not. Some browsers don’t display scrollbars, and on some screens, you might be hitting just the wrong resolution, so users won’t get any clues that some useful content is currently hidden and is just one swipe away.

{{< rimg breakout="true" href="https://www.srf.ch/news/international/wahl-in-frankreich-macron-laut-hochrechnungen-vor-le-pen-entscheid-in-stichwahl" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4020f4a-af8b-4187-a387-84432a3996db/48-designing-better-carousel-ux.png" width="800" height="372" sizes="100vw" caption="<a href='https://www.srf.ch/news/international/wahl-in-frankreich-macron-laut-hochrechnungen-vor-le-pen-entscheid-in-stichwahl'>SRF.ch</a>, with a fade-out for the last slide in the carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4020f4a-af8b-4187-a387-84432a3996db/48-designing-better-carousel-ux.png'>Large preview</a>)" alt="SRF.ch, a Swiss news website, shows the current topics and news with the help of arrows grouped and displayed on the sides with upcoming/further posts faded out" >}}

On [SRF](https://www.srf.ch/news/international/wahl-in-frankreich-macron-laut-hochrechnungen-vor-le-pen-entscheid-in-stichwahl), prev/next buttons are grouped and displayed on the right edge of the carousel, next to an upcoming slice which **fades out**. This makes it quite obvious that the user hasn’t seen all slides just yet, and can explore them if needed.

It’s a good idea to make sure that the last visible slide is either **cropped or fades out**, or use any other visual clue, also called *information scent*, that there is something out there to be discovered. If we don’t use any progress bar, nor indicate the overall number of slices, nor use any prev/next-buttons, we shouldn’t be expecting users understanding how the carousel works. If you want to avoid usability issues, **sprinkle a bit of information scent** on your carousel &mdash; your users might appreciate it.

{{% ad-panel-leaderboard %}}

## Avoid Auto-Advancing, Or Add At Least 5–7s Delay

Auto-advancing carousels **temper with users’ patience and their priorities**. Just like we’ve learned to ignore advertising banners, we tend to dismiss anything that’s blinking, moving or distracting us. This is true especially on mobile devices where users often scroll past the carousel too quickly to even notice that it’s actually auto-advancing. Any kind of unexpected movement rarely brings more attention to the carousel, but rather **drives the attention away** &mdash; both on mobile and on desktop.

However, if you *absolutely* need auto-advancing to draw and keep user’s interest, we could make it work as well — with a solid delay of **5–7s for each slide**.

{{< rimg breakout="true" href="http://www.7h34.fr/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69d20687-9de5-4021-bd7a-1e2d0146b43a/49-designing-better-carousel-ux.png" width="800" height="476" sizes="100vw" caption="<a href='http://www.7h34.fr/'>7h34.fr</a> with an auto-advancing carousel and a decent delay of 5s. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69d20687-9de5-4021-bd7a-1e2d0146b43a/49-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of a French website, 7h34.fr, that uses a circular interactive carousel" >}}

[7h34](http://www.7h34.fr), a lovely design agency website with a circular carousel, that flips clockwise. Users can also scroll up and down to jump through the slices of the carousel. The delay between auto-advancing is around **5s**.

{{< rimg breakout="true" href="https://store.google.com/us/product/pixel_buds_a_series?hl=en-US" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5757b8-9a2f-46a2-af39-96d765361535/50-designing-better-carousel-ux.png" width="800" height="524" sizes="100vw" caption="<a href='https://store.google.com/us/product/pixel_buds_a_series?hl=en-US'>Google Pixel Buds</a> with an auto-advancing carousel and each slide being filled in for 6s. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5757b8-9a2f-46a2-af39-96d765361535/50-designing-better-carousel-ux.png'>Large preview</a>)" alt="A photo of the Google Pixel Buds presented with labels" >}}

One way to improve it is to **set the right expectations** early on, so users get a sense about when the next slide of the carousel should be expected. [Google Pixel Buds](https://store.google.com/us/product/pixel_buds_a_series?hl=en-US), for example, is auto-advancing and contains labels. The progress indicator is being filled gradually and slowly, with a **6s delay for each slide,** providing enough time to act on the current slide, scroll down or leave the page altogether, without being interrupted along the way.

{{< rimg breakout="true" href="https://timeless.ee/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3da7daee-c608-49f0-a7b8-d3bac2fbb95e/51-designing-better-carousel-ux.png" width="800" height="491" sizes="100vw" caption="<a href='https://timeless.ee/'>Timeless.ee</a> uses a transition on the titles of its Estonian trolleybuses. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3da7daee-c608-49f0-a7b8-d3bac2fbb95e/51-designing-better-carousel-ux.png'>Large preview</a>)" alt="A screenshot of the Estonian Timeless.ee landinge page showing a trolley bus named Ikarus 55-14 Lux in which the title is half-filled in black color indicating the how many seconds left until the next trolley bus is presented" >}}

[Timeless.ee](https://timeless.ee/) uses trolley buses’ names that get filled in as the carousel is auto-advancing. The latter cycles through retro trolleybuses in Estonia available for booking or hiring. Like in the previous example, the **filling speed** indicates when the next slide should be expected. For some names, it takes slightly longer to fill in the name, but it’s always beyond **5s**.
 
{{< rimg breakout="true" href="https://www.ferrari.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f23d1b7-5185-42c1-bac2-7f5d7e367648/52-designing-better-carousel-ux.png" width="800" height="494" sizes="100vw" caption="<a href='https://www.ferrari.com/de-DE'>Ferrari.com</a> highlights a current position in the carousel and uses a little circular indicator. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f23d1b7-5185-42c1-bac2-7f5d7e367648/52-designing-better-carousel-ux.png'>Large preview</a>)" alt="A picture of a red Ferrari sports car on the right with text on the left of the website’s landing page which uses a little circular indicator at the bottom of the page" >}}

[Ferrari.com](https://www.ferrari.com/de-DE) highlights a current position in the carousel and uses a **little circular indicator** to explain that the carousel will auto-advance when the time expires. Ferrari also uses a **7s delay**. Unfortunately, here it’s impossible to pause auto-rotation.

{{< rimg breakout="true" href="https://casper.com/mattresses/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdb1ec71-67a9-4840-846d-a4e4f6ea581c/53-designing-better-carousel-ux.png" width="800" height="387" sizes="100vw" caption="<a href='https://casper.com/mattresses/'>Casper.com</a> shows and hides sections of the accordion in the left sidebar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdb1ec71-67a9-4840-846d-a4e4f6ea581c/53-designing-better-carousel-ux.png'>Large preview</a>)" alt="An image in the background advertising a bed mattress with a carousel on the left side of the page shown in longer and shorter bars" >}}

A slightly unusual auto-advancing experience on [Casper.com](https://casper.com/mattresses/), with the left bar growing, and accordions collapsing and expanding. The image doesn’t change as the text gets hidden and revealed. The delay for this experience is also **7s**.

As Christian Holst [has written previously](https://www.smashingmagazine.com/2016/07/ten-requirements-for-making-home-page-carousels-work-for-end-users/):

<blockquote>“The amount of text in a slide should largely determine the duration of a slide’s visibility. If it’s just a short heading, 5 to 7 seconds proved to be appropriate in our tests, whereas longer durations were needed for more text-heavy slides. (Nielsen Norman Group recommends 1 second <a href="https://www.nngroup.com/articles/designing-effective-carousels/">per 3 words</a> for auto-rotating slides.) One consequence of this is that you might need to assign unique durations to individual slides, showing some slides longer than others.”</blockquote>

## Always Include A “Pause” Button For Auto-Advancing Carousels

If it’s absolutely critical to include an auto-advancing behavior for one reason or another, consider what goals the carousel is trying to achieve. Chances are high that a carousel won’t help you bring good leads or effective clicks. If it’s absolutely necessary, however, please make sure to include a **“Pause” button** as well, so users have an option to pause auto-rotation.

{{< rimg breakout="true" href="https://www.walmart.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22b66eda-ed55-4e3e-9385-5d75a7a73208/55-56-designing-better-carousel-ux.png" width="800" height="356" sizes="100vw" caption="<a href='https://www.walmart.com'>Walmart.com</a> uses a carousel that auto-advances within a few seconds but it is unclear how many products are available or will be shown. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22b66eda-ed55-4e3e-9385-5d75a7a73208/55-56-designing-better-carousel-ux.png'>Large preview</a>)" alt="The Walmark website uses a carousel that auto-advances within a few seconds but it is unclear how many products are available or will be shown" >}}

A great example of the implementation is [Walmart.com](https://www.walmart.com) (above). The carousel auto-advances slowly, but **only if users don’t act on any of the images**. Most importantly, there is a visible **“Pause” button** both on mobile and desktop and there is a focus/active state on the slider as well. Unfortunately, it’s a bit hard to say how many items are available in the carousel. Numbers would probably help here.

It goes without saying that **auto-rotation should stop entirely when a user interacts** with a slice of the carousel, be it by hovering, focusing, or tapping through available options. Interrupting the exploration of selected items is a safe way to drive users away from the carousel for good.

## Alternatives to Carousels

With all of these considerations in mind, one might assume that carousels are often the best solution. But that’s quite unlikely to be true. Personally, I’m yet to see a carousel that slashes all expectations by large and drives KPIs through the roof. In corporate environment where I often find myself, nobody really trusts me. I always have to argue about design decisions based on evidence coming from usability and accessibility tests, and rely on business metrics to drive these decisions.

**Carousels rarely help in driving these metrics** — mostly because they hide relevant content and hence make it less accessible. Cards, teasers, buttons, navigation all would probably work better for navigation. However, when it comes to highlighting features or products or offerings, rather than navigation options, they might work as well. If you have a strong feeling that a carousel **isn’t really working**, or is just the wrong component to use, run a test on a Saturday morning when there might be less traffic, and build up a case highlighting that another design might be driving higher KPIs.

{{< rimg breakout="true" href="https://ra.co/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7703e762-7364-4399-98d2-92c45a0b6798/57-designing-better-carousel-ux.png" width="800" height="707" sizes="100vw" caption="<a href='https://ra.co/'>Resident Advisor</a> highlights recent news without a carousel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7703e762-7364-4399-98d2-92c45a0b6798/57-designing-better-carousel-ux.png'>Large preview</a>)" alt="An example of a website using a ‘View more features’ button to allow users to click in order to see more" >}}

In fact, there is no shortage of alternatives to carousels, and often they are quite easy to implement. [ResidentAdvisor](https://ra.co/) avoid carousels altogether, highlight three last features, and invites users to explore more with a “View more features” button. The button could be loading more items or moving users to a separate page. A predictable and calm design that shows just enough text and visuals to entice a user to dive in.

{{< rimg breakout="true" href="https://auspost.com.au/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19ed2f90-1c1a-4801-9b7a-361b10a0809f/58-designing-better-carousel-ux.png" width="800" height="376" sizes="100vw" caption="<a href='https://auspost.com.au'>Australia Post</a> uses a dynamic layout to highlight features. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19ed2f90-1c1a-4801-9b7a-361b10a0809f/58-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

Instead of using a carousel, [Australia Post](https://auspost.com.au/) uses a dynamic layout to highlight all features together in the same area. There are some carousels in use on the page as well, but hiding features in the carousel would make them inaccessible to at least some users who’d just quickly scroll past it.

{{< rimg breakout="true" href="https://168plymouth.com/#features" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46763930-e524-48a7-942e-c1a438eb60b0/59-designing-better-carousel-ux.png" width="800" height="533" sizes="100vw" caption="<a href='https://168plymouth.com/#features'>168plymouth.com</a> with mini-carousels used as galleries. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46763930-e524-48a7-942e-c1a438eb60b0/59-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

[168plymouth](https://168plymouth.com/#features) uses **mini-carousels** for each feature that they want to highlight. There is no rotation, no auto-advancing, and you can move only in a single direction &mdash; moving backward might not be necessary with just 4 images that every panel contains.

{{< rimg breakout="true" href="https://www.deutsches-museum.de/museumsinsel/programm/programm-a-z" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3817456a-636d-4bd1-8996-0249f1856ebd/60-designing-better-carousel-ux.png" width="800" height="424" sizes="100vw" caption="<a href='https://www.deutsches-museum.de/museumsinsel/programm/programm-a-z'>Deutsches Museum</a> uses the load more pattern to load in more items if needed. No carousel in use. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3817456a-636d-4bd1-8996-0249f1856ebd/60-designing-better-carousel-ux.png'>Large preview</a>)" alt="" >}}

[Deutsches Museum](https://www.deutsches-museum.de/museumsinsel/programm/programm-a-z) uses the “load more” pattern to show more items if needed. This makes the front page quite compact, without too many items appearing all over the page at a given time.

All of it is to say that **not every page needs a carousel**, and very often it might be a wrong and unnecessary pattern to use &mdash; so be cautious when using it, and explore alternatives as a part of your design process.

## Wrapping Up

Carousels have many accessibility and usability issues, from discoverability to accessibility. In a way, very much like [accordions](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/), they provide a way to **show and hide some pieces of content** &mdash; either manually or automatically. And that’s not something that many other components have.

When designing your next carousel, think about whether it could be replaced with another design pattern that would be serving **content discoverability** slightly better. If it’s out of the question, consider replacing progress indicators with labels or thumbnails. Indicate the current slice of the carousel. Include and group prev/next buttons and display them above or below the carousel. Use numbers to explain where users are and how far they can go. Resist auto-advancing as much as you can, and if you can’t, add a delay of 7s and allow users to pause rotation.

## Carousel UX Checklist

As usual, here’s a general checklist of a few **important guidelines to consider** when designing better carousels:

- Choose the **sequence of slides** carefully.
- Most important slides always come first.
- Limit the height of the slides to 45-50% of the screen’s height (max).
- Slides shouldn’t rotate too quickly (min delay of 5–7s).
- Try to **avoid auto-rotation** on mobile.
- Always pause auto-rotation on hover, stop on interaction.
- Don’t rely on dragging the carousel alone.
- Make sure the slides are keyboard-accessible.
- Always support swipe gestures on mobile.
- Always **indicate a slice** of the upcoming slide.
- Always show at which slide a user currently is.
- Consider replacing progress dots with labels, thumbnails, **key highlights**.
- On desktop, group prev/next steps and display them above the carousel.
- On mobile, group prev/next steps and display them below the carousel.
- **Combine carousels with navigation**, tabs, or filters.


## Meet Smart Interface Design Patterns

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 0"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.

## Useful Resources

- “[Designing Effective Carousels](https://www.nngroup.com/articles/designing-effective-carousels/),” Kara Pernice, Nielsen Norman Group 
- “[Auto-Forwarding Carousels and Accordions Annoy Users and Reduce Visibility](https://www.nngroup.com/articles/auto-forwarding/),” Jakob Nielsen, Nielsen Norman Group
- “[Creating Effective Carousels](https://www.uxmatters.com/mt/archives/2019/07/creating-effective-carousels.php),” Steven Hoober, UX Matters
- “[10 UX Requirements for a User-Friendly Homepage Carousel Design](https://www.smashingmagazine.com/2016/07/ten-requirements-for-making-home-page-carousels-work-for-end-users/),” Christian Holst and Jamie Appleseed, Baymard Institute

If you find this article useful, here’s an overview of similar articles we’ve published over the years &mdash; and a few more are coming your way.

### Related Articles

- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing Perfect Breadcrumbs](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)
- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- “[Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/),” written by Adam Silver

<!-- 
{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a64181b0-f314-4c3a-ab20-1aa142a5c53d/32-33-designing-better-carousel-ux.png" width="800" height="479" sizes="100vw" caption="Arrows in different positions: <a href='https://www.artmuseumgr.org/'>Gram Museum</a>, <a href='https://teatrlalka.pl/en/spektakle/rycerz-gwiazdy-wigilijnej/galeria/2'>Teatr Lalka</a> and <a href='https://www.ritual.com'>Ritual</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a64181b0-f314-4c3a-ab20-1aa142a5c53d/32-33-designing-better-carousel-ux.png'>Large preview</a>)" alt="A comparison of three websites as displayed on mobile devices" >}} -->

{{< signature "il" >}}
