---
title: 'A Comprehensive Website Planning Guide (Part 3)'
slug: comprehensive-website-planning-guide-part3
author: ben-seigel
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4291462c-673a-4b9e-8922-6e1569f0eac5/newharvesthomedesktop-screenshot.jpg
date: 2018-03-06T12:40:40+01:00
summary: >-
  Planning is essential for most businesses and organizations. Unfortunately, when it comes to websites there is often a failure to plan properly or at all. This guide aims to change that.
description: >-
  Planning is essential for most businesses and organizations. Unfortunately, when it comes to websites there is often a failure to plan properly or at all. This guide aims to change that.
categories:
  - Web Design
  - Workflow
  - Business
  - Clients
  - Planning
---
<p>In <a href="https://www.smashingmagazine.com/2018/02/comprehensive-website-planning-guide-part2/">Part 2</a>, I covered the details of evaluating a plan, choosing web professionals, and determining your website structure. The question of why planning for the web is just as important as planning for anything else associated with your business was covered in <a href="https://www.smashingmagazine.com/2018/02/comprehensive-website-planning-guide-part1/">Part 1</a>, so head on back to read that part first in case you missed it. In today's final part of this guide, I'll start with a few of the most common approaches in any initial design.</p>

## Initial Design: Three Common Approaches

<p>There are, of course, others, including hybrids which combine elements of each, and every design team and every project is different, but there are core approaches to creating a web design.</p>

### 1. Classic Photoshop mockup approach

<p>Commonly created in Adobe Photoshop (the industry standard) or other design software such as Sketch, the initial design will consist of a visually accurate image ("mockup") of the home page and at least one internal page.</p>

<p>Your business' visual branding elements should be applied here. If you have well-defined graphics in addition to your logo, they will dictate the design of the site. However, if your brand lacks detail, the designer will do their best to create work that accurately reflects the business, working with your existing graphics as a jumping off point.</p>

<p>Following is a short list of key points for successful mockups. We'll assume the designer is working in Photoshop, however, these guidelines also apply to other design programs.</p>

<ul><li>Start with a pre-made grid with pre-drawn, pixel-accurate guides. Some designers create their own, while others may adhere to a pre-set grid system. Whatever the case, it's important to have a clean template to start. Make your canvas wider than the width you're designing to, so you can add notes on one side and get a feel for what the site feels like when floating in a wide browser window.</li>

<li>Add the color palette and basic branding elements (i.e., fonts) in the margins of the canvas so you'll have it for reference when viewing on screen or in print.</li>

<li>Draw everything to exact pixels, and draw clear guides and/or slices around design elements. This becomes critical when the front end developer later creates the HTML from the mockup, however, your design will only be pixel-accurate when displayed on a ‘big screen' device.</li>

<li>Organize all design elements with a logical folder/subfolder structure, and label each item clearly.</li>

<li>If the designer will be handing off their files to an HTML developer, this is especially important. Name your folders and layers for their content so there's no confusion later. For example: "Sidebar &mdash; events header" is clear, "Layer14 Copy Copy Copy" is not.</li>
</ul>

{{% feature-panel %}}

<ul>
<li>Make clear notes dictating fonts, alignment, repeating background elements, gradients and anything that will need to be implemented with CSS techniques. In Photoshop, the sticky note feature is good for this. If unclear, ask the person who will be converting your design into a working page.</li>

<li>If using a common style for headers, navigation, or other design elements that appear throughout the site, consider making separate Photoshop documents for them. Some designers find it easier to "chunk it down", especially in big projects.</li>

<li>Use realistic content. Designers often use greeking ("lorem ipsum") to fill space, which is ok for body copy. However, for headlines, titles, events, etc., try to use realistic copy. Consider the two following headlines. Layout considerations are different for each:
<ul>
	<li>"Widgets, Inc. Wins Green Manufacturing Award"</li>
	<li>"Widgets, Inc. Employees Win Landmark Court Case Affirming Employee Right To Petition For College Tuition Reimbursement When Training Is Relevant To Work Role"</li>
</ul>
</li>
</ul>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6beea21d-c55d-4155-90e1-834744c4e79c/newharvesthomedesktop.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6beea21d-c55d-4155-90e1-834744c4e79c/newharvesthomedesktop.jpg'>Large preview</a>" alt="" >}}

#### The problem with this method

