---
title: Paris Metro Map – The Redesign
slug: redesigning-the-paris-metro-map
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa0c6046-0c4c-4df6-abd5-a0a2d81a987e/preview-paris-metro-map-500w-opt.png
date: 2017-01-30T21:47:47.000Z
author: constantinekonovalov
description: >-
  When I first visited Paris, it took me a while to get oriented and put
  together a route using the official map of the Paris metro. That’s all it took
  to spark the flame inside me to redraw it according to an entirely different
  set of principles. The goal was extremely ambitious, but why not try?

  In this article, I will attempt to describe the principal solutions involved
  in the development of my own version of the Paris metro map. But for a moment,
  I’ll just jump ahead to the result.
categories:
  - Inspiration
  - Design
  - UX
---
In this article, I will attempt to describe the principal solutions involved in the development of my own version of the Paris metro map. But for a moment, I’ll just jump ahead to the result:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efa7008b-4671-44d8-9481-f407cef0b2e4/paris-metro-map91.0-large-opt"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebe4bf6a-cee8-452e-b30c-34bd5f27e34d/paris-metro-map91.0-preview-opt" width="780" height="780" alt="Paris metro map (Constantine Konovalov)" /></a><figcaption>(Image: <a href="https://metromap.fr/en">metromap.fr</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efa7008b-4671-44d8-9481-f407cef0b2e4/paris-metro-map91.0-large-opt">View large version</a>)</figcaption></figure>

I am unable to discuss the entire process that went into the creation of this new map, because it took me around two and a half years to complete, and an article of that length would bore even the most committed of readers. In this light, I will cover only the principal graphical solutions. At the end of the report, I have included a time-lapse video of the entire creation process.

For comparison, this is the current official map.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8022812-c776-4ec7-83a3-042e155c978b/ratp-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f99828b-bf49-4563-b6de-47422cfaf441/ratp-preview-opt.png" width="780" height="785" alt="Paris metro map (official version)" /></a><figcaption>(Image: <a href="https://www.ratp.fr/informer/pdf/orienter/f_plan.php">RATP</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8022812-c776-4ec7-83a3-042e155c978b/ratp-large-opt.png">View large version</a>)</figcaption></figure>

Indeed, its appearance is rather forbidding. There are numerous lines twisted about chaotically, and the eye lacks a clear anchor, because there is nothing characteristic or memorable to grasp onto. Naturally, if used frequently, maps become customary and familiar. However, for a city that has more tourists than local residents, this element of urban navigation has obvious shortcomings.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Redesigning Ekaterinburg’s Metro Map](https://www.smashingmagazine.com/2016/06/map-design-redesigning-ekaterinburgs-metro-map/)
*   [Maps In Modern Web Design: Showcase and Examples](https://www.smashingmagazine.com/2010/04/maps-in-modern-web-design/)
*   [A Collection Of Train and Airport Signs](https://www.smashingmagazine.com/train-and-airport-signs-part-2/)
*   [50 Problems In 50 Days: The Power Of Not Knowing](https://www.smashingmagazine.com/2014/01/50-problems-in-50-days-the-power-of-not-knowing/)

## A Circular Image Of The City

Where did the circle come from in my version if the original map has nothing of the sort? Is Paris circular all of a sudden?

The answer is yes, Paris actually is circular to a certain extent. Let us take the maps of Moscow, London and Berlin as examples and match them with the real geographies of the cities. It is clear that all of these maps share a certain distinctive feature.

The map of the Moscow metro includes two ring-shaped lines, one brown and one pink (the surface metro line). But when the tracks of these lines are superimposed on the geographic map (on the left), both lines are seen to be circular in only the most remote sense. As can obviously be discerned from the metro map, these lines are shown as rings only for simplicity’s sake.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e04cbcb-e051-42cc-9602-b4fa36209243/moscow-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6f43a6a-ca1e-449a-bd16-fd62b8c16ea2/moscow-preview-opt.png" width="780" height="339" alt="Moscow" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e04cbcb-e051-42cc-9602-b4fa36209243/moscow-large-opt.png">View large version</a>)</figcaption></figure>

London’s map has a closed, bottle-shaped contour. This is not a circle, but it is still another memorable form that makes orienting oneself in the city easier. Even though, geographically speaking, the shape of the line is far more complex (as can be seen in the image to the left), it is nonetheless depicted in the shape of a bottle. Still, the line is locally known as the Circle.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e832d8f-a3af-4628-9fc7-2d8f0242de7d/london-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8f80b4-9521-478a-8d42-9b72464f1534/london-preview-opt.png" width="780" height="263" alt="London" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e832d8f-a3af-4628-9fc7-2d8f0242de7d/london-large-opt.png">View large version</a>)</figcaption></figure>

In Berlin, lines S41 and S42 are known as the Ring, even though, from a geographic perspective, the lines do not resemble a perfect circle. Also, the Ring is not drawn as a circle on the map, but is instead shown as a symmetrical octagon. What is most important is that, thanks to its geometric simplicity, this shape can be easily recognized on the map and forms the central tariff zone A. This is a great and super-convenient detail, even among other shortcomings of the Berlin map.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5995aff-eada-4f21-93bf-d40cba9a58d5/berlin-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/723e7682-16ac-4089-a9b8-c8ad4996a896/berlin-preview-opt.png" width="780" height="273" alt="Berlin" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5995aff-eada-4f21-93bf-d40cba9a58d5/berlin-large-opt.png">View large version</a>)</figcaption></figure>

But what about Paris? Paris is similar to these cities in its construction — the city can be broken down into two circles. One circle includes metro lines 2 and 6\. The second of the two tram routes has still yet to form a loop, but construction is in progress. Still, it is safe to nominally say that the second circle is in fact the administrative border of the city, which happens to correspond to the tram line. However, looking at the official map, we cannot see the same clear-cut contour we see in other cities. The fact is that these contours simply merge with the other numerous lines.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02e83502-ea8d-413d-a37f-4fc519701406/paris-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c460fd17-62a6-4b29-91a7-3ee4ea79218e/paris-preview-opt.png" width="780" height="273" alt="Paris" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02e83502-ea8d-413d-a37f-4fc519701406/paris-large-opt.png">View large version</a>)</figcaption></figure>

