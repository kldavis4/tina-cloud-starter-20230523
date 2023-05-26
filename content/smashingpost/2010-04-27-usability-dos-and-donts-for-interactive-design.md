---
title: Usability Do's And Don'ts For Interactive Design
slug: usability-dos-and-donts-for-interactive-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/870ea535-9f4c-42d5-8e85-5007e39393d7/02-diagram-sketched-opt.jpg
date: 2010-04-27T11:43:45.000Z
author: ben-macgowan
description: >-
  We often talk about how to make our websites more usable, whether it's
  tweaking the HTML structure of pages to benefit the user’s process or figuring
  out how best to display a message via CSS. But we never bring this thought
  process into our jQuery-based (and other JavaScript-based) elements. How can
  we enhance the user experience and usability of our jQuery events?
categories:
  - UX
  - Web Design
---
We often talk about how to make our websites more usable, whether it's tweaking the HTML structure of pages to benefit the user’s process or figuring out how best to display a message via CSS. But we never bring this thought process into our jQuery-based (and other JavaScript-based) elements. How can we enhance the user experience and usability of our jQuery events?

Below, we'll briefly discuss ways to look at the code and the result of our interactive designs and, thus, improve their usability.

You may want to take a look at the following related posts:

*   [30 Usability Issues To Be Aware Of](https://www.smashingmagazine.com/2007/10/09/30-usability-issues-to-be-aware-of/)
*   [12 Useful Techniques For Good Interface Design](https://www.smashingmagazine.com/2009/01/19/12-useful-techniques-for-good-user-interface-design-in-web-applications/)
*   [10 Useful Web Application Interface Techniques](https://www.smashingmagazine.com/2009/01/12/10-useful-web-application-interface-techniques/)
*   [Beyond Usability: Designing With Persuasive Patterns](https://www.smashingmagazine.com/2015/10/beyond-usability-designing-with-persuasive-patterns/)

## Don't Leave Users In The Dark

Most if not all jQuery is fired through events from the user, whether it's loading new content, posting forms or simply modifying the presentation of an item. Such events are fired through a click from the user.

{{% feature-panel %}}

While as designers and developers we would know that something is happening, without a visual representation, the user is left guessing what is going on. If the user clicks an element and nothing occurs immediately, they could wonder whether the page is broken or they have done something wrong.

But by simply displaying a message or loading graphic for the user, they are <strong>assured that something is happening</strong> and that their action will be completed shortly.

<a href="https://pinchzoom.com/">Pinchzoom</a> offers a consistent experience when loading new content by displaying a spinning graphic alongside the word "Loading." The constant motion of the graphic tells the user that the website is working on their request.

<a href="https://pinchzoom.com/"><img title="Pinchzoom offer a rotating graphic and text in a modal box to draw user’s attention and inform them that content is loading" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eee2f33f-4271-428c-8de3-b6d3314a28fb/pinchzoom-loading.jpg" alt="Pinchzoom offer a rotating graphic and text in a modal box to draw user’s attention and inform them that content is loading" width="500" height="200" /></a><br>
<em>Pinchzoom shows a rotating graphic and text in a modal box to catch the user’s attention and tell them that content is loading.</em>

## Always Put Your Code To The Test

As part of any testing process, designers make sure that their interactive design will work across multiple browsers. Unfortunately, we do not test our design elements by using them as a normal user would. You’d be surprised how differently we use our own websites.

Users vary widely in their behavior and viewing set-ups, so don't be reluctant to use your design in different ways and with different set-ups.

By trying to break your JavaScript, you could come across bugs that you didn't notice before, which will lead you to <strong>create a stabler and more solid user experience.</strong> Coming across an element that appears to be broken or not functioning correctly will often make users lose trust in the website as a whole.</p>

## Don't Add jQuery At The User's Expense

One of the last things you want is a confused user. Adding too many interactive elements can make the user unable to decide what to do or how to find what they need.

When building your website, <strong>restrict the number of controls</strong> to those that will help the user achieve their goal. By restricting choice, you create a much more effective user experience.

An example of this problem can be seen on the Crispin Porter + Bogusky website. This website has a lot of scrolling navigation and many "Read more" links that load more content on the page. This overloads the user with information. New users might be unsure what to do, where to go or if they've missed important information.

<img title="Crispin Porter + Bogusky website displays too much information and options for the user at once" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85f842cf-33d7-4261-b118-136d9a926d9e/crispinporter-overloading-information.jpg" alt="Crispin Porter + Bogusky website displays too much information and options for the user at once" width="500" height="375" /><br>
<em>Crispin Porter + Bogusky shows too many options at once.</em>

## Speed Isn’t Always Key

We always optimize our code to load pages faster and help users complete their tasks more quickly. On the other hand, there are instances when slowing down animations could improve the usability of a website.

Animations such as those showing rotation through messages or pictures are often set too fast. We must remember that users don’t want to be rushed. Give them time to take everything in. A user shouldn't be halfway through reading an item and then have to wait for it to rotate before being able to finish.

Whether you use a plug-in to generate the effect or core jQuery code, settings should be available to change the speed of the animation. In most cases, keywords such as “slow” or “fast” can be used. If you wish to be more exact with your timings, numeric values such as “800” or “1200” are available, which would specify time in milliseconds.

The home page of <a href="https://www.postbox-inc.com/">Postbox</a> features a rotating list of news and key items. Though not a prominent feature of the design, the delay between each item is long enough to <strong>allow the user to fully absorb the information</strong>.

<a href="https://www.postbox-inc.com/"><img title="Rotating messages featured on the Postbox homepage" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5e476be-d3f9-45da-b99c-223be7a16000/postbox-rotating-messages.jpg" alt="Rotating messages featured on the Postbox homepage" width="500" height="350" /></a><br>
<em>Rotating messages on the Postbox home page.</em>

## Make Tabs More Prominent

Though more of usability tip for design, this deserves mention nonetheless. If you are using tabs to show and hide content, make sure they are prominent and that each tab describes its content well.

Tabs are a great space-saver and some say they allow for more creativity in a design. But don’t risk the user <strong>overlooking potentially important content</strong>.

By making tabs prominent, you enable users to find more information easily should they need it. Also, being more descriptive in your labeling makes clear to the user what they should expect to see.

<a href="https://www.delibarapp.com/">Delibar</a> styles its tabs as bookmarks. The bold green draws the user’s attention. Delibar uses one-word labels to succinctly convey the product features and content behind the tabs. For example, the "Manage" tab leads to content that describes the numerous ways that users can manage their Delicious bookmarks using Delibar.

<a href="https://www.delibarapp.com/"><img title="Prominent tabs from Delibar draws the user’s attention so that they do not miss any important information about the product" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e534f55f-a0df-4b13-a9bc-0b92fc934ab6/delibar-tabs.jpg" alt="Prominent tabs from Delibar draws the user’s attention so that they do not miss any important information about the product" width="495" height="300" /></a><br>
<em>Prominent tabs draw attention so that users do not miss important information.</em>

## Don’t Take Control Away From Users

One-page websites with smooth scrolling (horizontal and/or vertical) are a growing trend now. But don't leave users stuck should they not want to use the navigation you provide.

Users who realize that the page extends beyond the fold will likely try to use their mouse or scroll bar to navigate down. Removing scrolling just shows how taking away basic browsing functionality (and thus taking control away from the user) can impair the overall experience. Users will feel that they are <strong>not in control of their own browsing</strong>.

If you are including page scrolling in your design, you could improve usability by providing keyboard navigation and shortcuts. This provide another option by which users can navigate the page. Now they'll have the scroll bar, the mouse and the keyboard. jQuery for Designers has a tutorial on adding keyboard navigation using jQuery.

When deciding how your design and its jQuery should function, think of how your choices might impede basic functionality and how users might react to that.

While providing links to navigate down the page, <a href="https://www.designinsocial.com/">designinsocial</a> does not let users browse freely with their mouse or scroll bar. As you can see below, content exists below the fold and users will want to scroll down.

<a href="https://www.designinsocial.com/"><img title="Screenshot of designinsocial at 1024x768 screen resolution" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33441b75-7061-46a4-90fe-403914eff04a/designinsocial-control.jpg" alt="Screenshot of designinsocial at 1024x768 screen resolution" width="500" height="375" /></a><br>
<em>Screenshot of designinsocial at 1024 x 768 pixel resolution.</em>

## Use jQuery To Improve Form Validation

jQuery can easily improve form validation and can be triggered either by the "Submit" button or by the user focusing off a field (<code>.blur()</code>). But remember that JavaScript form validation should never entirely replace server-side validation.

Using jQuery to help validate forms can have two very important benefits to users:

1.  The user won't have to wait for the page to reload to learn that they made an error. Also, if the page has to reload before an error message is displayed, the user might assume that their submission was successful and overlook the message.
2.  jQuery allows for easier and **more effective error highlighting**; for example, by changing the border and background color of relevant inputs or by using animation, such as a tooltip, to catch the user's attention.

Trevor Davis has an informative article entitled "<a href="https://trevordavis.net/blog/tutorial/ajax-forms-with-jquery/">AJAX Forms with jQuery</a>," which has some great tips on implementing form validation with jQuery.

<a href="https://www.blueskyresumes.com/"><img title="Blue Sky Resumes comment jQuery form validation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640483e6-f8c9-495b-b9e7-6b8f655b004c/blueskyresumes-formvalidation.jpg" alt="Blue Sky Resumes comment jQuery form validation" width="500" height="445" /></a><br>
<em>jQuery form validation for comments on Blue Sky Resumes.</em>

<a href="https://www.blueskyresumes.com/">Blue Sky Resumes</a> uses jQuery on its blog comment form by changing the background and border color to highlight input fields with errors. A validation summary also appears above the form to further explain the error.</p>

## Prevent Animations From Stacking

One of the great features of jQuery is that it allows you to enhance a design by animating elements. This includes fading, changing colors and moving elements. One jQuery animation, often used to de-clutter an interface, is to hide information such as image captions and then display it on hover.

<a href="https://www.cssbake.com/"><img title="CSSbake uses jQuery animations to display an item’s title and rating once you rollover the screenshot" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f137446-89b7-4963-97f2-18d12380fb80/cssbake-animation.jpg" alt="CSSbake uses jQuery animations to display an item’s title and rating once you rollover the screenshot" width="500" height="375" /></a><br>
<em>A CSS showcase uses jQuery animation to display an item’s title and rating when you roll over the screenshot.</em>

One problem that many designers and developers overlook, though, is that such animations can quickly "stack." When a page has many thumbnails, and a user quickly hovers over several at a time, then the animation will drag behind one by one, even though the user has stopped moving their mouse. Hovering over the four panels on <a href="https://www.druckbar.info/">druckbar</a> demonstrates this problem.

You can use one of two solutions to save users from this hassle. The first is the <a href="https://api.jquery.com/stop/">.stop()</a> function. When <code>.stop()</code> is called on an element, the currently running animation (if there is one) is immediately stopped. For instance, for an element hidden with <code>.slideUp()</code>, when <code>.stop()</code> is called, the element will be displayed but at a fraction of its previous height. Callback functions are not called.

CSSbake uses the following function in the example shown above to prevent animations from stacking:

<pre><code class="language-javascript">$("ol#gallery li").hover(function () {
$(".thumb-meta", this).stop().animate({ bottom: '0px' }, 400);
},
function () {
$(".thumb-meta", this).stop().animate({ bottom: '-22px' }, 400);
});</code></pre>

Alternatively, you could use a jQuery plug-in such as <a href="https://cherne.net/brian/resources/jquery.hoverIntent.html">hoverIntent</a>, which fires an animation only if the user's mouse slows down enough, making it obvious that they are intentionally hovering over an element.</p>

## Keep Content Animation To A Minimum

Because JavaScript functions are so easy to implement with jQuery, many of us easily get carried away with animations, causing disruption for the user. Some websites use jQuery to load images as the user scrolls down the page, thus making the initial page load faster and allowing users to access content more quickly. <a href="https://mashable.com/">Mashable</a>, a popular social media news website, does this. While this is great for users who have a slow Internet connection, it does have its drawbacks.

The fade-in animation tied into this technique can be quite distracting for the user. If a user is steeped in an article, the fade-in as they scroll down might break their flow. It would be more effective if the image loaded with no animation, ideally just before the image area came into the viewport, to avoid disruption.

So, think about how animation and other jQuery functionality will affect the user's ability to concentrate on the main content.</p>

## Conclusion

jQuery’s ever-growing popularity has brought to light the wide range of possibilities it offers. The points discussed here are just a handful of the current trends in interactive design. As you would with any design element, <strong>think of how your decisions will affect users</strong>. Is the element easy to use? Are the processes easily understandable? If something goes wrong for the user, how might they react? Questions like these can help iron out errors, giving users a more solid interactive design and user experience.</p>

## Showcase Of Websites With Effective jQuery

<a href="https://crushlovely.com/">Crush + Lovely</a>
Crush + Lovely uses jQuery to create a smooth scrolling effect when a navigation item is clicked. The user experience is enhanced through keyboard navigation: the left and right arrow keys scroll the page between sections.

<a title="Crush + Lovely" href="https://crushlovely.com/"><img title="Crush Lovely page navigation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12c68df7-e3e6-44e8-af77-9a3d808befb1/crushlovely-navigation.jpg" alt="Crush Lovely page navigation" width="500" height="375" /></a>

<a href="https://shauninman.com/pilation/">Shaun Inman</a>
Shaun Inman uses jQuery to highlight the item that the user is hovering over. The other animations make the interface and experience more fun for the user.

<a title="Shaun Inman" href="https://shauninman.com/pilation/"><img loading="lazy" decoding="async" class="39622" title="Shaun Inman navigation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bcc3f27-5648-40ff-8141-21f02aa5d5e5/shauninman-navigation.jpg" alt="Shaun Inman navigation" width="500" height="375" /></a>

<a href="https://www.robocatapps.com/">Robotcat</a>
Robotcat reinforces its newsletter sign-up form validation with jQuery, by highlighting any errors. Form fields are highlighted with a prominent red border.

<a href="https://www.robocatapps.com/"><img title="Robocat form validation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0db3c802-2a23-4a48-976a-11fe3d794f08/robocat-form-validation.jpg" alt="Robocat form validation" width="500" height="300" /></a>

<a href="https://panelfly.com/">Panelfly</a>
Panelfly features tabbed content in its high-impact design so that the user does not miss important content.

<a href="https://panelfly.com/"><img title="Panelfly tabbed content" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3669dc32-0021-4af3-ba1d-8d2b384c5e1e/panelfly-tabs.jpg" alt="Panelfly tabbed content" width="500" height="270" /></a>

<a href="https://www.ormanclark.com/">Orman Clark</a>
Orman Clark's portfolio has fixed navigation and jQuery that create smooth scrolling between the sections of the one-page design, while still allowing the user to move with the scroll bar or mouse.

<a href="https://www.ormanclark.com/"><img title="Orman Clark's portfolio navigation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dcbc338-714d-4dc9-9eec-8c84dc522f55/ormanclark-navigation.jpg" alt="Orman Clark's portfolio navigation" width="500" height="375" /></a>

<a href="https://koormann.de/">Jan-Eike Koormann</a>
Jan-Eike Koormann uses jQuery and AJAX to load items in his portfolio. When an item is loading, a graphic lets the user know that something is happening.

<a href="https://koormann.de/"><img title="Jan-Eike Koormann loading portfolio item" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b83833aa-207f-42f7-9507-7534c962cf55/janeikekoormann-loading.jpg" alt="Jan-Eike Koormann loading portfolio item" width="500" height="375" /></a>

<a href="https://www.yaypaul.com/">YAY Paul</a>
YAY Paul uses hover events to animate and display the titles of his portfolio pieces. Using the methods described above, Paul West prevents animations from stacking.

<a href="https://www.yaypaul.com/"><img title="YAY Paul hover animations" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98567f96-03f8-4d8a-99c2-600f95d9c613/yaypaul-hoverevents.jpg" alt="YAY Paul hover animations" width="500" height="295" /></a>

<a href="https://icondock.com/">IconDock</a>
IconDock uses jQuery to create a unique and playful experience when the user adds items to the cart. In addition to being able to click the "Add to Cart" links, users can drag icon images to the cart. A loading graphic lets users know that the cart is being updated.

<a href="https://icondock.com/"><img title="IconDock cart animations" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8784ae3-bd3a-4ebb-a1b7-733ffbae7fd2/icondock-cart.jpg" alt="IconDock cart animations" width="500" height="375" /></a>

## Useful Resources

*   [45+ New jQuery Techniques For Good User Experience](https://www.smashingmagazine.com/2009/01/15/45-new-jquery-techniques-for-a-good-user-experience/)
*   [9 Common Usability Mistakes In Web Design](https://www.smashingmagazine.com/2009/02/18/9-common-usability-blunders/)
*   [10 Usability Nightmares You Should Be Aware Of](https://www.smashingmagazine.com/2007/09/27/10-usability-nightmares-you-should-be-aware-of/)
*   [jQuery and JavaScript Coding: Examples and Best Practices](https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/)

{{< signature "al" >}}