<p>When you design pixel-perfect mockups, you can be assured that the website's appearance will be very close on the desktop web &mdash; but that's it. The minute you switch to a different device, it will change. So at the very least, you'll want to either convey to the business how the design will change as it is viewed on smaller screens (tablet, smartphone) by showing a site with similar layout, or design additional mockups at common screen sizes. As you can imagine, this is a lot of additional design work, and if you change an element on the desktop-focused mockup, you'll have to change it on the others too. Here's the smartphone view.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37a06782-3344-4315-a768-8c96106131c7/newharvesthomephone.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37a06782-3344-4315-a768-8c96106131c7/newharvesthomephone.jpg'>Large preview</a>" alt="" >}}

### 2. Design in the browser

<p>With the rise of responsive web design, some designers are moving away from the Photoshop mockup approach, instead using responsive frameworks like Bootstrap or Foundation, or tools like <a href="https://froont.com/">Froont</a> or <a href="https://typecast.com/">Typecast</a>. These tools allow very rapid, iterative design that allows you to see how the site will look on different devices.</p>

<p>You may still use Photoshop or other graphic design tools to create stylized elements to place within the design, but the bulk of the design will happen outside these tools. There is no good way to show the business "exactly what it will look like" so for designers used to making pixel-perfect mockups for the desktop web, in-browser design may not be the best approach. For many, this method also represents a major change to their process and can take a while to get the hang of. Most see this as a necessary evolution, since a Photoshop mockup can only represent one of the many "frames" in which your site's content is displayed, and the world of web is moving rapidly toward designing for multiple platforms from the get go.</p>

<p>When it's time to write the HTML, CSS and Javascript that will make up the site, you can either stick with the framework you used initially to create your design iterations, adapt its code, or write your own from scratch, using your framework designs as a guide.</p>

### 3.Element collage (also know as style tile, style collage)

<p>With this approach, the designer will assemble a range of elements that make up a website including header, navigation, icons, sample photography, illustrations, forms, interactive elements, and anything else deemed necessary to get a good sense of the site's look and feel. Additionally, depending on the design tool, these elements may be laid out in such a way as to show how their appearance will change in unison with the screen size. This is typically combined with some kind of graphic mockup of at least the home page and few internal pages. (It can be hard for businesses to visualize how pages in a site will look based solely on an element collage.)</p>

<p><strong>Note:</strong> These sample images are not to scale &mdash; our Photoshop version of the element collage is one long page, 1500X4500 pixels, so we can't fit it here in one piece.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9bd76c8-1b6b-405e-9523-019f9ae8b185/newharveststylecollage.jpg" sizes="70vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9bd76c8-1b6b-405e-9523-019f9ae8b185/newharveststylecollage.jpg'>Large preview</a>" alt="" >}}

<p>For designers (and businesses) long used to the Photoshop mockup method, this is also a new frontier, and requires a change in perspective. With a style prototype, you're not trying to layout a page exactly, but rather, to show the key parts of the site and get feedback on the general look and feel. Because a responsive site must change in appearance radically as the screen size changes, this method is much more about about the parts of a site and getting a feel for the direction the design is heading. You're not showing the site as a whole, let alone making a pixel-perfect representation of exactly how each and every page will look.</p>

<p>This can save a lot of time, but again, if the business isn't comfortable (or trusting) enough to let the designer make structural decisions later on down the line, this method may be a tough sell. That said, it really can create a flexible environment in which to rapidly create web designs for myriad platforms.</p>

<p>While the principles of graphic design are timeless, the approaches used for website design will change and evolve over time. I highly recommend you watch <a href="https://typecast.com/seminars/post-comp">Design Deliverables for a Post-Comp era</a> to discover the value of this approach.</p>

<p>When using this the element collage method, the business must accept there is no exact, precise, final draft of a given page, only layout guidelines to agree upon. The very nature of responsive sites is to adapt their content to the capabilities of each device, so the businessmust not expect to approve set-in-stone layouts prior to the development phase. With an approved style prototype, a designer may want to return to wireframes or working prototype to work out all the layouts your project requires. Then when it comes to build the site, you will assemble the elements of your collage into the visual structure of each unique layout.</p>

<p>There is much discussion and debate in the design community about the best tools, methods, and process for creating web designs. Designers tend to feel very strongly about which is the "best" method, and while that's understandable, it's important to use the most suitable process for the project and the business. It's smart for designers to get comfortable working with an array of methods and systems, and broaden their horizons when a project allows.</p>

<blockquote><strong>Author's note</strong><br />

