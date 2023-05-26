---
title: 'Mojo Motors’ Responsive Redesign With Fireworks: UX And Interaction Design'
slug: mojo-motors-responsive-redesign-with-adobe-fireworks-part-1
image: >-
  https://www.smashingmagazine.com/inspiration/2014/04/11/get-excited-about-emotional-branding/attachment/why-you-should-get-excited-about-emotional-branding-javascript-js-illu-jpg-6/attachment/reflector_projector/
date: 2013-08-26T10:00:45.000Z
author: olawale-oladunni
description: >-
  Thanks to strong mobile Web adoption worldwide, we have seen the launch of even more responsive designs in 2012 and 2013\. Most of these have been in the publishing category, but lately we are starting to see complex transactional websites, such as Currys UK, take a brave step into this new world.
categories:
  - Fireworks
  - Workflow
  - Techniques
---
When I joined Mojo Motors in May 2012 as head of UX, it had only a desktop website — but 21% of its total Web traffic was already coming from mobile devices. Of that number, 64% were from iOS devices and 34% from Android devices. It was quite clear to me that we had to think carefully about our mobile strategy when redesigning the new website. After carefully assessing the situation, we ended up adopting the <a href="https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/">responsive design</a> approach, for the following reasons:

{{% feature-panel %}}

*   We were planning to redesign the entire website from scratch.
*   Our content lends itself well to this approach, and we did not have to deal with ads like our competitors.
*   A large number of our users were already viewing, sharing and linking to retargeting emails on mobile devices.
*   It was the fastest point of entry to mobile for us, and the cost of development, management and maintenance was lower compared to building separate websites and native mobile apps alongside a desktop website.
*   Our UX and development teams are very small, agile and nimble — a key ingredient to helping a small startup such as ours get a minimum viable product to market quickly.

In this article, I’ll shed some light on the whole process and on how Adobe Fireworks fit into it.

Recommended reading: [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)

## Our Design Process And Adobe Fireworks

As any team that has taken on a responsive design project recently will tell you, the process is different and challenging, and it stretches the limits of what traditional Web design tools such as Photoshop, Fireworks and OmniGraffle are capable of accomplishing. So, to get things done, our design team adopted a <strong>hybrid approach</strong> of designing in visual tools and directly in the browser. For us, Adobe Fireworks became the workhorse visual tool that we depended on to get things done.

I’ll share the whole process that we used to craft our responsive website and the role that Adobe Fireworks played in it. To keep the content easy to digest while still providing enough detail, I will present it in two separate articles:

1.  Part 1: UX and interaction design stage;
2.  Part 2: Visual design and front-end development stage.</p>

## UX And Interaction Design

In this first article, I’ll share our interaction design process, the role of Adobe Fireworks and some of the other design tools that helped us bring our vision to life.</p>

### Research

Naturally, we began the process by doing user research to understand how people engaged with our non-responsive website. Armed with this information, we came up with design principles, product principles, personas, scenarios and so on to help us determine and <strong>prioritize the project’s requirements</strong>.

We came away from this process with a core set of features that would provide a consistent user experience across all platforms. The key for us was to quickly go through discovery so that we could move into the iterative design process.</p>

### Designing From the Content Out

We decided earlier in the project that we would adopt a <a title="Content First, by Luke Wroblewski" href="https://www.lukew.com/ff/entry.asp?1598">content-first</a> approach by allowing the website’s content to shape the grid’s structure and layouts.

Why? On a responsive website, you have very little control over content because it scales across varying device widths — and because users explicitly zoom the viewport. In addition, some content, such as images, video and ads, can wreak havoc on the layout and affect overall performance. Identifying the different types of content, their value to users and the constraints they present early on is important. It will help you to avoid headaches later on in the process.

<a title="Old Mojomotors site (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84617cab-f058-40cf-a11f-c76d12eddbe2/old-mojosite-large-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49c86bc-7e0d-4230-86ef-e805bd579743/old-mojosite-mini.jpg" alt="Mojo motors search and details page image" width="500" height="" /></a><br>
<em>The old Mojo Motors website, showing photo placement. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79608dec-4b2f-4791-925f-ec7782693b7c/old-mojosite-large.jpg">Large version</a>)</em>

In our project, the image dimensions, aspect ratios and placement drove the overall layout because these needed to be flexible. The reason is that, on most automotive marketplace websites such as ours, <strong>car photos are one of the primary drivers</strong> of the user’s initial engagement, next to the selling price. Furthermore, these photos are typically consumed from a feed in formats and sizes that are uploaded directly to the dealer’s system.

