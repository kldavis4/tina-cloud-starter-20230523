---
title: Building Accessible Menu Systems
author: Heydon Pickering
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb932c19-808d-484d-836b-d91629934104/4-phone-select-800w-opt.png
date: 2017-11-23T16:25:45+00:00
slug: building-accessible-menu-systems
summary: >-
  There are lots of different types of menu on the web. Creating inclusive
  experiences is a question of using the right menu patterns in the right
  places, with the right markup and behavior.
description: >-
  There are lots of different types of menu on the web. Creating inclusive
  experiences is a question of using the right menu patterns in the right
  places, with the right markup and behavior.
categories:
  - Accessibility
---

**Editor’s Note**: _This article originally appeared on [Inclusive Components](https://inclusive-components.design/menus-menu-buttons/). If you’d like to know more about similar inclusive component articles, follow [@inclusicomps](https://twitter.com/inclusicomps) on Twitter or subscribe to the [RSS feed](https://inclusive-components.design/rss/). By supporting [inclusive-components.design](https://www.patreon.com/inclusicomps) on Patreon, you can help to make it the most comprehensive database of robust interface components available._

<p>Classification is hard. Take crabs, for example. Hermit crabs, porcelain crabs, and horseshoe crabs are not &mdash; taxonomically speaking &mdash; <em>true</em> crabs. But that doesn’t stop us using the "crab" suffix. It gets more confusing when, over time and thanks to a process called <em>carcinisation</em>, untrue crabs evolve to resemble true crabs more closely. This is the case with king crabs, which are believed to have been hermit crabs in the past. Imagine the size of their shells!</p>

<p>In design, we often make the same mistake of giving different things the same name. They <em>appear</em> similar, but appearances can be deceptive. This can have an unfortunate effect on the clarity of your component library. In terms of inclusion, it may also lead you to repurpose a semantically and behaviorally inappropriate component. Users will expect one thing and get another.</p>

<p>The term "dropdown" names a classic example. Lots of things "drop down" in interfaces, including the set of <code>&lt;option&gt;</code>s from a <code>&lt;select&gt;</code> element, and the JavaScript-revealed list of links that constitute a navigation submenu. Same name; quite different things. (Some people call these "pulldowns", of course, but let’s not get into that.)</p>

<p>Dropdowns which constitute a set of options are often called "menus", and I want to talk about these here. We shall be devising a <em>true</em> menu, but there’s plenty to be said about not-really-true menus along the way.</p>

{{% feature-panel %}}

<p>Let’s start with a quiz. Is the box of links hanging down from the navigation bar in the illustration a menu?</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82a634a6-cfbc-4e9b-a6ad-a79476025c7e/1-menu-buttons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e61521-6374-407e-9580-d4fe857bb220/1-menu-buttons-800w-opt.png" width="800" height="262" alt="A navigation bar with includes a shop link, underneath which hangs a set of three further links to dog costumes, waffle irons, and magical orbs respectively."/></a><figcaption>A navigation bar with includes a shop link, underneath which hangs a set of three further links to dog costumes, waffle irons, and magical orbs respectively. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82a634a6-cfbc-4e9b-a6ad-a79476025c7e/1-menu-buttons-large-opt.png">Large preview</a>)</figcaption></figure>

The answer is no, not a true menu.</p>

<p>It’s a longstanding convention that navigation schemas are composed of lists of links. A convention nearly as longstanding dictates that sub-navigation should be provided as <em>nested</em> lists of links. If I were to remove the CSS for the component illustrated above, I should see something like the following, except colored blue and in Times New Roman.</p>

<p>Semantically speaking, nested lists of links are correct in this context. Navigation systems are really <strong>tables of content</strong> and this is how tables of content are structured. The only thing that really makes us think “menu” is the styling of the nested lists and the way they are revealed on hover or focus.</p>

<p>That’s where some go wrong and start adding WAI-ARIA semantics: <code>aria-haspopup="true"</code>, <code>role="menu"</code>, <code>role="menuitem"</code> etc. There is a place for these, as we’ll cover, but not here. Here are two reasons why:</p>

<ol>

<li>ARIA menus are not designated for navigation but for application behavior. Imagine the menu system for a desktop application.</li>

<li>The top-level link should be usable <em>as a link</em>, meaning it does not behave like a menu button.</li>

</ol>

<p>Regarding (2): When traversing a navigation region with submenus, one would expect each submenu to appear upon hovering or focusing the "top level" link ("Shop" in the illustration). This both reveals the submenu and places its own links in focus order. With a little help from JavaScript capturing focus and blur events to persist the appearance of the submenus while needed, someone using the keyboard should be able to tab through each link of each tier, in turn.</p>

