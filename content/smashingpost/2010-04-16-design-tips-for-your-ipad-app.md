---
title: Useful Design Tips For Your iPad App
slug: design-tips-for-your-ipad-app
image: null
date: 2010-04-16T15:14:02.000Z
author: jen-gordon
description: >-
  With tools like [Appcelerator's Titanium](https://www.appcelerator.com/) and some JavaScript programming skill, creating native iPhone and iPad apps is simple. The danger is in not being always on the look-out for the kind of design pitfalls that plague many products in the App Store. In this post,
  we'll consider some design tips that will get you on the road to iPad success.
categories:
  - Mobile
  - Design
  - Apps
  - iOS
  - iPad
---

## Design For People

Apps will define the iPad, it's true. But in developing your app idea, which comes first, the idea or the device? Good news: neither. It's people! When brainstorming and researching ideas for your app, step back and consider the context in which the device will be used by real live people. <strong>How does the iPad fit into our lives? In what situations would we prefer this device to a laptop or iPod Touch?</strong>

{{% feature-panel %}}

### Who Are Your People?

Ideally, your target audience includes you, but using this as a reason to decide that "I know what people like me want" could lead you to miss out on opportunities to enrich the product beyond your imagination. Surprises await when you consider the variety of people who might use your product. Your target audience may be different than what you think; or in defining your target audience, you may find that your product is missing important features.

For example, with our application (a drawing tool), our initial target audience included early-adopter techies. But after some analysis, we saw that the interface needed to be greatly simplified so that <strong>the children of the techies</strong> would also enjoy the app.

<strong>Tip:</strong> Define your target audience. Who are they? Where do they live, work and play? What challenges do they face? Give one of them a name, a job, a family, a car; then see how your perspective changes.</p>

### What Is Your People's Story?

Defining a target audience is only half of the equation. Now you have to put your audience into action! What do they do in their daily life? How will their daily life intersect with your product? Get into their minds. Try this, and I guarantee it will lead you down some expected <em>and</em> unexpected paths.

You don't need fancy software to do this. Below is an example of our use case sketches for our application. After writing out a few use cases, we learned that people lose interest in drawing games when they're forced to create original artwork. Many people will say, "I can't draw," but they still have a desire to create beautiful things. Originally, we planned for our app to ship with patterns, similar to the classic Lite-Brite toy, but it didn't occur to us that <strong>people would play with the app more</strong> if we provided pre-fab patterns and templates for them to color. Pretty important feedback!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae304b9-f0a0-40e5-8ddd-fd6f29e66e35/img-use-case.jpg" alt="ipad-use-case" width="500" height="368" /><br>
<em>In developing the idea for an app, our use cases revealed that the replay value of such an app is low unless you provide patterns for the user to get started.</em>

<strong>Tip:</strong> Think about the device in terms of lifestyle rather than features and technology. Will the iPad's unique characteristics and environmental and sociological factors make your idea resonate with people?

*   It's lightweight = "I'll carry it more places than I would a laptop."
*   It's smaller than a laptop = "It's discreet. Would I crack open my laptop to do some work in a waiting room? No. Would I switch on my iPad? Yes."
*   It has robust utilities and multimedia capabilities = "I can work and enjoy books, movies and games."
*   Its screen is larger than the iPhone's = "I can consume more media with less eye strain. My kids will be entertained on a road trip."
*   It has Wi-Fi and 3G Internet connectivity = "I can be online on a plane, train or car."

Designing for people is critical to weeding out weak (i.e. unprofitable, untargetable or unmarketable) ideas quickly and to developing a product that not only meets but anticipates the target audience's needs.</p>

## Minimalism Works Best on iPad

With robust, portable, location-aware devices like the iPad, the temptation is to throw in everything and the kitchen sink. If you're an iPhone developer, you're probably excited about the additional screen real estate. Resist the temptation to fill the space! Keep it simple. Display only the content and controls that are relevant to the user at that moment. This requires you to use the following two things in your interface design.

### Contextual Menus

Contextual menus are a great way to keep your UI out of the way. We wanted to keep sharing and community features out of the primary navigation. We used a contextual menu ("Share this thang!") to present actionable items at the appropriate time.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512dd146-5e2f-45a4-9fa2-a6727c13b0c7/contextual-menus2.jpg" alt="Example of a contextual sharing dialog" width="450" height="565" /><br>
<em>Example of a contextual sharing dialog, activated when you tap and hold on an image.</em>

### Modal Views (but Wisely)

With the increased real estate on the iPad, one can build in robust functionality that is impossible on an iPhone or iPod Touch screen. Modal views give you another way to organize your application; they give the user clear "modes" of operation; and they can be an elegant solution to UI clutter if executed wisely.

For example, "photos" on the iPad could operate similar to iPhoto on the desktop Mac. You have two "modes" of operation:

1.  View or edit an individual photo,
2.  Manage groups of photos.

In each scenario, packing the viewing, editing and managing functions into one view wouldn't make sense. Think of how you could segment features in your app, while maintaining a smooth connection between the two modes.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dd070f5-eea4-4305-817a-02d55fe3b1df/ipad-guitar-top.jpg" alt="modal view" width="500" height="336" /><br>
<em>iPhoto has two modes of operation: viewing and editing a photo</em> or <em>managing photos.</em>

<strong>Tip:</strong> What is the bare minimum your app could provide and still be useful to users?

## iPad's Two Orientation Are A Big Deal

Being able to switch views—landscape to portrait and back again—is not unique to the iPad, but it's a bigger deal on it. This is where paper prototyping will save you from wasting loads of time in Photoshop.

Having to consider every element of your app in these two sometimes radically different layouts is like designing for two devices… except that you're not designing for two devices. The trick is to keep the experience consistent in each view, allowing for a seamless user experience when switching views.

Below is a color palette we tested for our app. The palette looks great in landscape mode but absolutely hogs the screen in portrait mode. Oops.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/947001be-483f-4587-8e0c-83e0c1404c5a/01.jpg" alt="landscape" width="500" height="375" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a067325c-0797-45a1-a0b5-1a4c4192f35c/02.jpg" alt="portrait" width="500" height="667" /><br>
<em>This palette looks okay in landscape mode but gobbles up the interface in portrait.</em>

We reconfigured the color palette to have a smaller footprint in both landscape and portrait modes:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/315cc160-93e0-4ab7-8178-8bc2fa0b6d0e/04.jpg" alt="color-palette" width="500" height="375" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a5e6c46-3c67-4c2c-81e2-9033e6a2187c/03.jpg" alt="color-palette" width="500" height="667" /><br>
<em>A streamlined color palette allows accessibility while staying out of the way in both landscape and portrait views.</em>

<strong>Tip:</strong> Paper prototype all of your screens in portrait and landscape modes… a <em>lot</em>.

## Use Touch And Real-World Metaphors

Touch changes how we interact with, edit and perceive on-screen elements. With the iPad's larger screen, touch and gestures are turbo-charged. A quick run-down of unique UI elements on the iPad:

*   Select and take action on multiple items at once by dragging them to another area of the screen.
*   See both a list view and details of items in that list view (e.g. Mail).
*   Edit elements in place rather than from a global menu bar.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f31f18f-89f4-4ddc-87b6-776549a905b6/touch.jpg" alt="iphoto" width="500" height="215" /><br>
<em>Spread your fingers over a stack of photos to spread them out for viewing, as you might in the real world.</em>

<strong>Tip:</strong> Think of how you interact with things in the real world. Think of the on-screen elements as tangible things.</p>

## Design For Dynamic Content

The iPad's portability and bigger screen size gives users unlimited possibilities for <strong>quickly creating and sharing robust dynamic content on the go.</strong> Hybrid apps (i.e. native apps that draw from Web pages or that load real-time Web content) are becoming more common as users demand connectivity to Web-based tools. Designing for dynamic content means working through the challenges and opportunities of dealing with an Internet connection (e.g. slow downloads or lost connection). Think of what visuals you would present to users when they're stuck in East Bum with no connection to be found!

<strong>Tip:</strong> Plan for problematic situations in your design.</p>

## Get Started!

The first step to getting started is downloading the <a href="https://www.apple.com/ipad/sdk/">iPad SDK</a>. For Web developers looking to get into iPad development with their current skills, products such as Appcelerator's <a href="https://www.appcelerator.com/">Titanium</a> offer a good way to build native iPad, iPhone and Android apps in JavaScript.</p>

## Further Reading

*   [Ten Things To Think About When Designing Your iPad App](https://www.smashingmagazine.com/2012/01/ten-things-to-think-about-when-designing-your-ipad-app/)
*   [Web Development For The iPhone And iPad: Getting Started](https://www.smashingmagazine.com/2010/05/web-development-for-the-iphone-and-ipad-getting-started/)
*   [How To Make A Physiology-Friendly Application For The iPad](https://www.smashingmagazine.com/2016/03/how-to-make-user-friendly-application-ipad-physiology/)
*   [A Dad’s Plea To Developers Of iPad Apps For Children](https://www.smashingmagazine.com/2012/03/dads-plea-developers-ipad-apps-children/)

{{< signature "al" >}}

