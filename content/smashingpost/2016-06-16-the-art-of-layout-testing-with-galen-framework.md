---
title: The Art Of Layout Testing With Galen Framework
slug: the-art-of-layout-testing-with-galen-framework
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d417faf8-a698-4c70-9ee6-27582d48b40c/03-simple-example-preview-opt.png
date: 2016-06-16T18:02:45.000Z
author: ivanishubin
description: >-
  When designing a graphical user interface, there is always an open question:
  How do we automate testing for it? And **how do we make sure the website
  layout stays responsive** and displays correctly on all kinds of devices with
  various resolutions? Add to this the complications arising from dynamic
  content, requirements for internationalization and localization, and it
  becomes a real challenge.

  In this article, I will guide you through an interesting new layout testing
  technique. Using _Galen Framework_, I will provide a detailed tutorial for
  writing meaningful generalized layout tests, which can be executed in any
  browser and on any device and at the same time used as a single source of
  truth in your design documentation.
categories:
  - Mobile
  - Frameworks
  - Testing
---
When designing a graphical user interface, there is always an open question: How do we automate testing for it? And <strong>how do we make sure the website layout stays responsive</strong> and displays correctly on all kinds of devices with various resolutions? Add to this the complications arising from dynamic content, requirements for internationalization and localization, and it becomes a real challenge.

