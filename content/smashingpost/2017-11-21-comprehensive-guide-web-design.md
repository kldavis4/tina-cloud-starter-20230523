---
title: A Comprehensive Guide To Web Design
slug: comprehensive-guide-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f975f903-b50d-48c3-81cc-636fb7fd6253/a-b-testing-variations-conversions-preview-opt.png
date: 2017-11-21T03:22:13.000Z
author: nickbabich
disable_ads: true
disable_panels: true
canonical: https://theblog.adobe.com/a-comprehensive-guide-to-web-design/
description: >-
  In this article, I’ll focus on the main principles, heuristics and approaches
  that will help you to create a great user experience for your website. I’ll
  start with global things like the user journey (how to define the “skeleton”
  of the website) and work down to the individual page (what should be
  considered during web page design). We’ll also cover other essential aspects
  of design, such as mobile considerations and testing.
summary: >-
  In this article, I’ll focus on the main principles, heuristics and approaches
  that will help you to create a great user experience for your website. I’ll
  start with global things like the user journey (how to define the “skeleton”
  of the website) and work down to the individual page (what should be
  considered during web page design). We’ll also cover other essential aspects
  of design, such as mobile considerations and testing.
categories:
  - UX
  - Web Design
  - Resources
  - Responsive Design
  - Guides
  - Planning
---
_(This is a sponsored post)_. Web design is tricky. Designers and developers have to take a lot of things into account when designing a website, from visual appearance (_how the website looks_) to functional design (_how the website works_). To simplify the task, we’ve prepared this little guide.

In this article, I’ll focus on the main principles, heuristics, and approaches that will help you to create a great user experience for your website. I’ll start with global things like the user journey (how to define the “skeleton” of the website) and work down to the individual page (what should be considered during web page design). We’ll also cover other essential aspects of design, such as mobile considerations and testing.</p>

## Designing The User Journey

### Information Architecture

People often use the term “information architecture” (IA) to mean the menus on a website. But that’s not correct. While menus are a part of IA, they are only one aspect of it.

{{% feature-panel %}}

IA is all about the organization of information in a clear and logical way. Such organization follows a clear purpose: **helping users to navigate a complex set of information**. Good IA creates a hierarchy that aligns with user’s expectations. But good hierarchy and intuitive navigation don’t happen by chance. They are a result of proper user research and testing.

There are a number of ways to research user needs. Often, an information architect will take an active part in user interviews or card sorting, where they would hear of user expectations directly or see how prospective users would categorize a variety of information groups. Information architects also need access to the results of usability tests to see whether users are able to navigate efficiently.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed897001-10ad-45f0-9586-0df0187c0e63/37-a-comprehensive-guide-to-web-design-800w-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed897001-10ad-45f0-9586-0df0187c0e63/37-a-comprehensive-guide-to-web-design-800w-opt.jpg" width="800" height="640" alt="" /></a><figcaption>Card sorting is a simple way to figure out how best to group and organize content based on user input. One of the reasons why information architects like card sorting is because of the clarity of patterns that typically emerges. (Image credit: <a href="https://www.fostermilo.com/articles/card-sorting-with-creative-albuquerque">FosterMilo</a>)</figcaption></figure>

