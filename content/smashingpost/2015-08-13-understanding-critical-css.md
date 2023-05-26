---
title: Understanding Critical CSS
slug: understanding-critical-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e502def-874f-44ab-8a99-e65043018baa/02-browser-opt-small.jpg
date: 2015-08-13T18:39:59.000Z
author: dean-hume
description: >-
  Delivering a fast, smooth web experience is an important part of building
  websites today. Most of the time, we develop websites without understanding
  what the browser is actually doing under the hood. How exactly does the
  browser render our web pages from the HTML, CSS and JavaScript that we create?
  How can we use this knowledge to **speed up the rendering of our web pages**?
categories:
  - Coding
  - CSS
  - Optimization
  - Performance
---
<p><em>The web is slow, yet there are a few simple strategies to make websites faster. One of them is <strong>inlining critical CSS into the <code>&lt;head&gt;</code> of your pages</strong>, yet how exactly do you do it if your site contains hundreds of pages, or even worse, hundreds of different templates? You can't do it manually. Dean Hume explains an easy way to get it done. If you're a seasoned web developer, you might find the article obvious and self-explanatory, but it's a good piece to show to your clients and junior developers for sure. — Ed.</em></p>

Delivering a fast, smooth web experience is an important part of building websites today. Most of the time, we develop websites without understanding what the browser is actually doing under the hood. How exactly does the browser render our web pages from the HTML, CSS and JavaScript that we create? How can we use this knowledge to <strong>speed up the rendering of our web pages</strong>?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Improving Smashing Magazine’s Performance: A Case Study](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)
*   <span data-sheets-value="{&quot;1&quot;:2,&quot;2&quot;:&quot;An Introduction To PostCSS&quot;}">[An Introduction To PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)</span>
*   [Preload: What Is It Good For?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Front-End Performance Checklist](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)

If I’m looking to quickly improve the performance of a website, Google's <a href="https://developers.google.com/speed/pagespeed/insights/">PageSpeed Insights</a> tool is the first place I go. It can be very helpful when trying to profile a web page and find areas for improvement. You simply enter the URL of the page that you want to test, and the tool provides you with a list of performance suggestions.

{{% feature-panel %}}

If you’ve ever run one of your own websites through the PageSpeed Insights tool, you may have come across the following suggestion.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f853e4-81a6-42ff-8cf9-17cdd9bb6a81/01-blocking-css-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac61bd7-b93b-4ea4-925d-64c9c9d3b003/01-blocking-css-opt-small.jpg" alt="Critical CSS - Google PageSpeed Insights" width="500" height="144" /></a><figcaption>CSS and JavaScript will block the rendering of your page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f853e4-81a6-42ff-8cf9-17cdd9bb6a81/01-blocking-css-opt.jpg">View large version</a>)</figcaption></figure>

I must admit, the first time I saw this, I was a little confused. The suggestion reads:
<blockquote>“None of the above-the-fold content on your page could be rendered without waiting for the following resources to load. Try to <strong>defer or asynchronously load blocking resources</strong>, or inline the critical portions of those resources directly in the HTML.”</blockquote>

Fortunately, the solution to this problem is simpler than it seems! The answer lies in the way that the CSS and JavaScript are loaded in your web page.</p>

## What Is Critical CSS?

A request for a CSS file can significantly increase the time it takes a web page to render. The reason is that by default the browser will delay page rendering until it has finished loading, parsing and executing all the CSS files referenced in the <code>&lt;head&gt;</code> of your page. It does this because it needs to calculate the layout of the page.

Unfortunately, this means that if we have a really large CSS file and it takes a while to download, our users will end up waiting until the <em>whole file</em> has been downloaded before the browser can begin rendering the page. Fortunately, there is a sneaky technique that allows us to optimize the delivery of our CSS and mitigate the blocking. This technique is known as optimizing the <a href="https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path?hl=en">critical rendering path.</a>

The critical rendering path represents the steps that the browser takes to render a page. We want to find the <strong>minimum set of blocking CSS</strong>, or the <em>critical CSS</em>, that we need to make the page appear to the user. A <em>critical resource</em> is any resource that may block the initial rendering of the page. The idea behind this is that the website should get the first screen's worth of content (or "above-the-fold" content) to the user in the first few TCP packets of response. To give you a brief idea of how this would work for a web page, take a look at the image below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79f81b05-cb5e-40f3-ab1a-c07f650533b9/02-browser-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e502def-874f-44ab-8a99-e65043018baa/02-browser-opt-small.jpg" alt="Understanding what is critical" /></a><figcaption>Critical CSS is the minimum set of blocking CSS required to render the first screen's worth of content to the user. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79f81b05-cb5e-40f3-ab1a-c07f650533b9/02-browser-opt.jpg">View large version</a>)</figcaption></figure>