I was very hesitant to include some of the following content, because it highlights serious tensions in the business-designer relationship. While it may seem overly critical of business owners, I believe it is of great value to businesses because so much time and money is at risk in a website project.<br />

In the interest of diplomacy and preserving client relationships, designers probably won't voice these frustrations to business owners, but the following issues can and do derail projects.</blockquote>

#### Design approval and revisions

<p>Regardless of which design method was chosen for the project, when the design is complete, the results are are shared with the business for approval, and there is often a (hopefully short) revision process. The revision process involves the the designer and key stakeholders going back and forth a few times, trying different edits to the design until the design is approved.</p>

#### Design by committee: don't do it.

<p>A common (and completely avoidable) problem at this stage is the consideration of too many opinions, simply having too many cooks in the digital kitchen.</p>

<p>To help ensure a smooth process, the business must assign one person as the point of contact for the design team. That person is responsible both for communicating with the designer and for making final decisions about design direction.</p>

<p>Certainly, it is important to solicit feedback on design, and project stakeholders have valuable critique to offer, helping guide the design process so that the end result accurately represents their business.</p>

<p>Additionally, in some instances, review by legal and/or technical staff is needed. However, <strong>having the entire company offer input, and lending equal weight to all feedback leads quickly to nobody being satisfied</strong>. The best possible way to ensure a muddy, unfocused design is to give everybody input and then to run around making all the changes proposed.</p>

<p>Generally speaking, in small businesses or organizations, having any more than five people provide design feedback is a recipe for gridlock. The fewer the better, five is the maximum. These five (or fewer) people will solicit feedback from their subordinates or department colleagues, but that input should be compiled by each stakeholder and presented as a unified, single opinion. In other words, don't invite fifteen people to a design review meeting. Weed out all the back and forth before you go to the designer with input.  <strong>It's also very important to distinguish between objective design concerns ("does this color scheme really suit our bakery?") versus personal design preferences ("I love the color blue &mdash; let's use a lot more blue")</strong>.</p>

<p>Design is not an arbitrary pursuit. There is good design and bad. There are rules to be followed, best practices to be adhered to, and as long as planning has been done properly, design decisions are almost never really a matter of taste. That is, there's a good reason the designer used that exact blue, in that exact spot, or that font at that size. All of those little choices communicate things to the user. They may feel insignificant, but in reality, all these choices the designer makes are important. They can drastically affect the way the site functions and how it is received. Unfortunately, many businesses fail to understand that just because they like it doesn't mean everybody else will, and doing what's best for conveying the soul of the business is what the designer is hired to do. Opinion shouldn't enter into it unless absolutely necessary.</p>

#### When egos rule

<p>Any experienced designer has dealt with decision makers who have the dreadful combination of strong ego and poor design sensibility. In the worst case, designers will be asked to use a logo the CEO developed in Microsoft PowerPoint, or colors and fonts totally unsuited to the business' image. This, unfortunately, comes with the territory of being a designer. Sometimes it's possible to diffuse this by placing the offending artwork in a grid alongside professionally designed material from competitors or similar companies in the industry &mdash; Pinterest is a good tool for this.</p>

<p>If a competitive review was part of your needs assessment, you may want to refer to their brands for reference. The hope is that the business can see how awful their version looks next to the competition and rethink their commitment to the bad idea. Ultimately, however, decision makers can and do ruin projects by insisting, contrary to all available evidence, that their design sense should take priority over established design principles.</p>

#### Help! They won't budge!

<p>Readers of an earlier version of this book asked for ways to deal with the ego problem. I wish I had a clever or useful answer for you. Suffice to say this is a problem with people, not technology. Make your best case for the value of good design, fight your best fight, then be prepared to let it rest.</p>

### Design tension: designer vs. the business

<p class="c-pre-sidenote--left">Designers often deal with tension between their informed concepts of design and business' uninformed design critiques. This is best illustrated by the "bad idea" conundrum. The business will request a design feature that's either ugly, unworkable, or just a bad idea. (This is so common that there are many websites which chronicle clueless businesses and the headaches that result in this dynamic<sup>1</sup>.) The designer will respond somewhere on the continuum between "that's horrible, we won't do it" and "well, if that's what you prefer...". This response is dependent on a variety of ever-shifting factors, including:</p><p class="c-sidenote c-sidenote--right"><sup>1</sup><a href="https://clientsfromhell.net/">https://clientsfromhell.net</a>, <a href="https://theoatmeal.com/comics/design_hell">https://theoatmeal.com/comics/design_hell</a></p> ￼

