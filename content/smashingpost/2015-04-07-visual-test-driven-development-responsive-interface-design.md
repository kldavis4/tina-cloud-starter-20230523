---
title: Visual Test-Driven Development For Responsive Interface Design
slug: visual-test-driven-development-responsive-interface-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b07ad7a-2e0a-4038-99ab-e76bc56dd76d/devices-illu-opt.png
date: 2015-04-07T19:58:21.000Z
author: ivanishubin
description: >-
  Testing responsive websites is a laborious task. Until now, implementing a
  stable and maintainable automated solution for cross-browser and cross-device
  testing of a responsive layout has been nearly impossible. But what if we had
  **an opportunity to write visual tests for responsive websites**? What if we
  could describe the look and feel of an application and put this directly into
  our tests?

  Upon considering this question, I decided to also look at another interesting
  side of visual testing. For quite a long time I have been a fan of the
  test-driven development (TDD) methodology. It helps me in my daily programming
  work. TDD enables me to formalize the task and to make sure everything is
  implemented according to the requirements.
categories:
  - Mobile
  - Testing
  - Responsive Design
  - Interfaces
---
Testing responsive websites is a laborious task. Until now, implementing a stable and maintainable automated solution for cross-browser and cross-device testing of a responsive layout has been nearly impossible. But what if we had <strong>an opportunity to write visual tests for responsive websites</strong>? What if we could describe the look and feel of an application and put this directly into our tests?

