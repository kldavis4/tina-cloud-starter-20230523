---
title: 'Claymorphism: Will It Stick Around?'
slug: claymorphism-css-ui-design-trend
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6ceacdf-835e-497e-a1e0-be958d42ac76/claymorphism-css-ui-design-trend.jpg
date: 2022-03-16T11:00:00.000Z
summary: >-
  This fresh new design trend has been picking up steam with the rising popularity of colorful inflated 3D graphics in web illustrations and with the latest Virtual Reality projects like “Horizon Worlds”. Let’s see if there is room for Claymorphism on the UI, and how we can create this effect with CSS.
description: >-
  This fresh new design trend has been picking up steam with the rising popularity of colorful inflated 3D graphics in web illustrations and with the latest Virtual Reality projects like “Horizon Worlds”. Let’s see if there is room for Claymorphism on the UI, and how we can create this effect with CSS.
categories:
  - UI
  - CSS
  - Techniques
---

Design trends come and go, and just a fraction sticks around longer than others. Flat design and its more popular successor, Material design, have been dominating the web UI for quite some time, featuring a minimalistic aesthetic that eliminates visual clutter and favors user experience.

This approach is very utilitarian at its core as it eliminates most decorative elements and features, leaving room only for subtle shadows and gradients to achieve some visual depth and add a floating effect for elements that should sit on top of others. Visual hierarchy is usually achieved by using color and typography to make the specific elements more prominent.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae9a163c-e6e6-4f25-afc6-b7f2e403c062/1-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae9a163c-e6e6-4f25-afc6-b7f2e403c062/1-claymorphism-new-design-trend.png" width="800" height="510" sizes="100vw" caption="Flat design uses colors to establish visual hierarchy and to draw user attention. Although minimalistic by nature, this design approach relies on colors, layout, and typography to represent the brand and make it stand out. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae9a163c-e6e6-4f25-afc6-b7f2e403c062/1-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Harry’s website with its products" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06ae4e6b-ec13-4808-a30c-0087d55abec1/2-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06ae4e6b-ec13-4808-a30c-0087d55abec1/2-claymorphism-new-design-trend.png" width="800" height="410" sizes="100vw" caption="Smashing Magazine features a Flat design, and it makes use of subtle shadows to achieve depth and make these cards more prominent. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06ae4e6b-ec13-4808-a30c-0087d55abec1/2-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Smashing Magazine website" >}}

## Skeuomorphism And Flat Design

In the early days of personal computers, the learning curve had to be as soft as possible, so users could easily find their way around the new digital space. This was achieved with **Skeuomorphism** which relies on real-world aesthetics to make the UI intuitive and familiar. For example, delete functionality was represented by a realistic-looking trash can icon. 

