---
title: A Guide To Simple And Painless Mobile User Testing
slug: simple-and-painless-mobile-user-testing
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/440a9273-d414-4566-8f70-d44adb25bd8a/user-testing-overview-setup-500-opt.png
date: 2015-12-01T18:56:56.000Z
author: colmanwalsh
description: >-
  The incredible growth of mobile and the proliferation of mobile devices has
  made the UX designer’s job more challenging and interesting. It also means
  that **user-testing mobile apps and websites is an essential component of the
  UX toolkit**.

  But unlike the desktop environment, no out-of-the-box software packages such
  as Silverback or Camtasia are specifically designed to record mobile usability
  tests. Even if you’re not developing a mobile app, chances are that a large
  proportion of your website traffic is coming from mobile. Running **regular
  mobile usability tests** is the only way to gauge how well this channel is
  working for your customers.
categories:
  - Mobile
  - Testing
  - UX
---
The incredible growth of mobile and the proliferation of mobile devices has made the UX designer’s job more challenging and interesting. It also means that <strong>user-testing mobile apps and websites is an essential component of the UX toolkit</strong>.

But unlike the desktop environment, no out-of-the-box software packages such as Silverback or Camtasia are specifically designed to record mobile usability tests.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Field Guide To Mobile App Testing](https://www.smashingmagazine.com/2012/10/a-guide-to-mobile-app-testing/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Applying Participatory Design To Mobile Testing](https://www.smashingmagazine.com/2014/09/applying-participatory-design-to-mobile-testing/)

Even if you’re not developing a mobile app, chances are that a large proportion of your website traffic is coming from mobile. Running <strong>regular mobile usability tests</strong> is the only way to gauge how well this channel is working for your customers.

{{% feature-panel %}}

A bit of hacking is required. And, after years of experimentation, we think we’ve figured out the best hack available yet. If you want to test iPhone or Android experiences, this solution is simple, cost-effective and high quality.</p>

## The Old Hack: Wires And Duct Tape

In days gone by, we used a “sled” to <strong>mount a smartphone and camera</strong> into a position where we could record what users were doing on screen. (To create the sled, we bought some acrylic in a hardware store and bent it into shape over a toaster. Fun.)

We attached a webcam to the sled with duct tape and mounted the phone with tape and some velcro strips. Looking back, the device was pretty crude. It wasn’t a natural experience for users, who would often cradle the phone in two hands to keep the sled steady.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb6f39b-f487-4769-8cc4-031343c4b1c2/mobile-testing-old-way-opt.jpg"><img title="Smartphone on a sled" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e48eb3d9-60a5-40f6-91f9-0abac74d84bf/mobile-testing-old-way-500-opt.jpg" alt="Smartphone on a sled" /></a><figcaption>A user with smartphone and camera mounted on a sled. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb6f39b-f487-4769-8cc4-031343c4b1c2/mobile-testing-old-way-opt.jpg">View large version</a>)</figcaption></figure>

Technically, it wasn’t reliable. Because we were using two cameras on one laptop (the camera on the sled and the laptop’s built-in camera), we had to have two camera apps open at the same time. This led to flaky performance. Either setting it up would be a stressful time or we’d get a blackout in the middle of a test — or, often, both.

And there were other issues, such as screen glare and camera focus. Overall, it was <strong>time-consuming to set up</strong>, with unreliable performance and a suboptimal testing environment. It was particularly stressful if clients were around, but it was the best solution we knew at the time.</p>

## A Better Way: Wireless

Ideally, testing equipment and software should be invisible to the users. We want as natural an environment as possible, just the users and their smartphones — no wires, sleds, cameras or duct tape.

For the UX team, the focus should be on learning and insight. We don’t want to be sweating over the setup or worrying about blackouts.

I'd like to introduce you to a simple setup that achieves all of these goals. It allows the UX team to focus on what really matters, and lets users focus on their phones. And it’s so reliable that we regularly use it in front of clients and during our training classes.

We’ll focus here on <strong>testing usability on smartphones, using a MacBook as the recording device</strong>. But the approach works with Windows PCs, too.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e957132-cedc-4fc4-a257-c5a7d39dbef7/mobile-testing-wireless-opt.jpg"><img title="Wireless testing is more natural" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/101deb15-8a52-4e38-89d7-47f1467888da/mobile-testing-wireless-500-opt.jpg" alt="Wireless testing is more natural" /></a><figcaption>Wireless testing is more natural. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e957132-cedc-4fc4-a257-c5a7d39dbef7/mobile-testing-wireless-opt.jpg">View large version</a>)</figcaption></figure>

### Step 1: Install Software

The magic ingredient in this setup is Apple’s wireless <strong>AirPlay</strong> technology. This is the software that lets you stream music or videos wirelessly to an Apple TV.

So, the first software you’ll need to buy (for $15) and install is <a href="https://www.airsquirrels.com/reflector/">Reflector</a>, which converts your laptop into an AirPlay receiver, just like an Apple TV. This allows us to mirror the user’s smartphone screen onto the laptop: Whatever is on the user’s smartphone will also be seen on the laptop.

Now we have a scenario in which we don’t need an external camera to record the user’s smartphone screen. We just need screen-capturing software to record the smartphone on the laptop. My personal favorite is <a href="https://www.telestream.net/screenflow/overview.htm">ScreenFlow</a> ($99), for two reasons. It’s reliable, and it uses the laptop’s camera to record the user’s face during the session, an essential component of any usability test.</p>

### Step 2: Set Up Monitor

This step is optional, but I like to <strong>use an external display</strong> so that the facilitator and notetaker don’t have to peer over the user’s shoulder to see the action. It also minimizes distraction for the user; they won’t see a giant version of their smartphone on the laptop in front of them — it will be on the monitor instead.

So, run an extension cable from your MacBook to the monitor. If the monitor and the laptop are showing the exact same thing, that means they’re being mirrored, which we don’t want. Open up “System Preferences” and select “Displays,” and make sure the box for “Mirror Displays” is unchecked.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f60bcc7f-bc43-4c9f-ac12-a181dd1686b1/mac-system-preferences-opt.png"><img title="The correct display preferences for your Mac" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9856f76f-f64e-4407-98d8-fe89428c4385/mac-system-preferences-500-opt.png" alt="The correct display preferences for your Mac" /></a><figcaption>The correct display preferences for your Mac. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f60bcc7f-bc43-4c9f-ac12-a181dd1686b1/mac-system-preferences-opt.png">View large version</a>)</figcaption></figure>

### Step 3: Set Up Reflector

To start beaming the smartphone to the laptop, open Reflector on your Mac. You’ll see the Reflector icon in the toolbar in the top left of your screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55c1c38a-fe0d-4da2-8d7e-7276fbaa57e9/mac-reflector-toolbar-opt.png"><img title="You'll see this icon when Reflector is open" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/862e6d53-cd69-42c2-aa4f-735ecec424c8/mac-reflector-toolbar-500-opt.png" alt="You'll see this icon when Reflector is open" /></a><figcaption>You’ll see this icon when Reflector is open. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55c1c38a-fe0d-4da2-8d7e-7276fbaa57e9/mac-reflector-toolbar-opt.png">View large version</a>)</figcaption></figure>

