---
title: The Future Of Video In Web Design
slug: the-future-of-video-in-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04924297-4834-43bf-ad6c-5d3c8a2e281b/soundslice-opt-1.png
date: 2013-11-18T13:15:35.000Z
author: sean-fioritto
description: >-
  Federico was the only other kid on the block with a dedicated ISDN line, so I
  gave him a call. It had taken six hours of interminable waiting (peppered with
  frantic bouts of cursing), but **I had just watched 60 choppy seconds of the
  original Macintosh TV commercial in Firefox**, and I had to tell someone. It
  blew my mind.
categories:
  - Coding
  - CSS
  - JavaScript
  - Techniques
  - HTML
---
Federico was the only other kid on the block with a dedicated ISDN line, so I gave him a call. It had taken six hours of interminable waiting (peppered with frantic bouts of cursing), but I had just watched 60 choppy seconds of the original Macintosh TV commercial <em>in Firefox</em>, and I had to tell someone. It blew my mind.

Video on the Web has improved quite a bit since that first jittery low-res commercial I watched on my Quadra 605 back in 7th grade. <strong>But for the most part, videos are still separate from the Web</strong>, cordoned off by iframes and Flash and bottled up in little windows in the center of the page. They’re a missed opportunity for Web designers everywhere.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Syncing Content With HTML5 Video](https://www.smashingmagazine.com/2011/03/syncing-content-with-html5-video/)
*   [Creative Use of Video in Web Design: Background Videos](https://www.smashingmagazine.com/2011/01/creative-use-of-background-video-web-design-showcase/)
*   [HTML5 Media Source Extensions](https://www.smashingmagazine.com/2016/04/html5-media-source-extensions-bringing-production-video-web/)
*   [Making Embedded Content Work In Responsive Design](https://www.smashingmagazine.com/2014/02/making-embedded-content-work-in-responsive-design/)

But how do you integrate video into an app or a marketing page? What would it look like, and how do you implement it? In this article, you will find inspiration, how-tos and a few technical goodies to get you started with modern video on the Web.

{{% feature-panel %}}

## When Video Leaves Its Cage

Video combined with animation is a powerful tool for innovative and compelling user experiences. Imagine interactive screencasts and tutorials in which DOM elements flow and move around the page in sync with the instructor. Why not combine video with animation to walk new users through your app? Or what about including videos of your product on your marketing page, instead of static JPEGs? Getting carried away is easy — video can become little more than sophisticated blink tags if you’re not careful. But there are plenty of beautiful, inspiring examples of video tightly integrated in a design.

Apple’s new marketing page for the Mac Pro is a stunning example of video reaching out from its cage into the surrounding content. The new Mac Pro is featured in the center of the page, and as you scroll, <strong>it swoops and spins and disassembles itself</strong>. Supporting copy fades in to describe what you are seeing.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8588f28-06e5-439d-9218-8469997c20e8/macpro.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/139078db-0c9b-40c8-8161-e6b15b7231e9/mac-pro-opt.png" /></a><br>
<em>A static screenshot of the new landing page doesn’t do the new Mac Pro justice. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8588f28-06e5-439d-9218-8469997c20e8/macpro.png">larger view</a>)</em>

Another great example of interactive video is Adrian Holovaty’s <a href="https://www.soundslice.com/">Soundslice</a>. Soundslice is filled with YouTube videos of music sliced and diced into tablature (or tabs), which is notation that guitar players use to learn music.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37d2d5c-48ab-4208-a688-0a15dd739d2a/soundslice.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a4144fa-9fde-484a-93f8-3e820f7d8681/soundslice-opt.png" /></a><br>
<em>The musical bars at the bottom stay in sync with the video. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b37d2d5c-48ab-4208-a688-0a15dd739d2a/soundslice.png">larger view</a>)</em>

When you watch a music video, the tabs are animated at the bottom in time with the music, so that you can play along with your guitar. You can even slow down the video or loop selections to practice difficult sections, and the tab animation will stay in sync.</p>

## How Do You Add Video To A Design?

If you venture into video and animation in your next project, you won’t have many resources to lean on for implementation. No canonical, easy-to-use, open-source library for syncing video with animation exists, so every implementation is a bit different. Should you use a JavaScript animation library or pure CSS keyframes and transitions? Should you host the videos yourself and take advantage of HTML5’s <code>video</code> tag events or use YouTube or Vimeo? And then how exactly do you tie animations to a video?

Together, we will explore answers to the above-mentioned questions and more as we build our own micro JavaScript framework. <a href="https://github.com/sfioritto/charlie.js">Charlie.js</a> provides an easy-to-use API for building pages with synchronized video and CSS3 animation.

<a href="https://www.flickr.com/photos/89093669@N00/1535398417/"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cc18d02-2532-4959-8dab-8b47f8019c17/chaplin-skates.jpg" alt="" width="500" height="373" /></a><br>
<em>Charlie.js, named in honor of Charlie Chaplin. (<a href="https://www.flickr.com/photos/89093669@N00/1535398417/">Image source</a>)</em>

The best way to learn is by doing, so let’s dive in.</p>

## What Does Charlie.js Do?

We need a way to create animations and then trigger them at certain moments in a video. We also need to pause the animations if the video stops, and we’ll need a way to handle the user jumping around to different times in the video.

To limit the scope of this article, <strong>we’ll have Charlie.js use only CSS animations</strong>. JavaScript animation libraries are more flexible and powerful than CSS animations, but wrapping one’s head around the straightforward, declarative syntax of keyframes is pretty easy, and the effects are hardware-accelerated. Sticking with only CSS animations is a pretty good choice for small projects.

To keep it simple, Charlie.js will support only one video per page.

As we go through the exercise of building this library, remember that we’re using the framework just to learn about CSS animation and video on the Web. The goal is to learn, not to create production-quality code.</p>

## Define The API

For our little framework, defining the API first makes sense. In other words, we need to figure out how someone would use the library and then write the JavaScript to implement the API.

A video and animation library could work in many ways, but <strong>the main interface puzzle is to figure out how to couple the animation to the video</strong>. How should a developer specify which animations should appear on which elements and at which times they should start in the video?

One option is to suck down the data in JSON or XML. The opposite solution is to have no separate data files and to put all of the configuration into pure JavaScript function calls. Both are fine, but there is a middle road.

Normally, CSS animation is defined in a style sheet. Ideally, that’s where it should be defined for Charlie.js, not in a JSON file. It just makes sense, and doing it this way has advantages. When the animation is in a style sheet, rather than a JavaScript or JSON file, you can test it without loading the entire video and animation library.

The animations are coupled to an element with data attributes. The data attributes define the animation names and also specify the start times.

Let’s say you have a CSS animation named <code>fade</code> for dialing down the opacity, and another named <code>fling</code> for moving elements off the page. And you want a div on the page to use both animations three seconds into the video. Your markup would look like this:

<pre><code class="language-javascript">
&lt;div class="charlie" data-animations="fade, fling" data-times="3, 3"&gt;
...
&lt;/div&gt;
</code></pre>

Charlie.js will see this and know to run the <code>fade</code> and <code>fling</code> animations once the video hits three seconds.

The <code>fade</code> and <code>fling</code> animations are defined in a style sheet that is linked to the document.

Here is what the <code>fade</code> animation might look like (browser prefixes are excluded here but are <a href="https://caniuse.com/css-animation">required for Chrome and Safari</a>):

<pre><code class="language-javascript">
.fade {
    animation-name: fade;
    animation-duration: 3s;
    animation-timing-function: linear;
    animation-iteration-count: 1;
    animation-direction: normal;
    animation-fill-mode: forwards;
}

@keyframes fade {
    0% {
        opacity: 1;
    }

    100% {
        opacity: 0;
    }
}
</code></pre>

The <code>.fade</code> class is what Charlie.js applies to the animated element, which will trigger the <code>fade</code> animation.

## Host The Videos: HTML5 Vs. Flash And Silverlight

With the API out of the way, the next decision is how to host the video. The host will determine what kind of container the video is stuffed into, and the container will determine what is possible with the video.

Video embedded with Flash or Silverlight will limit your design options, so the video-hosting service should ideally support HTML5’s <code>video</code> tag. The <code>video</code> tag is easier to style and move around on the page. You can apply CSS filters and transforms and even use CSS animation on the video itself. Plus, the standard media events are robust and provide plenty of places and ways to hook your code into the video. The big downside of the <code>video</code> tag is compatibility. It doesn’t work in Internet Explorer 8.

What kinds of video-hosting should Charlie.js support? Building a library that supports multiple hosting options is feasible. For example, Popcorn.js (an awesome library for syncing content with video) supports several hosting options and APIs. But <strong>to keep it simple, our little library will support only a vanilla <code>video</code> tag</strong>. Anything in an iframe or Flash container won’t be supported.

That’s nice for Charlie.js, but what if you are stuck supporting old browsers and have to deal with a video stuffed in an iframe? Most video-hosting companies have decent APIs. At the very least, you should be able to use those APIs to sync up your animation — you’ll just be stuck working with an embedded Flash object. YouTube and Vimeo are the most popular services, and both offer extensive APIs. <a href="https://wistia.com/">Wistia</a> is another great option but less well known.

If you want to use a pure <code>video</code> tag but don’t want to host the video yourself, take a look at <a href="https://m.vid.ly/">Vid.ly</a>. Once you upload your video, Vid.ly will encode it in every format you need and give you a universal URL that you can use in your <code>video</code> tag, which will automatically choose the correct video type according to the user agent.

<pre><code class="language-javascript">
&lt;video id="video" src="https://vid.ly/4m4e2n?content=video" controls="" preload="none"&gt;
Your browser does not support the HTML5 video element.
&lt;/video&gt;
</code></pre>

## Heads Up

The JavaScript in most of these snippets uses <a href="https://underscorejs.org/">Underscore</a>; stuff like <code>_.forEach</code> and <code>_.toArray</code> are utility functions from that library. Underscore encourages a functional style of programming that might look strange if you’ve never seen it before, but a little time invested in learning Underscore can save you a lot of time and lines of code. It’s worth checking out. For this article, you’ll find comments in the code to tell you what’s going on, and it should be pretty easy to understand.

One other caveat: The code here will run in most modern browsers, but no attempt has been made to make this completely cross-browser compatible. If your business really needs CSS animation to be synced with video <em>and</em> to run in almost every browser, then this library will not help you out. But for my business, and perhaps for yours, supporting only modern browsers is fine. And even with this restriction, plenty of material here is still worth learning.</p>

## Control CSS Animations With JavaScript

<strong>JavaScript is the glue between video and CSS animation.</strong> There is no way to couple an animation to a video purely with CSS. Animation doesn’t start until a style is applied, and CSS gives you only so many ways to trigger extra styles (such as <code>:hover</code>). In order to sync animation to video, we will need to pause, stop, resume, skip to the middle, and even reverse running animations.

All of this is possible with JavaScript. So, the first step is to get the CSS animation out of the style sheet and into JavaScript. Every CSS animation has two parts. The first part is the keyframe and the properties used to configure how the animation behaves, such as duration, iteration and direction. The second part is what triggers the animation. Charlie.js will need to find both parts in the style sheets.

The first thing we need is a utility function to search through style sheets that are loaded on the page.

<pre><code class="language-javascript">
findRules = function(matches){

        //document.stylesheets is not an array by default.
        // It's a StyleSheetList. toArray converts it to an actual array.
        var styleSheets = _.toArray(document.styleSheets),
        rules = [];

        // forEach iterates through a list, in this case passing
        //every sheet in styleSheets to the next forEach
        _.forEach(styleSheets, function(sheet){

        //This foreach iterates through each rule in the style sheet
        //and checks if it passes the matches function.
        _.forEach(_.toArray(sheet.cssRules), function(rule){
            if (matches(rule)){
                rules.push(rule);
            }
        });
    });
return rules;
}
</code></pre>

The <code>findRules</code> function iterates through every rule of every style sheet and returns a list of rules that match the passed-in <code>matches</code> function. To get all of the keyframe rules, we pass in a function to <code>findRules</code> that checks whether the rule is a keyframe:

<pre><code class="language-javascript">
// A little code to handle prefixed properties
    var KEYFRAMES_RULE = window.CSSRule.KEYFRAMES_RULE
        || window.CSSRule.WEBKIT_KEYFRAMES_RULE
        || window.CSSRule.MOZ_KEYFRAMES_RULE
        || window.CSSRule.O_KEYFRAMES_RULE
        || window.CSSRule.MS_KEYFRAMES_RULE,

        ...

        var keyframeRules = findRules(function(rule){
            return KEYFRAMES_RULE === rule.type;
        }),

        ...
</code></pre>

At this point, we have the keyframes in JavaScript, but we still need the rest of the animation styles that define duration, iterations, direction and so on.

To find all of these classes, <strong>we again use the <code>findRules</code> function</strong> to go through every rule in every style sheet. This time, though, the <code>matches</code> function that we’ll pass in will check to see whether the rule has an <code>animationName</code> property.

<pre><code class="language-javascript">
    ...

    var animationStyleRules = findRules(function(rule){
        return rule.style &amp;&amp; rule.style[animationName(rule.style)];
    });

    ...
</code></pre>

The <code>animationsName</code> function is there to handle the prefixes, because the <code>animationName</code> property still requires prefixes in some browsers. That function looks like this:

<pre><code class="language-javascript">
...

if (style.animationName) {
    name = "animationName"; }
else if (style.webkitAnimationName) {
    name = "webkitAnimationName"; }
else if (style.mozAnimationName) {
    name = "mozAnimationName"; }
else if (style.oAnimationName) {
    name="oAnimationName"; }
else if (style.msAnimationName) {
    name = "msAnimationName"; }
else {
    name = "";
}
return name;

...
</code></pre>

Once the correct prefix has been determined, the name is cached and used for future look-ups.

Once the keyframes and animation styles have been collected, they get stuffed into an instance of a helper class and stored for Charlie.js to use later.

<pre><code class="language-javascript">
var CSSAnimations = function(keyframes, cssRules){
    this.keyframes = keyframes;
    this.cssRules = cssRules;
};
</code></pre>

## Get The Timing Information From The Data Attributes

Timing information is attached to the element that will be animated using a data attribute (remember that we decided this when we were defining the API). So, we need to crawl the document and pull out the information. Any element that will be animated is marked with the class of <code>charlie</code>, which makes it pretty easy to find the data attributes we are looking for.

<pre><code class="language-javascript">
var scrapeAnimationData = function() {

    /* Grab the data from the DOM. */
    var data = {};
    _.forEach(
        //loop through every element that should be animated
        document.getElementsByClassName("charlie"),

        //for each element, pull off the info from the dataset
        function(element) {

            /*
            * Creates an object of animation name: time, e.g.
            *
            * { swoopy: [
            *    { element: domElement,
            *  time: 6522 },
            *    { element: anotherElement,
            *  time: 7834 }]
            * }
            */

            //     var names = element.dataset.animations.split(/s*,s*/),
            times = element.dataset.times.split(/s*,s*/),

            // creates an array of arrays, each one called a "tuple"
            // basically ties the time to the
            // animation name, so it looks like this:
            //[["zippy", 1], ["fade", 2] ... ]
            tuples = _.zip(names, times);

            /*
            * turn the tuples into an object,
            * which is a little easier to work with.
            * We end up with an object that looks like this:
            * {
            *  fade: [ {element: domElement, time: "1.2s"}, ... ],
            *  fling: [ {element: domelement, time: "2.4s"}, ... ]
            * }
            * So, we can reuse an animation on different elements
            * at different times.
            */

            _.forEach(tuples, function(tuple){
                var name = tuple[0],
                time = tuple[1];
                data[name] = data[name] || [];
                data[name].push({
                    element: element,
                    time: time
                })
            });
        });
    return data;
},
</code></pre>

This stores all of the timing information in an object with the animation’s name as the key, followed by a list of times and elements. This object is used to create several <code>Animation</code> objects, which are then stuffed into various data structures to make it easy and fast to look up which animations should be running in the big loop.</p>

## The requestAnimationFrame Loop

The heart of Charlie.js is a loop that runs whenever the video runs. The loop is created with <code>requestAnimationFrame</code>.

<pre><code class="language-javascript">
tick: function(time){
    if (this.running){
        this.frameID = requestAnimationFrame(this.tick.bind(this));
        this.controller.startAnimations(time, video.currentTime);
    }
}
</code></pre>

The <code>requestAnimationFrame</code> function is specifically <strong>designed to optimize any kind of animation</strong>, such as DOM manipulations, painting to the canvas, and WebGL. It’s a tighter loop than anything you can get with <code>setTimeout</code>, and it’s calibrated to bundle animation steps into a single reflow, thus performing better. It’s also better for battery usage and will completely stop running when the user switches tabs.

The loop starts when the video starts and stops when the video stops. Charlie.js also needs to know whether the video ends or jumps to the middle somewhere. Each of those events requires a slightly different response.

<pre><code class="language-javascript">
video.addEventListener("play", this.start.bind(this), false);
video.addEventListener("ended", this.ended.bind(this), false);
video.addEventListener("pause", this.stop.bind(this), false);
video.addEventListener("seeked", this.seeked.bind(this), false);
</code></pre>

As the video plays, the loop keeps ticking. Each tick runs this code:

<pre><code class="language-javascript">
// allow precision to one tenth of a second
var seconds = roundTime(videoTime),
me = this;

//resume any paused animations
me.resumeAnimations();

/* start up any animations that should be running at this second.
* Don't start any that are already running
*/

if (me.bySeconds[seconds]){
    var animations = me.bySeconds[seconds],
    notRunning = _.filter(animations, function(animation){
        return !_.contains(me.running, animation);
    });

    /* requestAnimationFrame happens more than
    *  every tenth of a second, so this code will run
    *  multiple times for each animation starting time
    */

    _.forEach(notRunning, function(animation){
        animation.start();
        me.running.push(animation);
    });
}
</code></pre>

Everything we have done up to this point has been to support these few lines of code. The <code>seconds</code> variable is just the <code>video.currentTime</code> value rounded to the nearest tenth of a second. The <code>bySeconds</code> property is created from the time data that is scraped from the HTML — it’s just a quick way to grab a list of animations to start at a given time. The <code>running</code> array is a list of animations that are currently running. The <code>requestAnimationFrame</code> loop is really fast and runs many, many times a second, and Charlie.js only supports a resolution of one tenth of a second.

So, if one animation starts at the 2-second mark, then <code>requestAnimationFrame</code> will try to start it several times until the video has progressed to the next tenth of a second. To <strong>prevent animations from starting over and over again</strong> during that tenth of a second, they get put into the <code>running</code> array so that we know what is running and don’t start it again unnecessarily.

To start a CSS animation, just add the animation properties to an element’s style. The easiest way to do this is to just add the animation class to the element’s <code>classList</code>, and that is exactly what the animation’s <code>start</code> method does.

<pre><code class="language-javascript">
start: function(){
    var me = this;
    //The name of the animation is the same as the class name by convention.
    me.element.classList.add(me.name);
    onAnimationEnd(me.element, function(){
        me.reset();
    });
}
</code></pre>

The name of the animation is the same as the class name by convention.</p>

## Pause And Resume Animations

When the video stops, the animations should stop with it. There is a pretty straightforward way to do this using CSS animations: We just set the <code>animationPlayState</code> property of the element to <code>paused</code>.

<pre><code class="language-javascript">
...

//method on the animation object
pause: function(){
    this.element.style.webkitAnimationPlayState = "paused";
    this.element.style.mozAnimationPlayState = "paused";
    this.element.style.oAnimationPlayState = "paused";
    this.element.style.animationPlayState = "paused";
},

resume: function(){
    this.element.style.webkitAnimationPlayState = "running";
    this.element.style.mozAnimationPlayState = "running";
    this.element.style.oAnimationPlayState = "running";
    this.element.style.animationPlayState = "running";
}

...

//called on the video "pause" event
while(animation = me.running.pop()){
    animation.pause();
    //keep track of paused animations so we can resume them later ...
    me.paused.push(animation);
}
</code></pre>

The only trick here is to keep track of which animations have been paused, so that they can resume once the video starts again, like so:

<pre><code class="language-javascript">
while (animation = me.paused.pop()){
    animation.resume();
    me.running.push(animation);
}
</code></pre>

## How To Start An Animation In The Middle

What if someone skips ahead in the video and jumps right into the middle of an animation? How do you start a CSS animation in the middle? The <code>animationDelay</code> property is exactly what we need. Normally, <code>animationDelay</code> is set to a positive number. If you want an animation to start three seconds after the animation style has been applied, then you’d set <code>animationDelay</code> to <code>3s</code>. But if you set <code>animationDelay</code> to a negative number, then it will jump to the middle of the animation. For example, if an animation lasts three seconds, and you want the animation to start two seconds in, then set the <code>animationDelay</code> property to <code>-2s</code>.

Whenever a user scrubs to the middle of the video, Charlie.js will need to stop all of the animations that are currently running, figure out what should be running, and then set the appropriate <code>animationDelay</code> values. Here is the high-level code:

<pre><code class="language-javascript">
// 1. go through each to start
// 2. set the animation delay so that it starts at the right spot
// 3. start 'em up.

var me = this,
seconds = roundTime(videoTime),
toStart = animationsToStart(me, seconds);

// go through each animation to start
_.forEach(toStart, function(animation){

    //set the delay to start the animation at the right place
    setDelay(animation, seconds);

    //start it up
    animation.start();

    /* If the move is playing right now, then let the animation
    * keep playing. Otherwise, pause the animation until
    * the video resumes.
    */

    if (playNow) {
    me.running.push(animation);

    } else {
        me.paused.push(animation);
        animation.pause();
    }
});
</code></pre>

The <code>animationsToStart</code> function loops through a sorted list of animations and looks for anything that should be running. If the end time is greater than the current time and the start time is less than the current time, then the animation should be started.

<pre><code class="language-javascript">
var animationsToStart = function(me, seconds) {

    var toStart = [];

    for(var i = 0; i &lt; me.timeModel.length; i++) {

        var animation = me.timeModel[i];

        //stop looking, nothing else is running
        if (animation.startsAt &gt; seconds) {
            break;
        }

        if (animation.endsAt &gt; seconds) {
            toStart.push(animation);
        }
    }
    return toStart;
};
</code></pre>

The <code>timeModel</code> is a list of animations sorted by the times when the animations should end. This code loops through that list and looks for animations that start before the current time and end after the current time. The <code>toStart</code> array represents all of the animations that should be running right now.

Those values get passed up to the higher-level code, which then computes and sets the delay in the <code>setDelay</code> function.

<pre><code class="language-javascript">
setDelay = function(animation, seconds) {
    var delay = -(seconds - animation.startsAt);
    delay = delay &lt; 0 ? delay : 0,
    milliseconds = Math.floor(delay * 1000) + "ms";
    animation.element.style.webkitAnimationDelay = milliseconds;
    animation.element.style.mozAnimationDelay = milliseconds;
    animation.element.style.oAnimationDelay = milliseconds;
    animation.element.style.msAnimationDelay = milliseconds;
    animation.element.style.animationDelay = milliseconds;
};
</code></pre>

The <code>seconds</code> parameter is the current time in the video. Let’s say that the video is at 30 seconds, that the animation starts at 24 seconds and that it lasts for 10 seconds. If we set the delay to <code>-6s</code>, then it will start the animation 6 seconds in and will last another 4 seconds.</p>

## Look At The Code For Yourself

We’ve covered here how to use <code>requestAnimationFrame</code> to create a tight, optimized loop for animations, how to scrape keyframes and animation styles from the style sheet, how to start and stop animations with the video, and even how to start CSS animations in the middle. But to get to the point, we’ve skipped over quite a bit of glue code. Charlie.js is only a couple of hundred lines of code, and it is open source and commented thoroughly. You are welcome to <a href="https://github.com/sfioritto/charlie.js">grab the code</a> and read it.

You can even use it if you want, with a few caveats:

*   Charlie.js was made for educational purposes. It was made to be read and for you to learn about CSS animations, videos, `requestAnimationFrame`, etc. Don’t just plug it into your production code unless you really know what you are doing.
*   Cross-browser support for animation is pretty good, and Charlie.js tries to be friendly to all the browsers when it can be. However, it hasn’t been heavily tested.
*   It eats up CPU, even if the video is paused. (This has something to do with CSS animations still rendering.)
*   The user can’t drag the seek bar while the video is unpaused. If they do, then the animations will start and overlap each other.
*   Charlie.js does not respond to changes in frame rate. So, if the video stutters or you want to slow down the rate of the video, then the animations will fall out of sync. Also, you can’t run video backwards.
*   Animations won’t start if the current tab isn’t set to the video, due to `requestAnimationFrame` not running unless the video tab is active. This could confuse users who switch back and forth between tabs.

Some of these limitations can be fixed pretty easily, but Charlie.js was made for a very limited use case. I’ve put together a demo of Charlie.js in action so that you can see what it can do.

<strong>The future of video in Web design is filled with possibilities</strong>, and I for one can’t wait to see what happens.</p>

### Additional Resources

*   [A demo of Charlie.js](https://www.sketchingwithcss.com/flexbox/) See what you can do with video and CSS3 animation.
*   “[CSS3 Animation,](https://caniuse.com/css-animation)” Can I Use…
*   “[How Does the New Mac Pro Site Work](https://www.planningforaliens.com/blog/2013/06/11/mac-pro/),” Sean Fioritto
*   “[Syncing Content With HTML5 Video](https://www.smashingmagazine.com/2011/03/11/syncing-content-with-html5-video/),” Christian Heilmann, Smashing Magazine
*   “[Controlling CSS Animations and Transitions With JavaScript](https://css-tricks.com/controlling-css-animations-transitions-Javascript/),” CSS-Tricks
*   “[Adrian Holovaty’s Talks SoundSlice](https://vimeo.com/59193899)” (video), 37signals
*   “[100 Riffs: A Brief History of Rock n’ Roll](https://www.soundslice.com/tabs/1366/100-riffs-a-brief-history-of-rock-n-roll-tab/),” Soundslice An amazing demonstration of Soundslice
*   “[HTML5 Video With Filters and SVG](https://youtube.com/watch?v=q7BjhX3K-5w)” (video), idibidiart
*   “[requestAnimationFrame for Smart Animating](https://www.paulirish.com/2011/requestanimationframe-for-smart-animating/),” Paul Irish

{{< signature "al, ea, il" >}}

