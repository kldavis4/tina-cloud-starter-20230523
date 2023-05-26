---
title: How To Create Your Own Front-End Website Testing Plan
slug: how-to-create-your-own-front-end-website-testing-plan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f4bc67-7129-4ab8-8ec2-ddf3804828a8/testing-excerpt.png
date: 2014-11-24T20:12:08.000Z
author: lawrence-howlett
description: >-
  So, your designers and developers have created a fantastic front-end design,
  which the client is delighted with, and your job now is to test it. Your heart
  begins to sink: Think of all the browsers, all the devices and **all of these
  web pages you’ve got to test**, not to mention the iterations and bug fixes.
  You need a front-end testing plan.

  This article shows you what to consider when creating a front-end testing plan
  and how to test efficiently accross browsers, devices and web pages.
categories:
  - Coding
  - Mobile
  - Testing
  - Devices
  - Web Development
---
So, your designers and developers have created a fantastic front-end design, which the client is delighted with, and your job now is to test it. Your heart begins to sink: Think of all the browsers, all the devices and <strong>all of these web pages you’ve got to test</strong>, not to mention the iterations and bug fixes. You need a front-end testing plan.

This article shows you what to consider when creating a front-end testing plan and how to test efficiently accross browsers, devices and web pages.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Noah’s Transition To Mobile Usability Testing](https://www.smashingmagazine.com/2016/02/mobile-usability-testing/)
*   [The Basics Of Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [High-Impact, Minimal-Effort Cross-Browser Testing](https://www.smashingmagazine.com/2016/02/high-impact-minimal-effort-cross-browser-testing/)

## Benefits Of A Front-End Testing Plan

*   **Clarity on project’s scope** Knowing which browsers and devices are within the project’s specification will help you to focus and will reduce development time and costs.
*   **Reduced client friction**.  This is done by showing detailed reports of completed test plans.
*   **Confidence in deploying the project**.  This comes from knowing you’ve thoroughly tested the project.

{{% feature-panel %}}

In my experience, front-end website mockups are not extensively tested before they are handed over to the back-end development team, the reason being time and budget constraints. They’re usually tested in the front-end developer’s browser of choice and maybe on their smartphone. So, when we came up against a monster of a project, <a href="https://www.dad.info/">Dad Info</a>, which has a ton of responsive page types, we needed a plan to methodically and efficiently test functionality and performance across platforms and across devices.

Dad Info is a not-for-profit website, built on Joomla, that aims to help fathers in need, whatever their situation. Last year, it helped over 500,000 dads and delivered 220,000 pages of information every month. I will be using Dad Info as a case study throughout to demonstrate how to create and complete your own front-end testing plan.</p>

## Let’s Tool Up

Before getting started, you’re going to need to tool up. In this article, I’ll use the following toolkit to complete the testing process:

*   [Asana](https://asana.com) Used for bug-tracking and team management
*   [Chrome Developer Tools](https://developer.chrome.com/devtools) Used for inspecting, debugging and profiling
*   Windows’ Snipping Tool (or `Shift + Command + 4` on a Mac)
*   [BrowserStack](https://www.browserstack.com) Used to test cross-browser functionality on multiple virtual machines and emulators
*   Devices Ideally, you’ll want real devices. We have iPhone 4, 5 and 6; HTC One M8; Samsung Galaxy S5; Nokia Lumia 1520; Google Nexus 5; BlackBerry Curve; iPad 2; and Asus VivoTab Smart. If you don’t have these, you can use BrowserStack’s emulators.
*   [Google’s PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
*   [Pingdom Website Speed Test](https://tools.pingdom.com)
*   [Screenr](https://www.screenr.com) Web-based screen recording, with sharing capabilities

## What Are We Testing?

Because we’re front-end testers, our job is to know exactly what we are testing. We might not always find bugs per se; rather, we might find that something isn’t working as expected or that the developer has misunderstood the functionality requirements. Having a detailed specification up front that all stakeholders have agreed too will help to avoid some of these problems entirely. Later on in the Dad Info case study, we will go through a front-end specification to test the home page.</p>

## Who Are We Testing For?

First of all, you will need to understand your audience and how they will be consuming the website. Here are a few quick questions you should always ask:

*   What are the most **popular devices** your audience uses?
*   What **operating system** and **browser combinations** are most popular among your audience?
*   What **connection speeds** do they have (3G, 4G, broadband/fibre)?
*   **How tech-savvy** are they? We can make a judgment call here based on the topic of the website, their devices and their demographics.

For our Dad Info case study, the answers would be as follows:

*   iPhone 5, iPad 2+, desktop (1024 pixels and up)
*   Windows 7 Chrome, Windows 8 Chrome, Windows 8 Internet Explorer 10, OS X Safari, iOS 6 Safari
*   Broadband and 4G (a lot of city workers)
*   Our audience is mainly men between 18 and 35 years of age, fairly tech-savvy, with a smartphone in their pocket and an understanding of social media applications such as Facebook and Twitter.

So, how does this help us carry out a front-end test plan?

Armed with this information, we can instantly break down our huge to-do list into segments that are relevant to our audience and that prioritize our testing methodology. For functionality, we know which devices and browser to test in; for performance, we know what connections to test on; and for usability, we know that our audience uses social media applications, so we can include interface elements that they would be familiar with.</p>

## Know Your Limits

Know the limits of your project. At some point, you’re going to have a “That’s good enough” conversation with yourself. Projects limits are usually controlled by a few factors:

*   **Budget**.  Remember that you should charge for testing. A lot of designers don’t, which is crazy. Testing is time-consuming — and, being designers and developers, our product is time.
*   **Timeline**.  Include testing in the project’s timeline. It’s often left off the list and, therefore, rushed.
*   **Scope**.  Not every website needs to work on hundreds of devices. Figure out the main use case, and focus on fulfilling that audience’s requirements.</p>

### Browser and Device Support Levels

To set the scope of browser and device support easily with clients and to avoid those “bad conversations,” we’ve found that being up front about our “levels of support” really helps. Below are some simple definitions that you can apply to each page type you test.</p>

<strong>Support level 1: fully supported browsers and devices</strong>

*   All content must be readable.
*   All functionality must work.
*   Deviation from approved graphic design must be minimized.</p>

<strong>Support level 2: partially supported browsers and devices</strong>

*   All content must be readable.
*   Navigation must work.
*   Business login functionality must degrade gracefully.
*   Any degradation to presentation must not obscure content.</p>

<strong>Support level 3: unsupported browsers and devices</strong>

*   No support or testing is required.</p>

### Performance Support Levels

You might also want to agree with your client on a performance target. The quick and dirty method here is to agree on a score to reach in Google’s PageSpeed Insights and Pingdom’s Website Speed Test. Normally, we aim for at least 85 out of 100.

## Tools For Managing Your Test Plan

It doesn’t matter what tools you use. I use <a href="https://asana.com">Asana</a> and <a href="https://bugherd.com">BugHerd</a>; you could use a simple spreadsheet. It comes down to what works best for you. At a minimum, your tool should be able to do the following:

*   add bugs, issues and tasks in an ordered and segmented list, with the ability to tag (“priority, system critical, etc.);
*   assign bugs, issues and tasks to members of your team (or to yourself), with due dates;
*   comment on bugs, issues and tasks, with a date-ordered history thread;
*   upload screenshots, videos and documents related to bugs, issues and tasks;
*   mark a bug, issue or task as resolved or completed;
*   report on completed versus remaining bugs, issues and tasks.</p>

## How To Describe Bugs And Issues

Ever got a bug report from your client that stated, “I clicked on the blog and it doesn’t work”? Useless, right! So, what does a well-written bug report look like?

*   **Be specific**.  Without being wordy, clearly summarize the problem. Do not combine multiple bugs into one report; rather, submit a separate report for each issue.
*   **Show how to replicate**.  Detail step by step exactly what you did and what issue occurred as a result.
*   **Limit pronouns**.  Descriptions like “I clicked it and the window didn’t appear” are very unclear. Instead, “I clicked the ‘Submit’ button and the window marked ‘Registration’ did not load” tells the developer exactly what you did and what happened.
*   **Read what you’ve written** Does it make sense? Do you think it’s clear? Can you replicate the bug by following your own steps?

## Setting Up Your Front-End Test Plan

So far, you have collected a bunch of useful information and data, but you’re going to need a proper testing plan to succeed as a front-end tester. Without one, you’re shooting in the dark. So, what exactly does a front-end testing plan look like? In its simplest form, it’s a to-do list, with a bunch of tasks for testing each of your web page types against a set of agreed criteria. The best way to explain this is through a case study.</p>

## Case Study: Front-End Test Plan For Dad Info’s Home Page

### Test Plan Documentation

Here, we lay out an overview to give the tester some context about the project. And we let them know what we want tested, on which devices and browsers and how long they have to do it.</p>

<strong>Budget:</strong>

*   total of 10 days for testing
*   use one and a half days for front-end testing of home page

<strong>Timeline:</strong>

*   complete initial testing within one day, with feedback to front-end developers completed the same day
*   three days for fixing bugs
*   a further half day for retesting bugs

<strong>Scope:</strong>

*   Support level 1 (browsers):
    *   Windows 8: IE 10+, Chrome (latest), Firefox (latest), Safari (latest)
    *   Mac OS X Mavericks: Chrome (latest), Firefox (latest), Safari (latest)
*   Support level 1 (devices):
    *   iPhone 4 / 5, iPad 2, Asus VivoTab Smart
*   Support level 2:
    *   Windows 7: IE 9+, Chrome (latest), Firefox (latest), Safari (latest)
    *   Windows XP: IE 8, Chrome (latest), Firefox (latest), Safari (latest)
*   Support level 3:
    *   anything else

For this project, we require three <strong>reports</strong> to assure the client that the page has undergone and passed the testing process:

*   browser and device report: support level 1 and 2
*   responsive report: support level 1
*   performance report: minimum 85 out of 100

### Original Approved Design

Having a visual representation of what you are working towards is important to ensuring that graceful degradation is within acceptable limits and that the presentation doesn’t change much between browsers. We’ve added this image to the test plan documentation:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7e4f6df-a745-4158-9a83-97d704cabffa/01-dad-homepage-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a752e59-4686-4cde-b91a-d4c8dc55ad0f/01-dad-homepage-opt-small.jpg" alt="Homepage design of Dad Info" width="500" height="600" /></a><figcaption>Home page mock-up of Dad Info (Image: New Edge Media) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7e4f6df-a745-4158-9a83-97d704cabffa/01-dad-homepage-opt.jpg">View large version</a>)</figcaption></figure>

### Details of Page Functionality

In the home page design, I’ve highlighted all of the functionality that needs to be tested, highlighting them with block overlays. This helps everyone involved to know exactly what to look for and puts us all on the same page. I’ve also added this to the test plan documentation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60f85e40-dcfb-4cea-9ff2-2e3377b5c64b/02-homepage-overlay-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a82eb8be-e73c-4a9a-8a57-9ae5dc6b9956/02-homepage-overlay-opt-small.jpg" alt="Home page graphic design mock up with testing area overlays of DAD." width="500" height="599" /></a><figcaption>Home page mock-up, with overlays for testing areas (Image: New Edge Media) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60f85e40-dcfb-4cea-9ff2-2e3377b5c64b/02-homepage-overlay-opt.jpg">View large version</a>)</figcaption></figure>

Based on these overlays, we can produce a full list of functionality.

#### Search form

*   Click or touch in the search box and then press the search icon to submit the form.

#### Navigation:

*   Hover over navigation item to display white highlight.
*   Hover over navigation item “Family” to show drop-down mega menu.

#### Image carousel 1:

*   Press the up and down arrows to browse the slides.
*   Press the pagination elements to skip to a particular slide.
*   Swipe through the slides on touch devices.

#### News feed:

*   Hover over the headings to change their color.

#### Image carousel 2:

*   Press the up and down arrows to browse the slides.
*   Press the pagination elements to skip to a particular slide.
*   Swipe through the slides on touch devices.

#### Call-to-action block 1:

*   Hover over title to change it

#### Image carousel 3:

*   Press the up and down arrows to browse the slides.

#### Twitter:

*   No special front-end functionality

#### Forum:

*   No special front-end functionality

#### Topics:

*   Hover over a support topic to reveal a picture to the right, with a description. Click “More” to go to a new page.

#### Footer links:

*   Hover over an icon to change its opacity.

#### Newsletter:

*   Clicking in or touching the “Enter email address” box should work.
*   Press “Subscribe” to submit the form.

#### Footer bottom:

*   No special front-end functionality

### Browser and Device Report

Whether you decide to use a tool like Asana, BugHerd or Trello, your job as a tester is essentially to collect the following information to relay back to your front-end developers (or to use yourself if you’re solo). To quickly go through all of the browsers, I use BrowserStack, setting up virtual machines that run the OS and browser combinations that I require.
<table class="article-table four-columns"><br>
<tbody>
<tr>
<th>Test Item</th>
<th>Browser/Device</th>
<th>Pass/Fail</th>
<th>Bug/Issue Description</th>
</tr>
<tr>
<td>search form
1.a</td>
<td>Windows 8 (IE 10)</td>
<td>pass</td>
<td></td>
</tr>
<tr>
<td>navigation
1.a</td>
<td>Windows 8 (IE 10)</td>
<td>pass</td>
<td></td>
</tr>
<tr>
<td>navigation
1.b</td>
<td>Windows 8 (IE 10)</td>
<td>fail</td>
<td>Cannot move mouse to mega menu area without it disappearing. See <a href="https://screenr.com">this Screenr recording</a>.</td>
</tr>
<tr>
<td>image carousel
1 - 3.a</td>
<td>Windows 8 (IE 10)</td>
<td>fail</td>
<td>The left and right arrows in the yellow box do not scroll slide 4 back to slide 1.</td>
</tr>
</tbody>
</table>

It’s a methodical job of working through all of the browser and device combinations until you have completed the same tests for each one.</p>

### Real Bug From Dad Info

*   **item:** navigation’s “Join” button
*   **browser/device:** Windows 8, IE 10, 1024-pixel screen width
*   **pass/fail:** fail
*   **bug description:** The “Join” button overlaps the Twitter button, highlighted in blue. See attached screenshot.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eed1952e-63d9-41db-b136-2ade0a19277d/03-issuetracking-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e186a2d7-a1bd-4701-94db-5820f8325cac/03-issuetracking-opt-small.png" alt="03-issuetracking-opt-small" width="500" height="376" /></a><figcaption>Screenshot of “Join” button bug (Image: New Edge Media) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eed1952e-63d9-41db-b136-2ade0a19277d/03-issuetracking-opt.png">View large version</a>)</figcaption></figure>

### Responsive Report

In the report on responsiveness, we are specifically testing elements and functionality that change as the screen’s canvas reduces in size. This includes navigation, page layout and images.

We have a few possible testing methods:

*   **Resize the browser’s window** This is the quick and dirty method, grabbing your browser’s window by the corner and dragging across the break points to see what happens. This is a great way to quickly scan the overall responsiveness of a website to see which elements change.
*   **Use emulators**.  BrowserStack emulates the majority of popular devices, and in my experience it is good enough for testing.
*   **Use real devices**.  The expensive option! This entails thoroughly testing on actual devices in your hand. Getting a screenshot usually requires capturing a photo, emailing it to yourself and then annotating in Photoshop. There are some options for screen recording, including [UX Recorder](https://www.uxrecorder.com/) for the iPhone.

For the Dad Info project, we used a mixture of all three. The front-end developers resized their browser to get the gist of responsive elements, while the quality assurance team used emulators and real devices to complete the testing process to the client’s satisfaction.</p>

### Real Bug From Dad Info

*   **Item:** image carousel 1
*   **Browser/device:** iPhone 5, iOS 7
*   **Pass/fail:** fail
*   **Bug description:** The margins set at the bottom of the carousel push the “News support your child…” title for the featured article too far down. Featured article title 1 should be 20 pixels below image carousel 1\. See attached screenshot.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e29d3c-c81f-40f5-83e1-c94c2849da6e/04-iphone-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e66610f4-2f3a-404e-a620-e03806f1ce3c/04-iphone-opt-small.jpg" alt="04-iphone-opt-small" width="338" height="600" /></a><figcaption>Screenshot of iPhone bug (Image: New Edge Media) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e29d3c-c81f-40f5-83e1-c94c2849da6e/04-iphone-opt.jpg">View large version</a>)</figcaption></figure>

### Performance Report

In the performance report, we are looking to score a minimum of 85 out of 100 in Google’s PageSpeed Insights. To get the client to sign off on the report, we’ve included a screenshot of the page speed analysis. Of course, if it doesn’t pass the agreed upon standard, then we provide feedback to the front-end development team using the bug-tracking report template.

Tip: We use boilerplates (stored in GitHub repositories, which we fork) for our content management system and Magento builds, whose performance is already optimized. This saves us a bunch of time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be438496-530b-4357-a583-b16525d2833f/05-google-desktop-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7849d22-960f-4527-8b0d-fc8663e2fcc0/05-google-desktop-opt-small.png" alt="05-google-desktop-opt-small" width="499" height="591" /></a><figcaption>The desktop version passed Google’s PageSpeed test. (Image: New Edge Media) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be438496-530b-4357-a583-b16525d2833f/05-google-desktop-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74f3fc15-7da0-4197-a96f-ca6cdafb2b1a/06-google-mobile-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3af28b9-d54b-431c-bf71-ab9963b8aa59/06-google-mobile-opt-small.png" alt="06-google-mobile-opt-small" width="499" height="600" /></a><figcaption>The mobile version passed Google’s PageSpeed test. (Image: <a href="https://www.google.co.uk">Google</a>)(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74f3fc15-7da0-4197-a96f-ca6cdafb2b1a/06-google-mobile-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc277c4f-4365-4d74-bde0-2eadb09c43ea/07-pingtest-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dbf30f3-b89d-4d10-999f-51ad3ff9765d/07-pingtest-opt-small.png" alt="07-pingtest-opt-small" width="500" height="180" /></a><figcaption>The website passed Pingdom’s speed test. (Image: <a href="https://www.google.co.uk">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc277c4f-4365-4d74-bde0-2eadb09c43ea/07-pingtest-opt.png">View large version</a>)</figcaption></figure>

The reporting is complete. We have just a few issues to send back to the front-end developers to wrap up the front-end build. Once it gets to the quality assurance team, we will retest the elements that kept the project from getting a clean bill of health.</p>

## Automated testing tools for visual regression

One thing to consider is the need for visual regression testing post go live, allowing you to compare editions of pages to see if your new feature, css update or class rename has caused any problems.

Visual regression tests essentially do a DIFF on the two versions and outline (in varying ways) the differences between them, highlighting potential issues.

Here are some great resources to get you started:

*   [Wraith](https://github.com/BBC-News/wraith)
*   [PhantomCSS](https://github.com/Huddle/PhantomCSS)
*   [Huxley](https://github.com/facebook/huxley)
*   [CSS Regression Testing with Resemble.js](https://www.lullabot.com/blog/article/css-regression-testing-resemblejs)
*   CSSte.st

## Summing Up

Testing is a critical process that developers should integrate into their workflow to minimize the number of bugs that get caught in the quality assurance phase. Front-end testing also needs to be budgeted for — with time, resources and money. The process will appeal to methodical types because they don’t need to be creatively skilled to carry it out. Tools are out there to make your life a little easier, but they won’t do the work for you. Whichever tool you pick, stick with it, define a process and put the effort in. The result will be a better website, with significantly fewer bugs, which your client will love and which will reduce the number of “Why isn’t this working?” phone calls and emails on Sunday night.</p>

### Your Action Plan

Reading what you should do is one thing; actually doing it quite another. So, I suggest carrying out the following actions right now:

1.  List the devices you have on hand, or check out [Open Device Lab](https://opendevicelab.com) to find devices near you.
2.  Create support levels for your chosen browsers and devices.
3.  Make time for testing in your timelines and quotations.
4.  Select a management tool (Asana, BugHerd, etc.), or set up a spreadsheet to track bugs, issues and tasks.
5.  Select the first project to apply your test plan to.
6.  Go do it!

Front-end testing will give you and your client confidence in the finished project. You’ll know the website has been thoroughly tested for bugs and is ready for the world to see.

{{< signature "da, ml, al" >}}

