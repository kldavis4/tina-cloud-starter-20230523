---
title: Syncing Content With HTML5 Video
slug: syncing-content-with-html5-video
image: null
date: 2011-03-11T11:19:36.000Z
author: christian-heilmann
description: >-
  One of the main changes from HTML4 to HTML5 is that the new specification
  breaks a few of the boundaries that browsers have been confined to. Instead of
  restricting user interaction to text, links, images and forms, HTML5 promotes
  multimedia, from a generic `<object>` element to a highly specified `<video>`
  and `<audio>` element, and with a rich API to access in pure JavaScript.

  Native multimedia capability has a few benefits. For instance, end users have
  full control over the multimedia. The native controls of browsers allow users
  to save videos locally or email them to friends. Also, HTML5 video and audio
  are keyboard-enabled by default, which is a great accessibility benefit.
categories:
  - Coding
  - Techniques
  - Videos
  - HTML5
  - HTML
---
One of the main changes from HTML4 to HTML5 is that the new specification breaks a few of the boundaries that browsers have been confined to. Instead of restricting user interaction to text, links, images and forms, HTML5 promotes multimedia, from a generic <code>&lt;object&gt;</code> element to a highly specified <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> element, and with a rich API to access in pure JavaScript.

Native multimedia capability has a few benefits:

*   **End users have full control over the multimedia.**.  The native controls of browsers allow users to save videos locally or email them to friends. Also, HTML5 video and audio are keyboard-enabled by default, which is a great accessibility benefit.
*   **End users do not need to install a plug-in to play them.**.  The browser already has everything it needs to play movies and sound.
*   **Video and audio content on the page can be manipulated.**.  They are simply two new elements like any other that can be styled, moved, manipulated, stacked and rotated.
*   **You can build your own controls using HTML, CSS and JavaScript.**.  No new skills or development environment needed.
*   **Interaction with the rest of the page is simple.**.  The multimedia API gives you full control over the video, and you can make the video react both to changes in the video itself and to the page around it.

