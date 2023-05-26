---
title: Writing Unit Tests For WordPress Plugins
slug: writing-unit-tests-for-wordpress-plugins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1831c77-31cd-41ee-9de0-2a3867a7940c/wordpress-11.png
date: 2012-03-07T12:24:41.000Z
author: zack-grossbart
description: >-
  When my WordPress plugin had only three users, it didn’t matter much if I broke it. By the time I reached 100,000 downloads, every new update made my palms sweat.
categories:
  - WordPress
  - Coding
  - JavaScript
  - Plugins
  - Techniques (WP)
---
My first goal for the <a href="https://wordpress.org/extend/plugins/editorial-calendar/">WordPress Editorial Calendar</a> was to make it do anything useful. I was new to JavaScript and PHP and didn’t really know what I could pull off. In a few days I had a proof of concept. In a few more I had a working version and was asking friends to install it. The calendar worked… sort of.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How Commercial Plugin Developers Are Using The WordPress Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)
*   [Common WordPress Malware Infections](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)
*   [Manage Events Like A Pro With WordPress](https://www.smashingmagazine.com/2012/04/manage-events-like-pro-with-wordpress/)
*   [Useful Free Admin Plugins For WordPress](https://www.smashingmagazine.com/2012/03/useful-free-admin-plugins-wordpress/)

I spent three times as much time fixing bugs as I did coding. Once the plugin worked, I wrote unit tests to make sure it kept working.

{{% feature-panel %}}

The unit tests for my calendar use <a href="https://docs.jquery.com/QUnit">QUnit</a>, but they really use just three functions: <code>test</code>, <code>expect</code> and <code>ok</code>. This article shows you how to integrate unit tests into your WordPress plugin, where to write unit tests and how they can help you.</p>

## QUnit Basics

Unit tests follow a basic pattern: do something, then check the results. (“Is this variable <code>4</code> when it should be <code>5</code>?” “Does this line of my table show up where it’s supposed to?”)

<pre><code class="language-javascript">function myTest() {
    test('My test run', function() {
        expect(2);
        ok(5 === 5, 'This test will always pass');
        ok(5 === 6, 'This test will always fail');
    });
}</code></pre>

This structure forces you to think of your code in simple units that return <code>true</code> or <code>false</code>. The <code>test</code> function starts a test run with two arguments: the title for this test run, and the function containing the tests. The <code>expect</code> function tells QUnit how many tests are in the run. If we call too few or too many, it causes an error.

The <code>ok</code> function performs the test of the expression. It takes two arguments: a boolean indicating whether the test was successful, and a message.

Test runs are added to a special list section, which shows the total number of tests, whether each test passed or failed, and how long the tests took.

<img class="aligncenter size-full wp-image-118830" title="qunit_title" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3b2be87-34a4-4d80-8a77-d776eb6fb1eb/qunit-title.png" alt="" width="500" height="306" />

## A Real Unit Test

WordPress plugins complicate testing by using a combination of PHP and JavaScript. Even passing a simple value from PHP to JavaScript gets tricky.

The function below finds a WordPress preference with the <a href="https://codex.wordpress.org/Function_Reference/get_option"><code>get_option</code></a> function and creates a JavaScript variable with the resulting value.

<pre><code class="language-php">function getOption($myOption, $myVariable) {
    if (get_option($myOption) != "") {
        ?&gt;&lt;script type="text/javascript"&gt;
            &lt;?php echo($myVariable); ?&gt; = &lt;?php echo(get_option($myOption)); ?&gt;;
        &lt;php
    }
}</code></pre>

Now we’ll call it to get the name of the blog and set it to a variable named <code>myBlogName</code>.

<pre><code class="language-php">getOption("blogname", "myBlogName");</code></pre>

Little helper functions like these glue your plugin together, but they always worry me. Did I access the JavaScript variable with the right name or did I mistype it? Did I use the same name twice? A simple unit test makes all of these worries go away.

<pre><code class="language-javascript">function wpPrefTest() {
    test('Get access to WordPress preferences', function() {
        expect(1);
        ok(myBlogName, 'The variable (myBlogName) should be available.');
    });
}</code></pre>

This unit test checks whether the variable <code>myBlogName</code> exists. We could also look for a specific value or compare it to something else from the application.

Once you have this unit test, you’ll never need to worry about getting the blog’s name. It will always be there, and you’ll find out fast if you ever break it.</p>

## Integrating QUnit With WordPress

Testing in special development environments isn’t accurate. I wanted to add QUnit directly to my calendar, but I didn’t want to make the page’s size larger. The solution is a URL parameter and a little PHP to include QUnit only when I need it:

<pre><code class="language-php">wp_enqueue_script( "qunit", path_join(WP_PLUGIN_URL, basename( dirname( __FILE__ ) )."/lib/qunit.js"), array( 'jquery' ) );
wp_enqueue_script( "edcal-test", path_join(WP_PLUGIN_URL, basename( dirname( __FILE__ ) )."/edcal_test.js"), array( 'jquery' ) );</code></pre>

This tells WordPress to include the QUnit JavaScript and my unit tests from <a href="https://plugins.svn.wordpress.org/editorial-calendar/trunk/edcal_test.js"><code>edcal_test.js</code></a>. I could have just embedded the script’s reference directly on my page, but I might have run into trouble if other plugins on the same page use QUnit.

You can see the <a href="https://plugins.svn.wordpress.org/editorial-calendar/trunk/">full source code here</a>.

The next step was to make sure that these scripts load only when I need them. To do this, I wrapped the code in a check for a URL parameter:

<pre><code class="language-php">if ($_GET['qunit']) {
    wp_enqueue_script( "qunit", path_join(WP_PLUGIN_URL, basename( dirname( __FILE__ ) )."/lib/qunit.js"), array( 'jquery' ) );
    wp_enqueue_script( "edcal-test", path_join(WP_PLUGIN_URL, basename( dirname( __FILE__ ) )."/edcal_test.js"), array( 'jquery' ) );
}</code></pre>

This loads the scripts only if I’m running unit tests, and everything else in the plugin stays the same. You can run the unit tests at any time just by adding <code>&amp;qunit=true</code> to the end of the URL. That’s a good thing because my unit tests actually change what’s going on in the blog.

You can <a href="https://www.zackgrossbart.com/extras/sandbox/wp-admin/edit.php?page=cal&amp;qunit=true">run the Editorial Calendar’s unit tests in your browser right now</a>. Scroll down to see the unit test results at the bottom of the page.

The PHP makes sure that my scripts get to the browser. The last step is to call them from my JavaScript. Once again, I want to call them only if we’re in unit test mode. So, I add a small function to get the parameters from the URL:

<pre><code class="language-javascript">getUrlVars: function() {
    var vars = [], hash;
    var hashes = window.location.href.slice(window.location.href.indexOf('?') + 1).split('&amp;');
    for (var i = 0; i &lt; hashes.length; i++) {
        hash = hashes[i].split('=');
        vars.push(hash[0]);
        vars[hash[0]] = hash[1];
    }
    return vars;
}</code></pre>

And then I call my unit tests if the QUnit parameter is there:

<pre><code class="language-javascript">jQuery(document).ready(function() {
    if (edcal.getUrlVars().qunit) {
        edcal_test.runTests();
    }
});</code></pre>

This ensures that we call the unit tests only if they’re available.

The last step is to set up a space for the unit test’s output. QUnit writes its test results into specially designated tags on your HTML page. You could embed these tags directly in your HTML output, but because they need to be there only when QUnit is active, I create the HTML in JavaScript instead.

<pre><code class="language-javascript">jQuery('head').append('&lt;link&gt;');
css = jQuery('head').children(':last');
css.attr({
    rel: 'stylesheet',
    type: 'text/css',
    href: '../wp-content/plugins/edcal/lib/qunit.css'
});

jQuery('#wpbody-content .wrap').append('&lt;div id="edcal-qunit"&gt;&lt;/div&gt;');

jQuery('#edcal-qunit').append(
    '&lt;h1 id="qunit-header"&gt;WordPress Editorial Calendar Unit Tests&lt;/h1&gt;' +
    '&lt;h2 id="qunit-banner"&gt;&lt;/h2&gt;' +
    '&lt;div id="qunit-testrunner-toolbar"&gt;&lt;/div&gt;' +
    '&lt;h2 id="qunit-userAgent"&gt;&lt;/h2&gt;' +
    '&lt;ol id="qunit-tests"&gt;&lt;/ol&gt;' +
    '&lt;div id="qunit-fixture"&gt;test markup&lt;/div&gt;');</code></pre>

QUnit needs a list tag, a couple of divs and a style sheet.

<a href="https://www.zackgrossbart.com/extras/sandbox/wp-admin/edit.php?page=cal&amp;qunit=true"><img class="aligncenter size-full wp-image-118198" title="QUnit test output" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbdd6594-3dd3-41df-9c13-a81567bb8b49/qunit-panel.png" alt="" width="544" height="500" /></a>

Now we’re ready to write our first test.

## The First Unit Test

The first calendar unit tests scroll the calendar up and down and make sure we see the correct number of days.

<pre><code class="language-javascript">moveTests: function() {
    var curSunday = edcal.nextStartOfWeek(Date.today()).add(-1).weeks();
    edcal.moveTo(Date.today());

    test('Move to today and check visible dates', function() {
        expect(2);
        ok(edcal_test.getFirstDate().equals(curSunday.clone()),
           'firstDate should match ' + curSunday);
        ok(edcal_test.getLastDate().equals(
           curSunday.clone().add(edcal.weeksPref).weeks().add(-1).days()),
           'lastDate should match ' + curSunday);
    });
}</code></pre>

Our first test moves the calendar to today and checks to see if the first and last days are what we expect. We set up a variable, move the calendar and start the test by calling the <code>test</code> function.

<img class="aligncenter size-full wp-image-118199" title="QUnit test run expanded" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64732ac1-bb53-4e7f-b956-cc5042daf780/qunit-panel-expanded.png" alt="" width="540" height="614" />

In this case we want to make sure the dates are correct, so we compare the date from the calendar to the one we expect and then pass the result to the <code>ok</code> function. The test succeeds if they match and fails if they don’t.

This test may seem simple, but a lot is going on under the hood. We’re testing date handling, drawing and the fundamental arithmetic of the calendar.

Unit tests can do anything. The <a href="https://www.zackgrossbart.com/extras/sandbox/wp-admin/edit.php?page=cal&amp;qunit=true">WordPress Editorial Calendar unit tests</a> automate the plugin like a robot. They cover everything a user could do with the calendar.</p>

## What To Unit Test

I write a lot more unit tests for JavaScript than I do for compiled languages. In Java and C++, the compiler catches many of my mistakes, whereas JavaScript lets you pass a <code>string</code> when you meant to pass a <code>number</code> and lets you call a function with two arguments when it needs three.

Here’s the basic list of areas I test in JavaScript applications:

*   **Tests that make sure the program does what it is meant to do**.  These tests ensure the basic functionality keeps working; they do not test interactions. (The calendar lets you drag and drop posts, but writing unit tests for dragging and dropping wouldn’t make sense; instead, we would focus on what happens after the drop event.)
*   **Tests that make sure the program doesn’t do what it’s not meant to do** These tests ensure the program fails properly when it gets garbage.
*   **A unit test for every major bug I’ve found** These tests ensure that none of these bugs creep back in.

APIs and other clear boundaries in the code lend themselves well to unit tests, as do utility functions that you call from many places in the application. With the calendar, this means testing calendar movements and testing how we create and modify posts in WordPress, like this:

1.  Move the calendar and check the dates;
2.  Create a post and make sure it was created properly;
3.  Edit the post we just created and make sure it saves properly;
4.  Move the post and make sure it shows up at the correct date;
5.  Move the post from two places at the same time and make sure we get the proper warning message;
6.  Delete the post from the server and make sure it isn’t there anymore.

The penultimate test covers an error condition in which two people move the same post at the same time. Unit tests work well for this kind of error, because the error type is difficult to test and manual testing is less likely to uncover problems.

<img class="aligncenter size-full wp-image-118200" title="QUnit error test" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/958f265c-1262-4c02-b2ab-0f8267549401/calendar-err.png" alt="" width="549" height="423" />

For your own application, you should have at least one unit test for every data-changing operation that users can perform. I like to add them for all of the places where a user can get data, too. It might sound like a lot of work, but you can cut down on it by writing single tests that cover multiple areas.</p>

### Asynchronous Unit Tests

Many of these combination unit tests make AJAX calls. QUnit provides a special function for handling AJAX called <code>asyncTest</code>. This function works just like <code>test</code>, but it pauses the test run at the end of the function. The QUnit framework waits until your AJAX call completes and you call the <code>start</code> function before restarting the test run.

The <code>asyncTest</code> function handles all of the tests that edit posts from the calendar, including deleting the post at the end:

<pre><code class="language-javascript">asyncTest('Delete the post created for testing', function() {
    expect(1);

    edcal.deletePost(edcal_test.post.id, function(res)
    {
        equals(jQuery('#post-' + res.post.id).length, 0,
               'The post should now be deleted from the calendar.');
        start();
    });
});</code></pre>

When you restart the test framework you can call more tests. Calling the next test function at the end of the previous one chains them together, and it supports calling all of your tests with just a call to the first function.

These tests, which call AJAX, ensure that the integration between the JavaScript on the client side and the PHP on the back end works properly.</p>

### That’s Not a Unit Test

When I first learned to write unit tests in C++ the rule was this: a single test should only call code in a single module or CPP file. That is, a unit test should test one unit of code.

Changing posts from unit tests violates that rule. Instead of just testing JavaScript, I’m really testing JavaScript, PHP, WordPress itself and MySQL all at once. That makes it an automated integration test.

Integration tests aren’t traditional unit tests, but they work well for WordPress plugins. When I create a post, I’ll know that the AJAX code in my plugin works as well as the JavaScript code. Covering a larger portion of the application with fewer tests makes it easier to focus on what I should be testing.</p>

## What Not To Unit Test

You could write unit tests forever, but some are more useful than others. Here are some guidelines.

*   **Don’t unit test the UI.** The test has to run by itself. It can’t wait for you to click a button or look at something to make sure it appears correctly.
*   **Don’t unit test performance.** Tests take a variable amount of time on different machines and browsers. Don’t write unit tests that depend on a function being returned in a set amount of time.
*   **Don’t unit test code from other projects.** Adding unit tests for WordPress or a jQuery plugin you depend on might be tempting, but it rarely pays off. If you want to contribute unit tests to WordPress.org that’s great, but your unit tests should check that your plugin works.

The Editorial Calendar has 26 unit tests, at about 3,500 lines of code. That may not sound like much, but they’ve saved many of my releases.</p>

## Unit Tests Saved My Butt

I didn’t add unit tests until the thirteenth release of my plugin. By then, the calendar had a couple of hundred users and was growing fast. My plugin was working, and I was getting close to release 1.0.

Instead of adding new features, I took in a new framework, added special code to load it, wrote 381 lines of unit tests and integrated all of this into the plugin. It seems like a lot of work, but it saved my butt.

Right before a release, I wrote some harmless-looking PHP code like the following to get the JSON data that represented a set of posts to show up in the calendar:

<pre><code class="language-php">function edcal_postJSON($post) {
    setup_postdata($post);
    ?&gt;
    {
        "date" : "&lt;?php the_time('d') ?&gt;&lt;?php the_time('m') ?&gt;&lt;?php the_time('Y') ?&gt;",
        "title" : &lt;?php echo($this-&gt;edcal_json_encode(get_the_title())); ?&gt;,
        "author" : &lt;?php echo($this-&gt;edcal_json_encode(get_the_author())); ?&gt;
    },
    &lt;?php
}

function edcal_posts() {
    header("Content-Type: application/json");

    global $post;
    $args = array(
        'posts_per_page' =&gt; -1,
        'post_status' =&gt; "publish&amp;future&amp;draft",
        'post_parent' =&gt; null // any parent
    );

    $myposts = query_posts($args);

    ?&gt;[
        &lt;?php
        $size = sizeof($myposts);
        for($i = 0; $i &lt; $size; $i++) {
            $post = $myposts[$i];
            edcal_postJSON($post, $i &lt; $size - 1);
        }
    ?&gt; ]
    &lt;?php
}</code></pre>

I ran the code and everything worked. I was about to release the new version but ran my unit tests first to make sure. They failed. Can you spot the bug? I didn’t.

I was returning a JSON array, but the last item in the array had a trailing comma. That’s invalid JSON. Firefox accepts it, but Safari, Chrome and IE don’t. I almost shipped a broken plugin to over half of my users.

Now I run the unit tests on all major browsers whenever I release a new version. Any time WordPress releases a new version, I run the unit tests. WordPress 3.3 broke the calendar — and I found out exactly why in 15 seconds.</p>

## Popular Plugins Are Stable Plugins

Most WordPress plugins are free and open source, but free doesn’t always mean cheap. The <a href="https://en.wikipedia.org/wiki/Total_cost_of_ownership">total cost of ownership</a> of unstable plugins is more than people would pay. That’s a fancy way of saying that users will run from your plugin if it’s a bug fest.

My plugin became popular because of its features, but stability kept it popular. People remember one buggy release for a long time. If the Editorial Calendar deletes or corrupts posts from just one blog, thousands of people would stop using it. And they’d be justified.

Unit tests add the stability you need to support the multitude of browsers, mobile devices and dark corners involved in any JavaScript application. They’re easy to write, and they pay you back: because you find the bugs, and your users don’t.

{{< signature "al" >}}