In this article, I will guide you through an interesting new layout testing technique. Using <a href="https://galenframework.com/">Galen Framework</a>, I will provide a detailed tutorial for writing meaningful generalized layout tests, which can be executed in any browser and on any device and at the same time used as a single source of truth in your design documentation.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Visual Test-Driven Development For Responsive Interface Design](https://www.smashingmagazine.com/2015/04/visual-test-driven-development-responsive-interface-design/)
*   [The Basics Of Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [Diverse Test-Automation Frameworks For React Native Apps](https://www.smashingmagazine.com/2016/08/test-automation-frameworks-for-react-native-apps/)

I will also demonstrate how I came up with an optimized test for a messaging page on our classifieds website, <a href="https://www.marktplaats.nl">Marktplaats</a>. We will learn how to extend Galen’s syntax with our own language, how to improve the test code and how to turn a layout testing routine into art.

{{% feature-panel %}}

## Introduction To Galen Framework

Galen Framework was covered a year ago in “<a href="https://www.smashingmagazine.com/2015/04/visual-test-driven-development-responsive-interface-design/">Visual Test-Driven Development for Responsive Interface Design</a>.” At the time, its syntax was limited. It has improved a lot since and gotten many new features, which we will look at here.

In case you are unfamiliar with Galen Framework, it is a tool for responsive and cross-browser layout testing and functional testing, with its own testing language, named <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/">Galen Specs</a>. It is based on <a href="https://www.seleniumhq.org/projects/webdriver/">Selenium WebDriver</a> and also has a <a href="https://galenframework.com/docs/reference-javascript-tests-guide/">rich JavaScript API</a> that lets you work with WebDriver directly. Because you have control over WebDriver, you can run tests in any browser, in the cloud (SauceLabs, BrowserStack, PerfectoMobile, etc.) or on real mobile devices using <a href="https://appium.io/">Appium</a>.</p>

### Installing and Executing

Setting up Galen Framework is easy. Simply execute the following command to get it installed via <a href="https://www.npmjs.com/">npm</a>:

<pre><code class="language-bash">npm install -g galenframework-cli</code></pre>

If you don’t use npm, just download the <a href="https://galenframework.com/download/">latest Galen Framework archive</a>, extract the package and follow the <a href="https://galenframework.com/docs/getting-started-install-galen/#ManualInstallation">installation instructions</a>.

Once installed, Galen Framework can be launched in various ways. For instance, you can use the <code><a href="https://galenframework.com/docs/reference-working-in-command-line/#Singlepagetest">check</a></code> command to launch a quick test of a single page. For this command, you need to provide a <code>.gspec</code> file with your layout validations, and then you can invoke it like this:

<pre><code class="language-bash">galen check loginPage.gspec --url https://example.com --size 1024x768 --include desktop --htmlreport reports
</code></pre>

This command will launch a browser, open the specified URL, resize the browser window to 1024 × 768 pixels and execute all validations declared in the <code>loginPage.gspec</code> file. As a result, you will get a <a href="https://galenframework.com/public/samples/reports/report.html">detailed HTML report</a>.</p>

### Managing Test Suites

In the real world, an actual web application does not consist purely of static pages. Quite often you will have to perform some actions to get to the place you want to check. In this case, Galen offers <a href="https://galenframework.com/docs/reference-javascript-tests-guide/">JavaScript test suites</a> and the <a href="https://galenframework.com/docs/reference-galenpages-javascript-api/">GalenPages JavaScript API</a> for implementing the <a href="https://martinfowler.com/bliki/PageObject.html">page object model</a>. Here is a simple example of a JavaScript Galen test:

<pre><code class="language-javascript">test("Home page", function() {
    var driver = createDriver("https://galenframework.com",
    "1024x768");
    checkLayout(driver, "homePage.gspec", ["desktop"]);
});
</code></pre>

And here is an implementation of the page object model for a log-in page, taken from a <a href="https://github.com/galenframework/galen-sample-tests">real project</a>.

<pre><code class="language-javascript">WelcomePage = $page("Welcome page", {
    loginButton: "#welcome-page .button-login"
});

LoginPage = $page("Login page", {
    username: "input[name='login.username']",
    password: "input[name='login.password']",
    loginButton: "button.button-login"

    loginAs: loggedFunction ("Log in as ${_1.username} with password ${_1.password}", function(user) {
        this.username.typeText(user.username);
        this.password.typeText(user.password);
        this.loginButton.click();
    })
});

test("Login page", function() {
    var driver = createDriver("https://testapp.galenframework.com",
    "1024x768");

    var welcomePage = new WelcomePage(driver).waitForIt();
    welcomePage.loginButton.click();
    new LoginPage(driver).waitForIt();

    checkLayout(driver, "loginPage.gspec", ["desktop"]);
});
</code></pre>

For advanced usage, I advise you to look at the <a href="https://github.com/galenframework/galen-bootstrap">Galen Bootstrap</a> project. It is a JavaScript extension built specifically for Galen. It provides some extra functionality for UI testing and an easier way to configure browsers and execute complex test suites.</p>

## Simple Layout Test

Let me start by introducing a simple layout test in Galen Framework. Then, I will move on to advanced use cases and demonstrate how to extend the Galen Specs syntax. For this, we will look at a header with an icon and caption:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b64fc45-741f-4bc4-aa48-340fef11d069/01-icon-caption-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/809412c1-0053-496f-bbdf-8044af8ccd8f/01-icon-caption-example-preview-opt.png" alt="Icon and caption" width="500" height="205" /></a><figcaption>Icon and caption (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b64fc45-741f-4bc4-aa48-340fef11d069/01-icon-caption-example-opt.png">View large version</a>)</figcaption></figure>

In HTML code, it might look something like this:

<pre><code class="language-markup">&lt;body&gt;
    &lt;!-- … --&gt;
    &lt;div id="header"&gt;
        &lt;img class="header-logo" src="/imgs/header-logo.png"/&gt;
        &lt;h1&gt;My Blog&lt;/h1&gt;
    &lt;/div&gt;
    &lt;!-- … --&gt;
&lt;/body&gt;
</code></pre>

The simplest form of a Galen layout test would look something like the following. First, we have to declare <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#Objectdefinition">objects with CSS selectors</a>.</p>

<pre><code class="language-markup">@objects
    header          #header
    icon            #header img
    caption         #header h1

</code></pre>

Then, we declare a <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#TaggingandSections">test section</a> with a meaningful name and put all of our validations below it.</p>

<pre><code class="language-markup">= Icon and Caption =
    icon:
        left-of caption 10 to 15px
        width 32px
        height 32px
        inside header 10px top

    caption:
        aligned horizontally all header
        inside header
</code></pre>

Here we’ve tested two header elements: the icon and caption. All validations listed under the icon and caption elements are actually standard <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#SpecsReference">Galen Specs</a>. Those specs are the fundamental building blocks with which you can assemble your own layout testing solution. Each spec verifies a single property (such as width, height, text), relative positioning (such as inside, left of, above) or pixels in the screenshot (such as color scheme, image).

## Testing Multiple Elements Using forEach Loops

The previous example demonstrates a simple scenario. Let’s see how we can deal with a more complicated situation: a horizontal menu. First, let’s try a straightforward layout testing technique.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1da75fd-2674-4738-ad65-43ed3766d633/02-horizontal-menu-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e44360ac-84f8-405c-9c07-f924bfe021f1/02-horizontal-menu-preview-opt.png" alt="Horizontal menu" width="500" height="164" /></a><figcaption>Horizontal menu (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1da75fd-2674-4738-ad65-43ed3766d633/02-horizontal-menu-opt.png">View large version</a>)</figcaption></figure>

Begin by matching multiple elements on the page. With the following code, we’re telling Galen to search for elements that match the <code>#menu ul li</code> CSS selector.</p>

<pre><code class="language-markup">@objects
    menu            #menu
        item-*          ul li
</code></pre>

Later, we can refer to these items with names like <code>menu.item-1</code> and <code>menu.item-2</code> and iterate over all menu items using a <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#forEachLoop"><code>@forEach</code> loop</a>.</p>

<pre><code class="language-markup">= Menu =
    menu.item-1:
        inside menu 0px top left bottom

    @forEach [menu.item-*] as menuItem, next as nextItem
        ${menuItem}:
            left-of ${nextItem} 0px
            aligned horizontally all ${nextItem}
</code></pre>

As you can see, even though the actual check is not that complex, the code has already become less intuitive. Imagine if we had more similar code in our tests. At some point, it would become an unmaintainable mess. There should be a way to improve it.</p>

## Rethinking Layout Testing

If you think about the previous example, it seems we could express the layout in just one or two sentences. For instance, we could say something like, “All menu items should be aligned horizontally, with no margin in between. The first menu item should be located on the left side of the menu, with no margin.” Because we’ve formulated sentences to explain the layout we want, why can’t we just use them in our code? Imagine if we could write the code like this:

<pre><code class="language-markup">= Menu =
    |first menu.item-* is in top left corner of menu
    |menu.item-* are aligned horizontally next to each other
</code></pre>

In fact, that is real working code, copied from my project. In those last two lines (starting with the pipe, <code>|</code>), we’re invoking custom functions that collect their arguments by parsing those two statements. Of course, the example above will not work as is. In order for it to compile, we need to implement the handlers for those two statements. We will get back to this implementation later.

The key point with the example above is that layout testing has <strong>shifted from object-driven to expression-driven</strong> testing. It might not be obvious from such a minor example, but it is definitely noticeable at a larger scale. So, why is this significant? The short answer is that this changes our mindset and affects the way we design our software and write tests for it.

Using this technique, we don’t treat our page as a bunch of objects with specific relationships between them. We don’t test the CSS properties of individual elements. And we avoid writing complicated non-trivial code. Instead, we are trying to think of common layout patterns and meaningful statements. Rather than testing menu item 1, menu item 2 and so on separately, we apply generic statements that:

*   are reproducible on other elements;
*   don’t contain hardcoded pixel values;
*   are applied to abstractions and not to concrete objects;
*   and, last but not least, actually make sense when we read them.</p>

## How It Works

Let me explain the mechanism of custom layout expressions using this simple example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc04d158-8ba0-461e-83fd-d24c25c70b51/03-simple-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d417faf8-a698-4c70-9ee6-27582d48b40c/03-simple-example-preview-opt.png" alt="Simple sketch" width="500" height="300" /></a><figcaption>Simple sketch (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc04d158-8ba0-461e-83fd-d24c25c70b51/03-simple-example-opt.png">View large version</a>)</figcaption></figure>

