---
title: 7 Principles Of Clean And Optimized CSS
slug: 7-principles-of-clean-and-optimized-css-code
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df45d711-7e1e-4576-b087-88faac25ee30/css-clean.jpg
date: 2008-08-18T22:49:31.000Z
author: tony-white
description: >-
  Some of you may remember the days when 30KB was the recommended maximum size
  of a web page, a value which included HTML, CSS, JavaScript, Flash, and
  images. I find with every new project with even the slightest bit of
  complexity, it's not long before that 30 KB ideal is well out of my reach.
  With the popularity of CSS layouts and JavaScript-enriched web page
  experiences, it's not uncommon, particularly for large sites, for the CSS
  files alone to jump well beyond that 30KB ceiling.
categories:
  - Coding
  - Workflow
  - CSS
  - Principles
  - Optimization
---
Some of you may remember the days when 30KB was the recommended maximum size of a web page, a value which included HTML, CSS, JavaScript, Flash, and images. I find with every new project with even the slightest bit of complexity, it's not long before that 30 KB ideal is well out of my reach. 

With the popularity of CSS layouts and <a title="Useful JavaScript Libraries and jQuery Plugins" href="https://www.smashingmagazine.com/2012/09/useful-javascript-libraries-jquery-plugins/"> JavaScript-enriched web page experiences</a>, it's not uncommon, particularly for large sites, for the CSS files alone to jump well beyond that 30KB ceiling.

But there are some principles to consider during and after you <a title="Mastering CSS Principles: A Comprehensive Guide" href="https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/">write your CSS</a> to help keep it tight and optimized. <strong>Optimization isn't just minimizing file size</strong> — it's also about being organized, clutter-free, and efficient. You'll find that the more knowledge you have about <a title="12 Principles For Keeping Your Code Clean" href="https://www.smashingmagazine.com/2008/11/12-principles-for-keeping-your-code-clean/">optimal CSS practices</a>, smaller file size will inevitably come as an direct result of their implementation.

You may already be familiar with some of the principles mentioned below, but they are worth a review. Being familiar with this concepts will help you write optimized CSS code and make you a better all-around web designer.</p>

## 1\. Use Shorthand

If you're not already <strong>writing in shorthand</strong>, you're late to the party. But fortunately, this party never ends. Using shorthand properties is the single easiest practice you can do to cut down your code (and coding time). There's no better time than the present to start this efficient coding practice, or to review it.

{{% feature-panel %}}

