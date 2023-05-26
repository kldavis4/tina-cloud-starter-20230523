---
title: Dropbox’s Carousel Design Deconstructed
slug: dropbox-carousel-design-deconstructed-part-1
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32d05d93-de17-4fb5-8039-eaa90c8f0741/dropbox-carousel-part-1-illu.jpg
date: 2014-08-26T17:00:10.000Z
author: chrisbank
description: >-
  Many of today’s hottest technology companies, both large and small, are
  increasingly using the concept of the minimum viable product (MVP) as way to
  iteratively learn about their customers and develop their product ideas. By
  focusing on an integral set of core functionality and corresponding features
  for product development, these companies can efficiently launch and build on
  new products.

  While the concepts are relatively easy to grasp, the many trade-offs
  considered and decisions made in execution are seldom easy and are often
  highly debated. This two-part series, looks into the product design process of
  Dropbox’s Carousel and the product team at UXPin shares our way of thinking
  about product design, whether you’re in a meeting, whiteboarding, sketching,
  writing down requirements, or wireframing and prototyping.
categories:
  - UX
  - UX
  - Case Studies
  - Product Strategy
---
Many of today’s hottest technology companies, both large and small, are increasingly using the concept of the minimum viable product (MVP) as way to iteratively learn about their customers and develop their product ideas. Jump to <a href="https://www.smashingmagazine.com/2014/09/dropbox-carousel-design-deconstructed-part-2/">Part 2 of this case study</a>.