<p>Menu buttons which take the <code>aria-haspopup="true"</code> property do not behave like this. They are activated on <em>click</em> and have no other purpose than to reveal a secreted menu.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be356acb-48b9-46ae-aba6-8d9de7e9c45e/2-menu-buttons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/892b9a7e-8299-4747-81c2-8ecb2c90e468/2-menu-buttons-800w-opt.png" width="800" height="367" alt="ebook discounts bieten wir "/></a><figcaption>Left: a menu button labeled &#39;menu&#39; with a down-pointing arrow icon and the aria-expanded = false state. Right: The same menu button but with the menu open. This button is in the aria-expanded = true state. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be356acb-48b9-46ae-aba6-8d9de7e9c45e/2-menu-buttons-large-opt.png">Large preview</a>)</figcaption></figure>

As pictured, whether that menu is open or closed should be communicated with <code>aria-expanded</code>. You should only change this state on click, not on focus. Users do not usually expect an explicit change of state on a mere focus event. In our navigation system, state doesn’t really change; it’s just a styling trick. Behaviorally, we can <kbd>Tab</kbd> through the navigation as if no such show/hide trickery were occurring.</p>

## The Problem With Navigation Submenus

<p>Navigation submenus (or "dropdowns" to some) work well with a mouse or by keyboard, but they’re not so hot when it comes to touch. When you press the top-level "Shop" link in our example for the first time, you are telling it to both open the submenu and follow the link.</p>

<p>There are two possible resolutions here:</p>

<ol>

<li>Prevent the default behavior of top-level links (<code>e.preventDefault()</code>) and script in full WAI-ARIA menu semantics and behavior.</li>

<li>Make sure each top-level destination page has a table of contents as an alternative to the submenu.</li>

</ol>

<p>(1) is unsatisfactory because, as I noted previously, these kinds of semantics and behaviors are not expected in this context, where links are the subject controls. Plus users could no longer navigate to a top-level page, if it exists.</p>

### Sidenote: Which devices are touch devices?

<p>It’s tempting to think, “this isn’t a great solution, but I’ll only add it for touch interfaces”. The problem is: how does one detect if a device has a touch screen?</p>

<p>You certainly shouldn’t equate "small screen" with "touch activated". Having worked in the same office as folks making touch displays for museums, I can assure you that some of the largest screens around are touch screens. Dual keyboard and touch input laptops are becoming increasingly prolific too.</p>

<p>By the same token, many but not all smaller devices are touch devices. In inclusive design, you cannot afford to make assumptions.</p>

<p>Resolution (2) is more inclusive and robust in that it provides a "fallback" for users of all inputs. But the scare quotes around the fallback term here are quite deliberate because I actually think in-page tables of content are a <em>superior</em> way of providing navigation.</p>

<p>The award winning <a href="https://www.gov.uk/guidance/content-design/organising-and-grouping-content-on-gov-uk">Government Digital Services team</a> would appear to agree. You may also have seen them on Wikipedia.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea6ed29-b862-4ece-8c0d-a1df4533cd1e/3-gds-wikipedia-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ea6ed29-b862-4ece-8c0d-a1df4533cd1e/3-gds-wikipedia-opt.png" width="703" height="242" alt="Gov.uk tables of content are minimal with hyphens as list styles. Wikipedia provides a bordered grey box with numbered items. Both are labeled contents."/></a><figcaption>Gov.uk tables of content are minimal with hyphens as list styles. Wikipedia provides a bordered grey box with numbered items. Both are labeled contents.</figcaption></figure>

## Tables Of Content

<p>Tables of content are navigation for related pages or page sections and should be semantically similar to main site navigation regions, using a <code>&lt;nav&gt;</code> element, a list, and a group labeling mechanism.</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav aria-labelledby="sections-heading"&gt;
	&lt;h2 id="sections-heading"&gt;Products&lt;/h2&gt;
	&lt;ul&gt;
		&lt;li&gt;&lt;a href="/products/dog-costumes"&gt;Dog costumes&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/products/waffle-irons"&gt;Waffle irons&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/products/magical-orbs"&gt;Magical orbs&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;
&lt;/nav&gt;
&lt;!-- each section, in order, here --&gt;</code></pre></div>

### Notes

<ul>

<li>In this example, we’re imagining that each section is its own page, as it would have been in the dropdown submenu. </li>

<li>It’s important that each of these "Shop" pages has the same structure, with this "Products" table of content present in the same place. Consistency supports understanding.</li>

<li>The list groups the items and enumerates them in assistive technology output, such as a screen reader’s synthetic voice.</li>

<li>The <code>&lt;nav&gt;</code> is recursively labeled by the heading using <code>aria-labelledby</code>. This means "products navigation" will be announced in most screen readers upon entering the region by <kbd>Tab</kbd>. It also means that "products navigation" will be itemized in screen reader element interfaces, from which users can navigate to regions directly.</li>

</ul>

### All on one page

