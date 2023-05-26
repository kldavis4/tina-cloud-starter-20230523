---
title: Color Contrast And Why You Should Rethink It
slug: color-contrast-tips-and-tools-for-accessibility
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2463e545-f45e-4580-97c4-164e54679c92/weathervisionsim-large.png
date: 2014-10-22T21:07:33.000Z
author: cathyoconnor
description: >-
  When you browse your favorite website or check the latest version of your
  product on your device of choice, take a moment to look at it differently.
  Step back from the screen. Close your eyes slightly so that your vision is a
  bit clouded by your eyelashes. Can you still see and use the website? Are you
  able to read the labels, fields, buttons, navigation and small footer text?
  Can you imagine how someone who sees differently would read and use it?

  In this article, I’ll share one aspect of design accessibility: making sure
  that the look and feel (the visual design of the content) are sufficiently
  inclusive of differently sighted users.
categories:
  - UX
  - Colors
  - Color Theory
  - Accessibility
---
When you browse your favorite website or check the latest version of your product on your device of choice, take a moment to look at it differently. Step back from the screen. Close your eyes slightly so that your vision is a bit clouded by your eyelashes.

*   Can you still see and use the website?
*   Are you able to read the labels, fields, buttons, navigation and small footer text?
*   Can you imagine how someone who sees differently would read and use it?

In this article, I’ll share one aspect of design accessibility: making sure that the look and feel (the visual design of the content) are sufficiently inclusive of differently sighted users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c227a6ed-392b-4159-8643-dc22f8b67618/nocoffeevis-large.png"><img loading="lazy" decoding="async" title="Color Contrast And Why You Should Rethink It" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a065d5f-caf5-47de-8792-9ec972332d8a/nocoffeevis-500px.png" alt="Color Contrast And Why You Should Rethink It" width="500" height="255" /></a><figcaption>Web page viewed with NoCoffee low-vision simulation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c227a6ed-392b-4159-8643-dc22f8b67618/nocoffeevis-large.png">View large version</a>)</figcaption></figure>