By focusing on an integral set of core functionality and corresponding features for product development, these companies can efficiently launch and build on new products. While the concepts are relatively easy to grasp, the many trade-offs considered and decisions made in execution are seldom easy and are often highly debated.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [10 Requirements For Making Home Page Carousels](https://www.smashingmagazine.com/2016/07/ten-requirements-for-making-home-page-carousels-work-for-end-users/)
*   [An Exploration Of Carousel Usage On Mobile E-Commerce Websites](https://www.smashingmagazine.com/2015/02/carousel-usage-exploration-on-mobile-e-commerce-websites/)
*   [<span class="headline">It’s Crazy Powerful. It’s Magical. Already Know How To Use It.</span>](https://www.smashingmagazine.com/2012/09/you-already-know-how-to-use-it/)

This article looks into the product design process of Dropbox’s Carousel and the product team at UXPin shares our way of thinking about product design, whether you’re in a meeting, whiteboarding, sketching, writing down requirements, or wireframing and prototyping.

{{% feature-panel %}}

## The Carousel MVP

<a href="https://techcrunch.com/2014/04/09/dropbox-debuts-carousel-aiming-to-be-the-go-to-storage-app-for-your-entire-photo-archive/">It’s been reported</a>, that Dropbox wants Carousel, its new mobile photo and video gallery app, to be “the go-to place for people to store and access their digital photos [and videos],” to be the “one place for all your memories.” In effect, Carousel allows you to access all of your photos and videos stored in a Dropbox account on any device, unifying them in a single interface that automatically sorts files by time and location.

More specifically, the app launched with several key features:

*   **Backing up**.  It integrates directly with Dropbox’s file storage to save all photos and videos taken on your mobile phone.
*   **Viewing**.  A cloud-based media gallery displays all of your photos and videos without taking up local storage on your phone.
*   **Sharing**.  It offers many ways for you to share photos and videos with others, primarily by sending links to view them in Carousel.
*   **Discussing**.  A new chat thread is created for every group of people with whom you share a collection of pictures or videos.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/623c7f44-c56f-4ea4-a3ba-b8cb0b6c671a/02-carousel-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5884f89-005f-40ab-af0f-8600c013273a/02-carousel-opt-500.jpg" alt="Carousel screenshots of backup, viewing, sharing &amp; discussing." width="500" height="220" /></a><figcaption>Carousel screenshots of backup, viewing, sharing &amp; discussing. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/623c7f44-c56f-4ea4-a3ba-b8cb0b6c671a/02-carousel-opt.jpg">View large version</a>)</figcaption></figure>

Since launching, Carousel has received polarizing reviews. Amidst this uproar of praise and feature requests, we’ll go over how any product or design team could arrive at the same initial release — a critical exercise, especially in a market as crowded as the one for photo apps. First, we’ll summarize what Carousel is, then break down part of the design process for this MVP, and then compare the UI and UX to existing design patterns such as Apple’s Photos, Instagram, Google+, Camera+, Flickr, Facebook, Picturelife and Dropbox Photos itself.

You can be sure that the product team’s meetings sound little like this:
<blockquote>“Photos are hot.”

“People store a lot of photos on Dropbox.”

“So, let’s build a mobile gallery.”

“Want to copy Apple’s Photos but integrate it with Dropbox?”

“Sure, but we also need to copy Facebook Messenger because we’re social, too.”

“OK, draw some sketches, make some wireframes, create the final mockups and build a high-fidelity prototype.”

“Ready to ship to 275 million users?”

“Launch!”</blockquote>

Now that we have an idea of what Carousel is, let’s consider how the team might have gone about designing the app.</p>

## Core Users

Carousel clearly targets consumers, both young and old, rather than professionals or enterprises. No question about that. This is clear from the interface and the <a href="https://byalicelee.com/carousel/">visual design choices</a>, marked by a youthful montage of two personas, Nora and Owen (yes, they have names), who we see growing up.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f3c6835-1dda-40a7-8c4d-64e336a7b331/03-carousel-core-use-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e3a672f-12b6-4546-86ce-c617dbb97d31/03-carousel-core-use-opt-500.jpg" alt="Carousel’s core users: Nora and Owen, your everyday consumer" width="500" height="123" /></a><figcaption>Carousel’s core users: Nora and Owen, your everyday consumer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f3c6835-1dda-40a7-8c4d-64e336a7b331/03-carousel-core-use-opt.jpg">View large version</a>)</figcaption></figure>

## Users needs

A lot of decisions need to be made here because the market already has literally hundreds of apps for taking and managing photos. A few of the main use cases for these photo apps are:

*   taking photos (i.e. with the camera);
*   editing photos (with filters or advanced editing);
*   backing up and syncing across devices;
*   viewing;
*   managing (tagging, arranging, moving, deleting or hiding);
*   sharing (privately or publicly);
*   discussing (privately or publicly).

Clearly, a lot of user needs could be met by the first version of the product. But where to start? Francine Lee, now a UX researcher at Dropbox, took an initial stab at answering this question with a <a href="https://medium.com/@___fl/a-guerilla-usability-test-on-dropbox-photos-e6a1e37028b4">guerilla usability test</a> on Dropbox’s existing solution, Dropbox photos. I’m going to take her work a few steps further.</p>

## Business Goals

In general, Dropbox cares about the growth and monetization of its core business. This is what most companies, hot or not, care about.

Specifically, the company wants to continue growing its overall user base (whether those users come from the main Dropbox app or from Carousel), driving new users to its main service of backing up and syncing files, upselling them on larger plans, and keeping everyone as engaged and happy as possible.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e43dd8f-518a-4107-8d30-8e7f1a2e5d94/04-carousel-opt.jpg" alt="Carousel was built to help Dropbox grow" width="501" height="217" /><br>
<figcaption>Carousel was built to help Dropbox grow.</figcaption></figure>

So, how does this overlap with users’ needs and, ultimately, with the solution that needs to be designed and built?

## Existing Design Patterns And Their Gaps

Let’s look at relevant products and design patterns that satisfy both user and business needs, as well as identify any gaps that Carousel might fill. If you’re interested in learning more, check out UXPin’s ebook <a href="https://uxpin.com/mobile-design-patterns.html"><em>Mobile UI Design Patterns</em></a>.

We’ll review a few existing mobile photo galleries and other design patterns to understand why Dropbox’s Carousel looks so similar to Apple’s native Photos app as well as Instagram’s direct-messaging feature, which, not coincidentally, is similar to Facebook’s Messenger app. Beyond the fact that <a href="https://lifehacker.com/5814341/the-best-photo-management-app-for-iphone">Apple has made it nearly impossible</a> for third-party developers to build a better app, we believe that Dropbox has taken this path for many reasons. And we have much inspiration to take from Instagram.

Because Carousel targets the average consumer, we’ll also look at media-gallery applications that target this user base with a strong mobile presence — after all, eyeballs and engagement are going in the direction of mobile. As such, we didn’t look as much into desktop and web-first apps such as iPhoto, Picasa and Unbound or into power-user applications.

Instead, we’ll focus on Apple’s Photos, Instagram, Google+, Camera+, Flickr, Facebook, Picturelife and Dropbox Photos itself. In “<a href="https://www.theverge.com/2013/8/29/4560364/best-cloud-storage-photo-apps">The Best Photo Apps for Keeping Your Memories in the Cloud</a>,” The Verge analyzes existing solutions in depth and validates our focus on these types of products in evaluating Carousel’s MVP.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/431b2e5b-4bf8-4e61-b372-40b8bc872dfe/05-app-comparison-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9122ad35-ea15-41e0-bedf-7e2e6b3e989c/05-app-comparison-opt-500.jpg" alt="A comparison of photo apps" width="392" height="600" /></a><figcaption>A comparison of photo apps. (Image credit: <a href="https://www.theverge.com/2013/8/29/4560364/best-cloud-storage-photo-apps">The Verge</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/431b2e5b-4bf8-4e61-b372-40b8bc872dfe/05-app-comparison-opt.jpg">View large version</a>)</figcaption></figure>

Given that Loom, a popular photo and video gallery app, was acquired by Dropbox within a week after Carousel launched and then decommissioned a month later in May 2014, we did not include it in this discussion. Everpix also <a href="https://www.theverge.com/2013/11/5/5039216/everpix-life-and-death-inside-the-worlds-best-photo-startup">recently went out of business</a>, so we cannot mention much about it either. To give you an idea of how competitive this space is, Everpix was giving away a free two-year trial just for downloading the desktop app, uploading some photos and linking it to a smartphone.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd4dfdcd-3088-4fcc-83c1-867f906eb07f/06-demo-video-opt.jpg" alt="A demo video of the leading photo application" width="500" height="280" /><br>
<figcaption>A demo video of the leading photo application. (Image credit: Loom.com)</figcaption></figure>

### Taking Photos

Below are screenshots of Instagram, Apple’s Camera and Flickr.

They all provide roughly the same functionality (including filters), and all allow users to save copies of photos to their phone’s camera roll, which Dropbox already seamlessly backs up and syncs to the cloud when users opt in. Users don’t need any more options for taking photos, so building this into Carousel’s initial functionality wouldn’t make sense for Dropbox.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26bb346a-2824-4b49-b2e2-b128c067d809/07-instagram-apple-flickr-apps-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b5ac9d-adbc-410f-b1a7-f4f33d003286/07-instagram-apple-flickr-apps-opt-500.jpg" alt="Instagram, Apple Camera, and Flickr Mobile Apps, respectively." width="500" height="289" /></a><figcaption>Interface for taking photos in Instagram, Apple Camera, and Flickr Mobile Apps, respectively. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26bb346a-2824-4b49-b2e2-b128c067d809/07-instagram-apple-flickr-apps-opt.jpg">View large version</a>)</figcaption></figure>

