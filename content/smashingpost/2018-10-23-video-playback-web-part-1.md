---
title: 'Video Playback On The Web: The Current State Of Video (Part 1)'
slug: video-playback-on-the-web-part-1
author: doug-sillars
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7e76c6-16ae-494e-8c44-5e70eb0f2bce/video-playback-web-image-0.png
date: 2018-10-24T13:30:24+02:00
summary: >-
  Video content on the web increases customer engagement and satisfaction. Pages that load quickly have the same effect. The addition of video to your website will slow down the page rendering time, necessitating a balance between overall page load and video content. 
description: >-
  Video content on the web increases customer engagement and satisfaction. Pages that load quickly have the same effect. The addition of video to your website will slow down the page rendering time, necessitating a balance between overall page load and video content. 
categories:
  - Videos
  - Media
  - Performance
  - Optimization
  - Guides
---
Usage of video on the web is increasing as devices and networks become faster and more capable of handling video content. Research shows that sites with video increase engagement by 80%. E-Commerce sites with video have higher conversions than sites without video.

But adding video can come at a cost. Videos (being larger files) add to the page load time, and performance research shows that slower pages have the opposite effect of lower customer engagement and conversions. In this aticle, I’ll examine the important metrics to balance performance and video playback on the web, look at how video is being used today, and provide best practices on delivering video on the web.

One of the first steps to improve customer satisfaction is to **speed up the load time of a page**. Google has shown that mobile pages that take over three seconds to load lose 53% of their audience to abandonment. Other studies find that on improving site performance, usage and sales increase.

Adding video to a website will increase engagement, but it can also dramatically slow down the load time, so it is clear that a balance must be found between adding videos to your site and not impacting the load time too greatly.