In this example, we are supposed to check that the button stretches to the panel, with no margin on the left or right side. Without custom rules, we can approach it in different ways, but I prefer the following solution:

<pre><code class="language-markup">button:
    inside some_panel 0px left right
</code></pre>

The code above gives us the flexibility to declare custom margin on the sides, and it also implicitly tests that the button is contained completely within the panel. The downside is that it is not very readable, which is why I am going to put this validation behind the expression <code>button stretches to some_panel</code>. In order for that to work, we need to write a <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#CustomRules">custom rule</a> like this:

<pre><code class="language-markup">@rule %{elementName} stretches to %{parentName}
    ${elementName}:
        inside ${parentName} 0px left right
</code></pre>

That’s it. Now we can put it in our test in just one line:

<pre><code class="language-markup">| button stretches to some_panel</code></pre>

As you can see, this rule takes two arguments: <code>elementName</code> and <code>parentName</code>. This allows us to apply it to other elements as well. Just replace the names of those two objects.</p>

<pre><code class="language-markup">| login_panel stretches to main_container
| header stretches to screen
| footer stretches to screen
# etc.
</code></pre>

## Implementing Your Own Testing Language

Let’s get back to the initial examples of layout expressions for the horizontal menu.</p>

<pre><code class="language-markup">= Menu =
    | first menu.item-* is in top left corner of menu
    | menu.item-* are aligned horizontally next to each other
