---
title: Useful Fireworks Techniques And Features For Large Design Teams
slug: adobe-fireworks-enterprise
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/562f96e3-cbe2-436d-b2dd-9e3d00d6905b/fireworks-logo2.jpg
date: 2012-10-12T11:30:27.000Z
author: kris-niles
description: >-
  While Fireworks can be a useful and powerful tool for any screen designer,
  several aspects of it make it really shine in an enterprise environment when
  used by both small and large design teams. What do I mean by “enterprise”? For
  the purpose of this article, enterprise can be defined as any environment
  where multiple designers, developers and other stakeholders collaborate on a
  project.
categories:
  - Fireworks
  - Techniques
---
While Fireworks can be a useful and powerful tool for any screen designer, several aspects of it make it really shine in an enterprise environment when used by both small and large design teams.

What do I mean by “enterprise”? For the purpose of this article, enterprise can be defined as <strong>any environment where multiple designers, developers and other stakeholders collaborate on a project</strong>. In this situation, Fireworks excels for a variety of reasons.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Sketch, Illustrator or Fireworks?](https://www.smashingmagazine.com/2016/04/exploring-a-new-illustration-ui-design-app-gravit/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

I’ll share the <strong>top five reasons</strong> why our user experience (UX) team at <a href="https://www.citrixonline.com/collaboration/about_citrix_online">Citrix</a> (which consists of about 20 designers, researchers and editors, working on Web, desktop and mobile applications) uses Fireworks. I’ll illustrate my points with a few practical examples, as well as examples from other design firms.

{{% feature-panel %}}

## 1\. The (Smart) Fireworks PNG File Format

A huge benefit of Fireworks is that it saves images in the <a href="https://en.wikipedia.org/wiki/Portable_Network_Graphics">PNG</a> file format. PNG files are viewable in any browser or image viewer. And Windows Explorer and Mac’s Finder will display thumbnail previews of your Fireworks PNG files when you browse them locally.

Fireworks efficiently embeds all of the vector layer data into the meta data section of the PNG. This means you can view a Fireworks PNG file in any image viewer or directly in a Web browser, and if you open the same PNG in Fireworks, you have full editing capability of the vector paths, layers, pages, live filters, embedded bitmaps, symbols, etc.

The PNG format is also very efficient. In our experience, even complex multi-page documents rarely reach over 5 MB.

What does this mean in the enterprise? Quite a lot, actually!

On our company’s internal network, we have a shared drive that everyone stores files on. When we want to share mockups with stakeholders in the company, we just point them right at the files. For instance, if a PNG file is located at <code>X:/UXGroup/Project/Design.png</code>, we can send a link to anyone in the company (i.e. <code>https://shared/uxgroup/project/Design.png</code>), and they can view the file in their Web browser — no need to export the Fireworks PNG to any other format!

This saves us the additional steps of exporting JPGs (or PNGs) of our design files whenever we want to share them with stakeholders or with anyone who doesn’t have a copy of Fireworks.

I can even edit a file in Fireworks while on the phone with a stakeholder (or fellow designer), and as soon as I hit “Save” in Fireworks, the person on the other end of the line can simply refresh their browser and see the changes I just made! Excellent for quick copy revisions and brainstorming.

<a href="https://sonspring.com/">Nathan Smith</a> describes a similar process in his article “<a href="https://www.adobe.com/devnet/fireworks/articles/enterprise_it.html">Fireworks in Enterprise IT</a>”:
<blockquote>"Working as an interface designer at a Fortune 500 company, I used to save my work on a shared network drive. The user experience team had full access to our Adobe Fireworks PNG files, whereas all other stakeholders in the company (of which there were many) had read-only rights. This setup allowed my team to go about working in a typical fashion. When it was time to get sign-off for our mockup designs, rather than performing a batch export of hundreds of PSD files to JPG (or other) image format, we would just send a quick email: “Here are the project comps: <code>https://10.10.10.xx/uxd/project/</code>.”

The approval team could then peruse the interface mockups at their leisure, without us having to do anything extra special to allow them to see our designs. Even better: being on a conference call with the primary stakeholders reviewing my PNG file in their browsers, I could edit the design in real time, based on their feedback. I cannot even begin to estimate the amount of time I saved."</blockquote>

This can also work beautifully with any FTP client or with synchronization software such as Dropbox. Just place your PNGs in your Dropbox folder and send the public URL to your stakeholders or share the folder with them. Now, whenever you hit “Save” in Fireworks, your changes will be instantly synced to everyone you have shared them with.

One caveat to this approach is that <strong>browsers display only the first page</strong> of a Fireworks file. So, if your document has multiple pages, you will need to export each page to its own PNG file. On the positive side, Fireworks has fairly robust page-exporting options that make the process very easy, allowing you to export multiple pages at once.</p>

## 2\. Layer Management

If you are a Photoshop user, then you are probably very familiar with “layer management.” You have read articles on PSD etiquette and, heck, you might even be a Layer Mayor. While I can appreciate organization, managing layers and layer groups doesn’t sound like fun.

<img loading="lazy" decoding="async"  title="Fireworks Manifesto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f872ffc-ab40-4edf-94d5-3d200d0d2d26/manifestos.jpg" alt="Fireworks Manifesto" width="500" height="420" /><br>
<em>(Illustration sources: <a title="Illustration by Dan Rose" href="https://dribbble.com/shots/134283-Photoshop-Etiquette">Dan Rose</a>, <a title="Illustration by Tymn Armstrong" href="https://dribbble.com/shots/93622-Resolution-2011">Tymn Armstrong</a>, <a title="Illustration by Michel Bozgounov" href="https://dribbble.com/shots/94577-Fireworks-Resolution-2011">Michel Bozgounov</a>, <a title="Yellow Notebook Paper Texture (public domain)" href="https://www.photos-public-domain.com/2011/01/02/yellow-notebook-paper-texture/">PhotosPublicDomain.com</a>)</em>

In Fireworks, I hardly ever glance at the Layers panel. Alan Musselman, designer and developer of Android games, <a href="https://twitter.com/DeeSadler/status/224912957258211330">sums it up</a> nicely:
<blockquote>"By the time you organized your layers in Photoshop I’m outside enjoying the weather because I’m finished with the project [in Fireworks]."</blockquote>

How is this possible?

Fireworks’ interaction methodology is similar to Illustrator’s: when you hover your mouse over each object on the canvas, the object is highlighted (its outline changes to red), and then you can simply select it by clicking on it (the outline will change to blue). You can also select several objects by clicking on each while holding <code>Shift</code> or simply by dragging the mouse across them all.

Selecting objects on the canvas that are placed underneath other objects is possible, too, as Trevor Kay explains in “<a href="https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/">Interactive Prototypes and Time-Savers With Adobe Fireworks</a>”:
<blockquote>"The Select Behind tool enables you to select a top-most object and, with repeated clicking, select each of the elements directly beneath it in turn. This is yet another feature that helps you work more efficiently by not requiring you to awkwardly navigate the Layers panel, searching for an object either by name or tiny thumbnail."</blockquote>

In practice, this means you don’t need to bounce back and forth between the Layers panel and the canvas to find and select objects — you just work directly with them. I find it a much more intuitive way to work.

What’s more, after selecting one or more objects, you can easily <strong>change many of their properties all at once</strong>:

*   Resize, skew, rotate and use the [9-Slice Scaling](https://www.adobe.com/devnet/fireworks/articles/9-slice_scaling.html) tool;
*   Change the fill or stroke (edit colors, work with gradient fills, change the size and type of stroke, etc.);
*   Add or remove Fireworks live filters (and edit their properties);
*   Apply styles;
*   Change the objects’ blending mode;
*   Add or remove textures and patterns;
*   Change the roundness of rectangle corners;
*   And much more.

In short, what can be done with one object selected on the canvas can be done with multiple objects simultaneously. This really is a big time-saver, freeing you from having to hunt through the Layers panel!

Besides being a much faster and more intuitive way to work, it also makes the process of multiple designers collaborating on the same file or project much easier.

Finally, let me add that while naming layers and objects in Fireworks is often not necessary, it is still a good practice, especially when working on more complex projects. If you foresee opening an archived file years later or frequently sharing files with collaborators, then naming layers and objects will make file organization more efficient.</p>

## 3\. Did I Mention Pages And Master Pages?

<strong>Pages</strong> are a feature that illustrate a key difference between Fireworks and Photoshop. When working on complex interactions (a shopping-cart check-out flow, for example), showing how interactions unfold over time is essential. Having the ability to create multiple pages allows you to easily do this.

It also helps to keep the number of separate design files low, which, combined with the fact that each page can have its own settings (canvas size, canvas color, export settings, etc.), gives you a ton of flexibility.

And if you are using Pages in Fireworks, you can easily jump from a static design to an interactive prototype, which brings even more benefits (more on that later).

If you use pages, you can also create master pages. <strong>Master pages</strong> allow you to define common elements that appear across multiple pages. For instance, on the master page, you might put the website’s logo and header. As you create new pages, those elements will automatically appear on them, and if you make a change to any element on the master page, it will appear throughout the document. If you need to modify the header or any other recurring element, this method is far quicker than having to open multiple files and individually edit the given element in each one or having to manually tweak the same elements on multiple pages (or multiple layers).

Let me quickly illustrate this feature. For an example, we’ll use the <a title="See the first example: NationWide/NASCAR, made by Chris Stevens" href="https://webdesignledger.com/inspiration/18-great-examples-of-sketched-ui-wireframes-and-mockups">UI wireframe sketches of Chris Stevens</a>.

Suppose we have a design in which several elements — the header, logo, navigation and footer — will be the same on all pages. Let’s move them to the master page. All of the other pages will display these elements just as they appear on the master page:

<img loading="lazy" decoding="async"  title="Master Page Elements On All Pages" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c80374f-3e56-49df-b19b-09137c3b368e/master-page1.jpg" alt="Master Page Elements On All Pages" width="500" height="600" /><br>
<em>Elements on the master page will automatically appear on all pages.</em>

Next, suppose the design team decides that moving the logo to the right side and moving the navigation to the left would be better. The elements, which exist on the master page, need to be altered only once, then all of the other pages in the design will instantly reflect those changes:

<img loading="lazy" decoding="async"  title="Simultaneous Update On All Pages" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1889732-aed7-4a84-8d9e-730d88137d36/master-page2.jpg" alt="Simultaneous Update On All Pages" width="500" height="600" /><br>
<em>Edit an element (or several elements) on the master page and see all pages updated with those changes!</em>

Fireworks has other features that make complex design projects easier. Here are just a few:

*   In Fireworks, you can turn any object or group of objects into a **symbol**. Just create a symbol and copy it to a few layers and/or pages; then, whenever you edit the symbol, all instances of it throughout the document will automatically update. Symbols can be of different types — graphic symbols, button symbols, and component (rich) symbols — each of which serves a different purpose and has different benefits. (If you want to learn more, the “[Symbols](https://help.adobe.com/en_US/fireworks/cs/using/WS4c25cfbb1410b0021e63e3d1152b00db4b-7fd4.html)” section in Adobe’s documentation for Fireworks might help.)
*   Fireworks gives you the option to **share layers to pages** (i.e. share the contents of one layer to selected pages), so if the content of a layer is updated, then the changes are automatically shown on all of the pages on which the shared layer appears).
*   If you work with states, you also have the option to **share states to pages**.
*   You can use **styles** in your Fireworks PNG documents (and can even import and export them to reuse in more than one document).

By taking advantage of pages, master pages, symbols and styles, every designer on our team saves a huge amount of time every day!

## 4\. Interactive Prototyping Made Easy

If you are creating a complex interaction that spans multiple pages, being able to prototype the interaction before investing precious development time in coding it is often very beneficial. Again, Fireworks comes to the rescue with its built-in capabilities to create simple click-through prototypes for multi-page documents.

This subject was covered thoroughly by Smashing Magazine in a recent article by André Reinegger, “<a href="https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/">Create Interactive Prototypes With Adobe Fireworks</a>” (quoted below), and one by Trevor Kay, “<a href="https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/">Interactive Prototypes And Time-Savers With Adobe Fireworks</a>.” Check them out!
<blockquote>"A click-through prototype is an interactive mockup of a website or application that allows you to click through different pages and states and is packed with key interactions. Creating such a prototype in Adobe Fireworks is very easy. All you have to do is prepare the design for exporting as an interactive prototype: create slices for all interactive areas on the screen, and make pages for all of the different states of the application."</blockquote>

By defining slices and hotspots, you can quickly link the pages in your document together and export them all at once as HTML files.

<img loading="lazy" decoding="async"  title="Create Interactive Prototypes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66b5657e-5a15-413a-aa04-3778cb31ffca/pages-hotspots.jpg" alt="Create Interactive Prototypes" width="500" height="345" /><br>
<em>André Reinegger <a href="https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/">explains in detail</a> how to create interactive prototypes with Fireworks. Pages and hotspots are key parts of the process.</em>

For instance, if your shopping cart has a “Buy now” button on the first page, you can specify that, when clicked, the button will take the user to page 2 of the design; and on page 2, you can define more interactions, and so forth. Similarly, you can create simple navigation between the pages or create links that point to external resources. What’s more, any behavior added to the master page will also be active on every other page in the document (so, a navigation bar graphic could serve as a navigation bar in the whole interactive prototype). Build it once and it works everywhere!

Interactive prototypes also help you quickly experience how an interaction feels as you click through it. You can even use these prototypes for user testing, to work out any kinks before investing in the actual development.

Of course, you always have the option to use an external application for the live-interaction part of the design and development process, but for simple interactions, Fireworks does the trick nicely, and we don’t even have to switch to another app.</p>

## 5\. Fireworks Component Library With Evernote

One thing that makes collaboration between designers and developers much easier and more efficient is having a common set of design resources. Fireworks has a “Common Library” panel, but I won’t sugarcoat it: it’s not useful when multiple designers are collaborating and need to share a library of UI resources that needs to be updated over time.

However, taking advantage of Fireworks’ use of vector PNG files, we can use a third-party service — namely, <a href="https://evernote.com/">Evernote</a> — with Fireworks to create and maintain a <strong>synchronized component library</strong>. This will allow all designers on the team to simply drag and drop Fireworks PNG elements into their layouts from a common source. (See “<a href="https://www.smashingmagazine.com/2012/09/13/create-pattern-library-with-evernote-fireworks/">Creating a Pattern Library With Evernote and Fireworks</a>,” in which I speak about this technique in greater detail.)

Here are the benefits of this workflow:

*   **Easily browsable**.  Finding what you’re looking for is easier when you can just see it. And because source Fireworks PNG files can be viewed in the browser just like any regular image file, you can find the right asset in Evernote simply by browsing for it — while examining the previews! (This wouldn’t work with Photoshop, Illustrator or InDesign files because browsers cannot read their proprietary file formats.)
*   **Searchable**.  If you can’t find it by browsing, just search. And in Evernote, even the text in PNG files is indexed (a truly amazing feature, which, again, is possible because of the PNG format’s openness).
*   **Drag and droppable**.  Pulling elements into your layout is super-easy. Simply drag and drop them from Evernote into the Fireworks document!
*   **Synchronized**.  Any change made to a UI element propagates instantly, and everyone on the team always has access to the most recent version. Plus, Fireworks PNG files are fairly small, so synchronization is fast and easy.

<img loading="lazy" decoding="async"  title="Evernote And Fireworks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74ba5169-28cc-4196-b7ab-c0518d314ba6/evernote-fireworks.png" alt="Evernote And Fireworks" width="500" height="201" /><br>
<em>Evernote and Fireworks can make a component library an easy solution.</em>

## Conclusion

It’s fair to say that Fireworks is not perfect and has its limitations. For example, if you exceed a certain number of pages or objects in a file, Fireworks could suffer some drop in performance. The app is not 64-bit, so it cannot use all of the 16 GB of RAM you’ve just installed in your new computer, and its user interface is slightly different than other tools in the Adobe family.

However, in our design practice, we’ve found that the benefits of Fireworks <em>far</em> outweigh the disadvantages.

In one relatively short article, I can’t cover all of the reasons why we use Adobe Fireworks, but if you (and your design team) work in the field of screen design — UI, UX, Web, mobile — then I hope the five above are enough to give you ideas or inspire you to try something new!

### Further Reading

Here a few links to articles, tutorials and blog posts that discuss some of Fireworks’ most interesting features, as well a few complex workflows that are possible with it:

*   “[Fireworks for Beginners](https://medialoot.com/blog/fireworks-for-beginners/),” MediaLoot
*   “[Fireworks in Enterprise IT](https://www.adobe.com/devnet/fireworks/articles/enterprise_it.html),” Nathan Smith, Adobe Developer Connection
*   [Adobe Fireworks Hall of Fame](https://fireworksinterviews.com/) A project by Linus Lim, featuring interviews with designers.
*   “[Designing Interactive Products With Fireworks](https://www.adobe.com/devnet/fireworks/articles/cooper_interactive.html),” Nick Myers, Adobe Developer Connection
*   “[Prototyping for the Apple iPhone Using Fireworks](https://www.adobe.com/devnet/fireworks/articles/prototype_iphone_app.html),” Matthijs Collard, Adobe Developer Connection
*   “<span class="removed_link" title="https://qrayg.com/learn/fireworks/">Adobe Fireworks Tutorials</span>” Craig Erskine, Qrayg.com A mini-collection of advanced Fireworks tutorials.
*   “[How to Achieve Pixel Perfection in Your Designs With Adobe Fireworks](https://ivomynttinen.com/blog/how-to-achieve-pixel-perfection-in-your-designs-with-adobe-fireworks/),” Ivo Mynttinen
*   “[10 Reasons Why I Prefer Fireworks to Photoshop for Web Design](https://boagworld.com/design/fireworks-vs-photoshop),” Leigh Howells, Boagworld
*   “[We Love Fireworks](https://floridaflourish.com/news/detail/we-love-fireworks/),” Chris Brauckmuller, Flourish Web Design
*   “[Interactive Prototypes And Time-Savers With Adobe Fireworks](https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/),” Trevor Kay
*   “[Developing A Design Workflow In Adobe Fireworks](https://www.smashingmagazine.com/2012/06/11/developing-a-design-workflow-in-adobe-fireworks/),” Joshua Bullock
*   “[Refining Your Design In Adobe Fireworks](https://www.smashingmagazine.com/2012/05/07/refining-designs-adobe-fireworks/),” Benjamin De Cock

<em>(mb) (al)</em>