<p>If you can fit all the sections onto one page without it becoming too long and arduous to scroll, even better. Just link to each section’s hash identifier. For example, <code>href="#waffle-irons"</code> should point to <code>id="waffle-irons"</code>.</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav aria-labelledby="sections-heading"&gt;
	&lt;h2 id="sections-heading"&gt;Products&lt;/h2&gt;
	&lt;ul&gt;
		&lt;li&gt;&lt;a href="#dog-costumes"&gt;Dog costumes&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="#waffle-irons"&gt;Waffle irons&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="#magical-orbs"&gt;Magical orbs&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;
&lt;/nav&gt;

&lt;!-- dog costumes section here --&gt;
&lt;section id="waffle-irons" tabindex="-1"&gt;
&lt;h2&gt;Waffle Irons&lt;/h2&gt;
&lt;/section&gt;
&lt;!-- magical orbs section here --&gt;</code></pre></div>

<p>(<strong>Note:</strong> Some browsers are poor at actually sending focus to linked page fragments. Placing <code>tabindex="-1"</code> on the target fragment fixes this.)</p>

<p>Where a site has a lot of content, a carefully constructed information architecture, expressed through the liberal use of tables of content “menus” is infinitely preferable to a precarious and unwieldy dropdown system. Not only is it easier to make responsive, and requires less code to do so, but it makes things clearer: where dropdown systems hide structure away, tables of content lay it bare.</p>

<p>Some sites, including the Government Digital Service’s <a href="https://www.gov.uk/">gov.uk</a>, include index (or “topic”) pages that are <em>just</em> tables of content. It’s such a powerful concept that the popular static site generator Hugo <a href="https://gohugo.io/templates/list/">generates such pages by default</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90cbd8de-3745-4218-aa14-609c9b99e76b/4-menu-buttons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61a9b50e-3f53-485d-83bd-b74909e0dfda/4-menu-buttons-800w-opt.png" width="800" height="261" alt="Family tree style diagram with topic landing page at top with two individual page offshoots. Each of the individual page offshoots have multiple page section offshoots"/></a><figcaption>Family tree style diagram with topic landing page at top with two individual page offshoots. Each of the individual page offshoots have multiple page section offshoots (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90cbd8de-3745-4218-aa14-609c9b99e76b/4-menu-buttons-large-opt.png">Large preview</a>)</figcaption></figure>

Information architecture is a big part of inclusion. A badly organized site can be as technically compliant as you like, but will still alienate lots of users &mdash; especially those with cognitive impairments or those who are pressed for time. </p>

## Navigation Menu Buttons

<p>While we’re on the subject of faux navigation-related menus, it’d be remiss of me not to talk about navigation menu buttons. You’ve almost certainly seen these denoted by a three-line "hamburger" or "navicon" icon.</p>

<p>Even with a pared down information architecture and only one tier of navigation links, space on small screens is at a premium. Hiding navigation behind a button means there’s more room for the main content in the viewport.</p>

<p>A navigation button is the closest thing we’ve studied so far to a <em>true</em> menu button. Since it has the purpose of toggling the availability of a menu on click, it should:</p>

<ol>

<li>Identify itself as a button, not a link;</li>

<li>Identify the expanded or collapsed state of its corresponding menu (which, in strict terms, is just a list of links).</li>

</ol>

### Progressive enhancement

<p>But let’s not get ahead of ourselves. We ought to be mindful of progressive enhancement and consider how this would work without JavaScript.</p>

<p>In an unenhanced HTML document there’s not a lot you can do with buttons (except submit buttons but that’s not even closely related to what we want to achieve here). Instead, perhaps we should start with just a link which takes us to the navigation?</p>

<div class="break-out">

<pre><code class="language-html">&lt;a href="#navigation"&gt;navigation&lt;/a&gt;
&lt;!-- some content here perhaps --&gt;

&lt;nav id="navigation"&gt;
	&lt;ul&gt;
		&lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/about"&gt;About&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/shop"&gt;Shop&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/content"&gt;Content&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;
&lt;/nav&gt;</code></pre></div>

<p>There’s not a lot of point in having the link unless there’s a lot of content between the link and the navigation. Since site navigation should almost always appear near the top of the source order, there’s no need. So, really, a navigation menu in the absence of JavaScript should just be… some navigation.</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav id="navigation"&gt;
	&lt;ul&gt;
		&lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/about"&gt;About&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/shop"&gt;Shop&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/content"&gt;Content&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;
&lt;/nav&gt;</code></pre></div>

<p>You enhance this by adding the button, in its initial state, and hiding the navigation (using the <code>hidden</code> attribute):</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav id="navigation"&gt;
	&lt;button aria-expanded="false"&gt;Menu&lt;/button&gt;
	&lt;ul hidden&gt;
		&lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/about"&gt;About&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/shop"&gt;Shop&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="/contact"&gt;Contact&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;
&lt;/nav&gt;</code></pre></div>

