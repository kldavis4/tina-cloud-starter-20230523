---
title: 'Accessibility APIs: A Key To Web Accessibility'
slug: web-accessibility-with-accessibility-api
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/830ce5d6-90c1-4143-9e4b-8952ede5060e/excerpt-accessibilityapi.jpg
date: 2015-03-16T17:00:08.000Z
author: leoniewatsonchaalsnevile
summary: >-
  Technologies work together to extract accessibility information from a web interface and appropriately present it to the user. If appropriate content semantics are not available, then assistive technologies will use old and unreliable techniques to make the interface usable. A big part of accessibility is, therefore, an easily met responsibility of web developers.
description: >-
  Technologies work together to extract accessibility information from a web interface and appropriately present it to the user. A big part of accessibility is, therefore, an easily met responsibility of web developers.
categories:
  - Coding
  - UX
  - Accessibility
  - API
---
Web accessibility is about people. Successful web accessibility is about anticipating the different needs of all sorts of people, understanding your fellow web users and the different ways they consume information, empathizing with them and their sense of what is convenient and what frustratingly unnecessary barriers you could help them to avoid.

Armed with this understanding, accessibility becomes a cold, hard technical challenge. A firm grasp of the technology is paramount to making informed decisions about accessible design.

How do assistive technologies present a web application to make it accessible for their users? Where do they get the information they need? **One of the keys is a technology known as the accessibility API** (or accessibility application programming interface, to use its full formal title).

## Reading The Screen

To understand the role of an accessibility API in making Web applications accessible, it helps to know a bit about how assistive technologies provide access to applications and how that has evolved over time.

### A World of Text

With the text-based DOS operating system, the characters on the screen and the cursor position were held in a screen buffer in the computer’s memory. Assistive technologies could obtain this information by reading directly from the screen buffer or by intercepting signals being sent to a monitor. The information could then be manipulated &mdash; for example, magnified or converted into an alternative format such as synthetic speech.

### Getting Graphic

The arrival of graphical interfaces such as OS/2, Mac OS and Windows meant that key information about what was on the screen could no longer be simply read from a buffer. Everything was now drawn on screen as a picture, including pictures of text. So, assistive technologies on those platforms had to find a new way to obtain information from the interface.