Another thing we decided up front was to use real content wherever we could and to avoid placeholder copy like “Lorem Ipsum” and image placeholders with unknown dimensions. We were able to rise to this challenge early on by engaging our copywriter as soon as we identified missing copy throughout the project.

### Breakpoints and Grids

Before diving deep into design exploration, we knew that determining the screen widths we would support was important. For us, a healthy range between 320 and 1024 pixels was practical, based on our analytics data. We settled on three major breakpoints to support desktop and the most popular mobile and tablet device resolutions of current users. But this is not always optimal — why?

Because device specifications frequently change, as in the case of the recent taller iPhone 5 (which would be wider in landscape orientation). To mitigate this, we planned to introduce minor breakpoints and even adjust our three breakpoints as needed later during the HTML prototyping iteration stages.

<a title="Responsive grid (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dfc9f1c-2887-41b7-b89c-3cfb2c0549f6/mojogridset-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc5221ef-ab58-4d24-bde4-10e1960c7f54/mojogridset-mini.png" alt="Mojo motors final responsive grids" width="500" height="" /></a><br>
<em>Mojo Motors’ responsive grids, via the Gridset app. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ea20d63-b61d-4342-bba5-16aafbd3c963/mojogridset-large.png">Large version</a>)</em>

To aid in the creation of our grids, I played with a bunch of responsive grid systems from the endless choices of frameworks in the wild. We narrowed our choice to <a title="Gridset App" href="https://gridsetapp.com">Gridset</a>, by Mark Boulton’s team, and <a title="Gridpak App" href="https://gridpak.com">Gridpak</a>, by the good folks at Erskine. Both of these apps provide a grid image file for designing in Fireworks (or Photoshop) and an HTML framework for prototyping.

One of the factors that influenced our choice of grids was the need to accommodate the “vehicle listing module” image across breakpoints. Because we had sketched out the mobile “vehicle listing module” first, we wanted to find opportunities for reuse as we scaled up to the desktop.

In the end, we went with a 12-column grid for the desktop, a 12-column grid for tablets, and a 6-column grid for mobile in portrait orientation, <strong>via Gridset</strong>. This grid choice enabled us to reuse the module from the mobile layout proportionally across the three main breakpoints. For instance, the mobile and desktop modules are exactly the same dimensions, except that we display three modules side by side for desktop.</p>

### Sketching Mobile First

I can’t stress enough how important it is to resist the urge to jump into your favorite visual tool during the initial phase of generating ideas! Trust me, this stuff is hard enough — the last thing you need to worry about at this point is setting up the technical layouts and pixel perfection. So, if you must, work in your favorite wireframing tool — just solve the problem at hand.

Recommended reading: [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)

For me, making a few sketches of the website’s key pages at the three major breakpoints — starting with the mobile layouts and working my way up to the desktop version — and then iterating between them made sense. I personally found designing for <a title="Mobile First" href="https://www.abookapart.com/products/mobile-first">mobile first</a> to be an effective way to identify problems and resolve constraints presented by touch and small-screen devices.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a001fb-2b05-469c-af26-61bb96103f3c/mojo-mobilesketchesb-mini.png" alt="Initial sketches for mobile screens" width="500" height="" /><br>
<em>Initial sketches for mobile screens.</em>

To aid in creating your layouts, you might want to consider the <a title="Responsive Design Sketchbook" href="https://appsketchbook.com/products/responsive-design-sketchbook">Responsive Design Sketchbook</a> by App Sketchbook, or the <a title="Dot Grid Book" href="https://www.creativesoutfitter.com/product/34/dot-grid-book">Dot Grid Book</a> by Behance.

## Creating Wireframes And Prototypes

Before discussing in more detail why we used Adobe Fireworks in our project, I’d like to be clear that I find the endless debates about which design tool is better and whether to just code the darn thing to be fruitless banter.

In the end, a good designer is a creative problem-solver, and the tools are just a means to an end. Remember that users and clients don’t really care what tool we’ve used to create the final product. With that out of the way, I will focus the rest of these articles on why Adobe Fireworks made sense for our project.</p>

### High-Fidelity Wireframes in Fireworks

