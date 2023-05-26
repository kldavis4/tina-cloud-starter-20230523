---
title: Local Storage And How To Use It On Websites
slug: local-storage-and-how-to-use-it
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d545b60-5a44-4ba4-87ce-8a76a329fad0/fireburg2.jpg
date: 2010-10-11T10:59:02.000Z
author: christian-heilmann
description: >-
  Storing information locally on a user's computer is a powerful strategy for a developer who is creating something for the Web. In this article, we'll look at how easy it is to store information on a computer to read later and explain what you can use that for.
categories:
  - Coding
  - HTML5
  - HTML
---
Storing information locally on a user's computer is a powerful strategy for a developer who is creating something for the Web. In this article, we'll look at how easy it is to store information on a computer to read later and explain what you can use that for. 

## Adding State To The Web: The “Why” Of Local Storage

The main problem with HTTP as the main transport layer of the Web is that it is <strong>stateless</strong>. This means that when you use an application and then close it, its state will be reset the next time you open it. If you close an application on your desktop and re-open it, its most recent state is restored.

{{% feature-panel %}}

This is why, as a developer, you need to store the state of your interface somewhere. Normally, this is done server-side, and you would check the user name to know which state to revert to. But what if you don't want to force people to sign up?

This is where <strong>local storage</strong> comes in. You would keep a key on the user's computer and read it out when the user returns.</p>

## C Is For Cookie. Is That Good Enough For Me?

The classic way to do this is by using a cookie. A cookie is a text file hosted on the user's computer and connected to the domain that your website runs on. You can store information in them, read them out and delete them. Cookies have a few limitations though:

*   They add to the load of every document accessed on the domain.
*   They allow up to only 4 KB of data storage.
*   Because cookies have been used to spy on people's surfing behavior, security-conscious people and companies turn them off or request to be asked every time whether a cookie should be set.

To work around the issue of local storage — with cookies being a rather dated solution to the problem — the WHATWG and W3C came up with <a href="https://html.spec.whatwg.org/multipage/webstorage.html">a few local storage specs</a>, which were originally a part of HTML5 but then put aside because HTML5 was already big enough.</p>

## Using Local Storage In HTML5-Capable Browsers

Using <a href="https://hacks.mozilla.org/2009/06/localstorage/">local storage</a> in modern browsers is ridiculously easy. All you have to do is modify the <code>localStorage</code> object in JavaScript. You can do that directly or (and this is probably cleaner) use the <code>setItem()</code> and <code>getItem()</code> method:

<pre><code class="language-javascript">localStorage.setItem('favoriteflavor','vanilla');</code></pre>

If you read out the <code>favoriteflavor</code> key, you will get back "vanilla":

<pre><code class="language-javascript">var taste = localStorage.getItem('favoriteflavor');
// -&gt; "vanilla"</code></pre>

To remove the item, you can use — can you guess? — the <code>removeItem()</code> method:

<pre><code class="language-javascript">localStorage.removeItem('favoriteflavor');
var taste = localStorage.getItem('favoriteflavor');
// -&gt; null</code></pre>

That's it! You can also use <code>sessionStorage</code> instead of <code>localStorage</code> if you want the data to be maintained only until the browser window closes.</p>

## Working Around The "Strings Only" Issue

One annoying shortcoming of local storage is that you can only store strings in the different keys. This means that when you have an object, it will not be stored the right way.

You can see this when you try the following code:

<pre><code class="language-javascript">var car = {};
car.wheels = 4;
car.doors = 2;
car.sound = 'vroom';
car.name = 'Lightning McQueen';
console.log( car );
localStorage.setItem( 'car', car );
console.log( localStorage.getItem( 'car' ) );</code></pre>

Trying this out in the console shows that the data is stored as <code>[object Object]</code> and not the real object information:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c7f4cfb-16dc-40c8-9b56-644a1792a3c2/console-e1285930679229.png" alt="local storage - Objects get turned into a descriptive string when stored" width="382" height="301" />

You can work around this by using the native <code>JSON.stringify()</code> and <code>JSON.parse()</code> methods:

<pre><code class="language-javascript">var car = {};
car.wheels = 4;
car.doors = 2;
car.sound = 'vroom';
car.name = 'Lightning McQueen';
console.log( car );
localStorage.setItem( 'car', JSON.stringify(car) );
console.log( JSON.parse( localStorage.getItem( 'car' ) ) );</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93e057af-227f-4da7-831a-58df5c6eea93/console2-e1285930703974.png" alt="local storage - Encoding as JSON means you keep the right format of the object in local storage" width="381" height="299" />

## Where To Find Local Storage Data And How To Remove It

During development, you might sometimes get stuck and wonder what is going on. Of course, you can always access the data using the right methods, but sometimes you just want to clear the plate. In Opera, you can do this by going to <em>Preferences → Advanced → Storage</em>, where you will see which domains have local data and how much:

<a href="/wp-content/uploads/2010/10/opera-e1285930764969.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/596d7bfb-95b6-49ce-92dc-320753d1dcb8/storage-opera.png" alt="Local Storage in Opera" width="500" height="366" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef7833e6-66a2-437e-9990-adb5d3ff2ab5/opera-e1285930764969.png">Large view</a></em>

Doing this in Chrome is a bit more problematic, which is why we made a screencast:

Mozilla has no menu access so far, but will in future. For now, you can go to the Firebug console and delete storage manually easily enough.

So, that's how you use local storage. But what can you use it for?

## Use Case #1: Local Storage Of Web Service Data