Not only does a camera not belong in Dropbox’s core user experience today, but it wouldn’t complement the myriad of other digital cameras out there. By not building camera functionality into Carousel, Dropbox both minimizes development risks and plays nice with the majority of the market for capturing photos and videos, both apps and hardware alike. It just wants the picture once you’ve taken it.</p>

### Editing: Filters and Advanced Editing

Below are screenshots of Apple’s Photos, Instagram and Camera+.

As you can see, you’ll also have to consider a myriad of photo- and video-editing options. Enough reasonable solutions seem to be on the market. Again, most of these products allow users to save original and edited copies to their phone’s camera roll, which Dropbox already seamlessly backs up and syncs to the cloud when users opt in.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b4f40d5-73a7-449b-a4ca-f6bb5ed724d1/08-apple-instagram-cameraplus-apps-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0bead4c-d5f1-4d72-806b-1fa5991aa99c/08-apple-instagram-cameraplus-apps-opt-500-78x45.jpg" alt="Apple Photos, Instagram, and Camera+ Mobile Apps, respectively." width="500" height="289" /></a><figcaption>Filters and advanced editing in Apple Photos, Instagram, and Camera+ Mobile Apps, respectively. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b4f40d5-73a7-449b-a4ca-f6bb5ed724d1/08-apple-instagram-cameraplus-apps-opt.jpg">View large version</a>)</figcaption></figure>

Because capturing and editing photos are usually a part of the same workflow, Dropbox has the same reason for not providing this in the initial version of Carousel: It just wants the picture once you’ve taken it. In addition to this reason, users also theoretically cannot edit photos until they store them on Dropbox. Because one of Dropbox’s primary objectives with Carousel is to increase the number of photos that new and existing users store on Dropbox, what users do thereafter is less important and is potentially a distraction from saving all of their photos and moving on.</p>

### Backing Up and Syncing

Below are screenshots of Google+, Apple’s Photos, Facebook, Dropbox and Carousel.

Unfortunately, most camera and photo-editing apps still require users to save photos to the camera roll before backing up and syncing. This multi-step process of safely backing up photos and videos and then clearing the camera roll to save space is not only time-consuming when done at the last minute, but also stressful because there is always the worry that something hasn’t synced properly. Beyond the potential for improvement in tying together the processes of capturing and backing up media, current cloud solutions have some additional design problems.

On iOS, separating the option to back up the camera roll from the option to upload new photos to the photo stream across all devices could be confusing. In fact, I still barely understand the difference. Google+ also confuses this experience because users might presume they can edit these settings in Google Drive, which they can’t. While Google+ does offer auto-enhance and “Auto Awesome” — whatever that means — users might go over their data limits or their phone’s battery might die from uploading so many videos or photos over cellular data.

Facebook, on the other hand, has learned its lesson here and clearly makes media syncing private until the user does something. It also provides some granularity in the settings so that users can sync in the background with peace of mind. And users have a clear option to use Facebook for cloud storage, like Dropbox — obviously, Dropbox is interested in enabling this by default because this is its core business and product value, unlike Facebook.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41a8d830-d69d-4974-a7fa-acfecdcb9f51/09-googleplus-apple-facebook-apps-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2ff1743-c725-4f44-b22d-b38ff752d833/09-googleplus-apple-facebook-apps-opt-500.jpg" alt="Settings in Google+, Apple Photos, and Facebook Mobile Apps, respectively" width="500" height="290" /></a><figcaption>Settings in Google+, Apple Photos, and Facebook Mobile Apps, respectively. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41a8d830-d69d-4974-a7fa-acfecdcb9f51/09-googleplus-apple-facebook-apps-opt.jpg">View large version</a>)</figcaption></figure>

Dropbox takes care of these use cases elegantly and, as we’ll see, has completely migrated these settings for photos over to Carousel so that users can get to the right place even if they try to edit these settings in Dropbox’s main app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff108a7-6a55-4957-bc2b-f6c75e7aa92d/10-dropbox-carousel-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab136af3-a56f-4525-8862-f20708e1c873/10-dropbox-carousel-opt-500.jpg" alt="Settings in Dropbox and Carousel Mobile Apps, respectively" width="500" height="438" /></a><figcaption>Settings in Dropbox and Carousel Mobile Apps, respectively. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff108a7-6a55-4957-bc2b-f6c75e7aa92d/10-dropbox-carousel-opt.jpg">View large version</a>)</figcaption></figure>