The great thing about creating products at a startup is that you have no external client, so you can avoid artifacts that do nothing to move the ball forward. On the other hand, the clock is winding down as your competitor tries to get the next best thing out before you can launch yours. With this in the back of my mind, the choice of using Adobe Fireworks came down to speed, familiarity and capabilities.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65c163ab-a393-4349-b7e1-3c043384779c/hifidelity-wf-all-mini.jpg" alt="Hi-fidelity homepage wireframes for desktop, tablet and smartphones" width="500" height="" /><br>
<em>High-fidelity home page wireframes for desktop, tablet and smartphones.</em>

Because we needed to create a clickable prototype for user testing quickly, we decided to skip lo-fi wireframes and go straight from sketches to high-fidelity grayscale wireframes. Below are a few other reasons why we used Fireworks to create wireframes:

1.  Compared to other tools I had considered, Fireworks has the best vector and bitmap features suitable for creating both low- and high-fidelity wireframes, detailed visual UI designs and clickable prototypes, without having to switch between multiple tools.
2.  It offers a built-in set of symbol libraries, suitable for functionality that made our work quicker.
3.  The native Fireworks PNG file format is at least three to five times smaller than a comparable Photoshop PSD file and is easily sharable with stakeholders without requiring any software other than a browser or simple image viewer.
4.  The Pages and States features work really well for creating multi-screen layouts **within a single file**.
5.  I was in the process of hiring the rest of my team when the design phase began, and I needed to work pretty quickly.</p>

### Multi-Page vs. Multi-Breakpoint File Set-Up

In the past, I would have advocated setting up a single file with multiple pages and a master page for this project. But due to the constraints of creating responsive layouts, I decided that using the Pages functionality for <strong>different breakpoints of the same page</strong> was more efficient. I found this to be the best way to quickly switch between breakpoints during the iterative process. This method also allowed us to keep the file sizes small and made it easy for my team to share files and work concurrently on different screens.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbb86323-9902-4a6f-ad85-1ade50d4496d/pages-panel-mini.png" alt="Adobe Fireworks Pages panel" width="500" height="318" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70bca03a-84c2-4d0a-8804-be61321becee/desktop-wfversion-mini.jpg" alt="Adobe Fireworks Pages panel (example)" width="500" height="" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9371f0b5-3f05-42b3-b224-17bd51c21ff2/mobile-wfversion-mini.jpg" alt="Adobe Fireworks Pages panel (example)" width="500" height="" /><br>
<em>The Pages panel in Adobe Fireworks is used for different screen sizes of the same page.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9771a9e-0109-46e1-a25a-ecf94a4a4a53/layers-panel-mini.png" alt="Adobe Fireworks Layers panel" width="500" height="310" /><br>
<em>The Layers panel in Adobe Fireworks is used to manage layout elements.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0470634-5d92-4673-a157-591add10f097/states-panel-mini.png" alt="Adobe Fireworks States panel" width="500" height="320" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bd9f85d-c4d2-4770-8144-03d6cad0b2fa/mobile-wfaltstateversion1-mini.jpg" alt="Adobe Fireworks States panel (example)" width="500" height="" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ba90cdf-1af3-44c5-b3aa-0708be424697/mobile-wfaltstateversion2-mini.jpg" alt="Adobe Fireworks States panel image (example)" width="500" height="" /><br>
<em>The States panel in Adobe Fireworks is used to show different states of the same screen.</em>

The other benefit was that we could still use the States panel to document interaction states associated with each breakpoint independently. The final file structure consisted of a “Page” for each breakpoint, a Web layer, a grid layer and other layers for the website’s content. In our template file, the grid layer was placed between the content and Web layer, as shown.</p>

### Creating Reusable Modular Elements Using Symbols

In a design like this, thinking in terms of <strong>modular reusable components</strong> that can be converted to <strong>symbols</strong> is really helpful. Doing this saves a lot of time and makes it easy to update as you iterate.

One element that benefited from this approach was the car listing module. As illustrated below, it is composed of a few different elements, including a photo with a non-destructible saturation filter applied, heart and camera icons from the library, as well as styled text. Elements such as headers, branding, navigation and footers are good candidates for symbol conversion as well.

To create a symbol in Fireworks, all you have to do is select the objects and go to <code>Modify → Symbol → Convert to Symbol</code>, or just right-click on the selection and choose “Convert to Symbol.”

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a4242a8-03a4-4d86-969b-2e22a814317c/car-listing-follow-m-mini.jpg" alt="Car-Listing module" width="500" height="300" /><br>
<em>Car-listing module symbol.</em>

