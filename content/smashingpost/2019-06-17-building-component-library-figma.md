---
title: 'Building A Component Library Using Figma'
slug: building-component-library-figma
author: emiliano-cicero
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f4d7dba-6199-4d08-b6df-37a646ce5386/sketch-icons-menu.png
date: 2019-06-17T14:00:16+02:00
summary: >-
  Figma has become a very popular tool for web and product designers, mainly because of its focus on design teams and team libraries. This article aims to help you avoid mistakes and assist you with the building of your own Figma component library.
description: >-
  Figma has become a very popular tool for web and product designers, mainly because of its focus on design teams and team libraries. This article aims to help you avoid mistakes and assist you with the building of your own Figma component library.
categories:
  - Sketch
  - Figma
  - Workflow
  - Graphics
---
I’ve been working on the creation and maintenance of the main library of our design system, Lexicon. We used the Sketch app for the first year and then we moved to Figma where the library management was different in certain aspects, making the change quite challenging for us. 

To be honest, as with any library construction, it requires time, effort, and planning, but it is worth the effort because it will help with providing detailed components for your team. It will also help increase the overall design consistency and will make the maintenance easier in the long run. I hope the tips that I’ll provide in this article will make the process smoother for you as well.

This article will outline the steps needed for building a component library with Figma, by using styles and a master component. (A master component will allow you to apply multiple changes all at once.) I’ll also cover in detail the components’ organization and will give you a possible solution if you have a large number of icons in the library.

**Note:** *To make it easier to use, update and maintain, we found that it is best to use a separate Figma file for the library and then publish it as a team ‘library’ instead of publishing the components individually.*

{{% feature-panel %}}

## Getting Started

This guide was created from a designer’s perspective, and if you have at least some basic knowledge of Figma (or Sketch), it should help you get started with creating, organizing and maintaining a component library for your design team.

If you are new to <a href="https://www.figma.com">Figma</a>, check the following tutorials before proceeding with the article:

<ul>
  <li><a href="https://www.figma.com/blog/component-styles-and-shared-library-best-practices/">Best Practices: Components, Styles And Shared Libraries</a></li>
  <li><a href="https://www.youtube.com/watch?v=jk1T0CdLxwU">Intro To Figma: Beginner’s Guide To Figma Basics</a> (Video)</li>
  <li><a href="https://www.figmaforbeginners.com/">Figma For Beginners</a></li>
  <li><a href="https://trydesignlab.com/figma-101-course/introduction-to-figma/">Figma 101</a></li>
</ul>

## Requirements

Before starting, there are some requirements that we have to cover to define the styles for the library.

### Typography Scale

The first step to do is to define the typography scale; it helps to focus on how the text size and line height grow in your system, allowing you to define the visual hierarchy of your texts.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09103df0-7808-401a-b336-15d2a2709c85/typography.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09103df0-7808-401a-b336-15d2a2709c85/typography.png" sizes="100vw" caption="Typography scales are useful to improve the hierarchy of the elements, as managing the sizes and weights of the fonts can really guide the user through the content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09103df0-7808-401a-b336-15d2a2709c85/typography.png'>Large preview</a>)" alt="a scale of text in different sizes, from small to big" >}}

The type of scale depends on what you’re designing. It’s common to use a bigger ratio for website designs and a smaller ratio when designing digital products.

<p class="c-pre-sidenote--left">The reason for this is behind the design’s goal &mdash; a website is usually designed to communicate and convert so it gives you one or two direct actions. It’s easier in that context to have 36px for a main title, 24px for a secondary title, and 16px for a description text.</p><p class="c-sidenote c-sidenote--right">Related resource: “<a href="https://medium.freecodecamp.org/8-point-grid-typography-on-the-web-be5dc97db6bc">8-Point Grid: Typography On The Web</a>” by Elliot Dahl.</p>

On the other hand, digital products or services are designed to provide a solution to a specific problem, usually with multiple actions and possible flows. It means more information, more content and more components, all in the same space.

For this case, I personally find it rare to use more than 24px for texts. It’s more common to use small sizes for components &mdash; usually from 12 to 18 pixels depending on the text’s importance.

