---
title: 'Diving Into Procedural Content Generation, With WorldEngine'
slug: procedural-content-generation-introduction
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdd3cfdb-da42-4db6-9c73-5929f8027293/16-worldengine-map-6-opt.png
date: 2016-03-28T15:02:25.000Z
author: federicotomassettibretcurtis
description: >-
  When I was young and learning to program, I was fascinated by the possibility
  of creating things that could live inside my monitor. I had the same feeling
  when I started to play with **procedural content generation**, which is to
  find the rules behind a phenomenon, encode them in an algorithm, and use that
  algorithm to create something virtual, but realistic — a plausible simulation.

  Typically, you can give a seed or some initial parameters to a procedural
  content generation algorithm, and get some result. You could generate the
  landscape of a city, the shape of a tree or an entire world.
categories:
  - Coding
  - Data Visualization
---
When I was young and learning to program, I was fascinated by the possibility of creating things that could live inside my monitor. I had the same feeling when I started to play with <strong>procedural content generation</strong>, which is to find the rules behind a phenomenon, encode them in an algorithm, and use that algorithm to create something virtual, but realistic — a plausible simulation.

Typically, you can give a seed or some initial parameters to a procedural content generation algorithm, and get some result. You could generate the landscape of a city, the shape of a tree or an entire world.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Algorithm-Driven Design: How Artificial Intelligence Is Changing Design](https://www.smashingmagazine.com/2017/01/algorithm-driven-design-how-artificial-intelligence-changing-design/)
*   [Playful UX Design: Building A Better Game](https://www.smashingmagazine.com/2012/07/playful-ux-design-building-better-game/)
*   [<span class="headline">Conversational Interfaces: Where Are We Today? Where Are We Heading?</span>](https://www.smashingmagazine.com/2016/07/conversational-interfaces-where-are-we-today-where-are-we-heading/)
*   [Making Embedded Content Work In A Responsive iFrame](https://www.smashingmagazine.com/2014/02/making-embedded-content-work-in-responsive-design/)

Procedural content generation has been in use for the last 40 years in <strong>video games</strong>, and it’s a key characteristic of rogue-like games. Instead of manually writing different levels, defining where walls are or where monsters are hidden, you could <strong>use an algorithm to generate that for you</strong>. You would need some intelligence in the algorithm so that all rooms are reachable, or that monsters are properly distributed across the dungeon. Fun fact: one of the initial reasons to use procedural content generation was to save memory (think about Daggerfall with its 161,600 square kilometers open terrain to explore). If you think about it, you can just save a seed and simply regenerate the world from it each time you play.

{{% feature-panel %}}

Procedural content generation can also be used to simulate scenarios, such as <a href="https://link.springer.com/chapter/10.1007%2F978-3-642-40793-2_4">testing a robot's control algorithm</a>. If you're able to encode the rules of a phenomenon, you can tweak some parameters and run a simulation to understand what factors are the most important in a scenario. Another example would be to simulate flooding by using government-provided digital elevation maps (DEMs) and adjusting various factors like precipitation, ground saturation and density. This would be of benefit to risk assessment in flood insurance or government risk-management analyses.

Nowadays procedural content generation is also used in <strong>movies</strong> when there is the need to generate many similar objects: think about a warehouse with thousands of nearly identical items, or an army of soldiers running down a hill. From a few samples and an algorithm introducing realistic differences you could generate a much larger sample which seems realistic to the eyes of the viewer.

While there are many different situations in which it's possible to use procedural content generation, it's more evident in well-known video games. Think of Diablo or Minecraft. You could play Diablo over and over and find new artifacts and different levels. Today you could walk in Minecraft until the end of time and keep seeing new land being generated for you.

There is one example which is less well known but highly respected by passionate geeks: Dwarf Fortress. In this game an <strong>entire world is simulated with its history</strong>. You could meet a character and find out that a certain ancestor of his slayed a monster who was haunting the area you're passing by. It is an intriguing mix of ASCII art graphics and incredibly deep simulation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/341ab340-20cc-4370-a2ff-cb9f2a816bbc/01-dwarf-fortress-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/591bf016-9f3f-4b8f-ba8d-c6464489851b/01-dwarf-fortress-preview-opt.png" alt="Dwarf Fortress" /></a><figcaption>A city generated on Dwarf Fortress. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/341ab340-20cc-4370-a2ff-cb9f2a816bbc/01-dwarf-fortress-opt.png">View large version</a>)</figcaption></figure>

You can do very complex things with procedural content generation but it can be also very simple.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/428bb4f8-918b-4773-8ead-ba1dbcb57230/02-city-algorithm-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4514076-192b-4686-9209-b9ad4f4200c7/02-city-algorithm-preview-opt.png" alt="city algorithm" /></a><figcaption>A city generated by algorithms in fewer than 100 lines of code on <a href="https://www.google.com/url?q=https://mrdoob.com/lab/javascript/webgl/city/01/&amp;sa=D&amp;usg=AFQjCNEr5EWkJPLdt3X0xQ6VB3X1XPi6tg">https://mrdoob.com/lab/javascript/webgl/city/01/</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/428bb4f8-918b-4773-8ead-ba1dbcb57230/02-city-algorithm-opt.png">View large version</a>)</figcaption></figure>

## WorldEngine

Procedural content generation can generate all sorts of things. You can be very ambitious and generate an entire world: this is the goal of <a href="https://world-engine.org/">WorldEngine</a>. In the rest of this article we'll take a look at how WorldEngine works.

There are many ways to generate a world, some of which are very simple. You can use <strong>simplex noise</strong> (a technique to generate random matrices of values between -1 and 1) to generate an elevation map, where brighter color means higher elevation:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c44bfb4-f517-4d4f-bbef-88faa43ce8c8/03-simplex-noise-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8ba4079-2950-47b5-83f7-6298b0d5cb96/03-simplex-noise-preview-opt.jpg" alt="Simplex Noise" /></a><figcaption>Simplex noise. See tutorial on <a href="https://libnoise.sourceforge.net/tutorials/tutorial3.html">Libnoise</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c44bfb4-f517-4d4f-bbef-88faa43ce8c8/03-simplex-noise-opt.jpg">View large version</a>)</figcaption></figure>

However, this is not realistic. If you look at mountains ranges on Earth you will see that many of them tend to follow a line. Why is that? Because they appear at the border of tectonic plates. It is difficult to obtain realistic maps without simulating such phenomena. Indeed, the best way to generate a realistic world is to simulate the different physical phenomena which shape our world and make it appear as it is.

Let’s compare some real landscapes to those of WorldEngine:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f97bbf2-dab6-491a-8535-f5f1b1e68c4f/04-worldengine-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74a96a84-b8d8-47b4-98b1-a116a4d15e11/04-worldengine-1-preview-opt.png" alt="World Engine" /></a><figcaption>Left: a set of islands north of Japan. Notice that they form a distinct line. Right: a screenshot from a map generated by WorldEngine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f97bbf2-dab6-491a-8535-f5f1b1e68c4f/04-worldengine-1-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2365f3a7-e198-4e30-a4d5-dad8b63f87f7/05-worldengine-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d50d957-8b48-4491-ab45-e3c9d0faddd9/05-worldengine-2-preview-opt.png" alt="World Engine" /></a><figcaption>Left: the Andes mountains (from <a href="https://earthobservatory.nasa.gov/">NASA's Earth Observatory</a>). Look at how it follows the coast. On the right is a mountain range from a map generated by WorldEngine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2365f3a7-e198-4e30-a4d5-dad8b63f87f7/05-worldengine-2-opt.png">View large version</a>)</figcaption></figure>

Simulating plate tectonics allows us to generate a world which has a realistic general appearance. That alone puts WorldEngine ahead of its open source competitors. But there are many other aspects to consider.

Another extremely important characteristic is <strong>erosion</strong>. There are several types of erosion, but the most significant one is hydraulic erosion: erosion caused by water.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2db11821-c80f-4e33-bbab-97606fe43817/06-erosion-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feeaa7c2-a759-45b3-ac6a-1dc17f54863c/06-erosion-preview-opt.png" alt="erosion" /></a><figcaption>Map representing part of the Alps: you can easily see the channels produced by water flowing from the mountains. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2db11821-c80f-4e33-bbab-97606fe43817/06-erosion-opt.png">View large version</a>)</figcaption></figure>

If you do not simulate erosion you will never obtain realistic maps.

There are several algorithms to simulate hydraulic erosion and different aspects should be considered. In particular you want to pick an algorithm which has acceptable performance for your use case. If you want to explore this topic I suggest taking a look at <a href="https://www-evasion.imag.fr/Publications/2007/MDH07/FastErosion_PG07.pdf">“Fast Hydraulic Erosion Simulation and Visualization on GPU”</a> by Xing Mei et al.

You need to consider this point: where does the water come from? From precipitation and ice melting on the top of the mountains.

Consider the factors which control precipitation: the latitude, the temperature, winds, the rain-shadow effect, and so on. The list of phenomena is never-ending. Of course, in a simulation your goal should not be to reproduce completely the complexity of the real phenomena, but understand which elements are the most relevant and how to represent them, perhaps approximately.

There are many aspects to consider and all of them are very interesting to learn, but if your implementation time and CPU cycles are limited you need to identify your priorities. In WorldEngine we spent a good amount of energy refining our biome simulation, which is based on <a href="https://en.wikipedia.org/wiki/Holdridge_life_zones">Holdridge life zones</a>.

While other models could be slightly more precise, they require the simulation of seasonality, which is something we chose not to do in WorldEngine. We have a model which considers temperature and humidity, and can determine what kind of biome is present in an area among forty different types: from subpolar dry tundra to tropical rain forest, passing by subtropical desert scrub. Sure, not all of our users need such a complete model, and these biomes can be grouped in families like desert or jungle.</p>

## Algorithms

This article is an introduction to procedural content generation so it doesn't make sense to go into too many technical details, but it is important to give an idea of how this stuff can be implemented.

Procedural content generation can be used to simulate very different things, so most algorithms are specific to single applications. However, <strong>many different applications of procedural content generation use some form of noise</strong>. This is the case because reality is incredibly complex and rich with details. To properly simulate most real-life phenomena would require unfathomable computational power. Think about a world generator: while it makes sense to represent the phenomena which shape the continents and the main mountain ranges, we cannot simulate single rocks and determine the precise form of the shorelines. What we can do is add some noise to the high-level simulations, obtaining something which is still realistic and detailed, but doesn't require hundreds of thousands of years to be computed. This sounds like a bargain to me!

There are several noise functions. Perlin noise was very widespread in the past, while today it has been superseded by simplex noise. You can think of it as a function taking several parameters and returning a value between -1 and 1. Those parameters represent several dimensions: if you fix all but two of them you will get a bidimensional function which represents your bidimensional noise. You can regard the parameters you fixed as your seed.

Now, a great thing you can do with noise is to <strong>compose noise using different frequencies and amplitudes</strong>. Suppose you have a map and you've applied noise to it. Then you add a new simplex noise (changing the seed) but this time you divide the value of the noise by two, and you also increase the frequency (you simply multiply your coordinates by two). In this way, the second <em>octave</em> of noise will vary twice as fast but will contribute a smaller noise. You can repeat this many times, obtaining a complex noise, which shows both some general pattern and fine-grained details.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/528002c7-18a7-4ce3-b74d-b8df26c7154a/07-noise-periode-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71ceda21-c432-4630-9d92-bb0375398dd1/07-noise-periode-preview-opt.png" alt="noise period" /></a><figcaption>In this series of images you can take a look at how composing noise works. Each of the first seven images has a frequency double of the one preceding it. The last image combines all the images with different factors (the first image has the strongest factor, the second has half that factor, and so on). The final result presents the general pattern of the first image but it has many more details. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/528002c7-18a7-4ce3-b74d-b8df26c7154a/07-noise-periode-opt.jpg">View large version</a>)</figcaption></figure>

Time to see some code. Let's see how we can generate those images in Python:

<pre><code class="language-python">from noise import snoise2 # pip install noise
	from-opt.png import Writer # pip install p-opt.png

	def noise(width, height, seed, period):
	return [[snoise2(x / period * 2, y / period * 2, 1, base=seed) for x in range(width)] for y in range(height)]

	def draw_map(width, height, map, filename, pixel_function):
	"""
	Generic function to draw maps with P-opt.png
	"""
	writer = Writer(width, height)
	pixels = [reduce(lambda x, y: x + y, [pixel_function(elev) for elev in row]) for row in map]
	with open(filename, 'w') as f:
	writer.write(f, pixels)

	def draw_bw_map(width, height, map, filename):
	"""
	Produce black and white pixels
	"""

	def elev_to_pixel(elev):
	v = (elev + 1.0) * 255.0/2.0
	v = min(255, max(0, v))
	return v, v, v

	return draw_map(width, height, map, filename, elev_to_pixel)

	def combine_maps(width, height, maps_and_factors):
	"""
	Combine different maps using a specific weight for each of them
	"""

	def calc_elev(x, y):
	total = reduce(lambda x, y: x+y, [map[y][x] * factor for map, factor in maps_and_factors])
	return total / sum_factors

	sum_factors = reduce(lambda x, y: x + y, [f for m, f in maps_and_factors])
	return [[calc_elev(x, y) for x in range(width)] for y in range(height)]

	def main():
	width = 512
	height = 512
	seed = 77777

	map1 = noise(width, height, seed, 512.0)
	draw_bw_map(width, height, map1, "noise_period512-opt.png")

	map2 = noise(width, height, seed, 256.0)
	draw_bw_map(width, height, map2, "noise_period256-opt.png")

	map3 = noise(width, height, seed, 128.0)
	draw_bw_map(width, height, map3, "noise_period128-opt.png")

	map4 = noise(width, height, seed, 64.0)
	draw_bw_map(width, height, map4, "noise_period64-opt.png")

	map5 = noise(width, height, seed, 32.0)
	draw_bw_map(width, height, map5, "noise_period32-opt.png")

	map6 = noise(width, height, seed, 16.0)
	draw_bw_map(width, height, map6, "noise_period16-opt.png")

	map7 = noise(width, height, seed, 8.0)
	draw_bw_map(width, height, map7, "noise_period8-opt.png")

	map_combined = combine_maps(width, height, [(map1, 64), (map2, 32), (map3, 16), (map4, 8), (map5, 4), (map6, 2), (map7, 1)])
	draw_bw_map(width, height, map_combined, "example_combined-opt.png")

	if __name__ == "__main__":
	main()
</code></pre>

If you look at the main function, you can see that we generate different noise with an <strong>increasingly smaller period</strong>. A smaller period corresponds to a higher frequency. It means that the noise becomes faster – it varies more in a shorter space. We then combine all the single noises with a weight which ranged from 1 for the noise with the shortest period, to 64 for the ones with the longest period.

We use the <i>p-opt.png</i> library to generate images. We simply associate each point with a color ranging from black to white. Black will correspond to the lowest possible value (-1.0), and white to the highest one (+1.0).

At this point we could generate a proper map from this combined noise. The idea is simple: points with high values will be mountains and points with low values will be ocean. In WorldEngine we calculate which level corresponds to sea level by looking for the value which produces a certain percentage of land (for example, 70%). To keep things simple we just pick an arbitrary value (0.25, see line 1 in the code below).</p>

<pre><code class="language-python">ELEV_SEA = 0.25
	ELEV_HILL = 0.65

	...
	def gradient(value, low, high, low_color, high_color):
	"""
	Mix two colors according to the given proportion
	"""
	lr, lg, lb = low_color
	hr, hg, hb = high_color
	_range = float(high - low)
	_x = float(value - low) / _range
	_ix = 1.0 - _x
	r = int(lr * _ix + hr * _x)
	g = int(lg * _ix + hg * _x)
	b = int(lb * _ix + hb * _x)
	r = min(255, max(0, r))
	g = min(255, max(0, g))
	b = min(255, max(0, b))
	return r, g, b

	def draw_color_map(width, height, map, filename):
	"""
	Produce a maps with colors which depend on the elevation
	"""

	ELEV_MIN = -1.0
	ELEV_MOUNTAIN = 1.0

	COAST_COLOR = (203, 237, 128)
	HILL_COLOR = (65, 69, 28)
	MOUNTAIN_COLOR = (226, 227, 218)
	SHALLOW_SEA_COLOR = (128, 237, 235)
	DEEP_SEA_COLOR = (2, 69, 92)

	def elev_to_pixel(elev):
	if elev &gt; ELEV_HILL:
	return gradient(elev, ELEV_HILL, ELEV_MOUNTAIN, HILL_COLOR, MOUNTAIN_COLOR)
	elif elev &gt; ELEV_SEA:
	return gradient(elev, ELEV_SEA, ELEV_HILL, COAST_COLOR, HILL_COLOR)
	else:
	return gradient(elev, ELEV_MIN, ELEV_SEA, DEEP_SEA_COLOR, SHALLOW_SEA_COLOR)

	return draw_map(width, height, map, filename, elev_to_pixel)

	...    

	def main():
	...
	draw_color_map(width, height, map_combined, "example_combined_color-opt.png")
</code></pre>

We assign specific colors to certain elevation values. We have one for: the deepest possible sea (elevation -1.0); for the shallowest sea (elevation just below 0.25); for the coast (elevation 0.25); for hills (elevation 0.65); and for mountains (elevation 1.00). Then we look at the elevation of each point and find the range it is contained in.

We can then calculate the color of that point as a mix between the colors of the two extremes of the range. For example, a value of elevation 0.70 will correspond to a color obtained by mixing the color for hills and the one for mountains. It will be closer to the color for hills because 0.70 is closer to 0.65 (hills) than 1.00 (mountains). You can see the result in the image below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34a11aba-ac50-49a4-9815-b9da26e3ddf0/08-combined-color-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88a699c4-ab7b-4486-a055-5fed75cc502d/08-combined-color-preview-opt.png" alt="combined color" /></a><figcaption>Result of assigning specific colors to certain elevation values. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34a11aba-ac50-49a4-9815-b9da26e3ddf0/08-combined-color-opt.png">View large version</a>)</figcaption></figure>

To add more character to the map we can <strong>apply erosion</strong>. There are several algorithms to implement erosion and some of them work better at a low-level scale. However, here we have the map of an entire world and we need to use an algorithm which works at an appropriate scale, producing results which are realistic, visible and can be run in a reasonable amount of time. We are going to adapt the algorithm we use in WorldEngine.

The algorithm is designed to work on an instance of <code>world</code>, a class defined in WorldEngine. For this example, we provided a simple implementation of <code>world</code> which can be instantiated passing the elevation map we have created together. A <code>world</code> should also have its precipitation map, but in this case we just assume precipitation is uniform and we pick an arbitrary value. We need also an implementation of the A-Star algorithm to find paths. We added that implementation in the <a href="https://github.com/ftomassetti/procedural-content-generation-examples">example available at GitHub</a> but unfortunately there's no space to discuss it here. Let's take a look instead at the interesting part: <strong>the erosion algorithm</strong>:

<pre><code class="language-python">def execute(self, world, seed):
	water_flow = numpy.zeros((world.height, world.width))
	water_path = numpy.zeros((world.height, world.width), dtype=int)
	river_list = []
	lake_list = []
	river_map = numpy.zeros((world.height, world.width))
	lake_map = numpy.zeros((world.height, world.width))

	# step one: water flow per cell based on rainfall
	self.find_water_flow(world, water_path)

	# step two: find river sources (seeds)
	river_sources = self.river_sources(world, water_flow, water_path)

	# step three: for each source, find a path to sea
	for source in river_sources:
	river = self.river_flow(source, world, river_list, lake_list)
	if len(river) &gt; 0:
	river_list.append(river)
	self.cleanUpFlow(river, world)
	rx, ry = river[-1]  # find last cell in river
	if not world.is_ocean((rx, ry)):
	lake_list.append(river[-1])  # river flowed into a lake

	# step four: simulate erosion and updating river map
	for river in river_list:
	self.river_erosion(river, world)
	self.rivermap_update(river, water_flow, river_map, world.precipitations)

	# step five: rivers with no paths to sea form lakes
	for lake in lake_list:
	# print "Found lake at:",lake
	lx, ly = lake
	lake_map[ly, lx] = 0.1  # TODO: make this based on rainfall/flow

	return river_map, lake_map
</code></pre>

We start by calculating for each cell, which direction the water would flow from there (line 10), then we find river sources. We look for points with high elevation which collect a certain amount of in-flow from other cells (line 13). Then we calculate the path between the sources and the sea. Rivers which cannot reach the sea generate lakes (line 23). At this point we calculate erosion (line 27). Basically, we remove terrain depending on the amount of water flowing in. At the end of this process we have an eroded map, and as a by-product we have also a list of rivers and lakes present in our world.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f9e6d67-37dc-494c-96c7-eb3069e518fe/09-eroded-detail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0408e3d4-60f0-4690-b2b6-011d20f84685/09-eroded-detail-preview-opt.png" alt="Eroded detail" /></a><figcaption>Result of an eroded map. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f9e6d67-37dc-494c-96c7-eb3069e518fe/09-eroded-detail-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8919a832-1c0f-4c4a-8532-b27a9b2c5051/10-eroded-details-shadow-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/845cf831-2e5b-4f1b-9842-af897637523a/10-eroded-details-shadow-preview-opt.png" alt="Eroded detail shadow" /></a><figcaption>If you observe the map closely you'll notice the effects of erosion. Adding shadows makes it much easier to perceive the depth of the map and to pick out valleys and ridges carved by hydraulic erosion. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8919a832-1c0f-4c4a-8532-b27a9b2c5051/10-eroded-details-shadow-opt.png">View large version</a>)</figcaption></figure>

Drawing the shadows is reasonably easy. You suppose the sun has a certain position with respect to the map (for example, north-west); then for each cell you consider a few neighbours which are between the sun and the cell in question. If they have a greater altitude than the cell, they will cast a shadow on it. The color of the cell is than mixed with black (using the gradient function) proportionally to the amount of shadow present. More shadow means that the cell will look darker.</p>

<pre><code class="language-python">def shadow_color(color, x, y):
	alt = map[y][x]
	delta = 0
	for dist in range(SHADOW_RADIUS):
	# To avoid picking unexisting cells
	if x &gt; dist and y &gt; dist:
	other = map[y-1-dist][x-1-dist]
	diff = other-alt
	if other &gt; ELEV_SEA and other&gt;alt:
	delta += diff/(1.0+dist)
	delta = min(0.2, delta)
	return gradient(delta, 0, 0.2, color, (0, 0, 0))
</code></pre>

This should give you an idea of what we can achieve by combining a couple of reasonably simple algorithms. Let's see what we do to produce worlds in WorldEngine.</p>

### Algorithms In WorldEngine

In WorldEngine we use a lot of different algorithms for our simulations, but we apply simplex noise for all of the results. We start by using noise to generate the initial height map. Then we run the <strong>plate simulation</strong>: we move the plates around, we simulate plates clashing, mountains rising and so forth. To the final results we add more noise. At this point we translate the map to place the lowest elevation at the borders and the highest at the center. We then start to pour water from the borders, until we cover a certain percentage of the map. This is how we get the preliminary height map.

We then calculate the temperature. This depends on the elevation and the latitude of each single point. After that, we calculate the precipitation, which depends on the temperature and the noise. Once we have the temperature and the precipitation we are able to simulate hydraulic erosion. It is not really easy to get something which is realistic and fast enough to calculate. Our algorithm selects initial flow sources and then simulates how the water moves down, removing terrain as it passes and bringing sediment with the flow. It then looks for a path to the sea. It could end in a pit and form a lake, or manage to grow into a river. This is how we get our refined height map.

We consider precipitation for each single cell and we look how the water flows. Obviously, not all the cells will produce the same amount of precipitation. Because of the erosion, normally paths will tend to converge and water will be grouped along rivers. We determine in this way the single streams and the amount of water for each of them. Once we have the streams we calculate which areas can be irrigated from these streams and the permeability and humidity of each zone; once again we use noise in those steps. Finally we calculate the icecaps and we are done.

As you can see, we use many different simulations (and we are going to add some more), but one fundamental element is noise: without it, all simulations would seem predictable and boring.</p>

## How To Represent A Generated World

Once you have run several simulations you have a complete world full of details. You could now use it for your games, your simulations or any other goal that comes to mind. However, you have a new problem: how can you take a look? How do you represent this complex world for the user?

For each single point you have several pieces of information: you know the temperature and the precipitation, the elevation and the biome, even on which tectonic plate it sits.

WorldEngine can generate several different maps for a world.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec101bac-ab49-407a-b40e-04f428ef954a/11-worldengine-map-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd13eb53-bb17-4f1b-856a-143e1021a0b8/11-worldengine-map-1-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Precipitation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec101bac-ab49-407a-b40e-04f428ef954a/11-worldengine-map-1-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e42772cb-16a9-4438-b70d-d3f66b34b51e/12-worldengine-map-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e0f47bc-72a4-456d-a61f-bd794448823a/12-worldengine-map-2-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Temperature. In this map you can see that the main effect is due to latitude, though you can see spots with a lower temperature: they're the peaks and higher mountains. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e42772cb-16a9-4438-b70d-d3f66b34b51e/12-worldengine-map-2-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95434ba5-4d4c-47db-8d2f-a632ef1729e6/13-worldengine-map-3-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f44fc7e4-cf74-4bf0-82b3-9dd18ed9f2a8/13-worldengine-map-3-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Biome. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95434ba5-4d4c-47db-8d2f-a632ef1729e6/13-worldengine-map-3-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b4c71b-e21b-413d-a0b8-83c14d393407/14-worldengine-map-4-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b69d350-1bda-4a2f-bd1e-ca94e94a5bf2/14-worldengine-map-4-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Elevation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b4c71b-e21b-413d-a0b8-83c14d393407/14-worldengine-map-4-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ccccfde-6801-46f8-b1ce-1ae89af6b273/15-worldengine-map-5-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b57fb0d-47b7-40eb-8a42-f9e7fc9b67c8/15-worldengine-map-5-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - The world viewed from space. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ccccfde-6801-46f8-b1ce-1ae89af6b273/15-worldengine-map-5-opt.png">View large version</a>)</figcaption></figure>

Now, let’s take a look at this map for a second. There are two things that it are easy to overlook.

Elevation has shadows. Without shadows, it's very difficult to perceive elevation. The icecap is represented and this is possible because we know the temperature of each point.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdd3cfdb-da42-4db6-9c73-5929f8027293/16-worldengine-map-6-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1933d527-cf24-4c73-8498-d3379873008a/16-worldengine-map-6-preview-opt.png" alt="World Engine Map" /></a><figcaption>Another representation of the same world. This is what we call an “ancient map” and it is an example of how the same data can be presented in very different ways. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdd3cfdb-da42-4db6-9c73-5929f8027293/16-worldengine-map-6-opt.png">View large version</a>)</figcaption></figure>

WorldEngine generate worlds with a lot of information about each one. The world is basically a large matrix with different layers of information. For each tile there's information about:

*   on which tectonic plates the tile is placed
*   if the tile is an ocean tile or not
*   the elevation of the tile
*   the presence of rivers or lakes in the tile (if it's a land tile)
*   the presence of icecap (if it's an ocean tile)
*   values for the humidity, irrigation, permeability, precipitation and temperature of the tile
*   the biome present in the tile

### What Can Be Done With This Data?

Different users could need different parts of the data and ignore the rest of the information generated. Some uses of the data include:

*   Earthquakes and volcanoes could appear near tectonic plate borders
*   In an exploration game, ships could not enter the icecap region
*   Rivers could play an important role, to make the surrounding land more fertile, or requiring a bridge to be crossed – think of Egypt and the Nile.
*   Different biomes could affect the kind of animals which live in the area, or if they're suitable or not for establishing a new city.</p>

### How To Use This Data

One possible use is to generate beautiful maps to use as a wallpaper. WorldEngine can generate worlds in different open formats (currently protobuf and HDF5) for its users to do whatever they want.There are libraries which can load these formats in many different languages (for example, you can load protobuf files in C++, Java, Python, Ruby, Nano, Objective-C and C#).

For exporting the elevation map alone, WorldEngine supports <a href="https://www.gdal.org/formats_list.html">all the formats offered by the Geospatial Data Abstraction Library (GDAL)</a>: that is a long list. While WorldEngine would export just the elevation map, that elevation would have been affected by all the phenomena based on the other information that would be discarded.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdb3cbb-f5ef-447d-b13b-2f164dcc543c/17-map-tmx-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8937aad0-16bb-430f-aeb4-214cb1beb837/17-map-tmx-preview-opt.png" alt="TMX export" /></a><figcaption>TMX export of WordEngine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdb3cbb-f5ef-447d-b13b-2f164dcc543c/17-map-tmx-opt.png">View large version</a>)</figcaption></figure>

WorldEngine is going to be able to export maps in the <a href="https://doc.mapeditor.org/reference/tmx-map-format/">Tile Map XML (TMX) format</a>, which is supported by dozens of libraries and used in many games. It is also notably supported by the <a href="https://www.mapeditor.org/">Tiled editor</a>.

The creator of the Air XenoDawn video game told me that starting from a map helped him to create a story and give it some depth. I read a similar sentiment in the <a href="https://en.wikipedia.org/wiki/The_Rivan_Codex">Rivan Codex from David Eddings</a>: in that book my favorite fantasy novelist describes how he created his saga and how for him a good map was central to the creativity process. From a map he could envision the specificity of the people who lived there, by the coast or on the mountains, in a cold region or close to equator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6b20bd0-7398-479c-8bba-271e58428238/18-air-xenodawn-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83674dee-5d3f-410d-ab5a-1fd86fe8bc89/18-air-xenodawn-preview-opt.png" alt="Air XenoDawn" /></a><figcaption>The Air XenoDawn videogame (released on Steam) uses maps generated from WorldEngine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6b20bd0-7398-479c-8bba-271e58428238/18-air-xenodawn-opt.jpg">View large version</a>)</figcaption></figure>

WorldEngine has been used to generate maps for <a href="https://wl.widelands.org/maps/lost-islands/">Widelands</a>

## WorldEngine: An Open Source Project

To generate realistic worlds through procedural content generation is not an easy task. In addition to a theoretical background, a lot of effort is needed to implement different simulation techniques in way that is realistic and practical: no one wants to wait ten hours in front a monitor to generate a world.

	return river_map, lake_map
</code></pre>

We start by calculating for each cell, which direction the water would flow from there (line 10), then we find river sources. We look for points with high elevation which collect a certain amount of in-flow from other cells (line 13). Then we calculate the path between the sources and the sea. Rivers which cannot reach the sea generate lakes (line 23). At this point we calculate erosion (line 27). Basically, we remove terrain depending on the amount of water flowing in. At the end of this process we have an eroded map, and as a by-product we have also a list of rivers and lakes present in our world.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f9e6d67-37dc-494c-96c7-eb3069e518fe/09-eroded-detail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0408e3d4-60f0-4690-b2b6-011d20f84685/09-eroded-detail-preview-opt.png" alt="Eroded detail" /></a><figcaption>Result of an eroded map. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f9e6d67-37dc-494c-96c7-eb3069e518fe/09-eroded-detail-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8919a832-1c0f-4c4a-8532-b27a9b2c5051/10-eroded-details-shadow-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/845cf831-2e5b-4f1b-9842-af897637523a/10-eroded-details-shadow-preview-opt.png" alt="Eroded detail shadow" /></a><figcaption>If you observe the map closely you'll notice the effects of erosion. Adding shadows makes it much easier to perceive the depth of the map and to pick out valleys and ridges carved by hydraulic erosion. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8919a832-1c0f-4c4a-8532-b27a9b2c5051/10-eroded-details-shadow-opt.png">View large version</a>)</figcaption></figure>

Drawing the shadows is reasonably easy. You suppose the sun has a certain position with respect to the map (for example, north-west); then for each cell you consider a few neighbours which are between the sun and the cell in question. If they have a greater altitude than the cell, they will cast a shadow on it. The color of the cell is than mixed with black (using the gradient function) proportionally to the amount of shadow present. More shadow means that the cell will look darker.</p>

<pre><code class="language-python">def shadow_color(color, x, y):
	alt = map[y][x]
	delta = 0
	for dist in range(SHADOW_RADIUS):
	# To avoid picking unexisting cells
	if x &gt; dist and y &gt; dist:
	other = map[y-1-dist][x-1-dist]
	diff = other-alt
	if other &gt; ELEV_SEA and other&gt;alt:
	delta += diff/(1.0+dist)
	delta = min(0.2, delta)
	return gradient(delta, 0, 0.2, color, (0, 0, 0))
</code></pre>

This should give you an idea of what we can achieve by combining a couple of reasonably simple algorithms. Let's see what we do to produce worlds in WorldEngine.</p>

### Algorithms In WorldEngine

In WorldEngine we use a lot of different algorithms for our simulations, but we apply simplex noise for all of the results. We start by using noise to generate the initial height map. Then we run the <strong>plate simulation</strong>: we move the plates around, we simulate plates clashing, mountains rising and so forth. To the final results we add more noise. At this point we translate the map to place the lowest elevation at the borders and the highest at the center. We then start to pour water from the borders, until we cover a certain percentage of the map. This is how we get the preliminary height map.

We then calculate the temperature. This depends on the elevation and the latitude of each single point. After that, we calculate the precipitation, which depends on the temperature and the noise. Once we have the temperature and the precipitation we are able to simulate hydraulic erosion. It is not really easy to get something which is realistic and fast enough to calculate. Our algorithm selects initial flow sources and then simulates how the water moves down, removing terrain as it passes and bringing sediment with the flow. It then looks for a path to the sea. It could end in a pit and form a lake, or manage to grow into a river. This is how we get our refined height map.

We consider precipitation for each single cell and we look how the water flows. Obviously, not all the cells will produce the same amount of precipitation. Because of the erosion, normally paths will tend to converge and water will be grouped along rivers. We determine in this way the single streams and the amount of water for each of them. Once we have the streams we calculate which areas can be irrigated from these streams and the permeability and humidity of each zone; once again we use noise in those steps. Finally we calculate the icecaps and we are done.

As you can see, we use many different simulations (and we are going to add some more), but one fundamental element is noise: without it, all simulations would seem predictable and boring.</p>

## How To Represent A Generated World

Once you have run several simulations you have a complete world full of details. You could now use it for your games, your simulations or any other goal that comes to mind. However, you have a new problem: how can you take a look? How do you represent this complex world for the user?

For each single point you have several pieces of information: you know the temperature and the precipitation, the elevation and the biome, even on which tectonic plate it sits.

WorldEngine can generate several different maps for a world.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec101bac-ab49-407a-b40e-04f428ef954a/11-worldengine-map-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd13eb53-bb17-4f1b-856a-143e1021a0b8/11-worldengine-map-1-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Precipitation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec101bac-ab49-407a-b40e-04f428ef954a/11-worldengine-map-1-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e42772cb-16a9-4438-b70d-d3f66b34b51e/12-worldengine-map-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e0f47bc-72a4-456d-a61f-bd794448823a/12-worldengine-map-2-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Temperature. In this map you can see that the main effect is due to latitude, though you can see spots with a lower temperature: they're the peaks and higher mountains. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e42772cb-16a9-4438-b70d-d3f66b34b51e/12-worldengine-map-2-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95434ba5-4d4c-47db-8d2f-a632ef1729e6/13-worldengine-map-3-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f44fc7e4-cf74-4bf0-82b3-9dd18ed9f2a8/13-worldengine-map-3-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Biome. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95434ba5-4d4c-47db-8d2f-a632ef1729e6/13-worldengine-map-3-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b4c71b-e21b-413d-a0b8-83c14d393407/14-worldengine-map-4-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b69d350-1bda-4a2f-bd1e-ca94e94a5bf2/14-worldengine-map-4-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - Elevation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b4c71b-e21b-413d-a0b8-83c14d393407/14-worldengine-map-4-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ccccfde-6801-46f8-b1ce-1ae89af6b273/15-worldengine-map-5-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b57fb0d-47b7-40eb-8a42-f9e7fc9b67c8/15-worldengine-map-5-preview-opt.png" alt="World Engine Map" /></a><figcaption>WorldEngine - The world viewed from space. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ccccfde-6801-46f8-b1ce-1ae89af6b273/15-worldengine-map-5-opt.png">View large version</a>)</figcaption></figure>

Now, let’s take a look at this map for a second. There are two things that it are easy to overlook.

Elevation has shadows. Without shadows, it's very difficult to perceive elevation. The icecap is represented and this is possible because we know the temperature of each point.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdd3cfdb-da42-4db6-9c73-5929f8027293/16-worldengine-map-6-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1933d527-cf24-4c73-8498-d3379873008a/16-worldengine-map-6-preview-opt.png" alt="World Engine Map" /></a><figcaption>Another representation of the same world. This is what we call an “ancient map” and it is an example of how the same data can be presented in very different ways. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdd3cfdb-da42-4db6-9c73-5929f8027293/16-worldengine-map-6-opt.png">View large version</a>)</figcaption></figure>

WorldEngine generate worlds with a lot of information about each one. The world is basically a large matrix with different layers of information. For each tile there's information about:

*   on which tectonic plates the tile is placed
*   if the tile is an ocean tile or not
*   the elevation of the tile
*   the presence of rivers or lakes in the tile (if it's a land tile)
*   the presence of icecap (if it's an ocean tile)
*   values for the humidity, irrigation, permeability, precipitation and temperature of the tile
*   the biome present in the tile

### What Can Be Done With This Data?

Different users could need different parts of the data and ignore the rest of the information generated. Some uses of the data include:

*   Earthquakes and volcanoes could appear near tectonic plate borders
*   In an exploration game, ships could not enter the icecap region
*   Rivers could play an important role, to make the surrounding land more fertile, or requiring a bridge to be crossed – think of Egypt and the Nile.
*   Different biomes could affect the kind of animals which live in the area, or if they're suitable or not for establishing a new city.</p>

### How To Use This Data

One possible use is to generate beautiful maps to use as a wallpaper. WorldEngine can generate worlds in different open formats (currently protobuf and HDF5) for its users to do whatever they want.There are libraries which can load these formats in many different languages (for example, you can load protobuf files in C++, Java, Python, Ruby, Nano, Objective-C and C#).

For exporting the elevation map alone, WorldEngine supports <a href="https://www.gdal.org/formats_list.html">all the formats offered by the Geospatial Data Abstraction Library (GDAL)</a>: that is a long list. While WorldEngine would export just the elevation map, that elevation would have been affected by all the phenomena based on the other information that would be discarded.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdb3cbb-f5ef-447d-b13b-2f164dcc543c/17-map-tmx-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8937aad0-16bb-430f-aeb4-214cb1beb837/17-map-tmx-preview-opt.png" alt="TMX export" /></a><figcaption>TMX export of WordEngine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdb3cbb-f5ef-447d-b13b-2f164dcc543c/17-map-tmx-opt.png">View large version</a>)</figcaption></figure>

WorldEngine is going to be able to export maps in the <a href="https://doc.mapeditor.org/reference/tmx-map-format/">Tile Map XML (TMX) format</a>, which is supported by dozens of libraries and used in many games. It is also notably supported by the <a href="https://www.mapeditor.org/">Tiled editor</a>.

The creator of the Air XenoDawn video game told me that starting from a map helped him to create a story and give it some depth. I read a similar sentiment in the <a href="https://en.wikipedia.org/wiki/The_Rivan_Codex">Rivan Codex from David Eddings</a>: in that book my favorite fantasy novelist describes how he created his saga and how for him a good map was central to the creativity process. From a map he could envision the specificity of the people who lived there, by the coast or on the mountains, in a cold region or close to equator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6b20bd0-7398-479c-8bba-271e58428238/18-air-xenodawn-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83674dee-5d3f-410d-ab5a-1fd86fe8bc89/18-air-xenodawn-preview-opt.png" alt="Air XenoDawn" /></a><figcaption>The Air XenoDawn videogame (released on Steam) uses maps generated from WorldEngine. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6b20bd0-7398-479c-8bba-271e58428238/18-air-xenodawn-opt.jpg">View large version</a>)</figcaption></figure>

WorldEngine has been used to generate maps for <a href="https://wl.widelands.org/maps/lost-islands/">Widelands</a>

## WorldEngine: An Open Source Project

To generate realistic worlds through procedural content generation is not an easy task. In addition to a theoretical background, a lot of effort is needed to implement different simulation techniques in way that is realistic and practical: no one wants to wait ten hours in front a monitor to generate a world.

To build such a complex world generator has been possible because a community has grown around it. We have taken advantage of an existing project named <a href="https://sourceforge.net/projects/platec/">PlaTec, built by Lauri Viitanen</a> for his Masters thesis, and implemented the plate tectonics simulation. The community resurrected his code, porting it on several platforms, evolving it and make it more easily usable.

WorldEngine was then born by merging two separate projects, created by the current maintainers of WorldEngine (me and Bret Curtis).

To make WorldEngine a healthy <strong>open source project</strong>, a lot of effort has been made on improving tests, continuous integration, support for several platforms, building binary packages, addressing the issues reported, and promoting the project. From these efforts a healthy community of about ten developers has been grown, and more and more features are being implemented. Recently version 0.19.0 was released and the work keeps going on toward version 1.0.0. We hope to reach that soon and keep working to provide better worlds where endless adventures can be had. We hope you can have fun with WorldEngine and perhaps help us improve it.</p>

## Conclusions

Procedural content generation is fascinating: <strong>it helps us understand the forces which shape reality</strong> and allows us to play with them, creating something beautiful. I find it fulfilling just to learn about the phenomena which shape the world and simulate them, but this is just the start of infinite possible adventures that can be set on these worlds: all sort of games and simulations can use the results of procedural content generation in general and WorldEngine in particular. Infinite, complex, realistic worlds are just one click away.

{{< signature "jb, ml, rb, og" >}}

