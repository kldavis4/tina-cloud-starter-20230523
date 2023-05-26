---
title: 'An Introduction To Figma Interactive Components'
slug: introduction-figma-interactive-components
author: emiliano-cicero
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a8390d0-26c0-4476-bc00-19e8c89b60c5/introduction-figma-interactive-components.jpg
date: 2021-07-07T11:00:00.000Z
summary: >-
  In this article, Emiliano explains why Figma Interactive Components (now in beta) will improve how we create prototypes. The new feature reduces the time and effort needed to create interactions by bringing down the cost of design exploration. There’s no need for previous Figma knowledge and experience &mdash; all you’ll need is a free Figma account if you’d like to try it out for yourself.
description: >-
  Interactive Components in Figma allows designers to create a component with states (hover, active, clicked, focus) and make it interactive so that every copy of the component will inherit those same interactions by default. Let’s explore how it can reduce the time and effort needed to create interactions for your mock-ups.
categories:
  - Design
  - Figma
  - Tools
  - Workflow
---

Recently, Figma rolled out the beta for the newest interactive components feature that allows defining interactions and animations directly into the variants and propagates them to every component instance. This means that it is now possible to create a component with states (hover, active, clicked, focus) and make it interactive so that every copy of the component will inherit those same interactions by default, helping a lot in the prototyping phase. 

Here’s a comparison example of how the workflow will change:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba82d49-8dd6-4949-91eb-6e15f15a824d/28-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba82d49-8dd6-4949-91eb-6e15f15a824d/28-introduction-figma-interactive-components.png" width="800" height="339" sizes="100vw" caption="Four screens and eight different interactions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba82d49-8dd6-4949-91eb-6e15f15a824d/28-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Four devices connected with eight arrows showing that eight different interactions were needed to create a simple off and on effect." >}}

As you can see in the example above, it requires four screens and eight interactions to make the prototype work as a real product. And if I wanted to use three switches, I would have to add even more screens and interactions.

In the next example, it only requires one screen and one component with two variants for the interactions, and the switch is the same so it can be duplicated as many times as needed:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72d2bd25-8cb7-429c-9ccf-c4bbb54812ae/24-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72d2bd25-8cb7-429c-9ccf-c4bbb54812ae/24-introduction-figma-interactive-components.png" width="800" height="450" sizes="100vw" caption="One single interactive component used twice inside a screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72d2bd25-8cb7-429c-9ccf-c4bbb54812ae/24-introduction-figma-interactive-components.png'>Large preview</a>)" alt="There’s an iPhone at the left and a group of two variants at the right, the variants are connected with two arrows to show that only one component is needed to reproduce the same off and on effect as before." >}}

Using Interactive Components simplifies not only the final prototype but also the *logic* behind it, making it easier to learn how to build, maintain and update the prototypes.

Now, before we start:

### Interactive Components (Beta Access)

