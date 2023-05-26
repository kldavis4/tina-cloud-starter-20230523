---
title: 'Designing Better Tooltips For Mobile User Interfaces'
slug: designing-tooltips-mobile-user-interfaces
author: eric-olive
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e56444bf-c092-4699-94c2-04e228edda6c/designing-tooltips-mobile-user-interfaces.jpg
date: 2021-02-03T12:00:13.000Z
summary: >-
  Tooltips are powerful design patterns implemented to enhance the design experience by providing additional information precisely when users need it. In this article, we show you how to design tooltips that will amplify your mobile designs and explain where mobile tooltips are most effective.
description: >-
  Tooltips are powerful design patterns implemented to enhance the design experience by providing additional information precisely when users need it. Sometimes, however, tooltips are obtrusive, especially on mobile devices where available space is at a premium.
categories:
  - UI
  - Design
  - Mobile
  - Design Patterns
  - Web Design
  - Best Practices
---

Ideally, mobile designs would be seamless with no need for technical documentation, online help, or tooltips. In reality, even the best designs can benefit from supplemental information. A tooltip provides this **supplemental information** when users tap an icon, image, hyperlink, or other elements in a mobile user interface (UI). For example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df81d1d-71e8-482a-aae1-39580d226144/1-tooltip-solid-and-radial-fill-tooltips.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df81d1d-71e8-482a-aae1-39580d226144/1-tooltip-solid-and-radial-fill-tooltips.jpg" sizes="100vw" width="800" height="129" caption="Concise tooltips explain the purpose of each drawing icon. (Image Source: Sketchbook mobile app, gold arrows added by the author) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df81d1d-71e8-482a-aae1-39580d226144/1-tooltip-solid-and-radial-fill-tooltips.jpg'>Large preview</a>)" alt="Tooltip showing solid fill and radial fill on a mobile drawing app." >}}

By identifying the “Solid Fill” and “Radial Fill” functions, the tooltips shown above make it easy for users to find the drawing function they need. These tooltips appear in the proper context and are not obtrusive. A first-time user can easily understand the meaning of each icon while an experienced user is unlikely to find these tooltips distracting. In short, the designer has balanced the needs of new and seasoned users. The result of this successful balance is a set of tooltips that users will perceive as a **natural extension** of the design experience.

