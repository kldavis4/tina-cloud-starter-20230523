---
title: A Beginner’s Guide To jQuery-Based JSON API Clients
slug: beginners-guide-jquery-based-json-api-clients
image: null
date: 2012-02-09T12:45:51.000Z
author: ben-howdle
description: >-
  Are you fascinated by dynamic data? Do you go green with envy when you see tweets pulled magically into websites? Trust me, I’ve been there.
categories:
  - Coding
  - AJAX
  - JavaScript
  - jQuery
  - API
---
The goal of today’s tutorial is to create a simple Web app for grabbing movie posters from <a href="https://www.themoviedb.org/">TMDb</a>. We’ll use jQuery and the user’s input to query a JSON-based API and deal with the returned data appropriately.

I hope to convince you that APIs aren’t scary and that most of the time they can be a developer’s best friend.

## APIs Are The Future But, More Importantly, The Present

JSON-based APIs are a hot property on the Web right now. I cannot remember the last time I went onto a blog or portfolio without seeing the owner’s tweets or Facebook friends staring back at me. This interactivity makes the Web an exciting place. The only limit seems to be people’s imagination. As demonstrated by everything from pulled tweets to a self-aware <a href="https://josscrowcroft.github.com/open-exchange-rates/">exchange-rates API</a>, data is currently king, and websites are swapping it freely.

Developers are allowing us to get at their data much more openly now; no longer is everything under lock and key. Websites are proud to have you access their data and, in fact, encourage it. Websites such as <a href="https://www.themoviedb.org/">TMDb</a> and <a href="https://www.last.fm/">LastFM</a> allow you to build entirely separate applications based on the data they’ve spent years accumulating. This openness and receptiveness are fostering an intertwined network of users and their corresponding actions.

<img class="106952 alignnone" title="Front Row Home Page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e123a3ed-0019-4f42-b747-3999e893bece/screen-shot-2011-09-10-at-01.24" alt="screenshot" width="500" height="333" />

This article is aimed at people who are competent in HTML and CSS and have basic knowledge of jQuery techniques. We won’t delve deep into advanced JavaScript techniques, but will rather help the beginner who wants to create more complex Web tools.

### APIs in a Nutshell

In basic terms, an API enables you to access a website’s data without going near its databases. It gives us a user-friendly way to read and write data to and from a website’s databases.

{{% feature-panel %}}

## Sure, Great, But What Code Do I Need?

Like many developers, I bounce merrily between back-end and front-end development, and I am as happy working in PHP as in jQuery. It just depends on which hat I’m wearing that day.

Because this article is mainly about jQuery-based JSON API clients, we’ll focus on client-side code (i.e. jQuery).

When dealing with APIs, and armed with jQuery, one is more likely to encounter JSON.

### Player 1: JSON

<a href="https://www.json.org/">JSON</a> (or JavaScript Object Notation) is a lightweight, easy and popular way to exchange data. jQuery is not the only tool for manipulating and interfacing with JSON; it’s just my and many others’ preferred method.

A lot of the services we use everyday have JSON-based APIs: Twitter, Facebook and Flickr all send back data in JSON format.

A JSON response from an API looks like this:

<div class="break-out">

 <pre><code class="language-json">([{"score":
null,"popularity":
3,"translated":true,"adult":
false,"language":"en","original_name":"The Goonies","name":"The Goonies","alternative_name":"I Goonies",
"movie_type":"movie","id":9340,"imdb_id":"tt0089218",
"url":"https://www.themoviedb.org/movie/9340",
"votes":16,"rating":9.2,"certification":"PG","overview":"A young teenager named Mikey Walsh finds an old treasure map in his father's attic.
Hoping to save their homes from demolition, Mikey and his friends Data Wang, Chunk Cohen, and Mouth Devereaux runs off on a big quest
to find the secret stash of the pirate One-Eyed Willie.","released":"1985-06-07",
"posters":[{"image":{"type":"poster","size":"original","height":1500,"width":1000,
"url":"https://cf1.imgobject.com/posters/76b/4d406d767b9aa15bb500276b/the-goonies-original.jpg",
"id":"4d406d767b9aa15bb500276b"}}],"backdrops":[{"image":{"type":"backdrop","size":"original","height":1080,"width":1920,
"url":"https://cf1.imgobject.com/backdrops/242/4d690e167b9aa13631001242/the-goonies-original.jpg",
"id":"4d690e167b9aa13631001242"}}],"version":3174,"last_modified_at":"2011-09-12 13:19:05"}])</code></pre>
</div>