You need to [**sign up**](https://docs.google.com/forms/d/e/1FAIpQLSctELo9clvK0uP-0zDAxMqrgtCNyK0OB2hff6O7SnK9y4jo5g/viewform) for the Interactive Components Beta program to start experimenting with this new feature as it is not yet available in the current stable release. Joining the Beta is free and once you submit the form, it should not take more than two or three days before you see Interactive Components appear in your Figma design tool.

### Freebie

I have created a Figma design file with the examples from this article. Once you join the Beta, you can duplicate my design and follow along more easily.

- [Download the Figma design file&nbsp;&rarr;](https://www.figma.com/community/file/949638648436079728)

## Before Starting

It’s necessary to understand some key Figma elements that we are going to use, if you’re already familiar with them you can skip this part and start directly with the first tutorial (section: “Create your first Interactive Component”).

### Components

Think of these as items that, when duplicated, create a connection with its copy (called **instance**) and when the component is changed, the instance receives the same changes. You can also apply overrides to instances (which are basically style changes to the component properties which allow for some customization).

- Learn more about [**Components**&nbsp;&rarr;](https://help.figma.com/hc/en-us/articles/360038662654-Guide-to-Components-in-Figma)
- Learn more about [**Overrides**&nbsp;&rarr;](https://help.figma.com/hc/en-us/articles/360039150733)

### Variants

These are the different styles a component can have and are usually used to apply different properties such as size or states.

- Learn more about [**Variants**&nbsp;&rarr;](https://help.figma.com/hc/en-us/articles/360056440594-Create-and-use-variants)

### Interaction Details Panel

It’s important to understand the Interaction Details panel because it allows us to define the different interactions and animations for our interactive components. Figma has a lot of information on their site so I will include links for those of you that want to dig deeper.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64cea099-45ca-428f-a5ec-26b06a31d521/12-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64cea099-45ca-428f-a5ec-26b06a31d521/12-introduction-figma-interactive-components.png" width="800" height="497" sizes="100vw" caption="Interaction Details panel (annotated). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64cea099-45ca-428f-a5ec-26b06a31d521/12-introduction-figma-interactive-components.png'>Large preview</a>)" alt="The Figma interaction details panel with notes to identify the triggers, actions, destination and animations." >}}

#### Hotspot

Even though this is not inside the panel, the hotspot is the element where the interaction will happen, in our case, each variant will be an interactive hotspot for which you can define triggers and actions.

#### Triggers

These are known in development as **Events** and are the different ways we the user can activate an interaction.

- On Click,
- On Drag,
- While Hovering,
- While Pressing,
- Key/gamepad,
- Mouse Enter,
- Mouse Leave,
- Mouse Down,
- Mouse Up,
- After Delay.

- More information about [**Triggers**&nbsp;&rarr;](https://help.figma.com/hc/en-us/articles/360040035834-Prototype-triggers).

#### Actions

In this setting, you can define what will happen when the interaction is activated; for interactive components, we will use **Change To** which allows swapping the variants inside a component. 

- Change To,
- Navigate To,
- Open Overlay,
- Scroll To,
- Swap With (overlay),
- Back,
- Close Overlay,
- Open URL.

#### Destination

This is the final target of the action. In my examples, I will use a variant as the destination to swap it from Switch OFF to Switch ON.

#### Animations

Figma comes with a set of pre-defined transitions that can be useful for some cases (move in, push, slide-in) but I always prefer to go with **Smart Animate** and define my own transitions as it’s really easy to use &mdash; it basically checks the layer names and if there are changes between the selected frame and the destination frame, it will animate those layers.

- More information about Figma [**Transitions**](https://help.figma.com/hc/en-us/articles/360040522373-Prototype-animations) and [**Smart Animate**](https://help.figma.com/hc/en-us/articles/360039818874-Create-advanced-animations-with-Smart-Animate)&nbsp;&rarr;

#### Easing

Easing refers to the way the animation moves, it’s basically how the element accelerates and decelerates. I’m going to use two settings for this tutorial: **Ease In and Out** for the switch, and **Linear** for the loops, but have in mind that it’s also possible to define a custom easing so you might want to learn more about [**Easing**](https://help.figma.com/hc/en-us/articles/360051748654-Prototype-easing-curves). 

{{% feature-panel %}}

## Creating Your First Interactive Component

Now that you have all the information you can start making your first interactive component. I’ll show you a very common case by creating a simple switch that has two states (Off and On) and use the variants to replicate those states.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74698650-1de3-4868-848d-c85eea085a58/21-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74698650-1de3-4868-848d-c85eea085a58/21-introduction-figma-interactive-components.gif" width="400" height="280" alt="A switch component that is being activated by the pointer." /></a><figcaption>We’ll start by creating a simple switch.</figcaption></figure>

### Create A Component

The first step is to create a component.

- Using the Rectangle tool (`R`), create a grey rectangle (#A7A9BC) `56x32` pixels in size and apply a corner radius of `16` px. 
- Using the Ellipse tool (`O`) create a white circle (`#FFF`) `24x24` pixels in size and place it over the rectangle in the left part, leaving `4` px of spacing. This is how it should look:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0804cfbb-d848-43cf-a289-241525056079/20-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0804cfbb-d848-43cf-a289-241525056079/20-introduction-figma-interactive-components.png" width="800" height="251" sizes="100vw" caption="The switch component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0804cfbb-d848-43cf-a289-241525056079/20-introduction-figma-interactive-components.png'>Large preview</a>)" alt="A simple switch component in the off state." >}}

- Combine these two elements into a single component using <kbd>Ctrl/Cmd</kbd> + <kbd>Alt</kbd> + <kbd>K</kbd> (or using the Component icon from the top bar in Figma):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3193dbae-c024-4593-8c91-737760b3fffc/3-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3193dbae-c024-4593-8c91-737760b3fffc/3-introduction-figma-interactive-components.png" width="600" height="192" sizes="100vw" caption="The Component icon in the top bar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3193dbae-c024-4593-8c91-737760b3fffc/3-introduction-figma-interactive-components.png'>Large preview</a>)" alt="The Figma component icon, it’s composed by four squares rotated at 45 degrees." >}}

**Note:** Here and in other places, I will use the Windows/Mac universal key notation, where the <kbd>Ctrl</kbd> key in Windows corresponds to the <kbd>Cmd</kbd> key on the Mac; <kbd>Alt</kbd> in Windows is the equivalent of <kbd>Alt/Option</kbd> on the Mac, so I’ll use <kbd>Alt</kbd> for short, and <kbd>Shift</kbd> is the same on both platforms.

### Add A Variant

- Select the component you’ve just created and, in the right panel (inside the Design tab), click on the plus button near **Variants**:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d2db9f-6031-48f1-b70b-462f860eadae/6-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d2db9f-6031-48f1-b70b-462f860eadae/6-introduction-figma-interactive-components.png" width="800" height="470" sizes="100vw" caption="Part of the Design sidebar panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59d2db9f-6031-48f1-b70b-462f860eadae/6-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Part of the design sidebar panel showing the position of the button to add variants." >}}

It will generate a purple frame with a dashed border that represents the group of variants you have. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c7e4e7-b853-4a1f-ad20-34038d7708c0/26-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c7e4e7-b853-4a1f-ad20-34038d7708c0/26-introduction-figma-interactive-components.png" width="800" height="367" sizes="100vw" caption="The group of variants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c7e4e7-b853-4a1f-ad20-34038d7708c0/26-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Two switch components with the off state inside a variant group." >}}

You should have two variants by now, use the first one for the **Off** **state** and the second one for the **On** **state**. 

- Apply a different style to the **On** **state** to make it the active option, I recommend using a blue background (#0B5FFF) and move the circle to the right. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3a0f3ed-d446-4ded-b9fb-e68111adde0d/27-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3a0f3ed-d446-4ded-b9fb-e68111adde0d/27-introduction-figma-interactive-components.png" width="680" height="396" sizes="100vw" caption="Now the two styles are defined for the Off and On states. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3a0f3ed-d446-4ded-b9fb-e68111adde0d/27-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Two switch components inside the variant group, one turned on and the other one turned off." >}}

These are the states of the switch that are going to change from **Off** to **On** (and vice-versa) when the user clicks on the switch.

**Useful tip:** For this case it is *not* necessary but if you need to add *more variants* you can select a component inside the box and click the purple plus button, it will add a copy of the selected component and resize the box automatically. (It’s also possible to resize the box manually as if it was a frame and freely duplicate and arrange the variants inside it.)

#### Alternative approach

As you’ve seen, we’ve created these components by duplicating them inside the variant group but **it's also possible to create them individually and combine them as variants**, the final result will be exactly the same. If you want to try this method just create and select two components, the right panel will then have another action called “Combine as variants,” click it and done &mdash; you will now have the same two variants.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61803bd4-11c5-4852-b7b2-0033b19d167f/2-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61803bd4-11c5-4852-b7b2-0033b19d167f/2-introduction-figma-interactive-components.png" width="800" height="246" sizes="100vw" caption="Select the components and combine them as variants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61803bd4-11c5-4852-b7b2-0033b19d167f/2-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Two separated switch components at the left with an arrow pointing to the right, to a button with the action combine as variants. Next to the button there is another arrow pointing at the right to a variant box with the two switch components inside it." >}}

This alternative is really useful when you already have different components and only need to define the variants, if you're working on a library it will help you update it without having to recreate everything from scratch.

### Name Your Variants

Naming the variants won’t have a direct effect over the final result *(unless you use the same name more than once)*, but defining the names and hierarchies will help you have everything better organized and understandable for other colleagues that might need to use the prototype for other projects.

By default the main group of variants is named “Property 1”, you can change this from the sidebar when selecting the entire group. I suggest renaming this to “State” since we’re going to use Off and On states.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff2e8cc-eeb1-4389-9d02-58c44d1bdfba/14-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff2e8cc-eeb1-4389-9d02-58c44d1bdfba/14-introduction-figma-interactive-components.png" width="800" height="255" sizes="100vw" caption="Rename the variants from 'Property 1' to 'State'. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff2e8cc-eeb1-4389-9d02-58c44d1bdfba/14-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Two copies of the same panel that has one input for the variant name, the first panel at the left has the input filled with the word 'Property 1', and the second panel at the right has the input filled with the word 'State'. Between the panels there is an arrow pointing to the right to show the change from 'Property 1' to 'State'. " >}}

Renaming a single variant is done by using the same process but you need to select the single variant inside the group and in the same panel you’ll find the names “Default” and “Variant 2” that you can overwrite, for the switch name these should be “Off” and “On”.

As a result, the layer names of the variants will be automatically changed to “State=Off” and “State=On”.

**Fun fact:** If your component only has two variants and you use the names “Off” and “On”, it will show a switch instead of a dropdown in the destination!

### Let’s Make It Interactive!

Now that you have the component and the variants it’s time to apply the **interactions**.

- Click on the Prototype tab (at the top-right side of the screen) to open the Prototype panel and activate its features.
- Select the **Off** variant (it should have a blue dot) and drag it over the **On** variant to connect it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550657cb-d00a-4206-be1a-3e686c96073a/4-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550657cb-d00a-4206-be1a-3e686c96073a/4-introduction-figma-interactive-components.png" width="800" height="363" sizes="100vw" caption="The On state connected to the Off state. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550657cb-d00a-4206-be1a-3e686c96073a/4-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Two switch components inside a variant group, the first one is turned off and connected to the second one that is turned on." >}}

- Double-check that you have selected the whole variant and not just the background layer, this will make the interaction work even when the user clicks on the circle element.
- In the Interaction Details panel set the trigger to **On Click**.
- Make sure the action is set to **Change To**.
- Change the animation to **Smart Animate** and use Ease In And Out for a natural feeling.

I'll translate these settings into a single sentence to explain what will happen: when the user **Clicks** on ***Off*** **State** then **Change to** ***On*** **State** using **Smart Animate** with **Ease In And Out** at **300 milliseconds.**

- Apply the same settings to the **On State** variant so that when clicked again it, will turn off the switch. (**Note:** Figma will remember the interaction settings applied to the elements inside the group and will apply the same settings when dragging a new interaction so in this case, you would only need to double-check.)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/286d5aa0-5e13-4993-b0ea-9a00a48580b4/25-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/286d5aa0-5e13-4993-b0ea-9a00a48580b4/25-introduction-figma-interactive-components.png" width="800" height="323" sizes="100vw" caption="Both states are now connected. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/286d5aa0-5e13-4993-b0ea-9a00a48580b4/25-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Two switch components connected to each other." >}}

Done! If you want to check if it works you need to include one of the variants into a frame, select the frame and then click on the presentation button (represented by the play icon) that is placed over the tabs.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d71e63cd-948e-4ddd-8162-713deb2e2bd5/17-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d71e63cd-948e-4ddd-8162-713deb2e2bd5/17-introduction-figma-interactive-components.png" width="478" height="238" sizes="100vw" caption="The 'Play' icon. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d71e63cd-948e-4ddd-8162-713deb2e2bd5/17-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Part of the Figma interface with focus on the Play icon used for prototypes" >}}

It should allow you to turn On/Off every switch individually. 

However, if you want to see the real power of this feature, duplicate the component in the frame multiple times (at least three or more) and activate them individually in the presentation.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df848f72-3f4b-4425-b691-8c4147c548f1/22-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df848f72-3f4b-4425-b691-8c4147c548f1/22-introduction-figma-interactive-components.gif" width="400" height="440" alt="Three switch interactive components being pressed randomly and multiple times with the mouse cursor." /></a><figcaption>The switch interactive components in action.</figcaption></figure>

### Using More Than Two Variants

This feature becomes very powerful when you add multiple variants and connect them individually to make a realistic component. Here is an example where I’ve connected a total of **six** **variants** with small changes to the background color to recreate the multiple states of a button, a classic in the web design industry nowadays.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f241146-f537-4bc1-bf42-0273a645460c/7-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f241146-f537-4bc1-bf42-0273a645460c/7-introduction-figma-interactive-components.png" width="800" height="349" sizes="100vw" caption="A dropdown button with six different states as variants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f241146-f537-4bc1-bf42-0273a645460c/7-introduction-figma-interactive-components.png'>Large preview</a>)" alt="Six different dropdown buttons showing the color changes for each state." >}}

#### Component States

This is the list of the different states for this component, including also the triggers we’re going to use to change from one variant to another. 

1. Default &mdash; Default,
2. Hover &mdash; WhileHover,
3. Pressed &mdash; MouseDown,
4. Active &mdash; MouseUp (It could be possible to use On Click for the same result),
5. Hover while Active &mdash; WhileHover,
6. Pressed while Active &mdash; MouseDown.

**Useful tip:** It’s possible to use **MouseDown** to simulate the button being *pressed* but not released and then use **MouseUp** to activate a transition, it’s a nice interaction detail that makes the button feel more real.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/193b1539-0945-4c03-b91c-ee20cad2bbb6/8-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/193b1539-0945-4c03-b91c-ee20cad2bbb6/8-introduction-figma-interactive-components.gif" width="600" height="300" alt="One single dropdown button animated with its six different states." /></a><figcaption>Use the MouseDown trigger before the Click trigger.</figcaption></figure>

### Nested Interactive Components

As for the regular components, you can also create **nested** interactive components. 

Using the same example of the dropdown it would be possible to create a single interactive component called *Dropdown* with two interactive components inside it: the *Dropdown Button* and the *Dropdown Menu.* This will help you control how the button and the menu interact with each other, allowing you to define which variant of the button will trigger the opening of the menu.

**Note:** It would be possible to create another nested component for the dropdown menu options and use the override to change the different texts.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45458569-40d5-4658-8823-b25ca4668fd5/15-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45458569-40d5-4658-8823-b25ca4668fd5/15-introduction-figma-interactive-components.png" width="800" height="248" sizes="100vw" caption="The same dropdown button with a dropdown menu that only appears in the On Click and While Hover variants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45458569-40d5-4658-8823-b25ca4668fd5/15-introduction-figma-interactive-components.png'>Large preview</a>)" alt="A variant group with six variants composed by a dropdown button and a dropdown menu, the image is showing that it is possible to hide the menu in some states of the button." >}}

The main benefit of using nested interactive components is the new level of modularity that it provides for prototypes, you could define the interactions individually and mix them into infinite interactive components. The *Dropdown Menu* could be included in other components (a card, for example) without having to prototype how it works every single time. 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e7b8fe9-a988-4711-bd15-ad8ccd7301ae/10-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90c6fce3-989c-4bed-8a17-3188d989e1dc/10-introduction-figma-interactive-components-800w.gif" width="800" height="355" alt="Three dropdown buttons and a cursor showing how hover and click work, each dropdown opens and closes a menu." /></a><figcaption>It’s possible to simulate real Hover and Click effects. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e7b8fe9-a988-4711-bd15-ad8ccd7301ae/10-introduction-figma-interactive-components.gif">Large preview</a>)</figcaption></figure>

### Navigation

We can go even further, it’s also possible to navigate from a variant to an external frame, you can connect the single variant to the frame by using the **On Click** trigger and **Navigate To** action. In this example I’ve connected each one of the actions from the *Dropdown Menu* component to an external frame with a grey rectangle in the same position as the menu (Right, Top, Left, Bottom).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90711a09-4a37-403d-8e5b-dbc3f559bb34/16-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90711a09-4a37-403d-8e5b-dbc3f559bb34/16-introduction-figma-interactive-components.png" width="800" height="306" sizes="100vw" caption="Prototype destinations can be connected outside the variant frame. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90711a09-4a37-403d-8e5b-dbc3f559bb34/16-introduction-figma-interactive-components.png'>Large preview</a>)" alt="A diagram showing a group of five variants of a dropdown menu with four options: right, top, left, bottom. Each option is connected to an external artboard using the OnClick trigger." >}}

When one of these actions is clicked, it will navigate to the connected frame as it happens with regular prototypes, the real magic happens when you need to reuse the *Dropdown Menu* for another component, it will have all the interactions inside already done, so you don’t have to connect it over and over again. 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1a75579-a4f9-4b75-814e-e86f20009c11/9-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b39f389-bdb1-4fca-aee1-7957d9994eaf/9-introduction-figma-interactive-components-800w.gif" width="800" height="497" alt="A dropdown button opens a menu with four different options: right, top, left, bottom. When clicking one of these, a panel shows up from the same direction as the options." /></a><figcaption>This dropdown menu is a great example of how real an interactive component can get. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1a75579-a4f9-4b75-814e-e86f20009c11/9-introduction-figma-interactive-components.gif">Large preview</a>)</figcaption></figure>

This workflow and the features of the nested components are amazing for product design cases where you have tons of frames to connect as they will reduce the amount of work required to create a high-fidelity prototype for testing, or even if you want to create a components library for prototypes.

{{% ad-panel-leaderboard %}}

## Special Effects

That was all for the introduction to Figma **interactive components**. As you can see, it’s pretty easy to use this feature to create and connect interactions inside a prototype. But it’s also possible to create various kinds of special effects using **variants**.

In the following section, I will take a close look at these!

### Loops

It’s finally possible to make infinity loops inside Figma without too much effort and also you can create various spinners and loading indicators. 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7726525c-3a0e-4e7b-a277-1b65d134ca92/18-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c5191e-0041-437c-b1f6-b24ef37d8af8/18-introduction-figma-interactive-components-500w.gif" width="500" height="470" alt="Two different sets with three animated rectangles. In the first set, the rectangles resize randomly while in the second set the rectangles are aligned and simulate a carousel movement." /></a><figcaption>Elements can be resized to create infinite loops. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7726525c-3a0e-4e7b-a277-1b65d134ca92/18-introduction-figma-interactive-components.gif">Large preview</a>)</figcaption></figure>

To create a loop, use the **After Delay** trigger set to `1` ms to swap the variants automatically and connect at least two of them.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/722f4dec-52d2-42ec-8616-b17b443128fb/5-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/722f4dec-52d2-42ec-8616-b17b443128fb/5-introduction-figma-interactive-components.png" width="800" height="539" sizes="100vw" caption="Use the After Delay trigger set to 1 ms and connect the variants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/722f4dec-52d2-42ec-8616-b17b443128fb/5-introduction-figma-interactive-components.png'>Large preview</a>)" alt="A diagram with instructions to create a loop. There are three variants and arrows, the first variant is connected to the second variant, the second variant to the third, and the third variant to the first variant to create an infinite loop." >}}

**Note:** `1` ms is the **minimum** amount of time we can set in Figma to change from a variant to another and make it an almost instantaneous change; and, thanks to the AfterDelay trigger, it will happen automatically. It’s possible to use a higher delay time if you need the loop to look like it has a pause between the variants.

### Rotation

Let me start the next part of the article with a note about how strangely Figma handles rotation.

Figma has a weird way to rotate elements, it seems to be limited from `-179`º to a maximum of `180`º and does not allow to go further than these values. In addition, there is no way to define a rotation direction so if you try to rotate from `0`º to `180`º and vice-versa, instead of doing a `360`º turn, it will first rotate to `180`º and then come back to `0`º (like a swing). 

So, to let the system identify correctly the rotation you will need to use at least **three** variants.

Here’s how you can do it:

- Create a component with three variants: VariantA, VariantB, VariantC (for this example I modified an ellipse to make the triangle shape).
- Apply the following rotation to the elements **inside** the variants (**not** the variants themselves).
    - **VariantA:** set the element to `0`º and connect the variant to **VariantB**.
    - **VariantB:** set the element to `-120`º and connect the variant to **VariantC**.
    - **VariantC:** set the element to `120`º and connect the variant to **VariantA** to complete the loop.
- All the interactions should have **After Delay (1ms)** as a trigger and a **Linear** easing.

The result will be a neutral spinner that will have three small pauses of `1` ms each because of the variant swap, not perfect but fast and for a prototype, it’s good enough &mdash; and you will be probably the only one that will notice the pauses anyway. 

**Useful tip**: You can either use the same animation time for each variant to make a linear loop, or you can play with the animation using a faster time for some variants and a slower time for others, this will simulate a curved easing.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc57af1-e8c7-41eb-bf40-c3add3232315/19-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc11b95e-c702-4149-bf81-f26f3b6b2938/19-introduction-figma-interactive-components-800w.gif" width="800" height="404" alt="Two circular shapes similar to a pie missing a piece, the shapes are rotating with different timings, the first one is linear and the second one uses a combination of slow and fast times." /></a><figcaption>The rotation is the same but the animation times are different. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc57af1-e8c7-41eb-bf40-c3add3232315/19-introduction-figma-interactive-components.gif">Large preview</a>)</figcaption></figure>

#### Complex Spinners

I wouldn’t suggest using Figma interactive components for complex spinners, for such cases it might be better to create the spinner with a dedicated animation app (such as After Effects) and import it into the prototype as a GIF. 

### Micro Interactions

Interactive components allow you to include more delightful details into prototypes. I’ll go back to the switch example to show you how to add micro-interactions to this component using **MouseDown** and **On Click**. 

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21775d66-5c50-435d-aba3-075595de86cb/23-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21775d66-5c50-435d-aba3-075595de86cb/23-introduction-figma-interactive-components.gif" width="388" height="212" alt="This is the same switch as before, with two states, but with the difference that when clicked the circle inside the switch will deform in the opposite direction, creating a nice visual effect, as if the circle was magnetically attracted to the other side of the switch." /></a><figcaption>Do you want to turn a simple switch into an amazing switch?</figcaption></figure>

#### Component

To recreate this example you need to apply some changes to the structure of the switch:

- Make a copy of the **Off** state switch that you already created.
- Create another ellipse shape of `16*24` px, place it over the previous ellipse (the circle).
- Unify the two ellipses as a boolean group using **Union**.

- Learn more about [**Boolean groups**&nbsp;&rarr;](https://help.figma.com/hc/en-us/articles/360039957534-Boolean-Operations).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0880468c-9b60-4d74-83b5-22e65bcd3e68/1-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0880468c-9b60-4d74-83b5-22e65bcd3e68/1-introduction-figma-interactive-components.png" width="800" height="275" sizes="100vw" caption="The boolean group will combine these two shapes into a single circle. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0880468c-9b60-4d74-83b5-22e65bcd3e68/1-introduction-figma-interactive-components.png'>Large preview</a>)" alt="A diagram showing how a boolean union works using two ellipses, one big and another one small." >}}

- Apply `32` px of border-radius to the Union layer, this will create the distortion effect you can see in the example.
- Create the component (<kbd>Ctrl/Cmd</kbd> + <kbd>Alt</kbd> + <kbd>K</kbd>).

#### Variants and Prototype

You’ll need a total of four variants to make this work: `OffState`, `OffStatePressed`, `OnState`, and `OnStatePressed`.

- Use the **Mouse Down** trigger to simulate the mouse being pressed and activate the distortion by moving the bigger ellipse `8` px to the other side.
- Use the **On Click** trigger to change states from Off to On.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f0c2836-1fed-4ef4-9c28-e589ea1de8a7/13-introduction-figma-interactive-components.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f0c2836-1fed-4ef4-9c28-e589ea1de8a7/13-introduction-figma-interactive-components.png" width="800" height="599" sizes="100vw" caption="Here’s another fun diagram showing how to construct the interactive component! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f0c2836-1fed-4ef4-9c28-e589ea1de8a7/13-introduction-figma-interactive-components.png'>Large preview</a>)" alt="A diagram showing how to connect four variants to recreate the micro interaction. The first one uses MouseDown to activate the second variant, the second variant uses OnClick to activate the third variant, the third variant uses MouseDown to activate the fourth variant, and the fourth variant uses OnClick to activate the first variant." >}}

### 3D Animation With A Sequence Of Images

Before we continue, I want to thank [**Andrea Cau**](https://twitter.com/aerdna_c), the author of this cool 3D sequence that I’m going to use as an example. 

This is more of a hack to integrate 3D animations into a Figma prototype, you could also use GIFs but this way you gain full control over the images, not just play/stop, allowing you to create a prototype that simulates an interface to rotate objects, commonly seen in car websites where you can rotate the car.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57b98cb4-3803-4af7-9b72-b307c221e513/11-introduction-figma-interactive-components.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebd3177a-c9dc-4905-bc76-9a048767e4ed/11-introduction-figma-interactive-components-500w.gif" width="500" height="500" alt="The main object is a glass square with inside a porcelain sphere, it is a 3D composition and the object is positioned in a 45 degrees view. There are two arrows, one to the right and another one to the left. The animation shows the mouse clicking on the arrows and the object rotates to the same direction." /></a><figcaption>Imagine an e-commerce website with a 3D model that you can turn around. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57b98cb4-3803-4af7-9b72-b307c221e513/11-introduction-figma-interactive-components.gif">Large preview</a>)</figcaption></figure>

In this case, I’ve used nine images (you could use more, or less, depending on the rotation you need), the important steps to reproduce this interaction are: 

- Create one variant per image (in this case 9 variants will be needed) and include one image in each one, following the sequence order.
- Create the arrow button, it will be the Hotspot.
- Connect the right arrow to the next variant (repeat for every variant).
- Connect the left arrow to the previous variant (repeat for every variant).
- Use the **Instant** animation instead of Smart Animate to avoid the fade in/out effect and create the illusion of movement.

## Conclusion

The more I use this feature the more I think it will be a game-changer for companies working in the areas of web and product design. Mastering interactive components and variants will allow designers to produce better, more advanced, and realistic prototypes with less effort, giving you the freedom to work on the actual designs and focus less on the design tool itself.

As mentioned earlier, I’ve created a Figma community file with the examples from this article (and a few more experiments that I’ve been doing during the testing of the new feature). Once you [join the Beta](https://docs.google.com/forms/d/e/1FAIpQLSctELo9clvK0uP-0zDAxMqrgtCNyK0OB2hff6O7SnK9y4jo5g/viewform), feel free to duplicate my design, follow along or start experimenting, and **share your results!** Play with the animation times, change the easing, try to rotate, scale elements, try to nest different interactive components.

- [Download the Figma design file&nbsp;&rarr;](https://www.figma.com/community/file/949638648436079728)

If you have questions or something is not entirely clear, leave a question in the Comments section below, or ping me on Twitter ([@emi_cicero](https://twitter.com/emi_cicero)) &mdash; I’d be glad to help! :)

### Further Reading

- [Components](https://help.figma.com/hc/en-us/articles/360038662654-Guide-to-Components-in-Figma)
- [Overrides](https://help.figma.com/hc/en-us/articles/360039150733)
- [Variants](https://help.figma.com/hc/en-us/articles/360056440594-Create-and-use-variants)
- [Triggers](https://help.figma.com/hc/en-us/articles/360040035834-Prototype-triggers)
- [Smart Animate](https://help.figma.com/hc/en-us/articles/360039818874-Create-advanced-animations-with-Smart-Animate)
- [Easing](https://help.figma.com/hc/en-us/articles/360051748654-Prototype-easing-curves)
- [Figma interactive components playground](https://www.figma.com/community/file/946809607056414616)
- [Interactive Components in Figma](https://www.youtube.com/watch?v=slmLyaolF50) (video by [@mds](https://twitter.com/mds))
- [Advanced Interactive Components in Figma](https://www.youtube.com/watch?v=ChAyF6JeANw&ab_channel=MDSMDS) (video by [@mds](https://twitter.com/mds))
- [SketchTogether interactive components video](https://www.youtube.com/watch?v=plD2XRrK7hw&ab_channel=SketchTogether)

{{< signature "mb, vf, yk, il" >}}
