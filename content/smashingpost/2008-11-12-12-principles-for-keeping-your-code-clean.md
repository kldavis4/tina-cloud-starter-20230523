---
title: 12 Principles For Clean HTML Code
slug: 12-principles-for-keeping-your-code-clean
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13013bb9-055d-4978-b55a-9f55c3c39961/accessibility.jpg
date: 2008-11-12T23:02:26.000Z
author: chris-coyier
description: >-
  Beautiful HTML is the foundation of a beautiful website. When I teach people
  about CSS, I always begin by telling them that good CSS can only exist with
  equally good HTML markup. A house is only as strong as its foundation, right?
  The advantages of clean, semantic HTML are many, yet so many websites suffer
  from poorly written markup.
categories:
  - Coding
  - Workflow
  - CSS
  - Principles
  - Characters
  - Validation
---
Beautiful and clean HTML is the foundation of a beautiful website. When I teach people about <a title="Mastering CSS Principles: A Comprehensive Guide" href="https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/">CSS</a>, I always begin by telling them that good CSS can only exist with equally good HTML markup. A house is only as strong as its foundation, right? The advantages of clean, semantic HTML are many, yet so many websites suffer from poorly written markup.

Let's take a look at some poorly written HTML, discuss its problems, and then whip it into shape! Bear in mind, we are not passing any judgment on the <em>content</em> or <em>design</em> of this page, only the markup that builds it. If you are interested, take a peek at the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ee062dd-ce0a-4f77-afc3-10055bde8239/bad.html">bad code</a> and the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58380ca1-1fc3-4e03-9cd1-30c1cb4bf249/good.html">good code</a> before we start so you can see the big picture. Now let's start right at the top. 

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)
*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/7-principles-of-clean-and-optimized-css-code/)
*   [ESLint: The Next-Generation JavaScript Linter](https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/)
*   [An Introduction To PostCSS](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/)

## 1\. Strict DOCTYPE

If we are going to do this, let's just do it right. No need for a discussion about whether to use HTML 4.01 or XHTML 1.0: both of them offer a strict version that will keep us nice and honest as we write our code.

{{% feature-panel %}}

![clean html](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d36d9a9-0b7b-4f56-93d6-4c60083dd227/cleancode-1.png)

Our code doesn't use any tables for layout anyway (nice!), so there really is no need for a transitional DOCTYPE.

<strong>Resources:</strong>