Upon considering this question, I decided to also look at another interesting side of visual testing. For quite a long time I have been a fan of the <a href="https://en.wikipedia.org/wiki/Test-driven_development">test-driven development</a> (TDD) methodology. It helps me in my daily programming work. TDD enables me to formalize the task and to make sure everything is implemented according to the requirements.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Basics Of Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [The Art Of Layout Testing With Galen Framework](https://www.smashingmagazine.com/2016/06/the-art-of-layout-testing-with-galen-framework/)
*   [Diverse Test-Automation Frameworks For React Native Apps](https://www.smashingmagazine.com/2016/08/test-automation-frameworks-for-react-native-apps/)

More importantly, it helps me catch a lot of bugs before they go live. For the last seven years, my main focus has been testing automation for a big enterprise project. Over time, I became obsessed with the idea of applying automated testing using the TDD methodology to the look and feel of responsive websites. After years of research, I came up with the <a href="https://galenframework.com">Galen Framework</a> — a tool and a special language for visual testing. This has been running for a while, and once the language became mature enough, I decided to perform an experiment with visual test-driven development.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d907db3c-4314-4488-8185-29f28b1f3154/01-responsive-design-opt.png" alt="01-responsive-design-opt" /></figure>

In this article, I’ll describe this experiment in detail and propose TDD as a methodology for front-end development. We will look at the new visual testing technique and examine how to get the most out of it.</p>

## Introduction To Galen Framework

Though a new technology, Galen Framework has already been used by some big companies, such as eBay, SkyScanner, Gumtree and Bestseller.nl, and it was also used to test the <a href="https://www.washingtonpost.com/">Washington Post</a>’s website. Besides enterprise companies, it is also used in web studios, such as <a href="https://adcisolutions.com/">ADCI Solutions</a>. The framework is open-source and hosted on <a href="https://github.com/galenframework/galen">GitHub</a>, so anyone can participate in the project and contribute to the code.

The fundamental testing concept in Galen Framework centers on checking the location and size of all page elements relative to each other. This way, you can describe the layout for any browser window’s size and you don’t have to use absolute positioning.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1265f76-0768-423c-9638-38c5d03f5e0c/02-galen-introduction-01-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1d2d0f4-a71b-41b5-896b-508b7c6d0599/02-galen-introduction-01-opt-small.jpg" alt="A concept of visual testing with Galen Framework" /></a><figcaption>A concept of visual testing with Galen Framework (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1265f76-0768-423c-9638-38c5d03f5e0c/02-galen-introduction-01-opt.jpg">View large version</a>)</figcaption></figure>

The <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/">Galen Specs</a> language was designed to resemble natural English as closely as possible and has been implemented in a semi-Markdown way. So, what does it look like? Well, imagine that you want to check that a "Login" button is located next to a "Cancel" button and has a 10-pixel margin from the right side and that they are aligned horizontally. We can transform that statement into Galen Specs:

<pre><code class="language-markup">
login-button
  near: cancel-button 10px right
  aligned horizontally all: cancel-button
</code></pre>

Consider another example. What if we want to check that a logo should be located inside the header in the top-left corner, with approximately a 20-pixel margin? Here is how you do it:

<pre><code class="language-markup">
logo
  inside: header 17 to 22px top left
</code></pre>

We can even use a shortcut:

<pre><code class="language-markup">
logo
  inside: header ~ 20 px top left
</code></pre>

A lot of other check types exist, and all of them are described in detail in the <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#SpecsReference">official documentation</a>. The learning curve is not very steep. The structure of Galen Specs is pretty simple, and once you understand it, testing becomes easy. We’ll get back to the experiment I mentioned at the beginning in a moment, but first let me give you a bit of insight into TDD as a whole.</p>

## Test-Driven Development

TDD has been used for quite a long time and has proven itself to be a strong methodology for building solid applications. In the beginning, you might feel like you are wasting time writing tests, but you will spend much less time later on finding the root causes of problems. More importantly, you can concentrate on small units of code and make sure each unit is of good quality. The numbers of tests will grow with the main code, and essentially, you’ll get early feedback on any problems in your application.</p>

## A Concept Of Visual Test-Driven Development

So, how do we approach TDD for HTML and CSS? Obviously, it is a bit different from traditional TDD, where tests are implemented in a <a href="https://en.wikipedia.org/wiki/White-box_testing">white box</a>. That is why I added the word "visual" to it, as with the Galen Framework: We are testing how a website is rendered in the browser, and we don’t particularly care about its internal structure. So, it sounds more like black-box or gray-box testing. In this article, I will show you how to build a responsive web page by writing the layout tests first before we even have any page. One thing to keep in mind is that our tests will also serve as a source of documentation, explaining how the page should look on any device. With all this in mind, let’s clarify the process.

1.  **Design and test** Imagine how the page should look. Write a sketch, write a test.
2.  **Code** Implement the HTML and CSS code, and pass the test.
3.  **Refactor** Improve the code and tests.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d0ab773-0714-444d-b85e-2fe4da76a971/03-tdd-scheme-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9cc1989-fdc8-4139-b619-afbb80aac155/03-tdd-scheme-opt-small.jpg" alt="A basic TDD scheme" /></a><figcaption>A basic TDD scheme (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1265f76-0768-423c-9638-38c5d03f5e0c/02-galen-introduction-01-opt.jpg">View large version</a>)</figcaption></figure>

We are going to break down the whole development process into small iterations. Another important rule: For each iteration, we shall implement only the code that is needed for the tests. This way, we’ll make sure that our test coverage is always close to 100% and that we don’t get distracted by things that are not declared in the current iteration. This article is based on the visual TDD experiment from <a href="https://github.com/galenframework/workshop-shopping-cart/">Workshop Shopping Cart</a>. It is a GitHub project, so you can track all of the code changes in it.</p>

## The Experiment

Imagine that we have decided to build a shopping-cart page and we want it to be responsive. The page’s functionality is the same as in any online store: Users should be able to review their shopping items, proceed to pay or go back.</p>

### Phase 1: Sketched Requirements

We sat down, thinking through all of the details, and we came up with this sketch:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91af629e-8ef7-4395-afd4-f75e30ee151c/04-initial-sketch-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0152fa32-d749-4d72-ae1c-1bf27cce3a6a/04-initial-sketch-opt-small.jpg" alt="Initial sketch of design" /></a><figcaption>Initial sketch of design (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91af629e-8ef7-4395-afd4-f75e30ee151c/04-initial-sketch-opt.jpg">View large version</a>)</figcaption></figure>

