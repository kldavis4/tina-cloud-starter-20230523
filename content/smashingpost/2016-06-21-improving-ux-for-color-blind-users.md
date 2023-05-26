---
title: 'Accessibility: Improving The UX For Color-Blind Users'
slug: improving-ux-for-color-blind-users
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf3100b7-1a97-40b7-b4d6-c508fbbca75d/combinations-preview-opt.png
date: 2016-06-21T20:59:19.000Z
author: adam-silver
description: >-
  According to Colour Blind Awareness [4.5% of the population are
  color-blind](https://www.colourblindawareness.org/colour-blindness/). If your
  audience is mostly male this increases to 8%. Designing for color-blind people
  can be easily forgotten because most designers _aren't_ color-blind. In this
  article I provide 13 tips to improve the experience for color-blind people –
  something which can often benefit people with normal vision too.

  There are [many
  types](https://www.colourblindawareness.org/colour-blindness/types-of-colour-blindness/)
  of color blindness but it comes down to not seeing color clearly, getting
  colors mixed up, or not being able to differentiate between certain colors.
categories:
  - UX
  - Colors
  - UX
  - Accessibility
---
According to Colour Blind Awareness <a href="https://www.colourblindawareness.org/colour-blindness/">4.5% of the population are color-blind</a>. If your audience is mostly male this increases to 8%. Designing for color-blind people can be easily forgotten because most designers <em>aren't</em> color-blind. In this article I provide 13 tips to improve the experience for color-blind people – something which can often benefit people with normal vision too.</p>

## What Is Color Blindness?

There are <a href="https://www.colourblindawareness.org/colour-blindness/types-of-colour-blindness/">many types</a> of color blindness but it comes down to not seeing color clearly, getting colors mixed up, or not being able to differentiate between certain colors.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [Making Accessibility Simpler, With Ally.js](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/)
*   [<span class="headline">The Underestimated Power Of Color In Mobile App Design</span>](https://www.smashingmagazine.com/2017/01/underestimated-power-color-mobile-app-design/)

{{% feature-panel %}}

These problems can also be exacerbated by the environments in which people use websites. This could include low-quality monitors, bad lighting, screen glare, tiny mobile screens and sitting far away from a huge television screen.

Relying <em>solely</em> on color for readability and affordance makes a website difficult to use, which ultimately affects readership and sales.

While the following tips aren't exhaustive, they do cover the majority of problems color-blind people experience when using websites.</p>

## 1\. Text Readability

To ensure text is readable it should pass accessibility guidelines based on the combination of text color, background color and text size as follows:
<blockquote>“WCAG 2.0 level AA requires a contrast ratio of 4.5:1 for normal text and 3:1 for large text (14 point and bold or larger, or 18 point or larger).”
<cite>— <a href="https://webaim.org/resources/contrastchecker/">WebAim color contrast checker</a></cite></blockquote>

Here are a few examples of color and size combinations that do and do not pass:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/953497cc-9050-4e19-9097-c61d720d94ac/text-contrast-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9381379e-d394-49eb-82b2-bfb0cad5d726/text-contrast-preview-opt.png" alt="Contrast is based on color and size" /></a><figcaption>This illustrates how contrast is based on the combination of color and size. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/953497cc-9050-4e19-9097-c61d720d94ac/text-contrast-large-opt.png">View large version</a>)</figcaption></figure>

## 2\. Text Overlaid On Background Images

Text overlaid on imagery is tricky because some or all of the image may not have sufficient contrast in relation to the text.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bff596ba-f297-4da6-82ce-56f7e2101415/text-overlay-bad-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe4b838-9280-4d04-86e1-218cd19d8a6f/text-overlay-bad-preview-opt.jpg" alt="Description of the image." /></a><figcaption>Text overlaid on an image without a mask. (Image credit: <a href="https://unsplash.com/photos/N_Y88TWmGwA">Jay Wennington</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bff596ba-f297-4da6-82ce-56f7e2101415/text-overlay-bad-large-opt.jpg">View large version</a>)</figcaption></figure>

Reducing the background opacity increases the contrast, making the text easier to read.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f5aff0d-2d00-4a57-9dbd-7a1c91a1fcaa/text-overlay-good-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b5f770-2629-46d7-bee6-10eb337384d8/text-overlay-good-preview-opt.jpg" alt="Description of the image." /></a><figcaption>Text overlaid on an image with a mask. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f5aff0d-2d00-4a57-9dbd-7a1c91a1fcaa/text-overlay-good-large-opt.jpg">View large version</a>)</figcaption></figure>

Alternatively, you can style the text itself to have a solid color or a drop shadow, or anything else that matches your brand guidelines.</p>

## 3\. Color Filters, Pickers And Swatches

The screenshot below shows the <a href="https://www.amazon.co.uk/s/ref=nb_sb_noss?url=search-alias%3Daps&amp;field-keywords=t+shirts">color filter on Amazon</a> as seen by someone with and without protanopia (red–green color blindness). Without descriptive text it is impossible to differentiate between many of the options available.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5c96fe9-f002-4ac8-97a5-819303798fa7/amazon-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aaebaac-2890-4ea4-87dc-dcbcaa59ec7d/amazon-preview-opt.jpg" alt="Amazon color picker" /></a><figcaption>Color filter without labels as seen by someone with protanopia is impossible to use. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5c96fe9-f002-4ac8-97a5-819303798fa7/amazon-large-opt.jpg">View large version</a>)</figcaption></figure>

