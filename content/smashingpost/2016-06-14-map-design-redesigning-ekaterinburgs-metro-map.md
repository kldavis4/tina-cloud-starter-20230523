---
title: 'Map Design: Redesigning Ekaterinburg’s Metro Map'
slug: map-design-redesigning-ekaterinburgs-metro-map
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7e30790-f537-408e-b98c-932cefc63da9/ekaterinburg-metro-map-image16-preview-opt.jpg
date: 2016-06-14T22:00:09.000Z
author: ilyabirman
description: >-
  A large metropolitan underground train network might as well be a
  teleportation device: People don’t care how it gets them from A to B, just
  that it does. In London, Paris and Moscow, the map of the metro does not show
  surface geography, because there is not much empty space on the sheet.

  Designing a city’s metro map is quite a challenging task, even when there is
  just one line. Last year, my colleague Pasha Omelekhin and I were thrilled to
  work on the redesign of the metro map for Ekaterinburg, Russia. We had fun (he
  designed, I directed). In this article, we’ll cover our design process. It’s
  going to be detailed, so, depending on your interests, this might be very
  boring or very exciting. Still, we’ve left out so much. We hope this helps in
  case you have to work on a similar project.
categories:
  - UX
  - Graphic Design
  - UX
---
A large metropolitan underground train network might as well be a teleportation device: People don’t care how it gets them from A to B, just that it does. In London, Paris and Moscow, the map of the metro does not show surface geography, because there is not much empty space on the sheet.

