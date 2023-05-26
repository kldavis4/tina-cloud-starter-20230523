---
title: Transform A Tablet Into An Affordable Kiosk For Your Clients
slug: transform-tablet-affordable-kiosk-clients
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57fd0c30-d77c-4215-9984-92fad38cc42c/ipad-mounted2.jpg
date: 2012-11-26T16:13:49.000Z
author: jason-mark
description: >-
  Twenty minutes after unboxing my first iPad, I realized this device’s potential to revolutionize the world of kiosks.
categories:
  - Mobile
  - Business
  - Clients
  - Devices
  - iOS
  - iPad
---
Ten years ago, my team and I worked with Honda to develop touchscreen kiosks for its dealerships. Potential buyers could customize their purchase with a few touches of their fingertips. While innovative at the time, these early interactive kiosks didn’t come cheap, running Honda $3,000 to $5,000 per installation. Today, we can create such a kiosk for a fraction of the price.

Recommended reading: [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)

Which industries are the most likely candidates for tablet kiosks? Four that immediately spring to mind are hotels, restaurants, museums and retailers. Kiosks help streamline information-gathering processes, such as signing up for mailing lists, making reservations, ordering products and services and checking in and out of locations.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Design For Android Tablets](https://www.smashingmagazine.com/2011/08/designing-for-android-tablets/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)

By automating these processes, the kiosk eliminates the customer’s frustration from waiting in line to speak with a representative and, likewise, frees the employees to focus their energies on higher-level tasks.

{{% feature-panel %}}

Recent consumer-privacy laws put limits on the data that retailers may capture during a transaction. For example, a recent California ruling forbids the process of “reverse appending” by ZIP code. Kiosks give the retailer a second chance to collect customer data, away from the cash register. A privacy-savvy customer might balk at providing their personal information to a cashier at the time of purchase and yet be willing to enter the same information at a kiosk for a contest or discount. Success depends on having an appealing interface that encourages interaction.</p>

## Step 1: Hardware Considerations

Obviously, your client will need a tablet for this project. We’ll focus on the iPad here because it is what most of our clients choose, but other platforms such as Kindle Fire could also be used as kiosks. Whichever device you choose, consider how to secure the tablet so that it doesn’t disappear! We developed a device that securely mounts an iPad to a wall, counter or desk (<em>Padloc</em>). Remember that physical security is key; an unsecured tablet is an attractive target for thieves.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/188bb1cb-b7f2-4304-b5f5-89d98c3ec91b/droppedimage.jpg"><img class="111682" title="droppedImage" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/188bb1cb-b7f2-4304-b5f5-89d98c3ec91b/droppedimage.jpg" alt="iPad mounted in retail setting" width="500" height="289" /></a><br>
<em>iPad securely mounted with a Padloc.</em>

## Step 2: Software Considerations

Is it really necessary to develop an application for the kiosk? Perhaps your client simply wants to display their website or use a third-party app. In our experience, however, a customized interface can make or break the user experience. We recently worked with a client to develop a simple interface for gathering email addresses in exchange for special offers. Here is the process we followed:

1.  We decided to create a Web app rather than a conventional app, thus bypassing a potentially lengthy and complicated submission and approval process through the App Store.
2.  We picked the device to program on (in this case, the iPad). This was important because, knowing we would be using Mobile Safari, with all of the interesting little nuances available for it (through HTML5 and CSS3), we were able to streamline production.
3.  We designed an interface that was visually striking, intuitive and compliant with interface guidelines (including those related to the on-screen keyboard, viewport size and touchscreen conventions). (Apple has some great resources for developers, such as its [Human Interface Guidelines](https://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/Introduction/Introduction.html "Apple Human Interface Guidelines").)
4.  Because we were working in mobile Safari on the iPad, we were able to program some cool features into the Web app. But these came with restrictions, such as:
    *   The features would work only in portrait orientation,
    *   The Web app had to be saved to the iPad’s home screen and launch from there,
    *   All links in the Web app would open in a new browser tab.
5.  We also made some other tweaks:
    *   Hid the browser chrome (URL bar and buttons) using `<meta name="apple-mobile-web-app-capable" content="yes" />`;
    *   Created a bookmark icon for the home screen and linked to it using `<link rel="apple-touch-icon" href="/path/to/icon.png" />`;
    *   Set the color of the status bar (the options are black, gray or black translucent) using `<meta name="apple-mobile-web-app-status-bar-style" content="black" />`;
    *   Made all events `touch` events, as opposed to `hover` events, to accommodate the limitations of the touchscreen.</p>

## Do Clients Really Want This?

What is the current demand for touchscreen tablet kiosks? We recently conducted a survey of our existing and potential clients; 89% indicated that they would use a touchscreen for a kiosk, and the iPad was the tablet of choice for 84% of them.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20e8b164-1bae-4695-b4b4-27fcee92ef97/kiosk-survey-v2.jpg"><img class="111680" title="kiosk_survey-v2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20e8b164-1bae-4695-b4b4-27fcee92ef97/kiosk-survey-v2.jpg" alt="Survey Results" width="500" height="275" /></a><br>
<em>The results of our survey</em>

Pretty eye-opening, eh? We also asked survey participants to identify the biggest factor affecting their decision to move forward with a kiosk (choosing from 10 options, ranging from price to screen size to operating system to security options). Price was most important for 41% of respondents, with screen size coming next at 18%.

Recommended reading: [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)

Interestingly, a majority of respondents chose the iPad, yet also mentioned price as their top concern. This suggests that lower-cost entrants to the market (such as the Kindle Fire) are well positioned to gain market share and become viable candidates for these kiosk projects. Our survey shows a strong desire for kiosks, and the price barrier has been removed with these low-cost tablets!

## A Bright Future With New Possibilities

In addition, a wide array of hardware is constantly emerging, creating previously unimagined possibilities. Consider <a href="https://squareup.com/">Square</a>’s reader. Plug this tiny device into the headphone jack of your iPad, download the app, and you’re ready to take credit-card payments. Now, add a locking mount, install it anywhere in your store or in your trade-show booth, and you’ll have the best-looking, quickest-to-set-up cash register you’ve ever seen!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1537e783-7620-4bfd-84d5-f9e768d343a1/droppedimage-2.jpg"><img class="111683" title="droppedImage-2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1537e783-7620-4bfd-84d5-f9e768d343a1/droppedimage-2.jpg" alt="Padloc in Restaurant setting" width="500" height="287" /></a><br>
<em>iPad mounted with a Square reader to accept payments.</em>

As more advanced devices are introduced to the marketplace, the traditional limitations of kiosks are being surmounted. It’s time for us to think outside the box and imagine a new future for low-cost tablet kiosks!

## Conclusion

The clunky, expensive kiosks of yesterday are becoming irrelevant in today’s world of elegant low-cost touchscreen devices. Whether clients want to capture email addresses, enable customers to sign up for events in the store or add interactive elements to their artwork, a touchscreen kiosk can deliver the results they’re looking for. Tablet kiosks can be integrated into any decor smartly and sleekly. Now that affordability is no longer a factor, you can start working with clients to develop apps that bring imagination back to their business solutions.

{{< signature "al" >}}

