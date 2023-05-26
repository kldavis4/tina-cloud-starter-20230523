---
title: Entering The Wonderful World of Geo Location
slug: entering-the-wonderful-world-of-geo-location
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33fab8f4-0215-47ff-8cda-1fafb1e14844/geo.jpg
date: 2010-03-08T23:56:29.000Z
author: christian-heilmann
description: >-
  I thought I could not be out-geeked. With a background in radio, and having dabbled in the demo scene on the Commodore 64 and hung out on BBS and IRC for a long time and all the other things normal kids don't quite get, I thought I was safe in this area.
categories:
  - Coding
  - HTML5
---
Then I went to my first WhereCamp, an unconference dealing with geographical issues and how they relate to the world of Web development. Even my A-Levels in Astronomy did not help me there. I was out-geeked by the people who drive and tweak the things that we now consider normal about geo-location on the Web.

Pulling out your phone, find your location and getting directions to the nearest bar is easy, but a lot of work has gone into making that possible. The good news is that because of that effort, mere geo-mortals like you and me can now create geographically aware products using a few lines of code. So, let's give the geo-community a big hand.

Be sure to check out the following articles:

*   [Legal Guidelines For The Use Of Location Data On The Web](https://www.smashingmagazine.com/2016/03/location-data-web-development-and-the-law/)
*   [<span class="headline">Should You Ask The User Or Their Browser?</span>](https://www.smashingmagazine.com/2013/02/remove-interface-elements/)
*   [Improve User Experience With Real-Time Features](https://www.smashingmagazine.com/2016/04/improve-user-experience-real-time-features/)
*   [Redesigning The Country Selector](https://www.smashingmagazine.com/2011/11/redesigning-the-country-selector/)

{{% feature-panel %}}

## Why Geo Matters

First of all, why is it important to consider physical location on this planet (at this moment) when we develop Web products? There are a few answers to this.

The first answer is mobility. The days of people sitting in front of desktop machines at home are over. Sales of mobile devices, laptops and netbooks have overtaken those of bulky stationary computers in the last few years. The power of processors now allows us to use smaller, more mobile hardware to perform the same tasks. So, if people use their hardware on the go, we should bring our systems to them. Which brings us to the second—very important—point: relevance.

Giving the user content that is relevant to the physical space they are in at the moment makes a lot of sense. We are creatures of habit. While we love the reach of the Internet, we also want to be able to find things in our local area easily: people to meet, cafes to frequent, interesting buildings and museums to learn about. The advertising industry—especially of the adult and dating variety—realized this years ago. I am sure you have come across one of the following before:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b9f012-39ea-488a-9d45-454d7707e229/adultpersonals.jpg" alt="Adult personal ads with geo location" />

I am sure these ads are more successful than the ones that show only user names. That the photos and names are the same for every location doesn't seem to be a problem (but yes, I noticed it). So how does it all work?

## Getting The User's Location Via IP

Every computer on a network has a number that identifies it: its <a href="https://en.wikipedia.org/wiki/IP_address">IP address</a>. The Internet is nothing but a massive network, and your IP number is assigned to you by the service provider that you have used to connect to that network. Because the numbers that service providers assign change from one geographical location to the next (much like telephone numbers), you can make quite a good estimate of where your visitors are from.

To find out where a certain phone number is from, you use a phone book. To find out where an IP is from, you can use the <a href="https://maxmind.com">Maxmind GeoIP database</a>. Maxmind also provides a JavaScript solution that you can use on websites:

<pre><code class="language-javascript">&lt;script type="text/javascript" src="https://j.maxmind.com/app/geoip.js"&gt;&lt;/script&gt;
&lt;script&gt;
  var info = document.getElementById('info');
  var lat = geoip_latitude();
  var lon = geoip_longitude();
  var city = geoip_city();
  var out = '&lt;h3&gt;Information from your IP&lt;/h3&gt;'+
            '&lt;ul&gt;'+
            '&lt;li&gt;Latitude: ' + lat + '&lt;/li&gt;'+
            '&lt;li&gt;Longitude: ' + lon + '&lt;/li&gt;'+
            '&lt;li&gt;City: ' + city + '&lt;/li&gt;'+
            '&lt;li&gt;Region: ' + geoip_region() + '&lt;/li&gt;'+
            '&lt;li&gt;Region Name: ' + geoip_region_name() + '&lt;/li&gt;'+
            '&lt;li&gt;Postal Code: ' + geoip_postal_code() + '&lt;/li&gt;'+
            '&lt;li&gt;Country Code: ' + geoip_country_code() + '&lt;/li&gt;'+
            '&lt;li&gt;Country Name: ' + geoip_country_name() + '&lt;/li&gt;'+
            '&lt;/ul&gt;'
  info.innerHTML = out;
&lt;/script&gt;</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40ad0056-ed9d-42f5-a636-0eb22599dbff/geolocation.jpg" alt="Getting the users geographical location using IP - in this case Sunnyvale, California" />

This gives you some information on the user (<a href="https://isithackday.com/hacks/geo/js-location.html">try it out for yourself</a>). The challenge, though, is relevance. Your IP location is the location of the IP that your provider has assigned to you. Depending on your provider, this could be quite a ways off (in my case, I live in London, but my provider used to show me as living in Rochester). Another problem is if you work for a company that uses a <a href="https://en.wikipedia.org/wiki/Virtual_private_network">VPN</a>. At Yahoo, for example, I have to connect to the VPN to read my company email, and I have to choose a location to connect to:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/901e08f0-f862-4c3f-a8b9-092febda32c0/vpn.jpg" alt="A VPN client allowing me to connect to different servers around the world" />

So, for a solution like the one highlighted above, I would show up as being in a totally different part of the world (which might be useful for watching Internet TV in the UK while I am in the US). IP geo-location, then, is an approximation, not a dead-on science.</p>

## Getting The User's Location Via The W3C Geo API

Guessing geographical location via IP is possible, but it can also be pretty creepy. Being able to take advantage of your location is useful, but security-conscious users and people who are generally suspicious of the Internet are not happy with the idea of their movements being monitored by a computer. This makes sense: if I can monitor your whereabouts day and night, I would know where and when to rob your house without you being there.

There are a lot of solutions to the challenge of having good-quality geo-location and maintaining privacy. Google Gears <a href="https://code.google.com/apis/gears/api_geolocation.html">has a geo-location service</a>; Plazes helps you store your location; and Yahoo's Fire Eagle is probably the most polished way to securely maintain your location on the Web.

The problem with all of these services is that they require the user to either install a plug-in or visit a Web service to update their location. This is not fun; browsers should do the work for you.

We now have a <a href="https://www.w3.org/TR/geolocation-API/">W3C recommendation for a geo-location API</a> that allows browsers to request the geographical location of the user. This makes it less creepy, and you get real data back.

Firefox 3.5 and above <a href="https://www.mozilla.com/firefox/geolocation/">supports the W3C geo-location API</a>. So does <a href="https://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariWebContent/GettingGeographicalLocations/GettingGeographicalLocations.html">Safari on the iPhone if you run OS 3.0 or above</a>. If you use the API, the browser will ask the user whether they want to share their location with your website.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f2339a-ee52-4a9a-a1e3-64a954d4ce7c/geowarning.jpg" alt="The geolocation API asks the user if they want to share their location" />

Once the user allows you to get their location, you get much more detailed latitude and longitude values. Using the API is very easy:

<pre><code class="language-javascript">// if the browser supports the w3c geo api
if(navigator.geolocation){
  // get the current position navigator.geolocation.getCurrentPosition(

  // if this was successful, get the latitude and longitude function(position){
    var lat = position.coords.latitude;
    var lon = position.coords.longitude;
  },
  // if there was an error function(error){
    alert('ouch');
  });
}</code></pre>

<a href="https://isithackday.com/hacks/geo/js-w3c-location.html">Compare the IP and W3C solutions</a> side by side. As you can see, there can be quite a difference in measuring the visitor's location. The extent of the difference is <a href="https://isithackday.com/hacks/geo/distance.php">shown in the following demo</a>:

<a href="https://isithackday.com/hacks/geo/distance.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f22d851-1bef-4578-8f44-1b716bcb4a3c/difference.jpg" alt="Difference between IP location and W3C Geo API location" /></a>

## Converting Latitude And Longitude Back Into A Name

Having more information is nice, but we have lost the name of the city and all the other nice data that came with the Maxmind database. Because the location has changed, we cannot just grab that old data; we have to find a way to convert latitude and longitude coordinates into a name. This process is called "<a href="https://en.wikipedia.org/wiki/Reverse_geocoding">reverse geo-coding</a>," and several services on the Web allow you to do it. Probably the most well-known is <a href="https://www.geonames.org/export/reverse-geocoding.html">the geo-names Web service</a>, but it has a few issues. For starters, the results are very US-centric.

One freely available but lesser-known reverse geo-coder that works worldwide comes from a surprising source: Flickr. The <a href="https://www.flickr.com/services/api/flickr.places.findByLatLon.html">flickr.places.findByLatLon</a> service returns a location from a latitude and longitude coordinates. You can <a href="https://www.flickr.com/services/api/explore/?method=flickr.places.findByLatLon">try it out in the app explorer</a>, but by far the easiest way to use it is by using the <a href="https://developer.yahoo.com/yql">Yahoo Query Language</a> (or YQL). YQL deserves its own article, but let's just say that, instead of having to authenticate with the Flickr API and read the docs, reverse geo-coding becomes as easy as this:

<pre><code class="language-javascript">select * from flickr.places where lat=37.416115 and lon=-122.0245671</code></pre>

Using the YQL Web service, you can get the result back as XML or JSON. So, to use the service in JavaScript, all you need is the following:

<pre><code class="language-javascript">&lt;script type="text/javascript" charset="utf-8"&gt;
 function getPlaceFromFlickr(lat,lon,callback){
   // the YQL statement
   var yql = 'select * from flickr.places where lat='+lat+' and lon='+lon;

   // assembling the YQL webservice API
   var url = 'https://query.yahooapis.com/v1/public/yql?q='+
              encodeURIComponent(yql)+'&amp;format=json&amp;diagnostics='+
              'false&amp;callback='+callback;

   // create a new script node and add it to the document
   var s = document.createElement('script');
   s.setAttribute('src',url);
   document.getElementsByTagName('head')[0].appendChild(s);
 };

 // callback in case there is a place found
 function output(o){
   if(typeof(o.query.results.places.place) != 'undefined'){
     alert(o.query.results.places.place.name);
   }
 }

 // call the function with my current lat/lon
 getPlaceFromFlickr(37.416115,-122.02456,'output');
&lt;/script&gt;</code></pre>

Combine that with the other services, and we get a <a href="https://isithackday.com/hacks/geo/distance-info.php">more detailed result and can put a name to the coordinates</a>:

<a href="https://isithackday.com/hacks/geo/distance-info.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef9e60be-ecb1-4ac2-83c2-1d77cfef80b1/reversegeocode.jpg" alt="adding the flickr reverse geocode we can get a name for a lat and lon pair" /></a>

## The Trouble With Latitude And Longitude

While latitude and longitude coordinates are a good way to describe a location on Earth, it is also ambiguous. The coordinates could represent either the centre of a city or a point of interest (such as a museum or a pub) in that spot.</p>

### WOEID to the Rescue

To work around the problem, Yahoo and Flickr (and soon will Twitter) support another way to pinpoint a location. The <a href="https://developer.yahoo.com/geo/geoplanet/guide/concepts.html">Where On Earth Identifier</a> (or WOEID) is a more granular way to describe locations on Earth. Because Flickr supports it, we can easily get get photos from a particular area:

<pre><code class="language-markup tmp-sql">select * from flickr.photos.search where woe_id in (
  select place.woeid from flickr.places where lat=37.416115 and lon=-122.02456
)</code></pre>

Using this and <a href="https://isithackday.com/hacks/geo/flickr-yql-reverse-geocoding-photos.html">a few lines of JavaScript</a>, showing geo-located photos is pretty easy:

<a href="https://isithackday.com/hacks/geo/flickr-yql-reverse-geocoding-photos.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21a281f7-34e8-4d8f-8770-370007ceed32/geolocated-photos.jpg" alt="Photos from a geographical location using YQL and Flickr" /></a>

This has also been wrapped in a <a href="https://isithackday.com/hacks/geo/yql-photolist.html">simple-to-use YQL solution</a>. The following code will display 10 photos of Paris:

<pre><code class="language-markup tmp-html">&lt;script&gt;
  function photos(o){
    var container = document.getElementById('photos');
    container.innerHTML = o.results;
  }
&lt;/script&gt;
&lt;script src="https://query.yahooapis.com/v1/public/yql?q=
select%20*%20from%20flickr.photolist%20where%20location%3D%22<strong>paris%2Cfr</strong>
%22%20and%20text%3D%22%22%20and%20amount%3D<strong>10</strong>&amp;format=xml&amp;
env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys&amp;callback=<strong>photos</strong>"&gt;</code></pre>

You can also <a href="https://developer.yahoo.com/yql/console/?q=select%20*%20from%20flickr.photolist%20where%20location%3D%22paris%2Cfr%22%20and%20text%3D%22%22%20and%20amount%3D10&amp;env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys">play with this in the YQL console</a>.</p>

## Why Not Search For The Location's Name?

The main question about implementations such as the one above is why couldn't we just do a search on Flickr for the city, instead of doing all the complex geo-lookups? The reason is false positives. Take Paris, for example: if you want to show photos of Paris on a travel website, you don't want Paris Hilton to show up in there. Same goes for Jack London. You may also want to show photos of London, England, not London, Ontario. Geographic data is full of these kinds of gotchas, and the term for finding the right one is "disambiguation." See the <a href="https://en.wikipedia.org/wiki/Victoria_%28geographical_disambiguation%29">Wikipedia article on "Victoria"</a> to see just how many geographical contexts this term can have.</p>

## Turning Text Into Geo-Data

Finding a visitor's geographic location is all well and good, but it doesn't mean much if you can't link it to information for that area. This is where it gets tricky. For Flickr (and soon Twitter), this is easy, because both services are able to attach geographical locations to the content you put in them. This is not so for most of the information on the Web, though, and this is when we resort to clever algorithms, machine-learning, pattern-matching and all the other think-tank stuff that computers and the scientists in front of them do.

Say you want to identify the geographical locations that a particular text or Web page talks about. Yahoo offers a service for that called <a href="https://developer.yahoo.com/geo/placemaker/">Placemaker</a>, and it is pretty easy to use. You need to get a <a href="https://developer.yahoo.com/wsregapp/">developer key</a> and send this as <code>appid</code>, send a text as <code>documentContent</code>, define the type of the text as <code>documentType</code> and define the type of data you want back as <code>outputType</code>. All of this needs to be sent as a <code>POST</code> to <code>https://wherein.yahooapis.com/v1/document</code>:

<pre><code class="language-markup tmp-html">&lt;form action="<strong>https://wherein.yahooapis.com/v1/document</strong>" method="post"&gt;
  &lt;textarea id="text" name="documentContent"&gt;Hi there, I am Chris.
    I live in London, I am currently in Sunnyvale and will soon be in
    Atlanta and Las Vegas.&lt;/textarea&gt;
  &lt;div&gt;&lt;input type="submit" name="sub" value="get locations"&gt;&lt;/div&gt;
  &lt;input type="hidden" name="appid" value="<strong>{YOUR_APP_ID}</strong>"&gt;
  &lt;input type="hidden" name="documentType" value="text/plain"&gt;
  &lt;input type="hidden" name="outputType" value="xml"&gt;
&lt;/form&gt;</code></pre>

You can <a href="https://isithackday.com/hacks/geo/simple-placemaker.php">try this out yourself</a>. Using PHP to call the API instead of a simple form, you can even format the output nicely. See it in action <a href="https://isithackday.com/hacks/geo/placemaker.php">here</a>:

<a href="https://isithackday.com/hacks/geo/simple-placemaker.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07036298-271e-4c8e-87e4-ccd4178d8ae4/placemaker-results.jpg" alt="finding locations in a text and showing them on a map using Yahoo Placemaker" /></a>

While developers who have played around with Web services won't find Placemaker hard to use, the service can be daunting for the average developer. That is why I built <a href="https://icant.co.uk/geomaker">GeoMaker</a> some time ago. GeoMaker allows you to enter a text or URL, select the locations you want to include in the final outcome, and get the locations either as a map to copy and paste or as micro-formats.

<a href="https://icant.co.uk/geomaker/index.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22fea648-c673-4e04-9a9f-92977e9b8780/geomaker.jpg" alt="Geomaker in action" /></a>

However, because there is also a YQL solution for using PlaceMaker in JavaScript, we can do the same with a few lines of client-side code to enhance an HTML document. Check out the following example:

<a href="https://isithackday.com/hacks/geo/addmap.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1a5c301-0c84-4e25-93f2-1253b6a273fc/textandmap.jpg" alt="A map created from geographical locations in a text" /></a>

To use this, you need three things: a text with geographical locations in them in an element with an ID, a Google Maps API key (<a href="https://code.google.com/apis/maps/signup.html">which you can get here</a>) and the following few lines of code:

<pre><code class="language-markup tmp-html">&lt;script src="https://github.com/codepo8/geotoys/raw/master/addmap.js"&gt;&lt;/script&gt;
&lt;script&gt;
addmap.config.mapkey = 'COPY YOUR API KEY HERE';
addmap.analyse('content');
&lt;/script&gt;</code></pre>

This makes it incredibly easy to give your visitors a sense of what part of the world a text is related to.</p>

## Adding Maps To Your Documents

Online maps have been around for a while now (and Google Maps was instrumental in the rise of AJAX), and many providers out there allow you to add maps to your documents. Google is probably the leader, but Yahoo also has maps, as does Microsoft and many more. There is even a fully open map service called <a href="https://www.openstreetmap.org/">Open Street Maps</a>, which has been <a href="https://www.opengeodata.org/2010/01/24/osm-the-default-map-in-haiti/">instrumental in the recent rescue efforts in Haiti</a>.

If you want interactive maps, probably the easiest thing to use is <a href="https://www.mapstraction.com/">Mapstraction</a>, which is a JavaScript library that does away with the discrepancies between the various map providers and gives you a single interface for all of them. 24ways published a <a href="https://24ways.org/2007/get-to-grips-with-slippy-maps">good introduction to it</a> three years ago.

Probably the simplest way to show a map that supports markers and paths in your document without having to dive into JavaScript is the <a href="https://code.google.com/apis/maps/documentation/staticmaps/">Google static maps API</a>. It creates maps as images, and all you need to do is provide the map information in the <code>src</code> URI of the image. For example, in the script example above, this would be:

<pre><code class="language-javascript">https://maps.google.com/maps/api/staticmap?
sensor=false
&amp;size=200x200
&amp;maptype=roadmap
&amp;key=<em>YOUR_MAP_KEY</em>
&amp;markers=color:blue|label:1|37.4447,-122.161
&amp;markers=color:blue|label:2|37.3385,-121.886
&amp;markers=color:blue|label:3|37.3716,-122.038
&amp;markers=color:blue|label:4|37.7792,-122.42</code></pre>

You can define the size and type of the map. If all you provide is the location of markers, the API will automatically find the right zoom level and area to ensure that all markers are visible. Google's website even offers a detailed <a href="https://github.com/googlemaps/js-v2-samples">tool to create static maps</a>, including markers and paths.</p>

## Geo Is A Space To Watch

I hope this has given you some insight into all of the things you can do to bring the earth to your product and to put your product on the map. Geo-location and geo-aware services are already huge, and they'll be even more important this year. There will be more services—some mobile providers are ready to roll out new hardware and software—and now you can be a part of it.

What the geo-world needs now is a designer's eye, and this is where you can help the geo-geeks create apps that matter, that look great and that make a difference in our visitors' lives. For inspiration, check out <a href="https://youtube.com/watch?v=vVZkHuomqfM">Mapumental</a>, which allows you to pinpoint a place to live in London, or see how Google Earth and some 3-D Objects allow you to <span class="removed_link" title="https://earth-api-samples.googlecode.com/svn/trunk/demos/milktruck/index.html">race a milk truck on real map data</span>.

{{< signature "al" >}}