Looks OK for now. As you can see, we have three types of sketches: desktop, tablet and mobile. Now we can start implementing the tests.</p>

### Phase 2: Project Configuration

For this tutorial we don’t need any special IDE — any text editor will do. It’s going to be pretty simple. Let’s just create our project folder, <code>shopping-cart</code>, and in it create two folders: <code>website</code> and <code>galen-tests</code>. Of course, configuring a local webserver would be better, so that we can access the page through <code>https://localhost</code> in our tests. But because we have only one page, we can work with plain files for now, accessing them via <code>file:///…</code> URLs.</p>

<a href="https://galenframework.com/download/">Download</a> Galen Framework and <a href="https://galenframework.com/docs/getting-started-install-galen/">install it</a>. Galen Framework has installation scripts for Linux and Mac. If you are a Windows user, take a look at "<a href="https://mindengine.net/post/2014-01-08-configuring-galen-framework-for-windows/">Configuring Galen Framework for Windows</a>."

Create all of the folders that we discussed above:

<pre><code class="language-marku">
shopping-cart/
  |-- website/
  `-- galen-tests/
</code></pre>

That’s it for now.</p>

### Phase 3.1: Writing tests

Let’s think of how we can split our work into small iterations. The first thing we would think of is to build a basic page skeleton:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32bfa4e9-9906-4d2e-ad35-8e7ffbae42a8/05-skeleton-sketch-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8be21e88-752c-4384-a052-c6191dd85505/05-skeleton-sketch-opt-small.jpg" alt="Page skeleton sketch" /></a><figcaption>Page skeleton sketch (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32bfa4e9-9906-4d2e-ad35-8e7ffbae42a8/05-skeleton-sketch-opt.jpg">View large version</a>)</figcaption></figure>

This means that, at the moment, we have only five objects on the page: "Header," "Main," "Navigation," "Banner panel" and "Footer." Let’s start writing Galen tests for our skeleton. In the folder <code>galen-tests</code>, create another folder named <code>specs</code>. In it, we will keep all Galen Spec files.

Let’s create the first one, <code>galen-tests/specs/shopping-cart.spec</code>, with the following code:

<pre><code class="language-css">
=====================================
header          css #header
navigation      css #navigation
main            css #main-container
banner-panel    css #banner-panel
footer          css #footer
=====================================

@ *
--------------------
header
  inside: screen 0px top left right
  height: 60px

navigation
  inside: screen 0px left
  below: header 0px

footer
  inside: screen 0px bottom left right
  below: banner-panel 0px
  height: 100px

@ desktop
------------------
navigation
  width: 300px
  aligned horizontally all: main
  near: main 0px left

main
  below: header 0px

@ desktop, tablet
-------------------
banner-panel
  below: header 0px
  inside: screen 0px right
  width: 300px
  near: main 0px right
  aligned horizontally all: main

@ tablet
-----------------
navigation
  inside: screen 0px left right
  above: main 0px
  width: 60px

main
  inside: screen 0px left

@ mobile
----------------------
navigation
  inside: screen 0px left right
  above: main 0px
  height: &gt; 60px

main
  inside: screen 0px left right
  above: banner-panel 0px

banner-panel
  inside: screen 0px left right
  height: &gt; 50px
</code></pre>

As you can see, we’ve already defined some object locators in the beginning, even though we don’t have any HTML code yet. This might seem a bit weird, but on the other hand it could turn out to be a useful exercise. This way, we’ll have to think over our DOM structure up front, and we can already come up with some good ideas of how our HTML code could be structured. For instance, we already know that in our future page skeleton, we are going to have a <code>&lt;div id="header"&gt;…&lt;/div&gt;</code> element and <code>&lt;div id="footer"&gt;…&lt;/div&gt;</code>. The same goes for other page elements. And if for any reason we decide to change the DOM’s structure, we can always update our tests in a single place.

Now, let’s also prepare a test suite that will execute our tests for three sizes: desktop, tablet and mobile. To make it simple, we are going to emulate a mobile or tablet layout by resizing the browser’s window. Create a file named <code>galen-tests/shoppingCart.test</code> and put in the following code:

<pre><code class="language-markup">
@@ table devices
  | device    | size     |
  | mobile    | 500x700  |
  | tablet    | 900x600  |
  | desktop   | 1300x700 |

@@ parameterized using devices
Shopping cart on ${device} device
  ${websiteUrl} ${size}
    check specs/shopping-cart.spec --include "${device}"
</code></pre>

In the code above, we have declared a <code>devices</code> table containing settings for three screen sizes. Using this table, Galen Framework will invoke our test three times, each time with different <code>device</code> and <code>size</code> parameters. We’ve also defined a placeholder for the website’s URL, via the <code>${websiteUrl}</code> construction. We are going to provide this parameter later from the command line.</p>

### Phase 3.2: Writing Code

Because we have implemented the initial test code, we can start working on the HTML and CSS. For this experiment, I chose Twitter Bootstrap. You might think that Twitter Bootstrap is already well tested and responsive. Well, the point of visual TDD is to come up with solid tests and to build a pixel-perfect website. So, it doesn’t really matter which framework you use to build a website because in the end the only thing that Galen checks is the location of page elements on the screen. I picked Twitter Bootstrap merely to simplify the experiment because it already has some things I need, so I won’t have to waste time reimplementing them. Still, we have strict requirements in our Galen tests for the page skeleton, and we need to deliver a page according to those requirements. Download <a href="https://getbootstrap.com/">Twitter Bootstrap</a>, and copy all of its contents into the <code>website</code> folder. There, we should have the following structure:

<pre><code class="language-markup">
website/
  |-- css/
  | |-- bootstrap-theme.css
  | |-- bootstrap-theme.min.css
  | |-- bootstrap.css
  | `-- bootstrap.min.css
  |
  |-- fonts/
  `-- js/
    |-- bootstrap.js
    |-- bootstrap.min.js
    `-- npm.js
