---
title: Functional Animation In UX Design
slug: functional-ux-design-animations
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59b366f5-b2a0-483c-82a2-d9761c0092eb/animation.jpg'
date: 2015-05-14T14:59:27.000Z
author: amitdaliot
summary: >-
  This article contains many video examples that show functional animation. Therefore, it may take longer to load on slow connections.
description: >-
  This article contains many video examples that show functional animation. Therefore, it may take longer to load on slow connections.
categories:
  - UX
  - Animation
  - Usability
---
A good UX designer can easily explain the logic behind each decision in a [design concept](https://www.smashingmagazine.com/2015/02/27/design-principles-dominance-focal-points-hierarchy/). This includes the [information architecture](https://www.smashingmagazine.com/2014/10/20/improving-information-architecture-card-sorting-beginners-guide/), the [content hierarchy](https://www.smashingmagazine.com/2015/02/27/design-principles-dominance-focal-points-hierarchy/), the flow and the assumptions made.

Sooner or later, animation will be introduced to the wireframe concept, and then making design decisions or explaining them becomes harder. Reasons such as “It will be cool!” or “It’s trendy” or ”exciting” are exactly the areas where a design starts to lose its strength. Animations deserve a far better ground in our design considerations. We should be justified in defining animations and explaining their purpose — just the same way that we explain all other elements in a design.

## What Is Functional Animation?

Functional animation is subtle animation that we embed in a user interface design as part of our process.

Unlike animation made by Disney Studios or animation made for computer games, functional animation has a clear, logical purpose. Their purpose is to serve a design concept by supporting the solution we are trying to convey. Functional animation is yet another tool in our UX design arsenal.

In a perfect world, we should be able to validate functional animation against a well-defined set of logical purposes. If a certain animation in our design follows a logical purpose, then it is a valid functional animation and its existence in our design is probably justified. But if it fits no purpose, then it might be redundant and need to be reconsidered.

In the past year or so, while working on various projects, I’ve collected a family of nine logical purposes that today help me validate functional animation. I’ve realized that by examining a well-defined animation, I can easily fit it in one or more groups in this family.

It also works the other way around: When an animation doesn’t fit a functional purpose, it usually also feels awkward or annoying. Below are the family groups I have collected so far. I hope you find them useful in validating your own design animation.

{{% feature-panel %}}

## Orientation

Direction illuminates structure. In this group, we find animation that plays a role in our navigation, casting light on the website’s information architecture. The logic behind this type of animation is to maintain the user’s sense of orientation and to help the user comprehend the change that has just happened in the page’s layout, what has triggered the change and how to initiate the change again later on if needed.

A classic example is a button that toggles hidden content. When you click it, a hidden panel appears. And when you close the panel, it shrinks back into the action button.

The first time, a user cannot really predict an interaction that is about to happen. The opening animation of the hidden panel growing in size helps the user stay oriented and not feel that they have left the page or that content has suddenly vanished. They remain in control of everything that is happening. The closing animation helps the user associate the shrinking panel with the action button — so, the next time they will remember how to open the panel again.

**Logical purpose:** Avoid a surprising transition, and orient the user.

### Example Videos

{{< vimeo id="126783555" >}}

{{< vimeo id="126783556" >}}

## Same Location, New Action

A well-known usability rule is to be consistent in both the design and content of a website. A consistent website is predictable and, therefore, learnable. This rule applies to action buttons, among other things.

In certain cases, we are forced to design an action button whose functionality changes under certain conditions. We usually see this in designs where overall space is limited. Thus, a user who has learned the functionality of an action button may need to learn new functionality.

“Save” and ”Edit” buttons are probably the most common example of switchable buttons. But this is an easy case because, while the actions are contradictory, they have the same context. In other situations, when the two actions have no immediately apparent relationship, we face a usability challenge. That’s where functional animation can help.

**Logical purpose:** Emphasize a functional change in an action button.

### Example Videos

{{< vimeo id="127066640" >}}

{{< vimeo id="127066642" >}}

## Zoom In

The third family has some similarities with the orientation group we saw earlier. In these animations, the user selects an item in a list to zoom into its detailed view (which overtakes the list view) and is able to go back to the full list view.

We commonly see this in image galleries, cards and item selectors. A user will select an item and will immediately see the detailed screen that is associated with that selection.

The challenge here is to make sure the user feels they are still in control and remain in the given context. Functional animation is usually a must in this situation.

In examining numerous functional animations in this family group, I’ve noticed a common pattern that, when implemented accurately, enhances the animation’s effectiveness:

1.  The initial state is the original list of items.
2.  Each item is designated with a unique visual cue, such as a dominant color, a symbol, a bold title or a thumbnail image.
3.  When the user makes a selection, a new page is created and the selected visual cue is relocated to a prominent, dominant position. For example, the entire page might be colored with an item’s unique color; the item’s symbol would expand and be positioned in the page’s title; the item’s name would get bigger and appear in the page’s title.
4.  A noticeable action button to dismiss appears in the new page, such as “Cancel,” “Close,” “Back” or “x.”

**Logical purpose:** Associate a thumbnail with its detailed view.

{{% ad-panel-leaderboard %}}

### Example Videos

{{< vimeo id="126783740" >}}

{{< vimeo id="126783743" >}}

## Visual Hint

Visual hints assist users to better understand how to interact with a product’s interface. It is especially needed in designs that contain an unconventional object or a unique navigation method.

This kind of functional animation is easily detected when we open a page and a quick one-time animation is suddenly triggered that demonstrates how certain functionality in the design operates.

**Logical purpose:** Hint to exhibit unconventional functionality or a hidden action.

### Example videos

{{< vimeo id="126783744" caption="Video credit: <a href='https://dribbble.com/shots/1964352-Tasking-App'>Michael Martinho</a>" >}}

{{< vimeo id="126783746" caption="Video credit: <a href='https://www.buildinamsterdam.com/'>www.buildinamsterdam.com</a>" >}}

{{< vimeo id="126783747" caption="Video credit: <a href='https://dribbble.com/shots/1861517-Messages-Animation'>Dejan Markovic</a>" >}}

## Highlight

This family group assists users in those unfortunate situations when there is a need to rise above a noisy layout.

Designers usually strive to avoid noisy layouts, which load the screen with various pieces of textual and visual content that compete with each other for the user’s attention.

One way to minimize noise in an interface is by removing clutter. However, sometimes this task is not so trivial. Consider a news website whose owners want to remove pieces of textual news or images from the home page.

Motion, by its nature, has the highest level of prominence in a user interface. Neither text paragraphs nor static images can compete with motion. We can take advantage of this with this functional animation group. Remember, though, that increasing interface noise by adding an object with a higher level of prominence is a slippery slope.

In the animation sample below, we see that the addition of an item to the shopping cart is not noticeable enough due to the crowded background. So, animation is needed.

**Logical purpose:** Grab the user’s attention, and rise above a noisy layout.

### Example videos

{{< vimeo id="126783964" caption="Video credit: <a href='https://photojojo.com/store/'>www.Photojojo.com</a>" >}}

{{% ad-panel-leaderboard %}}

## Simulation

Sometimes during design analysis and user interviews, we find that users have a need that we can address only with a tailored simulation.

For these special cases, we would create a customized functional animation. In the example below, soccer analytics are presented in a way that figures, numbers, tables and graphs could never compete with. In the second example, the user can monitor temperatures on a map according to time and geography — a particular use case that could hardly be addressed any other way.

**Logical purpose:** Simulate topics that are otherwise hard to convey.

### Example videos

{{< vimeo id="126783965" caption="Video credit: <a href='https://dribbble.com/shots/1410455-Soccer-analytics'>Monterosa</a>" >}}

{{< vimeo id="126783966" >}}

## Visual Feedback

Visual feedback is extremely important in user interface design. In real life, buttons, controls and objects respond to our interaction, and this is how people expect things to work.

But remember that functional animation in this family group needs to be very subtle and should be designed responsively. Button feedback is extensively used in every interface, so using functional animation where it is not really needed will cause more harm than good. On touch devices, functional animation can be most beneficial as a substitute for rollover effects.

**Logical purpose:** Acknowledge the user’s action.

### Example videos

{{< vimeo id="126783967" >}}

{{< vimeo id="126783969" caption="Video credit: <a href='https://www.google.com/design/spec/animation/responsive-interaction.html#responsive-interaction-user-input'>Google material design</a>" >}}

## System Status

This group is all about control. For the user, control means knowing and understanding their current context in the system at any given time.

Functional animation provides real-time monitoring of system status, enabling the user to quickly understand when an action began, the time remaining and exactly when it has ended. Perhaps the very first functional animation that served this role in HTML websites is the spinner GIF, which is still being used in many interfaces to indicate an action in progress.

Effective functional animations in this family group usually follow this pattern:

1.  Show clear feedback to indicate that the process has initiated.
2.  Present ongoing feedback while the process is in progress.
3.  Estimate the completion of the process (a step, by the way, where spinners fail).
4.  Show clear feedback that the process has terminated.

A well-known animation in this group is “pull down to refresh,” which initiates a process of content updates on mobile devices. Examine the implementation of these animations in various applications, and you will soon notice that animations that do not fully comply with the four steps laid out above feel wrong. For example, uncertainty arising from the lack of clear feedback that a process has terminated could prompt the user to initiate the refresh action again.

**Logical purpose:** Impart a sense of control in a linear process.

### Example videos

{{< vimeo id="127066744" >}}

{{< vimeo id="126896464" caption="Video credit: <a href='https://www.yikyakapp.com/'>Yik Yak App</a>" >}}

## Marketing Tool

This group is all about Marketing — and it’s got some fun animations! Whereas the previous eight groups in our family of animations are quite logical, this one is full of emotions!

Suppose we need to indicate a product’s behavior, highlight a particular feature, promote a unique capability or even bundle a brand’s values and style into a product.

In any of these scenarios, an animation might serve the company’s marketing strategy well. The approach might not be clearly user-centered, but it definitely has a functional purpose.

**Logical purpose:** Support a company’s brand values or highlight a product’s strengths.

### Example videos

{{< vimeo id="126896518" caption="Video credit: <a href='https://dribbble.com/shots/1901531-Loading'>Creativedash</a>" >}}

{{< vimeo id="126896520" caption="Video credit: <a href='https://bellroy.com/slim-your-wallet'>www.Bellroy.com</a>" >}}

## Summary

When it comes to providing pleasure or delight in our websites and apps, animations contribute a lot. But always remember that they must be **functional first**.

Aarron Walter of MailChimp writes about the hierarchy of user needs in his book _Designing for Emotion_. It’s similar to Maslow’s hierarchy of needs, but rather than describing our personal needs, Aarron describes our needs as users. Walter’s hierarchy positions the functional need as the base of the pyramid, while the need for pleasure is up on top — and applicable only if the base has been fulfilled. In this article, I’ve dealt only with this functional base, without going into aspects of pleasure and delight, which deserve an article of their own.

So far, I’ve compiled a family of nine rules. These nine rules map well to every animation I’ve encountered so far. They help me to assess animations that I see in interfaces, and they are a strong set of guiding principles in deciding how to add animations to a wireframe design. I hope they serve you in your design process in the same way they serve me.

However, this research is in progress. So, the next time you come across a functional animation, go ahead and test it against one of these nine groups. If it doesn’t neatly fit any of them and the animation has a clear purpose, share it with us, maybe you have found the tenth family of rules!

### <span class="rh">Further reading</span> on Smashing:

*   [SVG and CSS animations with clip-path](https://www.smashingmagazine.com/2015/12/animating-clipped-elements-svg/)
*   [Creating 'hand-drawn' Animations With SVG](https://www.smashingmagazine.com/2015/09/creating-cel-animations-with-svg/)
*   [The new Web Animation API](https://www.smashingmagazine.com/2014/11/the-state-of-animation-2014/)
*   [Practical Animation Techniques](https://www.smashingmagazine.com/2015/06/practical-techniques-on-designing-animation/)
*   [The Math Behind JavaScript Animations](https://www.smashingmagazine.com/2011/10/quick-look-math-animations-javascript/)
*   [Designing Animations In Photoshop](https://www.smashingmagazine.com/2015/06/creating-advanced-animations-in-photoshop/)
*   [Fast Prototyping UI Animations In Keynote](https://www.smashingmagazine.com/2015/08/animating-in-keynote/)

{{< signature "cc, ml, al" >}}