In the example above, the critical part of the web page is only <strong>what the user can see when they first load the page</strong>. This means that we only need to load the minimum amount of CSS required to render the top portion of the page across all breakpoints. For the remainder of the CSS, we don’t need to worry as we can load it asynchronously.

How do we determine what is considered critical CSS? Determining the critical CSS for a page is rather complex and requires you to walk through the web page's DOM. Next, we need to determine the list of styles that currently apply to each element in view. Doing this manually would be a tedious process, but there are a number of great tools that will do this automatically.

In this article I am going to show you how to improve your web page rendering speed using critical CSS, and show you a tool that will help you do this <strong>automatically</strong>.</p>

## Critical CSS In Action

To start working with the critical CSS for our web page, we need to change our approach to the way we handle the CSS – this means splitting it into two files. For the first file, we extract only the minimum set of CSS required to render the above-the-fold content, and then we inline it in the web page. For the second file, or the non-critical CSS, we asynchronously load it so as not to block the web page.

It might seem a bit weird at first, but by inlining the critical CSS into our HTML, we can eliminate the additional round-trips in the critical path. This allows us to deliver the critical CSS in one round-trip and present something to users as soon as possible.

In order to understand what this might look like represented as HTML, the code below gives a basic example.</p>

<pre><code class="language-markup">&lt;!doctype html&gt;
&lt;head&gt;
  &lt;style&gt; /* inlined critical CSS */ &lt;/style&gt;
  &lt;script&gt; loadCSS('non-critical.css'); &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  ...body goes here
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

In the code above, we are extracting the critical CSS and inlining it in the HTML between the <code>style</code> tags. Next, we are using the <code>loadCSS();</code> function to asynchronously load the remaining, non-critical CSS. This is important because we are essentially off-loading the bulkier (<em>non-critical</em>) CSS and injecting it into the web page in the background.

At first, this may seem like a nightmare to maintain. Why would you manually want to inline a snippet of CSS in every page? There is good news, though – the process can be automated and in this example, I am going to run through a tool called <a href="https://github.com/addyosmani/critical">Critical</a>. Originally created by <a href="https://addyosmani.com/blog/">Addy Osmani</a>, it is a Node.js package that allows you to automatically extract and inline critical-path CSS in HTML pages.

We are going to combine this with <a href="https://gruntjs.com/">Grunt</a>, the JavaScript task runner, to automatically process the CSS. If you have never used Grunt before, the website has some very <a href="https://gruntjs.com/getting-started">detailed documentation</a>, as well as a variety of tips for configuring your project. I have also <a href="https://deanhume.com/Home/BlogPost/automatically-removing-unused-css-using-grunt/6101">previously blogged</a> about this awesome tool.</p>

### Getting Started

Let's begin by firing up the Node.js console and navigating to the path of your website. Install the Grunt command line interface by typing the following command into your console:

<pre><code class="language-bash">npm install -g grunt-cli</code></pre>

This will put the <code>grunt</code> command in your system path, allowing it to be run from any directory. Next, install the Grunt task runner with the following command:

<pre><code class="language-bash">npm install grunt --save-dev</code></pre>

Then install the <a href="https://github.com/bezoerb/grunt-critical">grunt-critical</a> plugin.</p>

<pre><code class="language-bash">npm install grunt-critical --save-dev</code></pre>

Next, you need to create a Gruntfile that contains the task configuration for your project. Mine looks a little like the code below.</p>

<pre><code class="language-javascript">module.exports = function (grunt) {

grunt.initConfig({
  critical: {
    dist: {
      options: {
        base: './'
      },
      // The source file
      src: 'page.html',
      // The destination file
      dest: 'result.html'
      }
    }
  });

  // Load the plugins
  grunt.loadNpmTasks('grunt-critical');

  // Default tasks.
  grunt.registerTask('default', ['critical']);
};</code></pre>

In the code above, I configured the <strong>Critical</strong> plugin to look at my <i>page.html</i> file. It will then process the CSS against the given page and calculate the critical CSS. Next, it will inline the critical CSS and update the HTML page accordingly.