<ul><li>When designer hopes to get paid.</li>

<li>How emotionally invested designer is in the project.</li>

<li>How much time the designer has invested in the design phase, and how much delay will result from implementing the bad idea.</li>

<li>How high the stakes are &mdash; how much damage the bad idea will do to the site as a whole.</li>

<li>Personality, businesses' willingness to take constructive counsel about their ideas.</li></ul>

<p class="c-pre-sidenote--left">Every project is different. When designers deal with businesses who continually request features that are ill- advised, at some point they may write off the project altogether. At a certain point, it's just too exhausting to continually explain why centered, bold paragraphs in red, WRITING IN ALL UPPERCASE, crazy Flash animations or poor quality photography make an ineffective website<sup>2</sup>. The designer's attitude rapidly shifts from "let's make something really great that we're proud of" to "let's just get it done so we never have to look at this again."</p><p class="c-sidenote c-sidenote--right"><sup>2</sup>Other mood killers include autoplay videos and fonts most often used in children's books.</p> ￼

<p>While considering the above, also realize that there's another side to this coin. People problems can also crop up on the designer end of the spectrum. Some designers' skills may not be up to par, they may refuse to listen to valid criticism of their work, or may not value the informed input of the business. A good way to avoid this is by getting good references from designers' past clients.</p>

#### Consider the content

<p>Think about expansion. For example, you may have a news section. To start, you have six news items. That's fine. You'll make a main news page with summaries and link the summaries to a detail page. But what happens when you have ten, twenty, or fifty news pieces? Now there are other considerations. Do you want to archive old news? Create pagination? Only show the most recent ten items? This should be considered in the design process. Plan around content as much as possible in the design process, and think ahead wherever you can &mdash; plan for the content you will have, not the content you have right now.</p>

#### Web style guide

<p>A style guide is where proper planning shines. A style guide will consist of all the design, layout, interactive (i.e. JavaScript) and type elements used throughout the site in one location. This is usually done in HTML, so if you're a designer who doesn't code, you'll need to create a mockup for your style guide and deliver it to your front end developer along with the rest of your designs. If you've used the element collage method covered earlier, you may not need to repeat yourself in a separate web style guide. If you're using the classic Photoshop mockup method, you will need one. Elements of a style guide include, but are not limited to:</p>

<ul><li>Navigation styles</li>

<li>&lt;h1&gt; through &lt;h5&gt;, also known as header tags</li>

<li>Paragraphs</li>

<li>Lists</li>

<li>Block quotes</li>

<li>Italics, bold face, underlines</li>

<li>Links, including active, hover and visited states, that is, the appearance of links, including when hovered over with the mouse</li>

<li>Icons</li>

<li>Use of images and image style</li>

<li>Use of background images or "watermarks"</li>

<li>Forms.</li></ul>

<p><a href="https://designschool.canva.com/blog/apple-google-starbucks-inside-the-web-design-style-guides-of-10-famous-companies/">This article from Canva</a> explores 10 web style guides for well known companies. You can also use an online tool like <a href="https://frontify.com/">Frontify</a>.</p>

## Using A Pattern Library

<p>For websites of larger scope, you might expand the web style concept to the more robust pattern library, which explains how various elements appear and how they are handled. Sample code for these elements is usually part of the library. It's not just a picture of it, but the thing itself. For example, what does a form look like, what happens visually when it has errors, what is the process for comment submission, etc.</p>

<p>Approved mockups, element collage and wireframes, along with the style guide, are used as the building blocks for the next steps of development.</p>

### HTML/CSS Creation

<p>Using the designs and style guide, an HTML/CSS expert (the front end Coder) will create HTML templates which accurately represent the design as approved. In some cases, templates will appear identical to mockups, however, where Photoshop was used for mockups, subtle differences are to be expected.</p>

<p>Your front end coder might also need additional guidelines and assets related to designs, like color palettes, specific images, icons, and &mdash; if not explicitly noted already &mdash; design rules like margins and padding. Make sure you know what all the deliverables will be before you start sending files. If designs and style guide were created with plenty of attention to detail, there should be few questions or guesswork at this stage; work should be humming along.</p>

### Interactive Element Creation