<p>Some older browsers &mdash; you know which ones &mdash; don’t support <code>hidden</code>, so remember to put the following in your CSS. It fixes the problem because <code>display: none</code> has the same affect of hiding the menu from assistive technologies and removing the links from focus order.</p>

<div class="break-out">

<pre><code class="language-css">[hidden] { display: none; }</code></pre></div>

<p>Doing one’s best to support older software is, of course, an act of inclusive design. Some are unable or unwilling to upgrade.</p>

### Placement

<p>Where a lot of people go wrong is by placing the button <em>outside</em> the region. This would mean screen reader users who move to the <code>&lt;nav&gt;</code> using a shortcut would find it to be empty, which isn’t very helpful. With the list hidden from screen readers, they’d just encounter this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav id="navigation"&gt;
&lt;/nav&gt;</code></pre></div>

<p>Here’s how we might toggle state:</p>

<div class="break-out">

<pre><code class="language-js">var navButton = document.querySelector('nav button');
navButton.addEventListener('click', function() {
	let expanded = this.getAttribute('aria-expanded') === 'true' || false;
	this.setAttribute('aria-expanded', !expanded);
	let menu = this.nextElementSibling;
	menu.hidden = !menu.hidden;
});</code></pre></div>

### aria-controls

<p>As I wrote in <a href="https://www.heydonworks.com/article/aria-controls-is-poop">Aria-controls Is Poop</a>, the <code>aria-controls</code> attribute, intended to help screen reader users navigate from a controlling element to a controlled element, is only supported in the JAWS screen reader. So you simply can’t rely on it.</p>

<p>Without a good method for directing users between elements, you should instead make sure one of the following is true:</p>

<ol>

<li>The expanded list’s first link is next in focus order after the button (as in the previous code example).</li>

<li>The first link is focused programmatically upon revealing the list.</li>

</ol>

<p>In this case, I would recommend (1). It’s a lot simpler since you don’t have to worry about moving focus back to the button and on which event(s) to do so. Also, there’s currently nothing in place to warn users that their focus will be moved to somewhere different. In the true menus we’ll be discussing shortly, this is the job of <code>aria-haspopup="true"</code>.</p>

<p>Employing <code>aria-controls</code> doesn’t really do much harm, except that it makes readout in screen readers more verbose. However, some JAWS users may expect it. Here is how it would be applied, using the list’s <code>id</code> as the cipher:</p>

<div class="break-out">

<pre><code class="language-html">&lt;nav id="navigation"&gt;
&lt;button aria-expanded="false" aria-controls="menu-list"&gt;Menu&lt;/button&gt;
&lt;ul id="menu-list" hidden&gt;
	&lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
	&lt;li&gt;&lt;a href="/about"&gt;About&lt;/a&gt;&lt;/li&gt;
	&lt;li&gt;&lt;a href="/shop"&gt;Shop&lt;/a&gt;&lt;/li&gt;
	&lt;li&gt;&lt;a href="/contact"&gt;Contact&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/nav&gt;</code></pre></div>

### The menu and menuitem roles

<p>A <em>true</em> menu (in the WAI-ARIA sense) should identify itself as such using the <code>menu</code> role (for the container) and, typically, <code>menuitem</code> children (<a href="https://www.w3.org/WAI/tutorials/menus/application-menus/">other child roles may apply</a>). These parent and child roles work together to provide information to assistive technologies. Here’s how a list might be augmented to have menu semantics:</p>

<div class="break-out">

<pre><code class="language-html">&lt;ul role="menu"&gt;
	&lt;li role="menuitem"&gt;Item 1&lt;/li&gt;
	&lt;li role="menuitem"&gt;Item 2&lt;/li&gt;
	&lt;li role="menuitem"&gt;Item 3&lt;/li&gt;
&lt;/ul&gt;</code></pre></div>

<p>Since our navigation menu is beginning to behave somewhat like a “true” menu, should these not be present?</p>

<p>The short answer is: no. The long answer is: no, because our list items contain links and <a href="https://w3c.github.io/html-aria/#index-aria-menuitem"><code>menuitem</code> elements are not intended to have interactive descendants</a>. That is, they <em>are</em> the controls in a menu.</p>

<p>We could, of course, suppress the list semantics of the <code>&lt;li&gt;</code>s using <a href="https://www.w3.org/TR/wai-aria/roles#presentation"><code>role="presentation"</code></a> or <code>role="none"</code> (which are equivalent) and place the <code>menuitem</code> role on each link. However, this would suppress the implicit link role. In other words, the example to follow would be announced as “Home, menu item”, <em>not</em> “Home, link” or “Home, menu item, link”. ARIA roles simply override HTML roles.</p>

<div class="break-out">

<pre><code class="language-html">&lt;!-- will be read as "Home, menu item" --&gt;
&lt;li role="presentation"&gt;
&lt;a href="/" role="menuitem"&gt;Home&lt;/a&gt;
&lt;/li&gt;</code></pre></div>

