---
title: 'Measuring Performance With Server Timing'
slug: performance-server-timing
author: drew-mclellan
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09dbcfe-de8a-4278-ae12-3d2296e12751/measuring-performance-drew-mclellan.png
date: 2018-10-30T03:40:14+02:00
summary: >-
  The Server Timing header provides a discrete and convenient way to communicate backend server performance timings to developer tools in the browser. Adding timing information to your application enables you to monitor back-end and front-end performance all in one place.
description: >-
  The Server Timing header provides a discrete and convenient way to communicate backend server performance timings to developer tools in the browser. Adding timing information to your application enables you to monitor back-end and front-end performance all in one place.
categories:
  - Performance
  - API
  - Techniques
---
When undertaking any sort of performance optimisation work, one of the very first things we learn is that before you can improve performance you must first measure it. Without being able to measure the speed at which something is working, we can’t tell if the changes being made are improving the performance, having no effect, or even making things worse.

Many of us will be familiar with working on a performance problem at some level. That might be something as simple as trying to figure out why JavaScript on your page isn’t kicking in soon enough, or why images are taking too long to appear on bad hotel wifi. The answer to these sorts of questions is often found in a very familiar place: your browser’s developer tools.

Over the years developer tools have been improved to help us troubleshoot these sorts of performance issues in the front end of our applications. Browsers now even have performance audits built right in. This can help track down front end issues, but these audits can show up another source of slowness that we can’t fix in the browser. That issue is slow server response times.

## “Time to First Byte”

There’s very little browser optimisations can do to improve a page that is simply slow to build on the server. That cost is incurred between the browser making the request for the file and receiving the response. Studying your network waterfall chart in developer tools will show this delay up under the category of “Waiting (TTFB)”. This is how long the browser waits between making the request and receiving the response. 

{{% feature-panel %}}

In performance terms this is know as _Time to First Byte_ - the amount of time it takes before the server starts sending something the browser can begin to work with. Encompassed in that wait time is everything the server needs to do to build the page. For a typical site, that might involve routing the request to the correct part of the application, authenticating the request, making multiple calls to backend systems such as databases and so on. It could involve running content through templating systems, making API calls out to third party services, and maybe even things like sending emails or resizing images. Any work that the server does to complete a request is squashed into that TTFB wait that the user experiences in their browser.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f2858fd-3989-424c-92bc-de1dab06d33f/st1.png"><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f2858fd-3989-424c-92bc-de1dab06d33f/st1.png" width="600" height="" alt="The Network panel in Chrome DevTools showing the inspection of a single page request" /></a>
<figcaption>Inspecting a document request shows the time the browser spends waiting for the response from the server.</figcaption>
</figure>

So how do we reduce that time and start delivering the page more quickly to the user? Well, that’s a big question, and the answer depends on your application. That is the work of performance optimisation itself. What we need to do first is _measure_ the performance so that the benefit of any changes can be judged.

## The Server Timing Header

