---
title: 'Everything Developers Must Know About Figma'
slug: everything-developers-must-know-about-figma
author: christine-vallaure
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57ba237f-8cb7-48aa-8538-93a3fe26d997/everything-developers-must-know-about-figma.jpg
date: 2022-08-15T11:30:00.000Z
summary: >-
  Christine highlights some of Figma’s features and possibilities to help you build a design that aligns with code as much as needed and improve your team work.
description: >-
  Christine highlights some of Figma’s features and possibilities to help you build a design that aligns with code as much as needed and improve your team work.
categories:
  - UI
  - Figma
  - Guides
  - Workflow
---

We must understand the possibilities and limitations of each other’s tools to work hand in hand, so let me show you the design side of things and all the little Figma treasures you might not yet understand fully.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb045466-6112-4611-a2f9-694637cad7c7/54-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb045466-6112-4611-a2f9-694637cad7c7/54-everything-developers-must-know-figma.png" width="800" height="343" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb045466-6112-4611-a2f9-694637cad7c7/54-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Two hearts with a Figma logo and code inside." >}}

1. [We work with components and variants in Figma](#1-we-work-with-components-and-variants-in-figma).
2. [We work with styles in Figma, but they are not very smart](#2-we-work-with-styles-in-figma-but-they-are-not-very-smart).
3. [We can set up and test responsive design!](#3-we-can-set-up-and-test-responsive-design)
4. [We have no breakpoints in Figma](#4-we-have-no-breakpoints-in-figma).
5. [We can also work with actual data (sort of)](#5-we-can-also-work-with-actual-data-sort-of).
6. [You might want to point out soft grid vs. hard grid to us](#6-you-might-want-to-point-out-soft-grid-vs-hard-grid-to-us).
7. [Why we sometimes mess up line-height](#7-why-we-sometimes-mess-up-line-height).
8. [All we have in Figma is PX](#8-all-we-have-in-figma-is-px).
9. [We can set up pretty sweet prototypes in Figma](/#9-we-can-set-up-pretty-sweet-prototypes-in-figma).
10. [We will invite you to ‘View Only’ rights, giving you access to everything you need as a developer](#10-we-will-invite-you-to-view-only-rights-giving-you-access-to-everything-you-need-as-a-developer).

## 1. We Work With Components And Variants In Figma

### Components In Figma

In Figma, we can set up re-usable UI components and create instances. **Components can also be nested.** Hence we can follow a nice [atomic design](https://atomicdesign.bradfrost.com/) path.

{{< vimeo id="736480249" >}}

#### We Also Have Variants

We can also create component sets containing variants, **swapping** them easily throughout our design via the properties panel. Therefore, all **states** of a component can be found in one place for documentation.

{{< vimeo id="736482094" >}}

Figma variants can be **one-dimensional or multi-dimensional**, adding **several properties.**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99d72008-835d-43bc-b1b9-bc1f5c5a200a/3-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99d72008-835d-43bc-b1b9-bc1f5c5a200a/3-everything-developers-must-know-figma.png" width="800" height="301" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99d72008-835d-43bc-b1b9-bc1f5c5a200a/3-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Figma variants with added several properties" >}}

**Tip:** *With `true/false or yes/no`, you can create a toggle of the entire component. This is a great way to create a `light/dark mode`.I saw this setup in [Joey Banks’s](https://www.joeyabanks.me/) excellent [iOS 16 UI Kit for Figma](https://www.figma.com/community/file/1121065701252736567). Best file setup I have ever seen in general!*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c28d06-66fc-40f8-8715-6219e5d35d67/4-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c28d06-66fc-40f8-8715-6219e5d35d67/4-everything-developers-must-know-figma.png" width="800" height="233" sizes="100vw" caption="Source: <a href='https://www.figma.com/community/file/1121065701252736567'>Joey Banks iOS UI Kit for Figma</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c28d06-66fc-40f8-8715-6219e5d35d67/4-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Joey Banks iOS UI Kit for Figma" >}}

#### We Have Props!

Component properties were released in March 2022. So I assume a lot of developers do not know about the possibility of using them in design yet. So far, we have **text props, for instance, swap and toggle props**. And of course, we can combine them all together.

{{< vimeo id="736484670" >}}

#### External Or Local Component Libraries

Just as in code, we can store components locally or create external libraries. (Same for styles, by the way). This way, we can pull components into multiple files in Figma yet remain a single source of truth and tidy structure.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/463ece74-bba6-494b-b6b1-bd91017f3d28/5-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/463ece74-bba6-494b-b6b1-bd91017f3d28/5-everything-developers-must-know-figma.png" width="800" height="322" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/463ece74-bba6-494b-b6b1-bd91017f3d28/5-everything-developers-must-know-figma.png'>Large preview</a>)" alt="External or local component libraries" >}}

### Opportunities Between Design And Code

#### Align UI And Code Components In Naming And Structure

Due to the use of components, variants, and props, we can align our UI components with code components. However, to do so, we need information about the structure, naming, behavior, etc., from development. So sit down with us, have a coffee, and show us the code base you have or dream of building. Many videos and tutorials show how different teams handle this alignment process. I leave you to the rabbit hole.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae29757-4197-49ad-a4e5-3890a26886e2/6-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae29757-4197-49ad-a4e5-3890a26886e2/6-everything-developers-must-know-figma.png" width="800" height="283" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae29757-4197-49ad-a4e5-3890a26886e2/6-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Screenshot of how to align UI and Code components in naming and structure" >}}

#### Quick Link UI And Code Components In Figma

If you want to link components to a code base without much effort and documentation, you can simply add a link and a description to the Figma component documentation (a bit hidden). The link will create a button in the inspect tab linking directly to, e.g., the Github section of the same component in code. The Figma component search also picks up the description, which is handy for larger systems.

{{< vimeo id="736486721" breakout="true" >}}

#### Embed A Figma Component In Your Documentation

You can simply copy a link (<kbd>Cmd</kbd> + <kbd>L</kbd>) of the Figma file (or frame) and live embed it in places like Notion, GitHub, and many more. I did just this in the example below. This is a great way to live embed your design with an existing (probably more code-heavy) documentation. It will, of course, update as you change your Figma file.

<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Ffile%2F4Yp6P5bn2x6RTRfWSMkvxf%2FDay-07-moonlearning-BookApp-Full%3Fnode-id%3D1%253A2" allowfullscreen></iframe>

#### Create A Test Environment And Swap Component Libraries

If components and styles have the same name in two different libraries, they can be swapped. This is a really great opportunity to set up test environments in Figma before pushing a new style or component to the master file. More relevant for advanced setups where code and components are already aligned.

{{< vimeo id="736489640" breakout="true" >}}

#### Align With Your Actual Components Via Storybook

There are some plugins to align UI components and code components. The most promising one I saw is [Storybook Connect](https://www.figma.com/community/plugin/1056265616080331589). By the way, if you have this fantastic setup, how do you align your code? And Figma makes sure to comment! I would love to hear and add it!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/491a5d5c-1581-4958-a896-140e62bf1aa9/9-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/491a5d5c-1581-4958-a896-140e62bf1aa9/9-everything-developers-must-know-figma.png" width="800" height="343" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/491a5d5c-1581-4958-a896-140e62bf1aa9/9-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Storybook Connect" >}}

**Note:** *Aligning components is fantastic, but it also takes a lot of effort and, most of all, maintenance, so use it where it makes sense, e.g., a design system. If you just design a one-pager website, you still use components with a clean and scalable design and clear building blocks to be coded, but they do not necessarily need to align with the code. It’s like you would not build an assembly line to streamline the process of making a cake if you would only want to bake a birthday cake for your friend. Yet you still use the same basic ingredients.*

{{% feature-panel %}}

## 2. We Work With Styles In Figma, But They Are Not Very Smart

### Styles In Figma

In Figma, we can create styles for **color, text, grids**, and **things like shadows or blurs** and re-apply them across our design. However, that’s pretty much it.

{{< vimeo id="736490819" breakout="true" >}}

**Tip:** *Click on the grey background area of the canvas, and you get an overview of all (local!) styles.*

**There is no magic documentation**

But any design team usually documents styles and their use either within the **same Figma file or in a separate file**. Just as with components, we can **link to external styles**. Oh, and there are **no spacing systems styles, so we just need** to document this and set the correct distances by hand.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dde98f58-9dbf-425f-88e9-7e1bedb17b17/11-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dde98f58-9dbf-425f-88e9-7e1bedb17b17/11-everything-developers-must-know-figma.png" width="800" height="586" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dde98f58-9dbf-425f-88e9-7e1bedb17b17/11-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Documentation of styles" >}}

### Opportunities Between Design And Code

**Figma Token Plugin to create or connect with existing tokens**

As you can see, Figma styles are a bit isolated and do not interact with one another. So you cannot set a base font size to scale and adapt the scaling rate. You can only set a fixed size. Also, we have no styles for spacing systems (yet). However, with the [Figma Tokens](https://www.figma.com/community/plugin/843461159747178978) plugin, you can create tokens in Figma and work with them. And even more impressive, you can connect and can align with code tokens. Check out the (really well-made) [documentation](https://docs.figmatokens.com/) and this fantastic [video by the creator Jan Six](https://www.youtube.com/watch?v=zkLfw6Jb6WM). So amazing!!!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7391714-0f56-4b6d-a592-b603930b83d0/12-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7391714-0f56-4b6d-a592-b603930b83d0/12-everything-developers-must-know-figma.png" width="800" height="370" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7391714-0f56-4b6d-a592-b603930b83d0/12-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Figma Tokens plugin" >}}

## 3. We Can Set Up And Test Responsive Design!

This is a big one! Let’s look at it step by step. The tools we have for responsive design are the following:

Our tools in Figma for responsive design:

- [Auto Layout](#auto-layout)
- [Constraints](#constraints)
- [Grid](#grid)

We can use the above tools **individually, not at all, or combine them**. It depends a lot on what we want to build. There is no right or wrong.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee5e30e-ee38-4415-9fdf-945e8876364f/13-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee5e30e-ee38-4415-9fdf-945e8876364f/13-everything-developers-must-know-figma.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ee5e30e-ee38-4415-9fdf-945e8876364f/13-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Tools in Figma for responsive design" >}}

Very important to know from a developer’s point of view is that **we have no automated breakpoints in Figma** (I will talk about how to deal with that in a bit).

### Auto Layout

Auto layout is really powerful but takes some practice to work with (and will drive you nuts to start with, but stick with it!!!). It is [(loosely) based on flexbox](https://www.figma.com/blog/behind-the-feature-the-making-of-the-new-auto-layout/), as you will notice when you glimpse at the Inspect tab.

{{< vimeo id="736493620" breakout="true" >}}

With the auto layout, we can set:

1. **Space between** items (can be positive for spacing or negative for stacking);
2. **Padding** on all sides individually;
3. **Alignment**;
4. Set child element so **packed or space between** (ideal for navigations);
5. **Resizing behavior** (full container, hug content, or fixed both horizontally and vertically);
6. **Nest auto layout** to create **powerful components and even entire pages**;
7. Add **relative positioned elements** inside an auto layout frame (new);
8. Automatically **adapt to new content** while keeping all settings in place.

### Constraints

Constraints are much more straightforward to work with in Figma. With constraints, you can pin elements to the parent frame when resizing. Note that they will react to a change in parent size but will not adapt to a change in content!

{{< vimeo id="736494363" breakout="true" >}}

**Note:** *You cannot add auto layout and constraints to the same frame. It is either or (small exception for relative positioned elements within auto-layout). There is no better or worse. It depends on what you want to build.*

### Grids

We can add grids to frames. When setting up grids, we can adjust columns, gutter, margin, and behavior.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018dfc88-d022-433e-8878-2224ffca27b8/16-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018dfc88-d022-433e-8878-2224ffca27b8/16-everything-developers-must-know-figma.png" width="800" height="301" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/018dfc88-d022-433e-8878-2224ffca27b8/16-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Grids" >}}

### Combine Grids And Constraints

The cool thing is that as soon as a grid is applied to a frame, the constraints will assume the columns as the parent frame. So we can set up really nice and straightforward responsive behavior by combining grids and constraints.

{{< vimeo id="736495427" breakout="true" >}}

**Tip:** *Figma is all about nesting. You can also apply grids to nested frames, e.g., to create a frame for the sidebar with a fixed with and another nested frame holding the content.*

{{< vimeo id="736495846" breakout="true" >}}

**Limitation:**

This works fine for a quick test or simple setup. However, as soon as you add more content, you will notice that the **margins and padding will not adapt when resizing**. This is a **Figma issue; in CSS, it would still work just fine.**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81a59d7b-afed-41ff-8b5a-15bebbb9cb90/19-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81a59d7b-afed-41ff-8b5a-15bebbb9cb90/19-everything-developers-must-know-figma.png" width="800" height="313" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81a59d7b-afed-41ff-8b5a-15bebbb9cb90/19-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Margins and padding do not adapt when resizing if you add more content" >}}

### Combine Grid, Constraints, And Auto Layout Elements

So even though we cannot combine auto layout and constraints within a frame, we can place auto layout elements/instances inside a parent frame and then use constraints around them. In this way, the content reshuffles nicely, keeping all set parameters.

{{< vimeo id="736497136" breakout="true" >}}

**Limitation:**

Horizontal spacing will still not adapt. So you will probably have the question in mind: “And if I make it all into an auto layout?” Yes, you can!

### Pure Auto Layout Pages

So we could also set up the design in auto layout entirely. There are two ways to use this:

1. **Imitating a classic grid**, then we just set the space between = gutter and get the same result.
2. Not **work with a Grid System at all,** but set up your design later in **flexbox, CSS-Grid or anything else,** then we just “auto layout away” as we want, you can also **mix fixed and fluid.**

{{< vimeo id="736497856" breakout="true" >}}

**Limitation:**

The auto layout will only distribute elements equally, so you cannot have one element occupying 60% and the other 40%; it will switch to 50/50%. You would have to fix one element and have the rest fluid.

{{% ad-panel-leaderboard %}} 

## 4. We Have No Breakpoints In Figma

Ok, great, so we have these sweet features to set up responsive components. However, we have no automation in Figma to set up a breakpoint to test across different screen sizes from mobile to desktop.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4be4c44e-1ac5-4e8a-a9ff-435b00f6434e/22-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4be4c44e-1ac5-4e8a-a9ff-435b00f6434e/22-everything-developers-must-know-figma.png" width="800" height="162" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4be4c44e-1ac5-4e8a-a9ff-435b00f6434e/22-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of no breakpoints in Figma" >}}

### We Can Make Our Own Breakpoints By Hand!

However, we can create our own breakpoints by hand! So with the technical information given, we can set up the visual representation in Figma. I am just using a random example of breakpoints here.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be615b1-df9c-4532-95dd-3c7ed9ef28ca/23-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be615b1-df9c-4532-95dd-3c7ed9ef28ca/23-everything-developers-must-know-figma.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be615b1-df9c-4532-95dd-3c7ed9ef28ca/23-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of how to create our own breakpoints by hand" >}}

We can then place our auto layout components within those ranges and see where adjustments are necessary. In my example, I switch from a full fluid screen on mobile to an overlay with a fixed size at breakpoint `S`.

{{< vimeo id="736504441" breakout="true" >}}

This way, we can really test our components and even entire pages and already have a pretty realistic idea of the look and feel.

#### If You Want To Work With A Responsive Grid

We can use the same testing setup for responsive grids if needed. With the necessary information, grids can be set up for several screen size ranges and then saved as styles and re-applied. We then just need to add the correct grid when testing the breakpoint range.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4604b3ca-31f4-4283-bd7a-348b5d16ceb4/25-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4604b3ca-31f4-4283-bd7a-348b5d16ceb4/25-everything-developers-must-know-figma.png" width="800" height="289" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4604b3ca-31f4-4283-bd7a-348b5d16ceb4/25-everything-developers-must-know-figma.png'>Large preview</a>)" alt="A responsive grid" >}}

**Note:** *Sometimes, you might use the same grid for several breakpoints, then just note, e.g., Grid: `S`+`M` (from 576 to 992). This way, you could always split it in two again in case the margin or anything changes in the future.*

#### Responsive Typography Is Non-Existent

Unfortunately, what kicks in automatically with media queries in CSS needs to be **added by hand in Figma**. We can set up a **responsive Typescale** and then need to make sure to **change text style (if applicable) when breakpoints are changing**. It’s a bit annoying and full of potential errors, I know.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72ef6ab-359a-44e4-8c83-dbc7d91960d4/26-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72ef6ab-359a-44e4-8c83-dbc7d91960d4/26-everything-developers-must-know-figma.png" width="800" height="351" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72ef6ab-359a-44e4-8c83-dbc7d91960d4/26-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of how to set up responsive typography" >}}

