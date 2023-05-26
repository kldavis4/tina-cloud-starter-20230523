---
title: '!important CSS Declarations: How and When to Use Them'
slug: the-important-css-declaration-how-and-when-to-use-it
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc9c98c0-f4dc-444a-bb36-1fa13a53196a/70expert.png
date: 2010-11-02T12:42:08.000Z
author: louis-lazaris
description: >-
  When the CSS1 specification was
  drafted in the mid to late 90s, it introduced `!important` declarations that
  would help developers and users easily override normal specificity when making
  changes to their stylesheets. For the most part, `!important` declarations
  have remained the same, with only one change in CSS2.1 and nothing new added
  or altered in the CSS3 spec in connection with this unique declaration.
categories:
  - Coding
  - CSS
  - Essentials
---
When the <a href="https://www.w3.org/TR/REC-CSS1-961217">CSS1 specification</a> was drafted in the mid to late 90s, it introduced <code>!important</code> declarations that would help developers and users easily override normal specificity when making changes to their stylesheets. For the most part, <code>!important</code> declarations have remained the same, with only one change in CSS2.1 and nothing new added or altered in the CSS3 spec in connection with this unique declaration. 

## <span class="rh">Further Reading</span> on SmashingMag:

*   [CSS Specificity And Inheritance](https://www.smashingmagazine.com/2010/04/css-specificity-and-inheritance/)
*   [Mastering CSS Principles: A Comprehensive Guide](https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/)
*   [CSS Specificity: Things You Should Know](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/)
*   [CSS Inheritance, The Cascade And Global Scope](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/)

<p>Let's take a look at <strong>what exactly these kinds of declarations are all about</strong>, and when, if ever, you should use them.</p>

## A Brief Primer on the Cascade

Before we get into <code>!important</code> declarations and exactly how they work, let's give this discussion a bit of context. In the past, Smashing Magazine has covered <a href="https://www.smashingmagazine.com/2010/04/07/css-specificity-and-inheritance/">CSS specificity</a> in-depth, so please take a look at that article if you want a detailed discussion on the CSS cascade and how specificity ties in.

{{% feature-panel %}}

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceba84b1-161d-4a43-af90-51d34579125d/overriding-styles-2.jpg" alt="Adding !important CSS in Developer Tools" width="500" height="224" />

Below is a basic outline of how any given CSS-styled document will decide how much weight to give to different styles it encounters. This is a general summary of <a href="https://www.w3.org/TR/CSS21/cascade.html#cascade">the cascade</a> as discussed in the spec:

*   Find all declarations that apply to the element and property
*   Apply the styling to the element based on importance and origin using the following order, with the first item in the list having the least weight:
    *   Declarations from the user agent
    *   Declarations from the user
    *   Declarations from the author
    *   Declarations from the author with `!important` added
    *   Declarations from the user with `!important` added
*   Apply styling based on specificity, with the more specific selector "winning" over more general ones
*   Apply styling based on the order in which they appear in the stylesheet (i.e., in the event of a tie, last one "wins")

With that basic outline, you can probably already see how <code>!important</code> declarations weigh in, and what role they play in the cascade. Let's look at <code>!important</code> in more detail.</p>

## What is Important CSS?

An <code>!important</code> declaration provides a way for a stylesheet author to give a CSS value <strong>more weight</strong> than it naturally has.</p>

## Syntax and Description

It should be noted here that the phrase "!important declaration" is a reference to an entire CSS declaration, including property and value, with <code>!important</code> added (thanks to Brad Czerniak for pointing out this discrepancy). Here is a simple code example that clearly illustrates how <code>!important</code> affects the natural way that styles are applied:

<pre><code class="language-css">#example {
	font-size: 14px !important;	
}

#container #example {
	font-size: 10px;
}</code></pre>

In the above code sample, the element with the id of "example" will have text sized at 14px, due to the addition of <code>!important</code>.

