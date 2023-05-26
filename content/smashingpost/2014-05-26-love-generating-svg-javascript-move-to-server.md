---
title: Love Generating SVG With JavaScript? Move It To The Server!
slug: love-generating-svg-javascript-move-to-server
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6c39b0b-33d3-41ca-a5f9-29a540e4ba42/love-generating-svg-with-javascript.png
date: 2014-05-26T21:52:52.000Z
author: ilya
description: >-
  I hope that by now, in 2014, there is no need to explain why SVG is a blessing
  to developers who want to ensure that their graphics look sharp on all
  devices, especially with their huge diversity of resolutions.
categories:
  - Coding
  - Tools
  - Techniques
  - SVG
---

But just like any other technology, SVG has its limitations. And in this article, we’ll talk about how to bypass some of them.

## What’s The Problem?

Why would you even need to generate SVG on the server? The technology is entirely client-side, so what would motivate anyone to move it from there?

{{% feature-panel %}}

Before answering these questions, <strong>let’s look at the state of the industry</strong>. When we talk about “generating SVG” nowadays, we mean “generating SVG with JavaScript.” The current state of browser support and libraries makes the creation of complex visuals (even with animations and user interaction) a trivial task: Just pick the library that suits your need.

And there are a lot to choose from, from general-purpose ones such as Raphaël.js, <a href="https://snapsvg.io/">Snap.svg</a> and <a href="https://www.svgjs.com/">svg.js</a> to the myriad of smaller ones, as well as, if you do plotting and data visualization, gRaphaël, <a href="https://www.highcharts.com/">Highcharts</a> and <a href="https://d3js.org/">D3</a>.

So the right question is, how do we continue generating SVG with JavaScript while also putting the results of the generation on the server? The question is a bit long, but here are the reasons why we should answer it:

*   **To enable the user to download a graphic**.  If we don’t want to scare the user with this “unknown” format, then we should convert the SVG to a PNG or PDF.
*   **To enable a graphic to inserted in an email**.  We all love charts in our emails, and we prefer Retina-ready ones.
*   **To enable a graphic to be displayed on another website**.  Think API.
*   **To improve performance**.  Complex visualization logic can easily hang the browser for multiple seconds. By generating the SVG on the server, we can cache the result and then deliver the cached SVG when the next user wants it.</p>

## Solutions

### Simply Recreate All Logic on the Server

This solution is possible, just not practical. The majority of mature back-end languages have libraries for generating SVG. But we are developers. We do not want to recreate the same logic twice, because that would lead to bugs, integration problems and a burdensome need for support.</p>

### Straightforward Solution

The easiest way to put the generated SVG on the server is just to send the generated data with an AJAX request when it’s complete.

Below is a simple example with Raphaël.js and jQuery. Let’s start with simple HTML as a boilerplate:

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
   &lt;head&gt;
      &lt;meta charset="utf-8"&gt;
      &lt;script src="https://code.jquery.com/jquery-2.1.0.min.js"&gt;&lt;/script&gt;
      &lt;script src="https://cdnjs.cloudflare.com/ajax/libs/raphael/2.1.2/raphael-min.js"&gt;&lt;/script&gt;
   &lt;/head&gt;
   &lt;body&gt;
      &lt;div id="svg"&gt;&lt;/div&gt;
   &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Now, add our drawing code to it:

<pre><code class="language-javascript">
$(function() {
   var svgContainer = document.getElementById("svg");
   var paper = Raphael(svgContainer, 640, 480);

   paper
      .rect(0, 0, 640, 480, 10)
      .attr({
         fill: '#fff',
         stroke: 'none'
      });

   var circle = paper
                .circle(320, 240, 60)
                .attr({
                   fill: '#223fa3', 
                   stroke: '#000',
                   'stroke-width': 80,
                   'stroke-opacity': 0.5
                });
   paper
      .rect(circle.attr('cx') - 10, circle.attr('cy') - 10, 20, 20)
      .attr({
         fill: '#fff',
         stroke: 'none'
      });

   $.post(
      '/svg_catcher',
      { content: svgContainer.innerHTML }
  );
});
</code></pre>