</code></pre>

Now, let’s actually write some HTML. Create a file named <code>shopping-cart.html</code> in the <code>website</code> folder with the following code:

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;
    &lt;title&gt;Galen Workshop - Shopping Cart&lt;/title&gt;

    &lt;!-- Bootstrap --&gt;
    &lt;link href="css/bootstrap.min.css" rel="stylesheet"&gt;

    &lt;link href="main.css" rel="stylesheet"&gt;

    &lt;!-- HTML5 shim and Respond.js for IE 8 support of HTML5 elements and media queries --&gt;
    &lt;!-- WARNING: Respond.js doesn't work if you view the page via file:// --&gt;
    &lt;!--[if lt IE 9]&gt;
    &lt;script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"&gt;&lt;/script&gt;
    &lt;script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"&gt;&lt;/script&gt;
    &lt;![endif]--&gt;

    &lt;!-- jQuery (necessary for Bootstrap's JavaScript plugins) --&gt;
    &lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"&gt;&lt;/script&gt;
    &lt;!-- Include all compiled plugins (below), or include individual files as needed --&gt;
    &lt;script src="js/bootstrap.min.js"&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;nav id="header" class="navbar" role="navigation"&gt;
      &lt;div class="container-fluid"&gt;
        &lt;div class="navbar-header"&gt;
          &lt;h3&gt;Header&lt;/h3&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/nav&gt;
    &lt;div id="middle"&gt;
      &lt;div class="row"&gt;
        &lt;div id="navigation"
            class="col-xs-12 col-sm-12 col-md-2 col-lg-2"&gt;
          Navigation
        &lt;/div&gt;
        &lt;div id="main-container"
            class="col-xs-12 col-sm-8 col-md-7 col-lg-7"&gt;
          Main container
        &lt;/div&gt;
        &lt;div id="banner-panel"
            class="col-xs-12 col-sm-4 col-md-3 col-lg-3"&gt;
          Banner panel
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
    &lt;div id="footer"&gt;
      &lt;p&gt;Footer&lt;/p&gt;
    &lt;/div&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Create a file named <code>main.css</code> in our <code>website</code> folder with the following contents:

<pre><code class="language-css">
#header {
  background: #2E849E;
  color: white;
  border-radius: 0;
}

