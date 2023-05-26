---
title: Web Scraping With Node.js
slug: web-scraping-with-nodejs
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147b5716-bc38-4619-b624-3c701a2afa30/words-illu-opt.png'
date: 2015-04-08T21:04:10.000Z
author: elliotbonneville
description: >-
  Web scraping is the process of programmatically retrieving information from
  the Internet. As the volume of data on the web has increased, this practice
  has become increasingly widespread, and a number of powerful services have
  emerged to simplify it.

  Unfortunately, the majority of them are costly, limited or have other
  disadvantages. Instead of turning to one of these third-party resources, **you
  can use Node.js to create a powerful web scraper** that is both extremely
  versatile and completely free.
categories:
  - Coding
  - JavaScript
  - Node.js
---
Web scraping is the process of programmatically retrieving information from the Internet. As the volume of data on the web has increased, this practice has become increasingly widespread, and a number of powerful services have emerged to simplify it. Unfortunately, the majority of them are costly, limited or have other disadvantages. Instead of turning to one of these third-party resources, <strong>you can use Node.js to create a powerful web scraper</strong> that is both extremely versatile and completely free.

In this article, I'll be covering the following:

*   two Node.js modules, Request and Cheerio, that simplify web scraping;
*   an introductory application that fetches and displays some sample data;
*   a more advanced application that finds keywords related to Google searches.