Skeuomorphism was used similarly in the early days of smartphones in the mid-2000s to easily onboard new users. On Apple’s iPhone OS 1, the YouTube app icon is a television instead of the iconic logo we know today! By leveraging this link between the real world and digital world in form of Skeuomorphism, these new devices managed to garner a wide audience right away.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/432d7ad7-c895-46dd-afbd-43958f6df7d3/3-claymorphism-new-design-trend.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/432d7ad7-c895-46dd-afbd-43958f6df7d3/3-claymorphism-new-design-trend.jpeg" width="800" height="485" sizes="100vw" caption="iPhone OS 1 using Skeuomorphism for app icons. Notice the YouTube app icon in the second row. (Image by <a href='http://www.deccanchronicle.com/technology/310316/iphone-2g-to-iphone-se-interesting-facts-about-the-devices.html?gImgId=258309#s'>Deccan Chronicle</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/432d7ad7-c895-46dd-afbd-43958f6df7d3/3-claymorphism-new-design-trend.jpeg'>Large preview</a>)" alt="A picture of iPhone’s display" >}}

Regardless of the success that Skeuomorphism achieved on these devices, it didn’t find its place on the web. Realistic and elaborate UI elements weren’t a good fit for websites that thrived on simplicity, clean layout, and straightforward usability. Additionally, as responsive web design grew in popularity and mobile performance became a concern, the visually rich and detailed graphics were being slowly phased out. 

As a result, minimalistic **Flat design** and its successor, **Material design**, took the web design scene by storm by providing a highly customizable, performant, and easy-to-implement aesthetic that can easily adapt to virtually any screen size and resolution. Even Apple moved away from Skeuomorphism around 2013 and fully embraced the widely-popular Flat design.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/056949d8-eee2-4020-8001-59cf9790dcc0/4-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/056949d8-eee2-4020-8001-59cf9790dcc0/4-claymorphism-new-design-trend.png" width="800" height="529" sizes="100vw" caption="Skeuomorphism UI on a website. It looks visually impressive and highly detailed, but it severely limits usability and performance. (This website doesn’t exist anymore and can be viewed on <a href='https://web.archive.org/web/20190529021922/http://www.cheeseandburger.com/bigben'>WaybackMachine</a>). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/056949d8-eee2-4020-8001-59cf9790dcc0/4-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Cheese and Burger Society’s website" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b32eb33f-6282-4687-abaa-7094fe75ea3a/5-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b32eb33f-6282-4687-abaa-7094fe75ea3a/5-claymorphism-new-design-trend.png" width="800" height="516" sizes="100vw" caption="Compared to the previous example, this Flat design example lacks visual impact, but it is more effective, responsive, easier to parse and use, and more performant. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b32eb33f-6282-4687-abaa-7094fe75ea3a/5-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Smashburger’s website" >}}

## Neumorphism

The dream of a more tactile-looking 3D web UI lived on, and it resurfaced in 2020 as **Neumorphism.** It draws inspiration from both Skeuomorphism and Flat design, and it takes a different approach to soft 3D UI instead of trying to mimic realistic graphics. Instead of making UI elements float above the background like in Material UI, it makes them extrude from the background. 

This is achieved by using a light and a dark shadow, and a background color that needs to be the same as the color of the element behind it. Optionally, gradients with darker and lighter background colors can be used to create a convex or concave surface, but I haven’t seen it used on web UI as much as a more simple flat surface.