They dealt with this by intercepting the drawing calls sent to the graphics engine and using that information to create an alternate off-screen version of the interface. As applications made drawing calls through the graphics engine to draw text, carets, text highlights, drop-down windows and so on, information about the appearance of objects on the screen could be captured and stored in a database called an off-screen model. That model could be read by screen readers or used by screen magnifiers to zoom in on the user’s current point of focus within the interface. Rich Schwerdtfeger’s seminal 1991 article in Byte, “[Making the GUI Talk](https://www.paciellogroup.com/blog/2015/01/making-the-gui-talk-1991-by-rich-schwerdtfeger/),” describes the then-emerging paradigm in detail.

### Off-Screen Models

Recognizing the objects in this off-screen model was done through heuristic analysis. For example, the operating system might issue instructions to draw a rectangle on screen, with a border and some shapes inside it that represent text. A human might look at that object (in the context of other information on screen) and correctly deduce it is a button. The heuristics required for an assistive technology to make the same deduction are actually very complex, which causes some problems.

To inform a user about an object, an assistive technology would try to determine what the object is by looking for identifying information. For example, in a Windows application, the screen reader might present the Window Class name of an object. The assistive technology would also try to obtain information about the state of an object by the way it is drawn &mdash; for example, tracking highlighting might help deduce when an object has been selected. This works when an object’s role or state can easily be determined, but **in many cases the relevant information is unclear**, ambiguous or not available programmatically.

This reverse engineering of information is both fallible and restrictive. An assistive technology could implement support for a new feature only once it had been introduced into the operating system or application. An object might not convey useful information, and in any case it took some time to identify it, develop the heuristics needed to support it and then ship a new version of the screen reader. This created a delay between the introduction of new features and assistive technology’s ability to support it.

The off-screen model needs to shadow the graphics engine, but the engines don’t make this easy. The off-screen model has to independently calculate things like white-space management and alignment coordination, and errors would almost inevitably mount up. These errors could result in anomalies in the information conveyed to assistive technology users or in garbage buildup and memory leaks that lead to crashes.

{{% feature-panel %}}

## Accessibility APIs

From the late 1990s, operating system accessibility APIs were introduced as a more reliable way to pass information to assistive technologies. Instead of applying complex heuristics to determine what an on-screen object might be, assistive technologies could query the accessibility API for specific information about each object. Authors could now provide the necessary information about an application in a form that they knew assistive technology would understand.

An accessibility API represents objects in a user interface, exposing information about each object within the application. Typically, there are several pieces of information for an object, including:

- **Its role** (for example, it might be a button, an application window or an image);
- **A name** that identifies it within the interface (if there is a visible label like text on a button, this will typically be its name, but it could be encoded directly in the object);
- **Its state** or current condition (for example, a checkbox might currently be selected, partially selected or not selected).

The first platform accessibility API, Microsoft Active Accessibility (MSAA), was made available in a 1997 update to Windows 95. MSAA provided information about the role and state of objects and some of their properties. But it gave no access to things like text formatting, and the relationships between objects in the interface were difficult or impossible to determine.

In 1998, IBM and Sun Microsystems built a cross-platform accessibility API for Java. Java Swing 1.0 gave access to rich text information, relationships, tables, hyperlinks and more. The Java Jive screen reader, built on this platform, was the first time a screen reader’s information about the components of a user interface included role, state and associated properties, as well as rich text formatting details.

Notably, Java Jive was written by three developers in roughly five months; developing a screen reader through an off-screen model typically took *several years*.

### Accessibility APIs Go Mainstream

In 2001 the Assistive Technology Service Provider Interface (AT-SPI) for Linux was released, based on the work done on Java, and in 2002 Apple included the NSAccessibility protocol with Mac OS X (10.2 Jaguar).

Meanwhile on Windows, the situation was getting complicated. Microsoft shipped the User Interface Automation (UIA) API as part of Windows 7, while IBM released IAccessible2 as an open standard for Windows and Linux, again evolved from the work done on Java.

Accessibility APIs existed for mobile platforms before touchscreen smartphones became dominant, but in 2009 Apple added the UI Accessibility API to iOS 3, and Android 1.6 (Donut) shipped with the Accessibility Framework.

By the beginning of 2015, Chrome OS stood out as the most mainstream platform lacking a standard accessibility API. But Google was beta testing its Automation API, intended to fill that gap in the platform.

### Modern Accessibility APIs

In modern accessibility APIs, user interfaces are represented as a hierarchical tree. For example, an application window would contain several objects, the first of which might be a menu bar. The menu bar would contain a number of menus, each of which contains a number of menu items, and so on. The accessibility API describes an object’s relationship to other objects to provide context. For example, a radio button would probably be one “sibling” within a group.

Other features such as information about text formatting, applicable headers for content sections or table cells and things such as event notifications have all become commonplace in modern accessibility APIs.

Assistive technologies now make standard method calls to the operating system to get information about the objects on the screen. This is far more reliable, and far more efficient, than intercepting low-level operating system messages and trying to deconstruct them into something meaningful.

{{% ad-panel-leaderboard %}}

## From The Web To The Accessibility API

In browsers, the platform accessibility API is used both to make information about the browser itself available to assistive technologies and to expose information about the currently rendered content.

Browsers typically support one or more of the available accessibility APIs for the platform they’re running on. For example, on Windows, Firefox, Chrome, Opera and Yandex support MSAA/IAccessible and IAccessible2, while Internet Explorer supports MSAA/IAccessible and UIAExpress. Safari and Chrome support NSAccessibility on OS X and UIAccessibility on iOS.

The browser uses the HTML DOM, along with further information derived from CSS, to generate an accessibility tree hierarchy of the content it is displaying, and it passes that information to the platform accessibility API. Information such as the role, name and state of each object in the content, as well as how it relates to other objects in the content, can then be queried by assistive technologies.

Let’s see how this works with some HTML:

<pre><code class="language-markup">&lt;p&gt;&lt;img src="mc.png" alt="My cat" longdesc="meeow.html"&gt;Rocks!&lt;/p&gt;
</code></pre>

We have an image, rendered as part of a paragraph. A browser exposes several pieces of information about the image to the accessibility API:

1.  It has a role of “image” (or “graphic” &mdash; details vary between platforms). This is implicitly determined from the fact that it is an HTML `img` element.
2.  Its name is “My cat”. For images, the name is typically derived from the `alt` attribute.
3.  A description is available on request, at the URL `meeow.html` (at the same “base” as the image).
4.  The parent is a paragraph element, with a role of “text.”
5.  The image has a “sibling” in the same container, the text node “Rocks!”

An assistive technology would query the accessibility API for this information, which it would present so the user can interact with it. For example, a screen reader might announce, “Graphic: My cat. Description available.”

(Does a cat picture need a full description? Perhaps not, but try explaining that to people who really want to tell you just how amazing and talented their feline friends actually are &mdash; or those of their readers who *want* to know all about what *this* cat looks like! Meanwhile, the philistines among us can ignore the extra information.)

### Roles

Most HTML elements have what are called “roles,” which are a way of describing elements. If you are familiar with WAI-ARIA, you will be aware of the `role` attribute, which sets a role explicitly. Most elements already have implicit roles, however, which go along with the element type. For example:

- `<ul>` and `<ol>` have “list” as implicit role,
- `<a>` has “link” or “hyperlink” as implicit role,
- `<body>` has “document” as implicit role.

These role mappings are being standardized and documented in the W3C’s “[HTML Accessibility API Mappings](https://www.w3.org/TR/html-aam-1.0/)” specification.

### Names

While roles are typically derived from the type of HTML element, the name (sometimes referred to as the “accessible name”) of an object often comes from one of several different sources. In the case of a form field, the name is usually taken from the label associated with the field:

<pre><code class="language-markup">&lt;input type="radio" id="tequila" name="drinks" checked&gt;
&lt;label for="tequila"&gt;Reposado&lt;/label&gt;
</code></pre>

In this example, a button has the “radio button” role. Its accessible name will be “Reposado,” the text content of the label element. So, when a speech-recognition tool is instructed to “Click Radio button Reposado,” it can target the correct object within the interface.

The `checked` attribute indicates the state of the button, so that a screen reader can announce “Radio button Reposado Checked” or allow a user to navigate directly between the checked options in order to rapidly review a form that contains multiple sets of radio buttons.

Authors have an important role to play, **providing the key information that assistive technologies need**. If authors don’t do the “right thing,” assistive technologies must look in other places to try to get an accessible name &mdash; if there is no label, then a title or some text content might be near the radio button, or its relationship to other elements might help the user through context.

It is important to note that authors should not rely on an assistive technology’s ability to do this, because it is generally unreliable. It is a “repair” strategy that gives assistive technology users some chance of using a poorly authored page or website, such as the following:

<pre><code class="language-markup">&lt;p&gt;How good is reposado?&lt;br&gt;
&lt;!--BAD CODE EXAMPLE: DON'T DO THIS--&gt;
&lt;input type="radio" id="fantastic" name="reposado" checked &gt;
&lt;label for="reposado"&gt;Fantastic&lt;/label&gt;&lt;br&gt;
&lt;input type="radio" id="notBad" name="tequila"&gt;&lt;br&gt;
&lt;input type="radio" id="meh" name="tequila" title="meh"&gt; Meh
</code></pre>

Faced with this case, a screen reader might provide information such as “second of three options,” based on information that the browser provides to the accessibility API about the form. Little else can be determined reliably from the code, though.

Nothing in the code associates the question with the set of radio buttons, and nothing informs the browser of what the accessible name for the first two buttons should be. The for` and id` attributes of the `<label>` and `<input>` for the first button do not share a common value, and nothing associates the nearby text content with the second button. The browser could use the title of the third button as an accessible name, but it duplicates the nearby text and unnecessarily bloats the code.

A well-authored version of this would use the fieldset` element to group the radio buttons and use a legend` element to associate the question with the group. Each of the buttons would also have a properly associated label.

<pre><code class="language-markup">&lt;fieldset&gt;&lt;legend&gt;How good is reposado?&lt;/legend&gt;
&lt;!-- THIS IS A BETTER WAY TO CODE THE EXAMPLE --&gt;
&lt;input type="radio" id="fantastic" name="reposado" checked&gt;
&lt;label for="fantastic"&gt;Fantastic&lt;/label&gt;&lt;br&gt;
&lt;input type="radio" id="notBad" name="reposado"&gt;
&lt;label for="notBad"&gt;Not bad&lt;/label&gt;&lt;br&gt;
&lt;input type="radio" id="meh" name="reposado"&gt;
&lt;label for="meh"&gt;Meh&lt;/label&gt;&lt;br&gt;
&lt;/fieldset&gt;
</code></pre>

Making this information available through the accessibility API is more efficient and less prone to error than relying on assistive technologies to create an off-screen model or guess at the information they need.

{{% ad-panel-leaderboard %}}

## Conclusion

Today’s technologies &mdash; operating systems, browsers and assistive technologies &mdash; work together to extract accessibility information from a web interface and appropriately present it to the user. If appropriate content semantics are not available, then assistive technologies will use old and unreliable techniques to make the interface usable.

The value of accessibility APIs is in allowing the operating system, browser and assistive technology to efficiently and reliably give users the information they need. It is now easy to make an interface developed with well-written HTML, CSS and JavaScript very accessible and usable for assistive technology users. A big part of accessibility is, therefore, an easily met responsibility of web developers: Know your job, use your tools well, and many pieces will fall into place as if by magic.

*With thanks to Rich Schwerdtfeger, Steve Faulkner and Dominic Mazzoni.*

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)
*   [Accessibility: Improving The UX For Color-Blind Users](https://www.smashingmagazine.com/2016/06/improving-ux-for-color-blind-users/)
*   [Inclusive Front-End Design Patterns, A New Smashing Book](https://www.smashingmagazine.com/inclusive-design-patterns/)

{{< signature "hp, al, ml" >}}