<p>We want the user to know that they are using a link and can expect link behavior, so this is no good. Like I said, true menus are for (JavaScript driven) application behavior.</p>

<p>What we’re left with is a kind of hybrid component, which isn’t quite a true menu but at least tells users whether the list of links is open, thanks to the <code>aria-expanded</code> state. This is a perfectly satisfactory pattern for navigation menus.</p>

### Sidenote: The <code>&lt;select&gt;</code> element

<p>If you’ve been involved in responsive design from the beginning, you may remember a pattern whereby navigation was condensed into a <code>&lt;select&gt;</code> element for narrow viewports.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f071bacd-365b-46c7-9da1-879f800cd7d6/5-menu-buttons-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cb749ed-0fb5-483b-adde-41ea2e72572f/5-menu-buttons-800w-opt.png" width="800" height="554" alt="handset with select element showing “home” selected at top of viewport"/></a><figcaption>Handset with select element showing “home” selected at top of viewport.</figcaption></figure>

As with the checkbox-based <a href="https://inclusive-components.design/toggle-button/">toggle buttons we discussed</a>, using a native element that behaves somewhat as intended without additional scripting is a good choice for efficiency and — especially on mobile — performance. And <code>&lt;select&gt;</code> elements <em>are</em> menus of sorts, with similar semantics to the button-triggered menu we shall soon be constructing.</p>

<p>However, just as with the checkbox toggle button, we’re using an element associated with entering input, not simply making a choice. This is likely to cause confusion for many users &mdash; especially since this pattern uses JavaScript to make the selected <code>&lt;option&gt;</code> behave like a link. The unexpected change of context this elicits is considered a failure according to WCAG’s <a href="https://www.w3.org/TR/WCAG20/#consistent-behavior-unpredictable-change">3.2.2 On Input (Level A)</a> criterion.</p>

## True Menus

<p>Now that we’ve had the discussion about false menus and quasi-menus, the time has arrived to create a <em>true</em> menu, as opened and closed by a true menu button. From here on in I will refer to the button and menu together as simply a “menu button”.</p>

<p>But in what respects will our menu button be true? Well, it’ll be a menu component intended for choosing options in the subject application, which implements all the expected semantics and corresponding behaviors to be considered conventional for such a tool.</p>

<p>As mentioned already, these conventions come from desktop application design. ARIA attribution and JavaScript governed focus management are needed to imitate them fully. Part of the purpose of ARIA is to help web developers create rich web experiences without breaking with usability conventions forged in the native world.</p>

<p>In this example, we’ll imagine our application is some sort of game or quiz. Our menu button will let the user choose a difficulty level. With all the semantics in place, the menu looks like this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;button aria-haspopup="true" aria-expanded="false"&gt;
Difficulty &lt;span aria-hidden="true"&gt;&amp;#x25be;&lt;/span&gt;
&lt;/button&gt;
&lt;div role="menu"&gt;
	&lt;button role="menuitem"&gt;Easy&lt;/button&gt;
	&lt;button role="menuitem"&gt;Medium&lt;/button&gt;
	&lt;button role="menuitem"&gt;Incredibly Hard&lt;/button&gt;
&lt;/div&gt;</code></pre></div>

### Notes

<ul>

<li>The <code>aria-haspopup</code> property simply indicates that the button secretes a menu. It acts as warning that, when pressed, the user will be moved to the “popup” menu (we’ll cover focus behavior shortly). Its value does not change &mdash; it remains as <code>true</code> at all times.</li>

<li>The <code>&lt;span&gt;</code> inside the button contains the unicode point for a black down-pointing small triangle. This convention indicates visually what <code>aria-haspopup</code> does non-visually &mdash; that pressing the button will reveal something below it. The <code>aria-hidden="true"</code> attribution prevents screen readers from announcing <em>“down pointing triangle”</em> or similar. Thanks to <code>aria-haspopup</code>, it’s not needed in the non-visual context.</li>

<li>The <code>aria-haspopup</code> property is complemented by <code>aria-expanded</code>. This tells the user whether the menu is currently in an open (expanded) or closed (collapsed) state by toggling between <code>true</code> and <code>false</code> values.</li>

<li>The menu itself takes the (aptly named) <code>menu</code> role. It takes descendants with the <code>menuitem</code> role. They do not need to be direct children of the <code>menu</code> element, but they are in this case &mdash; for simplicity.</li>

</ul>

## Keyboard And Focus Behavior

<p>When it comes to making interactive controls keyboard accessible, the best thing you can do is use the right elements. Because we’re using <code>&lt;button&gt;</code> elements here, we can be assured that click events will fire on <kbd>Enter</kbd> and <kbd>Space</kbd> keystrokes, as specified in <a href="https://developer.mozilla.org/en/docs/Web/API/HTMLButtonElement">the HTMLButtonElement interface</a>. It also means that we can disable the menu items using the button-associated <code>disabled</code> property.</p>