The job of [Server Timing](https://www.w3.org/TR/server-timing/) is not to help you actually time activity on your server. You’ll need to do the timing yourself using whatever toolset your backend platform makes available to you. Rather, the purpose of Server Timing is to specify how those measurements can be communicated to the browser. 

The way this is done is very simple, transparent to the user, and has minimal impact on your page weight. The information is sent as a simple set of HTTP response headers.

<pre><code class="language-javascript">Server-Timing: db;dur=123, tmpl;dur=56</code></pre>

This example communicates two different timing points named `db` and `tmpl`. These aren’t part of the spec - these are names that we’ve picked, in this case to represent some database and template timings respectively.

{{% ad-panel-leaderboard %}}

The `dur` property is stating the number of milliseconds the operation took to complete. If we look at the request in the Network section of Developer Tools, we can see that the timings have been added to the chart.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80063fdb-245f-4a8a-9212-700f17642840/st2.png"><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80063fdb-245f-4a8a-9212-700f17642840/st2.png" width="600" height="" alt="The Timings panel of a page request in Chrome DevTools showing a new Server Timing section." /></a>
<figcaption>A new Server Timing section appears, showing the timings set with the Server-Timing HTTP header.</figcaption>
</figure>

The `Server-Timing` header can take multiple metrics separated by commas:

<pre><code class="language-javascript">Server-Timing: metric, metric, metric</code></pre>

Each metric can specify three possible properties

1. A short **name** for the metric (such as `db` in our example)
2. A **duration** in milliseconds (expressed as `dur=123`)
3. A **description** (expressed as `desc="My Description"`)

Each property is separated with a semicolon as the delimiter. We could add descriptions to our example like so:

<div class="break-out">

<pre><code class="language-javascript">Server-Timing: db;dur=123;desc="Database", tmpl;dur=56;desc="Template processing"</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64e68903-dba3-44c1-a7ef-baa5fcc056ff/st3.png"><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64e68903-dba3-44c1-a7ef-baa5fcc056ff/st3.png" width="600" height="" alt="The Timings panel of a page request in Chrome DevTools showing descriptions used for Server Timing metrics." /></a>
<figcaption>The names are replaced with descriptions when provided.</figcaption>
</figure>

The only property that is required is `name`. Both `dur` and `desc` are optional, and can be used optionally where required. For example, if you needed to debug a timing problem that was happening on one server or data center and not another, it might be useful to add that information into the response without an associated timing.

<div class="break-out">

<pre><code class="language-javascript">Server-Timing: datacenter;desc="East coast data center", db;dur=123;desc="Database", tmpl;dur=56;desc="Template processing”</code></pre></div>

This would then show up along with the timings.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3e2f558-55b3-44d6-b575-1340cb2165ff/st4.png"><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3e2f558-55b3-44d6-b575-1340cb2165ff/st4.png" width="600" height="" alt="The Timings panel of a page request in Chrome DevTools showing a Server Timing with no time set." /></a>
<figcaption>The "East coast data center" value is shown, even though it has no timings.</figcaption>
</figure>

One thing you might notice is that the timing bars don’t show up in a waterfall pattern. This is simply because Server Timing doesn’t attempt to communicate the _sequence_ of timings, just the raw metrics themselves.

## Implementing Server Timing

The exact implementation within your own application is going to depend on your specific circumstance, but the principles are the same. The steps are always going to be:

1. Time some operations
2. Collect together the timing results
3. Output the HTTP header

In pseudocode, the generation of response might look like this:

<div class="break-out">

<pre><code class="language-javascript">startTimer('db')
getInfoFromDatabase()  
stopTimer('db')

startTimer('geo')
geolocatePostalAddressWithAPI('10 Downing Street, London, UK')
endTimer('geo')

outputHeader('Server-Timing', getTimerOutput())</code></pre></div>

The basics of implementing something along those lines should be straightforward in any language. A very simple PHP implementation could use the `microtime()` function for timing operations, and might look something along the lines of the following.

<div class="break-out">

<pre><code class="language-php">class Timers
{
	private $timers = [];

	public function startTimer($name, $description = null)
	{
		$this->timers[$name] = [
			'start' => microtime(true),
			'desc' => $description,
		];
	}

	public function endTimer($name)
	{
		$this->timers[$name]['end'] = microtime(true);
	}

	public function getTimers()
	{
		$metrics = [];

		if (count($this->timers)) {
			foreach($this->timers as $name => $timer) {
				$timeTaken = ($timer['end'] - $timer['start']) * 1000;
				$output = sprintf('%s;dur=%f', $name, $timeTaken);

				if ($timer['desc'] != null) {
					$output .= sprintf(';desc="%s"', addslashes($timer['desc']));
				} 
				$metrics[] = $output;
			}
		}

		return implode($metrics, ', ');
	}
}</code></pre></div>

A test script would use it as below, here using the `usleep()` function to artificially create a delay in the running of the script to simulate a process that takes time to complete.

<pre><code class="language-php">$Timers = new Timers();

$Timers->startTimer('db');
usleep('200000');
$Timers->endTimer('db');

$Timers->startTimer('tpl', 'Templating');
usleep('300000');
$Timers->endTimer('tpl');

$Timers->startTimer('geo', 'Geocoding');
usleep('400000');
$Timers->endTimer('geo');

header('Server-Timing: '.$Timers->getTimers());</code></pre>

Running this code generated a header that looked like this:

<div class="break-out">

<pre><code class="language-javascript">Server-Timing: db;dur=201.098919, tpl;dur=301.271915;desc="Templating", geo;dur=404.520988;desc="Geocoding"</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6b9d3a1-c662-45fc-8026-9cbfdaf91a2e/st5.png"><img data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6b9d3a1-c662-45fc-8026-9cbfdaf91a2e/st5.png" width="600" height="" alt="The Timings panel of a page request in Chrome DevTools showing the test values correctly displayed." /></a>
<figcaption>The Server Timings set in the example show up in the Timings panel with the delays configured in our test script.</figcaption>
</figure>

## Existing Implementations

Considering how handy Server Timing is, there are relatively few implementations that I could find. The [server-timing](https://www.npmjs.com/package/server-timing) NPM package offers a convenient way to use Server Timing from Node projects. 

If you use a middleware based PHP framework [tuupola/server-timing-middleware](https://github.com/tuupola/server-timing-middleware) provides a handy option too. I've been using that in production on [Notist](https://noti.st/) for a few months, and I always leave a few basic timings enabled if you'd like to see an example in the wild.

For browser support, the best I've seen is in Chrome DevTools, and that's what I've used for the screenshots in this article.

## Considerations

Server Timing itself adds very minimal overhead to the HTTP response sent back over the wire. The header is very minimal and is generally safe to be sending without worrying about targeting to only internal users. Even so, it’s worth keeping names and descriptions short so that you’re not adding unnecessary overhead.

More of a concern is the extra work you might be doing on the server to time your page or application. Adding extra timing and logging can itself have an impact on performance, so it’s worth implementing a way to turn this on and off when required.

Using a Server Timing header is a great way to make sure all timing information from both the front-end and the back-end of your application are accessible in one location. Provided your application isn't too complex, it can be easy to implement and you can be up and running within a very short amount of time. 

If you'd like to read more about Server Timing, you might try the following:

- The [W3C Server Timing Specification](https://www.w3.org/TR/server-timing/)
- The [MDN page on Server Timing](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Server-Timing) has examples and up to date detail of browser support
- An [interesting write-up](https://iplayer.engineering/server-timing-in-the-wild-bfb34816322e) from the BBC iPlayer team about their use of Server Timing.

{{< signature "ra" >}}