Also, when the geographic map is superimposed on the transit map, it is easy to see that on the official Paris metro map, lines 2 and 6 are considerably distorted and do not conform to the true geographic shape. If so, why not simplify these two lines and represent them as a recognizable shape, as in the cases of other cities?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf38317-12ec-4f50-bcd3-54b96d1bcece/geographic-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65a7880b-c16c-4411-ba83-5112cc46d21c/geographic-preview-opt.png" width="780" height="322" alt="geographic Paris metro map" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf38317-12ec-4f50-bcd3-54b96d1bcece/geographic-large-opt.png">View large version</a>)</figcaption></figure>

The only difference between Paris and other cities is that the ring would be formed from two lines.

Before World War II, the metro ring was even divided into three lines. A portion of the present-day 6 (the lower portion of the ring) was a continuation of the 5 (the orange line in the image below). Plus, even back then, attempts were made to simplify the map using a regular circle, but they ended without much success. Ever since then, many designers have tried their hand at depicting a circular Paris.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa6e9ddd-35eb-4e0f-9656-e5553bed63e0/oldmap-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72f8e5e0-054b-439e-a328-6ab633ff899b/oldmap-preview-opt.jpg" width="780" height="608" alt="Paris metro map 1936" /></a><figcaption>An unofficial map dating back to 1936 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa6e9ddd-35eb-4e0f-9656-e5553bed63e0/oldmap-large-opt.jpg">View large version</a>)</figcaption></figure>

Delving deeper into history, you’d discover that both of these Paris rings corresponded to the contours along which defensive walls were built in the city: the Farmers-General Wall (shown in blue in the image below) and the Thiers Wall (red), which themselves formed closed loops around the city. These days, the walls no longer exist, having been replaced by boulevards. These boulevards were then used to build some of the first metro lines, and a tram recently started operating along the outer ring. One particularly characteristic detail is that the metro lines tracing the location of former city walls are all above ground, with the exception of small underground sections. This allows riders to easily associate the metro ring with the above-ground portion of the city. In other words, if circular metro lines were shown as nominal circles on the map, then finding one’s desired station would be easier because a ring is easy to spot against a background of other numerous lines.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c1f187-2ef3-493d-8865-ce83067effe3/oldmap2-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad37a143-5af8-4c23-9a0b-36b354a52d29/oldmap2-preview-opt.jpg" width="780" height="666" alt="Paris map" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67c1f187-2ef3-493d-8865-ce83067effe3/oldmap2-large-opt.jpg">View large version</a>)</figcaption></figure>