A menu structure would be created based on the results of user interviews, and card sorting would be tested for whether it satisfies the user’s mental model. UX researchers use a technique called “tree testing” to prove that it will work. This happens before designing the actual interface.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fad1fdf7-91f3-4815-b2b1-2cf0ea2ff0d4/36-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/400e317e-20f5-4c51-84b7-8a0210ceb551/36-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="589" alt="" /></a><figcaption>Tree testing is a reliable method of finding whether users can work with the proposed menu structure. (Image credit: <a href="https://www.nngroup.com/articles/tree-testing/">Nielsen Norman Group</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fad1fdf7-91f3-4815-b2b1-2cf0ea2ff0d4/36-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Global Navigation

Navigation is a cornerstone of usability. It doesn’t matter how good your website is if users can’t find their way around it. That’s why navigation on your website should adhere to a few principles:

*   **Simplicity**
    Navigation should be designed in a way that gets visitors where they want to go with the fewest clicks possible.
*   **Clarity**
    There shouldn’t be any guessing about what each navigation option means. Every navigation option should be self-evident to visitors.
*   **Consistency**
    The navigation system should be the same for all pages on the website.

Consider a few things when designing navigation:

*   **Select a navigation pattern based on the user’s needs.**
    Navigation should accommodate the needs of the majority of your app’s users. A given target group expects a particular type of interaction with your website, so make these expectations work in your favor. For example, avoid hamburger-menu navigation if the majority of your users aren’t familiar with the meaning of the icon itself.
*   **Prioritize navigation options.**
    One simple way to prioritize navigation options is to assign different priority levels (high, medium, low) to common user tasks, and then give prominence in the layout to paths and destinations with high priority levels and frequent use.
*   **Make it visible.**
    As [Jakob Nielsen says](https://www.nngroup.com/articles/ten-usability-heuristics/), recognizing something is easier than remembering it. Minimize the user’s memory load by making all important navigation options permanently visible. The most important navigation options should be available at all times, not just when we anticipate that the user will need them.
*   **Communicate the current location.**
    “Where am I?” is a fundamental question to which users need an answer in order to effectively navigate. Failing to indicate the current location is a common problem on many websites. Think about location indicators.</p>

### Links and Navigation Options

Links and navigation options are key factors in the navigation process and have a direct effect on the user journey. Follow a few rules with these interactive elements:

*   **Recognize the difference between internal and external links.**
    Users expect different behavior for internal and external links. All internal links should open in the same tab (this way, you’ll allow users to use the “back” button). If you decide to open external links in a new window, you should provide an advanced warning before automatically opening a new window or tab. This might take the form of text added to the link text stating “(opens in a new window)”.
*   **Change the color of visited links.**
    When visited links don’t change color, users could unintentionally revisit the same pages.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53731b0b-d65f-4802-835c-5aaee47fada8/20-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53731b0b-d65f-4802-835c-5aaee47fada8/20-a-comprehensive-guide-to-web-design-preview-opt.png" width="400" height="222" alt="" /></a><figcaption>Knowing which pages they’ve visited keeps the user from unintentionally revisiting the same pages.</figcaption></figure>

*   **Double-check all links.**
    A user can easily get frustrated by clicking a link and getting a 404 error page in response. When a visitor is searching for content, they expect every link to take them where it says it will, not to a 404 error page or another place they weren’t expecting.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/979ef94a-99fd-43ee-8754-283e79540298/11-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/979ef94a-99fd-43ee-8754-283e79540298/11-a-comprehensive-guide-to-web-design-preview-opt.png" width="484" height="308" alt="" /></a><figcaption>(<a href="">View large version</a>)</figcaption></figure>

### “Back” Button in Browser

The “back” button is perhaps the second-most popular UI control in the browser (after the URL input field). Make sure the “back” button works according to user expectations. When a user follows a link on a page and then clicks the “back” button, they expect to return to the same spot on the original page. A**void situations in which clicking “back” brings the user to the top of the initial page**, instead of where they left off, especially on pages. Losing their spot forces the user to scroll through content they have already seen. It’s no surprise that users get frustrated quickly with no proper “back to position” functionality.</p>

### Breadcrumbs

Breadcrumbs are a set of contextual links that function as a navigation aid on websites. It’s a secondary navigation scheme that usually shows the user’s location on a website.

While this element doesn’t require a lot of explanation, a few things are worth mentioning:

*   **Don’t use breadcrumbs as a substitute for primary navigation.**
    The main navigation should be the element that leads the user, whereas breadcrumbs should only support the user. Relying on breadcrumbs as a primary method of navigation, rather than an extra feature, is usually an indication of poor navigation design.
*   **Use arrowheads, not slashes, as separators. Separate each level clearly.**
    A more-than sign (>) or right-pointing arrow (→) is recommended, because these symbols signal direction. A forward slash (/) isn’t recommended as a separator for e-commerce websites. If you’re going to use it, be certain that no product category will ever use a slash:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36cc5934-65f0-439a-b6fb-52e7b9bd068a/27-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/060a804d-4e8b-4408-9c12-def78dadf219/27-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="63" alt="" /></a><figcaption>Distinguishing between different levels of this breadcrumb trail is hard. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36cc5934-65f0-439a-b6fb-52e7b9bd068a/27-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Search

Some users come to a website looking for one particular item. They don’t want to use the navigation options. They want to type text in a search box, submit their search query and find the page they’re looking for.

Take these few basic rules into account when designing the search box:

*   **Put the search box where users expect to find it.**
    The chart below was created based on a study by A. Dawn Shaikh and Keisi Lenz. It shows the expected location of the search field, according to a survey of 142 participants. The study found that the most convenient spot is the top left or top right of every page on a website. Users can easily find it using the common F-shaped scanning pattern.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41d16ec9-6e50-4f21-b53e-1b98fdad050f/34-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41d16ec9-6e50-4f21-b53e-1b98fdad050f/34-a-comprehensive-guide-to-web-design-preview-opt.png" width="338" height="313" alt="" /></a></figure>

<li><strong>Display search prominently on content-rich websites.</strong><br>
If search is an important function on your website, display it prominently, because it can be the fastest route to discovery for users.</li>
<li><strong>Size the input box appropriately.</strong><br>
Making the input field too short is a common mistake among designers. Of course, users can type a long query into a short field, but only a portion of the text will be visible at a time, which is bad for usability because seeing the entire query at once won’t be possible. In fact, when a search box is too short, users are forced to use short, imprecise queries, because longer queries would be hard and inconvenient to read. Nielsen Norman Group recommends a <a href="https://www.nngroup.com/articles/top-ten-guidelines-for-homepage-usability/">27-character input field</a>, which would accommodate 90% of queries.</li>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b00efe-852f-456b-ae45-9b17d07e9c05/35-a-comprehensive-guide-to-web-design-800w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b00efe-852f-456b-ae45-9b17d07e9c05/35-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="376" alt="" /></a></figure>

<li><strong>Put the search box on every page.</strong><br>
Show the search box on every page, because if users cannot navigate to the content they are looking for, they will try to use search regardless of where they are on the website.</li>

## Designing Individual Pages

### Content Strategy

Perhaps the most important thing about content strategy is to focus the design on page objectives. Understand the goal of the page, and write content according to the goal.

Here are a few practical tips to improve content comprehension:

*   **Prevent information overload.**
    Information overload is a serious problem. It prevents users from making decisions or taking action because they feel they have too much information to consume. There are some simple ways to minimize information overload. One common technique is _chunking_ — breaking content into smaller chunks to help users understand and process it better. A checkout form is a perfect example. Display at most five to seven input fields at a time, and break down the checkout into pages, progressively disclosing fields as necessary.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/148a2af7-d6e7-4732-836c-bfd6e066a64b/43-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd433be8-830f-49b8-bd5b-1911b7e46847/43-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="438" alt="" /></a><figcaption>(Image credit: <a href="https://twitter.com/witteia">Witteia</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/148a2af7-d6e7-4732-836c-bfd6e066a64b/43-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Avoid jargon and industry-specific terms.**
    Each unknown term or phrase that appears on the page will increase the cognitive load on users. A safe bet is to write for all levels of readers, and pick words that are clearly and easily understandable to all groups of users.
*   **Minimize long content sections with a lot of detail.**
    In line with the point about information overload, try to avoid long blocks of text if the website isn’t geared to major information consumption. For example, if you need to provide details about a service or product, try to reveal details step by step. Write in small, scannable segments to facilitate discovery. According to [Robert Gunning](https://www.amazon.com/How-Take-Fog-Business-Writing/dp/0850132320)’s book “How to Take the Fog Out of Business Writing”, for comfortable reading, most sentences should be 20 words or less.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcb40b7-feb8-47fd-848c-7b45361196e7/29-a-comprehensive-guide-to-web-design-800w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcb40b7-feb8-47fd-848c-7b45361196e7/29-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="453" alt="" /></a><figcaption>(Image credit: <a href="https://www.dailyrindblog.com/wp-content/uploads/2013/04/Presentations_UsePlainEnglish.png">The Daily Rind</a>)</figcaption></figure>

*   **Avoid capitalizing all letters.**
    All-caps text — that is, text with all letters cap­i­tal­ized — is fine in tiny doses, such as for acronyms and logos. However, avoid all caps for anything longer (such as paragraphs, form labels, errors, notifications). As mentioned by [Miles Tinker](https://en.wikipedia.org/wiki/Miles_Tinker) in his book _Legibility of Print_, all caps dramatically reduces the speed of reading. Also, most readers find all capitals to be less legible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a6e1ed7-e3ff-4f59-bdc0-3020d2eb40ed/24-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a6e1ed7-e3ff-4f59-bdc0-3020d2eb40ed/24-a-comprehensive-guide-to-web-design-preview-opt.png" width="399" height="378" alt="" /></a><figcaption>Text in all caps is hard for users to read.</figcaption></figure>

### Page Structure

A properly structured page makes it clear where each user interface element is located in the layout. While there are no one-size-fits-all rules, there are a few guidelines that will help you create a solid structure:

*   **Make the structure predictable.**
    Align your design to user expectations. Consider websites from a similar category to find out which elements to use on the page and where. Use patterns that your target audience is familiar with.
*   **Use a layout grid.**
    A layout grid divides a page into major regions, and defines the relationships between elements in terms of size and position. With the help of a grid, combining different parts of a page together in a cohesive layout becomes much easier.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbd8d0c5-b680-418f-9c58-9e62b8d9c43e/15-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbd8d0c5-b680-418f-9c58-9e62b8d9c43e/15-a-comprehensive-guide-to-web-design-preview-opt.png" width="570" height="660" alt="" /></a><figcaption>Grids and layout systems are part of the heritage of design and are still relevant in a multi-screen world. Adobe XD’s layout grids enable designers to achieve consistent, organized designs for different screen sizes and to manage the proportions between elements with customized grids.</figcaption></figure>

*   **Use a low-fidelity wireframe to cut out clutter.**
    Clutter overloads an interface and reduces comprehension. Every added button, image and line of text makes the screen more complicated. Before building the page with real elements, create a wireframe, analyze it, and get rid of anything that isn’t absolutely necessary.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69332e38-7aca-4774-8d93-ad713c930e83/06-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/537b4dde-51a5-4652-aece-1877e9f6ced6/06-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="593" alt="" /></a><figcaption>A low-fidelity wireframe created in <a href="https://www.adobe.com/products/xd.html">Adobe XD</a> (Image credit: <a href="https://timhykes.com/lcblog.php">Tim Hykes</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69332e38-7aca-4774-8d93-ad713c930e83/06-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Visual Hierarchy

People are more likely to quickly scan a web page than to read everything there. Therefore, if a visitor wants to find content or complete a task, they are going to scan until they find where they need to go. You, as a designer, can help them with that by designing good visual hierarchy. Visual hierarchy refers to the arrangement or presentation of elements in a way that indicates importance (that is, where their eyes should focus first, second, etc.). A proper visual hierarchy makes it easy to scan the page.

*   **Use natural scanning patterns.**
    As designers, we have a lot of control over where people look when they’re viewing a page. To set the right path for the visitor’s eyes to follow, we can use two natural scanning patterns: the [F-shaped pattern](https://uxplanet.org/f-shaped-pattern-for-reading-content-80af79cd3394) and the [Z-shaped pattern](https://uxplanet.org/z-shaped-pattern-for-reading-web-content-ce1135f92f1c). For text-heavy pages, such as articles and search results, the F pattern is better, whereas the Z pattern is good for pages that aren’t text-oriented.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/716f545f-897f-4493-b208-b34a80d774f2/09-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b691df0e-0ad6-4139-b22c-023e44293285/09-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="457" alt="" /></a><figcaption>An F-shaped pattern is used by CNN. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/716f545f-897f-4493-b208-b34a80d774f2/09-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdfac270-dede-45a4-a300-50429f80d0fa/40-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49713c5c-72d4-49b3-bf3d-77aa22fb7b6f/40-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="456" alt="" /></a><figcaption>A Z-scanning pattern is used by Basecamp. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdfac270-dede-45a4-a300-50429f80d0fa/40-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Visually prioritize important elements.**
    Make screen titles, log-in forms, navigation options and other important content focal points, so that visitors see them right away.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/321b70c6-6448-4d88-bff9-02ddacf300d2/01-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbc3d69f-84b4-495d-adff-19b9069a26cf/01-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="391" alt="" /></a><figcaption>The “Learn More About Brains” call to action stands out. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/321b70c6-6448-4d88-bff9-02ddacf300d2/01-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Create mockups to clarify the visual hierarchy.**
    Mockups enable designers to see what a layout will look like when it’ll have a real data. Rearranging elements in a mockup is much easier than doing it when the developer is building the web page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44722d7f-236f-48b3-baff-39c4f4f9771f/28-a-comprehensive-guide-to-web-design-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17990546-98d5-4f82-b21e-2448ad757afa/28-a-comprehensive-guide-to-web-design-800w-opt.jpg" width="800" height="450" alt="" /></a><figcaption>A mockup created using Adobe XD. (Image credit: <a href="https://coursetro.com/posts/design/28/Website-Design-in-Adobe-XD-Tutorial">Coursetro</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44722d7f-236f-48b3-baff-39c4f4f9771f/28-a-comprehensive-guide-to-web-design-large-opt.jpg">View large version</a>)</figcaption></figure>

### Scrolling Behavior

A persistent myth among web designers is that people don’t scroll. To be clear: Today, [everybody scrolls](https://www.hugeinc.com/ideas/perspective/everybody-scrolls)!

Improving scrolling behavior is possible with a few tips:

*   **Encourage users to scroll.**
    Despite the fact that people usually [start scrolling](https://www.lukew.com/ff/entry.asp?1946) as soon as the page loads, content at the top of the page is still very important. What appears at the top sets the impression and expectation of quality for visitors. People do scroll, but only if what’s above the fold is promising enough. Thus, put your most compelling content at the top of the page:
    *   **Offer a good [introduction](https://www.nngroup.com/articles/blah-blah-text-keep-cut-or-kill/).**
        An excellent introduction sets the context for the content and answers the user’s question, “What’s this page about?”
    *   **Use [engaging imagery.](https://www.smashingmagazine.com/2017/01/more-than-just-pretty-how-imagery-drives-user-experience/)**
        Users pay close attention to images that contain relevant information.
*   **Persist navigation options.**
    When you create lengthy pages, keep in mind that users still require a sense of orientation (of their current location) and a sense of navigation (other possible paths). Long pages can make navigation problematic for users; if the top navigation bar loses visibility when the user scrolls down, they will have to scroll all the way back up when they’re deep within the page. The obvious solution to this is a [sticky menu](https://www.smashingmagazine.com/2012/09/sticky-menus-are-quicker-to-navigate/) that shows the current location and that remains on screen in a consistent area at all times.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56dc897e-e5bb-4bbc-bd4b-af83c7ef3de9/14-a-comprehensive-guide-to-web-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56dc897e-e5bb-4bbc-bd4b-af83c7ef3de9/14-a-comprehensive-guide-to-web-design.gif" width="666" height="191" alt="" /></a><figcaption>Scroll-activated sticky navigation (Image: Zenman)</figcaption></figure>

*   **Provide visual feedback when loading new content.**
    This is especially important for web pages where content loads dynamically (such as news feeds). Because content-loading during scrolling is supposed to be fast (it shouldn’t take longer than 2 to 10 seconds), you can use [looped animation to indicate](https://www.smashingmagazine.com/2016/12/best-practices-for-animated-progress-indicators/#types-of-progress-indicators) that the system is working.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d6d4ad2-0a72-426b-ac13-4c18094f5bab/04-a-comprehensive-guide-to-web-design-800w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d6d4ad2-0a72-426b-ac13-4c18094f5bab/04-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="420" alt="" /></a><figcaption>Subtle animation (such as Tumblr’s loading indicator) tells the user that more content is being loaded.</figcaption></figure>

*   **Don’t hijack scrolling.**
    Hijacked scrolling is one of the most annoying things because it takes control away from the user and makes the scrolling behavior completely unpredictable. When you design a website, let the user control their browsing and movement through the website.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63238ae5-add3-48da-809e-d5886b8fd2cd/tumblr-blogs-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87192c55-3f51-4cf0-8c46-bd295a874255/tumblr-blogs-800w-opt.png" width="800" height="411" alt="Tumbler’s signup page uses scroll hijacking." /></a><figcaption>Tumbler’s signup page uses scroll hijacking. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63238ae5-add3-48da-809e-d5886b8fd2cd/tumblr-blogs-large-opt.png">View large version</a>)</figcaption></figure>

### Content Loading

Content loading is worth additional clarification. While an instant response is best, there are occasions when your website will need more time to deliver content to visitors. A bad Internet connection could cause a slow reaction, or an operation could take a bit more time to complete. But no matter the cause of such behavior, your website should appear fast and responsive.

*   **Make sure regular loading doesn’t take long.**
    The attention span and patience of web users is very low. According to [Nielsen Norman Group research](https://www.nngroup.com/articles/powers-of-10-time-scales-in-ux/), 10 seconds is about the limit for keeping the user’s attention on a task. When visitors have to wait for a website to load, they will become frustrated and likely leave if the website doesn’t load quickly enough for them. Even with the most beautifully designed loading indicator, users will still leave if loading takes too long.
*   **Use skeleton screens during loading.**
    Many websites use progress indicators to show that data is loading. While the intention behind a progress indicator is good (providing visual feedback), the result can be negative. As [Luke Wroblewski mentions](https://www.lukew.com/ff/entry.asp?1797), “Progress indicators by definition call attention to the fact that someone needs to wait. It’s like watching the clock tick down — when you do, time seems to go slower.” There is an excellent alternative to progress indicators: skeleton screens. These containers are essentially a temporarily blank version of the page, into which information is gradually loaded. Rather than showing a loading indicator, designers can use a skeleton screen to focus users’ attention on actual progress and create anticipation for what’s to come. This creates a sense that things are happening immediately, as information is incrementally displayed on the screen and people see that the website is acting while they wait.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3f81df4-d8a2-4662-b789-aa88dc58fefb/10-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19702c7c-9878-4321-a2ab-58c9a59df6f3/10-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="373" alt="" /></a><figcaption>Facebook uses skeleton screens to fill out the UI as content is loaded incrementally. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3f81df4-d8a2-4662-b789-aa88dc58fefb/10-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Buttons

Buttons are vital to creating a smooth conversational flow. It’s worth paying attention to these basic best practices for buttons:

*   **Ensure that clickable elements look like ones.**
    With buttons and other interactive elements, think about how the design communicates affordance. How do users understand the element as a button? Form should follow the function: the way an object looks tells users how to use it. Visual elements that look like links or buttons but aren’t clickable (such as underlined words that aren’t links or elements that have a rectangular background but aren’t buttons) can easily confuse users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb543339-0fba-45a4-b56a-55951cf62f55/08-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95331981-e518-4e19-b32b-1a2843eb0d33/08-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="362" alt="" /></a><figcaption>Is the orange box in the top-left corner of the screen a button? No, but the shape and label make the element look like one. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb543339-0fba-45a4-b56a-55951cf62f55/08-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Label buttons according to what they do.**
    The label on any actionable interface element should always tie back to what it will do for the user. Users will feel more comfortable if they understand what action a button does. Vague labels such as “Submit” and abstract labels like in the example below don’t provide enough information about the action.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43803ae4-e3a3-4511-ae12-b7fbea78ec06/12-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43803ae4-e3a3-4511-ae12-b7fbea78ec06/12-a-comprehensive-guide-to-web-design-preview-opt.png" width="474" height="220" alt="" /></a><figcaption>Don’t make people wonder what an interface element does. (Image credit: <a href="https://www.uxmatters.com/mt/archives/2012/05/7-basic-best-practices-for-buttons.php">UX Matters</a>)</figcaption></figure>

*   **Design buttons consistently.**
    Users remember details, whether consciously or not. When browsing a website, they’ll associate a particular element’s shape with button functionality. Therefore, consistency will not only contribute to a great-looking design, but will also make the experience more familiar to users. The image below illustrates this point perfectly. Using three different shapes in one part of an app (such as the system toolbar) is not only confusing, but sloppy.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d4807b8-a2bb-4c34-937c-2c2191c3f73f/31-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d4807b8-a2bb-4c34-937c-2c2191c3f73f/31-a-comprehensive-guide-to-web-design-preview-opt.png" width="800" height="455" alt="" /></a><figcaption>Strive for consistency.</figcaption></figure>

### Imagery

As the saying goes, a picture is worth a thousand words. Human beings are highly visual creatures, able to process visual information almost instantly; [90% of all](https://www.webmarketinggroup.co.uk/blog/why-every-seo-strategy-needs-infographics/) information that we perceive and that gets transmitted to our brains is visual. Images are a powerful way to capture the user’s attention and to differentiate a product. A single image can convey more to the viewer than an elaborately designed block of text. Furthermore, images cross language barriers in a way that text simply can’t.

The following principles will help you integrate imagery in your web design:

*   **Make sure images are relevant.**
    One of the biggest dangers in design is imagery that conveys the wrong message. Select images that strongly support your product goals, and ensure that they are relevant to the context.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b48f81a-1607-4522-92dd-463b0adf787a/space-image25-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b96dc2cf-b6c0-4eaa-9838-dbbcb3262b5f/space-image25-800w-opt.png" width="800" height="453" alt="" /></a><figcaption>Images that aren’t related to the topic will cause confusion. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b48f81a-1607-4522-92dd-463b0adf787a/space-image25-large-opt.png">View large version</a>)</figcaption></figure>

*   **Avoid generic photos of people.**
    Using human faces in design is an effective way to engage users. Seeing faces of other humans makes viewers feel like they are connecting with them, and not just being sold a product. However, many corporate websites are notorious for using generic stock photos to build a sense of trust. [Usability tests](https://articles.uie.com/deciding_when_graphics_help/) show that such photos rarely add value to the design and more often impair rather than improve the user experience.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4625a7-3e39-45e2-a8c4-217326fc3507/46-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6e522e8-b03c-47d5-8b44-628ff644f0a0/46-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="450" alt="" /></a><figcaption>Inauthentic images leave the user with a sense of shallow, false pretence. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4625a7-3e39-45e2-a8c4-217326fc3507/46-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Use high-quality assets with no distortion.**
    The quality of assets of your website will have a tremendous impact on the user’s impression and expectations of your service. Make sure images are appropriately sized for displays across all platforms. Images shouldn’t appear pixelated, so test resolution sizes for various ratios and devices. Display photos and graphics in their original aspect ratio.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61a842a5-91d8-48dc-be0e-5f1dd59f165e/45-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1d0fa56-3a30-4665-bad8-da7c6c2dc8da/45-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="294" alt="" /></a><figcaption>A degraded image versus a properly sized image (Image credit: <a href="https://blogs.adobe.com/creativecloud/more-than-just-pretty-how-imagery-drives-ux/">Adobe</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61a842a5-91d8-48dc-be0e-5f1dd59f165e/45-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Video

With increasing Internet speeds, videos are becoming more popular, especially considering that they [extend time spent on site](https://www.forbes.com/sites/forbesagencycouncil/2017/02/03/video-marketing-the-future-of-content-marketing/). Today, video is everywhere. We’re watching it on our desktops, tablets and phones. When used effectively, video is one of the most powerful tools available for engaging an audience — it conveys more emotion and really gives people a feel for a product or service.

*   **Set audio to off by default, with the option to turn it on.**
    When users arrive on a page, they don’t expect that it will play any sound. Most users don’t use headphones and will be stressed because they’ll need to figure out how to turn the sound off. In most cases, users will leave the website as soon as it plays.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a4fbfc6-92c5-4ad4-8516-577e338910f7/22-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef5ea772-47b5-425e-ab3e-15648c985338/22-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="906" alt="" /></a><figcaption>Facebook videos play automatically as soon as the user reaches them, but no sound plays unless the user enables it. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a4fbfc6-92c5-4ad4-8516-577e338910f7/22-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Keep promo video as short as possible.**
    According to the [research by D-Mak Productions](https://dmakproductions.com/blog/what-is-the-ideal-length-for-web-video-production/), short videos are more appealing to the majority of users. Thus, keep business videos in the range of two to three minutes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f203e89b-10f7-4fe4-91bf-3f0a8f6adf37/26-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f203e89b-10f7-4fe4-91bf-3f0a8f6adf37/26-a-comprehensive-guide-to-web-design-preview-opt.png" width="532" height="355" alt="" /></a><figcaption>(Image credit: <a href="https://dmakproductions.com/blog/what-is-the-ideal-length-for-web-video-production/">Dmakproductions</a>)</figcaption></figure>

*   **Provide an alternative way to access content.**
    If a video is the only way to consume content, this can limit access to the information for anyone who cannot see or hear the content. For accessibility, include captions and a full transcript of the video.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/324dd715-0fa4-4db1-8798-1827affda00c/38-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04853679-4d68-464c-9a64-6a030a5579cf/38-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="450" alt="" /></a><figcaption>Subtitles and transcript will make video content more accessible. (Image credit: <a href="https://www.ted.com">TED</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/324dd715-0fa4-4db1-8798-1827affda00c/38-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Call-to-Action Buttons

Calls to action (CTA) are buttons that guide users towards your conversion goal. The whole point of a CTA is to direct visitors to a desired course of action. Some common examples of CTAs are:

*   “Start a trial”
*   “Download the book”
*   “Sign up for updates”
*   “Get a consultation”

Take a few things into account when designing CTA buttons:

*   **Size**
    The CTA should be large enough to see from a distance, but not so large as to detract attention from other content on the page. To confirm that your CTA is the most prominent element on the page, try the five-second test: View a web page for five seconds and then write down what you remember. If the CTA is on your list, then congrats! It’s sized appropriately.
*   **Visual prominence**
    The color you choose for CTAs has a tremendous impact on whether it will be noticeable. With color, you can make certain buttons stand out more than others by giving them more visual prominence. Contrasting colors work best for CTAs and make for striking buttons.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3499d7bf-e2c8-400a-8035-30afc7612da8/42-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04e68f87-4433-4bb3-a5ed-4932ed89f360/42-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="267" alt="" /></a><figcaption>The green of the CTA on Firefox’s page jumps off the page and immediately gets the user’s attention. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3499d7bf-e2c8-400a-8035-30afc7612da8/42-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Negative space**
    The amount of space around a CTA is important, too. White (or negative) space creates essential breathing room and separates a button from other elements in the interface.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563856b6-1abf-45a1-b767-a517f05ea72c/16-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffff62b5-68ff-4233-ac09-db1ba0833a35/16-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="325" alt="" /></a><figcaption>The previous version of Dropbox’s home page has a good example of using negative space to make the primary CTA pop. The blue “Sign up for free” CTA stands out against the light blue of the background. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563856b6-1abf-45a1-b767-a517f05ea72c/16-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

*   **Action-oriented text**
    Write text for the button that will compel visitors to take action. Begin with a verb like “Start,” “Get” or “Join.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea33797c-4293-4a49-abd8-14a0dd015567/30-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ac2ed78-4d76-4a2b-bfb1-37476dc3ae5c/30-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="307" alt="" /></a><figcaption>Evernote has one of the most common yet still effective action-oriented texts for its CTA. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea33797c-4293-4a49-abd8-14a0dd015567/30-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

**Tip:** You can quickly test a CTA using a blur effect. A blur test is a quick technique to determine whether the user’s eye will go where you want it to go. Take a screenshot of your page and [apply a blur effect in Adobe XD](https://helpx.adobe.com/experience-design/help/background-blur.html) (see the example on Charity Water below). Looking at the blurred version of your page, which elements stand out? If you don’t like what’s being projected, revise.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00cedbe7-0d38-41d9-9a9b-9f1d0b7ebb2e/02-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28d87970-94b8-431a-853d-aa971b4c03b1/02-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="414" alt="" /></a><figcaption>A blur test is a technique to reveal a design’s focal point and visual hierarchy. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00cedbe7-0d38-41d9-9a9b-9f1d0b7ebb2e/02-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Web Forms

Filling a form remains one of the most important types of interaction for users on the web. In fact, a form is often considered the final step in the completion of a goal. Users should be able to complete forms quickly and without confusion. A form is like a conversation, and like any conversation, there should be logical communication between two parties: the user and the website.

*   **Ask only what’s required.**
    Ask for only what you really need. Every extra field you add to a form will affect its conversion rate. Always think about why you’re requesting certain information from users and how you will be using it.
*   **Order the form logically.**
    Questions should be asked logically from the user’s perspective, not from the application or database’s perspective. For example, asking for someone’s address before their name would be incorrect.
*   **Group related fields together.**
    Group related information into logical blocks or sets. The flow from one set of questions to the next will better resemble a conversation. Grouping related fields together also helps the user make sense of the information.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/517c259e-0410-47d3-b971-fcdd8537c728/50-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/517c259e-0410-47d3-b971-fcdd8537c728/50-a-comprehensive-guide-to-web-design-preview-opt.png" width="700" height="589" alt="" /></a><figcaption>Group related fields together. (Image: Nielsen Norman Group)</figcaption></figure>

### Animation

More and more designers are incorporating [animation as a functional element](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/) to enhance the user experience. Animation is no longer just for delight; it is one of the most important tools for effective interaction. However, animation in design can enhance the user experience only if it’s incorporated at the right time and place. Good UI animation has a purpose; it is meaningful and functional.

Here are a few cases in which animation can enhance the experience:

*   **Visual feedback on user action**
    Good interaction design provides feedback. Visual feedback is helpful when you need to inform users about the result of an operation. In case an operation isn’t performed successfully, functional animation can provide information about the problem in a fast and easy way. For example, a shake animation can be used when a wrong password is entered. It’s easy to understand why the shake is a fairly universal gesture to communicate “no,” because a simple head shake is so prevalent in interpersonal communication.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be3e0fbc-352e-46a8-ac8b-c17f06c2cc12/44-a-comprehensive-guide-to-web-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be3e0fbc-352e-46a8-ac8b-c17f06c2cc12/44-a-comprehensive-guide-to-web-design.gif" width="534" height="214" alt="" /></a><figcaption>Users will see this animation and immediately understand the problem. (Image credit: <a href="https://thekineticui.com/your-app-login-is-boring/">The Kinetic UI</a>)</figcaption></figure>

*   **Visibility of system status**
    One of [Jakob Nielsen’s 10 heuristics for usability](https://www.nngroup.com/articles/ten-usability-heuristics/), visibility of system status remains among the most important principles in user interface design. Users want to know their current context in a system at any given time, and an app shouldn’t keep them guessing — it should tell the user what’s happening via appropriate visual feedback. Data uploading and downloading operations are great opportunities for functional animation. For example, an animated loading bar shows how fast a process is going and sets an expectation for how fast the action will be processed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/343cda2d-8022-47da-b178-314f15f0dba4/39-a-comprehensive-guide-to-web-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/343cda2d-8022-47da-b178-314f15f0dba4/39-a-comprehensive-guide-to-web-design.gif" width="800" height="600" alt="" /></a><figcaption>(Image credit: <a href="https://dribbble.com/xjw">xjw</a>)</figcaption></figure>

*   **Navigational transitions**
    Navigational transitions are movements between states on a website — for example, from a high-level view to a detailed view. State changes often involve hard cuts by default, which can make them difficult to follow. Functional animation eases users through these moments of change, smoothly transporting users between navigational contexts and explaining changes on the screen by creating visual connections between states.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cccc15d-7886-4b65-9dc6-708fec8f4c20/47-a-comprehensive-guide-to-web-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cccc15d-7886-4b65-9dc6-708fec8f4c20/47-a-comprehensive-guide-to-web-design.gif" width="800" height="600" alt="" /></a><figcaption>(Image credit: <a href="https://ramotion.com">Ramotion</a>)</figcaption></figure>

*   **Branding**
    Suppose you have dozens of websites that have the same exact features and help users to accomplish the same tasks. They might all offer a good user experience, but the one that people really love offers something more than just a good user experience. It establishes an emotional connection with users. Branding animation plays a key role in engaging users. It can support a company’s brand values, highlight a product’s strengths and make the user experience truly delightful and memorable.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6816ca3-f3f6-4a37-9722-ff4de5441226/05-a-comprehensive-guide-to-web-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6816ca3-f3f6-4a37-9722-ff4de5441226/05-a-comprehensive-guide-to-web-design.gif" width="800" height="424" alt="" /></a><figcaption>(Image credit: <a href="https://www.helloheco.com/">Heco</a>)</figcaption></figure>

## Mobile Considerations

Today, almost [50% of users](https://www.statista.com/topics/779/mobile-internet/) access the web from mobile devices. What does this mean for us web designers? It means that we must have a mobile strategy for every website we design.</p>

### Practice Responsive Web Design

It’s essential to optimize your website for the vast landscape of desktop and mobile browsers, each of which has a different screen resolution, supported technologies and user base.

*   **Aim for a single-column layout.**
    Single-column layouts usually work best on mobile screens. Not only does a single column help with managing the limited space on a small screen, but it also easily scales between different device resolutions and between portrait and landscape mode.
*   **Use the Priority+ pattern to prioritize navigation across breakpoints.**
    [Priority+](https://justmarkup.com/log/2012/06/19/responsive-multi-level-navigation/) is a term coined by Michael Scharnagl to describe navigation that exposes what’s deemed to be the most important elements and hides away less important items behind a “more” button. It makes use of available screen space. As space increases, the number of exposed navigation options increases as well, which can result in better visibility and more engagement. This pattern is especially good for content-heavy websites with a lot of different sections and pages (such as a news website or a large retailer’s store). The Guardian makes use of the Priority+ pattern for its section navigation. Less important items are revealed when the user hits the “All” button.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74bd09d7-d2c8-43df-bde2-a08f41617f36/51-a-comprehensive-guide-to-web-design.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74bd09d7-d2c8-43df-bde2-a08f41617f36/51-a-comprehensive-guide-to-web-design.gif" width="800" height="465" alt="" /></a><figcaption>The Guardian employs the Priority+ pattern for its section navigation. (Image credit: <a href="https://bradfrost.com/blog/post/revisiting-the-priority-pattern/">Brad Frost</a>)</figcaption></figure>

*   **Make sure images are sized appropriately for displays and platforms.**
    A website must adapt to look perfect on all of the different devices and in all of the various resolutions, pixel densities and orientations. Managing, manipulating and delivering images is one of the main challenges web designers face when building responsive websites. To simplify this task, you can use tools such as [Responsive Image Breakpoints Generator](https://www.responsivebreakpoints.com/) to generate breakpoints for images interactively.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd065b2-2547-49ff-b9c9-a41dc0479abd/52-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6ad2e56-bf97-4bc9-bd0d-9ef373e39c92/52-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="561" alt="" /></a><figcaption>Responsive Image Breakpoints Generator helps you to manage multiple sizes of images, enabling you to generate responsive image breakpoints interactively. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd065b2-2547-49ff-b9c9-a41dc0479abd/52-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Going From Clickable to Tappable

On the mobile web, interaction is done via finger taps, not mouse clicks. This means that different rules apply when you’re designing touch targets and interactions.

*   **Properly sized touch targets.**
    All interactive element (such as links, buttons and menus) should be tappable. While the desktop web lends itself well to links whose active (i.e. clickable) area is small and precise, the mobile web requires larger, chunkier buttons that can be easily pressed with a thumb. When a tap is used as a primary input method for your website, refer to the [MIT Touch Lab’s study](https://touchlab.mit.edu/publications/2003_009.pdf) to choose a proper size for your buttons. The study found that the average size of finger pads are between 10 and 14 millimeters and that fingertips range from 8 to 10, making 10 × 10 millimeters a good minimum touch target size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0cc040f-1e73-4e2e-abec-de2cb333c7a1/07-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0cc040f-1e73-4e2e-abec-de2cb333c7a1/07-a-comprehensive-guide-to-web-design-preview-opt.png" width="721" height="396" alt="" /></a><figcaption>Smaller touch targets are harder for users to tap than larger ones. (Image credit: <a href="https://developer.apple.com/design/tips/">Apple</a>)</figcaption></figure>

*   **Stronger visual signifiers of interactivity.**
    On the mobile web, there is no hover state. While on a desktop, it’s possible to provide additional visual feedback when a user hovers the mouse over an element (for example, revealing a dropdown menu), a mobile user would have to tap to see that response. Thus, users should be able to correctly predict how an interface element will behave just by looking at it.</p>

## Accessibility

Today’s products must be accessible to everyone, regardless of a person’s abilities. Designing for users with impairments is one way that designers can practice empathy and learn to experience the world from someone else’s perspective.</p>

### Users With Poor Eyesight

A lot of websites use low contrast for text copy. While low-contrast text may be trendy, it’s also illegible and inaccessible. Low contrast is especially problematic for users with low vision and who struggle with contrast sensitivity.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18d049e8-f37f-4710-a0f0-b1098eaa510d/41-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77ade7f2-8c62-46b5-b28e-71e8918b4568/41-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="414" alt="" /></a><figcaption>Gray text on a light-gray background is hard to read. The experience will be far from good, and the design simply won’t work. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18d049e8-f37f-4710-a0f0-b1098eaa510d/41-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

Low-contrast text is hard to read on a desktop, but it becomes even more difficult on mobile. Imagine trying to read low-contrast text on a mobile device while walking in bright sunlight. This is a good reminder that accessible visual design is better visual design for all users.

Never sacrifice usability for beauty. The most important characteristic of text and other vital elements on a website is readability. Readability requires sufficient contrast between text and background. To ensure that text is readable by people with visual impairments, the W3C’s Web Content Accessibility Guidelines (WCAG) has a [contrast-ratio recommendation](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html). The following contrast ratios are recommended for body text and image text:

*   Small text should have a contrast ratio of at least 4.5:1 against its background. A ratio of 7:1 is preferable.
*   Large text (at 14-point bold and 18-point regular and up) should have a contrast ratio of at least 3:1 against its background.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/680f0c8e-5a61-424c-9806-3fbdb8f13144/49-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/680f0c8e-5a61-424c-9806-3fbdb8f13144/49-a-comprehensive-guide-to-web-design-preview-opt.png" width="451" height="118" alt="" /></a><figcaption><strong>Bad:</strong> These lines of text do not meet the color-contrast ratio recommendations and are difficult to read against their background.</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dedf3b38-deae-4a9c-a646-14d53f9e2441/03-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dedf3b38-deae-4a9c-a646-14d53f9e2441/03-a-comprehensive-guide-to-web-design-preview-opt.png" width="451" height="119" alt="" /></a><figcaption><strong>Good:</strong> These lines of text follow the color-contrast ratio recommendations and are legible against their background.</figcaption></figure>

You can use WebAIM’s [Color Contrast Checker](https://webaim.org/resources/contrastchecker/) to quickly find out whether you’re within the optimal range.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d30ac089-01ad-49ca-a4e0-8974edc89462/13-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39da885a-8cbc-457e-9fee-8087d84e2d9c/13-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="271" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d30ac089-01ad-49ca-a4e0-8974edc89462/13-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Color Blind Users

It’s estimated that [4.5% of the global population](https://www.colourblindawareness.org/colour-blindness/) experience color blindness (that’s 1 in 12 men and 1 in 200 women), 4% suffer from low vision (1 in 30 people), and 0.6% are blind (1 in 188 people). It’s easy to forget that we design for this group of users because most designers don’t experience such problems.

To make design accessible for these users, avoid using color alone to convey meaning. As the [W3C states](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html), color shouldn’t be used “as the only visual means of conveying information, indicating an action, prompting a response, or distinguishing a visual element.”

One common example where color is used as the sole means of conveying information is alerts in forms. Success and error messages are often colored green and red, respectively. But red and green are the colors most affected by color-vision deficiency — these colors can be difficult to distinguish for people with deuteranopia or protanopia. Most probably, you’ve seen error messages like, “The fields marked in red are required.” While it might not seem like a big deal, this error message appearing in a form like the one below can be extremely frustrating for people with a color-vision deficiency. Designers should use color to highlight or complement what is already visible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e21078b-266a-40ff-83f8-05fc8fa731d0/32-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e21078b-266a-40ff-83f8-05fc8fa731d0/32-a-comprehensive-guide-to-web-design-preview-opt.png" width="720" height="280" alt="" /></a><figcaption><strong>Bad:</strong> This form relies only on red and green to indicate fields with and without errors. Color-blind users wouldn’t be able to identify the fields in red.</figcaption></figure>

In the form above, the designer should give more specific instruction, like, “The email address you entered is not valid.” Or at least display an icon near the field that requires attention.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fcbfc5b-6773-4179-b94b-686b26203931/33-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fcbfc5b-6773-4179-b94b-686b26203931/33-a-comprehensive-guide-to-web-design-preview-opt.png" width="720" height="299" alt="" /></a><figcaption><strong>Good:</strong> Icons and labels show which fields are invalid, better communicating the information to a color-blind user.</figcaption></figure>

### Blind Users

Images and illustrations are a significant part of the web experience. Blind people use assistive technologies such as screen readers to interpret websites. Screen readers “read” images by relying on alternative text attributed to the image. If that text is not present or is not descriptive enough, they won’t be able to get the information as intended.

Consider two examples — first, [Threadless](https://www.threadless.com/), a popular t-shirt store. This page doesn’t say much about the item being sold. The only text information available is a combination of price and size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b058ef7-4aba-4c01-be70-263087272399/19-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77950feb-5ac0-4b4f-a5e3-20528fec6d1c/19-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="457" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b058ef7-4aba-4c01-be70-263087272399/19-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

The second example is from ASOS. This page, selling a similar shirt, provides accurate alternative text for the item. This helps people who use screen readers to envision what the item looks like.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b3b855-c851-459e-a334-d9f27d266020/48-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b3b855-c851-459e-a334-d9f27d266020/48-a-comprehensive-guide-to-web-design-preview-opt.png" width="747" height="768" alt="" /></a></figure>

When creating text alternatives for images, follow this guideline:

*   All “meaningful” images require descriptive alternative text. (A “meaningful” photo adds context to the information being conveyed.)
*   A text alternative isn’t needed if an image is purely decorative and provides no useful information to the user to aid them in understanding the content of the page.</p>

### Keyboard-Friendly Experience

Certain users navigate the Internet using their keyboard, rather than a mouse. For example, people with motor impairments have difficulty with the fine motor movements required for using a mouse. Make interactive and navigation elements easily accessible to this group of users by enabling interactive elements to be focused with the `Tab` key and by displaying a keyboard-focus indicator.

Here are the most basic rules for keyboard navigation:

*   **Check that keyboard focus is visible and obvious.**
    Some web designers remove the keyboard focus indicator because they think it’s an eyesore. This hinders keyboard users from properly interacting with the website. If you don’t like the default indicator provided by the browser, don’t remove it altogether; instead, design it to satisfy your taste.
*   **All interactive elements should be accessible.**
    Keyboard users must be able to access all interactive elements, not just the main navigation options or primary calls to action.

You can find detailed requirements for keyboard interaction in the [“Design Patterns and Widgets” section](https://www.w3.org/TR/wai-aria-practices/#aria_ex) of the W3C’s “WAI-ARIA Authoring Practices” document.</p>

## Testing

### Iterative Testing

Testing is an essential part of the [UX design process](https://blogs.adobe.com/creativecloud/what-is-ux-and-why-should-you-care/). And like any other part of the design cycle, it is an iterative process. Gather feedback early on in the design process, and iterate throughout.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce530ccf-7c62-405d-9c26-44ff76cef16e/18-a-comprehensive-guide-to-web-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81d1c2b7-3bf3-4ece-b65d-980904fc14e8/18-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="500" alt="" /></a><figcaption>(Image credit: <a href="https://www.extremeuncertainty.com/why-agile-projects-need-to-fund-bml-properly/">Extreme Uncertainty</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce530ccf-7c62-405d-9c26-44ff76cef16e/18-a-comprehensive-guide-to-web-design-large-opt.png">View large version</a>)</figcaption></figure>

### Test Page-Loading Time

Users hate slow-loading web pages. That’s why response time is a critical factor on modern websites. According to Nielsen Norman Group, there are [three response-time limits:](https://www.nngroup.com/articles/response-times-3-important-limits/)

*   **0.1 second**
    This feels instant for users.
*   **1 second**
    This keeps the user's flow of thought seamless, but the user will sense a slight delay.
*   **10 seconds**
    This is about the limit for keeping the user's attention focused on the operation. A 10-second delay will often make users leave the website immediately.

Obviously, we shouldn’t make users wait 10 seconds for anything on our websites. But even a few seconds of delay, which happens regularly, makes an experience unpleasant. Users will be annoyed with having to wait for the operation.

What usually causes slow loading time?

*   Heavy content objects (such as embedded video and slideshow widgets),
*   Unoptimized back-end code,
*   Hardware-related issues (infrastructure that doesn’t allow for fast operations).

Tools like [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) will help you to find the causes of slow times.</p>

### A/B Testing

An A/B test is ideal when you’re struggling to choose between two versions of a design (such as an existing version and a redesigned version of a page). This testing method consists of showing one of two versions randomly to an equal number of users and then reviewing analytics to see which version accomplished your goal more effectively.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92c8e01-d391-4caa-adb3-b9ede1d18b2c/17-a-comprehensive-guide-to-web-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92c8e01-d391-4caa-adb3-b9ede1d18b2c/17-a-comprehensive-guide-to-web-design-preview-opt.png" width="605" height="293" alt="" /></a><figcaption>(Image credit: <a href="https://vwo.com/ab-testing/">VWO</a>)</figcaption></figure>

## Developer Handoff

A [UX design process](https://blogs.adobe.com/creativecloud/ux-process-what-it-is-what-it-looks-like-and-why-its-important/) has two important steps: prototyping the design and developing a working solution. The step that connects the two is called a _handoff_. As soon as the design is finalized and ready to be moved to development, designers prepare a specification, which is a document that describes how the design should be coded. A specification ensures that the design will be implemented according to the original intention.

**Precision in the specification is critical** because, with an inaccurate specification, the developers will have to either rely on guesswork when building the website or go back to the designer to get answers to their questions. But assembling a specification manually can be a headache and usually takes significant time, depending on the complexity of the design.

With Adobe XD’s design specs feature (in beta), designers can publish a public URL for developers to inspect flows, grab measurements and copy styles. Designers no longer have to spend time authoring specifications to communicate positioning, text styles or fonts to the developer.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4dc914-e546-4918-9526-e59730b7cdf6/25-a-comprehensive-guide-to-web-design-800w-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb4dc914-e546-4918-9526-e59730b7cdf6/25-a-comprehensive-guide-to-web-design-800w-opt.png" width="800" height="450" alt="" /></a><figcaption>Adobe XD’s design specs feature (in beta)</figcaption></figure>

## Conclusion

As with any aspect of design, the tips shared here are just a start. Mix and match these ideas with your own for best results. Treat your website as a continually evolving project, and use analytics and user feedback to constantly improve the experience. And remember that design isn’t just for designers — it’s for users.</p>

<blockquote>This article is part of the UX design series sponsored by Adobe. Adobe XD tool is made for a <a href="https://adobe.ly/2hI52UE">fast and fluid UX design process</a>, as it lets you go from idea to prototype faster. Design, prototype and share — all in one app.

You can check out more inspiring projects created with <a href="https://www.behance.net/galleries/adobe/5/XD">Adobe XD on Behance</a>, and also <a href="https://adobe.ly/2yKueO8">sign up for the Adobe experience design newsletter</a> to stay updated and informed on the latest trends and insights for UX/UI design.</blockquote>

{{< signature "ra, ms, al, il" >}}

