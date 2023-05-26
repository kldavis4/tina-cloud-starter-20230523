---
title: 'Composition-Based Design System In Figma'
slug: composition-based-design-system-figma
author: aleksandra-nagornaia
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/671611c3-eaf7-427e-9e5d-1bb74fbf62f5/composition-based-design-system-figma.jpg
date: 2022-01-03T13:00:00.000Z
summary: >-
  Figma has advanced enough where it now supports some powerful concepts that can help with the flexibility and maintainability of a design system. In this article, Sasha explains why she finds the Systems Designer position so rewarding &mdash; and it’s not only because of how fast certain tools have developed to help her master challenges she faces in her work projects.<br /><br />**Editor’s Note**: This article comes with a [Figma-playground file](https://www.figma.com/community/file/1052482110625940513/Composable-components), so feel free to jump in and explore the concept.
description: >-
  Figma has advanced enough where it now supports some powerful concepts that can help with the flexibility and maintainability of a design system. In this article, Sasha explains why she finds the Systems Designer position so rewarding &mdash; and it’s not only because of how fast certain tools have developed to help her master challenges she faces in her work projects.
categories:
  - Design
  - Tools
  - Figma
---

Working as a designer on a design system for a large product has taught me how precious the time you spend on a single task/component is. Things advance fast, and I try to keep up making it work for both designers and developers. It is no easy task.

I’ve noticed that a good chunk of team members’ productivity goes into **endless conversations** such as:

<blockquote>“Should this be a separate component?”<br /><br />“Should it be a variant?”<br /><br />“What should the configuration options look like?”<br /><br />...and so on.</blockquote>

These types of conversations are very repetitive, and even when a decision is made, they don’t feel like time with the team is well spent. There are so many questions to be answered.

**What do you optimize for?** Is it for consistency, scalability, creativity or maintainability? You can optimize for so many things &mdash; and choosing only one often sacrifices another.

It’s difficult to define a set of rules that would put an end to these meetings in the future. What topped this problem up was one interface element that stood out due to its huge reusability and variations: **list item**.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34489310-200b-4db2-b963-c4a919f908cc/8-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34489310-200b-4db2-b963-c4a919f908cc/8-composable-design-architecture.png" width="800" height="310" sizes="100vw" caption="Four list items: all same, but different. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34489310-200b-4db2-b963-c4a919f908cc/8-composable-design-architecture.png'>Large preview</a>)" alt="Title-Subtitle list item" >}}

If the **Title-Subtitle** list item is a component, then:

- Is the image (chevron) indicating a new component or a variant of one? 
- What if it’s not a navigation chevron at the end but an (info) icon instead?
- What if it has a leading image in front?
- What if it has a switch?

Aaand at the same time, **they share states** (selected, pressed, disabled, and so on). Try to get the team iOS, Android and designers in a call to make a decision on it. 🤯

Thankfully, I’ve been surrounded by people that are open to collaboration across teams. After teaming up with developers, I started recognizing developer terms and patterns in the designer tool.

At the same time, Figma has been peeking over developers' shoulders for **layout building tools** (like auto-layout, variants with properties, constraints, and so on), so now it allows designers to approach component building closer to how things look in code.

Observing developers in how they build and think about the components gives you a perspective on its structure. Soaking those patterns allowed me to build the components with *almost* the same rules in Figma (looking at you, min and max-width/height setting).

## Introducing “Composition” For Design Systems: Composable Content And Containers

Let’s take a look at this **list item** component:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9930b4b-bf64-43d9-9ee9-69ee7f3f0db7/13-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9930b4b-bf64-43d9-9ee9-69ee7f3f0db7/13-composable-design-architecture.png" width="800" height="503" sizes="100vw" caption="We always have a background that (in our case) could change depending on its state: primary, secondary, accent (plus its custom interaction and animation). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9930b4b-bf64-43d9-9ee9-69ee7f3f0db7/13-composable-design-architecture.png'>Large preview</a>)" alt="List item with primary, secondary and accent state" >}}

The way we had them in our project was just a collection of all the possible *list items*, i.e. with a large icon, small icon, subtitle, toggle, trailing text, and so on. They were all separately defined with their backgrounds and named numerically (starting from list item 1 to 8).

So, we had no semantics in place defining our *list items* in a more meaningful way, as well as no optimized way of maintaining updates to the defined background styling and layout. What started happening was that **new inconsistent states started appearing** in some files: 

1. A **choice-list item** would have a tinted background in one design file (indicating selection), but just a checkmark on the right side in another;
2. The **paddings** would be different across design files.

Reasonably, the backgrounds of *list items* should stay consistent throughout all screens and be flexible to fit different content inside. So, how do we enforce that through a design system *across all teams*?

There are a couple of ways, so let’s get a bit technical here. One approach is **Variation**.

{{% feature-panel %}}

### Variation

First, define all *list items* that exist in the interface and identify their variants:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668070d5-a060-4beb-abfe-381e84f22917/16-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668070d5-a060-4beb-abfe-381e84f22917/16-composable-design-architecture.png" width="800" height="531" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668070d5-a060-4beb-abfe-381e84f22917/16-composable-design-architecture.png'>Large preview</a>)" alt="Different list items in the interface." >}}

