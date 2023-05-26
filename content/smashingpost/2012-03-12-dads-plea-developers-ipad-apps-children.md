---
title: A Dad’s Plea To Developers Of iPad Apps For Children
slug: dads-plea-developers-ipad-apps-children
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f81bfe-13c0-4beb-b57c-7db0da089b43/ipad1.jpg'
date: 2012-03-12T12:39:03.000Z
author: rian-van-der-merwe
summary: >-
  Designing apps for children is extremely hard. Not only is quality, age-appropriate content hard to create, but designing the flow and interaction of these apps is made more difficult because designers must refrain from implementing advanced gestures, which would only confuse and frustrate kids (and, by extension, their parents).
description: >-
  Designing apps for children is extremely hard. Not only is quality, age-appropriate content hard to create, but designing the flow and interaction of these apps is made more difficult.
categories:
  - UX
  - Design
  - Usability
---
I spend a lot of time buying and testing iPad apps for kids. To be more specific, I lovingly do this for a certain two-year-old girl who is currently on a very successful #OccupyiPad mission in my house. Through extensive observational research, I’ve discovered what works and doesn’t work for my daughter, so I’m going to shamelessly generalize my findings to all children and propose four essential guidelines for developers who work on iPad apps for children.

## Affordance Is King

Most apps for children show a bunch of different things on the screen that you can touch to make stuff happen. Cows moo, windows open and close, honey pots need to be collected, etc. But most of these apps **give no indication** of which elements are interactive and which are not. This usually results in a frantic and frustrating game of whack-a-mole to find the elements that actually do something.

The solution is simple: [affordance](https://en.wikipedia.org/wiki/Affordance). Give the elements in question a characteristic that indicates they are touchable. The [Disney Puzzle Book](https://www.disneybookapps.com/) apps do this really well. For example, in the Winnie the Pooh Puzzle Book app, the honey pots wiggle around to show the user that they need to touch them in order to collect them.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/690e7ff7-bf57-4ab4-b7eb-7e0d2576b9fa/winnie-the-pooh-ipad.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/690e7ff7-bf57-4ab4-b7eb-7e0d2576b9fa/winnie-the-pooh-ipad.jpg" width="550" height="413" alt="winnie-the-pooh-ipad" /></a></figure>

{{% feature-panel %}}

## Pagination Is A Primary Action

Pagination is so important to the enjoyment of most children’s apps, but it is often a quagmire. Almost every app does this differently. The most common methods of pagination are touch-based arrows and swipe-based gestures (indicated by a skeuomorphic curled-up page corner). Both of these interactions are valid solutions, but because swipes can be tricky for tiny fingers and the gestures usually require some precision, the **arrow approach is much better** for kids.

Also, the entire bottom part of the screen is a hot area and needs to be avoided. Kids constantly touch that part of the tablet by accident, which makes accidental pagination inevitable if the controls are placed there. I like how the [Old MacDonald](https://www.duckduckmoosedesign.com/educational-iphone-itouch-apps-for-kids/old-macdonald/) app implements pagination: clearly marked forward and backward arrows at the top of the screen.

<a href="https://www.duckduckmoosedesign.com/educational-iphone-itouch-apps-for-kids/old-macdonald/"><img class="aligncenter size-full wp-image-110561" title="old-macdonald-pagination" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39652d08-3b62-4690-a498-1b0d46271ee2/old-macdonald-pagination.jpg" alt="" width="550" height="413" /></a>

## The Menu Is A Distant Secondary Action

Speaking of the bottom part of the screen: don’t put *any* interactive elements in the bottom part of the screen &mdash; especially menu actions, which are not important anyway once a child gets going with the app. The number of times I’ve had to stop the car to dismiss a random menu brought on by an accidental touch… well, it’s dangerous. The Mickey Mouse Puzzle Book app is a good example of this frustrating practice:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a73d7bd8-9570-4c47-b441-247f95946124/mickey-mouse-menu.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a73d7bd8-9570-4c47-b441-247f95946124/mickey-mouse-menu.jpg" width="550" height="413" alt="mickey-mouse-menu" /></a></figure>

<a href="https://www.myplaytales.com/en/">PlayTales</a> has a clever implementation of the menu action in many of its books. First, the menu button is placed in the top-right corner, out of accidental reach (although the top middle would be better, in keeping with the top-left and top-right pagination mentioned in the previous point).

More importantly, it uses a two-touch method to bring up the menu. The menu icon is semi-transparent in its normal state. One tap removes the transparency, and a second tap brings up the menu. Although not foolproof, it’s an excellent way to avoid accidental taps.

<figure><a href="https://www.myplaytales.com/en/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25d8a274-782a-4912-94c4-75b8248a0f90/touchybooks-menu1.jpg" width="550" height="120" alt="touchybooks-menu1" /></a></figure>

<figure><a href="https://www.myplaytales.com/en/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d6760a9-74d6-4fa1-9a3f-795ced96825c/touchybooks-menu2.jpg" width="550" height="120" alt="touchybooks-menu2" /></a></figure>

<figure><a href="https://www.myplaytales.com/en/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b2084a-7562-4d36-ab31-115809635b06/touchybooks-menu3.jpg" width="550" height="120" alt="touchybooks-menu3" /></a></figure>

## If You Try To Trick My Kid Into Buying Stuff, You’re Dead To Me

I’m looking at you, [Talking Tom Cat](https://itunes.apple.com/us/app/talking-tom-cat-2/id421997825?mt=8). A lot of apps do this, but Talking Tom Cat is the absolute worst. The screen is a landmine of carefully placed icons that **lead to accidental purchases** &mdash; not to mention the random animated banner ads that are designed to draw attention away from the app itself. GoDaddy’s [dark patterns](https://wiki.darkpatterns.org/) that try to trick users into buying more domains are one thing, but if you try to use [persuasive design](https://www.cennydd.co.uk/2010/the-perils-of-persuasion/) on my young daughter, all bets are off. Your app will be deleted, and we’ll never do business again.

<figure><a href="https://itunes.apple.com/us/app/talking-tom-cat-2/id421997825?mt=8"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e51b838b-0908-4adc-9186-0aa210cf8790/talking-tom-yuck.jpg" width="413" height="550" alt="talking-tom-yuck" /></a></figure>

## Conclusion

Designing apps for children is extremely hard. Not only is quality, age-appropriate content hard to create, but designing the flow and interaction of these apps is made more difficult because designers must refrain from implementing advanced gestures, which would only confuse and frustrate kids (and, by extension, their parents). Yet **all apps can and should adhere to certain basics**. Hopefully, the four guidelines discussed here can become fixtures of all children’s apps.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Ten Things To Think About When Designing Your iPad App](https://www.smashingmagazine.com/2012/01/ten-things-to-think-about-when-designing-your-ipad-app/)
*   [Designing Web Interfaces For Kids](https://www.smashingmagazine.com/2015/08/designing-web-interfaces-for-kids/)
*   [Useful Design Tips For Your iPad App](https://www.smashingmagazine.com/2010/04/design-tips-for-your-ipad-app/)
*   [Designing For Kids Is Not Child’s Play](https://www.smashingmagazine.com/2016/01/designing-apps-for-kids-is-not-childs-play/)

{{< signature "al, fi, il" >}}