</code></pre>

We can implement the first rule in the following way:

<pre><code class="language-markup">@rule first %{itemPattern} is in %{cornerSides} corner of %{parentElement}
    @if ${count(itemPattern) &gt; 0}
        ${first(itemPattern).name}:
            inside ${parentElement} 0px ${cornerSides}
</code></pre>

When used in our example, it would parse the arguments as follows:

*   `itemPattern` = `menu.item-*`
*   `cornerSides` = `top left`
*   `parentElement` = `menu`

Because we are done with our first expression, we can move to the next one. In the second expression, we are supposed to test the horizontal alignment of all menu items. I propose three simple steps:

1.  Find all menu items.
2.  Iterate over all of them until the penultimate element.
3.  Check that the element `n` is located to the left of element `n+1` and that their top and bottom edges align.

To get it working, we need to take a <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#forEachLoop"><code>@forEach</code> loop</a> and specs <code><a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#LeftofandRightof">left-of</a></code> and <code><a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#Aligned">aligned</a></code>. Fortunately, in Galen you can refer to the previous or next item in a loop. In case you’ve declared a reference to the next element, it will iterate only until the penultimate element, which is exactly what we need.</p>

<pre><code class="language-markup">@rule %{itemPattern} are aligned horizontally next to each other
    @forEach [${itemPattern}] as item, next as nextItem
        ${item}:
            left-of ${nextItem} 0px
            aligned horizontally all ${nextItem}
</code></pre>

You might ask, What if we have to specify a margin in our test (such as <code>~ 20px</code> or <code>10 to 20px</code>)? Then, I suggest either implementing a separate rule or extending the existing one to support an <code>%{margin}</code> argument.</p>

<pre><code class="language-markup">@rule %{itemPattern} are aligned horizontally next to each other with %{margin} margin
    @forEach [${itemPattern}] as item, next as nextItem
        ${item}:
            left-of ${nextItem} ${margin}
            aligned horizontally all ${nextItem}
</code></pre>

That’s it! We have created a generic expression that helps us validate the horizontal menu. However, because of its flexibility, we can do much more than that. We can use it to test any other elements on the page. We can even use it to test the alignment of two buttons:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b1e4f24-6ecd-49a3-aa7c-134d879cedd6/04-form-buttons-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e804b601-553b-43dc-8272-2f8b9cf456a6/04-form-buttons-preview-opt.png" alt="Form buttons" width="500" height="170" /></a><figcaption>Form buttons (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b1e4f24-6ecd-49a3-aa7c-134d879cedd6/04-form-buttons-opt.png">View large version</a>)</figcaption></figure>

<pre><code class="language-markup">| menu.item-* are aligned horizontally next to each other with 0px margin
| submit_button, cancel_button are aligned horizontally next to each other with 20px margin
</code></pre>

You might notice in these two examples that we’ve declared the first argument in two different ways. In the first expression, the first argument is <code>"menu.item-*"</code>, and in the second expression it is declared as <code>"submit_button, cancel_button"</code>. That is possible because the <code>@forEach</code> loop allows us to use a comma-separated list of objects together with the star operator. But we are still not done with refactoring. We could improve the code further and make it more readable. If we create groups for the menu items and the log-in form buttons, we could accomplish something like this:

<pre><code class="language-markup">@groups
    menu_items              menu_item-*
    login_form_buttons      submit_button, cancel_button

= Testing login page =
    | &amp;menu_items are aligned horizontally next to each other with 0px margin
    | &amp;login_form_buttons are aligned horizontally next to each other with 20px margin
</code></pre>

In this case, we have to use the <code>&amp;</code> symbol, which stands for a <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#ObjectGroups">group declaration</a>. That is already a good test. First, it just works, and we are able to test what we need. Also, the code is clear and readable. If another person were to ask you what the log-in page should look like and what the design requirements are, you could tell them to look at the test.

As you can see, implementing custom expressions for complex layout patterns is not really a big deal. It might be challenging in the beginning, but it still resembles something of a creative activity.</p>