In 1992, RATP, the Parisian public transportation operator, replaced its logo with a circle and a silhouette of girl looking upwards. This symbol also represents the Seine flowing through Paris, which happens to be depicted as a circle.

Lately, this sign can be seen on every metro car, bus, ticket and transit map in Paris.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d75c891-6557-4852-a849-201b11209121/logo-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9a50529-f6d3-4f72-a271-75a0dba813b8/logo-preview-opt.png" width="780" height="339" alt="RATP logo" /></a><figcaption>(Image: <a href="https://www.ratp.fr">RATP</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d75c891-6557-4852-a849-201b11209121/logo-large-opt.png">View large version</a>)</figcaption></figure>

## Map Grid And Non-Geographic Depiction

The existence of two metro maps is appropriate for a city: one aligned with the city’s geography, and the other composed according to schematic representation of the lines. When a transit map is made on a city’s actual map, the lines correspond to real positions in the city, which is convenient to the extent that geographic precision is preserved. Such a map, however, has many disadvantages.

For example, here is the official map of the Paris metro integrated with a map of the city:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d93def-58ac-4dc4-af65-3ee6fc503085/ratp2-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a977b027-9785-403b-88a9-05d26ce2c1d9/ratp2-preview-opt.png" width="780" height="580" alt="Paris metro map (official version)" /></a><figcaption>(Image: <a href="https://www.ratp.fr/informer/pdf/orienter/f_plan.php?nompdf=metro_geo&loc=secteur&fm=pdf">RATP</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d93def-58ac-4dc4-af65-3ee6fc503085/ratp2-large-opt.png">View large version</a>)</figcaption></figure>

There is a lot of information to handle here, beyond just station names and maps of metro lines, overloading it to an unacceptable extent. The names of stations are tiny compared to the map as a whole and cannot be easily read; using a map like this on the run would be very difficult. Just imagine trying to puzzle out interchanges on this map if you were to find yourself in an unfamiliar city:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ede3293-5908-4fb7-bbef-dbadfd791070/ratp3-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/317cee44-8342-4551-b379-32a583daaef1/ratp3-preview-opt.png" width="780" height="374" alt="Paris metro map (official version)" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ede3293-5908-4fb7-bbef-dbadfd791070/ratp3-large-opt.png">View large version</a>)</figcaption></figure>

This is why complex maps are usually simplified and drawn to be more readable. To simplify, geography is sacrificed, allowing the map to be built according to a set of rules designed for readability and easier plotting of routes from point A to point B.

These rules include line color, point size, station designations and the coordinate grid used to plot the lines. A grid with an angle increment of 45 degrees is typically used. This is sufficient for most transit maps. Still, when a map gets more complex and the number of lines increases, the lines start getting tangled with one another, creating extra curves and misleading sections with stacks of parallel lines in which it is easy to get lost.

Transit maps must connect station location points in the simplest way possible, and the coordinate grid should assist this process.

After studying the problematic spots on the official Paris metro map, I concluded that the 45-degree grid is not the best solution for Paris. I instead believe that if a 30-degree grid is employed, the extra curves and other tricky sections could be eliminated by virtue of a larger number of axes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8558c709-c6d3-409f-9ced-4c83a4368745/45degrees-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d877514c-ab68-41b6-8887-d7e15562b854/45degrees-preview-opt.png" width="780" height="" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8558c709-c6d3-409f-9ced-4c83a4368745/45degrees-large-opt.png">View large version</a>)</figcaption></figure>

When I first started working on the map, I imagined that, despite all of the advantages of the 30-degree grid, I would still be unable to create a stable graphical form for the overall map. The vertical sections of some lines still attract more attention than they are intended to.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/456ec346-fbc6-4985-a461-f993451fb0fc/process-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b938d7-e147-4d1e-8ea7-e5141ad43458/process-preview-opt.jpg" width="780" height="780" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/456ec346-fbc6-4985-a461-f993451fb0fc/process-large-opt.jpg">View large version</a>)</figcaption></figure>

