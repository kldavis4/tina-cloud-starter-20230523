---
title: Responsive Navigation On Complex Websites
slug: responsive-navigation-on-complex-websites
image: >-
  https://www.smashingmagazine.com/general/2013/04/09/133433-revision-65/attachment/3-seneca-example_mini/
date: 2013-09-11T09:57:37.000Z
author: jon-rundle
description: >-
  Central to a solid user experience is a well-structured, simple navigation
  system. Over the past few months, I’ve been involved in launching two large
  institutional websites with complex navigation systems.
categories:
  - Mobile
  - CSS
  - Techniques
  - Navigation
  - Responsive Design
---
Central to a solid user experience is a well-structured, simple navigation system. Over the past few months, I’ve been involved in launching two large institutional websites with complex navigation systems. Maintaining simplicity on such large websites becomes increasingly difficult as content requirements grow and tiers of navigation are added, not to mention the extra complexity added by small screens.

To illustrate the techniques involved in <strong>implementing responsive navigation on a large website</strong>, I’ll refer to two actual clients of mine. I’ll start with the process and how to get through it with research and mockups, then later get into some of the actual code that was used.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Progressive And Responsive Navigation](https://www.smashingmagazine.com/2012/02/progressive-and-responsive-navigation/)
*   [Navigation For Mega-Sites](https://www.smashingmagazine.com/2013/03/navigation-mega-sites/)
*   [<span class="headline">Implementing Off-Canvas Navigation For A Responsive Website</span>](https://www.smashingmagazine.com/2013/01/off-canvas-navigation-for-responsive-website/)
*   [Responsive Menus: Enhancing Navigation On Mobile Websites](https://www.smashingmagazine.com/2012/06/responsive-menus-enhancing-navigation-on-mobile-websites/)

## Middlesex-London Health Unit

### The Process

The key to success in every project, particularly a large website, is to work closely with the client, keeping them involved in as many aspects of the design process as possible. Before we get into code and how to build a website technically, we need to learn more about the project. At ResIM, <strong>we start with audience research</strong>, before progressing through <a href="https://www.omnigroup.com/products/omnigraffle/">information architecture</a>, <a href="https://www.mockflow.com/">wireframing</a> and wireframe usability testing.

{{% feature-panel %}}

In our latest project for a public health organization, the <a href="https://www.healthunit.com">Middlesex-London Health Unit</a> (MLHU), we started with audience research to find out the kinds of information that public users look for on health-related websites. Considering that MLHU’s website had over 1300 pages to be overhauled, we needed to make sure that priority content gets the focus it deserves.

As a design studio, we’ve tried different forms of audience research. One of our go-to methods is to bring in users to walk through a wireframe website, seeing how long it takes them to perform various tasks and to find various sections of the website, while <a href="https://silverbackapp.com/">video recording</a> them. This style of testing doesn’t always yield perfect results because many inexperienced users will have problems understanding a website without graphics, colors, etc. But it still provides valuable insight into how easy or difficult content is to find.

This method works well when the structure and site map are defined, but we weren’t quite at that stage and needed to step back. MLHU has various committees and groups that had to be represented on the website, and we needed to make sure that everyone’s voice is heard.

We started by meeting with all of the committee members who were appointed to work on the website, to <strong>determine which parts of the website were most important</strong>. After hearing each group state its case as to why its information needed to be prominent on the website, we started to build a proper hierarchy. We realized there were a lot of different sections and areas, and we needed a way to group them into fewer parent items in order for the user to be able to interpret and navigate more quickly. We decided to piece together a lot of similar categories, and we named each of these groups; these would become our four main navigation items.

This was a great accomplishment, but we quickly realized that we needed to call attention to other important pages that weren’t necessarily grouped into those four sections. We created a supporting menu to accommodate and provide access to some of these non-health-related topics. Once we had built this streamlined navigation and worked it into our wireframes, we ran them through a testing period, in which we had users walk through areas of the website, performing tasks and finding information.

Watching people use this streamlined navigation, we noticed that each of them was able to quickly find the section of the website they were looking for and then effortlessly find the particular page and information they were after. These <strong>results from real-world users reinforced the decisions</strong> we had made in the information architecture.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdcdc7ba-4a86-4d09-b6ad-a7607d88b9fa/1-mlhu-sitemap-large-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe6b0021-fa8c-4e1a-a31c-880c371541c7/1-mlhu-sitemap-mini.jpg" alt="MLHU site map" /></a><br>
<em>MLHU’s site map. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdcdc7ba-4a86-4d09-b6ad-a7607d88b9fa/1-mlhu-sitemap-large-mini.jpg">Larger view</a> | <a href="https://www.healthunit.com/">Source</a>)</em>

<strong>From here, we were able to move into the interface design phase</strong>, which included mocking up the responsive mobile view. Many clients struggle with the concept that a responsive mobile website is, in fact, the same website they see on their desktop, and not a whole new skin for mobile. Showing these clients a little less in the mockup phase is sometimes valuable.

For this reason, we typically leave tablet views out of this step, to enable us to control how the website transitions from the big “desktop” view down to the small “mobile” view. In the case of MLHU, I realized with the older ages of some of our target users, we couldn’t rely on typical top-right <a href="https://dribbble.s3.amazonaws.com/users/5973/screenshots/880056/lexicon-nuggets-2-ui-hamburger.png">hamburger-style</a> navigation.

Feeling that this solution would have been more difficult for certain users, I opted instead for vertical text-based navigation. This gave the second level of navigation a better layout, by <strong>allowing users to view all menu options</strong> before making a selection.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41d297cf-c9d0-4f0f-ba83-c83fdc589b8e/2-mlhu-example-large-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbe31c66-69f5-4c84-bb52-0e04c941b5a6/2-mlhu-example-mini.jpg" alt="MLHU website on mobile" width="500" height="393" /></a><br>
<em>MLHU’s website on mobile. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41d297cf-c9d0-4f0f-ba83-c83fdc589b8e/2-mlhu-example-large-mini.jpg">Larger view</a> | <a href="https://www.healthunit.com/">Source</a>)</em>

### Implementation

Our initial concern in the MLHU project was whether we could keep the mobile navigation structure congruent with the desktop version. Typically, one can hide navigation under a hamburger-style button, a common design pattern. However, our target audience included a wide age range, and we felt that displaying the full text of the navigation would be more user-friendly.

If we were to keep the navigation the same and then make some CSS adjustments to wrap the navigation in a box and stack the navigation vertically instead of horizontally, we could achieve the solution we were looking for.

<pre><code class="language-css">
@media only screen and (max-width: 600px) {
    nav li {
        width: 100%;
        box-sizing: border-box;
    }

    nav a {
        background: rgba(0,0,0,0.5);
        padding: 10px 12px;
        text-align: left;
        margin: 0;
        box-sizing: border-box;
    }
}
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c61c7e0c-ae5b-4b80-90ae-c5a318410b29/4-mlhu-code-example-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c61c7e0c-ae5b-4b80-90ae-c5a318410b29/4-mlhu-code-example-mini.jpg" alt="MLHU Mobile Navigation" width="500" height="308" /></a><br>
<em>MLHU’s mobile navigation. (<a href="https://www.healthunit.com/">Source</a>)</em>

A JavaScript-based solution for our desktop navigation interaction was in place, using the <a href="https://cherne.net/brian/resources/jquery.hoverIntent.html">hoverIntent plugin</a>, but we needed to adjust it to work properly on mobile. Our solution was to add a condition to check the screen’s size and, if small, to switch to a toggle slide instead of a hover fade in/out. <strong>A toggle slide gives a more native feel to the website</strong>, making it fit in and feel quicker on a mobile device, whereas a fade can feel slow and unresponsive when interacted with on a touchscreen.

<pre><code class="language-javascript">
function navIn() { 
    [...]
    } else if($(window).width() &lt; 600) {  /* Here's where we check for the screen size and do a slide instead. */
        $(this).children('ul').slideDown();
        $(this).addClass('hovering');
    } 
    [...]
}
</code></pre>

## Seneca College

### The Process

A second instance of our process was the design and UX overhaul of <a href="https://www.senecacollege.ca/">Seneca College</a>’s public website. We couldn’t reduce the main navigation as we did with MLHU because of different content requirements and organizational constraints. We didn’t need to work through an information architecture phase because the navigation was already set for us by the client; so, <strong>we moved right into wireframing and interface concepts</strong>. Similar to MLHU, we also mocked up a responsive mobile view and explored ways to display the navigation in an effective format.

Recognizing that this target audience is much younger, I felt strongly about using a streamlined navigation that is revealed via a hamburger-style vertical side menu. The hamburger icon has become popular through its use in many mobile applications, and it frees up space in the website’s header for the logo and search icon. A lot of sublevel pages needed to be displayed on Seneca College’s website, and showing them all at once in the header navigation would have been a bit too much.

My solution was to display sectional navigation at the top of every inner page. This secondary navigation would allow the user to quickly move through sections of the website without having to scroll through a long menu. With the complexity of a large website, making it navigable before showing the main content on the inner pages is sometimes necessary.

If you’re unsure of which route to take, try doing some extra audience research using mobile wireframes, and <strong>get a feel for how real-world users respond to the solutions</strong>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9e54f6-5d38-415e-b294-cd989b2cdae4/3-seneca-example-large-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b4ca290-3b11-4caf-9bb6-7636eadd35ca/3-seneca-example-mini.jpg" alt="Seneca website on mobile" width="500" height="393" /></a><br>
<em>Seneca’s website on mobile. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9e54f6-5d38-415e-b294-cd989b2cdae4/3-seneca-example-large-mini.jpg">Larger view</a> | <a href="https://www.senecacollege.ca/">Source</a>)</em>

### Implementation

Seneca’s navigation system is more complex and its mobile and desktop versions more different from each other than MLHU’s. We needed to find a way to replace the main navigation with a hamburger icon once the screen reaches a certain size. We started with a div for the mobile navigation that sits inside the header, but we didn’t want it to show up in the desktop view, so we hid it with CSS.

<pre><code class="language-markup">
&lt;div id="mobileNav"&gt;
    &lt;a id="searchIcon" href="#"&gt;&lt;img src="https://www.smashingmagazine.com/images/searchIcon.png" width="24px" height="24px" alt="" /&gt;&lt;/a&gt;
    &lt;a id="mobileNavIcon" href="#"&gt;&lt;img src="https://www.smashingmagazine.com/images/mobileNav.png" width="38px" height="20px" alt="" /&gt;&lt;/a&gt;
&lt;/div&gt;
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/214eb2cc-22ee-43c1-be8c-6cb4b0874b1f/5-seneca-code-example-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/214eb2cc-22ee-43c1-be8c-6cb4b0874b1f/5-seneca-code-example-mini.jpg" alt="Seneca Mobile Nav DIV" width="452" height="132" /></a><br>
<em>Seneca’s div for mobile navigation. (<a href="https://www.senecacollege.ca/">Source</a>)</em>

<pre><code class="language-css">
#mobileNav {
    display: none;
}
</code></pre>

For screens that are big enough, we display the aforementioned hidden div using media queries.

<pre><code class="language-css">
@media only screen and (max-width: 600px) {
    #mobileNav {
        display:block;
    }
}
</code></pre>

At the same time, we restyled the navigation and hid it. Feel free to get creative with restyling the navigation for mobile. I wanted full-width navigation that slides down, pushing the rest of the content, but <strong>you could instead absolutely position the menu to overlap the main content</strong>, or achieve an off-screen push effect using something like PageSlide. Many different techniques are possible; experiment with what you like and what feels best for the website.

<pre><code class="language-css">
@media only screen and (max-width: 600px) {
    nav {
        display: none;
        width: 100%;
        background: #000;
        margin-left: -20px;
        padding-right: 40px;
    }

    nav li {
        display: block;
        margin: 20px 0 20px 20px;
        width: 100%;
    }

    nav a {
        color: #FFF;
        margin: 0;
        width: 100%;
    }
}
</code></pre>

Lastly, completing our toggle is simply a matter of adding some JavaScript, similar to the example above.

<pre><code class="language-javascript">
$('#mobileNavIcon').click(function () {
    $('nav').slideToggle();
    return false;
});
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ebe917-47f9-4748-8947-62d51b9e0daf/6-seneca-finished-code-example-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ebe917-47f9-4748-8947-62d51b9e0daf/6-seneca-finished-code-example-mini.jpg" alt="Seneca mobile navigation opened" width="500" height="756" /></a><br>
<em>Seneca’s mobile navigation opened. (<a href="https://www.senecacollege.ca/">Source</a>)</em>

It’s imperative to make design decisions that enhance the user experience by considering the results of usability testing, the perceived skill level of all user sets, and the general characteristics of the audience. As demonstrated in the cases above, even though a hamburger-style menu icon has become the <a href="https://www.smashingmagazine.com/2012/10/08/the-semantic-responsive-design-navicon/">industry standard</a>, it might not be the best approach given the age or competency of the target audience.</p>

## Other Techniques

I’m always looking for new solutions to the problem of complex navigation. Below are a few examples that could be really useful, depending on the requirements of the project.</p>

### PageSlide

I like that PageSlide follows the current mobile app trend with a pull-out side menu. Users are getting more comfortable with these menus and how they work. The benefit is a much taller scrollable menu that doesn’t push content too far down.</p>

### Responsive Multi-Level Menu

<a href="https://tympanus.net/Development/ResponsiveMultiLevelMenu/index.html">Responsive Multi-Level Menu</a> is great for a few reasons. It mimics normal drop-down navigation, which is usually triggered by mouse hovering, and implements it effectively for touchscreens. It also makes it easy for users to jump down a few levels without forcing new pages to load.</p>

## Conclusion

Making design decisions based on your users should be paramount. If you aren’t involved in the initial design phase, then at least try to get involved in the responsive portion of the project. You need to help make sure that the direction taken is in the best interest of users, based on their comprehension of the systems you plan on using and their ability to access content.

Next, determine what code is needed to make a smooth transition from desktop to mobile. Does it require some JavaScript to animate nicely? Does its orientation need to change from horizontal to vertical? What can you do with the initial CSS to allow for an even smoother transition that requires fewer adjustments to media queries?

Lastly, <strong>don’t let a complex navigation system or information architecture intimidate you</strong>. There’s always a way to simplify it to its core and to provide those layers to the user in a way that is non-threatening and easy to understand. Take on the challenge and have fun with it!

### Other Resources

You may be interested in the following articles and related resources:

*   PageSlide This jQuery plugin slides a Web page over to reveal an interactive pane.
*   [Responsive Multi-Level Menu](https://tympanus.net/Development/ResponsiveMultiLevelMenu/index.html) This space-saving drop-down menu includes subtle effects.
*   “[Convert a Menu to a Dropdown for Small Screens](https://css-tricks.com/convert-menu-to-dropdown/),” CSS-Tricks
*   “[Responsive Navigation Patterns](https://bradfrostweb.com/blog/web/responsive-nav-patterns/),” Brad Frost

<em>(al) (ea)</em>