### Viewing

Below are screenshots of Apple’s Photos, Facebook, Instagram and Picturelife.

At a basic level, these apps all present photos and videos according to the time and location in which they were shot (sometimes even the building) and in groups and in enlarged individual views. However, this can get confusing when users toggle between views, especially in Apple’s Photos, which has albums, collections and moments, with little or no visual cue of how they relate to each other or what they even mean in the first place — I, for one, still have no idea. This becomes increasingly problematic when users delete photos from their camera roll periodically to save storage space, because there isn’t an easy way to view backed-up media in iCloud.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e255c0-b1c4-4043-8014-2800ad266738/11-apple-photo-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/321328e0-4233-4229-b692-11d7e01f5b54/11-apple-photo-app-opt-500.jpg" alt="Viewing photos with the Apple Photos Mobile App" width="500" height="289" /></a><figcaption>Viewing photos with the Apple Photos Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e255c0-b1c4-4043-8014-2800ad266738/11-apple-photo-app-opt.jpg">View large version</a>)</figcaption></figure>

Facebook is a much simpler solution but, like many cloud-based galleries, has issues with loading speed when the user scrolls quickly because it’s not a native app. Also, accessing these photos is not as simple as it should be — photos are still a secondary experience. On other other hand, Instagram is a photo-first app, but the viewing functionality is limited and extremely cluttered by supporting data (likes, comments, timestamps, etc.).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16a11bc0-c25c-45c3-8b70-ff449ad76fe6/12-facebook-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f18daba0-c240-4ada-8bba-c82f846052ca/12-facebook-app-opt-500.jpg" alt="12-facebook-app-opt-500" width="500" height="289" /></a><figcaption>Viewing photos with Facebook’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16a11bc0-c25c-45c3-8b70-ff449ad76fe6/12-facebook-app-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6cd00be-fe4b-479e-869f-6d8f9552755b/13-instagram-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/804cd3e3-3a08-4aeb-b7ac-9c500542c0e3/13-instagram-app-opt-500.jpg" alt="Viewing photos with Instagram’s Mobile App" width="500" height="288" /></a><figcaption>Viewing photos with Instagram’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6cd00be-fe4b-479e-869f-6d8f9552755b/13-instagram-app-opt.jpg">View large version</a>)</figcaption></figure>

Compared to the alternatives, Picturelife stands apart with its sheer breadth of options for viewing the media not only in your phone’s camera roll but in 10 popular galleries and social networks, including Dropbox, Facebook, Flickr, Foursquare, Google+, Instagram, Shutterfly, Smugmug, Tumblr and Twitter. Switch easily between timeline, places, faces, memories, favorites, screenshots and albums. Within each album, sort by album name, date taken, date modified, date created or number of pictures. Most importantly, users can use free-form search to find what they’re looking for.

The primary drawback to so many options is that getting lost in the myriad of photos you’ve taken is easy. Moreover, by syncing so many galleries and networks, many of which have reposted images, users will likely see many duplicates. Nevertheless, this product probably enables you to find any image more quickly than any other solution to date.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baf975b5-7137-40fb-8c86-842b9173268e/14-picturelife-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15c5900c-c856-4897-86ff-ba50604a3933/14-picturelife-app-opt-500.jpg" alt="Viewing photos with Picturelife’s Mobile App" width="500" height="288" /></a><figcaption>Viewing photos with Picturelife’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baf975b5-7137-40fb-8c86-842b9173268e/14-picturelife-app-opt.jpg">View large version</a>)</figcaption></figure>

### Managing

Below are screenshots of Apple’s Photos, Facebook and Picturelife.

This is where many media galleries and camera apps diverge. Management workflows (tagging, arranging, moving, deleting, hiding) are incredibly diverse, and each app seems to prioritize its own variation. At a basic level, most apps enable users to move media between folders, to use a preset viewing filter to stay organized automatically and to delete photos. These actions can typically be done at the level of picture, selected group or album. However, apps vary widely in how they enable users to hide media, duplicate media, save copies and originals, export to other applications, comment, change meta data, unduplicate, and even link media galleries and social networks.

Apple’s Photos, for instance, enables users to easily select one or more media files and move them between albums or delete them. Likewise, entire albums may be deleted. And a subset of Apple’s photo stream can sync locally, and third-party apps may store copies in Photos as well. However, you can’t manage these accounts from Photos directly. Any other advanced functionality for managing media doesn’t exist. It’s pretty basic.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90bbf99b-b9f5-4219-8baf-25ed67c20113/15-apple-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d8737f3-6355-4124-b3fc-09538004127a/15-apple-app-opt-500.jpg" alt="Managing Photos with Apple’s Photo Mobile App" width="500" height="291" /></a><figcaption>Managing Photos with Apple’s Photo Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90bbf99b-b9f5-4219-8baf-25ed67c20113/15-apple-app-opt.jpg">View large version</a>)</figcaption></figure>