A bit of a mess, right? Compare this to the same JSON viewed in Google Chrome’s developer console:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/014a3673-f138-470e-bdf9-ab3c528c6265/json-file-shown-in-google-chrome-dev-console.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/014a3673-f138-470e-bdf9-ab3c528c6265/json-file-shown-in-google-chrome-dev-console.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/014a3673-f138-470e-bdf9-ab3c528c6265/json-file-shown-in-google-chrome-dev-console.png'>Large preview</a>)" alt="JSON viewed in Google Chrome’s developer console" >}}

The JSON response is accessible via a jQuery function, allowing us to manipulate, display and, more importantly, style it however we want.

### Player 2: jQuery

Personally, I’d pick jQuery over JavaScript any day of the week. jQuery makes things a lot easier for the beginner Web developer who just wants stuff to work right off the bat. I use it every day. If I had to complete the same tasks using native Javascript, my productivity would grind right down. In my opinion, JavaScript is for people who want a deeper understanding of the scripting language and the DOM itself. But for simplicity and ease of use, jQuery is where it’s at.

In essence, jQuery is a JavaScript library, with handy functions like <code>getJSON</code>. This particular function will be the glue that holds our API client together.

{{% ad-panel-leaderboard %}}

## The Goal: A jQuery-Based JSON API Client

I recently submitted to An Event Apart the Web app that we’re about to go through now. It’s called Front Row.

The idea of the Web app is to take a movie title inputted by the user, run it through <a href="https://www.themoviedb.org/">TMDb</a>’s API, and return the relevant poster. The user could then share it or save it to their computer.

The Web app is split into HTML, CSS and jQuery. We’ll focus on the jQuery, because that’s where the magic happens.

### The HTML

Below is the basic structure of the Web app. Nothing special here.

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
   &lt;meta name="author" content="Ben Howdle and Dan Matthew"&gt;
   &lt;meta name="description" content="A responsive movie poster grabber"&gt;
   &lt;title&gt;Front Row by Ben Howdle&lt;/title&gt;
   &lt;meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=1.0"&gt;
   &lt;script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js"&gt;&lt;/script&gt;
        &lt;!--jQuery, linked from a CDN--&gt;
   &lt;script src="scripts.js"&gt;&lt;/script&gt;
   &lt;script type="text/javascript" src="https://use.typekit.com/oya4cmx.js"&gt;&lt;/script&gt;
   &lt;script type="text/javascript"&gt;try{Typekit.load();}catch(e){}&lt;/script&gt;
   &lt;link rel="stylesheet" href="style.css" /&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div class="container"&gt;
   &lt;header&gt;
      &lt;h1&gt;Front Row&lt;/h1&gt;
   &lt;/header&gt;
   &lt;section id="fetch"&gt;
      &lt;input type="text" placeholder="Enter a movie title" id="term" /&gt;
      &lt;button id="search"&gt;Find me a poster&lt;/button&gt;
   &lt;/section&gt;
   &lt;section id="poster"&gt;
   &lt;/section&gt;
   &lt;footer&gt;
      &lt;p&gt;Created by &lt;a href="https://twostepmedia.co.uk"&gt;Ben Howdle&lt;/a&gt;&lt;/p&gt;
   &lt;/footer&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

All we’ve got is a bit of Twitter self-indulgence, an input field and a submission button. Done!

The CSS is a bit off topic for this article, so I’ll leave it to you to inspect the elements of interest on the live website.

### The jQuery