## Dynamic Margins

Let’s look at another rare layout pattern that you might find sometimes on various websites. What if we wanted to test that elements have an equal distance between each other? Let’s try to implement another rule for that, but this time using a JavaScript implementation. I propose such a statement: <code>"box_item-* are aligned horizontally next to each other with equal distance"</code>. This is going to be a little tricky because we don’t know the margin between elements and we can’t just hardcode pixel values. Therefore, the first thing we have to do is to retrieve the actual margin between the first and last elements.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40a1a13c-ccf7-4b37-b35f-dd5360e91f55/05-equally-distant-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b56f3df-1594-429a-b7ac-dc65daeb645a/05-equally-distant-preview-opt.png" alt="Equally distant" width="500" height="173" /></a><figcaption>Equally distant (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40a1a13c-ccf7-4b37-b35f-dd5360e91f55/05-equally-distant-opt.png">View large version</a>)</figcaption></figure>

Once we obtain that margin, we can declare it in a <code>@forEach</code> loop similar to how we did before. I propose implementing this rule using the <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#CustomRulesJavaScriptbasedrules">JavaScript API</a> because the logic required is a bit more complex than in all of our previous examples. Let’s create a file named <code>my-rules.js</code> and type in this code:

<pre><code class="language-javascript">rule("%{objectPattern} are aligned horizontally next to each other with equal margin", function (objectName, parameters) {
  var allItems = findAll(parameters.objectPattern),
    distance = Math.round(Math.abs(allItems[1].left() - allItems[0].right())),
    expectedMargin = (distance - 1) + " to " + (distance + 1) + "px";

  if (allItems.length &gt; 0) {
    for (var i = 0; i &lt; allItems.length - 1; i += 1) {
      var nextElementName = allItems[i + 1].name;
      this.addObjectSpecs(allItems[i].name, [
        "aligned horizontally all " + nextElementName,
        "left-of " + nextElementName + " " + expectedMargin
      ]);
    }
  }
});
</code></pre>

In our test code, we will use it like this:

<pre><code class="language-markup">@script my-rules.js

# …

= Boxes =
    | box_item-* are aligned horizontally next to each other with equal distance
</code></pre>

As you can see, in Galen Framework we can choose between two languages when implementing rules: Galen Specs and JavaScript. For simple expressions, Galen Specs is easier to use, but for complex ones I always choose JavaScript. If you want to learn more about JavaScript rules, <a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#CustomRulesJavaScriptbasedrules">refer to the documentation</a>.</p>

## Galen Extras

Having played enough with various layout patterns, I realized that all of these Galen rules could be easily applied in any other test project. That gave me an idea to compile the most common layout expressions into their own library. That’s how I came to create the <a href="https://github.com/galenframework/galen-extras">Galen Extras</a> project. Below are some examples of what this library is capable of:

<pre><code class="language-markup">| header.icon should be squared

| amount of &amp;menu_items should be &gt; 3

| &amp;menu_items are aligned horizontally next to each other

| &amp;list_items are aligned vertically above each other with equal distance

| every &amp;menu_item is inside menu 0px top and has width &gt; 50px

| first &amp;menu_item is inside menu 0px top left

| &amp;menu_items are rendered in 2 column table

| &amp;menu_items are rendered in 2 column table, with 0 to 1px vertical and 10px horizontal margin

| &amp;login_form_elements sides are vertically inside content_container with 20px margin

login_panel:
    | located on the left side of panel and takes 70 % of its width

# etc …
</code></pre>

The Galen Extras library contains many of the layout patterns you would commonly find on websites, and I keep updating it as soon as I discover a useful pattern. Once this library was set up, I decided to try it on a real test project.</p>

## Testing The Messaging App

Currently, I work as a software engineer at Marktplaats. At some point, I decided to apply all of the experience I had gained to a real project. I needed to test the <a href="https://www.marktplaats.nl/mijnberichten/">messaging page</a> on our website. Here is what it looks like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc079775-e7ff-4282-b356-7adfa0624df6/06-messenger-page-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3818f9b-bcc8-4372-a52e-8dc3e08f39cb/06-messenger-page-preview-opt.png" alt="Messaging page" width="500" height="601" /></a><figcaption>Messaging page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc079775-e7ff-4282-b356-7adfa0624df6/06-messenger-page-opt.png">View large version</a>)</figcaption></figure>