Amazon shows descriptive text when the user hovers, but hover isn't available on mobile.</p>

<a href="https://www.gap.co.uk/">Gap</a> solves this problem by adding a text label beside each color as shown below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c875bb39-83b4-4a77-ae33-519f49882075/gap-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f435241-5f86-463f-b536-7f154823c417/gap-preview-opt.jpg" alt="Amazon color picker" /></a><figcaption>Color filter with labels as seen by someone with protanopia is easy to use. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c875bb39-83b4-4a77-ae33-519f49882075/gap-large-opt.jpg">View large version</a>)</figcaption></figure>

This happens to be beneficial for people with normal vision too. For example, black and navy are difficult colors to differentiate on screen. A text label takes the guesswork out of it.</p>

## 4\. Photographs Without Useful Descriptions

The screenshot below shows a <a href="https://www.superdry.com/mens/t-shirts/details/55971/pt-classics-vintage-logo-t-shirt">SuperDry T-shirt</a> for sale on its website. It is described as “Leaf Jaspe” which is ambiguous as leaves can come in an assortment of colors (green, yellow, brown. etc.).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e74ed5c2-fb54-4200-bc4f-4a1a0cbb686d/superdry-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43431209-d5c6-4547-b3b3-5a8fec5d46c5/superdry-preview-opt.jpg" alt="Description of the image." /></a><figcaption>It's hard for color-blind people to know what color this SuperDry T-shirt is. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e74ed5c2-fb54-4200-bc4f-4a1a0cbb686d/superdry-large-opt.jpg">View large version</a>)</figcaption></figure>

<em>Jaspe</em> (or rather “jaspé”) means randomly mottled or variegated, so using this in addition to the specific color would be useful: “Gray Green Leaf Jaspe.”

## 5\. Link Recognition

Links should be easy to spot without relying on color. The screenshot below simulates the vision of somebody with achromatopsia (can't see color) viewing the <a href="https://gds.blog.gov.uk/">UK Government Digital Service (GDS) website</a>. Many of the links are hard to see. For example, did you notice that “GDS team, User research” (located under the heading) are links?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/761e145a-554c-4175-b6dc-5bf47b5c541c/gds-screenshot-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ac4862a-2858-463e-8949-9826e3803d91/gds-screenshot-preview-opt.jpg" alt="GDS" /></a><figcaption>GDS blog as seen by someone with achromatopsia. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/761e145a-554c-4175-b6dc-5bf47b5c541c/gds-screenshot-large-opt.jpg">View large version</a>)</figcaption></figure>

To find a link, users are left having to hover with their mouse waiting for the cursor to change to a pointer. On mobile, they are left to tap on text hoping it will make a page request.

The links above with icons are easier to see. For those without, it would be a good idea to add an underline, which is exactly what GDS does within the body of its articles:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b251c9e-7a7b-458a-85b1-d51dcbecec14/gds2-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/520f1a23-c387-4861-9e33-4a74174131eb/gds2-preview-opt.jpg" alt="GDS" /></a><figcaption>Underlined links are easy to see by someone with achromatopsia. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b251c9e-7a7b-458a-85b1-d51dcbecec14/gds2-large-opt.jpg">View large version</a>)</figcaption></figure>