At some point, I understood that the reason why the shape is unstable is my use of a vertical axis. When the 30-degree grid is used, so many axes are created that its most vertical catches the eye more easily than the others when one is viewing the image as a whole. Humans have evolved to constantly look for patterns in everything. In this way, even adults can imagine that clouds take on the shape of animals. Two windows cut into a blank wall next to each other attract our attention, and pure imagination transforms them into the eyes of an unknown creature.

In this case, the vertical axis draws attention and is likened to a foreign object on the image. This is why I decided to get rid of all verticals, but continued to work with the 30-degree grid.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9456396d-23e3-4ba4-91b1-2fcac550d56a/process2-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae43f3d-e7c0-4b87-8209-7ad9bcd1f992/process2-preview-opt.jpg" width="780" height="780" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9456396d-23e3-4ba4-91b1-2fcac550d56a/process2-large-opt.jpg">View large version</a>)</figcaption></figure>

So, through trial and error, I found myself using the 30-degree grid, but without any vertical lines.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b3d4e1d-ee81-4e83-95fc-3cbf04c58883/30degrees-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea17233f-8509-49c4-a03e-f3105284acdb/30degrees-preview-opt.png" width="780" height="323" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b3d4e1d-ee81-4e83-95fc-3cbf04c58883/30degrees-large-opt.png">View large version</a>)</figcaption></figure>

Initially, I had wanted to simplify the complex shapes and limit the number of curves compared to the official map. By adopting a 30-degree grid, I was able to reduce the number of line curves by 2.5 times. Difficult interchange nodes were disentangled, thus becoming more easily understood.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98b8b6eb-bdf1-4c51-8cbc-b44167919cdd/chatelet-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d70332d6-f6b4-448c-a1b1-48dcf72ea5dc/chatelet-preview-opt.png" width="780" height="339" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98b8b6eb-bdf1-4c51-8cbc-b44167919cdd/chatelet-large-opt.png">View large version</a>)</figcaption></figure>

## Line Curvature Radius

Another requirement directly related to the coordinate grid is changing the radii of the line curvature. Many transit designers pay no attention to this detail, but it is very important to producing an attractive graphical image of transit lines. Let’s start with three angles, 90, 120 and 150 degrees:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad671b2-a641-452d-992a-69a8e7071025/angle-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae185e12-756c-4cb5-9614-7975d8f56031/angle-preview-opt.png" width="780" height="322" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dad671b2-a641-452d-992a-69a8e7071025/angle-large-opt.png">View large version</a>)</figcaption></figure>

If we smoothed them out with the same curvature radius, these lines would not look so similar. The bend of the 90-degree angle would be too smooth (about one-quarter of the curve), while the 150-degree angle would be so sharp that little difference would be perceived in the angle without rounding.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db960634-bb32-490d-a216-814b8305a549/angle-circle-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a2b9164-5254-41b2-b1f5-ad852beb2376/angle-circle-preview-opt.png" width="780" height="321" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db960634-bb32-490d-a216-814b8305a549/angle-circle-large-opt.png">View large version</a>)</figcaption></figure>

Let’s conduct a short experiment. Take a drinking straw and start bending it — first lightly, then all the way to an acute angle. Notice that when the bend is minor, the curvature radius is quite large, and when the angle is acute, the curvature radius shrinks. This observation is useful when building transit maps. The sharper the bend, the more noticeable it becomes, so the curvature radius should be smaller. If the curvature is insignificant, then there would be no point in sharply accentuating it, so the radius would increase in this case.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c12ea0f-3e22-46c1-a954-767dc093542c/straws-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e16112c-241e-47a0-a8ed-cebd959a2b4c/straws-preview-opt.png" width="780" height="322" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c12ea0f-3e22-46c1-a954-767dc093542c/straws-large-opt.png">View large version</a>)</figcaption></figure>

Note the bends on this map:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75712e44-1578-4fbd-b934-92bd706437d2/paris-metro-map-north-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15ad8834-2462-4447-aa1f-57b224229be3/paris-metro-map-north-preview-opt.png" width="780" height="352" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75712e44-1578-4fbd-b934-92bd706437d2/paris-metro-map-north-large-opt.png">View large version</a>)</figcaption></figure>

