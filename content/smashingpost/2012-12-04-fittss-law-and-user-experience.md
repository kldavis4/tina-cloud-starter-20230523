---
title: When You Shouldn’t Use Fitts Law To Measure User Experience
slug: fittss-law-and-user-experience
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c35869f-4887-4316-9dbb-80b72472b984/ux-10.jpg
date: 2012-12-04T13:18:03.000Z
author: anastasios-karafillis
description: >-
  The key statement of Fitts’s Law is that the time required to move a pointing
  device to a target is a function of the distance to the target and its size.
  In layman’s terms: **the closer and larger a target, the faster it is to click
  on that target**. This is easy to understand, not too difficult to implement
  and it doesn’t seem to make much sense to contradict such a simple and obvious
  statement.
categories:
  - UX
  - Navigation
  - Interfaces
---
The key statement of Fitts’s Law is that the time required to move a pointing device to a target is a function of the distance to the target and its size. In layman’s terms: the closer and larger a target, the faster it is to click on that target. This is easy to understand, not too difficult to implement and it doesn’t seem to make much sense to contradict such a simple and obvious statement.

![fitts law](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69791d95-c334-4db7-8e0c-9125a60cdafc/non-linear-progression-low-res.jpg "When You Shouldn’t Use Fitts Law To Measure User Experience")

