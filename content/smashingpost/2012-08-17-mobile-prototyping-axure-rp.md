---
title: Mobile Prototyping With Axure RP
slug: mobile-prototyping-axure-rp
image: null
date: 2012-08-17T11:20:13.000Z
author: will-hacker
description: >-
  Validating a design through user testing is necessary for the success of almost any product. And it’s even more critical in the mobile application space, where context and individual devices play an important role in how a product is experienced.
categories:
  - Mobile
  - Apps
  - Prototyping
---

Fortunately, interactive prototyping is a time-tested way to quickly get your design onto a user’s device and into their hands. So, let’s look at why prototyping matters and explore one powerful tool that will enable you to do it quickly.

## So, What Is A Prototype?

First of all, let’s define what a prototype is and is not. A prototype is a design artifact for end-user testing and for communicating functionality to business and development stakeholders. It isn’t meant to be a fully functioning entity with live data connections, although sometimes it can be. The best testing prototype has only what you need for your purpose and not a single thing more. The point is to design quickly, test it, fail fast and learn something. This is why you prototype. It’s a low-cost activity that saves you time and substantial expense over the life of a design project.

{{% feature-panel %}}

In this article, I’ll show you how I used Axure RP 6.5 to prototype a theoretical iPhone app for the Chicago chapter of the Interaction Design Association (IxDA). I created this sample prototype recently for an event about design tools run by our local IxDA chapter, but I approached it the way I would in an actual working situation.

If you aren’t familiar with it, Axure RP is a rapid prototyping tool that runs on Mac and Windows and can be used to create interactive prototypes for desktop websites and mobile products without writing any code. Axure costs $589 per user license, which allows you to install it on two computers. I run Axure on a MacBook Pro at work and on an iMac in my home office. Some alternatives are:

*   [iRise Studio](https://www.irise.com/)
*   [Balsamiq](https://www.balsamiq.com/) (Can be used to create clickable wireframes.)
*   [Microsoft SketchFlow](https://www.microsoft.com/expression/products/SketchFlow_Overview.aspx) (If you are in a .NET environment.)

If you are new to Axure, start by learning some of the things you shouldn’t do, such as creating unnecessary text widgets and not naming your prototype’s objects. Have a look at Axure’s own <a href="https://www.axure.com/top-5-mistakes">How to Avoid the Top 5 Mistakes When Starting to Use Axure RP</a>.</p>

## Getting Started

The first thing you’ll need to do is create a new Axure file.</p>

### Setting Up Your Project

For a mobile website or app, just create the prototype’s pages in a smartphone-friendly width and height. If you’re targeting the iPhone, create a page that’s 320 × 480 pixels (or 1024 × 768 if you are designing for the iPad). Because most mobile pages run longer than the height of the device’s screen, focusing on getting the width right is more important. And these widths will work on both Retina and non-Retina iOS displays. Because Axure is a WYSIWYG design tool, you can’t size pages by a percentage of the screen’s width, which would be ideal. Your prototype will not always expand to fill the screen’s width when you flip the device from portrait to landscape orientation, so take that into account if your app will normally be used in landscape mode.

For Android phones, a width of 480 pixels usually works, although I often just create a single 320-pixel-wide version for mobile Web testing on both platforms. This size has displayed correctly on most newer Android phones that I’ve encountered in testing (and some BlackBerry and other devices as well). Because the pixel width of an Axure project is fixed, testing Android phones on a device that you control is easier because of all the different screen resolutions available. But remember that it’s a testing prototype, so don’t worry about making it perfect. If you must test on a user’s device (perhaps because you need access to native apps such as their address book), then test the prototype on a few different versions of Android while you are building it. Use your website’s analytics software to find out what Android versions and handsets are the most popular among your users.

To create a prototype of a native app for Android or iPhone, you can start by adding existing widget libraries to Axure. A list of free and paid widget libraries is maintained on Axure’s website (see the “Resources” section below). If you have access to a visual design resource and need a higher level of fidelity, you can have the resource create tab bars, home screen icons and other widgets. If you are creating a lower-fidelity prototype, then the shapes and objects built into Axure might be all you need.

I usually test higher-fidelity prototypes because I want to see how people interact with buttons, icons and other controls. Testing lower-fidelity prototypes can help you learn whether users share your mental model of the app, but you don’t gain insight into whether a particular icon makes sense to someone who is using the app for the first time.

Having started the project, I needed to set up the basic framework for the prototype.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30083482-76f6-4667-b545-da29f14181e1/axurestartproject-550.png" alt="The project is organized as a simple one-page canvas" /><br>
<em>I started my project with one page in the “Sitemap” panel. I placed a rectangle that was 320 × 460 pixels on the page to create a canvas to work on.</em>

### Create Masters for Reusable Components

The first thing I did was create a page header by using a “master,” which is a reusable component that can be added to any page in Axure. Masters are powerful because any change you make to one is reflected in every instance of it in your prototype. I created a 300 × 50-pixel master that would hold the page header for all screens of the app other than the home screen.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbc714da-5f0d-4258-8774-fb59ae2c1b81/header-550.png" alt="The page header is created as a master" /><br>
<em>The project now had one page and one master.</em>

### Use Dynamic Panels for Multiple Screens and Screen States

The next step was to place a “dynamic panel” named “ContentPanel” on the canvas in the top-left corner, <code>(X = 0, Y = 0)</code>. A dynamic panel is a widget that can contain several of what Axure refers to as “states,” which are different views of some portion of the screen based on some user action or the value of a variable. The ContentPanel was 320 × 415 pixels and would hold the contents of the prototype that lie above the iOS tab bar. Dynamic panels are scrollable, so your content can be taller than 415 pixels and will scroll from underneath the tab bar. To keep the scroll bars from appearing, I selected “Never Show Scroll” bars from the “Edit Dynamical Panel” context menu.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f418979a-0fee-4903-a740-9b14c95ba7af/nevershowscrollbars.png" alt="You can set scrollbars to never display in a dynamic panel" /><br>
<em>The project now has one dynamic panel, which was created with one state by default. More can be added, and they can be renamed. Scroll bars were set to never show. The “Pin to Browser…” menu option will be used later to fix the tab bar to the bottom of the iPhone’s screen.</em>

I then created a second dynamic panel called “TabBarPanel” that was 320 × 45 pixels and positioned it beneath ContentPanel. This panel was used to hold the tab bar image, and it brought the total page height to 460 pixels. This left 20 pixels for the iPhone’s status bar, which displays at the top of most iPhone app screens.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64433fa7-2f99-4600-bf30-5bb2cfe2491b/tabbar-550.png" alt="The tab bar image is placed in its own dynamic panel" /><br>
<em>The tab bar is a PNG image placed in the Tab Bar state of the TabBarPanel. This state always displays and is where the button tap actions are set.</em>

I had to create the container for the tab bar image as a dynamic panel so that I could anchor it to the browser window. When positioning TabBarPanel on the main screen, select <code>Order → Bring to Front</code> from the context menu to ensure that it is never covered by other content.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6f2a9f1-70ca-4d9a-98a4-ad4b04d079c1/pintobrowser.png" alt="Pin the tab bar to the browser so it stays anchored at the bottom of the iPhone screen" /><br>
<em>The tab bar will be anchored to the bottom of the iPhone screen, with the contents of longer pages scrolling underneath it.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af8de03-40b9-432e-aef0-496c8005a09f/pintobrowserdialog.png" alt="The Pin to Browser dialog is where you set the behavior of the tab bar" /><br>
<em>The “Pin to Browser” dialog allows you to specify the tab bar’s position.</em>

### Always Use Object Names

A note on naming objects: Axure allows you to name all objects that you include in a prototype, and I always try to do so. As your prototype becomes more complex or as more people contribute to its development, these names make objects easier to identify when you have to select an object from a long list. I name my objects using my own variation of Hungarian Notation, so a button’s name would take the form “btnButtonPurpose,” and a text input’s name would take the form of “txtTextInputPurpose”; you would create your own names for the parts after “btn” and “txt,” of course.</p>

### Adding Interactivity to Dynamic Panels

Now we need to create some states for the ContentPanel and get to work on the actual screens of the app. Your panel already has one state because that is created automatically and is named “State1.” You can rename a state by double-clicking on its name in the Dynamic Panel Manager, and I prefer doing that in order to keep the prototype more manageable. To create additional states, just select “Add State” from an existing state’s context menu.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43b20606-3794-4001-b41d-11d39af2c362/dynamicpanelmanager-458.png" alt="States give your prototype the dynamic behavior of a functioning application" /><br>
<em>You can add an unlimited number of states to a dynamic panel.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d72e27dc-248a-48dc-a108-e208ea794cf6/newstate-550.png" alt="A new empty state" /><br>
<em>When you first open a new state, you will see an empty view with a blue dotted lined, which represents the boundaries of the dynamic panel on the Axure page that contains it.</em>

The more States you create, the better you will be able to test different usage scenarios. Because the main goal of prototyping is to learn how people interact with your app, creating only a happy path might not be enough. Create alternative flows when possible if only to see what people try to do with your app. The alternative flow could be as simple as a screen that says, “This page is not working in this prototype,” which still allows you to see what they tapped and to probe them on it (a user tapping on a dead link or button tells you almost nothing).

Once I created the six empty States that I needed for my IxDA prototype, I was ready to tie it all together by setting up the tab bar. To create the tab bar with four buttons, I followed these steps:

1.  Have a visual designer create a background image of the tab bar and its icons.
2.  Position the tab bar at the bottom of the main app page, `(X = 0, Y = 416)`.
3.  Right-click the tab bar, and select `Convert → Convert to Dynamic Panel` from the context menu (you have to convert the master to a dynamic panel so that you can anchor it to the bottom of the screen).
4.  From the panel’s context menu, select `Edit Dynamic Panel → Pin to Browser` to anchor it at the bottom of the iPhone screen.
5.  Double-click “State1” in the Dynamic Panel Manager on the right side of the screen to rename and edit the panel. I called my single state “Tab Bar.”
6.  In the Tab Bar state of the TabBarPanel, create four borderless transparent rectangles for the button actions, and position one rectangle over each icon.
7.  Set the OnClick event for each transparent rectangle to “Set ContentPanel state to X,” where X is the name of the panel that you want to display. This is done by launching the Case Editor from the Interactions view of the Widget Properties panel.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d13ab9e1-07e4-4d24-96ae-16fd46af7a99/tabbarclickaction-550.png" alt="Setting up behaviors for the tab bar using OnClick events" /><br>
<em>Each of the transparent rectangles has an OnClick event to load a new panel view when it is tapped. The Widget Properties panel is showing the OnClick event for the Job Board icon. In a normal project, the tab bar would be positioned at the coordinates <code>X = 0, Y = 0</code>, but I’ve moved it down slightly to show the annotation indicators for the footnotes that you can create in the requirements documentation feature of Axure, which is not addressed in this article.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd264eaf-84ed-4563-993d-2fa8c6cadf18/caseeditor-550.png" alt="" /><br>
<em>The Case Editor is used to create behaviors in an Axure prototype. Behaviors can be triggered by user behaviors or by the value of a variable set by an earlier user behavior.</em>

### Axure Event Types

You can trigger interactions or set variables in your Axure prototype using the many built-in actions, such as OnClick, OnMouseEnter, OnMouseOut, OnKeyUp, OnFocus, OnLostFocus, OnChange, and OnPanelStateChange. For mobile apps, Axure 6.5 introduced OnSwipeLeft and OnSwipeRight events, which allow you to swipe to the previous and next screens as though you were moving through a deck of cards. Axure’s website maintains pages for <a href="https://www.axure.com/basic-interactions">basic interactions</a> and more <a href="https://www.axure.com/dynamic-panels-advanced">advanced uses of dynamic panels</a>.

Once I had a main page, my dynamic panel states, and my tab bar, I was ready to start building the app’s content.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/727151d9-3dd2-491a-bf70-f43edfbac797/axureproject-550.png" alt="The protoype is almost complete" /><br>
<em>The prototype now has one page, one master, the tab bar Dynamic Panel, a dynamic panel with six states, and the home screen design.</em>

The prototype was almost done at this point. All I had to do was create the other five screens that would be stored in the different states of the ContentPanel. In addition to the four screens reached from the tab bar, the prototype included a contact form and a form response screen.</p>

### Focus on Your Forms and Icons

On the Contact Form screen, I wanted to capture the user’s name, email address and textual message and store them in variables for possible later use. The way I did this was to use the “Send Message” button’s OnClick event to store the values from the three fields in three separate variables. I also constructed the message that will display the user’s name and email address on the Form Response screen by connecting text strings and variables in the Case Editor. After capturing the data and preparing the response message, I set the ContentPanel to show the Form Response state. Axure supports chaining events together to create fairly robust screen flows.

If my prototype had multiple Axure pages, I could have used the OnPageLoad event on the Form Response screen to construct the feedback message to the user. But that event is not available to you when you are switching dynamic panel view states. The need to use the OnPageLoad event is one of the factors to consider when deciding how to organize your prototype.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a930433-d660-4ccb-8c03-6d895ce547a3/contactform-550.png" alt="Setting up the behaviors for the contact form" /><br>
<em>The Send Message button tap is set up to do three things: capture the form field data as individual variables, build the response message that the user will see, and send the user to the Form Response screen.</em>

Forms are definitely one of the most important areas of your prototype to test. In showing my prototype to a few people before our IxDA event, I learned that some found it annoying to have to fill out separate fields for their first and last name. Because the purpose of the screen was to send a simple message, there was no need to collect two separate pieces of data. So, I merged them into one field, which also allowed people to enter just a first name if they wished. For every form input that you want to place on a screen, ask yourself whether it is really necessary for the user to complete the task. Anything you can do to reduce the interaction cost will make your app more usable.

Icons are another important area to prototype, and you should aim for the highest fidelity possible with those because you’ll want to test what might ultimately end up in the app. Because icon design is an art form, try to use standard system icons where possible, but be sure to test when you opt for custom icons.

So, at this point, the prototype was complete.</p>

### Generating the Prototype

Once I was ready to generate the prototype, I used the Mobile/Device panel of the Generate Prototype dialog to generate the <code>viewport</code> meta tags for iOS and Android. The <code>viewport</code> meta tag is used to make sure that the prototype displays at an appropriate width and is not scaled down to fit the entire page in the mobile browser’s viewport. Even when you’re simulating a mobile app, Axure will generate HTML files that are displayed in the device’s native browser, so correct use of the <code>viewport</code> tag is a must.

These are the <code>viewport</code> meta tags that I generate for handheld mobile prototypes:

<strong>iPhone</strong>:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" /&gt;</code></pre>

<strong>Android</strong>:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=480, target-densityDpi=device-dpi" /&gt;</code></pre>

Axure 6.5 also has additional options for iOS devices, such as hiding the browser’s address and navigation bars, creating a home screen icon, and creating a splash screen for the iPhone and iPad. Hiding the browser’s chrome and using a splash screen will give your HTML-based prototype the look and feel of a native iOS app.

Now that the prototype is complete, you just need to place the HTML and other files that Axure generates onto a Web server that your in-house device or test participant’s device can access. I usually use Dropbox or a personal Web server for this. You can also use AxShare, a free service from Axure that let’s you host up to 10 prototypes, with discussion features so that your team can work out the final design specifications before entering the build phase. When testing, try to avoid Wi-Fi connections because smartphone carrier networks are usually slower and will give you a more realistic feel for an app’s performance, especially an app for the mobile Web. A slower connection might also cause a test participant to volunteer useful information about how often they experience a slow app and slow Web page response. This contextual information is extremely useful to have when designing your product.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/730d8c0a-df33-4884-a5ec-ecd06c4d241e/generateprototypedialog-550.png" alt="The Generate Prototype Dialog" /><br>
<em>Generating a prototype for an iPhone or iPad app allows you to produce an HTML prototype that feels and acts like a native app.</em>

### Test It in the Wild

Another essential part of prototyping and testing is doing it in the field. People use their mobile devices on noisy trains, in poorly lit rooms and sometimes with conversations going on around them. Lab-based testing eliminates many of these factors, which can lead to inaccurate interpretations of the test results. One in-field test of mine that always comes to mind was of a guy using a three-year-old BlackBerry in a Starbucks. I really got a feel for how painful every image download was to his overall experience of my mobile website.</p>

## Conclusion

As you can see, Axure enables you to quickly create a prototype for a mobile app or website, with no investment in development. By prototyping and testing in the field or in a lab, you can validate your design before ever touching more expensive programming resources. You can also easily update the prototype in the middle of a test cycle to quickly test new findings, something that is harder to do if you are testing with functioning application code or clickable wireframes.

This article touched on just a few of the capabilities of Axure. The tool has many native iOS and Android widgets and form controls that can be used for much more robust native app prototypes. There are also other ways to organize your prototype; the only correct way is to do whatever works best for your project. The important thing is to build the prototype quickly, test it, fail fast, learn and iterate on the design — because that learning is what makes prototyping essential to any successful mobile design project.</p>

### Resources

*   [A Deep Dive Into Axure 8: A Comprehensive Review](https://www.smashingmagazine.com/2016/07/a-deep-dive-into-axure-8-a-comprehensive-review/)
*   [Creating Responsive Prototypes With Adaptive Views In Axure RP 7](https://www.smashingmagazine.com/2014/02/creating-responsive-prototypes-with-adaptive-views-in-axure-rp-7/)
*   [Factors In Selecting A Mobile Prototyping Tool](https://www.smashingmagazine.com/2016/04/factors-selecting-mobile-prototyping-tool/)
*   [Mobile Prototyping With Proto.io](https://www.smashingmagazine.com/2015/02/mobile-prototyping-with-protoio/)

<em>(al) (il)</em>