Facebook provides similar functionality. However, slightly more can be done on a mobile phone, including tagging people, liking media files, and viewing all cloud-stored album-organized media that include tags of the user or that are synced from a phone. While the experience of viewing all synced media in the mobile app is sluggish, the user at least isn’t limited to the local storage on their mobile device. In any case, Facebook is still a limited solution.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b1351b3-d21f-4ab3-b53f-440138835555/16-facebook-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82b8fa2d-b513-4397-833d-04e4045595a7/16-facebook-app-opt-500.jpg" alt="Managing Photos with Facebook’s Mobile App" width="500" height="290" /></a><figcaption>Managing Photos with Facebook’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b1351b3-d21f-4ab3-b53f-440138835555/16-facebook-app-opt.jpg">View large version</a>)</figcaption></figure>

Picturelife, by contrast, seems to have it all. Users can either touch and hold an image to see resizing options via drag-and-drop gestures or use a standard vertical menu to favorite photos, add them to albums, hide, delete, comment and more. The flexibility of the viewing options makes managing photos and videos effortless. However, a big drawback is that users can’t select multiple images to add them to a new album or to move them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78836d09-693a-4d2f-a831-79b235277a0a/17-picturelife-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d35652b4-d564-413e-9ce1-653e056aec4b/17-picturelife-app-opt-500.jpg" alt="Managing Photos with Picturelife’s Mobile App" width="500" height="289" /></a><figcaption>Managing Photos with Picturelife’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78836d09-693a-4d2f-a831-79b235277a0a/17-picturelife-app-opt.jpg">View large version</a>)</figcaption></figure>

### Sharing (Private and Public)

Below are screenshots of Google+, Apple’s Photos and Picturelife.

Sharing a single piece or a group of media publicly is baked into every photo and video application we looked at. Whether they share directly from their photo gallery of choice or save to their camera roll in order to share later on another platform, users have options. That being said, how users add, remove and view media before sharing, how they engage with it once shared, where exactly they may share and how they add and remove people to share with vary widely. More importantly, in recent years certain applications give users the option to share media privately with a select audience — a common activity in chat and email clients.

Google+ is designed rather well to let users switch seamlessly between sharing a single photo, a selection of photos or an entire album, whether through Google+ itself or by saving directly to the phone’s camera roll. However, users will be sharing photos on Google’s network with “public” recipients as the default. If they want to send to individual recipients, they get a very limited subset of contacts to scroll through — and only within Google’s network — or a search box or preorganized list of contacts, which likely isn’t updated or properly maintained, especially compared to Facebook’s smart lists. Facebook is similar to Google in that it primarily lets you share media publicly with varying degrees of privacy. While Facebook Messenger’s integration of the camera roll into the private chatting experience is nice, users have no real way to send photos from a Facebook album directly to a private audience in chat.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8b531b-7c91-4364-8ece-9c5415abcd36/18-googleplus-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5cf01e-cb32-4ba1-af9c-eb9d20f330e7/18-googleplus-app-opt-500.jpg" alt="Sharing photos with the Google+ Mobile App" width="500" height="291" /></a><figcaption>Sharing photos with the Google+ Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8b531b-7c91-4364-8ece-9c5415abcd36/18-googleplus-app-opt.jpg">View large version</a>)</figcaption></figure>

Apple offers far greater flexibility with sharing on almost any social network, as well as through SMS and email. However, users get little assistance with selecting recipients and no additional organization of this sharing history, especially if they’ve ever shared across more than one channel. Users are also generally forced to share media publicly on social websites but can share privately through more traditionally private channels such as SMS and email.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85c8117a-6e86-418e-b154-7ed90b9821d1/19-apple-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae7958f-3240-4820-aa8f-40ea79a2a5fb/19-apple-app-opt-500.jpg" alt="Sharing photos with Apple’s Photos Mobile App" width="500" height="289" /></a><figcaption>Sharing photos with Apple’s Photos Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85c8117a-6e86-418e-b154-7ed90b9821d1/19-apple-app-opt.jpg">View large version</a>)</figcaption></figure>

Picturelife, on the other hand, provides clear flexibility in sending media to a person or group through the phone’s address book or posting to one or more popular social networks. Each option is emphasized equally, so the user can decide how they want to share their photos and videos. Oddly enough for a mobile solution, the way of selecting contacts is extremely sluggish and seems to only offer email options and no SMS option.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a4811f9-3286-48ad-8b41-d560dd63bd89/20-picturelife-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ada8f8e0-33c1-49ff-a843-dcf8d621ef13/20-picturelife-app-opt-500.jpg" alt="Sharing photos with Picturelife’s Mobile App" width="500" height="290" /></a><figcaption>Sharing photos with Picturelife’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a4811f9-3286-48ad-8b41-d560dd63bd89/20-picturelife-app-opt.jpg">View large version</a>)</figcaption></figure>

### Discussing (Private and Public)

Below are screenshots of Apple’s Photos, Facebook and Instagram.

While all of the limitations on posting publicly are due to the sharing limitations mentioned above, the designs to support private discussion are rather distinct from the designs for public discussion and seem to vary widely based on the product’s priorities.

