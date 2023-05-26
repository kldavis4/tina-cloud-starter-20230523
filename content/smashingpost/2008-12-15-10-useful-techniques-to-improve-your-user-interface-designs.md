---
title: 10 Useful Techniques To Improve Your User Interface Designs
slug: 10-useful-techniques-to-improve-your-user-interface-designs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58ce0d4c-5d50-4da8-88ba-7ba2dc08a73d/usability-principles.png
date: 2008-12-15T22:11:03.000Z
author: dmitry-fadeyev
description: >-
  Web design consists, for the most part, of interface design. There are many
  techniques involved in crafting beautiful and functional interfaces. Here's my
  collection of 10 that I think you'll find useful in your work. They're not
  related to any particular theme, but are rather a collection of techniques I
  use in my own projects. Without further ado, let's get started.
categories:
  - UX
  - Techniques
  - Usability
  - Interfaces
  - Web Design
  - UX
  - UI
  - Interaction Design
---
Web design consists, for the most part, of <a title="Better Interface Design: Logins, Menus, Toggles And Other Fancy Modules" href="https://www.smashingmagazine.com/2016/04/inspiring-ui-demos-logins-menus-toggles-and-more/">interface design</a>. There are many techniques involved in crafting beautiful and functional interfaces. Here's my collection of 10 that I think you'll find useful in your work. They're not related to any particular theme, but are rather a collection of <a title="12 Useful Techniques For Good User Interface Design" href="https://www.smashingmagazine.com/2009/01/12-useful-techniques-for-good-user-interface-design-in-web-applications/">techniques</a> I use in my own projects. Without further ado, let's get started. 

## 1\. Padded block links

Links (or anchors) are inline elements by default, which means that their clickable area spans only the height and width of the text. This clickable area, or the space where you can click to go to that link's destination, can be increased for greater usability. We can do this by <strong>adding padding</strong> and, in some cases, also <strong>converting the link into a block element</strong>. Here's an example of inline and padded links, with their clickable areas highlighted to show the difference:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/993aec36-8477-40b8-8445-f06541c38b86/padded-links-diagram.png" alt="Improve Your User Interface Designs" width="480" height="232" />

Obviously, the larger the clickable area is, the easier it is to click on the link because there is less of a chance of missing it. Converting links into block elements makes the text area span the whole width of the container, unless the width is specified otherwise. This makes it ideal for links located in sidebars. We can do it with the following code:

{{% feature-panel %}}

<pre><code class="language-css">a {
	display: block;
	padding: 6px;
}</code></pre>

Make sure to also add a healthy dose of padding to the links, because converting a link into a block only affects its behavior and width; adding padding ensures that the link is high enough and has some room to breathe.</p>

## 2\. Typesetting buttons

Attention to every detail is what separates a great product from a mediocre one. Interface elements such as buttons and tabs are clicked on many times a day by your users, so it pays to typeset them properly; and by typesetting I mean positioning the label. Here's a couple of examples of the kind of misplaced labels I sometimes notice:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/187eb5d2-2405-4aa2-b9cf-ba6066b15f8f/badly-typeset-buttons.png" alt="Badly typeset button labels" width="287" height="56" />

At first glance they look okay, but notice that the text is placed too high because the lowercase letters have been used as a guide to align the text vertically in the center, like so:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2033eab-15a9-4f77-b028-a352d2762ac0/button-typeset-1.png" alt="Badly typeset button labels" width="300" height="160" />

However, if we use uppercase letters as well as lowercase letters with ascenders ("t," "d," "f," "h," "k" and "l"), <strong>the balance shifts upwards</strong>, making the label appear too high on the button. In such cases, we should set the type using the uppercase height as a guide -- or set it a little bit higher if most of the letters are lowercase. Here's what I mean:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e369550-06fd-43a1-847e-316166d30d7a/button-typeset-2.png" alt="Badly typeset button labels" width="300" height="160" />

This gives the whole button a more <strong>balanced look and feel</strong>. Little touches like this go a long way towards making your interface more polished and satisfying to use.</p>

## 3\. Using contrast to manage focus