Another neat thing about the symbols feature is its <strong>nesting capability</strong>. You can include symbols inside a module that you want to convert to a symbol using the same process as above. We took advantage of this feature to make it easy to vary the listing photo and flags during prototyping and in preparation for user testing.

Creating a unique module to show a different car or flag was as simple as swapping the embedded symbol within the new main symbol variation. To do this, follow these steps:

1.  Select a copy of the main symbol and go to `Modify → Symbol → Break Apart`.
2.  While it’s still selected, save it as a new symbol variation.
3.  Double-click the new symbol to enter symbol-editing mode. Then, select the embedded symbol to update.
4.  Go to `Modify → Symbol → Swap Symbol` in the menu bar, choose the replacement symbol from the “Swap symbol” dialogue box, and you are done.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37ca2bd4-dabb-4674-ac77-b84b784d8fd8/symbol-swapb-mini.png" alt="Symbol swapping illustration" width="500" height="" /><br>
<em>Photo symbols embedded into car listing module symbol</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7fa5600-8fab-4172-99e8-884a7dbbbd0b/swap-symbol-dialogue-mini.jpg" alt="Symbol swapping process" width="497" height="" /><br>
<em>Swapping embedded photo symbols to create other similar modules.</em>

### Visual Scaling During Design and Live View

Another thing that is quite disorienting when creating mobile screens is mapping resolutions as you lay things out on your large monitor. Without careful planning or knowledge of best practices for things like touch target sizes and legible text sizes, you could end up creating layouts that are hard to use.

One tool that I cannot live without and I highly recommend is the <a title="Live View App" href="https://www.zambetti.com/projects/liveview/">Live View App</a>. It is available for the Mac, iPhone and iPad. All you have to do is place the app window over your Fireworks layout and it will let you see how things scale on a real device such as an iPhone or iPad.</p>

### Preparing and Sharing Wireframes for Design Review

Clear and frequent communication between stakeholders, developers and designers was essential to the successful completion of our project. It ensured that everyone understood the implications of design decisions and were able to ask questions.

To prepare screens for our design reviews, we just exported Fireworks PNG files directly from Fireworks into a folder. During the review, we simply dragged the PNGs into multiple tabs of the browser and discussed things. I personally prefer this method of testing desktop screens because the width of the wireframes is rendered closest to how a user would see them (compared to testing with PDF files).</p>

### “Export Responsive Prototype” Extension to the Rescue

While the method described above also worked for showing mobile and tablet screens, it was sometimes difficult for the team to visualize the scale, context and fixed viewport constraints of real devices. This is where the <a title="Export Responsive Prototype" href="https://mattstow.com/export-responsive-prototype.html">Export Responsive Prototype</a> extension for Fireworks (by <a href="https://twitter.com/stowball">Matt Stow</a>) came in handy.

Creating the quick prototype using the existing wireframe file was really easy. The first thing I needed to do was define which areas of the wireframe would be fixed width and which would be flexible widths using slices. By default, areas that have not been given slices are converted to percentage-based widths. To make a sliced area fixed width or absolutely positioned left, right or center, I assigned keywords in the “Target” attribute of the Property Inspector (PI) panel (or Properties panel). Note that slices without “Target” keyword assignments are also converted to percentage-based widths.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdd98736-d8a4-4dab-864b-a8f5f9969a79/exportrwd-demo-mini.png" alt="Visualizing responsive design wireframes using Fireworks extension" width="500" height="" /><br>
<em>Visualizing responsive design wireframes using Fireworks extension.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05624d2e-b88c-4216-9f28-b4538cc4b574/pi-rwd-panel-mini.png" alt="Assigning attributes in the Property Inspector panel" width="500" height="" /><br>
<em>Slices are assigned “Target” attributes in the PI panel.</em>

Once I was done setting up the file, all I had to do was go to <code>Commands → Prototype → Export Responsive Prototype</code> and export as “HTML and Images” files using the default settings. These files were then uploaded to a Web sharing folder on my computer or a Web server where it could be hosted. Next, we shared the URL with everyone, and from there anyone could view the mockup on any desktop, smartphone or tablet browser. For more details on using the extension, <a title="Export Responsive Prototype screencast" href="https://youtube.com/watch?feature=player_embedded&amp;v=Y3RO0SKPpJ8#!">watch the screencast</a> on YouTube.