I am a design consultant on PayPal’s accessibility team. I assess how our product designs measure up to the Web Content Accessibility Guidelines (WCAG) 2.0, and I review our company’s design patterns and best practices.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">The Underestimated Power Of Color In Mobile App Design</span>](https://www.smashingmagazine.com/2017/01/underestimated-power-color-mobile-app-design/)
*   [Color Theory for Designers, Part 1: The Meaning of Color](https://www.smashingmagazine.com/2010/01/color-theory-for-designers-part-1-the-meaning-of-color/)
*   [<span class="headline">The Code Side Of Color</span>](https://www.smashingmagazine.com/2012/10/the-code-side-of-color/)
*   [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)

I created our “Designers’ Accessibility Checklist,” and I will cover one of the most impactful guidelines on the checklist in this article: making sure that there is sufficient color contrast for all content. I’ll share the strategies, tips and tools that I use to help our teams deliver designs that most people can see and use without having to customize the experiences.

Our goal is to make sure that all visual designs meet the minimum color-contrast ratio for normal and large text on a background, as described in the WCAG 2.0, Level AA, “<a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html">Contrast (Minimum): Understanding Success Criterion 1.4.3</a>.”

Who benefits from designs that have sufficient contrast? Quoting from the WCAG’s page:
<blockquote>The 4.5:1 ratio is used in this provision to account for the loss in contrast that results from moderately low visual acuity, congenital or acquired color deficiencies, or the loss of contrast sensitivity that typically accompanies aging.</blockquote>

As an accessibility consultant, I’m often asked how many people with disabilities use our products. Website analytics do not reveal this information. Let’s estimate how many people could benefit from designs with sufficient color contrast by reviewing the statistics:

*   15% of the [world’s population have some form of disability](https://www.who.int/mediacentre/factsheets/fs352/en/), which includes conditions that affect seeing, hearing, motor abilities and cognitive abilities.
*   About 4% of the population have low vision, whereas 0.6% are blind.
*   7 to 12% of men have some form of color-vision deficiency (color blindness), and less than 1% of women do.
*   Low-vision conditions increase with age, and half of people over the age of 50 have some degree of low-vision condition.
*   Worldwide, the [fastest-growing population is 60 years of age and older](https://www.un.org/esa/population/publications/worldageing19502050/).
*   Over the age of 40, most everyone will find that they need reading glasses or bifocals to clearly see small objects or text, a condition caused by the natural aging process, called [presbyopia](https://www.mayoclinic.org/diseases-conditions/presbyopia/basics/causes/con-20032261).

Let’s estimate that 10% of the world population would benefit from designs that are easier to see. Multiply that by the number of customers or potential customers who use your website or application. For example, out of 2 million online customers, 200,000 would benefit.

Some <a href="https://www.nei.nih.gov/catalog/aging-eye-health-infographic">age-related low-vision conditions</a> include the following:

*   **Macular degeneration**.  Up to 50% of people are affected by age-related vision loss.
*   **Diabetic retinopathy**.  In people with diabetes, leaking blood vessels in the eyes can cloud vision and cause blind spots.
*   **Cataracts**.  Cataracts clouds the lens of the eye and decreases visual acuity.
*   **Retinitis pigmentosa**.  This inherited condition gradually causes a loss of vision.

All of these conditions reduce sensitivity to contrast, and in some cases reduce the ability to distinguish colors.

Color-vision deficiencies, also called color-blindness, are mostly inherited and can be caused by side effects of medication and age-related low-vision conditions.

Here are the types of <a href="https://webaim.org/articles/visual/colorblind">color-vision deficiencies</a>:

*   **Deuteranopia**.  This is the most common and entails a reduced sensitivity to green light.
*   **Protanopia**.  This is a reduced sensitivity to red light.
*   **Tritanopia**.  This is a reduced sensitivity to blue light, but not very common.
*   **Achromatopsia**.  People with this condition cannot see color at all, but it is not very common.

Reds and greens or colors that contain red or green can be difficult to distinguish for people with deuteranopia or protanopia.</p>

## Experience Seeing Differently

Creating a checklist and asking your designers to use it is easy, but in practice how do you make sure everyone follows the guidelines? We’ve found it important for designers not only to intellectually understand the why, but to experience for themselves what it is like to see differently. I’ve used a couple of strategies: immersing designers in interactive experiences through our Accessibility Showcase, and showing what designs look like using software simulations.

In mid-2013, we opened our PayPal Accessibility Showcase (video). Employees get a chance to experience first-hand what it is like for people with disabilities to use our products by interacting with web pages using goggles and/or assistive technology. We require that everyone who develops products participates in a tour. The user scenarios for designing with sufficient color contrast include wearing goggles that simulate conditions of low or partial vision and color deficiencies. Visitors try out these experiences on a PC, Mac or tablet. For mobile experiences, visitors wear the goggles and use their own mobile devices.

Fun fact: One wall in the showcase was painted with magnetic paint. The wall contains posters, messages and concepts that we want people to remember. At the end of the tour, I demonstrate vision simulators on our tablet. I view the message wall with the simulators to emphasize the importance of sufficient color contrast.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3451b09-b08e-4251-a391-aaee5c32b31b/a11ytoursgoggles-500px.jpg" alt="Showcase visitors wear goggles that simulate low-vision and color-blindness conditions" /><figcaption>Showcase visitors wear goggles that simulate low-vision and color-blindness conditions.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4d3a187-9795-4f96-9344-251c33227f31/goggles-500px.jpg" alt="Some of the goggles used in the Accessibility Showcase" /><figcaption>Some of the goggles used in the Accessibility Showcase.</figcaption></figure>

## Software Simulators

### Mobile Apps

Free mobile apps are available for iOS and Android devices:

*   **Chromatic Vision Simulator**.  Kazunori Asada’s app simulates three forms of color deficiencies: protanope (protanopia), deuteranope (deuteranopia) and tritanope (tritanopia). You can view and then save simulations using the camera feature, which takes a screenshot in the app. (Available for [iOS](https://itunes.apple.com/us/app/chromatic-vision-simulator/id389310222?mt=8 "CVSimulator for Apple iOS") and [Android](https://play.google.com/store/apps/details?id=asada0.android.cvsimulator&hl=en "CVSimulator for Android devices").)
*   **VisionSim**.  The Braille Institute’s app simulates a variety of low-vision conditions and provides a list of causes and symptoms for each condition. You can view and then save simulations using the camera feature, which takes a screenshot in the app. (Available for [iOS](https://itunes.apple.com/us/app/visionsim-by-braille-institute/id525114829?mt=8 "VisionSim app forApple iOS devices") and Android.)

### Chromatic Vision Simulator

The following photos show orange and green buttons viewed through the Chromatic Vision Simulator:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b899bd-93e0-4ccb-8fb7-e7a9cc278afb/cvsbuttonsog-large.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f465207-e220-441d-abdd-d03c92443838/cvsbuttonsog-500px.jpg" alt="Seen through Chromatic Vision Simulator, the green and orange buttons show normal (C), protanope (P), deuteranope (D) and tritanope (T)." width="500" height="375" /></a><figcaption>Seen through Chromatic Vision Simulator, the green and orange buttons show normal (C), protanope (P), deuteranope (D) and tritanope (T). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b899bd-93e0-4ccb-8fb7-e7a9cc278afb/cvsbuttonsog-large.jpg">View large version</a>)</figcaption></figure>

This example highlights the importance of another design accessibility guideline: Do not use color alone to convey meaning. If these buttons were online icons representing a system’s status (such as up or down), some people would have difficulty understanding it because there is no visible text and the shapes are the same. In this scenario, include visible text (i.e. text labels), as shown in the following example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55cd6d4d-d5e1-4143-9c2b-aaae6c482b99/textonbuttons-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/910aa786-f6cc-4e51-8c2b-d8591fc91630/textonbuttons-500px.png" alt="The green and orange buttons are viewed in Photoshop with deuteranopia soft proof and normal (text labels added)." /></a><figcaption>The green and orange buttons are viewed in Photoshop with deuteranopia soft proof and normal (text labels added). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55cd6d4d-d5e1-4143-9c2b-aaae6c482b99/textonbuttons-large.png">View large version</a>)</figcaption></figure>

### Mobile Device Simulations

Checking for sufficient color contrast becomes even more important on mobile devices. Viewing mobile applications through VisionSim or Chromatic Vision Simulator is easy if you have two mobile phones. View the mobile app that you want to test on the second phone running the simulator.

If you only have one mobile device, you can do the following:

1.  Take screenshots of the mobile app on the device using the built-in camera.
2.  Save the screenshots to a laptop or desktop.
3.  Open and view the screenshots on the laptop, and use the simulators on the mobile device to view and save the simulations.</p>

### How’s the Weather in Cupertino?

The following example highlights the challenges of using a photograph as a background while making essential information easy to see. Notice that the large text and bold text are easier to see than the small text and small icons.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b6f7ab1-8b4b-4fdd-bd74-b42073620f33/weathercvs-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e2c6c7c-52b3-45ac-b4b8-5d2a90437c22/weathercvs-500px.png" alt="The Weather mobile app, viewed with Chromatic Vision Simulator, shows normal, deuteranope, protanope and tritanope simulations." /></a><figcaption>The Weather mobile app, viewed with Chromatic Vision Simulator, shows normal, deuteranope, protanope and tritanope simulations. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b6f7ab1-8b4b-4fdd-bd74-b42073620f33/weathercvs-large.png">View large version</a>)</figcaption></figure>

### Low-Vision Simulations

Using the VisionSim app, you can simulate macular degeneration, diabetic retinopathy, retinitis pigmentosa and cataracts.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2463e545-f45e-4580-97c4-164e54679c92/weathervisionsim-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee17a407-deb1-47b8-8f03-b46e9a8b2a64/weathervisionsim-500px.png" alt="The Weather mobile app is being viewed with the supported condition simulations." /></a><figcaption>The Weather mobile app is being viewed with the supported condition simulations. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2463e545-f45e-4580-97c4-164e54679c92/weathervisionsim-large.png">View large version</a>)</figcaption></figure>

## Adobe Photoshop

PayPal’s teams use Adobe Photoshop to design the look and feel of our user experiences. To date, a color-contrast ratio checker or tester is not built into Photoshop. But designers can use a couple of helpful features in Photoshop to check their designs for sufficient color contrast:

*   Convert designs to grayscale by going to “Select View” → “Image” → “Adjustments” → “Grayscale.”
*   Simulate color blindness conditions by going to “Select View” → “Proof Setup” → “Color Blindness” and choosing protanopia type or deuteranopia type. Adobe provides [soft-proofs for color blindness](https://help.adobe.com/en_US/creativesuite/cs/using/WS3F71DA01-0962-4b2e-B7FD-C956F8659BB3.html#WS473A333A-7F61-4aba-8F67-5553208E349C).</p>

### Examples

If you’re designing with gradient backgrounds, verify that the color-contrast ratio passes for the text color and background color on both the lightest and darkest part of the gradient covered by the content or text.

In the following example of buttons, the first button has white text on a background with an orange gradient, which does not meet the minimum color-contrast ratio. A couple of suggested improvements are shown:

*   add a drop-shadow color that passes (center button),
*   change the text to a color that passes (third button).

Checking in Photoshop with the grayscale and deuteranopia proof, the modified versions with the drop shadow and dark text are easier to read than the white text.

If you design in sizes larger than actual production sizes, make sure to check how the design will appear in the actual web page or mobile device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26608601-7d3c-4864-bf3e-df41652d0a3b/buttongradients-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7cd71e7-c1b6-4b45-a350-f22295176db2/buttongradients-500px.png" alt="Button with gradients: normal view; view in grayscale; and as a proof, deuteranopia." /></a><figcaption>Button with gradients: normal view; view in grayscale; and as a proof, deuteranopia. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26608601-7d3c-4864-bf3e-df41652d0a3b/buttongradients-large.png">View large version</a>)</figcaption></figure>

In the following example of a form, the body text and link text pass the minimum color-contrast ratio for both the white and the gray background. I advise teams to always check the color contrast of text and links against all background colors that are part of the experience.

Even though the “Sign Up” link passes, if we view the experience in grayscale or with proof deuteranopia, distinguishing that “Sign Up” is a link might be difficult. To improve the affordance of “Sign Up” as a link, underline the link or link the entire phrase, “New to PayPal? Sign Up.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db7f349f-86c8-458d-8ac3-a8314215227a/logindev-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/716b601a-632d-40f7-8331-1b8bf1adaee7/logindev-500px.png" alt="Form example: normal view; in Photoshop, a view in grayscale; and as a proof, deuteranopia." /></a><figcaption>Form example: normal view; in Photoshop, a view in grayscale; and as a proof, deuteranopia. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db7f349f-86c8-458d-8ac3-a8314215227a/logindev-large.png">View large version</a>)</figcaption></figure>

Because red and green can be more difficult to distinguish for people with conditions such as deuteranopia and protanopia, should we avoid using them? Not necessarily. In the following example, a red minus sign (“-”) indicates purchasing or making a payment. Money received or refunded is indicated by a green plus sign (“+”). Viewing the design with proof, deuteranopia, the colors are not easy to distinguish, but the shapes are legible and unique. Next to the date, the description describes the type of payment. Both shape and content provide context for the information.

Also shown in this example, the rows for purchases and refunds alternate between white and light-gray backgrounds. If the same color text is used for both backgrounds, verify that all of the text colors pass for both white and gray backgrounds.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62063dc4-245d-4028-9815-a72cd3c37be9/rowsandicons-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be9d746d-7e6c-40d1-9ddc-92631f209f62/rowsandicons-500px.png" alt="Normal view and as a proof, deuteranopia: Check the text against the alternating background colors." /></a><figcaption>Normal view and as a proof, deuteranopia: Check the text against the alternating background colors. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62063dc4-245d-4028-9815-a72cd3c37be9/rowsandicons-large.png">View large version</a>)</figcaption></figure>

In some applications, form fields and/or buttons may be disabled until information has been entered by the user. Our design guidance does not require disabled elements to pass, in accordance with the WCAG 2.0’s “<a href="https://www.w3.org/TR/2014/NOTE-UNDERSTANDING-WCAG20-20140311/visual-audio-contrast-contrast.html">Contrast (Minimum): Understanding Success Criterion 1.4.3</a>:
<blockquote>Incidental: Text or images of text that are part of an inactive user interface component,… have no contrast requirement.</blockquote>

In the following example of a mobile app’s form, the button is disabled until a phone number and PIN have been entered. The text labels for the fields are a very light gray over a white background, which does not pass the minimum color-contrast ratio.

If the customer interprets that form elements with low contrast are disabled, would they assume that the entire form is disabled?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a789d3c-7c51-449f-8ea3-1cea7df67eca/mobiledisabledfields-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b01fe2b5-a975-41a2-a51c-c52c6623dbb4/mobiledisabledfields-500px.png" alt="Mobile app form showing disabled fields and button (left) and then enabled (right)." /></a><figcaption>Mobile app form showing disabled fields and button (left) and then enabled (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a789d3c-7c51-449f-8ea3-1cea7df67eca/mobiledisabledfields-large.png">View large version</a>)</figcaption></figure>

The same mobile app form is shown in a size closer to what I see on my phone in the following example. At a minimum, the text color needs to be changed or darkened to pass the minimum color-contrast ratio for normal body text and to improve readability.

To help distinguish between labels in fields and user-entered information, try to explore alternative visual treatments of form fields. Consider reversing foreground and background colors or using different font styles for labels and for user-entered information.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6a823a5-6deb-4b67-a6b0-94ec1e671462/mobiledisabledfields-bwcc-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ade5f5c-730b-4b43-9cd5-37ae5d5d6265/mobiledisabledfields-bwcc-500px.png" alt="Mobile app form example: normal, grayscale and proof deuteranopia." /></a><figcaption>Mobile app form example: normal, grayscale and proof deuteranopia. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6a823a5-6deb-4b67-a6b0-94ec1e671462/mobiledisabledfields-bwcc-large.png">View large version</a>)</figcaption></figure>

## NoCoffee Vision Simulator for Chrome

<a href="https://chrome.google.com/webstore/search/NoCoffee%20Vision%20Simulator?hl=en&amp;gl=US">NoCoffee Vision Simulator</a> can be used to simulate color-vision deficiencies and low-vision conditions on any pages that are viewable in the Chrome browser. Using the “Color Deficiency” setting “achromatopsia,” you can view web pages in grayscale.

The following example shows the same photograph (featuring a call to action) viewed with some of the simulations available in NoCoffee. The message and call to action are separated from the background image by a practically opaque black container. This improves readability of the message and call to action. Testing the color contrast of the blue color in the headline against solid black passes for large text. Note that the link “Mobile” is not as easy to see because the blue does not pass the color-contrast standard for small body text. Possible improvements could be to change the link color to white and underline it, and/or make the entire phrase “Read more about Mobile” a link.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca8ce9b6-dbbf-45da-9809-c1c5023cc10a/nocoffeecolorsim-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13738bd6-9213-42e4-8978-4cdaada6e02f/nocoffeecolorsim-500px.png" alt="Simulating achromatopsia (no color), deuteranopia, protanopia using NoCoffee." /></a><figcaption>Simulating achromatopsia (no color), deuteranopia, protanopia using NoCoffee. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca8ce9b6-dbbf-45da-9809-c1c5023cc10a/nocoffeecolorsim-large.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c67e6f14-28da-408f-9400-e5c9ec98e0dd/nocoffeevisionsims-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0806d9fe-7648-4490-a93b-e67980a212e7/nocoffeevisionsims-500px.png" alt="Simulating low visual acuity, diabetic retinopathy, macular degeneration and low visual acuity plus retinitus pigmentosa, using NoCoffee." /></a><figcaption>Simulating low visual acuity, diabetic retinopathy, macular degeneration and low visual acuity plus retinitus pigmentosa, using NoCoffee. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c67e6f14-28da-408f-9400-e5c9ec98e0dd/nocoffeevisionsims-large.png">View large version</a>)</figcaption></figure>

## Using Simulators

Simulators are useful tools to visualize how a design might be viewed by people who are aging, have low-vision conditions or have color-vision deficiencies.

For design reviews, I use the simulators to mock up a design in grayscale, and I might use color-blindness filters to show designers possible problems with color contrast. Some of the questions I ask are:

*   Is anything difficult to read?
*   Is the call to action easy to find and read?
*   Are links distinguishable from other content?

After learning how to use simulators to build empathy and to see their designs differently, I ask designers to use tools to check color contrast to verify that all of their designs meet the minimum color-contrast ratio of the WCAG 2.0 AA. The checklist includes a couple of tools they can use to test their designs.</p>

## Color-Contrast Ratio Checkers

The tools we cite in the designers’ checklist are these:

*   [WebAIM Color Contrast Checker](https://webaim.org/resources/contrastchecker), a browser-based tool, tests color codes specified in hexadecimal values.
*   The Paciello Group’s Colour Contrast Checker, an application available for Macs or PCs, tests color codes specified in RGB values.

There are many tools to check color contrast, including ones that check live products. I’ve kept the list short to make it easy for designers to know what to use and to allow for consistent test results.

Our goal is to meet the WCAG 2.0 AA color-contrast ratio, which is 4.5 to 1 for normal text and 3 to 1 for large text.

What are the minimum sizes for normal text and large text? The guidance provides recommendations on size ratios in the WCAG’s <a href="https://www.w3.org/TR/2014/NOTE-UNDERSTANDING-WCAG20-20140311/visual-audio-contrast-contrast.html">Contrast (Minimum): Understanding Success Criterion 1.4.3</a> but not a rule for a minimum size for body text. As noted in the WCAG’s guidance, thin decorative fonts might need to be larger and/or bold.</p>

### Testing Color-Contrast Ratio

You should test:

*   early in the design process;
*   when creating a visual design specification for any product or service (this documents all of the color codes and the look and feel of the user experience);
*   all new designs that are not part of an existing visual design guideline.</p>

### Test Hexadecimal Color Codes for Web Designs

Let’s use the <a href="https://webaim.org/resources/contrastchecker">WebAIM Color Contrast Checker</a> to test sample body-text colors on a white background (<code>#FFFFFF</code>):

*   <span style="color: #333333;">dark-gray text (#333333)</span>.
*   <span style="color: #666666;">medium-gray text (#666666)</span>.
*   light-gray text (#999999).

We want to make sure that body and normal text passes the WCAG 2.0 AA. Note that light gray (<code>#999999</code>) does not pass on a white background (<code>#FFFFFF</code>).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04dd8c22-b378-4afc-8641-4952bfe9c924/colorcontrastgrays-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32723229-8e38-4109-b02e-4d1b467ee355/colorcontrastgrays-500px.png" alt="Test dark-gray, medium-gray and light-gray using the WebAim Color Contrast Checker." /></a><figcaption>Test dark-gray, medium-gray and light-gray using the WebAim Color Contrast Checker.(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04dd8c22-b378-4afc-8641-4952bfe9c924/colorcontrastgrays-large.png">View large version</a>)</figcaption></figure>

In the tool, you can modify the light gray (<code>#999999</code>) to find a color that does pass the AA. Select the “Darken” option to slightly change the color until it passes. By clicking the color field, you will have more options, and you can change color and luminosity, as shown in the second part of this example.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d7b057-4cfa-42ad-9582-d2196eeddfa0/modifylightgray-large.png"><img title="Modify colors to pass" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142f0e4f-1de1-4ccf-8fb7-717e74dd2efb/modifylightgray-500px.png" alt="Modify colors to pass" /></a><figcaption>In the WebAim Color Contrast Checker, modify the light gray using the “Darken” option, or use the color palette to find a color that passes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d7b057-4cfa-42ad-9582-d2196eeddfa0/modifylightgray-large.png">View large version</a>)</figcaption></figure>

Tabular information may be designed with alternating white and gray backgrounds to improve readability. Let’s test medium-gray text (<code>#666666</code>) and light-gray text (<code>#757575</code>) on a gray background (<code>#E6E6E6</code>).

Note that with the same background, the medium text passes, but the lighter gray passes only for large text. In this case, use medium gray for body text instead of white or gray backgrounds. Use the lighter gray only for large text, such as headings on white and gray backgrounds.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24b5f43d-8956-4a62-9115-3a5dafd2798b/gray-graybackground-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d2efbac-a94d-4cbb-aef4-10d2ae0040f7/gray-graybackground-500px.png" alt="Color Contrast Checker - Test light-gray and medium-gray text on a gray background." width="1156" height="478" /></a><figcaption>Test light-gray and medium-gray text on a gray background. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24b5f43d-8956-4a62-9115-3a5dafd2798b/gray-graybackground-large.png">View large version</a>)</figcaption></figure>

### Test RGB Color Codes

For mobile applications, designers might use RGB color codes to specify visual designs for engineering. You can use the TPG Colour Contrast Checker. you will need to install either the PC or Mac version and run it side by side with Photoshop.

Let’s use the Colour Contrast Checker to test medium-gray text (<code>102 102 102</code> in RGB and <code>#666666</code> in hexadecimal) and light-gray text (<code>#757575</code> in hexadecimal) on a gray background (<code>230 230 230</code> in RGB and <code>#E6E6E6</code> in hexadecimal).

1.  Open the Colour Contrast Checker application.
2.  Select “Options” → “Displayed Color Values” → “RGB.”
3.  Under “Algorithm,” select “Luminosity.”
4.  Enter the foreground and background colors in RGB: `102 102 102` for foreground and `230 230 230` for background. Mouse click or tab past the fields to view the results. Note that this combination passes for both text and large text (AA).
5.  Select “Show details” to view the hexadecimal color values and information about both AA and AAA requirements.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d13f7e-3914-4d69-b24c-a7b7cc4fe745/ccanalysercolorwheel-large.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4df949cc-dc2f-4f33-a3e1-5b2d1dc3f412/ccanalysercolorwheel-500px.png" alt="Colour Contrast Analyser, and color wheel to modify colors" /></a><figcaption>Colour Contrast Analyser, and color wheel to modify colors. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d13f7e-3914-4d69-b24c-a7b7cc4fe745/ccanalysercolorwheel-large.png">View large version</a>)</figcaption></figure>

In our example, light-gray text (<code>117 117 117</code> in RGB) on a gray background (<code>230 230 230</code> in RGB) does not meet the minimum AA contrast ratio for body text. To modify the colors, view the color wheels by clicking in the “Color” select box to modify the foreground or background. Or you can select “Options” → “Show Color Sliders,” as shown in the example.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12cd6cb6-c90c-48f6-8511-6b8e7c605ec5/ccanalysersliders-500px.png" alt="Colour Contrast Analyser, with RGB codes. Show color sliders to modify any color that does not meet minimum AA guidelines." /><figcaption>Colour Contrast Analyser, with RGB codes. Show color sliders to modify any color that does not meet minimum AA guidelines.</figcaption></figure>

In most cases, minor adjustments to colors will meet the minimum contrast ratio, and comparisons before and after will show how better contrast enables most people to see and read more easily.</p>

## Best Practices

Test for color-contrast ratio, and document the styles and color codes used for all design elements. Create a visual design specification that includes the following:

*   typography for all textual elements, including headings, text links, body text and formatted text;
*   icons and glyphs and text equivalents;
*   form elements, buttons, validation and system error messaging;
*   background color and container styles (making sure text on these backgrounds all pass);
*   the visual treatments for disabled links, form elements and buttons (which do not need to pass a minimum color-contrast ratio).

Documenting visual guidelines for developers brings several benefits:

*   Developers don’t have to guess what the designers want.
*   Designs can be verified against the visual design specification during quality testing cycles, by engineers and designers.
*   A reference point that meets design accessibility guidelines for color contrast can be shared and leveraged by other teams.</p>

## Summary

If you are a designer, try out the simulators and tools on your next design project. Take time to see differently. One of the stellar designers who reviewed my checklist told me a story about using Photoshop’s color-blindness proofs. On his own, he used the proofs to refine the colors used in a design for his company’s product. When the redesigned product was released, his CEO thanked him because it was the first time he was able to see the design. The CEO shared that he was color-blind. In many cases, you may be unaware that your colleague, leader or customers have moderate low-vision or color-vision deficiencies. If meeting the minimum color-contrast ratio for a particular design element is difficult, take the challenge of thinking beyond color. Can you innovate so that most people can pick up and use your application without having to customize it?

If you are responsible for encouraging teams to build more accessible web or mobile experiences, be prepared to use multiple strategies:

*   Use immersive experiences to engage design teams and gain empathy for people who see differently.
*   Show designers how their designs might look using simulators.
*   Test designs that have low contrast, and show how slight modifications to colors can make a difference.
*   Encourage designers to test, and document visual specifications early and often.
*   Incorporate accessible design practices into reusable patterns and templates both in the code and the design.

Priorities and deadlines make it challenging for teams to deliver on all requests from multiple stakeholders. Be patient and persistent, and continue to engage with teams to find strategies to deliver user experiences that are easier to see and use by more people out of the box.</p>

## References

*   “[Contrast (Minimum): Understanding Success Criterion 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)” and [the note](https://www.w3.org/TR/2014/NOTE-UNDERSTANDING-WCAG20-20140311/visual-audio-contrast-contrast.html), Web Content Accessibility Guidelines 2.0, Level AA
*   “[Get a Sneak Peek Into PayPal Accessibility Showcase](https://www.paypal-engineering.com/2014/03/13/get-a-sneak-peek-into-paypal-accessibility-showcase/),” Victor Tsaran and Cathy O’Connor, PayPal Engineering
*   “[Adobe Photoshop](https://www.adobe.com/accessibility/products/photoshop.html)” Accessibility, Adobe
*   “[Soft-Proof for Color Blindness (Photoshop and Illustrator)](https://help.adobe.com/en_US/creativesuite/cs/using/WS3F71DA01-0962-4b2e-B7FD-C956F8659BB3.html#WS473A333A-7F61-4aba-8F67-5553208E349C),” Adobe
*   [Web Accessibility in Mind](https://webaim.org "Web Accessibility in Mind, WebAIM") (WebAIM)
    *   [Web-based Color Contrast Checker](https://webaim.org/resources/contrastchecker/) (web-based)
    *   [Web Accessibility Evaluation Tool](https://wave.webaim.org) (WAVE)
    *   “[Visual Disabilities: Color-Blindness](https://webaim.org/articles/visual/colorblind)”
*   [TPG Colour Contrast Analyser](https://www.paciellogroup.com/resources/contrastAnalyser/) (for Mac and PC), The Paciello Group
*   Color Vision Simulator for [iOS](https://itunes.apple.com/us/app/chromatic-vision-simulator/id389310222?mt=8 "CVSimulator for Apple iOS") and [Android](https://play.google.com/store/apps/details?id=asada0.android.cvsimulator&hl=en "CVSimulator for Android devices"), Kazunori Asada
*   VisionSim for [iOS](https://itunes.apple.com/us/app/visionsim-by-braille-institute/id525114829?mt=8 "VisionSim app forApple iOS devices") and Android, The Braille Institute
*   “[NoCoffee Vision Simulator](https://chrome.google.com/webstore/search/NoCoffee%20Vision%20Simulator?hl=en&gl=US), Aaron Leventhal (also see [Levanthal’s blog post about it](https://accessgarage.wordpress.com/2013/02/09/458/ "About No Coffee Vision Simulator for Chrome"))
*   “[Age-Related Eye Diseases](https://www.nei.nih.gov/catalog/aging-eye-health-infographic),” National Eye Institute
*   “[Disability and Health](https://www.who.int/mediacentre/factsheets/fs352/en/),” World Health Organization
*   “[Presbyopia](https://www.mayoclinic.org/diseases-conditions/presbyopia/basics/causes/con-20032261),” Mayo Clinic
*   “[World Population Ageing: 1950–2050](https://www.un.org/esa/population/publications/worldageing19502050/),” UN Department of Economic and Social Affairs

### Low-Vision Goggles and Resources

*   [Zimmerman Low Vision Simulation Kit](https://www.lowvisionsimulationkit.com)
*   [Low Vision Simulators](https://www.lowvisionsimulators.com/find-the-right-low-vision-simulator), Fork In the Road

{{< signature "hp, al, il, ml" >}}