Similarly, you can also manage the focus of your visitors' attention with contrast between elements. Here's an example of a post headline and some meta information underneath regarding who posted the article and its date:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e717ea40-2f8c-4d49-9975-3bdac8cf3b5d/headline1.png" alt="A typical blog post headline" width="480" height="80" />

All the text is set in black. Let's decrease the contrast between the meta information (the date and author's name) and the background by putting the text in a light shade of gray:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d0d19a9-7ece-4a87-8b23-b76441c21e70/headline2.png" alt="Headline with adjusted contrast" width="480" height="80" />

The highest contrast element here is the headline, so it literally pops out at us. The other elements fade into the background. Here, I've chosen the author as the second-most important element, and the date as the least. The font also differs in size and style, but the contrast level can be very powerful. Let's reverse the order of importance to date, author and headline:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/803baeb3-46ae-4d23-bbbe-59541a17f921/headline3.png" alt="Another headline with adjusted contrast" width="480" height="80" />

You can see how effective it is in shifting focus: the date now pops out at you, while the headline fades away. This technique comes in very handy for information-heavy websites, such as blogs, forums and social networks, in which you want to make a lot of information easily scannable while still showing a lot of additional things, like dates. Fading the extras allows visitors to easily focus their attention on the most important pieces of text.</p>

## 4\. Using color to manage attention

<a title="The Meaning of Color" href="https://www.smashingmagazine.com/2010/01/color-theory-for-designers-part-1-the-meaning-of-color/">Color</a> can also be used to effectively <strong>focus your visitors' attention on important or actionable elements</strong>. For example, during the US presidential election, pretty much all of the candidates' websites had the donation button colored red. Red is a very bright and powerful color so it attracts attention, and it stands out even more when the rest of the website is blue or another colder color.

Warmer tones like red, yellow and orange are naturally bright and so tend to attract the eye. They also "expand" when set against colder colors like blue and green. This means that an orange button on a blue background looks like it's flowing outwards and taking the front seat. Conversely, a blue button on an orange background contracts inward, wishing to stay in the background. Here's a picture to illustrate:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3bf5ce-6a80-4eb4-90d4-1d2793f288c4/colors.png" alt="Comparing warm and cold colors" width="370" height="141" />

Here's a couple of examples of websites that use color effectively to direct users' attention to the important elements:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7d51c27-6315-465f-b3aa-0d945aedb0dc/function.jpg" alt="Improve Your User Interface Designs" width="480" height="289" /><br>
<em>Function features a "We're Hiring" link on its jobs page. To ensure the link is not missed, the designers set it against a red background that pops out from the dark background header, effectively grabbing attention.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7eeeea6-9968-4148-90f5-24437ef449a2/causecast.jpg" alt="Causecast website" width="480" height="298" /><br>
<em>Causecast use color effectively. Four bright pink elements pop out at you: the logo, the feedback link, the donate link and the website description message.</em>

Want the "About" blurb on your website to grab the visitor's focus? Make the background yellow. Want to make the "Join" button stand out? Color it orange. Make sure not to highlight too many elements, though; if you do, they may get lost in each other's company.</p>

## 5\. White space indicates relationships

One of the most crucial elements in an interface is the white space between elements. If you're not familiar with the term white space, it means just that: space between one interface element and another, be it a button, a navigation bar, article text, a headline and so on. By manipulating white space, we can indicate relationships between certain elements or groups of elements.

So, for example, by putting the headline near the article text we indicate that it is related to that text. The text is then placed farther away from other elements to separate it and make it more readable. Here's an example in which white space could be improved:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ed33bc4-9b1d-4819-b619-24f894f44093/bad-whitespace.png" alt="Whitespace usage here can be improved" width="480" height="242" />

The text looks all right and is certainly readable, but because the spaces above and below each heading are equal, they don't separate each piece of text clearly. We can improve this by increasing the white space between each section and also by slightly tightening the line height of the paragraphs:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd06a112-39f0-46b6-a026-be54d57dd7bb/good-whitespace.png" alt="Improved whitespace" width="480" height="242" />

<strong>This results in more clearly defined blocks</strong>; we can easily tell which headings go with which pieces of text and can see the separate sections clearly. Good designers often squint or glance at their work from a distance, which lets them see the blocks of elements separated by white space as they merge together. If you cannot see these groups clearly then you may need to tweak your white space.