<p class="c-pre-sidenote--left">If you’re designing a digital product, it is useful to talk to the developers first. It’s easier to maintain a typography scale based on EM/REM more than actual pixels. The creation of a rule to convert pixels into EM/REM multiples is always recommended.</p><p class="c-sidenote c-sidenote--right">Related resource: “<a href="https://blog.prototypr.io/defining-a-modular-type-scale-for-web-ui-51acd5df31aa">Defining A Modular Type Scale For Web UI</a>” by Kelly Dern.</p>

### Color Scheme

Second, we need to define the color scheme. I think it’s best if you to divide this task into two parts.

<ol>
<li>First, <strong>you need to define the main colors of the system</strong>. I recommend keeping it simple and using a maximum of four or five colors (including validation colors) because the more colors you include here, the more stuff you’ll have to maintain in the future.</li>
<li>Next, <strong>generate more color values using the Sass functions</strong> such as “Lighten” and “Darken” &mdash; this works really well for user interfaces. The main benefit of this technique is to use the same hue for the different variants and obtain a mathematical rule that can be automated in the code. You can’t do it directly with Figma, but any Sass color generator will work just fine &mdash; for example, <a href="https://sassme.jim-nielsen.com">SassMe</a> by Jim Nielsen. I like to increase the functions by 1% to have more color selection.</li>
</ol>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6bc0d8-c07b-426c-a079-f180821ff33b/color-scheme.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6bc0d8-c07b-426c-a079-f180821ff33b/color-scheme.png" sizes="100vw" caption="Once you have your main colors (in our case, blue and grey), you can generate gradients using lighten and darken functions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6bc0d8-c07b-426c-a079-f180821ff33b/color-scheme.png'>Large preview</a>)" alt="2 different sets of colors with different tones" >}}

**Tip**: *In order to be able to apply future changes without having to rename the variables, avoid using the color as part of the color name. E.g., instead of* `$blue`, *use* `$primary`.

<p><strong>Recommended reading</strong>: <em>“<a href="https://css-tricks.com/what-do-you-name-color-variables">What Do You Name Color Variables?</a>” by Chris Coyier</em></p>

### Figma Styles

Once we have the typography scale and the color scheme set, we can use them to define the Library styles.

This is the first actual step into the library creation. This feature lets you use a *single set of properties in multiple elements*.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95873604-59dc-4843-b278-bd0a736ca848/figma-styles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95873604-59dc-4843-b278-bd0a736ca848/figma-styles.png" sizes="100vw" caption="Styles are the way to control all the basic details in your library. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95873604-59dc-4843-b278-bd0a736ca848/figma-styles.png'>Large preview</a>)" alt="2 shapes showing a color palette and a text to represent the possible styles" >}}

{{% ad-panel-leaderboard %}}

### Concrete Example

Let’s say you define your brand color as a style, it’s a soft-blue and you originally apply it to 500 different elements. If it is later decided that you need to change it to a darker blue with more contrast, thanks to the styles you can update all the 500 styled elements at once, so you won’t have to do it manually, element by element.

We can define styles for the following:

<ul>
  <li><a href="#text-styles">Text</a></li>
  <li><a href="#color-styles">Colors</a></li>
  <li><a href="#effects">Effects</a></li>
  <li><a href="#grids">Grids</a></li>
</ul>

If you have variations of the same style, to make it easier to find them later, you can name the single styles and arrange them inside the panel as groups. To do so, just use this formula:

<blockquote>Group Name/Style Name</blockquote>

I’ve included a suggestion of how to name texts and colors styles below.

#### Text Styles

Properties that you can define within a text style:

<ul>
  <li>Font size</li>
  <li>Font weight</li>
  <li>Line-height</li>
  <li>Letter spacing</li>
</ul>

**Tip**: *Figma drastically reduces the number of styles that we need to define in the library, as alignments and colors are independent of the style. You can combine a text style with a color style in the same text element.*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed77a04d-8689-4e00-be3a-3afe8db10c87/text-styles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed77a04d-8689-4e00-be3a-3afe8db10c87/text-styles.png" sizes="100vw" caption="You can apply all the typography scale we’ve seen before as text styles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed77a04d-8689-4e00-be3a-3afe8db10c87/text-styles.png'>Large preview</a>)" alt="4 shapes with text inside used as examples of different text styles" >}}