If a line follows its route and only bends 150 degrees, then the turn would be smoothed out by a streamlined curve. But if attention needs to be brought to a sharp turn (a 60-degree angle), then the curvature radius could be reduced, and the line bent more aggressively, catching the eye when the user is planning a route. Such curves are natural for the eye, because they approximate the physical curves encountered in a real environment.

(It is rather easy to guess the principle of radius change depending on the angle of the bend. I am fully confident that many readers can solve this simple geometric equation with alacrity.)

## Colors

In the process of its composition, the new map adopted a layout quite dissimilar from the official version. Therefore, I decided to stylize it with colors that would be more familiar to Parisians.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e0490bf-a60e-4748-84aa-f4487bb9d83f/paris-metro-map-white-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4967c44-3fb2-4e42-9492-c941b7a5acbf/paris-metro-map-white-preview-opt.png" width="780" height="390" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e0490bf-a60e-4748-84aa-f4487bb9d83f/paris-metro-map-white-large-opt.png">View large version</a>)</figcaption></figure>

I also repainted the background to match the style of the official map, so that it would be better associated with Paris.

To a certain extent, I dislike this solution because the map loses its sharpness, due to the yellow background. On the other hand, it looks much closer to the official map that so many have become accustomed to — a rather clever perception trick.

Also, to make the map easier to understand, I reduced it to the major geographic principles of the Paris transit system, including the official colors of lines, fonts and graphical designations.</p>

## Icons

In tourism capitals, it is very important to direct visitors to where the main sights are located, using directions and maps.

The color brown is typically used to depict walking proximity to noteworthy sights. To create icons for Paris’ most famous sights, I used a square, regular grid after approximately calculating that, when printing the map in A3 format, the printer would be able to precisely print each cell.

To make the sights more noticeable in smaller format, they must first be simplified. This turned out to be a rather fascinating process. The principal features of each building are singled out from their photographs. These could include recognizable windows and doors, bas-reliefs or sculptures. Naturally, an icon need not be very precise, but should only adhere to the shape and general image of the building. Similar to how the exact borders of the city or ring-shaped transport lines cannot be reproduced from memory, it is easier to just remember a more simplified, concise version of them, just as it is impossible to recall the precise number of sculptures on the facade of Notre Dame de Paris. An entire picture simply cannot fit into the average memory. People only remember general features: two towers, a circular window in the center, three arches below. This is sufficient to make an icon memorable and not to overload it at the same time. Icons with excessive detail in a small format look messy on a map.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20568f4a-7a01-46d9-ad95-26c660a40434/icons-notre-dame-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ff8d5e3-fe4e-460b-8828-892aa479eac7/icons-notre-dame-preview-opt.png" width="780" height="390" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20568f4a-7a01-46d9-ad95-26c660a40434/icons-notre-dame-large-opt.png">View large version</a>)</figcaption></figure>

But while many sights can be easily depicted based on a photo of the facade, there are exceptions. For example, a sports stadium or Disneyland would need to be drawn differently.

Yet stadiums are not always recognizable when viewed from the side, and they rarely possess any characteristic features or unique architectural forms. However, when viewed from the top, they are easily perceptible because the inside can be depicted as a football field. Also, people more frequently see stadiums on TV when they are filmed from a bird’s-eye view.

Places like Disneyland are more easily recognizable not from any architectural image, but from their symbols. For Disneyland, that is Mickey Mouse.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7626f8f-6261-4d7f-84d1-b4381d0805b5/icons-of-paris-attractions-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85140219-8393-4406-9a0a-6b97889b3605/icons-of-paris-attractions-preview-opt.png" width="780" height="390" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7626f8f-6261-4d7f-84d1-b4381d0805b5/icons-of-paris-attractions-large-opt.png">View large version</a>)</figcaption></figure>

## Line Harmony

To avoid making the map look chaotic and to give it a certain graphical rhythm, I needed to create connections between the similar placement of parallel lines on the map itself.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e0b408c-e802-4538-921d-4db90c08ee16/line-harmony-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb89a1ee-87e7-4309-b571-35cda52c24f3/line-harmony-preview-opt.png" width="780" height="467" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e0b408c-e802-4538-921d-4db90c08ee16/line-harmony-large-opt.png">View large version</a>)</figcaption></figure>