**Recommended reading**: *[Front-End Performance Checklist 2018 [PDF, Apple Pages]](https://www.smashingmagazine.com/2018/01/front-end-performance-checklist-2018-pdf-pages/)*

## Video On The Web Today

To examine the state of video on the web today, I’ll use data from the HTTP Archive. The HTTP Archive uses WebPageTest to scan the performance of 1.2 million mobile and desktop websites every two weeks, and then stores the data in Google BigQuery.

Typically just the main page of each domain is checked (meaning `www.cnn.com` is run, but `www.cnn.com/politics` is not). This data can help us understand how the usage of video on the web affects the performance of websites. Mobile tests are run on an emulated Motorola G4 with a 3G internet connection (1.6 MBPS down, 768 KBPS up, 300 ms RTT), and desktop tests run Chrome on a cable connection (5 MBPS down, 1 MBPS up, 28ms RTT). I’ll be using the data set from 1 August 2018.

{{% feature-panel %}}

### Sites That Download Video

As a first step to study sites with video, we should look at sites that download video files when the page loads. There are 35k mobile sites and 55k desktop sites with video file downloads in the HTTP Archive data set (that’s 3% of all mobile sites and 4.5% of all desktop sites). Comparing desktop to mobile, we find that 30k of these sites have video on both mobile and desktop (leaving &#126;5,800 sites on mobile with no video on the desktop).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7e76c6-16ae-494e-8c44-5e70eb0f2bce/video-playback-web-image-0.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7e76c6-16ae-494e-8c44-5e70eb0f2bce/video-playback-web-image-0.png" sizes="100vw" caption="Mobile and Desktop Sites with Video (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7e76c6-16ae-494e-8c44-5e70eb0f2bce/video-playback-web-image-0.png'>Large preview</a>)" alt="Pi chart showing overlap of mobile and desktop video sites" >}}

The median mobile page with video weighs in at a hefty 7 MB (583% larger than 1.2 MB found for the median mobile site). This increase is not fully accounted for by video alone (2.5 MB).  As sites with video tend to be more feature rich and visually engaging, they also use more images (the median site has over 1 MB more), CSS, and Javascript. The table below also shows that the median SpeedIndex (a measurement of how quickly content appears on the screen) for sites with video is 3.7s slower than a typical mobile site, taking a whopping 11.5 seconds to load.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist"></th>
            <th>SpeedIndex</th>
            <th>Bytes Total</th>
            <th>Bytes Video</th>
            <th>Bytes CSS</th>
            <th>Bytes Images</th>
            <th>Bytes JS</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Video</td>
            <td>11544</td>
            <td>6,963,579</td>
            <td>2,526,098</td>
            <td>80,327</td>
            <td>1,596,062</td>
            <td>708,978</td>
        </tr>
        <tr>
            <td>all sites</td>
            <td>7780</td>
            <td>1,201,802</td>
            <td>0</td>
            <td>40,648</td>
            <td>449,585</td>
            <td>336,973</td>
        </tr>
    </tbody>
</table>

This clearly shows that sites that are more interactive and have video content take (on average) longer to load that sites without video. But can we speed up video delivery?  What else can we learn from the data at hand?

## Video Hosting

When examining video delivery, are the files being served from a CDN or video provider, or are developers hosting the videos on their own servers?  By examining the domain of the videos delivered on mobile, we find that 12,163 domains are used to deliver video, indicating that &#126;49% of sites are serving their own video files. If we stack rank the domains by frequency, we are able to determine the most common video hosting solutions:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">Video Doman</th>
            <th>cnt</th>
            <th>%</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>fbcdn.net</td>
            <td>116788</td>
            <td>67%</td>
        </tr>
        <tr>
            <td>akamaihd.net</td>
            <td>11170</td>
            <td>6%</td>
        </tr>
        <tr>
            <td>googlevideo.com</td>
            <td>10394</td>
            <td>6%</td>
        </tr>
        <tr>
            <td>cloudinary.com</td>
            <td>3170</td>
            <td>2%</td>
        </tr>
        <tr>
            <td>amazonaws.com</td>
            <td>1939</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>cloudfront.net</td>
            <td>1896</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>pixfs.net</td>
            <td>1853</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>akamaized.net</td>
            <td>1573</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>tedcdn.com</td>
            <td>1507</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>contentabc.com</td>
            <td>1507</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>vimeocdn.ccom</td>
            <td>1373</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>dailymotion.com</td>
            <td>1337</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>teads.tv</td>
            <td>1022</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>youtube.com</td>
            <td>1007</td>
            <td>1%</td>
        </tr>
        <tr>
            <td>adstatic.com</td>
            <td>998</td>
            <td>1%</td>
        </tr>
    </tbody>
</table>

Top CDNs and domains Facebook, Akamai, Google, Cloudinary, AWS, and Cloudfront lead the way, which is not surprising. However, it is interesting to see YouTube and Vimeo so far down in the list, as they are two of the most popular video sharing sites. 

{{% ad-panel-leaderboard %}}

Let’s look into YouTube, Vimeo and Facebook video delivery:

### YouTube Video Counts

By default, pages with a YouTube video embedded do not actually download any video files &mdash; just scripts and a placeholder image, so they do not show up in a querly looking for sites with video downloads. One of the Javascript downloads for the YouTube Video player is `www-embed-player.js`. Searching for this file, we find 69k instances on 66,647 mobile sites. These sites have a median SpeedIndex of 10,700, and data usage of 3.31MB &mdash; better than sites with video downloaded, but still slower than sites with no video at all. The increase in data is directly associated with more images and Javascript (as shown below). 

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist"></th>
            <th>Speedindex</th>
            <th>Bytes Total</th>
            <th>Bytes Video</th>
            <th>Bytes CSS</th>
            <th>Bytes Images</th>
            <th>Bytes JS</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Video</td>
            <td>11544</td>
            <td>6,963,579</td>
            <td>2,526,098</td>
            <td>80,327</td>
            <td>1,596,062</td>
            <td>708,978</td>
        </tr>
        <tr>
            <td>All sites</td>
            <td>7780</td>
            <td>1,201,802</td>
            <td>0</td>
            <td>40,648</td>
            <td>449,585</td>
            <td>336,973</td>
        </tr>
        <tr>
            <td>YouTube script</td>
            <td>10700</td>
            <td>3,310,000</td>
            <td>0</td>
            <td>126,314</td>
            <td>1,733,473</td>
            <td>1,005,758</td>
        </tr>
    </tbody>
</table>

### Vimeo Video Counts

There are 14,148  requests for Vimeo videos in HTTP Archive for Video playback. I see only 5,848 requests for the *player.js* file (in the format `https://f.vimeocdn.com/p/3.2.0/js/player.js` &mdash; implying that perhaps there are many videos on one page, or perhaps another location for the video player file. There are 17 different versions of the player present into HTTP Archive, with the most popular being 3.1.5 and 3.1.4:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">URL</th>
            <th>cnt</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.5/js/player.js</code></td>
            <td>1832</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.4/js/player.js</code></td>
            <td>1057</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.17/js/player.js</code></td>
            <td>730</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.8/js/player.js</code></td>
            <td>507</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.10/js/player.js</code></td>
            <td>432</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.15/js/player.js</code></td>
            <td>352</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.19/js/player.js</code></td>
            <td>153</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.2/js/player.js</code></td>
            <td>117</td>
        </tr>
        <tr>
            <td><code>https://f.vimeocdn.com/p/3.1.13/js/player.js</code></td>
            <td>105</td>
        </tr>
    </tbody>
</table>

There does not appear to be any performance gain for any Vimeo Library &mdash; all of the pages have similar load times.

**Note**: *Using* `www-embed-player.js` *for YouTube or* `https://f.vimeocdn.com/p/*/js/player.js` *for Vimeo are good fingerprints for browsers with a clean cache, but if the customer has previously browsed a site with an embedded video, this file might already be in the browser cache, and thus will not be re-requested. But, as Andy Davies recently [noted](https://andydavies.me/blog/2018/09/06/safari-caching-and-3rd-party-resources/), this is not a safe assumption to make.*

### Facebook Video Counts

It is surprising that in the HTTP Archive data, 67% of all video requests are from Facebook’s CDN. It turns out that on Chrome, 3rd party Facebook widgets [download 30% of all videos](https://dougsillars.com/2018/08/21/excess-video-download-on-embedded-facebook-pages/) posted inside the widget (This effect does not occur in Safari or in Firefox.). It turns out that a 3rd party widget added with just a few lines of code is responsible for 57% of all the video seen in the HTTP Archive. 

## Video File Types

The majority of videos on pages tested are Mp4s. If we look at all the videos downloaded (excluding those from Facebook), we get the following view:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">File extension</th>
            <th>Video count</th>
            <th>%</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>.mp4</td>
            <td>48,448</td>
            <td>53%</td>
        </tr>
        <tr>
            <td>.ts</td>
            <td>18,026</td>
            <td>20%</td>
        </tr>
        <tr>
            <td>.webm</td>
            <td>3,946</td>
            <td>4%</td>
        </tr>
        <tr>
            <td></td>
            <td>14,926</td>
            <td>16%</td>
        </tr>
        <tr>
            <td>.m4s</td>
            <td>2,017</td>
            <td>2%</td>
        </tr>
        <tr>
            <td>.mpg</td>
            <td>1,431</td>
            <td>2%</td>
        </tr>
        <tr>
            <td>.mov</td>
            <td>441</td>
            <td>0%</td>
        </tr>
        <tr>
            <td>.m4v</td>
            <td>407</td>
            <td>0%</td>
        </tr>
        <tr>
            <td>.swf</td>
            <td>251</td>
            <td>0%</td>
        </tr>
    </tbody>
</table>

Of the files with no extension &mdash; 10k are `googlevideo.com` files. 

What can we learn about these files?  Let’s look each file type to learn more about the content being delivered. 

I used FFPROBE to query the 34k unique MP4 files, and obtained data for 14,700 videos (many of the videos had changed or been removed in the 3 weeks from HTTP Archive capture to analysis). 

## MP4 Video Data

Of the 14.7k videos in the dataset, 8,564 have audio tracks (58%). Shorter videos that autoplay or videos that play in the background do not require audio, so stripping the audio track is a great way to reduce the file size (and speed the delivery) of your videos.  

The next most important aspect to quickly downloading a video are the dimensions. The larger the dimensions (and in the case of video, there are three dimensions to consider: `width` &times; `height` &times; `time`), the larger the video file will be. 

### MP4 Video Duration

Most of the 14k videos studied are short: the median (50th percentile) duration is 21s. However, 10% of the videos surveyed are over 2 minutes in duration. Use cases here will, of course, be divided, but for short video loops, or background videos &mdash; shorter videos will use less data, and download faster.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c33e264c-0275-45ae-a7a8-e0da51f4908a/video-playback-web-image-6.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c33e264c-0275-45ae-a7a8-e0da51f4908a/video-playback-web-image-6.png" sizes="100vw" caption="Distribution of Video Duration (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c33e264c-0275-45ae-a7a8-e0da51f4908a/video-playback-web-image-6.png'>Large preview</a>)" alt="Column Chart breaking down video length in 10 second segments" >}}

### MP4 Video Width And Height

The dimensions of the video on the screen decide how many pixels each frame will have to use. The chart below shows the various video widths that are being served to the mobile device. (As a note, the Moto G4 has a screen size of 1080&times;1920, and the pages are all viewed in portrait mode).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c3e491-aa9d-42c2-984e-28209ab17eb9/video-playback-web-image-7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c3e491-aa9d-42c2-984e-28209ab17eb9/video-playback-web-image-7.png" sizes="100vw" caption="Video Counts by Width (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c3e491-aa9d-42c2-984e-28209ab17eb9/video-playback-web-image-7.png'>Large preview</a>)" alt="A column chart displaying the count of each video width observed in the data set" >}}

As the data shows, the two most utilized video widths are significantly larger than the G4 screen (when held in portrait mode). A full 49% of all videos are served with a width greater than 1080 pixels wide. The Alcatel 1x, a new Android Go device, has a 480&times;960-pixel screen. 77% of the videos delivered in the sample set are larger than 480 pixels wide.     

As dimensions of videos decrease, so does the files size (and thus time to deliver the video). This is the primary reason to resize videos. 

Why are these videos so large? If we correlate the videos served on mobile and desktop, we find that 18% of videos served on mobile are the same videos served on the desktop. This is a ‘problem’ solved for images years ago with responsive images. By serving differently sized videos to different sized devices, we can ensure that beautiful videos are served, but at a size and dimension that makes sense for the device.

{{% ad-panel-leaderboard %}}

### MP4 Video Bitrate

The bitrate of the video delivered to the device plays a large effect on how well the video will play back. The HTTP Archive tests are run on a 3G connection at 1.6 MBPS download speed. To playback (without stalling) the download has to be faster than playback. Let’s provide 80% of the available bitrate to video files (1.3 MBPS). 47% of the videos in the sample set have a bitrate over 1.3 MBPS, meaning that when these videos are played on a 3G connection, they are more likely to stall &mdash; leading to unhappy customers. 27% of videos have a bitrate higher than 2.5 MBPS, 10% are higher than 5 MBPS, and 35 of videos served to mobile devices have a bitrate > 10 MBPS. These larger videos are unlikely to play without stalling on many connections &mdash; fixed or mobile.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f724a0b-23d1-47bd-a786-7f4e0036b130/video-playback-web-image-8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f724a0b-23d1-47bd-a786-7f4e0036b130/video-playback-web-image-8.png" sizes="100vw" caption="Observed Video Bitrates (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f724a0b-23d1-47bd-a786-7f4e0036b130/video-playback-web-image-8.png'>Large preview</a>)" alt="Column chart listing video bitrates in 500 KBPS buckets." >}}

### What Leads To Higher Bitrates

Larger videos tend to carry a larger bitrate, as larger dimensioned videos require a lot more data to populate the additional pixels on the device. Cross referencing the bitrate of each video to the width confirms this:  videos with width 1280 (orange) and 1920 (gray) have a much broader distribution of bitrates (more data points to the right in the chart). The column marked in yellow denotes the 136 videos with width 1920, and a bitrate between 10-11 MBPS.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbf8c36-ca16-43e3-924b-b0b7e86b404b/video-playback-web-image-9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbf8c36-ca16-43e3-924b-b0b7e86b404b/video-playback-web-image-9.png" sizes="100vw" caption="Bitrate Vs. Video Width (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbf8c36-ca16-43e3-924b-b0b7e86b404b/video-playback-web-image-9.png'>Large preview</a>)" alt="3D Column chart showing how bitrate and video size are related" >}}

If we visualize only the videos over 1.6 MBPS, it becomes clear that the higher screen resolutions (1280 and 1920) are responsible for the higher bitrate videos.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47a8dacf-73e1-422d-bfdc-d6d9fcff5bbb/video-playback-web-image-10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47a8dacf-73e1-422d-bfdc-d6d9fcff5bbb/video-playback-web-image-10.png" sizes="100vw" caption="High Bitrate and Video Width (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47a8dacf-73e1-422d-bfdc-d6d9fcff5bbb/video-playback-web-image-10.png'>Large preview</a>)" alt="3D chart showing that larger width videos generally have higher bitrate" >}}

### MP4: HTTP vs. HTTPS

HTTP2 has redefined content delivery with multiplexed connections &mdash; where just one connection per server is required. For large files like video, does HTTP2 provide a meaningful improvement to content delivery?  If we look at the stats from the HTTP Archive:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c8c11b8-5fed-4323-89ff-2c08089827d0/11-video-playback-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c8c11b8-5fed-4323-89ff-2c08089827d0/11-video-playback-web.png" sizes="100vw" caption="HTTP1 vs HTTTP2 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c8c11b8-5fed-4323-89ff-2c08089827d0/11-video-playback-web.png'>Large preview</a>)" alt="Pie Chart of HTTP1 vs. HTTP2 for video delivery" >}}

Omitting the 116k Facebook videos (all sent via HTTP2), we see that it is about a 50:50 split between HTTP 1.1 and HTTP2. However, HTTP1.1 can utilize HTTPS, and when we filter for HTTPS usage, we find that 81% of video streams are sent via HTTPS, with HTTP2 being used slightly more than HTTPS1.1 (41%:36%)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b2249d-5d9c-49fa-a833-889e7f42c3b7/12-video-playback-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b2249d-5d9c-49fa-a833-889e7f42c3b7/12-video-playback-web.png" sizes="100vw" caption="HTTP vs. HTTP2 and secure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b2249d-5d9c-49fa-a833-889e7f42c3b7/12-video-playback-web.png'>Large preview</a>)" alt="Pie Chart further showing HTTP1 nonsecure and secure breakdown" >}}

As you can see, comparing the speed of HTTP and HTTP2 video delivery is a work in progress.

## HLS Video Streaming

Video streaming using adaptive bitrate is an ideal way to deliver video to the end user. Multiple versions of each video are built with different dimensions and bitrates. The list of available streams is presented to the playback device, and the video player on the device can choose the most appropriate stream based on the size of the device screen and the available network conditions. There are 1,065 manifest files (and 14k video stream files) in the HTTP Archive data set that I examined. 

### Video Stream Playback

One key metric in video streaming is to have the video start as quickly as possible. While the manifest file has a list of available streams, the player has no idea the available bandwidth of the network at the beginning of playback. To begin streaming, and because the player has to pick a stream, it typically chooses the first one in the list. In order to facilitate a fast video startup, it is important to place the correct stream at the top of your manifest file. 

**Note**: *Utilizing the Chrome Network Info API to generate manifest files on the fly might be a good way to quickly optimize video content at startup.*

One way to ensure that the video starts quickly is to start with the lowest quality video segment, as the download will be the fastest. The initial video quality may be pixelated, but as the player better understands the network quality, it can quickly adjust to a more appropriate (hopefully higher quality) video stream. With that in mind, let’s look at the initial stream bitrates in the HTTP Archive.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbd9944-9261-4a63-b87a-9f9cc7003223/video-playback-web-image-13.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbd9944-9261-4a63-b87a-9f9cc7003223/video-playback-web-image-13.png" sizes="100vw" caption="Initial Bitrate for video streams (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbd9944-9261-4a63-b87a-9f9cc7003223/video-playback-web-image-13.png'>Large preview</a>)" alt="Column chart showing initial bitrates in streaming videos. Many videos have too high an initial bitrate to stream on mobile." >}}

The red line in the above chart denotes 1.5 MBPS (recall that mobile tests are run at 1.6 MBPS, and not only video content is being downloaded). We see 30.5% of all of the streams (everything to the left of the line) start with an initial bitrate higher than 1.5 MBPS (and are thus unlikely to playback on a 3G connection)  17% start above 2 MBPS.

So what happens when video download is slower than the actual playback of the video? Initially, the player will attempt to download the (too) large bitrate files, but based on the download speed, will realise the problem. The player will then switch to downloading a lower bitrate video, so that download is faster than playback. The problem is that the initial download attempt takes time, and adding a delay to video playback start leads to customer abandonment.

We can also look at the most common bitrates of `.ts` files (the files that have the video content), to see what bitrates end up being downloaded on mobile. This data includes the initial bitrates, and any subsequent file downloaded during the WebPageTest run:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfbb01a0-6f17-4db2-818b-1e50991e5499/video-playback-web-image-14.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfbb01a0-6f17-4db2-818b-1e50991e5499/video-playback-web-image-14.png" sizes="100vw" caption="Observed Mobile Bitrates (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfbb01a0-6f17-4db2-818b-1e50991e5499/video-playback-web-image-14.png'>Large preview</a>)" alt="Column chart of observed bitrates once streaming begins" >}}

We can see two major groupings of video streaming bitrates (100-300 KBPS, and a broader peak from 300-1,000 MBPS). This is where we would expect streams to appear, given that the network speed is capped at 1.6 MBPS.

Comparing the data to the desktop, Mobile clearly is higher at the lower bitrates, and desktop streams have high peaks in the 500-600 and 800-900 KBPS ranges, that are not seen in mobile.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faef7695-db2e-4073-acf2-1a083292f890/15-video-playback-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faef7695-db2e-4073-acf2-1a083292f890/15-video-playback-web.png" sizes="100vw" caption="Observed mobile and Desktop streaming bitrates (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faef7695-db2e-4073-acf2-1a083292f890/15-video-playback-web.png'>Large preview</a>)" alt="Column chart comparing observed bitrates on mobile and desktop" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf045ea-5945-4016-b0c2-ca5de3e8ed4a/16-video-playback-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf045ea-5945-4016-b0c2-ca5de3e8ed4a/16-video-playback-web.png" sizes="100vw" caption="Observed bitrates, mobile, desktop compared to initial bitrate (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf045ea-5945-4016-b0c2-ca5de3e8ed4a/16-video-playback-web.png'>Large preview</a>)" alt="Column chart comparing initial bitrates with the observed bitrates for mobile and desktop." >}}

When we compare the initial bitrates observed (blue) with the actual files downloaded, it is very clear that for mobile the bitrate generally decreases during stream playback, indicating that lowering the initial bitrate for video streams might improve the performance of video startup and prevent stalls in early playback of the video. Desktop video also appears to decrease, but it is also possible that some video move to higher playback speeds.

## Conclusion

Video content on the web increases customer engagement and satisfaction. Pages that load quickly have the same effect. The addition of video to your website will slow down the page rendering time, necessitating a balance between overall page load and video content. To reduce the size of your video content, ensure that you have versions appropriately sized for mobile device dimensions, and use shorter videos when possible.

If playback of your videos is not essential, follow the path of YouTube and Vimeo &mdash; download all the required pieces to be ready for playback, but don’t actually download any video segments until the user presses play. Finally &mdash; if you are streaming video &mdash; start with the lowest quality setting to ensure a fast video playback.

In my [next post on video](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-2/), I will take these general findings, and dig deeper into how to resolve potential issues with examples.

{{< signature "dm, ra, il" >}}