<p class="c-pre-sidenote--left">Interactive elements may be as simple as a drop-down menu, or as elaborate as a pie chart creator. These elements are typically developed with JavaScript, often using a script library like jQuery. At the most general level, this consists of assembling (and writing) a set of instructions that interact with pages on your website. There may be interactivity between site and server to consider too. You might be connecting APIs<sup>3</sup>, making something like a booking or calendar system etc., or using widgets from third party services.</p>

<p class="c-sidenote c-sidenote--right"><sup>3</sup> Essentially, a bridge between one or more systems. For example, Facebook offers an API that allows you to pull in posts from your wall to an unrelated website.</p> ￼

### CMS Integration

<p>At long last your brilliant design has been converted to code and is ready to be integrated in a Content Management System (CMS). It's well on its way to becoming a website!</p>

<p>The individual or team tasked with doing the "stitching" of the code to the CMS will provide you with a login for the control panel of the CMS, which allows you to enter the content, including text, photos, videos, and documents. Most writers prefer to cut and paste from Microsoft Word.</p>

<p>Depending on the specifics of the CMS selected, you may be able to do this without issue, retaining simple formatting like bold, italics, and lists. However, the CMS may strip out this formatting when you cut and paste, requiring you to add it back. While sometimes tedious, this insures your content remains neat and orderly, which makes it more easily indexed by search engines, more easily printed, cited and converted to other formats.</p>

<p>Although in reality this process is quite involved, I've left out the details because the exact process will be unique to each CMS, and doing this well relies on the expertise of the Web/CMS Developer.</p>

### Training And Documentation

<p>While modern CMS can be very user friendly, it's important to coordinate training for the people responsible for entering content. When possible, on-site training is best, with web conference a second choice. Training works best in very small groups &mdash; 5 people or less. Additionally, having people actually follow the steps needed to complete a task on their own, (rather than just having them watch the trainer and try to remember how to do it when they're on their own) is much more effective.</p>

<p>Training should be supported by documentation, which can take many forms:</p>

<ul><li>Step-by-step video ("screencast")</li>

<li>PDFs with screenshots</li>

<li>Printed guidelines</li>

<li>Contextual help (built in to the CMS).</li></ul>

<p>Sometimes documentation combines some or all of the above. Whatever you choose, keep in mind the skill level of the people entering content. Many people who work in offices are competent at Microsoft Word and email, but can be challenged by basic but necessary "design" tasks like sizing and cropping images. Also remember that the business probably isn't working with the same set of professional design tools that the designer is, so make allowances for the business' technological concerns as well.</p>

<p>It's a good idea to save the writing of documentation until as close to the end of the project as possible. Remember that if you change something in the CMS mid-project, you may have to update documentation to match. This can be very time-consuming (and confusing too), so try to coordinate the parts of your project so the documentation is written once the content entry process has been finalized.</p>

#### Puttin' it all together...

<p>At this point, having followed the preceding steps, you should now be sitting on a pretty solid website. Regardless the size of your project, now is a good time to:</p>

<p>Review your content once again, checking it against the points listed under writing for the web above.</p>

<p>Ask a third party to proofread all your content. This is not the task of the designer or the original writer. It's best to bring in someone with a fresh perspective. Don't proofread your own work.</p>

### BETA TESTING

<p>When you feel your website is almost ready for the public to see, it's time for beta testing &mdash; a process of going through all aspects of the site, making sure everything appears and functions as intended. Consider this checklist, at minimum:</p>

<ul><li>Does the site look as intended in all targeted web browsers? Web browsers include the usual Internet Explorer, Firefox, Safari and Chrome, as well as those that come with common mobile devices. If you've been viewing the site on a desktop browser up until now, you may find unexpected glitches when you switch to a tablet or smartphone. This is the time to thoroughly review your site on a variety of devices before it can be considered ready for public consumption. Remember &mdash; your site's audience will use a wide range of devices to view your site, and it needs to work acceptably well on all of them. You don't have to physically test your site on every possible phone or tablet, but you should try it on a handful of common devices. Don't go out and buy a five-year-old Blackberry for testing purposes.<br />

"Emulation" websites and services like <a href="https://spoon.net/browsers">Spoon.net</a> will generate previews of your site on just about every browser or device known to humankind, giving you a good idea of how it will look in most scenarios.</li>

<li>Interactive features work smoothly.</li>

<li>Contact or other forms work predictably and generate the correct response to the user and recipient of the information submitted.</li>

<li>Error messages are helpful and human-friendly.</li>

<li>Internal and external links function.</li>

<li>Images are sized properly.</li>