If you want to work with **fluid typography** (VW units, `clamps()`, `calc()`, you name it), this is best **tested in the browser as we cannot simulate fluid text behavior with Figma**. We can, however, pick a specific min and max screen size to get a rough idea of the situation at a specific width.

### Breakpoint Plugin

However, to end on an exciting topic: Once you go through the effort of setting up your components and pages responsively, you can chuck them into the breakpoints plugin and get a really lovely overall idea of the design.

{{< vimeo id="736634749" breakout="true" >}}

### Opportunities Between Design & Code

#### Save Time, Money And Nerves

Let’s be honest handing in a static design and then seeing the result in the browser never leads to an easy-going relationship between design and development. It is a bottleneck that burns time, money, and nerves on both sides.

Now, this does not mean that we hand off design with a bit of auto layout on top, and that’s it. Seeing the outcome in the browser will surely hold some surprises and room for discussion. However, we have a solid base to start working from and can enter a constructive dialogue between design and development to fine-tune.

Some things will no doubt remain easier to test in CSS than in Figma (e.g., responsive typography), which is just fine. Ultimately, it is about working as a team and valuing each other’s time and effort to create great products.

#### Align Components With Code

We can also align components further with existing code by mimicking the behavior.

### Flexbox In The Inspect Tab. But In The End, It’s Up To Development!

