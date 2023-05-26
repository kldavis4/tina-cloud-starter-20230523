---
title: MJML – How To Make Responsive HTML Email Coding Easy
slug: making-responsive-html-email-coding-easy-with-mjml
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d4169fd-75d4-48ec-bb5c-64865c3d7ccc/mjml-vs-html-preview-opt.png
date: 2017-01-24T19:25:49.000Z
author: nicolasgarnier
description: >-
  Email is one of the best ways to engage with your users, especially during the
  holiday season. However, if you want to stand out, no matter how beautiful
  your emails are, you need to make sure they render correctly in your reader's
  inbox, regardless of what email client they're using. **Creating responsive
  email is not an easy task**, and there are various reasons for that.

  First, there is no standard in the way email clients render HTML. This is true
  for email clients from different companies, such as Outlook and Apple Mail,
  but not only. Even different versions of Outlook, such as Outlook 2003,
  Outlook 2013 and Outlook.com, render HTML differently.
categories:
  - Coding
  - CSS
  - Newsletters
  - HTML
  - Emails
---
First, there is no standard in the way email clients render HTML. This is true for email clients from different companies, such as Outlook and Apple Mail, but not only. Even different versions of Outlook, such as Outlook 2003, Outlook 2013 and Outlook.com, render HTML differently.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Design And Build Email Newsletters Without Losing Your Mind](https://www.smashingmagazine.com/2010/01/design-and-build-an-email-newsletter-without-losing-your-mind/)
*   [18 Email Templates For Web Designers And Developers](https://www.smashingmagazine.com/2013/06/email-templates-web-designers-developers-pdf-odt-txt/)
*   [How To Improve Your Email Workflow With Modular Design](https://www.smashingmagazine.com/2014/08/improve-your-email-workflow-with-modular-design/)

Then, while email clients render HTML, many of them have very limited support of it. Some email clients will just strip the head of your HTML file, including media queries, which is why <strong>inline styles are heavily recommended</strong>. On a good note, this is moving in the right direction with the <a href="https://www.mailjet.com/blog/gmail-responsive-email-design">Gmail update</a>.

{{% feature-panel %}}

Now, there are a few techniques out there to help email developers. You might be familiar with some of them, such as the <a href="https://litmus.com/blog/understanding-responsive-and-hybrid-email-design"> hybrid approach</a>, the <a href="https://getflywheel.com/layout/design-emails-for-mobile/">mobile-first approach</a> or even the <a href="https://medium.freecodecamp.com/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848#.86y5xm2q7">Fab Four technique</a> by <a href="https://twitter.com/hteumeuleu">HTeuMeuLeu</a>. But because of the reasons stated earlier, and especially the lack of a standard, none of these techniques will enable you to tame all email clients at once.</p>

## Abstracting Away The Complexity Of Responsive Email With MJML

MJML is an open-source framework that abstracts away the complexity of responsive email. The idea behind it is pretty simple. Just as jQuery normalizes the DOM and abstracts low-level interactions and animations, MJML abstracts the low-level hacks for responsive emails with an easy syntax. <strong>MJML is responsive by design</strong>. This means you can forget about nested tables and conditional comments and, more generally, about making your email responsive. MJML does it for you.

Leveraging a semantic syntax and high-level components such as the <a href="https://mjml.io/documentation/#mjml-carousel">carousel</a> (yes, you can display an interactive image gallery within an email!), MJML is really easy to learn for anyone. Responsive emails are no longer only accessible to a handful of experts anymore.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36f7724f-1b65-473c-bf84-c54c81882781/mj-carousel-gmail-preview-opt.gif"><img style="filter: url('#toggleGifsIndicatorFilter');" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36f7724f-1b65-473c-bf84-c54c81882781/mj-carousel-gmail-preview-opt.gif" alt="Example of an MJML component: carousel." width="695" height="435" /></a><figcaption>Example of an MJML component: carousel</figcaption></figure>

Being easy to use doesn't mean that MJML is not powerful. It just enables experts to streamline their development workflow, while still giving them the flexibility they need with lower-level components such as <a href="https://mjml.io/documentation/#mjml-table">tables</a>.

For instance, <a href="https://reallygoodemails.com/wp-content/uploads/discover-the-latest-trends.html">our example email</a> was coded in <a href="https://codepen.io/mjml/pen/woeNwp">788 lines of HTML</a> and reproduced in <a href="https://mjml.io/try-it-live/templates/thrive_email">fewer than 240 lines of MJML</a>.</p>

## The Approach

MJML is built in <a href="https://facebook.github.io/react/">React</a>, a JavaScript library developed and maintained by Facebook, and it leverages the power of React's components. The component names are semantic, starting with <code>mj-</code>, so that they are straightforward as well as easy to recognize and understand: <code>mj-text</code>, <code>mj-image</code>, <code>mj-button</code>, etc.

MJML will transpile to responsive HTML, following a mix of the mobile-first and hybrid coding approaches. Going mobile-first enables you to <strong>make sure that the most readable version is displayed by default</strong> in email clients that do not change the layout according to the device used.

For example, in Outlook.com, the mobile version will be displayed on both desktop and mobile (which is far more readable than a desktop version being displayed on mobile). The hybrid approach then enables the layout to change according to the device's size wherever possible, using a mix of fallbacks, conditional comments, nested tables and media queries to target as many clients as possible. The layout degrades nicely, with multi-column layouts on desktop turning into single-column layouts on mobile.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ea2599-d454-401d-a7a3-5a90588101f1/desktop-view2-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1ea2599-d454-401d-a7a3-5a90588101f1/desktop-view2-preview-opt.png" alt="2-column layout - desktop view." width="600" height="630" /></a><figcaption>Two-column layout, desktop view</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5be4bf1-972e-4a5e-9bdf-bc3b935aa3c9/mobile-view2-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5be4bf1-972e-4a5e-9bdf-bc3b935aa3c9/mobile-view2-preview-opt.png" alt="2-column layout - mobile view." width="498" height="1499" /></a><figcaption>Two-column layout, mobile view</figcaption></figure>

## Coding In MJML

Before we start the tutorial, let's get ready to code in MJML. We have different ways to use MJML, such as <a href="https://mjml.io/download">running it locally</a> or using the <a href="https://mjml.io/try-it-live">online editor</a>. By choosing the online editor, you'll be able to start immediately, but running it locally enables you to use MJML with your favorite code editor (with plugins for <a href="https://atom.io/users/mjmlio">Atom</a>, <a href="https://packagecontrol.io/packages/MJML-syntax">Sublime Text</a> and <a href="https://github.com/amadeus/vim-mjml">Vim</a>), task runners such as <a href="https://github.com/mjmlio/gulp-mjml">gulp-mjml</a> and <a href="https://github.com/smbeiragh/grunt-mjml">grunt-mjml</a> and <a href="https://mjml.io/community">a lot more</a>.

For this tutorial, the <a href="https://mjml.io/try-it-live">online editor</a> is recommended because it doesn't require any setup.

If you still want to use it locally, open your terminal and run <code>npm install mjml -g</code> (requires to have <a href="https://nodejs.org/en/">Node.js and npm</a> installed).

Once MJML is installed, create a file named <code>example.mjml</code> (or any name you like) with some MJML and run <code>mjml -r example.mjml</code> in your terminal (make sure to be in the same folder as the file you're rendering). It will render your MJML file in a file named <code>example.html</code>, with the responsive HTML inside. You can find all available options for the command line in <a href="https://mjml.io/documentation/#command-line-interface">the documentation</a>.</p>

## Creating Your First Newsletter With MJML

Now that you're all set up, we can start creating a responsive newsletter together. To find inspiration, one of the best places around is <a href="https://reallygoodemails.com/">ReallyGoodEmails</a>. I found a <a href="https://reallygoodemails.com/wp-content/uploads/discover-the-latest-trends.html">great example of a newsletter</a> by <a href="https://thrivemarket.com/">Thrive Market</a>. Let's recreate it with MJML!

(Brand names, logos and trademarks used herein remain the property of their respective owners, and their use does not imply any endorsement by or affiliation with Thrive Market.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9e99c64-6db7-4fae-923a-eb4c8a1f2f66/thrive-market-newsletter-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b054cfbc-f52b-4ae1-9f4c-6e0c9082f6d8/thrive-market-newsletter-cropped-preview-opt.png" alt="Thrive Market newsletter" width="639" height="2714" /></a><figcaption>Thrive Market newsletter</figcaption></figure>

First, here is what the <a href="https://mjml.io/documentation/#overview">basic layout</a> of an MJML document looks like:

<pre>		<code class="language-markup">
&lt;mjml&gt;
	&lt;mj-head&gt;
		&lt;!-- Head components go here: https://mjml.io/documentation/#standard-head-components --&gt;
	&lt;/mj-head&gt;

	&lt;!-- All of the content of our email will go in mj-body --&gt;
	&lt;mj-body&gt;
		&lt;!-- mj-container defines the default styling of our email, including the default width, set to 600px but overwritable --&gt;
		&lt;mj-container&gt;
			&lt;!-- Body components go here (https://mjml.io/documentation/#standard-body-components) --&gt;
		&lt;/mj-container&gt;
	&lt;/mj-body&gt;
&lt;/mjml&gt;
		</code>
</pre>

## Streamlining The Style

While inlining is the norm in HTML to ensure responsiveness, MJML also allows you to create custom MJML classes and MJML styles, which will then automatically be inlined from the <a href="https://mjml.io/documentation/#standard-head-components">head of your MJML file</a>. In MJML, styles come as component attributes.</p>

<pre><code class="language-markup">
&lt;mj-text font-size="20px" color="#F45E43" font-family="helvetica"&gt;
	Hello World
&lt;/mj-text&gt;</code></pre>

To start, we'll set a default <code>sans-serif</code> font family for text components, because <code>sans-serif</code> is used for most text here. Then, we'll create classes for elements used repeatedly, so that we don't have to manually set styles over and over again. We could have created more custom classes and styles, but the most useful styles will be for:

*   buttons,
*   image descriptions,
*   text below the six icons in the footer.

Here, we'll be leveraging <a href="https://mjml.io/documentation/#standard-head-components">head components</a> in three ways:

*   Set a default `padding` of `0` for every component, using `<mj-all />`. This default `padding` can be overridden by manually specifying a `padding` directly on the components we are using.
*   Override the default font family of `<mj-text>`, using `<mj-text />` in the head. Each time we use `<mj-text>`, the default font family will be `sans-serif`. We can still manually override this new default font by specifying a new one directly on the component.
*   Create classes using `<mj-class />` and, more specifically, using the following mj-classes:
    *   `pill` This is to design a nice button. Attributes worth noting are the `background-color` set to `transparent` and the `inner-padding`, used to size the button as we want.
    *   `desc` This is to style the descriptions of the images in the two-column layout.
    *   `ico` This is to style the text below the six icons just before the footer.</p>

<pre><code class="language-markup">
&lt;mj-head&gt;
  	&lt;mj-title&gt;Discover the latest trends&lt;/mj-title&gt;
    &lt;mj-attributes&gt;
	    &lt;mj-all padding="0" /&gt;
	    &lt;mj-text font-family="sans-serif" color="#8e8b85" /&gt;
	    &lt;mj-class name="pill" font-weight="700" color="#d5ad4b" border-radius="50" border="2px solid #d5ad4b" font-size="16px" line-height="16px" padding="8 20 20 20" inner-padding="10 75 10 75" background-color="transparent" /&gt;
	    &lt;mj-class name="desc" font-family="Georgia" font-size="20px" color="#45495d" padding="25 5 10 10" /&gt;
	    &lt;mj-class name="ico" font-family="Helvetica" font-size="14px" align="center" padding="0 0"/&gt;
    &lt;/mj-attributes&gt;
&lt;/mj-head&gt;
</code></pre>

(As you may have noticed, we have omitted the units on some attributes, such as <code>padding</code>. If you do so, MJML will output the attributes with <code>px</code> by default.)

## Adding Content

Now that the styles are defined in the <code>head</code> (you can see <a href="https://mjml.io/try-it-live/templates/thrive_head">here</a> what your code should look like now), let's start adding content to our email! MJML layouts are based on <a href="https://mjml.io/documentation/mjml-section"><code>&lt;mj-section&gt;</code></a> to create rows and <a href="https://mjml.io/documentation/#mjml-column"><code>&lt;mj-column&gt;</code></a> to create columns inside rows, which is very practical for email design. Note that, except for high-level components such as <a href="https://mjml.io/documentation/#mjml-hero"><code>&lt;mj-hero&gt;</code></a> and <a href="https://mjml.io/documentation/#mjml-navbar"><code>&lt;mj-navbar&gt;</code></a>, content should always be wrapped in a <a href="https://mjml.io/documentation/#mjml-column"><code>&lt;mj-column&gt;</code></a>, which itself should go in a <a href="https://mjml.io/documentation/#mjml-section"><code>&lt;mj-section&gt;</code></a>, even when there is only one column in a section.

Let's see this with two examples, the preheader and the header of the email.</p>

## Preheader

There's nothing very fancy here. We're just creating a text preheader using the <a href="https://mjml.io/documentation/mjml-text"><code>&lt;mj-text&gt;</code></a> component, wrapped in a column, and giving it some MJML styles.

Hack: <code>&lt;mj-text&gt;</code> enables you to use HTML directly inside MJML, granting you full control over the content and allowing you to use the <code>&lt;span&gt;</code> and <code>&lt;a&gt;</code> tags you're used to, for example.

<pre>		<code class="language-markup">
&lt;mj-section padding="0" background-color="#eeebe7"&gt;
	&lt;mj-column&gt;
		&lt;mj-text padding="0 2" align="center" font-size="10px"&gt;
			The latest tips, trends, recipes, and more
		&lt;/mj-text&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
		</code>
</pre>

## Header

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e05e1ff-c9c1-419d-8ca0-7a8fa0ac7e0d/header-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e05e1ff-c9c1-419d-8ca0-7a8fa0ac7e0d/header-preview-opt.png" alt="Header of the email" width="645" height="306" /></a><figcaption>Header of the email</figcaption></figure>

### Three-Column Layout for Blog, Logo and Referral Link

The header is a bit fancier but very easy to achieve with MJML. All we have to do is create a section that we'll split into three equal columns (because columns are equal, we don't even have to manually set the width). We'll use images as in the original email, leveraging the explicit component <a href="https://mjml.io/documentation/#mjml-image"><code>&lt;mj-image&gt;</code></a>, which comes with the common attributes you would expect, including <code>src</code>, <code>padding</code> and <code>border</code>.

By default, columns will stack in the mobile version of our email. Here, because we want those three columns to stay side by side even on mobile, we'll wrap them in an <a href="https://mjml.io/documentation/#mjml-group"><code>&lt;mj-group&gt;</code></a> component, which will prevent the columns from stacking.

Hack: As noted in the documentation, due to a bug in iOS, you might have to use a minifier, or else the columns could stack on iPhone even if they're wrapped in <code>&lt;mj-group&gt;</code>. The <a href="https://mjml.io/documentation/#command-line-interface">MJML command-line interface</a> comes with a <a href="https://github.com/mjmlio/mjml/blob/master/packages/mjml-cli/README.md#render-and-minify-the-output-html">built-in minifier</a> that you can use to run the <code>-m</code> option when rendering MJML.</p>

<pre><code class="language-markup">
&lt;mj-section padding="0" background-color="#ffffff"&gt;
	&lt;mj-group&gt;
		&lt;mj-column&gt;
			&lt;mj-image align="right" padding="40 0 0 0" width="100" href="https://thrivemarket.com/blog?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"
						src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/blog_zpscedcgvla.jpg" alt="blog" title="blog" /&gt;
		&lt;/mj-column&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="15 0 0 0" href="https://thrivemarket.com/?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"
				src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/thrive-logo-250_zps4lonavha.jpg" title="logo" alt="logo" /&gt;
		&lt;/mj-column&gt;
		&lt;mj-column&gt;
			&lt;mj-image align="left" padding="40 0 0 0" width="100" href="https://thrivemarket.com/customer/account/login/referer/aHR0cHM6Ly90aHJpdmVtYXJrZXQuY29tL2ludml0ZT9jY29kZT1LRzZPQ0QzSCZ1YWV4cHRpbWU9MTc3ODYzNzg2MiZ1YXRva2VuPTE0NjJiOTc3YzFmYTcwYjA5YjU4NWYzYTg5NDNkNzlhNzA3OWFiMzE0MzkzZmU4OTg1MmZkODNmZDA1YjYzMWUmdWlkPTUwMTk4NTAmdXRtX2NhbXBhaWduPWRheTgmdXRtX2NvbnRlbnQ9bGVhZF93ZWxjb21lJnV0bV9tZWRpdW09bGlmZWN5Y2xlJnV0bV9zb3VyY2U9c2FpbHRocnU,/"
				src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/refer_zpsnoo1uzvu.jpg" title="refer and win" alt="refer and win" /&gt;
		&lt;/mj-column&gt;
	&lt;/mj-group&gt;
&lt;/mj-section&gt;
	</code></pre>

### One-Column Layout for the GIF and CTA

We'll create another section in which we'll simply add an image, some text and a button. The only new component here is <a href="https://mjml.io/documentation/#mjml-button"><code>&lt;mj-button&gt;</code></a>, which should be clear enough and which comes with the standard attributes. Please note that you must specify an <code>href</code>, or else the text of the button might not display in some email clients.</p>

<pre><code class="language-markup">
&lt;mj-section padding="20"&gt;
	&lt;mj-column&gt;
		&lt;mj-image padding="5 0 23 0" width="200px" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/566f6a67e871e_zpskalhjefi.gif" /&gt;
		&lt;mj-text align="center" font-size="16px"&gt;
			Your daily destination for healthy living
		&lt;/mj-text&gt;
		&lt;mj-button padding="20 0 10 0" mj-class="pill" href="https://thrivemarket.com/blog?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;
			Read more
		&lt;/mj-button&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

### Divider Between Body and Header

Yes, there's a component for that, too! It's a good practice to split different rows into different sections, instead of dumping everything into the same section, because that gives you more control over styling (especially through <code>padding</code>), and it also makes it easier to isolate any problems that occur.</p>

<pre><code class="language-markup">
&lt;mj-section padding="0 0 20 0"&gt;
	&lt;mj-column&gt;
		&lt;mj-divider border-width="5px" border-color="#EEEBE7" /&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

We'll use the same divider between the body and footer later.</p>

## Body

Now that <a href="https://mjml.io/try-it-live/templates/thrive_header">we have a beautiful header</a>, let's start with what seems to be the complex part of this email.</p>

### Two-Column Layout That Stacks on Mobile

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4c0373b-75ed-4f44-9059-f78b70be230a/2-column-layout-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4c0373b-75ed-4f44-9059-f78b70be230a/2-column-layout-preview-opt.png" alt="Two-column layout" width="617" height="304" /></a><figcaption>Two-column layout</figcaption></figure>

Here, we'll create a section for each two-column row. Each column will consist of an image, a piece of text and a button. The good news is that, thanks to MJML's hybrid approach, we don't have to do anything to make the images stack on mobile. It's responsive by default!

Regarding the styling, we don't have much to do because we're leveraging the mj-classes <code>pill</code> and <code>desc</code>, which we created earlier. All we need to do is add some <code>padding</code> to match the style of the original email.

Hack: Due to an issue with Outlook 2000, 2002 and 2003 ignoring the set width, it's a good practice in MJML to set images to the sizes you want them to display at in those clients.</p>

<pre><code class="language-markup">
&lt;mj-section padding="20 10 0 10"&gt;
	&lt;mj-column&gt;
		&lt;mj-image width="280px" href="https://thrivemarket.com/blog/foods-for-happiness?uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;uid=5019850&amp;utm_campaign=day8&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_source=sailthru"
			src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/5-foods_zps9escvg7g.jpg" /&gt;
		&lt;mj-text mj-class="desc"&gt;
			&lt;a href="https://thrivemarket.com/blog/foods-for-happiness?uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;uid=5019850&amp;utm_campaign=day8&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_source=sailthru"&gt;
			5 Foods to Boost Your Happiness
			&lt;/a&gt;
		&lt;/mj-text&gt;
		&lt;mj-button mj-class="pill" href="https://thrivemarket.com/blog/foods-for-happiness?uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;uid=5019850&amp;utm_campaign=day8&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_source=sailthru"&gt;
			Read more
		&lt;/mj-button&gt;
	&lt;/mj-column&gt;
	&lt;mj-column&gt;
		&lt;mj-image width="280px" href="https://thrivemarket.com/blog/whiten-teeth-instantly-activated-charcoal?uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;uid=5019850&amp;utm_campaign=day8&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_source=sailthru"
			src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/teeth_zpsr1sycjxi.jpg" /&gt;
		&lt;mj-text mj-class="desc"&gt;
			&lt;a href="https://thrivemarket.com/blog/whiten-teeth-instantly-activated-charcoal?uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;uid=5019850&amp;utm_campaign=day8&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_source=sailthru"&gt;
				Whiten Teeth Instantly with Activated Charcoal
			&lt;/a&gt;
		&lt;/mj-text&gt;
		&lt;mj-button mj-class="pill" href="https://thrivemarket.com/blog/whiten-teeth-instantly-activated-charcoal?uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;uid=5019850&amp;utm_campaign=day8&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_source=sailthru"&gt;
			Read more
		&lt;/mj-button&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

Here, we can see that the default HTML style for links is applied. In addition to <code>&lt;mj-attributes&gt;</code>, you can also inline CSS right into MJML using <a href="https://mjml.io/documentation/#mjml-style"><code>&lt;mj-style&gt;</code></a>. Let's do just that by updating the <code>head</code> to overwrite the default style of links once and for all. We'll also create a CSS class to apply to the <code>&lt;a&gt;</code> tags to give them the right color (we're creating a class because the links in the email shouldn't all have the same color).</p>

<pre><code class="language-markup">
	&lt;mj-head&gt;
	    &lt;mj-title&gt;Discover the latest trends&lt;/mj-title&gt;
	    &lt;mj-attributes&gt;
	      &lt;mj-all padding="0" /&gt;
	      &lt;mj-text font-family="sans-serif" color="#8e8b85" /&gt;
	      &lt;mj-class name="pill" font-weight="700" color="#d5ad4b" border-radius="50" border="2px solid #d5ad4b" font-size="16px" line-height="16px" padding="8 20 20 20" inner-padding="10 75 10 75" background-color="transparent" /&gt;
	      &lt;mj-class name="desc" font-family="Georgia" font-size="20px" color="#45495d" padding="25 5 10 10" /&gt;
	      &lt;mj-class name="ico" font-family="Helvetica" font-size="14px" align="center" padding="0 0"/&gt;
	    &lt;/mj-attributes&gt;
			&lt;mj-style&gt;
				a {
					text-decoration:none;
				}
				.desc {
					color: #45495d;
				}
			&lt;/mj-style&gt;
	&lt;/mj-head&gt;
	</code></pre>

Follow the same steps with the other two-column sections.</p>

### Blue Section With CTA

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82650d8c-38c5-4287-b2a9-545a29d29521/blue-section-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82650d8c-38c5-4287-b2a9-545a29d29521/blue-section-preview-opt.png" alt="Blue section" width="657" height="104" /></a><figcaption>Blue section</figcaption></figure>

To create this section, we'll use the components that we're getting familiar with: <code>&lt;mj-section&gt;</code>, <code>&lt;mj-column&gt;</code> and <code>&lt;mj-button&gt;</code>.

First, we'll add a <code>background-color</code> to our section and some <code>padding</code> so that it looks as expected. Then, we just have to create two columns, one wider than the other, leveraging the <code>width</code> attribute with percentages. As usual, columns will stack on mobile. Because the button is different from the others here, we won't use the <code>pill</code> class, but rather will manually create a new style.

Hack: Because of poor support for shorthand HEX colors in Internet Explorer, we recommend using six-digit HEX colors. This is a hack that we'll reintegrate in MJML at some point to make sure that three-digit HEX codes are turned into six-digit codes.</p>

<pre><code class="language-markup">
&lt;mj-section background-color="#6d8be1" padding="15 40 10 40"&gt;
	&lt;mj-column width="60%"&gt;
		&lt;mj-text font-weight="bold" color="#ffffff" font-size="16px" padding="0 0 10 0"&gt;
			Get all your healthy groceries at Thrive Market!
		&lt;/mj-text&gt;
	&lt;/mj-column&gt;
	&lt;mj-column width="40%"&gt;
		&lt;mj-button background-color="#ffffff" color="#45495d" font-weight="800" font-family="sans-serif" font-size="16px" border-radius="2px" inner-padding="15 60"&gt;
			Shop Now
		&lt;/mj-button&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

## Last Section Of The Body

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58a5ea73-6a77-4deb-ae77-ee42f309aa7f/last-part-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58a5ea73-6a77-4deb-ae77-ee42f309aa7f/last-part-preview-opt.png" alt="Last section of the body" width="643" height="369" /></a><figcaption>Last section of the body</figcaption></figure>

To design the title, we'll create a three-column layout. The columns will consist of the following, respectively:

*   the dark blue line to the left of the title,
*   the title `"Want More Tips, Tricks, and Delicious Recipes?"`,
*   the dark blue line to the right of the title.

Then, we will wrap the three columns in an <code>&lt;mj-group&gt;</code> so that it doesn't stack on mobile.

We'll start creating the lines, leveraging the <code>&lt;mj-divider&gt;</code> component, setting its <code>border-width</code> to <code>2px</code> and adding some <code>padding</code> so that it looks the way we want. By default, the divider will fill the column it's contained in, so that it looks consistent across devices. Therefore, we don't need to explicitly set the width of the divider.

Then, we're just using <code>&lt;mj-text&gt;</code> to add our title, leveraging the <code>desc</code> mj-class (because we want to inherit some of the styles set in this class) and overriding the <code>font-family</code> and <code>align</code> properties that are different from this class. We could have also manually set the style without using the <code>desc</code> mj-class.

Finally, we just have to use our button with the <code>pill</code> mj-class as we did before. We're overriding the <code>inner-padding</code> because, according to the original design, this button is not as wide as the others.</p>

<pre><code class="language-markup">
&lt;mj-section padding="40px 0 0 0"&gt;
	&lt;mj-group&gt;
		&lt;mj-column width="12%"&gt;
			&lt;mj-divider border-width="2px" padding="10 0 0 10" /&gt;
		&lt;/mj-column&gt;
		&lt;mj-column width="75%"&gt;
			&lt;mj-text padding="0 0 20 0" mj-class="desc" font-family="Helvetica" align="center"&gt;
				&lt;a class="desc" href="https://thrivemarket.com/blog?utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;
					Want More Tips, Tricks, and Delicious Recipes?
				&lt;/a&gt;
			&lt;/mj-text&gt;
		&lt;/mj-column&gt;
		&lt;mj-column width="13%"&gt;
			&lt;mj-divider border-width="2px" padding="10 10 0 0" /&gt;
		&lt;/mj-column&gt;
	&lt;/mj-group&gt;
&lt;/mj-section&gt;

&lt;mj-section padding="5px"&gt;
	&lt;mj-column&gt;
		&lt;mj-image src="https://img.thrivemarket.com/emails/images/img-18.jpg" href="https://thrivemarket.com/blog?utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru" /&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;

&lt;mj-section padding="15px"&gt;
	&lt;mj-column&gt;
		&lt;mj-button mj-class="pill" inner-padding="12 25" href="https://thrivemarket.com/blog?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;
			Read our Blog
		&lt;/mj-button&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

<a href="https://mjml.io/try-it-live/templates/thrive_body">You can see</a> what our MJML template should look like so far.</p>

## Footer

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cc3c24d-baa5-41d4-b582-0bf9ad34f70b/footer-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cc3c24d-baa5-41d4-b582-0bf9ad34f70b/footer-preview-opt.png" alt="Footer of the email" width="650" height="575" /></a><figcaption>Footer of the email</figcaption></figure>

### Title

We're wrapping our title in a section and a column, as we've seen before, and we're using the <code>desc</code> style that we created earlier. We need to alter only a few styles by manually setting a different <code>align</code>, <code>font-size</code> and <code>font-style</code> from our mj-class.</p>

<pre><code class="language-markup">
&lt;mj-section background-color="#EEEBE7" padding="25"&gt;
  &lt;mj-column&gt;
	  &lt;mj-text padding-top="20px" mj-class="desc" align="center" font-size="28px" font-style="italic"&gt;
			Stay Connected
		&lt;/mj-text&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

### Six-Icon Section

This section is made up of six icons, with accompanying text below. The icons display side by side on desktop and wrap to two lines of three icons on mobile. By now, you probably know that creating such layouts is easy if we leverage the <code>&lt;mj-column&gt;</code> component. To make the icons stack onto two lines, all we have to do is wrap the columns in two groups of three columns in an <code>&lt;mj-group&gt;</code>.

To design the text below the icons, we just have to use the <code>ico</code> mj-class that we created before. We'll also create a CSS class named <code>ico</code> to apply to the <code>a</code> tags, like we did in the two-column layout section.</p>

<pre><code class="language-markup">
&lt;mj-section padding="40 0"&gt;
	&lt;mj-group&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="10" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/img-01_zpssvjtmopj.png" /&gt;
			&lt;mj-text mj-class="ico"&gt;&lt;a class="ico" href="https://thrivemarket.com/paleo?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Paleo&lt;/a&gt;&lt;/mj-text&gt;
		&lt;/mj-column&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="10" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/img-02_zpshj3vgh1w.png" href="https://thrivemarket.com/gluten-free?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"/&gt;
			&lt;mj-text mj-class="ico"&gt;&lt;a class="ico" href="https://thrivemarket.com/gluten-free?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Gluten Free&lt;/a&gt;&lt;/mj-text&gt;
		&lt;/mj-column&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="10" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/img-03_zpshvwomzpo.png" href="https://thrivemarket.com/vegan?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"/&gt;
			&lt;mj-text mj-class="ico"&gt;&lt;a class="ico" href="https://thrivemarket.com/vegan?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Vegan&lt;/a&gt;&lt;/mj-text&gt;
		&lt;/mj-column&gt;
	&lt;/mj-group&gt;
	&lt;mj-group&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="10" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/img-04_zpsyeczb1sp.png" href="https://thrivemarket.com/ingredients/gmo-free?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru" /&gt;
			&lt;mj-text mj-class="ico"&gt;&lt;a class="ico" href="https://thrivemarket.com/ingredients/gmo-free?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Non-GMO&lt;/a&gt;&lt;/mj-text&gt;
		&lt;/mj-column&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="10" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/img-05_zpsryppwpok.png" href="https://thrivemarket.com/certifications/certified-organic?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru" /&gt;
			&lt;mj-text mj-class="ico"&gt;&lt;a class="ico" href="https://thrivemarket.com/certifications/certified-organic?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Organic&lt;/a&gt;&lt;/mj-text&gt;
		&lt;/mj-column&gt;
		&lt;mj-column&gt;
			&lt;mj-image padding="10" src="https://i1044.photobucket.com/albums/b447/ngarnier/Thrive%20Market/img-06_zpsoq4ulmbq.png" href="https://thrivemarket.com/raw?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru" /&gt;
			&lt;mj-text mj-class="ico"&gt;&lt;a class="ico" href="https://thrivemarket.com/raw?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Raw&lt;/a&gt;&lt;/mj-text&gt;
		&lt;/mj-column&gt;
	&lt;/mj-group&gt;
&lt;/mj-section&gt;
</code></pre>

### Social Networks

Once again, this section is easy to achieve by leveraging the <code>&lt;mj-column&gt;</code> component, using one column per social network icon and wrapping all of the icons in an <code>&lt;mj-group&gt;</code> so that they don't stack on mobile. The only trick here is to fine-tune the <code>width</code> of the images and the padding so that the result is consistent with the original design.</p>

### Divider and Text

Because this part is pretty simple, it's OK to wrap the divider and the text in the same column and section, even though we could have separated the divider from the text. As we did before when styling the links, we'll create a <code>footer</code> class so that our links have the proper color.</p>

<pre><code class="language-markup">
&lt;mj-section background-color="#EEEBE7" padding="25 40"&gt;
	&lt;mj-column&gt;
		&lt;mj-divider /&gt;
		&lt;mj-text padding="30 0 0 0" align="center" font-size="14"&gt;&lt;a class="footer" href="https://thrivemarket.com/blog?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Read Our Blog&lt;/a&gt; &lt;a class="footer" href="https://thrivemarket.com/"&gt;View Email Online&lt;/a&gt;&lt;/mj-text&gt;
		&lt;mj-text align="center" color="#45495d" font-size="10px" line-height="14px"&gt;
			&lt;p&gt;Please don't hit 'reply' to this email—we won't be able to email you back from this address and help you thrive! If you need anything, visit our &lt;a class="footer" href="https://thrivemarket.com/faq?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;FAQ&lt;/a&gt; or contact &lt;a class="footer" href="https://thrivemarket.com/faq/contact?uid=5019850&amp;uaexptime=1778637862&amp;uatoken=1462b977c1fa70b09b585f3a8943d79a7079ab314393fe89852fd83fd05b631e&amp;ccode=KG6OCD3H&amp;utm_content=lead_welcome&amp;utm_medium=lifecycle&amp;utm_campaign=day8&amp;utm_source=sailthru"&gt;Member Services&lt;/a&gt; anytime, and we'll be happy to help!&lt;/p&gt;
			&lt;p&gt;We don't want to see you go, but if you no longer wish to receive promotional emails from us, you can &lt;a class="footer" href="https://thrivemarket.com/"&gt;unsubscribe here&lt;/a&gt; or &lt;a class="footer" href="https://thrivemarket.com/"&gt;change your email preferences&lt;/a&gt; anytime.&lt;/p&gt;
			&lt;p&gt;4509 Glencoe Ave, Marina Del Rey, CA 90292 &lt;br /&gt;@2016 Thrive Market All Rights Reserved&lt;/p&gt;
		&lt;/mj-text&gt;
	&lt;/mj-column&gt;
&lt;/mj-section&gt;
	</code></pre>

## Rendering the HTML File and Testing

You should now have fewer than 240 lines of MJML (you can check <a href="https://mjml.io/try-it-live/templates/thrive_email">the full code</a>), whereas the original file was a bit less than 800 lines of HTML. Congrats! You've just created your first responsive email using MJML! How easy was that?

Testing how an email renders in different email clients is always a good practice, so let's do just that using <a href="https://litmus.com/builder/">Litmus</a> (<a href="https://www.emailonacid.com/">Email on Acid</a> is another great platform for email testing).</p>

<a href="https://litmus.com/builder/">Go to Litmus</a> (create an account if you don't have one already), create a new project, and paste the HTML that we generated earlier in the code area. You'll be able to see the results in various email clients by clicking "Instant Previews" in the right pane. <a href="https://imgur.com/a/l3xHE">You can see</a> the results for major email clients, from Outlook 2003 to Inbox by Gmail.</p>

## Going Further

Now that you know how to use MJML to easily create a responsive email, why not try to create your own component? <a href="https://medium.com/mjml-making-responsive-email-easy/tutorial-creating-your-own-mjml-component-d3a236ab7093#.d1ji1oheq">My tutorial</a> will guide you through this step by step.

What did you think about your first experience with MJML? Feel free to reach out <a href="https://twitter.com/mjmlio">on Twitter</a> and join the MJML community now by signing up to the <a href="https://slack.mjml.io/">Slack</a> channel. You can also <a href="https://mjml.io/">subscribe to the newsletter</a> to keep up to date on the latest news.

{{< signature "rb, vf, yk, al, il" >}}

