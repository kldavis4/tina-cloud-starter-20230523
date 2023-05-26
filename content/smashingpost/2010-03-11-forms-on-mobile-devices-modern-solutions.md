---
title: 'Forms On Mobile Devices: Modern Solutions'
slug: forms-on-mobile-devices-modern-solutions
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8653313-2170-463a-ab33-1597691830c4/mobile2.jpg
date: 2010-03-11T11:58:05.000Z
author: luke-wroblewski
description: >-
  Mobile forms tend to have significantly more constraints than their desktop
  cousins: screens are smaller; connections are slower; text entry is trickier;
  the list goes on. So, limiting the number of forms in your mobile applications
  and websites is generally a good idea. When you do want input from users on
  mobile devices, radio buttons, checkboxes, select menus and lists tend to work
  much better than open text fields.

  But **constraints breed innovation**, and mobile forms are no different. The
  limitations of mobile devices have forced developers and designers to find new
  ways to allow users to input data faster and more easily. Thanks to the modern
  solutions covered in this article, the mobile space may not be a place to
  avoid forms much longer. Instead, it may become _the_ place to encourage them.
categories:
  - UX
  - Forms
  - Showcases
  - Web Design
---
Mobile forms tend to have significantly more constraints than their desktop cousins: screens are smaller; connections are slower; text entry is trickier; the list goes on. So, limiting the number of forms in your mobile applications and websites is generally a good idea. When you do want input from users on mobile devices, radio buttons, checkboxes, select menus and lists tend to work much better than open text fields.

But <strong>constraints breed innovation</strong>, and mobile forms are no different. The limitations of mobile devices have forced developers and designers to find new ways to allow users to input data faster and more easily. Thanks to the modern solutions covered in this article, the mobile space may not be a place to avoid forms much longer. Instead, it may become <em>the</em> place to encourage them.

You may also want to check out the following Smashing Magazine articles:

*   [Guidelines For Mobile Web Development](https://www.smashingmagazine.com/guidelines-for-mobile-web-development/)
*   [<span class="headline">Designing A Better Mobile Checkout Process</span>](https://www.smashingmagazine.com/2013/03/designing-a-better-mobile-checkout-process/)
*   [Mobile And Accessibility: Why You Should Care And What You Can Do About It](https://www.smashingmagazine.com/2014/05/mobile-accessibility-why-care-what-can-you-do/)

## Field Zoom

In many mobile Web browsers, when a user selects a form’s input field, the "field zoom" feature expands it to fill the screen's viewable area. This makes an otherwise tiny field large enough for people to actually see the data they are entering. Given that many form errors are caused by people not seeing their inputs well enough <a href="https://www.lukew.com/ff/entry.asp?941">to correct misspellings</a>, the usability of this feature is clear.

{{% feature-panel %}}

The Safari browser on Apple's iPhone makes use of field zoom together with a "form assistant." The form assistant displays "Previous," "Next," "AutoFill" and "Done" buttons below the magnified input field, giving people an easy way to move through and complete a form. No need to worry if an input field is off screen: the user just hits "Next" and won't miss it!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a41167a-71f4-4009-97d1-809869ac2672/mobileinputs1.jpg" width="600" height="423" />

However, not everyone will know about the form assistant or know how to hide the keyboard. So, make sure the controls on the Web page still allow them to complete the form. Excessive spacing around the "Submit" button can tuck it behind the keyboard.

Field zoom is another great reason to <a href="https://www.lukew.com/ff/entry.asp?504">top-align input field labels</a> in forms. As you can see on Google's registration form (screenshot below), left-aligned labels disappear when input fields are expanded to fill the screen. With no visible label, the user can easily forget what question they have to answer. Long input fields also suffer a bit with field zoom.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c060533e-bb67-480d-876e-3cc5cfc4b2b6/mobileinputs2.jpg" width="600" />

Mobile browsers that don't have field zoom also run into issues with left- and right-aligned input field labels. Anyone using such a form on Google's Android OS (below) faces the problem of disappearing labels. The screen simply does not have enough room for both the input field and its corresponding label. Top-aligned labels avoid this issue.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fb0365e-232c-4aed-845b-e3748bee0096/mobileinputs3.jpg" width="600" />

## Input Formats

Some mobile Web browsers recognize <a href="https://diveintohtml5.org/forms.html">specific input types</a> (part of the developing HTML5 standard) and adjust their input modes accordingly. For example, specifying an input of the type <code>url</code> brings up a virtual alphanumeric keyboard with ".", "/", and ".com" keys. Specifying an input of the type <code>email</code> brings up a virtual alphanumeric keyboard with "." and "@" keys. Specifying an input of the type <code>number</code> brings up a virtual numeric keyboard.

These input-specific keyboards make entering the particular type of data required by each input field much easier. Even browsers without virtual keyboards benefit from the use of <code>number</code>, because users would not have to switch to number mode to enter numeric data.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65a34856-d3d5-45f1-aba5-a1ae1f1b9010/mobileinputs4.jpg" width="600" />

## Password-Masking

Most password input fields in forms instantly obscure all characters that a user enters to keep sensitive information hidden from prying eyes. Automatic masking of passwords may provide <a href="https://www.zurb.com/article/279/how-to-mask-passwords-like-the-iphone">the appearance of security</a>, but it can also create usability issues when people are left staring at a row of bullets that they hope (but can't verify) is their password.

Many mobile devices address this issue by displaying the most recent character the user has entered, and then obscuring that character as a bullet only after a brief delay. This technique has made its way onto the desktop, as illustrated in this <a href="https://www.zurb.com/article/279/how-to-mask-passwords-like-the-iphone">password-masking solution</a> from ZURB.</p>

## Pop-Up Menu Controls

Drop-down select menus are one of the hardest input types to use. First, you have to click on the menu to open it. Then, you have to maneuver through a potentially long list of small targets. Once you find the value you want, you need position your cursor on the right target and select it. To top it off, many implementations of drop-down menus on the Web require you to keep your cursor on the menu while navigating the list, or else the menu closes!

Even dexterous users often miss them and need to start over. Couple this interactive challenge with the small screens of mobile devices and the need for a different solution for select menus becomes quite obvious.

For drop-down select menus on Web forms, Apple's iPhone presents users with a pop-up menu control. This control displays the options in the menu in a contained list that can be scrolled at various speeds though drag, nudge and flick gestures. The large touch targets also make it easy to select the right value once you've found it.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daca7963-45b8-4a6a-b39a-02139f0e49ce/mobileinputs5.jpg" width="600" />

Similarly, Google's Android provides a larger touch target for select menu options. When the user taps a drop-down select menu on an Android device, a scrollable list of menu options appears in a dialog window over the Web page.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69fc5a42-cbb9-4a67-91ba-3506b637530f/mobileinputs6.jpg" width="600" />

## Compound Menu Controls

Pop-up menu controls can be applied to compound inputs as well. So, instead of requiring three separate input fields for the month, day and year of a requested date, one date field can bring up a set of pop-up menus that allow people to scroll through three lists at once to find the right date. This approach can be applied to other kinds of compound inputs as well, such as height in feet and inches.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d19515bf-87c4-4774-be7f-b197def064f8/mobileinputs7.jpg" width="600" />

Google's Android has a compound input field solution, though it makes use of visible interface elements to move through a list instead of relying on gesture-based scrolling alone.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a3cc321-f896-41ea-b772-8c4fd21f0593/mobileinputs8.jpg" width="600" />

## Native Input Controls

In addition to having compound menu controls, most mobile operating systems have several other custom input controls available to application developers. Sliders, split buttons, rating widgets and scrubbers are just a few of the components worth considering in place of standard form controls to make inputting easier for users.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a616570e-fb5c-4d41-b3fa-369bd0464110/mobileinputs9.jpg" width="600" />

## Orientation

Because people like to hold mobile devices both horizontally and vertically in their hands, mobile forms should adjust accordingly to take advantage of the changing screen space. The compose email form on Google's Android does just that.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8dc7f0c-f20e-4aed-b0f1-1734b4900e88/mobileinputs10.jpg" width="600" />

When held vertically, the screen shows three input fields with several action buttons. In the horizontal position, the email body input takes over the screen, and one action button is shown on the right. This layout maximizes the screen space available for the message content.</p>

## Voice Input

Google's <a href="https://youtube.com/user/GoogleNexusOne">Nexus One</a> phone allows people to use voice input for any text field in an application. Users can swipe the virtual keyboard to switch the phone to audio input mode, or they can use the microphone button. The video below demonstrates both of these options in action. With effective voice input, typing any characters into the mobile device becomes a thing of the past.</p>

## What's Next?

Mobile is growing <a href="https://www.lukew.com/ff/entry.asp?993">exceptionally fast</a>, and as more designers and developers focus on the space, we'll hopefully see even further innovation in mobile forms. After all, anything that makes inputting (both on mobile and desktop devices) faster and easier will do <span class="removed_link" title="https://nform.ca/blog/2008/10/luke-wroblewski-on-forms-visua">a lot of good</span> for both companies and their customers.</p>

### About the Author

Luke Wroblewski is an internationally recognized <a href="https://www.lukew.com/about/index.asp">digital product design leader</a> and the author of <a href="https://www.lukew.com/ff/">two popular Web design books</a>. You can follow Luke on Twitter <a href="https://www.twitter.com/lukewdesign">@lukewdesign</a> or by using <a href="https://feeds.feedburner.com/FunctioningForm">RSS</a>.

Smashing Magazine readers can get a special <strong>20% off discount</strong> on Luke's latest book: Web Form Design Filling in the Blanks. Just use discount code <strong>MIX</strong> to order.

{{< signature "al" >}}