To be honest, implementing tests for such pages has always seemed a bit scary to me, especially layout tests. But with the Galen Extras library in place, it actually went pretty smoothly, and soon I was able to come up with this code:

<pre><code class="language-markup">@import ../selected-conversation.gspec
@groups
  (message, messages)                           messenger.message-*
  first_two_messages                            messenger.message-1,messenger.message-2
  first_message                                 messenger.message-1
  second_message                                messenger.message-2
  third_message                                 messenger.message-3
  (message_date_label, message_date_labels)     messenger.date_label-*
  first_date_label                              messenger.date_label-1
  second_date_label                             messenger.date_label-2

= Messages panel =
  = Messages and Date labels =
    |amount of visible &amp;message_date_labels should be 1
    |first &amp;message_date_label has text is "17 november 2015"

    |amount of visible &amp;messages should be 3
    |&amp;first_two_messages should be located at the left inside messenger with ~ 20px margin
    |&amp;third_message should be located at the right inside messenger with ~ 20px margin
    |&amp;messages are placed above each other with 10 to 15px margin

    |text of all &amp;messages should be ["Hi there!", "I want to buy something", "Hello! Sure, it's gonna be 100 euros"]

  = Styling =
    |&amp;first_two_messages should be styled as others message
    |&amp;third_message should be styled as own message
</code></pre>

### Extracting Pixel Ranges

The test looked OK: It was compact and readable but still far from perfect. I didn’t really like all of those margin definitions (<code>~ 20px</code>, <code>10 to 15px</code>). Some of them were repeated, and it was hard to understand what each of them stood for. That is why I decided to hide every margin behind a meaningful variable.</p>

<pre><code class="language-markup"># ...
@set
    messages_side_margin        ~ 20px
    messages_vertical_margin    10 to 15px

= Messages panel =
  = Messages and Date labels =
    |amount of visible &amp;message_date_labels should be 1
    |first &amp;message_date_label has text is "17 november 2015"

    |amount of visible &amp;messages should be 3
    |&amp;first_two_messages should be located at the left inside messenger with ${messages_side_margin} margin
    |&amp;third_message should be located at the right inside messenger with ${messages_side_margin} margin
    |&amp;messages are placed above each other with ${messages_vertical_margin} margin

# ...
</code></pre>

As you can see, I’ve moved the margins to <code>messages_vertical_margin</code> and <code>messages_side_margin</code>. I’ve also declared a <code>minimal</code> margin, which is a range between 0 and 1 pixel.</p>

<pre><code class="language-markup"># ...
@set
    minimal     0 to 1px

= Conversations Panel =
    | &amp;conversations are aligned above each other with ${minimal} margin

# ...
</code></pre>

### Image-Based Validation and Custom Expressions

Having covered the positioning of all main elements on the page, I decided also to test styling. I wanted to validate that each message has a background colour specific to the user’s role. When users are logged in, messages would have a light-blue background. Messages for other users would have a white background. In case a message has not been sent, the error alert would have a pink background. Here is the rule that helped me validate these styles:

<pre><code class="language-markup">@set
    OWN_MESSAGE_COLOR             #E1E8F5
    OTHERS_MESSAGE_COLOR          white
    ERROR_MESSAGE_COLOR           #FFE6E6
@rule %{item} should be styled as %{style} message
    ${item}:
        @if ${style === "own"}
            color-scheme &gt; 60% ${OWN_MESSAGE_COLOR}, 0.2 to 20 % ${MAJOR_TEXT_MESSAGE_COLOR}
        @elseif ${style === "error"}
            color-scheme &gt; 60% ${ERROR_MESSAGE_COLOR}, 0.2 to 20 % ${MAJOR_TEXT_MESSAGE_COLOR}
        @else
            color-scheme &gt; 60% ${OTHERS_MESSAGE_COLOR}, 0.2 to 20 % ${MAJOR_TEXT_MESSAGE_COLOR}
</code></pre>

The <code><a href="https://galenframework.com/docs/reference-galen-spec-language-guide/#Colorscheme">color-scheme</a></code> spec verifies the proportional distribution of colors within an element. It crops a screenshot of the page and analyzes the color distribution. So, to check the background color of an element, we just check that its distribution is greater than 60% of the total color range. In the test, this rule is invoked like so:

<pre><code class="language-markup">  = Styling =
    |&amp;first_two_messages should be styled as others message
    |&amp;third_message should be styled as own message