Take a look at these four fragments. It is not difficult to notice that the distance between two parallel lines in any of the four cases is the same. This was done on purpose as a way to “calm” the graphical elements on the map. In other words, this is another addition to the rules of the grid and radii of curvature. But here, no rule is ever set in stone. There may be several types of indentations between parallel lines, and their selection is directly related to the overall artistic theme.

Below, I used rectangles to highlight the places where the same space is left between parallel lines. They set the rhythm of the image.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194f5251-8273-4541-99ef-04dfbf35f804/line-harmony2-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ecbc79d-1d35-423b-aadf-b8d4fe071444/line-harmony2-preview-opt.png" width="780" height="780" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194f5251-8273-4541-99ef-04dfbf35f804/line-harmony2-large-opt.png">View large version</a>)</figcaption></figure>

Naturally, this is just a sample of the equal distances. There are far more of them, and their interdependencies might be far more complex.

For example, elegant graphics can be created by manipulating the curves of river and transit lines. The image on the left shows the river and RER C line (yellow) on the map, and the one on the right shows their actual geographic position.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ea88b2b-d128-4262-b531-ac928970f8d9/seine-river-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f715220-8198-4e4a-adea-7ca8c6798b78/seine-river-preview-opt.png" width="780" height="359" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ea88b2b-d128-4262-b531-ac928970f8d9/seine-river-large-opt.png">View large version</a>)</figcaption></figure>

A few paragraphs above, we covered the rules for smoothing angles and established certain principles, but the design also allows for exceptions to even the strictest rules. The curves of the RER C line do not follow the rules of the other bends. Here, the curvature radius of angles is formed following the river’s general rhythm, because the shape of the line depends largely on the route of the Seine. Therefore, the RER C line simply clings to the river and moves along with it.</p>

## Iterations

This article cannot cover each individual fragment of the map, so I will limit myself to a description of just one of the most complex sections and how it developed. The topic of focus here is the Montparnasse-Bienvenüe junction. I believe this example does a lot to explain the general process of working on this map.

First, I attempted to bring the lines together in such a way that the transfer would be depicted as a single point where the lines of each transfer station are intersecting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05092cd4-a723-48db-b4f9-8ceb98fa778c/process3-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac97c500-0e15-4a8d-bf75-1b4a1351d7da/process3-preview-opt.png" width="780" height="262" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05092cd4-a723-48db-b4f9-8ceb98fa778c/process3-large-opt.png">View large version</a>)</figcaption></figure>

But the resulting crossings were not visually pleasing, and the straight lines failed to meld with the ring line.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28d02ba4-f888-41af-b3a4-2b3473226f39/process4-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3bd8202-6174-42ed-bb5d-b28771c00253/process4-preview-opt.png" width="780" height="262" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28d02ba4-f888-41af-b3a4-2b3473226f39/process4-large-opt.png">View large version</a>)</figcaption></figure>

Ultimately, I tried several versions to solve this issue, and also attempted to draw sections of the straight lines as ring lines.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad8f6e7-c1da-45b7-82c9-1b6b8953d36e/process5-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56c76b44-1977-42e5-936b-00396d8f6c0e/process5-preview-opt.png" width="780" height="254" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ad8f6e7-c1da-45b7-82c9-1b6b8953d36e/process5-large-opt.png">View large version</a>)</figcaption></figure>

At some point, the junction even started to come into its own. I felt like I could just stop there, but after digging through the old maps of Paris and talking to city residents, I understood that the transfer as a whole could not be narrowed down to just a single point. The heart of the matter was that, in the past, the Montparnasse-Bienvenüe station did not yet exist; rather, there were actually two different transfer junctions, Gare Montparnasse and Bienvenüe. Between them there was no transfer. So, the common name, Montparnasse-Bienvenüe, was adopted only after they had been joined. And the distance between these stations is expansive, so transfers here are quite long and inconvenient.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ae72049-a8ba-4b5f-a71a-40e70e086b76/history-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56399292-0148-47b4-9f3a-3c8988847f14/history-preview-opt.jpg" width="780" height="382" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ae72049-a8ba-4b5f-a71a-40e70e086b76/history-large-opt.jpg">View large version</a>)</figcaption></figure>

