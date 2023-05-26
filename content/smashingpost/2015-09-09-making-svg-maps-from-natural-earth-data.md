---
title: A Guide To Building SVG Maps From Natural Earth Data
slug: making-svg-maps-from-natural-earth-data
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f249531-519c-4438-a5bb-c3fed6e821cb/09-interactive-world-opt.png
date: 2015-09-09T21:25:48.000Z
author: chrisyouderian
description: >-
  **Interactive maps** are a fantastic way to present geographic data to your
  visitors. Libraries like Google Maps and Open Street Maps are a popular choice
  to do this and they excel at visualizing street-level data. However, for
  small-scale maps, **SVG maps** are often a better option. They are
  lightweight, fully customizable and are not encumbered by any licensing
  restrictions.

  It's possible to find a number of SVG maps released under permissible licenses
  in the Wikimedia Commons. Unfortunately, it's likely that you will eventually
  find these options lacking. The map you need may not exist, may be out of date
  (as borders change), or may not be well-formatted for web use. This article
  will explain **how to create your own SVG maps using Natural Earth data** and
  open source tools. You will then be able to create SVG maps of any area of the
  world, using any projection, at any resolution. As an illustration, we will
  create an SVG world map.
categories:
  - Coding
  - Maps
  - SVG
---
**Interactive maps** are a fantastic way to present geographic data to your visitors. Libraries like Google Maps and Open Street Maps are a popular choice to do this and they excel at visualizing street-level data. However, for small-scale maps, **SVG maps** are often a better option. They are lightweight, fully customizable and are not encumbered by any licensing restrictions.