Designing a city’s metro map is quite a challenging task, even when there is just one line. Last year, my colleague Pasha Omelekhin and I were thrilled to work on the redesign of the metro map for Ekaterinburg, Russia. We had fun (he designed, I directed). In this article, we’ll cover our design process. It’s going to be detailed, so, depending on your interests, this might be very boring or very exciting. Still, we’ve left out so much. We hope this helps in case you have to work on a similar project.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Paris Metro Map – The Redesign](https://www.smashingmagazine.com/2017/01/redesigning-the-paris-metro-map/)
*   [The Joy Of Illustrated Maps In The Era Of Google Earth](https://www.smashingmagazine.com/2013/07/illustrated-maps-in-era-of-google-earth/)
*   [A Guide To Building SVG Maps From Natural Earth Data](https://www.smashingmagazine.com/2015/09/making-svg-maps-from-natural-earth-data/)
*   [Entering The Wonderful World of Geo Location](https://www.smashingmagazine.com/2010/03/entering-the-wonderful-world-of-geo-location/)

Let’s dive in!

{{% feature-panel %}}

## The Approach

This is the final map we created:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa86eae4-e10b-4361-9cf7-06c2ab0fb921/ekaterinburg-metro-map-image38-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/896ea5c7-d042-461e-906b-333a63285654/ekaterinburg-metro-map-image38-opt.png" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa86eae4-e10b-4361-9cf7-06c2ab0fb921/ekaterinburg-metro-map-image38-large-opt.png">View large preview</a>)</figcaption></figure>

Just for comparison, here’s what the previous version of map looked like:

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d553d83-55ab-4550-8ab0-b90cd0da3961/ekaterinburg-metro-map-image11-opt.jpg" alt="" /></figure>

The solid-green line above is the only existing subway line; the other two are merely “planned” lines, for which construction has not even started. Displaying all three would not make sense. So, our first sketch was a simple one-line diagram:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57a6b90-15c8-4d4e-9ce7-07ca09e2d69a/ekaterinburg-metro-map-image23-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57a6b90-15c8-4d4e-9ce7-07ca09e2d69a/ekaterinburg-metro-map-image23-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57a6b90-15c8-4d4e-9ce7-07ca09e2d69a/ekaterinburg-metro-map-image23-large-opt.jpg">View large preview</a>)</figcaption></figure>

Usually in a multi-line metro network, on each metro line they have a separate one-line diagram displayed above train doors. But here, one diagram could be used as both the full-network diagram and the line diagram. Small refinements would need to be made, and we did make them, but we wanted to rethink how such a diagram would be designed in general.

As mentioned, metropolitan centers with large underground networks, such as London, Paris and Moscow, do not show surface geography in their subway maps. There is simply not enough room to do so. Not so for small metros. Simplicity and lack of surface detail are only required when a rich map would get in the way of people finding their route. Ekaterinburg does not have this problem.

When there is just one subway line, you can’t afford to portray the system like a teleportation device. People have to use multiple modes of transportation to get to where they want to go. So, we wanted to show how the metro was connected to everything else.

A long time ago, the map of Paris’s underground was simply laid over top a city map:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbd29e5-3c3d-433f-a5b8-008c9d0d5446/ekaterinburg-metro-map-image16-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7e30790-f537-408e-b98c-932cefc63da9/ekaterinburg-metro-map-image16-preview-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbd29e5-3c3d-433f-a5b8-008c9d0d5446/ekaterinburg-metro-map-image16-large-opt.jpg">View large preview</a>)</figcaption></figure>

We figured that the two approaches could be combined: surface information could be laid over top the linear diagram, making the map both richly informative and suitable for use on trains. This would require us to bend the city in strange ways to fit important landmarks, but this has been known to work, as in the <a href="https://gothamist.com/2007/08/03/michael_hertz_d.php">case of New York City’s underground map</a>.</p>

## The Linear Diagram

Next, we added some streets to the map:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79454526-f934-4afa-99e4-c483a8b4db34/ekaterinburg-metro-map-image15-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79454526-f934-4afa-99e4-c483a8b4db34/ekaterinburg-metro-map-image15-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79454526-f934-4afa-99e4-c483a8b4db34/ekaterinburg-metro-map-image15-large-opt.jpg">View large preview</a>)</figcaption></figure>

The river seemed too dark here. Also, Ekaterinburg is not a popular tourist destination, so the Russian language is far more important than English; therefore, we decided to position the Russian names on the inside and the English translations on the outside relative to the line.

We wanted to experiment with style. We started with an unofficial M logo and cut the station “ticks” at angles to echo it. Later, we replaced the logo with the official one:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc6b734e-2843-4424-8c88-d0fd346cc4ea/ekaterinburg-metro-map-image21-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc6b734e-2843-4424-8c88-d0fd346cc4ea/ekaterinburg-metro-map-image21-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc6b734e-2843-4424-8c88-d0fd346cc4ea/ekaterinburg-metro-map-image21-large-opt.jpg">View large preview</a>)</figcaption></figure>

The gradient didn’t look right. And the logo was too large. So, instead of one large logo, we tried grouping several logos: the metro’s logo, the city’s coat of arms and an emblem of the transportation authority. This kind of thing usually looks cool.

In the end, though, we found that two logos work fine (the city’s logo being one of them):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/555cf5a7-a711-4482-974a-659dd8ee607a/ekaterinburg-metro-map-image05-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/555cf5a7-a711-4482-974a-659dd8ee607a/ekaterinburg-metro-map-image05-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/555cf5a7-a711-4482-974a-659dd8ee607a/ekaterinburg-metro-map-image05-large-opt.jpg">View large preview</a>)</figcaption></figure>

Notice how the river and streets have started morphing to better communicate their relationship with the line. We continued adding more surface geography:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fc7ea51-ba02-48f2-9517-e4d6dce81a5e/ekaterinburg-metro-map-image29-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fc7ea51-ba02-48f2-9517-e4d6dce81a5e/ekaterinburg-metro-map-image29-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fc7ea51-ba02-48f2-9517-e4d6dce81a5e/ekaterinburg-metro-map-image29-large-opt.jpg">View large preview</a>)</figcaption></figure>

Now we had a compass (the left-pointing arrow indicating north), the city’s TV tower and the circus. The line of the airport shuttle from Botanicheskaya was aligned with the angle of the ticks — a modification that would not survive as we made the geography feel more real, but it had its charm. Maybe it would work somewhere else.

We experimented more with the ticks:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449b5c00-1a82-4a9a-b854-81101977dc1b/ekaterinburg-metro-map-image73-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449b5c00-1a82-4a9a-b854-81101977dc1b/ekaterinburg-metro-map-image73-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/449b5c00-1a82-4a9a-b854-81101977dc1b/ekaterinburg-metro-map-image73-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0effa666-a69a-499c-a9a9-379f60b8e36c/ekaterinburg-metro-map-image10-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0effa666-a69a-499c-a9a9-379f60b8e36c/ekaterinburg-metro-map-image10-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0effa666-a69a-499c-a9a9-379f60b8e36c/ekaterinburg-metro-map-image10-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa3e329-18bc-4720-840c-f84e40f0a245/ekaterinburg-metro-map-image44-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa3e329-18bc-4720-840c-f84e40f0a245/ekaterinburg-metro-map-image44-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa3e329-18bc-4720-840c-f84e40f0a245/ekaterinburg-metro-map-image44-large-opt.jpg">View large preview</a>)</figcaption></figure>

We even played with long shadows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d538cdf-8fd4-40dc-828e-19fba8412214/ekaterinburg-metro-map-image03-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d538cdf-8fd4-40dc-828e-19fba8412214/ekaterinburg-metro-map-image03-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d538cdf-8fd4-40dc-828e-19fba8412214/ekaterinburg-metro-map-image03-large-opt.jpg">View large preview</a>)</figcaption></figure>

Some of these were nice, but still not special in any way.

Ekaterinburg is characterized by <a href="https://en.wikipedia.org/wiki/Constructivism_(art)">constructivist</a> architecture. What could we use to hint at this in the map? We sought inspiration from the art of Malevich and Kandinsky.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/409e48a5-2e5c-4df8-8962-ac45247c5d28/ekaterinburg-metro-map-image19-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/409e48a5-2e5c-4df8-8962-ac45247c5d28/ekaterinburg-metro-map-image19-large-opt.jpg" alt="" /></a></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc29e093-9a93-455b-9bd9-2531f09adb33/ekaterinburg-metro-map-image63-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc29e093-9a93-455b-9bd9-2531f09adb33/ekaterinburg-metro-map-image63-large-opt.jpg" alt="" /></a><figcaption>Pasha said, "I guess this is how Malevich would do an airport icon."</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42565d40-8fc2-4917-b878-bb20b736e699/ekaterinburg-metro-map-image48-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42565d40-8fc2-4917-b878-bb20b736e699/ekaterinburg-metro-map-image48-large-opt.jpg" alt="" /></a><figcaption>A similarly crazy train</figcaption></figure>

It might work!

We tried to add to the semblance of reality by laying the streets over top the metro line:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d5e1d8-2b3d-439b-ba38-a60bda1d0fdf/ekaterinburg-metro-map-image40-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d5e1d8-2b3d-439b-ba38-a60bda1d0fdf/ekaterinburg-metro-map-image40-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d5e1d8-2b3d-439b-ba38-a60bda1d0fdf/ekaterinburg-metro-map-image40-large-opt.jpg">View large preview</a>)</figcaption></figure>

But this looked like a mistake. Undo!

## Bending The Line

Drawing the metro line straight would be ideal, but it would distort the city too much. So, we introduced bends to hint at the line’s true form:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88117464-041d-4daa-97ba-cc5d81008b80/ekaterinburg-metro-map-image52-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88117464-041d-4daa-97ba-cc5d81008b80/ekaterinburg-metro-map-image52-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88117464-041d-4daa-97ba-cc5d81008b80/ekaterinburg-metro-map-image52-large-opt.jpg">View large preview</a>)</figcaption></figure>

This looked broken. We wanted the line to be smoother. Bye-bye, angled ticks!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c63d228d-a900-4eb4-a66e-df23648edf22/ekaterinburg-metro-map-image13-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c63d228d-a900-4eb4-a66e-df23648edf22/ekaterinburg-metro-map-image13-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c63d228d-a900-4eb4-a66e-df23648edf22/ekaterinburg-metro-map-image13-large-opt.jpg">View large preview</a>)</figcaption></figure>

Having gotten a taste of the geography influencing the form of the line, we wanted more of it, much more — roads, squares, parks, plants, the whole city. We started imagining how to add parks with nice trees and how to give the river a wavy texture.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf400ec1-d2d2-489f-bffb-3d95fd4ff24e/ekaterinburg-metro-map-image46-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf400ec1-d2d2-489f-bffb-3d95fd4ff24e/ekaterinburg-metro-map-image46-large-opt.jpg" alt="" /></a><figcaption>First attempt (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf400ec1-d2d2-489f-bffb-3d95fd4ff24e/ekaterinburg-metro-map-image46-large-opt.jpg">View large preview</a>)</figcaption></figure>

Now that we were getting more into the geography, the ticks were becoming a problem. They looked like they were pointing in the direction of the station exits, rather than the station names, which might confuse people. A new indicator was needed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfcd0ba6-8788-4dc3-a475-e9acd2750f70/ekaterinburg-metro-map-image60-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfcd0ba6-8788-4dc3-a475-e9acd2750f70/ekaterinburg-metro-map-image60-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfcd0ba6-8788-4dc3-a475-e9acd2750f70/ekaterinburg-metro-map-image60-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e119cb3-40f8-4d0b-9b66-f855af834010/ekaterinburg-metro-map-image26-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e119cb3-40f8-4d0b-9b66-f855af834010/ekaterinburg-metro-map-image26-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e119cb3-40f8-4d0b-9b66-f855af834010/ekaterinburg-metro-map-image26-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b68aa40-2274-4f42-a26e-7bc7866c274b/ekaterinburg-metro-map-image59-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b68aa40-2274-4f42-a26e-7bc7866c274b/ekaterinburg-metro-map-image59-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b68aa40-2274-4f42-a26e-7bc7866c274b/ekaterinburg-metro-map-image59-large-opt.jpg">View large preview</a>)</figcaption></figure>

Did the circles have to be on the line? What if we put them closer to the station’s name?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a4cc21d-7f95-4064-bf0d-fc49d9f10907/ekaterinburg-metro-map-image53-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a4cc21d-7f95-4064-bf0d-fc49d9f10907/ekaterinburg-metro-map-image53-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a4cc21d-7f95-4064-bf0d-fc49d9f10907/ekaterinburg-metro-map-image53-large-opt.jpg">View large preview</a>)</figcaption></figure>

Wait a minute! What if we <em>did</em> indicate the location of station exits?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a78472-5eda-4773-a3e7-a11e40b05c3a/ekaterinburg-metro-map-image02-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a78472-5eda-4773-a3e7-a11e40b05c3a/ekaterinburg-metro-map-image02-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a78472-5eda-4773-a3e7-a11e40b05c3a/ekaterinburg-metro-map-image02-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a45f335-54bb-4cae-ab30-53a1da739efa/ekaterinburg-metro-map-image34-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a45f335-54bb-4cae-ab30-53a1da739efa/ekaterinburg-metro-map-image34-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a45f335-54bb-4cae-ab30-53a1da739efa/ekaterinburg-metro-map-image34-large-opt.jpg">View large preview</a>)</figcaption></figure>

These exits were too small for the line and would be not visible from a distance. We needed a solution that screams “Here’s a station!” while subtly indicating the exits.</p>

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba5fb018-36af-4eb9-b362-57dd5c278244/ekaterinburg-metro-map-image25-opt.jpg" alt="" /></figure>

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc8c544-6644-45eb-9e4d-aee6ad6444a2/ekaterinburg-metro-map-image47-opt.jpg" alt="" /></figure>

## More Surface Features

Meanwhile, other work was progressing. The pictogram of the circus became more recognizable:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ccb4fe8-9b2b-43d8-a35c-bd7b12314654/ekaterinburg-metro-map-image17-opt-178x118.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ccb4fe8-9b2b-43d8-a35c-bd7b12314654/ekaterinburg-metro-map-image17-opt-178x118.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ccb4fe8-9b2b-43d8-a35c-bd7b12314654/ekaterinburg-metro-map-image17-opt-178x118.jpg">View large preview</a>)</figcaption></figure>

The abandoned TV tower got more detail:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7472e03-3e01-4e9d-80d5-6a308e8c7ca5/ekaterinburg-metro-map-image65-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7472e03-3e01-4e9d-80d5-6a308e8c7ca5/ekaterinburg-metro-map-image65-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7472e03-3e01-4e9d-80d5-6a308e8c7ca5/ekaterinburg-metro-map-image65-large-opt.jpg">View large preview</a>)</figcaption></figure>

The pictograms of the other modes of transportation got more attention, too:

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ca1185a-d5c9-45ec-a95a-cc699811a654/ekaterinburg-metro-map-image07-opt.jpg" alt="" /></figure>

Oh, and we threw in the surface railway network, as well as a design attribution to ourselves (nestled along the right):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47adf60c-ff10-4eb1-827e-ca02b3695dbb/ekaterinburg-metro-map-image24-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47adf60c-ff10-4eb1-827e-ca02b3695dbb/ekaterinburg-metro-map-image24-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47adf60c-ff10-4eb1-827e-ca02b3695dbb/ekaterinburg-metro-map-image24-large-opt.jpg">View large preview</a>)</figcaption></figure>

The river’s pattern didn’t look good. We tried thin lines reminiscent of the classic London tube map designed by Harry Beck:

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7a5faf5-ae91-4f4f-9c88-68f83874a972/ekaterinburg-metro-map-image56-opt.jpg" alt="" /></figure>

Too thin, almost invisible.

And we continued exploring representations of the station exits on paper:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08b6257c-396b-46cc-a954-db59069c233d/ekaterinburg-metro-map-image31-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08b6257c-396b-46cc-a954-db59069c233d/ekaterinburg-metro-map-image31-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08b6257c-396b-46cc-a954-db59069c233d/ekaterinburg-metro-map-image31-large-opt.jpg">View large preview</a>)</figcaption></figure>

One idea was to lay a detailed scheme of exits over top a semi-transparent metro line:

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0847e764-286a-480c-9f0c-a6bc8a7a6213/ekaterinburg-metro-map-image27-opt.jpg" alt="" /></figure>

## Cleaning Up

At this point, the map was looking quite busy. We decided to show English translations for only the station names. And we removed the circus. We also tried moving the indicators of rail and bus terminals to the corresponding metro stations:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22141e5-89fe-4796-bffe-24b12ed8846a/ekaterinburg-metro-map-image09-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22141e5-89fe-4796-bffe-24b12ed8846a/ekaterinburg-metro-map-image09-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22141e5-89fe-4796-bffe-24b12ed8846a/ekaterinburg-metro-map-image09-large-opt.jpg">View large preview</a>)</figcaption></figure>

The font changed from DIN to PT Sans Metro (a custom version of PT Sans with lowered capital letters).

Here’s an experiment to list surface transportation routes:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6f09b5-3220-407f-bb59-0f6e6f454117/ekaterinburg-metro-map-image20-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6f09b5-3220-407f-bb59-0f6e6f454117/ekaterinburg-metro-map-image20-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6f09b5-3220-407f-bb59-0f6e6f454117/ekaterinburg-metro-map-image20-large-opt.jpg">View large preview</a>)</figcaption></figure>

The street names were the noisiest element at this point. We tried setting them in all-caps:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34864a62-6c49-4d3a-9d97-e7a3693f2426/ekaterinburg-metro-map-image33-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34864a62-6c49-4d3a-9d97-e7a3693f2426/ekaterinburg-metro-map-image33-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34864a62-6c49-4d3a-9d97-e7a3693f2426/ekaterinburg-metro-map-image33-large-opt.jpg">View large preview</a>)</figcaption></figure>

Usually all-caps are inappropriate, particularly in wayfinding: The letters resemble rectangles, making them harder to distinguish. But we wanted the words to look quieter and simpler, so it worked.

We continued experimenting with station exits:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1505649-a688-4786-9d96-5942948e6543/ekaterinburg-metro-map-image62-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1505649-a688-4786-9d96-5942948e6543/ekaterinburg-metro-map-image62-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1505649-a688-4786-9d96-5942948e6543/ekaterinburg-metro-map-image62-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0dbac4-038b-457c-82b6-807e47b4dc12/ekaterinburg-metro-map-image12-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0dbac4-038b-457c-82b6-807e47b4dc12/ekaterinburg-metro-map-image12-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0dbac4-038b-457c-82b6-807e47b4dc12/ekaterinburg-metro-map-image12-large-opt.jpg">View large preview</a>)</figcaption></figure>

We thought the semi-transparent circles were needed to make the stations big enough to be seen from a distance.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79b4a4e5-68b3-4fde-93e0-fda0d7d254c0/ekaterinburg-metro-map-image67-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79b4a4e5-68b3-4fde-93e0-fda0d7d254c0/ekaterinburg-metro-map-image67-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79b4a4e5-68b3-4fde-93e0-fda0d7d254c0/ekaterinburg-metro-map-image67-large-opt.jpg">View large preview</a>)</figcaption></figure>

But having drawn in all of the exits, we realized they were not needed:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad88838-15e7-49a6-89df-86dc1854e40c/ekaterinburg-metro-map-image69-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad88838-15e7-49a6-89df-86dc1854e40c/ekaterinburg-metro-map-image69-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad88838-15e7-49a6-89df-86dc1854e40c/ekaterinburg-metro-map-image69-large-opt.jpg">View large preview</a>)</figcaption></figure>

The fatter semi-transparent line also proved unnecessary:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/975da324-266d-492a-8115-73e1e18aafde/ekaterinburg-metro-map-image43-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/975da324-266d-492a-8115-73e1e18aafde/ekaterinburg-metro-map-image43-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/975da324-266d-492a-8115-73e1e18aafde/ekaterinburg-metro-map-image43-large-opt.jpg">View large preview</a>)</figcaption></figure>

This was not the end of our work with the station exits, but it was an accomplishment.</p>

## Trolley And Bus Icons

The work on listing surface transportation routes carried on:

<figure><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9f4a52e-3598-4bd0-a043-01a682890203/ekaterinburg-metro-map-image57-opt.jpg" alt="" /></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa4fd40a-3783-4ded-8c49-d8eab80fa07d/ekaterinburg-metro-map-image66-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa4fd40a-3783-4ded-8c49-d8eab80fa07d/ekaterinburg-metro-map-image66-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa4fd40a-3783-4ded-8c49-d8eab80fa07d/ekaterinburg-metro-map-image66-large-opt.jpg">View large preview</a>)</figcaption></figure>

The parks got a nice pattern, and the TV tower and river were simplified:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91167632-9389-4966-a678-7318bdbcd984/ekaterinburg-metro-map-image41-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91167632-9389-4966-a678-7318bdbcd984/ekaterinburg-metro-map-image41-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91167632-9389-4966-a678-7318bdbcd984/ekaterinburg-metro-map-image41-large-opt.jpg">View large preview</a>)</figcaption></figure>

## Getting Serious About The Stations

We were still concerned about the visibility of stations from a distance. The exits alone were not enough to make the stations stand out. So, we tried other things:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e3f039c-6e9c-47a7-bc1a-1d645109ff82/ekaterinburg-metro-map-image08-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e3f039c-6e9c-47a7-bc1a-1d645109ff82/ekaterinburg-metro-map-image08-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e3f039c-6e9c-47a7-bc1a-1d645109ff82/ekaterinburg-metro-map-image08-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d2aa850-ca49-41ac-b36a-85b359b221a7/ekaterinburg-metro-map-image18-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d2aa850-ca49-41ac-b36a-85b359b221a7/ekaterinburg-metro-map-image18-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d2aa850-ca49-41ac-b36a-85b359b221a7/ekaterinburg-metro-map-image18-large-opt.jpg">View large preview</a>)</figcaption></figure>

We even tried making the metro line dotted:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a545e7a1-2c7f-448b-9942-abb1b3538135/ekaterinburg-metro-map-image30-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a545e7a1-2c7f-448b-9942-abb1b3538135/ekaterinburg-metro-map-image30-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a545e7a1-2c7f-448b-9942-abb1b3538135/ekaterinburg-metro-map-image30-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11356b4b-cac5-4b52-826b-b776508bc311/ekaterinburg-metro-map-image70-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11356b4b-cac5-4b52-826b-b776508bc311/ekaterinburg-metro-map-image70-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11356b4b-cac5-4b52-826b-b776508bc311/ekaterinburg-metro-map-image70-large-opt.jpg">View large preview</a>)</figcaption></figure>

Notice another key improvement here: Street names have been moved inside the streets themselves where space allowed. All-caps were very handy for this, contributing significantly to clarity.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/764ff0d3-a870-4270-babc-b7a2237a0e72/ekaterinburg-metro-map-image14-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/764ff0d3-a870-4270-babc-b7a2237a0e72/ekaterinburg-metro-map-image14-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/764ff0d3-a870-4270-babc-b7a2237a0e72/ekaterinburg-metro-map-image14-large-opt.jpg">View large preview</a>)</figcaption></figure>

We kept on with the stations:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb87c5c-e9e2-4fda-9750-2560379b95d9/ekaterinburg-metro-map-image64-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb87c5c-e9e2-4fda-9750-2560379b95d9/ekaterinburg-metro-map-image64-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb87c5c-e9e2-4fda-9750-2560379b95d9/ekaterinburg-metro-map-image64-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72236ea-132a-4d09-824c-a9c115796134/ekaterinburg-metro-map-image61-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72236ea-132a-4d09-824c-a9c115796134/ekaterinburg-metro-map-image61-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72236ea-132a-4d09-824c-a9c115796134/ekaterinburg-metro-map-image61-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdb7cdf-71dc-417d-8e23-a53598c08382/ekaterinburg-metro-map-image37-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdb7cdf-71dc-417d-8e23-a53598c08382/ekaterinburg-metro-map-image37-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cdb7cdf-71dc-417d-8e23-a53598c08382/ekaterinburg-metro-map-image37-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f404683-cafe-417c-95f4-923cc3b37779/ekaterinburg-metro-map-image04-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f404683-cafe-417c-95f4-923cc3b37779/ekaterinburg-metro-map-image04-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f404683-cafe-417c-95f4-923cc3b37779/ekaterinburg-metro-map-image04-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a4ef73c-191e-4b13-87b5-f30cf9c2e59c/ekaterinburg-metro-map-image36-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a4ef73c-191e-4b13-87b5-f30cf9c2e59c/ekaterinburg-metro-map-image36-large-opt.jpg" alt="" /></a><figcaption>Mondrian edition (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a4ef73c-191e-4b13-87b5-f30cf9c2e59c/ekaterinburg-metro-map-image36-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a11390c1-d84b-4e5e-872f-1e103c6560d3/ekaterinburg-metro-map-image22-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a11390c1-d84b-4e5e-872f-1e103c6560d3/ekaterinburg-metro-map-image22-large-opt.jpg" alt="" /></a><figcaption>Cast-iron edition (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a11390c1-d84b-4e5e-872f-1e103c6560d3/ekaterinburg-metro-map-image22-large-opt.jpg">View large preview</a>)</figcaption></figure>

We didn’t like that the river consisted of very thin lines, which aren’t used anywhere else in the map, so that changed:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcad002-905a-4b36-a0e2-05dab3bb57fd/ekaterinburg-metro-map-image28-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcad002-905a-4b36-a0e2-05dab3bb57fd/ekaterinburg-metro-map-image28-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcad002-905a-4b36-a0e2-05dab3bb57fd/ekaterinburg-metro-map-image28-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48ef1ca0-16cd-444b-a304-ffebba8e2819/ekaterinburg-metro-map-image50-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48ef1ca0-16cd-444b-a304-ffebba8e2819/ekaterinburg-metro-map-image50-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48ef1ca0-16cd-444b-a304-ffebba8e2819/ekaterinburg-metro-map-image50-large-opt.jpg">View large preview</a>)</figcaption></figure>

We are skipping many other attempts here, but the one below is worth pointing out. We thought this one had promise.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28110cb4-fb45-486e-a0b9-d40139542ac3/ekaterinburg-metro-map-image06-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28110cb4-fb45-486e-a0b9-d40139542ac3/ekaterinburg-metro-map-image06-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28110cb4-fb45-486e-a0b9-d40139542ac3/ekaterinburg-metro-map-image06-large-opt.jpg">View large preview</a>)</figcaption></figure>

## Everything Is Coming Together

Turning back to the streets, the thin ones looked odd. So, we tried giving all streets the same width:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/592b9bf6-9c47-4db7-b22f-2301c52261de/ekaterinburg-metro-map-image39-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/592b9bf6-9c47-4db7-b22f-2301c52261de/ekaterinburg-metro-map-image39-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/592b9bf6-9c47-4db7-b22f-2301c52261de/ekaterinburg-metro-map-image39-large-opt.jpg">View large preview</a>)</figcaption></figure>

Because there were no more thin lines anywhere, we gave the TV tower a fill instead of a contour:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e9d054-5d83-44c5-afd0-39616a07bb82/ekaterinburg-metro-map-image45-large-opt.png"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e9d054-5d83-44c5-afd0-39616a07bb82/ekaterinburg-metro-map-image45-large-opt.png" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e9d054-5d83-44c5-afd0-39616a07bb82/ekaterinburg-metro-map-image45-large-opt.png">View large preview</a>)</figcaption></figure>

Then we swapped the colors of the background and the streets, and we made the river look like it’s flowing:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6da1aad-17a3-4311-8cfd-88535e519053/ekaterinburg-metro-map-image71-large-opt.png"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6da1aad-17a3-4311-8cfd-88535e519053/ekaterinburg-metro-map-image71-large-opt.png" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6da1aad-17a3-4311-8cfd-88535e519053/ekaterinburg-metro-map-image71-large-opt.png">View large preview</a>)</figcaption></figure>

We also tried making the river wavy on the outside as well as inside:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f25f7f55-307f-4f86-8e5b-b2007618795e/ekaterinburg-metro-map-image32-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f25f7f55-307f-4f86-8e5b-b2007618795e/ekaterinburg-metro-map-image32-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f25f7f55-307f-4f86-8e5b-b2007618795e/ekaterinburg-metro-map-image32-large-opt.jpg">View large preview</a>)</figcaption></figure>

But this felt like a step back. It looked more like pasta than water.

Our compass was too simple as well:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c438738-3432-4e86-8541-76a1aa0811d6/ekaterinburg-metro-map-image42-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c438738-3432-4e86-8541-76a1aa0811d6/ekaterinburg-metro-map-image42-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c438738-3432-4e86-8541-76a1aa0811d6/ekaterinburg-metro-map-image42-large-opt.jpg">View large preview</a>)</figcaption></figure>

We took inspiration from Yuri Gordon’s arrows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bef7eb-cabe-41cb-aec6-25d9a78883bc/ekaterinburg-metro-map-image54-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bef7eb-cabe-41cb-aec6-25d9a78883bc/ekaterinburg-metro-map-image54-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bef7eb-cabe-41cb-aec6-25d9a78883bc/ekaterinburg-metro-map-image54-large-opt.jpg">View large preview</a>)</figcaption></figure>

Here’s the one we made:

<figure>&lt;<img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5e2d24-0c36-45b9-b299-e6ddabd5aa39/ekaterinburg-metro-map-image00-opt.jpg" alt="" /></figure>

## Final Touches

We kept returning to the metro line and stations again and again — obviously, because they are the most important elements.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5d6ca6f-cf61-4aed-8eab-1d88ed25d113/ekaterinburg-metro-map-image68-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5d6ca6f-cf61-4aed-8eab-1d88ed25d113/ekaterinburg-metro-map-image68-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5d6ca6f-cf61-4aed-8eab-1d88ed25d113/ekaterinburg-metro-map-image68-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afa8c6c9-c1ea-4895-9e9b-654e6a283daa/ekaterinburg-metro-map-image55-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afa8c6c9-c1ea-4895-9e9b-654e6a283daa/ekaterinburg-metro-map-image55-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afa8c6c9-c1ea-4895-9e9b-654e6a283daa/ekaterinburg-metro-map-image55-large-opt.jpg">View large preview</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fac4d23-9457-41c1-8cf9-2c380c50abed/ekaterinburg-metro-map-image72-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fac4d23-9457-41c1-8cf9-2c380c50abed/ekaterinburg-metro-map-image72-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fac4d23-9457-41c1-8cf9-2c380c50abed/ekaterinburg-metro-map-image72-large-opt.jpg">View large preview</a>)</figcaption></figure>

What’s the ugliest thing now? The parks. The way they bump up against the roads and each other is not nice. Particularly unpleasant are the parks surrounding the river. We’ve removed the background leaving only the trees while also tuning their color, and it became much nicer:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d042b54a-6dc2-4bc7-91c3-23f621c3f919/ekaterinburg-metro-map-image51-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d042b54a-6dc2-4bc7-91c3-23f621c3f919/ekaterinburg-metro-map-image51-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d042b54a-6dc2-4bc7-91c3-23f621c3f919/ekaterinburg-metro-map-image51-large-opt.jpg">View large preview</a>)</figcaption></figure>

The TV tower improved as well:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2823fc3-8ef1-4f06-9a27-9206887df950/ekaterinburg-metro-map-image35-large-opt.jpg"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2823fc3-8ef1-4f06-9a27-9206887df950/ekaterinburg-metro-map-image35-large-opt.jpg" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2823fc3-8ef1-4f06-9a27-9206887df950/ekaterinburg-metro-map-image35-large-opt.jpg">View large preview</a>)</figcaption></figure>

The PT Sans font was dispensed in favor of ALS Direct:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b35d3814-5e0f-4334-b23c-20375078e8e3/ekaterinburg-metro-map-image01-large-opt.png"><img loading="lazy" decoding="async"  title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b35d3814-5e0f-4334-b23c-20375078e8e3/ekaterinburg-metro-map-image01-large-opt.png" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b35d3814-5e0f-4334-b23c-20375078e8e3/ekaterinburg-metro-map-image01-large-opt.png">View large preview</a>)</figcaption></figure>

We added tram lines because they are prominent features on the street and would help with wayfinding.

Also, we tried aligning the text to a grid:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1211e794-c67e-4196-b6b7-fb7fc4895787/ekaterinburg-metro-map-image58-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1211e794-c67e-4196-b6b7-fb7fc4895787/ekaterinburg-metro-map-image58-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1211e794-c67e-4196-b6b7-fb7fc4895787/ekaterinburg-metro-map-image58-large-opt.jpg">View large preview</a>)</figcaption></figure>

And we added some shadows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b1070f-b655-4158-a94c-d51060a047cc/ekaterinburg-metro-map-image49-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b1070f-b655-4158-a94c-d51060a047cc/ekaterinburg-metro-map-image49-large-opt.jpg" alt="" /><br>
</a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80b1070f-b655-4158-a94c-d51060a047cc/ekaterinburg-metro-map-image49-large-opt.jpg">View large preview</a>)</figcaption></figure>

That’s about it! Pasha built all of it in Adobe Illustrator, directed by me, Ilya, via email.

In no way is this meant to be a comprehensive guide to designing a map. Each city presents its own set of problems and peculiarities. But hopefully this gives you an idea of what to look for and what to try if you take on such an assignment. What seemed at first like a small project turned out to be a rigorous exercise spanning several months.

{{< signature "vf, il, al" >}}