When peeking into the inspect tabs, we can see that auto layout translates to (sort of) flexbox, or as Figma put it, “[Auto Layout should be a thoughtful subset of flexbox](https://www.figma.com/blog/behind-the-feature-the-making-of-the-new-auto-layout/)” hmmm. This is also where it gets a little confusing because it does not mean you HAVE to use flexbox. In Figma, we only have constraints and auto layout, and as you saw, they both have pros and cons to them and do not reflect CSS behavior 100%. So if there is a more innovative or sensible way of setting something up, then, by all means, go for it!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa98138-ada7-45a0-8de6-b14855cbd5c4/28-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa98138-ada7-45a0-8de6-b14855cbd5c4/28-everything-developers-must-know-figma.png" width="800" height="383" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaa98138-ada7-45a0-8de6-b14855cbd5c4/28-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Flexbox in the inspect tab" >}}

## 5. We Can Also Work With Actual Data (Sort Of)

Figma cannot connect to a classic database, but we can use actual data with some preparation. You can use the[ Google Sheets Sync](https://www.figma.com/community/plugin/735770583268406934) plugin and just add actual content there. By simply naming our layers with #columnname, run the plugin, add the link, and hit sync. And boom, there you go. There is also a Plugin for [Airtable](https://www.figma.com/community/plugin/741940457537193498) and [Notion](https://www.figma.com/community/plugin/1116202373222780315) Sync working pretty much in the same way.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5607949d-3aab-416a-b735-5fe11676eb26/29-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5607949d-3aab-416a-b735-5fe11676eb26/29-everything-developers-must-know-figma.png" width="800" height="199" sizes="100vw" caption="Google sheet with real data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5607949d-3aab-416a-b735-5fe11676eb26/29-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Google sheet with real data" >}}

{{< vimeo id="736639771" breakout="true" >}}

**Tip:** *You can even swap variants dynamically! Isn’t that great?*

### Opportunities Between Design And Code

#### Know What You Are Dealing With

It’s great to test actual content and ask for some collaboration from copywriters or content managers on the fly. This way, we do not design with perfect lorem ipsum and stock image components but realistic components in content size and look.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a5badd2-1105-488c-a8ad-b820a962ed65/31-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a5badd2-1105-488c-a8ad-b820a962ed65/31-everything-developers-must-know-figma.png" width="800" height="343" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a5badd2-1105-488c-a8ad-b820a962ed65/31-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Deisgn chairs vs real chairs" >}}

