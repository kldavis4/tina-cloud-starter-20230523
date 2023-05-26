---
title: 'How To Create An Animated HTML Graph With CSS And jQuery'
slug: create-an-animated-bar-graph-with-html-css-and-jquery
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3ba235-30e2-435c-9487-5c2122a00a65/bar-graph-front-page.jpg
date: 2011-09-23T10:22:57.000Z
author: derek-mack
summary: >-
  There are actually quite a few ways to display graphs on the Web. There are pros and cons to the wide range of resources available to us, but this tutorial will not explore them all. Instead, we’ll create our graph using a progressively enhanced sprinkling of CSS3 and jQuery. 
description: >-
  There are pros and cons to the wide range of resources available to us, but this tutorial will not explore them all. Instead, we’ll create our graph using a progressively enhanced sprinkling of CSS3 and jQuery.
categories:
  - Coding
  - CSS
  - jQuery
  - Data Visualization
  - Animation
---

People in boardrooms across the world love a good graph. They go nuts for PowerPoint, bullet points and phrases like “run it up the flagpole,” “blue-sky thinking” and “low-hanging fruit,” and everything is always “moving forward.” Backwards is not an option for people who <a href="https://startupista.com/corporate-bullshit-generator/">facilitate paradigm shifts in the zeitgeist</a>. Graphs of financial projections, quarterly sales figures and market saturation are a middle-manager’s dream.

<figure><img loading="lazy" decoding="async" class="106433 size-full" title="Creating an Animated Bar Graph with HTML, CSS &amp; jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3a8dd25-425f-4c1d-9fd0-41a3cb23cc2b/graph-tut-image-header.jpg" alt="html graph" width="500" height="260" /></figure>

How can we as Web designers get in on all of this hot graph action? There are actually quite a few ways to display graphs on the Web. We could simply create an image and nail it to a Web page. But that’s not very accessible or interesting. We could use Flash, which is quite good for displaying graphs &mdash; but again, not very accessible. Besides, designers, developers and <a href="https://www.apple.com/hotnews/thoughts-on-flash/">deities</a> are falling out of love with Flash.

Technologies such as HTML5 can do many of the same things without the need for a plug-in. The new HTML5 <code>&lt;canvas&gt;</code> element could even be adapted to the task. Plenty of charting tools are online that we might use. But what if we wanted something a little more tailored?

There are pros and cons to the wide range of resources available to us, but this tutorial will not explore them all. Instead, we’ll create our graph using a <a href="https://www.smashingmagazine.com/2009/04/22/progressive-enhancement-what-it-is-and-how-to-use-it/">progressively enhanced</a> sprinkling of CSS3 and jQuery. Because we can.

{{% feature-panel %}}

## What Are We Making?

We’re making <a href="https://smashingmagazine.com/provide/graph_tut_files/ex_03.html">this</a>. And more! Here are some possibilities on how you can extend the techniques explored in this tutorial:

*   A progress bar that indicates how long until the end of all humanity in the event of a zombie plague;
*   A graph indicating the decline in safe outdoor activities during a zombie plague;
*   A frighteningly similar graph indicating the decline in manners during a zombie plague;
*   The increase of people who were unaware of the zombie plague because they were sharing with all of their now-deceased friends on Facebook what they did on [FarmVille](https://www.farmville.com/).

Or you could create a graph or quota bar that simply illustrates something useful and less full of dread and zombies. So, let’s get on with it.

### What You’ll Need

*   A text or HTML editor. [Take your pick](https://en.wikipedia.org/wiki/Comparison_of_HTML_editors); many are out there.
*   [jQuery](https://jquery.com/). Practice safe scripting and get the latest one. Keep the jQuery website open so that you can look up the documentation as you go.
*   Possibly an image editor, such as [Paint](https://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/mspaint_overview.mspx?mfr=true), to mock up what your graph might look like.
*   A modern and decent Web browser to preview changes.

That should do it. Please note that this tutorial is not designed as an introduction to either HTML, CSS, jQuery or zombies. Some intermediate knowledge of these three technologies and the undead is assumed.

## The Mark-Up

You can create the underlying HTML for a graph in a number of ways. In this tutorial, we’ll start with a <code>table</code>, because it will make the most sense visually if JavaScript or CSS is not applied. That’s a big checkmark in the column for accessibility.

Quick! You’ve just been given some alarming figures. The population of tanned zombies is projected to spiral out of control in the next few years. The carbon tigers and blue monkeys are under immediate threat. Then the tanned zombies will probably come for us. But you’re just a designer. What could you possibly do to help?

I know! You could make a Web page that illustrates our imminent demise with nice, calming, smoothly animated graphics!

To begin, let’s put this data into a table, with columns for each year, and rows for the different species.

<div class="break-out">

<pre><code class="language-markup tmp-html">&lt;!doctype html&gt;
&lt;html lang="en"&gt;
   &lt;head&gt;
      &lt;meta charset="utf-8"&gt;
      &lt;meta name="viewport" content="width=1024"&gt;
      &lt;title&gt;Example 01: No CSS&lt;/title&gt;
   &lt;/head&gt;

   &lt;body&gt;
      &lt;div id="wrapper"&gt;
         &lt;div class="chart"&gt;
            &lt;h3&gt;Population of endangered species from 2012 to 2016&lt;/h3&gt;
            &lt;table id="data-table" border="1" cellpadding="10" cellspacing="0"
            summary="The effects of the zombie outbreak on the populations
            of endangered species from 2012 to 2016"&gt;
               &lt;caption&gt;Population in thousands&lt;/caption&gt;
               &lt;thead&gt;
                  &lt;tr&gt;
                     &lt;td&gt;&amp;nbsp;&lt;/td&gt;
                     &lt;th scope="col"&gt;2012&lt;/th&gt;
                     &lt;th scope="col"&gt;2013&lt;/th&gt;
                     &lt;th scope="col"&gt;2014&lt;/th&gt;
                     &lt;th scope="col"&gt;2015&lt;/th&gt;
                     &lt;th scope="col"&gt;2016&lt;/th&gt;
                  &lt;/tr&gt;
               &lt;/thead&gt;
               &lt;tbody&gt;
                  &lt;tr&gt;
                     &lt;th scope="row"&gt;Carbon Tiger&lt;/th&gt;
                     &lt;td&gt;4080&lt;/td&gt;
                     &lt;td&gt;6080&lt;/td&gt;
                     &lt;td&gt;6240&lt;/td&gt;
                     &lt;td&gt;3520&lt;/td&gt;
                     &lt;td&gt;2240&lt;/td&gt;
                  &lt;/tr&gt;
                  &lt;tr&gt;
                     &lt;th scope="row"&gt;Blue Monkey&lt;/th&gt;
                     &lt;td&gt;5680&lt;/td&gt;
                     &lt;td&gt;6880&lt;/td&gt;
                     &lt;td&gt;6240&lt;/td&gt;
                     &lt;td&gt;5120&lt;/td&gt;
                     &lt;td&gt;2640&lt;/td&gt;
                  &lt;/tr&gt;
                  &lt;tr&gt;
                     &lt;th scope="row"&gt;Tanned Zombie&lt;/th&gt;
                     &lt;td&gt;1040&lt;/td&gt;
                     &lt;td&gt;1760&lt;/td&gt;
                     &lt;td&gt;2880&lt;/td&gt;
                     &lt;td&gt;4720&lt;/td&gt;
                     &lt;td&gt;7520&lt;/td&gt;
                  &lt;/tr&gt;
               &lt;/tbody&gt;
            &lt;/table&gt;
         &lt;/div&gt;
      &lt;/div&gt;
   &lt;/body&gt;
&lt;/html&gt;</code></pre></div>

View the example below to see how it looks naked, with no CSS or JavaScript applied. The accessibility of this table will enable people using screen readers to understand the data and the underlying message, which is “Run for your life! The zombies are coming!”

<figure><a href="https://smashingmagazine.com/provide/graph_tut_files/ex_01.html"><img loading="lazy" decoding="async" class="106437" title="Example 1: Mark-up only (no CSS or JavaScript)" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b52cf37-46a7-4f68-8de0-5f70bad50438/graph-tut-image-01.jpg" alt="screenshot" width="500" height="260" /></a></figure>

The easy part is now out of the way. Now, let’s tap into the power of CSS and JavasScript (via jQuery) to really illustrate what the numbers are telling us. Technically, our aim is to create a graph that works in all modern browsers, from IE 8 on.

Did I say all modern browsers? IE 8 is lucky: it gets to hang out with the cool kids. Browsers that support CSS3 will get a few extra sprinkles.

## “By Your Powers Combined…”

If you wish to summon <a href="https://en.wikipedia.org/wiki/Captain_Planet">Captain Planet</a>, you <a title="Earth!" href="https://en.wikipedia.org/wiki/Planeteer#Kwame">may</a> <a title="Fire!" href="https://en.wikipedia.org/wiki/Planeteer#Wheeler">have</a> <a title="Wind!" href="https://en.wikipedia.org/wiki/Planeteer#Linka">to</a> <a title="Water!" href="https://en.wikipedia.org/wiki/Planeteer#Gi">look</a> <a title="Heart!" href="https://en.wikipedia.org/wiki/Planeteer#Ma-Ti">elsewhere</a>. If you want to learn how to combine CSS and jQuery to create a graph that illustrates our impending doom at the hands of a growing army of zombies who prefer bronzer over brains, then read on.

The first thing to do is style our table with some basic CSS. This is a nice safety net for people who haven’t enabled JavaScript in their browser.

<figure><a href="https://smashingmagazine.com/provide/graph_tut_files/ex_02.html"><img loading="lazy" decoding="async" class="106438" title="Example 2: Markup with CSS (no JavaScript)" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a23dc7-3c5c-48f8-9053-bf565a88b495/graph-tut-image-02.jpg" alt="screenshot" width="500" height="260" /></a></figure>

## Getting Started In jQuery

We’ll use jQuery to create our graph on the fly, separate from the original data table. To do this, we need to get the data out of the table and store it in a more usable format. Then, we can add to our document new elements that use this data in order to construct our graph.

Let’s get started by creating our main <code>createGraph()</code> function. I’ve abbreviated some of the inner workings of this function so that you get a clearer picture of the structure. Don’t forget: you can always refer to the source code that comes with this tutorial.

Here’s our basic structure:

<div class="break-out">

<pre><code class="language-javascript">// Wait for the DOM to load everything, just to be safe
$(document).ready(function() {

   // Create our graph from the data table and specify a container to put the graph in
   createGraph('#data-table', '.chart');

   // Here be graphs
   function createGraph(data, container) {
      // Declare some common variables and container elements
      …

      // Create the table data object
      var tableData = {
         …
      }

      // Useful variables to access table data
      …

      // Construct the graph
      …

      // Set the individual heights of bars
      function displayGraph(bars) {
         …
      }

      // Reset the graph's settings and prepare for display
      function resetGraph() {
         …
         displayGraph(bars);
      }

      // Helper functions
      …

      // Finally, display the graph via reset function
      resetGraph();
   }
});</code></pre></div>

We pass two parameters to this function:

1.  The `data`, in the form of a `table` element;
2.  A `container` element, where we’d like to place our graph in the document.

Next up, we’ll declare some variables to manage our data and container elements, plus some timer variables for animation. Here’s the code:

<div class="break-out">

<pre><code class="language-javascript">// Declare some common variables and container elements
var bars = [];
var figureContainer = $('&lt;div id="figure"&gt;&lt;/div&gt;');
var graphContainer = $('&lt;div class="graph"&gt;&lt;/div&gt;');
var barContainer = $('&lt;div class="bars"&gt;&lt;/div&gt;');
var data = $(data);
var container = $(container);
var chartData;
var chartYMax;
var columnGroups;

// Timer variables
var barTimer;
var graphTimer;</code></pre></div>

Nothing too exciting here, but these will be very useful later.

## Getting The Data

Besides simply displaying the data, a good bar chart should have a nice big title, clearly labelled axes and a color-coded legend. We’ll need to strip the data out of the table and format it in a way that is more meaningful in a graph. To do that, we’ll create a JavaScript object that stores our data in handy little functions. Let’s give birth to our <code>tableData{}</code> object:

<div class="break-out">

<pre><code class="language-javascript">// Create table data object
var tableData = {
   // Get numerical data from table cells
   chartData: function() {
      …
   },
   // Get heading data from table caption
   chartHeading: function() {
      …
   },
   // Get legend data from table body
   chartLegend: function() {
      …
   },
   // Get highest value for y-axis scale
   chartYMax: function() {
      …
   },
   // Get y-axis data from table cells
   yLegend: function() {
      …
   },
   // Get x-axis data from table header
   xLegend: function() {
      …
   },
   // Sort data into groups based on number of columns
   columnGroups: function() {
      …
   }
}</code></pre></div>

We have several functions here, and they are explained in the code’s comments. Most of them are quite similar, so we don’t need to go through each one. Instead, let’s pick apart one of them, <code>columnGroups</code>:

<div class="break-out">

<pre><code class="language-javascript">// Sort data into groups based on number of columns
columnGroups: function() {
   var columnGroups = [];
   // Get number of columns from first row of table body
   var columns = data.find('tbody tr:eq(0) td').length;
   for (var i = 0; i &lt; columns; i++) {
      columnGroups[i] = [];
      data.find('tbody tr').each(function() {
         columnGroups[i].push($(this).find('td').eq(i).text());
      });
   }
   return columnGroups;
}</code></pre></div>

Here’s how it breaks down:

*   Create the `columnGroups[]` array to store the data;
*   Get the number of columns by counting the table cells (`td`) in the first row;
*   For each column, find the number of rows in the table body (`tbody`), and create another array to store the table cell data;
*   Then loop through each row and grab the data from each table cell (via the jQuery `text()` function), and then add it to the table cell data array.

Once our object is full of juicy data, we can start creating the elements that make up our graph.

## Using The Data

Using the jQuery <code>$.each</code> function, we can now loop through our data at any point and create the elements that make up our graph. One of the trickier bits involves inserting the bars that represent each species inside the yearly columns.

Here’s the code:

<div class="break-out">

<pre><code class="language-javascript">// Loop through column groups, adding bars as we go
$.each(columnGroups, function(i) {
   // Create bar group container
   var barGroup = $('&lt;div class="bar-group"&gt;&lt;/div&gt;');
   // Add bars inside each column
   for (var j = 0, k = columnGroups[i].length; j &lt; k; j++) {
      // Create bar object to store properties (label, height, code, etc.) and add it to array
      // Set the height later in displayGraph() to allow for left-to-right sequential display
      var barObj = {};
      barObj.label = this[j];
      barObj.height = Math.floor(barObj.label / chartYMax * 100) + '%';
      barObj.bar = $('&lt;div class="bar fig' + j + '"&gt;&lt;span&gt;' + barObj.label + '&lt;/span&gt;&lt;/div&gt;')
         .appendTo(barGroup);
      bars.push(barObj);
   }
   // Add bar groups to graph
   barGroup.appendTo(barContainer);
});</code></pre></div>

Excluding the headings, our table has five columns with three rows. For our graph, this means that for each column we create, three bars will appear in that column. The following image shows how our graph will be constructed:

<figure><img loading="lazy" decoding="async" class="106444" title="graph-tut-image-construction" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bacd9bf-6b0e-4516-a6ba-5daf7b691920/graph-tut-image-construction.png" alt="screenshot" width="500" height="390" /></figure>

Breaking it down:

*   For each column, create a container `div`;
*   Loop inside each column to get the row and cell data;
*   Create a bar object (`barObj{}`) to store the properties for each bar, such as its label, height and mark-up;
*   Add the mark-up property to the column, applying a CSS class of `'.fig' + j` to color code each bar in the column, wrapping the label in a `span`;
*   Add the object to our `bars[]` array so that we can access the data later;
*   Piece it all together by adding the columns to a container element.

Bonus points if you noticed that we didn’t set the height of the bars. This is so that we have more control later on over how the bars are displayed.

Now that we have our bars, let’s work on labelling our graph. Because the code to display the labels is quite similar, talking you through all of it won’t be necessary. Here’s how we display the y-axis:

<div class="break-out">

<pre><code class="language-javascript">// Add y-axis to graph
var yLegend   = tableData.yLegend();
var yAxisList   = $('&lt;ul class="y-axis"&gt;&lt;/ul&gt;');
$.each(yLegend, function(i) {
   var listItem = $('&lt;li&gt;&lt;span&gt;' + this + '&lt;/span&gt;&lt;/li&gt;')
      .appendTo(yAxisList);
});
yAxisList.appendTo(graphContainer);</code></pre></div>

This breaks down as follows:

*   Get the relevant table data for our labels,
*   Create an unordered list (`ul`) to contain our list items;
*   Loop through the label data, and create a list item (`li`) for each label, wrapping each label in a `span`;
*   Attach the list item to our list;
*   Finally, attach the list to a container element.

By repeating this technique, we can add the legend, x-axis labels and headings for our graph.

Before we can display our graph, we need to make sure that everything we’ve done is added to our container element.

<div class="break-out">

<pre><code class="language-javascript">// Add bars to graph
barContainer.appendTo(graphContainer);

// Add graph to graph container
graphContainer.appendTo(figureContainer);

// Add graph container to main container
figureContainer.appendTo(container);</code></pre></div>

{{% ad-panel-leaderboard %}}

## Displaying The Data

All that’s left to do in jQuery is set the height of each bar. This is where our earlier work, storing the height property in a bar object, will come in handy.

We’re going to animate our graph sequentially, one by one, uno por uno.

One possible solution is to use a callback function to animate the next bar when the last animation is complete. However, the graph would take too long to animate. Instead, our graph will use a timer function to display each bar after a certain amount of time, regardless of how long each bar takes to grow. Rad!

Here’s the <code>displayGraph()</code> function:

<div class="break-out">

<pre><code class="language-javascript">// Set the individual height of bars
function displayGraph(bars, i) {
   // Changed the way we loop because of issues with $.each not resetting properly
   if (i &lt; bars.length) {
      // Animate the height using the jQuery animate() function
      $(bars[i].bar).animate({
         height: bars[i].height
      }, 800);
      // Wait the specified time, then run the displayGraph() function again for the next bar
      barTimer = setTimeout(function() {
         i++;
         displayGraph(bars, i);
      }, 100);
   }
}</code></pre></div>

What’s that you say? “Why aren’t you using the <code>$.each</code> function like you have everywhere else?” Good question. First, let’s discuss what the <code>displayGraph()</code> function does, then why it is the way it is.

The <code>displayGraph()</code> function accepts two parameters:

1.  The `bars` to loop through,
2.  An index (`i`) from which to start iterating (starting at `0`).

Let’s break down the rest:

*   If the value of `i` is less than the number of bars, then keep going;
*   Get the current bar from the array using the value of `i`;
*   Animate the height property (calculated as a percentage and stored in `bars[i].height`);
*   Wait 100 milliseconds;
*   Increment `i` by 1 and repeat the process for the next bar.

“So, why wouldn’t you just use the <code>$.each</code> function with a <code>delay()</code> before the animation?"

You could, and it would work just fine… the first time. But if you tried to reset the animation via the “Reset graph” button, then the timing events wouldn’t clear properly and the bars would animate out of sequence.

I would like to be proven wrong, and if there is a better way to do this, feel free to sound off in the comments section.

Moving on, here’s <code>resetGraph()</code>:

<div class="break-out">

<pre><code class="language-javascript">// Reset graph settings and prepare for display
function resetGraph() {
   // Stop all animations and set the bar's height to 0
   $.each(bars, function(i) {
      $(bars[i].bar).stop().css('height', 0);
   });

   // Clear timers
   clearTimeout(barTimer);
   clearTimeout(graphTimer);

   // Restart timer
   graphTimer = setTimeout(function() {
      displayGraph(bars, 0);
   }, 200);
}</code></pre></div>

Let’s break <code>resetGraph()</code> down:

*   Stop all animations, and set the height of each bar back to 0;
*   Clear out the timers so that there are no stray animations;
*   Wait 200 milliseconds;
*   Call `displayGraph()` to animate the first bar (at index `0`).

Finally, call <code>resetGraph()</code> at the bottom of <code>createGraph()</code>, and watch the magic happen as we bask in the glory of our hard work.

Not so fast, sunshine! Before we go any further, we need to put some clothes on.

## The CSS

The first thing we need to do is hide the original data table. We could do this in a number of ways, but because our CSS will load well before the JavaScript, let’s do this in the easiest way possible:

<div class="break-out">

<pre><code class="language-css">#data-table {
   display: none;
}</code></pre></div>

Done. Let’s create a nice container area to put our graph in. Because a few unordered lists are being used to make our graph, we’ll also reset the styles for those. Giving the <code>#figure</code> and <code>.graph</code> elements a <code>position: relative</code> is important because it will anchor the place elements exactly where we want in those containers.

<div class="break-out">

<pre><code class="language-css">/* Containers */

#wrapper {
   height: 420px;
   left: 50%;
   margin: -210px 0 0 -270px;
   position: absolute;
   top: 50%;
   width: 540px;
}

#figure {
   height: 380px;
   position: relative;
}

#figure ul {
   list-style: none;
   margin: 0;
   padding: 0;
}

