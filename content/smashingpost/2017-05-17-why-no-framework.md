---
title: “Why We Didn’t Use A Framework” (Case Study)
slug: why-no-framework
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c7cd5f-265e-4cbd-9d1e-d7ee2de87382/dashboard-preview-500w-opt.png
date: 2017-05-17T20:13:08.000Z
author: nick-gauthier
description: >-
  When we set out to build MeetSpace (a video conferencing app for distributed
  teams), we had a familiar decision to make: What's our tech stack going to be?
  We gathered our requirements, reviewed our team's skillset and ultimately
  decided to use vanilla JavaScript and to avoid a front-end framework.

  Using this approach, we were able to create an incredibly fast and light web
  application that is also less work to maintain over time. The average page
  load on MeetSpace has just **1** uncached request and is **2 KB** to download,
  and the page is ready within **200 milliseconds**. Let's take a look at what
  went into this decision and how we achieved these results.
categories:
  - Coding
  - Frameworks
  - Case Studies
---
Using this approach, we were able to create an incredibly fast and light web application that is also less work to maintain over time. The average page load on <a href="https://www.meetspaceapp.com">MeetSpace</a> has just <strong>1</strong> uncached request and is <strong>2 KB</strong> to download, and the page is ready within <strong>200 milliseconds</strong>. Let's take a look at what went into this decision and how we achieved these results.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Adapting To A Responsive Design](https://www.smashingmagazine.com/2013/06/adapting-to-a-responsive-design-case-study/)
*   [Using Sketch For Responsive Web Design](https://www.smashingmagazine.com/2015/04/using-sketch-for-responsive-web-design-case-study/)
*   [Is App Indexing For Google Worth The Effort?](https://www.smashingmagazine.com/2017/01/case-study-app-indexing-google-worth-the-effort/)
*   [Lessons Learned In Big App Development (Hawaiian Airlines Example)](https://www.smashingmagazine.com/2015/12/lessons-learned-in-big-app-development-hawaiian-airlines/)

## Requirement: Be Better

The most important requirement for the entire business was to build a better video conferencing tool. Many video conferencing solutions are out there, and they all suffer from really similar problems: reliability, connectivity, call quality, <a href="https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/">speed</a> and ease of use. From our initial surveys, it was very clear that the most important problem for us to solve was to have flawless audio with low delay, high fidelity and high reliability.

{{% feature-panel %}}

We also found that the vast majority of our users (95% of those surveyed) were happy to use Chrome if it "delivered a superior video conferencing experience." This meant we could <strong>use cutting-edge WebRTC technology to achieve our goals</strong> without having to launch on multiple native platforms, which would have been significantly more work. We decided to target Chrome and Firefox because of their WebRTC support, and we have our eye on Safari and Edge for the future.
According to our technical experiments, the best way to achieve high-quality reliable audio is to keep the app's CPU and the network usage very low. This way, whenever traffic spikes on the network, there's room to spare and the call doesn't drop or stutter. This meant we needed to make our application very lightweight and very fast, so that it doesn't take up any more of the CPU or network than necessary, and so that it is very fast to reload if things go wrong.

This was a big point in favor of using vanilla JavaScript and not a large framework. We needed to have a lot of control over the weight of the application, as well as its boot speed and idle CPU usage (changing elements, repaints, etc). This is a particularly low-level requirement that not many applications share. Many app vendors today aim to be better via superior UI and UX, more features and greater ease of use.

In our case, we needed <strong>100% control over the UX of the video call</strong> to ensure that it was as light as possible and that we could maximally use whatever resources we had available to give priority to the call. As a bonus, this has the effect of not turning our users' laptops into attack helicopters when their fans kick up to the max.

While I'd love to go into depth about how we did this with WebRTC, that's a bit outside the scope of this article. However, I wrote an article about <a href="https://webrtchacks.com/limit-webrtc-bandwidth-sdp/">tuning WebRTC bandwidth by modifying the SDP payload</a>, which you can read if you'd like some details.</p>

## Small To Medium UX Needs

Next, we created rough designs for all of the pages we needed and took an inventory of the interactions we'd have on those pages. They ranged from small to medium interactions, with two pages being the most complicated. Let's look at a few.</p>

### Small: Link Copy

We had a lot of very small interactions. One example is a button to copy a link:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9d820d6-724a-430e-913c-e79962dc3d26/link-copy-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9d820d6-724a-430e-913c-e79962dc3d26/link-copy-preview-opt.png" alt="" width="402" height="" /></a><figcaption>Input element with URL and button to copy the link</figcaption></figure>

Here we have a simple <code>&lt;input&gt;</code> element with a "Copy" button that, when clicked, copies the link. For these kinds of interactions, we could use a very common style: a progressive enhancement pattern inspired by jQuery's plugins. On page load, we scan for a particular selector representing the component and enhance it with click-to-copy functionality. It's so simple that we can share the entire plugin here:

<pre><code class="language-html">&lt;form data-copy=true&gt;
  &lt;input type="text" value="{url}" data-click-select-all /&gt;
  &lt;input type="submit" value="Copy" /&gt;
&lt;/form&gt;</code></pre>

<pre><code class="language-javascript">// Copy component
(function() {
 window.addEventListener("load", function() {
   var els = document.querySelectorAll("[data-copy]");
   for(var i = 0; i &lt; els.length; i++) {
     var el = els[i];
     el.addEventListener("submit", function(event) {
       event.preventDefault();
       var text = event.target.querySelector('input[type="text"]').select();
       document.execCommand("copy");
     });
   }
 });
}());
// Select all component
(function() {
 window.addEventListener("load", function() {
   var els = document.querySelectorAll("[data-click-select-all]");
   for(var i = 0; i &lt; els.length; i++) {
     var el = els[i];
     el.addEventListener("click", function(event) {
       event.target.select();
     });
   }
 });
}());</code></pre>

This component is actually made up of two different components: the <code>copy</code> component and the <code>select-all</code> component. The <code>select-all</code> component enhances an input by selecting the contents on click. This way, a user can click the input area, then hit <code>Control/Command + C</code> to copy on their own. Or, with the <code>copy</code> component, when the "Copy" button is clicked (triggering a form submission), we intercept the submission and copy the contents.

These interactions were so small that we decided that small vanilla components would be the simplest, fastest and clearest way to achieve the functionality. At the time of writing, we have about 15 of these small components throughout the app.</p>

### Medium: Dashboard and Chat Pages

We identified two pages in the app with larger UX needs. This is where we weren't sure if we wanted to use vanilla JavaScript, a small library or a large framework. First, we looked at our dashboard:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236ad34a-d2ed-471e-9d94-246f98bb71bb/dashboard-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/236ad34a-d2ed-471e-9d94-246f98bb71bb/dashboard-preview-opt.png" alt="Dashboard" width="660" height="360" /></a><figcaption>The Meetspace dashboard</figcaption></figure>

On this page, the main dynamic part is the portraits inside the rooms. We wanted to have live feedback on who is in each room, and so we use WebSockets to push participant information to all clients in the dashboard when someone joins or leaves a room. Then we have to add that person's portrait inside the room. We decided that we'd be fine taking a simple approach here by pushing all participants down the socket for each room upon any change, then clearing out the room and rendering all participants fresh each time. The HTML was so simple that we didn't need to use templates — just a few <code>div</code>s and an <code>img</code> tag. The most complicated part was some dynamic sizing. We knew at the beginning we could get away with vanilla JavaScript here.

WebSockets ended up being quite easy to implement without a framework. Here's the basic scaffold for our WebSocket interactions:

<pre><code class="language-javascript">Dashboard.prototype = {
   connect: function() {
     this.socket = new WebSocket("/path/to/endpoint");
     this.socket.onmessage = this.onSocketMessage.bind(this);
     this.socket.onclose = this.onSocketClose.bind(this);
   },
   onSocketMessage: function(event) {
     var data = JSON.parse(event.data);
     switch (data.type) {
       case "heartbeat": console.log("heartbeat", this.roomID); break
       case "participants": this.participants(JSON.parse(data.data)); break
       default: console.log("unknown message", this.roomID, data);
     }
   },
   onSocketClose: function() {
     console.log("close", this.roomID);
     setTimeout(this.connect.bind(this), 1000);
   },
  // …
}</code></pre>

We initialize the socket when we construct the <code>Dashboard</code> instance, with a URL to our endpoint. Our messages are all in the format <code>{type: "type", data: { /* dynamic */ }}</code>. So, when we receive a message, we parse the JSON and switch on the type. Then we call the appropriate method and pass in the data. When the socket closes, we attempt a reconnection after waiting a second, which keeps us connected if the user's Internet stutters or if our servers have rebooted (for a deployment).

Next, we got to the largest page in the app, the video chat room:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02b0105a-431e-407b-b5c9-631ba73ca5c6/chat-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b59249ad-4523-4680-b9b0-11e70b650b62/chat-780w-opt.png" alt="Video chat" width="780" height="519" /></a><figcaption>MeetSpace's video chat page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02b0105a-431e-407b-b5c9-631ba73ca5c6/chat-large-opt.png">View large version</a>)</figcaption></figure>

Here we had numerous challenges:

*   people joining and leaving,
*   people muting and unmuting,
*   people turning the video on and off,
*   a custom "borderless" layout for varying numbers of participants (not possible with pure CSS),
*   WebRTC video capture and peer-to-peer streaming,
*   synchronization of all of the above across all clients through WebSockets.

For this page, we were really on the fence. We knew we'd be doing only a small amount of DOM manipulation (just adding simple elements for each participant), but the amount of WebSockets and WebRTC synchronization was a bit daunting.

We decided that we could handle the DOM and WebSocket events, but that we wanted some help on WebRTC, mainly because of cross-browser differences (WebRTC hasn't fully settled down). We opted to use the official WebRTC <code>adapter.js</code> because we had a lot of confidence in a first-party solution (and it's in use quite broadly). Additionally, it's a shim, so we didn't have to learn much to be able to use it, and its implementation is pretty simple (we knew we'd end up reading through a lot of it).

## Hypothesis: Less Code = Less Work

In addition to all the research we did ahead of time, we also had a hypothesis that we were very interested in testing: Could using less code (from others and including our own) and implementing from scratch result in less total work?
Our guess here was that the answer is yes when it comes to small to medium workloads. We knew that we had only a handful of pages and a handful of UX experiences, so we decided to take a risk and go without a lot of dependencies.

We'd all used (and enjoyed) many different frameworks in the past, but there's always a tradeoff. When you use a framework, you have the following costs:

*   learning it,
*   customizing it to fit your needs (i.e. using it),
*   maintaining it over time (upgrades),
*   diving deep when there are bugs (you have to crack it open eventually).

Alternatively, working from scratch has the opposite costs:

*   building it (instead of learning and customizing),
*   refactoring (instead of customizing),
*   solving bugs the first time (which others have already found and fixed in their respective frameworks).

We guessed that, because we fell in the medium area of the spectrum, working from scratch would be less work in total — more work in the beginning (but less confusion and learning), a bit more of our own code in total, less code overall (if you count dependencies), easy-to-fix bugs (because we don't have to dig deep) and generally much less maintenance.</p>

## The Result

MeetSpace has been around for a year now, and we have been surprisingly stable and reliable! I mean, I guess I shouldn't say "surprised," but honestly, I thought that coding it vanilla would cause more problems than it did. In fact, having full error traces and no frameworks to dig through makes debugging much easier, and less code overall means less problems. Another "fun" benefit is that when anything goes wrong, we immediately know it is our own fault. We don't have to troubleshoot to determine where the bug is. It is definitely our code. And we fix it fast because we are quite familiar with our code.

If you look at our commit graph, you can see we had a lot of work at the beginning, but then over time we've had only large spikes coinciding with features:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b94188cc-0456-4a87-836e-9f74b1f52261/commits-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/862272e5-6d69-49c6-86cf-8d51b67f20ac/commits-780-opt.png" alt="Commit graph" width="780" height="103" /></a><figcaption>MeetSpace's code commits over time (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b94188cc-0456-4a87-836e-9f74b1f52261/commits-large-opt.png">View large version</a>)</figcaption></figure>

We've never had any big refactorings or upgrades. The few times we did upgrade our libraries, nothing went wrong, because the updates were small and didn't break the libraries' APIs. It's hard to compare with how much work it would have been had we used a framework, so the best we can do is to compare with past projects. My gut feeling is that, had we used a framework, more time would have been spent in total because of extra time spent learning the framework, tracking bugs through framework code and doing upgrades across framework versions. The best we can say about this project is that, over time, tracking down bugs and performing upgrades has been very little work.

Now, let's get to the gory details: speed and size. For this section, I'll talk about three pages: sign-in, dashboard and chat. Sign-in is the absolute lightest page, because it's just a form and there's no user context. Dashboard is our heaviest page that is mostly static. Chat is our heaviest page with the most action on it.</p>

<em>Bootstrap 4Foundation for Sites 6UIkit 3Current version, release date4.0.0-alpha 6, released January 20176.3.0, released January 20173.00 beta 9, released February 2017.</em>

PageCold # requestsCold KBCold loadWarm # requestsWarm KBWarm load
<table class="tablesaw">
<thead>
<tr>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>Sign-in</td>
<td>13</td>
<td>87.2</td>
<td>253 ms</td>
<td>1</td>
<td>1.1</td>
<td>97 ms</td>
</tr>
<tr>
<td>Dashboard</td>
<td>23</td>
<td>210</td>
<td>318 ms</td>
<td>1</td>
<td>2.0</td>
<td>80 ms</td>
</tr>
<tr>
<td>Chat</td>
<td>13</td>
<td>202</td>
<td>321 ms</td>
<td>1</td>
<td>1.8</td>
<td>182 ms</td>
</tr>
</tbody>
</table>
<em>"Cold" refers to the initial visit, when the cache is empty; "warm" refers to subsequent visits, when cached files can be used.</em>

All our JavaScript, CSS and images are fully cached, so after the first cold load, the only request and transfer being performed is the HTML of the page. There are zero other requests — no other libraries, templates, analytics, metrics, nothing. With every page clocking in at about 100 milliseconds from click to loaded, the website feels as fast as a <a href="https://www.smashingmagazine.com/2015/12/reimagining-single-page-applications-progressive-enhancement/">single-page application</a>, but without anywhere nearly as much complexity. We set our <code>Cache-Control</code> headers far into the future to fully cache our assets. Ilya Grigorik has written a great <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching">article on HTTP caching</a>.

The majority of the page load is for waiting on the server to process the request, render and send the HTML. And I'm sure you're not surprised to hear that our back end is also almost entirely vanilla and frameworkless; built with Go, it's got an average median response time of 8.7 milliseconds.</p>

<strong>Please note</strong>: This article and the benchmarks here are for MeetSpace's inner application, not our marketing website. So, if you go to MeetSpace's website, you'll have to click "Sign in" to reach the main application, where these improvements reside. The main <code>www</code> site has a different architecture.</p>

## Would We Do It Again?

For MeetSpace? Definitely. What about other projects? I think that all of the research we did ahead of time, our hypothesis on cost and our results point to a pretty simple tradeoff based on one broad metric: complexity.

The simpler, smaller and lighter an application is, the cheaper and easier it will be to write from scratch. As complexity and size (of your application and of your team and organization) grow, so does the likelihood that you'll need a bigger base to build on. You'll see stronger gains from using a standard framework across a large application, as well as from using the common language of that framework across a large team.

At the end of the day, your job as a developer is to make the tough tradeoff decisions, but that's my favorite part!

### Related Links

*   [MeetSpace](https://www.meetspaceapp.com)
*   "[How to Create a Basic Plugin](https://learn.jquery.com/plugins/basic-plugin-creation/)," jQuery
*   "[Document.execCommand()](https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand)," Mozilla Developer Network
*   "[WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)," Mozilla Developer Network
*   "[WebRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API)," Mozilla Developer Network

{{< signature "da, vf, yk, al, il" >}}

