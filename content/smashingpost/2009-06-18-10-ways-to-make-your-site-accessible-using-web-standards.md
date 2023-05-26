---
title: 10 Ways To Make Your XHTML Site Accessible Using Web Standards
slug: 10-ways-to-make-your-site-accessible-using-web-standards
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13013bb9-055d-4978-b55a-9f55c3c39961/accessibility.jpg
date: 2009-06-18T12:23:05.000Z
author: michael-irigoyen
description: >-
  Without argument, one of the most important things to consider when creating a
  website is that it be accessible to everyone who wants to view it. Does your
  website play nice with screen readers? Can a user override your style sheet
  with a more accessible one and still see everything your website has to offer?
  Would another Web developer be embarrassed if they saw your code? If your
  website is standards-compliant, you could more confidently answer these
  questions.

  [![Accessibility](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d0f9959-a750-4b10-a928-45de9006b69a/accessibility.jpg)](https://www.smashingmagazine.com/2009/06/18/10-ways-to-make-your-site-accessible-using-web-standards/)

  Let’s take a look at **10 ways to improve the accessibility of your XHTML
  website by making it standards-compliant**. We'll go the extra mile and
  include criteria that fall beyond the standards set by the W3C but which you
  should follow to make your website more accessible. Each section lists the
  criteria you need to meet, explains why you need to meet them and gives
  examples of what you should and shouldn’t do.
categories:
  - Coding
  - XHTML
  - Standards
  - Accessibility
---
Without argument, one of the most important things to consider when creating a website is that it be accessible to everyone who wants to view it. Does your website play nice with screen readers? Can a user override your style sheet with a more accessible one and still see everything your website has to offer? Would another Web developer be embarrassed if they saw your code? If your website is standards-compliant, you could more confidently answer these questions.

You may want to take a look at the following related posts:

*   [Misunderstanding Markup: XHTML 2/HTML 5 Comic Strip](https://www.smashingmagazine.com/2009/07/misunderstanding-markup-xhtml-2-comic-strip/)
*   [Design Accessibly, See Differently: Color Contrast Tips And Tools](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/)
*   [10 Principles Of Effective Web Design](https://www.smashingmagazine.com/2008/01/10-principles-of-effective-web-design/)
*   [Bringing Interactivity To Your Website With Web Standards](https://www.smashingmagazine.com/2011/02/bringing-interactivity-to-your-website-with-web-standards/)

Let’s take a look at <strong>10 ways to improve the accessibility of your XHTML website by making it standards-compliant</strong>. We'll go the extra mile and include criteria that fall beyond the standards set by the W3C but which you should follow to make your website more accessible. Each section lists the criteria you need to meet, explains why you need to meet them and gives examples of what you should and shouldn’t do.</p>

## 1\. Specify The Correct DOCTYPE

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c33d878-c605-4c56-bf24-2b54d1ca9e1e/stepsix.png" alt="Specify the correct DOCTYPE" width="633" height="135" />

{{% feature-panel %}}

<strong>Criteria.</strong>
The Document Type declaration (DOCTYPE) is an instruction that sits at the top of your document. The DOCTYPE is required to tell the browser how to correctly display your page.

<strong>Why do I need it?</strong>
Without a proper DOCTYPE declaration, the browser tries to automatically assign a DOCTYPE to the page. This can slow down the rendering of your page and cause the page to be displayed inconsistently or incorrectly in different browsers. Consistency is the name of the game when it comes to accessibility.

<strong>Okay, so what do I do?</strong>
Include a proper DOCTYPE at the top of each page of your website. XHTML 1.1 is recommended, but XHTML 1.0 Strict is an option as well.

*   **XHTML 1.1**.  This is the cleanest way to code your website. All style for the website is contained in external CSS files. Be sure to add the XML declaration at the top, which is essential because XHTML 1.1 is considered to be true XML.

        <?xml version="1.0" encoding="UTF-8"?>
        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "https://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

    **Note:** if you are using XHTML 1.1, you cannot include the XML declaration for visitors who are using Internet Explorer 6\. Instead, to support IE6 users, you should conditionally display the XML declaration.
*   **XHTML 1.0 Strict**.  An alternative to XHTML 1.1\. The technical differences between the two are minor, but using XHTML 1.1 is recommended to accommodate future website growth.

        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "https://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

Two other XHTML 1.0 declarations exist for niche uses. But using either of these DOCTYPEs is discouraged.

*   **XHTML 1.0 Transitional**.  This is used for pages that need to be viewed on legacy browsers that don’t support CSS. Transitional allows inline styles to be applied to elements.

        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

*   **XHTML 1.0 Frameset**.  Use Frameset only on websites that require HTML frames. Of course, static CSS divisions should be used instead of HTML frames, right?

        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"
        "https://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">

## 2\. Define The Namespace And Default Language

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/610a6598-643d-462b-afc4-8cb349f12aff/steptwo.png" alt="Define the Namespace and Default Language" width="633" height="135" />

<strong>Criteria.</strong>
The XHTML namespace and default language of your page must be included in the <code>&lt;html&gt;</code> element.

<strong>Why do I need it?</strong>
XHTML websites should define the default namespace. A namespace defines all of the elements you can use within the page. Setting a default language allows a screen reader to tell the visitor which language the page is in without even seeing the content. It is also required by W3C standards.

<strong>Okay, so what do I do?</strong>
Append the <tt>xmlns</tt> and <tt>lang</tt> attributes to the <code>&lt;html&gt;</code> element. In XHTML 1.1, the <tt>lang</tt> attribute is <tt>xml:lang</tt>.

*   **XHTML 1.1**

        <html xmlns="https://www.w3.org/1999/xhtml" xml:lang="en">

*   **XHTML 1.0**

        <html xmlns="https://www.w3.org/1999/xhtml" lang="en">

## 3\. Supply Proper Meta Tags

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abb7dc36-6697-4166-a6e9-a407f49504d4/stepthree.png" alt="Supply proper Meta tags" width="633" height="135" />

<strong>Criteria.</strong>
Supply the <tt>http-equiv</tt>, <tt>language</tt>, <tt>description</tt> and <tt>keywords</tt> meta tags in the <tt>&lt;head&gt;</tt> element on your page.

<strong>Why do I need it?</strong>
The <tt>http-equiv</tt> meta tag is by far the most important. Used in conjunction with the DOCTYPE, it helps the browser display your page correctly. The <tt>language</tt> meta tag is important for non-English websites, but it has become common practice to include it on every page, despite the language. The <tt>description</tt> and <tt>keywords</tt> meta tags are required more for accessibility than to meet standards because they are commonly used by screen readers.

<strong>Okay, so what do I do?</strong>
Include these four meta tags in the <code>&lt;head&gt;</code> element on your page.

<pre><code class="language-php">&lt;meta http-equiv="content-type" content="text/html; charset=utf-8" /&gt;
&lt;meta name="language" content="en" /&gt;
&lt;meta name="description" content="Updating Windows using Microsoft Update" /&gt;
&lt;meta name="keywords" content="updating, windows, microsoft, update, techworld" /&gt;</code></pre>

Make sure the language you specify in the <code>&lt;html&gt;</code> element is the same one you define in the <tt>language</tt> meta tag. Also, if you are using XHTML 1.1, make sure the <tt>encoding</tt> specification in the XML declaration matches the <tt>charset</tt> in the <tt>http-equiv</tt> meta tag.

## 4\. Use Accessible Navigation

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577903ae-1ee7-4733-a745-f0b4ca6bc9c8/stepfour.png" alt="Use accessible navigation" width="633" height="135" />

<strong>Criteria.</strong>
Allow users to easily identify what page and sub-section of a page they are viewing.

<strong>Why do I need it?</strong>
A majority of websites today use a combination of text, colors and graphic styles to organize and display information. Many people with disabilities cannot see or use graphics and thus rely on screen readers, custom style sheets and other accessibility tools to retrieve information. Regardless of who visits your website, implementing an accessible navigation system helps them quickly and accurately find the information they are looking for.

<strong>Okay, so what do I do?</strong>
Create a descriptive title for your website, and then split the page into sub-sections using the heading elements.

*   Include exactly one `<title>` element within the `<head>` element:

        <title>Smashing Magazine</title>

*   Include exactly one `<h1>` element on the page. The `<h1>` element should match all or part of your `<title>` element:

        <h1>Smashing Magazine: We smash you with the information that makes your life easier. Really!</h1>

*   All heading tags (`<h1>`, `<h2>`, etc.) should have textual content. <tt>Alt</tt> tags on images do not count. **Incorrect:**

        <h2><img loading="lazy" decoding="async" src="logo.png" alt="Smashing Magazine" /></h2>

    **Correct:**

        <h2><img loading="lazy" decoding="async" src="logo.png" alt="Smashing Magazine" />Smashing Magazine</h2>

## 5\. Properly Escape JavaScript

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ac7fa5f-bc40-4810-9a49-543a2763cd24/stepfive.png" alt="Properly escape JavaScript" width="633" height="135" />

<strong>Criteria.</strong>
When including JavaScript directly on the page, you should properly escape it as character data.

<strong>Why do I need it?</strong>
In HTML, text in the <code>&lt;script&gt;</code> element is rendered as CDATA (character data). In XHTML, text in the <code>&lt;script&gt;</code> element is treated as PCDATA (parsed character data). PCDATA is processed by the W3C validator and, therefore, must be escaped properly as CDATA. In addition, while most screen readers are intelligent enough to ignore content within the <code>&lt;script&gt;</code> element, regardless of the type of data it contains, if the code isn't correctly escaped, another potential point of failure is created in accessibility.

<strong>Okay, so what do I do?</strong>
Use the CDATA tags around any content in the <code>&lt;script&gt;</code> element. We also comment out the CDATA tags for legacy browser support.

<strong>Example:</strong>

<pre><code class="language-php">&lt;script type="text/javascript"&gt;
//&lt;![CDATA[
$(function() {
$('#divone').tipsy({fade: true, gravity: 'n'});
$('#divtwo').tipsy({fade: true, gravity: 'n'});
});
//]]&gt;
&lt;/script&gt;</code></pre>

## 6\. Properly Escape HTML Entities

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c33d878-c605-4c56-bf24-2b54d1ca9e1e/stepsix.png" alt="Properly escape HTML entities" />

<strong>Criteria.</strong>
Ampersands, quotes, greater- and less-than signs and other HTML must be escaped.

<strong>Why do I need it?</strong>
Using HTML entities, especially in URLs, can cause not only validation problems but also usability problems. For example, the ampersand (&amp;) happens to be the initial character in HTML entities. If you do not properly escape the ampersand, the browser assumes you are telling it to show an HTML entity, one that doesn't even exist.

<strong>Okay, so what do I do?</strong>
Escape HTML entities with their appropriate entity value.

*   Replace & with &amp;
*   Replace " with &quot;
*   Replace < with &lt;
*   Replace > with &gt;
*   [Other HTML entities](https://htmlhelp.com/reference/html40/entities/special.html)

<strong>Example:</strong>

<pre><code class="language-php">&lt;a href="https://www.example.com?page=1&amp;amp;view=top"&gt;A &amp;quot;Cool&amp;quot; Link&lt;/a&gt;
&lt;code&gt;&amp;lt;div id=&amp;quot;content&amp;quot;&amp;gt;Test information.&amp;lt;/div&amp;gt;&lt;/code&gt;</code></pre>

## 7\. Use Only Lowercase Tags And Attributes

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20e7cd79-0663-452f-949e-041ac48718f3/stepseven.png" alt="Use only lowercase tags and attributes" width="633" height="135" />

<strong>Criteria.</strong>
All elements and element attributes must be lowercase. Attribute values can be both uppercase and lowercase.

<strong>Why do I need it?</strong>
Because the XHTML standard set by the W3C <a href="https://www.w3.org/TR/xhtml1/#h-4.2">says so</a>.

<strong>Okay, so what do I do?</strong>
Make sure you use only lowercase for all elements and attributes. A common mistake most developers make is using uppercase letters when giving an element JavaScript attributes (e.g. onClick, onLoad, etc.).

<strong>Incorrect:</strong>

<pre><code class="language-php">&lt;A href="#" onClick="doSomething();"&gt;Send us a message&lt;/A&gt;</code></pre>

<strong>Correct:</strong>

<pre><code class="language-php">&lt;a href="#" onclick="doSomething();"&gt;Send us a message&lt;/a&gt;</code></pre>

## 8\. Label All Form Input Elements

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31677b9f-8a98-437a-a174-cd71a67e4d2b/stepeight.png" alt="Label all form input elements" width="633" height="135" />

<strong>Criteria.</strong>
All form elements should be given a <code>&lt;label&gt;</code> tag.

<strong>Why do I need it?</strong>
The <code>&lt;label&gt;</code> element adds functionality for people who use the mouse and a screen reader. Clicking on text within the <code>&lt;label&gt;</code> element focuses the corresponding form element. Screen readers can read the label so that visitors know what information to provide.

<strong>Okay, so what do I do?</strong>
Add a <code>&lt;label&gt;</code> element to each field in your form.

<strong>Example:</strong>

<pre><code class="language-php">&lt;p&gt;&lt;label for="searchbox"&gt;Search: &lt;/label&gt;&lt;input type="text" id="searchbox" /&gt;&lt;/p&gt;
&lt;p&gt;&lt;input type="checkbox" id="remember" /&gt;&lt;label for="remember"&gt; Remember&lt;/label&gt;&lt;/p&gt;</code></pre>

## 9\. Supply Alternative Content For Images

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dfe6b96-069e-4d76-86fc-46d01342cf25/stepnine.png" alt="Supply alternative content for images" width="633" height="135" />

<strong>Criteria.</strong>
Every image on your page should be accompanied by a textual alt tag.

<strong>Why do I need it?</strong>
The alt tag tells visitors what an image is if it cannot be displayed or viewed. The Americans with Disabilities Act dictates that all images must have an alt tag.

<strong>Okay, so what do I do?</strong>
Include one with every image. The alt <del>tag</del> attribute must include text and cannot be left blank. If you use images in your design for stylistic reasons alone, find a way to achieve that style using CSS. And don't forget to provide explicit values for width and height of your images.

<strong>Incorrect:</strong>

<pre><code class="language-php">&lt;img src="picture.png" /&gt;
&lt;img src="spacer.gif" alt="" /&gt;</code></pre>

<strong>Correct:</strong>

<pre><code class="language-php">&lt;img src="picture.png" alt="A warm sunset" width="450" height="350" /&gt;</code></pre>

## 10\. Use The "id" And "class" CSS Attributes Correctly

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8d2ed74-25d9-4c5b-a64c-a1ce9bfaf7e6/stepten.png" alt="Correctly use CSS attributes &quot;id&quot; and &quot;class&quot;" width="633" height="135" />

<strong>Criteria.</strong>
When using CSS attributes, use each "id" only once on a page. Use each "class" as much as you want.

<strong>Why do I need it?</strong>
Developers often get careless and include an "id" multiple times on a single page. This can create unexpected results across different browsers and get you a big red "Validation Failed" from the W3C.

<strong>Okay, so what do I do?</strong>
Be certain to use a particular "id" only once on a page. If you need the same style applied to mutliple elements, use the "class" attribute.

<strong>Incorrect:</strong>

<pre><code class="language-php">&lt;p id="leftNav"&gt;Home&lt;/p&gt;
&lt;p id="leftNav"&gt;Contact&lt;/p&gt;</code></pre>

<strong>Correct:</strong>

<pre><code class="language-php">&lt;p id="homeNav" class="leftNav"&gt;Home&lt;/p&gt;
&lt;p id="contactNav" class="leftNav"&gt;Contact&lt;/p&gt;</code></pre>

## Summary: Validate, Validate, Validate!

Using all the techniques in this article, you'll be well on your way to a more accessible, standards-compliant website. But don't stop there! Continually validate your website and address problems immediately. Here is a list of validators you should run on every page you create:

*   [W3C Markup Validation Service](https://validator.w3.org/)
*   [W3C CSS Validation Service](https://jigsaw.w3.org/css-validator/)
*   [HiSoftware Cynthia Says Accessibility Validation](https://www.cynthiasays.com/)
*   Functional Accessibility Evaluator

{{< signature "al" >}}