In general, we should test components with different content such as ideal state, little content, heavy content, empty, error, and loading states where applicable. I made a [checklist for components](https://www.figma.com/community/file/1117518363362257693) you can use before release.

Working with actual data gives us a good idea of potential shortcomings. We can also see if the database needs some grooming or if the image pool needs a bit of love and attention to live up to the brand promise.

## 6. You Might Want To Point Out Soft Grid vs. Hard Grid To Us

When we click on Grids, Figma adds this px grid to the background. Order! Structure! As a designer, you jump at this, and as you were told to space with 8pt, you use the grid.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8ee096-d28d-4ca3-9867-f6ed2f7cbb7d/32-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8ee096-d28d-4ca3-9867-f6ed2f7cbb7d/32-everything-developers-must-know-figma.png" width="800" height="310" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f8ee096-d28d-4ca3-9867-f6ed2f7cbb7d/32-everything-developers-must-know-figma.png'>Large preview</a>)" alt="8pt Grid" >}}

So we have this grid, which is why many designers jump to conclusions using a hard grid to set their spacing (it can be used for other alignment and handy in mobile setup, though). We have no spacing blocks or cubes to create a soft grid, we can set this by hand, though, and nudge in steps of `8`, but that is about it.

**Tip:** *In Figma, we can alter the nudge amount. Press <kbd>Cmd</kbd> + <kbd>/</kbd> and type “nudge” and change to `8`. Make sure to keep `alt` pressing when nudging to see the distances. By pressing shift and up and down arrows, we then nudge in, e.g., `8pt` steps.*