.graph {
   height: 283px;
   position: relative;
}</code></pre></div>

Now for the legend. We position the legend right down to the bottom of its container (<code>#figure</code>) and line up the items horizontally:

<div class="break-out">

<pre><code class="language-css">/* Legend */

.legend {
   background: #f0f0f0;
   border-radius: 4px;
   bottom: 0;
   position: absolute;
   text-align: left;
   width: 100%;
}

.legend li {
   display: block;
   float: left;
   height: 20px;
   margin: 0;
   padding: 10px 30px;
   width: 120px;
}

.legend span.icon {
   background-position: 50% 0;
   border-radius: 2px;
   display: block;
   float: left;
   height: 16px;
   margin: 2px 10px 0 0;
   width: 16px;
}</code></pre></div>

The x-axis is very similar to the legend. We line up the elements horizontally and anchor them to the bottom of its container (<code>.graph</code>):

<div class="break-out">

<pre><code class="language-css">/* x-axis */

.x-axis {
   bottom: 0;
   color: #555;
   position: absolute;
   text-align: center;
   width: 100%;
}

.x-axis li {
   float: left;
   margin: 0 15px;
   padding: 5px 0;
   width: 76px;
}</code></pre></div>

The y-axis is a little more involved and requires a couple of tricks. We give it a <code>position: absolute</code> to break it out of the normal flow of content, but anchored to its container. We stretch out each <code>li</code> to the full width of the graph and add a border across the top. This will give us some nice horizontal lines in the background.

Using the power of negative margins, we can offset the numerical labels inside the <code>span</code> so that they shift up and to the left. Lovely!

<div class="break-out">

<pre><code class="language-css">/* y-axis */

.y-axis {
   color: #555;
   position: absolute;
   text-align: right;
   width: 100%;
}

.y-axis li {
   border-top: 1px solid #ccc;
   display: block;
   height: 62px;
   width: 100%;
}

.y-axis li span {
   display: block;
   margin: -10px 0 0 -60px;
   padding: 0 10px;
   width: 40px;
}</code></pre></div>

Now for the meat in our endangered species sandwich: the bars themselves. Let’s start with the container element for the bars and the columns:

<div class="break-out">

<pre><code class="language-css">/* Graph bars */

.bars {
   height: 253px;
   position: absolute;
   width: 100%;
   z-index: 10;
}

.bar-group {
   float: left;
   height: 100%;
   margin: 0 15px;
   position: relative;
   width: 76px;
}</code></pre></div>

Nothing too complicated here. We’re simply setting some dimensions for the container, and setting a <code>z-index</code> to make sure it appears in front of the y-axis markings.

Now for each individual <code>.bar</code>:

<div class="break-out">

<pre><code class="language-css">.bar {
   border-radius: 3px 3px 0 0;
   bottom: 0;
   cursor: pointer;
   height: 0;
   position: absolute;
   text-align: center;
   width: 24px;
}

.bar.fig0 {
   left: 0;
}

.bar.fig1 {
   left: 26px;
}

.bar.fig2 {
   left: 52px;
}
</code></pre></div>

The main styles to note here are:

*   `position: absolute` and `bottom: 0`, which means that the bars will be attached to the bottom of our graph and grow up;
*   the bar for each species (`.fig0`, `.fig1` and `.fig2`), which will be positioned within `.bar-group`.

Now, why don’t we minimize the number of sharp edges on any given page by using the <code>border-radius</code> property to round the edges of the top-left and top-right corners of each bar? OK, so <code>border-radius</code> isn’t really necessary, but it adds a nice touch for browsers that support it. Thankfully, the latest versions of the most popular browsers do support it.

Because we’ve placed the values from each table cell in each bar, we can add a neat little pop-up that appears when you hover over a bar:

<div class="break-out">

<pre><code class="language-css">.bar span {
   #fefefe url(../images/info-bg.gif) 0 100% repeat-x;
   border-radius: 3px;
   left: -8px;
   display: none;
   margin: 0;
   position: relative;
   text-shadow: rgba(255, 255, 255, 0.8) 0 1px 0;
   width: 40px;
   z-index: 20;

   -webkit-box-shadow: rgba(0, 0, 0, 0.6) 0 1px 4px;
   box-shadow: rgba(0, 0, 0, 0.6) 0 1px 4px;
}

.bar:hover span {
   display: block;
   margin-top: -25px;
}</code></pre></div>

First, the pop-up is hidden from view via <code>display: none</code>. Then, when a <code>.bar</code> element is hovered over, we’ve set <code>display: block</code> to bring it into view, and set a negative <code>margin-top</code> to make it appear above each bar.

The <code>text-shadow</code>, <code>rgba</code> and <code>box-shadow</code> properties are currently supported by most modern browsers as is. Of these modern browsers, only Safari requires a vendor prefix (<code>-webkit-</code>) to make <code>box-shadow</code> work. Note that these properties are simply enhancements to our graph and aren’t required to understand it. Our baseline of Internet Explorer 8 simply ignores them.

Our final step in bringing everything together is to color code each bar:

<div class="break-out">

<pre><code class="language-css">.fig0 {
   background: #747474 url(../images/bar-01-bg.gif) 0 0 repeat-y;
}

.fig1 {
   background: #65c2e8 url(../images/bar-02-bg.gif) 0 0 repeat-y;
}

.fig2 {
   background: #eea151 url(../images/bar-03-bg.gif) 0 0 repeat-y;
}</code></pre></div>

In this example, I’ve simply added a <code>background-color</code> and a <code>background-image</code> that tiles vertically. This will update the styles for the bars and the little icons that represent them in the legend. Nice.

And, believe it or not, that is it!

## The Finished Product

<figure><a href="https://smashingmagazine.com/provide/graph_tut_files/ex_03.html"><img loading="lazy" decoding="async" class="106432" title="Example 3: Animated Bar Chart with jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/052348b3-ef50-4466-825f-4ba889e2bbf9/graph-tut-image-03.jpg" alt="screenshot" width="500" height="260" /></a></figure>

That about wraps it up. I hope we’ve done enough to alert the public to the dangers of zombie over-population. More than that, however, I hope you’ve gained something useful from this tutorial and that you’ll continue to push the boundaries of what can be done in the browser &mdash; especially with proper Web standards and without the use of third-party plug-ins. If you’ve got ideas on how to extend or improve anything you’ve seen here, don’t hesitate to leave a comment below, or find me on Twitter <a href="https://twitter.com/derek_mack">@derek_mack</a>.

## Bonus: Unleashing The Power Of CSS3

This bonus is not as detailed as our main example. It serves mainly as a showcase of some features being considered in the CSS3 specification.

Because support for CSS3 properties is currently limited, so is their use. Although some of the features mentioned here are making their way into other Web browsers, Webkit-based ones such as Apple Safari and Google Chrome are leading the way.

We can actually create our graph using no images at all, and even animate the bars using CSS instead of jQuery.

Let’s start by removing the background images from our bars, replacing them with the <code>-webkit-gradient</code> property:

<div class="break-out">

<pre><code class="language-css">.fig0 {
   background: -webkit-gradient(linear, left top, right top, color-stop(0.0, #747474), color-stop(0.49, #676767), color-stop(0.5, #505050), color-stop(1.0, #414141));
}

.fig1 {
   background: -webkit-gradient(linear, left top, right top, color-stop(0.0, #65c2e8), color-stop(0.49, #55b3e1), color-stop(0.5, #3ba6dc), color-stop(1.0, #2794d4));
}

.fig2 {
   background: -webkit-gradient(linear, left top, right top, color-stop(0.0, #eea151), color-stop(0.49, #ea8f44), color-stop(0.5, #e67e28), color-stop(1.0, #e06818));
}</code></pre></div>

We can do the same with our little number pop-ups:

<div class="break-out">

<pre><code class="language-css">.bar span {
   background: -webkit-gradient(linear, left top, left bottom, color-stop(0.0, #fff), color-stop(1.0, #e5e5e5));
   …
}</code></pre></div>

For more information on Webkit gradients, check out the <a href="https://webkit.org/blog/175/introducing-css-gradients/">Surfin’ Safari</a> blog.

Continuing with the pop-ups, let’s introduce <code>-webkit-transition</code>. CSS transitions are remarkably easy to use and understand. When the browser detects a change in an element’s property (height, width, color, opacity, etc.), it will transition to the new property.

Again, refer to <a href="https://webkit.org/blog/138/css-animation/">Surfin’ Safari</a> for more information on <code>-webkit-transition</code> and CSS3 animation.

Here’s an example:

<div class="break-out">

<pre><code class="language-css">.bar span {
   background: -webkit-gradient(linear, left top, left bottom, color-stop(0.0, #fff), color-stop(1.0, #e5e5e5));
   display: block;
   opacity: 0;

   -webkit-transition: all 0.2s ease-out;
}

.bar:hover span {
   opacity: 1;
}</code></pre></div>

When you hover over the bar, the margin and opacity of the pop-up will change. This triggers a transition event according to the properties we have set. Very cool.

Thanks to <code>-webkit-transition</code>, we can simplify our JavaScript functions a bit:

<div class="break-out">

<pre><code class="language-javascript">// Set individual height of bars
function displayGraph(bars, i) {
   // Changed the way we loop because of issues with $.each not resetting properly
   if (i &lt; bars.length) {
      // Add transition properties and set height via CSS
      $(bars[i].bar).css({'height': bars[i].height, '-webkit-transition': 'all 0.8s ease-out'});
      // Wait the specified time, then run the displayGraph() function again for the next bar
      barTimer = setTimeout(function() {
         i++;
         displayGraph(bars, i);
      }, 100);
   }
}
// Reset graph settings and prepare for display
function resetGraph() {
   // Set bar height to 0 and clear all transitions
   $.each(bars, function(i) {
      <strong>$(bars[i].bar).stop().css({'height': 0, '-webkit-transition': 'none'});</strong>
   });

   // Clear timers
   clearTimeout(barTimer);
   clearTimeout(graphTimer);

   // Restart timer
   graphTimer = setTimeout(function() {
      displayGraph(bars, 0);
   }, 200);
}</code></pre></div>

Here are the main things we’ve changed:

*   Set the height of the bars via the jQuery `css()` function, and allowed CSS transitions to take care of the animation;
*   When resetting the graph, turned transitions off so that the height of the bars is instantly set to 0.

<a href="https://smashingmagazine.com/provide/graph_tut_files/ex_04.html">Check out the example</a> if you have the latest version of Safari or Chrome installed.

### Ultra-Mega Webkit Bonus: Now In 3-D!

For a sneak peek of what the future holds, <a href="https://smashingmagazine.com/provide/graph_tut_files/ex_05.html">check out a little experiment</a> that I put together, with a 3-D effect and CSS transforms. Again, it requires the latest versions of Safari or Chrome:

As in our previous Webkit example, there are **no images**, and **all animation is handled via CSS**. Kiss my face!

I can’t tell you what to do with all this information. But I do caution you about the potential misuse of your new powers. In the words of our friend Captain Planet, “The power is yours!”

Use it wisely.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Chartist.js, An Open-Source Library For Responsive Charts](https://www.smashingmagazine.com/2014/12/chartist-js-open-source-library-responsive-charts/)
*   [Functional Animation In UX Design](https://www.smashingmagazine.com/2015/05/functional-ux-design-animations/)
*   [Upgrading CSS Animation With Motion Curves](https://www.smashingmagazine.com/2016/08/css-animations-motion-curves/)
*   [Creating Graphs With Adobe Illustrator](https://www.smashingmagazine.com/2010/09/creating-graphs-with-adobe-illustrator/)

{{< signature "al, kw, il, mrn" >}}
