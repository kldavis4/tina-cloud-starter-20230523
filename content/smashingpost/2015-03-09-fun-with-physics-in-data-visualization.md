---
title: Fun With Physics In Data Visualization
slug: fun-with-physics-in-data-visualization
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12da2369-70a7-4929-845e-a1dee1420d5f/london-olympics-preview-opt.png
date: 2015-03-09T21:43:42.000Z
author: antanasmarcelionis
description: >-
  Data visualization is on the rise. Publishers around the world — individual
  bloggers and major online publications alike — are realizing that charts, maps
  and combinations of the two can convey a message far more effectively than
  plain numbers can.

  From simple charts to fancy infographics to complex timeline animations,
  **data visualizations are popping up all over the Internet**. However, as in
  any other area, once everyone gets on the train, distinguishing yourself from
  the pack becomes hard.
categories:
  - Coding
  - Data Visualization
  - JavaScript
---
Data visualization is on the rise. Publishers around the world — individual bloggers and major online publications alike — are realizing that charts, maps and combinations of the two can convey a message far more effectively than plain numbers can. From simple charts to fancy infographics to complex timeline animations, **data visualizations are popping up all over the Internet**. However, as in any other area, once everyone gets on the train, distinguishing yourself from the pack becomes hard.</p>

<figure<img property="image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3444c3a-fd7a-4cd0-a5ad-7e9d2e200391/coffee-codepen-example-opt.jpg" title="Fun With Physics In Data Visualization" alt="Physics Data Visualization" title="Fun With Physics In Data Visualization" /></figure>