</code></pre>

## Configuring Test Suites

The messaging app is a dynamic application that works together with the RESTful Messaging API. Therefore, to test its layouts in all different states, we have to prepare test data. I decided to mock up the Messaging API so that I would be able to configure all of my test messages in the test suite. Here is a fragment of my test suite that shows how our tests are structured.</p>

<pre><code class="language-javascript">// ...
testOnAllDevices("Unselected 2 conversations", "/", function (driver, device) {
  mock.onGetMyConversationsReturn(sampleConversations);
  refresh(driver);

  new MessageAppPage(driver).waitForIt();
  checkLayout(driver, "specs/tests/unselected-conversations.gspec", device.tags);
});

testOnAllDevices("When clicking a conversation it should reveal messages", "/", function (driver, device) {
  mock.onGetMyConversationsReturn(sampleConversations);
  mock.onGetSingleConversationReturn(sampleMessages);
  refresh(driver);

  var page = new MessageAppPage(driver).waitForIt();
  page.clickFirstConversation();

  checkLayout({
    driver: driver,
    spec: "specs/tests/three-simple-messages-test.gspec",
    tags: device.tags,
    vars: {
      expectedTextProvider: textProvider({
        "messenger.message-1": "Hi there!\n11:02",
        "messenger.message-2": "I want to buy something\n12:02",
        "messenger.message-3": "Hello! Sure, it's gonna be 100 euros\n13:02"
      })
    }
  });
});
// ...
</code></pre>

## Catching Bugs

Implementing those simple expressions pays off quite quickly. Let’s go over what kind of bugs we can catch with our test suite.</p>

### Styling Issue

Here is an example of when something goes wrong in our CSS code base and, as a result, all messages are rendered with the same background.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb35534e-cd62-407b-b461-0623ca6ddec4/06b-messenger-wrong-background-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb07046b-3222-46cf-a60d-4f1928f3b191/06b-messenger-wrong-background-preview-opt.png" alt="Wrong message background color" width="500" height="243" /></a><figcaption>Wrong message background color (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb35534e-cd62-407b-b461-0623ca6ddec4/06b-messenger-wrong-background-opt.png">View large version</a>)</figcaption></figure>

If you compare this screenshot with the original, you will notice that the last message has a white background, whereas it is supposed to be light blue. Let’s see how Galen reports this issue:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c19fec7-26be-4211-aa2d-17670783015d/07-messenger-wrong-background-report-screenshot-preview-opt-178x118.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/756944a8-1c38-418f-8376-465c679f67b0/07-messenger-wrong-background-report-screenshot-preview-opt.png" alt="Screenshot with error message" width="500" height="431" /></a><figcaption>Screenshot with error message (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c19fec7-26be-4211-aa2d-17670783015d/07-messenger-wrong-background-report-screenshot-preview-opt-178x118.png">View large version</a>)</figcaption></figure>

For the highlighted object, it displays the error <code>color #e1e8f5 on "messenger.message-3" is 0% but it should be greater than 60%</code>. To be honest, this error message doesn’t look all that clear, but because this check was generated from a custom rule, we can always look up its original name in a report branch:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/990baa42-7f27-419a-9830-e9dfc576763a/08-messenger-wrong-background-report-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef56fdbf-0789-4f20-b4c1-ed1116c9736d/08-messenger-wrong-background-report-preview-opt.png" alt="Reporting test failure" width="500" height="265" /></a><figcaption>Reporting test failure (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/990baa42-7f27-419a-9830-e9dfc576763a/08-messenger-wrong-background-report-opt.png">View large version</a>)</figcaption></figure>

If you scroll up, you’ll see that the original statement is <code>&amp;third_message should be styled as own message</code>. That is another benefit of using custom expressions: They help you understand the failure and nicely describe all of those generated validations.</p>

### Positioning Issue

Here is another example of when the layout goes wrong due to incorrect alignment of an element. In the following screenshot, you can see that the last message is positioned to the left side of the messaging viewport, instead of the right.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc318ea3-350c-4b9a-a532-59420ad6fdb6/09-messenger-wrong-position-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6fc7e20-1a8d-49c8-abf7-28417bbdc1f1/09-messenger-wrong-position-preview-opt.png" alt="Wrong position of message" width="500" height="249" /></a><figcaption>Wrong position of message (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc318ea3-350c-4b9a-a532-59420ad6fdb6/09-messenger-wrong-position-opt.png">View large version</a>)</figcaption></figure>