<p>There’s a lot more to menu button keyboard interaction, though. Here’s a summary of all the focus and keyboard behavior we’re going to implement, based on <a href="https://www.w3.org/TR/wai-aria-practices-1.1/#menubutton">WAI-ARIA Authoring Practices 1.1</a>:</p> <table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap><thead> <tr> <th data-tablesaw-priority="persist"></th> <th></th> </tr> </thead> <tbody> <tr> <td><kbd>Enter</kbd>, <kbd>Space</kbd> or <kbd>↓</kbd> on the menu button</td> <td>Opens the menu</td> </tr> <tr> <td><kbd>↓</kbd> on a menu item</td> <td>Moves focus to the next menu item, or the first menu item if you’re on the last one</td> </tr> <tr> <td><kbd>↑</kbd> on a menu item</td> <td>Moves focus to the previous menu item, or the last menu item if you’re on the first one</td> </tr> <tr> <td><kbd>↑</kbd> on the menu button</td> <td>Closes the menu if open</td> </tr> <tr> <td><kbd>Esc</kbd> on a menu item</td> <td>Closes the menu and focuses the menu button</td> </tr> </tbody> </table>

<p>The advantage of moving focus between menu items using the arrow keys is that <kbd>Tab</kbd> is preserved for moving out of the menu. In practice, this means users don’t have to move through every menu item to exit the menu — a huge improvement for usability, especially where there are many menu items.</p>

<p>The application of <code>tabindex="-1"</code> makes the menu items unfocusable by <kbd>Tab</kbd> but preserves the ability to focus the elements programmatically, upon capturing key strokes on the arrow keys.</p>

<div class="break-out">

<pre><code class="language-html">&lt;button aria-haspopup="true" aria-expanded="false"&gt;
Difficulty &lt;span aria-hidden="true"&gt;&amp;#x25be;&lt;/span&gt;
&lt;/button&gt;
&lt;div role="menu"&gt;
	&lt;button role="menuitem" tabindex="-1"&gt;Easy&lt;/button&gt;
	&lt;button role="menuitem" tabindex="-1"&gt;Medium&lt;/button&gt;
	&lt;button role="menuitem" tabindex="-1"&gt;Incredibly Hard&lt;/button&gt;
&lt;/div&gt;</code></pre></div>

### The open method

<p>As part of a sound API design, we can construct methods for handling the various events.</p>

<p>For example, the <code>open</code> method needs to switch the <code>aria-expanded</code> value to “true”, change the menu’s hidden property to <code>false</code>, and focus the first <code>menuitem</code> in the menu that isn’t disabled:</p>

<div class="break-out">

<pre><code class="language-js">MenuButton.prototype.open = function () {
	this.button.setAttribute('aria-expanded', true);
	this.menu.hidden = false;
	this.menu.querySelector(':not(\[disabled])').focus();
	return this;
}</code></pre></div>

<p>We can execute this method where the user presses the down key on a focused menu button instance:</p>

<div class="break-out">

<pre><code class="language-js">this.button.addEventListener('keydown', function (e) {
	if (e.keyCode === 40) {
		this.open();
	}
}.bind(this));</code></pre></div>

<p>In addition, a developer using this script will now be able to open the menu programmatically:</p>

<div class="break-out">

<pre><code class="language-js">exampleMenuButton = new MenuButton(document.querySelector('\[aria-haspopup]'));
exampleMenuButton.open();</code></pre></div>

### Sidenote: The checkbox hack

<p>As much as possible, it’s better not to use JavaScript unless you need to. Involving a third technology on top of HTML and CSS is necessarily an increase in systemic complexity and fragility. However, not all components can be satisfactorily built without JavaScript in the mix.</p>

<p>In the case of menu buttons, an enthusiasm for making them “work without JavaScript” has led to something called the checkbox hack. This is where the checked (or unchecked) state of a hidden checkbox is used to toggle the visibility of a menu element using CSS.</p>

<div class="break-out">

<pre><code class="language-css">/* menu closed */
[type="checkbox"] + [role="menu"] {
	display: none;
}

/* menu open */
[type="checkbox"]:checked + [role="menu"] {
	display: block;
}</code></pre></div>

<p>To screen reader users, the checkbox role and checked state are nonsensical in this context. This can be partly overcome by adding <code>role="button"</code> to the checkbox.</p>

<div class="break-out">

<pre><code class="language-html">&lt;input type="checkbox" role="button" aria-haspopup="true" id="toggle"&gt;</code></pre></div>

<p>Unfortunately, this suppresses the implicit checked state communication, depriving us of JavaScript-free state feedback (poor though it would have been as “checked” in this context).</p>

<p>But it <em>is</em> possible to spoof <code>aria-expanded</code>. We just need to supply our label with two spans as below.</p>

<div class="break-out">