## 6\. Color Combinations

In the physical world you can't always control which colors appear next to one another: a red apple may have dropped and nestled itself into some green grass. However, we <em>can</em> control the colors we use to design our website. The following color combinations should be avoided where possible:

*   green/red
*   green/brown
*   blue/purple
*   green/blue
*   light green/yellow
*   blue/grey
*   green/grey
*   green/black

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c52cb6d8-19a7-4f33-be5e-beba6ddc0c28/combinations-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf3100b7-1a97-40b7-b4d6-c508fbbca75d/combinations-preview-opt.png" alt="Colour combinations as seen with Protanopia" /></a><figcaption>Colour combinations as seen with Protanopia. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c52cb6d8-19a7-4f33-be5e-beba6ddc0c28/combinations-large-opt.png">View large version</a>)</figcaption></figure>

## 7\. Form Placeholders

Using a placeholder <em>without</em> a label is problematic because placeholder text usually lacks sufficient contrast. <a href="https://appleid.apple.com/account">Apple</a> has this problem with their registration form, as shown below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3805e27-cb22-4f08-aa19-d803f5e10d84/apple-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb39cc3a-ce2c-498c-8017-938708cf9594/apple-preview-opt.jpg" alt="Apple registration form" width="350" /></a><figcaption>Apple's registration form uses a placeholder without a label. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3805e27-cb22-4f08-aa19-d803f5e10d84/apple-large-opt.jpg">View large version</a>)</figcaption></figure>

Increasing the contrast is not advisable because it will then be hard to tell the difference between placeholder text and user input.

It's better to use labels – a <a href="https://www.christianheilmann.com/2015/12/04/a-quick-reminder-on-how-and-why-to-use-labels-in-forms-to-make-them-more-accessible/">good practice</a> anyway – with sufficient contrast, which is exactly what <a href="https://www.made.com">Made.com</a> does as shown below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24e48a07-9441-4e1b-8db5-7e785801c5b5/label-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3dd191-7706-43b1-a9ad-be8ed050ec9f/label-preview-opt.jpg" alt="Labels" width="300" /></a><figcaption>Made.com uses labels with good contrast. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24e48a07-9441-4e1b-8db5-7e785801c5b5/label-large-opt.jpg">View large version</a>)</figcaption></figure>

## 8\. Primary Buttons

Often, primary buttons use color alone to present themselves as such, and <a href="https://www.argos.co.uk">Argos</a> does just this on its login screen:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17867c4f-30b7-474a-b52e-8b8f0b7ca2c9/argos-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66e26377-7366-4c73-a82b-a92ba1d767e5/argos-preview-opt.jpg" alt="Argos login screen" /></a><figcaption>The Argos login screen relies on color to emphasize the primary button. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17867c4f-30b7-474a-b52e-8b8f0b7ca2c9/argos-large-opt.jpg">View large version</a>)</figcaption></figure>

Instead, consider using size, placement, boldness, contrast, borders, icons and anything else that will help – within the bounds of your brand guidelines. As an example, <a href="https://kidly.co.uk">Kidly</a> uses size, color and iconography:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba853c3-5141-41f7-9f76-e92d52cdcc29/kidly-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d572dd01-c746-4638-805d-d2aed50c78c3/kidly-preview-opt.jpg" alt="Kidly Basket buttons" /></a><figcaption>Kidly uses size, color and iconography to emphasize the primary button. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba853c3-5141-41f7-9f76-e92d52cdcc29/kidly-large-opt.jpg">View large version</a>)</figcaption></figure>

## 9\. Alert Messaging

Success and error messages are often colored green and red respectively. Most color-blind people don't suffer from achromatism, and so will naturally associate different colors with different messages. However, using prefix text such as "Success" or, my preference, an icon makes it quick and easy to read as shown below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5771c905-89f9-4809-832d-f659d93b627b/messaging-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8722ee5d-206d-4d1a-ade0-70dfc710e773/messaging-preview-opt.jpg" alt="Messaging with icons and text" /></a><figcaption>Alert messaging with text prefixes and icons. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5771c905-89f9-4809-832d-f659d93b627b/messaging-large-opt.jpg">View large version</a>)</figcaption></figure>