Too often, however, tooltips are an afterthought as shown in the following example of a mobile contrast checker:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b79e90-084d-4315-884e-805c144f4fdd/2-clear-content-but-lengthy-and-poor-placement.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b79e90-084d-4315-884e-805c144f4fdd/2-clear-content-but-lengthy-and-poor-placement.png" sizes="100vw" width="800" height="600" caption="Lengthy tooltip text obscures important information on the screen. (Image source: <a href='https://dribbble.com/shots/12127969-Tooltips-for-Contrast-Checker'>Stark</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87b79e90-084d-4315-884e-805c144f4fdd/2-clear-content-but-lengthy-and-poor-placement.png'>Large preview</a>)" alt="Lengthy tooltip text on a mobile contrast checker." >}}

While the explanation about the contrast checker is clear, the text is too long and covers important information on the screen. The result is a **clunky tooltip** that confuses as much as it elucidates. Avoiding troublesome tooltips requires thought and planning.

{{% feature-panel %}}

## How To Design Effective Tooltips

The key to designing tooltips that fit seamlessly into the overall design is to plan for them early in the design process. Specifically, designing useful tooltips requires:

- **Proper timing**<br />
Paying attention to tooltips and related design techniques during the sketching and early prototyping stages.
- **Proper implementation**<br />
Carefully considering tooltip context, placement, and clarity.

### Timing

Timing refers to when during the design process to consider tooltips. By referring to the widely use [design sprint](https://www.gv.com/sprint/), developed by Jake Knapp, we can identify the right stages in the design process to make decisions about design elements like tooltips.

Knapp’s sprint process consists of mapping out the problem, sketching solutions, choosing one solution, building a prototype, and then testing that prototype. In short, **generate an idea, build it, and test it**. The following image shows Knapp’s five-day design sprint process. I’ve added text to the sketching and prototype days to show *when* designers and developers should start thinking about tooltips.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b569a9c-35dc-4101-901a-97cf930fa10b/3-design-sprint-map.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b569a9c-35dc-4101-901a-97cf930fa10b/3-design-sprint-map.png" sizes="100vw" width="800" height="312" caption="Google Ventures Design Sprint. (Image Source: <a href='https://www.thesprintbook.com/how'>The Sprint Book</a>, gold text added by the author) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b569a9c-35dc-4101-901a-97cf930fa10b/3-design-sprint-map.png'>Large preview</a>)" alt="Sprint map from Google Ventures Design Sprint." >}}

Sketching is the logical place to begin when considering tooltips because potential points of confusion emerge as the layout and preliminary content take shape. Because initial sketches often do not include complete or detailed content, it is not necessary to **identify every possible tooltip** or even to include all designated tooltips at this stage. Rather, the point is to identify parts of the UI where a well-designed tooltip would help users complete the task at hand or more easily understand content.

For example, a tooltip on a field label makes it easier to fill out the form while also reducing data-entry errors. If it’s not yet clear whether a tooltip is necessary, simply include a **callout** with a question as shown in the figure below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b780ef-1c0b-4988-93f6-8e7af1aae25e/4a-tooltip-planning-during-the-sketching-stage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b780ef-1c0b-4988-93f6-8e7af1aae25e/4a-tooltip-planning-during-the-sketching-stage.png" sizes="100vw" width="800" height="420" caption="Sketching stage (Tuesday in Jake Knapp’s Design Sprint) with callout asking if a tooltip might be useful (Author’s drawing). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b780ef-1c0b-4988-93f6-8e7af1aae25e/4a-tooltip-planning-during-the-sketching-stage.png'>Large preview</a>)" alt="rough sketch of a form with a callout pointing to a field where a tooltip might be useful." >}}

The callout shown above serves as a reminder for the team to discuss before building the prototype. In the “CVV” example above, the team might decide that one persona represents users who are unfamiliar with financial terms and abbreviations. For this group, a **CVV tooltip** would likely be useful and could easily be incorporated into the prototype as shown below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8c883b-b726-4f4d-941b-db1742b7b15c/4b-tooltip-planning-during-the-prototype-stage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8c883b-b726-4f4d-941b-db1742b7b15c/4b-tooltip-planning-during-the-prototype-stage.png" sizes="100vw" width="800" height="357" caption="Prototype stage (Thursday in Jake Knapp’s Design Sprint) with information icon and tooltip shown in hover state. (Image source: Author’s drawing) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8c883b-b726-4f4d-941b-db1742b7b15c/4b-tooltip-planning-during-the-prototype-stage.png'>Large preview</a>)" alt="Prototype of a form with a tooltip" >}}

Considering the need for tooltips and other supplemental information early in the design process increases the chance of developing a useful and usable prototype.

{{% ad-panel-leaderboard %}}

### Implementation

The increasing complexity of mobile apps and limited space on mobile devices pose a significant challenge to designing effective tooltips.

Designers can meet this challenge by focusing on:

- **Context**<br />
Check, check, and re-check the context for every tooltip. What might appear obvious to you as the designer could easily confuse a first-time user. The principle of attending to context applies to all aspects of UX and UI design. It’s especially important for tooltips because their necessary brevity will leave users confused if the context is not clear.
- **Placement**<br />
Tooltips should be prominent and easy to find but should not obstruct important information on the screen.
- **Clarity and brevity**<br />
Edit each tooltip for clarity and brevity. As many editors tell their writers: “Cut, cut, and cut some more.” It’s okay to write longer tooltip text in early iterations as long as you remember to keep editing and condensing for clarity.

The tooltip in the following example fulfills these criteria by providing essential information without disrupting the flow in the mobile form.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82fbfb37-2c78-4298-acfc-e61b4c4b1e1d/5-mint-create-account-clear-field-level-tooltip.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82fbfb37-2c78-4298-acfc-e61b4c4b1e1d/5-mint-create-account-clear-field-level-tooltip.png" sizes="100vw" width="800" height="685" caption="The field-level tooltip is well placed and easy to understand. (Image source: Mint mobile app) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82fbfb37-2c78-4298-acfc-e61b4c4b1e1d/5-mint-create-account-clear-field-level-tooltip.png'>Large preview</a>)" alt="Field-level tooltip text in the Mint mobile app." >}}

Because space is limited on mobile devices, clarity, brevity, and placement are essential. The tooltip on the Mint registration screen shown above is well designed. It is clear, concise, and appears directly **below the zip code field** when users tap the information icon.

The Square mobile app shown below provides another example of good tooltip design by helping bi-lingual users select their preferred language.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b6c734e-054c-4f4c-bc86-45cf09fb3419/6-tooltip-english-espanol-square-app-cropped.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b6c734e-054c-4f4c-bc86-45cf09fb3419/6-tooltip-english-espanol-square-app-cropped.jpg" sizes="100vw" width="752" height="456" caption="Tooltip displaying language options for the Square mobile app. (Image source: Square mobile app) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b6c734e-054c-4f4c-bc86-45cf09fb3419/6-tooltip-english-espanol-square-app-cropped.jpg'>Large preview</a>)" alt="Tooltip showing English and Spanish language options on the Square mobile app." >}}

The “English/Español” tooltip shown above is clear, brief, and properly placed. When users tap the flag icon or “English” text, a tooltip appears with the option to select “English” or “Español.”

Well-placed tooltips enhance visual design by providing short, specific explanations when users need them. In the example above, users who are seeking information in other languages know immediately that they can choose between English or Spanish for this website. The language tooltip helps native Spanish speakers who might read English well but feel more comfortable using the Square app in their native language.

Utility is essential but not sufficient. Effective tooltips should be discreet to the point that users barely register their presence. Users only miss tooltips when they aren’t there. This approach to tooltips is an example of **the long-standing view that great design is invisible**. From this perspective, users never notice the design. Instead, they feel engaged and easily complete the task at hand.

The tooltip shown below on the Google Maps app is easy to find yet subtly integrated into the existing design:

- The icon for muting/unmuting appears in **a vertical row** of icons.
- The **placement** of these icons on the right makes them easy to see without obscuring important information on the map.
- The mute/unmute icon follows the **same style and color scheme** as the search icon immediately above.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5a10de-a836-47db-8f38-c4957248e9e2/7-google-maps-tooltip-after-tapping-sound-icon-to-unmute.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5a10de-a836-47db-8f38-c4957248e9e2/7-google-maps-tooltip-after-tapping-sound-icon-to-unmute.png" sizes="100vw" width="800" height="472" caption="Google Maps mobile app: The ‘Unmuted’ tooltip appears when users tap the sound icon to shift from mute to unmute. (Image source: Google maps mobile app, gold arrow, highlight, and bold text added by the author) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df5a10de-a836-47db-8f38-c4957248e9e2/7-google-maps-tooltip-after-tapping-sound-icon-to-unmute.png'>Large preview</a>)" alt="Tooltip explaining the meaning of unmuted on the Google maps mobile app." >}}

This Google map tooltips works because:

- **The context is clear**. The option to toggle on sound (before pulling out of the driveway) is useful because it’s easier and safer to listen to directions while driving than to look at the phone.
- The **placement of the mute/unmute icon** in a group of existing icons makes it easy to see without obscuring important information on the map.
- The one-word tooltip is brief, and **its meaning is clear**.

In contrast, the tooltip shown in the MyZone fitness mobile app below is poorly designed.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0897e432-0524-4d58-a841-9f0487af258f/8a-myzone-metrics.PNG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0897e432-0524-4d58-a841-9f0487af258f/8a-myzone-metrics.PNG" sizes="100vw" width="800" height="489" caption="Tapping ‘175 Max HR’ displays the tooltip shown above right. (Image source: MyZone mobile app, gold highlights added by author) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0897e432-0524-4d58-a841-9f0487af258f/8a-myzone-metrics.PNG'>Large preview</a>)" alt="Tooltip explaining maximum heart rate on the MyZone Fitness mobile app." >}}

While the context is clear, there are problems with the MyZone app tooltip:

- The **placement is clunky** because it obscures important information.
- The tooltip text is **lengthy**, and the explanation of “Max HR” is confusing.

To accommodate this lengthy text and the distracting green bar at the top, the tooltip is unnecessarily large. The result is a tooltip that is not discrete; it does not feel like a natural extension of the design.

Poor placement and confusing explanations are not the only problems users experience with mobile tooltips. A surprisingly **common issue is the redundant tooltip**. The tooltip example below is part of an illustration of cascading style sheets (CSS) smooth animation. The animation works and the illustration itself is clear; the problem is that the tooltip simply repeats the button text.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16b5111-0663-4f3d-a48d-1111614d8cb1/9-redundant-tooltip.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16b5111-0663-4f3d-a48d-1111614d8cb1/9-redundant-tooltip.png" sizes="100vw" width="800" height="287" caption="Redundant tooltip: Tooltip text repeats button label text. (Image source: <a href='https://codepen.io/linux/pen/xrEjaK'>Omar Dsooky</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16b5111-0663-4f3d-a48d-1111614d8cb1/9-redundant-tooltip.png'>Large preview</a>)" alt="Tooltip repeats button label text." >}}

In the article about CSS animation, the illustration shown above is only for demo purposes. Nonetheless, the image would be more useful with a clear and useful tooltip. As used here, the tooltip is not useful.

While redundant tooltips are useless, tooltips that appear in the wrong part of the UI are especially problematic because they distract users from the task at hand.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bca1794-11cf-4873-8453-89e7b1d85890/10-tooltip-in-wrong-place.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bca1794-11cf-4873-8453-89e7b1d85890/10-tooltip-in-wrong-place.png" sizes="100vw" width="800" height="432" caption="Tooltip out of context. (Image source: <a href='https://dribbble.com/shots/14607417-Daily-post'>Danta Griffthy</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bca1794-11cf-4873-8453-89e7b1d85890/10-tooltip-in-wrong-place.png'>Large preview</a>)" alt="Tooltips about grid systems appears in the wrong place." >}}

The screen shown above includes a title in large font with a statement about increasing income. Yet, the tooltip refers to a grid system tip icon that supposedly “boosts the value of your design.” At best, there is a tenuous connection between the tooltip and the main theme on this screen, increasing income. The icon and tooltip might be important, but they are in the **wrong place** in this app.

More broadly, context is a bedrock UX principle and applies to all design elements. For example, an image of a $150,000 sports car on a site or app targeting budget car shoppers would look and feel incongruous because the image would not match the user’s expectations. In short, the image would likely confuse the targeted user group.

**Context is particularly important for tooltips** because the purpose of a tooltip is to clarify and provide additional information. A misplaced tooltip does the opposite; it causes confusion.

{{% ad-panel-leaderboard %}}

## Where To Use Tooltips

Context is also a critical consideration when deciding where to use tooltips. Because tooltips work best when they amplify a well-designed UI, they are particularly effective for:

- Contextual Help,
- Brief instructions,
- New features.

### Contextual Help

Contextual help appears when users are in a specific part of the UI. The following example is from Airbnb. Tapping the icon or “3 reviews” text displays a tooltip with an explanation of reviews and a link that takes users to reviews about the individual shown on screen (the author, in this example).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ff52f64-85ad-42ff-b4f5-8f6638abecdc/11-airbnb-review-icon-with-tooltip-cropped.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ff52f64-85ad-42ff-b4f5-8f6638abecdc/11-airbnb-review-icon-with-tooltip-cropped.png" sizes="100vw" width="800" height="455" caption="Airbnb tooltip explaining the meaning of reviews. (Image source: Airbnb mobile app) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ff52f64-85ad-42ff-b4f5-8f6638abecdc/11-airbnb-review-icon-with-tooltip-cropped.png'>Large preview</a>)" alt="Airbnb review icon with tooltip cropped" >}}

The tooltip shown above is informative because it explains what reviews mean in the Airbnb app and, specifically, in the context of a single profile. In short, contextually specific tooltips appear at the precise moment users need additional information.

### Brief Instructions

Instructional tooltips should also appear when users need more information. The difference is that certain aspects of a mobile app might require an explanation at each step to ensure that users can complete the task at hand. For example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dff8e0-0bee-457c-a141-f13872c10f68/12a-irs-get-my-economic-impact-payment-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dff8e0-0bee-457c-a141-f13872c10f68/12a-irs-get-my-economic-impact-payment-1.png" sizes="100vw" width="800" height="466" caption="Step-by-step tooltip instructions. (Image source: IRS mobile site, gold highlights added by the author) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30dff8e0-0bee-457c-a141-f13872c10f68/12a-irs-get-my-economic-impact-payment-1.png'>Large preview</a>)" alt="Tooltip text guides users through each step of a form." >}}

Each tooltip in this part of the IRS app is paired with a specific task such as entering a social security number, date of birth, or street address. Because each tooltip is context-specific, users can easily learn what they need to do during each step and why the IRS needs this information.

### New Features

As Sofia Quintero explains in [Tooltips: your secret weapon for improving feature discovery](https://uxdesign.cc/tooltips-your-secret-weapon-for-improving-deature-discovery-e1c380562f2e), tooltips are an effective way to draw the user’s attention to new features, “To promote and publicize its new GIFs, Twitter displayed a full-screen message to users before gently directing them on how to incorporate GIFs into their tweets using a traditional tooltip.”

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebeefd0-d3b6-4efb-b2f0-aca831629baf/13-twitter-gif-tooltip.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebeefd0-d3b6-4efb-b2f0-aca831629baf/13-twitter-gif-tooltip.jpeg" sizes="100vw" width="800" height="571" caption="Twitter mobile app with tooltip showing the then new ‘GIF’ feature. (Image source: <a href='https://uxdesign.cc/tooltips-your-secret-weapon-for-improving-deature-discovery-e1c380562f2e'>Tooltips: your secret weapon for improving feature discovery</a>, gold callouts added by the author) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebeefd0-d3b6-4efb-b2f0-aca831629baf/13-twitter-gif-tooltip.jpeg'>Large preview</a>)" alt="Twitter gif tooltip" >}}

The GIF feature was introduced a few years ago, but it holds up as a useful presentation of a new feature. It’s clear and clean, standing out without dominating the UI. New users will see it while experienced users can proceed without distraction because the tooltip is well-integrated into the UI and does not cover up other screen elements.

## Conclusion

Tooltips amplify a mobile UI by providing supplemental information precisely when users need it. Leverage the power of tooltips by considering them when sketching designs and building early prototypes. During implementation, ensure that tooltips will help users by focusing on:

- **Context**<br />
Effective tooltips appear precisely when users need them.
- **Placement**<br />
Tooltips should be prominent and easy to find but should not obstruct important information on the screen.
- **Clarity and brevity**<br />
Review every tooltip in your app to ensure that it makes sense. Edit for brevity.

For tooltips to reinforce a well-designed UI, use them in parts of the UI where they work best such as:

- Contextual Help,
- Brief instructions,
- New features.

Tooltips are a powerful design pattern with a light footprint that enhances mobile designs when used judiciously.

### Additional Resources

- “[Tooltips: Your Secret Weapon For Improving Feature Discovery](https://uxdesign.cc/tooltips-your-secret-weapon-for-improving-deature-discovery-e1c380562f2e),” Sofia Quintero, UX Collective
- “[Why Tooltips Are Terrible And How To Better Design Them](https://www.trychameleon.com/blog/why-tooltips-are-terrible-and-why-you-should-use-them),” Pulkit Agrawal, Chameleon Intelligent Tech.
- “[Tooltips In UI Design](https://uxplanet.org/tooltips-in-ui-design-f63e117aa3d1),” Nick Babich, UX Planet
- “[Tooltip Guidelines](https://www.nngroup.com/articles/tooltip-guidelines/),” Alita Joyce , Nielsen Norman Group

{{< signature "ah, vf, yk, il" >}}