<em>A screencast by Matt Stow that explains this workflow.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bb69f74-59cd-43b2-afc8-c275438ec131/rwdfiles-mini.png" alt="Exported prototype files in finder window" width="500" height="" /><br>
<em>“HTML and Images” exported files.</em>

<strong>Note:</strong> The prototype that is created is not a responsive HTML production framework. It is only illustrative and to be used during the wireframe review process.

To keep the distraction down in a larger group, you could also mirror your iPhone or iPad onto a projection screen using <a title="Reflector App" href="https://www.reflectorapp.com/">Reflector</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/301cd555-93e5-4de2-ade1-1c123eaffcf3/reflector-projector-mini.jpg" alt="Projecting mobile screen using Reflector app" width="500" height="" /><br>
<em>Projecting a mobile screen using the Reflector app.</em>

### Creating the Prototype for User Testing

Putting together a clickable prototype in Fireworks is easy and flexible because Fireworks will accept almost any graphic file format and all HTML embeds such as videos, maps and social plugins.

For us, the first step was to plan the scenarios and determine what screens would be needed to simulate the tasks that we are asking our users to perform. In our case, we used some of the wireframes that we created and modified existing screenshots for others.

To complete the prototype, each existing wireframe and screenshot was imported as a page into a new Fireworks file and given an appropriate page name. Making edits to screenshots was a snap with the help of the bitmap tools, the vector tools and the “<a href="https://johndunning.com/fireworks/about/FillWithBackground">Fill with background</a>” command (by <a href="https://twitter.com/fwextensions">John Dunning</a>). Using these, we removed elements before compositing to reflect our own data.

Once assembled, all we needed to do was add hotspots to each page and select a destination from the PI panel. On some pages, elements were added to the States panel to simulate things like hover states.

(You can check “<a href="https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/">Creating Interactive Prototypes With Adobe Fireworks</a>” by André Reinegger and “<a href="https://www.adobe.com/devnet/fireworks/articles/atv_fw_interaction_design.html">Interaction Design and Rapid Prototyping With Fireworks</a>” by David Hogue for more in-depth exploration of the prototyping features available in Fireworks.)

Finalizing the prototype just required exporting the file using the “HTML and Images” option, and the project was ready to be hosted on the testing machine.

<strong>Note:</strong> The purpose of the prototypes at this stage was to test the website’s flow and structure. As such, we opted for this method to export separate non-responsive prototypes for each breakpoint to get initial feedback quickly. You may also decide just to use an HTML prototype framework such as <a title="Twitter Bootstrap" href="https://twitter.github.com/bootstrap/">Bootstrap</a> or <a title="Zurb Foundation" href="https://foundation.zurb.com/">Foundation</a> if your timeline and resources allow it — we opted for the quickest way to maintain our project’s velocity.</p>

## In The Next Article

Well, that’s it for this article. I know that so many workflow options are out there, which you may want to consider when designing responsively. I hope some of the ideas and workflows discussed in this article will come in handy and inspire you to consider Adobe Fireworks for your next project.

In the next article in this series, I will share our transition from the UX and interaction design phase of the project to the <strong>visual design and front-end development iterative cycle</strong>. Stay tuned!

<strong>Note:</strong> Even with the recent announcement by Adobe that it no longer plans to add <a href="https://blogs.adobe.com/fireworks/2013/05/the-future-of-adobe-fireworks.html">new features to Fireworks</a>, the tool is still very powerful and offers some of the best UI design features. Also, since Adobe plans to continue to sell Fireworks (version CS6) and provide updates to support the next major releases of both Mac OS X and Windows, it is still worthwhile considering Fireworks for your next project, because of its workflow efficiency, lightweight file size and many other advantages.</p>

### Further Reading and Resources

*   “[Developing a Design Workflow in Adobe Fireworks](https://www.smashingmagazine.com/2012/06/11/developing-a-design-workflow-in-adobe-fireworks/ "Developing A Design Workflow In Adobe Fireworks")", Joshua Bullock, Smashing Magazine
*   “[Useful Fireworks Techniques and Features for Large Design Teams](https://www.smashingmagazine.com/2012/10/12/adobe-fireworks-enterprise/),” Kris Niles, Smashing Magazine
*   “[Multi-Device Layout Patterns](https://www.lukew.com/ff/entry.asp?1514 "Multi-Device Layout Patterns"),” Luke Wroblewski
*   “[This Is Responsive](https://bradfrost.github.com/this-is-responsive/index.html "This is Responsive"),” Brad Frost