Read on to find out how a physics engine can really set your efforts apart.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Do’s And Don’ts Of Infographic Design](https://www.smashingmagazine.com/2011/10/the-dos-and-donts-of-infographic-design/)
*   [Data Visualizations and Infographics](https://www.smashingmagazine.com/2008/01/14/monday-inspiration-data-visualization-and-infographics/ "Data Visualizations and Infographics")
*   [Data Visualization: Modern Approaches](https://www.smashingmagazine.com/2007/08/02/data-visualization-modern-approaches/ "Data Visualization: Modern Approaches")
*   [Designing Flexible, Maintainable Pie Charts With CSS And SVG](https://www.smashingmagazine.com/2015/07/designing-simple-pie-charts-with-css/)

{{% feature-panel %}}

You don't need to look far for examples of data visualization. Take Google Analytics' real-time view, which places bubbles of various sizes over top a map to illustrate quantitative information:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e9ffd71-f34c-473d-802a-980d3a5906e5/google-analytics-large-preview-opt.jpg"><img property="image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f9698b0-a090-4d1d-bdf5-472c1834f602/google-analytics-preview-opt.jpg" alt="Sample bubble map." /></a><figcaption>A sample bubble map (Image: <a href="https://www.google.com/analytics/">Google Analytics</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e9ffd71-f34c-473d-802a-980d3a5906e5/google-analytics-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

Or take the "[Map of the Oil World](https://www.nytimes.com/interactive/2007/11/06/business/20071107_WINNERSLOSERS_GRAPHIC.html)" done by New York Times (which, by the way, does a lot of [nice data visualizations](https://www.nytimes.com/newsgraphics/2013/12/30/year-in-interactive-storytelling/)). That map does the job, but I'll bet most of you have come across fancier maps, ones in which the bubbles never overlap to form a distorted map and where the bigger bubbles nudge smaller ones out of place, as in the map below, also by the New York Times:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ae9e31-1ebc-4100-b64b-9fe4608bd351/london-olympics-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12da2369-70a7-4929-845e-a1dee1420d5f/london-olympics-preview-opt.png" alt="Sample bubble map." /></a><figcaption>Another bubble map (Image: <a href="https://london2012.nytimes.com/results">New York Times</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ae9e31-1ebc-4100-b64b-9fe4608bd351/london-olympics-large-preview-opt.png">View large version</a>)</figcaption></figure>

Maps like this are especially good when relatively few countries have assigned values — not all countries win a medal in the Olympics, after all. If the bubbles were to be placed directly over their respective countries, they would overlap and the result would not be as visually pleasing.

Having worked on the data visualization library [amCharts](https://www.amcharts.com/) for years, I'm always looking out for ways to help users visualize data in ways that are creative and aesthetically pleasing and that effectively convey their message. Maps like the ones discussed in this article are surely good means of relaying quantitative geographical information. Read on to find out how to make this happen.

The default features of our mapping library — JavaScript Maps — enable you to generate a standard bubble map quite easily:

See the Pen [Map with Bubbles](https://codepen.io/amcharts/pen/XJjGRM/) by amCharts ([@amcharts](https://codepen.io/amcharts)) on [CodePen](https://codepen.io).

The map above already looks nice and implementing it is very easy, but overlapping is still an issue. Let's solve that.

I could try to write my own script to detect and resolve collisions (not an easy task). From my own experience in game development, I know that all physics simulation libraries have collision detection built in. Let's use one of those.

But why stop there? Because we're tapping into the power of these libraries, we can use their other features, too. **Let's make our charts animate with lifelike motion** for a truly impressive result that will undoubtedly capture the user's attention.

A bunch of ready-made JavaScript physics libraries are available. I've chosen probably the most famous one — one of the JavaScript ports of Box2D, [box2dweb](https://code.google.com/p/box2dweb/). The idea is simple. We have a map with bubbles, and we have a box2d world (made invisible to the user) of the same size with the same bubbles replicated in it.

We'll use the (invisible) box2d world to simulate bubble movement and interaction (such as collision detection and other stuff), to monitor the bubbles' positions and to dynamically modify those positions on the map. I won't get into the technical details — you can view the source code if you want. To prevent the bubbles from falling, we simply set the gravity to `0`. And here is result:

See the Pen [Bubbles instead of countries + Gravity](https://codepen.io/amcharts/pen/MYOWGr/) by amCharts ([@amcharts](https://codepen.io/amcharts)) on [CodePen](https://codepen.io).

Great, isn't it? Now, I'm thinking to change the size of some bubbles at runtime and let the other bubbles move accordingly. To do that, we have to scale the box2d world's bubble and the map bubble together and simply observe what happens. After some testing, I see that this might work by increasing the sizes of bubbles, but not by reducing them — bubbles that are displaced before other big bubbles are reduced in size do not return back:

See the Pen [Bubbles instead of countries + change size](https://codepen.io/amcharts/pen/RNjweN/) by amCharts ([@amcharts](https://codepen.io/amcharts)) on [CodePen](https://codepen.io).

We need a more complex solution. After some experimenting, I came to this:

1.  Create a static object in the middle of each country that always stay in position.
2.  Make this object a "sensor," so that other objects don't collide into it.
3.  Create a joint between the fixed sensor and bubble, and adjust the properties of this joint to allow for some movement but while always being attracted to the position of the sensor.

That works nicely:

See the Pen [Bubbles instead of countries + working resize](https://codepen.io/amcharts/pen/yyPyQw/) by amCharts ([@amcharts](https://codepen.io/amcharts)) on [CodePen](https://codepen.io).

Just to show what can be done with a physics engine, below is another demo we made, a map of worldwide coffee consumption. Before you ask, we completely made up the data.

Our technical approach for this map is quite the same as the one for the last demo above. The only difference is that the bubbles initially are not joined to their destined locations, but rather are placed in the middle of the picture, just above the coffee pot. The coffee cup is made up of three rectangles in box2d. If you uncomment all of the lines about "debug draw" (two places in the JavaScript source and in the canvas element in HTML), you could get a box2d debug-draw view (very helpful when doing a job like this):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8ab3d1e-2e72-47c2-bf23-757e8788da00/box2d-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b61f4346-dbdc-42b0-ac54-9158ee02142a/box2d-preview-opt.png" alt="Debug wireframes for physics engine." /></a><figcaption>A wireframe for debugging physics in our imaginary board (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8ab3d1e-2e72-47c2-bf23-757e8788da00/box2d-large-preview-opt.png">View large version</a>)</figcaption></figure>

Awesome, isn't it? And it's only about 500 lines of code (not counting the data).

See the Pen [Map+Physics+Coffee](https://codepen.io/amcharts/pen/RNxrqo/) by amCharts ([@amcharts](https://codepen.io/amcharts)) on [CodePen](https://codepen.io).</p>

## Conclusion

Physics engines are not just for games and specialized simulations. They enable us to add stunning effects and, with just a few lines of code, to solve geometry problems that would otherwise have taken us weeks if not months to build on our own.

We've focused here on the box2d engine, which is robust and powerful, but it might get a bit slow on slower devices. Many engines are available. We encourage you to try some out to see which one clicks with you or is best suited to the task at hand. If you just need to solve a problem of overlapping, for example, then a lightweight option might do the trick just as well, and with a far smaller footprint and much lower processing overhead.

**There is virtually no limit to what you can do with the physics of data visualizations.** Create column charts and make them fall like dominos, or make pie charts roll, bounce and more. You can make objects in charts and maps roll, spin, bounce, change shape and morph in ways that will capture the viewer's attention much more quickly than regular static or even interactive versions.

You will find more fancy examples and tools for data visualization on the [amCharts](https://www.amcharts.com "JavaScript Charts and Maps") website.

{{< signature "rb, il, al" >}}