Run the plugin by typing <code>grunt</code> into the console.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d4c17e2-6672-42b7-8b43-d21760444d9c/03-critical-css-grunt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e72badb3-8d74-4b08-8f51-6acff27e079f/03-critical-css-grunt-small.gif" alt="Running Grunt Critical CSS" /></a><figcaption>Automating web performance using Grunt. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d4c17e2-6672-42b7-8b43-d21760444d9c/03-critical-css-grunt.gif">View large version</a>)</figcaption></figure>

If you navigate to the folder, you should now notice a file called <i>result.html</i> that contains the inlined critical CSS and the remaining CSS loaded asynchronously. Your web page is now ready to rock and roll!

Behind the scenes, this plugin actually uses <a href="https://phantomjs.org/">PhantomJS</a>, a headless WebKit browser, to capture the required critical CSS. This means it is able to silently load your web page and test for the optimal critical CSS. This functionality also gives the plugin flexibility when it comes to different screen sizes. For example, you can provide different screen dimensions and the <strong>plugin will capture and inline your critical CSS</strong> accordingly.</p>

<pre><code class="language-javascript">critical: {
  dist: {
    options: {
      base: './',
      dimensions: [{
        width: 1300,
        height: 900
      },
      {
        width: 500,
        height: 900
      }]
    },
    files: [
      {src: ['index.html'], dest: 'dist/index.html'}
    ]
  }
}</code></pre>

The code above will process the given file against multiple dimensions and inline the appropriate critical CSS. This means that you can run your site against a number of screen widths and ensure that your users will still have the same experience throughout. As we know, mobile connections using 3G and 4G can be flaky at the best of times – that’s why this technique is so important to mobile users.

## Using Critical In A Production Environment

Using a tool like Critical is a great way to automatically extract and inline your critical CSS without having to change the way you develop your websites, but how does this fit into the real world? To put the newly updated files into action, you simply deploy as you normally would – nothing needs to change on your production environment. You need only remember that you will need to run Grunt every time you build or make changes to your CSS files.

The code samples we have run through in this article have covered the use of a single file, but what happens when you need to <strong>process the critical CSS for multiple files</strong>, or even an entire folder? Your Gruntfile can be updated to handle multiple files, similar to the example below.</p>

<pre><code class="language-javascript">critical: {
  dist: {
    options: {
      base: './',
      dimensions: [{
        width: 1300,
        height: 900
       },
       {
        width: 500,
        height: 900
      }]
    },
    files: [
      {src: ['index.html'], dest: 'dist/index.html'},
      {src: ['blog.html'], dest: 'dist/blog.html'}
      {src: ['about.html'], dest: 'dist/about.html'}
      {src: ['contact.html'], dest: 'dist/contact.html'}
    ]
  }
}</code></pre>

You could also run the task against every HTML file in a given folder using the code below:

<pre><code class="language-javascript">critical: {
  dist: {
    options: {
      base: './',
      dimensions: [{
        width: 1300,
        height: 900
      },
      {
        width: 500,
        height: 900
      }],
      src: '*.html',
      dest:  'dist/'
    }
  }
}</code></pre>

The code samples above provide an insight into how this could be achieved across your website.</p>

### Testing

As always, testing any new changes is very important. If you'd like to test your changes, there are some amazing tools that are freely available online. Head over to <a href="https://developers.google.com/speed/pagespeed/insights/">Google's PageSpeed Insights</a> and run your URL through the tool. You should notice that your web page now no longer has any blocking resources and your performance improvements suggestion has gone green – <em>woohoo</em>! And you are probably familiar with another great tool, <a href="https://www.webpagetest.org/">WebPagetest</a>, too.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5713d6bb-fd05-4d34-882f-2ae69864ab01/04-webpagetest-filmstrip-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c07b23a-455a-40f2-b0d3-1b1e2f46991d/04-webpagetest-filmstrip-opt-small.jpg" alt="Using WebPagetest is a great way to test that your web page renders in a timely manner." /></a><figcaption>Using WebPagetest is a great way to test that your web page renders in a timely manner. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5713d6bb-fd05-4d34-882f-2ae69864ab01/04-webpagetest-filmstrip-opt.jpg">View large version</a>)</figcaption></figure>

It is a free tool that allows you to run a website speed test from multiple locations around the globe. Apart from an informative analytical review of your web page, if you choose “<a href="https://www.webpagetest.org/video/">Visual Comparison</a>”, the tool will compare two web pages with each other. This is a great way to compare your results before and after updating your critical CSS and play back the differences.

