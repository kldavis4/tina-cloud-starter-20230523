---
title: How We Built An iOS App To Shoot A 3D Video (Case Study)
slug: ios-app-3d-video-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf2b7c1-1831-43e8-b3fd-4f8631673ec7/shooting-process-500w-opt.jpg
date: 2017-07-12T20:39:20.000Z
author: evgenykhrolenokigormikheiko
summary: >-
  It wasn’t long after Hollywood released its first 3D films that the movie format quickly gained huge popularity worldwide. Thanks to developments in video-recording technology, any user can now shoot a video on their own. You can make a stereo record of memorable events in your life or create wonderful material for your business.
description: >-
  In this article, Evgeny Khrolenok and Igor Mikheiko share their lessons learned while developing an app to help folks create their very own 3D stereo videos. 
categories:
  - Mobile
  - Videos
  - iOS
  - Case Studies
---

Our team was also attracted to 3D filming. We thoroughly studied the features of the human visual apparatus and the technical details of stereoscopic photography. Then, we decided to develop an iOS app to shoot 3D videos and upload the videos to YouTube. The idea behind the app was to facilitate the shooting of 3D video by mounting two iPhones to a special frame &mdash; and we did it! That was how the [Stereo Video Recorder](https://itunes.apple.com/us/app/stereo-video-recorder/id1202260933) app appeared.

We have decided to share with Smashing Magazine’s readers our investigation into the creation of 3D video. We would also like to talk about the technical features of creating the application and provide detailed drawings of the framework used to mount the iPhones.

## How It All Began

In our study of 3D video features, we commenced with experiments on [virtual reality](https://www.smashingmagazine.com/2017/02/getting-started-with-vr-interface-design/). We constructed a cardboard frame and looked through it to the world via two iPhones in 3D format. Details of our research can be found [on our blog](https://www.instinctools.com/blog). We’ll go further here.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6954d891-aabc-497b-9807-8769da68a05b/cardboard-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f85b6f25-ae2b-459c-b064-879f3777baa6/cardboard-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>Cardboard made by us to study augmented reality (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6954d891-aabc-497b-9807-8769da68a05b/cardboard-large-opt.jpg">View large version</a>)</figcaption></figure>

Continuing this research, we decided to create another prototype of the application, one that allows you to record stereoscopic 3D video and upload it to YouTube.

Stereoscopy is a way of creating the illusion of depth in a flat image. Stereo recording has been known since the 19th century. In creating stereoscopic 3D video, we simulate binocular vision. Due to the distance between the pupils, it is much easier for the human brain to analyze the volume of surrounding space &mdash; the distance to objects. Binocular stereoscopy is widely used in the film industry. You can hardly come across a Hollywood masterpiece that doesn’t make use of stereo format.

The purpose of our app prototype was to shoot video simultaneously with two different iPhone cameras and then merge the resulting video files into one for viewing using any 3D glasses &mdash; for example, [Google Cardboard](https://vr.google.com/cardboard/), a virtual reality helmet or a 3D TV.

{{% feature-panel %}}

## Stereo Image And Our Perception Of A 3D Image

Let me elaborate on stereo images and our perception of 3D images. In fact, stereography works like our eyes, which evolved over time. Because there is a distance between our two eyes, the images projected onto the retinas of the left and right eyes are a little different. This difference is called parallax (an effect where the position of an object seems to be different when viewed from two different positions). However, the observer doesn’t see two separate images. The visual apparatus forms a perception of a single spatial image and can sense volume, distance, etc. It is important to understand that the visual apparatus detects, processes and projects spatial images and objects located in space at certain points.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8be3977-5136-4895-a130-9398b98ac0b9/visual-apparatus-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e4ef12f-ffa5-4493-9aba-1449c8d90e93/visual-apparatus-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>The visual apparatus creates a perception of volume based on parallax. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8be3977-5136-4895-a130-9398b98ac0b9/visual-apparatus-large-opt.jpg">View large version</a>)</figcaption></figure>

An understanding of how the human visual apparatus works allows for thorough investigation of how visual material needs to be prepared and reproduced so that the viewer can have a sense of a full 3D image.

Let’s look at everything in order.

Like any device that operates under the laws of physics, the human visual apparatus has its own features and limitations.

First of all, we need to understand that, in terms of our visual process, we focus our gaze on only a single point, called a point of view (POV). In fact, POV is the point where the eyes are focused and through which the left and right lines of sight pass. Depending on the distance to the POV, the angle between the lines of sight of the left and right eyes will be different. The eyes are directed such that the lines converge at the POV. These lines are parallel when the person looks into the distance, or, in other words, into infinity.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c7848e7-c1a6-42a6-a49e-e0bb3073b6d6/point-convergence-line-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfb5e060-4735-43c5-9e42-2a6e4c846fa5/point-convergence-line-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>The eyes do not always look in parallel &ndash; depending on the distance to the object (the point of convergence of lines). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c7848e7-c1a6-42a6-a49e-e0bb3073b6d6/point-convergence-line-large-opt.jpg">View large version</a>)</figcaption></figure>

Images projected onto the retina differ slightly due to the small displacement of the eyes. This is usually manifested in the form of displacement of the image that the person is looking at &mdash; to the left for the left eye, and to the right for the right eye. This phenomenon, already mentioned, is called parallax.

However, the visual apparatus can perceive volume only at certain parallax values. Depending on the distance to the object, the parallax will be different for near and far objects. It may be that the parallax exceeds the limit’s value and the person will see not a 3D object, but a bifurcated image. An experiment involving the switching of one’s view from near to far objects could offer a better understanding of the specifics of this.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b0364e2-051c-4e04-8a77-7bd9502bae73/side-effects-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6c958b1-6bb2-402a-8b2c-6735e77ffafd/side-effects-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>Perception of volume is only an illusion of our brain. In fact, there are certain side effects. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b0364e2-051c-4e04-8a77-7bd9502bae73/side-effects-large-opt.jpg">View large version</a>)</figcaption></figure>

As can be seen from the figure, if you fix your view on the foreground, then the background objects will begin to bifurcate. If you fix your view on the background, then the foreground image will bifurcate. This characteristic of the visual apparatus plays an essential role in the features of 3D shooting and the reproduction of stereo images.

In ordinary life, we don’t notice this effect because we are used to following only one object, and when you shift your view, your sight quickly adapts to the new conditions. However, when we try to artificially project a volumetric image using two pictures with a predetermined parallax, the visual apparatus can no longer adapt as quickly as it usually does. For the visual apparatus to work in a normal mode, the 3D video equipment must be adjusted to the viewer’s eyes, analyzing where the observation point is located. This equipment should also create stereo images with the required parallax.

However, implementing this is technically very difficult. Usually, a simple scheme with fixed geometric and technical shooting parameters is used. These parameters will be different for close-up and distant views. By geometric and technical parameters, we mean the field of view of the cameras, the horizontal displacement of the cameras from the center, the rotation angle of the cameras, and the convergence point of the cameras.

Therefore, you wouldn’t be able to shoot equally close and distant objects if you have only one set of shooting equipment (two cameras and a frame). More precisely, you could shoot, but it would be extremely uncomfortable for a person to watch a video in which, for example, the equipment is adjusted for a distant view but shoots a close-up view, or vice versa, with the stereo effect weakly expressed in the background.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbfd136-44d2-4155-9a25-f18140b5e7fb/configure-shooting-system-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87dce92f-7dd1-4a6d-94ab-35543615ce05/configure-shooting-system-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>The shooting system must be configured to match the parameters of the human visual system under certain observation conditions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbfd136-44d2-4155-9a25-f18140b5e7fb/configure-shooting-system-large-opt.jpg">View large version</a>)</figcaption></figure>

## From Idea To Practice: How To Mount The iPhones

Let’s return to our idea. We decided to develop a mobile app prototype that can record stereo 3D video. Considering all of the above, we needed to assess the following:

*   the basic possibility of shooting a stereo image using two iPhones;
*   the effective range of distances that would ensure high-quality and comfortable stereo perception, taking into account the usual conditions of using a camera.

When we came very close to creating a prototype, the first thing we did was evaluate the potential of the iPhone camera for our task. We were pleasantly surprised to discover that the iPhone gives an acceptable angle of view for a close-up shot. As already mentioned, just placing two cameras side by side isn’t enough to get a good stereo effect. Usually, the algorithm for calculating the shooting begins with setting the plan’s parameters &mdash; that is, the distances to the nearest and farthest objects, and the distances between objects in the frame’s plane. The installation parameters are then selected based on these data.

A simplified calculation of the distance between cameras can be done based on this formula:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5ad5ac3-1858-4b3f-91c4-7d0ac7fe5971/formula-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0637c9f-dc4f-46b0-8636-43281f2ab6aa/formula-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5ad5ac3-1858-4b3f-91c4-7d0ac7fe5971/formula-large-opt.jpg">View large version</a>)</figcaption></figure>

*   `Parallax<sub>fore</sub>` sets the maximum displacement of the foreground image when the stereo pair frames overlap each other.
*   `L<sub>fore</sub>` = distance to the foreground object
*   `f` = focal length of the lens
*   `L` = distance to the focal point of the lens
*   `M` = frame zoom

In our case, we had to slightly change the algorithm, because we were using a standard camera, and, accordingly, the focal length of the lens is rigidly set. Our task was to get a comfortable stereo effect and an acceptable range of distances to the shooting object. So, we needed to carry out several experiments &mdash; arranging both cameras relative to each other &mdash; in order to find the required distance between their centers (the distance between the centers of the cameras) and convergence angles.

To simplify the task in the prototyping process, we decided not to rotate the cameras to achieve convergence at a certain point, but to use convergence at infinity. It turned out that, to obtain the best result, it is necessary to accurately adjust the cameras’ convergence angle. And if we take into account the fact that we planned to make a cardboard frame to be used to mount the iPhones, then adjusting the cameras’ convergence angle becomes practically impossible. So, after a number of experiments, we arrived at a compromise, obtaining the optimal balance between the distance between the cameras to enable shooting in the near zone and getting a good stereo effect.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dd47203-ae48-491f-91d5-642bb5da03dc/phone-distance-large-opt.png"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b45ec564-89c5-4a69-91c6-295a8d2bc556/phone-distance-800w-opt.png" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>To achieve a good stereo effect and minimize adverse physiological effects, the distance between the phones must be strictly fixed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dd47203-ae48-491f-91d5-642bb5da03dc/phone-distance-large-opt.png">View large version</a>)</figcaption></figure>

Our aim was to develop the simplest frame for the iPhones, one that would be easy to manufacture, be convenient to operate, provide the necessary shooting parameters and have the required rigidity. So, we chose a 3D model that can be made of plastic or foam material (polystyrene, in this case) by milling or 3D printing. In the future, we will, of course, want to develop a device that is simpler to make &mdash; for example, a cardboard device.

{{% ad-panel-leaderboard %}}

The only hardware limitation at the moment is that you need to use the same devices, with absolutely identical cameras.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df6319af-0c62-453c-b6de-0c4d6a58622d/3d-video-frame-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58fb5211-12b5-4f1e-a69e-f8ed6e45a454/3d-video-frame-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e048128-d490-4269-ba17-55164b452a00/3d-video-frame-1-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/845718d5-06b6-4fb0-ad99-fbc2b67bcf8a/3d-video-frame-1-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>Simplest version of a 3D video shooting frame (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df6319af-0c62-453c-b6de-0c4d6a58622d/3d-video-frame-large-opt.jpg">View large version</a>)</figcaption></figure>

Below are detailed drawings of the frame for different versions of devices with screen sizes of 4.0, 4.7 and 5.5 inches &mdash; suitable for the iPhone 6+ and 6S+, for the 6, 6S and 7, and for the 5 and 5S.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67f5932a-7eba-4e49-af10-edb0bd762f01/drawing-6-plus-large-opt.png"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7c53f7-ef74-4044-a6c0-41a2f3fc1098/drawing-6-plus-800w-opt.png" alt="How To Shoot a 3D Video With Two iPhones." /></a><br />
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/965ebb7e-a0bd-4f9b-afda-215265877062/drawing-6-7-large-opt.png"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e46f182-61c4-4705-8264-52b3034da808/drawing-6-7-800w-opt.png" alt="How To Shoot a 3D Video With Two iPhones." /></a><br />
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07ea7367-cd5d-4f87-a133-0d054234e349/drawing-5s-large-opt.png"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea9f53db-041b-453f-902d-02d7e51239c7/drawing-5s-800w-opt.png" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>Drawings for your own homemade frame</figcaption></figure>

## App For Stereoscopic 3D Video Shooting

The app runs simultaneously on two devices, but the shooting is controlled from only one of the devices, so there is no need to control the shooting process in some special way.

In simplified form, the standard use scenario for the application consists of the following sequence of actions:

1.  Mount the two iPhones to the frame.
2.  Run the app on the two devices.
3.  Determine which of the devices will serve as the master and which as the slave. Start recording from the master device. (Take no additional action on the second device.)
4.  After recording, wait for synchronization of the recorded fragments and rendering of a video ready for uploading to YouTube.
5.  Upload the video to YouTube at any time after synchronization, and then view it on your 3D TV or via virtual-reality glasses.

It is worth noting that the main work takes place on only one of the iPhones, the master device. It’s on this iPhone that we initiate shooting. The video is processed and uploaded to YouTube also on the master device. It takes some time to prepare the video for uploading to YouTube. This will depend on the performance of the devices used and on the quality of the connection between the master and slave devices.

The second iPhone, acting as the slave, is used only as a second camera. At the end of shooting, it sends the video fragment to the master device.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f266482-0052-4283-87bf-cad3be251178/shooting-process-large-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8de12e98-0acb-408e-865b-c1af406fe48b/shooting-process-800w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>The 3D video-shooting process looks something like this. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f266482-0052-4283-87bf-cad3be251178/shooting-process-large-opt.jpg">View large version</a>)</figcaption></figure>

The screenshots of the main screen of the app, displaying the gallery of videos shot, are shown below. The videos can be viewed both via an embedded player and on YouTube. Here, you can also watch how further shooting roles (master and slave) are assigned to the devices.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242fd45b-79a9-4557-8e06-67018cd1b61e/ui-app-680w-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242fd45b-79a9-4557-8e06-67018cd1b61e/ui-app-680w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><br />
<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61470f44-5c12-4b43-9c3b-45cf44dcd08d/ui-app-1-680w-opt.jpg"> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61470f44-5c12-4b43-9c3b-45cf44dcd08d/ui-app-1-680w-opt.jpg" alt="How To Shoot a 3D Video With Two iPhones." /></a><figcaption>The user interface of the app</figcaption></figure>

## Technical Hurdles

### Desynchronization

All of the manipulations with the video fragments are performed with the help of the powerful framework AVFoundation, using, if possible, hardware acceleration.

To upload to YouTube, the video fragments are glued frame by frame, side by side. Obviously, every left frame should match with the right frame by time. With the slightest delay in the frames of one of the sources, the stereo effect will be lost or distorted (especially in dynamic scenes), and the picture will appear doubled.

To resolve this issue, we started recording video on the devices at the same time. In fact, the recording starts not immediately after pressing the start button, but after a short delay within which a certain algorithm activates &mdash; very similar to how the precision time protocol (PTP) measures clock skew. So, we were able to initiate video recording with a 30- to 50-millisecond divergence, which, in the worst case scenario, corresponds to approximately 1 desynchronization frame.

### Bugs in iOS Multipeer Connectivity

We used the native iOS library Multipeer Connectivity to establish communication between the two devices. This library establishes a direct connection between devices on the same Wi-Fi network, as well as via Bluetooth or using something similar to Wi-Fi Direct on the iPhone. Thus, you can shoot and synchronize video fragments even in an open field, without a wireless or mobile Internet network. But an Internet connection is needed to send the video to YouTube from the master device.

The main reason we decided to use this library is that it establishes communication between the two devices when not connected to the same network. Obviously, under poor stereo 3D shooting conditions, the most that can be expected is a 3G connection. To shoot a 3D video, it is vital to be able to – with minimum delay – transmit data packets for synchronization. In addition, if there were no Internet connection, we wouldn’t be able to shoot. Therefore, the Multipeer Connectivity library became a lifeline. Besides, it is a native solution for the Apple platform.

However, it is worth noting that not everything went exactly as we wanted. While integrating with Multipeer Connectivity, many bugs were detected, and the entire library was extremely unstable in its operation. Most of the declared features were only there in theory. When the devices operate within the same network segment, Multipeer Connectivity operates more effectively; the connection is established for an acceptable period of time; permissible dispersion of message-delivery time is achieved.

However, if we have, relatively speaking, poor stereo 3D shooting conditions, or, say, there are many mobile devices in one place, then establishing a connection becomes akin to a lottery. One gets the feeling that the Apple library is not yet fully developed and is still quite raw.

### Linking the Devices

We implemented the automatic linking protocol in the early version of our prototype. The protocol itself consists of a set of rules by which a coordinator is chosen among peer devices – based on a majority – at the initial timepoint.

Next, the coordinator periodically collects telemetry statistics from each device by passing a special marker in a circle between the slave devices. Based on these telemetry data, pairs of devices mounted to the frame are compared. After a pair has been identified, a master and slave are assigned in the pair, and a direct connection between them is established. At this stage, linking is complete.

{{% ad-panel-leaderboard %}}

### Automatic and Independent Searches

When necessary, automatic and independent searches (based on unique identifiers) for devices that had participated in the previous sessions were performed for synchronization (obtaining recorded video tracks in the event that data failed to load to the master device at the time of recording). Accelerometer readings were mainly used to identify which devices corresponded to the pair. The coordinator calculated the correlation between potential pairs. If the correlation exceeded a certain threshold, the devices were considered potential pairs and the secondary features were subsequently tested.

Because we couldn’t fully overcome the above-mentioned problems with Multipeer Connectivity, we decided to temporarily abandon automatic linking, because this would have affected the average user very negatively and spoilt the user experience.

## What We Ended Up With

In the end, we achieved a very interesting and high-quality app. Watching a video recorded via this app gives you the same feeling you get from watching 3D movies at the theater.

Of course, the human eye works a little differently: Its lines converge at a certain point in space and depend on the point of focus. In our case, the eyes always look in parallel. However, even with this fact, the stereo effect is very pronounced: The volume of space is felt at the foreground, midground and background about the same as on the screen.

You need VR glasses or 3D TV to view this video properly.

So, we have made it possible to use the Stereo Video Recorder app to shoot 3D stereo video on your own for your business needs or just for fun!

## Working On Bugs And Future Plans

Our goal was achieved: We studied the criteria for creating 3D video, and we created an app that enables any user to create a stereo video. But it’s not all as easy as it sounds. We need to work on some things. We had many problems with the Multipeer Connectivity library. We want to either replace it or find a workaround so that the app works well with limited Internet access.

We also need to:

*   implement synchronous focusing and exposure metering on the two devices, as well as implement recording of stereo audio tracks;
*   develop a more pragmatic frame for the devices;
*   integrate the automatic device-pairing mechanism;
*   provide support for different device options and be able to handle different video resolutions (at the moment, we can shoot video only with the same iPhone versions &mdash; for example, an iPhone 5S can only be paired with another iPhone 5S);
*   create an Android version of the app.

Our Stereo Video Recorder app is already in the [App Store](https://itunes.apple.com/us/app/stereo-video-recorder/id1202260933). You can use it to create 3D video. We are sure that the technology will continue to develop and that there will eventually be many more solutions for creating stereoscopic video. We will try to keep pace with the times.

Please leave your comments and ideas on your use of this app. We would be grateful for your opinion and feedback.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Four Ways To Build A Mobile Application, Part 1: Native iOS](https://www.smashingmagazine.com/2013/11/four-ways-to-build-a-mobile-app-part1-native-ios/)
*   [Prototyping iOS And Android Apps With Sketch (With A Freebie)](https://www.smashingmagazine.com/2015/01/prototyping-ios-android-apps-sketch-freebie/)
*   [The Future Of Video In Web Design](https://www.smashingmagazine.com/2013/11/the-future-of-video-in-web-design/)
*   [The Basics Of Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)

{{< signature "da, vf, al, il" >}}