**Text Styles Naming**

I recommend using a naming rule such as “Size/Weight”<br />*(eg: 16/Regular, 16/SemiBold, 16/Bold).*

Figma only allows one level of indentation, if you need to include the font you can always add a prefix before the size:<br />**FontFamily Size/Weight** or **FF Size/Weight**<br />*(eg: **SourceSansPro 16/Regular** or **SSP 16/Regular**).*

#### Color Styles

The color style uses its hex value (`#FFF`) and the opacity as properties.

**Tip**: *Figma allows you to set a color style for the fill and a different one for the border within the same element, making them independent of each other.*

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb60ddc-0053-4d49-9d11-570cb75c945a/color-styles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb60ddc-0053-4d49-9d11-570cb75c945a/color-styles.png" sizes="100vw" caption="You can apply color styles to fills, borders, backgrounds, and texts. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb60ddc-0053-4d49-9d11-570cb75c945a/color-styles.png'>Large preview</a>)" alt="4 shapes with colors inside, used as examples of different color styles" >}}

**Color Styles Naming**

For a better organization I recommend using this rule “Color/Variant”. We named our color styles using “Primary/Default” for the starter color, “Primary/L1”, “Primary/L2” for lighten variants, and “Primary/D1”, “Primary/D2" for darken variants.

#### Effects

When designing an interface you might also need to create elements that use some effects such as drop shadows (the drag&drop could be an example of a pattern that uses drop shadows effects). To have control over these graphic details, you can include effect styles such as shadows or layer blurs to the library, and also divide them by groups if necessary.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cb8acb4-ae86-4ca5-ae78-1685cbca3129/effect-styles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cb8acb4-ae86-4ca5-ae78-1685cbca3129/effect-styles.png" sizes="100vw" caption="Define shadows and blurs to manage special interaction effects such as drag-n-drop. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cb8acb4-ae86-4ca5-ae78-1685cbca3129/effect-styles.png'>Large preview</a>)" alt="2 shapes similar to paper, one above the other one to show the shadow effect" >}}

#### Grids

To provide something very useful for your team, include the grid styles. You can define the 8px grid, 12 columns grid, flexible grids so your team won’t need to recreate them.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29eed154-97b4-4805-9c7e-33ae30b7a799/grid-styles.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29eed154-97b4-4805-9c7e-33ae30b7a799/grid-styles.png" sizes="100vw" caption="There’s no need to memorize the grid sizes anymore. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29eed154-97b4-4805-9c7e-33ae30b7a799/grid-styles.png'>Large preview</a>)" alt="12 columns to represent the grid styles" >}}

**Tip**: *Taking advantage of this feature, you can provide all the different breakpoints as ‘grid styles’.*

## Master Component

Figma lets you generate multiple instances of the same component and update them through a single master component. It’s easier than you might think, you can start with some small elements and then use them to evolve your library.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a18738d-125a-4515-8fb0-6e7937b4fa9d/master-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a18738d-125a-4515-8fb0-6e7937b4fa9d/master-component.png" sizes="100vw" caption="One master component to rule them all! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a18738d-125a-4515-8fb0-6e7937b4fa9d/master-component.png'>Large preview</a>)" alt="a single group of three shapes that shows how you can get seven different results by hiding some of the shapes" >}}

To explain this workflow better, I will use one of the basic components all the libraries have: the buttons.

### Buttons!

Every system has different types of buttons to represent the importance of the actions. You can start having both primary and secondary buttons with only texts and one size, but the reality is that you’ll probably end up having to maintain something like this:

<ul>
<li>2 color types (<em>Primary</em> | <em>Secondary</em>)</li>
<li>2 sizes of buttons (<em>Regular</em> | <em>Small</em>)</li>
<li>4 content types (<em>Text Only</em> | <em>Icon Only</em> | <em>Text</em> + <em>Icon right</em> | <em>Icon Left</em> + <em>Text</em>)</li>
<li>5 states (<em>Default</em> | <em>Hover</em> | <em>Active</em> | <em>Disabled</em> | <em>Focus</em>)</li>
</ul>

