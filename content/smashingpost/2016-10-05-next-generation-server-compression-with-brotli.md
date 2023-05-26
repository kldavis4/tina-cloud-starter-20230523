---
title: Next Generation Server Compression With Brotli
slug: next-generation-server-compression-with-brotli
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0b13a18-e9c8-4cb8-8940-642911c35d49/brotli-opt.jpeg'
date: 2016-10-05T18:58:31.000Z
author: jeremywagner
description: >-
  Chances are pretty good that you’ve worked with, or at least understand the
  concept of, server compression. By compressing website assets on the server
  prior to transferring them to the browser, we’ve been able to achieve
  substantial performance gains.

  For quite some time, the venerable gzip algorithm has been the go-to solution
  for reducing the size of page assets. A new kid on the block has been gaining
  support in modern browsers, and its name is Brotli. In this article, you’ll
  get hands-on with Brotli by writing a Node.js-powered HTTP server that
  implements this new algorithm, and we’ll compare its performance to gzip.
categories:
  - Coding
  - Backend
  - Performance
  - Node.js
  - HTTPS
---
Chances are pretty good that you've worked with, or at least understand the concept of, server compression. By compressing website assets on the server prior to transferring them to the browser, we've been able to achieve substantial performance gains.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00447d0b-18d9-446d-9907-5e4f47d65c68/network-utility-500.png" width="500" height="58" alt="brotli" title="Next Generation Server Compression With Brotli" /></figure>