## 10\. Required Form Fields

Denoting required fields with color is a problem because some people may not be able to see the differences.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29cf1183-eb8a-4960-8056-30819b5786ca/required-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e58f768-4612-4a1a-ad46-73a783af7369/required-preview-opt.jpg" alt="Messaging with icons and text" /></a><figcaption>Denoting required fields by color. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5771c905-89f9-4809-832d-f659d93b627b/messaging-large-opt.jpg">View large version</a>)</figcaption></figure>

Instead, you could consider:

*   Marking required fields with an asterisk.
*   Even better, marking required fields with “required.”
*   Where possible, remove optional fields altogether.</p>

## 11\. Graphs

Color is often used to signify different segments of a graph. The image below demonstrates how people with different vision would see this. The color-blind-friendly graph is on the right.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f75f08d4-3827-4e19-b282-3a7ccd923564/graphs-normal-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f321b3d-81c1-41b8-8d87-c74355a69878/graphs-normal-preview-opt.png" alt="Graphs as seen with normal visions" /></a><figcaption>Graphs viewed with normal vision (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f75f08d4-3827-4e19-b282-3a7ccd923564/graphs-normal-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbd1cae-ec9a-4618-9481-33c46ca48d6e/graphs-protan-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66ce2cd1-3389-414f-a9d9-90b69c00605c/graphs-protan-preview-opt.png" alt="Graphs as seen with Protanopia" /></a><figcaption>Graphs viewed with protanopia (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbd1cae-ec9a-4618-9481-33c46ca48d6e/graphs-protan-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a2f5504-5dd9-41eb-a32a-f28f4841f013/graphs-achrom-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6793b5f5-8d31-4dca-8780-a5b760835616/graphs-achrom-preview-opt.png" alt="Graphs as seen with normal visions" /></a><figcaption>Graphs viewed with achromatopsia (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a2f5504-5dd9-41eb-a32a-f28f4841f013/graphs-achrom-large-opt.png">View large version</a>)</figcaption></figure>

Using patterns and, where possible, placing text within each segment makes graphs easy to understand. When text doesn't fit – as is often the case with a small pie chart segment – using a key will suffice.</p>

## 12\. Zoom

One accessibility feature that browsers have, is enabling someone to zoom in as much as they need. This improves readability--which is especially helpful on a mobile device.

Unfortunately, zoom can be disabled using the <a href="https://developer.mozilla.org/en/docs/Mozilla/Mobile/Viewport_meta_tag">Viewport Meta Tag</a>, which is problematic. For example, text size may be too small to read in relation to the color contrast—but zooming in effectively increases the font size, making it easier to read. So don't disable zoom on your website.</p>

## 13\. Relative Font Size

Similarly to the previous point, browsers provide the ability to increase text size (instead of zooming the entire page as a whole), in order to improve readability. However, some browsers disable this functionality when the font-size is specified in absolute units such as pixels. Using a relative font size unit, such as ems, ensures that all browsers afford this capability.</p>

## Tooling

There are lots of tools available to help you design for color-blind people:

1.  [Check My Colours](https://www.checkmycolours.com/): if you have an existing website, you can just enter a URL and receive feedback of what needs to be improved.
2.  [WebAim's color contrast checker](https://webaim.org/resources/contrastchecker/): provide two colors to see if they pass accessibility guidelines.
3.  [I Want To See Like The Color Blind](https://chrome.google.com/webstore/detail/i-want-to-see-like-the-o/jebeedfnielkcjlcokhiobodkjjpbjia?hl=en-GB): apply color blindness filters to your web page right within Chrome.
4.  [Color Oracle](https://colororacle.org/): a color blindness simulator for Windows, Mac and Linux, showing you what people with common color vision impairments will see.</p>

## Conclusion

The tips in this article are not exhaustive, and they are not necessarily applicable to every situation. However, they do cover the majority of problems color-blind people experience when using websites.

It's more important to take away the principles, so that you can integrate them into your own design process. Ultimately, websites aren't just meant to look good – they are meant to be easy to use for everyone, including people who are color-blind.

{{< signature "cc, og, il" >}}