*   [W3C: Recommended DTDs to use in your Web document](https://www.w3.org/QA/2002/04/valid-dtd-list.html)
*   [Fix Your Site With the Right DOCTYPE!](https://www.alistapart.com/stories/doctype/)
*   [No more Transitional DOCTYPEs, please](https://www.456bereastreet.com/archive/200609/no_more_transitional_doctypes_please/)

## 2\. Character set &amp; encoding characters

In our &lt;head&gt; section, the very first thing should be the declaration of our character set. We're using UTF-8 here, which is swell, but it's listed after our &lt;title&gt;. Let's go ahead and move it up so that the browser knows what character set it's dealing with before it starts reading any content at all.

![character example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/451cf76a-763c-4c50-93f5-a5d8979e9eaf/cleancode-2.png)

While we're talking about characters, let's go ahead and make sure any funny characters we are using are properly encoded. We have an ampersand in our title. To avoid any possible misinterpretation of that, we'll convert it to <code>&amp;amp;</code> instead.

<strong>Resources:</strong>

*   [Wikipedia: UTF-8](https://en.wikipedia.org/wiki/UTF-8)
*   [A tutorial on character code issues](https://www.cs.tut.fi/~jkorpela/chars.html)
*   [The Extended ASCII table](https://www.ascii-code.com/)

## 3\. Proper indentation

All right, we are about three lines in and I'm already annoyed by the lack of indentation. Indentation has no bearing on how the page is rendered, but it has a huge effect on the readability of the code. Standard procedure is to indent one tab (or a few spaces) when you are starting a new element that is a child element of the tag above it. Then move back in a tab when you are closing that element.

![indentation example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccd3815d-299e-490e-81ca-4fb02c8209b9/cleancode-3.png)

Indentation rules are far from set in stone; feel free to invent your own system. But I recommend being consistent with whatever you choose. Nicely indented markup goes a long way in beautifying your code and making it easy to read and jump around in.

<strong>Resources:</strong>

*   [Clean up your Web pages with HTML TIDY](https://www.w3.org/People/Raggett/tidy/)

## 4\. Keep your CSS and JavaScript external

We have some CSS that has snuck into our &lt;head&gt; section. This is a grievous foul because not only does it muddy our markup but it can only apply to this single HTML page. Keeping your CSS files separate means that future pages can link to them and use the same code, so changing the design on multiple pages becomes easy.

![external example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb631294-8c66-48db-aa47-520e656b5f9d/cleancode-4.png)

This may have happened as a "quick fix" at some point, which is understandable and happens to all of us, but let's get that moved to a more appropriate place in an external file. There is no JavaScript in our head section, but the same goes for that.</p>

## 5\. Nest your tags properly

The title of our site, "My Cat Site," is properly inside &lt;h1&gt; tags, which makes perfect sense. And as per the norm, the title is a link to the home page. However, the anchor link, &lt;a&gt;, wraps the header tags. Easy mistake. Most browsers will handle it fine, but technically it's a no-no. An anchor link is an "inline" element, and header tags are "block" elements. Blocks shouldn't go inside inline elements. It's like crossing the streams in Ghostbusters. It's just not a good idea.

![nesting example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccd3815d-299e-490e-81ca-4fb02c8209b9/cleancode-3.png)

## 6\. Eliminate unnecessary divs

I don't know who first coined it, but I love the term "divitis," which refers to the overuse of divs in HTML markup. Sometime during the learning stages of Web design, people learn how to wrap elements in a div so that they can target them with CSS and apply styling. This leads to a proliferation of the div element and to their being used far too liberally in unnecessary places.

![divitis example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cbd785b-145e-4b40-b74a-20df5f6d16b1/cleancode-6.png)

In our example, we have a div ("topNav") that wraps an unordered list ("bigBarNavigation"). Both divs and unordered lists are block-level elements. There really is no need whatsoever for the &lt;ul&gt; to be wrapped in a div; anything you can do with that div you can do with the &lt;ul&gt;.

<strong>Resources:</strong>

*   [Divitis: what it is, and how to cure it.](https://csscreator.com/?q=divitis)

## 7\. Use better naming conventions

This is a good time to bring up naming conventions, as we have just talked about that unordered list with an id of "bigBarNavigation." The "Navigation" part makes sense, because it's describing the content that the list contains, but "big" and "Bar" describe the design not the content. It might make sense right now because the menu is a big bar, but if you change the design of the website (and, say, change the website navigation to a vertical style), that id name will be confusing and irrelevant.

![naming conventions example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cde14740-68df-45f4-ab1f-e36ee4f16a47/cleancode-7.png)

Good class and id names are things like "mainNav," "subNav," "sidebar," "footer," "metaData," things that describe the content they contain. Bad class and id names are things that describe the design, like "bigBoldHeader," "leftSidebar," and "roundedBox."

## 8\. Leave typography to the CSS

The design of our menu calls for all-caps text. We just dig how that looks, and more power to us. We have achieved this by putting the text in all-caps, which of course works; but for better, future extensibility, we should abstract typographic choices like this one to the CSS. We can easily target this text and turn it to all-caps with {text-transform: uppercase}. This means that down the road, if that all-caps look loses its charm, we can make one little change in the CSS to change it to regular lowercase text.

![typography example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b8f8cae-5671-4720-bf9c-32e42d4a9413/cleancode-8.png)

## 9\. Class/id the <body>

By "class the body," I literally mean apply a class to the body, like &lt;body class="blogLayout"&gt;. Why? I can see two things going on in this code that lead me to believe that this page has a layout that is different than other pages on the website. One, the main content div is id'd "mainContent-500." Seems like someone had a "mainContent" div at one point and then needed to alter its size later on and, to do so, created a brand new id. I'm guessing it was to make it larger, because further in the code we see &lt;class="narrowSidebar"&gt; applied to the sidebar, and we can infer that that was added to slim down the sidebar from its normal size.

This isn't a very good long-term solution for alternate layouts. Instead, we should apply a class name to the body as suggested above. That will allow us to target both the "mainContent" and "sidebar" divs uniquely without the need for fancy new names or class additions.

![body class example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/706bb26e-9e60-4798-81aa-c56cf4787d74/cleancode-9.png)

Having unique class and id names for the body is very powerful and has many more uses than just for alternate layouts. Because every bit of page content lies in the "body" tag, you can uniquely target anything on any page with that hook; particularly useful for things like navigation and indicating <strong>current navigation</strong>, since you'll know exactly what page you are on with that unique body class.

<strong>Resources:</strong>

*   [ID Your Body For Greater CSS Control and Specificity](https://css-tricks.com/id-your-body-for-greater-css-control-and-specificity/)
*   [Case study: Re-using styles with a body class](https://www.37signals.com/svn/archives2/case_study_reusing_styles_with_a_body_class.php)

## 10\. Validate

Kind of goes without saying, but you should run your code through the ol' validator machine to pick up small mistakes. Sometimes the mistakes will have no bearing on how the page renders, but some mistakes certainly will. Validated code is certain to outlive non-validated code.

![validation example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68b39345-ec71-45f0-9024-7875c038e994/cleancode-10.png)

If for no other reason, seeing that green text on the W3C validator tool just makes you feel good inside.

<strong>Resources:</strong>

*   [The W3C Markup Validation Service](https://validator.w3.org/)
*   [XHTML-CSS Validator](https://xhtml-css.com/)

## 11\. Logical ordering

If it is at all possible, keeping the sections of your website in a logical order is best. Notice how the footer section lies above the sidebar in our code. This may be because it works best for the design of the website to keep that information just after the main content and out of the sidebar. Understandable, but if there is any way to get that footer markup down to be the last thing on the page and then use some kind of layout or positioning technique to visually put it where you need it, that is better.

![order example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c43ccb6d-b802-4495-89f6-818af2b42d45/cleancode-11.png)

## 12\. Just do what you can

We've covered a lot here, and this is a great start to writing clean HTML, but there is so much more. When starting from scratch, all of this seems much easier. When trying to fix existing code, it feels a lot more difficult. You can get bogged down in a CMS that is forcing bad markup on you. Or, there could be just so many pages on your website that it's hard to think of even where to begin. <strong>That's OK!</strong> The important thing is that you <strong>learn</strong> how to write good HTML and that you <strong>stick with it</strong>.

The next time you write HTML, be it a small chunk in a huge website, or the beginning of a fresh new project, <strong>just do what you can</strong> to make it right.

![order example](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6af28b75-20b2-4a94-a101-5ec524f612ac/cleancode-12.png)

_(al)_

