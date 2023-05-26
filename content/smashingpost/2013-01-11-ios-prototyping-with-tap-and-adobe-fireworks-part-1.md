---
title: iOS Prototyping With TAP And Adobe Fireworks (Part 1)
slug: ios-prototyping-with-tap-and-adobe-fireworks-part-1
image: >-
  https://www.smashingmagazine.com/wordpress/2013/10/09/conversion-rate-optimization-for-wordpress/attachment/kiss-landingpage-500px/attachment/cooper-3stages-1/
date: 2013-01-11T12:00:36.000Z
author: shlomo-goltz
summary: >-
  One of the strengths of Adobe Fireworks lies in its ability to produce <a href="https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/">basic-level prototypes</a> in HTML format for the purpose of sharing concepts, evaluating them and conducting usability tests. But did you know that you can use Fireworks in combination with other tools to create complex iOS prototypes (for both the iPhone and iPad) with similar ease?
description: >-
  Did you know that you can use Fireworks in combination with other tools to create complex iOS prototypes (for both the iPhone and iPad) with similar ease?
categories:
  - Fireworks
  - Tutorials
  - Prototyping
  - iOS
---
In this series of three articles, you’ll learn how to use Adobe Fireworks together with another tool, called <a title="TAP (Touch Application Prototypes)" href="https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/">TAP</a>, to create prototypes with animated transitions. The process is fairly straightforward, but because there are many properties and features one can tweak to enhance a prototype, I have separated the content into three parts:

1.  In **part one**, I’ll shed some light on the major stages of the design process that projects at [Cooper](https://www.cooper.com/) go through — Fireworks plays an important role during all of these stages. Next, I’ll talk about my preferred method of organizing Fireworks PNGs, which will be important later and will serve as the basis for the next part of the tutorial.
2.  In [part two](https://www.smashingmagazine.com/2013/01/ios-prototyping-with-tap-and-adobe-fireworks-part-2/), I’ll speak in detail about the use of pages, hotspots, gestures, transitions and timers and how to set them up for use with TAP. Then, I’ll show you how to start building a click-through prototype in Fireworks, which will later be converted into an interactive iOS prototype.
3.  In [part three](https://www.smashingmagazine.com/2013/02/15/ios-prototyping-adobe-fireworks-tap-part3/), the conversion to a TAP iOS prototype will be covered in detail. I will also share some tips on its use on iOS devices. You’ll get all of the demo files needed to complete the tutorial, as well as an extensive list of related resources on Fireworks and prototyping.

## Introduction

There has been an explosion of prototyping applications that claim to be mobile-centric, but few actually focus on the core differentiators of the modern mobile experience: <strong>gestures and transitions</strong>. One design tool that I have come to rely on for iOS prototyping is <strong>Adobe Fireworks</strong> — an application that has received a bit less attention from the design community. However, Fireworks is a powerful, extremely efficient and extensible program that has many indispensable features that cannot be found anywhere else. (Check out a couple of articles on <a href="https://www.smashingmagazine.com/2010/09/17/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/">what it can do</a> and <a href="https://medialoot.com/blog/fireworks-for-beginners/">what makes it unique</a> for details on what makes Fireworks so special.)

With <a href="https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/">TAP</a> (a free extension), you can transform Fireworks from a general wireframing application into an iOS prototyping powerhouse. Let’s find out how!

{{% feature-panel %}}

## How Fireworks Is Used At Cooper

As an intern at <a href="https://www.cooper.com/">Cooper</a> in the summer of 2011, I learned how to use Adobe Fireworks to make both interactive prototypes and polished visual designs. The versatility of Fireworks meant that everyone on the team could easily share files back and forth during a project.

Interaction designers use Fireworks as the digital equivalent of a <strong>refined sketching tool</strong>. More flexible than pen and paper (when using shared layers, symbols and styles), Fireworks retains the fast and direct nature of drawing but with a higher fidelity than pen and paper or a whiteboard. This technique is very useful early in the design process when many major decisions are still being evaluated. Many other tools for wireframing are out there that include libraries of UI components, but Fireworks is one of the only wireframing applications that also has robust <strong>illustration and design capabilities</strong> that can be used to create original content. This is one of the most overlooked benefits of Fireworks, because it increases the likelihood that you will come up with an original design that is tailored to the problem(s) you are designing a solution for.

### Our Tool of Preference for Both Interaction Design and Visual Design

In the article “<a title="Designing interactive products with Fireworks" href="https://www.adobe.com/devnet/fireworks/articles/cooper_interactive.html">Designing Interactive Products With Fireworks</a>,” published on <a title="Adobe Devnet - Fireworks section" href="https://www.adobe.com/devnet/fireworks.html">Adobe Developer Connection</a>, Nick Myers (previously principal visual designer at Cooper, and now managing director, design services) shares his thoughts about the design process and how Fireworks fits into the various stages:
<blockquote>"At Cooper, we design a wide variety of interactive products for platforms, including the desktop, the web, and mobile devices. Our design teams are small and usually consist of an interaction designer, design communicator, visual designer and, if there is a hardware component, industrial designer. The interaction designer and design communicator work together to design and document the behavior of the interface, while the visual designer is responsible for the interface’s visual appearance. The industrial designer handles the physical form factor of hardware. Finally, the team is managed by an engagement lead who designs the engagement and provides guidance and direction to the team.

During the solution-creation phases of a typical project, a design team begins storyboarding scenarios on whiteboards and then transfers these sketches to the screen, where they are iterated and refined over and over. The design is then documented for our clients to follow and reference as they build their products.

After the big ideas are generated, the interaction designer quickly transfers his work to Adobe Fireworks where the details are added to the product. Other design groups or firms may use one tool, like Visio or OmniGraffle, for interaction design and another, like Photoshop, for visual design, but we have learned over the years that <strong>working in Fireworks throughout the design process has many benefits</strong>.

First, it encourages our teams to be more collaborative as we pass our work back and forth and solve problems together. We also work much faster, as we don’t have to recreate elements or check our work against each other’s files. Finally, it reduces mistakes during design, as we aren’t managing multiple versions of files."</blockquote>

(You can also <a href="https://tv.adobe.com/watch/fireworks-tips-and-tricks/cooper/">watch a video</a> on the same subject, in which Tim McCoy and Nick Myers discuss how they use Adobe Fireworks for interaction and visual design.)

In another article, “<a title="Industry trends in prototyping" href="https://www.adobe.com/devnet/fireworks/articles/cooper_prototyping.html">Industry Trends in Prototyping</a>,” Dave Cronin (previously director of interaction design at Cooper and now at General Electric) shares more about the role of Fireworks at Cooper:
<blockquote>"While pen and paper can be a perfect medium for creating storyboards, we’ve found that the combination of a Wacom tablet and Adobe Fireworks allows us to work even more quickly and efficiently. At Cooper, we use Fireworks as our primary screen rendering and production tool for work from sketch to final graphic assets.

To create a sketchy storyboarded scenario in Fireworks, we typically rely on the States panel to represent each state in the scenario. We use layers, shared across states, and symbols to reuse screen elements, eliminating the need to draw the same thing over and over again."</blockquote>

## Cooper’s Project Workflow

For most projects at Cooper, the following are the four major stages of the design process. (Technically, there are many more — such as primary research, competitive analysis and persona development — but they are beyond the scope of this series of articles.)

1.  Framework drawing,
2.  Framework wireframing,
3.  Detailed visual design,
4.  iOS prototyping with Fireworks.

### Stage 1: Framework Drawing

The framework drawing (or sketch) is a high-level depiction of the main underlying concept and supporting structure that the whole design is based on. <strong>Lack of detail is intentional</strong> in order to elicit a broader scope of feedback from stakeholders.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5802c435-45f5-4cd0-8038-b1d4b3ac1247/cooper-3stages-1.jpg" alt="Cooper: four stages of solution evolution" width="500" height="395" /><br>
<em>Framework drawing stage</em>

### Stage 2: Framework Wireframing

The framework wireframe is a refined digital depiction of the framework that is used to further clarify and iterate on ideas from previous sketches. While key features may be explored at this stage, <strong>excessive detail is avoided</strong> so that stakeholders are not distracted by elements that haven’t yet been completely thought out. Renderings of the wireframe have a “pencil sketch” style and are not too polished, in order to elicit a moderate level of feedback from stakeholders.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b87c9b0-d9e7-45ae-9b48-902748e4b5a9/cooper-3stages-2.jpg" alt="Cooper: four stages of solution evolution" width="500" height="365" /><br>
<em>Framework wireframing stage</em>

### Stage 3: Detailed Visual Design

The detailed visual design is a fully rendered, detail-oriented, fleshed-out depiction of what the interface will look and feel like when the design is finished and in the hands of users. At this final stage, brand attributes are added to determine color, typography, iconography and other visual properties.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b02ab193-46ed-4633-9456-eed48776895c/cooper-3stages-3.jpg" alt="Cooper: four stages of solution evolution" width="500" height="365" /><br>
<em>Detailed visual design (visual rendering) stage</em>

In the later stages of the design process, Fireworks can turn the wireframes into fully rendered, production-ready graphics. And by adding hotspots to each page in a Fireworks document, non-linear navigation can be simulated, and click-through wireframes can be used to test and share the design flow.

### Stage 4: Extending Fireworks To Create iOS Prototypes

On its own, Fireworks can be used as a <a title="Interactive Prototypes and Time-Savers with Adobe Fireworks (an article by Trevor Kay)" href="https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/">simple wireframing tool with linking capabilities</a> — far different from the more robust prototyping tools that can accurately demonstrate more complex or nuanced interactions, especially ones that involve animated transitions.

Luckily for designers, some very smart people at UNITID (based in the Netherlands) have developed <a href="https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/">Touch Application Prototypes</a> (TAP), a utility that enables you to design in Fireworks and, with almost no coding, convert the design into an animated prototype that responds to particular gestures.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0125a03a-45c2-4613-86f3-67b6858e6443/tap-and-fireworks.png" alt="Touch Application Prototypes and Adobe Fireworks combined" width="500" height="120" /><br>
<em>TAP and Fireworks are all you need to create animated prototypes that respond to gestures.</em>

Best of all, you can experience the prototype right on any iOS device! Seeing your prototype respond to your touch and animate in real time is a satisfying and immersive experience, and the experiential learning and exploration can elicit a new understanding of the prototype.

### Why Animated Transitions and Gestures Matter

Thanks to the proliferation of touch interactions, animations have become essential characteristics of the mobile experience, and they are even beginning to influence the desktop as well (as can be seen in <a href="https://www.apple.com/osx/">Mac OS X Lion</a> and <a href="https://windows.microsoft.com/en-US/windows-8/meet">Windows 8</a>). Animated transitions provide useful feedback; they help visualize the results of actions taken; and they enhance the sense of direct manipulation. For more information on how essential transitions are to the mobile touch experience, check out Greg Nudelman’s article “<a href="https://boxesandarrows.com/view/storyboarding-ipad">Storyboarding iPad Transitions</a>.” Gestures help to make a prototype feel like a native application and can help designers evaluate a product’s effectiveness, something that’s becoming more critical as chrome disappears and affordances become less visible. For a taxonomy of gestures used for mobile, check out Luke Wroblewski’s “<a href="https://www.lukew.com/ff/entry.asp?1071">Touch Gesture Reference Guide</a>.” Much can be learned from using and testing animated and gesture-based prototypes.

{{% ad-panel-leaderboard %}}

## Laying The Foundation: Fw PNG Organizational Framework

Fireworks’ framework for file organization will play a very important role later, so let’s take a good look at it.

As with any powerful design tool, there are many ways to use Fireworks. The way in which we at Cooper organize Fireworks files (or Fw PNGs) has evolved over time. The organizational methodology that we’ll cover in this article enables designers to create intricate scenario-based wireframes that can be exported as interactive HTML prototypes or demos that allow observers to see and evaluate the merits of a design.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91230810-5dce-4f7a-b6e6-631f8fb49f74/fwelementhierarchy.png" alt="Fireworks elements' hierarchy" width="500" height="140" /><br>
<em>How Fw PNG files are organized: pages contain states, states contain layers, layers contain objects.</em>

### Pages

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50c6c0e1-836a-419b-965b-3c88a72e55ec/iconpages.png" alt="Pages icon" width="84" height="100" />

Each Fireworks PNG file can contain many pages, which are used to represent the various stages in a scenario and which build on one another.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29df4bb3-59f9-411a-a874-4ed0da56c100/pages-panel.png" alt="Pages Panel" width="500" height="245" /><br>
<em>Pages in Fireworks: a brief interaction example that contains three pages.</em>

In the example above, on page 1 the user types in their name; on page 2 the user types in their password; and on page 3 the user clicks the log-in button.

<strong>Note:</strong> Although states may be used to create rollovers and other interactive behaviors, they are not generally used in wireframes that are designed according to the methodology followed in this article. For more on how to use pages and states in Fireworks, check out Dave Hogue’s detailed article “<a href="https://www.adobe.com/devnet/fireworks/articles/pages_states_layers.html">Using Pages, States, and Layers in Fireworks CS4</a>.”

When you use pages as the primary way of organizing a scenario, you are able to export the work as a prototype consisting of HTML and images, where each page can be linked to others through hotspots. This HTML prototype allows anyone with a browser to experience your work in a way that is interactive and that replicates the feel of a real application. Non-linear and branching scenarios may be set up with multiple hotspots per page and can really make a project come alive.

### Shared Layers

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b402709-42c9-4562-a142-6fa28d3e1baa/iconsharelayertopages.png" alt="Share to Layers icon" width="84" height="100" />

You can use layers to organize the visuals shown on each page by controlling the stacking order of elements. Layers may be shared to pages when those pages must contain the same visuals. Sharing a layer is more versatile and efficient than merely copying and pasting objects from page to page because shared layers maintain consistency. This is a huge time-saver because common elements that appear across many pages can be <strong>changed once and updated across the entire project</strong> in one click! Share a layer if you want the same objects to appear across pages consistently (known as “object persistence”). Two commands are used to share layers: “Share Layer to Pages” and “Share Layer to All Pages.”

<strong>How to share layers to specific pages:</strong>

First, select the layer that you want to share in the Layers panel. Then, right-click (or Command + click on a Mac), and select the option “Share Layer to Pages.”

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26e16dd3-3aa2-4e51-bdce-1bce6c503b0b/sharelayersmenu.png" alt="Share Layers context menu" width="500" height="768" /><br>
<em>The contextual menu in the Layers panel lets you share layers to specific pages or to all pages in a document.</em>

A dialogue box will appear with two selection lists: the one on the left lists the pages that this layer is <em>not</em> shared with (named “Exclude layers from page(s)”), and the one on the right (named “Include layer from page(s)”) lists the pages that this layer <em>is</em> shared with. To share a layer to more pages, select the pages you want to share to in the left column (you can select multiple pages by pressing Control/Command + click), and click the “Add &gt;" button to move the pages to the list on the right.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7f81c11-b31d-4172-a512-2193fd322ae3/sharelayertopagesdualpicklist.png" alt="Share Layer to specific Pages dialogue box" width="500" height="400" /><br>
<em>The “Share Layer to (Specific) Pages” dialogue box controls which pages a layer is shared to. Note that there are no previews here, so naming your layers well is key.</em>

Sharing a layer to pages can be done and undone by selecting the “Share Layer to Pages” option and moving pages to and from the “Exclude layers from page(s)” and “Include layers from page(s)” lists.

<strong>Note:</strong> The stacking order of shared layers is controlled <strong>per page</strong>. The order of layers on a page may be unique and changed as needed without affecting other pages that share those same layers. This ability to change layer stacking per page is a <strong>powerful feature</strong> in Fireworks and makes it possible to draw multiple versions, modes and states of an interface just once on multiple layers, share those layers, and then choose which version is shown on each page simply by rearranging the layers.

{{% ad-panel-leaderboard %}}

<strong>How to share layers to all pages:</strong>

Use the same process as for “Share Layer to Pages,” but this time selecting the option “Share Layer to All Pages.” This command ensures that whenever a new page is created, it will not be a blank slate — those layers (and their contents) will be copied over automatically. When a single layer is shared to all pages, it will appear at the top of the layer stack.

When multiple objects within a layer are selected and then collectively shared to all pages, the stacking order of layers on newly created pages is different than the stacking order when the layers were created on the original page. The stacking order of layers is not always predictable and will not reflect the stacking order on the page you are sharing from; this seems to be a limitation (or a bug?) in Fireworks CS5. By comparison, in Fireworks CS6, the stacking order of objects within a layer is much more likely to be respected and maintained throughout a document.

<strong>Note:</strong> Be careful when using the “Share Layer to All Pages” command because there is no global “unshare layers” command. Once a layer has been shared to all pages, it will be automatically included (or shared) on every new page you create. You can manually unshare it from all pages in the document by using the “Share Layer to Pages” option and removing all of the shared pages. As long as “Share Layer to All Pages” remains checked in the menu, then all new pages will inherit that layer; if you uncheck “Share Layer to All Pages,” then all pages already sharing that layer will retain the shared layer, but any new pages created will not inherit that layer.

Here’s a brief example. If you create a layer on page 1, share it to all pages, and then go to page 5 and right-click on the shared layer, you can “detach” or “exclude” that shared layer from page 5. The “Detach” option will make a copy of the shared layer and break the connection with the original (similar to breaking off a symbol), without affecting the original or any other page. The “Exclude” option will remove the shared layer from the current page without affecting the original or any other page.

### Symbols

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/077fb562-aa00-4ac6-923e-266e3a128b57/iconsymbols.png" alt="Symbols icon" width="84" height="100" />

A symbol in Fireworks is a special kind of <strong>reusable graphic element</strong> — think of it as a <strong>master version</strong> of a graphic. Use a symbol whenever you will be repeatedly using a graphic, such as a logo. The advantage is that copies of a symbol (called symbol “instances”) will all be linked to the original; so, when properties of the original instance are changed, the other instances will change automatically.

Instances of symbols can be transformed (including by scaling, skewing, distorting and rotating) without affecting the original or other instances, and they may be given different properties (i.e. different from one another and from the original symbol):

*   Transformations (scale the size, skew or distort the shape, and rotate the object);
*   x and y coordinates (location on page);
*   Blending modes;
*   Opacity;
*   Apply live filters.

When a symbol is created, it is placed in the “<strong>Document Library</strong>.” The Document Library panel gives an overview of all symbols used in the current document. You can find symbols that you have already created there, and you can drag and drop them onto the canvas to create new instances.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da4a9615-5ea9-46bb-94a2-b6b0a2cf41eb/documentlibrary.png" alt="The Document Library panel in Fireworks" width="500" height="362" /><br>
<em>The Document Library panel</em>

Symbols may also be saved to the “Common Library” and, thus, made available for global use in Adobe Fireworks.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f620d7f-1874-4a2e-a0c4-ac3db8ce3008/commonlibrary.png" alt="The Common Library panel in Fireworks" width="500" height="362" /><br>
<em>The Common Library panel</em>

To save a symbol to the Common Library, select it in the Document Library panel and use the “Save to Common Library” option in the panel’s menu. Later, whole collections (or libraries) of symbols can be easily shared between designers on the team.

<strong>Why not turn every object into a symbol?</strong>

If symbols are so cool and offer so much power, you may be wondering, why not make everything a symbol? The answer is that if an object won’t be used repeatedly, there is no added benefit of making it a symbol; in fact, it would make your workflow slower, for two reasons. First, in order to edit the master symbol, you would usually enter a special “edit symbol” mode (similar to single layer editing), which slows down the workflow. Secondly, all symbols are listed in the Document Library panel, and this panel would soon become full of symbols, making file management difficult.

Because symbols are not the main topic of this article, I’ll simply refer you to the following resources:

*   “[Symbols](https://help.adobe.com/en_US/fireworks/cs/using/WS4c25cfbb1410b0021e63e3d1152b00db4b-7fd4.html "Symbols Overview"),” Adobe Fireworks Help
*   “[Editing Specific Symbol Instances](https://help.adobe.com/en_US/fireworks/cs/using/WS4c25cfbb1410b0021e63e3d1152b00db4b-7fd9.html "editing symbol instances"),” Adobe Fireworks Help
*   “[Understanding Styles and Symbols](https://www.adobe.com/designcenter-archive/fireworks/articles/lrvid4033_fw.html "Understanding styles and symbols")” (video tutorial), Jim Babbage

### Styles

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4b2543b-fe46-4b0b-a50f-734e61709c81/iconobjectstyles.png" alt="Object Styles icon" width="84" height="100" />

Just like in InDesign, Styles in Fireworks allow for the consistent application of fills, strokes, live filters and other styling properties. When a style is changed, objects with that style are automatically updated, too, similar to how global CSS styles work in HTML documents.

(Object) styles are perfect for when you want to create a consistent visual language in a design and want to be able to update the look and feel easily.

Let’s suppose you want to explore three variations of a button set design in an interface.

At the beginning of the design process, you would place the buttons on the canvas and apply a pencil-sketch style to them (so that the buttons don’t look too polished at this early stage of the project). Once the pencil look is achieved through various filters and effects, you can save the look as a style.

<strong>Note:</strong> Saving a new style in Fireworks is easy. Select the object with the style that you want to save, and then click on the “New Style” button in the bottom-right corner of the “Styles” panel. Or, alternatively, use the “New Style” option, accessible in the “Properties” panel (also known in Fireworks as the Property Inspector (PI) panel).

Later on, when the design is more refined, you might want an OS X aqua look. Because you are using styles, there is no need to redraw the buttons! To convert the design from a pencil-sketch look, select the button you want to modify, alter its visual properties to appear more glossy and fluid, and then click the “New Style” button. Repeat these steps to create a third style based on, say, a plastic-y Web 2.0 look. You can apply the three different styles to any button from now on! If you modify the style itself, all objects with that style will update as well.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4195da60-3f5d-4863-b36e-8c87d67a4716/stylesexampleandpanel.png" alt="Example of using Styles with the Styles panel" width="500" height="647" /><br>
<em>The Styles panel is used to create new styles and apply existing ones. Update a style in the panel and all objects with that style will update throughout the entire document.</em>

With the help of the Styles panel, you can also duplicate, delete, rename and redefine styles, break a link to a style, import or export whole style libraries, and more.

Because styles are a powerful feature on their own, I’ll refer you to Jim Babbage’s video tutorial “<a href="https://www.adobe.com/designcenter-archive/fireworks/articles/lrvid4033_fw.html">Understanding Styles and Symbols in Fireworks</a>.”

## Conclusion

Now that you understand the fundamental components of Fireworks (pages, shared layers, symbols and styles), let’s explore how you can use them to start building your own prototype!

In the <a href="https://www.smashingmagazine.com/2013/01/ios-prototyping-with-tap-and-adobe-fireworks-part-2/">next section of this tutorial</a>, you’ll learn how to use pages, hotspots, gestures, transitions and timers, and how to set them up for use with TAP. Then, we’ll create a click-through prototype in Fireworks, which will in turn be <a href="https://www.smashingmagazine.com/2013/02/15/ios-prototyping-adobe-fireworks-tap-part3/">exported as an iOS prototype</a>. Stay tuned!

### Further Reading

*   [Interactive Prototypes And Time-Savers With Adobe Fireworks](https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/)
*   [Design Cutting Edge iOS Apps With Adobe Fireworks](https://www.smashingmagazine.com/2012/12/03/design-ios-apps-with-adobe-fireworks/)
*   [Create Interactive Prototypes With Adobe Fireworks](https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/)

*   [Developing A Design Workflow In Adobe Fireworks](https://www.smashingmagazine.com/2012/06/developing-a-design-workflow-in-adobe-fireworks/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

{{< signature "mb, al, il" >}}