### Step 4: Mirror Your Smartphone

Now we come to the magic part. If you’re using an iPhone, swipe up from the bottom of the screen, and enable AirPlay. Then select your MacBook from the list (in this example, it’s “Colman’s MacBook Pro”). Finally, flick the “Mirroring” switch to active (green).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5ec94be-5fd9-4d6c-bb18-5c1958d1bc4d/ios-mirroring-setup-opt.png"><img title="Turning on mirroring on your iPhone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f15df13d-c45c-41bc-bffc-437f87c4076a/ios-mirroring-setup-500-opt.png" alt="Turning on mirroring on your iPhone" /></a><figcaption>Turning on mirroring on your iPhone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5ec94be-5fd9-4d6c-bb18-5c1958d1bc4d/ios-mirroring-setup-opt.png">View large version</a>)</figcaption></figure>

Your iPhone should now appear in the middle of your external monitor. Magic! (If the iPhone appears on your MacBook’s screen, just drag it onto the external monitor.)

For devices with Android 4.4.2 or higher, swipe down from the top of your screen to access the settings. Select the “Cast screen” option, and then select your MacBook.</p>

<strong>Note:</strong> Your smartphone and MacBook need to be on the same Wi-Fi network for any of this to work. It’s the first thing to do when troubleshooting if you can’t get it to work right away.</p>

### Step 5: Set Up ScreenFlow

