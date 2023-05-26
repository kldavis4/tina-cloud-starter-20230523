---
title: 'Optimizing Video For Size And Quality'
slug: optimizing-video-size-quality
author: doug-sillars
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/658beacf-da53-4624-bbab-418fdb4c7ed8/optimizing-video-size-quality.jpg
date: 2021-02-15T15:00:00.000Z
summary: >-
  Adding video to your application can increase customer engagement and satisfaction. But the exact opposite can occur when there are issues with the video playback: video stalls are frustrating and drive customers away. In this article, we’ll walk through the steps to optimize the video on your website to ensure fast playback and reduce stalls.
description: >-
  Adding video to your application can increase customer engagement and satisfaction. But the exact opposite can occur when there are issues with the video playback: video stalls are frustrating and drive customers away. In this article, we’ll walk through the steps to optimize the video on your website to ensure fast playback and reduce stalls.
categories:
  - Performance
  - Optimization
  - Tools
  - Videos
  - Guides
---

Over the last few years, more and more projects are using video as an integral part of the application.  This is a great direction, as videos are more engaging than still photos ([videos can double conversion rate](https://www.brafton.com/blog/video-marketing/results-videos-make-websites-2x-engaging/) and [increase time spent on site](https://www.forbes.com/sites/amitchowdhry/2018/09/18/study-relevant-video-content-drives-more-engagement-and-revenue/)), and as such, can really draw customers to explore details about products and services. However, it all goes sideways when there are issues related to the video playback.

**Video playback issues** are directly related to the size and bitrate of the video.  A video with large dimensions or a high bitrate will take longer to download and will require a higher speed network to play back smoothly.  This leads to longer startup times, and if the network cannot supply the video fast enough, the video will stall during video playback.

There is a solution though! By running basic optimizations of our videos before adding them to our websites, we can prevent these issues from occurring for good &mdash; well, most of them. All we really need to do is make the file smaller &mdash; in one way or another. So, now the trick is: how do we make the file smaller without reducing quality?

In this article, we’ll walk through the tools and some of the steps you can take to **optimize your videos for playback** &mdash; all of it to avoid stalls and impress your precious customers!

## Real-World Data

It’s not uncommon to find websites with extremely large videos — for example, used used as hero background videos. In my research, I was looking into sites found in the [December 2020 mobile HTTPArchive](https://mobile.httparchive.org/interesting.php), and it wasn’t difficult to spot a good number of sites loading *huge* video files by default, both on mobile and on desktop.

It’s of course doubtful that you will be able to achieve the same savings that I’ll be showing here, but you will get some useful pointers and tips on things to keep in mind when dealing with videos. In fact, it is very easy to accidentally place **extremely large videos** on your website if you are not careful, resulting in them being almost unusable for most of your customers.

{{% feature-panel %}}

## The Pumpkin Patch Story

Imagine that it’s mid-October, and you’re looking for a pumpkin patch and a corn maze to spend a weekend afternoon with your family. In the comfort of your desktop machine, you search the web for a nearby location and find the perfect one. The website looks lovely, with a beautiful **drone 4K video** of the fields playing at the top of the page. You pick the URL and send it to yourself and your loved ones so that you together can continue exploring this option on the go.

But when you open the page on your phone, you notice a glitch: the video is desperately trying to play on your phone, but unfortunately fails to do so. The video keeps **stalling and restarting over and over**, being much more disruptive and annoying than it was on your computer. Eventually you move on, bookmark the URL, and move on with your daily routine.

After a fun muddy day (well, I have recently lived in Seattle and the UK, so pumpkin patches are muddy), you’re back on your computer: perhaps you think yet again about that video and you wonder why it wasn’t playing well on your phone. Well, let’s diagnose what is going on.

You might start by opening DevTools in your browser. Once the page is loaded, we can move to the Network tab, and filter by “media” to see all the video files:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e80079f7-c6b2-4308-b072-40cb3e499bcf/2-optimizing-video-size-quality.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e80079f7-c6b2-4308-b072-40cb3e499bcf/2-optimizing-video-size-quality.png" width="800" height="374" sizes="100vw" caption="Filtering resources by 'Media' in DevTools. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e80079f7-c6b2-4308-b072-40cb3e499bcf/2-optimizing-video-size-quality.png'>Large preview</a>)" alt="" >}}

We see that an MP4 file is being downloaded. The file doesn’t come through the network as a standalone file; rather, the streaming service must be breaking up the file into a few **segments**, so you might see several `206` (partial content) requests for the same file.

Looking at the **response headers** for this file, we can spot some details:

<div class="break-out">
 <pre class="language-bash"><code>accept-ranges: bytes
access-control-allow-headers: x-test-header, Origin, X-Requested-With, Content-Type, Accept
access-control-allow-methods: GET, POST, PUT, DELETE, OPTIONS
Content-Length: 87690242
Content-Range: bytes 70025216-157715457/157715458
content-type: video/mp4
date: Fri, 22 Jan 2021 15:27:26 GMT
last-modified: Mon, 24 Jun 2019 05:13:04 GMT
server: Apache
</code></pre>
</div>

Now, some of these numbers are slightly scare as they are slightly large. In fact, they are often so large that I’ve found myself getting into the habit of adding commas, so I can get an idea of how large the files actually are. In this case, the partial download is 87 MB, and the entire file is 157,715,457 bytes. Yes, that’s right, this video is 157MB, and it (tried) to load on my phone earlier today! No wonder it didn’t succeed.

### So What’s Up With This Video?

Let’s dive a little bit deeper. Apparently, the video is way too large to play smoothly on a mobile phone with a lower memory and a slower network. But what do we need to fix it? To figure out what exactly is the problem, we can use [FFMPEG](https://ffmpeg.org/), which is open source and free, and proves to be one of the most **reliable tools to optimize videos**. We could endlessly tweak the configuration in FFMPEG, but let’s just touch on a few important ones in this article.

So, let’s start with the diagnosis tool called [FFprobe](https://ffmpeg.org/ffprobe.html). FFprobe gathers information from multimedia streams, and provides you with the details about how the video is encoded and how it will play. It’s a part of the FFMPEG package, and actually quite easy to use.

Even better: if your video is online already, there is an [online version of ffprobe](https://ffprobe.a.video) that we can jump to right away. So, let’s just enter the URL into the form, and get the details about the video in return (e.g. video dimensions, bitrate, and quite a bit of metadata).

When I add the MP4 URL from the pumpkin farm, we immediately see one of the issues. The `show_format` response from ffprobe returns a summary: apparently, there are 2 streams, and it’s 62s long (which all sounds normal enough to not raise any suspicions). But when we get to the **size and bitrate**, we immediately see where the video is failing.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74e9aa75-9955-41c9-a42e-674663be44be/3-optimizing-video-size-quality.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74e9aa75-9955-41c9-a42e-674663be44be/3-optimizing-video-size-quality.png" width="800" height="743" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74e9aa75-9955-41c9-a42e-674663be44be/3-optimizing-video-size-quality.png'>Large preview</a>)" alt="" >}}

As mentioned above, it might be a good idea to get used to adding commas to these large numbers. As it turns out, indeed the drone footage flying over the field is 157MB, and has a bitrate of 20 MB per second! It means that for the video to play seamlessly, the network must be able to **stream the video** at a rate faster than 20 MBPS, which is exactly why it was stalling on the phone.

### What is the ideal playback bitrate?

To avoid stall, we need to **stream the video at an appropriate rate**. That’s where bitrate becomes important. Bitrate is the playback speed of the video. For the browser to play the video smoothly, the video has to be downloading faster than it plays back &mdash; meaning that the video will only play back smoothly if the network speed is over 20 MBPS. When I think of network speeds, I tend to rely on [WebPageTest](https://webpagetest.org/)’s traffic profiles:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b23405-7c5d-4741-8822-7436f2a46f66/1-optimizing-video-size-quality.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b23405-7c5d-4741-8822-7436f2a46f66/1-optimizing-video-size-quality.png" width="800" height="438" sizes="100vw" caption="Traffic profiles to keep in mind on <a href='https://webpagetest.org/'>WebPageTest</a>: ranging from Cable and DSL to 3G Slow and 2G. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b23405-7c5d-4741-8822-7436f2a46f66/1-optimizing-video-size-quality.png'>Large preview</a>)" alt="" >}}

As we can tell from the overview abouve, the video *might* play well on the “Native Connection”, and on the ultra-fast optic cable FIOS connection (20 MBPS is exactly the speed required, so hopefully nothing else needs to be downloaded in the background). However, all the other connections have a downlink speed that’s **significantly lower than 20 MBPS**. If the video is loading at these speeds, the player will attempt to consume the video faster than it can be downloaded, and the video will permanently stall.

The bitrate of your video sets the minimum network speed that your customers can use. In general, **the bitrate of your video should be about 80%** of the available throughput on the network. So a 20 MBPS video really needs 24 MBPS network throughput to play the video seamlessly. Everyone on a slower connection will have a quite poor experience and is likely to not be able to watch the video at all. More specifically, this means that for us to play smoothly and silky on 4G, the bitrate has to stay **below 7.2 MBPS**.

### Can We Lower This Video’s Bitrate?

Yes! Let’s look at some of the [configurations](https://github.com/chgeuer/mybookmarks/blob/master/ffmpeg%20recipes.md) we can use to reduce this video’s bitrate. But first, let’s look at the data we get from FFprobe. One thing that is quite noticeable is the `r_frame_rate` value, which is the number of frames per second in the video. Its value is 60000&#47;1001. It means that the frame rate for the video is 60 frames per second. However, typical frame rates on the web are 25–30, so the first thing we can do is to **re-encode the video with a lower bitrate**.

Another thing to keep in mind is *Constant Rate Factor*. In FFMPEG, the principal quality/size benchmark is the Constant Rate Factor (CRF) compression, with values ranging from `0` (no compression) to `50` (high compression). The default value for CRF in FFMPEG is `23` (if you leave out the CRF parameter, your video is with that value). In my personal experience, values from 23-28 still produce **high-quality videos**, looking good on the web and greatly reduced in file size.

So let’s start at 30fps and a CRF of `23`. The Terminal command will look like this:

<div class="break-out">

 <pre><code class="language-bash">ffmpeg -i input.mp4 -vcodec h264 -acodec aac -crf 23 -strict -2 :v fps=fps=30 output.mp4
</code></pre>
</div>

*Voilà!* This results in an 81.5 MB video &mdash; already a 48% improvement. But the video is still very large, with a 10 MBPS bitrate. If we set CRF to 28, the file drops to 35.4MB, with a bitrate of 4.5 MBPS which is much more likely to play well on a 4G connection.

This is **a five-time improvement over the original video**. To make this video even more accessible, we can resize the video to make it smaller. That’s something we’ll discuss in the streaming section below.

{{% ad-panel-leaderboard %}}

## The Hungry For Pizza Story

Imagine that you’re in Los Angeles, perhaps visiting from abroad and roaming on your phone, and of course thinking about grabbing a slice of pizza. You find a remarkable pizza place on your phone, and decide to head there. You may have noticed a few videos and hero images on the page, but really, every pizza place kind of looks the same, so you didn’t bother to watch the video. You head and grab a slice or two before heading back to your hotel.

That night, you get a text from your carrier that you used a lot more data than you imagined (and definitely way more than you originally planned!). A couple of cabs, and the pizza website &mdash; how expensive was the pizza website again?

You pop the pizza website into [WebPageTest](https://webpagetest.org/) and check it on a mobile connection:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92509910-4e29-4e32-86b4-891ca630450f/4-optimizing-video-size-quality.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92509910-4e29-4e32-86b4-891ca630450f/4-optimizing-video-size-quality.png" width="800" height="" sizes="100vw" caption="A pie chart with the video taking up 80.2% of the entire data consumed. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92509910-4e29-4e32-86b4-891ca630450f/4-optimizing-video-size-quality.png'>Large preview</a>)" alt="" >}}

**44 MB of video**. Where is it coming from? Even beyond that, when we examine the source and the waterfall in a bit more detail, we can see that there are actually two videos! Fortunately (or unfortunately?), neither managed to be downloaded entirely:

<div class="scroll-pane">
<table data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
  <tr>
  <th>Video</th>
  <th>Size</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td>Video 1 downloaded</td>
      <td>11.8 MB (of 121 MB total)</td>
    </tr>
    <tr>
      <td>Video 2 downloaded</td>
      <td>31.1MB (of 139 MB total)</td>
    </tr>
  </tbody>
</table>
</div>

This raises a few concerns and a few questions.

First, why was so much video downloaded when it wasn’t autoplaying? We haven’t managed to click anything just yet, but already used almost 40 MB of data. The answer, as always, lies in the source. Well, “view source”, that is.

<div class="break-out">

 <pre><code class="language-markup">&lt;video
  id="u457537-video"
  class="video-js vjs-big-play-centered"
  controls
  preload="auto"
  width="1050"
  height="591"
  poster="assets/home_poster.jpg"
  data-setup='{"fluid": true}'&gt;</code>
  <code class="language-markup" style="background-color: #fffbd7">&lt;source src="assets/home_1.mp4" type='video/mp4'&gt;
  &lt;source src="assets/home.webm" type='video/webm'&gt;</code>
  <code class="language-markup">&lt;p class="vjs-no-js"&gt;To view this video please enable JavaScript, and consider
    upgrading to a web browser that &lt;a href="https://videojs.com/html5-video-support/"
    target="_blank"&gt;supports HTML5 video&lt;/a&gt;&lt;/p&gt;
&lt;/video&gt;
</code></pre>
</div>

Off the bat, we see [at least two issues](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-1/):

- **preload="auto"**  
When we set `preload="auto"`, we are overriding the browser’s default setting, **enforcing video download** &mdash; whether or not your customer has pressed “Play”. The default `preload` attribute is `metadata`, and would have resulted in a few 100KB downloaded. Admittedly, it is a much better outcome for site visitors who will never watch this video.
- **Video Order**  
If you have multiple versions of the video (in this case: h264 .mp4 and VP8 .webm encoded videos), the browser will choose the **first video** it knows how to play. Now, every modern browser supports mp4, while most modern browsers also support webm ([95.4% global support](https://caniuse.com/?search=webm), according to CanIUse).

One [trick that I like to use](https://dougsillars.com/2020/01/06/hiding-videos-on-the-mbile-web/) is to insert the appropriate video source line with Javascript. That way, if you so choose to not serve video on certain screens, you just have an empty &lt;video&gt; tag &mdash; and no video can be downloaded.

<pre class="break-out language-js">
<code>
	window.onload = addAutoplay();
	var videoLocation  = document.getElementById("hero-video");

	function addAutoplay() {
		if(window.innerWidth > 992){
			videoLocation.setAttribute("autoplay","");
	  };
	}
</code>
</pre>

If we now run an ffprobe on these two videos, we’ll discover significant differences in sizes:

<table>
  <thead>
  <tr>
  <th>Format</th>
  <th>Size</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td>Mp4</td>
      <td>121.2 MB</td>
    </tr>
    <tr>
      <td>Webm</td>
      <td>11.8 MB</td>
    </tr>
  </tbody>
</table>

The webm is 90% smaller, and yet **has 0 views**, since every browser supports the mp4. These two videos are both 640&times;360, and 140s long. Running the `ffmpeg` command from above on the mp4 results in a 12.4 MB video, so it’s likely that developers followed a similar process to compress and encode the .webm variant as well. Perhaps having `preload="auto"` for 12.5 MB would not be so bad after all.

The second video (drone footage inside the restaurant) is filmed in Full HD (1080p), but similarly gets compressed from 140MB to 35 MB. So, 120s with FFMPEG could **reduce the video weight** on this page from 160 MB to 57 MB.  Flipping the webm/mp4 order would save an additional few MB for 95% of the browsers that can support that format.

What if we wanted to do even better, perhaps make the videos responsive to various sized screens? Well, let’s get even smaller videos &mdash; with responsive videos!

The &lt;video&gt; tag [doesn’t support media queries](https://www.filamentgroup.com/lab/video-with-sizes/) to serve different video files to different screens, so we need a different way to provide videos sized for the device screen. The easiest way to achieve that is by using **video streaming**. This will add some Javascript and other assets for the video player that will be required, but the video savings will definitely make up for this extra data.

{{% ad-panel-leaderboard %}}

We can create video streams with FFMPEG (I have used [bash scripts like this](https://gist.github.com/maitrungduc1410/9c640c61a7871390843af00ae1d8758e) in the past), but this requires us to know all the sizes and settings we’d like to use (and as mentioned before, FFMPEG has a lot of settings!).

To make it easier to stream video, there are APIs (e.g. [api.video](https://api.video) and [Mux](https://mux.com)) where you upload your video, and the tools create video streams and host your video for you. For full disclouse, I do work at the former one, so to simplify my video processing pipeline, I’ll use [api.video](https://api.video), to transcode and host my videos. With the [upload API](https://upload.a.video), I can upload any video, and the tool will create a streaming version at many different dimensions and bitrates (currently 240p, 360p, 480p, 720p, 1080p and 4K).

The bitrates for the smaller videos are greatly reduced, as the dimensions of the video decrease. This means that **the video will require less network capacity on smaller screens** and will play on slower networks.

For brevity, we’ll test only the Pumpkin patch video. I’ve received similar results with the drone video (the other pizza video is just 360p, so it does not greatly benefit from smaller sizes).

**Note**: *Please recall that this video is currently a 1080p mp4 video at 60fps, and weighs 157 MB for all visitors.*

With some optimizations (CRF 28 and reducing the framerate to 30fps), the video was reduced to **35.7 MB**. Using DevTools, we can emulate devices to see how much data is used for video playback of streaming video on different sized screens.

The table below is showing the total amount of traffic used. With HLS video, there is a JavaScript player, CSS, fonts, etc. that add about 1 MB of additional overhead. This is included in the totals below:

<div class="scroll-pane">
<table>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Device</th>
      <th>Video Size (Pixels)</th>
      <th>Video Size (MB)</th>
      <th>Bitrate (MBPS)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Moto G4 (Portrait)</td>
      <td>240p</td>
      <td>3.1 MB</td>
      <td>0.35</td>
    </tr>
    <tr>
      <td>Moto G4 (Landscape)</td>
      <td>360p</td>
      <td>7.5 MB</td>
      <td>0.800</td>
    </tr>
    <tr>
      <td>Iphone 7/7/8 (Landscape)</td>
      <td>480p</td>
      <td>12.1 MB</td>
      <td>1.40</td>
    </tr>
    <tr>
      <td>Ipad (Landscape)</td>
      <td>720p</td>
      <td>21.2 MB</td>
      <td>2.6 </td>
    </tr>
    <tr>
      <td>Ipad Pro (Landscape)</td>
      <td>1080p</td>
      <td>39.4 MB</td>
      <td>4.4</td>
    </tr>
  </tbody>
</table>
</div>

At 1080p, there is about 4MB additional assets downloaded for the stream, but for every other size, there are significant data savings with no loss in video quality.  Not only will the video be **sized properly for the devices**, but it is much less likely to stall, as the bitrate is reduced for the devices most likely to be on slower mobile connections.

{{% pull-quote %}}
 Video streaming takes care of framerate, video size and quality concerns — ensuring fast playback on any size screen, and any speed network.
{{% /pull-quote %}}

Another advantage to video streaming: if the network is slow (or suddenly becomes slower), the player can adjust the video being shown, and play a lower quality version of the video &mdash; ensuring playback on the device &mdash; even in poor network conditions. (You can test the different videos with [StreamOrNot](https://dougsillars.github.io/StreamOrNot/), a little open source project that I've released a while back.

Now, isn’t it a little bit too much overhead? Couldn’t we do the same (just much faster) with YouTube or Vimeo? We surely could, but then we wouldn’t be able to completely remove the branding or advertising from the video, not to mention the overhead of scripts loaded within the video player iframe. Plus, sometimes you might want to use the video as a background video on your product page, and avoid any kind of external branding at all.

## Conclusion

We do not deploy images from our camera directly to the web, but we compress and resize them to balance quality and web performance. The same should be done for video files as well. **Smaller videos start playing faster** and stall less often, improving the user experience of the website.

In this article, we’ve walked through a few simple steps to optimize our videos, e.g. by lowering the quality and its framerate. We also looked at how video streaming can allow us to build a more responsive video experience for the web &mdash; automatically serving videos that are properly sized for the screen of the device.

Thanks for reading, and if you’d like to learn more, you may want to read more on **video best practices** here, on Smashing Magazine, and on my blog:

- [Video Playback On The Web: The Current State Of Video (Part 1)](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-1/)
- [Video Playback On The Web: Video Delivery Best Practices (Part 2)](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-2/)
- [Hiding Videos On the Mobile Web](https://dougsillars.com/2020/01/06/hiding-videos-on-the-mbile-web/)

{{< signature "vf, il" >}}