## 6\. Letter spacing

Web design is pretty limiting for typographers. But while there are only a few safe Web fonts and not a great many things you can do to style them, it's worth remembering that we do still have some level of control. "Tracking" is a term used in the field of typography to describe the adjustment of <strong>spacing between letters in words</strong>. We've got the ability to do this with CSS using the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing">letter-spacing property</a>.

If used with restraint and taste, this property can be effective in improving the look of your headlines. I wouldn't recommend using letter spacing on the body text because the default spacing generally provides the best readability for smaller font sizes.

Here's an example of letter spacing in use:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e311909-b6fa-4e96-a019-bd2cc1d28717/letter-spacing.png" alt="Letter spacin examples" width="340" height="155" />

And here's the CSS code used for the above examples:

<pre><code class="language-css">h1 {
	font-family: Helvetica;
	font-size: 27px;
}

h2 {
	font-family: Helvetica;
	font-size: 27px;
	letter-spacing: -1px;
}

h3 {
	font-family: Georgia;
	font-size: 24px;
	letter-spacing: 3px;
	font-variant: small-caps;
	font-weight: normal;
}</code></pre>

The effect can be useful when you want to craft a more aesthetically pleasing or more original heading. Here, I've used only a couple pixels for letter spacing, but already it makes a big difference to the style of the font.</p>

## 7\. Auto-focus on input

Many Web applications and websites feature forms. These may be search forms or input forms inviting you to submit something. If this form is the <strong>core feature</strong> of your application or website, you may want to consider <strong>automatically focusing the user's cursor on the input field</strong> when the website loads. This will speed things up because users can start typing right away without having to click on it. A good example of this is Google and Wikipedia's websites.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0082723-9358-4163-8761-be29a4b86641/wikipedia-auto-focus.png" alt="Wikipedia auto focus" width="420" height="70" /><br>
<em>Upon arriving at <a href="https://www.wikipedia.org">Wikipedia.org</a>, the search box is already highlighted, ready to accept text.</em>

To automatically focus on input fields, you'll need a little bit of JavaScript. There are various solutions, and the one you should use depends on the functionality you want to achieve. The simplest way to do it would be to add the following to your body tag:
<pre class="language-markup tmp-html">&lt;body onLoad="document.forms.form_name.form_field.focus()"&gt;</pre>

Your form code should look something like:
<pre class="language-markup tmp-html">&lt;form method="get" name="form_name" action="#"&gt;
	&lt;input type="text" name="form_field" size="20" /&gt;
	&lt;input type="submit" value="Go" /&gt;
&lt;/form&gt;</pre>

Now, every time the page loads, the text field called "form_field" will be automatically selected, ready for input.

The only problem with this is that if your users want to return to the previous page using the Backspace key, they will be out of luck because they'll just be deleting characters in the input field. Thankfully, Harmen Janssen has another simple JavaScript solution you can find <a href="https://www.whatstyle.net/articles/51/focus_onload_but_keep_backspace_intact">here</a>. Harmen's script allows the Backspace key to go to the previous page when there are no characters left in the input field to delete.</p>

## 8\. Custom input focus

While the default look of form elements suffices for most functions, sometimes we want something a little prettier or a little more standardized across various browsers and systems. We can style input fields by simply targeting it with an "id," "class" or plain old "input," like so:

<pre><code class="language-css">input {
	border: 2px solid #888;
	padding: 4px;
	font-size: 1em;
	background-color: #F8F8F8;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a737740-608c-4f4c-b99a-7edb4fbc4402/styled-input-field.png" alt="Default and styled input fields" width="300" height="165" />

What's more interesting is also being able to style the input field when it's in focus; that is, the state it's in when it has been clicked. To do this, we need to attach a "<strong>:focus</strong>" after the "input" property:

<pre><code class="language-css">input:focus {
	border-color: #000;
	background-color: #FFFE9D;
}</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/191c3eec-af1d-4592-8a67-4a5de5c44ba3/input-focused.png" alt="Input field in focus" width="300" height="60" />

If you're using custom backgrounds to style your input field, they may clash with some browsers and operating systems' default focus styles. For example, here's a screenshot of a custom-styled form clashing with the default blue OS X glow effect:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9a76fd-bbc6-4592-80e8-7a08c10345e1/blueglow.png" alt="OS X input glow" width="245" height="51" />

In such cases, you could also use the "input:focus" property to remove the default styling. The default blue glow in the screenshot above can be removed by disabling the "outline" property:

<pre><code class="language-css">input:focus {
	outline: none;
}</code></pre>

The blue glow effect will now be gone:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac651c5-dbf6-49a7-91a6-c2d85385d7ca/noglow.png" alt="OS X input glow removed" width="245" height="51" />

Obviously you would only want to remove the outline if you're replacing it with your own styling, so that you don't negatively affect the accessibility and usability of your forms.</p>

## 9\. Hover controls

Some Web applications have extra utility controls, such as edit and delete buttons, that don't necessarily have to be shown beside every item at all times. They can be hidden to <strong>simplify the interface and focus visitors' attention on the main controls and content</strong>. For example, these hover controls are used in Twitter when you hover over messages:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4152e6e-c4bd-4e5f-b9b3-dca2b6324679/twitter-hover-controls.png" alt="Twitter's hover controls" width="480" height="248" />

These hover controls can be achieved with some simple CSS code, without any JavaScript. Simply style the &lt;div&gt; with the controls when its parent &lt;div&gt; is in a hover state. Here's the code to hide and show the controls (using a &lt;div&gt; with the class "controls" inside a &lt;div&gt; with the class "message"):

<pre><code class="language-css">.message .controls { display: none; }
.message:hover .controls { display: block; }</code></pre>

When you hover over the "message" &lt;div&gt;, the "controls" &lt;div&gt; inside it will appear, along with all of its content, giving you the same functionality as shown in the Twitter screenshot above.

There may be an issue with accessibility because screen readers may not be able to read the hidden &lt;div&gt;. There are plenty of other ways to hide the inner &lt;div&gt;, such as offsetting it with a negative margin that takes it off the page (e.g. "left-margin: -9999px"), coloring its text the same color as the background or simply placing another &lt;div&gt; on top of it.

This technique should of course be used with <strong>restraint</strong> because you don't want to hide your important controls; but if used correctly, it can be useful for <strong>cleaning up your interface</strong> by removing those extra utility links that you don't want to show up at all times.

Note that this doesn't work in IE6, so you'll need to override the hiding property in your IE6-specific style sheet or, if you don't have one, simply use the following IE6-specific code inside the &lt;head&gt; section of your code:

<pre><code class="language-css">&lt;!--[if lt IE 7]&gt;
  &lt;style type="text/css" media="screen"&gt;
    .message .controls { display: block; }
  &lt;/style&gt;
&lt;![endif]--&gt;</code></pre>

## 10\. Verbs in labels

You can make options dialogs much more usable by thinking through the labels you use on buttons and links. If an error or message pops up and the options are "Yes," "No" and "Cancel," you have to read the whole message to be able to answer. Seems normal, right?

But we can actually speed things up by using verbs in the labels. So, if instead of "Yes," "No" and "Cancel," we have "Save," "Don't Save" and "Cancel" buttons, you wouldn't even need to read the message to understand what the options are and which action to perform. <strong>All the information is contained in the button labels.</strong>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/457cbde5-7339-4763-a167-798ad2f94d2f/save-dialogs.png" alt="WordPad and OS X save dialogs" width="480" height="364" />

Using verbs in labels on buttons and links makes the options dialogs more usable because the labels contain all of the information the user needs to be able to make a decision.</p>

## To Conclude

Hopefully, you've found a few new techniques that will be useful in your work. As always, using them effectively comes down to restraint and thoughtful implementation. For example, controls that appear on hover may clean up your interface, but they will also increase the learning curve because people may not notice these controls at first. But showing all controls at all times may not be the best strategy either because users would need to scan more things to find what they're looking for.

<a title="Don’t Follow Web Design Trends: Set Them!" href="https://www.smashingmagazine.com/2008/11/dont-follow-trends-set-them/">Striking the right balance between what you show and what you hide</a> is a delicate art and is completely in your hands as the designer. Don't use a technique just because it exists: <strong>use it if it makes sense in your context</strong>.<em> (al)</em>