Without the use of <code>!important</code>, there are two reasons why the second declaration block should naturally have more weight than the first: The second block is later in the stylesheet (i.e. it's listed second). Also, the second block has more specificity (<code>#container</code> followed by <code>#example</code> instead of just <code>#example</code>). But with the inclusion of <code>!important</code>, the first <code>font-size</code> rule now has more weight.

Some things to note about <code>!important</code> declarations:

*   When `!important` was first introduced [in CSS1](https://www.w3.org/TR/REC-CSS1-961217#important), an author rule with an `!important` declaration held more weight than a user rule with an `!important` declaration; to improve accessibility, this [was reversed in CSS2](https://www.w3.org/TR/CSS2/cascade.html#important-rules)
*   If `!important` is used on a shorthand property, this adds "importance" to all the sub-properties that the shorthand property represents
*   The `!important` keyword (or statement) must be placed at the end of the line, immediately before the semicolon, otherwise it will have no effect (although a space before the semicolon won't break it)
*   If for some particular reason you have to write the same property twice in the same declaration block, then add `!important` to the end of the first one, the first one will have more weight in every browser except IE6 (this works as an IE6-only hack, but doesn't invalidate your CSS)
*   In IE6 and IE7, if you use a different word in place of `!important` (like `!hotdog`), the CSS rule will still be given extra weight, while other browsers will ignore it

## When Should !important Be Used?

As with any technique, there are pros and cons depending on the circumstances. So when should it be used, if ever? Here's my subjective overview of potential valid uses.</p>

### Never

<code>!important</code> declarations <strong>should not be used unless they are absolutely necessary</strong> after all other avenues have been exhausted. If you use <code>!important</code> out of laziness, to avoid proper debugging, or to rush a project to completion, then you're abusing it, and you (or those that inherit your projects) will suffer the consequences.

If you include it even sparingly in your stylesheets, you will soon find that certain parts of your stylesheet will be harder to maintain. As discussed above, CSS property importance happens naturally through the cascade and specificity. When you use <code>!important</code>, <strong>you're disrupting the natural flow</strong> of your rules, giving more weight to rules that are undeserving of such weight.

If you never use <code>!important</code>, then that's a sign that you understand CSS and give proper forethought to your code before writing it.

That being said, the old adage "never say never" would certainly apply here. So below are some legitimate uses for <code>!important</code>.</p>

### To Aid or Test Accessibility

As mentioned, user stylesheets can include <code>!important</code> declarations, allowing <strong>users with special needs</strong> to give weight to specific CSS rules that will aid their ability to read and access content.

A special needs user can add <code>!important</code> to typographic properties like <code>font-size</code> to make text larger, or to color-related rules in order to increase the contrast of web pages.

In the screen grab below, Smashing Magazine's home page is shown with a user-defined stylesheet overriding the normal text size, which can be done using Firefox's Developer Toolbar:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1655dedf-2e55-4fc4-86c1-71c0431b5219/screen-grab-below1.jpg" alt="User Style Sheet Added to Smashing Magazine" width="450" height="443" />

In this case, the text size was adjustable without using <code>!important</code>, because a user-defined stylesheet will override an author stylesheet regardless of specificity. If, however, the text size for body copy was set in the author stylesheet using an <code>!important</code> declaration, the user stylesheet could not override the text-size setting, even with a more specific selector. The inclusion of <code>!important</code> resolves this problem and <strong>keeps the adjustability of text size within the user's power</strong>, even if the author has abused <code>!important</code>.</p>

### To Temporarily Fix an Urgent Problem

There will be times when something bugs out in your CSS on a live client site, and you need to apply a fix very quickly. In most cases, you should be able to use Firebug or another developer tool to track down the CSS code that needs to be fixed. But if the problem is occurring on IE6 or another browser that doesn't have access to debugging tools, you may need to do a quick fix using <code>!important</code>.

After you move the temporary fix to production (thus making the client happy), you can work on fixing the issue locally using a more maintainable method that doesn't muck up the cascade. When you've figured out a better solution, you can add it to the project and remove <code>!important</code> — and the client will be none the wiser.</p>

### To Override Styles Within Firebug or Another Developer Tool

Inspecting an element in Firebug or Chrome's developer tools allows you to edit styles on the fly, to test things out, debug, and so on — without affecting the real stylesheet. Take a look at the screen grab below, showing some of Smashing Magazine's styles in Chrome's developer tools:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01e1d3f6-66a3-4520-9c7a-b8358d68e3ac/overriding-styles.jpg" alt="Overriding Styles in Chrome's Developer Tools" width="500" height="232" />

The highlighted background <strong>style rule has a line through it</strong>, indicating that this rule has been overridden by a later rule. In order to reapply this rule, you could find the later rule and disable it. You could alternatively edit the selector to make it more specific, but this would give the entire declaration block more specificity, which might not be desired.

<code>!important</code> could be added to a single line to give weight back to the overridden rule, thus allowing you to test or debug a CSS issue without making major changes to your actual stylesheet until you resolve the issue.

Here's the same style rule with <code>!important</code> added. You'll notice the line-through is now gone, because <strong>this rule now has more weight</strong> than the rule that was previously overriding it:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceba84b1-161d-4a43-af90-51d34579125d/overriding-styles-2.jpg" alt="Adding !important in Developer Tools" width="500" height="224" />

### To Override Inline Styles in User-Generated Content

One frustrating aspect of CSS development is when user-generated content includes inline styles, as would occur with some WYSIWYG editors in CMSs. In the CSS cascade, <strong>inline styles will override regular styles</strong>, so any undesirable element styling that occurs through generated content will be difficult, if not impossible, to change using customary CSS rules. You can circumvent this problem using an <code>!important</code> declaration, because a CSS rule with <code>!important</code> in an author stylesheet will override inline CSS.</p>

### For Print Stylesheets

Although this wouldn't be necessary in all cases, and might be discouraged in some cases for the same reasons mentioned earlier, you could add <code>!important</code> declarations to your print-only stylesheets to help override specific styles without having to repeat selector specificity.</p>

### For Uniquely-Designed Blog Posts

If you've dabbled in uniquely-designed blog posts (many designers <a href="https://www.alistapart.com/articles/art-direction-and-design/">take issue</a> with using "art direction" for this technique, and rightly so), as showcased on <a href="https://heartdirected.com/">Heart Directed</a>, you'll know that such an undertaking requires each separately-designed article to have its own stylesheet, or else you need to use inline styles. You can give an individual page its own styles using the code presented <a href="https://digwp.com/2010/02/custom-css-per-post/">in this post</a> on the Digging Into Wordpress blog.

The use of <code>!important</code> could come in handy in such an instance, allowing you to easily override the default styles in order to create a unique experience for a single blog post or page on your site, without having to worry about natural CSS specificity.</p>

## Conclusion

<code>!important</code> declarations are best reserved for special needs and users who want to make web content more accessible by easily overriding default user agent or author stylesheets. So you should do your best to give your CSS proper forethought and <strong>avoid using <code>!important</code> wherever possible</strong>. Even in many of the uses described above, the inclusion of <code>!important</code> is not always necessary.

Nonetheless, <code>!important</code> is valid CSS. You might inherit a project wherein the previous developers used it, or you might have to patch something up quickly — so it could come in handy. It's certainly beneficial to understand it better and be prepared to use it should the need arise.

Do you ever use <code>!important</code> in your stylesheets? When do you do so? Are there any other circumstances you can think of that would require its use?

## Further Resources

*   [!important rules in the CSS2.1 spec](https://www.w3.org/TR/CSS2/cascade.html#important-rules)
*   [!important Declarations on SitePoint's CSS Reference](https://reference.sitepoint.com/css/importantdeclarations)
*   [CSS Specificity And Inheritance on Smashing Magazine](https://www.smashingmagazine.com/2010/04/07/css-specificity-and-inheritance/)
*   [Everything You Need to Know About !important CSS Declarations](https://www.impressivewebs.com/everything-you-need-to-know-about-the-important-css-declaration/)
*   [What are the implications of using "!important" in CSS?](https://stackoverflow.com/questions/3706819/what-are-the-implications-of-using-important-in-css/)