*   [View this code on Github](https://github.com/somebody32/generate-svg-on-the-server-with-js/tree/master/straightforward)

On the server, we just cache the result and store or process it any way we’d like. Here is the resulting image, in case you’re curious:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef72f397-a24d-49d6-97e2-67309475d675/result.svg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef72f397-a24d-49d6-97e2-67309475d675/result.svg" alt="" /></a><br>
<em>In case your browser does not support this image, here's a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b3d9f1f-8574-4012-ba3a-d5db5ee3639a/result.png">PNG version</a>.</em>

This technique is absolutely suitable not only for Raphaël, but for any SVG-generating library. I just picked Raphaël because it is a popular, battle-tested solution, with an API that is easy to understand. It drastically simplifies the creation and manipulation of images via JavaScript, and also supports VML for old browsers that don’t support SVG.

This approach is easy and straightforward, but it has a lot of downsides, too:

*   You will have to inline all external resources (mainly images) after uploading them; otherwise, all of the converters will show a white placeholder instead of the original source.
*   If the SVG is big and the user’s network is not reliable, then the resulting file might end up invalid. We could verify validity server-side, but that wouldn’t help with the next point.
*   Malicious input is a problem. Replacing a beautiful colorful business chart with the (SVG) image of a kitten is easy. Technically, it would be valid, but you can see why it would be harmful.

You could certainly take this approach if you trust your users (if it’s an intranet application, for example). Otherwise, the security risk might be too great.</p>

### PhantomJS

To eliminate the user’s input from the equation (or to minimize it as much as possible), we should move our generation script to the server.

A lot of complex code is running in the browser. The easiest way to run it on the server is to move the browser to the server. Thanks to <a href="https://phantomjs.org/">PhantomJS</a>, that is totally doable.

PhantomJS is a WebKit implementation that can be controlled with JavaScript. Roughly speaking, it is an actual — yet headless — browser, meaning that Web pages are never rendered.

Start by installing PhantomJS on your system, which is easy by following the <a href="https://phantomjs.org/download.html">official documentation</a>. Then, we’ll change our script a bit to make it work with PhantomJS: First, create <code>index.html</code> with the boilerplate code for our generator:

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
   &lt;head&gt;
      &lt;script src="https://cdnjs.cloudflare.com/ajax/libs/raphael/2.1.2/raphael-min.js"&gt;&lt;/script&gt;
      &lt;meta charset="utf-8"&gt;
   &lt;/head&gt;
   &lt;body&gt;
      &lt;div id="svg"&gt;&lt;/div&gt;
   &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Then, create <code>generator.js</code>, which will drive PhantomJS:

<pre><code class="language-javascript">
var fs = require('fs');
var page = require('webpage').create();
var url = 'file://' + fs.absolute('./index.html');

var svgDrawer = function() {
   var svgContainer = document.getElementById("svg");
   var paper = Raphael(svgContainer, 640, 480);
   paper
      .rect(0, 0, 640, 480, 10)
      .attr({
         fill: '#fff',
         stroke: 'none'
    });
   var circle = paper
                .circle(320, 240, 60)
                .attr({
                   fill: '#223fa3',
                   stroke: '#000',
                   'stroke-width': 80,
                   'stroke-opacity': 0.5
                });
   paper
      .rect(circle.attr('cx') - 10, circle.attr('cy') - 10, 20, 20)
      .attr({
         fill: '#fff',
         stroke: 'none'
    });

   return svgContainer.innerHTML;
};

page.open(url, function (status) {
   console.log(page.evaluate(svgDrawer));
   phantom.exit();
});
</code></pre>

*   [View this code on Github](https://github.com/somebody32/generate-svg-on-the-server-with-js/tree/master/phantomjs)

Now it is ready to generate SVG for us:

<pre><code class="language-none">
phantomjs generator.js &gt; result.svg
</code></pre>

So, we have a generator that fully works on our server, without our having written a lot of code.

Can we make it better? Yes!

Running <code>time phantomjs generator.js &gt; result.svg</code> took about 0.2 seconds on my machine.

<pre><code class="language-none">
0.14s user 0.03s system 74% cpu 0.232 total
</code></pre>

The most resource-consuming task was, of course, the “browser warming.” We have to do it on every request, which is somewhat inefficient. We can prevent this by turning our PhantomJS script from a “single-run” solution to a real server that listens to data and responds with SVG.

Let’s do that. We do not want to generate the same SVG every time, so we will also add dynamic support for our visualization. Our final workflow will look like this:

1.  Start the server, which will listen on the special port for our requests.
2.  Pass it the request with our data payload for visualization.
3.  Receive the response with SVG based on our data.

To run a server, we will use the built-in <a href="https://github.com/ariya/phantomjs/wiki/API-Reference-WebServer">module</a>:

<pre><code class="language-none">
var port, server, page, url, fs = require('fs');

port = 9494;
server = require('webserver').create();

page = require('webpage').create();
url = 'file://' + fs.absolute('./index.html');
</code></pre>

Then, we’ll change our drawer to support dynamic data:

<pre><code class="language-javascript">
var svgDrawer = function(data) {
   var svgContainer = document.getElementById("svg");
   var paper = Raphael(svgContainer, 640, 480);
   paper
      .rect(data.x, data.y, 640, 480, 10)
      .attr({
         fill: '#fff',
         stroke: 'none'
      });
   var circle = paper
                .circle(data.x/2, data.y/2, 60)
                .attr({
                   fill: '#223fa3',
                   stroke: '#000',
                   'stroke-width': 80,
                   'stroke-opacity': 0.5
                });
   paper
      .rect(circle.attr('cx') - 10, circle.attr('cy') - 10, 20, 20)
      .attr({
         fill: '#fff',
         stroke: 'none'
      });

   return svgContainer.innerHTML;
}
</code></pre>

Just some minor changes, as you can see. We’re passing the <code>data</code> parameter and taking the <code>x</code> and <code>y</code> properties from it to define our <code>rect</code> and <code>circle</code>.

Now, let’s prepare the function that will run on every request to the server. It will parse the request’s payload, evaluate our drawing code in the context of the page and return the result to us.

<pre><code class="language-javascript">
var service = server.listen(port, function (request, response) {
   var drawerPayload = JSON.parse(request.post).data;
   page.open(url, function (status) {
      var svg = page.evaluate(svgDrawer, drawerPayload);

      response.statusCode = 200;
      response.write(svg);
      response.close();
   });
});
</code></pre>

The last part is to check that everything has gone smoothly and to notify the user that we are ready to go:

<pre><code class="language-markup">
if (service) {
   console.log('Web server running on port ' + port);
} else {
   console.log('Error: Could not create web server listening on port ' + port);
   phantom.exit();
}
</code></pre>

*   [View this code on Github](https://github.com/somebody32/generate-svg-on-the-server-with-js/tree/master/phantomjs-server)

Now we are ready to test our server! Run <code>phantom server.js</code> and create the test payload file, <code>payload.json</code>:

<pre><code class="language-markup">
{
   "data": {
      "x": 700,
      "y": 490
   }
}

</code></pre>

And we’ll use cURL to request our server:

<pre><code class="language-none">
curl -X POST -d @payload.json -H "Content-Type: application/json" localhost:9494
</code></pre>

You should have received your custom SVG as a response. And the speed should have been drastically better:

<pre><code class="language-none">
0.00s user 0.00s system 30% cpu 0.026 total
</code></pre>

All in all, evaluating code with PhantomJS is the most functional way to generate SVG on the server.

Highcharts, a popular charting library, has its own scripts that you can use to easily generate images for emailed reports and other purposes.</p>

### JSDOM

A curious mind might ask, “But why do we need to move an actual browser to the server? Can’t we just use Node.js to run our JavaScript drawer in the back end?”

We could. The main obstacle, though, is not only how to require a browser-specific library in Node.js, but how to make it run without the DOM implementation.

Raphael, Snap.svg and other solutions use the DOM API extensively to create an SVG document, append nodes to it and manipulate it in different ways. Node.js lacks this kind of API.

<a href="https://github.com/tmpvar/jsdom">JSDOM</a>, then, is exactly what we are looking for: a JavaScript implementation of the DOM that can be used with Node.js.

Let’s convert our drawer to use it and see if any problems occur:

<pre><code class="language-javascript">
var jsdom = require('jsdom').jsdom;
var fs = require('fs');

var boilerplate = fs.readFileSync('index.html');

var doc = jsdom(boilerplate);
doc.implementation.addFeature(
  'https://www.w3.org/TR/SVG11/feature#BasicStructure', '1.1'
)
</code></pre>

Here, we have called JSDOM with our boilerplate HTML (identical to the previous examples) and added SVG 1.1 to the list of supported features.

Now, let’s add our drawing code to the <code>window.onload</code> callback:

<pre><code class="language-javascript">
var window = doc.parentWindow;

window.onload = function() {
   window.Raphael.prototype.renderfix = function(){};
   var svgContainer = window.document.getElementById('svg');
   var paper = window.Raphael(svgContainer, 640, 480);
   paper
      .rect(0, 0, 640, 480, 10)
      .attr({
         fill: '#fff',
         stroke: 'none'
      });
   var circle = paper
                .circle(320, 240, 60)
                .attr({
                  fill: '#223fa3',
                  stroke: '#000',
                  'stroke-width': 80,
                  'stroke-opacity': 0.5
                });
   paper
      .rect(circle.attr('cx') - 10, circle.attr('cy') - 10, 20, 20)
      .attr({
         fill: '#fff',
         stroke: 'none'
      });
   console.log(svgContainer.innerHTML);
};
</code></pre>

*   [View this code on Github](https://github.com/somebody32/generate-svg-on-the-server-with-js/tree/master/jsdom)

The drawing code remains untouched, except that we’ve prefixed all calls to the window-scoped variables with <code>window</code> and added one magic line:

<pre><code class="language-javascript">
window.Raphael.prototype.renderfix = function(){};
</code></pre>

This is a hack because JSDOM does not support certain SVG APIs, so be aware of that. In our example, if we remove this line, we will get this:

<pre><code class="language-none">
TypeError: Object [ SVG ] has no method 'createSVGMatrix'
</code></pre>

Here, we’ve overridden Raphael’s <code>renderfix</code> function, which uses <code>createSVGMatrix</code>, with an empty one. The solution is totally not production-ready, but it’s OK for our experiment.

Now we can run this example with <code>node index.js</code>. And what about speed?

<pre><code class="language-none">
0.49s user 0.06s system 89% cpu 0.612 total
</code></pre>

So, using JSDOM is possible, but way more unstable and slower then PhantomJS for our purpose. But be aware of this approach, and treat it as an interesting experiment.</p>

### Svable

The final touch: Svable. Its conversion API frees us from having to set up of any of the tools mentioned just above. Just send your SVG and you’ll get a PDF or PNG back:

<pre><code class="language-markup">
curl -X POST -d @payload.json \
      -H "Content-Type: application/json" \  
      -H "Authorization: Bearer your-svable-token" \
      https://svable.com/api/convert &gt; result.pdf
</code></pre>

And here is the <code>payload.json</code>:

<pre><code class="language-markup">
{
   "content": "&lt;svg&gt;…",
   "format": "pdf"
}
</code></pre>

For more details on the API, please consult the documentation on Svable’s website.

The second (and more interesting) part of this service is the functionality to generate SVGs. You can generate images without PhantomJS or any DOM emulation and without changing the drawing code.

Svable provides the API and special adapters for the most popular SVG-generation libraries. So, for our Raphaël example:

<pre><code class="language-javascript">
var Svable = require('svable');
var paper = Svable(0, 0, 640, 480, 'raphael');
paper
   .rect(0, 0, 640, 480, 10)
   .attr({
   fill: '#fff',
   stroke: 'none'
   });
var circle = paper
   .circle(320, 240, 60)
   .attr({
      fill: '#223fa3',
      stroke: '#000',
      'stroke-width': 80,
      'stroke-opacity': 0.5
   });
paper
   .rect(circle.attr('cx') - 10, circle.attr('cy') - 10, 20, 20)
   .attr({
      fill: '#fff',
      stroke: 'none'
   });

console.log(paper.burnSync());
</code></pre>

This will return our SVG, and <code>paper.burnSync({ format:"pdf" })</code> will return the converted PDF file.

This functionality is in the private beta now, so stay tuned to it.</p>

## Conclusion

It’s fair to say that, when it comes to generating SVG with JavaScript, we can no longer say, “It only works in the browser.”

A number of techniques will enable you to generate SVG on the server with the same code that you use in the browser, and resources and infrastructure are available for every type of visualization.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Math Behind JavaScript Animations](https://www.smashingmagazine.com/2011/10/quick-look-math-animations-javascript/)
*   [The Illusion Of Life: An SVG Animation Case Study](https://www.smashingmagazine.com/2016/07/an-svg-animation-case-study/)
*   [Generating SVG With React](https://www.smashingmagazine.com/2015/12/generating-svg-with-react/)
*   [A Few Different Ways To Use SVG Sprites In Animation](https://www.smashingmagazine.com/2015/03/different-ways-to-use-svg-sprites-in-animation/)

Start with the easiest one that satisfies your basic business needs, and then tune it to your ideal once you understand the drawbacks and bottlenecks.

Happy SVG’ing!

{{< signature "al, il" >}}