If there were no alternative options to building the route, they could just be left as they were, with no attention paid to the fact that transferring here takes so long. But when looking at the official map, many passengers travelling on the 12 (dark green) see the very first crossing with the 6 (light green) at the Montparnasse-Bienvenüe station, even though they could take a much shorter transfer at Pasteur if they continued a little further. But the eye fails to catch this detail.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/799e8b95-596f-40ec-96ff-8523ccd88aa4/way-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f110d6e-4b18-4859-9859-033fad981f61/way-preview-opt.png" width="780" height="375" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/799e8b95-596f-40ec-96ff-8523ccd88aa4/way-large-opt.png">View large version</a>)</figcaption></figure>

Thus, on my map, I divided up the transfer visually to hint at the long transfer time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59b97b9d-0807-4f50-8ff4-ae407a81c56d/process6-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d50b3df2-b425-4c6d-98f9-4e09cc319fc0/process6-preview-opt.png" width="780" height="255" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59b97b9d-0807-4f50-8ff4-ae407a81c56d/process6-large-opt.png">View large version</a>)</figcaption></figure>

After another dozen iterations, I arrived at the following result:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ea67f3-3557-4e4a-b941-44c48b8482ae/process7-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac32c5a0-317d-4356-8fa9-562e802356e6/process7-preview-opt.png" width="780" height="355" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ea67f3-3557-4e4a-b941-44c48b8482ae/process7-large-opt.png">View large version</a>)</figcaption></figure>

It seems wrong to break the transfer into two parts connected by a communication line, but after studying all of the details, it is evident that a map should first and foremost help passengers map the quickest routes.</p>

## Development Perspectives

When developing a new map for a rapidly growing city, studying plans for further construction is also a must. My idea for ring-shaped lines enjoys significant support from Paris’ future urban development plans. Another ring-shaped line will be made into a loop around Paris within the next 15 years. This time, the new ring will be made up of just the 15 line.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfbe864-d4d6-447a-bb75-740db8ea9e41/grand-paris-express-map-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b70847f-3c39-4a58-a908-80c2ea2426f5/grand-paris-express-map-preview-opt.jpg" width="780" height="790" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcfbe864-d4d6-447a-bb75-740db8ea9e41/grand-paris-express-map-large-opt.jpg">View large version</a>)</figcaption></figure>

I ultimately chose not to allocate much precious space to the new ring before it has even been built. So, I compressed it into the shape of an egg and only included the section that will be operational by 2024, the lower semi-ring.

To integrate the new semi-ring visually with the rest of the map, I repeated the shape in the already existing tram line T1, and I mirrored the semi-ring shape to the north.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34153a5c-9394-444d-abcf-9e7de64db5bd/15line-paris-large-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c9e25e6-1e9d-401f-8363-1b4cf4355fab/15line-paris-preview-opt.jpg" width="780" height="665" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34153a5c-9394-444d-abcf-9e7de64db5bd/15line-paris-large-opt.jpg">View large version</a>)</figcaption></figure>

Aside from the 15, serious changes are scheduled for both the RER E and 14, which will be extended beyond city limits. Therefore, when working on my map, I immediately took them into account. All lines currently being built are shown by dotted lines.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5e8b4c8-87c5-4448-bec8-e9ace86bd8e2/14line-paris-large-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34298220-0f53-498f-93e2-1c679dfe81c5/14line-paris-preview-opt.png" width="780" height="371" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5e8b4c8-87c5-4448-bec8-e9ace86bd8e2/14line-paris-large-opt.png">View large version</a>)</figcaption></figure>

## The Process

In my effort to create a new Paris metro map, I saved the intermediate versions so that I could return to them if I deviated too far in a certain direction for any reason. I created mockups of the map every 15 to 30 minutes by saving them to a new file. By the time the first version was completed, I had over 800 files saved.

I then combined all of these files into a video to show more concisely what went into the creation of the new map. You can now see how each node evolved as the project went on.</p>

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/168868441?title=0&byline=0&portrait=0" width="500" height="500" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

The map is still not recognized as official, but I have over one hundred reports of satisfied users after its publication in June.

I hope that the Paris public transportation operator will take my experience into account when updating the official map. I also intend to expand the map and supplement it with new stations as soon as they open. The latest version of the map is available [on my website](https://metromap.fr/en).

{{< signature "vf, il, yk, al" >}}