Also, a few things worth noting before we go on: <strong>A basic understanding of Node.js is recommended for this article</strong>; so, if you haven’t already, <a href="https://nodejs.org/">check it out</a> before continuing. Also, web scraping may violate the terms of service for some websites, so just make sure you’re in the clear there before doing any heavy scraping.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful Node.js Tools, Tutorials And Resources](https://www.smashingmagazine.com/2011/09/useful-node-js-tools-tutorials-and-resources/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Sailing With Sails.js: An MVC-style Framework For Node.js](https://www.smashingmagazine.com/2015/11/sailing-sails-js-mvc-style-framework-node-js/)
*   [The Issue With Global Node Packages](https://www.smashingmagazine.com/2016/01/issue-with-global-node-npm-packages/)

{{% feature-panel %}}

## Modules

To bring in the Node.js modules I mentioned earlier, we’ll be using <a href="https://www.npmjs.com/">NPM</a>, the Node Package Manager (if you’ve heard of Bower, it’s like that — except, you use NPM to install Bower). NPM is a package management utility that is automatically installed alongside Node.js to make the process of using modules as painless as possible. By default, NPM installs the modules in a folder named <code>node_modules</code> in the directory where you invoke it, so make sure to call it in your project folder.

And without further ado, here are the modules we’ll be using.</p>

### Request

While Node.js does provide simple methods of downloading data from the Internet via HTTP and HTTPS interfaces, you have to handle them separately, to say nothing of redirects and other issues that appear when you start working with web scraping. The <a href="https://github.com/request/request">Request module</a> merges these methods, abstracts away the difficulties and presents you with a single unified interface for making requests. We’ll use this module to download web pages directly into memory. To install it, run <code>npm install request</code> from your terminal in the directory where your main Node.js file will be located.</p>

### Cheerio

<a href="https://github.com/cheeriojs/cheerio">Cheerio</a> enables you to work with downloaded web data using the same syntax that jQuery employs. To quote the copy on its home page, “Cheerio is a fast, flexible and lean implementation of jQuery designed specifically for the server.” Bringing in Cheerio enables us to focus on the data we download directly, rather than on parsing it. To install it, run <code>npm install cheerio</code> from your terminal in the directory where your main Node.js file will be located.</p>

## Implementation

The code below is a quick little application to nab the temperature from a weather website. I popped in my area code at the end of the URL we’re downloading, but if you want to try it out, you can put yours in there (just make sure to install the two modules we’re attempting to require first; you can learn how to do that via the links given for them above).

<pre><code class="language-javascript">
var request = require("request"),
  cheerio = require("cheerio"),
  url = "https://www.wunderground.com/cgi-bin/findweather/getForecast?&amp;query=" + 02888;

request(url, function (error, response, body) {
  if (!error) {
    var $ = cheerio.load(body),
      temperature = $("[data-variable='temperature'] .wx-value").html();

    console.log("It’s " + temperature + " degrees Fahrenheit.");
  } else {
    console.log("We’ve encountered an error: " + error);
  }
});
</code></pre>

So, what are we doing here? First, we’re requiring our modules so that we can access them later on. Then, we’re defining the URL we want to download in a variable.

Then, we use the Request module to download the page at the URL specified above via the <code>request</code> function. We pass in the URL that we want to download and a callback that will handle the results of our request. When that data is returned, that callback is invoked and passed three variables: <code>error</code>, <code>response</code> and <code>body</code>. If Request encounters a problem downloading the web page and can’t retrieve the data, it will pass a valid error object to the function, and the body variable will be null. Before we begin working with our data, we’ll check that there aren’t any errors; if there are, we’ll just log them so we can see what went wrong.

If all is well, we pass our data off to Cheerio. Then, we’ll be able to handle the data like we would any other web page, using standard jQuery syntax. To find the data we want, we’ll have to build a selector that grabs the element(s) we’re interested in from the page. If you navigate to the URL I’ve used for this example in your browser and start exploring the page with developer tools, you’ll notice that the big green temperature element is the one I’ve constructed a selector for. Finally, now that we’ve got ahold of our element, it’s a simple matter of grabbing that data and logging it to the console.

We can take it plenty of places from here. I encourage you to play around, and I’ve summarized the key steps for you below. They are as follows.</p>

### In Your Browser

1.  Visit the page you want to scrape in your browser, being sure to record its URL.
2.  Find the element(s) you want data from, and figure out a jQuery selector for them.</p>

### In Your Code

1.  Use request to download the page at your URL.
2.  Pass the returned data into Cheerio so you can get your jQuery-like interface.
3.  Use the selector you wrote earlier to scrape your data from the page.</p>

## Going Further: Data Mining

More advanced uses of web scraping can often be categorized as <a href="https://en.wikipedia.org/wiki/Data_mining">data mining</a>, the process of downloading a lot of web pages and generating reports based on the data extracted from them. Node.js scales well for applications of this nature.

I’ve written a small data-mining app in Node.js, less than a hundred lines, to show how we’d use the two libraries that I mentioned above in a more complicated implementation. The app finds the most popular terms associated with a specific Google search by analyzing the text of each of the pages linked to on the first page of Google results.

There are three main phases in this app:

1.  Examine the Google search.
2.  Download all of the pages and parse out all the text on each page.
3.  Analyze the text and present the most popular words.

We’ll take a quick look at the code that’s required to make each of these things happen — as you might guess, not a lot.</p>

### Downloading the Google Search

The first thing we’ll need to do is find out which pages we’re going to analyze. Because we’re going to be looking at pages pulled from a Google search, we simply find the URL for the search we want, download it and parse the results to find the URLs we need.

To download the page we use Request, like in the example above, and to parse it we’ll use Cheerio again. Here’s what the code looks like:

<pre><code class="language-javascript">
request(url, function (error, response, body) {
  if (error) {
    console.log(“Couldn’t get page because of error: “ + error);
    return;
  }

  // load the body of the page into Cheerio so we can traverse the DOM
  var $ = cheerio.load(body),
    links = $(".r a");

  links.each(function (i, link) {
    // get the href attribute of each link
    var url = $(link).attr("href");

    // strip out unnecessary junk
    url = url.replace("/url?q=", "").split("&amp;")[0];

    if (url.charAt(0) === "/") {
      return;
    }

    // this link counts as a result, so increment results
    totalResults++;
</code></pre>

In this case, the URL variable we’re passing in is a Google search for the term “data mining.”

As you can see, we first make a request to get the contents of the page. Then, we load the contents of the page into Cheerio so that we can query the DOM for the elements that hold the links to the pertinent results. Then, we loop through the links and strip out some extra URL parameters that Google inserts for its own usage — when we’re downloading the pages with the Request module, we don’t want any of those extra parameters.

Finally, once we’ve done all that, we make sure the URL doesn’t start with a <code>/</code> — if so, it’s an internal link to something else of Google’s, and we don’t want to try to download it, because either the URL is malformed for our purposes or, even if it isn’t malformed, it wouldn’t be relevant.</p>

### Pulling the Words From Each Page

Now that we have the URLs of our pages, we need to pull the words from each page. This step consists of doing much the same thing we did just above — only, in this case, the URL variable refers to the URL of the page that we found and processed in the loop above.

<pre><code class="language-javascript">
request(url, function (error, response, body) {
  // load the page into Cheerio
  var $page = cheerio.load(body),
    text = $page("body").text();
</code></pre>

Again, we use Request and Cheerio to download the page and get access to its DOM. Here, we use that access to get just the text from the page.

Next, we’ll need to clean up the text from the page — it’ll have all sorts of garbage that we don’t want on it, like a lot of extra white space, styling, occasionally even the odd bit of JSON data. This is what we’ll need to do:

1.  Compress all white space to single spaces.
2.  Throw away any characters that aren’t letters or spaces.
3.  Convert everything to lowercase.

Once we’ve done that, we can simply split our text on the spaces, and we’re left with an array that contains all of the rendered words on the page. We can then loop through them and add them to our corpus.

The code to do all that looks like this:

<pre><code class="language-javascript">
// Throw away extra white space and non-alphanumeric characters.
text = text.replace(/\s+/g, " ")
       .replace(/[^a-zA-Z ]/g, "")
       .toLowerCase();

// Split on spaces for a list of all the words on that page and 
// loop through that list.
text.split(" ").forEach(function (word) {
  // We don't want to include very short or long words because they're 
  // probably bad data.
  if (word.length  20) {
    return;
  }

  if (corpus[word]) {
    // If this word is already in our corpus, our collection
    // of terms, increase the count for appearances of that 
    // word by one.
    corpus[word]++;
  } else {
    // Otherwise, say that we've found one of that word so far.
    corpus[word] = 1;
  }
});
</code></pre>

### Analyzing Our Words

Once we’ve got all of our words in our corpus, we can loop through that and sort them by popularity. First, we’ll need to stick them in an array, though, because the corpus is an object.

<pre><code class="language-javascript">
// stick all words in an array
for (prop in corpus) {
  words.push({
    word: prop,
    count: corpus[prop]
  });
}

// sort array based on how often they occur
words.sort(function (a, b) {
  return b.count - a.count;
});
</code></pre>

The result will be a sorted array representing exactly how often each word in it has been used on all of the websites from the first page of results of the Google search. Below is a sample set of results for the term “data mining.” (Coincidentally, I used this list to generate the word cloud at the top of this article.)

<pre><code class="language-html">
[ { word: 'data', count: 981 },
  { word: 'mining', count: 531 },
  { word: 'that', count: 187 },
  { word: 'analysis', count: 120 },
  { word: 'information', count: 113 },
  { word: 'from', count: 102 },
  { word: 'this', count: 97 },
  { word: 'with', count: 92 },
  { word: 'software', count: 81 },
  { word: 'knowledge', count: 79 },
  { word: 'used', count: 78 },
  { word: 'patterns', count: 72 },
  { word: 'learning', count: 70 },
  { word: 'example', count: 70 },
  { word: 'which', count: 69 },
  { word: 'more', count: 68 },
  { word: 'discovery', count: 67 },
  { word: 'such', count: 67 },
  { word: 'techniques', count: 66 },
  { word: 'process', count: 59 } ]
</code></pre>

If you’re interested in seeing the rest of the code, check out the <a href="https://gist.github.com/elliotbonneville/1bf694b8c83f358e0404">fully commented source</a>.

A good exercise going forward would be to take this application to the next level. You could optimize the text parsing, extend the search to multiple pages of Google results, even strip out common words that aren’t really key terms (like “that” and “from”). More bug handling could also be added to make the app even more robust — when you’re mining data, you want as many layers of redundancy as you can reasonably afford. The variety of content that you’ll be pulling in is such that inevitably you’ll come across an unexpected piece of text that, if unhandled, would throw an error and promptly crash your application.</p>

## In Conclusion

As always, if you find anything related to web scraping with Node.js that you think is helpful or just have questions or thoughts you want to share, be sure to let us know via the comments below. Also, follow me on Twitter @bovenille and check out <a href="https://heyjavascript.com">my blog</a> for more on Node.js, web scraping and JavaScript in general.

{{< signature "il, rb, al" >}}