<code>Margin</code>, <code>border</code>, <code>padding</code>, <code>background</code>, <code>font</code>, <code>list-style</code>, and even <code>outline</code> are all properties that allow shorthand (and that's not even an extensive list!).

CSS Shorthand means that instead of using different declarations for related properties...

<pre><code class="language-css">p { margin-top: 10px;
	margin-right: 20px;
	margin-bottom:  30px;
	margin-left: 40px; }</code></pre>

... you may use shorthand properties to combine those values like so:

<pre><code class="language-css">p { margin: 10px 20px 30px 40px; }</code></pre>

By specifying a different number of values, browsers would interpret the rules in a specified manner, illustrated in the diagram below.

<img loading="lazy" decoding="async" title="Illustration of how shorthand declarations are interpreted depending on how many values are specified for a property" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eb754a6-893b-4a48-b8d4-b9b2db0ee650/figurea.gif" alt="css optimization" width="630" height="243" /><br>
<em>Illustration of how shorthand declarations are interpreted depending on how many values are specified for a property. This order also applies to <code>padding</code> and <code>border-width</code> among other properties.</em>

Font is another helpful shorthand property that helps save some room and keystrokes.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9f1d28c-c6b4-40d7-a113-e51d27e562cc/figureb.gif" alt="Illustration of font shorthand examples" width="630" height="173" /><br>
<em>Examples of the font shorthand property. Note: leaving some values unspecified will mean that those properties will reset to thier initial values.</em>

Those are just two examples of shorthand, but by no means should be considered a comprehensive guide. Even if you are familiar with the rules above, be sure to look at the articles mentioned below for more helpful reminders of those powerful properties that help keep your code succinct. Because of the number of lines and characters saved, going from a previous version of a CSS file which used no shorthand properties to one that makes full use of shorthand can have dramatic effect on file size.

See <a href="https://www.dustindiaz.com/css-shorthand/">CSS Shorthand Guide</a> (dustindiaz.com) and <a href="https://www.456bereastreet.com/archive/200502/efficient_css_with_shorthand_properties/">Efficient CSS with shorthand properties</a> (456bereastreet.com) for more information about shorthand properties.</p>

## 2\. Axe the Hacks

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d817c95a-a3ab-463d-b366-0d41abcce3f4/figuree.jpg" alt="Jon Hick's blog hicksdesign.co.uk/journal makes use of conditional comments" width="630" height="358" /><br>
<em>Jon Hick's blog makes use of conditional comments</em><br>
<blockquote cite="https://www.digital-web.com/articles/keep_css_simple/">Hacks against dead browsers are safe, but hacks against the living aren't. None of them. Ever.

<cite><a href="https://www.digital-web.com/articles/keep_css_simple/">Keep CSS Simple</a> - Peter-Paul Koch (digitial-web.com)</cite></blockquote>

If you're like me, those words from Peter-Paul Koch's nearly 5-year-old article may make you feel a little embarrased. After all, who hasn't served hacks to Internet Explorer 6 and even Internet Explorer 7? As bad as we may want IE6 to lay six pixels under, the truth is it's far from dead.

But now we know that using conditional comments to serve <del>hacks</del> correctional declarations for IE6 and IE7 is an accepted practice, even recommended by the Microsoft IE development team. <strong>Using conditional comments</strong> to serve IE-specific CSS rules has the added benefit of serving a cleaner, and therefore smaller, default CSS file to more standards-compliant browsers, while only those browsers that need the hackery daiquri (i.e. IE) will download the additional page weight.

Here's how to use conditional comments to serve styles only to Internet Explorer 6:

<pre><code class="language-html">&lt;!--[if IE 6]&gt;
		&lt;link rel="stylesheet" type="text/css" href="ie6.css"&gt;
	&lt;![endif]--&gt;
</code></pre>

For IE7, you can use the above and substitute "6" for "7".

Alternatively, if there is hack-less way of getting the desired result using CSS, with all other things being equal, go for it! The less hacks you have to write, the simpler and lighter the code.</p>

## 3\. Use whitespace wisely

Whitespace, including spaces, tabs, and extra line breaks, is <strong>important for readability</strong> for CSS code. However, whitespace does add, however miniscule it may be, to page weight. Every space, line-break, and tab you can eliminate is like having one less character.

But this is one area where I would not encourage you to skimp just to get a smaller file. It's still important that you write in a way that is readable to you (and hopefully to others), and if that includes using whitespace for formatting, so be it. After all, if you can't read it, you're going to have a hard time applying the other principles mentioned in this article. Just be <em>aware</em> of the fact that whitespace is like air - you might not be able to see it, but it does weigh something.

The figure below shows two different extremes in formatting style, with much whitespace, and the other with very little. I happen to <strong>favor the single-line formatting option without tabs</strong>, as I can scan the selectors a little easier, and I develop using the full width of my wide-screen monitor. But that's just me. You may like your selectors to appear nested, and your declarations on each line.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0aefa1b6-93e0-434b-bf93-63dde5854786/figurec.gif" alt="Illustration of two extremes in CSS formatting, one with lots of whitespace, one with little whitespace" width="630" height="411" /><br>
<em>Illustration of two extremes in CSS formatting: lots of whitespace vs. very little whitespace</em>

Using whitespace effectively is great, and a recommended practice for easy-to-manage code, but be aware that the less whitespace you have, the smaller the file. Even if you choose work with whitespace with your working file, you can choose to remove it for the production version of your CSS file, so your files stay skinny where it really counts.</p>

## 4\. Prune frameworks and resets

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9ae4aac-2df0-4204-a1b1-5b1592f42597/figuref.jpg" alt="Nathan Smith's 960 Grid System uses a reset" width="630" height="347" /><br>
<em>Nathan Smith's <a href="https://960.gs/">960 Grid System</a> CSS framework uses a reset rule.</em>

If you've chosen to use a CSS framework (including ones you've written yourself), take the time to review the documentation <em>as well as every line</em> of the CSS file. You may find that the framework includes some rules that you don't care to use for your current project, and they can be weeded out. Also, you may find that the framework includes a more elegant and concise way of achieving a presentational detail than what you normally use, and knowing about them can help prevent you duplicating rule sets unintentionally.