For example, on iOS, users can share multiple photos at once and include anyone in their address book (which is usually anyone with an email address or phone number), but they can’t add more people to the conversation on the fly or reply to a subset of recipients in a separate conversation or view their full media history in a consolidated display (because photos and videos are kept separate).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a385c8a4-c230-4ae1-8f7c-73e7324eef5f/21-apple-app-opt-78x45.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/addc88bb-f422-4828-bd37-8247ed108ab7/21-apple-app-opt-500.jpg" alt="Discussing photos with Apple Photos Mobile App" width="500" height="289" /></a><figcaption>Discussing photos with Apple’s Photos Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a385c8a4-c230-4ae1-8f7c-73e7324eef5f/21-apple-app-opt-78x45.jpg">View large version</a>)</figcaption></figure>

Meanwhile, Facebook allows users to add new recipients, effectively creating a new chat. Additionally, Facebook more clearly displays the various ways users can communicate with recipients, not just by text, photo and video, but with audio and emojis; and the option to choose an existing photo or video or create a new one is obvious at a glance. However, users can only chat with people they’re connected with on Facebook, not anyone in their address book.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c23444b5-7ad4-42ce-80ed-8b3e3083ac0c/22-facebook-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2d77d46-c14e-48a6-be3c-d76e260b6657/22-facebook-app-opt-500.jpg" alt="Discussing photos with Facebook’s Mobile App" width="500" height="291" /></a><figcaption>Discussing photos with Facebook’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c23444b5-7ad4-42ce-80ed-8b3e3083ac0c/22-facebook-app-opt.jpg">View large version</a>)</figcaption></figure>

Instagram, on the other hand, makes it very easy to switch between private and public discussions. When users post to their followers to have a public discussion, they can also post to popular websites such as Facebook, Twitter, Tumblr and Flickr to continue the conversation there. Alternatively, they can send a direct message to anyone they’re connected with on Instagram. Again, they’re limited to the social network itself, but this is a dramatic improvement over many of the social alternatives.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84599530-23e4-4eee-a837-d06195e062e5/23-instagram-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5b71cdc-d8b1-4f78-9d1f-e3fa1d392e04/23-instagram-app-opt-500.jpg" alt="Discussing photos with Instagram’s Mobile App" width="500" height="290" /></a><figcaption>Discussing photos with Instagram’s Mobile App. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84599530-23e4-4eee-a837-d06195e062e5/23-instagram-app-opt.jpg">View large version</a>)</figcaption></figure>

## Time To Focus And Design Carousel

Now that we thoroughly understand Carousel’s core users, their general needs, Dropbox’s business needs and what exists on the market, it’s time to get something done.</p>

## Primary User Requirements

In a <a href="https://www.wired.com/2014/04/3-ingenious-design-details-in-carousel-dropboxs-new-photo-app/">Wired article</a> covering Carousel’s launch, Gentry Underwood, CEO and cofounder of Mailbox (which was acquired by Dropbox) and lead designer of Carousel, detailed some of the key requirements that his team prioritized.

Below is a list of some of them, as well as some requirements highlighted in <a href="https://techcrunch.com/2014/04/09/dropbox-debuts-carousel-aiming-to-be-the-go-to-storage-app-for-your-entire-photo-archive/">media coverage of Carousel’s launch</a> and from our evaluation of existing products and design patterns in part 1.

#### Back up all photos and videos

The app has to save not only the photos that users want to see in the gallery, but also ones they don’t want to see yet but might want to at a later date. Not to mention, this takes up more storage, which is ideal for Dropbox’s business. Most photo apps allow you only to delete photos, not hide them. “It’s a 100% destructive thing,” Underwood says. And the permanence of deleting photos requires a heavy two-step process of hitting the trash button and confirming the action. Underwood claims that this leads to users not deleting media and, ultimately, to sloppy media galleries with misfires, blurry selfies and many imperfect versions of the same shot.

#### Display all photos and videos

According to Underwood, another big problem with media gallery apps is that they seem to start from the last time you bought a smartphone. This is especially true for stock apps like Apple’s Photos. However, even with photo stream and other apps that sync a portion of your photos locally while saving the rest in the cloud, users can never see their entire media history — they have to go to their computer or the web for that.

#### Show the best photos and videos

The most obvious solution for this is to make it easy to manually hide undesired media, presumably with some quick swiping action. However, the app could also surface media that users would most likely want to see, like ones with faces or, more importantly, smiling faces. Beyond finding the best media, the app could also highlight one or more thumbnails of media that seem most interesting.

#### Enable quick navigation

Media should be automatically sorted in events based on common attributes such as time and location. The groupings should also show just a sample of the photos from that event in order to save space while navigating through a long list. Finally, users should have multiple ways to scroll through media (for example, slowly or quickly).

#### Feel native

Making it seem like everything is stored locally would set this application apart from the competition. After all, that snappy feeling is what makes Apple’s Photos more appealing than Facebook, Flickr, Instagram, Dropbox and the like. Among other things, fine-tuning the caching and other back-end tricks could help dramatically. But some clever perceptual tricks could also be done. For example, multiple thumbnails of each media file could be saved at various resolutions and be dynamically deployed based on how fast the user is scrolling through the gallery. Faster scrolling would trigger lower-resolution thumbnails so that they load instantly and make the app feel native. Moreover, adding, moving, changing and deleting media files from Carousel or Dropbox should happen lightning-fast.