<pre><code class="language-html">&lt;input type="checkbox" role="button" aria-haspopup="true" id="toggle" class="vh"&gt;
&lt;label for="toggle" data-opens-menu&gt; Difficulty &lt;span class="vh expanded-text"&gt;expanded&amp;lt;/span&gt;
	&lt;span class="vh collapsed-text"&gt;collapsed&lt;/span&gt;
	&lt;span aria-hidden="true"&gt;&amp;#x25be;&lt;/span&gt;
&lt;/label&gt;</code></pre></div>

<p>These are both visually hidden using <a href="https://a11yproject.com/posts/how-to-hide-content/">the <code>visually-hidden</code> class</a>, but — depending on which state we’re in — only one is hidden to screen readers as well. That is, only one has <code>display: none</code>, and this is determined by the extant (but not communicated) checked state:</p>

<div class="break-out">

<pre><code class="language-css">/* class to hide spans visually */
.vh {
	position: absolute !important;
	clip: rect(1px, 1px, 1px, 1px);
	padding: 0 !important;
	border: 0 !important;
	height: 1px !important;
	width: 1px !important;
	overflow: hidden;
}

/* reveal the correct state wording to screen readers based on state */

[type="checkbox"]:checked + label .expanded-text {
	display: inline;
}

[type="checkbox"]:checked + label .collapsed-text {
	display: none;
}

[type="checkbox"]:not(:checked) + label .expanded-text {
	display: none;
}

[type="checkbox"]:not(:checked) + label .collapsed-text {
	display: inline;
}</code></pre></div>

<p>This is clever and all, but our menu button is still incomplete since the expected focus behaviors we’ve been discussing simply cannot be implemented without JavaScript.</p>

<p>These behaviors are conventional and expected, making the button more usable. However, if you really need to implement a menu button without JavaScript, this is about as close as you can get. Considering the cut-down navigation menu button I covered previously offers menu content that is <em>not</em> JavaScript dependent itself (i.e. links), this approach may be a suitable option.</p>

<p>For fun, <a href="https://codepen.io/heydon/pen/afdeffcc8a349ab8138e32573ec85cd3">here’s a codePen implementing a JavaScript-free navigation menu button</a>.</p>

<p data-height="265" data-theme-id="0" data-slug-hash="vmKVJK" data-default-tab="css,result" data-user="heydon" data-embed-version="2" data-pen-title="Navigation menu button example no JS" class="codepen">See the Pen <a href="https://codepen.io/heydon/pen/vmKVJK/">Navigation menu button example no JS</a> by Heydon (<a href="https://codepen.io/heydon">@heydon</a>) on <a href="https://codepen.io">CodePen</a>.</p> <script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

<p>(<strong>Note:</strong> Only <kbd>Space</kbd> opens the menu.)</p>

### The "choose" event

<p>Executing some methods should emit events so that we can set up listeners. For example, we can emit a <code>choose</code> event when a user clicks a menu item. We can set this up using <code>CustomEvent</code>, which lets us pass an argument to the event’s <code>detail</code> property. In this case, the argument (“choice”) would be the chosen menu item’s DOM node.</p>

<div class="break-out">

<pre><code class="language-js">MenuButton.prototype.choose = function (choice) {
	// Define the 'choose' event
	var chooseEvent = new CustomEvent('choose', {
		detail: {
			choice: choice
		}
	});
 	// Dispatch the event
 	this.button.dispatchEvent(chooseEvent);
 	return this;
 }</code></pre></div>

<p>There are all sorts of things we can do with this mechanism. Perhaps we have a live region set up with an <code>id</code> of <code>menuFeedback</code>:</p>

<div class="break-out">

<pre><code class="language-html">&lt;div role="alert" id="menuFeedback"&gt;&lt;/div&gt;</code></pre></div>

<p>Now we can set up a listener and populate the live region with the information secreted inside the event:</p>

<div class="break-out">

<pre><code class="language-js">
exampleMenuButton.addEventListener('choose', function (e) {
	// Get the node's text content (label)
	var choiceLabel = e.details.choice.textContent;

	// Get the live region node
	var liveRegion = document.getElementById('menuFeedback');

	// Populate the live region
	liveRegion.textContent = 'Your difficulty level is ${choiceLabel}';
});</code></pre></div>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ce5a0ed-7288-4a3f-8ff8-24bbc36e8735/6-menu-buttons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c29f29c-59a2-42cf-8762-cb72e33f25d2/6-menu-buttons-800w-opt.png" width="800" height="257" alt="When a user chooses an option, the menu closes and focus is returned to the menu button. It’s important users are returned to the triggering element after the menu is closed." /></a><figcaption>When a user chooses an option, the menu closes and focus is returned to the menu button. It’s important users are returned to the triggering element after the menu is closed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ce5a0ed-7288-4a3f-8ff8-24bbc36e8735/6-menu-buttons-large-opt.png">Large preview</a>)</figcaption></figure>