To start recording, open ScreenFlow; the new recording configuration box will appear. You’ll need to adjust the following three settings:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58769161-4202-49b2-b8c5-c79400c2284a/screenflow-recording-setup-opt.jpg"><img title="Setting up ScreenFlow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da47c00d-50aa-407b-a5b1-05132c0ed188/screenflow-recording-setup-500-opt.jpg" alt="Setting up ScreenFlow" /></a><figcaption>Setting up ScreenFlow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58769161-4202-49b2-b8c5-c79400c2284a/screenflow-recording-setup-opt.jpg">View large version</a>)</figcaption></figure>

*   “Record desktop from” Check this and make sure to select the external monitor from the dropdown menu (“2270W” in the example below).
*   “Record video from” Check this and select “FaceTime HD Camera (Built-in),” which is the default option.
*   “Record audio from” Check this and select “Built-in microphone.”

### Step 6: Start Recording the Test

Position the user directly in front of the MacBook. You should see their face in the ScreenFlow preview. Then, press the large red record button. That’s it — you are now recording.

As you and the notetaker are watching the action on the monitor, the user will be sitting in front of a blank laptop, using their smartphone as they normally would — no wires, duct tape, cameras or intrusive mounts.

In the screenshot below, I’m playing around with Spotify on my iPhone. You can see that, as well as capturing the smartphone’s screen, ScreenFlow also provides a picture-in-picture display of the user, perfect for usability testing.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/582fe3d4-4efe-4224-8a8e-455cfa721b24/screenshot-of-recording-opt.png"><img title="A screenshot of the recording output of ScreenFlow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63caf49d-be4f-4be0-bfe1-010e2c66064a/screenshot-of-recording-500-opt.png" alt="TA screenshot of the recording output of ScreenFlow" /></a><figcaption>A screenshot of the recording output of ScreenFlow. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/582fe3d4-4efe-4224-8a8e-455cfa721b24/screenshot-of-recording-opt.png">View large version</a>)</figcaption></figure>

Granted, the recording won’t show the user’s fingers interacting with the device. But the overall benefits of this technique are so numerous (see the list below) that the trade-off is justifiable.</p>

### Overview of Setup

To be clear, let’s review what your setup should look like. The user should be sitting in front of the MacBook, with the smartphone in their hand. And the facilitator and notetaker (if you have one) should be sitting nearby, looking at the external monitor.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a9eed8-b3e6-4d71-bcb0-05c54cf57d3c/user-testing-overview-setup-opt.png"><img title="Room setup" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/440a9273-d414-4566-8f70-d44adb25bd8a/user-testing-overview-setup-500-opt.png" alt="Room setup" /></a><figcaption>How the room and screens should be set up for the test. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a9eed8-b3e6-4d71-bcb0-05c54cf57d3c/user-testing-overview-setup-opt.png">View large version</a>)</figcaption></figure>

Keep the monitor pointed away from the user. It can get distracting seeing their smartphone flashing on the big screen.</p>

## Conclusion

There are so many advantages to this approach that it would be worth listing them:

*   **Simple**.  After your first time getting things together, setup takes about five minutes the second time.
*   **Reliable**.  It’s not perfect, but crashes and setup issues are rare. With the sled-and-camera approach, however, problems were par for the course.
*   **Cost-effective**.  You can have this solution in place for less than $200 if you’re using a MacBook. (By comparison, Morae, the high-end usability testing software, sells for $2,000.)
*   **Professional**.  The output is high-quality and professional. It doesn’t look like a hack. We’ve shared our recordings with clients, executives, everybody.
*   **Flexible**.  The solution works with the major platforms: PC, Mac, Android and iOS.
*   **Convenient**.  Finally, because you don’t need any duct tape or velcro, test participants can use their own phones. This makes your tests even more natural and effective.</p>

### More Resources

*   [Reflector](https://www.airsquirrels.com/reflector/) For converting your laptop into an AirPlay receiver. Mac and PC versions available.
*   [ScreenFlow](https://www.telestream.net/screenflow/overview.htm) For screen recording and picture-in-picture on your Mac.
*   [Camtasia](https://www.techsmith.com/camtasia.html) For screen recording and picture-in-picture on your PC.
*   “[Quick Tip: Make Your Own iPhone Usability Testing Sled for £5](https://www.90percentofeverything.com/2010/05/07/quick-tip-make-your-own-iphone-usability-testing-sled-for-5/),” Harry Brignull The original blog post.

{{< signature "alda, ml, jb" >}}