Let’s look again at the screenshot with the error message:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d4b4ad5-cdcb-4185-830f-9009e9ff2719/10-messenger-wrong-position-report-screenshot-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b56ef41-4c44-4068-9d5d-dbf476e46067/10-messenger-wrong-position-report-screenshot-preview-opt.png" alt="Wrong position of message" width="500" height="475" /></a><figcaption>Wrong position of message (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d4b4ad5-cdcb-4185-830f-9009e9ff2719/10-messenger-wrong-position-report-screenshot-opt.png">View large version</a>)</figcaption></figure>

The screenshot highlights the messaging container and the last message element. Together with that, it shows the following error message: <code>"messenger.message-3" is 285px right which is not in range of 22 to 28px</code>. It might not be clear to a web developer why a margin of 22 to 28 pixels is expected on the right side. Again, you’d have to look for a validation statement in the report branch:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d5b2138-4b02-46b4-8f4e-23e1c85380bf/11-messenger-wrong-position-report-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32b14443-b8af-46c7-9094-41fd5043545a/11-messenger-wrong-position-report-preview-opt.png" alt="Wrong position of message" width="500" height="298" /></a><figcaption>Wrong position of message (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d5b2138-4b02-46b4-8f4e-23e1c85380bf/11-messenger-wrong-position-report-opt.png">View large version</a>)</figcaption></figure>

The original statement for that check is <code>&amp;third_message should be located at the right inside messenger with ~ 25px margin</code>. That makes much more sense. Moreover, other front-end engineers will understand this test report, even if they haven’t written the tests.</p>

## Layout Testing Guidelines

With all of these different experiments in mind, I decided to formalize all of the learning into general layout testing guidelines. Here is a quick checklist of steps to follow to ease your testing routine.

*   Identify layout patterns in the design.
*   Generalize validation statements. Try to condense most validations into single sentences.
*   Componentize! It’s always better to move tests of repeated elements into [dedicated components](https://galenframework.com/docs/reference-galen-spec-language-guide/#Component).
*   Use meaningful names for sections, rules and objects.
*   Avoid pixels. Try to replace pixel values (whether exact values or ranges) with meaningful variables.
*   Adjust your website’s code to make it easier to test. This will help you structure and maintain both your production and test code.</p>

## Acceptance Criteria To The Rescue

Often I get questions like, “So how detailed should a layout test be? And what should we be testing specifically?” A general answer is hard to give. The problem is that when the test’s coverage is small, you miss bugs. On the other hand, if you have too detailed tests, you might get a lot of false positives, and in future you might get lost in test maintenance. So, there is a trade-off. But I did figure out a general guideline for myself. If you split the work into smaller <a href="https://en.wikipedia.org/wiki/User_story">user stories</a>, then it becomes easier to structure a page’s design in the form of acceptance criteria. In the end, you might put this very acceptance criteria right in your test code. For instance, some of these statements could be defined in the form of custom rules, as shown in all of the previous code examples. A good example of acceptance criteria would be something like this:

*   Popups should be centered vertically and horizontally on the screen.
*   They should be 400 pixels wide.
*   Buttons should be aligned horizontally.
*   And so on

Once you describe the design in simple sentences, it becomes easier to convert them into reusable statements and to organize your test code.</p>

## Conclusion

As you can see, such an exercise helps you to structure a design and discover general layout patterns that can be shared across multiple page components. Even if the page is complex and consists of a lot of elements, you can always find a way to group them in your layout expressions. With this approach, layout testing becomes more of a tool for <a href="https://en.wikipedia.org/wiki/Test-driven_development">test-driven development</a>, helping you to design, implement and deliver software incrementally, which is especially useful in an agile environment.</p>

### Resources

*   [Galen Framework](https://galenframework.com) (official website)
*   [Galen Framework](https://github.com/galenframework/galen), GitHub
*   [Galen Extras](https://github.com/galenframework/galen-extras) (library), GitHub
*   [Galen Bootstrap](https://github.com/galenframework/galen-bootstrap), GitHub
*   “[Galen Framework Tutorials](https://www.youtube.com/playlist?list=PLyhyM1XhqdgWQ1DevSn-Zhxbvee3AQs_j),” YouTube

{{< signature "da, ml, al, il" >}}