Then, add all the defined *list items* states (secondary, accent, and so on) as variants per each list item. This will double each original component/variant per state and you’ll be able to account for all possible states that a *list item* might have.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7cb4cd0-693f-486f-b34e-0cb09118337d/15-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7cb4cd0-693f-486f-b34e-0cb09118337d/15-composable-design-architecture.png" width="800" height="507" sizes="100vw" caption="Example: One-sided List item has 3 original variants. If they have 2 additional states, we add them to each variant &mdash; 9 variants in total. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7cb4cd0-693f-486f-b34e-0cb09118337d/15-composable-design-architecture.png'>Large preview</a>)" alt="Defined list items states." >}}

This is how we first thought to approach the problem, but you can clearly see the issues with it: bloating the number of variants that need to be maintained where you have an unnecessary repetition of background and other elements.

Now, imagine this. Let’s try changing the following:

- Secondary background (grey) to have a different color/corner radius;
- Or font style of the Title;
- Or spacing between Title and Subtitle;
- Or image size.

You would have to go to every variant (32 in total in our case) and update each one manually in order to align these changes. 😨 This becomes a quite inefficient way to maintain these components, lightly speaking.

Let’s then move on to a better approach: **Composition**.

### Composition

We’ll start with composing a *container* 🔴. Here we define the background styling and padding (can also include corner radius, shadows, and so on), and nest the instance of a *Generic content placeholder* 🔷 that will allow us to swap it with any other component.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78f2663-0596-4504-8327-dc87ab89d181/14-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78f2663-0596-4504-8327-dc87ab89d181/14-composable-design-architecture.png" width="800" height="297" sizes="100vw" caption="Container basically defines the background look and a placeholder area for any content to be hosted in. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78f2663-0596-4504-8327-dc87ab89d181/14-composable-design-architecture.png'>Large preview</a>)" alt="Container basically defines the background look and a placeholder area for any content to be hosted in." >}}

Our list items will have a few *Enhancing elements* 🔶 in them, such as s checkmark, navigation chevron, switch or button. Since they might apply to any defined background and to all generic content, we would need to compose another container for those elements.

- The *container* defines the element and its location with paddings;
- Same *placeholder* instance is nested inside again for content.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6968053c-5757-4fff-968c-29c5d7842ace/2-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6968053c-5757-4fff-968c-29c5d7842ace/2-composable-design-architecture.png" width="800" height="391" sizes="100vw" caption="Notice how these don’t have neither background color nor padding, these come from what they’ll be nested in. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6968053c-5757-4fff-968c-29c5d7842ace/2-composable-design-architecture.png'>Large preview</a>)" alt="Notice how these don’t have neither background color nor padding, these come from what they’ll be nested in." >}}

Next, let’s define the list items *content* ⚫️ (e.g. *Multiline list item*) that your interface has without background (only text and images):

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f944b83-f779-4791-ac4d-f39a8280fd53/3-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f944b83-f779-4791-ac4d-f39a8280fd53/3-composable-design-architecture.png" width="800" height="310" sizes="100vw" caption="This one can be easily split into multiple components with less variants and nothing would change in our approach. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f944b83-f779-4791-ac4d-f39a8280fd53/3-composable-design-architecture.png'>Large preview</a>)" alt="This one can be easily split into multiple components with less variants and nothing would change in our approach." >}}

Now, in order for us to assemble the needed *list item*, we need to think from the ground up (Z-axis first):

- Take the *container* 🔴 and select a needed state;
- Swap the *placeholder* 🔷 inside with the list item *content* ⚫️ you defined >> ☑️
- Or if you have an *enhancing element* in a list item (like a switch, button, and so on):
    - Swap the *placeholder* 🔷 with the *element container* 🔶,
    - Then swap inside the *placeholder* 🔷 with a list item *content* ⚫️ >> ☑️.

{{< vimeo id="660077544" >}}