### Opportunities Between Design And Code

#### How Does Spacing Work For You In CSS?

Feel free to point out (preferably at the beginning of the project) that there is no such magic background grid in CSS and that the spacing system means measuring in spacing blocks from element to element (including the line height!). Or, in other words, explain the difference between the hard grid vs. the soft Grid that we use later in UI Design and CSS.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/001e58c5-9ae5-4c6d-b2b6-80d5dc9453c9/33-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/001e58c5-9ae5-4c6d-b2b6-80d5dc9453c9/33-everything-developers-must-know-figma.png" width="800" height="330" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/001e58c5-9ae5-4c6d-b2b6-80d5dc9453c9/33-everything-developers-must-know-figma.png'>Large preview</a>)" alt="soft grid vs. hard grid" >}}

**And yet again: Use the [Figma Tokens Plugin](https://www.figma.com/community/plugin/843461159747178978).**

Here we can just pull the real spacing system with spacing tokens and apply it to our components. We can also set up our own tokens just in Figma right in the plugin.

{{< vimeo id="736645277" breakout="true" >}}

{{% ad-panel-leaderboard %}} 

## 7. Why We Sometimes Mess Up Line-height

Typography is UI design, quite a complex topic. Here is a [detailed class](https://www.moonlearning.io/typography-preview) I made. Many UI Designers have a graphic design background, where text is aligned with the baseline. However, in Figma and CSS, we work with line height. This often leads to a lot of confusion amongst new designers, and I get the question “how do I get rid of this access space on top and bottom of my text?” a lot. You don’t. Just work with it!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed60fcca-2018-44d4-a4a5-a731aaa386dc/35-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed60fcca-2018-44d4-a4a5-a731aaa386dc/35-everything-developers-must-know-figma.png" width="800" height="182" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed60fcca-2018-44d4-a4a5-a731aaa386dc/35-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of how to set line height in Figma" >}}

**Note:** *We cannot set line height in Figma to something like `1.5` notation! By default, it uses px. But we can cheat a little and use `%`, so `1.5` in CSS would be `150%` in Figma. You will still find the px value only in the inspect tab.*

### Opportunities Between Design And Code

#### Explain It!

So as a developer, you might find that the line height is randomly set to `1`. This is a desperate design attempt to get rid of the “random” space we do not understand (yet). So it makes sense to remind (new) designers that UI Design is dynamic. Screen sizes change, and content length will vary (either because the content is added or translated into a new language). Thus, we can never assume a single line of the text remains a single line of text forever. Also, we do not want to create too many styles. So explain that working with the natural line height is just fine, and you will do the same in CSS.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12257b8b-43de-4834-a8a9-6bcf54776e2d/36-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12257b8b-43de-4834-a8a9-6bcf54776e2d/36-everything-developers-must-know-figma.png" width="800" height="189" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12257b8b-43de-4834-a8a9-6bcf54776e2d/36-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Line-height-1 vs line-hight-1.5" >}}