This would give us up to 88 different components to maintain only with the set of buttons mentioned above!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2375e5a6-e964-4ffc-99d7-3e1bc4d1dc26/buttons.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2375e5a6-e964-4ffc-99d7-3e1bc4d1dc26/buttons.png" sizes="100vw" caption="Thanks to how Figma is built, you can easily manage a lot of button instances all at once. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2375e5a6-e964-4ffc-99d7-3e1bc4d1dc26/buttons.png'>Large preview</a>)" alt="a screenshot with a total of 88 different button components" >}}

## Let’s Start Step By Step

The first step is to include all the variations together in the same place. For the buttons we’re going to use:

<ul>
<li>A single shape for the background of the button so that we can then place the color styles for the fill and the border;</li>
<li>The single text that will have both text and color styles;</li>
<li>Three icon components (positioned to the right, center and left) filled in with the color style (you will be able to easily swap the icons).</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154c5fef-860e-4e3f-812e-ef9cc738b2d8/single-elements.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154c5fef-860e-4e3f-812e-ef9cc738b2d8/single-elements.png" sizes="100vw" caption="A shape, a text, and an icon walk into a Figma bar... (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154c5fef-860e-4e3f-812e-ef9cc738b2d8/single-elements.png'>Large preview</a>)" alt="a group of divided elements: a rectangle shape, a button text and 3 icons" >}}

The second step is to create the master component (use the shortcut <kbd>Cmd</kbd> + <kbd>Alt</kbd> + <kbd>K</kbd> on Mac, or <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>K</kbd> on Windows) with all of the variations as instances. I suggest using a different and neutral style for the elements inside the master component and use the real styles on the sub-components, this trick will help the team use only sub-components.

You can see the visual difference between a master component and a sub-component in the next step:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/481a8216-63ac-4621-bb45-7ab501e00d5a/group-of-elements.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/481a8216-63ac-4621-bb45-7ab501e00d5a/group-of-elements.png" sizes="100vw" caption="The more elements, the more instances you can control. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/481a8216-63ac-4621-bb45-7ab501e00d5a/group-of-elements.png'>Large preview</a>)" alt="A group of elements centered in the same space, one over the other one" >}}

In the third step you need to duplicate the master component to generate an instance, now you can use that instance to create a sub-component, and from now on every change you make to the master component will also change the sub-component you’ve created.

You can now start applying the different styles we’ve seen before to the elements inside the sub-component and, of course, you can hide the elements you don’t need in that sub-component.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034f2cef-5f40-442d-9e2e-af91a897ed19/buttons-master.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034f2cef-5f40-442d-9e2e-af91a897ed19/buttons-master.png" sizes="100vw" caption="Thanks to the color styles you can generate different components using the same shape. In this example, primary and secondary styles are generated from the same master component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034f2cef-5f40-442d-9e2e-af91a897ed19/buttons-master.png'>Large preview</a>)" alt="An example showing how 8 different buttons can be generated from 1 single component" >}}

### Text Alignment

As I’ve shown you in the styles, the alignments are independent of the style. So if you want to change the text alignment, just select it by hitting <kbd>Cmd</kbd>/<kbd>Ctrl</kbd> and changing it. Left, center or right: it will all work and you can define different sub-components as I did with the buttons.

**Tip**: *To help you work faster without having to find the exact element layer, if you delete an element inside the instance, it will hide the element instead of actually deleting it.*

{{% ad-panel-leaderboard %}}

## Component Organization

If you’re coming from Sketch, you could be having trouble with the organization of the components in Figma as there are a few key differences between these two tools. This is a brief guide to help you organize the components well so that the instance menu doesn’t negatively affect your team’s effectiveness.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ee79a6-a29f-4935-a347-c60f9f0260c0/before-mess.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ee79a6-a29f-4935-a347-c60f9f0260c0/before-mess.png" sizes="100vw" caption="As you can see here, our library had so many sub-menus that as a result the navigation was going off the screen on MacBooks, that was a big problem for our library. We were able to find a workaround for this issue. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ee79a6-a29f-4935-a347-c60f9f0260c0/before-mess.png'>Large preview</a>)" alt="showing the instance menu open with more unordered sub-menus" >}}

{{< rimg breakout="true"href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/265ea746-f7b0-472d-9d83-b863466f6786/after-order.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/265ea746-f7b0-472d-9d83-b863466f6786/after-order.png" sizes="100vw" caption="This was the result after improving the library order following the rules for pages and frames, now it’s way more usable and organized for our teams. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/265ea746-f7b0-472d-9d83-b863466f6786/after-order.png'>Large preview</a>)" alt="showing the improvements on the instance menu open with ordered sub-menus" >}}

We’ve all been there, the solution is easier than you think!

Here’s what I have learned about how to organize the components.

### Figma Naming

While in Sketch all the organization depends only on the single component name, in Figma it depends on the *Page* name, the *Frame* name, and the single *Component* name &mdash; exactly in that order.

In order to provide a well-organized library, you need to think of it as a visual organization. As long as you respect the order, you can customize the naming to fit your needs.

Here’s how I’ve divided it:

<ul>
<li>File Name = Library Name (e.g. Lexicon);</li>
<li>Page Name = Component Group (e.g. Cards);</li>
<li>Frame Name = Component Type (e.g. Image Card, User Card, Folder Card, etc);</li>
<li>Component Name = Component State (e.g. Default, Hover, Active, Selected, etc).</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08170474-73db-474e-bc3e-383c86034831/cards-layers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08170474-73db-474e-bc3e-383c86034831/cards-layers.png" sizes="100vw" caption="This structure is the equivalent to the Sketch naming of ‘Cards/Image Card/Card Hover’. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08170474-73db-474e-bc3e-383c86034831/cards-layers.png'>Large preview</a>)" alt="Showing the main page named ‘Cards’, the frame named ‘Image Card’ and the layer named ‘Card Hover’" >}}

### Adding Indentation Levels

When creating the Lexicon library, I found that I actually needed more than three levels of indentation for some of the components, such as the buttons that we saw before.

For these cases, you can extend the naming using the same method as Sketch for nested symbols (using the slashes in the component name, e.g. “Component/Sub-Component”), under the condition that you do it only *after* the third level of indentation, respecting the structural order of the first three levels as explained in the previous point.

This is how I organized our buttons:

<ul>
<li>Page name = Component Group (e.g. Buttons);</li>
<li>Frame name = Component Size (e.g. Regular or Small);</li>
<li>Component name = Style/Type/State (e.g. Primary/Text/Hover).</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577a068b-5e96-48cd-8a94-1cf6f1c38c24/buttons-layers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577a068b-5e96-48cd-8a94-1cf6f1c38c24/buttons-layers.png" sizes="100vw" caption="This structure is the equivalent to the Sketch naming of '*Buttons/Buttons Regular/Primary/Text/Button Hover*'. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577a068b-5e96-48cd-8a94-1cf6f1c38c24/buttons-layers.png'>Large preview</a>)" alt="Showing the main page named 'Buttons', the frame named 'Buttons Regular' and the layer named 'Primary/Text/Button Hover' as example of the possible structures." >}}

**Tip**: *You can include the component name (or a prefix of the name) in the last level, this will help your team to better identify the layers when they import the components from the library.*

### Icons Organization

Organizing the icons in Figma can be challenging when including a large number of icons.

As opposed to Sketch which uses a scroll functionality, Figma uses the sub-menus to divide the components. The problem is that if you have a large number of icons grouped in sub-menus, at some point they might go off screen (my experience with Figma on a MacBook Pro).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f4d7dba-6199-4d08-b6df-37a646ce5386/sketch-icons-menu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f4d7dba-6199-4d08-b6df-37a646ce5386/sketch-icons-menu.png" sizes="100vw" caption="An example of how the components are organized inside a single scrollable sub-menu. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f4d7dba-6199-4d08-b6df-37a646ce5386/sketch-icons-menu.png'>Large preview</a>)" alt="Showing the instance menu for the icons with a single scrollable sub-menu." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7676eb6e-09fe-4be1-8aca-0921a1675c3f/figma-icons-menu.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7676eb6e-09fe-4be1-8aca-0921a1675c3f/figma-icons-menu.png" sizes="100vw" caption="As you can see, using a Macbook Pro the result was the menus going outside the screen. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7676eb6e-09fe-4be1-8aca-0921a1675c3f/figma-icons-menu.png'>Large preview</a>)" alt="Showing the instance menu for the icons with more than 10 sub-menus and cover all the screen." >}}

Here are two possible solutions:

- **Solution 1**  
Create a page named “Icons” and then a frame for each letter of the alphabet, then place each icon in the frame based on the icon’s name. For example, if you have an icon named “Plus”, then it will go in the “P” frame.
- **Solution 2**  
Create a page named “Icons” and then divide by frames based on the icon categories. For example, if you have icons that represent a boat, a car, and a motorcycle, you can place them inside a frame named “vehicles”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a6a8524-9cc2-4367-b925-d7937bc994fa/ordering-icons.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a6a8524-9cc2-4367-b925-d7937bc994fa/ordering-icons.png" sizes="100vw" caption="I, personally, applied solution 1. As you can see in this example, we had a huge number of icons so this was the better fit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a6a8524-9cc2-4367-b925-d7937bc994fa/ordering-icons.png'>Large preview</a>)" alt="The instance menu is open, showing the alphabetical order of the icons in Figma." >}}

## Conclusion

Now that you know what’s exactly behind a team’s library construction in Figma, you can start building one yourself! Figma has a free subscription plan that will help you to get started and experiment with this methodology in a single file (however, if you want to share a team library, you will need to subscribe to the “Professional” option).

Try it, create and organize some advanced components, and then present the library to your team members so you could amaze them &mdash; or possibly convince them to add Figma to their toolset.

Finally, let me mention that here in Liferay, we love open-source projects and so we’re sharing a copy of our [Lexicon library ](https://liferay.design/resources/figma/) along with some other resources. You can use the Lexicon library components and the other resources for free, and your feedback is always welcome (including as Figma comments, if you prefer).

- [Download the ‘Lexicon’ library](https://liferay.design/resources/figma/)

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0077e33c-f7a6-4a5b-81d9-fb76f0b88abf/lexicon.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0077e33c-f7a6-4a5b-81d9-fb76f0b88abf/lexicon.png" sizes="100vw" caption="Lexicon is the design language of Liferay, used to provide a Design System and a Figma Library for the different product teams. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0077e33c-f7a6-4a5b-81d9-fb76f0b88abf/lexicon.png'>Large preview</a>)" alt="The Lexicon logo, it’s similar to a hexagon and a fingerprint together." >}}

If you have questions or need help with your first component library in Figma, ask me in the comments below, or [drop me a line on Twitter](https://twitter.com/@EmilianoGCicero).

### Further Resources

<ul>
  <li>“<a href="https://medium.freecodecamp.org/8-point-grid-typography-on-the-web-be5dc97db6bc?ref=heydesigner">8-Point Grid: Typography On The Web</a>,” Elliot Dahl, freeCodeCamp</li>
<li><a href="https://blog.prototypr.io/defining-a-modular-type-scale-for-web-ui-51acd5df31aa?ref=heydesigner">Defining A Modular Type Scale For Web UI</a>,” Kelly Dern, Medium</li>
<li>“<a href="https://seesparkbox.com/foundry/relative_color_palettes_with_sass">Relative Color Palettes With Sass</a>,” Ethan Muller, Sparkbox</li>
  <li><a href="https://sassme.jim-nielsen.com">SassMe</a> (tool created by Jim Nielsen that lets you visualize Sass HSL color functions in real-time)</li>
<li>“<a href="https://css-tricks.com/what-do-you-name-color-variables/?ref=heydesigner">What Do You Name Color Variables?</a>,” Chris Coyier, CSS-Tricks</li>
<li>“<a href="https://www.figma.com/blog/component-styles-and-shared-library-best-practices/">Best Practices: Components, Styles, And Shared Libraries</a>,” Thomas Lowry, Figma</li>
  <li><a href="https://www.youtube.com/channel/UCQsVmhSa4X-G3lHlUtejzLA">Figma YouTube Channel</a></li>
  <li><a href="https://help.figma.com/collection/6-figma">Figma Help Articles</a></li>
</ul>

{{< signature "mb, yk, il" >}}