However, before you start applying Fitts Law on every single pixel you can find, consider a few problems that might arise for you as an interaction designer.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Is User Experience Design? Overview, Tools And Resources](https://www.smashingmagazine.com/2010/10/what-is-user-experience-design-overview-tools-and-resources/)
*   [<span class="headline">The Elements Of The Mobile User Experience</span>](https://www.smashingmagazine.com/2012/07/elements-mobile-user-experience/)
*   [The Lean UX Manifesto: Principle-Driven Design](https://www.smashingmagazine.com/2014/01/lean-ux-manifesto-principle-driven-design/)
*   [Redefining Hick’s Law](https://www.smashingmagazine.com/2012/02/redefining-hicks-law/)

{{% feature-panel %}}

## Fitts’s Rule Number 1: Create Larger Targets

The likely most prominent statement derived from Fitts’s Law is that the <em>larger</em> a target, the faster it is to acquire.</p>

### The Benefits

Creating larger targets will facilitate interaction as well as allow you to get the most pixels out of your interface.

For example, some websites do not extend the clickable area of a button or link to the entire target. As a result, more precision is required to move the cursor to the respective link, which leads to slower navigation times. Fitts’s Law would suggest <a href="https://msdn.microsoft.com/en-us/library/ms993291.aspx/">utilizing every available pixel</a> to enlarge the clickable area and thus making it a larger target to click.

<img title="The target to the left lets a few pixels of screen real estate go to waste. The target to the right makes itself larger and quicker to click by exploiting every pixel at its disposal." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6718be1d-7151-4a80-9098-e56dbe29283d/fitts-buttons-1a.png" alt="The target to the left lets a few pixels of screen real estate go to waste. The target to the right makes itself larger and quicker to click by exploiting every pixel at its disposal." width="500" height="86" /><br>
<em>The target to the left lets a few pixels of screen real estate go to waste. The target to the right makes itself larger and quicker to click by exploiting every pixel at its disposal. (Left example: <a href="https://support.mozilla.org/en-US/products/firefox/get-started">Firefox</a>, Right example: <a href="https://www.apple.com">Apple</a>)</em>

Increasing the absolute or relative size of a button to make it easier to click is also a popular technique among designers for <strong>communicating priorities</strong> within the interface and prompting or calling users to perform a particular action.

<a href="https://www.libreoffice.org/"><img title="Relative and absolute size communicate priority within an interface." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aca7812e-87f0-44a5-b02d-db21a610cb32/libreoffice.jpg" alt="Relative and absolute size communicate priority within an interface." width="500" height="174" /></a><br>
<em>Relative and absolute size communicate priority within an interface. (Example: <a href="https://www.libreoffice.org/">LibreOffice</a>)</em>

Although there are <a title="Designing call-to-action buttons" href="https://www.smashingmagazine.com/2009/10/13/call-to-action-buttons-examples-and-best-practices/">many more considerations</a> to be factored in when designing a call-to-action button, Fitts’s Law provides one of its foremost theoretical foundations.</p>

### The Perils

The downside of large targets is, of course, that they can break the balance in your interface as well as quickly take up screen real estate. However, even if you have plenty of space to spare, you do not have to constantly enlarge your target areas to make them more usable since <a title="Improving usability with Fitts’ Law" href="https://sixrevisions.com/usabilityaccessibility/improving-usability-with-fitts-law/">the predicted usability of the size of a button progresses in a non-linear fashion</a>.

<img title="Good for your pixels: The usability of the size of a button is a non-linear relationship." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69791d95-c334-4db7-8e0c-9125a60cdafc/non-linear-progression-low-res.jpg" alt="Good for your pixels: The usability of the size of a button is a non-linear relationship." width="500" height="298" /><br>
<em>Good for your pixels: The usability of the size of a button is a non-linear relationship.</em>

Thus, if you make a small button 10% larger, it will become much more clickable, but if you make an already very large button 10% larger, you will not gain much more in terms of its usability.

## Fitts’s Rule Number 2: Minimize Cursor Movement

A second statement one can deduce from Fitts’s Law is that the <em>closer</em> a target, the faster it is to acquire.</p>

### The Benefits

If you place the links and buttons users are most likely to access on a regular basis next to each other, rather than distribute them across the interface, you will speed up interaction by reducing the amount of pixels the cursor will have to travel.

Consider, for example, the <a title="Unity" href="https://unity.ubuntu.com">Ubuntu Unity</a> interface. It allows you to browse various sources and use two different filters on the results: a <em>text filter</em> and a <em>file type</em> filter. However, notice in the picture below how far apart the two filters are. While the text filter is placed at the very <em>top</em> of the screen, the file type filter is placed at the very <em>bottom</em>.

<a href="https://2.bp.blogspot.com/-EGUtb1LeTOE/T5ajPHzYL1I/AAAAAAAAIrk/Gw8zWuozgm0/s1600/unity2d-dash-home-lens-ubuntu12.04.png"><img title="Fitts would disagree: Search filters are often accessed successively and should therefore be placed close to each other." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b81d3c1-b885-41a3-82a6-50e5f80c0ab2/unity.jpg" alt="Fitts would disagree: Search filters are often accessed successively and should therefore be placed close to each other." width="500" height="306" /></a><br>
<em>Fitts would disagree: Search filters are often accessed successively and should therefore be placed close to each other. (Example: <a href="https://unity.ubuntu.com">Ubuntu Unity</a>, Screenshot: <a href="https://www.webupd8.org/2012/04/ubuntu-1204-lts-released-see-whats-new.html">Webupd8.org</a>)</em>

For a fluent workflow, this arrangement is not optimal. When performing search queries, users often access the input field and file type filters in quick succession to adjust their search results. In order to do that here, the cursor would have to travel quite a distance. Instead, placing the file type icons next to the input field would have minimized cursor movement and sped up interaction (as well as freed up some vertical space).</p>

### The Perils

Arranging elements strictly according to this formula can cause conflict with other important design principles, such as the principle of <strong>grouping and separating different classes of functionality or content</strong>. Its purpose is to give your interface a clear and consistent structure as well as increase its discoverability.

Notice in the picture below how the various tools are sorted into small, meaningful groups: in this case <em>table</em> tools to the left and <em>insert</em> tools to the right.

<img title="Sorting interface elements into meaningful groups will give your interface a clear, consistent structure." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8bd10ab-8354-4000-99ac-0b87ac59d188/numbers-toolbar-1.png" alt="Sorting interface elements into meaningful groups will give your interface a clear, consistent structure." width="500" height="70" /><br>
<em>Sorting interface elements into meaningful groups will give your interface a clear, consistent structure. (Example: <a href="https://www.apple.com/iwork/numbers/">Numbers</a>)</em>

This allows users to create a familiar mental map of where to access a certain kind of information or tool. By contrast, if you analyzed the buttons purely by the frequency in which they are accessed, you would probably choose a different arrangement to minimize cursor movement. This, however, would break the functionally-consistent structure of your interface.

Another principle Fitts’s Law can interfere with is the principle of <strong>providing a clean and tidy interface</strong>. In order to clean up their interfaces, many websites group their content into drop-down menus. Although many designers <a title="Drop-downs and usability" href="https://www.useit.com/alertbox/20001112.html">raise objections</a> against their usability (a discussion of which would go beyond the scope of this article), drop-downs are nonetheless acknowledged as a visually elegant and space-efficient way to unclutter the interface and organize its content.

<a href="https://www.blurb.com/book-ideas"><img title="Drop-downs can help you structure your content and unclutter the interface." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/247e469a-8515-4969-9270-99e8740e0148/blurb-1.jpg" alt="Drop-downs can help you structure your content and unclutter the interface." width="500" height="258" /></a><br>
<em>Drop-downs can help you structure your content and unclutter the interface. (Example: <a href="https://www.blurb.com">Blurb.com</a>)</em>

The reason Fitts’s Law does not recommend the use of drop-downs is that they involve a longer cursor movement since users cannot access the target in a straight line. Instead, users will have to first click or hover over the drop-down menu, and then move the cursor down the list (and possibly across sub-menus as well) until they eventually reach the desired entry. But considering the benefits of drop-down menus, a longer cursor movement can be an acceptable trade-off.

A third, very important principle that may force you to defy Fitts’s Law is the principle of <strong>building forgiving interfaces</strong>, which aim to prevent and minimize the costs of mistakes.

Fitts’s Law suggests placing elements directly next to each other to minimize cursor movement, which would also save some space. However, saving those few pixels can result in users accidentally clicking the wrong item, especially when item boundaries are not easily discernible or when focused items are not highlighted distinctly enough.

<a href="https://codebeamer.com/cb/issue/35151"><img title="Accidents waiting to happen: the placement of interface elements can either cause or prevent mistakes." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed610a6b-a859-4696-8abb-896ab9de8fee/input-mistake.jpg" alt="Accidents waiting to happen: the placement of interface elements can either cause or prevent mistakes." width="389" height="92" /></a><br>
<em>Accidents waiting to happen: the placement of interface elements can either cause or prevent mistakes. (Example: <a href="https://codebeamer.com/cb/issue/35151">Codebeamer.com</a>)</em>

Be aware, though, that <strong>the consequences of mistakes are less severe when the elements represent navigational functionality as opposed to sharing or editing functionality</strong>.

If I open the wrong link, I can simply click the “Back” button to revert my mistake. Thus, when it comes to the links in your header or sidebar, there is no real harm in leaving no space between them.

When it comes to <em>navigating</em> during <em>consumption</em>, things can become more annoying. When playing video or audio files or displaying text files, accidentally clicking the “Stop,” “Eject,” “Next Item” or “Clear Playlist” buttons will require more effort on the users part to revert to the original state.

However, when it comes to <em>editing</em> and (especially) <em>sharing</em> functionality, mistakes can become downright destructive. If I click on a button such as “Send,” “Print,” “Delete,” “Download,” “Upload,” “Burn,” “Rip,” “Close,” “Shut Down,” “Connect,” “Disconnect,” “Accept” or “Decline,” my actions can be of much more severe consequences and may not be undone as easily.

Therefore, especially for elements with <em>editing</em> or <em>sharing</em> functionality, <strong>you should take precautions to minimize mistakes</strong> and the consequences of mistakes:

*   Offer easy ways to undo the performed action (one option: [temporary undo buttons](https://www.thepicky.com/internet/recall-email-that-is-send-undo-send-in-gmail/)).
*   Try to leave a few pixels of space between the buttons.
*   Make item boundaries clearly visible.
*   Highlight focused items.
*   Group buttons to [minimize the damage if a mistake occurs](https://www.codinghorror.com/blog/2010/03/the-opposite-of-fitts-law.html).

To give an example for the last point in the list: if I accidentally click on the “Get Mail” instead of the “Write Mail” button, the results are not dramatic, but do not place the “Reply” and “Delete” buttons next to each other.

A special type of input method aiming to prevent mistakes is the <strong>two-step input</strong> method. Two-step input methods are slightly less usable since the two steps entail a longer hand or cursor movement yet, as a consequence, they are more secure. The basic idea is that while you can accidentally perform both actions separately, it is unlikely that you will accidentally perform them successively. Take, for example, swipe-to-delete.

<img title="First swipe, then delete. While each on its own can easily be triggered by accident, they become a fail-safe mechanism when combined." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad4e6ea-23c7-439c-9a16-635fac639363/swipe-to-delete.jpg" alt="First swipe, then delete. While each on its own can easily be triggered by accident, they become a fail-safe mechanism when combined." width="500" height="176" /><br>
<em>First swipe, then delete. While each on its own can easily be triggered by accident, they become a fail-safe mechanism when combined. (Example: Timelogger App)</em>

I can imagine myself accidentally swiping from left to right or accidentally pushing a button, but not accidentally performing both actions in succession.

Two-step input methods lend themselves for mobile devices, which are more prone to accidental inputs. However, they can also be more space efficient in that the second step doesn’t need to be visible until after the first step has occurred.

So, whether swipe/tap, swipe/swipe or tap/tap combinations, two-step input methods make things a bit more difficult than just pressing a large button, but the inconvenience adds a little bit of security that is sometimes necessary to safely get your work done.

## Fitts’s Rule Number 3: Avoid Muscular Tension

The goal of <a title="Fitts' Law as a Research and Design Tool in Human-Computer Interaction" href="https://www.smpp.northwestern.edu/savedLiterature/FittsLawPapers/FittsLaw%20as%20Research.Design.Tool.in.HCI.MacKenzie.pdf">Fitts’s index of performance</a> (PDF) is to quantify the information capacity of the human motor system. In other words: it aims to rank input methods according to the amount of physical effort they require to execute a certain command.</p>

### The Benefits

The benefits of effortless input methods are most obvious when working with cumbersome devices. The most prominent example is vertical touchscreens, which are typically deployed in professional environments to create, visualize and manage large sets of data.

<img title="Fitts’s Law can facilitate and prolong interaction with vertical touchscreens." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60d3c205-b6dc-41f2-8054-7702098615a1/vertical-touchscreen.jpg" alt="Fitts’s Law can facilitate and prolong interaction with vertical touchscreens." width="500" height="511" /><br>
<em>Fitts’s Law can facilitate and prolong interaction with vertical touchscreens. (Example: Perceptive Pixel)</em>

When working with vertical screens, keeping your arms in an upright position can quickly tire the deltoid muscles and cause input mistakes or force the user to abandon the interaction. Therefore, avoiding complex and strenuous input techniques can facilitate and prolong the interaction with those devices.</p>

### The Perils

Input methods that are more difficult to perform can sometimes actually prevent mistakes. For example, mobile devices are often carried around in pockets, which can trigger commands by accident. In those situations, <strong>high-precision input</strong> methods are deployed, which use a higher input difficulty to make sure that a command is not executed accidentally. However, these input methods are also a way of making users aware of the severity of the command. Take, for example, the way an iPhone is turned off:

<img title="Choosing UI elements by the severity of their consequences: Slide controls for dangerous commands, buttons for harmless ones." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7e399d4-8f6b-4581-837d-66d0058fb448/iphone-off-1.jpg" alt="Choosing UI elements by the severity of their consequences: Slide controls for dangerous commands, buttons for harmless ones." width="240" height="344" /><br>
<em>Choosing UI elements by the severity of their consequences: Slide controls for dangerous commands, buttons for harmless ones. (Example: <a href="https://www.apple.com/iphone/">iPhone</a>, Screenshot: <a href="https://outsideinnovation.blogs.com/pseybold/2010/12/my-mortifying-ipad-experience.html">Outsideinnovation.com</a>)</em>

Powering off or rebooting the device are quite weighty commands; once triggered, they cannot be undone. Therefore, they are made into sliders, which require a higher precision. By contrast, the cancel command is of no comparable consequence here; hence it is made a button.

Slide controls and other gestures that require a higher precision are the most secure but also the most tedious input methods. Therefore, in order to balance security and usability, they are usually reserved for dangerous commands that are executed <em>infrequently</em>, such as unlocking the screen, turning off the device, setting system-wide preferences, performing administrative tasks or silencing wake up alarms. When dangerous commands are supposed to be executed <em>quickly</em> or <em>frequently</em>, for example when editing, deleting or transferring items, a well-spaced icon arrangement or two-step input method are more appropriate. Although they do not offer the exact same degree of security, they are still fairly secure yet much easier to perform.

A second reason to implement more awkward input methods is to <strong>take advantage of the space-efficient nature of gestures</strong>. According to Fitts’s index of performance, gestures, which involve some degree of dragging, <a title="A Comparison of Input Devices in Elemental Pointing and Dragging Tasks" href="https://www.billbuxton.com/fitts91.html">require a higher muscular tension</a>, which is why Fitts’s Law favors pointing-and-clicking. However, the advantage of gestures is that they trigger functionality without requiring UI controls.

Take, for example, the way you manage your art collection at <a title="Deviantart" href="https://deviantart.com">deviantART</a>. In order to add an item to your Favorites, you do not have to press a button. Instead, as soon as you start dragging a picture, a pane is displayed which you can drop it onto.

<img title="Dragging-and-dropping provides functionality without needing visible elements to trigger it." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b61452-177a-4ca7-9bad-3349e5ee72b7/deviantart-1.jpg" alt="Dragging-and-dropping provides functionality without needing visible elements to trigger it." width="500" height="254" /><br>
<em>Dragging-and-dropping provides functionality without needing visible elements to trigger it. (Example: <a href="https://www.deviantart.com/">deviantART</a>)</em>

Since dragging-and-dropping doesn't require buttons or other UI elements to trigger that functionality, it is very space efficient. The downside, of course, is that gestures do not offer any obvious visual clues as to their existence (except perhaps through tooltips). Nonetheless, if screen real estate is crucial, these input methods, although more difficult to perform, become almost a necessity.</p>

## Fitts’s Rule Number 4: Exploit The Prime Pixels

The concept of prime pixels states that some pixels are faster to acquire than others. Corners and edges of the screen are especially fast to access. However, the fastest-to-acquire pixel in any situation is simply the pixel at the current cursor position, which has lead to the introduction of the right-click context menu into human–computer interaction.</p>

### The Benefits

Context menus appear at the very pixel you right-click and provide you with context-sensitive options for the selected item. As a result, you do not have to move the cursor to a possibly distant fixed location in the interface. There are two kinds of context menus: <strong>linear menus and radial or pie menus</strong>.

Consulting Fitts’s Law will reveal that it favors radial menus over linear menus. The reasons: First, the wedge-shaped menu entries offer larger target areas. And second, because the menu has a circular shape, the pixels the cursor has to travel to reach either menu entry are always identical. This consistency allows users to create a more efficient muscle memory. By contrast, in linear menus only the menu entries closest to the initial cursor position are quickly accessible, which is why the most frequently performed actions should have those spots reserved for them.

<img title="Fitts’s Law favors radial over linear menus." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8019f9a0-cce8-4f4d-b91f-f757d10a18a3/menus1-e1350578121106.jpg" alt="Fitts’s Law favors radial over linear menus." width="500" height="250" /><br>
<em>Fitts’s Law favors radial over linear menus. (Left example: OneNote 2013, Right example: <a href="https://www.mozilla.org/en-US/firefox/new/">Firefox</a>)</em>

The benefits of placing items at the corners and edges of the screen are that the screen frame guides and positions the cursor once it reaches that location.

<img title="Corners and edges are prime screen real estate." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab7519ad-0567-457b-837e-e074c56e7de6/fitts-corners-and-edges-1a.jpg" alt="Corners and edges are prime screen real estate." width="500" height="170" /><br>
<em>Corners and edges are prime screen real estate. (Diagrams: <a href="https://www.particletree.com/features/visualizing-fittss-law/">Particletree</a>)</em>

The user could basically throw the cursor to a corner or edge to select the respective item without having to readjust the cursor position. The result: the targets will be much easier and faster to click.</p>

### The Perils

Empirical studies <a title="Radial vs. Linear Menus" href="https://www.donhopkins.com/drupal/node/100">confirm the theoretical assumptions</a> about radial and linear context menus, stating that seek time and error rates give the former a slight edge over the latter. Yet when the participants were asked purely about their subjective preferences, the pie menu was not favored anymore.

In fact, the pie menu, although favored by Fitts’s Law, does have a few disadvantages that can outweigh its benefits in certain situations.

One issue is that the <strong>circular menu shape quickly leads to small target areas when more menu entries are added</strong>. One way to deal with this problem is to remove redundant options, in line with <a href="https://www.smashingmagazine.com/2012/02/23/redefining-hicks-law/">Hick’s Law</a>. For example, if menu entries are not only applicable to the selected item, or if they are already accessible somewhere else in the interface, they do not have to be incorporated into the context menu as well (“Cut,” “Copy” and “Paste” always apply solely to the selected area as opposed to “Undo,” “Redo,” “New File,” “Save File,” “Print File,” or “Zoom In/Out” and thus lend themselves as fixed toolbar items).

A second way to manage a large number of options are sub-menus. While this is possible within radial menus, doing so will quickly clutter the screen and make them appear less organized than traditional linear menus. This is related to a very specific advantage of linear over radial menus: linear menus make it easier to express hierarchies via sub-menus as well as to group entries.

<img title="Grouping entries is more easily done in linear menus." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d335f5f-0aa6-49b7-b4f7-f590deab3960/linear-menu.png" alt="Grouping entries is more easily done in linear menus." width="500" height="83" /><br>
<em>Grouping entries is more easily done in linear menus. (Example: <a href="https://www.microsoft.com/office/preview/en/word-2013-preview">Word 2013</a>, Screenshot: <a href="https://www.pcpro.co.uk/blogs/2012/07/17/word-2013-review-first-look/">PCPro.co.uk</a>)</em>

Finally, circular menus take up more space. This can lead to two problems: they can obscure selected items, and they are more likely to pop up at places other than the current cursor position when triggered close to screen edges.

Therefore, in summary, you should consider a linear context menu over a radial menu if:

*   You have to integrate many options,
*   You have to work with sub-menus,
*   You want to group and rank menu entries,
*   Screen real estate is critical.

And finally, as to the corners and edges of the screen, two potential problems should be mentioned when working with mouse-operated devices. On large screens, the amount of pixels the cursor will have to travel can somewhat offset the aforementioned benefits. Also, Web designers will not be able to benefit from this rule because their content (except when in full-screen mode) is run in a browser window. As a result, they cannot take advantage of the edges of the screen and will almost necessarily have to opt for a more compact, centered layout.

However, when working with devices that are <em>not</em> mouse-operated such as touchscreens and styli, placing interface elements at the corners and edges of the screen will not only yield no positive results as to speeding up interaction. It can even have a detrimental effect. On large screens it would require users to constantly stretch their arms, which can tire them very quickly. Consequently, frequently accessed tools should be made into freely movable objects on large devices. Thus, users would be able to work more comfortably by placing these tools close to their preferred or <em>prime</em> hand position, which, incidentally, would be very much in line with Fitts’s Law.</p>

## Final Thoughts

The difficulty faced by interaction designers and user experience designers is that they have to consider, balance and combine measurable and non-measurable dimensions of user experience to create the best possible product. Fitts’s Law tries to help user interface designers by giving them easily quantifiable, mathematically accurate values to base their design decisions on.

Of course, it is often possible to measure the quality of an interface using mathematical values: The fewer clicks required to access a certain set of data, the faster the navigation. The more vertical pixels a horizontally aligned interface preserves, the better it is suited for the respective device orientation. The closer the most frequently accessed buttons are placed, the more economic the cursor movement.

However, since <strong>interfaces are designed for humans</strong>, they also have to be consistent, considerate, inclusive, playful and discoverable: qualities that can hardly be measured as easily as clicks or pixels. The stunning accuracy and simplicity of mathematical formulas may sometimes lead designers to favor the measurable over not-so-easily-measurable dimensions. And while mathematical formulas can, indeed, help you enrich user experience, you should treat those formulas as <em>tools</em>, not as <em>principles</em>.

Instead, you should debate and choose anthropological principles first, and, if they permit it, use formulas such as Fitts’s Law as much as possible to actually improve user experience.</p>

## Further Reading

Resources you might be interested in:

*   [Fitts’ Law: Modeling Movement Time in HCI](https://www.cs.umd.edu/class/fall2002/cmsc838s/tichi/fitts.html) A brief overview of Fitts’s Law.
*   [The Information Capacity of the Human Motor System in Controlling the Amplitude of Movement](https://www.smpp.northwestern.edu/savedLiterature/FittsLawPapers/Information%20Capacity%20of%20Human%20Motor%20System%20Controlling%20Ampltude%20of%20Movement.Paul.Fitts.pdf) (PDF) Paul Fitts’s original article published in the Journal of Experimental Psychology in 1954.
*   [Visualizing Fitts’ Law](https://www.particletree.com/features/visualizing-fittss-law/) A list of diagrams visualizing the basic rules of Fitts’s Law.
*   [Fitts’s Law as a Research and Design Tool in Human-Computer Interaction](https://www.smpp.northwestern.edu/savedLiterature/FittsLawPapers/FittsLaw%20as%20Research.Design.Tool.in.HCI.MacKenzie.pdf) (PDF) A case study comparing the efficiency of various input methods.
*   [An Empirical Comparison of Pie vs. Linear Menus](https://www.donhopkins.com/drupal/node/100) A controlled experiment testing the seek time and error rates for pie versus linear menus.
*   [A Quiz Designed to Give You Fitts](https://www.asktog.com/columns/022DesignedToGiveFitts.html) A small quiz to test your knowledge of Fitts’s Law.

{{< signature "cp" >}}