<li>All placeholder content has been replaced by the final copy/images, etc.</li>

<li>Internal and external links, including email links, work properly.</li>

<li>Integrations with third party software, such as email service providers, are working.</li></ul>

<p>At this point its very wise to enlist someone who has had no involvement in the process to date, and ask them to methodically go through each page and feature in the site, noting any errors or glitches they find. Don't use someone who's been staring at the site for months. Problems to look out for could include typos, bad links, image sizing, failures on specific mobile devices, or content that's missing or incomplete. (Make sure to tell your tester that the design of the site is set in stone at this point, so they're not wasting time looking at non-content considerations.)</p>

#### Pre-launch coordination

<p>When you approach launch time, you'll need to coordinate with your company's other marketing efforts. If you're active on social media, write and proofread the announcement of your new/redesigned site, and set a schedule to post the announcement. Prepare to update your outgoing voicemail message and coordinate print advertising &mdash; everything needed to support the launch of the site.</p>

#### Redirecting traffic from the "old" site

<p>If your new website is replacing a previous version, it will probably have a different URL structure, and you need to map the old structure to the new. There are two reasons to do this. First, search engines have indexed the URLs of your old site. This indexing has a lot of value to people searching for what your company offers. When you launch a new site with different URLs, the old ones will break and users will get a "page not found" message (404 Error). You want to retain your hard-earned place in search engines. Second, site visitors may have bookmarked pages within your old site and want to return to them. If those pages' URLs change, you need to insure visitors still receive content that is relevant to their needs, instead of a page that no longer exists.</p>

<p>For example, your old site may have: </p>

<ul><li><em>https://oursite.com/company/history.html</em></li>

<li><em> https://oursite.com/staff/california.html</em></li></ul>

<p> while the new site has:</p>

<ul><li><em>https://oursite.com/company-history</em></li>

<li><em>https://oursite.com/staff/california</a></em></li></ul>

<p>The differences are subtle, but computers are very literal things &mdash; to the browser, the difference between "history.html" and "company-history.html" might as well be the distance between Mars and Earth. You need to go through the structure of the old site and make note of every page that has equivalent information in the new site and their URLs. If your old site has a lot of pages, you can use a tool like <a href="https://powermapper.com/">Powermapper</a> to help automate the process. Sometimes old and new URLs will line up pretty well, like those above. Other times an old URL may not have an equivalent in the new site. This often happens if you've closed a division of your company, discontinued a project, or reorganized a department. Regardless of the reason, you'll still need exact URLs to work with for the next step. There are three ways to handle old URLs:</p>

<ul><li>If they have an equivalent like the examples above, you can point the old URL to the new. To diverge in to the technical for a moment, this is done with a 301 Redirect, which tells search engines and users' web browsers that a URL has permanently changed. It looks like this: <code>Redirect 301 /company/history.html</code> <code>https://oursite.com/company-history</code></li>

<li>If the links have no equivalent, you can send site visitors to a page which says "Sorry we can't find what you you're looking for. We've redesigned and reorganized our site, and some content has changed or moved." and provide a site map and search option.</li>

<li>You can also point all non-existent URLs right to the home page.</li></ul>

<p>The larger the scale of your old site, the more work will be required to re-point old URLs. If you have analytics running on your old site, you may choose to re-point only the top 10 or 20 old URLs to new ones, and set a catch-all for all the rest, pointing them either to the "Sorry, we can't find what you're looking for…" page or the home page. Creating catch-all redirects, or those that match a specific URL pattern is a technical endeavor that we won't address here, but you can easily find information on .htaccess files (for Linux server) or web.config files (for NT server) at <a href="https://stackexchange.com/">Stack Exchange</a> or other resources.</p>

#### Never launch on a Friday

<p>It's never a good idea to launch a website, especially one on which many people depend, on a Friday or right before holidays. If something goes wrong, you may not have the resources to fix it when most of the office staff, vendors and other third parties who might be able to help have gone home for the weekend. Mondays are best for launching a new site, as that gives you the whole week to fix any unexpected problems that may arise, and plenty of support to help you do so.</p>

#### Launch!

<p>Once you've thoroughly beta tested the site, it's time to launch. Specific steps vary by project, but generally this means either moving the site (files, database, configuration) from a development environment to a public one making it visible to the world, or simply updating server settings to allow visitors to <em>yourcompany.com</em> to see the new site.</p>

### Post-Launch

#### Web statistics