#### Enable public and private sharing

Users should be able to share videos and photos with others easily without having to use platforms with storage limitations, such as email. Also, they should be able to easily select between public sharing (i.e. on social networks) and private sharing through email, SMS and private in-app chat. “Carousel’s sharing tools can be utilized through any email address or phone number, whether the recipient has a Dropbox account or not,” says Underwood.

#### Enable public and private discussion

Although in-app discussion is an option when media is shared privately, as mentioned above, it’s not necessary. However, allowing for focused discussion on a set of photos — particularly after an event, when users want to congregate and compare photos — can be valuable. As an alternative to Facebook Messenger, SMS and email, where many other conversations go on, offering a dedicated set of chat threads for users’ personal media and nothing else would be beneficial. It would also be a great way to acquire new users for Dropbox.</p>

## What Do Users Get?

Basically, users get a camera roll for Dropbox. As <a href="https://www.macstories.net/reviews/thoughts-on-dropbox-carousel/">Federico Viticci from MacStories eloquently puts it</a>, the app is a clean and imaginative “alternative Camera Roll and Photo Stream based on Dropbox storage with built-in sharing for individual or group conversations.”

Carousel’s MVP is effectively two things for most users: a Dropbox uploader for backing up local photos and videos, and an enhanced version of Apple’s native Photos app, with improved viewing, sharing and discussion functionality. The app doesn’t let users take, edit or manage photos, other than hiding them (or deleting them, if they can find that feature), or view in anything other than chronological order.

For now, if users want to take and edit photos, then their mobile camera, Instagram or Camera+ are great options. To organize photos into folders, they’ll need to use Dropbox directly. And to view them in anything other than chronological order, they would sync Dropbox with a more advanced media gallery such as iPhoto, Picasa or Unbound. You will understand Carousel’s MVP much more easily by testing it out than by listening to me explain it ad nauseam. Below are four screenshots of what you can expect. To help you along, <a href="https://www.macstories.net/reviews/thoughts-on-dropbox-carousel/">MacStories thoughtfully runs through</a> what you can expect in your first experience.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76e2a3cf-8fc5-41a0-b38b-5218571335f8/02-carousel-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff501e0c-754f-4576-bc9f-73c2870d02a1/02-carousel-app-opt-500.jpg" alt="Carousel mobile app" width="500" height="219" /></a><figcaption>Carousel mobile app (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76e2a3cf-8fc5-41a0-b38b-5218571335f8/02-carousel-app-opt.jpg">View large version</a>)</figcaption></figure>

## Results And Learning

Mills Baker, a product design analyst at Mokriya, paints a rather dismal picture of Carousel in “<a href="https://mokriya.quora.com/Designer-Duds-Losing-Our-Seat-at-the-Table?srid=h1hP&amp;share=1">Designer Duds: Losing Our Seat at the Table</a>”:
<blockquote>It’s honestly hard to determine what should be interesting about it, even in theory; it takes mostly standard approaches to organization, display, and sharing, and seems to do little to distinguish itself from the default iOS Photos app + iCloud Photo Sharing, let alone apps and services like Instagram, VSCO Cam, Snapchat, iMessage, Facebook Messenger, and so on.</blockquote>

To get an idea of why Mills feels so strongly about Carousel’s shortcomings, let’s look at the results since its launch.</p>

### Rankings

Since topping the charts on and around launch day, Carousel has steadily lost attention, now ranking 456th in the “Photo and Video” category of Apple’s App Store and falling off in the overall rankings across all categories. It has basically been buried in the crowded photo and video app market, and Dropbox will need to make some non-trivial changes in subsequent iterations to make it bounce back to the top.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f1c1455-5017-4d9a-9cb3-e0ae5938d949/03-carousel-ranking-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f1c1455-5017-4d9a-9cb3-e0ae5938d949/03-carousel-ranking-opt.jpg" alt="Carousel ranking has steadily declined since launch" width="832" height="645" /></a><figcaption>Carousel’s ranking has steadily declined since launch. (Image: <a href="https://www.Appannie.com">AppAnnie</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f1c1455-5017-4d9a-9cb3-e0ae5938d949/03-carousel-ranking-opt.jpg">View large version</a>)</figcaption></figure>

Upon launching in April 2014, the app certainly didn’t increase downloads of Dropbox’s main app, suggesting that Carousel’s main impact was on revenue or engagement, if anything.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec2f392-b82b-4222-86c3-4888c6bf2eaf/04-carousel-ranking-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3104bf7-b68d-47de-8399-48163b306ce7/04-carousel-ranking-opt-500.jpg" alt="Dropbox ranking hasn’t been affected by Carousel" width="500" height="393" /></a><figcaption>Dropbox’s ranking hasn’t been affected by Carousel. (Image: <a href="https://www.Appannie.com">AppAnnie</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec2f392-b82b-4222-86c3-4888c6bf2eaf/04-carousel-ranking-opt.jpg">View large version</a>)</figcaption></figure>

### Downloads