This goes for resets as well. <a href="https://yuilibrary.com/yui/docs/cssgrids/">YUI Grid CSS</a> uses a reset, and Eric Meyer's <a href="https://meyerweb.com/eric/tools/css/reset/">Reset</a> is also very popular. Resets are great to use because they help to neutralize a browser's default style. But if you know the nature of the site you are building, you may find some declarations that you know you'll never need. <code>&lt;pre&gt;</code> and <code>&lt;code&gt;</code> will likely go unused on my Aunt Martha's recipe blog. A design portfolio probably won't ever use <code>&lt;sub&gt;</code>, <code>&lt;dfn&gt;</code>, <code>&lt;var&gt;</code>, etc. So ditch what you don't need. It's not only ok, it's encouraged, even by Eric Meyer:
<blockquote cite="https://meyerweb.com/eric/thoughts/2008/04/17/crafting-ourselves/">As I say on <a href="https://meyerweb.com/eric/tools/css/reset/">the reset page</a>, those styles aren't supposed to be left alone by anyone. They're a starting point.

<cite><a href="https://meyerweb.com/eric/thoughts/2008/04/17/crafting-ourselves/">Crafting Ourselves</a> - Eric Meyer (meyerweb.com)</cite></blockquote>

Using a framework and/or a reset set of rules can help keep your work optimized, but they should not be accepted in their default state. Considering each declaration and cutting back on unneccessary ones can further help you keep your CSS files lean and readable.

## 5\. Future-proof your CSS

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b45b109-e4f2-4c02-ae57-43215539c671/figured.jpg" alt="Doug Bowman's stopdesign.com CSS reveals specially crafted selectors used for layout" width="630" height="400" /><br>
<em>Doug Bowman's CSS reveals specially crafted selectors used for layout.</em>

Another way to optimize your code is to separate layout-specific declarations from the rest of your rules. I've heard options of separating typography and colors from layout-specific rules in the CSS file. I've never been fond of this practice, as I don't care to repeat selectors just because I have different types of declarations to associate with them.

However, I'm warming up to the idea of <strong>separating layout styles from the rest of the styles</strong>, and giving layout it's own file, or at least it's own section. This is also advocated in Andy Clarke's Transcending CSS. Within the book, Clarke reminds us of the following:
<blockquote>Full CSS layouts have always been a compromise. The current CSS specifications were never designed to create the visually rich and complex interface layouts that modern Web demands. The current methods — floats and positioning — were never intended as layout tools.

<cite><a href="https://www.transcendingcss.com">Transcending CSS</a> - <a href="https://www.stuffandnonsense.co.uk">Andy Clarke</a>.</cite></blockquote>

One way of interpreting this is that floats and positions to establish sidebars and columns are, well, <em>layout hacks</em>. And though we really don't have an alternative, we hopefully will once a layout standard is agreed upon and browsers start supporting them. When that happens, it should be easy to swap out those hacked up box-model properties for ones intended for layout. Though it will be a while before new layout modules are here, using the right properties to handle layout instead of compensating for the quirks of our current limited set of properties will most certainly help condense page weight.</p>