For quite some time, the venerable gzip algorithm has been the go-to solution for reducing the size of page assets. A new kid on the block has been gaining support in modern browsers, and its name is Brotli. In this article, you'll get hands-on with Brotli by writing a Node.js-powered HTTP server that implements this new algorithm, and we'll compare its performance to gzip.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Improving Smashing Magazine’s Performance: A Case Study](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)
*   [Meet ImageOptim-CLI, A Batch Compression Tool](https://www.smashingmagazine.com/2013/12/imageoptim-cli-batch-compression-tool/)
*   [Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)

{{% feature-panel %}}

## Introducing Brotli

Brotli is a compression algorithm maintained by Google and first released in 2015. Its namesake is a <a href="https://en.wikipedia.org/wiki/Spanisch_Br%C3%B6tli">Swiss pastry product</a>. It was not initially released for use as a standalone algorithm (as gzip was), but rather as an offline compression solution for the <a href="https://en.wikipedia.org/wiki/Web_Open_Font_Format">WOFF2 font format</a>. This means that if you've been using WOFF2 fonts, you've already been using Brotli and you didn't even know it!

Later in 2015, Brotli went beyond providing offline compression of WOFF2 fonts. Brotli is now supported in a large segment of browsers as a new <code>Accept-Encoding</code> scheme that we can use to compress page assets like we've been doing with gzip, but with a reported improvement in compression ratios. This is an enticing prospect for the performance-minded developer.</p>

### Hold Up! What's the Browser Support?

Browser support for Brotli is not universal. The following browsers support Brotli out of the box, without requiring you to turn on support for them under the hood:

*   Chrome since version 50,
*   Android Browser version 50,
*   Chrome for Android since version 50,
*   Firefox since version 44,
*   Firefox for Android since version 46,
*   Opera since version 38.

While this list implies that Edge, Safari and others have left Brotli support out in the cold (for now, at least), caniuse.com indicates that its support is estimated at around 53% at the time of writing. Of course, this statistic will fluctuate over time, so <a href="https://caniuse.com/#search=brotli">see for yourself</a> what the support status is for this technology.

Either way, we're not talking about a small segment of users who would potentially benefit from the increased performance that this new algorithm provides, so it's worth investigating to see what the gains are. Before jumping in with both feet, however, we should talk about the requirement that browsers have for this feature — namely, HTTPS.</p>

### We Meet Again, HTTPS

It's hardly news that browser vendors have been advocating for the transition to a more secure web, and for good reason: HTTPS is no longer the burden it once was in terms of cost and performance. In fact, thanks to modern hardware and the HTTP/2 protocol's multiplexing of requests over a single connection, the overhead of HTTPS connections is <a href="https://istlsfastyet.com/#faq">less than you might think</a>.

In terms of cost, SSL certificates are downright cheap, at as little as $5 a year, depending on the reputation of the signing authority. If that cost is still a barrier for you, you can rely on <a href="https://letsencrypt.org/">Let's Encrypt</a> for free SSL certificates. The barrier to entry for regular folks who need a secure website couldn't be much flimsier than it is today, and that's how it should be.

As an additional motivator, browser vendors have been making SSL a <em>de facto</em> requirement for all sorts of new features, such as <a href="https://jakearchibald.com/2014/using-serviceworker-today/">Service Workers</a>, <a href="https://github.com/http2/http2-spec">HTTP/2</a> and, yes, even Brotli. We can see this requirement in action by visiting any secure website and examining any asset's <code>Accept-Encoding</code> request header for the <code>br</code> token in a Brotli-enabled browser:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad4818ac-5bb3-4962-af5b-82bd9dcbc366/accept-encoding-br.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad4818ac-5bb3-4962-af5b-82bd9dcbc366/accept-encoding-br.png" alt="The br token in the Accept-Encoding request header as seen in Google Chrome" width="500" height="23" /></a><figcaption>The <code>br</code> token in the <code>Accept-Encoding</code> request header, as seen in Google Chrome</figcaption></figure>

If you go to a non-secure website over HTTP and look at the value of the same request header for any asset, you'll see that the <code>br</code> token is absent.

I'm sure by now you've had enough of the hype and are ready to get your hands dirty with Brotli. So, let's get started by writing a small web server in Node.js using the Express framework, and implement Brotli using the <code>shrink-ray</code> package.</p>

## Building A Brotli-Enabled Web Server In Node.js

Adding Brotli to existing web servers such as Nginx or Apache can prove to be inconvenient, depending on your familiarity with them. A Brotli module <a href="https://github.com/google/ngx_brotli">does exist for Nginx</a>, as does <a href="https://github.com/kjdev/apache-mod-brotli">one for Apache</a>, but building and running the Apache module requires some know-how. That's fine if you're cool with that sort of thing, but most of us just want to install something and get right to the tinkering!

So, to make things a little easier on ourselves, I'll be showing you how to set up a small Brotli-capable server written in JavaScript using <a href="https://nodejs.org">Node.js</a> and <a href="https://expressjs.com">Express</a>. Even if you've never used these technologies, don't worry. All you'll need before you begin is to have a copy of Node.js installed; you'll be guided through the entire process. Before you know it, you'll have a Brotli-powered web server up and running on your local machine, ready for your scrutiny.</p>

### Installing the Prerequisites

Because our testing server is in HTTPS, we'll need to have a certificate and key handy. Generating these can be a chore. To make things easier, you can clone the certificates and directory structure we need by using <code>git</code>:

<pre>	<code class="language-bash">
git clone https://github.com/malchata/brotli-server.git
	</code>
</pre>

This will download a GitHub repository with our certificate and key files in the <code>crt</code> directory, and an empty web root directory of <code>htdocs</code>. You can enter into the repository directory by typing <code>cd brotli-server</code>.

(Want to skip ahead? If you're not terribly interested in writing the web server code from scratch and want to get right to messing with Brotli, you can skip ahead by switching to a branch with the completed code by typing <code>git checkout -f brotli-server</code>.)

In order for the server to work, we'll need to install a few packages using <a href="https://npmjs.com">npm</a>:

<pre>	<code class="language-bash">
npm install express https shrink-ray
	</code>
</pre>

This will install three packages:

*   `express` is the Express framework package. This is used to spin up a simple static web server that will serve content from the `htdocs` directory.
*   `https` is the package that enables us to serve files over HTTPS.
*   `shrink-ray` is the compression middleware that contains the Brotli functionality we want to test. It includes gzip functionality as well. _**Note:** If you're doing all of this on Windows, this package relies on node-gyp, which can be problematic for Windows users. You'll have better luck if you have a Linux subsystem, such as the one available on Windows 10\. Chances are that if you're developing for Node on Windows, you're aware of the idiosyncrasies. If not, [read this comment](https://github.com/nodejs/node-gyp/issues/629#issuecomment-225578519) in a Github gist regarding the subject._

Installing these dependencies might take a minute. Once it's finished, you'll be ready to write your web server code!

### Writing the Web Server Code

In your text editor of choice, create a new JavaScript file named <code>https.js</code>, and begin with the following code:

<pre>	<code class="language-javascript">
var express = require("express"), // Imports the express package
	https = require("https"), // Imports the https package
	shrinkRay = require("shrink-ray"), // Imports the compression middleware
	fs = require("fs"), // The file system module for reading files (part of Node.js core)
	path = require("path"), // The path module for working with files and directory paths (also part of Node.js core)
	app = express(), // An Express instance
	pubDir = "./htdocs"; // The web root directory
	</code>
</pre>

In case you're somewhat new to Node.js, the <code>require</code> method imports the modules we need for use in the current script. The <code>pubDir</code> variable is what we'll use to refer to the <code>htdocs</code> directory, which is where we'll serve files from.

Continuing on, we'll need to set up our compression middleware from the <code>shrink-ray</code> package by telling our Express instance in the <code>app</code> object to use it. We'll also instruct our Express instance to statically serve files from the <code>htdocs</code> directory:

<pre>	<code class="language-javascript">
app.use(shrinkRay()); // Tell Express to use the shrink-ray compression middleware
app.use(express.static(path.join(__dirname, pubDir))); // Tell Express to serve static files from the htdocs directory
	</code>
</pre>

We'll top it all off by setting up our HTTPS server and running it on port 8443:

<pre>	<code class="language-javascript">
https.createServer({ // Creates an instance of an HTTPS sever
	key: fs.readFileSync("crt/localhost.key"), // Reads in the key file
	cert: fs.readFileSync("crt/localhost.crt") // Reads in the SSL certificate
}, app).listen(8443); // Passes in our Express instance and instructs the server to run on port 8443
	</code>
</pre>

Now for the moment of truth, when we run our Brotli-powered web server:

<pre>	<code class="language-bash">
node https.js
	</code>
</pre>

If all has gone well, no errors should occur and the server will start. To test it out, point your browser to <a href="https://localhost:8443/readme.txt">https://localhost:8443/readme.txt</a>, and you should see a short message. If you've gotten to this point, you're ready to verify that Brotli is working.</p>

### How Can You Tell That Brotli Is Working?

By default, <code>shrink-ray</code> will compress content with Brotli if the requesting browser supports it and if the server is running on HTTPS. The easiest way to check for support is to grab a copy of a JavaScript library (<a href="https://fb.me/react-15.1.0.min.js">such as React</a>) and save it in the <code>htdocs</code> directory.

From here, open Chrome or Firefox and launch the developer tools. You can do this by pressing <code>F12</code> on a Windows machine or <code>Command + Alt + I</code> on a Mac. Once the tools are open, click on the “Network” tab. The “Network” tab is a common utility available in Chrome and Firefox's developer tools that shows all of the network requests for a given web page. With this tab open, navigate to the asset you saved in the <code>htdocs</code> folder on the local web server. You'll see the network utility populate with the requested resource.

In Chrome, we can see the value of an asset's <code>Content-Encoding</code> header in the network utility's “Content-Encoding” column. If this column is not visible, just right-click on the column headers and choose it from the menu that appears. If Brotli is working, you should see a <code>br</code> token in the “Content-Encoding” column similar to what's shown in the image below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c1ad14e-1940-4350-87ff-7e2cf7154611/network-utility.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00447d0b-18d9-446d-9907-5e4f47d65c68/network-utility-500.png" alt="The br token present in the Content-Encoding request header, as seen in Google Chrome" width="500" height="58" /></a><figcaption>The <code>br</code> token in the <code>Accept-Encoding</code> response header, as seen in Chrome's network utility (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c1ad14e-1940-4350-87ff-7e2cf7154611/network-utility.png">View large version</a>)</figcaption></figure>

Now that we've verified that Brotli is running on our local test web server, let's see how Brotli performs compared to gzip!

## Evaluating Brotli's Performance

Now to the meat of the matter: How well does Brotli perform compared to gzip? If you don't want to do a ton of testing, there's a <a href="https://github.com/crdumoul/brotli-perf-test">performance test</a> that gives a good overview of Brotli's performance. The test is set up to download assets from popular websites specified in a text file, and once the assets are gathered, the test process commences, as specified in the GitHub repository's <code>README</code> document:

1.  Read the file's contents into memory.
2.  Take a timestamp to mark the start of the test.
3.  Compress the file 100 times using Brotli level 1.
4.  Take a timestamp to mark the end of the test.
5.  Record the compressed file size and compression speed (in MB per second).
6.  Repeat steps 2 to 5 for Brotli levels 2 to 11.
7.  Repeat steps 2 to 5 for Gzip level 6.
8.  Output the results in JSON format.

The number of websites specified in the benchmark's text file is huge, and thus the test takes a very long time to complete. In the interest of time, I specified 20 websites that I frequent (including this website) and ran the benchmark over them instead. I felt that this would still provide a good high-level view of Brotli's performance on all compression levels compared to the default gzip setting of <code>6</code>. The average compression speeds of all Brotli settings versus the default gzip setting are shown in the table below:
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Algorithm</th>
<th>Compression level</th>
<th>Speed (MB per second)</th>
</tr>
<tr>
<td>gzip</td>
<td>6</td>
<td>11.8</td>
</tr>
<tr>
<td>Brotli</td>
<td>1</td>
<td>41.5</td>
</tr>
<tr>
<td>Brotli</td>
<td>2</td>
<td>16</td>
</tr>
<tr>
<td>Brotli</td>
<td>3</td>
<td>13.6</td>
</tr>
<tr>
<td>Brotli</td>
<td>4</td>
<td>6.83</td>
</tr>
<tr>
<td>Brotli</td>
<td>5</td>
<td>5.98</td>
</tr>
<tr>
<td>Brotli</td>
<td>6</td>
<td>5.8</td>
</tr>
<tr>
<td>Brotli</td>
<td>7</td>
<td>0.966</td>
</tr>
<tr>
<td>Brotli</td>
<td>8</td>
<td>0.758</td>
</tr>
<tr>
<td>Brotli</td>
<td>9</td>
<td>0.555</td>
</tr>
<tr>
<td>Brotli</td>
<td>10</td>
<td>0.119</td>
</tr>
<tr>
<td>Brotli</td>
<td>11</td>
<td>0.121</td>
</tr>
</tbody>
</table>

As said, this is a very high-level overview. The test collects a lot of data, but average compression speed gives us a basic idea of how Brotli compares to gzip's default compression level. The one flaw of this test is that it doesn't collect data for <em>all</em> gzip settings from <code>1</code> to <code>9</code>. It also can't really quantify how Brotli influences website loading times, because the test measures compression performance on files already on the disk. Despite this, this overview is somewhat indicative of what you'll see in the following tests, in that higher compression settings are going to be the slowest. We just need to see how this influences website loading times and how it compares to all available gzip settings.

To fill in the blanks a bit, I've done some of my own performance testing. First, we'll look at how well <em>all</em> Brotli compression settings compare to <em>all</em> gzip settings for a single asset. Then, we'll do the same for a Node.js-driven website running on a local machine that is bandwidth-throttled using Chrome's network-throttling utility. Then, we'll do the same again, but for an Apache-driven website using the <code>mod_brotli</code> compression module.</p>

### Testing Methods

When testing, I wanted to pick a JavaScript library that is popular and also very large. React fits the bill perfectly, coming in at 144 kilobytes minified. This seems like a reasonable test subject for comparing compression algorithm performance for a single file.

When comparing compression algorithms, we also want to know more than what the final size of a compressed asset is. While this dimension is strongly tied to page-loading time, it's important to note that it's not a consistent relationship in every scenario. Compressing content eats up CPU time, and if an algorithm is too CPU-intensive, there's a chance that any gains made in compression ratios will be nullified if the algorithm takes too long to do its job. Therefore, we want to know two dimensions: the final file size and the amount of time it takes for the compressed asset to load.

However, simply comparing gzip and Brotli out of the box isn't enough. We can adjust the settings for both of these technologies, and when we do so, we influence their performance. gzip allows us to specify a compression level between <code>0</code> and <code>9</code>, with <code>0</code> turning off compression altogether. Brotli can similarly be set between <code>1</code> and <code>11</code>. gzip's default is <code>6</code>, and the default that the <code>shrink-ray</code> package sets for Brotli is <code>4</code>. We can set Brotli's compression level like so:

<pre>	<code class="language-javascript">
app.use(shrinkRay({
	brotli: {
		quality: 11 // Compression level configurable from 1 to 11
	}
}));
	</code>
</pre>

In the table below is a comprehensive collection of final file sizes when compressing the selected JavaScript library on all configurable levels for both Brotli and gzip. Numbers are in kilobytes, and the lowest file sizes are underlined and bolded.
<table class="article-table four-columns"><br>
<tbody>
<tr>
<th>Level</th>
<th>gzip (KB)</th>
<th>Brotli (KB)</th>
</tr>
<tr>
<td>1</td>
<td>50.4</td>
<td><u><strong>48.6</strong></u></td>
</tr>
<tr>
<td>2</td>
<td>48.6</td>
<td><u><strong>44.8</strong></u></td>
</tr>
<tr>
<td>3</td>
<td>47.4</td>
<td><u><strong>44.1</strong></u></td>
</tr>
<tr>
<td>4</td>
<td>44.5</td>
<td><u><strong>42.9</strong></u></td>
</tr>
<tr>
<td>5</td>
<td>43.2</td>
<td><u><strong>40.2</strong></u></td>
</tr>
<tr>
<td>6</td>
<td>42.8</td>
<td><u><strong>39.8</strong></u></td>
</tr>
<tr>
<td>7</td>
<td>42.7</td>
<td><u><strong>39.5</strong></u></td>
</tr>
<tr>
<td>8</td>
<td>42.6</td>
<td><u><strong>39.4</strong></u></td>
</tr>
<tr>
<td>9</td>
<td>42.6</td>
<td><u><strong>39.3</strong></u></td>
</tr>
<tr>
<td>10</td>
<td><em>n/a</em></td>
<td>36.8</td>
</tr>
<tr>
<td>11</td>
<td><em>n/a</em></td>
<td>36.2</td>
</tr>
</tbody>
</table>

At a glance, we can see that the gains are quite impressive. At the highest compression level, Brotli outdoes gzip by 6.4 kilobytes, which is no small amount of data. As stated earlier, though, trade-offs can occur when compression levels are sufficiently high. Let's see how loading times are affected across the various compression levels:
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Level</th>
<th>gzip (milliseconds)</th>
<th>Brotli (milliseconds)</th>
</tr>
<tr>
<td>1</td>
<td>640.6</td>
<td><u><strong>623.8</strong></u></td>
</tr>
<tr>
<td>2</td>
<td>626</td>
<td><u><strong>577.8</strong></u></td>
</tr>
<tr>
<td>3</td>
<td>610.2</td>
<td><u><strong>578.2</strong></u></td>
</tr>
<tr>
<td>4</td>
<td>578</td>
<td><u><strong>563.2</strong></u></td>
</tr>
<tr>
<td>5</td>
<td>568</td>
<td><u><strong>534.8</strong></u></td>
</tr>
<tr>
<td>6</td>
<td>564.6</td>
<td><u><strong>532</strong></u></td>
</tr>
<tr>
<td>7</td>
<td>569.2</td>
<td><u><strong>514.4</strong></u></td>
</tr>
<tr>
<td>8</td>
<td>567.4</td>
<td><u><strong>514</strong></u></td>
</tr>
<tr>
<td>9</td>
<td>563</td>
<td><u><strong>517.2</strong></u></td>
</tr>
<tr>
<td>10</td>
<td><em>n/a</em></td>
<td>558.8</td>
</tr>
<tr>
<td>11</td>
<td><em>n/a</em></td>
<td>704.6</td>
</tr>
</tbody>
</table>

Because the test server runs locally, I ran the test in Chrome using the “Regular 3G” profile in the network-throttling utility, to simulate what loading times would be like over a slow mobile connection. Each figure is the average of five test runs.

In instances where direct comparisons can be made, Brotli seems to perform better in both file-size yield and loading time. Once we hit compression levels <code>10</code> and <code>11</code>, however, we started to see hugely diminishing returns. Even though these compression levels yield much smaller file sizes, the computational overhead erases the gains made in file size.

The <code>shrink-ray</code> package makes up for this overhead in its own way with a caching mechanism. In these tests, that caching mechanism was disabled to get an accurate picture of Brotli's performance with on-the-fly compression. The default behavior of <code>shrink-ray</code> is to first compress the response at the default quality setting. While that happens, the same asset is asynchronously compressed at the highest-quality setting and then cached for subsequent requests.

This caching mechanism yields a loading time of around 480 milliseconds for the React library. Note that this caching feature does not come standard with Brotli, but is rather how <code>shrink-ray</code> is designed to work. Any module that implements Brotli may or may not cache entries for recently compressed assets.</p>

### Performance in a Real Scenario

All of this seems rather clinical, because we're not actually applying this to a real website, but rather to a single file. To get an idea of real-world performance, I took a <a href="https://coyleappliancerepair.com">client's website</a> and ran it through the wringer on my local computer. I tested loading times over the varying quality levels for Brotli with caching disabled, and then with compression caching enabled to see how the <code>shrink-ray</code> package performs when left to its own devices. Below are comparisons of loading times using the same methodology outlined earlier:
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Level</th>
<th>gzip (milliseconds)</th>
<th>Brotli (milliseconds)</th>
</tr>
<tr>
<td>1</td>
<td>871.4</td>
<td><u><strong>869.2</strong></u></td>
</tr>
<tr>
<td>2</td>
<td>869.2</td>
<td><u><strong>848.4</strong></u></td>
</tr>
<tr>
<td>3</td>
<td>868</td>
<td><u><strong>858.4</strong></u></td>
</tr>
<tr>
<td>4</td>
<td><u><strong>845</strong></u></td>
<td>850.2</td>
</tr>
<tr>
<td>5</td>
<td><u><strong>850.8</strong></u></td>
<td>857.8</td>
</tr>
<tr>
<td>6</td>
<td>852.8</td>
<td><u><strong>844.8</strong></u></td>
</tr>
<tr>
<td>7</td>
<td>867.8</td>
<td><u><strong>846.4</strong></u></td>
</tr>
<tr>
<td>8</td>
<td>860.4</td>
<td><u><strong>833.8</strong></u></td>
</tr>
<tr>
<td>9</td>
<td>847.8</td>
<td><u><strong>832.6</strong></u></td>
</tr>
<tr>
<td>10</td>
<td><em>n/a</em></td>
<td>825.2</td>
</tr>
<tr>
<td>11</td>
<td><em>n/a</em></td>
<td>849</td>
</tr>
<tr>
<td>11 (Cached)</td>
<td><em>n/a</em></td>
<td>823.2</td>
</tr>
</tbody>
</table>

In this case, we're able to take a website that would otherwise be 52.4 KB at the highest gzip setting of <code>9</code>, and reduce its payload to 48.4 KB with Brotli's highest setting of <code>11</code>. This is a reduction of about 8%, and after the caching takes effect, we can reduce loading times further. Bear in mind that this example is of a small website. Your mileage may vary. That's not to say that there won't be a benefit for websites with larger payloads, only that you should perform your own analysis before fully implementing Brotli for your website.

Another scenario we can look at is a WordPress blog that runs on an Apache server. <a href="https://legendarytones.com">Legendary Tones</a> is a website that I host for a friend. Although the <a href="https://github.com/kjdev/apache-mod-brotli"><code>mod_brotli</code></a> module for Apache is in its nascent stage, it works well enough that we can test with it. I pulled down the website and ran it on my local Apache server, and I tested all available settings for both <code>mod_deflate</code> and <code>mod_brotli</code>. The conditions for this test are the same as before: Throttle the bandwidth using Chrome's throttling utility at the “Regular 3G” setting, but instead of 5 trials, I performed 20.
<table class="article-table four-columns"><br>
<tbody>
<tr>
<th>Level</th>
<th>gzip (milliseconds)</th>
<th>Brotli (milliseconds)</th>
</tr>
<tr>
<td>1</td>
<td><u><strong>3060</strong></u></td>
<td>3064</td>
</tr>
<tr>
<td>2</td>
<td><u><strong>2968</strong></u></td>
<td>2980</td>
</tr>
<tr>
<td>3</td>
<td>3004</td>
<td><u><strong>2914</strong></u></td>
</tr>
<tr>
<td>4</td>
<td>2900</td>
<td><u><strong>2894</strong></u></td>
</tr>
<tr>
<td>5</td>
<td>2910</td>
<td><u><strong>2772</strong></u></td>
</tr>
<tr>
<td>6</td>
<td>2858</td>
<td><u><strong>2758</strong></u></td>
</tr>
<tr>
<td>7</td>
<td>2836</td>
<td><u><strong>2806</strong></u></td>
</tr>
<tr>
<td>8</td>
<td><u><strong>2854</strong></u></td>
<td>2896</td>
</tr>
<tr>
<td>9</td>
<td>2998</td>
<td><u><strong>2990</strong></u></td>
</tr>
<tr>
<td>10</td>
<td><em>n/a</em></td>
<td>2910</td>
</tr>
<tr>
<td>11</td>
<td><em>n/a</em></td>
<td>2766</td>
</tr>
</tbody>
</table>

In most scenarios where direct comparisons can be made, Brotli seems to outperform gzip, even if only by a little bit. However, let's examine a few caveats for all of the tests we've done:

*   These tests were done on a local web server whose only traffic was me.
*   While Brotli yields significantly lower file sizes at the highest compression levels, the loading times of these assets _usually_ tend to suffer at the `10` and `11` quality settings.
*   If we can cache the compressed response ahead of time, we can negate the long processing time of higher Brotli compression levels. `shrink-ray` does this for us automatically, but other implementations might lack this caching mechanism.

If you're willing to test Brotli for your projects, you'll get a better idea of whether it's a good fit. The good news is that if you set up your web server properly, browsers that don't support Brotli will just fall back to gzip, meaning that everyone will get <em>some</em> benefit, regardless of what algorithms are supported. For example, here's a line from <a href="https://jeremywagner.me">my website</a>'s Apache configuration that implements both <code>mod_brotli</code> and <code>mod_deflate</code>:

<pre>	<code>
AddOutputFilterByType BROTLI;DEFLATE text/html text/css application/javascript text/javascript image/svg+xml text/plain text/xml application/x-javascript
	</code>
</pre>

The key piece of this configuration directive is the <code>BROTLI;DEFLATE</code> portion. When both the <code>mod_brotli</code> and <code>mod_deflate</code> modules are loaded, we can specify what compression algorithm is preferred. By placing <code>BROTLI</code> first in the chain, browsers that support it will receive content compressed by it. In the event that a browser comes along that doesn't support Brotli, it will be served by gzip (<code>DEFLATE</code>) instead.

With our time together coming to an end, let's take a minute to cover a bit of what we've learned about Brotli.</p>

## Conclusion

My findings at this time tell me that you have every good reason to do some research and see what's possible with Brotli on your website. In most situations, it seems that Brotli can squeeze a bit more performance out of your websites, which might be worth pursuing.

While Brotli really starts to get sluggish at higher compression levels, striking a good balance can provide some level of benefit. I can't possibly give any sweeping generalizations as to what compression settings are good for all websites. You'll just need to test on your own. I highly recommend using this approach to see what the results are for you and to see what implementations exist for your server. If you're serving pages with Node.js, Nginx or Apache, you've got options.

Furthermore, it's worth noting that Brotli is a continually evolving project. <a href="https://github.com/google/brotli">Google's GitHub repository</a> of the project shows that contributions are made regularly, and that's reason enough for the performance-minded web developer to keep an eye on this promising new technology.</p>

<em>This article is about a relatively new alternative to gzip compression, named Brotli. This and many other topics are covered in Jeremy's book </em>Web Performance in Action<em>, which you can get from <a href="https://manning.com">Manning Publications</a> for 38% off with the coupon code <code>smashmagpc</code>, as well as any other Manning book!</em>

{{< signature "rb, al, il" >}}