<p>Reviewing your website visitor statistics can give you vital insight in to how people are using your site. You'll need at least a month or two worth of data to make any determinations. Don't get too hung up on the pure numbers &mdash; all of them are approximate to one degree or another. Trends should be your main focus.  Here are a few key points to consider:</p>

<ul><li>Where are visitors coming from? Search engines, direct traffic (i.e., someone just typed your site's.</li>

<li>URL in to the browser), ads, links from other sites, etc.</li>

<li>Where do visitors live? Are they mostly local, regional, national, international?</li

<li>What pages are the most popular?</li>

<li>How long are visitors staying on the site?</li>

<li>What is the bounce rate, that is how many users visit only one page on the site before leaving it entirely?</li></ul>

<p><a href="https://www.google.com/analytics/">Google Analytics</a> is among the most commonly used web statistics software and you will easily find answers to these questions in the high-level data it presents. Other web statistics software like <a href="https://www.kissmetrics.com/">KISSMetrics</a> or <a href="https://clicky.com/">Clicky</a> should readily provide these answers as well.</p>

#### Technical documentation

<p>You'll also need detailed notes on how various parts of the site are implemented on the CMS. This is different from the documentation provided to the business. Much of your technical documentation will simply consist of the annotated elements discussed earlier in this document, including wireframes, style guide and Photoshop documents. Think about what information would be needed if you brought new people in to maintain the site, people who were not at all familiar with it. What do they require to pick up the project? They'll need:</p>

<ul><li>Credentials for the CMS, web server, and other services connected to the site.</li>

<li>Written or video instructions on how to perform tasks in the CMS: adding news items, blog posts, swapping out photos &mdash; everything that someone can do to the site.</li>

<li>Recommended technical maintenance &mdash; how often do the CMS and other services require updating?</li>

<li>Notes on backups &mdash; what is being backed up, how often, and where is it backed up to?</li></ul>

<p>Note: writing documentation of all kinds is one of a web professional's least favorite tasks, but it's very important. Don't slack on it. Think how terrible it would be to inherit a project without any technical documentation. Then use that dread as your inspiration! You don't want to leave anybody in a lurch down the line and doing this right will save time and frustration later on.</p>

#### Backup

<p>This is often overlooked by businesses and designers alike. Schedule regular backups of the site's files and database. Daily is ideal. Your hosting company may provide an automated way to do this, but if they don't, there are plenty of effective services and tools available to facilitate this process. That way, if your files or database get hacked, erased, corrupted or otherwise damaged, you can restore them with copies from the previous day.</p>

<p>Depending on the size of your site, frequency of updates and some technical matters that vary with each site, you may want to schedule more frequent backups. Ideally, your site will be backed up off-site, that is, in a different place than where it is hosted. Services like Amazon S3 or Rackspace Cloud are ideal for this purpose. The idea is that if your website gets irrevocably damaged, a recent copy is stored in a different physical location, allowing restoration of the site to the last undamaged version.</p>

#### Maintenance plan

<p>Your maintenance plan, which should have been budgeted for before you started, should clarify roles and responsibilities for every aspect of the site. For example, if two articles per week are to be posted, who is responsible for this, and who is that person's backup? If your site requires photos or graphics to be created regularly, make sure this work is assigned and understood by all involved. Determine who will check links, re-size images, write blog posts, etc. Write a simple maintenance plan and share it with everyone involved in the site's care and feeding. Remember, a good website isn't a one-time event, but rather an extensible communication tool that requires regular updates to remain valuable, relevant and compelling to site visitors.</p>

#### Solicit visitor feedback

<p>After it's been online for a while, a great way to improve the impact of your site is to solicit visitor feedback. There are a variety of ways to do this, from simple online surveys to on-site focus groups. Site visitors often have trouble articulating what they like and don't like about their experience. With this in mind, it's important to craft very clear and specific questions when soliciting feedback. And remember, if you're going to take a significant amount of visitors' time, offer something in return &mdash; a product discount, prize, or simply a handwritten note thanking them.</p>

## FIN

<p>OK, one more time for posterity: A good website isn't a one-time event, but rather an extensible communications tool. Once you've built a great website, keep the momentum going. Devote resources to regular maintenance, and check in with your site visitors regularly to identify areas for improvement.</p>

### Recommended Reading

