---
title: 'Mobile And Accessibility: Why You Should Care And What You Can Do About It'
slug: mobile-accessibility-why-care-what-can-you-do
image: >-
  https://www.smashingmagazine.com/general/2013/08/07/137143-revision-32/attachment/enter-key/
date: 2014-05-21T14:18:15.000Z
author: tj-vantoll
description: >-
  Mobile has revolutionized the way we use the web. This is especially true of
  disabled users, for whom mobile devices open the door to a whole new spectrum
  of interactions.
categories:
  - Mobile
  - UX
  - Accessibility
---
Mobile has revolutionized the way we use the web. This is especially true of disabled users, for whom mobile devices open the door to a whole new spectrum of interactions.

And they are taking advantage of it. A <a href="https://www.wirelessrerc.org/sites/default/files/publications/SUNspot_2013-03_Wireless_Devices_and_Adults_with_Disabilities_2013-07-12%5B1%5D.pdf">July 2013 survey</a> (PDF) of adults with disabilities done by the <a href="https://www.wirelessrerc.org/">Wireless Rehabilitation Engineering Research Center</a> found that 91% of people with disabilities use a “wireless device such as a cell phone or tablet.” Among these users, screen reader usage is common, even on mobile devices.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/#further-reading-on-smashingmag)

*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [Accessibility Originates With UX: A BBC iPlayer Case Study](https://www.smashingmagazine.com/2015/02/bbc-iplayer-accessibility-case-study/)
*   [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)
*   [Making Accessibility Simpler, With Ally.js](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/)
*   [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)

A <a href="https://webaim.org/projects/screenreadersurvey4/#mobile">study of 1782 screen reader users</a> done by <a href="https://webaim.org/">Web Accessibility in Mind</a> (WebAIM) in 2012 showed that 71.8% used screen readers on their mobile devices. And we're not talking about only a handful of people. The 2010 U.S. Census found that <a href="https://www.census.gov/newsroom/releases/archives/miscellaneous/cb12-134.html">nearly one in five people have a disability</a>!

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c892bca-60b3-4ad1-96cb-bee6bcc84754/webaim-mobile-survey.png" alt="Graphical representation of WebAIM's survey results" /><br>
<em>
The results of WebAIM’s study of screen reader users (Source: <a href="https://webaim.org/projects/screenreadersurvey4/#mobile">WebAIM</a>)</em>

Despite this, many basic best practices for accessibility are forgotten on mobile websites. Developers implement complex solutions such as responsive design and responsive images, yet forget about basic techniques such as image replacement. Therefore, disabled users — who have a difficult enough time on the desktop — are frequently presented with interfaces that are at best frustrating, and at worst, impossible to use.

While accessibility can be a complex topic, following a few best practices goes a long way towards building accessible sites and applications. In this article we'll discuss a few practical measures that address the most common issues disabled users encounter. Specifically, we’ll look at the importance of the following:

*   making sure everything works with a keyboard,
*   marking up forms semantically,
*   providing plenty of contrast,
*   ensuring that screen readers know what your controls do,
*   testing your website on an actual screen reader.

We’ll see that following these best practices leads to a better experience for everyone, not just disabled users. Let’s get started by looking at a piece of hardware rarely considered in the mobile space: the keyboard.</p>

## 1\. Make Sure Everything Works With The Keyboard

While we usually associate keyboards with traditional desktops and laptops, the situation is no longer that simple. Microsoft’s Surface tablet has a keyboard built into the cover, Bluetooth keyboards are made to work seamlessly on iOS and Android, and some <a href="https://www.google.com/search?site=&amp;tbm=isch&amp;source=hp&amp;biw=1600&amp;bih=1008&amp;q=roll-up+keyboard&amp;oq=roll-up+keyboard">keyboards can even be rolled up</a> for traveling.

Keyboard navigation on mobile websites has become increasingly important also because more websites are built responsively. Because these websites serve the same markup to all devices, the keyboard must function correctly, even if the vast majority of visitors use a touchscreen.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bb9eadb-7537-46a0-9caa-e23924168e3c/keyboard.jpg" alt="Image of a keyboard" /><br>
<em>Keyboard support is important, even on mobile. (Image: <a href="https://www.flickr.com/photos/24285431@N04/2375499336">Shane Pope</a>)</em>

Try putting your mouse away and visiting your website. Can you perform <em>all</em> tasks using only your keyboard? If not, then neither can keyboard users. Two main problems break keyboard navigation on the web. Let’s discuss each.</p>

### Not Using the Correct Element for the Task

Web browsers are really good at making keyboard navigation work automatically, as long as you use semantically appropriate elements. In particular, the following elements are focusable by default: <code>&lt;button&gt;</code>, <code>&lt;a&gt;</code> (with an <code>href</code> attribute), <code>&lt;input&gt;</code>, <code>&lt;select&gt;</code> and <code>&lt;textarea&gt;</code>. For these elements, keyboard navigation just works without any extra effort. However, developers frequently fail to use these elements appropriately, specifically <code>&lt;button&gt;</code> and <code>&lt;a&gt;</code>.

Buttons should be used for controls that perform actions, whereas links should be used for controls that navigate users to other documents. However, developers often incorrectly use generic elements, such as <code>&lt;span&gt;</code> and <code>&lt;div&gt;</code>, for controls that perform these actions. Consider the <a href="https://www.fidelity.com/interstitial/index.shtml">iPhone landing page of Fidelity</a>, a banking institution.

<img style="height: 250px;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/240c189a-dcd7-415c-9fba-13c03bca3a01/fidelity.png" alt="Fidelity's home page" /><br>
<em>
Are those buttons on Fidelity’s iPhone landing page or not?</em>

The two controls on this page sure look like buttons, but they’re actually generated by the following markup.

<pre><code class="language-markup">
&lt;div id="download_button"&gt;
	&lt;div id="download_text" onclick="goToStore();"&gt;Download the Fidelity App&lt;/div&gt;
&lt;/div&gt;

&lt;div id="no_thanks_button" onclick="goHome();"&gt;
	&lt;div id="no_thanks_text" onclick="goHome();"&gt;No thanks&lt;/div&gt;
&lt;/div&gt;
</code></pre>

Because of this, keyboards will not navigate to these controls. They would, however, if the controls were marked up as actual <code>&lt;button&gt;</code> elements.

<pre><code class="language-markup">
&lt;div id="download_button"&gt;
	&lt;button id="download_text" onclick="goToStore();"&gt;Download the Fidelity App&lt;/button&gt;
&lt;/div&gt;

&lt;div id="no_thanks_button" onclick="goHome();"&gt;
	&lt;button id="no_thanks_text" onclick="goHome();"&gt;No thanks&lt;/button&gt;
&lt;/div&gt;
</code></pre>

While this most commonly happens with buttons, links are often misused as well. Consider the popup that people see when visiting <a href="https://www.americanexpress.com/">American Express’ home page</a> on an iPad:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce6c631f-bfa8-442c-a75a-163e4c1bdfa9/americanexpress.png" alt="American Express' home page" /><br>
<em>
American Express shows this popup to iPad users on its home page.</em>

Despite the “Click here to download the American Express app” being a simple link, American Express uses the following HTML:

<pre><code class="language-markup">
&lt;div class="asl-link" role="link"&gt;
	&lt;div class="asl-app-store" title="..."&gt;
		Click here to download the American Express® App
	&lt;/div&gt;
&lt;/div&gt;
</code></pre>

The linking is done in JavaScript, with a click handler that changes <code>window.location</code>. Because a <code>&lt;div&gt;</code> is used, keyboards cannot access the control, but they would be able to if an <code>&lt;a&gt;</code> element were used.

<pre><code class="language-markup">
&lt;div class="asl-link"&gt;
	&lt;a href="..." class="asl-app-store"&gt;
		Click here to download the American Express® App
	&lt;/a&gt;
&lt;/div&gt;
</code></pre>

(On a related note, the “close” button in American Express’ popup is also a <code>&lt;div&gt;</code>, so keyboard users can neither perform that action in the popup nor close it.)

American Express could also have used the <a href="https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html">Apple approved</a> method of informing users that an app is available with an <code>apple-itunes-app</code> <code>&lt;meta&gt;</code> tag.

<pre><code class="language-markup">
&lt;meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL"&gt;
</code></pre>

In general, browsers provide keyboard access automatically for semantic elements. But what if you’re using elements more complex than a simple <code>&lt;button&gt;</code> or <code>&lt;a&gt;</code>?

### Writing Your Own Complex Widgets

As web developers, we often use widgets for complex interactions in our interfaces. We do this sometimes to work around deficiencies in a platform (for example, to build a more customizable <code>&lt;select&gt;</code> element) and sometimes to build a powerful UI element (for example, a grid, tab or chart).

Let’s look at replacing a <code>&lt;select&gt;</code> element. On the surface, this seems like an easy widget to write:

1.  Create a `<div>`.
2.  Create a `<ul>`, with an `<li>` element for each replacement `<option>`.
3.  On a click of the `<div>`, open the menu.
4.  On a click of an `<li>` element, transfer the value back into the `<div>`.

Easy.

However, consider all of the keyboard controls that a native <code>&lt;select&gt;</code> element has:

*   The space bar opens the menu of options.
*   The up and down arrows open the menu and cycle between options.
*   The page-up and page-down keys cycle through whole pages of options in long lists.
*   The “Escape” key closes the menu.
*   Typing in values while the element has focus will trigger autocompletion options.

Suddenly, replicating the native <code>&lt;select&gt;</code> element has gotten significantly harder. Not to mention that we have to ensure that screen readers can access the options and read them at the appropriate time.

To make these complex interactions possible, a special set of HTML attributes is available to provide the necessary context to screen readers. These are known as <a href="https://developer.mozilla.org/en-US/docs/Accessibility/ARIA">Accessible Rich Internet Applications</a>, or ARIA attributes.

The main ARIA attribute, <code>role</code>, tells browsers and assistive devices the general type of an object — for example, dialog, slider or alert. From there, a number of <code>aria-*</code> attributes are used to provide more detailed information about an element’s state. Below is a boilerplate for developing an accessible <code>&lt;select&gt;</code> replacement.

<pre><code class="language-markup">
&lt;span tabindex="0" id="button" role="combobox"
	aria-expanded="false" aria-autocomplete="list" aria-owns="menu"
	aria-haspopup="true" aria-activedescendant="option-1"
	aria-labelledby="option-1" aria-disabled="false"&gt;
		One
&lt;/span&gt;

&lt;ul aria-hidden="true" aria-labelledby="button" id="menu"
	role="listbox" tabindex="0" aria-activedescendant="option-1"
	style="display: none;"&gt;
		&lt;li id="option-1" role="option" tabindex="-1"&gt;One&lt;/li&gt;
		&lt;li id="option-2" role="option" tabindex="-1"&gt;Two&lt;/li&gt;
		&lt;li id="option-3" role="option" tabindex="-1"&gt;Three&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

Screen readers use these ARIA attributes to help keyboard users operate these controls. For example, because this example's <code>&lt;span&gt;</code> has a <code>role</code> of <code>"combobox"</code>, VoiceOver on OS X reads "You are currently on a combo box, type text or, to display a list of choices, press Control-Option-Space." VoiceOver knows what choices are available because the <code>&lt;span&gt;</code> has an <code>aria-owns</code> attribute set to <code>"menu"</code>, the <code>id</code> of the <code>&lt;ul&gt;</code> that contains the options.

But as you can see, there are a whole lot of ARIA attributes to account for; therefore, because of the difficultly of getting this right, most developers are better off using a JavaScript UI library for such controls rather than building them themselves. Many big libraries ensure that these controls are accessible by applying appropriate <a href="https://developer.mozilla.org/en-US/docs/Accessibility/ARIA/ARIA_Techniques">ARIA roles</a> and keyboard shortcuts automatically. For example, <a href="https://wiki.jqueryui.com/w/page/12138056/Selectmenu">jQuery UI’s upcoming <code>selectmenu</code></a> and <a href="https://demos.kendoui.com/web/dropdownlist/index.html">Kendo UI’s <code>DropDownList</code></a> both generate accessible <code>&lt;select&gt;</code> replacements.

This concludes our look at supporting keyboard navigation on the web. While this set of guidelines is by no means comprehensive, it should help you get the most important parts of your website working properly. For a more thorough list of keyboard accessibility, see the <a href="https://www.w3.org/WAI/WCAG20/quickref/#keyboard-operation">W3C’s complete guidelines</a>.

Next, we’ll look at another often abused best practice: building semantic forms.</p>

## 2\. Mark Up Forms Semantically

With the proliferation of single-page applications — especially mobile ones — a diminishing number of websites use native HTML form submissions. Instead, data is submitted to the server by JavaScript-initiated <code>XMLHttpRequest</code>s. While nothing is inherently wrong with this, using the same semantic markup that you would use if the data were to be sent with a native HTML form submission is still important.

Most screen readers have entire modes dedicated to form interaction that require forms to be marked up correctly. Consider this log-in form:

<pre><code class="language-markup">
Username: &lt;input type="text" id="username" name="username"&gt;
Password: &lt;input type="password" id="password" name="password"&gt;
&lt;button&gt;Submit&lt;/button&gt;
&lt;script&gt;
	document.querySelector( "button" )
		.addEventListener( "click", function() {
			// Send AJAX request to log user in
		});
&lt;/script&gt;
</code></pre>

While this form will log users in, it has a few problems that would make it painful for power users and impossible for impaired users to complete. Let’s look at the issues in turn.</p>

### Associating Labels With Inputs

Most screen readers require that form elements — <code>&lt;input&gt;</code>, <code>&lt;select&gt;</code> and <code>&lt;textarea&gt;</code> — be associated with <code>&lt;label&gt;</code> elements that describe them. Each <code>&lt;label&gt;</code> element should have a <code>for</code> attribute that corresponds to the appropriate form element’s <code>id</code> attribute, as shown here:

<pre><code class="language-markup">
&lt;label for="field"&gt;Field:&lt;/label&gt;
&lt;input id="field"&gt;
</code></pre>

As is, our log-in form does not have this association, which would trip up assistive devices. Below is the user name <code>&lt;input&gt;</code> that we’re currently using. Note that there is no <code>&lt;label&gt;</code>.

<pre><code class="language-markup">
Username: &lt;input type="text" id="username" name="username"&gt;
</code></pre>

When this user name <code>&lt;input&gt;</code> gets focus, the screen reader <a href="https://www.nvaccess.org/">NVDA</a> simply reads “Edit text, blank.”

This is common in the wild, unfortunately. Amazon, for instance, has a trimmed-down website, <a href="https://amazon.com/access">amazon.com/access</a>, that is “optimized for screen readers and mobile devices.”

The website is appropriately simple, with a single search box and a short list of links. Ironically, though, despite directing screen reader users to this page, Amazon has not given its search <code>&lt;input&gt;</code> a <code>&lt;label&gt;</code>; thus, many screen reader users will have no idea that the <code>&lt;input&gt;</code> can be used to search.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d02b3ed-59e6-4425-b254-1bdbe5a92347/amazon.png" alt="Image showing that amazon.com/access does not have a label for its search field." /><br>
<em>Amazon’s accessible website does not associate the “Search” label with the text box.</em>

(Note: As with browsers, screen readers vary in their support of markup patterns. In the example above, VoiceOver does read the “Search” text, but NVDA does not. We’ll discuss compatibility testing later in this article.)

We can easily solve this problem in our sample form with a few <code>&lt;label&gt;</code> elements:

<pre><code class="language-markup">
&lt;label for="username"&gt;Username:&lt;/label&gt;
&lt;input type="text" id="username" name="username"&gt;

&lt;label for="password"&gt;Password:&lt;/label&gt;
&lt;input type="password" id="password" name="password"&gt;

&lt;button&gt;Submit&lt;/button&gt;
&lt;script&gt;
	document.querySelector( "button" )
		.addEventListener( "click", function() {
			// Send AJAX request to log user in
		});
&lt;/script&gt;
</code></pre>

Now all screen readers will associate each form element with a label that describes it. This practice is beneficial to more than users of assistive devices. All browsers are smart enough to transfer clicks on <code>&lt;label&gt;</code> elements to their associated <code>&lt;input&gt;</code>, <code>&lt;select&gt;</code> or <code>&lt;textarea&gt;</code> elements.

Ever had trouble clicking a 10 × 10-pixel checkbox to accept a service’s terms of use? On websites with semantic markup, you can click a checkbox’s far larger label instead. On mobile devices, bigger targets help fat fingers hit them:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4612eed-e646-4c77-8888-929e67c2a4a5/label-focus.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4612eed-e646-4c77-8888-929e67c2a4a5/label-focus.png" alt="Image showing the effect of using labels on form elements" /></a><br>
<em>Clicking a label gives focus to the corresponding control.</em>

This solves one problem with our log-in form. But there’s still one more issue to discuss.</p>

### Handling the “Enter” Key

Have you ever noticed that some log-in forms on the web can be submitted by pressing the “Enter” key in a textbox and some cannot? What makes the “Enter” key work for a submission?

Submitting with the “Enter” key is known as an implicit submission, and it is supported by all browsers — even mobile ones. There are only two requirements to making implicit submission work.

1.  All `<input>` elements need to be in a `<form>`.
2.  If the form has more than one element — `<input>`, `<select>` or `<textarea>` — then the `<form>` must have a “Submit” button.

Our sample form already has a “Submit” button (the default <code>type</code> of <code>&lt;button&gt;</code> is <code>submit</code>). Therefore, we only need to add a <code>&lt;form&gt;</code>.

<pre><code class="language-markup">
&lt;form method="POST"&gt;
	&lt;label for="username"&gt;Username:&lt;/label&gt;
	&lt;input type="text" id="username" name="username"&gt;

	&lt;label for="password"&gt;Password:&lt;/label&gt;
	&lt;input type="password" id="password" name="password"&gt;

	&lt;button&gt;Submit&lt;/button&gt;
&lt;/form&gt;
&lt;script&gt;
	document.querySelector( "button" )
		.addEventListener( "click", function( event ) {
			// Prevent the default form submission
			event.preventDefault();

		// Send AJAX request
	});
&lt;/script&gt;
</code></pre>

A couple of things to note:

*   When implicit submission occurs, the browser performs a click on the `<form>`’s “Submit” button. Therefore, listening for `click` events on the “Submit” button to perform submit actions is still safe. You could, alternatively, listen for a `submit` event on the `<form>`.
*   Even though JavaScript will intercept the form’s submission, `method="POST"` is still explicitly declared. In case JavaScript fails (because of unsupported browsers, network issues, etc.), we don’t want the browser to submit a `GET` request that would place the user-supplied user name and password in the query string.

Enabling implicit submission saves mobile users some clicking. The image below shows two <code>&lt;input&gt;</code> elements, one in a <code>&lt;form&gt;</code> and one not. Note that the <code>&lt;form&gt;</code>-based example can be submitted while the <code>&lt;input&gt;</code> has focus — no need for additional taps or hunting for a “Submit” button.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f3937c-5bc1-42a3-8026-2367d1fa113e/enter-key.png" alt="This image shows two input elements, one in a form and one not. The one in the form has a Go button that submits the form, and the one not in the form has a Return button that does not submit the form." /><br>
<em>Implicit form submission works only with true form elements.</em>

This concludes our look at building accessible forms. As with keyboard access, these guidelines are far from comprehensive, but they address some of the most common problems with forms today. For a more complete list of best practices, check out the W3C’s <a href="https://www.w3.org/WAI/WCAG20/quickref/#minimize-error">guidelines for collecting input from users</a>.

Next, we’ll look at a problem that most smartphone owners have experienced at some point: low contrast.</p>

## 3\. Provide Plenty Of Contrast

If you’ve ever used your phone outdoors, especially in harsh sunlight, then you’ve struggled to read the screen at some point. This is not unlike what some users with vision disabilities experience all of the time.

When designing any website, remember that most users will not be visiting it indoors on a high-end monitor like yours. This is especially critical for mobile websites because of the wide variety of contexts in which people use their phone.

How do you make your website adapt to these contexts? Unlike more subjective aspects, contrast ratio can be calculated, and the W3C puts numeric guidelines for these ratios in its “<a href="https://www.w3.org/TR/WCAG/">Web Content Accessibility Guidelines</a>” (WCAG), a series of recommendations for making web content more accessible to individuals with disabilities.

The WCAG defines three levels of conformance: Level A, Level AA and Level AAA. <a href="https://www.w3.org/TR/WAI-WEBCONTENT/#wc-priority-1">According to the specification</a>, for a website to conform, Level A requirements <strong>must</strong> be met, Level AA requirements <strong>should</strong> be met and Level AAA requirements <strong>may</strong> be met.

The Level A contrast ratio is set at 3:1; Level AA is set at 4.5:1; and Level AAA is set at 7:1. As a point of reference, the <a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html">specification recommends</a> a contrast ratio of 4.5:1 for users with 20/40 vision, which is common among elderly people.

This means that we should make our contrast ratios at least 3:1 and, ideally, 4.5:1 or greater. But, how exactly do we calculate this?

### Calculating Contrast Ratio

Luckily, <a href="https://lea.verou.me/">Lea Verou</a> has <a href="https://leaverou.github.io/contrast-ratio/">created a tool to calculate contrast ratio</a> easily.

It’s simple to use. Input a background color and a text color, and the tool will output the contrast ratio:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abee21e9-e3e3-4313-ba22-975e1cbc9fb5/contrast-ratio.png" alt="Image showing how Lea Verou's tool can be used to calculate contrast ratio." /><br>
<em>Lea Verou’s tool determines the contrast ratio between text and its background.</em>

A couple of things to note:

*   The tool supports any CSS color that the browser supports. So, keywords (e.g. white), HEX, RGB, RGBa, HSL and HSLa are all accepted.
*   The tool generates unique URLs as you input valid values. For developers, this feature is perfect for telling designers that their gray on light-gray design is a [bad idea](https://leaverou.github.io/contrast-ratio/#gray-on-lightgray).

While high contrast seems like common sense, plenty of poor contrast can be found in the wild, even on major websites. <a href="https://squareup.com/">Square’s</a> footer fails Level A:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c145400f-d0f3-495e-bb4f-ecd2d54be28d/square.png" alt="The footer on squareup.com" /><br>
<em>Square’s footer has very low contrast.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/750af340-24d8-4093-9ded-fd2d975e61a3/square-ratio.png" alt="The footer text on squareup.com has a contrast ratio of 2:4." /><br>
<em>Square’s footer fails Level A.</em>

Even <a href="https://facebook.com">Facebook</a> is guilty. The links in its header on the desktop fail to meet Level A as well:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/183bd21d-6828-478e-8d4f-0746edde69cd/facebook.png" alt="The header on facebook.com's desktop page" /><br>
<em>The text in Facebook’s header has very low contrast.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37dc798a-d578-4eed-80ab-c2ad824710e9/facebook-ratio.png" alt="The header text on facebook.com has a contrast ratio of 2:4." /><br>
<em>Facebook’s header fails Level A.</em>

To summarize, giving all of your text a contrast ratio of at least 3:1 (and, ideally, 4.5:1 or greater) will make it accessible to people with vision impairments, as well as make it more readable for everyone. Lea Verou’s tool is perfect for calculating contrast ratios and sharing the results with others.

To find out more about conformance levels, the WCAG has a <a href="https://www.w3.org/TR/2006/WD-WCAG20-20060427/appendixB.html">formatted checklist of criteria</a> for each level.

Next, we’ll return to discussing screen readers — specifically, making sure they can understand our websites.</p>

## 4\. Ensure That Screen Readers Know What Your Controls Do

Earlier, we looked at a WebAIM study that shows that 71.8% of screen reader users also use a reader on their mobile device. In this same study, users were asked for the <a href="https://webaim.org/projects/screenreadersurvey4/#problems">most common problems they experience on the web</a>. Third and fourth on this list are the following:

1.  links or buttons that do not make sense,
2.  images with missing or improper descriptions (`alt` text).

(First and second on the list are Flash and CAPTCHAs. Please don’t use either.)

The following snippet shows both of these problems.

<pre><code class="language-markup">
&lt;style&gt;
	button {
		background: url('search.png') no-repeat;
	}
&lt;/style&gt;
&lt;button&gt;&lt;/button&gt;

&lt;img src="ABC123.jpg"&gt;
</code></pre>

The <code>&lt;button&gt;</code> would not make sense to a user on a screen reader; nothing would be read. For the <code>&lt;img&gt;</code>, screen readers would literally read <code>ABC123.jpg</code>, which is not very helpful.

The fixes for these problems are well documented. For the <code>&lt;button&gt;</code>, we can add text to our control and use one of <a href="https://css-tricks.com/css-image-replacement/"><em>many</em> image-replacement techniques</a> to make the text invisible to sighted users. The snippet below shows one of these techniques: applying a large negative <code>text-indent</code> rule.

<pre><code class="language-markup">
&lt;style&gt;
	button {
		background: url('search.png') no-repeat;
		text-indent: -9999px;
	}
&lt;/style&gt;
&lt;button&gt;Search&lt;/button&gt;
</code></pre>

The fix for the <code>&lt;img&gt;</code> is as simple as adding an <code>alt</code> attribute that describes the image.

<pre><code class="language-markup">
&lt;img src="ABC123.jpg" alt="A view of the trees outside my window in Lansing, Michigan"&gt;
</code></pre>

Despite these problems being well known and easy to fix, they continue to be abundant across the web. To prove this, let’s look at some actual websites. I live in the great US state of Michigan, known for its association with the “Big Three” automakers: Ford, GM and Chrysler. Surely, these large companies have produced accessible mobile websites that don’t violate these practices… right?

### Case Study: The Big Three Automakers

Let’s start with GM. <a href="https://m.gm.com">Its mobile website</a> is shown below. The appended text in quotation marks shows what VoiceOver on OS X actually reads when the corresponding element is selected.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adda0315-f2c5-4706-aafd-2db694fe5d27/gm.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adda0315-f2c5-4706-aafd-2db694fe5d27/gm.png" alt="Visual display of m.gm.com's accessibility issues" /></a><br>
<em>GM’s mobile website has accessibility issues. Items in quotation marks are what VoiceOver on OS X actually reads.</em>

As you can see, GM’s website relies heavily on large images that serve as links to additional content. Unfortunately, GM provides no text for these links, so screen readers are limited to the information they can find in the images. GM <em>does</em> provide <code>alt</code> attributes for these images; but, strangely, they are set to the images’ file names. For example, here is the source for the Cadillac image:

<pre><code class="language-markup">
&lt;img title="HomepageBrand_Cadillac_290x170.jpg" height="85"
alt="HomepageBrand_Cadillac_290x170.jpg" class="side-gutters"
src="/content/dam/gm/Global/master/mobilesite/en/home/Homepage/HomepageBrand_Cadillac_290x170.jpg"&gt;
</code></pre>

Thus, when this image is selected, VoiceOver literally reads “Homepagebrand underscore Cadillac underscore two nine zero x one seven zero dot jpeg.”

GM fails our tests, then. Next, let’s try Ford, <a href="https://m.ford.com/">whose mobile website</a> is shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0997fd6c-c688-4f5f-8c1e-2096512b3964/ford.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0997fd6c-c688-4f5f-8c1e-2096512b3964/ford.png" alt="Visual display of m.ford.com's accessibility issues" /></a><br>
<em>Ford’s mobile website also has accessibility issues. Items in quotation marks are what VoiceOver on OS X reads.</em>

Ford has some of the same problems as GM. Its banner is a link that has no text and an image with no <code>alt</code> attribute; so, VoiceOver reads “index.html image.”

Below this, Ford has a fancy 3-D cube effect with images of its vehicles. Unfortunately, this is implemented with a number of <code>&lt;div&gt;</code>s, with <code>background-image</code>s and JavaScript that takes the user away on click. Therefore, screen readers have absolutely no idea what’s going on in this large portion of the screen. VoiceOver on iOS just beeps when you touch this “cube” that takes up half the screen.

Finally, the “links” at the bottom of the screen are not actually links; they are <code>&lt;div&gt;</code>s with <code>onclick</code> attributes that change <code>window.location</code> to navigate the user. Thus, these controls are inaccessible from the keyboard and are confusing for screen readers.

Just when you thought things couldn’t get any worse, let’s look at the last of the Big Three automakers, Chrysler. <a href="https://m.chrysler.com/">Its mobile website</a> is shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43838dd9-b753-4d7b-bd65-a5688d981613/chrysler.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43838dd9-b753-4d7b-bd65-a5688d981613/chrysler.png" alt="Visual display of m.chrysler.com's accessibility issues" /></a><br>
<em>Chrysler’s mobile website, too, has accessibility issues. Items in quotation marks are what VoiceOver on OS X reads.</em>

You can see that almost nothing on Chrysler’s website provides any context for screen readers. We are reminded of the importance of meaningful <code>alt</code> attributes. Here, the one <code>alt</code> attribute that <em>is</em> provided — “This Is the Hero Carousal” — is less than helpful. Worse, all images in the carousel have the exact same <code>alt</code> attributes; so, screen reader users would have no idea that different links are being presented. To add insult to injury, the word “carousel” is spelled incorrectly (“carousal”), causing it to be mispronounced.

These carousel images occupy over half the space on an iPhone screen and are almost certainly the most clicked-on items on the screen. An <code>alt</code> attribute should tell users something about the image they’re seeing, as well as where they will go if they click the link. For example:

<pre><code class="language-markup">
&lt;img src="/path/to/TnC.jpg" alt="Learn more about the J.D. Power 2013 award-winning Chrysler Town &amp; Country"&gt;
</code></pre>

This tells screen reader users what the link is for and what they will see if they select it.

Unfortunately, examples like these are far too common. Even though many accessibility best practices are well documented, they are frequently forgotten — even on big websites and especially on mobile.

Why?

One reason is that the consequences of violating these best practices are not obvious. To sighted touch users, all of these websites operate fine. Secondly, no good way exists to automate your website’s accessibility. The <a href="https://validator.w3.org/">W3C’s validator</a> will warn of missing <code>alt</code> attributes, but it cannot test for more complex scenarios, such as icon buttons and lack of keyboard functionality. It also cannot test whether the <code>alt</code> attributes are actually meaningful.

Because of this, we must trust all web developers to learn and remember to use accessibility practices that have no apparent benefit. As we’ve seen in this case study, frequently they don’t.

But all is not doom and gloom. We've seen that applying a few easy-to-implement best practices can drastically improve the accessibility of your sites, and open them to a new, surprisingly large audience. That building accessible sites builds a better experience for everyone.

But if the W3C validator cannot catch accessibility issues, how do you verify that you're applying these best practices correctly? As it turns out, the best way to test the accessibility of your site is also a great way to gain insight into how disabled users interact with it — by using a screen reader.</p>

## 5\. Test Your Website On An Actual Screen Reader

Most web developers have a slew of browsers and devices to test their websites, yet few know how to use a single screen reader. Unfortunately, this has led most developers to treat accessibility guidelines as some sort of voodoo. They conjecture about what’s best for impaired users without actually testing their theories.

This is a shame, because the best way to discover whether your website is accessible is to try it out as an impaired user would. Personally, I’m not sure why screen readers are shrouded in mystery; they're actually quite easy to use.

If you’re on a Mac, type <code>Command + F5</code> to activate VoiceOver. Navigate around this page with the <code>Tab</code> key and see what’s read. You can also press <code>Control + Option</code> plus the left and right arrow keys to target content that is not in the tab order. There are <a href="https://www.apple.com/voiceover/info/guide/_1131.html">more advanced controls available</a>, but you can get the idea with these basics.

If you’re on Windows, you can download and use <a href="https://www.nvaccess.org/">NVDA</a> for free. <a href="https://www.freedomscientific.com/products/fs/jaws-product-page.asp">JAWS</a> is the most popular paid reader; it has a demo mode that you can try for free.

Mobile devices are a tad different because there is no keyboard by default. Therefore, using a screen reader forces you to reconsider how you interact with your device. Let’s explore this by looking at the screen readers built into iOS and Android — VoiceOver and TalkBack, respectively.</p>

### Using VoiceOver on iOS

VoiceOver is iOS’ primary accessibility aid for all applications, not just the Web. Because most users don’t use it, VoiceOver is disabled by default. To enable it, go to <code>Settings → General → Accessibility → VoiceOver</code>. You’ll see the screen shown below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78969b60-c780-48a0-a47a-0b1341f7fa85/voiceover.png" alt="VoiceOver’s settings screen" /><br>
<em>The settings screen for VoiceOver on iOS</em>

Be warned — once you turn it on, VoiceOver will fundamentally change the way you interact with the phone. Therefore, you <em>must</em> learn the basics; otherwise, you won’t be able to turn VoiceOver back off.

Once VoiceOver is on, a single tap on the screen will select an item but will not activate it. For example, if you tap on the Safari icon, VoiceOver will read “Safari” but will not launch the application. After a selection, a double tap is needed to actually start the application. This makes sense if you consider the perspective of someone who cannot see the icon. They would need confirmation that they’ve selected the correct item before activating it.

The other important difference with VoiceOver is that you have to use three fingers to scroll. Why? Because while in VoiceOver mode, iOS listens for one-finger “flick” gestures in all four directions:

*   “Up” Move to previous item based on rotor setting
*   “Down” Move to next item based on rotor setting
*   “Right” Move to previous item
*   “Left” Move to next item

What’s this “rotor”? We’ll get to that in a moment. First, try flicking left and right on the screen to move between available items. These flicks let vision-impaired users discover what’s on the screen without having to tap around.

Things get more interesting with VoiceOver’s rotor, a means of configuring how to navigate between items on the screen.

To activate the rotor, rotate two fingers on the screen as if you were turning a dial. The rotor and its default options are shown below.

Submitting with the “Enter” key is known as an implicit submission, and it is supported by all browsers — even mobile ones. There are only two requirements to making implicit submission work.

1.  All `<input>` elements need to be in a `<form>`.
2.  If the form has more than one element — `<input>`, `<select>` or `<textarea>` — then the `<form>` must have a “Submit” button.

Our sample form already has a “Submit” button (the default <code>type</code> of <code>&lt;button&gt;</code> is <code>submit</code>). Therefore, we only need to add a <code>&lt;form&gt;</code>.

<pre><code class="language-markup">
&lt;form method="POST"&gt;
	&lt;label for="username"&gt;Username:&lt;/label&gt;
	&lt;input type="text" id="username" name="username"&gt;

	&lt;label for="password"&gt;Password:&lt;/label&gt;
	&lt;input type="password" id="password" name="password"&gt;

	&lt;button&gt;Submit&lt;/button&gt;
&lt;/form&gt;
&lt;script&gt;
	document.querySelector( "button" )
		.addEventListener( "click", function( event ) {
			// Prevent the default form submission
			event.preventDefault();

		// Send AJAX request
	});
&lt;/script&gt;
</code></pre>

A couple of things to note:

*   When implicit submission occurs, the browser performs a click on the `<form>`’s “Submit” button. Therefore, listening for `click` events on the “Submit” button to perform submit actions is still safe. You could, alternatively, listen for a `submit` event on the `<form>`.
*   Even though JavaScript will intercept the form’s submission, `method="POST"` is still explicitly declared. In case JavaScript fails (because of unsupported browsers, network issues, etc.), we don’t want the browser to submit a `GET` request that would place the user-supplied user name and password in the query string.

Enabling implicit submission saves mobile users some clicking. The image below shows two <code>&lt;input&gt;</code> elements, one in a <code>&lt;form&gt;</code> and one not. Note that the <code>&lt;form&gt;</code>-based example can be submitted while the <code>&lt;input&gt;</code> has focus — no need for additional taps or hunting for a “Submit” button.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f3937c-5bc1-42a3-8026-2367d1fa113e/enter-key.png" alt="This image shows two input elements, one in a form and one not. The one in the form has a Go button that submits the form, and the one not in the form has a Return button that does not submit the form." /><br>
<em>Implicit form submission works only with true form elements.</em>

This concludes our look at building accessible forms. As with keyboard access, these guidelines are far from comprehensive, but they address some of the most common problems with forms today. For a more complete list of best practices, check out the W3C’s <a href="https://www.w3.org/WAI/WCAG20/quickref/#minimize-error">guidelines for collecting input from users</a>.

Next, we’ll look at a problem that most smartphone owners have experienced at some point: low contrast.</p>

## 3\. Provide Plenty Of Contrast

If you’ve ever used your phone outdoors, especially in harsh sunlight, then you’ve struggled to read the screen at some point. This is not unlike what some users with vision disabilities experience all of the time.

When designing any website, remember that most users will not be visiting it indoors on a high-end monitor like yours. This is especially critical for mobile websites because of the wide variety of contexts in which people use their phone.

How do you make your website adapt to these contexts? Unlike more subjective aspects, contrast ratio can be calculated, and the W3C puts numeric guidelines for these ratios in its “<a href="https://www.w3.org/TR/WCAG/">Web Content Accessibility Guidelines</a>” (WCAG), a series of recommendations for making web content more accessible to individuals with disabilities.

The WCAG defines three levels of conformance: Level A, Level AA and Level AAA. <a href="https://www.w3.org/TR/WAI-WEBCONTENT/#wc-priority-1">According to the specification</a>, for a website to conform, Level A requirements <strong>must</strong> be met, Level AA requirements <strong>should</strong> be met and Level AAA requirements <strong>may</strong> be met.

The Level A contrast ratio is set at 3:1; Level AA is set at 4.5:1; and Level AAA is set at 7:1. As a point of reference, the <a href="https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html">specification recommends</a> a contrast ratio of 4.5:1 for users with 20/40 vision, which is common among elderly people.

This means that we should make our contrast ratios at least 3:1 and, ideally, 4.5:1 or greater. But, how exactly do we calculate this?

### Calculating Contrast Ratio

Luckily, <a href="https://lea.verou.me/">Lea Verou</a> has <a href="https://leaverou.github.io/contrast-ratio/">created a tool to calculate contrast ratio</a> easily.

It’s simple to use. Input a background color and a text color, and the tool will output the contrast ratio:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abee21e9-e3e3-4313-ba22-975e1cbc9fb5/contrast-ratio.png" alt="Image showing how Lea Verou's tool can be used to calculate contrast ratio." /><br>
<em>Lea Verou’s tool determines the contrast ratio between text and its background.</em>

A couple of things to note:

*   The tool supports any CSS color that the browser supports. So, keywords (e.g. white), HEX, RGB, RGBa, HSL and HSLa are all accepted.
*   The tool generates unique URLs as you input valid values. For developers, this feature is perfect for telling designers that their gray on light-gray design is a [bad idea](https://leaverou.github.io/contrast-ratio/#gray-on-lightgray).

While high contrast seems like common sense, plenty of poor contrast can be found in the wild, even on major websites. <a href="https://squareup.com/">Square’s</a> footer fails Level A:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c145400f-d0f3-495e-bb4f-ecd2d54be28d/square.png" alt="The footer on squareup.com" /><br>
<em>Square’s footer has very low contrast.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/750af340-24d8-4093-9ded-fd2d975e61a3/square-ratio.png" alt="The footer text on squareup.com has a contrast ratio of 2:4." /><br>
<em>Square’s footer fails Level A.</em>

Even <a href="https://facebook.com">Facebook</a> is guilty. The links in its header on the desktop fail to meet Level A as well:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/183bd21d-6828-478e-8d4f-0746edde69cd/facebook.png" alt="The header on facebook.com's desktop page" /><br>
<em>The text in Facebook’s header has very low contrast.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37dc798a-d578-4eed-80ab-c2ad824710e9/facebook-ratio.png" alt="The header text on facebook.com has a contrast ratio of 2:4." /><br>
<em>Facebook’s header fails Level A.</em>

To summarize, giving all of your text a contrast ratio of at least 3:1 (and, ideally, 4.5:1 or greater) will make it accessible to people with vision impairments, as well as make it more readable for everyone. Lea Verou’s tool is perfect for calculating contrast ratios and sharing the results with others.

To find out more about conformance levels, the WCAG has a <a href="https://www.w3.org/TR/2006/WD-WCAG20-20060427/appendixB.html">formatted checklist of criteria</a> for each level.

Next, we’ll return to discussing screen readers — specifically, making sure they can understand our websites.</p>

## 4\. Ensure That Screen Readers Know What Your Controls Do

Earlier, we looked at a WebAIM study that shows that 71.8% of screen reader users also use a reader on their mobile device. In this same study, users were asked for the <a href="https://webaim.org/projects/screenreadersurvey4/#problems">most common problems they experience on the web</a>. Third and fourth on this list are the following:

1.  links or buttons that do not make sense,
2.  images with missing or improper descriptions (`alt` text).

(First and second on the list are Flash and CAPTCHAs. Please don’t use either.)

The following snippet shows both of these problems.

<pre><code class="language-markup">
&lt;style&gt;
	button {
		background: url('search.png') no-repeat;
	}
&lt;/style&gt;
&lt;button&gt;&lt;/button&gt;

&lt;img src="ABC123.jpg"&gt;
</code></pre>

The <code>&lt;button&gt;</code> would not make sense to a user on a screen reader; nothing would be read. For the <code>&lt;img&gt;</code>, screen readers would literally read <code>ABC123.jpg</code>, which is not very helpful.

The fixes for these problems are well documented. For the <code>&lt;button&gt;</code>, we can add text to our control and use one of <a href="https://css-tricks.com/css-image-replacement/"><em>many</em> image-replacement techniques</a> to make the text invisible to sighted users. The snippet below shows one of these techniques: applying a large negative <code>text-indent</code> rule.

<pre><code class="language-markup">
&lt;style&gt;
	button {
		background: url('search.png') no-repeat;
		text-indent: -9999px;
	}
&lt;/style&gt;
&lt;button&gt;Search&lt;/button&gt;
</code></pre>

The fix for the <code>&lt;img&gt;</code> is as simple as adding an <code>alt</code> attribute that describes the image.

<pre><code class="language-markup">
&lt;img src="ABC123.jpg" alt="A view of the trees outside my window in Lansing, Michigan"&gt;
</code></pre>

Despite these problems being well known and easy to fix, they continue to be abundant across the web. To prove this, let’s look at some actual websites. I live in the great US state of Michigan, known for its association with the “Big Three” automakers: Ford, GM and Chrysler. Surely, these large companies have produced accessible mobile websites that don’t violate these practices… right?

### Case Study: The Big Three Automakers

Let’s start with GM. <a href="https://m.gm.com">Its mobile website</a> is shown below. The appended text in quotation marks shows what VoiceOver on OS X actually reads when the corresponding element is selected.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adda0315-f2c5-4706-aafd-2db694fe5d27/gm.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adda0315-f2c5-4706-aafd-2db694fe5d27/gm.png" alt="Visual display of m.gm.com's accessibility issues" /></a><br>
<em>GM’s mobile website has accessibility issues. Items in quotation marks are what VoiceOver on OS X actually reads.</em>

As you can see, GM’s website relies heavily on large images that serve as links to additional content. Unfortunately, GM provides no text for these links, so screen readers are limited to the information they can find in the images. GM <em>does</em> provide <code>alt</code> attributes for these images; but, strangely, they are set to the images’ file names. For example, here is the source for the Cadillac image:

<pre><code class="language-markup">
&lt;img title="HomepageBrand_Cadillac_290x170.jpg" height="85"
alt="HomepageBrand_Cadillac_290x170.jpg" class="side-gutters"
src="/content/dam/gm/Global/master/mobilesite/en/home/Homepage/HomepageBrand_Cadillac_290x170.jpg"&gt;
</code></pre>

Thus, when this image is selected, VoiceOver literally reads “Homepagebrand underscore Cadillac underscore two nine zero x one seven zero dot jpeg.”

GM fails our tests, then. Next, let’s try Ford, <a href="https://m.ford.com/">whose mobile website</a> is shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0997fd6c-c688-4f5f-8c1e-2096512b3964/ford.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0997fd6c-c688-4f5f-8c1e-2096512b3964/ford.png" alt="Visual display of m.ford.com's accessibility issues" /></a><br>
<em>Ford’s mobile website also has accessibility issues. Items in quotation marks are what VoiceOver on OS X reads.</em>

Ford has some of the same problems as GM. Its banner is a link that has no text and an image with no <code>alt</code> attribute; so, VoiceOver reads “index.html image.”

Below this, Ford has a fancy 3-D cube effect with images of its vehicles. Unfortunately, this is implemented with a number of <code>&lt;div&gt;</code>s, with <code>background-image</code>s and JavaScript that takes the user away on click. Therefore, screen readers have absolutely no idea what’s going on in this large portion of the screen. VoiceOver on iOS just beeps when you touch this “cube” that takes up half the screen.

Finally, the “links” at the bottom of the screen are not actually links; they are <code>&lt;div&gt;</code>s with <code>onclick</code> attributes that change <code>window.location</code> to navigate the user. Thus, these controls are inaccessible from the keyboard and are confusing for screen readers.

Just when you thought things couldn’t get any worse, let’s look at the last of the Big Three automakers, Chrysler. <a href="https://m.chrysler.com/">Its mobile website</a> is shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43838dd9-b753-4d7b-bd65-a5688d981613/chrysler.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43838dd9-b753-4d7b-bd65-a5688d981613/chrysler.png" alt="Visual display of m.chrysler.com's accessibility issues" /></a><br>
<em>Chrysler’s mobile website, too, has accessibility issues. Items in quotation marks are what VoiceOver on OS X reads.</em>

You can see that almost nothing on Chrysler’s website provides any context for screen readers. We are reminded of the importance of meaningful <code>alt</code> attributes. Here, the one <code>alt</code> attribute that <em>is</em> provided — “This Is the Hero Carousal” — is less than helpful. Worse, all images in the carousel have the exact same <code>alt</code> attributes; so, screen reader users would have no idea that different links are being presented. To add insult to injury, the word “carousel” is spelled incorrectly (“carousal”), causing it to be mispronounced.

These carousel images occupy over half the space on an iPhone screen and are almost certainly the most clicked-on items on the screen. An <code>alt</code> attribute should tell users something about the image they’re seeing, as well as where they will go if they click the link. For example:

<pre><code class="language-markup">
&lt;img src="/path/to/TnC.jpg" alt="Learn more about the J.D. Power 2013 award-winning Chrysler Town &amp; Country"&gt;
</code></pre>

This tells screen reader users what the link is for and what they will see if they select it.

Unfortunately, examples like these are far too common. Even though many accessibility best practices are well documented, they are frequently forgotten — even on big websites and especially on mobile.

Why?

One reason is that the consequences of violating these best practices are not obvious. To sighted touch users, all of these websites operate fine. Secondly, no good way exists to automate your website’s accessibility. The <a href="https://validator.w3.org/">W3C’s validator</a> will warn of missing <code>alt</code> attributes, but it cannot test for more complex scenarios, such as icon buttons and lack of keyboard functionality. It also cannot test whether the <code>alt</code> attributes are actually meaningful.

Because of this, we must trust all web developers to learn and remember to use accessibility practices that have no apparent benefit. As we’ve seen in this case study, frequently they don’t.

But all is not doom and gloom. We've seen that applying a few easy-to-implement best practices can drastically improve the accessibility of your sites, and open them to a new, surprisingly large audience. That building accessible sites builds a better experience for everyone.

But if the W3C validator cannot catch accessibility issues, how do you verify that you're applying these best practices correctly? As it turns out, the best way to test the accessibility of your site is also a great way to gain insight into how disabled users interact with it — by using a screen reader.</p>

## 5\. Test Your Website On An Actual Screen Reader

Most web developers have a slew of browsers and devices to test their websites, yet few know how to use a single screen reader. Unfortunately, this has led most developers to treat accessibility guidelines as some sort of voodoo. They conjecture about what’s best for impaired users without actually testing their theories.

This is a shame, because the best way to discover whether your website is accessible is to try it out as an impaired user would. Personally, I’m not sure why screen readers are shrouded in mystery; they're actually quite easy to use.

If you’re on a Mac, type <code>Command + F5</code> to activate VoiceOver. Navigate around this page with the <code>Tab</code> key and see what’s read. You can also press <code>Control + Option</code> plus the left and right arrow keys to target content that is not in the tab order. There are <a href="https://www.apple.com/voiceover/info/guide/_1131.html">more advanced controls available</a>, but you can get the idea with these basics.

If you’re on Windows, you can download and use <a href="https://www.nvaccess.org/">NVDA</a> for free. <a href="https://www.freedomscientific.com/products/fs/jaws-product-page.asp">JAWS</a> is the most popular paid reader; it has a demo mode that you can try for free.

Mobile devices are a tad different because there is no keyboard by default. Therefore, using a screen reader forces you to reconsider how you interact with your device. Let’s explore this by looking at the screen readers built into iOS and Android — VoiceOver and TalkBack, respectively.</p>

### Using VoiceOver on iOS

VoiceOver is iOS’ primary accessibility aid for all applications, not just the Web. Because most users don’t use it, VoiceOver is disabled by default. To enable it, go to <code>Settings → General → Accessibility → VoiceOver</code>. You’ll see the screen shown below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78969b60-c780-48a0-a47a-0b1341f7fa85/voiceover.png" alt="VoiceOver’s settings screen" /><br>
<em>The settings screen for VoiceOver on iOS</em>

Be warned — once you turn it on, VoiceOver will fundamentally change the way you interact with the phone. Therefore, you <em>must</em> learn the basics; otherwise, you won’t be able to turn VoiceOver back off.

Once VoiceOver is on, a single tap on the screen will select an item but will not activate it. For example, if you tap on the Safari icon, VoiceOver will read “Safari” but will not launch the application. After a selection, a double tap is needed to actually start the application. This makes sense if you consider the perspective of someone who cannot see the icon. They would need confirmation that they’ve selected the correct item before activating it.

The other important difference with VoiceOver is that you have to use three fingers to scroll. Why? Because while in VoiceOver mode, iOS listens for one-finger “flick” gestures in all four directions:

*   “Up” Move to previous item based on rotor setting
*   “Down” Move to next item based on rotor setting
*   “Right” Move to previous item
*   “Left” Move to next item

What’s this “rotor”? We’ll get to that in a moment. First, try flicking left and right on the screen to move between available items. These flicks let vision-impaired users discover what’s on the screen without having to tap around.

Things get more interesting with VoiceOver’s rotor, a means of configuring how to navigate between items on the screen.

To activate the rotor, rotate two fingers on the screen as if you were turning a dial. The rotor and its default options are shown below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4de9b46-7777-4b28-bf4b-bc13474926c3/rotor.png" alt="VoiceOver's rotor with the various settings: words, lines, speech rate, containers, headings, links, form controls, and characters - annotated." /><br>
<em>The rotor control in VoiceOver for iOS</em>

By setting the rotor, you can change how up and down flicks navigate the page. For instance, if the rotor is set to “Links,” then up and down flicks will cycle between links on the page and nothing else. In this sense, the rotor acts as a filter, enabling users to sift through the type of content that they’re interested in.

The rotor shows the importance of semantic markup. If your links are not actually <code>&lt;a&gt;</code> tags, then they won’t show up in the rotor setting for “Links.” If your form’s controls are not actual form elements, then they won’t show up in the rotor setting for “Form Controls.”

As you can see, using a screen reader forces you to fundamentally change how you use and approach the web on a mobile device. Play around with any websites you maintain to see how well you can navigate and accomplish tasks. As an added challenge, once you’re familiar with VoiceOver, try closing your eyes and see what you can get done.</p>

### Using TalkBack on Android

Like VoiceOver, TalkBack is an accessibility service for vision-impaired users that is native to Android devices. Because most people do not need the service, it is also disabled by default. To enable it, go to <code>Settings → Accessibility → TalkBack</code> and tap the switch shown below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8cd80e0-f0ee-4205-89fc-337210fbff03/talkback.png" alt="TalkBack's settings page" /><br>
<em>The settings page for TalkBack on Android</em>

Again, be warned. Once TalkBack is activated, you’ll at least need to know the basic controls to turn it off.

TalkBack’s controls are extremely similar to VoiceOver’s. One tap selects an item, and a double tap activates it. Scrolling with TalkBack requires two fingers (recall that VoiceOver requires three), and TalkBack listens for the same flick actions to move between items on the page.

While TalkBack has nothing comparable to VoiceOver’s rotor, it does support a <a href="https://support.google.com/nexus/answer/2926960?hl=en">number of additional gestures</a> to customize the navigation.</p>

## Wrapping Up

In this article, we’ve discussed a number of best practices to improve the accessibility of your websites. How do you apply this information to your existing or new websites? Here are a few action items:

*   Keyboard
    *   Make sure that all tasks can be performed using only the keyboard.
    *   Use semantic elements — `<button>` for buttons and `<a>` for links.
    *   If you’re having trouble making complex widgets keyboard-friendly, consider using a framework.
*   Forms
    *   Use the actual `<form>` element.
    *   Associate all form elements (`<input>`, `<select>` and `<textarea>`) with a `<label>`.
    *   Make sure the “Enter” key can be used to submit the form.
*   Contrast
    *   Ensure that all text has a contrast ratio of at least 3.0, using Lea Verou’s [Contrast Ratio](https://leaverou.github.io/contrast-ratio/). Ideally, all text should meet this criterion, but focus on the main content first.
*   Images
    *   Include `alt` attributes that describe the images.
*   Links and buttons
    *   Always give these controls readable content. If the content should not be shown to sighted users, then use an image-replacement technique to hide it.

While this list is not comprehensive, it does provide a number of practices that are easy to implement and that address the most common problems affecting disabled users. Furthermore, we’ve seen that adhering to these guidelines benefits everyone, not just the disabled.

Finally, the best way to test your website is on an actual screen reader. By taking mere minutes to learn some commands, you will gain insight into how a good portion of the population interacts on the web.</p>

### Resources

*   “[Web Content Accessibility Guidelines 2.0](https://www.w3.org/TR/WCAG/),” W3C If you’re looking for a more comprehensive checklist than what’s provided in the conclusion above, this is it.
*   “[Shared Web Experiences: Barriers Common to Mobile Device Users and People With Disabilities](https://www.w3.org/WAI/mobile/experiences),” W3C Web Accessibility Initiative This page describes the issues that people with disabilities encounter on the Web and how they are addressed by the W3C’s guidelines and specifications.
*   “[Talk To Me](https://jzaefferer.github.io/talk-to-me/),” Jörn Zaefferer These slides are from Zaefferer’s 2013 talk on making websites accessible.
*   [Contrast Rebellion](https://contrastrebellion.com/) An amusing look at why contrast is important on the web.
*   “[VoiceOver Getting Started](https://help.apple.com/voiceover/info/guide/10.8/English.lproj/),” Apple The official guide to getting started with VoiceOver on OS X.
*   [The Accessibility Project](https://a11yproject.com/) A nice collection of accessibility tips.
*   “[You Can’t Create a Button](https://www.nczonline.net/blog/2013/01/29/you-cant-create-a-button/),” Nicholas Zakas Zakas explains when to use `<a>` and `<button>` elements.

{{< signature "al, il" >}}