## 8. All We Have In Figma Is PX

In Figma, we can only work with px, and we work at 1px=1pt. We do not have rem, em, or any other relative way to define things like font size. So if you see px everywhere in a UI Design, this does not mean we want it hard coded!!!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48a3efbd-4d82-4f7f-bb93-482d2eecceba/37-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48a3efbd-4d82-4f7f-bb93-482d2eecceba/37-everything-developers-must-know-figma.png" width="800" height="131" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48a3efbd-4d82-4f7f-bb93-482d2eecceba/37-everything-developers-must-know-figma.png'>Large preview</a>)" alt="px and all the other ways like rem and em are crossed out" >}}

## 9. We Can Set Up Pretty Sweet Prototypes In Figma

We can create rather impressive prototypes directly from our design files in Figma. If you hit the play button in the file (top right), you can see them. We can link frames to new pages or overlays and also animate within component sets from variant to variant.

{{< vimeo id="736648934" breakout="true" >}}

We can also set up individual flows, making them nice and tidy to navigate and test.

{{< vimeo id="736649450" breakout="true" >}}

## 10. We Will Invite You To ‘View Only’ Rights, Giving You Access To Everything You Need As A Developer

As a developer, you will probably receive an invite to “view only” a Figma file, team, or project. You can have a look at a file I set up in [view mode here](https://www.figma.com/file/4Yp6P5bn2x6RTRfWSMkvxf/Day-07-moonlearning-BookApp-Full?node-id=134%3A11758) (make to sign up for a free Figma account beforehand).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ddacc5f-ca2b-4843-900e-cfa9629511d1/40-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ddacc5f-ca2b-4843-900e-cfa9629511d1/40-everything-developers-must-know-figma.png" width="800" height="284" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ddacc5f-ca2b-4843-900e-cfa9629511d1/40-everything-developers-must-know-figma.png'>Large preview</a>)" alt="view only mode" >}}

### Opportunities Between Design And Code

As a developer, you will be able to navigate the file and pull out all information you need:

#### Pages

You can navigate the different frames on the canvas but note how there are different pages above the layers menu on the left. Every team uses pages differently, some for versions and sprints, some to structure the file into the design, components, and testing. In any case, ensure not to overlook the pages as they are the file’s structure.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e68e967-1eda-41e1-a5b5-fa0bb3aefbaf/41-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e68e967-1eda-41e1-a5b5-fa0bb3aefbaf/41-everything-developers-must-know-figma.png" width="800" height="414" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e68e967-1eda-41e1-a5b5-fa0bb3aefbaf/41-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of pages and the layer menu on the canvas" >}}

