---
title: 'Mobile Navigation For Smashing Magazine: A Case Study'
slug: mobile-navigation-for-smashing-magazine
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b93bb9d2-b04f-408d-a01a-05568c60fae4/mobile-navigation-now.png
date: 2015-09-21T14:53:34.000Z
author: marco-kunz
summary: >-
  In this article, Marco Hengstenberg explains how he helped rebuild the mobile navigation in order to enhance the experience for the readers of Smashing Magazine.
description: >-
  In this article, Marco Hengstenberg explains how he helped rebuild the mobile navigation in order to enhance the experience for the readers of Smashing Magazine.
categories:
  - Coding
  - CSS
  - Techniques
  - Navigation
  - Case Studies
---
Since we started plodding around on this rock in space, human beings have always been dissatisfied with their environment — which is (mostly) a good thing. Otherwise we might still live in caves, fearful of the weather and worshipping the sun. It's **dissatisfaction and curiosity** which drive us to fix things that ain't broken.

Back in spring 2013, Smashing Magazine sported a **`<select>` menu** as its mobile navigation. It wasn't considered an anti-pattern back then and I still think it's a viable solution to the complex problem of how to build [accessible](https://webaim.org/techniques/forms/controls#select) and functional cross-device navigation. Brad Frost wrote a few words about [the pros and cons of this pattern](https://bradfrost.com/blog/web/responsive-nav-patterns/#select) on his blog and I couldn't agree more.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f420526a-4568-4e31-92c5-98e6da1bf53a/select-menu-nav.png" alt="Screenshot of the mobile view of Smashing Magazine from 2013" /><figcaption>The mobile navigation in early 2013 – not exactly a beauty, but fully functional.</figure>

While it worked nicely, it also had a few problems. Mostly, it wasn't the most beautiful piece of UI on the web _and_ we had to throw some JavaScript on it to make the experience somehow worthwhile. **Rebuilding this mobile navigation** was one of the early tasks given to me after I started working here in January 2013.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Improving Smashing Magazine’s Performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)
*   [Creating A Living Style Guide: A Case Study](https://www.smashingmagazine.com/2016/05/creating-a-living-style-guide-case-study/)
*   [World Wide Web, Not Wealthy Western Web](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/)

## Replace All The Things

My first move towards a new and shiny mobile navigation was to kick the `<select>` menu in the bin and look around the web for options and best practices. Some [articles](https://www.smashingmagazine.com/2013/01/15/off-canvas-navigation-for-responsive-website/) about [responsive design](https://www.smashingmagazine.com/2013/04/09/javascript-plugin-for-responsive-navigation/) and a whole lot of [round-ups](https://speckyboy.com/2013/01/30/more-responsive-navigation-solutions/), [code examples](https://webdesign.tutsplus.com/tutorials/a-simple-responsive-mobile-first-navigation--webdesign-6074) and [Git repos](https://github.com/twbs) later I came to this conclusion:

<blockquote>“Write down the underlying HTML to have a solid base, then take care of the styling, and when that's done you might look for possible JS additions, if needed. And finally: testing, testing, testing!<br /><br />Still progressive enhancement running the game.”</blockquote>

For this article, I went as far as to rebuild one of the prototypes from back then with simplified HTML and CSS in CodePen (no media queries, no reset, just code from the top of my head). The jQuery part came in later on, after we realized that some people were confused when the toggle buttons didn't become inactive and weren't replaced after clicking/tapping them. After a short but intense phase of tests and adjustments, we decided to deploy it to the live blog in the middle of June 2013.

{{< codepen theme_id="8287" slug_hash="BNrxLZ" default_tab="result" user="Nice2MeatU" caption="One of the early prototypes for the new mobile navigation." >}}See the Pen <a href='https://codepen.io/Nice2MeatU/pen/BNrxLZ/'>BNrxLZ</a> by Marco (<a href='https://codepen.io/Nice2MeatU'>@Nice2MeatU</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

**Note**: _Feel free to take the code and tinker with it. You can also use it as a starting point for a project of your own or commercially or whatever. There is no license or copyright to it. That being said:_ **No guarantees or support!** _I wouldn't recommend copying and pasting the code into a project and simply leaving it there as is._

{{% feature-panel %}}

## When Good Is Not Good Enough

You might recognize the feeling, creeping up your spine over days or weeks, that some of your work just doesn't feel 100% right – may be 97% or 98% but definitely not the whole cake. This is what happened to me after some time passed by and I kept interacting with our new navigation. The closing buttons felt out of place and the jQuery part kept bothering me, since while it served its purpose well, it should not have been part of the experience, but just an enhancement. Without JavaScript enabled, the user experience I envisioned crumbled to bits. So I started over, tweaking and adjusting and rewriting and trying out different solutions to the same problem over and over again, whenever I found the time.

While it has been a really time-consuming task, it's also been a lot of fun to try out so many different solutions to the same problem. It was also worthwhile as now we had options to choose from – options we could test for performance, usability and the overall experience. Just to make this clear: building prototypes early on in a project can save you a whole lot of time later on. Sometimes it's the slightest change from one version to the next that makes all the difference.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92ba90d4-9888-4a99-addf-fad1e0ddba94/trying-and-trying.png" alt="Screenshot of several folders with different versions of a build for a mobile navigation" /><figcaption>At some point the folders started to pile up.</figcaption></figure>

In December 2013, just after Christmas and while I was on holiday, Vitaly made a decision and went for a CSS-only solution by following the [footer anchor pattern](https://bradfrost.com/blog/web/responsive-nav-patterns/#footer-anchor). He moved the navigation and the mobile search to the footer of the website but kept the buttons on top. That way it wouldn't be an issue if the buttons looked the same after the click/tap because they would be out of view. As we'd had the "Back to top" links in the Magazine since day one, there already was a solution to the problem that people might want to jump back to the header of the page.

### Yes But No But Yes But No

This time we received some emails with feedback on our decision to change the navigation pattern. When I returned to my desk in January 2014, a few users had filed bug reports about feeling completely lost after jumping down a whole page of the Magazine. Other users told us that while the buttons had already rendered on their mobile phone, they tapped them but didn't go anywhere as the footer hadn't loaded owing to their slow connection.

Another issue raised was that some users didn't find the "Back to top" link. They landed in the mobile menu and there was no option visible to simply return to the header: the link was out of view, above the navigation. Again, we had ended up at the point where we had something that wasn't exactly broken, but it wasn't the complete solution as well. _Two steps forward, one step back._

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/732af303-262b-4c1d-b072-36b40fe54b26/mobile-nav-2014.png" alt="Mobile navigation collapsed - The look from 2013 until 2015" /><figcaption>That's the way our mobile navigation looked when collapsed.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23dd71d0-1c86-4d93-b674-ed168eff0d4a/mobile-nav-2014-view.png" alt="Mobile Navigation toggled" /><figcaption>And here's the expanded view after adding a "Back to top" link.</figcaption></figure>

### So Little Time, So Much To Do

During the period between June 2013 and Fall 2014, I was completely occupied with [many different tasks](https://www.smashingmagazine.com/2014/09/08/improving-smashing-magazine-performance-case-study/). I don't want this to sound like an excuse, but being the only developer at Smashing Magazine means I work on a lot of different projects at the same time. I have to stay up to date with external developers and have at least one eye on Trello, one on Basecamp and one in my email inbox, while I always need both my remaining eyes for Skype and Slack (our constant meeting rooms). I think you understand by now that there's an anatomy-related problem.

That being said, I worked on the Smashing Magazine site and our [Conference websites](https://smashingconf.com/). We had a redesign for the [shop](https://shop.smashingmagazine.com/) behind the scenes, where I had been involved from time to time, and we also had a few projects that never saw the light of day. A few [landing](https://smashingconf.com/oxford-2014/landingpage/) [pages](https://smashingconf.com/freiburg-2014/landingpage/) needed to be designed and developed, and [other sites](https://www.smashing-links.com/) needed a complete revamp.

Long story short: the prototypes for the navigation were left lying around untouched for one and a half years until I was finally able to return to them.

{{% ad-panel-leaderboard %}}

## April Showers Bring May Flowers

In April this year, Vitaly opened a request on our Trello board to replace the infamous hamburger icon with the word "Menu." This sounded like an excellent opportunity to finally get my hands on the mobile navigation again.

The first thing I did was the task at hand. The hamburger icon went into the same bin the `<select>` menu once did and now we had "Menu" displayed as text.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b43671b-f084-4775-abaf-a26c4d0598da/mobile-nav-2015.png" alt="Mobile navigation, collapsed, in 2015" /><figcaption>The mobile header of Smashing Magazine now.</figcaption></figure>

The next step was to think of possible improvements and a solution to the closing mechanism. The goal set was: **no JavaScript** – an easy enough task but having a CSS-only solution is rarely seen as the sexiest one. The last solution built had the closing buttons inside the elements I made visible with the `:target` technique. For more information on the `:target` pseudo-selector, I recommend you to read Chris Coyier's thoughts on the [dos, don'ts and possible use cases](https://css-tricks.com/on-target/). In case you wondered, [support for this selector](https://caniuse.com/#search=%3Atarget) is perfect in the mobile landscape.

If you've never heard of the `:target` selector before, here is the most basic example I could think of:

{{< codepen height="300" theme_id="8287" slug_hash="ZGRXGw" default_tab="result" user="Nice2MeatU" caption="Very basic example of <code>:target</code>" >}}See the Pen <a href='https://codepen.io/Nice2MeatU/pen/ZGRXGw/'>ZGRXGw</a> by Marco (<a href='https://codepen.io/Nice2MeatU'>@Nice2MeatU</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

### Web Development Is Never Easy

That looks too easy to be true, right? And yes, it is. The technique is simple and effective but there are two issues with it:

1.  You need a second anchor to hide what you revealed.
2.  You add to the browser history with every click.

While the first one might not look like a big deal, I can assure you it is. Let me explain what happens when you click on the "Menu" button in the Magazine. I'll spare you most of the CSS related to our mobile search, as that follows the same pattern, and show you the parts that differ. I also added a few comments to the CSS to explain my thoughts behind those values.

What I wanted to achieve is a congruent closing button on top of the "Menu" button, covering it when the navigation is visible. The look and feel should be just as if you had a JavaScript toggle in place. The same goes for the search and its related closing button, which has a different size and position.

Here are the inline styles from our `<head>` section (slightly altered for easier understanding), the so-called [critical CSS](https://developers.google.com/speed/pagespeed/service/PrioritizeCriticalCss) part:

<div class="break-out">

<pre><code class="language-css">
header {
  width: 38.2%;
  margin-left: 5.5%;
  padding: 1.25em 0;

  /* To make the logo clickable when the navigation or the
     search are overlaid */
  z-index: 3;
}

.mobile-toggle-buttons-container {
  position: absolute;
  top: 1.5em;
  right: 1.5em;

  /* Again, to keep the buttons clickable when the closing
     button is overlaid. That way you can either just
     close the nav or switch to the search or click the logo. */
  z-index: 4;
}

.navigation-toggle-button,
.search-toggle-button {

  /* This makes it easier to match the width and height with
     the closing buttons */
  box-sizing: border-box;

  float: right;

  border: .08em solid #C73A11;

  border-radius: .25em;
  box-shadow: 0 .08em .08em rgba(0,0,0,0.25);
}

.search-toggle-button {
  /* If you wanted to hide the text but keep it accessible */
  text-indent: 150%;
  overflow: hidden;
  white-space: nowrap;

  /* Sweet technique to serve SVG to all capable browsers
     and leave the rest with PNG */
  background:
    url(search-icon.png) no-repeat 50% 50%,
    #e95c33);
  background:
    url(search-icon.svg) no-repeat 50% 50%,
    -webkit-linear-gradient(to bottom, #e95c33, #e95c33);
  background:
    url(search-icon.svg) no-repeat 50% 50%,
    linear-gradient(to bottom, #e95c33, #e95c33);

  /* You need to declare the background-size for WebKit
     otherwise it will do funny things to your SVG image */
  background-size: 1.875em auto;
  -webkit-background-size: 1.875em;

  padding: .4em;
  width: 2.9375em;
}

/* Nothing special from here on */
.navigation-toggle-button {
  text-transform: uppercase;

  margin-left: 1em;
  padding: .4em;

  color: #fff;
  background: #e95c33;
}

.mobile-navigation,
.mobile-search {
  width: 100%;
  height: 0;
  max-height: 0;
  padding-top: 0;
  opacity: 0;
  transition: none;
}

.mobile-navigation ul,
.mobile-search form,
.mobile-nav-closing-button,
.mobile-search-closing-button {
  display: none;
}
</code></pre></div>

I don't think any of the CSS needs a lot of explanation apart from what I gave away in the comments. If you still have trouble with one or a few selectors, attributes or values, hit the comment section and **fire those questions!**

If you want to get a deeper insight into the _gradient-svg-png technique_, I will gladly send you over to Pau Giner's blog, where I found [his article](https://pauginer.com/post/36614680636/invisible-gradient-technique) on the subject. The [text replacement](https://www.zeldman.com/2012/03/01/replacing-the-9999px-hack-new-image-replacement/) technique for the search button by Scott Kellum is one of [many ways](https://css-tricks.com/examples/ImageReplacement/) to come to such a result. In case you're wondering why I am working with such an odd value of `.08em`, there is a very good reason for that: browsers are very bad at rounding – they just don't get it right. Here's a [very basic CodePen example of the issue](https://codepen.io/Nice2MeatU/pen/nJial).

{{% ad-panel-leaderboard %}}

### Overwriting The Critical CSS Part

Now for the part that overwrites what we declared in the above-the-fold styles after a button has been clicked or tapped. All the following CSS is in the main style sheet (again, this is not the actual code but optimized for this context):

<div class="break-out">

<pre><code class="language-css">
.mobile-navigation-closing-button,
.mobile-search-closing-button {
  /* Again, this is for a bit of ease when we want
     to match the height and width of the "show" buttons */
  box-sizing: border-box;

  /* Here we already have the closing button for the nav in
     position */
  top: 1.5em;
  right: 1.5em;

  text-align: center;
  padding: .4em;
  width: 2.9375em;
  background: #e95c33;
  border: .08em solid #C73A11;

  border-radius: .25em;
  box-shadow: 0 .08em .08em rgba(0,0,0,0.25);
}

/* Width needs to match the nav button */
.mobile-navigation-closing-button {
  width: 3.8em;
}

/* Position needs to match with the search button */
.mobile-search-closing-button {
  right: 6.3em;
}

/* If one of the containers becomes targeted */
.mobile-navigation:target,
.mobile-search:target {
  /* The z-index is lower than anything in the header */
  z-index: 2;

  /* To prevent the browser window from scrolling
     down so the buttons in the header would become un-
     clickable without scrolling back up, we have to use
     this not so beautiful hack */
  top: -10em;
  padding-top: 10em;
  margin-bottom: -8em;

  /* This transition ensures a nice animation when
     opening the navigation or search */
  transition:
    opacity .4s ease-out,
    max-height .4s ease-out;

  height: 100%;
  max-height: 62.5em;
  opacity: 1;
}

/* By using the adjacent sibling combinator (only works with a
   certain markup, of course) I have full control over my closing
   buttons */
.mobile-navigation:target + .mobile-navigation-closing-button,
.mobile-search:target + .mobile-search-closing-button {
  /* Closing buttons have the highest z-index as they have to
     sit on top of the "show" buttons */
  z-index: 5;

  display: block;
}
</code></pre></div>

Again, I tried to use the comments to explain my way of thinking. I hope it all makes sense to you.

Finally, here is the underlying markup, the basis of our mobile navigation:

<div class="break-out">

<pre><code class="language-markup">
&lt;body id="top"&gt;
  &lt;div class="mobile-nav-buttons"&gt;
    &lt;a href="#mobile-navigation" role="button" title="Jump to the main navigation"&gt;Menu&lt;/a&gt;
    &lt;a href="#mobile-search" role="button" title="Jump to the search"&gt;Search&lt;/a&gt;
  &lt;/div&gt;
  &lt;a href="#content"&gt;Jump to the content&lt;/a&gt;
  &lt;header role="banner"&gt;
    &lt;h1&gt;&lt;a href="/"&gt;
      &lt;span&gt;Smashing Magazine&lt;/span&gt;
      &lt;img src="logo.png" alt="The logo of Smashing Magazine" /&gt;&lt;/a&gt;&lt;/h1&gt;
  &lt;/header&gt;
  &lt;nav class="mobile-navigation" id="mobile-navigation" role="navigation"&gt;
    &lt;ul class="mobile-nav-ul"&gt;
      &lt;li&gt;Smashing Pages&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item One&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Two&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Three&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Four&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
    &lt;ul class="mobile-nav-ul"&gt;
      &lt;li&gt;Smashing Categories&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Five&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Six&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Seven&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="#"&gt;Nav Item Eight&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/nav&gt;
  &lt;a class="mobile-nav-closing-button" role="button" href="#top" title="close the navigation"&gt;X&lt;/a&gt;
  &lt;div class="mobile-search" id="mobile-search"&gt;
    &lt;form&gt;
      &lt;label for="mobile-search-input"&gt;Search on Smashing Magazine&lt;/label&gt;
      &lt;input id="mobile-search-input" type="text" /&gt;
      &lt;button type="submit"&gt;Search&lt;/button&gt;
    &lt;/form&gt;
  &lt;/div&gt;
  &lt;a class="mobile-search-closing-button" role="button" href="#top" title="Close the Search"&gt;X&lt;/a&gt;
</code></pre></div>

By using the [adjacent sibling combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_selectors) to hide and show the closing buttons, the markup needs to be exactly as it is in the example HTML here, with the link for closing the navigation directly following the nav container. As I am currently working my way through the [W3C accessibility tutorials](https://www.w3.org/WAI/tutorials/) to learn more on best practices with [accessibility](https://webaim.org/techniques/skipnav/), the jump links to the navigation, search and content had to come first in the DOM tree. That way, people with a screen reader have a few options to skip content they don't need or want to read over and over again.

## Takeaway For You

Now that you've come this far I want to give you something practical. I reduced the code to its bare bones and made a CodePen out of it. Take it, play with it, use it for any project and improve it where possible. There is no license, no copyright, no warranty, no guarantee and no support for the code provided. Handle with care!

{{< codepen height="400" theme_id="8287" slug_hash="eNoGKp" default_tab="result" user="Nice2MeatU" caption="The bare-bones CSS toggle navigation" >}}See the Pen <a href='https://codepen.io/Nice2MeatU/pen/eNoGKp/'>Bare Bones CSS Only Toggle Navigation</a> by Marco (<a href='https://codepen.io/Nice2MeatU'>@Nice2MeatU</a>) on <a href='https://codepen.io'>CodePen</a>.{{< /codepen >}}

I also put together a little ZIP package for you. You can [download it](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b61d6a9-edbb-4b76-8daa-57047448e2f6/barebones-css-only-navigation.zip) right away.

## Finishing Touches

Currently, Christian Brückner from [Inpsyde](https://inpsyde.com) and I are trying to progressively enhance the experience a little further. We are looking into ways to work against the second issue. You remember? Every time you click the nav button or the closing button, you're adding an entry to your browser history. To prevent this we are looking at the [HTML5 History API](https://diveintohtml5.info/history.html) and other possible solutions like using `window.location.hash`.

In terms of accessibility we will switch from `<li>` to `<label>` for the navigation headlines _Smashing Pages_ and _Smashing Categories_.

All of the above being said, I think the way we built this is very personal and works for us. I don't want to proclaim anything like _this is it_, and I still think we could do better, too. We have ongoing discussions about different ways to integrate the search on mobile which could render the current solution obsolete. Another issue I have with this build is the positioning of the closing buttons not being right on all mobile devices out there because **browsers are pretty bad at math!**

{{< signature "og" >}}