It's possible to find a number of SVG maps released under permissible licenses in the Wikimedia Commons. Unfortunately, it's likely that you will eventually find these options lacking. The map you need may not exist, may be out of date (as borders change), or may not be well-formatted for web use. This article will explain **how to create your own SVG maps using Natural Earth data** and open source tools. You will then be able to create SVG maps of any area of the world, using any projection, at any resolution. As an illustration, we will create an SVG world map.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Adventures In The Third Dimension: CSS 3D Transforms](https://www.smashingmagazine.com/2012/01/adventures-in-the-third-dimension-css-3-d-transforms/)
*   [Animating Clipped Elements In SVG](https://www.smashingmagazine.com/2015/12/animating-clipped-elements-svg/)
*   [Designing an Interactive Exhibition With CSS Clip Paths](https://www.smashingmagazine.com/2015/06/the-making-of-in-pieces/)
*   [The Illusion Of Life: An SVG Animation Case Study](https://www.smashingmagazine.com/2016/07/an-svg-animation-case-study/)

The process will require us to:

{{% feature-panel %}}

*   Download geographic data from Natural Earth data
*   View and edit the geographic data using QGIS
*   Convert the geographic data into SVG using Kartograph.py

## Getting The Geographic Data

To start, we need **geographic data** for country borders. This data is available from [Natural Earth](https://www.naturalearthdata.com/). Natural Earth is built by volunteers and supported by the North American Cartographic Information Society. It specializes in small-scale maps that are well-suited for the web. This means the maps will look great at the country or province level, but aren’t of a high enough resolution to show the neighborhoods of a city. Natural Earth releases its maps into the public domain.

To see all maps available for download, view the [Natural Earth downloads page](https://www.naturalearthdata.com/downloads/).

Many borders in the world are hotly contested. Natural Earth’s policy is to draw borders based on who controls the situation on the ground. We will be primarily working off of a small-scale cultural map, which contains all 247 countries in the world, and has boundary lakes removed. You can [download it as a zip file (186KB)](https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/110m/cultural/ne_110m_admin_0_countries_lakes.zip).

The data you download is stored in the [shapefile](https://en.wikipedia.org/wiki/Shapefile) (_.shp_) format. Shapefile is an open standard geospatial vector data format created by Esri. The shapefile is accompanied by complementary files with the following extensions: _.dbf_, _.prj_ and _.shx_. Together, these files contain the vector geometry, attributes (`name`, `id`, etc.) and geospatial information for each country. For simplicity, when people refer to a shapefile, they are really referring to this group of files.</p>

## Viewing The Geographic Data

To see the data we just downloaded, we need to use [GIS](https://en.wikipedia.org/wiki/Geographic_information_system) (geographic information systems) software. QGIS is open source GIS software. It runs on Linux, Mac OS X and Windows. [Download it from QGIS.](https://www.qgis.org/en/site/index.html) This tutorial will be using QGIS 2.8.2 Wien.

After you have installed QGIS, open the QGIS Desktop application. QGIS is a powerful program that can work with many types of geographic data. Because of this, it can be quite intimidating. We’ll only be using a small fraction of its functionality and can ignore much of what QGIS offers. For example, since we aren’t working with any raster images (like satellite photography), we can ignore tools related to raster images.

To get started, we’ll add our shapefile as a vector layer to our project.

*   Select **Layer → Add Layer → Add Vector Layer** (from the menu bar)
*   Browse to and open _ne_110m_admin_0_countries_lakes.shp_
*   The map should appear in the window (it may be a different color for you)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0263507c-98a1-4c3e-ab72-4d4239c831a5/01-world-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b80af98f-d01c-4fb5-9c15-562616a9c224/01-world-opt-small.png" alt="World map" /></a><figcaption>The world map vector layer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0263507c-98a1-4c3e-ab72-4d4239c831a5/01-world-opt.png">View large version</a>)</figcaption></figure>

Notice that _ne_110m_admin_0_countries_lakes.shp_ has been added to the **Layers** dialog.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326c813d-ede7-444a-b7a6-3c19a7d243df/02-layer-opt.png" alt="Layers dialog" /><figcaption>The new layer. </figcaption></figure>

Layers in QGIS are similar to layers you find in photo editing software like Photoshop or GIMP. _You must select a layer before you can work on it_. As you go through this tutorial, if you find a tool isn’t working properly, you have likely neglected to select the current layer.

It's also possible to hide layers from view by unchecking the box. This allows you to add multiple shapefiles to your project and view them individually.

After adding a vector layer, it’s a good idea to save your work: **Project → Save**

Each country contains a list of attributes. You can view these attributes in a table: **Layer → Open Attribute Table**

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d76daa98-abce-40b5-be44-6455c5f12215/03-table-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/637ff837-92ab-41f0-9164-9056f4913477/03-table-opt-small.png" alt="Attribute table" /></a><figcaption>The country attribute table. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d76daa98-abce-40b5-be44-6455c5f12215/03-table-opt.png">View large version</a>)</figcaption></figure>

The Natural Earth data contains a wealth of information about each country. We’ll be using [two-letter ISO codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) to uniquely identify countries. These are stored in the `iso_a2` variable. We’ll also use the country name (`name`) to label countries in our SVG file. Feel free to explore the table to get a sense of the data. When you’re done, close the table.</p>

## Editing The Geographic Data

_(You can skip this section if you are happy with the Natural Earth data defaults.)_

It's possible to **edit the individual geographic shapes** using QGIS. You will probably not need to redraw borders, but you may want to split a country into parts.

Each shape in our shapefile is referred to as a _feature_ in QGIS. To select a feature, choose: **View → Select → Select Feature(s)** and then click on your target. The entire feature should turn yellow. For example, this is what France looks like when you click on it:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c52e413-7088-412d-b939-0dbe97e21076/04-france-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b97ccc54-7339-4e16-8342-5c53b79673a4/04-france-opt-small.png" alt="France selected" /></a><figcaption>France is selected and highlighted. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c52e413-7088-412d-b939-0dbe97e21076/04-france-opt.png">View large version</a>)</figcaption></figure>

Notice that France includes French Guiana in South America. This is because French Guiana is an overseas département and region of France ([French Guiana on Wikipedia](https://en.wikipedia.org/wiki/French_Guiana)). Nonetheless, French Guiana has its own unique ISO code and, for many applications, it makes sense to display it as a separate entity.

Splitting France into two separate entities is a straightforward process, but it requires a number of steps:

<ol><br>
<li>Install the Digitizing Tools QGIS Plugin: 
<ul><br>
<li><strong>Plugins &#8594; Manage and Install Plugins
</strong></li>   
  <li>Search for <strong>Digitizing Tools</strong></li>   
  <li>Select <strong>Digitizing Tools</strong></li>  
  <li><strong>Install Plugin</strong></li>
  </ul>
</li>

<li>Display editing tools in the toolbar: <strong>View &#8594; Toolbars &#8594; Advanced Digitizing</strong>; and <strong>View &#8594; Toolbars &#8594; Digitizing Tools</strong></li>

<li>Put the map in edit mode: <strong>Layer &#8594; Toggle Editing</strong></li>

<li>Select France: <strong>View &#8594; Select &#8594; Select Feature(s)</strong></li>

<li>Click on France in the map view</li>

<li>Choose <strong>Split selected multi-part features to single part</strong> from the toolbar.</p>

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ec6972-dbe6-4bf1-8f22-5c41c8a9fd73/05-split-opt.png" alt="05-split-opt" /><figcaption></figcaption></figure>

This will split all parts of France into separate entities.</li>

<li>Put France back together:

<ul>
<li>Select both the mainland of France and the island of Corsica. To select multiple features, hold down Ctrl (Cmd on Mac).</li>
<li>Merge the mainland of France and the island Corsica (<strong>Edit &#8594; Merge Selected Features</strong>) – you will be alerted that the feature attributes will also be merged. Click <strong>OK</strong>.</li>
</ul>
</li>

<li>Edit French Guiana’s attributes:

<ul><br>
<li><strong>View &#8594; Identify Features</strong></li>
<li>Click on French Guiana. This will bring up the attributes for French Guiana. It currently has the attributes for France. We need to replace these with attributes for French Guiana. Click on the <strong>Edit feature form</strong> icon as shown in the screenshot. Replace the ISO code with “GF” and the name with “French Guiana”.</li>
</ul>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12231e6a-f17c-4f5a-956b-374c113edba0/06-table-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f6c3db1-10e9-438d-86a3-3462a129fc50/06-table-opt-small.png" alt="Replacing attributes" /></a><figcaption>Replacing French Guiana’s attributes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12231e6a-f17c-4f5a-956b-374c113edba0/06-table-opt.png">View large version</a>)</figcaption></figure>

</li>

<li>Save your changes: <strong>Layer &#8594; Save Layer Edits</strong></li>
</ol>

That’s all! French Guiana is now its own feature and we’ve given it unique attributes. To learn more about editing, check out the [QGIS documentation](https://docs.qgis.org/testing/en/docs/user_manual/working_with_vector/editing_geometry_attributes.html).

## Creating SVG Files With Kartograph.py

[Kartograph.py](https://kartograph.org/about/kartograph.py/) is a lightweight Python library that will convert our shapefile into a web-friendly SVG file. It was created by New York Times graphics editor [Gregor Aisch](https://driven-by-data.net/) and is available under an AGPL license.

To install Kartograph.py, [follow these installation instructions](https://kartograph.org/docs/kartograph.py/#installing-kartograph-py). This process will require you to install a number of dependencies. If you’re not ready to commit to so many installations, you can install Kartograph.py in a virtual machine. Or, you can just download the SVG output shown as images in this article. This tutorial was created using Kartograph.py installed in Ubuntu 14.04 LTS.

Kartograph is a command line program that **requires a JSON configuration file**. Name this file _config.json_ and place it in the same directory as the shapefile. This file must contain a `layers` property with a dictionary of the layers we want to convert and the location of each layer’s shapefile. To convert _ne_110m_admin_0_countries_lakes.shp_ we can use the following _config.json_:

<pre><code class="language-javascript">{
  &quot;layers&quot;: {
    &quot;countries&quot;: {
      &quot;src&quot;: &quot;ne_110m_admin_0_countries_lakes.shp&quot;
    }
  }
}</code></pre>

Then execute the following Kartograph command in the console:

<pre><code class="language-bash">kartograph config.json -o world_basic.svg</code></pre>

Kartograph will create _world_basic.svg_ in the current directory. If you open this file in a modern browser, you will see a map of the world.

{{< codepen caption="SVG world map." height="360" theme_id="0" slug_hash="gaOXNv" default_tab="result" user="smashingmag" >}}See the Pen <a href='https://codepen.io/smashingmag/pen/gaOXNv/'>gaOXNv</a> by Smashing Magazine (<a href='https://codepen.io/smashingmag'>@smashingmag</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

## Changing The Map Projection

You may notice that this map looks somewhat different from the map in QGIS. There are a number of different ways to project our three-dimensional Earth into two-dimensional space. By default, **Kartograph uses the Robinson projection**, an aesthetically pleasing projection commonly used for world maps. However, you may prefer to work with the Mercator projection (used by Google Maps) which projects latitude and longitude as straight lines. To do so, add a `proj` object after the `layers` object in the _config.json_ file:

<pre><code class="language-javascript">&quot;proj&quot;: {
  &quot;id&quot;:&quot;mercator&quot;
}</code></pre>

## Reducing The File Size

Often, the SVG file you create may be too large to be practical for web use. Kartograph includes the [Visvalingam-Whyatt simplification algorithm](https://bost.ocks.org/mike/simplify/). This tool makes it possible to dramatically reduce the size of a file with only subtle visual changes to country borders. Our file is already quite small (231KB), but we can simplify it further by adding a `simplify` property to the end of the `countries` property:

<pre><code class="language-javascript">&quot;simplify&quot;: 1</code></pre>

The higher the value of `simplify`, the more country borders will be simplified and the smaller the file will become.</p>

## Filtering Out Features

By default, the map will include all the features present in the shapefile. You may, however, want to exclude certain features from the SVG file. For example, we may wish to remove Antarctica since it is of less relevance to our task. Kartograph includes a filter tool that makes it possible to filter features based on their attributes. We can exclude Antarctica using its ISO code. To do this, add a `filter` property to the `countries` layer:

<pre><code class="language-javascript">&quot;filter&quot;: [&quot;iso_a2&quot;, &quot;not in&quot;, [&quot;AQ&quot;]],</code></pre>

## Saving Data Within The SVG File

Finally, we want our SVG map to include data attributes with each country’s ISO code and name. This will allow us to identify SVG elements in the browser. To do this, add an `attributes` property to the `countries` layer:

<pre><code class="language-javascript">&quot;attributes&quot;: {
  &quot;id&quot;: &quot;iso_a2&quot;, 
  &quot;name&quot;: &quot;name&quot;
},</code></pre>

## Putting It All Together

After making these changes, _config.json_ will consist of the following:

<pre><code class="language-javascript">{
  &quot;layers&quot;: {
    &quot;countries&quot;: { 
      &quot;src&quot;: &quot;ne_110m_admin_0_countries_lakes.shp&quot;,
      &quot;filter&quot;: [&quot;iso_a2&quot;, &quot;not in&quot;, [&quot;AQ&quot;]],
      &quot;attributes&quot;: {
        &quot;id&quot;: &quot;iso_a2&quot;,
        &quot;name&quot;: &quot;name&quot;
      },
      &quot;simplify&quot;: &quot;1&quot;
    }
  },
  &quot;proj&quot;: {
    &quot;id&quot;: &quot;mercator&quot;
  }
}</code></pre>

Execute the same Kartograph command as before (with an updated file name):

<pre><code class="language-bash">kartograph config.json -o world.svg</code></pre>

Kartograph will create a new map _world.svg_ that is smaller and looks quite different:

{{< codepen caption="The new SVG world map." height="440" theme_id="0" slug_hash="LpYOob" default_tab="result" user="smashingmag" >}}See the Pen <a href='https://codepen.io/smashingmag/pen/LpYOob/'>LpYOob</a> by Smashing Magazine (<a href='https://codepen.io/smashingmag'>@smashingmag</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

If you open this file in a text editor, you will see that each `<path>` now includes identifying data in the following form:

<pre><code class="language-markup">data-id=&quot;US&quot; data-name=&quot;United States&quot; id=&quot;US&quot;</code></pre>

This introduction only scratches the surface of what is possible with Kartograph. You can use multiple layers, join features together, and frame the map using latitude and longitude. You can learn about these options and more in the [Kartograph.py documentation](https://kartograph.org/docs/kartograph.py/).</p>

## Adding The SVG Map To A Website

Now that you’ve created an SVG map, you’ll probably want to customize it and add it to your website. Modern browsers support SVG natively so you can add an SVG image to your webpage just like you would add any other image:

<pre><code class="language-markup">&lt;img src=&quot;world.svg&quot; alt=&quot;World Map&quot;&gt;</code></pre>

However, embedding the map this way makes it difficult to style the map and make it interactive. A simple way to apply CSS and JavaScript to the map is to first embed the SVG file inline. Simply open _world.svg_ in a text editor, copy the entire `<svg>` element, and paste it directly into your webpage.

The `<svg>` element contains a separate `<path>` for every country. To style the map, simply apply CSS to all `<path>` elements. Use the `fill` and `stroke` properties to style each country’s color and border respectively. For example, we can make all countries light gray and add a hover effect:

<pre><code class="language-css">
 path {fill: lightgray; stroke: white;}
 path:hover {fill: gray;}
</code></pre>

Similarly, we can use JavaScript to define event handlers. The following snippet will alert each country’s name with a click:

<pre><code class="language-javascript">&lt;script&gt;
 // &lt;![CDATA[
  var countryElements = document.getElementById(&#039;countries&#039;).childNodes;
  var countryCount = countryElements.length;
  for (var i = 0; i &lt; countryCount; i++) {
   countryElements[i].onclick = function() {
    alert(&#039;You clicked on &#039; + this.getAttribute(&#039;data-name&#039;));
   }
  }
 // ]]&gt;
&lt;/script&gt; </code></pre>

This should be placed after the inline `<svg>` element and right before the closing `<body>` tag. Your full HTML file should look like the example [provided in this Gist](https://gist.github.com/youderian/fbff53fe18b13116adf5).

Open this file in a browser, and you should see an interactive map of the world.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f249531-519c-4438-a5bb-c3fed6e821cb/09-interactive-world-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adfaedd1-0918-40e0-abf2-3bed0f73009a/09-interactive-world-opt-small.png" alt="Interactive map" /></a></figure>

Hopefully, this simple example illustrates how you can easily manipulate your SVG map with JavaScript and CSS. For more advanced interactions, such as animating SVG paths, check out an SVG JavaScript library like [Snap.js](https://snapsvg.io/).</p>

## Conclusion

Interactive maps can be intimidating, but they don’t have to be a black box. You can create your own custom SVG maps with open data and software. In no time at all, you will have enhanced your website with a beautiful, fully customizable, interactive map.

{{< signature "ml, ds, og" >}}