#### Inspect Mode

When entering a file with view mode, you will see the **inspect menu** open per default. Click on an element, and you will be shown the **distance** to the nearest objects and the **specs on the right-hand side menu.**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ee52f0-364e-41dd-b9c5-9f1457158d9e/42-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ee52f0-364e-41dd-b9c5-9f1457158d9e/42-everything-developers-must-know-figma.png" width="800" height="415" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26ee52f0-364e-41dd-b9c5-9f1457158d9e/42-everything-developers-must-know-figma.png'>Large preview</a>)" alt="inspect menu" >}}

You can switch between CSS, iOS, and Android.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/424ea34e-4f4b-4a60-82ff-177a220c07a0/43-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/424ea34e-4f4b-4a60-82ff-177a220c07a0/43-everything-developers-must-know-figma.png" width="800" height="245" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/424ea34e-4f4b-4a60-82ff-177a220c07a0/43-everything-developers-must-know-figma.png'>Large preview</a>)" alt=" CSS, iOS, and Android options on the menu" >}}

When clicking on the main component, you will see the link to the code documentation (if applicable) and any comments in inspect mode.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d2c7bbe-4341-49eb-a1c9-fbe4ee8af9e0/44-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d2c7bbe-4341-49eb-a1c9-fbe4ee8af9e0/44-everything-developers-must-know-figma.png" width="800" height="343" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d2c7bbe-4341-49eb-a1c9-fbe4ee8af9e0/44-everything-developers-must-know-figma.png'>Large preview</a>)" alt="the link to Github and some comments in inspect mode" >}}

This only shows up if it was added to the design tab’s component documentation. And you obviously only need this if you want to align UI and code components.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154d9e50-f09a-440b-aafb-f15869aeab02/45-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154d9e50-f09a-440b-aafb-f15869aeab02/45-everything-developers-must-know-figma.png" width="800" height="245" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154d9e50-f09a-440b-aafb-f15869aeab02/45-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of the inspect mode with the link to Github added to the design tab’s component documentation" >}}

By the way, it works with any link. However, some such Github links create a nice custom button.

#### Styles Overview

Click on the canvas to get an overview of all styles in the file. Note that this only shows local styles; some might be pulled in from an external library. So the best is to check for style documentation (every design team should set this up for you) to make sure you have all information.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d58e781b-9523-4a6d-9696-1d0b2cf1f941/46-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d58e781b-9523-4a6d-9696-1d0b2cf1f941/46-everything-developers-must-know-figma.png" width="800" height="343" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d58e781b-9523-4a6d-9696-1d0b2cf1f941/46-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Styles overview" >}}

