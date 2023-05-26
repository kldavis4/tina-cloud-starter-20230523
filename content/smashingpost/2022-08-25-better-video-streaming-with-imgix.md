---
title: 'Better Video Streaming With imgix'
slug: better-video-streaming-with-imgix
author: doug-sillars
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/746fe02f-c535-4bb9-bb61-f30467af2a58/better-video-streaming-with-imgix.jpg
date: 2022-08-25T08:00:00.000Z
summary: >-
  If you need to deliver a large number of images and videos, a solution like [imgix](https://imgix.com/?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08) can optimize and process both types of assets without you having to build it from the ground up or cobble together different solutions. Let’s take a closer look at how.
description: >-
  If you need to deliver a large number of images and videos, a solution like [imgix](https://imgix.com/?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08) can optimize and process both types of assets without you having to build it from the ground up or cobble together different solutions. Let’s take a closer look at how.
categories:
  - Tools
  - Video
  - Techniques
  - Performance
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: imgix
  link: https://imgix.com/?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8e0a226-81cf-4c92-85e3-2341f861367f/imgix-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://imgix.com/?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08">imgix</a> who build tools that make images and video on the Internet more beautiful, more performant, more valuable, and safer. <em>Thank you!</em>
---

Adding video to your website immediately adds value, but also a new level of complexity to your web development. Can I use the `<video>` tag? Do I need a JavaScript video player? What formats should the video be in for the best browser support? How do I account for different network speeds in different environments? How do I make sure that my videos will always play back with minimal buffering?

It sounds like a lot (and you might even consider throwing your hands up in the air asking, “Why don’t we just put it up on YouTube?”) This is a valid response &mdash; the more you dig into video and video delivery, more and more complexities arise that your developers will have to deal with.

For some, “toss it all on YouTube” might be an adequate solution to handle the complexities of video. But YouTube is based on ads and watching videos, and you probably don’t want an ad appearing in your mission critical content &mdash; even worse if it is an ad from your competition! Your goals with video delivery conflict directly with the goals of YouTube’s video delivery platform, making it a less than ideal solution for most enterprises. 

## Does That Mean We Are Back To Square One? 

With the biggest (and cheapest) service removed from consideration, what are the best ways to solve all of the questions in the first paragraph? It is entirely possible to ‘build your own’ video platform, but this leads us back to complexities and pulling your development team away from core features to handle video delivery. From time to market, cost (and cognitive overhead), the best way to add video is to utilize a video streaming service. The great thing today is that you *can* use the same technologies used by Netflix or Hulu to deliver your videos.

## What Is Video Streaming And Why You Need Adaptive Bitrate Video

Video streaming is the way that most video content is delivered on the web today. It features a number of advantages to just using a static video in the `<video>` tag.

The coolest feature that video streaming introduces is **Adaptive Bitrate Video**. Before adaptive bitrate video was developed, only one bitrate of the video could be delivered to the customer, regardless of the device or bandwidth environment. This solution is fine when network speeds are fast, but it can be problematic when network speeds are not fast (or fluctuate). And if there is one thing we all know &mdash; we cannot control the speed network our customers are using. 

On a slow network connection, a traditional video will be very slow to start and very likely to stall. (Stalling is the video streaming term for the video stopping and a “spinner of death” appearing). Adaptive bitrate videos have multiple versions of the video available and can adapt to the network speed of your customer. That ensures that the video will start playback quickly and is much less likely to stall during playback &mdash; no matter the speed of your user’s internet connection.

{{< rimg breakout="true" href="https://blog.imgix.com/2021/12/14/streaming-video-part-2-adaptive-bitrate-streaming?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3406e190-4aee-4548-9bd5-244f0a224f7d/video-file-requirements-imgix.png" width="800" height="391" sizes="100vw" caption="Fixed bitrate streaming doesn’t adapt to different device or bandwidth environments. (Image credit: <a href='https://blog.imgix.com/2021/12/14/streaming-video-part-2-adaptive-bitrate-streaming?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08'>imgix</a>)" alt="imgix video file requirements" >}}

If the network suddenly slows down, the player can also adapt (in the middle of the playback) and begin playing a lower bitrate version of the video. All of these features of adaptive bitrate streaming lead to a better video experience for your customers. It almost sounds like magic, but let’s look at the technology and how it works.

### HLS: The Magic Behind Smooth Video Streaming

The industry standard for video streaming is HTTP Live Streaming (HLS). The term Live in the name is a little misleading. While HLS can be used to stream live video, HLS is primarily used for playback of recorded videos, and can be found powering many of the top streaming services.

So how does HLS video work? The first step occurs on video upload when the streaming service generates a number of copies of the video in different bitrates. Then, each copy of the video is sliced into short segments &mdash; usually about 5-10 seconds long. 

{{< rimg breakout="true" href="https://blog.imgix.com/2021/12/15/streaming-video-part-3-http-live-streaming?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/189d63d7-fe0e-4d75-b055-f86b0188a98f/smooth-video-streaming.png" width="800" height="556" sizes="100vw" caption=" How HLS works. (Image credit: <a href='https://blog.imgix.com/2021/12/15/streaming-video-part-3-http-live-streaming?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08'>imgix</a>)" alt="imgix smooth video streaming" >}}

During playback, the video player handles the download and playback of the video. If the rate of download begins to slow compared to the rate of playback &mdash; it is possible that the video might stall. So when the player requests the next 5-10 second segment of the video, it requests a lower bitrate version &mdash; since lower bitrates download faster, and the chance of video stall is mitigated.

This is the magic of the adaptive bitrate playback &mdash; the player adapts the video to meet the network speeds of each unique viewer of your content!

### You Mention A Player. Do Browsers Not Support HLS?

HLS is not natively supported in many browsers (it does have native support in Safari). In order to play an HLS video, you’ll need a [JavaScript player](https://videojs.com/) as a part of your site to play back the video.

### This Sounds Complicated

With time and development, it is possible to build your own video streaming platform &mdash; delivering an incredible video experience by re-encoding the video to HLS and delivering a customized player to your audience. But, building a video encoding/streaming platform will take a lot of developer time, pulling the team away from building your product. This is why my recommendation is to use a video streaming platform.

## What Makes A Good Video Processing Solution?

Outsourcing complicated problems to the experts is a smart idea &mdash; you’re hiring domain experts to handle the complicated things rather than tackling them yourself. So what are the features that you should look for in a video streaming solution?

* **Think of the advantages of HLS adaptive bitrate streaming**.  
If you’re paying for high-quality and robust video delivery, you want to make sure the best streaming solution is in place.
* **Support conversion from all major file formats.**  
Mp4 (h264 and 265), MOV, WebM, and others. Videos come in a myriad of formats; there’s no reason to convert to a new format before uploading.
* **Your video streaming tool should fit into your existing media pipeline.**  
The media solution should be able to find your videos in your current process &mdash; when videos are added to the cloud, they should be automatically processed into streams. 
* **An out-of-the-box video player.**  
As discussed, HLS streams don’t play in all browsers. Does your solution include a customizable player that you can plug into your current website?
* If you deliver both images and videos, you want a solution that includes an **asset management dashboard** that allows you to visualize and organize images and videos
* **Last but not least, analytics.**  
How many viewers have watched your videos, and how long was each view? You also want to see processing analytics on how many videos have been fully encoded.

{{< rimg breakout="true" href="https://blog.imgix.com/2022/01/18/video-api-limited-availability?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/998552a2-2ca9-4f7c-b6a7-0ed571e663e1/imgix-video-streaming-requirements.png" width="800" height="234" sizes="100vw" caption="Components in an end-to-end video processing platform. (Image credit: <a href='https://blog.imgix.com/2022/01/18/video-api-limited-availability?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08'>imgix</a>)" alt="imgix video streaming requirements" >}}

## What Service Offers All Of These Features?

imgix has recently [released](https://imgix.com/solutions/video-api?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08) a Video API that meets all of these requirements. Your videos are automatically encoded and streamed from any cloud folder &mdash; and with native support for AWS S3, Google Cloud and Azure, imgix can fit seamlessly into your existing workflow.

The imgix API will create either HLS or MP4 versions of your video based on your needs, and you’ll have a customized playback URL to add to your website. You can see all your videos in [their Asset Manager](https://imgix.com/solutions/asset-management?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08), as well as detailed playback analytics. You also get an [out-of-the-box video player](https://imgix.github.io/ix-video/overview/?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08) that easily works in React, Vue, static HTML, and other popular frontend frameworks.

Most importantly, if you need to deliver a large number of images and videos, a solution like [imgix](https://imgix.com/?utm_medium=banner&utm_source=smashingmag&utm_campaign=video-api-smashingmag-article-2022-08) can optimize and process both types of assets without you having to build it from the ground up or cobble together different solutions. It’s truly a one-stop platform for visual media processing. 

{{< signature "vf, il" >}}
