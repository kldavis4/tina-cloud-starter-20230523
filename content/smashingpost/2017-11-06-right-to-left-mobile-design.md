---
title: Right-To-Left Development In Mobile Design
slug: right-to-left-mobile-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37f90b6c-ae56-49a6-83a6-25309c55e482/22-right-to-left-development-for-mobile-design-800w-opt-2.png
date: 2017-11-06T19:04:21.000Z
author: robertdodis
description: >-
  The Middle Eastern market is growing at a rapid pace, and, as a result, demand
  for IT products is also booming in the region. What is peculiar, though, is
  that Middle Eastern countries require design that is not only compatible with
  their needs and comfortable for their users, but that is also suitable to
  their language standards, making a serious adaptation process very important.
  Given that most languages spoken in the Middle East are written and read from
  right to left (such as
  [Arabic](https://www.smashingmagazine.com/2014/03/taking-a-closer-look-at-arabic-calligraphy/),
  Hebrew, and Urdu), developers often face a range of problems when creating
  products in those languages.
categories:
  - Mobile
  - User Interaction
  - Web Design
  - UX
---
The Middle Eastern market is growing at a rapid pace, and, as a result, demand for various IT products is also booming in the region. What is peculiar, though, is that Middle Eastern countries require design that is not only compatible with their needs and comfortable for their users, but that is also suitable to their language standards, making a serious adaptation process very important. Given that most languages spoken in the Middle East are written and read from right to left (such as [Arabic](https://www.smashingmagazine.com/2014/03/taking-a-closer-look-at-arabic-calligraphy/), Hebrew and Urdu), developers often face a range of problems when creating products in those languages.

Although this might seem like not that big of a deal, IT development for right-to-left (RTL) languages entails paying attention to a number of peculiarities. This is only further complicated by the fact that the RTL market is relatively new, and not many resources are available to help developers.

Our experience with RTL development has enabled us to compile a thorough list of tips that are useful for anyone developing an RTL product (such as a website or mobile app). By following the tips closely, you should be able to navigate the challenging waters of RTL development and deliver a functional, user-friendly result.</p>

## Flipping The Interface

First and foremost, the interface must be flipped from right to left. You might think this is rather “D’uh” advice, but we simply could not disregard it, because it is in fact the very first thing to do.

{{% feature-panel %}}

Here’s an example of Facebook’s left-to-right (LTR) design:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e7abb90-88b8-4781-bf9d-516600b5cc26/23-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd2d0934-f763-4070-b9b9-996aee9c94b5/23-right-to-left-development-for-mobile-design-800w-opt-2.png" width="800" height="421" alt="" /></a><figcaption>Facebook’s log-in page in LTR design. (Image source: <a href="https://www.facebook.com/">Facebook</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e7abb90-88b8-4781-bf9d-516600b5cc26/23-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

And here is the RTL version of Facebook:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb321480-c50c-42e4-a122-dd869dca7c9d/22-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37f90b6c-ae56-49a6-83a6-25309c55e482/22-right-to-left-development-for-mobile-design-800w-opt-2.png" width="800" height="421" alt="" /></a><figcaption>Facebook’s log-in page in RTL design. (Image source: <a href="https://www.facebook.com/">Facebook</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb321480-c50c-42e4-a122-dd869dca7c9d/22-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

There are several ways to achieve this.</p>

### 1. Using the dir Attribute or CSS

If the basic markup is built with floating blocks, it will look something like the example below.

For **LTR** design, pay attention to the styles. In this case, the link with logo will be fixed to the left, with the `login-container` to the right.</p>

<pre><code class="language-html">
    &lt;!doctype html&gt;
    &lt;html lang="en"&gt;
        &lt;head&gt;
            &lt;meta charset="utf-8"&gt;
            &lt;title&gt;Example&lt;/title&gt;
            &lt;style&gt;
                .float-left{
                float: left;
                }
                .float-right{
                float: right;
                }
                body[dir="rtl"] .float-left{
                float: right;
                }
                body[dir="rtl"] .float-right{
                float: left;
                }
            &lt;/style&gt;
        &lt;/head&gt;
        &lt;body&gt;
            &lt;header class="clearfix"&gt;
                &lt;a href="#" class="float-left logo"&gt;&lt;img src="static/logo.png"&gt;&lt;/a&gt;
            &lt;nav class="float-right login-container"&gt;&lt;/nav&gt;
        &lt;/header&gt;
    &lt;main&gt;&lt;/main&gt;
    &lt;footer&gt;&lt;/footer&gt;
    &lt;/body&gt;
    &lt;/html&gt;
    </code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dc85cec-de38-4b65-b73e-b404b960513c/11-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e6ecc0c-f492-48ec-86bb-4545a5261984/11-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="74" alt="" /></a><figcaption>Facebook’s top log-in bar in LTR design. (Image source: <a href="https://www.facebook.com/">Facebook</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dc85cec-de38-4b65-b73e-b404b960513c/11-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

For **RTL** design, once you’ve assigned the `body` tag to the `dir="rtl` attribute, the whole markup will be mirrored, placing the logo to the right and `login-container` to the left. The opposite properties will be then applied to blocks with the `float-left` or `float-right` class.</p>

<pre><code class="language-html">&lt;body dir="ltr"&gt;</code></pre>

The `dir` attribute specifies the text’s direction and display (either left to right or right to left). Normally, browsers recognize the direction because it’s assigned in the Unicode character set, but with the `dir` attribute, you can set whatever direction you want.

The possible variants are `dir="ltr"`, `dir="rtl"` and `dir="auto"`. This attribute can also be rewritten with the CSS `direction` property.

Because text direction is semantically tied to content and not to presentation, we recommend that, whenever possible, web developers use the `dir` attribute and not the CSS properties related to it. That way, the text will be displayed properly even in browsers that don’t support CSS (or in those where CSS support is turned off).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaced403-93aa-487f-863b-79d800e66ce4/12-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9360fd9-e671-4d30-9217-212334dfa3cf/12-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="74" alt="" /></a><figcaption>Facebook’s top log-in bar in RTL design. (Image source: <a href="https://www.facebook.com/">Facebook</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaced403-93aa-487f-863b-79d800e66ce4/12-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

With this attribute, you can horizontally mirror images, reassign fonts, align text to either side of the page, etc. However, the manual way is fairly labor-intensive. There are tools to automate the assembly of RTL styles, which we’ll get to a bit later in this post. In the meantime, we’ll describe another way of dealing with markup directional changes.</p>

### 2. Using Flexbox

Flexbox is popular among developers for a couple of good reasons. Not only does it provide flexibility when adjusting the alignment of page elements and other bits, but it also eliminates the need to reassign styles for RTL development. See the code snippets below for more details.

For **LTR**:

<pre><code class="language-html">
    &lt;div class="flex-container"&gt;
        &lt;div class="flex-item"&gt;1&lt;/div&gt;
        &lt;div class="flex-item"&gt;2&lt;/div&gt;
        &lt;div class="flex-item"&gt;3&lt;/div&gt;
    &lt;div&gt;
    </code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf63f005-df4a-4c38-8e02-b6f40fe43203/14-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ac4d574-72e5-465e-b73a-3d89169b53e3/14-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="416" alt="" /></a><figcaption>An example of flexbox layout in LTR design. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf63f005-df4a-4c38-8e02-b6f40fe43203/14-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

For **RTL**:

<pre>    <code class="language-html">
    &lt;div class="flex-container" style="direction: ltr;"&gt;
        &lt;div class="flex-item"&gt;1&lt;/div&gt;
        &lt;div class="flex-item"&gt;2&lt;/div&gt;
        &lt;div class="flex-item"&gt;3&lt;/div&gt;
    &lt;div&gt;
    </code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8826fa3-58ea-401d-80ba-29808eb43bc0/13-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38278ca2-7c5f-4413-aa7b-d4fafa4c6690/13-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="416" alt="" /></a><figcaption>An example of flexbox layout in RTL design. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8826fa3-58ea-401d-80ba-29808eb43bc0/13-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

The grid layout is also useful here. We set `grid-template-areas` in the containing block with `{display: grid;} property` (imagine it as a table with two columns and three rows). From the top: The header occupies the entire width of the screen, the sidebar is on the left, while the main content and the footer are on the right, one under another.

For **LTR**:

<pre><code class="language-html">
    &lt;div class="grid" 
    style="grid-template-areas: "header  header";
    "sidebar main"
    "sidebar footer";"&gt;
        &lt;div class="item-1" style="grid-area: header;"&gt;header&lt;/div&gt;
        &lt;div class="item-2" style="grid-area: sidebar;"&gt;sidebar&lt;/div&gt;
        &lt;div class="item-3" style="grid-area: main;"&gt;main&lt;/div&gt;
        &lt;div class="item-4" style="grid-area: footer;"&gt;footer&lt;/div&gt;
    &lt;/div&gt;
    </code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fed5225-bb45-48df-b0bb-8a670059db95/15-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fed5225-bb45-48df-b0bb-8a670059db95/15-right-to-left-development-for-mobile-design-preview-opt.png" width="700" height="544" alt="" /></a><figcaption>An example of basic direction of grid layout in LTR design. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

For **RTL**, by changing the `dir` attribute, the horizontal axis with the `grid` class and the `{display: grid;}` property will adjust to the specified direction. The layout matrix is then inverted:

<pre><code class="language-html">
    &lt;div class="grid" 
    style="grid-template-areas: "header header"
    "sidebar main"
    "sidebar footer"; 
    dir="rtl"&gt;
        &lt;div class="item-1" style="grid-area: header;"&gt;header&lt;/div&gt;
        &lt;div class="item-2" style="grid-area: sidebar;"&gt;sidebar&lt;/div&gt;
        &lt;div class="item-3" style="grid-area: main;"&gt;main&lt;/div&gt;
        &lt;div class="item-4" style="grid-area: footer;"&gt;footer&lt;/div&gt;
    &lt;/div&gt;
    </code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4fe3437-ffbc-45f2-a5b7-1141fcbddaa8/16-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4fe3437-ffbc-45f2-a5b7-1141fcbddaa8/16-right-to-left-development-for-mobile-design-preview-opt.png" width="700" height="544" alt="" /></a><figcaption>An example of inverted grid layout matrix in RTL design. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

Even though using tables to build layouts hasn’t been popular for a while now, they would still build flow direction as a component, just like in the previous examples, meaning that when you add the `dir="rtl"` tag, columns will start from the right and move from right to left. All table elements will follow this, unless the direction is clearly predefined beforehand.

## Character Encoding

Save your file using a character encoding that includes the characters you need (UTF-8 is a good bet). Declare that you are going to use such characters in the `head` tag of your HTML page with:

<pre><code class="language-html">&lt;meta charset="utf-8"/&gt;
    </code></pre>

**UTF-8** is a character encoding capable of encoding all possible Unicode code points, and it covers almost all languages, characters and punctuation symbols. Using UTF-8 also removes the need for server-side logic when individually determining each page’s character encoding or each incoming form submission. Coding helps to convert everything into binary numbers. For instance, “hello” in UTF-8 would be stored like this (in binary): `01101000 01100101 01101100 01101100 01101111`.</p>

## Formatted Text

Try as hard as you can to avoid using **bold** and _italics_. Bold text would make readability extremely difficult in most RTL languages (especially Arabic), and italics is simply never used. As well, capital letters are almost always disregarded in RTL languages.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788f09fe-f5aa-41ab-b2fe-589c6128f132/hello-world.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788f09fe-f5aa-41ab-b2fe-589c6128f132/hello-world.png" width="800" height="117" alt="" /></a><figcaption>An example of omitting capital letters in RTL languages. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788f09fe-f5aa-41ab-b2fe-589c6128f132/hello-world.png">View large version</a>)
</figcaption></figure>

If you need to highlight a certain part of text in Arabic, overline it instead of underlining, interspacing or italicizing. Here is how we do it:

<pre><code class="language-html">&lt;h1&gt;مثال&lt;/h1&gt;
    h1 {
        text-decoration: overline;
    }
    </code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de5e2d70-6898-46c0-bf68-a8422e745d87/03-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de5e2d70-6898-46c0-bf68-a8422e745d87/03-right-to-left-development-for-mobile-design-preview-opt.png" width="343" height="301" alt="" /></a><figcaption>An example of overlining Arabic text. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

Make sure that all text is aligned to the right, and that font and font size are adjusted properly (better yet, customize them), because Latin fonts tend to affect Arabic readability rather poorly.

Actually, the best way to deal with fonts is to speak to your client (assuming, of course, they speak the language). The thing is that languages such as Arabic tend to have a great number of spoken and written variations, and if you’re making a product catered specifically to some region, it should really display the language version used there. If you find this matter interesting, information about the history of Arabic writing systems is available [here](https://www.academia.edu/910536/Arabic_script_and_typography_A_brief_historical_overview_2002_).

In case your client isn’t a native speaker of the product’s language or isn’t able to help you, there is always the simple option of using one of the [Google Noto](https://www.google.com/get/noto/) fonts (there is one for every language, and all of them are free). Alternatively, Arabnet recommends [10 Arabic fonts](https://news.arabnet.me/best-web-fonts-arabic-text-screens/) (the list is from 2014, but things haven’t changed much in this area over the last three years). However, do keep in mind that your client always knows best which language variant is used most in their particular region, and if you have a chance to consult with them about it, do so right away.

Also, remember that words in RTL languages are often much shorter than words in English. So, adjust to keep a balance in how text is displayed on the page.</p>

## Icons

Using icons in RTL development can be tricky. Keep in mind that some of them might have to be mirrored, and some could be considered offensive to people of some nationalities, so double-check that the icons you’re using make sense.

Icons that are symmetrical and that don’t point in a particular direction should not be flipped.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aceec9ea-9e11-4f90-8f57-bb1255375f61/02-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aceec9ea-9e11-4f90-8f57-bb1255375f61/02-right-to-left-development-for-mobile-design-preview-opt.png" width="711" height="301" alt="" /></a><figcaption>There is no need to mirror symmetrical icons. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

On the other hand, icons that clearly point in a particular direction should be mirrored.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b7e84c-3d43-4f53-b366-60596d369657/01-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b7e84c-3d43-4f53-b366-60596d369657/01-right-to-left-development-for-mobile-design-preview-opt.png" width="605" height="301" alt="" /></a><figcaption>Mirror icons that point to a side. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

<pre><code class="language-css">&lt;span class="back-icon"&gt;&lt;/span&gt;
    body[dir="rtl"] {
        transform: scale(-1, 1);
    }
    </code></pre>

The scale (x, y) CSS function used in the example above modifies the size of an element. If set to `1`, it does nothing, but when negative, it performs as a “point reflection” and can modify size.

Icons that have characters or words from non-RTL languages don’t need to be mirrored. You should, however, localize them if necessary.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d682cede-e8f4-4231-b17c-f7cde1487b75/04-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d682cede-e8f4-4231-b17c-f7cde1487b75/04-right-to-left-development-for-mobile-design-preview-opt.png" width="535" height="301" alt="" /></a><figcaption>Icons containing words or characters from non-RTL languages don’t need be translated, but should be localized if necessary. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

Ensure that the icons you’re using are appropriate. For example, using a wine glass as a symbol for a restaurant or bar could be misunderstood because alcohol consumption is prohibited in Islam. Cultural peculiarities need to be taken into account, and developers should double-check that the symbols and icons they’re using are appropriate for the target market.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eca5e32-d2e6-4028-be5f-58c1ee04e7ea/05-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eca5e32-d2e6-4028-be5f-58c1ee04e7ea/05-right-to-left-development-for-mobile-design-preview-opt.png" width="605" height="301" alt="" /></a><figcaption>Avoid culturally inappropriate icons. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

## Navigation Menus

Logos, navigation buttons and menus should be located in the upper-right corner for RTL design. The two latter elements also need to be displayed in reverse order. You don’t, however, need to mirror all of the stuff related to controlling media content (such as play and pause buttons).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f58766b-d2e9-42de-9c50-7a3248c9a69a/21-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a152e70-dcd8-4a9e-a690-060ce8ee1e96/21-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="409" alt="" /></a><figcaption>Example of YouTube’s usage of media-content-management buttons in RTL design. (Image source: <a href="https://www.youtube.com/watch?v=e-5obm1G_FY">YouTube</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f58766b-d2e9-42de-9c50-7a3248c9a69a/21-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

## Digit Ordering

The order of digits in numbers should not be changed for RTL. Note the phone number below. The digits are displayed in the same order in both LTR and RTL, but the telephone icon changes position. The same rule applies to other digits (such as addresses and other numeric strings).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d96a8963-c2e2-41b8-bbc5-c34ef482b25a/08-right-to-left-development-for-mobile-design-large-opt-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb3fc13e-be78-4507-a30e-8ea1897a4e9d/08-right-to-left-development-for-mobile-design-800w-opt-1.png" width="800" height="117" alt="" /></a><figcaption>The order of digits shouldn’t change for RTL design. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d96a8963-c2e2-41b8-bbc5-c34ef482b25a/08-right-to-left-development-for-mobile-design-large-opt-1.png">View large version</a>)
</figcaption></figure>

## Position Of Control Buttons

Even though people speaking RTL languages perceive and process information from right to left, many of them are right-handed. Thus, it would be a good idea not to mirror control buttons, so that users can interact with them comfortably. Instead, center them to resolve any issues. For instance, if the orange button shown below was located to the left, it’d be extremely difficult for people to reach it with their right thumb while holding their device in one hand:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3920210-e18a-4759-99b6-a67416869669/19-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88262692-8699-42d6-9426-28b5223d8cee/19-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="762" alt="" /></a><figcaption>Placing the orange button to the left would be uncomfortable for users. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3920210-e18a-4759-99b6-a67416869669/19-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

In this case, it would be much more convenient for users if such important elements of interaction were large and located in the middle of the screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b0b57e0-fc97-48f2-bcfb-277fef8927b1/20-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f91dfe60-edc7-4ef5-b05c-4bb968b1f537/20-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="762" alt="" /></a><figcaption>Placing the orange button in the middle of the page would solve all convenience-related problems. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b0b57e0-fc97-48f2-bcfb-277fef8927b1/20-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

The elements in the bottom tab bar below should be positioned from right to left. **RTL also exists in the Persian language** — see example below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c3b2f7-9561-4566-82bb-9ef51da026a2/18-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5c3b2f7-9561-4566-82bb-9ef51da026a2/18-right-to-left-development-for-mobile-design-preview-opt.png" width="792" height="1265" alt="" /></a><figcaption>In RTL design, the elements in the bottom tab bar should be positioned from right to left. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)</figcaption></figure>

Navigation drawers should appear from the right side.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/686fb4ce-e798-4ddf-804a-75e23115b683/17-right-to-left-development-for-mobile-design-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/686fb4ce-e798-4ddf-804a-75e23115b683/17-right-to-left-development-for-mobile-design-preview-opt.png" width="792" height="1265" alt="" /></a><figcaption>In RTL design, drawers should appear from the right side. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>)
</figcaption></figure>

## Position Of Other Symbols

The position of symbols that can be used for both RTL and LTR (such as punctuation marks) will depend on the direction of the text as a whole. This is because browsers process RTL words in the RTL direction, even though the data format starts from the beginning. Punctuation is converted only towards the specified direction.

The following example should illustrate the issue better:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b28fbc0-48f6-4843-9349-260b9a8c48b1/09-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/414d634c-690d-4452-b6d8-7be98a37d67b/09-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="182" alt="" /></a><figcaption>You need to convert RTL and LTR strings into separate elements in order to have punctuation symbols appear in the right direction. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b28fbc0-48f6-4843-9349-260b9a8c48b1/09-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

To fix this problem, you can convert RTL and LTR strings (or text fragments) into separate elements. Then, specify their direction with either the `dir` attribute or the CSS `direction` property. In the first case, you would do this:

<pre><code class="language-html">
    &lt;p dir="rtl" class="rtl-text"&gt;?سوف أعطي مثالا على ذلك. لا تمانع&lt;/p&gt;
    &lt;p dir="ltr" class="ltr-text"&gt;I will give an example. Don’t you mind?&lt;/p&gt;
    </code></pre>

And in the second, this:

<pre><code class="language-css">.rtl-text {
    direction: rtl;
}

.ltr-text {
    direction: ltr;
}</code></pre>

Alternatively, you could also use the `bdi` tag to avoid this type of issue. However, it is only supported in Chrome (16) and Firefox (10).</p>

## Separate RTL CSS File

For basic CSS styles, you should create a separate RTL file and set the horizontal properties there (floating left and right, padding left and right, margins and so on), while also redefining them appropriately:

<pre><code class="language-css">div.class {
    width: 150px;
    height: 100px;
    float: left;
    padding: 0 15px 0 10px;
}</code></pre>

And in the `rtl.css` file:

<pre><code class="language-css">html[dir="rtl"] div.class {
    float: right;
    padding: 0 10px 0 15px;
}</code></pre>

If you need to eliminate some other LTR-directed features, you can always create and attach another separate `rtl.css` file.

In case this approach doesn’t meet your needs well enough, you can create two separate style files for LTR and RTL. Various utilities can be applied to automate their assembly. One such program is [css-flip](https://github.com/twitter/css-flip) (created by Twitter). With its help, you can easily compile a file with properties redefined for RTL from an existing source file.

In `input.css`:

<pre><code class="language-css">p {
    padding-left: 1em;
}</code></pre>

And in <code>output.rtl.css</code>:

<pre><code class="language-css">p {
    padding-right: 1em;
}</code></pre>

You can also use replacements and exceptions, based on directives in the source file. For example, in `input.css`:

<pre><code class="language-css">p {
    /<em>@replace: -32px -32px</em>/ background-position: -32px 0;
    /<em>@replace: "&gt;"</em>/ content: "&lt;";
    /<em>@noflip</em>/ float: left;
}</code></pre>

And in `output.rtl.css`:

<pre><code class="language-css">p {
    background-position: -32px -32px;
    content: "&gt;";
    float: left;
}</code></pre>

[RTLCSS](https://github.com/MohammadYounes/rtlcss) is another tool that supports replacements (exceptions) and makes it possible for developers to rename selectors, add local configurations of exception, and delete or add properties.

You could also use plugins for assembly instruments, including for [Gulp](https://github.com/jjlharrison/gulp-rtlcss), [Grunt](https://github.com/MohammadYounes/grunt-rtlcss) and [Webpack](https://github.com/romainberger/webpack-rtl-plugin).

For example, in `input.css`:

<pre><code class="language-css">.example {
    transform: translateY(10px) /*rtl:append:scaleX(-1)*/;
    font-family: "Helvetica Neue", Arial/*rtl:prepend:"Arabic fonts", */;
    font-size:1.3em/*rtl:1.2em*/;
    /*rtl:remove*/
    text-decoration:underline;
    /*rtl:begin:ignore*/
    margin-left:15px;
    padding-left:20px;
    /*rtl:end:ignore*/
}</code></pre>

And in `output.rtl.css`:

<pre><code class="language-css">.example {
    transform: translateY(10px) scaleX(-1);
    font-family: "Arabic fonts","Helvetica Neue", Arial;
    font-size:1.2em;
    margin-left:15px;
    padding-left:20px;
}</code></pre>

You can also make configurations for renaming selectors. Again, in `input.css`:

<pre><code class="language-css">/*rtl:begin:options: {
    "autoRename": true,
    "stringMap":[ {
       "name" : "prev-next",
       "search" : ["prev"],
       "replace" : ["next"],
       "options" : {"ignoreCase":false}
   } ]
} */
slide-prev {
    content: '<';
}
slide-next {
    content: '>';
}
/*rtl:end:options*/</code></pre>

And in `output.rtl.css`:

<pre><code class="language-css">slide-next {
    content: '<';
}
slide-prev {
    content: '>';
}</code></pre>

## Calendars

Calendars are probably one of the most important and complicated aspects of RTL design, because calendar years are different between LTR and RTL geographic regions.</p>

### Hijri

Hijri, the Islamic calendar, is lunar-based, which means that a year in the Gregorian calendar is longer than in the Islamic calendar. As a result, Hijri always has to shift according to the Gregorian calendar.</p>

### Hebrew Calendar

The Hebrew calendar, which has 12 lunar months, with an extra month added every few years, also differs from the Gregorian calendar. These differences make it hard to find an adequate tool for working with both Gregorian calendars in LTR scripts and non-Gregorian calendars in RTL scripts.</p>

### Tools for Displaying Calendars

One popular tool is [FullCalendar](https://github.com/fullcalendar/fullcalendar), because it calculates time based on Moment.js. However, it cannot convert between different types of calendars and is only useful for localizing dates and displaying RTL content.

[dijit/Calendar](https://dojotoolkit.org/reference-guide/1.10/dijit/Calendar.html) is able to display non-Gregorian calendars but has a rather limited range of tasks.

The `DateTimeFormat` constructor is an invaluable property for international objects. It makes it possible to pass additional options to the argument string when specifying the exact formatting for time and date.

Below, you can see how a date should be converted from the Gregorian calendar to the Islamic one:

<pre class="codehilite"><code class="language-javascript">var sampleDate = new Intl.DateTimeFormat("ru-RU-u-ca-islamicc").format(new Date()); // =&gt; "26.03.2017" console.log(sampleDate); // =&gt; "27.06.1438 AH"</code></pre>

## Abbreviations (Days Of Week)

Although abbreviating the names of the days of the week is standard in many languages, this isn’t possible in Arabic because all of them start with the same letter. Instead, simply display their whole names and reduce the font size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04383ab4-17ae-4f96-a70c-6b9e1cade393/10-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4467d5ad-fc61-4ece-90d8-4fca43809a78/10-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="424" alt="" /></a><figcaption>All names of weekdays start with the same letter in Arabic, meaning that you cannot abbreviate them like you would in English. (Image source: <a href="https://www.steelkiwi.com" rel="nofollow">SteelKiwi</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04383ab4-17ae-4f96-a70c-6b9e1cade393/10-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

## Internationalization

If your product requires internationalization, consider the ECMAScript Internationalization API. It comes with a language-sensitive string comparison and relevant formatting for numbers, dates and time.

Another important point is that ECMAScript supports not only Arabic, but also a wide range of other combinations, such as Arabic-Arabic and Arabic-Tunisian.

Also, keep in mind that the use of Eastern and Western Arabic numerals might depend on the language variant. Some regions might use Eastern Arabic numerals (123), while others use Western ones (١٢٣).</p>

### Formatting Arabic-Egyptian Numerals

<pre class="codehilite"><code class="language-javascript">var sampleNumber = new Intl.NumberFormat(‘ar-EG’).format(12345);
        console.log(sampleNumber); // =&gt; ١٢٬٣٤٥</code></pre>

In Tunisia, for instance, Eastern Arabic numerals are usually used:

<pre class="codehilite"><code class="language-javascript">var sampleNumber = new Intl.NumberFormat(‘ar-TN’).format(12345);
        console.log(sampleNumber); // =&gt; 12345</code></pre>

## Examples Of Native Arabic Websites

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3e4a60-a662-44ec-9b77-4683681bd83d/26-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d878ac3-9825-42a0-8180-265babba6cce/26-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="395" alt="" /></a><figcaption><a href="https://www.arageek.com/">Arageek</a> is dedicated to all hip geek news around the world. (Image source: <a href="https://www.arageek.com/">Arageek</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e3e4a60-a662-44ec-9b77-4683681bd83d/26-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d89d027-3164-4fa7-8826-5738f6484c4f/25-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a34e238-d728-4315-8569-53a62f368288/25-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="395" alt="" /></a><figcaption><a href="https://www.hawaaworld.com/">Hawaa Forum</a> is an online community for women. (Image source: <a href="https://www.hawaaworld.com">Hawaaworld.com</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d89d027-3164-4fa7-8826-5738f6484c4f/25-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1bae042-d2b4-444c-8302-3f45f1d99743/24-right-to-left-development-for-mobile-design-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26dcd10f-ce8d-4b46-8979-e341a80582c6/24-right-to-left-development-for-mobile-design-800w-opt.png" width="800" height="395" alt="Saudileague" /></a><figcaption><a href="https://saudileague.com//">Saudi League</a> is dedicated to football in Saudi Arabia, with news, tournament days, info about teams and more. (Image source: <a href="https://saudileague.com">Saudileague.com</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1bae042-d2b4-444c-8302-3f45f1d99743/24-right-to-left-development-for-mobile-design-large-opt.png">View large version</a>)
</figcaption></figure>

## Share Your Experience!

Cultural and linguistic peculiarities can be a hassle when you’re developing for different regions and markets. When it comes to the RTL market, developers must use their knowledge to adhere to a completely different set of rules, making the whole process more challenging and potentially frustrating. Using the 12 tips above, we hope you’re able to overcome some of the most common problems with RTL development.

If you have encountered any obstacles related to RTL development, please describe them (along with the solutions you’ve found) in the comments section below. The more that developers share their knowledge and experience, the easier it will be for all of us to deal with the peculiarities of RTL development.

{{< signature "da, vf, yk, al, il" >}}