You should, however, still receive a general overview of all styles from your design team, including internal and external styles used now or in the future.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c87cbf-8102-45e4-b886-5c805b46b301/47-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c87cbf-8102-45e4-b886-5c805b46b301/47-everything-developers-must-know-figma.png" width="800" height="586" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c87cbf-8102-45e4-b886-5c805b46b301/47-everything-developers-must-know-figma.png'>Large preview</a>)" alt="a general overview of all styles including internal and external styles" >}}

#### Jump To The Main Component

This is really important yet a bit hidden. Click on any instance on the canvas and then click on the diamond-shaped symbol sign, and you will jump to the main component and documentation. This is where you can get all information and measurements.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61fdeda4-bc93-4409-b364-d9c983921965/48-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61fdeda4-bc93-4409-b364-d9c983921965/48-everything-developers-must-know-figma.png" width="800" height="163" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61fdeda4-bc93-4409-b364-d9c983921965/48-everything-developers-must-know-figma.png'>Large preview</a>)" alt="A diamond-shaped symbol with a sign 'jump to the main component'" >}}

You should then be led to the **Figma UI component library.** This might be a local page or an external UI component document giving you all the necessary information and specs defined by the UI team. If you do not find such an overview, kindly ask your design team to set this up for you.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857bf36a-016d-41e1-a000-40f387aa182c/49-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857bf36a-016d-41e1-a000-40f387aa182c/49-everything-developers-must-know-figma.png" width="800" height="418" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857bf36a-016d-41e1-a000-40f387aa182c/49-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Figma UI component library" >}}

<blockquote>There is no magic automation for style and component overview in Figma. This needs to be set up and documented by the design team, and the format may vary.</blockquote>

#### Export Assets Of Any Size And Form

Assets can be exported to any asset in the format (JPG, PNG, SVG) and @size from the “view only” mode, so no bulk export by the design team is needed anymore.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/271ef2d7-00e9-4c87-9329-ef610fb3d323/50-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/271ef2d7-00e9-4c87-9329-ef610fb3d323/50-everything-developers-must-know-figma.png" width="800" height="461" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/271ef2d7-00e9-4c87-9329-ef610fb3d323/50-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Different formats (JPG, PNG, SVG) of how assets can be exported" >}}

**Tip:** *For a specific height or width, instead of `3x`, `2x`, just enter the width followed by `w` (e.g., `300w`), and it will export it, keeping the image proportions. It also works for height (`h`).*

#### Comment

Leave comments and discuss within your team.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622ffb65-5658-4fd5-9993-141829a3afe3/51-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622ffb65-5658-4fd5-9993-141829a3afe3/51-everything-developers-must-know-figma.png" width="800" height="343" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622ffb65-5658-4fd5-9993-141829a3afe3/51-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Visualization of a comments window" >}}

#### Prototype

Hit the play button (top right corner of your design file), and you will jump to the presentation mode seeing your prototype in action. Usually, the designer was nice enough to add some flows and structure the prototype, so you get a good idea of different flows.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/597f7b4c-5b1c-431c-ba11-4d57ac2e402b/52-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/597f7b4c-5b1c-431c-ba11-4d57ac2e402b/52-everything-developers-must-know-figma.png" width="800" height="290" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/597f7b4c-5b1c-431c-ba11-4d57ac2e402b/52-everything-developers-must-know-figma.png'>Large preview</a>)" alt="the play button at the corner of a design file and Prototype on the right" >}}

**Tip:** *Individual links can be created from every flow of the prototype menu. I like using this to set up an overview of the design and testing stages. You can also link to any other team planning file here.*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd9d451-fe34-4696-bc8a-0bbbf7a13ebf/53-everything-developers-must-know-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd9d451-fe34-4696-bc8a-0bbbf7a13ebf/53-everything-developers-must-know-figma.png" width="800" height="335" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd9d451-fe34-4696-bc8a-0bbbf7a13ebf/53-everything-developers-must-know-figma.png'>Large preview</a>)" alt="Individual links for different design and testing stages" >}}

## Stay In Touch!

If you liked this article, make sure to subscribe and visit me on [moonlearning.io](https://www.moonlearning.io/), where I teach about UX/UI Design+Figma. This article is also the base of my talk and workshop during the [Smashing Conference New York, the 10th to the 13th of October 2022](https://smashingconf.com/ny-2022/). See you there!

{{< signature "mb, vf, yk, il" >}}