#navigation {
  background: #faa;
  height: 100px;
}

#main-container {
  background: #afa;
  height: 100px;
}

#banner-panel {
  background: #aaf;
  height: 100px;
}

#footer {
  color: white;
  background: #222;
  height: 100px
}
</code></pre>

That’s it — we’re done with the code! You might want to check whether everything you made is same as in <a href="https://github.com/galenframework/workshop-shopping-cart/tree/v0.1">the GitHub repository</a>. Now we can run the tests and check that we’ve done everything well for this iteration.</p>

### Phase 3.3: Running Galen Tests

Because I haven’t configured a local web server, I decided to test it directly from my local file system. In my case, if I open this page in a browser, the URL would be <code>file:///home/ishubin/workspace/workshop-shopping-cart/website/shopping-cart.html</code>. So, below is how I am going to pass this URL to our tests:

<pre><code>galen test shoppingcart.test \
-DwebsiteUrl="file:///home/ishubin/workspace/workshop-shopping-cart/website/shopping-cart.html" \
--htmlreport reports</code></pre>

The command above will launch all of the tests and will generate an HTML report in the folder I’ve specified, <code>reports</code>. If you open the generated <code>reports/report.html</code> file in the browser, you should see this picture:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28fddc49-a9ea-43b2-bdb8-7bdfa62ab656/06-first-report-overview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6aad984-cfc9-4bd2-9209-2587da3b6822/06-first-report-overview-opt-small.png" alt="Report Overview" /></a><figcaption>Report overview (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28fddc49-a9ea-43b2-bdb8-7bdfa62ab656/06-first-report-overview-opt.png">View large version</a>)</figcaption></figure>

As you can see, we have some failures. If we click the "Shopping cart on desktop device" link, it takes us to a more detailed report.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99c5261e-a6f5-4fc6-bb91-71f6a153241e/07-first-detailed-report-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1830af43-ede3-4be0-a273-ca97d7b228fb/07-first-detailed-report-opt-small.png" alt="Detailed report of desktop tests" /></a><figcaption>Detailed report of desktop tests (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99c5261e-a6f5-4fc6-bb91-71f6a153241e/07-first-detailed-report-opt.png">View large version</a>)</figcaption></figure>

As you can see, the naming of sections isn’t all that pretty. Galen uses tag names by default. We will fix that a bit later. Let’s look at the error messages. There are a lot of them. Let’s just focus on the first failure for now. If you click it, you get a screenshot, highlighting the elements on it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a3480a7-8bbe-4175-9331-03b1677a2738/08-first-report-screenshot-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78094227-4332-4368-86aa-c0d0c136509a/08-first-report-screenshot-opt-small.png" alt="A screenshot of a failed layout" /></a><figcaption>A screenshot of a failed layout (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a3480a7-8bbe-4175-9331-03b1677a2738/08-first-report-screenshot-opt.png">View large version</a>)</figcaption></figure>

The error message we got was "Header is 15px right instead of 0px." What does that mean? Notice the misalignment of the right edges of the header and the banner panel? That’s right. The problem with this page is that the header’s width matches the viewport, but because the middle section is bigger, it is increasing the size of the screen. That also puts scroll bars on our page. And because we initially said to Galen that we want the header to be <code>inside: screen 0px top left right</code>, we meant that there should be no margin from the left and right edges. But there it is, so it is a bug.

Let’s look at another error message, "Navigation is 20px below header instead of 0px."

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1417bfaf-867c-4684-977f-ab907714b078/09-first-report-screenshot-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ec5383-2b1f-4d4b-ab56-502756de6155/09-first-report-screenshot-2-opt-small.png" alt="A screenshot of failed layout" /></a><figcaption>A screenshot of a failed layout (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1417bfaf-867c-4684-977f-ab907714b078/09-first-report-screenshot-2-opt.png">View large version</a>)</figcaption></figure>

