---
title: Create Interactive Prototypes With Adobe Fireworks
slug: create-interactive-prototypes-with-adobe-fireworks
image: null
date: 2012-06-25T12:15:12.000Z
author: andre-reinegger
description: >-
  Whilst designing for screens—including Web, mobile and RIAs—you often need to
  create a prototype to see whether the application works properly before moving
  onto the development stage. Prototypes are also essential in Web projects.
categories:
  - Fireworks
  - Tutorials
  - Prototyping
---
Whilst designing for screens—including Web, mobile and <a title="Rich Internet Applications" href="https://en.wikipedia.org/wiki/Rich_Internet_application">rich interaction applications</a> (RIAs)—you often need to create a prototype to see whether the application works properly before moving onto the development stage.

Prototypes are also essential in Web projects. For example, when you plan an online ordering process, you have to be sure that every step is correct and that no critical elements are missing. Usually, you would create different screens for all pages of a website, ordering process or application workflow, and then describe the connection between them. This way you can see whether the interactions work as expected, you can test the product with different users, and your client can review it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [Design Better And Faster With Rapid Prototyping](https://www.smashingmagazine.com/2010/06/design-better-faster-with-rapid-prototyping/)
*   [Prototyping iOS And Android Apps With Sketch](https://www.smashingmagazine.com/2015/01/prototyping-ios-android-apps-sketch-freebie/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

However, a static prototype is much harder to review and test—usually it is just a bunch of images (with some explanatory notes here and there), and grasping the connection between them may be hard. Why not make things more dynamic, and easier for the client, with the help of Adobe Fireworks?

{{% feature-panel %}}

## What Is A Prototype, And Why Should I Use One?

<blockquote>"A prototype is an early sample or model built to test a concept or process or to act as a thing to be replicated or learned from." — <a href="https://en.wikipedia.org/wiki/Prototype">Wikipedia</a></blockquote>

Using an interactive prototype brings a lot of benefits. The main benefit is that you are able to easily find errors in the interaction flow or the user interface (UI) at a very early stage, before development has even started. Your client can also provide detailed feedback early in the design process. The client will get a functioning demo with many interactions displayed right on the screen, instead of a collection of images with no interaction.

To learn more about the advantages of prototyping, have a look at “<a href="https://www.smashingmagazine.com/2010/06/16/design-better-faster-with-rapid-prototyping/">Design Better and Faster With Rapid Prototyping</a>” on Smashing Magazine. A couple of interesting articles have also been published on Boxes and Arrows: “<a href="https://boxesandarrows.com/view/integrating">Integrating Prototyping Into Your Design Process</a>,” and “Defining Feature Sets Through Prototyping.”

## What Is A Click-Through Prototype?

A click-through prototype is an interactive mockup of a website or application that allows you to click through different pages and states and is packed with key interactions.</p>

### HTML Prototypes

Creating such a prototype in Adobe Fireworks is very easy. All you have to do is prepare the design for exporting as an interactive prototype: create slices for all interactive areas on the screen, and make pages for all of the different states of the application. Slices can also have hover states and be linked to the various pages. At the end you will create a click-through prototype (also known as an interactive prototype or click-through dummy) by selecting “Export as HTML &amp; Images” in Fireworks. The exported HTML files can be viewed locally in the browser or uploaded to a Web server for reviewing and testing.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d87d2b15-c8dd-44ba-b69b-5cc3b2f3c8ed/prototype.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111345" title="prototype" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d87d2b15-c8dd-44ba-b69b-5cc3b2f3c8ed/prototype.jpg" alt="Fireworks Web Prototype" width="550" height="335" /></a><br>
<em>Web prototype exported from Adobe Fireworks.</em>

### (Interactive) PDF Files

Another option is “Export as Adobe PDF.” The difference here is that interactive PDFs have a somewhat reduced feature set: rollovers won’t work, and only rectangular hotspots will export with their links. The advantage is that you can email the PDF to the client, who can then easily give feedback using the comment tools in Acrobat or Adobe Reader. Keep in mind, though, that <strong>Fireworks does not generate a comment-enabled PDF file</strong>; you must open the PDF in Acrobat Pro, enable commenting, and then save the PDF before sending it to the client. (Enabling commenting in Acrobat Pro makes it possible for anyone with the free Acrobat Reader to add comments.) Of course, if Acrobat Pro is not an option, then feedback can be provided in any of the usual ways, such as email.

In my opinion, HTML prototypes are a better option. In this article we will show how effective this kind of workflow is in Fireworks. But before diving in, let’s quickly review the main benefits that the “live” prototyping phase brings to a project.</p>

## Advantages Of Prototyping

*   Get feedback at a very early stage.
*   Increase the effectiveness of your communication. Get more detailed client feedback.
*   The prototype can be used for usability and [A/B testing](https://en.wikipedia.org/wiki/A/B_testing).
*   Find errors early on. Fewer mistakes are made later in the development process.
*   Find errors in the interaction flow or UI before development has begun.
*   The exported graphics from the prototype can be used for development.
*   The developer or team will understand what needs to be done without needing detailed explanation.
*   Overall development time will be decreased.
*   Minimize the need for development changes
*   Your client will be impressed.</p>

## How To Impress Your Client

If your client is working with a Web designer or team for the first time, he might not be so impressed by having access to a click-through prototype early in the design process, because he wouldn’t know any different. But if they have gone through the process in the past, then they will probably be very impressed by seeing a <strong>live preview</strong> of the website right on the screen, with a lot of interaction, instead of a simple static preview or collection of image files.

Personally, I have used click-through prototypes from Adobe Fireworks for over 10 years, with much success and enthusiasm from my clients.

Every client who had experience with Web design was impressed with seeing a working prototype of the website <strong>right in the browser</strong>. My clients always appreciate this, and once your clients have used one, they will prefer to work that way, too.

A word of warning, though. Be clear that this is <strong>just a prototype</strong> and that it has yet to be developed into a real application, which will happen once the prototype is approved. Otherwise, the client might expect a functioning website to appear simply by you copying the prototype to the root folder of their domain.</p>

## How To Create Click-Through Prototypes In Fireworks

The click-through prototype that Fireworks creates consists of simple HTML files (i.e. HTML with tables and images). But this is not important because the prototype is used <strong>only in the early stages of the design process</strong>. Once the prototype has been approved and tested by the client, you can continue to the development phase of the website, with semantic HTML and CSS. Fireworks is helpful only for transferring the design to the development stage.

What are the key elements of an interactive prototype? Basically, a prototype consists of pages (and, optionally, a master page), states, slices and hotspots. Let’s review each in more detail.</p>

### Pages and Master Pages

To create a click-through prototype, you first need to set up <strong>multiple pages</strong> in your document. Every state of an application or every page of a website will need a separate page in Fireworks. To create an individual page, you can use the Pages panel. When all pages in a design share common elements—such as a header, logo and main navigation—you can use a master page.

In our example website, we will need six pages (home, products, shop, shop detail, support and contact). They will all have the same header area, with a logo, image and navigation, so creating a master page makes sense. To do so, create a page with only those elements on it, and then (just as in InDesign), right-click on the page in the Pages panel, and select “Set as Master Page,” Alternatively, you can use the options menu on the right side of the Pages panel. Now, every element that is placed on the master page will automatically appear on all pages, which will save us a lot of development time.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c8607e-6ba2-4914-a6bf-129218f6f0b2/masterpage1.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111379" title="master page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c8607e-6ba2-4914-a6bf-129218f6f0b2/masterpage1.jpg" alt="Fireworks Set as a Master Page" width="550" height="215" /></a><br>
<em>Set a master page in Fireworks.</em>

Based on the master page, we can now build all of the pages. Go to the Pages panel and click on the new page icon several times until you have six pages (plus the master page). Then give each a meaningful name. The home page should be named <code>index</code> in the Pages panel, and “Shop Detail” can be <code>shop_detail</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55b8faeb-111b-4fa4-8e12-d0881ead21f4/pages1.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111358" title="pages" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55b8faeb-111b-4fa4-8e12-d0881ead21f4/pages1.jpg" alt="Fireworks Pages Panel" width="550" height="345" /></a><br>
<em>The Pages panel in Fireworks.</em>

When it comes to exporting, Fireworks will automatically name these two pages <code>index.html</code> and <code>shop_detail.html</code>. Now, we can fill each of the six pages with its unique design elements (i.e. not the common elements, which will go in the master page).

All pages created in the Pages panel can later be linked to each other via hotspots and slices (more on that later).

<strong>Please note:</strong> All elements on the master page will appear in the same locations across all of the individual pages and cannot be moved on a page-by-page basis. So, if one page needs to be different than the master page, you will have to overlay the new elements on the master page’s elements, or use another Fireworks file.</p>

### States

To give the client more interactive feedback, you might also want to create hover states for the navigation elements. To do so, open up the States panel, and add a new state by clicking “New/Duplicate State.” If you are using a master page, you can create the second state right on the master page (thus saving a few clicks), and then it will be used on the individual pages. Now in the new state, you only need to place the elements that should change on hover, such as the navigation, links, drop-down menus, tooltips and so on.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ff530b9-26c9-47eb-a50a-aea1a315c2ee/states2.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111386" title="states" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ff530b9-26c9-47eb-a50a-aea1a315c2ee/states2.jpg" alt="Fireworks States panel" width="550" height="345" /></a><br>
<em>The States panel in Fireworks</em>

To show a hover effect for a navigation element, you simply need to place the graphic for the hover effect in this second state. You can change the color of the navigation background or a drop-shadow applied to a text object. All of these would change on hover in the second state (the hover state) in the States panel.

<strong>Please note:</strong> Fireworks does not use CSS <code>:hover</code> pseudo-classes. Instead, it uses JavaScript to swap the images in the prototype (a traditional JavaScript-based rollover or mouseover). This JavaScript behavior is rather old and should be used only during the rapid prototyping phase. During the development stage, it should be done with CSS pseudo-classes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98e4276c-31fe-4c43-947b-0fb1bc746218/add-states.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111388" title="add-states" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98e4276c-31fe-4c43-947b-0fb1bc746218/add-states.jpg" alt="Fireworks Add States" width="550" height="149" /></a><br>
<em>The “Add States” option in the States panel</em>

After all hover states have been created, you can reuse them for all pages. If you have a master page, you only have to create a second state for all pages by right-clicking on the States panel, or by clicking “Add States” in the options menu to the right of the panel.

The new state will automatically include all hover elements from the second state of the master page. If you don’t have a master page, you’ll have to copy and paste all hover elements to the second state on all individual pages.

With slices, you are able to define the regions that should change on hover.

<strong>Please note:</strong> When multiple states are used on the master page for rollovers and image swaps, you need to manually add additional states to all of the other pages.</p>

### Slices and Hotspots

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147b1d13-0d06-44ec-8171-f9f70246de0e/slices1.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111399" title="slices" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147b1d13-0d06-44ec-8171-f9f70246de0e/slices1.jpg" alt="Slices in Adobe Fireworks" width="550" height="245" /></a><br>
<em>Slices in Adobe Fireworks</em>

Slices can be used to define regions that are interactive and that will be linked to different pages on the same website or that even point to external URLs. Hotspots can only be used to generate areas for hyperlinks (internal or external).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21dbd2e0-3adb-4cc5-a3ea-ee5d5b1df7e0/create-slices.jpg"><img loading="lazy" decoding="async"  class="111391" title="create-slices" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21dbd2e0-3adb-4cc5-a3ea-ee5d5b1df7e0/create-slices.jpg" alt="Create Slices in Fireworks" width="550" height="200" /></a><br>
<em>Create Slices in Fireworks</em>

To make a hover state, select the Slice tool (step 1 in the image above), and then outline the whole area of the hover element (step 2).

You can also create a slice by selecting an object on the canvas, right-clicking and choosing “Insert Rectangular Slice.” This is often easier, faster and more accurate than using the Slice tool. If you select multiple objects, right-click and then insert a slice, Fireworks will show a dialog box with the option to insert multiple slices (one for each object) or one big slice that covers all of the selected objects.

After you have defined all of the areas, you can use the target in the middle of each slice to create the hover effect (step 3). To do so, click and drag out the target in the middle of the slice back into the same slice. In most cases, it will be the same location, so it has to be pointed to the same slice (step 4). If you want to show another image on hover, then the target must point to the slice with the image; but in the most cases it will be pointed to itself. Then Fireworks will ask you which state to choose for the image swap (step 5). Here is where you would pick the state with the hover image (for example, “State2”).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3337a19-59ea-460d-8f7f-6d12ade64ada/preview3.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111401" title="preview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3337a19-59ea-460d-8f7f-6d12ade64ada/preview3.jpg" alt="Preview in Adobe Fireworks" width="550" height="245" /></a><br>
<em>Preview the design in Adobe Fireworks</em>

After repeating this step for all hover areas, you can look at the result by clicking the “Preview” button in the top-left of the Fireworks PNG document.

For hover elements that appear on every single page, such as the main navigation, you can save time by creating the slices in the master page.

To help you, Fireworks provides some visual associations for slices (green) and hotspots (blue); and the Property Inspector panel (or Properties panel) will also show the slice or hotspot type. Standard slices and hotspots are semi-transparent, but HTML slices are opaque. You can also assign custom colors to slices and hotspots—useful if you want to differentiate the types of code that have been placed in them (HTML, JavaScript, embedded Flash objects and so on).

<strong>Please note:</strong> When using states for rollovers, copying or sharing background elements to the other states is sometimes necessary, otherwise blank areas might appear on rollover. For example, if a slice is larger than the object that will change on rollover, then the background <em>behind</em> the object will also need to appear in the rollover state (state 2). I recommend using “Share to states” for elements that will be the same in all states to maintain a consistent appearance during rollovers (or on hover). “Share to states” is accessible in the Layers panel (right-click on the layer that needs to be shared to the mouseover state).</p>

### Linking Pages

Now that all interactive elements have slices, the pages can be linked to each other. To generate hyperlinks, you would typically click on a slice (or on a hotspot, if no hover effect is needed) and enter a URL in the “Link” field in the Properties panel. For an external URL, you would enter, for example, <code>https://www.google.com</code>; for an internal link, you have to enter the name of the page from the Pages panel. All page names from the Pages panel are also available in the drop-down menu there, which prevents typos.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5605205b-3933-474d-852b-10829a5e5c04/links1.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111404" title="links" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5605205b-3933-474d-852b-10829a5e5c04/links1.jpg" alt="Linking Pages in Fireworks" width="550" height="345" /></a><br>
<em>Linking pages in Fireworks</em>

The names of the pages in the Pages panel should be Web-friendly (i.e. no spaces or special characters). You can check out the demo prototype you have just created, with all of the hyperlinks and interactive areas, by clicking on <code>File → Preview in Browser → Preview All Pages</code>.</p>

## Add Real Interactivity To Your Prototype

Many Fireworks users do not know about HTML slices. For every slice, there are three different options in the Properties panel (foreground image, background image and HTML). With foreground and background image, you can specify the exporting mode for images if you are exporting HTML and CSS out of Fireworks.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c515da-14fb-42d3-9635-2033f207b9b4/slice-types.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111346" title="slice-types" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c515da-14fb-42d3-9635-2033f207b9b4/slice-types.jpg" alt="Fireworks Slice Types" width="550" height="122" /></a><br>
<em>Slice types in Fireworks</em>

For click-through prototypes, which are based on HTML and images, the default “Foreground image” option works best. If you want to place different types of interaction in your prototype, the HTML slice is a good choice. You can place any HTML code in an HTML slice, which is very efficient if some elements already exist, such as interactions. Thanks to HTML slices, you can easily insert Google Maps, videos, animations and so on right in the prototype to show the client how the elements will function.</p>

### Embed Google Maps

What if we wanted the “Contact” page to have an embedded Google Map? You don’t need to take a screenshot of a map area to indicate the presence of Google Maps. In Fireworks, you can place the actual map itself right in the prototype.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7524099-ec7a-43a1-a034-1fd5785eed85/maps1.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111410" title="maps" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7524099-ec7a-43a1-a034-1fd5785eed85/maps1.jpg" alt="Use of HTML Slices" width="550" height="345" /></a><br>
<em>Using HTML slices in Fireworks</em>

To do so, select the Slice tool (step 1 above), and draw a slice over the area where you want to show the map (step 2). Next, change the type to “HTML” in the Properties panel (step 3). Now an “Edit” button will be available (step 4) that opens up a dialog box where you can paste the HTML code into the slice (step 5).

Next, go to <a href="https://maps.google.com/">Google Maps</a>, locate the client’s office on the map, copy the iframe HTML code for embedding, and then paste it into the HTML slice.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31a5f4d9-a5f5-4ec8-8037-c8e803e9dd47/maps.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111352" title="maps" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31a5f4d9-a5f5-4ec8-8037-c8e803e9dd47/maps.jpg" alt="Fireworks HTML Slice" width="550" height="345" /></a><br>
<em>The HTML slice in Fireworks</em>

The width and height of the iframe should have the same pixel dimensions as the slice. Review the embedded map in the prototype by going to <code>File → Preview in Browser → Preview in…</code>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b4c155-aff9-4dfd-9ce5-49d0c0f33130/maps-view.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111344" title="maps-view" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b4c155-aff9-4dfd-9ce5-49d0c0f33130/maps-view.jpg" alt="Fireworks Google Maps Include" width="550" height="345" /></a><br>
<em>Embedded Google Map in the Fireworks prototype</em>

See an <a title="Google Maps placed into a Fireworks website prototype" href="https://smashingmagazine.com/provide/fw-interactive-prototypes/html/contact.htm">example of Google Maps</a> embedded in a prototype of a website made with Fireworks.</p>

### Embed Video

Video can be easily embedded in the prototype, similar to maps. Go to the video that you want to embed (whether on YouTube, Vimeo, etc), and copy the embed code of the video. To see a live preview of the video, go again to <code>File → Preview in Browser → Preview in…</code>

<strong>Please note:</strong> The embed code will set the width and height of the video. The HTML slice in Fireworks should have the exact same dimensions in order to keep the proportions correct.</p>

### Embed Flash Animation And More

With an iframe, you can embed everything in a live prototype. Just place the element you want to embed in an iframe, and paste the code in the HTML slice. So even Flash animation, video and other elements stored on your own Web server can be easily embedded.

Of course, HTML slices are not limited to Google Maps and Flash video. Anything that can be wrapped in an iframe can be put in an HTML slice, including JavaScript and AJAX elements, JavaScript animation, HTML5 and CSS3 animations and much more. For example, with <a title="Adobe Edge (on Adobe Labs)" href="https://labs.adobe.com/technologies/edge/">Adobe Edge</a>, you can create animation and interactivity based on HTML5, CSS3 and JavaScript. Even Adobe Edge animations and interactions can be included in a Fireworks prototype. Alternatively, you could make your own HTML5 and CSS3 animation, and paste the code directly in the HTML slice. So many possibilities!

## Export The Click-Through HTML Prototype For Review

The final step of the process is to export the prototype for review. Before doing this, you can do a quick preview in the browser to make sure everything works as expected; go to <code>File → Preview in Browser → Preview all Pages in Browser</code>. Remember to select “Preview all Pages…”; if you select “Preview in…,” you will only see a preview of the <em>actual</em> page, and the links to other pages will not work. If you choose “Preview all Pages…,” you will be able to see all pages, with all interactions and internal links working.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cc29098-279e-4dc3-a221-f25cc2ac48c7/preview.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111354" title="preview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cc29098-279e-4dc3-a221-f25cc2ac48c7/preview.jpg" alt="Fireworks Preview in Browser" width="550" height="345" /></a><br>
<em>Fireworks preview in the browser</em>

Try everything out before exporting the live prototype. If everything is functioning properly, you can then export the click-through prototype by going to <code>File → Export…</code>. In the dialogue box, select “HTML &amp; Images,” “Export Slices,” “All Pages,” “Include Areas Without Slices” and “Images in Subfolder.“

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b6365c-577a-4a07-a9f3-f2d4bfe65bc8/export.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111343" title="export" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b6365c-577a-4a07-a9f3-f2d4bfe65bc8/export.jpg" alt="Fireworks Export" width="550" height="233" /></a><br>
<em>Options for exporting your prototype in Fireworks</em>

### A Couple Of Live Demos

See an <a title="Basic website prototype made with Fireworks" href="https://smashingmagazine.com/provide/fw-interactive-prototypes/html/">example of a prototype</a> with very basic interactions—such as mouseover states, linked pages and an embedded Google Map—exported right away from a Fireworks PNG file. (Feel free to explore the pages and available interactivity.)

Another method is to export an interactive PDF by going to <code>File → Export…</code> and selecting “Adobe PDF” as the exporting format. The PDF can then be sent to the client, who will be able to review the website and interactions offline and then provide you with feedback. See also an <a title="Example of an interactive PDF" href="https://smashingmagazine.com/provide/fw-interactive-prototypes/pdf/interactive-pdf.pdf">example of an interactive PDF</a> (an HTML live prototype is a more elegant solution, but it’s good to know that there are other options).</p>

### A Word On The New Mobile Web And Fireworks

While preparing interactive prototypes with Adobe Fireworks can be fast and easy, they are not <em>responsive</em> or adapted specifically to the modern mobile environment. Luckily, the <a href="https://www.mattstow.com/export-responsive-prototype.html">Export Responsive Prototypes with Adobe Fireworks</a> extension by <a href="https://twitter.com/stowball">Matt Stow</a> and <a href="https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/">Touch Application Prototypes (TAP) for Adobe Fireworks</a>, are here to help! Both extensions are free and will help you build responsive Web prototypes or iOS prototypes in Fireworks with greater ease.</p>

## Acting On Client Feedback

Finally, what do you do when the client provides feedback on the prototype and the interactions?

In Fireworks, acting on the client’s feedback is very easy. All you have to do is to make some adjustments to the design (based on the client’s notes and comments), re-export a new version of the prototype for review, and upload it to a test server. The whole process can be done in minutes, and you can make as many design changes and iterations as needed.

Fireworks fits perfectly in the workflow of a Web or mobile app designer. You can do the whole design in Fireworks, or you can import artwork from Photoshop or Illustrator and continue in Fireworks. The layout for all of the pages of the website can be easily created with the Pages panel, in combination with the master page feature. To add interactivity, you can set all of the different states of the website, with the help of the States panel. This whole process is fast because Fireworks is optimized for this type of workflow. Slices and hotspots enable you to link all pages to each other with ease.

Both the designer and client benefit from an interactive prototype. While preparing an interactive prototype certainly takes some time, it will more than pay off during the development process.</p>

### Further Reading

*   “[Create Interactive Prototypes](https://tv.adobe.com/watch/fireworks-tips-and-tricks/creating-interactive-prototypes/),” Adobe TV (video)
*   “[Design Better and Faster With Rapid Prototyping](https://www.smashingmagazine.com/2010/06/16/design-better-faster-with-rapid-prototyping/),” Lyndon Cerejo, Smashing Magazine
*   “[Integrating Prototyping Into Your Design Process](https://boxesandarrows.com/view/integrating),” Fred Beecher, Boxes and Arrows
*   “Defining Feature Sets Through Prototyping,” Laura Quinn, Boxes and Arrows
*   “[Touch Application Prototypes (TAP) for iPhone and iPad, using Adobe Fireworks](https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/),” Matthijs, UNITiD
*   “[Content Prototyping In Responsive Web Design](https://www.smashingmagazine.com/2011/09/26/content-prototyping-in-responsive-web-design/),” Ben Callahan, Smashing Magazine
*   “[Refining Your Design In Adobe Fireworks](https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/),” Benjamin De Cock, Smashing Magazine
*   “[Why Your Links Should Never Say “Click Here”](https://www.smashingmagazine.com/2012/06/20/links-should-never-say-click-here/),” Anthony T, Smashing Magazine

<em>(al) (mb)</em>