## 6\. Document your work

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b7671e0-cc9a-467c-b359-4dd55cf15da3/figureg.jpg" alt="David Shea's markup guide at mezzoblue.com" width="630" height="378" /><br>
<em>David Shea's <a href="https://www.mezzoblue.com/downloads/markupguide/">markup guide</a> illustrates the proper usage for HTML tags and how those are represented on his site. Even sites without dynamic HTML can have this simple and effective guide (using its own CSS file, of course!) as a starting point of documentation.</em>

For a team of designers, it is extremely important to <strong>communicate regularly</strong> so that markup and style rules are created in a consistent way, and also to create site standards. For example, if someone comes up with way to markup a tab interface for the site, documentation will keep others from duplicating that effort, preventing code bloat in the HTML and CSS.

<strong>Documentation, including markup guides and style sheet guides</strong>, is not just for group efforts — they are just as important for a one-man design team. After all, a year after working on other things, revisiting one of your own projects can feel quite foreign. Your future self might appreciate reminder of how your CSS grid framework is supposed to work, or what pages already have a treatment for a secondary action form button, and it will save you or someone else from appending redundant and unnecessary rules to your CSS.

The choice to use documentation has a bonus side effect of being a great place to park explanations that otherwise must be included as CSS comments. <strong>CSS comments</strong> are great for sectioning off chunks of long CSS files, but verbose comments that are used to explain design choices can add to file size, and might be better suited to a markup and style guide. Documenting your code using CSS comments within your working file is most definitely better than nothing at all, but housing that material in separate documentation is a great way to keep the code focus and free from bloat.</p>

## 7\. Make use of compression

Some great applications have been created to compress and optimize CSS for you, allowing you to serve a human-unreadable but still browser-friendly files that are a fraction of the origional working copies. Applications like <a href="https://csstidy.sourceforge.net/">CSSTidy</a> and the <a href="https://developer.yahoo.com/yui/compressor/">YUI Compressor</a> can compress whitespace, detect and correct for CSS properties that are overwrite each other, and look for opportunites to use CSS shorthand that you may have missed. (These types of applications are excellent sources to read about, if for no other reason, to learn what things you can further do by hand).

Even popular text editors like BBEdit, TextMate, and TopStyle, can help format your CSS files to your liking. There are also options serve zip versions of your CSS files <a href="https://paulstamatiou.com/2007/03/18/how-to-optimize-your-css-even-more">using PHP</a>. You can find more CSS compressors and optimizers in the post <a href="https://www.smashingmagazine.com/2006/09/02/list-of-css-tools/">List of CSS Tools</a>.

It is important to note that these applications do their best to minimize errors, but they <strong>aren't always perfect</strong>. Also, they work best when browser hacks are not included in the file set (which is yet another reason to keep those hacks external).

There is one last type of application that can help prune CSS file size I'd like to mention. It can crawl a web site and log which CSS rules and declarations are <em>not</em> being applied, then bring these to your attention. Unfortunately, this tool hasn't been inventend yet, but I would gladly pay for such a application.

I can recall times when I've been afraid to delete certain rules because there is no documentation that explains to me that those selectors are leftover from previous iterations of development. If an app can bring those rules to my attention, that will help with maintenance and keeping CSS files lean.</p>

## Conclusion

<a href="https://www.smashingmagazine.com/2009/10/mastering-css-coding-getting-started/">Clean and optimized code</a> is important not just for file size, but for maintenance and readability as well. The principles mentioned above are good considerations not just for CSS, but can be applied to HTML, JavaScript, and other programming languages. CSS files are not as prominent as the rendering of your web site to an end-user, but consideration of the above principles can help with both the user experience (in the form of smaller file sizes) and the developer experience (cleaner code). Apply these principles to your current and future projects, and and you will surely appreciate the efforts.