As of 16 July 2014, Carousel appears to have been downloaded 174,000 times globally. If Dropbox currently has <a href="https://thenextweb.com/insider/2014/05/29/dropbox-reaches-300m-users-adding-100m-users-just-six-months/">300 million users</a>, then it has managed to get a paltry .06% of its total customer base to adopt Carousel. Clearly, it needs to make some improvements to increase adoption.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/934fdba4-25f2-4f01-bf22-223eef2a80b6/05-carousel-downloads-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1332cd76-eea7-492a-b0a5-afc90493e575/05-carousel-downloads-opt-500.jpg" alt="Carousel downloads are sufficient for testing the app, not for claiming mass adoption" width="500" height="186" /></a><figcaption>Carousel downloads are sufficient for testing the app, not for claiming mass adoption. (Image: <a href="https://xyo.net/iphone-app/carousel-by-dropbox-mEYaRL4/">XYO</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/934fdba4-25f2-4f01-bf22-223eef2a80b6/05-carousel-downloads-opt.jpg">View large version</a>)</figcaption></figure>

### Ratings

If we look at reviews in Apple’s App Store, non-target users almost unanimously consider Carousel to be a failure. “Not what I wanted,” “MASSIVE oversight” and “Completely useless” smatter the reviews section — all valid complaints if people are using it professionally. Meanwhile, average consumers like Owen and Nora have mixed reviews, ranging from “Amazing app!!!! This app is the best way to back up and privately share my photos on iOS!!!” to “Bring back Loom! Complete downgrade from Loom… Sad.”

While it wasn’t a runaway success upon launch, Carousel drew user reviews in the US and internationally that at least skew favorably. In fact, the reviews are as good as the ones for Dropbox and even Mailbox, both excellent standards for any productivity app.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f5603d6-f956-4315-a2c9-41e8698b76af/06-carousel-ranking-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d178d586-f0c8-498d-8150-efee9277326c/06-carousel-ranking-opt-500.jpg" alt="Reviews for the first version of Carousel globally (left) and in the US (right)" width="500" height="186" /></a><figcaption>Reviews for the first version of Carousel globally (left) and in the US (right). (Image: <a href="https://www.Appannie.com">AppAnnie</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f5603d6-f956-4315-a2c9-41e8698b76af/06-carousel-ranking-opt.jpg">View large version</a>)</figcaption></figure>

While these reviews make it difficult to dispute Baker about the lackluster adoption of Carousel upon launch, 174,000 downloads is more than enough to learn about how people use Carousel, what needs to be improved and how well various features help Dropbox achieve its business goals.</p>

### In-App Purchases

While these statistics are highly coveted and, thus, kept very private, you can at least generalize that Carousel is achieving its primary objective of upselling existing users to premium accounts. However, many details suggest that Dropbox will need to make some major improvements to scale downloads and usage for new and existing users.

With Dropbox charging roughly ten times the price of Google’s popular cloud storage alternative, Drive, it will be interesting to see how much price has stunted adoption of and engagement with Carousel. If we’re being realistic, anyone who wasn’t born yesterday would know that Carousel <a href="https://www.technologyreview.com/news/526606/review-dropboxs-carousel-photo-sharing-app/">requires Dropbox’s Pro Plan</a> to work reliably. Dropbox will certainly have to address this as companies continue to compete on price in building up their cloud-based apps on top of virtually free cloud storage.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0139c646-b557-4356-8cf8-f3db87b4b3da/07-carousel-dropbox-apps-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7af829ae-da6c-4045-98a1-8c4f395c8223/07-carousel-dropbox-apps-opt-500.jpg" alt="Carousel and Dropbox apps, respectively" width="500" height="231" /></a><figcaption>Top in-app purchases for Carousel (left) and Dropbox (right). (Image: <a href="https://www.Appannie.com">AppAnnie</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0139c646-b557-4356-8cf8-f3db87b4b3da/07-carousel-dropbox-apps-opt.jpg">View large version</a>)</figcaption></figure>

## Looking Forward To The Next Iteration

As expected, this MVP is far from being a full photo and video manager. It lacks some features that hold users back from adopting it, including:

*   better meta data and a better organizational structure for navigating photos,
*   more granular syncing options to reduce clutter,
*   a web viewer for making sharing easier,
*   lower pricing.

However, if you look closely at everything Dropbox has done with Carousel, it has been extremely disciplined in prioritizing many of the most important features for its business and its users. It has drawn from the best relevant design patterns that I could find, many of which are not to be found in the closest alternatives, including Apple’s Photos and Instagram Direct. And while most mobile photos galleries aren’t that complex, Dropbox has managed to edit out features that are less important, such as a camera, editing features, heavy organization options, chat outside of sharing, and friend lists.

It still has a ton of work to do on the web and mobile. Considering how much people wish Loom was still around, many of its features will probably be included. Additionally, well-designed and robust apps such as Picturelife offer a great deal of inspiration for a dramatically simplified alternative to Carousel.

And while Dropbox might have done better to wait for what Rand Fishkin, cofounder of Moz, calls an <a href="https://moz.com/rand/7-unlikely-recommendations-for-startups-entrepreneurs/">EVP</a> — an exceptional viable product — Carousel has a promising future. Dropbox just needs to tweak what it’s got to get more people to download and use the app.

{{< signature "al, ml, il" >}}