<div class="break-out">

 <pre><code class="language-javascript">$(document).ready(function(){

   //This is to remove the validation message if no poster image is present

   $('#term').focus(function(){
      var full = $("#poster").has("img").length ? true : false;
      if(full == false){
         $('#poster').empty();
      }
   });
</code></pre>
</div>

I like validation messages to disappear when the user starts retyping in an input field. The script below checks whether an image is present (i.e. a movie poster), and if not, empties the container of the validation message once the input field gains focus.

<div class="break-out">

 <pre><code class="language-javascript">//function definition

   var getPoster = function(){

        //Grab the movie title and store it in a variable

        var film = $('#term').val();

         //Check if the user has entered anything

         if(film == ’){

            //If the input field was empty, display a message

            $('#poster').html("&lt;h2 class='loading'&gt;Ha! We haven't forgotten to validate the form! Please enter something.&lt;/h2&gt;");
</code></pre>
</div>

<img class="106961 alignnone" title="Front Row Form Validation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be361e57-b9e5-4482-aec6-546312438dae/screen-shot-2011-09-21-at-20.28" alt="" width="500" height="273" />

The reason why we store the main code that retrieves the data in a function will become clear later on (mainly, it’s for <a href="https://en.wikipedia.org/wiki/Don't_repeat_yourself">DRY programming</a>).

We then store the value of the input in a variable, so that when we use it again in the code, the jQuery doesn’t have to rescan the DOM.

Basic validation is performed on the input, checking that something has actually been entered in the field.

In an attempt at humor on my part, I display a message warning the user that they haven’t entered anything and asking them to please do so.

<div class="break-out">

 <pre><code class="language-javascript">} else {

            //They must have entered a value, carry on with API call, first display a loading message to notify the user of activity

            $('#poster').html("&lt;h2 class='loading'&gt;Your poster is on its way!&lt;/h2&gt;");
</code></pre>
</div>

If the input contains a value, we then process the user’s request. Another message is displayed, letting the user know that something is happening.

<div class="break-out">

 <pre><code class="language-javascript">$.getJSON("https://api.themoviedb.org/2.1/Movie.search/en/json/23afca60ebf72f8d88cdcae2c4f31866/" + film + "?callback=?", function(json) {

               //TMDb is nice enough to return a message if nothing was found, so we can base our if statement on this information

               if (json != "Nothing found."){

                  //Display the poster and a message announcing the result

                     $('#poster').html('&lt;h2 class="loading"&gt;Well, gee whiz! We found you a poster, skip!&lt;/h2&gt;&lt;img id="thePoster" src=' + json[0].posters[0].image.url + ' /&gt;');
</code></pre>
</div>

<img class="106962 alignnone" title="Front Row Found Poster" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/867f928b-95f9-442e-a835-9282d9362a81/screen-shot-2011-09-21-at-20.29" alt="" width="500" height="444" />

Here we get to the meat of our API client. We use jQuery’s <a href="https://api.jquery.com/jQuery.getJSON/"><code>getJSON</code></a> function, which, by definition, loads “JSON-encoded data from the server using a <code>GET</code> HTTP request.”

We then use the API’s URL, <a href="https://api.themoviedb.org/2.1/">suppled in this case by TMDb</a>. As with many other APIs, you have to register your application in order to receive a key (a 30-second process). We insert the API key (<code>23afca60ebf72f8d88cdcae2c4f31866</code>) into the URL and pass the user’s movie title into the URL as a search parameter.

One thing to mention is that appending <code>callback=?</code> to the end of the URL enables us to make cross-domain JSON and AJAX calls. Don’t forget this, otherwise the data will be limited to your own domain! This method uses what’s called JSONP (or JSON with padding), which basically allows a script to fetch data from another server on a different domain. To do this, we must specify the callback above when jQuery loads the data. It replaces the <code>?</code> with our custom function’s name, thereby allowing us to make cross-domain calls with ease.

In the function’s callback, we have put the word <code>json</code> (which holds our retrieved data), but we could have put <code>data</code> or <code>message</code>.

The next check is to see whether any data was returned. TMDb is kind enough to supply us with a message of “Nothing found” when it can’t find anything. So, we’ve based our <code>if</code> statement on this string’s value.

This check is API-specific. Usually if no results are found, we would expand the object to find a property named <code>length</code>, which would tell us how many results were returned. If this happens, the code might look something like this:

<pre><code class="language-javascript">if (json.length != 0){</code></pre>

As a side note, before writing even a line of code in the callback function of the JSON call, we should become familiar with the results returned in Chrome’s console or in Firebug. This would tell us exactly what to check for in <code>if</code> statements and, more importantly, what path to take to grab the data we want.

Let’s add <code>console.log(json);</code>, like so:

<div class="break-out">

 <pre><code class="language-javascript">$.getJSON("https://api.themoviedb.org/2.1/Movie.search/en/json/23afca60ebf72f8d88cdcae2c4f31866/" + film + "?callback=?", function(json) {
         console.log(json);
</code></pre>
</div>

This will output something like the following in the console of your favorite browser:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48e5ceb4-24f5-418f-a2cd-ec66234b16b0/result-in-favorite-browser.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48e5ceb4-24f5-418f-a2cd-ec66234b16b0/result-in-favorite-browser.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48e5ceb4-24f5-418f-a2cd-ec66234b16b0/result-in-favorite-browser.png'>Large preview</a>)" alt="the output in the console of your favorite browser" >}}

The last line of this code outputs our poster. We display another message to the user saying that we’ve found a result, and then proceed to show the image.

Let’s spend a moment figuring out how we got to the poster images using the line <code>json[0].posters[0].image.url</code>.

The reason we use <code>json[0]</code> is that — since we want to display only one poster, and knowing how relevant TMDb’s results are — we can gamble on the first result. We then access the <code>posters</code> array like so: <code>json[0].posters[0]</code>. Chrome even tells us that <code>posters</code> is an array, so we know what we’re dealing with. Again, we access the first value of the array, having faith that it will be most relevant. It then tells us that <code>image</code> is an object, so we can access it like so: <code>json[0].posters[0].image</code>. By expanding our object further, we see that <code>image</code> contains a property named <code>url</code>. Jackpot! This contains a direct image link, which we can use in the <code>src</code> attribute of our image element.

<div class="break-out">

 <pre><code class="language-javascript">} else {

   //If nothing is found, I attempt humor by displaying a Goonies poster and confirming that their search returned no results.

   $.getJSON("https://api.themoviedb.org/2.1/Movie.search/en/json/
23afca60ebf72f8d88cdcae2c4f31866/goonies?callback=?", function(json) {

      $('#poster').html('&lt;h2 class="loading"&gt;We're afraid nothing was found for that search. Perhaps you were looking for The Goonies?&lt;/h2&gt;&lt;img id="thePoster" src=' + json[0].posters[0].image.url + ' /&gt;');

   });
}</code></pre>
</div>

Having determined that the API has no results for the user, we could display an error message. But this being a movie-related Web app, let’s give the user a preset poster of The Goonies and let them know we couldn’t find anything. We’ll use the exact same <code>src</code> attribute for the image that we used before, this time with <code>goonies</code> hardcoded into the API call’s URL.

<div class="break-out">

 <pre><code class="language-javascript">});

          }

        return false;
   }

   //Because we've wrapped the JSON code in a function, we can call it on mouse click or on a hit of the Return button while in the input field

   $('#search').click(getPoster);

   $('#term').keyup(function(event){

       if(event.keyCode == 13){

           getPoster();

       }

   });

});
</code></pre>
</div>

It is now clear why we wrapped our JSON call in a function: doing so allows us to run the function when the user hits the submission button or presses Enter while in the input field.

<img class="106965 alignnone" title="Front Row Top Gun Poster" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c93217-1488-4209-b303-c38556da9a1f/front-row-by-ben-howdle-1316805278242-e1316805570421.png" alt="" width="500" height="525" />

## The Full Code

### The HTML

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
   &lt;meta name="author" content="Ben Howdle and Dan Matthew"&gt;
   &lt;meta name="description" content="A responsive movie poster grabber"&gt;
   &lt;title&gt;Front Row by Ben Howdle&lt;/title&gt;
   &lt;meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=1.0"&gt;
   &lt;script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js"&gt;&lt;/script&gt;
        &lt;!--jQuery, linked from a CDN--&gt;
   &lt;script src="scripts.js"&gt;&lt;/script&gt;
   &lt;script type="text/javascript" src="https://use.typekit.com/oya4cmx.js"&gt;&lt;/script&gt;
   &lt;script type="text/javascript"&gt;try{Typekit.load();}catch(e){}&lt;/script&gt;
   &lt;link rel="stylesheet" href="style.css" /&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div class="container"&gt;
   &lt;header&gt;
      &lt;h1&gt;Front Row&lt;/h1&gt;
   &lt;/header&gt;
   &lt;section id="fetch"&gt;
      &lt;input type="text" placeholder="Enter a movie title" id="term" /&gt;
      &lt;button id="search"&gt;Find me a poster&lt;/button&gt;
   &lt;/section&gt;
   &lt;section id="poster"&gt;
   &lt;/section&gt;
   &lt;footer&gt;
      &lt;p&gt;Created by &lt;a href="https://twostepmedia.co.uk"&gt;Ben Howdle&lt;/a&gt;&lt;/p&gt;
   &lt;/footer&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

### The jQuery

<div class="break-out">

 <pre><code class="language-javascript">$(document).ready(function(){

   $('#term').focus(function(){
      var full = $("#poster").has("img").length ? true : false;
      if(full == false){
         $('#poster').empty();
      }
   });

   var getPoster = function(){

        var film = $('#term').val();

         if(film == ’){

            $('#poster').html("&lt;h2 class='loading'&gt;Ha! We haven't forgotten to validate the form! Please enter something.&lt;/h2&gt;");

         } else {

            $('#poster').html("&lt;h2 class='loading'&gt;Your poster is on its way!&lt;/h2&gt;");

            $.getJSON("https://api.themoviedb.org/2.1/Movie.search/en/json/
23afca60ebf72f8d88cdcae2c4f31866/" + film + "?callback=?", function(json) {
               if (json != "Nothing found."){
                     $('#poster').html('&lt;h2 class="loading"&gt;Well, gee whiz! We found you a poster, skip!&lt;/h2&gt;&lt;img id="thePoster" src=' + json[0].posters[0].image.url + ' /&gt;');
                  } else {
                     $.getJSON("https://api.themoviedb.org/2.1/Movie.search/en/json/
23afca60ebf72f8d88cdcae2c4f31866/goonies?callback=?", function(json) {
                        console.log(json);
                        $('#poster').html('&lt;h2 class="loading"&gt;We're afraid nothing was found for that search. Perhaps you were looking for The Goonies?&lt;/h2&gt;&lt;img id="thePoster" src=' + json[0].posters[0].image.url + ' /&gt;');
                     });
                  }
             });

          }

        return false;
   }

   $('#search').click(getPoster);
   $('#term').keyup(function(event){
       if(event.keyCode == 13){
           getPoster();
       }
   });

});
</code></pre>
</div>

## Conclusion

That’s it: a handy method of reading data from a remote API with jQuery, and manipulating the JSON output to fit our needs.

Every API is different, and every one returns different results in a different structure — it’s all part of the fun! So, get used to using <code>console.log()</code>, and familiarize yourself with the results set before trying to access it with code or using it in your application.

Start with something practical and entertaining: build a check-in checker with Gowalla’s API; visualize trends with Twitter’s API; or make a face-recognition app with Face.com’s API.

APIs are fun. By definition, the data they bring to the page is dynamic, not static.

If you have any problems with the API we’ve used here or you have any success stories with other APIs, please do leave a comment.

## Further Resources

*   “[How to Use JSON APIs With jQuery](https://www.gethifi.com/blog/how-to-use-json-apis-with-jquery),” Joel Sutherland, HiFi
*   “How to Use jQuery With a JSON Flickr Feed to Display Photos,” Richard Shepherd
*   “[Bing Instant Search With jQuery and Ajax](https://www.9lessons.info/2011/02/bing-instant-search-with-jquery-and.html),” Srinivas Tamada, 9Lessons

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [Local Storage And How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)
*   [Understanding REST And RPC For HTTP APIs](https://www.smashingmagazine.com/2016/09/understanding-rest-and-rpc-for-http-apis/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)

{{< signature "al, il" >}}