One of the first uses for local storage that I discovered was caching data from the Web when it takes a long time to get it. My World Info entry for the Event Apart 10K challenge shows what I mean by that.

When you call the demo the first time, you have to wait up to 20 seconds to load the names and geographical locations of all the countries in the world from the <a href="https://developer.yahoo.com/boss/">Yahoo BOSS</a> Premium Web service. If you call the demo a second time, there is no waiting whatsoever because — you guessed it — I've cached it on your computer using local storage.

The following code (which uses jQuery) provides the main functionality for this. If local storage is supported and there is a key called <code>thewholefrigginworld</code>, then call the <code>render()</code> method, which displays the information. Otherwise, show a loading message and make the call to the Geo API using <code>getJSON()</code>. Once the data has loaded, store it in <code>thewholefrigginworld</code> and call <code>render()</code> with the same data:

<pre><code class="language-javascript">if(localStorage &amp;&amp; localStorage.getItem('thewholefrigginworld')){
  render(JSON.parse(localStorage.getItem('thewholefrigginworld')));
} else {
  $('#list').html('
</code></pre>

'+loading+'

'); var query = 'select centroid,woeid,name,boundingBox'+ ' from geo.places.children(0)'+ ' where parent_woeid=1 and placetype="country"'+ ' | sort(field="name")'; var YQL = 'https://query.yahooapis.com/v1/public/yql?q='+ encodeURIComponent(query)+'&amp;diagnostics=false&amp;format=json'; $.getJSON(YQL,function(data){ if(localStorage){ localStorage.setItem('thewholefrigginworld',JSON.stringify(data)); } render(data); }); }

You can see the difference in loading times in the following screencast:

The code for the world info is <a href="https://github.com/codepo8/worldinfo">available on GitHub</a>.

This can be extremely powerful. If a Web service allows you only a certain number of calls per hour but the data doesn't change all that often, you could store the information in local storage and thus keep users from using up your quota. A photo badge, for example, could pull new images every six hours, rather than every minute.

This is very common when using Web services server-side. Local caching keeps you from being banned from services, and it also means that when a call to the API fails for some reason, you will still have information to display.

<code>getJSON()</code> in jQuery is especially egregious in accessing services and breaking their cache, as explained in <a href="https://www.yqlblog.net/blog/2010/03/12/avoiding-rate-limits-and-getting-banned-in-yql-and-pipes-caching-is-your-friend/">this blog post from the YQL team</a>. Because the request to the service using <code>getJSON()</code> creates a unique URL every time, the service does not deliver its cached version but rather fully accesses the system and databases every time you read data from it. This is not efficient, which is why you should cache locally and use <code>ajax()</code> instead.</p>

## Use Case #2: Maintaining The State Of An Interface The Simple Way

Another use case is to store the state of interfaces. This could be as crude as storing the entire HTML or as clever as maintaining an object with the state of all of your widgets. One instance where I am using local storage to cache the HTML of an interface is the Yahoo Firehose research interface (<a href="https://github.com/codepo8/firehose-research">source on GitHub</a>):

The code is very simple — using YUI3 and a test for local storage around the local storage call:

<pre><code class="language-javascript">YUI().use('node', function(Y) {
  if(('localStorage' in window) &amp;&amp; window['localStorage'] !== null){
    var key = 'lastyahoofirehose';

    localStorage.setItem(key,Y.one('form').get('innerHTML'));

  if(key in localStorage){
      Y.one('#mainform').set('innerHTML',localStorage.getItem(key));
      Y.one('#hd').append('
</code></pre>

**Notice:** We restored your last search for you - not live data'); } } });

You don't need YUI at all; it only makes it easier. The logic to <a href="https://www.wait-till-i.com/2010/08/26/using-html5-storage-to-cache-application-interfaces/">generically cache interfaces in local storage</a> is always the same: check if a "Submit" button has been activated (in PHP, Python, Ruby or whatever) and, if so, store the <code>innerHTML</code> of the entire form; otherwise, just read from local storage and override the <code>innerHTML</code> of the form.</p>

## The Dark Side Of Local Storage

Of course, any powerful technology comes with the danger of people abusing it for darker purposes. Samy, the man behind the <a href="https://en.wikipedia.org/wiki/Samy_(computer_worm)">"Samy is my hero" MySpace worm</a>, recently released a rather scary demo called <a href="https://samy.pl/evercookie/">Evercookie</a>, which shows how to exploit all kind of techniques, including local storage, to store information of a user on their computer even when cookies are turned off. This code could be used in all kinds of ways, and to date there is no way around it.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Auto-Save User’s Input In Your Forms With HTML5 And Sisyphus.js](https://www.smashingmagazine.com/2011/12/sisyphus-js-client-side-drafts-and-more/)
*   [Keeping Web Users Safe By Sanitizing Input Data](https://www.smashingmagazine.com/2011/01/keeping-web-users-safe-by-sanitizing-input-data/)
*   [An In-Depth Introduction To Ember.js](https://www.smashingmagazine.com/2013/11/an-in-depth-introduction-to-ember-js/)
*   [Building A Simple Cross-Browser Offline To-Do List](https://www.smashingmagazine.com/2014/09/building-simple-cross-browser-offline-todo-list-indexeddb-websql/)

Research like this shows that we need to look at HTML5's features and add-ons from a security perspective very soon to make sure that people can't record user actions and information without the user's knowledge. An opt-in for local storage, much like you have to opt in to share your geographic location, might be in order; but from a UX perspective this is considered clunky and intrusive. Got any good ideas?

{{< signature "al" >}}