Originally in our specification file, we stated that the navigation panel should be <code>below: header 0px</code>, meaning that it should not have any margin from the top. But in the screenshot we clearly see the gap between header and middle section. Again, that is a bug, and we have to fix it.</p>

### Phase 4: Fixing The Failed Tests

I have already prepared a fix for it in the GitHub repository with the <a href="https://github.com/galenframework/workshop-shopping-cart/tree/v0.1.1">v0.1.1 tag</a> Also with the fix, I decided to make the tests give better reports by naming the specification sections.

Let’s first fix our <code>shopping-cart.html</code>. Here is the changed <code>body</code> element:

<pre><code class="language-markup">
&lt;body&gt;
  &lt;nav id="header" class="navbar" role="navigation"&gt;
    &lt;div class="container-fluid"&gt;
      &lt;div class="navbar-header"&gt;
        Header
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/nav&gt;
    &lt;div id="middle" class="container-full"&gt;
      &lt;div class="row"&gt;
        &lt;div id="navigation"
           class="col-xs-12 col-sm-12 col-md-2 col-lg-2"&gt;
          Navigation
        &lt;/div&gt;
        &lt;div id="main-container"
           class="col-xs-12 col-sm-8 col-md-7 col-lg-7"&gt;
          Main container
        &lt;/div&gt;
        &lt;div id="banner-panel"
           class="col-xs-12 col-sm-4 col-md-3 col-lg-3"&gt;
          Banner panel
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;div id="footer" class="container-fluid"&gt;
    &lt;p&gt;Footer&lt;/p&gt;
  &lt;/div&gt;
&lt;/body&gt;
</code></pre>

And now let’s update the <code>main.css</code> file:

<pre><code class="language-css">
#header {
  background: #2E849E;
  color: white;
  border-radius: 0;
}

.navbar {
  margin-bottom: 0;
}

#navigation {
  background: #faa;
}

#main-container {
  background: #afa;
}

#banner-panel {
  background: #aaf;
}

.container-full {
  margin 0 auto;
  width: 100%;
}

.row {
  margin: 0;
}

#footer {
  color: white;
  background: #222;
  height: 100px
}
</code></pre>

And below is the change to the <code>homepage.spec</code> file. Here I’ve defined proper names for the sections. Now reading the test will be easier. Also, once we get a test report, it will be properly structured, which will make it easier to understand the feedback.</p>

<pre><code class="language-css">
=====================================
header          css #header
navigation      css #navigation
main            css #main-container
banner-panel    css #banner-panel
footer          css #footer
=====================================

@ Header | *
--------------------
header
  inside: screen 0px top left right
  height: 50px

@ Navigation | *
-------------------
navigation
  inside: screen 0px left
   below: header 0px

@^| desktop
-----------------------
navigation
  width: 200 to 350px
  aligned horizontally all: main
  near: main 0px left

@^| tablet
-----------------
navigation
  inside: screen 0px left right
  above: main 0px
  % height: 50 to 100px

@^| mobile
----------------------
navigation
  inside: screen 0px left right
  above: main 0px
  % height: &gt; 60px

@ Footer | *
-------------------
footer
  % inside: screen 0px bottom left right
  below: banner-panel 0px
  height: 100px

@ Main | desktop
-----------------------
main, banner-panel
  below: header 0px

@^| tablet
----------
main
  inside: screen 0px left
  below: navigation 0px

@^| mobile
------------------
main
  inside: screen 0px left right
  above: banner-panel 0px

Let’s first fix our <code>shopping-cart.html</code>. Here is the changed <code>body</code> element:

<pre><code class="language-markup">
&lt;body&gt;
  &lt;nav id="header" class="navbar" role="navigation"&gt;
    &lt;div class="container-fluid"&gt;
      &lt;div class="navbar-header"&gt;
        Header
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/nav&gt;
    &lt;div id="middle" class="container-full"&gt;
      &lt;div class="row"&gt;
        &lt;div id="navigation"
           class="col-xs-12 col-sm-12 col-md-2 col-lg-2"&gt;
          Navigation
        &lt;/div&gt;
        &lt;div id="main-container"
           class="col-xs-12 col-sm-8 col-md-7 col-lg-7"&gt;
          Main container
        &lt;/div&gt;
        &lt;div id="banner-panel"
           class="col-xs-12 col-sm-4 col-md-3 col-lg-3"&gt;
          Banner panel
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;div id="footer" class="container-fluid"&gt;
    &lt;p&gt;Footer&lt;/p&gt;
  &lt;/div&gt;
&lt;/body&gt;
</code></pre>

And now let’s update the <code>main.css</code> file:

<pre><code class="language-css">
#header {
  background: #2E849E;
  color: white;
  border-radius: 0;
}

.navbar {
  margin-bottom: 0;
}

#navigation {
  background: #faa;
}

#main-container {
  background: #afa;
}

#banner-panel {
  background: #aaf;
}

.container-full {
  margin 0 auto;
  width: 100%;
}

.row {
  margin: 0;
}

#footer {
  color: white;
  background: #222;
  height: 100px
}
</code></pre>

And below is the change to the <code>homepage.spec</code> file. Here I’ve defined proper names for the sections. Now reading the test will be easier. Also, once we get a test report, it will be properly structured, which will make it easier to understand the feedback.</p>

<pre><code class="language-css">
=====================================
header          css #header
navigation      css #navigation
main            css #main-container
banner-panel    css #banner-panel
footer          css #footer
=====================================

@ Header | *
--------------------
header
  inside: screen 0px top left right
  height: 50px

@ Navigation | *
-------------------
navigation
  inside: screen 0px left
   below: header 0px

@^| desktop
-----------------------
navigation
  width: 200 to 350px
  aligned horizontally all: main
  near: main 0px left

@^| tablet
-----------------
navigation
  inside: screen 0px left right
  above: main 0px
  % height: 50 to 100px

@^| mobile
----------------------
navigation
  inside: screen 0px left right
  above: main 0px
  % height: &gt; 60px

@ Footer | *
-------------------
footer
  % inside: screen 0px bottom left right
  below: banner-panel 0px
  height: 100px

@ Main | desktop
-----------------------
main, banner-panel
  below: header 0px

@^| tablet
----------
main
  inside: screen 0px left
  below: navigation 0px

@^| mobile
------------------
main
  inside: screen 0px left right
  above: banner-panel 0px

@ Banner panel | desktop, tablet
-------------------
banner-panel
  inside: screen 0px right
  width: 220 to 400px
  near: main 0px right
  aligned horizontally all: main

@^| tablet
--------------------
banner-panel
  below: navigation 0px

@^| mobile
------------------
banner-panel
  inside: screen 0px left right
  % height: &gt; 50px
</code></pre>

Notice the way we are defining our sections and tags now? The pipe symbol tells Galen to use the first part as a name of a section, while the second part (after the pipe) will be used for tag notation. Also, that weird syntax <code>@^| tablet</code> means that Galen should reuse the name from the previous section. We need this to be able to use a different tag for some objects in the same section. And because we don’t want to type the same section’s name multiple times, we can just use the <code>^</code> symbol.

Another interesting feature is in this specification file. You may have noticed the <code>%</code> symbol in front of some checks. This tells Galen to ignore the failure and report it as a warning. I’ve declared this symbol for some checks because at the moment there is no content in the navigation, main or banner-panel sections. Once we add some content there, these warnings will go away and we can remove the symbol later.

Now that we have the fix, let’s run our tests again. Remember the command we used the first time? Don’t forget to use your own path on your local machine.</p>

<pre><code>galen test shoppingcart.test \
-DwebsiteUrl="file:///home/ishubin/workspace/workshop-shopping-cart/website/shopping-cart.html" \
--htmlreport reports</code></pre>