In the end, it is not only that we align design and development approaches by using composition, but in addition, it would be *the* most optimized way to build such components in design and code for consistency and maintainability. Now our design component has become almost like a pseudo code for developers.

Talking about code...

Let’s see how things look like in development. Here is some code and a rendered iOS preview for a few SwiftUI composition components:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/accccf37-1e78-43c6-9b73-d7b78a27d0bb/4-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/accccf37-1e78-43c6-9b73-d7b78a27d0bb/4-composable-design-architecture.png" width="800" height="543" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/accccf37-1e78-43c6-9b73-d7b78a27d0bb/4-composable-design-architecture.png'>Large preview</a>)" alt="Some code and a rendered iOS preview for a few SwiftUI composition components." >}}

Some of these combinations are silly, but they do showcase the power of the approach. Notice how the switch (toggle) component is actually native/system for iOS and how it plugs into our composition with our custom components completely seamlessly, both in code and visually. 

This is because modern front-end frameworks such as SwiftU for iOS and Jetpack Compose for Android (no kidding it literally has “Compose” in its name 😉) rely on the same composition approach that we are describing &mdash; and what Figma now allows, too.

## Why Even Build Composable Components?

Well, there are at least five good reasons why we’d want to build composable components:

- [Consistency](#1-consistency)
- [Error-Proof Design](#2-error-proof-design)
- [Absolute Flexibility](#3-absolute-flexibility)
- [Reduces Variants](#4-reduces-variants)
- [Better Teamwork](#5-brings-the-teams-together)

### 1. Consistency
  
By putting all the background patterns in one place to be reused, we ensure that those background states are represented consistently across the features and teams, as a single source of truth. When these states are not really defined, you get visually different designs for these states across the screens &mdash; the more designers on the team, the more inconsistencies there will be.

### 2. Error-Proof Design
  
We completely eliminate an opportunity for a designer to misuse the states, mistaken the paddings, introduce something that already exists, etc. Unless you detach the instance...

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0a16c7f-1dff-4413-b674-0dd5db2f9207/1-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0a16c7f-1dff-4413-b674-0dd5db2f9207/1-composable-design-architecture.png" width="800" height="384" sizes="100vw" caption="" alt="The text in the picture: you wouldn’t detach an instance, would you?" >}}
  
### 3. Absolute Flexibility

Do you need to nest some other component inside your *list item*? Voilà! We don’t need to limit a *list item* to host specific content only. You can put any content inside. Let’s see how we can put the contents that we used for *list items* into a *card* container absolutely seamlessly.

{{< vimeo id="660078019" >}}

Usually, consistency is achieved at the expense of flexibility, but not in this case.

### 4. Reduces Variants

There is no longer a need to include *list item* states in every *list item* component. You have it defined in one place and reused as a *container*, same for the *elements* that *list item* can host, like switches, buttons, icons, and so on. Helps for maintainability and scalability of the components.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64841e41-d33f-427a-976b-0eed70882af3/10-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64841e41-d33f-427a-976b-0eed70882af3/10-composable-design-architecture.png" width="800" height="471" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64841e41-d33f-427a-976b-0eed70882af3/10-composable-design-architecture.png'>Large preview</a>)" alt="Variation approach vs. Composition approach." >}}
  
Now scale this to a whole design system. You can see why I consider the *variation* approach unmaintainable.

### 5. Brings The Teams Together

Building components in design the same as in code removes the friction in documentation and specs, as well as allows sharing the same process and language between designers and developers.

And guess what, this can be applied to many other components that share a similar composable structure. The most obvious components that we put as candidates for this upgrade are:

- **cards**: reusing backgrounds like active, highlighted, disabled,
- custom **bottom sheets**: reusing container and putting any content inside.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2f0c9ec-4aaa-496c-a6dd-e273e03c19f4/9-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2f0c9ec-4aaa-496c-a6dd-e273e03c19f4/9-composable-design-architecture.png" width="800" height="347" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2f0c9ec-4aaa-496c-a6dd-e273e03c19f4/9-composable-design-architecture.png'>Large preview</a>)" alt="Cards and bottom sheets." >}}

{{% ad-panel-leaderboard %}}

## When To Use It And When Not?

You can probably already see that this structure optimizes consistent reuse and maintainability the most, but don’t go overboard with it. Here is **a general rule** of when you can go with composition:

<blockquote>You use composition when you can (reasonably) slice a component (on X/Y/Z axis) into 2 parts “Generic content” and “Enhancing elements” where:<br />
  <ul><li><strong>“Generic content”</strong> is the slice (area) of a component that hosts any UI content.</li>
    <li><strong>“Enhancing elements”</strong> include the constant UI elements (like switch, chevron, background) and interaction behaviour (animations) of a component.</li></ul></blockquote>

This rule leaves a lot of room for interpretation because slices can be seen differently by different people, but that’s fine because it demonstrates the flexibility and power of this approach where you have multiple ways to achieve your goal.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a67364c-3243-44a0-a515-7c025937f693/6-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a67364c-3243-44a0-a515-7c025937f693/6-composable-design-architecture.png" width="800" height="435" sizes="100vw" caption="Not only you want to reuse the generic content because it contains quite a bit of logic (icon colors, IBAN formatting), but also there are other possibilities of generic content for the Radio group and Choice list components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a67364c-3243-44a0-a515-7c025937f693/6-composable-design-architecture.png'>Large preview</a>)" alt="Generic content and Enhancing elements" >}}
  
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cf4ac8-afc0-49a1-a075-3da2cd1b3d55/5-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cf4ac8-afc0-49a1-a075-3da2cd1b3d55/5-composable-design-architecture.png" width="800" height="478" sizes="100vw" caption="Background here looks reusable but actually reacts to the input state, which creates coupling between the text field and the background, meaning they are not agnostic of each other. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cf4ac8-afc0-49a1-a075-3da2cd1b3d55/5-composable-design-architecture.png'>Large preview</a>)" alt="Background here looks reusable but actually reacts to the input state, which creates coupling between the text field and the background, meaning they are not agnostic of each other." >}}

{{% ad-panel-leaderboard %}}

## Managing The Power

If you decide to embrace the composable structure in your design system, I would recommend splitting your components into layers of hierarchy in Figma:

1. **Container-backgrounds**  
These compose on the Z-axis and only define:
    - **styling**: background color, corner radius, shadow, and so on.
    - **general layout**: paddings, the position of the content.
2. **Enhancing-elements containers**  
Containers that might include additional elements like chevron, switch, button, icon, etc.
3. **Content**  
Components that are actual generic content implementations. They are the final node of the composition tree.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15939de-f136-4a76-9715-b19bb4cc56d3/12-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15939de-f136-4a76-9715-b19bb4cc56d3/12-composable-design-architecture.png" width="800" height="337" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15939de-f136-4a76-9715-b19bb4cc56d3/12-composable-design-architecture.png'>Large preview</a>)" alt="Three layers of hierarchy in Figma: Container-backgrounds, Enhancing-elements containers, Content." >}}
  