Let’s quickly recap how you can use native video in the browser, starting with the embedding task.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Creative Use of Video in Web Design: Background Videos](https://www.smashingmagazine.com/2011/01/creative-use-of-background-video-web-design-showcase/)
*   [The Future Of Video In Web Design](https://www.smashingmagazine.com/2013/11/the-future-of-video-in-web-design/)
*   [Bringing Production Video To The Web](https://www.smashingmagazine.com/2016/04/html5-media-source-extensions-bringing-production-video-web/)

{{% feature-panel %}}

## Embedding Video

This is old news. Embedding video in a document is as easy as adding a <code>&lt;video&gt;</code> element and pointing it to the source video. Adding a <code>controls</code> attribute gives you native controls:

<pre><code class="language-markup tmp-xml">&lt;video src="chris.ogv" controls&gt;&lt;/video&gt;</code></pre>

This is the theory, though. In the real world of intellectual property, corporate competition and device-specific solutions, we as developers have to jump through a few hoops:

<pre><code class="language-markup tmp-xml">&lt;video controls="true" height="295" width="480"&gt;
  &lt;!-- hello iOS, Safari and IE9 --&gt;
  &lt;source src="chris.mp4" type="video/mp4"&gt;
  &lt;!-- Hello Chrome and Firefox (and Opera?) --&gt;
  &lt;source src="chris.webm" type="video/webm"&gt;
  &lt;!-- Hello Firefox and Opera --&gt;
  &lt;source src="chris.ogv" type="video/ogg"&gt;
  &lt;!-- Hello legacy --&gt;
  Your browser does not support the video tag, 
  &lt;a href="https://youtube.com/watch?v=IhkUe_KryGY"&gt;
    check the video on YouTube
  &lt;/a&gt;.
&lt;/video&gt;</code></pre>

This shows how we need to deliver video in three formats in order to satisfy all of the different browsers out there. There are a few ways to accomplish this. Here’s what I do…

## Convert Video With Miro Video Converter

<a href="https://www.mirovideoconverter.com/">Miro Video Converter</a> is an open-source tool for Mac that makes converting videos dead easy. Simply drag the video to the tool, select WebM as the output format, and watch the progress. A few <a href="https://www.webmproject.org/tools/">other converters for Windows and Linux</a> are available, too.

<a href="https://www.mirovideoconverter.com/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e84950a6-3862-496a-ad0c-6e48def71e50/miro.png" alt="Miro Video Converter in action - simply drag a video, select output format and press convert" /></a>

## Hosting And Automated Conversion On Archive.org

Because I license my videos with <a href="https://creativecommons.org">Creative Commons</a>, I can use <a href="https://archive.org">Archive.org</a> to both host the videos and convert the WebM versions to MP4 and OGV. Simply upload your video and wait about an hour. Reload the page, and the server pixies at Archive.org will have created the other two formats (and also a cool animated GIF of your video).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10fbeeeb-8435-4ab4-b3aa-945c94d161b4/archiveorg.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99ecb139-8d1a-45b2-9c7c-b5725ccc74d4/archive-org.jpg" alt="Different versions of an uploaded video by archive.org" width="550" height="449" /></a><br>
<em>You can use <a href="https://www.archive.org">Archive.org</a> to both host the videos and convert the WebM versions to MP4 and OGV. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10fbeeeb-8435-4ab4-b3aa-945c94d161b4/archiveorg.png">Large view</a>.</em>

## Industrial-Strength Conversion With Vid.ly

WebM, OGV and MP4 take care of only the major browsers, though. If you want to support all mobile devices, tablets and consoles and you want the video quality to adapt to the user’s connection speed, then you’ll have to create a few dozen versions of the same video. Encoding.com feels our pain and has released a free service called <a href="https://vid.ly">Vid.ly</a>, which converts any video you upload into many different formats more or less in real time. Unfortunately, the service is in private beta at the moment, but you can use the invite code <code>HNY2011</code>.

<a href="https://vid.ly"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73fa9680-7e08-4cdb-9cea-848ceec9fb98/vid-ly.jpg" alt="Different versions of an uploaded video by archive.org" width="550" height="587" /></a><br>
<em><a href="https://vid.ly">Vid.ly</a> converts any video you upload into many different formats more or less in real time. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/009cc25f-23f3-4c34-b02a-74c93e4c42c5/vidly.png">Large view</a>.</em>

Furthermore, Vid.ly creates a URL for your video that automatically redirects the browser or device calling it to the right format. This keeps your embed code as simple as possible:

<pre><code class="language-markup tmp-xml">&lt;video src="https://vid.ly/4f3q1f?content=video" controls&gt;&lt;/video&gt;</code></pre>

Cool, isn’t it?

## The Power Of The HTML5 Video API: Syncing Content

Now that our video is on the page, let’s check out the power of the API. Say, for example, you want to know what part of the movie is playing right now. This is as simple as subscribing to an event of the <code>&lt;video&gt;</code> element:

<pre><code class="language-javascript">&lt;div id="stage"&gt;
  &lt;video src="https://vid.ly/4f3q1f?content=video" controls&gt;&lt;/video&gt; 
  &lt;div id="time"&gt;&lt;/div&gt;
&lt;/div&gt;       
&lt;script&gt;
  (function(){
    var v = document.getElementsByTagName('video')[0]
    var t = document.getElementById('time');
    v.addEventListener('timeupdate',function(event){
      t.innerHTML = v.currentTime;
    },false);
  })();
&lt;/script&gt;</code></pre>

If you <a href="https://isithackday.com/syncing-video/play.html">try this out</a> in your browser, you will see the current time below the video when you play it.

<a href="https://isithackday.com/syncing-video/play.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e6cdbcc-5cc0-4756-9c96-8163d86d3e17/time.png" alt="Displaying the current time of a video" /></a>

You will also see that the <code>timeupdate</code> event gets fired a lot and at somewhat random times. If you want to use this to sync the showing and hiding of parts of the document, then you’ll need to throttle it somehow. The easiest way to do this is to <a href="https://isithackday.com/syncing-video/playfullsecond.html">limit the number to full seconds</a> using <code>parseInt()</code>:

<pre><code class="language-markup tmp-xml">&lt;div id="stage"&gt;
  &lt;video src="https://vid.ly/4f3q1f?content=video" controls&gt;&lt;/video&gt; 
  &lt;div id="time"&gt;&lt;/div&gt;
&lt;/div&gt;       
&lt;script&gt;
  (function(){
    var v = document.getElementsByTagName('video')[0]
    var t = document.getElementById('time');
    v.addEventListener('timeupdate',function(event){
      t.innerHTML = parseInt(v.currentTime) + ' - ' + v.currentTime;
    },false);
  })();
&lt;/script&gt;</code></pre>

<a href="https://isithackday.com/syncing-video/playfullsecond.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/534dcdc4-1c88-43f3-b8c6-fc20bf92e037/timesecond.png" alt="Displaying the current time of a video" /></a>

You can use this to trigger functionality at certain times. For example, you can sync an <a href="https://isithackday.com/spirit-of-indiana/">Indiana Jones-style animation of a map to a video</a>:

For a full explanation of this demo, check out the <a href="https://hacks.mozilla.org/2010/12/spirit-of-indiana-jones-syncing-html5-video-with-maps/">blog post on Mozilla Hacks</a>.

Let’s have a go at something similar: a video that shows the content from web pages being referred to by a presenter. Check out <a href="https://isithackday.com/syncing-video/">this video demo of me explaining what we’re doing here</a>, with the content appearing and disappearing at certain times in the video. Make sure to jump around the video with the controls.

<a href="https://isithackday.com/syncing-video/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33ea1e44-46a1-4710-b00e-d04ae380c5a7/syncing.jpg" alt="Syncing video and content" width="550" height="316" /></a>

We’ve already covered how to get the current time of a video in seconds. What I want now is to display and hide a few parts of the website at certain times in the video. If video is not supported in the browser, then I would just <a href="https://isithackday.com/syncing-video/allarticles.html">show all of the content without any syncing</a>.

The first issue I have to solve is to allow the maintainer to control what is shown when. Normally, I’d use a JSON object in the JavaScript, but I figure that keeping the maintenance in the markup itself makes much more sense.

HTML5 allows you to store information in <code>data-</code> attributes. So, to make it easy to tell the script when to show what, I just use <code>data-start</code> and <code>data-end</code> attributes, which define the time frames for the articles that I want to sync with the video:

<pre><code class="language-markup tmp-xml">&lt;article data-start="64" data-end="108"&gt;
  &lt;header&gt;&lt;h1&gt;Archive.org for conversion&lt;/h1&gt;&lt;/header&gt;
  &lt;p&gt;&lt;a href="https://archive.org"&gt;Archive.org&lt;/a&gt; is a website dedicated to 
archiving the Internet. For content released as under a Creative Commons
license, it offers hosting for video and audio and automatically converts the
content to MP4 and Ogg video for you.&lt;/p&gt;
  &lt;iframe src="https://archive.org"&gt;&lt;/iframe&gt;
&lt;/article&gt;</code></pre>

You can try it out by <a href="https://github.com/codepo8/Syncing-Video">downloading the code</a> and changing the values yourself (or use Firebug or the Web Inspector to change it on the fly).

Here’s the script (using jQuery) that makes this happen:

<pre><code class="language-javascript">/* if the document is ready… */
$(document).ready(function(){

/* if HTML5 video is supported */
  if($('video').attr('canPlayType')){

    $('aside::first').append('&lt;p&gt;Play the video above and see how ' +
                             'the different connected content sections ' +
                             'in the page appear at the right moment. '+
                             'Feel free to jump forward and backward&lt;/p&gt;');

    var timestamps = [],
        last = 0,
        all = 0,
        now = 0,
        old = 0,
        i=0;

/* hide all articles via CSS */
    $('html').addClass('js');

/* 
   Loop over the articles, read the timestamp start and end and store 
   them in an array
*/
    $('article').each(function(o){
      if($(this).attr('data-start')){
        timestamps.push({
          start : +$(this).attr('data-start'),
          end : +$(this).attr('data-end'),
          elm : $(this)
        });
      }
    });

    all = timestamps.length;

/* 
  when the video is playing, round up the time to seconds and call the 
  showsection function continuously
*/
    $('video').bind('timeupdate',function(event){
      now = parseInt(this.currentTime);

      /* throttle function calls to full seconds */
      if(now &gt; old){
        showsection(now);
      }
      old = now;

    });

/*
  Test whether the current time is within the range of any of the 
  defined timestamps and show the appropriate section.
  Hide all others.
*/
    function showsection(t){
      for(i=0;i&lt;all;i++){
        if(t &gt;= timestamps[i].start &amp;&amp; t &lt;= timestamps[i].end){
          timestamps[i].elm.addClass('current');
        } else {
          timestamps[i].elm.removeClass('current');
        }
      }
    };

  };
});</code></pre>

So, what’s going on here? First, we’re checking whether the browser is capable of playing HTML5 video by testing for the <code>canPlayType</code> attribute. If all is fine, then we add some explanatory text to the document (which wouldn’t make sense if the browser couldn’t show a video). Then, we define some variables to use and add a class of <code>js</code> to the root element of the document. This, together with the <code>.js article</code> selector in the CSS, hides all of the articles in the document.

We then loop through the articles, read out the timestamps for the start and end of each of the sections and store them in an array called <code>timestamps</code>.

We then subscribe to the <code>timeupdate</code> event, rounded up to full seconds, and call the <code>showsection()</code> function every new second.

The <code>showsection()</code> function loops through all of the timestamps and tests whether the current time of the video is in the range of one of the articles. If it is, then that article is displayed (by adding a <code>current</code> class) and all the others are hidden. This could be optimized by storing the current section and removing the class from only that element.

## Can We Do The Same With Less Or No Code?

If you like the idea of syncing content and video, check out the <a href="https://popcornjs.org/">Popcorn framework</a>, which is based on the same techniques but gives you much more control over the video itself.

<a href="https://popcornjs.org/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32568df7-bdab-44c1-b168-bff96273b37d/popcorn.gif" alt="popcorn.js" width="550" height="605" /></a>

<a href="https://popcornjs.org/butter/">Butter</a> is a point-and-click interface to go on top of Popcorn. It has a nice timeline editor that allows you to play a video and show all kinds of Web content at certain times. You can export and send your creations to friends, too.

<a href="https://popcornjs.org/butter/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d9a60e9-4640-484c-85d9-b02a7d68ab36/butter.jpg" alt="Screenshot Butter in action" width="550" height="380" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7f699a-7683-43b5-b495-d55124529d70/butter.png">Large view</a></em>

With systems like Popcorn and Butter, we are one step closer to having authoring tools for the rich interactions that HTML5 offers us. What can you think of building?

## Summary

Today we looked at how to embed video onto a Web document; and with the native video API that gives us event handlers for changes in a video, we saw how easy it is to make the video interact with the rest of the document. Instead of trying to control the video, we use native controls to make the page react to what is happening in the video itself. We used semantic HTML and data attributes to allow maintainers to use the syncing script without having to touch any JavaScript, and we looked at some services that make hosting and converting video easy.

All of these cool technologies give us a lot of power, but we can’t just, say, write some simple CSS, JavaScript and HTML to use them. If we want open technologies to succeed, then we have to make them easy for people to use. The next step now is to move from the “one-off implementation” phase and think about creating tools and step-by-step code-creation systems for users who want to use these cool new technologies but don’t want to spend much time and effort doing it.

With native audio and video in browsers, we’ve taken a massive step toward make the open Web more engaging and beautiful. The next step will be to use multimedia not only for output but for input. A lot of hardware these days comes with cameras and microphones; we need to start using and supporting open technology that allows our users to take advantage of this hardware to interact with our Web products.

<em>For a screencast on this topic, see <a href="https://hacks.mozilla.org/2011/03/syncing-page-content-with-html5-video/">Syncing page content with HTML5 video</a> on the Mozilla Hacks blog.</em>

{{< signature "al" >}}