<ul>
	<li>"<a href="https://sensible.com/">Don't Make Me Think, Revisited: A Common Sense Approach to Web Usability</a>" by <em>Steve Krug</em><br />Helps readers understand the principles of intuitive navigation and information design.</li>
	<li>"<a href="https://abookapart.com/products/content-strategy-for-mobile">Content Strategy for Mobile</a>" by <em>Karen McGrane</em></br />Making the case for a mobile strategy, publishing flexibly to multiple channels, and adapting your workflow to a world of emerging devices, platforms, screen sizes, and resolutions.</li>
	<li>"<a href="https://abookapart.com/products/design-is-a-job">Design Is A Job</a>" by <em>Mike Monteiro</em><br />From contracts to selling design, from working with clients to working with each other, learn why navigating the business of design is just as important as the craft of it.</li>
	<li>"<a href="https://icandy-graphics.com/grow-your-seo-book/">Grow your SEO</a>" by <em>Candy Phelps</em><br />A beginner's guide to SEO.</li>
</ul>

## DEFINITIONS

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Term</th>
			<th>Definitions</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Adobe Flash</td>
			<td>A proprietary system for creating rich, interactive website features such as charts, graphs, animations and streaming video. The Flash player, that is, the browser add-on that allows users to via Flash content, is free. Flash authoring software is sold by Adobe.</td>
		</tr>
		<tr>
			<td>Beta testing</td>
			<td>The process of reviewing a website to ensure everything works as intended prior to launch.</td>
		</tr>
		<tr>
			<td>Content Management System (CMS)</td>
			<td>Software that provides website authoring, collaboration and administration tools designed to allow users with little knowledge of web programming languages or markup languages to create and manage the site's content with relative ease. Offers users the ability to manage documents and output for multiple author editing and participation. Popular CMS include WordPress, ExpressionEngine, Drupal, Joomla, Perch, Statamic, Craft, and hundreds more.</td>
		</tr>
		<tr>
			<td>Grid system</td>
			<td>A grid takes the available screen area and divides it up in to equal parts, for example, 10 columns of 96 pixels = 960 pixels. This makes layout and design easier. Many grid systems are available &mdash; use a search engine to see what's current.</td>
		</tr>
		<tr>
			<td>HTML</td>
			<td>Short for 'Hypertext Markup Language.' HTML is a tag-based language which defines the elements of content on a web page. For example, surrounding content in <code>&lt;p&gt;...&lt;/p&gt;</code> tags creates a paragraph, while <code>&lt;strong&gt;...&lt;/strong&gt;</code> creates bold text (adapted from Wikipedia).</td>
		</tr>
		<tr>
			<td>Javascript (JS)</td>
			<td>A programming language that runs inside a user's web browser, enhancing websites with a wide range of features such as mouseovers, slide shows, moving and fading elements, and more. Commonly implemented through a library like jQuery.</td>
		</tr>
		<tr>
			<td>CSS</td>
			<td>Short for 'Cascading Style Sheets.'' CSS is a set of instructions which define the layout and appearance of HTML elements. For example, CSS may specify that all paragraphs be 12 point Verdana, dark gray.</td>
		</tr>
		<tr>
			<td>Layout</td>
			<td>Deals with the arrangement of visual elements on a page. It generally involves organizational principles of composition to achieve specific communication objectives.</td>
		</tr>
		<tr>
			<td>Lorem Ipsum ("Greeking")</td>
			<td>Placeholder text used by web and graphic designers to fill space in mockups and incomplete web pages until real content is provided. May be as old as the sixteenth century.</td>
		</tr>
		<tr>
			<td>Meta tags</td>
			<td>Information about a web page (for example, title, description, author) that helps search engines and other resources understand the contents of that page.</td>
		</tr>
		<tr>
			<td>Responsive Web Design (RWD)</td>
			<td>A set of web design techniques that insure a site adjusts its presentation appropriately for different devices. Term originally coined by Ethan Marcotte.</td>
		</tr>
		<tr>
			<td>Search Engine Optimization (SEO)</td>
			<td>The process of affecting the visibility of a website in a search engine's results.</td>
		</tr>
		<tr>
			<td>URL</td>
			<td>Stands for Uniform Resource Locator, that is, a unique address on the web that contains specific content. For example, <em>tastyfruit.com/citrus/oranges</em></td>
		</tr>
		<tr>
			<td>Wireframe</td>
			<td>A visual representation of the layout elements of a web page, intended to show page structure, element placement and sizing.</td>
		</tr>
	</tbody>
</table>

{{< signature "vf, ra, yk, il" >}}