When a menu item is selected, the screen reader user will hear, <em>“You chose [menu item’s label]”</em>. A live region (defined here with the <code>role="alert"</code> attribution) announces its content in screen readers whenever that content changes. The live region isn’t mandatory, but it is an example of what might happen in the interface as a response to the user making a menu choice.</p>

## Persisting Choices

<p>Not all menu items are for choosing persistent settings. Many just act like standard buttons which make something in the interface happen when pressed. However, in the case of our difficulty menu button, we’d like to indicate which is the current difficulty setting &mdash; the one chosen last.</p>

<p>The <code>aria-checked="true"</code> attribute works for items that, instead of <code>menuitem</code>, take the <code>menuitemradio</code> role. The enhanced markup, with the second item checked (<em>set</em>) looks like this:</p>

<div class="break-out">

<pre><code class="language-html">&lt;button aria-haspopup="true" aria-expanded="false"&gt; Difficulty
&lt;span aria-hidden="true"&gt;&amp;#x25be;&lt;/span&gt;
&lt;/button&gt;
&lt;div role="menu"&gt;
	&lt;button role="menuitemradio" tabindex="-1"&gt;Easy&lt;/button&gt;
	&lt;button role="menuitemradio" aria-checked="true" tabindex="-1"&gt;Medium&lt;/button&gt;
	&lt;button role="menuitemradio" tabindex="-1"&gt;Incredibly Hard&lt;/button&gt;
&lt;/div&gt;</code></pre></div>

<p>Native menus on many platforms indicate chosen items using check marks. We can do that with no trouble using a little extra CSS:</p>

<div class="break-out">

<pre><code class="language-css">
[role="menuitem"] [aria-checked="true"]::before {
content: '\2713\0020';
}</code></pre></div>

<p>While traversing the menu with a screen reader running, focusing this checked item will prompt an announcement like <em>“check mark, Medium menu item, checked”</em>.</p>

<p>The behavior on opening a menu with a checked <code>menuitemradio</code> differs slightly. Instead of focusing the first (enabled) item in the menu, the <em>checked</em> item is focused instead.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4134d8a8-81e7-411b-afe0-c4bdb78389c9/7-menu-buttons-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d66f1f9-5701-48ea-9879-f337a05575a4/7-menu-buttons-800w-opt.png" width="800" height="249" alt="The menu button starts with the menu unopened. On opening the second (Medium) difficulty setting is focused. It is prefixed with a check mark based on the aria-checked attribute&#39;s presence."/></a><figcaption>The menu button starts with the menu unopened. On opening the second (Medium) difficulty setting is focused. It is prefixed with a check mark based on the aria-checked attribute&#39;s presence. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4134d8a8-81e7-411b-afe0-c4bdb78389c9/7-menu-buttons-large-opt.png">Large preview</a>)</figcaption></figure>

What’s the benefit of this behavior? The user (any user) is reminded of their previously selected option. In menus with numerous incremental options (for example, a set of zoom levels), people operating by keyboard are placed in the optimal position to make their adjustment.</p>

## Using The Menu Button With A Screen Reader

<p>In this video, I’ll show you what it’s like to use the menu button with the Voiceover screen reader and Chrome. The example uses items with <code>menuitemradio</code>, <code>aria-checked</code> and the focus behavior discussed. Similar experiences can be expected across the gamut of popular screen reader software.</p>

<iframe loading="lazy" width="560" height="315" src="https://www.youtube.com/embed/Aw_HMHdId88" frameborder="0" allowfullscreen></iframe>

## Inclusive Menu Button On Github

<p><a href="https://twitter.com/KittyGiraudel">Kitty Giraudel</a> and I have worked together on creating a menu button component with the API features I have described, and more. You have Hugo to thank for many of these features, since they were based on the work they did on <a href="https://github.com/KittyGiraudel/a11y-dialog">a11y-dialog</a> — an accessible modal dialog. It is <a href="https://github.com/Heydon/inclusive-menu-button">available on Github</a> and NPM.</p>

<div class="break-out">

<pre><code class="language-terminal">npm i inclusive-menu-button --save</code></pre></div>

<p>In addition, Kitty has created a <a href="https://github.com/KittyGiraudel/react-menu-button">React version</a> for your delectation.</p>

## Checklist

<ul>

<li>Don’t use ARIA menu semantics in navigation menu systems.</li>

<li>On content heavy sites, don’t hide structure away in nested dropdown-powered navigation menus.</li>

<li>Use <code>aria-expanded</code> to indicate the open/closed state of a button-activated navigation menu.</li>

<li>Make sure said navigation menu is next in focus order after the button that opens/closes it.</li>

<li>Never sacrifice usability in the pursuit of JavaScript-free solutions. It’s vanity.</li>

</ul>

{{< signature "il" >}}