{{< codepen height="480" theme_id="light" slug_hash="jOagGJv" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Neumorphic Variations [forked]](https://codepen.io/smashingmag/pen/jOagGJv) by <a href="https://codepen.io/geoffgraham">Geoff Graham</a>.{{< /codepen >}} 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f96b831-da43-45a3-bcdd-afe4a49a7388/6-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f96b831-da43-45a3-bcdd-afe4a49a7388/6-claymorphism-new-design-trend.png" width="800" height="600" sizes="100vw" caption="Neumorphism is a fresh new approach to UI, but something doesn’t look right. Everything, including cards and other non-interactable elements, looks like a button. (<a href='https://dribbble.com/shots/9158186-Bank-App-Neomorphism-New-Skeuomorphism'>Bank App - Neomorphism New Skeuomorphism</a> by Mathis Freudenberger) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f96b831-da43-45a3-bcdd-afe4a49a7388/6-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Design of a bank app" >}}

Despite this fresh new take, Neumorphism came with considerable drawbacks. The severe background color limitation made it difficult to achieve visual hierarchy and draw user attention using color. Website branding couldn’t be featured more prominently, and customization was severely limited as a result of that limitation. 

I’ve talked about Neumorphism during its early days, and I’ve concluded that [flat UI was still significantly better](https://css-tricks.com/neumorphism-and-css/#aa-neumorphism-in-practice) and more effective at creating usable and prominent call-to-action elements. As a result of that, Neumorphism got visually boring and old pretty quickly, as it was difficult to create a distinct visual style due to these limitations.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c5e820-10eb-4a0e-a143-d5f3a5c6dd3c/7-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c5e820-10eb-4a0e-a143-d5f3a5c6dd3c/7-claymorphism-new-design-trend.png" width="800" height="600" sizes="100vw" caption="Although it’s visually interesting and fresh, this florist app example doesn’t look very distinct from the previous banking app example. And again, everything looks like a button! (<a href='https://dribbble.com/shots/9828470-Florist-App'>Florist App</a> by Darya Popkova) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c5e820-10eb-4a0e-a143-d5f3a5c6dd3c/7-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Design of a florist app" >}}

Neumorphism also has serious accessibility flaws. The poor contrast made the UI unusable for users with poor vision or color blindness, and it’s difficult to perceive visual hierarchy if the effect is overused. In the end, Neumorphism could only serve as an addition to Flat design. More specifically, a different take on achieving depth for non-interactable elements like cards and containers.

{{% feature-panel %}}

## 2D And 3D Illustrations On The Web

Over the past several years, digital illustrations have become increasingly popular, and we saw them used in many different styles like hand-drawn, isometric, abstract, and others. Some major brands and companies even started including [illustrations in their style guidelines](https://www.twilio.com/brand/elements/illustration-guidelines), making them a core part of their design identity.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c77f39b-cbeb-431e-b52a-f7ba00fd3b9c/8-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c77f39b-cbeb-431e-b52a-f7ba00fd3b9c/8-claymorphism-new-design-trend.png" width="800" height="360" sizes="100vw" caption="Mailchimp uses 2D digital illustrations extensively in their branding and marketing. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c77f39b-cbeb-431e-b52a-f7ba00fd3b9c/8-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Mailchimp’s website" >}}

With the advent of web-focused 3D design tools like [Spline](https://spline.design/), web designers would start exploring the world of 3D illustrations. One of the results from this experiment stood out above the rest &mdash; the soft and inflated 3D style. The result was astonishing &mdash; when combined with Flat design or Material design, these colorful soft 3D illustrations would inject a fresh, energetic, and playful new look into the UI.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a7b09a-a05c-4ef7-a13a-037877f7ba9a/9-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a7b09a-a05c-4ef7-a13a-037877f7ba9a/9-claymorphism-new-design-trend.png" width="800" height="499" sizes="100vw" caption="<a href='https://matterapp.com/'>Matter app</a> uses playful and colorful soft 3D image assets alongside the Flat design in UI elements like buttons and cards. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a7b09a-a05c-4ef7-a13a-037877f7ba9a/9-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Matter’s app" >}}

Many soft 3D design sets like [Humans 3.0](https://humans.wannathis.one/), [3D hands](https://icons8.com/l/3d-hands/), [3DIcons](https://3dicons.co/), [Homies](https://homies.craftwork.design/), and others were picking up steam as this fresh 3D direction was making rounds around the Internet. Some [design agencies even started specializing](https://dribbble.com/Vitality_Studio) in web 3D illustrations and pushed the limits of this design direction. More recently, projects like Meta’s [“Horizon Worlds”](https://www.oculus.com/horizon-worlds/) have fully embraced this soft and colorful 3D look to create a vibrant and delightful VR experience.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d97bcf0-d98c-4d3c-8059-539a50d6584d/10-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d97bcf0-d98c-4d3c-8059-539a50d6584d/10-claymorphism-new-design-trend.png" width="800" height="399" sizes="100vw" caption="Meta’s ‘Horizon Worlds’ made colorful soft 3D a core part of their design direction for both the app and website illustrations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d97bcf0-d98c-4d3c-8059-539a50d6584d/10-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Meta’s ‘Horizon Worlds’ design" >}}

{{% ad-panel-leaderboard %}}

## Claymorphism

It was inevitable that this trend will start spilling into the UI itself. This is where the idea of **Claymorphism** was born.

**What’s with all the “morphisms”, anyway?** This suffix seems to be a pet peeve for some, and they think that it shouldn’t just be slapped on every new art direction. We won’t concern ourselves too much with naming at the moment, and we’ll focus on exploring this design trend and its potential. With all that in mind, this term was coined by [Michal Malewicz](https://hype4.academy/articles/design/claymorphism-in-user-interfaces), who was also behind the Neumorphism trend a few years before.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b617c0e-e1b6-46e3-af45-d429f2ecd8c8/11-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b617c0e-e1b6-46e3-af45-d429f2ecd8c8/11-claymorphism-new-design-trend.png" width="800" height="600" sizes="100vw" caption="<a href='https://dribbble.com/shots/17325605-Task-Management-Mobile-App-Claymorphism-UI'>Task Management Mobile App / Claymorphism UI</a> by Vitalii Zhy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b617c0e-e1b6-46e3-af45-d429f2ecd8c8/11-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Task Management Mobile App" >}}

Claymorphism builds on top of Neumorphism foundations. Although both use rounded corners, they differ in how they use backgrounds and shadow. Instead of using light and dark outer shadow to achieve the extrusion effect, Claymorphism uses two inner shadows (dark and light) and an outer (usually darker) shadow to achieve a soft 3D and floating effect. This allows for Claymorphism to have any background color, independent of the background which was a major drawback with Neumorphism.

On a quick personal note &mdash; I adore this style. It’s charming, delightful, and vibrant without being overwhelming when used correctly. It also reminds me of one of my favorite cartoon series from my childhood &mdash; [Wallace and Gromit](https://wallaceandgromit.com/) by [Aardman](https://www.aardman.com/). After working with Flat design for years, it’s refreshing to experiment and play around with different design styles for a change. If you are a designer or a developer, and also like this trend and think it has potential, give it a try and see what you can come up with!

{{< youtube id="36GfaI0_B8E" breakout="true" >}}

One of the major points of criticism is that overusing Claymorphism and going overboard with colors and typography can give off a somewhat childish feel to the UI. Michał Malewicz [acknowledged this drawback](https://hype4.academy/articles/design/claymorphism-in-user-interfaces) and gives a few suggestions on how to avoid that.

<blockquote>“The friendliness of those shapes, along with the 3d imagery creates a slightly child-like interface. To counter it, it’s good to use minimal typography, strong accent colors good contrast.”<br /><br />&mdash; Michał Malewicz</blockquote>

The best use-case scenario for this design trend is, in a similar vein as Neumorphism, as an enhancement to the Flat design, but with a wider use-case than the more restrictive Neumorphism style.

### Potential Use-cases

#### More Prominent Call To Action Elements

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0db5706-db96-4652-b927-ce66dd6b7ccc/12-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0db5706-db96-4652-b927-ce66dd6b7ccc/12-claymorphism-new-design-trend.png" width="800" height="507" sizes="100vw" caption="<a href='https://www.figma.com/community/file/1066455834796929496'>Claymorphism UI</a> by Meng To. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0db5706-db96-4652-b927-ce66dd6b7ccc/12-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Claymorphism UI" >}}

{{< codepen height="480" theme_id="light" slug_hash="zYPgRyg" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Flat button &amp; Claymorphism button comparison [forked]](https://codepen.io/smashingmag/pen/zYPgRyg) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}  

#### Select Elements And Toggle Elements

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f593870-d4a2-4158-9568-26c5445c1842/13-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f593870-d4a2-4158-9568-26c5445c1842/13-claymorphism-new-design-trend.png" width="800" height="600" sizes="100vw" caption="<a href='https://dribbble.com/shots/17313123-Mobile-Banking-App'>Mobile Banking App</a> by Rezha Aaron. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f593870-d4a2-4158-9568-26c5445c1842/13-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Mobile Banking App" >}}

#### Charts

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/574d51ae-3455-437f-adaf-8cbe7591fbaa/14-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/574d51ae-3455-437f-adaf-8cbe7591fbaa/14-claymorphism-new-design-trend.png" width="800" height="453" sizes="100vw" caption="<a href='https://aimchess.site/'>Aimchess</a> uses soft 3D for both illustrations and interactive charts. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/574d51ae-3455-437f-adaf-8cbe7591fbaa/14-claymorphism-new-design-trend.png'>Large preview</a>)" alt="A screenshot from Aimchess' website" >}}

#### Cards And Containers

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bb647a2-bf2d-472d-a01d-db999a98d54f/15-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bb647a2-bf2d-472d-a01d-db999a98d54f/15-claymorphism-new-design-trend.png" width="800" height="600" sizes="100vw" caption="<a href='https://dribbble.com/shots/17468615-App-Shot-Online-Beverage-Store'>App Shot | Online Beverage Store</a> by Rushabh Khasnis. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bb647a2-bf2d-472d-a01d-db999a98d54f/15-claymorphism-new-design-trend.png'>Large preview</a>)" alt="App Shot | Online Beverage Store" >}}

### Claymorphism Effect In CSS

Let’s dive into the individual Claymorphism design features and see how we can achieve a similar effect with CSS:

- **Background**  
We’ll use `background` or `background-color`;
- **Rounded corners**  
We can use `border-radius`;
- **Shadows**  
We’ll use `box-shadow` with 3 values,
    - 2 inset shadows
    - 1 outset shadow;
- **Inflated effect**  
It cannot be easily achieved with CSS, so we’ll avoid this, as it’s not crucial.

Our CSS will look something like this. Of course, these values can be changed to fit the design and element dimensions.

<div class="break-out">

<pre><code class="language-css">.box {
  background: rgb(249, 174, 1);
  border-radius: 48px;
  box-shadow: 
    8px 8px 16px 0 rgba(0, 0, 0, .25), /&#42; Outset shadow &#42;/
    inset -8px -8px 12px 0 rgba(0, 0, 0, .25), /&#42; Dark inset shadow &#42;/
    inset 8px 8px 12px 0 rgba(255, 255, 255, 0.4); /&#42; Light inset shadow &#42;/
}</code></pre>
</div>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61f5079c-771d-4d91-9b84-dc194dd5ecc6/16-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61f5079c-771d-4d91-9b84-dc194dd5ecc6/16-claymorphism-new-design-trend.png" width="800" height="316" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61f5079c-771d-4d91-9b84-dc194dd5ecc6/16-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Illustration of the claymorphism effect in CSS" >}}

Repeating these three rules for multiple elements can become tedious and bloat the codebase, so let’s simplify this set of CSS rules by creating a [utility CSS class](https://frontstuff.io/in-defense-of-utility-first-css) and allowing for customization without resorting to increasing specificity or using complex overrides.

<div class="break-out">

<pre><code class="language-javascript">.clay {
  background: var(--clay-background, rgba(0, 0, 0, 0.005));
  border-radius: var(--clay-border-radius, 32px);
  box-shadow: 
    var(--clay-shadow-outset, 8px 8px 16px 0 rgba(0, 0, 0, 0.25)),
    inset var(--clay-shadow-inset-primary, -8px -8px 12px 0 rgba(0, 0, 0, 0.25)),
    inset var(--clay-shadow-inset-secondary, 8px 8px 12px 0 rgba(255, 255, 255, 0.4));
}</code></pre>
</div>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f49a1d03-ba15-40a0-9d0e-dff09e753116/17-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f49a1d03-ba15-40a0-9d0e-dff09e753116/17-claymorphism-new-design-trend.png" width="800" height="501" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f49a1d03-ba15-40a0-9d0e-dff09e753116/17-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Illustration of the claymorphism effect in CSS" >}}

With this handy utility micro-class, we can easily apply Claymorphism styles, customize them, and extend them without bloating the markup with repeated style snippets.

<pre><code class="language-css">&lt;button class="clay button button--cta"&gt;Add to cart&lt;/button&gt;</code></pre>

<pre><code class="language-css">.button {
  /&#42; Customize Claymorphism styles &#42;/
  --clay-border-radius: 1rem;

  /&#42; Extend base styles &#42;/
  padding: 1.5rem 3rem;
  color: #f5f5f5;
}

.button--cta {
  /&#42; Customize Claymorphism styles &#42;/
  --clay-background: hsl(360, 100%, 27%);


.button--cta:hover,
.button--cta:active {
  /&#42; Customize Claymorphism styles &#42;/
  --clay-background: hsl(360, 100%, 20%);
}}</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87c9fe01-b667-4e3b-a517-57ee0ac10e3d/18-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87c9fe01-b667-4e3b-a517-57ee0ac10e3d/18-claymorphism-new-design-trend.png" width="800" height="168" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87c9fe01-b667-4e3b-a517-57ee0ac10e3d/18-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Illustration of the claymorphism effect in CSS" >}}

I’ve created [`clay.css`](https://github.com/codeAdrian/clay.css/) as an easy way to include this fully customizable micro CSS class in your projects either via CDN link or [NPM package](https://www.npmjs.com/package/claymorphism-css).

<pre><code class="language-bash">&lt;link
  rel="stylesheet"
  href="https://unpkg.com/claymorphism-css/dist/clay.css"
/&gt;</code></pre>

<pre><code class="language-bash">npm i claymorphism-css
yarn add claymorphism-css</code></pre>

Alternatively, you can use it as a SASS mixin and easily apply this effect to pseudo-elements or any other element.

<pre><code class="language-css">@import "claymorphism-css/dist/clay.scss";

@import @include clay(
  $background: [value],
  $border-radius: [value],
  $shadow-outset: [value],
  $shadow-inset-primary: [value],
  $shadow-inset-secondary: [value]
);</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2e0c74d-78f9-42c6-b332-b65ee1b33714/19-claymorphism-new-design-trend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2e0c74d-78f9-42c6-b332-b65ee1b33714/19-claymorphism-new-design-trend.png" width="800" height="420" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2e0c74d-78f9-42c6-b332-b65ee1b33714/19-claymorphism-new-design-trend.png'>Large preview</a>)" alt="Illustration of clay.css" >}}

### Claymorphism And Accessibility

Although Claymorphism doesn’t introduce glaring accessibility issues out-of-the-box as Neumorphism does, it’s important to keep the [standard best practices](https://www.nngroup.com/articles/flat-design/) in mind.

Keep a clear and logical visual hierarchy. Depending on the use case, Claymorphism makes elements more prominent with the soft 3D effect, so we need to be careful not to disrupt visual hierarchy in the process.

Color is an important part of the Claymorphism design style. We need to be careful with contrast and color combinations, so we are able to provide [the best possible user experience](https://www.smashingmagazine.com/2017/10/nailing-accessibility-design/) for people with less contrast sensitivity and for people with color blindness.

Additionally, Claymorphism’s floating effect allows for motion animations and transitions. For example, clicking a button can be animated with scale transformation to achieve the effect of a 3D button being pushed. We should always respect [user motion preferences](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/) to either prevent overwhelming animations from running or provide a safer alternative.

{{% ad-panel-leaderboard %}}

## Conclusion

Flat and Material design has dominated the web UI landscape since the early days of responsive design, and with a good reason &mdash; it is easy to implement, flexible, robust, and easy to make responsive.

Although new design trends like Neumorphism picked up steam initially as a refreshing new alternative to the flat and Material designs, it fell short due to accessibility issues and design constraints.

With the rising popularity of 2D and soft 3D illustrations and in VR projects like Meta’s “Horizon Worlds”, Claymorphism was created as a result. It offers more flexibility in customization, and it doesn’t suffer from the issues that prevented Neumorphism from taking off. However, we will see if this design trend persists and picks up steam. We can already see some examples of soft 3D used on charts and buttons, and it is backed up by the already popular soft 3D illustration trend.

I want Claymorphism to stick around and become an enhancement or even a great alternative to the run-of-the-mill Flat design and Material Design. I hope designers and developers pick up on it and create amazing work. Let’s make the Web a bit more vibrant and fun!

What are your thoughts on Claymorphism as an emerging design trend? How would you use it in your design or dev work? Happy to hear your thoughts!

### References

- “[Claymorphism In User Interfaces](https://hype4.academy/articles/design/claymorphism-in-user-interfaces),” Michał Malewicz
- “[Neumorphism In User Interfaces](https://uxdesign.cc/neumorphism-in-user-interfaces-b47cef3bf3a6),” Michał Malewicz
- “[How To Create Claymorphism Using CS](https://hype4.academy/articles/coding/how-to-create-claymorphism-using-css),” Albert Walicki

{{< signature "vf, yk, il" >}}