On my machine, all of the tests passed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a3cf40-137e-4306-9a95-35f7a0558936/10-passed-report-overview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d18bd5c2-55e0-4870-af1d-b5c675047557/10-passed-report-overview-opt-small.png" alt="Passed report overview" /></a><figcaption>Passed report overview (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a3cf40-137e-4306-9a95-35f7a0558936/10-passed-report-overview-opt.png">View large version</a>)</figcaption></figure>

And here is the detailed report now that we have improved the naming of sections.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff282c66-5a38-4152-9be7-2d34052fc50f/11-passed-report-detailed-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e83baf-7a76-41d1-aac3-4e78300869e3/11-passed-report-detailed-opt-small.png" alt="Detailed test report" /></a><figcaption>Detailed test report (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff282c66-5a38-4152-9be7-2d34052fc50f/11-passed-report-detailed-opt.png">View large version</a>)</figcaption></figure>

Now we can move on to the next iteration.</p>

### Phase 5.10: Finish the Project

Delivering a responsive page from my original sketch took me around 10 iterations. I won’t go over all of these iterations here because the process was the same: test, code, refactor. But you can track all of the progress on the <a href="https://galenframework.github.io/workshop-shopping-cart/">workshop overview page</a>. You can also view the <a href="https://galenframework.github.io/workshop-shopping-cart/v0.6.1/website/shopping-cart.html">shopping-cart page</a> that I came up with in the end.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a55aa561-c901-45f3-b4ba-f1d4cbd1dfae/12-finished-page-overview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bbe096c-2b06-48d7-8cda-933b47f79ab7/12-finished-page-overview-opt-small.png" alt="Finished shopping-cart page" /></a><figcaption>Finished shopping-cart page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a55aa561-c901-45f3-b4ba-f1d4cbd1dfae/12-finished-page-overview-opt.png">View large version</a>)</figcaption></figure>

Of course, it still has some minor bugs in other browsers; I ran Galen tests only in Firefox. So, configuring the tests initially for real mobile devices along with all major desktop browsers might be a good idea. But the purpose of the experiment was just to try TDD for front-end development. That is why I didn’t focus on extensive cross-browser testing — although, to be honest, I think I should have. And if I had configured the website to be accessible from my Android phone and tablet, I could have used <a href="https://www.youtube.com/watch?v=zmbqTe0aUtc">Appium with Galen Framework</a> to test the layout.</p>

## Summary

It was an interesting experience. The way I worked in the past was to develop a website in one browser and then later hack it to work the same in other browsers. Fixing all of those nasty layout issues is really hard when you have a large HTML and CSS code base and a lot of third-party libraries — and especially if the website is supposed to be responsive. But applying TDD to front-end development helps a lot. It forces me to structure my code and my work process, and to focus on small things and deliver them at high quality.

In the end, I get complete test coverage, which I can use for all regression testing. At some point, I might change some fonts, modify the layout of certain components or add some elements to the page. If something goes wrong, Galen will alert me right away. I encourage you to try this approach, too. It might help you in your website development.</p>

## Resources

*   [Galen Framework](https://galenframework.com)
*   "[Shopping Cart: Visual Test-Driven Development](https://github.com/galenframework/workshop-shopping-cart)" (workshop project), GitHub
*   "[Galen Sample Test](https://github.com/galenframework/galen-sample-tests)," GitHub A real JavaScript-based test project implementing Galen tests
*   "[Cross-Browser Layout Testing With Galen Framework and Sauce Labs](https://sauceio.com/index.php/2015/01/cross-browser-layout-testing-with-galen-framework-and-sauce-labs/)," Amber Kaplan, Sauce Labs
*   [Image Comparison for Layout Tests With Galen Framework](https://www.youtube.com/watch?v=bheFQfEGR6U) (video tutorial), Ivan Shubin, YouTube
*   "[Galen](https://mindengine.net/category/galen/)," Mind Engine Articles about Galen Framework

{{< signature "da, ml, al, il" >}}

