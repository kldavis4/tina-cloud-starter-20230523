---
title: 'Not Your Parent’s Mobile Phone: UX Design Guidelines For Smartphones'
slug: not-your-parents-mobile-phone-ux-design-guidelines-smartphones
image: null
date: 2011-10-06T12:40:40.000Z
author: tim-r-todish
description: >-
  In your pocket right now is the most powerful “remote control” (as _Drew Diskin put it_) that has ever existed. It is no ordinary remote control. It can harness everything that all of the _previous mass media_ (television, radio, Internet, etc.) can do. People aren’t using them just for simple entertainment or for phone calls. They have become the hub of our personal lives.
categories:
  - UX
  - Mobile
  - Design
  - Interfaces
  - Design Patterns
---
Smartphones are what younger generations know as just phones. The iPad (aka <em>the</em> tablet) is giving your grandma’s PC a run for its money. You certainly are holding some amazing futuristic technology in your hands. It will be even better tomorrow, though, so why does it matter to us or to users? Moore’s Law tells us, in effect, that these things will continue to become capable of more than anything our minds can think up.

It’s no longer just about the evolving power and capabilities of these devices. It’s about us and how we, too, are changing. The user’s expectation of a great experience is the new standard. It falls to us as UX professionals to apply our skills to make this happen on the vast array of devices out there. It’s not always easy, though. The mobile realm has some <strong>unique constraints</strong> and offers some <strong>interesting opportunities</strong>. While covering all of the nuances of mobile UX in one article would be impossible, we’ll cover some fundamentals and concepts that should move you in the right direction with your projects.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketching A New Mobile Web](https://www.smashingmagazine.com/2012/06/sketching-a-new-mobile-web/)
*   [7 Guidelines For Designing High-Performance Mobile User Experiences](https://www.smashingmagazine.com/2011/07/seven-guidelines-for-designing-high-performance-mobile-user-experiences/)
*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)

{{% feature-panel %}}

## Mobile Constraints

The mobile realm has many constraints. Here are several of them, along with thoughts on what to keep in mind as you come upon them.</p>

### Form Factor

The most obvious constraint going from desktop to mobile is screen size. Mobile screens are smaller. A <em>lot</em> smaller. You need to seriously consider this when designing and developing your application. Antony Ribot makes a good point in his presentation, “<a href="https://www.slideshare.net/ribot/mobile-ux-the-intricacies-of-designing-for-mobile-devices-presentation">Mobile UX: The Intricacies of Designing For Mobile Devices</a>,” when he says, “Mobile is not about making things smaller.” It’s much more than that. We need to consolidate what’s on the screen. Boil the application down to the <strong>most critical functions</strong> and content, and then lay them out strategically in the available screen space. For example, action buttons should go in the lower third of the screen, where they are most easily tappable.</p>

### Input Methods

Another obvious constraint is the absence of or difference in certain input mechanisms, and the addition of others. First, there’s no mouse. No mouse means no hover states. It also means that there must be some other means of clicking and navigating content. In most cases, this other means is the user’s finger. This difference in input method can be quite exciting because it opens the door to new possibilities with various gestures. Many standards are forming around these new gesture capabilities: pinch to zoom, swipe to scroll, etc. Take the time to include support for these gestures in your application. In addition, think of new gestures that you could add to enhance interactivity.

Discovering new gestures can be a <strong>powerful experience</strong> for users. It adds a sense of excitement, mystery and achievement — “Hey, I just figured out something new!” Take care, though, not to change the function of standard gestures unless you have a very good reason to do so, or else you will cause unnecessary confusion and frustration in users.

<a href="https://www.lukew.com/touch/TouchGestureCards.pdf"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="107656" title="Gesture Card" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a12b9a-2aef-4176-aa37-cd6099527c0e/gesturecard.jpg" alt="Gesture Card" width="550" height="392" /></a><br>
<em>(Touch Gesture Cards (PDF): <a href="https://www.lukew.com/touch/TouchGestureCards.pdf">Luke Wroblewski</a>)</em>

One other caveat: consider the type of application you’re developing before getting too fancy with gestures. If it will be highly utilitarian in nature, then keeping things simple and straightforward would be best. If the application is for a specific task, then users will want to complete it as quickly and easily as possible. They don’t have the time or desire to discover new interactions.</p>

### Technical Constraints

While the capabilities of these devices improve with each new release it, keep in mind their limitations. Things like battery life and processing power are important to consider. Draining the battery or bringing the device to its knees with memory leaks or processor-intensive operations is a surefire way to destroy the user experience. This is why <strong>testing on the device early and often</strong> is imperative. Simulators cannot be trusted.</p>

### Data Transfer and Pricing

This will not be an issue for users who have unlimited data plans or who work on Wi-Fi networks. Unfortunately, unlimited plans are becoming increasingly rare. So, be sensitive to the amount of data you are transferring to and from your application. Keep the sizes of assets to a minimum, while maintaining quality. Don’t transfer data unnecessarily. For example, implement delta updates whenever possible (i.e. update only the data that has changed since the last transfer).

<a href="https://mediaqueri.es"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="107659" title="Food Sense - Responsive Web Design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60529080-0b02-4f6d-ad1a-8098f40e276b/foodsense.jpg" alt="Food Sense - Responsive Web Design" width="550" height="194" /></a><br>
<em>(Images: <a href="https://mediaqueri.es/">Mediaqueri.es</a> and <a href="https://foodsense.is/">Food Sense</a>)</em>

Much has been said recently about <strong>Responsive Web Design</strong>. This approach does create some challenges with minimizing data transfer. Jason Grigsby has a very good <a href="https://cloudfour.com/thinks/responsive-imgs-part-2/">write-up on the specifics</a>. To summarize, CSS media queries — part of the magic sauce of responsive design — do almost nothing to lessen the overhead of data transfer to mobile devices. Resizing or hiding unwanted images still requires the full images to be downloaded to the browser. In addition, resources such as JavaScript libraries might be downloaded to mobile devices without even being enabled for users.</p>

## Good General Practices

What follows are some good general principles to keep in mind when designing and developing mobile applications.</p>

### Mobile First

Luke Wroblewski has a great post on the “<a href="https://www.lukew.com/ff/entry.asp?933">Mobile First</a>” methodology. In a nutshell, focusing on mobile first puts your mind in the right place. It forces you to focus on and prioritize the most important features and content in your application. It also extends your abilities by offering new tools and services that are not available in a traditional desktop environment. By approaching your project with the mobile-first mentality, you will start off on the right foot.</p>

### Behaviors and Archetypes

Build on the behaviors and archetypes that your users are already accustomed to. This will go a long way to reducing the learning curve of your application. If your application responds predictably to a user’s interaction, then the user will immediately become more comfortable.

This applies to more than general behaviors and archetypes. You will want to use <strong>design patterns</strong> that are specific to your target devices. This means building multiple interfaces for various devices and platforms, which is extra work; but it will pay off in the long run because users will appreciate that your application behaves in the manner they’ve come to expect from their device. For example, iOS design patterns dictate that tabbed navigation be located at the bottom of the screen, whereas Android devices have it along the top.

As with most good UX principles, if done properly, the user won’t even notice, while their increased comfort level will encourage them to continue exploring the application. Which brings us to our next practice.</p>

### Encourage Exploration

The more that users feel comfortable with and enjoy your application, the more likely they will explore it. You may want to lead them down certain paths or provide a few cues or coach marks on how certain things work, but still allow your users to “discover.” I’m not suggesting that you make the application complicated or ambiguous; rather, for example, if there are multiple ways to perform an action, one more obvious and traditional and the other a quick and easy gesture, then the user might come to prefer the second option once they discover it. Such solutions improve the overall experience if they prove to be <strong>quicker and more efficient</strong> than traditional interactions.</p>

### Provide Immediate Feedback

We’ve all witnessed our less computer-savvy peers clicking violently and repeatedly on a button trying to force it to do whatever they so desperately want to achieve. Touchscreens only add to this anxiety because they don’t provide that tactile response that we’ve been conditioned to expect from tapping on a keyboard or clicking with a mouse. Providing some indication that the application has registered the user’s interaction is critical, whether it’s a small bounce at the end of a scrollable region or a subtle color change at the tap of a button. This not only compensates for the lack of tactile response, but assures users that something is happening even if the screen isn’t updating immediately due to slow network traffic or some processor-intensive operation.</p>

### Context

<img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="107645" title="Person using a tablet at home" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/263aa54a-5f6e-43a9-9f4d-8573585a13e8/ipad-home.jpg" alt="Person using a tablet at home" width="550" height="300" /><br>
<em>(Image: S. Diddy)</em>

Another glaring difference between mobile and desktop applications is context. With a desktop application, you can be relatively certain that it is being used in a particular environment. With mobile, all bets are off. This gives us some exciting opportunities: location-based services, on-the-spot social networking, the opportunities are vast.

It also raises some unique problems. Do your research to <strong>determine the context</strong> in which the majority of people will be using your application.

If you’re targeting on-the-go users, then you’ll want to build the application for speed: bold, obvious, stripped-down selectors and a streamlined workflow. If your application is more akin to a breakfast-table browser, then content will probably be more important to the user, but they may have only one hand free to navigate, while the other cradles their morning coffee. These are just two examples; the point is that your mobile application could be used in any number of contexts, and you will need to take the time to figure out how to provide the best experience to the user in their context.

One other thing to consider is the device(s) that you are targeting. Research suggests that a majority of tablet owners use their device mostly at home. Only 21% take their device with them on the go, compared to 59% of smartphone users who consult their device while out and about.</p>

### Ideate in the Wild

<a href="https://www.flickr.com/photos/niallkennedy/668454536/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="107647" title="Crowd of people" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86f9c678-22f3-4760-93a9-6d1d4d37ffde/crowd.jpg" alt="Crowd of people" width="550" height="300" /></a><br>
<em>(Image: <a href="https://www.flickr.com/photos/niallkennedy/668454536/">Niall Kennedy</a>)</em>

I’m borrowing this one directly from Rachel Hinman because she is spot on. The best way to determine context and to conduct research is to immerse yourself in the environments in which your application will be used.

Hang out where your target audience hangs out. If possible, do the things they do, go where they go. This will serve a couple purposes. First, it could give you ideas for great applications to build. Maybe you’ll observe common pain points and come up with a solution to alleviate them. Or, if you already have an idea for an application, you could gain valuable insight into how the application might be (or is being) used in the wild. We’d be surprised quite often by the difference between how we intend for our application to be used and how it is actually being used. This information can help us <strong>iterate</strong> our ideas and continually improve the application.</p>

## Conclusion

The way mobile devices are being used is changing all the time, and users are increasingly expecting exceptional experiences from the applications they use. While the mobile world has many constraints, its many more opportunities make building mobile applications a worthwhile venture. Keep in mind the constraints, and focus on mobile first when beginning your project.

Remember that innovative features and cutting-edge design aren’t as valuable to users as we may think. Users are concerned with getting the information they need through a sometimes limited connection, or perhaps getting accustomed to typing on a screen without any tactile feedback. Not everyone has an iPad… yet.

Talk to real people, follow common archetypes, and keep the context of your target users in mind. These guidelines should help you create a <strong>great experience</strong> in your mobile application.</p>

### Additional Resources

<strong>Design patterns:</strong>

*   [Apple iOS Patterns](https://pttrns.com)
*   [Mobile Patterns](https://mobile-patterns.com)
*   [Android Patterns](https://www.androidpatterns.com)

<strong>Design guidelines:</strong>

*   [iOS UX Guidelines](https://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/Introduction/Introduction.html)
*   [Android User Interface Guidelines](https://developer.android.com/guide/practices/ui_guidelines/index.html)
*   [Windows Phone UX Guidelines](https://msdn.microsoft.com/en-us/library/hh202915(v=VS.92).aspx)

<strong>Mobile statistics:</strong>

*   “<span class="removed_link" title="https://www.cloudfour.com/a-comprehensive-guide-to-mobile-statistics">A ‘Comprehensive’ Guide to Mobile Statistics</span>”

<strong>Article sources:</strong>

*   “[Mobile UX: The Intricacies of Designing for Mobile Devices](https://www.slideshare.net/ribot/mobile-ux-the-intricacies-of-designing-for-mobile-devices-presentation),” Anthony Ribot
*   “[Mobile UX Essentials](https://www.lukew.com/ff/entry.asp?1259),” Luke Wroblewski
*   “Getting Started With Mobile UX Design,” Springbox

{{< signature "al" >}}