You can see how you now have the power to compose anything. And just like lego pieces, your components are capable of infinite combinations that might actually be silly in practice, like in the example below.
  
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de4c50b-65e4-4a4e-994a-38019c16d379/11-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de4c50b-65e4-4a4e-994a-38019c16d379/11-composable-design-architecture.png" width="800" height="206" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3de4c50b-65e4-4a4e-994a-38019c16d379/11-composable-design-architecture.png'>Large preview</a>)" alt="An example of components which are capable of infinite combinations." >}}
  
So, you might decide that you want to limit the usage combinations of your composable components. As in the example of combining checkmark and switch, we clearly don’t want to nest both of these elements in one *list item*, so what we can do instead is to couple *enhancing-container* with applicable *container-backgrounds* as a new component.

In the *Navigation list item*, you couple *container-background* (with 2 variants, default and pressed) with *enhancing-container* (chevron). That way, you define all of the possible variations of this component. Also, even though you can still put any content inside, you cannot use another state (like highlighted) or add other elements like toggles to it.
  
{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9bc4c74-9ed8-43dc-9a58-2f66406f451b/7-composable-design-architecture.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9bc4c74-9ed8-43dc-9a58-2f66406f451b/7-composable-design-architecture.png" width="800" height="326" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9bc4c74-9ed8-43dc-9a58-2f66406f451b/7-composable-design-architecture.png'>Large preview</a>)" alt="Three columns: Navigation list item, Switch list item and Selectable list item." >}}
  
## Final Notes

So far, my team and I have adopted composable components for *cards* and *list items* for both mobile platforms, iOS and Android &mdash; and we love it.

Developers and designers quickly grew very fond of this approach. Although the component building is becoming more complex, everyone sees that it makes our design system more elaborate and elegant.

Generally, if you leave it to live only in a design system without syncing it in code, it will already be beneficial enough. You do need to put effort into building it, but then it pays off well with less maintenance &mdash; just as much as it does for design systems.

*This article was written in collaboration with my iOS developer husband. Thank you, Petar Kanev.*

{{< signature "vf, yk, il" >}}