The idea behind using critical CSS is that our web pages render sooner, thus presenting something to users as soon as possible. The best way to measure this is to use the <a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index">speed index</a>. It is a measurement, taken by WebPagetest, that measures how quickly the page contents are visually populated. The <strong>SpeedIndex measures the visual progress of the visible page loading</strong> and computes an overall score for how quickly the content was painted. Try to <a href="https://www.webpagetest.org/video/">compare</a> your SpeedIndex measurement before and after you have made changes by inlining your critical CSS. You will be impressed at how much of a difference it can make to your render times.</p>

### Diving A Little Deeper

As with most optimization techniques, there are always pros and cons that might affect your site. One of the downsides with inlining your critical CSS is that you <strong>miss out on caching CSS in the browser</strong> because it has been inlined in the page. If we are dealing with dynamic pages that change often, we wouldn't want to cache the HTML pages themselves. This means that the CSS inlined in the HTML is <a href="https://calendar.perfplanet.com/2011/why-inlining-everything-is-not-the-answer/">redownloaded every time</a>. There is a lot to be said for inlining only the critical CSS and instead asynchronously loading the remaining non-critical CSS. We can always cache this non-critical CSS. Depending on which side of the fence you sit with this, there are a lot of arguments for and against the concept of inling your CSS in the <code>&lt;head&gt;</code>, but for more information I recommend reading “<a href="https://medium.com/@drublic/a-counter-statement-putting-the-css-in-the-head-f98103d09ce1">A counter statement: Putting the CSS in the head</a>” by Hans Christian Reinl.

If you use a content delivery network (CDN), it is also worth remembering that you should still <strong>serve your non-critical CSS from the CDN</strong>. Doing so allows you to serve cached resources directly from the edge, delivering much faster response times, instead of routing all the way to the origin server to get them.

For traditional web pages, the technique of inlining your CSS works well, but it might not always be applicable depending on your situation. What if you have client-side JavaScript that generates HTML? What if you work on a single page application? If you can output as much of the critical CSS as soon as possible, it will boost page rendering, too. It's important to understand how critical CSS works and if it applies to you. I like Guy Podjarny's stance on this:
<blockquote>"Despite all these limitations, Inlining is still a good and important tool in the world of Front-End Optimization. As such, you should use it, but be careful not to abuse it."
—Guy Podjarny</blockquote>

In “<a href="https://calendar.perfplanet.com/2011/why-inlining-everything-is-not-the-answer/">Why Inlining Everything Is NOT The Answer</a>”, he provides good recommendations as to when you should <em>and shouldn't</em> inline your CSS.</p>

## It's Not Perfect

While many of the tools required to generate and inline critical CSS are constantly improving, there might be a few areas for improvement. If you notice any bugs in your project, <a href="https://github.com/addyosmani/critical/issues">open up an issue</a> or pull request and help contribute to the project on GitHub.

Optimizing the critical rendering path for your website can go a long way towards improving your page load times. Using this technique allows us to use a responsive layout without compromising on its well-known benefits. It’s also a great way to ensure that your page loads quickly without holding back on your design.</p>

### Further Resources

If you prefer to use another build system such as Gulp, you can use the plugin directly without downloading Grunt. There is also a useful tutorial showing <a href="https://github.com/addyosmani/critical-path-css-demo#tutorial">how to optimize a basic page with Gulp</a>.

There are other plugins that will extract your critical CSS, such as <a href="https://github.com/pocketjoso/penthouse">Penthouse</a>, and <a href="https://github.com/filamentgroup/criticalCSS">criticalCSS</a> from the Filament Group. I also thoroughly recommend reading “<a href="https://www.filamentgroup.com/lab/performance-rwd.html">How we make RWD sites load fast as heck</a>” by the Filament Group for a good overview of how they use this technique to ensure that their web pages load as quickly as possible.

The editor-in-chief of Smashing Magazine, Vitaly Friedman, wrote an article about how Smashing Magazine <a href="https://www.smashingmagazine.com/2014/09/08/improving-smashing-magazine-performance-case-study/">improved the performance</a> of this website using this technique. If you would like to learn more about the critical rendering path, there is <a href="https://www.udacity.com/course/ud884">a useful course available for free on the Udacity website</a>. The <a href="https://developers.google.com/web/fundamentals/performance/critical-rendering-path/">Google Developers website</a> also has some good content that covers <a href="https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path?hl=en">optimizing CSS delivery</a>. Patrick Hamman also wrote a great piece on <a href="https://patrickhamann.com/workshops/performance/tasks/2_Critical_Path/2_2.html">how to identify critical CSS</a> in his workshop, Building a Faster Web.

Are you inlining critical CSS in your project by default? What tools are you using? What problems have you been running into? Share your experiences in the comments to this article!

{{< signature "il, rb, ml, og" >}}

